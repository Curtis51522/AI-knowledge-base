Review
Trajectory Planning for Robotic Manipulators in Automated
Palletizing: A Comprehensive Review
SamuelRomero1,JorgeValero1,AndreaValentinaGarcía2,CarlosF.Rodríguez3,AnaMariaMontes1 ,
CesarMarín2 ,RubenBolaños2andDavidÁlvarez-Martínez1,*
1 DepartmentofIndustrialEngineering,UniversityofLosAndes,Bogotá111711,Colombia;
sj.romero10@uniandes.edu.co(S.R.);js.valero10@uniandes.edu.co(J.V.);a.montesf@uniandes.edu.co(A.M.M.)
2 IntegraS.A.,Pereira660003,Colombia;vgarcia@integra.com.co(A.V.G.);cmarin@integra.com.co(C.M.);
rbolanos@integra.com.co(R.B.)
3 DepartmentofMechanicalEngineering,UniversityofLosAndes,Bogotá111711,Colombia;
crodrigu@uniandes.edu.co
* Correspondence:d.alvarezm@uniandes.edu.co
Abstract: Recentindustrialproductionparadigmshaveseenthepromotionoftheoutsourc-
ingoflow-value-addedoperationstoroboticcellsasaservice,particularlyend-of-linepack-
aging. Asaresult,varioustypesofresearchhaveemerged,offeringdifferentapproachesto
thetrajectorydesignoptimizationofroboticmanipulatorsandtheirapplications.Overtime,
numerousimprovementsandupdateshavebeenmadetotheproposedmethodologies,
addressingthelimitationsandrestrictionsofearlierwork.Thissurvey-typearticlecompiles
researcharticlespublishedinrecentyearsthatfocusonthemainalgorithmsproposedfor
addressingplacementandminimum-timepathplanningforamanipulatorresponsiblefor
performingpick-and-placetasks. Specifically,theresearchexaminestheconstructionofan
automatedroboticcellforthepalletizingofregularheterogeneousboxesonacollision-free
mixedpallet. Byreviewingandsynthesizingthemostrecentresearch,thisarticlesheds
lightonthestate-of-the-artmanipulatorplanningalgorithmsforpick-and-placetasksin
palletizingapplications.
AcademicEditor:CharalamposP.
Keywords: robotic manipulators; collision; trajectory planning; palletizing; inverse
Bechlioulis
kinematic;B-spline
Received:25February2025
Revised:14April2025
Accepted:22April2025
Published:26April2025
1. Introduction
Citation: Romero,S.;Valero,J.;
Industrialrobotsareincreasinglyusedformanufacturingandpackagingoperations,
García,A.V.;Rodríguez,C.F.;Montes,
A.M.;Marín,C.;Bolaños,R.; includingend-of-linepalletizing. Inmodernproduction,companiesoftenoutsourcesuch
Álvarez-Martínez,D.Trajectory low-value-addedtaskstospecializedrobotizedcellsthatprovidepacking’asaservice’. A
PlanningforRoboticManipulatorsin typicalpalletizingcellconsistsofaconveyorfeedingproducts,apalletizingstation,and
AutomatedPalletizing:A
aroboticmanipulatorthattransfersproductsfromtheinfeedtothepallet[1]. Apossible
ComprehensiveReview.Robotics2025,
schematicofaroboticpackagingcellisshowninFigure1.
14,55. https://doi.org/10.3390/
Planningefficienttrajectoriesforthemanipulatorinthiscontextiscriticaltoensure
robotics14050055
high throughput and collision-free operation. Robotic trajectory planning generally in-
Copyright:©2025bytheauthors.
volves computing a path and time schedule for a robot to move from a start to a goal
LicenseeMDPI,Basel,Switzerland.
configurationwhilesatisfyingkinematicanddynamicconstraints. Classicobjectivesin-
Thisarticleisanopenaccessarticle
distributedunderthetermsand cludeminimizingmotiontime,distance,orenergyandavoidingcollisions. Overthepast
conditionsoftheCreativeCommons decades,awidevarietyofalgorithmshasbeendevelopedtoaddresstheseobjectives,from
Attribution(CCBY)license earlyoptimalcontrolapproachesinthe1980stomodernsampling-basedplannersand
(https://creativecommons.org/
machinelearningtechniques. Despitesignificantprogress,severalopenchallengesremain.
licenses/by/4.0/).
Robotics2025,14,55 https://doi.org/10.3390/robotics14050055

Robotics2025,14,55 2of23
Forexample,inamixed-casepalletizingscenario,therobotmustautonomouslydetermine
afeasiblestackingsequenceandtrajectoryonthefly,sincetheremaybenopre-defined
stackingpattern. Programmingarobottohandleheterogeneouspackageswithoutafixed
pattern under real-time constraints remains difficult. Moreover, achieving high-speed
motionwithoutsacrificingprecisionorcausingexcessivewearisanongoingconcern. The
manipulator operates in a semi-structured, dynamic environment—for example, boxes
arrivingonaconveyorinaconstrainedworkspace—whereitmustreliablyavoidstaticand
movingobstacleswhilecarryingpayloads.
Figure1.Schematicoftheassembly.
Anumberofrecentworkshavespecificallytargetedpalletizingapplicationstoaddress
thesechallenges. Forexample,researchershaveproposedheuristic“stacking”algorithms
forrobot-basedmixed-casepalletizingusingindustrialarms[2],aswellasmobilerobotic
systemscapableofbuildingheterogeneouspalletsfromhomogeneousunitloads[3]. Other
studies optimized palletizing operations by minimizing the robot’s travel distance via
integerlinearprogramming(ILP)[4]orbyintegratingvisualperceptionandhigh-level
planninginhuman–robotcollaborativepalletizingframeworks[5]. Theseeffortsunder-
scoretheactiveinterestinimprovingpalletizingefficiency,yetafullygeneralizedsolution
that meets all performance requirements in diverse scenarios is still lacking. However,
some recent studies have focused on the integrated design of complete palletizing sys-
tems,implementingspecializedalgorithmstoaddresseachsubsystem’schallenges. For
instance,Zhuet.al. [6]proposedapalletizingsystemcombiningvision-basedobjectdetec-
tion,packingarrangementcomputation,andcollision-freetrajectoryplanningtooptimize
theentireworkflow. Otherresearchershavetargetedspecificsubsystemsforincremental
improvements. Forexample,Boshoffet.al. [7]employedUnmannedAerialVehicles(UAVs)
to enhance obstacle and target pose estimation, enabling more accurate dynamic envi-
ronmentmapping. Songetal. [8]presentedalight-weightroboticsystemoptimizedfor
narrowcuboidspaces,introducinganadsorption-trayhybridgripperandatime-optimal
“lift-then-pick”strategythatenhancesefficiencyanddoublesrobustness. Anotherstudy
integrateddigitaltwintechnologywithreinforcementlearningtocreateanadaptivemotion
plannerthatdynamicallyselectsbetweengeometry-basedandRL-basedstrategieswhile
Bayesianoptimizationimprovesrewardtuning,resultinginfastertrainingandreliable
performanceacrosstasks[9]. Additionally,Zhixiangetal.[10]proposedanewtrajectory
planningmethodbasedonFourierseriesexpansion,achievingsmootherandmoreefficient

Robotics2025,14,55 3of23
jointmotionscomparedtoquinticpolynomials,effectivelyreducingimpactandincreasing
motioncontinuityinpalletizingoperations.
Industrialroboticmanipulatorsarethemostprevalentsolutionforpalletizingtasks,
withtheirclassificationtypicallybasedonfunctionalitycriteriaincludingautonomylevel,
payloadcapacity,degreesoffreedom(DOFs),andoperationalspeed[11,12]. Collaborative
manipulators(cobots)havebecomeparticularlyfavoredinpalletizingduetotheirflex-
ibilityandeaseofintegration[13],withMartínetal. [14]categorizingthesesystemsas
rigid,discrete,non-redundant,andnon-actuated(asillustratedinFigure2). Performance
metrics are critical for evaluating manipulator effectiveness in palletizing applications,
with Morenoetal. [15] identifying key performance indices, while Patel and Sobh [16]
reviewedmeasurementmethodologiesandHwangetal. [17]demonstratedoptimization
approachesforseven-DOFserialmanipulators—themostcommonarchitectureforcomplex
palletizingtasks.
Figure2. Venndiagramforrobotclassificationinpalletizingapplications. Whiteareasrepresent
non-applicableconfigurations.
Unlikepriorsurveysthatlookedbroadlyatmanipulatorkinematicsorcontrol(for
instance,ref. [18]reviewedoptimaltrajectoryplanningmethods,RatiuandPrichici[19]
surveyedtrajectoryoptimizationforindustrialrobots,andRahimiandNazemizadeh[20]
expounded upon dynamic analysisand intelligent controltechniques for flexible robot
manipulators from 1970 to 2013, and Haddadin et al. [21] presented the literature on
model-basedalgorithmsforreal-timecollisiondetection),thisworkconcentratesonthe
stateoftheartofusefulalgorithmsforroboticplacement,pathplanning,andtrajectory
optimizationinthecontextofautomatedpalletizing. Wecompilerelevantresearch,from
foundationalworksbefore2010tothemostrecentstudiespublishedin2025,highlighting
the evolution of approaches and the current state of the art. The contributions of this
reviewareto(1)summarizethekeyalgorithmsandstrategiesforrobotpathplanningand
trajectoryoptimization;(2)analyzetheirapplicabilitytopalletizingscenarios,includingthe
strengthsandlimitationsofeachmethod;and(3)identifyopenresearchdirectionsforfuture

Robotics2025,14,55 4of23
work. Thispaperisareviewarticle—allfindingsaresynthesizedfromexistingstudies,
andnonewexperimentalresultsarepresented. Intheremainderofthispaper,wefirst
outlinetheproblemscopeanddefinitions. Section2discussesmanipulatorplacementand
relatedperformancemetrics. Section3thenreviewstrajectoryplanningapproaches(path
generationandscheduling),andSection4coversspecificpathplanningmethods(graph
search,sampling-based,optimalcontrol,spline-based,andlearning-driventechniques).
Section5highlightsresearchgapsandfuturedirections,andfinally,Section6concludes
thepaperwithkeyinsightsforbothresearchandindustry.
2. ManipulatorPlacement
The choice of a robotic manipulator’s placement (i.e., the pose of its base in the
work cell) is a crucial initial decision that influences the robot’s reachable workspace
and performance for a given task. The base position and orientation determine which
targetpointsarereachablebytheendeffectorandaffectmetricssuchasachievablespeed,
payloadcapacity,andprecisionindifferentregionsoftheworkspace. Inpalletizingcells,
forexample,therobotbasemustbepositionedsothatallpalletlocationsandconveyor
pickuppointsliewithinthearm’sreachablevolume. Typically,onecanidentifyregionsin
themanipulator’sworkspace(sometimescalled“dexterous”or“high-performance”zones)
wheretherobotcanmovewithbetterkinematicordynamicperformance. Thegoalofbase
placementistoalignthesehigh-performancezoneswiththetaskrequirements(e.g.,the
palletlocations)tooptimizeoveralloperation.
Determining the optimal robot location is challenging because there are infinitely
manypossibleposesforthebaseandmanytask-relatedvariablestoconsider. Theproblem
isoftenformulatedasanoptimizationtask: givencertainperformanceindicators,findthe
baseposethatmaximizesthoseperformancemeasures. Researchershaveapproachedthis
byfirstidentifyingkeytaskproperties, thenselectingappropriateperformanceindices
to include in an objective function. Common performance criteria include kinematic
reachability,cycletime,energyconsumption,accuracy,andmanipulability.
2.1. PlacementPerformanceIndicators
Multiplestudieshaveproposedalgorithmstooptimizerobotbaseplacementforspe-
cificapplicationsbyfocusingonparticularperformanceindicators. Forexample,Nektarios
andAspragathos[22]formulatedanalgorithmtofindthebaselocationthatmaximizes
theendeffector’sachievablespeedalongagivenreferencetrajectory. Schneideretal. [23]
developedamethodtooptimizeamanipulator’slocationinamachiningprocessbycon-
sideringtherigidityoftherobotmechanism. Inanotherwork,Malhanetal. [24]soughtto
positionaworkpiecewithintherobot’sworkspacesuchthatthemanipulatorcouldexert
therequiredforcesforanassemblyoperation.
Other authors have optimized base placement under different criteria. Tian and
Collins [25] found placements that minimize the distance traveled by the end effector.
VosniakosandMatsas[26]exploredoptimalrobotlocationsformillingtasksbyevaluating
manipulabilityindicesandexternalforceinteractions. Similarly,Pámanes-Garcíaetal. [27]
investigatedbasepositioningusingvariouskinematicperformanceindices(e.g.,condition-
ingandmanipulability)asobjectives. Notably,somestrategieshavebeenproposedspecif-
icallytoimproveperformanceinpalletizingtasks. Forinstance, MasoodandKhan[28]
examineddifferentpalletpatternplacementstrategiesandtheireffectsonrobotpositioning
in a palletizing cell, highlighting how the base location can influence the efficiency of
stackingoperations.

