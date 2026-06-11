applied
sciences
Article
Engineering Method and Tool for the Complete Virtual
Commissioning of Robotic Cells
RobertoRaffaeli1 ,PietroBilancia1,* ,FedericoNeri2,MargheritaPeruzzini3 andMarcelloPellicciari1
1 DepartmentofSciencesandMethodsforEngineering,UniversityofModenaandReggioEmilia,
42122ReggioEmilia,Italy;roberto.raffaeli@unimore.it(R.R.);marcello.pellicciari@unimore.it(M.P.)
2 K-LOOPSS.R.L.,41125Modena,Italy;federico.neri@k-loops.com
3 DepartmentofEngineering“EnzoFerrari”,UniversityofModenaandReggioEmilia,41125Modena,Italy;
margherita.peruzzini@unimore.it
* Correspondence:pietro.bilancia@unimore.it
Abstract:Intelligentroboticmanufacturingcellsmustadapttoever-varyingoperatingconditions,
developingautonomouslyoptimalmanufacturingstrategiestoachievethebestqualityandoverall
productivity. Intelligentandcognitivebehaviorsarerealizedbyusingdistributedcontrollers,in
whichcomplexcontrollogicsmustinteractandprocessawidevarietyofinput/outputsignals.In
particular,programmablelogiccontrollers(PLCs)androbotcontrollersmustbecoordinatedand
integrated.Then,thereistheneedtosimulatetheroboticcells’behaviorforperformanceverification
andoptimizationbyevaluatingtheeffectsofbothPLCandrobotcontrolcodes.Inthiscontext,this
workproposesamethod,anditsimplementationintoanintegratedtool,toexploitthepotentialof
ABBRobotStudiosoftwareasavirtualprototypingplatformforroboticcells,inwhichrealrobots
controlcodesareexecutedonavirtualcontrollerandintegratedwithBeckhoffPLCenvironment.For
thispurpose,aPLCSmartComponentwasconceivedasanextensionofRobotStudiofunctionalities
(cid:1)(cid:2)(cid:3)(cid:1)(cid:4)(cid:5)(cid:6)(cid:7)(cid:8)(cid:1)
(cid:1)(cid:2)(cid:3)(cid:4)(cid:5)(cid:6)(cid:7) toexchangesignalswithaTwinCATinstance.Thenewmoduleallowsthevirtualcommissioningof
Citation:Raffaeli,R.;Bilancia,P.; acompleteroboticcelltobeperformed,assessingthecontrollogicseffectsontheoverallproductivity.
Neri,F.;Peruzzini,M.;Pellicciari,M. Thesolutionisdemonstratedonaroboticassemblycell,showingitsfeasibilityandeffectivenessin
EngineeringMethodandToolforthe optimizingthefinalperformance.
CompleteVirtualCommissioningof
RoboticCells.Appl.Sci.2022,12, Keywords:virtualcommissioning;roboticcell;RobotStudio;virtualprototyping;TwinCAT
3164. https://doi.org/10.3390/
app12063164
AcademicEditors:Alessandro
1. Introduction
UmbricoandMarcoFaroni
Thecurrentindustryischaracterizedbyincreasingproductscomplexityandpersonal-
Received:25February2022
ization[1,2]. Productsevolvebyintegratingadvancedcapabilitiesofsensing,communi-
Accepted:15March2022
catingandbyreactingtochangingsituationswithincreasinglevelsofreasonings. Smart
Published:20March2022
manufacturing,usuallygatheredundertheIndustry4.0umbrella,supportssuchascenario
Publisher’sNote:MDPIstaysneutral providingameanstoanswertoalwaysdifferentproductspecificationsmaintainingahigh
withregardtojurisdictionalclaimsin processefficiencyandeconomiccompetitiveness[3–5]. Manufacturingsystemsbecame
publishedmapsandinstitutionalaffil- more intelligent and autonomous due to the implementation of emerging communica-
iations.
tion, information and control technologies. Modern assets comprise advanced sensory
apparatus, service-oriented computing platforms and modular controllers, integrating
cyber–physicalsystemswithhigh-fidelitysimulationpredictivemodels[6]. Inparticular,
theongoingfactorydigitalizationhasinevitablychangednotonlythemanufacturingbut
Copyright: © 2022 by the authors.
alsothewaythatproductsaredesignedandconsumed[7].
Licensee MDPI, Basel, Switzerland.
Since modern markets continually demand flexible and customized products, de-
This article is an open access article
velopmentandcommissioningprocessesareoftenverycompressed[8]. Simulationand
distributed under the terms and
virtualprototypingtechnologiesareconsolidatingtheirroleintransferringtestingand
conditionsoftheCreativeCommons
Attribution(CCBY)license(https:// optimizationactivitiesinvirtualenvironments,pursuingrealism,easinessofuseandrelia-
creativecommons.org/licenses/by/ bility[9–12]. Theirapplicationextendstothewholeproductlifecycle[7,13]aswellasthe
4.0/). relatedproductionsystems.
Appl.Sci.2022,12,3164.https://doi.org/10.3390/app12063164 https://www.mdpi.com/journal/applsci

Appl.Sci.2022,12,3164 2of19
Nowadays,manufacturingplantsrequireahigheradaptability,whichisreacheddue
toreconfigurableautomationsystemsgovernedbyadvancedcontrollers,abletointerpret
operating scenarios and calculate and perform the optimal sequence of operations to
achievethebestproductivityandmanufacturingqualityinanycondition.Thus,thecontrol
logicsmustembedthemanufacturingknowledgeandintelligenceneededtointerpretthe
surroundingenvironmentandgeneratetheoptimalrobuststrategies. Theprogrammingof
suchintelligentroboticmanufacturinghasbecomeincreasinglycomplexandchallenging,
requiringalongtimeforverificationandvalidation. Furthermore,itmustbenotedthat
modernroboticcellsaregovernedbymultiplecontrollers,namelyatleastaprogrammable
logiccontroller(PLC)andarobotcontroller,whosecontrollogicsmustbecoordinated[14].
Therefore,fromtheinitialdesignstages,thecells’offlinedevelopmentanddebugging
is usually performed via the use of virtual prototyping software (i.e., general-purpose
computer-aidedengineeringorspecificcomputer-aidedroboticspackages—see[15,16])—
wherethelayoutofthecell,alongwithitsbehavior,canbemodeledandsimulated[17].
Inthesetools,thecellgeometry,kinematicofrobotsandotherdevices,andthegoverning
logiccanberepresented,includingexchangedsignalsandsequencesofcommandstobe
executed. Toobtainhigh-fidelitymodels,itisbeneficialtoincluderealhardwareand/or
softwareelements(e.g.,commercialcontrolunits)inthevirtualenvironment,whichwillbe
thenbecomepartoftheimplementedsolution. Theseapproaches,knownashardware-in-
the-loopandsoftware-in-the-loop[16,18],respectively,arethebasesforaneffectivevirtual
commissioning(VC)strategyforconcurrentengineeringproblems[19]. Theyprovidethe
capabilityofdevelopingandtestingcomplexplantsbeforetheirimplementation.
In a mechatronic system, due to the large variety of involved devices, an efficient
VCmustconnectdifferenthardwareandsoftwareelements,allowingfortheuseofthe
sameinterfaceandinteractionmodalityforboththerealandvirtualcounterparts. Current
virtualprototypingsolutionsoftensufferfromlimitedinteractioncapabilitieswithother
software/hardwaredevicesavailableonthemarket[20]. Therefore,theneedofinterfacing
toolsenablingthecommunicationbetweendifferentcomponents(followingstandardsand
architecturesofindustrialcommunicationprotocols)becomescrucial.
In this context, the present work proposes a method, and its implementation into
an integrated tool, for the complete VC of robotic cells. The reported tool enables the
concurrentsimulationofPLCandrobotprogramswithinarealisticvirtualmodelofthe
robotic system [21], significantly reducing the plant development time and providing
a means for generating, representing and validating information before its installation.
In this way, the sequence of operations of each device can be effectively verified and
optimizedonastandardPC,withoutanyrequireduseofthephysicalassets. Infact,the
multiplecontrollers’contributionstothefinalroboticmanufacturingperformancearetested
withaCAD-baseddigitalprototypeperformingtheactivities(debugging,performance
optimization,safetyandfault-tolerantverificationandvalidation)thataretraditionally
addressed during the physical commissioning of the cell. The considered software are
RobotStudio (RS) and TwinCAT (TC), namely the robot simulation and the IEC-61131
PC-basedautomationpackagesprovidedbyABBandBeckhoff,respectively. Although
thesecommercialplatformshavebeenfrequentlyemployedforthedesignofroboticcells,
eachenvironmenthasbeenseparatelyresearchedandimplemented. Therefore,themain
contribution of this research is to provide an improved VC approach, which integrates
the simulation capabilities of RS and TC and allows users to analyze and optimize cell
behaviorinanaccurateandefficientmanner. Thissameapproachcanbeextendedtoother
commercialplatforms.
TheremainderofthepaperdiscussestheintegrationbetweenRSandTCandreports
ademonstrativecasestudy. Itisorganizedasfollows: Section2brieflyrecallstheprevious
workinherenttoVC.Section3describestheproposedVCtool,involvingaspectsaboutthe
communicationandthefeaturesemployedinthedefinitionoftheapplication;Section4
presentsthecasestudyusedtotesttheapplication; Section5reportsobtainableresults

Appl.Sci.2022,12,3164 3of19
fromtheapplicationoftheproposedsystem;andfinally,Section6reportsconclusionsand
considerationsregardingthefuturedirections.
2. RelatedWork
Since traditional commissioning is proven to be time- and cost-consuming, many
authorshavethoroughlyinvestigatedVCtechnologyduringthelastfewyears. TheVC
isatechniquethataimstovalidatethecontrolsoftwareofamanufacturingsystemwith
asimulationmodel,inavirtualenvironmentandinanearlystageofitscommissioning
process[22,23]. AgreatadvantageapportedbytheVCisthatmanydesignactivitiescan
beparallelized. Thismakesitpossiblefordifferentengineerstoworktogethersimultane-
ously,reducingthedesigningtime[24]. Additionally,itallowsforpossibleerrorstobe
detectedandcorrected,improvingtheperformanceoftheentireroboticcellpriortoits
installation[25–27].
AdeterminingfactorforanefficientVCisitscapabilitytocombinetechnologiesfrom
differentengineeringfieldssoastocreateaholisticenvironmentwherealltheaspectsof
themanufacturingsystemsareconsideredatthesametime[28,29]. Despitesomerecent
advances,asevereabsenceofintegratedsimulation-basedplatformscanbenotedinthe
standardindustrialpractice[24]. Digitalplantmodelsstilldividethegeometryandphysics
of the system from the PLC control program and signals, which are tested within the
controlsoftwaredevelopmenttool(i.e.,withoutadirectvisionoftheprocessbehavior).
Alternatively,byexploitingtheopenplatformcommunications(OPC)protocol,thereal
PLC system can be connected with a 3D virtual model of the cell, defined in DELMIA
orDymolaenvironments,asin[30,31]. AnexampleofOPCcoupling,realizedthrough
theWINMODandSIMITpackages,canbeseenin[18,32],butitislimitedtotheSiemens
platform,whileopenIEC-61131PLCprogramsshouldalsobeemulated.
Somesoftwareproducersareheadingtowardsthedevelopmentofasingleapplication
thatincludesbothdevices’kinematicandPLCprogramsimulations. In[33],amanufac-
turingcellwassimulatedusingProcessSimulate,namelyaspecializedsoftwarethatis
partofSiemensTecnomatixsuiteandoffersa3Dmodelingenvironmentwheretheuser
cantesttheconnectionbetweenmechatronicdevicesandaPLC.Similarly,Simumatik3D
wasemployedin[25]tomodeladidacticroboticcellforapickandplacepurposeandto
testtherelatedPLCcontrolprogram. Arelevantimprovementprovidedbythissoftware
(comparedtoProcessSimulate)isthatPLCsofanyvendorcanbesimulated. Acommon
disadvantage,instead,regardstheirrelativelypoorrobotsimulationcapabilities. Infact,
robotmovementscanonlybeapproximatedsincethereisnorealvirtualcontrollerrunning
ontheapplication,onlyagenericemulator. Fromtheliteraturereview,itemergesthatone
ofthemainlimitationsofVCsolutionsforroboticcellsisrelatedtothescarcerealismof
thesimulatedautomatedplant. Therefore,theonlyviablestrategyforachievinghighly
reliable models seems to be the integration of dedicated commercial platforms [32,34].
Multi-software frameworks have been widely investigated by academic researchers in
recentyears,andnotonlyregardingVC.Theyhavebeenemployed,e.g.,forthedesignof
servo-actuatedmechanisms[12,35,36],thedynamiccharacterizationofroboticsystems[37],
andforthetuningofrobotcontrollers[38].
Inthiscontext,themainobjectiveofthisworkistodevelopandtestanovelVCtool
thatleveragestheintegrationbetweenRSandTC.SincethesoftwareTCturnsaPCintoa
real-timecontroller,theproposedapproachcanbeutilizedtoeither:
• TestarealPLCsystem,i.e.,realizingtheso-calledhybridcommissioningasapartof
thehardware-in-the-loopapproach;
• SimulateitsbehavioronastandardPC,i.e.,realizingafullVCwithasoftware-in-the-
loopapproach.
The PLC programs are tested in RS, where exact copies of the ABB controller and
settingsareavailable,obtainingextremelyaccuraterobotreplicas. Duringthesimulations,
RSprovidesseveralperformanceindices,suchaskineto-dynamicoutputs(end-effector
or joint position, velocity, acceleration, jerk, motor torque, etc.), as well as information

