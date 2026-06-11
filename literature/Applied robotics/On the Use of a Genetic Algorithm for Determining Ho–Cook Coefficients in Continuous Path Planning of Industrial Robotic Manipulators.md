machines
Article
On the Use of a Genetic Algorithm for Determining Ho–Cook
Coefficients in Continuous Path Planning of Industrial
Robotic Manipulators
TeodorGrenko1,† ,SandiBaressiŠegota2,*,† ,NikolaAnd¯elic´ 2 ,IvanLorencin2 ,DanielŠtifanic´ 2 ,
JelenaŠtifanic´ 2 ,MatkoGlucˇina2 ,BornaFranovic´ 2andZlatanCar2
1 ADRIA-ELECTRONICLtd.,AndrijeKacˇic´aMiošic´a13,51000Rijeka,Croatia
2 DepartmentofAutomationandElectronics,FacultyofEngineering,UniversityofRijeka,Vukovarska58,
51000Rijeka,Croatia
* Correspondence:sbaressisegota@riteh.hr;Tel.:+385-51-505-715
† Theseauthorscontributedequallytothiswork.
Abstract:Pathplanningisoneofthekeystepsintheapplicationofindustrialroboticmanipulators.
Theprocessofdeterminingtrajectoriescanbetime-intensiveandmathematicallycomplex,which
raisesthecomplexityanderrorpronenessofthistask. Forthesereasons, theauthorstestedthe
application of a genetic algorithm (GA) on the problem of continuous path planning based on
theHo–Cookmethod. Thegenerationoftrajectorieswasoptimizedwithregardtothedistance
betweenindividualsegments. Aboundaryconditionwassetregardingtheminimalvaluesthat
thetrajectoryparameterscanbesetinordertoavoidstationarysolutions.Anydistancesbetween
segments introduced by this condition were addressed with Bezier spline interpolation applied
betweenevolvedsegments. Thedevelopedalgorithmwasshowntogeneratetrajectoriesandcan
easilybeappliedforthefurtherpathplanningofvariousroboticmanipulators,whichindicatesgreat
promisefortheuseofsuchalgorithms.
Citation:Grenko,T.;BaressiŠegota,
S.;And¯elic´,N.;Lorencin,I.;Štifanic´, Keywords:evolutionarycomputing;geneticalgorithm;industrialroboticmanipulators;pathplanning
D.;Musulin,J.;Glucˇina,M.;Franovic´,
B.;Car,Z.OntheUseofaGenetic
AlgorithmfortheDetermining
Ho–CookCoefficientsinContinuous
1. Introduction
PathPlanningofIndustrialRobotic
The most significant element in the application of industrial robotic manipulators
Manipulators.Machines2023,11,167.
onrealistictasksisthepathplanningprocess[1]. Thisprocessdeterminesthetrajectory
https://doi.org/10.3390/
ofthejointmovements—theirpositions,speeds,andaccelerations—allowingtherobotic
machines11020167
manipulatortoperformoperationswithinitsenvironment[2]. Thegoalofpathplanning
AcademicEditors:PeterOdry,Akos
istocalculatepathsthatsatisfythepresetconditionsthathavetobefulfilledinorderto
OdryandJanAwrejcewicz
accomplishthetask. Therearetwomainparadigmsoftrajectorydetermination: point-
Received:23December2022 to-pointandcontinuouspathplanning[3,4]. Point-to-pointplanningconcernsitselfwith
Revised:13January2023 generatingpathsbetweentwopointsinspaceandiscommonlyusedforoperationssuch
Accepted:22January2023 asthepick-and-placetransferofobjects[5]. Continuouspathplanning,ontheotherhand,
Published:25January2023 takes into account the movement not just between the initial and final points in space
butalsothepositionsandspeedsbetweenthem. Suchanapproachiscommonlyusedfor
taskssuchasweldingorpaintingobjectsinspace[6]. Multipledeterministicmethodscan
beusedtoperformthepathplanningofindustrialroboticmanipulatorscontinuously: Ho–
Copyright: © 2023 by the authors.
Cook[7],Taylor’spolynomialapproach[8],orinterpolationbetweentrajectorypoints[9].
Licensee MDPI, Basel, Switzerland.
Whilethesealgorithmsperformwell,theycanbecomputationallycomplexand,depending
This article is an open access article
onthemodeofapplication,error-prone. Evolutionarycomputingisabranchofartificial
distributed under the terms and
intelligence that deals with the study of algorithms that imitate natural processes [10].
conditionsoftheCreativeCommons
Thebasicalgorithminthisareaistheso-calledgeneticalgorithm, which, byitsdesign,
Attribution(CCBY)license(https://
imitatesthenaturalprocessofevolution[11]. Evolutionarycomputingalgorithmshave
creativecommons.org/licenses/by/
beenshowntohavemanyusesinrobotics[12].
4.0/).
Machines2023,11,167.https://doi.org/10.3390/machines11020167 https://www.mdpi.com/journal/machines

Machines2023,11,167 2of19
Shuklaetal. (2021)[13]demonstratedtheuseofevolutionarycomputingforrobotic
graspmanipulation. TheauthorsappliedECalgorithmstoassistintrainingdeeplearning
models,inanapproachknownashybridmodels. Theymanagedtoachievehigh-precision
modelswiththisapproach. Ferigoetal. (2021)[14]appliedevolutionarycomputingalgo-
rithmsforevolvingsensoryapparatusinsoftcomputingapplications. Kimetal. (2021)[15]
demonstratedtheapplicationofevolutionarycomputingfortheissueofquadrupedrobot
gaitoptimization. TheauthorsutilizedGAtocreatepathsformobilerobots’legstoachieve
a more controlled gait. Liu et al. (2022) [16] created a digital twin, which is a virtual-
ized copy of a real robot. The authors then demonstrated the ability to apply GA for
thepathplanningofsucharobot,whichtheymanagedtosuccessfullytransfertoareal
robot. Lietal. (2021)[17]addressedanotherimportantissueinrobotics: taskallocation
through the application of a differential evolution algorithm. The authors managed to
achievestate-of-the-artresultsonamultitaskoptimizationproblem. Taskallocationwas
also addressed by Martin et al. (2021) [18]. In this paper, the authors specifically used
GAtodistributethetasksamongstrobotsbasedonthenonlinearbranchingcriteria. Path
planning for robots was also addressed by Hao et al. (2021) [19]. The authors utilized
GA to optimize a path concerning the possible collision risks, achieving paths that are
capableofavoidingobstructionsinthespace. Asimilarapproachwasdemonstratedby
RahmaniarandRakhmania(2022)[20]formobilerobots. Theauthorsdemonstratedthat
GA-optimizedpathsarecapableofachievingsmootherpathswhencomparedtoclassical
methods. TuningthepathsbasedonBeziersplinescanalsobeachievedusingevolutionary
computing algorithms, as demonstrated by Song et al. (2021) [21], who applied parti-
cleswarmoptimizationtodeterminetheparametersofthesplines. Lietal. (2022)[22]
demonstratedthesubgoalhybridplanningforthepathsmoothingofpathsobtainedwith
forwardsearchoptimizationincontrasttoDjikstra,A*,D*,andD*-litealgorithms. Theau-
thorscomparedtheperformanceofforwardsearchoptimizationandthenewlydeveloped
subgoal-basedhybridpathplanningalgorithm,demonstratingthatsmoothglobalpaths
canbeachievedwithsuchanapproach. Asimilarapproachtotheonepresentedinthis
paper, whereadeterministicalgorithmA*iscombinedwithanevolutionaryapproach,
namelythecoevolutionaryalgorithm,wasadaptedbyGarciaetal. (2023)[23]. Theauthors
demonstratedthatsuchanapproachhasahighenoughperformanceforapplicationson
edge nodes, and performs well in conditions where alternatives such as M* or WHCA
wouldfailtogeneratevalidpaths. Yuetal. (2023)[24]appliedtheartificialbeecolonyto
optimizeamulti-objectivepathplanningissue. Theauthorsdemonstratedthatsuchan
algorithmcanbesuccessfullyappliedtomulti-objectiveproblems,namelypathefficiency
andpathsecurity. Anothernature-inspiredalgorithmwasshownbyWuetal.[25],who
appliedtheantcolonyalgorithmtothepathplanningofthemobilerobot. Themodified
version of the ant colony algorithm that the authors developed shows a significant im-
provementincomparisontothestate-of-the-artmethods. Louetal. (2023)[26]applieda
graphicalcomputingmethodfortheproblemofcontinuouspathplanningforwelding.
Thesimulationsperformedbytheauthorsonthegeneratedpathsdemonstratethepossi-
bilityofapplyingtheinvestigatedmethodinreal-wordapplications. Anotherindustrial
productionapplication, namelysurfacegrinding, wasdiscussedbyLietal. (2023)[27].
The authors applied a revised Levenberg–Marquardt and differential evolution hybrid
algorithm,withreal-worldvalidationontheproblemofgrindingtitaniumblades.
Whilethestate-of-the-artresearchshowsmanyapplicationsofevolutionarycomput-
ingandGAintheareaofroboticsandpathplanning,noneaddressthecombinationof
algorithmssuchasHo–CookwithGAorsimilarevolutionaryalgorithms.
TheHo–Cookalgorithmwasselectedinparticularasthetopicoftheresearchdue
toseveraladvantagesthatitpossessescomparedtosimilaralgorithms: mainlytheability
to manually select as many points as desired (allowing for the granular control of the
trajectoryprecision)andthefactthatitincludestheorientationofthetool,bydesign—as
willbeshowninSection2. DuetothelackofpreviousresearchfocusingontheHo–Cook
algorithmparametertuningwithevolutionaryalgorithms,theauthorsselectedGAasthe

