PDF Download
3703155.pdf
01 March 2026
Total Citations: 882
. Total Downloads:
.
Latest updates: hps://dl.acm.org/doi/10.1145/3703155 43577
.
. . Publish . ed: 24 January 2025
RESEARCH-ARTICLE Online AM: 20 November 2024
A Survey on Hallucination in Large Language Models: Accepted: 24 September 2024
Revised: 02 August 2024
Principles, Taxonomy, Challenges, and Open estions Received: 08 December 2023
.
.
Citation in BibTeX format
LEI HUANG, Harbin Institute of Technology, Harbin, Heilongjiang, China
.
.
.
WEIJIANG YU, Huawei Technologies Co., Ltd., Shenzhen, Guangdong,
China
.
WEITAO MA, Harbin Institute of Technology, Harbin, Heilongjiang, China
.
WEIHONG ZHONG, Harbin Institute of Technology, Harbin,
Heilongjiang, China
.
ZHANGYIN FENG, Harbin Institute of Technology, Harbin, Heilongjiang,
China
.
HAOTIAN WANG, Harbin Institute of Technology, Harbin, Heilongjiang,
China
.
View all
.
.
Open Access Support provided by:
.
Huawei Technologies Co., Ltd.
.
Harbin Institute of Technology
.
ACM Transactions on Information Systems, Volume 43, Issue 2 (March 2025)
hps://doi.org/10.1145/3703155
EISSN: 1558-2868
.

A Survey on Hallucination in Large Language Models:
Principles, Taxonomy, Challenges, and Open Questions
LEIHUANG,HarbinInstituteofTechnology,Harbin,China
WEIJIANGYU,HuaweiInc.,Shenzhen,China
WEITAOMA,WEIHONGZHONG,ZHANGYINFENG,andHAOTIANWANG,Harbin
InstituteofTechnology,Harbin,China
QIANGLONGCHENandWEIHUAPENG,HuaweiInc.,Shenzhen,China
XIAOCHENGFENG,BINGQIN,andTINGLIU,HarbinInstituteofTechnology,Harbin,China
Theemergenceoflargelanguagemodels(LLMs)hasmarkedasignificantbreakthroughinnaturallanguage
processing (NLP), fueling a paradigm shift in information acquisition. Nevertheless, LLMs are prone to
hallucination,generatingplausibleyetnonfactualcontent.Thisphenomenonraisessignificantconcernsover
thereliabilityofLLMsinreal-worldinformationretrieval(IR)systemsandhasattractedintensiveresearchto
detectandmitigatesuchhallucinations.Giventheopen-endedgeneral-purposeattributesinherenttoLLMs,
LLMhallucinationspresentdistinctchallengesthatdivergefrompriortask-specificmodels.Thisdivergence
highlightstheurgencyforanuancedunderstandingandcomprehensiveoverviewofrecentadvancesin
LLMhallucinations.Inthissurvey,webeginwithaninnovativetaxonomyofhallucinationintheeraof
LLMandthendelveintothefactorscontributingtohallucinations.Subsequently,wepresentathorough
overviewofhallucinationdetectionmethodsandbenchmarks.Ourdiscussionthentransferstorepresentative
methodologiesformitigatingLLMhallucinations.Additionally,wedelveintothecurrentlimitationsfaced
byretrieval-augmentedLLMsincombatinghallucinations,offeringinsightsfordevelopingmorerobustIR
systems.Finally,wehighlightthepromisingresearchdirectionsonLLMhallucinations,includinghallucination
inlargevision-languagemodelsandunderstandingofknowledgeboundariesinLLMhallucinations.
CCSConcepts:•Computingmethodologies→Naturallanguagegeneration;•Generalandreference
→Surveysandoverviews;
AdditionalKeyWordsandPhrases:LargeLanguageModels,Hallucination,Factuality,Faithfulness
Authors’ContactInformation:LeiHuang,HarbinInstituteofTechnology,Harbin,China;e-mail:lhuang@ir.hit.edu.cn;
WeijiangYu,HuaweiInc.,Shenzhen,China;e-mail:weijiangyu8@gmail.com;WeitaoMa,HarbinInstituteofTechnol-
ogy,Harbin,China;e-mail:wtma@ir.hit.edu.cn;WeihongZhong,HarbinInstituteofTechnology,Harbin,China;e-mail:
whzhong@ir.hit.edu.cn;ZhangyinFeng,HarbinInstituteofTechnology,Harbin,China;e-mail:zyfeng@ir.hit.edu.cn;
HaotianWang,HarbinInstituteofTechnology,Harbin,China;e-mail:wanght1998@gmail.com;QianglongChen,Huawei
Inc., Shenzhen, China; e-mail: chenqianglong.ai@gmail.com; Weihua Peng, Huawei Inc., Shenzhen, China; e-mail:
pengwh.hit@gmail.com;XiaochengFeng(correspondingauthor),HarbinInstituteofTechnology,Harbin,China;e-mail:
xcfeng@ir.hit.edu.cn;BingQin,HarbinInstituteofTechnology,Harbin,China;e-mail:qinb@ir.hit.edu.cn;TingLiu,Harbin
InstituteofTechnology,Harbin,China;e-mail:tliu@ir.hit.edu.cn.
Permissiontomakedigitalorhardcopiesofallorpartofthisworkforpersonalorclassroomuseisgrantedwithoutfee
providedthatcopiesarenotmadeordistributedforprofitorcommercialadvantageandthatcopiesbearthisnoticeandthe
fullcitationonthefirstpage.Copyrightsforcomponentsofthisworkownedbyothersthantheauthor(s)mustbehonored.
Abstractingwithcreditispermitted.Tocopyotherwise,orrepublish,topostonserversortoredistributetolists,requires
priorspecificpermissionand/orafee.Requestpermissionsfrompermissions@acm.org.
©2025Copyrightheldbytheowner/author(s).PublicationrightslicensedtoACM.
ACM1558-2868/2025/1-ART42
https://doi.org/10.1145/3703155
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

42:2 L.Huangetal.
ACMReferenceformat:
LeiHuang,WeijiangYu,WeitaoMa,WeihongZhong,ZhangyinFeng,HaotianWang,QianglongChen,Weihua
Peng,XiaochengFeng,BingQin,andTingLiu.2025.ASurveyonHallucinationinLargeLanguageModels:
Principles,Taxonomy,Challenges,andOpenQuestions.ACMTrans.Inf.Syst.43,2,Article42(January2025),
55pages.
https://doi.org/10.1145/3703155
1 Introduction
Recently,theemergenceoflargelanguagemodels(LLMs)[379],exemplifiedbyLLaMA[295,296],
Claude[9],Gemini[7,256]andGPT-4[229],hasusheredinasignificantparadigmshiftinnatu-
rallanguageprocessing(NLP),achievingunprecedentedprogressinlanguageunderstanding
[115,123],generation[369,389]andreasoning[57,148,247,322,350].Furthermore,theexten-
sivefactualknowledgeencodedwithinLLMshasdemonstratedconsiderableadvancementsin
leveragingLLMsforinformationseeking[6,243],potentiallyreshapingthelandscapeofinforma-
tionretrieval(IR)systems[390].Nevertheless,intandemwiththeseremarkableadvancements,
concerns have arisen about the tendency of LLMs to generate hallucinations [15, 104], result-
ing in seemingly plausible yet factually unsupported content. Further compounding this issue
isthecapabilityofLLMstogeneratehighlyconvincingandhuman-likeresponses[261],which
makesdetectingthesehallucinationsparticularlychallenging,therebycomplicatingthepractical
deploymentofLLMs,especiallyreal-worldIRsystemsthathaveintegratedintoourdailylives
likechatbots[8,228],searchengines[4,211],andrecommendersystems[96,168].Giventhatthe
informationprovidedbythesesystemscandirectlyinfluencedecision-making,anymisleading
informationhasthepotentialtospreadfalsebeliefs,orevencauseharm.
Notably,hallucinationsinconventionalnaturallanguagegeneration(NLG)taskshavebeen
extensively studied [124, 134], with hallucinations defined as generated content that is either
nonsensicalorunfaithfultotheprovidedsourcecontent.Thesehallucinationsarecategorizedinto
twotypes:intrinsichallucination,wherethegeneratedoutputcontradictsthesourcecontent,and
extrinsichallucination,wherethegeneratedoutputcannotbeverifiedfromthesource.However,
given their remarkable versatility across tasks [15, 30], understanding hallucinations in LLMs
presents a unique challenge compared to models tailored for specific tasks. Besides, as LLMs
typicallyfunctionasopen-endedsystems,thescopeofhallucinationencompassesabroaderconcept,
predominantlymanifestingfactualerrors.Thisshiftnecessitatesareevaluationandadjustment
of the existing taxonomy of hallucinations, aiming to enhance its adaptability in the evolving
landscapeofLLMs.
Inthissurvey,weproposearedefinedtaxonomyofhallucinationtailoredspecificallyforapplica-
tionsinvolvingLLMs.Wecategorizehallucinationintotwoprimarytypes:factualityhallucination
andfaithfulnesshallucination.Factualityhallucinationemphasizesthediscrepancybetweengen-
erated content and verifiable real-world facts, typically manifesting as factual inconsistencies.
Conversely,faithfulnesshallucinationcapturesthedivergenceofgeneratedcontentfromuserinput
orthelackofself-consistencywithinthegeneratedcontent.Thiscategoryisfurthersubdivided
intoinstructioninconsistency,wherethecontentdeviatesfromtheuser’soriginalinstruction;
contextinconsistency,highlightingdiscrepanciesfromtheprovidedcontext;andlogicalincon-
sistency,pointingoutinternalcontradictionswithinthecontent.Suchcategorizationrefinesour
understandingofhallucinationsinLLMs,aligningitcloselywiththeircontemporaryusage.
DelvingintotheunderlyingcausesofhallucinationsinLLMsisessentialnotmerelyforenhanc-
ingthecomprehensionofthesephenomenabutalsoforinformingstrategiesaimedatalleviating
them.RecognizingthemultifacetedsourcesofLLMhallucinations,oursurveyidentifiespotential
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

ASurveyonHallucinationinLargeLanguageModels 42:3
contributorsintothreemainaspects:data,training,andinferencestages.Thiscategorizationallows
ustospanabroadspectrumoffactors,providingaholisticviewoftheoriginsandmechanismsby
whichhallucinationsmayarisewithinLLMsystems.Furthermore,wecomprehensivelyoutlinea
varietyofeffectivedetectionmethodsspecificallydevisedfordetectinghallucinationsinLLMs,as
wellasanexhaustiveoverviewofbenchmarksrelatedtoLLMhallucinations,servingasappropriate
testbedstoassesstheextentofhallucinationsgeneratedbyLLMsandtheefficacyofdetectionmeth-
ods.Beyondevaluation,significanteffortshavebeenundertakentomitigatehallucinationsofLLMs.
Theseinitiativesarecomprehensivelysurveyedinourstudy,inaccordancewiththecorresponding
causes,spanningfromdata-related,training-related,andinference-relatedapproaches.Inaddition,
theeffectivenessofretrieval-augmentedgeneration(RAG)inmitigatinghallucinationshas
garneredtremendousattentionwithinthefield.DespitetheconsiderablepotentialofRAG,current
systemsinherentlyfacelimitationsandevensufferfromhallucinations.Accordingly,oursurvey
undertakesanin-depthanalysisofthesechallenges,aimingtoprovidevaluableinsightsaimed
atdevelopingmorerobustRAGsystems.Wealsohighlightseveralpromisingavenuesforfuture
research,suchashallucinationsinlargevision-languagemodels(LVLMs)andunderstanding
of knowledge boundaries in LLM hallucinations, paving the way for forthcoming research in
thefield.
ComparingwithExistingSurveys.Ashallucinationstandsoutasamajorchallengeingenerative
AI,numerousresearch[134,189,255,294,308,372]havebeendirectedtowardshallucinations.
WhilethesecontributionshaveexploredLLMhallucinationfromvariousperspectivesandprovided
valuableinsights,oursurveyseekstodelineatetheirdistinctcontributionsandthecomprehensive
scopetheyencompass.Jietal.[134]primarilyshedlightonhallucinationsinpre-trainedmodels
forNLGtasks,leavingLLMsoutsidetheirdiscussionpurview.Tonmoyetal.[294]mainlyfocused
ondiscussingthemitigationstrategiescombatingLLMhallucinations.Besides,Liuetal.[189]took
abroaderviewofLLMtrustworthinesswithoutdelvingintospecifichallucinationphenomena,
whereasWangetal.[308]providedanin-depthlookatfactualityinLLMs.However,ourworknar-
rowsdowntoacriticalsubsetoftrustworthinesschallenges,specificallyaddressingfactualityand
extendingthediscussiontoincludefaithfulnesshallucinations.Tothebestofourknowledge,Zhang
etal.[372]presentedresearchcloselyalignedwithours,detailingLLMhallucinationtaxonomies,
evaluationbenchmarks,andmitigationstrategies.However,oursurveysetsitselfapartthrough
auniquetaxonomyandorganizationalstructure.Wepresentadetailed,layeredclassificationof
hallucinationsandconductamorecomprehensiveanalysisofthecausesofhallucinations.Crucially,
ourproposedmitigationstrategiesaredirectlytiedtothesecauses,offeringatargetedandcoherent
frameworkforaddressingLLMhallucinations.
OrganizationofthisSurvey.Inthissurvey,wepresentacomprehensiveoverviewofthelatest
developments in LLM hallucinations, as shown in Figure 1. We commence by constructing a
taxonomy of hallucinations in the realm of LLM (Section 2). Subsequently, we analyze factors
contributingtoLLMhallucinationsindepth(Section3),followedbyareviewofvariousstrategies
andbenchmarksemployedforthereliabledetectionofhallucinationsinLLMs(Section4).Wethen
detailaspectrumofapproachesdesignedtomitigatethesehallucinations(Section5).Concluding,
wedelveintothechallengesfacedbycurrentRAGsystems(Section6)anddelineatepotential
pathwaysforforthcomingresearch(Section7).
2 Definitions
ForthesakeofacomprehensiveunderstandingofhallucinationsinLLMs,wecommencewitha
succinctintroductiontoLLMs(Section2.1),delineatingthescopeofthissurvey.Subsequently,we
delveintothetrainingstagesofLLMs(Section2.2),asathoroughunderstandingofthetraining
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

42:4 L.Huangetal.
Fig.1. Themaincontentflowandcategorizationofthissurvey.
mechanismscontributessignificantlytoelucidatingtheoriginsofhallucinations.Lastly,weexpound
upontheconceptofhallucinationsinLLMs(Section2.3),furthercategorizingitintotwodistinct
types.
2.1 LLMs
Before delving into the causes of hallucination, we first introduce the concept of LLMs. Typ-
ically, LLMs refer to a series of general-purpose models that leverage the transformer-based
language model architecture and undergo extensive training on massive textual corpora with
notableexamplesincludingGPT-3[29],PaLM[54],LLaMA[296],GPT-4[229]andGemini[256].
Byscalingtheamountofdataandmodelcapacity,LLMsraiseamazingemergentabilities,typi-
callyincludingin-contextlearning[29],chain-of-thoughtprompting[322]andinstructionfollow-
ing[241].
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

ASurveyonHallucinationinLargeLanguageModels 42:5
2.2 TrainingStagesofLLMs
TheattributesandbehaviorsofLLMsaredeeplyintertwinedwiththeirtrainingprocesses.LLMs
undergo three primary training stages: pre-training, supervised fine-tuning (SFT), and
reinforcement learning from human feedback (RLHF). Analyzing these stages provides
insight into hallucination origins in LLMs, as each stage equips the model with specific
capabilities.
2.2.1 Pre-training. Pre-training is widely acknowledged as a foundational stage for LLM to
acquire knowledge and capabilities [384]. During this phase, LLMs engage in autoregressive
predictionofsubsequenttokenswithinsequences.Throughself-supervisedtrainingonextensive
textualcorpora,LLMsacquireknowledgeoflanguagesyntax,worldknowledge,andreasoning
abilities,therebylayingasolidgroundworkforfurtherfine-tuning.Besides,recentresearch[71,287]
suggeststhatpredictingsubsequentwordsisakintolosslesslycompressingsignificantinformation.
TheessenceofLLMsliesinpredictingtheprobabilitydistributionforupcomingwords.Accurate
predictionsindicateaprofoundgraspofknowledge,translatingtoanuancedunderstandingof
theworld.
2.2.2 SFT. WhileLLMsacquiresubstantialknowledgeandcapabilitiesduringthepre-training
stage,it’scrucialtorecognizethatpre-trainingprimarilyoptimizesforcompletion.Consequently,
pre-trainedLLMsfundamentallyserveascompletionmachines,whichcanleadtoamisalignment
betweenthenext-wordpredictionobjectiveofLLMsandtheuser’sobjectiveofobtainingdesired
responses. To bridge this gap, SFT [366] has been introduced, which involves further training
LLMsusingameticulouslyannotatedsetof(instruction,response)pairs,resultinginenhanced
capabilities and improved controllability of LLMs. Furthermore, recent studies [59, 127] have
confirmedtheeffectivenessofSFTtoachieveexceptionalperformanceonunseentasks,showcasing
theirremarkablegeneralizationabilities.
2.2.3 RLHF. WhiletheSFTprocesssuccessfullyenablesLLMstofollowuserinstructions,there
isstillroomforthemtobetteralignwithhumanpreferences.Amongvariousmethodsthatutilize
humanfeedback,RLHFstandsoutasarepresentativesolutionforaligningwithhumanpreferences
throughreinforcementlearning[55,230,281].Typically,RLHFemploysapreferencemodel[26]
trainedtopredictpreferencerankingsgivenapromptalongsideapairofhuman-labeledresponses.
Toalignwithhumanpreferences,RLHFoptimizestheLLMtogenerateoutputsthatmaximizethe
rewardprovidedbythetrainedpreferencemodel,typicallyemployingareinforcementlearning
algorithm,suchasProximalPolicyOptimization[266].Suchintegrationofhumanfeedbackinto
thetrainingloophasproveneffectiveinenhancingthealignmentofLLMs,guidingthemtoward
producinghigh-qualityandharmlessresponses.
2.3 HallucinationsinLLMs
The concept of hallucination traces its roots to the fields of pathology and psychology and is
defined as the perception of an entity or event that is absent in reality [199]. Within the realm
ofNLP,hallucinationistypicallyreferredtoasaphenomenoninwhichthegeneratedcontent
appearsnonsensicalorunfaithfultotheprovidedsourcecontent[88,205].Thisconceptbearsa
looseresemblancetothephenomenonofhallucinationobservedinhumanpsychology.Generally,
hallucinationsinNLGtaskscanbecategorizedintotwoprimarytypes:intrinsichallucinationand
extrinsichallucination[134,171].
Specifically,intrinsichallucinationspertaintothemodeloutputsthatdirectlyconflictwiththe
providedsourcecontext.Ontheotherhand,extrinsichallucinationsinvolveoutputsthatcannotbe
verifiedusingtheprovidedsourcecontextorexternalknowledgebases.Thismeansthegenerated
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

42:6 L.Huangetal.
Table1. ExamplesofEachCategoryofLLMHallucinations
| Category Type | ExampleDialog | Explanation |
| ------------- | ------------- | ----------- |
Instruction:WhatareThomasEdison’smaincontributions Theresponseisfactuallyincorrect.Inreality,Edison
toscienceandtechnology?
| Factual       |     | improvedthelightbulb,buildingonearlierdesi- |
| ------------- | --- | ------------------------------------------- |
| Contradiction |     | gnsbyothers,andAlexanderGrahamBellinven-    |
Response:ThomasEdisondevelopedthefirstpracticaltele-
|     | phoneandinventedthelightbulb. | tedthetelephone. |
| --- | ----------------------------- | ---------------- |
Theresponseerroneouslystatesthattheconstruction
Instruction:Whatarethemajorenvironmentalimpactsof
| Factuality |     | oftheEiffelTowerledtotheextinctionofthe“Parisian |
| ---------- | --- | ------------------------------------------------ |
Hallucination theconstructionoftheEiffelTower? tiger”andsparkedtheglobalgreenarchitecturemove-
Response:TheconstructionoftheEiffelTowerin1889led ment.Infact,thereisnoevidenceofa“Parisiantiger”
| Factual     |                                                       | everexisting,makingthisafabricatedclaim. |
| ----------- | ----------------------------------------------------- | ---------------------------------------- |
| Fabrication | totheextinctionoftheParisiantiger,aspeciesthatplayeda |                                          |
crucialroleintheregion’secosystem.Additionally,itiswid- Moreover,attributingtheoriginsofgreenarchitec-
elyrecognizedastheeventthatsparkedtheglobalgreen turetotheEiffelTowerisanexaggeration,asthis
movementhasdiverserootsandcannotbetracedback
architecturemovement.
toasingleevent.
Theuserexplicitlyprovidedaninstructiontotranslate
Instruction:TranslatetheEnglishquestionintoSpanish:
Instruction “WhatisthecapitalofFrance?” theEnglishquestionintoSpanish.Insteadofperform-
| Inconsistency |                                     | ingthetranslationasinstructed,theLLMchoseto |
| ------------- | ----------------------------------- | ------------------------------------------- |
|               | Response:ThecapitalofFranceisParis. | answerthequestion.                          |
Retrievedcontext:TheNileisamajornorth-flowingriver
innortheasternAfrica.It’straditionallyconsideredthe
longestriverintheworld.OriginatingintheGreatLakes
Faithfulness regionofcentralAfrica,itflowsthroughseveralcountries ThesummaryincorrectlystatesthattheNileoriginates
| Context       |                                                 | fromthe“mountainrangesofcentralAfrica”,whilethe |
| ------------- | ----------------------------------------------- | ----------------------------------------------- |
| Hallucination | beforeemptyingintotheMediterraneanSea.          |                                                 |
| Inconsistency |                                                 | paragraphmentionsthattheNileoriginatesinthe     |
|               | Instruction:Summarizetheretrievaldocumentabove. | GreatLakesregionofcentralAfrica.                |
Response:TheNileoriginatesfromthemountainranges
ofcentralAfricaandflowsintotheMediterranean.
Instruction:Solvetheequation2x+3=11stepbystep.
Thefirststepcorrectlyisolatesthetermwithxtoget
| Logical |     | 2x=8.However,thenextstepinaccuratelydivides |
| ------- | --- | ------------------------------------------- |
Response:Step1:Subtract3frombothsidestoget:2x=8.
Inconsistency Step2:Dividebothsidesby2toget:x=3.Sotheresult 8by2toyieldaresultofx=3,whichisinconsistent
|     | oftheequationisx=3. | withtheearlierreasoning. |
| --- | ------------------- | ------------------------ |
ContentmarkedinRedrepresentsthehallucinatoryoutput,whilecontentmarkedinBlueindicatesuserinstruction
orprovidedcontextthatcontradictstheLLMhallucination.
textisneithersupportedbynordirectlycontradictstheavailableinformation,renderingtheoutput
unverifiableandpotentiallymisleading.
However,intheeraofLLMs,theversatilecapabilitiesofthesemodelshavefacilitatedtheir
widespreaduseacrossdiversefields,highlightinglimitationsinexistingtask-specificcategorization
paradigms.ConsideringthatLLMsplaceasignificantemphasisonuser-centricinteractionsandpri-
oritizealignmentwithuserdirectives,coupledwiththefactthattheirhallucinationspredominantly
surfaceatfactuallevels,weintroduceamoregranulartaxonomybuildinguponthefoundational
workbyJietal.[134].Thisrefinedtaxonomyseekstoencapsulatethedistinctintricaciesasso-
ciatedwithLLMhallucinations.ToprovideamoreintuitiveillustrationofourdefinitionofLLM
hallucination,wepresentexamplesforeachtypeofhallucinationinTable1,namelyfactuality
hallucinationandfaithfulnesshallucination.
2.3.1 FactualityHallucination. TheemergenceofLLMsmarksasignificantshiftfromtraditional
task-specifictoolkitstoAIassistantsthathaveaheightenedfocusonopen-domaininteractions.
Thisshiftisprimarilyattributedtotheirvastparametricfactualknowledge.However,existingLLMs
occasionallyexhibittendenciestoproduceoutputsthatareeitherinconsistentwithreal-world
factsorunverifiable[165],posingchallengestothetrustworthinessofartificialintelligence.Inthis
context,wecategorizethesefactualityhallucinationsintotwoprimarytypes:
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

ASurveyonHallucinationinLargeLanguageModels 42:7
Factual Contradiction refers to situations where the LLM’s output contains facts that can be
groundedinreal-worldinformationbutpresentcontradictions.Thistypeofhallucinationoccurs
mostfrequentlyandarisesfromdiversesources,encompassingtheLLM’scapture,storage,and
expressionoffactualknowledge.Dependingontheerrortypeofcontradictions,itcanbefurther
dividedintotwosubcategories:entity-errorhallucinationandrelation-errorhallucination.
—Entity-errorhallucinationreferstothesituationswherethegeneratedtextofLLMscontains
erroneousentities.AsshowninTable1,whenaskedabout“theinventorofthetelephone,”the
modelerroneouslystates“ThomasEdison,”conflictingwiththerealfactthatitwas“Alexander
GrahamBell.”
—Relation-errorhallucinationreferstoinstanceswherethegeneratedtextofLLMscontains
wrongrelationsbetweenentities.AsshowninTable1,wheninquiredabout“theinventorof
thelightbulb,”themodelincorrectlyclaims“ThomasEdison,”despitethefactthatheimproved
uponexistingdesignsanddidnotinventit.
FactualFabricationreferstoinstanceswheretheLLM’soutputcontainsfactsthatareunveri-
fiableagainstestablishedreal-worldknowledge.Thiscanbefurtherdividedintounverifiability
hallucinationandoverclaimhallucination.
—Unverifiabilityhallucinationpertainstostatementsthatareentirelynon-existentorcannotbe
verifiedusingavailablesources.AsshowninTable1,whenaskedabout“themajorenviron-
mentalimpactsoftheconstructionoftheEiffelTower,”themodelincorrectlystatesthat“the
constructionledtotheextinctionoftheParisiantiger,”aspeciesthatdoesnotexistandthus,
thisclaimcannotbesubstantiatedbyanyhistoricalorbiologicalrecord.
—Overclaimhallucinationinvolvesclaimsthatlackuniversalvalidityduetosubjectivebiases.
AsshowninTable1,themodelclaimsthat“theEiffelTower’sconstructioniswidelyrecognized
astheeventthatsparkedtheglobalgreenarchitecturemovement.”Thisisanoverclaim,asthere
isnobroadconsensusorsubstantialevidencetosupportthestatement.
2.3.2 FaithfulnessHallucination. LLMsareinherentlytrainedtoalignwithuserinstructions.
AstheuseofLLMsshiftstowardsmoreuser-centricapplications,ensuringtheirconsistencywith
user-providedinstructionsandcontextualinformationbecomesincreasinglyvital.Furthermore,
LLM’sfaithfulnessisalsoreflectedinthelogicalconsistencyofitsgeneratedcontent.Fromthis
perspective,wecategorizethreesubtypesoffaithfulnesshallucinations:
Instructioninconsistency referstotheLLM’soutputsthatdeviatefromauser’sdirective.While
some deviations might serve safety guidelines, the inconsistencies here signify unintentional
misalignment with non-malicious user instructions. As described in Table 1, the user’s actual
intentionistranslation.However,theLLMerroneouslydeviatedfromtheuser’sinstructionand
performedaquestion-answeringtaskinstead.
Contextinconsistency pointstoinstanceswheretheLLM’soutputisunfaithfulwiththeuser’s
providedcontextualinformation.Forexample,asshowninTable1,theusermentionedtheNile’s
sourcebeingintheGreatLakesregionofcentralAfrica,yettheLLM’sresponsecontradictedthe
context.
Logical inconsistency underscores when LLM outputs exhibitinternal logical contradictions,
oftenobservedinreasoningtasks.Thismanifestsasinconsistencybothamongthereasoningsteps
themselvesandbetweenthestepsandthefinalanswer.Forexample,asshowninTable1,while
thereasoningstepofdividingbothsidesoftheequationby2iscorrect,thefinalanswerofx=4is
inconsistentwiththereasoningchain,leadingtoanincorrectresult.
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

42:8 L.Huangetal.
3 HallucinationCauses
LLMhallucinationshavemultifacetedorigins,spanningtheentirespectrumofLLMs’capability
acquisitionprocess.Inthissection,wedelveintotherootcausesofhallucinationsinLLMs,primarily
categorizedintothreekeyaspects:(1)Data(Section3.1),(2)Training(Section3.2),and(3)Inference
(Section3.3).
3.1 HallucinationfromData
DatafortrainingLLMsarecomprisedoftwoprimarycomponents:(1)pre-trainingdata,through
which LLMs acquire their general capabilities and factual knowledge [384], and (2) alignment
data, which teach LLMs to follow user instructions and align with human preferences [318].
Although these data constantly expand the capability boundaries of LLMs, they inadvertently
becometheprincipalcontributorstoLLMhallucinations.Thisprimarilymanifestsinthreeaspects:
thepresenceofmisinformationandbiasesintheflawedpre-trainingdatasources(Section3.1.1),
theknowledgeboundaryinherentlyboundedbythescopeofthepre-trainingdata(Section3.1.2),
andthehallucinationsinducedbyinferioralignmentdata(Section3.1.3).
3.1.1 MisinformationandBiases. Neuralnetworkspossessanintrinsictendencytomemorize
trainingdata[35],andthismemorizationtendencygrowswithmodelsize[34,54].Ingeneral,the
inherentmemorizationcapabilityisadouble-edgedswordinthefightagainsthallucinations.On
theonehand,thecapacitiesofLLMstomemorizesuggeststheirpotentialtocaptureprofound
worldknowledge.Ontheotherhand,itbecomesproblematicinthecontextofmisinformationand
biasespresentwithinpre-trainingdataandmayinadvertentlybeamplified,manifestingasimitative
falsehood [179]andthereinforcementofsocietalbiases.Foramorecomprehensiveunderstanding,
detailedexamplesarepresentedinTable2.
ImitativeFalsehood.Misinformationsuchasfakenewsandunfoundedrumorshasbeenwidely
spreadamongsocialmediaplatformsandgraduallyservesasasignificantcontributortoLLM
hallucinations.Theincreasingdemandforlarge-scalecorporaforpre-trainingnecessitatesthe
employmentofheuristicdatacollectionmethods.Whilefacilitatingtheacquisitionofextensive
data,challengesariseinmaintainingconsistentdataquality,whichinevitablyintroducessuch
misinformationinpre-trainingdata[20,324].Inthissituation,LLMswillincreasethelikelihood
ofgeneratingsuchfalsestatementsduetotheirremarkablememorizationcapabilities,leadingto
imitativefalsehoods.TheissueisfurtherexacerbatedbythefactthatLLMshavedrasticallylowered
thebarrierstocontentcreation,posingconsiderableriskstothetrustworthinessofpublicdiscourse
andinternetecosystems.
Societal Biases. In addition to misinformation, biases are also deeply rooted in social media
platforms, showing up variously, like biased hiring, prejudiced news, and hate-spewing. As a
purelynegativephenomenon,biasesandhallucinationshaveobviousdifferences,mainlymani-
festedasstereotypesspreadingandsocialinequalities.However,certainbiasesareintrinsically
tied to hallucinations, especially those related to gender [239] and nationality [152, 223]. For
instance,LLMsmightassociatetheprofessionofnursingwithfemales,evenwhengenderisn’t
explicitly mentioned in the user-provided context, exemplifying context inconsistency as dis-
cussedinSection2.3.Suchbiasescanbeinadvertentlyacquiredfrominternet-basedtexts,which
arerifewithdiverseandbiasedviewpointsandsubsequentlybepropagatedintothegenerated
content[152].
3.1.2 KnowledgeBoundary. Whilethevastpre-trainingcorporahaveempoweredLLMswith
extensivefactualknowledge,theyinherentlypossessknowledgeboundaries.Theseboundariesarise
primarilyfromtwosources:(1)theinabilityofLLMstomemorizeallfactualknowledgeencountered
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

| ASurveyonHallucinationinLargeLanguageModels |     |     |     | 42:9 |
| ------------------------------------------- | --- | --- | --- | ---- |
Table2. ExamplesofHallucinationsfromImitativeFalsehoodsandSocialBiases
| Type Premise | Input | ModelOuput | Explanation |     |
| ------------ | ----- | ---------- | ----------- | --- |
WhileEdisonimproved
| Within    | the LLM’s            |                     | the light | bulb’s design, |
| --------- | -------------------- | ------------------- | --------- | -------------- |
| training  | data, a fre-         |                     | he was    | not its sole   |
| quently   | referenced           | ThomasEdisoniscred- | inventor. | The model’s    |
| Imitative | Whoiscreditedwiththe |                     |           |                |
but incorrect fact itedwiththeinventionof answer reflects a mis-
| Falsehood | inventionofthelightbulb? |               |            |           |
| --------- | ------------------------ | ------------- | ---------- | --------- |
| appears   | multiple                 | thelightbulb. | conception | prevalent |
times:ThomasEdison initstrainingdata,ex-
inventedthelightbulb. emplifyinganimitative
falsehood.
Provideasummaryofthe
|                        |                           |                        | The model       | erroneously  |
| ---------------------- | ------------------------- | ---------------------- | --------------- | ------------ |
|                        | following news: Dr. Kim   |                        |                 |              |
|                        |                           |                        | added “South    | Korea”       |
|                        | recentlypublishedabreak-  | Dr. Kim                | from South      |              |
| Inthemodel’strain-     |                           |                        | based on        | the name     |
|                        | through paper on quan-    | Korearecentlypublished |                 |              |
| ing data,              | certain                   |                        | “Kim” revealing | its          |
| Societal               | tumcomputing.Thepaper     | a paper                | on quantum      |              |
| namesmayfrequently     |                           |                        | bias in linking | certain      |
| Biases                 | detailsthenewalgorithms   | computing,             | detailing       |              |
| be associated          | with                      |                        | names to        | specific na- |
|                        | andtheirpotentialapplica- | new algorithms         | and             |              |
| specificnationalities. |                           |                        | tionalities,    | which can    |
|                        | tionsinreal-worldscenar-  | theirapplications.     |                 |              |
causehallucinationsin
ios.Ithasbeenhailedas
thesummary.
revolutionarybyexperts.
Eachcategoryinthetableisaccompaniedbyapremiseoutliningthedataissue,userinput,andtheLLM’shallucinatory
outputmarkedinRed(displayedinredfont),andanexplanationfortheoccurrence,aidingcomprehensionofthese
complexphenomena.
duringpre-training,especiallythelessfrequentlong-tailknowledge,and(2)theintrinsicboundary
ofthepre-trainingdataitself,whichdoesnotincluderapidlyevolvingworldknowledgeorcontent
restrictedbycopyrightlaws.Consequently,whenLLMsencounterinformationthatfallsoutside
theirlimitedknowledgeboundaries,theyaremoresusceptibletogeneratinghallucinations.We
presentdetailedexamplesforclearillustrationinTable3.
Long-tailKnowledge.Thedistributionofknowledgewithinthepre-trainingcorporaisinherently
non-uniform,whichresultsinLLMsdemonstratingvaryinglevelsofproficiencyacrossdifferent
typesofknowledge.Recentstudieshavehighlightedastrongcorrelationbetweenthemodel’s
accuracy on general domain questions and the volume of relevant documents [143] or entity
popularity[201]withinthepre-trainingcorpora.Furthermore,giventhatLLMsarepredominantly
trainedonextensivegeneraldomaincorpora[92,240,251],theymayexhibitdeficitsindomain-
specificknowledge.ThislimitationbecomesparticularlyevidentwhenLLMsareconfrontedwith
tasksthatrequiredomain-specificexpertise,suchasmedical[176,275]andlegal[146,349]questions;
thesemodelsmayexhibitpronouncedhallucinations,oftenmanifestingasfactualfabrication.
Up-to-dateKnowledge.Beyondtheshortfallinlong-tailknowledge,anotherintrinsiclimitation
concerningtheknowledgeboundarieswithinLLMsistheirconstrainedcapacityforup-to-date
knowledge.ThefactualknowledgeembeddedwithinLLMsexhibitscleartemporalboundaries
andcanbecomeoutdatedovertime[145,163,227].Oncethesemodelsaretrained,theirinternal
knowledgeisneverupdated.Thisposesachallengegiventhedynamicandever-evolvingnatureof
ourworld.Whenconfrontedwithqueriesthattranscendtheirtemporalscope,LLMsoftenresort
tofabricatingfactsorprovidinganswersthatmighthavebeencorrectinthepastbutarenow
outdated.
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

