Article
Reinforcement Learning of a Six-DOF Industrial Manipulator for
Pick-and-Place Application Using Efficient Control in
Warehouse Management
AhmedIqdymat andGrigoreStamatescu*
DepartmentofAutomationandIndustrialInformatics,NationalUniversityofScienceandTechnology
PolitehnicaofBucharest,SplaiulIndependentei313,060042Bucharest,Romania;ahmed.iqdymat@stud.acs.upb.ro
* Correspondence:grigore.stamatescu@upb.ro;Tel.:+40-723425323
Abstract: This study investigates the integration of reinforcement learning (RL) with
optimalcontroltoenhanceprecisionandenergyefficiencyinindustrialroboticmanipu-
lation. Anovelframeworkisproposed,combiningDeepDeterministicPolicyGradient
(DDPG)withaLinearQuadraticRegulator(LQR)controller, specificallyappliedtothe
ABBIRB120,asix-degree-of-freedom(6-DOF)industrialmanipulator,forpick-and-place
tasksinwarehouseautomation. Themethodologyemploysanactor–criticRLarchitecture
witha27-dimensionalstateinputanda6-dimensionaljointactionoutput. TheRLagent
wastrainedusingMATLAB’sReinforcementLearningToolboxandintegratedwithABB’s
RobotStudiosimulationenvironmentviaTCP/IPcommunication. LQRcontrollerswere
incorporatedtooptimizejoint-spacetrajectorytracking,minimizingenergyconsumption
whileensuringprecisecontrol. Thenoveltyofthisresearchliesinitssynergisticcombina-
tionofRLandLQRcontrol,addressingenergyefficiencyandprecisionsimultaneously—an
areathathasseenlimitedexplorationinindustrialrobotics. Experimentalvalidationacross
100diversescenariosconfirmedtheframework’seffectiveness,achievingameanposition-
ingaccuracyof2.14mm(a28%improvementovertraditionalmethods),a92.5%success
rateinpick-and-placetasks,anda22.7%reductioninenergyconsumption. Thesystem
demonstratedstableconvergenceafter458episodesandmaintainedameanjointangle
AcademicEditors:MaurizioFaccio, errorof4.30◦,validatingitsrobustnessandefficiency.Thesefindingshighlightthepotential
JoãoReisandYuvalCohen of RL for broader industrial applications. The demonstrated accuracy and success rate
Received:28October2024 suggestitsapplicabilitytocomplextaskssuchaselectroniccomponentassembly,multi-step
Revised:4December2024 manufacturing,delicatematerialhandling,precisioncoordination,andqualityinspection
Accepted:15December2024
taskslikeautomatedvisualinspection,surfacedefectdetection,anddimensionalverifica-
Published:8January2025
tion. Successfulimplementationinsuchcontextsrequiresaddressingchallengesincluding
Citation: Iqdymat,A.;Stamatescu,
taskcomplexity,computationalefficiency,andadaptabilitytoprocessvariability,alongside
G.ReinforcementLearningofa
ensuringsafety, reliability, andseamlesssystemintegration. Thisresearchbuildsupon
Six-DOFIndustrialManipulatorfor
existingadvancementsinwarehouseautomation,inversekinematics,andenergy-efficient
Pick-and-PlaceApplicationUsing
EfficientControlinWarehouse robotics,contributingtothedevelopmentofadaptiveandsustainablecontrolstrategiesfor
Management.Sustainability2025,17, industrialmanipulatorsinautomatedenvironments.
432. https://doi.org/10.3390/
su17020432 Keywords: reinforcementlearning;energyefficientcontrol;industrialmanipulator;pick-
Copyright:©2025bytheauthors. and-place;automation;sustainability
LicenseeMDPI,Basel,Switzerland.
Thisarticleisanopenaccessarticle
distributedunderthetermsand
conditionsoftheCreativeCommons 1. Introduction
Attribution(CCBY)license
Whileexistingresearchhasmadesignificantprogressinroboticcontrolforwarehouse
(https://creativecommons.org/
licenses/by/4.0/). automation,thereremainsacriticalgapindevelopingenergy-efficientcontrolstrategies
Sustainability2025,17,432 https://doi.org/10.3390/su17020432

Sustainability2025,17,432 2of25
thatmaintainhighprecision. Currentapproachestypicallyoptimizeeitheraccuracyor
energyconsumptionseparately,leadingtosub-optimalsolutions. Additionally,traditional
control methods often struggle to adapt to varying warehouse conditions and lack the
flexibilityneededformodernautomationrequirements.
Inrecentyears,theoptimizationofroboticsystemshasbecomeincreasinglyimpor-
tantforenhancingefficiencyandproductivityinmodernwarehousemanagement. Rein-
forcementlearning(RL)hasemergedasapromisingtechniqueforcontrollingindustrial
manipulatorsandautomatingcomplextaskslikepick-and-placeoperations. Thisresearch
explorestheapplicationofRLtoasix-degree-of-freedom(DOF)industrialmanipulatorfor
warehousepick-and-placetasks.
Industrialmanipulatorsfaceseveralchallengesinreal-worldwarehouseenvironments,
includingtrajectoryplanning,inversekinematics,andoperatingwithinphysicalconstraints.
Traditional control methods often struggle with the complexity and dynamic nature of
thesetasks. RLoffersthepotentialtolearnoptimalpoliciesthroughinteractionwiththe
environment,potentiallyovercominglimitationsofconventionalapproaches.
ThisstudyaimstodevelopanefficientcontrolsystemforaSix-DOFindustrialma-
nipulatorusingRLtechniques. Thegoalistoenableprecise,adaptivemanipulationfor
pick-and-placeapplicationswhileoptimizingfactorslikeenergyefficiencyandtaskcom-
pletiontime. BycombiningRLwithindustrialrobotics,wehopetoadvancewarehouse
automationcapabilitiesandcontributetomoreflexible,responsivelogisticsoperations.
Theresearchhasimplicationsnotonlyforroboticsandautomation,butalsoforimproving
overallwarehousemanagementandsupplychainefficiency. AsIndustry4.0evolvesto-
wardsIndustry5.0,thefocusshiftsfrompureautomationtosustainableandhuman-centric
manufacturing. OurworkalignswithIndustry5.0principlesby:
• Optimizingenergyefficiencyforenvironmentalsustainability;
• Enhancingsystemadaptabilityforhuman–robotcollaboration;
• Implementingintelligentcontrolforresponsiveautomation;
• Reducingoperationalcostswhilemaintainingprecision.
2. LiteratureReview
Themodernindustriallandscapeischaracterizedbyrapidlyevolvingdemandsand
dynamicenvironments[1,2], necessitatingadvancedtechnologiestoenhanceefficiency
andprocesshandling[3,4]. Industrialrobotics,particularlywiththeintegrationofartificial
intelligenceandmachinelearning,offerssignificantadvantagesinprecision,consistency,
andadaptability[5–8].
Reinforcementlearninghasemergedasapowerfulapproachforenhancingtheperfor-
manceofindustrialmanipulators,leadingtoadvancementsincontrolprecision,operational
efficiency,andenergyoptimization[9]. DeepDeterministicPolicyGradient(DDPG)and
DynamicMovementPrimitives(DMPs)havebeenparticularlyeffectiveinachievingre-
markableaccuracyandimprovinglearningefficiency[10,11]. Paralleldeepreinforcement
learningmethodshavedemonstratedsignificantenergysavingsandcomprehensiveframe-
workshavebeendesignedforrobustandscalableimplementations[12,13].
Variouslearningstrategies,suchasimitationlearning,multi-tasklearningframeworks,
anddynamictrajectorymodelingwithtime-dependentstateanalysis,haveenhancedthe
effectivenessofreinforcementlearninginindustrialrobotics[14,15]. Notablecontributions
include,analysisofthelabor-savingimpactofrobotics[16],developmentofrobustpick-
and-placesystems[17],andneuralnetworkmappingfortasktimeprediction[18].
Predictivemaintenancecapabilities[19],havebecomeincreasinglyimportantinin-
dustrialrobotics. DeepQ-Network(DQN),ProximalPolicyOptimization(PPO),andSoft

Sustainability2025,17,432 3of25
Actor-Critic(SAC)architectureshavedemonstratedeffectivenessinmanipulatorcontrol,
adaptability,andenergyefficiency[20,21].
Compensationmethodsforunmodeledaberrations,introducedby[22],havestrength-
enedthepracticalapplicationofreinforcementlearninginindustrialsettings. Trajectoryop-
timizationadvances,suchassmoothpoint-to-pointmovementusinghigh-orderpolynomial
curvesandthe“whip-lashing”method[5],havebeencrucialforefficientpick-and-place
operations. ResearchershaveexploredtheintegrationofMATLABandRobotStudio[23,24]
artificialneuralnetworksfortrajectoryoptimization,andreal-timetrajectorygeneration
methodsforenergyefficiency.
Energyefficiencyhasbecomeakeyfocusinwarehouseoperations,withsignificant
advancementsinenergy-awarecontrolstrategiesandparalleldeepreinforcementlearning
methods[25]. Simulationtechnologies,digitaltwinframeworks,andwirelessnetworking
solutionshavefurtherenhancedthefieldofroboticcontrol[26].
Safetyframeworkshaveevolvedtoaddressthechallengesofrobotsoperatingalong-
side humans, including adaptive admittance control [27], the Unrolling Safety Layer
(USL)[28],comprehensivesafereinforcementlearningframeworks[29],andintegrationof
safetyconsiderationsinmulti-robotenvironments[30].
Despiteremarkableprogress,challengesremaininbridgingthesimulation-to-reality
gap,optimizingcomputationalefficiency,enhancingrobustness,implementingpredictive
maintenancestrategies,integratingwirelessnetworkingsolutions,anddevelopingrobust
compensation methods. Future research directions include the integration of multiple
learning paradigms, development of efficient training methodologies, implementation
ofadvancedsafetyframeworks,andoptimizationofenergyconsumptioninhigh-speed
pick-and-placeoperations[31].
Insummary,theapplicationofreinforcementlearningto6-DOFindustrialmanipula-
torshasledtosignificantadvancementsinwarehouseautomation,encompassingadvanced
AI-drivensystems,predictivemaintenancecapabilities,andsophisticatedcompensation
methods. Theintegrationofwirelessnetworkingsolutionshasfurtherenhancedsystem
reliabilityandcoordination. Ongoingadvancementsinadaptivelearningstrategiesand
safetyframeworkspointtopromisingdirectionsforfutureresearch,suggestingacontinued
evolutiontowardpractical,reliable,andsustainableindustrialapplications.
3. ProblemDescription
3.1. AutomatedPick-and-PlaceOperationsinModernWarehouses
Intoday’srapidlyevolvinglogisticslandscape,theefficiencyofwarehousemanagement
hasbecomeacriticaldeterminantoforganizationalsuccess.Amongthevarioustechnological
advancementsrevolutionizingthisfield,theautomationofpick-and-placeoperationsstands
outasapivotalinnovation,particularlyinlarge-scalewarehouseenvironments.
Pick-and-placeautomationreferstothesophisticatedprocessofautonomouslyretriev-
ingobjectsfrominventorystoragelocationsandpreciselypositioningthematdesignated
destinations. Thisseeminglysimpletaskencompassesacomplexinterplayofrobotics,sen-
sortechnologies,andadvancedcontrolalgorithms. Thesignificanceofthisautomationlies
initsabilitytodramaticallyreducehumanintervention,minimizeerrors,andsubstantially
increaseoperationalefficiency.
Thecomplexityofpick-and-placeoperationsinmodernwarehousesstemsfromsev-
eralfactors:
1. VarietyofObjects: Warehousestypicallyhandleadiverserangeofitemswithvarying
shapes, sizes, weights, andmaterialproperties. Thisdiversitynecessitatesflexible
grippingmechanismsandadaptivecontrolstrategies.

