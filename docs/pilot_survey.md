# PX4 Simulator Community Survey - Pilot Analysis

## Summary

A pilot survey was conducted with 6 PX4 developers to validate the survey instrument before wider distribution. Respondents were primarily professional engineerswith advanced to expert-level simulator expertise, and most have 5+ years of PX4 experience. The result of this pilot survey will be used to fine tune the final survey before it is being send out to the rest of the community.


## Simulator Usage and Goals

All pilot participants use Gazebo (Classic or Harmonic), confirming its dominance in the PX4 ecosystem. However, about half also use AirSim, FlightGear, or JSBSim, indicating demand for alternative simulator support. Primary use cases center on algorithm development, pre-flight testing and quality assurance in CI pipelines. Notably, all respondents simulate only single vehicles. This is a sharp contrast with forum analysis showing multi-vehicle simulation as a critical pain point for the broader community.

Vehicle types are dominated by quadcopters being the biggest group, and fixed-wing aircraft afterwards, with VTOL and specialized vehicles showing lower representation. The carried equipment by these quadcotpers are predominatly cameras and perception sensors.

## Technical Infrastructure

Hardware requirements prove significant: almost all had to purchased new systems or upgraded existing ones specifically for simulation. Ubuntu dominates with minimal Windows usage. Despite substantial hardware investment, half report no significant limitations, suggesting current system requirements are acceptable to experienced users. 

## Current Simulator Experience

Respondents evaluated their most recent simulator (primarily Gazebo variants) across multiple dimensions. For installation ease, there were mixed difficulties with that reported. But in general, the user experience for experience developers for these simulation intergration is possitive, but the opinion on the quality of documentation and tutorials varies quite a bit. Also it is unclear if they are referringn to the PX4 documentation or the documentation of the simulator itself.

Importantly, there seems to have been quite some comments on the physics realism, in particular in gazebo itself. The variety of sensors is received positive, but the sensor models and the interactive phycics in the simulator gets quite a lot of negative feedback, and is linked by som directly to the usefullness of the simulator itself. 

There have been some open-ended questions answered here and there that mentioned about the PX4 versioning issues with the simulators, that it was difficult to know which version worked with what (or that it was inconcistent). This goes in line with what has been observed in the forum analysis.

## Desired Features and Priority 

From the Desired Features and Priority section, there were several items that the pilot participants very important. Software in the loop  (SITL) is considered very important feature, even more so than Hardware in the loop (HITL), ROS/ROS2 intergration has a clear consensus that it needs to always be included too, and wanted the simulator to be run from a docker container.

Interestingly, having realistic phycis models is much more important than having photo realistic rendering, eventhough most of the pilot participants used cameras as main driving sensors. Also, multiagent-simulation was veery important to half of the pilot participants, eventhough they indicated that they usually only simulate one vehicle at the time, and there was a varied response on communication/network simulation (an important feature in swarms).

It oes seem that there is also a preference an the ability of creating their own sensor models into the simulators, and that it is easy to create a robot model as well. However, easy GUI intergrations as drag-en-drop capabilities or beginner friendliness scored low on the importance chart.

