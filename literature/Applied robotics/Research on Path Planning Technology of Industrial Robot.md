Research on Path Planning Technology of Industrial Robot
Xinning Zuo
Secondary School affiliated to Beijing Institute of Education, Beijing, China
Keywords: Path Planning, Industrial Robots, A Algorithm*.
Abstract: With the rapid development of robotics, path planning has become one of the hot topics in the field of robotics
Path planning is a key area in robotics, focusing on determining the optimal trajectory for robots from the
beginning to the destination while satisfying kinematic and dynamic constraints. In industrial scenarios, path
planning is crucial for optimizing production efficiency while maintaining operational safety, especially in
complex environments (such as multiple obstacles and dynamic scenes), path planning is the basis to ensure
the stable operation of industrial robots. In industrial applications, path planning is essential for optimizing
production efficiency and ensuring operational safety, particularly in complex environments with multiple
obstacles and dynamic changes. Recent advances have introduced reinforcement learning-based methods,
which utilize deep learning to achieve flexible path optimization in dynamic or uncertain environments.
Among various emerging approaches, path planning based on reinforcement learning has become one of the
key research directions. Despite progress, challenges remain. Complex environments, multi-robot
cooperation, and diverse task requirements demand solutions that balance real-time performance, accuracy,
and energy efficiency. To address these challenges, this paper examines traditional path planning approaches,
focusing on algorithms such as dynamic Dijkstra, A star, and genetic algorithms.
1 INTRODUCTION development of robots and artificial intelligence has
also been rapid. They are not only widely used in the
industrial field but also largely used in other fields,
The integration of intelligent robotics and Artificial
such as medical and health care, education, home
intelligence has transformed various aspects of
economics, field exploration, military, rescue, and so
modern society, from manufacturing to healthcare.
on (Jiang et al., 2021). The key technologies of robots
As AI develops rapidly and becomes more integrated
include perception, map construction, positioning,
with robots, the intelligent robot industry has
path planning, and control systems. As one of the core
achieved unprecedented development. Higher
technologies, path planning has attracted the attention
intelligence requirements also spread to industrial
of the majority of researchers. Route planning is
production and military fields in various countries
classified into two parts: the global route and the local
around the world. So, the rapid development of robots
route. Global path planning includes several well-
is the general trend. At present, Industry 4.0 has
established algorithms: A* for optimal pathfinding,
arrived, and the field of robotics needs to develop
RRT (Rapid-exploring Random Tree) for efficient
rapidly to meet the current social production and life.
space exploration, and D* for dynamic environments
Robots in various fields, such as medical robots,
(Huo et al., 2018). Along with the constant progress
industrial robots, and fighter aircraft, have attracted a
in the technique, the application area of the robot is
large number of scholars in the field of robotics. The
constantly enlarged. which is different from the
new concept of robots has been around since the last
previous limited to the field of science and
century when it was first mentioned in the works of
technology, but in a variety of fields, such as medical
Czech writer Karel Čapek (Murray et al., 2015). In
field, education field and service field. Robots are
the 1960s of the last century, the United States
becoming more and more comprehensive. In the late
developed the world's first practical value of
1970s, the United States Unimation company
industrial robots, and General Motors Company has a
developed PUMA, which is widely used in industry,
practical application. In the past 20 years, with the
which also shows that industrial robots are maturing,
obvious progress of science and technology, the
727
Zuo,X.
ResearchonPathPlanningTechnologyofIndustrialRobot.
DOI:10.5220/0014371800004918
PaperpublishedunderCClicense(CCBY-NC-ND4.0)
InProceedingsofthe3rdInternationalConferenceonComputerScienceandMechatronics(ICCSM2025),pages727-731
ISBN:978-989-758-786-3;ISSN:3051-7982
ProceedingsCopyright©2026bySCITEPRESS–ScienceandTechnologyPublications,Lda.

