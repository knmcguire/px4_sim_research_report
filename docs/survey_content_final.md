# B. PX4 Simulator Community Survey - Final {#sec-final}

This survey aims to understand the developer needs of PX4 users and their simulation experiences. We're hoping to improve the current situation and make things better for everyone.

**This survey should take only 10-15 minutes to fill in.**

## About This Survey

We're gathering feedback from the PX4 community to inform our simulation integration roadmap. Your input will help us prioritize which simulators to support, what features to develop, and where to focus our documentation efforts.

**Who should take this survey:**
- Anyone who has used or is interested in using simulation with PX4
- Users of any experience level, from beginners to experts
- Whether you're in academia, industry, or working as a hobbyist

**Your responses are anonymous.** We'll only collect email addresses if you volunteer for follow-up interviews.

---

<p style="font-size: 1.2em;"><strong>Getting to Know You</strong></p>

*We'd like to understand your background and experience level to better contextualize your feedback.*

**1. What is your primary profession?**

- Student (BSc/MSc)
- Researcher (Academic/Industry)
- Educator/Teacher
- Professional Engineer / Technical Consultant
- Hobbyist / Independent Developer
- Other: ___________

**2. What domain are you working in?**

- Academia/Education
- Aerospace/Drones (Commercial)
- Aerospace/Drones (Hobbyist)
- Defense/Government
- Research Institution
- Other: ___________

**3. What is your level of expertise regarding robotic simulators?**

- Novice
- Intermediate
- Advanced
- Expert

**4. How long have you been working with PX4?**

- I haven't worked with PX4
- I just started working with PX4 (< 1 month)
- 1 month - 1 year
- 1-3 years
- 3-5 years
- 5+ years

---

<p style="font-size: 1.2em;"><strong>Current Simulator Usage</strong></p>

*This section helps us understand which tools you're using and how you're using them in your current workflow.*

**5. Which simulators have you worked with in your setup? (Select all that apply)**

- Nvidia Isaac Sim
- Gazebo (formerly known as Ignition)
- Gazebo Classic
- JMAVSim
- AirSim
- MuJoCo
- Pybullet
- FlightGear
- JSBSim
- Simulink
- Other: ___________

**6. What was your primary purpose for using simulators? (Select all that apply)**

- Academic research
- Education/learning
- Robot prototyping/design
- Algorithm development
- Testing before real flights
- Demonstration/presentation
- Competition preparation
- Commercial product development
- Flight tooling design
- Other: ___________

**7. For which goals are you using simulators? (Select all that apply)**

- Development tool for robotic systems
- Quality assurance in continuous integration
- Data generation for machine learning
- Mission planning and validation
- Training pilots/operators
- Safety
- Regulatory compliance testing
- Other: ___________

**8. What type of aerial robotic vehicle are you working with? (Select all that apply)**

- Helicopter
- Quadcopter
- Multicopters (more than 4 propellers)
- Fixed wing
- Hybrid / VTOL vehicles
- Blimps
- Other: ___________

**9. Does your platform have additional equipment or payloads? (Select all that apply)**

- Manipulator arm
- Gripper/claw
- Gimbal
- Camera
- Cargo hook/winch
- Perception Sensors (lidar, sonar, etc.)
- Communication equipment
- None of the above
- Other: ___________

**10. How many robots/UAVs do you typically simulate simultaneously?**

- Just one (1)
- 2-4
- 5-10
- 10-100
- 100+

**11. How do you typically interact with your simulator? (Select all that apply)**

- Mainly through GUI
- Headless/CI environments
- Custom plugins/extensions
- ROS/ROS2 integration
- API/scripting
- Other: ___________

**12. What's do you like the most with current/latest simulator you are using?**

____ 

**13. What's your biggest frustration with current/latest simulator you are using?**

____ 
---

<p style="font-size: 1.2em;"><strong>Technical Setup & Constraints</strong></p>

*Understanding your hardware setup and limitations helps us design tools that work for everyone's environment.*

**14. Did you have to purchase/upgrade your computer specifically for simulation?**

