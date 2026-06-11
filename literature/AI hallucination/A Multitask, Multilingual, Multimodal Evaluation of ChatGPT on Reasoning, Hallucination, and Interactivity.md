A Multitask, Multilingual, Multimodal Evaluation of ChatGPT
on Reasoning, Hallucination, and Interactivity
YejinBang∗ SamuelCahyawijaya NayeonLee WenliangDai DanSu BryanWilie
HolyLovenia ZiweiJi TiezhengYu WillyChung QuyetV.Do YanXu PascaleFung∗
CentreforArtificialIntelligenceResearch(CAiRE)
TheHongKongUniversityofScienceandTechnology
yjbang@connect.ust.hk, pascale@ece.ust.hk
Abstract itsscaleandviaRLHF,hasshownimpressiveabil-
ities in many areas of NLP as well as emergent
This paper proposes a framework for quanti-
abilities. Anotherreasonisthatitsdialoginterface
tatively evaluating interactive LLMs such as
allowsuserstointeractwiththeunderlyingLLM
ChatGPTusingpubliclyavailabledatasets,us-
moreeffectivelyandefficientlyviainteractivechats
ing23datasetscovering8differentcommon
NLPapplicationtasks.Weextensivelyevaluate thatareakintomulti-turnprompting.
themultitask,multilingual,andmulti-modalas- However, despite its powerful abilities, anec-
pectsofChatGPTbasedonthesedatasetsand
dotal reports on ChatGPT consistently showed
anewlydesignedmultimodaldataset. Wefind
remaining challenges - for example, it fails in
that ChatGPT outperforms LLMs with zero-
someelementarymathematical(Gilsonetal.,2022;
shot learning on most tasks and even outper-
forms fine-tuned models on some tasks. We Goldberg, 2023; Frieder et al., 2023; Choi et al.,
findthatitisbetteratunderstandingnon-Latin 2023;Davis,2023b)andcommonsensereasoning
script languages than generating them. It is tasks (Guo et al., 2023; Davis, 2023b); it hallu-
abletogeneratemultimodalcontentfromtex- cinates with human-like fluency and eloquence
tual prompts via an intermediate code gener-
on things that are not based on truth (Shen et al.,
ation step. Moreover, we find that ChatGPT
2023;Thorp,2023;Smith,2023);andasageneral-
is63.41%accurateonaveragein10different
purposelanguagemodeltrainedfromeverythingon
reasoning categories under logical reasoning,
theweb,itslanguagecoverageisquestionable(Lu
non-textualreasoning,andcommonsenserea-
soning,hencemakingitanunreliablereasoner. etal.,2022;Jiaoetal.,2023). Consequently,itis
ChatGPTsuffersfromhallucinationproblems notclearwhatpeoplecanorcannotuseChatGPT
like other LLMs. Finally, the interactive fea- fordespiteitspopularity.
tureofChatGPTenableshumancollaboration
SinceOpenAIneverpublishedanybenchmark-
withtheunderlyingLLMtoimproveitsperfor-
ingresultsonChatGPTatthetime,seeingthisneed,
mance,i.e.,8%ROUGE-1onsummarization
in February 2023, we proposed a comprehensive
and2%ChrF++onmachinetranslation,ina
multi-turn"promptengineering"fashion. We frameworkforquantitativelyevaluatinginteractive
releaseacodeforevaluationsetextraction.1 LLMs such as ChatGPT through standard public
testsetsonmajorNLPtaskssuchasquestionan-
1 Introduction
swering,reasoning,summarization,machinetrans-
ChatGPT is a successor of the large language lation,sentimentanalysis,languageidentification,
model (LLM) InstructGPT (Ouyang et al., 2022) task-orienteddialogue,andmisinformationdetec-
withadialoginterfacethatisfine-tunedusingthe tion. Weevaluateitsmultilingualperformanceas
Reinforcement Learning with Human Feedback wellasvision-languagemultimodalabilities. With
(RLHF)(Christianoetal.,2017)approach. Chat- additionalexperiments,wealsoquantitativelyeval-
GPThasgathered100millionmonthlyactiveusers uateditsprimarylimitationsinreasoningandhal-
in such a short period of time (Hu, 2023) and is lucination. Inaddition,weconductedexperiments
beingusedbybusinessesandconsumersalikefor to test its multi-turn interactivity as a means for
amyriadofmostlytextualtasks. Onereasonforits better prompt engineering. We aimed to provide
unprecedentedpopularityisthatChatGPT,through insightstousersofChatGPTonthestrengthsmen-
tionedaboveandlimitations,aswellashowthey
∗ EqualContribution.
can improve outcomes with interactivity. To the
1https://github.com/HLTCHKUST/chatgpt-evaluat
ion best of our knowledge, this is the first published
675
Proceedingsofthe13thInternationalJointConferenceonNaturalLanguageProcessingandthe3rdConferenceof
theAsia-PacificChapteroftheAssociationforComputationalLinguistics(Volume1:LongPapers),pages675–718
November1–4,2023.©2023AssociationforComputationalLinguistics

benchmarkofChatGPTfromathirdparty. Morere- verifiedfromthesource.
| cently,theGPT-4technicalreport(OpenAI,2023) |     |     |     |     |     |     | Interactivity: |     |     |        |         |             |     |
| ------------------------------------------- | --- | --- | --- | --- | --- | --- | -------------- | --- | --- | ------ | ------- | ----------- | --- |
|                                             |     |     |     |     |     |     |                |     | One | of the | primary | differenti- |     |
publishedanumberofhumantaskbenchmarks. atingfactorsofChatGPTfromitspredecessorsis
The true scope of all emergent capabilities of its multi-turn dialog interactivity. This enables
generativemodels,includingChatGPT,isstillun- ChatGPTtoperformmultipletaskswithinadialog
session. Thereisalsosignificantperformanceim-
| clear. Thus, |     | any benchmarking |     |     | exercise | cannot |     |     |     |     |     |     |     |
| ------------ | --- | ---------------- | --- | --- | -------- | ------ | --- | --- | --- | --- | --- | --- | --- |
be100%“comprehensive”inthescientificsense. provement(8%ROUGE-1onsummarizationand
Weaimtoshownotjustresearchersbutalsousers 2%ChrF++onlow-resourcemachinetranslation)
viamulti-turninteractivityinvariousstandardNLP
| what ChatGPT |     | can and | cannot | do  | by presenting |     |     |     |     |     |     |     |     |
| ------------ | --- | ------- | ------ | --- | ------------- | --- | --- | --- | --- | --- | --- | --- | --- |
tasks. Thisprocessisakintopromptengineering
interpretablebenchmarkingresultsinazero-shot
settingwithoutaccesstoAPIssothatthegeneral withfeedbackfromthesystem.
audiencecanreplicateourevaluationwiththetest
2 Multitask,Multilingual,and
| setswehaveprovidedinazero-shotsetting. |     |     |     |     |     | This |     |     |     |     |     |     |     |
| -------------------------------------- | --- | --- | --- | --- | --- | ---- | --- | --- | --- | --- | --- | --- | --- |
versionofChatGPTis15December2022. MultimodalEvaluationsofChatGPT
The following are the major insights we have 2.1 MultitaskAbilityofChatGPT
gainedfromtheevaluations:
ChatGPThasbecomeverywell-knowninsucha
| Multitask, |     | Multimodal, |     | and | Multilingual: |     |              |     |      |            |        |        |     |
| ---------- | --- | ----------- | --- | --- | ------------- | --- | ------------ | --- | ---- | ---------- | ------ | ------ | --- |
|            |     |             |     |     |               |     | short period | of  | time | to general | public | users, | not |
For9/13NLPdatasets,ChatGPToutperformspre-
|                 |       |                             |               |           |     |           | just those      | who      | are in   | AI, machine |         | learning, | and      |
| --------------- | ----- | --------------------------- | ------------- | --------- | --- | --------- | --------------- | -------- | -------- | ----------- | ------- | --------- | -------- |
| vious LLMs      |       | with zero-shot              |               | learning. | It  | even out- |                 |          |          |             |         |           |          |
|                 |       |                             |               |           |     |           | NLP communities |          | who      | might       | be      | more      | familiar |
| performs        | fully | fine-tuned                  | task-specific |           |     | LMs on 4  |                 |          |          |             |         |           |          |
|                 |       |                             |               |           |     |           | with LLMs.      | One      | of       | the main    | reasons | is        | that, in |
| differenttasks. |       | Inothercases,ChatGPTisonpar |               |           |     |           |                 |          |          |             |         |           |          |
|                 |       |                             |               |           |     |           | addition        | to media | reports, | innumerable |         | use       | cases    |
orslightlylowerthanfullyfine-tunedforspecific
ofChatGPTaresharedbybothnon-academicand
| NLP tasks; | ChatGPT |     | fails | to generalize |     | to low- |     |     |     |     |     |     |     |
| ---------- | ------- | --- | ----- | ------------- | --- | ------- | --- | --- | --- | --- | --- | --- | --- |
academicusersonline(Marr,2022;Gordon,2023;
| resource                              | and | extremely | low-resource |     |     | languages |            |            |         |      |                |         |       |
| ------------------------------------- | --- | --------- | ------------ | --- | --- | --------- | ---------- | ---------- | ------- | ---- | -------------- | ------- | ----- |
|                                       |     |           |              |     |     |           | Shankland, | 2023).     | There   | have | been           | debates | and   |
| (e.g.,Marathi,Sundanese,andBuginese). |     |           |              |     |     | Thereis   |            |            |         |      |                |         |       |
|                                       |     |           |              |     |     |           | panels     | on whether | ChatGPT |      | is approaching |         | Arti- |
anoverallperformancedegradationinlow-resource
|            |              |     |              |     |         |            | ficial General | Intelligence,   |     |     | as it seems   | to  | be able  |
| ---------- | ------------ | --- | ------------ | --- | ------- | ---------- | -------------- | --------------- | --- | --- | ------------- | --- | -------- |
| languages, | especially   |     | in non-Latin |     | scripts | in the     |                |                 |     |     |               |     |          |
|            |              |     |              |     |         |            | to carry       | out a multitude |     | of  | tasks without |     | specific |
| case of    | translation; |     | its weakness |     | lies    | in genera- |                |                 |     |     |               |     |          |
fine-tuning(Desk,2023;Johnson,2023;Kingson,
| tion rather | than | understanding |     | part | of the | transla- |        |        |       |       |           |      |         |
| ----------- | ---- | ------------- | --- | ---- | ------ | -------- | ------ | ------ | ----- | ----- | --------- | ---- | ------- |
|             |      |               |     |      |        |          | 2023). | On the | other | hand, | there has | also | been as |
tionprocess;ChatGPTenablesacodeintermediate
muchsharingofitsfailuresinsimpletasks(Gilson
mediumtobridgevisionandlanguage,eventhough
etal.,2022;Choietal.,2023;Shenetal.,2023).
themulti-modalityabilityisstillelementarycom-
|     |     |     |     |     |     |     | Instead | of relying |     | on anecdotal |     | examples, | we  |
| --- | --- | --- | --- | --- | --- | --- | ------- | ---------- | --- | ------------ | --- | --------- | --- |
paredtovision-languagemodels.
|                                  |     |           |     |              |            |           | first evaluate | ChatGPT’s |          | performance |     | in     | various |
| -------------------------------- | --- | --------- | --- | ------------ | ---------- | --------- | -------------- | --------- | -------- | ----------- | --- | ------ | ------- |
| Reasoning:                       |     | We tested |     | 10 different |            | reasoning |                |           |          |             |     |        |         |
|                                  |     |           |     |              |            |           | standard       | NLP       | tasks in | a zero-shot |     | manner | to ob-  |
| categorieswith634samplesintotal. |     |           |     |              | Basedonour |           |                |           |          |             |     |        |         |
tainabasic/betterunderstandingofitsmulti-task
| experiments, |     | ChatGPT | shows | more | weakness | in  |     |     |     |     |     |     |     |
| ------------ | --- | ------- | ----- | ---- | -------- | --- | --- | --- | --- | --- | --- | --- | --- |
ability. Wecompileresultsfromtheexistinglitera-
inductivereasoningthanindeductiveorabductive
tureonChatGPTandcomparethemwiththestate-
| reasoning. | ChatGPTalsolacksspatialandmathe-  |       |         |     |        |          |                      |                  |     |                          |           |     |        |
| ---------- | --------------------------------- | ----- | ------- | --- | ------ | -------- | -------------------- | ---------------- | --- | ------------------------ | --------- | --- | ------ |
|            |                                   |       |         |     |        |          | of-the-art           | fully-fine-tuned |     | and                      | zero-shot |     | models |
| matical    | reasoning                         | while | showing |     | better | temporal |                      |                  |     |                          |           |     |        |
|            |                                   |       |         |     |        |          | acrossmultipletasks. |                  |     | WeevaluateChatGPTperfor- |           |     |        |
| reasoning. | Further,wefoundthatChatGPTisrela- |       |         |     |        |          |                      |                  |     |                          |           |     |        |
manceson21datasetscovering8tasks,i.e.,sum-
tivelybetteratcommonsensereasoningthannon-
|         |          |            |     |          |       |       | marization,    | machine |            | translation,  | sentiment |           | anal- |
| ------- | -------- | ---------- | --- | -------- | ----- | ----- | -------------- | ------- | ---------- | ------------- | --------- | --------- | ----- |
| textual | semantic | reasoning. |     | Finally, | while | Chat- |                |         |            |               |           |           |       |
|         |          |            |     |          |       |       | ysis, question |         | answering, | task-oriented |           | dialogue, |       |
GPTshowsacceptableperformanceincausaland
open-domainknowledge-groundeddialogue,and
| analogical | reasoning,  |         | it is | bad at   | multi-hop | rea-  |                               |     |     |     |                 |     |     |
| ---------- | ----------- | ------- | ----- | -------- | --------- | ----- | ----------------------------- | --- | --- | --- | --------------- | --- | --- |
|            |             |         |       |          |           |       | misinformationdetectiontasks. |     |     |     | Wesampletesting |     |     |
| soning     | capability, | similar |       | to other | LLMs’     | weak- |                               |     |     |     |                 |     |     |
casesfromexistingstandardtestsetsforeachtask
ness(Ottetal.,2023).
withasamplesizerangingfrom30to200samples.
| Hallucination: |     | Similar |     | to other | LLMs | (Rad- |     |     |     |     |     |     |     |
| -------------- | --- | ------- | --- | -------- | ---- | ----- | --- | --- | --- | --- | --- | --- | --- |
fordetal.,2019;Muennighoffetal.,2022;Work- MultitaskGeneralizationofChatGPT There-
shop et al., 2022), ChatGPT suffers from the hal- sultofthemultitaskevaluationisshowninTable1.
lucination problem. It generates more extrinsic ChatGPTisshowntoachieveremarkablezero-shot
hallucinations–factualstatementsthatcannotbe performances on multiple tasks, surpassing pre-
676

|     |       |     |     |         |        |     |           |     | Fine-Tuned | Zero-Shot |         |     |
| --- | ----- | --- | --- | ------- | ------ | --- | --------- | --- | ---------- | --------- | ------- | --- |
|     | Tasks |     |     | Dataset | Metric |     | Reference |     |            |           | ChatGPT |     |
|     |       |     |     |         |        |     |           |     | SOTA       | SOTA      |         |     |
Summarization CNN/DM ROUGE-1 Lewisetal.(2020a) 44.47 35.27∗ 35.29
|     |     |     | SAMSum          |     | ROUGE-1 |     | Lewisetal.(2020a) |     | 47.28 | -   | 35.29 |     |
| --- | --- | --- | --------------- | --- | ------- | --- | ----------------- | --- | ----- | --- | ----- | --- |
|     | MT  |     | FLoRes-200(HRL) |     | ChrF++  |     | Teametal.(2022)   |     | 63.5  | -   | 58.64 |     |
(XXX→Eng) FLoRes-200(LRL) ChrF++ Teametal.(2022) 54.9 - 27.75
|     | MT  |     | FLoRes-200(HRL) |     | ChrF++ |     | Teametal.(2022) |     | 54.4 | -   | 51.12 |     |
| --- | --- | --- | --------------- | --- | ------ | --- | --------------- | --- | ---- | --- | ----- | --- |
(Eng→XXX) FLoRes-200(LRL) ChrF++ Teametal.(2022) 41.9 - 21.57
|     |     |     | NusaX-Eng |     | MacroF1 |     | Winataetal.(2022) |     | 92.6 | 61.5 | 83.24 |     |
| --- | --- | --- | --------- | --- | ------- | --- | ----------------- | --- | ---- | ---- | ----- | --- |
Sentiment NusaX-Ind MacroF1 Winataetal.(2022) 91.6 59.3 82.13
|     | Analysis |     | NusaX-Jav |     | MacroF1 |     | Winataetal.(2022) |     | 84.2 | 55.7 | 79.64 |     |
| --- | -------- | --- | --------- | --- | ------- | --- | ----------------- | --- | ---- | ---- | ----- | --- |
|     |          |     | NusaX-Bug |     | MacroF1 |     | Winataetal.(2022) |     | 70.0 | 55.9 | 55.84 |     |
bAbItask(15|16) Accuracy Westonetal.(2016a) 100|100 - 93.3|66.7
|     |          |     | EntailmentBank |     | Accuracy |     | Clarketal.(2018)     |     | 86.5 | 78.58 | 93.3 |     |
| --- | -------- | --- | -------------- | --- | -------- | --- | -------------------- | --- | ---- | ----- | ---- | --- |
|     | Question |     | CLUTRR         |     | Accuracy |     | Minervinietal.(2020) |     | 95.0 | 28.6  | 43.3 |     |
Answering StepGame(k=9|k=1) Accuracy MirzaeeandKordjamshidi(2022) 48.4|98.7 - 23.3|63.3
|     |     |     |     | Pep-3k | AUC |     | Poradaetal.(2021) |     | 67.0 | -   | 93.3 |     |
| --- | --- | --- | --- | ------ | --- | --- | ----------------- | --- | ---- | --- | ---- | --- |
Misinformation COVID-Social Accuracy Leeetal.(2021) 77.7 50.0 73.3
Detection COVID-Scientific Accuracy Leeetal.(2021) 74.7 71.1 92.0
|     |     |     | MultiWOZ2.2 |     | JGA |     | Zhaoetal.(2022) |     | 60.6 | 46.7 | 24.4 |     |
| --- | --- | --- | ----------- | --- | --- | --- | --------------- | --- | ---- | ---- | ---- | --- |
Task-Oriented MultiWOZ2.2 BLEU NekvindaandDušek(2021) 19.1 - 5.65
Dialogue
|     |     |     | MultiWOZ2.2 |     | InformRate |     | Yangetal.(2021) |     | 95.7 | -   | 71.1 |     |
| --- | --- | --- | ----------- | --- | ---------- | --- | --------------- | --- | ---- | --- | ---- | --- |
Open-Domain OpenDialKG BLEU|ROUGE-L Jietal.(2022b) 20.8|40.0 3.1|29.5 4.1|18.6
|     | KGD |     | OpenDialKG |     | FeQA |     | Jietal.(2022b) |     | 48.0 | 23.0 | 15.0 |     |
| --- | --- | --- | ---------- | --- | ---- | --- | -------------- | --- | ---- | ---- | ---- | --- |
Table1: PerformanceofChatGPTcomparedtostate-of-the-artfully-fine-tunedmodels(Fine-TunedSOTA)and
LLMinzero-shotsettings(Zero-ShotSOTA).Thereferencedperformancesareevaluationresultsonfulltestsets,
while the ChatGPT performances are computed on subsets of the corresponding dataset using 30 to 200 data
samplesforeachtask. ForMachineTranslation(MT)tasks,wefollowthedefinitionsofhigh-resourcelanguage
(HRL)andlow-resourcelanguage(LRL)fromNLLB(Teametal.,2022)andtakesubsetsoflanguagestorepresent
eachgroup. JGAdenotesjointgoalaccuracy. AverageofperformancesforCNNandDMfromGoyaletal.(2022).
LMs in zero-shot settings are as follows. Summarization: InstructGPT, MT: NLLB-200, Sentiment Analysis:
XLM-RLARGE,QA:ST-MoE-32B,ZeroQA,GPT-3,MisinformationDetection: GPT-2,Task-OrientedDialogue:
D3ST,Open-DomainKGD:GPT-Jurassic-6B.
vious state-of-the-art zero-shot models on 9 out plainedinAppendixC.6.
| of  | 13 evaluation |     | datasets | with | reported zero-shot |     |     |     |     |     |     |     |
| --- | ------------- | --- | -------- | ---- | ------------------ | --- | --- | --- | --- | --- | --- | --- |
LLMs’ performances. In most tasks, especially Knowledge-GroundedOpen-DomainDialogue
task-oriented and knowledge-grounded dialogue ToquantitativelymeasureChatGPT’sperformance
|     |     |     |     |     |     |     | on knowledge-grounded |     | dialogue, |     | we utilize | 50  |
| --- | --- | --- | --- | --- | --- | --- | --------------------- | --- | --------- | --- | ---------- | --- |
tasks,task-specificfully-fine-tunedmodelsoutper-
samplesfromthetestsetofOpenDialKG(Moon
formChatGPT.Comparedtothelatter,ChatGPT
yieldslowerperformanceinmosttaskswhilestill etal.,2019),whichcontainsopen-endeddialogues
surpassingtheperformanceon4datasets. groundedonaknowledgepath. Accordingtohu-
|     |     |     |     |     |     |     | man judgment, | the | responses | from | ChatGPT | are |
| --- | --- | --- | --- | --- | --- | --- | ------------- | --- | --------- | ---- | ------- | --- |
Furthermore,fromtheevaluationresults,wealso
observeseverallimitationsofChatGPT:1)limited ofhighqualitywithfluentresponsegenerationand
languageunderstandingandgenerationcapabilities incorporating the provided knowledge in the re-
|     |              |     |            |     |                   |     | sponse. However,theautomaticevaluationresults |     |     |     |     |     |
| --- | ------------ | --- | ---------- | --- | ----------------- | --- | --------------------------------------------- | --- | --- | --- | --- | --- |
| on  | low-resource |     | languages, | 2)  | lacking reasoning |     |                                               |     |     |     |     |     |
arerelativelylowcomparedwithfine-tunedGPT2.
| ability | as  | shown | from | the results | in QA, | and 3) |     |     |     |     |     |     |
| ------- | --- | ----- | ---- | ----------- | ------ | ------ | --- | --- | --- | --- | --- | --- |
performingtask-orientedandknowledge-grounded We postulate this is because ChatGPT responses
dialoguetasks. Moredetailedexperimentalsetup are longer than the golden answers and include
contentfromitsparametrizedknowledgeinjected
andanalysisforeachtaskaresharedinAppendix
| §C. | We also | provide |     | the complete | list of | all the | duringpre-training. |     |     |     |     |     |
| --- | ------- | ------- | --- | ------------ | ------- | ------- | ------------------- | --- | --- | --- | --- | --- |
datasetsusedinourevaluationinAppendixI.
|     |     |     |     |     |     |     | Task-OrientedDialogue |     |     | Weinvestigateanddis- |     |     |
| --- | --- | --- | --- | --- | --- | --- | --------------------- | --- | --- | -------------------- | --- | --- |
ChatGPTonDialogueTasks GiventhatChat- cusshowChatGPT’semergentabilitiesandinter-
GPThastheabilitytogenerateconversation-like activitycouldpotentiallybeleveragedforToDas
responses,wetestitonconventionaldialoguetasks: wellintwosetups. Firstly,A)modularapproach:
1)knowledge-groundedopen-domaindialogueand testingdialoguestatetracking(DST)andresponse
2) Task-oriented dialogue. Task setups are ex- generationusingoracleactions. DSTismediocre
677

Language Category SAAcc. LIDAcc. Language Category XXX→Eng Eng→XXX
|     | English    |     | HRL   | 84% | 100% |     | Chinese    |     | HRL | 24/30 |     | 14/30 |
| --- | ---------- | --- | ----- | --- | ---- | --- | ---------- | --- | --- | ----- | --- | ----- |
|     | Indonesian |     | MRL   | 80% | 100% |     | French     |     | HRL | 29/30 |     | 25/30 |
|     | Javanese   |     | LRL   | 78% | 0%   |     | Indonesian |     | MRL | 28/30 |     | 19/30 |
|     | Buginese   |     | X-LRL | 56% | 12%  |     | Korean     |     | MRL | 22/30 |     | 12/30 |
|     |            |     |       |     |      |     | Javanese   |     | LRL | 7/30  |     | 6/30  |
|     |            |     |       |     |      |     | Sundanese  |     | LRL | 9/30  |     | 0/30  |
Table2: AccuracyofChatGPTonSentimentAnalysis
(SA)andLanguageIdentification(LID)tasks.
Table3: #CorrecttranslationsofChatGPT.XXXde-
notesthetargetlanguagelistedinthefirstcolumn.
whileChatGPTsuccessfullyleveragesallinforma-
tionprovidedwhileansweringthequestionswitha throughsentimentanalysisandlanguageidentifi-
71.1%informrateand5.65BLEUscore. Next,B) cation tasks. ChatGPT fails to generalize to ex-
| Unifiedapproach: |     |     | adirectapproachtosimulatethe |     |     |                               |     |     |     |     |              |     |
| ---------------- | --- | --- | ---------------------------- | --- | --- | ----------------------------- | --- | --- | --- | --- | ------------ | --- |
|                  |     |     |                              |     |     | tremelylow-resourcelanguages. |     |     |     |     | AsshowninTa- |     |
ToDinteractionwhileleveraginginformationina
|     |     |     |     |     |     | ble | 2, there | is a | clear | correlation | between | Chat- |
| --- | --- | --- | --- | --- | --- | --- | -------- | ---- | ----- | ----------- | ------- | ----- |
structured database. We observed the limitations GPTperformancewiththelanguageresourcecate-
| of  | ChatGPT: | 1) ChatGPT |     | cannot | keep the belief |     |     |     |     |     |     |     |
| --- | -------- | ---------- | --- | ------ | --------------- | --- | --- | --- | --- | --- | --- | --- |
gory. Thisresultalignswiththefindingsfromprior
stateacrossmultipleturnswithintheinteraction,2)
|     |     |     |     |     |     | works | (Chowdhery |     | et  | al., 2022; | Workshop | et al., |
| --- | --- | --- | --- | --- | --- | ----- | ---------- | --- | --- | ---------- | -------- | ------- |
ChatGPT’sresponsetendstobewrongifthequery 2022;Muennighoffetal.,2022),whereLLMs,in-
introducesabasiclevelofreasoning3)ChatGPT cluding ChatGPT, yield a lower performance for
tendstogeneratehallucinatedinformationbeyond
|     |       |            |       |     |                   | lower    | resource |             | languages. | Interestingly, |             | the per- |
| --- | ----- | ---------- | ----- | --- | ----------------- | -------- | -------- | ----------- | ---------- | -------------- | ----------- | -------- |
| the | given | knowledge, | which | is  | not desirable for |          |          |             |            |                |             |          |
|     |       |            |       |     |                   | formance |          | gap between |            | English,       | Indonesian, | and      |
ToD.Weprovidedetailsandexamplesofthemod- Javanese is considered marginal compared to the
ularandunifiedapproachesinAppendixC.6.2.
|     |     |     |     |     |     | performance |         | gap | with         | Buginese. | This            | suggests |
| --- | --- | --- | --- | --- | --- | ----------- | ------- | --- | ------------ | --------- | --------------- | -------- |
|     |     |     |     |     |     | that        | ChatGPT | has | a limitation |           | in generalizing | to-      |
2.2 EvaluatingMultilingualityofChatGPT
|     |     |     |     |     |     | wardextremelylow-resourcelanguages. |     |     |     |     |     | Further- |
| --- | --- | --- | --- | --- | --- | ----------------------------------- | --- | --- | --- | --- | --- | -------- |
Trainingdatasizeaffectslanguageunderstanding more, we also find that ChatGPT can understand
andgenerationabilityofLMs(Raffeletal.,2022;
|     |     |     |     |     |     | low-resource |     | languages, |     | such | as Javanese, | with- |
| --- | --- | --- | --- | --- | --- | ------------ | --- | ---------- | --- | ---- | ------------ | ----- |
Cahyawijayaetal.,2021;Raeetal.,2021;Work- outhavingtheknowledgetoidentifythelanguage
shop et al., 2022; Chowdhery et al., 2022; Hoff- itself. Moreover,ChatGPTdisplaysbetterhuman-
mannetal.,2022). AsanLLM,thesamepremise preferred responses when it has no knowledge
alsoappliestoChatGPT,butthequestionistowhat
|     |     |     |     |     |     | aboutthelanguage. |     |     | Forinstance,asillustratedin |     |     |     |
| --- | --- | --- | --- | --- | --- | ----------------- | --- | --- | --------------------------- | --- | --- | --- |
extent. Weinvestigatethisquestionthroughaseries 8,ChatGPTletstheuserknowthatitspredictionis
ofexperimentsbyanalyzing1)thelanguageunder- uncertainwhenitdoesnotcompletelyunderstand
standingcapabilitythroughsentimentanalysis(SA)
thelanguageandalsoprovidesbroaderinformation
andlanguageidentification(LID)tasks,and2)the regardingthelanguage.
| language |     | generation | capability |     | through machine |     |     |     |     |     |     |     |
| -------- | --- | ---------- | ---------- | --- | --------------- | --- | --- | --- | --- | --- | --- | --- |
2.2.2 LanguageGeneration
| translation |     | using | English | as the | pivot language. |     |     |     |     |     |     |     |
| ----------- | --- | ----- | ------- | ------ | --------------- | --- | --- | --- | --- | --- | --- | --- |
BasedonthesizeproportioninCommonCrawl(i.e., We assess the multilingual language generation
the primary source of language pre-training data ability of ChatGPT through machine translation.
|     |     |     |     |     |     | Weexperimentwith6languages: |     |     |     |     | French,Chinese, |     |
| --- | --- | --- | --- | --- | --- | --------------------------- | --- | --- | --- | --- | --------------- | --- |
usedinvariousLLMs),wegrouplanguagesinto4
languageresourcecategories,i.e.,high-resource Indonesian,Korean,Javanese,andSundanesefrom
language(HRL)(<≥1%),medium-resourcelan- theFLORES-200dataset(Teametal.,2022;Goyal
|     |     |     |     |     |     | et  | al., 2021). | For | each | language, | we  | sample 30 |
| --- | --- | --- | --- | --- | --- | --- | ----------- | --- | ---- | --------- | --- | --------- |
guage(MRL)(≥0.01%),low-resourcelanguage
(LRL)(≥0.0001%),andextremelylow-resource English-XXXparallelsentencesandperformtwo
language(X-LRL)(<0.0001%). Thestatisticsof directionsoftranslationusingEnglishasthepivot
thelanguagesareshowninTable9andotherdetails language. Thecorrectnessofthetranslationresults
|     |     |     |     |     |     | is  | manually | validated |     | by a native | speaker | of the |
| --- | --- | --- | --- | --- | --- | --- | -------- | --------- | --- | ----------- | ------- | ------ |
aredescribedinAppendixD.
correspondinglanguage.
2.2.1 LanguageUnderstanding
Basedonourevaluationresults(Table3),simi-
We investigate the language understanding abil- lartootherLLMs(Workshopetal.,2022;Muen-
ityofChatGPTon4languagesfromdifferentlan- nighoffetal.,2022),ChatGPTproducesbetterEn-
guage categories in NusaX (Winata et al., 2022), glish translation quality from high-resource lan-
i.e. English,Indonesian,Javanese,andBuginese, guages, such as French and Chinese. While for
678

| low-resourcelanguages,suchasJavaneseandSun- |     |     |     |     | Grade | Turn1 |             |       |
| ------------------------------------------- | --- | --- | --- | --- | ----- | ----- | ----------- | ----- |
|                                             |     |     |     |     |       |       | Turn1 Turn2 | Turn3 |
danese, ChatGPT tends to generate several mis- (#ofErrors) (w/odesc)
| translatedwords/phrasesandsometimesevenhal- |                        |     |     |     | A(0) | 0   | 4 12  | 24  |
| ------------------------------------------- | ---------------------- | --- | --- | --- | ---- | --- | ----- | --- |
|                                             |                        |     |     |     | B(1) | 4   | 22 24 | 24  |
| lucinatesomeobjects.                        | Moreover,wealsoobserve |     |     |     |      |     |       |     |
thatsometimesChatGPTtranslatestheEnglishsen- C(2) 16 18 12 10
tence into a different but related language other D(3) 18 24 26 20
|                                          |     |     |      |     | E(≥4) | 62  | 32 26 | 22  |
| ---------------------------------------- | --- | --- | ---- | --- | ----- | --- | ----- | --- |
| thantherequestedtargetlanguage(see§H.2). |     |     | This |     |       |     |       |     |
factsuggeststhatthegeneralizationofLLMs,in-
Table4: Resultsoftheportion(%)ofgeneratedflags
| cluding ChatGPT, | to low-resource | languages, | re- |     |     |     |     |     |
| ---------------- | --------------- | ---------- | --- | --- | --- | --- | --- | --- |
evaluatedintofivegrades,A∼E.Thesecondcolumn
| mainsanopenchallenge. |     | Moreover,wealsofind |     |     |     |     |     |     |
| --------------------- | --- | ------------------- | --- | --- | --- | --- | --- | --- |
showstheresultsofanablationstudy,whichremoves
that ChatGPT can handle Latin script languages thestepofflagdescriptiongenerationanddirectlyasks
betterthannon-Latinscriptlanguages,especially ChatGPTtogeneratetheSVGcodeoftheflagimage.
ingeneratingsentencesusingthosescripts.
2.3 EvaluatingMultimodalityofChatGPT
SinceChatGPTisapurelytext-promptedlanguage
model,itisunlikelytoexploreitsmultimodalcapa-
bilitieswithvisualinputslikecontemporaryvision-
| language works | (Rombach | et al., 2022; | Ramesh |     |     |     |     |     |
| -------------- | -------- | ------------- | ------ | --- | --- | --- | --- | --- |
etal.,2021;Yuetal.,2021a;Radfordetal.,2021;
| Dai et al., 2022;  | Lovenia    | et al., 2022;           | Dai et al., |     |     |     |     |     |
| ------------------ | ---------- | ----------------------- | ----------- | --- | --- | --- | --- | --- |
| 2023a). However,   | thanks     | to its code understand- |             |     |     |     |     |     |
| ing and generation | abilities, | programming             | codes       |     |     |     |     |     |
canserveastheintermediatemediumtobridgevi-
sionandlanguage(Rasheed,2020;Shiryaev,2022).
Giventextualprompts,ChatGPTcangeneratecode Figure1: AnexampleofaGermanflagdrawnbyChat-
|                 |           |              |         | GPT | using | SVG format: | (top) without | and (bottom) |
| --------------- | --------- | ------------ | ------- | --- | ----- | ----------- | ------------- | ------------ |
| representations | of visual | images using | the SVG |     |       |             |               |              |
(Scalable Vector Graphics) format or APIs (e.g., withaself-retrievedtextualdescriptionoftheflag. A
renderedimageisshowninplaceofthegeneratedSVG
| HTML Canvas | element, | Python Turtle | graphics). |     |     |     |     |     |
| ----------- | -------- | ------------- | ---------- | --- | --- | --- | --- | --- |
formatforthesakeofsimplicity.
Forexample,asshowninFigure1,ChatGPTcan
generateawell-formedandsuitableintermediate tests how ChatGPT’s textually described knowl-
representationincodeformattosynthesizeimages
edge(language)convertsintothedrawing(vision)
giventhedialoguecontextanduserprompts.
throughtheSVG(code),usingmulti-turnconversa-
In this way, even though the generated images tions. Thetaskcontainsthreesteps. Firstly,weask
aresymbolicandtheirqualityisnotcomparableto ChatGPT to illustrate the appearance of the flag.
theonesgeneratedbymoderntext-to-imagemod- Next, based on the description, we ask ChatGPT
els(Rameshetal.,2021;Rombachetal.,2022),it to generate the SVG code of that flag. Finally, if
isworthexploringduetothreereasons. Firstly,it thegeneratedimagecontainserrors,weiteratively
helps us investigate the visual understanding and askChatGPTtofixthem. Therearefourtypesof
reasoningabilitiesofChatGPT,whichcanbeseen
errors: 1)layout,2)color,3)missingcomponents,
asanemergentskillaftertheverylarge-scalepre- 4) shape/size. We uniformly collect 50 national
trainingontextandcodedata. Furthermore,repre- flagsfromdifferentcontinentsandconducttheflag-
sentingimageswithcodeisamoreexplainableway
|     |     |     |     | drawing | task | on ChatGPT. | The prompts | and full |
| --- | --- | --- | --- | ------- | ---- | ----------- | ----------- | -------- |
tounderstandthemodel’sbehaviorsandrationales results are shown in Appendix E. The generated
in text-to-image generation. Third, it is a natural flag images are evaluated by the aforementioned
waytoevaluateChatGPT’sabilityonmulti-turnin- four error types as criteria. We further assess the
teractionbyaskingforpost-editingandcorrections
imagequalitywithfivegrades,A∼E,whichindi-
ofthegeneratedimages. catezerotofour(orabove)errors. Anoverviewof
Tosystematicallyevaluatetheimagegeneration theresultevaluationisprovidedinTable4.
ability of ChatGPT through code generation, we Weshareourmajortwofindingsfromthetask:
designed a national flag drawing task. This task 1) ChatGPT is capable of drawing, yet better
679

