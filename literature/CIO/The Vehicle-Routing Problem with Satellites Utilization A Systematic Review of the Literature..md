SystematicReview
The Vehicle-Routing Problem with Satellites Utilization: A
Systematic Review of the Literature
RaúlSoto-Concha1,2,* ,JohnWillmerEscobar3 ,DanielMorillo-Torres4 andRodrigoLinfati5,*
1 FacultaddeIngeniería,UniversidaddelBío-Bío,Concepcion4051381,Chile
2 DepartamentodeCienciasdelaIngeniería,UniversidaddeLosLagos,PuertoMontt5480000,Chile
3 AccountingandFinanceDepartment,UniversidaddelValle,Cali760001,Colombia;
john.wilmer.escobar@correounivalle.edu.co
4 DepartmentofCivilandIndustrialEngineering,FacultyofEngineeringandSciences,PontificiaUniversidad
JaverianaCali,Cali760031,Colombia;daniel.morillo@javerianacali.edu.co
5 DepartamentodeIngenieríaIndustrial,UniversidaddelBío-Bío,Concepcion4051381,Chile
* Correspondence:rsotoco@ubiobio.cl(R.S.-C.);rlinfati@ubiobio.cl(R.L.)
Abstract: TheVehicle-RoutingProblem(VRP)representsacriticalchallengeinlogistics,
encompassing numerous variations, such as time window considerations, multi-depot
systems,two-echelonroutingaspects,andSatelliteLocations(SL).SLsareintermediate
facilities that support cross-docking, storage, and transshipment operations. However,
inconsistenciesindefining“satellite”havehinderedpreciseresearchandimplementation.
This study presents a systematic review of the use of satellites for VRP, employing the
PRISMAmethodologytoensureacomprehensiveandreproducibleanalysis. Thefindings
indicatethatabout50%ofthereviewedpapersincludeapath-splittingvariant.Atthesame
time,thereisanotablegapinaddressingrandomdemandsandpickupanddeliverywithin
cross-dockingenvironments. Amajorlimitationisthelackofawell-knownpublicdataset,
asabout50%ofthedatasetsarecreatedoradaptedforspecificstudies. Additionally,the
analysisrevealssignificantgapsindatasetstandardizationandtheintegrationofdynamic
routing under uncertainty. These findings underscore the potential of satellite-based
systemstooptimizeurbanlogisticsandsupplychainswhilepointingtocriticalavenues
forfutureresearch.
Keywords:VRP;PRISMA;satellite;intermediatefacilities;cross-docking;lastmilelogistics;
AcademicEditor:Shih-WeiLin
multipleechelon
Received:3March2025
Revised:20March2025
MSC:90-02
Accepted:24March2025
Published:26March2025
Citation: Soto-Concha,R.;Escobar,
J.W.;Morillo-Torres,D.;Linfati,R.The 1. Introduction
Vehicle-RoutingProblemwith
The transportation problem of products in last mile logistics is crucial, primarily
SatellitesUtilization:ASystematic
ReviewoftheLiterature.Mathematics duetoincreaseddeliveryvolumes,sustainabilityconsiderations,costs,servicelevel[1],
2025,13,1092. https://doi.org/ anagingworkforce,andnewchallengesposedbytechnologicaladvancementssuchas
10.3390/math13071092 autonomousdriving,drones,anddeliveryrobots[2]. Thisproblembelongstothefamily
Copyright:©2025bytheauthors. oftheVehicle-RoutingProblem(VRP)[3],whichplaysasignificantroleinsupplychain
LicenseeMDPI,Basel,Switzerland. management(SCM).TheVRPisintroducedbyDantzigsworktitledTruckDispatching
Thisarticleisanopenaccessarticle Problem(TDP)[4],andaccordingtothebest-knownalgorithms,theVRPisconsidered
distributedunderthetermsand
NP-Hard[5].
conditionsoftheCreativeCommons
AccordingtoMorandSperanza[6],inVRPsthedecisionsmustbemaderegarding
Attribution(CCBY)license
theassignmentofcustomerstovehiclesandthesequenceofvisits,andadditionaldecisions
(https://creativecommons.org/
licenses/by/4.0/). mustbeperformedcollectively,dependingonthespecificproblemframework.Forinstance,
Mathematics2025,13,1092 https://doi.org/10.3390/math13071092

Mathematics 2025, 13, 1092 2 of 29
According to Mor and Speranza [6], in VRPs the decisions must be made regarding
the assignment of customers to vehicles and the sequence of visits, and additional
Mathematics2025,13,1092 decisions must be performed collectively, depending on the specific problem fr2aomf2e8work.
For instance, ref. [7] addresses dynamic routing with stochastic requests, a critical aspect
in e-commerce, while ref. [8] includes the multi-depot, capacity, and two-echelon Vehicle-
ref.[7]addressesdynamicroutingwithstochasticrequests,acriticalaspectine-commerce,
Routing-Problem issue (2E-MDCVRP).
whileref.[8]includesthemulti-depot,capacity,andtwo-echelonVehicle-Routing-Problem
issuIte i(s2 eEs-MseDntCiaVlR foPr). the supply chain to address all aspects that satisfy customers(cid:31) orders
[9], espIetciisaellsys etnhtoiasle froerlathteeds utop uplrybacnha liongtiostaicdsd, rweshsicahll iansvpoelcvtsesth taratnsastpisofrytactuiostno macetrisv’itoire-s [10],
incdleurdsi[n9g], edsepleivciearlileyst hino suerrbelaante darteoasu r[b1a1n].l oOgniset icosf, wthhei cehleinmveonlvtse stotr acnosnpsoirdtaetri oinn adcetilviv-ering
priotdieusc[t1s0 ]t,oi ncculustdoinmgedrse liisv etrhiees uinseu orbf asnataerlelaitse[s1, 1w].hOicnhe aorfet hoefteelnem deenfitsnetod caosn siindteerrminediate
deliveringproductstocustomersistheuseofsatellites,whichareoftendefinedasinterme-
facilities [12], which can have storage capacity [13] or may serve for cross-docking
diatefacilities[12],whichcanhavestoragecapacity[13]ormayserveforcross-docking
operations [14]. Additionally, these facilities can be fixed ([15,16]) or mobile ([17,18]) (see
operations [14]. Additionally, these facilities can be fixed [15,16] or mobile [17,18] (see
Figure 1). The satellite locations ([19,20]) are defined as an intermediate site with limited,
Figure1). Thesatellitelocations[19,20]aredefinedasanintermediatesitewithlimited,or
or even non-existent, storage capacity [21], or as a physical space equipped for load
evennon-existent,storagecapacity[21],orasaphysicalspaceequippedforloadtransship-
transshipment and consolidation [22], when used as a keyword in string search engines
mentandconsolidation[22],whenusedasakeywordinstringsearchenginesforscientific
for scientific papers associated with VRPs.
papersassociatedwithVRPs.
SATELLITE
INTERMEDIATE
CROSS-DOCKING OTHER
FACILITIES OR DEPOTS
MOBILE FIXED
Figure1.Categories.
Theissuewithusingthekeyword“satellite”insearchstringsisthatthetermisnot
solelyassociatedwithtransportproblemsbutalsowithLow-EarthOrbit(LEO)satellite
networks[23],suchasinthestudyby[24],whichutilizestheAntColo nyOptimization
(ACO)tosolvethetrafficimbalanceprobleminsomehigh-demandinternetlinks. Another
Figure 1. Categories.
exampleistheresearchby[25],whichusesthesatelliteconcepttooptimizedatacollection
insatellitesystems.
The issue with using the keyword “satellite” in search strings is that the term is not
Recentreviews,suchasthosepresentedby[26],presentaliteraturereviewrelated
solely associated with transport problems but also with Low-Earth Orbit (LEO) satellite
tothetwo-echelonVehicle-RoutingProblem(2E-VRP),focusingondividingdistribution
networks [23], such as in the study by [24], which utilizes the Ant Colony Optimization
networksintotwoechelons,usingdifferentvehiclesateachechelontoachieveeconomies
(ACO) to solve the traffic imbalance problem in some high-demand internet links.
ofscaleandmeetspecificconstraints. Ontheotherhand,ref.[27]focusesonresearchinto
Another example is the research by [25], which uses the satellite concept to optimize data
2E-VRPthatcombinesgroundvehicles(GVs)anddrones(UAVs),emphasizingconnection
collection in satellite systems.
mechanismsbetweenthetwoechelons,suchassynchronizationatsatellitesandflexible
couRpelicnegn/td reecvoiuepwlisn, gsubcehtw aese tnhUosAeV psraensdenGtVeds. by [26], present a literature review related to
the twIon-ethchisesltound yV,weheipclreo-pRooseuatinsygs tPemroabtilcemrev (ie2wE-tVoRadPd),r efsosctuhseinVegh iocnle -dRiovuitdininggP rdoibsltermibution
newtwitohrtkhse inustoe towf soa eteclhlietelos,npsr, ouvsiidnign gdiaffgeureidnet ovnehaipcplelsy iantg etahcihs ceocnhceelopnt atnod acchonietvrieb uetcionngomies
of tsocaexleis atinndg mVRePet- rseplaetceidfirce cvoienwstsrnaionttpsr. eOvnio uthsely oetxhpelro rheadn.dO, urrefs.t u[2d7y] cfooncusisdeesr sotnh ereusseearocfh into
satellitesandtheirdifferentcategoriesbasedontheirnodecapacities,locationtypes,or
2E-VRP that combines ground vehicles (GVs) and drones (UAVs), emphasizing
theparticularuseoftheterm. ThestatementfollowsthePreferredReportingItemsfor
connection mechanisms between the two echelons, such as synchronization at satellites
SystematicReviewsandMeta-Analysis(PRISMA)[28],enablingananalysisofthemost
and flexible coupling/decoupling between UAVs and GVs.
commonproblemsandrecurringsolutionmethods.
In this study, we propose a systematic review to address the Vehicle-Routing
Problem with the use of satellites, providing a guide on applying this concept and

Mathematics 2025, 13, 1092 3 of 29
contributing to existing VRP-related reviews not previously explored. Our study
considers the use of satellites and their different categories based on their node capacities,
location types, or the particular use of the term. The statement follows the Preferred
Mathematics2025,13,1092 Reporting Items for Systematic Reviews and Meta-Analysis (PRISMA) [28], enabling 3aonf 28
analysis of the most common problems and recurring solution methods.
The paper is organized as follows: Section 2 describes the materials and methods
The paper is organized as follows: Section 2 describes the materials and methods
used to perform the review using the PRISMA guidelines. Section 3 shows the obtained
usedtoperformthereviewusingthePRISMAguidelines. Section3showstheobtained
results and provides some gaps related to the literature review. Sections 4 and 5 develop
resultsandprovidessomegapsrelatedtotheliteraturereview. Sections4and5develop
discussions and conclusions.
discussionsandconclusions.
2. Materials and Methods
2. MaterialsandMethods
This research includes developing a systematic literature review. The guidelines
This research includes developing a systematic literature review. The guidelines
described in PRISMA have been used to ensure a methodological framework for this
describedinPRISMAhavebeenusedtoensureamethodologicalframeworkforthisreview.
review. According to [28], the use of PRISMA guidelines was considered by over 60,000
Accordingto[28],theuseofPRISMAguidelineswasconsideredbyover60,000papersas
papers as of August 2020 [29]. Furthermore, between 2020 and 2023, review-type papers
ofAugust2020[29]. Furthermore,between2020and2023,review-typepapersbasedon
based on PRIMA methodology exceeded 20,000 in the Web of Science database alone
PRIMAmethodologyexceeded20,000intheWebofSciencedatabasealone(verifiedvia
(verified via search string TS = (PRISMA)).
searchstringTS=(PRISMA)).
Following this methodology and the literature that applied it to its systematic
Followingthismethodologyandtheliteraturethatappliedittoitssystematicreviews,
reviews, the following steps have been conducted:
thefollowingstepshavebeenconducted:
1. Research Questions
1
2
.
. S
R
e
e
a
s
r
e
c
a
h
r c
S
h
tra
Q
t
u
eg
e
y
st ions
2
3
.
. S
S
e
e
l
a
e
r
c
c
t
h
io
S
n
t
a
ra
n
t
d
e g
E
y
valuation Process
34.. ASenlaelcytsioisn aanndd SEyvnathluesaitsi onProcess
4. AnalysisandSynthesis
2.1. Research Questions
2.1. ResearchQuestions
Two research questions were formulated to guide the review and meet the review(cid:31)s
objecTtwivoesr:e searchquestionswereformulatedtoguidethereviewandmeetthereview’sobjectives:
QQ11.. HHooww iiss tthhee ccoonncceeppt toof f““sasatetellliltietse”s ”ddefienfiende dini nthteh VeeVheihcliec-lRe-oRuotuintgin PgrPobrolebmle m(VR(VPR) P)
ccoonntteexxtt,, wwhhaatt aarree tthhee ppaatttteerrnnss inin ththee uusese oof fththe ekkeyeywworodr d“s“astaetleliltleit”e, ”a,nadn dwhwaht aatrea rteheth e
iinnccoonnssiisstteenncciieess iinn ddiiffffeerreenntt rreesseeaarrcchh ssttuuddieiess??
QQ22.. WWhhaatt aarree tthhee cchhaalllleennggeess aanndd fufututurere rereseseaarcrhch ddiriercetcitoinons?s ?
22..22.. SSeeaarrcchh SSttrraatteeggyy
TThhee sseeaarrcchh sstrtraatteeggyyf oforrc oclollelcetcitninggp appaepresrrse rlaetleadtedto ttoh ethree sreeasrecahrctohp tiocpfoicc ufosecudsoend uosnin g
tuhseinkge ytwheo rkdesyawteolrlidte ssaintelVliRtePs. Ainc oVmRPbi.n Aat icoonmobfikneaytwioonr dosf wkeityhwBoorodlse awniltohg Bicooopleearnat olorsgiwc as
coopnefiragtuorresd w(ases ecFoingfiugruer2e)d. T(sheee sFeiagrucrhet a2r).g eTtheed speaaprcehrs tfarrogmetetdh eplaapsterfisv feroymea rtshe(2 l0a1s9t –fi2v0e2 3),
iynecalursd (i2n0g1t9h–o2s0e23fr),o mincJlaunduinagry thtoosJue nfreo2m02 J4a,naunadryw taos Jluimneit e2d02t4o, paneedr -wreavsi eliwmeidtedp atpoe prseefrro-m
trheeviWeweebdo fpaSpcieerns cefroamnd tShceo pWuesbd oaft aSbcaiseensc.e Tahnedu Ssecoopfutsh edsaetadbaatsaebsa. sTehsee nussuer eosf ththaetsoe ur
lditaetraabtausrees reevniseuwreiss gthroatu noduerd liintearartoubreu srtefvoiuenwd aisti ognr,oeunncdoemd pians sian grodbiuvsetr sfeoaunnddarteiloianb, le
reenlecovmanptassosuinrgce dsi.verse and reliable relevant sources.
(TS = (Vehicle Routing) OR TS = (VRP)) AND (TS = (Satel*))
FFiigguurree 22.. SSeeaarrcchh ssttrriinngg uusseedd ttoo sseeaarrcchh rreelalatetedd ppaappeersr.s .
TThhee kkeeyywwoorrdd ““SSaatetel*l*””w wasasu suesdedto tion cilnucdluedree sreeasrecahrcwhi twhittehr mtesrlmikse l“iskaet e“lsliattee”l,li“tes”a,t el-
l“itsea”te,lolirtes”im, oirla sri,mcoilnatrr, icbounttirnigbutotinthge toto tphiec .topic.
22..33.. SSeelleeccttiioonn aanndd EEvvaalluuaattiioonn PPrroocceessss
AAccccoorrddiinngg ttoo tthhee eessttaabblliisshheedd ccrritieterriaia, ,oonnlyly ppeeere-rr-erveiveiwewede dpappaepresr psupbulbislhisehde idn iEnnEgnligshli sh
wweerree iinncclluuddeedd dduuee tot othteh uenuivneivrsearls nalatnuarteu orfe tohfe tlahnegluaanggeu. aTghee. pTuhbelisphuinbgli stihminegfratimmee wfraasm e
wasalsolimited, consideringonlypaperspublishedinthelastfiveyears, from2019to
June2024. Thistemporalselectionaimstocapturethemostrecentandrelevantresearch,
ensuringanup-to-datestateoftheart. Additionally,onlystudiesincorporatingtheterm
“satellite”intheirresearchwereconsidered,ensuringafocusedanalysisofthisspecific
aspect of the VRP. Table 1 presents the detailed inclusion criteria used in this selection

