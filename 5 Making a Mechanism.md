## What is a Mechanism
On a robot, there are so many different components and each of them requires its own code. Take a look at some of the components we used in 2026. 
```
frontLeftDriveMotor 
frontRightDriveMotor 
rearLeftDriveMotor 
rearRightDriveMotor 

frontLeftTurningMotor 
frontRightTurningMotor 
rearLeftTurningMotor 
rearRightTurningMotor 

leftIntakeMotor 
intakePivotMotor 

indexerMotor 

feederMotor 
flywheelMotor 
hoodMotor 
turretMotor 

gyro
leftLimelight 
rightLimelight

 
```
Even just looking at this list makes my eyes blur. If we were to write code for each without any organization, it would quickly become a mess. Instead, we grouped related components together and controlled them with a mechanism. 

A mechanisms is code that manages and/or controls a group of related components that work together to complete a task. With it, our code won't have to manage each component individually. Instead, it can control the intake mechanism instead.

Take our 2026 intake mechanism as an example. 

@todo add photo

It's composed of two motors that work together to pick up and bring game pieces into the robot. Since they work together to bring game pieces into the robot, we control them with a single mechanism.  As a result, the rest of the code can work with the intake mechanism instead of both motors individually. 

## IO vs Mechaism files
Although a mechanism seems like one piece of code, it actually has two different responsibilities: communicating with the components and deciding what the mechanisms should do.  While one file could be used for both jobs, it would make the code harder to read. Instead, we separate the responsibilities into an IO file and what we call a Kt file. 

<details> Two Extra Benefits
	<summary>
	>- It makes it a lot easier to use AdvantageKit for logging and replaying matches 
	>- It makes simulating our robot a lot easier.
	</summary>
</details>
The IO file is responsible for communicating with the components themselves. This means it tells them what to do and receives information about the component's current state, such as motor speed, motor position, etc.

The Kt file is responsible for deciding what the mechanism should be doing. For example, let's say you pressed a button on a controller. The Kt file is the one that processes that input, and uses it to decide that the robot should raise its intake. To make this happen, the Kt file passes on the instructions about how the components should be have to the IO. Then the IO, passes on those instructions to the induvial components. 

### What I Mean by "IO File" and "KT File"
I've been referring to `IO` files and `Kt` files, but they aren't a special file type. Instead, they're just the names we use for the two files that make up a mechanism. 

```
intake
	-Intake.kt // this is the Kt file
	-IntakeIO.kt // this is the IO file
```

## Example IO 
Now you know what an IO file is, let's take a look at one. I'm going to walk you through what one looks like and explain the important parts.

```Kotlin
@Logged 
open class IntakeInputs { 
// The open means this class can be inhertited. It's required for logging
    var intakeMotorVelocity = 0.rotationsPerSecond
    var intakeMotorCurrent = Amps.zero()!!
    var pivotAngle = 0.degrees
    var pivotSetpoint = 0.degrees
    var intakePivotMotorCurrent = Amps.zero()!!
    var intakePivotMotorVoltage = Volts.zero()!!
    var intakePivotMotorSupplyVoltage = 0.0.volts
    var rightPivotMotorCurrent = Amps.zero()!!
}
```
At the start of every IO file, we have an `Inputs` class. It is responsible for holding important data about the mechanism, such as the current state of our components or other data we want to log. Since all of the mechanism's data is stored in one place, this makes it much easier to log the information.

```Kotlin
interface IntakeIO {
    fun setSpeed(percent: Double)
    fun setPivotVoltage(voltage: Voltage)
    fun setPivotSpeed(pivot: Double)
    fun setWheelMotorVoltage(voltage: Voltage)
    fun setPivotAngle(angle: Angle)
    fun updateInputs(inputs: IntakeInputs)
    fun zeroEncoder()
}
```

Sometimes when we need to test our code, we don't have the robot. So, instead we use a simulated robot. But the simulated robot doesn't have any physical hardware, so the `IntakeIOReal` won't work. Instead, we need to make another `IO` to allow our robot code to communicate with the simulated robot. However, we don't want the code inside of the `Kt` file to change just because we're simulating our robot. To solve this, we make an interface with the methods we want all of the `IO` classes to have. Then we make both classes implement it. This means both IO classes will have the same methods even if their code is different. This means the code inside of the `Kt` file can use either without caring if the robot is real or simulated.

<details> What are interfaces 
	<summary>
	An interface is like a class, except it typically only has methods. The methods themselves don't contain code. Instead, each class that implements them provides the code for its version. 
	
	Think of an interface as a job description. Two people might have the same job description, but they go about doing their jobs in a completely different way. The job description still applies to them both, they're just doing their jobs differently. In the same way, two classes can implement the same interface but using different code. 
	</summary>
	
