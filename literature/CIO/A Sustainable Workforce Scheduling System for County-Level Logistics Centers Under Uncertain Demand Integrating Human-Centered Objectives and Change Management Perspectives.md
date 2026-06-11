Article
A Sustainable Workforce Scheduling System for County-Level
Logistics Centers Under Uncertain Demand: Integrating
Human-Centered Objectives and Change
Management Perspectives
YixuanWu1,YuhanGong1,ZhenhengHu1,YiwenGao2andJunchiMa1,3,*
1 SchoolofTransportationEngineering,EastChinaJiaotongUniversity,Nanchang330013,China;
2023131005000210@ecjtu.edu.cn(Y.W.);2022131005000117@ecjtu.edu.cn(Y.G.);
2024138125604020@ecjtu.edu.cn(Z.H.)
2 SchoolofTransportation,BeijingJiaotongUniversity,Beijing100044,China;21114067@bjtu.edu.cn
3 JiangxiKeyLaboratoryofComprehensiveStereoscopicTrafficInformationPerceptionandFusion,EastChina
JiaotongUniversity,Nanchang330013,China
* Correspondence:3585@ecjtu.edu.cn
Abstract
Forlogisticsfacilitiesatthecountylevel,workforceschedulingisabasicoperationalcon-
cern. Althoughthesefacilitiesaredevelopingrapidly,theystillmostlyrelyonhumanand
semi-automatedwork. Significantdifferencesinemployeeproductivityandskilllevels,
alongwithregularchangesindemand,exacerbatethischallenge. Thisstudyproposesa
sustainability-orienteddual-objectiveoptimizationmodeltocoordinateoperationalcost
controlwithemployeewell-beingenhancement. Toaddressthisissue, wedesignedan
improvedGeneticAlgorithmthatcombinesheuristicinitializationwithspecializedrepair
operators, forming a systematic optimization framework. The effectiveness of the pro-
posedsystemdesignandalgorithmhasbeenvalidatedthroughreal-worldcasestudies.
Experimentalresultsdemonstratethatthismodelnotonlyachievesabalancebetweencost
andemployeesatisfactionunderuncertaindemandconditionsbutalsoprovidescounty-
levellogisticscenterswithsustainableschedulingsolutionsadaptabletobusinesschanges.
Managementrecommendationsbasedontheexperimentalresultsareproposed,suchas
implementingdifferentiatedschedulingstrategies,easingrestrictionsonmaximumwork-
inghourvariations,establishingaprogressiveoptimizationmechanism,andoptimizing
staffingandemployeestructureinaccordancewithcorporatecharacteristics. Thisstudy
providesscientificdecisionsupportforcounty-levellogisticssystemstoachievesustainable
operationsandhumanresourcemanagementtransformation.
Keywords: human-centeredsystemdesign;sustainableworkforcescheduling;uncertainty
AcademicEditors:ThrosturOlaf
andresilience;changemanagementinlogistics;geneticalgorithm;employeecomfort
SigurjonssonandJoséManuelRuano
delaFuente
Received:30January2026
Revised:4March2026
1. Introduction
Accepted:7March2026
Published:10March2026 WiththeadvancementofnationalstrategiesliketheIndustrialInternetandSmart
Copyright:©2026bytheauthors. Manufacturing,thelogisticsindustry,asafundamentalandpioneeringsectoroftheecon-
LicenseeMDPI,Basel,Switzerland.
omy,isenteringakeyperiodofopportunitytotransformtowardgreaterintelligenceanda
Thisarticleisanopenaccessarticle
strongerhumanfocus. Promotingnewsmartmanufacturingmodelsbasedon“human-
distributedunderthetermsand
machinecollaboration”and“human-centeredapproaches”isspecificallycalledforinthe
conditionsofthe CreativeCommons
Attribution(CCBY)license. “14thFive-YearPlanforSmartManufacturingDevelopment.”Ithighlightsthatinitiativesmust
Systems2026,14,295 https://doi.org/10.3390/systems14030295

Systems2026,14,295 2of40
concentrateonimprovingstaffskills,protectinglaborwelfare,andbolsteringorganiza-
tionalresilienceinadditiontoutilizingtechnologyempowerment[1]. Thispolicydirection
setsthepathformanagementoptimizationinthelogisticssectorbyreflectingtheequal
treatmentofhumandevelopmentandtechnicaladvancementatthenationallevel.
Meanwhile, the concept of Industry 5.0 has reinforced the importance of “human-
centered” principles in operational management. Instead of treating automation as an
ultimategoal,Industry5.0focusesoncollaborationbetweenhumansandmachines,the
improvementinskills, andthewell-beingofemployees. Itmakesuseoftechnologyto
develophumancapabilities,increaseproductivity,andprovideabetterworkingenviron-
ment[2,3]. Thisstrategyhasmadeitimperativetotransform“human-centered”concepts
intoworkable andeffectiveschedulingtechniques. Newdevelopmentsin thestudyof
logisticsoperationsmanagementarebeingdrivenbythisdemand.
The ambitious policy framework, however, stands in stark contrast to the actual
situationontheground. Atthecountylevel,relativelylowlaborcostscoexistwiththe
substantialinvestmentneededforautomatedequipment. Thegreatmajorityofcounty-
level logistics centers continue to rely mostly on human processes with relatively little
automation[4,5]. Againstthisbackdrop,operationalmanagementmustprioritizehuman
elements. However,conventionalandfrequentlyextensivemanagementapproachesare
posingseriousproblems. Thisisespeciallytrueforschedulingmodelsthatlackhuman-
centereddesignandscientificintegrity. Thesemodelsresultinunpredictableandhigh-
intensityworkschedules,whichloweremployeesatisfactionandcauseconsistentlyhigh
turnoverrates[6–8]. Incounty-levellogisticscenters,theproblemofpersonnelmobility
is particularly acute. For example, the turnover rate for express delivery workers in
Ningyang County is higher than 20%. Labor costs increase by an average of 12% each
yearasaresultoffrequentretrainingbroughtonbythisturnover[9]. Anindustry-wide
patternisrevealedbysupportingdata. AccordingtotheLogisticsIndustryHumanCapital
Index, over75%ofemployeesputinmorethanfivehoursofovertimeeachweek. The
annualvoluntaryturnoverrateforsomeentry-levelpositionsmightbeashighas40%[10].
Employeesatisfactionandturnoveraresignificantlycorrelatednegatively,accordingto
research[11]. Highturnoverhasobviousbusinessrepercussionsinthelogisticsindustry.
Inadditiontoincreasingtheincidenceofoperationalfailures, italsoraisesrecruitment
andtrainingcosts. Theindustry’salreadyslimprofitmarginsarefurthererodedbythese
combined consequences [12]. In contrast, after implementing an intelligent scheduling
system,anationalsupermarketchainreducedthetimespentonschedulingperemployee
from4hperweektojust15min. Customerwaittimesduringpeakhoursdecreasedby
40%,employeesatisfactionincreasedby32%,andmonthlylaborcostswerecutbyover
180,000yuan[13]. Thisdemonstratesthesignificantpotentialofscientificschedulingin
optimizingworkforcemanagement.
County-levellogisticscentersareunderintensepressurebecausetothefastexpansion
ofbusiness[14]andtheslowpaceofautomation. Thesefacilitieshavetodealwithavariety
ofpersonnelarrangementsandfrequentordervariations. Optimizingmanualscheduling
becomescrucialforimprovingoperationalefficiencyandreducinglaborexpensesinthis
environment. Workforce scheduling studies have changed dramatically in the modern
era. It now emphasizes a sophisticated decision-making process rather than static cost
optimization. Thisnewparadigmnecessitatessystematicbalancingofdifferentobjectives
and dynamic responses to uncertainty [15,16]. Using hierarchical modeling to manage
complexityisthefundamentalreasoningbehindthisstrategy. Advancedtechniqueslike
resilient optimization and stochastic programming are used to deal with resource and
demand uncertainty. At the same time, the range of optimization goals has expanded.
https://doi.org/10.3390/systems14030295

Systems2026,14,295 3of40
Insteadoffocusingoncostcontrolinisolation,itlooksforParetoimprovementsthatalso
improveoperationalefficiency[17,18].
Nevertheless, prior research has not given significant consideration to the unique
setting of county-level logistics centers. Numerous difficulties are introduced by the
particularoperationalsetting. Theseincludeskillgapsandtrainingrequirementsbrought
on by high employee turnover [9,10], unpredictability brought on by tidal swings in
order volume [19], and serious worries about cumulative exhaustion from physically
demandingjobs. Therefore,aschedulingsystemthatcandomulti-objectiveoptimization
is obviously needed. Practical limitations like skill disparities, training timetables, and
fatiguemanagementproceduresmustalsobeincorporatedintothisstructure.
Thegoalofthisprojectistocreateadual-objectiveschedulingoptimizationmodel
withafocusoncounty-levellogisticscenters. Inordertorepresentoperationalrealities
at the county level, the model strikes a balance between “cost control” and “employee
satisfaction”. Logisticscenterswouldbeabletomoreeffectivelyallocateworkerswith
varyingdegreesofefficiencyandrespondmoreflexiblytoordervolatilitywiththehelp
of such a model. Moreover, the approach aims to raise workers’ skill levels and job
satisfactionthroughthescientificdesignofworkdurations,shiftrotations,andtraining
mechanisms. Thisstrategymaintainscontroloverpersonnelexpenseswhilesupporting
thedualobjectivesofenhancingorganizationalstabilityandoperationalresilience.
Thefollowingresearchquestionsareputforthinthisstudy,whichfocusesonthelabor
schedulingoptimizationchallengeinlogisticswarehousingcenters:
• Howtoimplementrefinedhuman-centeredmanagementinscheduling?
• Howtoformulateaschedulingplanthataccuratelyrespondstouncertainlogisticsdemand?
• Howcantactical-levelschedulingincorporatestrategictrainingtocreateasynergy
betweendevelopmentandoperations?
Inconclusion,thisstudytacklesakeyissueincounty-levellogisticscenter:theconflict
betweenaheavyrelianceonlaborandquickcompanyexpansion. Itfocusesontheissueof
workerschedulingatlogisticsfacilitiesatthecountylevel. Theultimategoalistoimprove
both the operational efficiency and the employee’s satisfaction of county-level logistics
centersthroughahuman-centeredschedulingapproach.
Thestructureofthispaperisasfollows: Section2reviewstheliteratureonhuman-
centeredmanagementconcepts,workforceschedulingresearch,anduncertainplanning
methods;Section3discussesthedescriptionanduncertaintytheoryresearchonworkforce
schedulingissuesincounty-levellogisticscenters;Section4constructsadual-objectiveop-
timizationmodelaimingtominimizebothCostandemployeecomfortpenalties;Section5
designs improved Genetic Algorithm for solution; Section 6 analyzes the experimental
resultsandconductsasensitivityanalysis,andprovidesmanagementrecommendations;
finally,Section7summarizestheresearchfindingsandoffersdirectionalrecommendations
forfuturestudies.
2. LiteratureReview
Toaddresstheseresearchquestions,thefollowingliteraturereviewwillsystematically
examinethreeinterrelatedstreams: (1)theevolutionofhuman-centeredmanagementin
operations,(2)workforceschedulingmodelsunderuncertainty,and(3)theintegrationof
employeewell-beingintooptimizationframeworks.
2.1. TheRoleofHuman-CenteredManagementPhilosophyinCorporateOperations
WiththeriseofIndustry5.0,thefocusofmanufacturinghasshiftedfromtechnology-
centricapproachestoahuman-centeredvalueorientation. ThethreepillarsofIndustry
5.0areresilience,sustainability,andhuman-centereddesign[20]. Whilehuman-centered
https://doi.org/10.3390/systems14030295

Systems2026,14,295 4of40
managementstressesputtinghumanneeds,values,andwell-beingattheheartofbusiness
decision-making,traditionalmanagementtheorieshavemostlyconcentratedonefficiency
and profit maximization. According to Nasir et al. (2025) [20], Industry 5.0’s human-
centeredethosrepresentsasignificantdeparturefromIndustry4.0’stechnology-driven
paradigm. Throughtechnologyempowermentratherthanhumanreplacement,thisworld-
viewseekstofostersynergisticprogressbetweenhumansandrobots. Thesignificance
of“humanisticculture”forlong-termbusinessperformancewasoriginallysuggestedby
BlackandLaVenture(2015)[21], whoemphasizedthatmanagementshouldpayatten-
tiontothesocial,psychological,andphysiologicalrequirementsofemployees. Theterm
“human-centereddesign”wasfirstusedinmanagementdiscoursebyGiacomin(2014)[22],
whopromotedanethical,inclusivesystemthattakesintoaccountavarietyofstakeholders,
such as suppliers, customers, and employees. The “ethical business model,” put forth
bySpiller(2000)[23],emphasizesthatbusinessesshouldprioritizesocialresponsibility,
supplychainethics,andemployeewellbeinginadditiontopursuingfinancialgains. Ac-
cordingtoGhobakhlooetal. (2023)[24],technologyinterventionslikevirtualizationand
technicalsupportcanreduceemployees’physicalworkloadandincreasetheirinvolvement
indecision-making. TheuseofAIinhumanresourcemanagementisseenbyBlackand
vanEsch(2020)[25]andChen(2023)[26]asacrucialinstrumentforimprovingemployee
capabilitiesandsatisfaction.
2.2. WorkforceSchedulingResearch
Workforceschedulingisasignificanttopicinoperationsresearchandmanagement
science,aimingtodevelopefficient,equitable,andconstraint-compliantemployeework
schedulesfororganizations. Sincethe21stcentury,withadvancesincomputationalpower
andthedevelopmentofartificialintelligence,schedulingresearchhasgraduallyshifted
toward intelligent optimization and hybrid methods. Nasirian et al. (2024) [27] focus
onstrategic-levelmulti-skillhumanresourceallocation,employingtwo-stagestochastic
programmingandlogicalBendersdecompositiontoaddressdemanduncertainty,with
anemphasisonresolvingthelong-termdecisionof“whotohireandwhatskillstotrain.”
Cabreraetal. (2024)[28]delveintoreal-timeschedulingandpathplanningattheoper-
ationallevel, introducinganovel“stop-and-go”operationmode. Theyemployprecise
solutionsbasedonthebranch-and-boundpricingcuttingalgorithmandpulsealgorithm
tosimultaneouslydetermine“teamformation,taskallocation,andvehicle-Apedestrian
hybridpaths.”Huetal. (2024)[29]focusedonthedynamicschedulingproblemfornu-
cleicacidsamplingpersonnelduringthepandemic. Theyconstructedamulti-objective
robustoptimizationmodelanddesignedanimprovedNSGA-II-HCalgorithm,specifically
addressingdemanduncertaintyandmulti-rescue-pointcoordinationissues. ParkandKo
(2022) [30] developed a linear programming model incorporating absenteeism rates to
optimizelaborcostsinKorea’sconstructionindustryunderadjustedworkinghourpolicies
and irregular employee absences. They evaluated the stability of scheduling schemes
throughsimulation. Bocewiczetal. (2023)[31]investigatedthejobrotationscheduling
problemformulti-skilledemployees,employingaconstrainedprogrammingapproachto
maximizerobustnessagainstemployeeabsenceswhileensuringskillretention. Chenetal.
(2022)[32]focusedonmatchingemployeeskillproficiencywithproductioncycletimes
forpulsedassemblylines,employinganimprovedGeneticAlgorithmforoptimization.
Mystakidisetal. (2024)[33]addressedthecomplexissueofoncologynursingscheduling
byemployingintegerprogrammingtoachieveequitableandefficientresourceallocation.
https://doi.org/10.3390/systems14030295

Systems2026,14,295
5of40
2.3. UncertainProgrammingMethodandApplications
Inthefieldofoperationsmanagementandscheduling,demanduncertaintyisoneof
thecorechallenges. Toaddressthischallenge,scholarshavedevelopedvariousmodeling
andoptimizationapproaches. StochasticprogrammingwaspioneeredbyDantzig(1955)
andothers. LiuBaodengproposedthetheoryofuncertainty, establishinganaxiomatic
mathematicalsystemforhandlinguncertaintybasedoncredibilityratherthanfrequency.
Regardinghumanresourceschedulingchallenges,existingresearchhasproposedmultiple
approachestoaddressuncertainty. Wangetal. (2023)developedatwo-stagestochastic
programminganddata-drivendistributionrobustoptimizationmodeltotacklethedual
randomnessofdemandandservicedurationinhomecareservices[34]. Gongetal. (2025)
developedanefficientdecompositionalgorithmintheiroperatingroomschedulingstudy,
simultaneously accounting for the randomness of surgery duration and emergency de-
mand [35]. In retail workforce scheduling, Porto et al. (2025) constructed a two-stage
stochasticmodeltointegratemultiplelaborflexibilitystrategiesforexplicitlyhandling
demand fluctuations [36]. Bogataj et al. (2025) addressed the dual shortage of human
resourcesandhousingconstructioninlong-termcareservicesbyemployingfuzzyeval-
uationandtargetplanningfordynamicresourceallocation[37]. Regardingshiftdesign
undertask-orientedrequirements,Wuetal. (2023)proposedaprobabilisticmodelwith
constraintsandacorrespondingheuristicsolutionalgorithm[38].
Table1comparesthedifferencesbetweentheexistingliteratureandthispaper. The
existingliteratureonworkforceschedulinghasmadesignificantprogressintermsofmod-
elingtechniques,solutionalgorithms,andapplicationdomains. Butcurrentresearchin
logisticsschedulingrarelydeeplyintegratesuncertaindemand,human-centeredobjectives,
employeeheterogeneity. Meanwhile,existingschedulingmodelspredominantlyfocuson
sectorssuchashealthcare,aviation,andretail,lackingtargetedexplorationofthecomplex
scenariosinherentincounty-levellogisticsoperations. Moreover,despitethewidespread
acceptanceofthe“people-centered”philosophy,itlacksaquantifiableoperationalframe-
work. To this end, the study focuses on county-level logistics centers. By converting
uncertaindemandintoadeterministicequivalentformusingconfidencelevelsandinverse
uncertaintydistributions,andbydefining“employeecomfort”asaquantifiableobjective
thatcanbeco-optimizedwithcost. Itfillsaresearchgapincounty-levellogisticscenters
regardingcomplexschedulingandhuman-centeredobjectivequantificationmethods. This
gapmotivatesthedevelopmentofatailoredschedulingmodel, whichwillbeformally
definedinthenextsection.
Table1.LiteratureComparison.
|     |     |     | Employee | Uncertain |     |     |
| --- | --- | --- | -------- | --------- | --- | --- |
Refs. ModelObjective DecisionVariables ModelingMethod SolutionApproach
|     |     |     | Comfort | Demand |     |     |
| --- | --- | --- | ------- | ------ | --- | --- |
Logic-based
Recruitment
Benders
| Nasirianetal. |      | plan+Training |     | √   | Two-stagestochastic |                |
| ------------- | ---- | ------------- | --- | --- | ------------------- | -------------- |
|               | Cost |               | ×   |     |                     | decomposition+ |
| [27]          |      | plan+Employee |     |     | integerprogramming  |                |
Customized
schedulingplan
analyticalcutting
√
| Park&Ko |      | Employeescheduling |     | ×   |                   |       |
| ------- | ---- | ------------------ | --- | --- | ----------------- | ----- |
| [30]    | Cost | plan               |     |     | Linearprogramming | CPLEX |
Employeescheduling
Constraint
| Bocewicz  | Robustnessto    | plan+                 | √   |     |                     |                 |
| --------- | --------------- | --------------------- | --- | --- | ------------------- | --------------- |
|           |                 |                       |     | ×   | Declarativemodeling | programming(IBM |
| etal.[31] | employeeabsence | Substituteassignments |     |     |                     |                 |
ILOGCP)
incaseofabsence
|            |               |                    | √   |     |      | CPLEX+Java |
| ---------- | ------------- | ------------------ | --- | --- | ---- | ---------- |
| Mystakidis | Weightedshift | Employeescheduling |     |     |      |            |
|            |               |                    |     | ×   | MILP | (branchand |
| etal.[33]  | allocation    | plan               |     |     |      |            |
boundmethod)
https://doi.org/10.3390/systems14030295