ICCSM2025-TheInternationalConferenceonComputerScienceandMechatronics
and the robot has been widely used in industrial  in the environment and make specified actions for
production (Jiang et al., 2021).  concrete piles and steel pipes (Chen et al., 2021). The
In  the  1980s,  artificial  intelligence  gained  first  humanoid  robot  came  out  in  2000.  It  was
momentum. The first annual meeting of the American  independently  developed  by  China's  National
Association of Artificial Intelligence took place at the  University of Defense Technology. It has a human
beginning of that era, and a few years later saw the  shape and can also simulate basic human movements.
birth of AARON, an artistic robot (Tian, 2020 &  In 2015, ClearPath launched TurtleBot2, as shown in
Bogue, 2016). AARON can create abstract paintings,  Figure 1. The TurtleBot2 is a high-performance, A
and his work has been exhibited at the Tate Gallery  cheap  Willow  Garage  development  platform  for
and the San Francisco Museum of Modern Art. At the  robotics. It is the second generation product in the
same time, with the wide application of industrial  TurtleBot  family.  Its  application  in  the  field  of
robots in the body welding line, its working efficiency  scientific research, simple and convenient operation,
has  been  paid  more  and  more  attention.  The  strong technical expansion, and iterative update of
optimization  of  industrial  robot  path  planning  products provide a platform for scientific research.
| significantly  |     | impacts  | operational  |     | efficiency  | and  |     |     |     |     |     |     |     |
| -------------- | --- | -------- | ------------ | --- | ----------- | ---- | --- | --- | --- | --- | --- | --- | --- |
production throughput. The term "industrial robot"
| was  | proposed  | by  | the  | American  | Metal  | Market  |     |     |     |     |     |     |     |
| ---- | --------- | --- | ---- | --------- | ------ | ------- | --- | --- | --- | --- | --- | --- | --- |
Newspaper in 1960 and defined by the American
| Robotics Association  |     |     | as:  | "a  programmable  |     | multi- |     |     |     |     |     |     |     |
| --------------------- | --- | --- | ---- | ----------------- | --- | ------ | --- | --- | --- | --- | --- | --- | --- |
functional operator used to carry out the handling of
| mechanical  |     | parts  | or  workpieces,  |     | or  | a  special  |     |     |     |     |     |     |     |
| ----------- | --- | ------ | ---------------- | --- | --- | ----------- | --- | --- | --- | --- | --- | --- | --- |
mechanical device that can complete various jobs by
| changing  |     | the  program"  |     | (Liu  et  | al.,  | 2017).  This  |     |     |     |     |     |     |     |
| --------- | --- | -------------- | --- | --------- | ----- | ------------- | --- | --- | --- | --- | --- | --- | --- |
definition has now been adopted by the International

