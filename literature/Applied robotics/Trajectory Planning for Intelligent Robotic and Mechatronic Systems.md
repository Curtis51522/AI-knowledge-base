Editorial
Trajectory Planning for Intelligent Robotic and
Mechatronic Systems

Lorenzo Scalera 1,*

, Andrea Giusti 2

and Renato Vidoni 3

1

Polytechnic Department of Engineering and Architecture, University of Udine, 33100 Udine, Italy

2 Robotics and Intelligent Systems Engineering, Fraunhofer Italia Research, 39100 Bolzano, Italy;

andrea.giusti@fraunhofer.it
Faculty of Engineering, Free University of Bozen-Bolzano, 39100 Bolzano, Italy; renato.vidoni@unibz.it

3

* Correspondence: lorenzo.scalera@uniud.it

1. Trajectory Planning for Intelligent Robotic and Mechatronic Systems

Trajectory planning is a crucial and challenging problem for research on intelligent
robotic and mechatronic systems, which play a pivotal role in modern manufacturing
processes, and especially within the framework of Industry 4.0 [1]. Indeed, in every robotic
application, it is required to define not only a path, but also a motion law that can guarantee
a feasible and safe operation of the system according to the requirements of the task and the
limits of the robot [2]. Many approaches to the problem of trajectory planning have been
developed and investigated in the literature, with applications that span from industrial,
collaborative and, more in general, autonomous and intelligent robotic and mechatronic
systems [3,4].

The motion law of a robotic system can be planned by considering different goals.
The design of a proper motion law can be evaluated, for instance, in relation to the en-
ergy consumption of a robotic or mechatronic system, and, therefore, optimal trajectories
can be determined based on the best performance of the robot in terms of time-energy
consumption [5–7]. Another interesting field of application is that of vibration reduc-
tion. Indeed, many automatic machines and mechatronic applications require smooth
and jerk-limited trajectories during the prescribed operation [8–10]. Moreover, emerging
scenarios of industrial robotics, such as collaborative robotics and human–robot interaction,
demand advanced strategies for the planning of robot trajectories to ensure smoothness,
safety, and fluency during the execution of a task for a robot working alongside a human
operator [11–13]. Finally, the trajectory planning for robotic and mechatronic systems is
also tightly coupled with the motion control problem of such systems to guarantee high
performance in the execution of the demanded motion law [14,15].

In this Special Issue, we invited researchers to contribute with original works and re-
view articles related to trajectory planning for intelligent mechatronic systems, autonomous
machines, industrial and collaborative manipulators, as well as mobile and reconfigurable
robots. Original research papers on these themes have been sought, with a focus on both
theoretical investigations and real-world applications on these topics.

Suitable topics included, but were not restricted to, the following: path and trajectory
planning, dynamic modelling, energy efficiency, vibration suppression, smooth trajectories,
motion profile optimization, motion control, intelligent robotic and mechatronic systems,
collaborative robotics, and motion planning for human–robot interaction.

2. Special Issue

This Special Issue collects papers in open-access format on a broad number of aspects
of trajectory planning for intelligent robotic and mechatronic systems introduced above.
The call for the Special Issue “Trajectory Planning for Intelligent Robotic and Mechatronic
Systems” received 15 manuscripts, 12 of which were accepted for publication. In most of the

Citation: Scalera, L.; Giusti, A.;

Vidoni, R. Trajectory Planning for

Intelligent Robotic and Mechatronic

Systems. Appl. Sci. 2024, 14, 1179.

https://doi.org/10.3390/app14031179

Received: 18 December 2023

Revised: 9 January 2024

Accepted: 28 January 2024

Published: 31 January 2024

Copyright: © 2024 by the authors.

Licensee MDPI, Basel, Switzerland.

This article is an open access article

distributed under

the terms and

conditions of the Creative Commons

Attribution (CC BY) license (https://

creativecommons.org/licenses/by/

4.0/).

Appl. Sci. 2024, 14, 1179. https://doi.org/10.3390/app14031179

https://www.mdpi.com/journal/applsci

applied  sciencesAppl. Sci. 2024, 14, 1179

2 of 5

articles, numerical simulations are corroborated by experimental results. The contributions
are listed below in order of publication.

