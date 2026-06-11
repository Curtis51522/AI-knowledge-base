TYPE Original Research
PUBLISHED 13 November 2025
DOI 10.3389/fnbot.2025.1574044
Path planning of industrial robots
based on the adaptive field
OPEN ACCESS
EDITED BY cooperative sampling algorithm
Shude He,
Guangzhou University, China
REVIEWED BY Yongbo Zhuang 1, Sha Luo 1*, Qingdang Li 1*, Dianming Chu 1,
Mario Versaci,
Mediterranea University of Reggio Calabria, Wenjuan Bai 1, Xintao Liu 1, Mingyuan Fan 1 and Lv Wei 2
Italy
Isak Karabegović, 1 College of Electromechanical Engineering, Qingdao University of Science and Technology,
University of Bihać, Bosnia and Herzegovina Shandong Province, China, 2 Shandong Gaomi Technician Institute, Shandong Province, China
*CORRESPONDENCE
Sha Luo
luosha320@126.com For the low efficiency and poor generalization ability of path planning algorithm
Qingdang Li of industrial robots, this work proposes an adaptive field co-sampling algorithm
lqd@qust.edu.cn
(AFCS). Firstly, the environment complexity function is proposed to make full use
RECEIVED 10 February 2025 of environment information and improve its generalization ability of the traditional
ACCEPTED 25 August 2025
rapidly random search tree algorithm (RRT) algorithm. Then an optimal sampling
PUBLISHED 13 November 2025
CORRECTED 18 December 2025 strategy is proposed to make the improvement of the efficiency and optimal
direction of RRT algorithm. Finally, this article designs a collaborative extension
CITATION
Zhuang Y, Luo S, Li Q, Chu D, Bai W, Liu X, strategy, which introduces the improved artificial potential field algorithm (APF)
Fan M and Wei L (2025) Path planning of into the traditional RRT algorithm to determine the new nodes, so as to improve
industrial robots based on the adaptive field
the orientation and expansion efficiency of the algorithm. The proposed AFCS
cooperative sampling algorithm.
Front. Neurorobot. 19:1574044. algorithm completes simulation experiments in two environments with different
doi: 10.3389/fnbot.2025.1574044 complexity. Compared with the traditional RRT, RRT* and tRRT algorithm, the results
COPYRIGHT show that the AFCS algorithm has achieved great improvement in environmental
© 2025 Zhuang, Luo, Li, Chu, Bai, Liu, Fan
adaptability, stability and efficiency. At last, ROKAE industrial robot is taken as the
and Wei. This is an open-access article
distributed under the terms of the Creative object to build a simulation environment for the path planning, which further
Commons Attribution License (CC BY). The verifies the practicability of the algorithm.
use, distribution or reproduction in other
forums is permitted, provided the original
author(s) and the copyright owner(s) are KEYWORDS
credited and that the original publication in
industrial robot, path planning, RRT, APF, AFCs
this journal is cited, in accordance with
accepted academic practice. No use,
distribution or reproduction is permitted
which does not comply with these terms. 1 Introduction
Recently, the demand for intelligent robots is gradually increasing with the continuous
development of artificial intelligence technology. Especially for industrial robots, path
planning is a decisive factor to determine their safe operation. It refers to the autonomous
planning of industrial robots in their configuration space to find a continuous non-collision
smooth path between the initial pose and the target pose in order to reach the preset target
pose when moving in the surrounding static and dynamic obstacle environment. Meanwhile,
it must meet various constraints such as environmental, time and dynamic constraints of
industrial robots (Wei and Ren, 2018). Different from that of mobile robots, it is more complex
for industrial robots to realize path panning. It not only needs to consider constraints such as
obstacles, but also involves the mutual transformation of joint space and configuration space.
Therefore, the path planning algorithm of mobile robots is not completely applicable to the
path planning of industrial robots. At present, there are three kinds of path planning
algorithms of industrial robots: traditional obstacle avoidance planning method (Khatib, 1986;
Hart et al., 1972), intelligent obstacle avoidance planning algorithm (Guan-Zheng and Huan,
2007; Kavraki et al., 1994), sampling-based obstacle avoidance planning algorithm (Lavalle,
1998; Karman and Frazzoli, 2011). Among them, the sample-based RRT algorithm (Lavalle,
1998) is the most applicable one in path planning algorithms of industrial robots, who has the
characteristics of probability completeness and high dimensional space applicability (Lixing
Frontiers in Neurorobotics 01 frontiersin.org

Zhuang et al. 10.3389/fnbot.2025.1574044
Liu et al., 2023). And it was also proved that the sample-based RRT • A new algorithm called AFCS is proposed,which not only
algorithm owned the better efficiency and more smoother path than enhances the environmental adaptability of industrial robots, but
the intelligent obstacle avoidance planning algorithm for the industrial also improves sampling quality and scaling efficiency of the path
robots (Larsena, 2017). However, the traditional RRT algorithm has planning algorithm. The whole algorithm provides ideas for
some problems such as redundant sampling, low efficiency and improving the intelligence of the path planning algorithm.
non-optimal path, which limit its generalization ability in complex
environment (Jia et al., 2022). For these problems, research and The rest of this article is arranged as follows: The principle of path
improvement of RRT algorithm is a hot topic pursued by planning of robots is analyzed, and the principle of the traditional path
many scholars. planning algorithm is introduced in section 2. Then the AFCS
Among the variants of RRT algorithm, neither RRT algorithm, algorithms is introduced in section 3. Section 4, summary and analysis.
RRT* algorithm (Karman and Frazzoli, 2011) nor Informed RRT*
algorithm (Gammell et al., 2014) fundamentally solve the
2 Materials and models
randomness, low efficiency and optimality. Especially, in the
sampling stage, redundant sampling brings a large number of
branches, which not only leads to low efficiency, but also occupies For industrial robots, it is a prerequisite for path planning to
a large amount of memory space. Therefore, based on the above satisfy constraints in terms of kinematics and dynamics. In this article,
algorithms, scholars have make some research on RRT algorithm the relevant theories of industrial robot path planning are further
from the aspects of sampling and expansion strategy. In terms of studied based on the full study of the kinematics of industrial robots.
sampling strategies, the paper (Biao and Cao, 2021; Khan, 2020)
adopted target paranoia to achieve “de-randomness.” But this
2.1 Kinematic model of manipulators
strategy only reduced a small amount of the redundant sampling.
Therefore, to further reducing the sampling space, Liu et al. (2020),
Chi et al. (2022) and Ganesan and Natarajan (2021) set the sampling Path planning of industrial robot needs mutual transformation in
interval of the traditional RRT algorithm in different ways to make joint space and Cartesian space. So it involves the solution of inverse
the search more efficient. On the aspect of the extension strategy, kinematics. And the accuracy of the inverse kinematics solution also
the paper (Zhang et al., 2019; Wang et al., 2020; Kang et al., 2016; certainly affects the accuracy of path planning of industrial robots. In
Kang, 2019; Khan, 2020) fused the RRT algorithm with APF this paper, ROKAE 6-DOF industrial robot is taken as the research
algorithm. Specifically, it used the attractive action to guide the object, and the coordinate system is established according to the DH
production of new nodes and improve the search speed of the model (Hartenberg et al., 1964) as shown in Figure 1.
algorithm. In this process, although the target attraction is Based on the homogeneous coordinate transformation matrix, the
introduced, the repulsion of obstacles is not considered, so the role position and pose of the two adjacent coordinate systems i, i−1 of the
of the APF algorithm cannot be fully simulated. Wang et al. (2022), industrial robot are obtained as follows:
Kabutan and Nishida (2018) get new nodes by the guiding effect of
target gravity and obstacle repulsion. It improved not only the goal cosθ i −sinθ icosα i sinθ isinα i aicosθ i 
 