Robotics2025,14,55 5of23
2.2. OptimizationinTaskSpacevs. JointSpace
Whenformulatingplacementoptimizationmathematically,onecandefinetheprob-
lem in the task (Cartesian) space or in the joint (configuration) space of the robot. An
optimization in Cartesian space might aim to maximize coverage or performance over
a set of task points (e.g., pallet coordinates), whereas a joint-space formulation can in-
corporatetherobot’skinematicanddynamiccharacteristicsmoredirectly. Forexample,
Weingartshofer et al. [29] proposed an algorithm that uses the results of a joint-space
trajectoryplannertofindtheoptimallocationofthetoolcenterpoint(and,byextension,
therobotbase). Intheirapproach, theobjectivefunctionisbuiltfromcharacteristicsof
trajectoriesinjointspace,linkingtheplacementproblemwithpathplanningoutcomes.
In another study, Dos Santos et al. [30] presented a strategy to locate the robot base so
astominimizeenergyconsumptionwhilemaximizingpositioningaccuracyforagiven
trajectory. Theyintroducedperformanceindicesrelatingenergyusetomanipulabilityand
optimizedthebaseposebasedonthoseindices.
Forcomplexscenarioswherearobotmustperformmultipletasksorservicemulti-
plelocations,researchershaveemployedreachabilityanalysisandworkspacemapping
techniques. Insteadofoptimizingforasingletrajectory,thesemethodsconsiderthesetof
alltargetpointsandmotionstherobotmustexecute. Toolssuchasreachabilitymapsor
accessibilityindicescanevaluatehowwellacandidatebasepositionallowstherobotto
reachthenecessarypointswithacceptableorientations. Forexample,someauthorshave
computedreachableworkspacevolumesorusedinversionofreachabilitytodetermine
goodbaselocationsformulti-taskoperations[31].Techniquesliketheusedofareachability
indexandcapabilitymap[32,33]graphicallyrepresenthowreachableeachpointinthe
environmentisfromagivenbasepose. Byanalyzingthesemaps,onecanchooseabase
placementthatcoversallrequiredtaskpoints. Otherauthorshavesuggestedcompound
algorithmstosolvetheproblem. DoanandLin[34]presentedamethodologyofthreealgo-
rithms;thefirsttwoalgorithmssolvetherobot’skinematics,includingrangeconstraints,
singularity,andcollision-freetrajectories,andthethirdcycleoptimizestherobot’slocation
basedonthealreadyobtainedresults.
Inpalletizingapplications,suchanalysesensuretherobotcanaccesstheentirestack
footprintonthepallet,aswellaspick-uppointsontheconveyor. Additionally,eachof
the implemented algorithms can be adapted to optimize key parameters of interest in
thepalletizingtask,suchastotaltraveldistance,palletizingtime,andmaneuverability,
amongothers. Forinstance,themethodologyproposedin[35]addressesoptimalrobot
placement for the execution of diverse trajectories. This approach could be adapted to
minimizethenumberofmovementsrequiredinpalletizingtasks. Overall,theliterature
onmanipulatorplacementrevealsthatoptimizingtherobot’sbaselocation—thoughoften
treatedseparatelyfromtrajectoryplanning—formsanimportantfoundationforefficient
taskexecutioninautomatedpackingcells.
3. TrajectoryPlanning
Trajectoryplanningisconcernedwiththegenerationofafeasiblemotionfortherobot
thatmovesitthroughasequenceofposesorviapointsovertime.Thisinvolvesdetermining
notjustthegeometricpathinspacebutalsothetiming(velocityandaccelerationprofiles)
alongthatpath[36–39]. Atrajectoryistypicallydefinedineitherjointspace(anglesof
eachrobotjointasfunctionsoftime)ortaskspace(position/orientationoftheendeffector
asfunctionsoftime)oracombinationofboth. Accordingtoonedefinitionproposedby
FengandJia[40],trajectoryplanningspecifiesthevaluesofeachjointasafunctionoftime
suchthattherobotaccomplishesthedesiredmotion. Inessence,theplannermustfind

Robotics2025,14,55 6of23
acollision-freepathfromaninitialposetoatargetpose,thenassignatimelawtomove
alongthispathwhilerespectingthemanipulator’skinematicanddynamiclimits.
Forpick-and-placeoperationslikepalletizing,therobot’soverallmovementcanoften
besegmentedintodistinctphases: (1)movingtopickupaproduct(synchronizingwith
amovingconveyorifnecessary),(2)transferringtheproductthroughfreespaceathigh
speed,and(3)placingtheproductontothepalletwithcarefulpositioning. Eachphasecan
imposedifferentconstraints. Forexample,duringpickup,therobotmayneedtomatchthe
conveyorspeedtograsptheitem;duringtransfer,itmayacceleratetomaximumspeed
tominimizetraveltime;andduringplacement,itmustavoidcollisionswithpreviously
stackeditems,possiblymovingmoreslowlytoensureaccuracy.
Keyconsiderationsintrajectoryplanningincludetimeoptimality,energyefficiency,
andobstacleavoidance. Often,therearetrade-offsamongthesegoals. Aminimum-time
trajectorymaydemandrapidaccelerationsandjerking(rateofaccelerationchange),which
canexcitevibrationsorstressthemechanicalstructure. Ontheotherhand,atrajectory
optimizedforsmoothnessorenergymaynotbethefastest. Inindustrialpractice,planners
typicallygenerateanominalgeometricpath(viawaypointsoracontinuouscurve),then
performtimeparameterizationsubjecttovelocity,acceleration,andjerklimits. Shinand
McKay’sclassicwork[41]isanexampleoftime-optimaltrajectoryplanningalongapre-
definedpathunderactuatorconstraints. Severalstudieshaveaddressedminimum-time
pathplanninginrobotics. Messayetal. [42]proposedkinematiccalibrationalgorithmsto
minimizediscrepanciesbetweenthemanipulator’smathematicalmodelanditsgeometric
representation,incorporatingkinetic,dynamic,andpayloadconstraints—wheredynamics
involvetorque,power,andenergylimitsandkinematicsconsiderjointvelocity,acceleration,
andvibrationboundaries. Haddadetal. [43]introducedefficientschemesfortime-optimal
trajectoryplanning,whileLuanetal. [44]developedamaximum-speedalgorithmtailored
forserialpalletizingrobots,emphasizingreal-worldapplicability. Zhangetal. [45]formu-
latedtheproblemasaconvexoptimizationtogeneratesmooth,minimum-timetrajectories.
Similarly,XuandHong[46]devisedanoptimalpathplanningalgorithmtoenhanceef-
ficiencyandmitigatevibrations. Abu-Dakkaetal. [47]advancedaparallel-population
geneticalgorithmtocomputetime-optimaltrajectoriesformanipulators. Complementary
toplanning,trajectorytrackinghasbeenimplementedviadiversecontrollers;forinstance,
XiaoandYin[48]tackledtrackingcontrolunderunknowndynamicsandkinematics. While
suchoptimalcontrolformulationscanyieldminimumexecutiontimes,theyarecompu-
tationallyintensiveandmayrequiresimplifications(e.g.,trapezoidalvelocityprofilesor
piecewisepolynomialmotions)forpracticaluse.
Polynomial trajectory laws are widely used due to their computational simplicity
andguaranteeofsmoothness. Third-order(cubic)orfifth-order(quintic)polynomialsare
often employed to interpolate between waypoints with specified boundary conditions
(velocities and accelerations set to zero at end points, for instance). These polynomial
trajectoriesensurecontinuousvelocityandaccelerationprofiles. Higher-orderpolynomials
orsplinecurvescanfurtherensurecontinuityofjerk. Forexample,PiazziandVisioli[49]
presentedaglobaltrajectoryoptimizationproducingminimum-jerkmotionusingcubic
splines,effectivelycontrollingend-effectorvelocitiesandaccelerationstoreduceoverall
jerk. Suchspline-basedapproachesimprovemotionsmoothness,whichisimportantfor
high-speedpalletizing,whereabruptchangescouldtipordestabilizeacarriedpackage.
B-splinecurves,inparticular,arepowerfulfortrajectoryplanningbecausetheyofferlocal
control(adjustingonesegmentdoesnotgloballyaffecttheentiretrajectory)andcanenforce
smoothness constraints. B-splines have been used to shape and smooth robotic paths,
improvingtrackingperformanceandreducingcycletime. Theycanbeappliedineither
Cartesianorjointspace,andincreasingthesplinedegreeorthenumberofcontrolpoints

Robotics2025,14,55 7of23
providesgreatercontroloverthetrajectory. However,veryhigh-degreepolynomialscan
leadtonumericalissuesortrajectoryoscillations,soinpractice,amoderate-degreespline
ischosen.
Anessentialaspectoftrajectoryplanninginindustrialsettingsishandlingtherobot’s
dynamic limits while pushing for speed. Robots are asked to operate at ever higher
velocitiestoshortencycletimes,yetoperatingathighspeedcandegradeprecisionand
repeatability, in addition to increasing wear on joints and motors. Therefore, trajectory
plannersoftenincorporateconstraintsonaccelerationandjerktoavoidexcitingvibrations
intherobot’sstructure. Ahigh-speedtrajectorymustbecarefullytime-scaledsoasnotto
exceedtherobot’storquelimitsorcauseexcessiveend-effectorswaywhencarryingaload.
ResearchbyGasparettoetal. [50]notesthatadvancedmotionplanningisneededtoallow
robotstoachievehigherspeedswithoutcompromisingmechanicalintegrity. Inpalletizing,
thismeanstherobotshouldmoveasfastaspossiblebetweenpicksandplacementsbutwith
amotionprofilethattherobotcanphysicallyrealizewithoutovershootingoroscillation.
Another critical consideration is obstacle avoidance. In a palletizing scenario, ob-
staclesmayincludethepalletitself,apalletrack,andthestackofalreadyplaceditems
(whichgrowsovertime). Thetrajectoryplannermustensurethemanipulatordoesnot
collidewiththeseobjectsatanypoint. Thiscanbeaddressedbyplanningpathsinthe
configurationspacethatsteerclearofobstacleconfigurationsorbyaddingintermediate
viapointsabovethestack. Someworkshaveintegratedcollisionavoidancedirectlyinto
trajectory optimization. For instance, one can include potential field forces or collision
penaltytermsinanoptimalcontrolframeworktopushthetrajectoryawayfromobstacles.
ArecentapproachproposedbyTonanetal. [51]demonstratedtrajectoryplanningforan
underactuated2-DOFmanipulatorthatincludesviapointsspecificallytoavoidobstacles,
effectivelyachievingcollision-freemotion,evenwitharobotthathasfeweractuatorsthan
degreesoffreedom. Byexploitingtheconceptofdifferentialflatness,theyparameterized
thetrajectorywithhigh-orderpolynomialsthroughkeyviapoints,enablinganunderactu-
atedarmtomaneuveraroundobstaclessimilarlytoafullyactuatedrobot. Thisillustrates
howadvancedanalyticalmethodscanbroadenthescopeoftrajectoryplanning(inthis
case,tounderactuatedsystems)whilestillsatisfyingtypicalindustrialconstraints.
Insummary,trajectoryplanningprovidesthetime-parameterizedreferencethatthe
robot’scontrolsystemwilltrack.Itmustbalancecompetingobjectivesofspeed,smoothness,
precision,andsafety. Inthenextsection,wereviewprominentpathplanningandtrajectory
generation methods from the literature, ranging from classic graph search algorithms
to modern learning-based techniques, and we discuss how each can be applied to the
palletizingusecase.
4. PathPlanningMethods
Avarietyofalgorithmicmethodshasbeendevelopedtoplanpathsandtrajectoriesfor
roboticmanipulators. Here,wesurveythemaincategories,includinggraph-basedsearch
algorithms,sampling-basedplanners,artificialpotentialfieldmethods,splineinterpolation
techniques,andlearning-basedapproaches. Weemphasizehowthesemethodscontribute
totheoveralltrajectoryplanningproblemandtheirrelevancetopalletizingtasks. Table1
providesacomparativesummaryofthestrengthsandlimitationsofeachmethod.
4.1. GraphSearchAlgorithms(Grid-BasedPlanning)
Afoundationalpathplanningapproachinvolvesdiscretizingtherobot’sworkspace
orconfigurationspaceintoagridandsearchingforthelowestcostpath,asexemplified
by the A∗ algorithm [52]. A∗ efficiently guides the search from a start state to a goal
using heuristics, guaranteeing grid-based optimality for metrics like path length and