Mathematics 2025, 13, 1092 4 of 29
also limited, considering only papers published in the last five years, from 2019 to June
2024. This temporal selection aims to capture the most recent and relevant research,
ensuring an up-to-date state of the art. Additionally, only studies incorporating the term
“satellite” in their research were considered, ensuring a focused analysis of this specific
Mathematics2025,13,1092 aspect of the VRP. Table 1 presents the detailed inclusion criteria used in 4thoifs2 8selection
process. These criteria were designed to ensure consistency and objectivity in identifying
the most pertinent and suitable papers for the systematic review.
process. Thesecriteriaweredesignedtoensureconsistencyandobjectivityinidentifying
themostpertinentandsuitablepapersforthesystematicreview.
Table 1. Inclusion criteria to select articles in this review.
Table1.Inclusioncriteriatoselectarticlesinthisreview.
Criteria Description
LanguagCe riteria English Description
PLuabnlgicuaatgieon year BetEwngeleinsh 2019 and 2024 (Closed June 19)
PPuubblliiccaattiioonn yTeyapre PeeBre-trweeveinew20e1d9 jaonudrn20a2l 4ar(Ctilcolsee dJune19)
PublicationType RePseeaerr-crhev rieelwateeddj otuor tnhael aVrteihcliecle-Routing Problem with the use of
satellites.
Subject/content ResearchrelatedtotheVehicle-RoutingProblemwiththe
Thues aerotifcslaetse lmlituess.t relate the use of the satellite keyword in some
Subject/content
VRTPh evaarrtiiacnletss.m ustrelatetheuseofthesatellitekeywordin
someVRPvariants.
Database Scopus, Web of Science Core Collections
Database Scopus,WebofScienceCoreCollections
2.4. Analysis and Synthesis
2.4. AnalysisandSynthesis
The selected papers were analyzed based on the research questions. Additionally, the
Theselectedpaperswereanalyzedbasedontheresearchquestions. Additionally,the
variants of each classification, publications by year, and solution methods were analyzed
variantsofeachclassification,publicationsbyyear,andsolutionmethodswereanalyzed
to address the first research question. The database search on Web of Science and Scopus
toaddressthefirstresearchquestion. ThedatabasesearchonWebofScienceandScopus
retrieved 2593 records. Figure 3 shows the PRISMA 2020 flow diagram [28]. As shown in
retrieved2593records. Figure3showsthePRISMA2020flowdiagram[28]. Asshownin
Figure 3, the search was followed by identification, selection, and inclusion. In the
Figure3,thesearchwasfollowedbyidentification,selection,andinclusion. Intheselection
sstealgeec,ttihoen instcalugsei,o tnhcer iitnecrilausfrioomn cTraibteleri2a wfreormea pTpalbieled 2to wfieltreer ascpiepnliteifidc tpoa fipeltresrr eslcaiteendtitfioc papers
trheelatotepdic .to the topic.
FFiigguurere3 .3F. lFolwowd idagiaragmramou toliuntilningitnhge sthyset esmysatteicmliatteirca tluitreeraretuvireew reinviaecwco rinda anccceowrditahntchee wPRitIhS MthAe PRISMA
2020guidelines.
2020 guidelines.
Theselectionprocessinvolvedtwosteps:
1. RemovingduplicateDOIsfoundinWoSandScopusreducedthedatasetto1486publications.

Mathematics2025,13,1092 5of28
2. By using titles, abstracts, and keywords, a second filter was applied based on the
exclusioncriteriapresentedinTable2.
Afterapplyingtheexclusioncriteria,62papersremainedforclassification. Oneofthe
exclusioncriteriafortheanalysisistheinabilitytoaccessthepublication.
Table2.Exclusioncriteriatoselectarticlesinthisreview.
Criteria Description
Journalpapers
PublicationType
Survey/Reviewpapers
AllapplicationsofthesatelliteconceptbelongingtoVRP.
Applicationsonlyconsideringthenon-modelsatellite
Subject/content concept.
Researchtopicwithquantitativetechniquesfor
decision-making.
Access Papersonlywithfullaccess.
Inclusioncriteriawereestablishedtoensureconsistencyandobjectivityinidentifying
themostrelevantstudies. IntheScopusandWebofScience(WoS)databases,thesearch
stringindicatedinFigure2wasused,retrieving2953papersfrombothsourcescombined.
Then,onlypeer-reviewedjournalarticlespublishedinEnglishbetween2019andJune2024
(thedatethesearchwasconducted)wereconsidered,asdetailedinTable1.
Theselectionprocesswascarriedoutintwomainstages. First,duplicateDOIsfound
inWebofScienceandScopuswereremoved,reducingthedatasetto1486publications.
Then,asecondfilteringphasewasappliedbasedontitles,abstracts,andkeywords,using
the exclusion criteria defined in Table 2. The review focused on studies on the Vehicle-
RoutingProblemwithsatelliteutilization,ensuringthattheterm“satellite”wasexplicitly
linkedtoaVRPvariant,reducingtheselectionto73papers.
Finally,additionalexclusioncriteriawereapplied,suchasusingtheterm“satellite”in
anon-VRPcontext,retractedpapers,andpublicationswithoutfullaccess,amongothers,
resultinginafinalselectionof62relevantarticles.
Table3summarizestheselectionprocessstagesandtheexactnumberofexcluded
articlesateachstep.
Table3.ThesystematicliteraturereviewprocessinaccordancewiththePRISMA2020guidelines.
StageIdentification Process NumberofPapers
Screening ScopusandWoSdatabasesearchstingdownloading 2593
Screening ReviewofpaperspublishedinScopusandWoS −1107
Sub-total 1486
PapersexcluidedfornotbeingVRP,forexample,lowearth
Screening −1413
orbit(LEO)andothers
Sub-total 73
Papersexcludedbyothercriteria,suchasthefollowing:
− Noapplicationofthesatelliteconceptin
theirexperiment
Screening −11
− Retractedpaper
− PaperwithoutAccess
− Other
Included Total 62

Mathematics2025,13,1092 6of28
3. Results
Accordingtothefirstresearchquestionassociatedwiththekeyword“satellite”,the
analyzedpaperscanbecategorizedintothefollowingcategories:
− IntermediateDepots: Intermediatelocationsfortransferringproductswithcapacity
for unloading, vehicle replenishment, and storage [19], which can be fixed [13] or
mobile[18]. Forexample,ref.[13]usesparcellockersasfixedintermediatedepots
wherecustomerscanpickuptheirgoods. Inthecaseofmobiledepots,ref.[30]uses
parkinglotsasmobilestoragesatellitesforexchangingcontainers.
− Cross-Docking:Locationswithoutstoragecapacity,designedfortransferringproducts
fromonevehicletoanother[19],whichcanbedividedintothefollowingsubcategories:
◦ FixedSites: Stationslocatedinareasnotequippedfortransshipmentactivities,
asexemplifiedbyusingagasstationparkinglotforproductexchangebetween
vehicles[31].
◦ MobileSites: Deliverypointswithoutstoragecapacity,exemplifiedbyvehicle
locationswhereparcelscanbetransferredbetweenthem[32].
− SatelliteDepots: Asetoflocationswheretrailerscanbedetachedandproductscanbe
transferredbetweentrucksandtrailers[33]. Vehiclestransportingsmallervehiclesare
alsoincludedinthiscategory,suchas[34],whichdescribesaparkedvanservingasa
launchpointfordronestomakedeliveries.
− SatelliteCustomers:Acustomerthatcanbeservedwhiletheprimaryvehicleperforms
anaction,eitherthroughanalternativemeansoftransportorbyaperson,suchasa
customerthatcanbevisited“onfoot”whilethevehicleisrecharging[35].
− Withinthesecategories,thefollowingvariantswereidentified:
− PathLevel(oStep): Theprobleminvolvestwoechelonsofrouting: first,designing
routesfromdepotstoasubsetofsatellites,andsecond,routingfromthesatellitesto
servecustomers[36].
− Location: Involvesopeningspecificdepots,assigningcustomerstotheopendepots,
anddesigningvehicleroutesfromthedepotstothecustomers[37].
− Trailer Transfer: Applies to a fleet of trucks and trailers with capacity available to
serveasetofcustomers[38].
− Electromobility: Useofelectricvehicleswithzero-emissionenergy[39].
− TemporalSynchronization: Coordinationofvehiclearrivaltimesatsatellites[40].
− Multi Trip: The ability to make multiple trips to visit customers from a satellite,
delivergoods,andreturnemptytothesatellitetostartanotherjourneyorfinishatthe
depot[41].
− Multi-depots: Considerstwo(ormore)depotsfordeliveries[42].
− Pickup and Delivery: Customers with both pickup and delivery demands, where
vehiclesmustdelivergoodstocustomers,pickupothergoods,orperformboth[43].
− Randomdemands: Dynamicorsuddenlygrowingdemands[18,44].
− TimeConstraints: Classictimerestrictions(timewindows)orsynchronizationcon-
straints[45].
− DeliveryOptions: Allcustomerscanbeserveddirectlyorthroughnearbycoverage
locations,withthedecisionmadebythedistributor[13]orotheroptions([46]).
InTable4,thecompleteclassificationofeacharticleincludedinthisstudy,organized
bycategoryandvariant,canbefound:

Mathematics2025,13,1092
7of28
Table4.Classificationbycategoriesandvariants.
Categories
|                          |     |     |               |     |     |     | Satellite | Satellite |
| ------------------------ | --- | --- | ------------- | --- | --- | --- | --------- | --------- |
| IntermediateFacilitiesor |     |     | Cross-Docking |     |     |     |           |           |
|                          |     |     |               |     |     |     | Depots    | Customer  |
Depots
| Variants |     |     | Fixed |     | Mobile |     |     |     |
| -------- | --- | --- | ----- | --- | ------ | --- | --- | --- |
PathSplitting [13,15,18–20,30,40–44,46–69] [8,14,16,31,70–75] [17,22,32,76–80] [12,34]
| Location        |                  | [66,68,69] |     | [74,75] |     |     | [12]       |         |
| --------------- | ---------------- | ---------- | --- | ------- | --- | --- | ---------- | ------- |
| TrailerTransfer |                  |            |     |         |     |     | [38,81–83] | [84]    |
| Electromobility | [20,61–63,66,67] |            |     | [85]    |     |     | [34,83,84] | [35,84] |
Temporal
|     |     | [40] |     | [14,74,75] |     |     | [34,83] |     |
| --- | --- | ---- | --- | ---------- | --- | --- | ------- | --- |
Synchronization
| MultiTrip   |     | [19,41]       |     |        |     | [17] |     |     |
| ----------- | --- | ------------- | --- | ------ | --- | ---- | --- | --- |
| Multi-depot |     | [40,42,46,64] |     | [8,75] |     | [32] |     |     |
Pickupand
[19,43,56–59,69]
Delivery
Random
[18,44]
demands
[15,19,41,52–
| TimeConstraints |     |     |     | [14,72,73,75] |     | [32,76] | [34,82,83] | [35,84] |
| --------------- | --- | --- | --- | ------------- | --- | ------- | ---------- | ------- |
55,58,59,62,63,65]
DeliveryOptions [13,30,43,46,50,57,60,64,66] [8,16] [32,78] [12]
Next,eachofthearticlesindicatedinthetablewillbedescribedaccordingtotheuse
ofthekeywordsatellite:
3.1. DescriptionofArticles
3.1.1. IntermediateDepotsorFacilities
Inref.[47], thecapacitated2E-VRP(2E-CVRP)ispresented, wheresatellitesactas
“intermediatedepots”,aimingtominimizedeliverycostswhileconsideringvehiclecapacity
and satellite locations. The authors introduce a route-based formulation without flow
variablesandnewconstraintsforflowbalancingatsatellitesandproposeanimproved
branch-cut-and-price (BCP) algorithm with a novel branching strategy. This approach
solvesinstanceswithupto200customersand10satellites,generatingnewinstanceswith
upto300customersand15satellites. Conversely,ref.[48]addressesthe2E-CVRPusinga
matheuristicbasedonthe“cluster-firstroute-second”approach,applyingittoinstances
rangingfrom21to200customers,3to200vehiclesinthefirstechelon,4to1026vehiclesin
thesecondechelon,and4to10satellites.
Meanwhile,ref.[49]tacklesthe2E-VRPusinganembeddedHamiltoniangraphand
proposes the EHG-HA heuristic algorithm based on two schemes: initialization with
Hamiltoniangraphsanddynamicsatelliteadjustment. Thisapproachappliestoinstances
ranging from 21 to 200 customers, 2 to 10 satellites, 2 to 5 vehicles in the first echelon,
and 4 to 100 vehicles in the second. In ref. [50], the 2E-VRP is studied in e-commerce,
wherevanstravelfromthedepottothesatellites,andmotorcyclesdeliverfromsatellitesto
customers. K-meansclusteringandthe2-optalgorithmoptimizeroutesininstanceswith
100customers,10satellites,and2to10clusters. Similarly,ref.[51]introducesthe2EVRP
withTransshipmentNodesandOccasionalDrivers(2EVRP-TN-OD),whichincludesOD
to reduce operational costs. The problem is formulated as a mixed-integer nonlinear
programming(MINLP)andsolvedforinstancesrangingfrom1depot,2satellites,and
12customersto1depot,4satellites,and50customers.

