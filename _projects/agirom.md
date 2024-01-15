---
title: "AgIRoM"
excerpt: "A Replicated Hardware Research Platform for Agile Autonomous Vision-Based Flight<br/><br/><img src='/images/AgIRoM_fullbuild.jpg' width='600'>"
collection: portfolio
---

<img src='/images/agirom_desk.PNG' width='600'>

Overview
======
AgIRoM is a replicated platform, based on UZH Robotics and Perception Group's open-sourced platform [_Agilicious_](https://github.com/uzh-rpg/agilicious). The purpose for AgIRoM is for IRoM Lab to have a modular UAV (unmanned arial vehicle) research platform on hand that can be fitted to different research applications - for example, testing new control policies, or path-planning algorithms. In addition, there does not currently exist a 'standardized' UAV research platform capable of computer vision-based agile flight; the secondary purpose of AgIRoM is to affirm the process of standardizing a benchmark research platform for future lab work across the world to build upon - namely, _Agilicious_. For example, these platforms will funtion simlarly to how research labs may use a [Unitree Robotic Quadruped](https://m.unitree.com/en/), or a [Franka Robotic Arm](https://www.franka.de/). Considering the timely costs of building a new platform from the ground up every time a lab wants to conduct real-life UAV experiments, existing platforms that are readily available, easy to set up, and modularizeable, become a more lucrative option. 

In short, my work as an Undergraduate Researcher so far has been building AgIRoM, and setting it up for base-case autonomous flight operations using models pre-trained by UZH RPG's simulation software.

Build
======
Whilst _Agilicious'_ platform has most of the general build instructions detailed, issues such as deprecated software dependencies, version compatibilities with different hardware, parts being discontinued, will need to be ironed out individually. As such, I've written documentation for my process in building and developing AgIRoM, which can be found here:

<img src='/images/CAD_models.PNG' width='450'>

[Link to AgIRoM Build Guide!](https://jt7347.github.io/agirom-build-guide)

This guide will provide pointers for building and running the platform, including some conflicts I encountered + how I overcame them. In addition, it'll have instructions on how to configure and integrate newer/different hardware (for example, we used a Jetson Orin NX board instead of the discontinued Jetson TX2s used by _Agilicious_) and CAD files for mounting the sepcific parts we used. My hope is that this guide will help others understand what they're working with a little better - or as I like to think, there can never be too much documentation (or at least there's usually never enough of it...)!

For any questions, you can email jt7347 [at] princeton [dot] edu, or post an issue directly on the [_Agilicious_](https://github.com/uzh-rpg/agilicious) repo (request access reqired).

Flight Testing
======
Here are some videos of recent flight tests. The first test uses externally provided odometry through VICON motion tracking. 

<video muted controls width="750">
    <source src="/files/VICON.mp4" type="video/mp4" width='750'>
</video>

In this second video, the quadcopter is using onboard VIO algorithms for internally computed state estimation using a realsense T265 camera. 

<video muted controls width="750">
    <source src="/files/VISION_FEEDTHROUGH.mp4" type="video/mp4">
</video>

Simulation Software
======
One of the baseline purposes for AgIRoM is to be able to navigate unknown, changing environments in real time. The next step of AgIRoM was to get it working in base case situations: the interest of IRoM being navigation of UAVs in unknown changing environments. With the main purpose of the platform being 'development,' it would be useful to see if we could first implement a working application before additional features or policies could be implemented on top. For this purpose, I am currently looking into using UZH's [_Agile Autonomy_](https://github.com/uzh-rpg/agile_autonomy) repository as a benchmark for navigation. So far, I have been able to build and run their sample code (below is example of the output of the training).

<img src='/images/agile-autonomy.PNG' width='750'>