|     | The                      | Internal   |     | State | of an LLM | Knows | When                  | It’s | Lying |     |     |
| --- | ------------------------ | ---------- | --- | ----- | --------- | ----- | --------------------- | ---- | ----- | --- | --- |
|     |                          | AmosAzaria |     |       |           |       | TomMitchell           |      |       |     |     |
|     | SchoolofComputerScience, |            |     |       |           |       | MachineLearningDept., |      |       |     |     |
ArielUniversity,Israel CarnegieMellonUniversity,Pittsburgh,PA
Abstract
Plutoisthe
WhileLargeLanguageModels(LLMs)have
| shown | exceptional | performance |     | in various |     |     |     |     |     |     |     |
| ----- | ----------- | ----------- | --- | ---------- | --- | --- | --- | --- | --- | --- | --- |
tasks,oneoftheirmostprominentdrawbacks
is generating inaccurate or false information second largest smallest only most
| withaconfidenttone. |     | Inthispaper,weprovide |     |     |     |     |     |     |     |     |     |
| ------------------- | --- | --------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
celestial
| evidencethattheLLM’sinternalstatecanbe |     |     |     |     |     |     |     |     | bodyinthe |     |     |
| -------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --------- | --- | --- |
used to reveal the truthfulness of statements. dwarfplanet solarsystem
|     |     |     |     |     |     |     | inoursolar |     | thathas |     |     |
| --- | --- | --- | --- | --- | --- | --- | ---------- | --- | ------- | --- | --- |
Thisincludesbothstatementsprovidedtothe
|     |     |     |     |     |     |     | system. |     | everbeen |     |     |
| --- | --- | --- | --- | --- | --- | --- | ------- | --- | -------- | --- | --- |
classified
LLM,andstatementsthattheLLMitselfgen-
asaplanet.
erates. Ourapproachistotrainaclassifierthat
outputstheprobabilitythatastatementistruth-
Figure1: Atreediagramthatdemonstrateshowgener-
| ful, based | on the | hidden | layer | activations | of  |     |     |     |     |     |     |
| ---------- | ------ | ------ | ----- | ----------- | --- | --- | --- | --- | --- | --- | --- |
atingwordsoneatatimeandcommittingtothemmay
theLLMasitreadsorgeneratesthestatement.
resultingeneratinginaccurateinformation.
| Experiments | demonstrate |     | that | given a | set of |     |     |     |     |     |     |
| ----------- | ----------- | --- | ---- | ------- | ------ | --- | --- | --- | --- | --- | --- |
testsentences,ofwhichhalfaretrueandhalf
false,ourtrainedclassifierachievesanaverage
ofconfidentbutincorrectinformation,maycause
| of 71% | to 83% | accuracy | labeling | which | sen- |     |     |     |     |     |     |
| ------ | ------ | -------- | -------- | ----- | ---- | --- | --- | --- | --- | --- | --- |
significantharm,aspeoplemayaccepttheLLMas
tencesaretrueversusfalse,dependingonthe
aknowledgeablesource,andfallforitsconfident
| LLM | base model. | Furthermore, |     | we explore |     |     |     |     |     |     |     |
| --- | ----------- | ------------ | --- | ---------- | --- | --- | --- | --- | --- | --- | --- |
therelationshipbetweenourclassifier’sperfor- and compelling language, even when providing
| manceandapproachesbasedontheprobability |     |     |     |     |     | falseinformation. |     |     |     |     |     |
| --------------------------------------- | --- | --- | --- | --- | --- | ----------------- | --- | --- | --- | --- | --- |
assignedtothesentencebytheLLM.Weshow We believe that in order to perform well, an
thatwhileLLM-assignedsentenceprobability
LLMmusthavesomeinternalnotionastowhether
| is related | to sentence       |     | truthfulness, | this     | prob-  |            |                |           |                     |           |     |
| ---------- | ----------------- | --- | ------------- | -------- | ------ | ---------- | -------------- | --------- | ------------------- | --------- | --- |
|            |                   |     |               |          |        | a sentence | is true        | or false, | as this information |           | is  |
| ability    | is also dependent |     | on            | sentence | length |            |                |           |                     |           |     |
|            |                   |     |               |          |        | required   | for generating | (or       | predicting)         | following |     |
andthefrequenciesofwordsinthesentence,
tokens. Forexample,consideranLLMgenerating
| resulting | in our | trained | classifier | providing | a   |     |     |     |     |     |     |
| --------- | ------ | ------- | ---------- | --------- | --- | --- | --- | --- | --- | --- | --- |
more reliable approach to detecting truthful- thefollowingfalseinformation“Thesunorbitsthe
ness,highlightingitspotentialtoenhancethe Earth." After stating this incorrect fact, the LLM
reliability of LLM-generated content and its ismorelikelytoattempttocorrectitselfbysaying
practicalapplicabilityinreal-worldscenarios.
|     |     |     |     |     |     | thatthisisamisconceptionfromthepast. |              |             |      | Butafter |        |
| --- | --- | --- | --- | --- | --- | ------------------------------------ | ------------ | ----------- | ---- | -------- | ------ |
|     |     |     |     |     |     | stating                              | a true fact, | for example | “The | Earth    | orbits |
1 Introduction
thesun,"itismorelikelytofocusonotherplanets
Large Language Models (LLMs) have recently thatorbitthesun. Therefore,wehypothesizethat
demonstratedremarkablesuccessinabroadrange the truth or falsehood of a statement should be
of tasks (Brown et al., 2020; Bommarito II and representedby,andthereforeextractablefrom,the
| Katz,2022;Driessetal.,2023;Bubecketal.,2023). |     |     |     |     |     | LLM’sinternalstate. |     |     |     |     |     |
| --------------------------------------------- | --- | --- | --- | --- | --- | ------------------- | --- | --- | --- | --- | --- |
However,whencomposingaresponse,LLMstend Interestingly, retrospectively “understanding”
to hallucinate facts and provide inaccurate infor- that a statement that an LLM has just generated
mation(Jietal.,2023). Furthermore,theyseemto isfalsedoesnotentailthattheLLMwillnotgener-
providethisincorrectinformationusingconfident ateitinthefirstplace. Weidentifythreereasonsfor
and compelling language. The combination of a suchbehavior. ThefirstreasonisthatanLLMgen-
broadbodyofknowledge,alongwiththeprovision eratesatokenatatime,andit“commits”toeach
967
FindingsoftheAssociationforComputationalLinguistics:EMNLP2023,pages967–976
December6-10,2023©2023AssociationforComputationalLinguistics