Appl.Sci.2022,12,3164 4of19
regardingthecurrentrobots’energyconsumption,cycletimeandtasksexecution. Another
clearadvantageinemployingRSisthepossibilityfortheusertosupportthedesignof
customizedcelllayouts.Thebehaviorofrobotsandotherdevicescanbefaithfullymodeled,
anddesignchangescanbeappliedwithminimumeffort.
Inconclusion,comparedtothereferencedsolutions,theproposedtoolprovidesthe
followingpracticalcontributions:
• Thevirtualapplicationiseasyandrapidtosetup;
• TheRSenvironmentisstraightforwardandhasashortlearningcurve;
• Nothird-partysoftwareareneededasconnectionmeans;
• ThePLCinteractswiththevirtualcellasitwouldwiththerealcell;
• ThePLCprogrammingonthevirtualenvironmentiscompletelyreusableinthefinal
commissioned(i.e.,physical)system.
3. ProposedVirtualCommissioningApproach
Inthissection,theproposedsoftwarearchitectureisdescribedstartingfromabrief
introductionofthetwomainsoftwaresystems(RSandTC).Then,detailsaboutthenovel
softwarecomponentanditslogic,whichweredevelopedtoenabletheintegrationbetween
RSandTC,areprovided. AdemonstrativevideooftheproposedVCtoolcanbeviewed
atSupplementary.
3.1. IntegratedSoftwareTools
RSwaschosenasthesoftwaretooltorepresentthevirtualcellsinceitoffersfunc-
tionalitiestomodelthegeometricallayout,kinematicofdevices,physicalbehavior,and
controllogic. RSoriginatesasanofflineprogrammingsoftwareforABBrobots. Dueto
its virtual controller technology, RS can carry out extremely realistic simulations of the
movementsoftheABBrobotsandexecutecomplexRAPIDrobotprograms. Indeed,the
softwarerunningontherealrobotcontrollers(RobotWare)isthesameasthatutilizedby
thevirtualrobotcontrollers. Additionally,providesgivesthepossibilitytomodelorimport
3Dgeometriesofotherdevicesaswellastoimplementsmartcomponents(SCs). Theseare
reusableblocks,includinggeometry,kinematicsandfunctioninglogicsthatcanbeutilized
torealizethedesiredabstractionofrealdevices. SomebasicSCsareprovidedbydefaultin
RSandcanbecombinedtobuildmorecomplexones.
In addition, ABB offers a developing tool to extend the basic functionalities of the
software, namely the RS Software Development Kit (SDK). Due to the SDK, users can
developnewapplicationsbyexploitingtheMicrosoftVisualStudioenvironment,suchas
add-insorcustomizedSCs,expandingsoftwarepotentialities.
Ontheotherhand,TCisthesoftwareusedforconfiguringandprogrammingBeckhoff
devices,includingservodrivesandPLCs. APLCprogramcanbewrittenusingseveral
languages,suchasladderdiagram,instructionlist,functionblockdiagram,structuredtext
andsequentialfunctionchart(SFC).Suchprogramscontrolthetaskexecutionflowofthe
entirecell,exchangingsignalswiththecontrolsoftherobots,motors,linearaxesandother
devices. The PLC runs on a hardware system that is capable of real-time performance,
essentiallyadedicatedPCthatensuresthecyclesareexecutedinatimelymanner.
Thesetwosoftwarehavenonativewayofcommunicatingwitheachother. However,
inordertocreateacompleteVCofaroboticcell,itisessentialtoemulatecontributions
ofeachcontroller(namely,PLCandrobotcontroller)withspecificsimulationtoolsthat
mustbecoupledandsynchronized. Thisisthereasonfortheimplementationofatoolthat
allowsdataexchangebetweenTCandRS.
3.2. ArchitectureoftheVirtualCommissioningSystem
The main idea of the proposed approach is to replicate the physical automation
solutionarchitectureinavirtualenvironment(inthespecificcaseRS)referringtoaone-
to-onemappingbetweenrealphysicalcomponentsandtheirdigitalrepresentations. As
shownintheleftpartofFigure1,intheindustrialpractice,aroboticcellisusuallygoverned

Appl. Sci. 2022, 12, 3164 5 of 19
3.2. Architecture of the Virtual Commissioning System
The main idea of the proposed approach is to replicate the physical automation so-
Appl.Sci.2022,12,3164 5of19
lution architecture in a virtual environment (in the specific case RS) referring to a one-to-
one mapping between real physical components and their digital representations. As
shown in the left part of Figure 1, in the industrial practice, a robotic cell is usually gov-
erbnyedo nbeyP oLnCe ,PwLhCi,c whhexicchh aexncgheasnsgigens aslisgnwailtsh woitthhe ortahuetro amuatotimonatmioond muloeds,uil.ees.,, ci.oen., tcroonllterrosl-of
lerrosb ooft sr,omboottso, rms,oettocr.sT, hetec.s iTghnea lscigannarle cparne sreenptraenseyntty apneyo tfydpaet ao,fe d.ga.t,aB, oeo.gle.,a Bnoso,ilneatengse, risntaen-d
gerersa landda trae.alT dhaetac.o Tmhme cuonmicmatuionniciasticoonn ivse cyoendvereyfeedr rrienfgertroinag fitoe lad fibeulds ,bwush,i wchhiicshp ihsy pshicyasl-ly
implementedasacableconnectingthecontrollersandcelldevicesinseries.
ically implemented as a cable connecting the controllers and cell devices in series.
(a) (b)
FiFgiugruer e1.1 C.Conocnecpetputuala lrereppreresseenntatatitoionn ooff tthhee pprrooppoosseedd VVCC aapppprrooaacchh:: ((aa)) TTyyppicicaallh haardrdwwaraerea racrhcihteitcetcu-re
ture of a robotic cell; (b) Representation in a virtual environment of the control architecture to main-
ofaroboticcell;(b)Representationinavirtualenvironmentofthecontrolarchitecturetomaintaina
tain a correspondence between physical and virtual assets.
correspondencebetweenphysicalandvirtualassets.
The right side of Figure 1 depicts the proposed VC solution. The PLC system is main-
The right side of Figure 1 depicts the proposed VC solution. The PLC system is
taminaeidn taasi na ecdelal sgoavceerlnlignogv teoronl i(nhgybtoriodl s(holyubtrioidn)s oolru otpiotino)noarlloyp stuiobnstaitlluytesdu bbsyt iat uPtCed rubnynainPgC
anru enmnuinlagtaedn ePmLCul afoterd a PfLuCllyf ovriratufualll ystrvairtetugayl. sEtraacthe gpyh.yEsaiccahl pdheyvsicicea lisd reevpicreesiesnrteepdr einse tnhtee d
prinottohteyppirnogto stoyfptwinagres opfltawtfaorremp laast fao rvmirtausaal mviortduuallem, wodhiuclhe ,isw dheicshiginsedde tsoig hnaevdet othhe asvaemteh e
instaemrfaecien toefr ftahcee orefathl ecoreuanltceorpuanrtte,r pina rtte,rimntse ormf esxocfheaxncgheadn gseidgnsaiglsn aalnsda nedxpeexcpteecdt ebdebheahvaiovrio. r.
SuScuhc hvivrtiurtaul aml omdoedlse lasrea rreearleizaelidz eads SaCssS,C lesv,eleravgeirnagg itnhge ftuhnecftuionncatiloitnieasl iatineds aabnsdtraabctsitornac ctaio-n
pacabpilaitbieilsit oiefs RoSf bRyS pbryopvriodvinidgi ntog tthoet hueseurs tehret hpeopssoisbsiilbitiyli toyf odfedfienfiinngin rgeuresuasbalbe lbelbolcokcsk, sw,whihcihc h
enecnacpaspuslualtaet egegoemometerticriacla dledfeinfiintiiotinosn, sk,iknienmemataictisc, ss,esnesnosrosr sanadn dcocnotnrtorlo llolgoigcisc.s T.hTeh elelveevle olfo f
dedteatial iilni nthteh ererperperseesnetnattaiotino nofo fthteh esisnignlgel eddeveivciec eisi sa acocmompprormomisies ebebtewtweeene nthteh enenceecsessasrayr y
reraelaislimsm anadn dthteh eovoevrearlal lpleprefrofromrmanacnec eofo tfhteh esismimulualtaiotino nenevnivriornomnmenetn. tI.nI npapratrictiuclualra, ra,sapsepcetcst s
thtahta itnifnlufleunecnec ethteh epeprefrofromrmanacnec eofo tfhteh ePLPCLC mmusuts bteb eacaccucruartaetleyl ymmodoedlelellde,d s,uscuhc hasa dsydnyanmamici c
oro rsysnycnhcrhornoinziezde dacatcivtiivtiietise.s C. Conotnrtarsatsintignlgyl,y p,hpyhsyisciaclalyll ybabsaesde dcocmompuptuattaiotinosn sthtahta atcaccucruartaetleyl y
rerperperseesnetn styssytestmems psepreforfromramnacne cmeamya bye bdeemdeamndainndgi ning tienrmtesr mofs roesforuerscoeusr,c seos ,thseoyt hmeuysmt bues t
limbeitleimd tiote tdheto ptahretsp warhtesrwe thheerye pthreoyvipdreo tvhied enethceesnsaercye srseaarlyismre aalnisdm coahnedrecnochee rwenitche thwei trhepth-e
rerseepnrteesde nbteehdabveiohra, vaiso rd,iasscudsissecdu sisne d[39in]. [39].
AAnanlaolgooguouslsyly, ,tthhee ffllooww ooff ssigignnaalslso onnth tehfie eflidelbdu bsuisss iesa mselaemsslleyslsilnyk elidnktoeda fltoo wa oflfovwir toufa l
visritgunaal lssiginnathlse ivni rtthuea vlierntuvairlo ennmviernotn.mThenetc. oTmhem cuonmicmatuionnicbateitowne beentwtheeePnL tChea PnLdCth aenvdi rtthuea l
vierntuvairl oennmviernontmiseonbtt iasi noebdtaibnyeda bcoyn an ceocntinoenctiinotne rifnatceerfdaceev edleovpeeldopaesda aSs Ca .STCh. iTshcios mcopmonpeon-t,
nennatm, neadmPeLdC P_LBCec_kBheockffh,omffi,m micimstihcse tphree spernesceenocfet ohfe trheea rlePaLl CPLinC RinS .RTSh. Tehceo ncnonecnteioctniotno ttoh e
three arlePalL PCLiCs eisst aebstliasbhleisdhtehdr othurgohutghhe tahuet oamutaotimonatdioenv idceevsipceec isfipceactiifoicna(tAioDn S()ApDroSt)o pcorol,towchoilc, h
wihsipchro ivs ipdreodvbidyeBde bcyk hBoefcfkfhoorflfi nfokrin lgintkhiengd ethveic desevoifcaesc oofn tar ocolnchtraoiln c.hSaininc.e SAinDceS AADdvSa Andce-d
vaPnrocegdra PmromgirnagmImnitnergf aIncetesrf(aAcPesI) (AarPeI)a avraei laavbaleilafbolre MfoSr MNSE TNEFTra Fmraemwoewrkoprkla ptflaotrfmor,mth, ethCe #
Cp# rporgorgarmammminignlga nlagnugaugaegwe awsaus suesdedto tdoe dveevloeplotph tehPeL PCL_CB_eBcekchkohffofSfC SCto troe ardeaadn adnwd rwiteritteh e
thvea vluaeluseosf othf ethvea vriaarbilaebsledse dfienfeidneidn itnh ethTeC TPCL PCLpCr opgrroagmra.m.
FromthePLCpointofview,thePLC_BeckhoffSCactsasarealelementofthecontrol
chainandexchangesrealsignalsonthefieldbus.Contrastingly,thecomponentisintegrated
inthevirtualenvironmentofRSsothatitcanreadandwritethevirtualsignalsusedto
controlthesyntheticenvironment. TheusageoftheSCinRSisquitestraightforwardsince
itprovidesthepossibilitytofreelyaddsignalsthattheuserwantstoexchangewiththePLC
simplybynamingthemastheyappearinthePLCcode. Forinstance,Figure2showshow