Machines2023,11,167 3of19
secondfocusoftheresearch. GAisthebasicevolutionaryalgorithm,whichmeansthat
itshouldserveasagoodindicatorofperformanceformoreadvancedalgorithms[28,29].
ThegenesetupthatwasdevelopedandispresentedinSection2.2ofthismanuscriptisalso
novel,andcustomizedtotheHo–Cookproblem. Thischromosomeencodingdescribes
the Ho–Cook parametrization and may be used as the basis for the further research of
additional,moreadvancedevolutionaryalgorithms,asmostalgorithmsofthiskindwill
requirethisencodingtobeperformedinthesamemanner[12,30].
Thegoalofthispaperwastotestwhethertheprocessofpathplanninginacontinuous
environment,basedontheHo–Cookalgorithm,canbesimplifiedthroughtheapplication
of the GA. In addition, the parameters of GA that provide the best performance were
alsodetermined. Inthisapproach,thecommonissuesincontinuouspathplanningare
addressedthroughtheHo–Cookalgorithm,whoseshortcomingistheanalyticalcomplexity
ofthecoefficientdetermination,aswillbeshowninSection2.
2. MaterialsandMethods
ThissectionwillservetopresentthebasicideaoftheHo–Cookpathplanningprocess
topointoutwhichpartofitwillbetunedusingtheGA-basedapproach. Then,theprocess
ofGAdevelopmentwillbedescribed.
2.1. Ho–CookPathPlanning
TheHo–Cookpathplanningalgorithmisacontinuouspathplanningalgorithm. It
isbasedondeterminingnpointsthatwillbetheelementsofthetrajectory. Inthecaseof
theobstaclesbeingpresentinthetoolspaceinsideofwhichthepathplanningisbeing
performed,theaforementionedpointsshouldbeplacedinsuchawaythatobstaclesare
notpresent,asobstacleavoidanceisnotabuilt-infeatureoftheHo–Cookmethod[31].
DuetotheHo–Cookmethodhavingtopassthroughthepointsdefinedinitially,astheyare
starting/endingpointsofthesegments,themovementfromthesourcetothedestinationis
guaranteed. TheHo–Cookmethodworksbyinterpolatingbetweentheaforementioned
pointsofthedesiredtrajectorytoachievetheshortestpossiblepaththroughthecalculation
of in-between segments. Higher-order polynomials (4th and 3rd) are used to assure
thesmoothnessofthefinaltrajectory. Then, the n−1segmentsbetweenthepointsare
interpolatedusingthepolynomialsgivenas[32]:
| q   | (t) = B | +B t+B |     | t2+B | t3+B t4 | (1) |
| --- | ------- | ------ | --- | ---- | ------- | --- |
| k   |         | 0k 1k  | 2k  | 3k   | 4k      |     |
forthefirstandthelastsegments,whereastheothersegmentsareinterpolatedusing:
|     | q (t) = | B +B | t+B | t2++B | t3  | (2) |
| --- | ------- | ---- | --- | ----- | --- | --- |
|     | k       | 0k   | 1k  | 2k    | 3k  |     |
Thespeedsandaccelerationscanbederivedfromtheabove. Forthefirstandthelast
segment,theyaregivenas:
(˙t)
|     | q = | B +2B | t+3B | t2+4B | t3, | (3) |
| --- | --- | ----- | ---- | ----- | --- | --- |
|     | k   | 1k    | 2k   | 3k    | 4k  |     |
and
|     | q¨t | =2B +6B |     | t+12B | t2  | (4) |
| --- | --- | ------- | --- | ----- | --- | --- |
|     | k   | 2k      | 1k  |       | 4k  |     |
respectively. Thespeedandaccelerationfortheothersegmentsaregivensimilarlywith:
|     | q (˙t) | = B | +2B | t+3B | t2, | (5) |
| --- | ------ | --- | --- | ---- | --- | --- |
|     | k      | 1k  | 2k  |      | 3k  |     |
and
|     | q¨t | =2B +6B |     | t+12B | t2. |     |
| --- | --- | ------- | --- | ----- | --- | --- |
|     | k   | 2k      | 1k  |       | 4k  | (6) |
Intheaboveequations,thesymbolsusedareasfollows:
• k—thetrajectorypoint;

Machines2023,11,167 4of19
m—thetotalnumberoftrajectorypoints,and
•
• B—coefficientsoftheinterpolationpolynomials.
Foreachofthesegments,anumberofcoefficientsneedtobedetermined. Theycan
bedefinedwithinthematrixoftheshapek×n,wherenisthepolynomialdegree(third
orfourth)andkisthenumberofthejointsoftheroboticmanipulator. Inthepresented
research,thenumberofjointswasassumedtobesix,sincethisisacommonnumberof
degreesoffreedomforindustry-standardarticulatedrobots[33].
Todeterminetheabove,theDennavit–Hartenberg(D-H)algorithmwasperformed.
First,thesimplifiedkinematicschematicwiththenotedrotationaxeswasdesignedforthe
robotthatisbeingmodeled. AnexampleoftheABBIRB120robotcanbeseeninFigure1.
Ontheschematic,thejointsoftherobothaveorthonormalcoordinatesystemsadjoined,
withtheorientationdependentontherotationaxesoftherobotinquestion[34].
Figure1.SimplifiedkinematicschematicoftheABBIRB120robot,withtheassociatedD-Horthonor-
malcoordinatesystems.
Thiswillallowustodeterminethekinematicpropertiesoftherobot,whichcanbe
readfromtheschematic: jointdistanced,jointangleθ,linklengtha,andlinkrotationangle
α[35]. TheobtainedkinematicspropertiesfortherobotinquestionaregiveninTable1.
Table1.Thekinematicparametersoftheanalyzedroboticmanipulator.
| Θ[rad] | d[mm]  | a[mm] | α[rad]  |
| ------ | ------ | ----- | ------- |
| Θ =q   | d =290 | a =0  | α =−π/2 |
| 1 1    | 1      | 1     | 1       |
| Θ =q   | =0     | =270  | =0      |
| 2 2    | d 2    | a 2   | α 2     |
Θ
| 3 =q 3 | d 3 =0 | a 3 =70 | α 3 =−π/2 |
| ------ | ------ | ------- | --------- |
Θ
| =q   | d =302 | a =0 | α =π/2  |
| ---- | ------ | ---- | ------- |
| 4 4  | 4      | 4    | 4       |
| Θ =q | d =0   | a =0 | α =−π/2 |
| 5 5  | 5      | 5    | 5       |
| Θ =q | d =72  | a =0 | α =0    |
| 6 6  | 6      | 6    | 6       |

Machines2023,11,167 5of19
Thenextstepistoobtainthekinematictransformationmatrix,T6,whichistheproduct
0
ofeachindividualjointtransformationmatrix[35]:
 cosθ −cosα sinθ sinα sinθ a cosθ 
