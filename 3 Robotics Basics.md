## Safety 
Before we can get to writing for the robot, we need to talk about safety. After all, you'll be testing code on a heavy and powerful robot that could easily hurt someone or damage something. Even experienced programmers can make mistakes, which is why you should always pay attention to what the robot is doing. 

Most of the time, the robot is perfectly safe to work around. However, accidents can happen and sometimes people can be careless. So there are a few things to keep in mind whenever you're working with the robot.

- Before **enabling** the robot (allowing it to run code), say **enabling** loud enough that those nearby know the robot could move at any moment 
- If someone is working on the robot and/or trying to diagnose a mechanical error, do not enable the robot unless they tell you to. 
- Whenever letting an inexperienced person drive, always cap the robot's speed
- Whenever testing autos (code that runs without human input), be prepared to disable the robot to stop it.
- If you hear a grinding noise coming from the robot, stop testing and get someone from your Fabrication subteam (someone who assembles the robot)
- Never assume the robot is disabled
- Never put your hands into the robot when it's enabled
- Wear proper PPE whenever the situation requires.


## Robot Components 
Quick disclaimer, this won't include anything about pneumatics as my team don't use them 

>[!info]- Drivetrains
>In FRC there are several different types of drivetrains, but most can be sorted into either:
>>[!info]-  Swerve
>>@todo add photo 
>>A swerve drive is typically made up of 4 different modules at each corner of the robot.  They are able to move independently of each other.
>>
>>@todo insert photo here of swerve chassis 
>>
>>In each module there are two motors: one for spinning the wheel (the drive motor) and one for changing the direction the wheel is facing (the turning motor)
>>@todo insert photo with labeled motor
>>Since the driving motor moves independently from the turning motor, we can control each wheel's speed and direction independently. As a result, the robot drive in any direction and rotate simultaneously, making it really maneuverable. However, they are quite  expensive and harder to program.  
>
>>[!info]-  Tank
>>Tank drive has wheels on the left and right sides of the robot. The robot turns by driving one side faster than the other.
>>@todo add photo 
>>Compared to swerve, this is far cheaper and easier to program, but has less maneuverability 