Contribution 1 presents a research study on the trajectory and operational performance
of a wheel loader automatic shoveling. A test platform for the operational performance
of loaders is developed, and nine parallel shoveling trajectories of different depths are
designed and compared in terms of total time, fuel and energy consumption, as well as
operation resistance.

In Contribution 2, the authors describe the implementation and experimental val-
idation of an obstacle avoidance algorithm using the UR5e robot. An error analysis of
simulation and experiments allows one to conclude that the developed approach was
effectively applied to a real collaborative robotic system, exhibiting behavior similar to
what simulations predicted.

Another work dealing with a collaborative robotic application can be found in Contri-
bution 3, where a bin-picking task is enhanced to achieve a successful and fluent collab-
oration between human and robot. Experimental results show that the use of a robot in
collaboration with a human operator can be particularly useful to overcome typical bin
picking failures and to improve the fault tolerance of the system, increasing its flexibility
and reducing down times.

The authors of the paper in Contribution 4 illustrate the application of a motion profile
with elliptic jerk to the Cartesian space position control of serial robots. A SCARA-like
manipulator with four degrees of freedom (DOFs) and elastic balancing is considered,
and both integer-order and fractional-order controllers are applied to simulate the behavior
of the robot using the elliptic jerk profile.

The influence of joint stiffness and motion time on the trajectories of underactuated
robots is analyzed in Contribution 5. More in detail, trajectories for a 3-DOF robot moving
in the horizontal plane with two actuators and a torsional spring are planned, and com-
binations of torsional stiffness and motion time that minimize the motion torques or the
swept area are discussed.

The paper in Contribution 6 provides a comprehensive review on use of reinforcement
learning for dynamic obstacle avoidance and path planning algorithms. Publications from
the last 5 years (2018–2022) are collected and analyzed to evaluate the latest trends in mobile
robotics using reinforcement learning, including a discussion on performance metrics and
research gaps in this field.

In Contribution 7, an approach for frame-based slip detection for an underactuated
robotic gripper for assistance of users with disabilities is presented. The proposed method
effectively handles common issues associated with purely vision-based slip detection
methods, such as optical path occlusion or compliant objects, showing high performance in
terms of accuracy and robustness against changes of the environment.

Contribution 8 proposes a technique for positioning applications that involves em-
ploying a platform subjected to planar oscillations along circular, elliptical, and complex
trajectories. Dynamic and mathematical models of the motion of a small object on the
platform were developed to investigate the motion characteristics of the part by controlling
frequency and amplitude of the excitation force.

In Contribution 9, different learning methods based on artificial neural networks
are examined to replace the default speed controller for high-precision position control
and drift attenuation in robotic manipulators. Experimental tests on a UR5 robot yield to
comparable results with respect to the classical controller, showing the feasibility of the
proposed approach without the need for tuning the controller parameters.

Furthermore, in Contribution 10 a virtual force control for a six-axis robotic arm is
developed using both traditional mathematical modeling and machine learning techniques
in the implementation of the dynamic model of the manipulator. The proposed position
and force hybrid controller is based on a Raspberry Pi board with a real-time kernel,
demonstrating the fulfillment of the motion control requirements with a low-cost device.
The virtual force sensor is also used to detect collisions with the human operator.

Appl. Sci. 2024, 14, 1179

3 of 5

The work in Contribution 11 aims at developing a trajectory planning approach to
avoid collisions for a SCARA robotic manipulator in the context of collaborative robotics.
The authors show that the proposed approach based on topological path planning is a
collision-free, deterministic, and predictable route planning method with superior perfor-
mance with respect to alternative approaches, e.g., based on probabilistic roadmap methods
or on generalized Voronoi diagrams.

Finally, in Contribution 12 the authors propose a novel method for designing motion
profiles utilizing a sinusoidal jerk model to generate fast and smooth trajectories charac-
terized by low vibrations. Differently from previous studies, an analytical optimization
procedure for the profile parameters is introduced to minimize both the motion duration
and the excitation frequency contents. Numerical and experimental results on a linear axis
show the effectiveness of the proposed method in comparison with alternative strategies in
terms of smoothness and vibration attenuation.

