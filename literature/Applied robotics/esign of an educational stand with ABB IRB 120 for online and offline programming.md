ТЕХНІЧНІ НАУКИ ТА ТЕХНОЛОГІЇ

TECHNICAL SCIENCES AND TECHNOLOGIES

DOI: https://doi.org/10.25140/2411-5363-2025-3(41)-63-69
UDC 621.8

№ 3(41), 2025

Peter Marcinko
Assistant Professor, Assistant Professor of the Department of production systems and robotics
Technical University of Košice, (Košice, Slovakia)
E-mail: peter.marcinko@tuke.sk. ORCID: https://orcid.org/0000-0003-2853-5755
ResearcherID: DFK-9265-2022. Scopus Author ID: 57200138054

DESIGN OF AN EDUCATIONAL STAND WITH ABB IRB 120
FOR ONLINE AND OFFLINE PROGRAMMING

The aim of this research is an educational robotic cell with an ABB IRB 120 that unifies the needs of university teaching and
industrial training into a single modular and robust solution. The concept is based on a reconfigurable frame, standardized inter-
faces, and a design that prioritizes ease of part fabrication and maintenance. By leveraging a digital twin in ABB RobotStudio,
offline programming, trajectory verification, and seamless transfer to online mode are enabled without interrupting operation.
The work includes a comparison of available market stands according to criteria such as robustness, safety, flexible tool exchange,
cost, and serviceability. We model multiple work configurations and end-effector variants while analyzing the relationship between
the maximum mass of the handled object and jaw pressure based on static equilibrium, friction coefficient, and grasp geometry.
Laboratory verification monitors cycle time, positioning accuracy, and repeatability, demonstrating the applicability of the solu-
tion for standardized exercises and operator training. The proposed cell lays the groundwork for further extensions, including
machine vision, advanced safety functions, and IoT integration for real-time data collection and evaluation.

Keywords: ABB IRB 120; programming; educational stand.
Fig.: 6. References: 8.

Relevance of the research. The relevance of this research lies in linking academic instruc-
tion with real industrial requirements through a standardized, reconfigurable cell built around
the ABB IRB 120 robot. The proposed solution enables universities and training centres to ef-
fectively develop the practical skills of students and operators in offline/online programming,
occupational safety, and maintenance, directly increasing graduates’ employability. Thanks to
its modular architecture and the use of a digital twin in RobotStudio, the cell is scalable, quickly
adaptable to new tasks, and suitable for continuous education in the context of Industry 4.0/5.0.
For small and medium-sized enterprises, the proposed cell represents a low-cost entry point
into  robotics  with  measurable  benefits,  thereby  supporting  regional  competitiveness  and  the
resilience of supply chains. From a research perspective, the platform provides a unified envi-
ronment for experiments with machine vision, IoT, and advanced safety functions, facilitating
the transfer of practical experience into real-world applications by students.

Problem statement. The problem is the absence of an affordable, standardized, and recon-
figurable educational cell that simultaneously meets the educational requirements of teaching
and  the  operational  demands  of  industry.  Most  available  stands  either  do  not  support  full-
fledged offline/online programming with a seamless transfer to practice or fail to meet the re-
quirement for simple maintenance that students can verify themselves. Documentation is also
limited regarding the design of flanges (end-effector interfaces), the modularity of peripherals,
and the manufacturability of parts for academic workshops. The aim, therefore, is to define the
requirements and to design and experimentally validate an educational cell with an ABB IRB
120 that eliminates these shortcomings and provides a model for teaching and operator training.
Analysis of recent research and publications. Current educational stands for industrial
robotics  are  primarily  positioned  as  “ready-to-teach”  platforms  with  an  emphasis  on  rapid
course ramp-up, safety, and compatibility with the manufacturer’s industrial ecosystem. The
Chinese MR101M (Jinan Minrry) solution represents a broad didactic set oriented toward the
fundamentals  of  robotics,  automation,  and  sensorics,  while  declaring  support  for  multiple
brands (KUKA, Stäubli, Denso, etc.). It’s the benefit lies in the included equipment (mechanics,
Programmable Logic Controller, computer control), yet it communicates less clearly the degree
of  hardware  reconfigurability  and  the  openness  of  interfaces  for  custom  end-of-arm  tooling
development Помилка! Джерело посилання не знайдено.. KUKA Ready2 educate targets

