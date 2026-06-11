Article
Building Disaster Resilience: A Sustainable Approach to
Integrated Road Rehabilitation and Emergency Logistics
Optimization in Extreme Events
BochenWang*,ChangpingHe andYuhanGuo
SchoolofEconomicsandManagement,ShanghaiUniversityofElectricPower,Shanghai201306,China;
changping3dawn@163.com(C.H.);13402447808@163.com(Y.G.)
* Correspondence:websterchen@163.com
Abstract
Theincreasingfrequencyandintensityofextremedisasters,exacerbatedbyclimatechange,
posesignificantchallengestosustainabledevelopmentbydisruptingcriticalinfrastructure
andhamperingreliefefforts. Enhancingdisasterresilience—acoreobjectiveofsustainable
development—requiresintegratedapproachesthatsimultaneouslyaddressinfrastructure
restorationandefficientresourceallocation. Thisstudyproposesasustainableoptimiza-
tionframeworkforpost-disasterresponse,integratingroadrehabilitationdecisionswith
emergency logistics planning within a three-tier supply chain network. We develop a
mathematical model that synergistically optimizes repair crew scheduling, depot loca-
tion,andvehiclerouting,withtheobjectiveofmaximizingacomprehensivesatisfaction
indexthatbalancestimelydelivery(timesatisfaction)andfulfillmentofmaterialneeds
(demandsatisfaction). Thisintegratedapproachdirectlycontributestosustainabledisaster
AcademicEditor:BinJi managementbyensuringmorereliableandequitableaccesstovitalresourcesinaffected
Received:16October2025 communities. Atailoredvariableneighborhoodsearchalgorithmisdesignedtosolvethe
Revised:17November2025 modelefficiently,asdemonstratedthroughlarge-scalenumericalexperiments.Ourfindings
Accepted:24November2025 highlightseveralpolicy-relevantinsightsforsustainableemergencyplanning: adequate
Published:26November2025
budgetingiscrucialforuninterruptedreliefoperations;strategicinvestmentsinrapidroad
Citation: Wang,B.;He,C.;Guo,Y. repaircapabilitiesorvehiclefleetssignificantlyenhancesystemefficiency;andprioritizing
BuildingDisasterResilience:A
timesatisfaction(rapidresponse)yieldsgreateroverallbenefitsthanmerelyincreasing
SustainableApproachtoIntegrated
deliveredquantities.Furthermore,restoringcriticalroadinfrastructureisshowntomitigate
RoadRehabilitationandEmergency
transportationuncertainties,therebystrengtheningtheresilienceoftheentirereliefsystem.
LogisticsOptimizationinExtreme
Events.Sustainability2025,17,10591. Thisworkprovidesaquantifiablemethodologyandpracticaldecisionsupporttoolsfor
https://doi.org/10.3390/ buildingmoresustainableandresilientcommunitiesinthefaceofdisasters.
su172310591
CorrectionStatement:Thisarticlehas Keywords: disasterresilience;sustainableemergencylogistics;roadrestoration;variable
beenrepublishedwithaminorchange. neighborhoodsearch;humanitariansupplychain;emergencyresponse
Thechangedoesnotaffectthescientific
contentofthearticleandfurtherdetails
areavailablewithinthebackmatterof
thewebsiteversionofthisarticle.
1. Introduction
Copyright:©2025bytheauthors.
Inrecentyears, theintensificationofglobalclimatechangehasledtothefrequent
LicenseeMDPI,Basel,Switzerland.
occurrenceofextremenaturaldisasters,suchasearthquakes,floods,hurricanes,andother
Thisarticleisanopenaccessarticle
catastrophicevents,whichnotonlycausemajorcasualtiesandpropertydamagebutalso
distributedunderthetermsand
conditionsoftheCreativeCommons causedevastatingdamagetoinfrastructuresystems. Afteradisaster,thelarge-scalede-
Attribution(CCBY)license structionofroadnetworksoftenleadstotheinterruptionofthe‘lifeline’,whichseriously
(https://creativecommons.org/ hampersthetransportofemergencysuppliesandtheimplementationofrescueoperations.
licenses/by/4.0/).
Sustainability2025,17,10591 https://doi.org/10.3390/su172310591

Sustainability2025,17,10591 2of28
Accordingtothestatistics,inthe2008Wenchuanearthquake,thedamagerateofroadsin
thedisasterareawasashighas70%ormore,andasaresult,about30%oftheaffectedarea
duringthe72hgoldenrescueperiodcouldnotgettimelyrescue;thetsunamitriggeredby
the2011TohokuearthquakeinJapancausedmorethan4000roaddamages,whichreduced
theefficiencyofpost-disasterdistributionofmaterialsby60%. The2023earthquakein
Turkeyledtothedestructionof100,000kmofroads,andthe2021earthquakeinHenan
Provinceledtothedestructionof100,000kmofroads. Casessuchasthedestructionof
100,000kmofroadscausedbythe2023Turkeyearthquakeandtheparalysisofthetransport
networkcausedbytheheavyrainfallinHenanprovincein2021showthatthepost-disaster
emergencyresponsesystemisfacingthedualchallengesofroadinfrastructuredestruction
andsurgingdemandformaterials. Inthiscontext,determininghowtoachievethesyner-
gisticoptimizationofroadrepairandemergencymaterialdistributionthroughscientific
decision-makingmethodshasbecomeakeyscientificissuetoenhancethetimelinessof
emergencyrescueandsafeguardthelivesandpropertiesofaffectedpeople. Inextremedis-
astersituations,theemergencylogisticssystemmainlyfacesthreecorechallenges: (1)the
sharpdeclineintrafficaccessibilityduetodamagedroadnetworks;(2)thedynamicspatial
andtemporalcharacteristicsofthedemandformaterialsatthedisastersite;and(3)the
severeshortageofrescueresources(includingmaintenanceteams,transportvehicles,etc.).
Existingstudiestendtotreattheroadrehabilitationproblemandthematerialdistribu-
tion problem separately, ignoring the dynamic coupling relationship between the two.
Specifically,theroadrehabilitationdecisiondirectlyaffectstheconnectivityofthetransport
network, which, in turn, constrains the choice of material distribution paths; while the
urgencyofmaterialdistributioninturndeterminesthepriorityofroadrehabilitation. This
complex interaction makes it difficult to optimize either link individually to maximize
theoverallrescueefficiency. Therefore,itisofgreattheoreticalandpracticalsignificance
toestablishasynergisticoptimizationframeworkforroadrehabilitationandemergency
materialdistributiontoimprovetheemergencyrescueefficiencyatthesystemlevel.
In the field of emergency logistics research, many scholars have carried out an in-
depth exploration of the emergency warehouse location path problem (LRP). Existing
studiesmainlyfocusedonkeyfactorssuchasmaterialdemand[1–3],transporttimeuncer-
tainty[4,5],androadconditionuncertainty[6,7]. AliakbariandKomijan[8]constructed
ascenario-based robustoptimization modelbyconsideringthe uncertaintyofdemand
andtransporttime;Khanchehzarrinetal.[9]addressedtheuncertaintyofrescuematerial
demand,inventorylevel,andpriorityuncertaintiesandbuiltamulti-objectivetwo-layer
stochasticplanningmodel. Intermsofemergencysuppliesdistribution,Vidaletal.[10]
constructedanoptimization modelwiththeobjectiveofthe shortestdispatchdistance,
whileRahafroozandAlinaghian[11]proposedamulti-objectiverobustoptimizationmodel
thattakesintoaccountfairness,distributionrisk,andlogisticscost. Thesestudiesprovide
an important theoretical foundation for coping with material distribution problems in
extremedisasters. However,thereareobviouslimitationsintraditionalemergencylogistics
research. Generallyspeaking,themainshortcomingsoftheexistingstudiesareasfollows:
(1) road repair and material distribution are regarded as independent decision-making
processes,resultingininsufficientspatialandtemporalsynergybetweentherepairscheme
andthetransportpath;(2)thereisalackofanin-depthexplorationofthedifferentiated
treatmentof‘softandhardtimewindows’undertheconstraintsofthetimewindow;and
(3)themechanismoftheinfluenceofthedegreeofroadrepairontheuncertaintyofthe
transporttimehasnotyetbeenanalyzedinasystematicway. Theselimitationsseriously
restricttheoverallefficiencyofemergencyresourceallocation.
Thisstudyaddressestheabovetheoreticalgapsandinnovativelyproposesasyner-
gisticoptimizationframeworkforroadrehabilitationandemergencymaterialdistribu-

Sustainability2025,17,10591 3of28
tion. The breakthroughs that distinguish it from the existing literature are reflected in
threedimensions: (1)constructingathree-levelemergencymaterialdistributionnetwork
(emergencymaterialreservedepot-transitcenter-disastersite),embeddingroadrehabil-
itation decision variables into a site-path optimization model, and realizing integrated
decision-making between infrastructure rehabilitation and logistics resource allocation;
(2)introducingatimesatisfactionfunctiontoquantifytheurgencydifferencesofthecon-
straintsindifferenttimewindowsandcombiningthedemandformaterialstoestablish
abi-objectiveoptimizationmodel,whichbalancestimelinessandfairnessbyweighting
the comprehensive satisfaction index; (3) develop an improved variable neighborhood
search algorithm (VNS), which adopts an initial solution generation strategy based on
clusteranalysisandiscombinedwithanadaptiveneighborhoodswitchingmechanism
to enhance the solution efficiency of large-scale arithmetic cases. These innovations ef-
fectivelysolvethekeyproblemsoftraditionalmethods,suchasthefragmentationofthe
‘repair-distribution’decision,thesinglesatisfactionevaluation,andthelackofalgorithm
scalability. Thisstudyadoptsthemethodologicalsystemof‘problemmodeling–algorithm
development–experimentalanalysis’. First,amixed-integerplanningmodelisconstructed
withthegoalofmaximizingcomprehensivesatisfaction,whichinnovativelyintroducesthe
couplingconstraintsbetweenroadrepairstatevariablesandmaterialdistributionpathvari-
ables. Then,avariableneighborhoodsearchalgorithmintegratingagreedyinitialization
strategyisdesigned,whichdynamicallyadjuststheneighborhoodstructuretobalancethe
breadthanddepthofthesearch. Finally,sensitivityanalysisisconductedviaorthogonal
experimentstosystematicallyinvestigatetheinfluenceofkeyparameters—suchasbudget
constraints,maintenancecapacity,andthenumberofvehicles—onsystemperformance.
Inparticular,thisstudywillverifytheimportanthypothesisthat‘roadrepairprogressis
negativelycorrelatedwithtransporttimeuncertainty’,therebyprovidingascientificbasis
fortheformulationofhierarchicalrescuestrategies.
Thesubsequentchaptersofthisstudyarearrangedasfollows: Section2providesa
reviewoftherelatedresearchprogress;Section3elaboratesupontheconstructionprocess
ofthecollaborativeoptimizationmodel;Section4introducesthedesignprincipleofthe
variableneighborhoodsearchalgorithm;Section5verifiesthevalidityofthemodeland
algorithmthroughnumericalexperiments;Section6analyzesthedegreeofinfluenceof
eachuncertainparameteronthetargetvaluethroughsensitivityanalysis;andSection7
summarizestheresearchresultsandhighlightsfuturedirections. Throughthissystematic
research,weexpecttocontributenewsolutionstoenhancetheemergencyrescuecapability
underextremedisasters.
2. LiteratureReview
In recent years, with the intensification of global climate change, extreme natural
disasters(e.g.,earthquakes,floods,hurricanes,etc.)havebeenoccurringfrequently,causing
seriousdamagetohumansocietyandinfrastructure. Afteradisasteroccurs,roaddamage
andmaterialshortagesoftenbecomethekeyfactorsrestrictingtheefficiencyofemergency
relief. Determininghowtoefficientlyrepairdamagedroadsandoptimizethedistribution
pathofemergencymaterialsunderlimitedtimeandresourceconditionshasbecomean
importantresearchtopicinthefieldofemergencylogisticsmanagement. Inthispaper,
wesystematicallysortouttheexistingresearchonthetwoaspectsofroadrepairunder
extremedisastersandoptimizationofemergencymaterialdistributionandpointoutthe
shortcomingsoftheexistingresearchandtheinnovationsofthisresearch.

