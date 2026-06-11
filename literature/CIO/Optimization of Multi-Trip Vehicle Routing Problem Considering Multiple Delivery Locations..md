Article
Optimization of Multi-Trip Vehicle Routing Problem
Considering Multiple Delivery Locations
WansuZou*andHuixinSong
SchoolofEconomicsandManagement,JiangsuUniversityofScienceandTechnology,Zhenjiang212100,China;
211110401205@stu.just.edu.cn
* Correspondence:232211202227@stu.just.edu.cn
Abstract
Thispaperaddressesthechallengesofimprovinglast-milelogisticsdeliverysatisfaction
inurbanareasbystudyingamulti-tripvehicleroutingproblemwithmultipledelivery
locations(MTVRPMDL).TheMTVRPMDLsimultaneouslydecidesthevisitingorderof
customersforeachvehicleandselectsanappropriatedeliverylocationforeverycustomer.
Theproblemexhibitsintrinsicspatialanddecisionsymmetries,arisingfrominterchange-
ablevehicletrips,alternativedeliverylocationsforeachcustomer,andsymmetricroute
permutations that lead to equivalent operational outcomes. A mixed-integer program-
ming model is proposed, aiming to minimize the total vehicle travel time. Within an
iteratedlocalsearchframework,amodifiedSolomongreedyinsertionheuristicsuitablefor
multi-deliveryaddressandmulti-tripsettingsisdevelopedtogenerateinitialsolutions.
Duringtheiterativesearchphase,Or-optandRelocatelocalsearchoperatorsareemployed,
togetherwithrandomswapperturbations,toenhancesolutionexploration. Computational
experimentsconfirmtheefficiencyoftheproposedmodelandalgorithm,showingthat
allowingcustomerstohavemultipledeliverylocationscansignificantlyreduceoverall
traveltimeandimprovetheflexibilityofvehicleroutingdecisions.
Keywords: multi-tripvehicleroutingproblem;multipledeliveryaddresses;mixedinteger
programming;iteratedlocalsearch
1. Introduction
Last-mile distribution constitutes a major cost component in logistics operations,
frequentlyaccountingformorethan40%oftotaltransportationexpenditures,whilealso
exertingasignificantinfluenceoncustomersatisfaction. Asaresult,thedevelopmentof
efficientvehicleroutingstrategieshasbecomeacriticaloperationaldecisionforlogistics
serviceproviders,withdirectimplicationsfordeliveryefficiency,servicereliability,andthe
AcademicEditor:CalogeroVetro sustainabilityofurbanfreightsystems.SinceitsintroductionbyDantzigandRamser[1],the
vehicleroutingproblem(VRP)hasbecomeacentraltopicincombinatorialoptimizationand
Received:20December2025
Revised:26January2026 operationsresearch. TheVRPseekstodetermineasetofroutesforafleetofvehiclesthat
Accepted:27January2026 serveacollectionofcustomerswithknowndemands,subjecttooperationalconstraintssuch
Published:28January2026 asvehiclecapacityandservicetimewindows. Theobjectiveiscommonlyformulatedas
Copyright:©2026bytheauthors. theminimizationoftotalroutingcosts,includingtraveldistanceortraveltime. Aslogistics
LicenseeMDPI,Basel,Switzerland.
operationshavegrownmorecomplexinpractice,manyextendedVRPformulationshave
Thisarticleisanopenaccessarticle
beendevelopedtobetterreflectreal-worldconditions. Prominentexamplesincludethe
distributedunderthetermsand
vehicleroutingproblemwithtimewindows(VRPTW),VRPTWwithheterogeneousfleets,
conditionsoftheCreativeCommons
Attribution(CCBY)license.
Symmetry2026,18,233 https://doi.org/10.3390/sym18020233

Symmetry2026,18,233 2of23
dynamicVRPTW,VRPTWwithsimultaneouspickupanddelivery, andelectricvehicle
routingproblems[2–6].
Urbanfreighttransportationpoliciescommonlyrestrictthecirculationoflargetrucks
incitycenters,whichhasledlogisticsoperatorstorelypredominantlyonsmalldelivery
vehiclescharacterizedbylimitedpayloadcapacityanddrivingrange. Inlast-miledistribu-
tionsystems,wherecustomersaregeographicallyscatteredandordervolumesarehigh
butindividualshipmentsaretypicallysmall,suchvehiclesareoftenrequiredtoperform
severaldepot-to-customertourswithinasingleplanninghorizon. Asaconsequence,the
designofmulti-triproutingplanshasbecomeanimportantoperationalissue,particularly
inthecontextoflarge-scaleparceldeliverysystems. Therapidgrowthofexpressdelivery
furtheramplifiesthischallenge. AccordingtodatareleasedbytheStatePostBureauof
China,thetotalnumberofexpressdeliveriesexceeded105.17billionbytheendofOctober
2023, correspondingtoayear-on-yearincreaseof17.0%[7]. Thissustainedgrowthhas
generatedacontinuousexpansionindemandforefficientlast-miledeliveryservices.
IntheChineseurbancontext,trafficmanagementpoliciesaimedatalleviatingconges-
tionandreducingenvironmentalimpactsimposestrictaccesslimitationsonheavyfreight
vehiclesincentraldistricts. Asaresult,last-miledistributionisincreasinglycarriedout
usingsmallelectricdeliverytrucks. ClassicalformulationsoftheVRPandtheVRPTW,
aswellasmanyoftheirextensions,typicallyassumethateachvehiclecompletesatmost
onerouteduringtheplanningperiod. However,thisassumptionisofteninconsistentwith
practicaloperations,asthelimitedcapacityofsmallvehiclesleadstolowutilizationrates
whenonlysingletripsareallowed. Toenhancevehicleutilizationandcontroloperating
costsunderconstrainedfleetsizes,logisticsoperatorsfrequentlyschedulemultiplereturn
tripsforindividualvehicles. Theseoperationalrealitieshavemotivatedtheextensionof
theVRPandVRPTWtotheirmulti-tripcounterparts,namelythemulti-tripvehiclerouting
problem(MTVRP)andtheMTVRPwithtimewindows(MTVRPTW).Owingtotheircloser
alignmentwithlast-miledeliverypractices,thesemodelsoffergreaterpracticalrelevance
andhaveattractedincreasingresearchinterestinrecentyears[8].
Withtheideaof“customer-oriented”graduallytakingrootinsocio-economicactivities,
logisticscompaniesareincreasinglyfocusingonimprovingtheservicequalityandon-time
performanceof“last-mile”delivery. Duetothesharpincreaseinexpressordervolumes,
delivery failures have become more frequent, including mismatches between delivery
locations and actual delivery points, or packages being lost at collection points. These
issuesmayarisefromreasonssuchasrecipientsnotbeingathome,incorrectaddresses,or
unsuitabledeliverytimes. Toaddresstheseproblems,logisticscompanieshaveintroduced
multi-deliveryaddressservices,whichbetteralignwithcustomers’dailyroutines,thereby
improving delivery success rates and customer satisfaction. Among them, UPS, DHL,
andFedExalreadyofferserviceswithmultipledeliveryoptions,suchashomedelivery,
officedelivery,ordesignatedlocationdelivery. Customerscanchoosethemostconvenient
deliveryaddressbasedontheirneedsandpreferences,ensuringtheyreceivetheirpackages
at the right time and place. From an operational perspective for logistics companies,
providing multi-delivery address services enhances the flexibility and convenience of
logisticsdistribution,optimizingdeliveryroutesandimprovingefficiency. Additionally,
customersmayopttoreceivetheirparcelsatalternativelocations,suchastheirhomesor
workplaces,allowingdeliveriestobetteralignwiththeirdailyroutines. Thispersonalized
deliveryservicehelpsboostcustomersatisfactionandstrengthensthecompetitivenessof
logisticscompanies.
Therefore,thisstudyinvestigatesthemulti-tripvehicleroutingproblemwithmultiple
deliverylocations(MTVRPMDL),takingintoaccountvehicleloadconstraints,theunique
serviceconstraintformultipledeliverylocations,timewindowconstraints,traveltime,and
https://doi.org/10.3390/sym18020233

Symmetry2026,18,233 3of23
themaximumtriptimeconstraintforvehicles. Forsmaller-scalecustomerdeliveries,the
optimizationsoftwareCPLEX12.10canbeusedtosolvetheMTVRPMDLmodel.Forlarger-
scaleinstances,tobetteraddressthisproblem,thispaperdesignsaGreedyIteratedLocal
Search(GILS)algorithmbasedontheframeworkofILS,incorporatinggreedystrategies
withtheobjectiveofminimizingthetotalvehicletraveltime. Forinitialsolutiongeneration,
we developed an improved Solomon greedy insertion algorithm tailored for scenarios
withmultipledeliverylocationsandmulti-triproutes. Duringtheiterativesearchphase,
thispaperdesignsOr-opt,Relocatelocalsearchoperatorsandrandomswapperturbation
operations. Byalternatelyapplyingtheseoperatorsforiterativesearchandupdatingbased
ontheinitialorcurrentbestsolutions,bettersolutionscanbeobtained. Computational
experimentsvalidatetheperformanceoftheproposedmodelandsolutionapproach. The
resultsshowthatallowingcustomerstohavemultipledeliverylocationoptionsenables
carrierstoplanroutesandchoosedeliveryaddressesmoreflexibly,leadingtoreductions
inbothfleetsizerequirementsandtotalvehicletraveltime. Fromatheoreticalperspective,
theMTVRPMDLpossessesseveralformsofsymmetrythatarecentraltobothmodeling
andalgorithmdesign. First,spatialsymmetryarisesfromtheexistenceofmultipledelivery
locations for each customer, where alternative locations may lead to equivalent service
outcomes under different route configurations. Second, decision symmetry exists due
to the interchangeability of vehicle trips and route segments, as permuting trips of the
samevehicleorreassigningcustomersamongfeasibletripsmaynotchangetheobjective
value. Third,thedepot-returnstructureinducestemporalsymmetryacrossmultipletrips
withintheplanninghorizon. Recognizingandappropriatelyhandlingthesesymmetriesis
crucial,asignoringthemmayleadtoredundantsearcheffortsanddegradedcomputational
performance. Thisstudyexplicitlyincorporatessymmetryconsiderationsintoboththe
mathematicalformulationandtheheuristicsolutionprocess,therebyaligningtheproposed
approachwithsymmetry-awareoptimizationprinciples.
Themaincontributionsofthispapercanbesummarizedasfollows:
(i)Newproblemdefinition: WeformallyintroducetheMTVRPMDL,which,tothe
bestofourknowledge,isthefirstmodelthatjointlyintegratesmulti-triproutingdecisions
andflexibledeliverylocationselectionwithinaunifiedlast-miledeliveryframework. This
fills a gap between the MTVRP literature and the VRP with flexible delivery locations
literature,whichhave,sofar,treatedthesefeaturesseparately.
(ii)MILPformulationwithsymmetryconsiderations: Weproposeamixed-integer
linearprogrammingmodelthatsimultaneouslydeterminesvehicletripschedulesandde-
liverylocationselectionundertimewindowandcapacityconstraints. Wefurtherhighlight
theintrinsicspatial,temporal,anddecisionsymmetriesinducedbyinterchangeabletrips
andalternativedeliverylocations,whichdistinguishthestructureofMTVRPMDLfrom
standardMTVRPandVRPvariants.
(iii)TailoredGILSheuristicforMTVRPMDL:Wedesignaproblem-specificGreedy
IteratedLocalSearch(GILS)algorithmthatexplicitlyaccountsforthepresenceofmulti-
pledeliverylocationsandmulti-tripstructures. Thisincludes(1)animprovedSolomon
greedyinsertionprocedureadaptedtoflexibledeliverylocationsandmulti-triproutes,
(2)customized Or-opt and Relocate operators that reselect delivery locations and redis-
tribute customers across trips, and (3) perturbation mechanisms that implicitly break
symmetryandenhancediversification.
(iv)Computationalevidenceandmanagerialinsights: Throughextensiveexperiments
and a direct comparison with the MTVRPTW, we demonstrate that allowing multiple
deliverylocationscansignificantlyreducetotaltraveltimeandimproveroutingflexibility.
Theseresultsprovidebothquantitativevalidationofthemodelandactionableinsightsfor
last-milelogisticsoperators.
https://doi.org/10.3390/sym18020233

