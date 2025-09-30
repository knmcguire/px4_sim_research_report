# Forum Analysis: PX4 Simulation Integration Issues

## Executive Summary

This analysis examines 152 forum posts from the PX4 discussion forum (discuss.px4.io) spanning the past year (2024-2025) to identify pressing issues in simulation integration. The posts were categorized into ten priority areas based on technical depth, impact severity, and relevance to simulation integration. The analysis reveals that multi-vehicle simulation scalability, EKF positioning stability, and ROS2 integration reliability emerge as the most critical concerns affecting users. These findings will inform a subsequent user survey to validate development priorities and resource allocation for simulation improvements.

## Methodology

The forum posts were sourced from discuss.px4.io, covering discussions from September 2024 through March 2025. The analysis followed a systematic approach:

1. **Issue Categorization**: Posts were examined for technical depth, reproducibility, and relevance to simulation integration. Posts were categorized based on the primary technical domain affected (e.g., multi-vehicle support, sensor simulation, platform compatibility).

2. **Priority Assessment**: Issues were ranked considering frequency of occurrence, severity of impact (blocking vs. degraded functionality), and alignment with common use cases in the PX4 ecosystem.

This methodology identified 152 substantive technical issues warranting developer attention, organized into ten priority categories to guide development roadmap decisions.

## Key Findings

### Critical Breaking Issues

The most urgent category involves regressions introduced in recent PX4 versions.  This issues[@px4-41925] exemplifies this problem: parameters `SIM_GZ_HOME_LAT`, `SIM_GZ_HOME_LON`, and `SIM_GZ_HOME_ALT` were removed in v1.15.0, making it impossible to spawn drones at custom positions—a fundamental requirement for multi-vehicle simulations and mission testing. Similarly, there was a report[@px4-46594]  of that Hardware-in-the-Loop (HITL) actuators ceased functioning in v1.15.4, breaking a critical testing workflow for hardware validation.

Platform-specific build failures also fall into this critical category. Multiple users reported incompatibilities with macOS 15.0 (Sequoia) and difficulties with Apple Silicon builds. These issues are particularly problematic as they represent complete blockers: users cannot proceed with any simulation work until resolved. Several forum posts [@px4-40832][@px4-40889][@px4-43606][@px4-44661][@px4-44172][@px4-45887][@px4-46712] indicate systematic problems with build toolchains across different operating systems and versions.

### Core Simulation Stability

The Extended Kalman Filter (EKF) and positioning subsystems show recurring instability patterns. One discussion[@px4-40657] describes extreme position drift and jumping estimates—sometimes up to 50 meters—during basic hovering in a Docker-based Gazebo Harmonic setup. The user noted that "even when hovering, the copter experiences extreme drifts, which is very unusual for a simulation without wind." Similar reports[@px4-45701] [@px4-46410][@px4-45340], suggesting systematic problems with position estimation when using custom worlds, external visual odometry, or non-standard sensor configurations. There have also been additional EKF-related issues reported as well.[@px4-40696][@px4-41693][@px4-38605][@px4-42050][@px4-42291][@px4-42720][@px4-43607][@px4-41928]

Flight behavior issues frequently prevent basic operations. Multiple users report drones that arm successfully but fail to take off[@px4-43349][@px4-44266][@px4-44442], with some drones unable to climb above 0.1 meters despite proper command inputs. One forum post[@px4-39412] describes heavy drones that "climb unresponsively after takeoff," indicating problems with thrust-to-weight modeling or controller tuning in simulation. Another post[@px4-44460] reports takeoff failures after controller modifications, while a second post[@px4-45612] shows VTOL-specific takeoff problems. There are several other additional flight issues reported as well [@px4-45275][@px4-45842].

Timing and performance issues also affect simulation usability. A fundamental limitation was highlighted[@px4-47188]: custom simulators running slower than real-time cannot function with PX4 SITL due to lockstep timing assumptions. The user found their 15Hz sensor update rate caused EKF failures and failsafe triggers, as "PX4 expects ~50 Hz real-time updates." This constraint severely limits integration with high-fidelity physics simulators or resource-constrained environments. One forum post[@px4-43347] reports ROS subscribers dramatically slowing simulation, while another[@px4-44546] describes environment-specific crashes. There have been one discussion post[@px4-47475] that requests simulation speed improvements.

### Multi-Vehicle Simulation

Multi-vehicle simulation emerges as a critical pain point with both configuration complexity and performance issues. Issue [@px4-47532] reports startup times exceeding 20 minutes when launching multiple drones with Micro XRCE-DDS. The user describes how "while one instance is in that process [of creating DDS entities], the others remain waiting before they can establish their connection," creating a sequential bottleneck that scales poorly.

