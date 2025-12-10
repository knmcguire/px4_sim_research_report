# Survey Preperation

## Survey Design and Methodology

### Survey Structure

The PX4 Simulator Community Survey was designed to gather feedback from users across all aspects of their simulation experience. The survey is setup in six main sections: demographic background, current simulator usage patterns, technical infrastructure, simulator experience evaluation, feature priorities, and strategic recommendations. The survey uses a mixed-methods approach combining quantitative Likert-scale ratings with qualitative open-ended questions.


The survey begins by establishing user segments through profession, simulator expertise level, and PX4 experience duration. This segmentation enables analysis of how different user groups (students, researchers, commercial engineers) experience simulation differently and prioritize different improvements. Understanding whether issues affect primarily beginners or experienced users helps to prioritize development efforts.


Questions about which simulators users employ, their purposes (research, testing, commercial development), vehicle types, and scale (single vs. multi-vehicle) map the PX4 simulation landscape. This information is essential for resource allocation decisions: should development focus deepen and improve integration with existing simulators, or broaden support for alternative simulators or platforms?


Hardware and infrastructure questions assess barriers to adoption. Understanding whether users must purchase expensive systems, what operating systems they use, and where they encounter limitations (CPU, GPU, RAM) reveals accessibility issues and performance bottlenecks. This data informs decisions about which minimum system requirements the developers should take into account.


The survey uses detailed Likert-scale assessments across five dimensions: installation experience, user interface, technical performance, feature support, and community resources. This structured approach aims to identify specific pain points. For example, whether installation is problematic but documentation adequate, or vice versa. These type of questions should make it easier for users to answer to formulate their thoughts and if they agree. And if in any case a statement has been missed, this can be catched by the open ended questions at the end.


Users rate importance of potential improvements across technical capabilities, platform compatibility (OS support, ROS integration), usability , and advanced features. This creates a prioritization matrix showing which capabilities matter most to the community, enabling evidence-based development roadmap decisions.

The survey concludes with open-ended questions soliciting input on the most important improvements needed and offering opportunities for follow-up interviews. This acknowledges that while quantitative data identifies patterns, qualitative discussion often reveals underlying causes and context that ratings alone cannot capture.

The pilot version of the survey can be found in the Appendix ( @sec-pilot )

## Pilot Survey Analysis

A pilot survey was conducted with 6 PX4 developers to validate the survey instrument before wider distribution. Respondents were primarily professional engineers with advanced to expert-level simulator expertise, and most have 5+ years of PX4 experience. The results of this pilot survey will be used to fine-tune the final survey before it is sent out to the rest of the community.



### Simulator Usage and Goals

All pilot participants use Gazebo (Classic or Harmonic), confirming its dominance in the PX4 ecosystem. However, about half also use AirSim, FlightGear, or JSBSim, indicating demand for alternative simulator support. Primary use cases center on algorithm development, pre-flight testing, and quality assurance in CI pipelines. Notably, all respondents simulate only single vehicles. This is a sharp contrast with forum analysis (@sec-forum) showing multi-vehicle simulation as a critical pain point for the broader community.
Vehicle types are dominated by quadcopters being the biggest group, and fixed-wing aircraft afterwards, with VTOL and specialized vehicles showing lower representation. The equipment carried by these quadcopters is predominantly cameras and perception sensors.


### Technical Infrastructure

Hardware requirements prove significant: almost all had purchased new systems or upgraded existing ones specifically for simulation. Ubuntu dominates with minimal Windows usage. Despite substantial hardware investment, half report no significant limitations, suggesting current system requirements are acceptable to experienced users.

### Current Simulator Experience

Respondents evaluated their most recent simulator (primarily Gazebo variants) across multiple dimensions. For installation ease, there were mixed difficulties reported. But in general, the user experience for experienced developers for these simulation integrations is positive, but the opinion on the quality of documentation and tutorials varies quite a bit. Also, it is unclear if they are referring to the PX4 documentation or the documentation of the simulator itself.
Importantly, there seems to have been quite some comments on the physics realism, particularly in Gazebo itself. The variety of sensors is received positively, but the sensor models and the interactive physics in the simulator gets quite a lot of negative feedback, and is linked by some directly to the usefulness of the simulator itself.
There have been some open-ended questions answered here and there that mentioned the PX4 versioning issues with the simulators, that it was difficult to know which version worked with what (or that it was inconsistent). This goes in line with what has been observed in the forum analysis (found in the @sec-forum).


### Desired Features and Priority

From the Desired Features and Priority section, there were several items that the pilot participants rated as very important. Software-in-the-loop (SITL) is considered a very important feature, even more so than Hardware-in-the-loop (HITL). ROS/ROS2 integration has a clear consensus that it needs to always be included too, and participants wanted the simulator to be run from a Docker container.

Interestingly, having realistic physics models is much more important than having photorealistic rendering, even though most of the pilot participants used cameras as main driving sensors. Also, multi-agent simulation was very important to half of the pilot participants, even though they indicated that they usually only simulate one vehicle at a time, and there was a varied response on communication/network simulation (an important feature in swarms).

It does seem that there is also a preference for the ability of creating their own sensor models into the simulators, and that it is easy to create a robot model as well. However, easy GUI integrations such as drag-and-drop capabilities or beginner-friendliness scored low on the importance chart.

## Forum Analysis: PX4 Simulation Integration Issues {#sec-forum}


This analysis examines 152 forum posts from the PX4 discussion forum (discuss.px4.io) spanning September 2024 through September 2025 to identify pressing issues in simulation integration. Several representative forum messages are referenced throughout this text, but the full list of forum posts evaluated is available upon request.

Several categories emerged from this investigation, which will be discussed here.

### Version Stability and Platform Support

Occasionally, PX4 updates have introduced breaking changes that disrupt existing workflows. Critical parameters for custom spawn positions were removed without alternatives[@px4-41925], and Hardware-in-the-Loop functionality broke in newer versions[@px4-46594]. Platform-specific issues predominantly affect macOS users, especially those on Apple Silicon[@px4-45887].

### Core Simulation Reliability

Users report problems with simulation accuracy and stability. The Extended Kalman Filter exhibits severe position drift. Sometimes exceeding 50 meters during simple hovering[@px4-40657], particularly when using custom worlds or external sensors. Flight dynamics frequently malfunction: drones arm correctly but fail to take off, or cannot climb beyond minimal altitudes[@px4-43349; @px4-44266]. A critical architectural limitation prevents custom simulators from running slower than real-time[@px4-47188], restricting integration with high-fidelity physics engines.

### Multi-Vehicle Scalability

For multi-vehicle simulation, users report startup times exceeding 20 minutes for multiple drones[@px4-47532], indicating sequential bottlenecks rather than parallel initialization. Configuration complexity (managing unique ports, distinguishing sensor topics, and coordinating spawn positions) suggests the system was designed for single vehicles and later extended incrementally[@px4-41744; @px4-40885; @px4-40847]. Communication failures between ground control stations and multiple vehicles further complicate swarm research and industrial multi-agent applications[@px4-42697; @px4-44693].

### Ecosystem Integration

Many users want to leverage the ROS2 framework, but the ROS2 bridge exhibits reliability issues where sensor data visible in Gazebo fails to reach ROS2 topics[@px4-44447; @px4-47421]. Offboard control through ROS2 behaves inconsistently, with frame convention problems and actuator control failures[@px4-45073; @px4-44630]. Beyond ROS2, users struggle to integrate alternative simulators like Unity, AirSim, and MATLAB/Simulink[@px4-42508; @px4-45970; @px4-42303].

### Custom Model Development

Users modifying physical properties encounter unpredictable flight behavior[@px4-43417], while the motor control interface lacks clear physical meaning[@px4-46132]. Specialized vehicle types (VTOLs, coaxial configurations, fixed-wing aircraft) show particular gaps, with dangerous behaviors like uncontrolled dives during transitions[@px4-46487; @px4-46582]. The simulation framework appears optimized primarily for standard quadcopters, making integration of custom vehicle models challenging.

### Sensor and Environment Fidelity

Camera streams fail to initialize properly[@px4-42909], documented features like terrain following don't work[@px4-43683], and environmental effects such as wind fail to manifest despite available commands[@px4-45696]. Custom world integration frequently causes connection failures with ground control stations[@px4-46990], requiring undocumented workarounds[@px4-47409]. Sensor simulation shows inconsistent functionality according to users on the forum.

### Deployment and Containerization

Docker-based deployments face systematic issues including connection failures, missing video feeds, and rendering problems[@px4-46059; @px4-45983; @px4-44619]. These challenges limit adoption in cloud-based CI/CD pipelines and distributed development environments, which is why developers need to use local development setups.

## Final version survey

The final version of the PX4 Simulator Community Survey has certain improvements compared to the first version, based on pilot feedback and forum analysis. An important aspect was to reduce survey length while adding critical questions that address real community pain points. The survey was reduced from approximately 35 questions with over 70 individual items to 29 questions with fewer than 40 items for the participants the answer.

### Survey Length and Structure

The most significant change was removing the entire “Current Simulator Experience” section, which contained 30+ Likert-scale items asking respondents to rate installation ease, user experience, performance, and documentation. Pilot respondents explicitly complained about survey length, and analysis revealed these quantitative ratings provided limited insights compared to open-ended feedback questions as there was less consensus on which issues are important. Moreover, it will be difficult to evaluate this section if the users enter different simulators that they have used.
The survey now retains only two open-ended questions asking what users like most and their biggest frustration. The Gazebo team will be conducting their own survey on issues what people are having on with the gazebo simulator, so that could give insights that are relevant for this investigation as well.


### Audience Expansion

The pilot survey results had a bias because these were very experienced, mostly industrial-oriented developers, all simulating only single vehicles. However, forum analysis showed that many critical issues (installation problems, multi-vehicle challenges, documentation gaps) affect novice and intermediate users mostly. So in the final version adds explicit language in the introduction stating the survey is for “anyone who has used or is interested in using simulation with PX4” and adds “Hobbyist / Independent Developer” as a profession option. This will encourage more people to participate with the survey.

### Version Compatibility and Integration

Forum analysis (@sec-forum) revealed that version compatibility as a recurring crisis, with breaking changes between PX4 releases removing critical features like custom spawn positions. Multiple users expressed frustration that “things worked in one configuration, but does not in another.” So the final survey adds explicit questions aversion compatibility issues and importance as well.

### Multi-Vehicle and Advanced Features

While pilot respondents (core developers) all simulated single vehicles, forum analysis  did identified multi-vehicle simulation as an important pain point. The final survey keeps questions about the importance of multi vehicle simulation and networking communication simulation.

### Strategic Roadmap Priority

The most important addition is a new section asking respondents to select their single top priority for PX4 simulation development and justify why. This forced-choice question addresses will put extra emphasis on what the participant thinks the PX4 simulation gazebo team should be focused on, and to make the participant think about what is the most important pressing issue in his/hers workflow regarding the PX4 simulation integration.


_The final survey can be found in the Appendix ( @sec-final )_