Symmetry2026,18,233 4of23
Theremainderofthispaperisstructuredasfollows:Section2givesrelevantstudieson
MTVRPsandVRPwithmultipledeliveryaddresses. Section3introducestheMTVRPMDL
and presents its mixed-integer linear programming formulation. Section 4 details the
proposedGILS-basedsolutionapproach. Wepresentanddiscussthecomputationalresults
inSection5. Section6concludesthepaperandgivesfutureresearchdirections.
2. LiteratureReview
Inrecentyears,therehasbeenagrowingbodyofresearchonvariationsintheMTVRP.
For a comprehensive overview of the MTVRP and its variants, as well as the solving
algorithms,itisrecommendedtorefertothestudybyCattaruzzaetal. (2016)[8].
2.1. MTVRPandItsVariants
Since Fleischmann (1990) [9] first incorporated multiple vehicle uses into the VRP,
research on the MTVRP has gradually garnered interest among scholars in the field of
routeoptimization,particularlyinrecentyearswithinthe“last-mile”deliverysector. Vari-
antsofmulti-tripvehicleroutingproblemsoftenincorporateconstraintsonvehicletravel
time,withtheMTVRPTWbeingparticularlycommon. Typically,hardtimewindowsare
considered,meaningcarriersmustarrivebeforeorwithinthespecifiedtimewindowand
cannot be late. Macedo et al. (2011) [10], Cattaruzza et al. (2014) [11], Hernandez et al.
(2014,2016)[12,13]andFrancoisetal. (2016,2019)[14,15]haveenrichedandoptimized
algorithmsforsolvingtheMTVRPTW.Beyondtimewindows,manyscholarshaveincorpo-
ratedfactorsthataffectreal-worldtransportation. Cattaruzzaetal. (2016)[16]andLietal.
(2019) [17], while adding time window constraints, also considered the “Release date,”
afactorderivedfromurbanlogisticsanddeliverysystemsinvolvingurbandistribution
centers. Inurbanlogistics,goodsarefirstdeliveredtodistributioncentersbeforefinal-mile
delivery,sothetimegoodsarriveatthedistributioncenter(Releasedate)impactslast-mile
logistics[18]. Neiraetal. (2020)[19]proposedthatloadingtimecorrelateswiththenumber
ofcustomersvisitedduringatrip,settingloadingtimeproportionaltototalservicetime.
Traffic congestion may vary in different time periods and areas, leading to changes in
vehiclespeed. Panetal. (2021)[20]tookintoaccounttime-varyingtraveltimes,multiple
vehicletrips,andloadingtimeswiththeobjectiveofminimizingtotaltraveldistance. They
modeledthetime-varyingtimefunctionsanddurationfunctionsforcontinuousnodeseg-
mentsaspiecewiselinearfunctionsanddesignedahybridmetaheuristicalgorithmtosolve
theproblem. Huangetal. (2024)[21]presentanenhancedexactalgorithmfortheMTVRP
withtimewindowsandacapacitatedunloadingstation. Theauthorsproposeabranch-
price-and-cut framework based on a trip-based set partitioning model, incorporating a
two-phasecolumngenerationapproachwithabidirectionallabelingalgorithmtoefficiently
solvethepricingproblem. Zhangetal. (2024)[22]addressacomplexmulti-carriagetransit
trainroutingandschedulingproblemforairportbaggagehandling,modeledasaVRP
withuniquecross-routedependencies. Theproblemincorporatesseveralintricatepractical
constraints,includingsplitdemand,multipletrips,simultaneouspickupanddelivery,time
windows, baggagereleaseandwaitingtimes, andunloadingpriority. Bernardinoetal.
(2025)[23]introduceanovelMTVRPwithreleasedatesandinterrelatedperiods,motivated
by a real-world case of distributing car components to repair centers. They propose a
matheuristicemployingarolling-horizonapproachforsolvinglargerinstances.
Consideringtherestrictionsonlargetrucksinurbanareas,urbanlogisticsdistribution
isgenerallydividedintotwostages. Inthefirststage,vehiclestransportgoodstosuburban
distributioncenters,followedbythesecondstageinvolvingmulti-tripdeliveriesbyvehi-
cles. Grangieretal. (2016)[24]studiedthetwo-stageMTVRPandproposedanadaptive
largeneighborhoodsearchmethodtosolveit. Intheirresearch,Heetal. (2019)[25]treated
https://doi.org/10.3390/sym18020233

Symmetry2026,18,233 5of23
intermediate transfer stations as dynamic, framing the transportation issue of combine
harvestersasatwo-levelmulti-tripvehicleroutingproblemwithdynamictransferstations.
Basedontheproblem’scharacteristics,theydevelopedamixed-integerlinearprogram-
ming model and proposed a heuristic algorithm to address it. This study provided a
decision-makingmodelforagriculturalproductiontoimplementoptimalharvestingoper-
ations. Marquesetal. (2022)[26]examinedatwo-stageMTVRPvehicleroutingproblem
withconstraintsonunloadingandloadingsequences,involvingmultipletransferstations
wheresecond-stagevehiclesperformmulti-triptasksbetweenvarioustransferstations
andcustomers. Theyproposedamixed-integerprogrammingmodelforthisproblemand
introducedanexactalgorithmbasedonbranch-cut-and-pricetosolveit. Lehmannand
Winkenbach(2024)[27]introduceatwo-echelonmulti-tripvehicleroutingproblemwith
deliveries,pickupsandtimewindows,whichintegratesseveralreal-worldcomplexities
suchastimewindows,mixedpickupanddeliverydemands,vehiclerangeconstraints,and
multipletripsforsecond-echelonvehicles. Theauthorsproposeacompactexactformula-
tioncapableofsolvingsmallinstancestooptimalitywithinareasonabletime,alongsidea
tailoredmatheuristicdesignedformediumandlargeinstances. Thisheuristiccombines
anexactformulationforfirst-echelonroutingwithanadaptivelargeneighborhoodsearch
frameworkforthesecondechelon, demonstratingstrongperformanceinbothsolution
qualityandcomputationalefficiencywhenevaluatedonadaptedbenchmarksets. Withthe
rapiddevelopmentofintelligenttransportationsystemsandautonomousdrivingtechnolo-
gies,autonomousVRPhasattractedincreasingattentioninrecentyears[28]. Forexample,
Kashmirietal. (2024)[29]proposeanovelmulti-modaltransportationmanagementcenter
designedtointegrateautonomousvehiclesbyachievingsystemoptimalflowsacrossa
networkoveramulti-dayplanningcycle. Wangetal. (2024)[30]addressthereal-time
schedulingandroutingproblemforsharedautonomousvehicleswithafocusonleveraging
vehicle platooning at intersections to enhance urban travel efficiency. To maximize the
benefitsofSAVintegration,theauthorsproposeanovelstrategythatcoordinatesSAVsto
convergeatcorridorintersectionswithinspecifictimewindows,enablingplatoonforma-
tion. Kongetal. (2025)[31]investigateaVRPforanunmanneddeliverysystemintegrating
autonomousvehiclesanddronesundermultipledeliverymodes.
Some scholars have conducted research on the multi-trip vehicle routing problem
under multiple distribution centers, where each distribution center has its own fleet of
vehicles. Vehiclesdepartfromthedistributioncenter,visitaseriesofcustomers,andthen
returntotheoriginaldepot.Zhenetal.(2020)[18]consideredtheMTVRPwithreleasedates
atmultipledistributioncenters,aimingtominimizethetotaltraveltime. Theyconstructed
amixed-integerprogrammingmodelandproposedhybridparticleswarmoptimization
andhybridgeneticalgorithmstosolvetheproblem. Experimentalresultsshowedthat
the proposed algorithms achieved near-optimal solutions for small-scale instances and
solved large-scale cases within a reasonable time. Sahin et al. (2022) [32] studied the
MTVRP problem with multiple distribution centers, taking into account the scenario
ofheterogeneousvehicleswheresmallandlargevehicleshavedifferenttraveltimesin
certain areas. They formulated a mathematical model for the problem and proposed a
branch-and-pricealgorithmtosolveit.
2.2. VRPwithMultipleDeliveryAddresses
Tofurtherenhancetheflexibilityforcustomersandcarriers,scholarshaveconducted
researchonissuesrelatedtomultipledeliveryaddresses. Losetal. (2018)[33]considereda
variantofthepickupanddeliveryproblem,incorporatingmultiplecustomerlocationswith
timewindowsandassigningpreferencevaluestoeachlocation. Sadatietal. (2022)[34]
introducedanelectricvehicleroutingproblemwithflexibledeliveries,wherecustomers
https://doi.org/10.3390/sym18020233

Symmetry2026,18,233 6of23
couldspecifydifferentdeliveryaddressesacrossvaryingtimewindows,anddeveloped
a hybrid approach combining tabu search and variable neighborhood search to solve
it. Escudero-Santana et al. (2022) [35] studied the vehicle routing problem with multi-
pledeliveryaddressesandtimewindowsinlast-miledelivery, incorporatingcustomer
preferencestomaximizesatisfactionwhilemeetingdemands. Freyetal. (2023)[36]in-
vestigated the VRPTW and Flexible Delivery Locations. Each customer had multiple
deliveryaddresses,eachwithtimewindowsandcapacityconstraints,requiringavailabil-
ity confirmation during service. They formulated a mathematical model and designed
ahybridadaptivelargeneighborhoodsearchalgorithm,evaluatingtheutilityofflexible
deliverylocationsandcostfunctionsthroughcomputationalexperimentswhilevalidating
thealgorithm’sperformance.
Inresearchonmultipledeliveryaddresses,scholarshaveexploredcombinationsof
sharedandprivatedeliverylocations,complicatingproblem-solvingduetoconstraints
likesharedlocationcapacity. Zhangetal. (2016)[37]pioneeredtheinclusionofshared
deliverylocationsalongsideprivateoneswithtimewindows,drawingsignificantattention.
Considering that parcel lockers might reduce satisfaction compared to home delivery,
Mancinietal. (2020)[38]assumedcustomerscouldchooseeitherasharedlockerlocation,
a private address with time windows, or both, offering compensation to offset lower
satisfaction from shared locations. Dumez et al. (2021) [39] defined a vehicle routing
problemwithmultipledeliveryoptions,integratingsharedandprivatelocationswhile
accounting for preferences and time windows, designing a large neighborhood search
algorithmandgeneratingnewtestinstances. Tirkolaeeetal. (2021)[40]studiedamulti-
delivery-locationVRPwithtimewindows,incorporatingsmartlockeroptions,capacity
limits,andcustomerpreferences,solvingitwithanovelbranch-price-and-cutalgorithm.
Some scholars have also examined the roaming delivery location VRP. Reyes et al.
(2017)[41]proposedavehicleroutingproblemwithroamingdeliverylocations,simulat-
inglast-miledeliveriestocustomers’cartrunks,formulatingamathematicalmodeland
developing an improved heuristic. He et al. (2020) [42] incorporated stochastic travel
timesintoroamingdeliverylocationproblems,solvingthemwithahybridmetaheuristic.
Dragomiretal.(2022)[43]extendedtheproblemtoincludenon-overlappingtimewindows
forpickuplocationsandoverlappingonesformultipledeliveryaddressesandrecipients.
Roaming locations are typically applied in scenarios where deliveries are made to car
trunks,thoughpracticaladoptionremainslimitedduetocustomerprivacyconcerns.
Tothebestofourknowledge,thejointconsiderationofmulti-triproutingdecisions
and multiple delivery locations has not been systematically examined in the literature.
Treatingthesetwofeaturesseparatelymayleadtosuboptimalorevenmisleadingsolutions
inlast-miledeliverysystems,wheresmall-capacityvehiclesfrequentlyreturntodepots,
andcustomerscanflexiblyreceiveparcelsatdifferentlocations. Insuchsettings,delivery
locationselectionandtripschedulingareinherentlyinterdependent: thechoiceofdelivery
addressaffectsroutestructureandtripfeasibility,whiletheavailabilityofmultipletrips
alters the attractiveness of alternative delivery locations. This paper fills this gap by
introducing and studying the MTVRPMDL. The proposed model explicitly integrates
delivery location selection and multi-trip route planning within a unified optimization
framework,capturingtheirmutualinteractions. Bydoingso,thisstudyextendsboththe
MTVRPliteratureandtheresearchonflexibledeliverylocations,offeringamorerealistic
representationoflarge-scaleurbanlast-miledeliveryoperations.
3. ProblemDescriptionandFormulation
ThissectionformallydefinestheMTVRPMDLandpresentsitsMILPformulation.
https://doi.org/10.3390/sym18020233

