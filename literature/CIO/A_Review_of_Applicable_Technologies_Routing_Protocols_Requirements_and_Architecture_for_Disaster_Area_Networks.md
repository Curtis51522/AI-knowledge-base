Received2May2025,accepted13May2025,dateofpublication16May2025,dateofcurrentversion30May2025.
DigitalObjectIdentifier10.1109/ACCESS.2025.3570733
| A Review           | of Applicable |                                      | Technologies, |              | Routing |     |     |
| ------------------ | ------------- | ------------------------------------ | ------------- | ------------ | ------- | --- | --- |
| Protocols,         | Requirements, |                                      | and           | Architecture |         |     |     |
| for Disaster       | Area          | Networks                             |               |              |         |     |     |
| MOHAMMADM.ALSAYYED |               | 1,SELVAKUMARMANICKAM1,(Member,IEEE), |               |              |         |     |     |
|                    |               | 2,I.DEWAMADEWIDIA                    |               | 2,           |         |     |     |
EKARATRINOORWULANDARI
| ANDSHANKARKARUPPAYAH |     | 2,(Member,IEEE) |     |     |     |     |     |
| -------------------- | --- | --------------- | --- | --- | --- | --- | --- |
1CybersecurityResearchCentre(CYRES),UniversitiSainsMalaysia(USM),Penang11800,Malaysia
2FacultyofVocationalStudies,UniversitasBrawijaya,Malang65145,Indonesia
Correspondingauthors:ShankarKaruppayah(kshankar@usm.my)andDewaMadeWidia(dewa_vokasi@ub.ac.id)
ThisworkwassupportedbytheMinistryofEducationofMalaysiathroughtheTransdisciplinaryResearchGrantScheme(TRGS)under
GrantTRGS/1/2022/USM/02/3/4.
ABSTRACT The swift progress of various cutting-edge network topologies, especially Fifth-Generation
Networks (5G), Sixth-Generation Networks (6G), Unmanned Aerial Vehicles (UAVs), and satellite tech-
nologies, presents a promising opportunity to guarantee reliable communication and offer consistent and
secureemergencyservicesintimesofcalamities.Fuelledbytherapidevolutionofnetworkarchitectures,
this study provides a comprehensive overview of the emerging network topologies, technologies, routing
protocols,anddifficultiesassociatedwithdisasterareanetworks(DANs).Thisinvestigationseekstoexamine
theintegrationofvariousDANtopologies,includingaerial,terrestrial,andmaritimenetworks,toenhance
communicationduringadisaster.Subsequently,weassessnumerousnetworkperformancemetrics,suchas
delay, overhead, throughput, energy consumption, packet ratio, and security. The review is concluded by
illuminatingrecentresearchtrendsandopenissuesinthedomainofemergencycommunication.Ultimately,
thisreviewservesasavaluableresourceforresearchers,networkengineers,andpolicymakersinthedomain
ofDANs,offeringathoroughbasisforinformeddecision-makingtostreamlinenetworkdeploymentsand
preservelives.
INDEX TERMS Ad hoc network, artificial intelligence, disaster area network (DAN), deep learning,
emergencycommunications,geologicaldisaster,InternetofThings,routingprotocol.
|     |     |     |     | Developing | a comprehensive | disaster management | strategy |
| --- | --- | --- | --- | ---------- | --------------- | ------------------- | -------- |
I. INTRODUCTION
Recognizing the profound impact of natural and anthro- requires guidelines for recovering communications infras-
pogeniccatastrophes,preservingcommunicationsandinfras- tructure and deploying networks, together with procedures
| tructure is essential | to protecting | lives and | property during |     |     |     |     |
| --------------------- | ------------- | --------- | --------------- | --- | --- | --- | --- |
thatdelineatenetworkdesignandparameters[2].Truthfully,
emergencies. Consequently, launching a well-structured many nations are vulnerable to natural and human-caused
national disaster management plan involving strategies disasters, including floods, mudslides, terrorist attacks, and
and procedures is vital to fulfilling humanitarian aims. industrialmishaps[3].Malaysiaisregrettablysusceptibleto
A disaster management chain encompasses preparedness, flash floods due to severe meteorological conditions, with
| response, mitigation, | and recovery | activities | [1], which |                    |            |                         |       |
| --------------------- | ------------ | ---------- | ---------- | ------------------ | ---------- | ----------------------- | ----- |
|                       |              |            |            | figures indicating | an average | of 143 floods annually. | Flash |
ultimately formulate effective pre- and post-disaster strate- floodsoccurredacrossMalaysiainDecember2021,forcing
gies to deal with large-scale hazards and save lives. 14,459peopletoseekshelterandcausing48casualties[4].
Oneoftheparamountchallengesfollowingadisasterarises
|                      |              |               |                     | from maintaining | communication | among numerous | enti- |
| -------------------- | ------------ | ------------- | ------------------- | ---------------- | ------------- | -------------- | ----- |
| The associate editor | coordinating | the review of | this manuscript and |                  |               |                |       |
approvingitforpublicationwasWeiQuan. ties, including the federal and local governments, hospitals,

2025TheAuthors.ThisworkislicensedunderaCreativeCommonsAttribution4.0License.
VOLUME13,2025 Formoreinformation,seehttps://creativecommons.org/licenses/by/4.0/ 91129

M.M.Alsayyedetal.:ReviewofApplicableTechnologies,RoutingProtocols,Requirements,andArchitecture
patrols, rescue teams, volunteers, and victims. A commu- network topologies, known as the space-air-ground inte-
nication failure following disasters impedes rescue opera- gratednetwork(SAGIN),offersafeasiblesolutiontoreliable
tions. The disruption of communication hinders interaction emergency communication. SAGIN architecture is divided
between the victim and rescue personnel, restricting the intothreedistinctcategories:space,air,andground,includ-
abilitytoconveyinformationandascertainthevictim’sloca- ing various network topologies such as satellite, unmanned
tion or medical condition. Hence, the rapid deployment of aerial vehicles or balloons, and vehicular ad-hoc networks,
untraditionalnetworksystemsisimperativetoretainingcom- respectively[11].
municationduringemergencies[5]. With the rapid development of intelligent air-ground
In contrast to traditional cellular networks, ad-hoc net- integrated network architecture, UAVs represent a vital
works offer outshining characteristics that can be exploited component that connects high-altitude and terrestrial net-
in disaster situations. The characteristics of an ad-hoc net- works. The hierarchical topology, like Lasagna, is designed
work,whichisawirelessnetwork,includeself-configuration, to leverage the advancement of various UAVs, software-
temporal deployability, and the absence of infrastructure. definednetworking(SDN),andAItechnologies.Therefore,
Therefore, the above traits are essential in emergency inter- athree-layerarchitecturecomprisesground,low-altitude,and
vention,aidprocesses,andcatastropherelief[6]. high-altitudeplatformsdeployedtosupportrescueoperations
In the same context, effectively handling disasters andintelligentlymanagecommunicationusingSDNandAI
necessitates the integration of interdisciplinary physical techniquesduringdisasters.Deployinganintegratednetwork
and cyberspace components. Stated differently, adopting poses various obstacles, including compatibility between
cutting-edge technology is essential for successful disas- three-layer components and issues related to security and
ter management, particularly for swiftly deploying resilient privacy[12].
communication systems in affected regions. In the event Despite extensive research on DANs, there is no uni-
of a disaster, the integration of physical and data systems fied framework that evaluates and compares topologies,
encountersnumerouschallenges.Therefore,aviablesolution technologies, protocols, and requirements in the context of
toguaranteeoptimalperformanceandseamlessmaintenance cutting-edge emergency communication. The absence of a
of vital services involves implementing a resilient network systematicanalysisposesdifficultiesforresearchers,network
architecture that addresses and adapts to unforeseen obsta- engineers, and policymakers to identify the most effective
cles[7]. approachesformaintainingreliablecommunicationandfacil-
Moreover, artificial intelligence (AI) and the Internet of itating emergency services during calamity. Additionally,
Things (IoT) provide vital methods and technologies that the integration of multiple advanced network topologies,
canbeappliedtodisastermanagement.Artificialintelligence encompassing aerial, terrestrial, and maritime networks,
offers various techniques that have a beneficial impact on introducescommunicationcomplexities,suchasdelay,over-
rescuingvictims.AItechniquescomprisemachinelearning, head, throughput, energy consumption, packet ratio, and
network services, and analysis [8]. In parallel, IoT presents security.Accordingly,a comprehensiveanalysisoftheinte-
a feeder for AI algorithms to make comprehensive pre- and grationofcutting-edgetechnologiesisnecessarytostimulate
post-disaster predictions. IoT architecture and applications researchers to continue exploring in the same field. This,
enable various devices to connect and share information, inturn,facilitatestheincorporationofcutting-edgenetwork
which leads to an increase in the amount of valuable infor- designs, technologies, and protocols, providing innovative
mationusedindisastermanagement[9]. solutionsforefficientdisastermanagement.
Managing disasters, whether foreseen or unforeseen, This review thoroughly examines cutting-edge DANs,
demands the confluence of efforts to reduce serious harm highlighting relevant technologies, routing protocols, traits,
to individuals and property. Therefore, enhancing disas- requirements, and architectures. We systematically define
ter management models entails the development of early current DAN topologies and their features. In addition,
warning systems, risk estimation plans, mitigation proce- we evaluate existing DAN implementations, focusing on
dures, and recovery techniques applicable in disaster-prone their effectiveness in guaranteeing emergency communica-
regions. Several tools and approaches, such as Geograph- tion.Furthermore,wediscusstheroleofexistingprotocols,
ical Information Systems (GIS), spatial data management, AImechanisms,andIoTtechnologyinenhancingemergency
sensor networks and the Internet of Things, big data analy- services. Through this review, we aim to provide valuable
sis, and cloud computing, have been integrated to enhance insights for researchers and professionals in the realm of
decision-makingandresourcedistributionincatastrophesit- DANs while identifying key areas for further investigation
uations [10]. In addition, effectively managing disaster area anddevelopment.
networks is essential for risk reduction during calamities, Thefollowingoutlinesthecontributionsofthissurvey:
encompassingthedeployment,management,andintegration • Present a comprehensive literature review of state-of-
of network topologies. However, the infrastructure damage the-art disaster network topologies and technologies,
in the aftermath of the disaster may lead to the failure of along with key protocols, to facilitate the design and
the terrestrial network. Hence, the amalgamation of various deploymentofanefficientdisasternetwork.
91130 VOLUME13,2025

M.M.Alsayyedetal.:ReviewofApplicableTechnologies,RoutingProtocols,Requirements,andArchitecture
FIGURE1. Adhocnetworktypes,subclasses,characteristics,andapplicablescenarios.
• Examine the prospects of integrating various network discussesthechallengesandfuturedirectionsforcountering
architectures in disaster zones and conduct an in-depth theresearch-relatedconcerns.Finally,SectionVIIconcisely
investigation of existing solutions for disaster manage- concludesthisstudy.
mentsystems.
• Highlighttherequirementsofdisasterareanetworksto II. BACKGROUND
operateemergency-efficientservices,suchasresilience, Calamities lead to widespread infrastructure collapse and
reliability,scalability,andsecurity. large-scale power blackouts, while deployed disaster area
• Discuss the challenges and propose novel research networks(DANs)constituteafundamentalelementforpro-
avenuesforenhancingthedeploymentofnetworksand tectinglivesfollowingadisaster.Subsequently,thedeployed
ensuringemergencyservicesindisaster-strickenareas. DANsoughttopossesscertaintraits,includingbeingrapidly
This review is structured as follows: Section II presents a deployable,reliable,efficient,andstable,tomitigatetheside
conciseoverviewofDAN’sarchitectures,characteristics,and effectsandunforeseenrisksresultingfromdisaster[13].This
implementation challenges. Section III examines the exist- section, however, outlines the DAN topologies currently in
ing literature and novel disaster area network topologies useandtheirfeatures.
in the domain of DANs. In Section IV, we delineate the
research framework and the methodology for the literature A. ADHOCNETWORKS
review.Additionally,SectionVcomprehensivelyoutlinesthe In the occurrence of a crisis, device-to-device communi-
requirements of DANs and offers an assessment of mod- cation is essential for relief efforts. Therefore, deploying
ern network topologies and routing protocols. Section VI networkswithuniquetraitsisrequired.Theadhocnetwork,
VOLUME13,2025 91131

M.M.Alsayyedetal.:ReviewofApplicableTechnologies,RoutingProtocols,Requirements,andArchitecture
awirelessnetwork,representsapromisingandevolvednet-
| work that | offers | a wide | variety | of swift | response |     | topologies |     |     |     |     |     |     |     |
| --------- | ------ | ------ | ------- | -------- | -------- | --- | ---------- | --- | --- | --- | --- | --- | --- | --- |
andadaptablefeatures.Adhocnetworksexpandedintodif-
ferenttopologies,includingwirelessmeshnetworks(WMN),
| mobile ad | hoc | networks | (MANET), |     | accompanied |     | by their |     |     |     |     |     |     |     |
| --------- | --- | -------- | -------- | --- | ----------- | --- | -------- | --- | --- | --- | --- | --- | --- | --- |
respectivesubclasses,andwirelesssensornetworks(WSN).
Furthermore,adhocnetworksrelyonavarietyoftraits,such
asdynamictopology,mobility,reliability,density,computa-
| tional power, | etc.                  | [14]. | Figure | 1 illustrates              |     | ad hoc | network |     |     |     |     |     |     |     |
| ------------- | --------------------- | ----- | ------ | -------------------------- | --- | ------ | ------- | --- | --- | --- | --- | --- | --- | --- |
| types,their   | respectivesubclasses, |       |        | associatedcharacteristics, |     |        |         |     |     |     |     |     |     |     |
andapplicablescenarios.
1) WIRELESSMESHNETWORK(WMN)
Leveragingthecharacteristicsofthewirelessmeshnetwork,
| a multi-hop | wireless |              | network, | topology      | in  | several | critical |     |     |     |     |     |     |     |
| ----------- | -------- | ------------ | -------- | ------------- | --- | ------- | -------- | --- | --- | --- | --- | --- | --- | --- |
| scenarios,  | such     | as defensive |          | communication |     | and     | disaster |     |     |     |     |     |     |     |
mitigationefforts,offersapromisingsolution.Whileprocess-
| ing sensitive | information, |     | including |     | video, | data, | and VoIP, |     |     |     |     |     |     |     |
| ------------- | ------------ | --- | --------- | --- | ------ | ----- | --------- | --- | --- | --- | --- | --- | --- | --- |
FIGURE2. ThegeneraltopologyofWMN.
| presents    | a fundamental |              | dilemma,      | WMN | network       |      | topology  |     |     |     |     |     |     |     |
| ----------- | ------------- | ------------ | ------------- | --- | ------------- | ---- | --------- | --- | --- | --- | --- | --- | --- | --- |
| enables     | uninterrupted |              | communication |     | in the        | case | of poten- |     |     |     |     |     |     |     |
| tial router | failures.     | Furthermore, |               | the | decentralized |      | topology  |     |     |     |     |     |     |     |
additionalinfrastructure.Figure3exhibitstheMANETstruc-
| of WMS, | with | many | switches, | enables | valuable |     | functions |     |     |     |     |     |     |     |
| ------- | ---- | ---- | --------- | ------- | -------- | --- | --------- | --- | --- | --- | --- | --- | --- | --- |
turediagram.
suchascommunicationbetweennodes,scalability,andcon-
|           |      |         |                |     |              |     |       | Simultaneously, |                 | enhancing |     | mobile          | communication |     |
| --------- | ---- | ------- | -------------- | --- | ------------ | --- | ----- | --------------- | --------------- | --------- | --- | --------------- | ------------- | --- |
| nectivity | with | minimal | infrastructure |     | requirements |     | in an |                 |                 |           |     |                 |               |     |
|           |      |         |                |     |              |     |       | demands         | the integration |           | of  | several network | topologies,   |     |
emergency[15],[16]. including spatial, aerial, terrestrial, and maritime net-
| Permanent | wireless |     | mesh | routers | (WMR) | constitute | the |             |            |     |             |          |              |     |
| --------- | -------- | --- | ---- | ------- | ----- | ---------- | --- | ----------- | ---------- | --- | ----------- | -------- | ------------ | --- |
|           |          |     |      |         |       |            |     | works [20]. | Therefore, |     | this review | explores | the subclass | of  |
fundamentalcomponentsoftheWMN’smeshtopologythat
MANETtopologies,whicharedetailedbelow:
| establishes | wireless | communication |     |     | via the | internet. | How- |     |     |     |     |     |     |     |
| ----------- | -------- | ------------- | --- | --- | ------- | --------- | ---- | --- | --- | --- | --- | --- | --- | --- |
ever,themaindutyofWMRsistobuildconnectionsbetween
nodeswithinahopdestinationusingtheproperroutingproto-
col,hencecreatinganinternetlink.Furthermore,integrating
WMNwithavarietyofadhocnetworkarchitectures,includ-
| ing mobile | ad  | hoc networks |     | and wireless |     | sensor | networks, |     |     |     |     |     |     |     |
| ---------- | --- | ------------ | --- | ------------ | --- | ------ | --------- | --- | --- | --- | --- | --- | --- | --- |
istheidealadvancementforWMN[17].Figure2illustrates
thegeneraltopologyofWMNintegratedwithdifferentadhoc
networks.
2) MOBILEADHOCNETWORK(MANET)
Inthecontextofmobileadhocnetworks(MANET),numer-
| ous significant |     | traits | encompass | dynamic |     | topology, | multi- |     |     |     |     |     |     |     |
| --------------- | --- | ------ | --------- | ------- | --- | --------- | ------ | --- | --- | --- | --- | --- | --- | --- |
hop,absenceofinfrastructure,andsimplicityofdeployment.
| Moreover, | the | autonomous, |     | expandable, | and | wireless | link |     |     |     |     |     |     |     |
| --------- | --- | ----------- | --- | ----------- | --- | -------- | ---- | --- | --- | --- | --- | --- | --- | --- |
featuresprovidefurtherbenefitstomanagingcommunication
inchallengingcircumstancessuchashurricanes,earthquakes, FIGURE3. TheMANETstructurediagram.
| and tsunamis. |     | In addition, | individual |     | nodes | can | establish a |     |     |     |     |     |     |     |
| ------------- | --- | ------------ | ---------- | --- | ----- | --- | ----------- | --- | --- | --- | --- | --- | --- | --- |
direct link without infrastructure, while routing protocols, 1) Vehicular Ad Hoc Network (VANET): a wireless
suchasreactive(on-demand)routingprotocols,aredesigned network, is a subset of MANET. The VANET topol-
tofacilitatethedataflowbetweennodes[18]. ogy consists of roadside unit (RSU) and vehicles
Another survey [19] concentrated on the primary con- equipped with onboard units (OBUs) that enable var-
straints in establishing MANET. In particular, the authors ious types of communication. However, there are
focused on battery power management, which directly threetypesofcommunicationoverVANET:vehicle-to-
impacts the routing overhead and packet delivery ratio. vehicle(V2V),vehicle-to-roadside(V2R),andvehicle-
Nevertheless, despite the previously mentioned obstacles, to-infrastructure (V2I). Figure 4 illustrates the V2V,
MANETpersistsinsurpassingothernetworktopologiesdue V2R, and V2I communication. Moreover, the sys-
to the number of interconnected nodes and the absence of tem’scommunicationrangereliesonthetechnologies
| 91132 |     |     |     |     |     |     |     |     |     |     |     |     | VOLUME13,2025 |     |
| ----- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ------------- | --- |

M.M.Alsayyedetal.:ReviewofApplicableTechnologies,RoutingProtocols,Requirements,andArchitecture
implementedinVANETforboththesecurityandeffi- unmannedunderwatervehicles(UUVs)andunmanned
ciency of linked vehicles. Within the VANET realm, surface vehicles (USVs), is essential for eradicating
the prevailing technologies are dedicated short-range hazardous maritime operations and boosting emer-
communications (DSRCs) and long-term evolution gencycommunication[26].
vehicle-to-everything(LTE-V2X).Theenvironmentof Furthermore, employing standard maritime rescue
VANET presents several challenges, including multi- research systems, such as autonomous surface ves-
mediatransmission,bandwidthlimitation,andresource sels,underwatervehicles,oraerialplatforms,presents
availability,whichartificialintelligencecaneffectively considerabledifficulties.Fortunately,usingcontempo-
address [21]. Real-time applications are crucial for rary technology, such as unmanned systems, boosts
maintaining sustainable contact and communication SANET’s performance in terms of high efficiency,
among V2V, V2R, and V2I, while the updated data cost-effectiveness,andswiftdeployment[27].Figure6
encompasses news, weather, videos, and entertaining illustrates SANET’s topology and communication
| programs.      | Applications  |                  | on    | VANET        | typically      | fall           | into    | types. |     |     |     |
| -------------- | ------------- | ---------------- | ----- | ------------ | -------------- | -------------- | ------- | ------ | --- | --- | --- |
| the categories |               | of safety,       |       | traffic,     | entertainment, |                | and     |        |     |     |     |
| comfort.       | However,      |                  | those | applications | possess        |                | differ- |        |     |     |     |
| ent problems   |               | and difficulties |       | including    |                | risk analysis, |         |        |     |     |     |
| data           | verification, | prioritisation   |       | and          | packet         | congestion     |         |        |     |     |     |
control[22].
2) FlyAdHocNetwork(FANET):Drones,alsoknown
| as unmanned |     | aerial | vehicles | (UAVs), | constitute |     | the |     |     |     |     |
| ----------- | --- | ------ | -------- | ------- | ---------- | --- | --- | --- | --- | --- | --- |
FlyAdHocNetwork(FANET),anextremelypromis-
| ing avenue |              | for swift    | emergency |            | responses |             | in the  |     |     |     |     |
| ---------- | ------------ | ------------ | --------- | ---------- | --------- | ----------- | ------- | --- | --- | --- | --- |
| aftermath  | of           | catastrophic |           | events.    | The       | aim         | behind  |     |     |     |     |
| deploying  | FANET        |              | is to     | perform    | numerous  |             | crucial |     |     |     |     |
| tasks,     | particularly |              | disaster  | monitoring |           | and manage- |         |     |     |     |     |
ment.Variousdronefeatures,suchassizeandweight,
| altitude,    | range,      | application, |          | and      | flying   | mechanism,  |     |                                          |     |     |     |
| ------------ | ----------- | ------------ | -------- | -------- | -------- | ----------- | --- | ---------------------------------------- | --- | --- | --- |
| pose         | significant | obstacles    |          | to FANET |          | deployment. |     |                                          |     |     |     |
| In addition, |             | FANET’s      | topology |          | factors, | such        | as  |                                          |     |     |     |
|              |             |              |          |          |          |             |     | FIGURE4. TheV2V,V2R,andV2Icommunication. |     |     |     |
powerconsumption,frequencyband,radiopropagation
| model, | dynamic | network |     | architecture, | node | mobility, |     |     |     |     |     |
| ------ | ------- | ------- | --- | ------------- | ---- | --------- | --- | --- | --- | --- | --- |
andnodedensity,presentmajorissues[23].Regarding
the previously mentioned issues, authors in [24] pro- 3) WIRELESSSENSORNETWORKS(WSN)
vided a comprehensive overview of relevant research Presently,thereisawidespreadsurgeinresearchandqueries
onAIandML-basedsolutionsfordifferentchallenges regarding wireless sensor networks (WSNs) that leverage
in FANET-based networks. Meanwhile, incorporating the Internet of Things (IoT). The importance of employing
several techniques is required to improve security, WSN stems from the technologies involved, which include
wirelesscommunication,anextensivespectrumofreal-time
| resource | allocation, |     | and | precision | UAV | positioning |     |     |     |     |     |
| -------- | ----------- | --- | --- | --------- | --- | ----------- | --- | --- | --- | --- | --- |
in FANET. Furthermore, IoT, notably LoRa wire- applications, and a diverse range of sensors serving vari-
less technology, is essential in handling the FANET ous purposes. Moreover, WSNs play an essential role in
challenges, which demand low-power and long-range emergencycommunicationduringseveredisasterscenarios,
communications technology. FANETs can adopt var- such as fire management. Despite this, the implementation
|      |                |     |           |         |              |     |     | of WSNs eliminates | the limitations | associated with | other |
| ---- | -------------- | --- | --------- | ------- | ------------ | --- | --- | ------------------ | --------------- | --------------- | ----- |
| ious | architectures, |     | including | single, | multi-layer, |     | and |                    |                 |                 |       |
multi-group topologies. Leveraging these topological technologiesencompassingwiredsystems,cameras,satellite
traits allows for efficient communication in times of systems, and Bluetooth. Numerous obstacles are present,
emergency [25]. Figure 5 depicts the single, multi- including energy consumption, scalability, security, quality
layer,andmulti-grouptopologiesinFANET. of service, network reliability, and data management. Con-
sequently,thepreviousobstacleshavepromptedtheproposal
| 3) Sea | Ad Hoc | Network |     | (SANET): | also | known | as  |     |     |     |     |
| ------ | ------ | ------- | --- | -------- | ---- | ----- | --- | --- | --- | --- | --- |
maritimewirelesscommunication,isanetworktopol- ofseveralsolutionsthatrelyonmachinelearningalgorithms
ogy specifically intended for carrying out a range of andclusteringmethods[28],[29].
maritime activities. The necessity to exclude human Furthermore, the limited number of simulators under
involvement,however,stemsfromthesignificanthaz- assessment,theomissionofimportantfeatures,andthelack
ofexplicitperformancecriteriaraisechallengesinselecting
| ards | associated | with | maritime |     | activities. | Therefore, |     |     |     |     |     |
| ---- | ---------- | ---- | -------- | --- | ----------- | ---------- | --- | --- | --- | --- | --- |
cutting-edge technology, such as unmanned marine the optimal simulator for evaluating WSNs [30]. Figure 7
vehicles (UMVs) that fall into the categories of illustratestheWSNtopology.
| VOLUME13,2025 |     |     |     |     |     |     |     |     |     |     | 91133 |
| ------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ----- |