Systems2026,14,295
6of40
Table1.Cont.
|     |     |     | Employee | Uncertain |     |     |
| --- | --- | --- | -------- | --------- | --- | --- |
Refs. ModelObjective DecisionVariables ModelingMethod SolutionApproach
|             |                   |                     | Comfort | Demand |                       |            |
| ----------- | ----------------- | ------------------- | ------- | ------ | --------------------- | ---------- |
|             | Servicedistance   |                     |         |        |                       | Improved   |
|             |                   | Rescuepointdispatch |         | √      | Multi-objectiverobust |            |
| Huetal.[29] | andshortageloss   |                     | ×       |        |                       | NSGA-II-HC |
|             |                   | plantosamplingpoint |         |        | optimizationmodel     |            |
|             | &Satisfactionrate |                     |         |        |                       | algorithm  |
√
| Chenetal.    | Maximum        |                      |     |     | Proficiency-based   | ImprovedGenetic   |
| ------------ | -------------- | -------------------- | --- | --- | ------------------- | ----------------- |
|              |                | Processexecutionplan |     | ×   |                     |                   |
| [32]         | completiontime |                      |     |     | SchedulingModel     | Algorithm         |
|              |                | Employeescheduling   |     |     | Arc-basedinteger    | Branch-and-price  |
| Cabreraetal. |                |                      | ×   | ×   |                     |                   |
| [28]         | Cost           | plan+Driving         |     |     | programmingmodels   | cuttingalgorithm+ |
|              |                | directions           |     |     | andpath-basedmodels | Pulsealgorithm    |
Employeescheduling √ √ Dualobjectiveuncertain ImprovedGenetic
| OurStudy | Cost&Comfort |                   |     |     |             |           |
| -------- | ------------ | ----------------- | --- | --- | ----------- | --------- |
|          |              | plan+Trainingplan |     |     | programming | Algorithm |
3. ProblemStatement
Asordervolumesrapidlygrowwithincounty-levellogisticscenters,aheavyreliance
on manual labor has made workforce scheduling a core operational challenge. Order
pickersandfork-liftworkers,whoseskilllevelsandproductivityvarygreatly,makeupthe
diverseworkforceemployedbythesefacilities. Optimizingstaffshiftassignmentsacrossa
weeklyplanninghorizonisthemaingoalofthisschedulingproblem. Thereareseveral
timeperiodsineachday. Themaindifficultyisstrikingabalancebetweentwocompeting
goals: increasingemployeesatisfactionandreducingoperatingexpenses. Dailyvariations
indemandareoneoftheproblem’smainfeatures. Additionally,itrequirestheincorpo-
rationofhuman-centeredconsiderations. Thesefactorsincludetrainingneeds,personal
preferences for relaxation, and making sure that employees’ workloads are distributed
fairly. Theresearchtopic,theschedulingcycle,andthedistributionoftimeslotsarethe
maincomponentsoftheissue. Thefollowingsubsectionswillelaborateoneachlevelin
detailaccordingtothestructureshowninFigure1.
3.1. ResearchSubject
This subsection elaborates on the “Decision Variables and Constraints” layer in
Figure1.Inthissection,weprimarilyoutlinetheclassschedulesandtrainingarrangements;
otherconstraintswillbeformallydefinedinSection4.
Order Pickers. During the receiving process, order pickers deal with loose items.
Based on their efficiency, these workers are divided into two different subsets: high-
efficiencypickersandlow-efficiencypickers. Superiorproductivityisexhibitedbypickers
withhighefficiency. Asaresult,theyareusuallygivenshiftsduringtimesofhighdemand.
Toavoidundueweariness,theirshiftsmustbecarefullyplanned. Low-efficiencypickers
havelowerproductivityandrequireregularskill-enhancementtrainingduringoff-peak
hours. Trainingismandatoryandmustnotconflictwithworkshifts.
ForkliftOperators. Forkliftoperatorsareresponsibleforhandlingfullpalletship-
mentsduringthereceivingprocess. Itisassumedtheypossessuniformefficiency,meaning
|     |     | allarehighlyefficient. Forkliftoperatorsdonotparticipateintraining. |     |     |     |     |
| --- | --- | ------------------------------------------------------------------- | --- | --- | --- | --- |
3.2. ShiftSchedulingCycleandTimeSlotAllocation
Thissectioncorrespondstothetime-relatedelementsandcoreconstraintswithinthe
“BackgroundandProblemStatement”layerofFigure1.
The scheduling plan is formulated on a weekly basis. The daily work schedule is
divided into six consecutive shifts, each lasting two hours, covering the period from
8:00a.m. to8:00p.m. Theperiodfrom4:00p.m. to6:00p.m. isdesignatedasthepeak
hours. Thereceivingwindowisdividedintomorningandafternoonsessions. Themorning
receivingwindowopensat8:00a.m. Alllooseitemsandpalletizedshipmentsreceived
during this period must be processed by 2:00 p.m. Therefore, sufficient staff must be
https://doi.org/10.3390/systems14030295

Systems2026,14,295 7of40
allocatedthroughoutthemorningandlunchperiodstohandlethetotalvolumeofmorning
deliveries. Afternoon window restocking hours are from 2:00 p.m. to 8:00 p.m. Tasks
generatedduringthisperiodmustbecompletedby8:00p.m. thesameday. Afternoon
demand fluctuates across three time periods, with peak demand occurring during the
highestdemandperiod. Low-efficiencyemployeesrequiredtoattendeachtrainingsession
mustcompleteexactlyU sessionsperweek,andtrainingperiodsmustnotoverlapwith
min
workshifts. Trainingperiodsarescheduledduringpredefinedoff-peakhours.
Figure1.ProblemStatement.
Themodelseekstominimizeaweightedtotalofnormalizedcostsandcomfortpenal-
ties, as shown in the “Objectives to Achieve” layer in Figure 1. Both base salaries and
hourly pay are included in the model’s cost component. Employee satisfaction encom-
passesmultipledimensions. Toquantifytheimpactofschedulingdecisionsonemployee
well-being, this paper defines the “Comfort Penalty” metric as an inverse measure of
employeesatisfaction. Thispenaltytakesintoconsiderationanumberofcriteria,including
inconsistent shift assignments, deviations from desired rest intervals, and violations of
continuousworkhourrestrictions. Therefore,minimizingthecomfortpenaltycontributes
toenhancingoverallemployeesatisfactionwithworkschedules.
Tosumup,thisstudytacklesadual-objective,multi-constraintoptimizationissue.
AnimprovedGeneticAlgorithmisemployedtolocatesolutions. Thisstrategyseeksto
achieveabalancebetweenoperationaleffectivenessandhuman-centeredmanagement
principles. Theultimateobjectiveistoencouragesustainablegrowthatlogisticscentersat
thecountylevel.
https://doi.org/10.3390/systems14030295

Systems2026,14,295
8of40
4. ModelConstruction
4.1. ModelAssumptions
Toconstructthemathematicalmodel,thefollowingcoreassumptionsareproposed:
• Assumption 1. Forklift operations and picking are separate jobs. Operational ef-
ficiency is a known constant that is unaffected by working hours, tiredness levels,
orlearningeffects,andeachemployeeisgivenasinglejobtypeeveryshift. While
forkliftoperatorsmaintainconstantefficiency,pickersareclassifiedashigh-efficiency
orlow-efficiencybasedonperformance.
• Assumption2. Theschedulingcycleisoneweek. Dailyworkinghoursaredivided
intoequal-lengthperiods. Employeestatusiscategorizedonlyas“working”or“non-
working,”disregardingtaskinterruptionsorpauseswithinperiods. Dailyperiods
andtheirattributes(e.g.,peakvs. off-peakperiods)arepredefinedandfixed.
• Assumption 3. Training targets only low-performing pickers to enhance their op-
erational skills, scheduled during predefined off-peak periods. Employees do not
participateinactualtasksduringtraining,andthenumberoftrainingsessionsmust
meetminimumrequirements.
• Assumption4. Eachemployee’spreferenceforvacationdaysvariesindividuallyand
remainsrelativelystablethroughouttheschedulingcycle.
•
Assumption5.Supportingresourcessuchasequipment,facilities,andinformationsys-
temsaresufficientlyavailableanddonotconstitutebottlenecksforworkforcescheduling.
4.2. SymbolsandParameters
ThesymbolsystemusedinthemodelisshowninTable2.
Table2.SymbolLegend.
| Set | Definition |     |
| --- | ---------- | --- |
E ThesetofStaff,e∈E,Includingorderpickersandforkliftoperators
E ThesetofOrderPickers,Ep⊆E,{P1,P2,P3,P4,P5,P6,P7,P8,P9}
p
E ThesetofHigh-Efficiencyorderpickers,{P1,P2,P3,P4,P5,P6,P7}
ph
| E   | ThesetofInefficientorderpickers,{P8,P9} |     |
| --- | --------------------------------------- | --- |
pl
E ThesetofForkliftOperators,Ef ⊆E,{F1,F2,F3,F4,F5,F6,F7,F8,F9}
f
ThesetofTimeIntervals,t∈T,Eachsegmentlasts2h,From8:00a.m.
T
to8:00p.m.,Atotalof6timeslots
| T   | ThesetofPeakhours: | 4:00p.m. to6:00p.m. |
| --- | ------------------ | ------------------- |
peak
| T train    | Thesetoftrainingsessions,duringoff-peakhours. |     |
| ---------- | --------------------------------------------- | --- |
| D          | ThesetofDate,d∈D,7daysaweek                   |     |
| Parameters | Definition                                    |     |
| C e        | Employeee’sunittimecost(CNY)                  |     |
| L          | Maximumdailyworkinghours                      |     |
max
L
| cont | Maximumcontinuousoperatingtime |     |
| ---- | ------------------------------ | --- |
| L    | Minimumweeklyworkinghours      |     |
min
α CostWeightingFactor
| β                                                     | ComfortWeightingFactor |     |
| ----------------------------------------------------- | ---------------------- | --- |
| δ Maximumpermissiblevariationinweeklyworkinghours     |                        |     |
| γ Bufferdaysforlightshiftsfollowinghigh-intensitywork |                        |     |
H max Maximumnumberofpeak-periodworkdaysallowedwithinaweek
| U   | Numberoftrainingsessionsperweek |     |
| --- | ------------------------------- | --- |
min
Totalcostwhenallemployeesworkmaximumhourswithout
C max
consideringcomfort(theoreticalmaximum)
https://doi.org/10.3390/systems14030295

Systems2026,14,295
9of40
Table2.Cont.
Penaltyvalueundertheworst-casecomfortscenario,suchasall
P employeesWorking8consecutivehoursdaily,dailyshiftchanges,and
max
allrestpreferencesbeingviolated(theoreticalmaximum)
| W   |     | Employeeweeklytotalworkinghours |     |     |     |
| --- | --- | ------------------------------- | --- | --- | --- |
e
| H e | Numberofpeak-periodworkdaysperemployeewithinoneweek |     |     |     |     |
| --- | --------------------------------------------------- | --- | --- | --- | --- |
Totalnumberoflooseitemsrequiringhandlingbypickersformorning
I
| pick1 |     |     | deliveries(unit) |     |     |
| ----- | --- | --- | ---------------- | --- | --- |
Totalnumberoflooseitemsrequiringhandlingbypickersfor
I
| pick2 |     |     | afternoonrestocking(unit) |     |     |
| ----- | --- | --- | ------------------------- | --- | --- |
Numberoffullpalletshipmentsrequiringforkliftoperatorstohandle
I
| tank1 |     |     | duringmorningrestocking(pallet) |     |     |
| ----- | --- | --- | ------------------------------- | --- | --- |
Numberoffullpalletshipmentsrequiringforkliftoperatorstohandle
I tank2
duringafternoonrestocking(pallet)
I Afternoonpickingdemanddistributionbytimeslot: [x1,x2,x1]pieces
pick2t
Afternoonforkliftdemanddistributionbytimeslot: [x3,x4,x3]
I
| tank2t |     |     | palletizedcargotasks |     |     |
| ------ | --- | --- | -------------------- | --- | --- |
Numberoflooseitemsprocessedperhourbypickers(unit/h)
p e
|     |     | P1–P7: | P items/hour,P8–P9: | P items/hour |     |
| --- | --- | ------ | ------------------- | ------------ | --- |
|     |     |        | 1                   | 2            |     |
Numberoffullpallettaskshandledperhourbyforkliftoperators
f
e
(pallet/h)
| p   | Numberoflooseitemshandledbyhigh-efficiencypickers(unit) |     |     |     |     |
| --- | ------------------------------------------------------- | --- | --- | --- | --- |
high
p
| low |     | Numberoflooseitemshandledbyinefficientpickers(unit) |     |     |     |
| --- | --- | --------------------------------------------------- | --- | --- | --- |
Numberofpalletizedcargohandlingtaskscompletedby
f
| high |     | high-efficiencyforkliftoperators(pallet) |     |     |     |
| ---- | --- | ---------------------------------------- | --- | --- | --- |
∆
Thedurationofeachtimeslotis2h.
| pref |     | Employeee’spreferenceintensityforrestondated |     |     |     |
| ---- | --- | -------------------------------------------- | --- | --- | --- |
e,d~
|     | EmployeeE’sweeklybasesalary: |     |     | Picker: B1CNY/weekForklift |     |
| --- | ---------------------------- | --- | --- | -------------------------- | --- |
B e
|     |     |     | operator: | B2CNY/week |     |
| --- | --- | --- | --------- | ---------- | --- |
T Morningprocessingwindowaftergoodsarrival: 8:00a.m. to2:00p.m.
window1
Afternoonprocessingwindowfollowinginventoryreplenishment:
T
| window2 |     |     | 2:00p.m.                | to8:00p.m. |     |
| ------- | --- | --- | ----------------------- | ---------- | --- |
| R       |     |     | Numberofrestdaysperweek |            |     |
min
| L   |     | Maximumworkinghoursforlight-dutyshifts |     |     |     |
| --- | --- | -------------------------------------- | --- | --- | --- |
relax
| Relax |     | Employeeewasscheduledforaneasyshiftondated |     |     |     |
| ----- | --- | ------------------------------------------ | --- | --- | --- |
e,d
| HighIntensity | e,d | Employeee’shigh-intensityworkondated |     |     |     |
| ------------- | --- | ------------------------------------ | --- | --- | --- |
longest_cont Thelongestcontinuousworkinghoursforemployeeeondated
e,d
| κ   |     |     | Demandvolatilitycoefficient |     |     |
| --- | --- | --- | --------------------------- | --- | --- |
| τ   |     |     | Confidencelevel             |     |     |
Decision
Definition
Variables
| x   |     | Employeeeworkedondatedduringperiodt(0–1variable) |     |     |     |
| --- | --- | ------------------------------------------------ | --- | --- | --- |
e,t,d
| y   |     | Employeeeisoffondated(0–1variable) |     |     |     |
| --- | --- | ---------------------------------- | --- | --- | --- |
e,d
Employeeeattimeperiodtdatedwhethertrainingwasreceived(0–1
u
| e,t,d |     | variable,onlyforunderperformingemployees) |     |     |     |
| ----- | --- | ----------------------------------------- | --- | --- | --- |
4.3. ModelObjectivesandConstraints
4.3.1. ObjectiveFunctionAnalysis
Themodelpursuestwomutuallybalancingobjectives.
| (1)Objective1: | MinimizeTotalOperatingCosts |     |     |     |     |
| -------------- | --------------------------- | --- | --- | --- | --- |
Thetotalcostconsistsofafixedweeklybasesalaryandvariablepaybasedonactual
hoursworked,ascanbeseeninFunction(1).
|     |     | ∑     | ∑ ∑       | ∑ ·∆·x    |     |
| --- | --- | ----- | --------- | --------- | --- |
|     |     | Cost= | B e +     | c e e,t,d | (1) |
|     |     | e∈E   | e∈Et∈Td∈D |           |     |
https://doi.org/10.3390/systems14030295