Mathematics2025,13,1092 8of28
Noteworthyarethedifferentalgorithmsusedtoaddressthe2E-VRPinthesestudies,
includingexacttechniqueslikeBCPin[47],heuristicssuchasEHG-HAin[49],clustering
in [50], and occasional drivers in [51], applied to scenarios with varying instance sizes
andconfigurations.
The following studies focus on the 2E-VRPTW variants. In ref. [15], route costs
areminimizedusingaBranchandPrice(BP)algorithmappliedtoinstanceswithupto
100customersand5satellites. Incontrast,ref.[52]introducesthetwo-echelonemergency
Vehicle-RoutingProblemwithtimewindowassignment(2E-EVRPTWA)inthecontext
ofsupplydistributionduringtheCOVID-19outbreakinChongqing,China. Theyusetri-
objectivemixed-integerprogramming(MIP)anddevelopamulti-objectiveadaptivelarge
neighborhoodsearchwithasplitalgorithm(MOALNS-SA)tooptimizeoperationalcosts
anddeliverytimes,solvinginstanceswith30to60customers(thenumberofsatellitesisnot
specified). Ref.[53]addressesthee-orderfulfillmentproblem(EOFP),focusingonminimiz-
ingcostsandmeetingtimewindowsbyassigningorderstofulfillmentcenters(satellites).
Theyuseamixed-integerlinearprogramming(MILP)modelandadecomposition-based
approachwithagreedyheuristicandadaptivelargeneighborhoodsearch(ALNS).Thisap-
proachisappliedtoinstanceswith4–8distributioncentersand20–400customers. Ref.[54]
presents the 2E-VRP with time constraints (2E-TVRP), solving time-constrained routes
usingaMILPmodel,asavingsalgorithm,andvariableneighborhoodsearch(VNS)for
realisticinstanceswithupto23satellitesand1008customers.
Ref.[55]introducesthe2E-VRPwithdirectdeliveriesandaccessTW(2E-VRPDDATW),
whereheavytrucks’accesstourbanareasisrestricted. TheyproposeaMILPandALNS,
solvinginstancesrangingfrom1depot,3satellites,and15customersto6depots,5satellites,
and100customers.
Intheresearchon2E-VRPwithSimultaneousPickupsandDeliveries(2E-VRPSDP),
ref.[56]solvesinstanceswithupto200customersand10satellitesusingVNS.Ref.[57]
studies the 2E-VRPSPD to minimize the total travel distance using a hybrid heuristic
calledKNN_ALNS,whichcombinestheK-NearestNeighborhoodalgorithm(KNN)and
ALNS.Inthisapproach,customersarefirstassignedtosatellitesusingKNN,initialroutes’
solutions are generated, and, finally, ALNS is applied to improve them. The instances
consideredrangefrom60customersand2satellitesto100customersand5satellites. It
shouldbenotedthat[56]usesVNStosolvelargerinstancesthan[57].
Foritspart,ref.[43]addressesthe2E-VRPwithgroupingconstraintsandsimultaneous
pickup and delivery (2E-VRPGS), where a vehicle from the same satellite must serve
customerswithinthesameadministrativeregion,addingadimensionofgeographicand
groupingconstraints. Thegoalistominimizeoperatingcostswhilesatisfyingthecapacity
constraintsofvehiclesandsatellites.Theauthorsproposeapath-basedmodelandBCPwith
anoveldominanceruleinthelabelingalgorithmandcustomizedvalidinequalities. The
instancessolvedrangefrom20customersand2satellitesto100customersand10satellites.
Ref. [58] addresses the 2E-VRPTW with simultaneous pickup and delivery (2E-
VRPTWSPD),usingsatellitesasintermediatedepotstoreceiveproductsfromthecentral
depot,deliverthemtocustomers,collectorders,andsendthembacktothedepot. The
authorsproposeanMIPformulationandvariableneighborhoodtabusearch, applying
dummysatellitesandtimewindowstospeedupthesearch. Computationaltestswith
exactalgorithmswereperformedwithinstancesof7to12customersand2satellites,while
theheuristicwastestedoninstanceswithupto200customersand10satellites.
Ref.[59]aimstominimizetraveltimesandfuelconsumptiontoreducevehiclepollu-
tion,addressingthetwo-echelonpollution-routingproblemwithsimultaneouspickupand
deliverybyconsideringmultipletimewindows(2E-PRPSPD-MTW).Inthefirstechelon,
vehiclesdeliverandpickupgoodsatsatellites,andinthesecondechelon,thefleetmoves

Mathematics2025,13,1092 9of28
fromthesatellitestothecustomers. Theauthorsusethemulti-objectiveVNS(MOVNS)
algorithm,solvinginstanceswithupto100customersandfivesatellites.
Anothervarianttoanalyzeistheuseofbicyclesfordeliveries,whereref.[60]addresses
thelarge-scalebikesharingrepositioningproblem(BSRP)anddesignsoptimalroutesfrom
the central depot to satellite stations and then to customer stations. The objective is to
minimizetransportationandinventorycosts,adaptinga3E-VRPstructurefortheBSRP
andincorporatingafuzzyclusteringstrategyandafuzzycorrelation-basedadaptiveVNS
(FC-AVNS)algorithm. Inthiswork,instancesrangingfrom100to519withafleetof3to
8vehicleswithvariablecapacitieshavebeenusedtotesttheperformanceoftheapproach.
Foritspart,ref.[13]studiesthe2E-VRPwithcoveringoptions(2E-VRP-CO),inwhich
thefirstecheloninvolvesdeliveriesfromacentraldepottosatellitesandcoveragepoints,
such as parcel lockers, where customers pick up their products. In the second echelon,
products are distributed from the satellites to the customers using cargo bicycles. The
authorsproposeaMIPmodelanduseanALNStosolveinstanceswithupto101nodes,
5bicycles,and10satellites.
Ref.[30]presenta2E-CVRPthatcombinesvansandbicycles,introducingtheconcept
ofstandardcontainersandintegratingtramsanddecentralizedsatellites. However,unlike
previousstudies, theintermediatedepotsaremobile, offeringadistinctapproach. The
studyevaluatesvariousscenarios,suchastram–bikesystemswithstandardcontainers
andconsolidationcenters, designingaflexiblemodeltooptimizedistributioninurban
systems. Thisstudyintroducesamodifiedmulti-startheuristicalgorithmconsideringthe
costsincurredinbothechelonsaftereachallocation.Thealgorithmoperatesinthreephases:
initialclustering,clusteringimprovementthroughlocalsearch,anditerativereassignment
ofcustomerstosatellitesusingamulti-startapproachthatadjustsassignmentsbasedon
capacityandcostsinbothechelons. Theresearchvariesinbothmethodologiesandthe
size of the instances solved: Ref. [60] applies fuzzy clustering to instances with up to
519stationswithoutspecifyingthenumberofsatellites;Ref.[13]usesbicyclesandlockers
in instances with up to 101 nodes and 10 satellites; whereas ref. [30] focuses on more
complexmodels,incorporatingmultiplecombinationsofvehiclesandscenarios,giventhe
mobilenatureofdepots,proposingamoresophisticatedheuristicalgorithmfordifferent
logisticalconfigurations.
Regardingtheuseofelectricvehicles,ref.[61]presentsa2E-VRPwithrechargestations,
whereautomatedguidedvehicles(AGVs)mustrechargeduringtheirroutestomaintain
continuousoperation.Themainobjectiveistominimizetotaloperatingcostsandmaximize
theroutingefficiencyoftheAGVs. Theauthorsproposeamathematicalmodelandsolve
itusingacombinationoftheArbitraryInsertionAlgorithm(AI)togetherwithaGenetic
Algorithm (GA) and Hill Climbing Algorithm Improving (HC). The solved instances
includebetween48and96customers,with10satellitesand4vehicles,demonstratingthe
viabilityoftheproposedapproachacrossdifferentlogisticsnetworksizes.
Ontheotherhand,ref.[62]presentsa2E-VRPwithelectricvehicles,timewindows,
andbattery-swappingstations(2E-EVRPTW-BSS),wherethefleetincludesinternalcom-
bustionvehicles(ICVs)inthefirstechelonandelectricvehicles(EVs)inthesecondechelon.
Unlike[61],thisworkintegratesthecoordinationbetweenvehiclesofdifferenttechnolo-
gies, proposing a mixed-fleet scheme that ensures synchronization of the arrival times
of ICVs at the satellites. The solved instances with VNS are larger, with up to 200 cus-
tomers,10satellites,and40battery-swappingstations(BSS),makingitmoreapplicableto
urbanscenarios.
Similarly,ref.[63]addressesthe2E-EVRPbyaddingtimewindows(2E-EVRP-TW),
wheretheprimaryobjectiveistominimizetransportationcosts. Theproposedsolution
combinesMILPwiththeClarkeandWrightsalgorithm(CW)togenerateinitialsolutions,

Mathematics2025,13,1092 10of28
followedbyVNSimprovement. Whileitsharesthecostoptimizationgoalwith[61,63]
focusesonanurbansettingwheresatellitesarelocatedinthesurroundingareasofcities,
solvinginstancesrangingfrom5customersand2satellitesto100customersand21satellites.
Inturn,ref.[20]usesfossilfuelvehiclesinthefirstechelontotransportgoodsfrom
the depot to the satellites, while EVs are employed in the second echelon. This study
focusesonminimizingtransportationcosts,consideringthechargingneedsofEVs,and
proposesaschemeBPwithanarcflowmodeldecomposedintoanintegermasterproblem
toderivelowerboundsandapricingsubproblem.Theinstancesaddressedherearesmaller
than[61],solvingupto20customers,2satellites,and2rechargestations.
Othervariantsusedinconjunctionwith2E-VRPincludemulti-depotsystems. For
example,ref.[46]tacklesthemulti-depottwo-echelonVehicle-RoutingProblemwithde-
liveryoptions(MDTEVRP-DOs),designingroutesfrommultipledepotstosatellitesand,
subsequently,fromthesesatellitestocustomers. Theobjectiveistooptimizeroutesusing
simulatedannealing(SA)metaheuristic,consideringcapacityandworktimeconstraints.
Thesolvedinstancesrangefrom1depot,4satellitestations,10pickuppoints,and50cus-
tomersto3depots,12satellitestations,30pickuppoints,and200customers,reflectingits
capabilitytomanagelogisticsnetworksofvarioussizeswithmultipledeliveryoptions.
Refs.[40,42]presentcomplementaryapproaches. Ref.[42]focusesonthe2E-VRPwith
multi-depotfuelminimizing(MD2E-FMRP),aimingtominimizefuelconsumptionwitha
heterogeneousfleet. Forthispurpose,theyproposeaMIPformulationandusedriving
cyclessimulatingspeedvariations,allowingvehiclestoreturntoanysatellite. Testsinclude
upto56nodes,andALNSprovedmoreefficientintimethanGurobiinsolvingtheproblem
withinthetimelimitof10,000s.
Meanwhile,ref.[40]introducestheMulti-CommodityTwo-EchelonVehicle-Routing
ProblemwithSatelliteSynchronization(MC-2E-VRPSS),whichcombinesdepotsandsatel-
litesinafleetsynchronizationenvironment. TheauthorsdevelopanMIPandALNSto
solveinstancesrangingfrom5customersand2satellitesto275customersand19satellites,
standingoutforitsabilitytohandlemultipleproductsandtheneedforsynchronization
betweenechelonsofthelogisticssystem.
Incontrast,thestudiesby[18,64,65]exploreotheraspectsofthe2E-VRPwithinterme-
diatefacilities(2E-VRPTW-IF).Ref.[65]addressesthe2E-VRPTW-IF-OD,whichintroduces
intermediatefacilitiessuchasparcellockersortransshipmentnodes. Thisstudyemploys
aMILPmodelandaHybridALNS(HALNS),solvinginstanceswithupto50customers,
4satellites,and8transshipmentnodes,addinglogisticalcomplexity. Ref.[64]focuseson
enhancingtheefficiencyandsustainabilityoftheparceldistributionnetworkbyoptimizing
satellitelocations,conductingexperimentswithreal-worldinstancesinParis,France,and
evaluatingsustainabilityusingperformanceindicatorssuchasequivalentcarbondioxide
emissions, among others. They use unsupervised machine learning to assign delivery
pointstosatellitesandanearest-neighbor(NN)-basedalgorithmtodesignsecond-echelon
routes,solvinginstanceswithupto50customersand4satellites. Finally,ref.[18]proposes
thetwo-echelondynamicVehicle-RoutingProblemwithproactivesatellitestations(2E-
DVRP-PSSs),wheretrucksfirstservestaticcustomersandproactivesatellitestations(PSSs),
while light vehicles handle dynamic demand. To solve the problem in small instances,
theauthorsusecuttingplanesand,forlargeinstances,ahybridalgorithmthatcombines
improvedGAandtabusearch(GA-TS),highlightingtheabilitytorespondtodynamic
demandsinreal-time.
The multi-trip 2E-MTVRP is another relevant variant. Ref. [41] addresses the 2E-
VRPTW,utilizingsatellitesforloadingandunloadingbetweenechelons. Thisstudyaims
tominimizeoperationalandtransportationcosts. Tosolvetheproblem,theyfirstformulate
aMILPandsolveitusingBCP,incorporatingcolumngenerationandacutenumeration

Mathematics2025,13,1092 11of28
procedure for elementary routes adapted for multiple trips. Instances solved include
6 distribution centers, 5 satellites, 100 customers for single trips, and 8 satellites with
100customersformultipletrips.
Ref.[19]introducesthe2E-MTVRPwithcapacitatedsatellitesandreverseflows(2E-
MTVRP-CSRF).Thegoalistoproposeandevaluateasolutionalgorithmfortheproblem.
The authors developed a matheuristic, formulating a refined MILP and optimizing the
routesusingeachechelon’slargeneighborhoodsearch(LNS)algorithm. Theyalsoverify
solutionfeasibilitythroughlow-complexitytests. Instancesusedinclude50customers,
1vehicleinthefirstechelon,5vehiclesinthesecondechelon,and2,4,or8satellites;for
instanceswith100customers,thereare2vehiclesinthefirstechelonand10inthesecond
echelon,withthesamenumberofsatellitesasinthe50-customerinstance.
Ref.[44]presentsthe2E-VRPwithdemandblowout(2E-VRPDB).Thesolutionpro-
poses a hybrid fireworks algorithm (HFWA), combining the optimal cutting algorithm
(OCA)withanimprovedfireworksalgorithm(IFWA),whereastrategycalledtime-division
distribution(TDD)isfirstimplementedtomitigatedemandpressure. Instancesrangefrom
22to51customers,4to5vehicles,andupto10satellites(vehiclesandsatellitesarenot
specifiedindetail).
LRPisalsopresentasanadditionaltwo-echelonvariant(2E-LRP).Ref.[68]proposes
the2E-LRPwithrecommendedsatellites(2E-LRPRS),whichcanbereoptimized. Tosolve
thisproblem,theauthorsformulateanMILPandaBP.Solvedinstancescontainbetween
60and129customers,4to18vehicles,and4to10satellites. Ref.[69]addressesthe2E-
LRPSPD,presentingaMILP.Tosolvetheproblem,theyformulateaMILPandaBranchand
Cut(BC)toobtainsolutionsformedium-sizedinstances. TheyuseIteratedLocalSearch
andVNS-basedmetaheuristicalgorithms(ILS-VNS)andaVNS,whereILS-VNSprovides
initialsolutionsfortheBC,andVNSimproveseachbranching. Instancesrangefrom25to
200customers,5to10satellites,vehiclecapacitiesof750and850inthefirstechelon,and
100and150inthesecondechelon.
Ref.[66]addressesthemulti-modallastmilesystemasa2E-LRPwithmixedvehicles
andmixedsatellites(2E-LRP-MVMS),motivatedbythee-grocerydistributionindustry. It
incorporatesparcellockers(satellites)andautonomousdeliveryrobots(ADRs). Theobjec-
tiveistooptimizethelocationsofdepotsandsatellites,thenumberofparcelsdelivered,
andtheroutesinthetwoechelonstominimizecostsandcarbonemissions. Theyformulate
adistributionnetworkcombiningvans,parcellockers,androbots. Tosolvethisproblem,a
hybridimmunealgorithm(HIA)isintroduced,solvinginstanceswith2to12depots,3to
16satellites,7to26customers,2to9vans,and2to7ADRs.
IntheUAVvariant,ref.[67]aimstominimizetransportationcostsandemissionsin
adistributionnetworkfore-grocerydistribution,utilizingautonomousdeliveryvehicles
(ADVs). Theauthorsformulatea2E-VRPwithmixedvehicles(2E-VRP-MV)withanon-
linearobjectivefunction. Theproposedsolutionalgorithmisatwo-stepclustering-based
hybridGAandParticleSwarmOptimization(C-GA-PSO).Inthesolution,customersare
clusteredatsatellites(intermediatedepots)basedonminimumdistanceandmaximized
demand. Experimentswereconductedwithupto100customers.
3.1.2. Cross-Docking—Fixed
Cross-docking is the direct transfer of products from inbound vehicles to delivery
vehicles without intermediate storage [86], which can occur at fixed points in specific
locations. Incross-dockingwithfixedsatellites,the2E-VRPvariantpredominates. In[70],
a 2E-VRP with stochastic travel time is solved using simheuristics, a combination of
simulation and optimization. Satellites are referred to as Urban Consolidation Centers
(UCCs)beforefinaldeliverytocustomers. Tosolvetherouting,theyusedanalgorithm