Sustainability2025,17,10591 4of28
2.1. ResearchonRoadRepairUnderExtremeDisasters
The destructive impact of extreme disasters on roads often leads to serious traffic
disruption,affectingthetimelydistributionofrescuematerials. Toaddresstheproblem
ofemergencymaterialdistribution,theintroductionofroadrehabilitationresearchunder
extremedisasterscanensurethetimelydeliveryofreliefmaterialstothevictims. Rawls
andTurnquist[12]proposedatwo-phaseemergencyfacilitysitingmodelinresponseto
the uncertainty of the material demand and road damage in earthquake disasters. Du
andYi[13]believedthatthetimelinessoftheemergencylogisticsiscrucialand,therefore,
proposedtheemergencylogisticsvehiclepathmodelbasedonroadnetworkfailureand
solveditusingageneticalgorithm. Brunietal.[14]conductedariskassessmentofthe
roadnetworkaccessstateafteradisasterinordertoimprovethesafetyandreliabilityof
thevehiclepathschemeandproposedanemergencylogisticsmodelwiththeobjective
ofminimizingthedistributiontime,whichwassolvedusinganiterativegreedyheuristic
algorithm. Qiupingetal.[15]proposedahybridmeta-heuristicalgorithmforassessing
the reliability of road networks with different levels of damage. Sanci and Daskin [16]
proposedatwo-levelstochasticplanningmodelforemergencyresponsewiththeobjective
ofminimizingthetotalcost,consideringtheuncertaintyindemand,roaddamagerate,and
repairtimeandsolveditusinganintegerL-shapealgorithm. AslanandÇelik[17]assumed
infiniterepairresourcesandpresetasubsetofpathcandidatestodescribetheroadaccess
stateusingprobabilitydistributions,proposedatwo-stagestochasticplanningmodelwith
theobjectiveofminimizingthetotalrelieftime,andsolveditusingtheSampleAverage
Approximation(SAA)method. YuanandWang[18],alsotakingintoaccountthetraveling
timefactor,constructedasingle-objectivepathselectionmodelthatpursuestheshortest
travelingtime,incorporatingatime-varyingspeedconstrainttoreflecttrafficcongestion.
Khorsietal.[19]constructedamixed-integerplanningmodeltostudythedistributionof
emergencyrescueresourcesunderdamagedroadconditionsandthepathoptimizationand
decision-makingoftheemergencylogisticsdistributionpathandpathselectionproblem,
takingintoaccountthethreeaspectsofrescueefficiency,rescuefairness,andeffectiveness.
HuangandSong[20]pointedoutthatinthestudyofemergencylogisticsproblems,the
variablesthataredifficulttodetermineareusuallyestimatedbyexperts,andinviewofthe
unavailabilityofhistoricaldataofsomeparametersinemergencyevents,anemergency
logistics distribution path optimization model is constructed based on the uncertainty
theory. Ozdamar et al. [21] presented a constructive heuristic method for generating
roadsidedebriscleanupplansinpost-disasterroadrecovery,whichaimedtomaximize
cumulative network accessibility throughout the cleanup operation and minimize the
makespan. Changetal.[22]studiedtheemergencylogisticsproblemwithinformation
uncertaintyinthecontextoffloodinginordertoachieveareasonabledistributionofrescue
materials,usingArcGISDesktop(version10.8)software,basedonthepotentialmapofthe
floodedareatoobtainanestimateofthepossiblelocationoftheaffectedpointsandthe
numberofemergencyresources,toconstructtwostochasticplanningmodelsthatcanbe
effectivelyusedintheactualrescue,andtoimprovetheworkoftherelevantdepartments
oftheemergencyrelieftoprovideareferencebasis.
2.2. ResearchontheOptimizationofEmergencyMaterialDistribution
Emergencylogisticsisaspeciallogisticsactivitythatemphasizestimeefficiencyand
relatively weak economic efficiency, distinguishing it from ordinary commercial logis-
tics. Rescueoperationsinsuddennaturaldisasters,socialhazards,epidemics,andother
catastrophiceventsneedtorelyonthesupportofemergencylogistics. Theemergency
logisticspathproblemisaresearchhotspotinthefieldofemergencymanagement. Itwas
firstproposedbyDantzigandRamser[23],anditsmainresearchobjectiveistotransport

Sustainability2025,17,10591 5of28
materialsfromadistributioncentertocustomerpointswithdifferentneedsbyvehicles
andtoplanareasonablerouteforeachtransportvehicleunderthepremiseofmeetingall
transportrequirements.Vahdanietal.[24]andothersconstructedamulti-vehicleyardpath
optimizingtheminimizationofthetransporttimeofthematerialswiththemaximization
ofthesafetyoptimizationmodelandusedameta-heuristicalgorithmwithgoodresults
tosolvethismulti-objectiveoptimizationproblem. Chang[25]constructedanemergency
logisticsvehiclepathoptimizationmodelwiththeobjectivefunctionofmaximizingtime
satisfactionandverifiedtheeffectivenessofthemodelbycombiningahybridapproachofa
geneticalgorithmandanantcolonyalgorithm. Gao[26]definedthe‘costofunsatisfactory’
asanunsatisfieddemandandanoversupplyofmaterialsanddesignedatwo-levelhybrid
materialschedulingmodelwiththeshortesttotaltimeandthesmallestunsatisfiedcost
astheoptimizationobjectives. LiuandXie[27]carriedoutanexhaustiveanalysisofthe
availableinformationandtheroadnetworkaftertheearthquakedisastertoconstructa
dynamicoptimizationmodel,basedonwhichthecorrespondingresourceperformance
can be derived and the purpose of which is to achieve the maximum rescue efficiency.
Qinetal.[28]alsostudiedthedistributionproblemoflimitedrescueresources,focusing
ontheimpactofaninsufficientsupplyofmaterialsanduncertaindemandontherescue
effectwithin72hafteradisaster,consideringbothaninsufficientquantityofmaterials
anduncertaindemandinthemodel,focusingontherationalplanningofrescueroutes,
and improving the utilization rate of limited materials. Ahmadi-Javid [29] proposed a
mixed-integer planning LRP model with the objective of minimizing the total cost and
solved it using a two-stage heuristic algorithm. Lars et al. [30] proposed a three-stage
stochasticoptimizationmodelforemergencylogisticssitingdistribution,inwhichthefirst
stageisforthesitingstudyandthesecondandthirdstagesaredesignedforthescheduling
ofthematerialsundertheuncertaintyconditions. Shenetal.[31]proposedanemergency
logistics siting-path optimization model considering the environmental cost of carbon
emissionandusedatwo-stagehybridalgorithmofparticleswarmandforbiddensearchto
solvetheproblem. Xuetal.[32]proposedanemergencylogisticssiting-pathmodelunder
multipleconstraintsfortheurbanevacuationsitingprobleminanearthquakedisaster.
2.3. ResearchGaps
This study provides a systematic review and comparative analysis of the existing
literature, as detailed in Table 1. It identifies the following three limitations in the cur-
rentresearch: (1)intermsofmodelconstruction,existingstudiestendtoseparateroad
repairdecisionsandemergencymaterialdistributionnetworkdesign,lackingadynamic
integrated framework for their collaborative optimization; (2) in terms of optimization
objectives, the interactive influence mechanism between time satisfaction and demand
satisfactionhasnotbeenfullyconsidered;and(3)intermsofalgorithmdesign,existing
solutionmethodsfacecomputationalefficiencybottleneckswhendealingwithlarge-scale
post-disasteremergencylogisticsproblems.
Toaddresstheseresearchgaps,thispapermakesthefollowinginnovativecontributions:
(1) Itproposesathree-levelemergencymaterialcollaborativeoptimizationmodelinte-
gratingroadrepairdecisions,innovativelyincorporatingrepairpathselection,transfer
warehouselocationselection,andmulti-vehicleroutingplanningintoaunifiedframe-
workforjointoptimization,breakingthroughthelimitationsofsubsystemseparation
optimizationintraditionalresearch;
(2) Itconstructsadualsatisfaction-drivenmulti-objectiveoptimizationfunction,quanti-
fyingthedifferentialcontributionsoftimesatisfaction(materialdeliverytimeliness)
anddemandsatisfaction(materialallocationfairness)tooverallrescueeffectiveness
byintroducingaweightadjustmentmechanism;

Sustainability2025,17,10591
6of28
(3) Itdesignsahybridintelligentalgorithmbasedonimprovedvariableneighborhood
search(VNS),combiningaparametersensitivityanalysismethodtosystematically
reveal the impact mechanisms of key parameters, such as budget constraints and
repaircapacity,onsystemperformance.
Table1.Differencesintheliterature.
|      |                    | UncertaintyFactors |       | Decision |           |           |
| ---- | ------------------ | ------------------ | ----- | -------- | --------- | --------- |
|      |                    |                    |       |          | ModelType | Algorithm |
| Ref. | Reference          |                    |       |          |           |           |
|      |                    | AT AL              | DR RC | C UC     |           |           |
|      |                    |                    | √ √   | √        |           |           |
| [12] | RawlsandTurnquist. |                    |       |          | LP        | TS        |
√ √ √
| [13] | DuandYi        | √   | √   | √   | LP   | ACO |
| ---- | -------------- | --- | --- | --- | ---- | --- |
| [14] | Brunietal.     |     |     |     | MILP | GA  |
|      |                | √   | √ √ | √   |      |     |
| [15] | Qiupingetal.   |     |     |     | LP   | GA  |
|      |                | √   | √   | √   |      |     |
| [16] | SanciandDaskin |     |     |     | MILP | BD  |
√ √ √
| [17] | AslanandÇelik    |     |     |     | MILP  | B&P |
| ---- | ---------------- | --- | --- | --- | ----- | --- |
|      |                  | √   | √ √ | √   |       |     |
| [18] | YuanandWang      | √   | √ √ | √   | MILP  | ASM |
| [19] | Khorsietal.      |     |     |     | MINLP | GA  |
|      |                  | √   |     | √   |       |     |
| [20] | HuangandSong     |     |     |     | FMO   | GA  |
|      |                  | √ √ | √   | √   |       |     |
| [21] | Changetal.       |     |     |     | LP    | ASM |
|      |                  | √ √ |     | √   |       |     |
| [23] | DantzigandRamser |     |     |     | LP    | ASM |
|      |                  | √   | √ √ | √   |       |     |
| [24] | Vahdanietal.     | √ √ | √   | √   | LP    | TS  |
| [25] | Chang            |     |     |     | LP    | ACO |
|      |                  | √   | √   | √   |       |     |
| [26] | Gao              |     |     |     | MILP  | ASM |
|      |                  | √ √ | √   | √   |       |     |
| [27] | LiuandXie        | √ √ | √   | √   | MILP  | TS  |
| [28] | Qinetal.         |     |     |     | MILP  | ACO |
|      |                  | √ √ |     | √   |       |     |
| [29] | Ahmadi-Javid     | √   | √   | √   | MILP  | VNS |
| [30] | Larsetal.        |     |     |     | MILP  | ASM |
|      |                  | √ √ | √   | √   |       |     |
| [31] | Shenetal.        |     |     |     | BLPM  | GA  |
|      |                  | √   | √ √ | √   |       |     |
| [32] | Xuetal.          | √ √ | √ √ | √   | MINLP | GA  |
| -    | Thisstudy        |     |     |     | MILP  | VNS |
Note: AT: Accident time; AL: Accident location; DR: Demand resources; RC: Road condition; C: Certain;
UC:Uncertain; LP:Linearprogramming; MILP:Mixed-integerlinearprogramming; MINLP:Mixed-integer
non-linearprogramming;FMO:Fuzzymulti-objective;BLPM:Bi-levelprogrammingmodel;TS:Tabusearch;
ACO:Antcolonyoptimization;GA:Geneticalgorithm;BD:Bendersdecomposition;B&P:Branch-and-price;
ASM:Activesetmethod;VNS:Variableneighborhoodsearch.
TheVNSalgorithmhasbeenwidelyappliedinresearchoncombinatorialoptimization
andvehicleroutingproblems. Currently,thereislimitedresearchonemergencymaterial
distributionpathoptimizationforroadrepairunderextremedisasters. Moreover,when
consideringtheuncertaintycausedbydisasters,manystudiesassumethatitfollowsaprob-
abilitydistributionandusestochasticprogrammingmethods.However,actualdisastersare
morecomplex,makingitdifficulttoaccuratelycharacterizethepreciseprobabilitydistribu-
tionofuncertainparameters. Basedontheaboveanalysis,thispaperstudiesasecondary
emergency material distribution network, considering limited repair resources and all
transportationpaths,andexplorestheemergencylogisticsdistributionpathoptimization
problemunderthedamagedstateoftheroadnetworkduetonaturaldisasters. Thispaper
constructsadistributionpathoptimizationmodelwiththecomprehensivesatisfactionof
thematerialdistributionprocessastheobjective,andbasedontheactualdisastersituation
atdemandpoints,itachievesareasonabledistributionofemergencymaterialstomaximize
satisfaction. A variable neighborhood search (VNS) algorithm is designed to solve the
model,providingnewinsightsforemergencylogisticspathoptimizationresearch.

Sustainability2025,17,10591 7of28
3. ModelConstruction
3.1. ProblemDescription
Duringextremedisasters,theemergencymaterialdistributioninaffectedareasfaces
significantchallengesduetoahighuncertaintyinmaterialdemand,transportationtimes,
anddistributionrouteselection,whichsubstantiallyimpactstheefficiencyandtimeliness
of rescue operations, particularly as road conditions become a key influencing factor
with three main post-disaster scenarios. To systematically address these uncertainties,
the proposed model is designed primarily for pre-disaster strategic planning, while its
structureallowsforrapidpost-disasteroperationaladjustmentstailoredtodifferentroad
condition scenarios. After a disaster, the road conditions are usually classified into the
followingthreemainsituations:
(1) Severe road damage: Disasters may cause bridges to break, roadbeds to collapse,
or other situations, rendering some or all roads impassable. In this case, vehicles
cannotfollowtheoriginalroutes,andrescueeffortsmaystall,requiringeitherrepairs
or alternative paths. The repair time and the feasibility of alternative paths add
unpredictability,furtherprolongingthedistributiontimeofmaterials.
(2) Surgeintrafficvolume: Afteradisaster,affectedpopulationsneedtoevacuatequickly,
andrescueteamsneedtoenterurgently,allofwhichmayleadtoadramaticincrease
in traffic volume. In particular, in urban or densely populated areas, traffic may
become severely congested, causing a significant reduction in vehicle speeds and
potentiallyleadingtogridlock.Thissituationdirectlyimpactstheefficiencyofmaterial
transportationanddelaystheinitiationofrescueoperations.
(3) Goodroadconditions: Insomecases,theroadsmaynotbeseverelydamagedafterthe
disaster,andtrafficvolumemayremainrelativelylow. Inthiscase,vehiclescanfollow
theplannedroutesquickly,andthetransportationofmaterialsfacesnoobstacles. This
scenariorepresentsanidealcondition,ensuringthatrescuematerialscanbedelivered
todisastersitesinatimelyandeffectivemanner.
Therefore,inthefaceofdifferentroadconditions,thetransportroutes,scheduling,and
resourcedeploymentofemergencysuppliesneedtobeflexiblyadjustedaccordingtothe
specificconditionsofthedisastertoensurethattherescueefficiencyismaximized. Inthis
context,theestablishmentofaflexible,efficient,andreal-timeresponsetotheemergency
supply transport program is particularly important. In this case, vehicle b is required
totransportemergencymaterialspfromsupplypointkandemergencywarehousesto
disasterpointdthroughthematerialdistributionnetwork. Figure1showstheschematic
diagramofthedistributionofemergencysupplies. Someoftheroadsbetweenthesupply
point,theemergencywarehouse,andthedisastersiteneedtoberepairedduetodamage,
whichmakesthetransporttimeofvehiclebuncertain. Theseuncertaintyparametersare
characterizedbyaseriesofvaluesthatreflectthelikelihoodoftheparametersindifferent
scenarios. Scenario-based parameter and decision variables that may lead to scenarios
instochasticplanningmodelsareintroduced. Scenarioprobabilitiesareusedtodescribe
theuncertaintyofdemand,andtheuncertaintyoftransporttimeisportrayedusingthe
opportunityconstrainedplanningmethod. Theuncertaintyofdemandandtransporttime
ofemergencysuppliesdirectlyaffectsthesatisfactionofemergencysuppliesdistributionat
thedisastersiteduetothedisastersituation.
Insummary,thecoreproblemofdecision-makingishowtoproperlyarrangetherepair
ofdamagedroads,plantheservicepathsofemergencyvehiclesincombinationwiththe
roadnetworkconnectivityinformation,andensurethedistributionofemergencymaterials
to the affected points within the specified time, so as to maximize the comprehensive
satisfaction of the whole distribution system while meeting the constraints of supply