Systems2026,14,295
10of40
| (2)Objective2: |     |     | MinimizeTotalComfortPenalty |     |     |     |     |     |     |     |
| -------------- | --- | --- | --------------------------- | --- | --- | --- | --- | --- | --- | --- |
Comfortpenaltyquantifiesthenegativeimpactofschedulingonemployees’work
experience,including:
Continuous Work Penalty (P ): Penalizes exceeding the daily continuous work
cont
durationthreshold.
PenaltyforScheduleChanges(P ): Penalizesfrequentchangesinworkpatterns
shift
betweenadjacentworkdays.
RestPreferencePenalty(P ): Penalizesfailuretoaccommodateemployees’prefer-
pref
encesforrestonspecificdates.
ThiscanbeseeninFunction(2).
|     |     |     | Comfortpenalty= |     | P    | +P  | +P    |      |     | (2) |
| --- | --- | --- | --------------- | --- | ---- | --- | ----- | ---- | --- | --- |
|     |     |     |                 |     | cont |     | shift | pref |     |     |
6
| Amongthese,P |     |      | = ∑ ∑ max(0,longestcont |     |     | −L  | ),P  | = ∑ ∑     | ∑ |x −x | |,      |
| ------------ | --- | ---- | ----------------------- | --- | --- | --- | ---- | --------- | ------- | ------- |
|              |     | cont |                         |     |     | e,d | cont | shift     | e,t,d   | e,t,d−1 |
|              |     |      | e∈Ed∈D                  |     |     |     |      | e∈Ed=1s∈S |         |         |
| P =          | ∑ ∑ | pref | ·(1−y ).                |     |     |     |      |           |         |         |
| pref         |     | e,d  | e,d                     |     |     |     |      |           |         |         |
e∈Ed∈D
(3)ComprehensiveObjectiveFunction
Theweightedsummethodisemployed,normalizedusingthetheoreticalmaximum
values C max and P max to eliminate dimensional effects and enable managers to express
differingpreferencesforcostandcomfortthroughtheweightsαandβ,ascanbeseenin
Function(3).
|     |     |           |      | (cid:18) | Cost | Comfortpenalty |     | (cid:19) |     |     |
| --- | --- | --------- | ---- | -------- | ---- | -------------- | --- | -------- | --- | --- |
|     |     |           | =min | α·       |      | +β·            |     |          |     |     |
|     |     | MinimizeZ |      |          |      |                |     |          |     | (3) |
|     |     |           |      |          | C    |                | P   |          |     |     |
|     |     |           |      |          | max  |                | max |          |     |     |
4.3.2. ModelConstraints
(1)HumanResourceCoverageConstraints
MorningShiftStaffingCoverage. Foreachdated,thetotalprocessingcapacityofall
employeesduringthemorningshift(8:00a.m. to12:00p.m.) mustbesufficienttohandleat
leastthetotalnumberofitemsreceivedduringthemorningdelivery. WhereP e denotesthe
numberofitemsprocessedperhourbypickere,f denotesthenumberoftaskscompleted
e
perhourbyforkliftoperator,I representsthetotalnumberofloosegoodsreceivedin
pick1
representsthetotalnumberoffullpalletsreceivedinthemorning,∆
themorning,I
tank2
denotesthetimeperiodlength,andx e,t,d indicateswhethertheemployeeisworking,as
canbeseeninFunctions(4)and(5).
|     |     |     | (cid:32) |     |       | (cid:33) |       |     |     |     |
| --- | --- | --- | -------- | --- | ----- | -------- | ----- | --- | --- | --- |
|     |     |     | ∑        | ∑   | ∆·x   |          |       |     |     |     |
|     |     |     | p ·      |     |       | ≥        | I ∀d  | ∈ D |     | (4) |
|     |     |     | e        |     | e,t,d |          | pick1 |     |     |     |
|     |     |     | e∈Ep t∈T |     |       |          |       |     |     |     |
window1
|     |     |     | (cid:32) |     |       | (cid:33) |       |     |     |     |
| --- | --- | --- | -------- | --- | ----- | -------- | ----- | --- | --- | --- |
|     |     |     | ∑        | ∑   | ∆·x   |          |       |     |     |     |
|     |     |     | f e ·    |     |       | ≥        | I ∀d  | ∈ D |     | (5) |
|     |     |     |          |     | e,t,d |          | tank1 |     |     |     |
|     |     |     | e∈Ef t∈T |     |       |          |       |     |     |     |
window1
Afternoon Shift Staffing Coverage. For each date d and each time slot t between
2:00p.m. and8:00p.m.,thetotalprocessingcapacityofallpickersmustatleastmeetthe
pickingdemandI forthattimeslot. Afternoondemanddistributioncorrespondsto
pick2t
three timeperiods. Constraintsensurethat goodsareprocessed promptly duringeach
afternoonperiod,ascanbeseeninFunctions(6)and(7).
∑
|     |     |     | p ·∆·x  | ≥ I    | ∀d  | ∈ D, | T∈T |         |     | (6) |
| --- | --- | --- | ------- | ------ | --- | ---- | --- | ------- | --- | --- |
|     |     |     | e e,t,d | pick2t |     |      |     | window2 |     |     |
e∈Ep
∑
|     |     |     | f ·∆·x  | ≥ I    | ∀d  | ∈ D, | T∈T |         |     | (7) |
| --- | --- | --- | ------- | ------ | --- | ---- | --- | ------- | --- | --- |
|     |     |     | e e,t,d | tank2t |     |      |     | window2 |     |     |
e∈Ef
https://doi.org/10.3390/systems14030295

Systems2026,14,295
11of40
(2)On-the-jobConstraints
Foreachtimeslottanddated,atleastonepickerisonduty. Thisconstraintprevents
unattendedtimeslots,ascanbeseeninFunctions(8)and(9).
|     |     | ∑   |         | ≥1  |     |     |
| --- | --- | --- | ------- | --- | --- | --- |
|     |     |     | x e,t,d |     |     | (8) |
e∈Ep
∑
|     |     |     | x   | ≥1  |     | (9) |
| --- | --- | --- | --- | --- | --- | --- |
e,t,d
e∈Ef
(3)TrainingConstraints
WeeklyTrainingRequirements. EachinefficientpickermustreceiveexactlyU min
trainingsessionsperweek. Trainingisconductedonlyduringoff-peakhoursT ,and
train
thesesessionscannotoverlapwiththeirworkingshifts. Theconstraintensurestherequired
numberoftrainingsessionsismet,ascanbeseeninFunction(10).
|     | ∑   | ∑   |       |     |     |      |
| --- | --- | --- | ----- | --- | --- | ---- |
|     |     | u   | =U    | ∀e  | ∈ E | (10) |
|     |     |     | e,t,d | min | pl  |      |
d∈Dt∈Ttrain
WorkduringTrainingPeriods. Employeescannotworkduringtrainingperiods. That
is, x = 0. Restrictions ensure employees do not participate in work during training,
e,t,d
therebyavoidingconflicts,ascanbeseeninFunction(11).
| x     | =0∀e | ∈   | E ∪E | ,t ∈ T | ,d ∈ D | (11) |
| ----- | ---- | --- | ---- | ------ | ------ | ---- |
| e,t,d |      |     | pl   | fl     | train  |      |
TrainingDurationRestrictions. Eachemployeemayreceivetrainingnomorethan
once per day, meaning a maximum of one training session. This restriction prevents
trainingfrombecomingoverlyconcentratedandinterferingwithwork,ascanbeseenin
Function(12).
|     | ∑   | ≤1∀e  | ∈   | ∪E   | ∈       |      |
| --- | --- | ----- | --- | ---- | ------- | ---- |
|     | u   | e,t,d |     | E pl | fl ,d D | (12) |
t∈T
(4)TimeConstraints
DailyWorkingHoursLimit. Thetotalworkinghoursforemployeesondatedmust
notexceedthemaximumdailyworkinghoursL max ,ascanbeseeninFunction(13).
| ∑   |         | ≤     | ·(1−y | )∀e | ∈ ∈   |      |
| --- | ------- | ----- | ----- | --- | ----- | ---- |
|     | x e,t,d | L max |       | e,d | E,d D | (13) |
t∈T
Weekly Rest Requirements. y indicates whether an employee is on rest. M is a
e,d
sufficiently large constant to ensure that when y = 1, the working hours must be 0.
e,d
EachemployeemusthaveatleastR min daysofrestperweek. Thisconstraintsafeguards
employees’basicrestrights,ascanbeseeninFunctions(14)and(15).
| ∑   |         | ≤ M·(1−y |     | )∀e ∈ | ∈     |      |
| --- | ------- | -------- | --- | ----- | ----- | ---- |
|     | x e,t,d |          |     | e,d   | E,d D | (14) |
t∈T
∑
|     |     | y   | ≥ R | ∀e ∈ | E   | (15) |
| --- | --- | --- | --- | ---- | --- | ---- |
|     |     | e,d | min |      |     |      |
d∈D
ContinuousOperationLimit. Employeesshallnotworkcontinuouslyformorethan
L hoursduringtheirworkperiod. Thisconstraintpreventsexcessivecontinuouswork
cont
hoursandreducesfatigue,ascanbeseeninFunction(16).
t+L ∑cont/2
|     | x   | ≤     | L ∀e | ∈ E,t | ∈ T,d ∈ D | (16) |
| --- | --- | ----- | ---- | ----- | --------- | ---- |
|     |     | e,k,d | cont |       |           |      |
k=t
https://doi.org/10.3390/systems14030295

Systems2026,14,295
12of40
Minimum Working Hours Requirement. Each employee’s total weekly working
hours must be at least L min hours. This constraint ensures employees have sufficient
workload,ascanbeseeninFunction(17).
|     |     |     |     |     |     |     |     | ∑ ∑ | ∆·x   | ≥     | ∀e ∈ |     |      |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | ----- | ----- | ---- | --- | ---- |
|     |     |     |     |     |     |     |     |     | e,t,d | L min | E    |     | (17) |
t∈Td∈D
(5)EquilibriumConstraints
WeeklyTotalEngineeringTimeVariance. Calculatetheweeklytotalworkinghours
We for each employee, where the difference between the longest and shortest working
hoursmustnotexceedδhours. Thisconstraintensuresafairdistributionofworkload,as
canbeseeninFunction(18).
∑ ∑
|     |     |     |     |     |     |     | W = | 2·x | ,W    | −W  | ≤   | δ∀e ∈ E | (18) |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | ----- | --- | --- | ------- | ---- |
|     |     |     |     |     |     |     | e   |     | e,t,d | max | min |         |      |
d∈Dt∈T
FairnessinWorkAssignments. Eachemployee’sworktimesmaynotexceedH max
timesduringpeakhours(4:00p.m. to6:00p.m.) withinaweek. Thisconstraintprevents
certainemployeesfrombeingoverburdenedwithhigh-intensitywork,ascanbeseenin
Function(19).
|     |     |     |     |     |     |     |       | ∑ ∑ |     |         |          |     |      |
| --- | --- | --- | --- | --- | --- | --- | ----- | --- | --- | ------- | -------- | --- | ---- |
|     |     |     |     |     |     |     | H e = |     | x   | , H e ≤ | H max ∀e | ∈ E | (19) |
e,t,d
d∈Dt∈T
peak
(6)High-intensityworkconstraints
DefinitionofHigh-IntensityWork. Definewhetheranemployeeperformedhigh-
intensity work on date d. If an employee works during peak hours, or works for more
than 4 consecutive hours, or works for more than 8 h in total, then HighIntensity is 1.
e,d
Restrictionshelpidentifyhigh-intensityworkdaysforschedulinglightershiftsafterward.
Avalueof4indicatesthemaximumcontinuousoperatingtimeL cont =4h;8indicatesthe
maximumtotaldailyoperatingtimeL max =8h; Misalargeconstant,ascanbeseenin
Function(20).
|     |     |     |    |     |     |          |             |     |          |    | ∑ x    | ·∆−8 |     |
| --- | --- | --- | --- | --- | --- | -------- | ----------- | --- | -------- | --- | ------ | ------ | --- |
|     |     |     |     |     |     | (cid:18) |             |     | (cid:19) |     | e,t ,d |        |     |
|     |     |     |     | ∑   |     |          | longest ont | −4  |          |     | t∈T    |        |     |
HighIntensity =min1, x +max 0, c e,d +max0, ∀e ∈ E,d ∈ D (20)
|     |     | e,d |     |     | e,t,d |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | ----- | --- | --- | --- | --- | --- | --- | --- | --- |
|     |     |     |     |     |       |     | M   |     |     |     | M   |     |     |
t∈T pack
DefinitionofEasySchedule. Definewhetheranemployeeisscheduledforaneasy
shiftondated. Ifanemployeedoesnotworkduringpeakhoursandtheircontinuous
workingtimedoesnotexceed4h,thenRelax is1. Avalueof4indicatesthemaximum
e,d
continuousoperatingtimelimitL cont =4h;6indicatesthemaximumoperatingtimefor
lightdutyshifts6h;Misalargeconstant,ascanbeseeninFunction(21).
|       |      |       |      |     |         |          |             |     |          |    | ∑ x ·∆−6 |         |      |
| ----- | ---- | ------ | ----- | --- | ------- | -------- | ----------- | --- | -------- | --- | --------- | --------- | ---- |
|       |      |        |       |     |         | (cid:18) | longest ont | −4  | (cid:19) |     | e,t ,d    |           |      |
|       | =min |        | 0,1− |     | ∑       | −max     | c           | e,d | −max     |     | t∈ T      | ∀e∈E,d∈D | (21) |
| Relax | e,d  | 1,max |       |     | x e,t,d |          | 0,          |     |          | 0, |           |         |      |
|       |      |        |       |     |         |          | M           |     |          |     | M         |           |      |
t∈Tpeak
4.4. ModelConversion
ThissectionemploystheuncertaintytheoryproposedbyLiu[39]formodeltransfor-
mation;therelevanttheoreticalknowledgeandproofsaresummarizedinAppendixB.
|     |     |     |     | 4.4.1. | ModelingUncertainRequirements |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | ------ | ----------------------------- | --- | --- | --- | --- | --- | --- | --- | --- |
(1)DemandUncertaintyIndicates
Inthisstudy,wetreatorderpickingandforkliftoperationsduringeachdailytime
periodasmutuallyindependentlinearuncertainvariables,ascanbeseeninFormula(22).
https://doi.org/10.3390/systems14030295

Systems2026,14,295
13of40
|     |     |     | pick | ∼ L(dlow,d |     | high), ξfork | ∼   | L(dlow,d | high) |     |      |
| --- | --- | --- | ---- | ---------- | --- | ------------ | --- | -------- | ----- | --- | ---- |
|     |     |     | ξ    |            |     |              |     |          |       |     | (22) |
|     |     |     | t    |            | t   | t            | t   | t        | t     |     |      |
high
wheredlow = dbase × (1 − δ), d = dbase × (1 + δ),withdbase representingthebase
|     | t   | t   |     |     | t   | t   |     |     | t   |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
demandfortheperiodandδdenotingthedemandvolatility.
(2)ParameterDeterminationandConfidenceLevel
Basedonhistoricaldataorexperience,wedeterminethebaselinedemandforeach
timeperiod. Wesettheconfidencelevelτ=0.9toensurethattheschedulingplanmeets
demandin90%cases.
Byapplyinginverseuncertaintydistribution,uncertaindemandcanbeconvertedinto
adefinitevalue,asshowninFormula(23).
|     |     |     |                |     | (cid:108) | (cid:109) (cid:108) |                |     | (cid:109) |     |     |
| --- | --- | --- | -------------- | --- | --------- | ------------------- | -------------- | --- | --------- | --- | --- |
|     |     |     | ddeterministic | =   | Φ−1(τ)    | =                   | (1−τ)·dlow+τ·d |     | high      |     |     |
(23)
|     |     |     | t   |     | t   |     |     | t   | t   |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
4.4.2. UncertainPlanningModelConstruction
Workforceschedulingproblemsarefundamentallydual-objectiveoptimizationprob-
lemsrequiringabalancebetweentwoconflictinggoals.Tosimplifythesolution,weemploy
theweightedsummethodtotransformthedualobjectivesintoasingleobjective.Bysetting
weightcoefficientsα, β > 0suchthatα + β = 1,thecompositeobjectivefunctionis
expressedasshowninFormula(24).
minα·Cost(x,ξdeterministic)+β·Comfortpenalty(x)
(24)
Inanuncertainenvironment,economiccostsaredirectlyrelatedtoworkforceworking
hours,whilelabordemandisinfluencedbytheuncertaindemandξ. Theeconomiccost
functionisshowninFormula(25).
|     |     |     | Cost(x,ξdeterministic) |     |     | = ∑ | + ∑       | ∑ ∑ | ·∆·x      |     |      |
| --- | --- | --- | ---------------------- | --- | --- | --- | --------- | --- | --------- | --- | ---- |
|     |     |     |                        |     |     | B e |           |     | C e e,t,d |     | (25) |
|     |     |     |                        |     |     | e∈E | e∈Et∈Td∈D |     |           |     |      |
Toensurethatdemandissatisfiedatconfidencelevelα ,anopportunityconstraintis
k
introduced,asshowninFormula(26).
|     |      |      |       |     |      |       |       |       |        |          |        |
| --- | ----- | ---- | ----- | ---- | ---- | ------ | ----- | ----- | ------- | -------- | ------ |
|     |      |      |       |     |      |       |       |       |        |          |        |
|     | ∑     | ·∆·x |       | pick |      | ∑ ·∆·x |       | ξfork |         |          |        |
| M   |       | p    | ≥     | ξ ≥  | τ, M | f      |       | ≥     | ≥ τ, ∀t | ∈ T, d ∈ | D (26) |
|     |       | e    | e,t,d | t    |      | e      | e,t,d | t     |         |          |        |
|     | e∈Ep |      |       |     |      | e∈Ef  |       |       |        |          |        |
Atthesametime,workforcecoverageconstraintsmustalsobeconsidered,asshown
inFormula(27).
|     |     |      |         |    |        |          |          |          |            |       |      |
| --- | --- | ----- | ------- | --- | ------ | -------- | -------- | -------- | ---------- | ----- | ---- |
|     |     |       |         |     |        | (cid:40) |          | (cid:41) |            |       |      |
|     |     |      |         |    |        |          |          |          |            |       |      |
|     |     |       | ∑       |     |        | ∑        |          |          |            |       |      |
|     |     | M     | x e,t,d | ≥1  | ≥ τ, M | x        | e,t,d ≥1 | ≥        | τ, ∀t ∈ T, | d ∈ D | (27) |
|     |     | e∈Ep |         |    |        | e∈E      |          |          |            |       |      |
f
Insummary,theuncertainschedulingmodelcanbeexpressedasFormula(28).
https://doi.org/10.3390/systems14030295