© P. Marcinko, 2025

63

ТЕХНІЧНІ НАУКИ ТА ТЕХНОЛОГІЇ

TECHNICAL SCIENCES AND TECHNOLOGIES

№ 3(41), 2025

a  unified,  mobile  starter  kit  with  the  KR  4 AGILUS  industrial  robot  and  KR  C5  controller,
which brings high technological relevance but also a natural lock-in to proprietary software and
peripherals. A clear strength is the seamless transition to industrial practice; a potential weak-
ness is limited modularity outside the KUKA ecosystem Помилка! Джерело посилання не
знайдено.. Hytech (product brand) Didactic Robocell with a FANUC robot focuses on practi-
cal, real-time material-handling applications and the robustness of industrial hardware. Across
the portfolio, there is a dominant orientation toward rapid deployment of vendor-grade compo-
nents; recent overviews, however, lack detailed documentation of open mechanical interfaces,
performance comparison metrics, and systematic support for a cross-vendor offline/online dig-
ital-twin workflow. These observations motivate research into an educational cell with ABB
IRB 120 that combines industrial relevance with a reconfigurable design and an open, transpar-
ent methodology Помилка! Джерело посилання не знайдено..

Uninvestigated  parts  of  a  common  problem. Alongside  the  stated  objectives,  several
parts of the problem remain insufficiently explored in practice, despite their direct impact on
teaching and industrial deployment. When transitioning from the RobotStudio offline environ-
ment to the real cell, systematic trajectory deviations regularly appear due to differences in tool
calibration, TCP definition, and fixture compliance, yet a unified methodology for their correc-
tion is lacking. After mechanical interventions such as end-effector flange replacement, recali-
bration, or preventive maintenance it is rarely verified whether key parameters have changed.
A quick, didactic before and after test that would reveal such shifts is missing. With the proper
design of the robotic cell, some of these parameters can be verified directly 3.

Research objective. The objective of the research is to design, build, and experimentally
validate a multifunctional educational stand with an ABB IRB 120 robot that is mobile, recon-
figurable, and usable in both university and industrial environments. Based on an analysis of
existing solutions, we define the concept and structure of the stand to enable rapid exchange of
modules, flanges, and end effectors and to support packaging, sorting, and material-handling
tasks. The research goal includes selecting cost-effective components, performing 3D model-
ling and manufacturing of parts using FFF (Fused Filament Fabrication), as well as implemen-
ting a digital twin for offline programming and trajectory verification. It also includes preparing
robot programs for grasping, transferring, and placing parts. Through laboratory validation, we
aim to quantify cycle time, positioning accuracy, repeatability, and the time required for recon-
figuration between tasks, with the final output being a replicable reference design with docu-
mentation and a 3D visualization of operation.

The statement of basic materials. The proposed educational stand is built around the ABB
IRB 120 industrial robot, whose compact kinematics and payload capacity of several kilograms
make it suitable for manipulation, sorting, and the operation of simple fixtures in both labora-
tory and production environments. The stand’s main structure is made of aluminium profiles
with standardized T-slots, enabling rapid and repeatable repositioning of peripherals without
the need to modify load-bearing elements. The choice of aluminium provides a favourable stiff-
ness-weight ratio, easy machinability, and corrosion resistance, which are important in educa-
tional use for stand mobility, safe handling, and long-term serviceability. The overall dimen-
sions 700 × 1200 mm, Fig. 1.

64

ТЕХНІЧНІ НАУКИ ТА ТЕХНОЛОГІЇ

TECHNICAL SCIENCES AND TECHNOLOGIES

№ 3(41), 2025

Fig. 1. ABB IRB 120 with stand