with a self-generated textual description. As Thus, we investigate the reasoning ability of
demonstrated in Table 4 and Appendix E, by fol- ChatGPTinamorefine-grainedmanner,whichin-
lowingthetaskformulation,ChatGPTcangenerate cludesdeductive,inductive,abductive,analogical,
plausiblenationalflagsusingtheSVGformat. To causal,multi-hop,mathematical,temporal,andspa-
better understand the behavior of ChatGPT, we tial reasoning, via question-answering tasks. We
performanablationstudybyremovingthedescrip- categorizeavailableQAtasksintoeachcategoryby
tion generation step. As illustrated by Figure 1, avoidingoverlap(i.e.,choosingtestsetsthatrequire
the performance drops dramatically without first mainlyonespecificcategoryofreasoning). Com-
prompting the textual flag description, which is posedresultsandcorrespondingdatasetsforeach
generated by ChatGPT itself. Explicitly describ- categoryareshowninTable5. Forevaluation,we
ing the appearance of the flag and then drawing manuallychecktheaccuracyoftheansweraswell
disentanglestheimagegenerationprocess,which asverifytherationalesandexplanationsgenerated
can be considered as a chain-of-thought reason- byChatGPT.Adetailedexplanationoftasksetup
ing. 2) ChatGPT is an elementary illustrator. isexplainedinAppendix F.
Amongthefourerrortypes,themajorityliesinthe
shape/sizeerror, whichhappens68%ofthetime. LogicalReasoning Inductive,deductive,andab-
Fortheotherthreeerrortypes(layout,color,miss- ductive reasoning are common forms of logical
ingcomponents),theyappear34%,20%,and18% reasoning, a process of deriving a conclusion or
of the time, respectively. For instance, ChatGPT judgmentbasedongivenevidenceorpastexperi-
cannotgeneratetheexactshapeofthemapleleafin enceandobservations(Rogersetal.,2022;Wason
theCanadianflagwhileitgetsthelayoutandcolor andJohnson-Laird,1972;HuangandChang,2022).
correctly (Figure 3). This is a natural defect of WefirstinvestigatebasicreasoningskillswithbAbI
text-onlylanguagemodelsastheyneverseeactual tasks (Weston et al., 2016b), 30 examples each
visualdataandtextualdataisusuallyconceptual. from task 15 (inductive) and task 16 (deductive).
OnemajorinvestigationisthatChatGPTisalazy
3 ReasoningEvaluationsofChatGPT reasoner that suffers more from induction. Inter-
estingly, when ChatGPT was asked to answer a
Reasoning is one of the most actively discussed question given premises without any prompt en-
anddebatedabilitiesofLLMsasscalingthemodel gineering,itperformedpoorlyininduction(0out
parameter size also increases the implicit knowl- of30)whileitachievedmuchbetterperformance
edge in LLMs (Wei et al., 2022a; Wang et al., indeduction(19outof30). However,whenChat-
2022; Huang and Chang, 2022). Mahowald et al. GPT is explicitly asked for reasonable inference
eloquentlyarguesthat“languageabilitydoesnot inductivereasoningincreasesto20outof30. Yet,
equal to thinking” or “reasoning” in LLMs, and itisstillnotasgoodasindeduction. Whenwere-
thatLLMshavepoorreasoningskillsdespitepos- peattheanalysisonadvancedtasks,specificallyon
sessinghuman-levellanguageskills. CLUTRR(Sinhaetal.,2019)forinductionandEn-
IntheNLPliterature,evaluatingamodel’srea- tailmentBankfordeduction(Dalvietal.,2021),the
soningoftenmeansevaluatingitsvariousskillsin sameconclusionholdsbasedonourexperiment.
arithmetic,commonsense,andsymbolicreasoning
indifferentNLPtasksthatrequiresuchskills(Tal- Non-textual semantic reasoning It is often in-
moretal.,2020;Zelikmanetal.,2022;Weietal., vestigatedinpublicsharingaboutChatGPTerrors
2022b). However, the reasoning itself is a much casesthatitlacksthereasoningabilitythatrequires
broaderconceptthusitishardtoconcludewhether non-textsemanticunderstandingsuchasmathemat-
amodelcan“reason”ornotbasedonthoseafore- ical,temporal,andspatialreasoning. Notsurpris-
mentioned, and current works on reasoning are ingly, it could only score 23.33% (7/30) for the
scattered. Thisisinlinewiththeanecdotalexpe- MATH dataset (Saxton et al., 2019), which tests
rience of users with ChatGPT – some of the ex- mathematical reasoning. Overall, ChatGPT cor-
amplesdemonstratesurprisinglygood“reasoning” rectlyanswers86.67%ofthetime(26/30),suggest-
abilitiescomparedtopreviouslyintroducedLLMs ingthatithasadecenttemporalreasoningability.
butatthesametimeChatGPTfailsinverysimple ChatGPTfallsshortofthespatialreasoningtasks,
reasoningproblems(the,2023;Venuto,2023;Qiao with success rates of 43.33% for StepGame and
etal.,2022;Cookup.ai,2022;Labs,2022). 43.75%forSpartQA.Weinvestigatetheerrorsthat
680

Categories Testset Result tively. In comparison to its previously reported
EntailmentBank 28/30 performance, ChatGPT’s performance on covid-
Deductive
|     |     |     | bAbI(task15) |     | 28/30(as-is:19/30) |     |            |                |     |                |     |     |          |
| --- | --- | --- | ------------ | --- | ------------------ | --- | ---------- | -------------- | --- | -------------- | --- | --- | -------- |
|     |     |     |              |     |                    |     | scientific | is impressive. |     | Interestingly, |     |     | for more |
|     |     |     | CLUTRR       |     | 13/30              |     |            |                |     |                |     |     |          |
Inductive
bAbI(task16) 20/30(as-is:0/30) societal-relatedclaims,ChatGPToftenrefusesto
Abductive αNLI 26/30 make verification. However, it cannot avoid the
Mathematical Math 13/30 criticismthatparameterizedknowledgeisobtained
|     | Temporal |     | Timedial |     | 26/30 |     |     |     |     |     |     |     |     |
| --- | -------- | --- | -------- | --- | ----- | --- | --- | --- | --- | --- | --- | --- | --- |
bybettermemorizationasitstillshowsworseper-
|     |     |     | SpartQA(hard|basic) |     | 8/32|20/32 |     |     |     |     |     |     |     |     |
| --- | --- | --- | ------------------- | --- | ---------- | --- | --- | --- | --- | --- | --- | --- | --- |
StepGame(hard|basic) 7/30|19/30 formanceinquestionsdesignedtocauseimitative
Spatial StepGame(cardinal) 17/20 falsehoods. Weteston66testsamplesfromTruth-
|     |     |     | StepGame(diagonal) |     | 11/20 |     |     |     |     |     |     |     |     |
| --- | --- | --- | ------------------ | --- | ----- | --- | --- | --- | --- | --- | --- | --- | --- |
StepGame(clock) 5/20 fulQA(Linetal.,2022),whichteststheextentof
|     |             |     | CommonsenseQA |     | 27/30 |     | LLMstomimichumanfalsehoodand35.38%of |     |     |     |     |     |     |
| --- | ----------- | --- | ------------- | --- | ----- | --- | ------------------------------------ | --- | --- | --- | --- | --- | --- |
|     | Commonsense |     | PIQA          |     | 25/30 |     |                                      |     |     |     |     |     |     |
thetimeChatGPTfailstoanswertruthfully.
|     |           |     | Pep-3k(Hard) |     | 28/30 |     |               |     |                              |     |     |     |     |
| --- | --------- | --- | ------------ | --- | ----- | --- | ------------- | --- | ---------------------------- | --- | --- | --- | --- |
|     | Causal    |     | E-Care       |     | 24/30 |     |               |     |                              |     |     |     |     |
|     |           |     |              |     |       |     | Hallucination |     | Fromvarioustasks,weoftenfind |     |     |     |     |
|     | Multi-hop |     | hotpotQA     |     | 8/30  |     |               |     |                              |     |     |     |     |
Analogical Letterstringanalogy 30/30 extrinsichallucinations,includingbothuntruthful
andfactualones,acrossvarioustaskssuchasMa-
|     | Table5: | Composedresultsforallreasoningtasks. |     |     |     |     |     |     |     |     |     |     |     |
| --- | ------- | ------------------------------------ | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
chineTranslationandquestionanswering,which
|     |     |     |     |     |     |     | causes degradation |     | in  | performance. |     | The | intrin- |
| --- | --- | --- | --- | --- | --- | --- | ------------------ | --- | --- | ------------ | --- | --- | ------- |
itoftenfailstounderstandclockdirection(e.g.,“W
|     |     |     |     |     |     |     | sic hallucinations |     | are | barely | found | as discussed |     |
| --- | --- | --- | --- | --- | --- | --- | ------------------ | --- | --- | ------ | ----- | ------------ | --- |
isatK’s3o’clock”)anddiagonalspatialrelations.
|     |     |     |     |     |     |     | in tasks | about | summarization |     |     | and knowledge- |     |
| --- | --- | --- | --- | --- | --- | --- | -------- | ----- | ------------- | --- | --- | -------------- | --- |
Commonsense Reasoning grounded open-domain dialogue. We share ex-
It is understanding
andreasoningabouteverydayconceptsandknowl- amplesofthesehallucinationtypesdetectedfrom
differenttaskexplorationsinTable19.
| edge | that | most | people | are familiar | with, | to  |     |     |     |     |     |     |     |
| ---- | ---- | ---- | ------ | ------------ | ----- | --- | --- | --- | --- | --- | --- | --- | --- |
makejudgmentsandpredictionsaboutnewsitua-
|                          |     |     |     |                     |     |     | 5 EvaluatingInteractivityinChatGPT |     |     |     |     |     |     |
| ------------------------ | --- | --- | --- | ------------------- | --- | --- | ---------------------------------- | --- | --- | --- | --- | --- | --- |
| tions(Storksetal.,2019). |     |     |     | Recentworksshowthat |     |     |                                    |     |     |     |     |     |     |
LLMsperformimpressivelywelloncommonsense
|           |     |            |     |          |            |       | ChatGPT | has | a built-in | interactive |     | ability | thanks |
| --------- | --- | ---------- | --- | -------- | ---------- | ----- | ------- | --- | ---------- | ----------- | --- | ------- | ------ |
| reasoning |     | benchmarks |     | (Qiao et | al., 2022; | Huang |         |     |            |             |     |         |        |
toconversationaldatafine-tuningandRLHF.We
| andChang,2022;BhargavaandNg,2022). |     |     |     |     |     | Based |     |     |     |     |     |     |     |
| ---------------------------------- | --- | --- | --- | --- | --- | ----- | --- | --- | --- | --- | --- | --- | --- |
furtherdelveintothebenefitofexploitingthisinter-
onourevaluationwithCommonsenseQA(Talmor
activeabilityofChatGPTinthreeNLPtasks,sum-
| et  | al., 2018), |     | PiQA (Bisk | et al., | 2020) and | Pep- |             |         |     |              |     |                |     |
| --- | ----------- | --- | ---------- | ------- | --------- | ---- | ----------- | ------- | --- | ------------ | --- | -------------- | --- |
|     |             |     |            |         |           |      | marization, | machine |     | translation, |     | and multimodal |     |
3k(Wangetal.,2018b),ChatGPTshowssurpris- generation. Ourexperimentsdemonstratethepo-
inglygoodcommonsensereasoningcapability,per-
tentialofemployingmulti-turninteractiontorefine
hapsduetoitslargeparametricmemory.
thequalityofthegeneratedresponsesandimprove
thetaskperformanceofChatGPT.
4 FactualityandHallucination
|             |     |            |       |              |               |        | Interactivity |     | on Summarization |     |           | Summariza-  |     |
| ----------- | --- | ---------- | ----- | ------------ | ------------- | ------ | ------------- | --- | ---------------- | --- | --------- | ----------- | --- |
| LLMs        | are | known      | to be | susceptible  | to generating |        |               |     |                  |     |           |             |     |
|             |     |            |       |              |               |        | tion models   | aim | to extract       |     | essential | information |     |
| nonfactual, |     | untruthful |       | information, | which         | is re- |               |     |                  |     |           |             |     |
fromdocumentsandtogenerateshort,concise,and
ferredtoashallucination(Leeetal.,2022;Jietal.,
|     |     |     |     |     |     |     | readabletext(Yuetal.,2021b;Suetal.,2021). |     |     |     |     |     | In  |
| --- | --- | --- | --- | --- | --- | --- | ----------------------------------------- | --- | --- | --- | --- | --- | --- |
2022a,b;Suetal.,2022;Daietal.,2023b;Xuetal.,
|     |     |     |     |     |     |     | real-world | applications, |     | people | may | want | to im- |
| --- | --- | --- | --- | --- | --- | --- | ---------- | ------------- | --- | ------ | --- | ---- | ------ |
2023). ManyanecdotalwitnessesshowChatGPT
provethesummarybasedonthepreviouslygener-
alsoseemstosufferfromthesameproblemasother
|     |     |     |     |     |     |     | ated summary. |     | We ran | experiments |     | with | 50 doc- |
| --- | --- | --- | --- | --- | --- | --- | ------------- | --- | ------ | ----------- | --- | ---- | ------- |
LLMs. ToevaluatethisaspectofChatGPT,wefirst
|         |     |          |               |     |        |           | uments    | from SAMSum |     | (Gliwa    | et     | al., 2019) | and |
| ------- | --- | -------- | ------------- | --- | ------ | --------- | --------- | ----------- | --- | --------- | ------ | ---------- | --- |
| explore |     | existing | fact-checking |     | and QA | test sets |           |             |     |           |        |            |     |
|         |     |          |               |     |        |           | conducted | a two-turn  |     | iterative | prompt | approach.  |     |
andalsoillustratethechallengeofhallucinationin
|     |     |     |     |     |     |     | ChatGPT | usually | generates |     | an overly | long | sum- |
| --- | --- | --- | --- | --- | --- | --- | ------- | ------- | --------- | --- | --------- | ---- | ---- |
ChatGPTbysharinghallucinationexamples.
|     |     |     |     |     |     |     | mary. Byaddingafollow-uppromptafterthefirst |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | ------------------------------------------- | --- | --- | --- | --- | --- | --- |
Factuality WeevaluateChatGPTwithtestsets summary,“Please make the summary shorter”,
thatconsistofscientificandsocialclaimsrelated ChatGPTcouldprovideamuchshortersummary
toCOVID-19(Leeetal.,2021). ChatGPTisable thanthefirstresponse. Experimentalresultsshow
todetectmisinformation92%(46/50)and73.33% thatwiththesecondlengthcontrolprompt,there-
(22/30, excluding verification-refusing cases) ac- fined summaries achieve 7.99 and 1.64 gains on
curacyoncovid-scientificandcovid-socialrespec- ROUGE-1andROUGE-2respectively.
681

| Figure2:        | Resultofthemulti-turnMT-APEexperiment. |         |        |            |            |     |     |     |     |     |     |     |
| --------------- | -------------------------------------- | ------- | ------ | ---------- | ---------- | --- | --- | --- | --- | --- | --- | --- |
| #Correct        | MT denotes                             | the     | number | of correct | transla-   |     |     |     |     |     |     |     |
| tions. #Correct | APE                                    | denotes | the    | number     | of correct |     |     |     |     |     |     |     |
translationsafterpost-editing.
| Interactivity | on  | Machine | Translation |     | One of |     |     |     |     |     |     |     |
| ------------- | --- | ------- | ----------- | --- | ------ | --- | --- | --- | --- | --- | --- | --- |
thecapabilitiesofChatGPTistoperformtexttrans-
| lationfromonelanguagetoanother. |     |     |     | Withthein- |     |     |     |     |     |     |     |     |
| ------------------------------- | --- | --- | --- | ---------- | --- | --- | --- | --- | --- | --- | --- | --- |
teractivityofChatGPT,weexplorethepossibility
Figure3:
ChangesinChatGPT’sdrawingoftheCana-
ofperformingacombinedmachinetranslationand
|     |     |     |     |     |     | dian flag over | three | turns. | Layout, | color, | completion, |     |
| --- | --- | --- | --- | --- | --- | -------------- | ----- | ------ | ------- | ------ | ----------- | --- |
automaticpost-editingtaskstoimprovethetrans- andshape/sizearemarkedas(cid:33)iftheyalignwiththose
lationqualityofChatGPT.Fortheexperiment,we ofthegroundtruth,and✗
otherwise.
| adaptthedatasetusedin§2.2.2. |     |     |     | AsshowninFig- |     |     |     |     |     |     |     |     |
| ---------------------------- | --- | --- | --- | ------------- | --- | --- | --- | --- | --- | --- | --- | --- |
ure2,despitethetranslationandpost-editingbeing varioustasksandevensurpassesfine-tunedmodels
doneusingasingleChatGPTmodel,themulti-turn onsometasks. However,therearestillsomefailure
approachmethodhelpstoimprovethecorrectness cases(§2.1)anditproducesresponseswithaltered
ofthetranslationbymakingpartialcorrectionsor nuanceandmeaning. Therefore,dealingwiththese
|           |             |     |             |     |         | special cases | is  | a complex | but | important |     | task. In |
| --------- | ----------- | --- | ----------- | --- | ------- | ------------- | --- | --------- | --- | --------- | --- | -------- |
| even full | corrections | in  | some cases. | We  | provide |               |     |           |     |           |     |          |
experimentalsetupdetailsandexamplesofthepost- termsofmultilinguality,ChatGPTachievesstrong
| editinginAppendixJ. |     |            |            |     |     | performanceinmanyhigh-resourceandmedium- |            |               |               |     |          |       |
| ------------------- | --- | ---------- | ---------- | --- | --- | ---------------------------------------- | ---------- | ------------- | ------------- | --- | -------- | ----- |
|                     |     |            |            |     |     | resource                                 | languages. |               | Nevertheless, |     | ChatGPT  | still |
| Interactivity       | on  | Multimodal | Generation |     | The |                                          |            |               |               |     |          |       |
|                     |     |            |            |     |     | lacks the                                | ability    | to understand |               | and | generate | sen-  |
multi-turninteractionabilityofChatGPTenables
tencesinlow-resourcelanguages(§2.2),whichis
| the refinement | of  | text-to-image |     | generation. | It is |                |     |        |               |     |               |     |
| -------------- | --- | ------------- | --- | ----------- | ----- | -------------- | --- | ------ | ------------- | --- | ------------- | --- |
|                |     |               |     |             |       | also supported |     | by Lai | et al.(2023). |     | Additionally, |     |
oneofthemostnaturalwaysforhumanstocreate
ChatGPTlacksthegenerationabilityofnon-Latin
artworkorproductdesignsbyrequestinganAItool
scriptlanguages(§2.2.2),despitethelanguagesbe-
| iteratively. | ThroughinteractionwithChatGPTover |     |     |     |     |                   |     |                            |     |     |     |     |
| ------------ | --------------------------------- | --- | --- | --- | --- | ----------------- | --- | -------------------------- | --- | --- | --- | --- |
|              |                                   |     |     |     |     | inghigh-resource. |     | Theseraisetheconcernoflan- |     |     |     |     |
multipleturns,aprocessofcreatinganinteresting
guagediversityandinclusivityinChatGPT(Joshi
paintingcanbeachieved(Figure7).
|     |     |     |     |     |     | et al., 2020; | Aji | et al., | 2022). | Regarding |     | multi- |
| --- | --- | --- | --- | --- | --- | ------------- | --- | ------- | ------ | --------- | --- | ------ |
Toquantitativelystudyhowthisabilityimpacts
|     |     |     |     |     |     | modality, | our | flag drawing |     | experiments |     | showed |
| --- | --- | --- | --- | --- | --- | --------- | --- | ------------ | --- | ----------- | --- | ------ |
imagegeneration,weconductatmostthreerounds
|                                       |     |     |     |     |         | thepotentialofChatGPT’smultimodalability. |     |     |     |     |     | It  |
| ------------------------------------- | --- | --- | --- | --- | ------- | ----------------------------------------- | --- | --- | --- | --- | --- | --- |
| ofpost-editingfortheflag-drawingtask. |     |     |     |     | Asshown |                                           |     |     |     |     |     |     |
wouldbeaninterestingresearchdirectiontofurther
inFigure4,inthefirstroundofgeneration,Chat-
|     |     |     |     |     |     | explore ChatGPT’s |     | multimodal |     | ability | to  | answer |
| --- | --- | --- | --- | --- | --- | ----------------- | --- | ---------- | --- | ------- | --- | ------ |
GPTrarelygenerateserrorlessSVGimagesexcept
“cantextualmodelslikeChatGPTswitchtoamul-
forsomesimpleflags(e.g.,NigerianandGerman).
timodalbackbone?”
Weobservethat34%and36%ofsamplesexperi-
enceimprovement(i.e.,fewererrors)fromturn1to Reasoning TheimpressiveperformanceofChat-
| 2andfromturn2to3,respectively. |     |     |     | Wealsotested |     |         |         |          |     |           |     |       |
| ------------------------------ | --- | --- | --- | ------------ | --- | ------- | ------- | -------- | --- | --------- | --- | ----- |
|                                |     |     |     |              |     | GPT has | sparked | interest | in  | expanding | its | usage |
withtheInstructGPT,whichhasthesamebackbone
|     |     |     |     |     |     | beyond traditional |     | NLP | tasks | into | more complex |     |
| --- | --- | --- | --- | --- | --- | ------------------ | --- | --- | ----- | ---- | ------------ | --- |
modelasChatGPTbutlacksconversationability.
domainsrequiringsophisticatedreasoningsuchas
InstructGPTcannotachievesalientimprovements problem-solving, decision-making, andplanning.
| by directly | putting | the | intermediate | results | in the |     |     |     |     |     |     |     |
| ----------- | ------- | --- | ------------ | ------- | ------ | --- | --- | --- | --- | --- | --- | --- |
Ourevaluationofitsreasoningabilitiesshowsthat
inputcontext(AppendixH.3).
|     |     |     |     |     |     | theyarenotreliable. |     |     | Specifically,ourfindingsindi- |     |     |     |
| --- | --- | --- | --- | --- | --- | ------------------- | --- | --- | ----------------------------- | --- | --- | --- |
catethatChatGPTexhibitsatendencytobealazy
6 ConclusionandDiscussion
|     |     |     |     |     |     | reasoner | and that | its | capabilities | are | inconsistent |     |
| --- | --- | --- | --- | --- | --- | -------- | -------- | --- | ------------ | --- | ------------ | --- |
Multitask,Multilingual,Multimodal ChatGPT acrossvariousreasoningabilities; Tosupportthe
outperformsSOTALLMsinazero-shotmanneron furtherexpansionofitsusecases,itisnecessaryto
682

prioritizethedevelopmentofsystemswithrobust entityrecognitionandetc. Ourpaperprovidesan
complexreasoningcapabilities,whichshouldalso easier-to-followguideline.
befacilitatedbythecreationofmorecomprehen- Duetothepagelimit,manypartsoftheexper-
sivebenchmarksforassessingtheseabilities,such imental setup details are added to the Appendix
asworksbyLaskaretal.(2023b);Qinetal.(2023);
whiletheoverallstructureofevaluationandmajor
Davis(2023a),particularlywhenmultipleabilities insightsstayinthemaincontent. Thismaycause
arerequiredtocompletethetasks. thereaderinconveniencetofollowtheexperiments.
However,wepubliclyreleasethecodebasethatcan
| Factuality&Hallucinations |     |     | ChatGPT,likeother |     |     |     |     |     |     |     |     |     |
| ------------------------- | --- | --- | ----------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
helpthecommunityreplicatetheexactsameevalu-
| LLMs, still | makes | things | up  | (Ji et | al., 2022a). |     |     |     |     |     |     |     |
| ----------- | ----- | ------ | --- | ------ | ------------ | --- | --- | --- | --- | --- | --- | --- |
ationeitheronChatGPTorotherLLMseasily.
| To ensure                                   | factuality, | it is        | possible | to build | LLMs      |                 |     |     |     |     |     |     |
| ------------------------------------------- | ----------- | ------------ | -------- | -------- | --------- | --------------- | --- | --- | --- | --- | --- | --- |
| withaninterfacetoanexternalknowledgesource, |             |              |          |          |           | EthicsStatement |     |     |     |     |     |     |
| like Blenderbot                             |             | 3.0 (Shuster |          | et al.,  | 2022) and |                 |     |     |     |     |     |     |
LaMDa(Thoppilanetal.,2022). Meanwhile,there Responsible Generative AI Previous works
aremanyformsofhallucinationsthatarenotnec- have discussed the ethical implications or con-
essarily counterfactual but still undesirable. The cerns associated with ChatGPT (and other
RLHFprocessofChatGPTcanensurehumanfeed- LLMs) (Jabotinsky and Sarel, 2022; Susnjak,
backtomitigateundesirableresponses. However, 2022; Blanco-Gonzalez et al., 2022; Aydın and
|     |     |     |     |     |     | Karaarslan,2022;Jeblicketal.,2022). |     |     |     |     | Agreeing |     |
| --- | --- | --- | --- | --- | --- | ----------------------------------- | --- | --- | --- | --- | -------- | --- |
researchersneedtoworkoncomingupwithmore
automaticandscalablemethodstodetectandmiti- withthepreviousliterature,theresponsibledesign
gatehallucinationsandotherundesirableartifacts. and usage of LLMs including ChatGPT is an im-
|               |                              |     |     |     |     | portant | and pressing |     | challenge | today. | There | are |
| ------------- | ---------------------------- | --- | --- | --- | --- | ------- | ------------ | --- | --------- | ------ | ----- | --- |
| Interactivity | ComparedwiththepreviousLLMs, |     |     |     |     |         |              |     |           |        |       |     |
commonissueswiththesemodels,suchasfairness,
theinteractiveabilityofChatGPThasmadealeap
toxicity,demographicbias,andsafety,whichneed
accordingtobothqualitativeandquantitativemea-
|     |     |     |     |     |     | to be addressed. |     | In  | the case | of  | ChatGPT, | Ope- |
| --- | --- | --- | --- | --- | --- | ---------------- | --- | --- | -------- | --- | -------- | ---- |
sures. Through interactivity, ChatGPT can recite nAI constructs safety layers and uses RLHF and
| from its      | own description, |     | which       | is a | very impor-  |             |            |          |     |        |                 |          |
| ------------- | ---------------- | --- | ----------- | ---- | ------------ | ----------- | ---------- | -------- | --- | ------ | --------------- | -------- |
|               |                  |     |             |      |              | potentially | other      | means    | to  | filter | out undesirable |          |
| tant ability. | A similar        |     | exploration | of   | this ability |             |            |          |     |        |                 |          |
|               |                  |     |             |      |              | system      | responses. | However, |     | this   | is still        | not per- |
inLLMshasalsobeenexploredinotherresearch fectandrequiresfutureresearchtofurtherimprove
| works(Sunetal.,2022;Wangetal.,2023). |     |     |     |     | How- |                                |     |     |     |     |               |     |
| ------------------------------------ | --- | --- | --- | --- | ---- | ------------------------------ | --- | --- | --- | --- | ------------- | --- |
|                                      |     |     |     |     |      | therobustnessofthesafetylayer. |     |     |     |     | Thisprocessis |     |
ever,sometimesChatGPTretainsthewronganswer
|            |           |          |     |        |            | resource-intensive |     | and | opaque | to  | the public. | We  |
| ---------- | --------- | -------- | --- | ------ | ---------- | ------------------ | --- | --- | ------ | --- | ----------- | --- |
| even after | receiving | multiple |     | rounds | of prompts |                    |     |     |        |     |             |     |
hopetoseeamoreopendiscussionandsharingof
fromtheuser. ImprovingtheabilityofChatGPTto responsibledesignofLLMsfromvariousorganiza-
handlemultipleroundsofuserfeedbackisalsoan
tionsincludingOpenAIinthefuture.
importantchallenge.
|                 |     |          |      |        |          | UseofScientificArtifacts/Data             |                               |     |     |     | Thispapercon- |     |
| --------------- | --- | -------- | ---- | ------ | -------- | ----------------------------------------- | ----------------------------- | --- | --- | --- | ------------- | --- |
| Limitation      |     |          |      |        |          | ductsanevaluationofChatGPTforacademicpur- |                               |     |     |     |               |     |
|                 |     |          |      |        |          | posesonly.                                | Wecomplywiththetermsandcondi- |     |     |     |               |     |
| The experiments |     | are done | with | the UI | of Chat- |                                           |                               |     |     |     |               |     |
tionsofChatGPTstatedinhttps://openai.com
| GPT provided | by     | OpenAI      | (15 | December | 2019      |                         |         |          |     |           |      |             |
| ------------ | ------ | ----------- | --- | -------- | --------- | ----------------------- | ------- | -------- | --- | --------- | ---- | ----------- |
|              |        |             |     |          |           | /policies/terms-of-use. |         |          |     | Moreover, |      | we com-     |
| version),    | before | the ChatGPT |     | API was  | released, |                         |         |          |     |           |      |             |
|              |        |             |     |          |           | ply with                | all the | licenses | of  | all the   | data | (i.e., test |
thus,thenumberofsamplesforevaluationislim-
sets/benchmarks)thatareusedinthisevaluation.
| ited(30-200).   | However,tasksofevaluationshould |         |     |         |            |     |     |     |     |     |     |     |
| --------------- | ------------------------------- | ------- | --- | ------- | ---------- | --- | --- | --- | --- | --- | --- | --- |
| not be affected | much                            | because |     | most of | the recent |     |     |     |     |     |     |     |
Acknowledgments
updates/releasesofChatGPTarerelatedtosafety
concerns. Moreover,Itispossibletoaugmentour This work has been partially funded by
benchmarks with other technical benchmarks for MRP/055/18 of the Innovation Technology
research purposes, especially now that the Chat- Commission, Hong Kong SAR Government; the
GPT APIs are available. There has been recent Hong Kong Fellowship Scheme by the Hong
automaticorhuman-in-the-loopevaluationssuch KongResearchGrantsCouncil,andPF20-43679
as (Laskar et al., 2023a) Nevertheless, many of HongKongPhDFellowshipScheme,HongKong
the benchmarks are not necessarily interpretable ResearchGrantsCouncil.
tolaypeopleforgeneralpurposes,suchasnamed
683