Systems2026,14,295
14of40
|     |                         |       | (cid:0)          |     | (cid:1) |                    |     |     |     |     |
| --- | ------------------------ | ----- | ---------------- | --- | ------- | ------------------ | --- | --- | --- | --- |
|     | minλ                     | ·Cost | x,ξdeterministic |     | +λ      | ·Comfortpenalty(x) |     |     |     |     |
|     |  | 1     |                  |     | 2       |                    |     |     |     |     |
s.t.
|     |     | (cid:40) |         |           | (cid:41) |     |     |     |           |     |
| --- | --- | -------- | ------- | --------- | -------- | --- | --- | --- | --------- | --- |
|     | M   | ∑        | p · ∆ · | x ≥       | ≥        |     |     | ∀ t | ∈ T d ∈ D |     |
|     |     |          | e       | e , t , d | ξ t τ ,  |     |     |     | ,         |     |
∈
|     |     | e E      | p       |           |          |     |     |     |            |     |
| --- | --- | -------- | ------- | --------- | -------- | --- | --- | --- | ---------- | --- |
|     |     | (cid:40) |         |           | (cid:41) |     |     |     |            |     |
|     | M   | ∑        | f · ∆ · | x ≥       | ≥        |     |     | ∀ t | ∈ T ,d ∈ D |     |
|     |     |          | e       | e , t , d | ξ t τ ,  |     |     |     |            |     |
∈
|     |                            | e E      | f           |          |     |     |     |     |              |      |
| --- | -------------------------- | -------- | ----------- | -------- | --- | --- | --- | --- | ------------ | ---- |
|     |                            | (cid:40) |             | (cid:41) |     |     |     |     |              | (28) |
|     |  M | ∑        |             | ≥ ≥      |     |     |     | ∀   | ∈ T ∈        |      |
|     |                            |          | x e , t , d | 1        | τ , |     |     | t   | , d D        |      |
|     |                            | e ∈ E    | p           |          |     |     |     |     |              |      |
|     |                            | (cid:40) |             | (cid:41) |     |     |     |     |              |      |
|     | M                          | ∑        |             | ≥ ≥      |     |     |     | ∀   | ∈ T ∈        |      |
|     |                            |          | x e , t , d | 1        | τ , |     |     | t   | , d D        |      |
|     |                            | e ∈ E    | f           |          |     |     |     |     |              |      |
|     | M                          | {g ( x   | , ξ ) ≤     | 0} ≥ α   | ,   |     |     | k   | = 1, . .. ,m |      |
|     |                            | k        |             |          | k   |     |     |     |              |      |
x ∈ X
Amongthese,g representsotherresourcesandinstitutionalconstraints,α denotesthe
|     |     |     | k   |     |     |     |     |     | k   |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
confidencelevelforeachconstraint,andXdenotesthefeasibleregionfordecisionvariables.
AccordingtoLiu’suncertaintytheory[39], iftheobjectivefunctionandconstraint
functionsaremonotonicwithrespecttotheuncertainvariablesandtheuncertainvariables
are mutually independent, the aforementioned uncertain programming model can be
equivalentlytransformedintoadeterministicprogrammingmodel.
In our workforce scheduling context, we argue that the primary constraints (e.g.,
Formulas(12)–(15))satisfythemonotonicitycondition. Specifically,astheuncertainde-
mand(cid:101)I increases,therequiredtotalprocessingcapacity∑ P ·∆·x mustbenon-
|     | pick1 |     |     |     |     |     | e∈Ep | e   | e,t,d |     |
| --- | ----- | --- | --- | --- | --- | --- | ---- | --- | ----- | --- |
decreasingtomaintainfeasibility. Thisimpliesthattheconstraintfunctionismonotone
increasing with respect to the demand variable. Similarly, the cost objective function
(Formula(9)) is linear and additive, thus monotonic in the number of working hours,
whichisindirectlydeterminedbydemand.
Basedonthislogicalverificationofmonotonicity,andassumingmutualindependence
ofdemandvariablesacrossdifferentperiods,theuncertainmodelcanbetransformedinto
itsdeterministicequivalent. ThetransformeddeterministicmodelisshowninFormula(29).

|     |     |                          |           | (cid:0) ,ξd | et er m i n is tic (cid:1) | +λ          | (x) |     |     |     |
| --- | --- | ------------------------ | --------- | ----------- | -------------------------- | ----------- | --- | --- | --- | --- |
|     |     |  m i | n λ 1 C e | c o n x     |                            | 2 C comfort |     |     |     |     |
x
|     |     | s . t | .       |           |               |     |     |         |       |     |
| --- | --- | ----- | ------- | --------- | ------------- | --- | --- | ------- | ----- | --- |
|     |     | ∑     | ∆       |           | Φ − 1         |     |     |         |       |     |
|     |     |       | p e ·   | · x ≥     | ( τ ) ,       |     | ∀   | t ∈ T , | d ∈ D |     |
|     |     |       |         | e , t , d | t             |     |     |         |       |     |
|     |     | e ∈ E | p       |           |               |     |     |         |       |     |
|     |     | ∑     | f · ∆ · | x ≥       | Φ − 1 ( τ ) , |     | ∀   | t ∈ T , | d ∈ D |     |
|     |     |       | e       | e , t , d | t             |     |     |         |       |     |
e∈Ef
(29)
|     |     |  ∑ | x   | ≥ 1 , |     |     | ∀   | t ∈ T , | d ∈ D |     |
| --- | --- | ---------------------- | --- | ----- | --- | --- | --- | ------- | ----- | --- |
e , t , d
|     |     | e ∈ E |     |     |     |     |     |     |     |     |
| --- | --- | ----- | --- | --- | --- | --- | --- | --- | --- | --- |
p
|     |     | ∑   | x   | ≥ 1 , |     |     | ∀   | t ∈ T , | d ∈ D |     |
| --- | --- | --- | --- | ----- | --- | --- | --- | ------- | ----- | --- |
e , t , d
∈
|     |     | e E | f       |     |     |     |     |        |         |     |
| --- | --- | --- | ------- | --- | --- | --- | --- | ------ | ------- | --- |
|     |     | g   | ( x ) ≤ | 0 , |     |     |     | k = 1, | . .. ,m |     |
k
|       |                 | x ∈ | X        |             |     |         |                      |     |        |        |
| ----- | --------------- | --- | -------- | ----------- | --- | ------- | -------------------- | --- | ------ | ------ |
|       |                 |     | (Φ−1(τ), | Φ−1(τ),..., |     | Φ−1(τ)) |                      |     |        |        |
| where | ξdeterministic= |     |          |             |     |         | is the deterministic |     | demand | vector |
|       |                 |     | 1        |             | 2   | n       |                      |     |        |        |
for each time period, and g (x) ≤ 0 represents the other constraints converted to
k
deterministicform.
Given the NP-hard nature of this problem and the complexity of its constraints,
an exact solution method is impractical. Therefore, an improved Genetic Algorithm is
developedinthenextsectiontoefficientlysolvethemodel.
https://doi.org/10.3390/systems14030295

Systems2026,14,295 15of40
5. AlgorithmDesign
5.1. AlgorithmFramework
Workforceschedulingatcounty-levellogisticscentersisaclassiccombinatorialopti-
mizationproblem,characterizedbylargescale,multipleconstraints. Thesolutionspace
expands exponentially with increases in staff count, scheduling cycle length, and time
slot granularity. This growth, coupled with diverse and complex human resource and
operationalconstraints, renderstheproblemNP-hard. Traditionalexactsolutionmeth-
odsoftenproveimpracticalforsuchlarge-scalereal-worldproblemsduetoprohibitive
computationaltime.
GeneticAlgorithms,meta-heuristicsinspiredbynaturalselectionandgenetics,are
widelyappliedtoproblemslikeworkforceschedulingandjobdispatching. Thesetech-
niquesprovideanumberofdesirablebenefits. Theyshowgreatglobalsearchcapabilities
andminimalrelianceonproblem-specificstructures. Additionally,theyareideallysuited
forparallelprocessingandcanreadilyhandlecomplicatedrestrictions. Wheninvestigating
discrete,high-dimensionalsolutionspaces,thepopulation-basedevolutionarytechnique
worksverywell. Furthermore, itnaturallyintegratesavarietyofgoalsandlimitations
throughthefitnessfunction’sdesign.
Inordertosolvethedevelopeddual-objectiveschedulingmodel,thisresearchsuggests
animprovedgeneticmethod. Thecreationofeffectiveheuristicinitializationprocessesand
specialistrepairoperatorsareimportantadvancements. Bothelementsareadaptedtothe
particularlimitationsoftheissue,speedingupconvergencewhilepreservingtheviability
andqualityofthesolution.
ThegeneralmethodadherestoaGeneticAlgorithm’stypicalevolutionaryarchitecture.
Nevertheless,importantimprovementshavebeenmadetotheevolutionaryprocedures,
constraint-handlingsystems,andstartupphase. Theseadjustmentsdealwiththeparticular
difficultiesthatthisschedulingissuepresents. Theprimaryalgorithmflowisshownin
Figure2;moreinformationisgivenbelow. Forthepseudo-codeoftheGeneticAlgorithm,
seeTableA1inAppendixA.
Figure2.FlowchartoftheimprovedGeneticAlgorithm.
https://doi.org/10.3390/systems14030295

Systems2026,14,295 16of40
First,asomewhatlargestartingpopulationiscreatedusingaheuristicapproach. This
significantly speeds up the search by injecting high-quality genetic material. A fitness
functionwithdynamicpenaltytermsisusedtoassesseachgeneration’sindividualfitness.
Superior parent persons are then chosen through a tournament selection process. To
encouragecomprehensiveexplorationofthesolutionspace,thenexecutebitwisemutation
withalowerprobabilityandtwo-pointcrossoveroperationswithagreaterlikelihood.After
eachgeneticsurgery,anumberoftargetedrepairactivitiesareimmediatelytriggered,which
isthemainimprovement. Byquicklyresolvinganyconstraintviolations,theseremedies
guaranteechildren’ssurvival.Thealgorithmusesanappropriatelylargemaximumnumber
of generations and has an elite retention strategy. The final schedule is determined by
selectingthebestsolutionfoundacrossfivedifferentruns,whichincreasesthestabilityand
robustnessoftheresult.
5.2. EncodingandInitialization
Theencodingmethodusedisbinary,asshowninFigure3. Eachchromosomeencodes
acompleteweeklyshiftschedule. Thechromosomelengthis|E|·|D|·|T|. Eachgene
position, denotedasgene , correspondstoabinarydecisionvariablex . Avalue
(e,d,t) {e,t,d}
of1indicatesthatemployeeeworksduringtimeslottondated,while0indicatesthey
do not work. Training arrangements for inefficient pickers are recorded in a separate
list, ‘employee_training_slots’, and are not directly encoded in the chromosome. ‘em-
ployee_training_slots’isadictionarywherekeysrepresentinefficientpickerIDsandvalues
arethesetoftrainingslotsscheduledforthatemployeewithinaweek.Eachslotisuniquely
identifiedbyitsdateandtimeindex. Nonetheless,thesetrainingsessionsaresynchronized
duringdecodingandrepair.
Figure3.Encoding.
Toimproveinitialpopulationqualityandavoidthemanyinfeasiblesolutionstypical
ofpurelyrandominitialization,aheuristicproceduregenerateseachinitialindividual.First,
basedonoperationalneeds,prioritizeassigninghighlyefficientemployeestoensurethat
baselinestaffingrequirementsaremetduringallshifts.Meanwhile,pre-randomlyschedule
aspecifiednumberoftrainingsessionsforinefficientpickersandlocktheircorresponding
genepositionsonthechromosome. Finally,alightweightrepairfunctioncorrectsobvious
constraintviolationsinthegeneratedschedule. Thisstrategyyieldsaninitialpopulation
balancingdiversityandfeasibility,providingasolidfoundationforsubsequentevolution.
Pseudo-codeforAlgorithmInitializationSeeAppendixA,TableA2.
5.3. FitnessFunction
Thefitnessvalueofanindividualdirectlycorrespondstothevalueoftheobjective
functionZ.SinceGeneticAlgorithmstypicallyhandleminimizationproblems,asmaller
fitnessvalueindicatesabetterindividual.
https://doi.org/10.3390/systems14030295

Systems2026,14,295 17of40
Constraint handling employs a strategy combining the dynamic penalty function
method with a feasible solution priority rule. The fitness calculation can be seen as
Formulation(30).
∑
Fitness= Z+λ· w·V (30)
i i
i
Here,V representsthedegreeofviolationforconstraintclassi,w denotesthepenalty
i i
weightforthatconstraintclass,andλisacoefficientthatdynamicallyincreaseswiththe
evolutionarygenerationnumbertoimposestricterpenaltiesoninfeasiblesolutionsduring
laterevolutionarystages.
5.4. GeneticManipulationandRepairMechanisms
Thealgorithm’sgeneticoperatorsareselection,crossover,andmutation. Ineachselec-
tionevent,kindividualsarerandomlychosenfromthepopulation. Thefittestamongthese
entersthematingpool. Thecrossoveroperatorappliestwo-pointcrossover. Twocrossover
pointsarerandomlyselected. Thegenesegmentsbetweenthesepointsarethenexchanged
betweentwoparentstoproducetwooffspring. Formutation,acustombitwisemutation
schemeisused. Thisschemeflipsarandomlychosengenewithagivenprobability. To
minimizedisruption,therepairprocessisinitiatedimmediatelyaftermutation.
Aftercrossoverandmutation,offspringmayoccasionallyviolatecertainconstraints.
Repairfunctionsareusedtopromptlycorrecttheseissues. Thishelpsensurethatevery
solutionremainsvalid. Thesefunctionsruninsequenceandmayrepeatasneededuntilall
requirementsaresatisfied. Thespecificstepsincludethefollowing.
(1)TrainingConstraintRepairOperator: Adjustthefrequencyandschedulingoftrain-
ingsessionsforinefficientpickers,ensuringthattheweeklytrainingfrequencyprecisely
meetsU andoccursduringoff-peakhours.
min
(2)PeakWorkFrequencyRepairOperator: Randomlyremovesexcesspeak-period
workassignmentstolimitanemployee’sweeklypeak-periodworkfrequencytowithinH .
max
(3)TheRestDayConstraintRepairOperator: Ensuresweeklyrestdaysarenofewer
thanR .
min
(4)High-IntensityShiftRecoveryOperator: Forhigh-intensityworkdays,automati-
callyassignalight-dutyshiftthefollowingday.
(5) Minimum Working Hours Guarantee Operator: Randomly assign work to idle
periodsuntiltheemployee’sweeklytotalworkinghoursreachH .
min
(6)ContinuousWorkRepairOperator: Ensuresdailycontinuousworkdurationdoes
notexceedL byinterruptingcontinuousworksequences.
cont
(7) Uniqueness Guarantee Operator: Normalizes gene valuesto preventduplicate
schedulingofthesameemployeeduringthesametimeperiod.
From the algorithm flow described above, the time complexity of the proposed al-
gorithmmainlydependsonthepopulationsizeN,themaximumnumberofgenerations
G, and the decoding and fitness evaluation process of each individual. Since each in-
dividual corresponds to a three-dimensional binary matrix, fitness evaluation requires
traversing all time units and checking various constraints, resulting in a time complex-
ity of O( | E | · | D | · | T |). Therefore, the overall time complexity of the algorithm is
O(G·N·|E|·|D|·|T|).
6. CaseStudy
6.1. ExperimentalDataandParameterSettings
6.1.1. ExperimentalData
Theexperimentaldatainthisstudyoriginatefromtheactualoperationsofacounty-
level logistics center. These data are augmented with statistical figures from relevant
https://doi.org/10.3390/systems14030295

Systems2026,14,295 18of40
researchreportsandreasonableassumptions. Allparametersaremaintainedataconstant
baselineleveltoguaranteescientificrigorandexperimentalcomparability.
TheChinaFederationofLogistics&PurchasingandJD.comjointlyproducealogistics
indexfromwhichdemanddataisderived. Logisticsoperationalfeaturesatthecounty
levelareusedtoestablishfoundationaldemandparameters. Actualpaylevelsincounty
regionsareusedtocalculatelaborexpenses. varyingemploymentclassificationsaresubject
tovaryingsalaryrules.
Thefollowingessentialtraitsareincludedinthedata:
Ordervolumesexhibitnotablevariationswithrespecttothedistributionofordertime.
Deliveryperiodsinthemorningandafternooncoincidewithtwoprocessingpeaks. The
dailydemandpeakisbetween4:00and6:00p.m. A“high–medium–high”patternisused
todescribethedistributionofafternoondemand. Thismimicsthewave-likefeaturesseen
inreal-worldoperations.
Intermsofthenumberandmakeupoftheworkforce,thecenterhaseighteenemploy-
ees. Thisworkforcecomprises9orderpickers(7high-efficiencyand2low-efficiency)and
9ForkliftOperators,allofwhomarehigh-efficiency. Employeeefficiencyvariesconsid-
erably. High-efficiencyorderpickersprocess180itemsperhour,whereaslow-efficiency
orderpickershandle120itemsperhour. Eachemployeehastheirownpreferreddayoff.
Employees’preferencesforrestdaysaredetailedinTableA3ofAppendixC.
Toreflecttheinherentuncertaintyincounty-levellogisticsorders,baselinedemand
issettofluctuatewithinapercentagerangearoundareferencevalue. Thisvariabilityis
subsequentlyconvertedintoadeterministicvalueataspecifiedconfidencelevel,applying
uncertaintytheory. TheexperimentalbaselinedataareshowninTable3. Theexperiments
wereconductedonacomputerwithanIntelCorei7-12700Hprocessor(IntelCorporation,
Santa Clara, CA, USA), 32 GB of memory, and the Windows 11 operating system. The
algorithmwasimplementedinPython3.9anddevelopedusingtheDEAPframework(see
FigureA1inAppendixA).
Table3.ExperimentalBaselineData.
Parameter Parameter
ReferenceValue Note
Category Name
Numberofhigh-efficiencypickers(efficiency
E 7
ph p =180pieces/h)
e
Numberoflow-efficiencypickers(efficiency
Staffing E 2
pl p =120pieces/h,requiretraining)
e
Numberofforkliftoperators(efficiency
E 9
f f =40pallets/h)
e
Baseweeklysalary: 1000yuanforpickers,1500yuan
Be 1000/1500yuan/week
forforkliftoperators
CostParameters
Hourlywage: 20yuanforpickers,30yuanfor
Ce 20/30yuan/h
forkliftoperators
Totalinboundloosegoodsvolumeduringmorning
I 1300pieces
pick1 window(8:00–14:00)
Inboundloosegoodsvolumeforeachafternoontime
Requirement I pick2t [600,800,600]pieces slot(14:00–16:00,16:00–18:00,18:00–20:00)
Parameters
Totalinboundfullpalletvolumeduringmorning
I 320pallets
task1 window(8:00–14:00)
I [150,200,150]pallets Inboundfullpalletvolumeforeachafternoontimeslot
task2t
https://doi.org/10.3390/systems14030295