Robotics2025,14,55
8of23
time(seeFigure3). Whileeffectiveforlow-dimensionalspaces(e.g.,planarend-effector
A∗
motion), faces scalability challenges in high-DOF manipulators due to the curse of
dimensionality. Finelydiscretizedgridsexacerbatecomputationalcosts,andtheresulting
piecewise linear paths often require smoothing for practical execution. Despite these
limitations,A∗ remainsviableforpalletizingtasksreducibletolowerdimensionalsearches
(e.g.,gantrycranemotionorpick-and-placesequencing),sometimesintegratedwithsensor-
updatedoccupancygrids. Modifiedversions,suchasthoseproposedin[53,54],address
computationalefficiencyandadaptability.
Table1.Pathplanningandoptimizationmethodsforroboticpalletizing.
| Method   | KeyIdea          |           | Advantages            |               | Limitations   |                 | Elements |            |
| -------- | ---------------- | --------- | --------------------- | ------------- | ------------- | --------------- | -------- | ---------- |
|          |                  |           |                       |               | Computational | cost            |          |            |
|          | Graph search     | on a grid | Guaranteedoptimalpath |               |               |                 |          |            |
|          |                  |           |                       |               | grows         | exponentially   | Grid map | and vision |
| A*Search | using heuristics | to find   | onagrid;              | effectivewith |               |                 |          |            |
|          |                  |           |                       |               | with          | dimensionality; | sensor   |            |
|          | theshortestpath  |           | goodheuristics        |               |               |                 |          |            |
grid-constrainedpaths
|     | Randomly       | samples    |                         |     |              |          |     |     |
| --- | -------------- | ---------- | ----------------------- | --- | ------------ | -------- | --- | --- |
|     |                |            | Fastplanninginstaticen- |     | Trajectories | may need |     |     |
|     | collision-free | configura- |                         |     |              |          |     |     |
PRM vironments;reusablefor smoothing;notsuitedfor Localplanner
tionstobuildaroadmap
|     |     |     | multiplequeries |     | dynamicenvironments |     |     |     |
| --- | --- | --- | --------------- | --- | ------------------- | --- | --- | --- |
graph
|     |               |                 | Effective   | in high-         |                      |             |                     |     |
| --- | ------------- | --------------- | ----------- | ---------------- | -------------------- | ----------- | ------------------- | --- |
|     | Incrementally | grows           | a           |                  |                      |             |                     |     |
|     |               |                 | dimensional | spaces;          | Paths often          | suboptimal; |                     |     |
| RRT | random        | tree toward un- |             |                  |                      |             | Randomtreestructure |     |
|     |               |                 | good        | for single-query | noinfeasibilityproof |             |                     |     |
exploredspace
planning
|     | Goalasattractorandob- |     | Computationally | light; | Pronetolocalminima;no |     |     |     |
| --- | --------------------- | --- | --------------- | ------ | --------------------- | --- | --- | --- |
APF staclesasrepellersinthe real-time reactive capa- globaloptimalityguaran- Distancesensors
|     | potentialfield |     | bility           |       | tee     |                |     |     |
| --- | -------------- | --- | ---------------- | ----- | ------- | -------------- | --- | --- |
|     |                |     | Fast computation | after | Require | large training |     |     |
Learnpathgenerationor
NeuralNetworks training; no explicit datasets;interpretability Trainingdatasets
controlpoliciesfromdata
|          |               |            | modelneeded       |        | challenges            |             |             |           |
| -------- | ------------- | ---------- | ----------------- | ------ | --------------------- | ----------- | ----------- | --------- |
|          | Piecewise     | polynomial | Continuous        | veloc- |                       |             |             |           |
|          |               |            |                   |        | Not standalone;       | strug-      | High-degree | polynomi- |
| B-Spline | curves        | for smooth | ity/acceleration; | local  |                       |             |             |           |
|          |               |            |                   |        | gleswithsingularities |             | als         |           |
|          | interpolation |            | adjustability     |        |                       |             |             |           |
|          | Optimizes     | trajectory |                   |        | Complex               | implementa- |             |           |
Reducesenergyuseand
Energy-Optimal to minimize energy tion; may increase cycle Simulationmodels
mechanicalwear
|     | consumption |     |     |     | time |     |     |     |
| --- | ----------- | --- | --- | --- | ---- | --- | --- | --- |
Figure3.SchematicoftheA*algorithm.
4.2. Sampling-BasedMethods(ProbabilisticPlanning)
TheProbabilisticRoadmapMethod(PRM)andRapidly-exploringRandomTree(RRT)
algorithms offer distinct advantages for robotic palletizing tasks. The PRM constructs

Robotics2025,14,55 9of23
a collision-free roadmap through random sampling of the configuration space, which
isparticularlyeffectiveforpalletizinginknownenvironmentswhereobstaclelocations
arepredetermined. Whilecomputationallyintensiveforhigh-DOFmanipulators,recent
enhancements, likeenvironmentpre-learningandhybridPRM–reinforcementlearning
approaches,haveimproveditsefficiencyforpalletizingapplications.Thealgorithm’sabil-
itytofindoptimalpathsusinggraphsearchmethods(e.g.,A*)makesitsuitableforthe
optimizationofpalletizingsequenceswhencombinedwithpost-processingsmoothing
techniques. Conversely,RRTexcelsindynamicpalletizingenvironmentsthroughitsincre-
mentaltreegrowthmethod. Itsstrengthliesinreal-timeadaptability,whichisparticularly
valuablewhenhandlingvariablepalletloadsormovingobstacles,althoughpathquality
mayrequirerefinement[55,56].Thealgorithm’snaturalbiastowardunexploredregions
(Voronoibias)provesadvantageouswhenpalletizinginclutteredworkspaces.
4.3. ProbabilisticRoadmapMethod(PRM)
ThePRMconstructsacollision-freeroadmapthroughrandomsamplingoftherobot’s
configurationspace,whichisparticularlyeffectiveinknownenvironmentswherepallet
locationsandobstaclesarepredetermined[57]. Themethodrandomlygeneratesnumerous
validconfigurations(nodes)andconnectsthemwithfeasiblemotions(edges)toforma
graph;agraphsearch(e.g.,DijkstraorA*)isthenemployedonthisroadmaptofindan
optimalpathfromthestarttothegoal(seeFigure4). ThePRMiscomputationallyintensive
forhigh-DOFmanipulators,butseveralenhancementshaveimproveditsefficiencyfor
palletizing applications. For example, environmental pre-learning techniques can bias
samplingusingpriorknowledgeoftheworkspace[58],andhybridapproachescombinethe
PRMwithreinforcementlearningtoguidesamplingincomplexpalletlayouts[59]. Various
otherimprovementsandvariantsofthePRMhavebeendiscussedintheliterature[60,61],
aimingtoaccelerateroadmapconstructionandsolutionfinding.Notably,oncearoadmapis
built,classicalgraphsearchalgorithmscanbeusedtofindtime-optimalorenergy-optimal
paths through it, making the PRM suitable for optimizing palletizing sequences when
pairedwithpost-processingsmoothing. Inpractice,plannersoftenintegratethePRMwith
a smoothing stage (e.g., fitting a spline through the roadmap waypoints) to ensure the
piecewisepathcanbeexecutedfluidlyonthemanipulator.
4.4. RapidlyExploringRandomTrees(RRT)
RRTalgorithmsexcelindynamicorunstructuredpalletizingenvironmentsthrough
anincrementaltree-growthstrategy. RRTincrementallybuildsatreeintheconfiguration
spacebyextendingtowardrandomsamples. Ateachiteration,givenarandomlysampled
configuration(q ),thetreefindsitsnearestnode(q )(accordingtoadistancemetric)
rand near
andaddsanewnodeinthatdirection:
(q −q )
q = q +ϵ rand near , (1)
new near |q −q |
rand near
whereϵisafixedstepsize(seeFigure5). Byiteratingthisprocess,RRTrapidlyexploresthe
spaceandeventuallyfindsacollision-freepathtothegoal(whichcanthenbesmoothed
forexecution). Theseexamplesillustratetwocoreparadigms—splineinterpolationand
sampling-basedsearch—thatunderliemanypalletizingtrajectoryplanners. Startingfrom
the initial robot state, an RRT rapidly expands by stochastically sampling the configu-
ration space and extending toward unexplored regions. The key strength of RRT is its
real-timeadaptability—itcanquicklyfindafeasibleroutearoundnewlydetectedobstacles
or changing stack geometries—which is particularly valuable when handling variable
palletloadsormovingobstaclesonaconveyor. Thetrade-offisthattherawpathspro-

Robotics2025,14,55 10of23
ducedbyRRTtendtobejaggedorsuboptimal,oftenrequiringrefinementorsmoothing
beforeexecution[55,56].Thealgorithm’snaturalVoronoibiastowardunexploredspaceis
advantageousinclutteredworkspaces,asitefficientlyprobesfreeregionsofthepalletizing
cellthatmightbemissedbydeterministicplanners.
Insummary,thesesampling-basedplannersaddresscriticalpalletizingrequirements
incomplementaryways. ThePRMprovidesanoffline-optimizedroute(idealforrepetitive
tasksinstaticsetups),whileRRToffersonlineadaptabilitytodynamicconditions. Recent
RRTvariants,suchasbidirectionalRRTandRRT-Connect[62,63],andoptimizedsampling
strategies[64]havefurtherimprovedplanningspeedandpathquality,makingRRTmore
practical for high-speed palletizing. Moreover, combining the PRM or RRT with other
techniquescanyieldbetteroverallperformance. Forexample,integratingalocalartificial
potential field for reactive obstacle avoidance or smoothing the final trajectory with a
B-splineblendallowstheplannertosimultaneouslyoptimizemultiplecriteria(pathlength,
executiontime,andenergyuse)[59]. Theseintegrationsarefrequentlytunedtopalletizing-
specificconstraints(likemaintainingabox’sorientationoravoidingpreviouslystacked
items), highlightingtheflexibilityofsampling-basedmethodstobecustomizedforthe
palletizingdomain.
Figure4.PRMframeworkforpalletizingpathplanning.
4.5. ArtificialPotentialFieldMethods
TheArtificialPotentialField(APF)methodprovidesreal-timepathplanningbymod-
elingrobotmotionasparticledynamicsinavirtualforcefield. Inthisframework,attractive
forcesdrawtherobottowardpalletizingtargetswhilerepulsiveforcesdeflectitfromobsta-
cles,enablingreactivecollisionavoidance,whichiscrucialforhigh-speedpalletoperations.
The method’s computational efficiency stems from local force calculations, permitting
high-frequency trajectory adjustments, which are particularly valuable when handling
unexpectedobstacleslikefallenboxes. However,traditionalAPFmethodssufferfromlocal
minimatraps,whereforceequilibriahaltprogress,whichisasignificantlimitationindense
palletconfigurations.
Enhanced variants like the Velocity Potential Field (VPF) [65] address these short-
comings by incorporating motion dynamics to escape stagnant points. For palletizing,
APFexcelsinfinetuningend-effectorapproachesbetweentightlypackedboxes,whereits
fastresponseenablesgentle,collision-freeplacements[66]. Whileinsufficientforglobal
planningduetominimaissues,modernimplementationscombineAPFwithhigher-level
planners: globalalgorithms(e.g.,RRT)handleoverallpathplanning,whileAPFmodules
managereal-timeobstacleavoidanceandplacementprecision[67,68].Thishybridapproach
leveragesAPF’ssimplicityforlocalrefinementswhilemitigatingitstopologicallimitations.