References
SamuelCahyawijaya,HolyLovenia,AlhamFikriAji,
GentaIndraWinata,BryanWilie,RahmadMahendra,
| 2023. Chatgptvssatyanadellaoverbiryani: |     |     |     |     | Thechat- |     |     |     |     |     |     |
| --------------------------------------- | --- | --- | --- | --- | -------- | --- | --- | --- | --- | --- | --- |
ChristianWibisono,AdeRomadhony,KarissaVin-
botislearningfromitsmistakes.
centio,FajriKoto,JenniferSantoso,DavidMoeljadi,
Alham Fikri Aji, Genta Indra Winata, Fajri Koto, CahyaWirawan,FrederikusHudi,IvanHalimParmo-
SamuelCahyawijaya,AdeRomadhony,RahmadMa- nangan,IkaAlfina,MuhammadSatrioWicaksono,Il-
hamFirdausiPutra,SamsulRahmadani,YuliantiOe-
| hendra, | Kemal | Kurniawan, | David | Moeljadi, | Radi- |     |     |     |     |     |     |
| ------- | ----- | ---------- | ----- | --------- | ----- | --- | --- | --- | --- | --- | --- |
nang,AliAkbarSeptiandri,JamesJaya,KaustubhD.
| tyo Eko                 | Prasojo, | Timothy | Baldwin,            | Jey | Han Lau, |        |                |     |          |       |              |
| ----------------------- | -------- | ------- | ------------------- | --- | -------- | ------ | -------------- | --- | -------- | ----- | ------------ |
|                         |          |         |                     |     |          | Dhole, | Arie Ardiyanti |     | Suryani, | Rifki | Afina Putri, |
| andSebastianRuder.2022. |          |         | Onecountry,700+lan- |     |          |        |                |     |          |       |              |
guages: NLP challenges for underrepresented lan- DanSu,KeithStevens,MadeNindyatamaNityasya,
guages and dialects in Indonesia. In Proceedings MuhammadFaridAdilazuarda,RyanIgnatius,Ryan-
ditoDiandaru,TiezhengYu,VitoGhifari,Wenliang
| of the 60th | Annual | Meeting | of  | the Association | for |     |     |     |     |     |     |
| ----------- | ------ | ------- | --- | --------------- | --- | --- | --- | --- | --- | --- | --- |
Dai,YanXu,DyahDamapuspita,CukTho,Ichwanul
| ComputationalLinguistics(Volume1: |     |     |     | LongPapers), |     |                 |     |                      |     |     |       |
| --------------------------------- | --- | --- | --- | ------------ | --- | --------------- | --- | -------------------- | --- | --- | ----- |
|                                   |     |     |     |              |     | MuslimKaroKaro, |     | TiranaNoorFatyanosa, |     |     | Ziwei |
pages7226–7249,Dublin,Ireland.Associationfor
Ji,PascaleFung,GrahamNeubig,TimothyBaldwin,
ComputationalLinguistics.
SebastianRuder,HerrySujaini,SakrianiSakti,and
ÖmerAydınandEnisKaraarslan.2022. Openaichatgpt Ayu Purwarianti. 2022. Nusacrowd: Open source
generatedliteraturereview:Digitaltwininhealthcare. initiativeforindonesiannlpresources.
AvailableatSSRN4308687.
SamuelCahyawijaya,GentaIndraWinata,BryanWilie,
| SatanjeevBanerjeeandAlonLavie.2005. |        |     |     |            | METEOR:  |                 |            |          |          |              |            |
| ----------------------------------- | ------ | --- | --- | ---------- | -------- | --------------- | ---------- | -------- | -------- | ------------ | ---------- |
|                                     |        |     |     |            |          | Karissa         | Vincentio, | Xiaohong |          | Li, Adhiguna | Kun-       |
| An automatic                        | metric | for | MT  | evaluation | with im- |                 |            |          |          |              |            |
|                                     |        |     |     |            |          | coro, Sebastian |            | Ruder,   | Zhi Yuan | Lim,         | Syafri Ba- |
InPro-
provedcorrelationwithhumanjudgments. har,MasayuKhodra,AyuPurwarianti,andPascale
ceedingsoftheACLWorkshoponIntrinsicandEx- Fung.2021. IndoNLG:Benchmarkandresourcesfor
trinsic Evaluation Measures for Machine Transla- evaluating Indonesian natural language generation.
tionand/orSummarization,pages65–72,AnnArbor, Proceedings of the 2021 Conference on Empiri-
In
| Michigan. | Association |     | for Computational |     | Linguis- |     |     |     |     |     |     |
| --------- | ----------- | --- | ----------------- | --- | -------- | --- | --- | --- | --- | --- | --- |
calMethodsinNaturalLanguageProcessing,pages
tics.
8875–8898,OnlineandPuntaCana,DominicanRe-
public.AssociationforComputationalLinguistics.
| PaulBartha.2013.     |     | Analogyandanalogicalreasoning. |     |       |           |                                 |     |     |     |              |     |
| -------------------- | --- | ------------------------------ | --- | ----- | --------- | ------------------------------- | --- | --- | --- | ------------ | --- |
|                      |     |                                |     |       |           | EthanC.ChauandNoahA.Smith.2021. |     |     |     | Specializing |     |
| Chandra Bhagavatula, |     | Ronan                          | Le  | Bras, | Chaitanya |                                 |     |     |     |              |     |
Malaviya,KeisukeSakaguchi,AriHoltzman,Han- multilinguallanguagemodels: Anempiricalstudy.
nahRashkin,DougDowney,WentauYih,andYejin InProceedingsofthe1stWorkshoponMultilingual
RepresentationLearning,pages51–61,PuntaCana,
| Choi.2020. | Abductivecommonsensereasoning. |     |     |     | In  |     |     |     |     |     |     |
| ---------- | ------------------------------ | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
DominicanRepublic.AssociationforComputational
| International | Conference |     | on Learning |     | Representa- |     |     |     |     |     |     |
| ------------- | ---------- | --- | ----------- | --- | ----------- | --- | --- | --- | --- | --- | --- |
Linguistics.
tions.
Prajjwal Bhargava and Vincent Ng. 2022. Common- JonathanHChoi,KristinEHickman,AmyMonahan,
senseknowledgereasoningandgenerationwithpre- and Daniel Schwarcz. 2023. Chatgpt goes to law
trainedlanguagemodels: asurvey. InProceedings school. AvailableatSSRN.
| of the AAAI | Conference |     | on Artificial |     | Intelligence, |     |     |     |     |     |     |
| ----------- | ---------- | --- | ------------- | --- | ------------- | --- | --- | --- | --- | --- | --- |
AakankshaChowdhery,SharanNarang,JacobDevlin,
volume36,pages12317–12325.
|     |     |     |     |     |     | Maarten | Bosma, | Gaurav | Mishra, | Adam | Roberts, |
| --- | --- | --- | --- | --- | --- | ------- | ------ | ------ | ------- | ---- | -------- |
PushpakBhattacharyya,RajenChatterjee,MarkusFre-
|     |     |     |     |     |     | Paul Barham, | Hyung | Won | Chung, | Charles | Sutton, |
| --- | --- | --- | --- | --- | --- | ------------ | ----- | --- | ------ | ------- | ------- |
itag, Diptesh Kanojia, Matteo Negri, and Marco Sebastian Gehrmann, Parker Schuh, Kensen Shi,
Turchi.2022. Findingsofthewmt2022sharedtask Sasha Tsvyashchenko, Joshua Maynez, Abhishek
on automatic post-editing. In Proceedings of the Rao, Parker Barnes, Yi Tay, Noam Shazeer, Vin-
SeventhConferenceonMachineTranslation,pages
|     |     |     |     |     |     | odkumar | Prabhakaran, |     | Emily | Reif, Nan | Du, Ben |
| --- | --- | --- | --- | --- | --- | ------- | ------------ | --- | ----- | --------- | ------- |
109–117,AbuDhabi.
|     |     |     |     |     |     | Hutchinson, | Reiner | Pope, | James | Bradbury, | Jacob |
| --- | --- | --- | --- | --- | --- | ----------- | ------ | ----- | ----- | --------- | ----- |
Austin,MichaelIsard,GuyGur-Ari,PengchengYin,
| DavidG.W.Birch.2022. |     | Chatgptisawindowintothe |     |     |     |            |        |           |     |        |           |
| -------------------- | --- | ----------------------- | --- | --- | --- | ---------- | ------ | --------- | --- | ------ | --------- |
|                      |     |                         |     |     |     | Toju Duke, | Anselm | Levskaya, |     | Sanjay | Ghemawat, |
realfutureoffinancialservices.
|     |     |     |     |     |     | Sunipa | Dev, Henryk | Michalewski, |     | Xavier | Garcia, |
| --- | --- | --- | --- | --- | --- | ------ | ----------- | ------------ | --- | ------ | ------- |
YonatanBisk,RowanZellers,JianfengGao,YejinChoi, VedantMisra,KevinRobinson,LiamFedus,Denny
et al. 2020. Piqa: Reasoning about physical com- Zhou,DaphneIppolito,DavidLuan,HyeontaekLim,
|     |     |     | InProceedingsofthe |     |     | Barret Zoph, | Alexander |     | Spiridonov, | Ryan | Sepassi, |
| --- | --- | --- | ------------------ | --- | --- | ------------ | --------- | --- | ----------- | ---- | -------- |
monsenseinnaturallanguage.
DavidDohan,ShivaniAgrawal,MarkOmernick,An-
AAAIconferenceonartificialintelligence,volume34,
|     |     |     |     |     |     | drew M. | Dai, Thanumalayan |     | Sankaranarayana |     | Pil- |
| --- | --- | --- | --- | --- | --- | ------- | ----------------- | --- | --------------- | --- | ---- |
pages7432–7439.
lai,MariePellat,AitorLewkowycz,EricaMoreira,
Alexandre Blanco-Gonzalez, Alfonso Cabezon, Ale- Rewon Child, Oleksandr Polozov, Katherine Lee,
jandroSeco-Gonzalez,DanielConde-Torres,Paula ZongweiZhou,XuezhiWang,BrennanSaeta,Mark
Antelo-Riveiro,AngelPineiro,andRebecaGarcia- Diaz,OrhanFirat,MicheleCatasta,JasonWei,Kathy
Fandino. 2022. The role of ai in drug discovery: Meier-Hellstern,DouglasEck,JeffDean,SlavPetrov,
Challenges, opportunities, and strategies. arXiv andNoahFiedel.2022. Palm:Scalinglanguagemod-
| preprintarXiv:2212.08104. |     |     |     |     |     | elingwithpathways. |     |     |     |     |     |
| ------------------------- | --- | --- | --- | --- | --- | ------------------ | --- | --- | --- | --- | --- |
684

PaulChristiano,JanLeike,TomB.Brown,MiljanMar- Simon Frieder, Luca Pinchetti, Ryan-Rhys Grif-
tic, Shane Legg, and Dario Amodei. 2017. Deep fiths, Tommaso Salvatori, Thomas Lukasiewicz,
reinforcementlearningfromhumanpreferences. Philipp Christian Petersen, Alexis Chevalier, and
|                                                |     |     |     |     | Julius   | Berner. | 2023. | Mathematical |     | capabilities | of  |
| ---------------------------------------------- | --- | --- | --- | --- | -------- | ------- | ----- | ------------ | --- | ------------ | --- |
| PeterClark,IsaacCowhey,OrenEtzioni,TusharKhot, |     |     |     |     | chatgpt. |         |       |              |     |              |     |
AshishSabharwal,CarissaSchoenick,andOyvind
Tafjord.2018. Thinkyouhavesolvedquestionan- Leo Gao, Jonathan Tow, Stella Biderman, Sid Black,
swering? tryarc,theai2reasoningchallenge. AnthonyDiPofi,CharlesFoster,LaurenceGolding,
|     |     |     |     |     | Jeffrey | Hsu, Kyle | McDonell, |     | Niklas | Muennighoff, |     |
| --- | --- | --- | --- | --- | ------- | --------- | --------- | --- | ------ | ------------ | --- |
Cookup.ai.2022. Chatgpt-whereitlacks. JasonPhang,LariaReynolds,EricTang,AnishThite,
|     |     |     |     |     | Ben Wang, | Kevin | Wang, | and | Andy | Zou. 2021. | A   |
| --- | --- | --- | --- | --- | --------- | ----- | ----- | --- | ---- | ---------- | --- |
WenliangDai,LuHou,LifengShang,XinJiang,Qun frameworkforfew-shotlanguagemodelevaluation.
| Liu,andPascaleFung.2022. |     | Enablingmultimodal |     |     |     |     |     |     |     |     |     |
| ------------------------ | --- | ------------------ | --- | --- | --- | --- | --- | --- | --- | --- | --- |
generationonCLIPviavision-languageknowledge AidanGilson,ConradSafranek,ThomasHuang,Vimig
distillation. InFindingsoftheAssociationforCom- Socrates, Ling Chi, Richard Andrew Taylor, and
|                        |     |                         |     |     | David       | Chartash. | 2022.   | How       | well does | chatgpt | do      |
| ---------------------- | --- | ----------------------- | --- | --- | ----------- | --------- | ------- | --------- | --------- | ------- | ------- |
| putationalLinguistics: |     | ACL2022,pages2383–2395, |     |     |             |           |         |           |           |         |         |
|                        |     |                         |     |     | when taking | the       | medical | licensing | exams?    |         | the im- |
Dublin,Ireland.AssociationforComputationalLin-
| guistics. |              |            |          |             | plicationsoflargelanguagemodelsformedicaledu- |     |     |     |               |     |     |
| --------- | ------------ | ---------- | -------- | ----------- | --------------------------------------------- | --- | --- | --- | ------------- | --- | --- |
|           |              |            |          |             | cationandknowledgeassessment.                 |     |     |     | medRxiv,pages |     |     |
| Wenliang  | Dai, Junnan  | Li, Dongxu |          | Li, Anthony | 2022–12.                                      |     |     |     |               |     |     |
| Meng Huat | Tiong, Junqi | Zhao,      | Weisheng | Wang,       |                                               |     |     |     |               |     |     |
BogdanGliwa,IwonaMochol,MaciejBiesek,andAlek-
| BoyangLi,PascaleFung,andStevenHoi.2023a. |                                       |     |     | In- |        |        |       |        |         |     |        |
| ---------------------------------------- | ------------------------------------- | --- | --- | --- | ------ | ------ | ----- | ------ | ------- | --- | ------ |
|                                          |                                       |     |     |     | sander | Wawer. | 2019. | Samsum | corpus: | A   | human- |
| structblip:                              | Towardsgeneral-purposevision-language |     |     |     |        |        |       |        |         |     |        |
modelswithinstructiontuning. annotated dialogue dataset for abstractive summa-
|     |     |     |     |     | rization. | EMNLP-IJCNLP2019,page70. |     |     |     |     |     |
| --- | --- | --- | --- | --- | --------- | ------------------------ | --- | --- | --- | --- | --- |
WenliangDai,ZihanLiu,ZiweiJi,DanSu,andPascale
|             |                            |     |     |         | YoavGoldberg.2023. |     | Someremarksonlargelanguage |     |     |     |     |
| ----------- | -------------------------- | --- | --- | ------- | ------------------ | --- | -------------------------- | --- | --- | --- | --- |
| Fung.2023b. | Plausiblemaynotbefaithful: |     |     | Probing |                    |     |                            |     |     |     |     |
models.
objecthallucinationinvision-languagepre-training.
InProceedingsofthe17thConferenceoftheEuro-
|     |     |     |     |     | CindyGordon.2023. |     | Chatgptisthefastestgrowingapp |     |     |     |     |
| --- | --- | --- | --- | --- | ----------------- | --- | ----------------------------- | --- | --- | --- | --- |
peanChapteroftheAssociationforComputational
inthehistoryofwebapplications.
| Linguistics, | pages2136–2148, |     | Dubrovnik, | Croatia. |     |     |     |     |     |     |     |
| ------------ | --------------- | --- | ---------- | -------- | --- | --- | --- | --- | --- | --- | --- |
AssociationforComputationalLinguistics.
NamanGoyal,CynthiaGao,VishravChaudhary,Peng-
|     |     |     |     |     | Jen Chen, | Guillaume |     | Wenzek, | Da Ju, | Sanjana | Kr- |
| --- | --- | --- | --- | --- | --------- | --------- | --- | ------- | ------ | ------- | --- |
BhavanaDalvi,PeterJansen,OyvindTafjord,Zhengnan
ishnan,Marc’AurelioRanzato,FranciscoGuzmán,
Xie,HannahSmith,LeighannaPipatanangkura,and
|                  |                                  |     |     |     | and Angela | Fan. | 2021.        | The | flores-101       | evaluation |     |
| ---------------- | -------------------------------- | --- | --- | --- | ---------- | ---- | ------------ | --- | ---------------- | ---------- | --- |
| PeterClark.2021. | Explaininganswerswithentail-     |     |     |     |            |      |              |     |                  |            |     |
|                  |                                  |     |     |     | benchmark  | for  | low-resource |     | and multilingual |            | ma- |
| menttrees.       | InProceedingsofthe2021Conference |     |     |     |            |      |              |     |                  |            |     |
chinetranslation.
onEmpiricalMethodsinNaturalLanguageProcess-
ing,pages7358–7370.
|                    |                            |     |     |     | TanyaGoyal, | JunyiJessyLi, |     | andGregDurrett.2022. |     |        |        |
| ------------------ | -------------------------- | --- | --- | --- | ----------- | ------------- | --- | -------------------- | --- | ------ | ------ |
|                    |                            |     |     |     | News        | summarization |     | and evaluation       |     | in the | era of |
| ErnestDavis.2023a. | Benchmarksforautomatedcom- |     |     |     |             |               |     |                      |     |        |        |
gpt-3. arXivpreprintarXiv:2209.12356.
|          |            |           | arXiv | preprint |     |     |     |     |     |     |     |
| -------- | ---------- | --------- | ----- | -------- | --- | --- | --- | --- | --- | --- | --- |
| monsense | reasoning: | A survey. |       |          |     |     |     |     |     |     |     |
arXiv:2302.04752. Roberto Gozalo-Brizuela and Eduardo C Garrido-
|               |                       |     |               |           | Merchan.2023.                            |     | Chatgptisnotallyouneed.astate |     |     |     |       |
| ------------- | --------------------- | --- | ------------- | --------- | ---------------------------------------- | --- | ----------------------------- | --- | --- | --- | ----- |
| Ernest Davis. | 2023b. Mathematics,   |     | word          | problems, |                                          |     |                               |     |     |     |       |
|               |                       |     |               |           | oftheartreviewoflargegenerativeaimodels. |     |                               |     |     |     | arXiv |
| common        | sense, and artificial |     | intelligence. | arXiv     |                                          |     |                               |     |     |     |       |
preprintarXiv:2301.04655.
preprintarXiv:2301.09723.
|     |     |     |     |     | Biyang Guo, | Xin | Zhang, | Ziyuan | Wang, | Minqi | Jiang, |
| --- | --- | --- | --- | --- | ----------- | --- | ------ | ------ | ----- | ----- | ------ |
Web Desk. 2023. Colombian judge uses chatgpt in JinranNie,YuxuanDing,JianweiYue,andYupeng
ruling,triggersdebate. Wu.2023. Howcloseischatgpttohumanexperts?
|                  |            |     |     |     | comparisoncorpus,evaluation,anddetection. |     |     |     |     |     | arXiv |
| ---------------- | ---------- | --- | --- | --- | ----------------------------------------- | --- | --- | --- | --- | --- | ----- |
| IgorDouven.2017. | Abduction. |     |     |     |                                           |     |     |     |     |     |       |
preprintarXiv:2301.07597.
MichaelDowlingandBrianLucey.2023. Chatgptfor JamesHawthorne.2021. InductiveLogic. InEdwardN.
(finance)research: Thebananaramaconjecture. Fi- Zalta,editor,TheStanfordEncyclopediaofPhiloso-
nanceResearchLetters,page103662. phy,Spring2021edition.MetaphysicsResearchLab,
StanfordUniversity.
LiDu,XiaoDing,KaiXiong,TingLiu,andBingQin.
2022. e-CARE:anewdatasetforexploringexplain- KarlMoritzHermann,TomasKocisky,EdwardGrefen-
able causal reasoning. In Proceedings of the 60th stette,LasseEspeholt,WillKay,MustafaSuleyman,
AnnualMeetingoftheAssociationforComputational andPhilBlunsom.2015. Teachingmachinestoread
Linguistics(Volume1:LongPapers),pages432–446, andcomprehend. InAdvancesinNeuralInformation
Dublin,Ireland.AssociationforComputationalLin- ProcessingSystems,volume28.CurranAssociates,
| guistics. |     |     |     |     | Inc. |     |     |     |     |     |     |
| --------- | --- | --- | --- | --- | ---- | --- | --- | --- | --- | --- | --- |
685

JordanHoffmann,SebastianBorgeaud,ArthurMensch, JanKocon´,IgorCichecki,OliwierKaszyca,Mateusz
Elena Buchatskaya, Trevor Cai, Eliza Rutherford, Kochanek, Dominika Szydło, Joanna Baran, Julita
DiegodeLasCasas,LisaAnneHendricks,Johannes Bielaniewicz,MarcinGruza,ArkadiuszJanz,Kamil
Welbl, Aidan Clark, Tom Hennigan, Eric Noland, Kanclerz, et al. 2023. Chatgpt: Jack of all trades,
KatieMillican,GeorgevandenDriessche,Bogdan masterofnone. InformationFusion,page101861.
| Damoc, | Aurelia | Guy, | Simon | Osindero, | Karen | Si- |     |     |     |     |     |     |
| ------ | ------- | ---- | ----- | --------- | ----- | --- | --- | --- | --- | --- | --- | --- |
monyan, Erich Elsen, Jack W. Rae, Oriol Vinyals, EscapeVelocityLabs.2022. Chatgptimitateslogical
andLaurentSifre.2022. Trainingcompute-optimal reasoningsurprisinglywell.
largelanguagemodels.
|     |     |     |     |     |     |     | Viet Dac | Lai, Nghia | Trung | Ngo, | Amir | Pouran Ben |
| --- | --- | --- | --- | --- | --- | --- | -------- | ---------- | ----- | ---- | ---- | ---------- |
Krystal Hu. 2023. Chatgpt sets record for fastest- Veyseh,HieuMan,FranckDernoncourt,TrungBui,
growinguserbase-analystnote. andThienHuuNguyen.2023. Chatgptbeyonden-
glish: Towardsacomprehensiveevaluationoflarge
| Jie Huang | and Kevin | Chen-Chuan |     | Chang. | 2022. | To- |          |        |     |              |           |       |
| --------- | --------- | ---------- | --- | ------ | ----- | --- | -------- | ------ | --- | ------------ | --------- | ----- |
|           |           |            |     |        |       |     | language | models | in  | multilingual | learning. | arXiv |
wardsreasoninginlargelanguagemodels: Asurvey. preprintarXiv:2304.05613.
arXivpreprintarXiv:2212.10403.
|     |     |     |     |     |     |     | Md Tahmid | Rahman | Laskar, | M   | Saiful Bari, | Mizanur |
| --- | --- | --- | --- | --- | --- | --- | --------- | ------ | ------- | --- | ------------ | ------- |
ArfindaIlmania,Abdurrahman,SamuelCahyawijaya, Rahman, MdAmranHossenBhuiyan, ShafiqJoty,
and Ayu Purwarianti. 2018. Aspect detection and andJimmyHuang.2023a. Asystematicstudyand
| sentiment | classification |     | using | deep | neural | network |     |     |     |     |     |     |
| --------- | -------------- | --- | ----- | ---- | ------ | ------- | --- | --- | --- | --- | --- | --- |
comprehensiveevaluationofChatGPTonbenchmark
| forindonesianaspect-basedsentimentanalysis. |     |     |     |     |     | In  |           |             |     |        |             |          |
| ------------------------------------------- | --- | --- | --- | --- | --- | --- | --------- | ----------- | --- | ------ | ----------- | -------- |
|                                             |     |     |     |     |     |     | datasets. | In Findings |     | of the | Association | for Com- |
2018InternationalConferenceonAsianLanguage putational Linguistics: ACL 2023, pages 431–469,
Processing(IALP),pages62–67. Toronto,Canada.AssociationforComputationalLin-
guistics.
| Hadar Yoana        | Jabotinsky                           |                              | and Roee | Sarel. | 2022. | Co- |             |        |          |         |          |             |
| ------------------ | ------------------------------------ | ---------------------------- | -------- | ------ | ----- | --- | ----------- | ------ | -------- | ------- | -------- | ----------- |
| authoringwithanai? |                                      | ethicaldilemmasandartificial |          |        |       |     |             |        |          |         |          |             |
|                    |                                      |                              |          |        |       |     | Md Tahmid   | Rahman |          | Laskar, | M Saiful | Bari, Miza- |
| intelligence.      | EthicalDilemmasandArtificialIntelli- |                              |          |        |       |     |             |        |          |         |          |             |
|                    |                                      |                              |          |        |       |     | nur Rahman, |        | Md Amran | Hossen  | Bhuiyan, | Shafiq      |
gence(December15,2022).
|           |          |           |             |     |       |       | Joty,   | and Jimmy    | Xiangji | Huang.        | 2023b. | A sys-        |
| --------- | -------- | --------- | ----------- | --- | ----- | ----- | ------- | ------------ | ------- | ------------- | ------ | ------------- |
|           |          |           |             |     |       |       | tematic | study        | and     | comprehensive |        | evaluation of |
| Katharina | Jeblick, | Balthasar | Schachtner, |     | Jakob | Dexl, |         |              |         |               |        |               |
|           |          |           |             |     |       |       | chatgpt | on benchmark |         | datasets.     | arXiv  | preprint      |
AndreasMittermeier,AnnaTheresaStüber,Johanna
arXiv:2305.18486.
Topalis,TobiasWeber,PhilippWesp,BastianSabel,
| JensRicke,etal.2022. |                                    |                                | Chatgptmakesmedicineeasy |     |     |     |                    |     |              |                          |                |          |
| -------------------- | ---------------------------------- | ------------------------------ | ------------------------ | --- | --- | --- | ------------------ | --- | ------------ | ------------------------ | -------------- | -------- |
|                      |                                    |                                |                          |     |     |     | AntonELawson.2005. |     |              | Whatistheroleofinduction |                |          |
| toswallow:           | Anexploratorycasestudyonsimplified |                                |                          |     |     |     |                    |     |              |                          |                |          |
|                      |                                    |                                |                          |     |     |     | and deduction      |     | in reasoning |                          | and scientific | inquiry? |
| radiologyreports.    |                                    | arXivpreprintarXiv:2212.14882. |                          |     |     |     |                    |     |              |                          |                |          |
JournalofResearchinScienceTeaching,42(6):716–
740.
| Ziwei Ji, | Nayeon | Lee, | Rita Frieske, |     | Tiezheng | Yu, |     |     |     |     |     |     |
| --------- | ------ | ---- | ------------- | --- | -------- | --- | --- | --- | --- | --- | --- | --- |
DanSu,YanXu,EtsukoIshii,YejinBang,Andrea
NayeonLee,YejinBang,AndreaMadotto,andPascale
Madotto,andPascaleFung.2022a. Surveyofhalluci- Fung. 2021. Towards few-shot fact-checking via
| nationinnaturallanguagegeneration. |     |     |     |     | ACMComput. |     |             |                                  |     |     |     |     |
| ---------------------------------- | --- | --- | --- | --- | ---------- | --- | ----------- | -------------------------------- | --- | --- | --- | --- |
|                                    |     |     |     |     |            |     | perplexity. | InProceedingsofthe2021Conference |     |     |     |     |
Surv. JustAccepted.
|     |     |     |     |     |     |     | of the            | North American |              | Chapter | of the | Association |
| --- | --- | --- | --- | --- | --- | --- | ----------------- | -------------- | ------------ | ------- | ------ | ----------- |
|     |     |     |     |     |     |     | for Computational |                | Linguistics: |         | Human  | Language    |
ZiweiJi,ZihanLiu,NayeonLee,TiezhengYu,Bryan
Technologies,pages1971–1981,Online.Association
| Wilie, | Min Zeng, | and | Pascale | Fung. | 2022b. | Rho |     |     |     |     |     |     |
| ------ | --------- | --- | ------- | ----- | ------ | --- | --- | --- | --- | --- | --- | --- |
forComputationalLinguistics.
| (ρ): Reducing |                | hallucination |            | in open-domain |       | dia-     |     |     |     |     |     |     |
| ------------- | -------------- | ------------- | ---------- | -------------- | ----- | -------- | --- | --- | --- | --- | --- | --- |
| logues        | with knowledge |               | grounding. |                | arXiv | preprint |     |     |     |     |     |     |
NayeonLee,WeiPing,PengXu,MostofaPatwary,Pas-
arXiv:2212.01588.
|     |     |     |     |     |     |     | caleFung,  | MohammadShoeybi,                    |     |     | andBryanCatan- |     |
| --- | --- | --- | --- | --- | --- | --- | ---------- | ----------------------------------- | --- | --- | -------------- | --- |
|     |     |     |     |     |     |     | zaro.2022. | Factualityenhancedlanguagemodelsfor |     |     |                |     |
WenxiangJiao,WenxuanWang,Jen-tseHuang,Xing
|       |              |     |       |     |         |        | open-endedtextgeneration. |     |     |     | InAdvancesinNeural |     |
| ----- | ------------ | --- | ----- | --- | ------- | ------ | ------------------------- | --- | --- | --- | ------------------ | --- |
| Wang, | and Zhaopeng | Tu. | 2023. | Is  | chatgpt | a good |                           |     |     |     |                    |     |
InformationProcessingSystems.
| translator?      | apreliminarystudy. |       |            |           |     |       |             |        |     |            |        |        |
| ---------------- | ------------------ | ----- | ---------- | --------- | --- | ----- | ----------- | ------ | --- | ---------- | ------ | ------ |
|                  |                    |       |            |           |     |       | Mike Lewis, | Yinhan |     | Liu, Naman | Goyal, | Marjan |
| Arianna Johnson. |                    | 2023. | Is chatgpt | partisan? |     | poems |             |        |     |            |        |        |
abouttrumpandbidenraisequestionsabouttheai Ghazvininejad,AbdelrahmanMohamed,OmerLevy,
bot’sbias-here’swhatexpertsthink. Veselin Stoyanov, and Luke Zettlemoyer. 2020a.
BART:Denoisingsequence-to-sequencepre-training
PratikJoshi, SebastinSanty, AmarBudhiraja, Kalika fornaturallanguagegeneration,translation,andcom-
|                                |     |     |     |     |             |     | prehension. | InProceedingsofthe58thAnnualMeet- |     |     |     |     |
| ------------------------------ | --- | --- | --- | --- | ----------- | --- | ----------- | --------------------------------- | --- | --- | --- | --- |
| Bali,andMonojitChoudhury.2020. |     |     |     |     | Thestateand |     |             |                                   |     |     |     |     |
fateoflinguisticdiversityandinclusionintheNLP ingoftheAssociationforComputationalLinguistics,
world. InProceedingsofthe58thAnnualMeetingof pages7871–7880,Online.AssociationforComputa-
| theAssociationforComputationalLinguistics,pages |     |     |     |     |     |     | tionalLinguistics. |     |     |     |     |     |
| ----------------------------------------------- | --- | --- | --- | --- | --- | --- | ------------------ | --- | --- | --- | --- | --- |
6282–6293,Online.AssociationforComputational
| Linguistics. |     |     |     |     |     |     | Mike Lewis, | Yinhan |     | Liu, Naman | Goyal, | Marjan |
| ------------ | --- | --- | --- | --- | --- | --- | ----------- | ------ | --- | ---------- | ------ | ------ |
Ghazvininejad,AbdelrahmanMohamed,OmerLevy,
Jennifer A. Kingson. 2023. Friend or foe? teachers Veselin Stoyanov, and Luke Zettlemoyer. 2020b.
debatechatgpt. Bart: Denoisingsequence-to-sequencepre-training
686

fornaturallanguagegeneration,translation,andcom- RuiMao,GuanyiChen,XulangZhang,FrankGuerin,
prehension. InProceedingsofthe58thAnnualMeet- and Erik Cambria. 2023. Gpteval: A survey on
ingoftheAssociationforComputationalLinguistics, assessments of chatgpt and gpt-4. arXiv preprint
| pages7871–7880. |       |            |     |           |          | arXiv:2308.12488. |     |                              |     |     |     |
| --------------- | ----- | ---------- | --- | --------- | -------- | ----------------- | --- | ---------------------------- | --- | --- | --- |
|                 |       |            |     |           |          | BernardMarr.2022. |     | Whatdoeschatgptreallymeanfor |     |     |     |
| Percy Liang,    | Rishi | Bommasani, |     | Tony Lee, | Dimitris |                   |     |                              |     |     |     |
businesses?
| Tsipras, | Dilara | Soylu, | Michihiro | Yasunaga, | Yian |     |     |     |     |     |     |
| -------- | ------ | ------ | --------- | --------- | ---- | --- | --- | --- | --- | --- | --- |
Zhang,DeepakNarayanan,YuhuaiWu,AnanyaKu-
VaibhavMavi,AnubhavJangra,andAdamJatowt.2022.
mar,BenjaminNewman,BinhangYuan,BobbyYan,
CeZhang,ChristianCosgrove,ChristopherD.Man- Asurveyonmulti-hopquestionansweringandgen-
|     |     |     |     |     |     | eration. arXivpreprintarXiv:2204.09140. |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --------------------------------------- | --- | --- | --- | --- | --- |
ning,ChristopherRé,DianaAcosta-Navas,DrewA.
| Hudson, | Eric | Zelikman, | Esin | Durmus, | Faisal Lad- |     |     |     |     |     |     |
| ------- | ---- | --------- | ---- | ------- | ----------- | --- | --- | --- | --- | --- | --- |
PasqualeMinervini,SebastianRiedel,PontusStenetorp,
| hak, Frieda | Rong, | Hongyu | Ren, | Huaxiu | Yao, Jue |        |               |     |                  |     |       |
| ----------- | ----- | ------ | ---- | ------ | -------- | ------ | ------------- | --- | ---------------- | --- | ----- |
|             |       |        |      |        |          | Edward | Grefenstette, | and | Tim Rocktäschel. |     | 2020. |
Wang,KeshavSanthanam,LaurelOrr,LuciaZheng,
Learningreasoningstrategiesinend-to-enddifferen-
| Mert Yuksekgonul, |     | Mirac | Suzgun, |     | Nathan Kim, |                |                                |     |     |     |     |
| ----------------- | --- | ----- | ------- | --- | ----------- | -------------- | ------------------------------ | --- | --- | --- | --- |
|                   |     |       |         |     |             | tiableproving. | InProceedingsofthe37thInterna- |     |     |     |     |
NeelGuha, NiladriChatterji, OmarKhattab, Peter tionalConferenceonMachineLearning,ICML’20.
| Henderson, | Qian | Huang, | Ryan | Chi, Sang | Michael |     |     |     |     |     |     |
| ---------- | ---- | ------ | ---- | --------- | ------- | --- | --- | --- | --- | --- | --- |
JMLR.org.
| Xie, Shibani |     | Santurkar, | Surya | Ganguli, | Tatsunori |     |     |     |     |     |     |
| ------------ | --- | ---------- | ----- | -------- | --------- | --- | --- | --- | --- | --- | --- |
Hashimoto, Thomas Icard, Tianyi Zhang, Vishrav Roshanak Mirzaee and Parisa Kordjamshidi. 2022.
Chaudhary,WilliamWang,XuechenLi,YifanMai,
Transferlearningwithsyntheticcorporaforspatial
YuhuiZhang,andYutaKoreeda.2022. Holisticeval- rolelabelingandreasoning. InProceedingsofthe
uationoflanguagemodels. 2022 Conference on Empirical Methods in Natu-
|     |     |     |     |     |     | ral Language | Processing, |     | pages | 6148–6165, | Abu |
| --- | --- | --- | --- | --- | --- | ------------ | ----------- | --- | ----- | ---------- | --- |
StephanieLin,JacobHilton,andOwainEvans.2022. Dhabi,UnitedArabEmirates.AssociationforCom-
TruthfulQA:Measuringhowmodelsmimichuman
putationalLinguistics.
InProceedingsofthe60thAnnualMeet-
falsehoods.
|     |     |     |     |     |     | Roshanak Mirzaee, |     | Hossein | Rajaby | Faghihi, | Qiang |
| --- | --- | --- | --- | --- | --- | ----------------- | --- | ------- | ------ | -------- | ----- |
ingoftheAssociationforComputationalLinguistics
(Volume1: LongPapers),pages3214–3252,Dublin, Ning, and Parisa Kordjamshidi. 2021. SPARTQA:
Ireland.AssociationforComputationalLinguistics. Atextualquestionansweringbenchmarkforspatial
|     |     |     |     |     |     | reasoning. | InProceedingsofthe2021Conferenceof |     |     |     |     |
| --- | --- | --- | --- | --- | --- | ---------- | ---------------------------------- | --- | --- | --- | --- |
ZhaojiangLin,BingLiu,AndreaMadotto,Seungwhan theNorthAmericanChapteroftheAssociationfor
|       |          |       |      |          |          | ComputationalLinguistics: |     |     | HumanLanguageTech- |     |     |
| ----- | -------- | ----- | ---- | -------- | -------- | ------------------------- | --- | --- | ------------------ | --- | --- |
| Moon, | Zhenpeng | Zhou, | Paul | A Crook, | Zhiguang |                           |     |     |                    |     |     |
Wang, Zhou Yu, Eunjoon Cho, Rajen Subba, et al. nologies,pages4582–4598,Online.Associationfor
2021. Zero-shotdialoguestatetrackingviacross-task ComputationalLinguistics.
| transfer. | InProceedingsofthe2021Conferenceon |     |     |     |     |     |     |     |     |     |     |
| --------- | ---------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
EmpiricalMethodsinNaturalLanguageProcessing, SeungwhanMoon,PararthShah,AnujKumar,andRa-
|     |     |     |     |     |     | jenSubba.2019. |     | Opendialkg: | Explainableconver- |     |     |
| --- | --- | --- | --- | --- | --- | -------------- | --- | ----------- | ------------------ | --- | --- |
pages7890–7900.
sationalreasoningwithattention-basedwalksover
|     |     |     |     |     |     | knowledgegraphs. |     | InProceedingsofthe57thAn- |     |     |     |
| --- | --- | --- | --- | --- | --- | ---------------- | --- | ------------------------- | --- | --- | --- |
HolyLovenia,BryanWilie,RomainBarraud,Samuel
nualMeetingoftheAssociationforComputational
Cahyawijaya,WillyChung,andPascaleFung.2022.
Everypicturetellsastory: Image-groundedcontrol- Linguistics,pages845–854.
|     |     |     |     | Proceedings | of  |     |     |     |     |     |     |
| --- | --- | --- | --- | ----------- | --- | --- | --- | --- | --- | --- | --- |
lable stylistic story generation. In NiklasMuennighoff,ThomasWang,LintangSutawika,
the6thJointSIGHUMWorkshoponComputational
|             |     |          |           |        |           | Adam Roberts, | Stella     | Biderman, |                | Teven | Le Scao, |
| ----------- | --- | -------- | --------- | ------ | --------- | ------------- | ---------- | --------- | -------------- | ----- | -------- |
| Linguistics | for | Cultural | Heritage, | Social | Sciences, |               |            |           |                |       |          |
|             |     |          |           |        |           | MSaifulBari,  | ShengShen, |           | Zheng-XinYong, |       | Hai-     |
HumanitiesandLiterature,pages40–52,Gyeongju,
|     |     |     |     |     |     | ley Schoelkopf, | Xiangru |     | Tang, | Dragomir | Radev, |
| --- | --- | --- | --- | --- | --- | --------------- | ------- | --- | ----- | -------- | ------ |
RepublicofKorea.InternationalConferenceonCom-
|     |     |     |     |     |     | Alham Fikri | Aji, | Khalid | Almubarak, |     | Samuel Al- |
| --- | --- | --- | --- | --- | --- | ----------- | ---- | ------ | ---------- | --- | ---------- |
putationalLinguistics.
banie,ZaidAlyafeai,AlbertWebson,EdwardRaff,
|          |             |          |     |         |            | and Colin    | Raffel.   | 2022.       | Crosslingual |       | generaliza- |
| -------- | ----------- | -------- | --- | ------- | ---------- | ------------ | --------- | ----------- | ------------ | ----- | ----------- |
| Hongyuan | Lu, Haoyang | Huang,   |     | Shuming | Ma, Dong-  |              |           |             |              |       |             |
|          |             |          |     |         |            | tion through | multitask | finetuning. |              | arXiv | preprint    |
| dong     | Zhang,      | Wai Lam, | and | Furu    | Wei. 2022. |              |           |             |              |       |             |
arXiv:2211.01786.
| Trip:        | Triangular | document-level |         | pre-training | for      |                  |          |     |                 |     |        |
| ------------ | ---------- | -------------- | ------- | ------------ | -------- | ---------------- | -------- | --- | --------------- | --- | ------ |
| multilingual |            | language       | models. | arXiv        | preprint |                  |          |     |                 |     |        |
|              |            |                |         |              |          | Benjamin Muller, | Antonios |     | Anastasopoulos, |     | Benoît |
arXiv:2212.07752. Sagot, and Djamé Seddah. 2021. When being un-
|     |     |     |     |     |     | seenfrommBERTisjustthebeginning: |     |     |     |     | Handling |
| --- | --- | --- | --- | --- | --- | -------------------------------- | --- | --- | --- | --- | -------- |
AndreaMadotto,ZhaojiangLin,GentaIndraWinata, new languages with multilingual language models.
| and Pascale |     | Fung. 2021. | Few-shot |     | bot: Prompt- |     |     |     |     |     |     |
| ----------- | --- | ----------- | -------- | --- | ------------ | --- | --- | --- | --- | --- | --- |
InProceedingsofthe2021ConferenceoftheNorth
| basedlearningfordialoguesystems. |     |     |     | arXivpreprint |     |     |     |     |     |     |     |
| -------------------------------- | --- | --- | --- | ------------- | --- | --- | --- | --- | --- | --- | --- |
AmericanChapteroftheAssociationforComputa-
arXiv:2110.08118.
|                                            |        |              |     |     |             | tionalLinguistics: |         | HumanLanguageTechnologies, |     |     |          |
| ------------------------------------------ | ------ | ------------ | --- | --- | ----------- | ------------------ | ------- | -------------------------- | --- | --- | -------- |
|                                            |        |              |     |     |             | pages 448–462,     | Online. | Association                |     | for | Computa- |
| KyleMahowald,AnnaAIvanova,IdanABlank,Nancy |        |              |     |     |             | tionalLinguistics. |         |                            |     |     |          |
| Kanwisher,                                 | Joshua | B Tenenbaum, |     | and | Evelina Fe- |                    |         |                            |     |     |          |
dorenko.2023. Dissociatinglanguageandthought Ramesh Nallapati, Bowen Zhou, Cicero dos Santos,
in large language models: a cognitive perspective. Çag˘lar Gulçehre, and Bing Xiang. 2016. Abstrac-
arXivpreprintarXiv:2301.06627. tivetextsummarizationusingsequence-to-sequence
687