</details>
```Kotlin
class IntakeIOReal : IntakeIO {
	//IntakeIOReal : IntakeIO, means it's implementing IntakeIO 
    companion object Constants {
        val PID_GAINS = PIDGains(120.0, 0.0, 0.5)
        val PROFILE_CRUISE_VELOCITY = 320.0.degreesPerSecond
        val PROFILE_ACCELERATION = 400.degreesPerSecondPerSecond
        val PROFILE_JERK = 20.0
        val ENCODER_TO_PIVOT_GEAR_RATIO = 32.0 / 12.0
        val MOTOR_TO_ENCODER_GEAR_RATIO = 4.0
        val DISCONTINUITY_POINT = 0.999
        val MAGNET_OFFSET = 0.130859375
        val GRAVITY_COMPENSATION_GAIN = 1.0

        val PIVOT_MOTOR_DIRECTION = InvertedValue.CounterClockwise_Positive
        val WHEEL_MOTOR_DIRECTION = InvertedValue.CounterClockwise_Positive
    }
```
You don't have to understand everything you see in the `Constants` object.

When writing code there are times we have to use some fixed value. While we could just write them directly into the code, someone reading it later would have no idea what the number represents nor why it was chosen. These unexplained values are known as magic numbers.

To avoid situations with magic numbers, we store those values in constants. Then our team stores these constants in a companion object, since we find it makes updating, understanding, and/or checking constants far easier.

>[!info]- What is a Companion Object
>Companion objects belong to the class rather than an instance of one. This means every object created from the class has access to this one shared companion object, its values, and it methods.

```Kotlin
    private val intakePivotMotor = TalonFX(CTREDeviceId.IntakePivotMotor)
	//I removed the configuration for the piviot motor since it contained 
	//more advanced topics i'll cover later. 
    private val intakeMotor = TalonFX(CTREDeviceId.IntakeMotor)
    .apply {
        configurator.apply(TalonFXConfiguration().apply {
		         MotorOutput.Inverted = WHEEL_MOTOR_DIRECTION
		        MotorOutput.NeutralMode = NeutralModeValue.Coast
	         }
         )
    }

    private val encoder =  CANcoder(CTREDeviceId.IntakePivotEncoder).apply{
        configurator.apply(CANcoderConfiguration().apply {
            MagnetSensor.SensorDirection = 
			SensorDirectionValue.Clockwise_Positive
        })
        setPosition(0.degrees)
    }
```

Just because we have hardware, it doesn't mean our code can communicate with them just yet. First we have to create an object that will interact with the hardware. Luckily, the companies that make FRC hardware already provide the code needed to communicate with it. So all we have to do is configure the the object and add it in to our code. 

-`TalonFX(CTREDeviceId.IntakeMotor)`, 
This creates a new motor object with the CAN ID stored in `IntakeMotor`. Whenever adding code for a new piece of hardware, you always add its CAN ID to Enum in the CAN file

- `MotorOutput.Inverted = WHEEL_MOTOR_DIRECTION`
Sometimes a motors spins in the opposite direction to what we want. To fix that we can configure if the motor direction get inverted. 

- `MotorOutput.NeutralMode = NeutralModeValue.Coast` 
This tells the motor that it can spin freely when it has no instructions. If you want it to stop moving instead, you can use `NeutralModeValue.Brake`