M.M.Alsayyedetal.:ReviewofApplicableTechnologies,RoutingProtocols,Requirements,andArchitecture
FIGURE5. TheFANETtopologies.
FIGURE6. TheSANET’stopology.
B. CELLULARNETWORKS
Cellular networks, commonly known as mobile networks,
offerthefundamentalinfrastructureandconnectivityneces-
sary for effective message exchange among a vast number
ofmobiledevicesacrossvariousgeographicalregions.While
cellularnetworksmakeasignificantcontributiontoimprov-
FIGURE7. TheWSNtopology.
ing service quality in disaster-affected areas, deployment of
mobilenetworksposesnotablechallenges,suchasscalability,
throughputefficiency,overhead,etc.,whichrequirecreative
solutions to guarantee long-term viability and flexibility. forthcoming pandemics through the incorporation of the
However,theevolutionofmobilenetworks,specifically4G, Internet of Medical Things (IoMT). Hence, several schol-
5G, and 6G, fosters the continued development of smart ars concentrate on using significantly higher data rates,
cities.This,inturn,facilitatesthedeliveryofdiverseservices decreased latency, increased capacity, and a more efficient
like emergency vehicle navigation, instantaneous data shar- spectrum of next-generation technology for establishing
ing,andtrafficcontrol[31]. networks[32].
The advancements in fifth-generation (5G)/beyond 5G Additionally, light is shed on the latest research trends
(B5G)/six-generation (6G) technologies exhibit a remark- in the 6G technology, which enables a terahertz com-
able capacity to detect, manage, and address forthcoming munication system operating at T bits per second (Tbs)
pandemicsthroughtheincorporationoftheInternetofMed- [33]. Nevertheless, 6G technology offers a wide range
ical Things (IoMT). The advancements in fifth-generation of key enhancements, including reduced latency, enhanced
(5G)/beyond 5G (B5G)/six-generation (6G) technologies energy efficiency, increased data packet rate, greater con-
exhibitaremarkablecapacitytodetect,manage,andaddress nection density, and improved spectral efficiency. Thus, the
91134 VOLUME13,2025

M.M.Alsayyedetal.:ReviewofApplicableTechnologies,RoutingProtocols,Requirements,andArchitecture
previous major improvements of 6G enable the develop- literaturehavebeencarriedoutonrelatedtopics.Thissection
ment of three-dimensional (3D) coverage communication covers the literature on disaster area network technologies,
networksacrossvariousenvironments,includingunderwater, routingprotocols,andarchitecture.
terrestrial,aerial,andspace,aswellasdigitaltwins,extended Theresearchin[36]offeredanextensivesurveyofthepair-
reality (AR), and virtual reality (VR) applications. Figure 8 ingof5G-and-beyondnetworksinmultipleunmannedaerial
illustratesthecellularnetworktopology. vehicles (UAVs) to enhance network resilience, reliability,
|     |     |     |     | coverage, | and cost. The authors | discussed | the collabora- |
| --- | --- | --- | --- | --------- | --------------------- | --------- | -------------- |
C. SATELLITENETWORKS tion of various emerging technologies and applications to
Current research has primarily focused on satellite com- presentsalientfeaturesfordrones,5G,andwirelessnetworks.
munication techniques for resilient communication in rural Additionally, this survey covered the fundamental aspects
areasordisaster-affectedregions.Researchersareexploring of exploiting a range of network topologies, the Internet
|     |     |     |     | of Things | (IoT), and AI techniques | to protect | lives during |
| --- | --- | --- | --- | --------- | ------------------------ | ---------- | ------------ |
waystoprovidediverseservicesthatincludetelecommunica-
tions,radio,broadcast,computing,andmilitaryapplications. floods, storms, tornadoes, and severe snowstorms. Despite
In addition, the deployment of a variety of satellites, com- thepromisingadvancementsinthecutting-edgetechnologies
prising geosynchronous equatorial orbit (GEO) satellites, mentioned, several challenges emerge, including collision
medium earth orbit (MEO) satellites, low earth orbit (LEO) prevention,controllatency,energyconstraints,andsecurity.
| satellites,     | and ground stations,    | is an effective           | approach          |     |     |     |     |
| --------------- | ----------------------- | ------------------------- | ----------------- | --- | --- | --- | --- |
| for tackling    | emergency communication | challenges.               | Despite           |     |     |     |     |
| this, a complex | three-dimensional       | hierarchical              | network that      |     |     |     |     |
| includes        | the previous topologies | not only                  | enables effective |     |     |     |     |
| communication   | but also poses          | additional                | obstacles such as |     |     |     |     |
| administration, | integration,            | and security complexities | [34],             |     |     |     |     |
[35].Figure9depictsthesatellitenetworkarchitecture.
FIGURE9. Thesatellitenetworkarchitecture.
FIGURE8. Thecellularnetworktopology.
In[37],theauthorspaidmoreattentiontoartificialneural
network(ANN)approachesforriskmanagementintimesof
calamity,whicharepopularlyusedtoimproveresilienceand
III. RELATEDWORKS
Numerous studies have been conducted to leverage the rapiddeployment.Thestudyfullyclarifiesthereasonsbehind
deploymentofresilientandnon-infrastructurenetworksdur- thesupremacyofANN-basedapproachescomparedtoother
ingcatastrophestoboostrescueoperations.Whileintegrating approachesrelativetoperformance.Whileresearchershigh-
severalnetworktopologies,suchasmobilead-hocnetworks lighted the phases ranging from alleviation and planning
(MANET), vehicular ad-hoc networks (VANET), and wire- to response and recovery, they also outlined the different
less sensor networks (WSN), is essential, this integration typesofcatastrophes,includingfloods,wildfires,andothers.
aims to enhance communication among rescuers, victims, Afterwards, a thorough analysis was carried out, demon-
and emergency authorities. Accordingly, various pieces of strating the effectiveness of employing ANNs to forecast
| VOLUME13,2025 |     |     |     |     |     |     | 91135 |
| ------------- | --- | --- | --- | --- | --- | --- | ----- |

M.M.Alsayyedetal.:ReviewofApplicableTechnologies,RoutingProtocols,Requirements,andArchitecture
and control the risk of flooding. Subsequently, they pre- IV. RESEARCHMETHODOLOGY
sentedprospectsforthefuturethatencompassedthepotential This section defines the research framework. Furthermore,
fordevelopinghybridANNtechniquesformakingdisaster- thissectionoutlinestheprocessofsearchingforliteratureand
relateddecisions,addressingtheissueofdatashortages,and itsvariousclassifications.
incorporatingtheglobalpositioningsystem(GPS).
The reference research [38] explored the capability to A. LITERATURESEARCH
enhance the earthquake early warning systems (EEWS) by We initiated our literature review by studying three specific
leveraging the IoT and cloud architecture. Furthermore, the domainsofdisasterareanetworks:technologies,routingpro-
survey examined the deployment of IoT networks for mon- tocols, and architecture. We commenced our search using
itoring seismic waves and enabling cloud architecture to keywords such as Disaster Area Network (DAN), Ad Hoc
collectdata,assess,andemitalarms.Theauthorsadditionally Network, routing, emergency communications, geological
covered several novel techniques to boost disaster network disasters,artificialintelligence,deeplearning,andIoTinte-
deploymentandscalability,includingmachinelearning(ML) gration.Moreover,thedigitallibrariesandresearchplatforms
algorithms, distributed computing, and edge computing. usedinourexaminationareGoogleScholar,SpringerNature,
Regarding future directions, the research suggested some IEEE Xplore, Multidisciplinary Digital Publishing Institute
methods to improve the EEWS, consisting of establishing (MDPI), and Elsevier ScienceDirect. Initially, our search
precise and effective sensors, the fusion of artificial intelli- yielded over 300 articles with publishing years between
gence (AI) and ML, the standardization of communication 2019 and 2024. After examining the existing literature and
protocols,andtheuseoffree,open-sourcesoftware. research trends, we concentrated on relevant technologies,
The research in [39] provides a comprehensive synopsis routingprotocols,andarchitecturefordisasterareanetworks.
of the significance of employing the sensor as a pri- Hence,weenhancedoursearchforliteratureusingkeywords
mary deployed component during catastrophe management. like ad hoc networks, emergency communications, wireless
Inconjunctionwiththetypesofdeployedsensors,incorporat- mesh networks, mobile ad hoc networks, vehicular ad hoc
ingwirelesssensornetworks(WSN)andInternetofThings networks,flyadhocnetworks,seaadhocnetworks,wireless
(IoT) techniques play a pivotal role in designing effective sensornetworks,andcellularnetworks.Theenhancedsearch
disaster management networks. A design that considers a hasyieldedmorethan130articlesrelatedtoourresearch.
fewcrisismanagementresponsibilities,amongthemfinding
victims, lowering risk, and prompt tracking. Moreover, the B. LITERATURETAXONOMY
researchaimstoeffectivelyintegrateemergingtechnologies The authors used their own filtering choices to deter-
tosupportdeployablecalamitysensors.Thesupportedsensor mine the ultimate selection of publications. During the
technologiesincludecomputervision,AI,auditorysystems, first phase, we concentrated on recent review articles rel-
robots,WSNs,andIoT,whichintegratetoenhanceinterop- evant to the research issue, particularly those published
erability, mobility, real-time data, and scalability. However, from 2019 to 2024. In the second phase, we identified
the permanent sensors’ spots are susceptible to damage researcharticlesfocusingonthemostrecentapplicabletech-
under certain circumstances. In the future, the emphasis nologies, routing protocols, and architectures in the domain
will be placed on deploying WSNs and UAVs to ensure of disaster area networks backed by trustworthy publishers
real-time communication and convenient sensor mobility, like Elsevier ScienceDirect and Springer Nature. Our study
respectively. comprises31.4%reviewarticlesand68.6%researcharticles.
In [40], the authors placed greater emphasis on revolu- Themajorityofourselectionconsistsofpublishingyears,
tionary sixth-generation (6G) technology to improve data as illustrated in Table 2, from 2019 to 2024. Additionally,
throughput and reliability. While 6G technology will sur- Table2demonstratesthattheGoogleScholarresearchplat-
face following the global deployment of fifth-generation formcomprisesapproximately32.6%ofthearticles.Onthe
(5G), the study investigates the need for 6G technology contrary, IEEE Xplore and MDPI occupy the second and
and its implications for vital sectors such as public pro- third spots, at around 27.21% and 20.4%, respectively. We
tection and disaster relief (PPDR), autonomous vehicles, have systematically selected the timeframe to examine and
and smart transportation systems. In addition, the study reviewtheemergenceandevolutionofdisasterareanetworks
exploresthechallengesandpotentialofcombining6Gwith in the past few years. Therefore, reviews and research arti-
contemporary technologies, including terahertz communi- cles mentioned in our research show promising solutions in
cation, artificial intelligence (AI), machine learning (ML), the domain of disaster management by leveraging different
and quantum communication. Implementing 6G technology networktopologiesandtechnologiestofaceemergingglobal
involves significant obstacles, including limited bandwidth, threats.
highinvestmentcosts,andsecurityandprivacyconcernsthat
requirethoughtfulconsideration. V. DISASTERAREANETWORK:REQUIREMENTAND
Table 1 introduces a review of prior studies, accompa- COMPARATIVEEVALUATION
nied by an analysis and comparison of contributions for the Disaster area networks offer effective solutions by sustain-
reader’sbettercomprehension. ingcommunicationinregionswithdamagedornon-existent
91136 VOLUME13,2025

M.M.Alsayyedetal.:ReviewofApplicableTechnologies,RoutingProtocols,Requirements,andArchitecture
TABLE1. Overviewofpriorstudiesondisasterareanetworks.
infrastructure. Thus, these networks are engineered to oper- compromisestoconventionalcommunicationinfrastructure.
ate in severe conditions, facilitating vital functions such as Consequently, sustaining communication during emergen-
real-time data transmission and emergency services. More- cies necessitates paying attention to multiple requirements,
over, evaluating the performance of DAN is crucial to includingresilience,reliability,scalability,swiftdeployment,
guarantee network resilience and reliability in the event of energyefficiency,andsecurity.Thissectionshedslightonthe
acalamity. requirementsthatmustbeconsideredinthedisasternetwork
Metrics such as scalability, reliability, latency, through- designprocess.
put, and energy efficiency are essential for assessing the
capability of these networks under different scenarios. This 1) RESILIENCEANDRELIABILITY
sectiondelineatesthefundamentalrequirementsofDANand Undoubtedly, a key requirement for guaranteeing recovery
presentsacomparativeevaluationofmodernnetworktopolo- following a network failure is to increase the network’s
giesindisasterareas. resilience.Thus,deployingadisasterrecoveryframeworkis
imperative.Themeticulouslystructuredframeworkdemands
A. REQUIREMENTOFDISASTERAREANETWORK theimplementationofacircularanditerativeprocess,which
Network engineers design and develop a disaster area includesongoingpreparednessandrecoveryplanning,relief
network to operate essential emergency functions under and short-term recovery, long-term recovery, and transi-
severe and unpredictable circumstances. The network must tion[41].Integratingsoftware-definednetworksintoaUAV
continue functioning despite significant disruptions or enables the employment of a multipath routing method,
VOLUME13,2025 91137

M.M.Alsayyedetal.:ReviewofApplicableTechnologies,RoutingProtocols,Requirements,andArchitecture
TABLE2. Theaggregationofreviewandresearcharticlesobtainedthroughvariouscriteria.
whichenhancesthenetwork’sresilience,especiallyinemer- decision-makingindisaster-affectedregions.Enhancingscal-
gencies. Furthermore, the mesh network topology, which abilitynecessitatestheefficientmanagementofUAVfleets,
often connects nodes via many pathways, facilitates the which demands the integration of a robust mathematical
achievement of the same goal. Additionally, the implemen- algorithm to determine the minimum number of aircraft.
tationofswarmintelligencealgorithmsandtheuseofLoRa Hence,thedeploymentofapreciselydesignatedquantityof
technologysignificantlyboostnetworkresiliency[42]. UAVs facilitates optimal network resource allocation [47],
From another perspective, disaster area networks are [48]. Additionally, proactive and reactive protocols, each
susceptible to failure in extreme conditions due to the char- with distinct characteristics, enhance network efficiency by
acteristics of network nodes, including wearable devices, ensuring high data transfer rates, facilitating reliable com-
mobiles,UAVs,andsensors.Thus,enhancingnetworkrelia- munication, and reducing latency. The implementation of a
bilityisfundamentaltoobtainingreal-timedataandensuring position-basedprotocolinDAN,whichenablesthedetermi-
faulttolerance.However,leveragingcutting-edgetechnology, nationofnexthopsbasedonnodelocations,aimstoreduce
suchasdeployingtheInternetofEmergencyServices(IoES) overheadandimprovescalability[49].
| to collect real-time |     | data, directly | affected | the reliability of |     |     |     |     |     |     |
| -------------------- | --- | -------------- | -------- | ------------------ | --- | --- | --- | --- | --- | --- |
thenetwork[43].Inaddition,cloudcomputing,particularly
3) COVERAGE
| when combined | with | satellite | remote | sensing data and IoT, |           |         |           |              |     |                |
| ------------- | ---- | --------- | ------ | --------------------- | --------- | ------- | --------- | ------------ | --- | -------------- |
|               |      |           |        |                       | Expanding | network | coverage, | particularly |     | in rural areas |
providesreliableearthquakeemergencysystems.Thesignif-
|     |     |     |     |     | and remote | places, | is crucial | for delivering | emergency | ser- |
| --- | --- | --- | --- | --- | ---------- | ------- | ---------- | -------------- | --------- | ---- |
icanceofcloudcomputingtechnologystemsfromitsvarious vices. However, drones continue to play a significant role
features,includingrapiddataretrieval,extensivedatastorage,
inenhancingnetworkcoverage.Incorporatingthereinforce-
andcommunicationcapabilities[44].Moreover,establishing
|     |     |     |     |     | ment learning | (RL) | architecture | and | the Siamese-net | neural |
| --- | --- | --- | --- | --- | ------------- | ---- | ------------ | --- | --------------- | ------ |
areliablemonitoringsystemisessentialforthepost-disaster
network,whichleveragesadatabaseoftimesandareasthat
| phase. The | monitoring | system | comprises | multiple compo- |                   |     |                |     |          |                |
| ---------- | ---------- | ------ | --------- | --------------- | ----------------- | --- | -------------- | --- | -------- | -------------- |
|            |            |        |           |                 | drones previously |     | visited, leads | to  | enhanced | coverage [50]. |
nents,includingflyingsensornetworks(FSNets),cloud/fog Moreover, the deployment of UAVs as mobile aerial base
computing,andAIalgorithmsintegratedtosatisfytherelia-
|     |     |     |     |     | stations (MABSs) |     | after the | destruction | of terrestrial | infras- |
| --- | --- | --- | --- | --- | ---------------- | --- | --------- | ----------- | -------------- | ------- |
bilityrequirement[45].
|     |     |     |     |     | tructure facilitates |          | the preservation |            | of communication | and            |
| --- | --- | --- | --- | --- | -------------------- | -------- | ---------------- | ---------- | ---------------- | -------------- |
|     |     |     |     |     | addresses            | coverage | deficiencies.    | Leveraging |                  | the prior net- |
2) SCALABILITY workarchitecturenecessitatesacombinationofgraphtheory,
In the case of an emergency, a network needs to be suffi- a genetic algorithm (GA), and long-term evolution (LTE)
cientlyadaptivetocopewithafluctuatingnumberofnodes, technology, which together yield enhanced overall service
including victims, authorities, and on-site rescue teams. andcoveragethroughtheaffectedregions[51].
At this juncture, network engineers must evaluate the scal- Moreover,thedamagetothefiberopticconnectivityinfras-
ability requirement to accommodate the growing request tructure poses an additional obstacle to rescue operations.
for network resources. Therefore, using millimeter-wave Mitigatingthelackofconnectivityrequiresahybridcombi-
(mmWave) communications, an ultra-fast and low-latency nation of integrated access and backhaul (IAB) techniques
wirelesssystem,presentsasignificantopportunitytoexploit and non-terrestrial networks (NTN), which is considered a
network resources effectively. The distinctive attributes of promisingmethodinsuchscenarios.TheintegrationofIAB
mmWavesignals,suchasanexpandedbandwidthandexcep- and NTN, which encompasses high- and low-altitude plat-
tional data transfer rates, enhance network scalability in forms (HAPs/LAPs) and low-earth orbit (LEO) satellites,
numerousscenarios[46]. addresses the issue of network coverage during crises [52].
Furthermore, deploying UAV-operated networks is nec- In this context, the oscillating spider monkey optimiza-
essary for obtaining real-time data, which is vital for tion (OSMO) approach, which relies on a device-to-device
| 91138 |     |     |     |     |     |     |     |     |     | VOLUME13,2025 |
| ----- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ------------- |