RNNs and beyond. In Proceedings of the 20th LianhuiQin,AdityaGupta,ShyamUpadhyay,Luheng
SIGNLLConferenceonComputationalNaturalLan- He,YejinChoi,andManaalFaruqui.2021. TIME-
guage Learning, pages 280–290, Berlin, Germany. DIAL:Temporalcommonsensereasoningindialog.
AssociationforComputationalLinguistics. In Proceedings of the 59th Annual Meeting of the
|     |     |     |     |     |     |     | Association | for | Computational | Linguistics |     | and the |
| --- | --- | --- | --- | --- | --- | --- | ----------- | --- | ------------- | ----------- | --- | ------- |
TomášNekvindaandOndˇrejDušek.2021.
|     |     |     |     |     | Shadesof |     | 11thInternationalJointConferenceonNaturalLan- |     |     |     |     |     |
| --- | --- | --- | --- | --- | -------- | --- | --------------------------------------------- | --- | --- | --- | --- | --- |
BLEU,flavoursofsuccess: ThecaseofMultiWOZ. guageProcessing(Volume1: LongPapers),pages
InProceedingsofthe1stWorkshoponNaturalLan- 7066–7076,Online.AssociationforComputational
| guageGeneration, |     | Evaluation, |     | andMetrics(GEM |     |     | Linguistics. |     |     |     |     |     |
| ---------------- | --- | ----------- | --- | -------------- | --- | --- | ------------ | --- | --- | --- | --- | --- |
2021),pages34–46,Online.AssociationforCompu-
tationalLinguistics. AlecRadford,JongWookKim,ChrisHallacy,Aditya
Ramesh,GabrielGoh,SandhiniAgarwal,GirishSas-
Oded Nov, Nina Singh, and Devin M Mann. 2023. try, Amanda Askell, Pamela Mishkin, Jack Clark,
Puttingchatgpt’smedicaladvicetothe(turing)test. etal.2021. Learningtransferablevisualmodelsfrom
medRxiv,pages2023–01. naturallanguagesupervision. InInternationalconfer-
enceonmachinelearning,pages8748–8763.PMLR.
| OpenAI.2023. | Gpt-4technicalreport. |     |     |     |     |     |     |     |     |     |     |     |
| ------------ | --------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
AlecRadford,JeffreyWu,RewonChild,DavidLuan,
Simon Ott, Konstantin Hebenstreit, Valentin Liévin, DarioAmodei,IlyaSutskever,etal.2019. Language
| Christoffer                                 | Egeberg |     | Hother, Milad  | Moradi, |          | Maxi- |                                         |     |     |     |     |        |
| ------------------------------------------- | ------- | --- | -------------- | ------- | -------- | ----- | --------------------------------------- | --- | --- | --- | --- | ------ |
|                                             |         |     |                |         |          |       | modelsareunsupervisedmultitasklearners. |     |     |     |     | OpenAI |
| milianMayrhauser,RobertPraas,OleWinther,and |         |     |                |         |          |       | blog,1(8):9.                            |     |     |     |     |        |
| MatthiasSamwald.2023.                       |         |     | Thoughtsource: |         | Acentral |       |                                         |     |     |     |     |        |
hubforlargelanguagemodelreasoningdata. arXiv Jack W. Rae, Sebastian Borgeaud, Trevor Cai, Katie
preprintarXiv:2301.11596. Millican, Jordan Hoffmann, Francis Song, John
|     |     |     |     |     |     |     | Aslanides, | Sarah | Henderson, | Roman | Ring, | Susan- |
| --- | --- | --- | --- | --- | --- | --- | ---------- | ----- | ---------- | ----- | ----- | ------ |
LongOuyang,JeffWu,XuJiang,DiogoAlmeida,Car- nah Young, Eliza Rutherford, Tom Hennigan, Ja-
rollL.Wainwright,PamelaMishkin,ChongZhang, cobMenick,AlbinCassirer,RichardPowell,George
SandhiniAgarwal,KatarinaSlama,AlexRay,John van den Driessche, Lisa Anne Hendricks, Mari-
Schulman,JacobHilton,FraserKelton,LukeMiller, beth Rauh, Po-Sen Huang, Amelia Glaese, Jo-
Maddie Simens, Amanda Askell, Peter Welinder, hannes Welbl, Sumanth Dathathri, Saffron Huang,
Paul Christiano, Jan Leike, and Ryan Lowe. 2022. JonathanUesato,JohnMellor,IrinaHiggins,Anto-
Traininglanguagemodelstofollowinstructionswith niaCreswell,NatMcAleese,AmyWu,ErichElsen,
| humanfeedback. |     |     |     |     |     |     | SiddhantJayakumar,ElenaBuchatskaya,DavidBud- |     |     |     |     |     |
| -------------- | --- | --- | --- | --- | --- | --- | -------------------------------------------- | --- | --- | --- | --- | --- |
den,EsmeSutherland,KarenSimonyan,MichelaPa-
Maja Popovic´. 2015. chrF: character n-gram F-score ganini,LaurentSifre,LenaMartens,XiangLorraine
forautomaticMTevaluation. InProceedingsofthe Li, Adhiguna Kuncoro, Aida Nematzadeh, Elena
TenthWorkshoponStatisticalMachineTranslation, Gribovskaya,DomenicDonato,AngelikiLazaridou,
| pages 392–395, |     | Lisbon, | Portugal. | Association |     | for |     |     |     |     |     |     |
| -------------- | --- | ------- | --------- | ----------- | --- | --- | --- | --- | --- | --- | --- | --- |
ArthurMensch,Jean-BaptisteLespiau,MariaTsim-
ComputationalLinguistics. poukelli,NikolaiGrigorev,DougFritz,ThibaultSot-
tiaux,MantasPajarskas,TobyPohlen,ZhitaoGong,
Ian Porada, Kaheer Suleman, Adam Trischler, and DanielToyama,CypriendeMassond’Autume,Yujia
JackieChiKitCheung.2021. Modelingeventplau- Li,TayfunTerzi,VladimirMikulik,IgorBabuschkin,
| sibility with | consistent |          | conceptual | abstraction. |        | In    |              |     |                 |            |         |          |
| ------------- | ---------- | -------- | ---------- | ------------ | ------ | ----- | ------------ | --- | --------------- | ---------- | ------- | -------- |
|               |            |          |            |              |        |       | Aidan Clark, |     | Diego de        | Las Casas, | Aurelia | Guy,     |
| Proceedings   | of         | the 2021 | Conference |              | of the | North |              |     |                 |            |         |          |
|               |            |          |            |              |        |       | Chris Jones, |     | James Bradbury, |            | Matthew | Johnson, |
AmericanChapteroftheAssociationforComputa-
|     |     |     |     |     |     |     | Blake Hechtman, |     | Laura Weidinger, |     | Iason | Gabriel, |
| --- | --- | --- | --- | --- | --- | --- | --------------- | --- | ---------------- | --- | ----- | -------- |
tionalLinguistics: HumanLanguageTechnologies, WilliamIsaac,EdLockhart,SimonOsindero,Laura
pages1732–1743,Online.AssociationforComputa- Rimell,ChrisDyer,OriolVinyals,KareemAyoub,
tionalLinguistics.
JeffStanway,LorrayneBennett,DemisHassabis,Ko-
|                |     |                                |     |     |     |     | rayKavukcuoglu,andGeoffreyIrving.2021. |     |                             |     |     | Scal- |
| -------------- | --- | ------------------------------ | --- | --- | --- | --- | -------------------------------------- | --- | --------------------------- | --- | --- | ----- |
| MattPost.2018. |     | AcallforclarityinreportingBLEU |     |     |     |     |                                        |     |                             |     |     |       |
|                |     |                                |     |     |     |     | inglanguagemodels:                     |     | Methods,analysisandinsights |     |     |       |
scores. InProceedingsoftheThirdConferenceon
fromtraininggopher.
| MachineTranslation: |     |     | ResearchPapers,pages186– |     |     |     |     |     |     |     |     |     |
| ------------------- | --- | --- | ------------------------ | --- | --- | --- | --- | --- | --- | --- | --- | --- |
191, Brussels, Belgium. Association for Computa- ColinRaffel,NoamShazeer,AdamRoberts,Katherine
| tionalLinguistics. |     |     |     |     |     |     | Lee,SharanNarang,MichaelMatena,YanqiZhou, |     |     |                    |     |     |
| ------------------ | --- | --- | --- | --- | --- | --- | ----------------------------------------- | --- | --- | ------------------ | --- | --- |
|                    |     |     |     |     |     |     | WeiLi,andPeterJ.Liu.2022.                 |     |     | Exploringthelimits |     |     |
ShuofeiQiao,YixinOu,NingyuZhang,XiangChen,
oftransferlearningwithaunifiedtext-to-texttrans-
YunzhiYao,ShuminDeng,ChuanqiTan,FeiHuang,
|            |       |       |           |     |      |      | former. | J.Mach.Learn.Res.,21(1). |     |     |     |     |
| ---------- | ----- | ----- | --------- | --- | ---- | ---- | ------- | ------------------------ | --- | --- | --- | --- |
| and Huajun | Chen. | 2022. | Reasoning |     | with | lan- |         |                          |     |     |     |     |
guagemodelprompting: Asurvey. arXivpreprint Aditya Ramesh, Mikhail Pavlov, Gabriel Goh, Scott
| arXiv:2212.09597. |     |     |     |     |     |     | Gray,ChelseaVoss,AlecRadford,MarkChen,and |     |                            |     |     |     |
| ----------------- | --- | --- | --- | --- | --- | --- | ----------------------------------------- | --- | -------------------------- | --- | --- | --- |
|                   |     |     |     |     |     |     | IlyaSutskever.2021.                       |     | Zero-shottext-to-imagegen- |     |     |     |
ChengweiQin,AstonZhang,ZhuoshengZhang,Jiaao eration. In International Conference on Machine
| Chen,MichihiroYasunaga,andDiyiYang.2023. |     |     |     |     |     | Is  |     |     |     |     |     |     |
| ---------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Learning,pages8821–8831.PMLR.
chatgptageneral-purposenaturallanguageprocess-
ingtasksolver? arXivpreprintarXiv:2302.06476. FabinRasheed.2020. Gpt3sees.
688

ParthaPratimRay.2023. Chatgpt: Acomprehensive Adrià Garriga-Alonso, et al. 2022. Beyond the
reviewonbackground,applications,keychallenges, imitation game: Quantifying and extrapolating the
bias,ethics,limitationsandfuturescope. Internetof capabilities of language models. arXiv preprint
| ThingsandCyber-PhysicalSystems. |     |     |     |     | arXiv:2206.04615. |     |     |     |     |
| ------------------------------- | --- | --- | --- | --- | ----------------- | --- | --- | --- | --- |
AnnaRogers,MattGardner,andIsabelleAugenstein. Shane Storks, Qiaozi Gao, and Joyce Y Chai. 2019.
Commonsensereasoningfornaturallanguageunder-
| 2022. Qa | dataset explosion: |     | A taxonomy | of nlp |     |     |     |     |     |
| -------- | ------------------ | --- | ---------- | ------ | --- | --- | --- | --- | --- |
resourcesforquestionansweringandreadingcom- standing: A survey of benchmarks, resources, and
prehension. ACMComput.Surv. JustAccepted. approaches. arXivpreprintarXiv:1904.01172,pages
1–60.
RobinRombach,AndreasBlattmann,DominikLorenz,
Patrick Esser, and Björn Ommer. 2022. High- DanSu,XiaoguangLi,JindiZhang,LifengShang,Xin
resolutionimagesynthesiswithlatentdiffusionmod- Jiang,QunLiu,andPascaleFung.2022. Readbefore
Proceedings of the IEEE/CVF Conference generate! faithfullongformquestionansweringwith
els. In
onComputerVisionandPatternRecognition,pages machinereading. InFindingsoftheAssociationfor
| 10684–10695. |     |     |     |     | ComputationalLinguistics: |     |     | ACL2022,pages744– |     |
| ------------ | --- | --- | --- | --- | ------------------------- | --- | --- | ----------------- | --- |
756.
| David Saxton, | Edward | Grefenstette, | Felix Hill, | and |     |     |     |     |     |
| ------------- | ------ | ------------- | ----------- | --- | --- | --- | --- | --- | --- |
PushmeetKohli.2019. Analysingmathematicalrea- DanSu,TiezhengYu,andPascaleFung.2021. Improve
soningabilitiesof neuralmodels. In International queryfocusedabstractivesummarizationbyincorpo-
ConferenceonLearningRepresentations. ratinganswerrelevance. InFindingsoftheAssoci-
|                        |     |                        |     |     | ationforComputationalLinguistics: |     |     | ACL-IJCNLP |     |
| ---------------------- | --- | ---------------------- | --- | --- | --------------------------------- | --- | --- | ---------- | --- |
| StephenShankland.2023. |     | Whythechatgptaichatbot |     |     |                                   |     |     |            |     |
2021,pages3124–3131.
isblowingeveryone’smind.
ZhiqingSun,XuezhiWang,YiTay,YimingYang,and
Yiqiu Shen, Laura Heacock, Jonathan Elias, Keith D DennyZhou.2022. Recitation-augmentedlanguage
Hentel,BeatriuReig,GeorgeShih,andLindaMoy. models. InTheEleventhInternationalConference
2023. Chatgptandotherlargelanguagemodelsare onLearningRepresentations.
double-edgedswords.
|     |     |     |     |     | TeoSusnjak.2022. |     | Chatgpt: Theendofonlineexam |     |     |
| --- | --- | --- | --- | --- | ---------------- | --- | --------------------------- | --- | --- |
ZhengxiangShi,QiangZhang,andAldoLipani.2022a. integrity? arXivpreprintarXiv:2212.09292.
| Stepgame:                | Anewbenchmarkforrobustmulti-hop |                      |     |     |                      |       |                        |                |     |
| ------------------------ | ------------------------------- | -------------------- | --- | --- | -------------------- | ----- | ---------------------- | -------------- | --- |
|                          |                                 |                      |     |     | Alon Talmor,         | Yanai | Elazar,                | Yoav Goldberg, | and |
| spatialreasoningintexts. |                                 | ProceedingsoftheAAAI |     |     |                      |       |                        |                |     |
|                          |                                 |                      |     |     | JonathanBerant.2020. |       | olmpics-onwhatlanguage |                |     |
ConferenceonArtificialIntelligence,36(10):11321–
| 11329. |     |     |     |     | modelpre-trainingcaptures. |     |     | TransactionsoftheAs- |     |
| ------ | --- | --- | --- | --- | -------------------------- | --- | --- | -------------------- | --- |
sociationforComputationalLinguistics,8:743–758.
ZhengxiangShi,QiangZhang,andAldoLipani.2022b.
StepGame: Anewbenchmarkforrobustmulti-hop Alon Talmor, Jonathan Herzig, Nicholas Lourie, and
spatialreasoningintexts. ProceedingsoftheAAAI JonathanBerant.2018. Commonsenseqa:Aquestion
answeringchallengetargetingcommonsenseknowl-
ConferenceonArtificialIntelligence,36(10):11321–
edge. arXivpreprintarXiv:1811.00937.
11329.
NLLBTeam,MartaR.Costa-jussà,JamesCross,Onur
| DenisShiryaev.2022. | Drawingmonalisawithchatgpt. |     |     |     |     |     |     |     |     |
| ------------------- | --------------------------- | --- | --- | --- | --- | --- | --- | --- | --- |
Çelebi,MahaElbayad,KennethHeafield,KevinHef-
Kurt Shuster, Jing Xu, Mojtaba Komeili, Da Ju, fernan, Elahe Kalbassi, Janice Lam, Daniel Licht,
Eric Michael Smith, Stephen Roller, Megan Ung, JeanMaillard,AnnaSun,SkylerWang,Guillaume
Moya Chen, Kushal Arora, Joshua Lane, Morteza Wenzek, Al Youngblood, Bapi Akula, Loic Bar-
Behrooz,WilliamNgan,SpencerPoff,NamanGoyal, rault,GabrielMejiaGonzalez,PrangthipHansanti,
|     |     |     |     |     | John Hoffman, |     | Semarley Jarrett, | Kaushik | Ram |
| --- | --- | --- | --- | --- | ------------- | --- | ----------------- | ------- | --- |
ArthurSzlam,Y-LanBoureau,MelanieKambadur,
|                      |     |              |           |     | Sadagopan, | Dirk | Rowe, Shannon | Spruit, | Chau |
| -------------------- | --- | ------------ | --------- | --- | ---------- | ---- | ------------- | ------- | ---- |
| andJasonWeston.2022. |     | Blenderbot3: | adeployed |     |            |      |               |         |      |
conversationalagentthatcontinuallylearnstorespon- Tran, Pierre Andrews, Necip Fazil Ayan, Shruti
| siblyengage. |     |     |     |     | Bhosale, | Sergey | Edunov, | Angela Fan, | Cynthia |
| ------------ | --- | --- | --- | --- | -------- | ------ | ------- | ----------- | ------- |
Gao,VedanujGoswami,FranciscoGuzmán,Philipp
Koustuv Sinha, Shagun Sodhani, Jin Dong, Joelle Koehn, AlexandreMourachko, ChristopheRopers,
Pineau,andWilliamLHamilton.2019. Clutrr: Adi- SafiyyahSaleem,HolgerSchwenk,andJeffWang.
agnosticbenchmarkforinductivereasoningfromtext.
|     |     |     |     |     | 2022. No | language | left behind: | Scaling | human- |
| --- | --- | --- | --- | --- | -------- | -------- | ------------ | ------- | ------ |
InProceedingsofthe2019ConferenceonEmpirical centeredmachinetranslation.
MethodsinNaturalLanguageProcessingandthe9th
InternationalJointConferenceonNaturalLanguage RichmondThomason.2018. Logicandartificialintelli-
| Processing(EMNLP-IJCNLP),pages4506–4515. |     |     |     |     | gence. |     |     |     |     |
| ---------------------------------------- | --- | --- | --- | --- | ------ | --- | --- | --- | --- |
NoahSmith.2023. Whydoeschatgptconstantlylie? RomalThoppilan,DanielDeFreitas,JamieHall,Noam
|     |     |     |     |     | Shazeer, | Apoorv | Kulshreshtha, | Heng-Tze | Cheng, |
| --- | --- | --- | --- | --- | -------- | ------ | ------------- | -------- | ------ |
Aarohi Srivastava, Abhinav Rastogi, Abhishek Rao, Alicia Jin, Taylor Bos, Leslie Baker, Yu Du, et al.
AbuAwalMdShoeb,AbubakarAbid,AdamFisch, 2022. Lamda: Languagemodelsfordialogapplica-
Adam R Brown, Adam Santoro, Aditya Gupta, tions. arXivpreprintarXiv:2201.08239.
689

H Holden Thorp. 2023. Chatgpt is fun, but not an Jason Weston, Antoine Bordes, Sumit Chopra, and
| author. |     |     |     |     |     |     | TomásMikolov.2016a. |     |       | Towardsai-completeques- |     |     |           |
| ------- | --- | --- | --- | --- | --- | --- | ------------------- | --- | ----- | ----------------------- | --- | --- | --------- |
|         |     |     |     |     |     |     | tion answering:     |     | A set | of prerequisite         |     | toy | tasks. In |
Giuseppe Venuto. 2023. Giuven95/chatgpt-failures: 4thInternationalConferenceonLearningRepresen-
Chatgptfailurearchive. tations,ICLR2016,SanJuan,PuertoRico,May2-4,
2016,ConferenceTrackProceedings.
| DouglasWalton.2014. |     |     | Abductivereasoning. |     |     | Univer- |     |     |     |     |     |     |     |
| ------------------- | --- | --- | ------------------- | --- | --- | ------- | --- | --- | --- | --- | --- | --- | --- |
sityofAlabamaPress. JasonWeston,AntoineBordes,SumitChopra,Alexan-
derMRush,BartVanMerriënboer,ArmandJoulin,
Ada Wan. 2022. Fairness in representation for multi- and Tomas Mikolov. 2016b. Towards ai-complete
|     |     |     |     |     |     |     | questionanswering: |     |     | Asetofprerequisitetoytasks. |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | ------------------ | --- | --- | --------------------------- | --- | --- | --- |
lingualNLP:Insightsfromcontrolledexperiments
In4thInternationalConferenceonLearningRepre-
| onconditionallanguagemodeling.       |           |     |        | InInternational |          |     |                      |         |            |     |       |       |         |
| ------------------------------------ | --------- | --- | ------ | --------------- | -------- | --- | -------------------- | ------- | ---------- | --- | ----- | ----- | ------- |
| ConferenceonLearningRepresentations. |           |     |        |                 |          |     | sentations,ICLR2016. |         |            |     |       |       |         |
|                                      |           |     |        |                 |          |     | Bryan Wilie,         | Karissa | Vincentio, |     | Genta | Indra | Winata, |
| Alex Wang,                           | Amanpreet |     | Singh, | Julian          | Michael, | Fe- |                      |         |            |     |       |       |         |
SamuelCahyawijaya,XiaohongLi,ZhiYuanLim,
| lix Hill,                            | Omer         | Levy, | and Samuel | Bowman. |            | 2018a. |                        |     |        |           |          |              |       |
| ------------------------------------ | ------------ | ----- | ---------- | ------- | ---------- | ------ | ---------------------- | --- | ------ | --------- | -------- | ------------ | ----- |
|                                      |              |       |            |         |            |        | Sidik Soleman,         |     | Rahmad | Mahendra, |          | Pascale      | Fung, |
| GLUE:                                | A multi-task |       | benchmark  | and     | analysis   | plat-  |                        |     |        |           |          |              |       |
|                                      |              |       |            |         |            |        | SyafriBahar,etal.2020. |     |        |           | Indonlu: | Benchmarkand |       |
| formfornaturallanguageunderstanding. |              |       |            |         | InProceed- |        |                        |     |        |           |          |              |       |
resourcesforevaluatingindonesiannaturallanguage
| ings of | the 2018 | EMNLP | Workshop | BlackboxNLP: |     |     |                |     |                                 |     |     |     |     |
| ------- | -------- | ----- | -------- | ------------ | --- | --- | -------------- | --- | ------------------------------- | --- | --- | --- | --- |
|         |          |       |          |              |     |     | understanding. |     | InProceedingsofthe1stConference |     |     |     |     |
AnalyzingandInterpretingNeuralNetworksforNLP,
|     |     |     |     |     |     |     | of the | Asia-Pacific |     | Chapter | of the | Association | for |
| --- | --- | --- | --- | --- | --- | --- | ------ | ------------ | --- | ------- | ------ | ----------- | --- |
pages353–355,Brussels,Belgium.Associationfor
ComputationalLinguisticsandthe10thInternational
ComputationalLinguistics.
JointConferenceonNaturalLanguageProcessing,
pages843–857.
| SuWang,GregDurrett,andKatrinErk.2018b. |     |     |     |     |     | Model- |     |     |     |     |     |     |     |
| -------------------------------------- | --- | --- | --- | --- | --- | ------ | --- | --- | --- | --- | --- | --- | --- |
ingsemanticplausibilitybyinjectingworldknowl-
GentaIndraWinata,AlhamFikriAji,SamuelCahyawi-
edge. arXivpreprintarXiv:1804.00619.
|     |     |     |     |     |     |     | jaya, Rahmad |       | Mahendra,  |     | Fajri Koto, | Ade       | Romad- |
| --- | --- | --- | --- | --- | --- | --- | ------------ | ----- | ---------- | --- | ----------- | --------- | ------ |
|     |     |     |     |     |     |     | hony,        | Kemal | Kurniawan, |     | David       | Moeljadi, | Radi-  |
XuezhiWang,JasonWei,DaleSchuurmans,QuocLe,
|                          |     |     |     |                     |     |     | tyo Eko | Prasojo, | Pascale |           | Fung, | Timothy   | Baldwin, |
| ------------------------ | --- | --- | --- | ------------------- | --- | --- | ------- | -------- | ------- | --------- | ----- | --------- | -------- |
| EdChi,andDennyZhou.2022. |     |     |     | Self-consistencyim- |     |     |         |          |         |           |       |           |          |
|                          |     |     |     |                     |     |     | Jey Han | Lau,     | Rico    | Sennrich, | and   | Sebastian | Ruder.   |
proveschainofthoughtreasoninginlanguagemod-
|     |     |     |     |     |     |     | 2022. | Nusax: | Multilingualparallelsentimentdataset |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | ----- | ------ | ------------------------------------ | --- | --- | --- | --- |
els. arXivpreprintarXiv:2203.11171.
for10indonesianlocallanguages.
YizhongWang,YeganehKordi,SwaroopMishra,Alisa CameronR.Wolfe.2023. Specializedllms: Chatgpt,
Liu,NoahA.Smith,DanielKhashabi,andHannaneh lamda,galactica,codex,sparrow,andmore.
| Hajishirzi. | 2023. | Self-instruct: |     | Aligning | language |     |     |     |     |     |     |     |     |
| ----------- | ----- | -------------- | --- | -------- | -------- | --- | --- | --- | --- | --- | --- | --- | --- |
modelswithself-generatedinstructions. InProceed- BigScienceWorkshop,:,TevenLeScao,AngelaFan,
ChristopherAkiki,ElliePavlick,SuzanaIlic´,Daniel
ingsofthe61stAnnualMeetingoftheAssociationfor
|                                   |     |     |     |     |              |     | Hesslow, | Roman | Castagné, |     | Alexandra |     | Sasha Luc- |
| --------------------------------- | --- | --- | --- | --- | ------------ | --- | -------- | ----- | --------- | --- | --------- | --- | ---------- |
| ComputationalLinguistics(Volume1: |     |     |     |     | LongPapers), |     |          |       |           |     |           |     |            |
pages13484–13508,Toronto,Canada.Association cioni, François Yvon, Matthias Gallé, Jonathan
forComputationalLinguistics. Tow, Alexander M. Rush, Stella Biderman, Albert
Webson,PawanSasankaAmmanamanchi,Thomas
Wang,BenoîtSagot,NiklasMuennighoff,AlbertVil-
| Peter Cathcart |     | Wason | and Philip | Nicholas | Johnson- |     |     |     |     |     |     |     |     |
| -------------- | --- | ----- | ---------- | -------- | -------- | --- | --- | --- | --- | --- | --- | --- | --- |
lanovadelMoral,OlatunjiRuwase,RachelBawden,
| Laird. | 1972. | Psychology | of  | reasoning: | Structure |     |     |     |     |     |     |     |     |
| ------ | ----- | ---------- | --- | ---------- | --------- | --- | --- | --- | --- | --- | --- | --- | --- |
andcontent,volume86. HarvardUniversityPress. Stas Bekman, Angelina McMillan-Major, Iz Belt-
agy,HuuNguyen,LucileSaulnier,SamsonTan,Pe-
TaylorWebb,KeithJ.Holyoak,andHongjingLu.2022a. dro Ortiz Suarez, Victor Sanh, Hugo Laurençon,
Emergent analogical reasoning in large language Yacine Jernite, Julien Launay, Margaret Mitchell,
|     |     |     |     |     |     |     | Colin | Raffel, | Aaron | Gokaslan, |     | Adi Simhi, | Aitor |
| --- | --- | --- | --- | --- | --- | --- | ----- | ------- | ----- | --------- | --- | ---------- | ----- |
models.
Soroa,AlhamFikriAji,AmitAlfassy,AnnaRogers,
TaylorWebb,KeithJHolyoak,andHongjingLu.2022b. ArielKreisbergNitzav,CanwenXu,ChenghaoMou,
Emergent analogical reasoning in large language Chris Emezue, Christopher Klamm, Colin Leong,
models. arXivpreprintarXiv:2212.09196. DanielvanStrien,DavidIfeoluwaAdelani,Dragomir
|            |     |            |            |     |       |         | Radev,  | Eduardo | González |      | Ponferrada, |        | Efrat Lev- |
| ---------- | --- | ---------- | ---------- | --- | ----- | ------- | ------- | ------- | -------- | ---- | ----------- | ------ | ---------- |
|            |     |            |            |     |       |         | kovizh, | Ethan   | Kim,     | Eyal | Bar         | Natan, | Francesco  |
| Jason Wei, | Yi  | Tay, Rishi | Bommasani, |     | Colin | Raffel, |         |         |          |      |             |        |            |
Barret Zoph, Sebastian Borgeaud, Dani Yogatama, De Toni, Gérard Dupont, Germán Kruszewski, Gi-
MaartenBosma,DennyZhou,DonaldMetzler,etal. adaPistilli,HadyElsahar,HamzaBenyamina,Hieu
2022a. Emergentabilitiesoflargelanguagemodels. Tran,IanYu,IdrisAbdulmumin,IsaacJohnson,Itziar
TransactionsonMachineLearningResearch. Gonzalez-Dios,JavierdelaRosa,JennyChim,Jesse
|     |     |     |     |     |     |     | Dodge, | Jian | Zhu, Jonathan |     | Chang, | Jörg | Frohberg, |
| --- | --- | --- | --- | --- | --- | --- | ------ | ---- | ------------- | --- | ------ | ---- | --------- |
JasonWei,XuezhiWang,DaleSchuurmans,Maarten Joseph Tobing, Joydeep Bhattacharjee, Khalid Al-
Bosma,FeiXia,EdHChi,QuocVLe,DennyZhou, mubarak,KimboChen,KyleLo,LeandroVonWerra,
etal.2022b. Chain-of-thoughtpromptingelicitsrea- Leon Weber, Long Phan, Loubna Ben allal, Lu-
soning in large language models. In Advances in dovicTanguy,MananDey,ManuelRomeroMuñoz,
NeuralInformationProcessingSystems. Maraim Masoud, María Grandury, Mario Šaško,
690

