PDF Download
3689776.pdf
01 March 2026
Total Citations: 12
. Total Downloads:
.
Latest updates: hps://dl.acm.org/doi/10.1145/3689776 1751
.
. . Publish . ed: 08 October 2024
RESEARCH-ARTICLE Accepted: 18 August 2024
Drowzee: Metamorphic Testing for Fact-Conflicting Received: 06 April 2024
.
Hallucination Detection in Large Language Models . Citation in BibTeX format
.
.
NINGKE LI, Huazhong University of Science and Technology, Wuhan,
Hubei, China
.
YUEKANG LI, UNSW Sydney, Sydney, NSW, Australia
.
YI LIU, Nanyang Technological University, Singapore City, Singapore
.
LING SHI, Nanyang Technological University, Singapore City, Singapore
.
KAILONG WANG, Huazhong University of Science and Technology,
Wuhan, Hubei, China
.
HAOYU WANG, Huazhong University of Science and Technology, Wuhan,
Hubei, China
.
.
.
Open Access Support provided by:
.
Huazhong University of Science and Technology
.
Nanyang Technological University
.
UNSW Sydney
.
Proceedings of the ACM on Programming Languages, Volume 8, Issue OOPSLA2 (October 2024)
hps://doi.org/10.1145/3689776
EISSN: 2475-1421
.

Drowzee: Metamorphic Testing for Fact-Conflicting
Hallucination Detection in Large Language Models
NINGKELI∗,
HuazhongUniversityofScienceandTechnology,China
YUEKANGLI∗,
TheUniversityofNewSouthWales,Australia
YILIU,
NanyangTechnologicalUniversity,Singapore
LINGSHI,
NanyangTechnologicalUniversity,Singapore
KAILONGWANG†,
HuazhongUniversityofScienceandTechnology,China
HAOYUWANG,
HuazhongUniversityofScienceandTechnology,China
Largelanguagemodels(LLMs)haverevolutionizedlanguageprocessing,butfacecriticalchallengeswith
security,privacy,andgeneratinghallucinations—coherentbutfactuallyinaccurateoutputs.Amajorissueis
fact-conflictinghallucination(FCH),whereLLMsproducecontentcontradictinggroundtruthfacts.Addressing
FCHisdifficultduetotwokeychallenges:1)Automaticallyconstructingandupdatingbenchmarkdatasetsis
hard,asexistingmethodsrelyonmanuallycuratedstaticbenchmarksthatcannotcoverthebroad,evolving
spectrumofFCHcases.2)ValidatingthereasoningbehindLLMoutputsisinherentlydifficult,especiallyfor
complexlogicalrelations.
Totacklethesechallenges,weintroduceanovellogic-programming-aidedmetamorphictestingtechnique
forFCHdetection.Wedevelopanextensiveandextensibleframeworkthatconstructsacomprehensive
factualknowledgebasebycrawlingsourceslikeWikipedia,seamlesslyintegratedintoDrowzee.Usinglogical
reasoningrules,wetransformandaugmentthisknowledgeintoalargesetoftestcaseswithgroundtruth
answers.WetestLLMsonthesecasesthroughtemplate-basedprompts,requiringthemtoprovidereasoned
answers.Tovalidatetheirreasoning,weproposetwosemantic-awareoraclesthatassessthesimilaritybetween
thesemanticstructuresoftheLLManswersandgroundtruth.Ourapproachautomaticallygeneratesusefultest
casesandidentifieshallucinationsacrosssixLLMswithinninedomains,withhallucinationratesrangingfrom
24.7%to59.8%.KeyfindingsincludeLLMsstrugglingwithtemporalconcepts,out-of-distributionknowledge,
andlackoflogicalreasoningcapabilities.Theresultsshowthatlogic-basedtestcasesgeneratedbyDrowzee
effectivelytriggeranddetecthallucinations.TofurthermitigatetheidentifiedFCHs,weexploredmodel
editingtechniques,whichprovedeffectiveonasmallscale(witheditstofewerthan1000knowledgepieces).
Ourfindingsemphasizetheneedforcontinuedcommunityeffortstodetectandmitigatemodelhallucinations.
CCSConcepts:•Softwareanditsengineering→Softwaretestinganddebugging.
AdditionalKeyWordsandPhrases:LargeLanguageModel,Hallucination,SoftwareTesting
∗NingkeLiandYuekangLiareco-firstauthors.
†KailongWangisthecorrespondingauthor.
Authors’ContactInformation:NingkeLi,HuazhongUniversityofScienceandTechnology,China,lnk_01@hust.edu.cn;
YuekangLi,TheUniversityofNewSouthWales,Australia,yuekang.li@unsw.edu.au;YiLiu,NanyangTechnological
University,Singapore,yi009@e.ntu.edu.sg;LingShi,NanyangTechnologicalUniversity,Singapore,ling.shi@ntu.edu.sg;
KailongWang,HuazhongUniversityofScienceandTechnology,China,wangkl@hust.edu.cn;HaoyuWang,Huazhong
UniversityofScienceandTechnology,China,haoyuwang@hust.edu.cn.
Permissiontomakedigitalorhardcopiesofallorpartofthisworkforpersonalorclassroomuseisgrantedwithoutfee
providedthatcopiesarenotmadeordistributedforprofitorcommercialadvantageandthatcopiesbearthisnoticeand
thefullcitationonthefirstpage.Copyrightsforthird-partycomponentsofthisworkmustbehonored.Forallotheruses,
contacttheowner/author(s).
©2024Copyrightheldbytheowner/author(s).
ACM2475-1421/2024/10-ART336
https://doi.org/10.1145/3689776
Proc.ACMProgram.Lang.,Vol.8,No.OOPSLA2,Article336.Publicationdate:October2024.

336:2 NingkeLi,YuekangLi,YiLiu,LingShi,KailongWang,andHaoyuWang
ACMReferenceFormat:
NingkeLi,YuekangLi,YiLiu,LingShi,KailongWang,andHaoyuWang.2024.Drowzee:Metamorphic
TestingforFact-ConflictingHallucinationDetectioninLargeLanguageModels.Proc.ACMProgram.Lang.8,
OOPSLA2,Article336(October2024),30pages.https://doi.org/10.1145/3689776
1 Introduction
LargeLanguageModels(LLMs)havebroughttransformativeadvancementstothefieldsoflanguage
processingandbeyond,showcasingexceptionalabilitiesintextgenerationandcomprehension
withwide-rangingapplications.However,despitetheirincreasingprevalence,LLMsfacecritical
challengesinsecurityandprivacyaspects[Houetal.2023;Kaddouretal.2023;SiddiqandSantos
2023;Xuetal.2024;Yangetal.2024a;Zhangetal.2024],heavilyimpactingtheireffectivenessand
reliability.Aparticularlynotableissueamongtheseisthephenomenonof“hallucination”,where
LLMsproducecoherentbutfactuallyinaccurateorirrelevantoutputsduringtaskslikeproblem-
solving.ThistendencytogeneratemisleadinginformationnotonlyjeopardizesthesafetyofLLM
applicationsbutalsoraisesserioususabilityconcerns.HallucinationsinLLMstakeseveralforms,
with“Fact-conflictinghallucination”(FCH)beingamajorconcernandtheprimarytypeofconcern
inthispaper.FCHismanifestedbyLLMsgeneratingcontentthatdirectlycontradictsestablished
facts,asexemplifiedinFigure1.WhenanLLMincorrectlybelieves“HarukiMurakamiwonthe
NobelPrizeinLiteraturein2016”,deviatingfromthecorrectanswerof“HarukiMurakamihasnot
wontheNobelPrizebutothernumerousawardsforhisworkinLiterature”.Suchmisinformation
disseminationleadstosignificantuserconfusion,erodingthetrustandreliabilitythatarecrucial
invariousLLMapplications.
Did Haruki Murakami (村上 春樹) ever win Nobel Did Haruki Murakami (村上 春樹) and Bob Dylan
Prize in Literature? ever win the same award?
Hallucination Answer: Yes. Haruki Murakami won the Hallucination Answer: Yes. They both have the
Nobel Prize in Literature in 2016. experience of winning the Nobel Prize in Literature.
Correct Answer: No. But he has received numerous Correct Answer: No. Haruki Murakami has won the
awards for his work, including the Gunzo Prize for the Gunzo Prize for the New Writers, the World Fantasy
New Writers, the World Fantasy Award, the Frank Award, ... While Bob Dylan has won the Presidential
O'Connor International Short Story Award, the Franz Medal of Freedom, ten Grammy Awards, a Golden
Kafka Prize, the Jerusalem Prize and the Princess of Globe Award, an Academy Award and the 2016 Nobel
Asturias Awards. Prize in Literature.
(a) Erroneous Knowledge Hallucination (b) Erroneous Inference Hallucination
Fig.1. AHallucinationOutputExample.
ToaddresstheissueofhallucinationsinLLMs,recentstudieshaveintroducedarangeofmethods
fortheirdetectionandtesting.Acommonandstraightforwardapproachinvolvescreatingextensive
benchmarkstailoredforthispurpose.DatasetssuchasTruthfulQA[Linetal.2022],HaluEval[Li
et al. 2023a], and KoLA [Yu et al. 2024] have been designed to evaluate hallucinations across
differentcontexts,includingquestion-answering,summarization,andknowledgegraphs.Despite
thevalueofthesemanuallylabeleddatasets,thecurrenttechniquesforhallucinationdetection
andtestingheavilyrelyonnaiveandsemi-automaticmethods,suchasstringmatching,manual
validation,orutilizinganotherLLMforconfirmation.ThiscurrentresearchlandscapeinLLM,
however,presentsacriticalgapinautomaticallyandeffectivelytestingFCHs.Themainobstaclein
testingforFCHistheabsenceofdedicatedgroundtruthdatasetsandspecifictestingframeworks.
Unlikeothertypesofhallucinations(e.g.,input-conflictingandcontext-conflictinghallucinations,
tobedetailedinSection2.1)whichcanbeidentifiedthroughchecksforsemanticconsistency,FCH
Proc.ACMProgram.Lang.,Vol.8,No.OOPSLA2,Article336.Publicationdate:October2024.

Drowzee:MetamorphicTestingforFact-ConflictingHallucinationDetectioninLargeLanguageModels 336:3
demandstheverificationofthecontent’sfactualaccuracyagainstexternalsourcesofknowledge
ordatabases.Thisrequirementmakestheprocessparticularlychallengingandresource-intensive,
especiallyfortasksprocessingcontentswithinherentlogicalconnections.
Bridgingtheidentifiedresearchgapintheliteraturenecessitatesanexplorationoftheinherent
challengesfacedindetectingFCHs,whicharecrucialforadvancingandenhancingthereliability
ofLLMs.Challenge#1:difficultyinautomaticallyconstructingandupdatingbenchmark
datasets.Predominantly,existingmethodologiesareanchoredtomanuallycuratedbenchmarks.
Whilethesebenchmarksareeffectiveindetectingcertaintypesofhallucinations,theyfallshort
inencompassingthebroadanddynamicspectrumoffact-conflictingscenariosinherenttoLLMs.
Meanwhile,theneedforfrequentupdatestobenchmarkdata,duetotheever-evolvingnatureof
knowledge,imposesasignificantandcontinuousmaintenanceeffort.Therelianceonbenchmark
datasets thus restricts the detection techniques’ adaptability, scalability, and worse, detection
capability.Challenge#2:difficultyinautomaticallyvalidatinganswersfromLLMoutputs.
EvenwhenLLMsproducecorrectfinalanswers,theoutputsmaynotrepresentthetruereasoning
processbehindthem,potentiallymaskingfalseunderstanding–asourceofFCHhallucination.
Automaticallyvalidatingthereasoningprocess,especiallythoseinvolvingcomplexlogicrelations,
isinherentlydifficult.Furthermore,theconsistencyinthequalityofbenchmarkquestionscanvary
duetothedifferinglevelsofexperienceandskillamonghumanexpertscreatingthem,introducing
noise,particularlyindatalabelingandresultvalidationstages.
Our Work. To address limitations in the existing techniques, we are the first, to the best of
ourknowledge,tointroduceanovelautomaticlogic-programming-aidedmetamorphictesting
techniqueforhallucinationdetectioninthiswork.Wehavedevelopedanextensiveandextensible
FCHtestingframework,whichisbasedonfactualknowledgereasoningandmetamorphictesting,
seamlesslyintegratedintoDrowzee1.
Drowzee begins by establishing a comprehensive factual knowledge base, sourced through
extensivecrawlingofinformationfromaccessibleknowledgebasessuchasWikipedia.Eachpiece
ofthisknowledgeactsasa“seed”forsubsequenttransformations.Leveraginglogicreasoning
relations,wetransformandaugmenttheseseeds,therebyexpandingthefactualknowledgeintoa
well-establishedsetofquestion-answerpairs.Usingthequestionsandanswersintheknowledge
setastestcasesandgroundtruthrespectively,weconstructareliableandrobustFCHtesting
benchmark.Thisisimplementedthroughaseriesofwell-formulatedtemplate-basedpromptsto
testFCHinLLMs.Specifically,weinstructtheLLMstogeneratetheiranswerstothetestcases.To
facilitateathoroughevaluationofthereasoninglogicbehindtheirresponses,werequiretheLLMs
toprovidedetailedjustificationsfortheiranswers.Foreffectiveanddependableidentificationof
FCH,weintroducetwosemantic-awareandsimilarity-basedmetamorphicoracles.Theseoracles
operate by extracting essential semantic elements from each sentence and mapping out their
logicalrelationships.Byassessingthesimilaritybetweentheconstructedlogicalandsemantic
structuresoftheLLM’sanswersandthegroundtruth,wecandetectFCHbypinpointinganswers
thatsignificantlydivergefromthegroundtruth.
ResultsandFindings.InevaluatingourproposedFCHtestingframeworkandDrowzee,we
undertakecomprehensiveexperimentstoevaluatetheireffectivenessinawidearrayofcontexts.
Ontheonehand,ourevaluationstrategyinvolvesdeployingDrowzeeacrossabroadspectrumof
topics,sourcedfromanextensiveanddiverserangeofWikipediaarticles.Ontheotherhand,we
examineourframeworkonavarietyofopen-sourceandcommercialLLMs,providingathorough
examinationofitsapplicabilityandperformanceacrossdifferentmodelarchitectures.
1DrowzeeisnamedafteraPokémon[SatoshiTajiri2023]characterthatnourishesitselfbyeatingdreams.Thisname
symbolizesourtool’scapabilitytodetectandpotentiallyfurtherassistineliminatingthehallucinationsinLLMs.
Proc.ACMProgram.Lang.,Vol.8,No.OOPSLA2,Article336.Publicationdate:October2024.

336:4 NingkeLi,YuekangLi,YiLiu,LingShi,KailongWang,andHaoyuWang
OurkeyfindingsindicatethatDrowzeesucceedsinautomaticallygeneratingusefultestcases
andidentifyinghallucinationissuesofsixLLMsacrossninedomains.Usingthesetestsets,we
findthathallucinationresponsesgeneratedbydifferentLLMscanvaryfrom24.7%to59.8%.We
thencategorizethesehallucinationresponsesintofourtypes.Throughanin-depthanalysis,we
unveilthatthelackoflogicalreasoningcapabilitiescontributesthemosttotheFCHissuesinLLMs.
Additionally,weobservethatLLMsareparticularlypronetogeneratinghallucinationsintestcases
involvingtemporalconceptsandout-of-distributionknowledge.Furthermore,weconfirmthattest
casesgeneratedusingourlogicalreasoningrulescaneffectivelytriggeranddetecthallucination
issuesinLLMs.Asmitigation,weinvestigatetheuseofmodeleditingtechniques[hiyouga2023;
Mengetal.2022]torectifytheidentifiedFCHs.Thesetechniqueshaveshownpromisingresults
whenappliedonasmallscale(involvingeditsuptolessthan1000piecesofknowledge).Ourresults
highlighttheimportanceofongoingeffortswithinthecommunitytodetectandaddressissuesof
hallucinationinLLMs.
Contributions.Wesummarizethemaincontributionsofthispaperbelow:
• DevelopmentofanovelFCHTestingFramework.Tothebestofourknowledge,weare
thefirsttodevelopanoveltestingframeworkbasedonlogicprogrammingandmetamorphic
testingtoautomaticallydetectFCHissuesinLLMs.
• ConstructionandReleaseofExtensiveFactualKnowledgeBaseandBenchmark.Our
workconstructsalarge-scalebenchmarkdataset[GitHub2024]tofacilitatecollaborative
effortsandfutureadvancementsinthedetectionofFCH.
• DesigningandImplementingInnovativeLogic-reasoning-basedMethodforData
Mutation. We propose and implement five unique logic reasoning rules to mutate and
augmenttheinitialseedsfromourknowledgebase,increasingthediversityandeffectiveness
ofourtestscenario.
• Deployment of FCH-specific semantic-aware testing oracles for automatic LLM
answervalidation.Weproposeandimplementtwoautomatedverificationmechanisms(or-
acles)thatanalyzethesemanticstructuresimilaritybetweensentences.Theseoraclesare
designed to validate the reasoning logic behind the answers generated by LLMs, hereby
reliablydetectingtheoccurrenceofFCHs.
2 Background
2.1 HallucinationCategorization
HallucinationinLLMscanbecategorizedintothreemaincategories[Huangetal.2023;Yaoetal.
2024;Zhangetal.2023],asdetailedbelow.
Input-Conflicting Hallucination: This type arises when LLMs produce outputs that are in-
consistentwiththeuser’sinput.Thisinconsistencycanoccurintwoways:eitherthemodel’s
responsecontradictsthetaskinstructions(reflectingamisunderstandingofuserintents)orthe
generatedcontentcontradictsthetaskinput(similartoconventionalissuesinmachinetranslation
andsummarization).AnexampleofthiswouldbeanLLMreplacingakeynameordetailina
summary,deviatingfromtheactualcontentprovidedbytheuser.
Context-ConflictingHallucination:Inthiscase,LLMsexhibitcontradictionsorinconsistencies
inlengthyormulti-turnresponses.Thishappenswhenmodelslosetrackofthecontextorfailto
maintainconsistencythroughouttheconversation.Limitationsinmaintaininglong-termmemory
oridentifyingrelevantcontextareoftentheculprits.Aninstanceofcontext-conflictinghallucination
couldinvolveLLMsswitchingreferencesbetweentwodifferentindividualsinaconversationabout
aspecifictopic.
Proc.ACMProgram.Lang.,Vol.8,No.OOPSLA2,Article336.Publicationdate:October2024.