Sustainability2025,17,10591 8of28
capacityofthesupplypoints,thecapacityoftheemergencywarehouses,andthenumber
oftransportvehicles.
Supply Point 1
Disaster site 1
Emergency Warehouse 1
Emergency Warehouse 2
Disaster site 3
Supply Point 2
Disaster site 2
Emergency Warehouse 3
Supply Points Emergency warehouse distribution routes
Disaster sites Impaired distribution routes
Emergency Warehouses Supply point distribution routes
Figure1.Mapofroadconditionsandlogisticsnetwork.
3.2. ProblemAssumption
Assumption(1): Theamountofmaterialstoredateachsupplypointisknown.
Assumption(2): Thequantityofsuppliesrequiredateachdisastersiteisknown.
Assumption(3): Thecoordinatesofthelocationsofthesupplypointsandthedisaster
siteareknown.
Assumption (4): The capacity of all emergency warehouses is measured using a
unifiedstandardspatialunit. Additionally,eachsupplytypepossessesapredefinedspatial
conversionfactor. Thisfactorconvertsthequantityofaunitsupplyintothenumberof
standardspatialunitsitoccupies.Consequently,thetotalcapacityconstraintofawarehouse
referstotheaggregatespatialoccupancyofallstoredsupplies,convertedviathesefactors,
whichmustnotexceedthewarehouse’sratedcapacity.
3.3. ModelConstruction
3.3.1. Sets
K Thesetofallsupplypoints,k ∈ K.
k Theindexofthesupplypoint.
S Thesetofallcandidatecontingencywarehouses,s ∈ S.

Sustainability2025,17,10591 9of28
s Theindexofcandidatecontingencywarehouses.
D Thesetofallaffectedpoints,d ∈ D.
d Theindexofaffectedpoints.
Ω Thesetofallscenarios,ω ∈ Ω.
ω Theindexofscenarios.
P Thesetofallmaterialtypes, p ∈ P.
p Theindexofthetypeofmaterial.
Q Thesetofallemergencywarehousesizes,q ∈ Q.
q Theindexofthesizeoftheemergencywarehouse.
N Thesetofallnodes,i,j ∈ N,whereN = K∪S∪D.
Theindexofnodesintheemergencymaterialdistributionnetwork,includingall
i,j
supplypoints,emergencywarehouses,anddisasterpoints.
3.3.2. Parameters
ξ(ω) Denotestheprobabilityofscenarioωoccurring.
M Denotesasufficientlylargepositivenumber.
C Indicatesthetotalbudget.
r Indicatesthenumberofroadrehabilitationteams.
oc Denotesthecostofrehabilitatingtheroadperunitofrehabilitationteamr.
r
oc Denotesthecostofbuildingscaleqatnodes.
s,q
oc Denotesthecostoftransportingfromnodeitonodej.
i,j
zω Quantityofmaterial pthatsupplypointkcansupplyunderscenarioω.
k,p
Scenarioω,theamountofmaterial pthatisinitiallystoredinemergency
yω
s,p warehouses.
gω Scenarioω,thedemandforemergencysupplies patdisasterpointd.
d,p
Scenarioω,iftheroadfromnodeitonodejisnotdamaged,itis1;otherwiseit
ηω
i,j is0.
a Indicatesthemaximumdemandfactorattheaffectedsite.
1
a Denotestheminimumdemandcoefficientoftheaffectedpoint.
2
λ Denotestheimpactcoefficientofthedisasteronthedistributionroute.
rtω Scenarioω,thetimetorepairtheroadfromnodeitonodej.
i,j
lt Denotesthelatesttimeformaterialdistributionfrompointitopointj.
i,j
et Denotestheearliesttimeformaterialdistributiontoreachpointjfrompointi.
i,j
xt Denotesthedistributiontimefromnodeitopointjwhentheroadisintact.
i,j
3.3.3. DecisionVariables
Binaryvariable,1ifanemergencywarehouseofsizeqisestablishedatcandidate
α
i,q
pointi,0otherwise.
Binaryvariable,scenarioω,theroadfromnodeitonodejneedstoberepairedis
δω
i,j 1,0otherwise.
βω Binaryvariable,scenarioω,1ifnodejisreachedfromnodei,0otherwise.
i,j
Floatingvariable,scenarioω,theamountofmaterial pdeliveredfromsupply
ζω
k,d,p pointktodisasterpointd.
Floatvariable,scenarioω,withthenumberofdeliveriesofmaterial pfrom
ζω
k,s,p supplypointktoemergencydepots.
Floatvariable,scenarioω,withthenumberofdeliveriesofmaterial pfrom
ζω
s,d,p emergencydepotstodisasterpointd.

Sustainability2025,17,10591
10of28
3.3.4. ComprehensiveSatisfaction
Thethreedecisionscenariosdescribedinthissectionallemploythevariable,where
therangeofindicesiandjfollowsthedefinitioninSection3.3.1.
1. Timesatisfaction
The soft time window is used to construct the fuzzy affiliation function, where
tω = λ×xt + δω ×rtω; becauseofthedifferenttypesofdamagetotheroad,aroad
| i,j | i,j | i,j | i,j |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
impactcoefficientλ(λ ≥1)isintroduced. Therefore,thetimelinessofemergencymaterial
(cid:16) (cid:17)
distributionisportrayedasthetimesatisfactionfunction,andthetimesatisfaction f tω
i,j
ofmaterialdistributionattheaffectedpointisasfollows:

|     |     |     |          |          | 1 ,         | 0 < t ω | ⩽ e t     |     |     |
| --- | --- | --- | -------- | -------- | ----------- | ------- | --------- | --- | --- |
|     |     |     |          |      |             | i ,j    | i, j      |     |     |
|     |     |     | (cid:16) | (cid:17) | l ti,j −t ω |         |           |     |     |
|     |     |     | f        | tω =     | i ,j ,      | et <    | t ω ⩽ l t |     | (1) |
|     |     |     |          | i,j      | lt −eti,j   | i,d     | i,j i,j   |     |     |
0 i,j
|     |     |     |     |     | ,   | lt < tω |     |     |     |
| --- | --- | --- | --- | --- | --- | ------- | --- | --- | --- |
|     |     |     |     |     |     | i,j     | i,j |     |     |
Theoveralltimesatisfactionfunction f fortheemergencymaterialdistributionsystem
1
ateachdisastersiteisasfollows:
|     |     |     |     |     | 1   | (cid:16) (cid:17) |     |     |     |
| --- | --- | --- | --- | --- | --- | ----------------- | --- | --- | --- |
|     |     |     |     |     | =   | tω                |     |     |     |
|     |     |     |     |     | f 1 | f                 |     |     | (2) |
n i,j
Demandsatisfaction
2.
Thedegreeofsatisfactionwiththedemandforemergencysuppliesattheaffected
sitesisasfollows:
|     |     |     |     | (cid:16) (cid:17) |     |           |       |     |     |
| --- | --- | --- | --- | ----------------- | --- | --------- | ----- | --- | --- |
|     |     |     |     | ζω                | ∑ ∑ | βω(gω −ζω |       |     |     |
|     |     |     |     | f                 | =   |           | )     |     | (3) |
|     |     |     |     | i,j,p             |     | i,j j,p   | i,j,p |     |     |
i∈Np∈P
Thesatisfactionfunction f 2 fortheoveralldemandfortheemergencydistribution
systemateachdisastersiteisasfollows.
|     |     |     |     |     | 1     | (cid:16) (cid:17) |     |     |     |
| --- | --- | --- | --- | --- | ----- | ----------------- | --- | --- | --- |
|     |     |     |     |     | f = f | ζω                |     |     | (4) |
|     |     |     |     |     | 2     | i,j,p             |     |     |     |
n
3. Comprehensivesatisfaction
Thefunctionsetstheweightofthetimesatisfactionoftheaffectedpointθ andthe
weightofdemandsatisfaction1−θ,followedbythecomprehensivesatisfactionfunctionof
theaffectedpointonthedistributionofrescuematerialsoftheemergencylogisticssystem:
|     |     |     |     |     | = +  | (1−θ)f |     |     |     |
| --- | --- | --- | --- | --- | ---- | ------ | --- | --- | --- |
|     |     |     |     | f 3 | θf 1 |        | 2   |     | (5) |
3.3.5. ObjectiveFunction
1
|     |     |     |     | Max | f = | ∑ ξ(ω)f |     |     | (6) |
| --- | --- | --- | --- | --- | --- | ------- | --- | --- | --- |
|     |     |     |     |     | Ω   |         | 3   |     |     |
ω∈Ω
s.t.
|     |     |     |     | ∑     | α ≤1 | ∀i        | ∈ S    |     | (7) |
| --- | --- | --- | --- | ----- | ---- | --------- | ------ | --- | --- |
|     |     |     |     | q∈Q   | i,q  |           |        |     |     |
|     |     | ∑   | ζω  | ≤ Mβω |      | ∀d ∈ D,∀s | ∈ S,∀ω | ∈ Ω |     |
(8)
|     |     |     | p∈P | s,d,p | s,d |     |     |     |     |
| --- | --- | --- | --- | ----- | --- | --- | --- | --- | --- |
∑
|     |     |     | ζω        | ≤ Mβω |       | ∀k ∈ K,∀d | ∈ D,∀ω | ∈ Ω | (9)  |
| --- | --- | --- | --------- | ----- | ----- | --------- | ------ | --- | ---- |
|     |     |     | p∈P k,d,p |       | k,d   |           |        |     |      |
|     |     | ∑   | ζω        | Mβω   |       |           |        | Ω   |      |
|     |     |     |           | ≤     |       | ∀k ∈ K,∀s | ∈ S,∀ω | ∈   | (10) |
|     |     |     | p∈P       | k,s,p | k,s   |           |        |     |      |
|     |     | ∑   |           | ζω ≤  | zω    | ∀k ∈ K,∀p | ∈ P,∀ω | ∈ Ω | (11) |
|     |     |     | i∈S∪D     | k,i,p | k,p   |           |        |     |      |
|     |     |     |           | ∑ ∑   | δω ≤r | ∀ω∈       | Ω      |     |      |
(12)
|     |     |     |     | i∈N | j∈N i,j |     |     |     |     |
| --- | --- | --- | --- | --- | ------- | --- | --- | --- | --- |

