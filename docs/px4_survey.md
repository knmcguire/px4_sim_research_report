# Forum Analysis: PX4 Simulation Integration Issues

## Executive Summary

This analysis examines 152 forum posts from the PX4 discussion forum (discuss.px4.io) spanning the past year (2024-2025) to identify pressing issues in simulation integration. The posts were categorized into ten priority areas based on technical depth, impact severity, and relevance to simulation integration. The analysis reveals that multi-vehicle simulation scalability, EKF positioning stability, and ROS2 integration reliability emerge as the most critical concerns affecting users. These findings will inform a subsequent user survey to validate development priorities and resource allocation for simulation improvements.

## Methodology

The forum posts were sourced from discuss.px4.io, covering discussions from September 2024 through March 2025. The analysis followed a systematic approach:

1. **Issue Categorization**: Posts were examined for technical depth, reproducibility, and relevance to simulation integration. Posts were categorized based on the primary technical domain affected (e.g., multi-vehicle support, sensor simulation, platform compatibility).

2. **Priority Assessment**: Issues were ranked considering frequency of occurrence, severity of impact (blocking vs. degraded functionality), and alignment with common use cases in the PX4 ecosystem.

This methodology identified 152 substantive technical issues warranting developer attention, organized into ten priority categories to guide development roadmap decisions.

## Key Findings

### Critical Breaking Issues (Priority 1)

