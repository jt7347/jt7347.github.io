---
title: "Gesture Drone"
excerpt: "Modular Vision-Based Autonomous Quadcopter with Gesture Control Capabilities<br/><br/><img src='/images/Gesture_Drone.jpg' width='600'>"
collection: portfolio
---

Hello! This is my project page for the Gesture Drone - a modular autonomous computer-vision based quadcopter platform, developed by the Drone Team as part of Princeton University's Robotics Club. Computer-vision based gesture control was used as a benchmark goal to test the versatility of the platform, specifically within the realm of adapting close quarters human-robot interactions.

Here's the drone in action! In this video, the quad is taking off after a gesture 'cue' : a thumbs up signal from the operator.
<video muted controls>
    <source src="/files/Gesture_Control_Takeoff.mp4" type="video/mp4">
</video>
More refined controls will be added in the future (moving the quad, yawing the quad, etc.)!

Platform Details:

The platform is developed upon PX4: a open-source drone autopilot commonly used in both hobbyist and industrial settings. The quadcopter integrates a low level flight controller with a higher level controller (raspberry pi) for computer vision and decision making.

Build Guide:

- Parts list
- PX4 Flight Controller
- Quadcopter Electronics Basics
- CAD
- Sensors + Integration w/ PX4
- DroneKit (deprecated)
--> Direct to MAVSDK as newer controls API

Future Steps: