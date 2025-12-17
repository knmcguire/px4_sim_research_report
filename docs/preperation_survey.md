# Survey Preparation

## Survey Design and Methodology

### Survey Structure

The PX4 Simulator Community Survey was designed to gather feedback from users across all aspects of their simulation experience. The survey is set up in six main sections: demographic background, current simulator usage patterns, technical infrastructure, simulator experience evaluation, feature priorities, and strategic recommendations. The survey uses a mixed-methods approach combining quantitative Likert-scale ratings with qualitative open-ended questions.


The survey begins by establishing user segments through profession, simulator expertise level, and PX4 experience duration. This segmentation allows analysis of how different user groups (students, researchers, commercial engineers) experience simulation and what improvements they prioritize.


Questions about which simulators users employ, their purposes (research, testing, commercial development), vehicle types, and scale (single vs. multi-vehicle) help map the current PX4 simulation landscape. This information provides insight into how the community currently uses simulation tools.


Hardware and infrastructure questions examine potential barriers to adoption. The survey asks whether users have purchased new systems, what operating systems they use, and where they encounter limitations (CPU, GPU, RAM). This data provides information about current hardware requirements and performance constraints.


The survey uses detailed Likert-scale assessments across five dimensions: installation experience, user interface, technical performance, feature support, and community resources. This structured approach allows users to provide feedback on specific aspects of their simulation experience. Open-ended questions at the end allow participants to share observations that may not be captured by the structured questions.


Users rate importance of potential improvements across technical capabilities, platform compatibility (OS support, ROS integration), usability, and advanced features. This provides a prioritization matrix showing which capabilities matter most to different segments of the community.

The survey concludes with open-ended questions soliciting input on the most important improvements needed and offering opportunities for follow-up interviews. This acknowledges that while quantitative data identifies patterns, qualitative discussion often reveals underlying causes and context that ratings alone cannot capture.

The pilot version of the survey can be found in the Appendix ( @sec-pilot )

## Pilot Survey Analysis

A pilot survey was conducted with 6 PX4 developers to validate the survey instrument before wider distribution. Respondents were primarily professional engineers with advanced to expert-level simulator expertise, and most have 5+ years of PX4 experience. The results of this pilot survey will be used to fine-tune the final survey before it is sent out to the rest of the community.



### Simulator Usage and Goals

All pilot participants use Gazebo (Classic or Harmonic). About half also use AirSim, FlightGear, or JSBSim. Primary use cases center on algorithm development, pre-flight testing, and quality assurance in CI pipelines. All respondents simulate only single vehicles, which differs from forum analysis (@sec-forum) where multi-vehicle simulation appears as a recurring topic in the broader community.
Vehicle types are dominated by quadcopters, followed by fixed-wing aircraft, with VTOL and specialized vehicles showing lower representation. The equipment carried by these quadcopters is predominantly cameras and perception sensors.


### Technical Infrastructure

Almost all pilot participants had purchased new systems or upgraded existing ones specifically for simulation. Ubuntu dominates the operating system distribution with minimal Windows usage. Despite substantial hardware investment, half report no significant limitations.

### Current Simulator Experience

Respondents evaluated their most recent simulator (primarily Gazebo variants) across multiple dimensions. Installation ease received mixed feedback. The overall user experience for experienced developers appeared positive, though opinions on documentation and tutorials quality varied considerably. It is unclear whether respondents were referring to PX4 documentation or simulator documentation.
Several comments addressed physics realism, particularly in Gazebo itself. While sensor variety was received positively, sensor models and physics simulation received negative feedback from multiple respondents, with some linking this directly to simulator usefulness.
Several open-ended responses mentioned PX4 versioning issues with simulators, noting difficulty in determining compatible version combinations. This observation aligns with patterns observed in the forum analysis (found in @sec-forum).


### Desired Features and Priority

In the Desired Features and Priority section, pilot participants rated several items as very important. Software-in-the-loop (SITL) received higher importance ratings than Hardware-in-the-loop (HITL). ROS/ROS2 integration showed clear consensus as essential. Participants also indicated preference for Docker container support.

Realistic physics models received higher importance ratings than photorealistic rendering, despite most pilot participants using cameras as main sensors. Multi-agent simulation was rated as very important by half of the pilot participants, though they indicated typically simulating only single vehicles. Communication/network simulation received varied responses.

Participants showed preference for the ability to create custom sensor models and easily create robot models. GUI features such as drag-and-drop capabilities or beginner-friendly interfaces scored lower on importance ratings.

## Forum Analysis {#sec-forum}


This analysis examines 152 forum posts from the PX4 discussion forum (discuss.px4.io) spanning September 2024 through September 2025 to identify pressing issues in simulation integration. Several representative forum messages are referenced throughout this text, but the full list of forum posts evaluated is available upon request.

