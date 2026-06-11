S
symmetry
Citation:Pu,X.;Zhao,X.Post-
EarthquakeEmergencyLogistics
Location-RoutingOptimization
ConsideringVehicleThree-
DimensionalLoadingConstraints.
Symmetry2024,16,1080. https://
doi.org/10.3390/sym16081080
AcademicEditors:YunfeiFangand
PengWu
Received:4August2024
Revised:16August2024
Accepted:18August2024
Published:20August2024
Copyright: © 2024 by the authors.
Licensee MDPI, Basel, Switzerland.
Thisarticleisanopenaccessarticle
distributed under the terms and
conditionsoftheCreativeCommons
Attribution(CCBY)license(https://
creativecommons.org/licenses/by/
4.0/).
S
Article
Post-Earthquake Emergency Logistics Location-Routing
Optimization Considering Vehicle Three-Dimensional
Loading Constraints
XujinPu*andXuZhao
BusinessSchool,JiangnanUniversity,Wuxi214122,China;6220903017@stu.jiangnan.edu.cn
* Correspondence:puyiwei@ustc.edu
Abstract:Anefficienthumanitarianemergencylogisticsnetworkisvitalinrespondingtoearthquake
disasters. However,theasymmetricinformationinherentinthelocationanddistributionstages
cancomplicatethehumanitarianemergencylogisticsnetworkdesigningprocess,resultinginan
asymmetricoptimizationproblem.Thispaperaddressesamulti-objectivehumanitarianemergency
logisticsnetworkdesignproblemduringtheearthquakeresponsephase.Theobjectiveistoreduce
societalexpenses(e.g.,logisticalanddeprivationcosts)andmitigaterisktothelogisticsnetwork
byidentifyingidealsitesfordistributionhubs,optimalemergencymaterialdistributionstrategies,
andprecisematerialloadingplans.Theproposedmodeltakesintoaccountvariousconstrainttypes,
suchas3Dloadinglimitationsforreliefmaterials,interruptionsindistributionhubs,distribution
centers’capacity,transportvehicles’capacity,andspecifictimewindowsfordemandpoints.First,
amulti-objectivemixed-integerprogrammingmodelisestablishedtosolvetheproblem. Uncer-
taintyismodeledusingascenario-basedprobabilityapproach. Second,amulti-objectivegenetic
algorithmbasedonadaptivelargeneighborhoodsearch(MOGA-ALNS)isdesignedtofurtheropti-
mizethesolutionsobtainedfromtheevolutionaryprocessusinganadaptivelargeneighborhood
searchalgorithm.Furthermore,theMOGA-ALNSintegratesasimulatedannealingprocessinthe
neighborhoodsearchstagetoinhibitthealgorithmfromreachinglocaloptimums.Ultimately,the
MOGA-ALNSiscomparedtothreeadditionalmulti-objectiveoptimizationalgorithms.Thecompre-
hensiveanalysisanddiscussionconductedunequivocallyvalidatethecompetitivenessandefficacy
oftheproposedapproach.
Keywords:emergencylogistics;multi-objectiveoptimization;three-dimensionalloading;adaptive
largeneighborhoodsearch
1. Introduction
Theglobaloccurrenceofnaturaldisastershasbecomeincreasinglycommon.Afghanistan
experienceda6.8magnitudeearthquakeinJune2022,leadingtoaround1500deathsandnu-
merousinjuries. A7.8magnitudeearthquakeclosetotheTurkey–SyriaborderinFebruary
2023resultedinmorethan59,000fatalitiesandeconomicdamagessurpassing104billion
USD.Moroccoendureda6.8magnitudeearthquakeinSeptember2023,resultinginclose
to3000fatalitiesand6000injuries. Afghanistanexperiencedback-to-backearthquakesof
6.2magnitudeinOctober2023,leavingover2000peopledeadandcloseto10,000injured.
Clearly,naturaldisasters,haveresultedinconsiderablelossoflifeandextensiveeconomic
damage[1].Adoptingproactivemeasureshasbecomeamajorconcernforcountriesaround
theworldlookingtoensurethattheyarepreparedtorespondtosuddendisasters[2].
Theprocessofmanagingdisastersgenerallyencompassesfourprimaryphases: mit-
igation, preparedness, response, and recovery [3]. The focus of this research is on the
‘response’ phase, which is typically characterized by three principal elements inherent
in rescue missions: location, distribution, and routing. Challenges associated with the
responsephaseandrescuemissionsarisefromvariouselements,includingcooperation
Symmetry2024,16,1080.https://doi.org/10.3390/sym16081080 https://www.mdpi.com/journal/symmetry

Symmetry2024,16,1080 2of30
betweengovernmentalandnon-governmentalentities,infrastructurebreakdowns,destruc-
tionoftransportationpaths,andacriticallackofemergencyresources[4–7]. Suchelements
mightgreatlyaffectdecisionsregardingemergencyrescues,possiblyresultinginthefailure
ofhumanitarianreliefoperations. Consequently,creatingadependableemergencylogistics
network(ELN)iscrucialinensuringtheefficacyofrescuestrategies,directlyimpactingthe
efficiencyofrescueoperationsandtheultimateoutcomeofhumanitarianrelief.
StudiesonELNshaveresultedintheformulationofdiversemodelsthattakeinto
accountaspectssuchasrescueexpenses[8],equity[9],thedurationoftherescue[10],and
unpredictability[11]. However,themajorityofthesestudiesconcentratedexclusivelyon
factorssuchaslocation,routing,andallocation,payingminimalattentiontoemergency
supplyloadingstrategies. Itemsforemergencyaid,includingfood,potablewater,gener-
ators,fuel,tents,andblankets,differgreatlyintheirthree-dimensionaldimensionsand
frequentlyrequireconcurrenttransporttodisasterzones,likegeneratorswithfuel,food
withwater,tentswithblankets. However,themajorityofcurrentresearchhasoverlooked
this facet of providing aid resources, resulting in a lack of understanding as to how to
efficientlyusescarcetransportationspaceduringemergencies[12,13]. Additionally,given
thatthepresentprocessofloadingandunloadinggoodspredominantlydependsonman-
uallaborandisnotunderpinnedbyscientificloadingrules,loadingschemesfrequently
dependonsubjectiveelements,suchasemployees’workexperienceandpersonalpref-
erences[14,15]. However,becauseextantresearchhasprimarilyfocusedonaspectssuch
as cost and time efficiency, it has not adequately explored the optimization of loading
schemes. Consequently,integratingloadingschemesintothedevelopmentofELNsisvital
ineliminatingcurrentresearchgapsandboostingtheoverallefficiencyandeffectivenessof
rescueoperations.
Comparedtopreviousresearch,thelocation-routingoptimizationproblemthatload-
ingschemesismorecomplex,necessitatingtheconsiderationofthedistributionofdemand
pointsamongmultipledistributioncenters,theallocationofvehiclestodemandpoints,
andthedeliveryroutesvehiclesmighttake. Furthermore,byemployingthestrategyof
compartmentalization,thearrangementofitemsinadeliverysystemisdecidedbythe
orderofdemandpointsandthethree-dimensionalofgoods. Additionally,whenproviding
humanitarian aid following disasters, it is crucial to amalgamate principles of welfare
economics to guarantee that logistics networks maximize benefits for most people [16].
Concurrently,itiscrucialfortheconstructedlogisticsnetworktomaintainutmoststability
anddependabilityinsettingssusceptibletosubsequentcalamities. Moreover,wemust
considerdisruptionstodistributioncenters,thecapacitylimitationsandexpansionofdistri-
butioncenters,anddeliverytimewindowsrequiredbydemandpointstomoreaccurately
reflectpost-disasterscenariosintherealworld.
Giventheaforementionedconditions,thispaperstudiesthehumanitarianemergency
logisticslocation-routingproblem,optimizinglocation,routing,andloadingplanswhile
adhering to three-dimensional loading and resource constraints, and aims to minimize
bothsocialcostsandtherisktothelogisticsnetwork. Theprimarycontributionsofthis
paperareasfollows:
(1) A multi-objective location-routing problem with a three-dimensional loading con-
straintsoptimizationmodelisformulated. Thismodelisuniqueinthatitoptimizes
distributioncenters,vehiclescheduling,andloadingplanswhileconsideringthree-
dimensional loading constraints, facility disruptions, capacity limitations and ex-
pansions,andtimewindowconstraintswhilebalancingsocialcosts(logisticaland
deprivationcosts)andrisktothelogisticsnetwork. Byintegratingthesetwogoals,
themodelnotonlyenhancesresourceallocationefficiencybutalsostrengthensthe
reliabilityoftheELN.
(2) Amulti-objectivemixedgeneticalgorithm(MOGA)basedonadaptivelargeneigh-
borhoodsearch(ALNS)isproposed. ThisMOGA-ALNSemploysALNSforneigh-
borhoodsearch,withfiveremovalandinsertionoperatorsdesignedtoenhancethe
diversity and flexibility of the search process, effectively preventing convergence

Symmetry2024,16,1080 3of30
tolocaloptima. Simultaneously,itleveragestheglobalsearchcapabilityofgenetic
algorithmstoensurethediversityandcomprehensivenessofthesolutions.
The paper is organized as follows: Section 2 provides an overview of the extant
literatureonthetopic.Section3delvesintotheresearchissueandoutlinesthemathematical
model. Section4presentstheproposedsolutiontotheissue. Thenumericalexperiments
performedarereportedinSection5. Section6concludesthisstudyandsuggestsfuture
researchdirections.
2. LiteratureReview
2.1. EmergencyLogisticsNetwork
In contrast to conventional logistics systems, an ELN must account for potential
interruptionsinitsoperations. ThedesignofanELNmainlyencompassestwoelements:
infrastructure(e.g.,distributioncenters,hospitals,andshelters)andpathways. AnELN
primarily focuses on optimizing the facility location and distribution route. Scholarly
worksontheoptimizationoffacilitylocationshaveprimarilyconcentratedonidentifying
the ideal quantity and placement of facilities for construction, while choices regarding
distributionpathshavemainlybeenassociatedwiththedesignoftransportationroutes.
Crafting an ELN that ensures both high efficiency in delivery and reduced costs
necessitatesthestrategicselectionofsuitablelocations[17,18]. Yangetal.[19]tackledthe
unpredictabilityofemergencyneedsandthetimingofresourcedistributionindisastersby
creatingamulti-stagefacilitylocationmodelaimedatimprovingoverallcostefficiencyand
equityandbydevisinganalgorithmbasedonBendersforbranchandbound.Menetal.[20]
formulatedamulti-objectivelocationmodelforpinpointingfacilitiesinthemanagement
ofdisastrouschainchemicalincidents. Themodeltakesintoaccountnotjustthespatial
attributes of facilities but also addresses pertinent potential hazards. A multi-objective
evolutionaryalgorithmwasdevelopedtoaddressthisissue. Wangetal.[21]developed
adistributionallyrobustoptimizationmodelforoptimizingthelocationsofdistribution
centersandbackupwarehouses,aswellasthedistributionofreliefsuppliesinanELN,by
minimizingexpectedtotalcostsandtotaldeliverytimes. Theirproposedsolutionwasa
Bendersdecomposition-basedexactalgorithm.
Somestudiesonfacilitylocationshaveconsideredthepossibilityoffacilitydisrup-
tions. Malikietal.[21]formulatedamulti-phasemodelforlocatingfacilitiesduringcrises
characterized by extremely unpredictable demands. Their goal was to reduce overall
expensesandCO emissions,suggestingacomprehensiveoptimizationstrategyutilizing
2
thenon-dominantsortinggeneticalgorithm. Wangetal.[22]tackledthecomplexissueof
locatingfacilitiesamiduncertainty,developingtwokeyfunctions: ensuringcoveragerelia-
bilityandcalculatingtheoverallcost. Inresponsetothisissue,abi-population-oriented
evolutionary algorithm was suggested. Zhang et al. [23] explored the reliable issue of
location inventory, taking into account the reciprocal interplay between failures in the
simultaneousplacementofforwardandreversedistributioncenterswithinaclosed-loop
supplychain. Thelikelihoodofinterruptionsvariedbasedonthetypesoffacilities,with
thegoalbeingtoreduceoverallexpenses. Theirsuggestionwasadecompositionapproach
basedonthedominance-basedouterapproximationalgorithm.
Numerous studies have tackled issues related to the distribution of supply routes
in urgent situations [24–26]. Molina et al. [27] presented an adaptable multi-objective
algorithm for searching large neighborhoods, aimed at reducing vehicle count, overall
travel expenses, and the greatest delay in addressing the rescue vehicle routing issue.
Khanchehzarrinetal.[28]developedadual-layereddisasterlocation-routingmodelwith
multiplegoals,takingintoaccounttherisktosupplies. Forimprovedproblem-solving,the
bi-levelmulti-objectivemodelwasconvertedintoasingle-level,single-objectivemodel
throughtheapplicationoftheepsilon-constraintmethodandKarush–Kuhn–Tuckercondi-
tions. Wangetal.[29]introducedatwo-levelemergencyvehicleroutingproblemwithtime
windowsinaclosedarea,aimingtominimizetotaloperatingcosts,totaldeliverytime,and

Symmetry2024,16,1080 4of30
thenumberofvehicles. Theydesignedamulti-objectiveALNSsegmentationalgorithmas
aproposedsolution.
2.2. IntegratingResearchonDeliveryRouteOptimizationandThree-DimensionalPacking
Constraints(VRPTDLCs)
Duetothelimitedresearchontheintegrationofthelocation-routingproblem(LRP)
andthree-dimensionalpackingconstraints,thissectionanalyzesthecurrentstatusofre-
searchonLRP-relatedissues,primarilythevehicleroutingproblemwiththree-dimensional
loadingconstraints(VRPTDLCs). Whetherinemergencyreliefscenariosorinthedaily
logisticsindustry,thetypesofmaterialsfordistributionareextremelydiverse. Thisalso
meansthattheirsizesareinevitablydifferent. Becauseasmanygoodsaspossiblewith
givensizesandweightsmustbeloadedintoavehiclebeforedeliverytoservemoredemand
points,itisnecessarytodeterminethroughanoptimizationprocesswhetherthesegoods
canbesuccessfullyloaded. Reiletal.[30]studiedavehicleroutingproblem,considering
vehiclereturntrips,timewindows,and3Dpackingconstraints. Theycreatedabi-objective
model aimed at reducing the quantity of transport vehicles and shortening the travel
distance. Theresearchersformulatedahybridmethodthatmergestaboosearchwithan
evolutionaryalgorithm,targetingtheimprovementofvehicleroutingandfreightloading
strategies. Furthermore,Göçmenetal.[31]presentedthechallengeofselectingroutesfora
multimodaltransportnetwork,takingintoaccountthree-dimensionalloadinglimitations.
To address this issue, they developed a mixed-integer programming model, aiming to
reducebothtransportationexpensesandthevehiclecount. Specifically,theyemployeda
mixedalgorithm,integratingk-means,machinelearning,andgeneticalgorithms.
Intheexaminationofthree-dimensionalpackingconstraints,variouspracticalloading
considerations are commonly taken into account. These include the necessity for load
stability,therequirementforaminimumsupportarea,andtheadherencetolast-in-first-
out (LIFO) loading principles [32]. In addition, some variants of VRPTDLC have also
attractedscholarlyattention.Männeletal.[33]studiedapickupanddeliveryrouteproblem
that considers three-dimensional packing constraints with the objective of minimizing
transportationdistance. Acombinationoftreesearchandlargeneighborhoodsearchwas
employed in their hybrid algorithm to effectively address and optimize the issue. In a
separatestudy,Rajaeietal.[34]tackledamultifacetedreal-worldchallengethatmerges
thevehicleroutingissuewiththeuseofheterogeneousvehiclesandthree-dimensional
packinglimitations. Theydevelopedaheuristicalgorithmbasedoncolumngenerationto
determinethemostcost-effectivesetoftransportationroutes.
2.3. CompartmentalizationStrategiesforVehicles
Intherealmofpracticaltransport,dividingvehiclecompartmentsintomultiplesec-
tionsforcarryingdiversegoodsisseenasanefficientapproachtohandlingthedistribution
of goods of varying types and sizes [35]. This approach essentially involves segment-
ing a vehicle’s load area into a finite number of sections, each designated for a specific
kindofcargo. Historically,vehiclecompartmentalizationhasbeenappliedinscenarios
suchasthetransportationofvarioustemperature-sensitivefooditems(e.g.,frozen,fresh,
andambientproducts)tosupermarkets[36],thedeliveryofassortedpetroleumproducts
(e.g.,dieselandgasoline)tofuelstations[37],orthesegregationofdifferentkindsofwaste
(e.g.,coloredglasswaste)[38,39]. Yahyaouietal.[37]exploredascenariowhereaspecial-
izedfleetwithnumerouscompartmentalspaceswasdesignedtotransportvariedtypesof
fuelfromacentralwarehousetoseveralgasstations.ZbibandLaporte[38]investigatedthe
applicationofcompartmentalizationinroadsidewastecollection,creatingamathematical
model to reduce travel costs, and, ultimately, putting forth a tri-stage algorithm. Yang
etal.[39]devisedacompartmentalizationapproachforcity-widesolidwastecollection,
proposingthateachvehicle’scapacitybedividedintolimitedsections,eachtailoredfora
specificwastetype. Theirfindingsindicatedthatcostefficienciesincreasewithanincrease
inthenumberofcompartments. Tosumup,vehiclecompartmentalizationofferssubstan-