tokengenerated. Therefore,evenifmaximizingthe byanLLMistruthfulornot. Namely,webuilda
likelihoodofeachtokengiventheprevioustokens, classifierthatreceivesasinputtheactivationvalues
the overall likelihood of the complete statement ofthehiddenlayersofanLLM.Theclassifierde-
may be low. For example, consider a statement terminesforeachstatementgeneratedbytheLLM
about Pluto. The statement begins with the com- if it is true or false. Importantly, the classifier is
mon words "Pluto is the", then, since Pluto used trainedonout-of-distributiondata,whichallowsus
tobethesmallestplanettheword"smallest"may to focus specifically on whether the LLM has an
be a very plausible choice. Once the sentence is internalrepresentationofastatementbeingtrueor
"Pluto is the smallest", completing it correctly is false,regardlessofthestatement’stopic.
verychallenging,andwhenpromptedtocomplete
InordertotrainSAPLMAwecreatedadataset
| the sentence, |     | GPT-4 | (March | 23rd | version) | com- |         |           |            |     |        |           |      |
| ------------- | --- | ----- | ------ | ---- | -------- | ---- | ------- | --------- | ---------- | --- | ------ | --------- | ---- |
|               |     |       |        |      |          |      | of true | and false | statements |     | from 6 | different | top- |
pletes it incorrectly: “Pluto is the smallest dwarf ics. Each statement is fed to the LLM, and its
| planetinoursolarsystem.” |     |     |     | Infact,Plutoisthesec- |     |     |                                 |     |     |     |     |               |     |
| ------------------------ | --- | --- | --- | --------------------- | --- | --- | ------------------------------- | --- | --- | --- | --- | ------------- | --- |
|                          |     |     |     |                       |     |     | hiddenlayers’valuesarerecorded. |     |     |     |     | Theclassifier |     |
ondlargestdwarfplanetinoursolarsystem(after
|            |           |     |            |     |        |          | is then | trained | to predict | whether |     | a statement | is  |
| ---------- | --------- | --- | ---------- | --- | ------ | -------- | ------- | ------- | ---------- | ------- | --- | ----------- | --- |
| Eris). One | plausible |     | completion |     | of the | sentence |         |         |            |         |     |             |     |
trueorfalseonlybasedonthehiddenlayer’sval-
| correctly     | is “Pluto | is     | the smallest |          | celestial | body       |                   |      |             |                 |      |            |        |
| ------------- | --------- | ------ | ------------ | -------- | --------- | ---------- | ----------------- | ---- | ----------- | --------------- | ---- | ---------- | ------ |
|               |           |        |              |          |           |            | ues. Importantly, |      | our         | classifier      | is   | not tested | on     |
| in the solar  | system    | that   | has          | ever     | been      | classified |                   |      |             |                 |      |            |        |
|               |           |        |              |          |           |            | the topics        | it   | is trained, | but             | on a | held-out   | topic. |
| as a planet.” | (see      | Figure | 1).          | Consider | the       | follow-    |                   |      |             |                 |      |            |        |
|               |           |        |              |          |           |            | We believe        | that | this        | is an important |      | measure,   | as     |
ing additional example: “Tiztoutine is a town in it requires SAPLMA to extract the LLM’s inter-
| Africa | located | in the | republic | of  | Niger.” | Indeed, |             |        |      |          |     |             |     |
| ------ | ------- | ------ | -------- | --- | ------- | ------- | ----------- | ------ | ---- | -------- | --- | ----------- | --- |
|        |         |        |          |     |         |         | nal belief, | rather | than | learning | how | information |     |
TiztoutineisatowninAfrica,andmanycountries’
|     |     |     |     |     |     |     | mustbealignedtobeclassifiedastrue. |     |     |     |     | Weshow |     |
| --- | --- | --- | --- | --- | --- | --- | ---------------------------------- | --- | --- | --- | --- | ------ | --- |
namesinAfricabeginwith“therepublicof”. How- thatSAPLMA,whichleveragestheLLM’sinternal
| ever, Tiztoutine |     | is located |     | in Morocco, |     | which is |     |     |     |     |     |     |     |
| ---------------- | --- | ---------- | --- | ----------- | --- | -------- | --- | --- | --- | --- | --- | --- | --- |
states,resultsinabetterperformancethanprompt-
notarepublic,sooncetheLLMcommitsto“the
ingtheLLMtoexplicitlystatewhetherastatement
republicof”,itcannotcompletethesentenceusing
|     |     |     |     |     |     |     | istrueorfalse. |     | Specifically,SAPLMAreachesac- |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | -------------- | --- | ----------------------------- | --- | --- | --- | --- |
“Morocco",butcompletesitwith“Niger". Inaddi- curacylevelsofbetween60%to80%onspecific
tion,committingtoawordatatimemayleadthe
|     |     |     |     |     |     |     | topics, | while | few-shot | prompting |     | achieves | only |
| --- | --- | --- | --- | --- | --- | --- | ------- | ----- | -------- | --------- | --- | -------- | ---- |
LLMtoberequiredtocompleteasentencethatit
slightlyaboverandomperformance,withnomore
simplydoesnotknowhowtocomplete. Forexam- thana56%accuracylevel.
ple,whendescribingacity,itmaypredictthatthe
|            |        |             |     |               |             |          | Of course   |                 | there will | be some | relationship |     | be-     |
| ---------- | ------ | ----------- | --- | ------------- | ----------- | -------- | ----------- | --------------- | ---------- | ------- | ------------ | --- | ------- |
| next words | should | describe    |     | the city’s    | population. |          |             |                 |            |         |              |     |         |
|            |        |             |     |               |             |          | tween the   | truth/falsehood |            | of      | a sentence,  |     | and the |
| Therefore, | it     | may include |     | in a sentence |             | "Tiztou- |             |                 |            |         |              |     |         |
|            |        |             |     |               |             |          | probability | assigned        |            | to that | sentence     | by  | a well- |
tinehasapopulationof",butthepopulationsizeis
|     |     |     |     |     |     |     | trained | LLM. | But the | probability | assigned |     | by an |
| --- | --- | --- | --- | --- | --- | --- | ------- | ---- | ------- | ----------- | -------- | --- | ----- |
notpresentinthedataset,soitmustcompletethe
LLMtoagivenstatementdependsheavilyonthe
sentencewithapureguess.
frequencyofthetokensinthestatementaswellas
ThesecondreasonforanLLMtoprovidefalse
|             |     |         |        |       |     |         | its length. | Therefore, |     | sentence | probabilities |     | pro- |
| ----------- | --- | ------- | ------ | ----- | --- | ------- | ----------- | ---------- | --- | -------- | ------------- | --- | ---- |
| information | is  | that at | times, | there | may | be many |             |            |     |          |               |     |      |
videonlyaweaksignalofthetruth/falsehoodofthe
| ways to | complete | a sentence |     | correctly, |     | but fewer |           |                                |     |     |     |     |     |
| ------- | -------- | ---------- | --- | ---------- | --- | --------- | --------- | ------------------------------ | --- | --- | --- | --- | --- |
|         |          |            |     |            |     |           | sentence. | Atminimum,theymustbenormalized |     |     |     |     |     |
waystocompleteitincorrectly. Therefore,itmight tobecomeausefulsignaloftheveracityofastate-
| be that | a single | incorrect | completion |     | may | have a |     |     |     |     |     |     |     |
| ------- | -------- | --------- | ---------- | --- | --- | ------ | --- | --- | --- | --- | --- | --- | --- |
ment. Aswediscusslater,SAPLMAclassifications
| higher | likelihood | than | any | of the | correct | comple- |     |     |     |     |     |     |     |
| ------ | ---------- | ---- | --- | ------ | ------- | ------- | --- | --- | --- | --- | --- | --- | --- |
oftruth/falsehoodsignificantlyoutperformsimple
tions(whenconsideredseparately). sentenceprobability. Inonetestdescribedlaterin
Finally, since it is common for an LLM to not moredetail,weshowthatSAPLMAperformswell
usethemaximalprobabilityforthenextword,but onasetofLLM-generatedsentencesthatcontain
to sample according to the distribution over the 50%true,and50%falsestatements. Wefurtherdis-
words, it may sample words that result in false cusstherelationshipbetweenstatementprobability
| information. |     |     |     |     |     |     | andveracityinthediscussionsection. |     |     |     |     |     |     |
| ------------ | --- | --- | --- | --- | --- | --- | ---------------------------------- | --- | --- | --- | --- | --- | --- |
InthispaperwepresentourStatementAccuracy SAPLMAemploysasimpleandrelativelyshal-
Prediction,basedonLanguageModelActivations low feedforward neural network as its classifier,
(SAPLMA). SAPLMA is a simple yet powerful whichrequiresverylittlecomputationalpowerat
methodfordetectingwhetherastatementgenerated inference time. Therefore, it can be computed
968

alongside the LLM’s output. We propose for textsummarization. Theirbenchmarkisdeveloped
SAPLMA to supplement an LLM presenting in- bygatheringsummariesfromseveralsummariza-
formation to users. If SAPLMA detects that the tion methods and requested humans to annotate
LLM “believes” that a statement that it has just their errors. The authors analyze these anotation
generated is false, the LLM can mark it as such. andtheproportionofthedifferentfactualerrorof
ThiscouldraisehumantrustintheLLMresponses. the summarization methods. We note that most
Alternatively,theLLMmaymerelydeletethein- worksthatconsiderhallucinationdosowithrela-
correctstatementandgenerateanewoneinstead. tiontoagiveninput(e.g.,apassage)thatthemodel
|     |     |     |     |     |     |     | operateson. | Forexample,asummarizationmodel |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | ----------- | ------------------------------ | --- | --- | --- | --- |
Tosummarize,thecontributionofthispaperis
| twofold. |     |     |     |     |     |     | thatoutputsinformationthatdoesnotappearinthe |     |     |     |     |     |
| -------- | --- | --- | --- | --- | --- | --- | -------------------------------------------- | --- | --- | --- | --- | --- |
• The release of a dataset of true-false state- providedarticle,isconsideredhallucinateit,regard-
ments along with a method for generating lessiftheinformationisfactuallytrue. However,
inthisworkweconsideradifferentproblem—-the
suchinformation.
• Demonstrating that an LLM might “know” veracityoftheoutputofanLLM,withoutrespect
| when      | a statement |           | that it | has just | generated |     | toaspecificinput. |         |     |          |               |     |
| --------- | ----------- | --------- | ------- | -------- | --------- | --- | ----------------- | ------- | --- | -------- | ------------- | --- |
| is false, | and         | proposing | SAPLMA, |          | a method  |     |                   |         |     |          |               |     |
|           |             |           |         |          |           |     | Some              | methods | for | reducing | hallucination | as- |
forextractingthisinformation.
|     |     |     |     |     |     |     | sume that | the           | LLM is | a black | box       | (Peng et al., |
| --- | --- | --- | --- | --- | --- | --- | --------- | ------------- | ------ | ------- | --------- | ------------- |
|     |     |     |     |     |     |     | 2023).    | This approach |        | uses    | different | methods for   |
2 RelatedWork
promptingtheLLM,possiblybypostingmultiple
|                 |     |         |     |          |     |        | queries | for achieving |     | better | performance. | Some |
| --------------- | --- | ------- | --- | -------- | --- | ------ | ------- | ------------- | --- | ------ | ------------ | ---- |
| In this section | we  | provide | an  | overview | of  | previ- |         |               |     |        |              |      |
methodsthatcanbeusedfordetectingfalsestate-
ousresearchonLLMhallucination,accuracy,and
mentsmayincluderepeatedqueriesandmeasuring
| methods | for detecting |     | false information, |     | and | we  |     |     |     |     |     |     |
| ------- | ------------- | --- | ------------------ | --- | --- | --- | --- | --- | --- | --- | --- | --- |
discussdatasetsusedtothatend. thediscrepancyamongthem. Wenotethatinstead
ofaskingtheLLMtoanswerthesamequerymul-
| Many    | works have  | focused |     | on hallucination |     | in      |              |     |             |     |         |            |
| ------- | ----------- | ------- | --- | ---------------- | --- | ------- | ------------ | --- | ----------- | --- | ------- | ---------- |
|         |             |         |     |                  |     |         | tiple times, | it  | is possible | to  | request | the LLM to |
| machine | translation | (Dale   | et  | al., 2022;       | Ji  | et al., |              |     |             |     |         |            |
rephrasethequery(withoutchangingitsmeaning
| 2023). | For example, |     | Dale et | al. | (Dale | et al., |                 |     |         |     |             |           |
| ------ | ------------ | --- | ------- | --- | ----- | ------- | --------------- | --- | ------- | --- | ----------- | --------- |
|        |              |     |         |     |       |         | or any possible |     | answer) | and | then asking | it to an- |
2022)considerhallucinationsastranslationsthat
swereachrephrasedquestion.
aredetachedfromthesource,hencetheyproposea
methodthatevaluatesthepercentageofthesource OthermethodsfinetunetheLLM,usinghuman
contributiontoageneratedtranslation. Ifthiscon- feedback,reinforcementlearning,orboth(Bakker
tributionislow,theyassumethatthetranslationis et al., 2022; Ouyang et al., 2022). Ouyang et al.
detachedfromthesourceandisthusconsideredto proposeamethodtoimproveLLM-generatedcon-
behallucinated. Theirmethodimprovesdetection tentusingreinforcementlearningfromhumanfeed-
| accuracyhallucinations. |     |     | Theauthorsalsopropose |     |     |     |             |          |     |         |                |     |
| ----------------------- | --- | --- | --------------------- | --- | --- | --- | ----------- | -------- | --- | ------- | -------------- | --- |
|                         |     |     |                       |     |     |     | back. Their | approach |     | focuses | on fine-tuning | the |
tousemultilingualembeddings,andcomparethe LLMwitharewardmodelbasedonhumanjudg-
similarity between the embeddings of the source ments,aimingtoencouragethegenerationofbet-
sentenceandthetargetsentence. Ifthissimilarity tercontent. However,finetuning,ingeneral,may
islow,thetargetsentenceisconsideredtobehal- causeamodeltonotperformaswellonothertasks
lucinated. Theauthorsshowthatthelattermethod (Kirkpatricketal.,2017). Inthispaper,wetakean
worksbetter. However,theirapproachisverydif- intermediateapproach,thatis,weassumeaccessto
ferentthanours,aswedonotassumeanypairof
themodelparameters,butdonotfine-tuneormod-
sourceandtargetsentences. Inaddition,whilewe ifythem. Anotherapproachthatcanbeappliedto
alsousetheinternalstatesofthemodel,wedoso our settings is presented by (Burns et al., 2022),
byusingthehiddenstatestodescriminatebetween named Contrast-Consistent Search (CCS). How-
statements that the LLM “believes” are true and ever, CCS requires rephrasing a statement into a
those that are false. Furtheremore, we focus on question,evaluatingtheLLMontwodifferentver-
detectingfalsestatementsratherthanhallucination, sionoftheprompt,andrequirestrainingdatafrom
asdefinedbytheirwork.
|     |     |     |     |     |     |     | thesamedataset(topic)asthetestset. |     |     |     |     | Theselimi- |
| --- | --- | --- | --- | --- | --- | --- | ---------------------------------- | --- | --- | --- | --- | ---------- |
Other works have focused on hallucination in tationsrenderitunsuitableforrunninginpractice
textsummarization(Pagnonietal.,2021). Pagnoni on statements generated by an LLM. In addition,
etal. proposeabenchmarkforfactualitymetricsof CCSincreasestheaccuracybyonlyapproximately
969