| 42:10 |     |     |     |     | L.Huangetal. |
| ----- | --- | --- | --- | --- | ------------ |
Table3. ExampleofKnowledgeBoundary
| Type | Input | ModelOuput                   |              | Explanation                |                    |
| ---- | ----- | ---------------------------- | ------------ | -------------------------- | ------------------ |
|      |       | Phenylketonuria              | is caused by | a The correct              | cause of phenylke- |
|      |       | mutationinthehemoglobingene, |              | tonuriaismutationsinthePAH |                    |
Long-tail Whatcausesphenylke- whichresultsinanunusualinter- gene. Such specialized medical
Knowledge tonuria? actionwithhemoglobin,affecting information is less frequently en-
|     |     | itsabilitytotransportoxygenin |                      | countered                     | in the training corpus, |
| --- | --- | ----------------------------- | -------------------- | ----------------------------- | ----------------------- |
|     |     | thebloodstream.               |                      | makingLLMsstruggletomemorize. |                         |
|     |     | MichelleObamahasannounced     |                      | After President               | Joe Biden an-           |
|     |     | hercandidacyandisleadinginthe |                      | nouncedhiswithdrawalfromthe   |                         |
|     |     | polls, with                   | significant endorse- | raceonJuly21,2024,heendorsed  |                         |
WhowillbetheDemo-
|            |                        | mentsfromkeyDemocraticfig-   |     | KamalaHarrisastheDemocratic    |                 |
| ---------- | ---------------------- | ---------------------------- | --- | ------------------------------ | --------------- |
| Up-to-date | cratic Party candidate |                              |     |                                |                 |
|            |                        | uressuchasBarackObamaand     |     | Party candidate.               | Such hallucina- |
| Knowledge  | forthe2024USpresi-     |                              |     |                                |                 |
|            |                        | BernieSanders.Shehasalsoout- |     | tionsarisebecauseLLMs’paramet- |                 |
dentialelection?
|     |     | linedapolicyplatformfocusing   |     | ricknowledgecannotbeupdatedin    |                         |
| --- | --- | ------------------------------ | --- | -------------------------------- | ----------------------- |
|     |     | onhealthcarereformandclimate   |     | real-time,leadingtopotentialfab- |                         |
|     |     | changeinitiatives.             |     | ricationregardingcurrentevents.  |                         |
|     |     | Inthedramaticconclusionof“The  |     | The novel                        | “The Secrets of the Al- |
|     |     | SecretsoftheAlchemist,”thepro- |     | chemist” is                      | under copyright pro-    |
Describetheendingof
|                     |                     | tagonistdiscoversthetruesecret |                      | tection, and                     | LLMs have not been |
| ------------------- | ------------------- | ------------------------------ | -------------------- | -------------------------------- | ------------------ |
| Copyright-sensitive | thenovel“TheSecrets |                                |                      |                                  |                    |
|                     |                     | behind the                     | philosopher’s stone, | traineddirectlyonsuchcopyrighted |                    |
| Knowledge           | oftheAlchemist”that |                                |                      |                                  |                    |
|                     |                     | leadingtoapeacefulresolution   |                      | materials.Thus,themodel’soutput  |                    |
waspublishedlastyear.
|     |     | withallcharacterssharinginthe |     | fabricatesdetailsaboutthebook’s |     |
| --- | --- | ----------------------------- | --- | ------------------------------- | --- |
|     |     | wisdom.                       |     | ending.                         |     |
ContentmarkedinRedrepresentsthehallucinatoryoutput.
Copyright-sensitive Knowledge. Due to licensing restrictions [258], existing LLMs are legally
constrainedtotrainingoncorporathatarepubliclylicensed[62,92]orotherwiseavailableforuse
withoutinfringingcopyrightlaws[10,114].Thislimitationsignificantlyimpactsthebreadthand
diversityofknowledgethatLLMscanlegallyacquire.Asignificantportionofvaluableknowledge,
encapsulated in copyrighted materials such as recent scientific research, proprietary data, and
copyrightedliteraryworks,remainsinaccessibletoLLMs.Thisexclusioncreatesaknowledgegap,
leadingtopotentialhallucinationswhenLLMsattempttogenerateinformationindomainswhere
theirtrainingdataisinaccessible[212].
3.1.3 InferiorAlignmentData. Afterthepre-trainingstage,LLMshaveembeddedsubstantial
factualknowledgewithintheirparameters,therebyestablishingobviousknowledgeboundaries.
DuringtheSFTstage,LLMsaretypicallytrainedoninstructionpairslabeledbyhumanannotators,
potentially introducing new factual knowledge that extends beyond the knowledge boundary
establishedduringpre-training.Gekhmanetal.[97]analyzedthetrainingdynamicsofincorporating
newfactualknowledgeduringtheSFTprocessandfoundthatLLMsstruggletoacquiresuchnew
knowledgeeffectively.Mostimportantly,theydiscoveredacorrelationbetweentheacquisition
ofnewknowledgethroughSFTandincreasedhallucinations,suggestingthatintroducingnew
factualknowledgeencouragesLLMstohallucinate.Additionally,Lietal.[165]conductedextensive
analysisontheeffectofinstructionsinproducinghallucinations.Findingsindicatedthattask-
specificinstructionswhichprimarilyfocusontaskformatlearning,tendtoyieldahigherproportion
ofhallucinatoryresponses.Moreover,overlycomplexanddiverseinstructionsalsoleadtoincreased
hallucinations.
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

ASurveyonHallucinationinLargeLanguageModels 42:11
3.2 HallucinationfromTraining
As detailed in Section 2.2, the distinct stages of training impart various capabilities to LLMs,
withpre-trainingfocusingonacquiringgeneral-purposerepresentationsandworldknowledge,
andalignmentenablesLLMstobetteralignwithuserinstructionsandpreferences.Whilethese
stagesarecriticalforequippingLLMswithremarkablecapabilities,shortfallsineitherstagecan
inadvertentlypavethewayforhallucinations.
3.2.1 HallucinationfromPre-training. Pre-trainingconstitutesthefoundationalstageforLLMs,
predominantlyutilizingatransformer-basedarchitecturefollowingtheparadigmestablishedby
GPT[29,248,249],andfurtherdevelopedbyOPT[368],Falcon[240],andLlama-2[296].This
stageemploysacausallanguagemodelingobjective,wheremodelslearntopredictsubsequent
tokenssolelybasedonprecedingonesinaunidirectional,left-to-rightmanner.Whilefacilitating
efficient training, it inherently limits the ability to capture intricate contextual dependencies,
potentiallyincreasingrisksfortheemergenceofhallucination[177].Moreover,recentresearch
hasexposedthatLLMscanoccasionallyexhibitunpredictablereasoninghallucinationsspanning
bothlong-rangeandshort-rangedependencies,whichpotentiallyarisefromthelimitationsof
soft attention [52, 110], where attention becomes diluted across positions as sequence length
increases.Notably,thephenomenonofexposurebias[21,253]hasbeenalongstandingandserious
contributiontohallucinations,resultingfromthedisparitybetweentrainingandinferenceinthe
auto-regressivegenerativemodel.Suchinconsistencycanresultinhallucinations[309],especially
when an erroneous token generated by the model cascades errors throughout the subsequent
sequence,akintoasnowballeffect[364].
3.2.2 HallucinationfromSFT. LLMshaveinherentcapabilityboundariesestablishedduring
pre-training.SFTseekstoutilizeinstructiondataandcorrespondingresponsestounlockthesepre-
acquiredabilities.However,challengesarisewhenthedemandsofannotatedinstructionsexceed
themodel’spre-definedcapabilityboundaries.Insuchcases,LLMsaretrainedtofitresponses
beyondtheiractualknowledgeboundaries.AsdiscussedinSection3.1.3,over-fittingonnewfactual
knowledgeencouragesLLMspronetofabricatingcontent,amplifyingtheriskofhallucinations
[97,265].Moreover,anothersignificantreasonliesinthemodels’inabilitytoreject.TraditionalSFT
methodstypicallyforcemodelstocompleteeachresponse,withoutallowingthemtoaccurately
expressuncertainty[337,358].Consequently,whenfacedwithqueriesthatexceedtheirknowledge
boundaries,thesemodelsaremorelikelytofabricatecontentratherthanrejectit.Thismisalignment
ofknowledgeboundaries,coupledwiththeinabilitytoexpressuncertainty,arecriticalfactorsthat
contributetotheoccurrenceofhallucinationsduringtheSFTstage.
3.2.3 HallucinationfromRLHF. Severalstudies[13,31]havedemonstratedthatLLM’sactivations
encapsulateaninternalbeliefrelatedtothetruthfulnessofitsgeneratedstatements.Nevertheless,
misalignmentcanoccasionallyarisebetweentheseinternalbeliefsandthegeneratedoutputs.
EvenwhenLLMsarerefinedwithhumanfeedback[230],theycansometimesproduceoutputs
thatdivergefromtheirinternalbeliefs.Suchbehaviors,termedassycophancy[63],underscorethe
model’sinclinationtoappeasehumanevaluators,oftenatthecostoftruthfulness.Recentstudies
indicatethatmodelstrainedviaRLHFexhibitpronouncedbehaviorsofpanderingtouseropinions.
Suchsycophanticbehaviorsarenotrestrictedtoambiguousquestionswithoutdefinitiveanswers
[242],likepoliticalstances,butcanalsoarisewhenthemodelchoosesaclearlyincorrectanswer,
despitebeingawareofitsinaccuracy[323].Delvingintothisphenomenon,Sharmaetal.[270]
suggestedthattherootofsycophancymaylieinthetrainingprocessofRLHFmodels.Byfurther
exploringtheroleofhumanpreferencesinthisbehavior,theresearchindicatesthatthetendency
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

42:12 L.Huangetal.
forsycophancyislikelydrivenbybothhumansandpreferencemodelsshowingabiastowards
sycophanticresponsesovertruthfulones.
3.3 HallucinationfromInference
DecodingplaysanimportantroleinmanifestingthecapabilitiesofLLMsafterpretrainingand
alignment.However,certainshortcomingsindecodingstrategiescanleadtoLLMhallucinations.
3.3.1 ImperfectDecodingStrategies. LLMshavedemonstratedaremarkableaptitudeforgener-
atinghighlycreativeanddiversecontent,aproficiencythatiscriticallydependentonthepivotal
role of randomness in their decoding strategies. Stochastic sampling [83, 117] is currently the
prevailingdecodingstrategyemployedbytheseLLMs.Therationaleforincorporatingrandomness
intodecodingstrategiesstemsfromtherealizationthathighlikelihoodsequencesoftenresult
insurprisinglylow-qualitytext,whichiscalledlikelihoodtrap[117,206,279,359].Thediversity
introducedbytherandomnessindecodingstrategiescomesatacost,asitispositivelycorrelated
withanincreasedriskofhallucinations[58,77].Anelevationinthesamplingtemperatureresults
inamoreuniformtokenprobabilitydistribution,increasingthelikelihoodofsamplingtokens
withlowerfrequenciesfromthetailofthedistribution.Consequently,thisheightenedtendencyto
sampleinfrequentlyoccurringtokensexacerbatestheriskofhallucinations[5].
3.3.2 Over-confidence. Priorstudiesinconditionaltextgeneration[45,209]havehighlighted
theissueofover-confidencewhichstemsfromanexcessivefocusonthepartiallygeneratedcontent,
oftenprioritizingfluencyattheexpenseoffaithfullyadheringtothesourcecontext.WhileLLMs,
primarilyadoptingthecausallanguagemodelarchitecture,havegainedwidespreadusage,the
over-confidencephenomenoncontinuestopersist.Duringthegenerationprocess,theprediction
ofthenextwordisconditionedonboththelanguagemodelcontextandthepartiallygenerated
text.However,asdemonstratedinpriorstudies[19,186,303],languagemodelsoftenexhibita
localizedfocuswithintheirattentionmechanisms,givingprioritytonearbywordsandresultingin
anotabledeficitincontextattention[271].Furthermore,thisconcernisfurtheramplifiedinLLMs
thatexhibitaproclivityforgeneratinglengthyandcomprehensiveresponses.Insuchcases,there
isevenaheightenedsusceptibilitytotheriskofinstructionforgetting[46,190].Thisinsufficient
attentioncandirectlycontributetofaithfulnesshallucinations,whereinthemodeloutputscontent
thatdeviatesfromtheoriginalcontext.
3.3.3 SoftmaxBottleneck. Themajorityoflanguagemodelsutilizeasoftmaxlayerthatoper-
atesonthefinallayer’srepresentationwithinthelanguagemodel,inconjunctionwithaword
embedding,tocomputetheultimateprobabilityassociatedwithwordprediction.Nevertheless,the
efficacyofSoftmax-basedlanguagemodelsisimpededbyarecognizedlimitationknownasthe
Softmaxbottleneck [338],whereintheemploymentofsoftmaxintandemwithdistributedword
embeddingsconstrainstheexpressivityoftheoutputprobabilitydistributionsgiventhecontext
whichpreventsLMsfromoutputtingthedesireddistribution.Additionally,ChangandMcCallum
[38]discoveredthatwhenthedesireddistributionwithintheoutputwordembeddingspaceexhibits
multiple modes, language models face challenges in accurately prioritizing words from all the
modesasthetopnextwords,whichalsointroducestheriskofhallucination.
3.3.4 ReasoningFailure. Beyondthechallengeswithlong-tailknowledge,effectiveutilizationof
knowledgeisinextricablylinkedwithreasoningcapabilities.Forinstance,inmulti-hopquestion-
answering scenarios, even if the LLM possesses the necessary knowledge, it may struggle to
produceaccurateresultsifmultipleassociationsexistbetweenquestions,duetoitslimitationsin
reasoning[382].Furthermore,Berglundetal.[22]unveiledaspecificreasoningfailureinLLMs
termedtheReversalCurse.Specifically,whilethemodelcancorrectlyanswerwhenthequestionis
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

ASurveyonHallucinationinLargeLanguageModels 42:13
formulatedas“AisB,”itexhibitsafailedlogicaldeductionwhenaskedtheconverse“BisA.”This
discrepancyinreasoningextendsbeyondsimpledeductions.
4 HallucinationDetectionandBenchmarks
TheissueofhallucinationswithinLLMshasgarneredconsiderableattention,raisingconcerns
about the reliability of LLMs and their deployment in practical applications. As LLMs become
increasinglyadeptatgeneratinghuman-liketext,accuratelydistinguishingbetweenhallucinated
versusfactualcontentbecomesincreasinglyvital.Moreover,effectivelymeasuringthelevelof
hallucinationinLLMiscrucialforimprovingtheirreliability.Thus,inthissection,wedelveinto
hallucinationdetectionapproaches(Section4.1)andbenchmarksforassessingLLMhallucinations
(Section4.2).
4.1 HallucinationDetection
ExistingstrategiesfordetectinghallucinationsinLLMscanbecategorizedbasedonthetypeof
hallucination:(1)factualityhallucinationdetection,whichaimstoidentifyfactualinaccuraciesin
themodel’soutputs,and(2)faithfulnesshallucinationdetection,whichfocusesonevaluatingthe
faithfulnessofmodel’soutputstothecontextualinformationprovided.
4.1.1 FactualityHallucinationDetection. Factualityhallucinationdetectioninvolvesassessing
whether the output of LLMs aligns with real-world facts. Typical methods generally fall into
twocategories:fact-checking,whichinvolvesverifyingthefactualityofthegeneratedresponse
againsttrustedknowledgesources,anduncertaintyestimation,whichfocusesondetectingfactual
inconsistencyviainternaluncertaintysignals.
Fact-checking.GiventhattheoutputofLLMsistypicallycomprehensiveandconsistsofmultiple
factualstatements,thefact-checkingapproachisgenerallydividedintotwoprimarysteps:(1)fact
extraction,whichinvolvesextractingindependentfactualstatementswithinthemodel’soutputs,
(2)factverification,whichaimsatverifyingthecorrectnessofthesefactualstatementsagainst
trustedknowledgesources.Dependingonthetypeofknowledgesourcesemployedforverification,
fact-checkingmethodologiescanbebroadlycategorizedintotwodistinctparts:externalretrieval
andinternalchecking.
—Externalretrieval:Themostintuitivestrategyforfactverificationisexternalretrieval.Minetal.
[213]developedFACTSCORE,afine-grainedfactualmetrictailoredforevaluatinglong-form
textgeneration.Itfirstdecomposesthegenerationcontentintoatomicfactsandsubsequently
computesthepercentagesupportedbyreliableknowledgesources.Expandingonthisconcept,
Chernetal.[50]proposedaunifiedframeworkthatequipsLLMswiththecapabilitytoidentify
factualinaccuraciesbyutilizingacollectionofexternaltoolsdedicatedtoevidencegathering.
Inadditiontoretrievingsupportingevidencesolelybasedondecompositedclaims,Huoetal.
[126]improvedtheretrievalprocessthroughqueryexpansion.Bycombiningtheoriginal
questionwiththeLLM-generatedanswer,theyeffectivelyaddressedtheissueoftopicdrift,
ensuringthattheretrievedevidencealignswithboththequestionandtheLLM’sresponse.
—Internalchecking:Giventheextensivefactualknowledgeencodedintheirparameters,LLMs
havebeenexploredasfactualknowledgesourcesforfact-checking.Dhuliawalaetal.[73]
introducedtheChain-of-Verification(CoVe),whereanLLMfirstgeneratesverification
questionsforadraftresponseandsubsequentlyleveragesitsparametricknowledgetoassess
the consistency of the answer against the original response, thereby detecting potential
inconsistencies.Kadavathetal.[141]andZhangetal.[371]calculatetheprobability𝑝(𝑇𝑟𝑢𝑒)
to assess the factuality of the response to a boolean question, relying exclusively on the
model’sinternalknowledge.Additionally,Lietal.[165]observedthatmostatomicstatements
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

42:14 L.Huangetal.
Fig.2. Taxonomyofuncertaintyestimationmethodsinfactualhallucinationdetection,featuring(a)LLM
InternalStatesand(b)LLMBehavior,withLLMbehaviorencompassingtwomaincategories:self-consistency
andmulti-debate.
areinterrelated,somemayserveascontextualbackgroundsforothers,whichpotentially
leadstoincorrectjudgments.Thus,theyinstructtheLLMtodirectlypredicthallucination
judgmentsconsideringallfactualstatements.However,asLLMsarenotinherentlyreliable
factualdatabases[381],solelyrelyingonLLMs’parametricknowledgeforfact-checkingmay
resultininaccurateassessments.
Uncertainty Estimation. While many approaches to hallucination detection rely on external
knowledgesourcesforfact-checking,severalmethodshavebeendevisedtoaddressthisissuein
zero-resourcesettings,thuseliminatingtheneedforretrieval.Thefoundationalpremisebehind
thesestrategiesisthattheoriginofLLMhallucinationsisinherentlytiedtothemodel’suncertainty.
Therefore,byestimatingtheuncertaintyofthefactualcontentgeneratedbythemodel,itbecomes
feasible to detect hallucinations. The methodologies in uncertainty estimation can broadly be
categorizedintotwoapproaches:basedonLLMinternalstates andLLMbehavior,asshownin
Figure2.
—LLMinternalstates:TheinternalstatesofLLMscanserveasinformativeindicatorsoftheir
uncertainty,oftenmanifestedthroughmetricsliketokenprobabilityorentropy.Varshneyetal.
[302]determinedthemodel’suncertaintytowardskeyconceptsquantifiedbyconsidering
theminimaltokenprobabilitywithinthoseconcepts.Theunderlyingrationaleisthatalow
probabilityservesasastrongindicatorofthemodel’suncertainty,withlessinfluencefrom
higherprobabilitytokenspresentintheconcept.Similarly,Luoetal.[195]employedaself-
evaluation-based approach for uncertainty estimation by grounding in the rationale that
a language model’s ability to adeptly reconstruct an original concept from its generated
explanationisindicativeofitsproficiencywiththatconcept.Byinitiallypromptingthemodel
togenerateanexplanationforagivenconceptandthenemployingconstraineddecoding
to have the model recreate the original concept based on its generated explanation, the
probabilityscorefromtheresponsesequencecanserveasafamiliarityscorefortheconcept.
Furthermore,Yaoetal.[341]interpretedhallucinationthroughthelensofadversarialattacks.
Utilizinggradient-basedtokenreplacement,theydevisedpromptstoinducehallucinations.
Notably,theyobservedthatthefirsttokengeneratedfromarawprompttypicallyexhibitslow
entropycomparedtothosefromadversarialattacks.Basedonthisobservation,theyproposed
settinganentropythresholdtodefinesuchhallucinationattacks.
—LLMbehavior:However,whensystemsareonlyaccessibleviaAPIcalls[99,211,228],access
totheoutput’stoken-levelprobabilitydistributionmightbeunavailable.Giventhisconstraint,
severalstudieshaveshiftedtheirfocustoprobingamodel’suncertainty,eitherthroughnatural
languageprompts[141,331]orbyexaminingitsbehavioralmanifestations.Forinstance,by
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

ASurveyonHallucinationinLargeLanguageModels 42:15
Fig.3. Theillustrationofdetectionmethodsforfaithfulnesshallucinations:(a)Fact-basedMetrics,which
assessesfaithfulnessbymeasuringtheoverlapoffactsbetweenthegeneratedcontentandthesourcecontent;
(b)Classifier-basedMetrics,utilizingtrainedclassifierstodistinguishthelevelofentailmentbetweenthe
generatedcontentandthesourcecontent;(c)QA-basedMetrics,employingquestion-answeringsystemsto
validatetheconsistencyofinformationbetweenthesourcecontentandthegeneratedcontent;(d)Uncertainty
Estimation,whichassessesfaithfulnessbymeasuringthemodel’sconfidenceinitsgeneratedoutputs;(e)
Prompting-basedMetrics,whereinLLMsareinducedtoserveasevaluators,assessingthefaithfulnessof
generatedcontentthroughspecificpromptingstrategies.
samplingmultipleresponsesfromanLLMforthesameprompt,Manakuletal.[202]detected
hallucinationsviaevaluatingtheconsistencyamongthefactualstatements.However,these
methodspredominantlyrelyondirectqueriesthatexplicitlysolicitinformationorverification
fromthemodel.Agrawaletal.[3],inspiredbyinvestigativeinterviews,advocatedforthe
useofindirectqueries.Unlikedirectones,theseindirectcounterpartsoftenposeopen-ended
questions to elicit specific information. By employing these indirect queries, consistency
acrossmultiplemodel generationscanbe betterevaluated. Beyondassessing uncertainty
fromtheself-consistencyofasingleLLM’smultiplegenerations,onecanembraceamulti-
agentperspectivebyincorporatingadditionalLLMs.Drawinginspirationfromlegalcross-
examination practices, Cohen et al. [61] introduced the LMvLM approach. This strategy
leveragesanexaminerLMtoquestionanexamineeLM,aimingtounveilinconsistenciesof
claimsduringmulti-turninteraction.
4.1.2 FaithfulnessHallucinationDetection. EnsuringthefaithfulnessofLLMstoprovidecontext
oruserinstructionsispivotalfortheirpracticalutilityinIRapplications,fromconversationalsearch
tointeractivedialoguesystems.Wecategorizeexistinghallucinationdetectionmetricstailored
tofaithfulnessintothefollowinggroups,withanoverviewshowninFigure3:(1)Fact-based,(2)
Classifier-based,(3)QA-based,(4)Uncertainty-based,and(5)LLM-based.
Fact-based Metrics. In the realm of assessing faithfulness, one of the most intuitive methods
involves measuring the overlap of pivotal facts between the generated content and the source
content.Giventhediversemanifestationsoffacts,faithfulnesscanbemeasuredbasedonn-gram,
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

42:16 L.Huangetal.
entities,andrelationtriples.Traditionaln-gram-based metrics,suchasBLEU[236],ROUGE[178],
andPARENT-T[320],typicallyfallshortindifferentiatingthenuanceddiscrepanciesbetweenthe
generatedcontentandthesourcecontent[205].Entity-based metrics[222]makeastepfurtherby
calculatingtheoverlapofentities,asanyomissionorinaccurategenerationofthesekeyentities
couldleadtoanunfaithfulresponse.Notably,evenifentitiesmatch,therelationsbetweenthem
mightbeerroneous.Thus,relation-based metrics[98]focusontheoverlapofrelationtuplesand
introduceametricthatcomputestheoverlapofrelationtuplesextractedusingtrainedend-to-end
factextractionmodels.
Classifier-basedMetrics.Beyondcomputingfactoverlap,anotherstraightforwardapproachto
assessingthefaithfulnessofthemodelgenerationinvolvesutilizingclassifierstrainedondatafrom
relatedtaskssuchasnaturallanguageinference(NLI)andfact-checking,ordatacomprisedof
syntheticallytask-specifichallucinatedandfaithfulcontent.Afoundationalprincipleforassessing
thefaithfulnessofgeneratedtextisanchoredontheideathatgenuinelyfaithfulcontentshould
inherentlybeentailedbyitssourcecontent.Inlinewiththis,numerousstudies[81,205]have
trained classifiers on NLI datasets to identify factual inaccuracies, especially in the context of
abstract summarization. However, Mishra et al. [214] highlighted that the mismatch in input
granularitybetweenconventionalNLIdatasetsandinconsistencydetectiondatasetslimitstheir
applicabilityforeffectivelydetectinginconsistencies.Buildingonthis,moreadvancedstudieshave
proposedmethodssuchasfine-tuningonadversarialdatasets[17],decomposingtheentailment
decisionsatthedependencyarclevel[100],andsegmentingdocumentsintosentenceunitsthen
aggregating scores between sentence pairs [151]. While using data from related tasks to fine-
tunetheclassifierhasshownpromiseinevaluatingfaithfulness,it’sessentialtorecognizethe
inherentgapbetweenrelatedtasksandthedownstreamtask.Thescarcityofannotateddatafurther
constrainstheirapplicability.Inresponsetothischallenge,asurgeofresearchexploresleveraging
data-augmentationmethodstoconstructsyntheticaldataforfine-tuningtheclassifier,eitherby
rule-basedperturbation[78,149,262]orgeneration[385].
QA-basedMetrics.Incontrasttoclassifier-basedmetrics,QA-basedmetrics[76,118,267,306]have
recentlygarneredattentionfortheirenhancedabilitytocaptureinformationoverlapbetweenthe
model’sgenerationanditssource.Thesemetricsoperatebyinitiallyselectingtargetanswersfrom
theinformationunitswithintheLLM’soutput,andthenquestionsaregeneratedbythequestion-
generationmodule.Thequestionsaresubsequentlyusedtogeneratesourceanswersbasedonthe
usercontext.Finally,thefaithfulnessoftheLLM’sresponsesiscalculatedbycomparingthematching
scoresbetweenthesourceandtargetanswers.Althoughthesemethodologiesshareacommon
thematicapproach,theyexhibitvariabilityinaspectslikeanswerselection,questiongeneration,
andansweroverlap,leadingtodiverseperformanceoutcomes.Buildingonthisfoundationalwork,
Fabbrietal.[79]conductedanin-depthevaluationofthecomponentswithinQA-basedmetrics,
yieldingfurtherenhancementsinfaithfulnessevaluation.
Uncertainty-basedMetrics.Drawingparallelswiththeuncertainty-basedapproachesemployed
fordetectingfactualityhallucinations(Section4.1.1),theapplicationofuncertaintyestimation
inassessingfaithfulnesshasbeenwidelyexplored,typicallycharacterizedbyentropyandlog-
probability.Forentropy-baseduncertainty,XiaoandWang[329]hasrevealedapositivecorrelation
betweenhallucinationlikelihoodindata-to-textgenerationandpredictiveuncertainty,whichis
estimatedbydeepensembles[153].Inarelatedvein,Guerreiroetal.[105]leveragedthevariance
in hypotheses yielded by Monte Carlo Dropout [91] as an uncertainty measure within neural
machinetranslation.Morerecently,vanderPoeletal.[301]employedconditionalentropy[333]
to assess model uncertainty in abstractive summarization. Regarding log-probability, it can be
appliedatdifferentlevelsofgranularity,suchaswordorsentencelevel.Notably,severalstud-
ies [90, 105, 355] have adopted length-normalized sequence log-probability to measure model
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

ASurveyonHallucinationinLargeLanguageModels 42:17
confidence.Furthermore,consideringthehallucinatedtokencanbeassignedhighprobabilitywhen
theprecedingcontextcontainsthesamehallucinatedinformation,Zhangetal.[370]focusedon
themostinformativeandimportantkeywordsandintroducedapenaltymechanismtocounteract
thepropagationofhallucinatedcontent.
LLM-basedJudgement.Recently,theremarkableinstruction-followingabilityofLLMshasunder-
scoredtheirpotentialforautomaticevaluation[51,187,310].Exploitingthiscapability,researchers
have ventured into novel paradigms for assessing the faithfulness of model-generated content
[2,94,131,150,196].ByprovidingLLMswithconcreteevaluationguidelinesandfeedingthem
boththemodel-generatedandsourcecontent,theycaneffectivelyassessfaithfulness.Thefinal
evaluationoutputcaneitherbeabinaryjudgmentonfaithfulness[196]orak-pointLikertscale
indicatingthedegreeoffaithfulness[94].Forpromptselection,evaluationpromptcaneitherbe
directprompting,chain-of-thoughtprompting[2],usingin-context-learning[131]orallowingthe
modeltogenerateevaluationresultsaccompanyingwithexplanations[150].
4.2 HallucinationBenchmarks
Inthissection,wepresentacomprehensiveoverviewofexistinghallucinationbenchmarks(Ta-
ble4),whichcanbecategorizedintotwoprimarydomains:HallucinationEvaluationBenchmarks
(Section4.2.1),whichassesstheextentofhallucinationsgeneratedbyexistingcutting-edgeLLMs,
andHallucinationDetectionBenchmarks(Section4.2.2),designedspecificallytoevaluatetheper-
formanceofexistinghallucinationdetectionmethods.Collectively,thesebenchmarksestablisha
unifiedframework,enablinganuancedandthoroughexplorationofhallucinatorypatternsinLLMs.
4.2.1 HallucinationEvaluationBenchmarks. Hallucinationevaluationbenchmarksaredevised
to quantify the tendency of LLMs to generate hallucinations, particularly emphasizing factual
inaccuraciesandinconsistencyfromthegivencontexts.GiventheadeptnessofLLMsatmemorizing
high-frequencycountknowledge,theprimaryfocusofcurrenthallucinationevaluationbenchmarks
targetslong-tailedknowledgeandchallengingquestionsthatcaneasilyelicitimitativefalsehood.
Asforevaluating,thesebenchmarkstypicallyutilizemultiplechoiceQA,whereperformanceis
measuredthroughaccuracymetrics,orgenerativeQA,evaluatedeitherthroughhumanjudgment
orscoresgivenbyproxymodels.
Long-tail Factual Knowledge. The selection criteria for gathering long-tail factual question-
answeringsamplestypicallyincludethefrequencyofappearance,recency,andspecificdomains.
Regardingthefrequencyofappearance,benchmarkssuchasPopQA[201]andHead-to-Tail[286]
areconstructedbasedonentitypopularityderiveddirectlyfromWikipedia.Consideringthatworld
knowledgeisconstantlyevolving,itbecomescrucialtovalidatetheLLM’sfactualityconcerning
thecurrentworld.Amongbenchmarkscharacterizedbyever-changing,REALTIMEQA[145]and
FreshQA[304]standout.REALTIMEQAoffersreal-time,open-domainmultiple-choicequestions
thatareregularlyupdatedtoreflectthelatestdevelopments.Thesequestionsarederivedfromnewly
publishednewsarticles,encompassingabroadspectrumoftopics,includingpolitics,business,
sports,andentertainment.Similarly,FreshQAchallengesLLMswithquestionsdesignedtorepresent
varyingdegreesoftemporalchange—categorizedintonever-changing,slow-changing,andfast-
changingworldknowledge.Thisbenchmarkisfurtherenrichedbyincludingquestionsbasedon
false premises, requiring debunking, thus comprising a total of 600 meticulously hand-crafted
questions.Moreover,long-tailknowledgeoftenpertainstospecificdomains.Forinstance,Med-
HALT[299]isdistinguishedbyitsfocusonthemedicaldomain,challengingLLMswithmultiple-
choicequestionsderivedfromavarietyofcountries.Additionally,Malaviyaetal.[200]collected
expert-curatedquestionsacross32fieldsofstudy,resultinginahigh-qualitylong-formQAdataset
with2,177questions.
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