Sustainability2025,17,432 4of25
2. DynamicEnvironment: Thewarehouselayoutandinventorypositionsareoftenin
flux,requiringsystemsthatcanadapttochangingspatialconfigurationsandobstacle
placements.
3. SpeedandPrecisionRequirements: High-throughputoperationsdemandrapidmove-
ments,yetprecisioninobjectplacementiscrucialtomaintaininventoryintegrityand
preventdamage.
4. IntegrationwithExistingSystems: Automatedpick-and-placesystemsmustseam-
lesslyinterfacewithwarehousemanagementsoftware,inventorytrackingsystems,
andotherautomatedprocesses.
5. SafetyConsiderations: Withhumanworkersoftenpresentinthesamespace,robust
safetyprotocolsandcollisionavoidancemechanismsareparamount.
Theintegrationofrobotics,particularlyarticulatedarmmanipulators,hasbeentrans-
formativeinaddressingthesechallenges. Theseroboticsystemsofferunparalleledflexibil-
ity,precision,andconsistencyinexecutingpick-and-placetasks. However,theireffective
deploymenthingesonsophisticatedcontrolalgorithmsandlearningmechanismsthatcan
navigatethecomplexitiesofthewarehouseenvironment.
3.2. MathematicalModelingofPick-and-PlaceOperations
Toeffectivelyanalyzeandoptimizepick-and-placeoperations,arigorousmethodical
framework is essential. This framework typically employs concepts from robotics and
definestheobjectivefunction,decisionvariables,andconstraintsgoverningthesystem.
Theprimaryobjectiveistominimizeaweightedcombinationofpositioningerror,
energyconsumption,andtaskcompletiontime. Formally,wehaveexpressedtheobjective
functionas:
minimize J = ω ·positioning_error+ω ·energy_consumption+ω ·completion_time
1 2 3
Here, ω , ω , and ω areuser-definedweightingfactorsthatallowustoprioritize
1 2 3
therelativeimportanceofeachtermbasedonthespecificrequirementsoftheapplication.
Thedecisionvariablesinthisoptimizationproblemarethejointanglesθ = [θ ,θ ,...,θ ]
1 2 6
andtheircorrespondingangularvelocitiesω =[ω , ω , ..., ω ]ateachtimestepofthe
1 2 6
pick-and-placetrajectory.
Collisionavoidance:therobot’smovementsmustnotresultincollisionswithobstacles
intheenvironment. Byformulatingthepick-and-placetaskasaconstrainedoptimization
problem, we have established a comprehensive mathematical framework to guide the
reinforcementlearningagent’spolicyoptimization. ThisformulationallowstheRLagent
tolearncontrolstrategiesthatbalancepositioningaccuracy, energyefficiency, andtask
completiontime,whilerespectingthephysicallimitationsoftheindustrialmanipulator.
3.3. KinematicChallengesinIndustrialManipulators
Robots: whilethemathematicalmodelprovidesaclearframework,implementing
it in real-world systems presents significant challenges, particularly in the domain of
robotkinematics.
Forwardkinematics,whichinvolvescalculatingtheend-effectorpositiongiventhe
jointanglesandlinklengths,isrelativelystraightforward. However,inversekinematics—
determiningthejointconfigurationsrequiredtoachieveadesiredend-effectorpose—is
considerablymorecomplex.

Sustainability2025,17,432 5of25
Keychallengesininversekinematicsforindustrialmanipulatorsinclude:
• Solution Multiplicity: For a given end-effector pose, multiple joint configurations
maybepossible,especiallyinrobotswithredundantdegreesoffreedom. Selecting
the optimal solution often requires additional criteria such as energy efficiency or
obstacleavoidance.
• Singularities: Certain joint configurations can lead to a loss of degrees of freedom
ormathematicalsingularitiesinthekinematicequations. Thesesituationscancause
instabilityincontrolsystemsandmustbecarefullymanaged.
• WorkspaceLimitations: Eachrobothasafinitereachableworkspace. Ensuringthat
allrequiredpick-and-placelocationsarewithinthisworkspaceiscrucialforsystem
designandlayoutplanning.
• EnvironmentalConstraints: Obstaclesinthewarehouseenvironmentfurtherrestrict
therobot’smotion.Incorporatingtheseconstraintsintotheinversekinematicssolution
ischallengingbutessentialforsafeoperation.
• ComputationalComplexity: Asthenumberofdegreesoffreedomincreases,sodoes
thecomputationalcomplexityofsolvinginversekinematics. Real-timeperformance
requirementsinwarehouseoperationsnecessitateefficientalgorithmicapproaches.
• Dynamics Considerations: While kinematics deals with geometry of motion, real-
worldperformanceisalsoaffectedbydynamics—theforcesandtorquesinvolvedin
movement.Integratingdynamicconsiderationswithkinematicsolutionsaddsanother
layerofcomplexity.
Addressing these challenges is crucial for developing robust and efficient control
systemsforindustrialmanipulatorsinpick-and-placeapplications. Advancedtechniques
suchasnumericaloptimization,machinelearningalgorithms,andmodelpredictivecontrol
areincreasinglybeingemployedtoovercomethesehurdlesandachievehigh-performance
automatedwarehouseoperations.
3.4. ReinforcementLearningforIndustrialManipulators
Reinforcementlearning(RL)hassignificantlyreducedtheproblemsandcomplexities
of inverse kinematics, path planning, trajectory optimization, and controls. RL is an
advancedtechniqueofmachinelearninginwhichanintelligentagent(anetwork)learnsby
interactionwiththeenvironment. ThefollowingarethekeyblocksoftheRLframework:
• Reward: Rewardisafunctioneddefinedastorewardtheagentifitgetsclosertothe
solutionandpenalizeitifgoesawayfromthesolution.
• Agent–Environment Interaction: This function defines how an agent will interact
with the environment i.e., an agent will generate action (i.e., joint angles) and the
environmentwillprovidethefeedbackforwhether,withtheseactions,theendeffector
isgettingclosertothedestinationormovingawayfromit.
• LearningProcess: Throughiterativeinteractionwiththeenvironment,theRLagent
learnstoimproveitsdecision-makingpolicy. Itexploresdifferentactions,observesthe
resultingrewards,andupdatesitspolicytomaximizelong-termrewards. Theagent
graduallylearnsamappingfromthecurrentstateofthesystemtosuitableactions
(jointangleadjustments)thatleadtosuccessfulinversekinematicssolutions.
4. ProposedLayoutofSimulation
4.1. Implementation
4.1.1. ProposedAlgorithm
Reinforcementlearningalgorithmsformafoundationalpillarofmachinelearning,
enablingintelligentagentstomakesequentialdecisionsindynamicenvironments. Attheir

Sustainability2025,17,432 6of25
Sustainability 2025, 17, x FOR PEER REVIEW 6 of 26
Sustainability 2025, 17, x FOR PEER REVIEW 6 of 26
core,thesealgorithmsaimtomaximizeacumulativerewardsignalthroughtrial-and-error
and-error learning. Reinforcement learning algorithms often utilize concepts like value
learning. Reinforcementlearningalgorithmsoftenutilizeconceptslikevaluefunctions,
and-error learning. Reinforcement learning algorithms often utilize concepts like value
functions, policy optimization, and exploration–exploitation trade-offs to strike a balance
policyoptimization,andexploration–exploitationtrade-offstostrikeabalancebetween
functions, policy optimization, and exploration–exploitation trade-offs to strike a balance
between exploring new actions and exploiting known knowledge. Figure 1 shows the lay-
exploringnewactionsandexploitingknownknowledge. Figure1showsthelayoutofthe
between exploring new actions and exploiting known knowledge. Figure 1 shows the lay-
out of the proposed algorithm used in our research.
proposedalgorithmusedinourresearch.
out of the proposed algorithm used in our research.
FFiigguurree 11.. PPrrooppoosseedd aallggoorritihthmm flfloowwchcahratr. t.
Figure 1. Proposed algorithm flowchart.
FFiigguurree 22 sshhoowwss tthhee ccoommpplelteet eSiSmimuluinlikn kmmodoedl eolf othfet hReLR eLnveinrovnirmoennmt.e nt.
Figure 2 shows the complete Simulink model of the RL environment.
FFiigguurree 22.. TToopp--lleevveell aarrcchhiitteecctuturere. .
Figure 2. Top-level architecture.

Sustainability 2025, 17, x FOR PEER REVIEW 7 of 26
Sustainability2025,17,432 7of25
4.1.2. IRB120 Pick-and-Place
4.1.2. IRB120Pick-and-Place
This block diagram shows the IRB120_Pick_and_Place block that takes actions as in-
ThisblockdiagramshowstheIRB120_Pick_and_Placeblockthattakesactionsasinput
put and output observations, reward, and completion status of simulation.
andoutputobservations,reward,andcompletionstatusofsimulation.
Figure 3 shows the details of the IRB120_Pick_and_Place block.
Figure3showsthedetailsoftheIRB120_Pick_and_Placeblock.
FFigiguurree 33. .IInntteerrnnaall aarrcchhiitteeccttuurree ooff IIRRBB112200 PPiicckk--aanndd-P-Plalaccee..
RewardBlock
Reward Block
Therewardblockcontainstherewardfunctionasdefinedbelow.
The reward block contains the reward function as defined below.
reward = e −5d
𝑟𝑒𝑤𝑎𝑟𝑑 =𝑒(cid:2879)(cid:2873)(cid:3031)
whered = ∆x2+∆y2+∆z2i.e.,thedistancebetweentheinitialandfinalposition.
where 𝑑 =Δ𝑥(cid:2870)+Δ𝑦(cid:2870)+Δ𝑧(cid:2870) i.e., the distance between the initial and final position.
ObservationBlock
Observation Block
Theobservationblockcomputestwenty-sevenobservationsi.e.,twelvevaluesforsine
andTcohsei noebosfesrivxajtoiionnt abnlgolceks ,ctowmelpvuetveasl utwesefnotrys-isneevaennd ocbosseinrevaotfisoinxsj oii.net., atnwgeullvaer vvealolucietsie fsor
sainned atnhrde ecovsailnuee soffo srixth jeoidnitf faernegnlcees,b tewtweleveen vcaolouredsi nfaotre ssionfet haendin ictoiaslinaen doffi sniaxl jpooinsitt iaonngsu. lar
velocities and three values for the difference between coordinates of the initial and final
ISDONEBlock
positions.
The ISDONE block checks the termination conditions for the simulation i.e., the
ISsiDmOuNlaEti oBnlotecrkm inateswhenanyofthefollowingconditionistrue:
• T ∆ hθe fIoSrDaOnyNjEoi bnltoacnkg cleheisck ≥ s0 t.h5;e termination conditions for the simulation i.e., the sim-
u • latioEnn tderemffiencatotersh washsetnar atendy mofo tvhine gfoalwloawyifnrgo mcotnhdeitdieosnt iinsa ttriuone: position.
 ΔA𝜃n f y o o r n a e ny o f jo th in e t s a ix ng jo l i e n i t s a n≥g0le.5s ; e xceedingitslimitsasdefinedinthesespecifications