M.M.Alsayyedetal.:ReviewofApplicableTechnologies,RoutingProtocols,Requirements,andArchitecture
(D2D)communicationmode,presentsanalternativeforcel- service, this hybrid architecture still confronts a significant
lular networks. The suggested approach ensures coverage challengeduetoitscost[59].Consequently,theincorporation
by implementing cluster-based D2D communication [53]. ofmini-andmicrosatellitespresentsasignificantopportunity
Consequently, disaster network coverage can be classified todeploycost-effectivenetworks.Furthermore,commercial
into three distinct groups: local, regional, and global, based firms offer services such as low-power wide-area networks
onthenetworktopologiesandtechniquesapplied. (LPWANs) and spacecraft components. The preceding ser-
vicesenabletheuseofeconomicalspacetechnologiesduring
acrisis[60].
4) RAPIDDEPLOYMENT
|              |               |                                         |      |                |               |          |            | Developing           |               | advanced      | approaches |            | to boost       | the   | efficacy |
| ------------ | ------------- | --------------------------------------- | ---- | -------------- | ------------- | -------- | ---------- | -------------------- | ------------- | ------------- | ---------- | ---------- | -------------- | ----- | -------- |
| Intherealmof |               | disasterareanetworks,rapidnetworkestab- |      |                |               |          |            |                      |               |               |            |            |                |       |          |
|              |               |                                         |      |                |               |          |            | of the communication |               |               | network    | in         | disaster       | areas | (CNDA)   |
| lishment     | is a          | vital requirement.                      |      | Likewise,      |               | the      | ability to |                      |               |               |            |            |                |       |          |
|              |               |                                         |      |                |               |          |            | during information   |               | propagation   |            | plays      | a crucial      | role  | in ful-  |
| facilitate   | communication |                                         | with | minimal        | configuration |          | and        |                      |               |               |            |            |                |       |          |
|              |               |                                         |      |                |               |          |            | filling network      |               | requirements, |            | especially | regarding      |       | optimal  |
| without      | relying       | on pre-existing                         |      | infrastructure |               | requires | a          |                      |               |               |            |            |                |       |          |
|              |               |                                         |      |                |               |          |            | node density,        | communication |               |            | range,     | and deployment |       | cost.    |
seamlesstransitionfromaconventionalnetworktoanemer-
Inthiscontext,deployingtheadvancedmulti-layerinforma-
| gency network. |     | Hence, | addressing |     | the preceding |     | criteria |     |     |     |     |     |     |     |     |
| -------------- | --- | ------ | ---------- | --- | ------------- | --- | -------- | --- | --- | --- | --- | --- | --- | --- | --- |
tiondisseminationmodelofCNDA(MMND)boostsnetwork
| may foster | communication |     |     | during critical |     | situations. | Satel- |              |     |          |     |       |              |     |            |
| ---------- | ------------- | --- | --- | --------------- | --- | ----------- | ------ | ------------ | --- | -------- | --- | ----- | ------------ | --- | ---------- |
|            |               |     |     |                 |     |             |        | performance. | The | proposed |     | model | is segmented |     | into three |
litephonecommunication,whichdoesnotrequireterrestrial
|                 |     |        |          |          |      |            |     | layers according |     | to the      | information |       | scope.    | The first | layer |
| --------------- | --- | ------ | -------- | -------- | ---- | ---------- | --- | ---------------- | --- | ----------- | ----------- | ----- | --------- | --------- | ----- |
| infrastructure, |     | offers | numerous | features | that | facilitate | and |                  |     |             |             |       |           |           |       |
|                 |     |        |          |          |      |            |     | determines       | the | positioning | of          | UAVs, | while the | second    | layer |
enhancerapidemergencycommunication.Atthesametime,
permitsthesharingofcriticalinformationbetweenUAVsand
thistechnologyfacessomeobstacles,suchascostandpower
vehiclenodes.Thethirdlayerensurestheexchangeofinfor-
| efficiency. | However, |     | incorporating |     | advanced | technologies, |     |     |     |     |     |     |     |     |     |
| ----------- | -------- | --- | ------------- | --- | -------- | ------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
mationpertinenttothespecificrescueplanacrossvehicleand
includingAIalgorithms,low-data-ratemodulationschemes,
rescuernodes.Thus,theproposedmodelguaranteesoptimal
| low-bitrate | voice | codecs, | and | low-power |     | encryption | tech- |     |     |     |     |     |     |     |     |
| ----------- | ----- | ------- | --- | --------- | --- | ---------- | ----- | --- | --- | --- | --- | --- | --- | --- | --- |
nodedensityandcommunicationrangewhilesteadilyreduc-
| niques, | may enable |     | a swift | deployment |     | at a reasonable |     |     |     |     |     |     |     |     |     |
| ------- | ---------- | --- | ------- | ---------- | --- | --------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
ingthenetworkdeploymentcost[61].
cost[54].
| Three-dimensional |     |     | (3D) wireless |     | networks | offer | another |     |     |     |     |     |     |     |     |
| ----------------- | --- | --- | ------------- | --- | -------- | ----- | ------- | --- | --- | --- | --- | --- | --- | --- | --- |
tangible solution for achieving rapid deployment through a 6) ENERGYEFFICIENCY
combinationofterrestrial,aerial,andsatellitecommunication Disaster-hit regions are prone to the destruction of power
technologies. Notwithstanding the significance of deploy- sources, which frustrates efforts to extend battery life for
ing a 3D network framework, it still faces specific hurdles, mobilenodes.ImprovingenergyefficiencyinDANsrequires
including cybersecurity, cross-border coordination, and the enhanced techniques and protocols for data routing and
physicallayer[55].Furthermore,theescalatinguseofUAVs transmission.Concurrently,thegoalofapplyingadeeprein-
contributestotheswiftdeploymentofnetworks.Employing forcementlearning-basedalgorithmistodevelopanefficient
three-layer computing architectures, such as mobile edge multi-UAVframework.Theproposedframeworkdividesthe
computing(MEC)andvehiclefogcomputing(VFC),along disaster region into grid segments and enhances the UAV
withaUAVclientlayer,enhancesconnectivityandmeetsthe path, thereby alleviating issues related to UAV operations,
rapiddeploymentrequirementsinDAN[56]. suchasbatterylifetimeandcommunicationrange[62].
|     |     |     |     |     |     |     |     | Employing         | routing |     | protocols | is        | essential   | to  | guarantee |
| --- | --- | --- | --- | --- | --- | --- | --- | ----------------- | ------- | --- | --------- | --------- | ----------- | --- | --------- |
|     |     |     |     |     |     |     |     | energy efficiency |         | in  | DAN.      | Thus, the | recommended |     | reac-     |
5) COST
|            |              |     |       |              |      |                   |     | tive protocol       | known | as  | Distance        | and                 | Energy-aware |         | AODV     |
| ---------- | ------------ | --- | ----- | ------------ | ---- | ----------------- | --- | ------------------- | ----- | --- | --------------- | ------------------- | ------------ | ------- | -------- |
| The cost   | of deploying |     | DAN,  | particularly |      | in developing     |     |                     |       |     |                 |                     |              |         |          |
|            |              |     |       |              |      |                   |     | (DEAODV)            | leads | to  | the enhancement |                     | of           | network | nodes’   |
| countries, | presents     | a   | major | barrier.     | From | this perspective, |     |                     |       |     |                 |                     |              |         |          |
|            |              |     |       |              |      |                   |     | energy consumption. |       |     | During          | the decision-making |              |         | process, |
deployingandintegratingaffordablehardwareandsoftware
|                 |                  |          |               |                |                |              |          | the DEAODV     |            | generates | a          | routing      | matrix  | to identify  | the    |
| --------------- | ---------------- | -------- | ------------- | -------------- | -------------- | ------------ | -------- | -------------- | ---------- | --------- | ---------- | ------------ | ------- | ------------ | ------ |
| can effectively |                  | leverage | DAN           | in communities |                | with         | limited  |                |            |           |            |              |         |              |        |
|                 |                  |          |               |                |                |              |          | shortest       | trajectory | and       | node       | energy,      | thereby | extending    | the    |
| resources.      | Nevertheless,    |          | cloud         | computing,     |                | a low-cost   | com-     |                |            |           |            |              |         |              |        |
|                 |                  |          |               |                |                |              |          | network’s      | lifespan   | during    |            | a disaster   | [63].   | Furthermore, |        |
| puting method,  |                  | allows   | users         | to receive     | emergency      |              | services |                |            |           |            |              |         |              |        |
|                 |                  |          |               |                |                |              |          | the Disaster   | Scenario   |           | Optimal    | Link         | State   | Routing      | (DS-   |
| on demand       | without          |          | necessitating |                | prior hardware |              | deploy-  |                |            |           |            |              |         |              |        |
|                 |                  |          |               |                |                |              |          | OLSR) protocol |            | serves    | as a       | substitute   | for the | Optimal      | Link   |
| ment or         | the installation |          | of            | software       | on their       | devices      | [57].    |                |            |           |            |              |         |              |        |
|                 |                  |          |               |                |                |              |          | State Routing  |            | (OLSR).   | Whereas    | implementing |         | the          | OLSR   |
| Collaborative   | UAVs             | and      | edge          | intelligence   |                | provide      | several  |                |            |           |            |              |         |              |        |
|                 |                  |          |               |                |                |              |          | causes rapid   | energy     |           | depletion, | applying     | DS-OLSR |              | yields |
| additional      | capabilities,    |          | including     | smart          | device         | connectivity |          |                |            |           |            |              |         |              |        |
energysavings.Therefore,DS-OLSRsignificantlyenhances
| and collecting |     | and storing | data | in the | cloud. | Consequently, |     |     |     |     |     |     |     |     |     |
| -------------- | --- | ----------- | ---- | ------ | ------ | ------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
energyefficiencyinemergencycommunication[64].
theedgeintelligenceplatformofUAVsguaranteesmobility,
adaptability,andcost-effectiveness[58].
| Geographicalconstraintsdonotlimitsatellitecommunica- |     |     |     |     |     |     |     | 7) SECURITY |     |     |     |     |     |     |     |
| ---------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- | ----------- | --- | --- | --- | --- | --- | --- | --- |
tion,allowingittodeliveremergencyservicesinlargeareas Security constitutes a fundamental requirement for DANs.
withlimitedgroundinfrastructure.Althoughthedeployment The significance of meeting security requirements stems
of satellites, UAVs, and terrestrial networks boosts DAN from the extensive accessibility of public networks, such
| VOLUME13,2025 |     |     |     |     |     |     |     |     |     |     |     |     |     |     | 91139 |
| ------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ----- |

M.M.Alsayyedetal.:ReviewofApplicableTechnologies,RoutingProtocols,Requirements,andArchitecture
as Wi-Fi and the Next G networks. Meanwhile, the enor- computing facilitate data manipulation and the use of com-
mousvolumeofsensitivedataexchangedduringemergencies puter resources, respectively. Therefore, implementing the
presents an additional security challenge [65]. The dissem- prior computing techniques guarantees diminished latency,
ination of data during emergency communication, which enhanced bandwidth, and the accurate assessment of large
contains historical, health, and personal information, is sus- amountsofdatainemergencies[72].
| ceptible | to cyberattacks. |     | Wi-Fi | and | NextG | networks | meet |     |     |     |     |     |     |     |     |
| -------- | ---------------- | --- | ----- | --- | ----- | -------- | ---- | --- | --- | --- | --- | --- | --- | --- | --- |
securitystandardsbyusingsophisticatedprotocolsandtech-
|               |          |          |         |     |           |            |          | 9) INTEROPERABILITYANDMOBILITY |             |     |             |             |           |         |       |
| ------------- | -------- | -------- | ------- | --- | --------- | ---------- | -------- | ------------------------------ | ----------- | --- | ----------- | ----------- | --------- | ------- | ----- |
| niques.       | However, | security | threats |     | arise due | to the     | constant |                                |             |     |             |             |           |         |       |
|               |          |          |         |     |           |            |          | Effective                      | deployment  |     | of disaster | area        | networks  | entails | the   |
| communication |          | between  | devices |     | and the   | employment | of       |                                |             |     |             |             |           |         |       |
|               |          |          |         |     |           |            |          | adoption                       | of numerous |     | network     | topologies, | including |         | UAVs, |
emerging technologies. In consequence, DANs face sev- Wi-Fi, SDN, LTE, satellites, etc., to facilitate emergency
eralthreats,includingeavesdroppingattacks,impersonation
|          |                   |     |          |     |             |               |     | service.    | Moreover, | DANs     | must | incorporate |           | various    | types |
| -------- | ----------------- | --- | -------- | --- | ----------- | ------------- | --- | ----------- | --------- | -------- | ---- | ----------- | --------- | ---------- | ----- |
| attacks, | denial-of-service |     | attacks, |     | and message | falsification |     |             |           |          |      |             |           |            |       |
|          |                   |     |          |     |             |               |     | of handwear | and       | software | to   | enable      | emergency | assistance |       |
attacks[66].
|     |     |     |     |     |     |     |     | in heterogeneous |     | environments |     | and rapid | mobility. | Accord- |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ---------------- | --- | ------------ | --- | --------- | --------- | ------- | --- |
AI/MLmodulesprovideprecisemethodsofthreatidentifi-
|     |     |     |     |     |     |     |     | ingly, the | development |     | of a | sophisticated | framework, |     | such |
| --- | --- | --- | --- | --- | --- | --- | --- | ---------- | ----------- | --- | ---- | ------------- | ---------- | --- | ---- |
cation,especiallyincloudemergencymanagementsystems. as a unified 3D network framework, aims to accommodate
| Incorporating | intelligent |     | cloud | management |     | facilitates | clus- |     |     |     |     |     |     |     |     |
| ------------- | ----------- | --- | ----- | ---------- | --- | ----------- | ----- | --- | --- | --- | --- | --- | --- | --- | --- |
diversemobilitymodelsandheterogeneousconnectivity.The
| ter management |     | in  | distributed | areas | that | implement | the |     |     |     |     |     |     |     |     |
| -------------- | --- | --- | ----------- | ----- | ---- | --------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
unified3Dnetworkframeworksuccessfullycombinesspace,
Kubernetesclustertechnique.Theproposedapproachoffers air,andgroundnetworks.Theframeworkalsousesadvanced
essentialsecuritymeasurestodetectpossibleandsuspicious
|     |     |     |     |     |     |     |     | beamforming | techniques, |     | federated |     | learning | mechanisms, |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ----------- | ----------- | --- | --------- | --- | -------- | ----------- | --- |
threats. In addition, it facilitates a prompt response to miti- and energy-efficient computational offloading strategies to
gatesecurityissuesintimesofcrisis[67].Anappropriately
enhancenetworkperformanceduringdisasters[73].Inturn,
| developed | intrusion | detection |     | system | (IDS) | is essential | for |     |     |     |     |     |     |     |     |
| --------- | --------- | --------- | --- | ------ | ----- | ------------ | --- | --- | --- | --- | --- | --- | --- | --- | --- |
cross-platformsoftwareisvitalforboostinguserexperience
| precisely | monitoring |     | and preserving |     | sensitive | data. | IDS- |     |     |     |     |     |     |     |     |
| --------- | ---------- | --- | -------------- | --- | --------- | ----- | ---- | --- | --- | --- | --- | --- | --- | --- | --- |
byofferingintegrationswithdifferentoperatingsystems[74].
| enabled | UAVs | use a | dynamic | approach | in  | an SDN-FANET |     |              |             |     |          |       |       |            |     |
| ------- | ---- | ----- | ------- | -------- | --- | ------------ | --- | ------------ | ----------- | --- | -------- | ----- | ----- | ---------- | --- |
|         |      |       |         |          |     |              |     | Furthermore, | unregulated |     | mobility | poses | major | challenges |     |
to track and assess malicious activities. The IDS-enabled forDANsduetotheseamlessmovementofdiversedevices,
approachadoptedaUAVresource-awareloadbalancingstrat-
|     |     |     |     |     |     |     |     | including | wearables, |     | mobiles, | and | drones. | Nevertheless, |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --------- | ---------- | --- | -------- | --- | ------- | ------------- | --- |
egytoguaranteesecurecommunication[68].
|     |     |     |     |     |     |     |     | enhancing | mobility | in  | UAV networks |     | post-disaster |     | necessi- |
| --- | --- | --- | --- | --- | --- | --- | --- | --------- | -------- | --- | ------------ | --- | ------------- | --- | -------- |
Enhancing security measures to improve the safety of tatestheimplementationofmathematicalmodels,suchasthe
| emergency | applications, |     | particularly |     | cloud | computing | apps, |     |     |     |     |     |     |     |     |
| --------- | ------------- | --- | ------------ | --- | ----- | --------- | ----- | --- | --- | --- | --- | --- | --- | --- | --- |
long-distancepath-lossmodel.Themodelsimulatesandfore-
iscrucial.Furthermore,preservingdatainthecloudservers castsfluctuationsinsignalstrengthacrossvariousdistances
| necessitates | the | deployment |     | of a thorough |     | protection | solu- |     |     |     |     |     |     |     |     |
| ------------ | --- | ---------- | --- | ------------- | --- | ---------- | ----- | --- | --- | --- | --- | --- | --- | --- | --- |
inthree-dimensionalairspace[75].
| tion [69]. | However, |           | employing | the         | elliptic | curve         | Diffie- |     |     |     |     |     |     |     |     |
| ---------- | -------- | --------- | --------- | ----------- | -------- | ------------- | ------- | --- | --- | --- | --- | --- | --- | --- | --- |
| Hellman    | (ECDH)   | algorithm |           | contributes | to       | the promotion |         |     |     |     |     |     |     |     |     |
B. ACOMPARATIVEEVALUATIONOFDISASTERAREA
| of end-to-end |     | data encryption. |     | Authorised |     | users can | obtain |     |     |     |     |     |     |     |     |
| ------------- | --- | ---------------- | --- | ---------- | --- | --------- | ------ | --- | --- | --- | --- | --- | --- | --- | --- |
MODERNNETWORKTOPOLOGIES
| data through |     | the encryption |     | mechanism, |     | which | involves |          |               |     |        |     |           |             |     |
| ------------ | --- | -------------- | --- | ---------- | --- | ----- | -------- | -------- | ------------- | --- | ------ | --- | --------- | ----------- | --- |
|              |     |                |     |            |     |       |          | Disaster | Area Networks |     | (DANs) | are | essential | in preserv- |     |
exchangingkeysbasedonECDH.Implementationprotection
|     |     |     |     |     |     |     |     | ing individuals’ |     | lives | during | severe | events. | Accordingly, |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ---------------- | --- | ----- | ------ | ------ | ------- | ------------ | --- |
algorithms,suchasdigitalsignaturesandMD5,mayenhance
|     |     |     |     |     |     |     |     | several research |     | reports | exist | on the | benefits | and | draw- |
| --- | --- | --- | --- | --- | --- | --- | --- | ---------------- | --- | ------- | ----- | ------ | -------- | --- | ----- |
thesecurityofsensitivedataduringadisaster[70].
backsofemployingthevarioustopologies,technologies,and
|     |     |     |     |     |     |     |     | protocols. | Thus, | deploying | a   | well-designed |     | DAN required |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ---------- | ----- | --------- | --- | ------------- | --- | ------------ | --- |
couplingmultiplenetworkarchitectures,methods,androut-
8) HIGHTHROUGHPUTANDLOWLATENCY
ingalgorithmstoachieveahighQoSintimesofcrisis.The
| Providing | and | sustaining |     | effective | emergency |     | services, |     |     |     |     |     |     |     |     |
| --------- | --- | ---------- | --- | --------- | --------- | --- | --------- | --- | --- | --- | --- | --- | --- | --- | --- |
includingvideostreaming,voicecommunication,andemer- performance matrix is an indispensable component of the
|                 |     |     |              |     |            |     |       | DAN evaluation |     | approach, | encompassing |     | a   | rangeof | indica- |
| --------------- | --- | --- | ------------ | --- | ---------- | --- | ----- | -------------- | --- | --------- | ------------ | --- | --- | ------- | ------- |
| gency warnings, |     | is  | of paramount |     | importance | in  | DANs. |                |     |           |              |     |     |         |         |
Expanded emergency services require a massive informa- tors such as topology characteristics, implementation cost,
reliability,packetlatency,overhead,packetratio,etc.Inthis
| tion exchange; |     | consequently, |     | the | emergency | communica- |     |     |     |     |     |     |     |     |     |
| -------------- | --- | ------------- | --- | --- | --------- | ---------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
context,thissurveyexaminesthepreviouslymentionedpub-
| tion system | should |     | guarantee | high | throughput |     | and low |     |     |     |     |     |     |     |     |
| ----------- | ------ | --- | --------- | ---- | ---------- | --- | ------- | --- | --- | --- | --- | --- | --- | --- | --- |
latency. Sophisticated emergency communication systems licationstohighlighttheirspecificdistinctions.
| (ECSs) | leverage | hybrid | network |     | architectures, |     | such as |     |     |     |     |     |     |     |     |
| ------ | -------- | ------ | ------- | --- | -------------- | --- | ------- | --- | --- | --- | --- | --- | --- | --- | --- |
Wi-Fi,LPWAN,andSD-WAN,whichfacilitateVoIPservices 1) ACOMPARATIVEEVALUATIONOFMODERNNETWORK
with low latency. Accordingly, the amalgamation of differ- TOPOLOGIESANDTECHNOLOGIES
entnetworkarchitecturesenhancesqualityofservice(QoS) In the realm of DANs, several combinations of topologies
and quality of experience (QoE) during catastrophes [71]. andtechnologies,eachpossessingprosandcons,havebeen
AI algorithms enhance the handling of vast amounts of implementedtoboostdisasterreliefoperations.Despitethat,
data and elevated data rates by employing ML/DL tech- akeyfeatureofwell-manageddisastersistheintegrationof
niquesinthreatsurveillancesystems.Inturn,edgeandcloud diverse architecture and techniques throughout the pre- and
| 91140 |     |     |     |     |     |     |     |     |     |     |     |     |     | VOLUME13,2025 |     |
| ----- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ------------- | --- |

M.M.Alsayyedetal.:ReviewofApplicableTechnologies,RoutingProtocols,Requirements,andArchitecture
TABLE3. TheWMNdeploymentcharacteristics.
post-disasterstages,consequentlyenablingaswiftresponse However,eachWMNtopologyoffersdifferentadvantages
andprotectinglives. and considerations for appropriate communication during a
Numerousadditionalresearchfieldsexistthatpertaintothe disaster, and incorporating multiple technologies to design
implementation of WMN communications and networking MWNposesaneedforfurtherinvestigationinthisdomain.
to enhance data delivery, transmission range and scalability Table3illustratestheWMNdeploymentcharacteristicsmen-
incriticaltimes.Reference[76]proposedaWMNtopology tionedinthissection.
consisting of IoT sensors and LoRa, a long-range trans- Owing to its numerous advantages, MANET is widely
mission technology and devices. The implemented network deployed to boost communication during natural disasters.
architecture shows an increasing communication range and Researchers integrated a sensor system for disaster com-
deliveryratioinurbanareas. munication and detection powered by a machine-learning
Authors in [77] evaluate the performance of deployed algorithm into MANET [81]. In contrast, the study by [82]
Bluetooth 5.0 technology to mitigate fire in disaster. Addi- integratesaffordableLoRadevicesintoMANETtofacilitate
tionally,researchershaveexaminedthevalueofthereceived long-range device-to-device communication via Bluetooth
signal strength indicator (RSSI) in peer-to-peer (P2P) and andWi-Fi.
meshnetworkcommunication.Accordingtothestudy,mesh According to the MANET architecture, the quantity of
communication coordination enables self-healing capability connection nodes poses challenges in data transmission.
andreroutessignalstoalternativepathwaysacrossextensive An intelligent system design is necessary, considering the
disaster areas. Furthermore, the design of WMN topology significantroleofIoTandArtificialBeeColony(ABC)algo-
plays a crucial role in enhancing the installation of routes rithmsinenhancingemergencycommunication.In[83],the
onspecificmeshnetworknodes.In[78],authorsintroduced studyintroducedaninnovativeintelligentsystemarchitecture
novel triangular and quadrangular mesh network designs in the MANET environment. Moreover, the MANET cash-
based on connected safe set (CSS) nodes. These topologies ing mechanism plays a significant role in boosting network
allowdualloadstoendurefaultsanddisruptionsduringdis- performance.Withlimitedstoragecapacity,themanagement
asterrecovery. paradigmfordatacachingintheMANETisopentofurther
The incorporation of an unmanned aerial vehicle (UAV) refinement to ensure swift access to critical data. A holistic
and IoT devices to establish a mesh network is discussed solution based on a hybrid caching algorithm is introduced
in[79],exploringtheabilitytogatherdataandsustaincom- in[84].
municationinaninfrastructure-freeenvironment.Moreover, In[85],theresearchersdevelopedoptimizedresourceallo-
researchersdevelopedanintegerlinearprogramming(ILP)- cationUsingTokens(RAUT)andqueuemanagement(QM)
basedmodeltoenhancetheUAVtrajectories.Theconceptof models for elastic (EL) and inelastic (IEL) traffic flows.
fusingartificialintelligenceofthings(AIoT)forcatastrophe The research aims to improve end-to-end delay (EED) and
managementemployingWMNarchitectureiselucidatedina quality of service (QoS), which are critical factors in the
notablestudy[80].InadditiontoharnessingWMNfeatures, communicationservicesofferedamongMANETnodes.
including self-healing and network resilience, the authors Additionally, a significant obstacle in MANET is to
developed a lightweight multi-task model to enable a smart enhance performance metrics, such as network throughput,
disasterpreparednessplatform. latency,andenergyconsumption.Thestudyby[86]proposed
VOLUME13,2025 91141