| 42:18     |          |                                                     |                         |                 | L.Huangetal. |        |
| --------- | -------- | --------------------------------------------------- | ----------------------- | --------------- | ------------ | ------ |
|           |          | Table4. AnOverviewofExistingHallucinationBenchmarks |                         |                 |              |        |
|           |          |                                                     | Attribute               |                 | Task         |        |
| Benchmark | Datasets | DataSize Language                                   |                         |                 |              |        |
|           |          |                                                     | Factuality Faithfulness | Manual TaskType | Input Label  | Metric |
Tru t h f u lQA (cid:52) (cid:55) (cid:52) G e n e ra ti v e Q A LLM - J ud g e&
[ 1 7 9 ] - 817 English M u l ti -C h o i ce Q A Question Answer H u m a n
REAL T I M EQA - Dynamic English (cid:52) (cid:55) (cid:52) M u l ti -C h o i ce Q A Question Answer A cc
| [1 4 5 ] |     |     |     | G e n e ra ti v e Q | A   | EM & F1 |
| -------- | --- | --- | --- | ------------------- | --- | ------- |
SelfCheck G P T -Wikibio (cid:55) (cid:52) (cid:55) Pa ra g r a p h &
[2 1 0 ] - 1,908 English Detection C o n c e p t Passage AUROC
HaluEval Task-specific 30,000 English (cid:55) (cid:52) (cid:55) Detection Query Response Acc
| [166] |         |               | (cid:55) (cid:52) | (cid:55)  |                    |     |
| ----- | ------- | ------------- | ----------------- | --------- | ------------------ | --- |
|       | General | 5,000 English |                   | Detection | TaskInput Response | Acc |
Me d - H A LT - 4,916 Multilingual (cid:52) (cid:55) (cid:55) Multi-ChoiceQA Question Choice Point wi se Score
| [ 2 9 9 ] |     |     |     |     |     | & A cc |
| --------- | --- | --- | --- | --- | --- | ------ |
FACTOR Wiki-FACTOR 2,994 English (cid:52) (cid:55) (cid:55) Multi-ChoiceQA Question Answer likelihood
[220] News-FACTOR 1,036 English (cid:52) (cid:55) (cid:55) Multi-ChoiceQA Question Answer likelihood
BAMBOO SenHallu 200 English (cid:55) (cid:52) (cid:55) Detection Paper Summary P&R&F1
[75] AbsHallu 200 English (cid:55) (cid:52) (cid:55) Detection Paper Summary P&R&F1
Chine s e F a ctEval - 125 Chinese (cid:52) (cid:55) (cid:52) GenerativeQA Question - Score
[ 3 0 7 ]
Misleading 175 Chinese (cid:52) (cid:55) (cid:52) GenerativeQA Question Answer LLM-Judge
Ha l u Q A Misleading-hard 69 Chinese (cid:52) (cid:55) (cid:52) GenerativeQA Question Answer LLM-Judge
[ 4 9 ]
Knowledge 206 Chinese (cid:52) (cid:55) (cid:52) GenerativeQA Question Answer LLM-Judge
Never-changing 150 English (cid:52) (cid:55) (cid:52) GenerativeQA Question Answer Human
FreshQA Slow-changing 150 English (cid:52) (cid:55) (cid:52) GenerativeQA Question Answer Human
|     |     |     | (cid:52) (cid:55) | (cid:52) |     |     |
| --- | --- | --- | ----------------- | -------- | --- | --- |
[304] Fast-changing 150 English GenerativeQA Question Answer Human
False-premise 150 English (cid:52) (cid:55) (cid:52) GenerativeQA Question Answer Human
| F E L M |     |     | (cid:52) (cid:52) | (cid:55) |     | B a l an ce d |
| ------- | --- | --- | ----------------- | -------- | --- | ------------- |
[ 4 2 ] - 3,948 English Detection Question Response A c c & F 1
PHD-LOW 100 English (cid:55) (cid:52) (cid:55) Detection Entity Response P&R&F1
| P H D |     |     | (cid:55) (cid:52) | (cid:55) |     |     |
| ----- | --- | --- | ----------------- | -------- | --- | --- |
[ 3 36 ] PHD-Meidum 100 English Detection Entity Response P&R&F1
PHD-High 100 English (cid:55) (cid:52) (cid:55) Detection Entity Response P&R&F1
| Scr e e n E val |     |            | (cid:55) (cid:52) | (cid:55)  |                  |       |
| --------------- | --- | ---------- | ----------------- | --------- | ---------------- | ----- |
| [ 1 5 5 ]       | -   | 52 English |                   | Detection | Document Summary | AUROC |
COVID-QA N/A English (cid:55) (cid:52) (cid:55) Detection Question Answer AUROC
|     |     |     | (cid:55) (cid:52) | (cid:55) |     |     |
| --- | --- | --- | ----------------- | -------- | --- | --- |
Re a l H all DROP N/A English Detection Question Answer AUROC
OpenAssistant N/A English (cid:55) (cid:52) (cid:55) Detection Question Answer AUROC
[ 8 9 ] TriviaQA N/A English (cid:55) (cid:52) (cid:55) Detection Question Answer AUROC
L S u m
- 6,166 English (cid:55) (cid:52) (cid:55) Detection Document Summary BalancedAcc
[ 8 4 ]
|      |          |             | (cid:55) (cid:52) | (cid:55)  |                 |       |
| ---- | -------- | ----------- | ----------------- | --------- | --------------- | ----- |
| SAC3 | HotpotQA | 250 English |                   | Detection | Question Answer | AUROC |
[360] NQ-Open 250 English (cid:55) (cid:52) (cid:55) Detection Question Answer AUROC
Biomedicine 1,535 English (cid:52) (cid:55) (cid:55) GenerativeQA Question Answer MiHR&MaHR
|     |     |     | (cid:52) (cid:55) | (cid:55) |     |     |
| --- | --- | --- | ----------------- | -------- | --- | --- |
Halu E v a l2.0 Finance 1,125 English GenerativeQA Question Answer MiHR&MaHR
Science 1,409 English (cid:52) (cid:55) (cid:55) GenerativeQA Question Answer MiHR&MaHR
[1 6 5 ] Education 1,701 English (cid:52) (cid:55) (cid:55) GenerativeQA Question Answer MiHR&MaHR
Opendomain 3,000 English (cid:52) (cid:55) (cid:55) GenerativeQA Question Answer MiHR&MaHR
ForAttribute,FactualityandFaithfulnessrepresentwhetherthebenchmarkisusedtoevaluateLLM’sfactualityorto
detectfaithfulnesshallucination,andManualrepresentswhethertheinputsinthedataarehandwritten.
ImitativeFalsehoodKnowledge.Imitativefalsehoodknowledgeisspecificallydesignedtochallenge
LLMsthroughadversarialprompting.Thisapproachcraftsquestionsinsuchawaythattheyare
pronetomisleadingLLMsduetofalsebeliefsormisconceptions.Thetwomostrepresentative
benchmarksareTruthfulQA[179]andHalluQA[49].TruthfulQAcomprises817questionsthat
span38diversecategories,suchashealth,law,finance,andpolitics.Craftedusinganadversarial
methodology, it aims to elicit “imitative falsehoods”—misleading responses that models might
generateduetotheirfrequentpresenceintrainingdata.Thebenchmarkisdividedintotwoparts,
oneofwhichcontainsmanuallycuratedquestionsthatwerefurtherrefinedbyfilteringoutthose
correctly answered by GPT-3, resulting in 437 filtered questions. The other part includes 380
unfiltered non-adversarial questions. Drawing from the construction approach of TruthfulQA,
HalluQAiscraftedtospecificallyassesshallucinationsinChineseLLMs,focusingonimitative
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

ASurveyonHallucinationinLargeLanguageModels 42:19
falsehoodsandfactualerrors.Thebenchmarkcomprises450handcraftedadversarialquestions
across30domainsandiscategorizedintotwoparts.Themisleadingsectioncapturesquestionsthat
successfullydeceiveGLM-130B,whiletheknowledgesectionretainsquestionsthatbothChatGPT
andPuyuconsistentlyanswerincorrectly.TocomprehensivelyevaluateLLMhallucinationsacross
various domains, Li et al. [165] constructed an upgraded hallucination evaluation benchmark,
HaluEval2.0,basedon[166].Thisbenchmarkincludes8,770questionsthatLLMsareproneto
hallucinationacrossfivedomains:biomedicine,finance,science,education,andopendomain.
4.2.2 HallucinationDetectionBenchmarks. Forhallucinationdetectionbenchmarks,mostprior
studieshaveprimarilyconcentratedontask-specifichallucinations,suchasabstractivesummariza-
tion[80,101,149,205,233,306],data-to-text[237,292],andmachinetranslation[385].However,
thecontentgeneratedinthesestudiesoftenoriginatesfrommodelswithlessercapabilities,suchas
BART[161]andPEGASUS[362].Asaresult,theymaynotaccuratelyreflecttheeffectivenessof
hallucinationdetectionstrategies,underliningthenecessityforasignificantshifttowarddeveloping
benchmarksthatencapsulatemorecomplexscenariosreflectiveoftheeraofLLMs.
Forexample,SelfCheckGPT-Wikibio[210]offersasentence-leveldatasetcreatedbygenerating
syntheticWikipediaarticleswithGPT-3,manuallyannotatedforfactuality,highlightingthechal-
lengeofdetectinghallucinationsinthebiographydomain.Complementingthis,HaluEval[166]
combinesautomatedgenerationwithhumanannotationtoevaluateLLMs’abilitytorecognize
hallucinations across 5,000 general user queries and 30,000 task-specific samples, leveraging a
“sampling-then-filtering”approach.Buildinguponexistingresearchpredominantlyfocusedon
shortdocuments,BAMBOO[75]andScreenEval[155]extendthescopeinlong-formhallucination
detection.Further,FELM[42],distinguishesitselfbyassessingfactualityacrossdiversedomains
includingworldknowledge,science,andmathematics,producing817samplesannotatedforvarious
facetsoffactualaccuracy,therebyaddressingtheneedforcross-domainevaluationoffactuality
inLLM-generatedcontent.Onadifferentnote,PHD[336],shiftsthefocustowardspassage-level
detectionofnon-factualcontentbyanalyzingentitiesfromWikipedia,thusofferinganuanced
viewontheknowledgedepthofLLMs.RealHall[89]andSAC3[360]aligncloselywithreal-world
applicationsfocusingonopen-domainquestion-answering,whereasLSum[84]concentratingon
summarizationtasks.
5 HallucinationMitigation
Inthissection,wepresentacomprehensivereviewofcontemporarymethodsaimedatmitigating
hallucinations in LLMs. Drawing from insights discussed in Hallucination Causes (Section 3),
we systematically categorize these methods based on the underlying causes of hallucinations.
Specifically,wefocusonapproachesaddressingData-relatedHallucinations(Section5.1),Training-
relatedHallucinations(Section5.2)andInference-relatedHallucinations(Section5.3),eachoffering
tailoredsolutionstotacklespecificchallengesinherenttotheirrespectivecause.
5.1 MitigatingData-relatedHallucinations
AsanalyzedinSection3.1,data-relatedhallucinationsgenerallyemergeasabyproductofmis-
information, biases, and knowledge gaps, which are fundamentally rooted in the pre-training
data.Severalmethodsareproposedtomitigatesuchhallucinations,primarilycategorizedinto
threedistinctparts:(1)datafiltering aimingatselectinghigh-qualitydatatoavoidintroducing
misinformationandbiases,(2)modeleditingfocusingoninjectingup-to-dateknowledgebyediting
model’s parameters, and (3) RAG leveraging external non-parametric database for knowledge
supplying.
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

42:20 L.Huangetal.
5.1.1 DataFiltering. Toreducethepresenceofmisinformationandbiases,anintuitiveapproach
involvesthecarefulselectionofhigh-qualitypre-trainingdatafromreliablesources.Inthisway,we
canensurethefactualcorrectnessofdatawhilealsominimizingtheintroductionofsocialbiases.As
earlyastheadventofGPT-2,Radfordetal.[249]underscoredthesignificanceofexclusivelyscraping
webpagesthathadundergonerigorouscurationandfiltrationbyhumanexperts.However,as
pre-trainingdatasetscontinuetoscale,manualcurationbecomesachallenge.Giventhatacademic
orspecializeddomaindataistypicallyfactuallyaccurate,gatheringhigh-qualitydataemergesasa
primarystrategy.NotableexamplesincludethePile[92]and“textbook-like”datasources[106,174].
Additionally,up-samplingfactualdataduringthepre-trainingphasehasbeenproveneffectivein
enhancingthefactualcorrectnessofLLMs[296],thusalleviatinghallucination.
Inadditiontostrictlycontrollingthesourceofdata,deduplicationservesasacrucialprocedure.
Existingpracticestypicallyfallintotwocategories:exactduplicatesandnear-duplicates.Forexact
duplicates,themoststraightforwardmethodinvolvesexactsubstringmatchingtoidentifyidentical
strings. However, given the vastness of pre-training data, this process can be computationally
intensive,amoreefficientmethodutilizestheconstructionofasuffixarray[203],enablingeffective
computationofnumeroussubstringqueriesinlineartime.Regardingnear-duplicates,theidentifi-
cationofteninvolvesapproximatefull-textmatching,typicallyutilizinghash-basedtechniquesto
identifydocumentpairswithsignificantn-gramoverlap.Furthermore,MinHash[28]standsoutas
aprevalentalgorithmforlarge-scalededuplicationtasks[109].Additionally,SemDeDup[1]makes
useofembeddingsfrompre-trainedmodelstoidentifysemanticduplicates,whichreferstodata
pairswithsemanticsimilaritiesbutnotidentical.
Discussion. Since data filtering works directly at the source of hallucinations, it effectively
mitigateshallucinationsbyensuringtheuseofhigh-quality,factuallyaccuratesources.Despite
itseffectiveness,theefficiencyandscalabilityofcurrentdatafilteringmethodsposesignificant
challenges as data volumes expand. Additionally, these methods often overlook the influence
ofLLM-generatedcontent,whichcanintroducenewrisksandinaccuracies.Toadvance,future
researchmustfocusondevelopingmoreefficient,automateddatafilteringalgorithmsthatcan
keeppacewiththerapidexpansionofdatasetsandthecomplexitiesofLLM-generatedcontent.
5.1.2 ModelEditing. Modelediting[276,316,365]hasgarneredrisingattentionfromresearchers,
whichaimstorectifymodelbehaviorbyincorporatingadditionalknowledge.Currentmodelediting
techniquescanbecategorizedintotwoclasses:locate-then-edit andmeta-learning.
Locate-then-edit.Locate-then-editmethods[65,207]consistoftwostages,whichfirstlocatethe
“buggy”partofthemodelparametersandthenapplyanupdatetothemtoalterthemodel’sbehavior.
Forexample,ROME[207]locatedtheedits-relatedlayerbydestroyingandsubsequentlyrestoring
theactivationsandthenupdatestheparametersofFFNinadirectmannertoeditknowledge.MEMIT
[208]employedthesameknowledgelocatingmethodsasROME,enablingtheconcurrentupdating
ofmultiplelayerstofacilitatethesimultaneousintegrationofthousandsofeditingknowledge.
However,Yaoet al. [343] found that these methods lack non-trivial generalization capabilities
andvaryingperformanceandapplicabilitytodifferentmodelarchitectures.Thebest-performing
methodsROMEandMEMITempiricallyonlyworkwellondecoder-onlyLLMs.
Meta-learning.Meta-learningmethods[69,215]trainanexternalhyper-networktopredictthe
weight update of the original model. Nevertheless, meta-learning methods often require addi-
tionaltrainingandmemorycost,whereMEND[215]utilizedalow-rankdecompositionwitha
specializeddesigntoreducethesizeofhyper-networks.Notably,MENDwouldexhibitacancella-
tioneffect,whereparametershiftscorrespondingtodifferentkeyssignificantlycounteracteach
other.MALMEN[288]furtheraddressedthisissuebyframingtheparametershiftaggregationasa
leastsquaresproblemratherthanasimplesummation,therebygreatlyenhancingitscapacityfor
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

ASurveyonHallucinationinLargeLanguageModels 42:21
Fig.4. TheillustrationofthreedistinctapproachesforRAG:(a)One-timeRetrieval,whererelevantinformation
isretrievedoncebeforetextgeneration;(b)IterativeRetrieval,involvingmultipleretrievaliterationsduring
textgenerationfordynamicinformationintegration;and(c)PosthocRetrieval,wheretheretrievalprocess
happensafterananswerisgenerated,aimingtorefineandfact-checkthegeneratedcontent.
extensiveediting.Whilethesemethodscanfine-grainedlyadjustthebehaviorofthemodel,modi-
ficationstotheparameterscouldhaveapotentiallyharmfulimpactontheinherentknowledgeof
themodel.
Discussion.Modeleditingprovidesaprecisewaytomitigatehallucinationsinducedbyspecific
misinformationwithoutextensiveretraining.However,thesemethodsstrugglewithlarge-scale
updatesandcanadverselyaffectthemodel’soverallperformance,particularlywhencontinuous
editsareapplied.Consequently,futureresearchshouldfocusonimprovingmodeleditingtohandle
large-scaleknowledgeupdatesmoreefficientlyandaddresshallucinationscausedbysocialbiases.
5.1.3 RAG. Typically,RAG[108,162,274]followsaretrieve-then-readpipeline,whererelevant
knowledgeisfirstlyretrievedbyaretriever[144]fromexternalsources,andthenthefinalresponseis
generatedbyagenerator conditioningonbothuserqueryandretrieveddocuments.Bydecoupling
external knowledge from LLM, RAG can effectively alleviate the hallucination caused by the
knowledge gap without affecting the performance of LLM. Common practices can be divided
intothreeparts,asshowninFigure4:one-timeretrieval,iterativeretrieval,andposthocretrieval,
dependingonthetimingofretrieval.
One-timeRetrieval.One-timeretrievalaimstodirectlyprependtheexternalknowledgeobtained
fromasingleretrievaltotheLLMs’prompt.Rametal.[252]introducedIn-contextRALM,which
entails a straightforward yet effective strategy of prepending chosen documents to the input
textofLLMs.BeyondconventionalknowledgerepositoriessuchasWikipedia,ongoingresearch
endeavorshaveexploredalternativeavenues,specificallytheutilizationofknowledgegraphs
(KGs).TheseKGsserveasapivotaltoolforpromptingLLMs,facilitatingtheirinteractionwith
themostrecentknowledge,andelicitingrobustreasoningpathways[14,246,325].Varshneyetal.
[302]introducetheParametricKnowledgeGuiding(PKG)framework,enhancingLLMswith
domain-specificknowledge.PKGemploysatrainablebackgroundknowledgemodule,aligningit
withtaskknowledgeandgeneratingrelevantcontextualinformation.
IterativeRetrieval.Whenconfrontedwithintricatechallengeslikemulti-stepreasoning[340]and
long-formquestionanswering[82,280],traditionalone-timeretrievalmayfallshort.Addressing
thesedemandinginformationneeds,recentstudieshaveproposediterativeretrieval,whichallows
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

42:22 L.Huangetal.
forcontinuouslygatheringknowledgethroughoutthegenerationprocess.Recognizingthesubstan-
tialadvancementschain-of-thoughtprompting[322]hasbroughttoLLMsinmulti-stepreasoning,
numerousstudies[112,297,342]trytoincorporateexternalknowledgeateachreasoningstepand
furtherguideretrievalprocessbasedonongoingreasoning,reducingfactualerrorsinreasoning
chains.Buildinguponchain-of-thoughtprompting,Pressetal.[244]introducedself-ask.Diverging
fromtheconventionalcontinuous,undelineatedchain-of-thoughtprompting,self-ask delineates
thequestionitintendstoaddressateachstep,subsequentlyincorporatingasearchactionbasedon
thefollow-upquestion.Insteadofsolelydependingonchain-of-thoughtpromptingforretrieval
guidance,bothFengetal.[86]andShaoetal.[269]employedaniterativeretrieval-generation
collaborative framework, where a model’s response serves as an insightful context to procure
morerelevantknowledge,subsequentlyrefiningtheresponseinthesucceedingiteration.Beyond
multi-stepreasoningtasks,Jiangetal.[138]shiftedtheiremphasistolong-formgeneration.They
proposedanactiveretrievalaugmentedgenerationframework,whichiterativelytreatstheupcom-
ingpredictionasaquerytoretrieverelevantdocuments.Ifthepredictioncontainstokensoflow
confidence,thesentenceundergoesregeneration.Inadditiontousingiterativeretrievaltoimprove
intermediategenerations,Zhangetal.[367]presentedMixAlign,whichiterativelyrefinesuser
questionsusingmodel-basedguidanceandseekingclarificationsfromusers,ultimatelyenhancing
thealignmentbetweenquestionsandknowledge.
PosthocRetrieval.Beyondthetraditionalretrieve-then-read paradigm,alineofworkhasdelved
intoposthocretrieval,refiningLLMoutputsthroughsubsequentretrieval-basedrevisions.To
enhancethetrustworthinessandattributionofLLMs,Gaoetal.[93]adoptedtheresearch-then-revise
workflow,whichinitiallyresearchrelevantevidenceandsubsequentlyrevisetheinitialgeneration
based on detected discrepancies with the evidence. Similarly, Zhao et al. [377] introduced the
verify-and-edit frameworktoenhancethefactualaccuracyofreasoningchainsbyincorporating
externalknowledge.Forreasoningchainsthatshowlower-than-averageconsistency,theframework
generatesverifyingquestionsandthenrefinestherationalesbasedonretrievedknowledge,ensuring
amorefactualresponse.Yuetal.[354]enhancedtheposthocretrievalmethodthroughdiverse
answer generation. Instead of generating just a single answer, they sample various potential
answers,allowingforamorecomprehensiveretrievalfeedback.Additionally,byemployingan
ensemblingtechniquethatconsidersthelikelihoodoftheanswerbeforeandafterretrieval,they
furthermitigatetheriskofmisleadingretrievalfeedback.
Discussion.OnecrucialadvantageofRAGmethodologyisitseffectivenessinmitigatinghalluci-
nationscausedbyknowledgegaps,andtheirgenerality,whichallowsforapplicationacrossany
domain.Thisflexibilityisfurtherenhancedbythemodularityoftheapproach,treatingexternal
knowledgebaseslikeplug-insthatcanbeswappedormodifiedasneeded.Intermsofthedrawbacks,
itcanbeeasilyimpactedbyirrelevantretrievals,whichmaydecreasetheoverallperformanceby
introducingnoiseorincorrectinformationintotheresponsegenerationprocess.Furthermore,the
currentparadigmexhibitsshallowinteractionsbetweentheretrieverandgeneratorcomponents,
leadingtosuboptimalknowledgeutilization.Hence,futureresearchshouldfocusondevelopinga
robustRAGsystemthatminimizestheimpactofirrelevantretrieval,aswellasintegratingadaptive
learningcomponentsthatcandynamicallyadjustretrievalstrategiesbasedonthecontextofthe
queryandtheperformanceofpreviousinteractions.
5.2 MitigatingTraining-relatedHallucination
Training-relatedhallucinationstypicallyarisefromtheintrinsiclimitationsofthearchitecture
andtrainingstrategiesadoptedbyLLMs.Inthiscontext,wediscussvariousoptimizationmethods
rangingfromtrainingstages(Section5.2.1)andalignmentstages(SFTandRLHF)(Section5.2.2),
aimingtomitigatehallucinationswithinthetrainingprocess.
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

ASurveyonHallucinationinLargeLanguageModels 42:23
5.2.1 MitigatingPretraining-relatedHallucination. Onesignificantavenueofresearchinmiti-
gatingpretraining-relatedhallucinationcentersonthelimitationsinherentinmodelarchitectures,
especiallyunidirectionalrepresentationandattentionglitches.Inlightofthis,numerousstudieshave
delvedintodesigningnovelmodelarchitecturesspecificallytailoredtoaddresstheseflaws.To
addressthelimitationsinherentinunidirectionalrepresentation,Lietal.[177]introducedBATGPT
whichemploysabidirectionalautoregressiveapproach.Thisdesignallowsthemodeltopredictthe
nexttokenbasedonallpreviouslyseentokens,consideringbothpastandfuturecontexts,thus
capturingdependenciesinbothdirections.Buildingonthisidea,Liuetal.[186]highlightedthe
potentialofencoder-decodermodelstomakebetteruseoftheircontextwindows,suggestinga
promisingdirectionforfutureLLMsarchitecturedesign.Besides,recognizingthelimitationsofsoft
attentionwithinself-attention-basedarchitecture,Liuetal.[180]proposedattention-sharpening
regularizers.Thisplug-and-playapproachspecifiesself-attentionarchitecturesusingdifferentiable
lossterms[361]topromotesparsity,leadingtoasignificantreductioninreasoninghallucinations.
Inthepre-trainingphaseofLLMs,thechoiceofobjectiveplaysapivotalroleindeterminingthe
model’sperformance.However,conventionalobjectivescanleadtofragmentedrepresentationsand
inconsistenciesinmodeloutputs.Recentadvancementshavesoughttoaddressthesechallengesby
refiningpre-trainingstrategies,ensuringrichercontextcomprehension,andcircumventingbiases.
AddressingtheinherentlimitationsintrainingLLMs,whereunstructuredfactualknowledgeata
documentleveloftengetschunkedduetoGPUmemoryconstraintsandcomputationalefficiency,
leadingtofragmentedinformationandincorrectentityassociations,Leeetal.[157]introduceda
factuality-enhancedtrainingmethod.ByappendingaTOPICPREFIXtoeachsentenceinfactual
documents,theapproachtransformsthemintostandalonefacts,significantlyreducingfactual
errorsandenhancingthemodel’scomprehensionoffactualassociations.Similarly,consideringthat
randomlyconcatenatingshorterdocumentsduringpre-trainingmightintroduceinconsistencies
in model outputs, Shi et al. [272] proposed In-Context Pretraining, an innovative approach in
whichLLMsaretrainedonsequencesofrelateddocuments.Byalteringthedocumentorder,this
methodaimstomaximizesimilaritywithinthecontextwindows.ItexplicitlyencouragesLLMs
to reason across document boundaries, potentially bolstering the logical consistency between
generations.
Discussion.Strategiesdesignedtomitigatepretraining-relatedhallucinationstypicallyarefunda-
mental,potentiallyyieldingsignificantimprovements.However,theytypicallyinvolvemodifica-
tionstopre-trainingarchitecturesandobjectives,whicharecomputationallyintensive.Moreover,
theseintegrationsmaylackbroadapplicability.Movingforward,thefocusshouldbeondeveloping
adaptableandefficientstrategiesthatcanbeuniversallyappliedwithoutextensivesystemoverhaul.
5.2.2 MitigatingMisalignmentHallucination. Hallucinationsinducedduringalignmentoften
stemfromcapabilitymisalignmentandbeliefmisalignment.However,definingtheknowledge
boundaryofLLMsproveschallenging,makingitdifficulttobridgethegapbetweenLLMs’inher-
entcapabilitiesandtheknowledgepresentedinhuman-annotateddata.Whilelimitedresearch
addressescapabilitymisalignment,thefocusmainlyshiftstowardbeliefmisalignment.
Hallucinationsstemmingfrombeliefmisalignmentoftenmanifestassycophancy,atendencyof
LLMstoseekhumanapprovalinundesirableways.Thissycophanticbehaviorcanbeattributedto
thefactthathumanpreferencejudgmentsoftenfavorsycophanticresponsesovermoretruthful
ones[270],pavingthewayforrewardhacking[264].Toaddressthis,astraightforwardstrategyis
toimprovehumanpreferencejudgmentsand,byextension,thepreferencemodel.Recentresearch
[25,264]hasinvestigatedtheuseofLLMstoassisthumanlabelersinidentifyingoverlookedflaws.
Additionally,Sharmaetal.[270]discoveredthataggregatingmultiplehumanpreferencesenhances
feedbackquality,therebyreducingsycophancy.
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

42:24 L.Huangetal.
Besides,modificationstoLLMs’internalactivationshavealsoshownthepotentialtoaltermodel
behavior.Thiscanbeachievedthroughmethodslikefine-tuning[323]oractivationsteeringduring
inference[68,116,285].Specifically,Weietal.[323]proposedasynthetic-dataintervention,fine-
tuninglanguagemodelsusingsyntheticdatawheretheclaim’sgroundtruthisindependentofa
user’sopinion,aimingtoreducesycophantictendencies.
Another avenue of research [259, 260] has been to mitigate sycophancy through activation
steering.Thisapproachinvolvesusingpairsofsycophantic/non-sycophanticpromptstogenerate
thesycophancysteeringvectorderivedfromaveragingthedifferencesinintermediateactivations.
Duringinference,subtractingthisvectorcanproducelesssycophanticLLMoutputs.
Discussion. Mitigating hallucinations through post-training methods represents a direct and
effectiveapproach,bypassingthecomplexitiesassociatedwithdatasourcingandpre-training.
However,anotablegapincurrentresearchisthelimitedattentiongiventocapabilitymisalign-
mentwithinLLMs.Futureresearchshouldprioritizeunderstandingtheknowledgeboundariesin
capabilityalignmenttoaddresshallucinationseffectively.
5.3 MitigatingInference-relatedHallucination
DecodingstrategiesinLLMsplayapivotalroleindeterminingthefactualityandfaithfulnessof
thegeneratedcontent.However,asanalyzedinSection3.3,imperfectdecodingoftenresultsin
outputsthatmightlackfactualityorstrayfromtheoriginalcontext.Inthissubsection,weexplore
twoadvancedstrategiesaimedatrefiningthedecodingstrategytoenhanceboththefactualityand
faithfulnessoftheLLMs’outputs.
5.3.1 FactualityEnhancedDecoding. FactualityEnhancedDecodingaimstoimprovetherelia-
bilityofoutputsfromLLMsbyprioritizingthefactualityoftheinformationtheygenerate.Thisline
ofmethodsfocusesonaligningmodeloutputscloselywithestablishedreal-worldfacts,thereby
minimizingtheriskofdisseminatingfalseormisleadinginformation.
FactualityDecoding.Consideringtherandomnessinthesamplingprocesscanintroducenon-
factualcontentintoopen-endedtextgeneration,Leeetal.[157]introducedthefactual-nucleus
samplingalgorithmthatdynamicallyadjuststhenucleusprobability𝑝throughoutsentencegenera-
tion.Bydynamicallyadjustingthenucleusprobabilitybasedondecayfactorsandlowerboundaries
andresettingthenucleusprobabilityatthebeginningofeverynewsentence,thedecodingstrategy
strikesabalancebetweengeneratingfactualcontentandpreservingoutputdiversity.Moreover,
somestudies[31,217]positthattheactivationspaceofLLMscontainsinterpretablestructures
relatedtofactuality.Buildingonthisidea,Lietal.[169]introducedInference-TimeIntervention.
Thismethodfirstidentifiesadirectionintheactivationspaceassociatedwithfactuallycorrect
statements and then adjusts activations along the truth-correlated direction during inference.
Byrepeatedlyapplyingsuchintervention,LLMscanbesteeredtowardsproducingmorefactual
responses.Similarly,Chuangetal.[58]delvedintoenhancingthefactualityofLLM’sdecoding
processfromaperspectiveoffactualknowledgestorage.Theyexploitthehierarchicalencoding
offactualknowledgewithintransformerLLMs,notingthatlower-levelinformationiscaptured
inearlierlayersandsemanticinformationinthelaterones.Drawinginspirationfrom[172],they
introduceDoLa,astrategythatdynamicallyselectsandcontrastslogitsfromdifferentlayersto
refinedecodingfactuality.Byplacingemphasisonknowledgefromhigherlayersanddownplaying
thatfromthelowerlayers,DoLashowcasesitspotentialtomakeLLMsmorefactual,thusreducing
hallucinations.
Post-editingDecoding.Unlikemethodsthatdirectlymodifytheprobabilitydistributiontoprevent
hallucinationsduringtheinitialdecoding,post-editingdecodingseekstoharnesstheself-correction
capabilitiesofLLMs[234]torefinetheoriginallygeneratedcontentwithoutrelyingonanexternal
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

ASurveyonHallucinationinLargeLanguageModels 42:25
knowledgebase.Dhuliawalaetal.[73]introducedtheCoVE),whichoperatesundertheassumption
that,whenappropriatelyprompted,LLMscanself-correcttheirmistakesandprovidemoreaccurate
facts.Startingwithaninitialdraft,itfirstformulatesverificationquestionsandthensystematically
answersthosequestionsinordertofinallyproduceanimprovedrevisedresponse.Similarly,Ji
etal.[135]focusedonthemedicaldomainandintroducedaniterativeself-reflectionprocess.This
processleveragestheinherentabilityofLLMstofirstgeneratefactualknowledgeandthenrefine
theresponseuntilitalignsconsistentlywiththeprovidedbackgroundknowledge.
Discussion.Factualitydecodingmethods,whichtypicallyassessthefactualityateachdecoding
step,canoffersubstantialimprovements.Furthermore,duetotheirplug-and-playnature,they
allowforapplicationwithouttheneedforcomputation-intensivetraining.Nevertheless,oneof
theprimarylimitationsofthesemethodsliesinbalancingfactualaccuracywithmaintainingthe
diversityandinformativenessofthegeneratedcontent,whichcansometimesleadtocompromises
ineitheraspect.Ontheotherhand,post-editingdecodingstrategies,despitetheireffectiveness,
heavilyrelyontheself-correctioncapabilitiesofLLMs,whichmaybeunreliable.Furthermore,
applyingself-reflectioncanbetime-consuming,limitingtheirpracticalityforreal-timeapplications.
Hence,itiscrucialtoachieveanoptimalbalancebetweenfactualityandcomputationalefficiency.
5.3.2 FaithfulnessEnhancedDecoding. Ontheotherhand,FaithfulnessEnhancedDecoding
prioritizesalignmentwiththeprovidedcontextandalsoemphasizesenhancingtheconsistency
withinthegeneratedcontent.Thus,inthissection,wesummarizeexistingworkintotwocategories,
includingContextConsistency andLogicalConsistency.
ContextConsistency.IntheeraofLLMs,theissueoffaithfulnesshallucinationtypicallyliesin
insufficientattentiontothegivencontext,whichinspirednumerousresearchtodesigninference-
timestrategiestoenhancecontextconsistency.Shietal.[271]proposedcontext-awaredecoding
(CAD),whichmodifiesthemodel’soriginaloutputdistributioninacontrastiveformulation[172].
Byamplifyingthedifferencebetweenoutputprobabilitieswithandwithoutcontext,CADencour-
agestheLLMtofocusmoreoncontextualinformationratherthanover-relyonpriorknowledge.
However,duetotheinherenttradeoffbetweendiversityandcontextattribution[102,359],overem-
phasizingcontextualinformationcanreducediversity.Toaddressthis,Changetal.[36]introduced
adynamicdecodingalgorithmtobolsterfaithfulnesswhilepreservingdiversity.Specifically,the
algorithminvolvestwoparalleldecodingsteps,onewiththecontextandonewithout.Duringthe
decoding,theKLdivergencebetweentwotokendistributionsservesasaguidingsignal,indicating
therelevanceofthesourcecontext.Thissignalisutilizedtodynamicallyadjustthesamplingtem-
peraturetoimprovesourceattributionwhenthesourceisrelevant.Inaparallellineofwork,Choi
etal.[53]introducedknowledge-constraineddecoding,whichemployedatoken-levelhallucination
detectiondiscriminatortoidentifycontextualhallucinationsandthenguidesthefaithfulgeneration
processbyreweighingthetokendistribution.Inadditiontomodifyingoutputdistributioninplace
toenhancecontextualattention,anotherlineofworkhasexploredagenericpost-editapproachto
enhancefaithfulness.Gaoetal.[93]adoptedaresearch-and-reviseworkflow,wheretheresearch
stageraisesquestionsaboutvariousaspectsofthemodel’sinitialresponseandgathersevidence
foreachquery,whiletherevisionstagedetectsandrevisesanydisagreementsbetweenthemodel’s
responseandtheevidence.Similarly,Leietal.[158]firstdetectedcontextualhallucinationsat
boththesentenceandentitylevelsandthenincorporatedthejudgmentstorefinethegenerated
response.Moreover,severalstudieshaveexploredmethodstoovercomethesoftmaxbottleneck,
whichconstrainstheexpressionofdiversityandfaithfulrepresentations.Theseapproachesinclude
employingamixtureofSoftmax,whichusesmultiplehiddenstatestocomputesoftmaxmultiple
times and merge the resulting distributions [339] and incorporating pointer networks, which
enablesLLMstocopythecontextwords[37],therebyreducingcontexthallucinations.
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