Mathematics2025,13,1092 12of28
basedontheNearestNeighborProcedure,appliedtorealdatafromadeliverycompanyin
Paris,involving90,627deliveriesof4depotswith5satelliteseach. Thisstudyisnotablefor
incorporatingstochastictraveltimefromatriangulardistribution.
Ref. [71] integrate production into the 2E-VRP with cross-docking satellites (2E-
PRPCS),which,unlikeotherstudies,determinesdailyproduction,thenumberofdeliveries
fromdepottosatellitesandsatellitestocustomers,aswellasnetworkroutes,achieving
agoodbalancebetweenproductionandrouting. Satellitesactasintermediatepointsfor
cargotransferbetweenvehicles. TheauthorsformulateanMILPanddesignaBCalgorithm
andamatheuristictoobtaininitialsolutions,solvinginstanceswith10to35customers,2
to3satellites,and4or6satellitevehicles.
Ontheotherhand,ref.[31]addressesthe2E-VRPwithFixedFleetHeterogeneous(2E-
HVRP),wherevehiclesmuststopatintermediatepoints—gasstationsinthiscase—before
deliveringproducts. Theyuseanefficientisland-basedmemeticalgorithmwithalocal
searchprocedurebasedontheLin–Kernighanheuristic(IBMA-LK),testingtheirapproach
oninstanceswith50to125customersand20to30satellites.
Refs.[72,73]addTWtothe2E-VRP(2E-VRPTW).Ref.[72]developsanexactbranch-
price-and-cut (BPC) algorithm. In this approach, satellites serve as points where high-
capacity vehicles transfer goods to lower-capacity vehicles for final customer delivery.
Theyuseatwo-pathformulation(2E-2P)tosolveinstanceswith15to100customers,2to
6depots,and3to5satellites.
In contrast, ref. [73] presents the last mile delivery problem with scheduled lines
(LMDPSL),whichleveragestheunusedcapacityofanestablishedpublictransportation
system. Satellites are dedicated stations in this transportation network where vehicles
collectgoodsforfinaldelivery,addingtimewindowsandintermediatereplenishment. A
BPCisdevelopedandevaluatedoninstanceswith50,100,and150customersandallows
theexactandheuristicsolutionoftheLMDPSL.
Ref.[14]introducesthe2E-VRPwithsatellitebi-synchronization(2E-VRP-SBS),where
satellitesfunctionastransshipmentpointstoconsolidateandtransferloadsbetweentrucks
fromdifferentechelons. Theproblemissolvedusingamixed-integerprogrammingmodel
withCPLEXandamodifiedALNS(mALNS)ininstanceswithupto17originsatellites,
17destinationsatellites,and120customerspersatellite.
Meanwhile, ref. [8] developed a 2E-MDCVRP model for e-commerce applications
withatwo-stagesolutionprocess. Inthefirststage,satellitesarepositionedascentroids
in the clusters using the k-Means algorithm to form k-cluster sets, and the Repetitive
NearestNeighboralgorithmisemployedtodeterminetravelroutesinthesecondechelon.
Inthesecondstage,thetrial-and-errormethodestablishesroutingschedulesinthefirst
echelon. Althoughtheabstractmentionsthatsatellitestraveltothecustomers,theproblem
developmentclarifiesthatvehiclestravelfromsatellitestocustomers.
Ref.[16]introducesthe2E-CVRPwithSwapContainers(2E-CVRPSCs),wheresatel-
lites serve as transfer points between vans and bicycles. They develop a mathematical
formulationwithasymmetricdistancematricesforbicyclesandaParallelizedLNS(PLNS)
heuristic,evaluatedoninstancesrangingfrom21to300customerswith2to15satellites,
thoughthenumberofvehiclesusedintheinstancesisnotspecified.Theyalsoincorporated
groupingtomaketheinstancesmorerealistic.
ForLRPstudies,ref.[74]proposesaninnovativeTwoEchelonsLocationRoutingProb-
lem(2E-LRP)modelthatincorporatestemporalsynchronizationofvehiclesatsatellites
(2E-CLRPVS),appliedtotheGreaterMontrealarea. Satellitesactastransferpointsbetween
vehiclesfromdifferentechelons, andthemodelpenalizeswaitingtimesusingaBinary
VariableFixing(BVF)method. Instancesinvolve10to99customers,5satellites,2distribu-
tioncenters,andhomogeneousfleetsperechelon,thoughthefinalfleetisheterogeneous,

Mathematics2025,13,1092 13of28
with4to10vehiclesinthefirstechelonand10or15inthesecondechelon. Thisstudyhas
theadvantageofbeingareal-worldapplication.
In contrast, ref. [75] examines the Two-Echelon Multi-Attribute Location-Routing
ProblemwithfleetSynchronizationatintermediatefacilities(2E-MALRPS),whichincludes
multicommoditydemand,timewindowsfordeliveries,capacityconstraintsatsatellites,
andfleetsynchronizationbetweenechelons. TheauthorspresentanMIPmodelsolved
usingadynamicdiscretizationdiscovery(DDD)-basedalgorithmandahybridformulation,
wherenodesrepresentingfacilitiesareduplicatedineachperiod,whilecustomernodes
appearonlyinrelevantperiods.Instancesrangefrom5to50origin-to-destinationdemands,
with3to5satellitesandupto6potentialplatforms.
Comparing the two studies, ref. [74] focuses primarily on vehicle synchronization
withpenaltiesforwaitingtimesatsatellites,whileref.[75]expandstheproblemtoinclude
multicommoditydemandandadditionalconstraintsliketimewindowsandlimitedsatellite
capacity,offeringamorecomplexandmultidimensionalapproachthan[74].
ForUAVstudies,ref.[85]designsaplanfortransportingproductsfromdistribution
centersonthecity’speripherytosatellites(transshipmentpoints)withinthecityusing
a mixed fleet of autonomous and manual vehicles. This problem is termed the service
network design problem with mixed autonomous fleets (SNDMAFs). The authors for-
mulateanintegerprogram(IP)anddevelopacustomalgorithm,DDD-SNDMAF,which
enhancestheDDDframeworktoprovideoptimalsolutionsfortheSNDMAF.Instances
involve5externalzones,4ofwhichhave1depot,6to9satellites,and18to24products,
whilethefifthzonehas2depots,8satellites,and18to27products. Thisstudyincorporates
mixedfleetsofautonomousandmanualvehiclesinanurbanenvironment,representinga
significantadvancementintransportnetworkplanningforsmartcitiesandaddressingthe
challengeofintegratingnewtechnologiesintourbanlogistics.
3.1.3. Cross-Docking—Mobile
Ref.[17]addressesthe2E-MTVRPwithadynamicsatellite(2E-MTVRPDS),incorpo-
ratingcollectionanddynamicinformationusage. Here,satellitesaremobileintermediate
pointsinfragmentedagriculturalfields,enablingefficientgrainharvestingandtransport
coordination. This study introduces multiple trips in the first echelon and employs a
MemeticAlgorithm(MA)combiningaGAandaLocalSearchProcedure(LSP)tosolve
the problem. Instances include between 50 and 225 farmlands, 6 harvesters, and up to
6 trips. Ref. [22] introduces a two-echelon city logistics system with on-street satellites
(2E-CLS-OS),employingVNSandCWtooptimizeinitialroutes,testedoninstanceswith
upto900customersand30satellites.
Studies[79,80]tackle2E-VRPlogisticsproblemswithdifferentapproachesandsatellite
configurations. Ref.[79]proposesaGraph-BasedFuzzyEvolutionaryAlgorithm(GFEA)
to handle the 2E-VRP by assigning satellites to customers using fuzzy operators and
optimizingroutesoninstancesofupto200customersand10satellites. Incontrast,ref.[80]
introducesthe2E-CVRPwithSharingSatelliteResources(2E-CVRPSSR),solvingsmaller
instances(upto50customersand5satellites)withaMILPandALNSapproach. While
ref.[22]focusesonreal-timerouteoptimizationwithon-streetsatellites,and[79]innovates
withevolutionarylearning,ref.[80]optimizessharedsatelliteuseforgoodsconsolidation.
Allthreestudiestargetthe2E-VRP.
Ref.[32]introducesvariantswithmobilesatellites,timewindows,andintermediate
multi-depotsinalastmiledeliverysystem,utilizingmultiplelocaldepotsandmulti-modal
deliveryoptions. Satellitesaretemporaryon-streetlocationswherevehiclescantransfer
packagestoeachotherorbicycles.Thisnovelapproachintroducesmobilityandoperational
flexibility. Thestudyformulatesamathematicalmodelanddevelopsatwo-phaseheuristic:

Mathematics2025,13,1092 14of28
aconstructivephasethatusesbiasedrandomizationtoincrementallybuildsolutionsby
cost-rankedrandomselectionandanimprovementphaseoptimizingsolutionswithlocal
searchtechniquessuchastwo-optandcut-and-insert. Instancesspan50to440customers
with5to17satellites,distinguishingthisapproachthroughitsmobilesatelliteapplications
andtime-windowoptimization.
Ref.[76]focusesonintegratingIntervalTravelTimes(ITTs)intotheVRP,optimizing
routesbetweensatellitesandacentraldistributioncenter(CDC).Satellites,inthiscase,are
fixedbuttemporarytransferpointsthatimproveefficiencybyaccountingfortraffic-induced
traveltimevariations. TheLANTIMEmetaheuristicsolvesthisproblem. Instancesare
basedonrealtrafficdatafromcitieslikeStuttgartandNewYork,with37and24satellites,
respectively,reflectingatraffic-optimizedfixedapproach.
Unlike[76],whichsolelyaddressesthe2E-VRPwithITT,bothrefs.[77,78]incorporate
mobilesatelliteusage. Inref.[77],themodelextendstothetwo-echeloncitydispatching
modelwithmobilesatellites(2ECD-MS)byintroducingcrowd-shipping(2ECD-MS-CS).
Satellitesaretruckstransportinggoodsfromadistributioncenter, andcrowd-shipping
respondstofastdeliverydemandswithtimewindows.ThealgorithmisaMulti-Directional
EvolutionaryAlgorithm(MDEA),andinstancesrangefrom50to200customerswithupto
10mobilesatellites. Conversely,ref.[78]presentsthe2ECD-MSwithtrucksdispatchingdi-
rectly(2ECD-MS-TDD),wheresatellitetrucksrepositiondailybasedoncustomerdemand.
VNSoptimizesroutesforupto200customersand10mobilesatellites,differingfrom[77]
byemployingdailyrepositioningofmobiledepots.
3.1.4. SatelliteDepots
AnimportantvariantinthiscategoryistheTTRP,asaddressedby[38],wherethe
authorstacklethecapacitatedTTRP(CTTRP).Inthisstudy,satellitesactasdepotsforcargo
transfers,andtheauthorsproposeatwo-commodityflowformulationalongwithaBC
algorithmtomodeltheflowofgoodstransportedbytruckswithandwithouttrailers. The
solvedinstancesincludeupto50customers,30servedbytrucks,2to4trailers,andup
to7availabletrucks. Incontrast,ref.[81]focusesontheextendedsingleTTRP(XSTTRP),
developingahybridmetaheuristic,AVXS,applicabletootherroutingproblems. Thissolu-
tioninvolvesphasesofassignment,constructionofaninitialsolution,andimprovement,
consideringsatellitesaspointswheretrailersaretemporarilyparkedwhiletrucksserve
customers. Theinstancesrangebetween21and145customers,5to116parkingspots,and
between6and21satellites. Comparatively,ref.[38]presentsamorespecificapproachwith
strictercapacity constraints, while [81] offersa more generaland flexiblesolution fora
largernumberofcustomersandsatellites.
Inref.[82],theauthorsintroducetheProfitableSingleTTRPTW(PSTTRPTW),which
incorporatescapacityconstraints,timewindows,andcustomeraccessibility. Inthiscase,
satellites serve as depots where trailers can be decoupled from trucks. To address the
problem, the authors formulate an Integer Programming (IP) model and develop a BC
algorithm, solving instances with 9 to 46 customers and 1 to 6 satellites. Conversely,
ref. [83] explores the Truck-Drone Routing Problem with Time Windows (TDRP-TW),
wheresatellitesarecustomerlocationsactingasdronelaunchandrecoverypoints. The
authorsemployaBPCwithanALNS,namedALNS-BPC,solvingsmall-andmedium-sized
instanceswithupto50customersandlargeroneswith100customers. Itshouldbenoted
that[83]introduceddronesoperatingfromlaunchpointsontruckroutestotheTDRP-TW,
providingflexibilitybyincludingairtransportfromcustomerlocationsassatellites.
Inref.[12],theauthorsproposeanovelvariantofthe2E-LRP-MS,wherefixedsatellites
arereplacedbyfirst-levelvehicles(CT)actingasmobilesatellites,supplyingsecond-level
vehicles(CF)duringdeliveryroutes. TheyusetheheuristicClustering-BasedSimultaneous

Mathematics2025,13,1092 15of28
NeighborhoodSearch(CSNS),combinedwithK-meansforclusteringandselectingconsoli-
dationpoints(CP),prioritizedthroughFitnessProportionateSelection(FPS).Generated
routesareoptimizedusingfourlocalsearchalgorithms(Self-insert,Self-swap,Peer-insert,
Peer-swap). Solvedinstancesinclude20to200customers,5to10tripsfromthecentral
depot,and5to10consolidationpoints. Thisstudyintroducesmobilesatellites,provid-
inggreaterflexibilityforin-routereplenishmentandrevolutionizingthesatelliteconcept
by making them mobile, allowing for a more dynamic and adaptable approach to last
milelogistics.
Inref.[34],theauthorsintroducethe2E-VRPwithTimeWindowsandMobileSatellites
(2E-VRP-TM),incorporatingTWconstraintsandsynchronizationofmobilesatellites. In
thiscase,satellitesarevanstransportingUnmannedAerialVehicles(UAVs). Tosolvethe
problem,theydevelopedamathematicalformulationandanALNS.However,theydidnot
directlytestthemodelbutevaluatedALNSeffectivenessin21instances,solvingproblems
with100customers,upto5satellites,and33UAVs. Thisstudyemphasizessynchronization
betweenvansasmobilesatellitesanddrones,unlike[83],whichutilizesdroneslaunched
fromfixedpoints.
3.1.5. SatelliteCustomers
Inref.[35],theauthorspresenttheElectric-Vehicle-RoutingProblemwithTimeWin-
dowsandSatelliteCustomers(E-VRPTWsc),whichintroducesthepossibilityofanelectric
vehiclevisitingcustomersusinganalternativemodeoftransportwhilerechargingatasta-
tion. Inthiscontext,satellitesaredefinedascustomerswhocanbeservedbyanalternative
modeoftransportduringthevehicle’schargingtime,optimizingthisperiod. Theauthors
proposeamathematicalmodelandanIteratedLocalSearch(ILS)metaheuristicreinforced
byVariableNeighborhoodDescent(VND)andSetPartitioning. Instancesconsiderupto
100customers,between2and18vehicles,andupto15satellitecustomers.
Inref.[84],theauthorspresenttheTruckandUnmannedVehiclesRoutingProblem
with Time Windows (TUVRP-TW), where satellites are the customers. Trucks dispatch
orcollectUnmannedVehicles(UVs),whichcanserveonecustomerandbepickedupat
another,introducingasynchronizationelement. Toaddresstheproblem,theyformulate
a mathematical model and apply a hybrid approach using GRASP to generate initial
solutions,whicharethenimprovedthroughVNS.SolvedinstancesarebasedonSolomon’s
classicVRPTWproblems, accommodatingupto100customers, withupto75%served
by UVs. This study stands out in terms of integrating autonomous vehicles into last
milelogistics.
3.2. UsedInstances
Belowisananalysisoftheinstancesusedintheresearch,classifiedbasedonwhether
theywereobtainedfromexistingliteratureintheavailabledatabases,adaptedfromlitera-
turetoaddressthepresentedproblem,orcreatedbytheauthors. Theanalysisincludes
informationonfrequencyandpercentageofuseandtheauthorswhoutilizedthem. This
aimstoprovideaclearandstructuredoverviewoftheutilizationoftheseinstancesinthe
studiedcontext.
3.2.1. LiteratureInstances
Theanalysisoftheinstances,asshowintheTable5,revealsthattheirusagefrequency
and distribution across the reviewed studies show a clear trend. The most utilized in-
stanceis[87], with5appearances(5.95%). Thisisfollowedby[88,89], eachwith4uses
(4.76%each).