| Organization  |     | for  | Standardization.  |     | Based  | on  the  |     |     |     |     |     |     |     |
| ------------- | --- | ---- | ----------------- | --- | ------ | -------- | --- | --- | --- | --- | --- | --- | --- |
current research status of industrial robots, this paper  Figure 1: Clear Path's Turtle Bot2 (Xu et al., 2022).
| examines  |     | advanced  | path-planning  |     | methodologies  |     |     |     |     |     |     |     |     |
| --------- | --- | --------- | -------------- | --- | -------------- | --- | --- | --- | --- | --- | --- | --- | --- |
2.2  The Application of Industrial
with a focus on improving computational efficiency
| and trajectory optimization.   |     |     |     |     |     |     | Robots       |           |        |                  |            |                  |     |
| ------------------------------ | --- | --- | --- | --- | --- | --- | ------------ | --------- | ------ | ---------------- | ---------- | ---------------- | --- |
|                                |     |     |     |     |     |     | For  200     | years     | after  | the              | start  of  | the  Industrial  |     |
|                                |     |     |     |     |     |     | Revolution,  | machines  |        | were constantly  |            | updated          | to  |
2  CURRENT DEVELOPMENT
meet the needs of manufacturing. Especially after
AND RESEARCH STATUS OF
1950, manufacturing plants sprung up, and automatic
INDUSTRIAL ROBOTS  machine design and research procedures were also
prosperous, then three generations of robot products.
The first generation of robots belongs to the teaching
2.1  The Development of Industrial
|     | Robots  |     |     |     |     |     | and  reproducing  |     | type,  | which  | is  | an  important  |     |
| --- | ------- | --- | --- | --- | --- | --- | ----------------- | --- | ------ | ------ | --- | -------------- | --- |
breakthrough in robot manufacturing technology, but
its operation c entirely depends on manual control and
As the economy develops rapidly, the production
passive implementation. In the 1970s, driven by the
mode of manual operation has been far from meeting
|     |     |     |     |     |     |     | development  |     | of  | automation  | technology  |     | and  |
| --- | --- | --- | --- | --- | --- | --- | ------------ | --- | --- | ----------- | ----------- | --- | ---- |
the needs of society, so industrial robot technology
|          |     |          |        |            |         |          | component  | technology,  |     | the  | second  | generation  | of  |
| -------- | --- | -------- | ------ | ---------- | ------- | -------- | ---------- | ------------ | --- | ---- | ------- | ----------- | --- |
| emerges  |     | as  The  | Times  | requires.  | George  | Charles  |            |              |     |      |         |             |     |
Devol applied for a robot patent in 1954. Based on  robots is manufactured. With the advent of the era of
|             |          |               |     |                  |                |          | artificial  | intelligence,  |     | artificial  | intelligence  |             | robots  |
| ----------- | -------- | ------------- | --- | ---------------- | -------------- | -------- | ----------- | -------------- | --- | ----------- | ------------- | ----------- | ------- |
| this        | patent,  | Joseph        |     | F.  Engelberger  |                | founded  |             |                |     |             |               |             |         |
|             |          |               |     |                  |                |          | have  also  | opened         |     | the         | fourth        | scientific  | and     |
| Unimation,  |          | the  world's  |     | first  robot     | manufacturing  |          |             |                |     |             |               |             |         |
technological revolution. Intelligent robots are now
| company,    |     | in  1956  | and    | produced   | a   | robot  called  |         |          |     |          |           |            |     |
| ----------- | --- | --------- | ------ | ---------- | --- | -------------- | ------- | -------- | --- | -------- | --------- | ---------- | --- |
|             |     |           |        |            |     |                | widely  | applied  | in  | various  | sectors,  | including  |     |
| "Unimate."  |     | In        | 1959,  | Engelberg  |     | and  Devol     |         |          |     |          |           |            |     |
manufacturing, agriculture, mining, and healthcare.
collaborated in the United States to manufacture the
These robots show an increasing tendency to replace
world's first genuine industrial robot prototype. In
human labor. Jingwu Intelligent, the world's first
1968, the Stanford Research Institute of the United
three-dimensional space cleaning robot, applied to
| States  | showed  | the  | world's  | first  | intelligent  | robot,  |     |     |     |     |     |     |     |
| ------- | ------- | ---- | -------- | ------ | ------------ | ------- | --- | --- | --- | --- | --- | --- | --- |
complex health scenes, effectively reduces cleaning
Shakey. In 1973, Hitachi developed a robot equipped
with vision sensors that could detect moving objects  costs (Gasparetto et al., 2007). The application field
728