M.M.Alsayyedetal.:ReviewofApplicableTechnologies,RoutingProtocols,Requirements,andArchitecture
TABLE4. VariousrelatedtechnologiesandtechniquesimplementedinMANET.
aninnovativemethodthatleveragesnature-inspiredschedul- communication among vehicles through roadside RSUs in
ing algorithms, primarily relying on observing a neutral the metropolitan region. However, the proposed technique
system,toimproveschedulingperformanceindynamicand outperformswell-establishedleastsquares(LS)andweighted
decentralizedMANETs.Foreffectivepost-disastermessage leastsquaresmethods(WLS)techniquesintermsofdynamic
exchange,anadaptiveanddecentralizedroutingmechanism vehicleranging,rangingerror,andthroughput.
calledADRINisintroduced[87].Bysensinghumanmove- A novel online dynamic population evacuation (DPE)
ment, the proposed mechanism allows for effective data modeladdressesthechallengeoftheshelterallocationprob-
forwarding, which strikes a balance between data transmis- lem (SAP) in a real evacuation scenario. The model tackles
sionrateandenergyconsumptionwhilereducinglatency. theSAPbyapplyingdestinationselectionanddynamictraf-
However, exploiting MANET topology characteristics fic assignment techniques. The model under consideration
enables appropriate emergency communication. Incorporat- investigated two distinct VANET topology configurations,
ing various technologies, techniques, and protocols boosts including vehicular edge computing (VEC) and vehicular
thereliefoperation.Table4presentsasuccinctsummaryof cloudcomputing(VCC).Comparedtoothermodels,itexhib-
variousrelatedtechnologiesandtechniquesimplementedin itedsuperiorperformanceintermsofnetworkclearancetime,
MANET. end-to-end delay, and packet delivery ratio. The model was
Inacrisis,theincorporationofVANETwithcutting-edge discussed in detail in [90]. The authors conducted a study
technologies to bolster relief efforts is expected to pre- in [91] with the specific goal of enhancing the accuracy of
serve lives. Nevertheless, the emergency strategy hinges V2Vcommunicationbyleveragingthe5GNewRadio(NR)
on VANET’s ability to employ video streaming for pre- system.Theauthorsalsousedmodel-lanechanges(IDM-LC)
cisevehicleroutes,particularlyforemergencyvehicles.The and intelligent driver model avoidance (IDM-A) to investi-
authorsin[88]proposedamodelthatemploysvisualsensors, gate how vehicles move in a variety of road situations. The
cameras, and OBU to securely broadcast emergency video findings indicated that the suggested IDM models showed
to connected nodes via 5G wireless technology. A further feasibilityandeffectiveness.
study[89]concentratedonthedevelopmentofauniquetech- DatadisseminationinVANETsposesacriticalchallenge
nique known as received signal strength (RSS), an alternate in guaranteeing a superior quality of service and preventing
scheme for Global Positioning Systems (GPS) to establish unsafe situations. These issues arise due to congestion or a
91142 VOLUME13,2025

M.M.Alsayyedetal.:ReviewofApplicableTechnologies,RoutingProtocols,Requirements,andArchitecture
TABLE5. VariousrelatedtechnologiesandtechniquesimplementedinVANET.
broadcaststormandaddressingtheminVANETarchitectures appropriate protocols. Fusing various technologies, tech-
necessitatesimplementingpropertechniques.Themaingoal niques,andprotocolsraisesemergencyresponseoperations.
of the research in [92] is to implement a hybrid-trust-based Table 5 briefly describes various relevant technologies and
emergencymessagedissemination(HTEMD)modelthatwill techniquesemployedinVANET.
make the VANET topology more flexible and reliable. The A natural disaster caused significant damage to the
proposed model exhibits significant performance compared pre-establishedcommunicationinfrastructure,whichinstantly
to the baseline model, demonstrating a considerably higher resultedinalackofcommunicationbetweenvictimsandres-
rateofcorrectdecisionandresistancetoattack. cue teams. Consequently, innovative technology like drones
Theauthorsin[93]implementtwotypesofmessageaggre- offers effective methods to maintain communication amidst
gation by leveraging a cluster-based RSU-enabled message acrisis.Nonetheless,implementingawell-designedFANET
aggregation protocol (CluRMA). The message aggregation topology may mitigate the residual impacts of the disaster,
typeincludeslocalaggregationattheclusterheadsandglobal considering certain obstacles such as unexpected failures,
aggregationattheRSU.Additionally,theauthorsperformed communication capacity, and power availability. Therefore,
the aggregation process using adaptive Huffman compres- resolving previous obstacles directly influences the disas-
sionandarithmeticcodingtechniquestoidentifysafetyand ter management methodology and protects human life. In
non-safetymessages,respectively.In[94],theauthorsdevel- [96], the researchers conducted a study to improve reliable,
oped the Adaptive Scheduled Partitioning and Broadcasting self-aware, multi-hop UAV operation management to boost
Technique (ASPBT) to avoid a broadcast storm and mes- communication under infrastructure damage and overload
sage delivery failure. The results show that VANET has situations. Furthermore, the researchers suggested a UAV
an accurate and reliable emergency communication broad- operationmanagementframeworktoallowoptimalmission-
cast mechanism based on the proposed technique. In, [95], orientatedcoverage.Theenhancementanalysisdemonstrates
researchersintegratedameta-heuristicsearchapproachwith increasedflightperiods,compatibilitywithoverlaynetworks,
particle swarm optimization (PSO) and time delay-based andreliableservicesupply.
multipath routing (TMR) to tackle broadcast storms. The Theresearchin[97]focusesparticularlyontheimplemen-
proposedapproachofferssignificantimprovementsinterms tation of the Deep Deterministic Policy Gradient (DDPG)
ofthroughputandpacketlossratio,aswellasreducedend- method to enable spatiotemporal dynamic deployment of
to-enddelay. air-ground ANET (AGANET) nodes. The suggested ad hoc
However, vehicles can efficiently share emergency mes- network configuration comprises unmanned aerial vehicles
sages by exploiting VANET topology characteristics and (UAV) and ground-based nodes. Compared with traditional
VOLUME13,2025 91143

M.M.Alsayyedetal.:ReviewofApplicableTechnologies,RoutingProtocols,Requirements,andArchitecture
TABLE6. VariousrelatedtechnologiesandtechniquesimplementedinFANET.
methods, the proposed approach affords superior commu- disaster response efficiency in scenarios involving floods,
nication reliability, enhanced efficiency, and reduced costs earthquakes, and forest fires. Additionally, the proposed
in emergency events. In [98], the authors introduced two modelincorporatesaclusteringapproachtoreducetheenergy
separatemeta-heuristicoptimisationalgorithms,theCuckoo usageandboostnetworkperformance.Theevaluationofthe
SearchAlgorithm(CUCO)andtheParticleSwarmAlgorithm suggested model demonstrated enhanced network through-
(PSO),toprovideanunusualstrategyforhandlingclustersize put, reliability, and energy efficiency, along with broad
issues. The suggested method analysis reveals the improve- coverageofthedisasterzone.
mentinboththroughputandpacketdroppingrate(PDR). Nevertheless,adoptingFANETpropertiesmaybeahighly
In [99], the authors proposed an SDR-enabled FANET effectiveapproachtoprotectingpeopleduringdisasters.This
architecture in disaster-stressed regions. To enable features isparticularlytruewheninfrastructuredamageispermanent
like self-forming, self-organising, and self-healing capabil- andirreversible.Furthermore,theintegrationoftechnologies,
ities, the proposed architecture utilises wireless technology methodologies, and protocols in FANET aims to enhance
equipment, comprising 3G/4G/5G/Wi-Fi systems and Soft- the effectiveness of response operations. Table 6 provides a
ware Defined Radios (SDRs). Additionally, the authors concise overview of pertinent technologies and techniques
implementedahybridconnectivitymodule(HCM)toenrich usedinFANET.
thecommunicationamongUAVs,mobile-to-UAV,andUAV- Numerous innovative approaches have been introduced
to-mobile. In [100], researchers investigate the evolution of and examined using diverse technologies, such as maritime
the evolutionary particle swarm optimization (EPSO)-based wireless communication, radio communication for signal
emergency monitoring geospatial edge service chain within transmission, Delft 3D, and Delft Dashboard. While a con-
the emergency communications network. The experiment ventional tsunami early warning system that uses buoys
findings indicate notable improvements in efficiency, sta- equipped with sensors for emergency communication has
bility, and reliability in emergency monitoring, while the some limitations, the incorporation of existing technol-
investigated method facilitates prompt and reliable services ogy seeks to enhance communication between ships in the
intimesofcalamity. open ocean and ship-to-coastal radio stations. Researchers
In high-risk scenarios, the integration of advanced tech- in [102], combined the preceding technologies with VHF
nologies, such as unmanned aerial vehicles (UAVs) and radiocommunicationtechnologytoimprovecommunication
beyondfifth-generation(B5G)networks,enhancestheoper- in the worst-case scenario. In [103], researchers deployed
ational efficiency of search and rescue (SAR) teams. VHF and HF radio communication systems alongside the
A study [101] developed a multi-UAV and SAR device-to- preceding technologies to boost the duration of signal
device communication model aimed primarily at enhancing propagation.
91144 VOLUME13,2025

M.M.Alsayyedetal.:ReviewofApplicableTechnologies,RoutingProtocols,Requirements,andArchitecture
TABLE7. VariousrelatedtechnologiesandtechniquesimplementedinSANET.
Additionally, the cost of massive data transmission in establishaneffectiveaccesscontrolsystemthatfacilitatesfire
satellite communication technology presents a significant accident management. The outcome indicated the outstand-
obstacle to the SANET topology. The authors in [104] pro- ingefficacyofthemodelinprotectinglivesandassets.
posed a multi-objective optimization model that leverages Another study [107] particularly concentrates on offline
the features of unmanned aerial vehicles. The goal of UAV and online activity assignments for multiple UAVs in wire-
integrationwithageneticalgorithmistoenhancesea-based less sensor networks. For the offline activity assignments
maritime communication, including islands, large vessels, phase, authors enhance the immune multi-agent algorithm,
drones,andmarineaircraftcommunications.Hence,thefind- resulting in higher reliability and convergence efficiency.
ingsshowthepracticalityandefficiencyofthemodel. They enhance adaptive discrete cuckoo algorithms, which
In [105], the authors designed the SANET architecture, directly impact real-time online activity assignments. The
a space-air-ground-sea topology specifically designed to study by [108] introduced the intelligent healthcare system,
reduce the impact of earthquakes. Additionally, the sug- leveraging nanosensor features to improve emergency com-
gested design incorporates several technologies, including municationbetweenvictimsandclinicaldataservers.While
high-altitudeplatformstations(HAPS),6Gnetworks,renew- the primary goal of deployable nanosensors is to gather
able energy sources (RES), and battery energy storage health indicators in real-time, the responsibility of securely
systems(BESSs),toboosttheeffectivenessofnaturaldisaster safeguarding victim data falls to genetic-based encryption
response. The evaluation of the suggested topology reveals techniques.Theproposedintelligentsystemexhibitssuperior
thenetwork’sresilience. energyefficiency,reducedtimeconsumption,andenhanced
Nevertheless,leveragingSANETtopologyforemergency security.
communication seems potentially a viable area for future The authors in [109] offered an empirical model that
study and development. Even though various novel tech- fuses the WSN, based on IoT, with artificial intelligence to
nologies aid in deploying reliable and higher-performance develop an early warning system to deal with forest fires.
networks,routingprotocolscontinuetoposesignificantchal- The researcher developed the FFDNet technique for for-
lengesinSANET.Table7providesasummaryoftherelevant est fire detection by incorporating image sensors and deep
technologiesandmethodsusedinSANET. learning (DL) approaches. However, following the collec-
InaWSNcommunicationnetwork,whichcomprisesone tion of images by sensors assembled in the base station,
ormoresensors,theintegrationofvarioustechnologiesleads the FFDNet technique employed the kernel extreme learn-
to enhanced communication during an emergency. Authors ingmachine(KELM)modelfortheclassification.However,
in [106] introduced Fi-Model, a wireless sensor network the FFDNet approach utilises the kernel extreme learning
that leverages the IoT to enhance the monitoring, detecting, machine(KELM)modeltoclassifydataacquiredbysensors
and emitting alert processes in fire hazard scenarios. The at the base station. The assessments indicate improvements
proposedmodelintegratestheESP8285controller,aCloud- in the FFDNet technique compared to other deep learning
Based API, sensor, and machine learning approaches to models.
VOLUME13,2025 91145

M.M.Alsayyedetal.:ReviewofApplicableTechnologies,RoutingProtocols,Requirements,andArchitecture
TABLE8. VariousrelatedtechnologiesandtechniquesimplementedinWSN.
However,thedeploymentofWSNsbasedonIoTtopology findings demonstrate significant improvements in perfor-
for emergency communication offers a promising opportu- manceduringemergencies.
nity to improve pre- and post-disaster management proce- In[112],researchersproposedanemergencycommunica-
dures.DeployingWSNsinremoteareasnecessitatesimprov- tion approach, namely RESPOND-A, designed to facilitate
ing the network performance matrix by utilizing a variety theoperationoffirstresponders.Theproposedcommunica-
of routing protocols and technologies. Table 8 presents a tionarchitectureconsistsofacellular5GnetworkandWi-Fi
summaryofthepertinenttechnologiesandmethodsusedin 6 relay devices mounted on UAVs, enabling direct flight to
WSN. designated destinations and boosting communication. The
Extraordinary natural occurrences pose distinct obstacles suggested method successfully achieved high bit rates and
tocommunication.Harnessingthemobilenetworkinfrastruc- fulfilled the first mission communication requirements by
ture for modern emergency rescue missions is considered a establishing a direct link between the 5G base station and
feasible method. The study referenced in [110] conducted users’equipment.
a thorough evaluation of the intelligent crisis management Ultimately, incorporating cellular networks with diverse
system based on deep learning. The proposed smart system network topologies represents substantial progress in emer-
providesameanstosafeguardhumanlifeduringpandemics gencycommunication.Thebenefitstemsfromthepermanent
liketheCOVID-19epidemic.Theproposedsystemconsists infrastructure, high mobile density, resource allocation, and
ofseveralphases.Intheinitialphase,theWirelessBodySen- other related factors. Table 9 presents a summary of the
sorNetwork(WSN)andhospitalsprovideindividualmedical pertinenttechnologiesandmethodsusedincellularnetworks.
records.ThesecondphaseusestheKalmanmethodtofilter One intriguing and promising approach in the domain of
data, while the final phase applies the neural network-long satellite communication involves the integration of several
short-term memory (CNN-LSTM) algorithm to issue emer- network topologies, such as FANET and software-defined
gencyalerts.Moreover,thenetworkarchitectureconsistsof satellite networks, to refine communication after a disaster.
a wireless access vehicular environment (WAVE) and the Authors in [113] pointed out the significance of com-
fifth generation of wireless cellular technology (5G) con- bining the network of unmanned aerial vehicles (UAVs)
nectedwithIES-equippeddevices,includingambulancesand and low Earth orbit (LEO) satellites. To mitigate issues
helicopters. related to received signal strength, data rate, and latency,
Researchersin[111]proposedacomprehensiveapproach the authors introduce a vertical HO scheme that employs
foremergencycommunicationknownasOpen6GRAN.The Analytic Hierarch Process-Entropy (AHP-Entropy) weight-
proposed architectural framework is an innovative method ingandTechniqueforOrderPreferencebySimilaritytothe
thatseekstocreaterobust,durable,flexible,andopen-source Ideal Solution (TOPSIS). While the AHP-Entropy method
sixth-generation (6G) radio access networks with suitable is responsible for classification and selecting the optimal
communication capabilities to withstand natural disasters. network, mobile edge computing (MEC) on the LEO satel-
The researcher integrated an artificial intelligence-based lite is duty-bound for data compression to further reduce
radio access network (RAN) controller to enable various the LEO satellite feeder link delay. Nevertheless, experi-
servicesandswiftrecoverycapabilities,whiletheydeployed mentfindingsindicatethattheintroducedapproachsurpasses
aerial and space segments with the terrestrial network to the benchmark method in terms of throughput and reduced
accommodate emergency communication. Nevertheless, the disconnections.
91146 VOLUME13,2025

M.M.Alsayyedetal.:ReviewofApplicableTechnologies,RoutingProtocols,Requirements,andArchitecture
TABLE9. Variousrelatedtechnologiesandtechniquesimplementedincellularnetworks.
In[114],theauthorsuggestedharnessingtheQuasi-Zenith leveragingsoftware-definednetworking(SDN)andnetwork
Satellite System (QZSS) to develop the effectiveness of the function virtualisation (NFV) technologies to enhance net-
early warning system (EWS). The traditional ground-based work efficiency. The proposed architecture aims to enhance
network currently restricts the dissemination of warning service function chains (SFCs). Furthermore, the proposed
messages in regions affected by severe catastrophic events, adaptable network architecture incorporates rate-adaptive
whereasthesuggestedapproachaimstoincreasethiscapac- SFC management and wireless resource allocation, which
ity and guarantee emergency communication. Furthermore, enable superior network performance in severe conditions.
[115] examined the incorporation of non-terrestrial net- A thorough evaluation demonstrated the proposed archi-
works (NTNs) into 6G telecommunications to guarantee tecture’s effectiveness in managing SFC and significantly
communication across boundaries. Researchers exploit the enhanced resource allocation in highly dynamic network
combinationofIoTservices,UAVs,LEOs,MEOs,andGEOs topologies.
to mitigate communication challenges by reducing latency, Eventually, the integration of satellite networks with
improvingenergyefficiency,andfacilitatingseveralservices. diverse networktopologies providesan optimal solutionfor
The research in [116] dedicated to introducing edge- preserving global communication during emergencies. The
intelligence-driven collaborative SGIN architecture. The benefit lies in the absence of infrastructure, resource allo-
introduced architecture layers consist of the sensing layer, cation, and other related aspects. Table 10 offers a succinct
theforwardinglayer,thecontrollayer,theintelligencelayer, overview of pertinent technologies and techniques used in
andtheapplicationlayer,whichcollaboratetodetectdiverse satellitenetworks.
measurements, alleviate network congestion, and deliver Sustaining emergency cyber services across vast geo-
ubiquitous intelligence services. Concretely, a novel inte- graphicregionsisexceedinglychallengingduringadisaster.
grated learning framework based on convolutional neural Different network topologies allow for covering several
networks (CNN) is formulated to regulate the computation locations to facilitate communication through base stations,
ofoffloadingandnetworkfunctions.Consequently,thepro- UAVs, satellites, and cellular channels. The high-coverage
posedsmartsystemexhibitsasuperioraveragetransmission topologies outlined in [19], [94], [119], [120], and [121]
ratecomparedtorandomscheduling(RS)andgreedypolicy are appropriate for emergency communication over a broad
solutions. geographicalarea.
In [117], the authors introduced the centrally deep Asignificantconsequencethatauthoritiesencounteristhe
reinforcement learning-aided multi-node federated learn- interruption of infrastructure, which can lead to a break-
ing (CDRFL) architecture to foster resource allocation and down in communication between victims and rescue crews.
energy efficiency. The research thoroughly investigated the Furthermore,thenetworkexpansiondemandsconsistentper-
validity of the graph permutation property in the con- formance and a greater density of participating nodes to
text of the Satellite-Ground Integrated Networks (SGIN) enable emergency communication. To guarantee high net-
grapharchitectures.Furthermore,theassessmentofthestudy work capacity while preserving reliability and scalability,
involvesthedemonstrationoftheupperboundofquantization however, a range of high-performance network topologies
error through comprehensive mathematical derivation. The introducedin[86],[87],[92],[97],and[111]aresuitablefor
analysis revealed superior performance in terms of average deployinginhard-hitregions.
latencyandenergyconsumption. Additionally, incorporating different topologies and tech-
The deployment of space-air-ground integrated networks nologiesposeschallengesinthedeploymentofcostlyinfras-
(SAGINs)offersaresilientandadaptabletopologytoaddress tructures. To ensure optimal network performance, specific
thelimitationsofconventionalnetworks,especiallyinensur- factorssuchasscale,complexity,andnetworktypeshouldbe
ingthedeliveryofessentialservicesduringnaturaldisasters. considered,especiallyinemergencies.References[79],[84],
In [118], the authors proposed a novel SAGIN architecture and[87]investigateaffordablecosttopologies.Table11lists
VOLUME13,2025 91147

M.M.Alsayyedetal.:ReviewofApplicableTechnologies,RoutingProtocols,Requirements,andArchitecture
TABLE10. Variousrelatedtechnologiesandtechniquesimplementedinsatellitenetworks.
the characteristics of all topologies proposed in this survey Incontrast,thestudyconductedby[124]appliedanOpti-
to assist network engineers and researchers in selecting a mal Fuzzy Clustering and Trust-based Routing (OFC-TR)
suitabletopologythatmaymeettheirobjectives. approach to reduce the consumption of energy and latency
while simultaneously improving network security and lifes-
pan.In[125],theauthorscarriedoutastudytoinvestigatethe
2) EVALUATIONOFEXISTINGPROTOCOLS effectiveness of data transmission using the adaptive GPSR
Deployingtheemergencynetworktopologiesassessedinthe withdynamicthresholds(AGDT)protocol.Nevertheless,the
previous section presents substantial challenges. Although innovative method merges the Greedy Perimeter Stateless
emergencycommunicationencompassesmanyparticipating Routing (GPSR) with a dynamic threshold-based approach.
nodesthattransmitcriticaldatainashortperiod,choosingthe ThefindingsindicatethatAGDTsurpassescompetingproto-
appropriate network topology with the appropriate protocol cols in terms of packet delivery ratio, end-to-end delay, and
should consider various factors such as node mobility, type throughput.
ofdata,energyconsumption,security,andmore. In the context of VANET topology, routing protocols
OneofMANET’sinevitableproblemsisroutediscovery, are crucial for the real-time dissemination of emergency
which requires tailored solutions. The dynamic connection messages (EMs) among vehicles. However, broadcasting
andfreemobilityofnodes,enabledbytheMANETtopology, various types of EMs, such as videos, voices, traffic con-
directlyinfluencetheperformanceofthenetwork.However, gestion details, etc., demanded effective routing protocols
routingprotocolspresentanoptimalsolutiontoenhanceper- whileconsideringthedynamicnetworktopology,highnode
formance by detecting the routes during catastrophe events. mobility, volume of data, and network resource constraints.
The research reported in [119] provided a comprehensive IntheVANETenvironment,properlycraftedprotocolscon-
overview of the protocol type and traits, including the Ad tributetosuperiornetworkperformancebyreducinglatency,
hocOn-demandDistanceVectorRouting(AODV)protocol, increasingthroughput,andend-to-enddelay.
theDestination-SequencedDistanceVector(DSDV)routing SeveralfurtherresearchdomainsexisttoimproveVANET
algorithm,andtheDynamicSourceRoutingProtocol(DSR). routing protocols. In [126], the researchers introduced
In [122], the authors present a novel hybrid approach the Multi-Path Transmission Protocol for Video Streaming
that integrates two on-demand and one table-driven routing (MPTP-VS) to enhance the transmission of live emergency
protocol to improve the discovery route during disasters. video by leveraging fog computing architecture. Conse-
Additionally, the assessment revealed a higher network quently,theexperimentalevaluationoftheproposedprotocol
density in terms of end-to-end delay, routing load and demonstrates that it decreases latency, boosts throughput,
throughput,anddatapacketdeliverydensity.Fortheenhanc- andenhancesvideostreamingperformance.In[127],authors
ing Link State Routing Protocol (OLSR) protocol, the proposedageographicroutingtechniquethatreliesontrusted
extended osprey-aided optimized link state routing pro- nodestoimproveEMexchange.Whiletrustednodesconcen-
tocol (EO_OLSRP) method incorporates a deep learning trateonevaluatinglinkqualityandnodequality,theresearch
model was implemented to examine routing. The sug- resultsshowasubstantialperformanceenhancementinmes-
gested model demonstrates superior performance in terms sagedeliveryrate,end-to-enddelay,andnetworkthroughput.
of a packet-delivery ratio (PDR), average end delay, and In [128], the author introduces the supercluster-based
throughput[123]. urban multi-hop broadcast and best forwarder selection
91148 VOLUME13,2025