- Yes, bought entirely new system
- Yes, upgraded existing system
- No, used existing hardware
- Using cloud/remote computing
- Other: ___________

**15. What operating system do you primarily use for simulation?**

- Ubuntu
- Arch Linux
- Fedora Linux
- Windows
- MacOS
- Other: ___________

**16. What operating system version are you using for the above selection?**

___________

**17. Do you run simulations locally or remotely?**

- Locally on my machine
- On remote machines
- In the cloud
- Other: ___________

**18. Is your machine on which you run your simulation GPU-enabled?**

- Yes
- No
- Not sure

**19. What's your biggest hardware limitation?**

- CPU performance
- GPU/graphics performance
- RAM capacity
- Storage space
- Network bandwidth
- No significant limitations
- Other: ___________

**20. Anything to add to any of the questions answered in this section regarding computer specifications?**

___________

---

<p style="font-size: 1.2em;"><strong>Desired Features & Priorities</strong></p>

*This section helps us prioritize development efforts by understanding which features matter most to different types of users.*

**Please fill in the survey based on your first instinct (don't linger too long per question)**

**21. Please rate the preferred Technical Capabilities**

Rate on scale: 1 (Not important) to 5 (Very important), or No preference/opinion

- Hardware-in-the-loop support
- Software-in-the-loop support
- Faster than real-time simulation
- Photorealistic rendering
- Realistic physics simulation
- Weather/environmental simulation
- Failure mode simulation
- Communication simulation

**22. Please rate the preferred Platform & Compatibility**

Rate on scale: 1 (Not important) to 5 (Very important), or No opinion or preference

- Multiple OS support
- ROS/ROS 2 integration
- Cloud simulation capabilities
- Docker/containerization support
- Network capability (PX4 and simulator on different machines)
- Compatibility between different versions of  PX4 and simulators

**23. Please rate the preferred Usability & Accessibility**

Rate on scale: 1 (Not important) to 5 (Very important), or No opinion or preference

- Beginner-friendly interface
- Easy installation process
- Template/example library availability
- Real-time parameter tuning
- Real-time debug support (pause, step through simulation)
- Simulation snapshot/hotstart capability

**24. Please rate the preferred Advanced Features**

Rate on scale: 1 (Not important) to 5 (Very important), or No opinion or preference

- Multi-agent/swarm simulation
- Machine learning integration
- Custom sensor model creation
- Easy robot model creation
- Scenario scripting/automation
- Performance benchmarking tools
- CAD program integration for custom models

**25. Any more features that we should pay attention to as well?**

___________

---

<p style="font-size: 1.2em;"><strong>PX4 Simulation Roadmap</strong></p>

*This section helps us understand what strategic direction would best serve the PX4 community.*

**26. If there was one thing you'd like the PX4 simulation development team to work on, what would it be?**
- Improving the current Gazebo simulator intergration
- A new PX4-optimized simulator
- Add support for more simulators for PX4
- Better documentation and examples for existing PX4 simulation
- More simulation model creation capabilities (more types of vehicles)
- More realistic sensor/physics models
- Improve stability/performance of existing simulator integrations
- Better PX4-simulator integration (easier SITL setup, better parameter mapping)
- More realistic sensor/physics models (Sim2Real gap)
- Better multi-vehicle/swarm simulation support
- Improved ROS/ROS2 integration with PX4 simulation
- Fixing PX4 - Simulator version compatibility issues
- Other

**27. Why is this choice your top priority?**

___________

---

<p style="font-size: 1.2em;"><strong>Final Questions</strong></p>

*Final thoughts and opportunities for deeper engagement with our improvement efforts.*

**28. Any additional comments or suggestions?**

___________

**29. Would you be willing to participate in follow-up interviews? If yes, please provide an email address where we can contact you. Your email address will only be used for this exact purpose.**

___________

---

<p style="font-size: 1.2em;"><strong>Thank you!</strong></p>

Thank you for taking the time to share your experiences! Your feedback will help improve simulation tools for the entire PX4 community.

**Please press next to submit the form**