Robotics2025,14,55 11of23
Figure5.RRTexplorationinpalletizingconfigurationspace.
4.6. Learning-BasedApproachesandNeuralNetworks
Machinelearningtechniques,especiallyneuralnetworksandreinforcementlearning,
havebeenincreasinglyappliedtorobotpathplanningandcontrolinrecentyears. These
learning-basedapproachesaimtoallowtherobottoimproveitsplanningperformance
through experience or to generalize from examples rather than relying solely on hard-
codedmodels.
Early works on neural networks for manipulators often focused on solving sub-
problemslikeinversekinematicsorredundancyresolution. Forexample, Jinetal. [69]
providedacomprehensivesurveyofneuralnetworkapproachesforrobotmanipulator
controlandplanning.Neuralnetworkshavebeenusedtolearninversekinematicmappings
or to compute joint trajectories that satisfy certain criteria. In one study, Li et al. [70]
applied a primal dual neural network to solve a constrained optimization problem for
motioncontrol,effectivelycomputinganoptimalpaththatminimizesanL norm-based
1
cost in real time. Similarly, Xie et al. [71] designed a neural network-based scheme for
repetitive motion planning (RMP) in redundant manipulators. Their dynamic neural
networkcontrollerhandlesnonconvexconstraintsandcaniterativelyimprovetheplanned
trajectoryfortasksthatrepeat,whichisrelevantforrepetitivepalletizingcycles.
ReinforcementLearning(RL)hasemergedasaparticularlypromisingapproachfor
trajectoryplanningandcontrol. Inreinforcementlearning,therobot(oranagentcontrol-
lingtherobot)learnsapolicyforactions(e.g.,jointvelocitycommands)byinteractingwith
theenvironmentandreceivingfeedbackintheformofrewardsorpenalties. Overtime,
theagentcanlearnstrategiesthataredifficulttoderiveanalytically. Deepreinforcement
learningmethodshavebeenappliedtomanipulatorsforpick-and-placetaskswithnotable
success. For instance, Park et al. (2007) [59] demonstrated that combining RL with a
sampling-basedplanneryieldsefficientreal-timeplanninginuncertain,dynamicenviron-
ments. Morerecently,IqdymatandStamatescu(2025)[72]showedthatintegratingdeep
RLwithoptimalcontrolcansignificantlyimprovebothprecisionandenergyefficiencyfor
asix-DOFindustrialmanipulatorinawarehousepick-and-placescenario. Thiskindof
resultispromisingforpalletizing,asitsuggeststhatlearningalgorithmscanautonomously
discovertrajectoriesthatoptimizemultipleobjectives(time,energy,andaccuracy)inways
thathand-tunedtrajectoriesmightnot.
However, learning-based methods also have challenges. Training requires a large
numberoftrialsorqualitydata,andinrobotics,thatoftenmeansextensivesimulationor
riskingtrialsonrealhardware. Safetyisamajorconcern—anagentexploringtrajectories
might collide with objects or exceed joint limits if not carefully constrained. There are
ongoingdevelopmentsinsafereinforcementlearningtoaddressthis,suchasaddingsafety

Robotics2025,14,55 12of23
layersorconstrainthandlingwithinthelearningprocess. Dataefficiencyisanotherissue:
methodslikeimitationlearningandtheincorporationofmodelknowledge(e.g., using
model-predictivecontrolwithlearning)arebeingexploredtoreducetheamountoftrial
anderrorneeded.
Inthecontextofpalletizing,onecouldenvisionalearning-basedsystemthatobserves
theoutcomesofitspackingattempts(stackstability,timepercycle,andenergyused)and
gradually refines its motions. Over many pallets, it might learn subtle improvements,
likehowtoslightlyadjustitsapproachangletoplaceaboxwithoutdisturbingneighbors
or how to sequence picks to minimize energy use. Some recent works have combined
vision, planning, andlearningtocreateintelligentpalletizingrobotsthatimproveover
time [1,73]. The current literature indicates that while purely learning-driven planners
arestillemerging,theyaresettocomplementandenhanceclassicalmethodsbyhandling
complexityanduncertaintiesthatarehardtomodelexplicitly.
4.7. Spline-BasedTrajectoryGeneration
Splineinterpolationmethods,includingB-splinesandotherpolynomialsplines,are
widelyusedtogeneratesmoothtrajectoriesformanipulators. Spline-basedplanningsits
somewhere between pure path planning and control—it takes a coarse path or a set of
waypointsandproducesarefinedtrajectorythatarobotcanfollowsmoothly.
B-splines(basissplines)arepiecewisepolynomialfunctionsdefinedoverasequence
ofcontrolpoints. Thetrajectoryofdegreedcanbedefinedbycontrolpoints(P ,P ,...,Pn)
0 1
andbasisfunctions(N (u))onanormalizedtimeparameter(0≤ u ≤1):
i,d
n
∑
x(u) = N (u)·P , (2)
i,d i
i=0
whichguaranteesupto Cd−1 continuityatthecontrolpointsandyieldsasmoothpath
throughtheviapoints.
Intrajectoryplanning,thecontrolpointscanbechosentoguidetherobotthrough
certainpositions,andtheB-splineensuresasmoothcurvethatinterpolatesorapproximates
thosepoints. OnemajorbenefitofB-splinesisthattheyproducetrajectorieswithcontin-
uoushigher-orderderivatives(velocityandacceleration), whichiscrucialforavoiding
excitingvibrationsinarobot. Theyalsoallowforlocaladjustability: movingonecontrol
pointmainlyaffectsonlytheneighboringsegmentsofthetrajectory,nottheentirepath.
Accordingtorecentstudies,usingcubicB-splinestosmoothaplannedpathcanimprove
tracking performance and reduce motion time. For example, Yu et al. [74] suggested
learninganenvironment’slayoutfirsttogenerateaninitialcollision-freepath,followedby
pathsmoothingwithacubicB-splineforexecution. Thisisveryapplicabletopalletizing,
wheretheinitialpathmightcomefromadiscretealgorithmorheuristic(likeplacingabox
inacalculatedposition);then,asplineisfittedtoensurethemotionisgentleandfast.
Spline trajectories can be generated in either joint space or task space. Joint-space
splineshavetheadvantageofinherentlyrespectingjointlimitsifthecontrolpointsare
chosenappropriately,andtheyavoidsingularityissues. Task-spacesplines(likeCartesian
splinesfortheendeffector)candirectlyencodestraight-linemovesorspecificpathshapes
intheworkspace,whichmightbeneededtoavoidobstaclesoradheretoprocessconstraints
(e.g.,keepingaboxlevel).Often,plannersuseahybrid:theygenerateacoarsecollision-free
Cartesianpath(viawaypointsaroundobstaclesoroverstacks),thentime-parameterizeit
withajoint-spacesplinethatachievesthosewaypoints.
Therearealsooptimalspline-basedapproaches. WementionedtheworkbyPiazzi
andVisioli[49], whousedintervalanalysistofindaminimum-jerktrajectoryviacubic
splines. Otherresearchershaveformulatedmulti-objectiveoptimizationswherecontrol
pointsofasplineareadjustedtominimizetimeandenergyuseortoavoidobstacleswhile

Robotics2025,14,55 13of23
keepingthesplinesmooth[75–77]. Theseapproachesturntrajectorygenerationintoan
optimizationproblemoverthesplineparameters,whichcanbesolvedbytechniqueslike
sequentialquadraticprogrammingorevengeneticalgorithms.
Inpalletizing,splinemethodsareextremelyusefulingeneratingthefinaljointcom-
mandsfortherobot.Forinstance,onceasequenceofpick-and-placepositionsisdetermined
(theorderinwhichboxeswillbeplacedandtheirtargetcoordinates),aspline-basedtrajec-
toryplannercangenerateaseamlessmotionthatconnectsallthesepointswithminimal
idletimeandsmoothaccelerations. Thiscouldinvolveblendingsegmentsofstraight-line
motion (to extract and insert boxes vertically) with swift curved motions in free space.
B-splineblendingallowstherobottonotcompletelystopatintermediatepoints,saving
timebyroundingoffthecornersofthemotion,sotospeak,whilestillpassingnearthose
importantviapoints. Thepurposeoftheconstraintistoensurethattheseblendedmotions
donothitanyobstacles—achallengethatcanbemetbycarefulplacementofcontrolpoints
orbyimposingcollision-avoidanceconstraintsinsplineoptimization.
4.8. Energy-EfficientTrajectoryOptimization
Energyefficiencyhasgainedincreasingattentioninrobotictrajectoryplanning,espe-
ciallyforoperationslikepalletizingthatinvolverepetitivemotions. Anenergy-efficient
trajectoryisonethatcompletesthetaskwithminimalenergyconsumption,whichnotonly
reducesoperatingcostsandenvironmentalimpact(lowerelectricityusageandlowerCO
2
emissions)butcanalsoreducewearontherobot. Energyconsumptionforaroboticmanip-
ulatorisaffectedbyfactorssuchasthemassesmoved(includingthepayload),acceleration
anddecelerationprofiles,andthedurationsofmotionandidletimes.
Severalapproacheshavebeenexploredtoplanlow-energytrajectories. Onestraight-
forwardapproachistominimizepeakaccelerationsandvelocities,sincerapidaccelerations
generallyrequirehighmotortorquesandcurrents. Anotherapproachistoexploitgrav-
ityanddynamics. Forexample,motionscanbeplannedtorecuperateenergy(through
regenerativebrakingonmotors)oravoidfightingagainstgravitymorethannecessary. In
pick-and-placetasks,schedulingandtrajectorygohandinhandforenergyoptimization,
e.g.,placingheavierobjectslowerorsoonercouldreducetherobot’senergyexpenditure
overtheentirestackingprocess.
Numerousstudieshaveformulatedtrajectoryplanningasanoptimizationproblem
with an energy-related cost function. Srinivas and Javed [78,79] provided a review of
variousoptimizationapproachesaimedatimprovingtheenergyefficiencyofserialma-
nipulators. Specificcasestudiesonpalletizingrobotsshowthatpoint-to-pointtrajectory
planning(PTP)canbetunedforenergysavings. Forinstance,onemightextendthemotion
durationslightly(sacrificingabitofcycletime)ifitallowsmotorstooperateinamore
efficientregimeoravoidsharpaccelerations,therebyusinglessenergyoverall. Techniques
like iterative learning control have been used to optimize input shaping over repeated
cycles to converge to lower energy usage without deviating from the required motion
profile[80–87].
ApracticalexamplewasprovidedbyPaesetal. [88],whogeneratedenergy-optimal
trajectories through intelligent programming of the robot’s velocity profile, achieving
measurableenergyreductionspercycle. Vidussietal. [89]introducedanenergyanalysis
frameworkthatincludesaperformanceindexrelatingarobot’senergyconsumptiontoits
inertiaellipsoid(essentiallycapturinghowtherobot’sconfigurationaffectstherequired
effort). Byevaluatingsuchindices, aplannercanchooseconfigurationsandpathsthat
inherentlyfavorlowerenergyuse(forinstance,avoidingconfigurationswheretherobotis
stretchedoutandtorquerequirementsarehigher).