M.M.Alsayyedetal.:ReviewofApplicableTechnologies,RoutingProtocols,Requirements,andArchitecture
protocol(UMB-BFS).Theproposedprotocolemploysmod- ratio, end-to-end delay, throughput, and lifetime of the
ified density peak clustering (MDPC) for the clustering network.
process, while improved firefly optimisation (IFO) duty is The implementation of SANET-based ground systems to
to select the optimal path. However, the findings indicate facilitateair-to-sea(A2S)communicationnecessitatestheuse
outstanding results in Edge-RSU for 5G VANET, including ofavarietyofemergingtechnologies,including5Gand6G
transmission delay and packet delivery ratio. The research wireless technologies, cloud and edge computing, and the
in [129], suggested a unique clustering technique, known maritimeInternetofThings(MIoT).Inaddition,toimprove
astheCluster-BasedProtocolforPrioritizedMessageCom- A2Scommunication,carefullyengineeredroutingprotocols
munication in VANET. By eliminating any delay during are required to prevent delays and ensure reliable wireless
exchangeEMs,thesuggestedprotocolpermitsthetemporary transmissions. However, several protocols have been exam-
storage of non-urgent data. Consequently, it facilitates the inedinSANETtopology,includingend-to-endtransmission,
swiftexchangeofEMsamongvehicles. clusterrouting,andopportunisticroutingprotocols[134].
A study [130] presents a hybrid RF/VLC system to The work in [135] investigated the opportunistic routing
show an effective adaptive routing protocol for emergency protocols (ORP) within the framework of remote maritime
messages when there are a lot of people using VANET. emergencycircumstances,discussingtheprobabilityofeffec-
While the quickly emerging Visible Light Communications tivelytransmittingemergencycommunication.However,the
(VLC) offers complementary short-range connectivity with assessmentofcrucialindicators,suchastheaveragelatency
highbandwidthandlowinterference,thepresentedprotocol anddeliveryprobability,exposedthelimitationsoftheORP
increasessecurityandperformanceduringanemergency. indistantmaritimeregions.In[136],researchersinvestigated
Deploying FANET plays an essential role in facilitating the Ad hoc On-Demand Distance Vector Routing (AODV)
rescue efforts during catastrophes. However, employing the protocol for warship communication. They focused on two
proper protocol to enhance connectivity in infrastructure important matrices: the packet delivery ratio (PDR) and the
damaged areas offers numerous advantages, including the end-to-end delay. Nevertheless, the outcome demonstrated
abilitytoexpand,reliability,faulthandling,energyefficiency, the outperformance of AODV with structured movement,
localization,increasedcoverage,improvedconnectivity,and whilelimitationsarisewithrandommovement.
reduceddelay[120]. WSNnetworkspossessanotableadvantageinmonitoring
The authors in [131] proposed the Geographic Drone- and supervising critical infrastructures (CIs). Nevertheless,
Based Route Optimization (GDRO) approach, a uniquely implementingeffectiveroutingprotocolsiscrucialtoguaran-
designed communication link to achieve high connection tee reliability, security, and operational efficiency in several
stability and optimize FANET network performance. Addi- WSN applications. Additionally, the purpose of implement-
tionally,theauthorsincorporatedvariousmethods,including ingthewirelessprotocolsinWSNsistoenableinternetcon-
Geographical Graph-Based Mapping (GGM) and Global nectivityfornumerousIoTdevicesandtransferdata[137].
PositioningSystem(GPS).WhiletheGGMfacilitatesreach- The authors in [138] introduced the cluster energy
ing the anchor node, the GPS consistently transmits its hop-based dynamic route selection (CEH-DRS) approach,
locationinformationtoassistindetermininganaccurateloca- drawing inspiration from the strategies employed by bee
tion.Theproposedapproachoutperformedexistingmodelsin colony optimisers. The proposed approach facilitates the
disasterareanetworksintermsofimprovedcommunication routingofdatapacketsobtainedfrommultiplesensors,while
efficiency, higher throughput, decreased end-to-end delay, the clustering process is responsible for various character-
andpacketlossperformance. istics, such as throughput, delay, and packet delivery ratio.
FANET networks encounter many challenges, such as However, the studies demonstrated a boost in network per-
dynamictopology,highnodemobility,andlowdensity.These formancebyattainingbetterthroughput.
issuesnecessitatetheuseofadaptiverelayingtoensuresta- In [139], the author suggested an Urban Adaptive
ble routing. Researchers examined an energy-aware routing Location-based Routing Protocol (UALRP) that serves
schemebasedonavirtualrelaytunnel(EARVRT)in[132]. within the context of dynamic wireless sensor networks.
Inaddition,theproposedprotocoldemonstratesitssuperior- Furthermore, the proposed algorithm incorporates real-time
ityoverstandardroutingprotocolsintermsofdelay,network dataanalyticsmethodsandadaptivemachinelearningmodels
longevity,andpacketdeliveryspeed. to improve routing decisions in perpetual motion networks.
Researchers in [133] designed the Q-learning-aided The evaluation of the suggested protocol showed improve-
resilient routing protocol with hindsight pre-calculation mentsinthenetworkperformancematrix,includinglatency,
(QR2HPC) to establish emergency networks based on a throughput, and energy efficiency. In contrast, the study
swarm of unmanned aerial vehicles. The proposed proto- by [140] proposed an adaptive priority scheduling model to
col aimed at eliminating the intricate computation of deep improvecriticalpacketdeliverytimeandreduceaveragedata
reinforcement learning (DRL), which is not appropriate for delay. The protocol’s algorithm design relies on multilevel
emergency relief scenarios. Hence, the experiment yielded priority packet classification, preemptive packet queuing,
improved system performances in terms of packet delivery and an adaptive criticality-based packet next-hop selection
VOLUME13,2025 91149

M.M.Alsayyedetal.:ReviewofApplicableTechnologies,RoutingProtocols,Requirements,andArchitecture
mechanism. An assessment of performance reveals that the isolated regions. The assessment of the proposed routing
model effectively mitigates data loss and prioritizes emer- protocolshowsadecreaseinpacketdelay,energyusage,and
gencydatatransport. packetlossrate.
Promotinghigh-qualityservice(QoS)andqualityofexpe- Theintegrationofspace-air-groundnetworksposesnumer-
rience (QoE) is critical for effective communication among ous issues, including resource allocation and the establish-
user equipment (UEs) in cellular networks and beyond, ment of multiple paths. The difficulty resides in ensuring
particularly in the context of Fifth-Generation New Radio reliability,faulttolerance,andstablecommunicationinsatel-
(5G-NR).Ensuringefficientexecutionofhandoverprocesses lite networks. In [147], the authors proposed an approach
effectivelyallowsuserstocommunicatequickly,reliably,and to address the prior difficulties in Low Earth Orbit (LEO)
withlowlatency.However,toeliminatechallengesincellular satellitetopologies,termedtheRelativePosition-basedEffi-
networks,thesuccessfulimplementationofroutingprotocols cient Routing (RP-ER). The proposed approach formulates
requires careful consideration of critical performance met- the relative position model based on the laws of satellite
rics such as handover ratio, handover failure, and radio link motion. Afterwards, the central satellite provides address
failure[121]. allocationinstructions,permittingothersatellitestoallocate
Researchers in [141] introduced the collaborative independent addresses and concurrently create primary and
energy-efficient routing protocol (CEERP) based on the backup routes. The results of the experiment reveal that
multi-objective improved seagull algorithm (MOISA) to the RP-ER surpasses the traditional approaches, such as a
enhance and evaluate network performance during 5G and Distributed Address Assignment Mechanism (DAAM) and
6Gtransmission.Theproposedalgorithmleveragestherein- AODV,regardingaddressallocationandpackettransmission.
forcementlearningtechnique(R.L.)toemploycollecteddata During catastrophic circumstances, the network continu-
at the sink node and selection cluster head. The evaluation ously delivers various types of data, encompassing video,
ofCEERPrevealedanenhancementinnetworklifespanand audio, location, and notifications. Although real-time data
energyefficiencycomparedtoexistingprotocols. directly affects rescue operations, protocols are responsible
In [142], researchers developed an efficient mobile gate- for controlling data packet routes to shorten the duration
way selection and discovery-based routing protocol in a of the delay. Additionally, sustaining emergency commu-
heterogeneousnetwork.Providinginternetgatewaysthrough nication requires exploiting network resources to avoid
LongTermEvolution(LTE)technologyposesvariouschal- network overhead. The well-designed protocol results in
lenges,especiallywhenconsideringtheintegrationofcellular enhanced network performance metrics, including process-
communication and VANET architecture. The implemented ing,bandwidth,andhandshakes.However,[26],[133],[142]
routing protocol facilitated the identification and selection concentratedtheiranalysisonenhancingroutingprotocolsto
of internet getaways via an efficient multiple metrics-based reducedelayandoverhead.
relay selection method. Nevertheless, the results in terms Ononehand,transmittingvitaldatasuccessfullyoverthe
of packet delivery ratio, packet delay, and overhead meet network after a disaster represents an additional obstacle.
expectations.Incontrast,thestudyby[143]boostedcellular Thisdifficultystemsfromthelargevolumeofdatatransmit-
vehicle-to-everything(C-V2X)communicationsbyintroduc- ted simultaneously, which presents a negative influence on
ing a routing-aware (RA) protocol that is combined with the throughput indicator. On the other hand, the loss of one
cluster-based routing and a geo-based RA method. The ormoredatapacketsmayresultinasubstantiallossofcritical
proposed method offers an efficient strategy for managing information. The need to improve packet delivery ratios,
communication resources. However, the outcome evidences however,stemsfromtheprofoundinfluenceonnetworkper-
anenhancementinspectrumefficiency. formance.Routingtechniquesforenhancingthroughputand
Asthree-dimensionalhierarchicalsatellitenetwork,which packetratioarepresentedin[129],[132],and[140].
consistsofdifferentairandgroundlayers,encountersvarious The mobility of nodes and data transmission results in a
obstacles related to air computing. Air computing enables significant addition to energy consumption. While energy
severalservicestocatertoendusers’needs,suchassending constraints, particularly in mobile ad hoc networks, lead to
real-timevideoandcommunicatinginanemergency.There- deprivationofconnectivity,exploitingroutingprotocolchar-
fore,toimproveQoSandQoE,intelligentroutingprotocols acteristics may offer an optimal solution. Additionally, the
anddynamiccapacityenhancementarerequired[144]. secure routing of packets is a crucial aspect that demands
The authors in [145] assessed multi-hop routing in a furtherimprovement.Routingproceduresareusedtoensure
multi-tierhybridsatellite-terrestrialrelaynetwork(HSTRN) thesecurityofvitaldata,includingpersonalinformationand
tomeasurethereliabilityofmulti-hoproutinginsatellitenet- medicalrecords.However,[20],[23],[36],[125]evaluatesa
works.Theinvestigatedstationaryoptimalprioritytechnique fewsecurity-relatedenhancementmethods.
demonstratedanimprovementininterruptionprobabilityand Nevertheless,Table12providesanoverviewofthecriteria
low complexity. In [146], researchers introduced a novel for selecting protocols according to network topologies and
constrained multi-agent reinforcement learning approach limitations,suchasdelay,overhead,throughput,packetratio,
(CMADR) to enable seamless communication services in energy,andsecurity.Lastly,thissurveyoffersseveraltables
91150 VOLUME13,2025

M.M.Alsayyedetal.:ReviewofApplicableTechnologies,RoutingProtocols,Requirements,andArchitecture
that provide sufficient information to assist researchers and limitedpowerbatteries,whichposedifficultiesinrecharging
networkengineersinfulfillingtheirneeds. or replacement. Thus, deploying energy-intensive protocols
andhardwarepresentsabarriertosustainingnetworkopera-
tionsafteracalamity.
VI. CHALLENGESANDFUTUREDIRECTION
| Deploying | a disaster | area | network | constitutes |     | an effective |     |     |     |     |     |     |     |
| --------- | ---------- | ---- | ------- | ----------- | --- | ------------ | --- | --- | --- | --- | --- | --- | --- |
strategy for handling a range of disasters. The solutions 5) DYNAMICNETWORKTOPOLOGIES
|           |        |           |          |         |     |           | The swift | movement | of  | nodes | inside the catastrophe |     | zone |
| --------- | ------ | --------- | -------- | ------- | --- | --------- | --------- | -------- | --- | ----- | ---------------------- | --- | ---- |
| discussed | in the | preceding | sections | exhibit | the | potential |           |          |     |       |                        |     |      |
of DAN topologies, technologies, and protocols, together illustrates the very dynamic characteristics of disaster envi-
withtherespectiveimplementationoutcomesandunresolved ronments, including the mobility of portable devices and
issues. Furthermore, the recently proposed solutions lever- rescue teams. Moreover, frequent node mobility hinders the
aged cutting-edge architecture and technology, including development of effective routing protocols and the main-
|         |              |             |     |            |             |     | tenance | of stable | emergency | services. | The | deployment | of  |
| ------- | ------------ | ----------- | --- | ---------- | ----------- | --- | ------- | --------- | --------- | --------- | --- | ---------- | --- |
| drones, | IoT devices, | integration |     | of various | topologies, | and |         |           |           |           |     |            |     |
enhanced protocols to ensure emergency communication. space-air-groundtopologiesoffersafeasiblesolutiontomit-
Exploitingthefeaturesofpriortechnologiesandarchitectures igate node mobility challenges by encompassing extensive
posesauniquerangeoftechnical,security,deployment,and disasterareas.Thepriortopologyoffersapromisingsolution;
social issues. Accordingly, further refinements and evalu- nonetheless, it encounters a substantial challenge stemming
frominsufficienttechnologyinteroperabilityanddifficulties
| ation are | essential | to  | ensure emergency |     | communication | in  |     |     |     |     |     |     |     |
| --------- | --------- | --- | ---------------- | --- | ------------- | --- | --- | --- | --- | --- | --- | --- | --- |
life-threatening scenarios. This section outlines the primary inpredictingdisastrousexpansion.
| challenges | encountered |     | in the realm | of  | DAN and | explores |     |     |     |     |     |     |     |
| ---------- | ----------- | --- | ------------ | --- | ------- | -------- | --- | --- | --- | --- | --- | --- | --- |
6) DEPLOYMENTANDREPAIRRESTRICTIONS
potentialsolutionsforthedisastermanagementsystems.
|     |     |     |     |     |     |     | Theswift       | deploymentofa |     | disasterareanetwork |                    | isvitalyet |     |
| --- | --- | --- | --- | --- | --- | --- | -------------- | ------------- | --- | ------------------- | ------------------ | ---------- | --- |
|     |     |     |     |     |     |     | poses multiple | challenges.   |     | The                 | challenges include | damaged    |     |
A. CHALLENGES
|     |     |     |     |     |     |     | infrastructure, | resource | limitations, |     | and the | employment | of  |
| --- | --- | --- | --- | --- | --- | --- | --------------- | -------- | ------------ | --- | ------- | ---------- | --- |
1) SCALABILITYCHALLENGES
|               |            |          |                |           |         |              | autonomous        | systems. | Consequently, |              | leveraging | low-altitude |       |
| ------------- | ---------- | -------- | -------------- | --------- | ------- | ------------ | ----------------- | -------- | ------------- | ------------ | ---------- | ------------ | ----- |
| Scalability   | represents |          | the bottleneck | of the    | current | disaster     |                   |          |               |              |            |              |       |
|               |            |          |                |           |         |              | and high-altitude |          | network       | capabilities | could      | enhance      | rapid |
| area network. |            | Disaster | management     | generally |         | necessitates |                   |          |               |              |            |              |       |
deploymentandnetworkrepairduringacrisis.
| a scalable | network | architecture    |           | design | to support | numer-     |     |     |     |     |     |     |     |
| ---------- | ------- | --------------- | --------- | ------ | ---------- | ---------- | --- | --- | --- | --- | --- | --- | --- |
| ous users  | and     | mobile devices, | depending |        | on the     | extent and |     |     |     |     |     |     |     |
7) COSTEFFECTIVENESS
| breadth | of the | affected | area. Moreover, |     | ensuring | network |     |     |     |     |     |     |     |
| ------- | ------ | -------- | --------------- | --- | -------- | ------- | --- | --- | --- | --- | --- | --- | --- |
Developinganddeployingacutting-edgenetworkfordisaster
performanceandreliabilitybecomesincreasinglyessentialas
areaspresentsafinancialobstacle,particularlyforresource-
thenetworkexpands,presentingacontinualchallenge.
|     |     |     |     |     |     |     | limited | regions. The | space-air-ground |     | integrated |     | topology |
| --- | --- | --- | --- | --- | --- | --- | ------- | ------------ | ---------------- | --- | ---------- | --- | -------- |
posesasignificantcostchallenge,involvingcomplextechno-
2) TECHNOLOGICALINTEROPERABILITY
logicalandinfrastructurerequirements.Meanwhile,athree-
Expertsseektodevelopaunifiedframeworkfortheintegra-
|     |     |     |     |     |     |     | layer network | guarantees |     | the delivery | of proper | emergency |     |
| --- | --- | --- | --- | --- | --- | --- | ------------- | ---------- | --- | ------------ | --------- | --------- | --- |
tionofdiversetopologiesandtechnologies,includingdrones,
|                       |     |                  |     |            |     |              | services.        | Conversely, | ad       | hoc       | network architecture |          | offers |
| --------------------- | --- | ---------------- | --- | ---------- | --- | ------------ | ---------------- | ----------- | -------- | --------- | -------------------- | -------- | ------ |
| IoT devices,          | and | space-air-ground |     | networks.  |     | The signifi- |                  |             |          |           |                      |          |        |
|                       |     |                  |     |            |     |              | a cost-effective | solution    |          | in crisis | scenarios.           | However, | bal-   |
| cant interoperability |     | challenges       |     | arise from | the | employment   |                  |             |          |           |                      |          |        |
|                       |     |                  |     |            |     |              | ancing advanced  |             | features | with      | cost-effectiveness   | remains  | a      |
ofheterogeneousdevices,routingprotocols,communication
|     |     |     |     |     |     |     | significant | challenge, | constraining |     | broad deployment |     | and |
| --- | --- | --- | --- | --- | --- | --- | ----------- | ---------- | ------------ | --- | ---------------- | --- | --- |
standards,andsecurityschemes.However,establishingstan-
scalabilityinresource-limitedareas.
dardsisacrucialaspectofaddressingthesechallenges,which
demandevolutionforacohesivedisasterareanetwork.
8) SEVEREENVIRONMENTALCIRCUMSTANCES
|     |     |     |     |     |     |     | Diverse | disaster forms, | including |     | collapsed buildings, |     | flood |
| --- | --- | --- | --- | --- | --- | --- | ------- | --------------- | --------- | --- | -------------------- | --- | ----- |
3) SECUREMODELDESIGN zones, wildfires, and harsh weather, directly affect the net-
Designingasecuremodelisaprevalentconcerninemergency
workinfrastructure.Consequently,unpredictableterrainand
communication. Delivering emergency services entails the environmental factors obstruct reliable emergency commu-
transmissionandstorageofsensitiveinformation,including
nicationandthedeliveryofemergencyservicesduringsuch
medical records and victims’ identification. Consequently, events. Hence, severe environmental circumstances present
offeringasecuremodeltoprotecttheinformationofvictims an additional challenge to the deployment of disaster net-
| and authorities |     | from | cyberattacks, | such | as eavesdropping |     |     |     |     |     |     |     |     |
| --------------- | --- | ---- | ------------- | ---- | ---------------- | --- | --- | --- | --- | --- | --- | --- | --- |
works.
attacks,impersonationattacks,denial-of-serviceattacks,and
messagefalsificationattacks,posesmajorchallenges.
9) SOCIALANDMORALCONSIDERATIONS
Theearlierproposedsolutionsneglecttoaddressmoraland
4) ENERGYCONSTRAINTS societalaspects,whichareamongthemostcriticalconcerns.
Inextremedisasters,suchasanearthquake,infrastructureis Disaster response technologies must address issues related
vulnerabletodamage,leadingtoashortageofpowersources. toequitableaccessacrossallsocio-economicstatuses.Addi-
Portabledevicesemployedindisastercommunicationrelyon tionally, cultural sensitivities and rules associated with the
| VOLUME13,2025 |     |     |     |     |     |     |     |     |     |     |     |     | 91151 |
| ------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ----- |

M.M.Alsayyedetal.:ReviewofApplicableTechnologies,RoutingProtocols,Requirements,andArchitecture
TABLE11. Thecharacteristicsofalltopologiesproposedinthissurvey.
91152 VOLUME13,2025

M.M.Alsayyedetal.:ReviewofApplicableTechnologies,RoutingProtocols,Requirements,andArchitecture
TABLE11. (Continued.)Thecharacteristicsofalltopologiesproposedinthissurvey.
disseminationofpersonalinformationmustbeaddressedin constraints, and the integration of heterogeneous systems.
thecontextofdisasterareanetworks. Hence, establishing a secure system is essential for guaran-
teeingtheconfidentialityandreliabilityofdataexchangesin
B. FUTUREDIRECTION disasterscenarios.
1) STANDARDPROTOCOLSTOFOSTERINTEROPERABILITY
Different technologies and topologies are inevitably assimi- 4) RESILIENTNETWORKARCHITECTURES
latedintoadisastermanagementsystem.Thus,establishing Naturalcatastrophesoccurabruptlywithoutanypriornotifi-
common communication protocols and standards facilitates cation.Consequently,deployingaresilientnetworkarchitec-
thesmoothintegrationofheterogeneoussystems.Inacatas- tureisavitalmeanstooffereffectiveandrobustemergency
trophic event, the adopted protocols and standards should services. Furthermore, proper deployment of a resilient net-
be designed to accommodate the variances across dis- work entails adapting to dynamic topologies and harsh
tinct topologies, including spatial, aerial, and terrestrial environmentalcircumstances.
networks.
5) NETWORKSCALABILITYAPPROACHES
2) AI-POWEREDADAPTIVENETWORKING Future research should focus on developing an affordable,
Generally, leveraging artificial intelligence and machine scalable approach to ensure broad adoption and applica-
learning enhances disaster network management. Accord- bility in resource-limited regions. A prospective approach
ingly, AI and ML could be employed in various contexts to couldexploitopen-sourcesoftwareandhardwarecharacter-
meet constantly changing conditions in disaster scenarios. istics to enhance scalability in disaster areas. Additionally,
Potential improvements based on AI and ML encompass collaborative shared infrastructure models such as satel-
enhancingrouting,predictingfailures,boostingsecurity,and lite connections, several ad hoc network topologies, and
dynamicallyallocatingresources. cloud-basedservicescouldbeintegratedtoguaranteeemer-
gencycommunication.
3) SECUREANDTRUSTWORTHYMODELDEVELOPMENT
There is a lack of reliable mechanisms for emergency com- 6) EMPLOYINGEDGECOMPUTINGTECHNIQUES
munication. The absence of a trustworthy model arises Enhancing real-time communication and reducing latency
from various challenges, including node mobility, resource present a promising method for the swift provision of
VOLUME13,2025 91153