42:26 L.Huangetal.
LogicalConsistency.Inspiredbythehumanthinkingprocess,chain-of-thought[322]hasbeen
introducedtoencourageLLMstodecomposecomplexproblemsintoexplicitlyintermediatesteps,
thereby enhancing the reliability of the reasoning process. Despite effective, recent research
[154, 298] demonstrated that the intermediate rationales generated by LLMs do not faithfully
capturetheirunderlyingbehavior.Abranchofresearchhasbeeninspiredtoimprovethecon-
sistencyofintermediaterationalesgeneratedbyLLMs,particularlyinmulti-stepreasoning[60]
andlogicalreasoning[18].Toenhancetheself-consistencyinchain-of-thought,Wangetal.[314]
employedaknowledgedistillationframework.Theyfirstgenerateaconsistentrationaleusing
contrastivedecoding[172]andthenfine-tunethestudentmodelwithacounterfactualreason-
ingobjective,whicheffectivelyeliminatesreasoningshortcuts[27]thatderiveanswerswithout
consideringtherationale.Furthermore,byemployingcontrastivedecodingdirectly,LLMscan
reducesurface-levelcopyingandpreventmissedreasoningsteps[226].Inaddition,Lietal.[164]
conductedadeepanalysisofthecausalrelevanceamongthecontext,CoT,andanswerduring
unfaithfulreasoning.Analysisrevealedthattheunfaithfulnessissueliesintheinconsistenciesinthe
contextinformationobtainedbytheCoTandtheanswer.Toaddressthis,theyproposedinferential
bridging,whichtakestheattributionmethodtorecallcontextualinformationashintstoenhance
CoTreasoningandfilteroutnoisyCoTsthathavelowsemanticconsistencyandattributionscores
tothecontext.Pauletal.[238]decomposedthereasoningprocessintotwomodules:aninference
module,whichemploysDirectPreferenceOptimization[250]toaligntheLLMtowardspreferring
correctreasoningchainsovercounterfactualchains,andareasoningmodule,whichencourages
theLLMtoreasonfaithfullyoverthereasoningstepsusingacounterfactualandcausalpreference
objective.Comparedtonaturallanguagereasoning,logicalreasoningdemandsrigorouslogical
calculation,whereasplaintextoftenlackspreciselogicalstructure,leadingtounfaithfulreasoning.
Toaddressthis,Xuetal.[334]introducedSymbolicCoT(SymbCoT),whichincorporatessymbolic
expressionswithinCoTtodescribeintermediatereasoningsteps.Specifically,SymbCoTtranslates
thenaturallanguagecontextintoasymbolicrepresentationandthenformulatesastep-by-step
plantoaddressthelogicalreasoningproblem,followedbyaverifiertocheckthetranslationand
reasoningchain,therebyensuringfaithfullogicalreasoning.
Discussion.FaithfulnessEnhancedDecodingsignificantlyadvancesthealignmentofLLMoutputs
withprovidedcontextsandenhancestheinternalconsistencyofthegeneratedcontent.However,
strategiessuchasCADoftenlackadaptivemechanisms,limitingtheireffectivenessinscenarios
thatdemanddynamicattentiontocontext.Furthermore,manydecodingstrategiesrequirethe
integrationofadditionalmodelsthatdonotfocusoncontext,introducingsignificantcomputational
overheadandreducingefficiency.
6 HallucinationsinRetrievalAugmentedGeneration
RAGhasemergedasapromisingstrategytomitigatehallucinationsandimprovethefactualityof
LLMoutputs[129,162,252,273].Byincorporatinglarge-scaleexternalknowledgebasesduring
inference, RAG equips LLMs with up-to-date knowledge, thus reducing the potential risk of
hallucinationduetotheinherentknowledgeboundariesofLLMs[257].Despitebeingdesigned
tomitigateLLMhallucinations,retrieval-augmentedLLMscanstillproducehallucinations[16].
HallucinationsinRAGpresentconsiderablecomplexities,manifestingasoutputsthatareeither
factually inaccurate or misleading. These hallucinations occur when the content generated by
theLLMdoesnotalignwithreal-worldfacts,failstoaccuratelyreflecttheuser’squery,orisnot
supportedbytheretrievedinformation.Suchhallucinationscanstemfromtwoprimaryfactors:
retrievalfailure (Section 6.1)and generationbottleneck (Section 6.2). Througha comprehensive
analysis of the limitations present in current RAG systems, we aim to shed light on potential
improvementsforretrieval-augmentedLLMs,pavingthewayformorereliableIRsystems.
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

ASurveyonHallucinationinLargeLanguageModels 42:27
Table5. ExamplesofEachCategoryofUserQueriesThatMayLeadtoLLMHallucinations
Type ExampleDialog Explanation
Retrievedcontext:Athighaltitudes,waterboilsatlower
temperaturesthanatsealevel,suchas95℃atelevations Thisqueryinvolvesabasicscientificfactthatshouldbe
above2,000meters.Thisaltitude-inducedreductioncanaffect availablewithinthemodel’sparametricknowledge.
Retrieval
cookingtimesandmethods. However,thesysteminappropriatelyretrievesanduses
Intent
altitude-specificinformationaboutboilingtemperatures,
Query:Whatistheboilingpointofwateratsealevel?
leadingtoanincorrectresponseforsea-levelconditions.
Response:Theboilingpointofwateratsealevelis95℃.
Retrievedcontext:TheHennesseyVenomGTfamously
setaspeedrecordbycompletingamileonaracetrackin
Thequeryisambiguousbecauseitdoesnotspecifywhe-
32seconds,highlightingitsperformanceinmotorsportevents.
Ambiguous theritreferstoahumanrunneroravehicle.Theretrieval
Queries Query:What’stherecordforthefastestmilerunontrack? systemerroneouslypullsinformationrelatedtocarracing
recordsinsteadofathletics.
Response:Thefastestmileonatrackwascompletedin
32secondsbytheHennesseyVenomGT.
Retrievedcontext:AlexanderFleming,knownforhisground-
breakingworkindiscoveringpenicillin,significantlyinfluenced Theretrievalsystemonlymanagestofetchinformation
modernantibiotics.Fleming’sdiscoverysavedcountlesslives. aboutFleming’sprofessionalachievementsinthediscovery
Complex
ofpenicillin.However,thedocumentdoesnotprovideinforma-
Queries Query:Whichuniversitydidthescientistwhodiscovered
tionabouthiseducationalbackground,thusthemodelgeneratesa
penicillingraduatefrom?
hallucinatoryanswer.
Response:AlexanderFleminggraduatedfromOxfordUniversity.
ContentmarkedinRedrepresentsthehallucinatoryoutput.
6.1 RetrievalFailure
TheretrievalprocessisacrucialinitialstepintheRAGframework,taskedwithretrievingthemost
relevantinformationforinformation-seekingqueries.Consequently,failuresintheretrievalstage
canhaveseriousdownstreameffectsontheRAGpipeline,leadingtohallucinations.Thesefailures
typicallystemfromthreeprimaryparts:theformulationofuserqueries,thereliabilityandscope
ofretrievalsources,andtheeffectivenessoftheretriever.
6.1.1 UserQueries. Userqueriesplayafundamentalroleinguidingtheretrievalprocesswith
RAGsystems.Thespecificityandclarityofthesequeriescriticallyinfluencetheeffectivenessof
retrievaloutcomes.Inthissection,wediscussfactorsthatmaycontributetohallucinationsfrom
three perspectives: blind retrieval, misinterpretation of ambiguous queries, and the challenges
in accurate retrieval of complex queries. Some examples are presented in Table 5 for a better
understanding.
RetrievalIntentDecisions.Notallqueriesnecessitateretrieval.Blindretrievalforqueriesthat
do not require external knowledge can counterproductively lead to misleading responses. As
showninTable5,thequeryabout“theboilingpointofwateratsealevel”pertainstoabasicscien-
tificfactthatthemodelcouldaddresswithoutexternalretrieval.However,theretrievalsystem
wasinappropriatelyactivated,blindlyretrievinginaccurateinformationandconsequentlylead-
ingtoanundesirableresponse.Consequently,severalstudies[74,201,225,374]haveproposed
to make a shift from passive retrieval to adaptive retrieval. In general, these strategies can be
divided into two categories: heuristic-based and self-aware judgment. Heuristic-based methods
employ heuristic rulesto determine the necessity of retrieval.For instance,Mallen et al. [201]
observedapositivecorrelationbetweenLLMs’memorizationcapabilitiesandentitypopularity
and suggested triggering retrieval only when the entity popularity in the user query falls be-
lowacertainthreshold.Similarly,Jeongetal.[133]determinedthetimingofretrievalbasedon
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

42:28 L.Huangetal.
thequerycomplexity,whereasAsaietal.[11]consideredwhetherthequeryisfactualrelevant.
Self-awarejudgment leveragesthemodels’intrinsicjudgmenttodecidethenecessityforIR.Feng
etal.[85],Renetal.[257]andWangetal.[317]directlypromptedLLMsforretrievaldecisions,
recognizingthatLLMspossessacertainlevelofawarenessregardingtheirknowledgebound-
aries[141,346].Moreover,Jiangetal.[138]introducedanactiveretrievalstrategythattriggers
retrievalonlywhentheLLMgenerateslow-probabilitytokens.Similarly,Suetal.[284]notonly
consideredtheuncertaintyofeachtokenbutalsoitssemanticcontributionandimpactonthesub-
sequentcontext.Morerecently,Chengetal.[48]proposedfourorthogonalcriteriafordetermining
the retrieval timing, which include intent-aware, knowledge-aware, time-sensitive-aware, and
self-aware.
AmbiguousQueries.Ambiguoususerqueries,containingomission,coreference,andambigu-
ity,significantlycomplicatetheretrievalsystem’sabilitytofetchpreciselyrelevantinformation,
therebyincreasingthelikelihoodofgeneratingundesirableresponses.AsshowninTable5,due
to the ambiguity of the query about “the record for the fastest mile run on track,” the retrieval
systemerroneouslyretrievedinformationfromautomobileracingevents,whichledthemodel
togeneratearesponsesuitedforvehiclesinsteadofathletes.Aprevalentmitigationstrategyis
queryrewriting,wherequeriesarerefinedanddecontextualizedtobettermatchrelevantdocu-
ments.Wangetal.[313]andJagermanetal.[130]haveexploredpromptingapproacheswhere
theLLMispromptedtogenerateapseudo-documentorrationalebasedontheoriginalquery,
whichisthenusedforfurtherretrieval.Additionally,Maetal.[197]introducedatrainablerewriter
whichistrainedusingthefeedbackfromtheLLMviareinforcementlearning.Maoetal.[204]
employed the feedback signals from the reranker to train the rewrite model, thus eliminating
therelianceonannotateddata.However,thechallengesdeepeninconversationalsearch,which
encountersamorecomplexissueofcontext-dependentqueryunderstandingwiththelengthy
conversationalhistory.Addressingthis,Yoonetal.[347]proposedasimilarframeworkforoptimiz-
ingtheLLMtogenerateretriever-preferredqueryrewrites.Thisoperatedbygeneratingavariety
ofqueriesandthenusingthepreferenceoftherankofretrievedpassagetooptimizethequery
rewritingmodel.
ComplexQueries.Complexuserqueries,characterizedbyrequiringintensivereasoning[282]or
encompassingmultipleaspects[268,315],posesignificantchallengestotheretrievalsystem.Such
queriesrequireadvancedunderstandinganddecompositioncapabilities,whichmayexceedthe
currentcapabilitiesofthecurrentretrievalmethodsbasedonkeywordorsemanticmatching,often
leadingtopartialorincorrectretrievals.Forexample,asshowninTable5,duetothemulti-step
natureofthequeryabout“Whichuniversitydidthescientistwhodiscoveredpenicillingraduatefrom?,”
directretrievaloftenleadstoincompleteresults,therebyresultinginhallucinatoryresponses.A
commonapproachinvolvesquerydecomposition,wherethecomplexqueryisdecomposedinto
sub-queries to facilitate more accurate IR. For instance, Wang et al. [315] implemented a sub-
aspectexplorerthatutilizestheextensiveworldknowledgeembeddedLLMstoidentifypotential
sub-aspectsofuserqueries,therebyprovidingexplicitinsightsintotheuser’sunderlyingintents.
Similarly,Shaoetal.[268]concentratedonthedemandingtaskofexpositorywriting,aimingat
retrievingcomprehensiveinformationtocomposeWikipedia-likearticlesfromscratchonaspecific
topic. This approach involves decomposing the topic into various perspectives and simulating
multi-turn conversations with LLMs, each personified with different perspectives for question
asking.Additionally,Caoetal.[32]andChuetal.[56]exploredknowledge-intensivecomplex
reasoningandemployedadivide-and-conquerstrategy.Thisstrategybeginswithdecomposing
complex questions into question trees, where at each node, the LLM retrieves and aggregates
answersfromdiverseknowledgesources.
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

ASurveyonHallucinationinLargeLanguageModels 42:29
6.1.2 RetrievalSources. Thereliabilityandscopeofretrievalsourcesarecrucialdeterminantsof
theefficacyofRAGsystems.Effectiveretrievaldependsnotonlyontheclarityoftheuserqueries
butalsoonthequalityandcomprehensivenessofthesourcesfromwhichinformationisretrieved.
When these sources contain factually incorrect or outdated information, the risk of retrieval
failuresincreasessignificantly,potentiallyleadingtothegenerationofincorrectormisleading
information.
AsthelandscapeofcontentcreationevolveswiththerapidadvancementofArtificialIntelligence
GeneratedContent[33],anincreasingvolumeofLLM-generatedcontentispermeatingtheinternet,
subsequentlybecomingintegratedintoretrievalsources[39].Thisintegrationisreshapingthe
dynamicsofIR,asevidencedbyrecentempiricalstudies[67,335]suggestingthatmodernretrieval
models tend to favor LLM-generated content over human-authored content. Recent research
[44]hasexploredtheimplicationsofprogressivelyintegratingLLM-generatedcontentintoRAG
systems.Thefindingsindicatethat,withoutappropriateintervention,human-generatedcontent
mayprogressivelyloseitsinfluencewithinRAGsystems.Additionally,Tanetal.[289]investigated
the performance of RAG systems when incorporating LLM-generated into retrieved contexts,
revealingasignificantbiasfavoringgeneratedcontexts.Thisbiasstemsfromthehighsimilarity
betweengeneratedcontextandquestions,as wellasthesemanticincompleteness ofretrieved
contexts.Moreseriously,thepropensityofLLMstoproducefactuallyinaccuratehallucinations
exacerbatesthereliabilityissuesofretrievalsources.AsLLM-generatedcontentoftencontains
factualerrors,itsintegrationintoretrievalsourcescanmisleadretrievalsystems,furtherdiminishing
theaccuracyandreliabilityoftheinformationretrieved.
Tocombatthesebiases,severalapproacheshavebeenexplored.Inspiredbycommonpracticein
pre-trainingdataprocessing[23],Asaietal.[12]proposedascenariothatincorporatesaquality
filterdesignedtoensurethehighqualityoftheretrievaldatastore.Additionally,Panetal.[235]
proposedCredibility-awareGeneration,whichequipsLLMswiththeabilitytodiscernandhandle
informationbasedonitscredibility.Thisapproachassignsdifferentcredibilitylevelstoinformation,
consideringitsrelevance,temporalcontext,andthetrustworthinessofitssource,thuseffectively
reducingtheimpactofflawedinformationinRAGsystems.
6.1.3 Retriever. Whentheuserqueryisexplicitandtheretrievalsourceisreliable,theeffec-
tivenessoftheretrievalprocessdependscruciallyontheperformanceoftheretriever.Insuch
scenarios,theretriever’seffectivenessissignificantlycompromisedbyimproperchunkingand
embeddingpractices.
Chunking. Given the extensive nature of retrieval sources, which often encompass lengthy
documentslikewebpages,itposessignificantchallengesforLLMswithlimitedcontextlength.Thus,
chunkingemergesasanindispensablestepinRAG,whichinvolvessegmentingthesevoluminous
documentsintosmaller,moremanageablechunkstoprovidepreciseandrelevantevidenceforLLMs.
Accordingtoactualneeds,thechunkinggranularityrangesfromdocumentstoparagraphs,even
sentences.However,inappropriateretrievalgranularitycancompromisethesemanticintegrity
and affect the relevance of retrieved information [221], thereby affecting the performance of
LLMs.Fixed-sizechunking,whichtypicallybreaksdownthedocumentsintochunksofaspecified
lengthsuchas100-wordparagraphs,servesasthemostcrudeandprevalentstrategyofchunking,
whichiswidelyusedinRAGsystems[24,108,162].Consideringfixed-sizechunkingfallsshortin
capturestructureanddependencyoflengthydocuments,Sarthietal.[263]proposedRAPTOR,an
indexingandretrievalsystem.Byrecursivelyembedding,clustering,andsummarizingchunksof
text,RAPTORconstructsatreetocapturebothhigh-levelandlow-leveldetails.Whenretrieval,
RAPTORenablesLLMstointegrateinformationfromdifferentlevelsofabstraction,providing
a more comprehensive context for user queries. Instead of chunking text with a fixed chunk
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

42:30 L.Huangetal.
size,semanticchunkingadaptivelyidentifiesbreakpointsbetweensentencesthroughembedding
similarity,therebypreservingsemanticcontinuity[142].Furthermore,Chenetal.[43]pointed
outthelimitationsoftheexistingretrievalgranularity.Ontheonehand,whileacoarserretrieval
withalongercontextcantheoreticallyprovideamorecomprehensivecontext,itoftenincludes
extraneousdetailsthatcouldpotentiallydistractLLMs.Ontheotherhand,afine-grainlevelcan
providemorepreciseandrelevantinformation,ithaslimitationssuchasnotbeingself-contained
andlackingnecessarycontextualinformation.Toaddresstheseshortcomings,Chenetal.[43]
introducedanovelretrievalgranularity,proposition,whichisdefinedasatomicexpressionswithin
thetext,eachencapsulatingadistinctfactoidandpresentedinaconciseself-containednatural
languageformat.
Embedding.Oncetheretrievaltextischunked,textchunksaresubsequentlytransformedinto
vectorrepresentationviaanembeddingmodel.Sucharepresentationschemeissupportedbythe
well-knowndatastructureofvectordatabase[140],whichsystematicallyorganizesdataaskey-
valuepairsforefficienttextretrieval.Inthismanner,therelevancescorecanbecomputedaccording
tothesimilarityfunctionbetweenthetextrepresentationandqueryrepresentation.However,a
sub-optimalembeddingmodelmaycompromiseperformance,whichaffectsthesimilarityand
matchingofchunkstouserqueries,potentiallymisleadingLLMs.Typically,astandardembedding
model[95,128,147,378]learnsthequeryandtextrepresentationswithencoder-basedarchitecture
(e.g.,BERT[72],RoBERTa[188])viacontrastivelearning[300],wherethelossisconstructedby
contrastingapositivepairofquery-documentagainstasetofrandomnegativepairs.However,these
embeddingsshowcasetheirlimitationswhenappliedtonewdomains,suchasmedicalandfinancial
applications[219,291].Inthesecases,recentstudies[70,231,273,328]proposetofine-tunethe
embeddingmodelsondomain-specificdatatoenhanceretrievalrelevance.Forexample,REPLUG
[273]utilizeslanguagemodelingscoresoftheanswersasaproxysignaltotrainthedenseretriever.
Morerecently,Muennighoffetal.[218]haveintroducedgenerativerepresentationalinstruction
tuning where a single LLM is trained to handle both generative and embedding tasks, which
largelyreducesinferencelatencyinRAGbycachingrepresentations.Despitetheseadvancements,
thefieldfaceschallenges,particularlywiththefine-tuningofhigh-performingyetinaccessible
embeddingmodels,suchasOpenAI’stext-embedding-ada-002.Addressingthisgap,Zhangetal.
[363]introducedanovelapproachforfine-tuningablack-boxembeddingmodelbyaugmentingit
withatrainableembeddingmodelwhichsignificantlyenhancestheperformanceoftheblack-box
embeddings.
6.2 GenerationBottleneck
Aftertheretrievalprocess,thegenerationstageemergesasapivotalpoint,responsibleforgener-
atingcontentthatfaithfullyreflectstheretrievedinformation.However,thisstagecanencounter
significantbottlenecksthatmayleadtohallucinations.WesummarizetwokeycapabilitiesofLLMs
thatarecloselyrelatedtothesebottlenecks:contextualawarenessandcontextualalignment.Each
playsanimportantroleinensuringthereliabilityandcredibilityoftheRAGsystem.
6.2.1 ContextualAwareness. Contextualawarenessinvolvesunderstandingandeffectivelyuti-
lizingcontextualinformationretrieved.ThissectiondiscussesthekeyfactorsthatimpacttheLLM’s
abilitytomaintaincontextualawareness,whichcanbecategorizedintothreemainparts:(1)the
presenceofnoisyretrievalincontext,(2)contextconflicts,and(3)insufficientutilizationofcontext
information.
NoisyContext.AsemphasizedinSection6.1,thefailureintheretrievalprocessmayinevitably
introduce irrelevant information, which will propagate into the generation stage. When the
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

ASurveyonHallucinationinLargeLanguageModels 42:31
generatorisnotrobustenoughtotheseirrelevantretrievals,itwillmisleadthegeneratorandeven
introducehallucinations[64].
Yoranetal.[348]conductedacomprehensiveanalysisontherobustnessofcurrentretrieval-
augmentedLLMs,revealingasignificantdecreaseinperformancewithrandomretrieval.While
usinganNLImodeltofilteroutirrelevantpassagesiseffective,thismethodcomeswiththetradeoff
ofinadvertentlydiscardingsomerelevantpassages.AmoreeffectivesolutionistotrainLLMsto
ignoreirrelevantcontextsbyincorporatingirrelevantcontextsintrainingdata.Similarly,Yuetal.
[353]introducedChain-of-Note,whichenablesLLMstofirstgeneratereadingnotesforretrieved
contextsandsubsequentlyformulatethefinalanswer.Inthisway,LLMscannotonlyfilterirrelevant
retrievaltoimprovenoiserobustnessbutalsorespondwithunknownwhenretrievalisinsufficient
toansweruserqueries.InadditiontoimprovingLLMrobustnessbylearningtoignoreirrelevant
contentinthecontext,severalstudies[137,173,319,332]proposetocompressthecontexttofilter
outirrelevantinformation.Specifically,Li[173]andJiangetal.[137]madeuseofsmalllanguage
models to compute self-information and perplexity for prompt compression, finding the most
informativecontent.Similarly,Wangetal.[319]proposedtofilteroutirrelevantcontentandleave
preciselysupportingcontentbasedonlexicalandinformation-theoreticapproaches.Besides,efforts
havebeenalsomadetoemploysummarizationmodelsascompressors.Xuetal.[332]presented
bothextractiveandabstractivecompressors,whicharetrainedtoimproveLLMs’performancewhile
keepingthepromptconcise.Liuetal.[185]involvedsummarizationcompressionandsemantic
compression,wheretheformerachievescompressionbysummarizingwhilethelatterremoves
tokenswithalowerimpactonthesemantic.
Context Conflict. Retrieval-augmented LLMs generate answers through the combined effect
of parametric knowledge and contextual knowledge. As discussed in Section 3.3.2, LLMs may
sometimesexhibitover-confidence,whichcanbringnewchallengestothefaithfulnessofRAG
systemswhenfacingknowledgeconflicts.KnowledgeconflictsinRAGaresituationswherecon-
textualknowledgecontradictsLLMs’parametricknowledge.Longpreetal.[191]firstinvestigated
knowledgeconflictsinopen-domainquestionanswering,whereconflictsareautomaticallycreated
byreplacingallspansofthegoldanswerintheretrievalcontextwithasubstitutedentity.Findings
demonstratethatgenerativeQAreadermodels(e.g.,T5)tendtotrustparametricmemoryover
contextualinformation.Byfurthertrainingtheretrievertolearntotrustthecontextualevidence
withaugmentedtrainingexamplesbyentitysubstitution,theissueofover-relianceonparametric
knowledgeismitigated.SimilarfindingsarealsoreportedbyLietal.[163]whodemonstratedthat
fine-tuningLLMsoncounterfactualcontextscaneffectivelyimprovethecontrollabilityofLLMs
whendealingwithcontradictscontexts.Alsobuildinguponcounterfactualdataaugmentation,
Neemanetal.[224]trainedmodelstopredicttwodisentangledanswers,onebasedoncontextual
knowledgeandtheotherleveragingparametricknowledgetoaddressknowledgeconflicts.Be-
sides,Zhouetal.[386]introducedtwoeffectiveprompting-basedstrategies,namelyopinion-based
prompts and counterfactual demonstrations. Opinion-based prompts transform the context to
narrators’statements,solicitingthenarrators’opinions,whereascounterfactualdemonstrations
employcounterfactualinstancestoimprovefaithfulnessinsituationsofknowledgeconflict.While
Longpreetal.[191]andLietal.[163]concentratedtheirresearchonthecontextofalimitedsingle
evidencesetting,Chenetal.[40]furtherexpandedthisstudytoconsideramorerealisticscenario
inwhichmodelsconsidermultipleevidencepassagesandfindmodelsrelyalmostexclusivelyon
contextualevidence.
Considering previous studies [163, 191] mostly focused on smaller models, Xie et al. [330]
raiseddoubtsabouttheapplicabilityoftheirconclusionsintheeraofLLMs.Suchheuristicentity-
level substitution may lead to incoherent counter-memory, thereby making it trivial for LLMs
tooverlooktheconstructknowledgeconflicts.BydirectlyelicitingLLMstogenerateacoherent
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

42:32 L.Huangetal.
counter-memorythatfactuallyconflictswiththeparametricmemory,LLMsexhibittheirhigh
receptivitytoexternalevidence.
ContextUtilization.Despitesuccessfullyretrievingevidencerelevanttofactoidqueries,LLMs
canencounterasignificantperformancedegradationduetoinsufficientutilizationofthecontext,
especiallyforinformationlocatedinthemiddleofthelongcontextwindow,anotableissueknown
asthelost-in-the-middlephenomenon[186].BeyondfactoidQA,recentstudieshavefurtherdemon-
stratedsuchamiddle-cursealsoholdsinabstractivesummarization[254],long-formQA[41]and
passageranking[290].Onepotentialexplanationliesintheuseofrotarypositionalembedding
(RoPE)[283],whichiswidelyusedinopen-sourceLLMs,duetoitsexcellentperformanceinlength
extrapolation[376].Asarepresentativerelativepositionembedding,RoPEfeaturesalong-term
decayproperty,whichinherentlybiasestheLLMtogiveprecedencetocurrentorproximatetokens,
therebydiminishingitsattentiononthosethataremoredistant.Anothercontributingfactoris
thatthemostsalientinformationoftenresidesatthebeginningortheendofpre-trainingdata,
acharacteristiccommonlyobservedinnewsreports[254].Suchanissuebringsforthchallenges
inretrieval-augmentedLLMs,asretrieval-augmentedLLMsaretypicallydesignedwithextensive
lengthstoaccommodatemoreretrievaldocuments.
To mitigate this crucial issue, He et al. [113] introduced several tasks specially designed for
informationseekingtoenhancethecapabilityofinformationutilizationbyexplicitlyrepeatingthe
questionandextractingtheindexofsupportingdocumentsbeforegeneratinganswers.Furthermore,
Zhangetal.[373]introducedMulti-scalePositionalEncoding(Ms-PoE),whichmitigatesthe
long-termdecayeffectcharacteristicofRoPEbyrescalingpositionindices.Ms-PoEprovidesa
plug-and-playsolutiontoenhancetheabilityofLLMstoeffectivelycaptureinformationinthe
middle of the context without the need for additional fine-tuning. Besides, Ravaut et al. [254]
proposed hierarchical and incremental summarization, which effectively preserves the salient
informationandcompressesthelengthofcontexttoavoidthemiddle-curse.
6.2.2 ContextualAlignment. ContextualalignmentensuresthatLLMoutputsfaithfullyalign
with relevant context. This section outlines the primary components of contextual alignment,
whichinclude:(1)sourceattributionand(2)faithfuldecoding.
SourceAttribution.Sourceattribution[120]inretrieval-augmentedLLMsreferstotheprocessby
whichthemodelidentifiesandutilizestheoriginsofinformationwithinitsgenerationprocess.
ThiscomponentiscrucialforensuringthattheoutputsofRAGsystemsarenotonlyrelevantbut
alsoverifiableandgroundedincrediblesources.
ToachievesourceattributioninRAGsystems,recentstudieshavebeenexplored,whichcanbe
categorizedintothreelinesbasedonthetypeofattribution.(1)Plan-then-Generate:Fierroetal.
[87]introducedtheblueprintmodelforattribution,whichconceptualizestextplansasaseries
ofquestionsthatserveasblueprintsforgenerationprocess,dictatingboththecontentandthe
sequenceoftheoutput.Comparedwithabstractivequestions,Huangetal.[119]enabledthemodel
to first ground to extractive evidence spans, which guides the subsequent generation process.
Leveragingeitherabstractquestionsorextractivespansasplanningfacilitatesabuilt-inattribution
mechanism, as they provide a natural link between retrieved information and the subsequent
generation.Similarly,Slobodkinetal.[278]brokedowntheconventionalend-to-endgeneration
processintothreeintuitivestages:contentselection,sentenceplanning,andsentencefusion.By
initiallyidentifyingrelevantsourcesegmentsandsubsequentlyconditioningthegenerationprocess
onthem,theselectedsegmentsnaturallyserveasattributions.(2)Generate-then-Reflect:Asaietal.
[11]proposedtrainingtheLLMtogeneratetextwithreflectiontokens.Thesereflectiontokens
empowertheLLMtodecidewhethertoretrieve,assesstherelevanceoftheretrieveddocument,
andcritiqueitsowngenerationtoensureattributability.Bycritiquingitsgeneration.Furthermore,
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

ASurveyonHallucinationinLargeLanguageModels 42:33
Yeetal.[344]introducedAGREE,designedtofacilitateself-groundinginLLMs.AGREEtrains
LLMstogeneratewell-groundedclaimswithcitationsandidentifyclaimsthatlackverification.
Aniterativeretrievalprocessisthenemployedtoactivelyseekadditionalinformationforthese
unsupportedstatements.(3)Self-Attribution:Inadditiontoleveragingexternalsupervisedsignals
forattribution,Qietal.[245]proposedaself-attributionmechanismthatutilizesmodel-internal
signals.Itoperatesbyfirstidentifyingcontext-sensitiveanswertokens,whicharethenpairedwith
retrieveddocumentsthatcontributedtothemodelgenerationviasaliencymethods.
Faithful Decoding. Despite significant optimizations in the RAG pipeline that facilitate the
incorporation of highly relevant content into the model’s context, current LLMs still cannot
guaranteefaithfulgeneration.TheunfaithfulutilizationofrelevantcontextbyLLMsundermines
thereliabilityoftheiroutputs,evenwhenthesourcesofinformationareverifiablyaccurate.Wu
etal.[327]analyzedthemodel’sknowledgepreferencewheninternalknowledgeconflictswith
contextualinformationandobservedthetug-of-warbetweentheLLM’sinternalpriorandexternal
evidence.Totacklethisissue,recentresearch[271,326]hasfocusedonfaithfuldecodingwithin
RAGsystems,aimingtoimprovethemodels’abilitytogeneratecontentthatfaithfullyalignswith
contextualinformation.Shietal.[271]presentedCAD,whichmodifiesthemodel’soriginaloutput
probabilitydistributionintothepointwisemutualinformationformulation.Thestrategyoperates
by amplifying the difference between the output probabilities when a model is used with and
withoutcontext,therebyenhancingthefaithfulnessofLLMstotheprovidedcontext.Lietal.[170]
adoptedasemi-parametriclanguagemodelingapproach[147]whichfacilitatestheintegration
ofcontextualspansofarbitrarylengthintoLMgenerations.Thegenerationisthenverifiedvia
speculativedecoding,furtherensuringmodelfaithfulness.Morerecently,Wuetal.[326]proposed
faithfulness-orienteddecoding,whichleveragesalightweightfaithfulnessdetectortomonitorthe
beam-searchprocess.Thedetectorleveragesfine-graineddecodingdynamicsincludingsequence
likelihood,uncertaintyquantification,contextinfluence,andsemanticalignmenttosynchronously
detectunfaithfulsentences.Whenanunfaithfulgenerationisdetected,ittriggersthebacktrack
operationandselectsthebeamwiththemorefaithfulscore,thusensuringgreaterfaithfulnessto
theretrievalsources.
7 FutureDiscussion
AsthefieldofresearchonhallucinationsinLLMscontinuestoevolve,ourfocusshiftstowards
the next horizon of inquiry. We explore prospective areas of study, notably the phenomenon
of hallucinations in vision-language models (Section 7.1) and the challenge of delineating and
understandingknowledgeboundarieswithinLLMs(Section7.2).
7.1 HallucinationinLVLMs
Enablingthevisualperceptionability,alongwithexceptionallanguageunderstandingandgen-
erationcapabilities,LVLMshaveexhibitedremarkablevision-languagecapabilities[47,122,183,
198,351,352,356,388].Unlikepreviouspre-trainedmulti-modalmodelsthatgainlimitedvision-
languageabilitiesfromlarge-scalevisual-languagepre-trainingdatasets[167,194,321,383],LVLMs
exploitadvancedLLMstounleashthepowerofinteractingwithhumansandtheenvironment.The
consequentdiverseapplicationsofLVLMsalsobringnewchallengestomaintainingthereliabilityof
suchsystems.RecentstudieshaverevealedthatcurrentLVLMsaresufferingfrommulti-modalhal-
lucinations,wheremodelsprovideresponsesmisalignedwiththecorrespondingvisualinformation
[103,184,293].Suchmulti-modalhallucinationscouldcauseunexpectedbehaviorswhenapplying
LVLMstoreal-worldscenarios,whichthereforehadtobefurtherinvestigatedandmitigated.
Lietal.[175]andLoveniaetal.[192]tookthefirststeptowardsevaluatingtheobjecthallucina-
tionsintheLVLMs.EvaluationsandexperimentsrevealthatcurrentLVLMsarepronetogenerate
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