Symmetry2024,16,1080
5of30
tialbenefitsindistributingdiversegoods,yetitsapplicationinhumanitarianemergency
logisticshaslackedextensiveacademicexploration.
Inordertofurtherelucidatethedifferencesbetweenthisstudyandexistingresearch,
andtodefinethecontributionsofthisresearch,Table1liststherelevantresearchworks
andtheirmaincharacteristics. Bysummarizingtherelevantstudies,thisreviewyielded
thefollowinginsights: (1)Currently,mostresearchonhumanitarianemergencylogistics
hasfocusedoncostandtime;however,inpractice,thereliabilityofdistributionnetworks
constructedforemergencyresourcedistributioniscrucial;(2)Thereisagapintheliterature
onfacilitylocation,distributionroute,andloadingschemeoptimization,resultingininsuf-
ficientattentiontotheintersectingissuesconnectingthesethreeaspects;(3)Metaheuristic
algorithmshavebeenwidelyandsuccessfullyusedtoaddressrelatedissuesintheVRPT-
DLC;(4)Giventheinefficiencyoftraditionalmetaheuristicalgorithmsinsolvingcomplex
problems,scholarshavegenerallydesignedhybridalgorithmsaspotentialsolutions.
Table1.SummaryoftheliteraturepertainingtoELN.
Vulnerable
KeyConstraints
Section
| Reference | Location | Allocation | Objective |               |           |         | Solution |
| --------- | -------- | ---------- | --------- | ------------- | --------- | ------- | -------- |
|           |          |            |           |               | Fac. Fac. | 3D      |          |
|           |          |            |           | Facility Link |           | TWs     |          |
|           |          |            |           |               | Cap Exp   | Loading |          |
Totalcost
| Mohammadietal. | √   | √   | Makespan | √   | √   |     |     |
| -------------- | --- | --- | -------- | --- | --- | --- | --- |
Exa
| (2020)[40] |     | Transportcostbounds |     |     |     |     |     |
| ---------- | --- | ------------------- | --- | --- | --- | --- | --- |
variation
| Weietal. | √   | √   | Totalcost |     | √   | √   |     |
| -------- | --- | --- | --------- | --- | --- | --- | --- |
Met
| (2020)[41]        |     |     | Demandsatisfaction |     |     |     |     |
| ----------------- | --- | --- | ------------------ | --- | --- | --- | --- |
|                   | √   | √   |                    |     | √   |     |     |
| Lietal.(2020)[42] |     |     | Totalcost          |     |     |     | Exa |
| Sunetal.          | √   | √   | Totalcost          |     |     |     |     |
Exa
| (2021)[43] |     |     | Injuryseverityscore |     |     |     |     |
| ---------- | --- | --- | ------------------- | --- | --- | --- | --- |
| Gaoetal.   |     | √   | Fairness            | √   | √   |     |     |
Exa
| (2021)[44]   |     |     | Makespan  |     |     |     |     |
| ------------ | --- | --- | --------- | --- | --- | --- | --- |
| Abazarietal. | √   | √   | Totalcost |     |     |     |     |
Met
| (2021)[45] |     |     | Makespan |     |     |     |     |
| ---------- | --- | --- | -------- | --- | --- | --- | --- |
| Chengetal. |     | √   |          |     | √   |     |     |
|            |     |     | Fairness |     |     |     | Exa |
(2021)[46]
| Alemetal. | √   | √   |               |     | √ √ |     |     |
| --------- | --- | --- | ------------- | --- | --- | --- | --- |
|           |     |     | Effectiveness |     |     |     | Exa |
(2021)[47]
|            | √   | √   |                    |     |     | √   |     |
| ---------- | --- | --- | ------------------ | --- | --- | --- | --- |
| Pengetal.  |     |     | Totalcost          |     |     |     |     |
| (2022)[48] |     |     | Demandsatisfaction |     |     |     | Met |
Totalcosts
| Ghasemietal. | √   | √   |                 | √   | √   |     |     |
| ------------ | --- | --- | --------------- | --- | --- | --- | --- |
|              |     |     | Maximumnumberof |     |     |     | Met |
(2022)[49]
unsatisfieddemands
| Vosooghietal. | √   | √   | Totalcost |     | √ √ |     |     |
| ------------- | --- | --- | --------- | --- | --- | --- | --- |
Met
| (2022)[50]     |     |     | Responsetime |     |     |     |     |
| -------------- | --- | --- | ------------ | --- | --- | --- | --- |
| Bayraktaretal. | √   | √   |              |     |     |     |     |
|                |     |     | Totalcost    |     |     |     | Met |
(2022)[51]
| Wangetal.  | √   | √   | Totalcost | √   | √   |     |     |
| ---------- | --- | --- | --------- | --- | --- | --- | --- |
| (2023)[52] |     |     | Makespan  |     |     |     | Exa |
| Mengetal.  | √   | √   | Totalcost | √ √ |     |     |     |
Exa
| (2023)[10] |     |     | Makespan  |     |     |     |     |
| ---------- | --- | --- | --------- | --- | --- | --- | --- |
| Yangetal.  | √   | √   | Totalcost |     | √   |     |     |
Exa
| (2023)[19] |     |     | Fairness |     |     |     |     |
| ---------- | --- | --- | -------- | --- | --- | --- | --- |
| Wangetal.  | √   | √   | Timecost | √   | √   |     |     |
Heu
| (2023)[9]      |     | Quantityofshortsupplies |           |     |     |     |     |
| -------------- | --- | ----------------------- | --------- | --- | --- | --- | --- |
| Sheikholeslami | √   | √                       | Totalcost |     | √   |     |     |
Met
| etal.(2023)[53]   |     | Coverageofthenetwork    |           |     |     |     |      |
| ----------------- | --- | ----------------------- | --------- | --- | --- | --- | ---- |
|                   | √   | √                       |           | √   |     |     |      |
| Lietal.(2023)[54] |     | Totalcostintheworstcase |           |     |     |     | Heu  |
| Zhangetal.        | √   | √                       |           |     | √   |     |      |
|                   |     |                         | Totalcost |     |     |     | Meta |
(2023)[11]
| Yangetal. | √   | √   |           | √   | √   |     |     |
| --------- | --- | --- | --------- | --- | --- | --- | --- |
|           |     |     | Totalcost |     |     |     | Exa |
(2024)[55]
|           | √   | √   | Totalcost | √ √ | √ √ | √ √ |     |
| --------- | --- | --- | --------- | --- | --- | --- | --- |
| Thisstudy |     |     |           |     |     |     | Met |
Riskofnetwork
Note: Fac. Cap=Facilitycapaicity,Fac. Exp=Facilityexpansion,TWs=Timewindows,Exa=Exact,Met=
Metaheuristic,Heu=Heuristic.

Symmetry2024,16,1080 6of30
Giventheabove,thispaperproposesamulti-objectivelocation-routingproblemmodel
forhumanitarianemergencylogisticsintheeventoffacilitydisruptionsinnaturaldisaster
scenarios. Thismodeltakesintoaccounttheuniquechallengesassociatedwithdisaster
environments,suchasthelocationofdistributioncenters,vehiclerouting,andthethree-
dimensionalpackingofreliefsupplies. Additionally,ahybridalgorithmcomposedofan
improvedALNSalgorithmandageneticalgorithmisdesignedtosolvethisproblem.
3. ModelFormulation
3.1. ProblemDescription
TheELNinthisstudycomprisesasetofdemandpoints,multiplecandidatedistribu-
tioncenterswithcapacitylimits,andinterconnectedroadways. Eachdemandpointhasa
specificdeliverytimewindow,deviationsfromwhichincurpenalties. Thesupplyneedsat
thesedemandpointsarediverse,witheachitemhavingwell-definedattributes. Despite
capacitylimitations,thedistributioncentersthedistributioncenterscanundergoacertain
degreeofcapacityexpansion. Post-earthquake,theoperationofsomedistributioncenters
maybedisrupted, meaningthesedistributioncenterscannotbeconsideredinlocation-
allocation. Additionally, theriskfromsecondarynaturaldisasters, suchasaftershocks,
continuestoaffectboththeoperationaldistributioncentersandroadways.
In the optimization of cargo loading, a carriage segmentation strategy is adopted
forefficiency. Thespaceinavehicleisdividedintocompartmentsfordifferentmaterial
types. Whilemeetingthree-dimensionalloadingconstraints,goodsofthesamecategory
are placed in the same carriage according to the LIFO principle while adhering to the
deliverysequenceofthedemandpoints.
Inpractice,theconstructionofELNsneedstoconsidermultiplefactors. Socialand
deprivationcostscanindirectlyreflecttheefficiencyoftheentireemergencylogisticssystem.
Therefore,thismodelaimstominimizetotalrescuetransportationcosts(includinglocation,
expansion, transportation, vehicleusage, andtimepenalty-relatedcosts). Additionally,
given the risks of facility interruption and road damage, choosing a lower-risk ELN is
vital. Anetworkthatdoesnotconsiderriskvaluesmightleadtoseverelossesincases
of secondary disasters. Thus, this study aims to minimize both risk and total cost in
location-routingschemes.
Toillustrate,Figure1showsanexamplewithfourdistributioncenters(A,B,C,and
D)andninedemandpoints. Post-earthquake, CenterBisdisrupted, leavingA,C,and
D.CentersAandCarechosenforsupplydistribution. However,theoriginalcapacityof
CenterCisinsufficientinfulfillingthedemandvolumeofthedemandpoints,necessitating
acertaindegreeofcapacityexpansion. Thefinalresultispresentedasthelocation-routing
schemedepictedinFigure1. Figure2presentsafeasibleloadingplanforthetransport
route2-1-9inFigure1.
3.2. Symbols
G = (V,A) is an undirected network, where V is the set of nodes consisting of
a subset I of candidate distribution center locations and a subset J of geographically
dispersed demand points; A = {(i,j)|i,i∈V,i ̸= j} is the set of arcs connecting every
pairofnodesinV;K = {k|k =1,2,···h}isthesetofavailabledistributionvehicles;and
S = {s|s =1,2,··· ,p}isasetofscenarios,eachscenariospecifyingasetofsimultaneously
disrupteddistributioncenters. TableA1providestheparametersanddecisionvariables
requiredfortheformulatedmathematicalmodel.

Symmetry 2024, 16, x FOR PEER REVIEW 7 of 34
placed in the same carriage according to the LIFO principle while adhering to the delivery
sequence of the demand points.
In practice, the construction of ELNs needs to consider multiple factors. Social and
deprivation costs can indirectly reflect the efficiency of the entire emergency logistics sys-
tem. Therefore, this model aims to minimize total rescue transportation costs (including
location, expansion, transportation, vehicle usage, and time penalty-related costs). Addi-
tionally, given the risks of facility interruption and road damage, choosing a lower-risk
ELN is vital. A network that does not consider risk values might lead to severe losses in
cases of secondary disasters. Thus, this study aims to minimize both risk and total cost in
location-routing schemes.
To illustrate, Figure 1 shows an example with four distribution centers (A, B, C, and
D) and nine demand points. Post-earthquake, Center B is disrupted, leaving A, C, and D.
Centers A and C are chosen for supply distribution. However, the original capacity of
Center C is insufficient in fulfilling the demand volume of the demand points, necessitat-
ing a certain degree of capacity expansion. The final result is presented as the location-
Symmetry2024,16,1080 routing scheme depicted in Figure 1. Figure 2 presents a feasible 7looaf3d0ing plan for the
transport route 2-1-9 in Figure 1.
Symmetry 2024, 16, x FOR PEER REVIEW 8 of 34
Figure1.Illustrationoftheconsideredproblem.
Figure 1. Illustration of the considered problem.
Figure2.FeasibleloadingschemeforrouteinFigure1.
Figure 2. Feasible loading scheme for route in Figure 1.
3.3. EmergencyLogisticsNetworkRiskMeasurementFormula
3.2. Symbols
WangandSun[56]definedtheformulaformeasuringtheriskofELNsas:
𝐺 =(𝑉,𝐴) is an undirected network, where 𝑉 is the set of nodes consisting of a sub-
set 𝐼 of candidateR idskis=tribPurotiboanb iclieintyt(ePr )lo×caVtiuolnens raanbidli tay (sVub)s×etL o𝐽 s so(fL )geographically d(i1s)-
persed demand points; 𝐴={(i,𝑗)|i,i∈𝑉,𝑖 ≠𝑗} is the set of arcs connecting every pair of
w
n
h
o
e
d
r
e
e
s
P
in
s y𝑉m
;
b𝐾ol=ize{s𝑘|t𝑘he=li1k,e2l,i⋯hoℎo}d
i
o
s
f
t
r
h
is
e
k
s
d
et
u r
o
i
f
n g
av
h
a
u
il
m
ab
a
l
n
e
i t
d
a
i
r
s
i
t
a
r
n
ib
a
u
i
t
d
io
,
n
ta k
v
i
e
n
h
g
ic
i
l
n
e
t
s
o
;
a
a
c
n
c
d
o u𝑆n=t
f{a
𝑠
c|t
𝑠
or
=
s
1
su
,2
c
,
h
⋯
a
,
s 𝑝}r o
i
a
s
d
a
d
se
e
t
s t
o
r
f
u
s
c
c
t
e
io
n
n
ar
,
i
r
o
o
s
u
,
t
e
e
ac
i
h
n t
s
r
c
ic
e
a
n
c
a
y
r
,
io
c l
s
im
pe
a
c
t
i
i
f
c
yi
c
n
o
g
n d
a
i
s
t
e
io
t
n
o
s
f
,
s
a
im
nd
ul
t
t
h
an
e
e
c
o
h
u
a
s
n
ly
ce
d
o
is
f
-
a subsequent disaster. V symbolizes the likelihood of substantial losses following the
rupted distribution centers. Table A1 provides the parameters and decision variables re-
aforementionedrisks,influencedbyfactorssuchasgeographicposition,populationand
quired for the formulated mathematical model.
3.3. Emergency Logistics Network Risk Measurement Formula
Wang and Sun [56] defined the formula for measuring the risk of ELNs as:
𝑅𝑖𝑠𝑘=𝑃𝑟𝑜𝑏𝑎𝑏𝑖𝑙𝑖𝑖𝑡𝑦(𝑃)(cid:3400)𝑉𝑢𝑙𝑒𝑛𝑟𝑎𝑏𝑖𝑙𝑖𝑡𝑦(𝑉)(cid:3400)𝐿𝑜𝑠𝑠(𝐿) (1)
where 𝑃 symbolizes the likelihood of risk during humanitarian aid, taking into account
factors such as road destruction, route intricacy, climatic conditions, and the chance of a
subsequent disaster. 𝑉 symbolizes the likelihood of substantial losses following the
aforementioned risks, influenced by factors such as geographic position, population and
building density, traffic volume, and the significance and worth of the transported mate-
rials. 𝐿 denotes both the immediate and secondary impacts of the risk, encompassing fi-
nancial damages and fatalities. Within Wang and Sun’s [56] particular research frame-
work, the comprehensive risk examined is bifurcated into two segments: the hazard en-
countered during transit and the hazard associated with road upkeep. However, in actual
relief operations, aside from the various risks on the road, there is also the risk of second-
ary disasters occurring at distribution centers. In view of this, this study modified the
above formula to better fit real-world scenarios:

Symmetry2024,16,1080 8of30
buildingdensity,trafficvolume,andthesignificanceandworthofthetransportedmaterials.
Ldenotesboththeimmediateandsecondaryimpactsoftherisk,encompassingfinancial
damagesandfatalities. WithinWangandSun’s[56]particularresearchframework,the
comprehensiveriskexaminedisbifurcatedintotwosegments: thehazardencountered
during transit and the hazard associated with road upkeep. However, in actual relief
operations, aside from the various risks on the road, there is also the risk of secondary
disastersoccurringatdistributioncenters. Inviewofthis,thisstudymodifiedtheabove
formulatobetterfitreal-worldscenarios:
(cid:34) (cid:35)
Risk = ∑ P ∑ Ps·Ps·λS·xs+ ∑ ∑ ∑ Ps ·pPs ·λS ·ys (2)
s 1i 2i 1i i 1ij 2ij 2ij ijk
s∈S i∈I i∈Aj∈Ak∈K
wherePs·Ps·λS representstheriskofsecondarydisastersoccurringatdistributioncenters,
1i 2i 1i
andPs ·Ps ·λS representsrisksthatmightoccurduringthedistributiontransportation
1ij 2ij 2ij
processinthehumanitarianreliefchain.
3.4. MathematicalModel
The objective function serves as the foundation for determining how conflicting
objectivesarecoordinatedandhowscarceresourcesareoptimallyallocated.Ifamodeldoes
notestablisharelationshipthatreflectstherealsystem,itsabilitytogeneratereasonable
recommendations is compromised. Moreover, reducing logistics costs to a minimum
withoutconsideringthemagnitudeofdistributionplanriskscanhaveadverseeffectson
thepeopleinthedisaster-affectedarea. Therefore,thismodelsimultaneouslyconsiders
theminimizationofthetotalcost(sitelocationcostofdistributioncenters,expansioncosts,
transportationcosts,vehicleusagecosts,andtimepenaltycosts)andtheriskvalueofthe
logisticsnetwork. Subsequently,thefollowingoptimizationmodelisformulated:
∑ xs·γ + ∑ δs·e + ∑ ∑ ∑ ys ·f + ∑ ∑ ∑ ys ·δ ·τ 
i i i i ijk ijk ij
MinZ = ∑ P i∈I (cid:110) i∈I (cid:16) i∈Ij∈Jk∈K (cid:17) i∈A (cid:16) j∈Ak∈K (cid:17)(cid:111)  (3)
1 s +∑ ∑ φe·max Ts −ts ,0 +φe·max ts −Ts,0 
s∈S j 1j jk j jk 2j
j∈Jk∈K
(cid:34) (cid:35)
MinZ = ∑ P ∑ Ps·Ps·λS·xs+ ∑ ∑ ∑ Ps ·Ps ·λS ·ys (4)
2 s 1i 2i 1i i 1ij 2ij 2ij ijk
s∈S i∈I i∈Aj∈Ak∈K
∑ zs =1,∀j ∈ J,∀s ∈ S (5)
ij
i∈I
∑ ∑ ys =1,∀j ∈ J,∀s ∈ S (6)
ijk
i∈Vk∈k
ys ≤ xs,∀i ∈ I,∀j ∈ J,∀k ∈ K,∀s ∈ S (7)
ijk i
∑∑ ys ≥ xs,∀i ∈ I,∀s ∈ S (8)
ijk i
j∈Jk∈k
∑∑ ys ≤1,∀k ∈ K,∀s ∈ S (9)
ijk
i∈Ij∈J
∑ ys = ∑ ys ,∀i ∈V,∀k ∈ K,∀s ∈ S (10)
ijk ijk
j∈V j∈V
∑ ys = Ωs ,∀i ∈ I,∀k ∈ K,∀s ∈ S (11)
ijk ik
j∈J
∑∑ ys ≤ |S|−1,∀i ∈ I,∀k ∈ K,∀s ⊆V (12)
ijk
i∈Ij∈J
β ·xs+δs ≤ µ,∀i ∈ I,∀s ∈ S (13)
i i i i

Symmetry2024,16,1080 9of30
∑ ∑ Qs ·ms ·Ωs ≤β ·xs+δs,∀i ∈ I,∀s ∈ S (14)
kd kd ik i i i
k∈Kd∈Dk
∑ qs ·m s = Qs ,∀k ∈ K,∀s ∈ S (15)
kd kd kd
d∈Dk
∑ Qs ≤O,∀k ∈ K,∀s ∈ S (16)
kd
d∈Dk
∑ ls ·ws ·h s ·ms = σs ,∀k ∈ K,∀s ∈ S (17)
kdc kdc kdc kd kd
d∈Dk
∑ σs ≤ B,∀k ∈ K,∀s ∈ S (18)
kd
d∈Dk
(cid:16) (cid:17) s
ts = ts +ψs +δ /ν ·y ,∀i ∈ I,∀s ∈ S (19)
jk ik jk ij
ijk
∑ ηs = ∑ ηs + ∑ qs ·m s ,∀j ∈ J,∀k ∈ K,∀s ∈ S (20)
ijk jik kd kdj
i∈V i∈V d∈Dk
∑ ms ·εs = ms ,∀k ∈ K,d ∈ D ,∀s ∈ S (21)
kdj kj kd k
j∈J
x ≥0,∀k ∈ K,∀d ∈ D ,∀j ∈ J,∀s ∈ S,∀c ∈C,1≤ u ≤ mk (22)
Ckdjus k d
y ≥0,∀k ∈ K,∀d ∈ D ,∀j ∈ J,∀s ∈ S,∀c ∈C,1≤ u ≤ mk (23)
Ckdjus k d
z ≥0,∀k ∈ K,∀d ∈ D ,∀j ∈ J,∀s ∈ S,∀c ∈C,1≤ u ≤ mk (24)
Ckdjus k d
layers ·hk ≤ h ,∀k ∈ K,∀d ∈ D ,∀s ∈ S,∀c ∈C (25)
kd c d k
rows ·lk ≤ l ,∀k ∈ K,∀d ∈ D ,∀s ∈ S,∀c ∈C (26)
kd c d k
columns ·wk ≤ w ,∀k ∈ K,∀d ∈ D ,∀s ∈ S,∀c ∈C (27)
kd c d k
x −x ≥ hk,∀k ∈ K,∀d ∈ D , ∀s ∈ S,∀c ∈C,∀i ≤ j, C ∈ M (28)
Ckdjus Cskdju c k kdjus
y −y ≥ lk,∀k ∈ K,∀d ∈ D ,∀s ∈ S,∀c ∈C,∀i ≤ j, C ∈ N (29)
Ckdjus Cskdju c k kdjus
z −z ≥ wk,∀k ∈ K,∀d ∈ D ,∀s ∈ S,∀c ∈C,∀i ≤ j, C ∈ N (30)
Ckdjus Cskdju c k kdjus
xs = {0,1},i ∈ I,s ∈ S (31)
i
ys = {0,1},i ∈ I,j ∈ J,k ∈ K,s ∈ S (32)
ijk
zs = {0,1},i ∈ I,j ∈ J,s ∈ S (33)
ij
εs = {0,1},k ∈ K,d ∈ D ,j ∈ J,s ∈ S (34)
kj k
Ωs = {0,1},i ∈ I,k ∈ K,s ∈ S (35)
ik
ζs ≥0,i ∈ I,s ∈ S (36)
i
whereEquation(3)representsthetotalcostofthelogisticsnetwork,includingsiteselection
costsfordistributioncenters,expansioncostsfordistributioncenters,vehicletransporta-
tion costs, vehicle usage costs, and time penalty costs. Equation (4) represents the risk
value of the logistics network, consisting of the risk values of distribution centers and
distributionpaths. Constraint(5)ensuresthateachdemandpointisservedbyonlyone
distributioncenter. Constraint(6)ensuresthateachdemandpointisservicedonlyonce.
Constraints(7)and(8)ensurethatopendistributioncentershavevehiclesdepartingand
thatvehiclesareonlydepartingfromtheopendistributioncenters. Constraint(9)ensures
thateachvehicleisscheduledforadeliveryserviceatmostonce. Constraint(10)isaflow
conservationconstraint. Constraint(11)indicatesthevehicle’saffiliationwithdistribution