ResearchonPathPlanningTechnologyofIndustrialRobot
of industrial robots is continuously expanding, and choice depends on the minimum amount of labor, the
the work that can be completed is becoming more and shortest route, or the minimum amount of
more complex. Its main application industries are computation time. Essentially, it is a question of
automobile and motorcycle manufacturing, metal finding an optimum or viable solution in a number of
cold processing, metal casting and forging, smelting constrained conditions. The quality of route planning
gold, stone, plastic products, etc. Industrial robots has a direct influence on the real time performance
have been able to replace manual assembly, welding, and the outcome of the work. Since 70's, the study on
casting, spraying, grinding, polishing, and other robotic route planning has been carried out in all
complex work. kinds of robotic R&D countries, with notable
achievements. Based on the data character of the
2.3 Research Methods of Industrial research environment, route planning is classified
Robots into two parts: Discrete Domain Scope Route
Programming and Successive Domain Scope Route
Global path planning methods with common methods Planning (Ji et al., 2015). According to the time
are viewable, raster method, topology method, and evolution, the route planning method can be classified
other methods. In terms of the visible view method, into the conventional one and the modem one. Based
the robot is regarded as a point, and the visible view on the degree of knowledge about the work region,
is constructed by origin, the goal point of the robot, this paper classifies the route planning of the robot as
and the top of each obstacle, and the points are a part of region informatization (GIS) (Jiang et al.,
connected so that there are no obstacles and 2021). The local route planning is a kind of real time
boundaries between two points. The paths in the view route planning, which uses the local environment data
are collisionless, so the robot can avoid obstacles, gathered by the sensors in the process of executing
Then, the search for the optimum route is transformed the mission. But because of the dependence of local
into one that can be seen from the beginning to the environment characteristics, this method can only be
finish. The visible view method can be used for a local optimal, not a global optimal one, or even an
finding the shortest path; however, any change in impossible one. Based on the knowledge of global
starting or ending points requires reconstructing the environmental information, built a local
visible view. The second method is the artificial environmental map model, and then get the best or
potential field method, which simulates the best route on a region map. Lastly, lead a mobile
electrostatic field phenomenon in physics. Based on robot to a safe destination.
the repulsion force field in the vicinity of the barrier,
the robot can get rid of the obstruction and the 3.2 Dijkstra Algorithm
attraction force field surrounding the object to lure the
robot. The advantage of EMR is that it is easy to Dijkstra algorithm is mainly applied to search the
construct and less computation (Lee, 2014). The grid shortest path in the directed graph. Dijkstra algorithm
is used to divide the space in which the robot operates, starts by finding the shortest path between two points,
so that the location and dimensions of the barriers are and next derives a version, which starts with a vertex
not changed in the working space. Mesh size and finds other nodes with the shortest path to it, and
influences the route planning greatly. Although the finally gets the shortest path. The algorithm
size of the grain size is more accurate, it will take up iteratively checks the points in the node set and
a lot of memory and improve the performance of the expands by adding unvisited nearby points (Xu et al.,
algorithm. 2022). The algorithm selects the node with the
minimum distance among the unvisited nodes each
time, and uses it to update the distance of other nodes.
3 PATH PLANNING The algorithm uses the starting position of the object
as the starting point to inquiry the nodes in the map.
CALCULATION METHOD
The algorithm iteratively checks the points in the
node set, and then adds the nearby points that have
3.1 Path Programming not been checked to the node set. These nodes form a
complete path from the starting point to the goal
Route planning is an important technique in robot point. This algorithm guarantees finding an optimal
R&D. The route planning technique of a robot refers path when all edges have non-negative cost values.
to the selection of optimum or sub-optimal route
between the beginning and the destination. The
729

ICCSM2025-TheInternationalConferenceonComputerScienceandMechatronics
3.3  A*Algorithm  model the natural evolutionary course of biology (Liu
et al., 2017). It has better global optimization ability
A* algorithm is a heuristic search algorithm that  and parallel characteristics and has achieved good
combines cost evaluation and distance estimation in  planning results in single-robot and multi-robot path
artificial intelligence applications. This algorithm is  planning. As an international search algorithm, GA
|     |     |     |     |     | requires  | reasonable  |     | data  | encoding  | for  |
| --- | --- | --- | --- | --- | --------- | ----------- | --- | ----- | --------- | ---- |
the most popular in path planning search because of
its strong elasticity and super adaptability to different  implementation. This encoding process transforms
road conditions. The most successful feature of A*  the original data into chromosomes based on specific
situations. So as to form the initial chromosome and
algorithm is that it can realize the combination of the
above two algorithms, by analyzing the current node  then  the  chromosome  through  further  screening,
through the cost of the starting point and the node and  crossover, mutation, and other operations to produce
the heuristic evaluation of the node to the goal point.  better  than  the  previous  generation  of  new
The classical intelligent A-star algorithm is based on  chromosomes and finally get the optimal solution for
| heuristic algorithm, which includes the advantages of  |              |             |     |          | the population.  |     |     |     |     |     |
| ------------------------------------------------------ | ------------ | ----------- | --- | -------- | ---------------- | --- | --- | --- | --- | --- |
| Dijkstra  algorithm                                    | and  greedy  | algorithm.  |     | It  can  |                  |     |     |     |     |     |
reduce the search time and calculation while ensuring
optimality, and is widely used in robot path search,  4  CONCLUSION
| game  AI,  network  | routing  | and  other  | fields.  | The  |     |     |     |     |     |     |
| ------------------- | -------- | ----------- | -------- | ---- | --- | --- | --- | --- | --- | --- |
heuristic function is expressed as follows. Here is A  At present, the robot widely used in the industrial
simple example of using the A-star algorithm, as
industry is still mainly the traditional "demonstration"
| shown  in  Figure  | 2.  f(n)is  | mean  | the  evaluation  |     |     |     |     |     |     |     |
| ------------------ | ----------- | ----- | ---------------- | --- | --- | --- | --- | --- | --- | --- |
robot. This type of technology of industrial robot has
function of the initial point and the node and the target
been quite mature, but the traditional robot task model
point. And the g(n)is mean the true cost between an
of 3C and logistics industry has very big limitations.
initial point and a node in the state environment. H (n)
Robots that can do path design in a variety of complex
is mean the budget cost of the path from the current
environments are needed. The robot path planning
node n to the destination node.  problem is a big research hotspot in academic circles