h igh
E
li
n
g
d
h t
ef
t
f
h
e
e
ct
r
o
o
r
b
h
o
a
t’
s
s
s
s
ta
u
r
i
t
t
e
a
d
bi l
m
ity
ov
f
i
o
n
r
g
t
a
a
w
sk
a
s
y
r
f
e
r
q
o
u
m
ir i
t
n
h
g
e d
p
e
re
st
c
i
i
n
si
a
o
t
n
ion
in
p
c
o
o
s
n
it
fi
io
n
n
e
.
d spaces. The
relativelylowweightof25kgcoupledwithasubstantialarmreachof982mmprovidesan
Any one of the six joint angles exceeding its limits as defined in these specifications
excellentpayload-to-reachratio,enhancingitsversatilityinvariousindustrialsettings.
highlight the robot’s suitability for tasks requiring precision in confined spaces. The rela-
tiIvReBly12 l0owM awtheeigmhatt iocfa l2M5 kodg ecloupled with a substantial arm reach of 982 mm provides an
excellent payload-to-reach ratio, enhancing its versatility in various industrial settings.
TheABBIRB120representsasignificantadvancementincompactindustrialrobotics.
This versatile manipulator is designed to meet the demands of modern manufacturing
IRB120 Mathematical Model
environments where space efficiency and precision are paramount. As a six-degree-of-
freedTohme A(DBOBF I)RroBb 1o2t,0t hreepIrReBse1n2t0so af fseirgsnuinfipcaarnatl laedlevdaflnecxeimbielintyt iinn ctaosmkpexaecct uintidonu,smtriaakli nrogbiott-
icids.e Talhfios rvaerwsaidtieler amnagneipofualaptpolri ciast dioenssigfnroemd tdoe mliceaette tahses edmemblayntdosp orfe cmisoedmerante mriaalnhuafnadctluinrgin.g
enviroMnemchenantsi cwalhSepree csifipcaactei oenfsfi:cTiehnecIyR aBn1d2 0p’rsedceissiiognn aprreio priatirzaemsoaubnatl.a Ancse ab estiwx-edeengrceoem-o-f-
frpeaecdtnoemss (aDnOdFc)a rpoabboilti,t yth. eT aIbRlBe 112p0r eosfefnertss tuhnepkaeryalmleelecdha fnleicxaiblislpiteyc iifinc taatsiokn esxoefcuthtieoAn,B mBaIRkBing
it1 2id0eraolb footr. Taa wbleid2e prraensgene tosft haepIpRliBc1a2ti0oanxsi sfrcoomns tdrealiinctast.e assembly to precise material han-
dling.

Sustainability2025,17,432
8of25
The extensive range of motion, particularly in the wrist and turn axes, allows for
complexmanipulationsandenhancestherobot’sdexterityinconfinedspaces.
Table1.KeymechanicalspecificationsoftheABBIRB120robot.
|     | S.No. |     |     | Parameter |     | Value |     |
| --- | ----- | --- | --- | --------- | --- | ----- | --- |
|     | 1     |     |     | Payload   |     |       | 3Kg |
180mm×180mm
|     | 2   |     |             | Base        |     |                |     |
| --- | --- | --- | ----------- | ----------- | --- | -------------- | --- |
|     | 3   |     |             | RatedPower  |     | 3KVA           |     |
|     | 4   |     |             | ArmReach    |     | 982mm          |     |
|     | 5   |     |             | Weight      |     | 25Kg           |     |
|     | 6   |     | RobotHeight |             |     | 700mm          |     |
|     | 7   |     |             | Application |     | Pick-and-Place |     |
Table2.IRB120axisconstraints.
|     | Axis |     | TypeofMotion   |             |     | RangeofMovement |         |
| --- | ---- | --- | -------------- | ----------- | --- | --------------- | ------- |
|     | 1    |     | RotationMotion |             |     | −165◦           | to+165◦ |
|     | 2    |     |                | ArmMotion   |     | −110◦           | to+110◦ |
|     |      |     |                |             |     | −110◦           | to+70◦  |
|     | 3    |     |                | ArmMotion   |     |                 |         |
|     | 4    |     |                | WristMotion |     | −160◦           | to+160◦ |
|     | 5    |     |                | BendMotion  |     | −120◦           | to+120◦ |
|     |      |     |                |             |     | −400◦           | to+400◦ |
|     | 6    |     |                | TurnMotion  |     |                 |         |
MathematicalModelingApproach:
ToaccuratelymodeltheIRB120,weemploytheDenavit–Hartenberg(DH)[32]param-
etermethod. Thisapproach,widelyrecognizedinrobotics,providesastandardizedwayto
describethekinematicrelationshipsbetweenadjacentlinksinanarticulatedsystem. The
DHmethod’spowerliesinitsabilitytorepresentcomplexspatialrelationshipsusingjust
fourparametersperlink.
DHParametersforIRB120: ThespecificDHparametersfortheIRB120arepresented
inTable3.
Table3.IRB120DHparameters.
| i   |     | a   |     | α   | d   |     | θ   |
| --- | --- | --- | --- | --- | --- | --- | --- |
|     |     | i−1 |     | i−1 |     | i   | i   |
| 1   |     | 0   |     | 0   | 290 |     | θ   |
1
| 2   |     | 0   |     | −90◦ | 0   |     | θ −90◦ |
| --- | --- | --- | --- | ---- | --- | --- | ------ |
2
| 3   |     | 270 |     | 0   | 0   |     | θ   |
| --- | --- | --- | --- | --- | --- | --- | --- |
3
−90◦
| 4   |     | 70  |     |     | 302 |     | θ   |
| --- | --- | --- | --- | --- | --- | --- | --- |
4
| 5   |     | 0   |     | 90◦ | 0   |     | θ   |
| --- | --- | --- | --- | --- | --- | --- | --- |
5
−90◦
| 6   |     | 0   |     |     | 72  |     | θ 6 |
| --- | --- | --- | --- | --- | --- | --- | --- |
Theseparametersareessentialforderivingtheforwardkinematicsequations. Each
row in the table represents a link in the robot’s kinematic chain, with the parameters
describingthespatialrelationshipbetweenconsecutivejointaxes.
SignificanceofDHParameters:
• Thelengthofthecommonnormalbetweenthez-axesofjointsi−1andi.
a i−1 :

Sustainability2025,17,432 9of25
• α i−1 : Theangleaboutthecommonnormal,fromz i−1 toz i .
• d: Theoffsetalongthepreviousztothecommonnormal.
i
• θ i : Theangleaboutz i fromx i−1 tox i .
KinematicEquations: UsingtheseDHparameters,wecanconstructhomogeneous
transformationmatricesforeachjoint. Theproductofthesematricesyieldstheoverall
transformationfromtherobot’sbasetoitsend-effector,enablingustocomputetheend-
effector’spositionandorientationforanygivensetofjointangles.
Theforwardkinematicsequationcanbeexpressedas:
T6 = A ∗ A ∗ A ∗ A ∗ A ∗ A
0 1 2 3 4 5 6
whereeachA isa4×4homogeneoustransformationmatrixderivedfromtheDHparameters.
i
Applications of the Model: This mathematical model serves as the foundation for
variouscrucialaspectsofrobotcontrolandplanning:
• InverseKinematics: determiningjointanglesforadesiredend-effectorposition.
• TrajectoryPlanning: generatingsmoothandefficientpathsfortherobottofollow.
• Workspace Analysis: understanding the robot’s reachable space and potential
configurations.
• DynamicsModeling:incorporatingmassandinertialpropertiesforforce-basedcontrol.
Inourreinforcementlearningframework,thismodelprovidestheessentialstructure
forstaterepresentationandactiondefinition.Itallowsthelearningalgorithmtounderstand
therobot’sconfigurationspaceandmakeinformeddecisionsaboutjointmovementsto
achievedesiredend-effectorpositions.
Byleveragingthisdetailedmathematicalmodel,wecandevelopsophisticatedcon-
trolalgorithmsthatfullyexploittheIRB120’scapabilities,enablingpreciseandefficient
executionofcomplextasksinindustrialsettings.
ProposedEfficientController
A Linear Quadratic Regulator (LQR) controller was designed to efficiently control
the joint motion of the 6-DOF IRB120 robot. LQR is an optimal control technique that
minimizesaquadraticcostfunctionweightingthestateerrorsandcontroleffort. Fora
linearsystem:
.
x = Ax+Bu
withstatevectorxandcontrolinputu,theLQRcontrollerfindstheoptimalcontrollaw:
u = −Kx
thatminimizesthecostfunction:
(cid:90) ∞(cid:16) (cid:17)
J = xTQx+uTRu dt
0
whereQandRarepositivedefiniteweightingmatricesonthestateerrorandcontroleffort,
respectively. TheoptimalgainmatrixKisgivenby:
K = R −1BTP
wherePisfoundbysolvingthecontinuous-timeAlgebraicRiccatiEquation(ARE):
ATP+PA−PBR −1BTP+Q =0

Sustainability2025,17,432 10of25
Forthe6-DOFrobot,thestatevectorxwaschosenas:
(cid:104) . . . . . . (cid:105)T
x = θ ,θ ,θ ,θ ,θ ,θ ,θ ,θ ,θ ,θ ,θ ,θ
1 1 2 2 3 3 4 4 5 5 6 6
• AngularPositionsθ:
i
• Calculatedusingencoderreadingsfromeachjoint;
Sustainability 2025, 17, x FOR PEER REVIEW 10 of 26
• Normalizedtotherange[−π,π]radians;
• Updatedateachcontrolcycle(5ms).
.
• AngularVelocit iesCθ ia:lculated using encoder readings from each joint;
• Computed usiNnogrdmiasclirzeetde -ttoim theed riafnfegree n[−tia𝜋t,i𝜋o]n :radians;
 Updated at each control cycle (5 ms).
 Angular Velocities θ 𝜃. (cid:3114) ̇ ( : t) = θ i (t)−θ i (t−∆t))
 Computed usi
i
ng discrete-tim
∆
e
t
differentiation:
𝜃(t)−𝜃(t−Δt))
• Filteredusingasecond-orderlow𝜃̇-(pt)as=s fil(cid:3036)terwit(cid:3036)hcutofff requencyof50Hz;
(cid:3114) Δt
• Units: radians/second.
 Filtered using a second-order low-pass filter with cutoff frequency of 50 Hz;
• JointConstrain ts:
Units: radians/second.
Thecontro lstJroaitnetg Cyoandshtreariendtst: othemechanicalconstraintsoftheIRB120robot,ensur-
ingsafeandreliablTehoep ceornattiroonl :strategy adhered to the mechanical constraints of the IRB120 robot, en-
PositionLsiumriintsg: sθaf_em anind ≤relθiab≤leθ op_emraatxio;n:
i i i
VelocityLimitPs:o|sθit|io≤n Lθim_mitsa: x𝜃.ᵢ_min ≤ 𝜃ᵢ ≤ 𝜃ᵢ_max;
i i
TheseconstraiVnetlsowciteyr eLibmasitesd:|𝜃oᵢ̇|n ≤th e𝜃̇ᵢr_o𝑚b𝑎o𝑥t.’ smechanicalspecificationsasdetailedin
Table1. These constraints were based on the robot’s mechanical specifications as detailed in
Whererep T re a s b e l n e t 1 s . theangularpositionandθ theangularvelocityofjointi(i=1,2,...,6).
i
Where represents the angular position and 𝜃 the angular velocity of joint
Thematrices AandBweredeterminedfromthelinearstate–spac(cid:3036)erepresentationofthe
𝑖 (𝑖 =1,2,…,6 ). The matrices 𝐴 and 𝐵 were determined from the linear state–space rep-
robot’sdynamics,andthecontrolinputuconsistedofvoltagecommandsappliedtothe
resentation of the robot’s dynamics, and the control input 𝑢 consisted of voltage com-
jointmotors.
mands applied to the joint motors.
ThediagonalelementsoftheQmatrixwereusedtoweighttheimportanceofeach
The diagonal elements of the 𝑄 matrix were used to weight the importance of each
statevariable. Sincetheobjectivewastotrackadesiredjointspacetrajectory,theposition
state variable. Since the objective was to track a desired joint space trajectory, the position
errorswereweightedmoreheavilythanthevelocityerrors. TheRmatrixwaschosenasa
errors were weighted more heavily than the velocity errors. The 𝑅 matrix was chosen as
diagonalmatrixtoweightthecostofeachjointmotorcommand.
a diagonal matrix to weight the cost of each joint motor command.
SolvingtheAREgiventhechosen A,B,Q,andRmatricesyieldedtheoptimalstate
Solving the ARE given the chosen 𝐴, 𝐵, 𝑄, and 𝑅 matrices yielded the optimal state
feedback gain
fe
m
ed
a
b
tr
a
i
c
x
k
K
g
.
ain
T
m
hi
a
s
tr
L
ix
Q R𝐾. g
T
a
h
i
i
n
s L
m
Q
a
R
t r
g
ix
ain
w
m
as
at
u
ri
s
x
e
w
d
a
t
s
o
u
c
s
o
ed
m
t
p
o
u
c
t
o
e
m
t
p
h
u
e
te
jo
t
i
h
n
e
t
jo
m
in
o
t
t o
m
r
otor com-
commandsufrmoamndths e𝑢j ofirnotms ttahtee jeorinrot rsstaxtea etreraocrhs c𝑥o natt reoalcchy ccolne.trol cycle.
Figure4showFsitghuereb l4o schkodwias gthrae mbloocfkt hdeiaLgQraRmc oofn tthreo lLleQrRa rccohnittreocltleurr ea.rchitecture.
Figure4.Proposedefficientcontroller.
Figure 4. Proposed efficient controller.
ThebenefitsoftheLQRcontrollerforthisapplicationwereasfollows:
The benefits of the LQR controller for this application were as follows:
 Stability: The LQR controller guaranteed closed-loop stability of the joint space dy-