Symmetry2024,16,1080 10of30
centers. Constraint(12)eliminatessubcycles. Constraint(13)ensuresthattheexpanded
capacitydoesnotexceedthemaximumallowedexpansioncapacity.Constraint(14)ensures
thatthetotaldemandquantityfordemandpointsservicedbyadistributioncenterdoes
notexceeditscapacity. Constraints(15)and(16)calculatetheweightofgoodsloadedon
vehiclesandensurethattheweightdoesnotexceedthemaximumloadcapacityofthe
vehicles. Constraints(17)and(18)calculatethevolumeofgoodsloadedonvehiclesand
ensurethatthevolumedoesnotexceedthemaximumvolumecapacityofthevehicles.
Constraint(19)calculatesthearrivaltimeofvehiclesatdemandpoints. Constraint(20)
specifiesthequantityofgoodsloadedfrompointitopoint j. Constraint(21)calculates
thequantityofgoodsloadedineachcompartmentofthevehicle. Constraints(22)–(24)
guaranteethatallgoodsarepositionedwithinthevehicle’sconfinesanddonotsurpassthe
vehicle’slimits. Constraints(25)–(27)mandatethatgoodsareallocatedtotheirdesignated
compartments, adhering to compartmental boundaries. Constraints (28)–(30) are LIFO
constraints,meaningthatgoodsservicedlateratdemandpointscannotbeplacedontopof
goodsservicedearlieratthesamedemandpointsandshouldnotbeplacedbeforegoods
servicedearlieratotherdemandpoints. Finally,Constraints(31)–(36)limittherangeof
decisionvariables.
4. SolutionMethod
Insolvingmulti-objectiveoptimizationissues,variousPareto-optimaloutcomesare
typically produced, and the main goal in solving them is the identification and charac-
terization of a diverse set of Pareto-optimal solutions. Algorithms based on evolution
are recognized for their proficiency in navigating solution realms, making them partic-
ularly suitable for generating a variety of Pareto-optimal solutions in a single iteration.
Researchhasrepeatedlyshownthesuccessofevolutionaryalgorithmsinaddressingin-
tricatemulti-objectiveoptimizationchallenges[57,58]. Furthermore,theALNSalgorithm
hasdemonstratedsuperioreffectivenessoverconventionaltechniquesinaddressingvari-
ousvehicleroutingissues[59]. Consequently,thisdocumentoutlinesthecreationofthe
MOGA-ALNStoaddresstheissueunderstudy.
4.1. MainFrameworkoftheAlgorithm
ThemainframeworkoftheMOGA-ALNSisshowninFigure3. Thealgorithm’smain
structureisderivedfromgeneticalgorithms,andALNSisusedtofurtheroptimizethe
routepartineachiteration. Finally, theloadingplanforgoodsisdeterminedbasedon
the service sequence of each demand point. Detailed explanations are provided in the
subsequentsections.
4.2. RepresentationofSolutions
ThereareNdistributioncentersandMdemandpoints. Theindicesforalldistribution
centersareintegersof1, 2, ..., N, andtheindicesforalldemandpointsareintegersof
1,2,..., M.Eachsolutionisrepresentedbyatwo-dimensionalstringdividedintotwoparts:
AandB.ThesequencesoftheAandBpartscorrespondonetoone,whereeachpositionin
thesesequencesrepresentsaspecificdemandpoint. Thiscorrespondenceensuresthatthe
allocationanddeliverysequencesateachdemandpointareclearlydefined.
TheApart, anintegerstring, indicateseachopendistributioncenteranditscorre-
spondingdemandpoints. Forinstance,asshowninFigure4,DistributionCenter1serves
demandpoints1,3,4,and7,whileDistributionCenter2serves2,5,and6. Ifadistribution
center’s total distribution exceeds its capacity but not its maximum expansion limit, it
needsexpansion. However,exceedingthislimitmakesthesolution’sobjectivefunction
valueextremelylarge,disqualifyingitfromfurtherconsideration.
TheBpartconsistsoffloating-pointnumbersbetween0and1,assignedrandomlyto
eachsequenceposition. Sortingthesenumbersinascendingorderdeterminesthedelivery
sequence. ThiscombinationofAandBpartsclearlyindicatestheorderofdeliveriesfor
eachdistributioncenter. Forexample,Figure4showsDistributionCenter1dispatching

Symmetry 2024, 16, x FOR PEER REVIEW 12 of 34
the quantity of goods loaded in each compartment of the vehicle. Constraints (22)–(24)
guarantee that all goods are positioned within the vehicle’s confines and do not surpass
the vehicle’s limits. Constraints (25)–(27) mandate that goods are allocated to their desig-
nated compartments, adhering to compartmental boundaries. Constraints (28)–(30) are
LIFO constraints, meaning that goods serviced later at demand points cannot be placed
on top of goods serviced earlier at the same demand points and should not be placed
before goods serviced earlier at other demand points. Finally, Constraints (31)–(36) limit
the range of decision variables.
4. Solution Method
In solving multi-objective optimization issues, various Pareto-optimal outcomes are
typically produced, and the main goal in solving them is the identification and character-
ization of a diverse set of Pareto-optimal solutions. Algorithms based on evolution are
recognized for their proficiency in navigating solution realms, making them particularly
suitable for generating a variety of Pareto-optimal solutions in a single iteration. Research
has repeatedly shown the success of evolutionary algorithms in addressing intricate
multi-objective optimization challenges [57,58]. Furthermore, the ALNS algorithm has
demonstrated superior effectiveness over conventional techniques in addressing various
vehicle routing issues [59]. Consequently, this document outlines the creation of the
MOGA-ALNS to address the issue under study.
4.1. Main Framework of the Algorithm
Symmetry2024,16,1080 11of30
The main framework of the MOGA-ALNS is shown in Figure 3. The algorithm’s main
Symmetry 2024, 16, x FOR PEER REVIEsWtr ucture is derived from genetic algorithms, and ALNS is used to further optim13i zoef 3th4 e
route part in each iteration. Finally, the loading plan for goods is determined based on the
vehiclestoservedemandpointsintheorderof3-1-4-7,andCenter2intheorderof6-2-5to
service sequence of each demand point. Detailed explanations are provided in the subse-
deliversuppliestotheirrespectivedemandpoints.
4.q2u. eRnept rseescetniotantsio. n of Solutions
There are 𝑁 distribution centers and 𝑀 demand points. The indices for all distribu-
tion centers are integers of 1, 2, …, 𝑁, and the indices for all demand points are integers of
1, 2, …, 𝑀. Each solution is represented by a two-dimensional string divided into two
parts: A and B. The sequences of the A and B parts correspond one to one, where each
position in these sequences represents a specific demand point. This correspondence en-
sures that the allocation and delivery sequences at each demand point are clearly defined.
The A part, an integer string, indicates each open distribution center and its corre-
sponding demand points. For instance, as shown in Figure 4, Distribution Center 1 serves
demand points 1, 3, 4, and 7, while Distribution Center 2 serves 2, 5, and 6. If a distribution
center’s total distribution exceeds its capacity but not its maximum expansion limit, it
needs expansion. However, exceeding this limit makes the solution’s objective function
value extremely large, disqualifying it from further consideration.
The B part consists of floating-point numbers between 0 and 1, assigned randomly to
each sequence position. Sorting these numbers in ascending order determines the delivery
sequence. This combination of A and B parts clearly indicates the order of deliveries for
each distribution center. For example, Figure 4 shows Distribution Center 1 dispatching
vehicles to serve demand points in the order of 3-1-4-7, and Center 2 in the order of 6-2-5
to deliver supplies to their respective demand points.
This work adopts vehicle usage rules as shown in Figure 4 to optimize the number
of vehicles utilized. The methodology involves sequentially assigning demand points to
vehicles for delivery. When a vehicle reaches its maximum capacity, an additional vehicle
is allocated for the remaining demand points. Figure 5 elaborates on this process by de-
coding Route 1 from Figure 4 as a case study. Specifically, Route 1 is bifurcated into two
separate delivery paths in accordance with the vehicle usage rules, as depicted in Figure
5. The subsequent phase involves strategically determining the loading sequence of
goods, aligning with the established delivery order for each route. This effectively orches-
Figure 3. Flowchart of MOGA-ALNS.
traFtiegsu rtehe3. dFeloliwvechryar atnofdM loOaGdAin-gA LscNhSe.me, as visually represented in Figure 5.
FiFgiugruer 4e. 4Il.l
I
u
l
s
lu
tr
s
a
tr
ti
a
o
t
n
io
o
n
f
o
t
f
h
t
e
h
s
e
o
s
lu
ol
t
u
io
t
n
io
.
n.
ThisworkadoptsvehicleusagerulesasshowninFigure4tooptimizethenumber
of vehicles utilized. The methodology involves sequentially assigning demand points
to vehicles for delivery. When a vehicle reaches its maximum capacity, an additional
vehicleisallocatedfortheremainingdemandpoints. Figure5elaboratesonthisprocessby
decodingRoute1fromFigure4asacasestudy. Specifically,Route1isbifurcatedintotwo
separatedeliverypathsinaccordancewiththevehicleusagerules,asdepictedinFigure5.
Thesubsequentphaseinvolvesstrategicallydeterminingtheloadingsequenceofgoods,
aligningwiththeestablisheddeliveryorderforeachroute. Thiseffectivelyorchestratesthe
deliveryandloadingscheme,asvisuallyrepresentedinFigure5.

Symmetry 2024, 16, x FOR PEER REVIEW 14 of 34
S ymmetry2024,16,1080 12of30
Figure 5. Decoding process of Route 1 in Figure 4.
Figure5.DecodingprocessofRoute1inFigure4.
4.3. Population Initialization
4.3. PopulationInitialization
In this work, 𝑁 individuals are generated as the initial population to participate in
Inthiswork,Nindividualsaregeneratedastheinitialpopulationtoparticipateinthe
the subsequent optimization process. The method for generating individuals is as follows:
subsequentoptimizationprocess. Themethodforgeneratingindividualsisasfollows:
(1) When considering the distance between demand points and distribution centers, the
(1) Whenconsideringthedistancebetweendemandpointsanddistributioncenters,the
probability function [60] for assigning all demand points to distribution centers is
probabilityfunction[60]forassigningalldemandpointstodistributioncentersis
given by Equation (37), where 𝑑(cid:0)(𝐷,𝐶)(cid:1) represents the Euclidean distance between
givenbyEquation(37),whered D(cid:3036), C(cid:3037) representstheEuclideandistancebetween
i j
the distribution center 𝑖 and demand point 𝑗(cid:0) , 𝑑(cid:3364)(cid:3364)((cid:3364)(cid:3364)𝐷(cid:3364)(cid:3364),(cid:1) (cid:3364)𝐶(cid:3364)(cid:3364)(cid:3364)) signifies the average dis-
thedistributioncenterianddemandpointj,d D, C (cid:3115)signifiestheaveragedistance
j
tance from demand point 𝑗 to all distribution centers, with 𝑛 representing the total
fromdemandpointjtoalldistributioncenters,withnrepresentingthetotalcountof
count of demand points. The probability of assigning demand point 𝑗 to distribution
demandpoints. Theprobabilityofassigningdemandpointjtodistributioncenteriis
center 𝑖 is calculated as follows:
calculatedasfollows:
(cid:110) (cid:0) (cid:1) (cid:0) (cid:1) (cid:111)
𝑃P(cid:3435) (cid:0) 𝐷D (cid:3036)i,,𝐶C (cid:3037) (cid:3439)j (cid:1) == ∑(cid:3041)n 𝑚m𝑎a𝑥 m x(cid:4676) a 𝑑 (cid:3364) x d(cid:3364) (cid:3435) (cid:3364) (cid:110) (cid:3364) 𝐷 (cid:3364)D (cid:3364)d (cid:3364) (cid:3364) , (cid:0) (cid:3364) (cid:3364) ,𝐶 (cid:3364) (cid:3364)D C (cid:3115) (cid:3364) (cid:3364) (cid:3439) (cid:3364) (cid:3364) j ,(cid:3364) − C(cid:3364)(cid:3364) − (cid:3364) 𝑑 (cid:1) d(cid:3435) − 𝐷 (cid:3037) D d , (cid:0) 𝐶j , D (cid:3037) C(cid:3439),j , 0 C ,(cid:4677)0 (cid:1) ,0 (cid:111) ( ( 3 3 7 7 ) )
(cid:3533)j=1𝑚𝑎𝑥(cid:4676)𝑑(cid:3435)𝐷,𝐶(cid:3439)j −𝑑(cid:3435)𝐷,j𝐶(cid:3439)j,0(cid:4677)
(cid:3115) (cid:3037) (cid:3037)
(cid:3037)(cid:2880)(cid:2869)
According to Equation (37), demand points are more likely to be assigned to the
neareAsctcdoirsdtrinibgu ttoio Enquceantitoenr. (3A7)t, tdheemsaanmde ptoiminets, athreis mmoereth liokdelayl stoo btea kaesssiginnteoda tcoc tohuen ntetahre-
edsitv derisstitryibouftitohne cinenittiearl.p Aotp tuhlea stiaomn,ea tlilmowe,i tnhgisd memetahnodd paolsion ttsaktoesh ianvteo tahcecooupnpto trhtue ndiitvyetrosibtye
oafs stihgen iendittioalo pthoeprucleantitoenr,s athllaotwairnegf adretmhearnadw paoyi.nts to have the opportunity to be assigned
to other centers that are farther away.
(2) After assigning demand points and distribution centers, we must determine the
(2) Arefltaetri oansssihginpinbge tdweemenanvde hpiocilnestsa annddd deimstarinbdutpioonin ctse.nItnertsh, iwspe ampuers,tw deetuesrmetihnee gthreee rdey-
liantsioenrtsihoinpo bpeetrwaetoern fvoerhthicilsesin aintidal idzeamtioann,da psofoinlltosw. Isn: this paper, we use the greedy in-
sSetretpio1n: oAprerarantgoer aflolrd tehmisa innditpiaoliiznatstiionna, sacse nfodlilnogwos:r deroftheirearliestallowablearrival
Sttimepe 1w: Aithrrianntghee atilml deewmiannddo wpo.ints in ascending order of their earliest allowable arri-
vSatle ptim2:e Iwteirtahtien tthhreo utigmhe ewacinhdvoewh.i cletocheckifthesuppliesforeachdemandpoint
Sctaenp b2e: iIntesreartteed thinrotougthha teavcehh ivcleeh.iTclhei stoin cchluedcke sifc htheeck siunpgpiflitehse froeri seeancho udgehmcaanpda cpitoyintot
ccaanr rbyet ihneseitretmeds iinntoth tehatat svke.hIifctleh.e Tqhuisa nintictlyuodfesa nchyeictekmingin ift htheetraes kis, ewnhoeunghad cdapedactiotyt htoe
cqaurrayn ttihtye oitfesmusp ipnl itehsea tlaresakd. yIf itnheth qeuvaenhtiictyle o,ef xacneye ditsetmh einli mthiet ,ttahsekn, wthhaetnv eahdidcleedc taon tnhoet
qbueaunsteitdy foofr stuhpaptldieesm aalrnedadpyo iinnt .the vehicle, exceeds the limit, then that vehicle cannot
bSet eupse3d: fFoorr theaact hdevmehaincdle ,pcoainlctu. late the score (objective function value) of inserting
Satecpe r3t:a iFnorn oeadcehi nvteohiictl,ea, ncadlcrueclaotred ththee scinodree x(oobfjetchtievein fsuenrtcitoionnp voainlut,e)e voaf liunasteirntgingth ae
effectivenessofdifferentinsertionstrategies.
certain node into it, and record the index of the insertion point, evaluating the effec-
Step4: Amongallavailablevehicles,selecttheonethatresultsinthelowestinsertion
tiveness of different insertion strategies.
score. Alowerscoreindicatesthatinsertingthistaskcontributesleasttothegrowth
Step 4: Among all available vehicles, select the one that results in the lowest insertion
oftheobjectivefunction,whichmeansitisabetterinsertionpoint.
score. A lower score indicates that inserting this task contributes least to the growth
of the objective function, which means it is a better insertion point.