>[!info]- `.apply`
>After creating a motor object, most of the time we need to configure it. Kotlin's `.apply` make this a bit easier since we no longer need to refer back to the object that we just created several times. 
>
>Take this one for example. Instead of writing this : 
>```Kotlin
>private val intakeMotor = TaflonFX(CTREDeviceID.IntakeMotor)
>private val intakeMotorConfiguration = TalonFXConfiguration()
>
>init{
>	intakeMotorConfiguration.MotorOutput.Inverted = WHEEL_MOTOR_DIRECTION
>	intakeMotorConfiguration.MotorOutput.NeutralMode = NeutralModeValue.Coast
>	
>	intakeMotor.configurator.apply(intakeMotorConfiguration)
>}
>Like this:
> private val intakeMotor = TalonFX(CTREDeviceId.IntakeMotor)
>    .apply {
>	configurator.apply(TalonFXConfiguration().apply {
>		         MotorOutput.Inverted = WHEEL_MOTOR_DIRECTION
>		        MotorOutput.NeutralMode = NeutralModeValue.Coast
>	         }
>	)
> }
>```
> Now we no longer need a method for configurating the motor. Instead all of that happens when the motor object gets created. On top of that we don't need to use `intakeMotorConfiguration` repeatedly and we don't need a separate variable for storing the configuration. 
> 
>[If you want a more in-depth explanation, here is a good resource ](https://medium.com/@sujathamudadla1213/explain-the-apply-function-in-kotlin-with-example-b56d4f41fd51)
----------------------
```Kotlin
    override fun setSpeed(percent: Double) {
        intakeMotor.set(percent)
        //Tells the motor to spin a `percent` of it's max speed
    }

    override fun setPivotSpeed(pivot: Double) {
        intakePivotMotor.set(pivot)
        //This sets 
    }

```
These two methods tell the motors to try to a certain percentage of its max speed. So, if I were to do this `setSpeed(50%)`, the motor would try to spin at 50% of its max speed.


```Kotlin

    override fun setPivotVoltage(voltage: Voltage) {
        Logger.recordOutput("Intake/Pivot Attempted Voltage", voltage)
        intakePivotMotor.setVoltage(voltage.inVolts())
    }
    
    override fun setWheelMotorVoltage(voltage: Voltage) {
        intakeMotor.setVoltage(voltage.inVolts())
    }

```
This allows us to control how much voltage should be supplied to the motor. If a negative voltage is passed, then the motor spin `backwards`. This is why we tend to use this method over `setSpeed` when we don't need exact speeds.

```Kotlin
    override fun zeroEncoder() {
        encoder.setPosition(0.degrees)
    }
```
Sometime when we start the robot, the pivot is not in the right position. However, the encoder doesn't know that, instead it just assumes that it in the zero position. As a result, all of the encoders values are off which can lead to the pivot trying get to an angle outside of its range. However, by running this method, we can set where the encoder thinks the zero position is; thus, we can ensure the encoder gives us proper values and that the code does what we want. 

```Kotlin
    private val positionControl = MotionMagicVoltage(0.0)
    
    override fun setPivotAngle(angle: Angle) {
        Logger.recordOutput("Intake/Pivot Setpoint", angle)
        intakePivotMotor.setControl(
            positionControl.withPosition(angle)
//                .withFeedForward(sin(encoder.position.value.inRadians()) * GRAVITY_COMPENSATION_GAIN)
        )
    }

    var setpoint = 0.degrees
```
You don't have to understand how this works quite yet since this covered in Control Systems. All you need to know is this is how we get the pivot to go to specific angles.

```Kotlin
    override fun updateInputs(inputs: IntakeInputs) {
        inputs.intakeMotorVelocity = intakeMotor.velocity.value
        inputs.intakeMotorCurrent = intakeMotor.supplyCurrent.value

        inputs.intakePivotMotorCurrent = intakePivotMotor.supplyCurrent.value
        inputs.intakePivotMotorVoltage = intakePivotMotor.motorVoltage.value
        inputs.intakePivotMotorSupplyVoltage = intakeMotor.supplyVoltage.value
//        inputs.rightPivotMotorCurrent = rightPivotMotor.supplyCurrent.value
        inputs.pivotAngle = intakePivotMotor.position.value
        inputs.pivotSetpoint = setpoint
    }
}
```
This is how we get data from the motors and encoders and then store them in the `IntakeInputs`. 



--- 
I won't go into much detail about sim here, but keep in mind not all mechanisms need sim. Generally, sim is something we do if we finished coding our mechanism before we are able  work with the physical robot. Additionality, sometimes the library we use for sim doesn't have one to one matches for things like `setSpeed`. Instead, we try to get it as similar to the `RealIO`'s behavior.


```Kotlin 
class IntakeIOSim: IntakeIO {  
    var pivotStored = false  
    var pivotSetPoint = 0.degrees  
    val intakeSimulation = IntakeSimulation.OverTheBumperIntake(  
        "Fuel",  
        Drivetrain.getSwerveDriveSimulation(),  
        Drivetrain.Constants.BUMPER_WIDTH,  
        0.182.meters,  
        IntakeSimulation.IntakeSide.BACK,  
        40  
    )!!  
  
    fun setRunning(runIntake: Boolean) {  
        if (runIntake) {  
            intakeSimulation.startIntake()  
        } else {  
            intakeSimulation.stopIntake()  
        }  
    }  
  
    val isFuelInsideIntake: Boolean  
        get() {  
            return intakeSimulation.gamePiecesAmount != 0  
        }  
  
    override fun setSpeed(percent: Double) {  
        setRunning(percent > 0)  
    }  
  
    override fun setPivotVoltage(voltage: Voltage) {  
        pivotStored = voltage > 0.volts  
    }  
  
    override fun setPivotSpeed(pivot: Double) {  
	    pivotStored = pivot > 0
    }  
  
    override fun setWheelMotorVoltage(voltage: Voltage) {  
        setRunning(voltage > 0.volts)  
        //Since the library we're using doesn't let us spin the intake motor 
        //backwards I chose to skip the outtake behavior    }  
  
    override fun setPivotAngle(angle: Angle) {  
        pivotStored = abs((angle - Intake.Position.Deployed.angle).inDegrees()) > 1  
        pivotSetPoint = angle  
    }  
  
    override fun updateInputs(inputs: IntakeInputs) {  
        inputs.pivotAngle = if(!pivotStored) Intake.Position.Deployed.angle else Intake.Position.Stowed.angle  
        inputs.pivotSetpoint = pivotSetPoint  
  
        Logger.recordOutput("FieldSimulation/Stored", pivotStored)  
        Logger.recordOutput("FieldSimulation/NumberOfFuel", intakeSimulation.gamePiecesAmount)  
  
    }  
  
    override fun zeroEncoder() {  
        return ;  
        //Since we don't have a simulated encoder, there is nothing we can do about this.  
    }  
}
```