4%overthe0-shotLLMquery,whileourapproach Forthefirst5topics,weusedthefollowingmethod
Weusedareliablesource1
demonstratesanearly20%increaseoverthe0-shot tocomposethedataset.
| LLM |     |     |     | that included | a table | with several | properties | for |
| --- | --- | --- | --- | ------------- | ------- | ------------ | ---------- | --- |
Adatasetcommonlyusedfortrainingandfine- eachinstance. Forexample,forthe“chemicalel-
tuning LLMs is the Wizard-of-Wikipedia (Dinan ements" we used a table that included, for each
|              |                                  |     |     | element, | its name, atomic | number, | symbol, | stan- |
| ------------ | -------------------------------- | --- | --- | -------- | ---------------- | ------- | ------- | ----- |
| etal.,2018). | TheWizard-of-Wikipediadatasetin- |     |     |          |                  |         |         |       |
cludes interactions between a human apprentice dardstate,groupblock,andauniqueproperty(e.g.,
andahumanwizard. Thehumanwizardreceives Hydrogen, 1, H, Gas, Nonmetal, the most abun-
|     |     |     |     | dantelementintheuniverse). |     | Foreachelementwe |     |     |
| --- | --- | --- | --- | -------------------------- | --- | ---------------- | --- | --- |
relevantWikipediaarticles,whichshouldbeused
to select a relevant sentence and compose the re- composedtruestatementusingtheelementname
sponse. The goal is to replace the wizard with a andoneofitsproperties(e.g.,“Theatomicnumber
learned agent (such as an LLM). Another highly ofHydrogenis1”). Then,werandomlyselecteda
relevant dataset is FEVER (Thorne et al., 2018, differentrowforcomposingafalsestatement(e.g.,
2019). TheFEVERdatasetisdesignedfordevel- “The atomic number of Hydrogen is 34”). If the
oping models that receive as input a claim and a valueinthedifferentrowisidenticaltothevaluein
thecurrentrow,weresampleadifferentrowuntil
passage,andmustdeterminewhetherthepassage
supportstheclaim,refutesit,ordoesnotprovide we obtain a value that is different. This process
enoughinformationtosupportorrefuteit. While was repeated for the all topics except the “Scien-
theFEVERdatasetishighlyrelevant, itdoesnot tific Facts”. For the “Scientific Facts” topic, we
provide simple sentence that are clearly true or asked ChatGPT (Feb 13 version) to provide “sci-
falseindependentlyofaprovidedpassage. Inad- entific facts that arewell known tohumans” (e.g.
dition, the FEVER dataset is not partitioned into “Theskyisoftencloudywhenit’sgoingtorain”).
WethenaskedChatGPTtoprovidetheoppositeof
differenttopicsasthetrue-falsedatasetprovidedin
thispaper. each statement such that it becomes a false state-
In conclusion, while several approaches have ment(e.g.,“Theskyisoftenclearwhenit’sgoing
been proposed to address the problem of halluci- to rain”). The statements provided by ChatGPT
|     |     |     |     | were manually | curated, | and verified |     | by two hu- |
| --- | --- | --- | --- | ------------- | -------- | ------------ | --- | ---------- |
nationandinaccuracyinautomaticallygenerated
content,ourworkisuniqueinitsfocusonutilizing manannotators. Theclassificationof48factswere
the LLM’s hidden layer activations to determine questionedbyatleastoneoftheannotators;these
|                                   |     |     |           | facts were | removed | from the dataset. |     | The true- |
| --------------------------------- | --- | --- | --------- | ---------- | ------- | ----------------- | --- | --------- |
| theveracityofgeneratedstatements. |     |     | Ourmethod |            |         |                   |     |           |
offersthepotentialformoregeneralapplicabilityin falsedatasetcomprises6,084sentences,including
real-worldscenarios,operatingalongsideanLLM, 1,458sentencesfor“Cities",876for“Inventions",
without the need for fine-tuning or task-specific 930for“ChemicalElements",1,008for“Animals",
|     |     |     |     | 1,200 for | “Companies", | and 612 | for | “Scientific |
| --- | --- | --- | --- | --------- | ------------ | ------- | --- | ----------- |
modifications.
Facts". Thefollowingaresomeexamplesoftrue
| 3 TheTrue-FalseDataset |     |     |     | statementsfromthedataset: |                            |     |     |     |
| ---------------------- | --- | --- | --- | ------------------------- | -------------------------- | --- | --- | --- |
|                        |     |     |     | • Cities:                 | “OranjestadisacityinAruba” |     |     |     |
Theworkpresentedinthispaperrequiresadataset • Inventions: “Grace Hopper invented the
| oftrueandfalsestatements. |     | Thesestatementsmust |     |     |     |     |     |     |
| ------------------------- | --- | ------------------- | --- | --- | --- | --- | --- | --- |
COBOLprogramminglanguage”
haveacleartrueorfalselabel,andmustbebased
|     |     |     |     | • Animals: | “Thellamahasadietofherbivore” |     |     |     |
| --- | --- | --- | --- | ---------- | ----------------------------- | --- | --- | --- |
oninformationpresentintheLLM’strainingdata. • Companies: “Meta Platforms has headquar-
Furthermore,sinceourapproachintendstoreveal
tersinUnitedStates”
thatthehiddenstatesofanLLMhaveanotionof
|             |            |               |              | • Scientific | Facts: | “The Earth’s | tides | are pri- |
| ----------- | ---------- | ------------- | ------------ | ------------ | ------ | ------------ | ----- | -------- |
| a statement | being true | or false, the | dataset must |              |        |              |       |          |
marilycausedbythegravitationalpullofthe
coverseveraldisjointtopics,suchthataclassifier
moon”
| can be trained                   | on the | LLM’s activations | of some        |               |          |          |     |              |
| -------------------------------- | ------ | ----------------- | -------------- | ------------- | -------- | -------- | --- | ------------ |
|                                  |        |                   |                | The following | are some | examples | of  | false state- |
| topicswhilebeingtestedonanother. |        |                   | Unfortunately, |               |          |          |     |              |
mentsfromthedataset:
| we could | not find any | such dataset | and therefore, |     |     |     |     |     |
| -------- | ------------ | ------------ | -------------- | --- | --- | --- | --- | --- |
composethetrue-falsedataset.
|     |     |     |     | 1Cities: | Downloadedfromsimplemaps. |     | Inventions: | Ob- |
| --- | --- | --- | --- | -------- | ------------------------- | --- | ----------- | --- |
Ourtrue-falsedatasetcoversthefollowingtop- tainedfromWikipedialistofinventors.ChemicalElements:
Downloadedfrompubchemncbinlmnihgovperiodic-table.
ics: “Cities",“Inventions",“ChemicalElements",
Animals:Obtainedfromkidsnationalgeographics.Compa-
“Animals", “Companies", and “Scientific Facts". nies:ForbesGlobal2000List2022:TheTop200.
970