The robot is connected to the arm and the mounting plate via a flange compliant with ISO
9409-1. The flange interface  and the end-effector adapter are custom made using PETG 3D
printing, which lowers costs, enables rapid production of spare parts, and allows very fast fab-
rication of prisms of other sizes required for different objects. Material PETG was chosen for
its good toughness, dimensional stability, and ease of printing without demanding a fully en-
closed chamber; in an environment with frequent student interaction, the easy repairability and
reproducibility of parts is also advantageous Помилка! Джерело посилання не знайдено..
To preserve TCP (Tool Centre Point) accuracy and long-term reliability, the flange’s contact
surfaces are designed with reinforced lead-in zones and threaded inserts at locations subject to
repeated bolting. All tolerance critical surfaces that enter the tool definition in RobotStudio are
measured after printing and, if necessary, fine-finished to minimize deviation between the digital
twin and the real tool kinematics. The end effector is a parallel two-jaw gripper, type MHZL2-
25D1, with interchangeable jaws. Its selection reflects the need for a universal grip for small to
medium-sized objects in educational tasks, with the jaws likewise manufactured by 3D printing.
The jaws are equipped with contact extensions made from 3D printed PETG and with replaceable
rubber inserts, enabling laboratory experiments to demonstrate the influence of material and sur-
face finish on safe holding force. The pressure in the pneumatic branch is adjustable via a local
regulator with a pressure gauge mounted directly on the stand, allowing students to repeatedly
verify the relationship between the set pressure and the actual gripping force, Fig. 2.

Fig. 2. Proposed end effector for easy manipulation task

65

ТЕХНІЧНІ НАУКИ ТА ТЕХНОЛОГІЇ

TECHNICAL SCIENCES AND TECHNOLOGIES

№ 3(41), 2025

The selected composition of materials and components pursues three main goals: proof of
industrial applicability, low cost, and high replicability. The ABB IRB 120 provides the work-
station  with  the same programming  interface and philosophy that students will encounter in
practice. Aluminum profiles supply a modular frame with long service life, while 3D printed
PETG flanges, prisms, and pallets enable rapid iteration of curricular exercises without addi-
tional expenses and with minimal fabrication time. The result is a fully functional educational
stand ready to perform various tasks in personnel training and in executing handling operations,
with industrial robot programs designed to be flexibly adapted to changes in station layout and
in the inclination of working planes. The combination of these basic materials forms the tech-
nical and methodological foundation on which standardized exercises can be built, parameters
of cycle time, accuracy, and repeatability can be compared, and operating costs and mainte-
nance demands can be kept at a level suitable for university laboratories. Fig. 3 representing
proposed educational stand 5.

Fig. 3. Educational stand with robot ABB IRB 120

Fig. 4. Preparation I/O signals for end effector

66

ТЕХНІЧНІ НАУКИ ТА ТЕХНОЛОГІЇ

TECHNICAL SCIENCES AND TECHNOLOGIES

№ 3(41), 2025

Offline programming in ABB RobotStudio makes it possible to create a digital twin of the
workstation, verify kinematics, and simulate trajectories without interrupting real operations.
Within the environment, tools (TCP  – Tool Centre Point), work frames (WorkObjects), and
precise models of objects, pallets, and prisms are defined to minimize the gap between simula-
tion and reality.  The simulator enables collision, reach, and singularity detection, as well as
cycle-time estimation at different speeds, accelerations, and motion types (joint, linear). RAPID
programs are generated and debugged offline, including gripping logic and intermediate steps
and then transferred to the controller with minimal correction. After basic calibration of the
(TCP – Tool Centre Point) and WorkObjects, it is usually sufficient to fine-tune only reference
points, which significantly shortens commissioning. Students can safely experiment with sta-
tion layout variants, tooling, and trajectories, evaluating each change through simulation. The
result is faster task iteration, higher safety, and validated procedures that are directly transfera-
ble to industrial practice 7.