Robotics2025,14,55 14of23
Anotherlineofresearchcombinesenergyoptimizationwithotherobjectives. Multi-
objectiveoptimizationcanseekatrade-offbetweentimeandenergyuse. Forexample,
usingaPareto-optimalapproachorevolutionaryalgorithmslikeNSGA-II,onecanobtain
asetoftrajectoriesrangingfromfastest(higherenergy)tomostenergy-efficient(slower),
thenselectasuitablecompromise[90]. Inindustrialsettings,often,thefastestcyclethat
doesnotexceedagivenenergythreshold(orthatstaysbelowatemperaturethresholdfor
motors)isdesired,sosuchatrade-offanalysisisvaluable.
Forpalletizing,energy-efficientplanningmightalsoconsiderthelayoutoftasks—not
justhowtomovebutwhatsequencetomovein. Researchhasshownthateventhepath
order (which box to place next) can affect energy usage, essentially coupling schedul-
ing with trajectory planning. Integrating these decisions is complex but has potential
foroptimization.
Asummaryofthemainaspectsofthebasicalgorithmsforplanningoroptimizingthe
trajectoryofaroboticmanipulatorispresentedinTable 1.
4.9. ExperimentalSetupsandPerformanceMetrics
Anumberofcitedstudieshavevalidatedtrajectoryplanningapproacheswithrealor
simulatedpalletizingexperiments,emphasizingvariousperformancemetrics. Common
performanceindicesincludethecycletimeperpickandplace(whichdeterminesthrough-
putinboxesperhour),energyconsumptionoftherobotduringmotion,peakoraverage
accelerations(relatedtomechanicalstressandvibration),andprecisionofplacement[15].
Standardmethodologiesformeasuringandcomparingthesemetricsinroboticsystems
weresurveyedbyPatelandSobh[16]. Here,wesummarizekeyexperimentalfindings
fromtheliterature.
Moreno et al. [15] identified throughput, energy per cycle, and placement accu-
racyascriticalmetricsforpalletizingrobots. Intheirevaluations,optimizedtrajectories
achieved faster cycle times without increasing energy usage beyond acceptable limits,
illustratingtheimportanceofsmoothmotionprofiles. Hwangetal. [17]demonstrated
thatforaseven-DOFserialmanipulator,carefullyoptimizedjointtrajectoriescanreduce
energyconsumptionbyminimizingunnecessarymotionswhilestillmeetingthetask’s
timeconstraints—animportantresultforheavy-payloadpalletizing, whereenergyeffi-
ciencyandheatbuildupareconcerns. Zhuetal. [6]implementedacompletepalletizing
system(combiningvision-baseddetection,packingsequenceoptimization,andtrajectory
planning)andreportedsignificantimprovementsinthroughputoverbaselinemethods;
intheircasestudy,theintegratedapproachallowedforadaptivepickingandstackingof
mixedboxeswithvirtuallyzerocollisions,improvingthepalletizingratebyanorderof
magnitudecomparedtomanualplanning. Sakamotoetal. [91]focusedonmotionplanner
performanceand,inexperiments,showedthattheirreusableroadmapplannersgreatly
decreasecomputationtimeonrepeatedpalletizingtasks: inatrialof30pick-and-place
cycles,astandardPRMfailedtofindapath30%ofthetimeinaclutteredscenario,whereas
theirreuse-basedPRMsucceededin100%oftrialsandkeptplanningtimesbelow0.4s
forallsubsequentpicks. Thistranslatedtoahighersustainedthroughput,sincetherobot
spentlesstimewaitingforanewtrajectorytobeplanned. Similarly,XuandHong[92]
developedanS-curvetime-optimaltrajectoryforapalletizingrobotunderkinematiccon-
straints and verified on hardware thatit significantly reduced cycle time andvibration
compared to a non-optimized motion—the robot could move faster between pick-and-
placepositionswithoutexcitingdangerousoscillations,improvingtheoverallpalletizing
speed. Acrossthesestudies,theconsensusisthatcarefullyplannedtrajectories(whether
optimizedofflineoradjustedonline)candramaticallyenhancepalletizingperformance.
Thechoiceofmetricoftendependsontheuse-case: automotiveandfast-movingconsumer

Robotics2025,14,55 15of23
goodsindustriesprioritizecycletime(boxesperminute),whereascontextslikefoodor
pharmaceuticalpalletizingmightemphasizegentlehandling(lowerimpactforces)and
energyefficiency. Byexaminingmetricsliketheseinexperimentalsettings,researchers
canquantitativelydemonstratethebenefitsofadvancedtrajectoryplanningalgorithmsfor
palletizingapplications.
5. ResearchGapsandFutureDirections
Robotictrajectoryplanningmethodologieshaveevolvedgreatlyoverthepastdecades,
anddifferentapproachestendtoexcelunderdifferentpalletizingconditions. Inthe1980s,
classicaloptimalcontrolformulationswereappliedtomanipulatormotion—forexample,
solvingforminimum-timeorminimum-energyjointtrajectoriesalongpredefinedpaths[41].
Theseearlymethodsassumedwell-structuredtasks(fixedstart/endpointsandnomoving
obstacles) and proved effective for straightforward palletizing scenarios where a robot
repeatedlymovesidenticalobjects.Undersuchconditions,simpletime-optimalpolynomial
profilesorbang–bangcontrolcouldminimizecycletime. Bythe1990s,researchersbegan
addressingmorecomplexenvironments;techniqueslikeartificialpotentialfieldsemerged
toenablereal-timeobstacleavoidance,whichwasparticularlyusefulaspalletizingrobots
started to handle irregular stacking patterns in semi-structured warehouses. However,
potentialfieldplannerscouldgetstuckinlocalminimaifapalletconfigurationwasdensely
packed,highlightingthatnosinglemethodworkeduniversally.
The late 1990s and early 2000s saw the rise of graph search and sampling-based
planners. Grid-based algorithms (e.g., A∗ variants) were adapted for robotic arms, but
the high dimensionality of a six-DOF or seven-DOF palletizer made exhaustive search
impractical,exceptforsimplifiedsub-tasks. Thisledtoprobabilisticalgorithms—notably,
the PRM [57] and RRT [55]—which trade completeness for efficiency. These methods
broughtaboutsignificantadvantagesforpalletizinginmoreunpredictablesettings: aPRM
couldpre-computeroadmapsforaknownworkspace(usefulifthepalletlayoutisstatic
for long periods), while RRT could quickly re-plan on the fly when boxes shift or new
obstacles(likeaforkliftintrusion)appear. Duringthe2010s,attentionshiftedtooptimality
andlearning. Researchersintroducedmulti-objectiveoptimizationsthatbalancespeed,
energy,andsmoothness—animportantdevelopmentforpalletizing,sincethepaththat
isfastestmayalsocausewearorrequireexcessivepower. Forinstance,techniqueswere
developedtoadjustsplinecontrolpointsortimescalingtominimizebothmotiontimeand
energyconsumption[92]. Atthesametime,learning-basedapproachesgainedtraction:
reinforcementlearningandimitationlearninghavebeenexploredtoallowrobotstolearn
palletizing strategies from experience [59]. These are promising approaches for highly
unstructuredscenarios(e.g.,aservicerobotthatmustadapttoarbitrarypalletpatterns),
buttheytypicallyrequiremanytrainingexamplesandcarefultuningtoensuresafetyand
reliabilityonhardware.
Overall, this historical trajectory shows that no one-size-fits-all solution exists in
trajectoryplanning;instead,eachmethodhasspecificapplicabilityconditionsinpalletizing.
Classical polynomial and spline methods are extremely efficient for regular, repetitive
palletizingtaskswheretheenvironmentisknownapriori—theyleveragesmoothmotion
generationandlowcomputationtimebutarelessadaptabletochange. Sampling-based
plannershandlechangingoruncertainenvironmentswellandare,thus,employedwhen
thepalletcontentsorsurroundingsvary(atthecostofextrasmoothingstepstoimprove
pathquality). Optimization-basedplanners(includingmodernmodel-predictivecontrol
andhybridoptimizationalgorithms)arefavoredwhenfinetuningofperformancemetrics
isneeded—forexample,inhigh-throughputpalletizingcellswhereevenasmallreduction
incycletimeperpickcanyieldhugegainsoverthousandsofcyclesorinenergy-critical

Robotics2025,14,55 16of23
operations where minimizing peak power usage prolongs robot life. Learning-based
methods,whilestillemerging,arebeginningtoshowvalueinscenarioswheretherobot
mustgeneralizetonewpalletarrangementsorcollaboratewithhumans; insuchcases,
theabilitytoimproveperformancewithexperiencecancomplementthefixedstrategies
derivedfromclassicalalgorithms.
Eachapproach’shistoricalcontextinformsitsbestuse: whatwasonceatheoretical
optimalcontrolsolutionisnowapracticalcomponent(forinstance,usedtotime-optimize
asegmentofanRRTpath),andwhatwasonceanexperimentallearningalgorithmmight
soon become a standard feature in next-generation palletizing robots. The palletizing
domaincontinuestodrivesuchinnovations,asevidencedbytheincreasingintegrationof
thesediverseplanningtechniquesinbothresearchprototypesandindustrialsolutions.
However,despitethericharrayofmethodsdemonstratedintheliteratureformanip-
ulatortrajectoryplanning,severalcriticalchallengesremain,particularlyintherealmof
high-mixpalletizingandservice-orientedautomation. Inthissection,wehighlightsome
openissuesandsuggestdirectionsforfutureresearch.
1. Real-time adaptation and autonomy: Many advanced planning algorithms (e.g.,
optimalcontrolorglobaloptimizationmethods)arecomputationallyintensiveand
runoffline. Inadynamicpackingenvironment,thesystemshouldadaptontheflyto
changingconditions—suchaslast-minutepackageadditionsorashiftingload.Future
researchshouldfocusonreal-timetrajectoryplanningframeworksthatcanre-plan
or adjust mid-course without stopping the operation. This might involve hybrid
approaches(combiningfastreactiveplanningwithsloweroptimalrefinements)or
leveragingofthespeedoflearning-basedmethodstoupdateplansonline. Ensuring
stabilityandsafetyduringsuchreal-timere-planningisakeychallenge.
2. Integratedtaskandmotionplanning: Inpalletizing,decidingwhattodo(taskplan-
ning,i.e,whichitemtopicknextandwheretoplaceit)istightlycoupledwithhow
to do it (motion planning, i.e., planning the trajectory to execute that pick/place).
However,mostcurrentresearchtreatstheseseparately. Thereisaneedforintegrated
planningthatconsidersthesequenceofactionsandtrajectoriesjointlyforoptimiza-
tion. Forexample,analgorithmcouldevaluatetheestimatedenergyortimecostof
placingaboxinvariouscandidatelocationsandchoosetheplanthatminimizesa
globalobjective. Thisintegrationleadstoacombinatorialexplosionincomplexity,
butsmarterheuristicsordecompositiontechniques(or,again,learningapproaches
thatcanapproximatethesolution)couldmakethistractable. Someinitialworkalong
theselines,particularlyusingILPforsequencing,combinedwithmotionplanning,is
promisingbutcanbeexpandedtomorecomplexscenarios(multiplerobots,random
arrivalofitems,etc.).
3. Safetyandcollisionavoidanceinlearning-basedsystems: Asreinforcementlearning
andotherAI-drivenmethodsbecomemoreprevalent,ensuringsafetyduringboth
training and deployment is paramount. Robots learning their own motions must
beconstrainedsotheydonotdamagegoodsorthemselves. Futureresearchmight
exploresafeexplorationtechniquesinRL,wheretheagentisguidedbyabaseline
planner(forinstance,anRRTorasplineplanner)andonlyallowedtomakemodest
deviationsthatareknowntobesafe. Anotherconceptinvolvesaddingasafetylayer
thatmonitorsandoverrideslearnedpoliciesifapotentialcollisionorlimitviolationis
predicted. DevelopingverifiablysafeRLformanipulatorsinindustrialsettingsisan
importantdirection,whichwilllikelyinvolveinterdisciplinaryworkbetweencontrol
theoryandmachinelearning.
4. Handlingofuncertainties: Inapackingcell,uncertaintiesabound—theexactweight
ofaboxmightdeviate,thebox’scontentsmayshift,sensornoisecanaffectperception