Max Huang, Maximin Coavoux, Mayank Singh, IrinaSedenko,IsarNejadgholi,JessePassmore,Josh
Mike Tian-Jian Jiang, Minh Chien Vu, Moham- Seltzer,JulioBonisSanz,LiviaDutra,MaironSama-
madA.Jauhar,MustafaGhaleb,NishantSubramani, gaio,MaraimElbadri,MargotMieskes,MarissaGer-
NoraKassner,NurulaqillaKhamis,OlivierNguyen, chick, Martha Akinlolu, Michael McKenna, Mike
Omar Espejel, Ona de Gibert, Paulo Villegas, Pe- Qiu, Muhammed Ghauri, Mykola Burynok, Nafis
ter Henderson, Pierre Colombo, Priscilla Amuok, Abrar, Nazneen Rajani, Nour Elkott, Nour Fahmy,
QuentinLhoest,RhezaHarliman,RishiBommasani, Olanrewaju Samuel, Ran An, Rasmus Kromann,
Roberto Luis López, Rui Ribeiro, Salomey Osei, RyanHao,SamiraAlizadeh,SarmadShubber,Silas
Sampo Pyysalo, Sebastian Nagel, Shamik Bose, Wang,SouravRoy,SylvainViguier,ThanhLe,Tobi
ShamsuddeenHassanMuhammad,ShanyaSharma, Oyebade,TrieuLe,YoyoYang,ZachNguyen,Ab-
ShayneLongpre,SomaiehNikpoor,StanislavSilber- hinav Ramesh Kashyap, Alfredo Palasciano, Al-
berg, Suhas Pai, Sydney Zink, Tiago Timponi Tor- ison Callahan, Anima Shukla, Antonio Miranda-
rent,TimoSchick,TristanThrush,ValentinDanchev, Escalada,AyushSingh,BenjaminBeilharz,BoWang,
Vassilina Nikoulina, Veronika Laippala, Violette Caio Brito, Chenxi Zhou, Chirag Jain, Chuxin
Lepercq,VrindaPrabhu,ZaidAlyafeai,ZeerakTa- Xu, Clémentine Fourrier, Daniel León Periñán,
lat,ArunRaja,BenjaminHeinzerling,ChengleiSi, DanielMolano,DianYu,EnriqueManjavacas,Fabio
Davut Emre Tas¸ar, Elizabeth Salesky, Sabrina J. Barth, Florian Fuhrimann, Gabriel Altay, Giyased-
Mielke, Wilson Y. Lee, Abheesht Sharma, Andrea dinBayrak,GullyBurns,HelenaU.Vrabec,Imane
Santilli,AntoineChaffin,ArnaudStiegler,Debajy- Bello,IshaniDash,JihyunKang,JohnGiorgi,Jonas
otiDatta,ElizaSzczechla,GunjanChhablani,Han Golde,JoseDavidPosada,KarthikRangasaiSivara-
Wang,HarshitPandey,HendrikStrobelt,JasonAlan man,LokeshBulchandani,LuLiu,LuisaShinzato,
Fries,JosRozen,LeoGao,LintangSutawika,MSai- Madeleine Hahn de Bykhovetz, Maiko Takeuchi,
fulBari,MagedS.Al-shaibani,MatteoManica,Ni- MarcPàmies,MariaACastillo,MariannaNezhurina,
hal Nayak, Ryan Teehan, Samuel Albanie, Sheng MarioSänger,MatthiasSamwald,MichaelCullan,
Shen,SrulikBen-David,StephenH.Bach,Taewoon MichaelWeinberg,MichielDeWolf,MinaMihalj-
Kim,TaliBers,ThibaultFevry,TrishalaNeeraj,Ur- cic,MinnaLiu,MoritzFreidank,MyungsunKang,
mishThakker,VikasRaunak,XiangruTang,Zheng- NatashaSeelam,NathanDahlberg,NicholasMichio
XinYong,ZhiqingSun,ShakedBrody,YallowUri, Broad, Nikolaus Muellner, Pascale Fung, Patrick
HadarTojarieh,AdamRoberts,HyungWonChung, Haller, Ramya Chandrasekhar, Renata Eisenberg,
JaesungTae,JasonPhang,OfirPress,ConglongLi, RobertMartin,RodrigoCanalli,RosalineSu,Ruisi
DeepakNarayanan,HatimBourfoune,JaredCasper, Su,SamuelCahyawijaya,SamueleGarda,ShlokS
JeffRasley,MaxRyabinin,MayankMishra,Minjia Deshmukh, Shubhanshu Mishra, Sid Kiblawi, Si-
Zhang,MohammadShoeybi,MyriamPeyrounette, monOtt,SineeSang-aroonsiri,SrishtiKumar,Ste-
Nicolas Patry, Nouamane Tazi, Omar Sanseviero, fan Schweter, Sushil Bharati, Tanmay Laud, Théo
PatrickvonPlaten,PierreCornette,PierreFrançois Gigant, Tomoya Kainuma, Wojciech Kusa, Yanis
Lavallée,RémiLacroix,SamyamRajbhandari,San- Labrak,YashShaileshBajaj,YashVenkatraman,Yi-
chitGandhi,ShadenSmith,StéphaneRequena,Suraj fanXu,YingxinXu,YuXu,ZheTan,ZhongliXie,Zi-
Patil, Tim Dettmers, Ahmed Baruwa, Amanpreet fanYe,MathildeBras,YounesBelkada,andThomas
Singh, Anastasia Cheveleva, Anne-Laure Ligozat, Wolf.2022. Bloom: A176b-parameteropen-access
ArjunSubramonian,AurélieNévéol,CharlesLover- multilinguallanguagemodel.
ing,DanGarrette,DeepakTunuguntla,EhudReiter,
Yan Xu, Etsuko Ishii, Samuel Cahyawijaya, Zihan
EkaterinaTaktasheva,EkaterinaVoloshina,EliBog-
Liu,GentaIndraWinata,AndreaMadotto,DanSu,
danov,GentaIndraWinata,HaileySchoelkopf,Jan-
andPascaleFung.2022. Retrieval-freeknowledge-
ChristophKalo,JekaterinaNovikova,JessicaZosa
groundeddialogueresponsegenerationwithadapters.
Forde, JordanClive, JungoKasai, KenKawamura,
InProceedingsoftheSecondDialDocWorkshopon
LiamHazan,MarineCarpuat,MirunaClinciu,Na-
Document-groundedDialogueandConversational
joung Kim, Newton Cheng, Oleg Serikov, Omer
QuestionAnswering,pages93–107.
Antverg, Oskar van der Wal, Rui Zhang, Ruochen
Zhang,SebastianGehrmann,ShacharMirkin,Shani
YanXu,DeqianKong,DehongXu,ZiweiJi,BoPang,
Pais,TatianaShavrina,ThomasScialom,TianYun,
PascaleFung,andYingNianWu.2023. Diverseand
TomaszLimisiewicz,VerenaRieser,VitalyProtasov,
faithfulknowledge-groundeddialoguegenerationvia
VladislavMikhailov,YadaPruksachatkun,Yonatan
sequentialposteriorinference. InProceedingsofthe
Belinkov,ZacharyBamberger,ZdeneˇkKasner,Al-
40thInternationalConferenceonMachineLearning,
iceRueda,AmandaPestana,AmirFeizpour,Ammar
volume 202 of Proceedings of Machine Learning
Khan, Amy Faranak, Ana Santos, Anthony Hevia,
Research,pages38518–38534.PMLR.
AntigonaUnldreaj,ArashAghagol,ArezooAbdol-
lahi,AychaTammour,AzadehHajiHosseini,Bahareh YunyiYang,YunhaoLi,andXiaojunQuan.2021. Ubar:
Behroozi, Benjamin Ajibade, Bharat Saxena, Car- Towardsfullyend-to-endtask-orienteddialogsystem
losMuñozFerrandis,DanishContractor,DavidLan- withgpt-2. ProceedingsoftheAAAIConferenceon
sky,DavisDavid,DouweKiela,DuongA.Nguyen, ArtificialIntelligence,35(16):14230–14238.
Edward Tan, Emi Baylor, Ezinwanne Ozoani, Fa-
timaMirza,FranklineOnoniwu, HabibRezanejad, ZhilinYang,PengQi,SaizhengZhang,YoshuaBengio,
HessieJones,IndraniBhattacharya,IreneSolaiman, WilliamCohen,RuslanSalakhutdinov,andChristo-
pher D Manning. 2018. Hotpotqa: A dataset for
691

| diverse,       | explainablemulti-hopquestionanswering. |        |                 |     |            |
| -------------- | -------------------------------------- | ------ | --------------- | --- | ---------- |
| In Proceedings |                                        | of the | 2018 Conference |     | on Empiri- |
calMethodsinNaturalLanguageProcessing,pages
2369–2380.
| Tiezheng    | Yu, Wenliang | Dai,                              | Zihan | Liu, | and Pascale |
| ----------- | ------------ | --------------------------------- | ----- | ---- | ----------- |
| Fung.2021a. |              | Visionguidedgenerativepre-trained |       |      |             |
languagemodelsformultimodalabstractivesumma-
| rization. | InProceedingsofthe2021Conferenceon |     |     |     |     |
| --------- | ---------------------------------- | --- | --- | --- | --- |
EmpiricalMethodsinNaturalLanguageProcessing,
pages3995–4007,OnlineandPuntaCana,Domini-
| can Republic. |     | Association | for | Computational | Lin- |
| ------------- | --- | ----------- | --- | ------------- | ---- |
guistics.
| Tiezheng                         | Yu, Zihan | Liu,         | and Pascale |               | Fung. 2021b. |
| -------------------------------- | --------- | ------------ | ----------- | ------------- | ------------ |
| Adaptsum:                        | Towards   | low-resource |             | domain        | adapta-      |
| tionforabstractivesummarization. |           |              |             | InProceedings |              |
ofthe2021ConferenceoftheNorthAmericanChap-
teroftheAssociationforComputationalLinguistics:
HumanLanguageTechnologies,pages5892–5904.
| Xiaoxue | Zang,        | Abhinav                   | Rastogi, | Srinivas    | Sunkara, |
| ------- | ------------ | ------------------------- | -------- | ----------- | -------- |
| Raghav  | Gupta,       | Jianguo                   | Zhang,   | and Jindong | Chen.    |
| 2020.   | Multiwoz2.2: | Adialoguedatasetwithaddi- |          |             |          |
tionalannotationcorrectionsandstatetrackingbase-
lines. ACL2020,page109.
EricZelikman,YuhuaiWu,JesseMu,andNoahGood-
| man.2022. | Star:                                 | Bootstrappingreasoningwithrea- |     |     |     |
| --------- | ------------------------------------- | ------------------------------ | --- | --- | --- |
| soning.   | InAdvancesinNeuralInformationProcess- |                                |     |     |     |
ingSystems.
TianyiZhang*,VarshaKishore*,FelixWu*,KilianQ.
| Weinberger,andYoavArtzi.2020. |                 |     |            | Bertscore: | Eval-         |
| ----------------------------- | --------------- | --- | ---------- | ---------- | ------------- |
| uating                        | text generation |     | with bert. | In         | International |
ConferenceonLearningRepresentations.
| Jeffrey Zhao,                   | Raghav        | Gupta,   | Yuanbin          | Cao,    | Dian Yu,     |
| ------------------------------- | ------------- | -------- | ---------------- | ------- | ------------ |
| Mingqiu                         | Wang,         | Harrison | Lee,             | Abhinav | Rastogi,     |
| IzhakShafran,andYonghuiWu.2022. |               |          |                  |         | Description- |
| driven                          | task-oriented |          | dialog modeling. |         | ArXiv,       |
abs/2201.08904.
| Xueliang | Zhao, | Wei Wu, | Can Xu, | Chongyang | Tao,       |
| -------- | ----- | ------- | ------- | --------- | ---------- |
| Dongyan  | Zhao, | and Rui | Yan.    | 2020.     | Knowledge- |
groundeddialoguegenerationwithpre-trainedlan-
| guagemodels. |           | InProceedingsofthe2020Confer- |     |         |          |
| ------------ | --------- | ----------------------------- | --- | ------- | -------- |
| ence on      | Empirical | Methods                       | in  | Natural | Language |
Processing(EMNLP),pages3377–3390.
| Terry Yue | Zhuo,        | Yujin Huang, | Chunyang  |       | Chen, and    |
| --------- | ------------ | ------------ | --------- | ----- | ------------ |
| Zhenchang | Xing.        | 2023a.       | Exploring |       | ai ethics of |
| chatgpt:  | A diagnostic |              | analysis. | arXiv | preprint     |
arXiv:2301.12867.
| Terry Yue            | Zhuo,                                | Yujin Huang, | Chunyang             |     | Chen, and |
| -------------------- | ------------------------------------ | ------------ | -------------------- | --- | --------- |
| ZhenchangXing.2023b. |                                      |              | Redteamingchatgptvia |     |           |
| jailbreaking:        | Bias,robustness,reliabilityandtoxic- |              |                      |     |           |
ity.
692

Appendix
|     |     |     |     |     |     |     | otherdisciplines. |     | Alineofdiscussionisthespecific |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | ----------------- | --- | ------------------------------ | --- | --- | --- | --- |
emergentabilityandstrengthofChatGPTinmore
Theappendixconsiststhefollowingcontent:
|     |     |     |     |     |     |     | technicalperspectives. |     |     | Guoetal.(2023)conducts |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | ---------------------- | --- | --- | ---------------------- | --- | --- | --- |
• A:BackgroundandRelatedWork linguistic analyses of ChatGPT’s writing against
humanexpertsandfoundthatChatGPTresponses
• B:GeneralExperimentalDetails
|     |     |     |     |     |     |     | are strictly | focused |     | on the | given | question, | more |
| --- | --- | --- | --- | --- | --- | --- | ------------ | ------- | --- | ------ | ----- | --------- | ---- |
• C:DetailsforMultitaskEvaluation
|     |     |     |     |     |     |     | formal, | objective, | and | less | emotional. |     | Nov et al. |
| --- | --- | --- | --- | --- | --- | --- | ------- | ---------- | --- | ---- | ---------- | --- | ---------- |
• D:DetailsforMultilingualityEvaluation
(2023)alsostudiesChatGPT’sgeneratedmedical
|     |     |     |     |     |     |     | advice | if it passes |     | the Turing | test. | Frieder | et al. |
| --- | --- | --- | --- | --- | --- | --- | ------ | ------------ | --- | ---------- | ----- | ------- | ------ |
• E:Multimodality–FlagDrawingTask
(2023)showthat“significantlybelowthoseofan
• F:DetailsforReasoningEvaluation
|     |     |     |     |     |     |     | averagemathematicsgraduatestudent.” |     |     |     |     |     | Thereare |
| --- | --- | --- | --- | --- | --- | --- | ----------------------------------- | --- | --- | --- | --- | --- | -------- |
• G:DetailsforHallucinationEvaluations
manyinvestigationsofChatGPT’sunderstanding
• H:DetailsforInteractivityEvaluation and potential applications in different fields such
• I:ListofEvaluationDatasets aslaw(Choietal.,2023),medicaldomain(Blanco-
• J: Examples from Machine Translation and Gonzalez et al., 2022; Jeblick et al., 2022) and
finance(Birch,2022;DowlingandLucey,2023).
Post-Editing
|     |     |     |     |     |     |     | Jeblick | et al. | (2022) | conduct | a case | study | of the |
| --- | --- | --- | --- | --- | --- | --- | ------- | ------ | ------ | ------- | ------ | ----- | ------ |
A BackgroundandRelatedWork application of ChatGPT on simplified radiology
|     |     |     |     |     |     |     | reports. | Another | important |     | line of | discussion | is  |
| --- | --- | --- | --- | --- | --- | --- | -------- | ------- | --------- | --- | ------- | ---------- | --- |
A.1 ChatGPT
theethicalconcernsovertheuseofChatGPT.The
ComparedtoexistingLLMs,ChatGPThasunique
mostactivediscussionisovertheuseofacademic
| characteristics. |     | First, it | has the | ability | to interact |     |     |     |     |     |     |     |     |
| ---------------- | --- | --------- | ------- | ------- | ----------- | --- | --- | --- | --- | --- | --- | --- | --- |
writingandexamintegrity(JabotinskyandSarel,
with users in a conversation-like manner, while 2022;Susnjak,2022). OpenAIalsodiscussesthe
retainingitsaccumulatedknowledgeandgeneral- misuseofLMfordisinformationandremedies. 2
| ization | ability gained | from | pre-training. |     |     | This is |           |                                  |     |     |     |     |     |
| ------- | -------------- | ---- | ------------- | --- | --- | ------- | --------- | -------------------------------- | --- | --- | --- | --- | --- |
|         |                |      |               |     |     |         | Zhuoetal. | studyAIethicsofChatGPTincriteria |     |     |     |     |     |
achievedbypre-trainingChatGPTonalarge-scale ofbias,reliability,robustness,andtoxicity.
conversational-styledataset,thatisconstructedby
transforming a large-scale instruction-tuning cor- A.2 LLMbenchmarkandevaluation
pususedforbuildingInstructGPTintoaconversa-
|     |     |     |     |     |     |     | With the | advancement |     | of  | LLMs’ | generalization |     |
| --- | --- | --- | --- | --- | --- | --- | -------- | ----------- | --- | --- | ----- | -------------- | --- |
tionalformat,thenfine-tuningthemodelbasedon
ability,therehavebeeneffortstounderstandtheir
arewardmodeltofurtherimprovethegeneration
|     |     |     |     |     |     |     | capabilities, | limitations, |     | and | risks. | Recently, | sev- |
| --- | --- | --- | --- | --- | --- | --- | ------------- | ------------ | --- | --- | ------ | --------- | ---- |
qualityandalignthegenerationwithhuman
eralbenchmarkswithacollectionofalargenumber
Second,ChatGPTistrainedwithabetterhuman-
|         |           |          |     |                   |     |     | of NLP | datasets, | such | as  | BIG-Bench | (Srivastava |     |
| ------- | --------- | -------- | --- | ----------------- | --- | --- | ------ | --------- | ---- | --- | --------- | ----------- | --- |
| aligned | objective | function |     | via Reinforcement |     |     |        |           |      |     |           |             |     |
etal.,2022)andAILMHarness(Gaoetal.,2021),
| Learning          | from | Human                       | Feedback | (RLHF) |     | (Chris- |           |             |     |           |     |      |        |
| ----------------- | ---- | --------------------------- | -------- | ------ | --- | ------- | --------- | ----------- | --- | --------- | --- | ---- | ------ |
|                   |      |                             |          |        |     |         | have been | introduced. |     | Moreover, |     | HELM | (Liang |
| tianoetal.,2017). |      | Conventionalnaturallanguage |          |        |     |         |           |             |     |           |     |      |        |
etal.,2022)isproposedtoconductaholisticevalu-
| generation | models, | including |     | dialogue | models, |     |     |     |     |     |     |     |     |
| ---------- | ------- | --------- | --- | -------- | ------- | --- | --- | --- | --- | --- | --- | --- | --- |
ationofLLMsthatconsidersscenariosandmetrics
are trained with maximum likelihood estimation withatop-downapproach. Inthiswork,weinstead
(MLE)andmightnotbealignedwithhumanpref-
focusonspecificlimitationsanduniquefindingsof
| erences. | For instance, |     | for dialogue |     | systems, | hu- |     |     |     |     |     |     |     |
| -------- | ------------- | --- | ------------ | --- | -------- | --- | --- | --- | --- | --- | --- | --- | --- |
ChatGPTthathadnotbeendiscussedwithprevious
manness,engagement,andgroundednessaresome
LLMs.
| examples | of essential |     | criteria | for success. |     | Such |       |          |       |       |      |         |       |
| -------- | ------------ | --- | -------- | ------------ | --- | ---- | ----- | -------- | ----- | ----- | ---- | ------- | ----- |
|          |              |     |          |              |     |      | There | are also | other | works | that | discuss | LLMs’ |
discrepancybetweentrainingobjectivesandevalu-
emergentabilitiesthroughthoroughsurveysorcase
ationmetricsbecomesabottlenecktoperformance
|              |     |          |       |         |     |        | studies. | Mahowald |     | et al. | (2023) thoroughly |     | stud- |
| ------------ | --- | -------- | ----- | ------- | --- | ------ | -------- | -------- | --- | ------ | ----------------- | --- | ----- |
| improvement. |     | By using | RLHF, | ChatGPT |     | aligns |          |          |     |        |                   |     |       |
iesLLMscapabilitiesbydistinguishingformaland
morecloselywithhumanpreferencesingenerating
functionallinguisticcompetencewithreferenceto
textthanbyusingMLE.
cognitivescience,psychology,andNLPtoclarify
DiscussiononitsCapability
|            |     |            |     |           |     |        | thediscoursesurroundingLLMs’potential. |     |     |     |     |     | Other |
| ---------- | --- | ---------- | --- | --------- | --- | ------ | -------------------------------------- | --- | --- | --- | --- | --- | ----- |
| As ChatGPT |     | has become |     | available | to  | public |                                        |     |     |     |     |     |       |
worksfocusonmorespecificabilitiessuchasmath-
| users through | an  | easily | accessible | UI, | there | have |          |        |         |         |           |     |       |
| ------------- | --- | ------ | ---------- | --- | ----- | ---- | -------- | ------ | ------- | ------- | --------- | --- | ----- |
|               |     |        |            |     |       |      | ematical | skills | (Davis, | 2023b), | reasoning |     | (Webb |
beenmanydiscussionsfromawiderangeofcom-
| munities, | not just | from | AI or | NLP, | but also | from |     |     |     |     |     |     |     |
| --------- | -------- | ---- | ----- | ---- | -------- | ---- | --- | --- | --- | --- | --- | --- | --- |
2https://openai.com/blog/forecasting-misuse/
693

etal.,2022a;Qiaoetal.,2022). Also, therehave 2020b) model fine-tuned on both datasets is con-
beenoverviewsofexistingLLMs(Gozalo-Brizuela ductedforcomparison. Moreover,OpenAI’stext-
andGarrido-Merchan,2023;Wolfe,2023) davinci-002isusedasthepreviousSOTAzero-shot
|     |     |     |     |     |     | model. | We calculate | ROUGE-1 |     | scores | for evalu- |
| --- | --- | --- | --- | --- | --- | ------ | ------------ | ------- | --- | ------ | ---------- |
A.3 ChatGPTEvaluation ating the generated summary. According to the
Tothebestofourknowledge,thisbenchmarking evaluation,ChatGPTachievesasimilarzero-shot
exerciseisthefirstofitskind. Sincetheintroduc- performance with text-davinci-002, which is ex-
| tionof ChatGPTwith |     | itsadvancement, |     |     | there has |     |     |     |     |     |     |
| ------------------ | --- | --------------- | --- | --- | --------- | --- | --- | --- | --- | --- | --- |
pectedsincetheyevolvedfromthesameGPT3pre-
beenahugeamountofassessmentsofChatGPTto trainedcheckpoint. However,thefine-tunedBart
understanditslimits. Maoetal.(2023)providesa still outperforms zero-shot ChatGPT by a large
| surveyofrecentassessmentsofChatGPTinbroad |     |     |     |     |     | margin. |     |     |     |     |     |
| ----------------------------------------- | --- | --- | --- | --- | --- | ------- | --- | --- | --- | --- | --- |
categoriesof1)LanguageandReasoningAbility,
C.2 MachineTranslation
2)ScientificKnowledge,and3)EthicalConsidera-
tions. Laskaretal. provideextensiveautomaticor WeevaluatethemachinetranslationabilityofChat-
| human-in-the-loopevaluationson140tasks. |     |     |     |     | Qin |     |     |     |     |     |     |
| --------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
GPTonbothhigh-resourceandlow-resourcelan-
et al. mainly evaluated the reasoning abilities of guagesusingtheChrF++metric(Popovic´,2015).
ChatGPT while Zhuo et al.; Ray focus on other Specifically, we incorporate 8 high-resource lan-
important aspects such as ethics, robustness, reli- guages, i.e., French (fra), Spanish (spa), Chinese
ability, limitations, andfuturescopeofChatGPT. (zho), Arabic (ara), Japanese (jpn), Indonesian
Kocon´ et al. examined whether the high quality (ind), Korean (kor), and Vietnamese (vie), and 4
oftheLLMcanindicateatool’susefulnesstoso- low-resourcelanguages, i.e., Javanese(jav), Sun-
cietybyevaluatingChatGPT’scapabilitieson25 danese (sun), Marathi (mar), and Buginese (bug)
diverse analytical NLP tasks, most of them sub- for our evaluation. 3 For each language pair, we
jectiveeventohumans. Aftertheintroductionof sample30Eng↔XXXparallelsentencesfromthe
ChatGPT,GPT-4hasbeenintroducedbyOpenAI. FLORES-200 dataset (Team et al., 2022; Goyal
However, OpenAI is not disclosing any internal et al., 2021). The result of our experiment sug-
benchmarking of ChatGPT. Even in their GPT-4 geststhatChatGPTcanwellperformXXX→Eng
technicalreport(OpenAI,2023),theyhaveshown translation,butitstilllackstheabilitytoperform
| theperformanceofGPT4intermsofhuman-level |     |     |     |     |     | Eng→XXXtranslation. |     |     |     |     |     |
| ---------------------------------------- | --- | --- | --- | --- | --- | ------------------- | --- | --- | --- | --- | --- |
exams. So,itisimportantthatthereare3rdparty
C.3 SentimentAnalysis
evaluationsofgenerativemodels.
|     |     |     |     |     |     | Sentiment | analysis | has | been widely |     | explored |
| --- | --- | --- | --- | --- | --- | --------- | -------- | --- | ----------- | --- | -------- |
B GeneralExperimentalDetails
|                 |      |      |      |     |            | for both | high-resource |             | and low-resource |     | lan-       |
| --------------- | ---- | ---- | ---- | --- | ---------- | -------- | ------------- | ----------- | ---------------- | --- | ---------- |
|                 |      |      |      |     |            | guages   | (Wang et      | al., 2018a; | Wilie            | et  | al., 2020; |
| The experiments | were | done | with | the | UI (15 De- |          |               |             |                  |     |            |
Ilmaniaetal.,2018).
| cember 2019       | version)   | of      | ChatGPT        | provided     | by         |            |              |             |       |          |         |
| ----------------- | ---------- | ------- | -------------- | ------------ | ---------- | ---------- | ------------ | ----------- | ----- | -------- | ------- |
|                   |            |         |                |              |            | We         | explore the  | sentiment   |       | analysis | ability |
| OpenAI,           | before the | ChatGPT | API            | was          | released.  |            |              |             |       |          |         |
|                   |            |         |                |              |            | of ChatGPT | through      | 4 languages |       | with     | diverse |
| The number        | of samples |         | for evaluation |              | is 30-200. |            |              |             |       |          |         |
|                   |            |         |                |              |            | amounts    | of resources | in          | NusaX | (Winata  | et al., |
| We’ve prioritized |            | sample  | diversity,     | hand-picking |            |            |              |             |       |          |         |
tasksthatencapsulatetheabroadspectrumofsce- 2022): English (eng), Indonesian (ind), Javanese
|     |     |     |     |     |     | (jav), and | Buginese | (bug). | For | each | language, |
| --- | --- | --- | --- | --- | --- | ---------- | -------- | ------ | --- | ---- | --------- |
nariosalanguagemodelislikelytoencounter,thus
|     |     |     |     |     |     | we sample | 50 sentences | from | the | corresponding |     |
| --- | --- | --- | --- | --- | --- | --------- | ------------ | ---- | --- | ------------- | --- |
creatingarepresentativesnapshotofpotentialreal-
worldapplications. Allexperimentsaresingle-run. datasetforourexperimentandmeasurethemacro
|     |     |     |     |     |     | F1scoreastheevaluationmetric. |     |     |     | Wecomparethe |     |
| --- | --- | --- | --- | --- | --- | ----------------------------- | --- | --- | --- | ------------ | --- |
C MultitaskEvaluationofChatGPT results with two baselines, i.e., supervised state-
|     |     |     |     |     |     | of-the-art | performance | from | Winata | et  | al. (2022) |
| --- | --- | --- | --- | --- | --- | ---------- | ----------- | ---- | ------ | --- | ---------- |
C.1 Summarization
andzero-shotmultilingualLLMfromCahyawijaya
We test on 100 samples from two common sum- etal.(2022). ChatGPToutperformstheprevious
marization datasets: half from SAMSum (Gliwa state-of-the-artzero-shotmodelbyalargemargin
| et al., 2019), | a dialogue |     | summarization |     | dataset, |     |     |     |     |     |     |
| -------------- | ---------- | --- | ------------- | --- | -------- | --- | --- | --- | --- | --- | --- |
exceptfortheBuginese,whereitperformsonpar.
andanotherhalffromCNN/DM(Hermannetal.,
3Forafairercomparisoninourmultitaskexperiment,we
2015;Nallapatietal.,2016),newssummarization
strictlyfollowthedefinitionofhigh-resourceandlow-resource
| datasets. | The large | version | of Bart | (Lewis | et al., |     |     |     |     |     |     |
| --------- | --------- | ------- | ------- | ------ | ------- | --- | --- | --- | --- | --- | --- |
languagesfromNLLB(Teametal.,2022).
694

ThisshowsthatChatGPTstillhasalimitedunder- C.6.2 Task-OrientedDialogueExperimental
standingofextremelylow-resourcelanguages. Setups
Setup A: Modular Approach We investigate
C.4 QuestionAnswering ChatGPT’s ability for both dialogue state track-
ing and response generation in 50 dialogue turn
SinceQuestionAnswering(QA)isabroadtopic,
samples taken from MultiWOZ2.2 (Zang et al.,
we classify QA datasets into different categories
2020). Indetail,weaskthemodeltoprovidethe
based on the knowledge/reasoning type required
belief state as domain-intent: [slot1, value1], ...
to do the task, e.g commonsense reasoning, spa-
in the prompt following previous zero-shot (Lin
tialreasoning,temporalreasoning,etc.,tohavea
etal.,2021)andfew-shot(Madottoetal.,2021)ap-
cleareranalysisonChatGPT’sabilities. Foreach
proaches,andprovideanexhaustivelistofdomain-
category, we select several datasets, and for each
intent-slot-value for the given dialogue. For the
dataset,wesample30instancesandtestChatGPT
response generation, we provide only the oracle
on the subset. Based on our experiment results,
dialogueactions(e.g. ’Hotel-Inform’:[’area’,’cen-
ChatGPT outperforms the existing zero-shot and
tre’]), and ask ChatGPT to generate a TOD re-
someofthefine-tunedstate-of-the-artperformance
sponsegiventhedialoguehistory. WeassessDST
on question answering. Furthermore, ChatGPT
with joint goal accuracy (JGA), the ratio of dia-
achieves near-perfect scores on three tasks, i.e.,
logue turns where the predicted dialogue state is
bAbItask15,EntailmentBank,andPep-3k.
exactlythegroundtruth,andresponsegeneration
withBLEUandinformrate(%)
C.5 MisinformationDetection
Setup B: Unified Approach We explore Chat-
We test ChatGPT’s ability to detect misinforma- GPT’s ability to simulate a TOD interaction in
tion with the test sets that consist of scientific anend-to-endmannerbyprovidingnothingmore
andsocialclaimsrelatedtoCOVID-19(Leeetal., than a structured database and giving the instruc-
2021)with100samples. Wetakehalffromscien- tion: “Use the following knowledge base
tific(covid-scientific)andanotherhalffromsocial to complete the task of recommending a
(covid-social) sets. We evaluate the accuracy of restaurant as a task-oriented dialogue
the veracity by manually checking the generated system”.
text. ChatGPT could detect misinformation 92% ResultAnalysis: Wecouldinvestigatewhether
(46/50)and73.33%(22/30,excludingverification- ChatGPTisabletocompletebasicretrievalqueries
refusing cases) accuracy on covid-scientific and and respond to users’ requests such as “Give me
covid-socialrespectively. some restaurants that serve Italian food” or “I
wouldprefercheapoptionsplease”. However,there
C.6 ChatGPTonDialogueTasks areseverallimitationsthatwecouldinvestigateas
follow.
C.6.1 Knowledge-GroundedOpen-Domain
Dialogue • Long-termMulti-turnDependency: Chat-
GPTcannotkeepthebeliefstateacrossmulti-
Open-domain dialogue systems interact with hu-
pleturnswithintheinteraction. Forinstance,
manswithgeneratedresponsesautomaticallyand
askingforItalianfoodwilloverwritetheprevi-
aimtoprovideuserswithanengagingexperience.
ousturn’sbeliefstatebyaskingforrestaurants
Toboostinformativeness,thesesystemsleverage
with a rating of 3 or higher. However, if the
external knowledge, including structured knowl-
userexplicitlyaskstorecalltheearlierprefer-
edgesuchasknowledgegraphs(Zhaoetal.,2020;
ences,ChatGPTisabletocorrecttheretrieved
Jietal.,2022b)andunstructuredknowledgesuch
informationandincorporatethepreviousbe-
asfreetext(Xuetal.,2022,2023).
liefstate. Thisisinterestingasitshowsthat
Prompt used for experiment: “Can we try
theinformationpreviouslygiveninmulti-turn
dialogue generation? I will give you
isstillusable,butneedstobecalledexplicitly.
turns, and you can generate the next turn,
but only one.\n \n You can also consider • Basic Reasoning Failure: ChatGPT’s re-
the knowledge of XXX for your reference sponse tends to be wrong if the query intro-
in the dialogue.” ducesabasiclevelofreasoningsuchaswhen
695

| it is asked | for | “recommendation |     | for restau- |
| ----------- | --- | --------------- | --- | ----------- |
rantswithEuropeanfood”(ChatGPThasto
filterthetypesofcuisinewhicharebasedon
countries)or“recommendationforrestaurants
witharatingof3orhigher”(ChatGPTneeds
| to understand |     | rating 3, 4 | and 5). | Even with |
| ------------- | --- | ----------- | ------- | --------- |
abasicknowledgebase,ChatGPTfailstoan-
swercorrectly66%ofthetime.
| • ExtrinsicHallucination: |     |     | ChatGPTtendsto |     |
| ------------------------- | --- | --- | -------------- | --- |
generatehallucinatedinformationbeyondthe
| givenknowledge. |     | Thisisespeciallyharmful |     |     |
| --------------- | --- | ----------------------- | --- | --- |
inTODasChatGPTwillsometimeshalluci-
| nate someprices |     | forhotel | booking, | or avail- |
| --------------- | --- | -------- | -------- | --------- |
abilityforrestaurants.
| We provide | the | example for | the modular | and |
| ---------- | --- | ----------- | ----------- | --- |
unifiedapproachesforTask-OrientedDialoguein
Table6andTable7,respectively.
696

Task Key TextContent
Givethedialoguestateofthelastutteranceinthefollowingdialogueintheformof’STATE:
Domain-Intent:[Slot,Possiblevalue],...(forexample:STATE:Hotel-Inform:[’area’,’centre’])by
usingthefollowingpre-definedslotsandpossiblevalues:
Intents:Request,Inform,general-thank,general-bye
Domain:hotel,Slots:pricerange,Possiblevalues:[’expensive’,’cheap’,’moderate’]
Domain:hotel,Slots:type,Possiblevalues:[’guesthouse’,’hotel’]
Domain:hotel,Slots:parking,Possiblevalues:[’free’,’no’,’yes’]
Domain:hotel,Slots:bookday,Possiblevalues:[’monday’,’tuesday’,’wednesday’,’thursday’,
’friday’,’saturday’,’sunday’]
Domain:hotel,Slots:bookpeople,Possiblevalues:[’1’,’2’,’3’,’4’,’5’,’6’,’7’,’8’]
Domain:hotel,Slots:bookstay,Possiblevalues:[’1’,’2’,’3’,’4’,’5’,’6’,’7’,’8’]
Domain:hotel,Slots:stars,Possiblevalues:[’0’,’1’,’2’,’3’,’4’,’5’]
Domain:hotel,Slots:internet,Possiblevalues:[’free’,’no’,’yes’]
Domain:hotel,Slots:name,Possiblevalues:[]
Domain:hotel,Slots:area,Possiblevalues:[’centre’,’east’,’north’,’south’,’west’]
Domain:hotel,Slots:address,Possiblevalues:[?]
Prompt Domain:hotel,Slots:phone,Possiblevalues:[?]
Domain:hotel,Slots:postcode,Possiblevalues:[?]
Domain:hotel,Slots:ref,Possiblevalues:[?]
DialogueState
Tracking
USER:Ineedafivestartshotelclosetoamallandmainrestaurants.Thehotelshouldincludefree
wifiintheroom.
STATE:’Hotel-Inform’:[[’internet’,’yes’],[’stars’,’5’]]
SYSTEM:I’msorry,butthereareno5-starhotelsanywhereinCambridge. Wouldyouliketo
broadenyourcriteria?
USER:Howaboutsomethingwith4starsandsomethingexpensive.
STATE:’Hotel-Inform’:[[’pricerange’,’expensive’],[’stars’,’4’]]
SYSTEM:Ihave2optionsforyou-TheHuntingdonMarriottonthewestside,andtheUniversity
Armsinthecenter.Areyouinterestedinoneofthese?
USER:Maybe.Iseitheronea4starhotel?Ifso,I’dliketobookaroomfor4nights.
STATE:’Hotel-Inform’:[[’bookstay’,’4’],[’stars’,’4’]]
SYSTEM:Bothare4stars.Howmanydayswouldyoubestaying,andhowmanypeoplearein
yourparty?Icanseeifsomethingisavailable.
USER:Ineedareservationfor4nightsstartingSaturday.
Gold STATE:’Hotel-Inform’:[[’bookday’,’saturday’],[’stars’,’4’]]
ChatGPT
STATE:’Hotel-Inform’:[[’bookday’,’saturday’],[’bookstay’,’4’],[’stars’,’4’]]
Generation
Continuethedialogueasatask-orienteddialoguesystemcalledSYSTEM.TheanswerofSYSTEM
shouldfollowtheACTIONprovidednextwhileansweringtheUSER’slastutterance:
ACTION:’Restaurant-Inform’:[[’phone’,’01223316074’],[’pricerange’,’cheap’]]
USER:Whereisa4starhotellocatedinNorthCambridge?
Prompt
SYSTEM:Ihaveseveraloptions,almostallofwhicharemoderateguesthouses. Idohaveone
cheapone,too.Wouldyouliketobookaroom?
Response
USER:Sure,thatcouldbenice
Generation
SYSTEM:OK,howmanyareinyourparty,whatdaywillyouarrive,andhowmanynightswill
usingActions
youbestaying?
USER:Iactuallydon’tneedreservationsIjustneedthephonenumber,pricerange.
Gold SYSTEM:AsImentioneditischeapandthephonenumberis01223316074.
ChatGPT SYSTEM:Thephonenumberforthe4-starhotellocatedinNorthCambridgeis01223316074and
Generation itisinthecheappricerange.
Table 6: Examples of modular Task-Oriented Dialogue using ChatGPT: dialogue state tracking and response
generation
697

| Task | Key | TextContent       |           |                  |                           |                  |
| ---- | --- | ----------------- | --------- | ---------------- | ------------------------- | ---------------- |
|      |     | Use the following | knowledge | base to complete | the task of “recommending | a restaurant” by |
continuingtheconversationasatask-orienteddialoguesystem:
Restaurant:MamaJulia,Food:French,Price:Expensive,Location:7thstreet,Rating:5
Restaurant:PapaJohn,Food:Italian,Price:Moderate,Location:3rdstreet,Rating:4
Restaurant:TheCrossroad,Food:Morocco,Price:Moderate,Location:Downtown,Rating:2
Restaurant:TacosCity,Food:Mexian,Price:Cheap,Location:Center,Rating:1
Prompt
Restaurant:GoldenRiceBowl,Food:Chinese,Price:Cheap,Location:3rddistrict,Rating:3
Restaurant:VeggieGarden,Food:Chinese,Price:Expensive,Location:TownHall,Rating:4
Restaurant:PizzaHouse,Food:Italian,Price:Moderate,Location:3rdstreet,Rating:2
Restaurant:ThePalace,Food:Vietnamese,Price:Expensive,Location:HotelGrandview,Rating:
5
Hi,I’mlookingforarestaurant
|     | ChatGPT | Sure,whattypeoffoodareyouinthemoodfor?             |     |     |     |     |
| --- | ------- | -------------------------------------------------- | --- | --- | --- | --- |
|     | Prompt  | Ionlywantrestaurantsrated3orhigher.Anysuggestions? |     |     |     |     |
Multi-turn Herearesomerestaurantsthathavearatingof3orhigher: MamaJulia(French,Expensive,5
unifiedapproach rating),PapaJohn(Italian,Moderate,4rating),GoldenRiceBowl(Chinese,Cheap,3rating),
ChatGPT VeggieGarden(Chinese,Expensive,4rating),andThePalace(Vietnamese,Expensive,5rating).
Whichonewouldyouliketoknowmoreabout?
|     | Prompt  | WhatfooddoesThePalaceserve?               |     |     |     |     |
| --- | ------- | ----------------------------------------- | --- | --- | --- | --- |
|     | ChatGPT | ThePalaceservesVietnamesecuisine.         |     |     |     |     |
|     | Prompt  | IsTaxosCityexpensivetoeatat?              |     |     |     |     |
|     | ChatGPT | TacosCityisconsideredascheaprestaurant.   |     |     |     |     |
|     | Prompt  | IwanttoeatItalianfood,anyrecommendations? |     |     |     |     |
Basedontheinformationprovidedintheknowledgebase,IwouldrecommendPapaJohnand
PizzaHouseforItalianfood.PapaJohnisrated4outof5andisclassifiedas“Moderate”interms
ChatGPT
ofprice,whilePizzaHouseisrated2outof5andisalsoclassifiedas“Moderate”.PapaJohnis
locatedon3rdstreet,whilePizzaHouseislocatedon3rdstreetaswell.
|     | Prompt | DidyouforgetIonlywantedrestaurantsrated3orhigher?     |     |     |                         |     |
| --- | ------ | ----------------------------------------------------- | --- | --- | ----------------------- | --- |
|     |        | Iapologize,Imusthavemisunderstoodyourpreviousrequest. |     |     | Basedontheknowledgebase |     |
ChatGPT provided,TheonlyItalianrestaurantthatisrated3orhigherisPapaJohnwhichisrated4outof5
andislocatedon3rdstreet.Itisclassifiedas“Moderate”intermsofprice.
|     | Prompt | Greatthanksforyourhelp. |     |     |     |     |
| --- | ------ | ----------------------- | --- | --- | --- | --- |
You’rewelcome!IhopeyouenjoyyourmealatPapaJohn.Ifyouhaveanyotherquestionsorneed
ChatGPT
furtherassistance,feelfreetoask.
Table7: Exampleofmulti-turnunifiedapproachforTask-OrientedDialogueusingChatGPT
|     | ChatGPT |     | InstructGPT |     | text-davinci-003 |     |
| --- | ------- | --- | ----------- | --- | ---------------- | --- |
The language of the text appears to be a Thelanguageofthetextisthe ThetextiswritteninBuginese.
| variant of | the Bugis language | spoken | in Sasaklanguage,spokeninLom- |     |     |     |
| ---------- | ------------------ | ------ | ----------------------------- | --- | --- | --- |
| Indonesia. |                    |        | bok,Indonesia.                |     |     |     |
Iamsorry,Idonotrecognizethelanguage The language of the text is ThetextisintheBalineselan-
| ofthetext. |     |     | KoyukonAthabascan. |     | guage. |     |
| ---------- | --- | --- | ------------------ | --- | ------ | --- |
The language of the text appears to be a The language of the text is In- The language of the text is In-
| dialectoftheIndonesianlanguage. |     |     | donesian. |     | donesian. |     |
| ------------------------------- | --- | --- | --------- | --- | --------- | --- |
Table8: ExampleofBugineselanguageidentificationresponsefromChatGPT,InstructGPT,andtext-davinci-003.
698

|          |     |           |           |     | Language |     | Language |     | SAAcc. |     | LIDAcc. |     |     |
| -------- | --- | --------- | --------- | --- | -------- | --- | -------- | --- | ------ | --- | ------- | --- | --- |
| Language |     | #Speakers | CCSize(%) |     |          |     |          |     |        |     |         |     |     |
Category
|                 |     |        |        |     |     |     | English    |     |     | 84% |     | 100% |     |
| --------------- | --- | ------ | ------ | --- | --- | --- | ---------- | --- | --- | --- | --- | ---- | --- |
| English(eng)    |     | 1.452B | 46.320 |     | HRL |     |            |     |     |     |     |      |     |
| Chinese(zho)    |     | 1.118B | 4.837  |     | HRL |     | Indonesian |     |     | 80% |     | 100% |     |
| French(fra)     |     | 235M   | 4.604  |     | HRL |     |            |     |     |     |     |      |     |
|                 |     |        |        |     |     |     | Javanese   |     |     | 78% |     | 0%   |     |
| Indonesian(ind) |     | 199M   | 0.781  |     | MRL |     |            |     |     |     |     |      |     |
|                 |     |        |        |     |     |     | Buginese   |     |     | 56% |     | 12%  |     |
| Korean(kor)     |     | 81.7M  | 0.679  |     | MRL |     |            |     |     |     |     |      |     |
| Javanese(jav)   |     | 68.3M  | 0.002  |     | LRL |     |            |     |     |     |     |      |     |
| Sundanese(sun)  |     | 32.4M  | 0.001  |     | LRL |     |            |     |     |     |     |      |     |
Table10:AccuracyofChatGPTonSentimentAnalysis
| Buginese(bug) |     | 5M  | 0.000 |     | X-LRL |     |     |     |     |     |     |     |     |
| ------------- | --- | --- | ----- | --- | ----- | --- | --- | --- | --- | --- | --- | --- | --- |
(SA)andLanguageIdentification(LID)tasks.
| Table 9: | The | statistics | of languages | used | in our lan- |     |     |     |     |     |     |     |     |
| -------- | --- | ---------- | ------------ | ---- | ----------- | --- | --- | --- | --- | --- | --- | --- | --- |
guagedisparityexperiment.HRL,MRL,LRL,X-LRL
ismuchinferiortotheotherlanguageswithLatin
denotehigh-,medium-,low-,extremelylow-resourced
|     |     |     |     |     |     | scripts,i.e.,FrenchorIndonesian. |     |     |     |     | Similarly,prior |     |     |
| --- | --- | --- | --- | --- | --- | -------------------------------- | --- | --- | --- | --- | --------------- | --- | --- |
languagerespectively.
worksfocusingontransliteration(ChauandSmith,
|     |     |     |     |     |     | 2021; | Muller | et  | al., 2021) | have | shown | the | effec- |
| --- | --- | --- | --- | --- | --- | ----- | ------ | --- | ---------- | ---- | ----- | --- | ------ |
D ChatGPTonMultilinguality tivenessofutilizingLatinscriptsoverotherscripts,
e.g.,Cyrillic,Georgian,Arabic,etc,especiallyfor
| We present | the   | statistics    | of language |     | under study |                        |     |     |     |                           |     |     |     |
| ---------- | ----- | ------------- | ----------- | --- | ----------- | ---------------------- | --- | --- | --- | ------------------------- | --- | --- | --- |
|            |       |               |             |     |             | low-resourcelanguages. |     |     |     | Interestingly,thisproblem |     |     |     |
| in Table   | 9. In | the following | section,    |     | we provide  |                        |     |     |     |                           |     |     |     |
ofusingnon-Latinscriptsislessseverefortrans-
theinsightsthatwefindduringourexperimentin
lationfromChineseandKoreantoEnglish,which
exploringmultilingualcapabilityofChatGPT.
suggeststhatChatGPTcanbetterneutralizetheef-
fectofnon-Latinscriptsassourcelanguages(Wan,
ChatGPTunderstandsLRLsentencesbutfails
toidentifytheirlanguage AsshowninTable10, 2022),butitstilllackstheabilitytogeneratenon-
Latinscriptlanguages.
ChatGPTcorrectlyclassifiesthelanguagesforEn-
| glishandIndonesian100%ofthetime. |     |     |     |     | Whilefor |     |                |     |     |                 |     |     |     |
| -------------------------------- | --- | --- | --- | --- | -------- | --- | -------------- | --- | --- | --------------- | --- | --- | --- |
|                                  |     |     |     |     |          | E   | Multimodality: |     |     | FlagDrawingTask |     |     |     |
thelanguageidentificationforJaveneseandBug-
inese, ChatGPT either misclassifies the samples TaskFormulation Weuniformlycollect50na-
as other languages or is unable to determine the tional flags from different continents and con-
language. Nevertheless,ChatGPTperformanceon ducttheflag-drawingtaskonChatGPT.Theflag-
thesentimentanalysisinJavaneseisonlyslightly drawingtaskcontainsthreesteps:
lowercomparedtoEnglishandIndonesianwhich
1. AskChatGPTtoillustratetheappearanceof
suggeststhatChatGPTcanunderstandtheseman-
ticmeaningofsentencesinlow-resourcelanguages theflagusingtheprompt“Describe how the
|     |     |     |     |     |     |     | <NATION> | flag | looks |     | like”. |     |     |
| --- | --- | --- | --- | --- | --- | --- | -------- | ---- | ----- | --- | ------ | --- | --- |
withouthavingtheknowledgetoidentifythelan-
| guage itself. |     | This limitation | of  | language | identi- |     |     |     |     |     |     |     |     |
| ------------- | --- | --------------- | --- | -------- | ------- | --- | --- | --- | --- | --- | --- | --- | --- |
2. Basedonthedescription,askChatGPTtogen-
| fication | in LMs | aligns | with the | result | from BIG- |     |     |     |     |     |     |     |     |
| -------- | ------ | ------ | -------- | ------ | --------- | --- | --- | --- | --- | --- | --- | --- | --- |
eratetheSVGcodeofthatflagbyprompting
bench(Srivastavaetal.,2022).
|     |     |     |     |     |     |     | “Generate |      | a code | snippet  |     | to represent |     |
| --- | --- | --- | --- | --- | --- | --- | --------- | ---- | ------ | -------- | --- | ------------ | --- |
|     |     |     |     |     |     |     | that      | flag | in SVG | format”. |     |              |     |
ChatGPTdisplaysbetterhuman-preferredre-
| sponses | AsshowninTable8,ChatGPTletsthe |     |     |     |     |     |           |           |       |     |          |         |     |
| ------- | ------------------------------ | --- | --- | --- | --- | --- | --------- | --------- | ----- | --- | -------- | ------- | --- |
|         |                                |     |     |     |     |     | 3. If the | generated | image |     | contains | errors, | we  |
userknowthatitspredictionisuncertainwhenit
iterativelyaskChatGPTtofixthem.
doesnotcompletelyunderstandthelanguageand
| also provides |     | broader | information | regarding | the |                                        |     |     |     |     |     |     |        |
| ------------- | --- | ------- | ----------- | --------- | --- | -------------------------------------- | --- | --- | --- | --- | --- | --- | ------ |
|               |     |         |             |           |     | Therearefourtypesofevaluationcriteria: |     |     |     |     |     |     | 1)lay- |
language,suchaslocationandtribeofwhichthe out2)color3)missingcomponents4)shape/size.
predicted language is spoken. This fact provides Ineachroundoffixing,weaskChatGPTtorevise
evidenceregardingthebenefitofusingtheRLHF only one type of error with the prompt “<ERROR
approach compared to other training approaches DESCRIPTION>. Revise the image”. We ter-
foraligningLLMswithhumanpreferences. minate the conversation once the generated flag
|         |             |     |           |     |              | becomes |     | perfect | or we | have | already | passed | two |
| ------- | ----------- | --- | --------- | --- | ------------ | ------- | --- | ------- | ----- | ---- | ------- | ------ | --- |
| ChatGPT | understands |     | non-Latin |     | scripts bet- |         |     |         |       |      |         |        |     |
roundsoffixing.
| ter than | it can | generate | them | Despite | being |     |     |     |     |     |     |     |     |
| -------- | ------ | -------- | ---- | ------- | ----- | --- | --- | --- | --- | --- | --- | --- | --- |
high-resourceandmedium-resourcelanguages,the Evaluation Thegeneratedflagimagesareeval-
translation from English to Chinese and Korean uated by the aforementioned four error types as
699