namics, ensuring the robot would stably track the desired trajectory.
 Optimal control: By minimizing the quadratic cost on state error and control effort,
the LQR controller produced optimal joint motion that balanced tracking perfor-
mance and energy efficiency.

Sustainability2025,17,432 11of25
• Stability: TheLQRcontrollerguaranteedclosed-loopstabilityofthejointspacedy-
namics,ensuringtherobotwouldstablytrackthedesiredtrajectory.
• Optimalcontrol: Byminimizingthequadraticcostonstateerrorandcontroleffort,
Sustainability 2025, 17, x FOR PEER REVIEW 11 of 26
theLQRcontrollerproducedoptimaljointmotionthatbalancedtrackingperformance
andenergyefficiency.
• Robustness: The LQR controller provided good robustness to model uncertainty,
 Robustness: The LQR controller provided good robustness to model uncertainty,
maintainingstableperformanceevenwithsomemismatchbetweenthelinearmodel
maintaining stable performance even with some mismatch between the linear model
andactualrobotdynamics.
and actual robot dynamics.
• Efficientcomputation: TheLQRgainmatrixwascomputedofflinebysolvingtheARE.
 Efficient computation: The LQR gain matrix was computed offline by solving the
A T R h E e . r T e h a e l- t r i e m al e -ti c m on e t c r o o n l t t r h o e l n th o e n n l y on r l e y q u re i q re u d ire a d m a a m tri a x tr m ix u m lt u ip lt l i i p c l a ic ti a o ti n on u 𝑢 = = − −K𝐾x𝑥, , w hich
wchoiuchld cboueledf fibcei eefnfticlyieinmtlyp liemmpelenmteedn.ted.
• SStattaet erergeuglualtaiotnio: nT:hTish ciosnctornoltlreorl lies rcaispcaabplea obfl ereogfurleagtiunlga ttihneg sttahtee svtaartieabvlaer aiagbaliensatg aa insta
ddeseisrierde dseste ptopionitn. t.
• CClolsoesde-dlo-loopo pcocnotrnotlr:o Tl:hiTsh ciosnctoronltlreor lplerrovpirdoevsi da ecsloasecdlo-lsoeodp- lcooonptrcool nsttrraotlegstyr,a wtehgiyc,hw hich
mmeaenasn sthtehye cyocnotinntuinouuosluys alydjaudstju thste tchoentcroonl tirnopluitn bpaustedb aosne dthoe nsytshteemsy’ss tceumrr’esnctu srtareten. tstate.
TThhisi sadadapatpatbaibliitlyit ayllaolwlosw fosrf oimrpimropvreodv pederpfoerrmfoarnmcea nanced adnisdtudribsatuncreb arenjceectrioejne.c tion.
• SStattaet efefeedebdabcakc kcocnotrnotlr:o Tl:hiTs hciosnctoronltleror lmleornmitoornsi tcoormspcolemtep slteattee sotfa tteheo fsytshteemsy tshtaetm that
makes it more efficient in term of performance as compared to other controllers.
makesitmoreefficientintermofperformanceascomparedtoothercontrollers.
The reference trajectory 𝑑 was compared to the measured joint states 𝑥 to compute
Thereferencetrajectory(cid:3051)d wascomparedtothemeasuredjointstatesxtocompute
x
the error 𝑒. This was multiplied by the LQR gain matrix 𝐾 to produce the control 𝑢,
theerrore. ThiswasmultipliedbytheLQRgainmatrixKtoproducethecontrolu,which
which was then sent to the joint motor voltage commands.
wasthensenttothejointmotorvoltagecommands.
In summary, an LQR controller was designed to optimally and efficiently control the
Insummary,anLQRcontrollerwasdesignedtooptimallyandefficientlycontrolthe
joint space motion of the 6-DOF robot. The ARE was solved offline to determine the opti-
jointspacemotionofthe6-DOFrobot.TheAREwassolvedofflinetodeterminetheoptimal
mal gain matrix. This feedback control law minimized tracking error while constraining
gainmatrix. Thisfeedbackcontrollawminimizedtrackingerrorwhileconstrainingcontrol
control effort, providing stable and robust performance for executing the desired pick-
effort,providingstableandrobustperformanceforexecutingthedesiredpick-and-place
and-place trajectories.
trajectories.
4.1.3. RL Agent
4.1.3. RLAgent
PPoolilciycy PProrcoecsess s
TThhe epoploiclyic yprporcoescse sfsorf othret hReLR aLgeangt eins tshisoswhno winn FiinguFrieg 5u.r eIt 5ta.kIetst aakcteiosna cbtaiosend boans ed on
ccuurrrerennt tobosbesrevravtaiotino, nr,ewreawrda,r dan,adn sdomsoem perepvrioeuvsio euxspeerxipenerciee. nce.
Figure5.PolicyprocessfortheRLagent.
Figure 5. Policy process for the RL agent.
CriticandActorNetwork
Critic and Actor Network
Theactor–criticarchitectureisafundamentalframeworkinreinforcementlearning,
The actor–critic architecture is a fundamental framework in reinforcement learning,
enabling effective optimization of an agent’s behavior through the interplay between
enabling effective optimization of an agent’s behavior through the interplay between two
twokeycomponents: theactornetworkandthecriticnetwork. Figure6illustratesthe
key components: the actor network and the critic network. Figure 6 illustrates the actor–
actor–criticnetworkofanagentinreinforcementlearning.
critic network of an agent in reinforcement learning.

Sustainability 2025, 17, x FOR PEER REVIEW 12 of 26
Su stainability2025,17,432 12of25
FFiigguurree 66.. CCrritiitcic aanndd acatcotro nrentewtworokr fkorf othreth ReLR aLgeangte. nt.
TThhee ccrrititicic nneetwtworokr kisi srersepsopnosnibslieb lfeorf oersteimstaimtinagti nthge tvhaeluvea fluunecftuionnc,t iwohni,cwh hqiucahnqtiufiaesn tifies
tthhee eexxppeecctteedd ccuummuulaltaivtiev ererwewaradr dof oafctaicotnios.n Bsy. Bevyaeluvaatliunagt itnhge qthuealqituya olift aycotifoancst tiaoknesnt abkye nby
tthhee aaggeenntt, ,tthhee ccrirtiitci cpprorvoivdiedse essessesnetinatli afelefdebedacbka cthkatth gautidguesi dthees ltehaernleinagrn pinrogcepsrso, cheeslsp,inhge lping
tthhee aaggeennt tidiednetniftyif hyighhig-vha-lvuael aucetiaocntsi ofonrs spfoercisfipce sctaifitecs.s Ctaotnevs.erCseolyn,v tehres aecltyo,rt nheetwacotrokr rnepet-work
rreespernetsse nthtse tphoelipcyo lfiucyncftuionnc,t imona,pmpianpgp tihneg ctuhrerecnutr rsetantte sttoa tae ptoroabpabroilbitayb diliisttyridbiusttiroinb uotvioenr over
ppoossssiibbllee aaccttioionn. .ItIst spprirmimarayr yobojebcjteicvtei vise tios tmoamxiamxiizme itzhee tehxepeecxtpeedc cteudmcuulamtivuela rteivwearrdew bya rdby
sseelleeccttiinngg oopptitmimaal lacatcitoinosn ascarcorsos sdsivdeivrseer ssetastetas.t eTso.gTeothgeert,h tehre,steh neseetwnoertkwso frokrmsf ao rfmeedabfaecekd back
loop in which the critic evaluates the actor’s actions, enabling iterative refinement of the
loop in which the critic evaluates the actor’s actions, enabling iterative refinement of
policy.
thepolicy.
In this work, the reinforcement learning agent for the 6-DOF ABB IRB120 manipula-
Inthiswork,thereinforcementlearningagentforthe6-DOFABBIRB120manipulator
tor leverages this actor–critic architecture, featuring carefully designed neural networks
leveragesthisactor–criticarchitecture,featuringcarefullydesignedneuralnetworksfor
for both components. The actor network translates the robot’s state into joint angle com-
bothcomponents. Theactornetworktranslatestherobot’sstateintojointanglecommands,
mands, with an architecture that includes the following:
withanarchitecturethatincludesthefollowing:
 Input layer: 27 neurons representing the joint angles, joint velocities, and end-effector
• Inputlayer: 27neuronsrepresentingthejointangles,jointvelocities,andend-effector
position error.
positionerror.
 Hidden layers: Two fully connected layers with 400 and 300 neurons, respectively,
• Hiddenlayers:Twofullyconnectedlayerswith400and300neurons,respectively,utiliz-
utilizing ReLU activation functions and batch normalization for enhanced training
sintagbiRlietyL.U activationfunctionsandbatchnormalizationforenhancedtrainingstability.
• OOuuttppuut tlalayyeer:r :6 6nenueruornosn wsiwthi tthantahn ahctaivctaitvioanti,o enn,seunrisnugr ionugtpouuttsp ruetmsarienm waiitnhiwn itthhei n the
rroobboott’’ss jojoinint tlilmimitist.s .
TThhee ccrritiitcic nneetwtworokr,k t,atsaksekde dwiwthi tehsteimstiamtinagti nthge tahcetiaocnt-ivoanlu-vea fluunecftiuonnc (tQio-nva(lQu-ev),a elume-),em-
ppllooyyss aa dduuaall--bbrraanncchh ddeseisging,n i,nicnluclduidngin tgheth feolfloowlloinwgi:n g:
• SSttaattee bbrraanncchh: :AA 272-7n-enueruorno innpinupt ulatyleary, eidr,eindteicnatli ctaol thtoe tahcetoarc’st ostra’stes itnapteuitn, fpoullto,wfoeldlo bwye dby
aa 440000--nneeuurroonn hhididddene nlalyaeyre. r.
• AAccttiioonn bbrraanncchh: A: A 6-6n-enueruorno innpinupt ulatyleary ceorrcreosrpreosnpdoinngd itno gjotiontj oainngtlea ncogmlemcoamndms, afnold-s,fol-
lowed by its own 400-neuron hidden layer.
lowedbyitsown400-neuronhiddenlayer.
• Merged layer: A combined 300-neuron layer that processes information from
bothbranches.
• Outputlayer: AsingleneuronrepresentingtheestimatedQ-value.