Several categories emerged from this investigation, which will be discussed here.

### Version Stability and Platform Support

Forum posts indicate that some PX4 updates have introduced breaking changes. Users report that critical parameters for custom spawn positions were removed without alternatives[@px4-41925], and Hardware-in-the-Loop functionality broke in newer versions[@px4-46594]. Platform-specific issues appear more frequently for macOS users, especially those on Apple Silicon[@px4-45887].

### Core Simulation Reliability

Users report problems with simulation accuracy and stability. Some posts describe Extended Kalman Filter position drift exceeding 50 meters during simple hovering[@px4-40657], particularly when using custom worlds or external sensors. Flight dynamics issues appear in multiple posts: drones arm correctly but fail to take off, or cannot climb beyond minimal altitudes[@px4-43349; @px4-44266]. One post identifies an architectural limitation preventing custom simulators from running slower than real-time[@px4-47188].

### Multi-Vehicle Scalability

For multi-vehicle simulation, users report startup times exceeding 20 minutes for multiple drones[@px4-47532]. Configuration complexity appears in multiple posts, including managing unique ports, distinguishing sensor topics, and coordinating spawn positions[@px4-41744; @px4-40885; @px4-40847]. Posts also describe communication failures between ground control stations and multiple vehicles[@px4-42697; @px4-44693].

### Ecosystem Integration

Multiple posts describe ROS2 bridge reliability issues where sensor data visible in Gazebo fails to reach ROS2 topics[@px4-44447; @px4-47421]. Offboard control through ROS2 shows inconsistent behavior in several posts, including frame convention problems and actuator control failures[@px4-45073; @px4-44630]. Beyond ROS2, posts describe difficulties integrating alternative simulators like Unity, AirSim, and MATLAB/Simulink[@px4-42508; @px4-45970; @px4-42303].

### Custom Model Development

Posts describe unpredictable flight behavior when modifying physical properties[@px4-43417], and unclear physical meaning in the motor control interface[@px4-46132]. Specialized vehicle types (VTOLs, coaxial configurations, fixed-wing aircraft) appear in several posts describing issues, including dangerous behaviors like uncontrolled dives during transitions[@px4-46487; @px4-46582].

### Sensor and Environment Fidelity

Posts describe camera streams failing to initialize properly[@px4-42909], documented features like terrain following not working[@px4-43683], and environmental effects such as wind failing to manifest despite available commands[@px4-45696]. Multiple posts report connection failures with ground control stations when using custom worlds[@px4-46990], with some requiring undocumented workarounds[@px4-47409].

### Deployment and Containerization

Posts report Docker-based deployment issues including connection failures, missing video feeds, and rendering problems[@px4-46059; @px4-45983; @px4-44619].

## Final Survey Preperation

The final version of the PX4 Simulator Community Survey incorporates changes based on pilot feedback and forum analysis. The survey was reduced from approximately 35 questions with over 70 individual items to 29 questions with fewer than 40 items for participants to answer.

### Survey Length and Structure

The most significant change was removing the entire "Current Simulator Experience" section, which contained 30+ Likert-scale items asking respondents to rate installation ease, user experience, performance, and documentation. Pilot respondents mentioned survey length concerns, and these quantitative ratings showed less consensus compared to open-ended feedback.
The survey now retains two open-ended questions asking what users like most and their biggest frustration. The Gazebo team will be conducting their own survey on Gazebo simulator issues separately.


### Audience Expansion

The pilot survey participants were primarily experienced, industrial-oriented developers, all simulating only single vehicles. Forum analysis showed issues (installation problems, multi-vehicle challenges, documentation gaps) that appear to affect novice and intermediate users. The final version adds explicit language in the introduction stating the survey is for "anyone who has used or is interested in using simulation with PX4" and adds "Hobbyist / Independent Developer" as a profession option.

### Version Compatibility and Integration

Forum analysis (@sec-forum) revealed version compatibility as a recurring topic, with posts describing breaking changes between PX4 releases removing critical features like custom spawn positions. Multiple users expressed frustration that "things worked in one configuration, but does not in another." The final survey adds explicit questions about version compatibility issues and importance.

### Multi-Vehicle and Advanced Features

While pilot respondents all simulated single vehicles, forum analysis identified multi-vehicle simulation as a recurring topic. The final survey retains questions about the importance of multi-vehicle simulation and networking communication simulation.

### Strategic Roadmap Priority

A new section asks respondents to select their single top priority for PX4 simulation development and justify why. This forced-choice question aims to identify what participants consider the most important issue in their workflow regarding PX4 simulation integration.


_The final survey can be found in the Appendix ( @sec-final )_