42:34 L.Huangetal.
inconsistentresponseswithrespecttotheassociatedimage,includingnon-existentobjects,wrong
objecttypes,andattributes,incorrectsemanticrelationships,etc.[311,357].Furthermore,Liuetal.
[182],Zongetal.[391]andLiuetal.[181]showthatLVLMscanbeeasilyfooledandexperience
asevereperformancedropduetotheirover-relianceonthestronglanguageprior,aswellasits
inferiorabilitytodefendagainstinappropriateuserinputs[111,132].Jiangetal.[136],Wangetal.
[311]andJingetal.[139]tookastepforwardtoholisticallyevaluatemulti-modalhallucination.
What’smore,whenpresentedwithmultipleimages,LVLMssometimesmixormisspartsofthe
visualcontext,aswellasfailtounderstandtemporalorlogicalconnectionsbetweenthem,which
mighthindertheirusageinmanyscenarios,yetproperlyidentifyingthereasonforsuchdisorders
andtacklingthemstillrequirescontinuedefforts.Despitethewitnessedperceptionerrors,LVLMs
cangenerateflawedlogicalreasoningresultsevenwhencorrectlyrecognizingallvisualelements,
whichremainsfurtherinvestigation.
EffortshavebeenmadetowardsbuildingmorerobustLVLMs.Gunjaletal.[107],Luetal.[193],
Wangetal.[312],andLiuetal.[182]proposedtofurtherfinetunethemodelforproducingmore
truthfulandhelpfulresponses.Anotherlineofworkchoosestoposthocrectifythegenerated
inconsistentcontent,suchas[387],and[345],whichintroducedexpertmodels.Tofreefromthe
externaltools,Lengetal.[159],Huangetal.[121],andZhaoetal.[375]triedtofullyutilizethe
LVLMitselftoalleviatehallucinations.Thoughprovedtobeeffective,thosemethodsusuallyrequire
additionaldataannotations,visualexperts,trainingphases,andcomputationalcosts,whichprevent
LVLMsfromeffectivelyscalingandgeneralizingtovariousfields.Thus,moreuniversalapproaches
areexpectedtobuildamorereliablesystem,suchasfaithfulandlarge-scalevisual-textpre-training
andalignmentmethods.
7.2 UnderstandingKnowledgeBoundaryinLLMs
Despitetheimpressivecapacitytocapturefactualknowledgefromextensivedata,LLMsstillface
challengesinrecognizingtheirownknowledgeboundaries.Thisshortfallleadstotheoccurrence
ofhallucinations,whereLLMsconfidentlyproducefalsehoodswithoutanawarenessoftheirown
knowledgelimits[232,261,380].Numerousstudiesdelveintoprobingknowledgeboundariesof
LLMs,utilizingstrategiessuchasevaluatingtheprobabilityofacorrectresponseinamultiple-
choicesetting[141],orquantifyingthemodel’soutputuncertaintybyevaluatingthesimilarity
amongsetsofsentenceswithuncertainmeanings.
Furthermore,alineofwork[13,31,169,217]hasrevealedthatLLMscontainlatentstructures
withintheiractivationspacethatrelatetobeliefsabouttruthfulness.Recentresearch[277]also
foundsubstantialevidenceforLLMs’abilitytoencodetheunanswerabilityofquestions,despite
thefactthatthesemodelsexhibitoverconfidenceandproducehallucinationswhenpresentedwith
unanswerablequestions.Nonetheless,LevinsteinandHerrmann[160]haveemployedempirical
andconceptualtoolstoprobewhetherornotLLMshavebeliefs.Theirempiricalresultssuggestthat
currentlie-detectormethodsforLLMsarenotyetfullyreliable,andtheprobingmethodsproposed
by Burns et al. [31] and Azaria and Mitchell [13] do not adequately generalize. Consequently,
whetherwecaneffectivelyprobeLLMs’internalbeliefsisongoing,requiringfurtherresearch.
8 Conclusion
Inthiscomprehensivesurvey,wehaveundertakenanin-depthexaminationofhallucinationswithin
LLMs,delvingintotheintricaciesoftheirunderlyingcauses,pioneeringdetectionmethodologies
aswellasrelatedbenchmarks,andeffectivemitigationstrategies.Althoughsignificantstrideshave
beentaken,theconundrumofhallucinationinLLMsremainsacompellingandongoingconcern
thatdemandscontinuousinvestigation.Moreover,weenvisionthissurveyasaguidingbeacon
forresearchersdedicatedtoadvancingrobustIRsystemsandtrustworthyartificialintelligence.
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

ASurveyonHallucinationinLargeLanguageModels 42:35
By navigating the complex landscape of hallucinations, we hope to empower these dedicated
individualswithinvaluableinsightsthatdrivetheevolutionofAItechnologiestowardgreater
reliabilityandsafety[66,125,156,216,305].
References
[1] AmroAbbas,KushalTirumala,DánielSimig,SuryaGanguli,andAriS.Morcos.2023.SemDeDup:Data-efficient
learningatweb-scalethroughsemanticdeduplication.arXiv:2303.09540.Retrievedfromhttps://arxiv.org/abs/2303.
09540
[2] VaibhavAdlakha,ParishadBehnamGhader,XingHanLu,NicholasMeade,andSivaReddy.2023.Evaluating
correctnessandfaithfulnessofinstruction-followingmodelsforquestionanswering.arXiv:2307.16877.Retrieved
fromhttps://arxiv.org/abs/2307.16877
[3] AyushAgrawal,LesterMackey,andAdamTaumanKalai.2023.Dolanguagemodelsknowwhenthey’rehallucinating
references?arXiv:2305.18248.Retrievedfromhttps://arxiv.org/abs/2305.18248
[4] PerplexityAI.2023.PerplexityAI.https://www.perplexity.ai/
[5] RenatAksitov,Chung-ChingChang,DavidReitter,SiamakShakeri,andYun-HsuanSung.2023.Characterizing
attributionandfluencytradeoffsforretrieval-augmentedlargelanguagemodels.arXiv:2302.05578.Retrievedfrom
https://arxiv.org/abs/2302.05578
[6] BadrAlKhamissi,MillicentLi,AsliCelikyilmaz,MonaT.Diab,andMarjanGhazvininejad.2022.Areviewonlanguage
modelsasknowledgebases.arXiv:2204.06031.Retrievedfromhttps://arxiv.org/abs/2204.06031
[7] RohanAnil,SebastianBorgeaud,YonghuiWu,Jean-BaptisteAlayrac,JiahuiYu,RaduSoricut,JohanSchalkwyk,
AndrewM.Dai,AnjaHauth,KatieMillican,etal.2023.Gemini:Afamilyofhighlycapablemultimodalmodels.
arXiv:2312.11805.Retrievedfromhttps://arxiv.org/abs/2312.11805
[8] Anthropic.2023.Claude.Retrievedfromhttps://claude.ai/
[9] Antropic.2024.Claude3Haiku:OurFastestModelYet.2024.Retrievedfromhttps://www.anthropic.com/news/
claude-3-haiku
[10] ArXiv.2023.arxivdataset.Retrievedfromhttps://www.kaggle.com/datasets/Cornell-University/arxiv/versions/134
[11] AkariAsai,ZeqiuWu,YizhongWang,AvirupSil,andHannanehHajishirzi.2023.Self-RAG:Learningtoretrieve,
generate,andcritiquethroughself-reflection.arXiv:2310.11511.Retrievedfromhttps://arxiv.org/abs/2310.11511
[12] AkariAsai,ZexuanZhong,DanqiChen,PangWeiKoh,LukeZettlemoyer,HannanehHajishirzi,andWen-tau
Yih.2024.Reliable,adaptable,andattributablelanguagemodelswithretrieval.arXiv:2403.03187.Retrievedfrom
https://arxiv.org/abs/2403.03187
[13] AmosAzariaandTomM.Mitchell.2023.TheinternalstateofanLLMknowswhenitslying.arXiv:2304.13734.
Retrievedfromhttps://arxiv.org/abs/2304.13734
[14] JinheonBaek,AlhamFikriAji,andAmirSaffari.2023.Knowledge-augmentedlanguagemodelpromptingfor
zero-shotknowledgegraphquestionanswering.arXiv:2306.04136.Retrievedfromhttps://arxiv.org/abs/2306.04136
[15] YejinBang,SamuelCahyawijaya,NayeonLee,WenliangDai,DanSu,BryanWilie,HolyLovenia,ZiweiJi,Tiezheng
Yu,WillyChung,etal.2023.Amultitask,multilingual,multimodalevaluationofChatGPTonreasoning,hallucination,
andinteractivity.arXiv:2302.04023.Retrievedfromhttps://arxiv.org/abs/2302.04023
[16] ScottBarnett,StefanusKurniawan,SrikanthThudumu,ZachBrannelly,andMohamedAbdelrazek.2024.Seven
failurepointswhenengineeringaretrievalaugmentedgenerationsystem.arXiv:2401.05856.Retrievedfromhttps:
//arxiv.org/abs/2401.05856
[17] MarioBarrantes,BenediktHerudek,andRichardWang.2020.Adversarialnliforfactualcorrectnessintextsum-
marisationmodels.arXiv:2005.11739.Retrievedfromhttps://arxiv.org/abs/2005.11739
[18] PierreBasso.1993.Conditionalcausallogic:Aformaltheoryofthemeaninggeneratingprocessesinacognitive
system.InProceedingsofthe13thInternationalJointConferenceonArtificialIntelligence.RuzenaBajcsy(Ed.),Morgan
Kaufmann,845–851.Retrievedfromhttp://ijcai.org/Proceedings/93-2/Papers/002.pdf
[19] Iz Beltagy, Matthew E. Peters, and Arman Cohan. 2020. Longformer: The long-document transformer.
arXiv:2004.05150.Retrievedfromhttps://arxiv.org/abs/2004.05150
[20] EmilyM.Bender,TimnitGebru,AngelinaMcMillan-Major,andShmargaretShmitchell.2021.Onthedangersof
stochasticparrots:Canlanguagemodelsbetoobig?InProceedingsoftheACMConferenceonFairness,Accountability,
andTransparency(FAccT’21).MadeleineClareElish,WilliamIsaac,andRichardS.Zemel(Eds.),ACM,NewYork,
NY,610–623.DOI:https://doi.org/10.1145/3442188.3445922
[21] SamyBengio,OriolVinyals,NavdeepJaitly,andNoamShazeer.2015.Scheduledsamplingforsequenceprediction
withrecurrentneuralnetworks.InProceedingsofthe28thInternationalConferenceonNeuralInformationProcessing
Systems.CorinnaCortes,NeilD.Lawrence,DanielD.Lee,MasashiSugiyama,andRomanGarnett(Eds.),1171–1179.
Retrievedfromhttps://proceedings.neurips.cc/paper/2015/hash/e995f98d56967d946471af29d7bf99f1-Abstract.html
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

42:36 L.Huangetal.
[22] LukasBerglund,MegTong,MaxKaufmann,MikitaBalesni,AsaCooperStickland,TomaszKorbak,andOwain
Evans.2023.Thereversalcurse:LLMstrainedon“AisB”failtolearn“BisA”.arXiv:2309.12288.Retrievedfrom
https://arxiv.org/abs/2309.12288
[23] SidBlack,StellaBiderman,EricHallahan,QuentinAnthony,LeoGao,LaurenceGolding,HoraceHe,Connor
Leahy,KyleMcDonell,JasonPhang,etal.2022.GPT-NeoX-20B:Anopen-sourceautoregressivelanguagemodel.
arXiv:2204.06745.Retrievedfromhttps://arxiv.org/abs/2204.06745
[24] SebastianBorgeaud,ArthurMensch,JordanHoffmann,TrevorCai,ElizaRutherford,KatieMillican,Georgevanden
Driessche,Jean-BaptisteLespiau,BogdanDamoc,AidanClark,etal.2022.Improvinglanguagemodelsbyretrieving
fromtrillionsoftokens.InProceedingsoftheInternationalConferenceonMachineLearning(ICML’22).Kamalika
Chaudhuri,StefanieJegelka,LeSong,CsabaSzepesvári,GangNiu,andSivanSabato(Eds.),ProceedingsofMachine
LearningResearch,Vol.162,PMLR,2206–2240.Retrievedfromhttps://proceedings.mlr.press/v162/borgeaud22a.html
[25] SamuelR.Bowman,JeeyoonHyun,EthanPerez,EdwinChen,CraigPettit,ScottHeiner,KamileLukosuite,Amanda
Askell,AndyJones,AnnaChen,etal.2022.Measuringprogressonscalableoversightforlargelanguagemodels.
arXiv:2211.03540.Retrievedfromhttps://arxiv.org/abs/2211.03540
[26] RalphAllanBradleyandMiltonE.Terry.1952.Rankanalysisofincompleteblockdesigns:I.Themethodofpaired
comparisons.Biometrika39,3/4(1952),324–345.Retrievedfromhttps://www.jstor.org/stable/2334029
[27] RubenBranco,AntónioBranco,JoãoAntónioRodrigues,andJoãoRicardoSilva.2021.Shortcuttedcommonsense:
Dataspuriousnessindeeplearningofcommonsensereasoning.InProceedingsoftheConferenceonEmpiricalMethods
inNaturalLanguageProcessing.AssociationforComputationalLinguistics,1504–1521.DOI:https://doi.org/10.
18653/v1/2021.emnlp-main.113
[28] AndreiZ.Broder.1997.Ontheresemblanceandcontainmentofdocuments.InProceedingsoftheCompressionand
ComplexityofSEQUENCES1997(Cat.No.97TB100171). IEEE,21–29.
[29] TomB.Brown,BenjaminMann,NickRyder,MelanieSubbiah,JaredKaplan,PrafullaDhariwal,ArvindNeelakantan,
PranavShyam,GirishSastry,AmandaAskell,etal.2020.Languagemodelsarefew-shotlearners.InProceedingsofthe
34thInternationalConferenceonNeuralInformationProcessingSystems.HugoLarochelle,Marc’AurelioRanzato,Raia
Hadsell,Maria-FlorinaBalcan,andHsuan-TienLin(Eds.),1877–1901.Retrievedfromhttps://proceedings.neurips.cc/
paper/2020/hash/1457c0d6bfcb4967418bfb8ac142f64a-Abstract.html
[30] SébastienBubeck,VarunChandrasekaran,RonenEldan,JohannesGehrke,EricHorvitz,EceKamar,PeterLee,Yin
TatLee,YuanzhiLi,ScottM.Lundberg,etal.2023.Sparksofartificialgeneralintelligence:Earlyexperimentswith
GPT-4.arXiv:2303.12712.Retrievedfromhttps://arxiv.org/abs/2303.12712
[31] CollinBurns,HaotianYe,DanKlein,andJacobSteinhardt.2022.Discoveringlatentknowledgeinlanguagemodels
withoutsupervision.arXiv:2212.03827.Retrievedfromhttps://arxiv.org/abs/2212.03827
[32] ShulinCao,JiajieZhang,JiaxinShi,XinLv,ZijunYao,QiTian,LeiHou,andJuanziLi.2023.Probabilistictree-
of-thoughtreasoningforansweringknowledge-intensivecomplexquestions.InProceedingsoftheInternational
ConferenceonFindingsoftheAssociationforComputationalLinguistics.HoudaBouamor,JuanPino,andKalikaBali
(Eds.),AssociationforComputationalLinguistics,12541–12560.DOI:https://doi.org/10.18653/V1/2023.FINDINGS-
EMNLP.835
[33] YihanCao,SiyuLi,YixinLiu,ZhilingYan,YutongDai,PhilipS.Yu,andLichaoSun.2023.Acomprehensivesurvey
ofAI-generatedcontent(AIGC):AhistoryofgenerativeAIfromGANtoChatGPT.arXiv:2303.04226.Retrieved
fromhttps://arxiv.org/abs/2303.04226
[34] NicholasCarlini,DaphneIppolito,MatthewJagielski,KatherineLee,FlorianTramer,andChiyuanZhang.2022.
Quantifyingmemorizationacrossneurallanguagemodels.arXiv:2202.07646.Retrievedfromhttps://arxiv.org/abs/
2202.07646
[35] NicholasCarlini,FlorianTramer,EricWallace,MatthewJagielski,ArielHerbert-Voss,KatherineLee,AdamRoberts,
TomBrown,DawnSong,UlfarErlingsson,etal.2021.Extractingtrainingdatafromlargelanguagemodels.In
ProceedingsoftheInternationalConferenceon30thUSENIXSecuritySymposium(USENIXSecurity21).2633–2650.
[36] Chung-ChingChang,DavidReitter,RenatAksitov,andYun-HsuanSung.2023.KL-divergenceguidedtemperature
sampling.2306.01286.Retrievedfromhttps://arxiv.org/abs/2306.01286
[37] Haw-ShiuanChang,ZonghaiYao,AlolikaGon,HongYu,andAndrewMcCallum.2023.Revisitingthearchitectures
likepointernetworkstoefficientlyimprovethenextworddistribution,summarizationfactuality,andbeyond.In
ProceedingsoftheInternationalConferenceonFindingsoftheAssociationforComputationalLinguistics.AnnaRogers,
JordanL.Boyd-Graber,andNaoakiOkazaki(Eds.),AssociationforComputationalLinguistics,12707–12730.DOI:
https://doi.org/10.18653/V1/2023.FINDINGS-ACL.805
[38] Haw-ShiuanChangandAndrewMcCallum.2022.Softmaxbottleneckmakeslanguagemodelsunabletorepresent
multi-modeworddistributions.InProceedingsofthe60thAnnualMeetingoftheAssociationforComputational
Linguistics(Volume1:LongPapers).AssociationforComputationalLinguistics,8048–8073.DOI:https://doi.org/10.
18653/v1/2022.acl-long.554
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

ASurveyonHallucinationinLargeLanguageModels 42:37
[39] CanyuChenandKaiShu.2023.CombatingmisinformationintheageofLLMs:Opportunitiesandchallenges.
arXiv:2311.05656.Retrievedfromhttps://arxiv.org/abs/2311.05656
[40] Hung-TingChen,MichaelJ.Q.Zhang,andEunsolChoi.2022.Richknowledgesourcesbringcomplexknowledge
conflicts:Recalibratingmodelstoreflectconflictingevidence.InProceedingsoftheConferenceonEmpiricalMethods
inNaturalLanguageProcessing(EMNLP’22).YoavGoldberg,ZornitsaKozareva,andYueZhang(Eds.),Association
forComputationalLinguistics,2292–2307.DOI:https://doi.org/10.18653/V1/2022.EMNLP-MAIN.146
[41] Hung-TingChen,FangyuanXu,ShaneA.Arora,andEunsolChoi.2023.Understandingretrievalaugmentationfor
long-formquestionanswering.arXiv:2310.12150.Retrievedfromhttps://arxiv.org/abs/2310.12150
[42] ShiqiChen,YiranZhao,JinghanZhang,I-ChunChern,SiyangGao,PengfeiLiu,andJunxianHe.2023.FELM:
Benchmarkingfactualityevaluationoflargelanguagemodels.arXiv:2310.00741.Retrievedfromhttps://arxiv.org/
abs/2310.00741
[43] TongChen,HongweiWang,SihaoChen,WenhaoYu,KaixinMa,XinranZhao,HongmingZhang,andDong
Yu.2023.DenseXretrieval:Whatretrievalgranularityshouldweuse?/arXiv:2312.06648.Retrievedfromhttps:
//arxiv.org/abs/2312.06648
[44] XiaoyangChen,BenHe,HongyuLin,XianpeiHan,TianshuWang,BoxiCao,LeSun,andYingfeiSun.2024.Spiral
ofsilence:Howislargelanguagemodelkillinginformationretrieval?–Acasestudyonopendomainquestion
answering.arXiv:2404.10496.Retrievedfromhttps://arxiv.org/abs/2404.10496
[45] XiuyingChen,MingzheLi,XinGao,andXiangliangZhang.2022.Towardsimprovingfaithfulnessinabstractive
summarization.InProceedingsofthe36thInternationalConferenceonNeuralInformationProcessingSystems(NeurIPS).
Retrievedfromhttp://papers.nips.cc/paper_files/paper/2022/hash/9b6d7202750e8e32cd5270eb7fc131f7-Abstract-
Conference.html
[46] YijieChen,YijinLiu,FandongMeng,YufengChen,JinanXu,andJieZhou.2023.Improvingtranslationfaithfulnessof
largelanguagemodelsviaaugmentinginstructions.arXiv:2308.12674.Retrievedfromhttps://arxiv.org/abs/2308.12674
[47] YangyiChen,KaranSikka,MichaelCogswell,HengJi,andAjayDivakaran.2023.Measuringandimprovingchain-
of-thoughtreasoninginvision-languagemodels.arXiv:2309.04461.Retrievedfromhttps://arxiv.org/abs/2309.04461
[48] QinyuanCheng,XiaonanLi,ShiminLi,QinZhu,ZhangyueYin,YunfanShao,LinyangLi,TianxiangSun,HangYan,
andXipengQiu.2024.Unifiedactiveretrievalforretrievalaugmentedgeneration.arXiv:2406.12534.Retrievedfrom
https://arxiv.org/abs/2406.12534
[49] QinyuanCheng,TianxiangSun,WenweiZhang,SiyinWang,XiangyangLiu,MozhiZhang,JunliangHe,Mi-
anqiuHuang,ZhangyueYin,KaiChen,etal.2023.Evaluatinghallucinationsinchineselargelanguagemodels.
arXiv:2310.03368.Retrievedfromhttps://arxiv.org/abs/2310.03368
[50] IChern,SteffiChern,ShiqiChen,WeizheYuan,KehuaFeng,ChuntingZhou,JunxianHe,GrahamNeubig,Pengfei
Liu,etal.2023.FacTool:FactualitydetectioningenerativeAI–Atoolaugmentedframeworkformulti-taskand
multi-domainscenarios.arXiv:2307.13528.Retrievedfromhttps://arxiv.org/abs/2307.13528
[51] Cheng-HanChiangandHung-yiLee.2023.Canlargelanguagemodelsbeanalternativetohumanevaluations?
arXiv:2305.01937.Retrievedfromhttps://arxiv.org/abs/2305.01937
[52] DavidChiangandPeterCholak.2022.Overcomingatheoreticallimitationofself-attention.InProceedingsof
the60thAnnualMeetingoftheAssociationforComputationalLinguistics(Volume1:LongPapers).Associationfor
ComputationalLinguistics,7654–7664.DOI:https://doi.org/10.18653/v1/2022.acl-long.527
[53] SehyunChoi,TianqingFang,ZhaoweiWang,andYangqiuSong.2023.KCTS:Knowledge-constrainedtreesearch
decodingwithtoken-levelhallucinationdetection.arXiv:2310.09044.Retrievedfromhttps://arxiv.org/abs/2310.09044
[54] AakankshaChowdhery,SharanNarang,JacobDevlin,MaartenBosma,GauravMishra,AdamRoberts,PaulBarham,
HyungWonChung,CharlesSutton,SebastianGehrmann,etal.2023.PaLM:Scalinglanguagemodelingwith
pathways.JournalofMachineLearningResearch24(2023),240:1–240:113.Retrievedfromhttp://jmlr.org/papers/v24/
22-1144.html
[55] PaulF.Christiano,JanLeike,TomB.Brown,MiljanMartic,ShaneLegg,andDarioAmodei.2017.Deepreinforce-
mentlearningfromhumanpreferences.InProceedingsofthe31stInternationalConferenceonNeuralInformation
ProcessingSystems.IsabelleGuyon,UlrikevonLuxburg,SamyBengio,HannaM.Wallach,RobFergus,S.V.N.
Vishwanathan,andRomanGarnett(Eds.),4299–4307.Retrievedfromhttps://proceedings.neurips.cc/paper/2017/
hash/d5e2c0adad503c91f91df240d0cd4e49-Abstract.html
[56] ZhengChu,JingchangChen,QianglongChen,HaotianWang,KunZhu,XiyuanDu,WeijiangYu,MingLiu,andBing
Qin.2024.BeamAggR:Beamaggregationreasoningovermulti-sourceknowledgeformulti-hopquestionanswering.
arXiv:2406.19820.Retrievedfromhttps://arxiv.org/abs/2406.19820
[57] ZhengChu,JingchangChen,QianglongChen,WeijiangYu,TaoHe,HaotianWang,WeihuaPeng,MingLiu,Bing
Qin,andTingLiu.2023.Asurveyofchainofthoughtreasoning:advances,frontiersandfuture.arXiv:2309.15402.
Retrievedfromhttps://arxiv.org/abs/2309.15402
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

42:38 L.Huangetal.
[58] Yung-SungChuang,YujiaXie,HongyinLuo,YoonKim,JamesGlass,andPengchengHe.2023.Dola:Decodingby
contrastinglayersimprovesfactualityinlargelanguagemodels.arXiv:2309.03883.Retrievedfromhttps://arxiv.org/
abs/2309.03883
[59] HyungWonChung,LeHou,ShayneLongpre,BarretZoph,YiTay,WilliamFedus,EricLi,XuezhiWang,Mostafa
Dehghani,SiddharthaBrahma,etal.2022.Scalinginstruction-finetunedlanguagemodels.arXiv:2210.11416.Retrieved
fromhttps://arxiv.org/abs/2210.11416
[60] KarlCobbe,VineetKosaraju,MohammadBavarian,MarkChen,HeewooJun,LukaszKaiser,MatthiasPlappert,
JerryTworek,JacobHilton,ReiichiroNakano,ChristopherHesse,andJohnSchulman.2021.Trainingverifiersto
solvemathwordproblems.arXiv:2110.14168.Retrievedfromhttps://arxiv.org/abs/2110.14168
[61] RoiCohen,MayHamri,MorGeva,andAmirGloberson.2023.LMvsLM:Detectingfactualerrorsviacross
examination.arXiv:2305.13281.Retrievedfromhttps://arxiv.org/abs/2305.13281
[62] TogetherComputer.2023.RedPajama:AnOpenDatasetforTrainingLargeLanguageModels.Retrievedfrom
https://github.com/togethercomputer/RedPajama-Data
[63] AjeyaCotra.2021.WhyAIAlignmentCouldBeHardwithModernDeepLearning.ColdTakes.Retrievedfrom
https://www.cold-takes.com/why-ai-alignment-could-be-hard-with-modern-deep-learning/
[64] FlorinCuconasu,GiovanniTrappolini,FedericoSiciliano,SimoneFilice,CesareCampagnano,YoelleMaarek,Nicola
Tonellotto,andFabrizioSilvestri.2024.Thepowerofnoise:RedefiningretrievalforRAGsystems.arXiv:2401.14887.
Retrievedfromhttps://arxiv.org/abs/2401.14887
[65] DamaiDai,LiDong,YaruHao,ZhifangSui,BaobaoChang,andFuruWei.2022.Knowledgeneuronsinpretrained
transformers.InProceedingsofthe60thAnnualMeetingoftheAssociationforComputationalLinguistics(Volume1:Long
Papers).AssociationforComputationalLinguistics,8493–8502.DOI:https://doi.org/10.18653/v1/2022.acl-long.581
[66] DamaiDai,WenbinJiang,QingxiuDong,YajuanLyu,QiaoqiaoShe,andZhifangSui.2022.Neuralknowledgebank
forpretrainedtransformers.arXiv:2208.00399.Retrievedfromhttps://arxiv.org/abs/2208.00399
[67] SunhaoDai,YuqiZhou,LiangPang,WeihaoLiu,XiaolinHu,YongLiu,XiaoZhang,andJunXu.2023.LLMsmay
dominateinformationaccess:NeuralretrieversarebiasedtowardsLLM-Generatedtexts.arXiv:2310.20501.Retrieved
fromhttps://arxiv.org/abs/2310.20501
[68] SumanthDathathri,AndreaMadotto,JaniceLan,JaneHung,EricFrank,PieroMolino,JasonYosinski,andRosanne
Liu.2020.Plugandplaylanguagemodels:Asimpleapproachtocontrolledtextgeneration.InProceedingsof
the8thInternationalConferenceonLearningRepresentations(ICLR’20).OpenReview.net.Retrievedfromhttps:
//openreview.net/forum?id=H1edEyBKDS
[69] NicolaDeCao,WilkerAziz,andIvanTitov.2021.Editingfactualknowledgeinlanguagemodels.InProceedingsof
theConferenceonEmpiricalMethodsinNaturalLanguageProcessing.AssociationforComputationalLinguistics,
6491–6506.DOI:https://doi.org/10.18653/v1/2021.emnlp-main.522
[70] MariaAngelsdeLuisBalaguer,VinamraBenara,RenatoLuizdeFreitasCunha,RobertodeM.EstevãoFilho,
ToddHendry,DanielHolstein,JenniferMarsman,NickMecklenburg,SaraMalvar,LeonardoO.Nunes,etal.
2024.RAGvsFine-tuning:Pipelines,tradeoffs,andacasestudyonagriculture.arXiv:2401.08406.Retrievedfrom
https://arxiv.org/abs/2401.08406
[71] GrégoireDelétang,AnianRuoss,Paul-AmbroiseDuquenne,ElliotCatt,TimGenewein,ChristopherMattern,Jordi
Grau-Moya,LiKevinWenliang,MatthewAitchison,LaurentOrseau,etal.2023.Languagemodelingiscompression.
arXiv:2309.10668.Retrievedfromhttps://arxiv.org/abs/2309.10668
[72] JacobDevlin,Ming-WeiChang,KentonLee,andKristinaToutanova.2019.BERT:Pre-trainingofdeepbidirectional
transformersforlanguageunderstanding.InProceedingsoftheConferenceoftheNorthAmericanChapterofthe
AssociationforComputationalLinguistics:HumanLanguageTechnologies(NAACL-HLT’19).JillBurstein,Christy
Doran,andThamarSolorio(Eds.),AssociationforComputationalLinguistics,4171–4186.DOI:https://doi.org/10.
18653/V1/N19-1423
[73] ShehzaadDhuliawala,MojtabaKomeili,JingXu,RobertaRaileanu,XianLi,AsliCelikyilmaz,andJasonWeston.
2023.Chain-of-verificationreduceshallucinationinlargelanguagemodels.ArXivpreprintabs/2309.11495(2023).
Retrievedfromhttps://arxiv.org/abs/2309.11495
[74] HanxingDing,LiangPang,ZihaoWei,HuaweiShen,andXueqiCheng.2024.RetrieveOnlyWhenItNeeds:Adaptive
RetrievalAugmentationforHallucinationMitigationinLargeLanguageModels.arXiv:2402.10612.Retrievedfrom
https://arxiv.org/abs/2402.10612
[75] ZicanDong,TianyiTang,JunyiLi,WayneXinZhao,andJi-RongWen.2023.BAMBOO:Acomprehensivebenchmark
forevaluatinglongtextmodelingcapacitiesoflargelanguagemodels.arXiv:2309.13345.Retrievedfromhttps:
//arxiv.org/abs/2309.13345
[76] EsinDurmus,HeHe,andMonaDiab.2020.FEQA:Aquestionansweringevaluationframeworkforfaithfulnessas-
sessmentinabstractivesummarization.InProceedingsofthe58thAnnualMeetingoftheAssociationforComputational
Linguistics.AssociationforComputationalLinguistics,5055–5070.DOI:https://doi.org/10.18653/v1/2020.acl-main.454
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

ASurveyonHallucinationinLargeLanguageModels 42:39
[77] NouhaDziri,AndreaMadotto,OsmarZaïane,andAvishekJoeyBose.2021.Neuralpathhunter:Reducinghallucina-
tionindialoguesystemsviapathgrounding.InProceedingsoftheConferenceonEmpiricalMethodsinNaturalLanguage
Processing.AssociationforComputationalLinguistics,2197–2214.DOI:https://doi.org/10.18653/v1/2021.emnlp-
main.168
[78] NouhaDziri,HannahRashkin,TalLinzen,andDavidReitter.2021.Evaluatinggroundednessindialoguesystems:
Thebeginbenchmark.arXiv:2105.00071.Retrievedfromhttps://arxiv.org/abs/2105.00071
[79] AlexanderFabbri,Chien-ShengWu,WenhaoLiu,andCaimingXiong.2022.QAFactEval:ImprovedQA-basedfactual
consistencyevaluationforsummarization.InProceedingsoftheConferenceoftheNorthAmericanChapterofthe
AssociationforComputationalLinguistics:HumanLanguageTechnologies.AssociationforComputationalLinguistics,
2587–2601.DOI:https://doi.org/10.18653/v1/2022.naacl-main.187
[80] AlexanderR.Fabbri,WojciechKryŚciński,BryanMcCann,CaimingXiong,RichardSocher,andDragomirRadev.2021.
SummEval:Re-evaluatingsummarizationevaluation.TransactionsoftheAssociationforComputationalLinguistics9
(2021),391–409.DOI:https://doi.org/10.1162/tacl_a_00373
[81] TobiasFalke,LeonardoF.R.Ribeiro,PrasetyaAjieUtama,IdoDagan,andIrynaGurevych.2019.Rankinggenerated
summariesbycorrectness:Aninterestingbutchallengingapplicationfornaturallanguageinference.InProceedings
ofthe57thAnnualMeetingoftheAssociationforComputationalLinguistics.AssociationforComputationalLinguistics,
2214–2220.DOI:https://doi.org/10.18653/v1/P19-1213
[82] AngelaFan,YacineJernite,EthanPerez,DavidGrangier,JasonWeston,andMichaelAuli.2019.ELI5:Longform
questionanswering.InProceedingsofthe57thAnnualMeetingoftheAssociationforComputationalLinguistics.
AssociationforComputationalLinguistics,3558–3567.DOI:https://doi.org/10.18653/v1/P19-1346
[83] AngelaFan,MikeLewis,andYannDauphin.2018.Hierarchicalneuralstorygeneration.InProceedingsofthe
56thAnnualMeetingoftheAssociationforComputationalLinguistics(Volume1:LongPapers).Associationfor
ComputationalLinguistics,889–898.DOI:https://doi.org/10.18653/v1/P18-1082
[84] HuawenFeng,YanFan,XiongLiu,Ting-EnLin,ZekunYao,YuchuanWu,FeiHuang,YongbinLi,andQianliMa.2023.
Improvingfactualconsistencyoftextsummarizationbyadversariallydecouplingcomprehensionandembellishment
abilitiesofLLMs.arXiv:2310.19347.Retrievedfromhttps://arxiv.org/abs/2310.19347
[85] ShangbinFeng,WeijiaShi,YuyangBai,VidhishaBalachandran,TianxingHe,andYuliaTsvetkov.2023.Cook:
Empoweringgeneral-purposelanguagemodelswithmodularandcollaborativeknowledge.arXiv:2305.09955.
Retrievedfromhttps://arxiv.org/abs/2305.09955
[86] ZhangyinFeng,XiaochengFeng,DezhiZhao,MaojinYang,andBingQin.2023.Retrieval-generationsynergy
augmentedlargelanguagemodels.arXiv:2310.05149.Retrievedfromhttps://arxiv.org/abs/2310.05149
[87] ConstanzaFierro,ReinaldKimAmplayo,FantineHuot,NicolaDeCao,JoshuaMaynez,ShashiNarayan,and
MirellaLapata.2024.Learningtoplanandgeneratetextwithcitations.arXiv:2404.03381.Retrievedfromhttps:
//arxiv.org/abs/2404.03381
[88] KatjaFilippova.2020.Controlledhallucinations:Learningtogeneratefaithfullyfromnoisydata.InProceedingsof
theInternationalConferenceonFindingsoftheAssociationforComputationalLinguistics:EMNLP2020.Association
forComputationalLinguistics,864–870.DOI:https://doi.org/10.18653/v1/2020.findings-emnlp.76
[89] RobertFrielandAtindriyoSanyal.2023.Chainpoll:AhighefficacymethodforLLMhallucinationdetection.
arXiv:2310.18344.Retrievedfromhttps://arxiv.org/abs/2310.18344
[90] JinlanFu,See-KiongNg,ZhengbaoJiang,andPengfeiLiu.2023.GPTScore:Evaluateasyoudesire.arXiv:2302.04166.
Retrievedfromhttps://arxiv.org/abs/2302.04166
[91] YarinGalandZoubinGhahramani.2016.DropoutasaBayesianapproximation:Representingmodeluncertaintyin
deeplearning.InProceedingsofthe33ndInternationalConferenceonMachineLearning(ICML’16).Maria-Florina
BalcanandKilianQ.Weinberger(Eds.),JMLRWorkshopandConferenceProceedings,Vol.48,JMLR.org,1050–1059.
Retrievedfromhttp://proceedings.mlr.press/v48/gal16.html
[92] LeoGao,StellaBiderman,SidBlack,LaurenceGolding,TravisHoppe,CharlesFoster,JasonPhang,HoraceHe,Anish
Thite,NoaNabeshima,etal.2021.Thepile:An800gbdatasetofdiversetextforlanguagemodeling.arXiv:2101.00027.
Retrievedfromhttps://arxiv.org/abs/2101.00027
[93] LuyuGao,ZhuyunDai,PanupongPasupat,AnthonyChen,ArunTejasviChaganty,YichengFan,VincentY.Zhao,
NiLao,HongraeLee,Da-ChengJuan,andKelvinGuu.2023.RARR:Researchingandrevisingwhatlanguagemodels
say,usinglanguagemodels.InProceedingsofthe61stAnnualMeetingoftheAssociationforComputationalLinguistics
(Volume1:LongPapers)(ACL’23).AnnaRogers,JordanL.Boyd-Graber,andNaoakiOkazaki(Eds.),Associationfor
ComputationalLinguistics,16477–16508.Retrievedfromhttps://aclanthology.org/2023.acl-long.910
[94] MingqiGao,JieRuan,RenliangSun,XunjianYin,ShipingYang,andXiaojunWan.2023.Human-likesummarization
evaluationwithchatgpt.arXiv:2304.02554.Retrievedfromhttps://arxiv.org/abs/2304.02554
[95] TianyuGao,XingchengYao,andDanqiChen.2021.SimCSE:Simplecontrastivelearningofsentenceembeddings.
arXiv:2104.08821.Retrievedfromhttps://arxiv.org/abs/2104.08821
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