Systems2026,14,295
19of40
Table3.Cont.
| Parameter | Parameter |     |     |
| --------- | --------- | --- | --- |
ReferenceValue Note
| Category | Name |     |                          |
| -------- | ---- | --- | ------------------------ |
|          | L    | 8h  | Maximumdailyworkinghours |
max
|     | L cont | 4h   | Maximumcontinuousoperatingtime |
| --- | ------ | ---- | ------------------------------ |
|     | R      | 1day | Minimumweeklyrestdays          |
min
|     | H   | 24h | Minimumweeklyworkinghours |
| --- | --- | --- | ------------------------- |
min
Maximumpermissiblevariationinweeklyworking
|             | δ     | 6h                                        |                     |
| ----------- | ----- | ----------------------------------------- | ------------------- |
| Operational |       |                                           | hoursamongemployees |
| Constraints |       | Maximumnumberofpeak-periodworkdaysallowed |                     |
|             | H max | 3days                                     |                     |
withinaweek
Bufferdaysrequiringalightshiftfollowinga
|     | γ   | 1day |     |
| --- | --- | ---- | --- |
high-intensityworkday
Numberoftrainingsessionsperweekfor
|     | U   | 2sessions |     |
| --- | --- | --------- | --- |
min
low-efficiencypickers
Basedonthepreferencesobservedinthesurveyedreal-worldenterprises,wesetthe
weightstoα=0.7andβ=0.3. Differentcompanieshavedifferentpreferences,andthe
modelcanbeconfiguredwithweightsbasedonthecompany’sactualcircumstances.
6.1.2. AlgorithmParameterSettings
TheparametersettingsfortheimprovedGeneticAlgorithmweredeterminedwith
referencetotheparameterselectionapproachesusedbyWangetal.[40]andJiangetal.[41].
Thesesettingsweresubsequentlyfine-tunedbasedontheactualoperationalperformance
inthecasestudytoachieveoptimalschedulingoutcomes. Theoptimalparametersare
summarizedinTable4. ComfortpenaltysettingsareshowninTable5.
Fieldinterviewswithmanagersandfrontlinestaffatcounty-levellogisticscenters
revealedthatcontinuousworkistheprimarysourceoffatigue. Thereisadose–response
linkbetweenextendedworkinghoursandhealthdeficits,accordingtoempiricaldatafrom
the literature. Further, it has been demonstrated that prolonged work results in worse
performancethenextday. Theseresultsinformthemodel’sdesign,whichpenalizesongo-
ingworkmoreseverely. Thisstrategyplacesahighpriorityonreducingthecumulative
consequencesofweariness[42–45].
Furthermore,tovalidatethemodel’seffectivenessacrossdifferentscenarios,weestab-
lishedmultipleweightcombinationsforcomparativeanalysis. Theresultsarepresentedin
Figure4.
Table4.ParametersettingsfortheimprovedGeneticAlgorithm.
Parameter
|     | ParameterName | Value | BasisandExplanationforSettings |
| --- | ------------- | ----- | ------------------------------ |
Symbol
Balancingsearchbreadthandcomputationalefficiency. A
scalethatistoosmallmayleadtopremature
| N   | Populationsize | 500 |     |
| --- | -------------- | --- | --- |
convergence,whileonethatistoolargemayresultin
slowconvergence.
MaximumEvolutionary Ensurethealgorithmhassufficientiterationstoconverge
| G   |            | 300 |                    |
| --- | ---------- | --- | ------------------ |
|     | Generation |     | toastablesolution. |
Ahigherprobabilityofpromotingthecombinationand
| P c | Cross-probability | 0.85 |     |
| --- | ----------------- | ---- | --- |
disseminationofsuperiorgenesegments.
Alowerprobabilityismaintainedtopreservepopulation
| P m | Probabilityofmutation | 0.05 |     |
| --- | --------------------- | ---- | --- |
diversityandavoiddisruptingvaluablegenetictraits.
https://doi.org/10.3390/systems14030295

Systems2026,14,295
20of40
Table4.Cont.
Parameter
|     | ParameterName |     | Value | BasisandExplanationforSettings |
| --- | ------------- | --- | ----- | ------------------------------ |
Symbol
Retainthemostsuperiorindividualsfromeach
| E   | NumberofEliteRetained |     | 10  |     |
| --- | --------------------- | --- | --- | --- |
generationtopreventthelossofvaluablegenetictraits.
Balancingindividualselectionpressureswiththe
| k TournamentSelectionScale |     |     | 3   |     |
| -------------------------- | --- | --- | --- | --- |
preservationofdiversity.
Thedynamicpenaltyfunctionλ=λ ×(1+gen/G)
0
InitialDynamic initiallypermitsslightinfeasibilitytoexpandthesearch
| λ   |     |     | 100 |     |
| --- | --- | --- | --- | --- |
0
PenaltyCoefficient space,thenstrengthensthepenaltytoforceconvergence
towardthefeasibleregion.
Table5.ComfortPenaltyInternalWeightingCoefficient.
| PenaltyItems |     | Symbol | WeightValue | ReasonforSetting |
| ------------ | --- | ------ | ----------- | ---------------- |
Continuousovertimeworksignificantlyimpacts
| ContinuousWorkPenalty |     | ω   | 10                                               |     |
| --------------------- | --- | --- | ------------------------------------------------ | --- |
|                       |     | c   | fatiguelevels,resultinginhigherpenaltiesperunit. |     |
| Penaltyfor            |     |     | Thebaselinepenaltyisoneunitofinconveniencefor    |     |
|                       |     | ω s | 1                                                |     |
ScheduleChanges eachshiftchange.
Individualrequirementsarerespectedwhenpreference
| RestPreferencePenalty |     | ω p | 1   |     |
| --------------------- | --- | --- | --- | --- |
intensityvaluesaredirectlyusedaspunishments.
Figure4.ComparativeAnalysisofDifferentWeightings.
It can be seen that under different weighting combinations, the total cost and the
overalltargetvalueexhibitdifferences. Thisalsoreflectsthatwhileenterprisesconsider
different comfort preferences, they simultaneously impact both the total cost and the
targetvalue.
|     | 6.1.3. | AlgorithmPerformanceComparison |     |     |
| --- | ------ | ------------------------------ | --- | --- |
TovalidatetheeffectivenessoftheimprovedGeneticAlgorithm,thisstudyconducted
comparativeexperimentswiththetraditionalGeneticAlgorithmandParticleSwarmOpti-
mizationAlgorithm. TheresultsareshowninTable6. TheimprovedGeneticAlgorithm
https://doi.org/10.3390/systems14030295

Systems2026,14,295 21of40
demonstratedthebest performanceacross metrics includingaverageoptimalobjective
value, computational time, and convergence iterations. This demonstrates that the im-
provedstrategysignificantlyenhancesthealgorithm’ssolutionqualityandefficiencyunder
limitedcomputationalresources.
Table6.AlgorithmComparisonAcross10IndependentRuns.
Algorithm AverageOptimalTargetValue CPUTime(s) ConvergenceGen
TraditionalGA 0.48305774 168 296.4
PSO 0.47287577 1743 861.8
ImprovedGA
0.46324206 159 293
(OurAlgorithm)
6.2. OverallResultAnalysis
ToverifythepracticalityandreliabilityoftheproposedGAenhancements,thissection
performs a systematic validation focusing on two aspects: algorithm performance and
constraintsatisfaction. AlltestsutilizethebenchmarkparametersdefinedinSection6.1.
We employed a Bernoulli repeated experiment approach, running the improved
geneticalgorithmindependently20times. Figure5displaysthedistributionofoptimal
fitnessvaluesfromgeneration0togeneration300. Theboxwidthsteadilynarrowsasthe
generationsgoon,andthemedianandmeanofthegreatestfitnessvaluesoftendecline.
Thisimpliesthatthealgorithmretainspopulationvarietyandhasrobustglobalsearch
capabilitiesintheearlystages,allowingittorapidlyconvergetowardtheidealarea. Later
on,itmovesintoamorefocusedsearchphase. Themethodbecomesclosertoconvergence,
thesolutiondistributiongetsmoreconcentrated,anditsstabilitygreatlyincreases. The
qualityofthesolutionstaysexcellentevenasthepaceofconvergenceslowsdownlater.
Allthingsconsidered,thissuggeststhatthealgorithmstrikesahealthybalancebetween
localexploitationandworldwideexploration.
All formal restrictions are satisfied by the final timetable. A single run takes 159 s
ofCPUtime. Thisdemonstratesthatthealgorithm’scomputationalcostisacceptablefor
practicalapplications. Workloadsarebalancedandresourcesaredistributedlogically.
Figure5.Boxplotdistributionoftheoptimalfitnessvalueover300generations.
Thesuggestedstrategyproducesnotablegainsincost,comfort,andoverallobjective
valueascomparedtoconventionalschedulingtechniques. Thus,itgivescounty-levellogis-
https://doi.org/10.3390/systems14030295

Systems2026,14,295 22of40
ticscentersascientificdecision-supporttool. Theidealtimetableisfurtherdemonstrated
bytheheatmapsinFigures6and7. (a)displaystheoverallschedule,whichshowsthe
generalshiftarrangementsforallorderpickersorforkliftoperators, while(b)presents
individualschedules,detailingeachemployee’sspecificshiftassignments. Theyverifythe
rationaleandbalanceoftheschedulebyofferingavisualdepictionofshiftdistributions
foreachorderpickerandforkliftoperator.
Figure6.OrderPickers’Schedule.
Anintelligentschedulingsystemwassuccessfullycreatedandverifiedinthisstudy.
Thesystemcombinesamulti-objectiveevolutionaryalgorithmwithuncertaintytheory.
Thetechnologyproducesexcellentschedulingsolutionsindynamic,simulatedbusiness
contexts. Thesesolutionsprioritizehuman-centeredexperienceandareeconomical,com-
pliant,anddependable. Thefindingsshowthatthisapproachaccomplishesmulti-objective
optimizationinintricateconstraintnetworkswhilealsosuccessfullyaddressingdemand
uncertainty. Theapproacheffectivelystrikesacompromisebetweenhuman-centeredcom-
fort and cost objectives. It has great potential for wider use and strong practical value.
Table 7 summarizes the results of the investigation. Individual workload and comfort
penaltymetricsforeachemployeearelistedinTableA4ofAppendixC.
Thecoststructureisstillinbalance. Forkliftoperatorsareresponsibleforabout60%
oftotalcost. Thispercentageisinlinewiththeirhigherhourlysalaries, themakeupof
theworkforcetoday,andthetypeofjobtheyaregiven. Meanwhile,evenwhenadjusting
toerraticvariationsindemand,theschedulingsystemmaintainstotalexpenseswithina
reasonablerange.
Overallcomfortpenaltiesarekepttoaminimum. Thisshowsthatanumberofele-
ments,suchasconsecutiveworkinghours,dailyshiftvariances,andindividualpreferences
forrestdays,areproperlytakenintoconsiderationbytheschedulingplan.
Weconductedacomparativeanalysistovalidatethemodel’seffectivenessundera
benchmark requirement of two to three times the baseline, specifically for a workforce
https://doi.org/10.3390/systems14030295

Systems2026,14,295
23of40
sizeof30to50employees. Theresults,asshowninTable8,demonstratethatourmodel
maintainsacertaindegreeofapplicabilityacrossdifferentscalingrequirements.
Figure7.ForkliftOperators’Schedule.
Table7.SummaryofExperimentalResults.
|     |     | IndicatorCategory |     |                                  | SpecificIndicators      |     |     | NumericalValue |     |
| --- | --- | ----------------- | --- | -------------------------------- | ----------------------- | --- | --- | -------------- | --- |
|     |     |                   |     |                                  | TotalWorkingHours(h)    |     |     | 462            |     |
|     |     | WorkTimeAnalysis  |     | TotalWorkingHoursforPickers(h)   |                         |     |     | 230            |     |
|     |     |                   |     | TotalForkliftOperatorHours(h)    |                         |     |     | 232            |     |
|     |     |                   |     |                                  | TotalCostofPickers(CNY) |     |     | 13,600         |     |
|     |     | CostAnalysis      |     | TotalCostofForkliftOperator(CNY) |                         |     |     | 20,460         |     |
|     |     |                   |     |                                  | TotalCost(CNY)          |     |     | 34,060         |     |
|     |     |                   |     |                                  | PickerComfortPenalty    |     |     | 125            |     |
|     |     | ComfortAnalysis   |     | ForkliftOperatorComfortPenalty   |                         |     |     | 159            |     |
|     |     |                   |     |                                  | OverallComfortPenalty   |     |     | 284            |     |
|     |     | OverallAnalysis   |     |                                  | Targetvalue             |     |     | 0.4681         |     |
Table8.Solutionresultsondifferentscenarios.
|        |         | Numberof | Numberof  |           |     |         |         |        |        |
| ------ | ------- | -------- | --------- | --------- | --- | ------- | ------- | ------ | ------ |
|        | Number  | Experi-  | Inexperi- | Numberof  |     |         | Total   |        |        |
|        |         |          |           |           |     | Working |         | Total  | Target |
| Demand | ofEm-   | enced    | enced     | Forklift  |     |         | Comfort |        |        |
|        |         |          |           |           |     | Hours   |         | Cost   | Value  |
|        | ployees | Order    | Order     | Operators |     |         | Penalty |        |        |
|        |         | Pickers  | Pickers   |           |     |         |         |        |        |
| Double | 30      | 12       | 3         |           | 15  | 838     | 505     | 58,500 | 0.4828 |
|        | 50      | 19       | 6         |           | 25  | 1240    | 836     | 93,520 | 0.4656 |
demand
Threetimes
|     | 50  | 19  | 6   |     | 25  | 1290 | 878 | 94,680 | 0.4742 |
| --- | --- | --- | --- | --- | --- | ---- | --- | ------ | ------ |
demand
https://doi.org/10.3390/systems14030295

Systems2026,14,295 24of40
6.3. SensitivityAnalysis
6.3.1. UncertaintyParameter
Atwo-dimensionalparametricanalysisgridwasbuiltinordertoassesstheimpactof
demanduncertaintyonschedulingperformance. Thisgridexaminesthecombinedimpacts
on total cost and total comfort penalty of the confidence level (ranging from 0.5 to 1.0)
andthedemandfluctuationcoefficient(rangingfrom0.1to0.5). Figures8and9present
thefindings.
Figure8.ImpactofDemandVolatilityCoefficientandConfidenceLevelonCosts.
Figure9.TheEffectofDemandVariabilityCoefficientandConfidenceLevelonComfortPenalty.
AsshowninFigure8,totalcostarecomparativelylowwhendemandvariationsfall
between0.1and0.3andtheconfidencelevelislessthan0.6.Costincreaseisverymildwhen
confidencevariesbetween0.7and0.9. However,totalcostsincreasedramaticallywhen
demandvolatilitysurpasses0.4andgreaterconfidencelevels(beyond0.9)areneeded.
As shown in Figure 9, when both the demand fluctuation coefficient and the con-
fidence level are low, the overall comfort penalty remains mild. Minor adjustments to
theseparametersdonotcausesignificantfluctuationsinthecomfortpenalty. Astheconfi-
https://doi.org/10.3390/systems14030295

Systems2026,14,295 25of40
dencelevelincreasesfrom0.7to0.9,theoverallcomfortpenaltydecreases. Yet,oncethe
confidencelevelexceedsthe0.9threshold,theoverallcomfortpenaltyincreasessharply.
6.3.2. StaffingStrategy
Staffing plays a key role in shaping the operational performance of county-level
logisticscenters. Thisstudyexaminestwodimensions: thenumberofexperiencedorder
pickers and the overall workforce composition. The goal is to determine what type of
staffingstrategyisbestsuitedtodifferentoperationalcontexts.
(1)VariationsintheQuantityofExperiencedOrderPickers
Theexperimentassessedhowvaryingthenumberofpickersbetween4and11in-
fluenced both comfort penalties and operational costs. The corresponding results are
presentedinFigure10.
Figure10.TheEffectofDemandVariabilityConfidenceLevelonComfortPenalty.
Whenthenumberofskilledpickersincreasedfrom4to6, thecomfortpenaltyde-
creased significantly from 331 to 239. However, when the number of skilled pickers
decreasedto4,itcouldnotmeetthepickingdemand. Asthenumberofpickersincreased
from6to12,thelossincomfortgraduallyrecoveredto341. Furthermore,costscontinued
toriseasthenumberofskilledpickersincreased.
(2)ChangesinOrderPickersTypeStructure
The experiment investigates the impact of different combinations of experienced
and inexperienced pickers on total cost and total comfort penalty. The horizontal axis
representsthenumberofexperiencedpickers,whiletheverticalaxisrepresentsthenumber
ofinexperiencedpickers(0–9),asshowninFigure11.
In the chart, the horizontal coordinate “E0” represents zero skilled pickers, while
“I0”representszerounskilledpickers. Thepoint(S0,I0)indicatesthatbothskilledand
unskilledpickersareabsent. Therefore,boththecostandcomfortpenaltyatthispointare
zero. Experimentaldataindicatesthatwhenthetotalnumberofpickersfallsbelowsix,no
adjustmenttotheratioofskilledtounskilledworkerscanmeetproductiondemands.
https://doi.org/10.3390/systems14030295