Configuration challenges compound performance problems. Users struggle with MAVLink port allocation (issue #24), distinguishing sensor topics between drones (issue #16), and setting unique spawn positions (issue #14). Issue #51 reports inability to arm multiple drones simultaneously in SITL, while issue #119 describes MAVSDK communication failures in multi-drone setups. These issues collectively indicate that multi-vehicle simulation lacks the robustness and documentation needed for swarm research and industrial applications.

### ROS2/MAVROS Integration

The ROS2 bridge exhibits systematic reliability problems affecting sensor data flow. A couple of forum posts[@px4-44447][@px4-44810] report failures in the ros_gz_bridge preventing camera image topics from reaching RViz2, despite the topics being visible in Gazebo's native tools. Also a problem was described that scan topics that never publish messages[@px4-47421], breaking SLAM toolbox integration. There have been several reports that also indicate similar sensor data failurs[@px4-47421][@px4-43428][@px4-43476]. One forum post[@px4-45529] describes problems launching ROS with PX4 SITL, and  reports general topic publication failures[@px4-45852]. Also, visual odometry topic issues have been reported[@px4-46126], while other reports shows the disconnect between Gazebo and ROS2 topic visibility[@px4-46979] . These communication failures force users to implement workarounds or abandon ROS2 integration entirely.

Offboard control through ROS2 shows inconsistent behavior. There have been a report[@px4-45073] that direct actuator control fails to respond, while another[@px4-42010] describes VTOL-specific offboard control challenges. One user[@px4-44630] notes frame convention problems with `MAV_FRAME_BODY_NED`, causing unexpected offsets. Several users[@px4-42506][@px4-46447] report general offboard mode difficulties. These issues suggest incomplete or inconsistent implementation of the MAVLink-to-ROS2 control path.

### Custom Models and Airframes

Users attempting to create custom vehicle models encounter inadequate documentation and unpredictable behavior. One post[@px4-43417] describes an octocopter that "only takes off at 0.8m and does not reach the desired altitude" after modifying mass and inertia properties, even with increased motor velocity limits. This suggests disconnects between physical model parameters and PX4's internal vehicle assumptions.

A user[@px4-46241] highlights the difficulty of determining correct motor constants for Gazebo models. Another support post[@px4-46132] identifies a potential bug in the GZ bridge ESC interface, where the relationship between PWM values and motor commands lacks clear physical meaning. A developer comment acknowledges: "The main problem is that there is no good model for an ESC...What is slightly not elegant is probably how this translates to rotor velocity or thrust." This architectural uncertainty makes accurate custom vehicle modeling unnecessarily difficult. One user has requested clearer motor parameter definitions[@px4-34747], while many others[@px4-40607][@px4-40575][@px4-43858][@px4-46547][@px4-6700][@px4-47541] represent various custom model creation challenges.

Specialized vehicle types show particular gaps. Multiple issues[@px4-46487][@px4-46582][@px4-46561] report VTOL tilt-rotors diving dangerously during transitions and one users[@px4-46838] notes reversible motors cannot actually reverse in SITL. One user[@px4-28805] describes coaxial octocopter simulation problems, while another post[@px4-32781] requests airship simulation support. Additional specialized vehicle issues[@px4-18807][@px4-42031][@px4-42077][@px4-42324][@px4-43654][@px4-5207][@px4-46457][@px4-46469][@px4-46758][@px4-47231][@px4-47263]. These suggest the simulation framework optimizes for standard quadcopters at the expense of other vehicle types.

### Sensor Simulation

Camera and vision sensors show inconsistent functionality. A couple of posts[@px4-42909][@px4-43155] report video streams that are "unavailable" despite proper configuration, breaking computer vision workflows. One user[@px4-45077] describes hardware encoding errors in Gazebo camera plugins, while others[@px4-45711][@px4-45952] highlight camera integration difficulties. One user[@px4-43035] addresses point cloud visualization challenges. The inability to reliably stream simulated camera data undermines visual navigation, object detection, and SLAM research.

Advanced navigation sensors face integration challenges. [@px4-43683] and [@px4-47022] report terrain following that "does not work" in PX4 Gazebo despite being a documented feature. [@px4-43527] asks about optical flow without GPS—a common real-world scenario—but receives no clear implementation path. [@px4-47156] requests RTABMAP SLAM integration with Gazebo Harmonic, while [@px4-36406] addresses Hector SLAM for GPS-denied scenarios. [@px4-45225] reports general sensor loading failures, and [@px4-45919] requests multi-sensor setup guidance. These gaps limit the simulation environment's utility for advanced autonomy research. show inconsistent functionality. Issues #59 and #64 report video streams that are "unavailable" despite proper configuration, breaking computer vision workflows. Issue #131 describes hardware encoding errors in Gazebo camera plugins. The inability to reliably stream simulated camera data undermines visual navigation, object detection, and SLAM research.

Advanced navigation sensors face integration challenges. Issue #141 reports terrain following that "does not work" in PX4 Gazebo despite being a documented feature. Issue #139 asks about optical flow without GPS—a common real-world scenario—but receives no clear implementation path. Issue #213 requests RTABMAP SLAM integration with Gazebo Harmonic, indicating demand for modern SLAM frameworks. These gaps limit the simulation environment's utility for advanced autonomy research.

### Alternative Simulator Integration

Users seek integration with non-Gazebo simulators but face insufficient interfaces. A user[@px4-42508] requests Unity integration, while another[@px4-45970] reports inability to connect MAVSDK with PX4 SITL in AirSim/Unreal Engine. Multiple issues[@px4-42303][@px4-44244][@px4-25459][@px4-43561][@px4-46425] describe problems with MATLAB/Simulink integration, an important platform for control system development in aerospace. One user[@px4-44512] requests integration with Simcenter Amesim.

[@px4-47152] asks about "custom simulator in SITL," highlighting that the current architecture assumes Gazebo. The response of another forumpost[@px4-41775] confirms that simulators running slower than real-time are fundamentally incompatible with PX4's lockstep scheduler. This inflexibility prevents integration with high-fidelity simulators common in aerospace (e.g., FlightGear, X-Plane) or game engines popular for reinforcement learning research.

### Docker and Deployment

Containerized simulation shows deployment challenges. One issue[@px4-46059] reports generic failures when running PX4 SITL in containers, while another[@px4-32048] describes connection problems with dockerized simulations. Specifically one post[@px4-45983] notes video feeds fail to forward from Docker containers—a critical limitation for headless server deployments or cloud-based simulation infrastructure.

Graphics rendering issues compound Docker problems. One post[@px4-44619] reports Gazebo entities that spawn successfully but remain invisible, while  describes[@px4-39733] Gazebo failing to load entirely. One issue shows general Gazebo startup failures[@px4-43070], and another[@px4-45702] addresses VM-specific challenges. These problems suggest OpenGL/EGL configuration difficulties in containerized environments, limiting the simulation's utility in CI/CD pipelines or distributed testing frameworks.

### World and Environment

Custom world integration lacks robustness. There have been reports[@px4-43167][@px4-46990][@px4-47171] that QGroundControl failing to connect when using custom world files, despite the simulation appearing to run correctly. One user[@px4-47409] indicates that custom worlds cause magnetometer initialization problems in v1.16, requiring manual parameter adjustments that aren't documented. One post[@px4-43738] addresses version compatibility with custom worlds, while another user[@px4-46242] reports arming failures in custom environments.

Environmental effects show limited support. A user[@px4-42846] asks how to simulate altitude effects on lift—fundamental for high-altitude operations, while another user[@px4-45696] reports the documented windy environment command (`make px4_sitl gz_x500_windy`) fails to produce wind effects.

### Parameter and Configuration

Parameter access and modification during simulation shows gaps. One user reports[@px4-47359] reports `PARAM_REQUEST_LIST` MAVLink commands failing to return complete parameter sets, breaking automated configuration tools. [@px4-47399] asks about changing MAVLink ports for multiple ground stations but finds the process undocumented. [@px4-40908] addresses parameter access in offboard mode, while [@px4-41678] requests PWM configuration guidance.

Simulation-specific configurations lack flexibility. One user[@px4-42119] requests the ability to disable failsafes during testing—a reasonable development need—but finds no supported mechanism. Another user[@px4-42015] asks whether drone instances can start in "clean state" regardless of previous flights, important for reproducible experiments. A forum post[@px4-42586] describes time synchronization problems between components, while another[@px4-41998] questions network configuration options. A user[@px4-42754] requests GPS disabling for VIO testing, while another[@px4-43097] addresses external odometry configuration, and another user[@px4-47082] seeks to disable Gazebo's odometry publisher. Several other (support) request have been made like highlights sensor frame orientation challenges[@px4-46035],  arbitrary state initialization for ML[@px4-43846], and  external vision aiding issues [@px4-44400]. Several users are addressing data-bridging issues [@px4-43777][@px4-46164][@px4-46632][@px4-46694]. Additional configuration issues are reported as well[@px4-46698][@px4-46856][@px4-44060][@px4-46000][@px4-47434]. 


## Concluding remarks

The presence of multiple version-specific breaking changes (v1.14, v1.15.0, v1.15.4) indicates insufficient regression testing in the simulation domain. Features like custom spawn positions[@px4-41925] were removed without documented alternatives, suggesting simulation use cases aren't adequately represented in the development process. This pattern risks eroding user confidence in upgrading, fragmenting the community across incompatible versions.

Build failures concentrated on macOS—particularly Apple Silicon—reveal platform-specific testing gaps. Given macOS's popularity in robotics research and development, these failures represent a significant accessibility barrier. The lack of working Docker solutions exacerbates this by preventing macOS users from using containerized Linux environments as a workaround. The multitude of multi-vehicle support request seem to suggest the importantso of this feature. The 20-minute startup time for multi-drone simulations ([@px4-47532]) and numerous configuration difficulties might suggest that multi-vehicle support was added incrementally. Port conflicts, topic namespace collisions, and other initialization bottlenecks indicate the system architecture assumes single-vehicle operation. This fundamentally limits PX4's applicability to swarm robotics and multi-agent research.

There has also been a high frequency of ROS2 bridge failures reported suggests this integration path would need additional work. The disconnect between topics visible in Gazebo versus ROS2, combined with offboard control inconsistencies, indicates incomplete abstraction between the simulation and robotics middleware. This is particularly concerning given ROS2's importance in the robotics research community. In the forum, recurring "how do I" questions about several features (terrain following, optical flow, custom models) suggest that users find the documentation or tutorials a bit hard to find, or that it does not doesn't match actual system behavior as described. 

## References


