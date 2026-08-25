Our code rarely works as intended on the first try. There is always something that can be improved, whether that be some logic or PID constants (which I'll cover later). And without some means of knowing what the code is doing, we'll just be doing guesswork. To avoid this, we do something called logging.

Just like how a journal records the events of a day, our logs record what happened while the robot was running. And the processes of logging is just saving information about the robot to that log. But how do we actually log? 

Well in FRC, there are many different ways to log; however, we use AdvantageKit. AdvantageKit is a logging framework created by team 6328, Mechanical Advantage.  Once it's set up it's really easy to use. All you have to do is this : 

```Kotlin
Logger.recordOutput(key,value)
```
The **key** what the **value** will be saved under. So if you have a key like, `Intake/Piviot Angle`, then the value will be stored withing a `Intake` folder, similar to how Network Tables does it.

## Viewing Logged Data
Right now, we have logs, but now way to view them; however, thanks to Advantage Scope, another tool by Mechanical Advantage, it's really easy.  With it, we can view life data from the robot, or replay matches.


>[!info]- Setting Up Advantage Scope 
>@todo 


>[!info]- Viewing Live Data from the Robot
>@todo

>[!info]- Replaying Matches
>@todo


>[!info]- Navigating Advantage Scope 
>There are plenty of good resources explain how to navigate Advantage Scope.  For example, the [official documentation ](https://docs.advantagescope.org/overview/navigation/)



Viewing data 

Replaying matches
%%
1) What is loggging and why we use it 
2) How we log info 
3) Viewing data via akit
4) Allowing for sim
5) Activyt 
	1) Look at file in adavtage scope
	2) Add logging to code 
	3) 