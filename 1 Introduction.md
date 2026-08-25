# What Is FRC Programming

Every year, FIRST Robotics announces a brand-new game that each team designs and builds a robot to participate in. It is our job as programmers to write code that controls how the robot behaves. This is everything from simply moving motors to automated complex tasks like scoring game pieces. 

Often, automated tasks are created to help the driver during matches. For example, in the 2025 game Reefscape, drivers had to precisely align their robots with a structure known as the Reef to score, but this became challenging when fast moving robots were blocking them. To help with this challenge, we created a tool that automatically aligned our robot with the Reef to help our driver score quickly and consistently.  

I couldn’t find footage of our own auto-align, so I've included an example from Team 4561, TerroBytes. 
[TerroBytes' Auto align](https://www.youtube.com/watch?v=wnomO6tZais) 

# What Does Robot Code Do During A Match

Each match can be broken down into two phases: Autonomous (Auto) and Teleoperated (Teleop).    

In Auto, the robot can’t receive any inputs from the driver. Instead, it will follow a set of instructions that we previously programmed. For example, one might tell the robot to drive forward, pick up a game piece, and score it.

In Teleop, the driver controls the robot, so inputs, like moving a joystick, are turned into actions that the robot will perform.

# What a Typical Build Season Looks Like


A typical build season starts with a team brainstorming session right after kickoff. This gives our team time to understand the game and decide what we want our robot to be capable of. By the next meeting, our CAD team usually has a general idea of what mechanisms the robot will have.  After a meeting with the CAD team, we divvy up the different mechanisms and start writing code for them. 

Once the initial code is written, we either spend time training new people, testing code logic with a simulated robot, or working on non essential projects like object detection while the robot is being built. Once the robot is assembled, we move onto our busiest time of year. From that point onwards, we begin debugging our code with a physical robot, tuning subsystems so they behave how we want, and writing autos.


	