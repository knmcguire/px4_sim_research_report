# Survey Design and Methodology

## Survey Structure

The PX4 Simulator Community Survey was designed to gather feedback from users across all aspects of their simulation experience. The survey is setup in six main sections: demographic background, current simulator usage patterns, technical infrastructure, simulator experience evaluation, feature priorities, and strategic recommendations. The survey uses a mixed-methods approach combining quantitative Likert-scale ratings with qualitative open-ended questions.

## Design Rationale

### Understanding the User Base

The survey begins by establishing user segments through profession, simulator expertise level, and PX4 experience duration. This segmentation enables analysis of how different user groups (students, researchers, commercial engineers) experience simulation differently and prioritize different improvements. Understanding whether issues affect primarily beginners or experienced users helps to prioritize development efforts.

### Mapping the Ecosystem

Questions about which simulators users employ, their purposes (research, testing, commercial development), vehicle types, and scale (single vs. multi-vehicle) map the PX4 simulation landscape. This information is essential for resource allocation decisions: should development focus deepen and improve integration with existing simulators, or broaden support for alternative simulators or platforms?

### Technical Constraints

Hardware and infrastructure questions assess barriers to adoption. Understanding whether users must purchase expensive systems, what operating systems they use, and where they encounter limitations (CPU, GPU, RAM) reveals accessibility issues and performance bottlenecks. This data informs decisions about which minimum system requirements the developers should take into account.

### Experience Assessment

The survey uses detailed Likert-scale assessments across five dimensions: installation experience, user interface, technical performance, feature support, and community resources. This structured approach aims to identify specific pain points. For example, whether installation is problematic but documentation adequate, or vice versa. These type of questions should make it easier for users to answer to formulate their thoughts and if they agree. And if in any case a statement has been missed, this can be catched by the open ended questions at the end.

### Feature Prioritization

Users rate importance of potential improvements across technical capabilities, platform compatibility (OS support, ROS integration), usability , and advanced features. This creates a prioritization matrix showing which capabilities matter most to the community, enabling evidence-based development roadmap decisions.

### Strategic Direction

The survey concludes with open-ended questions soliciting input on the most important improvements needed and offering opportunities for follow-up interviews. This acknowledges that while quantitative data identifies patterns, qualitative discussion often reveals underlying causes and context that ratings alone cannot capture.

## Pilot survey and further investigations

This survey will first be tested out to a handfull of core-developers within the PX4 communinity to see if this survey needs any further improvement. In the mean time, more investigations in the PX4 community will also be conducted (as in support forums) to see if there is anything that the initial survey has missed as well. 

The first version of the survey can be found in the Appendix ( @sec-pilot )