Symmetry2026,18,233
7of23
3.1. NotationDefinition
TobetterdescribetheMTVRPMDLproblemandconstructitsmixed-integerprogram-
mingmodel,thefollowingnotationsaredefinedinTable1.
Table1.Thenotationsusedinthispaper.
|     | Sets | Disctription |                                           |     |     |     |     |     |     |
| --- | ---- | ------------ | ----------------------------------------- | --- | --- | --- | --- | --- | --- |
|     | C    | C            | = {1,2,...,m}representsthesetofmcustomers |     |     |     |     |     |     |
Thesetofnavailabledeliverylocationsofcustomerc,
|     | N c |     | (cid:8) ic,...,ic(cid:9) |     |     |     |     |     |     |
| --- | --- | --- | ------------------------ | --- | --- | --- | --- | --- | --- |
N =
|             |     | c               | 1   | n   |     |           |     |                   |     |
| ----------- | --- | --------------- | --- | --- | --- | --------- | --- | ----------------- | --- |
|             |     | Thesetofnodes,N |     |     | = N | ∪N ∪...∪N |     | . Node0represents |     |
| N∪{0,|N|+1} |     |                 |     |     |     | 1 2       |     | m                 |     |
thedepot,and|N|+1representsaduplicateofthedepot
|     |     | Thesetoftrips,R |     |     | = {1,2,...,r |     | }wherer |     | isanupper |
| --- | --- | --------------- | --- | --- | ------------ | --- | ------- | --- | --------- |
|     | R   |                 |     |     |              | UB  |         | UB  |           |
boundonthenumberoftrips
Thesetofarcs,
A
|     |     | A                         | = {(i,j)|i,j | ∈   | N∪{0,N+1}, |     | i ̸= j, | i ̸= N+1, | j ̸=0} |
| --- | --- | ------------------------- | ------------ | --- | ---------- | --- | ------- | --------- | ------ |
|     | K   | Thesetofavailablevehicles |              |     |            |     |         |           |        |
Parameters
|     | q   | Demandofeachcustomerc |     |     |     | ∈C  |     |     |     |
| --- | --- | --------------------- | --- | --- | --- | --- | --- | --- | --- |
c
|     | t   | Traveltimet                |     |     | isassociatedwitharc(i, |     |     | j)  |     |
| --- | --- | -------------------------- | --- | --- | ---------------------- | --- | --- | --- | --- |
|     | ij  |                            |     | ij  |                        |     |     |     |     |
|     | s   | Servicetimeofeachcustomerc |     |     |                        | ∈C  |     |     |     |
c
|     | (cid:2) ec,lc(cid:3) |     |     |     |     |     |     |     | ∈C  |
| --- | -------------------- | --- | --- | --- | --- | --- | --- | --- | --- |
Thetimewindowofithdeliverylocationforcustomerc
i i
|     | Q   | Capacityofeachvehicle |     |     |     |     |     |     |     |
| --- | --- | --------------------- | --- | --- | --- | --- | --- | --- | --- |
[0,T]
Theplanningperiodfordeliveryservice
|     | M   | Abigpositivenumber |     |     |     |     |     |     |     |
| --- | --- | ------------------ | --- | --- | --- | --- | --- | --- | --- |
Decisionvariables
Continuousvariable,indicatesthetimeatwhichtriprof
|     | akr | vehiclekvisitsnodesi       |     |     | ∈   | N,akr(resp.     | akr | )isthetimeat |     |
| --- | --- | -------------------------- | --- | --- | --- | --------------- | --- | ------------ | --- |
|     | i   |                            |     |     |     | 0               | N+1 |              |     |
|     |     | whichtherouterstarts(resp. |     |     |     | ends)atthedepot |     |              |     |
Binaryvariable,iftriprofvehiclektravelsthrougharc
xkr
|     | ij  | (i,                                               | j), xkr | =1;otherwise,xkr |     | =0  |     |     |     |
| --- | --- | ------------------------------------------------- | ------- | ---------------- | --- | --- | --- | --- | --- |
|     |     |                                                   | ij      |                  |     | ij  |     |     |     |
|     |     | Binaryvariable,iftriprofvehiclekvisitsvertexi,ykr |         |                  |     |     |     |     | =1; |
|     | ykr |                                                   |         |                  |     |     |     |     | i   |
|     | i   | otherwise,ykr                                     |         | =0               |     |     |     |     |     |
i
3.2. ProblemDescription
The MTVRPMDL is defined on a directed graph G = (V,A), where the vertex set
is given by V = N∪0,|N|+1 with N denoting the collection of all customer delivery
addresses,0representsthedepotand|N|+1representsaduplicateofthedepot.Thearcset
|             | = (i,j)|i,j | ∈   | ̸=   | ̸= |N|+1, |     | ̸=0.ThesetC |     | =1,2,...,mrepresents |     |
| ----------- | ----------- | --- | ---- | --------- | --- | ----------- | --- | -------------------- | --- |
| isdefinedas | A           | N,  | i j, | i         |     | j           |     |                      |     |
the customers to be served. Each customer c ∈ C has n alternative delivery addresses,
|     |     |     |     |     |     |     |     |     | (cid:8) ic,...,ic(cid:9) |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | ------------------------ |
andthesetofdeliveryaddressesforcustomerc ∈CisdenotedasN = ,with
|     |     |     |     |     |     |     |     | c   | 1 n |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
(cid:2) ec,lc(cid:3)
N ⊆ N. Eachdeliveryaddressisassociatedwithatimewindow ,indicatingthe
| c                      |     |                      |     |     |     |                                  |     | i i |     |
| ---------------------- | --- | -------------------- | --- | --- | --- | -------------------------------- | --- | --- | --- |
|                        |     | ∈Catdeliveryaddressi |     |     |     | ∈                                |     |     |     |
| timewindowforcustomerc |     |                      |     |     |     | N c . Thetransportationdemandfor |     |     |     |
customerc ∈Cisq ,andtheservicetimeiss Vehiclesmustserveeachcustomercatone
|     | c   |     |     |     | c . |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
(cid:2) ec,lc(cid:3)
oftheirdeliveryaddresseswithinthetimewindow . Ifavehiclearrivesatcustomer
|     |     |     |     |     |     | i i |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
pointiearlierthanec,itmustwaituntilec tobeginservice. Thetimewhenvehiclekstarts
|     | i   |     |     | i   |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
servingcustomercintriprisdenotedasakr.
Vehiclesarenotallowedtoservecustomerc
c
| laterthanlc. | Thetraveltimebetweeneacharc(i, |     |     |     | j)  | ∈    |                             |     |     |
| ------------ | ------------------------------ | --- | --- | --- | --- | ---- | --------------------------- | --- | --- |
|              |                                |     |     |     |     | Aist | ij ,whichisassumedtosatisfy |     |     |
i
thetriangleinequality,i.e.,t < t +t . ThedepothasKidenticalvehicleswithacapacity
|     |     | ij  | ik  | kj  |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
of Q. Thedepot’sworkingtimewindowis[0, T]. Vehiclesdepartfromthedepot,visit
severalcustomerpoints,andmustreturntothedepotbeforetimeT,withmultipletrips
allowed. ThesetoftripsforvehiclesisR = {1,...,r UB },wherer UB istheupperboundon
=0,
thenumberoftripsavehiclecanperform. Withoutlossofgenerality,thispapersetsq 0
| s =0,andt | =0.  |     |     |     |     |     |     |     |     |
| --------- | ---- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0         | 0N+1 |     |     |     |     |     |     |     |     |
https://doi.org/10.3390/sym18020233

Symmetry2026,18,233
8of23
TobetterillustratetheMTVRPMDLproblemstudiedinthispaper,anexamplewill
beusedtobrieflyexplaintheissue. Thisexamplesimulatesthelast-milevehicledelivery
scenario in real-life practice, as shown in Figure 1. The example depicts the delivery
process of two vehicles. The depot operates from 8:00 to 20:00, and the vehicles need
to serve 12customers. Each customer has two delivery addresses, representing their
home, workplace, or a third social location. Each delivery address is associated with a
timewindow. Thevehiclesdepartfromthedepotandfollowtheoptimalroutetovisit
unservedcustomersinsequence. Onlyonedeliveryaddresspercustomerisprovidedwith
door-to-doordeliveryservice,andthevehicleseventuallyreturntothewarehouse. During
thisprocess,multipleroundtripsbetweenthedepotandcustomersareallowed. Inthe
example,VehicleV1completes3trips,whileVehicleV2completes2trips. Theroutefor
|                      |       | →6→3→ |        | →1→4→ |           | →2→7→5→ |        |     |
| -------------------- | ----- | ----- | ------ | ----- | --------- | ------- | ------ | --- |
| VehicleV1is:         | Depot |       | Depot  |       | Depot     |         | Depot. | The |
| routeforVehicleV2is: |       | Depot | →9→10→ | Depot | →8→11→12→ |         | Depot. |     |

Figure1.AschematicdiagramoftheMTVRPMDL.
ThispaperconsidersthefollowingassumptionsfortheMTVRPMDL:
• Thereisasingledepot. Eachvehicletripdepartsfromthedepot,servestheassigned
customernodesalongitsplannedroute,andfinallyreturnstothedepot.
• Thedemandofcustomersisknown.
• Onlyoneofthemultipledeliveryaddressesofeachcustomercanbeserved.
• ThetotalcargovolumeofeachtripcannotexceedthevehicleloadcapacityQ.
• Customersarenotallowedtobeabsentduringthetimewindowatthedeliveryaddress.
•
Vehiclescannotbelatewhenprovidingservicestocustomers.
3.3. ModelFormulation
WedevelopthefollowingMILPmodel,theMTVRPMDL.
|     |     |     | MinZ | = ∑ t       | ∑ ∑   | xkr |     |     |
| --- | --- | --- | ---- | ----------- | ----- | --- | --- | --- |
|     |     |     |      | ij          |       | ij  |     | (1) |
|     |     |     |      | (i,j)∈A k∈K | r∈R   |     |     |     |
|     |     |     | ∑ ∑  | ∑ ykr =1,   | ∀c ∈C |     |     |     |
|     |     |     |      | i           |       |     |     | (2) |
k∈Kr∈Ri∈Nc
|     | ∑       | xkr | ∑ xkr   | ykr,∀i     |        |        |       |     |
| --- | ------- | --- | ------- | ---------- | ------ | ------ | ----- | --- |
|     |         | =   |         | = ∈        | N∪{0}, | k ∈ K, | r ∈ R |     |
|     |         | ij  |         | ji i       |        |        |       | (3) |
|     | j∈N\{i} |     | j∈N\{i} |            |        |        |       |     |
|     |         | ∑   | q ∑     | ykr ≤ Q,∀k | ∈ K, r | ∈ R    |       |     |
|     |         |     | c       | i          |        |        |       | (4) |
|     |         | c∈C | i∈Nc    |            |        |        |       |     |
https://doi.org/10.3390/sym18020233