The presented contributions collectively explore diverse dimensions of trajectory plan-
ning for intelligent robotic and mechatronic systems. To summarize, Contributions 1, 4 and
5 delve into trajectory planning and control strategies for robotic manipulators, empha-
sizing factors like operational performance, motion profiles, and joint stiffness influences.
Contributions 2 and 11 address the challenges of obstacle avoidance and collision-free
trajectory planning in collaborative robotic applications. In the same context, the virtual
force sensor presented in Contribution 10 is used to detect collision with the body of the
human operator working alongside the robot. Contributions 3 and 7 focus on enhancing
collaboration between humans and robots in specific tasks, such as bin-picking and slip
detection for a robotic gripper. Contributions 6 and 9 explore the integration of artificial in-
telligence, with a focus on reinforcement learning and artificial neural networks, to improve
dynamic obstacle avoidance, path planning, and position control in robotic systems. Finally,
Contributions 8 and 12 explore the effects of motion design on mechanical vibrations.

3. Final Remarks

As technology advances, the vision for trajectory planning in intelligent robotic and
mechatronic systems is evolving towards more sophisticated and adaptive solutions. The in-
tegration of artificial intelligence and machine learning techniques opens new avenues for
optimizing trajectory planning algorithms. Future developments may emphasize real-time
adaptability to dynamic environments, enhanced collision avoidance strategies, and im-
proved coordination in multi-robot systems. The trajectory planning field aims to create
frameworks that not only ensure precision and efficiency, but also consider the inher-
ent complexities of real-world scenarios. With the continued integration of cutting-edge
technologies, the trajectory planning field will play a pivotal role in the advancement of
autonomous robotics and mechatronic applications.

This Special Issue contains valuable research works focused on the trajectory planning
for intelligent mechatronic and robotic systems, covering a wide area of applications. This
collection demonstrates the high level of research interest in these topics, as well as the
potential for future developments. We sincerely hope that this Special Issue on “Trajectory
Planning for Intelligent Robotic and Mechatronic Systems” will be a useful resource for
academics and researchers working on these topics.

Author Contributions: Conceptualization, L.S., A.G. and R.V.; writing–original draft preparation,
L.S.; writing–review and editing, L.S., A.G. and R.V.; supervision, project administration, R.V. All
authors have read and agreed to the published version of the manuscript.

Funding: This research received no external funding.

Conflicts of Interest: The authors declare no conflict of interest.

Appl. Sci. 2024, 14, 1179

4 of 5

List of Contributions

1.

3.

Chen, Y.; Jiang, H.; Shi, G.; Zheng, T. Research on the Trajectory and Operational
Performance of Wheel Loader Automatic Shoveling. Appl. Sci. 2022, 12, 12919.
2. Neri, F.; Forlini, M.; Scoccia, C.; Palmieri, G.; Callegari, M. Experimental evaluation of
collision avoidance techniques for collaborative robots. Appl. Sci. 2023, 13, 2944.
Boschetti, G.; Sinico, T.; Trevisani, A. Improving Robotic Bin-Picking Performances
through Human–Robot Collaboration. Appl. Sci. 2023, 13, 5429.
Bruzzone, L.; Stretti, D. Application of Elliptic Jerk Motion Profile to Cartesian Space
Position Control of a Serial Robot. Appl. Sci. 2023, 13, 5601.
Tonan, M.; Doria, A.; Bottin, M.; Rosati, G. Influence of Joint Stiffness and Motion
Time on the Trajectories of Underactuated Robots. Appl. Sci. 2023, 13, 6939.

5.

4.

6. Almazrouei, K.; Kamel, I.; Rabie, T. Dynamic Obstacle Avoidance and Path Planning

through Reinforcement Learning. Appl. Sci. 2023, 13, 8174.

7. Marx, L.; Pálsdóttir, Á.A.; Andreasen Struijk, L.N. Frame-Based Slip Detection for an
Underactuated Robotic Gripper for Assistance of Users with Disabilities. Appl. Sci.
2023, 13, 8620.
Kilikeviˇcius, S.; Liutkauskien ˙e, K.; ˇCesnaviˇcius, R.; Keršys, A.; Makaras, R. Inves-
tigation of the Motion Characteristics of Parts on a Platform Subjected to Planar
Oscillations. Appl. Sci. 2023, 13, 9576.

8.

9. Mystkowski, A.; Wolniakowski, A.; Kadri, N.; Sewiolo, M.; Scalera, L. Neural Network
Learning Algorithms for High-Precision Position Control and Drift Attenuation in
Robotic Manipulators. Appl. Sci. 2023, 13, 10854.