Symmetry2024,16,1080 13of30
4.4. Selection,Crossover,andMutation
Toenhancethealgorithm’ssearchcapability,thisstudydividesthepopulationinto
multipleclustersusingamethodbasedonindividualdominancerelationships. Individuals
atLevel1thatarenotdominatedareallocatedtothefirstrankofnon-dominance,whereas
thosethatareonlydominatedbyindividualsatLevel1receivethesecondrankofnon-
dominance,continuinginthismannerforsubsequentlevels.Therefore,allindividualshave
non-dominatedranks,andindividualswiththesamerankbelongtothesamecluster,with
thecrowdingdistanceofeachindividualintheclustersubjecttocalculation. Individuals
aregroupedbasedontheirrankvalues,formingclusters. Thisresearchproposesspecific
selection,crossover,andmutationtechniquestailoredtoaddresstheproblemdescribed.
Inourselectionapproach,binarytournamentselectionisutilizedwhenchoosingthe
parentpopulationforcrossoverandmutation.Thedetailedprocedureisasfollows:(1)Two
individualsarerandomlychosenfromthepopulationandevaluatedtheirnon-dominated
ranks. Anindividualwiththelowerrankisselectedandpreserved. Theindividualwitha
greatercrowdingdistanceischosenifbothindividualsholdidenticalranks,and(2)the
aforementionedproceduresarerepeateduntiltheoffspringpopulationattainsthesizeof
theoriginalpopulation.
Thecrossoveroperationinourstudygeneratesnewsolutionsbyexchangingsegments
of genetic information among individuals in the population. To enhance diversity and
exploration in our evolutionary optimization, we use the simulated binary crossover
(SBX)strategy. Thisoperationreassignsandblendsthegeneticinformationoftwoparent
solutions,therebyintroducingexploratorybehaviorinthesolutionspace. Thedetailed
process of this crossover is depicted in Figure 6. Additionally, this operator requires
the use of two formulas to calculate the values after crossover. Assuming two parent
(cid:0) (cid:1) (cid:0) (cid:1) (cid:0) (cid:1)
individualsp1 x1, ...,x1 andp2 x2, ...,x2 ,thetwooffspringindividualso1 x1, ...,o1
(cid:0) 1(cid:1) n 1 n 1 n
ando2 x2, ...,o2 generatedusingtheSBXoperatorcanbeobtainedusingthefollowing
1 n
Formula(38):
(cid:40) (cid:2) (cid:3)
y1 =0.5· (1+β)·x1+(1−β)·x2
i (cid:2) i i (cid:3) (38)
y2 =0.5· (1−β)·x1+(1+β)·x2
i i i
whereβisdeterminedbythedistributionfactorηaccordingtoFormula(39):
(cid:40)
(rand·2)1/(1+η) rand ≤0.5
β = (39)
{1/[(1−rand)·2]}1/(1+η)
otherwise
Additionally,itshouldbenotedthatalthoughchromosomeencodinginvolvesboth
integers and floating-point numbers, both rules are applicable to the above crossover
strategy. Theonlydifferenceisthatforintegerencoding,afterobtainingtheintermediate
value through the formula, it is necessary to round it to ensure compliance with the
encodingrules.
Afterthecrossoveroperation,thenextstepistoperformthemutationoperationas
shown in Figure 7. Each variable for each individual is evaluated. A random number
between 0 and 1 is generated and compared with the mutation probability P . If the
m
generatedrandomnumberisgreaterthanP ,theoriginalvariableisretained. Otherwise,
m
thepolynomialmutationstrategyisappliedformutationoperations. Withaprobability,
eachvariableintheindividualischangedbyintroducingrandomperturbationtoincrease
explorationinthesolutionspace. Themutationintensityiscontrolledbythedistribution
factor,wherelargervaluesresultingreaterperturbation,increasingindividualdiversity
andhelpingescapefromlocaloptimatoenhanceglobalsearchcapability. Similarly,the
differencebetweenthemutationinintegerencodingandreal-numberencodingliesinthe
needtoroundtointegerswithintherange.
Thecombinationoftheaboveselection,crossover,andmutationstrategiesdrivesthe
populationevolution. Ifthenewindividualsgeneratedduringthecrossoverandmutation
processes do not satisfy the 3D packing constraints, they are replaced, and the same

Symmetry2024,16,1080 14of30
procedureisfollowedinthesubsequentALNSphase. Ultimately,throughthisprocess,a
largenumberofnewindividualsaregenerated,andallindividualsaremerged. ThetopN
SSyymmmmeetrtryy 2 2002244, ,1 166, ,x x F FOORR P PEEEERR R REEVVIEIEWW 1166 oof f 3344
bestindividualsareselectedbasedonnon-dominancerankandcrowdingdistancetoform
anewpopulation.
FFigiguurree 6 6. .I Illlulusstrtraatitoionn o of ft hthee S SBBXX c crroossssoovveerr o oppeerraatitoionn. .
Figure6.IllustrationoftheSBXcrossoveroperation.
FFigiguurree 7 7. .I Illlulusstrtraatitoionn o of ft hthee p poolylynnoommiaial lm muutatatitoionn o oppeerraatitoionn. .
Figure7.Illustrationofthepolynomialmutationoperation.
TThhee c coommbbininaattioionn o off t thhee a abboovvee s seeleleccttioionn, ,c crroossssoovveerr, ,a anndd m muuttaattioionn s sttrraatteeggieiess d drriviveess t thhee
4.5. NeighborhoodSearch
ppooppuulalattioionn e evvooluluttioionn. .I Iff t thhee n neeww i ninddivivididuuaalsls g geenneerraatteedd d duurriningg t thhee c crroossssoovveerr a anndd m muuttaattioionn
Inthispaper, theneighborhoodsearchiscombinedwithALNSandthesimulated
pprroocceesssseess d doo n noott s saattisisffyy t thhee 3 3DD p paacckkiningg c coonnssttrraaininttss, ,t thheeyy a arree r reepplalacceedd, ,a anndd t thhee s saammee p prroo--
annealing concept. The ALNS framework provides a variety of removal and insertion
cceedduurree isis ffoolllolowweedd inin tthhee ssuubbsseeqquueenntt AALLNNSS pphhaassee. . UUltltimimaatteelyly, , tthhrroouugghh tthhisis pprroocceessss, , aa
operatorstoachieverapidimprovementandconvergenceofsolutions. Atthesametime,
lalarrggee n nuummbbeerr o off n neeww i ninddivivididuuaalsls a arree g geenneerraatteedd, ,a anndd a alll li ninddivivididuuaalsls a arree m meerrggeedd. .T Thhee t toopp
throughtemperaturecontrolandacceptancerulesinspiredbysimulatedannealing,the
𝑁𝑁 bbeesstt i ninddivivididuuaalsls a arree s seelelecctteedd b baasseedd o onn n noonn--ddoommininaannccee r raannkk a anndd c crroowwddiningg d disisttaannccee t too
algorithmexploresthesearchspace,allowingtheacceptanceofworsesolutionstoavoid
ffoorrmm a a n neeww p pooppuulalattioionn. .
gettingstuckinlocaloptima.
TheALNScanadaptivelyselecttheoperatorswithahistoryofgoodperformance
44.5.5. .N Neeigighhbboorrhhoooodd S Seeaarrcchh
forthenextiteration,allowingtheoperatorstofullyexploittheirsearchcapabilities. This
paperIInd n e ts thh iigsi n s ps pat aph pee err f, o , tl thl h oee w nn ien eigi g ghh tbh bor o errhe hod ooo eds d t sr seu eac art rci c ohh n isi a s n ccod omm twbbioniner e edd p wa w iirtitho h pA A eLr L aNN toSS r as anf ndo d r tt thh hee e sr siemim seuu alal r a ctteh edd
par ano nnb nel e eaa mlilni ; nge g ac c coh onnco cep epe ptr t.a .T t T ohh ree iA s ALa LNs N sSi S g f n frrae amd mea eww woo eri rkg k hp p trroa ovn viddidea esn s a a i nv v iat ari riaei l ett syy c o o ofr f er r ,eema m nod ovvat a hl l ea a snn edd w i ni e nsi seg erh rtt tioi s ona n no o dpp--
sec ero rar ate tos orr ass r te too u ap acc dhh aiei t e evv dee arraf a tpe pirdid o ibmim tapp irn roi o nvveg emm aeb enn ett t t ae anr nds d o cl cou ont n ivo ven errgu ges eni n ncceg e ot o hff e ssoo olpulu ettiroi a ont n oss r. . As A ott t th thh aee t so saa pmm eer e a tt tiomim rsee, ,
wtthi h trh roo huu igg ghh h e tter ems m cpo per ere ras att cuu arr nee b ccoe onu nts trr eoo dl l ai a nnnds d u ab acc sce cee qpp uttae ann nct cei e t errur u alel t e iso s inni s nss tpo piri o ree bdd t a bi byn y hssiimi g m huu -lqala uttea edl d i t ay ann sno nel eau altil ini o ngn g,s , t. thhee
aalglgoorritithhmm e exxpplolorreess t thhee s seeaarrcchh s sppaaccee, ,a alllolowwiningg t thhee a acccceeppttaannccee o off w woorrssee s sooluluttioionnss t too a avvooidid
ggeettttiningg s sttuucckk i nin l oloccaal lo oppttimimaa. .
TThhee A ALLNNSS c caann a addaappttiviveelyly s seelelecctt t thhee o oppeerraattoorrss w witithh a a h hisisttoorryy o off g goooodd p peerrffoorrmmaannccee f foorr
tthhee n neexxtt i titeerraattioionn, ,a alllolowwiningg t thhee o oppeerraattoorrss t too f fuulllyly e exxpploloitit t thheeirir s seeaarrcchh c caappaabbiliiltitieiess. .T Thhisis p paa--
ppeerr d deessigignnss t thhee f foolllolowwiningg t thhrreeee d deessttrruuccttioionn a anndd t twwoo r reeppaairir o oppeerraattoorrss f foorr t thhee r reesseeaarrcchh p prroobb--
lelemm; ;e eaacchh o oppeerraattoorr i sis a assssigignneedd a a w weeigighhtt a anndd a ann i ninititiaial ls sccoorree, ,a anndd t thheessee w weeigighhttss a anndd s sccoorreess

Symmetry2024,16,1080
15of30
ShawRemovalOperator. Calculatethesimilaritybasedonthedistancebetweennodes
andtherequiredservicetime,andremovethetopNtaskswiththehighestsimilarity.
Random Removal Operator. Randomly remove n task nodes from the vehicle’s deliv-
eryroute.
WorstRemovalOperator. Removethentasknodesthatresultinthelargestincreasein
totalcost.
GreedyInsertionOperator. Sortthetasknodestobeinsertedinascendingorderoftheir
lefttimewindowsandinsertthemtominimizethedeliverytimeasmuchaspossible.
RegretInsertionOperator. Foreachunallocatedtasknode,thealgorithmcalculatesthe
scoreafterinsertingitatacertainposition,sortsthescores,andselectsthetopmscores
ascandidateinsertionpositions. Itcomputesthesumoftheabsolutedifferencesbetween
thehighestscoreandthescoresofothercandidateinsertionpositionsastheregretvalue
forthatcandidateinsertionposition. Thisoperatoriteratesthroughthelistofunallocated
tasks,findingtheinsertionpositionwiththehighestregretvalueforeachtask.
Toescapelocaloptima,thisstudyreferstotheacceptancecriteriadesignedbyLin
istheinitialsolution,andζ′
| etal.[61]. | Supposeζ |     |     |     | isthenewsolutionobtainedfollowing |     |     |     |
| ---------- | -------- | --- | --- | --- | --------------------------------- | --- | --- | --- |
one iteration of ALNS; Table 2 outlines five criteria for acceptance. Here, ∆f and ∆f
|     |     |     |     |     |     |      |       | 1 2    |
| --- | --- | --- | --- | --- | --- | ---- | ----- | ------ |
|     |     |     |     |     |     | ∆f = | (ζ′)− | (ζ)and |
denotethedifferencesinobjectivevaluesbetweentwosolutions: 1 f 1 f 1
∆f = f (ζ′)− f (ζ). Additionally, we need P , P , and r, where P = exp(−∆f /K·T),
| 2   | 2       | 2      |     |     | 1 2 | 1   |     | 1   |
| --- | ------- | ------ | --- | --- | --- | --- | --- | --- |
| =   | exp(−∆f | /K·T); |     |     |     |     |     |     |
P 2 2 r is a random number uniformly distributed in [0, 1], T is the
| temperaturecoefficient,andtheBoltzmannconstantK |     |     |     |     | =1. |     |     |     |
| ----------------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- |
Table2.Theneighborhoodsearchintroducesfivecriteriaforacceptingsolutions.
| (1) | ∆f ≤0,∆f | ≤0:ζ′isaccepted;            |            |      |                            |     |     |     |
| --- | -------- | --------------------------- | ---------- | ---- | -------------------------- | --- | --- | --- |
|     | 1        | 2                           |            |      |                            |     |     |     |
| (2) | ∆f ≤0,   | ∆f >0:ζ′isacceptedonlyifr<P |            |      | ;                          |     |     |     |
|     | 1        | 2                           |            |      | 1                          |     |     |     |
|     | ∆f       | ∆f ≤0:ζ′isacceptedonlyifr<P |            |      |                            |     |     |     |
| (3) | 1 >0,    | 2                           |            |      | 2 ;                        |     |     |     |
|     | ∆f >0,   | ∆f >0and∆f                  | (ζ′)<∆f    |      | (ζ′):ζ′isacceptedonlyifr<P |     |     |     |
| (4) | 1        | 2                           | 1 /f 1     | 2 /f | 2                          |     | 2 ; |     |
| (5) | ∆f >0,   | ∆f >0and∆f                  | /f (ζ′)>∆f | /f   | (ζ′):ζ′isacceptedonlyifr<P |     | ;   |     |
|     | 1        | 2                           | 1 1        | 2    | 2                          |     | 1   |     |
During every iteration, the probability pl governs the refinement of each solution
X throughtheneighborhoodsearchprocess. Itisimportanttonotethattherearethree
Xt
distinct instances of X in this context: X refers to the current solution, refers to the
currentsolution X aftertheremovalandinsertionoperations, and Xb referstothebest
historicalsolutionuptothecurrentpoint. Furthermore,thescoreforsolutionXisdenoted
asG(X),whereRem(X)representstheremovaloperationappliedtosolutionX,andIns(X)
ρ−
represents the insertion operation applied to solution X. represents the probability
ofchoosingdifferentremovaloperators,whileρ+ representstheprobabilityofselecting
|                              |     |     | Initially,bothρ− |     | andρ+                         |     |     |     |
| ---------------------------- | --- | --- | ---------------- | --- | ----------------------------- | --- | --- | --- |
| differentinsertionoperators. |     |     |                  |     | aresetto1,meaningalloperators |     |     |     |
haveanequalchanceofbeingselected. Aftereachiteration,theseprobabilitiesareupdated.
θ− denotesthesetofremovaloperators,andθ+
|     |     |     |     |     | denotesthesetofinsertionoperators. |     |     | The |
| --- | --- | --- | --- | --- | ---------------------------------- | --- | --- | --- |
currentchoiceofremovalandinsertionoperatorsforeachiterationisdeterminedusing
aroulettewheelselectionmethod. Inthismethod,theprobabilityofselectionisdirectly
proportionaltothevaluesofρ− andρ+,meaninghighervaluesforρ− andρ+ resultina
greaterlikelihoodofbeingchosen. Theprocedureoftheneighborhoodsearchisprovided
byAlgorithm1.

Symmetry2024,16,1080 16of30
Algorithm1.ProcedureoftheNeighborhoodSearch
1: input:afeasiblesolutionX
2: Xb =X;ρ− =(1,...,1);ρ+ =(1,...,1);
3: repeat
4: selectremovalandinsertionoperationsRem ∈ θ−andIns∈
5: θ−usingρ−andρ+;
6: Xt = Ins(Rem(X));
7: if(anyoffiveconditionsissatisfied)then
8: X=Xt;
9: endif
10: ifG (cid:0) Xt(cid:1) <G (cid:16) Xb (cid:17) then
11: Xb =Xt;
12: endif
13: updateρ−andρ+;
14: untilstopcriterionismet
15: returnXb
5. NumericalExperiments
Giventhelackofconsiderationforourresearchedprobleminexistingstudies,the
correspondingalgorithmsintheliteraturecannotbedirectlyemployedtosolvetheprob-
lemunderinvestigation. Therefore,thisworkchoosesthestrengthparetoevolutionary
algorithmII(SPEA-II)[62],multi-objectiveevolutionaryalgorithmbasedondecomposition
(MOEA/D)[63],andmulti-objectiveevolutionaryalgorithmbasedondecompositionwith
dynamicresourceallocation(MOEA/D-DRA)[64]ascomparativealgorithms. TheSPEA-II
andMOEA/Dareclassicmulti-objectiveevolutionaryalgorithmsandhavereceivedposi-
tiveevaluationsinvehicleroutingproblems[65–68]. TheMOEA/D-DRAisavariantofthe
MOEA/D,introducingadynamicresourceallocationstrategytomakemoreefficientuseof
computationalresourcesandenhancetheperformanceandefficiencyofthealgorithm[69].
Inthispaper,wecompareourproposedalgorithmtothesethree. DetailsontheSPEA-II,
MOEA/D,andMOEA/D-DRAareasfollows:
(1) SPEA-IIadoptsthesolutionrepresentationmethodsimilartotheMOGA-ALNS,as
detailedinSection4.2. Itbeginswiththegenerationofarandompopulationusing
the method described in the same section. The selection and population update
mechanismsadheretothefoundationalstructureoftheSPEA-II,asoutlinedinthe
literature[62]. Forgeneticoperations,SPEA-IIincorporatesthesamecrossoverand
mutation techniques as found in the MOGA-ALNS, ensuring consistency in the
approachtoevolvingsolutions.
(2) AligningwiththeMOGA-ALNSforsolutionrepresentation,theMOEA/Dleverages
theTchebycheffapproachtocreateaseriesofsubproblemstargetingdifferentparts
oftheobjectivespace[63]. Theprocessesforconstructingneighborhoods,selecting
individuals,andupdatingindividualsolutionsareallbasedonthecoreprinciples
of the MOEA/D [63]. Furthermore, the algorithm applies identical crossover and
mutationstrategiesastheMOGA-ALNS,facilitatingauniformmethodofintroducing
geneticdiversityandexploringthesolutionspace.
The MOEA/D-DRA not only aligns with the MOGA-ALNS in terms of solution
representationbutalsointheemploymentoftheTchebycheffapproachforformulating
single-objectivesubproblems. Themethodforbuildingneighborhoodsandtheprotocols
forindividualselectionandupdatesareinlinewiththeMOEA/D-DRAframework[64].
Liketheotheralgorithms,theMOEA/D-DRAutilizesthesamecrossoverandmutation
operations as the MOGA-ALNS, ensuring a coherent approach to optimization across
differentmethodologies.