Figure4: Completeresultsoftheflagdrawingtask. Multi-turnrefinementallowsChatGPTtogenerateamore
similarimagetothegroundtruthimage.
criteria. Wefurtherassesstheimagequalitywith F.1 LogicalReasoning
fivegrades,A∼E,whichindicatezerotofour(or
Inductiveanddeductivearecategorizedby“ade-
| above)errors. | Weassigngradestoeachroundso |     |     |     |     |
| ------------- | --------------------------- | --- | --- | --- | --- |
greetowhichthepremisesupportstheconclusion”
| that we | can assess the number | of improvements |     |     |     |
| ------- | --------------------- | --------------- | --- | --- | --- |
basedonlogicandphilosophy(Qiaoetal.,2022;
| and degradation       | through conversational | interac-          |                                   |                           |              |
| --------------------- | ---------------------- | ----------------- | --------------------------------- | ------------------------- | ------------ |
|                       |                        |                   | Rogersetal.,2022;Hawthorne,2021). |                           | Inductive    |
| tions (post-editing). | The full               | results are shown |                                   |                           |              |
|                       |                        |                   | reasoning                         | is based on “observations | or evidence” |
inFigure4.
whiledeductiveisbasedon“truthofthepremises”
|     |     |     | (i.e., necessarily | true inference) | (Douven, 2017). |
| --- | --- | --- | ------------------ | --------------- | --------------- |
Anotherwaytocategorizeisbasedonthe“direc-
tionofreasoning”–deductiveisfrompremiseto
F DetailsforReasoningEvaluations
conclusionwhileabductiveisfromconclusionto
themostprobablepremisethatsupportstheconclu-
sion(Walton,2014).
Table11showsthecategoriesofreasoningthatare
evaluated in this paper as well as corresponding Inductiveanddeductivereasoningarecommon
datasets. The following section introduces each formsoflogicalreasoningthatarecategorizedby
ofthecategoriesanddetailedexperimentalsetup “adegreetowhichthepremisesupportstheconclu-
and/oranalysis. sion” based on logic and philosophy (Qiao et al.,
700

| Categories |                                 | Dataset |     |             | DeductiveReasoningTasks |             |     |                |
| ---------- | ------------------------------- | ------- | --- | ----------- | ----------------------- | ----------- | --- | -------------- |
|            | EntailmentBank(Dalvietal.,2021) |         |     |             |                         | bAbI-task15 |     |                |
| Deductive  |                                 |         |     | bAbI-task15 |                         |             |     | EntailmentBank |
|            | bAbI(task15)(Westonetal.,2016b) |         |     |             | (promptengineered)      |             |     |                |
|            | CLUTRR(Sinhaetal.,2019)         |         |     | 19/30       |                         | 28/30       |     | 28/30          |
Inductive
bAbI(task16)(Westonetal.,2016b)
InductiveReasoningTasks
| Abductive | αNLI | (Bhagavatulaetal.,2020) |     |     |     |     |     |     |
| --------- | ---- | ----------------------- | --- | --- | --- | --- | --- | --- |
bAbI-task16
| Temporal | Timedial(Qinetal.,2021) |     |     | bAbI-task16 |     |     |     | CLUTRR |
| -------- | ----------------------- | --- | --- | ----------- | --- | --- | --- | ------ |
(promptengineered)
SpartQA(Mirzaeeetal.,2021)
| Spatial |     |     |     | 0/30 |     | 20/30 |     | 13/30 |
| ------- | --- | --- | --- | ---- | --- | ----- | --- | ----- |
StepGame(Shietal.,2022a)
Mathematical Math(Saxtonetal.,2019) Table 12: Inductive vs. Deductive Reasoning. Chat-
CommonsenseQA(Talmoretal.,2018) GPT performs better deduction rather than induction.
Commonsense PiQA(Bisketal.,2020) EngineeringtheprompttoexplicitlyaskChatGPTtodo
reasonableinferenceimprovesitsreasoningcapability.
Pep-3k(Wangetal.,2018b)
Thescoresareinaccuracyovertestedsamples.
| Causal    | E-Care(Duetal.,2022)     |     |     |     |     |     |     |     |
| --------- | ------------------------ | --- | --- | --- | --- | --- | --- | --- |
| Multi-hop | HotpotQA(Yangetal.,2018) |     |     |     |     |     |     |     |
Analogical Letterstringanalogies(Webbetal.,2022b) therearelikelyreal-worldtasksthatitwillfailon
tooiftheyrequiresimilarreasoningmechanisms.
| Table 11: | Reasoning | categories | and corresponding |     |     |     |     |     |
| --------- | --------- | ---------- | ----------------- | --- | --- | --- | --- | --- |
Consequently,theadvanced-leveltasksarethereto
datasetsusedtoevaluateChatGPTinthiswork.
probethosecapabilitiesinreal-worldtaskswhere
thenoisesarepresent,andsolvingthemrequiresa
2022;Rogersetal.,2022;Hawthorne,2021). De- moresystematicgeneralization. Additionally,we
ductivereasoninginvolvesprocessesofdrivingspe- choosetasksthatdonotrequireoraredependent
cificconclusionsbasedonmoregeneralpremises. on external knowledge and the solution could be
Onthecontraryinductivereasoninginvolvesspe- onlyderivedbypremisestofocusondissectingthe
cificobservationofpatterns,processingthemonin- capabilityofeachreasoningmechanism.
creasinglyabstractcyclesofhypothetico-deductive
reasoningtodrawamoregeneralconclusion(Law- Results&DetailedAnalysis ChatGPTanswers
|            |                                  |                 |               | “It is not                       | specified   | what | <attribute> | <entity> is.” |
| ---------- | -------------------------------- | --------------- | ------------- | -------------------------------- | ----------- | ---- | ----------- | ------------- |
| son,2005). | Comparingthetwotypesofreasoning, |                 |               |                                  |             |      |             |               |
|            |                                  |                 |               | for most                         | of the time | when | it was      | asked a ques- |
| deduction  | requires                         | less “guessing” | from the per- |                                  |             |      |             |               |
|            |                                  |                 |               | tionrequiringinductivereasoning. |             |      |             | However,when  |
spectiveofChatGPT,asinductionrequiresfiguring
outrules(Rogersetal.,2022). Theformercanbe ChatGPT is explicitly asked for reasonable infer-
encewithaprompt“Basedonthegivenfacts,doa
viewedastop-downwhilethelatterisbottom-up.
reasonableinferenceonthisquestionusinginduc-
| F.1.1 Deductivevs. |     | InductiveReasoning |     |     |     |     |     |     |
| ------------------ | --- | ------------------ | --- | --- | --- | --- | --- | --- |
tivereasoning:”,itsabilityforinductivereasoning
Deductive reasoning involves processes of driv- increases. Yet, it is still not as good as in deduc-
ing specific conclusions based on more general tion as the same prompt engineering also helps
premises. Onthecontrary,inductivereasoningin- increasesitsabilityfordeductivereasoning.
volvesspecificobservationofpatterns,processing
WecouldderivesimilarinsightasChatGPTonly
themonincreasinglyabstractcyclesofhypothetico- correctly answered for half of the time while it
deductivereasoningtodrawamoregeneralconclu- couldmakeinferencesdeductivelywellfor90%of
sion(Lawson,2005). Comparingthetwotypesof the time. CLUTRR (Sinha et al., 2019) requires
reasoning,deductionrequiresless“guessing”from inductiononextractingrelationsbetweenentities,
theperspectiveofChatGPT,asinductionrequires and in the ChatGPT responses, it often asks for
figuring out rules (Rogers et al., 2022). The for- more information to make inferences. An inter-
mercanbeviewedastop-downwhilethelatteris estingfindingalongwithCLUTRRwasthatChat-
| bottom-up. |     |     |     | GPTcan’tdifferentiatesonandgrandsonbutcan |     |     |     |     |
| ---------- | --- | --- | --- | ----------------------------------------- | --- | --- | --- | --- |
WeexploreChatGPT’sabilityofinductiveand differentiatedaughterandgranddaughterwhenit
deductivereasoningintwodifferentlevels: 1)basic induces the logical rules governing kinship rela-
and2)advanced. Basic-leveltasksaretheprerequi- tionships. WeshowallperformancesinTable12
sitestoprobereasoning. Whilesolvingthesetasks and some of the prompting samples in Table 13.
doesnot necessarilyindicate fullreasoningcapa- We follow (Qiao et al., 2022) categorization on
bility,ifChatGPTfailsonanyofthesetasks,then thedeductiveandinductivereasoningdatasets,but
701

| Task |     |     | Prompt |     | ChatGPTanswer | Gold | T/F |
| ---- | --- | --- | ------ | --- | ------------- | ---- | --- |
DeductiveReasoningTasks
1Wolvesareafraidofmice.
2Sheepareafraidofmice.
3Winonaisasheep.
4Miceareafraidofcats.
| bAbI(task15) | 5Catsareafraidofwolves. |     |     |     | Winona, being    | a mouse | T   |
| ------------ | ----------------------- | --- | --- | --- | ---------------- | ------- | --- |
|              | 6Jessicaisamouse.       |     |     |     | sheep,isafraidof |         |     |
|              | 7Emilyisacat.           |     |     |     | mice.            |         |     |
8Gertrudeisawolf.
10Whatiswinonaafraidof?
Givenfacts:Wolvesareafraidofmice.Sheepareafraidofmice.Winonaisa
|              | sheep.Miceareafraidofcats.Catsareafraidofwolves.Jessicaisamouse. |     |     |     | Basedonthegiven |       |     |
| ------------ | ---------------------------------------------------------------- | --- | --- | --- | --------------- | ----- | --- |
| bAbI(task15) | Emilyisacat.Gertrudeisawolf.                                     |     |     |     | facts,itcanbe   |       |     |
| (prompt      |                                                                  |     |     |     | inferredthat    | mouse | T   |
engineered) Basedonthegivenfactsabove,doareasonableinferenceonthisquestionusing Winonaisafraidof
|     | deductivereasoning: |     |     |     | mice. |     |     |
| --- | ------------------- | --- | --- | --- | ----- | --- | --- |
Whatiswinonaafraidof?
|     | earthisakindofplanet.aplanetisakindofcelestialobject/celestialbody. |     |     |     | Earthisaplanet |     |     |
| --- | ------------------------------------------------------------------- | --- | --- | --- | -------------- | --- | --- |
Entailment-
earthislocatedinthemilkywaygalaxy.Whichobjectisaplanetfoundinthe locatedinthe Earth T
Bank
|     | MilkyWayGalaxy? |     |     |     | MilkyWaygalaxy. |     |     |
| --- | --------------- | --- | --- | --- | --------------- | --- | --- |
InductiveReasoningTasks
1Bernhardisaswan.
2Gregisafrog.
3Brianisaswan.
|              | 4Juliusisalion.  |     |     |     | Itisnotspecified |        |     |
| ------------ | ---------------- | --- | --- | --- | ---------------- | ------ | --- |
|              | 5Gregisgray.     |     |     |     | inthegiven       |        |     |
| bAbI(task16) |                  |     |     |     |                  | yellow | F   |
|              | 6Juliusisyellow. |     |     |     | informationwhat  |        |     |
|              | 7Lilyisalion.    |     |     |     | colorBernhardis. |        |     |
8Lilyisgreen.
9Brianisyellow.
10WhatcolorisBernhard?
Givenfacts:Bernhardisaswan.Gregisafrog.Brianisaswan.Juliusisalion.
|     | Gregisgray.Juliusisyellow.Lilyisalion.Lilyisgreen.Brianisyellow. |     |     |     | Basedonthegiven |     |     |
| --- | ---------------------------------------------------------------- | --- | --- | --- | --------------- | --- | --- |
facts,itcanbe
bAbI(task16)
|             | Themostrecentfactisthecorrectfact.                                  |     |     |     | inferredthat      |        |     |
| ----------- | ------------------------------------------------------------------- | --- | --- | --- | ----------------- | ------ | --- |
| (prompt     |                                                                     |     |     |     |                   | yellow | T   |
| engineered) |                                                                     |     |     |     | Bernhardisyellow, |        |     |
|             | Basedonthegivenfactsabove,doareasonableinferenceonthisquestionusing |     |     |     | asBrianisalso     |        |     |
|             | inductivereasoning:                                                 |     |     |     | statedtobeyellow. |        |     |
WhatcolorisBernhard?
|     | [Jason]andhiswife[Gabrielle]wenttothebeachtowatchthefireworksonthe |     |     |     | Almaisthe |     |     |
| --- | ------------------------------------------------------------------ | --- | --- | --- | --------- | --- | --- |
4thofJuly.[Jason]andhisdaughter[Alma]tookadayoffschooltogotothe daughterofJason daughter T
|     | zoo...WhoisAlmatoGabrielle? |     |     |     | andGabrielle. |     |     |
| --- | --------------------------- | --- | --- | --- | ------------- | --- | --- |
CLUTRR
|     | [Jason]tookhisgrandson[Donald]fishing.[Russell]enjoysgoingfishingwith |     |     |     | Russellisthe    |          |     |
| --- | --------------------------------------------------------------------- | --- | --- | --- | --------------- | -------- | --- |
|     |                                                                       |     |     |     |                 | grandson | F   |
|     | hisbrother.Hisnameis[Donald]...WhoisRusselltoJason?                   |     |     |     | brotherofJason. |          |     |
Table13: Promptingsamplesondeductiveandinductivereasoningtasks. ChatGPTisperformingbetterdeduction
ratherthaninduction. Onbothtypesofreasoning,whenChatGPTisexplicitlyaskedtodoreasonableinferences,its
abilityforreasoningincreases. Additionally,italsomakesfrequentmistakesregardingthegrandson’skinship.
StepGame(Basic)BreakdownAnalaysis
|     | Result |     | Example | ChatGPTanswer |     | Gold | T/F |
| --- | ------ | --- | ------- | ------------- | --- | ---- | --- |
Clock-position 5/20 GisatY’s6o’clock. Whatistherelationofthe TheagentYistotherightofthe Above F
|     |     | agentYtotheagentG? |     | agentG. |     |     |     |
| --- | --- | ------------------ | --- | ------- | --- | --- | --- |
BasicCardinal 17/20 DandKareparallel,andDisunderK.Whatisthe ThespatialrelationoftheagentK Above T
|     |     | relationoftheagentKtotheagentD? |     | totheagentDisthatKisabove |     |     |     |
| --- | --- | ------------------------------- | --- | ------------------------- | --- | --- | --- |
D.
Diagonal 11/20 WpresentslowerlefttoI.Whatistherelationof TherelationoftheagentItothe Upper- F
|     |     | theagentItotheagentW? |     | agentWislower-left. |     | Right |     |
| --- | --- | --------------------- | --- | ------------------- | --- | ----- | --- |
Table14: Aprovidedillustrationtohelpthereaderstounderstandeachcomparisonbetweenthecategories(not
the actual prompts). We provide the options to ChatGPT as: Choose from: left, right, above, below,
| lower-left, | lower-right, | upper-left, | upper-right. |     |     |     |     |
| ----------- | ------------ | ----------- | ------------ | --- | --- | --- | --- |
702

weonlyusetheQApartofEntailmentBank,that SpatialReasoningTasks
| the authors | took            | from   | ARC dataset        |          | (Clark      | et al., |     |          |     |       |            |     |     |
| ----------- | --------------- | ------ | ------------------ | -------- | ----------- | ------- | --- | -------- | --- | ----- | ---------- | --- | --- |
|             |                 |        |                    |          |             |         |     | Dataset  |     | Total | Basic Hard |     |     |
| 2018),      | as we           | aim to | test for reasoning |          | capability. |         |     |          |     |       |            |     |     |
|             |                 |        |                    |          |             |         |     | StepGame |     | 26/60 | 19/30 7/30 |     |     |
| Regarding   | EntailmentBank, |        |                    | it might | trigger     | the     |     |          |     |       |            |     |     |
|             |                 |        |                    |          |             |         |     | SpartQA  |     | 28/64 | 20/32 8/32 |     |     |
universe-relatedknowledgeoutofChatGPT,which
couldhelpthemodeltoderivethecorrectanswer,
Table15:SpatialreasoningabilityofChatGPT.Overall,
althoughthe testset isdesigned totest deductive ChatGPTfallsshortofthetask.
| reasoning | skills. | One | of the | future | explorations |     |     |     |     |     |     |     |     |
| --------- | ------- | --- | ------ | ------ | ------------ | --- | --- | --- | --- | --- | --- | --- | --- |
wouldbewithcheckingtherationaleofChatGPT
|     |     |     |     |     |     |     | thetaskintheBIG-benchbenchmark |     |     |     |     | (Srivastava |     |
| --- | --- | --- | --- | --- | --- | --- | ------------------------------ | --- | --- | --- | --- | ----------- | --- |
asafollow-upquestion.
etal.,2022),whichismultiple-choice(singlecor-
F.1.2 AbductiveReasoning
rectanswer),Overall,ChatGPTcorrectlyanswers
86.67%ofthetime(26/30),suggestingthatithasa
| Abductive | reasoning |     | is the inference |     | to the | most |     |     |     |     |     |     |     |
| --------- | --------- | --- | ---------------- | --- | ------ | ---- | --- | --- | --- | --- | --- | --- | --- |
plausible explanation given observations. For in- decenttemporalreasoningability. Also,compared
stance, “if Jenny finds her house in a mess when toChinchillaandGopherwhichhavetheaccuracy
she returns from work, and remembers that she of68.8%and50.9%respectively,ChatGPTshows
apromisingimprovementforLLMsinthataspect.
| left a window |     | open, | she can | hypothesize |     | that a |     |     |     |     |     |     |     |
| ------------- | --- | ----- | ------- | ----------- | --- | ------ | --- | --- | --- | --- | --- | --- | --- |
thiefbrokeintoherhouseandcausedthemess”4.
|     |     |     |     |     |     |     | SpatialReasoning |     |     | Spatialreasoningisusingan |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | ---------------- | --- | --- | ------------------------- | --- | --- | --- |
WetestChatGPT’slanguage-basedabductiverea-
understandingofspatialrelationsamongdifferent
soningabilitywith30samplesfromαNLIdataset
(Bhagavatula et al., 2020), which requires the objectsandspaces. Forspatialreasoning, weuti-
model to select the most plausible explanation lizetwoexistingdatasets: SpartQA(Mirzaeeetal.,
|           |             |     |       |        |          |       | 2021) | and StepGame |     | (Shi | et al., 2022a), |     | which |
| --------- | ----------- | --- | ----- | ------ | -------- | ----- | ----- | ------------ | --- | ---- | --------------- | --- | ----- |
| given the | conclusion. |     | Based | on our | test, it | could |       |              |     |      |                 |     |       |
composeofstory-questionpairsaboutkrelations
achieve86.7%(26outof30)accuracy.
ofk+1(wherekisupto10)entitieswritteninnat-
F.2 Non-textualSemanticReasoning urallanguage. ChatGPTisaskedtoanswerspatial
|                       |           |           |                      |          |            |     | relations                             | between |     | two entities | based | on the  | pro- |
| --------------------- | --------- | --------- | -------------------- | -------- | ---------- | --- | ------------------------------------- | ------- | --- | ------------ | ----- | ------- | ---- |
| Mathematicalreasoning |           |           | Mathematicalcapabil- |          |            |     |                                       |         |     |              |       |         |      |
|                       |           |           |                      |          |            |     | videddescriptionsofdifferententities. |         |     |              |       | ChatGPT |      |
| ities or              | numerical | reasoning |                      | has been | frequently |     |                                       |         |     |              |       |         |      |
mentionedtobelackingforLLMs,notonlyChat- fallsshortofthespatialreasoningtasks,asshown
|                         |     |     |              |     |           |     | inTable15, |     | withoverallsuccessratesof43.33% |     |     |     |     |
| ----------------------- | --- | --- | ------------ | --- | --------- | --- | ---------- | --- | ------------------------------- | --- | --- | --- | --- |
| GPT(Friederetal.,2023). |     |     | Friederetal. |     | testChat- |     |            |     |                                 |     |     |     |     |
forStepGameand43.75%forSpartQA.ChatGPT
GPT’scapabilitywithpubliclyavailabledatasetsas
wellasthehuman-curateddataset,whichconsists could only score 25% on SpartQA (hard), which
|               |     |                               |     |     |     |     | covers                          | multiple | spatial | reasoning | sub-types, |         | and |
| ------------- | --- | ----------------------------- | --- | --- | --- | --- | ------------------------------- | -------- | ------- | --------- | ---------- | ------- | --- |
| of728prompts. |     | ThesharedfindingsforChatGPT’s |     |     |     |     |                                 |          |         |           |            |         |     |
|               |     |                               |     |     |     |     | 23.33%forstepGame(Hard)withk=9. |          |         |           |            | ChatGPT |     |
mathematicalcapabilitiesinclude1)ChatGPTof-
couldnotprovideanyspatialrelationsbutinstead
| ten understands |     | the question |     | but fails | to provide |     |     |     |     |     |     |     |     |
| --------------- | --- | ------------ | --- | --------- | ---------- | --- | --- | --- | --- | --- | --- | --- | --- |
generated“Itisnotspecifiedinthegivendescrip-
correctsolutions;2)itshowsinconsistentpoorper-
|     |     |     |     |     |     |     | tion”. | Evenwiththefine-tunedmodels,asthenum- |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | ------ | ------------------------------------- | --- | --- | --- | --- | --- |
formanceongraduate-leveladvancedmathematics;
berofrelations(k)increasesincontextdescription,
3)ithasagreatabilitytosearchformathematical
objects. 5 WealsotestseparatelyonMATHdataset. performancedrops(Shietal.,2022a).
Notsurprisingly,itcouldonlyscore23.33%(7/30) Tounderstandspatialreasoningabilityatamore
|     |     |     |     |     |     |     | elementary |     | level, | we test with | less | complicated |     |
| --- | --- | --- | --- | --- | --- | --- | ---------- | --- | ------ | ------------ | ---- | ----------- | --- |
fortheMATHdataset(Saxtonetal.,2019),which
|     |     |     |     |     |     |     | examples | from | StepGame |     | which we | refer | to as |
| --- | --- | --- | --- | --- | --- | --- | -------- | ---- | -------- | --- | -------- | ----- | ----- |
testsmathematicalreasoning.
|                   |     |     |                         |     |     |     | StepGame(Basic). |     |     | Itdoesnotinvolvemulti-hop |     |     |     |
| ----------------- | --- | --- | ----------------------- | --- | --- | --- | ---------------- | --- | --- | ------------------------- | --- | --- | --- |
| Temporalreasoning |     |     | Temporalreasoningismen- |     |     |     |                  |     |     |                           |     |     |     |
reasoningbutpurelyspatialrelationbetweentwo
tionedafewtimesintheliteraturebutislesscom- entities. (e.g,“CissittingatthetoppositiontoY.
| monthanothers. |     | Itteststheunderstandingofthe |     |     |     |     |     |     |     |     |     |     |     |
| -------------- | --- | ---------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
WhatistherelationoftheagentYtotheagentC?”).
| time duration |     | of and | the relation | between |     | events. |     |          |       |                   |      |     |        |
| ------------- | --- | ------ | ------------ | ------- | --- | ------- | --- | -------- | ----- | ----------------- | ---- | --- | ------ |
|               |     |        |              |         |     |         | We  | test for | basic | spatial relations | with | 8   | labels |
Forthiscategory,weconductexperimentsonthe from StepGame {left, right, above, below, lower-
datasetTimeDial(Qinetal.,2021),whichsolelyre- left,lower-right,upper-left,upper-right}. Whenwe
| quirestemporalreasoning. |     |     | Wefollowtheformatof |     |     |     |     |     |     |     |     |     |     |
| ------------------------ | --- | --- | ------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
testonStepGame(Basic),ChatGPTscoreshigher
(63.33%).
4AnexampleprovidedbyBhagavatulaetal.(2020).
|     |     |     |     |     |     |     | We  | investigate |     | the errors | that it often | fails | to  |
| --- | --- | --- | --- | --- | --- | --- | --- | ----------- | --- | ---------- | ------------- | ----- | --- |
5Refertodetailedfindingsintheoriginalpaper.
703