Sustainability2025,17,10591
11of28
| ∑   | ∑ ζω | ∑     | yω  | ∑     | ∑     | ζω        |        |          | Ω      |      |
| --- | ---- | ----- | --- | ----- | ----- | --------- | ------ | -------- | ------ | ---- |
|     |      | ≤     |     | +     |       |           |        | ∀s ∈     | S,∀ω ∈ | (13) |
| p∈P | d∈D  | s,d,p | p∈P | s,p   | p∈P   | k∈K k,s,p |        |          |        |      |
|     | a gω | ≤ ∑   | ζω  | ≤ a   | gω    | ∀d        | ∈ D,∀p | ∈ P,∀ω ∈ | Ω      |      |
|     | 1    | d,p   |     | i,d,p | 2 d,p |           |        |          |        | (14) |
i∈K∪S
|     |     |     | ∑        | βω               |      |           |     | Ω   |     |      |
| --- | --- | --- | -------- | ---------------- | ---- | --------- | --- | --- | --- | ---- |
|     |     |     |          | ≥1               |      | ∀d ∈ D,∀ω |     | ∈   |     | (15) |
|     |     |     | i∈K∪S    | i,d              |      |           |     |     |     |      |
|     |     |     | δω ≤1−ηω |                  | ∀i,j | ∈ N,∀ω    | ∈   | Ω   |     | (16) |
|     |     |     | i,j      | i,j              |      |           |     |     |     |      |
|     |     |     | (cid:16) | (cid:17)(cid:16) |      | (cid:17)  |     |     |     |      |
Ω
|     |         | βω ≤1− | 1−ηω  |         | 1−δω   |     | ∀i,j ∈ | N,∀ω ∈   |      | (17)   |
| --- | ------- | ------ | ----- | ------- | ------ | --- | ------ | -------- | ---- | ------ |
|     |         | i,j    |       | i,j     | i,j    |     |        |          |      |        |
|     | ∑       | ζω     | −M ∑  |         | ≤0     | ∀s  | ∈ S,∀p | ∈ P,∀ω ∈ | Ω    |        |
|     |         |        |       | α i,q   |        |     |        |          |      | (18)   |
|     | k∈K     | k,s,p  |       | q∈Q     |        |     |        |          |      |        |
| ∑ ∑ |         | ∑      | ∑     |         | ∑      | ∑   |        |          |      |        |
|     | oc      | βω +   |       | δωoc    | +      |     | oc     | α ≤C     | ∀ω ∈ | Ω (19) |
| i∈N | j∈N i,j | i,j    | i∈N   | j∈N i,j | r      | q∈Q | s∈S    | s,q s,q  |      |        |
|     |         |        | ζω ≥0 |         | ∀i,j ∈ | ∈   | P,∀ω   | ∈ Ω      |      |        |
|     |         |        |       |         |        | N,p |        |          |      | (20)   |
i,j,p
rtω
|     |     |     |     | ≥0  |     | ∀i,j ∈ | N   |     |     | (21) |
| --- | --- | --- | --- | --- | --- | ------ | --- | --- | --- | ---- |
i,j
|     |     |     | εω  |     |      |       |       | Ω   |     |      |
| --- | --- | --- | --- | --- | ---- | ----- | ----- | --- | --- | ---- |
|     |     |     | ≥0  |     | ∀j ∈ | N,p ∈ | P,ω ∈ |     |     | (22) |
b,i,p
|     |     | βω,δω,ηω,α |         | ∈   | {0,1} | ∀i,j | ∈ N,ω | ∈ Ω |     | (23) |
| --- | --- | ---------- | ------- | --- | ----- | ---- | ----- | --- | --- | ---- |
|     |     | i,j        | i,j i,j | i,q |       |      |       |     |     |      |
The objective function (6) denotes the maximization of the overall satisfaction.
Constraint(7) denotes that, at most, one size of emergency depot can be established at
anyemergencydepotcandidate. Constraints(8)–(10)denotethatthetransportofsupplies
occursonlyatnodeswheretheroutesareconnected. Constraint(11)denotesthesupply
capacityconstraintofthematerialsupplyprovider. Constraint(12)denotestheroadteam
repairquantityconstraint. Constraint(13)denotestheconstraintonthedistributionof
materialsfromtheemergencywarehouse. Constraint(14)indicatesthatthetotalamount
ofeachtypeofemergencysupplytransportedtothedisastersitecanmeettheminimum
demandindifferentscenarioswhilenotexceedingthemaximumdemand. Constraint(15)
indicatesthateachaffectedpointisservedbyatleastonevehicle. Constraint(16)indicates
that the repair team only repairs the damaged roads. Constraint (17) indicates that the
repaired road is restored to traffic. Constraint (18), on the other hand, ensures that no
supplypointwillsendemergencysuppliestoanemergencywarehousecandidatepointif
nowarehouseisestablishedatthatpoint. Constraint(19)indicatesthetotalbudgetlimit.
Constraints(20)–(23)denotetherangeofvaluesforthedecisionvariables.
4. AlgorithmDesign
Variable neighborhood search (VNS) algorithms have been widely used to solve
combinatorialoptimizationproblems[33]andvehiclepathproblems[34]. Inthispaper,
wefocusonthejointpathproblemofroadrehabilitationandemergencywarehousesiting.
Astheproblemsizecontinuestogrow,thetimerequiredforcomputationwillincrease
exponentially. Tocopewiththischallenge,thispaperadoptstwodifferentinitialsolution
generationstrategies(VNS-RandomStartandVNS-GreedyStart)andcombinestheVNS
algorithm with the CPLEX solver to propose a new solution model. This study aims
toconductanin-depthanalysisofthedifferencesbetweenCPLEXandVNSalgorithms
withdifferentinitialsolutiongenerationstrategies,aswellastheeffectsofdifferentinitial
solutiongenerationstrategies(VNS-RandomStartandVNS-GreedyStart)onthesolution
efficiencyoftheVNSalgorithm.
4.1. Solution
andβω,ζω
| Basedontheanalysis,itcanbeseenthatthevariablesα |     |     |     |     |     |     |     |         | arethemain |     |
| ----------------------------------------------- | --- | --- | --- | --- | --- | --- | --- | ------- | ---------- | --- |
|                                                 |     |     |     |     |     |     |     | i,q i,j | i,j,p      |     |
decisionvariablesinthemodelproposedinthisstudy,andtherestofthedecisionvariables
depend on these three decision variables. Therefore, this study uses VNS to perform a

Sustainability2025,17,10591
12of28
neighborhoodsearchforthesethreedecisionvariables,andeachtimeanewneighborhood
isgenerated,thecommercialsolverCPLEXisinvokedtosolvethemodelanddetermine
whetherthevalueoftheobjectivefunctionhasimproved. Ifabettersolutionisfound,itis
necessarytojumpoutofthecurrentneighborhoodtogobacktothefirstneighborhood
andstartthesearchagain. Whenabettersolutioncannotbefoundwithinoneiteration,a
neighborhoodperturbationisperformedonthecurrentincumbentsolution,afterwhichit
proceedstothenextiterationtocontinuesearchinguntilnoshakingispossible.
According to the basic framework, the key issues in solving the model include
(i)initialization: how to give a good and feasible solution, including alternatives, and
the size of the contingency store; (ii) neighborhood structure: how to set up a suitable
neighborhoodstructure,whichcanfindtheincumbentsolutioninaveryshortperiodof
time;and(iii)neighborhoodshakingprocess: howtoavoidfallingintolocaloptimality.
4.2. InitialSolutionGeneration
Abetterinitialsolutionmaybelocatedinabetterregionofthesolutionspace,which
helpstheVNSalgorithmtofindahigh-qualitysolutionfaster. Conversely,apoorerinitial
solutionmaycausethealgorithmtospendmoretimeinapoorerregionofthesolution
spaceearlyinthesearch. Startingfromabetterinitialsolution,theVNSalgorithmmay
convergetoabettersolutionfasterbecauseitmaybeclosertotheglobalincumbentsolution.
Forthisreason,twosolutionmethodswithdifferentinitialsolutions(VNS-RandomStart
andVNS-GreedyStart)areproposedinthisstudy.
4.2.1. VNS-RandomStart
Therandomlygeneratedinitialsolutionalgorithm(hereinafterreferredtoasVNS-R)
firstcalculatesthetotaldemandforalltypesofmaterialsatallaffectedsites,andbased
on the total demand quantity among all warehouse sizes that can satisfy the demand,
itselectsthelargestoneasthesizeofthewarehouse, whoselocationisknown. Inthis
βω,becauseofthecomplexityoftheroute
| way,thevalueofα | i,q canbedetermined; | for |     |     |     |
| --------------- | -------------------- | --- | --- | --- | --- |
i,j
deploymentproblem,thesuppliesarerandomlydistributedfromthefirstsupplypoint(K)
oremergencywarehouse(S)toanydisaster-strickenpoint(D)untilthestoragecapacityof
thesuppliesatthesupplypoint(K)oremergencywarehouse(S)isdistributed. Thus,aset
ofinitialsolutionsforβω
isobtained;thepseudo-codeisshowninAlgorithm1.
i,j
| Algorithm1: | RandomStrategyforGeneratingInitialSolution |                          |     |     |     |
| ----------- | ------------------------------------------ | ------------------------ | --- | --- | --- |
|             | S;gω                                       | zω                       |     |     |     |
| 1: Input:D; | K;                                         | ;{1,2,...,Q};{1,2,...,P} |     |     |     |
|             | d,p                                        | i,p                      |     |     |     |
| 2: Output:α | ;βω                                        |                          |     |     |     |
i,q i,j
3: Procedure:
=0;βω
| 4: Initializeallα | i,q | =0  |     |     |     |
| ----------------- | --- | --- | --- | --- | --- |
i,j
5: ForeachcommodityP:
|                          |     | TotalDemand=∑ |     | gω  |     |
| ------------------------ | --- | ------------- | --- | --- | --- |
| 6: Calculatetotaldemand: |     |               | d∈D |     |     |
d,p
ForeachwarehousesizeoptionQ:IfQ≥TotalDemand,markQasfeasible
7:
SelectthelargestfeasibleQ,setα =1
| 8:  |     |     | i,q |     |     |
| --- | --- | --- | --- | --- | --- |
9: ForeachcommodityP:
| 10: Combinesources: | Sources | = K∪S. |     |     |     |
| ------------------- | ------- | ------ | --- | --- | --- |
11: WhilethereexistsunmetdemandinDandavailablesupplyinSources:
∈ Sourceswithyω
| 12: RandomlyselectaSourcei |     |     |     | s,p >0 |     |
| -------------------------- | --- | --- | --- | ------ | --- |
Randomlyselectadisasterpointj ∈ Dwithgω
| 13:                               |         |     |          | >0              |          |
| --------------------------------- | ------- | --- | -------- | --------------- | -------- |
|                                   |         |     | (cid:16) | d,p             | (cid:17) |
| 14: Computetransportamount:amount |         |     | = Min    | yω , zω , gω −∑ | βω       |
|                                   |         |     |          | s,p k,p d,p     | k∈K k,j  |
| 15: Assignβω                      | =amount |     |          |                 |          |
i,j

Sustainability2025,17,10591
13of28
| Algorithm1: Cont.              |     |             |     |
| ------------------------------ | --- | ----------- | --- |
| 16: Updatecapacity:            | zω  | ←zω −amount |     |
|                                |     | i,p i,p     |     |
| 17: Updatedemand:              | gω  | ←gω −amount |     |
|                                |     | d,p d,p     |     |
| 18: Ifzω =0,removeifromSources |     |             |     |
i,p
;βω
| 19: Returnα | i,q |     |     |
| ----------- | --- | --- | --- |
i,j
4.2.2. VNS-GreedyStart
Theinitialsolutionalgorithmgeneratedbythegreedystrategy(hereinafterreferred
toasVNS-G)isamethodofconstructingaglobalincumbentsolutionbyselectingalocal
incumbentsolution. First,thetotaldemandgω ofalltheaffectedpointsforvarioustypes
d,p
ofsuppliesiscalculated,andaccordingtothenumberofthetotaldemandamongallthe
warehouse sizes that can satisfy the demand, the one with the largest scale is selected
as the warehouse size, and the warehouse’s location is known. This enables a set of
initialsolutionsforα tobeobtained;forβω,theclosestsupplypoint(K)oremergency
|     | i,q | i,j |     |
| --- | --- | --- | --- |
warehouse(S)isselectedbasedonthelocationoftheaffectedpointtoprovidethesupplies
untilthereisnostoragecapacityforthesuppliesatthissupplypoint(K)oremergency
warehouse(S).Then,thesecondclosestsupplypoint(K)oremergencywarehouse(S)is
Thus,aseriesofinitialsolutionsofβω
changedtodistributethesupplies. aregenerated.
i,j
Thepseudo-codeisshowninAlgorithm2.
| Algorithm2: FunctiongreedyAlgorithm(Problem,Strategy) |         |                                              |     |
| ----------------------------------------------------- | ------- | -------------------------------------------- | --- |
| 1: Input:D;                                           | K; S;gω | ;zω ;{1,2,...,Q};P;Distance(i,j);{1,2,...,P} |     |
|                                                       | d,p     | i,p                                          |     |
| 2: Output:α                                           | ; βω    |                                              |     |
i,q i,j
3: Procedure:
=0;βω
| 4: Initializeallα |     | =0  |     |
| ----------------- | --- | --- | --- |
|                   | i,q | i,j |     |
5: ForeachcommodityP:
|                          |     | TotalDemand=∑ | gω    |
| ------------------------ | --- | ------------- | ----- |
| 6: Calculatetotaldemand: |     |               | d∈D . |
d,p
7: ForeachwarehousesizeoptionQ:IfQ≥TotalDemand,markQasfeasible
=1
| 8: SelectthelargestfeasibleQ,setα |     | i,q |     |
| --------------------------------- | --- | --- | --- |
9: ForeachcommodityP:
| 10: Combinesources: |     | Sources = K∪S |     |
| ------------------- | --- | ------------- | --- |
Foreachdisasterpointj ∈ D: SortSourcesbyDistance(i,j)inascendingorder
| Whilegω | >0and∃i | ∈Sourceswithzω | >0  |
| ------- | ------- | -------------- | --- |
11:
|     | d,p |     | i,p |
| --- | --- | --- | --- |
12: Selecttheclosestsourceifromthesortedlist
13: Computetransportamount:
|              | (cid:16) |          | (cid:17) |
| ------------ | -------- | -------- | -------- |
|              | zω       | gω −∑ βω |          |
| 14: amount=  | Min      | , k∈K    |          |
|              | i,p      | d,p k,j  |          |
| 15: Assignβω | =amount  |          |          |
i,j
| 16: Updatecapacity:            | zω  | ←zω −amount |     |
| ------------------------------ | --- | ----------- | --- |
|                                |     | i,p i,p     |     |
| 17: Updatedemand:              | gω  | ←gω −amount |     |
|                                |     | d,p d,p     |     |
| 18: Ifzω =0,removeifromSources |     |             |     |
i,p
| 19: Returnα | ;βω |     |     |
| ----------- | --- | --- | --- |
i,q i,j
4.3. NeighborhoodStructure
Sincethemodelinthisstudyisamixed-integerprogrammingmodel,thedecision
variablessearchedintheVNScontainbinaryvariablesandfloatvariables,andasuitable
neighborhoodstructureisdesignedaccordingtothedecisionvariablesinvolvedinthe
algorithm. Thisstudycanencodetheneighborhoodselectionofα i,q ,whichisthedecision

Sustainability2025,17,10591 14of28
variableforthelocationoftheemergencystockpile, accordingtothedimensionalityof
the decision variable after expanding it, with 1 representing the establishment of the
warehouseand0representingthenon-establishmentofthewarehouse. Neighborhoods
canbegeneratedbymutation,exchange,andinsertion,butafterperformingtheabove
operations,itisnecessarytodeterminewhetherthesiteselectionofthewarehousemeets
therestrictionsofconstraint(3).Forthedecisionvariableβω,1meansthatunderscenarioω,
i,j
thepointfromnodeireachesnodej,and0meansthattheaffectedpointisservedbyother
nodes,andthedecisionvariableβω,needstosatisfytherequirementsofconstraint(2).
i,j
4.3.1. DomainStructure1: Mutation
Randomlyselectα ,ifitsoriginalvalueis0andthenchangeitto1; ifitis1,then
i,q
changeitto0. Subsequently,thefeasibilityofthesolutionmustbeverified. Specifically,if
acandidatepointisselectedtohostanewwarehouseofacertainsize,butoursolution
has already assigned a different-sized warehouse to that same point, an adjustment is
required. Toenforcetheconstraintthateachcandidatepointcanaccommodateatmost
onewarehouse,thecodesforallotherwarehousesizesatthispointmustbesetto0,while
thecodeforthenewlyselectedwarehousesizeissetto1. Thisadjustmentprocess,which
ensuresthefeasibilityoftheneighborhoodsolutiongeneratedbythemutationoperator,is
illustratedinFigure2.
Figure2.Domainstructure1:schematicdiagramofα mutation.
i,q
4.3.2. DomainStructure2: Exchange
TheprocessofexchangeisshowninFigure3;first,twovaluesofα arerandomlyse-
i,q
lectedfromtheinitialsolutionarrayofα =1,whichcanonlybethevaluescorresponding
i,q
todifferentsupplypointsoremergencywarehousesdistributingemergencysuppliesto
theaffectedpoints. Swapthevaluescorrespondingtothetwopoints. Again,itisnecessary
tojudgewhetheritisfeasibleornotafterdoingtheswap. Thesamestrategy,asshownin
Figure4,exchangesthedistributionoftwosupplypointsortheaffectedpointsservedby
twosupplypoints.
Figure3.Domainstructure2:schematicofα exchange.
i,q

