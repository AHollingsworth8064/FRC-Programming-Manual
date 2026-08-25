## What are Commands 
On our team, we use commands to control the robot. A command is a task the robot can perform. These commands can be anything as simple as spinning an intake to something as complex as automatically aiming a shooter. 

Commands don't run by themselves; instead, something called the scheduler manages them. The scheduler is responsible for keeping track of which commands need to be run each robot loop and running them. 

Since the scheduler handles the commands, we can just focus on writing code that describes how the robot can behave. It also allows us to keep our code organized and easy to read by breaking down complex behaviors into smaller commands that we can reuse later by itself or as a part of a larger command. 
## Commands V3
In 2027, WPILib released a new version for commands. This new version uses coroutines, but what are coroutines?
### What are Coroutines
Coroutines are blocks of code that can be paused. Normally, once you've called a function, the code would not run anything else until the function is finished. However, with coroutines, we can pause that function, and let another one run. Then we can resume the first one. 

Let's say you're making a cake, and you're following the instructions below.
- `Grab supplies`
- `Set temperature for preheat` 
- `wait until it's finished preheating `
- `Mix batter`
- `Put cake in oven ``
- `wait until it's finished cooking`
- `make frosting`
- `apply frosting`
If these were normal functions, we would spend time waiting for the oven to preheat.  Once that's done, only then we could move on to mixing the batter. Similarly, we couldn't make frosting until the cake finished cooking.

With coroutines, we wouldn't have to spend time waiting. Instead, we could just pause the coroutine responsible for waiting until the oven is preheated. Then we could mix the batter before resuming waiting. Similarly, we could pause waiting for cake for 10 minutes, and make the frosting instead. This lets us make progress on other work instead of sitting idle while we're waiting.

### Different Command Types 
#### <span style="display:none">Run</span>
One of the simplest ways to make a command is with run. The code inside of run is what the command will execute when it's scheduled.
```Kotlin 
val intake : Command? = run ({//The run method is from the mechanism class 
	coroutine -> {//the stuff here is what will be run.
		io.intakeMotorVoltage(5.volts)
	}
}).named("intake")//WPILib requries us to name all commands like this
```
Above, we're making a new command that will spin the Intake's flywheel once it get's scheduled.  

>[!info]- What do the `{}` mean

Sometimes we want to wait for a command to finish before continuing. For example, we don't want to spin the Intake's flywheels while it's not deployed. Instead, we should first ensure the Intake is meant to be deployed, then spin the intake motor once it has been deployed. Fortunately, we can do this with an `await()`
#### <span style="display:none">Sequence</span>
```Kotlin
val intake : Command? = run({
	coroutine -> {
		if(inputs.pivotSetpoint == Postion.Deployed.angle){
			coroutine!!.await(deployIntake)
			io.intakeMotorVoltage(5.volts)
		} 
	}
}).named("intake")
```
The `await()` pause the current coroutine until the command passed into is done. So, once `deployIntake` is done, the coroutine will resume and spin the Intake Motor.
#### <span style="display:none">Parallel</span>
It is nice to be able to run commands sequentially (in a sequence), but sometimes we need to run two commands at the same time. For example, intaking and spinning the indexer. To do this, we use `fork()` .
```Kotlin
val intake : Command? = run({
	coroutine -> {
		if(inputs.piviotSetPoint == Postion.Deployed.angle){
			coroutine!!.await(deployIntake)
			coroutine!!.fork(index)
			io.intakeMotorVoltage(5.volts)
		} 
	}
}).named("intake")
```
The `fork` runs the passed command in the background, while the main one is running. However, if the main one, known as the parent, where to finish executing first, the forked command would be canceled.   

>[!info]- Another way to do this
>In WPILib, we can run two or more commands in parallel through the Parallel command. 
>```kotlin 
>	val intakeSequence : Command? = Command.parallel(lowerIntake, intake)
>```

If you want to guarantee both commands have ended, then use the `awaitAll`. Take, for example, if we wanted a command that would drive the robot to a point and deploy the intake at the same time.
```Kotlin
val driveAndIntake : Command? = run({
	coroutine -> {
		coroutine!!.awaitAll(deployIntake,driveToPoint)
		coroutine!!.await(intake)
	}
})
```
The `intake` command won't start until both `deployIntake` and `driveToPoint` have ended.
#### <span style="display:none">Until</span>

How would `driveToPoint` work? After all, it's not a task that the robot can do instantly. It needs to continually update what the drive train is doing. On top of that, don't want to have to make a new command every time we drive to a new pose. 

Well, if we only cared about going to one point, then we could save the command as a `val` However, if we want to specify where the robot drive, we use a function like this:

```Kotlin
fun driveToPoint(point : Pose2d) : Command?{
	return run({
		coroutine -> {
			
		}
	})
}
```
But how could we make sure the command runs until the robot actually get to that point?  Well we can do that by using a `while` and `yield`. 