Symmetry2026,18,233
9of23
|       |     |         |         |         | (cid:32) |         |       | (cid:33) |         |     |
| ----- | --- | ------- | ------- | ------- | -------- | ------- | ----- | -------- | ------- | --- |
| akr+s |     | + ∑     | ∑ t xkr | ≤ akr+M |          | 1− ∑    | ∑ xkr | ,∀c      | ∈C∪{0}, |     |
| c     | c   |         | ij ij   | c′      |          |         |       | ij       |         |     |
|       |     | i∈Ncj∈N |         |         |          | i∈Ncj∈N |       |          |         | (5) |
|       |     |         | c′      |         |          |         | c′    |          |         |     |
c′
|       |     |      |         | ∈C\{c}, | k        | ∈ K, r ∈ | R        |     |              |     |
| ----- | --- | ---- | ------- | ------- | -------- | -------- | -------- | --- | ------------ | --- |
|       |     |      |         |         | (cid:32) |          | (cid:33) |     |              |     |
| akr+s |     | ∑    | xkr akr |         |          | ∑ xkr    |          |     |              |     |
|       | c + | t    | ≤       | +M      | 1−       |          | ,∀c      | ∈C, | k ∈ K, r ∈ R | (6) |
| c     |     | i0   | i0      | |N|+1   |          |          | i0       |     |              |     |
|       |     | i∈Nc |         |         |          | i∈Nc     |          |     |              |     |
|       |     |      | akr     | akr     |          |          |          |     |              |     |
|       |     |      | ≤       |         | ,∀k ∈    | K, r ∈   | R\{n}    |     |              | (7) |
|       |     |      | 0       | |N|+1   |          |          |          |     |              |     |
|       |     |      | akr     | k(r+1)  |          |          |          |     |              |     |
|       |     |      |         | ≤ a     | ,∀k      | ∈ K, r ∈ | R\{m}    |     |              | (8) |
|       |     |      | |N|+1   | 0       |          |          |          |     |              |     |
|       |     |      | akr     | ≤       | T,∀k     | ∈        | ∈        |     |              |     |
|       |     |      |         |         |          | K, r     | R        |     |              | (9) |
|N|+1
|     | ∑    | ec ∑    | xkr ≤ akr | ≤ ∑    | lc      | ∑ xkr,       | ∀c ∈C, | k ∈ | K, r ∈ R |      |
| --- | ---- | ------- | --------- | ------ | ------- | ------------ | ------ | --- | -------- | ---- |
|     |      | i       | ij        | c      | i       | ij           |        |     |          | (10) |
|     | i∈Nc | j∈N\{i} |           | i∈Nc   | j∈N\{i} |              |        |     |          |      |
|     |      | akr     | ≥0,∀k     | ∈ K, r | ∈ R,    | c ∈C∪{0,N+1} |        |     |          | (11) |
c
xkr
|     |     | ∈ {0,1},∀k |     | ∈ K, r | ∈ R, | i ∈ N∪{0}, | j   | ∈ N∪{0} |     | (12) |
| --- | --- | ---------- | --- | ------ | ---- | ---------- | --- | ------- | --- | ---- |
ij
|     |     | ykr | ∈ {0,1},∀k |     | ∈ K, r | ∈ R, i | ∈ N∪{0} |     |     | (13) |
| --- | --- | --- | ---------- | --- | ------ | ------ | ------- | --- | --- | ---- |
i
Theobjectivefunction(1)minimizesthetotaltraveltimeofvehicles. Constraint(2)
ensuresthatamongmultipledeliverylocationsofeachcustomer,onlyonedeliverylocation
is visited by a vehicle and is served in exactly one trip of one vehicle. Constraint (3)
∖{0}is
enforcesflowbalancealongeachroute. Specifically,ifadeliverylocationi ∈ N
visitedduringther-thtripofvehiclek,thenumberofarcsenteringnodeimustequalthe
numberofarcsleavingit. Whenicorrespondstothedepot0,theconstraintensuresthatthe
numberofincomingarcsequalsthenumberofoutgoingarcsatthedepot. Constraint(4)
restrictsthetotaldemandservedineachtripofavehicletobewithinthevehiclecapacity
Q. Constraints (5) and (6) define the relationship between the arrival times at points i
andjwhentheyaresequentiallyvisitedinther-thtripofavehicle,thatis,whenxkr =1.
ij
Constraints(7)and(8)ensuretemporalconsistencybetweentrips: foreachvehiclek,the
departuretimefromthedepotintriprcannotexceedthecorrespondingreturntime,and
thereturntimeattheendoftriprmustbenolaterthanthedeparturetimeatthebeginning
oftripr+1. Constraint(9)limitsthecompletiontimeofeachvehicletriptonotexceed
theplanninghorizon T. Constraint(10)requiresthatwhenvehicle k servescustomer c
in trip r, the service must be provided within the time window of its delivery address.
Constraints(11)–(13)definethevaluerangesofthedecisionvariablesakr,xkr,andykr.
|     |     |     |     |     |     |     |     |     | c ij | i   |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | ---- | --- |
Theproposedformulationadmitsmultiplesymmetricoptimalsolutionsduetoin-
terchangeable vehicle trips and alternative delivery location choices for each customer.
(1)Vehicle-indexsymmetry: Inparticular,iftwovehiclesexecutedifferentsetsoftripsand
routeswiththesametotaltraveltimeandfeasibility,thensimplyswappingtheirvehicle
indicesproducesadistinctMILPsolutionthatisoperationallyidentical. Thefollowing
Constraint(14)isasymmetry-breakingconstraintthatremovesvehicle-indexsymmetry.
Thisconstraintensuresthatthelower-indexedvehiclesareusedfirst. (2)Delivery-location
symmetry: Whenacustomerhasmultiplefeasibledeliveryaddresseswithsimilartime
windowsandspatialpositions,selectingdifferentaddressesmayleadtonearlyidenticalor
identicalroutecosts,againgeneratingmultipleequivalentoptimalsolutions. Thesesym-
metriesdonotaffectoptimalitybutsignificantlyenlargethefeasiblesolutionspace,thereby
weakeningLPrelaxationsandslowingconvergence. WhiletheMILPmodelpreservesall
https://doi.org/10.3390/sym18020233

Symmetry2026,18,233 10of23
symmetricsolutions,theheuristicapproachintroducedinSection4isspecificallydesigned
tonavigatesymmetricneighborhoodsefficientlyandreduceredundantexplorations.
∑ ∑ xkr ≥ ∑ ∑ x (k+1)r ,∀k =1,...,|K|−1
ij ij (14)
r∈R(i,j)∈A r∈R(i,j)∈A
4. GILSAlgorithmfortheMTVRPMDL
Compared to the MTVRP and its variants, including MTVRPMTW, which is an
NP-hardproblem,solvingMTVRPMDLismorecomplex. MTVRPMDLconsidersprovid-
ingcustomerswithmultipledeliveryaddresses,whichmeansthenumberofaddresses
involvedinplanningdoublesorevenmultipliescomparedtothestandardvehiclerouting
problem. MTVRPMDL must ensure that each customer is served at only one delivery
addressandthatserviceisprovidedwithintheassociatedtimewindow. Whentheproblem
sizeislarge,optimizationsolvers(suchasCPLEX,Gurobi)struggletofindanexactsolution
fortheMTVRPMDLproblemwithinashorttime. Therefore,tosolvetheMTVRPMDL
problemmoreefficiently,problem-specificheuristicscanbedesignedtoaddresstheunique
challengesofMTVRPMDL.ILSisasimpleyetrobustandefficientmetaheuristic[44]. Its
fundamentalprincipleinvolvesstartingfromaninitialsolution,whichisthenimproved
throughalocalsearchprocedure. Theresultinglocallyoptimizedsolutionissubsequently
perturbedtoescapelocaloptima,afterwhichlocalsearchisappliedagain.Thiscycle—local
searchfollowedbyperturbation—isrepeatediteratively,witheachiterationusingtheout-
comeoftheprevioussearchasthenewstartingpoint,untilapredefinedstoppingcondition
issatisfied. ILShasbeensuccessfullyemployedtosolveavarietyofcombinatorialopti-
mizationproblems,includingthetravelingsalesmanproblem[45–47]andtheVRPalong
with its variants [48–51]. Based on the ILS algorithm framework, this paper designs a
tailoredGILSalgorithmfortheMTVRPMDLwiththefollowingspecificsteps:
Step1: GenerateaninitialsolutionusingSolomon’sgreedyinsertionalgorithm.
Step2: Beforetheterminationcriteriaaremet,thefollowingstepsareexecuted:
Localsearch: ThecurrentsolutionisrefinedusingOr-optandRelocateoperators. The
Or-optoperatoraimstominimizethetotaltraveltimeofthevehicles,yieldingalocally
improvedsolution.TheRelocateoperatorthenworksonthissolutiontoreducethenumber
ofvehiclesused.
Perturbation: Ifthecurrentsolutionbecomestrappedinalocaloptimum,aRandom
Exchangeperturbationisappliedtoescapeitanddiversifythesearch.
Terminationcriteria: Thealgorithmterminateswhenthenumberofiterationsexceeds
aspecifiedthreshold. Upontermination,thebestsolutionfoundisreturned.
4.1. GILSProcedure
Algorithm 1 presents the overall framework of the GILS heuristic for solving the
MTVRPMDL. The stopping criterion is defined by a maximum number of iterations,
denoted as Max_IT. Once this limit is reached, the algorithm terminates and returns
the best solution found. The GILS procedure operates as follows. An initial solution
is first generated using the improved Solomon greedy insertion algorithm (Steps 1–3).
The algorithm then enters the local search phase, where the Or-opt operator is applied
to refine vehicle routes, while the Relocate operator is used to reduce the number of
vehiclesandfurtherimprovetotaltraveltime(Steps4–12). Theseoperators,togetherwith
theperturbationmechanisms,arestructuredtobreaksymmetryimplicitlybyreselecting
deliverylocations,reorderingtripsequences,andredistributingcustomersacrosstrips,
therebypromotingdiversificationwhilepreservingfeasibility. Whennofurtherreduction
inthenumberofvehiclescanbeachieved,thesearchisconsideredtohavereachedalocal
optimum. Atthisstage,perturbationstrategiesaretriggered,includingarandomexchange
https://doi.org/10.3390/sym18020233

Symmetry2026,18,233
11of23
operation(Steps13–15)andastronger2-opt*perturbation(Steps16–17). Subsequently,
solutionsusingtheminimumnumberofvehiclesareselected,andanExchangeprocedure
is applied to further optimize their routing structures. Acceptance and selection rules
are based solely on the number of vehicles and total travel time, not on trip indices or
addresslabels,whichpreventsthealgorithmfromtreatingsymmetricencodingsasdistinct
high-qualitysolutions. Finally,thesolutionwiththelowesttotaltraveltimeamongthis
subsetisreturned(Steps18–24).
| Algorithm1: | TheGILSfortheMTVRPMDL |     |     |     |
| ----------- | --------------------- | --- | --- | --- |
Input: InstanceoftheMTVRPMDL,maximumiterationnumberMax_ITandmaximum
perturbationcountG
Output: Deliverylocationselectionforeachcustomer,vehicleroutes,Totalvehicle
traveltime
1: Generateinitialsolutions byimprovedSolomoninsertionmethod//seeSection4.2
0
| 2: DefineStobetheLocaloptimalsolutionset, |     |     | S ← {} |     |
| ----------------------------------------- | --- | --- | ------ | --- |
3: Thebestsolutions*←s ,Iterationcount t ←0,Perturbationcount g ←0
0
| 4: whilet<Max_IT | andg<Gdo          |                  |     |     |
| ---------------- | ----------------- | ---------------- | --- | --- |
| 5:               | t ← t+1           |                  |     |     |
| 6:               | Updates*←Or-opt(s | )//seeSection4.3 |     |     |
0
| 7:  | UpdateS←S∪s* |     |     |     |
| --- | ------------ | --- | --- | --- |
s′
| 8:  | ←Relocate(s*)//seeSection4.3 |     |     |     |
| --- | ---------------------------- | --- | --- | --- |
ifvehiclenumberofs′
| 9:  |                  | <vehiclenumberofs*then |      |     |
| --- | ---------------- | ---------------------- | ---- | --- |
| 10: | s*←s′,initialize | S ← {},initialize      | t ←0 |     |
| 11: | continue         |                        |      |     |
| 12: | else             |                        |      |     |
Randomexchange(s′)//seeSection4.4
Perturbationoperation:
13:
← g+1
g
| 14: | Acceptallperturbationsolutions*←s′ |     |     |     |
| --- | ---------------------------------- | --- | --- | --- |
| 15: | endif                              |     |     |     |
Strongperturbationoperation2-opt*(s′)//seeSection4.4
16:
17: endwhile
| 18: s ← | TheminimumnumberofvehiclesfromsetS |     |     |     |
| ------- | ---------------------------------- | --- | --- | --- |
v
| 19: S*←{s | ∈ S |vehiclenumberof(s | )=min(vehiclenumber) |     | s } |
| --------- | ---------------------- | -------------------- | --- | --- |
|           | i                      | i                    |     | v   |
20: forsinS*do
| 21: | Optimizevehiclerouting: | Exchange(s) |     |     |
| --- | ----------------------- | ----------- | --- | --- |
22: endfor
23: s*←solutioninS*withminimumtraveltimes
24: Returns*
4.2. InitialSolutionGeneration
Before constructing an initial solution for the MTVRPMDL, several preprocessing
stepsarerequired: (1)Noderepresentation: Treateachdeliveryaddress(customerdelivery
point)asanode,andalsotreatthewarehouselocationasanode. Allthesenodestogether
form the solution space of the problem. (2) Distance matrix calculation: Calculate the
distancesbetweenallnodes,includingthedistancesfromthewarehousetoeachnodeand
themutualdistancesbetweennodes. Thisdistanceinformationwillhelpdeterminethe
vehicletraveltimecostinrouteplanning.
TheimprovedSolomongreedyinsertionalgorithmusedtogeneratetheinitialsolution
fortheMTVRPMDLproceedsasfollows:
| Step1: | Initializationofcustomerdeliveryaddresses. |     |     |     |
| ------ | ------------------------------------------ | --- | --- | --- |
https://doi.org/10.3390/sym18020233