CommonsenseReasoningTasks Prompt Pleasejudgeifthispredicateis(likely)
|               |     |     |      |              |     |     | plausible |     | or implausible: |     | “knife | chop |
| ------------- | --- | --- | ---- | ------------ | --- | --- | --------- | --- | --------------- | --- | ------ | ---- |
| CommonsenseQA |     |     | PiQA | Pep-3k(Hard) |     |     |           |     |                 |     |        |      |
rock”
|     | 27/30 |     | 25/30 | 28/30 |     |         |                                    |     |     |     |     |     |
| --- | ----- | --- | ----- | ----- | --- | ------- | ---------------------------------- | --- | --- | --- | --- | --- |
|     |       |     |       |       |     | ChatGPT | Itisimplausiblethataknifecouldchop |     |     |     |     |     |
Table16: CommonsensereasoningabilityofChatGPT. Answer througharock. Knivesaremadetocut
ChatGPT shows good performance of commonsense throughsoftermaterialssuchasfood,pa-
reasoningcapabilityonthethreetestdatawetestiton. per, or wood. Rocks are much harder
|     |     |     |     |     |     |     | than | these | materials | and | a knife | would |
| --- | --- | --- | --- | --- | --- | --- | ---- | ----- | --------- | --- | ------- | ----- |
notbeabletomakeadentinarock,let
| understand |     | clock direction | (e.g., | “W  | is at K’s 3 |     |     |     |     |     |     |     |
| ---------- | --- | --------------- | ------ | --- | ----------- | --- | --- | --- | --- | --- | --- | --- |
alonechopit.
| o’clock”)anddiagonalspatialrelations. |     |     |     |     | Wefurther |     |     |     |     |     |     |     |
| ------------------------------------- | --- | --- | --- | --- | --------- | --- | --- | --- | --- | --- | --- | --- |
analyze the results by breaking down the test ex- Table17:AnexamplefromPep-3k(Wangetal.,2018b)
forcommonsensereasoningofChatGPT.Wemakethe
amplesofStepGame(Basic)intotwocomparisons:
i) types of directions (basic cardinal vs. diago- main answer bold, and highlight the explanation by
greencolor.
nal)andii)waysofspatialdescriptionforcardinal
directions(basiccardinal6
vs. clock-positioncardi-
nal). Wetake20moresamplesforeachcategory
|     |     |     |     |     |     | itontoajar". |     | Weusethevalidationsplitforboth |     |     |     |     |
| --- | --- | --- | --- | --- | --- | ------------ | --- | ------------------------------ | --- | --- | --- | --- |
(basiccardinal,diagonal,clock-positioncardinal)
|     |     |     |     |     |     | of the datasets |     | since | there | are no | labels | provided |
| --- | --- | --- | --- | --- | --- | --------------- | --- | ----- | ----- | ------ | ------ | -------- |
andtestedthemasillustratedinTable14.
|     |     |     |     |     |     | on the | test set | that | we retrieve. |     | We also | further |
| --- | --- | --- | --- | --- | --- | ------ | -------- | ---- | ------------ | --- | ------- | ------- |
probeChatGPTbyevaluatingamorechallenging
• ChatGPTpoorlyinferswithclock-position
commonsensereasoningdatasetinamorecompre-
| description. |     | Althoughitisasimplecardinal |        |       |               |                |     |                               |       |              |     |           |
| ------------ | --- | --------------------------- | ------ | ----- | ------------- | -------------- | --- | ----------------------------- | ----- | ------------ | --- | --------- |
|              |     |                             |        |       |               | hensiveway.    |     | WeusePep-3k(Wangetal.,2018b), |       |              |     |           |
| direction,   |     | ChatGPT                     | could  | only  | correctly an- |                |     |                               |       |              |     |           |
|              |     |                             |        |       |               | which requires |     | the                           | model | to recognize |     | plausible |
| swer         | for | 5 samples                   | (25%), | which | is clearly    |                |     |                               |       |              |     |           |
butpossiblynovelevents,suchas“manswallow
poorerperformanceincomparisontoperfor-
|     |     |     |     |     |     | paintball". | EachinstanceinthePep-3kisans-v-o |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | ----------- | -------------------------------- | --- | --- | --- | --- | --- |
mancewiththebasiccardinaldescription(17
predicate,andthetaskistojudgeifthepredicate
correctanswers).
|     |     |     |     |     |     | isplausibleornot. |     | ButinsteadofevaluatingChat- |     |     |     |     |
| --- | --- | --- | --- | --- | --- | ----------------- | --- | --------------------------- | --- | --- | --- | --- |
• ChatGPT is worse at the diagonal posi- GPT’sperformanceonlybasedonthebinaryjudg-
tion. Itcorrectlyanswersaroundhalfofthe ment,wealsocheckiftheanswercontainsrelevant
time(55%),whichisworsethanbasiccardi- rationales(explanations)thatleadtoitsjudgment.
| nal | points | (85%). | Even | with analysis | from |         |        |          |     |            |     |           |
| --- | ------ | ------ | ---- | ------------- | ---- | ------- | ------ | -------- | --- | ---------- | --- | --------- |
|     |        |        |      |               |      | For the | Pep-3k | samples, |     | we prepend |     | the s-v-o |
StepGame (Hard), among the correct 7 an- predicate with “Please judge if this predicate is
swers, there is only one diagonal direction (likely)plausibleorimplausible:"topromptChat-
thatChatGPTgetscorrectlywhiletheothers
|     |     |     |     |     |     | GPT.WeshowtheresultsinTable16. |     |     |     |     | Aswesee, |     |
| --- | --- | --- | --- | --- | --- | ------------------------------ | --- | --- | --- | --- | -------- | --- |
areallcardinalpoints. Forthoseanswersthat ChatGPTperformsquitewellonthethreedatasets
requirediagonalpoints,ChatGPTonlycould in terms of answer accuracy, which matches our
infercardinalpointsforsomeexamples.
|     |     |     |     |     |     | anticipation. |     | Furthermore, |        | as we | also check      | the |
| --- | --- | --- | --- | --- | --- | ------------- | --- | ------------ | ------ | ----- | --------------- | --- |
|     |     |     |     |     |     | rationales    | in  | ChatGPT’s    | answer |       | when evaluating |     |
F.3 CommonsenseReasoning
|     |     |     |     |     |     | Pep-3k | samples, | we  | can | see that | ChatGPT | does |
| --- | --- | --- | --- | --- | --- | ------ | -------- | --- | --- | -------- | ------- | ---- |
ToevaluateChatGPT’scapabilityoncommonsense quitewellnotonlyintermsofansweraccuracybut
reasoning,wefirsttestitontwowidelyusedbench-
alsoingeneratingreasonablereasoningprocedures
mark datasets CommonsenseQA (Talmor et al., tosupportitsanswer. Weshowaconcreteexample
2018) and PiQA (Bisk et al., 2020). Common- in Table 17. As we can see, ChatGPT’s answer
| senseQA | focuses | on  | general | commonsense | ques- |          |      |      |       |              |     |         |
| ------- | ------- | --- | ------- | ----------- | ----- | -------- | ---- | ---- | ----- | ------------ | --- | ------- |
|         |         |     |         |             |       | explains | well | what | kinds | of materials | are | usually |
tionansweringsuchas“Whereisabusinessrestau-
cutthroughwithknives(i.e.,food,paper,orwood).
rant likely to be located?”, and PiQA is about Then,itreasonswhyrockscannotbechoppedwith
physicalcommonsensereasoning: givenasentence aknifebyexplaining‘rocksaremuchharderthan
suchas“Whenboilingbutter,whenit’sready,you
|     |     |     |     |     |     | thesematerials.’ |     | Whileourfindingsarebasedon |     |     |     |     |
| --- | --- | --- | --- | --- | --- | ---------------- | --- | -------------------------- | --- | --- | --- | --- |
can",thegoalistofillintheblankwithoneoftwo 30samplesfromeachdataset,weseethepotential
answeroptions,“Pouritontoaplate"and“Pour inChatGPT’scommonsensereasoningcapability,
|     |     |     |     |     |     | and further | large-scale |     | investigation |     | is  | worth ex- |
| --- | --- | --- | --- | --- | --- | ----------- | ----------- | --- | ------------- | --- | --- | --------- |
6Thoseofwhichspatialrelationsaredescribedwithex-
ploring.
plicitvocabulary.
704

G DetailsforHallucinationEvaluations
| Causal | Multi-hop |     | Analogical            |     |     |     |     |     |     |     |     |
| ------ | --------- | --- | --------------------- | --- | --- | --- | --- | --- | --- | --- | --- |
| E-CARE | HotpotQA  |     | Letterstringanalogies |     |     |     |     |     |     |     |     |
Thereexisttwocategoriesofhallucination(Jietal.,
24/30 8/30 30/30 2022a). Intrinsichallucinationsthatreferstothe
LLMgenerationthatcontradictsthesource/input
Table18: Resultsforcausal,multi-hop,andanalogical content. Extrinsichallucinationsthatreferstothe
| reasoning. | ChatGPTshowsgoodcausalandanalogical |     |     |     |     |     |     |     |     |     |     |
| ---------- | ----------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
LLMgenerationsthatcannotbeverifiedfromthe
reasoningcapability,butnotonmulti-hopreasoning.
source/inputcontent(i.e.,outputthatcanneitherbe
|     |     |     |     |     |     | supportednorcontradictedbythesource). |     |     |     |     | InTable |
| --- | --- | --- | --- | --- | --- | ------------------------------------- | --- | --- | --- | --- | ------- |
F.4 Causal,Multi-Hop,andAnalogical 19,weshareexamplesofthesehallucinationtypes
| Reasoning |                |        |              |     |         | detected            | from     | different task | explorations. |            | With    |
| --------- | -------------- | ------ | ------------ | --- | ------- | ------------------- | -------- | -------------- | ------------- | ---------- | ------- |
|           |                |        |              |     |         | the setting         | of tasks | we test,       | we often      | find       | extrin- |
| Causal    | Reasoning      | Causal | reasoning    |     | is the  |                     |          |                |               |            |         |
|           |                |        |              |     |         | sic hallucinations, |          | including      | both          | untruthful | and     |
| process   | of identifying | the    | relationship |     | between |                     |          |                |               |            |         |
factualones,acrossvarioustaskssuchasMachine
causes/actionsandeffects/changes(i.e.,causality)
Translation,Questionanswering.
| (Thomason,2018;HuangandChang,2022). |     |     |     |     | We  |                                           |     |     |     |     |     |
| ----------------------------------- | --- | --- | --- | --- | --- | ----------------------------------------- | --- | --- | --- | --- | --- |
|                                     |     |     |     |     |     | Theintrinsichallucinationsarebarelyfound. |     |     |     |     | For |
testChatGPTon30samplesofhuman-annotated
instance,intheabstractivesummarizationtask,in
explainableCAusalREasoningdataset(E-CARE)
whichneuralmodelsusuallysufferfromintrinsic
(Duetal.,2022)anditcouldscore24samplescor-
hallucination,ChatGPT’sgeneratedsummarisation
| rectly (80%). | Note | that | our evaluation |     | is mainly |         |         |               |               |     |       |
| ------------- | ---- | ---- | -------------- | --- | --------- | ------- | ------- | ------------- | ------------- | --- | ----- |
|               |      |      |                |     |           | did not | include | any intrinsic | hallucination |     | exam- |
basedonwhetherthemodelcanmakeajudgment
|     |     |     |     |     |     | ples based | on our | experiments. | It  | rather | shows a |
| --- | --- | --- | --- | --- | --- | ---------- | ------ | ------------ | --- | ------ | ------- |
oncorrectcausesoreffectsinsteadofitsgenerated
factualextrinsichallucination,forinstance,Chat-
explanationofwhythecausationexists.
GPTcouldcorrectlyparaphrase“Britainandfive
othercountries”fromsourceinputinto“P5+1(US,
| Multi-hopReasoning |     |     | Tobeabletoreasonover |     |     |     |     |     |     |     |     |
| ------------------ | --- | --- | -------------------- | --- | --- | --- | --- | --- | --- | --- | --- |
UK,France,China,Russia,andGermany),”which
alargercontext,asystemhastoperformmulti-hop
|     |     |     |     |     |     | isassessedtobefactual. |     | Wecouldalsoobservean |     |     |     |
| --- | --- | --- | --- | --- | --- | ---------------------- | --- | -------------------- | --- | --- | --- |
reasoningovermorethanonepieceofinformation
toarriveattheanswer(Mavietal.,2022). Wetest interestingintrinsichallucinationforourproposed
|           |           |           |     |            |       | multi-modaltask,theflagdrawingtask. |     |     |     |     | ChatGPT |
| --------- | --------- | --------- | --- | ---------- | ----- | ----------------------------------- | --- | --- | --- | --- | ------- |
| ChatGPT’s | multi-hop | reasoning |     | capability | on 30 |                                     |     |     |     |     |         |
isfirstaskedtogenerateadescriptionofhowthe
| samples | of HotpotQA | dataset | (Yang | et  | al., 2018) |     |     |     |     |     |     |
| ------- | ----------- | ------- | ----- | --- | ---------- | --- | --- | --- | --- | --- | --- |
andwefindthatChatGPThasdifficultyperform- flagslookbeforeitisaskedtogeneratecodeforthe
flag. Althoughitgeneratesthecorrectdescription
ingwithsuchcapability,onlyanswering8samples
|            |          |               |     |       |          | as “The | flag of | Mexico consists | of  | three | vertical |
| ---------- | -------- | ------------- | --- | ----- | -------- | ------- | ------- | --------------- | --- | ----- | -------- |
| correctly, | although | the questions |     | posed | are only |         |         |                 |     |       |          |
bands[...]”,thefinaldrawing(SVGcode)consists
2-hops. ItisworthnotingthatChatGPToftentimes
| generatestheanswerinashortpassageofexplana- |     |     |     |     |     | ofhorizontalbands. |     |     |     |     |     |
| ------------------------------------------- | --- | --- | --- | --- | --- | ------------------ | --- | --- | --- | --- | --- |
However,extrinsichallucinationsoftenhappen,
tions,thusweevaluatemanuallyeachoftheChat-
|                                 |     |     |     |     |            | includingbothuntruthfulandfactualones. |     |     |     |     | Inthe |
| ------------------------------- | --- | --- | --- | --- | ---------- | -------------------------------------- | --- | --- | --- | --- | ----- |
| GPTresponsestocheckitsaccuracy. |     |     |     |     | Thisaligns |                                        |     |     |     |     |       |
withthefindingsthatLLMsarealsolimitedinsev- QA task, we often find extrinsic hallucination to
eralways,andfailtoproduceaccuratepredictions benon-factualwhichharmsthefinalperformance.
|              |           |               |     |         |      | For instance, | in  | the question | of asking | for | the re- |
| ------------ | --------- | ------------- | --- | ------- | ---- | ------------- | --- | ------------ | --------- | --- | ------- |
| due to their | inability | to accomplish |     | complex | rea- |               |     |              |           |     |         |
soning,suchassolvingtasksthatrequiremulti-hop lationshipamongentities,althoughstepkindship
reasoning(Ottetal.,2023). is never mentioned in the question, ChatGPT an-
swersthequestionwithstepkinship,asillustrated
AnalogicalReasoning Analogicalreasoningisa inTable19. WecouldalsoobservethatChatGPT’s
wayofthinkingthatreliesuponananalogy,com- weaknesswithextrinsichallucinationalsodegrades
paring two or more objects or systems of objects machinetranslation. Whenitisaskedtotranslate
(Bartha,2013)todriveaconclusion. Wetestwith the text “Like some other experts, he is skeptical
30samplesfromWebbetal.(2022b)andevaluate about whether diabetes can be cured, noting that
basedonhumanevaluation,toseeifthegenerated these findings have no relevance to people who
answermatchwith/containthegoldanswer. Chat- alreadyhaveType1diabetes.” intoKorean,itcon-
GPTcouldcorrectlyanswerall30examples,which tainsapieceofinformationthatwasnotfoundin
thesource,“저주파치료”(transcutaneouselectri-
mayrevealthatChatGPThasagoodcapabilityin
analogicalreasoningskills. calnervestimulation)inthetranslatedtext.
705

Task Key TextContent
(Javanese)KrajanAnyarMesirkunonggumunmarangmonumen-monumenleluhure,singnalika
Prompt
ikutetepapikluwihsekasewutaun.
Machine ChatGPT TheancientEgyptianPharaohsbuiltbeautifulmonumentsthatarestillwell-preservedafterthou-
Translation Generation sandsofyears.
Hallucination Extrinsic-NewKingdomancientEgyptiansmarveledattheirpredecessorsmonuments,which
werethenwelloverathousandyearold.
[...]ButtheRussianpresidentliftedthebanafterTehranstruckaninterimdealwithBritainand
Prompt
fiveothercountriestocurbnuclearactivitiesinexchangeforsanctionsrelief.[...]
ChatGPT ThemovecomesfollowingtherecentframeworkdealbetweenIranandtheP5+1(US,UK,France,
Summarization Generation China,Russia,andGermany)tocurbIran’snuclearactivitiesinexchangeforsanctionsrelief.
Hallucination ExtrinsicFactual-“P5+1”aretheexactcountriesthatthesourcedocumentmentionsandthemodel
cancorrectlylistthenamesofthesecountriesinsummary.
Continuethedialogueasatask-orienteddialoguesystemcalledSYSTEM.TheanswerofSYSTEM
shouldfollowtheACTIONprovidednextwhileansweringtheUSER’slastutterance:
ACTION: ’Train-Inform’: [[’choice’, ’12’], [’leaveat’, ’05:16’], [’leaveat’, ’16:16’]], ’Train-
OfferBook’:[[’none’,’none’]]
Prompt USER:Ineedtrainreservationsfromnorwichtocambridge
SYSTEM:Ihave133trainsmatchingyourrequest.Isthereaspecificdayandtimeyouwouldlike
totravel?
Task-oriented
USER:I’dliketoleaveonMondayandarriveby18:00.
Dialogue
SYSTEM:Thereare12trainsforthedayandtimeyourequest.Wouldyouliketobookitnow?
USER:Beforebooking,Iwouldalsoliketoknowthetraveltime,price,anddeparturetimeplease.
SYSTEM:ThetraveltimeforthetrainsfromNorwichtoCambridgeisapproximately1hourand
ChatGPT
30minutes.Thepricesforthesetrainsrangefrom£10to£30,andthedeparturetimesare5:16and
Generation
16:16.Pleaseletmeknowifyouwouldliketobookatrainnow.
Hallucination Extrinsic-Therearenoinformationprovidedaboutneithertraveltimenorpricerange
Canwetrydialoguegeneration?Iwillgiveyouturnsandyoucangeneratethenextturn,butonly
one. Youcanalsoconsidertheknowledgeof“PierreCoffinisstarredinDespicableMe2"and
Prompt “DespicableMe2iswrittenbyCincoPaul"foryourreferenceinthedialogue.
Knowledge-
Grounded User:DoyouknowofanymoviesdirectedbyPierreCoffin?
Open-domain
ChatGPT
Dialogue Yes,PierreCoffinistheco-directoroftheanimatedfilm“DespicableMe2."CincoPaulisthe
Generation
film’swriter.
Hallucination animatedfilmisafactualextrinsichallucination.
Prompt [Jason]isverymuchinlovewithhiswife.Hernameis[Gabrielle].[Jason]hasadaughtercalled
[Alma]..WhoisAlmatoGabrielle?
Question
ChatGPT
Answering AlmaisJason’sdaughterandthereforeGabrielle’sstepdaughter.
Generation
Hallucination intrinsic-stepkinshipnevermentionedintheprompt.Groundtruthisdaughter
Prompt WheredopeoplesmokemoreonaveragethaninRussia?
Question ThereareseveralcountrieswherepeoplesmokemoreonaveragethaninRussia. Accordingto
Answering datafromtheWorldHealthOrganization,thefollowingcountrieshavehighersmokingratesthan
(TruthfulQA) Russia:
ChatGPT Indonesia:55.2%ofadultssmoke China:52.9%ofadultssmoke Serbia:47.5%ofadults
Generation smoke SerbiaandMontenegro:45.6%ofadultssmoke Montenegro:45.6%ofadultssmoke
Greece:44.5%ofadultssmoke BosniaandHerzegovina:41.8%ofadultssmoke Kazakhstan:
41.3%ofadultssmoke Kosovo:41.3%ofadultssmoke Moldova:40.9%ofadultssmoke
It’simportanttonotethatthesefiguresareestimatesandmayvaryslightlyfromothersources.
Hallucination Extrinsic-thegeneratedanswerincludeswrongstatistics. (Comparedwithstatisticsfromthe
prevalenceofcurrenttobaccouse(%ofadults)fromtheWorldBankstatistics.7)
[USER-prompt]:DescribehowtheMexicanflaglookslike.
[ChatGPTgeneration]:TheflagofMexicoconsistsofthreeverticalbandsingreen,white,and
Prompt(history)
red.Thegreenbandislocatedatthehoistsideoftheflagandrepresentshope,joy,andlove.[...]
National [USER-prompt]:GenerateacodesnippettorepresentthatflaginSVGformat.
Flag
ChatGPT
Drawing
Generation
Hallucination Intrinsic-Itsaystherearethree“vertical"bandsbutgeneratesthreehorizontalbands.
Table19: Examplesofhallucinationindifferenttasks
706

|     |     |     |     |     |     | Label |     | Metric |     | w/oAPE | w/APE |       |
| --- | --- | --- | --- | --- | --- | ----- | --- | ------ | --- | ------ | ----- | ----- |
|     |     |     |     |     |     |       |     | HTER   |     | 88.14  |       | 88.79 |
Post-Edited
|     |     |     |     |     |     |     |     | SacreBLEU |     | 4.81 |     | 4.20 |
| --- | --- | --- | --- | --- | --- | --- | --- | --------- | --- | ---- | --- | ---- |
MarathiText
|     |     |     |     |     |     |             |                                         | METEOR    |     | 13.10 |     | 12.74 |
| --- | --- | --- | --- | --- | --- | ----------- | --------------------------------------- | --------- | --- | ----- | --- | ----- |
|     |     |     |     |     |     |             |                                         | HTER      |     | 65.36 |     | 63.13 |
|     |     |     |     |     |     | Source      |                                         | SacreBLEU |     | 25.54 |     | 27.20 |
|     |     |     |     |     |     | EnglishText |                                         | METEOR    |     | 43.71 |     | 47.51 |
|     |     |     |     |     |     |             |                                         | BERTScore |     | 92.30 |     | 92.59 |
|     |     |     |     |     |     | Table20:    | Resultoftranslationw/andw/opost-editing |           |     |       |     |       |
onWMT2022English→MarathiAPEsharedtask
2. Queryforthepost-editingusingthefollowing
|     |     |     |     |     |     | prompt       |     | template:                         | “Could               | you | perform | a   |
| --- | --- | --- | --- | --- | --- | ------------ | --- | --------------------------------- | -------------------- | --- | ------- | --- |
|     |     |     |     |     |     | post-editing |     |                                   | to ensure            | the | meaning | is  |
|     |     |     |     |     |     | equivalent   |     | to                                | “[INPUT_SENTENCE]"?” |     |         |     |
|     |     |     |     |     |     | Evaluation:  |     | Thepost-editingresultsaremanually |                      |     |         |     |
validatedbyanativespeakerinthecorresponding
| Figure5: | Anexampleofdialoguesummarization |     |     |     |     |          |              |     |          |             |                 |     |
| -------- | -------------------------------- | --- | --- | --- | --- | -------- | ------------ | --- | -------- | ----------- | --------------- | --- |
|          |                                  |     |     |     |     | language | to validate: |     | 1)       | whether     | the post-edited |     |
|          |                                  |     |     |     |     | sentence | is better    |     | than the | translation | one,            | and |
H DetailsforInteractivityEvaluation
2)whetherthepost-editedsentenceisthecorrect
translationofthegivenEnglishsentence.
H.1 InteractivityonSummarization
Basedontheevaluation,performingautomatic
Figure5showsanexampleofhowmulti-turninter-
|     |     |     |     |     |     | post-editing |     | through | interactive |     | LLMs, | such as |
| --- | --- | --- | --- | --- | --- | ------------ | --- | ------- | ----------- | --- | ----- | ------- |
actionhelpstocontrolthelengthofthesummary.
ChatGPT,yieldsconsistentlybettertranslationre-
|                               |     |                          |        |          |       | sults compared         |     | to         | a single-turn         | machine    |             | transla- |
| ----------------------------- | --- | ------------------------ | ------ | -------- | ----- | ---------------------- | --- | ---------- | --------------------- | ---------- | ----------- | -------- |
| Experiment:                   |     | Two-turniterativeprompt. |        |          |       |                        |     |            |                       |            |             |          |
|                               |     |                          |        |          |       | tion, which            | is  | especially |                       | useful for | translation | in       |
| 1. Given                      | an  | input dialogue           | as the | context, | we    |                        |     |            |                       |            |             |          |
|                               |     |                          |        |          |       | low-resourcelanguages. |     |            | Weprovideper-language |            |             |          |
| firstinputtheprompt“Summarize |     |                          |        | the      | above |                        |     |            |                       |            |             |          |
examplesofthemachine-translatedandpost-edited
dialogue”totheChatGPT.
sentencesinAppendixJ.
| 2. To               | refine | the summary, | we simply |     | input an- |            |              |     |                       |             |     |      |
| ------------------- | ------ | ------------ | --------- | --- | --------- | ---------- | ------------ | --- | --------------------- | ----------- | --- | ---- |
|                     |        |              |           |     |           | H.2.2      | Experiment2: |     | Automaticpost-editing |             |     |      |
| otherprompt–“Please |        |              | make      | the | summary   |            |              |     |                       |             |     |      |
|                     |        |              |           |     |           | To further | strengthen   |     | our                   | hypothesis, | we  | con- |
shorter”afterthefirstresponse.
|             |     |           |           |     |        | duct an      | additional |       | experiment | on           | the automatic |     |
| ----------- | --- | --------- | --------- | --- | ------ | ------------ | ---------- | ----- | ---------- | ------------ | ------------- | --- |
| Evaluation: | We  | calculate | the ROUGE |     | scores |              |            |       |            |              |               |     |
|             |     |           |           |     |        | post-editing |            | (APE) | shared     | task dataset | on            | WMT |
(ROUGE-1,ROUGE-2,andROUGE-L)ofthefirst 2022(Bhattacharyyaetal.,2022),whichfocuses
andsecondsummariesandcomparebetweenturns. on English→Marathi post-editing task. Marathi
(mar)isalsoalow-resourcelanguagewith0.02%
H.2 InteractivityonMachineTranslation
|       |              |     |                         |     |     | data size | on CommonCrawl. |     |     | We  | sample | 50 sam- |
| ----- | ------------ | --- | ----------------------- | --- | --- | --------- | --------------- | --- | --- | --- | ------ | ------- |
| H.2.1 | Experiment1: |     | Multi-turnPost-Editting |     |     |           |                 |     |     |     |        |         |
plesfromthecorrespondingdataset.
WeexplorethecapabilityontranslationfromEn- Evaluation: 1) human-targeted translation er-
| glish to | the target  | language. | For       | the experiment, |      |          |           |     |           |        |               |     |
| -------- | ----------- | --------- | --------- | --------------- | ---- | -------- | --------- | --- | --------- | ------ | ------------- | --- |
|          |             |           |           |                 |      | ror rate | (HTER)8,  |     | SacreBLEU | (Post, | 2018)         | and |
| we adapt | the dataset | used      | in §2.2.2 | which           | sam- |          |           |     |           |        |               |     |
|          |             |           |           |                 |      | METEOR   | (Banerjee |     | and       | Lavie, | 2005) between |     |
ples 30 parallel sentences from 6 language pairs the Marathi generated sentence compared to the
| in NusaX | (Winata | et al., | 2022), Chinese, |     | French, |       |             |     |           |     |       |        |
| -------- | ------- | ------- | --------------- | --- | ------- | ----- | ----------- | --- | --------- | --- | ----- | ------ |
|          |         |         |                 |     |         | human | post-edited |     | sentence, | 2)  | HTER, | Sacre- |
Indonesian,Korean,Javanese,andSundanese.
BLEU,METEOR,andsemanticsimilarityscore,
|          |       |              |     |            |      | i.e., BERTScore |     | (Zhang* |     | et al., | 2020), between |     |
| -------- | ----- | ------------ | --- | ---------- | ---- | --------------- | --- | ------- | --- | ------- | -------------- | --- |
| 1. Query | model | to translate | to  | the target | lan- |                 |     |         |     |         |                |     |
theEnglishback-translatedsentenceandoriginal
| guageusing“What |     |     | is [TARGET_LANGUAGE] |           |     |     |     |     |     |     |     |     |
| --------------- | --- | --- | -------------------- | --------- | --- | --- | --- | --- | --- | --- | --- | --- |
| translation     |     | of  | the                  | following |     |     |     |     |     |     |     |     |
8HTERistheofficialevaluationmetricusedintheAPE
sentence?\n\n[INPUT_SENTENCE]”
2022sharedtask.
707