When creating a program, you must start by defining points (targets) where the robot will
perform its tasks, including the necessary approach points. After the program points are created,
they should be merged into a single path. Timers and output instructions must also be added to
this  path  to  handle  part  manipulation.  The  final  part  of  programming  the  stand  is  to  set  the
motion type (Joint, Linear, Circular), configure zones, and specify speeds at the various points.

Fig. 5. Creating action and move instructions in RobotStudio

The outcome of our work was the development of a concept for an educational stand. It was
necessary to design the main structural parts of the stand, their assembly, and their fastening. The
result is a fully functional educational stand ready to perform various tasks in personnel training
and in executing different handling operations. We also prepared the required program for the
industrial  robot,  which  can  be  flexibly  modified  if  the  positions  of  stand  components  on  the
mounting plate or the inclination angle of the pallet plane change, using new WorkObjects.

From the robot arm, we routed compressed-air hoses to the pneumatic gripper, which will be
used to open and close the gripper. The pallet with four holes for placing parts is equipped with
a wing nut to allow simple and quick fastening of the pallet surface at the desired angle. All parts
of the stand are securely attached to the mounting plate and can be quickly reconfigured if needed.
An electro-pneumatic valve switches the direction of compressed air based on a signal from
the robot controller. Compressed air is supplied to the valve inlet and, depending on the con-
troller signals, is directed either to outlet 2 or outlet 4, enabling the pneumatic gripper to close

67

ТЕХНІЧНІ НАУКИ ТА ТЕХНОЛОГІЇ

TECHNICAL SCIENCES AND TECHNOLOGIES

№ 3(41), 2025

and  open.  We  connected  two  sensors  to  the  pneumatic  gripper,  which  transmit  to  the  robot
controller whether the gripper is in the closed or open state, and everything can be monitored
online using RobotStudio.

Fig. 6. Educational stand

Conclusions. The developed educational stand can be used to train university students and
employees of companies that utilize robotic solutions in their technological processes. Thanks to
its construction, it can also serve as a production device a readily adaptable, multipurpose stand
capable of performing packaging and product-sorting operations as an independent process.

In  this  work,  we  considered  existing  educational  and  training  stands,  analysed  their  ad-
vantages and disadvantages, and on that basis determined the concept and structure of our stand.
We also analysed the pros and cons of different types of industrial robots and selected the model
that best fits the given tasks. We chose components for our stand that would allow us to solve all
design tasks as efficiently and economically as possible. We worked on the stand’s design to
ensure it is mobile and easily configurable for various tasks. We created 3D models of the com-
ponents and units of the developed stand and generated programs for 3D printers that enabled us
to print the necessary parts. We performed the necessary calculations to assess the effectiveness
and reliability of the proposed assemblies of the stand. We created several variants of robot pro-
grams for grasping, transferring, and placing parts. A 3D visualization of the operation of the
training stand was developed and implemented. The mounting design of the stand’s modules on
the base plate enables quick and flexible changes to the tasks performed by the operator during
the training process. The developed modules are reliable and simple, easily reproducible by 3D
printing, and low-cost. The stand we developed has a multifunctional design that allows it to fulfil
various tasks in the professional training of students and company employees.

Statement on use of AI and AI-based technologies in the process of article writing.
The author(s) used [ChatGPT 5.0] – [translate] while writing this material. After using this
tool/service, the author(s) have reviewed and edited the content as necessary and take full re-
sponsibility for the content of the article.

68

ТЕХНІЧНІ НАУКИ ТА ТЕХНОЛОГІЇ

TECHNICAL SCIENCES AND TECHNOLOGIES

№ 3(41), 2025

This article was created thanks to the VEGA project support: 1/0215/23 Research and de-

velopment of robotic workplaces equipped with industrial and collaborative robots.

Acknowledgements

References

1.  Minrry  Education.  (2025).  Industrial  robot  educational  equipment:  Mechatronics  training

equipment. Retrieved June 19, 2025. https://minrry-education.com/products/industrial-robot.