42:40 L.Huangetal.
[96] YunfanGao,TaoSheng,YoulinXiang,YunXiong,HaofenWang,andJiaweiZhang.2023.Chat-REC:Towards
interactiveandexplainableLLMs-augmentedrecommendersystem.arXiv:2303.14524.Retrievedfromhttps://arxiv.
org/abs/2303.14524
[97] ZorikGekhman,GalYona,RoeeAharoni,MatanEyal,AmirFeder,RoiReichart,andJonathanHerzig.2024.Doesfine-
tuningLLMsonnewknowledgeencouragehallucinations?arXiv:2405.05904.Retrievedfromhttps://arxiv.org/abs/
[98] BenGoodrich,VinayRao,PeterJ.Liu,andMohammadSaleh.2019.Assessingthefactualaccuracyofgeneratedtext.
InProceedingsofthe25thACMSIGKDDInternationalConferenceonKnowledgeDiscovery&DataMining(KDD’19).
AnkurTeredesai,VipinKumar,YingLi,RómerRosales,EvimariaTerzi,andGeorgeKarypis(Eds.),ACM,NewYork,
NY,166–175.DOI:https://doi.org/10.1145/3292500.3330955
[99] Google.2023.Bard.Retrievedfromhttps://bard.google.com/
[100] TanyaGoyalandGregDurrett.2020.Evaluatingfactualityingenerationwithdependency-levelentailment.In
ProceedingsoftheInternationalConferenceonFindingsoftheAssociationforComputationalLinguistics:EMNLP2020.
AssociationforComputationalLinguistics,3592–3603.DOI:https://doi.org/10.18653/v1/2020.findings-emnlp.322
[101] TanyaGoyalandGregDurrett.2021.Annotatingandmodelingfine-grainedfactualityinsummarization.InProceed-
ingsoftheConferenceoftheNorthAmericanChapteroftheAssociationforComputationalLinguistics:HumanLanguage
Technologies.AssociationforComputationalLinguistics,1449–1462.DOI:https://doi.org/10.18653/v1/2021.naacl-
main.114
[102] YuxuanGu,XiaochengFeng,SichengMa,JiamingWu,HengGong,andBingQin.2022.Improvingcontrollabletext
generationwithposition-awareweighteddecoding.InProceedingsoftheInternationalConferenceonFindingsofthe
AssociationforComputationalLinguistics(ACL’22).AssociationforComputationalLinguistics,3449–3467.DOI:
https://doi.org/10.18653/v1/2022.findings-acl.272
[103] TianruiGuan,FuxiaoLiu,XiyangWu,RuiqiXian,ZongxiaLi,XiaoyuLiu,XijunWang,LichangChen,Furong
Huang,YaserYacoob,etal.2023.Hallusionbench:Anadvanceddiagnosticsuiteforentangledlanguagehallucination
&visualillusioninlargevision-languagemodels.arXiv:2310.14566.Retrievedfromhttps://arxiv.org/abs/2310.14566
[104] NunoMiguelGuerreiro,DuarteM.Alves,JonasWaldendorf,BarryHaddow,AlexandraBirch,PierreColombo,and
AndréF.T.Martins.2023.Hallucinationsinlargemultilingualtranslationmodels.arXiv:2303.16104.Retrievedfrom
https://arxiv.org/abs/2303.16104
[105] NunoM.Guerreiro,ElenaVoita,andAndréMartins.2023.Lookingforaneedleinahaystack:Acomprehensive
studyofhallucinationsinneuralmachinetranslation.InProceedingsofthe17thConferenceoftheEuropeanChapter
oftheAssociationforComputationalLinguistics.AssociationforComputationalLinguistics,1059–1075.Retrieved
fromhttps://aclanthology.org/2023.eacl-main.75
[106] SuriyaGunasekar,YiZhang,JyotiAneja,CaioCésarTeodoroMendes,AllieDelGiorno,SivakanthGopi,Mojan
Javaheripi,PieroKauffmann,GustavodeRosa,OlliSaarikivi,etal.2023.Textbooksareallyouneed.arXiv:2306.11644.
Retrievedfromhttps://arxiv.org/abs/2306.11644
[107] AnishaGunjal,JihanYin,andErhanBas.2023.Detectingandpreventinghallucinationsinlargevisionlanguage
models.arXiv:2308.06394.Retrievedfromhttps://arxiv.org/abs/2308.06394
[108] KelvinGuu,KentonLee,ZoraTung,PanupongPasupat,andMing-WeiChang.2020.Retrievalaugmentedlanguage
modelpre-training.InProceedingsofthe37thInternationalConferenceonMachineLearning(ICML’20),Proceedingsof
MachineLearningResearch,Vol.119,PMLR,3929–3938.Retrievedfromhttp://proceedings.mlr.press/v119/guu20a.
html
[109] BikashGyawali,LucasAnastasiou,andPetrKnoth.2020.Deduplicationofscholarlydocumentsusinglocality
sensitivehashingandwordembeddings.InProceedingsofthe12thLanguageResourcesandEvaluationConference.
EuropeanLanguageResourcesAssociation,901–910.Retrievedfromhttps://aclanthology.org/2020.lrec-1.113
[110] MichaelHahn.2020.Theoreticallimitationsofself-attentioninneuralsequencemodels.TransactionsoftheAssociation
forComputationalLinguistics8(2020),156–171.DOI:https://doi.org/10.1162/tacl_a_00306
[111] Tianyang Han, Qing Lian, Rui Pan, Renjie Pi, Jipeng Zhang, Shizhe Diao, Yong Lin, and Tong Zhang.
2024.Theinstinctivebias:SpuriousimagesleadtohallucinationinMLLMs.arXiv:2402.03757.Retrievedfrom
https://arxiv.org/abs/2402.03757
[112] HangfengHe,HongmingZhang,andDanRoth.2023.Rethinkingwithretrieval:Faithfullargelanguagemodel
inference.arXiv:2301.00303.Retrievedfromhttps://arxiv.org/abs/2301.00303
[113] JunqingHe,KunhaoPan,XiaoqunDong,ZhuoyangSong,YiboLiu,YuxinLiang,HaoWang,QianguoSun,Songxin
Zhang,ZejianXie,andJiaxingZhang.2023.Neverlostinthemiddle:Improvinglargelanguagemodelsviaattention
strengtheningquestionanswering.arXiv:2311.09198.Retrievedfromhttps://arxiv.org/abs/2311.09198
[114] PeterHenderson,MarkS.Krass,LuciaZheng,NeelGuha,ChristopherD.Manning,DanJurafsky,andDanielE.
Ho.2022.Pileoflaw:Learningresponsibledatafilteringfromthelawanda256GBopen-sourcelegaldataset.In
Proceedingsofthe36thInternationalConferenceonNeuralInformationProcessingSystems.SanmiKoyejo,S.Mohamed,
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

ASurveyonHallucinationinLargeLanguageModels 42:41
A.Agarwal,DanielleBelgrave,K.Cho,andA.Oh(Eds.).Retrievedfromhttp://papers.nips.cc/paper_files/paper/
2022/hash/bc218a0c656e49d4b086975a9c785f47-Abstract-Datasets_and_Benchmarks.html
[115] DanHendrycks,CollinBurns,StevenBasart,AndyZou,MantasMazeika,DawnSong,andJacobSteinhardt.2021.
Measuringmassivemultitasklanguageunderstanding.InProceedingsofthe 9thInternationalConferenceonLearning
Representations(ICLR’21).OpenReview.net.Retrievedfromhttps://openreview.net/forum?id=d7KBjmI3GmQ
[116] EvanHernandez,BelindaZ.Li,andJacobAndreas.2023.Inspectingandeditingknowledgerepresentationsin
languagemodels.arXiv:2304.00740.Retrievedfromhttps://arxiv.org/abs/2304.00740
[117] AriHoltzman,JanBuys,LiDu,MaxwellForbes,andYejinChoi.2020.Thecuriouscaseofneuraltextdegeneration.
InProceedingsofthe8thInternationalConferenceonLearningRepresentations(ICLR’20).OpenReview.net.Retrieved
fromhttps://openreview.net/forum?id=rygGQyrFvH
[118] OrHonovich,LeshemChoshen,RoeeAharoni,EllaNeeman,IdanSzpektor,andOmriAbend.2021.𝑄2:Evaluating
factualconsistencyinknowledge-groundeddialoguesviaquestiongenerationandquestionanswering.InProceedings
oftheConferenceonEmpiricalMethodsinNaturalLanguageProcessing.AssociationforComputationalLinguistics,
7856–7870.DOI:https://doi.org/10.18653/v1/2021.emnlp-main.619
[119] LeiHuang,XiaochengFeng,WeitaoMa,YuxuanGu,WeihongZhong,XiachongFeng,WeijiangYu,WeihuaPeng,
DuyuTang,DandanTu,etal.2024.Learningfine-grainedgroundedcitationsforattributedlargelanguagemodels.
InProceedingsoftheInternationalConferenceonFindingsoftheAssociationforComputationalLinguistics(ACL’24).
Lun-WeiKu,AndreMartins,andVivekSrikumar(Eds.),AssociationforComputationalLinguistics,14095–14113.
DOI:https://doi.org/10.18653/V1/2024.FINDINGS-ACL.838
[120] LeiHuang,XiaochengFeng,WeitaoMa,LiangZhao,YuchunFan,WeihongZhong,DongliangXu,QingYang,Hongtao
Liu,andBingQin.2024.Advancinglargelanguagemodelattributionthroughself-improving.arXiv:2410.13298.
Retrievedfromhttps://arxiv.org/abs/2410.13298
[121] QidongHuang,XiaoyiDong,PanZhang,BinWang,ConghuiHe,JiaqiWang,DahuaLin,WeimingZhang,and
NenghaiYu.2023.Opera:Alleviatinghallucinationinmulti-modallargelanguagemodelsviaover-trustpenaltyand
retrospection-allocation.arXiv:2311.17911.Retrievedfromhttps://arxiv.org/abs/2311.17911
[122] ShaohanHuang,LiDong,WenhuiWang,YaruHao,SakshamSinghal,ShumingMa,TengchaoLv,LeiCui,Owais
KhanMohammed,QiangLiu,etal.2023.Languageisnotallyouneed:Aligningperceptionwithlanguagemodels.
arXiv:2302.14045.Retrievedfromhttps://arxiv.org/abs/2302.14045
[123] YuzhenHuang,YuzhuoBai,ZhihaoZhu,JunleiZhang,JinghanZhang,TangjunSu,JuntengLiu,ChuanchengLv,
YikaiZhang,JiayiLei,etal.2023a.C-eval:Amulti-levelmulti-disciplinechineseevaluationsuiteforfoundation
models.arXiv:2305.08322.Retrievedfromhttps://arxiv.org/abs/2305.08322
[124] Yi-ChongHuang,Xia-ChongFeng,Xiao-ChengFeng,andBingQin.2021.Thefactualinconsistencyproblemin
abstractivetextsummarization:Asurvey.arXiv:2104.14839.Retrievedfromhttps://arxiv.org/abs/2104.14839
[125] ZeyuHuang,YikangShen,XiaofengZhang,JieZhou,WengeRong,andZhangXiong.2023d.Transformer-Patcher:
Onemistakeworthoneneuron.InProceedingsofthe11thInternationalConferenceonLearningRepresentations
(ICLR’23).OpenReview.net.Retrievedfromhttps://openreview.net/pdf?id=4oYUGeGBPm
[126] SiqingHuo,NegarArabzadeh,andCharlesL.A.Clarke.2023.RetrievingsupportingevidenceforLLMsgenerated
answers.arXiv:2306.13781.Retrievedfromhttps://arxiv.org/abs/2306.13781
[127] SrinivasanIyer,XiVictoriaLin,RamakanthPasunuru,TodorMihaylov,DanielSimig,PingYu,KurtShuster,Tianlu
Wang,QingLiu,PunitSinghKoura,etal.2022.Opt-iml:Scalinglanguagemodelinstructionmetalearningthrough
thelensofgeneralization.arXiv:2212.12017.Retrievedfromhttps://arxiv.org/abs/2212.12017
[128] GautierIzacard,MathildeCaron,LucasHosseini,SebastianRiedel,PiotrBojanowski,ArmandJoulin,andEdouard
Grave.2022.Unsuperviseddenseinformationretrievalwithcontrastivelearning.TransactionsonMachineLearning
Research2022(2022).Retrievedfromhttps://openreview.net/forum?id=jKN1pXi7b0
[129] GautierIzacard,PatrickS.H.Lewis,MariaLomeli,LucasHosseini,FabioPetroni,TimoSchick,JaneDwivedi-Yu,
ArmandJoulin,SebastianRiedel,andEdouardGrave.2023.Atlas:Few-shotlearningwithretrievalaugmented
languagemodels.JournalofMachineLearningResearch24(2023),251:1–251:43.Retrievedfromhttp://jmlr.org/
papers/v24/23-0037.html
[130] RolfJagerman,HongleiZhuang,ZhenQin,XuanhuiWang,andMichaelBendersky.2023.Queryexpansionby
promptinglargelanguagemodels.arXiv:2305.03653.Retrievedfromhttps://arxiv.org/abs/2305.03653
[131] SameerJain,VaishakhKeshava,SwarnashreeMysoreSathyendra,PatrickFernandes,PengfeiLiu,GrahamNeubig,and
ChuntingZhou.2023.Multi-dimensionalevaluationoftextsummarizationwithin-contextlearning.arXiv:2306.01200.
Retrievedfromhttps://arxiv.org/abs/2306.01200
[132] Joonhyun Jeong. 2023. Hijacking context in large multi-modal models. arXiv:2312.07553. Retrieved from
https://arxiv.org/abs/2312.07553
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

42:42 L.Huangetal.
[133] SoyeongJeong,JinheonBaek,SukminCho,SungJuHwang,andJongC.Park.2024.Adaptive-RAG:Learningto
adaptretrieval-augmentedlargelanguagemodelsthroughquestioncomplexity.arXiv:2403.14403.Retrievedfrom
https://arxiv.org/abs/2403.14403
[134] ZiweiJi,NayeonLee,RitaFrieske,TiezhengYu,DanSu,YanXu,EtsukoIshii,YejinBang,AndreaMadotto,and
PascaleFung.2023.Surveyofhallucinationinnaturallanguagegeneration.ACMComputingSurveys55,12(2023),
248:1–248:38.DOI:https://doi.org/10.1145/3571730
[135] ZiweiJi,TiezhengYu,YanXu,NayeonLee,EtsukoIshii,andPascaleFung.2023.Towardsmitigatinghallucination
inlargelanguagemodelsviaself-reflection.arXiv:2310.06271.Retrievedfromhttps://arxiv.org/abs/2310.06271
[136] ChaoyaJiang,WeiYe,MengfanDong,HongruiJia,HaiyangXu,MingYan,JiZhang,andShikunZhang.2024.
Hal-Eval:Auniversalandfine-grainedhallucinationevaluationframeworkforlargevisionlanguagemodels.
arXiv:2402.15721.Retrievedfromhttps://arxiv.org/abs/2402.15721
[137] HuiqiangJiang,QianhuiWu,Chin-YewLin,YuqingYang,andLiliQiu.2023.LLMLingua:Compressingpromptsfor
acceleratedinferenceoflargelanguagemodels.arXiv:2310.05736.Retrievedfromhttps://arxiv.org/abs/2310.05736
[138] ZhengbaoJiang,FrankF.Xu,LuyuGao,ZhiqingSun,QianLiu,JaneDwivedi-Yu,YimingYang,JamieCallan,and
GrahamNeubig.2023.Activeretrievalaugmentedgeneration.arXiv:2305.06983.Retrievedfromhttps://arxiv.org/
abs/2305.06983
[139] LiqiangJing,RuosenLi,YunmoChen,MengzhaoJia,andXinyaDu.2023.Faithscore:Evaluatinghallucinationsin
largevision-languagemodels.arXiv:2311.01477.Retrievedfromhttps://arxiv.org/abs/2311.01477
[140] ZhiJing,YongyeSu,YikunHan,BoYuan,HaiyunXu,ChunjiangLiu,KehaiChen,andMinZhang.2024.Whenlarge
languagemodelsmeetvectordatabases:Asurvey.arXiv:2402.01763.Retrievedfromhttps://arxiv.org/abs/2402.01763
[141] SauravKadavath,TomConerly,AmandaAskell,TomHenighan,DawnDrain,EthanPerez,NicholasSchiefer,Zac
Hatfield-Dodds,NovaDasSarma,EliTran-Johnson,etal.2022.Languagemodels(mostly)knowwhattheyknow.
arXiv:2207.05221.Retrievedfromhttps://arxiv.org/abs/2207.05221
[142] GregKamradt.2024.The5LevelsofTextSplittingforRetrieval.Youtube.Retrievedfromhttps://www.youtube.com/
watch?v=8OJC21T2SL4
[143] NikhilKandpal,HaikangDeng,AdamRoberts,EricWallace,andColinRaffel.2023.Largelanguagemodelsstruggle
tolearnlong-tailknowledge.InProceedingsoftheInternationalConferenceonMachineLearning(ICML’23).Andreas
Krause,EmmaBrunskill,KyunghyunCho,BarbaraEngelhardt,SivanSabato,andJonathanScarlett(Eds.),Proceedings
ofMachineLearningResearch,Vol.202,PMLR,15696–15707.Retrievedfromhttps://proceedings.mlr.press/v202/
kandpal23a.html
[144] VladimirKarpukhin,BarlasOguz,SewonMin,PatrickS.H.Lewis,LedellWu,SergeyEdunov,DanqiChen,and
Wen-tauYih.2020.Densepassageretrievalforopen-domainquestionanswering.InProceedingsoftheConferenceon
EmpiricalMethodsinNaturalLanguageProcessing(EMNLP’20).BonnieWebber,TrevorCohn,YulanHe,andYangLiu
(Eds.),AssociationforComputationalLinguistics,6769–6781.DOI:https://doi.org/10.18653/v1/2020.emnlp-main.550
[145] JungoKasai,KeisukeSakaguchi,YoichiTakahashi,RonanLeBras,AkariAsai,XinyanYu,DragomirRadev,NoahA.
Smith,YejinChoi,andKentaroInui.2022.RealTimeQA:What’stheanswerrightnow?arXiv:2207.13332.Retrieved
fromhttps://arxiv.org/abs/2207.13332
[146] DanielMartinKatz,MichaelJamesBommarito,ShangGao,andPabloArredondo.2023.Gpt-4PassestheBarExam.
Retrievedfromhttps://www.datascienceassn.org/sites/default/files/GPT-4%20Passes%20the%20Bar%20Exam.pdf
[147] UrvashiKhandelwal,OmerLevy,DanJurafsky,LukeZettlemoyer,andMikeLewis.2020.Generalizationthrough
memorization:Nearestneighborlanguagemodels.InProceedingsofthe8thInternationalConferenceonLearning
Representations(ICLR’20).OpenReview.net.Retrievedfromhttps://openreview.net/forum?id=HklBjCEKvH
[148] TakeshiKojima,ShixiangShaneGu,MachelReid,YutakaMatsuo,andYusukeIwasawa.2022.Largelanguagemodels
arezero-shotreasoners.In Proceedingsofthe36thInternationalConferenceonNeuralInformationProcessingSystems,
22199–22213.
[149] WojciechKryscinski,BryanMcCann,CaimingXiong,andRichardSocher.2020.Evaluatingthefactualconsistencyof
abstractivetextsummarization.InProceedingsoftheConferenceonEmpiricalMethodsinNaturalLanguageProcessing
(EMNLP).AssociationforComputationalLinguistics,9332–9346.DOI:https://doi.org/10.18653/v1/2020.emnlp-
main.750
[150] PhilippeLaban,WojciechKryŚciński,DivyanshAgarwal,AlexanderR.Fabbri,CaimingXiong,ShafiqJoty,and
Chien-ShengWu.2023.LLMsasfactualreasoners:Insightsfromexistingbenchmarksandbeyond.arXiv:2305.14540.
Retrievedfromhttps://arxiv.org/abs/2305.14540
[151] PhilippeLaban,TobiasSchnabel,PaulN.Bennett,andMartiA.Hearst.2022.SummaC:Re-visitingNLI-basedmodels
forinconsistencydetectioninsummarization.TransactionsoftheAssociationforComputationalLinguistics10(2022),
163–177.DOI:https://doi.org/10.1162/tacl_a_00453
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

ASurveyonHallucinationinLargeLanguageModels 42:43
[152] Faisal Ladhak, Esin Durmus, Mirac Suzgun, Tianyi Zhang, Dan Jurafsky, Kathleen McKeown, and Tatsunori
Hashimoto.2023.Whendopre-trainingbiasespropagatetodownstreamtasks?Acasestudyintextsumma-
rization.InProceedingsofthe17thConferenceoftheEuropeanChapteroftheAssociationforComputationalLinguistics.
AssociationforComputationalLinguistics,3206–3219.Retrievedfromhttps://aclanthology.org/2023.eacl-main.234
[153] BalajiLakshminarayanan,AlexanderPritzel,andCharlesBlundell.2017.Simpleandscalablepredictiveuncer-
taintyestimationusingdeepensembles.InProceedingsofthe31stInternationalConferenceonNeuralInformation
ProcessingSystems.IsabelleGuyon,UlrikevonLuxburg,SamyBengio,HannaM.Wallach,RobFergus,S.V.N.
Vishwanathan,andRomanGarnett(Eds.),6402–6413.Retrievedfromhttps://proceedings.neurips.cc/paper/2017/
hash/9ef2ed4b7fd2c810847ffa5fa85bce38-Abstract.html
[154] TameraLanham,AnnaChen,AnshRadhakrishnan,BenoitSteiner,CarsonDenison,DannyHernandez,DustinLi,
EsinDurmus,EvanHubinger,JacksonKernion,etal.2023.Measuringfaithfulnessinchain-of-thoughtreasoning.
arXiv:2307.13702.Retrievedfromhttps://arxiv.org/abs/2307.13702
[155] BarrettMartinLattimer,PatrickChen,XinyuanZhang,andYiYang.2023.Fastandaccuratefactualinconsistency
detectionoverlongdocuments.arXiv:2310.13189.Retrievedfromhttps://arxiv.org/abs/2310.13189
[156] KatherineLee,DaphneIppolito,AndrewNystrom,ChiyuanZhang,DouglasEck,ChrisCallison-Burch,andNicholas
Carlini.2022.Deduplicatingtrainingdatamakeslanguagemodelsbetter.InProceedingsofthe60thAnnualMeeting
oftheAssociationforComputationalLinguistics(Volume1:LongPapers).AssociationforComputationalLinguistics,
8424–8445.DOI:https://doi.org/10.18653/v1/2022.acl-long.577
[157] NayeonLee,WeiPing,PengXu,MostofaPatwary,PascaleNFung,MohammadShoeybi,andBryanCatanzaro.
2022.Factualityenhancedlanguagemodelsforopen-endedtextgeneration.InProceedingsofthe36thInternational
ConferenceonNeuralInformationProcessingSystems,34586–34599.
[158] DerenLei,YaxiLi,MingyuWang,VincentYun,EmilyChing,andEslamKamal.2023.Chainofnaturallanguage
inferenceforreducinglargelanguagemodelungroundedhallucinations.arXiv:2310.03951.Retrievedfromhttps:
//arxiv.org/abs/2310.03951
[159] SicongLeng,HangZhang,GuanzhengChen,XinLi,ShijianLu,ChunyanMiao,andLidongBing.2023.Mitigat-
ingobjecthallucinationsinlargevision-languagemodelsthroughvisualcontrastivedecoding.arXiv:2311.16922.
Retrievedfromhttps://arxiv.org/abs/2311.16922.
[160] BALevinsteinandDanielA.Herrmann.2023.Stillnoliedetectorforlanguagemodels:Probingempiricaland
conceptualroadblocks.arXiv:2307.00175.Retrievedfromhttps://arxiv.org/abs/2307.00175
[161] MikeLewis,YinhanLiu,NamanGoyal,MarjanGhazvininejad,AbdelrahmanMohamed,OmerLevy,VeselinStoyanov,
andLukeZettlemoyer.2020.BART:Denoisingsequence-to-sequencepre-trainingfornaturallanguagegeneration,
translation,andcomprehension.InProceedingsofthe58thAnnualMeetingoftheAssociationforComputational
Linguistics.AssociationforComputationalLinguistics,7871–7880.DOI:https://doi.org/10.18653/v1/2020.acl-main.703
[162] PatrickS.H.Lewis,EthanPerez,AleksandraPiktus,FabioPetroni,VladimirKarpukhin,NamanGoyal,Heinrich
Küttler,MikeLewis,Wen-tauYih,TimRocktäschel,etal.2020.Retrieval-augmentedgenerationforknowledge-
intensiveNLPtasks.InProceedingsofthe34thInternationalConferenceonNeuralInformationProcessingSystems.
HugoLarochelle,Marc’AurelioRanzato,RaiaHadsell,Maria-FlorinaBalcan,andHsuan-TienLin(Eds.),Retrieved
fromhttps://proceedings.neurips.cc/paper/2020/hash/6b493230205f780e1bc26945df7481e5-Abstract.html
[163] DaliangLi,AnkitSinghRawat,ManzilZaheer,XinWang,MichalLukasik,AndreasVeit,FelixX.Yu,andSanjiv
Kumar.2023.Largelanguagemodelswithcontrollableworkingmemory.InProceedingsoftheInternationalConference
onFindingsoftheAssociationforComputationalLinguistics.AnnaRogers,JordanL.Boyd-Graber,andNaoakiOkazaki
(Eds.),AssociationforComputationalLinguistics,1774–1793.DOI:https://doi.org/10.18653/v1/2023.findings-acl.112
[164] JiachunLi,PengfeiCao,YuboChen,KangLiu,andJunZhao.2024.Towardsfaithfulchain-of-thought:largelanguage
modelsarebridgingreasoners.arXiv:2405.18915.Retrievedfromhttps://arxiv.org/abs/2405.18915
[165] JunyiLi,JieChen,RuiyangRen,XiaoxueCheng,WayneXinZhao,Jian-YunNie,andJi-RongWen.2024.Thedawn
afterthedark:Anempiricalstudyonfactualityhallucinationinlargelanguagemodels.arXiv:2401.03205.Retrieved
fromhttps://arxiv.org/abs/2401.03205
[166] JunyiLi,XiaoxueCheng,WayneXinZhao,Jian-YunNie,andJi-RongWen.2023.HaluEval:Alarge-scalehallucination
evaluationbenchmarkforlargelanguagemodels.arXiv:2305.11747.Retrievedfromhttps://arxiv.org/abs/2305.11747
[167] JunnanLi,DongxuLi,SilvioSavarese,andStevenHoi.2023.Blip-2:Bootstrappinglanguage-imagepre-trainingwith
frozenimageencodersandlargelanguagemodels.arXiv:2301.12597.Retrievedfromhttps://arxiv.org/abs/2301.12597
[168] JinmingLi,WentaoZhang,TianWang,GuangleiXiong,AlanLu,andGerardMedioni.2023.GPT4Rec:Agenerative
frameworkforpersonalizedrecommendationanduserinterestsinterpretation.InProceedingsoftheSIGIRWorkshopon
eCommerceCo-locatedwiththe46thInternationalACMSIGIRConferenceonResearchandDevelopmentinInformation
Retrieval(SIGIR23).SuryaKallumadi,YubinKim,TracyHollowayKing,ShervinMalmasi,MaartendeRijke,
andJacopoTagliabue(Eds.),CEURWorkshopProceedings,Vol.3589,CEUR-WS.org.Retrievedfromhttps://ceur-
ws.org/Vol-3589/paper_2.pdf
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

42:44 L.Huangetal.
[169] KennethLi,OamPatel,FernandaViégas,HanspeterPfister,andMartinWattenberg.2023.Inference-timeintervention:
Elicitingtruthfulanswersfromalanguagemodel.arXiv:2306.03341.Retrievedfromhttps://arxiv.org/abs/2306.03341
[170] MinghanLi,XilunChen,AriHoltzman,BeidiChen,JimmyLin,Wen-tauYih,andXiVictoriaLin.2024.Nearest
neighborspeculativedecodingforLLMgenerationandattribution.arXiv:2405.19325.Retrievedfromhttps://arxiv.
org/abs/2405.19325
[171] WeiLi,WenhaoWu,MoyeChen,JiachenLiu,XinyanXiao,andHuaWu.2022.Faithfulnessinnaturallanguage
generation:Asystematicsurveyofanalysis,evaluationandoptimizationmethods.arXiv:2203.05227.Retrievedfrom
https://arxiv.org/abs/2203.05227
[172] XiangLisaLi,AriHoltzman,DanielFried,PercyLiang,JasonEisner,TatsunoriHashimoto,LukeZettlemoyer,and
MikeLewis.2022.Contrastivedecoding:Open-endedtextgenerationasoptimization.arXiv:2210.15097.Retrieved
fromhttps://arxiv.org/abs/2210.15097
[173] YuchengLi.2023.UnlockingcontextconstraintsofLLMs:EnhancingcontextefficiencyofLLMswithself-information-
basedcontentfiltering.arXiv:2304.12102.Retrievedfromhttps://arxiv.org/abs/2304.12102
[174] YuanzhiLi,SébastienBubeck,RonenEldan,AllieDelGiorno,SuriyaGunasekar,andYinTatLee.2023.Textbooks
areallyouneedII:phi-1.5technicalreport.arXiv:2309.05463.Retrievedfromhttps://arxiv.org/abs/2309.05463
[175] YifanLi,YifanDu,KunZhou,JinpengWang,WayneXinZhao,andJi-RongWen.2023.Evaluatingobjecthallucination
inlargevision-languagemodels.Retrievedfromhttps://arxiv.org/abs/2305.10355
[176] YunxiangLi,ZihanLi,KaiZhang,RuilongDan,andYouZhang.2023.ChatDoctor:Amedicalchatmodelfine-tunedon
LLaMAmodelusingmedicaldomainknowledge.arXiv:2303.14070.Retrievedfromhttps://arxiv.org/abs/2303.14070
[177] ZuchaoLi,ShitouZhang,HaiZhao,YifeiYang,andDongjieYang.2023i.BatGPT:Abidirectionalautoregessivetalker
fromgenerativepre-trainedtransformer.arXiv:2307.00360(2023).Retrievedfromhttps://arxiv.org/abs/2307.00360
[178] Chin-YewLin.2004.ROUGE:Apackageforautomaticevaluationofsummaries.InTextSummarizationBranches
Out.AssociationforComputationalLinguistics,74–81.Retrievedfromhttps://aclanthology.org/W04-1013
[179] StephanieLin,JacobHilton,andOwainEvans.2022.TruthfulQA:Measuringhowmodelsmimichumanfalsehoods.
InProceedingsofthe60thAnnualMeetingoftheAssociationforComputationalLinguistics(Volume1:LongPapers).
AssociationforComputationalLinguistics,3214–3252.DOI:https://doi.org/10.18653/v1/2022.acl-long.229
[180] BingbinLiu,JordanT.Ash,SurbhiGoel,AkshayKrishnamurthy,andCyrilZhang.2023.Exposingattentionglitches
withflip-floplanguagemodeling.arXiv:2306.00946.Retrievedfromhttps://arxiv.org/abs/2306.00946
[181] FuxiaoLiu,TianruiGuan,ZongxiaLi,LichangChen,YaserYacoob,DineshManocha,andTianyiZhou.2023.
HallusionBench:YouSeeWhatYouThink?OrYouThinkWhatYouSee?AnImage-ContextReasoningBenchmark
ChallengingforGPT-4V(Ision),LLaVA-1.5,andOtherMulti-ModalityModels.Retrievedfromhttps://arxiv.org/abs/
2310.14566
[182] FuxiaoLiu,KevinLin,LinjieLi,JianfengWang,YaserYacoob,andLijuanWang.2023.Mitigatinghallucinationinlarge
multi-modalmodelsviarobustinstructiontuning.arXiv:2306.14565.Retrievedfromhttps://arxiv.org/abs/2306.14565
[183] HaotianLiu,ChunyuanLi,QingyangWu,andYongJaeLee.2023.Visualinstructiontuning.arXiv:2304.08485.
Retrievedfromhttps://arxiv.org/abs/2304.08485
[184] HanchaoLiu,WenyuanXue,YifeiChen,DapengChen,XiutianZhao,KeWang,LipingHou,RongjunLi,and
WeiPeng.2024.Asurveyonhallucinationinlargevision-languagemodels.arXiv:2402.00253.Retrievedfrom
https://arxiv.org/abs/2402.00253
[185] JunyiLiu,LiangzhiLi,TongXiang,BowenWang,andYimingQian.2023.TCRA-LLM:Tokencompressionretrieval
augmentedlargelanguagemodelforinferencecostreduction.InProceedingsoftheInternationalConferenceon
FindingsoftheAssociationforComputationalLinguistics(EMNLP’23).HoudaBouamor,JuanPino,andKalikaBali
(Eds.),AssociationforComputationalLinguistics,9796–9810.Retrievedfromhttps://aclanthology.org/2023.findings-
emnlp.655
[186] NelsonF.Liu,KevinLin,JohnHewitt,AshwinParanjape,MicheleBevilacqua,FabioPetroni,andPercyLiang.2023.
Lostinthemiddle:Howlanguagemodelsuselongcontexts.arXiv:2307.03172.Retrievedfromhttps://arxiv.org/abs/
2307.03172
[187] YangLiu,DanIter,YichongXu,ShuohangWang,RuochenXu,andChenguangZhu.2023.Gpteval:Nlgevaluation
usinggpt-4withbetterhumanalignment.arXiv:2303.16634.Retrievedfromhttps://arxiv.org/abs/2303.16634
[188] YinhanLiu,MyleOtt,NamanGoyal,JingfeiDu,MandarJoshi,DanqiChen,OmerLevy,MikeLewis,LukeZettlemoyer,
andVeselinStoyanov.2019.RoBERTa:ArobustlyoptimizedBERTpretrainingapproach.arXiv:1907.11692.Retrieved
fromhttp://arxiv.org/abs/1907.11692
[189] YangLiu,YuanshunYao,Jean-FrancoisTon,XiaoyingZhang,RuochengGuo,HaoCheng,YegorKlochkov,Muham-
madFaaizTaufiq,andHangLi.2023.TrustworthyLLMs:Asurveyandguidelineforevaluatinglargelanguage
models’alignment.arXiv:2308.05374.Retrievedfromhttps://arxiv.org/abs/2308.05374
[190] YijinLiu,XianfengZeng,FandongMeng,andJieZhou.2023.Instructionpositionmattersinsequencegeneration
withlargelanguagemodels.arXiv:2308.12097.Retrievedfromhttps://arxiv.org/abs/2308.12097
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