Symmetry2026,18,233 12of23
Foreachcustomerwithmultipledeliveryaddresses,firstdeterminewhichdelivery
addressshouldbeprioritizedastheinitialdeliveryaddressforthecustomer. Todothis,
wesortthecustomer’sdeliveryaddressesbasedontheirdistancefromthewarehouseand
selecttheaddressclosesttothewarehouseastheinitialdeliveryaddress.
Step2: Initializationofvehicleroutes.
Avehiclerouteisinitializedbyincludingthedepot,theinitialdeliveryaddressofa
selectedseedcustomer,andacopyofthedepotasthereturnnode. Theseedcustomeris
chosenastheonewhoseinitialdeliveryaddressisfarthestfromthedepot.
Step3: Routeconstruction.
Startingfromtheseednode,thevehiclerouteisextendedusingagreedyinsertion
strategy. Whilerespectingvehiclecapacityconstraintsandcustomertimewindows,the
algorithm iteratively selects the most suitable unvisited customer, determines the best
delivery address for that customer, and identifies the optimal insertion position in the
currentroute. Thisprocessfollowstwodecisionrules.
Rule1: ThisruleislargelyconsistentwiththeILS-basedinsertionstrategyproposed
byWuetal. (2024)[52]. Foreachunvisitedcustomerpointu,thealgorithmevaluatesall
feasibleinsertionpositionsinthecurrentroutetodeterminetheoptimalpredecessorand
successornodes, denotedbyi(u) and j(u), basedonEquations(15)–(18). Equation(15)
minimizesthetimecostwheninsertingcustomeru. Bysequentiallytestingallinsertion
positions, subject to capacity and time window feasibility, the algorithm identifies the
optimal insertion location and the corresponding time window. Here, ρ represents the
indexofpointsintheexistingroute,and m representsthetotalnumberofnodesinthe
route, including the depot copy. Equation (16) defines a weighted combination of the
increaseintraveltimeandtheadditionalservicedelaycausedbyinsertingcustomeru,
which together quantify the time-related cost of the insertion. The parameters α and
1
α denotethecorrespondingweightcoefficients. Equation(17)measurestheadditional
2
traveldistanceresultingfrominsertingcustomer u, where t representsthetraveltime
ij
betweennodesiandj,andµistheweightassignedtothetraveltimebetweentheselected
insertionpositionsi(u)and j(u). Equation(18)capturestheshiftinservicestarttimeof
thesubsequentnodeduetotheinsertion,whereb andb denotetheservicestarttimesof
j ju
thatnodebeforeandafterinsertingcustomeru,respectively.
(cid:8) (cid:0) (cid:1)(cid:9)
c 1 (i(u),u,j(u)) = min c 1 i ρ−1 ,u,j ρ , ρ =1,2,...,m (15)
c (i,u,j) = α c (i,u,j)+α c (i,u,j), α +α =1; α ≥0, α ≥0 (16)
1 1 11 2 12 1 2 1 2
c (i,u,j) = t +t −µt , µ ≥0 (17)
11 iu uj ij
c (i,u,j) = b −b (18)
12 ju j
Rule2: BasedontheoptimalinsertionpositiondeterminedbyRule1, wecompre-
hensivelyconsiderthedistancebetweentheinitialdeliveryaddressofcustomerpointu
and the depot, prioritizing the insertion of delivery addresses that are farther from the
warehousetomaximizerouteefficiencyandminimizetotaltravelcosts. Specifically,we
define Equations(19)and(20) to represent the vehicle’s travel costs before and after in-
serting point u, where d denotes the distance between the initial delivery address of
0u
customerpointuandthedepot,andλrepresentsthecoefficientofd ,whichisusedto
0u
calculatethedistancecostgeneratedbyinsertingtheinitialdeliveryaddressofpointu.
Equation(18)usesEquation(19)toidentifythecustomerpointwiththehighestc value
2
amongallunvisitedcustomers’initialdeliveryaddressesastheoptimalinsertionpoint.
c (i(u∗),u,j(u∗)) = max{c (i(u),u,j(u))} (19)
2 2
https://doi.org/10.3390/sym18020233

Symmetry2026,18,233 13of23
c (i(u),u,j(u),) = λd −c (i,u,j) (20)
2 0u 1
Select the best customer point from the unvisited ones and insert it at its optimal
insertionposition,applyingagreedystrategyduringinsertion. Calculatethestartservice
time for each delivery address after insertion based on the distance between the best
customer point u and the previous node, as well as the time window of the delivery
address. Prioritizethedeliveryaddresswiththeearlieststartservicetime. Continuously
updatetherouteinformationduringinsertiontoensuretheconstructedvehicleroutemeets
the vehicle load capacity and does not violate customer time windows. The insertion
selectsonedeliveryaddresspercustomerbasedondepotproximityandfeasibility,thereby
collapsing many delivery-location-symmetric alternatives at the construction stage. If
no feasible customer can be selected for further insertion, a virtual depot is inserted to
terminatethecurrenttripandinitiateanewone. Thisprocesscontinuesuntilnoadditional
tripscanbecreated. Anewvehicleisthenintroduced,andtheprocedureisrepeateduntil
allcustomershavebeenserved.
4.3. LocalSearch
IntheMTVRPMDLproblem,eachcustomerpointhasmultipledeliveryaddresses,so
wheninsertingacustomerpointintoaroute,multipleattemptscanbemade,prioritizing
theselectionoftheoptimaldeliveryaddressforinsertion. Thisremovalandreinsertion
operationofcustomerpointscaneffectivelyexpandthelocalsearchscope,increasesearch
diversity,andimprovesolutionquality.IntheGILSalgorithmfortheMTVRPMDLproblem,
wefirstusetheOr-optoperatortoperformlocalsearchwithinasingleroutetobroadenthe
searchrange. Subsequently,theRelocateoperatorisemployedtooptimizesearchesboth
withinasinglerouteandbetweendifferentroutes,aimingtofurtherrefinethesolutions
obtainedfromtheOr-optlocalsearchandescapelocaloptima. TheroleoftheRelocate
operatoralsoincludesreducingvehicletraveltimecostsandminimizingthenumberof
vehiclesused,therebycomprehensivelyoptimizingthedeliveryplan.
Or-optOperator: Or-optoperatorisoneofthecommonlyusedlocalsearchoperators
in vehicle routing optimization problems. The Or-opt operator in the GILS algorithm
forMTVRPMDLfocusesonreducingroutecosts, reconstructingthecurrentroute, and
reselectingdeliveryaddressesforallcustomerpointsinthereconstructedroutetogenerate
acandidatesolutionsetforlocalsearch.Specifically,theimplementationstepsoftheOr-opt
operatorintheMTVRPMDLproblemincluderemovingthreesub-pathsfromtheoriginal
route,cyclicallyswappingtheendpointsofthesesub-paths,andconnectingthemtoforma
completenewroute. Thisnewrouteundergoesaninitializationprocesswherethenearest
feasibledeliveryaddress,withinthetimewindoworbeforeit,issequentiallyselectedfor
eachpoint. Whenthevehiclereachesitsmaximumloadcapacity,itreturnstothedepot
andstartsanewtrip,repeatingtheprocessuntilthevehicleservesthelastcustomeron
therouteandreturnstothedepot. Aftercomputingthetotaltraveltimeofeachfeasible
solution,therouteisupdatedifanimprovementisobtained,andthesearchthenmovesto
thenextroute.
RelocateOperator: TheRelocateoperatoremploystwostrategiesintheGILSalgo-
rithmforsolvingMTVRPMDL:oneinvolvesadjustmentswithinasinglepath,whilethe
othermodifiesbetweendifferentpaths. Figures2and3illustratetheimplementationof
the Relocate operator in this algorithm. In route R, “△” represents the depot, and “ ”
representsthecustomer. (cid:35)
Fortheintra-routeoperationsforFigure2,thedetailedstepsoftheRelocateoperator
areasfollows: foreachrouteinthecurrentsolution, performthefollowingoperations
sequentially—takeoutarouteRfromthesolution,removecustomersintheorderofvehicle
service,andattempttoinserteachdeliveryaddressoftheremovedcustomersintoother
https://doi.org/10.3390/sym18020233

Symmetry2026,18,233 14of23
positionsintherouteonebyone,checkingthefeasibilityoftheroute. Iffeasible,calculate
thetotaltraveltimeofthevehicleforeachnewsolution,compareallsolutionstofindthe
onethatreducesthetotaltraveltimethemost,andacceptandupdatetherouteaccordingly.
Figure2.AnillustrationofRelocateOperatorwithinroute.
Figure3.AnillustrationofRelocateOperatorbetweendifferentroutes.
Intheinter-routeoperationsforFigure3,theRelocateoperatortransferscustomer
pointsfromonevehicle’sroutetoanothertooptimizetheoverallvehicleschedulingplan.
Therefore,duringimplementation,multipledeliveryaddressesofeachremovedcustomer
needtobeinsertedintodifferentpositionsinotherroutesonebyone,prioritizingsolutions
that reduce the number of vehicles used, followed by those that reduce the total travel
time. Thiscomplexprocessensuresanimprovementintheoverallefficiencyofthevehicle
schedulingplan. TheOr-optandRelocateoperatorsreconstructrouteswhilereselecting
delivery addresses and redistributing customers across trips, which naturally merges
symmetricsolutionsintoasinglerepresentativeconfiguration.
4.4. PerturbationOperation
To ensure that the perturbation operation can cover a broader solution space and
increasethechancesoffindingbettersolutions,weneedtodesignmoreflexibleanddiverse
perturbationstrategiestofullyexploredifferentsolutions. Toavoidprematureconvergence
tolocaloptima,acertainlevelofrandomnessorheuristicguidanceisintroducedintothe
perturbation phase, enabling the search to escape local optima and continue exploring
improvedsolutions. FortheMTVRPMDLproblem,thispaperdesignsweakandstrong
perturbationstrategies. Amongthem,theweakperturbationadoptstheRandomexchange
method,whilethestrongperturbationemploysthe2-opt*method. Figure4illustratesa
schematicdiagramofthe2-opt*implementation.
Figure4.Anexampleof2-opt*perturbationoperation.
Theweakperturbation’sRandomExchangesharesthesamefundamentalapproach
astheperturbationoperationforsolvingMTVRPMTWinWuetal. (2024)[52],withthe
differencebeingthatwhenexchangingcustomernodes,multipledeliverableaddressesof
theexchangednodesmustbeconsidered. Theselectionisbasedonthecalculationoftravel
https://doi.org/10.3390/sym18020233

Symmetry2026,18,233 15of23
timecosts,choosingthefeasibledeliveryaddresswiththelowestpost-exchangecost.2-opt*
isoneofthecommonmethodsinthefieldofvehiclerouteoptimization. Itsbasicideaisto
crosstwoexistingroutestooptimizethevehiclepath. Thespecificimplementationprocess
of2-opt*inthisalgorithmisasfollows: sequentiallyselecttworoutesfromthecurrent
solution,performallpossiblecrossoveroperations,andcheckthenewlygeneratedroutes
post-crossovertodetermineiftheyarefeasiblesolutions. Iffeasible,recordthereduction
intimecostcomparedtotheoriginalroutes,andexecutethe2-opt*operationthatyields
thegreatestreductionintimecost. Itshouldbenotedthat,intheMTVRPMDL,the2-opt*
operatorpreservestheoriginaldeliveryaddressassignments.
Vehiclerouteoptimization: Aftermultipleiterationsofsearchandperturbationopera-
tions,weobtainedasetofrelativelystableandhigh-qualitysolutions. Tofurtheroptimize
thetotaltraveltimeofvehicles,weintroducedtheExchangealgorithmtorefinethecurrent
solution set. The core idea of the Exchange algorithm is similar to random swapping,
butitsuniquenessliesinattemptingtoremoveallcustomerpointsfromeveryrouteand
sequentially reinsert their corresponding delivery addresses into any position of other
routes.Aslongasthegeneratedrouteisfeasibleandthesolutionqualityimproves,thenew
solutionwillbeaccepted. TheExchangealgorithmenhancessolutionspaceexploration
andimprovesoverallsolutionqualitybyfurtheroptimizingtotalvehicletraveltime.
5. NumericalExperiments
This section validates the effectiveness of the proposed MTVRPMDL model and
GILS heuristic through numerical experiments. Based on the examples from Dumez
etal. (2021)[39],wedesignedtwotypesofinstances,totaling48. Forsmall-scaleexam-
ples,CPLEXwasusedforsolving. BycomparingthesolutionsoftheMTVRPMDLand
MTVRPTWproblems,weanalyzedtheperformanceimprovementofintroducingmultiple
deliveryaddresses. Wealsoinvestigatetheapplicabilityandsolvingperformanceofthe
GILSalgorithmfortheseinstances. Allcomputationalexperimentsinthecasestudywere
implementedinJava,withIBMILOGCPLEX12.10employedastheoptimizationsolver.
The experiments were executed on a standard desktop computer featuring a 2.60 GHz
processorand32GBofmemory.
5.1. InstancesGeneration
SinceMTVRPMDLisanewcombinatorialoptimizationproblemwithnobenchmark
instancesintheliterature,thisstudyadoptstheinstancegenerationmethodologyofDumez
etal.(2021)[39]originallydevelopedforVRPwithmultipledeliveryoptions.Bymodifying
parameters such as vehicle capacity and delivery locations to suit the multi-trip and
multi-delivery-locationattributesofMTVRPMDL,wegeneratedtwotypesoftestinstance
sets: one with narrower time windows and another with wider time windows. These
twocategoriesinclude16smaller-scaleinstanceswithcustomercountsof10and15,aswell
as32larger-scaleinstanceswithcustomercountsof25,50,100,and200. Consideringthat
real-worldscenariostypicallyinvolvetwodeliveryaddressespercustomer,all48instance
setswereconfiguredwithtwodeliveryaddressespercustomer. Therelevantparameters
andconstructionmethodsfortheinstancesetsareasfollows:
(1)Allcustomerdeliveryaddressesarerandomlydistributedwithina50×50square
area, with the depot located at (0, 0). The depot’s time window is set to [0, 720], and
Euclideandistanceisusedfordistancecalculations.
(2)Eachcustomerhastwodeliveryaddresses,withtheirassociatedtimewindows
assignedtomorningandafternoonperiods,respectively. Forthemorning/afternoontime
window ec, arandomnumberisselectedfromtheintervals[0, 240]or[360, 600]asthe
i
https://doi.org/10.3390/sym18020233

