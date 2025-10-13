
### Short Summary

This analysis examines forum posts and request for simulation support from the PX4 discussion forum (discuss.px4.io) spanning the past year (2024-2025). This is done to preliminary identify pressing issues in simulation integration within the PX4 autopilot simlation. In this analysis, the posts were filtered and categorized into ten priority areas based on technical depth, impact severity, and relevance to simulation integration. The analysis reveals that multi-vehicle simulation scalability, EKF positioning stability, and ROS2 integration reliability emerge as the  critical concerns affecting users. These findings will be used to further fine tune user survey to validate development priorities and resource allocation for simulation improvements.

### Method

The forum posts were sourced from discuss.px4.io, covering discussions from September 2024 through September 2025. The analysis followed a systematic approach:

1. **Filtering**: Posts were screened to remove low-effort support requests (e.g., "help! I can't connect" with no debugging information), duplicate threads, and topics such as hardware-specific issues or general learning resource requests.
1. **Categorization**:  Posts were categorized based on the primary technical domain affected (e.g., multi-vehicle support, sensor simulation, platform compatibility).

2. **Priority Assessment**: Issues were ranked considering frequency of occurrence, severity of impact (blocking vs. degraded functionality), and alignment with common use cases in the PX4 ecosystem.

For this analysis, we started with 242 forum topics, which resulted in 152 substantive technical issues, down to 136 issues due to duplication questions. These were organized into ten priority categories, namely:

* Critical Breaking Issues
* Core Simulation Stability
* Multi-Vehicle Simulation
* ROS2/MAVROS Integration
* Custom Models and Airframes
* Sensor Simulation
* Docker and Deployment
* World and Environment
* Parameter and Configuration

### Findings per category

#### Critical Breaking Issues

The most urgent category involves regressions introduced in recent PX4 versions.  For instance an issue[@px4-41925] indicated that it impossible to spawn drones at custom positions—a fundamental requirement for multi-vehicle simulations and mission testing due to the mismatch in parameters. Similarly, there was a report of that Hardware-in-the-Loop (HITL) actuators ceased functioning in a later version, breaking a testing workflow for hardware validation.[@px4-46594]

Platform-specific build failures also fall into this category as well. Multiple users reported incompatibilities with macOS 15.0 (Sequoia) and difficulties with Apple Silicon builds. These issues are particularly problematic as they represent blockers, which means that users cannot proceed with any simulation work until resolved. Several forum posts [@px4-40832; @px4-40889; @px4-43606; @px4-44661; @px4-44172; @px4-45887; @px4-46712] indicate problems with build toolchains across different operating systems and versions.


#### Core Simulation Stability

The Extended Kalman Filter (EKF) and positioning subsystems show recurring instability patterns. One discussion[@px4-40657] describes extreme position drift and jumping estimates during basic hovering in a Docker-based Gazebo Harmonic setup.  Similar reports[@px4-45701; @px4-46410; @px4-45340] suggest problems with position estimation when using custom worlds, external visual odometry, or non-standard sensor configurations. There have also been additional EKF-related issues reported as well in other posts.[@px4-40696; @px4-41693; @px4-38605; @px4-42050; @px4-42291; @px4-42720; @px4-43607; @px4-41928]

Flight behavior issues frequently prevent basic operations. Multiple users report drones that arm successfully but fail to take off[@px4-43349; @px4-44266; @px4-44442]. One forum post[@px4-39412] describes heavy drones that "climb unresponsively after takeoff," indicating that they were having problems with thrust-to-weight modeling or controller tuning in simulation. Another post[@px4-44460] reports take-off failures after controller modifications, while a second post[@px4-45612] shows VTOL-specific takeoff problems. There are several other additional flight issues reported as well [@px4-45275; @px4-45842].

Timing and performance issues also affect simulation performance. A fundamental limitation was highlighted[@px4-47188]: custom simulators running slower than real-time cannot function with PX4 SITL due to lockstep timing assumptions. One forum post[@px4-43347] reports ROS subscribers slowing simulation, while another[@px4-44546] describes environment-specific crashes. There have been one discussion post[@px4-47475] that requests simulation speed improvements.