Sustainability2025,17,432
13of25
Thenetworksaretrainedusingspecifichyperparameters,includinglearningratesof
1×10−5fortheactorand1×10−4forthecritic,abatchsizeof128,andatargetnetwork
updaterateof0.001. Thissetupensuresstableandefficientlearning,allowingtheagentto
refineitspolicybasedonthecritic’sevaluations.
Thisactor–criticframeworkequipstheagentwiththecapabilitytodevelopanopti-
mized,energy-efficientcontrolstrategyfortheIRB120manipulator. Byeffectivelylearning
fromtheenvironment,theagentachieveshighprecisionandperformanceinpick-and-place
tasks,demonstratingthepotentialofreinforcementlearninginindustrialautomation
4.2. NetworkTrainingandAnimation
4.2.1. NetworkTraining
TraininganRLagentinvolvesteachinganAIsystemtomakeoptimaldecisionsina
givenenvironment.RLdiffersfromothermachinelearningapproachesbecauseitfocuseson
learningthroughinteractionwiththeenvironmentratherthanrelyingsolelyonlabeleddata.
Thetrainingprocesstypicallyfollowsatrial-and-errorparadigm,wheretheRLagent
interactswiththeenvironment,receivesfeedbackintheformofrewardsorpenalties,and
learnstomaximizeitscumulativerewardovertime. Thisfeedbackloopenablestheagent
tolearnfromitsactionsandadjustitsbehavioraccordingly.
HyperParameters
Hyperparametersaredifferentparameterssetbytheuserorresearcherbeforetraining.
Theseparametersinfluencethetrainingprocess.
Thefollowingaresomemajorhyperparametersthatwereusedforthetrainingalgorithm.
•
Learningrate:Thisdeterminesthestepsizeofmodel’sparametersduringthetrainingpro-
cess.Thisparameterinfluencestheconvergencetimeandpatternofthetrainingalgorithm.
• Hiddenlayers: Theselayersdefinethecomplexityofthenetwork. Morehiddenlayers
arerequiredtocapturethenon-linearityofthemodelandenvironment.
• Batchsize: Thisdefinesthenumberofsamplesseenbythetrainingalgorithmbefore
updatingitsparameters. Largerbatchsizeresultsinsmoothgradientsbutismore
computationallyexpensive.
• Discountfactor: Thissetsthepreferenceforthetrainingalgorithmtoprioritizethe
optimizationofcurrentepisoderewardversusfuturecumulativereward.
Hyperparameterswerecarefullyselectedbecausetrainingprogressandconvergence
highlydependuponthesehyperparameters.
Table4showsthehyperparametersusedinthetrainingofthereinforcementlearn-
ingagent.
Table4.IRB120axisconstraints.
| Axis | TypeofMotion           | RangeofMovement |
| ---- | ---------------------- | --------------- |
| 1    | SampleTime             | 5ms             |
| 2    | TargetSmoothFactor     | 1×10−3          |
| 3    | ExperienceBufferLength | 1×106           |
| 4    | MiniBatchSize          | 128             |
| 5    | NumWarmStartSteps      | 100             |
| 6    | DiscountFactor         | 0.98            |
| 7    | Algorithm              | Adam            |
| 8    | LearnRate              | 1×10−5          |
| 9    | GradientThreshold      | 1               |

Sustainability 2025, 17, x FOR PEER REVIEW 14 of 26
6 Discount Factor 0.98
7 Algorithm Adam
Sustainability2025,17,432 8 Learn Rate 1×10(cid:2879)(cid:2873) 14of25
9 Gradient Threshold 1
OOppttimimizizaatitoionn AAlglogroitrhitmhm
RReeininfofrocrecmemenetn letalrenairnngi ndgepdeenpdes nudpsonu pa olont oaf loopttiomfiozpattiiomni azlagtoiorinthamlgs otori uthpmdastet othue pdate
pthareapmaertaemrs eotfe trhseo nfetuhreanl neuetrwalonrke tawndo rikmapnrodviem thper oavgeentth’se paogleicnyt.’ sSopmoleic oyf. tShoem meaojofr tohpe-major
toimptizimatiizoant iaolngoarligthomristh umsesdu fsoerd rfeoinrfroericnefmorecnetm leeanrtnlienagr nininclgudinec SlutodcehaSsttoicc hGarsatidcieGnrta Ddiee-ntDe-
sscceennt t(S(SGGDD),) ,RRMMSpSrporpo p(R(oRoot oMteMane aSnquSaqruea PreroPpraogpaatigoant)i,o And),aAGdraadG (rAadda(pAtidvae pGtirvaediGenrta dient
AAllggoorriitthhmm),) ,PPrrooxxiimmaall PPoolliiccyy OOppttiimmiizzaattiioonn (P(PPPOO)),,T rTursutsRt eRgeigoinonP oPlioclyicOy pOtipmtiimzaitzioatnio(nT RPO),
(DTReePpOD), eDteeerpm DineitsetricmPinoilsitciyc PGorlaicdyi eGnrtasd(iDenDtsP (GD)D,aPnGd),A andda mAd(Aamd a(AptdivapetMiveo mMeonmteEnstt Eims-ation).
tWimeautisoend). tWhee Ausdeadm thael gAodriatmhm alfgoorrittrhamin ifnorg torauirnninegt wouorr kn.eTtwhoertkr.a Tinhien gtrapirnoincegs psrfooclelossw sthe
follows the Adam algorithm flowchart shown in Figure 7.
AdamalgorithmflowchartshowninFigure7.
Figure7.FlowchartoftheAdaptiveMomentumEstimation(ADAM)algorithm.
Figure 7. Flowchart of the Adaptive Momentum Estimation (ADAM) algorithm.
Adamcombinestheadvantagesoftwootherpopularoptimizationtechniques: gradi-
Adam combines the advantages of two other popular optimization techniques: gra-
entdescentwithmomentumandRMSprop(RootMeanSquarePropagation). Itcombines
dient descent with momentum and RMSprop (Root Mean Square Propagation). It com-
theinformationfromthemomentumterm“m”andtheadaptivelearningrateterm“v”
bines the information from the momentum term “m” and the adaptive learning rate term
to update the model parameters. It computes the update for each parameter based on
theratioof“m”tothesquarerootof“v”(withbiascorrection)andscalesitbyahyper
parametercalledthelearningrate. Figure7showstheflowchartoftheAdamalgorithm.
WechosetheAdamoptimizerfortrainingourreinforcementlearningagent,given
itsadaptivelearningratecapabilities,whichcombinemomentumandRMSpropbenefits,
offeringstableconvergenceinnon-linear,high-dimensionalenvironmentstypicalofrein-
forcementlearning. Adam’sadaptivemechanism,adjustinglearningratesperparameter,

Sustainability2025,17,432 15of25
enhances stability over basic gradient descent, which is essential for our application’s
complexity. TheoptimizeralsointegrateswellwithourofflineLinearQuadraticRegulator
(LQR) controller. By computing the LQR gain matrix in advance, the system achieves
efficient,real-timecontrolviamatrixmultiplication,minimizingmemoryandcomputa-
tionaldemands.
Insummary,Adam’sbalanceofstability,adaptability,andefficiencysupportseffective
policylearningandstreamlinedreal-timecontrolfortheIRB120manipulatorinourpick-
and-placetask.
4.2.2. ComputingHardwareandSoftwareSpecifications
Thetrainingofthereinforcementlearning(RL)agentinvolvedsignificantcomputa-
tionalresources,includinghardware,software,andperformancemetrics. Keydetailsare
summarizedinTable5below,highlightingthesignificantcomputationaldemandsand
optimizationsmadeforefficiency.
Table5.ComputationalresourcesandperformancemetricsforRLtraining.
Category Specification
IntelXeonE5-2690v4(14cores,28threads),128GBDDR4RAM,NVIDIARTXA5000
Hardware
(24GB),2TBNVMeSSD
Ubuntu20.04LTS,MATLABR2023b(ReinforcementLearningToolbox),CUDA11.8,cuDNN
Software
8.6,ABBRobotStudio2023.1
Training
150h,13,000episodes,1×106replaysamples,128mini-batchsize,~41.6s/episode
Details
Gradientcheckpointingtoreducememoryusage,batchprocessingforefficientexperience
Optimizations replay,optimizedTCP/IPcommunication,andasynchronousdataloggingtominimize
I/Ooverhead
Performance Neuralnetworktraining(65%),physicssimulation(30%),communicationoverhead(3%),
Metrics dataloggingandcheckpointing(2%)
4.2.3. IntegratedSystem
We integrated MATLAB with ABB’s RobotStudio to develop and simulate robotic
applicationsfortheIRB120industrialmanipulator.
• Keycomponentsoftheintegratedsystem:
MATLAB:Usedforalgorithmdevelopment,dataanalysis,andvisualization;
ABB’sRobotStudio: SimulationandofflineprogrammingsoftwareforABBrobots;
IRB120robotmodel: 6-DOFindustrialmanipulatormodeledinRobotStudio.
• Integrationbenefits:
AllowsseamlessconnectionbetweenMATLABandRobotStudio;
Enablesdevelopmentofcomplexroboticcontrolalgorithmsandsimulations;
Combines MATLAB’s computational capabilities with RobotStudio’s robot-
specificfeatures.
• Communication:
MATLABandRobotStudiocommunicateusingaTCP/IPcommunicationframework.
Figure8showstheReinforcementLearningRobotStudiothatwasintegratedwithMATLAB
forsimulationpurposes.
• Workflow:
ReinforcementlearningagentdevelopedandtrainedinMATLAB;
(cid:35) LearnedagentintegratedwiththeIRB120modelinRobotStudio.
(cid:35)

Sustainability 2025, 17, x FOR PEER REVIEW 16 of 26
MATLAB and RobotStudio communicate using a TCP/IP communication frame-
Sustainability2025,17,432 work. Figure 8 shows the Reinforcement LearningRobot Studio that was integrated wit1h6 of25
MATLAB for simulation purposes.
FFiigguurree 88.. IInntteeggrraatteedd ssyysstetemm aracrhchitietcetcutruer. e.
 WThoirskfelonwab: led testing and visualization of the RL-based control in a realistic robot
simuloa tionReenivnifroorncemmeenntt. learning agent developed and trained in MATLAB;
• Ao pplicLaetaiornnesd: agent integrated with the IRB120 model in RobotStudio.
This enTabralejedc tteosrtyinogp atnimd ivziasutiaolniz;ation of the RL-based control in a realistic robot sim-
ulati(cid:35)on envi
P
ro
ic
n
k
m
-a
e
n
nt
d
.
-placeoperations;
 A(cid:35)pplicaEtionnesr:g y-efficientcontrolstrategies.
(cid:35) Toh is iTnrtaejegcrtaotreyd opstyimstiezmatioanl;l ows researchers to leverage the strengths of both
platfoor ms—PiMckA-aTnLdA-pBla’csea odpvearantcioednsc; omputationandRobotStudio’srobot-specificsimu-
o Energy-efficient control strategies.
lationcapabilities-todevelop,test,andvalidatereinforcementlearningalgorithmsfor
indusTthriias lirnotebgortaicteadp spyliscteamtio nalsl.ows researchers to leverage the strengths of both plat-
forms—MATLAB’s advanced computation and RobotStudio’s robot-specific simulation
5c.apRaebisliutiletss-to develop, test, and validate reinforcement learning algorithms for industrial
robotic applications.
The complete system with the IRB120 model, reward block, observation block, IS-
DONE block, and RL agent was trained using the Simulink/MATLAB Reinforcement
5. Results
LearningToolbox. Thesystemhassixactions,twenty-sevenobservations,andthreeout-
The complete system with the IRB120 model, reward block, observation block, IS-
puts. Duetothesemultipleinputsandmultipleoutputs,itstrainingwasahighlydifficult
DONE block, and RL agent was trained using the Simulink/MATLAB Reinforcement
exercise. Moreover,thetrainingprocesswascomputationallyexpensive. Ittookapproxi-
Learning Toolbox. The system has six actions, twenty-seven observations, and three out-
mately150htorunapproximately13,000episodes. Thesystemwastrainedwellwiththe
puts. Due to these multiple inputs and multiple outputs, its training was a highly difficult
desiredaccuracy.
exercise. Moreover, the training process was computationally expensive. It took approxi-
Sustainability 2025, 17, x FOR PEER REVIEWF igures9and10illustratetherewardsforindividualepisodes(forafe1w7 oef p2i6s odes)
mately 150 h to run approximately 13,000 episodes. The system was trained well with the
andthecumulativereward,respectively.
desired accuracy.
Figures 9 and 10 illustrate the rewards for individual episodes (for a few episodes)
and the cumulative reward, respectively.
Figure 9. Reward of each episode (each colored line corresponds to one training episode).
Figure 10. Cumulative and average cumulative reward.
 Figure 9 (Episode Rewards): The figure illustrates the reward values achieved during