Symmetry2024,16,1080 17of30
5.1. TestCase
Inthispaper,wemadeappropriatemodificationstotheclassicinstancesproposed
byCordeautoaccommodatethecharacteristicsofourproblemanddesignedthetestcase
set used in the following sections, which consists of 20 instances. We considered five
different scenarios. Specifically, the first scenario represents a situation where none of
thecandidatedistributioncentersexperiencedisruptions. Intheotherscenarios,oneor
twodistributioncentersencounterdisruptions. Theseinstancesaredistinguishedbythe
namedform|I|−|J|−a,where|I|isthenumberofcandidatedistributioncenters,|J|is
thenumberofdemandpoints,arepresentsthefirstscenario,andb,c,d,anderepresent
theotherfourscenarios.
Fourdifferenttypesofcommoditieswereselected,andthedemandquantityofeach
commodityforeachcustomerisrandomlygeneratedintherangeof[10,20]. Penaltycoeffi-
cientsforearlyandlatearrivalsarerandomlygeneratedfromtherange[1,3],transportation
costsperunittimearerandomlygeneratedfromtherange[5,10],vehicletransportation
speedsarerandomlygeneratedintherange[5,10],distributioncenterlocationcostsare
randomlygeneratedfromtherange[100,200],unitexpansioncostsarerandomlygenerated
fromtherange[10,20],andtheprobabilitiesofsecondarydisastersoccurringatindividual
distributioncentersandroadsegments,aswellastheprobabilityofsignificantdamage
causedbydisasters,arerandomlygeneratedintherange(0,0.5]. Thecapacityβ ofeach
i
distributioncenterisdeterminedusingthefollowingmethod:wefirstcalculatetheaverage
requiredcapacityβusingthefollowingFormula(40):
d
β = (40)
|I|
wheredrepresentsthetotalcapacityofthematerialsrequiredatthepointofdemand,and
|I| represents the number of candidate distribution centers. Then, the capacity of each
(cid:2) (cid:3)
distributioncenterβ israndomlygeneratedat 1.5β, 2β .
i
5.2. PerformanceMetrics
TheaimoftheMOGA-ALNSistodiscoverasetofsolutionsthatexhibitbothgood
convergenceanddiversity. Consequently,tobetterassesstheapproximationanddistri-
butionoftheobtainedsolutionset,thisstudyutilizesC-metric[70],IGD-metric[71],and
hypervolume-metric[72]asevaluationindicators. Moreover,weemploythet-testtoana-
lyzethesignificanceoftheresultsobtainedusingtheMOGA-ALNS,SPEA-II,MOEA/D,
andMOEA/D-DRA.WhentheMOGA-ALNSissignificantlybetter,significantlyworse,or
statisticallyequivalenttootheralgorithms,theresultsareindicatedas“+”,“−”,or“∼”.
(1) The C-metric, a tool for evaluating the comparative performance of two different
algorithmsthroughtheirsolutionsetsXandY,quantifiestheextenttowhichoneset
dominatesanother. Specifically,C(X, Y)representstheproportionofsolutionsinset
Ythataredominatedbyatleastonesolutioninset X. Theformulaforcalculating
thismetricisasfollows:
|{yϵY|∃xϵX : x ≺ y}|
C(X,Y) = (41)
|Y|
(2) TheIGD-metriccalculatestheminimumEuclideandistancebetweentheapproximate
solution set and the Pareto-optimal front. A smaller IGD value indicates that the
solution set generated by the algorithm is closer to the true front. Let Z∗ and Z
represent the optimal solution set and the approximate solution set, respectively.
Formula(41)forIGDmeasurementisasfollows:
IGD(Z, Z ∗) = 1 ∑ dist(z,Z) (42)
|Z∗|
z∈Z∗