• Chemical Elements: “Indium is in the Lan- aretrueandwhichit“believes”arefalse,inagen-
| thanidegroup” |     |     |     | eralsetting,andnotspecificallywithrespecttothe |     |     |     |
| ------------- | --- | --- | --- | ---------------------------------------------- | --- | --- | --- |
• Animals: “The whale has a long, tubular topicbeingtested. Toobtainmorereliableresults,
snout,largeears,andapowerfuldiggingabil- we train each classifier three times with different
itytolocateandconsumetermitesandants.” initialrandomweights. Thisprocessisrepeatedfor
• ScientificFacts: “Icesinksinwaterduetoits eachtopic,andwereporttheaccuracymeanover
| higherdensity”                              |                      |                  |        | thesethreeruns. |     |     |     |
| ------------------------------------------- | -------------------- | ---------------- | ------ | --------------- | --- | --- | --- |
| Other candidates                            | for topics           | to be added      | to the |                 |     |     |     |
| datasetincludesports,celebrities,andmovies. |                      |                  | The    | 5 Results       |     |     |     |
| true-false                                  | dataset is available | at: azariaa.com/ |        |                 |     |     |     |
WecomparetheperformanceofSAPLMAagainst
Content/Datasets/true-false-dataset.zip.
|          |     |     |     | three different                               | baselines. | The first | is BERT, for |
| -------- | --- | --- | --- | --------------------------------------------- | ---------- | --------- | ------------ |
| 4 SAPLMA |     |     |     | whichwetrainaclassifier(withanidenticalarchi- |            |           |              |
tecturetotheoneusedbySAPLMA)ontheBERT
Inthissection,wepresentourStatementAccuracy embeddingsofeachsentence. Oursecondbaseline
Prediction,basedonLanguageModelActivations is a few shot-learner using OPT-6.7b. This base-
| (SAPLMA), | a method designed | to determine | the |     |     |     |     |
| --------- | ----------------- | ------------ | --- | --- | --- | --- | --- |
lineisanattempttorevealwhethertheLLMitself
truthfulness of statements generated by an LLM “knows”whetherastatementistrueorfalse. Un-
usingthevaluesinitshiddenlayers. Ourgeneral fortunately,anyattemptstoexplicitlypromptthe
hypothesisisthatthevaluesinthehiddenlayersof LLMina‘zero-shot”mannertodeterminewhether
anLLMcontaininformationonwhethertheLLM astatementistrueorfalsecompletelyfailedwith
“believes”thatastatementistrueorfalse. However, accuracylevelsnotgoingbeyond52%. Therefore,
itisunclearwhichlayershouldbethebestcandi- weuseafewshot-queryinstead, whichprovided
| dateforretainingsuchinformation. |     | Whilethelast |     |              |              |          |            |
| -------------------------------- | --- | ------------ | --- | ------------ | ------------ | -------- | ---------- |
|                                  |     |              |     | the LLM with | truth values | from the | same topic |
hidden layer should contain such information, it it is being tested on. Note that this is very dif-
isprimarilyfocusedongeneratingthenexttoken. ferent from our methodology, but was necessary
Conversely,layersclosertotheinputarelikelyfo- forobtainingsomeresults. Namely,weprovided
cusedonextractinglower-levelinformationfrom fewstatementsalongwiththeground-truthlabel,
theinput. Therefore,weuseseveralhiddenlayers and then the statement in question. We recorded
ascandidates. WeusetwodifferentLLMs: Face- theprobabilitythattheLLMassignedtothetoken
bookOPT-6.7b(Zhangetal.,2022)andLLAMA2-
|     |     |     |     | “true”andtothetoken“false”. |     | Unfortunately,the |     |
| --- | --- | --- | --- | --------------------------- | --- | ----------------- | --- |
7b (Roumeliotis et al., 2023); both composed of LLMhadatendencytoassignhighervaluestothe
32layers. ForeachLLM,wecomposefivediffer- “true”token;therefore,wedividedtheprobability
entmodels,eachusingactivationsfromadifferent assigned to the “true” token by the one assigned
layer. Namely, we use the last hidden layer, the to the “false” token. Finally, we considered the
28thlayer(whichisthe4thbeforelast),the24th LLM’s prediction “true” if the value was greater
layer(whichisthe8thbeforelast),the20thlayer thantheaverage,and“false”otherwise. Wetested
(whichisthe12thbeforelast),andthemiddlelayer a3-shotanda5-shotversion. Thethirdbaseline,
(whichisthe16thlayer). Wenotethateachlayer givenastatement‘X’,wemeasuretheprobabilities
iscomposedof4096hiddenunits. (usingOPT-6.7)ofthesentences“ItistruethatX”,
SAPLMA’s classifier employs a feedforward and“ItisfalsethatX”,andpickthehigherproba-
neuralnetwork,featuringthreehiddenlayerswith bility(consideringonlytheprobabilitiesforX,not
decreasingnumbersofhiddenunits(256,128,64), theaddedwords). Thisnormalizesthelengthand
| allutilizingReLUactivations. |                        | Thefinallayerisa |     | frequencyfactors. |            |               |             |
| ---------------------------- | ---------------------- | ---------------- | --- | ----------------- | ---------- | ------------- | ----------- |
| sigmoidoutput.               | WeusetheAdamoptimizer. |                  | We  |                   |            |               |             |
|                              |                        |                  |     | Table 1           | and Figure | 2 present the | accuracy of |
donotfine-tuneanyofthesehyper-parametersfor all the models tested using the OPT-6.7b LLM,
thistask. Theclassifieristrainedfor5epochs. foreachofthetopics,alongwiththeaverageaccu-
Foreachtopicinthetrue-falsedataset,wetrain racy. Asdepictedbythetableandfigure,SAPLMA
the classifier using only the activation values ob- clearlyoutperformsBERTandFew-shotlearning,
tainedfromallothertopicsandtestitsaccuracyon with BERT, 3-shot, and 5-shot learning achiev-
thecurrenttopic. Thisway,theclassifierisrequired ingonlyslightlyabovearandomguess(0.50). It
todeterminewhichsentencestheLLM“believes” canalsobeobservedthatSAPLMAforOPT-6.7b
971