all along, and involves some fields such as robot
ℱ(cid:4666)𝑛(cid:4667)(cid:3404)ℊ(cid:4666)𝑛(cid:4667)(cid:3397)Η(cid:4666)𝑛(cid:4667)                           (1)
kinematics, collision detection, path planning and

|     |     |     |     |     | velocity           | planning.  | This         | paper  | studies         | the  key     |
| --- | --- | --- | --- | --- | ------------------ | ---------- | ------------ | ------ | --------------- | ------------ |
|     |     |     |     |     | algorithms,        | such       | as  genetic  |        | algorithm       | A  specific  |
|     |     |     |     |     | algorithm dynamic  |            | algorithm    |        | dominant point  | and          |
|     |     |     |     |     | optimization       | problem,   |              | with   | the  main       | aim  of      |
promoting the working efficiency of robots as far as
|     |     |     |     |     | possible  | under       | the  premise  |                | of  industrial  | robots       |
| --- | --- | --- | --- | --- | --------- | ----------- | ------------- | -------------- | --------------- | ------------ |
|     |     |     |     |     | smoothly  | completing  |               | the            | expected        | task.  Path  |
|     |     |     |     |     | planning  | based       | on            | reinforcement  | learning        | has          |
emerged as a key research direction, leveraging deep
|     |     |     |     |     | learning's    | adaptability  |     | to  achieve  | robust  | path        |
| --- | --- | --- | --- | --- | ------------- | ------------- | --- | ------------ | ------- | ----------- |
|     |     |     |     |     | optimization  | in            | a   | dynamic      | and     | incomplete  |
information environment. The application of error

compensation technology has promoted the accuracy
Figure 2: Path Planning Diagram (Gasparetto et al., 2007).  of path planning distinctly and provided important
|     |     |     |     |     | support  | for  high-precision  |     | manufacturing.  |     | Virtual  |
| --- | --- | --- | --- | --- | -------- | -------------------- | --- | --------------- | --- | -------- |
3.4  Genetic Algorithm
simulation and digital twin technology optimize the
planning scheme through simulation test and virtual
A  genetic  algorithm  was  first  put  forward  by  model to reduce the potential problems before the
Professor John Holland of the University of Michigan
actual deployment. Traditional algorithms such as
in 1975. The algorithm initiates by evaluating the  Dijkstra, A * (a *), and genetic are used for systematic
quality of each individual in an initial solution set,  path planning analysis of industrial robots. Dijkstra is
which then guides subsequent genetic operations.
used to find the shortest path of directional graph. The
Through selection, crossing, and mutation, a new
A * algorithm, which combines cost evaluation and
group is produced, which is then repeated for a new  distance  estimation,  is  one  of  the  most  popular
| group.  A  genetic  | algorithm  | (GA)Is  | a   | kind  of  |     |     |     |     |     |     |
| ------------------- | ---------- | ------- | --- | --------- | --- | --- | --- | --- | --- | --- |
methods for path planning navigation, and is the
| probability  search  | method  which  | can  | be  | used  to  |     |     |     |     |     |     |
| -------------------- | -------------- | ---- | --- | --------- | --- | --- | --- | --- | --- | --- |
easiest to implement. Modern path planning methods
730