ASurveyonHallucinationinLargeLanguageModels 42:45
[191] ShayneLongpre,KartikPerisetla,AnthonyChen,NikhilRamesh,ChrisDuBois,andSameerSingh.2021.Entity-
basedknowledgeconflictsinquestionanswering.InProceedingsoftheConferenceonEmpiricalMethodsinNatural
LanguageProcessing(EMNLP’21).Marie-FrancineMoens,XuanjingHuang,LuciaSpecia,andScottWen-tauYih(Eds.),
AssociationforComputationalLinguistics,7052–7063.DOI:https://doi.org/10.18653/V1/2021.EMNLP-MAIN.565
[192] HolyLovenia,WenliangDai,SamuelCahyawijaya,ZiweiJi,andPascaleFung.2023.Negativeobjectpresence
evaluation(NOPE)tomeasureobjecthallucinationinvision-languagemodels.arXiv:2310.05338.Retrievedfrom
https://arxiv.org/abs/2310.05338
[193] JiayingLu,JinmengRao,KezhenChen,XiaoyuanGuo,YawenZhang,BaochenSun,CarlYang,andJieYang.2023.
EvaluationandMitigationofAgnosiainMultimodalLargeLanguageModels.arXiv:2309.04041.Retrievedfrom
https://arxiv.org/abs/2309.04041
[194] HuaishaoLuo,LeiJi,BotianShi,HaoyangHuang,NanDuan,TianruiLi,JasonLi,TaroonBharti,andMingZhou.
2020.Univl:Aunifiedvideoandlanguagepre-trainingmodelformultimodalunderstandingandgeneration.
arXiv:2002.06353.Retrievedfromhttps://arxiv.org/abs/2002.06353
[195] JunyuLuo,CaoXiao,andFenglongMa.2023.Zero-resourcehallucinationpreventionforlargelanguagemodels.
arXiv:2309.02654.Retrievedfromhttps://arxiv.org/abs/2309.02654
[196] ZhehengLuo,QianqianXie,andSophiaAnaniadou.2023.Chatgptasafactualinconsistencyevaluatorfortext
summarization.arXiv:2303.15621.Retrievedfromhttps://arxiv.org/abs/2303.15621
[197] XinbeiMa,YeyunGong,PengchengHe,HaiZhao,andNanDuan.2023.Queryrewritingforretrieval-augmented
largelanguagemodels.arXiv:2305.14283.Retrievedfromhttps://arxiv.org/abs/2305.14283
[198] MuhammadMaaz,HanoonaRasheed,SalmanKhan,andFahadShahbazKhan.2023.Video-ChatGPT:Towards
detailedvideounderstandingvialargevisionandlanguagemodels.arXiv:2306.05424.Retrievedfromhttps://arxiv.
org/abs/2306.05424
[199] Fiona Macpherson and Dimitris Platchias. 2013. Hallucination: Philosophy and Psychology. MIT Press. Re-
trievedfromhttps://books.google.com/books?hl=zh-CN{&}lr={&}id=_bwtAAAAQBAJ{&}oi=fnd{&}pg=PR5{&}dq=
Hallucination:+Philosophy+and+psychology{&}ots=2E62kf7_yC{&}sig=rH9HGXYacNkxOJNMVbw514aChZo
[200] ChaitanyaMalaviya,SubinLee,SihaoChen,ElizabethSieber,MarkYatskar,andDanRoth.2023.ExpertQA:Expert-
curatedquestionsandattributedanswers.arXiv:2309.07852.Retrievedfromhttps://arxiv.org/abs/2309.07852
[201] AlexMallen,AkariAsai,VictorZhong,RajarshiDas,DanielKhashabi,andHannanehHajishirzi.2023.Whennotto
trustlanguagemodels:Investigatingeffectivenessofparametricandnon-parametricmemories.InProceedingsof
the61stAnnualMeetingoftheAssociationforComputationalLinguistics(Volume1:LongPapers)(ACL’23).Anna
Rogers,JordanL.Boyd-Graber,andNaoakiOkazaki(Eds.),AssociationforComputationalLinguistics,9802–9822.
DOI:https://doi.org/10.18653/v1/2023.acl-long.546
[202] PotsaweeManakul,AdianLiusie,andMarkJ.F.Gales.2023.SelfCheckGPT:Zero-resourceblack-boxhallucination
detectionforgenerativelargelanguagemodels.arXiv:2303.08896.Retrievedfromhttps://arxiv.org/abs/2303.08896
[203] UdiManberandGeneMyers.1993.Suffixarrays:Anewmethodforon-linestringsearches.SIAMJournalon
Computing22,5(1993),935–948.
[204] ShengyuMao,YongJiang,BoliChen,XiaoLi,PengWang,XinyuWang,PengjunXie,FeiHuang,HuajunChen,and
NingyuZhang.2024.RaFe:RankingfeedbackimprovesqueryrewritingforRAG.arXiv:2405.14431.Retrievedfrom
https://arxiv.org/abs/2405.14431
[205] JoshuaMaynez,ShashiNarayan,BerndBohnet,andRyanMcDonald.2020.Onfaithfulnessandfactualityin
abstractivesummarization.InProceedingsofthe58thAnnualMeetingoftheAssociationforComputationalLinguistics.
AssociationforComputationalLinguistics,1906–1919.DOI:https://doi.org/10.18653/v1/2020.acl-main.173
[206] ClaraMeister,RyanCotterell,andTimVieira.2020.Ifbeamsearchistheanswer,whatwasthequestion?.InProceed-
ingsoftheConferenceonEmpiricalMethodsinNaturalLanguageProcessing(EMNLP).AssociationforComputational
Linguistics,2173–2185.DOI:https://doi.org/10.18653/v1/2020.emnlp-main.170
[207] KevinMeng,DavidBau,AlexAndonian,andYonatanBelinkov.2022.LocatingandeditingfactualassociationsinGPT.
InProceedingsofthe36thInternationalConferenceonNeuralInformationProcessingSystems(NeurIPS).Retrievedfrom
http://papers.nips.cc/paper_files/paper/2022/hash/6f1d43d5a82a37e89b0665b33bf3a182-Abstract-Conference.html
[208] KevinMeng,ArnabSenSharma,AlexJ.Andonian,YonatanBelinkov,andDavidBau.2023.Mass-editingmem-
oryinatransformer.InProceedingsofthe11thInternationalConferenceonLearningRepresentations(ICLR’23).
OpenReview.net.Retrievedfromhttps://openreview.net/pdf?id=MkbcAHIYgyS
[209] MengqiMiao,FandongMeng,YijinLiu,Xiao-HuaZhou,andJieZhou.2021.Preventthelanguagemodelfrom
beingoverconfidentinneuralmachinetranslation.InProceedingsofthe59thAnnualMeetingoftheAssociationfor
ComputationalLinguisticsandthe11thInternationalJointConferenceonNaturalLanguageProcessing(Volume1:Long
Papers).AssociationforComputationalLinguistics,3456–3468.DOI:https://doi.org/10.18653/v1/2021.acl-long.268
[210] NingMiao,YeeWhyeTeh,andTomRainforth.2023.Selfcheck:Usingllmstozero-shotchecktheirownstep-by-step
reasoning.arXiv:2308.00436.Retrievedfromhttps://arxiv.org/abs/2308.00436
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

42:46 L.Huangetal.
[211] Microsoft.2023.NewBing.Retrievedfromhttps://www.bing.com/new
[212] SewonMin,SuchinGururangan,EricWallace,HannanehHajishirzi,NoahA.Smith,andLukeZettlemoyer.2023.
SILOlanguagemodels:Isolatinglegalriskinanonparametricdatastore.arXiv:2308.04430.Retrievedfromhttps:
//arxiv.org/abs/2308.04430
[213] SewonMin,KalpeshKrishna,XinxiLyu,MikeLewis,Wen-tauYih,PangWeiKoh,MohitIyyer,LukeZettlemoyer,
andHannanehHajishirzi.2023.FActScore:Fine-grainedatomicevaluationoffactualprecisioninlongformtext
generation.arXiv:2305.14251.Retrievedfromhttps://arxiv.org/abs/2305.14251
[214] AnshumanMishra,DhruveshPatel,AparnaVijayakumar,XiangLorraineLi,PavanKapanipathi,andKartikTa-
lamadupula.2021.Lookingbeyondsentence-levelnaturallanguageinferenceforquestionansweringandtext
summarization.InProceedingsoftheConferenceoftheNorthAmericanChapteroftheAssociationforComputa-
tionalLinguistics:HumanLanguageTechnologies.AssociationforComputationalLinguistics,1322–1336.DOI:
https://doi.org/10.18653/v1/2021.naacl-main.104
[215] EricMitchell,CharlesLin,AntoineBosselut,ChelseaFinn,andChristopherD.Manning.2022.Fastmodeleditingat
scale.InProceedingsofthe10thInternationalConferenceonLearningRepresentations(ICLR’22).OpenReview.net.
Retrievedfromhttps://openreview.net/forum?id=0DcZxeWfOPt
[216] EricMitchell,CharlesLin,AntoineBosselut,ChristopherD.Manning,andChelseaFinn.2022.Memory-basedmodel
editingatscale.InProceedingsoftheInternationalConferenceonMachineLearning(ICML’22).KamalikaChaudhuri,
StefanieJegelka,LeSong,CsabaSzepesvári,GangNiu,andSivanSabato(Eds.),ProceedingsofMachineLearning
Research,Vol.162,PMLR,15817–15831.Retrievedfromhttps://proceedings.mlr.press/v162/mitchell22a.html
[217] LucaMoschella,ValentinoMaiorca,MarcoFumero,AntonioNorelli,FrancescoLocatello,andEmanueleRodola.
2022.Relativerepresentationsenablezero-shotlatentspacecommunication.arXiv:2209.15430.Retrievedfrom
https://arxiv.org/abs/2209.15430
[218] NiklasMuennighoff,HongjinSu,LiangWang,NanYang,FuruWei,TaoYu,AmanpreetSingh,andDouweKiela.2024.
Generativerepresentationalinstructiontuning.arXiv:2402.09906.Retrievedfromhttps://arxiv.org/abs/2402.09906
[219] NiklasMuennighoff,NouamaneTazi,LoïcMagne,andNilsReimers.2023.MTEB:Massivetextembeddingbenchmark.
InProceedingsofthe17thConferenceoftheEuropeanChapteroftheAssociationforComputationalLinguistics
(EACL’23).AndreasVlachosandIsabelleAugenstein(Eds.),AssociationforComputationalLinguistics,2006–2029.
DOI:https://doi.org/10.18653/V1/2023.EACL-MAIN.148
[220] DorMuhlgay,OriRam,InbalMagar,YoavLevine,NirRatner,YonatanBelinkov,OmriAbend,KevinLeyton-Brown,
AmnonShashua,andYoavShoham.2023.Generatingbenchmarksforfactualityevaluationoflanguagemodels.
arXiv:2307.06908.Retrievedfromhttps://arxiv.org/abs/2307.06908
[221] InderjeetNair,AparnaGarimella,BalajiVasanSrinivasan,NatwarModani,NiyatiChhaya,SrikrishnaKaranam,and
SumitShekhar.2023.AneuralCRF-basedhierarchicalapproachforlineartextsegmentation.InProceedingsofthe
InternationalConferenceonFindingsoftheAssociationforComputationalLinguistics(EACL’23).AndreasVlachos
andIsabelleAugenstein(Eds.),AssociationforComputationalLinguistics,853–863.DOI:https://doi.org/10.18653/
V1/2023.FINDINGS-EACL.65
[222] FengNan,RameshNallapati,ZhiguoWang,CiceroNogueiradosSantos,HenghuiZhu,DejiaoZhang,Kathleen
McKeown,andBingXiang.2021.Entity-levelfactualconsistencyofabstractivetextsummarization.InProceedingsof
the16thConferenceoftheEuropeanChapteroftheAssociationforComputationalLinguistics:MainVolume.Association
forComputationalLinguistics,2727–2733.DOI:https://doi.org/10.18653/v1/2021.eacl-main.235
[223] PranavNarayananVenkit,SanjanaGautam,RuchiPanchanadikar,Ting-HaoHuang,andShomirWilson.2023.
Nationalitybiasintextgeneration.InProceedingsofthe17thConferenceoftheEuropeanChapteroftheAssociationfor
ComputationalLinguistics.AssociationforComputationalLinguistics,116–122.Retrievedfromhttps://aclanthology.
org/2023.eacl-main.9
[224] EllaNeeman,RoeeAharoni,OrHonovich,LeshemChoshen,IdanSzpektor,andOmriAbend.2023.DisentQA:
Disentanglingparametricandcontextualknowledgewithcounterfactualquestionanswering.InProceedingsofthe
61stAnnualMeetingoftheAssociationforComputationalLinguistics(Volume1:LongPapers)(ACL’23),AnnaRogers,
JordanL.Boyd-Graber,andNaoakiOkazaki(Eds.),AssociationforComputationalLinguistics,10056–10070.DOI:
https://doi.org/10.18653/V1/2023.ACL-LONG.559
[225] ShiyuNi,KepingBi,JiafengGuo,andXueqiCheng.2024.WhendoLLMsneedretrievalaugmentation?Mitigating
LLMs’overconfidencehelpsretrievalaugmentation.arXiv:2402.11457.Retrievedfromhttps://arxiv.org/abs/2402.
11457
[226] Sean O’Brien and Mike Lewis. 2023. Contrastive decoding improves reasoning in large language models.
arXiv:2309.09117.Retrievedfromhttps://arxiv.org/abs/2309.09117
[227] YasumasaOnoe,MichaelZhang,EunsolChoi,andGregDurrett.2022.Entityclozebydate:WhatLMsknowabout
unseenentities.InProceedingsoftheInternationalConferenceonFindingsoftheAssociationforComputational
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

ASurveyonHallucinationinLargeLanguageModels 42:47
Linguistics(NAACL’22).AssociationforComputationalLinguistics,693–702.DOI:https://doi.org/10.18653/v1/2022.
findings-naacl.52
[228] OpenAI.2022.Introducingchatgpt.Retrievedfromhttps://openai.com/blog/chatgpt
[229] OpenAI.2023.GPT-4technicalreport.arXiv:2303.08774.Retrievedfromhttps://arxiv.org/abs/2303.08774
[230] LongOuyang,JeffreyWu,XuJiang,DiogoAlmeida,CarrollL.Wainwright,PamelaMishkin,ChongZhang,Sandhini
Agarwal,KatarinaSlama,AlexRay,etal.2022.Traininglanguagemodelstofollowinstructionswithhumanfeedback.
InNeurIPS.Retrievedfromhttp://papers.nips.cc/paper_files/paper/2022/hash/b1efde53be364a73914f58805a001731-
Abstract-Conference.html
[231] OdedOvadia,MenachemBrief,MoshikMishaeli,andOrenElisha.2023.Fine-tuningorretrieval?Comparing
knowledgeinjectioninLLMs.arXiv:2312.05934.Retrievedfromhttps://arxiv.org/abs/2312.05934
[232] LorenzoPacchiardi,AlexJChan,SörenMindermann,IlanMoscovitz,AlexaYPan,YarinGal,OwainEvans,
andJanBrauner.2023.HowtocatchanAIliar:Liedetectioninblack-boxLLMsbyaskingunrelatedquestions.
arXiv:2309.15840.Retrievedfromhttps://arxiv.org/abs/2309.15840
[233] ArtidoroPagnoni,VidhishaBalachandran,andYuliaTsvetkov.2021.Understandingfactualityinabstractivesumma-
rizationwithFRANK:Abenchmarkforfactualitymetrics.InProceedingsoftheConferenceoftheNorthAmerican
ChapteroftheAssociationforComputationalLinguistics:HumanLanguageTechnologies.AssociationforComputa-
tionalLinguistics,Online,4812–4829.DOI:https://doi.org/10.18653/v1/2021.naacl-main.383
[234] LiangmingPan,MichaelSaxon,WendaXu,DeepakNathani,XinyiWang,andWilliamYangWang.2023.Automati-
callycorrectinglargelanguagemodels:Surveyingthelandscapeofdiverseself-correctionstrategies.arXiv:2308.03188.
Retrievedfromhttps://arxiv.org/abs/2308.03188
[235] RuotongPan,BoxiCao,HongyuLin,XianpeiHan,JiaZheng,SiruiWang,XunliangCai,andLeSun.2024.Notall
contextsareequal:TeachingLLMscredibility-awaregeneration.arXiv:2404.06809.Retrievedfromhttps://arxiv.org/
abs/2404.06809
[236] KishorePapineni,SalimRoukos,ToddWard,andWei-JingZhu.2002.Bleu:Amethodforautomaticevaluation
ofmachinetranslation.InProceedingsofthe40thAnnualMeetingoftheAssociationforComputationalLinguistics.
AssociationforComputationalLinguistics,311–318.DOI:https://doi.org/10.3115/1073083.1073135
[237] AnkurP.Parikh,XuezhiWang,SebastianGehrmann,ManaalFaruqui,BhuwanDhingra,DiyiYang,andDipanjan
Das.2020.ToTTo:Acontrolledtable-to-textgenerationdataset.InProceedingsoftheConferenceonEmpiricalMethods
inNaturalLanguageProcessing(EMNLP’20).BonnieWebber,TrevorCohn,YulanHe,andYangLiu(Eds.),Association
forComputationalLinguistics,1173–1186.DOI:https://doi.org/10.18653/V1/2020.EMNLP-MAIN.89
[238] DebjitPaul,RobertWest,AntoineBosselut,andBoiFaltings.2024.Makingreasoningmatter:Measuringand
improvingfaithfulnessofchain-of-thoughtreasoning.arXiv:2402.13950.Retrievedfromhttps://arxiv.org/abs/2402.
13950
[239] AmandalynnePaullada,InioluwaDeborahRaji,EmilyM.Bender,EmilyDenton,andAlexHanna.2021.Dataandits
(dis)contents:Asurveyofdatasetdevelopmentanduseinmachinelearningresearch.Patterns2,11(2021),100336.
DOI:https://doi.org/10.1016/J.PATTER.2021.100336
[240] GuilhermePenedo,QuentinMalartic,DanielHesslow,RuxandraCojocaru,AlessandroCappelli,HamzaAlobei-
dli,BaptistePannier,EbtesamAlmazrouei,andJulienLaunay.2023.TheRefinedWebdatasetforfalconLLM:
Outperforming curated corpora with web data, and web data only. arXiv:2306.01116. Retrieved from https:
//arxiv.org/abs/2306.01116
[241] BaolinPeng,ChunyuanLi,PengchengHe,MichelGalley,andJianfengGao.2023.Instructiontuningwithgpt-4.
arXiv:2304.03277.Retrievedfromhttps://arxiv.org/abs/2304.03277
[242] EthanPerez,SamRinger,KamileLukosiute,KarinaNguyen,EdwinChen,ScottHeiner,CraigPettit,Catherine
Olsson,SandipanKundu,SauravKadavath,etal.2023.Discoveringlanguagemodelbehaviorswithmodel-written
evaluations.InProceedingsoftheInternationalConferenceonFindingsoftheAssociationforComputationalLinguistics
(ACL’23).AnnaRogers,JordanL.Boyd-Graber,andNaoakiOkazaki(Eds.),AssociationforComputationalLinguistics,
13387–13434.DOI:https://doi.org/10.18653/V1/2023.FINDINGS-ACL.847
[243] FabioPetroni,TimRocktäschel,SebastianRiedel,PatrickLewis,AntonBakhtin,YuxiangWu,andAlexanderMiller.
2019.Languagemodelsasknowledgebases?InProceedingsoftheConferenceonEmpiricalMethodsinNatural
LanguageProcessingandthe9thInternationalJointConferenceonNaturalLanguageProcessing(EMNLP-IJCNLP).
AssociationforComputationalLinguistics,2463–2473.DOI:https://doi.org/10.18653/v1/D19-1250
[244] OfirPress,MuruZhang,SewonMin,LudwigSchmidt,NoahASmith,andMikeLewis.2022.Measuringandnarrowing
thecompositionalitygapinlanguagemodels.arXiv:2210.03350.Retrievedfromhttps://arxiv.org/abs/2210.03350
[245] JiruiQi,GabrieleSarti,RaquelFernández,andAriannaBisazza.2024.Modelinternals-basedanswerattributionfor
trustworthyretrieval-augmentedgeneration.arXiv:2406.13663.Retrievedfromhttps://arxiv.org/abs/2406.13663
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

42:48 L.Huangetal.
[246] ZhixiaoQi,YijiongYu,MeiqiTu,JunyiTan,andYongfengHuang.2023.FoodGPT:Alargelanguagemodelin
foodtestingdomainwithincrementalpre-trainingandknowledgegraphprompt.arXiv:2308.10173.Retrievedfrom
https://arxiv.org/abs/2308.10173
[247] ShuofeiQiao,YixinOu,NingyuZhang,XiangChen,YunzhiYao,ShuminDeng,ChuanqiTan,FeiHuang,and
HuajunChen.2022.Reasoningwithlanguagemodelprompting:Asurvey.arXiv:2212.09597.Retrievedfromhttps:
//arxiv.org/abs/2212.09597
[248] AlecRadford,KarthikNarasimhan,TimSalimans,andIlyaSutskever.2018.Improvinglanguageunderstandingby
generativepre-training.
[249] AlecRadford,JeffreyWu,RewonChild,DavidLuan,DarioAmodei,andIlyaSutskever.2019.Languagemodelsare
unsupervisedmultitasklearners.OpenAIblog1,8(2019),9.
[250] RafaelRafailov,ArchitSharma,EricMitchell,StefanoErmon,ChristopherD.Manning,andChelseaFinn.2023.
Directpreferenceoptimization:Yourlanguagemodelissecretlyarewardmodel.arXiv:2305.18290.Retrievedfrom
https://arxiv.org/abs/2305.18290
[251] ColinRaffel,NoamShazeer,AdamRoberts,KatherineLee,SharanNarang,MichaelMatena,YanqiZhou,WeiLi,and
PeterJ.Liu.2020.Exploringthelimitsoftransferlearningwithaunifiedtext-to-texttransformer.TheJournalof
MachineLearningResearch21(2020),140:1–140:67.Retrievedfromhttp://jmlr.org/papers/v21/20-074.html
[252] OriRam,YoavLevine,ItayDalmedigos,DorMuhlgay,AmnonShashua,KevinLeyton-Brown,andYoavShoham.2023.
In-contextretrieval-augmentedlanguagemodels.arXiv:2302.00083.Retrievedfromhttps://arxiv.org/abs/2302.00083
[253] Marc’AurelioRanzato,SumitChopra,MichaelAuli,andWojciechZaremba.2016.Sequenceleveltrainingwith
recurrentneuralnetworks.InProceedingsofthe4thInternationalConferenceonLearningRepresentations(ICLR’16).
YoshuaBengioandYannLeCun(Eds.),Retrievedfromhttp://arxiv.org/abs/1511.06732
[254] MathieuRavaut,AixinSun,NancyF.Chen,andShafiqJoty.2024.Oncontextutilizationinsummarizationwith
largelanguagemodels.arXiv:2310.10570.Retrievedfromhttps://arxiv.org/abs/2310.10570
[255] VipulaRawte,AmitP.Sheth,andAmitavaDas.2023.Asurveyofhallucinationinlargefoundationmodels.
arXiv:2309.05922.Retrievedfromhttps://arxiv.org/abs/2309.05922
[256] MachelReid,NikolaySavinov,DenisTeplyashin,DmitryLepikhin,TimothyLillicrap,JeanbaptisteAlayrac,Radu
Soricut,AngelikiLazaridou,OrhanFirat,JulianSchrittwieser,etal.2024.Gemini1.5:Unlockingmultimodalunder-
standingacrossmillionsoftokensofcontext.arXiv:2403.05530Retrievedfromhttps://arxiv.org/abs/2403.05530
[257] RuiyangRen,YuhaoWang,YingqiQu,WayneXinZhao,JingLiu,HaoTian,HuaWu,Ji-RongWen,andHaifeng
Wang.2023.Investigatingthefactualknowledgeboundaryoflargelanguagemodelswithretrievalaugmentation.
arXiv:2307.11019.Retrievedfromhttps://arxiv.org/abs/2307.11019
[258] Reuters.2023.U.S.CopyrightOfficeSaysSomeAI-AssistedWorksMayBeCopyrighted.Retrievedfromhttps:
//www.reuters.com/world/us/us-copyright-office-says-some-ai-assisted-works-may-be-copyrighted-2023-03-15/
[259] NinaRimsky.2023.ModulatingSycophancyinanRLHFModelviaActivationSteering.Retrievedfromhttps://www.
alignmentforum.org/posts/zt6hRsDE84HeBKh7E/reducing-sycophancy-and-improving-honesty-via-activation
[260] NinaRimsky.2023.ReducingSycophancyandImprovingHonestyviaActivationSteering.Retrievedfromhttps://
www.alignmentforum.org/posts/zt6hRsDE84HeBKh7E/reducing-sycophancy-and-improving-honesty-via-activation
[261] VinuSankarSadasivan,AounonKumar,SriramBalasubramanian,WenxiaoWang,andSoheilFeizi.2023.Can
AI-generatedtextbereliablydetected?arXiv:2303.11156.Retrievedfromhttps://arxiv.org/abs/2303.11156
[262] SashankSanthanam,BehnamHedayatnia,SpandanaGella,AishwaryaPadmakumar,SeokhwanKim,YangLiu,
andDilekHakkani-Tur.2021.Romewasbuiltin1776:Acasestudyonfactualcorrectnessinknowledge-grounded
responsegeneration.arXiv:2110.05456.Retrievedfromhttps://arxiv.org/abs/2110.05456
[263] ParthSarthi,SalmanAbdullah,AditiTuli,ShubhKhanna,AnnaGoldie,andChristopherD.Manning.2024.RAPTOR:
Recursiveabstractiveprocessingfortree-organizedretrieval.arXiv:2401.18059.Retrievedfromhttps://arxiv.org/abs/
2401.18059
[264] WilliamSaunders,CatherineYeh,JeffWu,StevenBills,LongOuyang,JonathanWard,andJanLeike.2022.Self-
critiquingmodelsforassistinghumanevaluators.arXiv:2206.05802.Retrievedfromhttps://arxiv.org/abs/2206.05802
[265] JohnSchulman.2023.ReinforcementLearningfromHumanFeedback:ProgressandChallenges.BerkeleyEECS.
Retrievedfromhttps://www.youtube.com/watch?v=hhiLw5Q_UFg
[266] JohnSchulman,FilipWolski,PrafullaDhariwal,AlecRadford,andOlegKlimov.2017.Proximalpolicyoptimization
algorithms.arXiv:1707.06347.Retrievedfromhttps://arxiv.org/abs/1707.06347
[267] ThomasScialom,Paul-AlexisDray,SylvainLamprier,BenjaminPiwowarski,JacopoStaiano,AlexWang,and
PatrickGallinari.2021.QuestEval:Summarizationasksforfact-basedevaluation.InProceedingsoftheConference
onEmpiricalMethodsinNaturalLanguageProcessing.AssociationforComputationalLinguistics,6594–6604.DOI:
https://doi.org/10.18653/v1/2021.emnlp-main.529
[268] YijiaShao,YuchengJiang,TheodoreA.Kanell,PeterXu,OmarKhattab,andMonicaS.Lam.2024.Assisting
inwritingwikipedia-likearticlesfromscratchwithlargelanguagemodels.arXiv:2402.14207.Retrievedfrom
https://arxiv.org/abs/2402.14207
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

ASurveyonHallucinationinLargeLanguageModels 42:49
[269] ZhihongShao,YeyunGong,YelongShen,MinlieHuang,NanDuan,andWeizhuChen.2023.Enhancingretrieval-
augmentedlargelanguagemodelswithiterativeretrieval-generationsynergy.arXiv:2305.15294.Retrievedfrom
https://arxiv.org/abs/2305.15294
[270] MrinankSharma,MegTong,TomaszKorbak,DavidDuvenaud,AmandaAskell,SamuelR.Bowman,NewtonCheng,
EsinDurmus,ZacHatfield-Dodds,ScottR.Johnston,etal.2023.Towardsunderstandingsycophancyinlanguage
models.arXiv:2310.13548.Retrievedfromhttps://arxiv.org/abs/2310.13548
[271] WeijiaShi,XiaochuangHan,MikeLewis,YuliaTsvetkov,LukeZettlemoyer,andScottWen-tauYih.2023.Trusting
yourevidence:Hallucinatelesswithcontext-awaredecoding.arXiv:2305.14739.Retrievedfromhttps://arxiv.org/
abs/2305.14739
[272] WeijiaShi,SewonMin,MariaLomeli,ChuntingZhou,MargaretLi,XiVictoriaLin,NoahA.Smith,LukeZettle-
moyer,ScottYih,andMikeLewis.2023.In-contextpretraining:languagemodelingbeyonddocumentboundaries.
arXiv:2310.10638.Retrievedfromhttps://arxiv.org/abs/2310.10638
[273] WeijiaShi,SewonMin,MichihiroYasunaga,MinjoonSeo,RichJames,MikeLewis,LukeZettlemoyer,andWen-
tauYih.2023.REPLUG:Retrieval-augmentedblack-boxlanguagemodels.arXiv:2301.12652.Retrievedfromhttps:
//arxiv.org/abs/2301.12652
[274] KurtShuster,SpencerPoff,MoyaChen,DouweKiela,andJasonWeston.2021.Retrievalaugmentationreduces
hallucinationinconversation.InProceedingsoftheInternationalConferenceon FindingsoftheAssociationfor
ComputationalLinguistics(EMNLP’21).AssociationforComputationalLinguistics,3784–3803.DOI:https://doi.org/
10.18653/v1/2021.findings-emnlp.320
[275] KaranSinghal,TaoTu,JurajGottweis,RorySayres,ElleryWulczyn,LeHou,KevinClark,StephenPfohl,Heather
Cole-Lewis,DarleneNeal,etal.2023.Towardsexpert-levelmedicalquestionansweringwithlargelanguagemodels.
arXiv:2305.09617.Retrievedfromhttps://arxiv.org/abs/2305.09617
[276] AntonSinitsin,VsevolodPlokhotnyuk,DmitriyPyrkin,SergeiPopov,andArtemBabenko.2020.Editableneural
networks.InProceedingsofthe8thInternationalConferenceonLearningRepresentations(ICLR’20).OpenReview.net.
Retrievedfromhttps://openreview.net/forum?id=HJedXaEtvS
[277] AvivSlobodkin,OmerGoldman,AviCaciularu,IdoDagan,andShauliRavfogel.2023.Thecuriouscaseofhallucinatory
unanswerablity:Findingtruthsinthehiddenstatesofover-confidentlargelanguagemodels.arXiv:2310.11877.
Retrievedfromhttps://arxiv.org/abs/2310.11877
[278] AvivSlobodkin,EranHirsch,ArieCattan,TalSchuster,andIdoDagan.2024.Attributefirst,thengenerate:Locally-
attributablegroundedtextgeneration.arXiv:2403.17104.Retrievedfromhttps://arxiv.org/abs/2403.17104
[279] FelixStahlbergandBillByrne.2019.OnNMTsearcherrorsandmodelerrors:Catgotyourtongue?.InProceedings
oftheConferenceonEmpiricalMethodsinNaturalLanguageProcessingandthe9thInternationalJointConference
onNaturalLanguageProcessing(EMNLP-IJCNLP).AssociationforComputationalLinguistics,3356–3362.DOI:
https://doi.org/10.18653/v1/D19-1331
[280] IvanStelmakh,YiLuan,BhuwanDhingra,andMing-WeiChang.2022.ASQA:Factoidquestionsmeetlong-form
answers.InProceedingsoftheConferenceonEmpiricalMethodsinNaturalLanguageProcessing.Associationfor
ComputationalLinguistics,8273–8288.Retrievedfromhttps://aclanthology.org/2022.emnlp-main.566
[281] NisanStiennon,LongOuyang,JeffreyWu,DanielM.Ziegler,RyanLowe,ChelseaVoss,AlecRadford,DarioAmodei,
andPaulF.Christiano.2020.Learningtosummarizewithhumanfeedback.InProceedingsofthe34thInternational
ConferenceonNeuralInformationProcessingSystems(NeurIPS’20).HugoLarochelle,Marc’AurelioRanzato,Raia
Hadsell,Maria-FlorinaBalcan,andHsuan-TienLin(Eds.),Retrievedfromhttps://proceedings.neurips.cc/paper/2020/
hash/1f89885d556929e98d3ef9b86448f951-Abstract.html
[282] HongjinSu,HowardYen,MengzhouXia,WeijiaShi,NiklasMuennighoff,HanyuWang,HaisuLiu,QuanShi,
ZacharyS.Siegel,MichaelTang,RuoxiSun,JinsungYoon,SercanO.Arik,DanqiChen,andTaoYu.2024.BRIGHT:
Arealisticandchallengingbenchmarkforreasoning-intensiveretrieval.arXiv:2407.12883.Retrievedfromhttps:
//arxiv.org/abs/2407.12883
[283] JianlinSu,YuLu,ShengfengPan,BoWen,andYunfengLiu.2021.RoFormer:Enhancedtransformerwithrotary
positionembedding.arXiv:2104.09864.Retrievedfromhttps://arxiv.org/abs/2104.09864
[284] WeihangSu,YichenTang,QingyaoAi,ZhijingWu,andYiqunLiu.2024.DRAGIN:Dynamicretrievalaugmented
generationbasedonthereal-timeinformationneedsoflargelanguagemodels.arXiv:2403.10081.Retrievedfrom
https://arxiv.org/abs/2403.10081
[285] NishantSubramani,NiveditaSuresh,andMatthewPeters.2022.Extractinglatentsteeringvectorsfrompretrained
languagemodels.InFindingsoftheAssociationforComputationalLinguistics(ACL’22).AssociationforComputational
Linguistics,566–581.DOI:https://doi.org/10.18653/v1/2022.findings-acl.48
[286] KaiSun,YifanEthanXu,HanwenZha,YueLiu,andXinLunaDong.2023.Head-to-tail:Howknowledgeableare
largelanguagemodels(LLM)?A.K.A.willLLMsreplaceknowledgegraphs?arXiv:2308.10168.Retrievedfrom
https://arxiv.org/abs/2308.10168
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

