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

Note that nothing in our program is happening in *parallel*, we are simply hopping back and forth between different parts of our code to create the illusion of parallelization.

### Anatomy of a Command

Creating a command requires a lot of specialized syntax which may look foreign, or you might think it does something it doesn't. We'll start with the `run` command builder, creating a command which will spin the Intake motor.

```kotlin
// In subsystems/intake/Intake.kt
val intake = run({ coroutine ->
    io.intakeMotorVoltage(5.volts)
}).named("intake") 
```

Notice how the command is stored into a value `intake`. The most important thing to understand about commands is that functions like `run` **do not** actually run the command. Many times this has been a point of confusion and results in entire parts of the robot not functioning. Rather, these functions are command *builders*. They take some info and use it to build a `Command`, which can then be *triggered* later. In this particular example, we would attach the `intake` variable itself to a trigger, which we will learn how to do later in the chapter.

To understand how the `run` function actually works, it is important to know about an important feature of modern languages like Kotlin: *A function can be passed as an argument to another function.* Furthermore functions can also be defined inline, and this is called an anonymous function (or lambda, the terms mean about the same thing). To understand exactly what that means, let's look at a normal Kotlin function:

```kotlin
fun myFunction(param1: Int, param2: Double): String {
    ..
}
```

Now let's see the anonymous equivilant of this function:

```kotlin
takesAFunction({ param1, param2 -> .. })
```

This syntax is quite different, and should only be used as an argument to a function. Notice that you don't need to define the types of the parameters, because the function `takesAFunction` already defines the types it wants them to have. In the case of the `run` function before, one parameter is expected for the command, which we call `coroutine`. You'll see what `coroutine` can be used for in the future. After the arrow (`->`) the actual code in the function runs. 

### Different Command Types <span style="display:none">Run</span>

One of the simplest ways to make a command is with the `run` function. The code inside of run is what the command will execute when it's scheduled.

> [!info]- What do the `{}` mean

Sometimes we want to wait for a command to finish before continuing. For example, we don't want to spin the Intake's flywheels while it's not deployed. Instead, we should first ensure the Intake is meant to be deployed, then spin the intake motor once it has been deployed. Fortunately, we can do this with an `await()`

```kotlin
val intake = run({ coroutine -> 
    if(inputs.pivotSetpoint == Postion.Deployed.angle){
        coroutine!!.await(deployIntake)
        io.intakeMotorVoltage(5.volts)
    }
}).named("intake")
```

The `await()` pause the current coroutine until the command passed into is done. So, once `deployIntake` is done, the coroutine will resume and spin the Intake Motor.

It is nice to be able to run commands sequentially (in a sequence), but sometimes we need to run two commands at the same time. For example, intaking and spinning the indexer. To do this, we use `fork()` .

```kotlin
val intake = run({ coroutine -> 
    if(inputs.piviotSetPoint == Postion.Deployed.angle){
        coroutine!!.await(deployIntake)
        coroutine!!.fork(index)
        io.intakeMotorVoltage(5.volts)
    } 
}).named("intake")
```

The `fork` runs the passed command in the background, while the main one is running. However, if the main one, known as the parent, where to finish executing first, the forked command would be canceled.   

> [!info]- Another way to do this
> In WPILib, we can run two or more commands in parallel through the Parallel command. 
> 
> ```kotlin
>    val intakeSequence : Command? = Command.parallel(lowerIntake, intake)
> ```

If you want to guarantee both commands have ended, then use the `awaitAll`. Take, for example, if we wanted a command that would drive the robot to a point and deploy the intake at the same time.

```kotlin
val driveAndIntake = run({ coroutine -> 
    coroutine!!.awaitAll(deployIntake,driveToPoint)
    coroutine!!.await(intake)
})
```

The `intake` command won't start until both `deployIntake` and `driveToPoint` have ended.

How would `driveToPoint` work? After all, it's not a task that the robot can do instantly. It needs to continually update what the drive train is doing. On top of that, don't want to have to make a new command every time we drive to a new pose. 

Well, if we only cared about going to one point, then we could save the command as a `val` However, if we want to specify where the robot drive, we use a function like this:

```kotlin
// In subsystems/drivetrain/Drivetrain.kt
fun driveToPoint(point: Pose2d): Command? {
    return run({ coroutine -> 
        // ???
    })
}
```

But how could we make sure the command runs until the robot actually get to that point?  Well we can do that by using a `while` and `yield`. 

```kotlin
fun driveToPoint(point: Pose2d): Command? {
    return run({ coroutine -> 
        while (!autoPilot.atTarget(Drivetrain.estimatedPose, point)) {
            alignWithAutopilot()
            yield()
        }
    })
}
```