10. Hung, C.W.; Jiang, G.Y. Application of External Torque Observer and Virtual Force

Sensor for a 6-DOF Robot. Appl. Sci. 2023, 13, 10917.

11. Batista, J.G.; Ramalho, G.L.; Torres, M.A.; Oliveira, A.L.; Ferreira, D.S. Collision
Avoidance for a Selective Compliance Assembly Robot Arm Manipulator Using
Topological Path Planning. Appl. Sci. 2023, 13, 11642.
Fang, Y.; Zhu, G.N.; Zhao, Y.Z.; Gu, C. Design Procedure of Motion Profiles with
Sinusoidal Jerk for Vibration Reduction. Appl. Sci. 2023, 13, 13320.

12.

References

1.

2.

3.
4.

5.

6.

7.

8.

Javaid, M.; Haleem, A.; Singh, R.P.; Suman, R. Substantial capabilities of robotics in enhancing Industry 4.0 implementation.
Cogn. Robot. 2021, 1, 58–75. [CrossRef]
Biagiotti, L.; Melchiorri, C. Trajectory Planning for Automatic Machines and Robots; Springer Science & Business Media:
Berlin/Heidelberg, Germany, 2008.
Siciliano, B.; Khatib, O.; Kröger, T. Springer Handbook of Robotics; Springer: Berlin/Heidelberg, Germany, 2008; Volume 200.
Corke, P.I.; Jachimczyk, W.; Pillat, R. Robotics, Vision and Control: Fundamental Algorithms in MATLAB; Springer: Berlin/Heidelberg,
Germany, 2011; Volume 73.
Paes, K.; Dewulf, W.; Vander Elst, K.; Kellens, K.; Slaets, P. Energy efficient trajectories for an industrial ABB robot. Procedia Cirp
2014, 15, 105–110. [CrossRef]
Carabin, G.; Scalera, L. On the trajectory planning for energy efficiency in industrial robotic systems. Robotics 2020, 9, 89.
[CrossRef]
Boscariol, P.; Richiedei, D. Energy-efficient design of multipoint trajectories for Cartesian robots. Int. J. Adv. Manuf. Technol. 2019,
102, 1853–1870. [CrossRef]
Gasparetto, A.; Zanotto, V. A new method for smooth trajectory planning of robot manipulators. Mech. Mach. Theory 2007,
42, 455–471. [CrossRef]

9. Haschke, R.; Weitnauer, E.; Ritter, H. On-line planning of time-optimal, jerk-limited trajectories. In Proceedings of the 2008
IEEE/RSJ International Conference on Intelligent Robots and Systems, Nice, France, 22–26 September 2008; pp. 3248–3253.
10. Bianco, C.G.L.; Ghilardelli, F. A scaling algorithm for the generation of jerk-limited trajectories in the operational space. Robot.

Comput.-Integr. Manuf. 2017, 44, 284–295. [CrossRef]

11. Vicentini, F. Collaborative robotics: A survey. J. Mech. Des. 2021, 143, 040802. [CrossRef]
12.

Scalera, L.; Vidoni, R.; Giusti, A. Optimal scaling of dynamic safety zones for collaborative robotics. In Proceedings of the 2021
IEEE International Conference on Robotics and Automation (ICRA), Xi’an, China, 30 May–5 June 2021; pp. 3822–3828.
Scalera, L.; Giusti, A.; Vidoni, R.; Gasparetto, A. Enhancing fluency and productivity in human-robot collaboration through
online scaling of dynamic safety zones.

Int. J. Adv. Manuf. Technol. 2022, 121, 6783–6798. [CrossRef]

13.

Appl. Sci. 2024, 14, 1179

5 of 5

14. Brady, M. Robot Motion: Planning and Control; MIT Press: Cambridge, MA, USA, 1982.
15. De Luca, A.; Oriolo, G. Trajectory planning and control for planar robots with passive last joint. Int. J. Robot. Res. 2002, 21, 575–590.

[CrossRef]

Disclaimer/Publisher’s Note: The statements, opinions and data contained in all publications are solely those of the individual
author(s) and contributor(s) and not of MDPI and/or the editor(s). MDPI and/or the editor(s) disclaim responsibility for any injury to
people or property resulting from any ideas, methods, instructions or products referred to in the content.