Symmetry2026,18,233 16of23
starttimeofthetimewindowfordeliveryaddressiofcustomerc. Theendtimelc isthen
i
determinedbyaddingthetimewindowwidthtoec.
i
(3)Timewindowsarecategorizedintonarrowandwidetypes. Narrowtimewindows
havewidthsof60or120,whilewidetimewindowshavewidthsof120or180.
(4) The service time per customer is set to 10, and customer demand is a random
integerbetween[10,20]. Thevehiclecapacityis100inallcases.
Figure5showsthescatterplotof25customersand50deliveryaddressesinonegroup
oftheexamples,wherethereddotsrepresentwarehouses,thebluedotsrepresentoneof
thecustomers’deliveryaddresses,andthegreendotsrepresentanotherdeliveryaddress
ofthecustomer. FromFigure5,itcanbeseenthatthe50deliveryaddressesareevenly
distributedinthisarea. However,whenplanningthevehicleroute,thevehicleonlyneeds
to deliver to one of the two delivery addresses of the customer. Compared to a single
deliveryaddress,consideringmultipledeliveryaddressesgivesthecarriermoreflexibility.
Figure5.Scatterplotofdeliveryaddressesforanexamplewith25customers.
5.2. ComparisonwithMTVRPTW
Toassessthebenefitsofincorporatingmultipledeliveryaddresses,wecomparethe
solutionsobtainedforsmallinstancesusingtheMTVRPMDLmodelwiththosederived
fromtheMTVRPTWmodel. TheMTVRPTWformulationfollowsWuetal. (2024)[52].
Since the MTVRPTW and MTVRPMDL models do not impose any restrictions on the
numberofvehicles,wewillfirstdeterminetheminimumnumberofvehiclesrequiredfor
eachsetofinstancesunderbothproblemsthroughmultipleexperiments. Thesolution
resultsforMTVRPTWandMTVRPMDLareshowninTable2. Here, |K|representsthe
minimumnumberofvehiclesused,r indicatesthemaximumnumberoftripsamong
max
all vehicles, TT and TT denote the total travel time of vehicles for
MTVRPMDL MTVRPTW
MTVRPMDLandMTVRPTW,respectively. DuetothehighcomplexityoftheMTVRPMDL
problem,asthenumberofcustomersincreases,someinstancescannotbesolvedprecisely
within a short time. Therefore, for such instances, we set the number of vehicles to be
thesameasthatundertheMTVRPMDLproblemsolvedbytheGILSheuristicalgorithm,
usingthelowerboundobtainedafter3hasthebenchmarkforcomparison. ∆ represents
TT
theproportionaldifferenceintotaltraveltimebetweentheMTVRPMDLandMTVRPTW
modelsunderthesamesetofinstances,calculatedusingformula(21).
∆ = TTMTVRPMDL −TTMTVRPTW ×100% (21)
TT TTMTVRPMDL
AscanbeseenfromTable2,amongthese16instances,theinstanceswith10customers
forboththeMTVRPTWandMTVRPMDLproblemscanobtainexactsolutionswithin3h.
Thenumberofvehiclesusedandthemaximumnumberoftripsarethesame. However,
compared to the total vehicle travel time of MTVRPTW, the total vehicle travel time of
https://doi.org/10.3390/sym18020233

Symmetry2026,18,233
17of23
MTVRPMDL, which considers multiple delivery addresses, can be reduced by at least
29.2%. Inthecaseu_s_10_02,thetotalvehicletraveltimeofMTVRPMDLwasreducedby
74.4%. Onaverage,theMTVRPMDLmodelwith10customersreducedthetotaltraveltime
by49.5%comparedtoMTVRPTW.Fortheinstanceswith15customers,onlyoneinstance
ofMTVRPMDLobtainedanexactsolutionwithin3h,whileMTVRPTWconsistentlyfound
exactsolutionsquickly. Insomecases,MTVRPMDLusedfewervehiclesthanMTVRPTW.
ComparedtotheoptimalsolutionsofMTVRPTW,thefeasiblesolutionsofMTVRPMDL
couldreducethetotalvehicletraveltimebyupto51.7%. Theseresultsdemonstratethat
consideringmultipledeliveryaddressesiseffectiveforMTVRPs. Thesettingofmultiple
deliveryaddressescandirectlyreducelogisticscostsforcarriersandincreasetheflexibility
ofvehiclerouteplanning.
Table2.ComputationalresultsofMTVRPMDLandMTVRPTWsolvedbyCPLEX.
|          |     | MTVRPMDL |     | MTVRPTW |     |     |
| -------- | --- | -------- | --- | ------- | --- | --- |
| Instance | Q n |          |     |         |     | ∆   |
TT
|           |        | |K| r max | TT MTVRPMDL | |K| r max | TT MTVRPTW |        |
| --------- | ------ | --------- | ----------- | --------- | ---------- | ------ |
| u_s_10_01 | 100 10 | 1 2       | 195.6       | 1 2       | 265.8      | −35.9% |
−74.4%
| u_s_10_02 | 100 10 | 1 2 | 204.9 | 1 2 | 357.4 |        |
| --------- | ------ | --- | ----- | --- | ----- | ------ |
| u_s_10_03 | 100 10 | 1 2 | 193.7 | 1 2 | 301.8 | −55.8% |
| u_s_10_04 | 100 10 | 1 2 | 204.8 | 1 2 | 264.6 | −29.2% |
| u_w_10_01 | 100 10 | 1 2 | 197.4 | 1 2 | 313.2 | −58.7% |
| u_w_10_02 | 100 10 | 1 2 | 219.2 | 1 2 | 309.8 | −41.3% |
−33.1%
| u_w_10_03 | 100 10 | 1 2 | 189.7 | 1 2 | 252.4 |        |
| --------- | ------ | --- | ----- | --- | ----- | ------ |
| u_w_10_04 | 100 10 | 1 2 | 154.3 | 1 2 | 258.5 | −67.5% |
| AVG       | - -    | - - | 195.0 | - - | 290.0 | −49.5% |
−34.6%
| u_s_15_01 | 100 15 | 1 2 | 267.4 | 2 2 | 359.9 |        |
| --------- | ------ | --- | ----- | --- | ----- | ------ |
| u_s_15_02 | 100 15 | 1 3 | 312.2 | 2 2 | 352.6 | −12.9% |
| u_s_15_03 | 100 15 | 1 3 | 276.2 | 2 2 | 343.7 | −24.4% |
| u_s_15_04 | 100 15 | 1 3 | 265.7 | 1 3 | 388.4 | −46.2% |
| u_w_15_01 | 100 15 | 1 3 | 266.9 | 1 3 | 405.0 | −51.7% |
−32.8%
| u_w_15_02 | 100 15 | 1 3 | 302.1 | 1 3 | 401.3 |        |
| --------- | ------ | --- | ----- | --- | ----- | ------ |
| u_w_15_03 | 100 15 | 1 3 | 282.2 | 1 3 | 357.1 | −26.5% |
| u_w_15_04 | 100 15 | 1 3 | 310.4 | 1 3 | 391.3 | −26.1% |
| AVG       | - -    | - - | 282.0 | - - | 374.9 | −31.9% |
5.3. PerformanceoftheGILSAlgorithm
This section reports numerical experiments on the small- and large-scale cases in-
troduced earlier. The GILS is benchmarked against exact solutions from CPLEX (small
instances). BycomparingtheexactsolutionresultsobtainedfromCPLEXwiththosefrom
the GILS algorithm, the performance of GILS in solving MTVRPMDL is validated. In
the GILS algorithm, multiple sets of values were assigned to α 1 , α 2 , µ, and λ: (1,1,1,0),
(2,1,1,0),(1,0,1,0),(2,0,1,1),(1,0.5,1,0.5),and(2,0.5,1,0.5). Duringtheinitialsolutiongenera-
tionprocess,theseparametersweresequentiallyconfigured,andthesolutionyieldingthe
minimalvehicletraveltimeundertheminimumnumberofvehicleswasselectedasthe
finaloutputinitialsolution. TheGILSalgorithminvolvesseveralparametersrelatedtothe
initialsolutionconstruction. SincenopriorbenchmarkexistsfortheMTVRPMDL,these
parameterswereselectedbasedonpreliminarycomputationalexperiments. Specifically,
multiple candidate parameter combinations were tested sequentially during the initial
solutiongenerationphase. Foreachinstance,thecombinationthatproducedtheminimum
totaltraveltimeundertheminimumnumberofvehicleswaschosenasthestartingsolution
forthesubsequentGILSiterations. Ourexperimentsindicatethatthealgorithmisrelatively
insensitivetomoderateparametervariations,asthelocalsearchandperturbationphases
https://doi.org/10.3390/sym18020233

Symmetry2026,18,233
18of23
dominatetheoveralloptimizationprocess. Thisstrategybalancessolutionqualityand
computationalefficiencywhileavoidinginstance-specificoverfittingofparameters.
Table3presentstheresultsofCPLEXandGILSforsolvingtheMTVRPMDLforin-
stanceswith10and15customers. Here,ndenotesthenumberofvehicles,Qrepresents
vehiclecapacity,|K|indicatesthenumberofvehiclesused,r specifiesthemaximum
max
TT′
numberoftripspervehicle, and TT representtheobjectivefunctionvalues
|     |     |     |     | MDL MDL |     |     |
| --- | --- | --- | --- | ------- | --- | --- |
t′
forCPLEXandGILSsolutions, respectively. and t (s) denotethecomputationtimes
(s)
for CPLEX and GILS, respectively. Due to the high complexity of the problem, CPLEX
failed to obtain exact solutions for some 15-customer instances within 3 h. Thus, feasi-
ble solutions obtained after 3 h of CPLEX runtime were used as benchmarks, marked
∆
with “*” above the objective function values. TTMDL indicates the difference in objec-
tivefunctionvaluesbetweenGILSandCPLEXsolutionsforMTVRPMDL,calculatedas
|     | (TT | ′ −TT )/TT′ | ×100%. |     |     |     |
| --- | --- | ----------- | ------ | --- | --- | --- |
|     |     | MDL MDL     | MDL    |     |     |     |
Table3.ComputationalresultsobtainedfromCPLEXandGILSalgorithmonsmall-scaleinstances.
|     |     | CPLEX |     | GILS |     |     |
| --- | --- | ----- | --- | ---- | --- | --- |
∆
| Instance  | Q n    |           |       |           |        | TTMDL    |
| --------- | ------ | --------- | ----- | --------- | ------ | -------- |
|           |        |           | TT’   | t’        |        |          |
|           |        | |K| r max |       | |K| r max | TT MDL | t (s)    |
|           |        |           | MDL   | (s)       |        |          |
| u_s_10_01 | 10 100 | 1 2       | 195.6 | 65 1 2    | 247.8  | 0.2 21%  |
| u_s_10_02 | 10 100 | 1 2       | 204.9 | 79 1 2    | 256.9  | 0.1 20%  |
| u_s_10_03 | 10 100 | 1 2       | 193.7 | 105 1 2   | 227.8  | 0.1 15%  |
| u_s_10_04 | 10 100 | 1 2       | 204.8 | 83 1 2    | 280.5  | 0.1 27%  |
| u_w_10_01 | 10 100 | 1 2       | 197.4 | 98 1 2    | 268.4  | 0.1 26%  |
| u_w_10_02 | 10 100 | 1 2       | 219.2 | 224 1 2   | 227.7  | 0.1 4%   |
| u_w_10_03 | 10 100 | 1 2       | 189.7 | 118 1 2   | 221.3  | 0.1 14%  |
| u_w_10_04 | 10 100 | 1 2       | 154.3 | 148 1 2   | 192.6  | 0.1 20%  |
| AVG       | - -    |           | 195.0 | 115       | 240.4  | 0.1 18%  |
| u_s_15_01 | 15 100 | 1 2       | 267.4 | 2741 1 2  | 377    | 0.2 29%  |
| u_s_15_02 | 15 100 | 1 3       | 312.2 | 7200 2 2  | 345.5  | 0.3 10%  |
| u_s_15_03 | 15 100 | 1 3       | 276.2 | 7200 1 3  | 378.8  | 0.1 27%  |
| u_s_15_04 | 15 100 | 1 3       | 265.7 | 7200 2 2  | 246.7  | 0.2 −8%  |
| u_w_15_01 | 15 100 | 1 3       | 266.9 | 7200 1 3  | 299.8  | 0.1 11%  |
| u_w_15_02 | 15 100 | 1 3       | 302.1 | 7200 1 3  | 325.3  | 0.1 7%   |
| u_w_15_03 | 15 100 | 1 3       | 282.2 | 7200 1 3  | 371.2  | 0.1 24%  |
| u_w_15_04 | 15 100 | 1 3       | 310.4 | 7200 2 2  | 311.9  | 0.1 0.5% |
| AVG       | - -    |           | 285.4 | -         | 310.35 | 0.15 8%  |
AsshowninTable3,CPLEXisabletoobtainoptimalsolutionsforalleightinstances
withbothwideandnarrowtimewindowsinvolving10customerswithinalimitedcom-
putationtime,withanaveragesolutiontimeof115s. ComparedtoCPLEX,GILShasa
shortersolutiontimeandcanfindtheoptimalsolutionwithin0.2s,showingsignificant
improvement in solution time. Additionally, the average objective function difference
betweenGILSandCPLEXforsolvingMTVRPMDLis18%. Forthe8setsofinstanceswith
15customers,CPLEXfailstoobtainexactsolutionswithinthespecifiedtime,whileGILS
canfindtheoptimalsolutionwithin0.3s,againdemonstratingsubstantialimprovementin
solutiontime. CPLEXusesfeasiblesolutionsobtainedafter3hofruntimeasabenchmark
forcomparison,andtheaverageobjectivefunctiondifferencebetweenGILSandCPLEX
forsolvingMTVRPMDLis8%,indicatingbettersolutionquality. Acrossbothtimewindow
configurations,instanceswithwidetimewindowsfor10and15customersconsistently
producebettersolutionsthantheirnarrowtimewindowcounterparts,astheexpanded
timewindowsallowgreaterflexibilityinthesearchprocess.
GiventhatCPLEXstruggledtoobtainexactsolutionswithinthe3hlimitforinstances
with15customers(seeTable3),solvingthelargerinstances(n ≥25)tooptimalitywithan
https://doi.org/10.3390/sym18020233