k k k k k k k
T6 = Π6   sinθ k cosα k cosθ k −sinα k cosθ k a k sinθ k  (7)
0 k=1 0 sinα k cosα k d k 
0 0 0 1
InsertingthevaluesfromTable1intotheaboveequationyieldsthefollowingequation
thatdescribesthetransformationmatrix:
T6 = [[1.0∗((sin(q )∗sin(q )+cos(q )∗cos(q )∗cos(q +q ))∗cos(q )−sin(q )
0 1 4 1 4 2 3 5 5
∗sin(q +q )∗cos(q ))∗cos(q )+1.0∗(sin(q )∗cos(q )−1.0∗sin(q )∗cos(q )
2 3 1 6 1 4 4 1
cos(q +q ))∗sin(q ),1.0∗(−(sin(q )∗sin(q )+cos(q )∗cos(q )∗cos(q +q ))
2 3 6 1 4 1 4 2 3
cos(q )+sin(q )∗sin(q +q )∗cos(q ))∗sin(q )+1.0∗(sin(q )∗cos(q )
5 5 2 3 1 6 1 4
−1.0∗sin(q )∗cos(q )∗cos(q +q ))∗cos(q ),−1.0∗(sin(q )∗sin(q )
4 1 2 3 6 1 4
+cos(q )∗cos(q )∗cos(q +q ))∗sin(q )−1.0∗sin(q +q )∗cos(q )∗cos(q ),
1 4 2 3 5 2 3 1 5
−0.072∗sin(q )∗sin(q )∗sin(q )−0.072∗sin(q )∗cos(q )∗cos(q )∗cos(q +q )
1 4 5 5 1 4 2 3
−0.072∗sin(q +q )∗cos(q )∗cos(q )−0.302∗sin(q +q )∗cos(q )
2 3 1 5 2 3 1
+0.29∗cos(q )∗cos(q )+0.07∗cos(q )∗cos(q +q )],[1.0∗((sin(q )∗cos(q )
1 2 1 2 3 1 4
cos(q +q )−sin(q )∗cos(q ))∗cos(q )−sin(q )∗sin(q )∗sin(q +q ))
2 3 4 1 5 1 5 2 3
cos(q )−1.0∗(sin(q )∗sin(q )∗cos(q +q )+cos(q )∗cos(q ))∗sin(q ),
6 1 4 2 3 1 4 6
1.0∗((−sin(q )∗cos(q )∗cos(q +q )+sin(q )∗cos(q ))∗cos(q )+sin(q ) (8)
1 4 2 3 4 1 5 1
sin(q )∗sin(q +q ))∗sin(q )−1.0∗(sin(q )∗sin(q )∗cos(q +q )+cos(q )∗cos(q ))
5 2 3 6 1 4 2 3 1 4
cos(q ),1.0∗(−sin(q )∗cos(q )∗cos(q +q )+sin(q )∗cos(q ))∗sin(q )
6 1 4 2 3 4 1 5
−1.0∗sin(q )∗sin(q +q )∗cos(q ),−0.072∗sin(q )∗sin(q )∗cos(q )∗cos(q +q )
1 2 3 5 1 5 4 2 3
−0.072∗sin(q )∗sin(q +q )∗cos(q )−0.302∗sin(q )∗sin(q +q )
1 2 3 5 1 2 3
+0.29∗sin(q )∗cos(q )+0.07∗sin(q )∗cos(q +q )
1 2 1 2 3
+0.072∗sin(q )∗sin(q )∗cos(q )],[−1.0∗(sin(q )∗cos(q +q )+sin(q +q )∗cos(q )
4 5 1 5 2 3 2 3 4
cos(q ))∗cos(q )+1.0∗sin(q )∗sin(q )∗sin(q +q ),1.0∗(sin(q )∗cos(q +q )
5 6 4 6 2 3 5 2 3
+sin(q +q )∗cos(q )∗cos(q ))∗sin(q )+1.0∗sin(q )∗sin(q +q )∗cos(q ),
2 3 4 5 6 4 2 3 6
1.0∗sin(q )∗sin(q +q )∗cos(q )−1.0∗cos(q )∗cos(q +q ),−0.29∗sin(q )
5 2 3 4 5 2 3 2
+0.072∗sin(q )∗sin(q +q )∗cos(q )−0.07∗sin(q +q )
5 2 3 4 2 3
−0.072∗cos(q )∗cos(q +q )−0.302∗cos(q +q )+0.29],[0,0,0,1]]
5 2 3 2 3
The above matrix defines the equations that may be used to calculate the position
[x y z]andorientation[φ θ ψ]. Theseequationsaregivenas:
x = −0.072·sin(q )·sin(q )·sin(q )−0.072·sin(q )·cos(q )·cos(q )·cos(q +q )
1 4 5 5 1 4 2 3
−0.072·sin(q +q )·cos(q )·cos(q )−0.302·sin(q +q )·cos(q ) (9)
2 3 1 5 2 3 1
+0.29·cos(q )·cos(q )+0.07·cos(q )·cos(q +q ),
1 2 1 2 3
y = −0.072·sin(q )·sin(q )·cos(q )·cos(q +q )−0.072·sin(q )·sin(q +q )·cos(q )
1 5 4 2 3 1 2 3 5
−0.302·sin(q )·sin(q +q )+0.29·sin(q )·cos(q )+0.07·sin(q )·cos(q +q ) (10)
1 2 3 1 2 1 2 3
+0.072·sin(q )·sin(q )·cos(q ),
4 5 1
z = −0.29·sin(q )+0.072·sin(q )·sin(q +q )·cos(q )−0.07·sin(q +q )
2 5 2 3 4 2 3
(11)
−0.072·cos(q )·cos(q +q )−0.302·cos(q +q )+0.29,
5 2 3 2 3

Machines2023,11,167 6of19
forthelinearcoordinatesinthetoolspace,whereastheorientationisdefinedby:
φ = −1.0·(sin(q )·sin(q )+cos(q )·cos(q )·cos(q +q ))·sin(q )
1 4 1 4 2 3 5
(12)
−1.0·sin(q +q )·cos(q )·cos(q ),
2 3 1 5
θ =1.0·(−sin(q )·cos(q )·cos(q +q )+sin(q )·cos(q ))·sin(q )
1 4 2 3 4 1 5
(13)
−1.0·sin(q )·sin(q +q )·cos(q ),
1 2 3 5
and
ψ = −0.072·sin(q )·sin(q )·cos(q )·cos(q +q )
1 5 4 2 3
−0.072·sin(q )·sin(q +q )·cos(q )
1 2 3 5
(14)
−0.302·sin(q )·sin(q +q )+0.29·sin(q )·cos(q )
1 2 3 1 2
+0.07·sin(q )·cos(q +q )+0.072·sin(q )·sin(q )·cos(q )
1 2 3 4 5 1
Theaboveequationscanbetransformedinordertoobtainthejointvaluesforthegiven
positionandorientation. ThisishowtheHo–Cooktrajectoryplanningprocessiscapable
oftakingintoaccounttheorientationandtheposition,asthepointsthataredefinedasthe
pointsofthetrajectoryinvolveorientationaswellastheposition[x y z φ θ ψ][31].
The process of defining the Ho–Cook trajectory can then be followed by defining the
followingrelation:
 
3 + 2 t 0 ··· 0 0
t2 t3 4
 q˙ 2    t 1 3 2·(t 3 +t 4 ) t 5 ··· 0 0   
 q˙ 3  0 t 3 2·(t 4 +t 5 ) ··· 0 0 
  


. .
.




. .
.
. .
.
. .
.
... . .
.
. .
.


  
q m ˙−2   0 0 0 ··· t m−1 0  
q m ˙−1   0 0 0 ··· 2·(t m−2 +t m−1 ) tm t −1  
0 0 0 ··· t m−2 tm 2 −1 + t 3 m (15)
 
6(q −q )+ 3(q −q )
t2 2 1 t2 3 2
   t3 3 t4 [t2 3 (q 4 −q 3 )+ 3 t2 4 (q 3 −q 2 )]   
=  3 [t2(q −q )+t2(q −q )] 




tm−2
6
tm−1
[t2
m−
t4
2
t5
(q
m
4
−1
5
−q
m
4
−2
)+
5
t2
m
4
−1
(q
3
m−2
−q
m−3
)]




t
6
2 m
(q
m
−q
m−1
)+
t2 m
3
−1
(q
m−1
−q
m−2
)
Finally,thesegmentcoefficientsoftheHo–Cooktrajectoriesarethencalculatedusing
threedifferentequationsets. Thefirstsegmentcoefficientsarecalculatedas:
 1 0 0 −4 3 
t3 t4
2 2
[B 1 0B 1 1B 1 2B 1 3B 1 4] = [q 1 q 2 q˙ 1 q˙ 2 ]·     0 0 0 0 0 0 t 0 4 3 2 − 0 t 3 4 2     . (16)
 
0 0 0 −1 1
t2 t3
2 2
Thesegmentsbetweenthefirstandthelastonecanbecalculatedusing:
 1 0 − 3 2 
t2 t3
k+1 k+1
[B k 0B k 1B k 2B k 3] = [q k q k+1 q˙ k q k ˙ +1 ]·       0 0 0 1 − t2 k t 3 + k 2 + 1 1 − t2 k t 1 + 3 k 2 + 1 1       . (17)
0 0 − 1 1
tk+1 t2
k+1