M.M.Alsayyedetal.:ReviewofApplicableTechnologies,RoutingProtocols,Requirements,andArchitecture
TABLE12. Recommendedprotocolsaccordingtonetworktopologiesandlimitations.
emergency services through the integration of several 9) HUMAN-CENTEREDDESIGN
topologies and technologies. Additionally, adopting edge Effective disaster response necessitates leveraging every
computing to process real-time data allows expedited available method. Generally, a potential disaster response
decision-makingneardisasterzones. frameworkcouldbedesignedtoprovideemergencyservices
withoutrequiringadvancedtechnicalskills.Therefore,inte-
7) LOW-COSTALTERNATIVE grating a user-friendly interface and conducting a training
programempowerstheefforttosafeguardindividuals’lives.
Low-costalternativesareessentialforthegrowthanddeploy-
| ment of | disaster area networks. | Reducing | the | deployment |     |     |     |     |     |
| ------- | ----------------------- | -------- | --- | ---------- | --- | --- | --- | --- | --- |
cost of network infrastructure, including technologies and 10) POLICYANDREGULATORYFRAMEWORKS
equipment, is crucial for the extensive adoption of disaster Establishing a comprehensive global framework to gov-
areatopologies.
|     |     |     |     |     | ern the moral     | and equitable | deployment     | of  | disaster area  |
| --- | --- | --- | --- | --- | ----------------- | ------------- | -------------- | --- | -------------- |
|     |     |     |     |     | networks could    | effectively   | address social | and | cultural chal- |
|     |     |     |     |     | lenges. Fostering | international | collaboration  |     | contributes to |
8) RENEWABLEENERGYTECHNOLOGIES
Enhancingenergy-efficientroutingprotocolsoffersaviable regulatinginnovativesolutionsthatproviderobust,efficient,
|        |                   |                         |     |           | and impactful | responses, | ultimately safeguarding |     | lives and |
| ------ | ----------------- | ----------------------- | --- | --------- | ------------- | ---------- | ----------------------- | --- | --------- |
| method | to extend battery | lifetime. Additionally, |     | renewable |               |            |                         |     |           |
energy sources play an essential role in regions affected boostingglobaldisasterresponseendeavours.
| by disaster. | Entire network | nodes must | be  | engineered | to  |     |     |     |     |
| ------------ | -------------- | ---------- | --- | ---------- | --- | --- | --- | --- | --- |
operateunderlow-powerconditions,regardlessofthetrans- VII. CONCLUSION
ferreddataduringemergencies,includingvideos,audio,and This paper provides a comprehensive review of the evolu-
location. tionoftopologies,emergingtechnologies,routingprotocols,
| 91154 |     |     |     |     |     |     |     |     | VOLUME13,2025 |
| ----- | --- | --- | --- | --- | --- | --- | --- | --- | ------------- |

M.M.Alsayyedetal.:ReviewofApplicableTechnologies,RoutingProtocols,Requirements,andArchitecture
challenges, and research trends related to disaster area net- V2I Vehicle-to-infrastructure.
| works. This | review | commences | with a concise | overview | of  |       |                                     |     |     |     |     |     |
| ----------- | ------ | --------- | -------------- | -------- | --- | ----- | ----------------------------------- | --- | --- | --- | --- | --- |
|             |        |           |                |          |     | DSRCs | Dedicatedshort-rangecommunications. |     |     |     |     |     |
variousDANnetworkarchitectures,subsequentlypresenting VEC Vehicularedgecomputing.
relevant literature and a systematic classification of diverse VCC Vehicularcloudcomputing.
DANtopologies.Moreover,thisstudyinvestigatedtheincor- EMs Emergencymessages.
poration of various topologies and technologies, including FANET FlyAdHocNetwork.
| 5G, 6G, | UAVs, | satellites, | and AI innovations, | to  | meet |       |                  |     |     |     |     |     |
| ------- | ----- | ----------- | ------------------- | --- | ---- | ----- | ---------------- | --- | --- | --- | --- | --- |
|         |       |             |                     |     |      | SANET | SeaAdHocNetwork. |     |     |     |     |     |
the requirements of DAN. This review exhibits diverse UMVs Unmannedmarinevehicles.
techniques for boosting the performance matrix, such as UUVs Unmannedunderwatervehicles.
throughput, delay, overhead, security, and energy consump- USVs Unmannedsurfacevehicles.
tion.Afterwards,acomparativeassessmentofcontemporary A2S Air-to-sea.
| network | topologies | and routing | protocols | is conducted | to  |      |                            |     |     |     |     |     |
| ------- | ---------- | ----------- | --------- | ------------ | --- | ---- | -------------------------- | --- | --- | --- | --- | --- |
|         |            |             |           |              |     | MIoT | MaritimeInternetofThings.. |     |     |     |     |     |
identify various gaps and solutions. Ultimately, an analysis DL Deeplearning.
of current research trends and unresolved gaps in the field IoMT InternetofMedicalThings.
ishighlightedwiththeidentificationofpotentialavenuesfor UEs Userequipment.
| futureresearch. |        |                 |          |           |     | GEO | Ggeosynchronousequatorialorbit. |     |     |     |     |     |
| --------------- | ------ | --------------- | -------- | --------- | --- | --- | ------------------------------- | --- | --- | --- | --- | --- |
| This            | survey | aims to provide | valuable | resources | for |     |                                 |     |     |     |     |     |
|                 |        |                 |          |           |     | MEO | Mediumearthorbit.               |     |     |     |     |     |
researchers, network engineers, and policymakers in the LEO Lowearthorbit.
domainofDANandemergencycommunication.Inaddition, SDN Software-definednetworking.
itprovidesathoroughanalysisofthestate-of-the-artdisaster
|     |     |     |     |     |     | LTE | LongTermEvolution. |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | ------------------ | --- | --- | --- | --- | --- |
areanetworksanddelineatesthekeychallengesandresearch SGIN Satellite-GroundIntegratedNetworks.
trajectoriesnecessary.Thehopeisthatthissurveywillinspire
|     |     |     |     |     |     | BPNN | BackpropagationNeuralNetworks. |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | ---- | ------------------------------ | --- | --- | --- | --- | --- |
furtherinvestigationinthiscurrentareaandexpediteDAN’s CNN ConvolutionalNeuralNetworks.
| advancement. |     |     |     |     |     | DSDV | Destination-SequencedDistanceVector. |     |     |     |     |     |
| ------------ | --- | --- | --- | --- | --- | ---- | ------------------------------------ | --- | --- | --- | --- | --- |
|              |     |     |     |     |     | NFV  | Networkfunctionvirtualization.       |     |     |     |     |     |
ABBREVIATIONSLIST CDRFL Centrally deep reinforcement learning-aided
| Term  | Description.            |     |     |     |     |              | multi-nodefederatedlearning. |              |            |         |                     |               |
| ----- | ----------------------- | --- | --- | --- | --- | ------------ | ---------------------------- | ------------ | ---------- | ------- | ------------------- | ------------- |
| DAN   | DisasterAreaNetwork.    |     |     |     |     |              |                              |              |            |         |                     |               |
| 5G    | Fifthgeneration.        |     |     |     |     |              |                              |              |            |         |                     |               |
| 6G    | Sixthgeneration.        |     |     |     |     | REFERENCES   |                              |              |            |         |                     |               |
|       |                         |     |     |     |     | [1] D. Cicek | and                          | B. Kantarci, | ‘‘Use      | of      | mobile crowdsensing | in            |
| AI    | Artificialintelligence. |     |     |     |     |              |                              |              |            |         |                     |               |
|       |                         |     |     |     |     | disaster     | management:                  | A            | systematic | review, | challenges,         | and open      |
| IoT   | TheInternetofThings.    |     |     |     |     |              |                              |              |            |         |                     |               |
|       |                         |     |     |     |     | issues,’’    | Sensors,                     | vol. 23,     | no. 3,     | p.1699, | Feb. 2023,          | doi: 10.3390/ |
| MANET | Mobilead-hocnetworks.   |     |     |     |     | s23031699.   |                              |              |            |         |                     |               |
VANET Vehicularad-hocnetworks. [2] M.Matracia,N.Saeed,M.A.Kishk,andM.-S.Alouini,‘‘Post-disaster
WSN Wirelesssensornetworks. communications: Enabling technologies, architectures, and open chal-
lenges,’’IEEEOpenJ.Commun.Soc.,vol.3,pp.1177–1205,2022,doi:
| UAVs | Unmannedaerialvehicles. |     |     |     |     | 10.1109/OJCOMS.2022.3192040. |     |     |     |     |     |     |
| ---- | ----------------------- | --- | --- | --- | --- | ---------------------------- | --- | --- | --- | --- | --- | --- |
ANN Artificialneuralnetwork. [3] M.Ouaissa,M.Ouaissa,S.E.Himer,andZ.Boulouard,‘‘AIandIoT
integrationfornaturaldisastermanagement:Acomprehensivereviewand
| GPS | Theglobalpositioningsystem. |     |     |     |     |        |               |           |         |           |          |             |
| --- | --------------------------- | --- | --- | --- | --- | ------ | ------------- | --------- | ------- | --------- | -------- | ----------- |
|     |                             |     |     |     |     | future | directions,’’ | in AI and | IoT for | Proactive | Disaster | Management. |
EEWS Theearthquakeearlywarningsystems. Hershey,PA,USA:IGI-Global,2024,pp.1–16,doi:10.4018/979-8-3693-
| ML   | Machinelearning.                    |     |     |     |     | 3896-4.ch001.     |                  |              |            |            |             |                |
| ---- | ----------------------------------- | --- | --- | --- | --- | ----------------- | ---------------- | ------------ | ---------- | ---------- | ----------- | -------------- |
|      |                                     |     |     |     |     | [4] M. Safizadeh, | M.               | H. Marzbali, | A.         | Abdullah,  | and N. Z.   | Maliki, ‘‘Pro- |
| LoRa | LongRange.                          |     |     |     |     |                   |                  |              |            |            |             |                |
|      |                                     |     |     |     |     | posed             | flood evacuation | routes       | for        | heritage   | areas based | on spatial     |
| RSSI | Thereceivedsignalstrengthindicator. |     |     |     |     |                   |                  |              |            |            |             |                |
|      |                                     |     |     |     |     | configuration     | analysis:        | A            | case study | of Penang, | Malaysia,’’ | J. Facil-      |
P2P Peer-to-peer. ities Manage., vol. 22, no. 2, pp.295–309, Mar. 2024, doi: 10.1108/
jfm-11-2021-0137.
| WMN | WirelessMeshNetwork. |     |     |     |     |                                                                |     |     |     |     |     |     |
| --- | -------------------- | --- | --- | --- | --- | -------------------------------------------------------------- | --- | --- | --- | --- | --- | --- |
|     |                      |     |     |     |     | [5] S.Prasanna,M.R.Lenka,andA.R.Swain,‘‘Asurveyonroutingproto- |     |     |     |     |     |     |
| ABC | ArtificialBeeColony. |     |     |     |     |                                                                |     |     |     |     |     |     |
colsfordisastermanagement,’’SocialNetw.Comput.Sci.,vol.5,no.2,
QoS Qualityofservice. Jan.2024,Art.no.216,doi:10.1007/s42979-023-02509-2.
QoE Qualityofexperience. [6] M.A.Al-Absi,A.A.Al-Absi,M.Sain,andH.Lee,‘‘Movingadhoc
networks—Acomparativestudy,’’Sustainability,vol.13,no.11,p.6187,
| AODV | Ad  | hoc On-demand | Distance | Vector | routing |     |     |     |     |     |     |     |
| ---- | --- | ------------- | -------- | ------ | ------- | --- | --- | --- | --- | --- | --- | --- |
May2021,doi:10.3390/su13116187.
protocol.
|     |     |     |     |     |     | [7] L. Khaloopour, | Y.  | Su, F. | Raskob, | T. Meuser, | R. Bless, | L. Janzen, |
| --- | --- | --- | --- | --- | --- | ------------------ | --- | ------ | ------- | ---------- | --------- | ---------- |
DSDV Destination-SequencedDistanceVectorrouting K. Abedi, M. Andjelkovic, H. Chaari, P. Chakraborty, M. Kreutzer,
M.Hollick,T.Strufe,N.Franchi,andV.Jamali,‘‘Resilience-by-design
protocol.
in6Gnetworks:Literaturereviewandnovelenablingconcepts,’’2024,
| DSR | DynamicSourceRoutingProtocol.. |     |     |     |     |     |     |     |     |     |     |     |
| --- | ------------------------------ | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
arXiv:2405.17480.
| RSUs | Roadsideunits. |     |     |     |     |           |                    |     |             |     |           |               |
| ---- | -------------- | --- | --- | --- | --- | --------- | ------------------ | --- | ----------- | --- | --------- | ------------- |
|      |                |     |     |     |     | [8] S. K. | Abid, N. Sulaiman, |     | S. W. Chan, | U.  | Nazir, M. | Abid, H. Han, |
OBUs Onboardunits. A. Ariza-Montes, and A. Vega-Muñoz, ‘‘Toward an integrated disas-
termanagementapproach:Howartificialintelligencecanboostdisaster
| V2V | Vehicle-to-vehicle. |     |     |     |     |     |     |     |     |     |     |     |
| --- | ------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
management,’’Sustainability,vol.13,no.22,p.12560,Nov.2021,doi:
| V2R           | Vehicle-to-roadside. |     |     |     |     | 10.3390/su132212560. |     |     |     |     |     |       |
| ------------- | -------------------- | --- | --- | --- | --- | -------------------- | --- | --- | --- | --- | --- | ----- |
| VOLUME13,2025 |                      |     |     |     |     |                      |     |     |     |     |     | 91155 |

M.M.Alsayyedetal.:ReviewofApplicableTechnologies,RoutingProtocols,Requirements,andArchitecture
[9] K.Sharma,D.Anand,M.Sabharwal,P.K.Tiwari,O.Cheikhrouhou,and [28] S. Rajendran and N. Chenniappan, ‘‘A comprehensive survey on sev-
T.Frikha,‘‘AdisastermanagementframeworkusingInternetofThings- eral fire management approaches in wireless sensor networks,’’ Bull.
basedinterconnecteddevices,’’Math.ProblemsEng.,vol.2021,pp.1–21, Electr. Eng. Informat., vol. 13, no. 2, pp.947–954, Apr. 2024, doi:
May2021,doi:10.1155/2021/9916440. 10.11591/eei.v13i2.5833.
[10] S. M. Khan, I. Shafi, W. H. Butt, I.D.L.T.Diez, M.A.L.Flores, [29] K.Kaur,A.Kaur,K.Sarita,K.Saini,S.Kour,andS.Kaur,‘‘Emerging
J.C.Galán,andI.Ashraf,‘‘Asystematicreviewofdisastermanagement applications and ongoing challenges in WSN assisted IoT networks,’’
systems:Approaches,challenges,andfuturedirections,’’Land,vol.12, WorldJ.Adv.Eng.Technol.Sci.,vol.11,no.2,pp.501–507,Apr.2024,
no.8,p.1514,Jul.2023,doi:10.3390/land12081514. doi:10.30574/wjaets.2024.11.2.0143.
[11] M. J. Anjum, T. Anees, F. Tariq, M. Shaheen, S. Amjad, F. Iftikhar, [30] G.H.Adday,S.K.Subramaniam,Z.A.Zukarnain,andN.Samian,‘‘Inves-
and F. Ahmad, ‘‘SpaCE-AIR-Ground integrated network for disas- tigating and analyzing simulation tools of wireless sensor networks: A
ter management: Systematic literature review,’’ Appl. Comput. Intell. comprehensivesurvey,’’IEEEAccess,vol.12,pp.22938–22977,2024,
Soft Comput., vol. 2023, pp.1–20, Feb. 2023, doi: 10.1155/2023/ doi:10.1109/ACCESS.2024.3362889.
6037882. [31] S.Islam,A.Z.Abdulsalam,B.A.Kumar,M.K.Hasan,R.Kolandaisamy,
[12] P.Chen,L.Luo,D.Guo,G.Tang,B.Zhao,Y.Li,andX.Luo,‘‘Why and N. Safie, ‘‘Mobile networks toward 5G/6G: Network architecture,
andhowLasagnaworks:Anewdesignofair-groundintegratedinfras- opportunities and challenges in smart city,’’ IEEE Open J. Com-
tructure,’’ IEEE Netw., vol. 38, no. 2, pp.132–140, Mar. 2024, doi: mun. Soc., vol. 6, pp.3082–3093, 2025, doi: 10.1109/OJCOMS.2024.
10.1109/MNET.2024.3350025. 3419791.
[13] Q. Wang, W. Li, Z. Yu, Q. Abbasi, M. Imran, S. Ansari, Y. Sambo, [32] C.-F. Lin and S.-H. Chang, ‘‘Advanced mobile communication tech-
L.Wu,Q.Li,andT.Zhu,‘‘Anoverviewofemergencycommunication niques in the fight against the COVID-19 pandemic era and beyond:
networks,’’RemoteSens.,vol.15,no.6,p.1595,Mar.2023,doi:10.3390/ Anoverviewof5G/B5G/6G,’’Sensors,vol.23,no.18,p.7817,Sep.2023,
rs15061595. doi:10.3390/s23187817.
[14] R.Agrawal,N.Faujdar,C.A.T.Romero,O.Sharma,G.M.Abdulsahib, [33] M.Banafaa,I.Shayea,J.Din,M.HadriAzmi,A.Alashbi,Y.Ibrahim
O. I. Khalaf, R. F. Mansoor, and O. A. Ghoneim, ‘‘Classification and Daradkeh,andA.Alhammadi,‘‘6Gmobilecommunicationtechnology:
comparisonofadhocnetworks:Areview,’’EgyptianInformat.J.,vol.24, Requirements, targets, applications, challenges, advantages, and oppor-
no.1,pp.1–25,Mar.2023,doi:10.1016/j.eij.2022.10.004. tunities,’’ Alexandria Eng. J., vol. 64, pp.245–274, Feb. 2023, doi:
[15] Z.Nurlan,T.Zhukabayeva,M.Othman,A.Adamova,andN.Zhakiyev, 10.1016/j.aej.2022.08.017.
‘‘Wirelesssensornetworkasamesh:Visionandchallenges,’’IEEEAccess, [34] W. Jiang, ‘‘Software defined satellite networks: A survey,’’ Digit.
vol.10,pp.46–67,2022,doi:10.1109/ACCESS.2021.3137341. Commun. Netw., vol. 9, no. 6, pp.1243–1264, Dec. 2023, doi:
[16] N. M. Jovanovic, ‘‘Analyzing wireless mesh network using spectral 10.1016/j.dcan.2023.01.016.
graph theory,’’ Artif. Intell. Appl., vol. 2, no. 3, pp. 195–201, [35] C. Raja, M. Ramachandran, K. Ramu, and C. Sivaji, ‘‘Radio resource
Feb.2023.[Online].Available:https://scholar.google.com/scholar?as_q= managementsatellitecommunicationnetworksMCDMmethod,’’Com-
Analyzing+Wireless+Mesh+Network+Using+Spectral+Graph+Theory& put. Sci., Eng. Technol., vol. 1, no. 2, pp.23–33, Jan. 2024, doi:
as_occt=title&hl=en&as_sdt=0%2C31 10.46632/cset/1/2/4.
[17] A. Singh, S. Singh, and S. Prakash, ‘‘Critical comparative analysis [36] M.K.Banafaa,Ö.Pepeoğlu,I.Shayea,A.Alhammadi,Z.A.Shamsan,
and recommendation in MAC protocols for wireless mesh networks M.A.Razaz, M. Alsagabi, and S. Al-Sowayan, ‘‘A comprehensive
usingmulti-objectiveoptimizationandstatisticaltesting,’’WirelessPers. survey on 5G-and-beyond networks with UAVs: Applications, emerg-
Commun.,vol.129,no.4,pp.2319–2344,Apr.2023,doi:10.1007/s11277- ing technologies, regulatory aspects, research trends and challenges,’’
023-10228-3. IEEEAccess,vol.12,pp.7786–7826,2024,doi:10.1109/ACCESS.2023.
[18] S. Al Ajrawi and B. Tran, ‘‘Mobile wireless ad-hoc network routing 3349208.
protocolscomparisonforreal-timemilitaryapplication,’’SpatialInf.Res., [37] S. Guha, R. K. Jana, and M. K. Sanyal, ‘‘Artificial neural net-
vol.32,no.1,pp.119–129,Feb.2024,doi:10.1007/s41324-023-00535-z. work approaches for disaster management: A literature review,’’ Int.
[19] S. Hemalatha, M. Rajasekaran, L. K. Sagar, C. R. Komala, J. Disaster Risk Reduction, vol. 81, Oct. 2022, Art.no.103276, doi:
G.N.S.Vijayakumar, A. Nageswaran, M. Syamala, and J. Deepa, ‘‘A 10.1016/j.ijdrr.2022.103276.
reviewofpowermanagementapproachesformobileadhocnetworks,’’ [38] M.Abdalzaher,M.Krichen,D.Yiltas-Kaplan,I.B.Dhaou,andW.Adoni,
J. Européen des Systèmes Automatisés, vol. 57, no. 1, pp.137–145, ‘‘Early detection of earthquakes using IoT and cloud infrastructure:
Feb.2024,doi:10.18280/jesa.570114. A survey,’’ Sustainability, vol. 15, no. 15, p.11713, Jul. 2023, doi:
[20] H.Zhao,F.Ji,Y.Wang,K.Yao,andF.Chen,‘‘Space–air–ground–sea 10.3390/su151511713.
integratednetworkwithfederatedlearning,’’RemoteSens.,vol.16,no.9, [39] Z. T. AlAli and S. A. Alabady, ‘‘A survey of disaster management
p.1640,May2024,doi:10.3390/rs16091640. and SAR operations using sensors and supporting techniques,’’ Int.
[21] M.OkpokandB.Kihei,‘‘Challengesandopportunitiesformultimedia J. Disaster Risk Reduction, vol. 82, Nov. 2022, Art.no.103295, doi:
transmission in vehicular ad hoc networks: A comprehensive review,’’ 10.1016/j.ijdrr.2022.103295.
Electronics, vol. 12, no. 20, p.4310, Oct. 2023, doi: 10.3390/electron- [40] R. Chataut, M. Nankya, and R. Akl, ‘‘6G networks and the AI
ics12204310. revolution—Exploring technologies, applications, and emerging chal-
[22] A. W. K. Al-Nasir and F. S. Mubarek, ‘‘Vehicular Ad-hoc networks lenges,’’ Sensors, vol. 24, no. 6, p.1888, Mar. 2024, doi: 10.3390/
(VANETs):Asurveyonconnectivity,’’AIPConf.Proc.,vol.2793,no.1, s24061888.
pp.1–12,Aug.2023,doi:10.1063/5.0163036. [41] Z. Lokmic-Tomkins, D. Bhandari, C. Bain, A. Borda, T.C.Kariotis,
[23] F.Pasandideh,J.P.J.daCosta,R.Kunst,N.Islam,W.Hardjawana,and
and D. Reser, ‘‘Lessons learned from natural disasters around
E.P.deFreitas,‘‘Areviewofflyingadhocnetworks:Keycharacteristics,
digital health technologies and delivering quality healthcare,’’ Int.
applications,andwirelesstechnologies,’’RemoteSens.,vol.14,no.18,
J.Environ.Res.PublicHealth,vol.20,no.5,p.4542,Mar.2023,doi:
p.4459,Sep.2022,doi:10.3390/rs14184459.
10.3390/ijerph20054542.
[24] F. Pasandideh, J. P. J. D. Costa, R. Kunst, W. Hardjawana, and
[42] M. A. B. Siddiki Abir, M. Z. Chowdhury, and Y. M. Jang,
E.P.deFreitas,‘‘Asystematicliteraturereviewofflyingadhocnetworks:
‘‘Software-defined UAV networks for 6G systems: Requirements,
State-of-the-art,challenges,andperspectives,’’J.FieldRobot.,vol.40,
opportunities,emergingtechniques,challenges,andresearchdirections,’’
no.4,pp.955–979,Jun.2023,doi:10.1002/rob.22157.
IEEE Open J. Commun. Soc., vol. 4, pp.2487–2547, 2023, doi:
[25] W.D.Paredes,H.Kaushal,I.Vakilinia,andZ.Prodanoff,‘‘LoRatechnol-
10.1109/OJCOMS.2023.3323200.
ogyinflyingadhocnetworks:Asurveyofchallengesandopenissues,’’
[43] R.Damaševičius,N.Bacanin,andS.Misra,‘‘Fromsensorstosafety:Inter-
Sensors,vol.23,no.5,p.2403,Feb.2023,doi:10.3390/s23052403.
netofEmergencyServices(IoES)foremergencyresponseanddisaster
[26] I.BaeandJ.Hong,‘‘Surveyonthedevelopmentsofunmannedmarine
management,’’J.SensorActuatorNetw.,vol.12,no.3,p.41,May2023,
vehicles:Intelligenceandcooperation,’’Sensors,vol.23,no.10,p.4643,
doi:10.3390/jsan12030041.
May2023,doi:10.3390/s23104643.
[27] J. Li, G. Zhang, C. Jiang, and W. Zhang, ‘‘A survey of maritime [44] C.Cheng,W.Chen,Y.Li,Y.Ji,S.Niu,Y.Hou,Q.Guo,andX.Chai,
unmanned search system: Theory, applications and future ‘‘Analysisofearthquakeemergencycommandsystemaccordingtocloud
directions,’’ Ocean Eng., vol. 285, Oct. 2023, Art.no.115359, doi: computingmethods,’’IEEEAccess,vol.9,pp.146970–146983,2021,doi:
10.1016/j.oceaneng.2023.115359. 10.1109/ACCESS.2020.3019833.
91156 VOLUME13,2025