individual training episodes of the reinforcement learning agent. It shows a charac-
teristic learning progression starting with highly variable rewards in early episodes,
reflecting the agent’s initial exploratory phase. As training progresses, the reward val-
ues begin to stabilize and trend upward, with particularly notable improvement be-
tween episodes 2000–8000. Around episode 8000, the rewards consistently approach
and stabilize near the maximum value of 1.0, indicating the agent has learned an ef-
fective policy for the pick-and-place task. The reduction in reward volatility in later
episodes demonstrates the transition from exploration to exploitation of learned be-
haviors.
 Figure 10 (cumulative and average cumulative reward): This figure displays the ac-
cumulation of rewards over the entire training period, showing both the total cumu-
lative reward and a smoothed average trend line. The graph exhibits three distinct
phases: a steep initial learning curve in the first 4000 episodes where the agent rapidly
improves its performance, a more gradual increase in cumulative reward between
episodes 4000–8000 representing refinement of the learned policy, and finally a
draweR
evitalumuC
Figure9.Rewardofeachepisode(eachcoloredlinecorrespondstoonetrainingepisode).

Sustainability 2025, 17, x FOR PEER REVIEW 17 of 26
Sustainability2025,17,432 17of25
Figure 9. Reward of each episode (each colored line corresponds to one training episode).
Figure 10. Cumulative and average cumulative reward.
 Figure 9 (Episode Rewards): The figure illustrates the reward values achieved during
individual training episodes of the reinforcement learning agent. It shows a charac-
teristic learning progression starting with highly variable rewards in early episodes,
reflecting the agent’s initial exploratory phase. As training progresses, the reward val-
ues begin to stabilize and trend upward, with particularly notable improvement be-
tween episodes 2000–8000. Around episode 8000, the rewards consistently approach
and stabilize near the maximum value of 1.0, indicating the agent has learned an ef-
fective policy for the pick-and-place task. The reduction in reward volatility in later
episodes demonstrates the transition from exploration to exploitation of learned be-
haviors.
 Figure 10 (cumulative and average cumulative reward): This figure displays the ac-
cumulation of rewards over the entire training period, showing both the total cumu-
lative reward and a smoothed average trend line. The graph exhibits three distinct
phases: a steep initial learning curve in the first 4000 episodes where the agent rapidly
improves its performance, a more gradual increase in cumulative reward between
episodes 4000–8000 representing refinement of the learned policy, and finally a
draweR
evitalumuC
Figure10.Cumulativeandaveragecumulativereward.
• Figure9(EpisodeRewards): Thefigureillustratestherewardvaluesachieveddur-
ing individual training episodes of the reinforcement learning agent. It shows a
characteristic learning progression starting with highly variable rewards in early
episodes,reflectingtheagent’sinitialexploratoryphase. Astrainingprogresses,the
rewardvaluesbegintostabilizeandtrendupward,withparticularlynotableimprove-
mentbetweenepisodes2000–8000. Aroundepisode8000,therewardsconsistently
approach and stabilize near the maximum value of 1.0, indicating the agent has
learnedaneffectivepolicyforthepick-and-placetask. Thereductioninrewardvolatil-
ityinlaterepisodesdemonstratesthetransitionfromexplorationtoexploitationof
learnedbehaviors.
• Figure 10 (cumulative and average cumulative reward): This figure displays the
accumulation of rewards over the entire training period, showing both the total
cumulative reward and a smoothed average trend line. The graph exhibits three
distinctphases: asteepinitiallearningcurveinthefirst4000episodeswheretheagent
rapidly improves its performance, a more gradual increase in cumulative reward
betweenepisodes4000–8000representingrefinementofthelearnedpolicy,andfinally
aplateauphaseafterepisode8000wherethelearningstabilizes.Thesmoothedaverage
linehelpsvisualizetheoveralllearningtrajectorybyreducingtheimpactofepisode-
to-episodevariations,clearlyshowingtheconvergencetowardoptimalperformance.
These results demonstrate successful training of the reinforcement learning agent
fortheindustrialmanipulatortask,withclearevidenceofbothlearningprogressionand
ultimateperformanceachievement. Thetrainingprofilesuggeststhesystemdevelopeda
reliableandstablecontrolpolicysuitableforindustrialapplications.
Thisresearchexplorestheapplicationofreinforcementlearning(RL)fortrajectory
optimization of the ABB IRB120 industrial manipulator, a six-degree-of-freedom robot
usedforpick-and-placetasks. Theprimarygoalwastodesignanenergy-efficientcontrol
strategythatimprovesprecisionandminimizesenergyconsumption. Belowisadetailed
overviewofthefindings:
5.1. TrainingProcess
TheRLagentwastrainedusingMATLAB’sReinforcementLearningToolbox. The
systemcomplexity,involvingsixactions,27observations,andthreeoutputs,resultedina
computationallyintensivetrainingprocess:

Sustainability2025,17,432 18of25
(cid:5)
UsedMATLAB’sReinforcementLearningToolbox;
(cid:5)
Duration: Approximately150h;
(cid:5)
Episodes: Approximately13,000;
(cid:5)
Systemcomplexity: sixactions,27observations,threeoutputs.
5.2. PositioningAccuracyandComparisonwithReferenceMethod
The RL agent’s performance was evaluated in 100 test cases, and its positioning
accuracy was compared to a traditional inverse kinematics and trajectory optimization
approach. Table 6 summarizes both the RL agent’s positioning accuracy and the error
comparisonwiththereferencemethod:
Table6.Positioningaccuracyandcomparisonwithreferencemethod.
Metric Value ReferenceMethod MLEvaluationMetrics
MeanPositioningError 2.14mm 3.27mm Accuracy:91.2%
MedianPositioningError 1.92mm 2.89mm Precision:89.7%
MaximumPositioningError 6.83mm 9.15mm Recall:93.4%
MinimumPositioningError 0.37mm 0.21mm F1-Score:91.5%
StandardDeviation 1.45mm 2.06mm -
Positioning metrics show improvement over the reference method with ML evaluation revealing balanced
performance(F1-Score)andcompleteMLmetricsprovidebettermodelqualityassessment.
5.2.1. Axis-SpecificErrors
(cid:5)
X-axis: Meanerrorof2.14mm(SD:1.32mm);
(cid:5)
Y-axis: Meanerrorof1.87mm(SD:0.98mm);
(cid:5)
Z-axis: Meanerrorof1.62mm(SD:1.15mm);
(cid:5)
OverallEuclideanDistanceError: Meanof3.28mm(SD:1.67mm).
Sustainability 2025, 17, x FOR PEER REVIEWT hedistributionofpositioningerrorsacrossthetestcasesisvisualizedint1h9e offo 2ll6o wing
chart(Figure11):
FFiigguurere 111.1 D.Disitsrtibriubtuiotnio onf orofbroobt optospiotisointiionngi enrgroerrsr.o rs.
Key observations:
 The majority of positioning errors fall within the 1–3 mm range, consistent with the
mean error of 2.14 mm.
 Few cases exceed 4 mm error, aligning with the maximum reported error of 6.83 mm.
 The distribution shows a slight right skew, indicating occasional larger errors.
The RL agent’s performance was compared to a reference method using traditional
inverse kinematics and trajectory optimization. The results are visualized in the following
chart (Figure 12):
Figure 12. Error comparison chart between the RL agent and the reference method.

Sustainability 2025, 17, x FOR PEER REVIEW 19 of 26
Sustainability2025,17,432 19of25
Figure 11. Distribution of robot positioning errors.
Keyobservations:
Key observations:
• Themajorityofpositioningerrorsfallwithinthe1–3mmrange,consistentwiththe
 The majority of positioning errors fall within the 1–3 mm range, consistent with the
meanerrorof2.14mm.
mean error of 2.14 mm.
• Fewcasesexceed4mmerror,aligningwiththemaximumreportederrorof6.83mm.
 Few cases exceed 4 mm error, aligning with the maximum reported error of 6.83 mm.
• Thedistributionshowsaslightrightskew,indicatingoccasionallargererrors.
 The distribution shows a slight right skew, indicating occasional larger errors.
TheRLagent’sperformancewascomparedtoareferencemethodusingtraditional
The RL agent’s performance was compared to a reference method using traditional
iinnvveerrssee kkininememataictisc asnadn tdratjreacjteocrtyo royptoimptiizmatiizoant.i oTnh.eT rehseurletss uarlets vaisreuavliiszueda liinz ethdei nfotlhloewfionlglo wing
cchhaarrt t(F(Figiguurer e121)2: ):
FFiigguurere 112.2 E.rErrorro crocmompapriasroinso cnhacrhta brettbweetewne tehne tRhLe aRgLenatg aenndt athned rtehfeerreenfceer emnectehomde. thod.
5.2.2. ComparisonKeyFindings
• TheRLagentoutperformedthereferencemethodinmeanerror,medianerror,maxi-
mumerror,andstandarddeviation.
• OnlyinminimumerrordidthereferencemethodslightlyoutperformtheRLagent
(0.21mmvs. 0.37mm).
• TheRLagentshowedparticularimprovementinreducingmaximumerrorandstan-
darddeviation,indicatingmoreconsistentperformanceacrossscenarios.
5.3. ValidationandBenchmarkAnalysisofRLforRoboticControl
Thevalidationmethodologyencompassesthreeprimarycomponents: quantitative
performanceanalysis,empiricaltesting,andcomparativeevaluationagainstestablished
methodologies.
Thetrainingqualityassessmentutilizedmultipleperformanceindicators,including
episode reward convergence, cumulative reward progression, temporal stability analy-
sis,andcomputationalefficiencymetrics. Empiricalvalidationwasconductedthrough
100standardizedtestscenarios,evaluatingkeyperformanceparameters: positioningaccu-
racy,trajectoryoptimization,andenergyconsumptionefficiency. Statisticalanalyseswere
performedtoverifythereliabilityandreproducibilityoftheresults.
For benchmark comparison, traditional inverse kinematics (IK) with trajectory op-
timization was selected as the reference methodology, given its widespread industrial
implementationandestablishedtheoreticalfoundation. Thisselectionwasbasedonthree
crucialfactors: itspositionasanindustrystandardinrobotics,itscapabilitytoprovide
deterministicsolutionswithquantifiablecomputationalrequirements,anditsextensive
practicalimplementationinindustrialapplications.