#### Multi-Vehicle Simulation

Multi-vehicle simulation emerges as a pain point with both configuration complexity and performance issues. Issue [@px4-47532] reports startup times exceeding 20 minutes when launching multiple drones which is resulted by a sequential bottleneck. Configuration challenges compound performance problems. Users struggle with MAVLink port allocation[@px4-47156], distinguishing sensor topics between drones[@px4-40885], and setting unique spawn positions[@px4-40847]. There have been one report[@px4-42697] of an inability to arm multiple drones simultaneously in SITL, while issue[@px4-44693] describes MAVSDK communication failures in multi-drone setups. 

#### ROS2/MAVROS Integration

The ROS2 bridge exhibits some reliability problems affecting sensor data flow. A couple of forum posts[@px4-44447; @px4-44810] report failures in the ros_gz_bridge preventing camera image topics from reaching RViz2, despite the topics being visible in Gazebo's native tools. Also a problem was described that scan topics that never publish messages[@px4-47421], breaking SLAM toolbox integration. There have been several reports that also indicate similar sensor data failures[@px4-47421; @px4-43428; @px4-43476]. One forum post[@px4-45529] describes problems launching ROS with PX4 SITL, and  reports general topic publication failures[@px4-45852]. Also, visual odometry topic issues have been reported[@px4-46126], while other reports shows the disconnect between Gazebo and ROS2 topic visibility[@px4-46979].

Offboard control through ROS2 has been reported having issues as well. There have been a report[@px4-45073] that direct actuator control fails to respond, while another[@px4-42010] describes VTOL-specific offboard control challenges. One user[@px4-44630] notes frame convention problems with `MAV_FRAME_BODY_NED`, causing unexpected offsets. Several users[@px4-42506; @px4-46447] report general offboard mode difficulties. 

#### Custom Models and Airframes

Users attempting to create custom vehicle models are encountering some unpredictable behavior and have difficulty find documentations. One post[@px4-43417] describes an octocopter that "only takes off at 0.8m and does not reach the desired altitude" after modifying mass and inertia properties, even with increased motor velocity limits. 

A user[@px4-46241] highlights the difficulty of determining correct motor constants for Gazebo models. Another support post[@px4-46132] identifies a potential bug in the GZ bridge ESC interface, where the relationship between PWM values and motor commands lacks clear physical meaning. One user has requested clearer motor parameter definitions[@px4-34747], while many others[@px4-40607; @px4-40575; @px4-43858; @px4-46547; @px4-6700; @px4-47541] have reported various custom model creation challenges.

Specialized vehicle types show gaps in simulation intergration. Multiple issues[@px4-46487; @px4-46582; @px4-46561] report VTOL tilt-rotors diving uncontrolably during transitions and one users[@px4-46838] notes reversible motors cannot actually reverse in SITL. One user[@px4-28805] describes coaxial octocopter simulation problems, while another post[@px4-32781] requests airship simulation support. Additional specialized vehicle issues[@px4-18807; @px4-42031; @px4-42077; @px4-42324; @px4-43654; @px4-5207; @px4-46457; @px4-46469; @px4-46758; @px4-47231; @px4-47263]. These suggest the simulation framework optimizes for standard quadcopters at the expense of other vehicle types.

#### Sensor Simulation

Camera and vision sensors reportely show inconsistent functionality. A couple of posts[@px4-42909; @px4-43155] report video streams that are "unavailable". One user[@px4-45077] describes hardware encoding errors in Gazebo camera plugins, while others[@px4-45711; @px4-45952] highlight camera integration difficulties. One user[@px4-43035] addresses point cloud visualization challenges. 

Advanced navigation sensors face integration challenges. [@px4-43683] and [@px4-47022] report terrain following that "does not work" in PX4 Gazebo despite being a documented feature. [@px4-43527] asks about optical flow without GPS—a common real-world scenario—but receives no clear implementation path.  [@px4-45225] reports general sensor loading failures, and [@px4-45919] requests multi-sensor setup guidance. Issues[@px4-42909; @px4-43167] report video streams that are "unavailable" despite proper configuration, breaking computer vision workflows. One issue [@px4-45077] describes hardware encoding errors in Gazebo camera plugins. 