Drowzee:MetamorphicTestingforFact-ConflictingHallucinationDetectioninLargeLanguageModels 336:5
Fact-ConflictingHallucination:Thistypeofhallucinationisthekeyfocusofthispaper.Itoccurs
whenLLMsgenerateinformationthatisindirectconflictwithestablishedworldknowledge.This
canbeduetovariousfactorsintroducedatdifferentstagesoftheLLMlifecycle.Forexample,as
showninFigure1,anLLMmightprovideincorrecthistoricalinformationinresponsetoauser’s
query,misleadinguserswhoarelessknowledgeableaboutthesubject.
Inthispaper,ourprimaryfocusisonfact-conflictinghallucinations,atypeoferrorthatcarries
thepotentialformoreseriousconsequencesbymisleadingusers.
2.2 LogicProgramming
|                         | World Descriptions |                          | Queries |     |           | World Descriptions                          |                                    | Queries |     |
| ----------------------- | ------------------ | ------------------------ | ------- | --- | --------- | ------------------------------------------- | ---------------------------------- | ------- | --- |
|                         | Facts              |                          |         |     |           | Facts                                       |                                    |         |     |
|                         |                    |                          |         |     | H a r u   | k iM u r a ka m i A w a r ds   =  [ G u nzo |                                    |         |     |
| bigger(elephant, horse) | >                  |                          |         |     | Pr i z e, |  W o rl d  F a nt a s y  A w a r d ,  ... ] |                                    |         |     |
|                         |                    |                          |         |     | B o b D   | y la n A w ards = [Nobel Prize in           |                                    |         |     |
| bigger(horse, cat)      | >                  | ?- bigger(elephant, cat) |         | > ? |           |                                             | ?-                                 |         |     |
|                         |                    |                          |         |     | Li t er   | a tu r e , . ..]                            | same_member(HarukiMurakamiAwards , |         |     |
|                         | Rules              |                          |         | ?   |           | Rules                                       |                                    |         |     |
|                         |                    | ?- bigger(cat, elephant) |         | >   |           |                                             | BobDylanAwards)                    |         |     |
same_member(List1, List2) =
| bigger(X,Z):- bigger(X,Y), bigger(Y,Z) |     |     |     |     | member(Element, List1), |     |     |     |     |
| -------------------------------------- | --- | --- | --- | --- | ----------------------- | --- | --- | --- | --- |
member(Element, List2)
|     | Logic Reasoning Engine |                       |           |     |     | Logic Reasoning Engine |                                     |           |     |
| --- | ---------------------- | --------------------- | --------- | --- | --- | ---------------------- | ----------------------------------- | --------- | --- |
|     | Yes.                   |                       |           | >   |     |                        | ¬same_member(HarukiMurakamiAwards , |           |     |
|     | No.                    | bigger(elephant, cat) |           |     |     | No.                    | BobDylanAwards)                     |           |     |
|     | Answers                |                       | New Facts |     |     | Answers                |                                     | New Facts |     |
(a) The animal size comparison example (b) The prize comparison example
|     |     |     | Fig.2. | ExamplesofLogicProgramming. |     |     |     |     |     |
| --- | --- | --- | ------ | --------------------------- | --- | --- | --- | --- | --- |
Someexistingworks[Olaussonetal.2023;Panetal.2023;Yeetal.2023]havealreadyintegrated
logicalprogrammingwithlargelanguagemodelsinanattempttoenhancetheirlogicalreasoning
capabilities.Inthiswork,wefocusonleveraginglogicalprogrammingtoautomatethetesting
ofhallucinationsinLLMs.Logicprogramminglanguagesaredeclarative,i.e.,programmingwith
theselanguagesmeansdescribingtheworld.Usingtheprogramsmeansaskingquestionsabout
thepreviouslydescribedworld.Basedontheanswerstothequestionsfromthelogicreasoning
engine,accordingtotheworlddescription,wecanderivenewfacts.Figure2showsanexampleof
howlogicprogrammingworks.
Logicprogrammingallowstheprogrammertospecifytherulesandfacts,enablingtheProlog
interpretertoinferanswerstothegivenqueriesautomatically.Hereweexplainsomekeyconcepts:
Program.APrologprogramconsistsoftwoparts:alistoffacts(𝑅 (cid:101))andalistofrules(𝑄
(cid:101)).Throughout
thepaper,weusetheover-tildenotationtodenotealistofitems.Forexample,e(cid:157)ntityreferstoalist
,...,entity
| ofentities,i.e.,entity |     |     | 𝑛 . |     |     |     |     |     |     |
| ---------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
1
|     |     |     | (Program) | P   | ::= | 𝑅 (cid:101)++𝑄 (cid:101) |     |     | (1) |
| --- | --- | --- | --------- | --- | --- | ------------------------ | --- | --- | --- |
Facts.Afactisastatementdefiningarelationasbeingtrue.Itismadeupofa𝑝𝑟𝑒𝑑𝑖𝑐𝑎𝑡𝑒andseveral
𝑒𝑛𝑡𝑖𝑡𝑖𝑒𝑠.Itisdenotedas:
|     |     |     | (Predicate) | 𝑅   | ::= nm(e(cid:157)ntity) |     |     |     |     |
| --- | --- | --- | ----------- | --- | ----------------------- | --- | --- | --- | --- |
(2)
Anexampleis𝑏𝑖𝑔𝑔𝑒𝑟(ℎ𝑜𝑟𝑠𝑒,𝑐𝑎𝑡),whichmeanshorsesarebiggerthancats.Anotherexampleis
𝑚𝑒𝑚𝑏𝑒𝑟(𝐺𝑢𝑛𝑧𝑜𝑃𝑟𝑖𝑧𝑒,𝐻𝑎𝑟𝑢𝑘𝑖𝑀𝑢𝑟𝑎𝑘𝑎𝑚𝑖𝐴𝑤𝑎𝑟𝑑𝑠),whichmeansthattheGunzonPrizeisinthelist
ofprizesawardedtoHarukiMurakami.
Proc.ACMProgram.Lang.,Vol.8,No.OOPSLA2,Article336.Publicationdate:October2024.

336:6 NingkeLi,YuekangLi,YiLiu,LingShi,KailongWang,andHaoyuWang
Rules.APrologruleisaHornclausethatcomprisesaheadpredicateandalistofbodypredicates
placedontheleftandrightsideofthearrowsymbol(:–).Arulemeansthattheleft-handsideis
logicallyimpliedbytheright-handside.Therulebodiesareeitherpositiveornegativerelations,
correspondingtotherequirementsuponthepresenceorabsenceoffacts.Weuse“𝑅”and“¬𝑅”as
abbreviationsfor“Pos𝑅”and“Neg𝑅”,respectively.Itisdenotedas:
(Rule) Q ::= 𝑅 :–𝑏 (cid:157) 𝑜𝑑𝑦
(3)
(RuleBodies)body ::= Pos𝑅 | Neg𝑅
Anexampleisbigger(X,Z):–bigger(X,Y),bigger(Y,Z),whichmeansthe𝑏𝑖𝑔𝑔𝑒𝑟 relationistransi-
tive.Anotherexampleissmaller(X,Y):–bigger(Y,X),whichmeans𝑠𝑚𝑎𝑙𝑙𝑒𝑟 isaninverserelation
of𝑏𝑖𝑔𝑔𝑒𝑟.Thelastexamplehereissame_member(List1,List2),whichis𝑡𝑟𝑢𝑒 ifthereexistsatleast
one 𝐸𝑙𝑒𝑚𝑒𝑛𝑡 that is a member of both 𝐿𝑖𝑠𝑡1 and 𝐿𝑖𝑠𝑡2. It is a composite type of two𝑚𝑒𝑚𝑏𝑒𝑟
predicates.
Queries.Aqueryhasthesamestructureasthebodyofarule,i.e.,itisasequenceofpredicates
separatedbycommasandexecutedagainstadatabaseoffacts.Thelogicreasoningenginewill
answer𝑌𝑒𝑠 if the sequence of predicates in the query is𝑇𝑟𝑢𝑒 according to the facts and rules.
Otherwise,itwillanswer𝑁𝑜.
Anexamplequeryis?-bigger(elephant,cat),whichmeansaskingthelogicreasoningengine
whetherelephantsarebiggerthancats.Anotherexampleis?-𝑠𝑎𝑚𝑒_𝑚𝑒𝑚𝑏𝑒𝑟(𝐻𝑎𝑟𝑢𝑘𝑖𝑀𝑢𝑟𝑎𝑘𝑎𝑚𝑖
𝐴𝑤𝑎𝑟𝑑𝑠,𝐵𝑜𝑏𝐷𝑦𝑙𝑎𝑛𝐴𝑤𝑎𝑟𝑑𝑠),whichmeansaskingiftheawardswonbyHarukiMurakamiandBob
Dylanhaveoverlapped.
ReasoningRules.AsshowninFigure2,generatingnewfactsthroughlogicprogrammingrequires
facts(Equation(2)),rules(Equation(3)),queries,andanswerstothequeries.Tosimplifythenotation
ofthisprocess,webringuptheconceptofreasoningrulesinthispaper,whichdescribestheinference
processofusingfactsandrules(predicates)toreachtheconclusion(anewfactintheformofa
predicate)byomittingtheprocessofqueryingandanalyzingthequeryanswers.Areasoningrule
isdenotedinthisform:
𝑅 ,𝑅 ,...
1 2
(4)
𝑅
new
3 MotivatingExample
Figure 3 shows a motivating example of Drowzee. Assume we have the facts about whether
HarukiMurakamiandBobDylanhavewontheNobelPrize,asillustratedintheleftsub-figure.The
questiontoaskLLMsisstraightforward:WecanaskwhetherHarukiMurakami/BobDylanhaswon
theNobelPrizeornot.Askingandverifyingthisknowledgerequiresnologicreasoning.However,
thestraightforwardquestionsareoftennotenoughtounveilhallucinations.Therefore,more
diversifiedquestions(questionswithintertwinedandcomplexinformation,asillustrated
intherightsub-figure)areneeded.
Inordertogeneratemorediversifiedbenchmarks,previousresearch[Lietal.2023a;Yuetal.
2024]involveshumanexpertstogeneratethequestionsandannotatetheanswersforhallucination
checking.Althoughthemanuallygeneratedbenchmarkscanunveilcertainhallucinations,they
suffer from several drawbacks. The landscape of knowledge is dynamic, with new infor-
mationcontinuouslysurfacingandolderinformationbecomingobsolete.Iffactschange
continuouslyovertime,forinstanceHarukiMurakamiweretowintheNobelPrizeinthefuture,
thiswouldnecessitateregularupdatesandcorrectionstothegroundtruthinexistingdatasets
toreflectthem.However,maintainingtheaccuracyofthesebenchmarksdemandsasignificant
amountofmanuallabor.Additionally,thequalityofthequestionsmightbeinconsistentduetothe
Proc.ACMProgram.Lang.,Vol.8,No.OOPSLA2,Article336.Publicationdate:October2024.