Sustainability2025,17,10591 15of28
Swap Swap
Initial solution
Supply Points
Supply Points
Supply Points
Supply Points
Supply Points
Supply Points
Figure4.Domainstructure2:schematicofβω exchange.
i,j
4.3.3. DomainStructure3: Insertion
TheprocessofinsertionisshowninFigure5;fortwodifferentsupplypointsk,one
ofthem,βω =1,isbroughttotheothersupplypoint. Afterdoingtheinsertion,itisagain
i,j
necessarytojudgewhetheritisfeasibleornot.
Supply Points
Supply Points
Insert
Supply Points
Supply Points
Figure5.Domainstructure3:schematicofβω insertion.
i,j
4.3.4. DomainStructure4: AdditionandSubtraction
Forthecontinuousdecisionvariableζω ,thisstudyemploysfixed-stepneighborhood
s,d,p
search. Specifically,wepresetareasonablestepsize∆ζ. Theneighborhoodofthisvariable
isdefinedas{ζ−∆ζ,ζ + ∆ζ }. Toavoidexcessivecomputationalresourceconsumption
duringlocalsearchonasinglevariable,welimitthenumberofconsecutivesearchesin
eitherdirection(increaseordecrease)toamaximumofKsteps(K=20inthisstudy). This
approachapproximatesthecontinuousproblemasacombinatorialonethroughdiscretized
search. While it introduces minor precision errors due to step size and search depth
constraints,theseerrorsremainwithinmanageablelimitsandareoffsetbyasignificant
improvementincomputationalefficiency.
4.4. BasicVariableNeighborhoodDescent
Variable neighborhood descent is the framework of the algorithm, which searches
in the neighborhood structure. The algorithm will completely explore a neighborhood
structureandthenmovetothenextneighborhoodstructureifabettersolutioncannotbe
found;theflowofVNSisshowninAlgorithm3.

Sustainability2025,17,10591 16of28
Algorithm3: VariableNeighborhoodDescent(VND)
incumbent_sol,candidate_sol,k←1//incumbent_solisthecurrentbestsolution,candidate_solisfor
Input:
neighborhoodexploration,kistheindexoftheneighborhoodstructure
1: candidate_sol←incumbent_sol
2: While(true)do
3: switch(k)
4: case1:
apply_NH_1(candidate_sol)//Applythefirstneighborhoodoperator
5: ifcandidate_sol.fitness>incumbent_sol.fitnessthen
6: incumbent_sol←candidate_sol
7: k←0
8: endif
9: break
10: case2:
11: apply_NH_2(candidate_sol)//Applythesecondneighborhoodoperator
12: ifcandidate_sol.fitness>incumbent_sol.fitnessthen
13: incumbent_sol←candidate_sol
14: k←0
15: endif
16: break
17: case3:
18: apply_NH_3(candidate_sol)//Applythethirdneighborhoodoperator
19: ifcandidate_sol.fitness>incumbent_sol.fitnessthen
20: incumbent_sol←candidate_sol
21: k←0
22: endif
23: break
24: case4:
25: apply_NH_4(candidate_sol)//Applythefourthneighborhoodoperator
26: ifcandidate_sol.fitness>incumbent_sol.fitnessthen
27: incumbent_sol←candidate_sol
28: k←0
29: endif
30: break
31: default:
32: return
33: endswitch
34: k←k+1
35: endwhile
36: candidate_sol←incumbent_sol
4.5. NeighborhoodPerturbationProcess
Invariableneighborhoodsearchalgorithms, aneighborhoodperturbationprocess
mustbeexecutedaftereachiterationtopreventgettingstuckinlocaloptima. Thisstudy
employsastructuredblockperturbationstrategy: first,thecurrentincumbentsolutionis
dividedintomultipledecisionblocksbasedoncandidatewarehouselocations,witheach
blockcontainingallconfigurationvariablesforaspecificlocation;Basedoneachblock’s
contributiontotheobjectivefunction,aquality-orientedprobabilisticselectionmechanism
determinestheblocktobeperturbed,prioritizingblockswithalowercontribution. Sub-
sequently,theselectedblockisreassignedtoanunusedcandidatelocationinthecurrent

Sustainability2025,17,10591 17of28
solution. Thenewlocationisdeterminedfollowingadiversity-firstprinciple,prioritizing
candidatepointsfartherfromtheoriginallocation.Sincetheinternalstructureofeachblock
(particularlywarehousesizeattributes)remainsunchangedduringperturbation,thenew
solutioninherentlysatisfiesallwarehouseconfigurationconstraints. Thisensuressolution
feasibility while enabling effective search space transfer. By systematically altering the
spatiallayoutstructureofthesolution,thealgorithmescapesthecurrentattractorregion.
ThespecificoperationalflowisillustratedinFigure6.
Figure6.VNSneighborhoodperturbationprocessmap.
4.6. StepsofVariableNeighborhoodSearchAlgorithm
Thevariableneighborhoodsearch(VNS)algorithmbeginsbygeneratingafeasible
initialsolution. Thissolutionisthenrefinedusingalocalsearchcomponentcalledvariable
neighborhood descent (VND), which leverages predefined neighborhood structures to
findalocallyimprovedsolution. Toavoidbecomingtrappedinlocaloptima,ashaking
procedureisapplied.Thisstepstrategicallyperturbsthecurrentsolutionwithinthefeasible
region,providinganewstartingpointforsubsequentiterations. Thealgorithmterminates
wheneitherthemaximumnumberofiterationsisreachedorwhennoimprovementis
observedforaspecifiednumberofconsecutivecycles. Thecompleteframeworkisoutlined
inAlgorithm4.
Algorithm4: VariableNeighborhoodSearch(VNS)
max_iterations,global_best,current_sol,stagnation_count←0,max_iterations←10//
Input: max_iterationsisthemaximumstagnationcount,global_bestisthebestsolution,current_sol
istheworkingsolution
Output: Objectivevalue
1: global_best←GenerateInitialSolution()
2: While(stagnation_count<max_iterations)do
3: current_sol←global_best
4: shaking_phase(current_sol)//Applyshakingtoescapelocaloptimum
5: Variable_Neighborhood_Descent(current_sol)//CallAlgorithm3forlocalsearch
6: If(current_sol.fitness>global_best.fitness)then
7: global_best←current_sol
8: stagnation_count←0//Resetcounteronimprovement
9: Endif
10: stagnation_count←stagnation_count+1
11: Endwhile
12: Returnglobal_best.fitness

Sustainability2025,17,10591
18of28
5. NumericalExperiments
Inordertoverifytheeffectivenessoftheproposedmodelsandalgorithmsforpractical
applications,thisstudyimplementstwoalgorithms,VNS-RandVNS-G,usingtheC#pro-
gramminglanguageintheVisualStudio2022environment. Thehardwareconfigurations
used for the experiments include a computer with 16 GB of RAM, an AMD R7-4680H
processor,andaWindows10operatingsystem. Theemergencywarehousesitingproblem
inthisstudyisastochasticplanningmodelthatconsidersdifferentscenariosofdemandat
thedisastersite. Thescenariosaregeneratedbasedonhistoricaldisasterdata,thedemand
attheaffectedpointsobeysaPoissondistribution,andtheprobabilityofroaddamageis
settobeuniformlydistributedfrom20%to40%. Thenumberofscenarioshasasignificant
impactontheexperimentalresults: toofewscenarioscannotfullyreflecttherobustnessof
themodel,whiletoomanyscenarioswillleadtoadecreaseincomputationalefficiency.
InthecaseofoptimizingthemodelsizetoA5-10-25-3-3,themeaningoftheexampleID
A5-10-25-3-3is5supplypoints,10emergencywarehouses,25affectedpoints,3different
sizesofwarehouseswithdifferentcapacities,and3differenttypesofemergencysupplies.
Wedesignedexperimentstodeterminethenumberofscenariosforthesystem. Asshown
inTable2,wetestedsevengroupsofscenarioquantities(10,20,50,100,200,400,and800),
with10randomlygeneratedinstancesforeachgroupandallscenariosusingtheequal
probabilityassumption(1/|Ω|).
Table2.Testmodelrununderadifferentnumberofscenarios.
| Numberof  | Maximum | Minimum |                 | Standard  | AverageCPU |
| --------- | ------- | ------- | --------------- | --------- | ---------- |
|           |         |         | Difference Mean |           |            |
| Scenarios | Value   | Value   |                 | Deviation | Runtime(s) |
| 10        | 0.9877  | 0.9241  | 0.0636 0.9550   | 0.0209    | 17.12      |
| 20        | 0.9851  | 0.9341  | 0.0510 0.9549   | 0.0162    | 20.55      |
| 50        | 0.9963  | 0.9501  | 0.0462 0.9749   | 0.0156    | 34.88      |
| 100       | 0.9975  | 0.9557  | 0.0418 0.9730   | 0.0124    | 71.22      |
| 200       | 0.9887  | 0.9688  | 0.0199 0.9743   | 0.0055    | 178.99     |
| 400       | 0.9883  | 0.9689  | 0.0194 0.9752   | 0.0054    | 485.33     |
| 800       | 0.9888  | 0.9702  | 0.0186 0.9750   | 0.0050    | 1547.22    |
AsshowninTable2,thestandarddeviationoftheobjectivefunctiondecreaseswith
thenumberofscenariosandstabilizesafter |Ω|≥ 100(<0.0125);therunningtimein-
|Ω|≥
creasesapproximatelylinearlywiththenumberofscenarios,andwhen 200,the
magnitudeoftheobjectivefunctionimprovement(<0.1%)isnolongersignificant. Based
ontheconvergence-efficiencytrade-offanalysis,wechoose100scenariosasthecriterion
forsubsequentexperiments. Thisnumberensuresthestabilityoftheresults(standarddevi-
ation<1.25%)andkeepsthetimeofasingleexperimentwithinareasonablerange(about
71s). Atthesametime,100scenarioscanadequatelycoverthedemandfluctuationsunder
typicaldisastersituations. Therefore,weuse100scenariosinthesubsequentnumerical
experiments. Werandomlygeneratedasetofscenarios,eachreflectingaspecificdisaster
situation. AsshowninTable3,itcontainsdeterministicinformationsuchasthelocationof
thedisastersite,thesupplysite,thelocationoftheemergencywarehouse,andthedamage
totheroad.
Table3.Relevantparametersettings.
| Parameter | Value       | Parameter | Value       | Parameter | Value      |
| --------- | ----------- | --------- | ----------- | --------- | ---------- |
| zω        | [3000,7000] | gω        | [1000,3000] | oc        | [800,1500] |
| k,p       |             | d,p       |             | r         |            |
1/|Ω|
| ξ(ω) |     | xt  | [360,720] | oc s,q | [10,000,30,000] |
| ---- | --- | --- | --------- | ------ | --------------- |
i,j
| λ   | [1,3] | rtω | [60,120] | oc  | [20,80] |
| --- | ----- | --- | -------- | --- | ------- |
|     |       | i,j |          | i,j |         |
| a   | 0.8   | a   | 0.5      | r   | [30,50] |
| 1   |       | 2   |          |     |         |