Symmetry2026,18,233
19of23
exactsolverwasdeemedcomputationallyintractable. Therefore,toassessthescalability
andperformanceofourproposedmethodonrealisticproblemsizes,weevaluatedtheGILS
algorithmexclusivelyontheselargerinstancesets. TheresultsarepresentedinTable4.
Table4presentsthesolvingresultsoftheGILSalgorithmunderdifferentcustomerscales
(25, 50, 100, 200). The results show that as the problem size increases, the solving time
exhibits a gradually increasing trend. For instances with 25 customers and 50 delivery
addresses,thesolvingtimeiswithin1s;forinstanceswith50customersand100delivery
addresses,thesolvingtimeiswithin3s. Whenthecustomercountreaches100andthe
total delivery addresses reach 200, the solving time begins to increase rapidly, with an
average solving time of 1741 s. When the customer scale increases to 200 and the total
deliveryaddressscalereaches400,all8setsofinstancescanstillfindtheoptimalsolution
within6min,indicatingthatthealgorithmhashighsolvingefficiency. Additionally,as
thenumberofcustomersincreases,theaveragemaximumnumberofvehicletripsalso
graduallyincreases,withtheaveragevehicletripsbeingaround4. Whenthenumberof
customersreaches200,vehiclescanperformupto6trips,reachingthemaximumvehicle
tripsandoptimalvehicleutilization. Anincreaseintheaveragenumberofvehicletrips
implies a reduction in the number of vehicles required. Therefore, in actual logistics
operations,companiesshouldfocusonincreasingthenumberofvehicletripstoimprove
vehicleutilizationandtherebyreducefixedcostexpenditures.
Table 4. Computational results obtained from GILS for solving the instances with more than
25customersofMTVRPMDL.
| Instance  | n |K| | r TT      | t Instance     | n |K|  | r TT       | t     |
| --------- | ----- | --------- | -------------- | ------ | ---------- | ----- |
|           |       | max MDL   | (s)            |        | max MDL    | (s)   |
| u_s_25_01 | 25 2  | 3 583.0   | 0.6 u_s_100_01 | 100 5  | 4 1831.6   | 8.9   |
| u_s_25_02 | 25 2  | 3 554.2   | 0.7 u_s_100_02 | 100 6  | 4 1767.8   | 15.1  |
| u_s_25_03 | 25 2  | 3 475.9   | 0.3 u_s_100_03 | 100 6  | 4 1626.5   | 12.4  |
| u_s_25_04 | 25 2  | 3 560.7   | 0.5 u_s_100_04 | 100 6  | 4 1800.3   | 9.5   |
| u_w_25_01 | 25 2  | 3 461.7   | 0.3 u_w_100_01 | 100 5  | 5 1775.4   | 10.1  |
| u_w_25_02 | 25 2  | 3 453.9   | 0.4 u_w_100_02 | 100 5  | 5 1742.4   | 9.8   |
| u_w_25_03 | 25 2  | 3 527.2   | 0.4 u_w_100_03 | 100 5  | 5 1585.1   | 9.6   |
| u_w_25_04 | 25 2  | 3 469.0   | 0.4 u_w_100_04 | 100 5  | 4 1801.8   | 23.4  |
| AVG       | - 2   | 3 510.7   | 0.5 AVG        | - 5.4  | 4.4 1741.4 | 12.4  |
| u_s_50_01 | 50 3  | 4 985.7   | 1.9 u_s_200_01 | 200 10 | 4 3316.2   | 109.0 |
| u_s_50_02 | 50 3  | 4 1037.8  | 1.7 u_s_200_02 | 200 10 | 4 3242.0   | 132.7 |
| u_s_50_03 | 50 3  | 4 893.9   | 1.2 u_s_200_03 | 200 10 | 4 3073.7   | 223.8 |
| u_s_50_04 | 50 3  | 4 1008.8  | 1.1 u_s_200_04 | 200 10 | 5 3280.3   | 99.9  |
| u_w_50_01 | 50 3  | 4 999.6   | 1.8 u_w_200_01 | 200 8  | 6 2991.6   | 74.7  |
| u_w_50_02 | 50 3  | 5 818.5   | 2.4 u_w_200_02 | 200 9  | 5 3029.9   | 241.7 |
| u_w_50_03 | 50 3  | 4 986.4   | 1.7 u_w_200_03 | 200 9  | 5 2888.0   | 148.3 |
| u_w_50_04 | 50 3  | 5 929.7   | 1.8 u_w_200_04 | 200 9  | 5 3182.2   | 114.6 |
| AVG       | - 3   | 4.3 957.6 | 1.7 AVG        | - 9.4  | 4.8 3125.5 | 143.1 |
To our knowledge, there is currently no publicly available state-of-the-art (SOTA)
heuristictailoredtothemulti-tripvehicleroutingproblemwithmultipledeliverylocations
andtimewindows. Althoughpowerfulmetaheuristicssuchasadaptivelargeneighbor-
hood search (ALNS) and variable neighborhood search (VNS) have been successfully
appliedtovariousVRPvariants,directlyapplyingtheseframeworkstotheMTVRPMDL
isnotstraightforward. Inparticular,destroy–repairorneighborhoodoperatorsmustbe
redesignedtosimultaneouslyhandlemulti-tripsequencing,delivery-locationreselection,
and time window feasibility, which fundamentally alters the algorithmic structure and
computationalbehavior. Withoutsuchproblem-specificadaptations,adirectcomparison
withgenericSOTAimplementationswouldnotbemethodologicallyfairandmayleadto
https://doi.org/10.3390/sym18020233

Symmetry2026,18,233 20of23
misleadingconclusions. Therefore,thisstudyfocusesonvalidatingtheproposedGILS
frameworkthroughexactbenchmarksonsmallinstancesandmodel-basedbaselines,while
thedevelopmentofdelivery-location-awareALNS/VNSalgorithmsandtheirsystematic
comparisonwithGILSisleftasanimportantdirectionforfutureresearch.
6. Conclusions
This paperaddresses the challengesof improving last-milelogistics deliverysatis-
factioninurbanareasandsolvingtheMTVRPMDL.WedevelopanMILPmodelaimed
atminimizingthetotalvehicletraveltime. Twotypesofinstancesaredesignedforthis
problem,andexactsolutionsareobtainedusingCPLEX.Thecomputationalresultsindicate
thatallowingmultipledeliverylocationsconsistentlyreducestotaltraveldistanceand,in
severalcases,decreasesthenumberofvehiclesrequiredcomparedwiththeMTVRPTW
baseline. For small instances, the proposed GILS algorithm achieves optimal or near-
optimalsolutionswithverysmalloptimalitygapsrelativetoCPLEX.Forlargerinstances,
GILSremainscomputationallyefficientandrobust,producinghigh-qualitysolutionswithin
shorttimelimits,whileexactsolversbecomeintractable. Theseresultsconfirmboththe
modeling benefits of flexible delivery locations and the effectiveness of the proposed
symmetry-awareheuristicframework.
Futureworkcouldexpandinseveralpromisingdirections. Onekeyareainvolves
introducingcustomerpreferenceandservicepriorityintothemultiple-delivery-location
framework. By assigning different priority levels to various delivery time windows or
locations,modelscouldbedevelopedthatjointlyoptimizelogisticalefficiencyandaquan-
tifiedmeasureofcustomersatisfaction,betterreflectingreal-worldservicetrade-offs. Itis
alsonecessarytoincorporatesimultaneouspickupanddeliveryoperations,leadingtoa
multi-tripvehicleroutingproblemwithmultipledeliverylocationsandpickup–delivery
interactions. Thiswouldrequirejointload-flowmodelingandredesignedsymmetry-aware
heuristic operators, and is left for future research. Secondly, the problem formulation
couldbeenrichedbyincorporatingalternativedeliverymodalities,suchassharedcollec-
tionpointsorparcellockers, alongsidetraditionaldoor-to-doorservice. Thisextension
would require modeling the capacity constraints of shared locations and analyzing the
cost–benefitdynamicsbetweendifferentdeliveryoptions. Thirdly, animportantexten-
sionofthisworkistoadaptwidelyusedmetaheuristicssuchasALNSandVNStothe
MTVRPMDLandconductasystematicperformancecomparisonunderidenticalinstance
setsandstoppingconditions. Certainly,devisingspecializedexactsolutionmethods,such
asbranch-and-pricealgorithmstailoredtothisproblem’scharacteristics,wouldbevalu-
able for generating optimal benchmarks for larger instances and further validating the
performanceofheuristicapproaches. Finally,inthisstudy,weassumeahomogeneousfleet
ofidenticalvehicles. Thisassumptionallowsustofocusonthecoreinteractionbetween
multi-triproutingdecisionsandflexibledeliverylocationselection,andhelpskeepboth
theMILPformulationandtheheuristicdesigncomputationallytractable. However, in
practicalurbanlogisticsoperations,fleetsareoftenheterogeneous,withvehiclesdiffering
incapacity,operatingcost,energyconsumption,oraccessibilityrestrictions. Extendingthe
proposedMTVRPMDLtoheterogeneousfleetsrepresentsanimportantdirectionforfuture
research. Suchanextensionwouldrequirevehicle-specificparametersinthemodeland
correspondingadaptationsoftheGILSoperatorstohandleheterogeneousfeasibilityand
coststructures. Incorporatingfleetheterogeneitywouldfurtherenhancetherealismand
applicabilityoftheproposedframework.
Author Contributions: Conceptualization, W.Z.; methodology, H.S.; software, H.S.; validation,
W.Z.andH.S.;formalanalysis,H.S.;investigation,H.S.;writing—originaldraftpreparation,W.Z.;
https://doi.org/10.3390/sym18020233