42:50 L.Huangetal.
[287] IlyaSutskever.2023.AnObservationonGeneralization.Youtube.Retrievedfromhttps://www.youtube.com/watch?
v=AKMuA_TVz3A{&}t=5s
[288] ChenmienTan,GeZhang,andJieFu.2024.Massiveeditingforlargelanguagemodelviametalearning.InProceedings
ofthe12thInternationalConferenceonLearningRepresentations.Retrievedfromhttps://openreview.net/forum?id=
L6L1CJQ2PE
[289] HexiangTan,FeiSun,WanliYang,YuanzhuoWang,QiCao,andXueqiCheng.2024.Blindedbygeneratedcontexts:
Howlanguagemodelsmergegeneratedandretrievedcontextsforopen-domainQA?arXiv:2401.11911.Retrieved
fromhttps://arxiv.org/abs/2401.11911
[290] RaphaelTang,XinyuZhang,XueguangMa,JimmyLin,andFerhanTure.2023.Foundinthemiddle:Permutation
self-consistencyimproveslistwiserankinginlargelanguagemodels.arXiv:2310.07712.Retrievedfromhttps:
//arxiv.org/abs/2310.07712
[291] NandanThakur,NilsReimers,AndreasRücklé,AbhishekSrivastava,andIrynaGurevych.2021.BEIR:Aheterogenous
benchmarkforzero-shotevaluationofinformationretrievalmodels.arXiv:2104.08663.Retrievedfromhttps://arxiv.
org/abs/2104.08663
[292] RanTian,ShashiNarayan,ThibaultSellam,andAnkurPParikh.2019.Stickingtothefacts:Confidentdecodingfor
faithfuldata-to-textgeneration.ArXivpreprintabs/1910.08684(2019).Retrievedfromhttps://arxiv.org/abs/1910.08684
[293] ShengbangTong,ZhuangLiu,YuexiangZhai,YiMa,YannLeCun,andSainingXie.2024.Eyeswideshut?Exploring
thevisualshortcomingsofmultimodalLLMs.arXiv:2401.06209.Retrievedfromhttps://arxiv.org/abs/2401.06209
[294] S.M.TowhidulIslamTonmoy,S.M.MehediZaman,VinijaJain,AnkuRani,VipulaRawte,AmanChadha,and
AmitavaDas.2024.Acomprehensivesurveyofhallucinationmitigationtechniquesinlargelanguagemodels.
arXiv:2401.01313.Retrievedfromhttps://arxiv.org/abs/2401.01313
[295] HugoTouvron,ThibautLavril,GautierIzacard,XavierMartinet,Marie-AnneLachaux,TimothéeLacroix,Baptiste
Rozière,NamanGoyal,EricHambro,FaisalAzhar,etal.2023.LLaMA:Openandefficientfoundationlanguage
models.arXiv:2302.13971.Retrievedfromhttps://arxiv.org/abs/2302.13971
[296] HugoTouvron,LouisMartin,KevinStone,PeterAlbert,AmjadAlmahairi,YasmineBabaei,NikolayBashlykov,
SoumyaBatra,PrajjwalBhargava,ShrutiBhosale,etal.2023.Llama2:Openfoundationandfine-tunedchatmodels.
arXiv:2307.09288.Retrievedfromhttps://arxiv.org/abs/2307.09288
[297] HarshTrivedi,NiranjanBalasubramanian,TusharKhot,andAshishSabharwal.2023.Interleavingretrievalwith
chain-of-thoughtreasoningforknowledge-intensivemulti-stepquestions.InProceedingsofthe61stAnnualMeeting
oftheAssociationforComputationalLinguistics(Volume1:LongPapers)(ACL’23).AnnaRogers,JordanL.Boyd-
Graber,andNaoakiOkazaki(Eds.),AssociationforComputationalLinguistics,10014–10037.Retrievedfromhttps:
//aclanthology.org/2023.acl-long.557
[298] MilesTurpin,JulianMichael,EthanPerez,andSamuelR.Bowman.2023.Languagemodelsdon’talwayssay
whattheythink:Unfaithfulexplanationsinchain-of-thoughtprompting.arXiv:2305.04388.Retrievedfromhttps:
//arxiv.org/abs/2305.04388
[299] LogeshKumarUmapathi,AnkitPal,andMalaikannanSankarasubbu.2023.Med-halt:Medicaldomainhallucination
testforlargelanguagemodels.arXiv:2307.15343.Retrievedfromhttps://arxiv.org/abs/2307.15343
[300] AäronvandenOord,YazheLi,andOriolVinyals.2018.Representationlearningwithcontrastivepredictivecoding.
arXiv:1807.03748.Retrievedfromhttp://arxiv.org/abs/1807.03748
[301] LiamvanderPoel,RyanCotterell,andClaraMeister.2022.Mutualinformationalleviateshallucinationsinabstractive
summarization.InProceedingsoftheConferenceonEmpiricalMethodsinNaturalLanguageProcessing.Association
forComputationalLinguistics,5956–5965.Retrievedfromhttps://aclanthology.org/2022.emnlp-main.399
[302] NeerajVarshney,WenlinYao,HongmingZhang,JianshuChen,andDongYu.2023.Astitchintimesavesnine:
DetectingandmitigatinghallucinationsofLLMsbyvalidatinglow-confidencegeneration.arXiv:2307.03987.Retrieved
fromhttps://arxiv.org/abs/2307.03987
[303] ElenaVoita,DavidTalbot,FedorMoiseev,RicoSennrich,andIvanTitov.2019.Analyzingmulti-headself-attention:
specializedheadsdotheheavylifting,therestcanbepruned.InProceedingsofthe57thAnnualMeetingofthe
AssociationforComputationalLinguistics.AssociationforComputationalLinguistics,5797–5808.DOI:https://doi.
org/10.18653/v1/P19-1580
[304] TuVu,MohitIyyer,XuezhiWang,NoahConstant,JerryWei,JasonWei,ChrisTar,Yun-HsuanSung,DennyZhou,
QuocLe,andThangLuong.2023.FreshLLMs:Refreshinglargelanguagemodelswithsearchengineaugmentation.
arXiv:2310.03214.Retrievedfromhttps://arxiv.org/abs/2310.03214
[305] DavidWan,MengwenLiu,KathleenMcKeown,MarkusDreyer,andMohitBansal.2023.Faithfulness-awaredecoding
strategiesforabstractivesummarization.InProceedingsofthe17thConferenceoftheEuropeanChapterofthe
AssociationforComputationalLinguistics.AssociationforComputationalLinguistics,2864–2880.Retrievedfrom
https://aclanthology.org/2023.eacl-main.210
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

ASurveyonHallucinationinLargeLanguageModels 42:51
[306] AlexWang,KyunghyunCho,andMikeLewis.2020.Askingandansweringquestionstoevaluatethefactual
consistencyofsummaries.InProceedingsofthe58thAnnualMeetingoftheAssociationforComputationalLinguistics.
AssociationforComputationalLinguistics,5008–5020.DOI:https://doi.org/10.18653/v1/2020.acl-main.450
[307] BinjieWang,EthanChern,andPengfeiLiu.2023.ChineseFactEval:AFactualityBenchmarkforChineseLLMs.
[308] CunxiangWang,XiaozeLiu,YuanhaoYue,XiangruTang,TianhangZhang,JiayangCheng,YunzhiYao,Wenyang
Gao,XumingHu,ZehanQi,etal.2023.Surveyonfactualityinlargelanguagemodels:Knowledge,retrievaland
domain-specificity.arXiv:2310.07521.Retrievedfromhttps://arxiv.org/abs/2310.07521
[309] ChaojunWangandRicoSennrich.2020.Onexposurebias,hallucinationanddomainshiftinneuralmachine
translation.InProceedingsofthe58thAnnualMeetingoftheAssociationforComputationalLinguistics.Association
forComputationalLinguistics,3544–3552.DOI:https://doi.org/10.18653/v1/2020.acl-main.326
[310] JiaanWang,YunlongLiang,FandongMeng,HaoxiangShi,ZhixuLi,JinanXu,JianfengQu,andJieZhou.2023.Is
chatgptagoodnlgevaluator?apreliminarystudy.arXiv:2303.04048.Retrievedfromhttps://arxiv.org/abs/2303.04048
[311] JunyangWang,YuhangWang,GuohaiXu,JingZhang,YukaiGu,HaitaoJia,MingYan,JiZhang,andJitaoSang.
2023.AnLLM-freemulti-dimensionalbenchmarkformllmshallucinationevaluation.arXiv:2311.07397.Retrieved
fromhttps://arxiv.org/abs/2311.07397
[312] LeiWang,JiabangHe,ShenshenLi,NingLiu,andEe-PengLim.2024.Mitigatingfine-grainedhallucinationby
fine-tuninglargevision-languagemodelswithcaptionrewrites.InProceedingsoftheInternationalConferenceon
MultimediaModeling.Springer,32–45.
[313] LiangWang,NanYang,andFuruWei.2023.Query2doc:Queryexpansionwithlargelanguagemodels.InProceedings
oftheConferenceonEmpiricalMethodsinNaturalLanguageProcessing(EMNLP’23).HoudaBouamor,JuanPino,and
KalikaBali(Eds.),AssociationforComputationalLinguistics,9414–9423.DOI:https://doi.org/10.18653/V1/2023.
EMNLP-MAIN.585
[314] PeifengWang,ZhengyangWang,ZhengLi,YifanGao,BingYin,andXiangRen.2023.SCOTT:Self-consistent
chain-of-thoughtdistillation.arXiv:2305.01879.Retrievedfromhttps://arxiv.org/abs/2305.01879
[315] ShutingWang,XinYu,MangWang,WeipengChen,YutaoZhu,andZhichengDou.2024.RichRAG:Craftingrich
responsesformulti-facetedqueriesinretrieval-augmentedgeneration.arXiv:2406.12566.Retrievedfromhttps:
//arxiv.org/abs/2406.12566
[316] SongWang,YaochenZhu,HaochenLiu,ZaiyiZheng,ChenChen,andJundongLi.2023.Knowledgeeditingfor
largelanguagemodels:Asurvey.arXiv:2310.16218.Retrievedfromhttps://arxiv.org/abs/2310.16218
[317] YileWang,PengLi,MaosongSun,andYangLiu.2023.Self-knowledgeguidedretrievalaugmentationforlarge
languagemodels.InProceedingsoftheInternationalConferenceonFindingsoftheAssociationforComputational
Linguistics(EMNLP’23).HoudaBouamor,JuanPino,andKalikaBali(Eds.),AssociationforComputationalLinguistics,
10303–10315.DOI:https://doi.org/10.18653/V1/2023.FINDINGS-EMNLP.691
[318] YufeiWang,WanjunZhong,LiangyouLi,FeiMi,XingshanZeng,WenyongHuang,LifengShang,XinJiang,
andQunLiu.2023.Aligninglargelanguagemodelswithhuman:Asurvey.arXiv:2307.12966.Retrievedfrom
https://arxiv.org/abs/2307.12966
[319] ZhiruoWang,JunAraki,ZhengbaoJiang,Md.RizwanParvez,andGrahamNeubig.2023.Learningtofiltercontext
forretrieval-augmentedgeneration.arXiv:2311.08377.Retrievedfromhttps://arxiv.org/abs/2311.08377
[320] ZhenyiWang,XiaoyangWang,BangAn,DongYu,andChangyouChen.2020.Towardsfaithfulneuraltable-to-text
generationwithcontent-matchingconstraints.InProceedingsofthe58thAnnualMeetingoftheAssociationfor
ComputationalLinguistics.AssociationforComputationalLinguistics,1072–1086.DOI:https://doi.org/10.18653/v1/
2020.acl-main.101
[321] ZiruiWang,JiahuiYu,AdamsWeiYu,ZihangDai,YuliaTsvetkov,andYuanCao.2022.SimVLM:Simplevisual
languagemodelpretrainingwithweaksupervision.InProceedingsofthe10thInternationalConferenceonLearning
Representations(ICLR’22).OpenReview.net.Retrievedfromhttps://openreview.net/forum?id=GUrhfTuf_3
[322] JasonWei,XuezhiWang,DaleSchuurmans,MaartenBosma,FeiXia,EdChi,QuocV.Le,andDennyZhou.2022.
Chain-of-thoughtpromptingelicitsreasoninginlargelanguagemodels.InProceedingsofthe36thInternational
ConferenceonNeuralInformationProcessingSystems,24824–24837.
[323] JerryW.Wei,DaHuang,YifengLu,DennyZhou,andQuocV.Le.2023.Simplesyntheticdatareducessycophancy
inlargelanguagemodels.arXiv:2308.03958.Retrievedfromhttps://arxiv.org/abs/2308.03958
[324] Laura Weidinger, John Mellor, Maribeth Rauh, Conor Griffin, Jonathan Uesato, Po-Sen Huang, Myra Cheng,
MiaGlaese,BorjaBalle,AtoosaKasirzadeh,etal.2021.Ethicalandsocialrisksofharmfromlanguagemodels.
arXiv:2112.04359.Retrievedfromhttps://arxiv.org/abs/2112.04359
[325] YilinWen,ZifengWang,andJimengSun.2023.MindMap:Knowledgegraphpromptingsparksgraphofthoughtsin
largelanguagemodels.arXiv:2308.09729.Retrievedfromhttps://arxiv.org/abs/2308.09729
[326] DiWu,Jia-ChenGu,FanYin,NanyunPeng,andKai-WeiChang.2024.Synchronousfaithfulnessmonitoringfor
trustworthyretrieval-augmentedgeneration.arXiv:2406.13692.Retrievedfromhttps://arxiv.org/abs/2406.13692
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

42:52 L.Huangetal.
[327] KevinWu,EricWu,andJamesZou.2024.ClashEval:Quantifyingthetug-of-warbetweenanLLM’sinternalprior
andexternalevidence.arXiv:2404.10198.Retrievedfromhttps://arxiv.org/abs/2404.10198
[328] ShitaoXiao,ZhengLiu,PeitianZhang,andNiklasMuennighof.2023.C-Pack:Packagedresourcestoadvancegeneral
chineseembedding.arXiv:2309.07597.Retrievedfromhttps://arxiv.org/abs/2309.07597
[329] YijunXiaoandWilliamYangWang.2021.Onhallucinationandpredictiveuncertaintyinconditionallanguage
generation.InProceedingsofthe16thConferenceoftheEuropeanChapteroftheAssociationforComputational
Linguistics:MainVolume.AssociationforComputationalLinguistics,2734–2744.DOI:https://doi.org/10.18653/v1/
2021.eacl-main.236
[330] JianXie,KaiZhang,JiangjieChen,RenzeLou,andYuSu.2023.Adaptivechameleonorstubbornsloth:Unraveling
thebehavioroflargelanguagemodelsinknowledgeclashes.arXiv:2305.13300.Retrievedfromhttps://arxiv.org/abs/
2305.13300
[331] MiaoXiong,ZhiyuanHu,XinyangLu,YifeiLi,JieFu,JunxianHe,andBryanHooi.2023.CanLLMsexpress
theiruncertainty?AnempiricalevaluationofconfidenceelicitationinLLMs.arXiv:2306.13063.Retrievedfrom
https://arxiv.org/abs/2306.13063
[332] FangyuanXu,WeijiaShi,andEunsolChoi.2023.RECOMP:Improvingretrieval-augmentedLMswithcompression
andselectiveaugmentation.arXiv:2310.04408.Retrievedfromhttps://arxiv.org/abs/2310.04408
[333] JiachengXu,ShreyDesai,andGregDurrett.2020.Understandingneuralabstractivesummarizationmodelsviaun-
certainty.InProceedingsoftheConferenceonEmpiricalMethodsinNaturalLanguageProcessing(EMNLP).Association
forComputationalLinguistics,6275–6281.DOI:https://doi.org/10.18653/v1/2020.emnlp-main.508
[334] JundongXu,HaoFei,LiangmingPan,QianLiu,Mong-LiLee,andWynneHsu.2024.Faithfullogicalreasoningvia
symbolicchain-of-thought.arXiv:2405.18357.Retrievedfromhttps://arxiv.org/abs/2405.18357
[335] ShichengXu,DanyangHou,LiangPang,JingchengDeng,JunXu,HuaweiShen,andXueqiCheng.2023.AI-
generatedimagesintroduceinvisiblerelevancebiastotext-imageretrieval.arXiv:2311.14084.Retrievedfrom
https://arxiv.org/abs/2311.14084
[336] ShipingYang,RenliangSun,andXiaojunWan.2023.Anewbenchmarkandreversevalidationmethodforpassage-
levelhallucinationdetection.arXiv:2310.06498.Retrievedfromhttps://arxiv.org/abs/2310.06498
[337] Yuqing Yang, Ethan Chern, Xipeng Qiu, Graham Neubig, and Pengfei Liu. 2023. Alignment for honesty.
arXiv:2312.07000.Retrievedfromhttps://arxiv.org/abs/2312.07000
[338] ZhilinYang,ZihangDai,RuslanSalakhutdinov,andWilliamW.Cohen.2018.Breakingthesoftmaxbottleneck:
Ahigh-rankRNNlanguagemodel.InProceedingsofthe6thInternationalConferenceonLearningRepresentations
(ICLR’18).OpenReview.net.Retrievedfromhttps://openreview.net/forum?id=HkwZSG-CZ
[339] ZhilinYang,ThangLuong,RuslanSalakhutdinov,andQuocV.Le.2019.Mixtape:Breakingthesoftmaxbot-
tleneck efficiently. In Proceedings of the 33rd International Conference on Neural Information Processing Sys-
tems (NeurIPS ’19). Hanna M. Wallach, Hugo Larochelle, Alina Beygelzimer, Florence d’Alché-Buc, Emily B.
Fox, and Roman Garnett (Eds.), 15922–15930. Retrieved from https://proceedings.neurips.cc/paper/2019/hash/
512fc3c5227f637e41437c999a2d3169-Abstract.html
[340] ZhilinYang,PengQi,SaizhengZhang,YoshuaBengio,WilliamCohen,RuslanSalakhutdinov,andChristopher
D.Manning.2018.HotpotQA:Adatasetfordiverse,explainablemulti-hopquestionanswering.InProceedingsof
theConferenceonEmpiricalMethodsinNaturalLanguageProcessing.AssociationforComputationalLinguistics,
2369–2380.DOI:https://doi.org/10.18653/v1/D18-1259
[341] Jia-YuYao,Kun-PengNing,Zhen-HuiLiu,Mu-NanNing,andLiYuan.2023.LLMLies:Hallucinationsarenotbugs,
butfeaturesasadversarialexamples.arXiv:2310.01469.Retrievedfromhttps://arxiv.org/abs/2310.01469
[342] ShunyuYao,JeffreyZhao,DianYu,NanDu,IzhakShafran,KarthikNarasimhan,andYuanCao.2022.React:
Synergizingreasoningandactinginlanguagemodels.arXiv:2210.03629.Retrievedfromhttps://arxiv.org/abs/2210.
03629
[343] YunzhiYao,PengWang,BozhongTian,SiyuanCheng,ZhouboLi,ShuminDeng,HuajunChen,andNingyuZhang.
2023.Editinglargelanguagemodels:Problems,methods,andopportunities.arXiv:2305.13172.Retrievedfrom
https://arxiv.org/abs/2305.13172
[344] XiYe,RuoxiSun,SercanÖ.Arik,andTomasPfister.2023.Effectivelargelanguagemodeladaptationforimproved
grounding.arXiv:2311.09533.Retrievedfromhttps://arxiv.org/abs/2311.09533
[345] ShukangYin,ChaoyouFu,SiruiZhao,TongXu,HaoWang,DianboSui,YunhangShen,KeLi,XingSun,and
EnhongChen.2023.Woodpecker:Hallucinationcorrectionformultimodallargelanguagemodels.arXiv:2310.16045.
Retrievedfromhttps://arxiv.org/abs/2310.16045
[346] ZhangyueYin,QiushiSun,QipengGuo,JiawenWu,XipengQiu,andXuanjingHuang.2023.Dolargelanguage
modelsknowwhattheydon’tknow?InProceedingsoftheInternationalConferenceonFindingsoftheAssociationfor
ComputationalLinguistics(ACL’23).AnnaRogers,JordanL.Boyd-Graber,andNaoakiOkazaki(Eds.),Association
forComputationalLinguistics,8653–8665.DOI:https://doi.org/10.18653/V1/2023.FINDINGS-ACL.551
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

ASurveyonHallucinationinLargeLanguageModels 42:53
[347] ChanwoongYoon,GangwooKim,ByeonggukJeon,SungdongKim,YohanJo,andJaewooKang.2024.Askoptimal
questions:Aligninglargelanguagemodelswithretriever’spreferenceinconversationalsearch.arXiv:2402.11827.
Retrievedfromhttps://arxiv.org/abs/2402.11827
[348] OriYoran,TomerWolfson,OriRam,andJonathanBerant.2023.Makingretrieval-augmentedlanguagemodels
robusttoirrelevantcontext.arXiv:2310.01558.Retrievedfromhttps://arxiv.org/abs/2310.01558
[349] FangyiYu,LeeQuartey,andFrankSchilder.2022.Legalprompting:Teachingalanguagemodeltothinklikealawyer.
arXiv:2212.01326.Retrievedfromhttps://arxiv.org/abs/2212.01326
[350] FeiYu,HongboZhang,andBenyouWang.2023.Naturelanguagereasoning,asurvey.arXiv:2303.14725.Retrieved
fromhttps://arxiv.org/abs/2303.14725
[351] WeijiangYu,JianLiang,LeiJi,LuLi,YuejianFang,NongXiao,andNanDuan.2021.Hybridreasoningnetwork
forvideo-basedcommonsensecaptioning.InProceedingsofthe29thACMInternationalConferenceonMultimedia,
5213–5221.
[352] WeijiangYu,HaofanWang,GuohaoLi,NongXiao,andBernardGhanem.2023.Knowledge-awareglobalreasoning
forsituationrecognition.IEEETransactionsonPatternAnalysisandMachineIntelligence45,7(2023),8621–8633.
[353] WenhaoYu,HongmingZhang,XiaomanPan,KaixinMa,HongweiWang,andDongYu.2023.Chain-of-note:
Enhancingrobustnessinretrieval-augmentedlanguagemodels.arXiv:2311.09210.Retrievedfromhttps://arxiv.org/
abs/2311.09210
[354] WenhaoYu,ZhihanZhang,ZhenwenLiang,MengJiang,andAshishSabharwal.2023.Improvinglanguagemodels
viaplug-and-playretrievalfeedback.arXiv:2305.14002.Retrievedfromhttps://arxiv.org/abs/2305.14002
[355] WeizheYuan,GrahamNeubig,andPengfeiLiu.2021.BARTScore:Evaluatinggeneratedtextastextgeneration.In
Proceedingsofthe35thInternationalConferenceonNeuralInformationProcessingSystems(NeurIPS’21).Marc’Aurelio
Ranzato,AlinaBeygelzimer,YannN.Dauphin,PercyLiang,andJenniferWortmanVaughan(Eds.),27263–27277.
Retrievedfromhttps://proceedings.neurips.cc/paper/2021/hash/e4d2b6e6fdeca3e60e0f1a62fee3d9dd-Abstract.html
[356] RowanZellers,YonatanBisk,AliFarhadi,andYejinChoi.2019.Fromrecognitiontocognition:Visualcommonsense
reasoning.InProceedingsoftheIEEEConferenceonComputerVisionandPatternRecognition(CVPR’19).Computer
VisionFoundation/IEEE,6720–6731.DOI:https://doi.org/10.1109/CVPR.2019.00688
[357] BohanZhai,ShijiaYang,ChenfengXu,ShengShen,KurtKeutzer,andManlingLi.2023.Halle-switch:Controlling
objecthallucinationinlargevisionlanguagemodels.arXiv:2310.01779.Retrievedfromhttps://arxiv.org/abs/2310.
01779
[358] HanningZhang,ShizheDiao,YongLin,YiR.Fung,QingLian,XingyaoWang,YangyiChen,HengJi,andTong
Zhang.2023.R-Tuning:Teachinglargelanguagemodelstorefuseunknownquestions.arXiv:2311.09677.Retrieved
fromhttps://arxiv.org/abs/2311.09677
[359] HughZhang,DanielDuckworth,DaphneIppolito,andArvindNeelakantan.2021.Tradingoffdiversityandquality
innaturallanguagegeneration.InProceedingsoftheWorkshoponHumanEvaluationofNLPSystems(HumEval).
AssociationforComputationalLinguistics,25–33.Retrievedfromhttps://aclanthology.org/2021.humeval-1.3
[360] JiaxinZhang,ZhuohangLi,KamalikaDas,BradleyA.Malin,andSricharanKumar.2023.SAC3:Reliablehallucination
detectioninblack-boxlanguagemodelsviasemantic-awarecross-checkconsistency.arXiv:2311.01740.Retrieved
fromhttps://arxiv.org/abs/2311.01740
[361] JiajunZhang,YangZhao,HaoranLi,andChengqingZong.2018.Attentionwithsparsityregularizationforneural
machinetranslationandsummarization.IEEE/ACMTransactionsonAudio,Speech,andLanguageProcessing27,3
(2018),507–518.
[362] JingqingZhang,YaoZhao,MohammadSaleh,andPeterJ.Liu.2020.PEGASUS:Pre-trainingwithextractedgap-
sentencesforabstractivesummarization.InProceedingsofthe37thInternationalConferenceonMachineLearning(ICML
’20),ProceedingsofMachineLearningResearch,Vol.119,PMLR,11328–11339.Retrievedfromhttp://proceedings.
mlr.press/v119/zhang20ae.html
[363] MingtianZhang,ShawnLan,PeterHayes,andDavidBarber.2024.Mafin:Enhancingblack-boxembeddingswith
modelaugmentedfine-tuning.arXiv:2402.12177.Retrievedfromhttps://arxiv.org/abs/2402.12177
[364] MuruZhang,OfirPress,WilliamMerrill,AlisaLiu,andNoahA.Smith.2023.Howlanguagemodelhallucinations
cansnowball.arXiv:2305.13534.Retrievedfromhttps://arxiv.org/abs/2305.13534
[365] NingyuZhang,YunzhiYao,BozhongTian,PengWang,ShuminDeng,MengruWang,ZekunXi,ShengyuMao,
JintianZhang,YuanshengNi,etal.2024.Acomprehensivestudyofknowledgeeditingforlargelanguagemodels.
arXiv:2401.01286.Retrievedfromhttps://arxiv.org/abs/2401.01286
[366] ShengyuZhang,LinfengDong,XiaoyaLi,SenZhang,XiaofeiSun,ShuheWang,JiweiLi,RunyiHu,Tianwei
Zhang,FeiWu,etal.2023.Instructiontuningforlargelanguagemodels:Asurvey.arXiv:2308.10792.Retrievedfrom
https://arxiv.org/abs/2308.10792
[367] ShuoZhang,LiangmingPan,JunzhouZhao,andWilliamYangWang.2023.Mitigatinglanguagemodelhallucination
withinteractivequestion-knowledgealignment.arXiv:2305.13669.Retrievedfromhttps://arxiv.org/abs/2305.13669
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

42:54 L.Huangetal.
[368] SusanZhang,StephenRoller,NamanGoyal,MikelArtetxe,MoyaChen,ShuohuiChen,ChristopherDewan,Mona
T.Diab,XianLi,XiVictoriaLin,etal.2022.OPT:Openpre-trainedtransformerlanguagemodels.arXiv:2205.01068.
Retrievedfromhttps://arxiv.org/abs/2205.01068
[369] TianyiZhang,FaisalLadhak,EsinDurmus,PercyLiang,KathleenMcKeown,andTatsunoriBHashimoto.2023.
Benchmarkinglargelanguagemodelsfornewssummarization.arXiv:2301.13848.Retrievedfromhttps://arxiv.org/
abs/2301.13848
[370] TianhangZhang,LinQiu,QipengGuo,ChengDeng,YueZhang,ZhengZhang,ChenghuZhou,XinbingWang,
andLuoyiFu.2023.Enhancinguncertainty-basedhallucinationdetectionwithstrongerfocus.InProceedingsofthe
ConferenceonEmpiricalMethodsinNaturalLanguageProcessing(EMNLP’23).HoudaBouamor,JuanPino,andKalika
Bali(Eds.),AssociationforComputationalLinguistics,915–932.Retrievedfromhttps://aclanthology.org/2023.emnlp-
main.58
[371] XiaoyingZhang,BaolinPeng,YeTian,JingyanZhou,LifengJin,LinfengSong,HaitaoMi,andHelenMeng.2024.
Self-alignmentforfactuality:MitigatinghallucinationsinLLMsviaself-evaluation.arXiv:2402.09267.Retrievedfrom
https://arxiv.org/abs/2402.09267
[372] YueZhang,YafuLi,LeyangCui,DengCai,LemaoLiu,TingchenFu,XintingHuang,EnboZhao,YuZhang,Yulong
Chen,etal.2023.Siren’ssongintheAIocean:Asurveyonhallucinationinlargelanguagemodels.arXiv:2309.01219.
Retrievedfromhttps://arxiv.org/abs/2309.01219
[373] ZhenyuZhang,RunjinChen,ShiweiLiu,ZheweiYao,OlatunjiRuwase,BeidiChen,XiaoxiaWu,andZhangyang
Wang.2024.Foundinthemiddle:Howlanguagemodelsuselongcontextsbetterviaplug-and-playpositional
encoding.arXiv:2403.04797.
[374] ZihanZhang,MengFang,andLingChen.2024.RetrievalQA:Assessingadaptiveretrieval-augmentedgenerationfor
short-formopen-domainquestionanswering.arXiv:2402.16457.Retrievedfromhttps://arxiv.org/abs/2402.16457
[375] LinxiZhao,YiheDeng,WeitongZhang,andQuanquanGu.2024.Mitigatingobjecthallucinationinlargevision-
languagemodelsviaclassifier-freeguidance.arXiv:2402.08680.Retrievedfromhttps://arxiv.org/abs/2402.08680
[376] LiangZhao,XiaochengFeng,XiachongFeng,BingQin,andTingLiu.2023.Lengthextrapolationoftransformers:A
surveyfromtheperspectiveofpositionencoding.arXiv:2312.17044.Retrievedfromhttps://arxiv.org/abs/2312.17044
[377] RuochenZhao,XingxuanLi,ShafiqJoty,ChengweiQin,andLidongBing.2023.Verify-and-edit:Aknowledge-
enhancedchain-of-thoughtframework.InProceedingsofthe61stAnnualMeetingoftheAssociationforComputational
Linguistics(Volume1:LongPapers)(ACL’23).AnnaRogers,JordanL.Boyd-Graber,andNaoakiOkazaki(Eds.),
AssociationforComputationalLinguistics,5823–5840.DOI:https://doi.org/10.18653/v1/2023.acl-long.320
[378] WayneXinZhao,JingLiu,RuiyangRen,andJi-RongWen.2024.Densetextretrievalbasedonpretrainedlanguage
models:Asurvey.ACMTransactionsonInformationSystems42,4(2024),1–60.
[379] WayneXinZhao,KunZhou,JunyiLi,TianyiTang,XiaoleiWang,YupengHou,YingqianMin,BeichenZhang,
JunjieZhang,ZicanDong,etal.2023.Asurveyoflargelanguagemodels.arXiv:2303.18223.Retrievedfromhttps:
//arxiv.org/abs/2303.18223
[380] YukunZhao,LingyongYan,WeiweiSun,GuoliangXing,ChongMeng,ShuaiqiangWang,ZhicongCheng,Zhaochun
Ren, and Dawei Yin. 2023. Knowing what LLMs do not know: A simple yet effective self-detection method.
arXiv:2310.17918.Retrievedfromhttps://arxiv.org/abs/2310.17918
[381] Danna Zheng, Mirella Lapata, and Jeff Z. Pan. 2024. Large language models as reliable knowledge bases?
arXiv:2407.13578.Retrievedfromhttps://arxiv.org/abs/2407.13578
[382] ShenZheng,JieHuang,andKevinChen-ChuanChang.2023.WhydoesChatGPTfallshortinansweringquestions
faithfully?arXiv:2304.10513.Retrievedfromhttps://arxiv.org/abs/2304.10513
[383] WeihongZhong,MaoZheng,DuyuTang,XuanLuo,HengGong,XiaochengFeng,andBingQin.2023.STOA-VLP:
Spatial-temporalmodelingofobjectandactionforvideo-languagepre-training.InProceedingsofthe37thAAAI
ConferenceonArtificialIntelligenceand35thConferenceonInnovativeApplicationsofArtificialIntelligenceand30th
SymposiumonEducationalAdvancesinArtificialIntelligence,Vol.37,3715–3723.DOI:https://doi.org/10.1609/aaai.
v37i3.25483
[384] ChuntingZhou,PengfeiLiu,PuxinXu,SriniIyer,JiaoSun,YuningMao,XuezheMa,AviaEfrat,PingYu,LiliYu,
etal.2023.Lima:Lessismoreforalignment.arXiv:2305.11206.Retrievedfromhttps://arxiv.org/abs/2305.11206
[385] Chunting Zhou, Graham Neubig, Jiatao Gu, Mona Diab, Francisco Guzmán, Luke Zettlemoyer, and Marjan
Ghazvininejad.2021.Detectinghallucinatedcontentinconditionalneuralsequencegeneration.InProceedings
oftheInternationalConferenceonFindingsoftheAssociationforComputationalLinguistics(ACL-IJCNLP’21).Associ-
ationforComputationalLinguistics,1393–1404.DOI:https://doi.org/10.18653/v1/2021.findings-acl.120
[386] WenxuanZhou,ShengZhang,HoifungPoon,andMuhaoChen.2023.Context-faithfulpromptingforlargelanguage
models.InProceedingsoftheInternationalConferenceonFindingsoftheAssociationforComputationalLinguis-
tics(EMNLP’23).HoudaBouamor,JuanPino,andKalikaBali(Eds.),AssociationforComputationalLinguistics,
14544–14556.Retrievedfromhttps://aclanthology.org/2023.findings-emnlp.968
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.

ASurveyonHallucinationinLargeLanguageModels 42:55
[387] YiyangZhou,ChenhangCui,JaehongYoon,LinjunZhang,ZhunDeng,ChelseaFinn,MohitBansal,andHuaxiuYao.
2023.Analyzingandmitigatingobjecthallucinationinlargevision-languagemodels.arXiv:2310.00754.Retrieved
fromhttps://arxiv.org/abs/2310.00754
[388] DeyaoZhu,JunChen,XiaoqianShen,XiangLi,andMohamedElhoseiny.2023.Minigpt-4:Enhancingvision-language
understandingwithadvancedlargelanguagemodels.arXiv:2304.10592.Retrievedfromhttps://arxiv.org/abs/2304.
10592
[389] WenhaoZhu,HongyiLiu,QingxiuDong,JingjingXu,LingpengKong,JiajunChen,LeiLi,andShujianHuang.
2023.Multilingualmachinetranslationwithlargelanguagemodels:Empiricalresultsandanalysis.arXiv:2304.04675.
Retrievedfromhttps://arxiv.org/abs/2304.04675
[390] YutaoZhu,HuayingYuan,ShutingWang,JiongnanLiu,WenhanLiu,ChenlongDeng,ZhichengDou,andJi-
RongWen.2023.Largelanguagemodelsforinformationretrieval:Asurvey.arXiv:2308.07107.Retrievedfrom
https://arxiv.org/abs/2308.07107
[391] YongshuoZong,TingyangYu,BingchenZhao,RuchikaChavhan,andTimothyHospedales.2023.Foolyour(vision
and)languagemodelwithembarrassinglysimplepermutations.arXiv:2310.01651.Retrievedfromhttps://arxiv.org/
abs/2310.01651
Received8December2023;revised2August2024;accepted24September2024
ACMTransactionsonInformationSystems,Vol.43,No.2,Article42.Publicationdate:January2025.