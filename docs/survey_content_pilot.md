# A. PX4 Simulator Community Survey - Pilot {#sec-pilot}

This survey aims to understand the developer needs of PX4 users and their simulation experiences. We're hoping to improve the current situation and make things better for everyone.

This survey should take only 10-15 minutes to fill in.

---

<p style="font-size: 1.2em;"><strong>Getting to Know You</strong></p>

*We'd like to understand your background and experience level to better contextualize your feedback.*

**1. What is your primary profession?**

- Student (BSc/MSc)
- Researcher (Academic/Industry)
- Educator/Teacher
- Professional Engineer / Technical Consultant
- Other: ___________

**2. What is your level of expertise regarding robotic simulators?**

- Novice
- Intermediate
- Advanced
- Expert

**3. How long have you been working with PX4?**

- I haven't worked with PX4
- I just started working with PX4 (< 1 month)
- 1 month - 1 year
- 1-3 years
- 3-5 years
- 5+ years

---

<p style="font-size: 1.2em;"><strong>Current Simulator Usage</strong></p>

*This section helps us understand which tools you're using and how you're using them in your current workflow.*

**4. Which simulators have you worked with in your setup? (Select all that apply)**

- Nvidia Isaac Sim
- Gazebo (formerly known as Ignition)
- Gazebo Classic
- AirSim
- MuJoCo
- Pybullet
- FlightGear
- JSBSim
- Other: ___________

**5. What was your primary purpose for using simulators? (Select all that apply)**

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

**6. For which goals are you using simulators? (Select all that apply)**

- Development tool for robotic systems
- Quality assurance in continuous integration
- Data generation for machine learning
- Mission planning and validation
- Training pilots/operators
- Safety
- Regulatory compliance testing
- Other: ___________

**7. What type of aerial robotic vehicle are you working with?**

- Helicopter
- Quadcopter
- Multicopters (more than 4 propellers)
- Fixed wing
- Hybrid / VTOL vehicles
- Blimps
- Other: ___________

**8. Does your platform have additional equipment or payloads? (Select all that apply)**

- Manipulator arm
- Gripper/claw
- Gimbal
- Camera
- Cargo hook/winch
- Perception Sensors (lidar, sonar, etc.)
- Communication equipment
- None of the above
- Other: ___________

**9. How many robots/UAVs do you typically simulate simultaneously?**

- Just one (1)
- 2-4
- 5-10
- 10-100
- 100+

---

<p style="font-size: 1.2em;"><strong>Technical Setup & Constraints</strong></p>

*Understanding your hardware setup and limitations helps us design tools that work for everyone's environment.*

**10. Did you have to purchase/upgrade your computer specifically for simulation?**

- Yes, bought entirely new system
- Yes, upgraded existing system
- No, used existing hardware
- Using cloud/remote computing
- Other: ___________

**11. What operating system do you primarily use for simulation?**

- Ubuntu
- Arch Linux
- Fedora Linux
- Windows
- MacOS
- Other: ___________

**12. Which version of the operating system have you selected above?**
___________

**13. Do you use a GPU enabled computer, and if so, what kind of specifications does it have?**
___________

**14. What's your biggest hardware limitation?**

- CPU performance
- GPU/graphics performance
- RAM capacity
- Storage space
- Network bandwidth
- No significant limitations
- Other: ___________

**15. Do you find the necessary hardware/computer specifications for simulation acceptable or workable?**

- Yes
- No

**16. Anything to add to any of the questions answered in this section regarding computer specifications?**
___________

---

<p style="font-size: 1.2em;"><strong>Current Simulator Experience</strong></p>

*Here we dive deep into your experience with simulators - what works well and what doesn't. This feedback is crucial for identifying the biggest areas for improvement.*

**Please fill in the survey based on your first instinct (don't linger too long per question)**

**17. Which simulator have you used most recently?**
___________

**18. Setup and Installation Experience**

Rate on scale: 1 (I agree) to 5 (I do not agree)

- "The simulator was easy to install."
- "I had to install too many external dependencies"
- "The error and debug messages were easy to understand"

**19. User Experience**

Rate on scale: 1 (I agree) to 5 (I do not agree)

- "I needed to use an extensive guide to navigate through the GUI"
- "Using the simulator was a smooth experience."
- "The user interface felt cluttered and complex."
- "The error/bug messages were easy to read"

**20. Technical Performance**

Rate on scale: 1 (I agree) to 5 (I do not agree)

- "Objects in the simulation didn't behave realistically."
- "The simulator can run simulations faster than real-time."
- "The simulation's graphics were very photo-realistic."
- "I experienced frequent crashes and freezes."

**21. Feature Support**

Rate on scale: 1 (I agree) to 5 (I do not agree)

- "The simulator offered a wide variety of sensors."
- "I can not easily make a custom drone in this simulator"
- "I'm able to use this simulator easily with swarms"

**22. Documentation and Tutorials**

Rate on scale: 1 (I agree) to 5 (I do not agree)

- "The documentation/website was easy to find."
- "The documentation was difficult to follow."
- "There were plenty of tutorials available."

**23. Community and Support**

Rate on scale: 1 (I agree) to 5 (I do not agree)

- "It was hard to find a clear way to get help or ask questions."
- "The community and support forums were helpful."
- "It took too long to get my questions answered."

**24. What do you like the most about current/latest simulator you are using?**
___________

**25. What's your biggest frustration with current/latest simulator you are using?**
___________

**26. Anything else to add?**
___________

---

<p style="font-size: 1.2em;"><strong>Desired Features & Priorities</strong></p>

*This section helps us prioritize development efforts by understanding which features matter most to different types of users.*

**Please fill in the survey based on your first instinct (don't linger too long per question)**

**27. Please rate the preferred Technical Capabilities**

Rate on scale: 1 (Not important) to 5 (Very important), or No preference/opinion

- Hardware-in-the-loop support
- Software-in-the-loop support
- Faster than real-time simulation
- Photorealistic rendering
- Realistic physics simulation
- Weather/environmental simulation
- Failure mode simulation
- Communication simulation

**28. Please rate the preferred Platform & Compatibility**

Rate on scale: 1 (Not important) to 5 (Very important), or No opinion or preference

- Multiple OS support
- ROS/ROS 2 integration
- Cloud simulation capabilities
- Docker/containerization support

**29. Please rate the preferred Usability & Accessibility**

Rate on scale: 1 (Not important) to 5 (Very important), or No opinion or preference

- Beginner-friendly interface
- Easy installation process
- Drag-and-drop model capability
- Template/example library availability
- Real-time parameter tuning

**30. Please rate the preferred Advanced Features**

Rate on scale: 1 (Not important) to 5 (Very important), or No opinion or preference

- Multi-agent/swarm simulation
- Machine learning integration
- Custom sensor model creation
- Easy robot model creation
- Scenario scripting/automation
- Performance benchmarking tools
- CAD program integration for custom models

**31. Any more features that we should pay attention too as well?**
___________

---

<p style="font-size: 1.2em;"><strong>Final Questions</strong></p>

*Final thoughts and opportunities for deeper engagement with our improvement efforts.*

**32. What's the most important improvement needed in simulation supported in the PX4-ecosystem?**
___________

**33. Any additional comments or suggestions?**
___________

**34. Would you be willing to participate in follow-up interviews?**
- Yes
- No

**35. If yes, please provide on which email address we can contact you. Your email address will only be used for this exact purpose.**
___________

---

<p style="font-size: 1.2em;"><strong>Thank you!</strong></p>

Thank you for taking the time to share your experiences! Your feedback will help improve simulation tools for the entire PX4 community.

**Please press next to submit the form**