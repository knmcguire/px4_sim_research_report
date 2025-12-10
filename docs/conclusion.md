# Brief Discussion and Recommendation

The section will reflect  the survey’s results and give out a general recommendation of the next steps. Mind that this survey is written in mind to figure out the main priorities of the users of simulation and to find next steps. Of the 120 participants and an estimated community size of 15000 developers, the margin of error is about 8-9 %. That means that the results need to be taken with slight caution as that is higher than the recommend 5%, however the results give a significant preference that it is recommended to use it as a guide line.

## Reflections on the Survey Results

Overall, participants agreed that software-in-the-loop support is essential and must remain a priority. While there were few direct comments about SITL functionality itself, several respondents noted that it was unclear what happens in the background or how to adjust features and sensors. This suggests the SITL documentation could benefit from review.

One surprising result was the difference in perceived importance between realistic physics models and photorealistic rendering. These two features were nearly opposite on the importance scale. This is unexpected given that AirSim and Isaac Sim, both celebrated for their rendering capabilities, were mentioned as popular alternatives to Gazebo. However, users of these simulators represented only a small portion of respondents. An interesting suggestion from the survey was to explore JSBSim integration for flight dynamics in Gazebo New. That said, it is difficult to evaluate "how realistic" physics models need to be without widely accepted benchmarks for simulator evaluation.

Documentation emerged as a significant pain point. Many participants reported difficulty finding proper documentation, though they did not always specify where. Several mentions pointed to Gazebo's physics plugins, such as the multicopter plugin, environment plugins like wind, and physics integration, as being poorly documented. These are areas where the PX4 community could contribute directly to Gazebo.

A clear difference emerged between the needs of more experienced developers (P1 and P3) and those with limited experience (P2, P4). The latter group showed stronger preference for better examples and tutorials, which is also reflected in the feature importance scores. Senior engineers and researchers expressed more interest in improving simulator realism, primarily related to physics. Senior engineers (P1) additionally emphasized improving the overall PX4-Gazebo integration.

Regarding which simulator to prioritize: Gazebo New is both the most used and the most requested for improvement. A substantial portion of users (the second-largest group) still relies on Gazebo Classic despite growing compatibility issues. Since Gazebo Classic is end-of-life, there will be limited support from the maintenance team to address these. For issues with Gazebo New, this survey lacked the granularity to create specific tickets, so additional effort is needed within the community to properly document problems and create minimal reproducible examples.

## Recommendation

The following recommendations are offered by this report's author; final decisions should be made in consultation with the PX4 simulation maintenance team based on their availability and capabilities.

Based on the survey results, the recommendation is not to focus efforts on building a new simulator or integrating with community simulators like AirSim forks or Isaac Sim. Instead, development efforts should focus solely on improving the current PX4 and Gazebo New integration. Gazebo Classic should no longer be recommended, as it is end-of-life and out of scope.

The most immediate opportunity is improving documentation. The quick-start guide appears sufficient for most users, as basic setup runs mostly out-of-the-box. However, users struggle to understand the underlying workflows. When junior developers and students need to customize their frame or model, they encounter difficulties due to a lack of examples. These could be developed through structured efforts similar to ROS's and Gazebo's tutorial parties.

For advanced developers, there is a need for better troubleshooting guides and more comprehensive API documentation-contributions that would also benefit Gazebo's plugin documentation. Additionally, a version compatibility matrix documenting tested combinations of ROS, PX4, and Gazebo versions would address a frequently cited frustration. Given the complexity of these version combinations, it must remain possible for developers to contribute fixes and documentation to either the PX4 or Gazebo teams.

The next priority should be custom model and sensor creation, which was consistently mentioned as a pain point. This is challenging both from the Gazebo side and the PX4 integration side. Junior engineers would benefit most from improvements here.

Finally, there is clear interest in better physics simulation. However, as in aerial robotics more broadly, it is difficult to define what "better physics" means without knowing the application. Swarm simulations may require minimal physics fidelity, while a quadcopter carrying a payload demands much more. An investigation into benchmarking techniques (perhaps drawn from the game development industry) could help establish evaluation criteria for physics simulation quality.