Machines2023,11,167 7of19
Thefinalsegmentoftheinterpolatedtrajectorycanthenbedefinedas:
|      |        |         |      |                   |        |     |     |           |
| ---- | ------ | ------- | ---- | ----------------- | ------- | --- | --- | ---------- |
|      |        |         |      |                   | 1 0     | − 6 | 8   | − 3        |
|      |        |         |      |                   |         | t2  | t3  | t4         |
|      |        |         |      |                   |         | m   | m   | m          |
|      |        |         |      |                   |  0 0   | 6   | − 8 | 3         |
| 0    | 1 2    | 3       | 4    |                   |        | 2   | 3   | 4         |
| [B B | B      | B B     | ] =  | [q m−1 q q ˙−1 q˙ | ]·     | t m | t m | t m  (18) |
| m −1 | m −1 m | −1 m −1 | m −1 | m m               | m  0 0 | − 3 | 3   | 1         |
|      |        |         |      |                   |         | t2  | t2  | t3         |
|      |        |         |      |                   |        |     |     |           |
|      |        |         |      |                   |         |     | 2   | 2          |
|      |        |         |      |                   | 0 0     | 0   | 0   | 0          |
Theseequationsalsoallowforthecalculationofthejointpositionsandspeedsifthe
coefficientsareknown,whichwillbethefocusofthepapergoingforward. Themotion
oftherobotisonlylimitedbythenaturallimitationsoftheroboticmanipulatorathand
(forABBIRB120,firstjointinrange<−2.88,2.88>[rad],secondjoint<−1.92,1.92>[rad]
thirdjoint<−1.22, 1.92>[rad], fourthjoint<−2.79, 2.79>[rad], fifthjoint<−2.09, 2.09>
[rad],and<0,6.28>[rad]forthefinaljoint)[36],orotherrobotpositionalissues,suchas
singularities[37]. TheseissuescanbeaddressedwithintheGAbyartificiallyloweringthe
fitnessofthesolutionsthatareoutsideofthebonds.
2.2. GeneticAlgorithm
Ageneticalgorithm(GA)isanoptimizationalgorithmbasedonthenaturalevolution
process[38]. Thealgorithmworksbygeneratingapopulationofrandomlyselectedpoten-
tialsolutions[28]. Then,eachofthesesolutionsisevaluatedindividuallyaccordingtoa
pre-definedfunction: theso-calledfitnessfunction[39]. TheiteratingprocessoftheGA
thenstartsbyrandomlyselectingthepotentialsolutionsandperformingtheevolutionary
operationsonthem,whichgeneratesanewsolutionset[40]. Thisprocesswillrepeatuntil
asatisfactorysolutionisachieved[16]. Theprocessisbasedontheevolutionaryopera-
tions,ofwhich,therearethreeinGA:crossover,mutation,andreproduction. Crossover
wasperformedontwooftherandomlyselectedpotentialsolutions,andtheywerecom-
bined into a new solution [41]. This process allows for the newly generated solutions,
andwhentheinitialrandomselectionprocessisperformedbyweightingittowardsthe
better-performingsolutions,previousresearchshowsthatnewlygeneratedsolutionstend
towardtheoptimalsolution[42]. Still,therearetwoissuesthatthecrossoveroperation
can introduce: theconvergenceinto localoptima, and theloss of quality solutions [28].
Thefirstonewasaddressedbyintroducingthemutationoperation,whichwillrandomly
modifyasinglerandomlyselectedsolution. Thisallowsustocheckawiderareawithin
thepossiblesolutions[43]. Thelossofqualitysolutionsreferstothephenomenainwhicha
goodsolutionis,throughtheapplicationofcrossoverandmutation,replacedwithaworse
one. Toaddressthis,thereproductionoperationsimplytransferredaqualitysolutioninto
thenextsolutionset[44]. Fromtheabove,itcanbeconcludedthatmultiplevaluesneedto
bedefinedortestedtodefinehowtheGAwillbeapplied:
• Shapeofthepotentialsolutions;
• Thewayinwhichthecrossoverandmutationwillbeapplied;
• Theprobabilitieswithwhichtheevolutionaryoperationswilloccur;
• Thefitnessfunctionthatwillevaluatethesolutions;
• Thenumberofiterations(generations)ofthealgorithm;
• Thenumberofcandidatesolutionsinthealgorithm;
• Themannerofthesolutionselectionfortheoperations.
Eachoftheseelements,inthecontextofthepaper’sgoal,willbefurtherdiscussed.
2.2.1. SolutionConstruction
Theshapeoftheindividualsolutionsfirstneedstobedetermined,asitisthebasisfor
definingtheremainingelementsofGA.Inthediscussedproblem,itwasdecidedthata
six-pointtrajectorywouldbeused;inotherwords,fivesegmentsneedtobegeneratedin
theshapeofthevectorsB ,B ,B ,B ,B . Accordingtotheprevioussubsection,B andB
|     |     | 1   | 2 3 | 4 5 |     |     |     | 1 5 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
consistoffiveelementsandtheremainingonesconsistoffourelements. Forsimplicity,

Machines2023,11,167 8of19
alloftheseelementswerejoinedinasinglevectorthatcanbeusedfortheevolutionary
computationoperationsas:
B = [B0B1B2B3B4B0B1B2B3B0B1B2B3B0B1B2B3B0B1B2B3B4]. (19)
1 1 1 1 1 2 2 2 2 3 3 3 3 4 4 4 4 5 5 5 5 5
Each of the initial population candidate solutions were uniformly randomly filled
withvaluesintherangeof[−5,5]. Trajectorypointsweresetrandomly.
2.2.2. ApplicationofEvolutionaryComputingOperations
Thethreeaforementionedoperations—crossover,mutation,andreproduction—need
to be defined, as their manner of implementation is an important element. Each of the
operations also has a probability of occurring, with the previous research in the area
indicating that the probability of the crossover occurring should be very high (>80%),
whereasthemutationshouldbelow(<5%),withtheremainingiterationsbeingfulfilled
withthereproduction[45]. Reproductionisthesimplest,asitonlycopiesthepotential
solutionbetweenthegenerations. Itsoccurrencewassetto7%. Themannerinwhichthe
crossoverwasimplementedwastheso-calledrandomcrossover.AsshowninEquation(19),
eachofthesegmentshasanindividualset. Thealgorithmofcrossoverwasthenperformed
on two candidate solutions. For each of the five segments, one of the two candidate
solutionswasselected,anditssegmentwasinsertedintothenewsolution. Thisprocess
is shown in Figure 2. This yields a solution that is the combination of segments from
previoussolutions.
Figure2.Anillustrationoftherecombinationmethodologyused,where(A,B)representtwocandi-
datesolutionsselectedfromtheexistingpopulationand(C)presentstheresultingcandidatesolution
afterthecrossoverbetween(A)and(B)isperformed.
Thecrossoveroperationwasperformedwiththe90%probability.Finally,themutation
needs to be performed. The mutation will randomly replace an entire segment of the
randomlyselectedsolution,asshowninFigure3. Withoutthismechanic,duetohowthe
crossoveroperationisperformed,onlytheinitiallygeneratedsegmentsarepresentinallof
thegenerationsofthealgorithm. Theoccurrencerateofthisoperationwassetto3%.

Machines2023,11,167 9of19
2.2.3. TheFitnessFunction
Todeterminethequalityofthesolution,afitnessfunctionneedstobedetermined.
Suchafunctionshouldbesimpletocalculatetoallowforafastcalculationandexecution
ofthealgorithmwhileprovidingarealisticmetricoftheagentperformance[46]. Ascanbe
seeninthepreviousFigures2and3,thesegmentsgeneratedbytheGAarenotcontinuous
witheachother. Thisisoneofthemainpointsthatneedtobeaddressedwhentrajectory
planningisperformed,and,assuch,thiswasselectedtorepresentthemeasureofquality
forthecandidatesolution. AnillustrationofthesedistancesisgiveninFigure4.
Figure3. Anillustrationofthemutationmethodologyused,where(A)istherandomlyselected
candidatesolutionfromthepopulationand(B)istherandomlymodifiedsolution.
Figure4.Theillustrationofthefitnessfunction,whichisthesumofthedistancesbetweenthefirst
andthelastelementsofthesegments,asindicatedwithredarrows.
Tocalculatethis,thesumofalloftheverticaldistancesbetweenthesegmentswas
consideredandcalculated. Inotherwords,ifthelastvalueofsegmentB isgivenasB [i]
k k
andthefirstvalueofthefollowingsegmentB
k+1
isgivenasB
k+1
[0],thefitnessfunctionF
canbedefinedas:
4
∑
F = |B k [i]−B k+1 [0]|. (20)
k=0
Due to this being a minimization problem, the lower value of the fitness function
indicates a higher-quality solution. It is important to note that boundary conditions
need to be set. The initial testing showed that, when allowing the GA to minimize the
distancecompletely,solutionswilltendtoastationarytrajectory,withoutanymovement
amongstthesegments. Inotherwords,theelementsofthematrixgiveninEquation(19)
will converge to zero. As this is not the desired outcome, the boundary condition was
introduced. Theboundaryconditionstateddefinesthatallcandidatesolutionsmusthavea
totalsumofthetrajectoryparametersequaltoorhigherthanacertainvalue,whichwillbe
determinedthroughtesting. Allofthecandidatesolutionsthatdonotsatisfythiscondition
will be removed from the population, and replaced with another randomly generated
solutionthatdoessatisfytheaforementionedcondition.