Sustainability2025,17,432 20of25
The results demonstrate that the RL approach achieved comparable or superior per-
formancetotraditionalIKmethodsacrossstandardevaluationmetrics,whilemaintaining
practicalapplicabilityforindustrialdeployment. Thisvalidationframeworkestablishesa
robustfoundationforevaluatingRL-basedroboticcontrolsystemsinindustrialapplications.
5.4. TrajectoryCharacteristics
The trajectory visualization presented here is a representation of the learned path
comparedtothedesiredpath. ThisTypicalTrajectoryComparisonhasbeencreatedbased
onthecharacteristicsstudiedandtheresultsobtainedfromtheresearch.
The trajectory performance of the RL model was thoroughly evaluated through a
multi-planespatialanalysis,asshowninFigure13. Thisanalysiscomparesthedesired
(blue)andlearned(green)trajectoriesacrossthe(a)XYplane(topview),(b)XZplane(side
view), (c)YZplane(frontview), (d)full3Dvisualizationoftheend-effector’spath. By
examiningthetrajectoriesinthesedifferentviewingplanes,acomprehensiveassessment
Sustainability 2025, 17, x FOR PEER REVIEW 21 of 26
ofthemodel’strackingcapabilityacrossallspatialdimensionsisprovided.
Figure13.Simulatedlearnedtrajectoryvs.desiredtrajectory.
Figure 13. Simulated learned trajectory vs. desired trajectory.
This multi-plane approach allows for a detailed understanding of the RL model’s
This analysis presents a detailed interpretation of the RL model’s performance across
performanceintmraucltkipinleg stphaetidale spilraendesp taot he,vdaleumatoe nitsst rtaratijnecgtoirtys atrcaccukrinagcy aaccnudrascpya. tTiahle srteasbuilltist yd.emon-
Thisanalyssitsraptree mseinnitmsaal ddeetvaiailteiodni bnettewrpeerent tahteio dnesoirfetdh aenRdL lemarondede lp’satphes,r ifnodrmicaatnincge tahcer roosbsustness
multiplespatialopfl athnee RsLto aepvparoluacahte init csotnratrjoelcltinogry thtrea 6c-kDiOngF aincdcuusrtarciayl. mThaneipreusluatlotsr. demonstrate
minimaldeviationbeIntw theee nXYth Peladnees iVreiedwa, nthde lperairmnaerdy pmaothtiso,ni npdroifcialet ionfg ththee pricokb-uanstdn-peslascoe ftathske is cap-
tured. The RL model tracks the trajectory with excellent precision, achieving a mean error
RLapproachincontrollingthe6-DOFindustrialmanipulator.
of 0.11 mm. The greatest deviation occurs at the motion extremes, and the maximum
IntheXYPlaneView,theprimarymotionprofileofthepick-and-placetaskiscaptured.
height reaches 6 mm at t = 4 − 5 s. The trajectory shows smooth acceleration and deceler-
The RL model tracks the trajectory with excellent precision, achieving a mean error of
ation, reflecting effective control throughout the task. This indicates that the RL model can
0.11mm. Thegreatestdeviationoccursatthemotionextremes,andthemaximumheight
follow the desired path while maintaining a stable velocity profile.
reaches 6 mm at t = 4–5 s. The trajectory shows smooth acceleration and deceleration,
The XZ Plane View presents the side view of the trajectory, emphasizing the vertical
reflectingeffectivecontrolthroughoutthetask. ThisindicatesthattheRLmodelcanfollow
motion control. The Z-axis variation is contained within ±0.5 mm, and vertical deviation
thedesiredpathwhilemaintainingastablevelocityprofile.
from the planned path remains minimal. This demonstrates the RL model’s ability to
maintain a stable height during the pick-and-place operation, with consistent perfor-
mance across the entire motion.
In the YZ Plane, the front view of the trajectory reveals that the RL model maintains
a tight grouping around the planned path. The maximum lateral deviation is under 0.2
mm, confirming excellent cross-plane stability and validating the motion’s planarity. This
indicates that the model efficiently controls lateral movement without significant devia-
tion from the desired trajectory.
The 3D Trajectory View provides a complete spatial visualization, confirming that
the predominant motion occurs along the XY plane. The model shows minimal deviation
in the out-of-plane directions, validating the overall path consistency and spatial stability.
This 3D perspective solidifies the RL approach’s ability to track trajectories effectively
across all spatial dimensions.

Sustainability2025,17,432 21of25
TheXZPlaneViewpresentsthesideviewofthetrajectory,emphasizingthevertical
motioncontrol. TheZ-axisvariationiscontainedwithin±0.5mm,andverticaldeviation
from the planned path remains minimal. This demonstrates the RL model’s ability to
maintainastableheightduringthepick-and-placeoperation,withconsistentperformance
acrosstheentiremotion.
IntheYZPlane,thefrontviewofthetrajectoryrevealsthattheRLmodelmaintainsa
tightgroupingaroundtheplannedpath. Themaximumlateraldeviationisunder0.2mm,
confirming excellent cross-plane stability and validating the motion’s planarity. This
indicatesthatthemodelefficientlycontrolslateralmovementwithoutsignificantdeviation
fromthedesiredtrajectory.
The3DTrajectoryViewprovidesacompletespatialvisualization,confirmingthatthe
predominantmotionoccursalongtheXYplane. Themodelshowsminimaldeviationinthe
out-of-planedirections,validatingtheoverallpathconsistencyandspatialstability. This
Sustainability 2025, 17, x FOR PEER REVIEW 22 of 26
3DperspectivesolidifiestheRLapproach’sabilitytotracktrajectorieseffectivelyacrossall
spatialdimensions.
In summary, the key precision metrics of the RL model include a mean tracking
In summary, the key precision metrics of the RL model include a mean tracking error
error of 0.11 mm and a maximum deviation of 0.21 mm, demonstrating its consistent
of 0.11 mm and a maximum deviation of 0.21 mm, demonstrating its consistent perfor-
performance. The motion characteristics reflect smooth trajectory following with well-
mance. The motion characteristics reflect smooth trajectory following with well-controlled
controlledaccaeclceerlaetriaotnioann adndde dceelceerlaertiaotnio,nc,o cnotnritbriubtuintigngto tom miniinmimalasl pspataitaialld drirfitf.t.P Peerrfoforrmmaannccee valida-
validationindtiiocna tiensdsicuapteesr isourpterraicokr itnrgaciknintgh einX tYhep XlaYn pelwanieth weixthc eelxlecneltlevnetr vtiecratlicsatla sbtialibtiylitayn adnd mini-
minimaldevimatiaol ndienvitahteioXnZ ina nthde YXZZ palnadn eYsZ,r epilnafnoersc,i nregintfhoercrionbgu tshtne ersosbaunsdtneefsfis cainendc eyffoicfitehnecy of the
RL-basedconRtrLo-lbsaysesdte cmo.ntrol system.
5.5. JointAngl5e.5A. nJoailnyts Aisnagnled ADnHal-yRsiLs Panedrf oDrHm-aRnLc ePCerofomrmpaarniscoe nComparison:
TovalidatethTeo pvaelrifdoartme athnec epeorffoorumraRnLcem ofo oduerl RcoLm mpoadreeld cotomtpraardeidti oton atrlaidnivtieornsael kininveer-se kine-
matics,weanmaalytizcesd, wthe eanjoailnytzeadn gthlee tjroainjetc atonrgilees trgaejnecetroartieesd gbeynebroattheda pbyp rbooatchh aepsp.rFoiagcuhrees.1 F4igure 14
presentsacopmrpesaernattsi vae caonmaplyarsaistivbee tawneaelynsiDs Hbetiwnveeenrs DeHki ninevmerasteic ksinanemdaRtiLcss aonludt iRoLn ssoflourtiaons for a
typicalpick-atnydpi-cpalla pceicmk-aontido-np.laTchee mcootmiopna. Trihsoe ncoemncpoamrispoans esenscoamllpsaixssjeosi natlla snixg ljoesinat nadngtlheesi arnd their
corresponding error metrics over a 9 s trajectory. This analysis is crucial for demonstrating
correspondingerrormetricsovera9strajectory. Thisanalysisiscrucialfordemonstrating
the RL model’s capability to generate feasible joint angles while maintaining accuracy
the RL model’s capability to generate feasible joint angles while maintaining accuracy
comparable to conventional inverse kinematics solutions.
comparabletoconventionalinversekinematicssolutions.
Figure14.ComparisonofjointangletrajectoriesbetweenDHandRLsolutions.
Figure 14. Comparison of joint angle trajectories between DH and RL solutions.
The reinforcement learning (RL) model achieves joint angle trajectories closely
aligned with the Denavit–Hartenberg (DH) inverse kinematics solution. In the top plot,
the dashed lines represent the DH solution, while the solid lines depict the RL results,
illustrating precise tracking of all six joint angles. The bottom plot provides a quantitative
analysis of the joint angle errors, showing a mean position error of 0.12 mm and a mean
joint angle error of 4.30°. These results validate the accuracy of the RL approach for joint-
space control.
5.6. Applicability
The results suggest that the proposed approach, using reinforcement learning with
an efficient LQR controller, is effective for learning optimal control policies for the IRB120
industrial manipulator in a simulated pick-and-place scenario.

Sustainability2025,17,432 22of25
Thereinforcementlearning(RL)modelachievesjointangletrajectoriescloselyaligned
withtheDenavit–Hartenberg(DH)inversekinematicssolution. Inthetopplot,thedashed
lines represent the DH solution, while the solid lines depict the RL results, illustrating
precisetrackingofallsixjointangles. Thebottomplotprovidesaquantitativeanalysisof
thejointangleerrors,showingameanpositionerrorof0.12mmandameanjointangle
errorof4.30◦. TheseresultsvalidatetheaccuracyoftheRLapproachforjoint-spacecontrol.
5.6. Applicability
Theresultssuggestthattheproposedapproach,usingreinforcementlearningwith
anefficientLQRcontroller,iseffectiveforlearningoptimalcontrolpoliciesfortheIRB120
industrialmanipulatorinasimulatedpick-and-placescenario.
5.7. StatisticalMetrics
TheevaluationoftheIRB120industrialmanipulator’spositioningaccuracyisbasedon
acomprehensivesetofstatisticalmetricsthatcollectivelyprovideadetailedunderstanding
ofitsperformance,asreflectedbyTable7.
Table7. ThestatisticalmetricsusedtoevaluatethepositioningaccuracyoftheIRB120indus-
trialmanipulator.
Metric Formula Description
Meanerrorof2.14mmrepresentstheaverage
Mean n
PositioningError µ= n 1 ∑ x i ge d n e e v ra ia l t s i e o n n s f e ro o m fa t c h c e ur t a a c rg y e b t u p t o i s s it a i f o f n ec . t I e t d p b ro y v o id u e tl s ie a rs.
i=1
Medianerrorof1.92mmsuggeststhathalfofthe
Median
Middlevalueoforderedpositioningerrors errorsarebelowthisvalue.Itislesssensitiveto
PositioningError
outlierscomparedtothemean.
(cid:118)
(cid:117) n
StandardDeviation σ= (cid:117) (cid:116) n 1 ∑ (x i −µ)2 S l t o a w nd er ar v d al d u e e v i i n at d io ic n at o e f s 1 m .45 or m e m con q s u i a s n te t n ifi t e p s e v r a fo ri r a m b a il n it c y e . . A
i=1
Themaximumerrorof6.83mmhighlightsthe
Maximum
PositioningError
max(|x
i
−xtrue |) worst-casescenarioinperformance,crucialfor
evaluatingreliabilityincriticaltasks.
Theminimumerrorof0.37mmshowcasestherobot’s
Minimum
PositioningError
min(|x
i
−xtrue |) bestperformanceunderidealconditions,thoughnot
reflectiveoftypicalperformance.
(cid:115)
Dis
E
t
u
an
cl
c
i
e
de
E
a
r
n
ror
E=
(cid:0) y
measured
(
−
x m
y
e
t
a
ru
su
e
r
(cid:1)
e
2
d
+
−
(
x
z
t
m
ru
e
e
a
)
s
2
u
+
red
−ztrue )2
MeanEu
m
cl
e
id
as
e
u
a
r
n
e
e
o
r
f
ro
3
r
D
o
p
f
o
3
s
.2 it
8
io
m
n
m
ing
p
a
ro
cc
v
u
id
ra
e
c
s
y
a
.
noverall
5.8. EnergyOptimizationandWarehousePerformance
EnergyMinimizationandWarehouseAutomationImprovements: Energyminimiza-
tioninroboticsystemsisachievedbyoptimizingoperationalparameterstobalanceeffi-
ciencyandperformance. Inthisstudy,reducingtherobot’sspeedledtosignificantbenefits,
includinglowerpowerconsumption, reducedmechanicalstressandwear, andquieter,
cooleroperation. However,theseadvantagesareaccompaniedbytrade-offs,suchaslonger
taskcompletiontimes, feweroperationspershift, andaslightreductioninpositioning
precision. Thisenergy-efficientmodeisparticularlywell-suitedforlow-prioritytasksbut
maynotbeidealforhigh-throughputproductionlineswherespeedandtaskfrequency
arecritical. Theselectionbetweenenergy-efficientandhigh-performancemodesmustbe
tailoredtothespecificrequirementsoftheapplication.
WarehouseAutomationImprovements: Theproposedreinforcementlearning(RL)
framework, combined with an efficient Linear Quadratic Regulator (LQR) controller,