ResearchonPathPlanningTechnologyofIndustrialRobot
can  be  categorized  into  two  main  approaches:  Jiang W., Sun Y., Liang J, et al., Robot Iterative PD
learning-based methods like reinforcement learning,  Optimization  Control  Algorithm  and  Offline  VR
Verification, Forest Chemicals Review 2021, 1554-
| and  optimization-based  |     |     | methods  | like  | genetic  |     |
| ------------------------ | --- | --- | -------- | ----- | -------- | --- |
1570.
| algorithms.  | To  achieve  |     | superior  | performance  | in  |     |
| ------------ | ------------ | --- | --------- | ------------ | --- | --- |
Ke, Tian. Research on Path Planning Algorithm of Mobile
dynamic and complex environments. At the same
Robot in Complex Environment [D]. Beijing University
time, the application of virtual simulation and digital
of Chemical Technology, 2020.
twin technology provides an effective testing and  Lee, D. H., Robots in the shipbuilding industry, Robotics
optimization platform for path planning, enabling the
and Computer-Integrated Manufacturing 30, 442-450
algorithm to reduce potential problems before the
(2014).
actual  deployment.  In  the  future,  route  planning  Liu C. J., Han J. Q., An K., et al., Dynamic Path Planning
technology will focus more on convergence with  for  RoboCup  Robot  Based  on  Improved  RRT
artificial  intelligence.  Through  the  in-depth  Algorithm, Robot 33, 199-201 (2017).
Murray, Richard M., Zexiang Li, and S. Shankara Sastry, A
| reinforcement  | of  | learning  | techniques,  |     | the  self- |     |
| -------------- | --- | --------- | ------------ | --- | ---------- | --- |
Mathematical Introduction to Robotic Manipulation,
adaptability and learning ability of algorithms in the
Second Edition (Taylor and Francis, 2015).
incomplete information environment can be further
Shi-ming, Ji and Huang Xi-huan, Review of development
enhanced. At the same time, the multi-bot distributed
and application of industrial robot technology, Journal
path planning and the cooperative path planning of  of  Mechanical  &  Electrical  Engineering  32,  1-13
| human and computer will become the research hot  |     |     |     |     |     | (2015).  |
| ------------------------------------------------ | --- | --- | --- | --- | --- | -------- |
spots in the future, driving the application of robots in  Yuzhen, Xu, Indoor Mobile Robot Path Planning Method
Research [D]. Shenyang University of Technology,
| complex                                               | cooperative  | tasks.  | Building     |     | upon  these  |        |
| ----------------------------------------------------- | ------------ | ------- | ------------ | --- | ------------ | ------ |
| theoretical foundations, this paper investigates the  |              |         |              |     |              | 2022.  |
| integrated                                            | approach     | of      | kinematics,  |     | trajectory   |        |
planning, control algorithms and virtual methods.
| Despite       | the  achievements,  |         | several   |                  | technical  |     |
| ------------- | ------------------- | ------- | --------- | ---------------- | ---------- | --- |
| challenges    | emerged             | during  | the       | implementation,  |            |     |
| particularly  | in  dynamic         |         | obstacle  | avoidance        | and        |     |
algorithm optimization. Although there is a relatively
| good  real-time  |            | obstacle   | evacuation  |          | effect  for  |     |
| ---------------- | ---------- | ---------- | ----------- | -------- | ------------ | --- |
| relatively       | low-speed  | obstacles  |             | in  the  | dynamic      |     |
obstacle evacuation of robots, potential risks exist due
to failure to respond in time to high-speed obstacles
or several high-speed obstacles. Therefore, the future
| dynamic       | identification       | efficiency  |        | will           | be  raised.  |     |
| ------------- | -------------------- | ----------- | ------ | -------------- | ------------ | --- |
| While         | genetic  algorithms  |             | offer  | robust         | global       |     |
| optimization  | capabilities,        |             | they   | face           | challenges   |     |
| including     | slow  convergence,   |             | high   | computational  |              |     |
costs, and sensitivity to initial population selection in
calculating the optimal path.
REFERENCES
Bogue R., The role of robots in the battlefields of the future,
Industrial Robot 43, 354-359 (2016).
Chen J., Zhao Y., Xu X., Improved RRT-Connect Based
Path Planning Algorithm for Mobile Robots, IEEE
Access 9, 145988-145999 (2021).
Gasparetto, A. and V. Zanotto, A new method for smooth
trajectory planning of robot manipulators, Mechanism
and Machine Theory 42, 455-471 (2007).
Huo F. C., Chi J., Huang Z. J., et al., Review of Path
Planning Algorithms for Mobile Robots, Journal of
Jilin University: Information Science Edition 36, 639-
647 (2018).
731