Model Cities Invent. Elements Animals Comp. Facts Average Model Cities Invent. Elements Animals Comp. Facts Average
last-layer 0.7796 0.5696 0.5760 0.6022 0.6925 0.6498 0.6449 last-layer 0.7574 0.6735 0.6814 0.7338 0.6736 0.7444 0.7107
28th-layer 0.7732 0.5761 0.5907 0.5777 0.7247 0.6618 0.6507 28th-layer 0.8146 0.7207 0.6767 0.7249 0.6894 0.7662 0.7321
24th-layer 0.7963 0.6712 0.6211 0.5800 0.7758 0.6868 0.6886 24th-layer 0.8722 0.7816 0.6849 0.7394 0.7094 0.7858 0.7622
| 20th-layer 0.8125 | 0.7268 | 0.6197 0.6058 | 0.8122 0.6819 | 0.7098 |            |               |        |        |               |        |
| ----------------- | ------ | ------------- | ------------- | ------ | ---------- | ------------- | ------ | ------ | ------------- | ------ |
|                   |        |               |               |        | 20th-layer | 0.8820 0.8459 | 0.6950 | 0.7758 | 0.8319 0.8053 | 0.8060 |
middle-layer 0.7435 0.6400 0.5645 0.5800 0.7570 0.6237 0.6515 16th-layer 0.9223 0.8938 0.6939 0.7774 0.8658 0.8254 0.8298
| BERT 0.5357   | 0.5537 | 0.5645 0.5228 | 0.5533 0.5302 | 0.5434 |         |                                             |     |     |     |     |
| ------------- | ------ | ------------- | ------------- | ------ | ------- | ------------------------------------------- | --- | --- | --- | --- |
| 3-shot 0.5410 | 0.4799 | 0.5685 0.5650 | 0.5538 0.5164 | 0.5374 |         |                                             |     |     |     |     |
|               |        |               |               |        | Table2: | Accuracyclassifyingtruthfulnessofexternally |     |     |     |     |
| 5-shot 0.5416 | 0.4799 | 0.5676 0.5643 | 0.5540 0.5148 | 0.5370 |         |                                             |     |     |     |     |
It-is-true 0.523 0.5068 0.5688 0.4851 0.6883 0.584 0.5593 generatedsentencesusingSAPLMAwithLLAMA2-7b.
Thetableshowsaccuracyofallthemodelstestedfor
Table1: Accuracyclassifyingtruthfulnessofexternally
eachofthetopics,andtheaverageaccuracy.
| generatedsentencesduringreading. |     |     | Thetableshows |     |     |     |     |     |     |     |
| -------------------------------- | --- | --- | ------------- | --- | --- | --- | --- | --- | --- | --- |
accuracyofallthemodelstestedforeachofthetopics,
andaverageaccuracyusingOPT-6.7bastheLLM.
|     |     |     |     |     | As for | the differences |     | between | the topics, | we  |
| --- | --- | --- | --- | --- | ------ | --------------- | --- | ------- | ----------- | --- |
believethatthesevaluesdependverymuchonthe
1
trainingdataoftheLLM.Thatis,webelievethat
| 0.9          |     |     |     |     | thedatausedfortrainingOPT-6.7bandLLAMA2-      |     |     |     |     |     |
| ------------ | --- | --- | --- | --- | --------------------------------------------- | --- | --- | --- | --- | --- |
| ycaruccA 0.8 |     |     |     |     | 7bincludesinformationorstoriesaboutmanycities |     |     |     |     |     |
andcompanies,andnotasmuchonchemicalele-
0.7
|     |     |     |     |     | ments and | animals | (other | than the | very | common |
| --- | --- | --- | --- | --- | --------- | ------- | ------ | -------- | ---- | ------ |
0.6
|     |     |     |     |     | ones). Therefore,weconjecturethatisthereason |     |     |     |     |     |
| --- | --- | --- | --- | --- | -------------------------------------------- | --- | --- | --- | --- | --- |
0.5 Comp. Average SAPLMA achieves high accuracy for the “cities”
| Cities | Invent. Elements | Animals | Facts |     |     |     |     |     |     |     |
| ------ | ---------------- | ------- | ----- | --- | --- | --- | --- | --- | --- | --- |
topic(whiletrainedonalltherest)andthe“com-
SAPLMA It-is-true BERT 3-shot 5-shot panies” topic, but achieves much lower accuracy
Figure 2: A bar-chart comparing the accuracy of whentestedonthe“animals”and“elements”top-
| SAPLMA (20th-layer), |     | BERT, 3-shot, | 5-shot, | and It- | ics. |     |     |     |     |     |
| -------------------- | --- | ------------- | ------- | ------- | ---- | --- | --- | --- | --- | --- |
is-trueonthe6topics,andtheaverage. SAPLMAcon- In addition to the topics from the true-false
sistentlyoutperformsothermodelsacrossallcategories. dataset,wealsocreatedaseconddatasetofstate-
Sincethedataisbalanced,arandomclassifiershould
mentsgeneratedbytheLLMitself(theOPT-6.7b
obtainanaccuracyof0.5.
|     |     |     |     |     | model). | For generating |     | statements, | we  | provided |
| --- | --- | --- | --- | --- | ------- | -------------- | --- | ----------- | --- | -------- |
atruestatementnotpresentinthedataset,andal-
seemstoworkbestwhenusingthe20thlayer(out lowedtheLLMtogenerateafollowingstatement.
of 32). Recall that each model was trained three We first filtered out any statements that were not
factualstatements(e.g.,“I’mnotfamiliarwiththe
times. Wenotethatthestandarddeviationbetween
the accuracy among the different runs was very Japaneseversionsofthegames.”). Allstatements
small; therefore, the differences in performance weregeneratedusingthemostprobablenextword
betweenthedifferentlayersseemconsistent. How- at each step, i.e., we did not use sampling. This
|     |     |     |     |     | resultedin245labeledstatements. |     |     |     | Thestatements |     |
| --- | --- | --- | --- | --- | ------------------------------- | --- | --- | --- | ------------- | --- |
ever,theoptimallayertobeusedforSAPLMAis
verylikelytodependontheLLM. werefact-checkedandmanuallylabeledbythree
We note that the average training accuracy for humanjudgesbasedonweb-searches. Thehuman
|     |     |     |     |     | judges had | a very | high | average | observed | agree- |
| --- | --- | --- | --- | --- | ---------- | ------ | ---- | ------- | -------- | ------ |
SAPLMA(usingOPT-6.7b’s20thlayer)is86.4%.
Webelievethatthisrelativelyhighvaluemayindi- mentof97.82%,andanaverageCohen’sKappaof
cateonceagainthattheveracityofastatementisin- 0.9566. Themajoritydeterminedtheground-truth
herittotheLLM.Todemonstratethis,werunatest labelforeachstatement. 48.6%ofthestatements
werelabeledastrue,resultinginabalanceddataset.
wherethetrue/falselabelsarerandomlypermuted.
Theaverageaccuracyontherandomtrainingdata Eachofthemodelswastrained14timesusing
isonly62.5%. Thisindicatesthatourmodeldoes the same classifier described in Section 4. The
not have the capacity to completely over-fit the modelsweretrainedontheentiretrue-falsedataset
trainingdata,andthus,mustexploitstructureand (i.e.,alltopics,butnotthegeneratedsentences)and
| patternsthatappearinthedata. |     |     |     |     | testedonthegeneratedsentences. |     |     |     |     |     |
| ---------------------------- | --- | --- | --- | --- | ------------------------------ | --- | --- | --- | --- | --- |
Additionally,Table2presentstheperformance Table3presentstheaverageaccuracyofallmod-
of SAPLMA using LLAMA2-7b. As expected, els on the sentences generated by the LLM. As
SAPLMAusingLLAMA2-7bachievesmuchbet- anticipated, SAPLMA (using OPT-6.7b) clearly
ter performance. Interestingly, for LLAMA2-7b, outperformsthebaselines,whichappeartobeen-
themiddlelayerperformsbest. tirelyineffectualinthistask,achievinganaccuracy
972

Model Accuracy AUC number of positive predictions would match the
numberofnegativepredictions,whichmatchesthe
| last-layer | 0.6187 | 0.7587 |     |     |     |     |
| ---------- | ------ | ------ | --- | --- | --- | --- |
distributioninofthedata.
| 28th-layer   | 0.6362 | 0.7614 |              |              |        |          |
| ------------ | ------ | ------ | ------------ | ------------ | ------ | -------- |
| 24th-layer   | 0.6134 | 0.7435 | Model        | AvgThreshold |        | Accuracy |
| 20th-layer   | 0.6029 | 0.7182 |              |              |        |          |
|              |        |        | last-layer   |              | 0.8687 | 0.7052   |
| middle-layer | 0.5566 | 0.6610 |              |              |        |          |
|              |        |        | 28th-layer   |              | 0.8838 | 0.7134   |
| BERT         | 0.5115 | 0.5989 | 24th-layer   |              | 0.8801 | 0.6988   |
| 3-shot       | 0.5041 | 0.4845 | 20th-layer   |              | 0.9063 | 0.6587   |
| 5-shot       | 0.5125 | 0.4822 |              |              |        |          |
|              |        |        | middle-layer |              | 0.8123 | 0.650    |
Table3: Accuracyclassifyingtruthfulnessofsentences BERT 0.9403 0.5705
generatedbytheLLM(OPT-6.7b)itself.
Table4: Accuracyclassifyingtruthfulnessofsentences
|     |     |     | generatedbytheLLMitself. |     | UnlikethedatainTable |     |
| --- | --- | --- | ------------------------ | --- | -------------------- | --- |
3,whereathresholdof0.5ontheclassifieroutputwas
| near50%. However,theaccuracyofSAPLMAon |     |     |                  |           |         |                       |
| -------------------------------------- | --- | --- | ---------------- | --------- | ------- | --------------------- |
|                                        |     |     | used to classify | sentences | as true | or false, in this ta- |
thesesentencesisnotaspromisingastheaccuracy bletheresultswereobtainedbyestimatingtheoptimal
achievedwhentestedonsomeofthetopicsinthe
thresholdfromaheld-outvalidationdataset(30%of
| true-false dataset | (i.e., the cities | and companies). | theoriginaltest-set). |     |     |     |
| ------------------ | ----------------- | --------------- | --------------------- | --- | --- | --- |
SinceweexpectedtheLLMtogeneratesentences
thataremorealignedwiththedataitwastrained Table4presentstheaccuracyofallmodelswhen
on,wedidexpectSAPLMA’sperformanceonthe usingtheoptimalthresholdfromthevalidationset.
generatedsentencestobeclosertoitsperformance Clearly, SAPLMA performs better with a higher
ontopicssuchascitiesandcompanies,whichare threshold. Thissomewhatconfirmsourassumption
likelyalignedwiththedatatheLLMwastrained thatthetruthvalueofthesentencesgeneratedby
on. However,theremaybealsoacounter-effectin theLLMismoresubjectivethanthosethatappear
play: the sentences in the true-false dataset were in the true-false dataset. We note that also the
mostly generated using a specific pattern (except BERT embeddings perform better with a higher
thescientificfactstopic),suchthateachsentenceis threshold. Theuseofahigherthresholdcanalso
clearlyeithertrueorfalse. However,thesentences bejustifiedbythenotionthatitisbettertodelete
generated by the LLM where much more open, ortomarkasunsureasentencethatisactuallytrue,
and their truth value may be less clearly defined thantopromotefalseinformation.
(despitebeingagreeduponbythehumanjudges). Anotherinterestingobservationisthatthe20th-
Forexample,oneofthesentencesclassifiedbyall layer no longer performs best for the statements
humanjudgesasfalseis“Limagetsanaverageof generatedbytheLLM,butthe28thlayerseemsto
1 hour of sunshine per day.” However, this sen- performbest. Thisissomewhatperplexingandwe
tenceistrueduringthewinter. Anotherexampleis donothaveagoodguessastowhythismightbe
“Brinkisariver,”whichwasalsoclassifiedasfalse happening. Nevertheless,westressthatthediffer-
byallthreehumanjudges;however,brinkrefersto encesbetweentheaccuracylevelsofthe28th-layer
riverbank(butisnotanameofaspecificriver,and andtheothersarestatisticallysignificant(usinga
doesnotmeanriver). Indeed,SAPLMAclassified two-tailedstudentt-test;p < 0.05). Infuturework
approximately70%ofthesentencesastrue,andthe we will consider fusing multiple layers together,
AUCvaluesseemmorepromising. Thismayhint and using the intermediate activation values out-
thatanysentencethatseemsplausibleisclassified puttedbytheLLMforallthewordsappearingin
as true. Therefore, we evaluate the models using the statement (rather than using only the LLM’s
30% of the generated sentences for determining outputforthefinalword).
whichthresholdtouse,i.e.,anypredictionabove We also ran the statements generated by the
the threshold is considered true. Importantly, we OPT6.7bmodelonGPT-4(March23rdversion),
donotusethisvalidationsetforanyothergoal. We promptingittodeterminewhethereachstatement
testthemodelsontheremaining70%ofthegen- was true or false. Specifically, we provided the
eratedsentences. Wedonotevaluatethefewshot followingprompt“Copythefollowingstatements
modelsagain,asourevaluationguaranteedthatthe and for each statement write true if it is true and
973