Sustainability2025,17,10591 19of28
5.1. PerformanceComparisonofTwoDifferentInitialSolutionAlgorithms
Tables4and5showtheexperimentalresultsforthesmall-andmedium-sizedalgo-
rithms,respectively. Here,thevariableZrepresentsthevaluationoftheobjectivefunction,
while T refers to the computational time of the algorithm. The subscripts C, R, and G
correspondtothethreesolutionmethods,i.e.,CPLEX,VNS-R,andVNS-G,respectively.
TheGAPmetricinthetableisusedtoquantifythedeviationbetweenthesolutionobtained
by the algorithm and the exact solution of CPLEX, which is calculated as (f − f)/f .
C C
Here,thesubscriptsC,R,andGalsorefertotheCPLEX,VNS-R,andVNS-Galgorithms,
respectively. Accordingtothetestdata,neitheralgorithmterminatestheiterativeprocess
whenthepresetmaximumnumberofiterationsisreachedorwhennofurtherexploration
forabettersolutionispossible.
InTable4, thisstudyconductsanexhaustiveteston6outof18setsofsmall-scale
arithmetic cases and compares the performance of three different algorithms in terms
ofsolutionandcomputationtime. ThemeaningsofthealgorithmIDsA2-3-5-3-3-1are
as follows: two supply points, three emergency warehouses, five affected points, three
differentsizesofwarehouseswithdifferentcapacities,threedifferenttypesofemergency
supplies, and the index of the calculated cases. The difference between the four cases
in each group of scales lies mainly in the stochastic demand of supplies at the affected
points. The CPLEX method solves the model directly, whereas the other two methods,
VNS-R and VNS-G, search for the best solution. As shown in Table 4, both heuristic
algorithmsfoundthesamesolutionasCPLEX.Inall24cases,theaveragedifferencein
theincumbentsolutionsis0.0%,showingtheveryhighsolutionqualityoftheVNS-Rand
VNS-Galgorithms. Intermsofcomputationtime, CPLEXshowsgreatefficiencywhen
dealingwithsmall-scalecases,withasolutiontimeoflessthan10sforCPLEXwhenthe
casesizecontainsonly5scenarios,whilethesolutiontimeofVNS-RandVNS-Gismore
than10s. However,asthecasesizeincreases,theVNS-RandVNS-Galgorithmsbeginto
outperformCPLEX.Withthecaseconfigurationof4candidatewarehouses,10affected
regions,andmorethan10scenarios,bothVNS-RandVNS-Gcancompletethecomputation
inabout25s,withVNS-Ghavingaslightlybettersolvingspeedandbeingabletokeepthe
solvingtimeunder20s. Incontrast,thesolutiontimeofCPLEXgraduallydecreases.
Table5showstheexperimentalresultsformedium-sizedarithmeticcases,inwhich
12configurationsfromthreesetsofarithmeticcasesareselectedinthisstudyandcombined
withotherrelevantparameters.TheVNS-RandVNS-Galgorithmssignificantlyoutperform
CPLEXintermsofsolutiontimeformedium-sizedproblems. Formedium-sizedproblems,
CPLEXappearstobetime-consuminginfindingtheincumbentsolution. Inthefirstset
ofexamples,A5-5-20-3-3-1,A5-5-20-3-3-2,A5-5-20-3-3-3,andA5-5-20-3-3-4,thesolution
time of CPLEX is about three times that of VNS-R and five times that of VNS-G. This
timegapisfurtherwidenedinthefollowingtwosetsofexamplesduetotheexponential
increaseinthesolutiontimeofCPLEX.Intermsofsolutionquality,theVNS-RandVNS-G
algorithmsareabletofindthebestsolutionmatchingCPLEXinmostcases. Onlyinafew
caseswastheincumbentsolutionnotreached,buttheaveragedifferencewasstilllessthan
2percent. ThisfindingconfirmsthattheVNS-RandVNS-Galgorithmsdevelopedinthis
studycanimprovetheefficiencyofsolvingcomplexmodelswhileensuringtheaccuracyof
thesolutions. VNS-GdemonstratesbetterperformancethanVNS-Rintermsofsolution
qualityandsolutiontime. Thisresultisconsistentwiththefindingsofotherresearchers.
Intheapplicationofthemixed-integerprogrammingmodel,VNS-GoutperformsVNS-
R in overall performance, especially in the location allocation problem in supply chain
management, where VNS-G not only exhibits better behavioral characteristics but also
requireslesssolutiontime.

Sustainability2025,17,10591 20of28
Table4.ComparisonofthetwoalgorithmsandCPLEXinsmall-scalearithmeticcases.
CPLEX VNS-R Comparison VNS-G Comparison
CaseID
f C T C f R T R T T R C GAP R f G T G T T G C GAP G
A2-3-5-3-3-1 0.8721 3.2 0.8721 12.7 3.97 0.00% 0.8721 10.5 3.28 0.00%
A2-3-5-3-3-2 0.8786 4.2 0.8786 11.9 2.83 0.00% 0.8786 11.0 2.61 0.00%
A2-3-5-3-3-3 0.8749 5.8 0.8749 11.1 1.91 0.00% 0.8749 10.3 1.78 0.00%
A2-3-5-3-3-4 0.8812 5.2 0.8811 12.3 2.37 0.00% 0.8812 10.6 2.04 0.00%
Avg. 0.8773 4.2 0.8773 12 2.86 0.00% 0.8773 10.6 2.52 0.00%
A3-3-5-3-3-1 0.8846 6.9 0.8846 22.4 3.25 0.00% 0.8846 12.4 1.80 0.00%
A3-3-5-3-3-2 0.8721 7.6 0.8721 20.8 2.74 0.00% 0.8721 14.8 1.95 0.00%
A3-3-5-3-3-3 0.8785 10.4 0.8785 18.9 1.82 0.00% 0.8785 13.9 1.34 0.00%
A3-3-5-3-3-4 0.8812 9.9 0.8812 21.5 2.17 0.00% 0.8812 15.3 1.55 0.00%
Avg. 0.8793 8.7 0.8793 20.9 2.40 0.00% 0.8793 14.1 1.62 0.00%
A2-4-10-3-3-1 0.8819 8.2 0.8819 12.3 1.50 0.00% 0.8819 10.1 1.23 0.00%
A2-4-10-3-3-2 0.8968 5.6 0.8968 14.1 2.52 0.00% 0.8968 10.8 1.93 0.00%
A2-4-10-3-3-3 0.9066 7.5 0.9066 13.2 1.76 0.00% 0.9066 10.6 1.41 0.00%
A2-4-10-3-3-4 0.9102 8.3 0.9102 15.2 1.83 0.00% 0.9102 12.1 1.46 0.00%
Avg. 0.8963 7.4 0.8963 13.7 1.85 0.00% 0.8963 11.9 1.61 0.00%
A3-4-10-3-3-1 0.8812 15.1 0.8812 21.2 1.40 0.00% 0.8812 15.6 1.03 0.00%
A3-4-10-3-3-2 0.8888 19.5 0.8888 21.4 1.10 0.00% 0.8888 16.3 0.84 0.00%
A3-4-10-3-3-3 0.8745 22.7 0.8745 21.6 0.95 0.00% 0.8745 15.8 0.70 0.00%
A3-4-10-3-3-4 0.8778 22.7 0.8778 21.6 0.95 0.00% 0.8778 17.1 0.75 0.00%
Avg. 0.8826 20 0.8826 21.45 1.07 0.00% 0.8826 16.2 0.81 0.00%
A2-5-15-3-3-1 0.8821 20.1 0.8821 11.4 0.57 0.00% 0.8821 10.8 0.54 0.00%
A2-5-15-3-3-2 0.8797 22.2 0.8797 11.9 0.54 0.00% 0.8797 10.1 0.45 0.00%
A2-5-15-3-3-3 0.8971 22.8 0.8971 10.6 0.46 0.00% 0.8971 10.9 0.48 0.00%
A2-5-15-3-3-4 0.9052 23.3 0.9052 12.1 0.52 0.00% 0.9052 11.9 0.51 0.00%
Avg. 0.889 22.1 0.889 11.5 0.52 0.00% 0.889 10.8 0.49 0.00%
A3-5-15-3-3-1 0.8977 32.4 0.8977 22.4 0.69 0.00% 0.8977 18.2 0.56 0.00%
A3-5-15-3-3-2 0.8959 29.6 0.8959 22.8 0.77 0.00% 0.8959 17.9 0.60 0.00%
A3-5-15-3-3-3 0.8992 25.3 0.8992 24.7 0.98 0.00% 0.8992 19.7 0.78 0.00%
A3-5-15-3-3-4 0.9013 35.1 0.9013 24.7 0.70 0.00% 0.9013 19.7 0.56 0.00%
Avg. 0.8983 30.6 0.8983 23.3 0.76 0.00% 0.8983 18 0.59 0.00%
Note:(1)fC,fR,fGdenotetheobjectivevaluessolvedbytheCPLEX,VNS-R,andVNS-Galgorithms;(2)TC,TR,TG
denotethetimeconsumedbythesolutionofCPLEX,VNS-R,andVNS-Galgorithms;(3)GAPR =(fC −fR )/fC;
GAPG =(fC −fG )/fC.
Table5.ComparisonofthetwoalgorithmsandCPLEXinthemedium-sizedcase.
CPLEX VNS-R Comparison VNS-G Comparison
CaseID
f C T C f R T R T T R C GAP R f G T G T T G C GAP G
A5-5-20-3-3-1 0.8997 326.8 0.8997 103.8 0.32 0.00% 0.8997 59.6 0.18 0.00%
A5-5-20-3-3-2 0.8984 278.7 0.8984 98.6 0.35 0.00% 0.8984 54.4 0.20 0.00%
A5-5-20-3-3-3 0.8932 263.6 0.8932 97.3 0.37 0.00% 0.8932 57.6 0.22 0.00%
A5-5-20-3-3-4 0.9047 287.3 0.9047 105.9 0.37 0.00% 0.9047 61.6 0.21 0.00%
Avg. 0.899 289.1 0.899 101.4 0.35 0.00% 0.899 58.3 0.20 0.00%
A5-10-25-3-3-1 0.8779 783.8 0.8779 111.3 0.14 0.00% 0.8779 57.4 0.07 0.00%
A5-10-25-3-3-2 0.8699 812.1 0.8699 105.6 0.13 0.00% 0.8699 62.4 0.08 0.00%
A5-10-25-3-3-3 0.8322 804.1 0.8211 104.1 0.13 1.33% 0.8322 57.5 0.07 0.00%
A5-10-25-3-3-4 0.8484 798.8 0.8363 115.4 0.14 1.43% 0.8392 57.5 0.07 1.08%
Avg. 0.8571 799.7 0.8513 109.1 0.14 0.68% 0.8548 58.7 0.07 0.27%
A5-15-30-3-3-1 0.8447 2224.2 0.8311 129.5 0.06 1.61% 0.8447 59.2 0.03 0.00%
A5-15-30-3-3-2 0.8515 2483.5 0.8379 112.3 0.05 1.60% 0.8503 67.7 0.03 0.14%
A5-15-30-3-3-3 0.8442 2560.7 0.8376 116.4 0.05 0.78% 0.8442 58.8 0.02 0.00%

Sustainability2025,17,10591
21of28
Table5.Cont.
|     | CPLEX |     | VNS-R |     | Comparison |     | VNS-G |     | Comparison |     |
| --- | ----- | --- | ----- | --- | ---------- | --- | ----- | --- | ---------- | --- |
CaseID
T
|     | f   | T   | f   | T   | T R | GAP | f   | T   | G   | GAP |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|     | C   | C   | R   |     | R T | R   | G   | G   | T   | G   |
|     |     |     |     |     | C   |     |     |     | C   |     |
A5-15-30-3-3-4 0.8612 2760.4 0.8486 125 0.05 1.46% 0.8452 64.1 0.02 1.86%
Avg. 0.8504 2507.2 0.8388 120.8 0.05 1.36% 0.8461 62.45 0.02 0.51%
Note:(1)fC,fR,fGdenotetheobjectivevaluessolvedbytheCPLEX,VNS-R,andVNS-Galgorithms;(2)TC,TR,TG
denotethetimeconsumedbythesolutionofCPLEX,VNS-R,andVNS-Galgorithms;(3)GAPR =(fC −fR )/fC;
|     | GAPG =(fC | −fG )/fC. |     |     |     |     |     |     |     |     |
| --- | --------- | --------- | --- | --- | --- | --- | --- | --- | --- | --- |
5.2. Large-ScaleExperiments
InordertoverifytheeffectivenessoftheVNS-RandVNS-Galgorithmsproposedin
thisstudyindepth, weconductedextendedtestsonthevalueoftheschemes. Mostof
thevariablesinTable6havethesamemeaningsasthoseinTable5. Theonlydifference
liesintheGAPmetric,whichrepresentsthedifferencebetweentheVNS-GandVNS-R
|     | solutionsandiscalculatedas(f |     |     |     | − )/f |                                          |     |     |     |     |
| --- | ---------------------------- | --- | --- | --- | ----- | ---------------------------------------- | --- | --- | --- | --- |
|     |                              |     |     |     | G f R | G ;thesubscriptsRandGalsorefertotheVNS-R |     |     |     |     |
and VNS-G algorithms, respectively. It is obvious that the average computation time
shows an upward trend as the scale of the algorithm increases. According to the data
summarizedinTable6,CPLEXfailstofindafeasiblesolutionin7200s,whichlimitsits
feasibilityinpracticalapplications. Whencomparingthesetwoalgorithmswithdifferent
initialsolutions,wefindthatVNS-Gisalwaysabletofindthesameorbettersolutionsas
VNS-R.ThecomputationtimeofVNS-Gshowsalinearincreaseasthesizeofthealgorithm
increases,anditsperformanceissuperiortothatofCPLEXandVNS-R.Thisresultfurther
provestheefficiencyandrobustnessoftheVNS-Galgorithmindealingwithlarge-scale
problems and also shows that different initial solutions can affect the efficiency of the
VNSalgorithm.
Table6.ComparisonofthetwoalgorithmsandCPLEXinlarge-scalecases.
|     | CPLEX |     |     | VNS-R |     | VNS-G |     |     | Comparison |     |
| --- | ----- | --- | --- | ----- | --- | ----- | --- | --- | ---------- | --- |
CaseID
T
|     | f   | T C |     | f   | T R | f   | T G |     | R GAP | GR  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | ----- | --- |
|     | C   |     |     | R   |     | G   |     |     | T G   |     |
A10-10-40-3-3-1 - >7200 0.8225 1886.8 0.8325 1186.8 1.59 1.20%
A10-10-40-3-3-2 - >7200 0.8123 1788.7 0.8422 1188.7 1.50 3.55%
A10-10-40-3-3-3 - >7200 0.8099 1906.6 0.8399 1206.2 1.58 3.57%
A10-10-40-3-3-4 - >7200 0.8245 1906.3 0.8514 1087.5 1.75 3.16%
| Avg. | -   | >7200 | 0.8173 |     | 1872.1 | 0.8415 | 1167.3 |     | 1.60 | 2.88% |
| ---- | --- | ----- | ------ | --- | ------ | ------ | ------ | --- | ---- | ----- |
A10-10-40-3-3-1 - >7200 0.8122 2084.9 0.8322 1584.6 1.32 2.40%
A10-10-40-3-3-2 - >7200 0.8187 2030.4 0.8387 1430.2 1.42 2.38%
A10-10-40-3-3-3 - >7200 0.8012 2017.6 0.8212 1577.6 1.28 2.44%
A10-10-40-3-3-4 - >7200 0.8271 2118.7 0.8411 1442.4 1.47 1.66%
| Avg. | -   | >7200 | 0.8148 |     | 2062.9 | 0.8333 | 1508.7 |     | 1.37 | 2.22% |
| ---- | --- | ----- | ------ | --- | ------ | ------ | ------ | --- | ---- | ----- |
A10-10-50-3-3-1 - >7200 0.8191 1925.8 0.8511 1225.8 1.57 3.76%
A10-10-50-3-3-2 - >7200 0.8191 1897.3 0.8531 1197.3 1.58 3.99%
A10-10-50-3-3-3 - >7200 0.8101 1812.4 0.8503 1212.3 1.50 4.73%
A10-10-50-3-3-4 - >7200 0.8073 1978.1 0.8487 1198.2 1.65 4.88%
| Avg. | -   | >7200 | 0.8139 |     | 1903.4 | 0.8508 | 1208.4 |     | 1.58 | 4.34% |
| ---- | --- | ----- | ------ | --- | ------ | ------ | ------ | --- | ---- | ----- |
A10-10-50-3-3-1 - >7200 0.8099 2071.2 0.8499 1871.2 1.11 4.71%
A10-10-50-3-3-2 - >7200 0.8304 2123.7 0.8603 1823.7 1.16 3.48%
| A10-10-50-3-3-3 | -   | >7200 | 0.8209 |     | 2073 | 0.8509 | 1973 |     | 1.05 | 3.53% |
| --------------- | --- | ----- | ------ | --- | ---- | ------ | ---- | --- | ---- | ----- |
A10-10-50-3-3-4 - >7200 0.8484 2217.3 0.8673 1845.3 1.20 2.18%
| Avg. | -   | >7200 | 0.8274 |     | 2121.3 | 0.8571 | 1878.3 |     | 1.13 | 3.47% |
| ---- | --- | ----- | ------ | --- | ------ | ------ | ------ | --- | ---- | ----- |
Note:(1)fC,fR,fGdenotetheobjectivevaluessolvedbytheCPLEX,VNS-R,andVNS-Galgorithms;(2)TC,TR,TG
|     |     |     |     |     |     |     |     |     | = (fG | − fR) |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | ----- | ----- |
denotethetimeconsumedbythesolutionofCPLEX,VNS-R,andVNS-Galgorithms;(3)GAPGR f .
G