Appl. Sci. 2022, 12, 3164 6 of 19
From the PLC point of view, the PLC_Beckhoff SC acts as a real element of the control
chain and exchanges real signals on the field bus. Contrastingly, the component is inte-
grated in the virtual environment of RS so that it can read and write the virtual signals
used to control the synthetic environment. The usage of the SC in RS is quite straightfor-
ward since it provides the possibility to freely add signals that the user wants to exchange
Appl.Sci.2022,12,3164 6of19
with the PLC simply by naming them as they appear in the PLC code. For instance, Figure
2 shows how the two signals RS_Input1 and RS_Output1, defined in the robot controller
Cothnetrtwololesri_gnRa1l,s RarSe_ Inlipnukte1da ntdo RtSh_eO PutLpCut 1v,adreifianbeledsi nPtLhCer_oObouttcpountt1ro allnerdC PonLtCro_llIenr_pRu1t,1, respec-
tivaerelyl.i nTkheed ttwo toh elaPttLeCr vvaarriiaabblelessP LarCe_ Oseuatprcuht1eda nidn PthLeC _TInCp urut1n,nreinspge cctoivdeely a.nTdh ethtwe ovalues are
aultaottmeravtiacraialblyle ssyanrechsreoarncihzeedd ibnyt hteheT CSCru. nning code and the values are automatically
synchronizedbytheSC.
Figure2.UsageofthedevelopedPLC_BeckhoffSCinRS.Input/outputsignalsfromthePLC,i.e.,
FigPuLCre_ I2n.p Uuts1aagned oPf LthCe_ Oduetvpeulto1p, aerde PexLcCha_nBgeecdkhwoitfhf SroCb oint cRonSt.r oInllperusti/gonuatlps,uit.e s.,igRnSa_Ilns pfurot1ma nthde PLC, i.e.,
PLRCS__IOnuptuput1t1 ,abnyde PstLabCli_sOhiungtpluogt1ic, caornen eecxtciohnasnignetdh ewLiotghi crSotbaotito ncopnantreollolefrR Ss.igTnhaelnsa, mi.ees., oRfSth_eInput1 and
RSs_igOnualtspduetfi1n, ebdyi nesthtaebPlLisCh_iBnegc klhoogfifcS Ccocnonineccidtieownsit hint htehvea Lrioabgliecn Satmateisoinn tphaenPeLlC ocfo RdeS.. The names of the
signals defined in the PLC_Beckhoff SC coincide with the variable names in the PLC code.
3.3. DescriptionofthePLC_BeckhoffSmartComponentInterface
Inthissection,adescriptionofthePLC_BeckhoffSCuserinterfaceisprovided. Inthe
3.3. Description of the PLC_Beckhoff Smart Component Interface
RSenvironment,aSCinterfaceissubdividedintoPropertiesandI/OSignals,asshownin
FiguInre t3h.iCs osneccetrinoinng, ath edIe/sOcrsiepcttiioonn, ofofu trhdee fPauLlCts_igBneaclkshwoefrfe SpCro vuidseedr ainstpeurlfsaecdet yips ep,irnovided. In
thoer RdeSr etnovaiprpoenamrteontth, ea uSsCer inastebrufattcoen sist osuabctdivivatiedseidg ninaltom Panroagpeemrteienst faunndct Ii/oOns S,inganmaellsy, as shown
inC FriegauterSei g3n. aCl,oDnecleetrenSiignnga tl,hSet aIr/tOa nsdecSttioopn.,T fhoeusre dsiegfnaaulsl’tn saimgnesalasr ewreesreer vperdovaniddethde aresf opruelsed type,
excludedfromtheexchangemechanismviaADScommunication. Theyareusedtooperate
in order to appear to the user as buttons to activate signal management functions, namely
andconfiguretheSCtocreateanewsignalwithagivenname,deleteasignal,startanADS
CreateSignal, DeleteSignal, Start and Stop. These signals’ names are reserved and there-
connection,andstoptheconnection,respectively.
fore excluded from the exchange mechanism via ADS communication. They are used to
InthePropertiessection,AdsAddressandPortarethetwofieldsrequiredbytheADS
opperroatoteco alntod rceaocnhfitghuerTeC thPeL CSCan tdoe cstraebaltiesh at hneecwo msimgunnailc awtiiothn. aO gnicveetnhe nyaamreefi, ldleedleinte, a signal,
staclritc kainn gAoDnSt hceonbuntetcotnioSnta, rat,nadc sotnonpe ctthioen coatntenmecpttiownil,l rbeespmeacdtiev:eiflyth. e connection fails,
an eInrr otrhem ePsrsoapgeerwtiiells bseedctiisopnla,y AeddisnAtdhderReSsso uatnpdu tPmoersts aagrees twhein tdwowo .fiTehldesp rroepqeurtiyred by the
DisconnectWhenSimulationStopsisaBooleanvaluethatdeterminesiftheADSconnection
ADS protocol to reach the TC PLC and establish the communication. Once they are filled
mustbeinterruptedornotwhentheRSsimulationisstopped.
in, clicking on the button Start, a connection attempt will be made: if the connection fails,
The last two properties, SignalName and SignalType, are involved in the creation
an error message will be displayed in the RS output messages window. The property Dis-
ordeletionofasignal. Oncetherelatedfieldsarefilledin,thebuttonCreateSignalwill
coinnnsteacnttWiatheeansSigimnaulloaftitohneSstpoepcisfi eisd aty Bpoe,oalneadni tvwailluleb ethadatd eddetteortmheinSeCs ciuf stthome AsiDgnSa lcsonnection
mluisstt. bSiem iinlatrelryr,uapsitgenda locra nnobte wrehmeonv ethdef rRomS sthimemuleanttiioonn eids lsitsotpbypewdr.i tingitsnameinthe
SignTahlNe alamset ptwroop eprtryoapnedrttiheesn, ScliigcknianlgNoanmthee aDnedle tSeiSgingnaalTlbyupteto, na.rTeh iensveotulvpepdh ainse tehned csreation or
ensuringthateachTCvariablethatmustbeexchangedwithRSisaddedtotheSC.
deletion of a signal. Once the related fields are filled in, the button CreateSignal will in-
stantiate a signal of the specified type, and it will be added to the SC custom signals list.
Similarly, a signal can be removed from the mentioned list by writing its name in the
SignalName property and then clicking on the DeleteSignal button. The setup phase ends
ensuring that each TC variable that must be exchanged with RS is added to the SC.

Appl. SciA. 2p0pl2.2S,c 1i.22, 032126,41 2,3164 7of71 9of 19
(a) (b)
FiguFreig 3u.r eD3e.faDuelfta ualptpaepapreaanracne coefo tfhteh ePPLLCC__BBeecckkhhooffff SSCC iinnR RSS..( a()a)G Grarpahpihciucs uerseinrt einrftaecrefaocfet hoef SthCei nSC in
the StthaetiSotnat LioongLico gsieccstieocnti oonf oRfSR: Si:ni nthteh efifigguurree,, nnoo ssiiggnnaall ttoob beee xecxhcahnagnegdewd iwthitthhe thPeL CPLhCas hyaets byeeetn been
defindeedfi;n (ebd); S(bC) SinC eindietd mitomdoed: et:hteh eusuesre rccaann uussee tthhiiss ffoorrmmt otoc ocnofingfiugruerAe DASDcSo ncnoencntieocntioopnt ioopnstiaonnds and
creatcer esaigtensaiglsn tahlsatth aartea rreeqreuqiureirde dfofro rspspeecciiffiicc aapppplliiccaattiioonnss..
3.4. DescriptionoftheSignalExchangeMechanism
3.4. Description of the Signal Exchange Mechanism
Asmentionedbefore,accordingtothedevicesutilizedinthecellandtherequired
As mentioned before, according to the devices utilized in the cell and the required
signals,theuseraddsthenecessaryI/Osignals,providinganamewhichcorrespondsto
signals, the user adds the necessary I/O signals, providing a name which corresponds to
the desired variable in TC to be connected. As an example, a variable could be named
the dases“iMreAdI vNa.Rrioabbolet1 i.nbu TsCy” t.oT bhies cmoenannesctthedat., Ainst hane PeLxCamcopdlee,, aa vvaarriiaabblleen caomueldd “bbeu nsyam”iesd as
“MAseINarc.Rheodboint1th.beuinsyst”a.n cTeh“iRs omboeta1n”so ftahafut,n cintio tnhbel oPckLCth actolidkee,l yai nvcalurdiaebslteh encahmareadct e“rbisutiscys” is
searochfaedsp ienc itfihcer oinbosttatynpcee; “thReoinbsotta1n”c eo“fR ao fbuont1c”tihoans bbeleonckd etchlaarte ldikineltyh einpcrolugdraems tohrgea cnhizaartaiocnteris-
tics ounf iat (sPpOeUci)finca rmoebdo“t MtyApIeN; ”th. Ee sisnesnttaianlclye, s“uRcohbeoxtp1e”d iheanst rbeepernes ednetcslaardeidre icnt mtheea npsrtoogmraamp or-
RobotStudiosignalnamestoTCvariables.
ganization unit (POU) named “MAIN”. Essentially, such expedient represents a direct
In the following, pseudocode of the PLC_Beckhoff SC (Algorithm 1) outlines the
means to map RobotStudio signal names to TC variables.
initialization of the communication by mapping the RS signals to TC variables. IOS
In the following, pseudocode of the PLC_Beckhoff SC (Algorithm 1) outlines the ini-
referstothecollectionofsignalsmanagedfromthePLC_BeckhoffSC,whichiscycledto
tialization of the communication by mapping the RS signals to TC variables. IOS refers to
instantiateaSignalMapInfoobjectmiforeachelementtobemappedwiththePLC.Such
the coobljleeccttsioanre otfh seingnstaolrse dmianntawgoedse ftrso,mna tmheed PSLIC(i_.eB.e,cinkphuotffs iSgCna, lwshoficthh eisP cLyCc_leBde ctkoh ionfsftSaCnt,iate
a SiggnoainlMg farpoImnfRoS otbojeTcCt )main fdorS Oea(cih.e .e,loeumtpenutt stoig bnael smoafptpheedP LwCit_hB etchkeh PoLffCS.C S,ugcohin ogbfjreocmts are
thenT sCtotoreRdS i)n.T towsoy nscehtsro, nniazmetehde SvaI l(ui.eeo.,f iannpRuSt ssiiggnnaallsw oitfh tThCe PanLdCv_iBceecvkehrsoaf,f tShCe,m gaopipnign gfrom
RS tdo aTtaCi)n aclnudd eS:O (i.e., output signals of the PLC_Beckhoff SC, going from TC to RS). To
sync•hronAizree ftehreen vcaeltuoet hoef RanS sRigSn sailgonbajel cwt;ith TC and vice versa, the mapping data include:
• •
A re
A
fe
p
r
o
e
i
n
n
c
t
e
er
t
t
o
o
t
t
h
h
e
e
R
ha
S
n
s
d
i
l
g
e
n
p
a
r
l
o
o
p
b
er
je
ly
ct
c
;
r eatedtoreachthedesiredvariableinTCfromthe
userspecifiedname;
•
A pointer to the handle properly created to reach the desired variable in TC from the
• Thelastexchangedvalueofthesignal.
user specified name;
•
The last exchanged value of the signal.
Algorithm 1 Communication initialization
INITIALIZECOMMUNICATION()
in: TC client host name tcHostName,
TC client port name tcPortName,
set of IO Signals IOS from RS
out: TC connected client ads
set of input signals SI (from RS to TC)
set of output signals SO (from TC to RS)