o
d
r
is
ie
a
n
d
t
v
a
a
t
n
io
ta
n
g e
b
s
u t
o f
a l
u
so
n r
t
e
h
a
e
c h
o
a
b
b
s
l
t
e
a c
t
l
a
e
r g
a
e
v
t
o
a
id
n
a
d
n
l
c
o
e
c
a
a
b
l
i
m
lit
i
y
n
.
im
Bu
a
t
,
w
th
i
e
th
A
t
P
h
F
e i−1 iT= 

sin
0
θ i cos
s
θ
in
ic
α
o
i
sα i −co
c
s
o
θ
s
i
α
si
i
nα i ais
d
in
i
θ i

(1)
 
algorithm made the RRT algorithm unable to find new sampling  0 0 0 1 
points in some cases (Yin et al., 2018). Therefore, a path planning
algorithm with strong stability, high efficiency and strong
generalization ability is urgently needed for the characteristics of
high latitude and complex collision detection process of
industrial robots.
To get more improvement on the adaptability and stability of the
path planning algorithm, an APCS algorithm is proposed, which
combines the efficient search and optimization ability of the improved
APF algorithm with the completeness of the RRT algorithm. And it
fundamentally solves the problem of environment adaptability and
redundant sampling. Contributions of this paper are summarized
as follows:
• An environment complexity function is proposed to make path
planning algorithm adapt to the environment;
• An optimal sampling strategy is proposed, which not only makes
full use of environmental information, but also considers the
optimality of sampling points;
• A field cooperative expansion strategy is proposed, in which the
FIGURE 1
improved APF algorithm is proposed and guides the generation The coordinate system of ROKAE industrial robot.
of new nodes;
Frontiers in Neurorobotics 02 frontiersin.org

Zhuang et al. 10.3389/fnbot.2025.1574044
θ i represents the angle between the X axes of adjacent coordinate constraints. However, it is more and more difficult to model the
systems, α i represents the Angle between the Z axes of adjacent environment in the more complex scenario. The complexity of
coordinate systems, ai is the length of the common perpendicular of environment modeling is an important problem that restricts the path
the Z axis, di is the distance between ai and ai−1. planning of robots. This article puts forward the environmental
According to the DH method, it is easy to get the forward complexity function to counter the difficulty of environment
kinematics equation of the industrial robot as follows: modeling. This strategy realizes the prediction of the environment
where the path planning is located, and lays a theoretical foundation
nx ox ax px  for path planning algorithm to take full advantage of the environmental
 
0 6T=0 1T1 2T2 3T3 4T4 5T5 6T= 

n
nz
y o
oz
y a
az
y p
pz
y