2.  KUKA. (2025). KUKA ready2_educate [Online]. Retrieved June 19, 2025. https://www.kuka.com/

en-us/products/robotics-systems/kuka-ready2_use/kuka-ready2_educate.

3.  Hytech  Didactic.  (2025).  Handling  Robocell  with  PLC  &  IIOT [Online].  Retrieved  June  20,

2025. https://hytechdidactic.com/manufacturer-of-handling-robocell-plc-iiot-pune.

4.  Marcinko, P., Semjon, J., & Jánoš, R. (2021). Vytváranie robotických buniek pomocou offline

prostredia ABB RobotStudio I (1st ed.). Košice: Technická univerzita v Košiciach. [CD-ROM].

5.  Marcinko, P. (2022). The use of SmartComponents in the design of complex robotic workplaces.

Technical Sciences and Technologies, 29(3), 52-58. Chernihiv National University of Technology.

6.  Marcinko, P., Jánoš, R., & Varga, J. (2024). Vytváranie robotických buniek pomocou off-line pros-
tredia ABB RobotStudio II (1. vyd.). Košice: Technická univerzita v Košiciach. ISBN 978-80-553-4732-5.
7.  The use of SmartComponents in the design of complex robotic workplaces: Marcinko, P., Kovaľuk,
D., 2022. In: Technical Sciences and Technologies. - Černihiv (Ukrajina) Chernihiv National University of
Technology Roč. 29, č. 3 (2022), s. 52-58. ISSN 2411-5363.

8.   Mamontov, A. Návrh edukačného standu s robotom ABB IRB 120. Diplmová práca. Košice. 2025.

Отримано 19.09.2025

УДК 621.8

Петер Марцінко
доцент, доцент кафедри виробничих систем та робототехніки
Кошицький технічний університет (Кошице, Словаччина)
E-mail: peter.marcinko@tuke.sk. ORCID: https://orcid.org/0000-0003-2853-5755
ResearcherID: DFK-9265-2022. Scopus Author ID: 57200138054

ПРОЄКТУВАННЯ НАВЧАЛЬНОГО СТЕНДА З ABB IRB 120
ДЛЯ ОНЛАЙН ТА ОФЛАЙН ПРОГРАМУВАННЯ

Метою цього дослідження є створення навчальної робототехнічної камери з ABB IRB 120, яка об'єднує потреби
університетського навчання та промислового навчання в єдине модульне та надійне рішення. В основі концепції ле-
жить реконфігурована рама, стандартизовані інтерфейси та конструкція, що надає пріоритет простоті вигото-
влення деталей та технічного обслуговування. Завдяки використанню цифрового двійника в ABB RobotStudio, офлайн-
програмування, перевірка  траєкторії  та  безперебійний  перехід  в онлайн-режим  можливі  без  переривання роботи.
Робота включає порівняння доступних ринкових стендів за такими критеріями, як міцність, безпека, гнучкість за-
міни  інструментів, вартість  та  зручність  обслуговування. Ми  моделюємо різні  конфігурації роботи  та  варіанти
кінцевих виконавчих механізмів, аналізуючи взаємозв'язок між максимальною масою оброблюваного об'єкта та тис-
ком захвату на основі статичної рівноваги, коефіцієнта тертя та геометрії захвату. Лабораторна перевірка кон-
тролює час циклу, точність позиціонування та повторюваність, демонструючи придатність рішення для стандар-
тизованих  вправ  та  навчання  операторів.  Запропонована  камера  створює  основу  для  подальших  розширень,
включаючи машинний зір, вдосконалені функції безпеки та інтеграцію IoT для збору та оцінки даних у реальному часі.

Ключові слова: ABB IRB 120; програмування; навчальний стенд.
Рис.: 6. Бібл.: 8.

Marcinko, P. (2025). Design of an educational stand with ABB IRB 120 for online and offline programming. Technical sciences and technol-
ogies, (3(41)), 63-69. DOI: https://doi.org/10.25140/2411-5363-2025-3(41)-63-69.

69