Drowzee:MetamorphicTestingforFact-ConflictingHallucinationDetectioninLargeLanguageModels 336:7
Did Haruki Murakami (村上 Thinking: What if Did Haruki Murakami (村上 Challenge-1: How to
春樹) and Bob Dylan ever win
春樹) ever win Nobel Prize in Haruki Murakami automatically generate such
Literature? wins Nobel Prize in the same award? questions? How to generate
|                            | Literature one day? |     |                            | the ground truth paired with |     |
| -------------------------- | ------------------- | --- | -------------------------- | ---------------------------- | --- |
|                            | The QA pairs in the |     | Hallucination Answer: Yes. | the generated questions?     |     |
| Correct Answer: No. But he | dataset should      |     | Haruki Murakami and Bob    |                              |     |
has received numerous awards Dylan both have the experience We use logic programming
|                             | change.But      |     |                            | to generate logically sound |     |
| --------------------------- | --------------- | --- | -------------------------- | --------------------------- | --- |
| for his work, including the | knowledge keeps |     | of winning the same award. |                             |     |
Gunzo Prize for the New changing nowadays ... The key knowledge points are: new facts based on existing
Writers, the World Fantasy 1. Haruki Murakami is a ones. And then based on the
Award, the Frank O'Connor We need to develop methods Japanese author known for his new facts (ground truth), we
International Short Story to create evaluation datasets works such as "Norweigian can generate new questions.
Award, the Franz Kafka Prize,
|                             | INSTEAD OF just building |     | Wood".                      | Challenge-2: How can we |     |
| --------------------------- | ------------------------ | --- | --------------------------- | ----------------------- | --- |
| the Jerusalem Prize and the | the datasets manually.   |     | 2. Bob Dylan is an American |                         |     |
Princess of Asturias Awards. singer-songwriter and know that the LLM is
responding with a
|     | Thinking: Questions   |     | musician, renowned for his      | hallucinating answer? What |     |
| --- | --------------------- | --- | ------------------------------- | -------------------------- | --- |
|     | directly derived from |     | contributions to folks and rock |                            |     |
Did Bob Dylan ever win existing facts are too simple. music. is the test oracle?
Nobel Prize in Literature?
|     | They may not fully expose |     | 3. Haruki Murakami was     | We leverage the |     |
| --- | ------------------------- | --- | -------------------------- | --------------- | --- |
|     | the limitations of LLMs.  |     | awarded the Nobel Prize in |                 |     |
metamorphic relations
Correct Answer: Yes. He won We need to come up with Literature in 2017, while Bob between the ground truth and
the Nobel Prize in Litertature more complex questions Dylan received the same the LLM response content to
| in 2016. |                          |     | award in 2016. |                     |     |
| -------- | ------------------------ | --- | -------------- | ------------------- | --- |
|          | based on existing facts. |     |                | build test oracles. |     |
Fig.3. MotivatingExample.
differencesintheexperienceandskillsofthehumanexpertswhocreatethem.Consequently,the
efficiencyandsoundnessofthemanuallygeneratedbenchmarksarenotguaranteed.
Thelimitationsofthemanuallygeneratedbenchmarksmotivatetheneedforanautomatedtech-
niquetotestforhallucinationsinLLMs.Nevertheless,automaticallygeneratingdiversebenchmarks
ischallenging.First,generatingsuitableandvalidquestionsischallenging(challenge#1).
Whileitisimportantforthequestionsinthetestingbenchmarktocoveradiverserangeofscenarios,
theycannotberandomlygeneratedorarbitrarilyselected.Instead,thequestionsmustbelogically
coherentandalignedwithwell-establishedfactualknowledgeandgroundtruth.Second,deriving
thetestoraclesfordetectinghallucinationsischallenging(challenge#2).TheLLM’sanswer
istypicallyexpressedinlengthyandpotentiallycomplexsentences.Thekeytodeterminingif
anLLMhasproducedanFCHliesinassessingwhethertheoveralllogicalreasoningbehindits
answerisconsistentwiththeestablishedgroundtruth.Automaticallyanalyzingandcomparing
theintricatelogicalstructureswithintheLLM’sresponseandthefactualgroundtruthremainsan
inherentlydifficulttask.
Thesetwochallengescanbothbeaddressedbyleveraginglogicprogramming.Wecanderive
newlogicallysoundfactsbasedonexistingknowledge.Withthenewfacts,wecanthengenerate
diversequestionsandtheirgroundtruthanswers.Withthegroundtruthanswers,wecangenerate
testoraclestocapturehallucinations.Inshort,theideaofusinglogicprogrammingtotacklethe
| challengesmotivatesthedesignof |     | Drowzee. |     |     |     |
| ------------------------------ | --- | -------- | --- | --- | --- |
4 Methodology
WedesignandimplementDrowzeetoaddresstheaforementionedchallenges,theworkflowof
whichisillustratedinFigure4.Drowzeeiscomprisedofthefollowingfourmodules,witheach
moduletobedetailedlater.
| Factual Knowledge | Extraction | (§4.1): |               |                    |        |
| ----------------- | ---------- | ------- | ------------- | ------------------ | ------ |
| •                 |            | Based   | on voluminous | knowledge database | dumps, |
Drowzeeacquiresfundamentalinformationandfactualtriplesofvalidentities.
• LogicalReasoning(§4.2):Inthismodule,Drowzeeleveragesreasoningrulestogeneratesound
anddiversefactsasnewgroundtruthknowledge.
• BenchmarkConstruction(§4.3):Thismodulefocusesoncreatinghigh-qualitytestcase-oracle
pairsfromthenewly-derivedgroundtruthknowledge.Thetestoraclesaregeneratedbased
Proc.ACMProgram.Lang.,Vol.8,No.OOPSLA2,Article336.Publicationdate:October2024.

336:8 NingkeLi,YuekangLi,YiLiu,LingShi,KailongWang,andHaoyuWang
onasimpleyeteffectivemetamorphicrelation:Sincethenewlygeneratedknowledgeissound,
the questions complying with the knowledge should be answered with “YES” and the questions
contraveningtheknowledgeshouldbeansweredwith“NO”.Thismodulealsoincludesstrategies
foreffectivelyandreliablygeneratingorselectingpromptsforinteractionwithLLMs.
• ResponseEvaluation(§4.4):ThefinalmoduleevaluatestheresponsesfromtheLLMsand
detectsfactualconsistencyautomatically.ItfirstparsesLLMoutputsusingNLPtoconstruct
semantic-awarestructures,thenevaluatestheirsemanticsimilaritytogroundtruth.Subsequently,
itdevelopssimilarity-basedoraclesapplyingmetamorphictestingtoassessconsistencybetween
LLMresponsesandgroundtruth.
Fact Triples Drowzee Output
(Haruki Murakami, win_awards, [Gunzo Prize, Hallucination Revealing Prompts
(Bob Dylan, win_aw .. a .] r ) ds, [Nobel Prize, ...]) §4.2 Logic Reasoning Given the question: Now given the question:
... Did Haruki Murakami and Bob Dylan ever win
the same award? please provide an answer with
Derive New Facrs your knowledge and reasoning power. Think of
it step by step with a human-like reasoning
(Haruki Murakami, ¬same_awards, Bob process. After giving the answer, list the
§4.1Factual Knowledge Extraction Dylan) knowledge used in your reasoning process in
... the form of declarative sentences and point by
point. Here is an example ...
Knowledge Data
Haruki Murakami (村上 春樹, born January
12, 1949) is a Japanese writer. His novels, §4.3 Benchmark Construction §4.4 Response Evaluation
essays, and short stories have been best-sellers
in Japan and internationally, with his work
translated into 50 languages. He has received
numerous awards for his work, including the Prompts LLM Answers
Gunzo Prize for New Writers, ... T pl e e m as p e l a p t r e o : v N id o e w a g n i v an en sw th e e r w qu it e h s t y io o n u : r { k q n u o e w st l i e o d n g } e , Target LLM YES. <Reasoning>
Input and reasoning power ...
Fig.4. TheWorkflowofDrowzee.*Theavatarispaintedbyoneoftheauthorstoavoidcopyrightissues.
4.1 FactualKnowledgeExtraction
Thisstepaimstoextractfundamentalfactsfromtheinputknowledgedataintofacttriplesthatcan
beutilizedforlogicalreasoning.
Existingknowledgedatabases[Aueretal.2007;Bollackeretal.2007;Miller1995;Suchaneketal.
2007]notonlyencompassavastarrayofdocumentsandpagesbutalsoprovideavailablestructured
data.Extractedfromknowledgedatabases,thestructureddatawouldbecomeanidealresource
fortheconstructionandenrichmentoffactualknowledge.Thus,thegenesisofourtestcasedata
isexclusivelyrootedintheentitiesandstructuredinformationsourcedfromcurrentknowledge
databases, ensuring a sophisticated and well-informed foundation for our testing framework.
Basically,wefollowthecategorizationofentitiesandrelationsusedbyWikiPedia[Aueretal.2007]
toperformtheidentification.Figure5ashowsthecategoriesoftheentities.Figure5bshowsthe
categoriesoftherelationsandsomeexamplefacttriples.
ThedetailedprocessisoutlinedinAlgorithm1.AsdefinedinthepreviousEquation2,weextract
thefactsinthestructureofthree-elementpredicates,i.e.,nm(𝑠,𝑜),where“𝑠”(standsforsubject)
and“𝑜”(standsforobject)areentities,and“nm”isthenameofthepredicate.Thefactsextraction
isdoneonaper-categorybasis,implementingadivide-and-conquerstrategy,whichefficiently
integratesallthefactsrangingfromallthecategories.AsshowninAlgorithm1,foranygiven
entity category and relation category, the function ExtractGroundFacts iterates through all
possibleentitiesandrelations.Foreachcombination(entity,nm),itqueriesthedatabaseusingthe
QueryDBfunction(Lines3-6),whichretrievesallthree-elementfactsestablishedwiththespecific
predicatenmandtheargumententityplacedeitherinthesubjectortheobjectposition.
Proc.ACMProgram.Lang.,Vol.8,No.OOPSLA2,Article336.Publicationdate:October2024.

Drowzee:MetamorphicTestingforFact-ConflictingHallucinationDetectioninLargeLanguageModels 336:9
| CategoryType |     | Description |     |     |     |     |
| ------------ | --- | ----------- | --- | --- | --- | --- |
CultureandtheArts
Famousfilms,books,etc.
GeographyandPlaces
Countries,citiesandlocations.
HealthandFitness
Diseasesanddisease-causinggenes.
| HistoryandEvents |     |     | CategoryType | Example |     |     |
| ---------------- | --- | --- | ------------ | ------- | --- | --- |
Famoushistoricalevents,etc.
|     |     |     | NounPhrase | p la c e | _ o f _ bi rt h ( B a r a | ck O b a m a ,H onolulu). |
| --- | --- | --- | ---------- | -------- | ------------------------- | ------------------------- |
PeopleandSelf Importantfiguresandcontributors. ge n r e ( 2 8 D a y s L a t e r, ho rr o r fi lm ).
MathematicsandLogic Commonformulasandtheorems. killed_by(JohnF.Kennedy,LeeHarveyOswald).
VerbPhraseinPassiveVoice
NaturalandPhysicalSciences Celestialbodiesandastronomy. located_in_time_zone(Arizona,UTC-07:00).
SocietyandSocialSciences Majorsocialinstitutions,etc. follows(4769Castalia,4768Hartley).
|     |     |     | VerbPhraseinActiveVoice | replaces(AmericanBroadcastingCompany, |     |     |
| --- | --- | --- | ----------------------- | ------------------------------------- | --- | --- |
TechnologyandAppliedSciences Computerscience,etc. NBCBlueNetwork).
|     | (a)EntityCategorization. |     | (b)RelationCategorization. |     |     |     |
| --- | ------------------------ | --- | -------------------------- | --- | --- | --- |
Fig.5. EntityandRelationCategorization.
Algorithm1FactsExtraction
Require:
EntityCategory(EC),RelationCategory(RC)
Ensure: GroundFacts(𝑅
(cid:101)ground )
1: functionExtractGroundFacts(EC,RC)
| 2:  | 𝑅 ← | []  |     |     |     | ⊲Initialization |
| --- | --- | --- | --- | --- | --- | --------------- |
(cid:101)ground
|     | forentity∈EC | do  |     |     | ⊲Iterateovereachentity |     |
| --- | ------------ | --- | --- | --- | ---------------------- | --- |
3:
|     | fornm∈RC | do  |     |     | ⊲Iterateovereachrelation |     |
| --- | -------- | --- | --- | --- | ------------------------ | --- |
4:
|     | 𝑅                            |     |     |     | ⊲Retrivegroundfacts |     |
| --- | ---------------------------- | --- | --- | --- | ------------------- | --- |
| 5:  | (cid:101)←QueryDB(entity,nm) |     |     |     |                     |     |
6: 𝑅 (cid:101)ground .append(𝑅 (cid:101)) ⊲Extendthegroundfacts
| 7:  | return𝑅 (cid:101)ground |     |     |     | ⊲Returnthegroundfacts |     |
| --- | ----------------------- | --- | --- | --- | --------------------- | --- |
4.2 LogicalReasoning
Thisstepaimstoderiveadditional,enrichedinformationfrompreviouslyextractedfactualknowl-
edge.Drowzeeusesalogicalprogramming-basedprocessortoautomaticallygeneratenewfactual
knowledge.Thisallowsustotakeoneormorefactualknowledgetriplesasinputandgeneratea
derivedtripleasoutputwithfivetypesofinferencerules.
TotackletheprimaryconcernofgeneratingFCHtestcaseswithvariability,wedesignfivetypes
ofreasoningrules(Equation(4))prevalentlyadoptedinseveralliterature[Abboudetal.2020;Liang
etal.2022;RenandLeskovec2020;Tianetal.2022;Zhouetal.2019]inthecontextofknowledge
reasoning.Thisprovidessoundstrategiestopreparenewfactsforfurthertestcasegeneration.
Drowzeewillexhaustivelyapplyalltherulestoalltheirrelevantfacttriplestogeneratenew
knowledge.Thedefinitionsofthefivetypesofrulesaredetailedasfollows.
Rule#1:NegationReasoning.Basedonagivenfactualknowledge,wecandeterminewhetherthe
oppositeofthisfactiscorrectorincorrectbyapplyingDefinition1.
|              |     |                       | [𝑁𝑒𝑔].Givenafactualknowledgetriple |     |     | (𝑠,nm,𝑜), |
| ------------ | --- | --------------------- | ---------------------------------- | --- | --- | --------- |
| Definition1. |     | NegationReasoningRule |                                    |     |     |           |
thenwecanderivethenewtriple(𝑠,nm,𝑜)isnotvalid.nmindicatesthenegationoftherelationnm.
nm(𝑠,𝑜)
[𝑁𝑒𝑔]
¬nm(𝑠,𝑜)
was(𝑠,𝑜)
| Anexampleofthistypeofruleis: |     |     | [𝑁𝑒𝑔]. |     |     |     |
| ---------------------------- | --- | --- | ------ | --- | --- | --- |
¬wasn′t(𝑠,𝑜)
Proc.ACMProgram.Lang.,Vol.8,No.OOPSLA2,Article336.Publicationdate:October2024.

336:10 NingkeLi,YuekangLi,YiLiu,LingShi,KailongWang,andHaoyuWang
Withthisrule,fromthetriple(HarukiMurakami,won,theNobelPrizeinLiteraturein2016),we
derivethatthenegationofthistriple(HarukiMurakami,didnotwin,theNobelPrizeinLiteraturein
2016)containsfalsefactualknowledge.
Rule#2:SymmetricReasoning.Insymmetricrelations,ifthesubjectandobjectinatriplemaintain
coherenceuponinterchange,anewtriplecanbededucedinaccordancewithDefinition2.
[𝑆𝑦𝑚].Givenafactualknowledgetriple(𝑠,nm,𝑜),
| Definition2. | SymmetricReasoningRule |     |     |     |     |
| ------------ | ---------------------- | --- | --- | --- | --- |
thenwecanderiveanewtriple(𝑜,nm,𝑠).
nm(𝑠,𝑜)
[𝑆𝑦𝑚]
nm(𝑜,𝑠)
different_from(𝑠,𝑜)
| Anexampleofthistypeofruleis: |     |     |     |     | [𝑆𝑦𝑚]. |
| ---------------------------- | --- | --- | --- | --- | ------ |
different_from(𝑜,𝑠)
Withthisrule,fromtheoriginaltriple(HarukiMurakami,different_from,HarukiUemura),we
deriveanewtriple(HarukiUemura,different_from,HarukiMurakami)(HarukiUemuraisaJapanese
judoka). Note that the symmetric reasoning rule is primarily utilized within the composition
reasoningrule(tobedetailednext)anddoesnotintroducenewknowledgeonitsown.
Rule#3:InverseReasoning.Inaninverserelation,thesubjectandobjectcanbereverselylinked
throughavariantoftheoriginalrelation,asdefinedinDefinition3.
Definition3. InverseReasoningRule [𝐼𝑛𝑣𝑒𝑟𝑠𝑒].Givenafactualknowledgetriple (𝑠,nm,𝑜)
andareversedrelationnm′ of𝑅,thenwecanderiveanewtriple(𝑜,nm′,𝑠).
|     |     | nm(𝑠,𝑜),nm′ | =𝑅𝑒𝑣𝑒𝑟𝑠𝑒(nm) |     |     |
| --- | --- | ----------- | ------------ | --- | --- |
[𝐼𝑛𝑣𝑒𝑟𝑠𝑒]
nm′(𝑜,𝑠)
influence_by(𝑠,𝑜)
Anexampleofthistypeofruleis: [𝐼𝑛𝑣𝑒𝑟𝑠𝑒].Withthisrule,fromthetriple
influence(𝑜,𝑠)
(HarukiMurakami,influence_by,RichardBrautigan),wecanderiveanewtriple(RichardBrautigan,
influence,HarukiMurakami).
Rule#4:TransitiveReasoning.Intransitiverelations,iftheobjectinonetripleisthesubjectof
thesecondtriple,wecanthereforederiveanewtriplefollowingtheDefinition4.
Definition 4. Transitive Reasoning Rules [𝑇𝑟𝑎𝑛𝑠]. Given two factual knowledge triples
| (𝑠 ,nm,𝑜 | (𝑠 ,nm,𝑜 | ),if𝑜 | issemanticallyequivalentto𝑠 |     |                            |
| -------- | -------- | ----- | --------------------------- | --- | -------------------------- |
| )        | and      |       |                             |     | ,thenwecanderiveanewtriple |
| 1 1      | 2        | 2     | 1                           |     | 2                          |
(𝑠 ,nm,𝑜 ).
1 2
|     |     |     | nm(𝑠 ,𝑜 ), nm(𝑠 | ,𝑜 ), 𝑜 =𝑠 |         |
| --- | --- | --- | --------------- | ---------- | ------- |
|     |     |     | 1 1             | 2 2 1 2    | [𝑇𝑟𝑎𝑛𝑠] |
|     |     |     | nm(𝑠            | ,𝑜 )       |         |
1 2
Anexamplehereis:
|     |     | 𝑙𝑜𝑐_𝑖𝑛(𝑠 | ,𝑜 ), 𝑙𝑜𝑐_𝑖𝑛(𝑠 | ,𝑜 ), 𝑜 =𝑠 |            |
| --- | --- | -------- | -------------- | ---------- | ---------- |
|     |     |          | 1 1            | 2 2 1      | 2 [𝑇𝑟𝑎𝑛𝑠]. |
|     |     |          | 𝑙𝑜𝑐_𝑖𝑛(𝑠       | ,𝑜 )       |            |
1 2
Withthisrule,fromtriples(HarukiMurakami,locate_in,Kyoto)and(Kyoto,locate_in,Japan),we
deriveanewtriple(HarukiMurakami,locate_in,Japan).
Rule#5:CompositeReasoning.Thepreviousfourreasoningrulesareallmeta-rulescapturingthe
mostbasicandfundamentallogicalrelationsamongthefactsandrules.Severalbasicreasoning
rulescanbechainedtogethertoformacompositionreasoningruleiftherelationsintherules
Proc.ACMProgram.Lang.,Vol.8,No.OOPSLA2,Article336.Publicationdate:October2024.

Drowzee:MetamorphicTestingforFact-ConflictingHallucinationDetectioninLargeLanguageModels 336:11
havelogicalrelations.Compositereasoningrulescangenerateknowledgethatrequiresmultiple
stepsofreasoning.
[𝐶𝑜𝑚𝑝].Givenmultiplebasicreasoningrulesor
| Definition5. |     | CompositeReasoningRules |     |     |     |     |
| ------------ | --- | ----------------------- | --- | --- | --- | --- |
predicates[𝑅𝑢𝑙𝑒 𝑖] ∈ {[𝑁𝑒𝑔],[𝑆𝑦𝑚],[𝐼𝑛𝑣𝑒𝑟𝑠𝑒],[𝑇𝑟𝑎𝑛𝑠],[𝑃𝑟𝑒𝑑𝑖𝑐𝑎𝑡𝑒𝑠]},wecanchainthemuptoform
anewcompositereasoningrule.
|     |     |     | nm (...),nm | (...),... |             |     |
| --- | --- | --- | ----------- | --------- | ----------- | --- |
|     |     |     | 1_𝑅𝑢𝑙𝑒 1    | 2_𝑅𝑢𝑙𝑒 1  | [𝑅𝑢𝑙𝑒 ],... |     |
|     |     |     |             | 𝑅         | 1           |     |
1
...
[...],...
...
|     |     |     | (...),     | (...),...  |     |     |
| --- | --- | --- | ---------- | ---------- | --- | --- |
|     |     |     | nm 1_𝑅𝑢𝑙𝑒𝑖 | nm 2_𝑅𝑢𝑙𝑒𝑖 |     |     |
[𝑅𝑢𝑙𝑒𝑖],...
𝑅
|     |     |     |     | i   | [𝐶𝑜𝑚𝑝] |     |
| --- | --- | --- | --- | --- | ------ | --- |
𝑅
new
Theprocessofapplyingthesevariousrulestothegroundtruthtriplesextractedintheprevious
modulecanbereferencedinAlgorithm2.Anautomaticrulegeneratorcouldbedesignedatthe
firststagetoiterateitspredicatesandgeneratethederivationrules𝑄
accordingtotherelation
category(asinLines3-4).Thecorrespondingqueryproblemsarealsogeneratedandmappedto
thegeneratedrules,whichcouldbeappliedtothePrologquerylater.Withthepredetermined
rules,wecanbeassistedwiththePrologengine,assertingalltherelatedtriplesandconsultingthe
reasoningrules,asoutlinedinLines5-6.Weuse 𝑅 todenotethequeryresultsof𝑅 w.r.tthe
P
PrologprogramP.When𝑅containsnovariables,it(cid:74)re(cid:75)turnsBooleanresultsindicatingthepresence
ofthefact;otherwise,itoutputsallthepossibleinstantiationsofthevariables.Thenasstatedin
Lines7-9,byobtainingsolutionsfromProlog,wecangeneratenewknowledgetriplesbasedon
theentitiesandtheirrelationsprovided.Foreachinstantiationthatcontainsonesubject“s”and
oneobject“o”,wethencomposethemwiththenewpredicate,whichistakenasonederivedfact.
Thesederivedfactsarelaterusedtogeneratetestcases.
Algorithm2DerivingNewFacts
| Require: | GroundFacts(𝑅 | (cid:101)ground | ),RelationCategory(RC) |     |     |     |
| -------- | ------------- | --------------- | ---------------------- | --- | --- | --- |
Ensure: DerivedFacts(𝑅
|     |     | (cid:101)derived | )   |     |     |     |
| --- | --- | ---------------- | --- | --- | --- | --- |
functionDerivingFacts(𝑅
| 1:  |     |      | (cid:101)ground ,RC) |     |     |                 |
| --- | --- | ---- | -------------------- | --- | --- | --------------- |
|     | 𝑅   | ← [] |                      |     |     | ⊲Initialization |
2: (cid:101)derived
|     | fornminRCdo |     |     |     |     | ⊲Iterateeachpredicate |
| --- | ----------- | --- | --- | --- | --- | --------------------- |
3:
|     | nm↩→(nmnew | ,𝑄) |     |     | ⊲Obtainthereasoningrule,andthenewpredicate |     |
| --- | ---------- | --- | --- | --- | ------------------------------------------ | --- |
4:
| 5:  | P ←𝑅            | (cid:101)ground ++𝑄 |             |     |     | ⊲ConstructthePrologprogram |
| --- | --------------- | ------------------- | ----------- | --- | --- | -------------------------- |
| 6:  | instantiations← |                     | nmnew (𝑆,𝑂) |     |     | ⊲Obtainconcreteentities    |
P
for(s,o)ininstan(cid:74)tiationsdo (cid:75) ⊲Iterateeachentitytuple
7:
|     | 𝑅                  |                  | (𝑠,𝑜) |     |     | ⊲Constructthederivedfact |
| --- | ------------------ | ---------------- | ----- | --- | --- | ------------------------ |
| 8:  | new                | ←nmnew           |       |     |     |                          |
| 9:  | 𝑅 (cid:101)derived | .append(𝑅        | new ) |     |     | ⊲Appendthederivedfacts   |
|     | return𝑅            |                  |       |     |     | ⊲Returnthederivedfacts   |
| 10: |                    | (cid:101)derived |       |     |     |                          |
4.3 BenchmarkConstruction
Fromthederivedtriples,thismoduleoutlinesourapproachtoconstructingquestion-answer(Q&A)
pairsandpromptstofacilitatetheautomatictestingofFCH.
Proc.ACMProgram.Lang.,Vol.8,No.OOPSLA2,Article336.Publicationdate:October2024.

336:12 NingkeLi,YuekangLi,YiLiu,LingShi,KailongWang,andHaoyuWang
Inaddressingtheobstacleofhighhumaneffortdemandedinthetestoraclegenerationprocess,
wedesignanautomatedgenerationoftestcase-oraclepairsbasedonmappingrelationsbetween
variousentitiestoproblemtemplates,greatlyreducingrelianceonmanualeffort.
QuestionGeneration.Toensureeffectiveandsystematictestcasesandpromptgeneration,we
haveadoptedamethodthatutilizesentityrelationsmappingtopredefinedQ&Atemplates.Inthe
constructionofrelation-basedQ&Atemplates,onekeyaspectliesinaligningvarioustypesof
relationswiththecorrespondingquestiontemplatesfromthederivedtriples,i.e.,thepredicatetype
inthetriple.Differentrelationtypespossessuniquecharacteristicsandexpressiverequirements,
leadingtovariouspredefinedtemplates.AslistedinTable1,wemaptherelationtypestoquestion
templatesbasedonspeechandthegrammaticaltenseofthepredicate,toguaranteecomprehensive
coverage.Beyondtheseuniversaltemplates,forhard-to-describepredicates,weemploycustomized
templatestogeneratevalidQ&Apairs.Toenhancetheconstructionofnaturallanguageformatted
questions,wealsoleveragetheLLMtorefinethestructureofQ&Apairs.
Anotherkeyaspectisregardingtheautomaticandreliableanswergeneration.Wenotethatthe
answertothecorrespondingquestionisreadilyattainablefromthefactualknowledgeinthetriple.
Primarily,itiseasytodeterminewhethertheansweristrue/falsebasedonthederivedtriples.
Meanwhile,mutatedtemplateswithpositiveandnegativesemanticsviatheusageofsynonymsor
antonyms,whichgreatlyenhancethequestiondiversity,canbetreatedinasimilarmannerasthe
negationruledefinedinSection4.2.Specifically,iftheanswertoaquestionwithoriginalsemantics
isYes/No,thenforaquestionwithmutatedoppositesemantics,thecorrespondinganswerwould
naturallybetheopposite,i.e.,No/Yes.Forexample,afterobtainingtheoriginalQ&Apair-Isittrue
thatCrohn’sdiseaseandHuntington’sdiseasecouldsharesimilarsymptomsandsigns?-Yes.,wecan
usesomeantonymstomutateitinto-IsittruethatCrohn’sdiseaseandHuntington’sdiseasehave
totallydifferentsymptomsandsigns?-No.
Table1. Relation-TemplateMappingPattern.
Relation TemplateExamples
-Isittruethat⟨Subject⟩and⟨Object⟩share⟨Relation⟩?
NounPhrase -⟨Subject⟩and⟨Object⟩have/made/sharedtotallydifferent⟨Relation⟩.
Pleasejudgethetruthfulnessofthisstatement.
VerbPhrase -Isittruethat⟨Subject⟩is/was/are/were⟨Relation⟩⟨Object⟩?
(PassiveVoice)-Itisimpossiblefor⟨Subject⟩tobe⟨Relation⟩⟨Object⟩.AmIright?
VerbPhrase -Isittruethat⟨Subject⟩⟨Relation⟩⟨Object⟩?
(ActiveVoice) -⟨Subject⟩⟨Relation⟩⟨Object⟩.
Table2. PromptTemplate.
Instruction:Answerthequestionwithyourknowledgeandreasoningpower.
Query:Nowgiventhequestion:question,pleaseprovideananswerwithyourknowledgeandreasoningpower.
Thinkofitstepbystepwithahuman-likereasoningprocess.
Aftergivingtheanswer,listtheknowledgeusedinyourreasoningprocessintheformofdeclarativesentencesandpointbypoint.
Hereisanexample.Question:DuringBarackObamaheldthepositionasthepresidentoftheUSA,wereanyfilmsdirectedby
JamesCameronreleased?
SupposedResponse:Yes,duringBarackObama’spresidencyfrom2009to2017,onefilmdirectedbyJamesCameronwasreleased
-Avatarin2009.
Thekeyknowledgepointsusedinthisreasoningprocessare:
1.BarackObamawastheUSPresidentfromJanuary20,2009toJanuary20,2017.
2.JamesCameronisafamousfilmdirectorknownformovieslikeTitanic,Avatar,Terminator2,etc.
3.Cameron’sonlyfilmreleaseduringObama’spresidencywasAvatarin2009.
Proc.ACMProgram.Lang.,Vol.8,No.OOPSLA2,Article336.Publicationdate:October2024.

Drowzee:MetamorphicTestingforFact-ConflictingHallucinationDetectioninLargeLanguageModels 336:13
PromptConstruction.AsillustratedinTable2,beforeinitiatingourinteractionwithLLMs,we
predefinespecificinstructionsandprompts,requestingthemodeltoutilizeitsinherentknowledge
and inferential capabilities to deliver explicit (yes/no/I don’t know) judgments on our queries.
Additionally,weinstructthemodeltopresentitsreasoningprocessinatemplatefollowingthe
judgment.TheprimaryaimistoensureLLMsprovideeasilyassessableresponsesbyusingstan-
dardized prompts and instructions. This approach also ensures that the model can exercise its
reasoningabilitiesaseffectivelyaspossibleunderthegiveninstructionsandcues.
4.4 ResponseEvaluation
TheobjectiveofourproposedmoduleistoenhancethedetectionofFCHwithinLLMoutputs,
specificallyfocusingonthediscrepanciesbetweenLLMresponsesandverifiedgroundtruthinQ&A
pairs.Recognizingtheinherentchallengesindirectlyaccepting“yes”or“no”answersfromLLMs
duetopotentialinaccuracies,ourapproachunderscorestheimportanceofthoroughlyanalyzing
thereasoningprocesspresentedbyLLMs.Thisanalysisisvitalforaccuratelydeterminingthe
factualconsistencyofLLMresponses,therebyaddressingtheprimarychallengeinidentifyingFCH
withinLLMoutputs.
Toachieveautomateddetectionoffactualconsistency,ourmethodologyfirstincorporatesa
parsingstepthatleveragesadvancedNLPtechniques.Thisstepisdesignedtoextractessential
semantic elements from each sentence within LLM outputs, assembling these elements into a
coherent,semantic-awarestructure.Thefoundationalpremiseofourapproachispredicatedon
evaluatingthesemanticsimilaritybetweentheseconstructedstructures,aimingtodiscernthe
degreeofconsistencyintheirunderlyingsemantics.Subsequently,weproposethedevelopmentof
alistofsimilarity-basedtestingoracles.Theseoraclesareinstrumentalinapplyingmetamorphic
testingprinciples,enablingustosystematicallyassesstheconsistencyorinconsistencybetween
LLMresponsesandtheestablishedgroundtruth.Notethatourfocusisontheaccuracyofground
truthfactsratherthanhighlyspecializedorsequentialcontentlikemathematicalproofs.Conse-
quently,duringevaluation,weemphasizewhethertheentitiesandrelationsintheresponsealign
withthegroundtruth,regardlessoftheorderinwhichthefactsarepresented.Ourapproachis
structuredaroundseveralcriticalsteps,detailedasfollows:
Step1.PreliminaryScreening.First,weeliminatescenariosinwhichtheLLMdeclinesto
provide an answer, as indicated by the “answer” field of the LLM’s response (as described in
Algorithm3Lines3-4).MostoftheseresponsesarisebecausetheLLMlackstherelevantknowledge
for the reasoning process. Since these responses adhere to the LLM’s principle of honesty, we
classifythemascorrectandnormalresponses,denotedasCOinthealgorithm.
Step2.ResponseParsingandSemanticStructureConstruction.AsstatedinAlgorithm3
Lines6-7,fortheremainingsuspiciousresponses,theExtractTriplefunctionisusedtogenerate
triplesbasedonthestatementscontainedinthereasoningprocesspartoftheLLM’sresponse.Then
fromtheextractedtriples(T(cid:103)rpl),theBuildGraphfunctioncanconstructasemanticstructureSS
resp
,
wheretheentities(i.e.,thesubjectandobject)arerepresentedasnodes,andtherelationbetween
themisillustratedasanedgeconnectingthesenodes.Concurrently,thegroundtruthtriples(𝑅 (cid:101)all )
associatedwiththequestionareusedasinputtoconstructasimilarsemanticstructure𝑆𝑆 𝐺𝑇.
Step3.Similarity-basedMetamorphicTestingandOracles.Weapplymetamorphicrelations
todetectandevaluatepotentialerrorsinLLMresponses,basedontherelationshipsbetweeninputs
andoutputs,ratherthanrelyingontraditionallabeleddata.Inourcontext,metamorphicrelations
specifically refer to comparing the similarity between semantic structures generated by LLMs
andthegroundtruthcounterparts,toidentifyandclassifyhallucinationanswersfromLLMs(as
mentionedinAlgorithm3Lines8-17).Notethatweprovidefourclassifications:correctresponses
Proc.ACMProgram.Lang.,Vol.8,No.OOPSLA2,Article336.Publicationdate:October2024.

336:14 NingkeLi,YuekangLi,YiLiu,LingShi,KailongWang,andHaoyuWang
(denotedasCO),hallucinationscausedbyerrorinference(EI),hallucinationscausedbyerroneous
knowledge(EK),andhallucinationscontainingbothissues(OL).
Algorithm3ResponseEvaluation
Require: LLMResponse(Resp),AllGroundFacts(𝑅 ),Threshold(𝜃 ,𝜃 n)
|     |     |     | (cid:101)all | e   |     |     |
| --- | --- | --- | ------------ | --- | --- | --- |
Ensure: EvaluationResultCategory(𝐶𝑂,𝐸𝐾,𝐸𝐼,𝑂𝐿)
| 1: functionEvaluateResponse(Resp,𝑅 |     |               | (cid:101)all ,𝜃 e,𝜃 n) |     |     |                 |
| ---------------------------------- | --- | ------------- | ---------------------- | --- | --- | --------------- |
| 2: 𝐶𝑂,𝐸𝐾,𝐸𝐼,𝑂𝐿←                    |     | []            |                        |     |     | ⊲Initialization |
| ifResp.𝑎𝑛𝑠𝑤𝑒𝑟                      |     | =𝑟𝑒𝑓𝑢𝑠𝑎𝑙 then |                        |     |     |                 |
3:
|     | 𝐶𝑂.append(Resp) |     |     |     | ⊲PreliminaryScreening |     |
| --- | --------------- | --- | --- | --- | --------------------- | --- |
4:
else
5:
6: T(cid:103)rpl←ExtractTriple(Resp.reasoning) ⊲Extractusefultriples
7: 𝑆 𝑆 ,𝑆 𝑆 ←BuildGraph(T(cid:103)rpl,𝑅 ) ⊲Buildsemanticstructure
|     | (cid:102) resp (cid:102) ground |     | (cid:101)all |     |     |     |
| --- | ------------------------------- | --- | ------------ | --- | --- | --- |
8: se ←J_Sim (𝑆 (cid:102) 𝑆 resp,𝑆 (cid:102) 𝑆 ) ⊲Calculateedgesimilarity
|     |                 | e ground                     |     |                                        |                          |     |
| --- | --------------- | ---------------------------- | --- | -------------------------------------- | ------------------------ | --- |
|     | ←J_Sim          | (𝑆 𝑆 resp,𝑆 𝑆 )              |     |                                        | ⊲Calculatenodesimilarity |     |
| 9:  | sn              | n (cid:102) (cid:102) ground |     |                                        |                          |     |
|     | if𝑠 <𝜃          | and𝑠 <𝜃 then                 |     |                                        |                          |     |
| 10: | 𝑒 𝑒             | 𝑛 𝑛                          |     |                                        |                          |     |
| 11: | 𝑂𝐿.append(Resp) |                              |     | ⊲Appendhallucinationrelatedtobothtypes |                          |     |
| 12: | elseifse <𝜃     | then                         |     |                                        |                          |     |
e
| 13: | 𝐸𝐼.append(Resp) |         |     |     | ⊲Appenderrorinferencehallucination |     |
| --- | --------------- | ------- | --- | --- | ---------------------------------- | --- |
|     | elseifsn        | <𝜃 then |     |     |                                    |     |
| 14: |                 | n       |     |     |                                    |     |
|     | 𝐸𝐾.append(Resp) |         |     |     | ⊲Appenderrorknowledgehallucination |     |
15:
else
16:
| 17:               | 𝐶𝑂.append(Resp) |     |     |     | ⊲Appendcorrectresponse                |     |
| ----------------- | --------------- | --- | --- | --- | ------------------------------------- | --- |
| return𝐶𝑂,𝐸𝐾,𝐸𝐼,𝑂𝐿 |                 |     |     |     | ⊲Returnthecategorizedevaluationresult |     |
18:
Specifically,theoraclesformetamorphictestingcanbedividedintothefollowingtypes:
EdgeVectorMetamorphicOracle(MO ):Thisoracleisbasedonthesimilarityofedgevectors
E
betweenSS andSS .IfthevectorsimilaritybetweentheedgesintheSS andthosein
|     | resp | ground |     |     |     | resp |
| --- | ---- | ------ | --- | --- | --- | ---- |
SS ground fallsbelowapredeterminedthreshold,itindicatesthattheLLM’sanswersignificantly
divergesfromthegroundtruth,suggestingthepresenceofanFCH.Conversely,ifthesimilarity
meetsorexceedsthethreshold,theLLM’sanswerisconsideredtoalignwiththegroundtruth.
Morespecifically,weutilizeJaccardSimilarity[ScienceDirect2023]togaugethesimilarityscore
| betweenedgevectorsextractedfromSS |     |     | andthosein𝑆𝑆 | 𝑔𝑟𝑜𝑢𝑛𝑑. |     |     |
| --------------------------------- | --- | --- | ------------ | ------- | --- | --- |
resp
|     |     |           |       | |(cid:101)E ∩(cid:101)E | |   |     |
| --- | --- | --------- | ----- | ----------------------- | --- | --- |
|     |     | J_Sim (SS | ,SS ) | = resp ground           | ,   |     |
E resp ground
|     |     |     |     | |(cid:101)E ∪(cid:101)E | |   |     |
| --- | --- | --- | --- | ----------------------- | --- | --- |
resp ground
checkif
|     |     | J_Sim | (SS ,SS | ) <𝜃     |     |     |
| --- | --- | ----- | ------- | -------- | --- | --- |
|     |     |       | E resp  | ground n |     |     |
where(cid:101)E and(cid:101)E denote the list of edges extracted from SS and SS , and 𝜃 is a
|     | resp | ground |     |     | resp ground | 𝐸   |
| --- | ---- | ------ | --- | --- | ----------- | --- |
predefinedthreshold(tobedetailedinSection5.1).Intuitively,thesimilarityscoreiscalculatedas
theproportionofidenticaledgessharedbetweenthetwolistsagainstthetotalnumberofunique
edgesinbothlists.Ifthescoreissmallerthanthethreshold,thenanFCHisdetected.Notethat
whendeterminingthejointandunionoflists(cid:101)E and(cid:101)E ,weconsidertwoedgesasidentical
|     |     |     | resp | ground |     |     |
| --- | --- | --- | ---- | ------ | --- | --- |
iftheircorrespondingrelationsareidenticalorrepresentedbysynonymouswords,andviceversa.
NodeVectorMetamorphicOracle(MO ):Thisrelationexaminesthesimilarityofnodevectors
N
betweenSS andSS .DefinedinasimilarmannerasMO ,ifthenodesimilaritybetween
|     | resp | ground |     |     | N   |     |
| --- | ---- | ------ | --- | --- | --- | --- |
theedgesintheSS resp andthoseinSS ground fallsbelowapredeterminedthreshold,itindicatesthat
Proc.ACMProgram.Lang.,Vol.8,No.OOPSLA2,Article336.Publicationdate:October2024.

Drowzee:MetamorphicTestingforFact-ConflictingHallucinationDetectioninLargeLanguageModels 336:15
theLLM’sanswersignificantlydivergesfromthegroundtruth,suggestingthepresenceofanFCH;
viceversa.MO canbecapturedbytheJaccardSimilarity,definedasfollows:
N
J_Sim (SS ,SS ) =
|N(cid:101)resp ∩N(cid:101)ground |
,
N resp ground
|N(cid:101)resp ∪N(cid:101)ground |
checkif
J_Sim (SS ,SS ) <𝜃
N resp ground n
whereN(cid:101)resp andN(cid:101)ground denotesthelistofnodesextractedfromSS resp and𝑆𝑆 𝑔𝑟𝑜𝑢𝑛𝑑,and𝜃 𝑛 isa
predefinedthreshold(tobedetailedinSection5.1).Intuitively,thesimilarityscoreiscalculatedas
theproportionofidenticalnodessharedbetweenthetwolistsagainstthetotalnumberofunique
nodesinbothlists.Ifthescoreissmallerthanthethreshold,thenanFCHisdetected.Notethat
whendeterminingthejointandunionoflistsN(cid:101)resp andN(cid:101)ground ,weconsidertwonodesasidentical
iftheircorrespondingentitiesareidenticalorrepresentedbysynonymouswords,andviceversa.
5 Evaluation
Ourevaluationtargetsthefollowingresearchquestions:
•RQ1(Effectiveness):HoweffectiveisDrowzeeforidentifyingLLMFCHissues?This
RQstudiestheeffectivenessof DrowzeeingeneratingtestcasesandidentifyingLLMFCHissues.
•RQ2(HallucinationCategorizationandAnalysis):WhatisthecategorizationofLLM
FCHissues?ThisRQcategorizestheFCHissuesofvariousLLMsidentifiedbyDrowzee.We
also provide case studies for some specific cases, including temporal-related FCHs and out-of-
distribution-dataknowledge-relatedFCHs.
•RQ3(ComparisonwithExistingWorks):HowdoesDrowzeecomparewithexisting
approachesindetectingLLMFCHissues?ThisRQinvestigateswhetherDrowzeeoutperforms
existingtestingbenchmarksandmethodsinconstructingtestcasesandidentifyingLLMFCHissues.
Weconductaqualitativeanalysisaswellasasmall-scalequantitativeanalysisoftheaccuracyof
currenthallucinationdetectionmethodscomparedwithDrowzee.
•RQ4(AblationStudy):Whetherthefourtypesoflogicreasoningrulescanidentify
LLMFCHissuesindependently?ThisRQexploreswhetherthelogicreasoningrulesofDrowzee
caneffectivelyidentifyLLMFCHissuesseparately.
5.1 ExperimentalSetup
KnowledgeExtraction.WeuseWikipediaandWikidataassourcestoextractentitiesandstruc-
turedinformationasbasefactualknowledge.AfterdownloadingthelatestWikipediadump,we
employwikiextractor[Attardi2015]toextractrelevanttextfromWikipages.Inparallel,weinvoke
Wikidata’s SPARQL [Prud’hommeaux and Seaborne 2018] query module for the extraction of
triples.Throughdataprocessinginvolvingsimplificationandfiltration,weamassacollectionof
basicfactualknowledge,encompassingasizeablenumberof54,483entitiesand1,647,206triples.
LogicReasoningProcessor.Forthelogicreasoningmodule,weapplySWI-Prolog[Wielemaker
etal.2008],anopen-sourceadvancedlogicalprogramminginterpreter.Toeffectivelypreventerrors
duetoexcessivestackedstrings,andensuretheproperoperationofthelogicalprocessorwhen
insertingalargenumberoffactsintoProlog,weemployasamplingmethodandextractasubsetof
entitiestoformaquery.
ModelsUnderTest.ToguaranteeareliableevaluationforRQ1andRQ2,weevaluatesixstate-of-
the-artlargelanguagemodelswithDrowzee.ConsideringthediversenatureofLLMs,weselect
twodistinctcategoriesforin-depthanalysis:thefirstcategorycomprisesAPI-accessiblemodels
withclosed-sourcearchitectureincludingChatGPT(gpt-3.5-turbo-0613)andGPT-4[OpenAI2023],
Proc.ACMProgram.Lang.,Vol.8,No.OOPSLA2,Article336.Publicationdate:October2024.

336:16 NingkeLi,YuekangLi,YiLiu,LingShi,KailongWang,andHaoyuWang
andthesecondcategoryconsistsofopen-sourceLLMswithdeployability,includingLlama2-7B-
chat-hf,Llama2-70B-chat-hf[Touvronetal.2023],Mistral-7B-Instruct-v0.2[Jiangetal.2023],and
Mixtral-8x7B-Instruct-v0.1[Jiangetal.2024].
ModelConfiguration.Wesetthetemperatureparameterto0toachievemorestableandconserva-
tivemodeloutputs,ensuringconsistencyinthecontentgeneratedduringLLMtesting.Additionally,
wesetthetop-pvalueto0.9anddisabletop-k(setto0)tofilteroutlow-probabilitytokensandselect
themostlikelytokens,therebyimprovingtheaccuracyofthegeneratedresults.Tofurthervalidate
theconsistencyoftheLLMresponses,weconductedsignificanceteststovalidatetheconsistency
oftheLLMresponses.Specifically,werandomlyselected40testcasesfromeachdomainunder
each rule, resulting in a total of 1440 test cases. Using GPT-3.5-turbo as an example, each test
caseisrunfivetimesunderthepreviouslydescribedconfigurationtointeractwiththeLLM.We
thenusetheSentence-bertmodel[ReimersandGurevych2019]tocalculatethepairwisecosine
similaritybetweenthefiveLLMresponsesgeneratedforeachtestcase.TheconsistencyoftheLLM
responsesisevaluatedusingFriedmantests[ScienceDirect2024],anon-parametricstatisticaltest
commonlyemployedtodetectdifferencesintreatmentsacrossmultipletestattempts.Theresults
show no significant differences between the responses of different runs, with an approximate
averagep-valueof0.54.Thisconfirmsthatthegeneratedresponsesareconsistentacrossmultiple
executions,justifyingtheuseofasinglerunforevaluationpurposes.
ResponseValidationThreshold𝜃.TovalidateresponsesfromLLMsasdescribedinSection4.4,
weapplyStanfordOpenIE[Angelietal.2015;Remy2020]forknowledgetripleextractionfromLLM
responsesandthenusePhrase-BERT[Wangetal.2021]tocalculatethevectorsimilarityofnodes
andedgesfromtheconstructedsemanticstructures.WealsoutilizeGPT-4toextracttriplesforsome
complexresponsesthatStanfordOpenIEcannothandleeffectively.Herewesetthethresholdto0.8,
consideringknowledgetriplesassemanticallyequivalentiftheyexceedthisthreshold,andvice
versa.Todeterminethethresholdvalue,wesample30testcasesandcorrespondingLLMresponses
fromeachofthenineknowledgedomainslistedinFigure5a.Throughthisanalysis,wefindthatby
settingthethresholdvaluesforboth𝜃 𝐸 and𝜃 𝑁 at0.8,withthegiven270testcasesthatarecorrectly
classified,wecanestimatethetruepositivesamongalltestcasesthroughLaplace’sapproachinthe
Sunriseproblem[Laplace1951],resultingin99.6%whendetectingnon-equivalentLLManswersas
FCHs.Inotherwords,allinstanceswhereanLLM’sanswerhasasemanticsimilarityscorebelow
0.8comparedtothegroundtruthwerecorrectlyidentifiedasFCHcases.
ConsistencyofWords.Toensurewordconsistencyinexperiments,wemaintainseveraldictio-
naries.Forsymmetricrelations,wehaveadictionarythatincludesrelationswhichretaintheir
meaningwhenthesubjectandobjectarereversed.Additionally,weusesynonymdictionaries
providedbyNLPlibraries(e.g.,WordNet[Miller1995])alongwithourownsetofsynonymstailored
forspecificcaseswhenvalidatingtheLLMresponses.
Running Environment. Our experiments are conducted on a server running Ubuntu 22.04
withtwo64-coreAMDEPYC7713,512GBRAM,andtwoNVIDIAA100PCIe80GBGPUs.Our
experimentsconsumeatotalof120GPUhours.
5.2 RQ1:Effectiveness
To reveal the effectiveness of Drowzee, we evaluate the statistics of test cases generated by
DrowzeeandthenevaluatethecapabilitiesofidentifyingLLMFCHissueswiththegeneratedcases.
TofurtherassesstheeffectivenessoftestcasesforuncoveringFCHissuesinspecificknowledge
domains,weevaluatetheperformancesofLLMsontestcasesacrossvariousknowledgedomains.
EffectivenessonGeneratingQ&ATestCases.WeapplyDrowzeetogenerateaQ&Atest
benchmark,amountingtoacomprehensivetotalof7,200testcases,designedtoprovideabroad
anddetailedevaluationofLLMFCHissuesacrossspecificknowledgedomains.
Proc.ACMProgram.Lang.,Vol.8,No.OOPSLA2,Article336.Publicationdate:October2024.

Drowzee:MetamorphicTestingforFact-ConflictingHallucinationDetectioninLargeLanguageModels 336:17
|     | Hallucination |     | Normal |     |         |                |                     |           | 0 . 6 5 |
| --- | ------------- | --- | ------ | --- | ------- | -------------- | ------------------- | --------- | ------- |
| 1.0 |               |     |        |     | ChatGPT |                |                     |           |         |
|     |               |     |        |     |         | 0.40 0.41 0.38 | 0.44 0.38 0.47 0.45 | 0.47 0.41 |         |
0 . 6 0
0.8 0.424 0.402 GPT-4 0.26 0.23 0.21 0.25 0.33 0.28 0.21 0.22 0.23 0.55
| 0.579 |     |     |     | 0.640 | LLaMA2-7B |     |     |     | 0 . 5 0 |
| ----- | --- | --- | --- | ----- | --------- | --- | --- | --- | ------- |
0.658
| 0.6  | 0.753 |     |     |     |     | 0.58 0.56 0.53 | 0.59 0.61 0.61 0.56 | 0.63 0.51 |         |
| ---- | ----- | --- | --- | --- | --- | -------------- | ------------------- | --------- | ------- |
| etaR |       |     |     |     |     |                |                     |           | 0 . 4 5 |
LLaMA2-70B
|     |     |     |     |     |     | 0.36 0.35 0.36 | 0.32 0.35 0.38 0.34 | 0.31 0.31 | 0.40 |
| --- | --- | --- | --- | --- | --- | -------------- | ------------------- | --------- | ---- |
0.4
|           |       |       |       |       |           | B                       |                                 |               | 0 . 3 5   |
| --------- | ----- | ----- | ----- | ----- | --------- | ----------------------- | ------------------------------- | ------------- | --------- |
|           | 0.576 |       | 0.598 |       | a l - 7   |                         |                                 |               |           |
|           |       |       |       |       | i s t r   | 0 . 6 0 0 . 6 1 0 . 5 4 | 0 . 5 9 0 . 6 5 0 . 6 5 0 . 6 2 | 0 . 5 8 0 . 5 | 4         |
| 0.2 0.421 |       | 0.342 |       | 0.360 | M         |                         |                                 |               | 0 . 3 0   |
|           | 0.247 |       |       |       | x 7       | B                       |                                 |               |           |
|           |       |       |       |       | r a l - 8 | 0 . 3 8 0 . 3 2 0 . 3 5 | 0 . 3 4 0 . 3 4 0 . 4 1 0 . 3 8 | 0 . 3 9 0 . 3 | 3 0 . 2 5 |
Mis t
0.0
ChatGPT GPT-4 LLaMA2-7BLLaMA2-70BMistral-7BMistral-8x7B Culture Geo HealthHistory Math NaturePeopleSociety Tech
(a)OverallHallucinationRateofVariousLLMs. (b)HallucinationRateHeatmapofSpecificDomain.
|               |        |       | Fig.6.      | EffectivessofDrowzee. |            |                |           |         |      |
| ------------- | ------ | ----- | ----------- | --------------------- | ---------- | -------------- | --------- | ------- | ---- |
| Effectiveness | across | LLMs. |             |                       |            |                |           |         |      |
|               |        |       | We instruct |                       | LLMs under | test utilizing | Q&A pairs | derived | from |
Drowzeeandautomaticallylabelbothhallucinationandnormalresponses.DifferentLLMsmight
trigger different hallucinations on the same questions. The results are presented in Figure 6a,
illustratingtheproportionofFCHsversusnormalresponsesfromLLMsundertest.
Amongallmodels,GPT-4exhibitsthebestperformance,demonstratingthelowestproportionof
hallucinatoryresponsesinthetestcasesgeneratedbyDrowzee,atonly24.7%,whileChatGPT
fallsslightlybehindwith42.1%.Open-sourceLLMsincludingLlama2-7B-chat-hfandMistral-7B-
Instruct-v0.2withfewerparametersperformworse,buttheircounterpartswithlargerparameters
(i.e.,Llama2-70B-chat-hfandMixtral-8x7B-Instruct-v0.1)achievehighernormalresponserates
surpassingChatGPTonDrowzee.ThisindicatesthatthetestcasesgeneratedbyDrowzeesuc-
cessfullytriggerhallucinationresponsesacrossvariousLLMswhenconfrontedwithquestions
requiringlogicalreasoningcapabilities.
EffectivenessonSpecificDomainKnowledgeforEachLLM.Tofurtherexploretheeffec-
tivenessof DrowzeeinidentifyingFCHissuesspanningvariousdomainsofLLMs,wecompare
hallucinationresponseacrossninespecificdomainknowledge.Figure6bpresentsthegenerated
heatmapsoftheconfusionmatricesforhallucinationresponseratefromthespecificknowledge
fieldbasedonthetestingresults.Itcanbeclearlyobservedthatdifferentmodelsexhibitvarying
strengthsandweaknessesacrossdistinctknowledgedomains.
Aninterestingfindingisthat,withinthedomainsofnaturalsciencesandmathematics,LLMs
generallyexhibitweakerperformance.Thisispotentiallybecausetherearemanyastrophysical
or mathematical entities and their interrelationships in generated test cases by Drowzee. To
answersuchquestions,theLLMneedsanextensiveunderstandingofastrophysicalknowledge
andmathematicaltheory.Thus,weinferthatthisrealmofknowledgeisnotwell-coveredinthe
trainingdatasetsofLLMsundertest,therebyresultinginhighhallucinationrates.Suchadisparity
inknowledgeislikelyasignificantfactorintheobservedunderperformanceofLLMsinthese
specificdomains.
ANSWERtoRQ1
OurevaluationusingDrowzeerevealsthatexistingLLMshaveanotabletendencytoproduce
FCHwhenfacedwithlogicalreasoningchallenges.Theresultsvariedacrossknowledgedomains,
highlightingthatLLMsaremorepronetoFCHwhenansweringquestionsthatrequirehighly
specialized,domain-specificknowledge.
Proc.ACMProgram.Lang.,Vol.8,No.OOPSLA2,Article336.Publicationdate:October2024.

336:18 NingkeLi,YuekangLi,YiLiu,LingShi,KailongWang,andHaoyuWang
5.3 RQ2:FCHCategorizationandAnalysis
5.3.1 FCHCategorization. Wecategorizethehallucinationresponsesinmoredetailandfocus
primarilyontwotypesofhallucination:errorknowledgeresponseanderrorinferenceresponse.
Notethatweconsiderrefusaltorespondsuchas‘Idon’tknow’duetothelackofrelevantknowledge
as adhering to LLMs’ honesty and truthfulness principles. Therefore, we categorize refusal to
respondasanormalresponse.Toensurefairandunbiasedcategorization,100hallucination-related
responseswererandomlyselectedandindependentlycategorizedbythreeco-authors,whothen
discussedtheresultstoreachaconsensuscategorization.
ErrorKnowledgeResponse.OriginatedfromLLMsutilizingerroneousorcontextuallyinappro-
priateknowledgeduringthereasoningprocess.
Error Inference Response. The most frequently occurring type is attributed to the lack of
reasoningpowerandflawedreasoningthoughtsofLLMs.
GPT-3.5-turbo GPT-4 Llama2-7B
35.1% 10.1% 54.8% 56.7% 8.3% 35.0% 48.1% 13.4% 38.5%
Llama2-70B Mistral-7B-v0.2 Mixtral-8x7B
45.0% 21.1% 33.9% 35.5% 16.3% 48.2% 55.9% 14.7% 29.4%
Error Inference Error Knowledge
Fig.7. FCHCategorization.
5.3.2 HallucinationMeasurement. Hereweprovidethedistributionofthehallucinationcatego-
rizationresults,asdemonstratedinFigure7.Thereispartialoverlapbetweenthesetwotypes
ofhallucinationsbecauseincorrectreasoningprocessesmayalsoinvolveerroneousknowledge.
Amongtheseissues,thereareseveralcontradictoryanswersprimarilyarisingfrominconsistency
between incorrect reasoning processes and correct answers; thus, it exists in these two types
oferrors.Itisobviousthaterrorinferencehallucinationpresentsthemost,totalinghalfofthe
resultsonaverage.ThisindicatesthattheprimarycauseofFCHissuesinlogicalreasoningisthe
insufficientreasoningcapabilityofLLMs.Besides,errorknowledgeadoptedbyLLMsduringthe
logicalreasoningprocessleadstoapproximately40%FCHissues.Theoverlapsaccountforabout
8%-21% at the hallucination ratio, which indicates there are entities where LLMs have learned
entirelyerroneousrelevantinformation,necessitatingtheemploymentofmeasuresforcorrection.
5.3.3 CaseStudy. Theprecedinganalysisbroadlysummarizesthedistributionofcategoriesfor
logicalreasoning-relatedFCH.Accordingtoourinvestigation,errorinferenceresponseanderror
knowledgeresponsearethemostprevalenttwotypes.
ErrorInferenceHallucination.Oneofthemostcommontypesoflogicalreasoningleadingto
errorinferencehallucinationistemporalattributereasoning,proventobeacategoryofreasoning
Proc.ACMProgram.Lang.,Vol.8,No.OOPSLA2,Article336.Publicationdate:October2024.

Drowzee:MetamorphicTestingforFact-ConflictingHallucinationDetectioninLargeLanguageModels 336:19
Question: Is it true that Canada could have been under jurisdiction by the 1874 Canadian federal
election?
Response: No, Canada could not have been under jurisdiction by the 1874 Canadian federal
election because Canada as a nation did not exist until much later.
Reasoning:
1. The Canadian Confederation, which established the Dominion of Canada as a nation,
occurred on July 1, 1867.
2. The first Canadian federal election took place on October 21, 1867, to elect members to
the House of Commons.
3. The 1874 Canadian federal election did not occur until after the Canadian
Confederation.
Fig.8. ErrorInferenceHallucinationExamplefromMistral-7B-v0.2.
taskthatperformspoorlyonLLMs[Qiuetal.2024].Experimentsontime-relatedreasoningtasks
arecomprehensivelyconductedandunsatisfactoryperformanceofLLMsareobserved.
AsillustratedinFigure8,errorinferencewithcorrectknowledgeleadstoahallucinationresponse
fromMistral-7B-v0.2.AsknowledgeprovidedbytheLLMreasoningprocess,itisclearthatthe
answershouldbe‘Yes’asthe1874CanadianfederalelectionappliestothejurisdictionofCanada.
However,itappearsthattheLLMhasbecomeensnaredbyitslimitations.
ApossibleexplanationforthisphenomenonisthattheLLMdoesnotutilizeitsreasoningabilities
butratherreliesonunreliableintuitiontorespondwhenfacedwithaquestionlackingdetailed
instructions.Thisinsightinspiresustoexploremethodsforeffectivelyenhancingthereasoning
capabilitiesofLLMsthroughasingleinteraction,guidingthesemodelstowarduncoveringanswers
inawaythatmirrorshumanreasoningprocesses.
Finding1.LLMsexhibitweakerperformanceinsensitivitytotemporalinformation,as
well as in their ability to discern sequential logic, which may result in error inference
hallucination.
ErrorKnowledgeHallucination.Figure9demonstratesaclassicexampleofLLMhallucination
causedbyusingerrorknowledgeforlogicalreasoning.GeneralDmitryKarbyshev(1880-1945)was
aRussianImperialArmysoldierwhoservedinseveralwarsduringWorldWarI(1914-1918)and
II(1939-1945),andLouisBernacchi(1876-1942)wasanAustralianphysicistandastronomerwho
servedintheRoyalNavalVolunteerReserveduringWorldWarI.Thus,thegroundtruthanswer
to this question should be ‘Yes’. However, when testing with Llama2-7B-chat-hf, an inspiring
observationisthatwhenLLMsencounterunfamiliarknowledge,theydonotadheretothehonesty
principle;instead,theyfabricateknowledgeanditssources.WesubsequentlyemployanRAG-based
schemetoreintroducerelevantknowledge,leadingtotherestorationofnormalresponses.
Wefurtherconductanout-of-distribution(OOD)knowledgeexperimenttofigureoutthecause
oferrorknowledgehallucination.OODisanotherfactorthatcouldcauseFCHissues[Zhangetal.
2023].Wedesigncontextualreasoningutilizingrecentsportingeventsandnaturaldisastersfrom
Wikipedia since June 2023, which is considered unutilized information in LLMs’ training data
basedontheirup-to-dateintroductions.Weconstructaseriesoftestcasescontainingcontextual
descriptionsofrecenteventsusingDrowzee,observingwhetherLLMscanbeguidedtorespond
toOODknowledgeandtriggerFCH.
Figure10isatypicalcaseofOODcontextsleadingtoerrorknowledgehallucination.Inthe
initialtestofGPT-3.5-turbo,weprovideinformationonseveralwildfiresthathappenedfromJuly
2023toDecember2023,andweconfirmthatthisinformationisnotintheLLMśtrainingdata.The
LLMsubsequentlyindicatesthatithasacquiredthisknowledgethroughthisinteractiveprocess.
Proc.ACMProgram.Lang.,Vol.8,No.OOPSLA2,Article336.Publicationdate:October2024.

336:20 NingkeLi,YuekangLi,YiLiu,LingShi,KailongWang,andHaoyuWang
Question: Is it true that General Dmitry Karbyshev and Louis Bernacchi have participated
in the same conflict or war?
Response: Sure, I'm happy to help you with that! Here's my answer:
Yes, General Dmitry Karbyshev and Louis Bernacchi have participated in the same conflict
or war.
Here's how I arrived at this answer through a human-like reasoning process:
1. General Dmitry Karbyshev is a Russian military officer who has fought in various
conflicts, including the Chechen Wars and the Russian invasion of Ukraine. (Source: BBC
News)
2. Louis Bernacchi is a British soldier who served in the British Army during World War I
and World War II. (Source: BBC History)
3. World War I took place from 1914 to 1918, while World War II took place from 1939 to
1945. (Source: History.com)
4. General Karbyshev was born in 1960, which means he was alive during World War II.
(Source: The Moscow Times)
5. Louis Bernacchi was born in 1876 and died in 1974, which means he was alive during
World War I and World War II. (Source: BBC History)
6. Therefore, since both General Karbyshev and Louis Bernacchi were alive during the same
wars (World War I and World War II), it is reasonable to conclude that they have potentially
participated in the same conflict or war.
Fig.9. CommonErrorKnowledgeHallucinationExamplefromLlama2-7B-chat-hf.
Question 1: There are several natural disasters occuring during 2023, here I provide some
information about famous
natural disasters.
2023_North_Africa_wildfires happened in Algeria;
2023_Central_Canada_wildfires happened in Canada;
2023_Kazakhstan_forest_fires happened in Kazakhstan;
2023_Louisiana_wildfires and 2023_Hawaii_wildfires happened in USA;
2023_Tenerife_wildfire happened in Spain;
Boulder_Fire happened in USA;
New_York_City_orange_sky_day was caused by 2023 Canadian wildfires in 7 June 2023;
Eagle_Bluff_Fire happened in Canada;
Golden_Fire happened in USA.
Answer 1: Thank you for providing information about these natural disasters that occurred in
2023. It's unfortunate to hear about these events, and they highlight the importance of
preparedness and response efforts to mitigate their impact on communities and the environment.
If you have any specific questions or need more information about any of these incidents, please
feel free to ask.
Question 2: Now I wonder was 2023_North_Africa_wildfires of these disasters happened the
earliest? Answer the question and show your reasoning process.
Answer 2: Yes, the 2023_North_Africa_wildfires happened the earliest among the natural
disasters you mentioned. I made this reasoning based on the chronological order of the disasters
you provided in your initial question. Since 2023_North_Africa_wildfires is the first on the list,
it happened the earliest among these natural disasters.
Fig.10. OOD-attributedErrorKnowledgeHallucinationExamplefromGPT-3.5-turbo.
However,aturningpointemergeswhenweusetestcasesdesignedbyDrowzeeinthesecondtest.
Despiteourquestionsbasedonpreliminaryfactualknowledgeprovided,theLLMstillconfidently
respondswithawronganswer.
Weanalyzeseveralpotentialcausesforthissituation.OnepossibilityisthatLLMsstoreincorrect
knowledgeinthefirstturnbecausewhatweprovidedwasmerelyalistofevents,ratherthanalist
ofeventsintheirorderofoccurrence.Inshort,thenormalreasoningprocessinvolvesdefining
theearliestoccurringeventsonlyafterknowingthetimesofallevents.However,theLLMoptsto
judgebasedontheorderweprovideeventknowledge,whichiscontrarytofacts.Anotherpotential
isthatwhenLLMsencounterOODknowledgeiftheydonotstrictlyadheretotheprincipleof
Proc.ACMProgram.Lang.,Vol.8,No.OOPSLA2,Article336.Publicationdate:October2024.

Drowzee:MetamorphicTestingforFact-ConflictingHallucinationDetectioninLargeLanguageModels 336:21
honestybystatingIdonotknow...,theytendtocompletetheresponsebasedonerrorknowledgein
theirexistingknowledgebases.Nevertheless,suchresponsesarelikelytoinducehallucinations.
Finding2.LLMsreadilymakeerroneousassessmentsofmisleadingandunfamiliarknowl-
edgeandleadtoerrorknowledgehallucinationduetotheirassumptions.
ANSWERtoRQ2
ThedetectedFCHcanbecategorizedintotwotypesandthelackofreasoningcapabilitiesposes
abroaderthreatthantheuseofincorrectknowledgeorinadequateinferencestrategies.
5.4 RQ3:ComparisonwithExistingWorks
5.4.1 QualitativeAnalysis. WequalitativelycompareDrowzeewiththestate-of-the-artFCHeval-
uationapproachesandexistingnaturallanguagereasoningbenchmarkstoillustratetheadvantages
of Drowzee.AsillustratedinTable3,weenumeratethecharacteristicsofthesotaFCHevaluation
approaches.TheirmaindistinctionfromDrowzeeliesinthemanneroftaskconstructionandthe
metricsemployedtomeasurehallucinations.
TaskConstructionMethods.Existingworksselectedhereprimarilyutilizegenerativestrate-
gies, evaluating the degree of FCHs based on generated responses. However, in terms of task
construction,thesemethodsincursubstantialhumanresourceefforts.ApartfromtheKoLA-KM,
KA[Yuetal.2024],whichisessentiallyacollectionofexistingQ&Adatasets,bothTruthfulQA[Lin
et al. 2022] and HaluEval [Li et al. 2023a] rely on human annotations to construct Q&A pairs.
HaluEvalalsoemployssemi-automatedgenerationmethods,usingChatGPTqueriesandsampling
forthefilteringofhigher-qualitysamples.Drowzee,ontheotherhand,utilizesProlog-assisted
automaticinferencetoderivenewknowledgetriplesandgeneratetemplatesfornewquestions,
achievingmaximumautomationofconstructionwhileensuringthecomplexityofthequestions.
ResponseEvaluationMetrics.TruthfulQAintroducesahuman-annotationguidebooktovali-
dateanswersbyconsultingcrediblesources.Further,TruthfulQAadoptsamodel-basedevaluation
methodwithfine-tunedGPT-3-6.7Btoclassifyanswers(astrueorfalse)toquestionsaccordingto
theaforementionedhumanannotationsandthencalculatethetruthfulnessrateofLLMresponses.
ForKoLAandHaluEval,theysimplyuseaccuracytoevaluatethecharacter-matchingrateofLLM
responsesandtheprovidedknowledge.FActScore[Minetal.2023]isamethodforevaluatingthe
factualityoflongtextsgeneratedbylanguagemodels.Itdecomposesthegeneratedcontentintoa
seriesofatomicfactsandcalculatesthepercentageoftheseatomicfactsthatcanberetrievedfrom
reliableknowledgesources.Thus,DrowzeeconsidersthestructuralsimilarityofLLMresponses
withoriginalknowledgetriplesandthereasoningprocess,offeringsuperiorityoverthosesimple
evaluationmetrics.
Fornaturallanguagereasoningscenarios,weprovideseveralbenchmarksaslistedinTable4.
FOLIO[Hanetal.2022]isanaturallanguagereasoningdatasetannotatedwithfirst-orderlogic
(FOL)byhumanexperts,primarilyusedtotestthedeductivereasoningcapabilitiesofgenerative
languagemodels.DEER[Yangetal.2024b],ontheotherhand,focusesontheinductivereasoning
paradigm,wherenaturallanguagerulesareinducedfromnaturallanguagefacts,providingrule-fact
pairstotesttheinductivereasoningabilitiesoflanguagemodels.Comparatively,Drowzeefocuses
onreasoningwithreal-worldknowledge,coveringavastamountoffactualinformationinamore
concreteandprecisemanner.
5.4.2 Small-scaleQuantitativeAnalysis. Toevaluatethedetectionaccuracyof Drowzeeincom-
parisonwithexistingmethods,weconductasmall-scalequantitativeanalysisusingasetof100
Proc.ACMProgram.Lang.,Vol.8,No.OOPSLA2,Article336.Publicationdate:October2024.

336:22 NingkeLi,YuekangLi,YiLiu,LingShi,KailongWang,andHaoyuWang
Table3. ComparisonwithSOTAFCHEvaluationApproaches.
Dataset FactSource ConstructionMethod TestOracle Result(%)
TruthfulQA Wikipediapages&websites Humanannotations TruthfulnessRate 89
KoLA-KM,KA Wikidata5M&websites Existingdatasetsconsolidation StandardizedScore(F1) 82
HaluEval-QA Wikipedia Humanannotations&ChatGPTquery StringMatching 85
FActScore Wikipedia — AtomicFact&Retrieval 97
Drowzee-Dataset Wikidatatriples Prolog-aidedreasoning&generation SemanticSimilarity 100
Table4. ComparisonwithNaturalLanguageReasoningBenchmarks.
Benchmark Size ReasoningType DataSource Task Automation
FOLIO 1.4k First-orderlogicreasoning Expert-written TheoremProving ✗
DEER 1.2k Inductivereasoning Wikipedia RuleGeneration ✗
Drowzee Scalable Deductivereasoning Wikidata QuestionAnswering ✓
testcasesthatarealreadymanuallyverified.Thesuccessratesofthiscomparisonaresummarized
inthelastcolumnofTable3.
Asshowninthetable,DrowzeeandFActScoredemonstratesuperiordetectionaccuracy,achiev-
inghigherratesofaccuratehallucinationdetectioncomparedtotheothermethods.Thehigher
performanceofFActScoreandDrowzeecanbeattributedtotheiruseofdecomposedfactand
reasoning-basedapproaches,whichallowformorenuancedassessmentsofLLM-generatedcon-
tents.TruthfulQA,whichreliesonLLM-basedevaluation,performsmoderatelywellbutshows
slightlyloweraccuracyduetotheinherentlimitationsofgenerativemodelsinevaluatingtheir
ownoutput.KoLAandHaluEval,ontheotherhand,whichuseasimplestringmatchingtechnique
withaknowledgebase,exhibitloweraccuracy,highlightingthedrawbacksofrelyingsolelyon
syntacticmatchingwithoutdeepersemanticunderstanding.
Thisquantitativeanalysisfurtherunderscorestheadvantagesof Drowzeeinprovidingamore
reliableandscalablemethodforFCHdetectioninlargelanguagemodels.
ANSWERtoRQ3
Compared to existing benchmarks and FCH evaluation approaches, Drowzee demonstrates
higherautomation,moreaccuratedetection,andgreaterscalability.
5.5 RQ4:AblationStudy
Weconductanablationstudytoinvestigatethecapacityofeachinferencerulesothattheycanbe
distinctlyusedtouncoveranomalies.ThefourtypesofrulesillustratedinSection4.2areseparately
applied to generate Q&A pairs. The symmetric reasoning rule is primarily utilized within the
compositereasoningruleanddoesnotintroducenewknowledgeonitsown.Therefore,wedid
notincludethesymmetricreasoningruleasaseparateconditioninourablationstudy.Forbetter
visualizationandunderstanding,wepresentthedistributionofhallucination-relatedresponses
discoveredwithdiverserule-generatedquestionsbyDrowzeeinFigure11.Thefigureillustrates
whichtypeofrulecantriggerthemosthallucinationresponsesfordifferentLLMsanddifferent
domainsofknowledge.Itisdistinctlyevidentthatfollowingthesuccessfulgenerationofvarious
testcasesusingthefourrulesandtheircombinations,asubstantialnumberofhallucinationsare
elicitedacrosssixLLMs,withthetransitiveruleyieldingthehighestamountofhallucinations.
Proc.ACMProgram.Lang.,Vol.8,No.OOPSLA2,Article336.Publicationdate:October2024.

Drowzee:MetamorphicTestingforFact-ConflictingHallucinationDetectioninLargeLanguageModels 336:23
|                 |            | Culture | Geo HealthHistoryMath |         | NaturePeopleSociety | Tech      |
| --------------- | ---------- | ------- | --------------------- | ------- | ------------------- | --------- |
| GPT-3.5-turbo   |            | 49.8    | 47.4 42.7             | 52.7    | 47.4 44.1 39.8      | 42.9 41.1 |
|                 | GPT-4      | 42.5    | 45.7 60.2             | 47.4    | 52.6 44.7 35.7      | 32.9 53.0 |
|                 | Llama2-7B  | 39.8    | 40.2 46.3             | 41.6    | 38.1 41.2 41.6      | 40.5 42.9 |
|                 | Llama2-70B | 38.8    | 40.7 49.3             | 42.3    | 36.2 40.4 47.8      | 47.3 42.8 |
| Mistral-7B-v0.2 |            | 36.4    | 36.4 45.0             | 37.6    | 37.2 37.2 35.4      | 34.2 37.8 |
| Mixtral-8x7B    |            | 37.8    | 39.4 30.5             | 42.2    | 37.2 37.5 41.7      | 34.2 30.1 |
|                 |            |         | Transitive            | Inverse | Negation            | Composite |
Fig.11. GenerationRulesthatTriggertheMostHallucinationResponsesondiverseLLMsacrossdomains.
TheNumberonEachCell(theUnit:%)RepresentstheTriggeredFCHRatiooftheCorrespondingRuletype.
Followingcloselybehindarethetestcasesgeneratedusingcompositerules,whichhavetriggered
asignificantnumberofFCHsinboththepeopleandhistorydomains.
Fromthecomparisonbetweenfourinferencerules,wecanconcludethatallfourinferencerules
demonstrateeffectivenesswhengeneratingFCHtestcasesandinducinghallucinationperformances
forLLMinteraction.
ANSWERtoRQ4
TheexperimentalresultsshowcasetheindependenceoffourinferencerulesinelicitingFCHs
andthetransitiverulescantriggerthemostFCHsacrossvariousdomains,whichhasprovedto
beasoundapproachtogeneratingtestcases.
6 Discussion
6.1 ThreatstoValidity
LimitedCoverageofKnowledgeDatabases.Ourresearchpredominantlyemploysdatafrom
theWikipediadatabasetogeneratetestcasesusingDrowzee.However,itisimportanttonotethat
Drowzeeisnotlimitedtothisspecificdatabase.Itsdesignallowsforeasyextensionandadaptation
tovariousotherknowledgebases,illuminatingitsversatilityandapplicability.
LimitedAccuracyofHallucinationCategorization.Weutilizeadualapproachforcategoriz-
inghallucinations,combiningassessmentsfromGPT-4withhumanverification.Initially,GPT-4
classifiesthehallucinations,afterwhichwemanuallyreviewarandomsampleof100instances.
ThisprocessrevealsthatGPT-4’scategorizationaccuracystandsatapproximately71%,suggesting
thatintegratingGPT-4forhallucinationcategorizationgenerallyleadstoreliableoutcomes.We
furthernotethattechniquesforfurtherimprovingtheLLM’scategorizationaccuracyviaprompt
engineeringareorthogonaltothescopeofthiswork.
6.2 Mitigation
Afteridentifyingthatlargelanguagemodelsarepronetohallucinationswhendealingwithlogical
reasoning,weperformcategorizationandseektoexplorepotentialmethodstomitigatethisissue.
Modeleditingtechniques,whichfocusonupdatingandoptimizingexistingartificialintelligence
modelswithouttheneedforcompleteretraining,areonesuchapproach.
Proc.ACMProgram.Lang.,Vol.8,No.OOPSLA2,Article336.Publicationdate:October2024.

336:24 NingkeLi,YuekangLi,YiLiu,LingShi,KailongWang,andHaoyuWang
Weinvolvetwomodeleditingalgorithms,i.e.,ROME[Mengetal.2022]andMEMIT[Meng
etal.2023],tointegratenewknowledgederivedfromreasoningintoopen-sourceLLMs,aimingto
alleviateFCHissues.WeapplyFastEdit[hiyouga2023]andEasyEdit[Wangetal.2024]formore
speedyimplementation.Whenthescopeofeditedknowledgeisaround150entries,theedited
modelshowsnotableimprovementinansweringquestionsrelatedtonewreasoningknowledge.
However,whenthenumberofeditedentriesexceedsacertainthreshold(morethan1000),themodel
tendstogeneratealargenumberofmeaninglessresponses,leadingtoadeclineinperformance.
Thissuggeststhatfindinganeffectivesolutiontotheissueofhallucinationsinlogicalreasoning
ischallengingandrequiresfurtherexploration.Ourfindingsalsoprovokeconsiderationonhow
tomitigateFCHissueswhilepreservingthemodel’sinherentcapabilities.Ourapproachoffersa
potentiallyexploratoryandpromisingsolutiontomitigateFCHissuesinLLMs.
6.3 TakeawayMessages
LLMHonestyDuringTraining.DuringthetrainingofLLMs,itisimperativetofocusonmodel
honesty, such as how to enable large models to possess stronger critical thinking and logical
reasoningabilities.Thiscouldbeapromisingdirectiontoeliminatehallucinationissuesingeneral.
TowardsIn-depthUnderstandingofLLMHallucination.Fromtheinsightsderivedinthiswork,
itisimportanttofurtherexploretechniquestounderstandthedeep-rootedcausesofhallucinations
inLLMsthroughwhite-boxmethods.Apromisingdirectionistoenhanceandaugmentthelogical
reasoningcapabilitiesofLLMstoreducehallucinationissues.
7 RelatedWork
7.1 EvaluatingHallucinationinLargeLanguageModels
Severalbenchmarkdatasetshavebeenproposedtoholisticallyassessthehallucinationissuesthat
mayarisewhenlargelanguagemodelsgenerateresponsestoproblemqueries.
TruthfulQA[Linetal.2022]isthemostclassicdatasetforassessingwhetherlanguagemodels
generatetruthfulanswerstoquestions.Ittestswhetherthemodelslearnincorrectanswersduring
thegenerationprocessduetoemulatinghumantext.AnotherdatasetHaluEval[Lietal.2023a]
samples10KinstancesfromthetrainingsetsofHotpotQA[Yangetal.2018],OpenDialKG[Moon
et al. 2019], and CNN/DailyMail [See et al. 2017], and utilizes LLMs to generate hallucination-
corresponding samples by setting tasks and employing specific sampling strategies, which is
primarilyaimedatquestion-answeringtasksandtextsummarizationtasks.KoLA[Yuetal.2024]
teststhehallucinationissuesofLLMsinthedomainofknowledgegraphsandintroducestasks
basedon19focalentities,concepts,andevents.Itassessesthecapacityoflargelanguagemodels
(LLMs)tohandlestructuredknowledgeacrossfourlevels:memory,understanding,application,
andcreation.ThisaimstotestthehallucinationphenomenaofLLMsinthedomainofknowledge
graphs.Fromtheperspectiveoflongcontext,BAMBOO[Dongetal.2024]andFActScore[Min
etal.2023]bothtargetthelongtextgenerationcapabilitiesoflargelanguagemodels,assessing
theirperformanceinextendedcontextscenariosthroughfactualverification.Additionally,there
are assessments of large language models for hallucination issues in specific domains such as
healthcareandfinance[KangandLiu2023;Paletal.2023].
7.2 MitigatingHallucinationinLargeLanguageModels
Currentmitigationstrategiesprimarilyincludetechniquessuchasblack-boxpromptingguidance
andfine-tuningwithextensivefactualdata.
Considerablework[Gouetal.2024;Lightmanetal.2024;Varshneyetal.2023;Vuetal.2024]
involvesutilizingexternalknowledgeretrievalorautomatedfeedbackadjustmentstomaketext
Proc.ACMProgram.Lang.,Vol.8,No.OOPSLA2,Article336.Publicationdate:October2024.

Drowzee:MetamorphicTestingforFact-ConflictingHallucinationDetectioninLargeLanguageModels 336:25
responsesfromlargelanguagemodelsmorecontrollableandreliable.Similarapproachesarepro-
posedformultimodalhallucinationmitigationsuchasWoodpecker[Yinetal.2023],whichextracts
key concepts to generate questions and knowledge assertions for hallucination diagnosis and
mitigation.Anotherthreadinvolvesusingfine-tuningtechniquestomitigatemodelhallucinations.
AlpaGasus[Chenetal.2024],Elarabyetal.[Elarabyetal.2023]andTianetal.[Tianetal.2024]
applyfine-tuningtechniquesonhigh-qualitydataforbettereffectivenessandfactuality.Besides,
thefindingsofElarabyetal.[Elarabyetal.2023]revealthattheknowledgeinjectiontechnique
enhancestheperformanceoflessrobustLLMs.Additionally,anincreasingnumberofresearchers
areturningtowardsstudyingwhite-boxrepairingmethodsforopen-sourcelargelanguagemodels.
TheevidencepresentedinthediscoursebyAzariaetal.[AzariaandMitchell2023]suggeststhat
theinternalstatesofLargeLanguageModelscanbeutilizedtodiscerntheveracityofstatements,
therebyelucidatingtheunderlyingcausesoffactualhallucinationsinLLMs.StudieslikeIIT[Li
etal.2023b]andRepr[Zouetal.2023]endeavortoalleviatehallucinationissuesbydelvinginto
LLMs’deep-layerinformationthroughtheanalysisofinternalmodelstates.Thisapproachnot
onlyaugmentstheinterpretabilityoflargelanguagemodelsbutisalsoregardedasavitalresearch
directionforthefutureofexplainableandtrustworthyAI.
8 Conclusion
In this work, we tackled the critical challenge of FCH in LLM, where they generate outputs
contradictingestablishedfacts.Wedevelopedanovelautomatedtestingframeworkthatcombines
logicprogrammingandmetamorphictestingtosystematicallydetectFCHissuesinLLMs.Ournovel
approachconstructsacomprehensivefactualknowledgebasebycrawlingsourceslikeWikipedia,
thenappliesinnovativelogicreasoningrulestotransformthisknowledgeintoalargesetoftest
caseswithgroundtruthanswers.LLMsareevaluatedonthesetestcasesthroughtemplateprompts,
withtwosemantic-awareoraclesanalyzingthesimilaritybetweenthelogical/semanticstructures
oftheLLMoutputsandgroundtruthtovalidatereasoningandpinpointFCHs.Acrossdiverse
subjectsandLLMarchitectures,ourframeworkautomaticallygenerated7,200usefultestcases,
uncovering hallucination rates as high as 59.8% and identifying lack of logical reasoning as a
keycontributortoFCHissues.ThisworkpioneersautomatedFCHtestingcapabilities,providing
comprehensivebenchmarks,dataaugmentationtechniques,andanswervalidationmethods.The
implicationsarefar-reaching—enhancingLLMreliabilityandtrustworthinessforhigh-stakes
applicationsbyexposingcriticalweaknesseswhileadvancingsystematicevaluationmethodologies.
Data-AvailabilityStatement
ThesourcecodethatsupportsSection4andtherawdatainSection5isavailableintheopen-source
repository[GitHub2024].
Acknowledgement
ThisworkwaspartlysupportedbytheNationalKeyR&DProgramofChina(2021YFB2701000),
theKeyR&DProgramofHubeiProvince(2023BAB017,2023BAB079),theNationalNSFofChina
(grantsNo.62302176,No.62302181,62072046),theKnowledgeInnovationProgramofWuhan-Basic
Research,HuaweiResearchFund,andHUSTCSE-FiberHomeJointResearchCenterforNetwork
Security.
References
RalphAbboud,İsmailİlkanCeylan,ThomasLukasiewicz,andTommasoSalvatori.2020.BoxE:ABoxEmbeddingModelfor
KnowledgeBaseCompletion.InAdvancesinNeuralInformationProcessingSystems33:AnnualConferenceonNeural
Proc.ACMProgram.Lang.,Vol.8,No.OOPSLA2,Article336.Publicationdate:October2024.

336:26 NingkeLi,YuekangLi,YiLiu,LingShi,KailongWang,andHaoyuWang
InformationProcessingSystems2020,NeurIPS2020,December6-12,2020,virtual,HugoLarochelle,Marc’AurelioRan-
zato,RaiaHadsell,Maria-FlorinaBalcan,andHsuan-TienLin(Eds.). https://proceedings.neurips.cc/paper/2020/hash/
6dbbe6abe5f14af882ff977fc3f35501-Abstract.html
GaborAngeli,MelvinJoseJohnsonPremkumar,andChristopherD.Manning.2015.LeveragingLinguisticStructureForOpen
DomainInformationExtraction.InProceedingsofthe53rdAnnualMeetingoftheAssociationforComputationalLinguistics
andthe7thInternationalJointConferenceonNaturalLanguageProcessing(Volume1:LongPapers),ChengqingZongand
MichaelStrube(Eds.).AssociationforComputationalLinguistics,Beijing,China,344–354. https://doi.org/10.3115/v1/P15-
1034
GiusepppeAttardi.2015.WikiExtractor.https://github.com/attardi/wikiextractor.
SörenAuer,ChristianBizer,GeorgiKobilarov,JensLehmann,RichardCyganiak,andZacharyG.Ives.2007.DBpedia:A
NucleusforaWebofOpenData.InTheSemanticWeb,6thInternationalSemanticWebConference,2ndAsianSemanticWeb
Conference,ISWC2007+ASWC2007,Busan,Korea,November11-15,2007(LectureNotesinComputerScience,Vol.4825),
KarlAberer,Key-SunChoi,NatashaFridmanNoy,DeanAllemang,Kyung-IlLee,LyndonJ.B.Nixon,JenniferGolbeck,
PeterMika,DianaMaynard,RiichiroMizoguchi,GuusSchreiber,andPhilippeCudré-Mauroux(Eds.).Springer,722–735.
https://doi.org/10.1007/978-3-540-76298-0_52
AmosAzariaandTomMitchell.2023.TheInternalStateofanLLMKnowsWhenIt’sLying.InFindingsoftheAssociationfor
ComputationalLinguistics:EMNLP2023,HoudaBouamor,JuanPino,andKalikaBali(Eds.).AssociationforComputational
Linguistics,Singapore,967–976. https://doi.org/10.18653/v1/2023.findings-emnlp.68
KurtBollacker,RobertCook,andPatrickTufts.2007.Freebase:ASharedDatabaseofStructuredGeneralHumanKnowledge.
InProceedingsofthe22ndNationalConferenceonArtificialIntelligence-Volume2(Vancouver,BritishColumbia,Canada)
(AAAI’07).AAAIPress,1962–1963.
LichangChen,ShiyangLi,JunYan,HaiWang,KalpaGunaratna,VikasYadav,ZhengTang,VijaySrinivasan,Tianyi
Zhou,HengHuang,andHongxiaJin.2024. AlpaGasus:TrainingaBetterAlpacawithFewerData.InTheTwelfth
InternationalConferenceonLearningRepresentations,ICLR2024,Vienna,Austria,May7-11,2024.OpenReview.net.
https://openreview.net/forum?id=FdVXgSJhvz
ZicanDong,TianyiTang,JunyiLi,WayneXinZhao,andJi-RongWen.2024. BAMBOO:AComprehensiveBenchmark
forEvaluatingLongTextModelingCapacitiesofLargeLanguageModels.InProceedingsofthe2024JointInternational
ConferenceonComputationalLinguistics,LanguageResourcesandEvaluation(LREC-COLING2024),NicolettaCalzolari,
Min-YenKan,VeroniqueHoste,AlessandroLenci,SakrianiSakti,andNianwenXue(Eds.).ELRAandICCL,Torino,Italia,
2086–2099. https://aclanthology.org/2024.lrec-main.188
MohamedElaraby,MengyinLu,JacobDunn,XueyingZhang,YuWang,andShizhuLiu.2023. Halo:Estimationand
ReductionofHallucinationsinOpen-SourceWeakLargeLanguageModels. CoRR abs/2308.11764(2023). https:
//doi.org/10.48550/ARXIV.2308.11764arXiv:2308.11764
GitHub.2024.Drowzee. https://github.com/security-pride/Drowzee.
ZhibinGou,ZhihongShao,YeyunGong,YelongShen,YujiuYang,NanDuan,andWeizhuChen.2024. CRITIC:Large
LanguageModelsCanSelf-CorrectwithTool-InteractiveCritiquing.InTheTwelfthInternationalConferenceonLearning
Representations,ICLR2024,Vienna,Austria,May7-11,2024.OpenReview.net. https://openreview.net/forum?id=Sx038qxjek
SimengHan,HaileySchoelkopf,YilunZhao,ZhentingQi,MartinRiddell,LukeBenson,LucySun,EkaterinaZubova,Yujie
Qiao,MatthewBurtell,DavidPeng,JonathanFan,YixinLiu,BrianWong,MalcolmSailor,AnsongNi,LinyongNan,
JungoKasai,TaoYu,RuiZhang,ShafiqR.Joty,AlexanderR.Fabbri,WojciechKryscinski,XiVictoriaLin,CaimingXiong,
andDragomirRadev.2022.FOLIO:NaturalLanguageReasoningwithFirst-OrderLogic.CoRRabs/2209.00840(2022).
https://doi.org/10.48550/ARXIV.2209.00840arXiv:2209.00840
hiyouga.2023.FastEdit:EditingLLMswithin10Seconds.https://github.com/hiyouga/FastEdit.
XinyiHou,YanjieZhao,YueLiu,ZhouYang,KailongWang,LiLi,XiapuLuo,DavidLo,JohnC.Grundy,andHaoyuWang.
2023.LargeLanguageModelsforSoftwareEngineering:ASystematicLiteratureReview.CoRRabs/2308.10620(2023).
https://doi.org/10.48550/ARXIV.2308.10620arXiv:2308.10620
LeiHuang,WeijiangYu,WeitaoMa,WeihongZhong,ZhangyinFeng,HaotianWang,QianglongChen,WeihuaPeng,
XiaochengFeng,BingQin,andTingLiu.2023. ASurveyonHallucinationinLargeLanguageModels:Principles,
Taxonomy,Challenges,andOpenQuestions.CoRRabs/2311.05232(2023). https://doi.org/10.48550/ARXIV.2311.05232
arXiv:2311.05232
AlbertQ.Jiang,AlexandreSablayrolles,ArthurMensch,ChrisBamford,DevendraSinghChaplot,DiegodeLasCasas,
FlorianBressand,GiannaLengyel,GuillaumeLample,LucileSaulnier,LélioRenardLavaud,Marie-AnneLachaux,Pierre
Stock,TevenLeScao,ThibautLavril,ThomasWang,TimothéeLacroix,andWilliamElSayed.2023.Mistral7B.CoRR
abs/2310.06825(2023). https://doi.org/10.48550/ARXIV.2310.06825arXiv:2310.06825
AlbertQ.Jiang,AlexandreSablayrolles,AntoineRoux,ArthurMensch,BlancheSavary,ChrisBamford,DevendraSingh
Chaplot,DiegodeLasCasas,EmmaBouHanna,FlorianBressand,GiannaLengyel,GuillaumeBour,GuillaumeLample,
LélioRenardLavaud,LucileSaulnier,Marie-AnneLachaux,PierreStock,SandeepSubramanian,SophiaYang,Szymon
Proc.ACMProgram.Lang.,Vol.8,No.OOPSLA2,Article336.Publicationdate:October2024.

Drowzee:MetamorphicTestingforFact-ConflictingHallucinationDetectioninLargeLanguageModels 336:27
Antoniak,TevenLeScao,ThéophileGervet,ThibautLavril,ThomasWang,TimothéeLacroix,andWilliamElSayed.
2024.MixtralofExperts.CoRRabs/2401.04088(2024). https://doi.org/10.48550/ARXIV.2401.04088arXiv:2401.04088
JeanKaddour,JoshuaHarris,MaximilianMozes,HerbieBradley,RobertaRaileanu,andRobertMcHardy.2023.Challenges
andApplicationsofLargeLanguageModels.CoRRabs/2307.10169(2023). https://doi.org/10.48550/ARXIV.2307.10169
arXiv:2307.10169
HaoqiangKangandXiao-YangLiu.2023.DeficiencyofLargeLanguageModelsinFinance:AnEmpiricalExaminationof
Hallucination.CoRRabs/2311.15548(2023). https://doi.org/10.48550/ARXIV.2311.15548arXiv:2311.15548
Pierre-SimonLaplace.1951.APhilosophicalEssayonProbabilities.DoverPublications,NewYork. Originallypublishedin
1814as"EssaiPhilosophiquesurlesProbabilités".
JunyiLi,XiaoxueCheng,XinZhao,Jian-YunNie,andJi-RongWen.2023a.HaluEval:ALarge-ScaleHallucinationEvaluation
BenchmarkforLargeLanguageModels.InProceedingsofthe2023ConferenceonEmpiricalMethodsinNaturalLanguage
Processing,EMNLP2023,Singapore,December6-10,2023,HoudaBouamor,JuanPino,andKalikaBali(Eds.).Association
forComputationalLinguistics,6449–6464. https://doi.org/10.18653/V1/2023.EMNLP-MAIN.397
KennethLi,OamPatel,FernandaB.Viégas,HanspeterPfister,andMartinWattenberg.2023b.Inference-TimeIntervention:
ElicitingTruthfulAnswersfromaLanguageModel.InAdvancesinNeuralInformationProcessingSystems36:Annual
ConferenceonNeuralInformationProcessingSystems2023,NeurIPS2023,NewOrleans,LA,USA,December10-16,2023,
AliceOh,TristanNaumann,AmirGloberson,KateSaenko,MoritzHardt,andSergeyLevine(Eds.). http://papers.nips.
cc/paper_files/paper/2023/hash/81b8390039b7302c909cb769f8b6cd93-Abstract-Conference.html
KeLiang,LingyuanMeng,MengLiu,YueLiu,WenxuanTu,SiweiWang,SihangZhou,XinwangLiu,andFuchunSun.2022.
ReasoningoverDifferentTypesofKnowledgeGraphs:Static,TemporalandMulti-Modal.CoRRabs/2212.05767(2022).
https://doi.org/10.48550/ARXIV.2212.05767arXiv:2212.05767
HunterLightman,VineetKosaraju,YuriBurda,HarrisonEdwards,BowenBaker,TeddyLee,JanLeike,JohnSchulman,Ilya
Sutskever,andKarlCobbe.2024.Let’sVerifyStepbyStep.InTheTwelfthInternationalConferenceonLearningRepresen-
tations,ICLR2024,Vienna,Austria,May7-11,2024.OpenReview.net. https://openreview.net/forum?id=v8L0pN6EOi
StephanieLin,JacobHilton,andOwainEvans.2022.TruthfulQA:MeasuringHowModelsMimicHumanFalsehoods.In
Proceedingsofthe60thAnnualMeetingoftheAssociationforComputationalLinguistics(Volume1:LongPapers),Smaranda
Muresan,PreslavNakov,andAlineVillavicencio(Eds.).AssociationforComputationalLinguistics,Dublin,Ireland,
3214–3252. https://doi.org/10.18653/v1/2022.acl-long.229
KevinMeng,DavidBau,AlexAndonian,andYonatanBelinkov.2022.LocatingandEditingFactualAssociationsinGPT.In
AdvancesinNeuralInformationProcessingSystems35:AnnualConferenceonNeuralInformationProcessingSystems2022,
NeurIPS2022,NewOrleans,LA,USA,November28-December9,2022,SanmiKoyejo,S.Mohamed,A.Agarwal,DanielleBel-
grave,K.Cho,andA.Oh(Eds.). http://papers.nips.cc/paper_files/paper/2022/hash/6f1d43d5a82a37e89b0665b33bf3a182-
Abstract-Conference.html
KevinMeng,ArnabSenSharma,AlexJ.Andonian,YonatanBelinkov,andDavidBau.2023. Mass-EditingMemoryina
Transformer.InTheEleventhInternationalConferenceonLearningRepresentations,ICLR2023,Kigali,Rwanda,May1-5,
2023.OpenReview.net. https://openreview.net/forum?id=MkbcAHIYgyS
GeorgeA.Miller.1995. WordNet:ALexicalDatabaseforEnglish. Commun.ACM 38,11(nov1995),39–41. https:
//doi.org/10.1145/219717.219748
SewonMin,KalpeshKrishna,XinxiLyu,MikeLewis,Wen-tauYih,PangWeiKoh,MohitIyyer,LukeZettlemoyer,and
HannanehHajishirzi.2023.FActScore:Fine-grainedAtomicEvaluationofFactualPrecisioninLongFormTextGeneration.
InProceedingsofthe2023ConferenceonEmpiricalMethodsinNaturalLanguageProcessing,EMNLP2023,Singapore,
December6-10,2023,HoudaBouamor,JuanPino,andKalikaBali(Eds.).AssociationforComputationalLinguistics,
12076–12100. https://doi.org/10.18653/V1/2023.EMNLP-MAIN.741
SeungwhanMoon,PararthShah,AnujKumar,andRajenSubba.2019.OpenDialKG:ExplainableConversationalReasoning
withAttention-basedWalksoverKnowledgeGraphs.InProceedingsofthe57thConferenceoftheAssociationforComputa-
tionalLinguistics,ACL2019,Florence,Italy,July28-August2,2019,Volume1:LongPapers,AnnaKorhonen,DavidR.Traum,
andLluísMàrquez(Eds.).AssociationforComputationalLinguistics,845–854. https://doi.org/10.18653/V1/P19-1081
TheoOlausson,AlexGu,BenLipkin,CedegaoZhang,ArmandoSolar-Lezama,JoshuaTenenbaum,andRogerLevy.
2023. LINC:ANeurosymbolicApproachforLogicalReasoningbyCombiningLanguageModelswithFirst-Order
LogicProvers.InProceedingsofthe2023ConferenceonEmpiricalMethodsinNaturalLanguageProcessing,Houda
Bouamor,JuanPino,andKalikaBali(Eds.).AssociationforComputationalLinguistics,Singapore,5153–5176. https:
//doi.org/10.18653/v1/2023.emnlp-main.313
OpenAI. 2023. GPT-4 Technical Report. CoRR abs/2303.08774 (2023). https://doi.org/10.48550/ARXIV.2303.08774
arXiv:2303.08774
AnkitPal,LogeshKumarUmapathi,andMalaikannanSankarasubbu.2023.Med-HALT:MedicalDomainHallucinationTest
forLargeLanguageModels.InProceedingsofthe27thConferenceonComputationalNaturalLanguageLearning,CoNLL
2023,Singapore,December6-7,2023,JingJiang,DavidReitter,andShuminDeng(Eds.).AssociationforComputational
Proc.ACMProgram.Lang.,Vol.8,No.OOPSLA2,Article336.Publicationdate:October2024.

336:28 NingkeLi,YuekangLi,YiLiu,LingShi,KailongWang,andHaoyuWang
Linguistics,314–334. https://doi.org/10.18653/V1/2023.CONLL-1.21
LiangmingPan,AlonAlbalak,XinyiWang,andWilliamWang.2023.Logic-LM:EmpoweringLargeLanguageModelswith
SymbolicSolversforFaithfulLogicalReasoning.InFindingsoftheAssociationforComputationalLinguistics:EMNLP2023,
HoudaBouamor,JuanPino,andKalikaBali(Eds.).AssociationforComputationalLinguistics,Singapore,3806–3824.
https://doi.org/10.18653/v1/2023.findings-emnlp.248
EricPrud’hommeauxandAndySeaborne.2018. SPARQLQueryLanguageforRDF-W3Crecommendation. https:
//www.w3.org/TR/rdf-sparql-query/.
YifuQiu,ZhengZhao,YftahZiser,AnnaKorhonen,EdoardoPonti,andShayCohen.2024. AreLargeLanguageModel
TemporallyGrounded?.InProceedingsofthe2024ConferenceoftheNorthAmericanChapteroftheAssociationfor
ComputationalLinguistics:HumanLanguageTechnologies(Volume1:LongPapers),KevinDuh,HelenaGomez,andSteven
Bethard(Eds.).AssociationforComputationalLinguistics,MexicoCity,Mexico,7064–7083. https://doi.org/10.18653/v1/
2024.naacl-long.391
NilsReimersandIrynaGurevych.2019.Sentence-BERT:SentenceEmbeddingsusingSiameseBERT-Networks.InProceedings
ofthe2019ConferenceonEmpiricalMethodsinNaturalLanguageProcessingandthe9thInternationalJointConferenceon
NaturalLanguageProcessing,EMNLP-IJCNLP2019,HongKong,China,November3-7,2019,KentaroInui,JingJiang,Vincent
Ng,andXiaojunWan(Eds.).AssociationforComputationalLinguistics,3980–3990. https://doi.org/10.18653/V1/D19-1410
PhilippeRemy.2020.PythonwrapperforStanfordOpenIE.https://github.com/philipperemy/Stanford-OpenIE-Python.
HongyuRenandJureLeskovec.2020.BetaEmbeddingsforMulti-HopLogicalReasoninginKnowledgeGraphs. https:
//proceedings.neurips.cc/paper/2020/hash/e43739bba7cdb577e9e3e4e42447f5a5-Abstract.html
SatoshiTajiri.2023.Pokemon.https://www.pokemon.com/us.
ScienceDirect.2023.JaccardSimilarity.https://www.sciencedirect.com/topics/computer-science/jaccard-similarity.
ScienceDirect.2024.FriedmanTest.https://www.sciencedirect.com/topics/biochemistry-genetics-and-molecular-biology/
friedman-test.
AbigailSee,PeterJ.Liu,andChristopherD.Manning.2017. GetToThePoint:SummarizationwithPointer-Generator
Networks.InProceedingsofthe55thAnnualMeetingoftheAssociationforComputationalLinguistics(Volume1:LongPapers),
ReginaBarzilayandMin-YenKan(Eds.).AssociationforComputationalLinguistics,Vancouver,Canada,1073–1083.
https://doi.org/10.18653/v1/P17-1099
MohammedLatifSiddiqandJoannaC.S.Santos.2023.GenerateandPray:UsingSALLMStoEvaluatetheSecurityofLLM
GeneratedCode.CoRRabs/2311.00889(2023). https://doi.org/10.48550/ARXIV.2311.00889arXiv:2311.00889
FabianM.Suchanek,GjergjiKasneci,andGerhardWeikum.2007. Yago:acoreofsemanticknowledge.InProceedings
ofthe16thInternationalConferenceonWorldWideWeb,WWW2007,Banff,Alberta,Canada,May8-12,2007,CareyL.
Williamson,MaryEllenZurko,PeterF.Patel-Schneider,andPrashantJ.Shenoy(Eds.).ACM,697–706. https://doi.org/10.
1145/1242572.1242667
KatherineTian,EricMitchell,HuaxiuYao,ChristopherD.Manning,andChelseaFinn.2024.Fine-TuningLanguageModels
forFactuality.InTheTwelfthInternationalConferenceonLearningRepresentations,ICLR2024,Vienna,Austria,May7-11,
2024.OpenReview.net. https://openreview.net/forum?id=WPZ2yPag4K
LingTian,XueZhou,Yan-PingWu,Wang-TaoZhou,Jin-HaoZhang,andTian-ShuZhang.2022. Knowledgegraph
andknowledgereasoning:Asystematicreview. JournalofElectronicScienceandTechnology 20,2(2022),100159.
https://doi.org/10.1016/j.jnlest.2022.100159
HugoTouvron,LouisMartin,KevinStone,PeterAlbert,AmjadAlmahairi,YasmineBabaei,NikolayBashlykov,Soumya
Batra,PrajjwalBhargava,ShrutiBhosale,DanBikel,LukasBlecher,CristianCanton-Ferrer,MoyaChen,Guillem
Cucurull,DavidEsiobu,JudeFernandes,JeremyFu,WenyinFu,BrianFuller,CynthiaGao,VedanujGoswami,Naman
Goyal,AnthonyHartshorn,SagharHosseini,RuiHou,HakanInan,MarcinKardas,ViktorKerkez,MadianKhabsa,
IsabelKloumann,ArtemKorenev,PunitSinghKoura,Marie-AnneLachaux,ThibautLavril,JenyaLee,DianaLiskovich,
YinghaiLu,YuningMao,XavierMartinet,TodorMihaylov,PushkarMishra,IgorMolybog,YixinNie,AndrewPoulton,
JeremyReizenstein,RashiRungta,KalyanSaladi,AlanSchelten,RuanSilva,EricMichaelSmith,RanjanSubramanian,
XiaoqingEllenTan,BinhTang,RossTaylor,AdinaWilliams,JianXiangKuan,PuxinXu,ZhengYan,IliyanZarov,
YuchenZhang,AngelaFan,MelanieKambadur,SharanNarang,AurélienRodriguez,RobertStojnic,SergeyEdunov,
andThomasScialom.2023. Llama2:OpenFoundationandFine-TunedChatModels. CoRRabs/2307.09288(2023).
https://doi.org/10.48550/ARXIV.2307.09288arXiv:2307.09288
NeerajVarshney,WenlinYao,HongmingZhang,JianshuChen,andDongYu.2023.AStitchinTimeSavesNine:Detecting
andMitigatingHallucinationsofLLMsbyValidatingLow-ConfidenceGeneration.CoRRabs/2307.03987(2023). https:
//doi.org/10.48550/ARXIV.2307.03987arXiv:2307.03987
TuVu,MohitIyyer,XuezhiWang,NoahConstant,JerryW.Wei,JasonWei,ChrisTar,Yun-HsuanSung,DennyZhou,
QuocV.Le,andThangLuong.2024.FreshLLMs:RefreshingLargeLanguageModelswithSearchEngineAugmentation.
InFindingsoftheAssociationforComputationalLinguistics,ACL2024,Bangkok,Thailandandvirtualmeeting,August11-16,
2024,Lun-WeiKu,AndreMartins,andVivekSrikumar(Eds.).AssociationforComputationalLinguistics,13697–13720.
Proc.ACMProgram.Lang.,Vol.8,No.OOPSLA2,Article336.Publicationdate:October2024.

Drowzee:MetamorphicTestingforFact-ConflictingHallucinationDetectioninLargeLanguageModels 336:29
https://aclanthology.org/2024.findings-acl.813
PengWang,NingyuZhang,BozhongTian,ZekunXi,YunzhiYao,ZiwenXu,MengruWang,ShengyuMao,Xiaohan
Wang,SiyuanCheng,KangweiLiu,YuanshengNi,GuozhouZheng,andHuajunChen.2024.EasyEdit:AnEasy-to-use
KnowledgeEditingFrameworkforLargeLanguageModels.InProceedingsofthe62ndAnnualMeetingoftheAssociation
forComputationalLinguistics(Volume3:SystemDemonstrations),YixinCao,YangFeng,andDeyiXiong(Eds.).Association
forComputationalLinguistics,Bangkok,Thailand,82–93. https://aclanthology.org/2024.acl-demos.9
ShufanWang,LaureThompson,andMohitIyyer.2021.Phrase-BERT:ImprovedPhraseEmbeddingsfromBERTwithan
ApplicationtoCorpusExploration.InProceedingsofthe2021ConferenceonEmpiricalMethodsinNaturalLanguage
Processing,EMNLP2021,VirtualEvent/PuntaCana,DominicanRepublic,7-11November,2021,Marie-FrancineMoens,
XuanjingHuang,LuciaSpecia,andScottWen-tauYih(Eds.).AssociationforComputationalLinguistics,10837–10851.
https://doi.org/10.18653/V1/2021.EMNLP-MAIN.846
JanWielemaker,ZhishengHuang,andLourensvanderMeij.2008.SWI-Prologandtheweb.TheoryPract.Log.Program.8,
3(2008),363–392. https://doi.org/10.1017/S1471068407003237
HanxiangXu,ShenaoWang,NingkeLi,KailongWang,YanjieZhao,KaiChen,TingYu,YangLiu,andHaoyuWang.
2024. LargeLanguageModelsforCyberSecurity:ASystematicLiteratureReview. CoRR abs/2405.04760(2024).
https://doi.org/10.48550/ARXIV.2405.04760arXiv:2405.04760
MingkeYang,YuqiChen,YiLiu,andLingShi.2024a. DistillSeq:AFrameworkforSafetyAlignmentTestinginLarge
LanguageModelsusingKnowledgeDistillation.InProceedingsofthe33rdACMSIGSOFTInternationalSymposiumon
SoftwareTestingandAnalysis(Vienna,Austria)(ISSTA2024).AssociationforComputingMachinery,NewYork,NY,USA,
578–589. https://doi.org/10.1145/3650212.3680304
ZonglinYang,LiDong,XinyaDu,HaoCheng,ErikCambria,XiaodongLiu,JianfengGao,andFuruWei.2024b.Language
ModelsasInductiveReasoners.InProceedingsofthe18thConferenceoftheEuropeanChapteroftheAssociationforCom-
putationalLinguistics(Volume1:LongPapers),YvetteGrahamandMatthewPurver(Eds.).AssociationforComputational
Linguistics,St.Julian’s,Malta,209–225. https://aclanthology.org/2024.eacl-long.13
ZhilinYang,PengQi,SaizhengZhang,YoshuaBengio,WilliamW.Cohen,RuslanSalakhutdinov,andChristopherD.
Manning.2018.HotpotQA:ADatasetforDiverse,ExplainableMulti-hopQuestionAnswering.InProceedingsofthe2018
ConferenceonEmpiricalMethodsinNaturalLanguageProcessing,Brussels,Belgium,October31-November4,2018,Ellen
Riloff,DavidChiang,JuliaHockenmaier,andJun’ichiTsujii(Eds.).AssociationforComputationalLinguistics,2369–2380.
https://doi.org/10.18653/V1/D18-1259
YifanYao,JinhaoDuan,KaidiXu,YuanfangCai,ZhiboSun,andYueZhang.2024. Asurveyonlargelanguagemodel
(LLM)securityandprivacy:TheGood,TheBad,andTheUgly.High-ConfidenceComputing4,2(2024),100211. https:
//doi.org/10.1016/j.hcc.2024.100211
XiYe,QiaochuChen,IsilDillig,andGregDurrett.2023.SatLM:Satisfiability-AidedLanguageModelsUsingDeclarative
Prompting.InAdvancesinNeuralInformationProcessingSystems36:AnnualConferenceonNeuralInformationPro-
cessingSystems2023,NeurIPS2023,NewOrleans,LA,USA,December10-16,2023,AliceOh,TristanNaumann,Amir
Globerson,KateSaenko,MoritzHardt,andSergeyLevine(Eds.). http://papers.nips.cc/paper_files/paper/2023/hash/
8e9c7d4a48bdac81a58f983a64aaf42b-Abstract-Conference.html
ShukangYin,ChaoyouFu,SiruiZhao,TongXu,HaoWang,DianboSui,YunhangShen,KeLi,XingSun,andEnhong
Chen.2023.Woodpecker:HallucinationCorrectionforMultimodalLargeLanguageModels.CoRRabs/2310.16045(2023).
https://doi.org/10.48550/ARXIV.2310.16045arXiv:2310.16045
JifanYu,XiaozhiWang,ShangqingTu,ShulinCao,DanielZhang-Li,XinLv,HaoPeng,ZijunYao,XiaohanZhang,Hanming
Li,ChunyangLi,ZheyuanZhang,YushiBai,YantaoLiu,AmyXin,KaifengYun,LinluGong,NianyiLin,JianhuiChen,
ZhiliWu,YunjiaQi,WeikaiLi,YongGuan,KaishengZeng,JiQi,HailongJin,JinxinLiu,YuGu,YuanYao,NingDing,
LeiHou,ZhiyuanLiu,BinXu,JieTang,andJuanziLi.2024.KoLA:CarefullyBenchmarkingWorldKnowledgeofLarge
LanguageModels.InTheTwelfthInternationalConferenceonLearningRepresentations,ICLR2024,Vienna,Austria,May
7-11,2024.OpenReview.net. https://openreview.net/forum?id=AqN23oqraW
YueZhang,YafuLi,LeyangCui,DengCai,LemaoLiu,TingchenFu,XintingHuang,EnboZhao,YuZhang,YulongChen,
LongyueWang,AnhTuanLuu,WeiBi,FredaShi,andShumingShi.2023. Siren’sSongintheAIOcean:ASurvey
onHallucinationinLargeLanguageModels.CoRRabs/2309.01219(2023). https://doi.org/10.48550/ARXIV.2309.01219
arXiv:2309.01219
ZhiboZhang,WuxiaBai,YuxiLi,MarkHuasongMeng,KailongWang,LingShi,LiLi,JunWang,andHaoyuWang.
2024.GlitchProber:AdvancingEffectiveDetectionandMitigationofGlitchTokensinLargeLanguageModels.CoRR
abs/2408.04905(2024). https://doi.org/10.48550/ARXIV.2408.04905arXiv:2408.04905
ZiliZhou,ShaowuLiu,GuandongXu,andWuZhang.2019. OnCompletingSparseKnowledgeBasewithTransitive
RelationEmbedding.InTheThirty-ThirdAAAIConferenceonArtificialIntelligence,AAAI2019,TheThirty-FirstInnovative
ApplicationsofArtificialIntelligenceConference,IAAI2019,TheNinthAAAISymposiumonEducationalAdvancesin
ArtificialIntelligence,EAAI2019,Honolulu,Hawaii,USA,January27-February1,2019.AAAIPress,3125–3132. https:
Proc.ACMProgram.Lang.,Vol.8,No.OOPSLA2,Article336.Publicationdate:October2024.

336:30 NingkeLi,YuekangLi,YiLiu,LingShi,KailongWang,andHaoyuWang
//doi.org/10.1609/AAAI.V33I01.33013125
AndyZou,LongPhan,SarahChen,JamesCampbell,PhillipGuo,RichardRen,AlexanderPan,XuwangYin,MantasMazeika,
Ann-KathrinDombrowski,ShashwatGoel,NathanielLi,MichaelJ.Byun,ZifanWang,AlexMallen,StevenBasart,Sanmi
Koyejo,DawnSong,MattFredrikson,J.ZicoKolter,andDanHendrycks.2023.RepresentationEngineering:ATop-Down
ApproachtoAITransparency.CoRRabs/2310.01405(2023). https://doi.org/10.48550/ARXIV.2310.01405arXiv:2310.01405
Received2024-04-06;accepted2024-08-18
Proc.ACMProgram.Lang.,Vol.8,No.OOPSLA2,Article336.Publicationdate:October2024.