Mathematics2025,13,1092
16of28
Table5.FrequencyandDistributionofLiteratureInstances.
| Instance | Frequency | Research         | UsagePercentage |      |
| -------- | --------- | ---------------- | --------------- | ---- |
| [87]     | 5         | [49,51,64,67,79] |                 | 5.95 |
| [88]     | 4         | [49,59,67,79]    |                 | 4.76 |
| [89]     | 4         | [49,51,65,79]    |                 | 4.76 |
| [15]     | 3         | [41,55,72]       |                 | 3.57 |
| [26]     | 2         | [48,80]          |                 | 2.38 |
| [90]     | 2         | [38,81]          |                 | 2.38 |
| [91]     | 2         | [38,81]          |                 | 2.38 |
| [92]     | 1         | [48]             |                 | 1.19 |
| [93]     | 1         | [51]             |                 | 1.19 |
| [94]     | 1         | [52]             |                 | 1.19 |
| [95]     | 1         | [65]             |                 | 1.19 |
| [96]     | 1         | [65]             |                 | 1.19 |
| [21]     | 1         | [41]             |                 | 1.19 |
| [37]     | 1         | [13]             |                 | 1.19 |
| [41]     | 1         | [19]             |                 | 1.19 |
| [97]     | 1         | [65]             |                 | 1.19 |
| [98]     | 1         | [52]             |                 | 1.19 |
| [99]     | 1         | [35]             |                 | 1.19 |
| [100]    | 1         | [81]             |                 | 1.19 |
| [33]     | 1         | [81]             |                 | 1.19 |
| [38]     | 1         | [81]             |                 | 1.19 |
| [101]    | 1         | [81]             |                 | 1.19 |
http://www.bernabe.
dorronsoro.es/vrp/
|     | 1   | [18] |     | 1.19 |
| --- | --- | ---- | --- | ---- |
(accessedon
24January2025)
http://prodhonc.free.fr/
Instances/instancesLRP2E_
|     | 1   | [12] |     | 1.19 |
| --- | --- | ---- | --- | ---- |
us.htm(accessedon
24January2025)
http://comopt.ifi.uni-
heidelberg.de/software/
|     | 1   | [18] |     | 1.19 |
| --- | --- | ---- | --- | ---- |
TSPLIB95/tsp/(accessed
on24January2025)
https://prolog.univie.ac.
at/research/TwoEVRP/
|     | 1   | [49] |     | 1.19 |
| --- | --- | ---- | --- | ---- |
(accessedon
24January2025)
Thesethreeinstancesaccountfor15.48%ofthetotal,makingthemthemostrepre-
sentative in the research field. A significant portion of the instances is used only once,
representing1.19%ofthetotalforeach. Thishighlightsahighdispersionintheselectionof
instancesandlowrepetitionacrossthestudies.

Mathematics2025,13,1092
17of28
Thisdistributionsuggeststhatwhilesomeinstancesstandoutasmorefrequentlyused,
theselectionofinstancesinthestudiesishighlydispersed. Thelowrepetitionindicatesa
lackofconsensuswithintheresearchcommunityonwhichinstancesarethemostrelevant
orrepresentative,whichcouldimpactthecomparabilityandreproducibilityofresultsin
thisfield.
3.2.2. AdaptedInstances
Theanalysisoftheinstances,asshowintheTable6,revealsadispersionintheirusage,
asmost(80%)areusedinonlyonestudy,representing1.19%each. Refs.[15,98]standout
withadaptationsinthreestudieseach(3.57%),while[87,102]appearintwostudies(2.38%).
Thesefourinstancesaccountforonly11.9%ofthetotal,reflectingtherelevanceof[98]and
theinterestin[15]asarecentinstance.
Table6.FrequencyandDistributionofAdaptedInstances.
| Instance | Frencuency | Research   | UsagePercentage |      |
| -------- | ---------- | ---------- | --------------- | ---- |
| [15]     | 3          | [55,58,75] |                 | 3.57 |
| [98]     | 3          | [34,83,84] |                 | 3.57 |
| [87]     | 2          | [42,67]    |                 | 2.38 |
| [102]    | 2          | [20,62]    |                 | 2.38 |
| [103]    | 1          | [71]       |                 | 1.19 |
| [104]    | 1          | [82]       |                 | 1.19 |
| [105]    | 1          | [20]       |                 | 1.19 |
| [106]    | 1          | [31]       |                 | 1.19 |
| [107]    | 1          | [47]       |                 | 1.19 |
| [108]    | 1          | [78]       |                 | 1.19 |
| [109]    | 1          | [69]       |                 | 1.19 |
| [36]     | 1          | [46]       |                 | 1.19 |
| [110]    | 1          | [57]       |                 | 1.19 |
| [111]    | 1          | [56]       |                 | 1.19 |
| [89]     | 1          | [58]       |                 | 1.19 |
| [112]    | 1          | [43]       |                 | 1.19 |
| [113]    | 1          | [53]       |                 | 1.19 |
| [99]     | 1          | [63]       |                 | 1.19 |
https://www.bernabe.
dorronsoro.es/vrp/
|     | 1   | [77] |     | 1.19 |
| --- | --- | ---- | --- | ---- |
(accessedon
24January2025)
http://vrp.galgos.inf.puc-
| rio.br/(accessedon | 1   | [68] |     | 1.19 |
| ------------------ | --- | ---- | --- | ---- |
24January2025)
Itisworthnotingthatinstance[87]isusedinsevenstudies,eitherinitsoriginalform
oradapted, followedbyinstance[15]withsixstudies,instance[89]withfiveuses,and
instances[88,98]withfoureach,representing10.45%,8.96%,7.46%,and5.97%,respectively,
ofthetotalinstancesreferencedintheseinvestigations(67).
Instance adaptations are made due to the lack of directly applicable test cases, re-
quiringtheadditionofparametersormodificationsbasedonthecontext. Forexample,

Mathematics2025,13,1092
18of28
ref.[34]baseditsexperimentsforthe2E-VRP-TMontheinstancesfrom[98],introducing
randommodificationstoparameterssuchastheloadcapacityofVUACs,UACs,andTW.
Additionally,randomchangesweremadetothedemandofVUACsandUACs,andthe
timewindows. Servicetimeswerealsoincluded.
3.2.3. CreatedInstances
AmongthecreatedinstancesasshowintheTable7,ref.[15]standsout,assinceits
creation,ithasbeenusedinfivedifferentstudies,bothastheoriginalinstancewithout
adaptation[41,55,72]andinadaptedversions[55,58,75]. Additionally,itisimportantto
notethatref.[55]uses[15]’sinstancesintheirexperiments,bothintheoriginalandadapted
forms. Now,withsevenoccurrences,ref.[87]becomesthemostfrequentlyusedinstance
(fiveoriginalandtwoadapted).
Table7.CreatedInstancesandYearofCreation.
| Instance | Year | Instance | Year |
| -------- | ---- | -------- | ---- |
| [15]     | 2019 | [66]     | 2021 |
| [17]     | 2019 | [44]     | 2022 |
| [42]     | 2019 | [60]     | 2022 |
| [54]     | 2019 | [70]     | 2022 |
| [61]     | 2019 | [73]     | 2022 |
| [22]     | 2020 | [19]     | 2023 |
| [76]     | 2020 | [32]     | 2023 |
| [85]     | 2020 | [40]     | 2023 |
| [14]     | 2021 | [74]     | 2023 |
| [16]     | 2021 |          |      |
3.2.4. AccessibilityofInstancesandTrendinVRPResearchwithSatellites
This section reveals that, among the instances presented in the research, various
difficultiesareobservedintheirarticles. Thefirstdifficultyarisesintheworksof[8,50],
whichdonotspecifywhethertheycreatedtheinstancesoriftheycomefromtheliterature.
Ontheotherhand,ref.[30]mentionsthattheirinstanceswerecreatedfromarealcasebut
donotprovidefurtherdetails. Refs.[61,66,70,76]indicatethattheirinstancesarecreated
butonly presentthe datasetparameters. Otherstudieswith difficulties include[44,77],
which provide access to their datasets but are inaccessible. Finally, ref. [74] falls into a
separatecategory,asaccesstothedatasetisonlypossiblethrougharequesttotheauthors.
RegardingthetrendofVRPinvestigationsthatusesatellites,theyhaveincreasedfrom
2019tothedateofinclusionofarticles,asshowninFigure4:

Mathematics 2025, 13, 1092 18 of 29
Table 7. Created Instances and Year of Creation.
Instance Year Instance Year
[15] 2019 [66] 2021
[17] 2019 [44] 2022
[42] 2019 [60] 2022
[54] 2019 [70] 2022
[61] 2019 [73] 2022
[22] 2020 [19] 2023
[76] 2020 [32] 2023
[85] 2020 [40] 2023
[14] 2021 [74] 2023
[16] 2021
3.2.4. Accessibility of Instances and Trend in VRP Research with Satellites
This section reveals that, among the instances presented in the research, various
difficulties are observed in their articles. The first difficulty arises in the works of [8,50],
which do not specify whether they created the instances or if they come from the
literature. On the other hand, ref. [30] mentions that their instances were created from a
real case but do not provide further details. Refs. [61,66,70,76] indicate that their instances
are created but only present the dataset parameters. Other studies with difficulties include
[44,77], which provide access to their datasets but are inaccessible. Finally, ref. [74] falls
into a separate category, as access to the dataset is only possible through a request to the
authors.
Mathematics2025,13,1092 Regarding the trend of VRP investigations that use satellites, they have increa1s9eodf 28
from 2019 to the date of inclusion of articles, as shown in Figure 4:
Mathematics 2025, 13, 1092 19 of 29
FFiigguurree 44.. VVRRPP aarrttiicclleess wwiitthh ssaatteelllliitteess uussee ppeerr yyeeaarr..
The analysis shows that the European Journal of Operational Research and
ComTpThuheete grgrsra a&pp hIhn sdshhuooswtwrsisa ala Eg gnrorgowinwieniengrgiin nignt etaerrerees stthti eni nmV VoRsRPt Pf(r Ve(eVqhueihecnilcetl -esR-oRouuoructietnisng, gwP iPrtohrob sblielxme am)r)tr iecrsleeessae aercarhcchhi .n -
vTionrlvavoninlsvpgionsrgat taestlailoittenel luiStsece ie,unasscee,e ,v aisTd reeanvncisdepdeonbrctyeadtai nobniyn cRarnees aeisnaecricrneha psuPeba rilnitc aBptiu,o bnalsnicdsat taiEortnxinps gesrittna rS2tiy0n2sgt2e .miAns l t2h0wo2iu2t.hg h
2AA02plt4phlsoihucaogtwhio s2na0s2 lh4oa wsvheeor fwcoousu ra na ltro,twiitcleiesrs p ceoraeucsnhut.m ,I tiet s dihsto hpuarletdst uhbimes nefiodgt uethdrea tthm tahatiy s2 0rfii sageru,trigceil vemse anbyet lhroianstegt, h tgoei vcdeuinfft- eotrhfefanfto t r
tjthohiuesr rcneuavtl-isoe, wffe afwcohra twshiiintsh rJ ueav nfireeew2q0u w2e4na.sc yin o Jfu onnee 2, 0w2h4i. ch are grouped in the “Other” category.
FFFiiiggguuurrreee 655 appnrraeelssyeeznnettsss taahnne adaninasatlyrliysbisusi stoiofo ntfh otehf desoidsltuirstitibrouinbt iumotneio tohnfo todhfse t u6hs2ee dp6 a2ipnp etrahspe s e6er2lse scseteleeldec ctaetcedcd opraadpcicenorgsr d. -
iTtnohg itstho celt ahcsersiitcfierrciitaaet.ri oiTan.h ipTsrh ocivslaicdslseaisfis scaianfit icooanvtie orpnvriopevwriod voeifsd teihnsesi inpgsrhietgd hiontmtioni nttoahnetth meapmapinaro inapcuphbuelbsic laaictpiaoptnliio ensdo sutooru cterhcsee s
cVcooRnntPtrr iwibbuiutthtiin nSgga ttteool lVVitReR PPU rtrieelssizeeaaatrriccohhn uu. ssiinngg ssaatteelllliitteess..
FFiigguurree 55.. DDiissttrriibbuuttiioonn ooff aannaallyyzzeedd ppaappeerrss bbyy jjoouurrnnaall..
TheanalysisshowsthattheEuropeanJournalofOperationalResearchandComputers
&IndustrialEngineeringarethemostfrequentsources,withsixarticleseach. Transporta-
tionScience,TransportationResearchPartB,andExpertSystemswithApplicationshave
fourarticleseach. Itshouldbenotedthat20articlesbelongtodifferentjournals,eachwith
afrequencyofone,whicharegroupedinthe“Other”category.
Figure6analyzesthedistributionofsolutionmethodsusedinthe62selectedpapers.
ThisclassificationprovidesanoverviewofthepredominantapproachesappliedtotheVRP
withSatelliteUtilization.
Figure 6. Distribution of solution methods in the selected papers.
The analysis of Figure 6 reveals that trajectory-based metaheuristics are the most
widely used approach, appearing in 31 articles, highlighting its effectiveness in solving
this type of problem. Exact methods are applied in 13 articles, demonstrating their
relevance despite their computational limitations for large-scale cases. Hybrid methods
are used in 8 articles, and heuristics appear in 5. Population-based metaheuristics are used
in 4 articles, showing a minor presence. Finally, matheuristic methods are the least
common, appearing in only one study.