| Figure6: | ExampleoftheCanadianflagdrawnbyIn- |     |     |     |     |
| -------- | ---------------------------------- | --- | --- | --- | --- |
structGPT.
Englishsentence.9
| As shown | on Table | 20, | the single-turn | transla- |     |
| -------- | -------- | --- | --------------- | -------- | --- |
tionwithoutpost-editingproducesaslightlybetter
evaluationscoreontheMarathilanguage,butthe
multi-turnwithpost-editingconsistentlyyieldsbet-
terevaluationperformanceontheback-translated
| Englishtextonallmetrics. |     |     | Thissuggeststhatpost- |     |     |
| ------------------------ | --- | --- | --------------------- | --- | --- |
editingenablesthetranslationresultstobecloserto
| theactualmeaningofthesourcetext. |     |             |          | Nevertheless, |      |
| -------------------------------- | --- | ----------- | -------- | ------------- | ---- |
| the translation                  | to  | the Marathi | language | is            | much |
worsecomparedtothebaselineMTprovidedfrom
| the APE     | 2022 shared | task     | (Bhattacharyya |             | et al., |
| ----------- | ----------- | -------- | -------------- | ----------- | ------- |
| 2022) which | further     | supports | the            | limitations | of      |
ChatGPTongeneratingsentencesinlow-resource
andnon-Latinscriptlanguages.
H.3 InteractivityonMultimodalGeneration
| We show | an example | of  | a multi-turn | flag | draw- |
| ------- | ---------- | --- | ------------ | ---- | ----- |
ingofInstructGPT,whichhasthesamebackbone
modelasChatGPTbutlacksconversationability,
| inFigure6. | SimilartoChatGPT,InstructGPTcan |      |          |            |     |
| ---------- | ------------------------------- | ---- | -------- | ---------- | --- |
| revise the | generated                       | flag | image in | each turn, | al- |
Figure7: FromfruitstoaChristmastree. Step-by-step
though the generation quality is still elementary. imagedrawingandmodificationbyChatGPT.
Figure7showstheprocessofcreatinganinterest-
| ing painting | by prompting |     | ChatGPT | with | varied |
| ------------ | ------------ | --- | ------- | ---- | ------ |
requirementsthroughmultipleturns.
9thebacktranslationprocessisdoneviaGoogleTranslate
(https://translate.google.com/).
708

I ListofEvaluationDatasets
WeprovideadetailedlistofallthedatasetsusedinourexperimentonTable21.
| Dataset | Task | Description |     |     |     |     | Reference | #TestSize | #ChatGPTEval |
| ------- | ---- | ----------- | --- | --- | --- | --- | --------- | --------- | ------------ |
National Flag IG NationalFlagDrawingisadesignedsyntheticdatasetwhichisusedto Curatedbyauthorsof 50 50
Drawing evaluate the multimodal understanding of LLMs. The instruction for thispaper
|     |     | theNationalFlagDrawingisasfollow: |     | givenanation,drawthecorre- |     |     |     |     |     |
| --- | --- | --------------------------------- | --- | -------------------------- | --- | --- | --- | --- | --- |
spondingnationalflagandreviseitbasedonthefollow-upcorrection
requests.
CNN/DM SUM TheCNN/DailyMailDatasetisanEnglish-languagedatasetcontaining Nallapatietal.(2016) 11490 50
|     |     | just over | 300k unique news | articles as written      | by journalists  | at CNN |     |     |     |
| --- | --- | --------- | ---------------- | ------------------------ | --------------- | ------ | --- | --- | --- |
|     |     | and the   | Daily Mail. The  | current version supports | both extractive | and    |     |     |     |
abstractivesummarization,thoughtheoriginalversionwascreatedfor
machine-readingandcomprehensionandabstractivequestionanswer-
ing.
SAMSum SUM SAMSumdatasetcontainsabout16kmessenger-likeconversationswith Gliwaetal.(2019) 819 50
|     |     | summaries.       | Conversationswerecreatedandwrittendownbylinguists |     |     |     |     |     |     |
| --- | --- | ---------------- | ------------------------------------------------- | --- | --- | --- | --- | --- | --- |
|     |     | fluentinEnglish. | Linguistswereaskedtocreateconversationssimilar    |     |     |     |     |     |     |
709
tothosetheywriteonadailybasis,reflectingtheproportionoftopicsof
theirreal-lifemessengerconvesations.
FLoRes-200 MT FLoResisabenchmarkdatasetformachinetranslationbetweenEnglish Goyaletal.(2021) 1012 per language 30 per language (12
andfourlowresourcelanguages,Nepali,Sinhala,KhmerandPashto, (200languages) languages)
basedonsentencestranslatedfromWikipedia.
NusaX SA NusaXisahigh-qualitymultilingualparallelcorpusthatcovers12lan- Winataetal.(2022) 400 50
guages,Indonesian,English,and10Indonesianlocallanguages,namely
|     |     | Acehnese, | Balinese, Banjarese, | Buginese, | Madurese, Minangkabau, |     |     |     |     |
| --- | --- | --------- | -------------------- | --------- | ---------------------- | --- | --- | --- | --- |
Javanese,Ngaju,Sundanese,andTobaBatak.
bAbItask15 QA ThisbasicdeductionbAbItasksistakenfromthe(20)QAbAbItasks Westonetal.(2016b) 1000 30
thatasetofproxytasksthatevaluatereadingcomprehensionviaques-
|     |     | tion answering. | The tasks        | measure understanding | in several | ways:      |     |     |     |
| --- | --- | --------------- | ---------------- | --------------------- | ---------- | ---------- | --- | --- | --- |
|     |     | whether         | a system is able | to answer questions   | via simple | deduction. |     |     |     |
Thetasksaredesignedtobeprerequisitesforanysystemthataimstobe
capableofconversingwithahuman.

bAbItask16 QA ThisbasicinductionbAbItasksistakenfromthe(20)QAbAbItasksthat Westonetal.(2016b) 1000 30
asetofproxytasksthatevaluatereadingcomprehensionviaquestion
| answering.                                       | Thetasksmeasureunderstandinginseveralways: |     |     |     |     |             | whethera |
| ------------------------------------------------ | ------------------------------------------ | --- | --- | --- | --- | ----------- | -------- |
| systemisabletoanswerquestionsviasimpleinduction. |                                            |     |     |     |     | Thetasksare |          |
designedtobeprerequisitesforanysystemthataimstobecapableof
conversingwithahuman.
EntailmentBank QA ENTAILMENTBANK,thefirstdatasetofmultistepentailmenttreesfor Dalvietal.(2021) 340 30
| QA,tosupportentailment-basedexplanation. |            |       |            |        | ENTAILMENTBANK |         |       |
| ---------------------------------------- | ---------- | ----- | ---------- | ------ | -------------- | ------- | ----- |
| contains                                 | two parts: | 1,840 | entailment | trees, | each tree      | showing | how a |
question-answerpair(QA)isentailedfromasmallnumberofrelevant
sentences(e.g.,Figure1);andageneralcorpusC,containingthoseand
othersentencesofdomain-specificandgeneralknowledgerelevantto
theQAdomain.
CLUTRR QA CLUTRR(CompositionalLanguageUnderstandingandText-basedRe- Sinhaetal.(2019) 1146 30
lationalReasoning),adiagnosticbenchmarksuite,isfirstintroducedin
(https://arxiv.org/abs/1908.06177)totestthesystematicgeneralization
| and inductive | reasoning |     | capabilities | of NLU | systems. | The | CLUTRR |
| ------------- | --------- | --- | ------------ | ------ | -------- | --- | ------ |
benchmarkallowsustotestamodel’sabilityforsystematicgeneraliza-
| tion by | testing on | stories | that contain | unseen | combinations |     | of logical |
| ------- | ---------- | ------- | ------------ | ------ | ------------ | --- | ---------- |
710
| rules, and | test for | the | various | forms of | model robustness |     | by adding |
| ---------- | -------- | --- | ------- | -------- | ---------------- | --- | --------- |
differentkindsofsuperfluousnoisefactstothestories.
αNLI QA AbductiveNaturalLanguageInference(αNLI)isanewcommonsense Bhagavatula et al. 3059 30
| benchmarkdatasetdesignedtotestanAIsystem’scapabilitytoapply |     |     |     |     |     |     | (2020) |
| ----------------------------------------------------------- | --- | --- | --- | --- | --- | --- | ------ |
abductivereasoningandcommonsensetoformpossibleexplanations
| for a given | set of | observations. |     | Formulated | as a binary-classification |     |     |
| ----------- | ------ | ------------- | --- | ---------- | -------------------------- | --- | --- |
task,thegoalistopickthemostplausibleexplanatoryhypothesisgiven
twoobservationsfromnarrativecontexts.
CommonsenseQA QA CommonsenseQAisanewmultiple-choicequestionansweringdataset Talmoretal.(2018) 1221 30
thatrequiresdifferenttypesofcommonsenseknowledgetopredictthe
| correctanswers.                       |            | Itcontains12,102questionswithonecorrectanswer |     |                             |             |     |           |
| ------------------------------------- | ---------- | --------------------------------------------- | --- | --------------------------- | ----------- | --- | --------- |
| and four                              | distractor | answers.                                      | The | dataset                     | is provided | in  | two major |
| training/validation/testingsetsplits: |            |                                               |     | “Randomsplit"whichisthemain |             |     |           |
evaluationsplit,and“Questiontokensplit",seepaperfordetails.

HotpotQA QA HotpotQAisanewdatasetwith113kWikipedia-basedquestion-answer Yangetal.(2018) 7405 30
|     | pairswithfourkeyfeatures: |     |     | (1)thequestionsrequirefindingandrea- |     |     |     |     |     |
| --- | ------------------------- | --- | --- | ------------------------------------ | --- | --- | --- | --- | --- |
soningovermultiplesupportingdocumentstoanswer;(2)thequestions
|     | are diverse | and | not constrained |     | to any | pre-existing |     | knowledge | bases |
| --- | ----------- | --- | --------------- | --- | ------ | ------------ | --- | --------- | ----- |
orknowledgeschemas;(3)weprovidesentence-levelsupportingfacts
requiredforreasoning,allowingQAsystemstoreasonwithstrongsu-
pervisionandexplainthepredictions;(4)weofferanewtypeoffactoid
comparisonquestionstotestQAsystems’abilitytoextractrelevantfacts
andperformnecessarycomparison.
PiQA QA To apply eyeshadow without a brush, should I use a cotton swab or Bisketal.(2020) 1838 30
|     | a toothpick? | Questions | requiring |     | this | kind | of physical | commonsense |     |
| --- | ------------ | --------- | --------- | --- | ---- | ---- | ----------- | ----------- | --- |
poseachallengetostate-of-the-artnaturallanguageunderstandingsys-
tems. ThePIQAdatasetintroducesthetaskofphysicalcommonsense
reasoningandacorrespondingbenchmarkdatasetPhysicalInteraction:
QuestionAnsweringorPIQA.Physicalcommonsenseknowledgeisa
majorchallengeontheroadtotrueAI-completeness,includingrobots
|     | that interact | with | the world | and | understand |     | natural | language. | PIQA |
| --- | ------------- | ---- | --------- | --- | ---------- | --- | ------- | --------- | ---- |
focusesoneverydaysituationswithapreferenceforatypicalsolutions.
Thedatasetisinspiredbyinstructables.com,whichprovidesuserswith
711
|     | instructions | on  | how to build, | craft, | bake, | or  | manipulate | objects | using |
| --- | ------------ | --- | ------------- | ------ | ----- | --- | ---------- | ------- | ----- |
everydaymaterials.
E-Care QA UnderstandingcausalityhasvitalimportanceforvariousNaturalLan- Duetal.(2022) 2122 30
|     | guage Processing |     | (NLP) | applications. |     | Beyond | the | labeled | instances, |
| --- | ---------------- | --- | ----- | ------------- | --- | ------ | --- | ------- | ---------- |
conceptualexplanationsofthecausalitycanprovideadeepunderstand-
|     | ing of the | causal | fact to | facilitate | the | causal | reasoning | process. | We  |
| --- | ---------- | ------ | ------- | ---------- | --- | ------ | --------- | -------- | --- |
presentahuman-annotatedexplainableCAusalREasoningdataset(e-
CARE),whichcontainsover20Kcausalreasoningquestions,together
withnaturallanguageformedexplanationsofthecausalquestions.
Letterstringanal- QA The letter string analogy domain was introduced in order to evaluate Webbetal.(2022b) - 30
| ogy | computationalmodelsofanalogicalreasoning. |     |     |     |     |     | Thistaskiscomposed |     |     |
| --- | ----------------------------------------- | --- | --- | --- | --- | --- | ------------------ | --- | --- |
ofsimplealphanumericcharacters,butneverthelessrequireasignificant
degreeofabstractiontoidentifyananalogy.

SpaRTQA QA SpartQA is a textual question answering benchmark for spatial rea- Mirzaeeetal.(2021) 510 64
| soning | on natural | language |     | text which | contains | more | realistic | spatial |
| ------ | ---------- | -------- | --- | ---------- | -------- | ---- | --------- | ------- |
phenomenanotcoveredbypriordatasetsandthatischallengingforstate-
of-the-artlanguagemodels(LM).SPARTQAisbuiltonNLVR’simages
| containingmoreobjectswithricherspatialstructures. |     |     |     |     |     |     | SPARTQA’ssto- |     |
| ------------------------------------------------- | --- | --- | --- | --- | --- | --- | ------------- | --- |
riesaremorenatural,havemoresentences,andricherinspatialrelations
ineachsentence,andthequestionsrequiredeeperreasoningandhave
| fourtypes:    | findrelation(FR),findblocks(FB),chooseobject(CO),and |              |     |                   |     |          |     |            |
| ------------- | ---------------------------------------------------- | ------------ | --- | ----------------- | --- | -------- | --- | ---------- |
| yes/no        | (YN),                                                | which allows | for | more fine-grained |     | analysis |     | of models’ |
| capabilities. | Thedefaulttestsetofthisdatasetishuman-annotatedtest  |              |     |                   |     |          |     |            |
set,whichconsistsof510instances.
StepGame QA StepGame is a robust multi-hop spatial reasoning dataset in textual Shietal.(2022b) 30000 30
formatwhichaddressesthelimitationfromthebAbIdatasettask17and
task19. Inthistask,theAIsystemisrequiredtointerpretastoryofk
spatialrelations(e.gleft,top-right,90degreeclockwise)ofk+1entities
| (k is up                                      | to 10) | expressed | in  | natural language |     | and             | answer | a question |
| --------------------------------------------- | ------ | --------- | --- | ---------------- | --- | --------------- | ------ | ---------- |
| abouttherelativepositionoftwoofthoseentities. |        |           |     |                  |     | Foreachkfrom1to |        |            |
10,thereare30000,1000,and30000samplesfortrain,valid,andtest
respectively.
712
Pep-3k QA Pep-3kisadatasetofphysicalsemanticplausibilityjudgmentsofsingle Wangetal.(2018b) 3080 30
events. Itrequiresamixtureofcommonsenseknowledgeandconceptual
| knowledge                                       | to  | solve. Each | event | consists | of                       | a subject, | a verb,        | and an |
| ----------------------------------------------- | --- | ----------- | ----- | -------- | ------------------------ | ---------- | -------------- | ------ |
| object,i.eithasthesimples-v-oformat.            |     |             |       |          | Forexample,theeventcanbe |            |                |        |
| manswallowpaintball,withthelabel0(implausible). |     |             |       |          |                          |            | Intotal,Pep-3k |        |
has3080instanceswithplausible-implausibledatabalance.
COVID-Social MD COVID-19-related claims fact-checked by journalists from a website Leeetal.(2021) 340 50
| calledPolitifact.com. |     | UnliketheCovid19-Scientificdataset,itcontains |     |     |     |     |     |     |
| --------------------- | --- | --------------------------------------------- | --- | --- | --- | --- | --- | --- |
non-scientificandsocially-relatedclaims,suchas“Forthecoronavirus,
thedeathrateinTexas,percapitaof29millionpeople,we’reoneofthe
| lowestinthecountry.” |     |     | Suchclaimsmaynotbelife-and-deathmatters, |     |     |     |     |     |
| -------------------- | --- | --- | ---------------------------------------- | --- | --- | --- | --- | --- |
buttheystillhavethepotentialtobringnegativesociopoliticaleffects.
COVID- MD COVID-ScientificisatestsetconsistsofCOVID-19-relatedscientific Leeetal.(2021) 172 50
Scientific ormedicalmythsthatmustbedebunkedcorrectlytoensurethesafety
ofthepublic(e.g.,“Drinkingableachsolutionwillpreventyoufrom
gettingCOVID-19").

TruthfulQA QA The dataset comprises questions that span 38 categories, including Linetal.(2022) 817 65
| health,law,financeandpolitics. |                | Thequestionsareofthosethatsome |                |                   |     |     |
| ------------------------------ | -------------- | ------------------------------ | -------------- | ----------------- | --- | --- |
| humans would                   | answer falsely | due to                         | a false belief | or misconception. |     |     |
(e.g.,[conspiracy]“Ifit’scoldoutsidewhatdoesthattellusaboutglobal
warming?”;[health]“Cancoughingeffectivelystopaheartattack?”)
MultiWOZ2.2 TOD MultiWOZ2.2isanimprovedversionofMultiWOZ2.1,whichiden- Zangetal.(2020) 5000dialogueturns 50dialogturns
| tifies and fixes | dialogue | state annotation | errors across | 17.3% | of the |     |
| ---------------- | -------- | ---------------- | ------------- | ----- | ------ | --- |
utterancesontopofMultiWOZ2.1andredefinestheontologybydis-
allowingvocabulariesofslotswithalargenumberofpossiblevalues
(e.g.,restaurantname,timeofbooking)andintroducingstandardized
slotspanannotationsfortheseslots.
OpenDialKG KGD OpenDialKGisadatasetofconversationsbetweentwocrowdsourcing Moonetal.(2019) 2.25k dialogue ses- 50dialogueturns
| agents engaging | in a dialog | about a given | topic. Each | dialog turn | is  | sions |
| --------------- | ----------- | ------------- | ----------- | ----------- | --- | ----- |
pairedwithitscorresponding“KGpaths”thatweavetogethertheKG
entitiesandrelationsthatarementionedinthedialog.
Table21: Listofalldatasetsusedinourexperiments. IGdenotesimagegeneration,SUMdenotessummarization,MTdenotesmachinetranslation,SAdenotessentimentanalysis,QAdenotes
questionanswering,MDdenotesmisinformationdetection,TODdenotestask-orienteddialogue,andKGDdenotesknowledge-groundeddialogue. Someofthedescriptionsaredirectlyfromthe
originalreference.
713

J ExamplesfromMachineTranslationandPost-Editing
| Target | EnglishText |     |     | Label | Translation | Post-EditedText |     |
| ------ | ----------- | --- | --- | ----- | ----------- | --------------- | --- |
Chinese Althoughthreepeoplewereinsidethe 虽然车撞到房子时，房子里面有 尽管有三个人在汽车撞上房子 尽管汽车撞上房子时有三个人在
|     |     |     |     | 三个人，但最后并没有人受伤。 | 的时候在屋里，但他们都没有受 | 屋里，但他们都没有受伤。 |     |
| --- | --- | --- | --- | -------------- | -------------- | ------------ | --- |
housewhenthecarimpactedit,none
|     | ofthemwerehurt. |     |     |     | 伤。  |     |     |
| --- | --------------- | --- | --- | --- | --- | --- | --- |
Chinese 34percentofthoseinthepollshare 34% 的受访者一致表示，希望英 这项民意调查显示，34%的人希望 根据民意调查显示，34%的人希望
|     |     |     |     | 国女王伊丽莎白二世成为澳大利 | 伊丽莎白二世是澳大利亚的最后 | 伊丽莎白二世成为澳大利亚的最 |     |
| --- | --- | --- | --- | -------------- | -------------- | -------------- | --- |
thisview,wantingQueenElizabethII
|     |     |     |     | 亚的最后一任君主。 | 一位君主。 | 后一位君主。 |     |
| --- | --- | --- | --- | --------- | ----- | ------ | --- |
tobeAustralia’slastmonarch.
Chinese Thequalitiesthatdetermineasubcul- 让亚文化变得与众不同的特质， 什么决定一个亚文化作为不同的 决定一个亚文化与众不同的特质
tureasdistinctmaybelinguistic,aes- 可能是语言、美学、宗教、政 特质可能是语言的、审美的、宗 可能是语言的、审美的、宗教
|     |     |     |     | 治、性别、地理或多种因素的组 | 教的、政治的、性的、地理的， | 的、政治的、性的、地理的，或 |     |
| --- | --- | --- | --- | -------------- | -------------- | -------------- | --- |
thetic,religious,political,sexual,geo-
|     |     |     |     | 合。  | 或者这些因素的组合。 | 者是这些因素的组合。 |     |
| --- | --- | --- | --- | --- | ---------- | ---------- | --- |
graphical,oracombinationoffactors.
Chinese NewKingdomancientEgyptiansmar- 新王国时期的古埃及人惊叹于其 新王朝古埃及人惊叹于他们的前 新王朝的古埃及人惊叹于他们前
velled at their predecessors monu- 前辈的已有一千多年历史的纪念 人的纪念碑，当时已经有一千多 人留下的纪念碑，当时已经有超
|     |        |            |                | 碑。  | 年的历史了。 | 过一千年的历史。 |     |
| --- | ------ | ---------- | -------------- | --- | ------ | -------- | --- |
|     | ments, | which were | then well over | a   |        |          |     |
thousandyearold.
714
Chinese The U.S. Corps of Engineers esti- 美国陆军工兵部队估计，6英寸的 美国工程兵部队估计，6英寸的降 美国工程兵部队估计，6英寸的降
mated that 6 inches of rainfall could 降雨量就可能冲垮之前损坏的堤 雨可能会破坏先前受损的堤坝。 雨可能会使先前受损的堤坝再次
|     |        |                |              | 坝。  |     | 损坏。 |     |
| --- | ------ | -------------- | ------------ | --- | --- | --- | --- |
|     | breach | the previously | damaged lev- |     |     |     |     |
ees.
Korean Althoughthreepeoplewereinsidethe 차가 집에 충ᅩᆯᄃ했을 때 세 명이 안 차가 집에 부딪히자 집 안에 세 사 차가 집에 부딪히자 집 안에 세 사
에있었지만,그들ᅮᆼᄌ한ᅧᆼᄆ도다치 람이 있었지만, 아무도 다치지 않 람이 있었지만, 아무도 상해를 입
housewhenthecarimpactedit,none
|     |     |     |     | 지않ᅡᆻᄋ다. | 았습니ᅡᄃ. | 지않았습니다. |     |
| --- | --- | --- | --- | ----------- | ----------- | ---------------- | --- |
ofthemwerehurt.
Korean 34percentofthoseinthepollshare 여론조ᅡᄉ에서34퍼센트ᅡᄀ엘리ᅡᄌ 34%가 이 의견을 공감하며, 아스 이 조사에서는 34%가 엘리ᅡᄌ베스
thisview,wantingQueenElizabethII 베스 2세가 호주의 마지막 군주이 트레일리아의최후의왕조가엘리 2세가 아스트레일리아의 최후의
길바란다는의견을보였습니ᅡᄃ. 자ᅦᄇ스2세가되기를원한다. 왕조가 ᅬᄃ기를 원한다는 의견을
tobeAustralia’slastmonarch.
공감ᅡᆫᄒ다.
Korean Thequalitiesthatdetermineasubcul- 하위문화를명확하게구분하는특 “다음 ᅮᆫᄆ장의 ᅡᆫᄒ국어 번역은 무엇 부문문화가구별되는특성은언어
tureasdistinctmaybelinguistic,aes- 징은언어적,미적,종교적,정치적, 입니까? 부문문화를 구별되게 하 적, 예술적, 종교적, 정치적, 성적,
성적, 지리적 요소가 있으며, 이러 특성은 언어, 예술, 종교, 정치, 지리적 요소 하나일 수도 있고,
|     | thetic,religious,political,sexual,geo- |     |     |     | 는 |     | 중 |
| --- | -------------------------------------- | --- | --- | --- | --- | --- | --- |
한요ᅩᄉ들의결합일수ᅩᄃ있다. 성,지리요소일수있거나이들요 이들 요소의 조합일 수도 있습니
graphical,oracombinationoffactors.
|     |     |     |     |     | 소의조합일수도있습니다." | 다. |     |
| --- | --- | --- | --- | --- | ---------------------------- | --- | --- |

Korean NewKingdomancientEgyptiansmar- 고대 신왕국 이집트인들은 조상 신나라이집트인들은전자들이지 신나라이집트인들은전자들이지
의 기념비적인 보고 경 금보다 약 이상 오래된 고 금보다 약 이상 오래된 고
velled at their predecessors monu- ᅥᆫᄀ축물을 1,000년 1,000년
탄했고 이것은 그 당시 기준으로 대유적을창구로칭ᅢᆻᄒ습니다. 대 유적을 창구로 칭ᅢᆻᄒ고, 그들은
|     | ments, which | were then well | over a |     |     |
| --- | ------------ | -------------- | ------ | --- | --- |
thousandyearold. 1000년은족히넘은건축물이었습 그것들ᅳᆯᄋ참화했습니다.
니ᅡᄃ.
미국 공병대는 시간ᅡᆼᄃ 6인치의 ᅡᆼᄀ 미국 엔지니어 중대는 6인치의 비 미국 엔지니어 중대는 6인치의 비
| Korean | The U.S. | Corps of Engineers | esti- |     |     |
| ------ | -------- | ------------------ | ----- | --- | --- |
우량이 기 파손된 제방을 무너뜨 가 이전에 손상된 제방을 깨고 들 가 이전에 손상된 제방을 깨고 가
|     | mated that | 6 inches of rainfall | could |     |     |
| --- | ---------- | -------------------- | ----- | --- | --- |
breach the previously damaged lev- 릴수있다ᅩᄀ추정ᅢᆻᄒ다. 어올수있다고추정ᅢᆻᄒ습니다. 로막을 칠 수 있다고 추정했습니
다.
ees.
|          |                                  |     | 車の衝突時には３人が家の中に | この文を日本語に訳すと、「車 | もしよろしければ、この文を元 |
| -------- | -------------------------------- | --- | -------------- | -------------- | -------------- |
| Japanese | Althoughthreepeoplewereinsidethe |     |                |                |                |
housewhenthecarimpactedit,none いましたが、怪我人はいません が家に衝突したときには家の中 の文の意味を維持しながら、よ
|     | ofthemwerehurt. |     | でした。 | に3人いましたが、そのうちの誰 | り日本語らしい表現に書き換え |
| --- | --------------- | --- | ---- | --------------- | -------------- |
|     |                 |     |      | も傷を負わなかった」となりま  | ることもできます。例えば次の |
|     |                 |     |      | す。              | ようになります。「車が家に衝 |
突したときには、家の中には3人
いましたが、どの人も怪我をし
なかった」
|          |                                |     | 世論調査では34%の人がこの意見 | の人たちは、この見解を共 | のアンケートに参加した人 |
| -------- | ------------------------------ | --- | ---------------- | ------------ | ------------ |
| Japanese | 34percentofthoseinthepollshare |     |                  | 34%          | 34%          |
715 thisview,wantingQueenElizabethII に賛成しており、エリザベス女 有して、イングランド女王エリ たちのうち、この見解を共有し
|     |     |     | 王2世がオーストラリア最後の君 | ザベス2世が最後の王位を持つこ | ており、イングランド女王エリ |
| --- | --- | --- | --------------- | --------------- | -------------- |
tobeAustralia’slastmonarch.
|     |     |     | 主であることを望んでいます。 | とを望む。 | ザベス2世がオーストラリアで最 |
| --- | --- | --- | -------------- | ----- | --------------- |
後の王位を持つことを望んでい
ます。
|          |                                   |     | サブカルチャーの特徴を決定付 | サブカルチャーを特徴的なもの | そのような品質は、サブカル |
| -------- | --------------------------------- | --- | -------------- | -------------- | ------------- |
| Japanese | Thequalitiesthatdetermineasubcul- |     |                |                |               |
|          |                                   |     | ける性質は、言語、美、宗教、 | とする品質は、言語的、美学  | チャーを特徴的なものとする |
tureasdistinctmaybelinguistic,aes-
thetic,religious,political,sexual,geo- 政治、性、地理、またはそれら 的、宗教的、政治的、性的、地 ものである可能性があります。
graphical,oracombinationoffactors. の要素の組み合わせかもしれま 理的、あるいはそれらの要因の 言語的、美学的、宗教的、政治
|     |     |     | せん。 | 組み合わせであることがありま | 的、性的、地理的、あるいはそ |
| --- | --- | --- | --- | -------------- | -------------- |
|     |     |     |     | す。             | れらの要因の組み合わせである |
ことがあります。
|          |                                |                    | 新王国の古代エジプト人たち  | 新王国時代のエジプト人は、    | 新王国時代のエジプト人は、そ |
| -------- | ------------------------------ | ------------------ | -------------- | ---------------- | -------------- |
| Japanese | NewKingdomancientEgyptiansmar- |                    |                |                  |                |
|          |                                |                    | は、当時千年以上前に建てられ | 当時すでに1000年以上も古い前 | れらの先人の墓苑が当時すで  |
|          | velled at                      | their predecessors | monu-          |                  |                |
ments, which were then well over a た前身のモニュメントに驚嘆し 人のモニュメントに驚嘆しまし に1000年以上も古いことに驚嘆
|     | thousandyearold. |     | ました。 | た。  | しました。 |
| --- | ---------------- | --- | ---- | --- | ----- |

716
Japanese The U.S. Corps of Engineers esti- 米工兵隊は、以前に決壊した堤 米国エンジニア兵団は、6インチ 以前に損傷を受けた堤防が、米
mated that 6 inches of rainfall could 防が6インチの降水量で再び決壊 の降雨で以前に損傷した堤防が 国エンジニア兵団が推定する6イ
breach the previously damaged lev- する可能性があると推定してい 浸水すると推定しています。 ンチの降雨で浸水するかもしれ
ees. ます。 ません。
French Althoughthreepeoplewereinsidethe Bien que trois personnes aient été Bienquetroispersonnessetrouvaient Même si trois personnes étaient à
housewhenthecarimpactedit,none présentes dans la maison quand la à l’intérieur de la maison lorsque l’intérieur de la maison lorsque la
ofthemwerehurt. voiture l’a percutée, aucune n’a été la voiture a percuté celle-ci, aucune voiture a heurté celle-ci, aucune
blessée. d’entreellesn’aétéblessée. d’entreellesn’aétéblessée.
French 34percentofthoseinthepollshare 34%despersonnesinterrogéesparta- 34pourcentdeceuxquiontparticipé 34pourcentdeceuxquiontparticipé
thisview,wantingQueenElizabethII gentcepointdevue,etsouhaitentque àl’enquêtepartagentcetavis,souhai- à l’enquête souhaitent que la reine
tobeAustralia’slastmonarch. la reine Elizabeth II soit la dernière tant que la reine Elizabeth II soit la ElizabethIIsoitladernièremonarchie
monarqueàrégnersurl’Australie. dernièremonarchied’Australie d’Australie.
French Thequalitiesthatdetermineasubcul- Lescritèresquidéterminentunesous- Lesqualitésquidéterminentunesous- Les caractéristiques qui déterminent
tureasdistinctmaybelinguistic,aes- culturecommedistinctepeuventêtre culturecommedistinctepeuventêtre unesous-culturecommedistinctepeu-
thetic,religious,political,sexual,geo- linguistiques, esthétiques, religieux, linguistiques,esthétiques,religieuses, ventêtrelinguistiques,esthétiques,re-
graphical,oracombinationoffactors. politiques,sexuels,géographiquesou politiques, sexuelles, géographiques ligieuses, politiques, sexuelles, géo-
unecombinaisondefacteurs. ouunecombinaisondefacteurs." graphiquesouunecombinaisondeces
éléments.
French NewKingdomancientEgyptiansmar- Les Égyptiens antiques du Nouvel LesÉgyptiensanciensdelaNouvelle- LesÉgyptiensanciensdelaNouvelle-
velled at their predecessors monu- Empire étaient émerveillés par les République admiraient les monu- République admiraient les monu-
ments, which were then well over a monuments de leurs prédécesseurs, ments de leurs prédécesseurs, qui ments de leurs prédécesseurs, qui
thousandyearold. qui avaient alors bien plus de mille étaientalorsbienplusâgésd’unmil- avaientalorsplusdemilleans.
ans. lénaire.
French The U.S. Corps of Engineers esti- D’après le U.S. Corps of Engineers, Le Corps des ingénieurs des États- Le Corps des ingénieurs des États-
mated that 6 inches of rainfall could une pluviométrie de 6 pouces pour- Unisaestiméqu’unepluiede15cm Unis a estimé qu’une pluie de 15
breach the previously damaged lev- raitouvrirunebrèchedanslesdigues pourraitaffaiblirlesdiguesprécédem- cm pourrait mettre à mal les digues
ees. précédemmentendommagées. mentendommagées. précédemmentendommagées.
Indonesian Althoughthreepeoplewereinsidethe Walauadatigaorangdidalamrumah Meskipun tiga orang ada di dalam Meskipun tiga orang ada di dalam
housewhenthecarimpactedit,none yang ditabrak mobil, tak satu pun rumahsaatmobilmenabraknya,tidak rumah saat mobil menabraknya,
ofthemwerehurt. yangcedera. adayangterluka. merekasemuaselamat.
Indonesian 34percentofthoseinthepollshare Dalamjajakpendapatmengenaipan- 34 persen dari orang yang terlibat 34 persen dari orang yang terlibat
thisview,wantingQueenElizabethII dangan ini, 34 persen dari mereka dalampollinginimemilikipandangan dalampollinginimemilikipandangan
tobeAustralia’slastmonarch. menginginkanRatuElizabethIImen- yangsama,yaituinginRatuElizabeth yangsama,yaituinginRatuElizabeth
jadipemimpinmonarkiterakhirAus- IImenjadiratuterakhirdiAustralia. IImenjadiratuterakhirdiAustralia.
tralia.

717
Indonesian Thequalitiesthatdetermineasubcul- Kualitasyangmenentukansuatusub- Kualitasyangmenentukansuatusub- Faktor-faktor yang menentukan se-
tureasdistinctmaybelinguistic,aes- kultur berbeda dari yang lain bisa kultur sebagai distinct dapat berupa buah subkultur sebagai distinct bisa
thetic,religious,political,sexual,geo- berupabahasa,estetika,agama,poli- linguistik, estetika, agama, politik, berupa faktor linguistik, estetika,
graphical,oracombinationoffactors. tik,seksual,geografis,ataukombinasi seksual, geografis, atau kombinasi agama, politik, seksual, geografis,
sejumlahfaktor. faktor-faktortersebut. atau kombinasi dari beberapa faktor
tersebut.
Indonesian NewKingdomancientEgyptiansmar- Kerajaan Baru Mesir kuno men- Kekaisaran Baru orang-orang Mesir Orang-orangMesirkunoKekaisaran
velled at their predecessors monu- gagumimonumenparapendahulunya, kuno terpesona dengan monumen- Baru terpesona dengan monumen-
ments, which were then well over a yangsaatituberusialebihdariseribu monumen pendahulunya, yang saat monumen pendahulunya, yang saat
thousandyearold. tahun. itusudahlebihdariseributahuntua. itusudahlebihdariseributahuntua.
Indonesian The U.S. Corps of Engineers esti- U.S. Corps of Engineers memperki- Korps Engineer AS menghitung Badan Engineer AS memperkirakan
mated that 6 inches of rainfall could rakan bahwa curah hujan sebesar 6 bahwa hujan 6 inci dapat merusak bahwahujan6incidapatmenembus
breach the previously damaged lev- inci ini mampu menerobos tanggul parityangsebelumnyasudahrusak. parityangsebelumnyasudahrusak.
ees. yangsudahrusak.
Javanese Althoughthreepeoplewereinsidethe Sanadyan uwong telu ana ing njero Walaupuntigaorangberadadidalam Walaupun ana ing tiga wong ing
housewhenthecarimpactedit,none omahnalikamobilkuwinabrak,nang- rumahsaatmobilmenabraknya,tidak rumahkalamobilmbentakingkono,
ofthemwerehurt. ingkabehselamet. adadiantaramerekayangterluka. oraanasakaingkangterluka.
Javanese 34percentofthoseinthepollshare 34 per sen sing menehi swara se- Sebagian34persendarimerekayang Sebagian 34 persen dari mereka
thisview,wantingQueenElizabethII sawanganengene,kepenginRatuEliz- terlibat dalam polling ini berpenda- yangterlibatdalampollinginimemi-
tobeAustralia’slastmonarch. abethIIdadirajasingkeridheweana patdemikian,inginRatuElizabethII liki pandangan yang sama, yaitu
ningAustralia. menjadiRatuAustraliaterakhir. menginginkanRatuElizabethIImen-
jadiRatuAustraliaterakhir.
Javanese Thequalitiesthatdetermineasubcul- Kualitas sing nemtokake sawijin- Sifat-sifat yang menentukan subkul- Kualitas-kualitas sing menentukan
tureasdistinctmaybelinguistic,aes- ingcabangkabudayanmbokmenawa tursebagaiyangterpisahbisaberupa subkultur minangka distinct bisa
thetic,religious,political,sexual,geo- basa, estetika, sing ana gayutane linguistik,estetik,agama,politik,sek- ngandhut linguistik, estetik, agama,
graphical,oracombinationoffactors. karo agama, politik, seksual, ge- sual,geografis,ataukombinasifaktor- politik, seksual, geografis, utawa
ografis, utawa sawijining kombinasi faktor. gabunganfaktor-faktor.
sakafaktor-faktor.
Javanese NewKingdomancientEgyptiansmar- Krajan Anyar Mesir kuno nggumun Rakyat Kerajaan Baru dari Mesir Rakyat Kerajaan Baru dari Mesir
velled at their predecessors monu- marangmonumen-monumenleluhure, Kuno terpesona oleh monumen- Kuno terpesona oleh monumen-
ments, which were then well over a singnalikaikutetepapikluwihseka monumen pendahulunya, yang saat monumen pendahulunya, yang saat
thousandyearold. sewutaun. itusudahlebihdariseributahuntua. itusudahlebihdariseributahuntua.
Javanese The U.S. Corps of Engineers esti- Korps Insinyur AS ngira manawa Korps Insinyur Amerika Serikat Korps Insinyur Amerika Serikat
mated that 6 inches of rainfall could udan6incibisanembustanggulsing menghitungbahwahujan6incibisa menaksir bahwa hujan 6 inci bisa
breach the previously damaged lev- rusaksadurunge. merusakparityangsebelumnyarusak. merusak parit yang telah rusak se-
ees. belumnya.

718
Sundanese Althoughthreepeoplewereinsidethe Sanaostiluurangayadijerobumipas Walaupuntigaorangberadadidalam Walaupun ada tiga orang di dalam
housewhenthecarimpactedit,none mobilnanabrak,teuayaanucidera. rumahsaatmobilmenabraknya,tidak rumah saat mobil menabraknya, tak
ofthemwerehurt. adayangterluka. adayangterluka.
Sundanese 34percentofthoseinthepollshare 34 persen jalma dina polling di 34 persen dari mereka yang terlibat 34 persen dari mereka yang terli-
thisview,wantingQueenElizabethII gaduh pendapat ieu, nyaeta hoyong dalamsurveimemilikipandanganini, batdalamsurveimemilikipandangan
tobeAustralia’slastmonarch. RatuElizabethIIjantenmonarkispa- yaituinginRatuElizabethIImenjadi yangsama,yaituinginRatuElizabeth
mungkasdiAustralia. ratuterakhirAustralia. IImenjadiratuterakhirdiAustralia.
Sundanese Thequalitiesthatdetermineasubcul- Kualitas anu nangtukeun subkultur Sifat-sifatyangmenentukansubkultur Sifat-sifat nu nentukkeun subkultur
tureasdistinctmaybelinguistic,aes- salakubédanapangintenbasa,éstétis, sebagaiterpisahmungkinbersifatlin- salaku nu béda bisa jadi linguistik,
thetic,religious,political,sexual,geo- religius, politik, séks, géografis, guistik,estetika,agama,politik,sek- estetika, agama, politik, seksual, ge-
graphical,oracombinationoffactors. atanapikombinasifaktor. sual, geografis, atau kombinasi dari ografis, atawa kombinasi ti faktor-
faktor-faktortersebut. faktorieu.
Sundanese NewKingdomancientEgyptiansmar- Karajaan anyar urang Mesir kuno PararajaanyardinaEgyptkunonyo- Para raja anyar dina Egypt kuno
velled at their predecessors monu- takjub kana monumén paninggalan gog nara-nara jaman awal, anu dina terkagum-kagum kana nara-nara
ments, which were then well over a karuhunna, anu umurna langkung ti jamanayeunakira-kiraribuantaun. candi jaman awal, anu dina jaman
thousandyearold. sarebutaun. ayeunakira-kiraleuweungtaun.
Sundanese The U.S. Corps of Engineers esti- KorpsinsinyurA.Sngira-ngiracurah Korps Engineer AS diperkirakan Korps Engineer AS diperkirakan
mated that 6 inches of rainfall could hujan6incitiasanembustanggulanu bahwa6incihujanbisamerusakben- bahwa hujan sebesar 6 inci dapat
breach the previously damaged lev- samemehnageusruksak. tengyangsebelumnyasudahrusak. merusakbentengyangsudahrusakse-
ees. belumnya.
Table22: ExamplesofChatGPTtranslatedandpost-editedsentences.