Sustainability2025,17,432 23of25
demonstratedsubstantialenhancementsinwarehouseautomationandoperationalproduc-
tivity. TheintegrationofRLresultedinthefollowing:
• CargoDistributionOptimization: Achievinga25%improvementcomparedtotradi-
tionalmethods,attributedtobetter-balancedstorageandmoreefficientspaceutiliza-
tionwithinthewarehouse.
• OperationalEfficiency: Whileminimizingenergyconsumption,theRL-basedsystem
maintainedhightaskperformance, streamliningpick-and-placeoperations. These
findingsunderscorethepotentialoftheRL-basedcontrolsystemtoenhancewarehouse
automationbyimprovingbothproductivityandenergyefficiency,addressingcritical
demandsofmodernindustrialandlogisticsenvironments
5.9. FutureWork
Theresultssuggestthatfurtheranalysiscouldbeconductedtoinvestigatethesources
of larger positioning errors and potential strategies to improve the overall positioning
accuracyandconsistencyoftheRLagent’spolicy.
6. Conclusions
Thisstudydemonstratesthesuccessfulapplicationofreinforcementlearning(RL)for
optimizingtrajectoryandcontrollingthesix-degree-of-freedomIRB120industrialmanipula-
torinpick-and-placetasks.TheRLagentdevelopedanefficientpolicythatachievedprecise
positioningwithsub-5mmaccuracywhileminimizingenergyconsumption,makingit
suitableforvariousindustrialapplications.
AnefficientLinearQuadraticRegulator(LQR)controllerwasimplementedforeach
jointoftheIRB120,modeledinSimulinkandintegratedwithRobotStudioforsimulation.
ThetrainedRLmodelexhibitedpromisingperformancecomparedtotraditionalinverse
kinematicsandtrajectoryoptimizationmethods.
ThesefindingshighlightthepotentialofRLinwarehouseautomationandindustrial
robotics,offeringenhancedaccuracy,energysavings,andconsistencyincomplexmanipula-
tiontasks. TheRLagentconsistentlyoutperformedtraditionalinversekinematicsmethods,
deliveringsmootherandmoreefficienttrajectories,suggestingpotentialenergysavings,
reducedwear,andincreasedoperationalefficiencyinroboticsystems. Thisstudyunder-
scoresthepotentialofRLtechniquestoenhanceaccuracy,consistency,andenergyefficiency,
layingafoundationformoreadaptiveandpreciseroboticapplicationsinthefuture.
AuthorContributions:Conceptualization,A.I.andG.S.;implementation,A.I.;networktraining,A.I.;
validation,A.I.andG.S.;supervision,G.S.;projectadministration,G.S.Allauthorshavereadand
agreedtothepublishedversionofthemanuscript.
Funding:SupportfromtheNationalUniversityofScienceandTechnologyPolitehnicaofBucharest
throughthePubArtprogramisgratefullyacknowledged.
DataAvailabilityStatement:Theoriginalcontributionspresentedinthestudyareincludedinthe
article,furtherinquiriescanbedirectedtothecorrespondingauthor.
ConflictsofInterest:Theauthorsdeclarenoconflictsofinterest.
References
1. Vytvytska,O.D.;Martynyuk,O.A.;Shpak,N.O.;Karcheva,G.T.;Medynsky,I.P.Structural-functionalmodelingforthedeter-
minationofthecompany’sequilibriumconditionsinthedynamicbusinessenvironment.J.Phys.Conf.Ser.2019,1457,012033.
[CrossRef]
2. Wang,H.;Wang,H.;Huang,J.;Zhao,B.;Quan,L.Smoothpoint-to-pointtrajectoryplanningforindustrialrobotswithkinematical
constraintsbasedonhigh-orderpolynomialcurve.Mech.Mach.Theory2019,139,284–293.[CrossRef]

Sustainability2025,17,432 24of25
3. Ang, Z.H.; Ang, C.K.; Lim, W.H.; Yu, L.J.; Solihin, M.I. Development of an artificial intelligent approach in adapting the
characteristicofpolynomialtrajectoryplanningforrobotmanipulator.Int.J.Mech.Eng.Robot.Res.2020,9,408–414.[CrossRef]
4. Pavel, M.D.; Rosioru, S.; Arghira, N.; Stamatescu, G.ControlofOpenMobileRoboticPlatformUsingDeepReinforcement
,
Learning.InServiceOriented,HolonicandMulti-AgentManufacturingSystemsforIndustryoftheFuture;SOHOMA2022;Studiesin
ComputationalIntelligence;Borangiu,T.,Trentesaux,D.,Leitão,P.,Eds.;Springer:Cham,Switzerland,2023;Volume1083.
5. Benotsmane,R.;Dudás,L.;Kovács,G.Trajectoryoptimizationofindustrialrobotarmsusinganewlyelaborated“whip-lashing”
method.Appl.Sci.2020,10,8666.[CrossRef]
6. Bertolini,M.;Mezzogori,D.;Neroni,M.;Zammori,F.MachineLearningforindustrialapplications:Acomprehensiveliterature
review.ExpertSyst.Appl.2021,175,114820.[CrossRef]
7. Xia,K.;Sacco,C.;Kirkpatrick,M.;Saidy,C.;Nguyen,L.;Kircaliali,A.;Harik,R.Adigitaltwintotraindeepreinforcement
learningagentforsmartmanufacturingplants: Environment,interfacesandintelligence. J.Manuf. Syst. 2021,58,210–230.
[CrossRef]
8. Liu,Z.;Liu,Q.;Xu,W.;Wang,L.;Zhou,Z.RobotLearningTowardsSmartRoboticManufacturing:AReview.Robot.Comput.
Integr.Manuf.2022,77,102360.[CrossRef]
9. Calderón,C.A.A.;Sarango,R.;Castillo,D.;Lakshminarayan,V.ADeepReinforcementLearningFrameworkforControlof
RoboticManipulatorsinSimulatedEnvironments.IEEEAccess2023,12,103133–103161.[CrossRef]
10. Djeffal,S.;Morakchi,M.R.;Ghoul,A.;Kargin,T.C.DDPG-BasedReinforcementLearningforControllingaSpatialThree-Section
ContinuumRobot.Eng.Appl.Artif.Intell.2023,121,106323.[CrossRef]
11. Li,S.;Huang,W.;Miao,C.;Xu,K.;Chen,Y.;Sun,T.;Cui,Y.EfficientRobotManipulationviaReinforcementLearningwith
DynamicMovementPrimitives-BasedPolicy.Appl.Sci.2024,14,10665.[CrossRef]
12. Wang, X.; Cao, J.; Cao, Y.; Zou, F. Energy-efficient trajectory planning for a class of industrial robots using parallel deep
reinforcementlearning.NonlinearDyn.2024,1–21.[CrossRef]
13. Vodovozov, V.; Raud, Z.; Petlenkov, E. Intelligent Control of Robots with Minimal Power Consumption in Pick-and-Place
Operations.Energies2023,16,7418.[CrossRef]
14. Lobbezoo,A.;Qian,Y.;Kwon,H.-J.ReinforcementLearningforPickandPlaceOperationsinRobotics:ASurvey.Robotics2021,
10,105.[CrossRef]
15. Simon,J.;Gogolák,L.;Sárosi,J.DeepReinforcementLearning-AssistedTeachingStrategyforIndustrialRobotManipulator.Appl.
Sci.2024,14,10929.[CrossRef]
16. Montobbio,F.;Staccioli,J.;Virgilito,M.E.;Vivarelli,M.RobotsandtheOriginofTheirLabour-SavingImpact.Technol.Forecast.
Soc.Chang.2022,174,121122.[CrossRef]
17. Zeng,A.;Song,S.;Yu,K.T.;Donlon,E.;Hogan,F.R.;Bauza,M.;Ma,D.;Taylor,O.;Liu,M.;Romo,E.;etal.Roboticpick-and-place
ofnovelobjectsinclutterwithmulti-affordancegraspingandcross-domainimagematching.Int.J.Robot.Res.2022,41,690–705.
[CrossRef]
18. Mazzei,D.;Ramjattan,R.MachineLearningforIndustry4.0:ASystematicReviewUsingDeepLearning-BasedTopicModelling.
Sensors2022,22,8641.[CrossRef][PubMed]
19. Borgi, T.; Hidri, A.; Neef, B.; Naceur, M.S. Data Analytics for Predictive Maintenance of Industrial Robots: A Review. In
Proceedingsofthe2017InternationalConferenceonAdvancedSystemsandElectricTechnologies(IC_ASET),Hammamet,
Tunisia,14–17January2017;pp.412–417.
20. Zhao,W.;Queralta,J.P.;Qingqing,L.;Westerlund,T.TowardsClosingtheSim-to-RealGapinCollaborativeMulti-RobotDeep
ReinforcementLearning. InProceedingsofthe20205thInternationalConferenceonRoboticsandAutomationEngineering
(ICRAE),Singapore,20–22November2020;pp.200–204.
21. Bahrpeyma,F.;Reichelt,D.AReviewoftheApplicationsofMulti-AgentReinforcementLearninginSmartFactories.Front.Robot.
AI2022,9,3152.[CrossRef]
22. Yudha,P.P.;Nageshrao,S.P.;Kober,J.;Babuska,R.ReinforcementLearning-BasedCompensationMethodsforRobotManipulators.
Eng.Appl.Artif.Intell.2019,78,236–247.
23. Zhou,L.;An,J.;Zhao,R.;Mu,H.TrajectoryPlanningandSimulationofIndustrialRobotBasedonMATLABandRobotStudio.In
Proceedingsofthe2021IEEE4thInternationalConferenceonElectronicsTechnology(ICET),Chengdu,China,7–10May2021.
24. Iqdymat,A.;Stamatescu,G.AnalysisofTrajectoryOptimizationforSolvingTowerofHanoiProblemusingIndustrialManipulator.
InProceedingsofthe202324thInternationalConferenceonControlSystemsandComputerScience(CSCS),Bucharest,Romania,
18–20May2023.
25. Rahul,M.R.;Chiddarwar,S.S.IntegratingVirtualTwinandDeepNeuralNetworksforEfficientandEnergy-AwareRobotic
DeburringinIndustry4.0.Int.J.Precis.Eng.Manuf.2023,24,1517–1534.[CrossRef]
26. Kim,H.;Kim,Y.-J.;Kim,W.-T.DeepReinforcementLearning-BasedAdaptiveSchedulingforWirelessTime-SensitiveNetworking.
Sensors2024,24,5281.[CrossRef]

Sustainability2025,17,432 25of25
27. Sun,Y.;Van,M.;McIlvanna,S.;Minh,N.N.;McLoone,S.;Ceglarek,D.AdaptiveAdmittanceControlforSafety-CriticalPhysical
Human-RobotCollaboration.IFAC-PapersOnLine2023,56,1313–1318.[CrossRef]
28. Zhang,L.;Zhang,L.;Shen,L.;Yuan,B.;Wang,X.;Tao,D.EvaluatingModel-FreeReinforcementLearningTowardSafety-Critical
Tasks.Proc.AAAIConf.Artif.Intell.2023,37,14098–14106.[CrossRef]
29. Gu,S.;Yang,L.;Du,Y.;Chen,G.;Walter,F.;Wang,J.;Knoll,A.AReviewofSafeReinforcementLearning:Methods,Theoriesand
Applications.IEEETrans.PatternAnal.Mach.Intell.2023,11216–11235.[CrossRef]
30. Tzes,M.;Bousias,N.;Chatzipantazis,E.;Pappas,G.GraphNeuralNetworksforMulti-RobotActiveInformationAcquisition.
IEEERobot.Autom.Lett.2023,8,3497–3503.
31. Azadeh,K.;deKoster,M.B.M.;Roy,D.RobotizedandAutomatedWarehouseSystems:ReviewandRecentDevelopments.Transp.
Sci.2019,53,917–945.[CrossRef]
32. Denavit,J.;Hartenberg,R.S.Akinematicnotationforlower-pairmechanismsbasedonmatrices.J.Appl.Mech.1955,22,215–221.
[CrossRef]
Disclaimer/Publisher’sNote: Thestatements, opinionsanddatacontainedinallpublicationsaresolelythoseoftheindividual
author(s)andcontributor(s)andnotofMDPIand/ortheeditor(s).MDPIand/ortheeditor(s)disclaimresponsibilityforanyinjuryto
peopleorpropertyresultingfromanyideas,methods,instructionsorproductsreferredtointhecontent.