(2) i
s
n
h
f
o
o
w
rm
n
a
i
t
n
io n
F
.
i g
Th
ur
i
e
s p
3
a
)
p
,
e
i
r
n
d e
w
s
h
ig
i
n
ch
s tw
th
o
e
k
s
i
u
n
p
d
e
s
r
o
io
f
r
e
i
n
ty
v ir
o
o
f
n
p
m
a
e
th
n t
p
m
la
a
n
p
n
s
i
(
n
a
g
s
 
0 0 0 1  algorithm can be better reflected.
As shown in Figure 3, the number of obstacles in two maps is the
same, but the complexity of the environment is different because of
Where,
i−1
1T represents the homogeneous transformation matrix the different distribution of obstacles. The pixel size of the two maps
of adjacent coordinate systems. According to the principle of forward is1500*1500. In this paper, the starting point position coordinate of
kinematics, the position and attitude of the industrial robot can path planning is (0, 0, 0), and the target point coordinate is set to
be solved according to Equation 2. The inverse kinematics solution is (1000, 1000, 1000).
the inverse process of the forward kinematics solution. In the path
planning of industrial robots, forward and inverse kinematics can
2.3 Path planning algorithm
be calculated as needed. The DH parameters of the ROKAE industrial
robot used in this paper are shown in Table 1.
The sampling-based RRT algorithm and APF algorithm are the
most widely used in path planning of industrial robots. By fully
2.2 Path planning and model of
studying the traditional APF algorithm and RRT algorithm, this
environment
article summarizes the advantages and disadvantages of the two
methods. At the same time, this article makes same improvement of
2.2.1 Path planning the traditional algorithms in view of their shortcomings, and a new
The core of path planning is planning, and its goal is to obtain a AFCS algorithm with strong environment adaptability is proposed.
path that satisfies the conditions. The path is a continuous curve in the
configuration space of robots. Specifically, path planning may be to 2.3.1 RRT algorithm
plan a non-collision and shortest path for mobile robots in There is a path search algorithm called the RRT algorithm, which
two-dimensional space. It also can plan a safe, non-collision or expands by random sampling. It establishes the search tree from the
relatively optimized path for industrial robots (as shown in Figure 2). starting point. Subsequently, it undergoes random sampling, expands
Jiang Xinsong, the father of Chinese robots, defines path planning as new nodes, avoids obstacles, and finally finds an optimal path.
follow: The goal of path planning is to get a non-collision path in the Figure 4 shows the implementation process of the traditional RRT
environment with obstacles according to certain evaluation criteria algorithm, and its pseudo-code is shown in Figure 5.
(Hong et al., 2022). Deservedly, the different distribution of obstacles The core of traditional RRT algorithm can be divided into four
in the environment directly affects the planned path, and the target stages: sampling, expansion, collision detection and path query. There
location determination is provided by the higher-level task are three important factors that lead to the low efficiency and poor
decomposition module (Hong et al., 2022). applicability of RRT algorithm, which are the redundant sampling in
the sampling phase, the way and efficiency of generating new nodes
2.2.2 Model of environment in the expansion phase, and the amount of calculation in collision
In traditional path planning, environment modeling is the first detection (Junxiang and Wang, 2021). Especially in the sampling
step of path planning in order to better satisfy configuration space stage, the redundant sampling not only has strong randomness, but
also does not consider the optimality of sampling. Moreover, in the
measurement connection stage, the generation of new nodes is neither
TABLE 1 The DH parameters of the ROKAE industrial robot.
guided nor considering the influence of obstacles, so that the
calculation of collision detection of the RRT algorithm is very large.
i di (mm) αi (deg) ai (mm) θi (deg)
Generally, the randomness and efficiency of the RRT algorithm are
1 508 −90 160 θ1 important factors affecting its development. Therefore, this paper
proposes an efficient RRT algorithm to solve the strong randomness
2 0 0 790 θ2 and low efficiency.
3 0 −90 155 θ3
2.3.2 APF algorithm
4 795 90 0 θ4
The APF algorithm is a simple and effective local path planning
5 0 −90 0 θ5 algorithm. It constructed by Dr. Oussama Khatib who introduced the
concept of “field” in traditional mechanics (Fan et al., 2020; Rostami,
6 145 0 0 θ6
2019). The potential field includes the attractive and repulsive
Frontiers in Neurorobotics 03 frontiersin.org

| Zhuang et al.  |     |     |     |     | 10.3389/fnbot.2025.1574044 |     |     |
| -------------- | --- | --- | --- | --- | -------------------------- | --- | --- |
FIGURE 2
The schematic diagram of path planning of robots.
FIGURE 3
Two environmental maps with different complexity.
( )
potential field, which are formed by the target and the obstacle,  by the node P is expressed as Urep P ,kr is the repulsion coefficient;
respectively. The agent moves along the resultant force of the attractive  ||P−Pobs|| denotes the distance between two nodes P and Pobs;  D2
and repulsive forces (Yuan et al., 2021). The attractive and repulsive  indicates  the  influence  threshold  of  an  obstacle;  When
potential field functions are modeled as follows ||P−Pobs||≥D2  the node is not affected by obstacles; When
,
P−Pgoal <D2, the node is affected by the repulsive potential field of
|     | ( )=   | 1 P−Pgoal | the obstacle. |     |     |     |     |
| --- | ------ | --------- | ------------- | --- | --- | --- | --- |
|     | Uatt P | kt        | (3)           |     |     |     |     |
2 The model of the attractive and repulsive forces are shown
|     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- |
as follow:
|     |    | dP||−Pobs||≥D2 |     |     |     |     |     |
| --- | --- | -------------- | --- | --- | --- | --- | --- |
0

| Urep (      | P )=                                                     |                   |       | Fatt ( P )=−∆Uaat | ( P )=kt||P−Pgoal|| |     |     |
| ----------- | ---------------------------------------------------------- | ------------------ | ----- | ----------------- | ------------------- | --- | --- |
|             | k r 1                                                      | 1                  | (4)   |                   |                     |     | (5) |
|             |                                                          | −  dP−||Pobs||<D2 |       |                   |                     |     |     |
|             | 2 ||P− Pobs||                                             | D                 |       |                   |                     |     |     |
|             |                                                           | 2                  |       |                   |                     |     |     |
|             |                                                            |                    |       | ( )=−∆Urep        | ( )=                |     |     |
|             |                                                            |                    |       | Frep P            | P                   |     |     |
|             |                                                            |                    |       |  0               | d||P−Pobs||≥D2      |     |     |
| Where, Uatt | ( P )  denotes the attractive potential field of the node  |                    |       |                  |                     |     |     |
|             |                                                            |                    |       |   1             | 1                  |     |     |
|             |                                                            |                    |       | −kr               | − d||P−Pobs||<D2    |     | (6) |
P , k t  is   t h e  a t tr a c t iv e   c o e ffi c i e n t. | | P − P g o a l | |   d e n o t e s  t h e   d is t a n c e    
|     |     |     |     |   ||P−Pobs|| | D2 |     |     |
| --- | --- | --- | --- | -------------- | --- | --- | --- |
be t w e e n   tw o   n o d e s  P   a n d   Pg ; Th e  r ep u ls i v e   p o t e n t ia l  fi e l d  g e n e r a te d
|                            | o a l |     |     |     |     |                 |     |
| -------------------------- | ----- | --- | --- | --- | --- | --------------- | --- |
| Frontiers in Neurorobotics |       |     | 04  |     |     | frontiersin.org |     |

Zhuang et al.  10.3389/fnbot.2025.1574044
FIGURE 4
The implementation of the RRT algorithm.
The resultant force of attraction and repulsion is shown as follow: APF algorithm, and introduces it into the traditional RRT algorithm
to improve its real-time performance.
|     | ( )=Fatt | ( )+Frep ( ) |     |     |
| --- | -------- | ------------ | --- | --- |
|     | Ftotal P | P P          | (7) |     |
2.4 The adaptive field cooperative sampling
| The agent realizes obstacle avoidance path planning under the  |     |     | algorithm |     |
| -------------------------------------------------------------- | --- | --- | --------- | --- |
guidance of the resultant force, and its schematic diagram is shown in
Figure 6. On  the  principle  of  path  planning  algorithm,  this  paper
On the basis of the principle of the APF algorithm, it can  innovatively put forward an adaptive field cooperative sampling
be known that the magnitude of the attraction and repulsion force of  algorithm. Firstly, the environment complexity function is proposed
the agent are related to the corresponding distance. So its main  for the difficulty of environment modeling. Then, an improved APF
disadvantages are the inaccessible target and local minimum (Wang  algorithm is proposed to solve the inaccessible target and local
et al., 2022). Otherwise, the essence of the APF algorithm is a control  minimum. Finally, based on the framework of the traditional RRT
method, and its path is generated by the control quantity in real time.  algorithm, an optimal sampling strategy is proposed, and the AFCS
Therefore,  its  real-time  performance  is  more  strong.  For  the  algorithm is obtained by introducing the environment complexity
shortcomings of the APF algorithm, this paper proposes an improved  function and the improved APF algorithm into the RRT algorithm.
| Frontiers in Neurorobotics |     |     | 05  | frontiersin.org |
| -------------------------- | --- | --- | --- | --------------- |

| Zhuang et al.  |     |     |     |     | 10.3389/fnbot.2025.1574044 |
| -------------- | --- | --- | --- | --- | -------------------------- |
FIGURE 6
The schematic diagram of path planning of the APF algorithm.
minimum distance between obstacles is 883 mm. The green sphere
environment is relatively complex. Therefore, the design of the
environment complexity function is reasonable.
2.4.2 Optimal sampling strategy
For the RRT algorithm and its variants, the ideal sampling
procedure is one that reduces redundant sampling while keeping the
sampling point on or near the optimal path as much as possible. Based
on the above ideas, this article proposes an optimal sampling strategy
to solve redundant sampling and poor quality of sampling points in
the sampling stage. The idea of this strategy is to randomly generate
FIGURE 5
The pseudo-code of the traditional RRT algorithm. multiple sampling points at the same time, and then determine the
sampling quality function based on the density of obstacles around the
sampling points and the smoothness of the path. In this way, random
sampling points with optimal quality can be obtained. The sampling
2.4.1 Environment complexity function quality function is modeled as follows:
Aiming at the complex of environment modeling, this article
|     |     |     |     | ∗ρ  | ∗σ  |
| --- | --- | --- | --- | --- | --- |
designs the environment complexity function S based on the relative  MP =w1 +w2 (9)
|     |     |     |     | randi P randi | P randi  |
| --- | --- | --- | --- | ------------- | -------- |
position of obstacles in the environment. Then it is introduced into
t h e   t r a d i ti o n a l   R R T   a l g o r i t h m .   Th i s  op e ra t i o n   e n a bl e s  t h e  a lg o r it h m   max||Pra −Pobs||
|     |     |     |     | = ndi |     |
| --- | --- | --- | --- | ----- | --- |
to   i n t e l li g e n tl y   a d ju s t   t h e  i t e r at i o n  t im e  in s t e a d   o f  m a n u a l ly  a d ju s t in g  Prandi (10)
A
|                 |             |                                 |          |     |     |
| --------------- | ----------- | ------------------------------- | -------- | --- | --- |
| the  iteration  | parameters  | according  to  the  complexity  | of  the  |     |     |
e n v i ro n m e n t.  A n d   i t  al so   im p r o v es   it s   e n v i r o n m e n t a l  a d a p t a b il it y .  O n   ∠Prandi
P n ea restPk−1
σ randi = (11)
th e   b as i s o f  t h e  v o l u m e  r a tio   o f  o b s t a c l e s ,  t h i s a r t ic l e   in t r o d u c e s   th e  
|     |     |     |     | 1 8 0 |     |
| --- | --- | --- | --- | ----- | --- |
distance between obstacles to further distinguish the complexity, so as
to make the path planning algorithm suitable for environments with
different  complexity.  The  environment  complexity  function  is  Where, MP  represents the quality function of the i random
randi
as follows: sampling point Prandi. ρ  is the density of obstacles around the
P
|     |     |     | random sampling point Prandi. σ | randi                                |     |
| --- | --- | --- | ------------------------------- | ------------------------------------ | --- |
|     |     |     |                                 | P  represents the smoothness of the  |     |
|     |     | e10 |                                 | r a nd i                             |     |
n1V r a n d o m   s a m p li n g   p o in t   P .   | | P − P ||   r ep r e s e n t s   t h e
|     | S=λ | ob s 1 | (8) | ra n d i | r a n d i o b s |
| --- | --- | ------ | --- | -------- | --------------- |
1 3 d is t a n ce  b e t w ee n   th e   ra n d o m   s a m p l i n g   p o i nt   P  a n d  t h e   n e a r e s t
|     |     | V L   |                                                                          |     | ra n di |
| --- | --- | ----- | ------------------------------------------------------------------------ | --- | ------- |
|     |     |       | obstacle Pobs ∠PrandiPnearestPk−1 represents the angle between the line  |     |         |
PrandiPnearest and PnearestPk−1w1,w2 represent the influence factors of
Where, S represents the environment complexity. n1 respectively  obstacle density and smoothness of sampling points.
indicates the number of static in the environment (Urain et al., 2023).  The schematic diagram of optimal sampling process is shown in
| Vobs1 represents the volume of static obstacles. V represents the total  |     |     | Figure 7. |     |     |
| ------------------------------------------------------------------------ | --- | --- | --------- | --- | --- |
| volume. Only one class of static obstacle cases is studied here, so λ    |     |     | 1 =1.     |     |     |
According to the proposed environment complexity function, the  2.4.3 Field cooperative expansion strategy
environment complexity of the two maps in Figure 4 can be,
respectively, calculated as: 2301, 1809. Although the number of  2.4.3.1 The improved APF algorithm
obstacles in the two maps is the same, the relative position of obstacles  For the problem of the inaccessible target and local minimum, this
is different. In the green sphere environment, the minimum distance  article, respectively, introduces the distance between the target point
between obstacles is 697 mm. In the red sphere environment, the  and the robot into the attractive potential field and the repulsive
| Frontiers in Neurorobotics |     |     | 06  |     | frontiersin.org |
| -------------------------- | --- | --- | --- | --- | --------------- |

| Zhuang et al.  |     |     |     |     |     |     |     |     |     |     |     | 10.3389/fnbot.2025.1574044 |     |     |
| -------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | -------------------------- | --- | --- |
FIGURE 7
The schematic diagram of optimal sampling process (the blue path represents the optimal sampling process, and the black path represents the path
generated by the random sampling process).
potential field function of the traditional APF algorithm. Based on  The attractive and repulsive function models are shown as follows:
papers (Ahmadi et al., 2022; Guo et al., 2022), the attractive and
r e p u l s iv e  potential field models proposed in this paper are shown   k ||P − P || d | | P − P | |≤ D
|         |           |      |          |         |               |           |      | (    | )=   | t          | g o a l                |       | g o a       | l 1         |
| ------- | --------- | ---- | -------- | ------- | ------------- | --------- | ---- | ---- | ---- | ---------- | ---------------------- | ----- | ----------- | ----------- |
| a s  fo | l l o w : |      |          |         |               |           |      | Fatt | P   |            |                        |       |             | (14)        |
|         |           |      |          |         |               |           |      |      | D1 | ⋅kt ⋅ | |P | − Pg o a l || − kt ⋅D1 | d | | | P − P g o a | l | | > D 1 |
|         |           |      |          |         |               |           |      |      |      |            |                        |       |             |             |
|         |           |  k  | || P − P | ||      |               |           |      | (    | )    |            |                        |       |             |             |
|         |           |      | t        | g o a l | −             | |≤        |      | F P  | =    |            |                        |       |             |             |
|         |           |     |          |         | d | | P P g o | a l | D 1 |      | r ep |      |            |                        |       |             |             |
|         | (         | )=  | 2        |         |               |           |      |     |      | 0          |                        | d     | | | P − P   | s| | ≥ D    |
|         | Uatt P    |     |          |         |               |           | (12) |      |      |            |                        |       | o           | b 2         |
|         |           |      |          |         | 2             |           |      |     |      |            |                        |       |             |             |
|         |           |     |          | kt D1   |               |           |      |    | 1    | 1          |                       |       |             |             |
 D1kt| | P − P go a l | | − d | | P − P g o a l | | > D 1 − − +σ||P−Pgoal|| − < (15)
|     |     |     |     | 2   |     |     |     |  kr  |               |     |    | d   | | | P Po | b s | | D 2 |
| --- | --- | --- | --- | --- | --- | --- | --- | ------ | ------------- | --- | --- | --- | -------- | ----------- |
|     |     |     |     |     |     |     |     |      | | | P− Pobs|| | D   | 2  |     |          |             |
|     |     |     |     |     |     |     |     |        |               |     |     |     |          |             |
( )= In this paper, the field cooperative expansion strategy is to
Urep P
introduce the improved APF algorithm into the traditional RRT
|    |     |     |     |     | d||P−Pobs||≥D2 |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | -------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
0
 algorithm. The position and orientation of the new nodes are
|    |    |     |    |     |     |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
k r 1 − 1 − 1 σ||P−Pgoal|| d||P−Pobs||<D2 (13) c a lc u la t e d  a c c o r d i n g  t o  the improved APF algorithm. The new node
|    |        |          |    |     |     |     |      |             |                  |             |     |     |     |     |
| --- | ------- | -------- | --- | --- | --- | --- | ---- | ----------- | ---------------- | ----------- | --- | --- | --- | --- |
|    | 2 ||P− | Pobs|| D |  2 |     |     |     |      |             |                  |             |     |     |     |     |
|     |         |          | 2   |     |     |     |   is |  c a lc u l | a te d  a s   fo | l l o w s : |     |     |     |     |
F ( P )
t o t a l
|     |     | ( ) |     |     |     |     |     |     | Pnew | =Pnearest | +β 1Prand +β | 2   |     | (16) |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | ---- | --------- | ------------ | --- | --- | ---- |
W h e r e ,  U att P   r e p re se n ts   t h e  a t tr a c t i v e   p o t e n t ia l  fi e ld , k t   is   t h e   || F ( P ) ||
|       |             |                      |         |            |                              |                   |           |     |     |     |     | t o t a | l   |     |
| ----- | ----------- | -------------------- | ------- | ---------- | ---------------------------- | ----------------- | --------- | --- | --- | --- | --- | ------- | --- | --- |
| attra | cti v e   c | o effi ci e n t.   | | | P − P | | |  d e n | o t e s   t h e   d i st a n | c e  b e tw e e n |   t w o   |     |     |     |     |         |     |     |
go a l
n o d e s  P a n d  t   P g o a l.   D 1  r e p r es e n t s  t h e  th r es h o l d   f o r  th e   n o d e   to   r e a ch   ( )=Fatt ( )+Frep ( )
|     |     |     |     |     |     |     |     |     |     | Ftotal | P P | P   |     | (17) |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ------ | --- | --- | --- | ---- |
th e  t a r ge t  p o i n t .   W h e n   | | P − P | |≤ D ,  t h e   r o b o t  a p p r o a c h e s   th e
|     |     |     |     | g o a l | 1   |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | ------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
target point at a faster speed. Otherwise, the robot approaches the  Where, Pnew is the new node. Prand represents the random
|     |     |     |     |     | ( ) |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
target point at a slower speed. Urep P  represents the repulsive  sampling point, whose nearest point on the random tree is expressed
potential field. kr is the repulsion coefficient. ||P−Pobs|| denotes the  as Pnearest. β 1,β 2 represents the influence factors of the random node
( )
distance between two nodes P and Pobs;  D2 indicates the influence  and target gravity on the new node. Ftotal P  represents the resultant
( )
threshold of an obstacle. σ represents the distance influence factor.  force of the potential field. Fatt P  represents the sum of the attractive
When ||P−Pobs||≥D2,  the node is not affected by obstacles; When  forces of the random node and the target node on the new node.
( )
||P−Pgoal||<D2 , the repulsive potential field of the obstacle dose  Frep P  represents the sum of the repulsive forces of obstacles on
| not work.                  |     |     |     |     |     |     | new nodes. |     |     |     |     |     |     |                 |
| -------------------------- | --- | --- | --- | --- | --- | --- | ---------- | --- | --- | --- | --- | --- | --- | --------------- |
| Frontiers in Neurorobotics |     |     |     |     |     |     | 07         |     |     |     |     |     |     | frontiersin.org |

Zhuang et al. 10.3389/fnbot.2025.1574044
The schematic diagram of field cooperative expansion strategy is In the aspect of industrial robot simulation, this paper mainly
shown in Figure 8. integrates the AFCS algorithm with industrial robot simulation to
verify its effectiveness and practicability.
2.4.4 The adaptive field cooperative sampling In two maps with different complexity, this article conducts
algorithm multiple simulation experiments with the same number of iterations
Based on the above innovative strategy, an adaptive field and step size, respectively. The multiple operation results of the
co-sampling algorithm is proposed in this paper. It not only avoids traditional RRT algorithm and RRT* algorithm are shown in
complex environment modeling, but also makes full use of Figures 11, 12.
environment information. Moreover it solves the redundant sampling In Figures 11, 12, the RRT algorithm and RRT* algorithm fail the
and low efficiency of traditional RRT algorithm by the optimal path planning due to the large amount of redundant sampling in the
sampling strategy and the introduction of improved APF algorithm. tow environments. Although both RRT and RRT* algorithms are
The flow chart of the AFCS algorithm is shown in Figure 9. probabilistic complete, such a time-consuming strategy is not
The pseudo-code of the AFCS algorithm is shown in Figure 10. desirable in practice. Therefore, this article focuses on the comparison
and analysis of simulation results between the AFCS algorithm and
the most representative tRRT algorithm.
3 Experiments and results
3.1 Experiment of algorithm simulation
Simulation experiment is an important way to show the
superiority of the algorithm. The simulation experiment in this paper
is carried out in two aspects: algorithm simulation and industrial 3.1.1 Analysis of environmental adaptability
robot simulation. Environmental adaptability is an embodiment of the intelligence
In terms of algorithm simulation, two environments with of path planning algorithm. It is also an important direction to
different complexity are used to carry out simulation experiments improve the intelligence of industrial robots. Five consecutive
to verify the environmental adaptability of the algorithm. At the simulation experiments are carried out in two environments with
same time, this paper verifies the effectiveness and practicability different complexity (as shown in Figures 13, 14) to verify the
of the AFCS algorithm by analyzing the experimental results with environmental adaptability of the algorithm. It should be noted that
the traditional RRT algorithm, RRT* algorithm and tRRT the number of iterations of the AFCS algorithm is related to the
algorithm from three aspects: planning time, path cost and the environment complexity function without manual mediation. The
number of path points. iteration and step size of the tRRT algorithm are the same.
FIGURE 8
The schematic diagram of field cooperative expansion strategy.
Frontiers in Neurorobotics 08 frontiersin.org

Zhuang et al. 10.3389/fnbot.2025.1574044
FIGURE 9
The flow chart of the AFCS algorithm.
algorithm changes (from red sphere environment to green sphere
environment), the branches of its path becomes more and more.
Therefore, the proposed AFCS algorithm has better adaptability to the
environment and higher stability.
3.1.2 Analysis of efficiency
Time is an important reflection of efficiency. In this paper, the
planning time of the algorithm in the same environment is taken as
one of the criteria to measure the efficiency of the algorithm. The
AFCS algorithm and tRRT algorithm are run 10 times in two
environments with different complexity to obtain the average planning
time of the algorithm (as shown in Table 2).
According to the data in Table 2, in the environment with different
complexity, the planning time of the AFCS algorithm remains stable
and does not float with the change of environment. In contrast, the
efficiency of the tRRT algorithm fluctuates by about 27% as the
complexity of the environment changes. This fluctuation of operating
efficiency will affect the expansion of application scenarios of the
algorithm. On the other hand, in the environment with the same
complexity, the AFCS algorithm has shorter planning time and higher
stability than the tRRT algorithm.
This paper runs the AFCS algorithm and the tRRT algorithm for
20 times, respectively, in the green sphere environment to further
FIGURE 10
The pseudo-code of the AFCS algorithm. verify the stability of the AFCS algorithm. The path planning time of
the two algorithms is shown in Table 3.
In Table 3, the planning time of 20 times of the AFCS algorithm
It can be seen from Figures 13, 14 that the results of the AFCS is stable between 3.904 s–5.2919 s, and the planning time fluctuates
algorithm are more stable. And the branches of the path obtained by little in the green sphere environment. However, the 20 times path
the AFCS algorithm are less. But when the environment of the tRRT planning time of tRRT algorithm fluctuates from 4.4478 s to 46.7573 s.
Frontiers in Neurorobotics 09 frontiersin.org

Zhuang et al. 10.3389/fnbot.2025.1574044
FIGURE 11
The simulation results of the RRT algorithm in two environments.
FIGURE 12
The simulation results of the RRT* algorithm in two environments.
Therefore, the AFCS algorithm not only has high planning efficiency, adaptive field co-sampling algorithm is shorter. After running the
but also has good stability. algorithm 5 times, the path cost float of the AFCS algorithm is smaller
than that of the tRRT algorithm, which indicates that the AFCS
3.1.3 Analysis of path quality algorithm has better stability.
Path quality is an important factor to measure the planning In this paper, the AFCS algorithm and tRRT algorithm were run
efficiency of the algorithm. Path cost and the number of path nodes five times, respectively, in two environments, and the number of path
are important performances of path quality. In this paper, the sum nodes was obtained, as shown in Figure 16.
of distance between nodes on the path is taken as the path cost. In In Figure 16, the number of path nodes planned by the AFCS
this paper, the path cost obtained by running the AFCS algorithm algorithm for five times is also smaller than that of the tRRT algorithm
and tRRT algorithm 5 times in two environments is shown in in the red sphere environment, and the number of nodes decreases
Figure 15. within a range of 2–5%. In the green sphere environment, the
In Figure 15, the path cost of the AFCS algorithm is about 20% advantage of the adaptive field co-sampling algorithm is more obvious,
smaller than that of the tRRT algorithm in the red sphere environment. and the reduction interval of the number of path nodes for 5 times is
In a more complex environment (green sphere environment), the path 21.1–50%. For different complex environments, the number of path
cost of the adaptive field co-sampling algorithm is about 50% less than nodes of the AFCS algorithm fluctuates little, ranging from 1.4
that of the tRRT algorithm, which indicates that the path of the to 5.4%.
Frontiers in Neurorobotics 10 frontiersin.org

| Zhuang et al.  |     |     |     |     |     | 10.3389/fnbot.2025.1574044 |     |
| -------------- | --- | --- | --- | --- | --- | -------------------------- | --- |
FIGURE 13
Five consecutive simulation results of the tRRT algorithm.
FIGURE 14
Five consecutive simulation results of the AFCS algorithm.
TABLE 2 The planning time of the AFCS algorithm and tRRT algorithm. environment. The whole system of the path planning experiment is
composed of computer, ROKAE industrial robot XB20 and ZED2
| i   | Green Ball |      | Red Ball  |                 |               |                     |               |
| --- | ---------- | ---- | --------- | --------------- | ------------- | ------------------- | ------------- |
|     |            |      |           | depth  camera.  | Among  them,  | the  communication  | and  logical  |
|     | AFCS       | tRRT | AFCS tRRT |                 |               |                     |               |
relationship of the three hardware devices are shown in Figure 17.
Based on the above hardware devices, the experimental flow is
| 1   | 4.8414 | 7.4142 4.7543 | 4.4731 |     |     |     |     |
| --- | ------ | ------------- | ------ | --- | --- | --- | --- |
shown in Figure 18. The whole process of the experiment consisted of
| 2   | 4.5426 | 5.9894 4.3211 | 4.9958 |     |     |     |     |
| --- | ------ | ------------- | ------ | --- | --- | --- | --- |
three parts (as shown in Figure 18). The first one is obstacle
3 4.5295 5.2871 4.4687 4.3985 recognition based on ZED2 depth camera, which mainly obtains the
| 4   | 3.8931 | 6.4891 4.3451 | 4.6828 |     |     |     |     |
| --- | ------ | ------------- | ------ | --- | --- | --- | --- |
position of obstacles for path planning of industrial robots. The
5 4.6952 5.3633 4.2883 4.1987 second is path planning based on adaptive field cooperation, which
mainly obtains collision-free paths of industrial robots. The third is to
| AVE | 4.5004 | 6.1086 4.4355 | 4.5498 |     |     |     |     |
| --- | ------ | ------------- | ------ | --- | --- | --- | --- |
control the operation of industrial robots based on collision-free paths
(Table 4).
3.2 Experiment of industrial robot
Specifically, the experimental steps and the results of key steps are
as follows:
In order to verify the practicability of the algorithm, the path
planning simulation experiment is carried out combining the AFCS    1 The information of the experiment scene can be obtained by
algorithm with ROAKE industrial robot XB20 in the green sphere  the depth camera. And the 3D coordinates of obstacles in the
| Frontiers in Neurorobotics |     |     |     | 11  |     |     | frontiersin.org |
| -------------------------- | --- | --- | --- | --- | --- | --- | --------------- |

| Zhuang et al.  |     |     |     |     |     |     | 10.3389/fnbot.2025.1574044 |     |
| -------------- | --- | --- | --- | --- | --- | --- | -------------------------- | --- |
TABLE 3 The running time of the AFCS algorithm and tRRT algorithm.
|     | No  | 1 2 | 3 4 | 5   | 6   | 7   | 8   | 9 10 |
| --- | --- | --- | --- | --- | --- | --- | --- | ---- |
Time (s) 5.593 47.252 5.336 26.35 5.739 19.945 6.995 40.209.506 12.134 19.228
AFCS
|     | No  | 11 12 | 13 14 | 15  | 16  | 17  | 18  | 19 20 |
| --- | --- | ----- | ----- | --- | --- | --- | --- | ----- |
Time (s) 16.58 18.991 7.135 23.16 4.899 32.178 36.55 15.46 18.733 4.976
|     | No  | 1 2 | 3 4 | 5   | 6   | 7   | 8   | 9 10 |
| --- | --- | --- | --- | --- | --- | --- | --- | ---- |
Time (s) 3.804 3.9724 4.1898 4.753 4.298 4.2431 4.4561 4.5607 4.569 4.145
tRRT
|     | No  | 11 12 | 13 14 | 15  | 16  | 17  | 18  | 19 20 |
| --- | --- | ----- | ----- | --- | --- | --- | --- | ----- |
Time (s) 4.235 4.1579 4.3760 4.409 4.3345 4.4708 4.4809 4.3547 4.6079 5.1245
FIGURE 15
The path cost obtained of the AFCS algorithm and tRRT algorithm in two environments.
FIGURE 16
The number of path nodes of the AFCS algorithm and tRRT algorithm.
industrial  robot  coordinate  system  can  be  obtained  by    2 Based on the three-dimensional coordinates of obstacles, the
binocular camera calibration and hand-eye calibration. path planning is carried out by the adaptive field co-sampling
algorithm, and the Angle values of each joint of the industrial
The results of hand-eye calibration are shown in Equation 18: robot  are  obtained  based  on  the  inverse  kinematics
solution method.
  3 The time series of six joint angles of industrial robot is obtained
−0.0196 −0.0668 by  using  the  trajectory  planning  algorithm  (7th  degree
|     | 0.9976 |     | 16.7035 |     |     |     |     |     |
| --- | ------- | --- | -------- | --- | --- | --- | --- | --- |
|     |        |     |         |     |     |     |     |     |
0.0222 0.9990 0.0389 6.4285 polynomial trajectory planning algorithm).

X= (18)   4 Socket software is used to send the joint Angle value of the
|     | 0.0660 | −0.0403 0.9970 | 108.3157 |     |     |     |     |     |
| --- | ------- | -------------- | --------- | --- | --- | --- | --- | --- |
  industrial robot to ROKAE industrial robot XB20 to control
|                            |  0 | 0 0 | 1.0000   |     |                     |     |     |                 |
| -------------------------- | ---- | --- | ---------- | --- | ------------------- | --- | --- | --------------- |
|                            |      |     |            |     | the movement of it. |     |     |                 |
| Frontiers in Neurorobotics |      |     |            | 12  |                     |     |     | frontiersin.org |

Zhuang et al. 10.3389/fnbot.2025.1574044
FIGURE 17
The communication and logical relationship of the three hardware devices.
TABLE 4 The result of calibration of binocular camera.
Category of parameters Parameters
Intrinsic parameter of left camera
fx=21.853, fy=20.206, cx=22.023, cy
=612.37
Radial distortion parameters of the left k1= − 0.0108, k2= 0.3905, k3
camera = − 0.9366
Tangential distortion parameters of the p1= − 0.0257, p2= 0.0113
left camera
Intrinsic parameter of right camera
fx=21.234, fy=21.379, cx=21.666, cy
=609.82
Radial distortion parameters of the left k1= 0.0149, k2= 0.0693, k3= − 0.1083
camera
Tangential distortion parameters of the p1= − 0.0210, p2= 0.0135
right camera
External parameters of binocular R=[0.9906 0.0053 0.0121
camera −0.0055 0.9889 0.0002
−0.0131 -0.0103 0.9809]
T=[−191.2268–6.7915 -31.7064]
path planning algorithm can drive industrial robots to obtain a
FIGURE 18
The flow chart of the whole experiment. collision-free smooth path. The process of path planning of industrial
robots based on adaptive field cooperative sampling algorithm is
shown in Figure 21.
During the planning process, the Angle changes of the six joints
4 Conclusion
of ROKAE industrial robot XB20 are shown in Figure 19.
The joint Angle velocity curve of 6 joints of path planning based
on adaptive field cooperative sampling path planning algorithm is This article studies the path planning of industrial robots from the
shown in the Figure 20. unique perspective of improving the intelligence of path planning
It can be seen from the change curve of joint Angle value of algorithm. And an AFCS algorithm with strong environmental
industrial robots in Figure 20, the adaptive field cooperative sampling adaptability is proposed. It uses the traditional RRT algorithm as the
Frontiers in Neurorobotics 13 frontiersin.org

Zhuang et al. 10.3389/fnbot.2025.1574044
FIGURE 19
The angle changes of the six joints of ROKAE industrial robot XB20.
FIGURE 20
The joint Angle velocity curve of 6 joints of path planning based on adaptive field cooperative sampling path planning algorithm.
main framework to realize path planning. For the disadvantages of paper firstly improves the traditional APF algorithm, and then
redundant sampling and low efficiency of the traditional RRT introduces it to the node expansion stage of the traditional RRT
algorithm, this paper designs an optimal sampling strategy and algorithm. This approach provides a theoretical basis for the
improves the node expansion stage. The optimal sampling strategy not generation of new nodes and improves the overall efficiency of the
only solves the problem of redundant sampling, but also improves the algorithm. More importantly, compared with other algorithms, the
quality of sampling points. The optimal sampling strategy is also efficiency and practicability of the AFCS algorithm are improved, and
beneficial to improve the path optimality. In the expansion stage, this the adaptability to the environment is significantly improved in the
Frontiers in Neurorobotics 14 frontiersin.org

Zhuang et al. 10.3389/fnbot.2025.1574044
FIGURE 21
The process of path planning of industrial robots based on adaptive field cooperative sampling algorithm.
Conflict of interest
path planning of industrial robots. This approach not only provides
ideas for the intelligent development of path planning algorithms, but
also provides guarantees for the intelligent development of MF, XL were employed by Datang Shandong Power Generation
industrial robots. Co., Ltd.
The remaining authors declare that the research was conducted in
the absence of any commercial or financial relationships that could
Data availability statement
be construed as a potential conflict of interest.
Correction note
The raw data supporting the conclusions of this article will
be made available by the authors, without undue reservation.
A correction has been made to this article. Details can be found
at: 10.3389/fnbot.2025.1754834.
Author contributions
Generative AI statement
YZ: Investigation, Writing – original draft. SL: Formal analysis,
Methodology, Writing – review & editing. QL: Investigation, Writing – The authors declare that no Gen AI was used in the creation of
original draft. DC: Conceptualization, Project administration, this manuscript.
Writing – review & editing. WB: Formal analysis, Supervision, Any alternative text (alt text) provided alongside figures in this
Writing – review & editing. XL: Investigation, Resources, Writing – article has been generated by Frontiers with the support of artificial
review & editing. MF: Supervision, Visualization, Writing – original intelligence and reasonable efforts have been made to ensure accuracy,
draft. LW: Investigation, Resources, Writing – original draft. including review by the authors wherever possible. If you identify any
issues, please contact us.
Funding Publisher’s note
The author(s) declare that financial support was received for the All claims expressed in this article are solely those of the authors
research and/or publication of this article. This work is supported and do not necessarily represent those of their affiliated organizations,
by the Taishan Scholar Project of Shandong Province or those of the publisher, the editors and the reviewers. Any product
(tshw201502042), National Natural Science Foundation of China that may be evaluated in this article, or claim that may be made by its
(NO.52206096). manufacturer, is not guaranteed or endorsed by the publisher.
Frontiers in Neurorobotics 15 frontiersin.org

Zhuang et al. 10.3389/fnbot.2025.1574044
References
Ahmadi, B., Zakeri, E., and Xie, W.-F. (2022). Optimal image-based task-sequence/ Karman, S., and Frazzoli, E. (2011). Sampling-based algorithms for optimal motion
path planning and robust hybrid vision/force control of industrial robots. IEEE Access planning. Int. J. Robotics Res. 30, 846–894. doi: 10.1177/0278364911406761
10, 26347–26368. doi: 10.1109/ACCESS.2022.3156919
Kavraki, L. E., Svestka, P., Latombe, J.-C., and Overmars, M. H. (1994). Probabilistic
Biao, H., and Cao, Z. (2021). Meng Chu Zhou, an efficient RRT-based framework for roadmaps for path planning in high-dimensional configuration spaces. IEEE Trans.
planning short and smooth wheeled robot motion under inodynamic constraints. IEEE Robot. Autom. 12, 566–580.
Trans. Ind. Electron. 68, 3292–3302. doi: 10.1109/TIE.2020.2978701 Khan, A. T. (2020). Shuai Li, Seifedine Kadry, Yunyoung Nam, control framework for
Chi, W., Ding, Z., Wang, J., Chen, G., and Sun, L. (2022). A generalized Voronoi trajectory planning of soft manipulator using optimized RRT algorithm. IEEE Access 8,
diagram-based efficient heuristic path planning method for RRTs in Mobile robots. IEEE 171730–171743. doi: 10.1109/ACCESS.2020.3024630
Trans. Ind. Electron. 69, 4926–4937. doi: 10.1109/TIE.2021.3078390 Khatib, O. (1986). Real-time obstacle avoidance for manipulators and Mobile robots.
Fan, X., Guo, Y., Liu, H., Wei, B., and Lyu, W. (2020). Improved artificial potential field Int. J. Robotics Res. 5, 90–98. doi: 10.1177/027836498600500106
method applied for AUV path planning. Math. Probl. Eng. 2020, 1–21. Larsena, L. (2017). Jonghwa Kimb *, Michael Kupkea, Alfons Schuster, automatic path
Gammell, Jonathan D., Srinivasa, Siddhartha S., and Barfoot, Timothy D., Informed planning of industrial robots comparing sampling-based and computational intelligence
RRT*: optimal sampling-based path planning focused via direct sampling of an methods. Procedia Manufacturing 11, 241–248. doi: 10.1016/j.promfg.2017.07.237
admissible ellipsoidal heuristic. The IEEE RSJ international conference on intelligent Lavalle, S., Rapidly-exploring random trees: A new tool forpath planning. [J]
robots and sys-tems (IROS) (2014). Computer Science. (1998).
Ganesan, Sivasankar, and Natarajan, Senthil Kumar, Asokan Thondiyath, G-RRT*: Liu, B., Feng, W., Li, T., Chunhe, H., and Zhang, J. (2020). A variable-step RRT* path
Goal-oriented sampling-based RRT* path planning algorithm for mobile robot planning algorithm for quadrotors in below-canopy. IEEE Access 8, 62980–62989. doi:
navigation with improved convergence rate. Advances in robotics -5th international 10.1109/ACCESS.2020.2983177
conference of the robotics society (2021) 1–6.
Lixing Liu, X., Wang, X. Y., Liu, H., Li, J., and Wang, P. (2023). Path planning
Guan-Zheng, T. A. N., and Huan, H. E. (2007). Aaron SLOMAN, Ant Colony System techniques for mobile robots: review and prospect. Expert Syst. Appl. 227:120254. doi:
Algorithm for Real-Time Globally Optimal Path Planning of Mobile Robots. Acta 10.1016/j.eswa.2023.120254
Automatica Sinica 33, 279–285. Rostami, S. M. H. (2019). Arun Kumar Sangaiah, Xiaozhu Liu, Jin Wang, obstacle
Guo, T., Wang, J., Wang, Z., Chen, W., Chen, G., and Zhang, S. (2022). Research on avoidance of mobile robots using modified artificial potential field algorithm. EURASIP
path planning of Mobile robot with a novel improved artificial potential field algorithm. J. Wirel. Commun. Netw. 2019, 1687–1690. doi: 10.1186/s13638-019-1396-2
Math. Probl. Eng. 2022, 1–13. doi: 10.1155/2022/5692350 Urain, J., Li, A., Liu, P., D’Eramo, C., and Peters, J. (2023). Composable energy policies
Hart, P. E., Nilsson, N. J., and Raphael, B. (1972). A formal basis for the heuristic for reactive motion generation and reinforcement learning. Int. J. Robo. Res., 42, 1–14.
determination of minimum cost paths. IEEE Trans. Syst. Sci. Cybernetics 4, 28–29. doi: 10.1177/02783649231179499
Hartenberg, R., Danavit, J., and Freudenstein, F. (1964). Kinematic synthesis of Wang, J., Meng, M. Q. H., and Khatib, O. (2020). EB-RRT: optimal motion planning for
linkages. New York: McGraw-Hill. Mobile robots. IEEE Trans. Autom. Sci. Eng. 17, 2063–2073. doi: 10.1109/TASE.2020.2987397
Hong, B., Lin, Z., Chen, X., Hou, J., Lv, S., and Gao, Z. (2022). Development and Wang, Ping, Xie, Xudong, Zheng, Hongxing, and Yu, Xiaoqiang, Rapid obstacle
application of key technologies for guide dog robot: a systematic literature review. Robot. avoidance planning of patrol under multi-obstacle constraint [D], proceedings of 2021
Auton. Syst. 154:104104. doi: 10.1016/j.robot.2022.104104 international conference on autonomous unmanned systems (ICAUS 2021) (2022), pp.
3380–3387
Jia, L., Huang, Y., Chen, T., Guo, Y., Yin, Y., and Chen, J. (2022). MDA + RRT: a general
Wang, D., Zheng, S., Ren, Y., and Danjie, D. (2022). Path planning based on the
approach for resolving the problem of angle constraint for hyper-redundant manipulator.
improved RRT* algorithm for the mining truck. Comp. Materials Continua 71,
Expert Syst. Appl. 193:116379. doi: 10.1016/j.eswa.2021.116379
3571–3587. doi: 10.32604/cmc.2022.022183
Junxiang, X., and Wang, J. (2021). Effective motion planning of manipulator based on Wei, K., and Ren, B. (2018). A method on dynamic path planning for robotic
SDPS-RRTConnect. Robotica 40, 1855–1867. doi: 10.1017/S0263574721001417 manipulator autonomous obstacle avoidance based on an improved RRT algorithm.
Kabutan, R., and Nishida, T. (2018). Motion planning by T-RRT with potential Sensors (Basel) 18, 1424–1438. doi: 10.3390/s18020571
function for vertical articulated robots. Electric. Eng. Japan 204, 34–43. doi: Yin, Q., Xiong, Z., and Zhang, G. (2018). Path planning for EOD robots. Int. J. Wireless
10.1002/eej.23103 and Mobile Computing 15, 223–229. doi: 10.1504/IJWMC.2018.096005
Kang, G. (2019). Yong bum Kim, young Hun Lee, Hyun Seok Oh, won Suk You, Yuan, Q., Yi, J., Sun, R., and Bai, H. (2021). Path planning of a mechanical arm based
Hyouk Ryeol Choi, sampling-based motion planning of manipulator with goal-oriented on an improved artificial potential field and a rapid expansion random tree hybrid
sampling. Intell. Serv. Robot. 12, 265–273. doi: 10.1007/s11370-019-00281-y algorithm. Algorithms 14, 813–819. doi: 10.3390/a14110321
Kang, Gitae, Kim, Yong Bum, You, Won Suk, Lee, Young Hun, Oh, Hyun Seok, Moon, Zhang, Z., Defeng, W., Jiadong, G., and Li, F. (2019). A path-planning strategy for
Hyungpil, et al., Sampling-based path planning with goal oriented sampling. 2016 IEEE unmanned surface vehicles based on an adaptive hybrid dynamic Stepsize and target
international conference on advanced intelligent mechatronics (AIM) (2016) 1285. attractive force-RRT algorithm. J Mar Sci Eng 7, 1–14. doi: 10.3390/jmse7050132
Frontiers in Neurorobotics 16 frontiersin.org