>[!info]- Motors
>Motors are what allow things on the robot to move. Whether it's driving or launching a game piece, there is a motor that converts electricity from the battery into motion.
>
>There are two types of motors that we could use, brushed and brushless; however, most modern teams use brushless since they tend to be better. If you want to know more about the advantages of brushless, [here is a Chief Delphi thread talking about it](https://www.chiefdelphi.com/t/brushed-v-brushless-motors/372876/4).
>
>If you want to know more about the differences between brushless and brushed motors, [then take a look at this](https://www.monolithicpower.com/en/learning/resources/brushless-vs-brushed-dc-motors)

>[!info]- Motor Controllers 
>When we want to control a motor, we don't send the instructions directly to the motor. Instead, we send them to a motor controller. Then the motor controller uses those directions to control the motor. 

>[!info]- Encoders
>Imagine you're making an elevator. How would you go about making sure it arrives to the right elevation? 
>
>One way we can do it is by measuring how many times it has rotated. To do this, we use something called an encoder. Encoders are sensors that monitor the rotation speed and rotation of a motor.

>[!info]- Cameras 
>In FRC, there are these things called April Tags. There are several placed around the field and each act as a sort of QR codes that help the robots know where they are on the field.  By adding cameras, we allow our robot to see the April Tags and estimate where the robot is on the field.
>
>The two of the most common vision systems used in FRC are:
>- Limelight makes their own cameras with closed source software. Additionally, they are pretty easy to set up, have a pretty good GUI, and have code available to make incorporating into code pretty easy.  However, they are expensive and you're quite limited by the hardware you can use with it. 
>
>- PhotonVision is an open-source software that allows the user to decide what hardware they want to use. As a result, you only need to purchase compatible hardware such as a coprocessor and camera. However, it is more annoying to set up. 

>[!info]- Gyro
>By itself, the robot has no means of knowing which way it's facing. Without that information, we can't do things like auto-align or auto-aim. To fix that, we add a gyro which keeps track of how much the robot has rotated, allowing it to determine which way it's facing.

>[!info]- RoboRIO and System Core
>System Core is the brain of the robot. It runs the robot's code, processes information from the robot's sensors, and controls the robot's other components.
>
>>[!info]- RoboRIO
>>Before 2027, FRC robot used something called the roboRIO. It served the same purpose as System Core, but was much more limited and slower. This is why if you look at older FRC resources you might see them mention a roboRIO.

>[!info]- Radio
>The radio is what allows us to connect to the robot wirelessly. This lets us deploy code (sending code to the robot), control the robot, and receive information from the robot without using any extra wires.

>[!info]- Power Distribution Hub 
>The Power Distribution Hub, or PDH for short, is what sends power from the robot's battery to the robot's electrical components. 

>[!info]- Main Breaker
>The Main Breaker is the robot's power switch. This makes it really easy to turn the robot on and off.

>[!info]- Robot Signal Lights (RSL)
>RSL (Robot Signal Light) lets us quickly tell whether the robot is enabled or disabled without needing to check the Driver Station (the computer connected to the robot). Whenever a RSL is flashing, the robot is enabled. If the RSL is solid, then the robot is disabled.


## CAN 
If System Core is the brain of the robot, then the CAN is the nervous system. It's responsible for carrying messages between the System Core and the robot's components.

Instead of each component being individually attached to the System Core, CAN uses a chain of components wired together. 

For each component on the CAN chain, we must assign it a CAN ID. Once that's done, System Core will be able to communicate with the component by sending out a message with the CAN ID attached. Then each component on the CAN chain will look at the ID to see if it matches its own. If so, the component will follow the message's instructions. 

@todo  link to the indepth slideshow from the chickens

## Battery Voltage

For the robot to move around, it requires an energy source. In FRC, we use 12-volt batteries. However, they don't last forever, so it's really important to keep an eye on the battery's voltage. If it were to drop too low, the robot's performance may start to decline and may eventually shut down. 

### Brownout 
If the robot's voltage drops below a certain threshold (the default is 6.3 volts), the robot will enter brownout protection. During this time, System Core will disable all outputs. As a result, the robot will become unresponsive. When this happens, the RSL will turn amber and your Driver Station will say brownout. 

If you want to know the specifics of what happens during a brownout, [check out WPILib's documentation  ](https://docs.wpilib.org/en/stable/docs/software/roborio-info/roborio-brownouts.html).

### Where to Check Battery Voltage 
You can view the battery's current voltage by looking at the Driver Station.

@todo add photo

### When to Switch Batteries
There are a few things that indicate when you should switch a battery when testing the robot.
- If the battery voltage indicator on the Driver Station has some red parts 
- If the battery voltage is approaching 10.5 volts while moving the robot 

## Connecting to the Robot 
### Over Wi-Fi 
You can connect to the robot via Wi-Fi if it's enabled. The best way to find out if it's on is to ask your programming lead or another more senior member of the team. If it is enabled, then 
1) Turn on the robot
2) Look for the robot's Wi-Fi (Ask another member if you don't know)
3) Connect to it

### Tethering 
If you take a look at the radio, you should see an Ethernet port labeled DS. 
@todo get photo
All you need to do is plug an Ethernet cable into the DS port, then plug the other end into your computer. 

## Deploying Code 
Once you've finished writing robot code, you need a way to transfer it to the robot. In FRC, we do this through a process known as deploying. But, before we can deploy code to the robot, make sure you either connected to the robots Wi-Fi or tethered to it. I personally recommend tethering as it's a lot faster.




### Installing WPILib
If you haven't installed WPILib, then follow this [guide](@todo). It will help you install WPILib and get it working with IntelliJ. 

### Deploying your Code 
Before you deploy your code, take sure of a few things:
- Make sure the robot is on 
- Make sure you're connected to the robot 