Systems2026,14,295 26of40
Figure11.ImpactofEmployeeStructureonTotalCostsandComfortPenalties.
AsshowninFigure11a,totalcostsexhibitaconsistentupwardtrendasthenumber
of pickers increases. As shown in Figure 11b, when the number of skilled pickers or
unskilled pickers is low, the fluctuation range of employee comfort penalties increases
significantly. Asthenumberofpickersincreases,thecomfortpenaltygraduallystabilizes
andremainsatalow-to-moderatelevel. Itisworthnotingthatthecomfortpenaltiesfor
thethreepoints(E0,I1),(E1,I0),and(E2,I0)areclosetozero. Thisbenefitresultsfrom
fewerstaffbeinginvolved,whichmakesiteasiertoaccommodateemployeepreferences
andmaintainschedulingcontinuity. However,comfortpenaltiesincreasedramaticallyat
sites(E3,I1)and(E2,I3). Thisisbecauseitischallengingtofosterproductiveteamwork
insuchaworkforcestructure,whichcanthenresultinseriousworkloadimbalancesand
otheroperationalproblems.
6.3.3. ComparisonandEvaluationofSchedulingStrategies
Tocomprehensivelyevaluatetheperformancedifferencesamongvariousscheduling
strategies, this study proposes three core scheduling strategies based on the baseline
approach. Thesestrategiesweresubsequentlycombinedinpairsandinthreesimultaneous
combinations,ultimatelyyieldingeightdistinctschedulingschemes. Theproposalswere
quantitativelyevaluatedusingfourmetrics: cost,comfortpenalty,overallobjectives,and
workinghours. Toallowforcomparison,weappliedinversenormalizationtoallmetrics.
Each original value x was transformed into a normalized value x’ using the formula
x′ = (max− x)/(max−min),wheremaxandminarethemaximumandminimumvalues
forthatmetric. Afterthistransformation,ahigherx’indicatesbetterperformance. The
normalizedresultsarepresentedinaradarchart,asshowninFigure12.
Thefollowingwillelaborateonthedefinitionsofthethreeproposedstrategies:
(1)BalancedRotation
TheBalancedRotationaimstosupportworkers’work–lifebalance. Itsfundamental
ideaistoprovidesufficientsleepandavoidburnoutbyrequiringrestdaysandallocating
workhoursinasensiblemanner. Thispolicyrequiresatleasttwonon-consecutivedaysoff
perweekforeachemployee. Italsolimitsaveragedailyworkinghoursonweekdaystosix
hours. Evenifanemployeeispermittedtoworkeighthoursonagivenday,theaverage
dailyworkinghoursfortheweekmustbekeptbelowsixhours. Akeyruleisthatrestdays
cannotbeconsecutive. Thispreventsemployeesfromworkingintensiveextendedperiods
rightafteralongbreak.
https://doi.org/10.3390/systems14030295

Systems2026,14,295 27of40
Figure12.Radarchartcomparisonofeightschedulingstrategiesacrossfournormalizedperformance
metrics.
(2)SpecializedSkills
The Specialized Skills strategy is a scheduling model that assigns roles based on
employees’specificcompetenciesandexpertise. Itscoreprincipleistomaximizeoverall
operationalefficiencybyscientificallydistributingtaskstofullyutilizeeachemployee’s
strengthsandefficiencyadvantages. Thisstrategyrequireshigh-efficiencyorderpickersto
coveratleast60%ofpeak-periodwork.Low-efficiencypickersareexemptfrompeakduties
duringtheirtraining. ForkliftOperatorsarespecializedintoheavy-dutyandlight-duty
groupsbasedoncargotype. Wherepossible,thesameoperatorhandlesthesamecargo
typeconsecutivelytominimizeskill-switchingcosts.
(3)FlexibleWorkingHours
TheFlexibleWorkingHoursstrategyisaschedulingmodelthatgrantsemployees
greaterworkscheduleautonomy. Thecoreprincipleistoenhancebothemployeesatisfac-
tionandproductivity. Thisisachievedbyincreasingflexibilityinworkinghours. Finally,
thisapproachaimstoaccommodatethepersonalizedtimerequirementsofemployees. This
policyallowsemployeestoindicatepreferredandavoidedworkperiods. Whileensuring
weeklytotalworkinghoursmeetrequirements,dailyworkinghourscanflexiblyfluctuate
between4and8h. Employeesmayrequesttimeoffonparticulardatesusingthismethod.
Italsocreatesanaccountsystemforflexibleworkinghours.Employeescanusethismethod
toconvertovertimeworkedinoneweekintopaidtimeoffthenextweek.
Thevalue1.0inthechartrepresentsthemaximumscore. Thecloserthevalueisto1.0,
thebetterthestrategyperformsinthataspect.
Experimentalresultsindicatethatthebalancedshiftstrategydemonstratesthemost
optimalperformanceintermsofcost. Butconsiderablecomfortissacrificedinorderto
obtain this cost benefit. It indicates that although strict rest schedules can lower labor
costs,theyadverselyaffecttheemployeeexperience. Whenitcomestostrikingabalance
betweencomfortpenaltiesandoveralltargetvalues,thebaselinetechniqueworkswell.
Thismethodrankedfifthwithatotalcostscoreof0.678. Itachievesagoodbalancebetween
expenseandworkercomfort.
TheBalancingRotation+SpecializedSkills+FlexibleWorkingHourshasshowntobe
highlybeneficial. Itsoverallobjectivescoreof0.936isrankedsecond,itscomfortpenalty
scoreof0.817isrankedfifth,anditstotalcostscoreof0.966isrankedsecond. Ontheother
https://doi.org/10.3390/systems14030295

Systems2026,14,295 28of40
hand,thecombinationofflexibleworkinghoursandbalancedshiftsfaredbadly,placing
lastintotalobjectivevaluesandsufferingthelargestcomfortpenalty.
Intermsofcomfort,theSpecializedSkillsstrategydidremarkablywell,comingin
third. TheplanwithFlexibleWorkingHoursisthemostexpensiveandperformstheworst
overall. Thisfindingsuggeststhatfullyflexiblearrangementsresultingreatermanagement
andcoordinationcostswithintheexistingorganizationalsetting. Theanticipatedreduction
in employee comfort penalties did not materialize. Even if it costs a little more than
the basic strategy, it is still within a reasonable range. This illustrates how specialized
division of labor may increase productivity without having a major negative effect on
workersatisfaction.
6.3.4. MaximumWorkingTimeDifference
Thisexperimentlookedathowcostandcomfortlevelswereaffectedbyvariationsin
maximumworkinghours. Maximumdisparitiesinworkinghoursbetweentwoandten
werefound.
Figure 13 illustrates the negative link between the total comfort penalty and the
variation in weekly working hours among employees. In particular, the total comfort
penaltyexhibitsadecliningtendencyasthetoplimitofthisgaprises.
Figure13.ImpactofMaximumOperatingDurationDifferencesonCostandComfort.
6.4. ManagementInsightsandRecommendations
Thesensitivityanalysisaboveprovidespractitionerswithactionableinsights.Onthe
basisofthesefindings,weoffertailoredmanagementrecommendationsfordifferententerprises.
(1)ChooseSchedulingSolutionsUnderVariousDemandFluctuationCoefficients
andConfidenceLevelsBasedontheEnterprise’sCharacteristics
Demandfluctuationcoefficientsareusuallylowforestablishedindustrialbusinesses
with reliable operations and precise forecasting. For effective scheduling, a rather low
confidencelevelisadvised. Demandvolatilityisparticularlynoticeableforcompanies
inindustrieslikeretail,e-commerce,andlogisticsthatseelargeseasonalswings. Using
dynamicconfidencelevelmethodsisessentialtogoodmanagement. Tobalanceexpenses
andteamstability,keepyourconfidencelevelbetween0.7and0.8duringoff-peakorsteady
seasons. Inordertoguaranteeservicecapacityduringexpectedpeakseasonsorsignificant
https://doi.org/10.3390/systems14030295

Systems2026,14,295 29of40
promotionalperiods,proactivelyraisetheconfidencelevelto0.85–0.95andaugmentwith
aflexiblepersonnelpool.
(2)OptimizeEmployeeStructureandStaffingNumberstoStrikeaBalancebetween
ComfortandCost
Itisadvisedthatbusinesseskeeptheirpersonnelwithinacceptablebounds. Make
surethereareenoughqualifiedpickersondutytofulfilloperationalneedswhenplanning
dailyshifts.
Thefundamentalreasoningbehindstaffingfororganizationsthatprioritizeemployee
comfortistomaximizeteamskilldensity. Dataunequivocallydemonstratesthattheteam’s
totalcomfortpenaltydecreasesasthepercentageofhigh-efficiencyworkersincreases.High-
efficiencyworkers’jobtraitsarethemaincauseofthis.Ateam’soverallworkflowimproves
whenthesepeopleareincharge. Therearelessoperationaldelaysorburdensbrought
onbylessproductivepersonnel. Asaresult, theteam’sgeneralpainandaccumulated
wearinessarereduced. Buildingalean,highlytalentedstaffshouldthusbethemaingoal.
Forcost-consciousenterprises,thecoreofstaffingliesinidentifyingandmaintain-
ing the “minimum effective combination of working hours that meets operational re-
quirements.”Itisrecommendedtodeterminethecriticalthresholdfortheproportionof
high-efficiencyemployees,whichwasapproximately50%inourexperiments.
Findingawideselectionofthebestvalueformoneyistheaimforcompanieslooking
tostrikeabalancebetweencomfortandaffordability. Thisrangeusuallycorrespondsto
staffing setups in which order pickers with high efficiency make up 60% to 80% of the
workforce. Throughthecoredominanceofhigh-efficiencypersonnel,thesedesignsbalance
effortandefficiencywhileacknowledgingtherealityofheterogeneousteams.
(3)ChooseandIntegrateSchedulingStrategiestoSupportBusinessManagementGoals
Thestudysuggestsusingdifferentapproachesforvariousbusinesses. Atthesame
time,weincorporatetheperspectivesofemployers,employees,customers,andacompre-
hensiveview. Employersprimarilyfocusoncostandoperationalefficiency,employees
careaboutcomfortandwork–lifebalance,whilecustomersvalueserviceefficiencyand
quality. Aholisticperspectiveemphasizesbalancingcostandcomfort. Table9outlinesthe
mainideasforstrategyadviceandexecution.
(4)ModeratelyRelaxWorkingHourVariationManagementtoEnhanceIndividual
AdaptabilityamongEmployees
Theexperimentalresultsindicatethatappropriatelyeasingtheupperlimitonweekly
working hour variations among employees can effectively reduce the overall comfort
penalty. Byreducingthiscomfortpenalty,employeesatisfactioniscorrespondinglyen-
hanced.Rigid,one-size-fits-allmanagementtechniquesarediscouraged.Businessesshould
allowforamodestvarianceinworkinghourswhilemakingsureoperationsareimpacted.
Schedulesarebettermatchedtothedemandsandworkhabitsofindividualemployeesas
aresult.
(5)EstablishaProgressiveOptimizationMechanismandSupportSystem
Whicheverapproachisused,apilot-firststrategywithagradualrolloutisadvised.
Cost,efficiency,andcomfortpenaltyareexamplesofparametersthatneedtoberoutinely
assessed. Establishing clear lines of communication, skill-training initiatives, and data-
drivenschedulingsupportsystemsisalsonecessaryforsuccessfuldeployment. Business
strategy,businessculture,andpeopleneedsmustallbetakenintoaccountwhenchoosing
afinalplan. Theongoinganddynamicoptimizationofhumanresourcemanagementis
madepossiblebythisalignment.
https://doi.org/10.3390/systems14030295

Systems2026,14,295
30of40
Table9.ShiftSchedulingStrategyRecommendations.
| BusinessManagement | Recommended | CoreCompetitive |     |     |
| ------------------ | ----------- | --------------- | --- | --- |
ImplementationGuidelines
| Orientation | SchedulingStrategy | Advantages |     |     |
| ----------- | ------------------ | ---------- | --- | --- |
•
Clearlystipulateatleasttwo
non-consecutiverestdaysper
weekandthemaximumaverage
| CostControl |     | Reducetotalcost | dailyworkinghours. |     |
| ----------- | --- | --------------- | ------------------ | --- |
• Maintaintransparent
| takesPriority | BalancedRotation | whilesuccessfully |     |     |
| ------------- | ---------------- | ----------------- | --- | --- |
(Employer Strategy managingovertime communicationtoexplaincost
Perspective—CostFirst) andoverstaffing. savingsandbusinessneeds.
• Introducemoderateflexibility
duringoff-peakperiodsto
mitigateemployeeresistance.
•
|     |     |     | BasicStrategy: Maintain |     |
| --- | --- | --- | ----------------------- | --- |
existingschedulinglogic,
prioritizingshiftcontinuityand
Excellentoverall
loadbalancing.
|     |     | balancewithlittle | • SkillSpecialization: | Establish |
| --- | --- | ----------------- | ---------------------- | --------- |
EmployeeComfort BasicStrategy compromiseoncomfort; skillgroupingandcertification
| comesfirst | orSpecialized | skillspecialization |     |     |
| ---------- | ------------- | ------------------- | --- | --- |
mechanismstoensure
(EmployeePerspective) SkillsStrategy improvesprofessional high-performingemployees
competencewithout
coverpeakperiods.
|     |     | sacrificingcomfort. | • ComplementaryEmployeeCare |     |
| --- | --- | ------------------- | --------------------------- | --- |
MeasuresandCareer
DevelopmentPathways.
• Beginwithfundamental
techniquesandprogressively
addlimitedflexibilityor
skillgrouping.
Thebasicstrategy
BasicStrategy
BalancingCost rankedfirstoverall;the • Ifacombinationapproachis
|            | orBalanced |                   | chosen,acoordination |     |
| ---------- | ---------- | ----------------- | -------------------- | --- |
| andComfort |            | portfoliostrategy |                      |     |
rotation+Specialized
| (Comprehensive |     | achievedagood | mechanismmustbesetupand |     |
| -------------- | --- | ------------- | ----------------------- | --- |
Skills+Flexible
itmustfirstgothroughpilot
| Perspective) |                      | balancebetweencost |                         |     |
| ------------ | -------------------- | ------------------ | ----------------------- | --- |
|              | WorkingHoursstrategy |                    | testingandverification. |     |
andcomfort.
• Evaluatecostandcomfort
penaltyindicatorsona
regularbasis.
• Workteamsshouldbearranged
accordingtoskilllevelor
Specializeddivisionof
|     |     | laborenhances | cargocategory. |     |
| --- | --- | ------------- | -------------- | --- |
PrioritizeEfficiency
SpecializedSkills operationalefficiency • Toreduceswitchingcosts,
| andQuality |          |                       | schedulerelated |     |
| ---------- | -------- | --------------------- | --------------- | --- |
|            | Strategy | andquality,delivering |                 |     |
(CustomerPerspective)
|     |     | excellentcomfort | tasksconsecutively. |     |
| --- | --- | ---------------- | ------------------- | --- |
• Createasystemfortrainingand
performance.
monitoringquality.
https://doi.org/10.3390/systems14030295

Systems2026,14,295 31of40
Table9.Cont.
BusinessManagement Recommended CoreCompetitive
ImplementationGuidelines
Orientation SchedulingStrategy Advantages
• Setflexibleguidelines,suchas
preferredtimeslotdeclarations
anddailyworkinghourranges.
AvoidpurelyFlexible Deliveringflexibility
Intendto • Combiningjobassignments
WorkingHours;adopt whilecontrollingcosts
implementFlexible basedonskillgroupingwiththe
aBalanced andmaintaining
WorkSchedules remainingneedsofbalanced
rotation+Specialized operationalorder,with
(EmployerPerspective— shiftrotation.
Skills+Flexible overallsatisfactory
FlexibilityFirst) • Makeuseofinformation
WorkingHoursstrategy performance
technologytofacilitate
timetrackingand
schedulingcoordination.
7. Conclusions
Thisstudymakesthreemajorcontributionstothefieldofworkforceschedulingin
county-levellogisticssystems:
(1)Thestudyconvertstheconceptof“human-centeredmanagement”intoquantifiable
objectivesandspecificschedulingguidelines.
(2) The study provides a useful tool for decision-making for logistics managers in
county-levelcenters. Managersjustinputbasicdataandexecutetheenhancedalgorithm
inday-to-dayoperations. Itgeneratesaweeklycalendarinamatterofminutes,balancing
expensesandpenaltiesassociatedwithcomfort.
(3) The results are very applicable outside of this particular instance. Despite the
fact that the data in this paper originates from a specific county-level logistics center,
thecharacteristicsidentified,includingworkerdifferences,demandfluctuations,andthe
coordination between training and scheduling, are common in many similar settings.
Therefore,themodelingframeworkandoptimizationmethodpresentedinthispapercan
beappliedtootherlabor-intensivelogisticsnodesatthecountylevel. Thisoffersuseful
insightsforleanhumanresourcemanagementinsimilarlogisticssystems.
Nevertheless,thisstudyincludesseveralshortcomingsthatsuggestareasforfurther
research. First,sincethemodelwasvalidatedonlyonsmall-to-medium-sizeddatasets,the
generalizabilityofitsresultsislimited. Futureresearchshouldincorporatelarger-scale
scenariostoevaluatethemodel.Second,themodelassumedthatskillacquisitionisabinary
processandthatuncertaindemandfollowsauniformdistributioninordertosimplifythe
problem. Futurestudiesshouldinvestigatedifferentkindsofdemanddistributionsand
presentmoreaccuratelearningcurvemodelsthatshowhowskillsimprovegraduallyover
time. Third,thegoalofthisstudywastoofferasinglecompromiseoptionthatstrikesa
balancebetweenemployeecomfortpenaltyandcost. Thisillustratesthefactthatmanagers
frequentlyhavedistinctpriorities. Theexistingmodelcanbeexpandedinfurtherworkif
managerswanttoinvestigateeverypossibletrade-off. Forexample,thewholeParetofront
mightbegeneratedusinganevolutionarymulti-objectivealgorithmlikeNSGA-II.This
wouldprovidemorechoicestoaidinmakingstrategicdecisions. Fourth,theweightingof
relevantindicatorsinthisstudywasdeterminedbasedoncorporatepreferencesidentified
throughactualsurveys. Inthefuture,wewillexploremorescientificallygroundedweight-
ingmethodsandinvestigatetheirimpactonoptimizationoutcomes. Finally,thispaper
exhibitsrelativelylimitedinnovationatthealgorithmiclevel,lackssystematicparameter
tuning, and suffers from slow runtime performance, indicating room for improvement
incomputationalefficiency. Movingforward,wewilladoptadvancedmethodssuchas
Bayesianoptimizationtoachieveautomaticoptimizationofkeyparameters. Wewillalso
https://doi.org/10.3390/systems14030295