false if it is false:”, and fed it 30 statements at a bility. However,whileSAPLMAstillclassifiesthe
time. Itachievedanaccuracylevelof84.4%,anda statement“KevinDurantisbasketeer”asfalse,it’s
Cohen’sKappaagreementlevelof0.6883withthe stillmuchmoreconfidentthatKevinDurantisnot
truelabel. a baseball player, in contrast to the probabilities.
|              |     |     |     |     |     |     | Since the                                     | statement | “Kevin |     | Duarnt | is basketball |     |
| ------------ | --- | --- | --- | --- | --- | --- | --------------------------------------------- | --------- | ------ | --- | ------ | ------------- | --- |
| 6 Discussion |     |     |     |     |     |     | player”hasatypo,itsprobabilityisextremelylow, |           |        |     |        |               |     |
butSAPLMAstillclassifiesthestatementastrue.
Inthisworkweexplicitlydonotconsidermodels
“JenniferAnistonisafemaleperson”isanim-
that were trained or fine-tuned on data from the plicittruth,afactthatisuniversallyacknowledged
| sametopicofthetest-set. |     |     | Thisisparticularlyim- |     |     |     |         |         |       |            |         |       |       |
| ----------------------- | --- | --- | --------------------- | --- | --- | --- | ------- | ------- | ----- | ---------- | ------- | ----- | ----- |
|                         |     |     |                       |     |     |     | without | needing | to be | explicitly | stated; | thus, | it is |
portantforthesentencesgeneratedbytheLLM,as
unlikelytobementionedintheLLM’strainingdata.
trainingonaheld-outsetfromthemwouldallow
Therefore,itsprobabilityisverylow—muchlower
theclassifiertolearnwhichtypeofsentencesgen-
than“JenniferAnistonisnotanactress”—despite
| erated by  | the   | LLM are | generally   |     | true, and | which  |        |          |        |     |        |               |     |
| ---------- | ----- | ------- | ----------- | --- | --------- | ------ | ------ | -------- | ------ | --- | ------ | ------------- | --- |
|            |       |         |             |     |           |        | having | the same | number | of  | words. | Nevertheless, |     |
| are false. | While | this    | information |     | may be    | useful |        |          |        |     |        |               |     |
SAPLMAclassifiesitcorrectly,albeitnotwithvery
| in practice, | and | its usage | is  | likely | to yield | much | highconfidence. |     |     |     |     |     |     |
| ------------ | --- | --------- | --- | ------ | -------- | ---- | --------------- | --- | --- | --- | --- | --- | --- |
higheraccuracy,itdeviatesfromthispaper’sfocus.
Whileweshowthattheprobabilitiescannotbe
| We note | that | the | probability | of  | the entire | sen- |     |     |     |     |     |     |     |
| ------- | ---- | --- | ----------- | --- | ---------- | ---- | --- | --- | --- | --- | --- | --- | --- |
usedalonetodeterminetheveracityofastatement,
| tence (computed |     | by  | multiplying |     | the conditional |     |     |     |     |     |     |     |     |
| --------------- | --- | --- | ----------- | --- | --------------- | --- | --- | --- | --- | --- | --- | --- | --- |
theyarenotuselessanddoconveyimportantinfor-
probabilities of each word, given the previous mation. Therefore,infutureworkwewillconsider
words)cannotbedirectlytranslatedtoatruthvalue
|     |     |     |     |     |     |     | providing | SAPLMA | with | the | probabilities |     | of the |
| --- | --- | --- | --- | --- | --- | --- | --------- | ------ | ---- | --- | ------------- | --- | ------ |
forthesentence,asmanywordsaremorecommon
generatedwords;however,thisinformationmaybe
thanothers. Therefore,whilesentenceprobabilities redundant,especiallyifSAPLMAusestheinterme-
| may be | useful | to determine |     | which | of two | similar |     |     |     |     |     |     |     |
| ------ | ------ | ------------ | --- | ----- | ------ | ------- | --- | --- | --- | --- | --- | --- | --- |
diateactivationvaluesforallthewordsappearing
sentencesistrue,theycannotbeusedaloneforthe
inthestatement.
generalpurposeofdeterminingthetruthfulnessof
| agivensentence. |     |     |     |     |     |     | Statement |     |     |     | Label Probability |     | SAPLMA |
| --------------- | --- | --- | --- | --- | --- | --- | --------- | --- | --- | --- | ----------------- | --- | ------ |
(28th-layer)
InTable5wecomparetheprobabilityassigned
|     |     |     |     |     |     |     | H2Oiswater,whichisessentialforhumans |     |     |     | True 6.64E-16 |     | 0.9032 |
| --- | --- | --- | --- | --- | --- | --- | ------------------------------------ | --- | --- | --- | ------------- | --- | ------ |
bytheLLMandthesigmoidoutputfromSAPLMA Humansdon’tneedwater False 2.65E-10 0.0282
|     |     |     |     |     |     |     | Thesunishot,anditradiatesitsheattoEarth |     |     |     | True 1.01E-17 |     | 0.9620 |
| --- | --- | --- | --- | --- | --- | --- | --------------------------------------- | --- | --- | --- | ------------- | --- | ------ |
on14statements,whichdonotappearinthetrue-
|     |     |     |     |     |     |     | ThesunprotectsEarthfromheat |     |     |     | False 2.03E-14 |     | 0.3751 |
| --- | --- | --- | --- | --- | --- | --- | --------------------------- | --- | --- | --- | -------------- | --- | ------ |
false dataset. We use the 28-layer, as it proved TheEarthisflat False 5.27E-07 0.0342
|            |      |     |                |     |           |     | Theworldisroundandrotates  |     |     |     | True 2.96E-11  |     | 0.6191 |
| ---------- | ---- | --- | -------------- | --- | --------- | --- | -------------------------- | --- | --- | --- | -------------- | --- | ------ |
| to perform | best | on  | the statements |     | generated | by  |                            |     |     |     |                |     |        |
|            |      |     |                |     |           |     | TheEarthisflatlikeapancake |     |     |     | False 3.88E-10 |     | 0.0097 |
the LLM, but we note that other layers provide KevinDurantisabasketballplayer True 2.89E-10 0.9883
|     |     |     |     |     |     |     | KevinDurantisabaseballplayer |     |     |     | False 4.56E-12 |     | 0.0001 |
| --- | --- | --- | --- | --- | --- | --- | ---------------------------- | --- | --- | --- | -------------- | --- | ------ |
very similar results on this set of statements. As KevinDurantisabasketeer True 5.78E-16 0.0469
depicted by the table, the probabilities provided KevinDuarntisabasketballplayer True 1.52E-21 0.7105
|     |     |     |     |     |     |     | JenniferAnistonisanactress |     |     |     | True 1.88E-10 |     | 0.9985 |
| --- | --- | --- | --- | --- | --- | --- | -------------------------- | --- | --- | --- | ------------- | --- | ------ |
by the LLM are highly susceptible to the syntax, JenniferAnistonisnotanactress False 1.14E-11 0.0831
|           |       |       |         |             |     |         | JenniferAnistonisafemaleperson |     |     |     | True 2.78E-14  |     | 0.6433 |
| --------- | ----- | ----- | ------- | ----------- | --- | ------- | ------------------------------ | --- | --- | --- | -------------- | --- | ------ |
| i.e., the | exact | words | and the | statement’s |     | length. |                                |     |     |     |                |     |        |
|           |       |       |         |             |     |         | HarryPotterisreal              |     |     |     | False 9.46E-09 |     | 0.0016 |
Thefirsttwosetsofexamplesinthetableillustrate HarryPotterisfictional True 1.53E-09 0.9256
|     |     |     |     |     |     |     | HarryPotterisanimaginaryfigure |     |     |     | True 6.31E-14 |     | 0.8354 |
| --- | --- | --- | --- | --- | --- | --- | ------------------------------ | --- | --- | --- | ------------- | --- | ------ |
howsentencelengthhighlyaffectstheprobabilities,
but not SPLMA. In the following examples the Table 5: Comparison of the probability assigned by
|     |     |     |     |     |     |     | the LLM | and | the sigmoid | output | from | SAPLMA’s |     |
| --- | --- | --- | --- | --- | --- | --- | ------- | --- | ----------- | ------ | ---- | -------- | --- |
falsestatementsarenotnecessarilyshorterthanthe
truestatements,yettheprobabilitiesremainhighly 28th layer (using OPT-6.7b), color-coded for clarity.
|             |       |       |           |     |          |     | SAPLMA’s | values | are | much better | aligned |     | with the |
| ----------- | ----- | ----- | --------- | --- | -------- | --- | -------- | ------ | --- | ----------- | ------- | --- | -------- |
| unreliable, | while | SPLMA | generally |     | succeeds | in  |          |        |     |             |         |     |          |
truthvalue.
makingaccuratepredictions.
Thestatement“TheEarthisflat”aswellas“The
Earthisflatlikeapancake”probablyappearseveral
|     |     |     |     |     |     |     | 7 Conclusions&FutureWork |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | ------------------------ | --- | --- | --- | --- | --- | --- |
timesintheLLM’strainingdata,therefore,ithasa
relativelyhighprobability;however,SAPLMAis In this paper, we tackle a fundamental problem
notbaffledbyitandisalmostcertainthatbothsen- associated with LLMs, i.e., the generation of in-
tencesarefalse. Abasketeerisararewordmeaning correctandfalseinformation. Wehaveintroduced
a basketball player. It seems that the LLM is not SAPLMA,amethodthatleveragesthehiddenlayer
familiarwiththephraseandassignsitalowproba- activations of an LLM to predict the truthfulness
974