Appl.Sci.2022,12,3164 8of19
Algorithm1Communicationinitialization
INITIALIZECOMMUNICATION()
in: TCclienthostnametcHostName,
TCclientportnametcPortName,
setofIOSignalsIOSfromRS
out: TCconnectedclientads
setofinputsignalsSI(fromRStoTC)
setofoutputsignalsSO(fromTCtoRS)
local: currentRSsignalsbeingconsidered,
signalmappinginfomi
1: InstantiationoftheADSconnection
2:(cid:3)ads←connect(tcHostName,tcPortName)
3: Instantiationofthesignalmaps
4:(cid:3)|MI|←0
5:|MO|←0
6: InstantiationofasignalinfomapmitoTCforeachRSsignal
7:f(cid:3)oralls∈IOSdo
8: casename(s)of
9: “Start”: Nothingtodo
10: “Stop”: (cid:3)Nothingtodo
11: “CreateSignal”: (cid:3)Nothingtodo
12: “DeleteSignal”: (cid:3)Nothingtodo
13: others: (cid:3)
14: Instantiateandpopulatemappinginfomi
15: (cid:3)mi←CREATEMAPPINGINFO(s)
16: rsSignal(mi)←s
17: tcHandle(mi)←CREATETCVARIABLEHANDLE(ads,name(s))
18: lastValue(mi)←value(s)
19: Addmitotheproperset
20: (cid:3)ifisInput(mi)then
21: ADDELEMENT(MI,mi)
22: else
23: ADDELEMENT(MO,mi)
24: endif
25: endcase
WhenthebuttonStartisclicked,theADSconnectionisestablishedandthehandle
variables are automatically created due to the initialization procedure described above.
After that, RS simulation can also be run. As long as the simulation is active, an event
handlercalledOnSimulationStepiscalledforeveryRSelementarysimulationstep. The
codeexecutedateachstepiterationincludestwomethods:
• ROBOTSTUDIOREADTWINCATWRITE,whichupdatesthevaluesofvariablesinTC
fromsignalchangesinRS;
• TWINCATREADROBOTSTUDIOWRITE,whichchangesthestatusofsignalsinRSasa
variablevalueischangedinTC.
Thepseudocodeofthefirstofthetwofunctionsisreportedbelow(Algorithm2). The
otherfunctionhasaspecularstructure. Foreachmappedsignal,thevalueinRSisread
andthecorrespondingvariableinTCisupdated. Anoptimizationstrategyisusedtoavoid
uselessoperations. Thelastregisteredvalueisstoredinthemappinginfoobject,anditis
comparedwiththenewvalueinthenextcycleinordertoskipthewritingoperationifthe
valuehasnotchanged. Thisstrategyallowsthecommunicationoverheadtobereduced
andmakesthesignalssynchronizationfaster.

Appl.Sci.2022,12,3164 9of19
Algorithm2UpdatevariablesinTC
ROBOTSTUDIOREADTWINCATWRITE(ads,MI)
in: clientadsconnectedtoTC,
setMIofthemappinginfosoftheinputsignals(fromRStoTC)
local: currentmappinginfomibeingconsidered,
currentvaluecvofasignal
1:forallmi∈MIdo
2: cv←currentValue(mi)
3: ifcv(cid:54)=lastValue(mi)then
4: WritecvinTCvariableusingadsclient
5: (cid:3)WRITE(ads,tcHandle(mi),cv)
6: lastValue(mi)←cv
7: endif
4. CaseStudy: RoboticAssemblyCell
The approach described in Section 3 has been applied to a robotic assembly cell
for gearboxes. The virtual model of the cell was realized in RS starting from a CAD
representationoftherealimplementedprototype. ThedevelopedcaseallowedtheVC
capabilitiesoftheproposedapproachtobetestedinacomplexscenariomadeoftworobots
andvariousadditionalsystems. Inparticular,theinteractionmechanismbetweenthePLC
andthevirtualrepresentationofthecelldevicesisreportedhereindetail.Finally,anextract
ofthePLCcodeisshownanddiscussed,aswellasthecapabilityoftheVCapproachto
improvetheoverallperformanceofthesystem.
4.1. DescriptionoftheRoboticAssemblyCell
TheroboticassemblycellincludestwoABBindustrialrobotsworkinginthesame
workspace.Theaimofthecellistomountfastenersandbearingsonabasementresembling
the case of a gearbox. The basement is placed on a Cartesian positioning table that is
translatedbytwolinearaxes. Thetablecanarrangethebasementindifferentpositions
underanelectricpress,thatisactivatedwhenpinsorbearingsmustbepressedintheir
seats. Custom-designedpunchesareuseddependingontheobjectthatmustbepressed:
theyarebroughtintherightpositionbyarobotandlockedonthepressduetoitsfasttool
changerinterface.
Thetworobotsinthecellareequippedwithdifferenttools. IRB1600-10/1.2(Robot1)
mountsatoolchanger,whichisusedtolocktheappropriategripperdependingonthe
objectthathastobepickedandthenplacedinthebasement. FiveSchunkgrippersare
providedbelongingtotwodifferentfamilies: thePNG-plus80-1,whichincludesparallel
grippers,andthePNZ-plus80-1family,whichisathree-fingercentricgripper. Inparticular,
two parallel grippers are used to pick and place pins and handle punches, while three
centricgrippersareusedtopickupbearings.
IRB2600-20/1.65(Robot2)mountsanelectric,torque-controlledscrewerfromBosch
Rexroth. Itpicksthefastenersfromtheirholderandscrewsthemonthebasement.
ThesystemiscoordinatedbyaBeckhoffEmbeddedPCCX5140PLCequippedwith
IntelAtomquad-coreprocessor. AnEtherCATfieldbusconnectsthedevicesinthecelland
isresponsiblefortheI/Osignalsconnections.
AlistofthemainhardwarecomponentspresentinthecellisgiveninTable1.

Appl.Sci.2022,12,3164 10of19
Table1.Detailsonthemaindevicesemployedinthecell.
|                                   |                            | Name |     | Quantity |     |                                   |                            | Description   |     |
| --------------------------------- | -------------------------- | ---- | --- | -------- | --- | --------------------------------- | -------------------------- | ------------- | --- |
|                                   | ABBIRB1600-10/1.2          |      |     |          | 1   |                                   | Serialmanipulator          |               |     |
|                                   | ABBIRB2600-20/1.65         |      |     |          | 1   |                                   | Serialmanipulator          |               |     |
| SchunkQuick-Change-SystemsSWS-011 |                            |      |     |          | 1   |                                   |                            | Toolchanger   |     |
|                                   | SchunkPNG-plus80-1         |      |     |          | 2   |                                   | Parallelgripper            |               |     |
|                                   | SchunkPNZ-plus80-1         |      |     |          | 3   |                                   | Three-fingercentricgripper |               |     |
|                                   | BoschRexrothCS351          |      |     |          | 1   | Electric,torque-controlledscrewer |                            |               |     |
|                                   | CoretecServoPressCS20-350B |      |     |          | 1   |                                   |                            | Electricpress |     |
BoschRexrothIntraDriveCsSystems 2 Motorsanddriversforlinearaxis
BeckAhppol.f fScEi.m 20b22e,d 1d2,e 3d16P4 CCX5140 10 of 19
|     |     |     |     |     | 1   |     |     | PLC |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Thevirtualmodelofthecellwascreatedstartingfroma3Drepresentationrealized
The virtual model of the cell was created starting from a 3D representation realized
in SolidWorks, including both the models used to design the components and models
in SolidWorks, including both the models used to design the components and models
providedbythemanufacturersofthedevices(Figure4). Then,thegeometrywasimported
provided by the manufacturers of the devices (Figure 4). Then, the geometry was im-
intoRS.Thisisthenfollowedbyastandardworkflow,whichincludesthedefinitionof
ported into RS. This is then followed by a standard workflow, which includes the defini-
movabledevices,knownasmechanisms,usedinthespecificcaseforthepress,positioning
tion of movable devices, known as mechanisms, used in the specific case for the press,
tableandgrippers.
positioning table and grippers.