Mathematics 2025, 13, 1092 19 of 29
The analysis shows that the European Journal of Operational Research and
Computers & Industrial Engineering are the most frequent sources, with six articles each.
Transportation Science, Transportation Research Part B, and Expert Systems with
Applications have four articles each. It should be noted that 20 articles belong to different
journals, each with a frequency of one, which are grouped in the “Other” category.
Figure 6 analyzes the distribution of solution methods used in the 62 selected papers.
This classification provides an overview of the predominant approaches applied to the
VRP with Satellite Utilization.
Mathematics2025,13,1092 20of28
Figure 5. Distribution of analyzed papers by journal.
FFiigguurree6 6.. DDiissttrriibbuuttiioonn ooffs soolluuttiioonnm meetthhooddssi innt thhees seelelecctteeddp paappeerrss..
TThhee aannaallyyssiiss ooff FFiigguurree 66 rreevveeaalsls ththaatt trtraajejeccttoorryy--bbaasseedd mmeettaahheeuurriissttiiccss aarree tthhee mmoosstt
wwidideelylyu usesdeda papprporaocahc,ha, pappepaerainrginign i3n1 3a1r taicrlteisc,lehsi,g hhilgighhltiginhgtiintsg eiftfse cetffiveecntievsesnienssso ilnv isnoglvthinisg
ttyhpise otyfpper oobfl epmr.oEblxeamct. mEextahcot dmseatrheoadpsp laireed ianpp13lieadrt iicnle s1,3d eamrtiocnlesst,r adtienmgotnhsetirrarteinlegv atnhceeir
dreeslepvitaentchee direcsopmitep uthtaetirio cnoamllpimutiatatitoionnasl fliomriltaartgioe-nssc afoler claasregse.-sHcaylber icdasmese.t hHoydbsraidre muestehdoidns
8aarert uicsleeds, iann 8d ahretiucrleisst,i casnadp hpeeuarrisintic5s. aPpoppeualra tiino n5.- bPaospeudlamtieotanh-beausreisdt imcseatraehueuserdistiincs4 aarret iuclseesd,
sihno w4 ianrgtiaclmesi,n oshropwreisnegn cae .mFiinnaolrly ,pmreastehnecuer.i sFtiicnamlleyt,h omdasthareeutrhisetilce amstectohmodmso anr,ea ptpheea rleinagst
icnoomnmlyoonn, eapstpuedayr.ing in only one study.
4. Discussion
Before starting this section, it is important to highlight that the limitations of this
studyareprimarilydefinedbytheexclusiveinclusionofpeer-reviewedpaperspublished
in English between 2019 and June 2024. While this ensures the review’s relevance, it
excludesresearchpublishedinotherlanguages. Additionally,thesearchwasrestricted
totheScopusandWebofSciencedatabases,leavingoutstudiesfromothersources,such
asdoctoraldissertations, duetothelackofopenaccess. Theselectionwasalsolimited
to research explicitly using the term “satellite” about a VRP variant, excluding studies
wheretheconceptwasappliedinadifferentcontext. Furthermore,studieswithoutfull
access, retracted papers, and those that did not employ quantitative decision-making
techniqueswereexcluded. Whiletheserestrictionswerenecessarytomaintainconsistency
andobjectivityinthereview,theymayhavelimitedtheinclusionofalternativeapproaches
andgrayliteratureintheanalysisofsatellite-basedVRP.
TheTable3analysisallowsustoestablishthatIntermediateDepotsutilizetheconcept
ofsatellitesthemost,especiallyexploringthevariantPathSplitting,with35studiesassoci-
atedwithit. Notably,amongthe12studiesclassifiedundertheTimeConstraintsvariant
in “Intermediate Facilities or Depots”, all are also categorized under the Path-Splitting
variant. Specifically,moststudiesonIntermediateDepotsexplorePathSplittingandTime
Constraints. Atthesametime,variantssuchasTemporalSynchronization,Multi-Trip,and
RandomDemandInformationhavesignificantresearchpotentialduetothelimitednumber
ofstudiesaddressingthem. Thisisimportantforlastmilelogisticscompanies,asmany
mustconsiderdemandrandomnessandresourceefficiency. Therefore,synchronizationin
multipletripsrepresentsarealandrelevantapplication. Ontheotherhand,theuseofTem-
poralSynchronization,Multi-Trip,orRandomDemandInformationrepresentsresearch
topicswithsignificantpotentialfordevelopment,giventhelimitednumberofarticlesthat

Mathematics2025,13,1092 21of28
explorethesevariantsincombinationwithIntermediateFacilities. Thesestudiesapply
toloadtransfersystemswithtimeconstraints,wherevehiclesmustmakemultipletrips
tocustomersduetotheirlimitedcapacity. Additionally,demanduncertaintymakesthe
problemhighlyrealisticandrelevantforlastmiledeliverycompanies.
Anotherfuturechallengefacingoptimizationsolutionmethodsisintegratingmachine
learningandlinearprogramming-basedalgorithmsthatcanrunefficientlyonGPUsfor
high-performancecomputing(HPC).Inaddition,incorporatingheuristics,particularlyin
mathematics(matheuristics),couldimprovesolutionapproaches. Theuseofpopulation-
based metaheuristics for VRP with satellites has been scarcely studied, as indicated in
Figure6,whereafutureresearchdirectionistoadaptalgorithmsforotherVRPvariants,
suchas[114,115]. Developingandimplementingthesetechniquesshouldbeconsideredas
futureworktoimprovetheefficiencyandscalabilityofoptimizationmodels.
InthecaseofCross-Docking,studiespredominantlyfocusonfixedtransferpoints
combinedwiththePath-Splittingvariantfromthedepottothecustomer. Theimplementa-
tionofTimeConstraintsandsynchronizationfurthersupportsthis. Researchopportunities
inthisareaarisearoundtheMulti-Tripvariantandtheincorporationofdynamicinforma-
tion,whichcouldbeenhancedbyaddingcomponentslikePickupandDelivery,Clustering,
orElectromobility. FurtherresearchisneededonVRPwithsatelliteutilizationforcross-
docking to reload vehicles in routes, avoiding their return to the central depot. This is
particularlyrelevantformobilecross-docking,wheretheLocationvariantcouldbefurther
developed. Thus,theresultsindicatethatspecificcombinationsofMulti-Trip,Clustering,
PickupandDelivery,andElectromobilityshouldbeexploredinCross-DockingandSatellite
Depots,inadditiontoimprovingtheclassificationanddefinitionoftheterm“satellite”in
thecontextofVRP.Theseopportunitiespresentanexcellentchancetoexpandresearchin
thisfield,applyingthesesolutionstoproductionorlocationdecisionsandotherunexplored
variants. Theaboveappliestoproblemsinvolvingvehicleswithloworlimitedcapacity,
optimizingdeliverytimes, andaddressinglatewarehousedeparturesduetoinventory
shortages,makingitparticularlyrelevantforcompanieswithinthesupplychain.
RegardingSatelliteDepots,thiscategoryisdominatedbytheTrailerTransfervariant,
whichiscomplementedbytheuseofElectromobilityandtheintegrationofTimeWindows.
Additionally,twostudieshavebeenidentified,focusingonPathSplittingwithsynchroniza-
tionandTimeConstraintsorDeliveryOptions. Researchopportunitiesinthisareainclude
exploring Multi-Trips, different depot types, demand characteristics, Delivery Options,
andClustering.
TheuseofSatelliteCustomersappearsintwostudies,focusingonusingTimeCon-
straints and Electromobility. This highlights a lack of research on leveraging customer
locationsasdeliveryoptionsandoptimizingprocessingtimes. Itshouldbenotedthata
SatelliteCustomercanbeserved. Atthesametime,theprimaryvehicleactseitherthrough
an alternative of transport or by a person, such as visiting a customer “on foot” while
the vehicle is recharging. This raises the question: How can using Satellite Customers
asdeliveryandprocessingpointsbeoptimized? Expandingresearchinthisareacould
improvedistributionefficiencybyintegratingcustomerproximityintoroutingdecisions
andrefiningtimemanagementstrategies.
PathLevelplaysacrucialroleinthiscontextbyallowingbetterdistributionofcargo
flowthroughmulti-leveloperations,facilitatinglastmilemanagement,andenablingaccess
tocustomerswithvehiclerestrictions,particularlyforheavyvehicles. Similarly,Location
optimizesthestrategicdistributionofdepots,reducinglong-termlogisticscostsanden-
hancingdistributionnetworkefficiency,especiallyforexpandingcompanies. However,
itsimplementationrequiresahighinitialinvestmentininfrastructure,whichmaylimit
itsadoption.

Mathematics2025,13,1092 22of28
TrailerTransferenhancesdistributionflexibilityandimprovesvehiclecapacityman-
agementinlong-distanceoperationsorwhencargotransfersbetweentrucksarenecessary.
Itsmainlimitationistheneedforspecifictransferpoints. Electromobilityisappliedin
urbanenvironmentswithenvironmentalrestrictionsandsustainabilitystrategies,allowing
electricvehiclestoreduceemissionsandfuelcosts. However,itsfeasibilitydependson
thesevehicles’autonomyandcharginginfrastructureavailability.
ThecombinationofTemporalSynchronizationandTimeConstraintsisusedinsys-
temswithmultipletransshipmentpointsorwherevehiclesdependonspecificarrivaltimes,
improvingcoordinationandreducingwaitingtimes. However,itrequirespreciseman-
agementofschedulesandresources. Multi-Tripallowsvehiclestobereusedformultiple
dailytrips,increasingefficiencyandreducingoperationalcosts. Itisparticularlyuseful
insystemswhereloadingandunloadingarequickandthetripsbetweencustomersand
satellitesareshort.
Multi-depotsprovidegreaterflexibilityindistributionandreducedeliverytimes,mak-
ingthemidealforlarge-scaledistributionnetworksormarketswithhigh,geographically
disperseddemand. ThePickupandDeliverymodeloptimizesvehicleusebyminimizing
emptytrips,asthesametransportcanperformbothdeliveriesandcollections. However,
thismayincreaseservicetimes.
RandomDemandsareusefulinmarketswithhighvolatilitysincetheyallowplanning
tobeadjustedtodynamicandmorerealisticscenarios. However,thisvariantincreases
planning complexity. Finally, Delivery Options enable flexible distribution, improving
customercoverageinhard-to-reachorgeographicallydispersedareas. However,hybrid
deliverymethods,suchaslockersorotherintermediatepoints,maynotalwaysbefeasible
duetologisticalandinfrastructurelimitations.
The selection of satellite locations, routing, and vehicle types in a Vehicle-Routing
ProblemwithSatellitesUtilizationisprimarilyinfluencedbydistance-relatedcosts,rep-
resentingthemostsignificantfactor. Fixedcostsassociatedwithvehiclesandroutesalso
playacrucialrole,impactingtheoveralloperationalbudget. Waitingtimesintransitand
atservicepointsfurtheraffectschedulingefficiencyandmayleadtoadditionalpenalties.
Handlingcosts,includingloadingandunloadingoperations,areanotherkeyconsideration,
astheyinfluenceoverallservicetimeandresourceallocation. Lastly,fuelconsumption
andemissionscostsareessentialfactors,especiallyinsustainability-focusedlogistics,as
theydirectlyimpactbothoperationalexpensesandenvironmentalimpact. Theseelements
collectivelyshapetheefficiencyandprofitabilityofthesystem,emphasizingtheneedfor
strategicplanninginthedistributionnetwork.
Anotheraspecttoconsiderisusingsolutionmethods,wheremetaheuristicspredomi-
nate,appliedtoinstancesrangingfrom27to1008customers. Ontheotherhand,hybrid
methodssolveinstancesfrom26upto90,627customers(realcase). Regardingexactmeth-
ods,instancesrangebetween20and300customers. Whencalculatingtheaverages,exact
methodssolveanaverageof110points,metaheuristics220,andhybrids,excludingthe
extremecaseof90,627customers,achieveanaverageof77.Thisfactindicatesthatalthough
metaheuristicsandhybridalgorithmscanhandlelargerinstances,theaverageinstance
sizedifferenceisinsignificant. Thus,itisevidentthatlarge-scalereal-worldcases(over
1000customers)arerelativelyrare. Thisobservationraisesthequestion: Howdoesusing
apublicoropendatasetaffectcomparingsolutionmethods? Thisfactmayresultfrom
thelowstandardizationofinstances,asobservedintheresults,wherealargepercentage
consistsofadaptedornewlycreatedinstances.
Regardingtheimpactofnewtechnologies,ref.[18]pointsoutthatthetransportation
sectorisundergoingatransformationdrivenbythedevelopmentoftheInternetofThings
(IoT),Blockchain,andothertechnologies. IoTfacilitatesmassivedatacollection,which

Mathematics2025,13,1092 23of28
mustbeproperlystoredandsecured,makingblockchaindevelopmentessential. Subse-
quently,advancedartificialintelligence(AI)techniquescananalyzethislargevolumeof
data,generatingmorepreciseparametersandoptimizationalgorithms,andimprovingthe
qualityofsolutions. Theabilitytocollectdataonline,processitefficiently,andexecuteop-
timizationalgorithmsinrealtimeenhancesdecision-makingandoperationalperformance.
The previous analysis was conducted based on the methods reported by the au-
thors. However,manystudiesemployedmorethanonemetaheuristicoracombination
oftechniques. Accordingto[116],hybridmetaheuristicsintegratemultiplealgorithmic
components,oftenderivedfromoptimizationalgorithmsinotherresearchareas. Therefore,
thesolutionmethodmaynothavebeenaccuratelyclassifiedunderthisdefinition.
Finally, itcanbestatedthattheterm“satellite”intheVRPcanadoptvariousdefi-
nitions, primarily depending on the problem being addressed. This term also presents
challengesinnarrowingthescopeofsearches,asitisassociatedwithotherfields,suchas
satellitenetworksinlowEarthorbits. Additionally,theuseofthiskeywordcomplicates
classificationefforts,asnotallarticlesclearlydefinefromtheoutsetwhetherthesesatellites
havestoragecapacity,whichwouldcategorizethemasintermediatedepotsorfacilitiesor
lacksuchcapacity,therebydefiningthemascross-dockingpoints.
Accordingtothereviewedarticlesandthemostcommonlyutilizedcharacteristics,
theterm“satellite”issuggestedtobedefined,inthecontextofVRP,asanintermediate
physical point used in distribution systems, facilitating the connection between one or
morecentraldepotsandcustomersforthetransferofproductsbetweendifferentmeansof
transport. Satellitesmayhavetemporarystoragecapacityandcanbeestablishedasfixed
ormobilesites,dependingonthesystem’soperationalrequirements.
5. Conclusions
Basedontheclassificationresultsconductedinthisstudy,itcanbeconcludedthat
thekeyword“satellite”notonlyrepresentsaspecificlogisticalelementbutalsoencom-
passesasetofapproachesandvariantsfundamentaltosolvingcontemporarylogistical
challenges. Itsapplicationadaptstodiversecontextsandneeds,demonstratingaflexibility
that positions it as a key concept for advancing the optimization of supply chains and
urbanlogistics.
Additionally,theresearchanalysisonVRPusingsatellitesbetween2019andJune2024
revealsagrowingacademicinterest,asevidencedbyasteadyincreaseinpublicationsin
recentyears. Oneofthemostsignificantfindingsofthisstudyisthediversityofinstances
usedintheanalyzedworks,withmorethan40%beingcreatedoradapted. Thisaspect
highlights the complexity of this type of study. It suggests a lack of standardization in
datasetusage, which,inturn,presentsanopportunitytoestablishcommonlyaccepted
referencedatabases. Multipleinstancesutilizedintheliteratureindicateastrongpoten-
tial for future research to rely on standardized databases, allowing for more consistent
comparisonsandimprovedreproducibilityofresults,therebystrengtheningthescientific
foundationofVRPresearchinvolvingsatellites.
Regardingresearchopportunities,theanalysishighlightsseveralareaswithlittletono
exploration.Specifically,inthecategoryofIntermediateDepots,theleastdevelopedaspects
includeTemporalSynchronization,whichcouldenhancecoordinationbetweenvehicles
and depots; the Multi-Trip strategy, which optimizes vehicle usage through multiple
deliveryrounds;andtheconsiderationofRandomDemand,whichintroducesstochastic
elementstocreatemorerealisticscenarios.
Research opportunities exist in strategies such as Multi-Trip, Pickup and Delivery,
Clustering,andElectromobilityforcross-docking. Furthermore,inthecaseofmobilecross-
docking,studyingsynchronizationalongsidetheintegrationofdynamicinformationand