Robotics2025,14,55 17of23
of positions, etc. Robust trajectory planning that can tolerate or compensate for
uncertaintiesisanopenproblem. Techniquessuchasrobustoptimization,stochastic
trajectoryplanning,andfeedbackmotionplanning(wherethetrajectoryiscontinually
adjustedbasedonsensorfeedback)areworthinvestigating. Forinstance,ifabox’s
position on the conveyor is slightly off from expectation, the trajectory to grab it
shouldadjustinrealtime(perhapsusingvisualservoing). Whilebasicapproaches
exist (many industrial arms come with vision-guided correction capabilities), the
challengeistointegratetheseseamlesslywithhigher-levelplanningsothattheentire
operation(frompicktoplace)isrobust,notjustindividualsub-motions.
5. Advancedcontrolofunderactuatedandredundantsystems: Mostpalletizingrobots
todayarefairlystandardsix-axisarticulatedarms(fullyactuatedandtypicallynon-
redundant in their workspace). However, the push for cheaper or more flexible
systemscouldintroduceunderactuatedmanipulators(tosavecost)ormobilebase
manipulators(introducingredundancy). Therecentworkondifferentiallyflatun-
deractuated planning hints at the potential for using clever trajectory planning to
getgoodperformanceoutofcheaperhardware. Furtherresearchcouldextendthese
methodstohigher-DOFsystemsorunderactuatedarms,makingroboticpalletizing
solutionsmoreaccessibleandeconomical. Ontheotherend,exploitingredundancy
(such as a seven-DOF arm or a robot on a sliding rail) for obstacle avoidance and
singularityavoidanceisanareathatcanbedeepened. Redundancyresolutioninreal
time,especiallyfortime-optimalorenergy-optimalcriteria,remainsacomplexissue
thatfuturealgorithmsneedtomanage,possiblybycombiningsearchmethodswith
instantoptimizationatthecontrollevel.
6. Human–robotcollaborationandergonomics: Anothergrowingtrendiscollaborative
palletizing,whererobotsworkalongsidehumanworkerstobuildpallets. Insuch
settings,trajectoryplanningmustalsoaccountforhumansafety,ergonomics,and
unpredictability. Therobot’smotionsmightneedtobenotjustcollision-freebutalso
intuitiveorpredictabletothehumanpartner. Futureresearchcouldexploretrajectory
generationthatmaximizescriterialikehumancomfortortaskdivisionefficiency. This
involvesintegratinghumanmotionpredictionintotheplanningloopandensuring
therobot’strajectoryplannercanrespondsmoothlytohumanactions(slowingdown,
changingcoursesafely,etc.). Whilethisextendsbeyondpuretrajectoryplanninginto
thedomainofhuman–robotinteraction,itisavitalfrontierfor“as-a-service”robots
thatmayoperateinsemi-structuredwarehouseenvironments.
7. Benchmarking and standardization: Given the variety of available methods, it
can be difficult to determine which approach is best suited for a new palletizing
application[93]. Theliteraturewouldbenefitfromstandardizedbenchmarks—for
example,asetofpalletizingscenariosofvaryingcomplexity(simplepatterns,random
casesizes,mixed-SKUpallets,etc.) onwhichdifferentplanningalgorithmsaretested
and compared. Future research could establish such benchmarks and evaluation
metrics(beyondtimeandenergy,includingmaintainability,scalability,andeaseof
implementation). Thiswouldhelptranslateacademicresultsintoindustrialpractice
by clarifying the trade-offs. It would also highlight which areas (e.g., dynamic re-
planningandmulti-robotcoordination)areleastaddressedbycurrentmethodsand,
thus,needmorefocus.
Inconclusion,addressingthesegapswillrequirethecombinationofinsightsfromclas-
sicalrobotics(kinematics,dynamics,andcontrol)withmoderntechniquesincomputation
andAI.Thecontinuingdevelopmentoffasterprocessors;cloudcomputing;and,perhaps,
dedicatedmotionplanninghardwarecouldalsounlockreal-timecapabilitiesthatwere
previouslyinfeasible. Theconceptofrobotizedas-a-servicepackinginherentlydemands

Robotics2025,14,55 18of23
flexibility,adaptability,andreliability;hence,trajectoryplanningresearchmustcontinueto
evolvetomeetthesedemandsinincreasinglyunstructuredandchallengingenvironments.
6. Conclusions
This review has surveyed the state of the art in manipulator trajectory planning
andpathoptimization,withaparticularfocusonapplicationsinroboticpalletizingand
automatedpacking. Wesummarizedabroadspectrumofapproaches—fromclassicalalgo-
rithmslikeA*anddynamicprogrammingtosampling-basedplannerssuchasPRM/RRT
andmoderntechniquesinvolvingsplinesandmachinelearning. Eachcategoryofmeth-
odsoffersdistinctstrengths: graphsearchandsamplingplannersprovidefundamental
toolsforfindingfeasiblepathsincomplexspaces,polynomialandsplinetechniquesen-
suresmoothandhigh-speedmotions,andlearning-basedmethodspromiseadaptiveand
efficientcontrolthatcanimproveovertime.
Onekeyfindingisthatthereisnoone-size-fits-allsolution;instead,successfulsystems
often integrate multiple planning layers. For example, a palletizing robot might use a
high-levelplanner(orevensimpleheuristics)todecidetheplacementorderandrough
paths,thenrefinethosewithasplineortime-optimalsegmentandfinallyadjustinrealtime
usingalocalavoidanceorfeedbackcontroller. Bycombiningapproaches,theweaknesses
ofonemethodcanbemitigatedbythestrengthsofanother—suchhybridstrategieshave
beenevidencedinseveralstudies(suchasbycombiningthePRMwithRLorusingvision
feedbackontopofpre-plannedpaths).
Fromapracticalindustryperspective,someinsightscanbedrawn. First,forrelatively
structuredpalletizingtasks(e.g.,uniformboxsizesandknownlayouts),traditionalmotion
planningmethods(likeprecomputedtrajectoriesorpattern-basedapproaches)areoften
sufficientandveryefficient. However,asproductvariabilityincreasesandasservice-based
deploymentsdemandquickreconfiguration,moreadvancedplanningbecomesnecessary.
Companiescanbenefitfrominvestmentsintrajectoryoptimization: evenasmallreduction
incycletimeorenergyperpick–placecycle,whenmultipliedbythousandsofcyclesper
day,canyieldsignificantproductivityandcostgains. Forinstance,smoothingarobot’s
motionwithsplineinterpolationcanreducewearandavoidabruptmoves,leadingtoless
downtime for maintenance. Likewise, energy-efficient trajectories can lower operating
costsandhelpmeetsustainabilitytargetswithoutrequiringnewhardware.
Ourreviewalsohighlightedthatpalletizingapplicationsdrivespecificresearchneeds,
suchasplanningwithincreasingobstacles(asthepalletstackgrows)andhandlingheavy
payloaddynamics. SolutionslikecontinuallyupdatedRRTsforeachlayerofthestackand
pre-emptiveavoidancemaneuvershavebeendevelopedtoaddressthese. Furthermore,the
integrationofcomputervision(foritemdetectionandlocalization)withmotionplanning
iscrucialinpalletizingcells. Modernsystemsemployvisiontoinformtheplannerabout
theenvironment,essentiallyclosingtheloopfromperceptiontoaction.
Finally,weidentifiedseveralfutureresearchdirections,includingreal-timeadaptive
planning,integratedtaskandmotionoptimization,safelearning-basedcontrol,andhuman–
robot collaborative planning. Advancements in these areas will likely define the next
generationof“smart”packingrobots.Suchrobotswouldnotonlyexecutepre-programmed
motions but could also learn and optimize their trajectories based on operational data,
adapttonewproductsorlayoutswithminimalreprogramming,andworksafelyalongside
humansinsharedenvironments.
In conclusion, the field of manipulator trajectory planning is rich and continually
evolving. Forroboticpalletizing,whichsitsattheintersectionoflogisticsandautomation,
leveraging the latest planning algorithms can significantly enhance performance. By
applyingthemethodsreviewedinthispaper,industrypractitionerscandesignrobotic

Robotics2025,14,55 19of23
cellsthatarefaster,moreefficient,andmoreflexible. Atthesametime,ongoingresearch—
particularlyonthecombinationofclassicaloptimalcontrolwithartificialintelligence—
is poised to unlock even greater capabilities, making robot-as-a-service palletizing an
increasinglyattractiveandreliableoptionforawiderangeofend-of-linepackagingneeds.
Author Contributions: Formal analysis: D.Á.-M.; Funding acquisition: C.M., R.B., C.F.R. and
D.Á.-M.; Investigation: A.V.G., A.M.M., S.R. and J.V.; Project administration: C.M., R.B. and
D.Á.-M.; Supervision: C.F.R. and D.Á.-M.; Visualization: A.M.M.; Writing—original draft: S.R.,
J.V.andA.M.M.; Writing—reviewandediting,D.Á.-M.Allauthorshavereadandagreedtothe
publishedversionofthemanuscript.
Funding:ThisresearchwasmadepossiblethankstofundingfromthePATRIMONIOAUTÓNOMO
FONDONACIONALDEFINANCIAMIENTOPARALACIENCIA,LATECNOLOGÍAYLAIN-
NOVACIÓNFRANCISCOJOSÉDECALDASandthesupportprovidedbyIntegraS.A.Allauthors
acknowledgefinancialsupportprovidedbytheVicePresidencyofResearch&Creationpublication
fundoftheUniversidaddelosAndes.
DataAvailabilityStatement:Nonewdatawerecreatedinthisstudy.
ConflictsofInterest:AuthorsAndreaValentinaGarcía,CesarMarín,RubenBolañoswereemployed
bythecompanyIntegraS.A.Theremainingauthorsdeclarethattheresearchwasconductedinthe
absenceofanycommercialorfinancialrelationshipsthatcouldbeconstruedasapotentialconflict
ofinterest.
References
1. Valero,S.;Martinez,J.C.;Montes,A.M.;Marín,C.;Bolaños,R.;Álvarez,D. MachineVision-AssistedDesignofEndEffectorPose
inRoboticMixedDepalletizingofHeterogeneousCargo. Sensors2025,25,1137.[CrossRef]
2. Nguyen-Vinh,K.;Dewasurendra,H.;Gonapaladeniya,S.;Sarbahi,U.;Le,N. StackAlgorithmImplementationinRobot-Based
MixedCasePalletizingSystem. InProceedingsofthe20224thInternationalConferenceonElectrical,ControlandInstrumentation
Engineering(ICECIE),KualaLumpur,Malaysia,26November 2022;pp. 1–8.[CrossRef]
3. Baldassarri, A.; Innero, G.; Di Leva, R.; Palli, G.; Carricato, M. Development of a mobile robotized system for palletizing
applications. InProceedingsofthe202025thIEEEInternationalConferenceonEmergingTechnologiesandFactoryAutomation
(ETFA),Vienna,Austria,8–11September2020;IEEE:Piscataway,NJ,USA,2020;Volume1,pp.395–401.
4. Parisi,F.;Mangini,A.M.;Fanti,M.P. Optimaltrajectoryplanningforaroboticmanipulatorpalletizingtasks. InProceedingsof
the2020IEEEInternationalConferenceonSystems,Man,andCybernetics(SMC),Toronto,ON,Canada,11–14October2020;
IEEE:Piscataway,NJ,USA,2020;pp.2901–2906.
5. Lamon,E.;Leonori,M.;Kim,W.;Ajoudani,A. Towardsanintelligentcollaborativeroboticsystemformixedcasepalletizing. In
Proceedingsofthe2020IEEEInternationalConferenceonRoboticsandAutomation(ICRA),Paris,France,31May–31August
2020;IEEE:Piscataway,NJ,USA,2020;pp.9128–9134.
6. Zhu,W.;Fu,Y.;Zhou,Y.3Ddynamicheterogeneousroboticpalletizationproblem. Eur.J.Oper.Res.2024,316,584–596.[CrossRef]
7. Boshoff,M.;Kuhlenkötter,B.;Koslowski,P. DynamicCameraPlanningforRobot-IntegratedManufacturingProcessesUsinga
UAV. Robotics2025,14,23.[CrossRef]
8. Song,Y.;Zhao,J.;Huang,T.;Lau,D.;Liu,Y.H. ALight-WeightRoboticSystemforFlexibleandEfficientHeavy-LoadPalletizing
inCuboidSpaces. IEEE/ASMETrans.Mechatronics2025.[CrossRef]
9. Zhou,Q.;Wu,J.;Li,B.;Li,S.;Feng,B.;Liu,J.;Bi,Y. AdaptiveRobotMotionPlanningforSmartManufacturingBasedonDigital
TwinandBayesianOptimization-EnhancedReinforcementLearning. J.Manuf.Sci.Eng.2025,147,051009.[CrossRef]
10. Zhixiang,X.;Baoliang,L.;Ao,Y.;Haojie,X. TrajectoryPlanningofPalletizingRobotBasedonFourierSeriesExpansion. LightInd.
Mach.2024,42,29.
11. Availableonline:https://www.esneca.lat/blog/tipos-robots-industriales-caracteristicas/(accessedon12December2024).
12. González, V.R. Robots Industriales. 2002. Available online: https://www.iso.org/standard/62996.html (accessed on 12
December2024).
13. Vicentini,F. Collaborativerobotics:Asurvey. J.Mech.Des.2021,143,040802.[CrossRef]
14. MartínBarrio,A.;Terrile,S.;Barrientos,A.;delCerro,J. Robotshiper-redundantes:Clasificación,estadodelarteyproblemática.
Rev.Iberoam.Autom.EInform.Ind.2018,15,351–362.[CrossRef]
15. Moreno,H.A.;Saltaren,R.;Carrera,I.;Puglisi,L.;Aracil,R. Índicesdedesempeñoderobotsmanipuladores:Unarevisióndel
estadodelarte. Rev.Iberoam.Autom.Inform.Ind.2012,9,111–122.[CrossRef]