Figure 4. Full view of the assembly cell reproduced in RobotStudio 3D environment.
Figure4.FullviewoftheassemblycellreproducedinRobotStudio3Denvironment.
|     |     | 4.2. Communic4a.t2io. nCoPmatmteurnnibcaettwioene nPaPtLteCrna nbedtwCeelelnD PeLvCic easnd Cell Devices  |     |     |     |     |     |     |     |
| --- | --- | --------------------------------------------------------------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
TheroleoftheTPhLeC roilset oofc tohoer PdLinCa ties tthoe coaoctridviintyatoef tthhee arcotbivoittsya onfd ththe erodbeovtisc easnidn cthlued deedvices included
inthecell. Accino rtdhien gcetlol. tAheccporrodpionsge dtoa tphper poarochp,oisnedth aepRpSrovaircthu, ailnm thoed eRlS, avdiretduiacla mteoddSeCl, ias dedicated SC
createdforeacihs pcrheyastiecda lfdore veiacceh. TphheySsCicarle pdreevsiecnet.s Tthhee bSeCh arevpiorresoefntthse tphhe ybseichaalvaisosre otfb ethineg physical asset
representedrebceuirnrgin rgeptoretsheenftuedn crteicounrarliintige stop trhoev ifduendctbioynRaSli.tiHeso wpreovveird,ethde biyn tReSrf. aHceowofetvheer, the interface
SCintermsofoef xthchea SnCg eind tseirgmnasl omf euxscthbaenegqeuda slitgontahle mreuaslt dbeev eiqceuainl toor dtheer rteoapl edremviictea irne aolrder to permit
VCofthecell.a real VC of the cell.
A communicaAti ocnompamttuenrnicawtiaosn dpeafitnteerdn bweatws edeenfintheed PbLeCtwaenend tthhee PotLhCe radnedv tihcees obtyher devices by
meansofastandardizedsetofsignals,whicharesummarizedinTable2. Thereported
means of a standardized set of signals, which are summarized in Table 2. The reported
signalsrepresentaminimumcoresettoguaranteeanefficientinteractionbetweenthePLC
signals represent a minimum core set to guarantee an efficient interaction between the
andthecelldevices.
PLC and the cell devices.
Table 2. List of the core I/O signals exchanged between a robot/device and the PLC.
|     |     | Signal Name  | From (Output)  |     | To (Input)  |     |     |     | Description  |
| --- | --- | ------------ | -------------- | --- | ----------- | --- | --- | --- | ------------ |
procedureNumber
|     |     |                |      |     | Robot or   | Contains a coded data to identify the action that the  |     |                           |     |
| --- | --- | -------------- | ---- | --- | ---------- | ------------------------------------------------------ | --- | ------------------------- | --- |
|     |     | programNumber  | PLC  |     |            |                                                        |     |                           |     |
|     |     |                |      |     | Device     |                                                        |     | device has to carry out.  |     |
targetPosition
|     |     |          |      |     | Robot or   | Triggers the execution of the procedure whose code  |     |                                     |     |
| --- | --- | -------- | ---- | --- | ---------- | --------------------------------------------------- | --- | ----------------------------------- | --- |
|     |     | execute  | PLC  |     |            |                                                     |     |                                     |     |
|     |     |          |      |     | Device     |                                                     |     | has been transmitted to the device  |     |
Robot or
|     |     | done  |     |     | PLC  | Raised when the device completes the procedure.  |     |     |     |
| --- | --- | ----- | --- | --- | ---- | ------------------------------------------------ | --- | --- | --- |
Device
Robot or  Error code being raised in case of faults in the proce-
|     |     | error  |         |     | PLC  |     |     |     |                 |
| --- | --- | ------ | ------- | --- | ---- | --- | --- | --- | --------------- |
|     |     |        | Device  |     |      |     |     |     | dure execution  |
The actions performed by the robots and the devices in the cell were subdivided in
elementary procedures, which are combined to perform more complex tasks. The PLC
elaborates the required sequence of operations, the possible simultaneity of the actions
according to the general assembly task of the cell, and the space-sharing constraints.

Appl.Sci.2022,12,3164 11of19
Table2.ListofthecoreI/Osignalsexchangedbetweenarobot/deviceandthePLC.
| SignalName | From(Output) | To(Input) |     | Description |
| ---------- | ------------ | --------- | --- | ----------- |
procedureNumber
|               |     | Robotor | Containsacodeddatatoidentifytheactionthat |     |
| ------------- | --- | ------- | ----------------------------------------- | --- |
| programNumber | PLC |         |                                           |     |
|               |     | Device  | thedevicehastocarryout.                   |     |
targetPosition
|         |     | Robotor | Triggerstheexecutionoftheprocedurewhose |     |
| ------- | --- | ------- | --------------------------------------- | --- |
| execute | PLC |         |                                         |     |
|         |     | Device  | codehasbeentransmittedtothedevice       |     |
Robotor
| done |     | PLC | Raisedwhenthedevicecompletestheprocedure. |     |
| ---- | --- | --- | ----------------------------------------- | --- |
Device
|       | Robotor |     | Errorcodebeingraisedincaseoffaultsinthe |                    |
| ----- | ------- | --- | --------------------------------------- | ------------------ |
| error |         | PLC |                                         |                    |
|       | Device  |     |                                         | procedureexecution |
Theactionsperformedbytherobotsandthedevicesinthecellweresubdividedin
elementaryprocedures, whicharecombinedtoperformmorecomplextasks. ThePLC
elaboratestherequiredsequenceofoperations, thepossiblesimultaneityoftheactions
according to the general assembly task of the cell, and the space-sharing constraints.
Therefore, the PLC is in charge of sending identifiers of the procedures to be executed
to cell devices, which were named as procedureNumber in case of manipulators and
programNumber for the press. For the X-Y axes of the positioning table, the numeric
value of the coordinate to be reached, i.e., the targetPosition, is provided. Finally, the
communicationpatternwascompletedwithadditionalerrorsignalsinordertoguarantee
therequiredsafetyandrobustnessinindustrialimplementations.
Figure5showstheappearanceofPLC_BeckhoffSCconnectedtothecelldevices,as
theconfigurationstageofthecelliscompletedaccordingtothesignalpatternexplained
above. Thesignalexchangeisbasedonasimpleremoteprocedurecall(RPC),i.e.,aclient–
server interaction implemented via request–response messages. This pattern is able to
safelymanagecomplexscenariosinastandardizedmanner.
Inpractice,asdepictedinFigure6,anoperationisactivatedbytheexecutesignal,and
itgivesfeedbackwhenactivityendsbythedonesignal. OncethePLChasreceivedthe
donesignal,itresetstheexecutesignal. Finally,thedeviceresetsthedonesignalassoonas
itreceivestheinformationthattheexecutesignalhasbeenreset.
The same logic is applied to devices and robots, leveraging respective controllers’
codingsmeanstohandlethesignals’exchanges. Forinstance, inthespecificcaseofan
ABBrobot,theRPCschemeismanagedbyamainloopoperatingintheRAPIDcode,i.e.,
thecoderunningintherobotcontroller. AsshowninFigure7,therobotactsasanyother
device: itreceivesanexecutecommandfromthePLCanditreturnsadonesignalwhenthe
requestedprocedureisfinished. Asreportedinthefollowingpseudocode(Algorithm3),
thealgorithmrunningontherobotcontrollerincludesastandardMAINsectionwithaloop
implementingtheRPCpattern.Thecodeensuresthemanagementoftheexchangedsignals
andtheinvokingofthedesiredprocedureaccordingtothevalueoftheprocedureNumber.
Othercodesectionsarethenimplementedtodetailtheactionrequiredbythespecific
operation procedure, such as a joint movement, gripper attaching, object grabbing, etc.
Suchproceduresweredefinedaccordingtothesubdivisionoftherobottasksinelementary
operationsaccomplishedintheinitialdesignphaseoftheassemblyprocess.
4.3. PLCProgramming
TheSFCgraphiclanguage,definedintheinternationalstandardIEC61131-3,hasbeen
chosenasPLCprogrammingmeansforitssuitabilitytovisualizeconditionalproceduresas
typicallyhappensinindustrialapplications. Moreover,thislanguageiseasytounderstand,
as some basic interpretation rules are provided and can be combined with other PLC
programminglanguages.

Appl. Sci. 2022, 12, 3164 11 of 19
Therefore, the PLC is in charge of sending identifiers of the procedures to be executed to
cell devices, which were named as procedureNumber in case of manipulators and pro-
Appl. Sci. 2022, 12, 3164 gramNumber for the press. For the X-Y axes of the positioning table, the nume11r ico fv 1a9l ue of
the coordinate to be reached, i.e., the targetPosition, is provided. Finally, the communica-
Appl.Sci.2022,12,3164 tion pattern was completed with additional error signals in order to g12uoafr19antee the re-
Thereqfuoirree, dth sea fPeLtyC a ins din r ocbhuarsgtnee osfs sinen idnidnugs tirdieanl tiimfiperles mofe tnhtae tpiornosc.e dures to be executed to
cell deviceFsi,g wurhei c5h s hwoewres nthaem aepdp aesa rparnoccee odfu PreLNCu_Bmebcekrh ionf fc SaCse c oofn nmeacnteipdu tloa ttohres c aenlld d pevroic-es, as
InFigure8,asimplediagramisshownasanexampletorecallthebasicsofSFC.The
gramtNhue mcobnefri gfourr athtieo np rsetsasg. eF oofr tthhee Xce-lYl iasx ceos mofp tlheete pdo ascitcioorndiningg t atob lteh, et hseig nnuaml pearitcte vranl uexe polfa ined
Initblockwiththedoubleoutlineistheentrypointoftheprogram. Thelittlerectangle
the coaobrodvien.a Tteh eto s ibgen raela ecxhcehda,n ig.ee., i tsh bea tsaerdg oetnP ao ssiitmiopnl,e i sre pmroovteid perdo.c Fedinuarlely c,a tlhl e(R cPoCm)m, i.uen.,i ac ac-lient–
below,linkedbyaverticalline,representsatransition,i.e.,astepforwardinthegraph
tion eps x eae rtctv uee tri r on n inwfl t oae wsra ;ct c hot e imo r n epl aliet m etdepdc l o e nwm dii etthi n o t naedi d sd p vioti iia no tne r d eaqlo u uee trrb sot y –rt r h eseisgl p anb oae n llssb e ei snm id oe esritds . aeU grn e tts iol . t T hge hut iar s ar an pns a itt t iet oee n rtnh eis r ae-ble to
quirecsdoan sfdeailftyeio tmny iaasnnnadogt revo ecbroiufimsetdpn,leteshxse sipncre oingnardarumiossct ryiicnal ilac ia mslltyapnelexdmeacruedtneitszaetthdioe mncosad. neninecrl.u dedinthespecific
bFliogcuk.reW 5h esnhothwesc otnhdei taiopnpeexaprraenssceed oinf PthLeCla_bBeelciskmhoetf,ft hSeCe cxoecnuntieocnteodft thoe tphroeg crealml dweivllices, as
passtothenextblock,andsoon. IntheSFC,itisalsopossibletomaketheprogramexecute
the configuration stage of the cell is completed according to the signal pattern explained
twoormoreblocksinthesamecycle,usingaparallelbranch. Intheexampleshownin
above. The signal exchange is based on a simple remote procedure call (RPC), i.e., a client–
Figure 8, after var1 has become true, Step2_1 and Step2_2 are both cyclically executed
server interaction implemented via request–response messages. This pattern is able to
untilthevariablevar2becomestrue. Finally,thearrowindicatesajump,meaningthatthe
safelpyr mogaranmageex eccoumtiopnleisxb srcoeungahrtiboasc kint oat shteabnldocakrdniazmeedd masatnhneelarb. elnexttothearrow.
Figure 5. Connection of the PLC_Beckhoff SC to the SCs representing the controllers of the devices
in the assembly cell.
In practice, as depicted in Figure 6, an operation is activated by the execute signal,
and it gives feedback when activity ends by the done signal. Once th e PLC has received
the done signal, it resets the execute signal. Finally, the device resets the done signal as
FigurFei g5u. rCeo5.n
C
n
o
e
n
c
n
ti
e
o
c
n
tio
o
n
f
o
t
f
h
t
e
h e
P
P
L
L
C
C
_
_
B
B
e
ec
c
k
k
h
h
o
o
ff
ff
S C
SC
to
t
t
o
h e
th
SC
e
s
S
r
C
ep
s
r
r
e
e
se
p
n
r
t
e
in
s
g
en
th
ti
e
n
c
g
o n
t
t
h
ro
e
l l
c
e
o
rs
n
o
tr
f
o
th
ll
e
e
d
rs
e v
o
ic
f
e
t
s
h
i
e
n
devices
in thet s hao eso assen sme a mbs bl yi ly t cr cee elllc l.. e ives the information that the execute signal has been reset.
In practice, as depicted in Figure 6, an operation is activated by the execute signal,
and it gives feedback when activity ends by the done signal. Once the PLC has received
the done signal, it resets the execute signal. Finally, the device resets the done signal as
soon as it receives the information that the execute signal has been reset.
FFigiguurere6. 6S.c Shcemheamticaotifct hoef RthPeC RemPCpl oeymedplinoytheedP iLnC t–hdee vPiLceCc–odmemviucnei ccaotimonm. unication.
Figure 6. Schematic of the RPC employed in the PLC–device communication.

Appl. Sci. 2022, 12, 3164  12 of 19

The same logic is applied to devices and robots, leveraging respective controllers’ cod-
ings means to handle the signals’ exchanges. For instance, in the specific case of an ABB
robot, the RPC scheme is managed by a main loop operating in the RAPID code, i.e., the
code running in the robot controller. As shown in Figure 7, the robot acts as any other device:
it receives an execute command from the PLC and it returns a done signal when the re-
quested procedure is finished. As reported in the following pseudocode (Algorithm 3), the
algorithm running on the robot controller includes a standard MAIN section with a loop
implementing the RPC pattern. The code ensures the management of the exchanged signals
and the invoking of the desired procedure according to the value of the procedureNumber.
Algorithm 3 Main section with loop for RPC pattern
MAIN()
| in:                 |     | signal procedureNumber; signal execute          |     |     |                         |     |
| ------------------- | --- | ----------------------------------------------- | --- | --- | ----------------------- | --- |
| out:                |     | signal done; signal do_error                    |     |     |                         |     |
| constant:           |     | integer procedure identifier N_SZ_ObjectHolder  |     |     |                         |     |
|                     |     | integer procedure identifier N_SZ_ToolHolder    |     |     |                         |     |
|                     |     | …                                               |     |     |                         |     |
| 1: INITIALIZATION   |     |                                                 |     |     | ▷ Initialize variables  |     |
Appl.Sci.2022,12,3164 13of19
▷ Loop continuously
| 2: while TRUE do   |           |     |     |     |                      |     |
| ------------------ | --------- | --- | --- | --- | -------------------- | --- |
| 3:                 | done ← 0  |     |     |     | ▷ Reset done signal  |     |
4A: lgoriwthhmil3e  e x e c u t e   ≠  1  d o       ▷   W a i t  until execute signal is true
|     |     | M a i n s e | c ti o n w it h | lo op forRP | C   | p at te r n |
| --- | --- | ----------- | --------------- | ----------- | --- | ----------- |
5:   MAIN() end while
6i:n :  case procsiegdnuarlepNrocuemdubreeNr uomfb er;sig▷n aCleaxlelc ustpeecific robot procedure
| out:              |        | signaldone;signaldo_error                   |                                                 |     |                                    |                     |
| ----------------- | ------ | ------------------------------------------- | ----------------------------------------------- | --- | ---------------------------------- | ------------------- |
| 7:                |        | N_SZ_ObjectHolder: SZ_OBJECTHOLDER          |                                                 |     |                                    |                     |
| constant:         |        | integerprocedureidentifierN_SZ_ObjectHolder |                                                 |     |                                    |                     |
| 8 :               |        | N _ S Z                                     | _ T o o l HNo_lSdZe_rT: oSoZlH_oTldOerOLHOLDER  |     |                                    |                     |
| i n teger         | proced | u re i de                                   | n ti fi e r                                     |     |                                    |                     |
| 9.:. .            |        | …                                           |                                                 |     | ▷ Put other robot procedures here  |                     |
| 1: INITIALIZATION |        |                                             |                                                 |     |                                    | Initializevariables |
| 10:               |        | others:                                     |                                                 |     |                                    |                     |
| 2: whileTRUEdo    |        |                                             |                                                 |     | (cid:3)Loopcontinuously            |                     |
131::  do ne←0do_error ← 1    ▷  URnesketndoownensi gpnraolcedure number
(cid:3)
142::  wehnilede cxeacsuete (cid:54)=1do (cid:3) Waituntilexecutesignalistrue
| 5 : en                   | d w h     | ile |     |                            | ▷   | (cid:3)          |
| ------------------------ | --------- | --- | --- | -------------------------- | --- | ---------------- |
| 1 3 :                    | d on e  ← |  1  |     |                            |     | Set done signal  |
| 6: caseprocedureNumberof |           |     |     | Callspecificrobotprocedure |     |                  |
174::   while exeNcu_StZe _≠O 0b jedcotH  (cid:3)olde r: ▷  W a iHt  u n t il  execute signal is false
|         |                            |     |     | SZ_O          |     | B JEC T O L D E R           |
| ------- | -------------------------- | --- | --- | ------------- | --- | --------------------------- |
| 185::   | end whilNe_ SZ_ToolHolder: |     |     | SZ_TOOLHOLDER |     |                             |
| 9:      |                            | ... |     |               |     | Putotherrobotprocedureshere |
16: end while
| 10: |     | others: |     |     | (cid:3) |     |
| --- | --- | ------- | --- | --- | ------- | --- |
do_error←1
| 11: |     |     |     |     |     | Unknownprocedurenumber |
| --- | --- | --- | --- | --- | --- | ---------------------- |
12: Oentdhecars ceode sections are then im(cid:3)plemented to detail the action required by the specific
done←1
| 13: |     |     |     |     |     | Setdonesignal |
| --- | --- | --- | --- | --- | --- | ------------- |
operation procedure, such as a joint movement, gripper attaching, object grabbing, etc.
14: whileexecute(cid:54)=0do (cid:3) Waituntilexecutesignalisfalse
Such procedures were defined according to the subdivision of the robot tasks in elemen-
| 15: endwhile |     |     |     |     | (cid:3) |     |
| ------------ | --- | --- | --- | --- | ------- | --- |
t1a6r:ye nodpwerhailteions accomplished in the initial design phase of the assembly process.
RAPID Program
Initialization
WHILE loop
RPC
(ProcedureSelection)

FFigiguurer7e. 7Sc. hSecmhaetimcoaftithc eosft rtuhcteu rsetroufcthtuerReA oPIfD thpero RgrAamPIaDdd pedroingtrhaemvi ratduadlecdon itnro ltlhereo vfbirottuhal controller of both
rroobbotostisn cilnucdleuddinedth einc etlhl.e cell.
Intheroboticassemblycelltestcase,theSFCprogramminglanguagehasbeenem-
  ploy edtoprogramthePLC.Figure9reportsaportionoftheprogramtoshowthelogic
usedtobuildit. Eachblockofthediagramcorrespondstoanoperationofacertaindevice.
ThefeaturesoftheSFC,i.e.,parallelbranches,allowedtheactivities,whichmustbeper-
formedatthesametime,tobemanaged. Forinstance,AxisXandAxisYaresupposedtobe
movedsimultaneouslyinordertoreachthetargetpositionofthetableintheminimum
amountoftime.Onthecontrary,thepressmustbeactuatedonlywhenthetablereachesthe
targetposition,asrequiredbythesequentialconstrainthatisexpressedbythetransition
conditionnamedReady.

Appl. Sci. 2022, 12, 3164 13 of 19
4.3. PLC Programming
The SFC graphic language, defined in the international standard IEC 61131-3, has
been chosen as PLC programming means for its suitability to visualize conditional proce-
dures as typically happens in industrial applications. Moreover, this language is easy to
understand, as some basic interpretation rules are provided and can be combined with
other PLC programming languages.
In Figure 8, a simple diagram is shown as an example to recall the basics of SFC. The
Init block with the double outline is the entry point of the program. The little rectangle be-
low, linked by a vertical line, represents a transition, i.e., a step forward in the graph execu-
tion flow; the related condition is pointed out by the label beside it. Until the transition con-
dition is not verified, the program cyclically executes the code included in the specific block.
When the condition expressed in the label is met, the execution of the program will pass to
the next block, and so on. In the SFC, it is also possible to make the program execute two or
more blocks in the same cycle, using a parallel branch. In the example shown in Figure 8,
after var1 has become true, Step2_1 and Step2_2 are both cyclically executed until the vari-
Appl.Sci.2022,12,3164 able var2 becomes true. Finally, the arrow indicates a jump, meanin1g4 othf1a9t the program exe-
cution is brought back to the block named as the label next to the arrow.
Appl. Sci. 2022, 12, 3164 14 of 19
FFigiguurer8e. 8E.x aEmxpalmeopflSeF Cofg SraFpChi cgarlapprohgircaamlm pirnogglarnagmuamgeinfogr PlaLnCg.uage for PLC.
In the robotic assembly cell test case, the SFC programming language has been em-
ployed to program the PLC. Figure 9 reports a portion of the program to show the logic
used to build it. Each block of the diagram corresponds to an operation of a certain device.
The features of the SFC, i.e., parallel branches, allowed the activities, which must be per-
formed at the same time, to be managed. For instance, AxisX and AxisY are supposed to
be moved simultaneously in order to reach the target position of the table in the minimum
amount of time. On the contrary, the press must be actuated only when the table reaches
the target position, as required by the sequential constrain that is expressed by the transi-
tion condition named Ready.
FFiigguurere9 .9P. oProtirotnioonf tohfe tPhLeC PpLroCg rparmogdreavmelo dpeevdefloorptheedr foobro ttihcea srsoebmobtliyc taesstsecamseb.ly test case.
5. ToolValidationandResults
5. Tool Validation and Results
TheimplementedintegrationbetweenRSandTCwastestedagainstthepossibilityto
The implemented integration between RS and TC was tested against the possibility
performaneffectiveVCofthecell.Inparticular,aseriesofassemblytasksweredefinedand
stiom puelartfeodrmto aidne netfiffeyctthiveeo pVtCim oafl tahssee cmeblll.y Isne qpuaernticceufloarrt,h ae sperroipeso soefd agsesaermbobxlyas tsaesmkbsl wy ere defined
taanskd. sFiomrualabteettde rtou niddeenrsttiafnyd tihneg oopfttihmeaexl eacsusteemdbwlyor ske,qauveindecoe fsohro wthien gprthoepVosCedof gtehaerbox assem-
absl-yse tmabskly. cFeollri sap broevttideer duinndtheersStuapnpdleimngen otaf rtyhMe aetxeericaulSteedct iwono.rIkn,t hae vviiddeeoo, sthheoPwLiCnagn tdhe VC of the
thevirtualcellinRSaredisplayedside-by-side. Inparticular,anexampleoftheassembly
assembly cell is provided as additional material to this paper. In the video, the PLC and
sequencewasshownthathasbeenrecordedtoillustratethecommandactivationfromthe
the virtual cell in RS are displayed side-by-side. In particular, an example of the assembly
PLCandthevariationinthesignals’statuses,bothinTCandRS.
sequence was shown that has been recorded to illustrate the command activation from
Thewholegearboxassemblytaskwassubdividedinalistofelementaryoperationsto
btheea rPraLnCge adnidn pthroep verasreiaqtuieonnc eins. tThhee seixganmaplsle’s sotaftcuonsesisd, ebreodtho piner TatCio nasnidn cRluSd. e:
• LTochkeI nwsehrto:lleo cgaetearabpouxs haisnsgeminsbelryt itnatshke wpraess ssaunbddaitvtaidchedit tion tah eliesnt doef fefelcetmore;ntary operations
to be arranged in proper sequences. The examples of considered operations include:
•
LockInsert: locate a pushing insert in the press and attach it to the end effector;
•
UnlockInsert: detach an insert from the press and locate in the magazine;
•
PickBearing: grab a bearing with a gripper;
•
PlaceBearing: locate a bearing on its assembly position;
•
ScrewStud: screw a threaded stud by the torque-controlled screwdriver.
Following the architecture described in the previous section, the code in the control-
lers of the robots and other cell devices is in charge of activating the operations according
to the signals received by the PLC. The actual sequence of operations is determined by the
PLC program. Therefore, several PLC programs, including different sequences of opera-
tions were generated and tested.
From the experimental activity, it emerges that, in the virtual environment, various
aspects can be verified and optimized. At first, the appropriate sequence of actions and the
correctness of signals exchange between PLC and controllers must be verified and opti-
mized. Therefore, PLC program robustness is verified and tested in normal operating con-
ditions as well as in fault events caused by errors, safety alarms or unexpected situations.
The reachability of the desired locations, the quality and fluency of the movements,
the absence of collisions, as well as the overall time required to accomplish the tasks are
other significant tasks that can be verified before commissioning the real cell to ensure a
successful result.
Finally, the VC was analyzed as a means to optimize the sequence of the operations
coordinated by the PLC. The absence of collisions between two robots sharing their work-
space (see Figure 10), the interchangeability of the single assembly operation, and the pos-
sibility to parallelize actions performed in different zones of the cell make the solution
space of all of the possible operating sequences quite vast. This opens up to the possibility

Appl.Sci.2022,12,3164 15of19
• UnlockInsert: detachaninsertfromthepressandlocateinthemagazine;
• PickBearing: grababearingwithagripper;
• PlaceBearing: locateabearingonitsassemblyposition;
• ScrewStud: screwathreadedstudbythetorque-controlledscrewdriver.
Followingthearchitecturedescribedintheprevioussection,thecodeinthecontrollers
oftherobotsandothercelldevicesisinchargeofactivatingtheoperationsaccordingtothe
signalsreceivedbythePLC.TheactualsequenceofoperationsisdeterminedbythePLC
program. Therefore,severalPLCprograms,includingdifferentsequencesofoperations
weregeneratedandtested.
Fromtheexperimentalactivity,itemergesthat,inthevirtualenvironment,various
aspectscanbeverifiedandoptimized. Atfirst,theappropriatesequenceofactionsand
the correctness of signals exchange between PLC and controllers must be verified and
optimized. Therefore,PLCprogramrobustnessisverifiedandtestedinnormaloperating
conditionsaswellasinfaulteventscausedbyerrors,safetyalarmsorunexpectedsituations.
Thereachabilityofthedesiredlocations,thequalityandfluencyofthemovements,
theabsenceofcollisions,aswellastheoveralltimerequiredtoaccomplishthetasksare
othersignificanttasksthatcanbeverifiedbeforecommissioningtherealcelltoensurea
successfulresult.
Finally,theVCwasanalyzedasameanstooptimizethesequenceoftheoperationsco-
ordinatedbythePLC.Theabsenceofcollisionsbetweentworobotssharingtheirworkspace
Appl. Sci. 2022, 12, 3164 (seeFigure10),theinterchangeabilityofthesingleassemblyoperation,andtheposs1i5b iolfi t1y9
to parallelize actions performed in different zones of the cell make the solution space
ofallofthepossibleoperatingsequencesquitevast. Thisopensuptothepossibilityof
oopf toimptiizminizginthge thoer doerrdeorf othf ethoep oepraetriaotniosnrse rqeuqeusetesdtedo fotfh tehetw twoor orboobtostsa nanddo oththeerrd deevviciceessi inn
orderminimizetheoverallaccomplishingtime.
order minimize the overall accomplishing time.
FFiigguurree1 100.. TThhee sshhaarriinngg ooff tthhee wwoorrkkssppaaccee ooff tthhee ttwwoo rroobboottss mmaakkeess iitt eesssseennttiiaall ttoo ssttuuddyy tthhee aapppprroopprriiaattee
sseeqquueenncceess ooff aaccttiioonnss iinn aav virirttuuaalle ennvviriroonnmmeenntt ttooa avvooididc coolllilsisiioonnss.. IInn tthhee fifigguurree,, RRoobboott 22 loloccaattiinngg aa
bbeeaarriinngg,,c coolllildideessw witithhR Roobboott1 1w whhilielei titi siss sccrreewwiningga as stutudd..
FFiigguurree 1111 rreeppoorrttss aann eexxaammpplele oof ftetsetsst psepreforfromremde tdo tiodeindteinfyt itfhyet ohpetiompatilm seaqluseenqcuee npceer-
pmerumtautitoanti oofn thoef sthame sea lmiste olfi sotpoefraotipoenrsa.t Iino nths.e fIinguthree, tfihgrueere d,itfhferreeentd sifefqeureenntcesse qaruee rnecpeosraterde,
rreepsopretcetdiv,erleys,p aescstiigvneleyd, atoss tighne epdotsoititohneinpgo stiatibolne ianxgesta, bthlee apxreess,st, haenpdr tehses, tawnod rtohbeottws.o Trhoeb ocotsl-.
Tohreedc oblaorrse sdhboawr sthseh oawctivthaetioanct tivimateiso noft tihmee dseovficthese, dase vhiicgehsl,igahstheidg hblyi gthhete ldegbeyndthse inle tgheen fdigs-
iunreths.e Itfi igsu erveisd.enItt ihsoewv isdoemnte hoopwerastoiomnes coapne rbaet ipoanrsalclealnizbede, pwahraillele ilniz oedth,ewr mhiolemienntost,h tehre
mopoemraebnitlsi,tyth oefo ap edreavbiicleit ymoufsat dbeev siucespmeunsdtebde usunstipl esnpdeecdifiuc natciltisopnesc iafirce accotmionpsleateredc. oHmopwleetveedr.,
Hlooowkienvge ra,t ltohoek tihnrgeea dtitfhfeeretnhtr eoepedriaftfieorne nsteqoupeenrcaetiso int esmeqeurgeensc ethsaitt deimffeerregnets letvhealts doiff foepreernat-
levels of operations can simultaneously be reached. For instance, in the reported case,
tions can simultaneously be reached. For instance, in the reported case, (a) the operations
(a)theoperationsperformedbyRobot1(yellowband),whichisthedevicewithamajor
performed by Robot 1 (yellow band), which is the device with a major workload in the cell,
are fragmented, and the overall cycle time is degraded due to frequent downtime periods.
(a)

Appl. Sci. 2022, 12, 3164 15 of 19
of optimizing the order of the operations requested of the two robots and other devices in
order minimize the overall accomplishing time.
Figure 10. The sharing of the workspace of the two robots makes it essential to study the appropriate
sequences of actions in a virtual environment to avoid collisions. In the figure, Robot 2 locating a
bearing, collides with Robot 1 while it is screwing a stud.
Figure 11 reports an example of tests performed to identify the optimal sequence per-
mutation of the same list of operations. In the figure, three different sequences are reported,
respectively, assigned to the positioning table axes, the press, and the two robots. The col-
ored bars show the activation times of the devices, as highlighted by the legends in the fig-
ures. It is evident how some operations can be parallelized, while in other moments, the
Appl.Sci.2022,12,3164 16of19
operability of a device must be suspended until specific actions are completed. However,
looking at the three different operation sequences it emerges that different levels of opera-
tions can simultaneously be reached. For instance, in the reported case, (a) the operations
pweroforkrmloeadd biny tRhoebcoetll 1, a(ryeelflroawgm beanntde)d, ,wahnidchth ies othvee rdaelvlcicyec lweittihm ae misadjoerg rwaodrekdlodaude itno tfhreeq cueelln, t
ardeo fwrangtmimeentpeedr,i oandds. the overall cycle time is degraded due to frequent downtime periods.
Appl. Sci. 2022, 12, 3164 16 of 19
(a)
(b)
(c)
FFiigguurree 1111.. RReessuullttss oobbttaaiinneedd bbyyt htheeV VCCa pappproraocahc.hA. Ab ebtetettrear lateltrenrantiaotnioonf oofp oepraetriaotniosnasll oawlloswasr ead ruecdtiuocn-
tiniotnh eino vtherea ollvceerlallcly ccelellt icmycelea ntdimeen earngdy ceonnesrugmy pcotinosnu:m(ap)tiinointi:a l(a(s) uibn-iotipatl im(sualb)-soepqtuimenacle) ;s(ebq)uimenpcreo; v(ebd)
improved sequence and (c) final (refined) sequence.
sequenceand(c)final(refined)sequence.
TThhee iimmpprroovveedds seeqquueenncecesso foof poepreartaiotinosnlse aldeasdtos aton aonv eorvalelrcayllc lceytcimle etirmedeu rcetidouncotifo3n0 %of,
3i.0e%.,f, rio.em., ftrhoemin tihtiea iln1i0ti1als 1t0o1a sn tion taenr minetedrimateedsiuabte- osputbim-opaltismolaul tsioolnu(tii.oen., (7i4.e.s,, 7c4a sse, c(abs))e a(bn)d)
afinndal lfyin,taollay,s taov ian sgaovfinmgo oref mseocoren dsesc(oi.ned.,s7 1(i.se,.c, a7s1e s(,c c))a.sAe s(ca))f.u Artsh ae rfudretmheorn dstermatioonnstorfatthioenV oCf
tthooe lVpCo tteonotli apliotiteesn,ttihaleitsieasm, ethpei cstaumree rpeipcoturtrse trheepRorStse stthime RatSi oenstoimftahteiotno toafl ethnee rtgoytarle eqnueirrgedy
required by the motors of the robots during the entire work cycle, comparing the sub-
optimal and the optimal sequences. It can be observed that the last case provides an over-
all reduction in energy consumption of 3% (i.e., from 17,067 J to 16,556 J). It is worth noting
that, based on the declared design intents, any other output made available by RS simu-
lation can be utilized as a performance index in the optimization study.
As a further development, an additional optimization algorithm may be foreseen to
generate candidate sequences to be sent to the PLC, and then automatically elaborated in
the proposed VC system to check for the resulting performance, such as collision avoid-
ance and cycle time. Such a system would be helpful in searching for optimal solutions in
an automatic, faster and more reliable way.

Appl.Sci.2022,12,3164 17of19
bythemotorsoftherobotsduringtheentireworkcycle,comparingthesub-optimaland
theoptimalsequences. Itcanbeobservedthatthelastcaseprovidesanoverallreduction
inenergyconsumptionof3%(i.e.,from17,067Jto16,556J).Itisworthnotingthat,based
onthedeclareddesignintents,anyotheroutputmadeavailablebyRSsimulationcanbe
utilizedasaperformanceindexintheoptimizationstudy.
Asafurtherdevelopment,anadditionaloptimizationalgorithmmaybeforeseento
generatecandidatesequencestobesenttothePLC,andthenautomaticallyelaboratedin
theproposedVCsystemtocheckfortheresultingperformance,suchascollisionavoidance
andcycletime. Suchasystemwouldbehelpfulinsearchingforoptimalsolutionsinan
automatic,fasterandmorereliableway.
6. Conclusions
VCtechnologyisanefficienttoolforcompaniestobecompetitivesinceitallowsthe
commissioningactivitiesofaproductionsystemtobeanticipatedduringthedesignphase,
offering the chance to find errors and improve the project when engaged investments
are still relatively low. On the other hand, mechatronic systems are often complex and
composed by devices from different producers, each one recurring for a different soft-
wareplatform. Consequently,toolsthatvalidateandverifytheinteractionsofdifferent
controllers codes become strategic in the VC perspective. In this context, the tools that
enablethecommunicationbetweentwocommonsoftwareintheindustrialautomation
panorama,RSandTC,wereproposed.Theyallowasignalexchangetobeeasilyestablished
betweenPLCandotherdevices,asisthecaseinrealsystems. Thetooldemonstratedan
effectiveperformance,andtheconnectionwassolidandreliable. Themainoutcomeisthat
bothPLCandrobotprogramscanbecheckedconcurrentlyandoptimizedbeforebeing
implementationinthephysicalsystem. Theeffectofanychangeatcodelevelcanbetested
onthewholesysteminasingleenvironmentwithouttheneedtosimplifyoridealizethe
partsbehavior.
Beyondtheseencouragingresults,futureworkcouldbefocusedontheimprovement
oftheworkingperformanceoftheapplication,aimingforamoreefficientcommunication
code to reduce latency. Moreover, since both RS and TC are proprietary solutions that
onlycomprisevendor-specificdevices, thepresentedapproachcaneitherbereplicated
withothercommercialplatformsorevenextendedtogeneral-purposeplatforms,where
productsfrommanyvendorscanbesimulated.
SupplementaryMaterials:AdemonstrativevideooftheproposedVCtoolcanbeviewedathttps:
//www.youtube.com/watch?v=QG22pVg31XI(accessedon24February2022).
AuthorContributions:Conceptualization,R.R.andF.N.;methodology,R.R.andP.B.;software,F.N.;
validation,F.N.;writing—originaldraftpreparation,R.R.andP.B.;writing—reviewandediting,P.B.
andM.P.(MargheritaPeruzzini).;coordination,M.P.(MarcelloPellicciari).Allauthorshavereadand
agreedtothepublishedversionofthemanuscript.
Funding: ThisresearchwasfundedbytheEuropeanCommunity’sHORIZON2020programme
undergrantagreementNo.958303(PENELOPE).
InstitutionalReviewBoardStatement:Notapplicable.
InformedConsentStatement:Notapplicable.
ConflictsofInterest:Theauthorsdeclarenoconflictofinterest.
References
1. Oztemel,E.;Gursev,S.LiteratureReviewofIndustry4.0andRelatedTechnologies.J.Intell.Manuf.2020,31,127–182.[CrossRef]
2. Waris,M.M.;Sanin,C.;Szczerbicki,E.SmartInnovationEngineering(SIE):Experience-BasedProductInnovationSystemfor
Industry4.0.InAdvancesinIntelligentSystemsandComputing;Springer:Cham,Switzerland,2018;Volume657,pp.379–388.
3. Kamble,S.S.;Gunasekaran,A.;Gawankar,S.A.SustainableIndustry4.0Framework:ASystematicLiteratureReviewIdentifying
theCurrentTrendsandFuturePerspectives.ProcessSaf.Environ.Prot.2018,117,408–425.[CrossRef]

Appl.Sci.2022,12,3164 18of19
4. Sony,M.;Naik,S.KeyIngredientsforEvaluatingIndustry4.0ReadinessforOrganizations:ALiteratureReview.Benchmarking
2020,27,2213–2232.[CrossRef]
5. Kusiak,A.SmartManufacturing.Int.J.Prod.Res.2018,56,508–517.[CrossRef]
6. Lattanzi,L.;Raffaeli,R.;Peruzzini,M.;Pellicciari,M.DigitalTwinforSmartManufacturing:AReviewofConceptstowardsa
PracticalIndustrialImplementation.Int.J.Comput.Integr.Manuf.2021,34,567–597.[CrossRef]
7. Chau,K.Y.;Tang,Y.M.;Liu,X.;Ip,Y.K.;Tao,Y.InvestigationofCriticalSuccessFactorsforImprovingSupplyChainQuality
ManagementinManufacturing.Enterp.Inf.Syst.2021,15,1418–1437.[CrossRef]
8. Noga,M.;Juhás,M.;Gulan,M.HybridVirtualCommissioningofaRoboticManipulatorwithMachineVisionUsingaSingle
Controller.Sensors2022,22,1621.[CrossRef]
9. Aromaa,S.VirtualPrototypinginDesignReviewsofIndustrialSystems. InProceedingsofthe21stInternationalAcademic
MindtrekConference,AcademicMindtrek,NewYork,NY,USA,20–21September2017;AssociationforComputingMachinery,
Inc.:TimesSquare,NY,USA,2017.
10. Mejía-Gutiérrez,R.;Carvajal-Arango,R.DesignVerificationthroughVirtualPrototypingTechniquesBasedonSystemsEngineer-
ing.Res.Eng.Des.2017,28,477–494.[CrossRef]
11. Charif,A.;Busnot,G.;Mameesh,R.;Sassolas,T.;Ventroux,N.FastVirtualPrototypingforEmbeddedComputingSystemsDesign
andExploration.InProceedingsoftheACMInternationalConferenceProceedingSeries,NewYork,NY,USA,19–21September
2019;AssociationforComputingMachinery:TimesSquare,NY,USA,2019;VolumePartF148382.
12. Pellicciari,M.;Vergnano,A.;Berselli,G.Hardware-in-the-LoopMechatronicVirtualPrototypingofaHigh-SpeedCapsuleFilling
Machine.InProceedingsoftheMESA2014—10thIEEE/ASMEInternationalConferenceonMechatronicandEmbeddedSystems
andApplications,Senigallia,Italy,10–12September2014;InstituteofElectricalandElectronicsEngineersInc.:Piscataway,NJ,
USA,24October2014.
13. Tang,Y.M.;Chau,K.Y.;Fatima,A.;Waqas,M.Industry4.0TechnologyandCircularEconomyPractices:BusinessManagement
StrategiesforEnvironmentalSustainability.Environ.Sci.Pollut.Res.2022,1–18.[CrossRef]
14. Pérez,L.;Rodríguez-Jiménez,S.;Rodríguez,N.;Usamentiaga,R.;García,D.F.DigitalTwinandVirtualRealityBasedMethodology
forMulti-RobotManufacturingCellCommissioning.Appl.Sci.2020,10,3633.[CrossRef]
15. VatankhahBarenji,A.;Liu,X.;Guo,H.;Li,Z.ADigitalTwin-DrivenApproachtowardsSmartManufacturing:ReducedEnergy
ConsumptionforaRoboticCell.Int.J.Comput.Integr.Manuf.2021,34,844–859.[CrossRef]
16. Ribeiro,F.M.;Pires,J.N.;Azar,A.S.ImplementationofaRobotControlArchitectureforAdditiveManufacturingApplications.
Ind.RobotInt.J.Robot.Res.Appl.2019,46,73–82.[CrossRef]
17. Gadaleta,M.;Pellicciari,M.;Berselli,G.OptimizationoftheEnergyConsumptionofIndustrialRobotsforAutomaticCode
Generation.Robot.Comput.-Integr.Manuf.2019,57,452–464.[CrossRef]
18. Makris,S.;Michalos,G.;Chryssolouris,G.VirtualCommissioningofanAssemblyCellwithCooperatingRobots.Adv.Decis.Sci.
2012,2012,428060.[CrossRef]
19. Oppelt,M.;Wolf,G.;Urbas,L.TowardsanIntegratedUseofSimulationwithintheLife-CycleofaProcessPlant:APrototypical
Implementation.InProceedingsoftheIEEEInternationalConferenceonEmergingTechnologiesandFactoryAutomation,ETFA,
Luxembourg,8–11September2015;InstituteofElectricalandElectronicsEngineersInc.:Piscataway,NY,USA,2015.
20. Liu,Z.;Suchold,N.;Diedrich,C.7VirtualCommissioningofAutomatedSystems;IntechOpen:London,UK,2012.
21. Hoffmann,P.;Schumann,R.;Maksoud,T.M.A.;Premier,G.C.VirtualCommissioningofManufacturingSystemsAReviewAnd
NewApproachesForSimplification.InProceedingsoftheECMS,KualaLumpur,Malaysia,1–4June2010.
22. Lechler,T.;Fischer,E.;Metzner,M.;Mayr,A.;Franke,J.VirtualCommissioning—ScientificReviewandExploratoryUseCasesin
AdvancedProductionSystems.ProcediaCIRP2019,81,1125–1130.[CrossRef]
23. Langmann,R.;Stiller,M.ThePLCasaSmartServiceinIndustry4.0ProductionSystems.Appl.Sci.2019,9,3815.[CrossRef]
24. Barbieri,G.;Bertuzzi,A.;Capriotti,A.;Ragazzini,L.;Gutierrez,D.;Negri,E.;Fumagalli,L.AVirtualCommissioningBased
MethodologytoIntegrateDigitalTwinsintoManufacturingSystems.Prod.Eng.2021,15,397–412.[CrossRef]
25. Fernández,I.A.;Eguía,M.A.;Echeverría,L.E.VirtualCommissioningofaRoboticCell:AnEducationalCaseStudy.InProceedings
ofthe201924thIEEEInternationalConferenceonEmergingTechnologiesandFactoryAutomation(ETFA),Zaragoza,Spain,
10–13September2019;pp.820–825.
26. Lee,C.G.;Park,S.C.SurveyontheVirtualCommissioningofManufacturingSystems. J.Comput. Des. Eng. 2014,1,213–222.
[CrossRef]
27. Eguti,C.C.A.;Trabasso,L.G.TheVirtualCommissioningTechnologyAppliedintheDesignProcessofaFlexibleAutomation
System.J.Braz.Soc.Mech.Sci.Eng.2018,40,196.[CrossRef]
28. Gomes,C.;Thule,C.;Broman,D.;Larsen,P.G.;Vangheluwe,H.Co-Simulation:StateoftheArt.arXiv2017,arXiv:1702.00686.
29. Schamp,M.;vandeGinste,L.;Hoedt,S.;Claeys,A.;Aghezzaf,E.H.;Cottyn,J.VirtualCommissioningofIndustrialControl
Systems—A3DDigitalModelApproach.ProcediaManuf.2019,39,66–73.[CrossRef]
30. Vermaak,H.;Niemann,J.VirtualCommissioning: ATooltoEnsureEffectiveSystemIntegration. InProceedingsofthe2017
IEEEInternationalWorkshopofElectronics,Control,Measurement,SignalsandtheirApplicationtoMechatronics,ECMSM,San
Sebastian,Spain,24–26May2017;InstituteofElectricalandElectronicsEngineersInc.:Piscataway,NY,USA,9June2017.

Appl.Sci.2022,12,3164 19of19
31. Tebani,K.;Plateaux,R.;Puyenchet,C.;Penas,O.;Baroux,C.;Limou,S.Real-TimeCommunicationbetweenPLCandDymola
forVirtualCommissioningApplication.InProceedingsoftheInternationalConferenceonAdvancedSystemsandEmergent
Technologies,IC_ASET2020,Hammamet,Tunisia,15–18December2020;InstituteofElectricalandElectronicsEngineersInc.:
Piscataway,NY,USA,15December2020;pp.83–88.
32. Brazina,J.;Vetiska,J.;Stanek,V.;Bradac,F.;Holub,M.VirtualCommissioningasPartoftheEducationalProcess.InProceedings
ofthe202019thInternationalConferenceonMechatronics—Mechatronika,ME2020,Prague,CzechRepublic,2–4December
2020;InstituteofElectricalandElectronicsEngineersInc.:Piscataway,NY,USA,2December2020.
33. Guerrero,L.V.;López,V.V.;Mejía,J.E.VirtualCommissioningwithProcessSimulation(Tecnomatix).Comput.-AidedDes.Appl.
2014,11,S11–S19.[CrossRef]
34. Min,B.-K.;Huang,Z.;Pasek,Z.J.;Yip-Hoi,D.;Husted,F.;Marker,S.Integrationofreal-timecontrolsimulationtoavirtual
manufacturingenvironment.J.Adv.Manuf.Syst.2002,1,67–87.[CrossRef]
35. Bilancia,P.;Berselli,G.;Bruzzone,L.;Fanghella,P.ACAD/CAEIntegrationFrameworkforAnalyzingandDesigningSpatial
CompliantMechanismsviaPseudo-Rigid-BodyMethods.Robot.Comput.-Integr.Manuf.2019,56,287–302.[CrossRef]
36. Park,H.S.;Dang,X.P.StructuralOptimizationBasedonCAD–CAEIntegrationandMetamodelingTechniques.Comput.-Aided
Des.2010,42,889–902.[CrossRef]
37. Cheraghpour,F.;Vaezi,M.;ShooriJazeh,H.E.;Moosavian,S.A.A.DynamicModelingandKinematicSimulationofStubli©TX40
RobotUsingMATLAB/ADAMSCo-Simulation.InProceedingsofthe2011IEEEInternationalConferenceonMechatronics,ICM
2011—Proceedings,Istanbul,Turkey,13–15April2011;pp.386–391.
38. Bilancia,P.;Berselli,G.;Palli,G.VirtualandPhysicalPrototypingofaBeam-BasedVariableStiffnessActuatorforSafeHuman-
MachineInteraction.Robot.Comput.-Integr.Manuf.2020,65,101886.[CrossRef]
39. Raffaeli,R.;Neri,F.;Peruzzini,M.;Berselli,G.;Pellicciari,M.VirtualPrototypingasaSupportingToolfortheDesignofComplex
RoboticCells.InProceedingsoftheInternationalConferenceonDesign,Simulation,Manufacturing,TheInnovationExchange
2021,Lviv,Ukraine,8–11June,2021;Springer:Cham,Switzerland,2021.