Mathematics2025,13,1092 24of28
stochasticmodelswouldenablethedevelopmentofreoptimizationapproachestoenhance
lastmilelogisticsefficiency. Incorporatingthesefactorscouldimprovetheadaptabilityand
efficiencyofcross-dockingoperations,particularlyinenvironmentswhereflexibilityisa
crucialelement.
Incontrast,theSatelliteDepotsandSatelliteCustomerscategoriesexhibitparticular
characteristics,whichcouldhindertheiralignmentwithastandardizeddefinitionofthe
term “satellite” in VRP research. Nevertheless, their application in logistics optimiza-
tionissignificant,suggestingtheymayrequireadistinctclassificationtohighlighttheir
importanceintheliterature.
Thisstudyunderscorestheneedtoaddresstheseresearchgapstoencouragefurther
explorationofthe underrepresented aspectsofsatelliteusage inVRPs. Additionally, it
emphasizes the importance of promoting standardization in dataset usage to facilitate
researchdevelopmentanditsapplicationinlastmilelogistics.
AuthorContributions:Conceptualization,R.S.-C.,J.W.E.,D.M.-T.andR.L.;methodology,J.W.E.and
R.L.;software,R.S.-C.;validation,J.W.E.,D.M.-T.andR.L.;formalanalysis,R.S.-C.;investigation,
R.S.-C.;resources,J.W.E.andR.L.;datacuration,R.S.-C.;writing—originaldraftpreparation,R.S.-C.;
writing—reviewandediting,R.S.-C.,J.W.E.,D.M.-T.andR.L.;visualization,R.S.-C.;supervision,
D.M.-T.;projectadministration,R.L.;fundingacquisition,J.W.E.andR.L.Allauthorshavereadand
agreedtothepublishedversionofthemanuscript.
Funding:ProjectsUniversityofBío-Bío—UBIOBIOGI2380142,andFondoNacionaldeDesarrollo
CientíficoyTecnológico—ANIDFONDECYTREGULAR1230125.
Data Availability Statement: For specific classification data, please contact the corresponding
authordirectly.
Acknowledgments: PhD Scholarship, Universidad del Bío-Bío, Chile; Scholarship Alianza del
Pacífico;OperationsModelingandManagementResearchGroup(MGO),PontificiaUniversidad
JaverianaCali,Colombia.
ConflictsofInterest:Theauthorsdeclarenoconflictsofinterest.
References
1. Mardešic´,N.;Erdelic´,T.;Caric´,T.;Ðurasevic´,M.ReviewofStochasticDynamicVehicleRoutingintheEvolvingUrbanLogistics
Environment.Mathematics2024,12,28.[CrossRef]
2. Boysen,N.;Fedtke,S.;Schwerdfeger,S.Last-MileDeliveryConcepts:ASurveyfromanOperationalResearchPerspective;Springer:
Berlin/Heidelberg,Germany,2021;Volume43,ISBN0123456789.
3. Toth,P.;Vigo,D.VehicleRouting,Problems,Methods,andApplications;SIAM:Philadelphia,PA,USA,2014;ISBN9781611973587.
4. Dantzig,G.B.;Ramser,J.H.Thetruckdispatchingproblem.Encycl.Oper.Res.Manag.Sci.1959,6,80–91.[CrossRef]
5. Toth,P.;Vigo,D.TheVehicleRoutingProblem;SIAM:Philadelphia,PA,USA,2002;ISBN0898715792.
6. Mor,A.;Speranza,M.G.Vehicleroutingproblemsovertime:Asurvey.Ann.Oper.Res.2022,314,255–275.[CrossRef]
7. Ulmer,M.W.Anticipationversusreactivereoptimizationfordynamicvehicleroutingwithstochasticrequests.Networks2019,73,
277–291.[CrossRef]
8. Zuhanda,M.K.;Suwilo,S.;Sitompul,O.S.;Mardiningsih;Caraka,R.E.;Kim,Y.;Noh,M.OptimizationofVehicleRoutingProblem
intheContextofE-commerceLogisticsDistribution.Eng.Lett.2023,31,279–286.
9. Chopra,S.;Meindl,P.SupplyChainManagement: Strategy,Planning,andOperation;Pearson: NewYork,NY,USA,2016;ISBN
9780133800203.
10. Lo,S.C.;Chuang,Y.L.VehicleRoutingOptimizationwithCross-DockingBasedonanArtificialImmuneSysteminLogistics
Management.Mathematics2023,11,811.[CrossRef]
11. Neghabadi,P.D.;Samuel,K.E.;Espinouse,M.L.Systematicliteraturereviewoncitylogistics:Overview,classificationandanalysis.
Int.J.Prod.Res.2019,57,865–887.[CrossRef]
12. Sutrisno,H.;Yang,C.L.Atwo-echelonlocationroutingproblemwithmobilesatellitesforlast-miledelivery: Mathematical
formulationandclustering-basedheuristicmethod.Ann.Oper.Res.2023,323,203–228.[CrossRef]

Mathematics2025,13,1092 25of28
13. Enthoven,D.L.J.U.;Jargalsaikhan,B.;Roodbergen,K.J.;uithetBroek,M.A.J.;Schrotenboer,A.H.Thetwo-echelonvehiclerouting
problemwithcoveringoptions:Citylogisticswithcargobikesandparcellockers.Comput.Oper.Res.2020,118,104919.[CrossRef]
14. Li,H.;Wang,H.;Chen,J.;Bai,M.Two-echelonvehicleroutingproblemwithsatellitebi-synchronization.Eur.J.Oper.Res.2021,
288,775–793.[CrossRef]
15. Dellaert,N.;Saridarq,F.D.;VanWoensel,T.;Crainic,T.G.Branch-and-price-basedalgorithmsforthetwo-echelonvehiclerouting
problemwithtimewindows.Transp.Sci.2019,53,463–479.[CrossRef]
16. Mühlbauer,F.;Fontaine,P.Aparallelisedlargeneighbourhoodsearchheuristicfortheasymmetrictwo-echelonvehiclerouting
problemwithswapcontainersforcargo-bicycles.Eur.J.Oper.Res.2021,289,742–757.[CrossRef]
17. He,P.;Li,J.Thetwo-echelonmulti-tripvehicleroutingproblemwithdynamicsatellitesforcropharvestingandtransportation.
Appl.SoftComput.J.2019,77,387–398.[CrossRef]
18. Xue,G.;Wang,Y.;Guan,X.;Wang,Z.AcombinedGA-TSalgorithmfortwo-echelondynamicvehicleroutingwithproactive
satellitestations.Comput.Ind.Eng.2022,164,107899.[CrossRef]
19. Dumez,D.;Tilk,C.;Irnich,S.;Lehuédé,F.;Olkis,K.;Péton,O.Amatheuristicfora2-echelonvehicleroutingproblemwith
capacitatedsatellitesandreverseflows.Eur.J.Oper.Res.2023,305,64–84.[CrossRef]
20. Wu,Z.;Zhang,J.Abranch-and-pricealgorithmfortwo-echelonelectricvehicleroutingproblem.ComplexIntell.Syst.2023,9,
2475–2490.[CrossRef]
21. Grangier,P.;Gendreau,M.;Lehuédé,F.;Rousseau,L.M.Anadaptivelargeneighborhoodsearchforthetwo-echelonmultiple-trip
vehicleroutingproblemwithsatellitesynchronization.Eur.J.Oper.Res.2016,254,80–91.[CrossRef]
22. Li,H.;Liu,Y.;Chen,K.;Lin,Q.Thetwo-echeloncitylogisticssystemwithon-streetsatellites.Comput.Ind.Eng.2020,139,105577.
[CrossRef]
23. Yuan,P.;Wang,Y.;Su,M.;Yang,Z.;Zhang,Q.Markovdecisionprocess-basedroutingalgorithminhybridSatellites/UAVs
disruption-tolerantsensingnetworks.IETCommun.2019,13,1415–1424.[CrossRef]
24. Deng,X.;Zeng,S.;Chang,L.;Wang,Y.;Wu,X.;Liang,J.;Ou,J.;Fan,C.AnAntColonyOptimization-BasedRoutingAlgorithm
forLoadBalancinginLEOSatelliteNetworks.Wirel.Commun.Mob.Comput.2022,2022,3032997.[CrossRef]
25. Barkaoui,M.;Berger,J.Anewhybridgeneticalgorithmforthecollectionschedulingproblemforasatelliteconstellation.J.Oper.
Res.Soc.2020,71,1390–1410.[CrossRef]
26. Sluijk,N.;Florio,A.M.;Kinable,J.;Dellaert,N.;VanWoensel,T.Two-echelonvehicleroutingproblems:Aliteraturereview.Eur.J.
Oper.Res.2023,304,865–886.[CrossRef]
27. Li,H.;Chen,J.;Wang,F.;Bai,M.Ground-vehicleandunmanned-aerial-vehicleroutingproblemsfromtwo-echelonscheme
perspective:Areview.Eur.J.Oper.Res.2021,294,1078–1095.[CrossRef]
28. Page,M.J.; McKenzie,J.E.; Bossuyt,P.M.; Boutron,I.; Hoffmann,T.C.; Mulrow,C.D.; Shamseer,L.; Tetzlaff,J.M.; Akl,E.A.;
Brennan,S.E.;etal.ThePRISMA2020statement:Anupdatedguidelineforreportingsystematicreviews.BMJ2021,372,n71.
[CrossRef]
29. Mena-Reyes,J.F.;Vergara,F.;Linfati,R.;Escobar,J.W.QuantitativeTechniquesforSustainableDecisionMakinginForest-to-
LumberSupplyChain:ASystematicReview.Forests2024,15,297.[CrossRef]
30. SinaMohri,S.;Mohammadi,M.;VanWoensel,T.Designingzero-emissionscontainerizedlast-miledeliverysystems: Acase
studyformelbourne.Transp.Res.PartCEmerg.Technol.2024,159,104492.[CrossRef]
31. Bevilaqua,A.;Bevilaqua,D.;Yamanaka,K.ParallelislandbasedMemeticAlgorithmwithLin–Kernighanlocalsearchfora
real-lifeTwo-EchelonHeterogeneousVehicleRoutingProblembasedonBrazilianwholesalecompanies.Appl.SoftComput.J.
2019,76,697–711.[CrossRef]
32. Bayliss,C.;Bektas¸,T.;Tjon-Soei-Len,V.;Rohner,R.Designingamulti-modalandvariable-echelondeliverysystemforlast-mile
logistics.Eur.J.Oper.Res.2023,307,645–662.[CrossRef]
33. Villegas,J.G.;Prins,C.;Prodhon,C.;Medaglia,A.L.;Velasco,N.GRASP/VNDandmulti-startevolutionarylocalsearchforthe
singletruckandtrailerroutingproblemwithsatellitedepots.Eng.Appl.Artif.Intell.2010,23,780–794.[CrossRef]
34. Li,H.;Wang,H.;Chen,J.;Bai,M.Two-echelonvehicleroutingproblemwithtimewindowsandmobilesatellites.Transp.Res.
PartBMethodol.2020,138,179–201.[CrossRef]
35. Cortés-Murcia,D.L.;Prodhon,C.;MuratAfsar,H.Theelectricvehicleroutingproblemwithtimewindows,partialrechargesand
satellitecustomers.Transp.Res.PartELogist.Transp.Rev.2019,130,184–206.[CrossRef]
36. Zhou,L.;Baldacci,R.;Vigo,D.;Wang,X.AMulti-DepotTwo-EchelonVehicleRoutingProblemwithDeliveryOptionsArisingin
theLastMileDistribution.Eur.J.Oper.Res.2018,265,765–778.[CrossRef]
37. Veenstra,M.;Roodbergen,K.J.;Coelho,L.C.;Zhu,S.X.Asimultaneousfacilitylocationandvehicleroutingproblemarisingin
healthcarelogisticsintheNetherlands.Eur.J.Oper.Res.2018,268,703–715.[CrossRef]
38. Bartolini,E.;Schneider,M.Atwo-commodityflowformulationforthecapacitatedtruck-and-trailerroutingproblem.Discret.
Appl.Math.2020,275,3–18.[CrossRef]

Mathematics2025,13,1092 26of28
39. Ren,X.;Zhang,H.;Hu,R.;Qiu,Y.Locationofelectricvehiclechargingstations:Aperspectiveusingthegreydecision-making
model.Energy2019,173,548–553.[CrossRef]
40. Jia,S.;Deng,L.;Zhao,Q.;Chen,Y.anAdaptiveLargeNeighborhoodSearchHeuristicforMulti-CommodityTwo-EchelonVehicle
RoutingProblemWithSatelliteSynchronization.J.Ind.Manag.Optim.2023,19,1187–1210.[CrossRef]
41. Marques,G.;Sadykov,R.;Deschamps,J.-C.Abranch-cut-and-priceapproachforthesingle-tripandmulti-triptwo-echelon
vehicleroutingproblemwithtimewindows.Transp.Sci.2022,56,1598–1617.[CrossRef]
42. Kancharla,S.R.;Ramadurai,G.Multi-depotTwo-EchelonFuelMinimizingRoutingProblemwithHeterogeneousFleets:Model
andHeuristic.Netw.Spat.Econ.2019,19,969–1005.[CrossRef]
43. Li,J.;Xu,M.;Sun,P.Two-echeloncapacitatedvehicleroutingproblemwithgroupingconstraintsandsimultaneouspickupand
delivery.Transp.Res.PartBMethodol.2022,162,261–291.[CrossRef]
44. Zhang,M.;Xiong,G.;Bao,S.;Meng,C.ATime-DivisionDistributionStrategyfortheTwo-EchelonVehicleRoutingProblemWith
DemandBlowout.J.Ind.Manag.Optim.2022,18,2847–2872.[CrossRef]
45. Li,H.;Zhang,L.;Lv,T.;Chang,X.Thetwo-echelontime-constrainedvehicleroutingprobleminlinehaul-deliverysystems.
Transp.Res.PartBMethodol.2016,94,169–188.[CrossRef]
46. Yu,V.F.;Lin,S.W.;Zhou,L.;Baldacci,R.Afastsimulatedannealingheuristicforthemulti-depottwo-echelonvehiclerouting
problemwithdeliveryoptions.Transp.Lett.2024,16,921–932.[CrossRef]
47. Marques, G.; Sadykov, R.; Deschamps, J.C.; Dupas, R. An improved branch-cut-and-price algorithm for the two-echelon
capacitatedvehicleroutingproblem.Comput.Oper.Res.2020,114,104833.[CrossRef]
48. Guimarães,J.C.F.;daCunha,C.B.Math-HeuristicfortheCapacitatedTwo-EchelonVehicleRoutingProblem.Pesqui.Operacional
2023,43,e270829.[CrossRef]
49. Huang,H.;Yang,S.;Li,X.;Hao,Z.AnEmbeddedHamiltonianGraph-GuidedHeuristicAlgorithmforTwo-EchelonVehicle
RoutingProblem.IEEETrans.Cybern.2022,52,5695–5707.[CrossRef]
50. Zuhanda,M.K.;Suwilo,S.;Sitompul,O.S.;Mardiningsih.ACombinationK-MeansClusteringand2-OptAlgorithmforSolving
theTwoEchelonE-CommerceLogisticDistribution.Logforum2022,18,213–225.[CrossRef]
51. Yu,V.F.;Nguyen,M.P.K.;Putra,K.;Gunawan,A.;Dharma,I.G.B.B.TheTwo-EchelonVehicleRoutingProblemwithTransshipment
Nodes and Occasional Drivers: Formulation and Adaptive Large Neighborhood Search Heuristic. J. Adv. Transp. 2022,
2022,5603956.[CrossRef]
52. Wang,Y.;Wang,X.;Fan,J.;Wang,Z.;Zhen,L.Emergencylogisticsnetworkoptimizationwithtimewindowassignment.Expert
Syst.Appl.2023,214,119145.[CrossRef]
53. Jiang,D.;Li,X.Orderfulfilmentproblemwithtimewindowsandsynchronisationarisingintheonlineretailing.Int.J.Prod.Res.
2021,59,1187–1215.[CrossRef]
54. Li,H.;Bai,M.;Zhao,Y.;Dai,C.Vehicleflowformulationfortwo-echelontime-constrainedvehicleroutingproblem.J.Manag.Sci.
Eng.2019,4,75–90.[CrossRef]
55. Zhou,S.;Zhang,D.;Ji,B.;Li,S.Two-echelonvehicleroutingproblemwithdirectdeliveriesandaccesstimewindows.ExpertSyst.
Appl.2024,244,121150.[CrossRef]
56. Liu,R.;Jiang,S.Avariableneighborhoodsearchalgorithmwithconstraintrelaxationforthetwo-echelonvehicleroutingproblem
withsimultaneousdeliveryandpickupdemands.SoftComput.2022,26,8879–8896.[CrossRef]
57. Li,Q.;Wang,Y.;Xiong,Y.;Zhang,S.;Zhou,Y.Machinelearning-basedoptimisationinatwo-echelonlogisticsnetworkforthedry
portoperationinChina.Int.J.Syst.Sci.Oper.Logist.2023,10,2252321.[CrossRef]
58. Zhou,H.;Qin,H.;Zhang,Z.;Li,J.Two-echelonvehicleroutingproblemwithtimewindowsandsimultaneouspickupand
delivery.SoftComput.2022,26,3345–3360.[CrossRef]
59. Paul,A.;Kumar,R.S.;Rout,C.;Goswami,A.Abi-objectivetwo-echelonpollutionroutingproblemwithsimultaneouspickup
anddeliveryundermultipletimewindowsconstraint.Opsearch2021,58,962–993.[CrossRef]
60. Lv, C.; Zhang, C.; Lian, K.; Ren, Y.; Meng, L. A two-echelon fuzzy clustering based heuristic for large-scale bike sharing
repositioningproblem.Transp.Res.PartBMethodol.2022,160,54–75.[CrossRef]
61. Agárdi,A.;Kovács,L.;Bányai,T.Two-EchelonVehicleRoutingProblemwithRechargeStations.Transp.Telecommun.2019,20,
305–317.[CrossRef]
62. Wang,D.;Zhou,H.Atwo-echelonelectricvehicleroutingproblemwithtimewindowsandbatteryswappingstations.Appl.Sci.
2021,11,10779.[CrossRef]
63. Akbay,M.A.;Kalayci,C.B.;Blum,C.;Polat,O.VariableNeighborhoodSearchfortheTwo-EchelonElectricVehicleRouting
ProblemwithTimeWindows.Appl.Sci.2022,12,1014.[CrossRef]
64. Ramírez-Villamil,A.;Montoya-Torres,J.R.;Jaegler,A.;Cuevas-Torres,J.M.Reconfigurationoflast-milesupplychainforparcel
deliveryusingmachinelearningandroutingoptimization.Comput.Ind.Eng.2023,184,109604.[CrossRef]
65. Yu,V.F.;Jodiawan,P.;Schrotenboer,A.H.;Hou,M.L.Thetwo-echelonvehicleroutingproblemwithtimewindows,intermediate
facilities,andoccasionaldrivers.ExpertSyst.Appl.2023,234,120945.[CrossRef]