of generated statements. We demonstrated that andYi,2021). Theoverallsystemcanbenefitfrom
SAPLMAoutperformsfew-shotpromptinginde- multipleoutcomes,suchthatiftheLLMisnotpos-
tectingwhetherastatementistrueorfalse,achiev- itivewhetherthestatementistrueorfalse,itcanbe
ing accuracy levels between 60% to 80% on spe- markedfortheusertotreatwithcaution. However,
cific topics when using OPT-6.7b, and between if a statement is classified as false, the LLM can
70% to 90% when using LLAMA2-7b. This is a deleteitandgenerateadifferentstatementinstead.
significant improvement over the maximum 56% Toavoidregeneratingthesamestatementagain,the
accuracylevelachievedbyfew-shotprompting(for probabilityofsamplingthewordsthatappearinthe
| OPT-6.7b). |     |     |     |     |     |     | currentstatementshouldbeadjusteddownward. |     |     |     |     |     |     |
| ---------- | --- | --- | --- | --- | --- | --- | ----------------------------------------- | --- | --- | --- | --- | --- | --- |
Our findings suggest that LLMs possess an in- OurworkwasonlytestedinEnglish. However,
ternalrepresentationofstatementaccuracy,which webelievethatamultilingualLLMcanbetrained
canbeharnessedbySAPLMAtofilteroutincor- ononelanguageandappliedonstatementsinan-
|                  |      |        |                |         |     |           | other language. |     | We  | will | test this hypothesis |     | in  |
| ---------------- | ---- | ------ | -------------- | ------- | --- | --------- | --------------- | --- | --- | ---- | -------------------- | --- | --- |
| rect information |      | before | it             | reaches | the | user, and |                 |     |     |      |                      |     |     |
| furthermore      | that | this   | representation |         | of  | accuracy  | futurework.     |     |     |      |                      |     |     |
is very different from the probability assigned to In our work, we collected the activation val-
the sentence by the LLM. Using SAPLMA as a ueswheneachsentencewasgeneratedseparately.
supplement to LLMs may increase human trust However,inpractice,inanLLMgeneratinglonger
in the generated responses and mitigate the risks responsestheactivationvaluesdevelopovertime,
associatedwiththedisseminationoffalseinforma- sotheymayprocessbothcorrectandincorrectin-
tion. Furthermore,wehavereleasedthetrue-false formation. Therefore,theactivationvalueswould
datasetandproposedamethodforgeneratingsuch need to be decoupled so that they can be tested
data. This dataset, along with our methodology, whetherthemostrecentstatementwastrueorfalse.
providesvaluableresourcesforfutureresearchin Oneapproachmightbetosubtractthevalueofthe
improvingLLMs’abilitiestogenerateaccurateand activations obtained after the previous statement
reliableinformation. fromthecurrentactivationvalues(adiscretederiva-
In future work we intend to apply our method tive). Clearly,trainingmustbeperformedusingthe
sameapproach.
tolargerLLMs,andrunexperimentswithhumans,
suchthatacontrolgroupwillinteractwithanunfil-
9 EthicalImpact
teredLLM,andtheexperimentalgroupwillinter-
actwithasystemthataugmentsSAPLMAandan
|         |      |     |             |     |             |       | One of | the primary |     | ethical | concerns | of LLMs | is  |
| ------- | ---- | --- | ----------- | --- | ----------- | ----- | ------ | ----------- | --- | ------- | -------- | ------- | --- |
| LLM. We | hope | to  | demonstrate |     | that humans | trust |        |             |     |         |          |         |     |
thegenerationoffalseinformation;yet,webelieve
| and better | understand |     | the | limitations | of  | a system |     |     |     |     |     |     |     |
| ---------- | ---------- | --- | --- | ----------- | --- | -------- | --- | --- | --- | --- | --- | --- | --- |
thatSAPLMAcouldpotentiallyreducethisissue.
thatisabletoreviewitselfandmarkstatementsthat
Ontheotherhand,itisimportanttoacknowledge
| itisunsureabout. |     | Wealsointendtostudyhowthe |     |     |     |     |              |         |         |     |               |     |      |
| ---------------- | --- | ------------------------- | --- | --- | --- | --- | ------------ | ------- | ------- | --- | ------------- | --- | ---- |
|                  |     |                           |     |     |     |     | that certain | ethical | issues, |     | such as bias, | may | per- |
activationsdevelopovertimeasadditionalwords
sist,potentiallybeingtransferredfromtheLLMto
aregenerated,andconsidermultilingualinput.
|     |     |     |     |     |     |     | SAPLMA. | Specifically, |     | if  | the LLM | exhibits | bias |
| --- | --- | --- | --- | --- | --- | --- | ------- | ------------- | --- | --- | ------- | -------- | ---- |
towardscertainethnicgroups,SAPLMAmaylike-
8 Limitations
|     |     |     |     |     |     |     | wise classify |     | statements | as  | true or false | based | on  |
| --- | --- | --- | --- | --- | --- | --- | ------------- | --- | ---------- | --- | ------------- | ----- | --- |
theseinheritedbiasesfromtheoriginalLLM.Nev-
| This paper | focuses |     | on detecting |     | whether | a state- |     |     |     |     |     |     |     |
| ---------- | ------- | --- | ------------ | --- | ------- | -------- | --- | --- | --- | --- | --- | --- | --- |
ertheless,itmaybepossibletoadapttheapproach
| mentistrueorfalse. |     |     | However,inpractice,itmay |     |     |     |     |     |     |     |     |     |     |
| ------------------ | --- | --- | ------------------------ | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
presentedinthispapertobiasmitigation.
bemorebeneficialtodetectiftheLLMispositive
| that a statement |     | is  | correct | or if | it is unsure. | The |     |     |     |     |     |     |     |
| ---------------- | --- | --- | ------- | ----- | ------------- | --- | --- | --- | --- | --- | --- | --- | --- |
10 Acknowledgments
mostsimpleadjustmenttotheproposedmethodin
thispaperistolifttherequiredthresholdforclassi- Thisworkwassupported,inpart,bytheMinistry
| fyingastatementastrueabove0.5; |     |     |     |     | however, | the |     |     |     |     |     |     |     |
| ------------------------------ | --- | --- | --- | --- | -------- | --- | --- | --- | --- | --- | --- | --- | --- |
ofScienceandTechnology,Israel,andbytheIsrael
exactvaluewouldrequiresomeformofcalibration InnovationAuthority.
| ofthemodel(Bellaetal.,2010). |     |     |     |     | Anotheroption |     |     |     |     |     |     |     |     |
| ---------------------------- | --- | --- | --- | --- | ------------- | --- | --- | --- | --- | --- | --- | --- | --- |
istousemultipleclassifiersandtorequireall(or
| avastmajorityof)classifierstooutput“true”,for |     |     |     |     |                |     | References |         |        |           |        |          |     |
| --------------------------------------------- | --- | --- | --- | --- | -------------- | --- | ---------- | ------- | ------ | --------- | ------ | -------- | --- |
| thestatementtobeconsideredtrue.               |     |     |     |     | Alternatively, |     |            |         |        |           |        |          |     |
|                                               |     |     |     |     |                |     | Michiel    | Bakker, | Martin | Chadwick, | Hannah | Sheahan, |     |
dropoutlayerscanbeusedforthesamegoal(Chen Michael Tessler, Lucy Campbell-Gillingham, Jan
975

Balaguer, Nat McAleese, Amelia Glaese, John JamesKirkpatrick,RazvanPascanu,NeilRabinowitz,
Aslanides,MattBotvinick,etal.2022. Fine-tuning JoelVeness,GuillaumeDesjardins,AndreiARusu,
languagemodelstofindagreementamonghumans Kieran Milan, John Quan, Tiago Ramalho, Ag-
AdvancesinNeuralInfor-
withdiversepreferences. nieszka Grabska-Barwinska, et al. 2017. Over-
mationProcessingSystems,35:38176–38189. coming catastrophic forgetting in neural networks.
|                                                  |     |     |     |     |               |     | Proceedings        | of  | the national | academy | of sciences, |     |
| ------------------------------------------------ | --- | --- | --- | --- | ------------- | --- | ------------------ | --- | ------------ | ------- | ------------ | --- |
| AntonioBella,CèsarFerri,JoséHernández-Orallo,and |     |     |     |     |               |     | 114(13):3521–3526. |     |              |         |              |     |
| MaríaJoséRamírez-Quintana.2010.                  |     |     |     |     | Calibrationof |     |                    |     |              |         |              |     |
LongOuyang,JeffreyWu,XuJiang,DiogoAlmeida,
| machinelearningmodels. |     |     | InHandbookofResearch |     |     |     |     |     |     |     |     |     |
| ---------------------- | --- | --- | -------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
CarrollWainwright,PamelaMishkin,ChongZhang,
| onMachineLearningApplicationsandTrends: |     |     |     |     |     | Al- |     |     |     |     |     |     |
| --------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
SandhiniAgarwal,KatarinaSlama,AlexRay,etal.
gorithms,Methods,andTechniques,pages128–146.
| IGIGlobal. |     |     |     |     |     |     | 2022. Training |       | languagemodelsto |          | followinstruc- |        |
| ---------- | --- | --- | --- | --- | --- | --- | -------------- | ----- | ---------------- | -------- | -------------- | ------ |
|            |     |     |     |     |     |     | tions with     | human | feedback.        | Advances | in             | Neural |
InformationProcessingSystems,35:27730–27744.
| Michael | Bommarito | II  | and Daniel |     | Martin         | Katz. |                   |     |          |               |     |       |
| ------- | --------- | --- | ---------- | --- | -------------- | ----- | ----------------- | --- | -------- | ------------- | --- | ----- |
| 2022.   | Gpt takes | the | bar exam.  |     | arXiv preprint |       |                   |     |          |               |     |       |
|         |           |     |            |     |                |       | Artidoro Pagnoni, |     | Vidhisha | Balachandran, | and | Yulia |
arXiv:2212.14402.
|            |          |     |            |        |         |     | Tsvetkov.2021.     |     | Understandingfactualityinabstrac- |        |             |     |
| ---------- | -------- | --- | ---------- | ------ | ------- | --- | ------------------ | --- | --------------------------------- | ------ | ----------- | --- |
|            |          |     |            |        |         |     | tive summarization |     | with                              | frank: | A benchmark | for |
| Tom Brown, | Benjamin |     | Mann, Nick | Ryder, | Melanie |     |                    |     |                                   |        |             |     |
|            |          |     |            |        |         |     | factualitymetrics. |     | arXivpreprintarXiv:2104.13346.    |        |             |     |
Subbiah,JaredDKaplan,PrafullaDhariwal,Arvind
Neelakantan,PranavShyam,GirishSastry,Amanda
BaolinPeng,MichelGalley,PengchengHe,HaoCheng,
| Askell,etal.2020. |     | Languagemodelsarefew-shot |     |     |     |     |     |     |     |     |     |     |
| ----------------- | --- | ------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
YujiaXie,YuHu,QiuyuanHuang,LarsLiden,Zhou
learners. Advancesinneuralinformationprocessing Yu,WeizhuChen,etal.2023. Checkyourfactsand
systems,33:1877–1901. try again: Improving large language models with
|           |         |       |                 |     |       |     | externalknowledgeandautomatedfeedback. |     |     |     |     | arXiv |
| --------- | ------- | ----- | --------------- | --- | ----- | --- | -------------------------------------- | --- | --- | --- | --- | ----- |
| Sébastien | Bubeck, | Varun | Chandrasekaran, |     | Ronen | El- |                                        |     |     |     |     |       |
preprintarXiv:2302.12813.
| dan, Johannes |     | Gehrke, | Eric | Horvitz, | Ece Kamar, |     |     |     |     |     |     |     |
| ------------- | --- | ------- | ---- | -------- | ---------- | --- | --- | --- | --- | --- | --- | --- |
Peter Lee, Yin Tat Lee, Yuanzhi Li, Scott Lund- KonstantinosIRoumeliotis,NikolaosDTselikas,and
berg,etal.2023. Sparksofartificialgeneralintelli- Dimitrios K Nasiopoulos. 2023. Llama 2: Early
gence: Earlyexperimentswithgpt-4. arXivpreprint adopters’utilizationofmeta’snewopen-sourcepre-
| arXiv:2303.12712. |     |     |     |     |     |     | trainedmodel. |     |         |          |          |     |
| ----------------- | --- | --- | --- | --- | --- | --- | ------------- | --- | ------- | -------- | -------- | --- |
|                   |     |     |     |     |     |     | James Thorne, |     | Andreas | Vlachos, | Christos |     |
CollinBurns,HaotianYe,DanKlein,andJacobStein-
|        |                   |         |              |           |                |         | Christodoulopoulos, |             | and     | Arpit | Mittal.         | 2018. |
| ------ | ----------------- | ------- | ------------ | --------- | -------------- | ------- | ------------------- | ----------- | ------- | ----- | --------------- | ----- |
| hardt. | 2022. Discovering |         | latent       | knowledge |                | in lan- |                     |             |         |       |                 |       |
|        |                   |         |              |           |                |         | Fever: a            | large-scale | dataset | for   | fact extraction | and   |
| guage  | models            | without | supervision. |           | arXiv preprint |         |                     |             |         |       |                 |       |
arXiv:2212.03827. verification. arXivpreprintarXiv:1803.05355.
|                              |     |     |     |                |     |     | James Thorne, | Andreas | Vlachos, |     | Oana Cocarascu, |     |
| ---------------------------- | --- | --- | --- | -------------- | --- | --- | ------------- | ------- | -------- | --- | --------------- | --- |
| YuanyuanChenandZhangYi.2021. |     |     |     | Adaptivesparse |     |     |               |         |          |     |                 |     |
ChristosChristodoulopoulos,andArpitMittal.2019.
| dropout:    | Learning  | the | certainty       | and | uncertainty | in  |                        |     |     |                        |     |     |
| ----------- | --------- | --- | --------------- | --- | ----------- | --- | ---------------------- | --- | --- | ---------------------- | --- | --- |
|             |           |     |                 |     |             |     | Thefever2.0sharedtask. |     |     | InProceedingsoftheSec- |     |     |
| deep neural | networks. |     | Neurocomputing, |     | 450:354–    |     |                        |     |     |                        |     |     |
ondWorkshoponFactExtractionandVERification
| 361. |     |     |     |     |     |     | (FEVER),pages1–6. |     |     |     |     |     |
| ---- | --- | --- | --- | --- | --- | --- | ----------------- | --- | --- | --- | --- | --- |
David Dale, Elena Voita, Loïc Barrault, and Marta R Susan Zhang, Stephen Roller, Naman Goyal, Mikel
| Costa-jussà.2022. |     | Detectingandmitigatinghalluci- |     |     |     |     |     |     |     |     |     |     |
| ----------------- | --- | ------------------------------ | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Artetxe,MoyaChen,ShuohuiChen,ChristopherDe-
nationsinmachinetranslation: Modelinternalwork- wan,MonaDiab,XianLi,XiVictoriaLin,etal.2022.
ings alone do well, sentence similarity even better. Opt: Openpre-trainedtransformerlanguagemodels.
arXivpreprintarXiv:2212.08597. arXivpreprintarXiv:2205.01068.
| Emily Dinan,                         | Stephen                        | Roller,           | Kurt | Shuster, | Angela         |     |     |     |     |     |     |     |
| ------------------------------------ | ------------------------------ | ----------------- | ---- | -------- | -------------- | --- | --- | --- | --- | --- | --- | --- |
| Fan,MichaelAuli,andJasonWeston.2018. |                                |                   |      |          | Wizard         |     |     |     |     |     |     |     |
| of wikipedia:                        |                                | Knowledge-powered |      |          | conversational |     |     |     |     |     |     |     |
| agents.                              | arXivpreprintarXiv:1811.01241. |                   |      |          |                |     |     |     |     |     |     |     |
DannyDriess,FeiXia,MehdiSMSajjadi,CoreyLynch,
AakankshaChowdhery,BrianIchter,AyzaanWahid,
| Jonathan | Tompson,                       | Quan                         | Vuong, | Tianhe | Yu, | et al. |     |     |     |     |     |     |
| -------- | ------------------------------ | ---------------------------- | ------ | ------ | --- | ------ | --- | --- | --- | --- | --- | --- |
| 2023.    | Palm-e:                        | Anembodiedmultimodallanguage |        |        |     |        |     |     |     |     |     |     |
| model.   | arXivpreprintarXiv:2303.03378. |                              |        |        |     |        |     |     |     |     |     |     |
ZiweiJi,NayeonLee,RitaFrieske,TiezhengYu,Dan
| Su, Yan                            | Xu, | Etsuko | Ishii, Ye | Jin              | Bang, Andrea |     |     |     |     |     |     |     |
| ---------------------------------- | --- | ------ | --------- | ---------------- | ------------ | --- | --- | --- | --- | --- | --- | --- |
| Madotto,andPascaleFung.2023.       |     |        |           | Surveyofhalluci- |              |     |     |     |     |     |     |     |
| nationinnaturallanguagegeneration. |     |        |           |                  | ACMComput-   |     |     |     |     |     |     |     |
ingSurveys,55(12):1–38.
976