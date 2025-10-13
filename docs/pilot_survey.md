# PX4 Simulator Community Survey - Pilot Analysis

## Summary

A pilot survey was conducted with 6 PX4 developers to validate the survey instrument before wider distribution. Respondents were primarily professional engineers (66.7%) with advanced to expert-level simulator expertise (83.3%), and most have 5+ years of PX4 experience (66.7%). The pilot revealed strong consensus on critical priorities while identifying gaps between developer perspectives and broader user needs documented in forum analysis.

## Respondent Profile

The pilot group represents highly experienced users: two-thirds are professional engineers, half have advanced simulator expertise, and two-thirds have 5+ years with PX4. This experienced cohort is ideal for validating technical questions but may not reflect novice user perspectives—an important consideration for final survey distribution.

## Simulator Usage and Goals

All respondents use Gazebo (Classic or Harmonic), confirming its dominance in the PX4 ecosystem. However, 50% also use AirSim, FlightGear, or JSBSim, indicating demand for alternative simulator support. Primary use cases center on algorithm development (66.7%), pre-flight testing (66.7%), and quality assurance in CI pipelines (83.3%). Notably, all respondents simulate only single vehicles, which contrasts sharply with forum analysis showing multi-vehicle simulation as a critical pain point for the broader community.

Vehicle types are dominated by quadcopters (83.3%) and fixed-wing aircraft (66.7%), with VTOL and specialized vehicles showing lower representation. Equipment focuses heavily on cameras (83.3%) and perception sensors (83.3%), aligning with autonomous systems development priorities.

## Technical Infrastructure

Hardware requirements prove significant: 83.3% purchased new systems or upgraded existing ones specifically for simulation. Ubuntu dominates (83.3%) with minimal Windows usage. Despite substantial hardware investment, 50% report no significant limitations, suggesting current system requirements are acceptable to experienced users. However, one respondent noted that users processing high-resolution images may need more capable specifications than their own setup.

## Current Simulator Experience

Respondents evaluated their most recent simulator (primarily Gazebo variants) across multiple dimensions:

**Installation:** Mixed difficulty reported, with error messages particularly problematic—dependency management and debugging information rated poorly.

**User Experience:** Generally neutral to positive, with most finding simulators usable but acknowledging complexity. Interface clutter and documentation clarity received mixed feedback.

**Technical Performance:** Significant concerns emerged around physics realism and crash frequency. Respondents split on whether simulators can run faster than real-time. Photo-realism was not prioritized by this technical audience.

**Feature Support:** Sensor variety received positive ratings, but custom drone creation and swarm support showed weaknesses—particularly concerning given forum analysis priorities.

**Documentation and Community:** Documentation accessibility rated positively, but quality and tutorial availability showed room for improvement. Community support forums rated helpful, though response time satisfaction varied.

## Priority Features

Clear consensus emerged on critical capabilities:

**Highest Priorities:**
- Software-in-the-loop support (5/6 rated "Very Important")
- ROS/ROS2 integration (5/6 rated "Very Important")
- Multi-agent/swarm simulation (3/6 rated "Very Important")
- Realistic physics simulation (3/6 rated "Very Important")

**Lower Priorities:**
- Photorealistic rendering (low importance)
- Beginner-friendly interfaces (surprisingly low)
- Drag-and-drop capabilities (low importance)

Respondents emphasized the critical need for physics realism for CI testing and highlighted desires for simulation hotstart/snapshot capabilities and better PX4 version management within simulators.

## Key Open-Ended Feedback

**Strengths identified:**

- "Interfaces nicely with ROS 2"
- "Reliable, does not do magic but I can use it pretty easily"
- "Open source, tight ROS2 integration"

**Major frustrations:**

- "Startup and shutdown time"
- "Difficulty creating realistic flight dynamics models"
- "Lack of resources and misleading docs can be annoying"
- Extensive critique of Gazebo naming confusion, poor documentation, sensor plugin gaps, multi-vehicle performance issues, and repository fragmentation

**Most important improvements needed:**

- macOS support
- Better compatibility across PX4/simulator/ROS2 versions
- Migration from Gazebo Classic to Gazebo Harmonic
- Improved sensor physics (barometers unaffected by wind)
- Multi-vehicle performance (20+ vehicles)
- Failure injection and CI test improvements

## Key Findings for Final Survey

Based on pilot results and comparison with forum analysis, the final survey should:

- **Expand audience beyond core developers** to capture novice/intermediate users experiencing multi-vehicle, installation, and documentation issues not reflected in pilot
- **Add explicit questions about multi-vehicle challenges** (startup time, configuration complexity, swarm performance) since pilot respondents don't use this but forum shows it's critical
- **Include platform-specific issue questions** for macOS, Docker, and Windows to validate forum-identified barriers
- **Add version compatibility and migration questions** (Gazebo Classic → Harmonic, PX4 version stability)
- **Validate physics realism requirements** across different use cases (CI/CD vs. development vs. demonstration)
- **Clarify simulator-specific terminology** (e.g., "Gazebo" naming confusion) and separate questions by simulator rather than "most recent"
- **Probe documentation quality vs. accessibility gap** since docs are findable but content accuracy problematic
- **Include questions on simulation state management** (hotstart, snapshots) and alternative simulator integration depth