Sustainability2025,17,10591 22of28
ThroughthecomparativeanalysisofVNS-GandVNS-Rindifferentscaleproblems,
as shown in Table 6, in the same VNS structure, the objective values (comprehensive
satisfaction)solvedbyusingtheVNS-Galgorithmareallbetterthantheresultsofusingthe
VNS-Ralgorithm(f ≥ f ),andthevaluesofGAP areallcontrolledwithin5%. Thus,
G R GR
wedrawthefollowingconclusions:
(1) Awell-designedcomplexmixed-integerplanningmodelplaysakeyroleinconstruct-
ingascientificresourcetransmissionnetworkinthecaseofasuddendisaster.
(2) Ahigh-qualityinitialsolutioncanacceleratetheconvergenceofthealgorithm. Ifthe
initialsolutionisalreadyclosetotheincumbentsolution,theVNSalgorithmmayonly
needasmallnumberoflocalsearchandperturbationstepstoreachtheincumbentor
near-incumbentsolution.
(3) Byoptimizingtheresourceallocationandtransmissionstrategies,themodelaimsto
maximizetheoverallsatisfactionandensurethatthedemandineachaffectedregion
isfullysatisfied.
(4) Thequalityoftheinitialsolutiondirectlyaffectsthequalityofthefinalsolution,anda
goodinitialsolutioncanimprovetheoptimizationofthefinalsolution,especiallyin
problemswithalargesolutionspaceandhighsearchdifficulty.
(5) Differentinitialsolutionsmaycausethealgorithmtotakedifferentpathsinthesearch
process,andastableinitialsolutioncanmakethealgorithmproducemoreconsistent
resultsinmultipleruns. IntheVNSalgorithm,theinitialsolutiongeneratedbythe
greedyalgorithmusuallyprovidesastartingpointthatisclosertotheincumbentsolu-
tionbecauseitisbasedonlocallyincumbentdecisions. Suchaninitialsolutionhelps
theVNSalgorithmtoexplorethesolutionspacemoreefficientlyduringsubsequent
searches,whichmayincreasetheprobabilityoffindingagloballyincumbentsolution.
6. SensitivityAnalysis
Theoptimizationofemergencyrescuesystemsisinfluencedbyvariationsinmultiple
parameters. Toexploretheimpactofthesechanges,weconductedasensitivityanalysis
ofthetotalbudget,numberofrepairteams,anddemandcoefficient. Theconfigurations
A3-5-15-3-3,A5-5-20-3-3,andA10-10-40-3-3representsmall,medium,andlargeinstances,
respectively. Beyondcomparingchangesinobjectivefunctionvaluesbasedonsensitivity
analysis, we also documented variations in different metrics of the obtained solutions,
particularlythosereflectingservicequality: servicecoverageandaveragedelaytime.
6.1. AnalysisofTotalBudgetImpactonDecision-Making
Thefirstsensitivityanalysisexaminestheinfluenceofthesystem’stotalbudget. To
evaluatetheimpactofthetotalbudgetonvariousmetrics,thissectionconductssensitivity
analysis using different total budgets. Based on the selected calculation examples, the
budgetproportionforeachexampleisscaled. ByuniformlyincreasingtheCparameter
representingthetotalbudgetforeachscaledexample, thechangesinthetargetvaluef
(comprehensivesatisfaction),servicecoveragerate,andaveragedelaytimeareanalyzed.
TheresultsareshowninFigure7.
AsshowninFigure7A–C,sensitivityanalysisofbudgetvariationsrevealsthatin-
creasingthebudgetgenerallyenhancestheoverallsatisfactionandservicecoverageof
theemergencyrescuesystemwhileeffectivelyreducingtheaveragedelaytime. However,
improvementsinallperformancemetricsexhibitdiminishingmarginalreturns,meaning
thatbeyond1.1timesthebaselinebudget,therateofbenefitgrowthslowssignificantly.The
analysisalsorevealspronouncedscaledifferences: thesmall-scalecasestudy(A3-5-15-3-3)
exhibitsincumbentabsoluteperformanceandthehighestsensitivitytobudgetchanges
(delay reduction up to 26%), while the medium-scale scenario (A5-5-20-3-3) shows the

Sustainability2025,17,10591 23of28
greatest magnitude of performance improvement. Conversely, the large-scale scenario
(A10-10-40-3-3)exhibitsarelativelysluggishresponseandrequiressubstantiallyhigher
budgetstoachievenoticeablegains. Collectively,thesefindingsindicatethatbudgetalloca-
tionstrategiesshouldprioritizesmall-to-medium-scaleemergencyscenariosandmaintain
budgetswithinthe1.0–1.1timesbenchmarkrangetoachieveincumbentcost-effectiveness.
Figure7.Sensitivityanalysisofthetotalbudget:(A)Impactoncomprehensivesatisfaction;(B)Impact
onservicecoveragerate;(C)Impactonaveragedelaytime.
6.2. SensitivityAnalysisoftheNumberofRepairTeams
Toexaminetheimpactofthenumberofrepairteamsonthetargetvalue f (overall
satisfaction),thissectionconductsasensitivityanalysisusingadifferentnumberofrepair
teams.Underthesamecasestudyscale,itanalyzeschangesinthetargetvaluef(overallsat-
isfaction),servicecoveragerate,andaveragedelaytime. TheresultsareshowninFigure8.
Figure8. Sensitivityanalysisofthenumberofrepairteams: (A)Small-scaleemergencysystem;
(B)Medium-scaleemergencysystem;(C)Large-scaleemergencysystem.
AsshowninFigure8,theimpactofthenumberofrepairteamsontheperformance
ofemergencysystemsofvaryingscalesisrevealed, characterizedbypronouncedscale
effectsanddiminishingmarginalreturns. Emergencysystemsofdifferentscalesexhibit
distinctlydifferentresponsestovariationsinthenumberofrepairteams. Asillustrated
inFigure8A,small-scaleexperimentsdemonstratehighlysensitiveresponses. Increasing
teams from1to4 reduces the delay time by 40% (from 14.73 h to 8.83 h) while steadily
improving satisfaction and coverage. This indicates that adding teams directly and ef-
fectively resolves bottlenecks in small systems. As shown in Figure 8B, medium-scale
experimentsexhibitnoticeableresponsesbutfaceathresholdforactivation. Increasing
teamsfrom2to5reducedlatencyby24.5%(from14.87hto11.22h),withsatisfactionand
coverage showing significant improvement only after reaching 4 teams. This indicates
thatacriticalmassofteamsisrequiredfornoticeableeffects. AsshowninFigure8C,the

Sustainability2025,17,10591 24of28
large-scalecaseexhibitedsluggishresponsewiththefastestdiminishingreturns.Increasing
teamsfrom3to7reducedlatencybyonly17.8%(from16.61hto13.66h),withminimal
gains in satisfaction and coverage. This suggests that for large and complex networks,
addingrepairteamsaloneyieldslimitedoverallperformanceimprovements,potentially
requiringmorecomprehensiveoptimization. Allsystemsexhibitdiminishingmarginal
returns. Asthenumberofteamsincreases,theperformanceimprovementperadditional
team—particularly in reducing the delay time—gradually diminishes. For instance, in
smallsystems,addingthesecondteamslashesthedelaybynearly3h,whilethefourth
teamcontributeslessthan1.3hofreduction. Thenumberofrepairteamsdirectlydeter-
minestheroadnetwork’scapacity,makingitsimpactondelaytimethemostimmediate
andsignificant. Satisfactionandcoverageratesexhibitrelativelydelayedresponsestothe
numberofteams,especiallyinmedium-to-largesystems. Thesemetricstypicallybegin
improving only after reaching a “critical threshold” (e.g., 4 teams in the medium-scale
simulation),indicatingthatoveralllogisticsefficiencyundergoesqualitativeimprovement
onlyaftercriticalpathsarecleared.
Theimpactofthenumberofrepairteamsonemergencysystemperformanceexhibits
pronouncedscaleeffectsanddiminishingmarginalreturns: smallsystemsrespondmost
sensitively, where increasing teams from 1 to 4 drastically reduces delay by 40% while
simultaneouslyboostingsatisfactionandcoverage. Medium-sizedsystemsfaceanotice-
able activation threshold, requiring 4–5 teams to achieve a 24.5% delay reduction and
performanceenhancement. Largesystemsrespondrelativelysluggishly,whereincreasing
teamsfrom3to7yieldsonlya17.8%delayimprovementwithminimalsatisfactiongrowth.
Thisindicatesthataddingrepairteamssignificantlybenefitssmall-to-mediumsystems,but
complexlargesystemsrequirecomplementaryoptimizationstrategies. Allsystemsexhibit
diminishingreturnswitheachadditionalteam.
6.3. AnalysisofDemandCoefficientImpactonDecision-Making
Toexaminetheinfluenceoftheminimumdemandcoefficienta atthedisaster-affected
1
pointontheobjectivevaluef(comprehensivesatisfaction),thissectionanalyzeschanges
in f (comprehensive satisfaction), service coverage rate, and average delay time under
differentcalculationscenarios. TheresultsareshowninFigure9.
As shown in Figure 9, sensitivity analysis of variations in the minimum demand
coefficient(a )revealsthatthiscoefficientexertsasystemicinfluenceontheperformanceof
1
theemergencyrescuesystem. AsdepictedinFigure9A,D,G,increasinga from0.6to1.0
1
leadstoadeclineinoverallsatisfactionacrossallscaledexperiments. Satisfactiononly
exhibitsasignificantsurgeoncethenumberofteamsexceedsacriticalthreshold. This
indicatesthatacertainscaleofteamdeploymentisnecessarytoeffectivelyinitiateandsub-
stantiallyenhancerescueoutcomes. AsdepictedinFigure9B,E,H,thethreecoveragerate
linechartssimilarlyexhibitconsistentdownwardtrends,withpatternshighlyanalogous
tothesatisfactioncurves. Thisoccursbecausethecoveragerateformsacrucialfounda-
tion for satisfaction; the inability to meet higher demand standards inevitably reduces
thenumberofdisasterpointsthatcanbecovered. Thechartsrevealthatnosystemsize
achieves100%coverage,withallfallingtoapproximately0.8orlowerunderthehighest
standard(a =1.0).Thisvisuallydemonstratesthatpursuing100%fulfillmentofalldisaster
1
sites’maximumdemandsisunrealisticinemergencylogistics,ultimatelydiminishingthe
system’soverallcoverageefficiency. AsshowninFigure9C,F,I,thethreedelaytimeline
chartsexhibitaclearupwardtrend. Thisrepresentsoneofthemostcriticalfindingsof
thisanalysis: increasingdemandstandardsdirectlyleadstohigheraveragesystemdelay
times. Thedelaycurvesforlarge-scalesystemsconsistentlyoccupythehighestpositions,
withtheirdeterioration(slope)becomingmorepronouncedasa increases. Thisfurther
1

Sustainability2025,17,10591 25of28
demonstrates the vulnerability of large-scale systems when confronting high-standard
demands. Alltrendlinesconvergeonthesameconclusion: settingtheminimumdemand
coefficienta constitutesacriticalstrategicdecision. Highera_1valuescomeatthecostof
1
reducedoverallsystemefficiency(decreasedsatisfactionandcoverage)andperformance
(increasedlatency).
Figure 9. Sensitivity analysis of the minimum demand coefficient at disaster sites: (A) Overall
satisfaction(small-scale);(B)Servicecoveragerate(small-scale);(C)Averagedelaytime(small-scale);
(D)Overallsatisfaction(medium-scale);(E)Servicecoveragerate(medium-scale);(F)Averagedelay
time(medium-scale);(G)Overallsatisfaction(large-scale);(H)Servicecoveragerate(large-scale);
(I)Averagedelaytime(large-scale).
7. Conclusions
Thisstudyconstructsasecondaryemergencyreliefnetworkmodelthattakesroad
rehabilitation into account and aims to optimize the efficiency of emergency material
distribution. This study proposes a material distribution model with the optimization
objectiveofcomprehensivesatisfactioninthecontextofuncertaintyindemandandtrans-
porttime. Inthisstudy,theVNS-RandVNS-Galgorithmsareusedtosolvethemodel,
andtheeffectsofdifferentinitialsolutionsontheperformanceoftheVNSalgorithmare
analyzed. TheresultsofthealgorithmsshowthattheinitialsolutionqualityoftheVNS-G
algorithm is better than that of the VNS-R algorithm, and both algorithms are able to
solvethelarge-scaleproblemefficientlyinareasonabletime. Wesummarizethefollowing
literaturecontributions.
(1) Distributionandschedulingdecisionsinemergencylogisticsarecloselyrelated. Ar-
rangingdistributionvehiclesaccordingtospecificdemandsanddeployingthemfrom