M.M.Alsayyedetal.:ReviewofApplicableTechnologies,RoutingProtocols,Requirements,andArchitecture
[45] H.Fesenko,O.Illiashenko,V.Kharchenko,I.Kliushnikov,O.Morozova, [64] U. Aliyu, H. Takruri, M. Hope, A. H. Gidado, and H. A. Adamu,
A. Sachenko, and S. Skorobohatko, ‘‘Flying sensor and edge network- ‘‘Disaster scenario optimised link state routing protocol and message
basedadvancedairmobilitysystems:Reliabilityanalysisandapplications prioritisation,’’IETNetw.,vol.13,nos.5–6,pp.395–412,Sep.2024,doi:
for urban monitoring,’’ Drones, vol. 7, no. 7, p.409, Jun. 2023, doi: 10.1049/ntw2.12125.
10.3390/drones7070409. [65] J. P. J. Peixoto, J. C. N. Bittencourt, T. C. Jesus, D.G.Costa,
[46] A. E. C. Redondi, C. Innamorati, S. Gallucci, S. Fiocchi, and P.Portugal, and F. Vasques, ‘‘Exploiting geospatial data of con-
F. Matera, ‘‘A survey on future millimeter-wave communication nectivity and urban infrastructure for efficient positioning of emer-
applications,’’ IEEE Access, vol. 12, pp.133165–133182, 2024, doi: gency detection units in smart cities,’’ Comput., Environ. Urban Syst.,
10.1109/access.2024.3438625. vol.107,Jan.2024,Art.no.102054,doi:10.1016/j.compenvurbsys.2023.
[47] C.InduandK.Vipin,‘‘3Ddeploymentofmulti-UAVnetworkindisaster 102054.
zones to achieve coverage and connectivity,’’ in Proc. Int. Conf. Cog- [66] Q. Xiao, J. Zhao, S. Feng, G. Li, and A. Hu, ‘‘Securing NextG net-
nit. Robot. Intell. Syst. (ICC - ROBINS), Apr. 2024, pp.715–722, doi: workswithphysical-layerkeygeneration:Asurvey,’’Secur.Saf.,vol.3,
10.1109/icc-robins60238.2024.10534020. Jan.2024,Art.no.2023021,doi:10.1051/sands/2023021.
[48] M. R. Rezaee, N. A. W. A. Hamid, M. Hussin, and Z. A. Zukarnain, [67] H. Li, J. Sun, and X. Ke, ‘‘AI-driven optimization system for
‘‘Comprehensive review of drones collision avoidance schemes: Chal- large-scale Kubernetes clusters: Enhancing cloud infrastructure avail-
lengesandopenissues,’’IEEETrans.Intell.Transp.Syst.,vol.25,no.7, ability, security, and disaster recovery,’’ J. Artif. Intell. Gen. Sci.
pp.6397–6426,Jul.2024,doi:10.1109/TITS.2024.3375893. (JAIGS), vol. 2, no. 1, pp.281–306, Feb. 2024. [Online]. Available:
[49] I.ChandranandK.Vipin,‘‘Multi-UAVnetworksfordisastermonitoring: https://ojs.boulibrary.com/index.php/JAIGS
Challengesandopportunitiesfromanetworkperspective,’’DroneSyst. [68] M. G. Spina, M. Tropea, and F. De Rango, ‘‘SURA-LB: Software-
Appl.,vol.12,pp.1–28,Jan.2024,doi:10.1139/dsa-2023-0079. definedIDSwithUAVresourceawareload-balancinginFANETdisaster
[50] C.Gruffeille,A.Perrusquía,A.Tsourdos,andW.Guo,‘‘Disasterarea scenarios,’’ Comput. Commun., vol. 223, pp.101–114, Jul. 2024, doi:
coverageoptimisationusingreinforcementlearning,’’inProc.Int.Conf. 10.1016/j.comcom.2024.05.015.
UnmannedAircr.Syst.(ICUAS),Jun.2024,pp.61–67. [69] R.Gao,S.Jing,M.Li,Y.Sun,G.Si,andY.Zhang,‘‘Researchonhealth
[51] M.S.Adam,R.Nordin,N.F.Abdullah,A.Abu-Samah,O.A.Amodu, evaluationmethodofdatacentersecurityprotectionsystem,’’Proc.SPIE,
andM.H.Alsharif,‘‘Optimizingdisasterresponsethroughefficientpath vol.13175,p.72,Jun.2024,doi:10.1117/12.3032059.
planningofmobileaerialbasestationwithgeneticalgorithm,’’Drones, [70] K. P. Kumar, B. R. Prathap, M. M. Thiruthuvanathan, H. Murthy, and
vol.8,no.6,p.272,Jun.2024,doi:10.3390/drones8060272. V.J.Pillai,‘‘Secureapproachtosharingdigitizedmedicaldatainacloud
[52] H.Lin,M.A.Kishk,andM.-S.Alouini,‘‘Virtualbackhaulconnectivityfor environment,’’DataSci.Manage.,vol.7,no.2,pp.108–118,Jun.2024,
enhancedcoverageinfiber-lessareas,’’IEEEWirelessCommun.,vol.31, doi:10.1016/j.dsm.2023.12.001.
no.4,pp.324–330,Aug.2024,doi:10.1109/MWC.012.2300371. [71] V. Cheimaras, S. Papagiakoumos, N. Peladarinos, A. Trigkas,
[53] Y. M. Balakrishna and V. Shivashetty, ‘‘Device-to-device based path P.Papageorgas,D.D.Piromalis,andR.A.Munteanu,‘‘Low-cost,open-
selection for post disaster communication using hybrid intelligence,’’ source, experimental setup communication platform for emergencies,
Int. J. Electr. Comput. Eng., vol. 14, no. 1, p.796, Feb. 2024, doi: based on SD-WAN technology,’’ Telecom, vol. 5, no. 2, pp.347–368,
10.11591/ijece.v14i1.pp796-810. May2024,doi:10.3390/telecom5020018.
[54] F.Kagai,P.Branch,J.But,R.Allen,andM.Rice,‘‘Rapidlydeployable [72] E. Cadet, O. S. Osundare, H. O. Ekpobimi, Z. Samira, and
satellite-basedemergencycommunicationsinfrastructure,’’IEEEAccess, Y.W.Weldegeorgise, ‘‘AI-powered threat detection in surveillance
vol.12,pp.139368–139410,2024,doi:10.1109/access.2024.3465512. systems: A real-time data processing framework,’’ Open Access
[55] A.Alhammadi,A.Abraham,A.Fakhreddine,Y.Tian,J.Du,andF.Bader, Res. J. Eng. Technol., vol. 7, no. 2, pp.31–45, Oct. 2024, doi:
‘‘Envisioningthefutureroleof3Dwirelessnetworksinpreventingand 10.53022/oarjet.2024.7.2.0057.
managingdisastersandemergencysituations,’’2024,arXiv:2402.10600. [73] M. Rihan, D. Wübben, A. Bhattacharya, M. Petrova, X. Yuan,
[56] G. Sun, L. He, Z. Sun, Q. Wu, S. Liang, J. Li, D. Niyato, and A. Schmeink, and A. Fellan, ‘‘Unified 3D networks: Architecture,
V.C.M.Leung,‘‘Jointtaskoffloadingandresourceallocationinaerial- challenges, recent results, and future opportunities,’’ IEEE Open J.
terrestrialUAVnetworkswithedgeandfogcomputingforpost-disaster Veh. Technol., vol. 6, pp.170–201, 2024, doi: 10.1109/OJCOMS.2024.
rescue,’’ IEEE Trans. Mobile Comput., vol. 23, no. 9, pp.8582–8600, 011100.
Sep.2024. [74] O.DeborahSegun-Falade,O.SojiOsundare,W.EdgarKedi,P.Azuka
[57] A.Samarakkody,D.Amaratunga,andR.Haigh,‘‘Technologicalinnova- Okeleke, T. Ignatius Ijomah, and O. Yetunde Abdul-Azeez, ‘‘Develop-
tionsforenhancingdisasterresilienceinsmartcities:Acomprehensive ingcrossplatformsoftwareapplicationstoenhancecompatibilityacross
urban scholar’s analysis,’’ Sustainability, vol. 15, no. 15, p.12036, devicesandsystems,’’Comput.Sci.ITRes.J.,vol.5,no.8,pp.2040–2061,
Aug.2023,doi:10.3390/su151512036. Aug.2024,doi:10.51594/csitrj.v5i8.1491.
[58] S.H.Alsamhi,F.A.Almalki,H.Al-Dois,A.V.Shvetsov,M.S.Ansari, [75] S.Hafeez,R.Cheng,L.Mohjazi,Y.Sun,andM.AliImran,‘‘Blockchain-
A.Hawbani,S.K.Gupta,andB.Lee,‘‘Multi-droneedgeintelligenceand enhancedUAVnetworksforpost-disastercommunication:Adecentralized
SAR smart wearable devices for emergency communication,’’ Wireless flockingapproach,’’2024,arXiv:2403.04796.
Commun.MobileComput.,vol.2021,no.1,Jan.2021,Art.no.6710074, [76] C.-W.Liang,Y.-L.Wu,C.-Y.Shi,S.-M.Lu,andH.-C.Lee,‘‘Evaluation
doi:10.1155/2021/6710074. of a LoRA mesh wireless networking system supporting time-critical
[59] W.Feng,Y.Wang,Y.Chen,N.Ge,andC.-X.Wang,‘‘Structuredsatellite- transmission and data lost recovery,’’ in Proc. 18th Int. Conf. Inf.
UAV-terrestrialnetworksfor6GInternetofThings,’’IEEENetw.,vol.38, Process. Sensor Netw., Apr. 2019, pp.317–318, doi: 10.1145/3302506.
no.4,pp.48–54,Jul.2024,doi:10.1109/MNET.2024.3380052. 3312607.
[60] O.Ledesma,P.Lamo,andJ.A.Fraire,‘‘TrendsinLPWANtechnologies [77] B. Black, J. Rafferty, J. Santos, A. Ennis, P. Perry, and M. McKee,
forLEOsatelliteconstellationsintheNewSpacecontext,’’Electronics, ‘‘Bluetooth5.0suitabilityassessmentforemergencyresponsewithinfire
vol.13,no.3,p.579,Jan.2024,doi:10.3390/electronics13030579. environments,’’ Electronics, vol. 12, no. 22, p.4599, Nov. 2023, doi:
[61] Y. Zhang, Y. Hong, M. Guizani, S. Wu, P. Zhang, and R. Liu, 10.3390/electronics12224599.
‘‘A multi-layer information dissemination model and interference opti- [78] R.Iqbal,A.Kashif,O.Alharbi,S.Zafar,A.Aljaedi,andY.Qasaymeh,
mizationstrategyforcommunicationnetworksindisasterareas,’’IEEE ‘‘Robustness in mesh networks using connected safe set and
Trans. Veh. Technol., vol. 73, no. 1, pp.1239–1252, Jan. 2024, doi: applications,’’ IEEE Access, vol. 12, pp.18021–18027, 2024, doi:
10.1109/TVT.2023.3304707. 10.1109/ACCESS.2024.3357623.
[62] K.Demir,V.Tumen,S.Kosunalp,andT.Iliev,‘‘Adeepreinforcement [79] A.ChapnevisandE.Bulut,‘‘UAVmeshnetworktrajectoryplanningfor
learningalgorithmfortrajectoryplanningofswarmUAVfulfillingwildfire age optimal data collection in infrastructureless areas,’’ in Proc. IEEE
reconnaissance,’’ Electronics, vol. 13, no. 13, p.2568, Jun. 2024, doi: Int.Conf.Commun.,Jun.2024,pp.1563–1568.
10.3390/electronics13132568. [80] M.Tham,Y.J.Wong,B.-H.Kwan,X.H.Ng,andY.Owada,‘‘Artifi-
[63] M. A. Soomro, M. I. Channa, S. Z. Nizamani, M. A. Bhutto, and cialintelligenceofthings(AIoT)fordisastermonitoringusingwireless
A.A.Ghoto, ‘‘Distance and energy aware DEAODV routing protocol mesh network,’’ in Proc. 6th Int. Conf. Softw. Eng. Inf. Manage.
in disastrous situation,’’ VAWKUM Trans. Comput. Sci., vol. 12, no. 2, (ICSIM),PalmerstonNorth,NewZealand,Jan.2023,pp.234–239,doi:
pp.137–148,Nov.2024,doi:10.21015/vtcs.v12i2.1977. 10.1145/3584871.3584905.
VOLUME13,2025 91157

M.M.Alsayyedetal.:ReviewofApplicableTechnologies,RoutingProtocols,Requirements,andArchitecture
[81] D.Thaha,M.V.Lakshmi,S.Swathi,S.A.Sabatini,andT.Manikandan, [99] R.Rukaiya,S.A.Khan,M.U.Farooq,andI.Matloob,‘‘Communication
‘‘MANETbasedintegratedsensorsystemfordisasterdetectionandcom- architectureandoperationsforSDR-enabledUAVsnetworkindisaster-
municationinhazardousenvironments,’’Nanotechnology,vol.20,no.S7, stressedareas,’’AdHocNetw.,vol.160,Jul.2024,Art.no.103506,doi:
pp.82–92,2024.[Online].Available:http://www.nano-ntp.com 10.1016/j.adhoc.2024.103506.
[82] J.Höchst,L.Baumgärtner,F.Kuntke,A.Penning,A.Sterz,M.Sommer, [100] S.He,X.Tan,Y.Zhong,M.Huang,Z.Mei,Y.Wan,andH.Wang,‘‘Evo-
and B. Freisleben, ‘‘Mobile device-to-device communication for crisis lutionaryPSO-basedemergencymonitoringgeospatialedgeservicechain
scenariosusinglow-costLoRAmodems,’’inDisasterManagementand intheemergencycommunicationnetwork,’’Int.J.Digit.Earth,vol.16,
InformationTechnology(PublicAdministrationandInformationTechnol- no.1,pp.2797–2817,Oct.2023,doi:10.1080/17538947.2023.2239765.
ogy),vol.40.Cham,Switzerland:Springer,Jan.2023,pp.235–268,doi: [101] A.Saif,K.Dimyati,K.A.Noordin,N.A.Mosali,andS.H.Alsamhi,
10.1007/978-3-031-20939-0_12. ‘‘Skyward bound: Empowering disaster resilience with multi-UAV-
[83] N.Verma,M.Varshney,andN.Verma,‘‘RoleofMANETandartiicialbee
|     |     |     |     |     |     |     |     | assisted | B5G networks |     | for enhanced | connectivity |     | and energy effi- |
| --- | --- | --- | --- | --- | --- | --- | --- | -------- | ------------ | --- | ------------ | ------------ | --- | ---------------- |
colony(ABC)algorithmtomakesmartcampusmodel,withsmartsen- ciency,’’ Internet Things, vol. 23, Oct. 2023, Art.no.100885, doi:
sors,’’Res.Square,vol.2023,pp.1–19,Jun.2023,doi:10.21203/rs.3.rs- 10.1016/j.iot.2023.100885.
3075962/v1. [102] M.B.Adityawan,A.K.Nurendyastuti,M.R.Purnama,M.S.Arifianto,
[84] A. Abu Salem, ‘‘An effective management model for data caching M.Farid,A.A.Kuntoro,andWidyaningtias,‘‘Developmentofatsunami
| in MANET |     | environment,’’ | Int. | Arab J. | Inf. Technol., | vol. | 20, no. 6, |               |        |     |           |               |     |                   |
| -------- | --- | -------------- | ---- | ------- | -------------- | ---- | ---------- | ------------- | ------ | --- | --------- | ------------- | --- | ----------------- |
|          |     |                |      |         |                |      |            | early warning | system | on  | the coast | of Palu based | on  | maritime wireless |
pp.841–851,Nov.2023,doi:10.34028/iajit/20/6/1. communication,’’Prog.DisasterSci.,vol.19,Oct.2023,Art.no.100290,
[85] I.Ambika,S.Bhatia,S.Basheer,andP.Dadheech,‘‘Optimizedresource doi:10.1016/j.pdisas.2023.100290.
allocation and queue management for traffic control in MANET,’’ [103] A.K.Nurendyastuti,M.B.Adityawan,M.Rizki,M.S.A.Purnama,
Comput. Syst. Sci. Eng., vol. 45, no. 2, pp.1323–1342, 2023, doi: M. Farid, and A. A. Kuntoro, ‘‘A new approach for a tsunami early
10.32604/csse.2023.030786.
warningsystembasedonmaritimewirelesscommunication,casestudy,
[86] S. K. A. S. Syed Wajahat Abbas Rizvi, ‘‘Enhancing MANET perfor- pangandaran,Indonesia,’’J.Appl.Sci.Eng.,vol.17,no.4,pp.2285–2294,
mance:Anovelapproachthroughnature-inspiredschedulingalgorithms,’’ 2023,doi:10.6180/jase.202404_27(4).0007.
J.Electr.Syst.,vol.20,no.3s,pp.2030–2038,Mar.2024. [104] X. Li and S. Jiang, ‘‘Deployment method for aircraft-based maritime
[87] S. Halder, S. Roy, P. Ghosh, and N. Ghosh, ‘‘ADRIN2.0: Enabling emergency communication resource reserve bases,’’ J. Mar. Sci. Eng.,
post-disaster communication through adaptive mobility-informed vol.12,no.5,p.844,May2024,doi:10.3390/jmse12050844.
| routing,’’ | IEEE | Access, | vol. | 12, pp.102368–102380, |     |     | 2024, doi: |                   |     |             |     |            |       |                |
| ---------- | ---- | ------- | ---- | --------------------- | --- | --- | ---------- | ----------------- | --- | ----------- | --- | ---------- | ----- | -------------- |
|            |      |         |      |                       |     |     |            | [105] B. Karaman, |     | I. Basturk, | S.  | Taskin, F. | Kara, | E. Zeydan, and |
10.1109/ACCESS.2024.3432866. H. Yanikomeroglu, ‘‘Enhancing resiliency of integrated space-air
[88] M.Awais,Y.Saeed,A.Ali,S.Jabbar,A.Ahmad,Y.Alkhrijah,U.Raza, ground-seanetworkswithrenewableenergies:Ausecaseafterthe2023
andY.Saleem,‘‘Deeplearningbasedenhancedsecureemergencyvideo türkiyeearthquake,’’IEEECommun.Mag.,vol.62,no.12,pp.104–111,
streaming approach by leveraging blockchain technology for vehicular Dec. 2024. [Online]. Available: https://blog.cloudflare.com/q1-2023-
AdHoc 5G networks,’’ J. Cloud Comput., vol. 13, no. 1, Aug. 2024, internet-disruption-summary/
Art.no.130,doi:10.1186/s13677-024-00665-1. [106] M. Ifeanyi Akazue, A. Efetobore Edje, M. D. Okpor, W. Adigwe,
[89] W.Ahmad,G.Husnain,S.Ahmed,F.Aadil,andS.Lim,‘‘Receivedsignal P. O. Ejeh, C. C. Odiakaose, A. A. Ojugo, E. B. Edim, R. E. Ako,
strength-based localization for vehicle distance estimation in vehicular andV.O.Geteloma,‘‘FiMoDeAL:Pilotstudyonshortestpathheuris-
ad hoc networks (VANETs),’’ J. Sensors, vol. 2023, no. 1, Jan. 2023, tics in wireless sensor network for fire detection and alert ensemble,’’
Art.no.7826992,doi:10.1155/2023/7826992. Bull.Electr.Eng.Informat.,vol.13,no.5,pp.3534–3543,Oct.2024,doi:
[90] H.Idoudi,M.Ameli,C.NguyenVanPhu,M.Zargayouna,andA.Rachedi, 10.11591/eei.v13i5.8084.
‘‘Smart dynamic evacuation planning and online management using [107] L.Ye,Y.Yang,W.Meng,X.Wu,X.Li,andR.Zhu,‘‘Offlineandonline
vehicularcommunicationsystem,’’Comput.-AidedCivilInfrastruct.Eng., taskallocationalgorithmsformultipleUAVsinwirelesssensornetworks,’’
vol.39,no.10,pp.1452–1468,May2024,doi:10.1111/mice.13148. EURASIPJ.Adv.SignalProcess.,vol.2024,no.1,Feb.2024,Art.no.21,
| [91] R. Ali, | R. Liu, | A. Nayyar, | I.  | Waris, L. | Li, and | M. A. Shah, | ‘‘Intel- |     |     |     |     |     |     |     |
| ------------ | ------- | ---------- | --- | --------- | ------- | ----------- | -------- | --- | --- | --- | --- | --- | --- | --- |
doi:10.1186/s13634-024-01116-4.
ligent driver model-based vehicular ad hoc network communication in [108] T. Jabeen, I. Jabeen, H. Ashraf, N. Z. Jhanjhi, A. Yassine, and
real-timeusing5Gnewradiowirelessnetworks,’’IEEEAccess,vol.11, M. S. Hossain, ‘‘An intelligent healthcare system using IoT in wire-
pp.4956–4971,2023,doi:10.1109/ACCESS.2023.3234964. lesssensornetwork,’’Sensors,vol.23,no.11,p.5055,May2023,doi:
10.3390/s23115055.
| [92] J. Qi, | N. Zheng, | M.  | Xu, P. Chen, | and | W. Li, ‘‘A | hybrid-trust-based |     |     |     |     |     |     |     |     |
| ----------- | --------- | --- | ------------ | --- | ---------- | ------------------ | --- | --- | --- | --- | --- | --- | --- | --- |
emergency message dissemination model for vehicular ad hoc net- [109] K. K. Paidipati, C. Kurangi, A. S. K. Reddy, G. Kadiravan, and
works,’’ J. Inf. Secur. Appl., vol. 81, Mar. 2024, Art.no.103699, doi: N.H.Shah,‘‘Wirelesssensornetworkassistedautomatedforestfiredetec-
10.1016/j.jisa.2024.103699. tionusingdeeplearningandcomputervisionmodel,’’MultimediaTools
Appl.,vol.83,no.9,pp.26733–26750,Sep.2023,doi:10.1007/s11042-
| [93] B. Bhabani |     | and J. | Mahapatro, | ‘‘CluRMA: | A   | cluster-based | RSU- |     |     |     |     |     |     |     |
| --------------- | --- | ------ | ---------- | --------- | --- | ------------- | ---- | --- | --- | --- | --- | --- | --- | --- |
023-16647-5.
| enabled | message |     | aggregation | scheme | for | vehicular | ad hoc |     |     |     |     |     |     |     |
| ------- | ------- | --- | ----------- | ------ | --- | --------- | ------ | --- | --- | --- | --- | --- | --- | --- |
networks,’’ Veh. Commun., vol. 39, Feb. 2023, Art.no.100564, doi: [110] H. Frikha, F. Kamoun-Abid, A. Meddeb-Makhoulf, and F. Zarai,
10.1016/j.vehcom.2022.100564. ‘‘AsmartemergencyresponsesystembasedondeeplearningandKalman
filter:ThecaseofCOVID-19,’’IndonesianJ.Electr.Eng.Comput.Sci.,
| [94] M. R. | Devi, | I. J. S. | Jeya, and | S. Lokesh, | ‘‘Adaptive | scheduled | par- |     |     |     |     |     |     |     |
| ---------- | ----- | -------- | --------- | ---------- | ---------- | --------- | ---- | --- | --- | --- | --- | --- | --- | --- |
vol.34,no.1,p.630,Apr.2024,doi:10.11591/ijeecs.v34.i1.pp630-640.
| titioning | technique | for | reliable | emergency | message | broadcasting | in  |                |        |     |            |           |           |             |
| --------- | --------- | --- | -------- | --------- | ------- | ------------ | --- | -------------- | ------ | --- | ---------- | --------- | --------- | ----------- |
|           |           |     |          |           |         |              |     | [111] M. Yaser | Yagan, | S.  | Kayraklik, | S. Kesir, | G. Sumen, | I. Hokelek, |
VANETforintelligenttransportationsystems,’’Automatika,vol.64,no.2,
M.Basaran,G.C.Alexandropoulos,E.Basar,C.Cavdar,H.Arslan,and
pp.341–354,Apr.2023,doi:10.1080/00051144.2022.2140392.
[95] D.Desai,H.El-Ocla,andS.Purohit,‘‘DatadisseminationinVANETs A.Gorcin,‘‘Fastnetworkrecoveryfromlarge-scaledisasters:Aresilient
andself-organizingRANframework,’’2024,arXiv:2408.08609.
| using | particle | swarm | optimization,’’ | Sensors, | vol. | 23, no. | 4, p.2124, |          |             |       |          |              |     |                  |
| ----- | -------- | ----- | --------------- | -------- | ---- | ------- | ---------- | -------- | ----------- | ----- | -------- | ------------ | --- | ---------------- |
|       |          |       |                 |          |      |         |            | [112] M. | Batistatos, | M.-A. | Kourtis, | G. Xilouris, |     | D. Santorinaios, |
Feb.2023,doi:10.3390/s23042124.
A.Oikonomakis,E.-Z.Bozis,andA.Kourtis,‘‘Wi-Fi6aerialrelaynodein
| [96] M. | A. Abdel-Malek |     | and M. | Azab, | ‘‘UAV-fleet | management | for |     |     |     |     |     |     |     |
| ------- | -------------- | --- | ------ | ----- | ----------- | ---------- | --- | --- | --- | --- | --- | --- | --- | --- |
5Gnetworkforemergencyoperations,’’AEU-Int.J.Electron.Commun.,
extended NextG emergency support infrastructure with QoS and cost vol.170,Oct.2023,Art.no.154776,doi:10.1016/j.aeue.2023.154776.
| aware,’’ | Internet | Things, | vol. | 25, Apr. | 2024, Art.no.101043, |     | doi: |                |     |        |        |                   |          |          |
| -------- | -------- | ------- | ---- | -------- | -------------------- | --- | ---- | -------------- | --- | ------ | ------ | ----------------- | -------- | -------- |
|          |          |         |      |          |                      |     |      | [113] K. Chen, | L.  | Zhang, | and J. | Zhong, ‘‘Vertical | handover | strategy |
10.1016/j.iot.2023.101043.
|     |     |     |     |     |     |     |     | in satellite-aerial |     | based | emergency | communication |     | networks,’’ in |
| --- | --- | --- | --- | --- | --- | --- | --- | ------------------- | --- | ----- | --------- | ------------- | --- | -------------- |
[97] Y.Zeng,X.Tan,M.Sha,Z.KhadimHussain,T.Lin,J.Tu,H.Wang,B.Liu,
|     |     |     |     |     |     |     |     | Proc. | 11th Int. | Conf. | Wireless | Netw. Mobile, | vol. | 46, Jul. 2024, |
| --- | --- | --- | --- | --- | --- | --- | --- | ----- | --------- | ----- | -------- | ------------- | ---- | -------------- |
C.Li,F.Huang,andZ.Sha,‘‘ThestudyofDDPGbasedspatiotemporal pp.1–6.[Online].Available:https://eprints.whiterose.ac.uk/
dynamicdeploymentoptimizationofair-groundadhocnetworkfordis- [114] G. Potutan and K. Suzuki, ‘‘Addressing early warning challenges
asteremergencyresponse,’’Int.J.Appl.EarthObserv.Geoinformation,
|     |     |     |     |     |     |     |     | using | satellites | to improve | emergency | evacuation,’’ |     | Emergency Man- |
| --- | --- | --- | --- | --- | --- | --- | --- | ----- | ---------- | ---------- | --------- | ------------- | --- | -------------- |
vol.128,Apr.2024,Art.no.103708,doi:10.1016/j.jag.2024.103708.
age.Sci.Technol.,vol.3,no.1,pp.1–10,2023,doi:10.48130/emst-2023-
| [98] A. F. | M. S. | Shah, M. | A. Karabulut, | and | K. Rabie, | ‘‘Improvement | of  | 0004. |     |     |     |     |     |     |
| ---------- | ----- | -------- | ------------- | --- | --------- | ------------- | --- | ----- | --- | --- | --- | --- | --- | --- |
emergencycommunicationsystemsusingdronesin5Gandbeyondfor [115] K.PatilandB.Desai,‘‘Fromremoteoutbacktourbanjungle:Achieving
safetyapplications,’’inProc.IEEEFutureNetw.WorldForum(FNWF), universal 6G connectivity through hybrid terrestrial-aerial-satellite net-
Nov.2023,pp.1–6.
works,’’Adv.Comput.Sci.,vol.6,no.1,pp.1–13,2023.
| 91158 |     |     |     |     |     |     |     |     |     |     |     |     |     | VOLUME13,2025 |
| ----- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ------------- |