Advanced navigation implementation rreportatly has issues. One issue[@px4-43683] reports terrain following that "does not work" in PX4 Gazebo despite being a documented feature. One user[@px4-43527] asks about optical flow without GPS but can't find clear implementation instructions.[@px4-47156] requests RTABMAP SLAM integration with Gazebo Harmonic, while [@px4-36406] addresses Hector SLAM for GPS-denied scenarios. 

#### Alternative Simulator Integration

Users seek integration with non-Gazebo simulators but face interfacing issues. A user[@px4-42508] requests Unity integration, while another[@px4-45970] reports inability to connect MAVSDK with PX4 SITL in AirSim/Unreal Engine. Multiple issues[@px4-42303; @px4-44244; @px4-25459; @px4-43561; @px4-46425] describe problems with MATLAB/Simulink integration, an important platform for control system development in aerospace. One user[@px4-44512] requests integration with Simcenter Amesim.

[@px4-47152] asks about "custom simulator in SITL," highlighting that the current architecture assumes Gazebo. The response of another forumpost[@px4-41775] confirms that simulators running slower than real-time are fundamentally incompatible with PX4's lockstep scheduler. 

#### Docker and Deployment

Containerized simulation shows deployment challenges. One issue[@px4-46059] reports generic failures when running PX4 SITL in containers, while another[@px4-32048] describes connection problems with dockerized simulations. Specifically one post[@px4-45983] notes video feeds fail to forward from Docker containers—a critical limitation for headless server deployments or cloud-based simulation infrastructure.

Graphics rendering issues compound Docker problems. One post[@px4-44619] reports Gazebo entities that spawn successfully but remain invisible, while anotehr describes[@px4-39733] Gazebo failing to load entirely. One issue shows general Gazebo startup failures[@px4-43070], and another[@px4-45702] addresses VM-specific challenges. 

#### World and Environment

Custom world integration lacks robustness. There have been reports[@px4-43167; @px4-46990; @px4-47171] that QGroundControl failing to connect when using custom world files, despite the simulation appearing to run correctly. One user[@px4-47409] indicates that custom worlds cause magnetometer initialization problems in v1.16, requiring manual parameter adjustments that aren't documented. One post[@px4-43738] addresses version compatibility with custom worlds, while another user[@px4-46242] reports arming failures in custom environments.

Environmental effects show limited support. A user[@px4-42846] asks how to simulate altitude effects on lift—fundamental for high-altitude operations, while another user[@px4-45696] reports the documented windy environment command (`make px4_sitl gz_x500_windy`) fails to produce wind effects.

#### Parameter and Configuration

Parameter access and modification during simulation have been reported to cause issues too. One user reports[@px4-47359] reports MAVLink commands failing to return complete parameter sets, breaking automated configuration tools. [@px4-47399] asks about changing MAVLink ports for multiple ground stations but finds the process undocumented. [@px4-40908] addresses parameter access in offboard mode, while [@px4-41678] requests PWM configuration guidance.

Simulation-specific configurations seem to cause confusion. One user[@px4-42119] requests the ability to disable failsafes during testing but finds no supported mechanism. Another user[@px4-42015] asks whether drone instances can start in "clean state" regardless of previous flights, important for reproducible experiments. A forum post[@px4-42586] describes time synchronization problems between components, while another[@px4-41998] questions network configuration options. A user[@px4-42754] requests GPS disabling for VIO testing, while another[@px4-43097] addresses external odometry configuration, and another user[@px4-47082] seeks to disable Gazebo's odometry publisher. Several other (support) request have been made like highlights sensor frame orientation challenges[@px4-46035],  arbitrary state initialization for ML[@px4-43846], and  external vision aiding issues [@px4-44400]. Several users are addressing data-bridging issues [@px4-43777; @px4-46164; @px4-46632; @px4-46694]. Additional configuration issues are reported as well[@px4-46698; @px4-46856; @px4-44060; @px4-46000; @px4-47434]. 