Systems2026,14,295 32of40
explorehybridalgorithmdesignswhiledevelopingmorecompactencodingschemesto
reducethesearchspaceandenhancecomputationalefficiencyinlarge-scalescenarios.
AuthorContributions:Conceptualization,Y.W.andJ.M.;methodology,Y.W.;software,Y.W.;vali-
dation,Y.W.,Y.G.(YuhanGong)andZ.H.;formalanalysis,Y.G.(YuhanGong);investigation,Z.H.;
resources,Y.G.(YiwenGao);datacuration,Y.G.(YiwenGao);writing—originaldraftpreparation,
Y.W.;writing—reviewandediting,J.M.;visualization,Y.W.andY.G.(YuhanGong);supervision,
J.M.;projectadministration,J.M.;fundingacquisition,J.M.Allauthorshavereadandagreedtothe
publishedversionofthemanuscript.
Funding:Thisresearchwasfundedby“JiangxiProvinceCareerEarlyYouthScienceandTechnol-
ogyTalentProgram(20244BCE52148)”and“EastChinaJiaotongUniversityPh.D.StartProgram
(2003424033)”.
DataAvailabilityStatement:Dataarecontainedwithinthearticle.
Acknowledgments:Theauthorsextendgratitudetothemanagementandstaffofthecounty-level
logisticscenterfortheirsupportindatacollectionandoperationalinsights.Wealsoacknowledgethe
technicalsupportprovidedbytheLogisticsLaboratoryofEastChinaJiaotongUniversity.
ConflictsofInterest:Theauthorsdeclarenoconflictsofinterest.
AppendixA.AlgorithmPseudo-CodeandImplementationFramework
TableA1.Pseudo-codefortheimprovedGeneticAlgorithms.
Input:
ProblemParameters: EmployeeSetE,DateSetD,TimeSlotSetT,DemandParameters,etc.
AlgorithmParameters: N=500,G=300,Pc=0.85,Pm=0.05,E=10,k=3
Output:
best_ind,best_fitness
begin
P←∅
fori=1toNdo
ind_i←HEURISTIC_INITIALIZATION()
P←P∪{ind_i}
endfor
best_ind←null
best_fitness←∞
forgen=1toGdo
foreachindinPdo
fitness(ind)←CALCULATE_FITNESS(ind,gen)
iffitness(ind)<best_fitnessthen
best_fitness←fitness(ind)
best_ind←ind
endif
endfor
mating_pool←∅
forj=1toNdo
candidates
winner←argmin_{cand∈candidates}fitness(cand)
mating_pool←mating_pool∪{winner}
endfor
offspring←∅
forj=1toN/2do
p1,p2←Randomlyselecttwoparentsfromthematingpool.
ifrandom(0,1)<Pcthen
https://doi.org/10.3390/systems14030295

Systems2026,14,295 33of40
TableA1.Cont.
crossover_points←Randomlyselecttwointersectionpoints
(c1,c2)←TWO_POINT_CROSSOVER(p1,p2,crossover_points)
else
c1←p1,c2←p2
endif
offspring←offspring∪{c1,c2}
endfor
foreachindinoffspringdo
foreachgeneininddo
ifrandom(0,1)<Pmthen
FLIP_GENE(gene)
endif
endfor
REPAIR_INDIVIDUAL(ind)
endfor
elite←SelecttheEindividualswiththehighestfitnessfromP.
P←offspring∪elite
endfor
returnbest_ind,best_fitness
end
TableA2.Pseudo-codefortheheuristicinitialization.
Input: EmployeesetE,DaysD,TimeslotsT,Demandmatrices(deterministicequivalents)I_pick(d,t),I_fork(d,t)
Output: Initialchromosomeind(binaryarrayoflength|E|·|D|·|T|),traininglistemployee_training_slots
InitializeanemptyscheduleSasa3Darray[|E|][|D|][|T|]filledwith0.
Initializeemployee_training_slots←emptydictionarymappingemployeeindicestolistof(day,slot)pairs.
LetL_low←indicesofinefficientpickers(type=‘pick’andefficiency=low).
//---Step1: Pre-assigntrainingslotsforinefficientpickers---
foreachemp_idxinL_lowdo
training_slots←emptylist
randomlyselectU_mindistinctdaysfromD(withoutreplacement)
foreachselecteddaydo
randomlyselectaslottfromT_train(non-peakslots)
append(day,t)totraining_slots
setS[emp_idx][day][t]←0 //ensurenoworkduringtraining
endfor
employee_training_slots[emp_idx]←training_slots
endfor
//---Step2: Demand-drivenassignmentforeachdayandslot---
foreachdayinDdo
foreachslotinTdo
//Assignpickerstomeetpickingdemand
remaining_pick←I_pick[day][slot]
sortpickersbydescendingefficiency(onlythosenotintrainingatthis(day,slot))
foreachemp_idxinsortedpickersdo
ifremaining_pick≤0thenbreak
ifS[emp_idx][day][slot]==0andworkingheredoesnotexceedconsecutivehourslimitthen
setS[emp_idx][day][slot]←1
remaining_pick←remaining_pick-efficiency[emp_idx]×2
endif
endfor
https://doi.org/10.3390/systems14030295

Systems2026,14,295 34of40
TableA2.Cont.
//Assignforkliftstomeetforkliftdemand
remaining_fork←I_fork[day][slot]
foreachforkliftindexemp_idx(allforkliftsareefficient)do
ifremaining_fork≤0thenbreak
ifS[emp_idx][day][slot]==0andconsecutivehourslimitsatisfiedthen
setS[emp_idx][day][slot]←1
remaining_fork←remaining_fork-efficiency[emp_idx]×2
endif
endfor
//Ensureatleastonepickerandoneforkliftareonduty
ifnopickerworkingat(day,slot)then
randomlyselectanavailablepicker(notintraining)andsetS[emp_idx][day][slot]←1
endif
ifnoforkliftworkingat(day,slot)then
randomlyselectanavailableforkliftandsetS[emp_idx][day][slot]←1
endif
endfor
endfor
//---Step3: Applyconstraintrepairoperators---
S←repair_weekly_rest(S)
S←repair_peak_work_count(S)
S←repair_minimum_hours(S)
S←repair_intensity_relaxation(S) //ensuresarelaxedshiftafterahigh-intensityday
S←repair_consecutive_hours(S)
S←repair_training(S) //correcttrainingcountsandconflicts
S←ensure_uniqueness(S) //noduplicateassignmentsperemployeeperslot
//---Step4: Flattenscheduleintochromosome---
ind←emptylist
foreachemp_idxinEdo
foreachdayinDdo
foreachslotinTdo
appendS[emp_idx][day][slot]toind
endfor
endfor
endfor
returnind,employee_training_slots
FigureA1.DEAPCoreModulesandImplementedFunctions.
AppendixB.PreliminariesonUncertainTheory
AppendixB.1. AxiomsandDefinitions
Demandisoftenvulnerabletoseveralsourcesofuncertaintyinreal-worldlogistics
andlaborscheduling,includingseasonalvariations,dailyorderswings,andunforeseen
disruptiveoccurrences.Asaresult,itisfrequentlychallengingtomakeaccuratepredictions
https://doi.org/10.3390/systems14030295

Systems2026,14,295
35of40
usingfixednumbers. Suchintrinsicuncertaintiesarebeyondthecapabilitiesoftraditional
deterministicoptimizationmethods. Inordertobuildaworkforceschedulingmodelbased
onunpredictabledemand,thispaperintroducesuncertaintytheory.
Thetheoryofuncertainty,proposedbyLiu,providesacompleteaxiomaticframework
for handling uncertain information lacking historical data or relying on expert experi-
ence[39]. Itscoreisthemeasureofuncertainty,whichsatisfiesthefollowingfouraxioms:
AxiomA1(RegularityAxiom).
|     |     | M{Γ} | =1  |     |     |     |
| --- | --- | ---- | --- | --- | --- | --- |
(A1)
Here,Γdenotestheuniversalset,indicatingthatthemeasureofacertaineventoccurringis1.
ForanyeventΛ,wehaveFormula(A2).
AxiomA2(DualityAxiom).
M{Λ}+M{Λc}
|     |     |     |     | =1  |     | (A2) |
| --- | --- | --- | --- | --- | --- | ---- |
AxiomA3(AdditivityAxiom). Foranycountablesequenceofevents{Λ},Formula(A3)holds.
i
|     |     | (cid:26) (cid:27) | ∞   |       |     |      |
| --- | --- | ----------------- | --- | ----- | --- | ---- |
|     |     | ∞                 | ∑   |       |     |      |
|     | M   | ∪Λ                | ≤   | M{Λ } |     | (A3) |
|     |     | i                 |     | i     |     |      |
i=1
i=1
(Γ,L,M)
Axiom A4 (Product Axiom). Let denote the uncertainty space, then the product
uncertaintymeasureMsatisfiesFormula(A4).
|     | (cid:26) | ∞ (cid:27) |      |      |     |      |
| --- | -------- | ---------- | ---- | ---- | --- | ---- |
|     | M        | ∩ Λ        | = Λ∞ | M {Λ |     |      |
|     |          | k          | k=1  | k    | k } | (A4) |
k=1
whereΛ ∈
k L k .
(Γ,L,M)
Definition A1 (Uncertain Variable). Let denote the uncertainty space. If a func-
tion :Γ→ R satisfiesthatforanyBorelset B ⊂ R,theset{γ ∈ Γ| ξ(γ) ∈ B} ∈ LisinL,
ξ
thenξiscalledanuncertainvariable.
DefinitionA2(UncertaintyDistribution). Theuncertaintydistribution Φ: R → [0,1]ofthe
uncertainvariable ξisdefinedasshowninFormula(A5).
|     |     | Φ(x) = | M{ξ | ≤ x} |     | (A5) |
| --- | --- | ------ | --- | ---- | --- | ---- |
AnuncertaintydistributionΦ(x)issaidto
DefinitionA3(RegularUncertaintyDistribution).
beregularifitiscontinuousandstrictlyincreasingwithrespecttoxwherever0< Φ(x) <1,and
satisfies,asshowninFormula(A6).
|     |      | Φ(x) =0, |      | Φ(x) =1 |     |      |
| --- | ---- | -------- | ---- | ------- | --- | ---- |
|     | lim  |          | lim  |         |     | (A6) |
|     | x→−∞ |          | x→+∞ |         |     |      |
DefinitionA4(IndependenceofUncertainVariables). Uncertainvariablesξ ,ξ ,...,ξ are
1 2 n
saidtobeindependentifforanyBorelsetsB , B ,..., B ,asshowninFormula(A7).
|     |          | 1        | 2   | n   |     |     |
| --- | -------- | -------- | --- | --- | --- | --- |
|     | (cid:26) | (cid:27) |     |     |     |     |
n
| M   | ∩(ξ | ∈ B) | = Λn | M{ξ | ∈ B}. | (A7) |
| --- | --- | ---- | ---- | --- | ----- | ---- |
|     |     | i i  | i=1  | i   | i     |      |
i=1
DefinitionA5(LinearUncertainVariables). Ifthevariableξ isnotassumedtofollowalinear
uncertaintydistribution,thenasshowninFormula(A8).
https://doi.org/10.3390/systems14030295

Systems2026,14,295
36of40

|     |     |     |     |     | 0,  | x < | a   |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |

|     |     |     |     | Φ(x) = | x−a, |     |       |     |     |      |
| --- | --- | --- | --- | ------ | ---- | --- | ----- | --- | --- | ---- |
|     |     |     |     |        |      | a ≤ | x < b |     |     | (A8) |
b−a
1,
|     |     |     |     |     |     | x ≥ | b   |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Thenξ isreferredtoasalinearuncertainvariable,denotedasL(a,b),wherea < b.
DefinitionA6(InverseUncertaintyDistribution). Foranuncertainvariableξ witharegular
uncertaintydistributionΦ(x),itsinverseuncertaintydistribution Φ−1:(0,1) → R isdefinedas
afunctionsatisfyingthefollowingconditions,asshowninFormula(A9).
Φ−1(α)
|     |     |     |     | =inf{x | ∈R| | Φ(x) | ≥ α} |     |     | (A9) |
| --- | --- | --- | --- | ------ | --- | ---- | ---- | --- | --- | ---- |
For the linear uncertain variable L(a,b), its inverse uncertainty distribution is given by
Formula(A8).
Φ−1(α)
|              |                   |     |     | =   | (1−α)a+αb, |     | α ∈ (0,1) |     |     | (A10) |
| ------------ | ----------------- | --- | --- | --- | ---------- | --- | --------- | --- | --- | ----- |
| AppendixB.2. | TheoremsandProofs |     |     |     |            |     |           |     |     |       |
Thefollowingtheoremsarefundamentalforconvertinganuncertainprogramming
modelwithmonotonefunctionsintoanequivalentdeterministicform. Theyaredueto
Liu[39]andformthetheoreticalbasisforthemodelconversioninSection4.4.
TheoremA1(ExpectedValueofMonotoneFunction). Letξ ,ξ ,...,ξ beindependentuncer-
|     |     |     |     |     |     |     | 1 2 | n   |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
tainvariableswithregularuncertaintydistributionsΦ,Φ,...,Φ ,respectively.Supposethefunc-
|     |     |     |     |     |     | 1   | 2 n |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
tion f(x,ξ ,ξ ,...,ξ )iscontinuous,strictlyincreasingwithrespecttoξ ,ξ ,...,ξ andstrictly
|     | 1 2 | n   |     |     |     |     |     | 1 2 | m   |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
decreasingwithrespecttoξ m+1 ,ξ m+2 ,...,ξ n . Thentheexpectedvalueof f(x,ξ 1 ,ξ 2 ,...,ξ n )is
givenbyFormula(A11).
|         |                |     | (cid:90) 1 (cid:16) |              |     |         |                |        | (cid:17) |       |
| ------- | -------------- | --- | ------------------- | ------------ | --- | ------- | -------------- | ------ | -------- | ----- |
| E[f(x,ξ |                | )]= | x,Φ                 | −1(α),...,Φ− |     | 1(α),Φ− | 1 (1−α),...,Φ− | 1(1−α) |          |       |
|         | 1 ,ξ 2 ,...,ξn |     | f                   |              | m   |         | m+             | n      | dα       | (A11) |
|         |                |     | 0                   | 1            |     |         | 1              |        |          |       |
ProofofTheoremA1. Sinceξ ,...,ξ areindependentandregular,theinverseuncertainty
|     |     |     | 1   | n   |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
distribution of f(x,ξ 1 ,...,ξ n ) is shown in Formula (A12), by the operational law for
| monotonefunctions. |        | (Theorem3.20inLiu[39]) |                         |     |     |     |                    |     |          |       |
| ------------------ | ------ | ---------------------- | ----------------------- | --- | --- | --- | ------------------ | --- | -------- | ----- |
|                    | Ψ−1(α) | (cid:16)               | x,Φ−1(α),...,Φ−1(α),Φ−1 |     |     |     | (1−α),...,Φ−1(1−α) |     | (cid:17) |       |
|                    |        | = f                    |                         |     |     |     |                    |     |          | (A12) |
|                    |        |                        | 1                       |     | m   | m+1 |                    | n   |          |       |
AccordingtoTheorem3.26inLiu[39],theexpectedvalueofanuncertainvariable
| withinversedistributionΨ−1(α)isgivenby |     |     |     |     | (cid:82)1Ψ−1(α)dα. |     |     |     |     |     |
| -------------------------------------- | --- | --- | --- | --- | ------------------ | --- | --- | --- | --- | --- |
Substitutingtheexpressionfor
0
| Ψ−1(α)yields(41). |     | □   |     |     |     |     |     |     |     |     |
| ----------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Theorem A2 (Chance Constraint Transformation). Let ξ ,ξ ,...,ξ be independent un-
|     |     |     |     |     |     |     | 1   | 2 n |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Φ,Φ,...,Φ
certain variables with regular uncertainty distributions n respectively. Sup-
|     |     |     |       |     |     |     | 1 2 |     |     |     |
| --- | --- | --- | ----- | --- | --- | --- | --- | --- | --- | --- |
|     |     |     | g(x,ξ |     | )   |     |     |     |     |     |
pose the constraint function 1 ,ξ 2 ,...,ξ n is continuous, strictly increasing with respect
toξ ,ξ ,...,ξ andstrictlydecreasingwithrespecttoξ ,ξ ,...,ξ . Thenforagivenconfi-
| 1           | 2 k                                               |     |         |     |           | k+1   | k+2 | n   |     |       |
| ----------- | ------------------------------------------------- | --- | ------- | --- | --------- | ----- | --- | --- | --- | ----- |
| dencelevelα | ∈ (0,1),thechanceconstraintisshowninFormula(A13). |     |         |     |           |       |     |     |     |       |
|             |                                                   |     | M{g(x,ξ |     | ,ξ ,...,ξ | ) ≤0} | ≥ α |     |     | (A13) |
|             |                                                   |     |         |     | 1 2       | n     |     |     |     |       |
IfandonlyifEquation(A14)holds.
|     | (cid:16) |                         |     |     |                    |     |     | (cid:17) |     |       |
| --- | -------- | ----------------------- | --- | --- | ------------------ | --- | --- | -------- | --- | ----- |
|     |          | x,Φ−1(α),...,Φ−1(α),Φ−1 |     |     | (1−α),...,Φ−1(1−α) |     |     |          |     |       |
|     | g        |                         |     |     |                    |     |     | ≤0.      |     | (A14) |
|     |          | 1                       |     | k   | k+1                |     | n   |          |     |       |
https://doi.org/10.3390/systems14030295

Systems2026,14,295
37of40
Proof of Theorem A2. By the operational law, the inverse uncertainty distribution of
|     |     | g(x,ξ    |     | )isshowninFormula(A15). |                                  |     |     |     |                    |     |          |
| --- | --- | -------- | --- | ----------------------- | -------------------------------- | --- | --- | --- | ------------------ | --- | -------- |
|     |     | 1 ,...,ξ | n   |                         |                                  |     |     |     |                    |     |          |
|     |     |          |     | −1(α)                   | (cid:16) x,Φ−1(α),...,Φ−1(α),Φ−1 |     |     |     | (1−α),...,Φ−1(1−α) |     | (cid:17) |
|     |     |          | Y   | =                       | g                                |     |     |     |                    |     | (A15)    |
|     |     |          |     |                         |                                  | 1   | k   | k+1 |                    | n   |          |
ForanuncertainvariableηwithinversedistributionY−1,theinequalityM{η ≤ 0} ≥
αisequivalenttoY −1(α) ≤0. Applyingthisequivalencetoη = g(x,ξ ,...,ξ ),weobtain
|     |     |                                                      |     |     |     |     |     |     |     | 1   | n   |
| --- | --- | ---------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|     |     | thatcondition(43)holdsifandonlyifcondition(44)holds. |     |     |     |     |     |     | □   |     |     |
TheoremA3(EquivalentCrispFormulation). Consideranuncertainprogrammingmodel,as
showninFormula(A16).

