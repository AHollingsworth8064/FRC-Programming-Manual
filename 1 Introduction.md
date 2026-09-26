# Introduction

Welcome to the Programming subteam! Every subteam on our team is a tight-knit community of friends, and Programming is no different. Programming is arguably one of the most useful skills you can learn from robotics (otherwise we wouldn't be on this team), one that will serve you well in unexpected places in your future. 

That said, learning the art of writing code requires dedication. A lot of effort went into writing this book for new members who haven't yet taken the AP Computer Science elective, and hopefully you will put that same effort into reading it. Programming often spends late nights after school testing the robot at a [practice field](https://maps.app.goo.gl/GYxfae37Z8MUGWG58) in Camas, Washington, and if you want to learn faster how we do things you should come out there with us (if you can). 

But, don't let any of this discourage you! It is so incredibly rewarding to see your own code working on a robot in a competition. And, by all means, if you put in the effort you will see your own code running on the robot in a few months! The first step is to spend time reading through this book.

## What Is FRC Programming

Every year, FIRST Robotics announces a brand-new game that each team designs and builds a robot to participate in. It is our job as programmers to write code that controls how the robot behaves. This is everything from simply moving motors to automated complex tasks like scoring game pieces. 

Often, automated tasks are created to help the driver during matches. For example, in the 2025 game Reefscape, drivers had to precisely align their robots with a structure known as the Reef to score, but this became challenging when fast moving robots were blocking them. To help with this challenge, we created a tool that automatically aligned our robot with the Reef to help our driver score quickly and consistently.  

I couldn’t find footage of our own auto-align, so I've included an example from Team 4561, TerroBytes. 
[TerroBytes' Auto align](https://www.youtube.com/watch?v=wnomO6tZais) 

## What Does Robot Code Do During A Match

Each match can be broken down into two phases: Autonomous (Auto) and Teleoperated (Teleop).    

In Auto, the robot can’t receive any inputs from the driver. Instead, it will follow a set of instructions that we previously programmed. For example, one might write code telling the robot to drive forward, pick up a game piece, and score it. Although the Auto period is short relative to Teleop, in Programming we spend a lot of our time focusing on it; it takes a lot of complex code and fine-tuning to autonomously control a robot in an efficient and precise manner.

In Teleop, the driver controls the robot, so inputs, like moving a joystick, are turned into actions that the robot will perform. 

## What a Typical Build Season Looks Like

A typical build season starts with a team brainstorming session right after kickoff. This gives our team time to understand the game and decide what we want our robot to be capable of. By the next meeting, our CAD team usually has a general idea of what mechanisms the robot will have.  After a meeting with the CAD team, we divvy up the different mechanisms and start writing code for them (one of the challenges here is that we don't fully know what the mechanisms will look like). 

Once the initial code is written, we either spend time training new people, testing code logic with a simulated robot, or working on non-essential projects like object detection while the robot is being built. Once the robot is assembled, we move onto our busiest time of year. From that point onwards, we begin debugging our code with a physical robot, tuning subsystems so they behave how we want, and writing autos. Because of this, programming has a unique vibe—we spend a lot of the year without much urgent work to do, but when the robot is built the work becomes urgent and highly integrated with other subteams.

## Guide to the Chapters

1. Introduction: This chapter.

2. Basic Programming Lesson Plan: This will teach you all you need to know to program in Kotlin. If you already know a programming language like Java or Python, you can skim through this as long as you understand the concepts.

3. Robotics Basics: An overview of the different components of the robot and its code.

4. How we Structure our Code: An overview of the different components of our own code.

5. Making a Mechanism: Learn how to write a mechanism, like the intake or the shooter. At this point you will probably be able to write your own code for our robot!

6. Commands: How the robot actually does things.

7. Git: The way we—and virtually all teams of programmers around the world—collaborate and write code in parallel.

8. Sensors: How we read the world around the robot.

9. Logging: The logging tools we use to convert loads of data on the robot to a format that is readable.