```Kotlin
fun driveToPoint(point : Pose2d) : Command?{
	return run({
		coroutine -> {
			while(!autoPilot.atTarget(Drivetrain.estimatedPose, point)){
				alignWithAutopilot()
				yield()
			}
		}
	})
}
//To keep this simple, I've replaced the logic with the alignWithAutopiolot
//Auto Pilot is a libary that we've recently started using for autos
//You can find it's documentation at https://therekrab.github.io/autopilot/
```
The `while` loop will continue to run until the robot is at the point where we want it. The `yield` passes control back to the scheduler, and allows the other commands in this robot loop to run. If we didn't do this, then no other commands could run at all.

>[!info]- Race
>There are time we when want two commands to run parallel, but once one ends both stop running. Like if the robot was driving towards a point  where we can no longer score. Once that happens, we want the robot to stop shooting. To make this happen can use `awaitAny`
>```Kotlin
>val driveToPoseOneAndShoot : Command? = run{
>	coroutine ->{
>		coroutine.awaitAny(
>			shoot,
>			driveToPoint(point1)
>		)
>	}
>}
>```
>>[!info]- Another way to do this 
>>```Kotlin
>>val driveToPoseOneAndShoot = Command.race(shoot, driveToPoint(point1))
>>```
#### <span style="display:none">Race</span>

## Triggers 
Now you know how to write a command, how do you actually get it to run? Well, one way is through something called a trigger. 

### What are Triggers 
Imagine your boss told you to watch the front door. Whenever someone walks through, you ring a bell. You aren't constantly ringing the bell, rather only when a person walks through the door.

Well triggers are similar. It watches a true or false condition, and then schedules a command based on how that condition has changed.

### Writing a Trigger 
Let's say we want to automatically feed another game piece into our shooter after it finishes shooting. However, this can only happen if the robot actually has another game piece. 

```Kotlin
val shouldFeed = Trigger ({
	(shooter.hasGamePiece && intake.heldGamePieces > 0)
}) 

//This has been simplfied 
```
- The stuff inside of the `{}` is a lambda. In this case, `Trigger` is expecting the lambda to act as a `Supplier`. A `Supplier` is something that returns a value when it's run. Here, the `Supplier` gets used to tell the Trigger if the condition it's monitoring is true or false.  
 
Now we need to tell it what to run when the condition becomes true.
```Kotlin
shouldFeed.onTrue(feedIntoShooter)
//this will run once when shouldFeed's condition becomes true.
```
>[!info]- Command Bindings
>- `whileTrue`
>- `onFalse`
>- `whileFale`
>- `toggleOnTrue`
>- `toggleOnFalse`

>[!info]- Combining Trigges 
>- `and`
>- `or`

>[!info]- Other Useful Methods
>-`debounce` 
>`getAsBoolean` 
### Using Controller Inputs
Now we have commands and triggers, but how does the driver tell the robot what to do? Well we can map inputs, such as button presses, from a controller to triggers.  This allows the driver to schedule commands, such as intake, by just pressing a button. And luckily for us, WPILib provides classes that make working with different controllers really easy.
 

>[!info]- Xbox, PlayStation, and other controllers
>Making a controller object is really simple. All you have to do is provide which port the controller is assigned within Driver Station. 
>
>If you don't know how to find that, or assiagn controllers to specific ports, then go through this slide show  @todo add the link to the DS slide show once finished
>```Kotlin
>val xboxController = CommandNiDsXboxController(3)
>val psController = CommandNiDsPS5Controller(4)
>```
>
>Once you've made your object, then you can start mapping commands to indivual buttons.
>```Kotlin
>psController.triangle().onTrue(intake)
>xboxController.x().onTrue(intake)
>```
>
>But buttons aren't the only inputs you can pull from the controller. After all, controllers have joysticks, which have a range of possible values that we can use. For example, if we wanted to allow the y axis (up and down) of the left joystick to control how fast a robot goes forward. Whereas, the x axis of the right joystick determines how much it should rotate.
>  
>```Kotlin
>//This is a simiplfied exmaple
>val drive : Command? = run({
>	Drivetrain.arcadeDriveIK(psController.leftY, psController.rightX)
>	//not an actual method 
>})
>```

>[!info]-  Joysticks
>Creating a joystick object is just as easy as any other controller : 
>```Kotlin
>val joystick = CommandJoystick(1)
>```
>
>However, mapping commands to buttons works a bit differently. Instead of having a method for each button like `xboxController.x()`, the `button()` method take a number corresponding to a specific button 
>```Kotlin
>joystick.button(1).whileTrue(shoot)
>```
>
>Since a `CommandJoystick` has a single stick, we can also get the stick's position along the X-axis using `joystick.x`.
>


%%
Commands v3 

What are commands 

What are corutintines and why we use them 

1) Types of commands ve
	1) Parrell
	2) Race 
	3) Run, end 
	4) start, run, end
	5) ect
2) Trigers/ running them 
	1) What are triggers 
	2) Mapping commands to conroler input

What happen if try to run two commands at once/ ownership.