Symmetry2026,18,233 21of23
writing—reviewandediting,W.Z.andH.S.;visualization,H.S.;supervision,H.S.;projectadministra-
tion,H.S.Allauthorshavereadandagreedtothepublishedversionofthemanuscript.
Funding:Thisresearchreceivednoexternalfunding.
DataAvailabilityStatement:Theoriginalcontributionspresentedinthestudyareincludedinthe
article,furtherinquiriescanbedirectedtothecorrespondingauthor.
ConflictsofInterest:Theauthorsdeclarenoconflictsofinterest.
Abbreviations
Thislistincludesallmajoracronymsandabbreviationsusedthroughoutthepaper,presented
inalphabeticalorderforeasyreference.
ALNS AdaptiveLargeNeighborhoodSearch
GILS GreedyIteratedLocalSearch
ILS IteratedLocalSearch
MILP Mixed-IntegerLinearProgramming
MTVRP Multi-TripVehicleRoutingProblem
MTVRPMDL Multi-TripVehicleRoutingProblemwithMultipleDeliveryLocations
MTVRPTW Multi-TripVehicleRoutingProblemwithTimeWindows
NP-hard Non-deterministicPolynomial-timehard
SOTA State-Of-The-Art
VNS VariableNeighborhoodSearch
VRP VehicleRoutingProblem
VRPTW VehicleRoutingProblemwithTimeWindows
References
1. Dantzig,G.B.;Ramser,J.H.Thetruckdispatchingproblem.Manag.Sci.1959,6,80–91.[CrossRef]
2. Golden, B.L.; Raghavan, S.; Wasil, E.A.TheVehicleRoutingProblem: LatestAdvancesandNewChallenges; SpringerScience&
BusinessMedia:NewYork,NY,USA,2008;pp.3–589.
3. Toth,P.;Vigo,D.VehicleRouting:Problems,Methods,andApplications,2nded.;SocietyforIndustrialandAppliedMathematics:
Philadelphia,PA,USA,2014;pp.1–452.
4. Braekers,K.;Ramaekers,K.;VanNieuwenhuyse,I.Thevehicleroutingproblem:Stateoftheartclassificationandreview.Comput.
Ind.Eng.2016,99,300–313.[CrossRef]
5. Tan,K.;Liu,W.;Xu,F.;Li,C.Optimizationmodelandalgorithmoflogisticsvehicleroutingproblemundermajoremergency.
Mathematics2023,11,1274.[CrossRef]
6. Vidal,T.;Laporte,G.;Matl,P.Aconciseguidetoexistingandemergingvehicleroutingproblemvariants.Eur.J.Oper.Res.2020,
286,401–416.[CrossRef]
7. PostOfficeofthePeople’sRepublicofChina. 2023PostalIndustryDevelopmentStatisticalBulletin. Availableonline: https:
//www.spb.gov.cn/gjyzj/c100015/c100016/202401/59eeb6e8b0e7404f8127aa2c7aebded6.shtml(accessedon20October2025).
8. Cattaruzza,D.;Absi,N.;Feillet,D.Vehicleroutingproblemswithmultipletrips.Q.J.Oper.Res.2016,14,223–259.[CrossRef]
9. Fleischmann,B.TheVehicleRoutingProblemwithMultipleUseofVehicles;TechnicalReport;FachbereichWirtschaftswissenschaften,
UniversitätHamburg:Hamburg,Germany,1990.
10. Macedo,R.;Claudio,A.J.M.;Valerio,D.C.;Clautiaux,F.;Hanafi,S.Solvingthevehicleroutingproblemwithtimewindowsand
multipleroutesexactlyusingapseudo-polynomialmodel.Eur.J.Oper.Res.2011,214,536–545.[CrossRef]
11. Cattaruzza,D.;Absi,N.;Feillet,D.;Vigo,D.Aniteratedlocalsearchforthemulti-commoditymulti-tripvehicleroutingproblem
withtimewindows.Comput.Oper.Res.2014,51,257–267.[CrossRef]
12. Hernandez,F.;Feillet,D.;Giroudeau,R.;Naud,O.Anewexactalgorithmtosolvethemulti-tripvehicleroutingproblemwith
timewindowsandlimitedduration.Q.J.Oper.Res.2014,12,235–259.[CrossRef]
13. Hernandez,F.;Feillet,D.;Giroudeau,R.;Naud,O.Branch-and-pricealgorithmsforthesolutionofthemulti-tripvehiclerouting
problemwithtimewindows.Eur.J.Oper.Res.2016,249,551–559.[CrossRef]
14. Francois,V.;Arda,Y.;Crama,Y.Largeneighborhoodsearchformulti-tripvehiclerouting.Eur.J.Oper.Res.2016,255,422–441.
[CrossRef]
https://doi.org/10.3390/sym18020233

Symmetry2026,18,233 22of23
15. Francois,V.;Arda,Y.;Crama,Y.Adaptivelargeneighborhoodsearchformultitripvehicleroutingwithtimewindows.Transp.Sci.
2019,53,1706–1730.[CrossRef]
16. Cattaruzza,D.;Absi,N.;Feillet,D.Themulti-tripvehicleroutingproblemwithtimewindowsandreleasedates.Transp.Sci.2016,
50,676–693.[CrossRef]
17. Li,W.L.;Yong,W.;Kumar,P.N.;Li,K.Multi-tripvehicleroutingproblemwithorderreleasetime.Eng.Optim.2019,52,1279–1294.
[CrossRef]
18. Zhen,L.;Ma,C.;Wang,K.;Xiao,L.;Zhang,W.Multi-depotmulti-tripvehicleroutingproblemwithtimewindowsandrelease
dates.Transp.Res.PartELogist.Transp.Rev.2020,135,101866.[CrossRef]
19. Neira,D.A.;Aguayo,M.M.;DelaFuente,R.;Klapp,M.A.Newcompactintegerprogrammingformulationsforthemulti-trip
vehicleroutingproblemwithtimewindows.Comput.Ind.Eng.2020,144,106399.[CrossRef]
20. Pan,B.B.;Zhang,Z.Z.;Lim,A.Multi-triptime-dependentvehicleroutingproblemwithtimewindows.Eur.J.Oper.Res.2021,
291,218–231.[CrossRef]
21. Huang,N.;Qin,H.;Xu,G.;Wan,F.Anenhancedexactalgorithmforthemulti-tripvehicleroutingproblemwithtimewindows
andcapacitatedunloadingstation.Comput.Oper.Res.2024,168,106688.[CrossRef]
22. Zhang,Z.;Che,Y.;Liang,Z.Split-demandmulti-tripvehicleroutingproblemwithsimultaneouspickupanddeliveryinairport
baggagetransit.Eur.J.Oper.Res.2024,312,996–1010.[CrossRef]
23. Bernardino,R.;Janela,J.;Martins,C.;Mourão,M.C.;Pinto,L.S.;Rodrigues,F.Amulti-tripvehicleroutingproblemwithrelease
datesandinterrelatedperiods.Networks2025,85,189–204.[CrossRef]
24. Grangier,P.;Gendreau,M.;Lehuede,F.;Rousseau,L.M.Anadaptivelargeneighborhoodsearchforthetwo-echelonmultiple-trip
vehicleroutingproblemwithsatellitesynchronization.Eur.J.Oper.Res.2016,254,80–91.[CrossRef]
25. He,P.F.;Li,J.Thetwo-echelonmulti-tripvehicleroutingproblemwithdynamicsatellitesforcropharvestingandtransportation.
Appl.SoftComput.2019,77,387–398.[CrossRef]
26. Marques, G.; Ruslan, S.; Remy, D.; Jean-Christophe, D. A branch-cut-and-price approach for the single-trip and multi-trip
two-echelonvehicleroutingproblemwithtimewindows.Transp.Sci.2022,56,1598–1617.[CrossRef]
27. Lehmann,J.;Winkenbach,M.Amatheuristicforthetwo-echelonmulti-tripvehicleroutingproblemwithmixedpickupand
deliverydemandandtimewindows.Transp.Res.PartCEmerg.Technol.2024,160,104522.[CrossRef]
28. Stamadianos,T.;Kyriakakis,N.A.;Marinaki,M.;Marinakis,Y.RoutingProblemswithElectricandAutonomousVehicles: A
ReviewandFutureResearchDirections.Oper.Res.Forum.2023,4,46.[CrossRef]
29. Kashmiri, F.A.; Lo, H.K. Routing of multi-modal autonomous vehicles for system optimal flows and average travel cost
equilibriumovertime.Transp.Res.PartCEmerg.Technol.2024,159,104483.[CrossRef]
30. Wang,Z.;An,K.;Correia,G.;Ma,W.Real-timeschedulingandroutingofsharedautonomousvehiclesconsideringplatooning
inintermittentsegregatedlanesandpriorityatintersectionsinurbancorridors. Transp. Res. PartELogist. Transp. Rev. 2024,
186,103546.[CrossRef]
31. Kong,J.;Wang,H.;Xie,M.Autonomousdeliveryvehicleroutingproblemwithdronesbasedonmultipledeliverymodes.Comput.
Oper.Res.2025,179,107032.[CrossRef]
32. Sahin,M.K.;Yamana,H.Abranchandpricealgorithmfortheheterogeneousfleetmulti-depotmulti-tripvehicleroutingproblem
withtimewindows.Transp.Sci.2022,56,1636–1657.[CrossRef]
33. Los,J.;Spaan,M.T.;Negenborn,R.R.Fleetmanagementforpickupanddeliveryproblemswithmultiplelocationsandpreferences.
In Dynamics in Logistics: Proceedings of the 6th International Conference LDIC 2018, Bremen, Germany; Springer International
Publishing:Cham,Switzerland,2018;pp.86–94.
34. Sadati,M.E.H.;Akbari,V.;Çatay,B.Electricvehicleroutingproblemwithflexibledeliveries.Int.J.Prod.Res.2022,60,4268–4294.
[CrossRef]
35. Escudero-Santana,A.;Muñuzuri,J.;Lorenzo-Espejo,A.;Muñoz-Díaz,M.L.Improvinge-commercedistributionthroughlast-mile
logisticswithmultiplepossibilitiesofdeliveriesbasedontimeandlocation. J.Theor. Appl. Electron. Commer. Res. 2022,17,
507–521.[CrossRef]
36. Frey,C.M.M.;Jungwirth,A.;Frey,M.;Kolisch,R.Thevehicleroutingproblemwithtimewindowsandflexibledeliverylocations.
Eur.J.Oper.Res.2023,308,1142–1159.[CrossRef]
37. Zhang,S.Z.;Lee,C.K.M.Flexiblevehicleschedulingforurbanlastmilelogistics:Theemergingtechnologyofsharedreception
box.InProceedingsoftheIEEEInternationalConferenceonIndustrialEngineeringandEngineeringManagement(IEEM),Bali,
Indonesia,4–7December2016;pp.1917–1919.
38. Mancini,S.;Gansterer,M.Vehicleroutingwithprivateandshareddeliverylocations.Comput.Oper.Res.2021,133,12.[CrossRef]
39. Dumez,D.;Lehuédé,F.;Péton,O.Alargeneighborhoodsearchapproachtothevehicleroutingproblemwithdeliveryoptions.
Transp.Res.PartBMethodol.2021,144,103–132.[CrossRef]
40. Tirkolaee,E.B.;Abbasian,P.;Weber,G.W.Sustainablefuzzymulti-triplocation-routingproblemformedicalwastemanagement
duringtheCOVID-19outbreak.Sci.TotalEnviron.2021,756,143607.[CrossRef][PubMed]
https://doi.org/10.3390/sym18020233

Symmetry2026,18,233 23of23
41. Reyes,D.;Savelsbergh,M.;Toriello,A.Vehicleroutingwithroamingdeliverylocations.Transp.Res.PartCEmerg.Technol.2017,
80,71–91.[CrossRef]
42. He,Y.;Wang,X.;Zhou,F.;Lin,Y.Dynamicvehicleroutingproblemconsideringsimultaneousdualservicesinthelastmile
delivery.Kybernetes2020,49,1267–1284.[CrossRef]
43. Dragomir,A.G.;VanWoensel,T.;Doerner,K.F.Thepickupanddeliveryproblemwithalternativelocationsandoverlappingtime
windows.Comput.Oper.Res.2022,143,105758.[CrossRef]
44. Lourenço,H.R.;Martin,O.C.;Stützle,T.Iteratedlocalsearch:Frameworkandapplications.InHandbookofMetaheuristics;Springer:
Cham,Switzerland,2019;Volume272,pp.129–168.
45. Archetti,C.;Feillet,D.;Mor,A.;Speranza,M.G.Aniteratedlocalsearchforthetravelingsalesmanproblemwithreleasedates
andcompletiontimeminimization.Comput.Oper.Res.2018,98,24–37.[CrossRef]
46. Mardones, B.; Gatica, G.; Contreras-Bolton, C. A Metaheuristic for the double traveling salesman problem with partial
last-in-first-outloadingconstraints.Int.Trans.Oper.Res.2023,30,3904–3929.[CrossRef]
47. Dasari,K.V.;Singh,A.Twoheuristicapproachesforclusteredtravelingsalesmanproblemwithd-relaxedpriorityrule.Expert
Syst.Appl.2023,224,120003.[CrossRef]
48. Máximo,V.R.;Nascimento,M.C.Ahybridadaptiveiteratedlocalsearchwithdiversificationcontroltothecapacitatedvehicle
routingproblem.Eur.J.Oper.Res.2021,294,1108–1119.[CrossRef]
49. Penna,P.H.V.;Subramanian,A.;Ochi,L.S.Aniteratedlocalsearchheuristicfortheheterogeneousfleetvehicleroutingproblem.
Heuristics2013,19,201–232.[CrossRef]
50. Osorio-Mora,A.;Escobar,J.W.;Toth,P.Aniteratedlocalsearchalgorithmforlatencyvehicleroutingproblemswithmultiple
depots.Comput.Oper.Res.2023,158,106293.[CrossRef]
51. Yahiaoui,A.E.;Afifi,S.;Allaoui,H.Enhancediteratedlocalsearchforthetechnicianroutingandschedulingproblem.Comput.
Oper.Res.2023,160,106385.[CrossRef]
52. Wu,Y.;Du,H.;Song,H.AnIteratedLocalSearchHeuristicfortheMulti-TripVehicleRoutingProblemwithMultipleTime
Windows.Mathematics2024,12,1712.[CrossRef]
Disclaimer/Publisher’sNote: Thestatements, opinionsanddatacontainedinallpublicationsaresolelythoseoftheindividual
author(s)andcontributor(s)andnotofMDPIand/ortheeditor(s).MDPIand/ortheeditor(s)disclaimresponsibilityforanyinjuryto
peopleorpropertyresultingfromanyideas,methods,instructionsorproductsreferredtointhecontent.
https://doi.org/10.3390/sym18020233