M.M.Alsayyedetal.:ReviewofApplicableTechnologies,RoutingProtocols,Requirements,andArchitecture
[116] Y.Gong,H.Yao,andA.Nallanathan,‘‘Intelligentsensing,communica- [135] C.LiewandM.Radenkovic,‘‘Exploringopportunisticroutingforremote
tion,computation,andcachingforsatellite-groundintegratednetworks,’’ seaemergencies,’’2024,arXiv:2404.03013.
IEEENetw.,vol.38,no.4,pp.9–16,Jul.2024. [136] A.JalaTirtaSegaraandA.D.Ramadhani,‘‘Performanceanalysisof
[117] Y. Gong, D. Yu, X. Cheng, C. Yuen, M. Bennis, and M. Debbah, mobilead-hocnetworksbasedonTCPandUDPtrafficonAODVprotocol
‘‘Computationoffloadingandquantizationschemesforfederatedsatellite- for warship communication,’’ J. Syst. Eng. Inf. Technol., vol. 2, no. 2,
groundgraphnetworks,’’IEEETrans.WirelessCommun.,vol.23,no.10, pp.53–58,Sep.2023,doi:10.29207/joseit.v2i2.5343.
pp.14140–14154,Oct.2024,doi:10.1109/twc.2024.3409691. [137] S.Daousis,N.Peladarinos,V.Cheimaras,P.Papageorgas,D.D.Piroma-
[118] J.He,N.Cheng,Z.Yin,C.Zhou,H.Zhou,W.Quan,andX.-H.Lin, lis,andR.A.Munteanu,‘‘Overviewofprotocolsandstandardsforwireless
‘‘Service-orientednetworkresourceorchestrationinspace-air-groundinte- sensornetworksincriticalinfrastructures,’’FutureInternet,vol.16,no.1,
gratednetwork,’’IEEETrans.Veh.Technol.,vol.73,no.1,pp.1162–1174, p.33,Jan.2024,doi:10.3390/fi16010033.
Jan.2024,doi:10.1109/TVT.2023.3301676. [138] K.K.Almuzaini,S.Joshi,S.Ojo,M.Aggarwal,P.Suman,P.K.Pareek,
[119] Y.Jahir,M.Atiquzzaman,H.Refai,A.Paranjothi,andP.G.LoPresti, and P. K. Shukla, ‘‘Optimization of the operational state’s routing
‘‘Routing protocols and architecture for disaster area network: for mobile wireless sensor networks,’’ Wireless Netw., vol. 30, no. 6,
A survey,’’ Ad Hoc Netw., vol. 82, pp.1–14, Jan. 2019, doi: pp.5247–5261,Aug.2024,doi:10.1007/s11276-023-03246-3.
10.1016/j.adhoc.2018.08.005. [139] O. I. Akinola, ‘‘Adaptive location-based routing protocols for
[120] R. Dhall and S. Dhongdi, ‘‘Review of protocol stack develop- dynamic wireless sensor networks in urban cyber-physical systems,’’
ment of flying ad-hoc networks for disaster monitoring applications,’’ J. Eng. Res. Rep., vol. 26, no. 7, pp.424–443, Jul. 2024, doi:
Arch.Comput.MethodsEng.,vol.30,no.1,pp.37–68,Jan.2023,doi: 10.9734/jerr/2024/v26i71220.
10.1007/s11831-022-09791-y. [140] M. C. Pognon, A. Quintero, and S. Pierre, ‘‘Adaptive priority
[121] A. Haghrah, M. P. Abdollahi, H. Azarhava, and J. M. Niya, ‘‘A sur- scheduling of Internet of Things data for disaster management in
veyonthehandovermanagementin5G-NRcellularnetworks:Aspects, smart cities,’’ IEEE Access, vol. 12, pp.83285–83298, 2024, doi:
approaches and challenges,’’ EURASIP J. Wireless Commun. Netw., 10.1109/ACCESS.2024.3407672.
vol.2023,no.1,Jun.2023,doi:10.1186/s13638-023-02261-4. [141] H.L.Gururaj,R.Natarajan,N.A.Almujally,F.Flammini,S.Krishna,
[122] A. M. Soomro, A. B. Naeem, B. Senapati, K. Bashir, S.Pradhan, and S. K. Gupta, ‘‘Collaborative energy-efficient routing protocol
M. I. Ghafoor, and H. A. Sakr, ‘‘In MANET: An improved for sustainable communication in 5G/6G wireless sensor networks,’’
hybrid routing approach for disaster management,’’ in Proc. IEEE IEEE Open J. Commun. Soc., vol. 4, pp.2050–2061, 2023, doi:
Int. Conf. Emerg. Trends Eng., Sci. Technol. (ICES&T), Jan. 2023, 10.1109/OJCOMS.2023.3312155.
pp.1–6,doi:10.1109/ICEST56843.2023.10138831. [142] D.Abada,R.Adrdor,O.Boutkhoum,andA.Bohouch,‘‘Anefficient
[123] H.A.AhmedandH.A.A.Al-Asadi,‘‘Anoptimizedlinkstaterouting mobilegatewayselectionanddiscoverybased-routingprotocolinhetero-
protocolwithablockchainframeworkforefficientvideo-packettransmis- geneousLTE-VANETnetworks,’’Int.J.Comput.Netw.Commun.,vol.15,
sionandsecurityovermobilead-hocnetworks,’’J.SensorActuatorNetw., no.2,pp.57–79,Mar.2023,doi:10.5121/ijcnc.2023.15204.
vol.13,no.2,p.22,Mar.2024,doi:10.3390/jsan13020022. [143] J. S. Alrubaye and B. S. Ghahfarokhi, ‘‘Geo-based resource allo-
[124] C. Edwin Singh, S. Sharon Priya, B. Muthu Kumar, K. Saravanan, cation for joint clustered V2I and V2V communications in cellu-
A.Neelima,andB.Gireesha,‘‘Trustawarefuzzyclusteringbasedreliable lar networks,’’ IEEE Access, vol. 11, pp.82601–82612, 2023, doi:
routinginmanet,’’Meas.,Sensors,vol.33,Jun.2024,Art.no.101142,doi: 10.1109/ACCESS.2023.3300294.
10.1016/j.measen.2024.101142. [144] B.Yamansavascilar,A.Ozgovde,andC.Ersoy,‘‘Aircomputing:Asurvey
[125] A. Kumari, ‘‘AGDT: A mathematical model of hybrid algorithm onanewgenerationcomputationparadigm,’’Comput.Netw.,vol.251,
for efficient routing in MANETs using dynamic thresholds,’’ Com- Sep.2024,Art.no.110653,doi:10.1016/j.comnet.2024.110653.
mun.Appl.NonlinearAnal.,vol.31,no.2s,pp.72–83,May2024. [145] R. Wang, M. A. Kishk, and M.-S. Alouini, ‘‘Reliability analy-
[126] S. Benzerogue, S. Abdelatif, S. Merniz, S. Harous, and L. Khamer, sis of multi-hop routing in multi-tier LEO satellite networks,’’ IEEE
‘‘Multi-pathtransmissionprotocolforvideostreamingovervehicularfog Trans.WirelessCommun.,vol.23,no.3,pp.1959–1973,Mar.2024,doi:
computingenvironments,’’IEEEAccess,vol.12,pp.87199–87216,2024, 10.1109/TWC.2023.3293467.
doi:10.1109/ACCESS.2024.3417288. [146] Y.Lyu,H.Hu,R.Fan,Z.Liu,J.An,andS.Mao,‘‘Dynamicrouting
[127] B. Su and L. Tong, ‘‘Transmission protocol of emergency messages forintegratedsatellite-terrestrialnetworks:Aconstrainedmulti-agentrein-
in VANET based on the trust level of nodes,’’ IEEE Access, vol. 11, forcementlearningapproach,’’IEEEJ.Sel.AreasCommun.,vol.42,no.5,
pp.68243–68256,2023,doi:10.1109/ACCESS.2023.3292234. pp.1204–1218,May2024.
[128] M.A.Albeyar,I.Smaoui,H.Mnif,andS.Alani,‘‘Proposedsupercluster- [147] Z. Xu, W. Quan, N. Cheng, M. Liu, J. Deng, L. Han, and D. Gao,
basedUMBBFSroutingprotocolforemergencymessagedisseminationin ‘‘RP-ER:RelativepositionbasedefficientroutingmechanismforLEO
edge-RSUfor5GVANET,’’Computers,vol.13,no.8,p.208,Aug.2024, satellite network,’’ in Proc. IEEE Global Commun. Conf., Dec. 2023,
doi:10.3390/computers13080208. pp.5967–5972,doi:10.1109/GLOBECOM54140.2023.10437726.
[129] S.Saha,V.V.Kumar,V.R.Niveditha,V.A.Kannan,K.Gunasekaran,
andK.Venkatesan,‘‘Cluster-basedprotocolforprioritizedmessagecom-
municationinVANET,’’IEEEAccess,vol.11,pp.67434–67442,2023,
doi:10.1109/ACCESS.2023.3286936.
[130] N. Hassan, X. Fernando, and I. Woungang, ‘‘An emergency message
routingprotocolforimprovedcongestionmanagementinhybridRF/VLC
VANETs,’’Telecom,vol.5,no.1,pp.21–47,Dec.2023,doi:10.3390/tele-
com5010002. MOHAMMADM.ALSAYYEDreceivedthemas-
[131] V. Krishnakumar and R. Asokan, ‘‘Geographic drone-based ter’s degree in computer science from Al Balqa
route optimization approach for emergency area ad-hoc network,’’ Applied University, where their thesis exam-
Comput. Syst. Sci. Eng., vol. 45, no. 1, pp.985–1000, 2023, doi: inedthecryptosystemdesignbasedonHermitian
10.32604/csse.2023.029189. curves,amoderncryptographicmethoddesigned
[132] M. Hosseinzadeh, S. Ali, A. H. Mohammed, J. Lansky, S. Mildeova, toprotectinformationresourcesandensurerobust
M. S. Yousefpoor, E. Yousefpoor, O. Hassan Ahmed, A. M. Rahmani,
protection against compromises. He is currently
andA.Mehmood,‘‘Anenergy-awareroutingschemebasedonavirtual
pursuing the Ph.D. degree in cybersecurity with
relay tunnel in flying ad hoc networks,’’ Alexandria Eng. J., vol. 91,
UniversitiSainsMalaysia,concentratingonsecu-
pp.249–260,Mar.2024,doi:10.1016/j.aej.2024.02.006.
rity for mobile ad hoc networks and emergency
[133] J.Tang,Z.Zhou,W.Feng,andK.K.Wong,‘‘Adistributedandadaptive
routingprotocolforUAV-aidedemergencynetworks,’’inProc.IEEE98th communication.Hispreviousworkexaminestheimplementationofalge-
Veh.Technol.Conf.(VTC-Fall),Oct.2023,pp.1–6. braic algorithm cryptography based on an error correction code. Beyond
[134] S.Liu,L.Zhu,F.Huang,A.Hassan,D.Wang,andY.He,‘‘Asurveyon academia,hehasactivelyengagedincollaborativeprojectsandinterdisci-
Air-to-SeaintegratedmaritimeInternetofThings:Enablingtechnologies, plinaryresearchtotranslatetheoreticalinsightsintopracticalapplications.
applications,andfuturechallenges,’’J.Mar.Sci.Eng.,vol.12,no.1,p.11, Hisresearchinterestsincludetheissueofsecurecommunicationinintelli-
Dec.2023,doi:10.3390/jmse12010011. gentsystems,disasterareanetworks,andalgebraicalgorithmcryptography.
VOLUME13,2025 91159

M.M.Alsayyedetal.:ReviewofApplicableTechnologies,RoutingProtocols,Requirements,andArchitecture
SELVAKUMAR MANICKAM (Member, IEEE) I.DEWAMADEWIDIAwasborninBali,Indone-
is a leading authority in cybersecurity and AI. sia,in1968.Hereceivedthebachelor’sdegreein
HeiscurrentlyaProfessorandtheDirectorofthe electricalengineeringfromUniveristasBrawijaya,
CybersecurityResearchCenter,hehasbeeninstru- Malang,in1991,andthemaster’sdegreeinelectri-
mentalinadvancingsecurityandprivacyresearch. calengineeringfromtheUniversityofIndonesia,
Hiscontributionshavesignificantlyshapedalgo- Jakarta, in 1999. Currently, he is pursuing the
rithms and models that address complex chal- Ph.D.degreewithUniveristasBrawijaya.
lengesincybersecurity.Hispassionliesinforging Beforebecomingalecturer,heworkedatPT.
connections between theory and practice, often INDOSAT, one of the largest cellular network
byintegratingcybersecurityandAItechnologies. operatorsinIndonesia.HestartedjoiningasaLec-
He is equipped with decades of software development expertise, and he turerwithUniveristasBrawijaya,in2016,theInformationTechnologyStudy
alsospearheadscutting-edgeprojectsinAI-drivenautomation,optimizing Program,FacultyofVocationalStudies.ThescopeofworkatPT.INDOSAT
efficiency and safety across diverse sectors, including manufacturing and inthefieldofsubmarinecables,satellites,fiberoptics,andcellularnetworks.
agriculture.Hisworkhascatalyzedsignificantimprovementsinproductivity
and security, showcasing the transformative potential of AI in real-world
applications.Aprolificresearcherandauthor,heconsistentlypublishesin
top-tierjournalsandpresentsatprestigiousconferences.Hehascultivateda
newgenerationofexpertsinthehybridfieldofAIandcybersecurity.His SHANKAR KARUPPAYAH (Member, IEEE)
insights are highly valued by journalists and industry leaders, solidifying received the B.Sc. (Hons.) degree in computer
hisreputationasathoughtleaderincybersecurityandAI.Hisdedication science from Universiti Sains Malaysia (USM),
topushingtheboundariesofknowledgemakeshimaninfluentialfigurein in 2009, the M.Sc. degree in software systems
shapingthefutureofthesecriticalfields. engineering from the King Mongkut’s Univer-
sityofTechnologyNorthBangkok(KMUTNB),
in 2011, and the Ph.D. degree from Technische
UniversitätDarmstadt,Germany,in2016,witha
dissertationtitled‘‘AdvancedMonitoringinP2P
Botnets.’’HeiscurrentlyanAssociateProfessor
andtheDeputyDirectoroftheCybersecurityResearchCentre(CYRES),
Universiti Sains Malaysia. He was previously a Senior Researcher with
EKA RATRI NOOR WULANDARI receivedthe the Telecooperation Group, Technische Universität Darmstadt, and has
bachelor’s degree in chemistry from Universitas workedcloselywiththeNationalResearchCenterforAppliedCybersecurity
BrawijayaMalang,in2010,andthedualmaster’s (ATHENE),formerlyknownasCRISP.Hehasalsocontributedtodisaster
degreefromUniversitasBrawijayaandNational managementtechnologies,particularlyinenhancingtheresilienceandsecu-
CentralUniversity,Taiwan. rityofcommunicationsystemsduringemergencies.Hehasbeeninvolvedin
From2010to2014,shewasaResearchAssis- variousnationalandinternationalresearchprojectsandcollaborations,and
tant with the LCAMIA Research Group, Chem- haspublishedwidelyinreputablejournalsandconferencesinthefieldsof
istry Department, Univeristas Brawijaya. She is cybersecurity,networking,anddistributedcomputing.Hisprimaryresearch
currentlyaLecturerwiththeFacultyofVocational interestsincludethedomainsofcomputerandnetworksecurity,distributed
Studies,UniversitasBrawijaya.Herresearchinter- systems,peer-to-peer(P2P)networks,wirelessmeshnetworks(WMNs),and
estsincludetheappliedchemistryformultipurposeanalysisandintegrated theInternetofThings(IoT)security.
instrumentationforanalysis.
91160 VOLUME13,2025