Symmetry2024,16,1080
18of30
Z)istheEuclideandistancebetweenasolutionzinZ∗
| wheredist(z, |     |     |     | andtheclosest |
| ------------ | --- | --- | --- | ------------- |
solutiontoitinZ. Therefore,inthecalculationofIGD,itisfirstnecessarytohavea
knowntruefrontoranidealfrontthatrepresentsthebestsolutionstotheproblem.
SincethePareto-optimalfrontofthestudiedproblemisunknown,thisstudycombines
allnon-dominatedsolutionsobtainedbyvariousmethodsandconsidersthemasan
approximatePareto-optimalfront. Furthermore,thisstudynormalizesallobjective
values,mappingthemintotherange[0,1]beforecalculatingtheIGD.
(3) Thehypervolume-metricmeasuresthecoveragerangesizeoftheapproximatesetin
theobjectivespace. Ahigherhypervolumevalueindicatesabroadercoveragerange
oftheapproximatesetintheobjectivespace,whichtypicallyimpliesthehigherquality
|     |     | Lety∗ | (cid:0) y∗, y∗(cid:1) |     |
| --- | --- | ----- | --------------------- | --- |
oftheobtainednon-dominatedsolutionset. = bethereferencepointin
1 2
theobjectivespacedominatedbyalloptimalsolutions. Then,thehypervolumevalue
ofthesolutionsetrepresentsthevolumeofaregionwhereallsolutionsaredominated
bythesolutionsetanddominatey∗.
Whencalculatingthehypervolume-metric,a
referencepointneedstobeselected. Inthispaper,(1,1)isusedasthereferencepoint,
and all objective values in the approximate solution set are normalized, mapping
themintotherange[0,1].
5.3. ParameterConfiguration
Toinvestigatetheimpactofalgorithmparametersettingsontheperformanceofthe
MOGA-ALNS,weemployedanorthogonalexperimenttoexploretheoptimalparameter
combinations,includingpopulationsizeN,simulatedannealingrateα,andthenumberof
iterationswithoutimprovementθ. Wedefinedfourlevelsforeachofthethreeparameters:
N ∈ {50, 75, 100, 125}, α ∈ {0.3, 0.5, 0.7, 0.9}, and θ ∈ {30, 60, 90, 120}. Conse-
(cid:0) (cid:1)
quently,weconstructedanorthogonalarrayL 43 with16parametercombinations,as
16
showninTable3.
Table3.Orthogonaltableandexperimentalresults.
| No  | N   | α   | θ   | ARV    |
| --- | --- | --- | --- | ------ |
| 1   | 50  | 0.3 | 30  | 0.7555 |
| 2   | 50  | 0.5 | 60  | 0.7659 |
| 3   | 50  | 0.7 | 90  | 0.8319 |
| 4   | 50  | 0.9 | 120 | 0.8440 |
| 5   | 75  | 0.3 | 60  | 0.8035 |
| 6   | 75  | 0.5 | 30  | 0.8853 |
| 7   | 75  | 0.7 | 120 | 0.8059 |
| 8   | 75  | 0.9 | 90  | 0.9506 |
| 9   | 100 | 0.3 | 90  | 0.9447 |
| 10  | 100 | 0.5 | 120 | 0.8874 |
| 11  | 100 | 0.7 | 30  | 0.8825 |
| 12  | 100 | 0.9 | 60  | 0.8303 |
| 13  | 125 | 0.3 | 120 | 0.8796 |
| 14  | 125 | 0.5 | 90  | 0.9341 |
| 15  | 125 | 0.7 | 60  | 0.8624 |
| 16  | 125 | 0.9 | 30  | 0.9682 |
Inthisexperiment,weselectedthehypervolume-metricastheresponsevalue(RV)
andindependentlyraneachparametercombination20times,calculatingtheaverageRV
valuebasedontheresultsof20independentruns. Theresultsoftheorthogonalexperiment
are shown in Table 3, and the significance ranking of parameters is shown in Table 4.
Furthermore,Figure8depictsthetrendsinparameterinfluence. Basedontheresultsfrom
Table4andFigure8,wecanobservethatthepopulationsizeNplaysthemostcrucialrole
intheMOGA-ALNS,followedbythenumberofiterationswithoutimprovementθranking
second,andthesimulatedannealingrateαrankingthird. Therefore,thisstudyconcludes,

| Symmetry 2024, 16, x FOR PEER REVIEW  |     |     |     |     |     |     |     | 21 of 34  |
| ------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --------- |

|     | 10  | 100  |     | 0.5  |     | 120  |     | 0.8874  |
| --- | --- | ---- | --- | ---- | --- | ---- | --- | ------- |
|     | 11  | 100  |     | 0.7  |     | 30   |     | 0.8825  |
|     | 12  | 100  |     | 0.9  |     | 60   |     | 0.8303  |
|     | 13  | 125  |     | 0.3  |     | 120  |     | 0.8796  |
|     | 14  | 125  |     | 0.5  |     | 90   |     | 0.9341  |
|     | 15  | 125  |     | 0.7  |     | 60   |     | 0.8624  |
Symmetry2024,16,1080
|     | 16  | 125  |     | 0.9  |     | 30  |     | 0.9682  19of30 |
| --- | --- | ---- | --- | ---- | --- | --- | --- | -------------- |
Table 4. Influence trend and rank.
throughananalysisoftheexperimentalresults,thattheMOGA-ALNSperformsbestwhen
N=125,α=0.9,andθ=90.
|     | Level                            |       | 𝑵       |        |               | 𝜶      |               | 𝜽      |
| --- | -------------------------------- | ----- | ------- | ------ | ------------- | ------ | ------------- | ------ |
|     | 1  Table4.Influencetrendandrank. |       | 0.7993  |        | 0.8458        |        | 0.8729        |        |
|     | 2                                |       | 0.8613  |        | 0.8682        |        | 0.8155        |        |
|     |                                  | Level |         | N      |               |        |               |        |
|     |                                  |       |         |        |               | α      |               | θ      |
|     | 3                                |       | 0.8862  |        | 0.8456        |        | 0.9153        |        |
|     |                                  | 1     |         | 0.7993 |               | 0.8458 |               | 0.8729 |
|     | 4                                |       | 0.9111  |        | 0.8983        |        | 0.8542        |        |
|     |                                  | 2     |         | 0.8613 |               | 0.8682 |               | 0.8155 |
|     | Delta                            | 3     | 0.1117  | 0.8862 | 0.0526 0.8456 |        | 0.0909.981 53 |        |
|     |                                  | 4     |         | 0.9111 |               | 0.8983 |               | 0.8542 |
|     | Rank                             |       | 1       |        |               | 3      |               | 2      |
|     |                                  | Delta |         | 0.1117 |               | 0.0526 |               | 0.0998 |
|     |                                  | Rank  |         | 1      |               | 3      |               | 2      |
|     |                                  |       |         |        |               |        |               |        |
Figure8.InfluencetrendofparametersintheMOGA-ALNS.
Figure 8. Influence trend of parameters in the MOGA-ALNS.
|     | 5.4. EffectivenessofNeighborhoodSearch |     |     |     |     |     |     |     |
| --- | -------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
5.4. Effectiveness of Neighborhood Search
IntheMOGA-ALNS,ALNSisutilizedasaneighborhoodsearchmechanismtofurther
In the MimOpGrAov-eAtLheNsSo,l uAtiLonNsSfo irs puattihliozpetdim aisz aat inone.igThobaossrehsosothde sceonartrcihbu mtioencshoafnnisemigh tboo rfhuoro-d
ther improves teharec hsowluithtiionnthse foMrO pGaAth-A oLpNtiSmfriazmateiwoonr.k T,wo eadsseevseslo tpheed caomnotrdiibfiuedtivoenrssi oonf ntheaitgohpberoart-es
withouttheneighborhoodsearchcomponent,referredtoasMOGA-ALNS-w/o-NS.Subse-
hood search within the MOGA-ALNS framework, we developed a modified version that
quently,weprocessedallinstancesusingbothMOGA-ALNSandMOGA-ALNS-w/o-NS,
operates without the neighborhood search component, referred to as MOGA-ALNS-w/o-
evaluatingtheirexperimentaloutcomesthroughthehypervolume-metricandIGD-metric,
NS. Subsequently, we processed all instances using both MOGA-ALNS and MOGA-
as presented in Table 5 (where “var” denotes variance). Among the 20 instances, the
ALNS-w/o-NMS,O eGvAal-uAaLtNinSga tlhgeoirrit hexmpoeuritmpeernfotraml oedutMcoOmGeAs- tAhLrNouS-gwh/ toh-eN hSyinpe1r8vionlsutamncee-sm, eastreicv i-
and IGD-metdreinc,c eads bpyrietssehnigtheedr mine aTnahbylep e5r v(owluhmeer-em “evtraicr”v adlueens,ottheuss vuanrdiearnsccoer)i.n Agtmheoenfgfe ctthivee n2e0s s
ofincorporatingneighborhoodsearchinenhancingalgorithmicperformance.
instances, the MOGA-ALNS algorithm outperformed MOGA-ALNS-w/o-NS in 18 in-
By computing the average means and variances in the hypervolume-metric from
stances, as evidenced by its higher mean hypervolume-metric values, thus underscoring
20independenttrials,theresultantaverageHypervolumevaluesfortheMOGA-ALNSand
the effectiveness of incorporating neighborhood search in enhancing algorithmic perfor-
MOGA-ALNS-w/o-NSare0.8319and0.7605,respectively. Thecorrespondingvariances
mance.  fortheseaveragesare0.0090fortheMOGA-ALNSand0.0131forMOGA-ALNS-w/o-NS.
By compTuhtisiningd tihcaet easvtehraatgthee mMeOaGnsA a-AnLdN vSaoriuatnpecrefso rimn sthMeO hGyAp-eArLvNolSu-mw/eo-m-NeSt,raics iftraocmhi e2v0e s
independent atrhiiaglhse, rthave erreasguelvtaanlute arveleartaivgeet oHtyhpeemrveaonlu. Tmheis vsaulpueersio froitry tshueg gMesOtsGthAa-tAthLeNinSc launsido n
oflocalsearchcontributessignificantlytoperformance,reflectingitsabilitytofindmore
MOGA-ALNS-w/o-NS are 0.8319 and 0.7605, respectively. The corresponding variances
effectivesolutionsbyexploitingthesearchspacemoreefficiently.
for these averages are 0.0090 for the MOGA-ALNS and 0.0131 for MOGA-ALNS-w/o-NS.
ByaveragingthemeansoftheIGD-metricacross20runs,theaveragevaluesforthe
This indicates that the MOGA-ALNS outperforms MOGA-ALNS-w/o-NS, as it achieves a
MOGA-ALNSandMOGA-ALNS-w/o-NSwithrespecttothemeanarefoundtobe0.2334
higher averagane dv0a.l2u6e4 6r,erleastpivecet itvoe ltyh,ea nmdewainth. Trehsipse cstutpoevraioriraintyce ,suthgegaevsetrsa gtheavta tluhees ianrcel0u.s0i0o1n2 aonfd
local search c0o.0n0t1r3ib,uretsepse scitgivneilfiy.caTnhtislyi ntdoi cpaetrefsotrhmatatnhceeM, rOeflGeAc-tAinLgN iStso aubtpileirtfyo rtmo sfiMndO mGAo-rAe LeNf-S-
fective solutiown/so -bNyS e,xapsliotiatcihnige vtehsel osewaerrcahv sepraagcee vmalourees einffitecriemnstloyf. both mean and variance. The
By averaging the means of the IGD-metric across 20 runs, the average values for the  loweraveragevaluesfortheMOGA-ALNSreflectitssuperiorperformance,demonstrating
itsefficiencyinproducingsolutionsthatarenearertothetrueParetofrontandwithless
MOGA-ALNS and MOGA-ALNS-w/o-NS with respect to the mean are found to be 0.2334
variabilitybetweenruns,thusunderliningtheeffectivenessofintegratingneighborhood
and 0.2646, respectively, and with respect to variance, the average values are 0.0012 and
searchstrategieswithintheMOGA-ALNSframeworkforoptimizingsolutions.
0.0013, respectiveTloyr. igTohroisu silnydeivcaaluteaste tahnadt ctohmep MareOthGeAp-eArfoLrNmSan oceudtpifeferrfeonrcmessb eMtwOeGenAth-AeMLNOGS-A-
ALNSandMOGA-ALNS-w/o-NS,thisstudyemploysstatisticaltestingmethods,specifi-
callytheFriedmantest[73]andtheNemenyipost-hoctest[74].Thesetestsareinstrumental

Symmetry2024,16,1080 20of30
inidentifyingstatisticallysignificantdifferencesinthealgorithms’performancesacross
multipledatasetsorprobleminstances.
Table 5. Experimental results for the MOGA-ALNS and MOGA-ALNS-w/o-NS based on the
hypervolume-metricandIGD-metric.
Hypervolume-Metric IGD-Metric
Instance MOGA-ALNS MOGA-ALNS-w/o-NS MOGA-ALNS MOGA-ALNS-w/o-NS
Mean Var Rank Mean Var Rank Mean Var Rank Mean Var Rank
5-40-a 0.8442 0.0083 1 0.7442 0.0161 2 0.2064 0.0015 1 0.2679 0.0016 2
5-40-b 0.7867 0.0101 1 0.7589 0.0108 2 0.0726 0.0005 1 0.2746 0.0009 2
5-40-c 0.8359 0.0104 1 0.7537 0.0105 2 0.1721 0.0011 1 0.2642 0.0014 2
5-40-d 0.8119 0.0131 1 0.7894 0.0086 2 0.1621 0.0017 1 0.2222 0.0018 2
5-40-e 0.8217 0.0097 1 0.7670 0.0093 2 0.1329 0.0005 1 0.2541 0.0013 2
5-60-a 0.7867 0.0106 2 0.7936 0.0103 1 0.1708 0.0018 1 0.2468 0.0022 2
5-60-b 0.7986 0.0182 1 0.7274 0.0203 2 0.1739 0.0013 1 0.2630 0.0016 2
5-60-c 0.8148 0.0190 1 0.7952 0.0152 2 0.1500 0.0009 1 0.2173 0.0014 2
5-60-d 0.7829 0.0180 1 0.7577 0.0153 2 0.1308 0.0008 1 0.2500 0.0014 2
5-60-e 0.8466 0.0060 1 0.7323 0.0146 2 0.1713 0.0013 1 0.2790 0.0023 2
5-80-a 0.8939 0.0089 1 0.7733 0.0140 2 0.1714 0.0022 1 0.2062 0.0012 2
5-80-b 0.8251 0.0148 1 0.7641 0.0195 2 0.1803 0.0016 1 0.2119 0.0011 2
5-80-c 0.8641 0.0043 1 0.7670 0.0184 2 0.1966 0.0009 1 0.2035 0.0013 2
5-80-d 0.8354 0.0030 1 0.7626 0.0076 2 0.1580 0.0017 1 0.2647 0.0015 2
5-80-e 0.8456 0.0043 1 0.7557 0.0125 2 0.2485 0.0027 2 0.2094 0.0013 1
5-100-a 0.8317 0.0024 1 0.7618 0.0104 2 0.1700 0.0016 1 0.3164 0.0010 2
5-100-b 0.7985 0.0098 1 0.7070 0.0054 2 0.1795 0.0007 1 0.2278 0.0010 2
5-100-c 0.8173 0.0056 1 0.8095 0.0154 2 0.0988 0.0007 1 0.1916 0.0010 2
5-100-d 0.9211 0.0015 1 0.7455 0.0178 2 0.1797 0.0007 2 0.1587 0.0013 1
5-100-e 0.8750 0.0024 1 0.7647 0.0105 2 0.1401 0.0007 1 0.1633 0.0006 2
Average 0.8319 0.0090 1.0500 0.7605 0.0131 1.9500 0.1632 0.0012 1.1000 0.2346 0.0013 1.9000
(1) IntheFriedmantest,weorganizetheMOGA-ALNSandMOGA-ALNS-w/o-NSby
descendingaveragevaluesofthehypervolume-metricandascendingaveragevalues
fortheIGD-metric,assigningthemranksof1and2,respectively.Wethencalculatethe
averageranksacrossallinstancesasdepictedinTable5. Forthehypervolume-metric,
theaverageranksare1.05fortheMOGA-ALNSand1.95forMOGA-ALNS-w/o-NS.
Similarly,fortheIGD-metric,theaverageranksstandat1.1000fortheMOGA-ALNS
and1.9000forMOGA-ALNS-w/o-NS.Thisdifferentiationinaverageranksallows
ustodeduceastatisticallysignificantdisparityinperformancebetweentheMOGA-
ALNSandMOGA-ALNS-w/o-NSaccordingtotheFriedmantest.
(2) TodelvedeeperintothedistinctionsbetweentheMOGA-ALNSandMOGA-ALNS-
w/o-NS, we employ the Nemenyi post-hoc test at a significance level of 0.05 to
ascertainthecriticaldiscrepancyintheiraveragerankvalues. Thegapinaverage
ranksforthehypervolume-metricis0.9000,surpassingthecriticalthresholdof0.4382.
Similarly,fortheIGDmetric,thedifferenceinaverageranksis0.8000,alsoexceeding
thecriticalvalue. ThesefindingsunderscoretheMOGA-ALNS’snotablesuperiority
overMOGA-ALNS-w/o-NSacrossbothevaluatedmetrics.
Theresultsindicatethattheneighborhoodsearchindeedenhancesthesearchcapabili-
tiesoftheMOGA-ALNS,playingapositiveroleinthesearchprocess. Thisdemonstrates
the effectiveness of integrating neighborhood search strategies into the MOGA-ALNS
framework,leadingtoimprovedperformanceinsolvingoptimizationproblemsbyfacili-
tatingamorethoroughexplorationofthesolutionspace.
5.5. ExperimentalResults
This section provides a comprehensive comparison of the MOGA-ALNS, SPEA-II,
MOEA/D, and MOEA/D-DRA. The parameter settings for the experiments are as fol-

Symmetry2024,16,1080
21of30
lows[68,75]. ForSPEA-II,thepopulationsizeissetto100,withacrossoverprobabilityof
0.7andamutationprobabilityof0.3. MOEA/Dhasapopulationsizeof100,acrossover
probabilityof0.8,amutationprobabilitysetto1,andaneighborhoodsizesetto20. The
parameter settings for the MOEA/D-DRA are from the literature [64], which include a
populationsizeof600,acrossoverprobabilityof0.8,amutationprobabilityof0.2,anda
neighborhoodsizeof20.
5.5.1. AnalysisoftheC-Metric
Table6presentstheoutcomesoftheC-metricanalysis,withtheacronyms“GA”,“EAD”,
“SPEA”,and“DRA”denotingtheMOGA-ALNS,SPEA-II,MOEA/D,andMOEA/D-DRA,
respectively.Foreachinstance,theaveragevaluecalculatedusingtheC-metricover20runs
ispresented. Furthermore,toensureaclearanalysisoftheexperimentaloutcomes,we
employaone-tailedt-testwith38degreesoffreedomanda0.05significancelevel[70]to
verifythedifferencesbetweenMOGA-ALNSanditscompetitors. Table6illustratesthe
performancecomparisonusingthesymbols“+”,“−”,and“∼”toindicatescenarioswhere
theMOGA-ALNSissignificantlysuperior,significantlyinferior,orstatisticallyonparwith
thecomparedalgorithms,respectively.
Table6.C-metriccomparisonofthefourapproaches.
|          | C(GA,  | C(EAD, | C(GA,    | C(SPEA, | C(GA,    | C(DRA, |        |
| -------- | ------ | ------ | -------- | ------- | -------- | ------ | ------ |
| Instance |        |        | t-Test   |         | t-Test   |        | t-Test |
|          | EAD)   | GA)    | SPEA)    | GA)     | DRA)     | GA)    |        |
| 5-40-a   | 0.7589 | 0.0807 | + 0.7267 | 0.0863  | + 0.5183 | 0.0923 | +      |
| 5-40-b   | 0.8063 | 0.0208 | + 0.8110 | 0.0513  | + 0.7292 | 0.0618 | +      |
| 5-40-c   | 0.8481 | 0.0310 | + 0.6696 | 0.0575  | + 0.6801 | 0.0836 | +      |
| 5-40-d   | 0.7870 | 0.0518 | + 0.8489 | 0.0499  | + 0.6589 | 0.0731 | +      |
|          |        |        | +        |         | +        |        | +      |
| 5-40-e   | 0.8945 | 0.0146 | 0.8588   | 0.0208  | 0.7427   | 0.0427 |        |
| 5-60-a   | 0.7667 | 0.0458 | + 0.7828 | 0.0739  | + 0.2857 | 0.1631 | +      |
| 5-60-b   | 0.7624 | 0.0000 | + 0.7983 | 0.0405  | + 0.6721 | 0.1010 | +      |
| 5-60-c   | 0.8135 | 0.0467 | + 0.8265 | 0.0351  | + 0.6653 | 0.0494 | +      |
| 5-60-d   | 0.8787 | 0.0000 | + 0.8546 | 0.0310  | + 0.6967 | 0.1147 | +      |
|          |        |        | +        |         | +        |        | +      |
| 5-60-e   | 0.8237 | 0.0208 | 0.8574   | 0.0296  | 0.5813   | 0.1120 |        |
| 5-80-a   | 0.6475 | 0.0143 | + 0.6276 | 0.0482  | + 0.4677 | 0.0488 | +      |
| 5-80-b   | 0.6470 | 0.0250 | + 0.8523 | 0.0350  | + 0.4133 | 0.0417 | +      |
| 5-80-c   | 0.8275 | 0.0333 | + 0.7361 | 0.0393  | + 0.6665 | 0.0714 | +      |
| 5-80-d   | 0.8558 | 0.0458 | + 0.6980 | 0.1244  | + 0.7835 | 0.0796 | +      |
|          |        |        | +        |         | +        |        | +      |
| 5-80-e   | 0.7614 | 0.0125 | 0.8023   | 0.0000  | 0.6322   | 0.0333 |        |
| 5-100-a  | 0.9483 | 0.0083 | + 0.9217 | 0.0167  | + 0.7924 | 0.0917 | +      |
| 5-100-b  | 0.7964 | 0.0283 | + 0.7343 | 0.0767  | + 0.5742 | 0.1233 | +      |
| 5-100-c  | 0.5983 | 0.0444 | + 0.7663 | 0.1409  | + 0.6745 | 0.1937 | +      |
| 5-100-d  | 0.8598 | 0.0100 | + 0.7638 | 0.0267  | + 0.4888 | 0.1600 | +      |
|          |        |        | +        |         | +        |        | +      |
| Average  | 0.7902 | 0.0284 | 0.7848   | 0.0495  | 0.5218   | 0.0429 |        |
IncomparingtheMOGA-ALNStotheSPEA-II,itisevidentthattheMOGA-ALNS
yieldsbetterresultsthantheSPEA-II,asthesolutionsobtainedusingtheMOGA-ALNS
areallsuperiortothoseobtainedusingtheSPEA-II.Conversely,sincetheC(SPEA,GA)
valuesarealllessthanC(GA,SPEA)in20instances,itindicatesthatthesolutionsobtained
using the SPEA-II are not superior to those found using the MOGA-ALNS. Similarly,
incomparingtheMOGA-ALNStotheMOEA/D,itisobservedthatinall20instances,
thesolutionsobtainedusingtheMOGA-ALNSaresuperiortothoseobtainedusingthe
MOEA/D.Incontrast,withallinstancesshowingC(EAD,GA)valueslessthanC(GA,
EAD),thesolutionsobtainedusingtheMOEA/Darenotsuperiortothosefoundbythe
MOGA-ALNS.Similarly,bycomparingtheMOGA-ALNStotheMOEA/D-DRA,itcan
beinferredthattheMOGA-ALNSachievesbetteroutcomesthantheMOEA/D-DRA,as
themajorityofsolutionsobtainedusingtheMOGA-ALNSinall20instancesaresuperior
tothosefoundusingtheMOEA/D-DRA.Basedontheaboveanalysis,wecanconclude
thattheMOGA-ALNSexhibitsabetterabilitytofindmorenon-dominatedsolutionsand

Symmetry2024,16,1080 22of30
demonstrates superior performance in solving related problems compared to SPEA-II,
MOEA/D,andMOEA/D-DRA.
5.5.2. AnalysisoftheIGD-Metric
TheIGD-metricresultsobtainedfromtheexperimentscomparingtheMOGA-ALNS
totheotheralgorithmsarepresentedinTable7. TheMOGA-ALNSdemonstratessuperior
performance over the MOEA/D in every instance, evidenced by the lower mean and
variance in IGD-metric values for the MOGA-ALNS compared to the MOEA/D, after
conducting20trialsperinstance. Furthermore,theMOGA-ALNSissuperiortoboththe
SPEA-IIandMOEA/D-DRAin19outof20instances,asindicatedbytheloweraverage
IGD-metricvaluesoftheMOGA-ALNScomparedtothoseoftheSPEA-IIandMOEA/D-
DRA.Morespecifically,t-testresultsshowthattheMOGA-ALNSperformssignificantly
betterthantheSPEA-IIin19of20instancesandsignificantlybetterthantheMOEA/D-DRA
in16of20instances.
Table7.ExperimentalresultsobtainedusingtheIGD-metric.
MOGA-ALNS SPEA-II MOEA/D MOEA/D-DRA
Instance
Mean Var Mean Var t-Test Mean Var t-Test Mean Var t-Test
5-40-a 0.2065 0.0030 0.2411 0.0011 + 0.3199 0.0019 + 0.3630 0.0022 +
5-40-b 0.0697 0.0003 0.2794 0.0016 + 0.2995 0.0024 + 0.2411 0.0011 +
5-40-c 0.1722 0.0012 0.2538 0.0014 + 0.2764 0.0015 + 0.2674 0.0011 +
5-40-d 0.1572 0.0008 0.2361 0.0020 + 0.2110 0.0016 + 0.2097 0.0006 +
5-40-e 0.1315 0.0004 0.2647 0.0014 + 0.2763 0.0007 + 0.2065 0.0005 +
5-60-a 0.1708 0.0018 0.2783 0.0017 + 0.2598 0.0020 + 0.1805 0.0009 ∼
5-60-b 0.1740 0.0013 0.2698 0.0016 + 0.2881 0.0019 + 0.2234 0.0022 +
5-60-c 0.1501 0.0009 0.2499 0.0014 + 0.2499 0.0009 + 0.1951 0.0015 +
5-60-d 0.1309 0.0009 0.2195 0.0006 + 0.2787 0.0013 + 0.2235 0.0018 +
5-60-e 0.1714 0.0013 0.2898 0.0009 + 0.2954 0.0017 + 0.2907 0.0009 +
5-80-a 0.1799 0.0002 0.2267 0.0011 + 0.2392 0.0007 + 0.1949 0.0011 +
5-80-b 0.1808 0.0001 0.2345 0.0015 + 0.2353 0.0011 + 0.2204 0.0009 +
5-80-c 0.1938 0.0001 0.2180 0.0017 + 0.2328 0.0016 + 0.2175 0.0010 +
5-80-d 0.1642 0.0002 0.2260 0.0021 + 0.2528 0.0007 + 0.2670 0.0008 +
5-80-e 0.2110 0.0002 0.2102 0.0012 ∼ 0.2255 0.0013 + 0.2129 0.0008 ∼
5-100-a 0.1658 0.0019 0.2771 0.0019 + 0.3093 0.0026 + 0.2875 0.0021 +
5-100-b 0.1806 0.0003 0.2027 0.0008 + 0.2371 0.0007 + 0.1808 0.0007 ∼
5-100-c 0.1023 0.0002 0.1886 0.0012 + 0.2019 0.0014 + 0.1830 0.0008 +
5-100-d 0.1649 0.0002 0.1840 0.0010 + 0.1856 0.0003 + 0.1356 0.0008 −
5-100-e 0.1434 0.0002 0.1929 0.0011 + 0.1814 0.0010 + 0.1717 0.0005 +
Average 0.1610 0.0008 0.2372 0.0014 + 0.2528 0.0014 + 0.2236 0.0011 +
Byaveragingthemeansandvariancesofthe20runs,asshowninTable7,theaverage
meanvaluesfortheMOGA-ALNS,SPEA-II,MOEA/D,andMOEA/D-DRAare0.1610,
0.2372,0.2528,and0.2236,respectively,withtheaveragevariancesbeing0.0008,0.0014,
0.0014,and0.0011,respectively. Thus,theMOGA-ALNSexhibitssmalleraveragemean
andvariancevalues,outperformingthecomparativealgorithms.
Foravisualrepresentationoftheresults,Figure9displaysboxplotsforeachinstance
processedbythefourmethods. ItcanbeseenthattheresultsoftheMOGA-ALNSaremore
stableandconcentratedcomparedtothecomparativealgorithms. Theaboveresultsand
analysisoftheIGD-metricconfirmthattheMOGA-ALNScanachieveabetterapproxi-
mationandamoreuniformlydistributednon-dominatedsolutionsetwhensolvingthe
consideredproblems.
5.5.3. AnalysisofHypervolume-Metric
Theexperimentalresultsforthehypervolume-metricarepresentedinTable8. From
thistable,itisapparentthattheMOGA-ALNSsignificantlyoutperformstheSPEA-IIin19

Symmetry 2024, 16, x FOR PEER REVIEW 25 of 34
5-100-b 0.1806 0.0003 0.2027 0.0008 + 0.2371 0.0007 + 0.1808 0.0007 ~
5-100-c 0.1023 0.0002 0.1886 0.0012 + 0.2019 0.0014 + 0.1830 0.0008 +
5-100-d 0.1649 0.0002 0.1840 0.0010 + 0.1856 0.0003 + 0.1356 0.0008 −
5-100-e 0.1434 0.0002 0.1929 0.0011 + 0.1814 0.0010 + 0.1717 0.0005 +
SymmAetvryer2a02g4e, 16,10800.1610 0.0008 0.2372 0.0014 + 0.2528 0.0014 + 0.2236 0.0011
23
+
o f30
For a visual representation of the results, Figure 9 displays boxplots for each instance
pourotcoefs2se0din bsyta tnhcee sf,oausri nmdeitchaotedds.b Iyt tchaen hbige hseerenh ytpheartv tohleu mrees-umltest roifc tmhee aMnOvaGluAe-sAaLcNhiSe vaerde
musoinreg sthtaebMleO anGdA c-AonLcNenStirnattehdes ceoimnsptaanrecdes t.oC tohme cpoamrepdatroatthiveeM aOlgEoArit/hDmasn. dThMeO abEoAv/eD r-eDsuRlAts,
athnedM aOnaGlyAs-iAs LoNf tShies IsGigDni-fimceatnrtilcy csounpfierrmio rtihnat1 7thaen dM1O6GinAst-aAnLceNsS,r ceaspne acctihvieelvye. Ian bavetterearg ainpg-
pthreoxmimeaantsioann adnvda ari amnocrees uofn2if0orrmunlys, dthisetrMibOuGteAd -nAoLnN-dSosmhionwatsead lsaorgluetrioanv esreatg wehmeena snoalvnidnga
tshmea clolenrsaidveerreadg epvroabrilaenmces., indicatingbetterperformancethanthecomparativealgorithms.
FFiigguurree 99.. BBooxxpplloottss ooff tthhee IIGGDD--mmeettrriicc vvaalluueess..
FortheFriedmantest,weorderedtheMOGA-ALNS,SPEA-II,MOEA/D,andMOEA/D-
5.5.3. Analysis of Hypervolume-Metric
DRA by decreasing mean hypervolume-metric scores, assigning ranks of 1 through 4
accordingly. Subsequentcalculationoftheirmeanranksacrossallinstancesisdetailedin
Table8. Forthehypervolume-metric,theaverageranksfortheMOGA-ALNS,SPEA-II,
MOEA/D,andMOEA/D-DRAare1.1000,3.2000,2.6000,and3.1000,respectively. The
Friedmantestindicatesastatisticallysignificantdifferenceinperformanceamongthefour
algorithmsduetotheinequalityoftheiraverageranks.Additionally,theNemenyipost-hoc
test,withasignificancethresholdof0.05,isusedtoevaluatedisparities. Thevariancesin
meanranksbetweentheMOGA-ALNSandSPEA-II,MOGA-ALNSandMOEA/D,and
MOGA-ALNSandMOEA/D-DRAare2.1000, 1.5000, and2.0000, respectively. Eachof

Symmetry2024,16,1080 24of30
thesedifferencessurpassthecriticalthresholdof1.0488,signifyingstatisticallysignificant
performancedistinctionsbetweenthealgorithms.
Table8.Experimentalresultsobtainedusingthehypervolume-metric.
MOGA-ALNS SPEA-II MOEA/D MOEA/D-DRA
Instance
Mean Var Rank Mean Var Rank t-Test Mean Var Rank t-Test Mean Var Rank t-Test
5-40-a 0.8442 0.0083 1 0.8029 0.0079 3 + 0.7315 0.0153 4 + 0.8139 0.0087 2 +
5-40-b 0.7867 0.0101 2 0.6933 0.0140 4 + 0.6990 0.0211 3 + 0.8072 0.0061 1 ∼
5-40-c 0.8438 0.0022 1 0.7788 0.0145 2 + 0.7765 0.0131 3 + 0.7543 0.0064 4 +
5-40-d 0.8119 0.0131 1 0.6793 0.0120 4 + 0.7678 0.0248 2 + 0.7413 0.0057 3 +
5-40-e 0.8217 0.0097 1 0.7861 0.0135 2 + 0.7499 0.0129 3 + 0.6809 0.0079 4 +
5-60-a 0.7867 0.0106 2 0.7191 0.0195 3 + 0.8342 0.0084 1 ∼ 0.6746 0.0028 4 +
5-60-b 0.8196 0.0027 1 0.8064 0.0086 2 ∼ 0.7689 0.0089 3 + 0.7410 0.0083 4 +
5-60-c 0.8232 0.0024 1 0.7793 0.0153 2 + 0.7480 0.0259 3 + 0.7100 0.0063 4 +
5-60-d 0.8006 0.0021 1 0.7486 0.0157 4 + 0.7565 0.0145 3 + 0.7781 0.0083 2 ∼
5-60-e 0.8466 0.0060 1 0.7180 0.0094 4 + 0.7361 0.0147 3 + 0.8044 0.0088 2 +
5-80-a 0.8939 0.0089 1 0.7364 0.0074 4 + 0.7963 0.0087 2 + 0.7631 0.0106 3 +
5-80-b 0.8198 0.0023 1 0.7488 0.0064 4 + 0.8016 0.0110 3 ∼ 0.8182 0.0116 2 ∼
5-80-c 0.8641 0.0043 1 0.7834 0.0199 3 + 0.8006 0.0127 2 + 0.6968 0.0075 4 +
5-80-d 0.8354 0.0030 1 0.7983 0.0084 3 + 0.8183 0.0189 2 + 0.7729 0.0092 4 +
5-80-e 0.8456 0.0043 1 0.7583 0.0112 3 + 0.7937 0.0145 2 + 0.7237 0.0083 4 +
5-100-a 0.8317 0.0024 1 0.6763 0.0324 4 + 0.7940 0.0120 3 + 0.8087 0.0119 2 +
5-100-b 0.7985 0.0098 1 0.6820 0.0434 4 + 0.7718 0.0163 3 ∼ 0.7810 0.0143 2 ∼
5-100-c 0.8173 0.0056 1 0.7787 0.0042 2 + 0.7697 0.0102 3 + 0.6957 0.0127 4 +
5-100-d 0.9211 0.0015 1 0.6818 0.0192 4 + 0.8211 0.0156 2 + 0.7957 0.0091 3 +
5-100-e 0.8750 0.0024 1 0.6833 0.0231 3 + 0.7831 0.0171 2 + 0.6674 0.0222 4 +
Average 0.8343 0.0055 1.1000 0.7419 0.0153 3.2000 + 0.7759 0.0148 2.6000 + 0.7514 0.0093 3.1000 +
Figure10showsacurvegraphoftheFriedmantestresultsforagraphicalillustrationof
theoutcomes.Thegraphrevealsdistinctseparations,withnooverlapsbetweentheMOGA-
Symmetry 2024, 16, x FOR PEER REVIEW 27 of 34
ALNSandSPEA-II,MOGA-ALNSandMOEA/D,andMOGA-ALNSandMOEA/D-DRA.
This clear delineation emphasizes the significant performance disparities between the
MOGA-ALNSandthecomparedalgorithms.
Figure 10. Friedman test on 20 instances comparing four optimization methods based on the
Figure 10. Friedman test on 20 instances comparing four optimization methods based on the hyper-
hypervolume-metric.
volume-metric.
Additionally,Figure11presentstheboxplotsofthehypervolume-metric(HV)values
foraAllidndstiatniocnesapllryo,c Fesigseudrbey 1t1h perfoeusernatlgs otrhiteh bmosx.pFrloomts Foifg tuhree 1h1y,pitecravnobluemobese-mrveedtrtihc a(tHV) values
foinr tahlel minasjotarintyceosf cparsoesc,etshseerdes buylt sthobet afoinuerd aulsginogritthhemMsO. GFrAo-mAL FNiSguarreem 1o1r,e itc ocnacne nbtera otebdserved that
andstablecomparedtothoseofthecomparativealgorithms. Basedontheanalysispre-
in the majority of cases, the results obtained using the MOGA-ALNS are more concen-
sented, itisevidentthatthe MOGA-ALNSoutperformsthecomparativealgorithmsin
trated and stable compared to those of the comparative algorithms. Based on the analysis
solvingtheproposedproblems,demonstratingitseffectivenessandefficiencyinachieving
presented, it is evident that the MOGA-ALNS outperforms the comparative algorithms in
superiorresults.
solving the proposed problems, demonstrating its effectiveness and efficiency in achiev-
ing superior results.

Symmetry 2024, 16, x FOR PEER REVIEW 28 of 34
Symmetry2024,16,1080 25of30
FFiigguurree 1111.. BBooxxpplloottss ooff tthhee hhyyppeerrvvoolluummee--mmeettrriicc vvaalluueess..
6. Conclusions
6. Conclusions
Inviewoftheasymmetricinformationinthelocationandthedistributionstages,this
In view of the asymmetric information in the location and the distribution stages, this
studyproposesamodel,referredtoasthelocation-routingproblemwiththree-dimensional
study proposes a model, referred to as the location-routing problem with three-dimen-
loadingconstraints,specificallytailoredtooptimizingELNsintheaftermathofanearth-
sional loading constraints, specifically tailored to optimizing ELNs in the aftermath of an
quake. Iteffectivelyaddressesthecomplexityandurgencyofpost-disastermaterialdistri-
earthquake. It effectively addresses the complexity and urgency of post-disaster material
bution. OurresearchfocusesonoptimizingthedesignofELNstoensuretherapidand
distribution. Our research focuses on optimizing the design of ELNs to ensure the rapid
efficientallocationofreliefmaterialsfollowingdisasters. Byintroducingtimewindows
and efficient allocation of relief materials following disasters. By introducing time win-
andthree-dimensionalloadconstraints,thismodelconsidersnotonlythediversityofrelief
dows and three-dimensional load constraints, this model considers not only the diversity
materialsbutalsothetimelinessoftransportationinemergencysituations. Additionally,
of relief materials but also the timeliness of transportation in emergency situations. Addi-
wetakeintoaccountpotentialdisruptionsatdistributioncentersandroaddamage,thereby
tionally, we take into account potential disruptions at distribution centers and road dam-
increasingthepracticalapplicabilityofthemodel.
age, thereby increasing the practical applicability of the model.
To address this complex optimization problem, we develop the MOGA-ALNS. By
To address this complex optimization problem, we develop the MOGA-ALNS. By
combiningtheimprovedadaptivelargeneighborhoodsearchalgorithmwiththegenetic
combining the improved adaptive large neighborhood search algorithm with the genetic
algorithm,thealgorithmisbetterabletoescapelocaloptima. Animportantcontribution
algorithm, the algorithm is better able to escape local optima. An important contribution
of this study is the proposal of a practical model that provides a fresh perspective and
of this study is the proposal of a practical model that provides a fresh perspective and new
newmethodsforoptimizingELNs. Usingcasestudies,wevalidatetheeffectivenessof
methods for optimizing ELNs. Using case studies, we validate the effectiveness of the

Symmetry2024,16,1080
26of30
themodelandalgorithm,offeringrobusttheoreticalsupportandpracticalguidancefor
post-disasterrelieflogistics.
Futureresearchcanfurtherexploreapplicationsinvariousreal-worldscenarios,in-
cludingspecificresponsestrategiesfordifferenttypesofdisastersandconsiderationsof
additionalfactors,suchastrafficandweatherchanges,onlogisticaldistribution.
AuthorContributions: Conceptualization,X.P.andX.Z.;methodology,X.Z.;software,X.Z.;vali-
dation,X.P.andX.Z.;formalanalysis,X.P.;investigation,X.Z.;resources,X.P.;datacuration,X.Z.;
writingoriginaldraftpreparation,X.Z.;writingreviewandediting,X.P.;visualization,X.Z.;supervi-
sion,X.P.;projectadministration,X.P.;fundingacquisition,X.P.Allauthorshavereadandagreedto
thepublishedversionofthemanuscript.
Funding:ThisresearchwasfundedbyNationalNaturalScienceFoundationofChinagrantnum-
ber72271109.
DataAvailabilityStatement:Therawdatasupportingtheconclusionsofthisarticlewillbemade
availablebytheauthorsonrequest.
Acknowledgments:Forhelpfulcommentsanddiscussions,wethankYapingFu.
ConflictsofInterest:Theauthorsdeclarenoconflictsofinterest.
AppendixA
Themodelingprocessofthisstudyinvolvesnumerousparameters,sets,anddecision
variables,whicharecrucialforunderstandingthemathematicalmodelsandexperimental
designspresentedinthepaper. Giventheextensivenatureofthesedetails, incorporat-
ing them within the main text would potentially disrupt the coherence and readability.
Consequently,wehavechosentopresentthecompletelistinthisappendix. Tofacilitate
a better understanding and indexing for the readers, it is recommended to consult this
appendixinconjunctionwiththerelateddiscussionsinthemaintextforamorein-depth
andcomprehensivecomprehension.
TableA1.Indices,parameters,anddecisionvariablesutilizedintheformulatedmodel.
| Notation |     |     |     | Description |     |     |     |
| -------- | --- | --- | --- | ----------- | --- | --- | --- |
Indices
|     |     |     | ={i|i=1,··· |     | ,n}, |     |     |
| --- | --- | --- | ----------- | --- | ---- | --- | --- |
Setofcandidatedistributioncenters;I nindicatesthenumberofcandidate
I
distributioncenters.
J Setofdemandpoints;J ={j|j=n+1,··· ,n+m}, mrepresentsthenumberofdemandpoints.
| V   | Setofdistributioncentersanddemandpoints;V |     |     | = I∪J. |     |     |     |
| --- | ----------------------------------------- | --- | --- | ------ | --- | --- | --- |
Setofsegmentsinthedistributionnetwork;A={(i,j)|i, j∈V, i̸= j}, i,andjrepresentnodesin
A
thenetwork.
Setofdistributionvehicles;K={k|k=1,2,···h},
| K   |     |     |     | hrepresentsthetotalcountofvehicles. |     |     |     |
| --- | --- | --- | --- | ----------------------------------- | --- | --- | --- |
Setofscenarios;S={s|s=1,2,··· ,p},whereprepresentsthenumberofscenarios,eachofwhich
S
hasasetofdistributioncentersexperiencingasimultaneousdisruption.
| N   | Setofdemandpointsforvehiclekservices;k∈K. |     |     |     |     |     |     |
| --- | ----------------------------------------- | --- | --- | --- | --- | --- | --- |
k
Setofgoodstypesneededacrossalldemandpoints;C={c|c=1,...,l},whereldenotesthelth
C
typeofgoods.
Setofspacesinthedistributionvehiclecompartmentofvehiclek, D ={d|d=1,...,q},k∈K,and
| D   |                             |     |     |     |     | k   |     |
| --- | --------------------------- | --- | --- | --- | --- | --- | --- |
| k   | qistheoverallcountofspaces. |     |     |     |     |     |     |
Setofgoodsplacedinthesamespaceofthesamevehiclewithgoodcs andoverlappingwiththe
kdju
| G   | under-planeprojectionofgoodsinscenario |           |          |          |          |           |           |
| --- | -------------------------------------- | --------- | -------- | -------- | -------- | --------- | --------- |
|     | (cid:110) (cid:12)                     |           |          |          |          |           | (cid:111) |
|     | cs (cid:12)∀c∈C,                       | s∈S, k∈K, | d∈D i,j∈ | J,1≤v≤ms |          | i= j,v̸=u |           |
|     | s,G kdjv(cid:12)                       |           | k ,      |          | kd andif |           | .         |
Setofgoodsplacedinthesamespaceofthesamevehiclewithgoodcs andthebottomsurfaceof
kdju
| U   |                                        |     |     | (cid:110)    | (cid:12)       |          | (cid:111) |
| --- | -------------------------------------- | --- | --- | ------------ | -------------- | -------- | --------- |
|     | goodcs isatthesameheightinscenarios,U= |     |     | cs           | (cid:12)cs ∈G, | =z       |           |
|     | kdju                                   |     |     | kdjv(cid:12) | kdjv           | z Cskdiu | Cskdiu .  |

Symmetry2024,16,1080
27of30
TableA1.Cont.
|     | Notation |     |     |     |     | Description |     |     |     |
| --- | -------- | --- | --- | --- | --- | ----------- | --- | --- | --- |
Parameters
δ ij Distancebetweenthedepotordemandpointianddemandpointj,i, j∈ I∪J.
|     | β   | Thebasecapacityofthedistributioncenteri, |     |     |     | i∈  | I.  |     |     |
| --- | --- | ---------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
i
µ Themaximumcapacityofthedistributioncentericanbeexpanded,i∈ I.
i
|     |     | Thecostofconstructingthedistributioncenteri, |     |     |     |     | i∈ I. |     |     |
| --- | --- | -------------------------------------------- | --- | --- | --- | --- | ----- | --- | --- |
|     | γ i |                                              |     |     |     |     |       |     |     |
i∈
|     | e i | Theunitexpansioncostofthedistributioncenteri, |     |     |     |     | I.  |     |     |
| --- | --- | --------------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
|     | f   | Fixedoperatingcostofthevehicle.               |     |     |     |     |     |     |     |
|     | τ   | Thecostperunitdistancetraveledbythevehicle.   |     |     |     |     |     |     |     |
|     | ν   | Thespeedofvehicles.                           |     |     |     |     |     |     |     |
|     | O   | Themaximumloadingvolumeofthevehicle.          |     |     |     |     |     |     |     |
|     | B   | Themaximumloadcapacityofthevehicle.           |     |     |     |     |     |     |     |
layers
Theactualcountoflayersofgoodsloadedinthedthspaceofvehiclek, k∈K, d∈D .
|     | kd  |     |     |     |     |     |     |     | k   |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
rows Theactualcountofrowsofgoodsloadedinthedthspaceofvehiclek, k∈K, d∈D .
|     | kd  |     |     |     |     |     |     |     | k   |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
columns Theactualcountofcolumnsofgoodsloadedinthedthspaceofvehiclek, k∈K, d∈D .
|     | kd  |     |     |     |     |     |     |     | k   |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
ms Thecountofgoodsplacedwithinthedthspaceofvehiclekinscenarios, s∈S, k∈K, d∈D .
kd k
ms Thenumberofgoodsloadedatdemandpointjwithinregiondbydeliveryvehiclekinscenario
|     | kdj | s, s∈S, | k∈K, dϵD | , j∈ J. |     |     |     |     |     |
| --- | --- | ------- | -------- | ------- | --- | --- | --- | --- | --- |
k
qs Theindividualqualityofthegoodsloadedinregiondbydeliveryvehiclek, k∈K, d∈D .
kd k
Qs Theoverallqualityofgoodsplacedinthedthspaceofvehiclek, k∈K, d∈D .
|     | kd  |     |     |     |     |     |     |     | k   |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
σs Theoverallsizeofgoodsplacedinthedthspaceofvehiclek, k∈K, d∈D .
|     | kd  |                                                       |     |     |     |     |     |          | k   |
| --- | --- | ----------------------------------------------------- | --- | --- | --- | --- | --- | -------- | --- |
|     | cs  |                                                       |     |     |     |     |     | k∈K, d∈D |     |
|     |     | Theoverallnumberofgoodsplacedinthedthspaceofvehiclek, |     |     |     |     |     |          | k . |
kdiu
L,W,H Thedimensionsofthecarriage,includingitslength,width,andheight..
l ,w ,h Thelength,width,andheightofthedthspaceofvehiclek, k∈K, d∈D .
|     | kd kd kd |     |     |     |     |     |     | k   |     |
| --- | -------- | --- | --- | --- | --- | --- | --- | --- | --- |
ls , ws , hs Thelength,width,andheightofthegoodsloadedinthedthspaceofvehiclek, c∈C, k∈K, d∈D .
|     | kd kd kd |     |     |     |     |     |     |     | k   |
| --- | -------- | --- | --- | --- | --- | --- | --- | --- | --- |
(cid:16) (cid:17) Thecoordinateattheupper-rightcornerofthefrontsideoftheuthcarriageoftheithpointinthedth
| x Cskdju | ,y ,z Cskdju |                  |     | c∈ k∈ | d∈     | j∈ 1≤u≤ms |     |     |     |
| -------- | ------------ | ---------------- | --- | ----- | ------ | --------- | --- | --- | --- |
|          | Cskdju       | spaceofvehiclek, |     | C,    | K, D k | , J,      |     | .   |     |
kd
(cid:18) (cid:19) Thecoordinateatthelower-leftcornerofthebacksideoftheuthcarriageoftheithpointinthedth
| x   | ,y ,z |     |     |     |     |     |     |     |     |
| --- | ----- | --- | --- | --- | --- | --- | --- | --- | --- |
Cskdju Cskdju spaceofvehiclek, c∈C, k∈K, d∈D , j∈ J, 1≤u≤ms .
|     | Cskdju |                                         |     |     | k   |     |     | kd  |     |
| --- | ------ | --------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
|     | Ps     | Theprobabilityofscenariosoccurring,s∈S. |     |     |     |     |     |     |     |
Theprobabilityofsecondarydisasterssuchasaftershocksoccurringatthedistributioncenter
Ps
|     | 1i  | i, i∈ I, s∈S. |     |     |     |     |     |     |     |
| --- | --- | ------------- | --- | --- | --- | --- | --- | --- | --- |
Theprobabilityofhugelossescausedbydisasterssuchasaftershocksaffectingthedistribution
Ps
|     | 2i  | centerinscenarios, |     | s∈S, i∈ | I.  |     |     |     |     |
| --- | --- | ------------------ | --- | ------- | --- | --- | --- | --- | --- |
λs Thecostoflossesincurredbydistributioncenteriduetodisasterriskssuchasaftershocksin
|     | 1i  | scenarios, | s∈S, i∈ | I.  |     |     |     |     |     |
| --- | --- | ---------- | ------- | --- | --- | --- | --- | --- | --- |
Ps Theprobabilityoftransportationriskassociatedwiththeroutesection(i, j)inscenarios, i, j∈ A.
1ij
Ps Theprobabilityofsignificantlossofgoodsduetotransportationriskoccurringalongroutesegment
|     | 2ij | (i, j)inscenarios, |     | i, j∈ A. |     |     |     |     |     |
| --- | --- | ------------------ | --- | -------- | --- | --- | --- | --- | --- |
Thecostoflossduetotransportationriskwhengoodsaretransportedfromitojinscenario
λS
|     | 2i  | s, i, j∈ A. |     |     |     |     |     |     |     |
| --- | --- | ----------- | --- | --- | --- | --- | --- | --- | --- |
ηs Thecargoloadofvehiclekwhentransportingfromitojinscenarios, i, j∈ I∪J, k∈K, i̸= j.
ijk
ts Thetimeforvehiclektoreachpointjinscenarios, s∈S, j∈ J, k∈K.
jk
|     | ψs  |                                                        |     |     |     |     |     | s∈S, j∈ | k∈K. |
| --- | --- | ------------------------------------------------------ | --- | --- | --- | --- | --- | ------- | ---- |
|     |     | Thetimevehiclekrequirestoservedemandpointjinscenarios, |     |     |     |     |     |         | J,   |
jk
φe Thepenaltycoefficientforvehiclesarrivingatdemandpointjaheadofschedule,j∈ J.
j
φl
Thepenaltycoefficientforvehiclesarrivingatdemandpointjbehindschedule,j∈ J.
j
|     | Ts  | Theearliestacceptableservicetimefordemandpointj, |     |     |     |     | j∈  | J.  |     |
| --- | --- | ------------------------------------------------ | --- | --- | --- | --- | --- | --- | --- |
1j
|     | Ts  | Thelatestacceptableservicetimefordemandpointj, |     |     |     |     | j∈  | J.  |     |
| --- | --- | ---------------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
2j
ξs Thevalueis1ifdistributioncenterifailsinscenarios;otherwise,itis0,s∈S, i∈
|     | i   |     |     |     |     |     |     |     | I.  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Thevalueis1ifvehiclekisloadedwithclasscgoodswithinregiond;otherwise,itis0,
ω
|     | kc  | k∈K, c∈C, | d∈D | .   |     |     |     |     |     |
| --- | --- | --------- | --- | --- | --- | --- | --- | --- | --- |
k

Symmetry2024,16,1080 28of30
TableA1.Cont.
Notation Description
Decisionvariable
Thevalueis1ifadistributioncenterisestablishedatlocationiinscenarios;otherwise,itis0,
xs
i s∈S, i∈ I.
Thevalueis1ifvehiclektravelsfromnodeitonodejinscenarios;otherwise,itis0,
ys
ijk s∈S, i, j∈ I∪J, k∈K, i̸= j.
Thevalueis1ifdemandpointjisservicedbydistributioncenteriinscenarios;otherwise,itis0,
zs
ij s∈S, i∈ I, j∈ J.
Thevalueis1ifvehiclekcarriesthegoodsofdemandpointjwithinregiond;otherwise,itis0,
γs
kj s∈S, j∈ J, k∈K, d∈D
k..
Ωs
Thevalueis1ifvehiclekdepartsfromdistributioncenteritoprovidedeliveryservicesinscenarios;
ik otherwise,itis0,s∈S, i∈ I, k∈K.
ζs Thecapacityexpansionamountofdistributioncenteriinscenarios, s∈S, i ∈ I.
i
References
1. Rahmani,D.Designingarobustanddynamicnetworkfortheemergencybloodsupplychainwiththeriskofdisruptions.Ann.
Oper.Res.2018,283,613–641.[CrossRef]
2. Shen,L.;Tao,F.;Shi,Y.;Qin,R.OptimizationofLocation-RoutingProbleminEmergencyLogisticsConsideringCarbonEmissions.
Int.J.Environ.Res.PublicHealth2019,16,2982.[CrossRef][PubMed]
3. Su,Z.;Zhang,G.;Liu,Y.;Yue,F.;Jiang,J.Multipleemergencyresourceallocationforconcurrentincidentsinnaturaldisasters.Int.
J.DisasterRiskReduct.2016,17,199–212.[CrossRef]
4. Bagloee,S.A.;Sarvi,M.;Wolshon,B.;Dixit,V.Identifyingcriticaldisruptionscenariosandaglobalrobustnessindextailoredto
realliferoadnetworks.Transp.Res.PartELogist.Transp.Rev.2017,98,60–81.[CrossRef]
5. Jalali,S.;Seifbarghy,M.;Niaki,S.T.A.Arisk-averselocation-protectionproblemunderintentionalfacilitydisruptions:Amodified
hybriddecompositionalgorithm.Transp.Res.PartELogist.Transp.Rev.2018,114,196–219.[CrossRef]
6. Liu,Y.;Cui,N.;Zhang,J.Integratedtemporaryfacilitylocationandcasualtyallocationplanningforpost-disasterhumanitarian
medicalservice.Transp.Res.PartELogist.Transp.Rev.2019,128,1–16.[CrossRef]
7. Huang,C.-H.;Chang,K.-H.;Liu,C.-H.;Chang,T.-Y.;Lin,Y.-K.Networkreliabilityanalysisoncasualtyrescuefornaturaldisaster
evaluation.Ann.Oper.Res.2023,Feb10,1–21.[CrossRef]
8. Qi,M.;Yang,Y.;Cheng,C.Locationandinventorypre-positioningproblemunderuncertainty.Transp.Res.PartELogist.Transp.
Rev.2023,177,103236.[CrossRef]
9. Wang,Z.;Leng,L.;Ding,J.;Zhao,Y.Studyonlocation-allocationproblemandalgorithmforemergencysuppliesconsidering
timelinessandfairness.Comput.Ind.Eng.2023,177,109078.[CrossRef]
10. Meng,L.;Wang,X.;He,J.;Han,C.;Hu,S.Atwo-stagechanceconstrainedstochasticprogrammingmodelforemergencysupply
distributionconsideringdynamicuncertainty.Transp.Res.PartELogist.Transp.Rev.2023,179,103296.[CrossRef]
11. Zhang, J.; Long, D.Z.; Li, Y. A reliable emergency logistics network for COVID-19 considering the uncertain time-varying
demands.Transp.Res.ELogist.Transp.Rev.2023,172,103087.[CrossRef][PubMed]
12. Martins,S.;Ostermeier,M.;Amorim,P.;Hübner,A.;Almada-Lobo,B.Product-orientedtimewindowassignmentforamulti-
compartmentvehicleroutingproblem.Eur.J.Oper.Res.2019,276,893–909.[CrossRef]
13. Frank,M.;Ostermeier,M.;Holzapfel,A.;Hübner,A.;Kuhn,H.Optimizingroutinganddeliverypatternswithmulti-compartment
vehicles.Eur.J.Oper.Res.2021,293,495–510.[CrossRef]
14. Bortfeldt,A.;Yi,J.TheSplitDeliveryVehicleRoutingProblemwiththree-dimensionalloadingconstraints.Eur.J.Oper.Res.2020,
282,545–558.[CrossRef]
15. Castellucci,P.B.;Costa,A.M.;Toledo,F.Networkschedulingproblemwithcross-dockingandloadingconstraints.Comput.Oper.
Res.2021,132,105271.[CrossRef]
16. Holguín-Veras,J.;Pérez,N.;Jaller,M.;VanWassenhove,L.N.;Aros-Vera,F.Ontheappropriateobjectivefunctionforpost-disaster
humanitarianlogisticsmodels.J.Oper.Manag.2013,31,262–280.[CrossRef]
17. Afify,B.;Soeanu,A.;Awasthi,A.Separationlinearizationapproachforthecapacitatedfacilitylocationproblemunderdisruption.
ExpertSyst.Appl.2021,169,114187.[CrossRef]
18. Wang,W.;Wu,S.;Wang,S.;Zhen,L.;Qu,X.Emergencyfacilitylocationproblemsinlogistics:Statusandperspectives.Transp.
Res.PartELogist.Transp.Rev.2021,154,102465.[CrossRef]
19. Yang,Y.;Yin,Y.;Wang,D.;Ignatius,J.;Cheng,T.C.E.;Dhamotharan,L.Distributionallyrobustmulti-periodlocation-allocation
withmultipleresourcesandcapacitylevelsinhumanitarianlogistics.Eur.J.Oper.Res.2023,305,1042–1062.[CrossRef]
20. Men,J.; Jiang,P.; Zheng,S.; Kong,Y.; Zhao,Y.; Sheng,G.; Su,N.; Zheng,S.AMulti-ObjectiveEmergencyRescueFacilities
LocationModelforCatastrophicInterlockingChemicalAccidentsinChemicalParks.IEEETrans.Intell.Transp.Syst.2020,21,
4749–4761.[CrossRef]

Symmetry2024,16,1080 29of30
21. Maliki,F.;Souier,M.;Dahane,M.;BenAbdelaziz,F.Amulti-objectiveoptimizationmodelforamulti-periodmobilefacility
locationproblemwithenvironmentalanddisruptionconsiderations.Ann.Oper.Res.2022,Sep8,1–26.[CrossRef]
22. Wang,C.;Wang,Z.;Tian,Y.;Zhang,X.;Xiao,J.ADual-PopulationBasedEvolutionaryAlgorithmforMulti-ObjectiveLocation
ProblemUnderUncertaintyofFacilities.IEEETrans.Intell.Transp.Syst.2022,23,7692–7707.[CrossRef]
23. Zhang,Y.;Diabat,A.;Zhang,Z.-H.Reliableclosed-loopsupplychaindesignproblemunderfacility-type-dependentprobabilistic
disruptions.Transp.Res.PartBMethodol.2021,146,180–209.[CrossRef]
24. Zahedi,A.;Kargari,M.;HusseinzadehKashan,A.Multi-objectivedecision-makingmodelfordistributionplanningofgoods
androutingofvehiclesinemergencymulti-objectivedecision-makingmodelfordistributionplanningofgoodsandroutingof
vehiclesinemergency.Int.J.DisasterRiskReduct.2020,48,101587.[CrossRef]
25. Zhong,S.;Cheng,R.;Jiang,Y.;Wang,Z.;Larsen,A.;Nielsen,O.A.Risk-averseoptimizationofdisasterrelieffacilitylocationand
vehicleroutingunderstochasticdemand.Transp.Res.PartELogist.Transp.Rev.2020,141,102015.[CrossRef]
26. Zhang,G.;Zhu,N.;Ma,S.;Xia,J.Humanitarianreliefnetworkassessmentusingcollaborativetruck-and-dronesystem.Transp.
Res.PartELogist.Transp.Rev.2021,152,102417.[CrossRef]
27. Molina,J.;López-Sánchez,A.D.;Hernández-Díaz,A.G.;Martínez-Salazar,I.AMulti-startAlgorithmwithIntelligentNeighbor-
hoodSelectionforsolvingmulti-objectivehumanitarianvehicleroutingproblems.J.Heuristics2017,24,111–133.[CrossRef]
28. Khanchehzarrin,S.;GhaebiPanah,M.;Mahdavi-Amiri,N.;Shiripour,S.Abi-levelmulti-objectivelocation-routingoptimization
modelfordisasterreliefoperationsconsideringpublicdonations.Socio-Econ.Plan.Sci.2022,80,101165.[CrossRef]
29. Wang,Y.;Wang,X.;Fan,J.;Wang,Z.;Zhen,L.Emergencylogisticsnetworkoptimizationwithtimewindowassignment.Expert
Syst.Appl.2023,214,119145.[CrossRef]
30. Reil, S.; Bortfeldt, A.; Mönch, L. Heuristics for vehicle routing problems with backhauls, time windows, and 3D loading
constraints.Eur.J.Oper.Res.2018,266,877–894.[CrossRef]
31. Göçmen,E.;Erol,R.Transportationproblemsforintermodalnetworks:Mathematicalmodels,exactandheuristicalgorithms,
andmachinelearning.ExpertSyst.Appl.2019,135,374–387.[CrossRef]
32. Wei,L.;Zhang,Z.;Lim,A.Anevolutionarylocalsearchforthecapacitatedvehicleroutingproblemminimizingfuelconsumption
underthree-dimensionalloadingconstraints.InProceedingsofthe201410thInternationalConferenceonNaturalComputation
(ICNC),Xiamen,China,19–21August2014;pp.203–208.[CrossRef]
33. Männel,D.;Bortfeldt,A.Solvingthepickupanddeliveryproblemwiththree-dimensionalloadingconstraintsandreloadingban.
Eur.J.Oper.Res.2018,264,119–137.[CrossRef]
34. Rajaei, M.; Moslehi, G.; Reisi-Nafchi, M. The split heterogeneous vehicle routing problem with three-dimensional loading
constraintsonalargescale.Eur.J.Oper.Res.2022,299,706–721.[CrossRef]
35. Elbek,M.;Wøhlk,S.Avariableneighborhoodsearchforthemulti-periodcollectionofrecyclablematerials.Eur.J.Oper.Res.2016,
249,540–550.[CrossRef]
36. Hübner,A.;Ostermeier,M.AMulti-CompartmentVehicleRoutingProblemwithLoadingandUnloadingCosts.Transp.Sci.2019,
53,282–300.[CrossRef]
37. Yahyaoui,H.;Kaabachi,I.;Krichen,S.;Dekdouk,A.Twometaheuristicapproachesforsolvingthemulti-compartmentvehicle
routingproblem.Oper.Res.2018,20,2085–2108.[CrossRef]
38. Zbib, H.; Laporte, G. The commodity-split multi-compartment capacitated arc routing problem. Comput. Oper. Res. 2020,
122,104994.[CrossRef]
39. Yang,J.;Tao,F.;Zhong,Y.Dynamicroutingforwastecollectionandtransportationwithmulti-compartmentelectricvehicleusing
smartwastebins.WasteManag.Res.2022,40,1199–1211.[CrossRef]
40. Mohammadi,S.; AvakhDarestani,S.; Vahdani,B.; Alinezhad,A.Arobustneutrosophicfuzzy-basedapproachtointegrate
reliablefacilitylocationandroutingdecisionsfordisasterreliefunderfairnessandaftershocksconcerns.Comput.Ind.Eng.2020,
148,106734.[CrossRef]
41. Wei,X.;Qiu,H.;Wang,D.;Duan,J.;Wang,Y.;Cheng,T.C.E.Anintegratedlocation-routingproblemwithpost-disasterrelief
distribution.Comput.Ind.Eng.2020,147,106632.[CrossRef]
42. Li,Y.;Zhang,J.;Yu,G.Ascenario-basedhybridrobustandstochasticapproachforjointplanningofrelieflogisticsandcasualty
distributionconsideringsecondarydisasters.Transp.Res.PartELogist.Transp.Rev.2020,141,102029.[CrossRef]
43. Sun,H.;Wang,Y.;Xue,Y.Abi-objectiverobustoptimizationmodelfordisasterresponseplanningunderuncertainties.Comput.
Ind.Eng.2021,155,107213.[CrossRef]
44. Gao,X.;Jin,X.;Zheng,P.;Cui,C.Multi-modaltransportationplanningformulti-commodityrebalancingunderuncertaintyin
humanitarianlogistics.Adv.Eng.Inform.2021,47,101223.[CrossRef]
45. Abazari,S.R.;Aghsami,A.;Rabbani,M.Prepositioninganddistributingreliefitemsinhumanitarianlogisticswithuncertain
parameters.Socio-Econ.Plan.Sci.2021,74,100933.[CrossRef]
46. Cheng,J.;Feng,X.;Bai,X.Modelingequitableandeffectivedistributionprobleminhumanitarianrelieflogisticsbyrobustgoal
programming.Comput.Ind.Eng.2021,155,107183.[CrossRef]
47. Alem,D.; Bonilla-Londono,H.F.; Barbosa-Povoa,A.P.; Relvas,S.; Ferreira,D.; Moreno,A.Buildingdisasterpreparednessand
responsecapacityinhumanitariansupplychainsusingtheSocialVulnerabilityIndex.Eur.J.Oper.Res.2021,292,250–275.[CrossRef]
48. Peng,Z.X.;Wang,C.;Xu,W.Q.;Zhang,J.S.ResearchonLocation-RoutingProblemofMaritimeEmergencyMaterialsDistribution
BasedonBi-LevelProgramming.Mathematics2022,10,1243.[CrossRef]

Symmetry2024,16,1080 30of30
49. Ghasemi,P.;Goodarzian,F.;Abraham,A.Anewhumanitarianrelieflogisticnetworkformulti-objectiveoptimizationunder
stochasticprogramming.Appl.Intell.2022,52,13729–13762.[CrossRef]
50. Vosooghi,Z.;MirzapourAl-e-hashem,S.M.J.;Lahijanian,B.Scenario-basedredesigningofareliefsupply-chainnetworkby
consideringhumanitarianconstraints,triage,andvolunteers’help.Socio-Econ.Plan.Sci.2022,84,101399.[CrossRef]
51. Bayraktar,O.B.;Günneç,D.;Salman,F.S.;Yücel,E.ReliefAidProvisiontoEnRouteRefugees: Multi-PeriodMobileFacility
LocationwithMobileDemand.Eur.J.Oper.Res.2022,301,708–725.[CrossRef]
52. Wang, D.; Peng, J.; Yang, H.; Cheng, T.C.E.; Yang, Y. Distributionally robust location-allocation with demand and facility
disruptionuncertaintiesinemergencylogistics.Comput.Ind.Eng.2023,184,109617.[CrossRef]
53. Sheikholeslami,M.;Zarrinpoor,N.Designinganintegratedhumanitarianlogisticsnetworkforthepreparednessandresponse
phasesunderuncertainty.Socio-Econ.Plan.Sci.2023,86,101496.[CrossRef]
54. Li,J.; Chu,F.; Che,A.; Yin,Y.AThree-StageReliefNetworkDesignApproachforPredictableDisastersConsideringTime-
DependentUncertainty.IEEETrans.Intell.Transp.Syst.2023,25,5418–5434.[CrossRef]
55. Yang,R.;Li,Y.;Zhang,B.;Yang,R.Location–allocationproblemintheemergencylogisticssystemconsideringlateraltransship-
mentstrategy.Comput.Ind.Eng.2024,187,109771.[CrossRef]
56. Wang,Y.;Sun,B.Multiperiodoptimalemergencymaterialallocationconsideringroadnetworkdamageandriskunderuncertain
conditions.Oper.Res.2021,22,2173–2208.[CrossRef]
57. Wang,Y.;Wang,X.;Guan,X.;Li,Q.;Fan,J.;Wang,H.Acombinedintelligentandgametheoreticalmethodologyforcollaborative
multicenterpickupanddeliveryproblemswithtimewindowassignment.Appl.SoftComput.2021,113,107875.[CrossRef]
58. Wang,Y.;Peng,S.;Zhou,X.;Mahmoudi,M.;Zhen,L.Greenlogisticslocation-routingproblemwitheco-packages.Transp.Res.
PartELogist.Transp.Rev.2020,143,102118.[CrossRef]
59. Méndez-Fernández, I.; Lorenzo-Freire, S.; González-Rueda, Á.M. An Adaptive Large Neighbourhood Search algorithm for a
real-worldHomeCareSchedulingProblemwithtimewindowsanddynamicbreaks.Comput.Oper.Res.2023,159,106351.[CrossRef]
60. Kuo,Y.;Wang,C.-C.Avariableneighborhoodsearchforthemulti-depotvehicleroutingproblemwithloadingcost.ExpertSyst.
Appl.2012,39,6949–6954.[CrossRef]
61. Lin,S.-W.;Ying,K.-C.Minimizingmakespanandtotalflowtimeinpermutationflowshopsbyabi-objectivemulti-startsimulated-
annealingalgorithm.Comput.Oper.Res.2013,40,1625–1647.[CrossRef]
62. Zitzler,E.;Laumanns,M.;Thiele,L.SPEA2:Improvingthestrengthparetoevolutionaryalgorithm.TIKRep.2001,103,35.
63. Zhang,Q.F.;Li,H.MOEA/D:Amultiobjectiveevolutionaryalgorithmbasedondecomposition.IEEETrans.Evol.Comput.2007,
11,712–731.[CrossRef]
64. Zhang,Q.;Liu,W.;Li,H.TheperformanceofanewversionofMOEA/DonCEC09unconstrainedMOPtestinstances.InProceedings
ofthe2009IEEECongressonEvolutionaryComputation,Trondheim,Norway,18–21May2009;pp.203–208.[CrossRef]
65. Ghorai,C.;Shakhari,S.;Banerjee,I.ASPEA-BasedMultimetricRoutingProtocolforIntelligentTransportationSystems.IEEE
Trans.Intell.Transp.Syst.2021,22,6737–6747.[CrossRef]
66. Zhou,Y.W.;Liu,J.;Zhang,Y.T.;Gan,X.H.Amulti-objectiveevolutionaryalgorithmformulti-perioddynamicemergencyresource
schedulingproblems.Transp.Res.PartE-Logist.Transp.Rev.2017,99,77–95.[CrossRef]
67. Leng,L.;Zhang,J.;Zhang,C.;Zhao,Y.;Wang,W.;Li,G.Decomposition-basedhyperheuristicapproachesforthebi-objectivecold
chainconsideringenvironmentaleffects.Comput.Oper.Res.2020,123,105043.[CrossRef]
68. Rabbani,M.;Nikoubin,A.;Farrokhi-Asl,H.Usingmodifiedmetaheuristicalgorithmstosolveahazardouswastecollection
problemconsideringworkloadbalancingandservicetimewindows.SoftComput.2020,25,1885–1912.[CrossRef]
69. Li,H.;Li,G.;Jiang,Q.;Wang,J.;Wang,Z.MOEA/Dwithcustomizedreplacementneighborhoodanddynamicresourceallocation
forsolving3L-SDHVRP.SwarmEvol.Comput.2024,85,101463.[CrossRef]
70. Fu,Y.;Wang,H.;Tian,G.;Li,Z.;Hu,H.Two-agentstochasticflowshopdeterioratingschedulingviaahybridmulti-objective
evolutionaryalgorithm.J.Intell.Manuf.2018,30,2257–2272.[CrossRef]
71. Li,J.-Q.;Chen,X.-L.;Duan,P.-Y.;Mou,J.-H.KMOEA:AKnowledge-BasedMultiobjectiveAlgorithmforDistributedHybrid
FlowShopinaPrefabricatedSystem.IEEETrans.Ind.Inform.2022,18,5318–5329.[CrossRef]
72. Ding,J.;Yang,C.;Xiao,Q.;Chai,T.;Jin,Y.DynamicEvolutionaryMultiobjectiveOptimizationforRawOreAllocationinMineral
Processing.IEEETrans.Emerg.Top.Comput.Intell.2018,3,36–48.[CrossRef]
73. Hou,Y.;Fu,Y.;Gao,K.;Zhang,H.;Sadollah,A.Modellingandoptimizationofintegrateddistributedflowshopschedulingand
distributionproblemswithtimewindows.ExpertSyst.Appl.2022,187,115827.[CrossRef]
74. Pereira,D.G.;Afonso,A.;Medeiros,F.M.OverviewofFriedman’stestandpost-hocanalysis.Commun.Stat.-Simul.Comput.2015,
44,2636–2653.[CrossRef]
75. Chang,P.C.;Chen,S.H.;Zhang,Q.;Lin,J.L.MOEA/Dforflowshopschedulingproblems. InProceedingsofthe2008IEEE
CongressonEvolutionaryComputation(IEEEWorldCongressonComputationalIntelligence),HongKong,China,1–6June
2008;pp.1433–1438.[CrossRef]
Disclaimer/Publisher’sNote: Thestatements, opinionsanddatacontainedinallpublicationsaresolelythoseoftheindividual
author(s)andcontributor(s)andnotofMDPIand/ortheeditor(s).MDPIand/ortheeditor(s)disclaimresponsibilityforanyinjuryto
peopleorpropertyresultingfromanyideas,methods,instructionsorproductsreferredtointhecontent.