The most urgent category involves regressions introduced in recent PX4 versions. [Issue #1](https://discuss.px4.io/t/impossible-custom-spawn-position-in-sitl-gazebo-since-v1-15-0/41925) exemplifies this problem: parameters `SIM_GZ_HOME_LAT`, `SIM_GZ_HOME_LON`, and `SIM_GZ_HOME_ALT` were removed in v1.15.0, making it impossible to spawn drones at custom positions—a fundamental requirement for multi-vehicle simulations and mission testing. Similarly, [issue #2](https://discuss.px4.io/t/hil-actuators-not-working-on-px4-v1-15-4/46594) reports that Hardware-in-the-Loop (HITL) actuators ceased functioning in v1.15.4, breaking a critical testing workflow for hardware validation.

Platform-specific build failures also fall into this critical category. Multiple users reported incompatibilities with macOS 15.0 (Sequoia) and difficulties with Apple Silicon builds. These issues are particularly problematic as they represent complete blockers: users cannot proceed with any simulation work until resolved. [Issue #3](https://discuss.px4.io/t/error-in-mac-toolchain-instructions/40832), [issue #4](https://discuss.px4.io/t/mac-os-15-0/40889), [issue #5](https://discuss.px4.io/t/gz-garden-install-error/43606), [issue #6](https://discuss.px4.io/t/protoc-error-on-build/44661), [issue #7](https://discuss.px4.io/t/simulation-tools-installtion-fail-on-osx/44172), [issue #8](https://discuss.px4.io/t/px4-setup-for-macos-m3-sequoia/45887), and [issue #9](https://discuss.px4.io/t/cmake-error-in-px4/46712) collectively indicate systematic problems with build toolchains across different operating systems and versions.

### Core Simulation Stability (Priority 2)

The Extended Kalman Filter (EKF) and positioning subsystems show recurring instability patterns. [Issue #10](https://discuss.px4.io/t/unexpected-imprecise-attitude-in-sitl/40657) describes extreme position drift and jumping estimates—sometimes up to 50 meters—during basic hovering in a Docker-based Gazebo Harmonic setup. The user noted that "even when hovering, the copter experiences extreme drifts, which is very unusual for a simulation without wind." Similar reports appear in [issue #11](https://discuss.px4.io/t/gazebo-harmonic-sitl-external-pose-input-drifts/45701), [issue #12](https://discuss.px4.io/t/gazebo-vio-setup-commander-takeoff-denied-due-to-invalid-position-estimate/46410), and [issue #13](https://discuss.px4.io/t/gazebo-simulation-px4v1-15-4-gps-yaw-errors-even-before-take-off/45340), suggesting systematic problems with position estimation when using custom worlds, external visual odometry, or non-standard sensor configurations. Additional EKF-related issues include [issue #14](https://discuss.px4.io/t/ekf2-no-available-instance/40696), [issue #15](https://discuss.px4.io/t/ekf2-replay-results-dont-match/41693), [issue #16](https://discuss.px4.io/t/height-estimate-not-stable-ekf2-missing-data/38605), [issue #17](https://discuss.px4.io/t/px4-sitl-heading-estimate-not-stable-omnicopter/42050), [issue #18](https://discuss.px4.io/t/how-can-i-make-a-drone-that-is-far-away-from-the-origin-estimate-its-position/42291), [issue #19](https://discuss.px4.io/t/issue-with-drone-local-position-in-px4-sitl-on-gazebo-simulation/42720), [issue #20](https://discuss.px4.io/t/position-errors-when-using-vehicle-visual-odometry/43607), and [issue #21](https://discuss.px4.io/t/gps-vertical-pos-drift-too-high-while-running-sitl-on-modified-world/41928).

Flight behavior issues frequently prevent basic operations. Multiple users report drones that arm successfully but fail to take off ([issue #22](https://discuss.px4.io/t/drone-arm-but-not-takeoff-sitl-gazebo/43349), [issue #23](https://discuss.px4.io/t/px4-sitl-drone-not-climbing-above-0-1m-during-takeoff/44266), [issue #24](https://discuss.px4.io/t/using-gazebo-to-simulate-the-drone-does-not-take-off/44442)), with some drones unable to climb above 0.1 meters despite proper command inputs. [Issue #25](https://discuss.px4.io/t/heavy-drone-climbs-unresponsively-after-takeoff-in-px4-sitl-gazebo/39412) describes heavy drones that "climb unresponsively after takeoff," indicating problems with thrust-to-weight modeling or controller tuning in simulation. [Issue #26](https://discuss.px4.io/t/after-replacing-multicopter-rate-controller-the-quadrotor-cannot-take-off/44460) reports takeoff failures after controller modifications, while [issue #27](https://discuss.px4.io/t/custom-vtol-cannot-takeoff-px4-sitl-with-gazebo-sim/45612) shows VTOL-specific takeoff problems. Additional flight issues include [issue #28](https://discuss.px4.io/t/sitl-drone-cannot-fly-due-to-qgc-not-ready-status/45275) and [issue #29](https://discuss.px4.io/t/cannot-arm-in-mission-mode-with-sitl/45842).

Timing and performance issues also affect simulation usability. [Issue #30](https://discuss.px4.io/t/slow-simulator-does-not-work-in-sitl/47188) highlights a fundamental limitation: custom simulators running slower than real-time cannot function with PX4 SITL due to lockstep timing assumptions. The user found their 15Hz sensor update rate caused EKF failures and failsafe triggers, as "PX4 expects ~50 Hz real-time updates." This constraint severely limits integration with high-fidelity physics simulators or resource-constrained environments. [Issue #31](https://discuss.px4.io/t/ros-subscriber-slowing-sim-down/43347) reports ROS subscribers dramatically slowing simulation, while [issue #32](https://discuss.px4.io/t/sitl-drone-crash-in-vscode-but-not-from-command-line/44546) describes environment-specific crashes. [Issue #33](https://discuss.px4.io/t/gazebo-sim-speed-up/47475) requests simulation speed improvements.

### Multi-Vehicle Simulation (Priority 3)

Multi-vehicle simulation emerges as a critical pain point with both configuration complexity and performance issues. Issue #240 reports startup times exceeding 20 minutes when launching multiple drones with Micro XRCE-DDS. The user describes how "while one instance is in that process [of creating DDS entities], the others remain waiting before they can establish their connection," creating a sequential bottleneck that scales poorly.

Configuration challenges compound performance problems. Users struggle with MAVLink port allocation (issue #24), distinguishing sensor topics between drones (issue #16), and setting unique spawn positions (issue #14). Issue #51 reports inability to arm multiple drones simultaneously in SITL, while issue #119 describes MAVSDK communication failures in multi-drone setups. These issues collectively indicate that multi-vehicle simulation lacks the robustness and documentation needed for swarm research and industrial applications.

### ROS2/MAVROS Integration (Priority 4)

The ROS2 bridge exhibits systematic reliability problems affecting sensor data flow. [Issue #52](https://discuss.px4.io/t/ros-gz-bridge-not-working-unable-to-use-rviz2-to-fetch-px4-x500-mono-cam-image-topic/44447) and [issue #53](https://discuss.px4.io/t/ros-gz-bridge-not-working-unable-to-use-rviz2-to-fetch-px4-gazebo-x500-mono-cam-image-topic/44810) report failures in the ros_gz_bridge preventing camera image topics from reaching RViz2, despite the topics being visible in Gazebo's native tools. [Issue #54](https://discuss.px4.io/t/why-is-my-ros2-scan-topic-not-publishing-any-messages-slam-toolbox-lifecycle-fails-python-subscriber-inactive/47421) describes scan topics that never publish messages, breaking SLAM toolbox integration. [Issue #55](https://discuss.px4.io/t/not-able-to-get-the-camera-or-sensor-data-from-ros2-topics-to-avoid-obstacles/43428) reports similar sensor data failures, while [issue #56](https://discuss.px4.io/t/gz-x500-lidar-2d-cant-publish-scan/43476) specifically affects lidar. [Issue #57](https://discuss.px4.io/t/issue-when-launching-ros-with-px4-sitl-after-successful-gazebo-simulation/45529) describes problems launching ROS with PX4 SITL, and [issue #58](https://discuss.px4.io/t/px4-sitl-sensor-datas-arent-published-by-topic/45852) reports general topic publication failures. [Issue #59](https://discuss.px4.io/t/ros2-px4-1-fmu-in-vehicle-visual-odometry-topic-subscribe-issue/46126) highlights visual odometry topic issues, while [issue #60](https://discuss.px4.io/t/how-to-see-px4-gazebo-camera-topic-in-ros-2-foxy-can-see-in-gz-topic-but-not-ros2-topic/46979) shows the disconnect between Gazebo and ROS2 topic visibility. These communication failures force users to implement workarounds or abandon ROS2 integration entirely.

Offboard control through ROS2 shows inconsistent behavior. [Issue #61](https://discuss.px4.io/t/ros2-offboard-control-direct-actuator-control-not-working/45073) reports that direct actuator control fails to respond, while [issue #62](https://discuss.px4.io/t/about-the-offboard-control-of-vtol-by-ros-2/42010) describes VTOL-specific offboard control challenges. [Issue #63](https://discuss.px4.io/t/offset-issue-in-offboard-mode-with-mav-frame-body-ned-and-mavlink/44630) notes frame convention problems with `MAV_FRAME_BODY_NED`, causing unexpected offsets. [Issue #64](https://discuss.px4.io/t/offboard-mode-with-px4-hitl-mavros-and-qgc/42506) and [issue #65](https://discuss.px4.io/t/offboard-mode-in-sitl-with-jmavsim/46447) report general offboard mode difficulties. These issues suggest incomplete or inconsistent implementation of the MAVLink-to-ROS2 control path.

### Custom Models and Airframes (Priority 5)

Users attempting to create custom vehicle models encounter inadequate documentation and unpredictable behavior. [Issue #66](https://discuss.px4.io/t/px4-sitl-gazebo-harmonic-modify-physical-properties/43417) describes an octocopter that "only takes off at 0.8m and does not reach the desired altitude" after modifying mass and inertia properties, even with increased motor velocity limits. This suggests disconnects between physical model parameters and PX4's internal vehicle assumptions.

[Issue #67](https://discuss.px4.io/t/determining-motor-constants-for-gazebo-and-px4-from-an-actual-motor/46241) highlights the difficulty of determining correct motor constants for Gazebo models. [Issue #68](https://discuss.px4.io/t/potential-bug-in-px4-gz-bridge-esc-interface/46132) identifies a potential bug in the GZ bridge ESC interface, where the relationship between PWM values and motor commands lacks clear physical meaning. A developer comment acknowledges: "The main problem is that there is no good model for an ESC...What is slightly not elegant is probably how this translates to rotor velocity or thrust." This architectural uncertainty makes accurate custom vehicle modeling unnecessarily difficult. [Issue #69](https://discuss.px4.io/t/gazebo-sdf-file-motor-parameters-definitions/34747) requests clearer motor parameter definitions, while [issue #70](https://discuss.px4.io/t/creating-multiple-components/40607), [issue #71](https://discuss.px4.io/t/simulating-drone-with-rangefinder/40575), [issue #72](https://discuss.px4.io/t/adding-custom-model-in-gazebo-classic/43858), [issue #73](https://discuss.px4.io/t/create-custom-airframe-for-sitl/46547), [issue #74](https://discuss.px4.io/t/create-custom-model-for-sitl/6700/41), and [issue #75](https://discuss.px4.io/t/adding-a-custom-gazebo-model-that-works-with-px4/47541) represent various custom model creation challenges.

Specialized vehicle types show particular gaps. Multiple issues ([issue #76](https://discuss.px4.io/t/tiltrotor-vtol-dive-on-transition/46487), [issue #77](https://discuss.px4.io/t/tri-tiltrotor-vtol-dive-on-transition/46582), [issue #78](https://discuss.px4.io/t/hitl-vtol-transition/46561)) report VTOL tilt-rotors diving dangerously during transitions. [Issue #79](https://discuss.px4.io/t/reversible-motor-in-sitl-not-able-to-reverse/46838) notes reversible motors cannot actually reverse in SITL. [Issue #80](https://discuss.px4.io/t/coaxial-octocopter-gazebo-simulation-problems/28805) describes coaxial octocopter simulation problems, while [issue #81](https://discuss.px4.io/t/simulating-custom-airship-in-gazebo/32781) requests airship simulation support. Additional specialized vehicle issues include [issue #82](https://discuss.px4.io/t/using-gazebo-motor-failure-plugin-in-gazebo-simulation/18807), [issue #83](https://discuss.px4.io/t/drone-motor-failure-simulation/42031), [issue #84](https://discuss.px4.io/t/custom-controlallocation-logic-in-case-of-rotor-failure/42077), [issue #85](https://discuss.px4.io/t/px4-sitl-jsbsim-makes-rolling-airplane/42324), [issue #86](https://discuss.px4.io/t/state-of-jsbsim-sitl-for-fixed-wing-rascal-model/43654), [issue #87](https://discuss.px4.io/t/dual-tailsitter-gazebo-hover-simulation/5207/11), [issue #88](https://discuss.px4.io/t/omnicopter-simulation-in-gazebo/46457), [issue #89](https://discuss.px4.io/t/px4-autopilot-with-8-lift-motors-and-1-pusher-motor/46469), [issue #90](https://discuss.px4.io/t/fixed-wing-control-in-offboard-mode/46758), [issue #91](https://discuss.px4.io/t/simulating-px4-with-servo-motors/47231), and [issue #92](https://discuss.px4.io/t/simulate-given-stability-derivatives-onto-a-generic-plane/47263). These suggest the simulation framework optimizes for standard quadcopters at the expense of other vehicle types.

### Sensor Simulation (Priority 6)

Camera and vision sensors show inconsistent functionality. [Issue #93](https://discuss.px4.io/t/px4-sitl-video-stream-unavailable/42909) and [issue #94](https://discuss.px4.io/t/px4-sitl-video-stream-unavailable-on-udp-5600/43155) report video streams that are "unavailable" despite proper configuration, breaking computer vision workflows. [Issue #95](https://discuss.px4.io/t/drone-camera-hardware-encoding-error-in-gazebo/45077) describes hardware encoding errors in Gazebo camera plugins, while [issue #96](https://discuss.px4.io/t/need-help-with-integrating-camera-to-px4-gazebo-simulation/45711) and [issue #97](https://discuss.px4.io/t/how-to-use-iris-depth-camera/45952) highlight camera integration difficulties. [Issue #98](https://discuss.px4.io/t/visualisation-of-point-cloud-data-of-depth-camera-via-rviz2/43035) addresses point cloud visualization challenges. The inability to reliably stream simulated camera data undermines visual navigation, object detection, and SLAM research.

Advanced navigation sensors face integration challenges. [Issue #99](https://discuss.px4.io/t/terrain-following-not-working-in-px4-gazebo-simulation-environment/43683) and [issue #100](https://discuss.px4.io/t/terrain-following-is-not-working-in-px4-autopilot-software/47022) report terrain following that "does not work" in PX4 Gazebo despite being a documented feature. [Issue #101](https://discuss.px4.io/t/how-to-fly-a-quadcopter-using-optical-flow-without-gps-in-the-gazebo-garden-simulation-environment/43527) asks about optical flow without GPS—a common real-world scenario—but receives no clear implementation path. [Issue #102](https://discuss.px4.io/t/rtabmap-slam-in-gazebo-harmonic/47156) requests RTABMAP SLAM integration with Gazebo Harmonic, while [issue #103](https://discuss.px4.io/t/gazebo-simulation-hector-slam-for-position-estimation-of-gps-denied-drone/36406) addresses Hector SLAM for GPS-denied scenarios. [Issue #104](https://discuss.px4.io/t/cant-get-sensors-to-load-in-gazebo-stand-alone-mode/45225) reports general sensor loading failures, and [issue #105](https://discuss.px4.io/t/how-to-setup-multiple-distance-sensors-in-px4-gazebo-sitl/45919) requests multi-sensor setup guidance. These gaps limit the simulation environment's utility for advanced autonomy research. show inconsistent functionality. Issues #59 and #64 report video streams that are "unavailable" despite proper configuration, breaking computer vision workflows. Issue #131 describes hardware encoding errors in Gazebo camera plugins. The inability to reliably stream simulated camera data undermines visual navigation, object detection, and SLAM research.

Advanced navigation sensors face integration challenges. Issue #141 reports terrain following that "does not work" in PX4 Gazebo despite being a documented feature. Issue #139 asks about optical flow without GPS—a common real-world scenario—but receives no clear implementation path. Issue #213 requests RTABMAP SLAM integration with Gazebo Harmonic, indicating demand for modern SLAM frameworks. These gaps limit the simulation environment's utility for advanced autonomy research.

### Alternative Simulator Integration (Priority 7)

Users seek integration with non-Gazebo simulators but face insufficient interfaces. [Issue #106](https://discuss.px4.io/t/integrate-px4-and-unity/42508) requests Unity integration, while [issue #107](https://discuss.px4.io/t/cant-make-mavsdk-commuincate-with-px4-sitl-in-airsim-unreal-engine/45970) reports inability to connect MAVSDK with PX4 SITL in AirSim/Unreal Engine. Multiple issues ([issue #108](https://discuss.px4.io/t/px4-sitl-with-simulink-gazebo/42303), [issue #109](https://discuss.px4.io/t/px4-doesnt-takeoff-in-sitl-with-simulink-in-jmavsim/44244), [issue #110](https://discuss.px4.io/t/px4-sitl-with-matlab-simulink-model/25459), [issue #111](https://discuss.px4.io/t/issue-with-running-and-monitoring-the-px4-host-target-and-jmavsim-in-simulink/43561), [issue #112](https://discuss.px4.io/t/help-with-px4-sitl-simulink-connection/46425)) describe problems with MATLAB/Simulink integration, an important platform for control system development in aerospace. [Issue #113](https://discuss.px4.io/t/px4-control-with-simcenter-amesim-simulation-software/44512) requests integration with Simcenter Amesim.

[Issue #114](https://discuss.px4.io/t/custom-simulator-in-sitl/47152) asks about "custom simulator in SITL," highlighting that the current architecture assumes Gazebo. The response to issue #30 confirms that simulators running slower than real-time are fundamentally incompatible with PX4's lockstep scheduler. This inflexibility prevents integration with high-fidelity simulators common in aerospace (e.g., FlightGear, X-Plane) or game engines popular for reinforcement learning research.

### Docker and Deployment (Priority 8)

Containerized simulation shows deployment challenges. [Issue #115](https://discuss.px4.io/t/issue-running-px4-sitl-in-a-container/46059) reports generic failures when running PX4 SITL in containers, while [issue #116](https://discuss.px4.io/t/unable-to-connect-dockerized-simulation/32048) describes connection problems with dockerized simulations. [Issue #117](https://discuss.px4.io/t/running-sim-on-a-vm-in-a-docker-container/45983) specifically notes video feeds fail to forward from Docker containers—a critical limitation for headless server deployments or cloud-based simulation infrastructure.

Graphics rendering issues compound Docker problems. [Issue #118](https://discuss.px4.io/t/gazebo-entities-not-rendered/44619/3) reports Gazebo entities that spawn successfully but remain invisible, while [issue #119](https://discuss.px4.io/t/gazebo-not-loading/39733/4) describes Gazebo failing to load entirely. [Issue #120](https://discuss.px4.io/t/cannot-start-gazebo-simulation-besides-gz-xxx/43070) shows general Gazebo startup failures, and [issue #121](https://discuss.px4.io/t/how-to-run-gazebo-from-px4-running-on-vm-multipass/45702) addresses VM-specific challenges. These problems suggest OpenGL/EGL configuration difficulties in containerized environments, limiting the simulation's utility in CI/CD pipelines or distributed testing frameworks.

### World and Environment (Priority 9)

Custom world integration lacks robustness. [Issue #122](https://discuss.px4.io/t/qgc-not-connected-to-custom-drone-urdf/43167), [issue #123](https://discuss.px4.io/t/qgc-does-not-connect-to-px4-sitl-in-custom-world/46990), and [issue #124](https://discuss.px4.io/t/qgc-not-connecting-to-the-vehicle-in-custom-world-for-sitl/47171) report QGroundControl failing to connect when using custom world files, despite the simulation appearing to run correctly. [Issue #125](https://discuss.px4.io/t/using-a-custom-world-environment-in-px4-v1-16/47409/4) indicates that custom worlds cause magnetometer initialization problems in v1.16, requiring manual parameter adjustments that aren't documented. [Issue #126](https://discuss.px4.io/t/updating-px4-version-in-a-gazebo-simulation/43738) addresses version compatibility with custom worlds, while [issue #127](https://discuss.px4.io/t/px4-gazebo-harmonic-gz-x500-fails-to-arm-in-custom-warehouse-world/46242) reports arming failures in custom environments.

Environmental effects show limited support. [Issue #128](https://discuss.px4.io/t/how-to-simulate-the-effect-of-altitude-on-quad-lift/42846) asks how to simulate altitude effects on lift—fundamental for high-altitude operations—but receives no clear answer. [Issue #129](https://discuss.px4.io/t/unable-to-simulate-wind-via-make-px4-sitl-gz-x500-windy/45696) reports the documented windy environment command (`make px4_sitl gz_x500_windy`) fails to produce wind effects. These limitations prevent realistic testing of environmental robustness.

### Parameter and Configuration (Priority 10)

Parameter access and modification during simulation shows gaps. [Issue #130](https://discuss.px4.io/t/param-request-list-does-not-return-a-list-of-all-parameters/47359) reports `PARAM_REQUEST_LIST` MAVLink commands failing to return complete parameter sets, breaking automated configuration tools. [Issue #131](https://discuss.px4.io/t/change-px4-sitl-gazebo-ports-for-gcs-and-api/47399) asks about changing MAVLink ports for multiple ground stations but finds the process undocumented. [Issue #132](https://discuss.px4.io/t/how-to-access-px4-parameters-in-offboard-mode/40908/5) addresses parameter access in offboard mode, while [issue #133](https://discuss.px4.io/t/how-to-change-pwm-value-and-saturation-in-sils-or-gazebo/41678) requests PWM configuration guidance.

Simulation-specific configurations lack flexibility. [Issue #134](https://discuss.px4.io/t/disabling-failsafe-option-for-simulation/42119) requests the ability to disable failsafes during testing—a reasonable development need—but finds no supported mechanism. [Issue #135](https://discuss.px4.io/t/is-it-possible-to-create-drone-instances-in-a-clean-state-regardless-of-past-flight-missions/42015) asks whether drone instances can start in "clean state" regardless of previous flights, important for reproducible experiments. [Issue #136](https://discuss.px4.io/t/how-to-make-time-syncrhronization-before-start-simulator/42586) describes time synchronization problems between components, while [issue #137](https://discuss.px4.io/t/tcp-port-open-vs-closed-for-simulation-env/41998) questions network configuration options. [Issue #138](https://discuss.px4.io/t/disable-gps-to-use-vio/42754) requests GPS disabling for VIO testing, [issue #139](https://discuss.px4.io/t/use-external-odometry-in-enu-for-px4/43097) addresses external odometry configuration, and [issue #140](https://discuss.px4.io/t/disabling-gazebo-odometry-publisher-px4-link/47082) seeks to disable Gazebo's odometry publisher. [Issue #141](https://discuss.px4.io/t/sensor-frame-orientation-custom-simulation/46035) highlights sensor frame orientation challenges, [issue #142](https://discuss.px4.io/t/setting-px4-to-an-arbitrary-state-for-machine-learning-simulations/43846) requests arbitrary state initialization for ML, and [issue #143](https://discuss.px4.io/t/px4-external-vision-aiding-with-gazebo-dynamic-pose-issue-with-position-reset/44400) reports external vision aiding issues. [Issue #144](https://discuss.px4.io/t/send-position-from-ros2-topics-to-mavlink-messages/43777) and [issue #145](https://discuss.px4.io/t/gps-to-non-gps-transition-using-ros2/46164) address data bridging challenges, [issue #146](https://discuss.px4.io/t/gz-bridge-failed-to-start-and-spawn-model/46632) reports bridge startup failures, and [issue #147](https://discuss.px4.io/t/px4-sitl-to-gazebo-rotor-velocity-bridge/46694) questions rotor velocity bridging. Additional configuration issues include [issue #148](https://discuss.px4.io/t/drone-position-hold-non-gps-using-aruco-detection/46698), [issue #149](https://discuss.px4.io/t/gps-jamming-issue/46856), [issue #150](https://discuss.px4.io/t/px4-gazebo-static-maps-plugin/44060), [issue #151](https://discuss.px4.io/t/segmentation-fault-or-timeout-caused-by-the-combination-of-multiple-parameters/46000), and [issue #152](https://discuss.px4.io/t/training-dl-model-on-imu-ground-truth-gps-denied-simulation-and-vision-pose-integration-in-px4-sitl/47434). These issues indicate the simulation environment doesn't adequately support the iterative development workflows users need.

## Patterns and Implications

### Regression Management

The presence of multiple version-specific breaking changes (v1.14, v1.15.0, v1.15.4) indicates insufficient regression testing in the simulation domain. Features like custom spawn positions ([issue #1](https://discuss.px4.io/t/impossible-custom-spawn-position-in-sitl-gazebo-since-v1-15-0/41925)) were removed without documented alternatives, suggesting simulation use cases aren't adequately represented in the development process. This pattern risks eroding user confidence in upgrading, fragmenting the community across incompatible versions.

### Platform Diversity Challenges

Build failures concentrated on macOS—particularly Apple Silicon—reveal platform-specific testing gaps. Given macOS's popularity in robotics research and development, these failures represent a significant accessibility barrier. The lack of working Docker solutions exacerbates this by preventing macOS users from using containerized Linux environments as a workaround.

### Multi-Vehicle as an Afterthought

The 20-minute startup time for multi-drone simulations ([issue #34](https://discuss.px4.io/t/slow-startup-of-multiple-px4-sitl-instances-with-micro-xrce-dds-agent-multi-drone-setup/47532)) and numerous configuration difficulties suggest multi-vehicle support was added incrementally rather than designed architecturally. Port conflicts, topic namespace collisions, and sequential initialization bottlenecks indicate the system architecture assumes single-vehicle operation. This fundamentally limits PX4's applicability to swarm robotics and multi-agent research.

### ROS2 Integration Maturity

The frequency of ROS2 bridge failures suggests this integration path hasn't achieved production readiness despite being heavily promoted. The disconnect between topics visible in Gazebo versus ROS2, combined with offboard control inconsistencies, indicates incomplete abstraction between the simulation and robotics middleware. This is particularly concerning given ROS2's importance in the robotics research community.

### Documentation Gaps

Recurring "how do I" questions about documented features (terrain following, optical flow, custom models) suggest documentation either doesn't exist, is hard to find, or doesn't match actual system behavior. The gap between advertised capabilities and user ability to utilize them represents a significant usability barrier.

## Preliminary Survey Focus Areas

Based on this analysis, the forthcoming user survey should prioritize validation of these key areas:

**Experience Metrics**: Installation ease, error message clarity, time to first successful simulation, and update stability will provide quantitative baselines for usability issues identified qualitatively in forums.

**Critical Functionality**: Multi-vehicle reliability, takeoff/flight behavior consistency, ROS2 integration stability, and position estimation accuracy should be directly rated by users to confirm severity and prevalence.

**Feature Importance**: Users should rank the relative importance of improvements in areas like multi-drone support, custom model workflows, alternative simulator integration, and platform compatibility to guide resource allocation.

**Use Case Coverage**: Understanding whether users primarily need basic vehicle testing, swarm simulations, vision-based autonomy, or advanced control research will help prioritize which gaps have the broadest impact.

The survey will validate whether the patterns observed in forum posts represent widespread issues or edge cases affecting only vocal minorities. This empirical foundation will enable evidence-based prioritization of simulation integration improvements.

## References

### Priority 1: Critical Breaking Issues & Regressions
1. https://discuss.px4.io/t/impossible-custom-spawn-position-in-sitl-gazebo-since-v1-15-0/41925
2. https://discuss.px4.io/t/hil-actuators-not-working-on-px4-v1-15-4/46594
3. https://discuss.px4.io/t/error-in-mac-toolchain-instructions/40832
4. https://discuss.px4.io/t/mac-os-15-0/40889
5. https://discuss.px4.io/t/gz-garden-install-error/43606
6. https://discuss.px4.io/t/protoc-error-on-build/44661
7. https://discuss.px4.io/t/simulation-tools-installtion-fail-on-osx/44172
8. https://discuss.px4.io/t/px4-setup-for-macos-m3-sequoia/45887
9. https://discuss.px4.io/t/cmake-error-in-px4/46712

### Priority 2: Core Simulation Stability
10. https://discuss.px4.io/t/unexpected-imprecise-attitude-in-sitl/40657
11. https://discuss.px4.io/t/gazebo-harmonic-sitl-external-pose-input-drifts/45701
12. https://discuss.px4.io/t/gazebo-vio-setup-commander-takeoff-denied-due-to-invalid-position-estimate/46410
13. https://discuss.px4.io/t/gazebo-simulation-px4v1-15-4-gps-yaw-errors-even-before-take-off/45340
14. https://discuss.px4.io/t/ekf2-no-available-instance/40696
15. https://discuss.px4.io/t/ekf2-replay-results-dont-match/41693
16. https://discuss.px4.io/t/height-estimate-not-stable-ekf2-missing-data/38605
17. https://discuss.px4.io/t/px4-sitl-heading-estimate-not-stable-omnicopter/42050
18. https://discuss.px4.io/t/how-can-i-make-a-drone-that-is-far-away-from-the-origin-estimate-its-position/42291
19. https://discuss.px4.io/t/issue-with-drone-local-position-in-px4-sitl-on-gazebo-simulation/42720
20. https://discuss.px4.io/t/position-errors-when-using-vehicle-visual-odometry/43607
21. https://discuss.px4.io/t/gps-vertical-pos-drift-too-high-while-running-sitl-on-modified-world/41928
22. https://discuss.px4.io/t/drone-arm-but-not-takeoff-sitl-gazebo/43349
23. https://discuss.px4.io/t/px4-sitl-drone-not-climbing-above-0-1m-during-takeoff/44266
24. https://discuss.px4.io/t/using-gazebo-to-simulate-the-drone-does-not-take-off/44442
25. https://discuss.px4.io/t/heavy-drone-climbs-unresponsively-after-takeoff-in-px4-sitl-gazebo/39412
26. https://discuss.px4.io/t/after-replacing-multicopter-rate-controller-the-quadrotor-cannot-take-off/44460
27. https://discuss.px4.io/t/custom-vtol-cannot-takeoff-px4-sitl-with-gazebo-sim/45612
28. https://discuss.px4.io/t/sitl-drone-cannot-fly-due-to-qgc-not-ready-status/45275
29. https://discuss.px4.io/t/cannot-arm-in-mission-mode-with-sitl/45842
30. https://discuss.px4.io/t/slow-simulator-does-not-work-in-sitl/47188
31. https://discuss.px4.io/t/ros-subscriber-slowing-sim-down/43347
32. https://discuss.px4.io/t/sitl-drone-crash-in-vscode-but-not-from-command-line/44546
33. https://discuss.px4.io/t/gazebo-sim-speed-up/47475

### Priority 3: Multi-Vehicle Simulation
34. https://discuss.px4.io/t/slow-startup-of-multiple-px4-sitl-instances-with-micro-xrce-dds-agent-multi-drone-setup/47532
35. https://discuss.px4.io/t/mavlink-ports-for-multiple-drones-using-gazebo-and-ros/41744
36. https://discuss.px4.io/t/how-to-distinguish-depth-camera-topics-for-multiple-drones-in-gazebo-harmonic/40885/3
37. https://discuss.px4.io/t/setting-custom-home-location-in-multi-vehicle-simulation/40847
38. https://discuss.px4.io/t/unable-to-arm-drones-in-multi-vehicle-sitl-setup-with-px4-and-microxrceagent/42697
39. https://discuss.px4.io/t/mavsdk-multiple-drones-problem/44693
40. https://discuss.px4.io/t/gazebo-multi-sim/42058
41. https://discuss.px4.io/t/error-spawning-multiple-drones-with-cameras-in-px4-sitl-and-gazebo-classic/42609
42. https://discuss.px4.io/t/spawn-px4-instances-of-same-drone-with-different-properties/42930
43. https://discuss.px4.io/t/multiple-drone-connection-in-qgroundcontrol-are-not-connecting-at-a-time/45546
44. https://discuss.px4.io/t/accel-0-timeout-error-in-swarm-uavs-with-ros2-uxrce-dds-and-gazebo-harmonic/46587
45. https://discuss.px4.io/t/how-to-obtain-the-correct-px4-instance-or-target-system-in-multi-vehicle-simulation-with-ros-2/45441
46. https://discuss.px4.io/t/trouble-with-ros-2-offboard-control-for-multi-vehicle-simulation/47049
47. https://discuss.px4.io/t/impossible-to-publish-for-multi-drone-simulation-with-ros2-gazebo/35682
48. https://discuss.px4.io/t/multi-drone-sim-qgroundcontrol-failure/46347
49. https://discuss.px4.io/t/multi-vehicle-simulation-in-v1-14/47540
50. https://discuss.px4.io/t/how-to-experiment-with-multi-vehicle-simulation/44235
51. https://discuss.px4.io/t/px4-multiple-vehicle-simulation-help/44734

### Priority 4: ROS2/MAVROS Integration
52. https://discuss.px4.io/t/ros-gz-bridge-not-working-unable-to-use-rviz2-to-fetch-px4-x500-mono-cam-image-topic/44447
53. https://discuss.px4.io/t/ros-gz-bridge-not-working-unable-to-use-rviz2-to-fetch-px4-gazebo-x500-mono-cam-image-topic/44810
54. https://discuss.px4.io/t/why-is-my-ros2-scan-topic-not-publishing-any-messages-slam-toolbox-lifecycle-fails-python-subscriber-inactive/47421
55. https://discuss.px4.io/t/not-able-to-get-the-camera-or-sensor-data-from-ros2-topics-to-avoid-obstacles/43428
56. https://discuss.px4.io/t/gz-x500-lidar-2d-cant-publish-scan/43476
57. https://discuss.px4.io/t/issue-when-launching-ros-with-px4-sitl-after-successful-gazebo-simulation/45529
58. https://discuss.px4.io/t/px4-sitl-sensor-datas-arent-published-by-topic/45852
59. https://discuss.px4.io/t/ros2-px4-1-fmu-in-vehicle-visual-odometry-topic-subscribe-issue/46126
60. https://discuss.px4.io/t/how-to-see-px4-gazebo-camera-topic-in-ros-2-foxy-can-see-in-gz-topic-but-not-ros2-topic/46979
61. https://discuss.px4.io/t/ros2-offboard-control-direct-actuator-control-not-working/45073
62. https://discuss.px4.io/t/about-the-offboard-control-of-vtol-by-ros-2/42010
63. https://discuss.px4.io/t/offset-issue-in-offboard-mode-with-mav-frame-body-ned-and-mavlink/44630
64. https://discuss.px4.io/t/offboard-mode-with-px4-hitl-mavros-and-qgc/42506
65. https://discuss.px4.io/t/offboard-mode-in-sitl-with-jmavsim/46447

### Priority 5: Custom Models and Airframes
66. https://discuss.px4.io/t/px4-sitl-gazebo-harmonic-modify-physical-properties/43417
67. https://discuss.px4.io/t/determining-motor-constants-for-gazebo-and-px4-from-an-actual-motor/46241
68. https://discuss.px4.io/t/potential-bug-in-px4-gz-bridge-esc-interface/46132
69. https://discuss.px4.io/t/gazebo-sdf-file-motor-parameters-definitions/34747
70. https://discuss.px4.io/t/creating-multiple-components/40607
71. https://discuss.px4.io/t/simulating-drone-with-rangefinder/40575
72. https://discuss.px4.io/t/adding-custom-model-in-gazebo-classic/43858
73. https://discuss.px4.io/t/create-custom-airframe-for-sitl/46547
74. https://discuss.px4.io/t/create-custom-model-for-sitl/6700/41
75. https://discuss.px4.io/t/adding-a-custom-gazebo-model-that-works-with-px4/47541
76. https://discuss.px4.io/t/tiltrotor-vtol-dive-on-transition/46487
77. https://discuss.px4.io/t/tri-tiltrotor-vtol-dive-on-transition/46582
78. https://discuss.px4.io/t/hitl-vtol-transition/46561
79. https://discuss.px4.io/t/reversible-motor-in-sitl-not-able-to-reverse/46838
80. https://discuss.px4.io/t/coaxial-octocopter-gazebo-simulation-problems/28805
81. https://discuss.px4.io/t/simulating-custom-airship-in-gazebo/32781
82. https://discuss.px4.io/t/using-gazebo-motor-failure-plugin-in-gazebo-simulation/18807
83. https://discuss.px4.io/t/drone-motor-failure-simulation/42031
84. https://discuss.px4.io/t/custom-controlallocation-logic-in-case-of-rotor-failure/42077
85. https://discuss.px4.io/t/px4-sitl-jsbsim-makes-rolling-airplane/42324
86. https://discuss.px4.io/t/state-of-jsbsim-sitl-for-fixed-wing-rascal-model/43654
87. https://discuss.px4.io/t/dual-tailsitter-gazebo-hover-simulation/5207/11
88. https://discuss.px4.io/t/omnicopter-simulation-in-gazebo/46457
89. https://discuss.px4.io/t/px4-autopilot-with-8-lift-motors-and-1-pusher-motor/46469
90. https://discuss.px4.io/t/fixed-wing-control-in-offboard-mode/46758
91. https://discuss.px4.io/t/simulating-px4-with-servo-motors/47231
92. https://discuss.px4.io/t/simulate-given-stability-derivatives-onto-a-generic-plane/47263

### Priority 6: Sensor Simulation
93. https://discuss.px4.io/t/px4-sitl-video-stream-unavailable/42909
94. https://discuss.px4.io/t/px4-sitl-video-stream-unavailable-on-udp-5600/43155
95. https://discuss.px4.io/t/drone-camera-hardware-encoding-error-in-gazebo/45077
96. https://discuss.px4.io/t/need-help-with-integrating-camera-to-px4-gazebo-simulation/45711
97. https://discuss.px4.io/t/how-to-use-iris-depth-camera/45952
98. https://discuss.px4.io/t/visualisation-of-point-cloud-data-of-depth-camera-via-rviz2/43035
99. https://discuss.px4.io/t/terrain-following-not-working-in-px4-gazebo-simulation-environment/43683
100. https://discuss.px4.io/t/terrain-following-is-not-working-in-px4-autopilot-software/47022
101. https://discuss.px4.io/t/how-to-fly-a-quadcopter-using-optical-flow-without-gps-in-the-gazebo-garden-simulation-environment/43527
102. https://discuss.px4.io/t/rtabmap-slam-in-gazebo-harmonic/47156
103. https://discuss.px4.io/t/gazebo-simulation-hector-slam-for-position-estimation-of-gps-denied-drone/36406
104. https://discuss.px4.io/t/cant-get-sensors-to-load-in-gazebo-stand-alone-mode/45225
105. https://discuss.px4.io/t/how-to-setup-multiple-distance-sensors-in-px4-gazebo-sitl/45919

### Priority 7: Alternative Simulator Integration
106. https://discuss.px4.io/t/integrate-px4-and-unity/42508
107. https://discuss.px4.io/t/cant-make-mavsdk-commuincate-with-px4-sitl-in-airsim-unreal-engine/45970
108. https://discuss.px4.io/t/px4-sitl-with-simulink-gazebo/42303
109. https://discuss.px4.io/t/px4-doesnt-takeoff-in-sitl-with-simulink-in-jmavsim/44244
110. https://discuss.px4.io/t/px4-sitl-with-matlab-simulink-model/25459
111. https://discuss.px4.io/t/issue-with-running-and-monitoring-the-px4-host-target-and-jmavsim-in-simulink/43561
112. https://discuss.px4.io/t/help-with-px4-sitl-simulink-connection/46425
113. https://discuss.px4.io/t/px4-control-with-simcenter-amesim-simulation-software/44512
114. https://discuss.px4.io/t/custom-simulator-in-sitl/47152

### Priority 8: Docker and Deployment
115. https://discuss.px4.io/t/issue-running-px4-sitl-in-a-container/46059
116. https://discuss.px4.io/t/unable-to-connect-dockerized-simulation/32048
117. https://discuss.px4.io/t/running-sim-on-a-vm-in-a-docker-container/45983
118. https://discuss.px4.io/t/gazebo-entities-not-rendered/44619/3
119. https://discuss.px4.io/t/gazebo-not-loading/39733/4
120. https://discuss.px4.io/t/cannot-start-gazebo-simulation-besides-gz-xxx/43070
121. https://discuss.px4.io/t/how-to-run-gazebo-from-px4-running-on-vm-multipass/45702

### Priority 9: World and Environment
122. https://discuss.px4.io/t/qgc-not-connected-to-custom-drone-urdf/43167
123. https://discuss.px4.io/t/qgc-does-not-connect-to-px4-sitl-in-custom-world/46990
124. https://discuss.px4.io/t/qgc-not-connecting-to-the-vehicle-in-custom-world-for-sitl/47171
125. https://discuss.px4.io/t/using-a-custom-world-environment-in-px4-v1-16/47409/4
126. https://discuss.px4.io/t/updating-px4-version-in-a-gazebo-simulation/43738
127. https://discuss.px4.io/t/px4-gazebo-harmonic-gz-x500-fails-to-arm-in-custom-warehouse-world/46242
128. https://discuss.px4.io/t/how-to-simulate-the-effect-of-altitude-on-quad-lift/42846
129. https://discuss.px4.io/t/unable-to-simulate-wind-via-make-px4-sitl-gz-x500-windy/45696

### Priority 10: Parameter and Configuration
130. https://discuss.px4.io/t/param-request-list-does-not-return-a-list-of-all-parameters/47359
131. https://discuss.px4.io/t/change-px4-sitl-gazebo-ports-for-gcs-and-api/47399
132. https://discuss.px4.io/t/how-to-access-px4-parameters-in-offboard-mode/40908/5
133. https://discuss.px4.io/t/how-to-change-pwm-value-and-saturation-in-sils-or-gazebo/41678
134. https://discuss.px4.io/t/disabling-failsafe-option-for-simulation/42119
135. https://discuss.px4.io/t/is-it-possible-to-create-drone-instances-in-a-clean-state-regardless-of-past-flight-missions/42015
136. https://discuss.px4.io/t/how-to-make-time-syncrhronization-before-start-simulator/42586
137. https://discuss.px4.io/t/tcp-port-open-vs-closed-for-simulation-env/41998
138. https://discuss.px4.io/t/disable-gps-to-use-vio/42754
139. https://discuss.px4.io/t/use-external-odometry-in-enu-for-px4/43097
140. https://discuss.px4.io/t/disabling-gazebo-odometry-publisher-px4-link/47082
141. https://discuss.px4.io/t/sensor-frame-orientation-custom-simulation/46035
142. https://discuss.px4.io/t/setting-px4-to-an-arbitrary-state-for-machine-learning-simulations/43846
143. https://discuss.px4.io/t/px4-external-vision-aiding-with-gazebo-dynamic-pose-issue-with-position-reset/44400
144. https://discuss.px4.io/t/send-position-from-ros2-topics-to-mavlink-messages/43777
145. https://discuss.px4.io/t/gps-to-non-gps-transition-using-ros2/46164
146. https://discuss.px4.io/t/gz-bridge-failed-to-start-and-spawn-model/46632
147. https://discuss.px4.io/t/px4-sitl-to-gazebo-rotor-velocity-bridge/46694
148. https://discuss.px4.io/t/drone-position-hold-non-gps-using-aruco-detection/46698
149. https://discuss.px4.io/t/gps-jamming-issue/46856
150. https://discuss.px4.io/t/px4-gazebo-static-maps-plugin/44060
151. https://discuss.px4.io/t/segmentation-fault-or-timeout-caused-by-the-combination-of-multiple-parameters/46000
152. https://discuss.px4.io/t/training-dl-model-on-imu-ground-truth-gps-denied-simulation-and-vision-pose-integration-in-px4-sitl/47434