Mathematics2025,13,1092 27of28
66. Liu,D.;Deng,Z.;Zhang,W.;Wang,Y.;Kaisar,E.I.Designofsustainableurbanelectronicgrocerydistributionnetwork.Alex.Eng.
J.2021,60,145–157.[CrossRef]
67. Liu, D.; Liu, D.; Deng, Z.; Mao, X.; Yang, Y.; Yang, Y.; Kaisar, E.I. Two-Echelon Vehicle-Routing Problem: Optimization of
AutonomousDeliveryVehicle-AssistedE-GroceryDistribution.IEEEAccess2020,8,108705–108719.[CrossRef]
68. Tian, X.D.; Hu, Z.H.Abranch-and-pricemethodforatwo-echelonlocationroutingproblemwithrecommendedsatellites.
Comput.Ind.Eng.2023,184,109593.[CrossRef]
69. Yıldız,E.A.;Karaog˘lan,I˙.;Altiparmak,F.AnexactalgorithmforTwo-EchelonLocation-Routingproblemwithsimultaneous
pickupanddelivery.ExpertSyst.Appl.2023,231,120598.[CrossRef]
70. Ramirez-Villamil,A.;Jaegler,A.;Montoya-Torres,J.R.Sustainablelocalpickupanddelivery:ThecaseofParis.Res.Transp.Bus.
Manag.2022,45,100692.[CrossRef]
71. Qiu,Y.;Zhou,D.;Du,Y.;Liu,J.;Pardalos,P.M.;Qiao,J.Thetwo-echelonproductionroutingproblemwithcross-dockingsatellites.
Transp.Res.PartELogist.Transp.Rev.2021,147,102210.[CrossRef]
72. Mhamedi,T.;Andersson,H.;Cherkesly,M.;Desaulniers,G.ABranch-Price-and-CutAlgorithmfortheTwo-EchelonVehicle
RoutingProblemwithTimeWindows.Transp.Sci.2022,56,245–264.[CrossRef]
73. Schmidt,J.;Tilk,C.;Irnich,S.Usingpublictransportina2-echelonlast-miledeliverynetwork. Eur. J.Oper. Res. 2022,317,
827–840.[CrossRef]
74. Agnimo,V.;Ouhimmou,M.;Paquet,M.;Montecinos,J.Integratedstrategicandtacticaldesignofmulti-echeloncitydistribution
systemswithvehiclessynchronization:AcaseoftheGreaterMontréalarea.Comput.Ind.Eng.2023,183,109458.[CrossRef]
75. Escobar-Vargas,D.;Crainic,T.G.Multi-attributetwo-echelonlocationrouting:Formulationanddynamicdiscretizationdiscovery
approach.Eur.J.Oper.Res.2024,314,66–78.[CrossRef]
76. Groß,P.O.;Ehmke,J.F.;Mattfeld,D.C.Intervaltraveltimesforrobustsynchronizationincitylogisticsvehiclerouting.Transp.Res.
PartELogist.Transp.Rev.2020,143,102058.[CrossRef]
77. Lan,Y.L.;Liu,F.;Ng,W.W.Y.;Gui,M.;Lai,C.Multi-ObjectiveTwo-EchelonCityDispatchingProblemWithMobileSatellitesand
Crowd-Shipping.IEEETrans.Intell.Transp.Syst.2022,23,15340–15353.[CrossRef]
78. Lan,Y.L.;Liu,F.G.;Huang,Z.;Ng,W.W.Y.;Zhong,J.Two-EchelonDispatchingProblemwithMobileSatellitesinCityLogistics.
IEEETrans.Intell.Transp.Syst.2022,23,84–96.[CrossRef]
79. Yan,X.;Huang,H.;Hao,Z.;Wang,J.AGraph-BasedFuzzyEvolutionaryAlgorithmforSolvingTwo-EchelonVehicleRouting
Problems.IEEETrans.Evol.Comput.2020,24,129–141.[CrossRef]
80. Zhang,D.;Zhou,S.;Ji,B.;Li,S.ATwo-EchelonCapacitatedVehicleRoutingProblemwithSharingSatelliteResources. IEEE
Trans.Intell.Transp.Syst.2024,25,12216–12227.[CrossRef]
81. Accorsi,L.; Vigo,D.Ahybridmetaheuristicforsingletruckandtrailerroutingproblems. Transp. Sci. 2020,54,1351–1371.
[CrossRef]
82. daCruz,H.F.A.;SallesdaCunha,A.TheProfitableSingleTruckandTrailerRoutingProblemwithTimeWindows:Formulation,
validinequalitiesandbranch-and-cutalgorithms.Comput.Ind.Eng.2023,180,109238.[CrossRef]
83. Li,H.;Wang,F.Branch-price-and-cutforthetruck–droneroutingproblemwithtimewindows.Nav.Res.Logist.2023,70,184–204.
[CrossRef]
84. Li, H.; Zhao, J.; Zhan, Z.TruckandUnmannedVehicleRoutingProblemwithTimeWindows: ASatelliteSynchronization
Perspective.J.Adv.Transp.2022,2022,6599089.[CrossRef]
85. Scherr,Y.O.;Hewitt,M.;NeumannSaavedra,B.A.;Mattfeld,D.C.Dynamicdiscretizationdiscoveryfortheservicenetwork
designproblemwithmixedautonomousfleets.Transp.Res.PartBMethodol.2020,141,164–195.[CrossRef]
86. Issi,G.C.;Linfati,R.;Escobar,J.W.Mathematicaloptimizationmodelfortruckschedulinginadistributioncenterwithamixed
service-modedockarea.J.Adv.Transp.2020,2020,8813372.[CrossRef]
87. Perboli,G.;Tadei,R.;Vigo,D.Thetwo-echeloncapacitatedvehicleroutingproblem:Modelsandmath-basedheuristics.Transp.
Sci.2011,45,364–380.[CrossRef]
88. Crainic,T.G.;Perboli,G.;Mancini,S.;Tadei,R.Two-EchelonVehicleRoutingProblem:Asatellitelocationanalysis.Procedia-Soc.
Behav.Sci.2010,2,5944–5955.[CrossRef]
89. Hemmelmayr,V.C.;Cordeau,J.F.;Crainic,T.G.AnadaptivelargeneighborhoodsearchheuristicforTwo-EchelonVehicleRouting
Problemsarisingincitylogistics.Comput.Oper.Res.2012,39,3215–3228.[CrossRef]
90. Chao,I.M.Atabusearchmethodforthetruckandtrailerroutingproblem.Comput.Oper.Res.2002,29,33–51.[CrossRef]
91. Lin,S.W.;Yu,V.F.;Chou,S.Y.Anoteonthetruckandtrailerroutingproblem.ExpertSyst.Appl.2010,37,899–903.[CrossRef]
92. Voigt,S.;Frank,M.;Fontaine,P.;Kuhn,H.Hybridadaptivelargeneighborhoodsearchforvehicleroutingproblemswithdepot
locationdecisions.Comput.Oper.Res.2022,146,105856.[CrossRef]
93. Archetti,C.;Savelsbergh,M.;Speranza,M.G.TheVehicleRoutingProblemwithOccasionalDrivers.Eur.J.Oper.Res.2016,254,
472–480.[CrossRef]

Mathematics2025,13,1092 28of28
94. Vidal,T.;Crainic,T.G.;Gendreau,M.;Lahrichi,N.;Rei,W.Ahybridgeneticalgorithmformultidepotandperiodicvehicle
routingproblems.Oper.Res.2012,60,611–624.[CrossRef]
95. Huang,Y.;Savelsbergh,M.;Zhao,L.Designinglogisticssystemsforhomedeliveryindenselypopulatedurbanareas.Transp.Res.
PartBMethodol.2018,115,95–125.[CrossRef]
96. Yu, V.F.; Jodiawan, P.; Hou, M.L.; Gunawan, A. Design of a two-echelon freight distribution system in last-mile logistics
consideringcoveringlocationsandoccasionaldrivers.Transp.Res.PartELogist.Transp.Rev.2021,154,102461.[CrossRef]
97. Baldacci,R.;Mingozzi,A.;Roberti,R.;Calvo,R.W.Anexactalgorithmforthetwo-echeloncapacitatedvehicleroutingproblem.
Oper.Res.2013,61,298–314.[CrossRef]
98. Solomon,M.M.AlgorithmsfortheVehicleRoutingandSchedulingProblemswithTimeWindowConstraints.Oper.Res.1987,35,
254–265.[CrossRef]
99. Schneider,M.;Stenger,A.;Goeke,D.Theelectricvehicle-routingproblemwithtimewindowsandrechargingstations.Transp.
Sci.2014,48,500–520.[CrossRef]
100. Tuzun,D.; Burke,L.I.Two-phasetabusearchapproachtothelocationroutingproblem. Eur. J.Oper. Res. 1999,116,87–99.
[CrossRef]
101. Cordeau,J.F.;Gendreau,M.;Laporte,G.Atabusearchheuristicforperiodicandmulti-depotvehicleroutingproblems.Networks
1997,30,105–119.[CrossRef]
102. Breunig,U.;Baldacci,R.;Hartl,R.F.;Vidal,T.Theelectrictwo-echelonvehicleroutingproblem. Comput. Oper. Res. 2019,103,
198–210.[CrossRef]
103. Adulyasak,Y.;Cordeau,J.F.;Jans,R.Formulationsandbranch-and-cutalgorithmsformultivehicleproductionandinventory
routingproblems.INFORMSJ.Comput.2014,26,103–120.[CrossRef]
104. Lin,S.W.;Yu,V.F.;Lu,C.C.Asimulatedannealingheuristicforthetruckandtrailerroutingproblemwithtimewindows.Expert
Syst.Appl.2011,38,15244–15252.[CrossRef]
105. Desaulniers,G.;Errico,F.;Irnich,S.;Schneider,M.ExactAlgorithmsforElectricVehicle-RoutingProblemswithTimeWindows.
Oper.Res.2016,64,1388–1405.[CrossRef]
106. Taillard,É.D.AheuristiccolumngenerationmethodfortheheterogeneousfleetVRP.RAIRO-Oper.Res.1999,33,1–14.[CrossRef]
107. Schneider,M.;Löffler,M.Largecompositeneighborhoodsforthecapacitatedlocation-routingproblem. Transp. Sci. 2019,53,
301–318.[CrossRef]
108. Nguyen,V.P.;Prins,C.;Prodhon,C.Solvingthetwo-echelonlocationroutingproblembyaGRASPreinforcedbyalearning
processandpathrelinking.Eur.J.Oper.Res.2012,216,113–126.[CrossRef]
109. Nguyen,V.P.;Prins,C.;Prodhon,C.Amulti-startevolutionarylocalsearchforthetwo-echelonlocationroutingproblem. In
HybridMetaheuristics,Processingsofthe7thInternationalWorkshop,HM2010,Vienna,Austria,1–2October2010;LectureNotesin
ComputerScience;Springer:Berlin/Heidelberg,Germany,2010;pp.88–102.[CrossRef]
110. Wang,Y.;Li,Q.;Guan,X.;Xu,M.;Liu,Y.;Wang,H.Two-echeloncollaborativemulti-depotmulti-periodvehicleroutingproblem.
ExpertSyst.Appl.2021,167,114201.[CrossRef]
111. Breunig,U.;Schmid,V.;Hartl,R.F.;Vidal,T.Alargeneighbourhoodbasedheuristicfortwo-echelonroutingproblems.Comput.
Oper.Res.2016,76,208–225.[CrossRef]
112. Liu,T.;Luo,Z.;Qin,H.;Lim,A.Abranch-and-cutalgorithmforthetwo-echeloncapacitatedvehicleroutingproblemwith
groupingconstraints.Eur.J.Oper.Res.2018,266,487–497.[CrossRef]
113. Crainic,T.G.;Mancini,S.;Perboli,G.;Tadei,R.Clustering-BasedHeuristicsfortheTwo-EchelonVehicleRoutingProblem;CIRRELT
Publ.:Montréal,QC,USA,2008;pp.179–190.
114. Xu,P.;Lan,D.A.N.;Yang,H.;Kim,H.;Shin,I.ShipFormationandRouteOptimizationDesignBasedonImprovedPSOandD-P
Algorithm.IEEEAccess2025,13,15529–15546.[CrossRef]
115. Li,J.;Liu,R.;Wang,R.Handlingdynamiccapacitatedvehicleroutingproblemsbasedonadaptivegeneticalgorithmwithelastic
strategy.SwarmEvol.Comput.2024,86,101529.[CrossRef]
116. Blum,C.;Puchinger,J.;Raidl,G.R.;Roli,A.Hybridmetaheuristicsincombinatorialoptimization:Asurvey.Appl.SoftComput.J.
2011,11,4135–4151.[CrossRef]
Disclaimer/Publisher’sNote: Thestatements, opinionsanddatacontainedinallpublicationsaresolelythoseoftheindividual
author(s)andcontributor(s)andnotofMDPIand/ortheeditor(s).MDPIand/ortheeditor(s)disclaimresponsibilityforanyinjuryto
peopleorpropertyresultingfromanyideas,methods,instructionsorproductsreferredtointhecontent.