|     |     |     |     |   | min E[f(x,ξ |     | ,ξ ,...,ξ )] |         |                   |     |       |
| --- | --- | --- | --- | --- | ----------- | --- | ------------ | ------- | ----------------- | --- | ----- |
|     |     |     |     |     | x           | 1   | 2 n          |         |                   |     |       |
|     |     |     |     |     | subjectto:  |     |              |         |                   |     | (A16) |
|     |     |     |     |     | (cid:8)     |     |              | (cid:9) |                   |     |       |
|     |     |     |     |   | M g (x,ξ    | ,ξ  | ,...,ξ ) ≤0  | ≥       | α , j =1,2,...,p, |     |       |
|     |     |     |     |     | j           | 1   | 2 n          |         | j                 |     |       |
where ξ ,ξ ,...,ξ are independent uncertain variables with regular uncertainty distribu-
|     |     |     | 1 2 | n   |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
tions Φ,Φ,...,Φ . Assume that f(x,ξ ,ξ ,...,ξ ) is continuous, strictly increasing
|     |     |     | 1 2 | n   |     |     | 1   | 2   | n   |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
with respect to ξ ,ξ ,...,ξ m and strictly decreasing with respect to ξ m+1 ,ξ m+2 ,...,ξ n ; For
1 2
|     |     |     | (x,ξ |     | )   |     |     |     |     |     |     |
| --- | --- | --- | ---- | --- | --- | --- | --- | --- | --- | --- | --- |
each j, g j 1 ,ξ 2 ,...,ξ n is continuous, strictly increasing with respect to ξ 1 ,ξ 2 ,...,ξ kj and
|     |     | strictlydecreasingwithrespecttoξ |     |     |     |       | ,ξ ,...,ξ | .   |     |     |     |
| --- | --- | -------------------------------- | --- | --- | --- | ----- | --------- | --- | --- | --- | --- |
|     |     |                                  |     |     |     | kj +1 | kj +2     | n   |     |     |     |
Thentheuncertainprogrammingmodel(46)isequivalenttothefollowingFormula(A17):
|     |     |           | (cid:82) | (cid:16)           |     |         |                    |     |          | (cid:17)     |       |
| --- | --- | ---------- | -------- | ------------------ | --- | ------- | ------------------ | --- | -------- | ------------ | ----- |
|     |     | minx       | 1        | f x,Φ −1(α),...,Φ− |     | 1(α),Φ− | 1 (1−α),...,Φ−     |     | 1(1−α)   | dα           |       |
|     |     |         | 0        | 1                  |     | m       | m+ 1               |     | n        |              |       |
|     |     | subjectto: |          |                    |     |         |                    |     |          |              | (A17) |
|     |     |         | (cid:16) |                    |     |         |                    |     | (cid:17) |              |       |
|     |     | g          | x,Φ−1(α  | ),...,Φ−1(α        |     | ),Φ−1   | (1−α ),...,Φ−1(1−α |     | ) ≤0,    | j=1,2,...,p. |       |
|     |     |            | j        | 1 j                | kj  | j kj    | +1 j               | n   | j        |              |       |
ProofofTheoremA3. TheoremA3followsdirectlybyapplyingTheoremA1totransform
theobjectivefunctionandTheoremA2totransformeachchanceconstraintin(46). The
□
resultingexpressionsareexactlythosein(47).
AppendixC.IndividualEmployeeMetrics
TableA3.EmployeePreferences.
EmployeeID Monday Tuesday Wednesday Thursday Friday Saturday Sunday
| P1  | 0   |     | 0   |     | 0   |     | 0   |     | 0   | 1   | 0   |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| P2  | 0   |     | 0   |     | 0   |     | 0   |     | 1   | 0   | 0   |
| P3  | 0   |     | 0   |     | 0   |     | 1   |     | 0   | 0   | 0   |
| P4  | 0   |     | 0   |     | 1   |     | 0   |     | 0   | 0   | 0   |
| P5  | 0   |     | 1   |     | 0   |     | 0   |     | 0   | 0   | 0   |
| P6  | 1   |     | 0   |     | 0   |     | 0   |     | 0   | 0   | 0   |
| P7  | 0   |     | 0   |     | 1   |     | 0   |     | 0   | 0   | 0   |
| P8  | 0   |     | 0   |     | 0   |     | 1   |     | 0   | 0   | 0   |
| P9  | 0   |     | 0   |     | 0   |     | 0   |     | 1   | 0   | 0   |
| F1  | 0   |     | 0   |     | 0   |     | 0   |     | 0   | 0   | 1   |
| F2  | 0   |     | 0   |     | 0   |     | 0   |     | 0   | 1   | 0   |
| F3  | 0   |     | 0   |     | 0   |     | 1   |     | 0   | 0   | 1   |
| F4  | 0   |     | 0   |     | 1   |     | 0   |     | 0   | 0   | 0   |
| F5  | 0   |     | 1   |     | 0   |     | 0   |     | 0   | 0   | 0   |
| F6  | 1   |     | 0   |     | 0   |     | 0   |     | 0   | 1   | 0   |
| F7  | 0   |     | 0   |     | 0   |     | 0   |     | 1   | 0   | 0   |
https://doi.org/10.3390/systems14030295

Systems2026,14,295
38of40
TableA3.Cont.
EmployeeID Monday Tuesday Wednesday Thursday Friday Saturday Sunday
| F8  | 0   | 0   | 0   | 1   | 0   | 0   |     | 0   |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| F9  | 1   | 0   | 0   | 0   | 0   | 0   |     | 0   |
TableA4.EmployeeIndividualWorkloadandComfortPenaltyMetrics.
WorkingHours
|     | EmployeeID |     |     |     | Cost(RMB) | TotalComfortPenalty |     |     |
| --- | ---------- | --- | --- | --- | --------- | ------------------- | --- | --- |
(Hours/Week)
|     |     | P1  | 28  |     | 1560.00 |     | 15.0 |     |
| --- | --- | --- | --- | --- | ------- | --- | ---- | --- |
|     |     | P2  | 30  |     | 1600.00 |     | 14.0 |     |
|     |     | P3  | 26  |     | 1520.00 |     | 16.0 |     |
|     |     | P4  | 24  |     | 1480.00 |     | 10.0 |     |
|     |     | P5  | 24  |     | 1480.00 |     | 13.0 |     |
|     |     | P6  | 24  |     | 1480.00 |     | 13.0 |     |
|     |     | P7  | 26  |     | 1520.00 |     | 16.0 |     |
|     |     | P8  | 24  |     | 1480.00 |     | 14.0 |     |
|     |     | P9  | 24  |     | 1480.00 |     | 14.0 |     |
|     |     | F1  | 24  |     | 2220.00 |     | 18.0 |     |
|     |     | F2  | 26  |     | 2280.00 |     | 17.0 |     |
|     |     | F3  | 24  |     | 2220.00 |     | 17.0 |     |
|     |     | F4  | 24  |     | 2220.00 |     | 14.0 |     |
|     |     | F5  | 24  |     | 2220.00 |     | 15.0 |     |
|     |     | F6  | 24  |     | 2220.00 |     | 18.0 |     |
|     |     | F7  | 30  |     | 2400.00 |     | 19.0 |     |
|     |     | F8  | 26  |     | 2280.00 |     | 20.0 |     |
|     |     | F9  | 30  |     | 2400.00 |     | 21.0 |     |
References
1. The 14th Five-Year Plan for Smart Manufacturing Development. Available online: https://www.gov.cn/2021-12/28/
content_5664996.htm(accessedon21January2026).
2. Wang, M.; Kumar, M.; Tsolakis, N.ExploringtheRoleofJobSatisfactioninEnhancingLogisticsPerformanceintheEraof
Industry5.0.Int.J.Logist.Res.Appl.2025,Earlyaccess.[CrossRef]
3. Pasparakis, A.; De Vries, J.; De Koster, R. Assessing the Impact of Human–Robot Collaborative Order Picking Systems on
WarehouseWorkers.Int.J.Prod.Res.2023,61,7776–7790.[CrossRef]
4. Li,Y.;Lin,X.H.;Chen,J.X.AnalysisoftheCurrentSituationandApproachesfortheConstructionofCounty-Township-Village
Three-LevelExpressDeliveryLogisticsSystem.JiazhiGongcheng2022,41,42–44.
5. Zhou,H.M.DigitalTechnologyEmpowerstheDevelopmentofCountyLogisticsIndustry.DangdaiXianyuJingji2024,10,88–89.
6. Odunayo,H.;Abe,I.TheRelationshipbetweenEmployeeSatisfactionandOrganizationalEfficiency:ACaseStudyofSelected
NigerianRetailChains.NIUJ.Soc.Sci.2023,9,187–197.[CrossRef]
7. JunaidiAmrin,M.;Abadi,F.TheEffectofWorkFlexibilityonEmployeePerformanceandJobSatisfactionasMediationina
LogisticsCompany.MediaBinaIlm.2024,18,1491–1502.[CrossRef]
8. Sitorus,T.H.;Siagian,H.L.BebanKerjaDanFleksibilitasKerjaTerhadapKepuasanKerjaDenganMotivasiSebagaiPemediasi.
J.Manag.Bussines(JOMB)2023,5,1182–1194.[CrossRef]
9. Investigation Report on the Development Status of the Express Delivery Industry in Ningyang County. Available online:
http://www.ny.gov.cn/art/2025/10/16/art_228261_10358435.html(accessedon16January2026).
10. Releaseofthe2023GuangzhouHumanCapitalIndex(LogisticsIndustry). Availableonline: https://baijiahao.baidu.com/
s?id=1782786745747947322(accessedon16January2026).
11. Li,J.StudyontheRelationshipbetweenJobHappinessandTurnoverIntention—BasedontheMediatingRoleofEmployees’
Self-Efficacy.ChinaManag.Inform.2025,28,188–190.
12. Gu,F.;Ding,J.AnalysisofCountermeasuresforTalentLossinLogisticsEnterprises.Logist.Technol.2019,38,31–34.
13. NetEaseSmartSchedulingSystem:ANewEngineforAI-DrivenDigitalTransformationinHumanResources.Availableonline:
https://www.163.com/dy/article/JV23JPJ205382F02.html?spss=dy_author(accessedon21February2026).
https://doi.org/10.3390/systems14030295

Systems2026,14,295 39of40
14. Yu,Y.;Yu,C.;Xu,G.;Zhong,R.Y.;Huang,G.Q.AnOperationSynchronizationModelforDistributionCenterinE-Commerce
LogisticsService.Adv.Eng.Inform.2020,43,101014.[CrossRef]
15. Marchesi,J.F.;Hamacher,S.;Peres,I.T.StochasticModelforPhysicianStaffingandSchedulinginEmergencyDepartmentswith
MultipleTreatmentStages.Eur.J.Oper.Res.2025,324,492–505.[CrossRef]
16. Naderi,B.;Begen,M.A.;Zaric,G.S.;Roshanaei,V.ANovelandEfficientExactTechniqueforIntegratedStaffing,Assignment,
Routing,andSchedulingofHomeCareServicesunderUncertainty.Omega2023,116,102805.[CrossRef]
17. Jafry,M.A.;Jenny,A.M.;Lubinga,S.J.;Larsen-Cooper,E.;Crawford,J.;Matemba,C.;Babigumira,J.B.ExaminationofPatient
FlowinaRuralHealthCenterinMalawi.BMCRes.Notes2016,9,2347.[CrossRef][PubMed]
18. Lin,M.M.;Shu,Y.-C.;Lu,B.-Z.;Fang,P.-S.SolvingNurseSchedulingProblemviaPyQUBO.Ann. Math. Sci. Appl. 2025,10,
149–168.[CrossRef]
19. Ma,H.;Wang,S.;Gu,X.ResearchonStaffSchedulinginSortingCentersBasedonSARIMA-CEEMD-LSTMModelandTwo-Stage
OptimizationModel.IEEEAccess2025,13,179419–179437.[CrossRef]
20. Nasir,V.;Hosseini,A.;Binfield,L.;Hasani,N.;Ghotb,S.;Diederichs,V.;Fox,G.O.;McCann,A.J.;Riggio,M.;Chandler,K.D.;etal.
Human-CentricIndustry5.0Manufacturing:AMulti-LevelFrameworkfromDesigntoConsumptionwithinSociety5.0.Int.J.
Sustain.Eng.2025,18,2551000.[CrossRef]
21. Black,J.;LaVenture,K.TheHumanFactortoProfitability:LeveragingPeople-CenteredCulturesasMeaningfulOrganizations.
PublicIntegr.2017,20,444–458.[CrossRef]
22. Giacomin,J.WhatIsHumanCentredDesign?Des.J.2015,17,606–623.[CrossRef]
23. Spiller,R.EthicalBusinessandInvestment:AModelforBusinessandSociety.J.Bus.Ethics2000,27,149–160.[CrossRef]
24. Ghobakhloo,M.;Iranmanesh,M.;Tseng,M.-L.;Grybauskas,A.;Stefanini,A.;Amran,A.BehindtheDefinitionofIndustry5.0:A
SystematicReviewofTechnologies,Principles,Components,andValues.J.Ind.Prod.Eng.2023,40,432–447.[CrossRef]
25. Black,J.S.;vanEsch,P.AI-EnabledRecruiting: WhatIsItandHowShouldaManagerUseIt? Bus. Horiz. 2020,63,215–226.
[CrossRef]
26. Chen,Z.ArtificialIntelligence-VirtualTrainer:InnovativeDidacticsAimedatPersonalizedTrainingNeeds.J.Knowl.Econ.2022,
14,2007–2025.[CrossRef]
27. Nasirian, A.; Zhang, L.; Costa, A.M.; Abbasi, B. Multiskilled Workforce Staffing and Scheduling: A Logic-Based Benders’
DecompositionApproach.Eur.J.Oper.Res.2024,323,20–33.[CrossRef]
28. Cabrera,N.;Cordeau,J.;Mendoza,J.E.TheWorkforceSchedulingandRoutingProblemwithPark-And-Loop.Networks2024,85,
38–60.[CrossRef]
29. Hu,Y.;Liu,Q.;Li,S.;Wu,W.Multi-ObjectiveRobustOptimizationofStaffSchedulingforEmergencyunderStochasticDemand.
ExpertSyst.Appl.2024,254,124214.[CrossRef]
30. Park,C.H.;Ko,Y.D.APracticalStaffSchedulingStrategyConsideringVariousTypesofEmploymentintheConstructionIndustry.
Algorithms2022,15,321.[CrossRef]
31. Bocewicz,G.;Smutnicki,C.;Jasiulewicz-Kaczmarek,M.;Wójcik,R.;Banaszak,Z.Competence-BasedRobustSchedulingofCyclic
WorkforceRelocation.IFAC-PapersOnLine2023,56,132–137.[CrossRef]
32. Chen,S.;Zhang,N.;Wang,A.PulsatingAssemblyProductionPersonnelSchedulingTechnologyBasedonImprovedGenetic
Algorithm. In Proceedings of the 2022 IEEE International Conference on Mechatronics and Automation (ICMA), ELECTR
NETWORK,Guilin,China,7–10August2022;pp.1346–1351.[CrossRef]
33. Mystakidis,A.;Koukaras,C.;Koukaras,P.;Kaparis,K.;Stavrinides,S.G.;Tjortjis,C.OptimizingNurseRostering:ACaseStudy
UsingIntegerProgrammingtoEnhanceOperationalEfficiencyandCareQuality.Healthcare2024,12,2545.[CrossRef]
34. Wang, R.; Shehadeh, K.S.; Xie, X.; Li, L. Data-Driven Integrated Home Service Staffing and Capacity Planning: Stochastic
OptimizationApproaches.Comput.Oper.Res.2023,159,106348.[CrossRef]
35. Gong,X.;Wang,J.-J.;Miao,H.;Yu,L.;Liu,Z.AStochasticOptimizationModelandDecompositionTechniquesforSurgery
SchedulingwithDurationandEmergencyDemandUncertainty.Comput.Ind.Eng.2025,204,111096.[CrossRef]
36. Porto,A.F.;Lusa,A.;Herazo,S.;Henao,C.A.ImprovingtheRobustnessofRetailWorkforceManagementwithaLaborFlexibility
StrategyandConsiderationofDemandUncertainty.Oper.Res.Perspect.2025,15,100345.[CrossRef]
37. Bogataj,M.;Bogataj,D.;Drobne,S.TheDynamicsofSpecialisedHousingConstructioninaTimeofHumanResourceShortages
inLong-TermCareServices.Int.J.Prod.Econ.2025,287,109670.[CrossRef]
38. Wu,Z.;Chen,Q.;Mao,N.;Xu,G.TwoScenario-BasedHeuristicsforStochasticShiftDesignProblemwithTask-BasedDemand.
Appl.Sci.2023,13,10070.[CrossRef]
39. Liu,B.UncertaintyTheory;Springer:NewYork,NY,USA,2016;ISBN9783662499887.
40. Wang,Q.B.;Liang,Y.H.;Zheng,J.F.RouteOptimizationofNortheastAsia-EuropeMultimodalTransportConsideringTimeUncer-
tainty.J.Transp.Syst.Eng.Inf.Technol.2026,inpress.Availableonline:https://link.cnki.net/urlid/11.4520.U.20251210.1722.011
(accessedon24February2026).
https://doi.org/10.3390/systems14030295

Systems2026,14,295 40of40
41. Jiang,G.T.;Ji,J.Y.;Dong,J.W.Multi-typeVehicleDynamicRouteOptimizationforGreenLogisticsDistribution.Syst.Eng.Theory
Pract.2024,44,2362–2380.
42. Zheng,H.;Vatsa,P.;Ma,W.;Zhou,X.WorkingHoursandJobSatisfactioninChina:AThresholdAnalysis.ChinaEcon.Rev.2023,
77,101902.[CrossRef]
43. tenBrummelhuis,L.L.;Calderwood,C.;Rosen,C.;Gabriel,A.PeakingToday,TakingItEasyTomorrow: DailyPerformance
DynamicsofWorkingLongHours.J.Organ.Behav.2024,46,530–547.[CrossRef]
44. Lee,Y.;Seo,E.-H.;Lee,W.C.LongWorkingHoursandtheRiskofGlucoseIntolerance:ACohortStudy.Int.J.Environ.Res.Public
Health2022,19,11831.[CrossRef][PubMed]
45. Ma,X.ImpactofLongWorkingHoursonMentalHealth:EvidencefromChina.Int.J.Environ.Res.PublicHealth2023,20,1641.
[CrossRef]
Disclaimer/Publisher’sNote: Thestatements, opinionsanddatacontainedinallpublicationsaresolelythoseoftheindividual
author(s)andcontributor(s)andnotofMDPIand/ortheeditor(s).MDPIand/ortheeditor(s)disclaimresponsibilityforanyinjuryto
peopleorpropertyresultingfromanyideas,methods,instructionsorproductsreferredtointhecontent.
https://doi.org/10.3390/systems14030295