Machines2023,11,167 10of19
2.2.4. CandidateSolutionSelection
ToachieveanimprovementacrossthegenerationsoftheGA,thecandidatesolutions
selectedfortheapplicationofevolutionaryoperationsneedtobeselectedwisely. Onlyif
thesolutionsselectedareofhighqualitycantheimprovementintheoverallpopulation
fitnessbeexpected. Toachievethis,afitnessproportionateselectionwasused. Thisrefers
to the type of randomized selection in which fitness is of a higher quality. The type of
fitnessproportionalselectionusedinthepresentedworkwastheso-calledroulettewheel
selection. Inthistypeofselection,theprobabilityofselectingacertaincandidatesolutionis
equaltoitsratiototheoverallfitness. IfthetotalfitnessisF andtheindividualfitness
total
ofcandidatesolution AisF ,thentheprobabilityofselectingitwouldbeequalto:
A
F
p = A . (21)
A F
total
Since,inthepresentedcase,thesmallerfitnessindicatesthebettersolution,theabove
method can be applied to calculating a vector that determines the probability of each
candidatesolution,sortedindescendingorder. Thecandidatesolution’sprobabilitiesare
thensortedinreverseorderandtheindividualprobabilityisassignedtoeach. Thisprocess
isillustratedinFigure5.
Figure5.Anillustrationoftheroulettewheelselectionprocess.Instep(1)thefitnessiscalculated
accordingtoEquation(20)(lowerisbetter).Then,in(2),theprobabilityiscalculatedasthepercentage
ofthetotalpopulationfitness(intheillustration,thetotalsumofindividualfitnessis3.0).Finally,
duetotheminimizationproblembeingobserved,theprobabilityvectorisinvertedin(3).
Withalloftheseelementsdefined,itcanbestatedthattheGAusedinthisresearchis
theGAbasedoncrossoverandmutationwiththeroulette-wheeltypeselectionandfixed
fitnessfunction[47].
2.3. Interpolation
Previously,whendiscussingthefitnessvalueusedduringthepresentedresearch,it
was mentioned that the lower bound needed to be set on the fitness that the solutions
canachieveinordertopreventthestationarysolutions. Thisapproachyieldssolutions
that will, even when optimized fully to the extent of the GA possibility, have vertical
gapsbetweensegments,meaningthatatrajectorygeneratedinsuchamannercannotbe

