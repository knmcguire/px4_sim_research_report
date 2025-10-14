# PX4 Simulator Community Survey - Pilot Analysis

## Summary

A pilot survey was conducted with 6 PX4 developers to validate the survey instrument before wider distribution. Respondents were primarily professional engineers with advanced to expert-level simulator expertise, and most have 5+ years of PX4 experience. The results of this pilot survey will be used to fine-tune the final survey before it is sent out to the rest of the community.

## Simulator Usage and Goals

All pilot participants use Gazebo (Classic or Harmonic), confirming its dominance in the PX4 ecosystem. However, about half also use AirSim, FlightGear, or JSBSim, indicating demand for alternative simulator support. Primary use cases center on algorithm development, pre-flight testing, and quality assurance in CI pipelines. Notably, all respondents simulate only single vehicles. This is a sharp contrast with forum analysis showing multi-vehicle simulation as a critical pain point for the broader community.

Vehicle types are dominated by quadcopters being the biggest group, and fixed-wing aircraft afterwards, with VTOL and specialized vehicles showing lower representation. The equipment carried by these quadcopters is predominantly cameras and perception sensors.

## Technical Infrastructure

Hardware requirements prove significant: almost all had purchased new systems or upgraded existing ones specifically for simulation. Ubuntu dominates with minimal Windows usage. Despite substantial hardware investment, half report no significant limitations, suggesting current system requirements are acceptable to experienced users.

## Current Simulator Experience

Respondents evaluated their most recent simulator (primarily Gazebo variants) across multiple dimensions. For installation ease, there were mixed difficulties reported. But in general, the user experience for experienced developers for these simulation integrations is positive, but the opinion on the quality of documentation and tutorials varies quite a bit. Also, it is unclear if they are referring to the PX4 documentation or the documentation of the simulator itself.

Importantly, there seems to have been quite some comments on the physics realism, particularly in Gazebo itself. The variety of sensors is received positively, but the sensor models and the interactive physics in the simulator gets quite a lot of negative feedback, and is linked by some directly to the usefulness of the simulator itself.

There have been some open-ended questions answered here and there that mentioned the PX4 versioning issues with the simulators, that it was difficult to know which version worked with what (or that it was inconsistent). This goes in line with what has been observed in the forum analysis.

## Desired Features and Priority

From the Desired Features and Priority section, there were several items that the pilot participants rated as very important. Software-in-the-loop (SITL) is considered a very important feature, even more so than Hardware-in-the-loop (HITL). ROS/ROS2 integration has a clear consensus that it needs to always be included too, and participants wanted the simulator to be run from a Docker container.

Interestingly, having realistic physics models is much more important than having photorealistic rendering, even though most of the pilot participants used cameras as main driving sensors. Also, multi-agent simulation was very important to half of the pilot participants, even though they indicated that they usually only simulate one vehicle at a time, and there was a varied response on communication/network simulation (an important feature in swarms).

It does seem that there is also a preference for the ability of creating their own sensor models into the simulators, and that it is easy to create a robot model as well. However, easy GUI integrations such as drag-and-drop capabilities or beginner-friendliness scored low on the importance chart.

## Key Findings Summary

- **Physics realism is the top priority:** Realistic physics models are significantly more important than photorealistic rendering, with sensor models and interactive physics in Gazebo receiving substantial negative feedback that directly impacts perceived simulator usefulness.

- **Version compatibility is a persistent issue:** PX4 versioning with simulators creates confusion about which versions are compatible, with inconsistent version support—a pain point that aligns with broader forum analysis.

- **Multi-vehicle simulation is needed but underutilized:** Despite all respondents currently simulating only single vehicles, multi-agent simulation is very important to half the participants, highlighting a gap between current practice and future needs identified in community forums.

- **Core integrations are non-negotiable:** SITL capability, ROS/ROS2 integration, and Docker container support are considered essential features with clear consensus among experienced developers.

- **Customization over ease-of-use:** Developers prioritize the ability to create custom sensor models and robot configurations over beginner-friendly GUI features, reflecting the professional and advanced nature of the user base.