(alignWithAutopilot hides some of the more complex auto logic. We use a program called [Autopilot](https://therekrab.github.io/autopilot/) for that).

It's very important to reinforce that calling `driveToPoint` **will not** make the robot drive to a point. All this function does is build a `Command` with custom parameters (which is why we state that the function returns `Command?`). 

The `while` loop will continue to run until the robot is at the point where we want it. The `yield` passes control back to the scheduler, and allows the other commands in this robot loop to run. If we didn't do this, then no other commands could run at all.

### Race

There are time we when want two commands to run parallel, but once one ends both stop running. Like if the robot was driving towards a point  where we can no longer score. Once that happens, we want the robot to stop shooting. To make this happen can use `awaitAny`

```kotlin
val driveToPoseOneAndShoot = run { coroutine ->
   coroutine.awaitAny(
       shoot,
       driveToPoint(point1)
   )
}
```

Or:

```kotlin
val driveToPoseOneAndShoot = Command.race(shoot, driveToPoint(point1))
```

## Triggers

Now you know how to write a command, how do you actually get it to run? Because, remember, it won't run by calling the `run` function or any function that returns a `Command`. Well, one way is through something called a trigger. 

### What are Triggers?

Imagine your boss told you to watch the front door. Whenever someone walks through, you ring a bell. You aren't constantly ringing the bell, rather only when a person walks through the door.

Well triggers are similar. It watches a true or false condition, and then schedules a command based on how that condition has changed.

### Writing a Trigger

Let's say we want to automatically feed another game piece into our shooter after it finishes shooting. However, this can only happen if the robot actually has another game piece. 

```kotlin
val shouldFeed = Trigger ({
    shooter.hasGamePiece && intake.heldGamePieces > 0
}) 

// This has been simplfied 
```

The code inside of the `{}` is a lambda. In this case, `Trigger` is expecting the lambda to act as a `Supplier`. A `Supplier` is something that returns a value when it's run. Here, the `Supplier` gets used to tell the `Trigger` if the condition it's monitoring is true or false.  

Now we need to tell it what to run when the condition becomes true, and it would make sense that we run `feedIntoShooter` in that case.

```kotlin
shouldFeed.onTrue(feedIntoShooter)
```

Command Bindings

- `whileTrue`: Repeatedly runs a command when a trigger is `true`.

- `whileFalse`: Repeatedly runs a command when a trigger is `false`.

- `onFalse`: Run a command when a trigger changes from `true` to `false`.

- `toggleOnTrue`: When the trigger changes from `false` to `true`, runs the command if it isn't running, otherwise cancels it.

- `toggleOnFalse`: Same as `toggleOnTrue`, but when the trigger changes from `true` to `false`.

Combining Trigges 

- `and`: When both conditions are true, for example `shouldFeed.and(hasBalls)`.

- `or`: When either one or both of the conditions are true, for example `shouldFeed.or(shouldShoot)`.

Other Useful Methods

- `debounce`: Forces a trigger to remain in the same state for a certain amount of time after it changes to that state.

- `getAsBoolean`: Returns the trigger's state as a boolean.

### Using Controller Inputs

Now we have commands and triggers, but how does the driver tell the robot what to do? Inputs from controllers can be mapped directly to triggers. This allows the driver to schedule commands like `intake`, by simply pressing a button. And luckily for us, WPILib provides classes that make working with different controllers really easy.

#### Xbox, PlayStation, and other controllers

Making a controller object is really simple. All you have to do is provide which port the controller is assigned within Driver Station. 

If you don't know how to find that, or assiagn controllers to specific ports, then go through this slide show  @todo add the link to the DS slide show once finished.

We write all our bindings in the `robot/Bindings.kt` file inside a function called `configureBindings`. This function is then called from the `Robot` class during setup. 

```kotlin
// In robot/Bindings.kt
val xboxController = CommandNiDsXboxController(3)
val psController = CommandNiDsPS5Controller(4)
```

Once you've made your object, then you can start mapping commands to indivual buttons.

```kotlin
fun configureBindings() {
    psController.triangle().onTrue(intake)
    xboxController.x().onTrue(intake)
}
```

But buttons aren't the only inputs you can pull from the controller. After all, controllers have joysticks, which have a range of possible values that we can use. For example, if we wanted to allow the y axis (up and down) of the left joystick to control how fast a robot goes forward. Whereas, the x axis of the right joystick determines how much it should rotate.

```kotlin
val drive = run({ coroutine ->
   Drivetrain.arcadeDriveIK(psController.leftY, psController.rightX)
})
```

#### Joysticks

Joysticks are the cool things you may have seen our drivers using instead of a normal controller. Creating a joystick object is just as easy as any other controller : 

```kotlin
val joystick = CommandJoystick(1)
```

However, mapping commands to buttons works a bit differently. Instead of having a method for each button like `xboxController.x()`, the `button()` method take a number corresponding to a specific button 

```kotlin
fun configureBindings() {
    joystick.button(1).whileTrue(shoot)
}
```

What happen if try to run two commands at once/ ownership.