Machines2023,11,167 11of19
considered as continuous. To address this, an interpolation technique was introduced.
Asthelengthofeachsegmentisdefinedas1[s],thestartingandending0.1[s]ofeach
segmentweredeleted. Thefirstandfinalsegmentsonlyhadtheirfinalorinitial0.1[s]
elementremoved,respectively. Thisyieldsfourmissingsegments,withalengthof0.2s
thatneedtobeinterpolated.
Interpolationwasperformedusingsecond-degreeBeziersplines[48],definedas[49]:
x−t t −x
B i,k (x) = t i+k − i t i B i,k−1 (x)+ t i+ i+ k+ k+ 1 1 −t i+1 B i+1,k−1 (x), (22)
and
(cid:40)
B (x) = 1, x ∈ [t i ,t i+1 > (23)
i,0
0, otherwise.
Intheequations,tisthenumberofBeziersplinenodes,cisthecoefficientofthespline
determinedbasedonthevaluesofsegmentsbeingconnected,andkisthesplinedegree,
equalto2. Anexampleoftheresultconcerningthesplineisgiveninthefollowingsection.
3. ResultsandDiscussion
Inthissection,theresultsoftheappliedmethodologywillbediscussed. Theresults
in the process determination of boundary conditions for the obtained matrices will be
demonstratedandcommentedon,followedbytheresultsofGAparametertesting.
3.1. DeterminingtheOptimalBoundaryCondition
Asmentionedpreviously,theboundaryconditionsweresetastheminimalvalueof
thesumofallelementsofthecandidatesolutionvectorasgiveninEquation(19). Five
differentvaluesoftheboundweretested: noboundaryconditions,0.2,0.1,0.05,and0.005.
Forthetestingofthebound,thepopulationsizeofthecandidatesolutionsandthenumber
ofgenerationswerebothsetto10. Whiletheseparametervaluesaretoosmalltoachieve
anysignificantresults,asshownbyfurthertesting,theyperformwellenoughtoindicate
theperformanceoftheboundaryconditiontestedwithoutrequiringtoomuchexecution
time. Foreachofthetestsperformed, theresultswillbegivenasavisualizationofthe
best-performingcandidatesolutionattheendoftheoptimizationprocess(jointpositions,
speeds,andaccelerationsgiven),alongwithagraphshowingthechangeinthefitnessof
thebestsolutionthroughtheoptimizationprocess.
Thefirsttestwasperformedwithoutanyboundaryconditionset,andtheresultsare
showninFigure6.Ascanbeseen,thereareminimalmovementsoftheroboticmanipulator
present,withthejointmovementrangingfrom0.1to−0.25.
Figure6.Thebehaviorofthealgorithmwithoutsettingtheboundarycondition.Thebest-achieved
solutionisvisualizedonthe(left),andthefitnesschangethroughgenerationsisonthe(right).
Thefirstintroducedboundaryconditionhasavalueof0.2andtheresultsareshown
inFigure7. Here,itcanbeseenthattherangeofmovementishigher,but,observingthe

Machines2023,11,167 12of19
graph of fitness through generations, we can see that the value to which the algorithm
convergesisveryhigh.
Figure7. Thebehaviorofthealgorithmfortheboundaryconditionsetto0.2. Thebest-achieved
solutionisvisualizedonthe(left),andthefitnesschangethroughgenerationsisonthe(right).
Similarbutslightlyimprovedresultsareachievedwiththeboundsetto0.1,seenin
Figure8. Therangeofthemovementiskept,butthealgorithmconvergestoabetteroverall
solution. Theimprovedresultsachievedbysettingthisvalueindicatetheneedtocontinue
testinglowervalues.
Figure8. Thebehaviorofthealgorithmfortheboundaryconditionsetto0.1. Thebest-achieved
solutionisvisualizedonthe(left),andthefitnesschangethroughgenerationsisonthe(right).
Whentheboundaryconditionissettothevalueof0.05,thegraphsgiveninFigure9
indicatethatthemovementrangeiskeptwithafurtherimprovementintheconvergence
valueofoptimization,withthedistancesbetweensegmentsbelow0.05[rad]andtherange
ofmotionabove1.0[rad].
Figure9. Thebehaviorofthealgorithmfortheboundaryconditionsetto0.05. Thebest-achieved
solutionisvisualizedonthe(left),andthefitnesschangethroughgenerationsisonthe(right).

Machines2023,11,167 13of19
The final value for the boundary condition tested was 0.005, as demonstrated in
Figure10. Thisvalueshowsasimilarbehaviortotheconfigurationinwhichnoboundary
conditionisset. Thisindicatesthatvaluesthislowshouldnotbeconsidered.
Figure10.Thebehaviorofthealgorithmfortheboundaryconditionsetto0.005.Thebest-achieved
solutionisvisualizedonthe(left),andthefitnesschangethroughgenerationsisonthe(right).
The tests performed indicate that lowering the boundary condition improves the
resultsoftheGA,aslongastheconditionisnotsettoolow. Whentheconditionissettoo
low, theGAperformsinthesamemannerasitdoeswhennoconditionisset. Forthis
reason,theboundaryconditionof0.05wasselectedforfurthertesting.
3.2. DeterminingtheGAParameters
Aftertheboundaryconditionwasdeterminedandsetto0.05,themainparametersof
theGA—thepopulationsizeandthenumberofgenerationsthatthealgorithmwillrun
for—neededtobedetermined. Threeseparateconfigurationsweretested:
• Populationsizeof100executedfor100generations;
• Populationsizeof1000executedfor50generations;
• Populationsizeof10,000executedfor20generations.
Thefirstconfiguration,with100candidatesolutionsand100generations,istheleast
memory-intensive and computationally complex due to the fact that it has the lowest
populationvalue. Itisshowntoachieveafitnessfunctionof1.001,whichisnotsatisfactory
inthecontextoftheproblem. Theachievedsolutionshowsthelargedistancesbetween
multiplesectionsofthetrajectory. TheresultsarepresentedinFigure11.
Figure11.TheachievedresultsfortheGAwith100candidatesolutionstrainedfor100generations.
Thebest-achievedsolutionisvisualizedonthe(left),andthefitnesschangethroughgenerationsis
onthe(right).
Anincreaseinthepopulationsizeto1000yieldsasignificantincreaseinperformance,
evenwiththelowergenerationboundof50. AsshowninFigure12,thelowernumber
ofgenerationsdoesnotnegativelyaffecttheperformance,asthealgorithmisshownto

Machines2023,11,167 14of19
convergesignificantlybeforethefiftiethgeneration. Thelowestachievedfitnessfunction
valueis0.33,whichmaybeconsideredsatisfactory.
Figure12.TheachievedresultsfortheGAwith1000candidatesolutionstrainedfor50generations.
Thebest-achievedsolutionisvisualizedonthe(left),andthefitnesschangethroughgenerationsis
onthe(right).
Thefinaltestedconfigurationhas10,000candidatesolutionsandwasoptimizedfor
20generations,theresultsofwhichareshowninFigure13. Thetrendfromtheprevious
configurationcontinues,asthelargerconfigurationachievesasignificantlyimprovedresult
of0.098. TheGAconvergesbetweengenerations12and15,indicatingthat20generations
selectedforthisalgorithmareenoughforittoconverge,despitethelargerpopulationsize.
Figure13.TheachievedresultsfortheGAwith10,000candidatesolutionstrainedfor20generations.
Thebest-achievedsolutionisvisualizedonthe(left),andthefitnesschangethroughgenerationsis
onthe(right).
Todiscusstheoverallresults,itisshownthatanincreaseinpopulationsizeyields
significantperformanceincreases. The numberofgenerationsseemstohavelessofan
influence,andcanbemorelimitedinfurtherresearch,asthealgorithmtendstoconverge
toasolutionaroundthe15thgenerationinallofthetestedcases.
ExecutionTime
Animportantconsiderationfortheapplicationofalgorithmsistheexecutiontimes
ofthealgorithmsintestedconfigurations. Thetestswereperformedonallthepreviously
testedconfigurationsandaveragedacross10runs. Theconfigurationusedfortestingwas
alaptopcomputerwithCPUIntel(R)Core(TM)i7-1065G7CPU,withtheCPUclocklocked
at1.30GHzforthetest. Themachinewasequippedwith16GBofRAM.Thecodewas
executedinasingle-threadedmode. TheresultsofthetestaregiveninTable2.

Machines2023,11,167 15of19
Table2.Theexecutiontimesofvariousconfigurations,averagedovertenruns,withanaveragetime
pergenerationandthetotalexecutiontimegiven.
Population Generations TotalTime[s] AverageTimeperGeneration[s]
100 100 23.4 0.234
1000 50 119.5 2.39
10,000 20 403.4 20.17
Itcanbeseenthattheaveragetimepereachagentinthepopulationremainsrelatively
uniform(around2·10−3s). Thismeansthattheincreaseinpopulationsizehasasignificant
influenceonexecutiontimes. Thesmallestconfiguration,whichyieldsthepoorestresults,
finishestheexecutioninaroundtwentyseconds. Thetwofollowingconfigurationstake
almosttwominutes,orslightlybelowsevenminutes,respectively.
3.3. ResultIllustration
ThepathasgivenintheFigure14representsthemotionofthejointoverthecourseof
fivesecondsbetweenthepositionof−0.47[rad]to1.0[rad]. Thegeneratedpathissmooth,
withoutanysuddenchangesinthejointmotiondirection,owingtotheinterpolationac-
complishedwithBeziersplines. Someminorchangestothetorqueandnegativevibrations
maybepresentduetothechangesinthedirectionpresentbetweenthepoints,butasthese
transitionsaresmooth,theseeffectsshouldnotbeoverlynegativeonthemotionofthe
path. Themotionnotbeingmonotonousmayhaveanegativeeffectinthesenseofusing
moreenergythanwouldbenecessaryifmanuallytunedcoefficientswereused,butthis
negativeeffectshouldbeminorandoutweighedbythecomplexityofmanuallytuningthe
parameters,exceptinsituationswhereloweringtheenergyuseiscrucial. Themotionis
continuousthroughthepath,withoutdiscretepointsoftheHo–Cookmethodbeingclearly
visible. Anydelaysinthemovementshouldnotbepresentwiththegeneratedpath,asthe
entiregeneratedtrajectoryiscontinuous.
Figure14.Theillustrationoftheinterpolationprocess.
ThegeneratedtrajectorieswereappliedwithintheRobotStudiosoftwareinorderto
illustrateapossiblepathobtainedfromthemethod. Twenty-fivetrajectorypointswere
insertedintothesimulationwithinthesoftwareandthesimulationwasrun. Figure15
showstheinitial,sixth,twelfth,eighteenth,andfinal(twenty-fourth)trajectorypoints.

Machines2023,11,167 16of19
(a) (b)
(c) (d)
(e)
Figure 15. An illustration of the generated path. (a) The initial step of the simulated trajectory.
(b)Thesixthstepofthesimulatedtrajectory.(c)Thetwelfthstepofthesimulatedtrajectory.(d)The
eighteenthstepofthesimulatedtrajectory.(e)Thetwenty-fourthstepofthesimulatedtrajectory.
4. Conclusions
Inthispaper,theGAapproachtodeterminingHo–Cookalgorithmparameterswas
investigated. Theresultsofthisinvestigationpointtowardsthefactthatthisapproachis
avalidalternativetoanalyticallydeterminingtheHo–Cookcoefficients. Thisapproach
canbeusedinfurtherresearch,withadditionaloptimizationparameters,suchasenergy
efficiencyortorqueoptimizationforcontinuouspathplanning. Still,itisshownthatGAis
notcapableofgeneratingthefinaltrajectoriesbyitselfduetotheboundaryconditionsthat
needtobesetinordertoavoidstationaryresults,andBeziersplineinterpolationneeds
tobeutilizedtoaddressthis. Theinvestigationoftheparametersofthealgorithmshows
thatthealgorithmhasthebestperformancewhentheboundaryconditionissetto0.05and
thepopulationsizeissetto10,000. Thenumberofgenerationsdoesnotseemtoinfluence
theconvergencepoint,whichisshowntobebetween15and20generations,nomatter
thepopulationsize. Whiletheresultsaresatisfactorywithinthecontextoftheresearch,
theydonotparticularlyimprovethecurrentstate-of-the-artresultsintheresearch[13–27].
Still,asthereisaclearlackoftheHo–Cookalgorithmbeingusedforplanning,thevalue
of the achieved results lies in the fact that it can achieve results similar to the existing
ones,indicatingthatthereisroomforimprovementwhenmoreadvancedevolutionaryor
swarm-basedoptimizationalgorithmsareused. Theexecutiontimesofthealgorithmpoint
outthatitcannotbeusedinonlinereal-timeplanningascurrentlypresented, withthe
algorithmonlybeingusableinofflineplanning,wherethetrajectoriesaretunedbefore
theirapplicationinmanufacturing. Still, inthecurrentform, thealgorithmastestedis
executed in a single-threaded mode, and executing the algorithm on multiple threads
simultaneouslycouldsignificantlyimprovetheresults. Otherlimitationsconcerningthe
shownapproachincludetheneedtobefamiliarwiththeHo–Cookpathplanningalgorithm

Machines2023,11,167 17of19
inordertoapplytheGAdevelopedinthispaper,aswellasthegeneratedpathnotbeing
necessarilyoptimal,asonlyanear-optimalpathisguaranteedbytheGA.Pathplanningin
thedemonstratedmannerhascertainnaturallimitationswhencomparedtoothermethods
such as the dynamic position adjustment of robotic manipulator during the operation.
Thepathsplannedinthismannerareinflexibletolateradjustment,asthealgorithmneeds
tobere-runtoobtaintheadjustedpath.Thiscancauseissuesinwhichonlythekeychanges
aremadetothepaths(e.g.,newpathsarecalculated),asopposedtothecontinuoustuning
ofthepathsforahigherefficiency(productionandenergy-wise)[50]. Sometimes,detailed
pathplanningisunnecessaryandsimplytime-consumingcomparedtotheuseofsimple
trajectories generated by online path planning [51]. This manner of online movement
training is less skill-intensive compared to detailed offline path-planning, causing an
increaseinthecost[52]. Finally,fine-tunedofflineplannedpathssuchastheseareonly
applicableinpredictableenvironments,withalackofcapabilityindynamicplanning[53],
whichwouldtakeintoaccountthestochasticnatureoftherealisticenvironments. Therigid
planningsuchasthatpresentedcancauseafalsesenseofsecurity,asastaticenvironment
isintrinsicallyassumed,whichisrarelythecaseinrealproductionenvironments,where
issuesthatmaycausefaultsarerife[54].
Futureworkintheareashouldfocusonthetestingofotherevolutionaryalgorithms
on the framework developed for GA, such as differential evolution or particle swarm
optimization,todeterminewhetherthosealgorithmscanachievebetterresults.
AuthorContributions:Datacuration,S.B.Š.,N.A.;formalanalysis,N.A.,I.L.,Z.C.;fundingacqui-
sition,Z.C.;investigation,T.G.,S.B.Š.,M.G.;methodology,S.B.Š.,D.Š.,J.Š.;projectadministration,
Z.C.; resources, D.Š., J.Š.; software, T.G., S.B.Š.; supervision, I.L., Z.C.; validation, D.Š., J.Š., B.F.;
visualization,T.G.,M.G.;writing—originaldraft,T.G.,S.B.Š.,I.L.,M.G.;writing—reviewandediting,
N.A.,D.Š.,J.Š.,B.F.,Z.C.Allauthorshavereadandagreedtothepublishedversionofthemanuscript.
Funding:Thisresearchreceivednoexternalfunding.
InstitutionalReviewBoardStatement:Notapplicable.
InformedConsentStatement:Notapplicable.
DataAvailabilityStatement:Notapplicable.
Acknowledgments: Thisresearchhasbeen(partly)supportedbytheCEEPUSnetworkCIII-HR-
0108, European Regional Development Fund under the grant KK.01.1.1.01.0009 (DATACROSS),
projectCEKOMunderthegrantKK.01.2.2.03.0004,Erasmus+projectWICTunderthegrant2021-1-
HR01-KA220-HED-000031177,andUniversityofRijekascientificgrantsuniri-mladi-technic-22-61,
uniri-mladi-technic-22-57,uniri-tehnic-18-275-1447.
ConflictsofInterest:Theauthorsdeclarenoconflictofinterest.
References
1. Chen,H.;Fuhlbrigge,T.;Li,X. Automatedindustrialrobotpathplanningforspraypaintingprocess:Areview. InProceedingsof
the2008IEEEInternationalConferenceonAutomationScienceandEngineering,Washington,DC,USA,23–26August2008;
pp.522–527.
2. Raja,P.;Pugazhenthi,S. Optimalpathplanningofmobilerobots:Areview. Int.J.Phys.Sci.2012,7,1314–1320.[CrossRef]
3. Angeles,J.;Rojas,A.;Lopez-Cajun,C.S. Trajectoryplanninginroboticcontinuous-pathapplications. IEEEJ.Robot.Autom.1988,
4,380–385.[CrossRef]
4. Chettibi,T. Smoothpoint-to-pointtrajectoryplanningforrobotmanipulatorsbyusingradialbasisfunctions. Robotica2019,
37,539–559.[CrossRef]
5. Cowley,A.;Cohen,B.;Marshall,W.;Taylor,C.J.;Likhachev,M. Perceptionandmotionplanningforpick-and-placeofdynamic
objects. InProceedingsofthe2013IEEE/RSJInternationalConferenceonIntelligentRobotsandSystems,Tokyo,Japan,3–7
November2013;pp.816–823.
6. Khan,A.T.;Cao,X.;Li,Z.;Li,S. EvolutionaryComputationBasedReal-timeRobotArmPath-planningUsingBeetleAntennae
Search. EAIEndorsedTrans.AIRobot.2022,1,1–10.[CrossRef]
7. Draganjac,I.;Sesar,V.;Bogdan,S.;Kovacic,Z. Aninternet-basedsystemforremoteplanningandexecutionofSCARArobot
trajectories. InProceedingsofthe200834thAnnualConferenceofIEEEIndustrialElectronics,Orlando,FL,USA,10–13November
2008;pp.3485–3490.

Machines2023,11,167 18of19
8. Lengagne,S.;Mathieu,P.;Kheddar,A.;Yoshida,E. Generationofdynamicmotionsundercontinuousconstraints: Efficient
computationusingb-splinesandtaylorpolynomials. InProceedingsofthe2010IEEE/RSJInternationalConferenceonIntelligent
RobotsandSystems,Taipei,Taiwan,18–22October2010;pp.698–703.
9. Lian,J.;Yu,W.;Xiao,K.;Liu,W. Cubicsplineinterpolation-basedrobotpathplanningusingachaoticadaptiveparticleswarm
optimizationalgorithm. Math.Probl.Eng.2020,2020,1849240.[CrossRef]
10. Carrasco,J.;García,S.;Rueda,M.;Das,S.;Herrera,F. Recenttrendsintheuseofstatisticaltestsforcomparingswarmand
evolutionarycomputingalgorithms:Practicalguidelinesandacriticalreview. SwarmEvol.Comput.2020,54,100665.[CrossRef]
11. Bansal,J.C.;Singh,P.K.;Pal,N.R. EvolutionaryandSwarmIntelligenceAlgorithms;Springer:Berlin/Heidelberg,Germany,2019;
Volume779.
12. BaressiŠegota, S.; And¯elic´, N.; Lorencin, I.; Saga, M.; Car, Z. Pathplanningoptimizationofsix-degree-of-freedomrobotic
manipulatorsusingevolutionaryalgorithms. Int.J.Adv.Robot.Syst.2020,17,1729881420908076.[CrossRef]
13. Shukla,P.;Kumar,H.;Nandi,G.C. Roboticgraspmanipulationusingevolutionarycomputinganddeepreinforcementlearning.
Intell.Serv.Robot.2021,14,61–77.[CrossRef]
14. Ferigo,A.;Iacca,G.;Medvet,E. Beyondbodyshapeandbrain:Evolvingthesensoryapparatusofvoxel-basedsoftrobots. In
ProceedingsoftheInternationalConferenceontheApplicationsofEvolutionaryComputation(PartofEvoStar),VirtualEvent,
20–22April2021;Springer:Berlin/Heidelberg,Germany;pp.210–226.
15. Kim,J.;Ba,D.X.;Yeom,H.;Bae,J. Gaitoptimizationofaquadrupedrobotusingevolutionarycomputation. J.BionicEng.2021,
18,306–318.[CrossRef]
16. Liu,X.;Jiang,D.;Tao,B.;Jiang,G.;Sun,Y.;Kong,J.;Tong,X.;Zhao,G.;Chen,B. Geneticalgorithm-basedtrajectoryoptimization
fordigitaltwinrobots. Front.Bioeng.Biotechnol.2022,9,1433.[CrossRef]
17. Li,J.Y.;Zhan,Z.H.;Tan,K.C.;Zhang,J. Ameta-knowledgetransfer-baseddifferentialevolutionformultitaskoptimization. IEEE
Trans.Evol.Comput.2021,26,719–734.[CrossRef]
18. Martin,J.G.;Frejo,J.R.D.;García,R.A.;Camacho,E.F. Multi-robottaskallocationproblemwithmultiplenonlinearcriteriausing
branchandboundandgeneticalgorithms. Intell.Serv.Robot.2021,14,707–727.[CrossRef]
19. Hao,K.;Zhao,J.;Wang,B.;Liu,Y.;Wang,C. Theapplicationofanadaptivegeneticalgorithmbasedoncollisiondetectioninpath
planningofmobilerobots. Comput.Intell.Neurosci.2021,2021,5536574.[CrossRef]
20. Rahmaniar,W.;Rakhmania,A.E. MobileRobotPathPlanninginaTrajectorywithMultipleObstaclesUsingGeneticAlgorithms.
J.Robot.Control(JRC)2022,3,1–7.[CrossRef]
21. Song,B.;Wang,Z.;Zou,L.AnimprovedPSOalgorithmforsmoothpathplanningofmobilerobotsusingcontinuoushigh-degree
Beziercurve. Appl.SoftComput.2021,100,106960.[CrossRef]
22. Li,H.;Zhao,T.;Dian,S. Forwardsearchoptimizationandsubgoal-basedhybridpathplanningtoshortenandsmoothglobal
pathformobilerobots. Knowl.-BasedSyst.2022,258,110034.[CrossRef]
23. García,E.;Villar,J.R.;Tan,Q.;Sedano,J.;Chira,C. Anefficientmulti-robotpathplanningsolutionusingA*andcoevolutionary
algorithms. Integr.Comput.-AidedEng.2023,30,41–52.[CrossRef]
24. Yu,Z.;Duan,P.;Meng,L.;Han,Y.;Ye,F. Multi-objectivepathplanningformobilerobotwithanimprovedartificialbeecolony
algorithm. Math.Biosci.Eng.2023,20,2501–2529.[CrossRef]
25. Wu,L.;Huang,X.;Cui,J.;Liu,C.;Xiao,W. Modifiedadaptiveantcolonyoptimizationalgorithmanditsapplicationforsolving
pathplanningofmobilerobot. ExpertSyst.Appl.2023,215,119410.[CrossRef]
26. Lou,J.; Yu,X.; Chen,Y.; Sun,Z.; Zheng,P. RobotWeldingPathPlanningandApplicationBasedonGraphicalComputing.
InProceedingsoftheSeventhInternationalCongressonInformationandCommunicationTechnology;Springer: Berlin/Heidelberg,
Germany,2023;pp.597–605.
27. Li,J.;Zou,L.;Luo,G.;Wang,W.;Lv,C. Enhancementandevaluationinpathaccuracyofindustrialrobotforcomplexsurface
grinding. Robot.Comput.-Integr.Manuf.2023,81,102521.[CrossRef]
28. Deng,W.;Zhang,X.;Zhou,Y.;Liu,Y.;Zhou,X.;Chen,H.;Zhao,H. Anenhancedfastnon-dominatedsolutionsortinggenetic
algorithmformulti-objectiveproblems. Inf.Sci.2022,585,441–453.[CrossRef]
29. Zhou,J.;Huang,S.;Zhou,T.;Armaghani,D.J.;Qiu,Y. EmployingageneticalgorithmandgreywolfoptimizerforoptimizingRF
modelstoevaluatesoilliquefactionpotential. Artif.Intell.Rev.2022,55,5673–5705.[CrossRef]
30. Budi,H.S.;Elveny,M.;Zhuravlev,P.;Jalil,A.T.;Al-Janabi,S.;Alkaim,A.F.;Saleh,M.M.;Shichiyakh,R.A. Developmentofan
adaptivegeneticalgorithmtooptimizetheproblemofunequalfacilitylocation. Found. Comput. Decis. Sci. 2022,47,111–125.
[CrossRef]
31. Orsag,M.;Poropat,M.;Bogdan,S. Hybridfly-by-wirequadrotorcontroller. Automatika2010,51,19–32.[CrossRef]
32. Konjevic´,B.;Kovacˇic´,Z. CONTINUOUSJERKTRAJECTORYPLANNINGALGORITHMS. InProceedingsoftheInternational
ConferenceonInformaticsinControl,AutomationandRobotics,SCITEPRESS,Noordwijkerhout,TheNetherlands,28–31July
2011;Volume2,pp.481–489.
33. Konjevic´,B.;Puncˇec,M.;Kovacˇic´,Z. Twoapproachestoboundedjerktrajectoryplanning. InProceedingsofthe201212thIEEE
InternationalWorkshoponAdvancedMotionControl(AMC),Sarajevo,BosniaandHerzegovina,25–27March2012;pp.1–7.
34. Mocˇnik,G.;Kacˇicˇ,Z.;Šafaricˇ,R.;Mlakar,I. CapturingConversationalGesturesforEmbodiedConversationalAgentsUsingan
OptimizedKaneda–Lucas–TomasiTrackerandDenavit–Hartenberg-BasedKinematicModel. Sensors2022,22,8318.[CrossRef]

Machines2023,11,167 19of19
35. Shim,S.;Lee,S.;Joo,S.;Seo,J. Denavit-HartenbergNotation-BasedKinematicConstraintEquationsforForwardKinematicsof
the3–6StewartPlatform. J.Mech.Robot.2022,14,054505.[CrossRef]
36. BaressiŠegota,S.; And¯elic´,N.; Šercer,M.; Meštric´,H. DynamicsModelingofIndustrialRoboticManipulators: AMachine
LearningApproachBasedonSyntheticData. Mathematics2022,10,1174.[CrossRef]
37. Milenkovic,P.;Wang,Z.;Rodriguez,J.I. Encounteringsingularitiesofaserialrobotalongcontinuouspathsathighprecision.
Mech.Mach.Theory2023,181,105224.[CrossRef]
38. Katoch,S.;Chauhan,S.S.;Kumar,V. Areviewongeneticalgorithm: Past,present,andfuture. Multimed. ToolsAppl. 2021,
80,8091–8126.[CrossRef]
39. Han,S.;Xiao,L. Animprovedadaptivegeneticalgorithm. SHSWebConf.2022,140,01044.[CrossRef]
40. Wang,B.;Yao,X.;Jiang,Y.;Sun,C.;Shabaz,M. Designofareal-timemonitoringsystemforsmokeanddustinthermalpower
plantsbasedonimprovedgeneticalgorithm. J.Healthc.Eng.2021,2021,7212567.[CrossRef]
41. Ibrahim, M.; Nurhakiki, F.; Utama, D.; Rizaki, A. Optimised genetic algorithm crossover and mutation stage for vehicle
routingproblempick-upanddeliverywithtimewindows. InProceedingsoftheIOPConferenceSeries:MaterialsScienceand
Engineering,Sanya,China,12–14November2021;Volume1071,p.012025.
42. Damia,A.;Esnaashari,M.;Parvizimosaed,M. AdaptiveGeneticAlgorithmBasedonMutationandCrossoverandSelection
Probabilities. InProceedingsofthe20217thInternationalConferenceonWebResearch(ICWR),Tehran,Iran,19–20May2021;
pp.86–90.
43. Saadaoui,D.;Elyaqouti,M.;Assalaou,K.;Lidaighbi,S. ParametersoptimizationofsolarPVcell/moduleusinggeneticalgorithm
basedonnon-uniformmutation. EnergyConvers.Manag.X2021,12,100129.[CrossRef]
44. Sohail,A. Geneticalgorithmsinthefieldsofartificialintelligenceanddatasciences. Ann.DataSci.2021,1–12.[CrossRef]
45. Bhattacharjee, P.; Jana, R.K.; Bhattacharya, S. AComparativeStudyofDynamicApproachesforAllocatingCrossoverand
MutationRatiosforGeneticAlgorithm-basedOptimizationofWindPowerGenerationCostinJafrabadRegioninIndia. In
ProceedingsoftheInternationalConferenceon“RecentAdvancementsinScience,Engineering&Technology,andManagement,
Nagpur,India,25–26March2021.
46. Avdeenko,T.;Serdyukov,K.GeneticAlgorithmFitnessFunctionFormulationforTestDataGenerationwithMaximumStatement
Coverage. InProceedingsoftheInternationalConferenceonSwarmIntelligence,Qingdao,China,17–21July2021;Springer:
Berlin/Heidelberg,Germany,2021;pp.379–389.
47. Fogel,D.B. Evolutionaryalgorithmsintheoryandpractice.Complexity1997,2,26–27[CrossRef]
48. Liu,J.;Jin,B.;Yang,J.;Xu,L.SeasurfacetemperaturepredictionusingacubicB-splineinterpolationandspatiotemporalattention
mechanism. RemoteSens.Lett.2021,12,478–487.[CrossRef]
49. Tayebi,S.; Momani,S.; Arqub,O.A. ThecubicB-splineinterpolationmethodfornumericalpointsolutionsofconformable
boundaryvalueproblems. Alex.Eng.J.2022,61,1519–1528.[CrossRef]
50. Gigras,Y.;Gupta,K. Artificialintelligenceinrobotpathplanning. Int.J.SoftComput.Eng.(IJSCE)2012,2,2231–2307.
51. Liu,M. Roboticonlinepathplanningonpointcloud. IEEETrans.Cybern.2015,46,1217–1228.[CrossRef]
52. Xie,Z.;Zhang,Q.;Jiang,Z.;Liu,H. Robotlearningfromdemonstrationforpathplanning:Areview. Sci.ChinaTechnol.Sci.2020,
63,1325–1334.[CrossRef]
53. Bonny,T.;Kashkash,M. HighlyoptimizedQ-learning-basedbeesapproachformobilerobotpathplanninginstaticanddynamic
environments. J.FieldRobot.2022,39,317–334.[CrossRef]
54. And¯elic´, N.; Car, Z.; Šercer, M. Neural Network-Based Model for Classification of Faults During Operation of a Robotic
Manipulator. Teh.Vjesn.2021,28,1380–1387.
Disclaimer/Publisher’s Note: The statements, opinions and data contained in all publications are solely those of the individual
author(s)andcontributor(s)andnotofMDPIand/ortheeditor(s).MDPIand/ortheeditor(s)disclaimresponsibilityforanyinjuryto
peopleorpropertyresultingfromanyideas,methods,instructionsorproductsreferredtointhecontent.