Robotics2025,14,55 20of23
16. Patel,S.;Sobh,T. Manipulatorperformancemeasures-acomprehensiveliteraturesurvey. J.Intell.Robot.Syst.2015,77,547–570.
[CrossRef]
17. Hwang,S.;Kim,H.;Choi,Y.;Shin,K.;Han,C. Designoptimizationmethodfor7DOFrobotmanipulatorusingperformance
indices. Int.J.Precis.Eng.Manuf.2017,18,293–299.[CrossRef]
18. Ata,A.A. Optimaltrajectoryplanningofmanipulators:Areview. J.Eng.Sci.Technol.2007,2,32–54.
19. Ratiu,M.;Prichici,M.A. Industrialrobottrajectoryoptimization-areview. InMATECWebofConferences;EDPSciences:LesUlis,
France,2017;Volume126,p.02005.
20. Rahimi,H.;Nazemizadeh,M. Dynamicanalysisandintelligentcontroltechniquesforflexiblemanipulators: Areview. Adv.
Robot.2014,28,63–76.[CrossRef]
21. Haddadin,S.;DeLuca,A.;Albu-Schäffer,A. Robotcollisions:Asurveyondetection,isolation,andidentification. IEEETrans.
Robot.2017,33,1292–1312.[CrossRef]
22. Nektarios,A.;Aspragathos,N.A. Optimallocationofageneralpositionandorientationend-effector’spathrelativetomanipula-
tor’sbase,consideringvelocityperformance. Robot.Comput.-Integr.Manuf.2010,26,162–173.[CrossRef]
23. Schneider,U.;Posada,J.R.D.;Verl,A. Automaticposeoptimizationforroboticprocesses. InProceedingsofthe2015IEEE
InternationalConferenceonRoboticsandAutomation(ICRA),Seattle,DC,USA,26–30May2015;IEEE:Piscataway,NJ,USA,
2015;pp.2054–2059.
24. Malhan,R.K.;Kabir,A.M.;Shah,B.;Gupta,S.K. Identifyingfeasibleworkpieceplacementwithrespecttoredundantmanipulator
forcomplexmanufacturingtasks. InProceedingsofthe2019InternationalConferenceonRoboticsandAutomation(ICRA),
Montreal,QC,Canada,20–24May2019;IEEE:Piscataway,NJ,USA,2019;pp.5585–5591.
25. Tian,L.;Collins,C. Motionplanningforredundantmanipulatorsusingafloatingpointgeneticalgorithm. J.Intell.Robot.Syst.
2003,38,297–312.[CrossRef]
26. Vosniakos,G.C.;Matsas,E. Improvingfeasibilityofroboticmillingthroughrobotplacementoptimisation. Robot.Comput.-Integr.
Manuf.2010,26,517–525.[CrossRef]
27. Pamanes-García,J.;Cuan-Durón,E.;Zeghloul,S. Singleandmulti-objectiveoptimizationofpathplacementforredundant
roboticmanipulators. Ing.Investig.Tecnol.2008,9,231–257.[CrossRef]
28. Masood, S.; Khan, H.A. Developmentofpalletpatternplacementstrategiesinroboticpalletisation. Assem. Autom. 2014,
34,151–159.[CrossRef]
29. Weingartshofer,T.;Hartl-Nesic,C.;Kugi,A. OptimalTCPandRobotBasePlacementforaSetofComplexContinuousPaths. In
Proceedingsofthe2021IEEEInternationalConferenceonRoboticsandAutomation(ICRA),Xi’an,China,30May–5June2021;
IEEE:Piscataway,NJ,USA,2021;pp.9659–9665.
30. dosSantos,R.R.;Steffen,V.;Saramago,S.d.F.P. Optimaltaskplacementofaserialrobotmanipulatorformanipulabilityand
mechanicalpoweroptimization. Sci.Res.2010,2,2779.[CrossRef]
31. Spensieri, D.; Carlson, J.S.; Bohlin, R.; Kressin, J.; Shi, J. Optimalrobotplacementfortasksexecution. ProcediaCIRP2016,
44,395–400.[CrossRef]
32. Zacharias,F.;Borst,C.;Hirzinger,G. Capturingrobotworkspacestructure:Representingrobotcapabilities. InProceedingsofthe
2007IEEE/RSJInternationalConferenceonIntelligentRobotsandSystems,SanDiego,CA,USA,29October–2November2007;
IEEE:Piscataway,NJ,USA,2007;pp.3229–3236.
33. Makhal,A.;Goins,A.K. Reuleaux: Robotbaseplacementbyreachabilityanalysis. InProceedingsofthe2018SecondIEEE
InternationalConferenceonRoboticComputing(IRC),LagunaHills,CA,USA,31January–2February2018;IEEE:Piscataway,
NJ,USA,2018;pp.137–142.
34. Doan,N.C.N.;Lin,W. Optimalrobotplacementwithconsiderationofredundancyproblemforwrist-partitioned6Rarticulated
robots. Robot.Comput.-Integr.Manuf.2017,48,233–242.[CrossRef]
35. Xu,J.;Harada,K.;Wan,W.;Ueshiba,T.;Domae,Y. Planninganefficientandrobustbasesequenceforamobilemanipulator
performingmultiplepick-and-placetasks. InProceedingsofthe2020IEEEInternationalConferenceonRoboticsandAutomation
(ICRA),Paris,France,31May–31August2020;IEEE:Piscataway,NJ,USA,2020;pp.11018–11024.
36. Julián,P.P.;María.,M. DefiniciónTrayectoria.Definicion.de.2010. Availableonline:https://definicion.de/trayectoria/(accessed
on12December2024).
37. Siciliano,B.; Sciavicco,L.; Villani,L.; Oriolo,G. TrajectoryPlanning. InRobotics: Modelling,PlanningandControl; Springer:
London,UK,2009;pp.161–189.
38. Saha,S.K. ControldeTrayectoria. InProceedingsoftheIntroducciónalaRobotica;McGrawHill:NewYork,NY,USA,2010;p.30.
39. Romero,S.;Montes,A.M.;Rodríguez,C.F.;Martínez,D.Á.;Valero,J.S. Time-optimaltrajectoryplanningforindustrialrobots
withend-effectoraccelerationconstraints. InProceedingsofthe2023IEEE6thColombianConferenceonAutomaticControl
(CCAC),Popayán,Colombia,17–20October2023;IEEE:Piscataway,NJ,USA,2023;pp.1–6.
40. Feng,L.;Jia,J. ImprovedalgorithmofRRTpathplanningbasedoncomparisonoptimization. JisuanjiGongchengYuYingyong
(Computer.Eng.Appl.)2011,47,210–218.

