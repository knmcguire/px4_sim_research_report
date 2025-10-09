# PX4 Simulator Community Survey

This survey aims to understand the developer needs of PX4 users and their simulation experiences. We're hoping to improve the current situation and make things better for everyone.

This survey should take only 10-15 minutes to fill in.

**Draft V4**

---

## Getting to Know You

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

## Current Simulator Usage

*This section helps us understand which tools you're using and how you're using them in your current workflow.*

**5. Which simulators have you worked with in your setup? (Select all that apply)**
- Nvidia Isaac Sim
- Gazebo (formerly known as Ignition)
- Gazebo Classic
- AirSim
- MuJoCo
- Pybullet
- FlightGear
- JSBSim
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

---

## Technical Setup & Constraints

*Understanding your hardware setup and limitations helps us design tools that work for everyone's environment.*

**12. Did you have to purchase/upgrade your computer specifically for simulation?**
- Yes, bought entirely new system
- Yes, upgraded existing system
- No, used existing hardware
- Using cloud/remote computing
- Other: ___________

**13. What operating system do you primarily use for simulation?**
- Ubuntu
- Arch Linux
- Fedora Linux
- Windows
- MacOS
- Other: ___________

**14. What operating system version are you using for the above selection?**
___________

**15. Do you run simulations locally on your machine?**
- Yes, with a GPU
- Yes, without a GPU
- No, I don't run locally

**16. Do you run simulations on cloud/remote machines?**
- Yes, with a GPU
- Yes, without a GPU
- No, I don't use cloud/remote
- Other: ___________

**17. What's your biggest hardware limitation?**
- CPU performance
- GPU/graphics performance
- RAM capacity
- Storage space
- Network bandwidth
- No significant limitations
- Other: ___________

**18. Anything to add to any of the questions answered in this section regarding computer specifications?**
___________

---

## Current Simulator Experience

*Here we dive deep into your experience with simulators - what works well and what doesn't. This feedback is crucial for identifying the biggest areas for improvement.*

**Please fill in the survey based on your first instinct (don't linger too long per question)**

**19. Which simulator have you used most recently?**
___________

**20. Setup and Installation Experience**

*Note: This refers to setting up the complete PX4 simulation environment (PX4 + simulator)*

Rate on scale: 1 (Strongly disagree) to 5 (Strongly agree)

- "The simulator was easy to install and set up with PX4"
- "I had to install too many external dependencies"
- "The error and debug messages were easy to understand"

**21. User Experience**

Rate on scale: 1 (Strongly disagree) to 5 (Strongly agree)

- "I needed to use an extensive guide to navigate through the GUI"
- "Using the simulator was a smooth experience"
- "The user interface felt cluttered and complex"
- "The error/bug messages were easy to read"

**22. Technical Performance**

Rate on scale: 1 (Strongly disagree) to 5 (Strongly agree)

- "Objects in the simulation didn't behave realistically"
- "The simulator can run simulations faster than real-time"
- "The simulation's graphics were very photo-realistic"
- "I experienced frequent crashes and freezes"

**23. Feature Support**

Rate on scale: 1 (Strongly disagree) to 5 (Strongly agree)

- "The simulator offered a wide variety of sensors"
- "I cannot easily make a custom drone in this simulator"
- "I'm able to use this simulator easily with swarms"

**24. Documentation and Tutorials**

Rate on scale: 1 (Strongly disagree) to 5 (Strongly agree)

- "The documentation/website was easy to find"
- "The documentation was difficult to follow"
- "There were plenty of tutorials available"

**25. Community and Support**

Rate on scale: 1 (Strongly disagree) to 5 (Strongly agree)

- "It was hard to find a clear way to get help or ask questions"
- "The community and support forums were helpful"
- "It took too long to get my questions answered"

**26. What do you like the most about current/latest simulator you are using?**
___________

**27. What's your biggest frustration with current/latest simulator you are using?**
___________

**28. Anything else to add?**
___________

---

## Desired Features & Priorities

*This section helps us prioritize development efforts by understanding which features matter most to different types of users.*

**Please fill in the survey based on your first instinct (don't linger too long per question)**

**29. Please rate the preferred Technical Capabilities**

Rate on scale: 1 (Not important) to 5 (Very important), or No preference/opinion

- Hardware-in-the-loop support
- Software-in-the-loop support
- Faster than real-time simulation
- Photorealistic rendering
- Realistic physics simulation
- Weather/environmental simulation
- Failure mode simulation
- Communication simulation

**30. Please rate the preferred Platform & Compatibility**

Rate on scale: 1 (Not important) to 5 (Very important), or No opinion or preference

- Multiple OS support
- ROS/ROS 2 integration
- Cloud simulation capabilities
- Docker/containerization support
- Network capability (PX4 and simulator on different machines)

**31. Please rate the preferred Usability & Accessibility**

Rate on scale: 1 (Not important) to 5 (Very important), or No opinion or preference

- Beginner-friendly interface
- Easy installation process
- Drag-and-drop model capability
- Template/example library availability
- Real-time parameter tuning
- Real-time debug support (pause, step through simulation)
- Simulation snapshot/hotstart capability

**32. Please rate the preferred Advanced Features**

Rate on scale: 1 (Not important) to 5 (Very important), or No opinion or preference

- Multi-agent/swarm simulation
- Machine learning integration
- Custom sensor model creation
- Easy robot model creation
- Scenario scripting/automation
- Performance benchmarking tools
- CAD program integration for custom models

**33. Any more features that we should pay attention to as well?**
___________

---

## PX4 Simulation Roadmap

*This section helps us understand what strategic direction would best serve the PX4 community.*

**34. For the PX4 simulation roadmap, what should be the TOP priority?**
- Improve stability/performance of existing simulator integrations
- Add support for more simulators
- Better documentation and examples
- A new PX4-optimized simulator
- Better sim-to-real transfer tools
- More realistic sensor/physics models
- Other: ___________

**35. Why is this your top priority?**
___________

---

## Final Questions

*Final thoughts and opportunities for deeper engagement with our improvement efforts.*

**36. What's the most important improvement needed in simulation supported in the PX4-ecosystem?**
___________

**37. Any additional comments or suggestions?**
___________

**38. Would you be willing to participate in follow-up interviews?**
- Yes
- No

**39. If yes, please provide on which email address we can contact you. Your email address will only be used for this exact purpose.**
___________

---

## Thank you!

Thank you for taking the time to share your experiences! Your feedback will help improve simulation tools for the entire PX4 community.

**Please press next to submit the form**