@todo slide show with visual how to deploy

## Robot Modes
Depending on what we're doing, we might want the robot to behave differently. Sometimes we want the robot to be controlled by the driver. Other times, we might want the robot to move on its own. In FRC, we accomplish this through robot modes.

There are four important robot states that you'll encounter:
- Disabled, where the robot doesn't accept user inputs and won't move any components.
- Auto (autonomous), where the robot doesn't accept user inputs, but follows a pre-programmed routine.
- Teleop (Teleoperated), where the robot can receive user inputs and acts accordingly.
- E-Stopped (Emergency Stop). This state is practically the same as Disabled, however the robot can't be reenabled afterwards.

There is also test mode, but our team doesn't really use it. 

## Driver Station
Once we've deployed code on the robot, we need a way to communicate with the robot. Without that, we won't be able to disable or enable the robot, change which mode it's in, or send the driver's inputs.


### What is Driver Station
Driver Station is a tool used in FRC that allows us to pass the driver's joystick and controller inputs to the robot, lets us view important robot information such as error messages and battery voltage, and lets us control the robot's current state.

### Navigating the Driver Station 
@todo on the plan e

>[!info]- Download 
>@todo, when there is an official non alpha version download. 

## Robot Loops 
Robot code doesn't just run once and then stop. After all, the robot's inputs are constantly changing. This requires the code to repeatedly check its inputs, control its components, and perform other tasks. This is why the robot code runs in a continuous loop called the robot loop. A new robot loop typically begins every 20ms. However, if the code inside the loop takes too long to run, the next loop will start later than expected. We call this a loop overrun.

## NetworkTables
Our code often requires several different programs to communicate with each other. For example, the robot needs to know which AprilTags our Limelights see and the Driver Station needs to know the robot's battery voltage. But how do these things share this information between each other? Well, it's through something called NetworkTables. 

NetworkTables are like a shared location on the robot's network where programs can connect and exchange information. Instead of sending information directly to each other, each program writes and updates information on the NetworkTables. Then, other programs can access the information stored there.

### Topic
A topic is similar to a variable. It has a name and stores a single value, like battery voltage. Unlike normal variables, topics can be shared across several programs. Take the following topics for example.

@todo, add code examples
```Kotlin


// Making a topic for voltage 

//Make a topic for robot states.
```
Each of these creates a new topic that can store a single value. But as code grows, a lot more topics will be created.  

@todo add actual example of too many 
```Koltlin 
/robotBatteryVoltage
/robotPose
/robotMode

/leftLimelightAprilTagsSeen
/leftLimelightHB 

 
```
Without some way to organize them, finding the topic you're looking for can quickly become difficult. To solve this, topics are organized into a hierarchy, similar to folders on your computer.

@todo add actual examples for this 
```
/Robot 
	-/BatteryVoltage
	-/Heading 
	-/Pose
	-/Ect
```

@todo finish this 
So the full name of //example batteryVoltage would be /Robot/BatteryVoltage


Actually doing this in code is really easy. You just do this.

@todo add actual examples. Take a look at the object detection code for a good example
```Kotlin

//this is bs/ filler
NT.newTopic("/Robot/Apple")
```


### Publishers 
Once we have a topic, we need a way to put information onto it. To do that, we create an object called a publisher that is responsible for updating the value stored in a specific topic.   

@todo add exmaples and fix the you might notice 
```Kotlin
createPublisher.

updating pubser 
```

You might notice that we're creating a @todo. This is because different types of information require different publisher classes. For example, battery voltage. Since it's stored as a double, we have to use a double publisher.  


```Kotlin
```


### Subscribing
Just as publishers are used for updating the value stored in topics, subscribers are used to read from them.

@todo example code creating a subscriber and accessing information
```
eg
```

Now whenever the publisher updates @todo, @todo name will automatically receive the new value. So the next time you read from @todo, it will have the updated value.