Sustainability2025,17,10591 26of28
supplypointsandemergencywarehousestoreachthedisaster-strickenpointsusu-
allyneedstobesynchronizedwithschedulingoptimizationtoensurethatsufficient
transportresourcesareavailabletomeetthedemands. Therefore,ourmodelaims
tosolveanemergencylogisticsdistributionandschedulingprobleminvolvinglong-
andshort-termdiscontinuities. Thisstudytakesintoaccountmoreuncertaintiesin
real-worldenvironmentsthantheexistingliterature,especiallythespecialneedsof
emergencylogisticsanddistribution. Wealsoconsiderthestochasticnatureofthelo-
cationandtimeofthedisaster,theuncertaindemandforvariousemergencysupplies,
andtheuncertaintyofthestatusofthedistributionpathsbetweenthesupplypoints,
emergencywarehouses,andthedisastersites.
(2) TherelationshipbetweentheVNSalgorithmicprocessandthemodelcharacteristics
needstobeemphasizedwhendevelopingthemodelsolutiontool. Sincethedecision
variablesinthetwostagesofthemodelinteractwitheachother,intheVNDprocess,
we nested the neighborhood structure of decision variables belonging to different
stages. Unliketheindependentneighborhoodstructuresinmoststudies,thismethod
effectivelypreventsthealgorithmfromlosingpotentialincumbentsolutionsinthe
localsearch. Thenumericalexperimentalresultsshowthatthesolutiontimeofthe
VNS-Galgorithmisreducedbyabout30%comparedtotheVNS-Ralgorithm,andit
ismoreeffective.
(3) Weconductedacomprehensivesensitivityanalysistorevealhowdifferentparameters
areinfluencedbythetotalbudgetC,thenumberofrepairteamsr,andtheminimum
demand coefficient at affected points. This analysis provides valuable insights for
practical management. Specifically, to reduce rescue costs, road rescue managers
shouldrationallyallocatematerialsuppliesandensurethenumberofrepairteams
alignswiththeminimumdemandcoefficientataffectedpoints. Furthermore,they
shouldrecognizethatdeterminingthenumberofrepairteamsandschedulingarrange-
mentsrequiresbalancingeconomicefficiency(i.e.,controllingtotalbudgetC)with
timeliness(i.e.,enhancingaffectedsitesatisfactionanddemandresponsespeed). The
marginaleffectofadditionalresources(suchasrepairteamsandsupplies)diminishes
progressivelyuntilitreacheszero.
Thisstudyhassomelimitations. Scenario-basedoptimizationrequiresidentifyingthe
locationandrescueneedsofeachaccident-proneroadwayinordertobuildthescenarios.
Infuturestudies,attemptsshouldbemadetoconsiderrobustoptimizationunderdynamic
roadconditions. Inthispaper,thefocusofsolvingtheemergencylogisticsanddistribution
problem,consideringroadconditions,istodefineasuitableuncertaintysetfordifferent
hazards. The model can be applied to situations where there are not enough data to
calibratethestochasticplanningmodel.Inaddition,althoughweextendourmodeltocases
whereextremedisastersmayarisedynamicallytoproposeasimpledynamicscheduling
mechanisminthefuture,alternativeapproaches,suchaspredictivepathalgorithms,can
be used to improve the performance of emergency logistics distribution in real-world
environments. The capability of material supply services is crucial in the emergency
responsesystem. Futureresearchcouldfocusontheintegrationofemergencymaterial
supplyanddistributionandexploretheapplicationofmultimodaltransportmodessuch
ashelicopters,drones,andvehicles. Inaddition,inemergencyrescueoperations,theremay
becontradictionsbetweenobjectives,suchastheshortesttransporttime,thelowestcost,
andthemaximumcoverage. Futureresearchcouldbedevotedtothetrade-offproblemin
multi-objectiveoptimization,aimingtoachieverapidresponseandmaximizetheeffectof
emergencyrescuebasedonacarefulconsiderationofvariousfactors.

Sustainability2025,17,10591 27of28
Author Contributions: Conceptualization, B.W., C.H. and Y.G.; Methodology, B.W. and C.H.;
Software, B.W. and C.H.; Validation, B.W., C.H. and Y.G.; Formal analysis, B.W.; Investigation,
B.W.;Resources,B.W.;Datacuration,B.W.andY.G.;Writing—originaldraft,B.W.,C.H.andY.G.;
Writing—review&editing,B.W.,C.H.andY.G.;Visualization,Y.G.;Supervision,B.W.Allauthors
havereadandagreedtothepublishedversionofthemanuscript.
Funding:ThisresearchwasfundedbytheMinistryofEducationofthePeople’sRepublicofChina,
HumanitiesandSocialSciencesProject,grantnumber22YJC630128.
InstitutionalReviewBoardStatement:Notapplicable.
InformedConsentStatement:Notapplicable.
DataAvailabilityStatement:Dataarecontainedwithinthearticle.
ConflictsofInterest:Theauthorsdeclarenoconflictofinterest.
References
1. Zhong,S.;Cheng,R.;Jiang,Y.;Wang,Z.;Larsen,A.;Nielsen,O.A.Risk-averseoptimizationofdisasterrelieffacilitylocationand
vehicleroutingunderstochasticdemand.Transp.Res.PartELogist.Transp.Rev.2020,141,102015.[CrossRef]
2. Aghaie,S.;Karimi,B.Location-allocation-routingforemergencysheltersbasedongeographicalinformationsystem(ArcGIS)by
NSGA-II(casestudy:EarthquakeoccurrenceinTehran(District-1)).Socio-Econ.Plan.Sci.2022,84,101420.[CrossRef]
3. Zhuang,X.;Zhang,Y.;Han,L.;Jiang,J.;Hu,L.;Wu,S.Two-stagestochasticprogrammingwithrobustconstraintsforthelogistics
networkpost-disruptionresponsestrategyoptimization.Front.Eng.Manag.2023,10,67–81.[CrossRef]
4. Balcik, B.; Yanıkog˘lu, I˙. A robust optimization approach for humanitarian needs assessment planning under travel time
uncertainty.Eur.J.Oper.Res.2020,282,40–57.[CrossRef]
5. Vahdani,B.;Veysmoradi,D.;Noori,F.;Mansour,F.Two-stagemulti-objectivelocation-routing-inventorymodelforhumanitarian
logisticsnetworkdesignunderuncertainty.Int.J.DisasterRiskReduct.2018,27,290–306.[CrossRef]
6. Sabouhi,F.;Bozorgi-Amiri,A.;Vaez,P.Stochasticoptimizationfortransportationplanningindisasterreliefunderdisruptionand
uncertainty.Kybernetes2020,50,2632–2650.[CrossRef]
7. Wang, Q.; Nie, X.F. A stochastic programming model for emergency supply planning considering transportation network
mitigationandtrafficcongestion.Socio-Econ.Plan.Sci.2022,79,101119.[CrossRef]
8. Aliakbari,A.;RashidiKomijan,A.;Tavakkoli-Moghaddam,R.;Najafi,E.Anewrobustoptimizationmodelforrelieflogistics
planningunderuncertainty:Areal-casestudy.SoftComput.2022,26,3883–3901.[CrossRef]
9. Khanchehzarrin,S.;Panah,M.G.;Mahdavi-Amiri,N.;Shiripour,S.Abi-levelmulti-objectivelocation-routingoptimizationmodel
fordisasterreliefoperationsconsideringpublicdonations.Socio-Econ.Plan.Sci.2022,80,101165.[CrossRef]
10. Vidal,T.;Crainic,T.G.;Gendreau,M.;Prins,C.Ahybridgeneticalgorithmwithadaptivediversitymanagementforalargeclass
ofvehicleroutingproblemswithtime-windows.Comput.Oper.Res.2013,40,254–262.[CrossRef]
11. Rahafrooz,M.;Alinaghian,M.Anovelrobustchanceconstrainedpossibilisticprogrammingmodelfordisasterrelieflogistics
underuncertainty.Int.J.Ind.Eng.Comput.2016,7,327–334.[CrossRef]
12. Rawls,C.G.;Turnquist,M.A.Pre-positioningofemergencysuppliesfordisasterresponse.Transp.Res.PartB2010,44,521–534.
[CrossRef]
13. Du,M.;Yi,H.Researchonmulti-objectiveemergencylogisticsvehicleroutingproblemunderconstraintconditions.J.Ind.Eng.
Manag.2013,6,258–266.[CrossRef]
14. Bruni,M.;Beraldi,P.;Khodaparasti,S.Afastheuristicforroutinginpost-disasterhumanitarianrelieflogistics. Transp. Res.
Procedia2018,30,304–313.[CrossRef]
15. Li,Q.;Tu,W.;Zhao,L.ReliableRescueRoutingOptimizationforUrbanEmergencyLogisticsunderTravelTimeUncertainty.Int.
J.Geo-Inf.2018,7,77.
16. Sanci,E.;Daskin,M.S.AnintegerL-shapedalgorithmfortheintegratedlocationandnetworkrestorationproblemindisaster
relief.Transp.Res.PartBMethodol.2021,145,152–184.[CrossRef]
17. Aslan, E.; Çelik, M. Pre-positioning of relief items under road/facility vulnerability with concurrent restoration and relief
transportation.IISETrans.2019,51,847–868.[CrossRef]
18. Yuan, Y.; Wang, D. Path selection model and algorithm for emergency logistics management. Comput. Ind. Eng. 2009,
56,1081–1094.[CrossRef]
19. Khorsi,M.;Chaharsooghi,S.K.;Bozorgi-Amiri,A.;Kashan,A.H.Amulti-objectivemulti-periodmodelforhumanitarianrelief
logisticswithsplitdeliveryandmultipleusesofvehicles.J.Syst.Sci.Syst.Eng.2020,29,360–378.[CrossRef]

Sustainability2025,17,10591 28of28
20. Huang,X.;Song,L.Anemergencylogisticsdistributionroutingmodelforunexpectedevents.Ann.Oper.Res.2018,269,223–239.
[CrossRef]
21. Ozdamar,L.;Aksu,D.T.;Ergünes,B.Coordinatingdebriscleanupoperationsinpostdisasterroadnetworks.Socio-Econ.Plan.Sci.
2014,48,249–262.[CrossRef]
22. Chang,M.S.;Tseng,Y.L.;Chen,W.Ascenarioplanningapproachforthefloodemergencylogisticspreparationproblemunder
uncertainty.Transp.Res.PartELogist.Transp.Rev.2007,43,737–754.[CrossRef]
23. Dantzig,G.B.;Ramser,J.H.TheTruckDispatchingProblem.Manag.Sci.1959,6,80–91.[CrossRef]
24. Vahdani,B.;Veysmoradi,D.;Shekari,N.;Mousavi,S.M.Multi-Objective,Multi-PeriodLocation-RoutingModeltoDistributeRelief
AfterEarthquakebyConsideringEmergencyRoadwayRepair;Springer:London,UK,2018.
25. Qing,C.Vehicleschedulingmodelofemergencylogisticsdistributionbasedoninternetofthings.Int.J.Appl.Decis.Sci.2018,
11,36–54.[CrossRef]
26. Gao,X.Abi-levelstochasticoptimizationmodelformulti-commodityrebalancingunderuncertaintyindisasterresponse.Ann.
Oper.Res.2019,319,115–148.[CrossRef]
27. Liu,J.;Xie,K.Emergencymaterialstransportationmodelindisastersbasedondynamicprogrammingandantcolonyoptimization.
Kybernetes2017,46,656–671.[CrossRef]
28. Qin,J.;Ye,Y.;Cheng,B.R.;Zhao,X.;Ni,L.Theemergencyvehicleroutingproblemwithuncertaindemandundersustainability
environments.Sustainability2017,9,288.[CrossRef]
29. Ahmadi-Javid,A.;Seddighi,A.H.Alocation-routingproblemwithdisruptionrisk.Transp.Res.PartE2013,53,63–82.[CrossRef]
30. Rennemo,S.J.;Rø,K.F.;Hvattum,L.M.;Tirado,G.Athree-stagestochasticfacilityroutingmodelfordisasterresponseplanning.
Transp.Res.PartELogist.Transp.Rev.2014,62,116–135.[CrossRef]
31. Shen,L.;Tao,F.;Shi,Y.;Qin,R.OptimizationofLocation-RoutingProbleminEmergencyLogisticsConsideringCarbonEmissions.
Int.J.Environ.Res.PublicHealth2019,16,2982.[CrossRef]
32. Xu,J.;Yin,X.;Chen,D.;An,J.;Nie,G.Multi-criterialocationmodelofearthquakeevacuationshelterstoaidinurbanplanning.
Int.J.DisasterRiskReduct.2016,20,51–62.[CrossRef]
33. Lamb,J.D.Variableneighbourhoodstructuresforcyclelocationproblems.Eur.J.Oper.Res.2012,223,15–26.[CrossRef]
34. Sadati,M.E.H.;Çatay,B.Ahybridvariableneighborhoodsearchapproachforthemulti-depotgreenvehicleroutingproblem.
Transp.Res.PartELogist.Transp.Rev.2021,149,102293.[CrossRef]
Disclaimer/Publisher’sNote: Thestatements, opinionsanddatacontainedinallpublicationsaresolelythoseoftheindividual
author(s)andcontributor(s)andnotofMDPIand/ortheeditor(s).MDPIand/ortheeditor(s)disclaimresponsibilityforanyinjuryto
peopleorpropertyresultingfromanyideas,methods,instructionsorproductsreferredtointhecontent.