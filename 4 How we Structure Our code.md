Robot code tends to be big and without any means of organization, it becomes really hard to navigate. Take, for example, our team's 2026 code without any folders.

@todo screenshot of project without any folders >:)

Even though the code is already split into separate files, finding the file that you're looking for without folders is pretty annoying. But it could get so much worse if we were to combine all of the code into a single file. The resulting mess would make it impossible to find anything. As a result, trying to change anything is quite the chore. We can't have that. Instead, we use organization to make it easier to navigate projects, make small changes, and understand our code.

To help explain how our team's (3636) code is organized, I've made an interactive file tree from our 2026 code. Also don't worry if you don't understand every file yet. The purpose of this is to show where different kinds of code can be found.

**This version of our 2026 file tree has been updated to match the 2027 version of WPILib..**
>[!info]- This is used to represent a folder


>[!note]- This is used to represent a file 


>[!info]- `src/main/kotlin/com/frcteam3636/frc2026`
>>[!info]- `robot`
>>>[!note]- `Binding.kt`
>>>This file decides which buttons will run which commands. So, when a specific button, like `B`, is pressed, the robot will run a command like `autoAlign`. 
>>>
>>>We used to do this inside of `Robot.kt`, but that was already a big file. So every time we wanted to change a binding, we had to look through `Robot.kt`. This quickly became tedious, so instead we chose to make a separate file for them. 
>>
>>>[!note]- `Robot.kt`
>>>This file is where we set up the main `Robot` object. It's in charge of 
>>>- initializing subsystems
>>>- configuring logging (recording and saving information)
>>>- deciding which auto should be used based on user input 
>>>- setting up the dashboard
>>>- deciding what should be done when the robot is disabled
>>>- deciding what to do when entering disabled, autonomous, test, or teleoperated mode.
>>>- reporting diagnostics like CAN health.  
>>>
>>
>
>>[!info]- `mechanisms`
>>I'll get into mechanism later, but for now, all you need to know each one contains code to control a some part of the robot. 
>>
>>Each Mechanism is broken into two files
>>- An IO file responsible for communicating with the hardware 
>>- An 'Kt' that hold all of the logic that determines what the subsystem should be doing.
>>>[!info]- `drivetrain`
>>>
>>>>[!note]- `AbsolutePose.kt`
>>>>This helps the robot figure out its position on the field. This allows us to do things like auto-aim, auto-align, and accurate autos. 
>>>
>>>>[!note]- `Autos.kt`
>>>>This is where we create autos that the robot will run during the autonomous portion of a match.  
>>>
>>>>[!note]- `Drivetrain.kt`
>>>>This determines how the drivetrain subsystem should behave.
>>>
>>>>[!note]- `DrivetrainIO.kt`
>>>>This is responsible for communicating with the drivetrain's components.
>>>
>>>>[!note]- `Gyro.kt`
>>>>This is responsible for getting information from the gyro.
>>>
>>>>[!note]- `Module.kt`
>>>>This file contains code to control the swerve modules on our drivetrain.
>>>
>>>>[!note]- `PhoenixOdometryThread.kt`
>>>>This helps with reading sensor data.
>>>
>>>>[!note]- `TunerConstants.kt`
>>>>This file contains the constants that help our code accurately control the drivetrain.
>>
>>>[!info]- `feeder`
>>>The feeder subsystem is in charge of moving the game pieces from the indexer to our shooter. 
>>>>[!info]- `Feeder.kt`
>>>
>>>>[!info]- `FeederIO.kt`
>>>>
>>>
>>
>>>[!info]- `indexer`
>>>	When the intake picks up game pieces off the field, they're moved to a hopper. The indexer subsystem is responsible for moving the game pieces to the shooter.  
>>>>[!info]- `Indexer.kt`
>>>>
>>>>[!info]- `IndexerIO.kt`
>>>>
>>
>>>[!info]- `intake`
>>>This subsystem is in charge of moving the game pieces from the field into the hopper. 
>>>>[!info]- `Intake.kt`
>>>>
>>>
>>>>[!info]- `IntakeIO.kt`
>>>>
>>
>>>[!info]- `shooter`
>>>The shooter subsystem is in charge of shooting the game pieces. 
>>>
>>>Since the shooter has so many different moving parts that each need to move separately, we broke it into several smaller subsystems. 
>>>>[!info]- `flywheel`
>>>>The flywheel subsystem is in charge of launching the ball. We can vary the speed of the flywheel to change how fast the game piece leaves the shooter. 
>>>>>[!info]- `Flywheel.kt`
>>>>>
>>>>
>>>>>[!info]- `FlywheelIO.kt`
>>>>>
>>>>
>>>
>>>>[!info]- `hood`
>>>>The hood subsystem allows us to change the angle that the game piece leaves the shooter.
>>>>>[!info]- `Hood.kt`
>>>>>
>>>>
>>>>>[!info]- `HoodIO.kt`
>>>>>
>>>>
>>>
>>>>[!info]- `turret`
>>>>The turret subsystem is what allows our shooter to rotate. 
>>>>>[!info]- `Turret.kt`
>>>>>
>>>>
>>>>>[!info]- `TurretIO.kt`
>>>>T
>>>
>>>>[!note]- `ShooterLogic.kt` 
>>>>This file is in charge of getting the other mechanisms within `shooter` to work together to shoot the game piece.
>>>
>>
>
>>[!info]- `utils`
>> This folder contains reusable code that we've written to make our code easier to read and less repetitive.
>>>[!info]- `auto`
>>>
>>>>[!note]- `AutoUtils.kt`
>>>>This file contains utility code, such as `flipPath()`, that makes the main `Auto.kt` easier to read and write.
>>>
>>
>>>[!info]- `math`
>>>>[!note]- `Control.kt`
>>>>This file makes configuring things like PID and Feedforward a lot easier.  
>>>
>>>>[!note]- `Math.kt`
>>>> This file contains several math methods and classes that we use throughout the code, including `Vector2d`
>>>
>>>>[!note]- `PoseTransformation.kt`
>>>>This file allows us to flip `Pose2d`s and `Translation2d`s
>>>
>>>>[!note]- `Units.kt`
>>>>This file contains units, like meters, and functions for converting between units.
>>
>>>[!info]- `swerve`
>>>>[!note]- `Swerve.kt`
>>>>This file makes it easier to work with or pull information from swerve modules. 
>>>
>>
>>>[!note]- `CANUtils.kt`
>>>This file makes it easy to check our CAN bus cache status.
>>
>>>[!note]- `Input.kt`
>>>This file allows us to convert joystick inputs into a `Translation2d`.
>>
>>>[!note]- `LogTableUtils.kt`
>>>This file makes it easier to add and get values from NetworkTables.
>>
>
>>[!note]- `CAN.kt`
>>This is where we put all the CAN IDs of different components. 
>
>>[!note]- `Dashboard.kt`
>>This is where we set up the Dashboard to allow the driver to pick an auto to run.
>
>>[!note]- `Diagnostics.kt`
>>This file checks for any problems with the robot. If there is one, it will display an alert on the Driver Station.
>
>>[!note]- `Main.kt`
>> This is the first file that gets run. Inside it is where we create an instance of the robot and get the robot code running. 