Robotics2025,14,55 21of23
41. Shin,K.;McKay,N. Minimum-timecontrolofroboticmanipulatorswithgeometricpathconstraints. IEEETrans.Autom.Control
1985,30,531–541.[CrossRef]
42. Messay,T.;Ordóñez,R.;Marcil,E.Computationallyefficientandrobustkinematiccalibrationmethodologiesandtheirapplication
toindustrialrobots. Robot.Comput.-Integr.Manuf.2016,37,33–48.[CrossRef]
43. Haddad,M.;Khalil,W.;Lehtihet,H. Trajectoryplanningofunicyclemobilerobotswithatrapezoidal-velocityconstraint. IEEE
Trans.Robot.2010,26,954–962.[CrossRef]
44. Luan,N.;Zhang,H.;Tong,S. Optimummotioncontrolofpalletizingrobotsbasedoniterativelearning. Ind.Robot.Int.J.2012,
39,162–168.[CrossRef]
45. Zhang,Q.;Li,S.R.;Gao,X.S. Practicalsmoothminimumtimetrajectoryplanningforpathfollowingroboticmanipulators. In
Proceedingsofthe2013AmericanControlConference,Washington,DC,USA,17–19June2013;IEEE:Piscataway,NJ,USA,2013;
pp.2778–2783.
46. Xu,Y.P.;Hong,Y. Timeoptimalpathplanningofpalletizingrobot. Appl.Mech.Mater. 2014,470,658–662.[CrossRef]
47. Abu-Dakka,F.J.;Assad,I.F.;Alkhdour,R.M.;Abderahim,M. Statisticalevaluationofanevolutionaryalgorithmforminimum
timetrajectoryplanningproblemforindustrialrobots. Int.J.Adv.Manuf.Technol.2017,89,389–406.[CrossRef]
48. Xiao,B.;Yin,S. Exponentialtrackingcontrolofroboticmanipulatorswithuncertaindynamicsandkinematics. IEEETrans.Ind.
Informatics2018,15,689–698.[CrossRef]
49. Piazzi,A.;Visioli,A. Globalminimum-jerktrajectoryplanningofrobotmanipulators. IEEETrans.Ind.Electron.2000,47,140–149.
[CrossRef]
50. Gasparetto,A.;Boscariol,P.;Lanzutti,A.;Vidoni,R. Pathplanningandtrajectoryplanningalgorithms:Ageneraloverview. In
MotionandOperationPlanningofRoboticSystems;Springer:Cham,Switzerland, 2015;pp.3–27.
51. Tonan,M.;Bottin,M.;Doria,A.;Rosati,G. Motionplanningofdifferentiallyflatplanarunderactuatedrobots. Robotics2024,
13,57.[CrossRef]
52. Duchonˇ,F.;Babinec,A.;Kajan,M.;Benˇo,P.;Florek,M.;Fico,T.;Jurišica,L. Pathplanningwithmodifiedastaralgorithmfora
mobilerobot. ProcediaEng.2014,96,59–69.[CrossRef]
53. Wang, D. Indoor mobile-robot path planning based on an improved A* algorithm. J. Tsinghua Univ. Sci. Technol. 2012,
52,1085–1089.
54. Zidane,I.M.;Ibrahim,K. Wavefrontanda-staralgorithmsformobilerobotpathplanning. InProceedingsoftheInternational
ConferenceonAdvancedIntelligentSystemsandInformatics,Cairo,Egypt,9–11September2017;Springer:Berlin/Heidelberg,
Germany, 2017;pp.69–80.
55. Nieto,J.;Slawinski,E.;Mut,V.;Wagner,B. Onlinepathplanningbasedonrapidly-exploringrandomtrees. InProceedingsofthe
2010IEEEInternationalConferenceonIndustrialTechnology,ViadelMar,Chile,14-17March2010;IEEE:Piscataway,NJ,USA,
2010;pp.1451–1456.
56. LaValle,S.M.;KuffnerJr,J.J. Randomizedkinodynamicplanning. Int.J.Robot.Res.2001,20,378–400.[CrossRef]
57. Kavraki, L.E.; Svestka, P.; Latombe, J.C.; Overmars, M.H. Probabilistic roadmaps for path planning in high-dimensional
configurationspaces. IEEETrans.Robot.Autom.1996,12,566–580.[CrossRef]
58. Yu,X.;Zhao,Y.;Wang,C.;Tomizuka,M. Trajectoryplanningforrobotmanipulatorsconsideringkinematicconstraintsusing
probabilisticroadmapapproach. J.Dyn.Syst.Meas.Control2017,139,021001.[CrossRef]
59. Park,J.J.;Kim,J.H.;Song,J.B. Pathplanningforarobotmanipulatorbasedonprobabilisticroadmapandreinforcementlearning.
Int.J.ControlAutom.Syst.2007,5,674–680.
60. Akbaripour,H.;Masehian,E. Semi-lazyprobabilisticroadmap:Aparameter-tuned,resilientandrobustpathplanningmethod
formanipulatorrobots. Int.J.Adv.Manuf.Technol.2017,89,1401–1430.[CrossRef]
61. Chen,G.;Luo,N.;Liu,D.;Zhao,Z.;Liang,C. Pathplanningformanipulatorsbasedonanimprovedprobabilisticroadmap
method. Robot.Comput.-Integr.Manuf.2021,72,102196.[CrossRef]
62. Wei,K.;Ren,B. Amethodondynamicpathplanningforroboticmanipulatorautonomousobstacleavoidancebasedonan
improvedRRTalgorithm. Sensors2018,18,571.[CrossRef][PubMed]
63. Zhang,H.;Wang,Y.;Zheng,J.;Yu,J.PathplanningofindustrialrobotbasedonimprovedRRTalgorithmincomplexenvironments.
IEEEAccess2018,6,53296–53306.[CrossRef]
64. Yang,H.;Li,L.;Gao,Z. Obstacleavoidancepathplanningofhybridharvestingmanipulatorbasedonjointconfigurationspace.
Trans.Chin.Soc.Agric.Eng.2017,33,55–62.
65. Jaryani,M.H. Aneffectivemanipulatortrajectoryplanningwithobstaclesusingvirtualpotentialfieldmethod. InProceedings
ofthe2007IEEEInternationalConferenceonSystems,ManandCybernetics,Montreal,QC,Canada,7–10October2007;IEEE:
Piscataway,NJ,USA,2007;pp.1573–1578.
66. Li,G.;Yamashita,A.;Asama,H.;Tamura,Y. Anefficientimprovedartificialpotentialfieldbasedregressionsearchmethodfor
robotpathplanning. InProceedingsofthe2012IEEEInternationalConferenceonMechatronicsandAutomation,Chengdu,
China,5–8August2012;IEEE:Piscataway,NJ,USA,2012;pp.1227–1232.

Robotics2025,14,55 22of23
67. Xu,T.;Zhou,H.;Tan,S.;Li,Z.;Ju,X.;Peng,Y. Mechanicalarmobstacleavoidancepathplanningbasedonimprovedartificial
potentialfieldmethod. Ind.Robot.Int.J.Robot.Res.Appl.2022,49,271–279.[CrossRef]
68. Wang,H.;Lyu,W.;Yao,P.;Liang,X.;Liu,C. Three-dimensionalpathplanningforunmannedaerialvehiclebasedoninterfered
fluiddynamicalsystem. Chin.J.Aeronaut.2015,28,229–239.[CrossRef]
69. Jin, L.; Li, S.; Yu, J.; He, J. Robotmanipulatorcontrolusingneuralnetworks: Asurvey. Neurocomputing2018, 285,23–34.
[CrossRef]
70. Li,Z.;Li,S. AnL -NormBasedOptimizationMethodforSparseRedundancyResolutionofRoboticManipulators. IEEETrans.
1
CircuitsSyst.IIExpressBriefs2021,69,469–473.[CrossRef]
71. Xie,Z.;Jin,L.;Du,X.;Xiao,X.;Li,H.;Li,S. OngeneralizedRMPschemeforredundantrobotmanipulatorsaidedwithdynamic
neuralnetworksandnonconvexboundconstraints. IEEETrans.Ind.Inform.2019,15,5172–5181.[CrossRef]
72. Iqdymat,A.;Stamatescu,G. ReinforcementLearningofaSix-DOFIndustrialManipulatorforPick-and-PlaceApplicationUsing
EfficientControlinWarehouseManagement. Sustainability2025,17,432.[CrossRef]
73. Martínez-Franco,J.C.;Rojas-Álvarez,A.;Tabares,A.;Álvarez-Martínez,D.;Marín-Moreno,C.A. LatentSpaceRepresentations
forMarker-LessRealtimeHand–EyeCalibration. Sensors2024,24,4662.[CrossRef]
74. Liu,H.;Lai,X.;Wu,W. Time-optimalandjerk-continuoustrajectoryplanningforrobotmanipulatorswithkinematicconstraints.
Robot.Comput.-Integr.Manuf.2013,29,309–317.[CrossRef]
75. Xu,Z.;Li,S.;Chen,Q.;Hou,B. MOPSObasedmulti-objectivetrajectoryplanningforrobotmanipulators. InProceedingsofthe
20152ndInternationalConferenceonInformationScienceandControlEngineering,Shanghai,China,24–26April2015;IEEE:
Piscataway,NJ,USA,2015;pp.824–828.
76. Wan,N.;Xu,D.;Ye,H. ImprovedcubicB-splinecurvemethodforpathoptimizationofmanipulatorobstacleavoidance. In
Proceedingsofthe2018ChineseAutomationCongress(CAC),Xi’an,China,30November–2December2018;IEEE:Piscataway,
NJ,USA,2018;pp.1471–1476.
77. Mei,J.;Zang,J.;Qiao,Z.;Liu,S.;Song,T. Trajectoryplanningof3-DOFdeltaparallelmanipulator. J.Mech.Eng2016,52,9–17.
[CrossRef]
78. Srinivas,G.L.;Javed,A. Optimizationapproachesofindustrialserialmanipulatorstoimproveenergyefficiency:Areview. In
ProceedingsoftheIOPConferenceSeries:MaterialsScienceandEngineering,Sozopol,Bulgaria,10–13September2020;IOP
Publishing:Bristol,UK,2020;Volume912,p.032058.
79. Paryanto;Brossog,M.;Bornschlegl,M.;Franke,J. Reducingtheenergyconsumptionofindustrialrobotsinmanufacturing
systems. Int.J.Adv.Manuf.Technol.2015,78,1315–1328.
80. Huang,M.S.;Hsu,Y.L.;Fung,R.F. Minimum-energypoint-to-pointtrajectoryplanningforamotor-toggleservomechanism.
IEEE/ASMETrans.Mechatronics2011,17,337–344.[CrossRef]
81. Pellicciari,M.;Berselli,G.;Leali,F.;Vergnano,A. Amethodforreducingtheenergyconsumptionofpick-and-placeindustrial
robots. Mechatronics2013,23,326–334.[CrossRef]
82. Bonami,P.;Olivares,A.;Staffetti,E. Energy-optimalmulti-goalmotionplanningforplanarrobotmanipulators. J.Optim.Theory
Appl.2014,163,80–104.[CrossRef]
83. Wang,Y.;Zhao,Y.;Bortoff,S.A.;Ueda,K. Areal-timeenergy-optimaltrajectorygenerationmethodforaservomotorsystem.
IEEETrans.Ind.Electron.2014,62,1175–1188.[CrossRef]
84. Fung,R.F.;Cheng,Y.H. TrajectoryplanningbasedonminimumabsoluteinputenergyforanLCDglass-handlingrobot. Appl.
Math.Model.2014,38,2837–2847.[CrossRef]
85. Liu,Y.;Liang,L.;Han,H.;Zhang,S. Amethodofenergy-optimaltrajectoryplanningforpalletizingrobot. Math.Probl.Eng.2017,
2017.[CrossRef]
86. Pellegrinelli,S.;Borgia,S.;Pedrocchi,N.;Villagrossi,E.;Bianchi,G.;Tosatti,L.M. Minimizationoftheenergyconsumptionin
motionplanningforsingle-robottasks. ProcediaCIRP2015,29,354–359.[CrossRef]
87. He,Y.;Mei,J.;Fang,Z.;Zhang,F.;Zhao,Y. Minimumenergytrajectoryoptimizationfordrivingsystemsofpalletizingrobot
joints. Math.Probl.Eng.2018,2018,7247093.[CrossRef]
88. Paes,K.;Dewulf,W.;VanderElst,K.;Kellens,K.;Slaets,P. EnergyefficienttrajectoriesforanindustrialABBrobot. ProcediaCirp
2014,15,105–110.[CrossRef]
89. Vidussi,F.;Boscariol,P.;Scalera,L.;Gasparetto,A. Localandtrajectory-basedindexesfortask-relatedenergeticperformance
optimizationofroboticmanipulators. J.Mech.Robot.2021,13,021018.[CrossRef]
90. Meike,D.;Pellicciari,M.;Berselli,G. Energyefficientuseofmultirobotproductionlinesintheautomotiveindustry:Detailed
systemmodelingandoptimization. IEEETrans.Autom.Sci.Eng.2013,11,798–809.[CrossRef]
91. Sakamoto,T.;Harada,K.;Wan,W. Real-timeplanningroboticpalletizingtasksusingreusableroadmaps. J.Robot.Netw.Artif.
Life2020,6,240–245.[CrossRef]

Robotics2025,14,55 23of23
92. Xu,W.-F.;Wang,X.-Q.;Xue,Q.;Liang,B. Studyontrajectoryplanningofdual-armspacerobotkeepingthebasestabilized. Acta
Autom.Sin.2013,39,69–80.[CrossRef]
93. Pantoja-Benavides,G.;Giraldo,D.;Montes,A.;García,A.;Rodríguez,C.;Marín,C.;Álvarez-Martínez,D.ComprehensiveReview
ofRobotizedFreightPacking. Logistics2024,8,69.[CrossRef]
Disclaimer/Publisher’sNote: Thestatements, opinionsanddatacontainedinallpublicationsaresolelythoseoftheindividual
author(s)andcontributor(s)andnotofMDPIand/ortheeditor(s).MDPIand/ortheeditor(s)disclaimresponsibilityforanyinjuryto
peopleorpropertyresultingfromanyideas,methods,instructionsorproductsreferredtointhecontent.