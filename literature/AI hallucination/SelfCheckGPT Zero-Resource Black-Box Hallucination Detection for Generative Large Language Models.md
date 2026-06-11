SELFCHECKGPT: Zero-Resource Black-Box Hallucination Detection
|     |     | for Generative |     | Large | Language |     | Models |     |     |     |     |     |
| --- | --- | -------------- | --- | ----- | -------- | --- | ------ | --- | --- | --- | --- | --- |
PotsaweeManakul,AdianLiusie,MarkJ.F.Gales
ALTAInstitute,DepartmentofEngineering,UniversityofCambridge
|     | pm574@cam.ac.uk, |     |     | al826@cam.ac.uk, |     | mjfg@eng.cam.ac.uk |     |     |     |     |     |     |
| --- | ---------------- | --- | --- | ---------------- | --- | ------------------ | --- | --- | --- | --- | --- | --- |
Abstract
Stochastically-generated responses
|            |       |          |        |        |            | LLM |     | sample1                 |     | sampleN                 |     |     |
| ---------- | ----- | -------- | ------ | ------ | ---------- | --- | --- | ----------------------- | --- | ----------------------- | --- | --- |
| Generative | Large | Language | Models | (LLMs) |            |     |     |                         |     |                         |     |     |
|            |       |          |        |        | e.g. GPT-3 |     |     | Giuseppe Mariani was an |     | Giuseppe Mariani was an |     |     |
suchasGPT-3arecapableofgeneratinghighly Italian painter, sculptor, Italian violinist,
|     |     |     |     |     |     |     |     | and engraver. He was |     | ... pedagogue and |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | -------------------- | --- | ----------------- | --- | --- |
fluent responses to a wide variety of user born in Naples, Italy, in composer. He was born
|          |          |          |       |         |     |           |     | 1882, and died in Paris, |     | in Pavia, Italy, on 4 June |     |     |
| -------- | -------- | -------- | ----- | ------- | --- | --------- | --- | ------------------------ | --- | -------------------------- | --- | --- |
|          |          |          |       |         |     | N samples |     |                          |     | 1836. [truncated]          |     |     |
| prompts. | However, | LLMs are | known | to hal- |     |           |     | France, in 1944.         |     |                            |     |     |
[truncated]
lucinatefactsandmakenon-factualstatements
| whichcanunderminetrustintheiroutput. |     |     |     | Ex- |     |     |     | LLM |     |     |     |     |
| ------------------------------------ | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Giuseppe Mariani was
| istingfact-checkingapproacheseitherrequire |     |     |     |     | an Italian professional |     |     |     |     |     |     |     |
| ------------------------------------------ | --- | --- | --- | --- | ----------------------- | --- | --- | --- | --- | --- | --- | --- |
footballer who played
access to the output probability distribution as a forward. He was Does {sample1} Does {sampleN}
|     |     |     |     |     |     |     |     | support {sentence}? |     | ... support {sentence}? |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ------------------- | --- | ----------------------- | --- | --- |
born in Milan, Italy. He
(whichmaynotbeavailableforsystemssuch died in Rome, Italy. Answer: [Yes/No] Answer: [Yes/No]
[truncated]
asChatGPT)orexternaldatabasesthatarein-
|     |     |     |     |     | L L | M 's  p a s s a g | e   |     | ... | ... |     |     |
| --- | --- | --- | --- | --- | --- | ----------------- | --- | --- | --- | --- | --- | --- |
terfacedviaseparate,oftencomplex,modules. to  b e  e v a lu a t e d  at No Yes No
| Inthiswork,wepropose"SelfCheckGPT",a |     |     |     |     | sentence-level  |     |     |     |     |     |     |     |
| ------------------------------------ | --- | --- | --- | --- | --------------- | --- | --- | --- | --- | --- | --- | --- |
SelfCheckGPT Score
simple sampling-based approach that can be (e.g. how often is the sentence supported by the samples)
usedtofact-checktheresponsesofblack-box
models in a zero-resource fashion, i.e. with- Figure1:SelfCheckGPTwithPrompt.EachLLM-generated
|                        |     |                    |     |     | sentence | is compared |             | against   | stochastically |              | generated | re-    |
| ---------------------- | --- | ------------------ | --- | --- | -------- | ----------- | ----------- | --------- | -------------- | ------------ | --------- | ------ |
| outanexternaldatabase. |     | SelfCheckGPTlever- |     |     |          |             |             |           |                |              |           |        |
|                        |     |                    |     |     | sponses  | with        | no external | database. |                | A comparison |           | method |
agesthesimpleideathatifanLLMhasknowl-
canbe,forexample,throughLLMpromptingasshownabove.
| edge of a | given | concept, sampled | responses |     |     |     |     |     |     |     |     |     |
| --------- | ----- | ---------------- | --------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
arelikelytobesimilarandcontainconsistent
facts. However,forhallucinatedfacts,stochas- tools to draft reports, virtual assistants and sum-
ticallysampledresponsesarelikelytodiverge
|     |     |     |     |     | marization |     | systems. | Despite |     | the convincing |     | and |
| --- | --- | --- | --- | --- | ---------- | --- | -------- | ------- | --- | -------------- | --- | --- |
andcontradictoneanother. Weinvestigatethis realisticnatureofLLM-generatedtexts,agrowing
approachbyusingGPT-3togeneratepassages
|     |     |     |     |     | concern | with | LLMs | is their | tendency |     | to  | halluci- |
| --- | --- | --- | --- | --- | ------- | ---- | ---- | -------- | -------- | --- | --- | -------- |
aboutindividualsfromtheWikiBiodataset,and
|     |     |     |     |     | natefacts. |     | Ithasbeenwidelyobservedthatmod- |     |     |     |     |     |
| --- | --- | --- | --- | --- | ---------- | --- | ------------------------------- | --- | --- | --- | --- | --- |
manuallyannotatethefactualityofthegener-
atedpassages. WedemonstratethatSelfCheck- elscanconfidentlygeneratefictitiousinformation,
|         |                                   |     |     |     | and worryingly |     | there | are | few, | if any, | existing | ap- |
| ------- | --------------------------------- | --- | --- | --- | -------------- | --- | ----- | --- | ---- | ------- | -------- | --- |
| GPTcan: | i)detectnon-factualandfactualsen- |     |     |     |                |     |       |     |      |         |          |     |
tences;andii)rankpassagesintermsoffactu- proachestosuitablyidentifyLLMhallucinations.
ality.Wecompareourapproachtoseveralbase- Apossibleapproachofhallucinationdetection
linesandshowthatourapproachhasconsider- istoleverageexistingintrinsicuncertaintymetrics
ablyhigherAUC-PRscoresinsentence-level
todeterminethepartsoftheoutputsequencethat
hallucinationdetectionandhighercorrelation
thesystemisleastcertainof(Yuanetal.,2021;Fu
| scores in | passage-level | factuality | assessment |     |     |     |     |     |     |     |     |     |
| --------- | ------------- | ---------- | ---------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
comparedtogrey-boxmethods.1 et al., 2023). However, uncertainty metrics such
|     |     |     |     |     | as token | probability |     | or entropy |     | require | access | to  |
| --- | --- | --- | --- | --- | -------- | ----------- | --- | ---------- | --- | ------- | ------ | --- |
1 Introduction token-level probability distributions, information
|                |        |        |      |          | which | may | not be | available | to  | users | for example |     |
| -------------- | ------ | ------ | ---- | -------- | ----- | --- | ------ | --------- | --- | ----- | ----------- | --- |
| Large Language | Models | (LLMs) | such | as GPT-3 |       |     |        |           |     |       |             |     |
whensystemsareaccessedthroughlimitedexter-
(Brownetal.,2020)andPaLM(Chowdheryetal.,
|     |     |     |     |     | nal APIs. |     | An alternate |     | approach | is  | to leverage |     |
| --- | --- | --- | --- | --- | --------- | --- | ------------ | --- | -------- | --- | ----------- | --- |
2022)arecapableofgeneratingfluentandrealistic
fact-verificationapproaches,whereevidenceisre-
| responsestoavarietyofuserprompts. |     |     |     | Theyhave |     |     |     |     |     |     |     |     |
| --------------------------------- | --- | --- | --- | -------- | --- | --- | --- | --- | --- | --- | --- | --- |
trievedfromanexternaldatabasetoassesstheve-
beenusedinmanyapplicationssuchasautomatic
|     |     |     |     |     | racity | of a | claim | (Thorne | et al., | 2018; | Guo | et al., |
| --- | --- | --- | --- | --- | ------ | ---- | ----- | ------- | ------- | ----- | --- | ------- |
2022). However,factscanonlybeassessedrelative
1Codeanddatasetcanbefoundontheprojectpageat
https://github.com/potsawee/selfcheckgpt. totheknowledgepresentinthedatabase. Addition-
9004
Proceedingsofthe2023ConferenceonEmpiricalMethodsinNaturalLanguageProcessing,pages9004–9017
December6-10,2023©2023AssociationforComputationalLinguistics

ally,hallucinationsareobservedoverawiderange internalstatesoftheLLM,whichmaynotbeavail-
oftasksbeyondpurefactverification(Kryscinski ablethroughAPIcalls,andrequireslabelleddata
etal.,2020;Maynezetal.,2020). forsupervisedtraining. Anotherrecentapproach
In this paper, we propose SelfCheckGPT, a isself-evaluation(Kadavathetal.,2022),wherean
sampling-basedapproachthatcandetectwhether LLM is prompted to evaluate its previous predic-
responsesgeneratedbyLLMsarehallucinatedor tion, e.g., topredicttheprobabilitythatitsgener-
factual. Tothebestofourknowledge,SelfCheck- atedresponse/answeristrue.
| GPT is    | the first | work | to analyze | model | halluci- |       |                                        |     |     |     |     |     |     |
| --------- | --------- | ---- | ---------- | ----- | -------- | ----- | -------------------------------------- | --- | --- | --- | --- | --- | --- |
|           |           |      |            |       |          |       | 2.2 SequenceLevelUncertaintyEstimation |     |     |     |     |     |     |
| nation of | general   | LLM  | responses, | and   | is the   | first |                                        |     |     |     |     |     |     |
zero-resourcehallucinationdetectionsolutionthat
|                                 |     |     |     |     |             |     | Token probabilities |                  | have | been | used     | as an    | indica- |
| ------------------------------- | --- | --- | --- | --- | ----------- | --- | ------------------- | ---------------- | ---- | ---- | -------- | -------- | ------- |
| canbeappliedtoblack-boxsystems. |     |     |     |     | Themotivat- |     |                     |                  |      |      |          |          |         |
|                                 |     |     |     |     |             |     | tion of             | model certainty. |      | For  | example, | OpenAI’s |         |
ing idea of SelfCheckGPT is that when an LLM GPT-3webinterfaceallowsuserstodisplaytoken
hasbeentrainedonagivenconcept,thesampledre-
probabilities(asshowninFigure2),andfurtherun-
sponsesarelikelytobesimilarandcontainconsis-
certaintyestimationapproachesbasedonaleatoric
tentfacts. However,forhallucinatedfacts,stochas- and epistemic uncertainty have been studied for
ticallysampledresponsesarelikelytodivergeand autoregressivegeneration(XiaoandWang,2021;
| maycontradictoneanother. |     |     |     | Bysamplingmultiple |     |     |         |            |        |               |     |     |        |
| ------------------------ | --- | --- | --- | ------------------ | --- | --- | ------- | ---------- | ------ | ------------- | --- | --- | ------ |
|                          |     |     |     |                    |     |     | Malinin | and Gales, | 2021). | Additionally, |     |     | condi- |
responsesfromanLLM,onecanmeasureinforma-
|     |     |     |     |     |     |     | tional language |     | model | scores | have | been | used to |
| --- | --- | --- | --- | --- | --- | --- | --------------- | --- | ----- | ------ | ---- | ---- | ------- |
tion consistency between the different responses evaluatepropertiesoftexts(Yuanetal.,2021;Fu
anddetermineifstatementsarefactualorhalluci-
|              |     |              |     |                |     |      | et al., 2023). | Recently, |     | semantic | uncertainty |     | has |
| ------------ | --- | ------------ | --- | -------------- | --- | ---- | -------------- | --------- | --- | -------- | ----------- | --- | --- |
| nated. Since |     | SelfCheckGPT |     | only leverages |     | sam- |                |           |     |          |             |     |     |
beenproposedtoaddressuncertaintyinfree-form
pledresponses,ithastheaddedbenefitthatitcan generation tasks where probabilities are attached
| be used | for black-box |     | models, | and | it requires | no  |     |     |     |     |     |     |     |
| ------- | ------------- | --- | ------- | --- | ----------- | --- | --- | --- | --- | --- | --- | --- | --- |
toconceptsinsteadoftokens(Kuhnetal.,2023).
| externaldatabase. |     | FivevariantsofSelfCheckGPT |     |             |     |      |     |     |     |     |     |     |     |
| ----------------- | --- | -------------------------- | --- | ----------- | --- | ---- | --- | --- | --- | --- | --- | --- | --- |
| for measuring     |     | informational              |     | consistency | are | con- |     |     |     |     |     |     |     |
sidered: BERTScore,question-answering,n-gram,
| NLI,andLLMprompting. |     |     | Throughanalysisofan- |     |     |     |     |     |     |     |     |     |     |
| -------------------- | --- | --- | -------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
notatedarticlesgeneratedbyGPT-3,weshowthat
SelfCheckGPTisahighlyeffectivehallucination
| detection | method | that | can | even outperform |     | grey- |     |     |     |     |     |     |     |
| --------- | ------ | ---- | --- | --------------- | --- | ----- | --- | --- | --- | --- | --- | --- | --- |
boxmethods,andservesasastrongfirstbaseline
foranincreasinglyimportantproblemofLLMs.
2 BackgroundandRelatedWork
2.1 HallucinationofLargeLanguageModels
|     |     |     |     |     |     |     | Figure2: | ExampleofOpenAI’sGPT-3webinterfacewith |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | -------- | -------------------------------------- | --- | --- | --- | --- | --- |
Hallucinationhasbeenstudiedintextgeneration
outputtoken-levelprobabilitiesdisplayed.
tasks,includingsummarization(Huangetal.,2021)
anddialoguegeneration(Shusteretal.,2021),as
wellasinavarietyofothernaturallanguagegen- 2.3 FactVerification
| eration | tasks | (Ji et al., | 2023). | Self-consistency |     |     |          |                   |     |            |     |        |     |
| ------- | ----- | ----------- | ------ | ---------------- | --- | --- | -------- | ----------------- | --- | ---------- | --- | ------ | --- |
|         |       |             |        |                  |     |     | Existing | fact-verification |     | approaches |     | follow | a   |
decodinghasshowntoimprovechain-of-thought
|           |             |     |     |         |           |     | multi-stage | pipeline | of  | claim | detection, | evidence |     |
| --------- | ----------- | --- | --- | ------- | --------- | --- | ----------- | -------- | --- | ----- | ---------- | -------- | --- |
| prompting | performance |     | on  | complex | reasoning |     |             |          |     |       |            |          |     |
retrievalandverdictprediction(Guoetal.,2022;
| tasks(Wangetal.,2023). |                 |     | Further,Liuetal.(2022) |     |          |      |              |             |          |           |     |          |      |
| ---------------------- | --------------- | --- | ---------------------- | --- | -------- | ---- | ------------ | ----------- | -------- | --------- | --- | -------- | ---- |
|                        |                 |     |                        |     |          |      | Zhong et     | al., 2020). | Such     | methods,  |     | however, | re-  |
| introduce              | a hallucination |     | detection              |     | dataset, | how- |              |             |          |           |     |          |      |
|                        |                 |     |                        |     |          |      | quire access | to          | external | databases |     | and can  | have |
ever,textsareobtainedbyperturbingfactualtexts
considerableinferencecosts.
andthusmaynotreflecttrueLLMhallucination.
Recently,AzariaandMitchell(2023)traineda
|     |     |     |     |     |     |     | 3 Grey-BoxFactualityAssessment |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | ------------------------------ | --- | --- | --- | --- | --- | --- |
multi-layerperceptionclassifierwhereanLLM’s
hidden representations are used as inputs to pre- This section will introduce methods that can be
dictthetruthfulnessofasentence. However,this usedtodeterminethefactualityofLLMresponses
approach is a white-box approach that uses the inazero-resourcesettingwhenonehasfullaccess
9005

distributions.2
| to output |     |     |     | We will | use ‘factual’ to | Entropy |     |     |     |     |     |     |
| --------- | --- | --- | --- | ------- | ---------------- | ------- | --- | --- | --- | --- | --- | --- |
definewhenstatementsaregroundedinvalidinfor- Theentropyoftheoutputdistributionis:
| mation,i.e. |     | whenhallucinationsareavoided,and |     |     |     |     |     |     |     |     |     |     |
| ----------- | --- | -------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
‘zero-resource’whennoexternaldatabaseisused.
|     |     |     |     |     |     |     | =    |     | p (w˜)logp |     | (w˜) |     |
| --- | --- | --- | --- | --- | --- | --- | ---- | --- | ---------- | --- | ---- | --- |
|     |     |     |     |     |     |     | H ij | −   | ij         |     | ij   |     |
w˜
| 3.1 | Uncertainty-basedAssessment |     |     |     |     |     |     | X∈W |     |     |     |     |
| --- | --------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
To understand how the factuality of a generated wherep (w˜)istheprobabilityofthewordw˜being
ij
responsecanbedeterminedinazero-resourceset- generatedatthej-thtokenofthei-thsentence,and
| ting, | we consider | LLM | pre-training. |     | During pre- |        |        |              |     |       |                |     |
| ----- | ----------- | --- | ------------- | --- | ----------- | ------ | ------ | ------------ | --- | ----- | -------------- | --- |
|       |             |     |               |     |             | is the | set of | all possible |     | words | in the vocabu- |     |
W
training,themodelistrainedwithnext-wordpre- lary. Similartotheprobability-basedmetrics,two
dictionovermassivecorporaoftextualdata. This entropy-basedmetricsareused:
givesthemodelastrongunderstandingoflanguage
| (Jawahar | et  | al., 2019; | Raffel | et al., | 2020), power- |        | 1   |     |        |     |      |     |
| -------- | --- | ---------- | ------ | ------- | ------------- | ------ | --- | --- | ------ | --- | ---- | --- |
|          |     |            |        |         |               | Avg( ) | =   |     | ; Max( | ) = | max( | )   |
|          |     |            |        |         |               |        |     | ij  |        |     |      | ij  |
ful contextual reasoning (Zhang et al., 2020), as H J H H j H
j
X
| wellasworldknowledge(Liusieetal.,2023). |           |         |     |          | Con-        |     |     |     |     |     |     |     |
| --------------------------------------- | --------- | ------- | --- | -------- | ----------- | --- | --- | --- | --- | --- | --- | --- |
| sider                                   | the input | "Lionel |     | Messi is | a _". Since |     |     |     |     |     |     |     |
4 Black-BoxFactualityAssessment
| Messi | is a | world-famous |     | athlete | who may have |     |     |     |     |     |     |     |
| ----- | ---- | ------------ | --- | ------- | ------------ | --- | --- | --- | --- | --- | --- | --- |
appearedmultipletimesinpre-training,theLLM A drawback of grey-box methods is that they re-
is likely to know who Messi is. Therefore given quireoutputtoken-levelprobabilities. Thoughthis
the context, the token "footballer" may be as- may seem a reasonable requirement, for massive
signedahighprobabilitywhileotherprofessions LLMs only available through limited API calls,
suchas"carpenter"maybeconsideredimproba-
suchtoken-levelinformationmaynotbeavailable
ble. However,foradifferentinputsuchas"John (such as with ChatGPT). Therefore, we consider
Smith is a _",thesystemwillbeunsureofthe black-box approaches which remain applicable
continuationwhichmayresultinaflatprobability evenwhenonlytext-basedresponsesareavailable.
| distribution.                     |     | Duringinference,thisislikelytolead |     |     |     |           |     |     |     |     |     |     |
| --------------------------------- | --- | ---------------------------------- | --- | --- | --- | --------- | --- | --- | --- | --- | --- | --- |
| toanon-factualwordbeinggenerated. |     |                                    |     |     |     | ProxyLLMs |     |     |     |     |     |     |
This insight allows us to understand the con- A simple approach to approximate the grey-box
nectionbetweenuncertaintymetricsandfactuality. approachesisbyusingaproxyLLM,i.e. another
Factualsentencesarelikelytocontaintokenswith
LLMthatwehavefullaccessto,suchasLLaMA
higherlikelihoodandlowerentropy,whilehalluci-
|     |     |     |     |     |     | (Touvronetal.,2023). |     |     | AproxyLLMcanbeused |     |     |     |
| --- | --- | --- | --- | --- | --- | -------------------- | --- | --- | ------------------ | --- | --- | --- |
nationsarelikelytocomefrompositionswithflat toapproximatetheoutputtoken-levelprobabilities
probabilitydistributionswithhighuncertainty.
|     |     |     |     |     |     | oftheblack-boxLLMgeneratingthetext. |     |     |     |     |     | Inthe |
| --- | --- | --- | --- | --- | --- | ----------------------------------- | --- | --- | --- | --- | --- | ----- |
nextsection,weproposeSelfCheckGPT,whichis
Token-levelProbability
alsoablack-boxapproach.
GiventheLLM’sresponseR,letidenotethei-th
| sentence | in  | R, j denote | the | j-th token | in the i-th |     |     |     |     |     |     |     |
| -------- | --- | ----------- | --- | ---------- | ----------- | --- | --- | --- | --- | --- | --- | --- |
5 SelfCheckGPT
| sentence,J |     | isthenumberoftokensinthesentence, |     |     |     |     |     |     |     |     |     |     |
| ---------- | --- | --------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
andp betheprobabilityofthewordgeneratedby SelfCheckGPT is our proposed black-box zero-
ij
theLLMatthej-thtokenofthei-thsentence. Two resourcehallucinationdetectionscheme,whichop-
probabilitymetricsareused:
|     |     |     |     |     |     | erates by | comparing | multiple |     | sampled | responses |     |
| --- | --- | --- | --- | --- | --- | --------- | --------- | -------- | --- | ------- | --------- | --- |
andmeasuringconsistency.
1
|     | Avg( | logp) | =   |     | logp | Notation: | Let | R refer | to  | an LLM | response |     |
| --- | ---- | ----- | --- | --- | ---- | --------- | --- | ------- | --- | ------ | -------- | --- |
|     |      |       |     | −J  | ij   |           |     |         |     |        |          |     |
−
|     |     |     |     | j   |     | drawn from | a   | given user | query. | SelfCheckGPT |     |     |
| --- | --- | --- | --- | --- | --- | ---------- | --- | ---------- | ------ | ------------ | --- | --- |
X
Max( logp) = max( logp ) drawsafurtherN stochasticLLMresponsesam-
|      |       | −        |     | −          | ij         |                          |          |     |             |                    |         |     |
| ---- | ----- | -------- | --- | ---------- | ---------- | ------------------------ | -------- | --- | ----------- | ------------------ | ------- | --- |
|      |       |          |     | j          |            | ples S1,S2,...,Sn,...,SN |          |     |             | usingthesamequery, |         |     |
|      |       |          |     |            |            | {                        |          |     | }           |                    |         |     |
|      |       |          |     |            |            | and then                 | measures | the | consistency |                    | between | the |
| Max( | logp) | measures | the | sentence’s | likelihood |                          |          |     |             |                    |         |     |
−
|     |     |     |     |     |     | response | and the | stochastic |     | samples. | We  | design |
| --- | --- | --- | --- | --- | --- | -------- | ------- | ---------- | --- | -------- | --- | ------ |
byassessingtheleastlikelytokeninthesentence.
SelfCheckGPTtopredictthehallucinationscoreof
|                                                        |     |     |     |     |     | thei-thsentence, |     | (i),suchthat                   |     | (i) | [0.0,1.0], |     |
| ------------------------------------------------------ | --- | --- | --- | --- | --- | ---------------- | --- | ------------------------------ | --- | --- | ---------- | --- |
| 2Alternatewhite-boxapproachessuchasthatofAzaria        |     |     |     |     |     |                  |     | S                              |     | S   | ∈          |     |
|                                                        |     |     |     |     |     | where (i)        |     | 0.0ifthei-thsentenceisgrounded |     |     |            |     |
| andMitchell(2023)requireaccesstofullinternalstates,and |     |     |     |     |     | S                | →   |                                |     |     |            |     |
islesspracticalandsonotconsideredinthiswork. invalidinformationand (i) 1.0ifthei-thsen-
|     |     |     |     |     |     |     |     |     | S   | →   |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
9006

| tenceishallucinated.3 |     |     |     |     |     | Nn  |     |     |     |     |     |     |
| --------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Thefollowingsubsections . Totakeintoaccounttheanswerabilityof
Nm+Nn
willdescribeeachoftheSelfCheckGPTvariants. generatedquestions,weshowinAppendixBthat
wecanmodifytheinconsistencyscorebyapplying
5.1 SelfCheckGPTwithBERTScore
soft-counting,resultingin:
Let (.,.)denotetheBERTScorebetweentwosen-
| B        |                                   |     |     |     |     |     |     |     |     | N    |     |     |
| -------- | --------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | ---- | --- | --- |
| tenc es. | SelfCheckGPTwithBERTScorefindsthe |     |     |     |     |     |     |     |     | γ n′ |     |     |
2
|                                          |     |     |     |     |     |     |     | QA (i,q) | =   |         |     | (5) |
| ---------------------------------------- | --- | --- | --- | --- | --- | --- | --- | -------- | --- | ------- | --- | --- |
| averageBERTScoreofthei-thsentencewiththe |     |     |     |     |     |     |     | S        |     | N       | N   |     |
|                                          |     |     |     |     |     |     |     |          |     | γ m′ +γ | n′  |     |
|                                          |     |     |     |     |     |     |     |          |     | 1       | 2   |     |
mostsimilarsentencefromeachdrawnsample:
|     |     |     |     |     |     | where | N = | the effective |     | match | count, | N = the |
| --- | --- | --- | --- | --- | --- | ----- | --- | ------------- | --- | ----- | ------ | ------- |
|     |     |     |     |     |     |       | m′  |               |     |       |        | n′      |
N
|     |      |     | 1    |     |         | effectivemismatchcount,withγ |     |                             |     |     | andγ | defined |
| --- | ---- | --- | ---- | --- | ------- | ---------------------------- | --- | --------------------------- | --- | --- | ---- | ------- |
|     | (i)  | = 1 | max( | (r  | ,sn))   |                              |     |                             |     |     | 1    | 2       |
|     | BERT |     |      |     | i k (1) |                              |     |                             |     |     |      |         |
| S   |      | − N |      | k B |         | inAppendixB.1.               |     | Ultimately,SelfCheckGPTwith |     |     |      |         |
n=1
|        |                                   |     | X   |     |     | QAistheaverageofinconsistencyscoresacrossq, |     |     |     |     |     |     |
| ------ | --------------------------------- | --- | --- | --- | --- | ------------------------------------------- | --- | --- | --- | --- | --- | --- |
| wherer | representsthei-thsentenceinRandsn |     |     |     |     |                                             |     |     |     |     |     |     |
|        | i                                 |     |     |     | k   |                                             |     |     |     |     |     |     |
representsthek-thsentenceinthen-thsampleSn. (i) = [ (i,q)] (6)
|     |     |     |     |     |     |     |     | QA  | Eq  | QA  |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|     |     |     |     |     |     |     |     | S   |     | S   |     |     |
Thiswayiftheinformationinasentenceappears
5.3 SelfCheckGPTwithn-gram
inmanydrawnsamples,onemayassumethatthe
S1,...,SN
informationisfactual,whereasifthestatementap- Givensamples generatedbyanLLM,
|     |     |     |     |     |     |     |     | {   |     | }   |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
pearsinnoothersample,itislikelyahallucination. onecanusethesamplestocreateanewlanguage
Inthiswork,RoBERTa-Large(Liuetal.,2019)is modelthatapproximatestheLLM.Inthelimitas
usedasthebackboneofBERTScore. N getssufficientlylarge,thenewlanguagemodel
|     |     |     |     |     |     | will converge |     | to the | LLM | that | generated | the re- |
| --- | --- | --- | --- | --- | --- | ------------- | --- | ------ | --- | ---- | --------- | ------- |
5.2 SelfCheckGPTwithQuestionAnswering sponses. WecanthereforeapproximatetheLLM’s
We also consider using the automatic multiple- tokenprobabilitiesusingthenewlanguagemodel.
choice question answering generation (MQAG) Inpractice,duetotimeand/orcostconstraints,
therecanonlybealimitednumberofsamplesN.
framework(Manakuletal.,2023)tomeasurecon-
sistencyforSelfCheckGPT.MQAGassessescon- Consequently,wetrainasimplen-grammodelus-
sistency by generating multiple-choice questions ingthesamples S1,...,SN aswellasthemain
|     |     |     |     |     |     |     |     | {   |     | }   |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
overthemaingeneratedresponse,whichaninde- response R (which is assessed), where we note
pendentansweringsystemcanattempttoanswer thatincludingRcanbeconsideredasasmoothing
whileconditionedontheothersampledresponses. method where the count of each token in R is in-
Ifquestionsonconsistentinformationarequeried, creasedby1. Wethencomputetheaverageofthe
log-probabilitiesofthesentenceinresponseR,
theansweringsystemisexpectedtopredictsimilar
| answers. | MQAGconsistsoftwostages: |     |     |     | question |     |     |     |     |     |     |     |
| -------- | ------------------------ | --- | --- | --- | -------- | --- | --- | --- | --- | --- | --- | --- |
1
generationGandquestionansweringA.Forthesen- Avg (i) = logp˜ (7)
|     |     |     |     |     |     |     | Sn-gram |     |     |     | ij  |     |
| --- | --- | --- | --- | --- | --- | --- | ------- | --- | --- | --- | --- | --- |
−J
| tence | r i in the | response | R, we | draw | questions q |     |     |     |     | j   |     |     |
| ----- | ---------- | -------- | ----- | ---- | ----------- | --- | --- | --- | --- | --- | --- | --- |
X
andoptionso:
|     |     |     |     |     |     | wherep˜ | istheprobability(ofthej-thtokenofthe |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | ------- | ------------------------------------ | --- | --- | --- | --- | --- |
ij
q,o P (q,o r ,R) (2) i-thsentence)computedusingthen-grammodel.
|     |     |     | G   | i   |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|     |     | ∼   |     | |   |     |     |     |     |     |     |     |     |
Similartothegrey-boxapproach,wecanalsouse
TheansweringstageAselectstheanswers: themaximumofthenegativelogprobabilities,
|     | a   | = argm | ax[P (o | q,R,o)] | (3) |     | M   | ax (i) | = m | ax( logp˜ | )   | (8) |
| --- | --- | ------ | ------- | ------- | --- | --- | --- | ------ | --- | --------- | --- | --- |
|     | R   |        | A       | k       |     |     | Sn  | -g ram |     |           | ij  |     |
|     |     | k      |         | |       |     |     |     |        |     | j −       |     |     |
q,Sn,o)]
|     | a Sn | = argmax[P | (o  |     | (4) |                         |     |     |     |     |     |     |
| --- | ---- | ---------- | --- | --- | --- | ----------------------- | --- | --- | --- | --- | --- | --- |
|     |      |            | A   | k | |     | 5.4 SelfCheckGPTwithNLI |     |     |     |     |     |     |
k
|                   |     |     |            |     |         | Natural                                      | Language |     | Inference | (NLI) | determines |     |
| ----------------- | --- | --- | ---------- | --- | ------- | -------------------------------------------- | -------- | --- | --------- | ----- | ---------- | --- |
| Wecomparewhethera |     |     | isequaltoa |     | foreach |                                              |          |     |           |       |            |     |
|                   |     |     | R          |     | Sn      | whetherahypothesisfollowsapremise,classified |          |     |           |       |            |     |
S1,...,SN
| samplein     |     |       | ,yielding#matchesN |               | m and |             |                                   |     |     |     |     |     |
| ------------ | --- | ----- | ------------------ | ------------- | ----- | ----------- | --------------------------------- | --- | --- | --- | --- | --- |
|              | {   |       | }                  |               |       | into either | entailment/neutral/contradiction. |     |     |     |     | NLI |
| #not-matches |     | N . A | simple             | inconsistency | score |             |                                   |     |     |     |     |     |
n
measureshavebeenusedtomeasurefaithfulnessin
| for the         | i-th sentence |        | and question | q   | based on the |                |            |       |            |         |               |         |
| --------------- | ------------- | ------ | ------------ | --- | ------------ | -------------- | ---------- | ----- | ---------- | ------- | ------------- | ------- |
|                 |               |        |              |     |              | summarization, |            | where | Maynez     |         | et al. (2020) | use     |
| match/not-match |               | counts | is defined:  |     | (i,q) =      |                |            |       |            |         |               |         |
|                 |               |        |              |     | S QA         | a textual      | entailment |       | classifier | trained |               | on MNLI |
(Williamsetal.,2018)todetermineifasummary
3WiththeexceptionofSelfCheckGPTwithn-gramasthe
scoreofthen-gramlanguagemodelisnotbounded. contradictsacontextornot. InspiredbyNLI-based
9007

summaryassessment,weconsiderusingtheNLI 6 DataandAnnotation
contradictionscoreasaSelfCheckGPTscore.
As, currently, there are no standard hallucination
ForSelfCheck-NLI,weuseDeBERTa-v3-large
detectiondatasetsavailable,weevaluateourhallu-
(He et al., 2023) fine-tuned to MNLI as the NLI
cinationdetectionapproachesby1)generatingsyn-
model. TheinputforNLIclassifiersistypicallythe
theticWikipediaarticlesusingGPT-3ontheindi-
premise concatenated to the hypothesis, which
viduals/conceptsfromtheWikiBiodataset(Lebret
for our methodology is the sampled passage Sn
etal.,2016);2)manuallyannotatingthefactuality
concatenated to the sentence to be assessed r .
i
ofthepassageatasentencelevel;3)evaluatingthe
Only the logits associated with the ‘entailment’
system’sabilitytodetecthallucinations.
and‘contradiction’classesareconsidered,
WikiBioisadatasetwhereeachinputcontains
P(contradict r ,Sn) = exp(z c ) (9) thefirstparagraph(alongwithtabularinformation)
i
| exp(z )+exp(z ) ofWikipediaarticlesofaspecificconcept. Werank
e c
the WikiBio test setin termsof paragraph length
where z and z are the logits of the ‘entailment’
e c and randomly sample 238 articles from the top
and‘contradiction’classes,respectively. Thisnor-
20%oflongestarticles(toensurenoveryobscure
malization ignores the neutral class and ensures
concept is selected). GPT-3 (text-davinci-003) is
that the probability is bounded between 0.0 and
thenusedtogenerateWikipediaarticlesonacon-
1.0. The SelfCheckGPT with NLI score for each
cept, using the prompt "This is a Wikipedia
sampleSn isthendefinedas,
passage about {concept}:". Table 1 provides
N thestatisticsofGPT-3generatedpassages.
1
(i) = P(contradict r ,Sn) (10)
NLI i
S N |
n=1 #Passages #Sentences #Tokens/passage
X
5.5 SelfCheckGPTwithPrompt 238 1908 184.7 36.9
±
LLMshaverecentlybeenshowntobeeffectivein
Table1:ThestatisticsofWikiBioGPT-3datasetwherethe
assessinginformationconsistencybetweenadoc-
numberoftokensisbasedontheOpenAIGPT-2tokenizer.
umentanditssummaryinzero-shotsettings(Luo
et al., 2023). Thus, we query an LLM to assess We then annotate the sentences of the generated
whetherthei-thsentenceissupportedbysample passages using the guidelines shown in Figure 3
Sn (asthecontext)usingthefollowingprompt. suchthateachsentenceisclassifiedaseither:
------------------------------------------------
Context: {} • MajorInaccurate(Non-Factual,1): Thesen-
Sentence: {}
tenceisentirelyhallucinated,i.e. thesentence
Is the sentence supported by the context above?
isunrelatedtothetopic.
Answer Yes or No:
------------------------------------------------
• Minor Inaccurate (Non-Factual, 0.5): The
Initial investigation showed that GPT-3 (text-
sentence consists of some non-factual infor-
davinci-003) will output either Yes or No 98% of
mation,butthesentenceisrelatedtothetopic.
thetime,whileanyremainingoutputscanbesetto
N/A.Theoutputfrompromptingwhencomparing • Accurate(Factual, 0): Theinformationpre-
thei-thsentenceagainstsampleSn isconvertedto sentedinthesentenceisaccurate.
scorexn throughthemapping{Yes: 0.0,No: 1.0,
i
Ofthe1908annotatedsentences,761(39.9%)of
N/A: 0.5}. The final inconsistency score is then
thesentenceswerelabelledmajor-inaccurate,631
calculatedas:
(33.1%)minor-inaccurate,and516(27.0%)accu-
N
1 rate. 201sentencesinthedatasethadannotations
(i) = xn (11)
S Prompt N i fromtwodifferentannotators. Toobtainasinglela-
n=1
X belforthissubset,ifbothannotatorsagree,thenthe
SelfCheckGPT-Prompt is illustrated in Figure 1. agreedlabelisused. However,ifthereisdisagree-
Notethatourinitialinvestigationsfoundthatless ment, then the worse-case label is selected (e.g.,
capablemodelssuchasGPT-3(text-curie-001)or {minorinaccurate,majorinaccurate}ismappedto
LLaMAfailedtoeffectivelyperformconsistency majorinaccurate). Theinter-annotatoragreement,
assessmentviasuchprompting. as measured by Cohen’s κ (Cohen, 1960), has κ
9008

|     |     |     |     |     | N=20samples. |     | FortheproxyLLMapproach,we |     |     |     |     |
| --- | --- | --- | --- | --- | ------------ | --- | ------------------------- | --- | --- | --- | --- |
No
Is it related to Major Inaccurate useLLaMA(Touvronetal.,2023),oneofthebest-
the context (Non-factual 1) performingopen-sourceLLMscurrentlyavailable.
ForSelfCheckGPT-Prompt,weconsiderbothGPT-
Yes
3(whichisthesameLLMthatisusedtogenerate
passages)aswellasthenewlyreleasedChatGPT
Is it Factual? No (gpt-3.5-turbo). Moredetailsaboutthesystemsin
Minor Inaccurate
e.g. using Wikipedia /
|     |     |     | (Non-factual 0.5) |     | SelfCheckGPTandresultsusingotherproxyLLMs |     |     |     |     |     |     |
| --- | --- | --- | ----------------- | --- | ----------------------------------------- | --- | --- | --- | --- | --- | --- |
Google Search
canbefoundintheappendix.
Yes
7.1 Sentence-levelHallucinationDetection
|     | Accurate |     |     |     | First,weinvestigatewhetherourhallucinationde- |     |     |     |     |     |     |
| --- | -------- | --- | --- | --- | --------------------------------------------- | --- | --- | --- | --- | --- | --- |
(Factual 0)
tectionmethodscanidentifythefactualityofsen-
Figure3:Flowchartofourannotationprocess tences. In detecting non-factual sentences, both
|     |     |     |     |     | major-inaccurate |     | labels | and minor-inaccurate |     |     | la- |
| --- | --- | --- | --- | --- | ---------------- | --- | ------ | -------------------- | --- | --- | --- |
belsaregroupedtogetherintothenon-factualclass,
valuesof0.595and0.748,indicatingmoderateand
whilethefactualclassreferstoaccuratesentences.
| substantial | agreement | (Viera | et al., | 2005) for the |     |     |     |     |     |     |     |
| ----------- | --------- | ------ | ------- | ------------- | --- | --- | --- | --- | --- | --- | --- |
Inaddition,weconsideramorechallengingtaskof
3-classand2-classscenarios,respectively.4
|     |     |     |     |     | detecting | major-inaccurate |     | sentences |     | in passages |     |
| --- | --- | --- | --- | --- | --------- | ---------------- | --- | --------- | --- | ----------- | --- |
Furthermore,passage-levelscoresareobtained
thatarenottotalhallucinationpassages,whichwe
byaveragingthesentence-levellabelsineachpas-
.5 |       |                  |     |               |           | refer to | as non-factual |     | Figure | 5           | and Table | 2     |
| ----- | ---------------- | --- | ------------- | --------- | -------- | -------------- | --- | ------ | ----------- | --------- | ----- |
| sage. | The distribution | of  | passage-level | scores is |          |                |     | ∗      |             |           |       |
|       |                  |     |               |           | show the | performance    |     | of our | approaches, |           | where |
showninFigure4,whereweobservealargepeak
thefollowingobservationscanbemade:
at+1.0. Werefertothepointsatthispeakastotal
1)LLM’sprobabilitiespcorrelatewellwith
hallucination,whichoccurswhentheinformation
|     |     |     |     |     | factuality. | Ourresultsshowthatprobabilitymea- |     |     |     |     |     |
| --- | --- | --- | --- | --- | ----------- | --------------------------------- | --- | --- | --- | --- | --- |
oftheresponseisunrelatedtotherealconceptand
|     |     |     |     |     | sures (from | the | LLM | generating | the | texts) | are |
| --- | --- | --- | --- | --- | ----------- | --- | --- | ---------- | --- | ------ | --- |
isentirelyfabricatedbytheLLM.
|     |     |     |     |     | strong                                         | baselines | for assessing |      | factuality. | Factual  |     |
| --- | --- | --- | --- | --- | ---------------------------------------------- | --------- | ------------- | ---- | ----------- | -------- | --- |
|     |     |     |     |     | sentences                                      | can       | be identified | with | an          | AUC-PR   | of  |
|     | 30  |     |     |     | 53.97,significantlybetterthantherandombaseline |           |               |      |             |          |     |
|     | 25  |     |     |     | of27.04,withtheAUC-PRforhallucinationdetec-    |           |               |      |             |          |     |
|     |     |     |     |     | tionalsoincreasingfrom72.96to83.21.            |           |               |      |             | Thissup- |     |
20
| tnuoC |     |     |     |     | portsthehypothesisthatwhentheLLMsareuncer- |     |     |     |     |     |     |
| ----- | --- | --- | --- | --- | ------------------------------------------ | --- | --- | --- | --- | --- | --- |
15
tainaboutgeneratedinformation,generatedtokens
10
oftenhavehigheruncertainty,pavingapromising
|     |     |     |     |     | direction | for | hallucination | detection |     | approaches. |     |
| --- | --- | --- | --- | --- | --------- | --- | ------------- | --------- | --- | ----------- | --- |
5
|     |     |     |     |     | Also, the | probability |     | p measure | performs |     | better |
| --- | --- | --- | --- | --- | --------- | ----------- | --- | --------- | -------- | --- | ------ |
0
|     | 0.0 0.2                                                  | 0.4 | 0.6 0.8 | 1.0 |                |     |                       |     |     |     |     |
| --- | -------------------------------------------------------- | --- | ------- | --- | -------------- | --- | --------------------- | --- | --- | --- | --- |
|     |                                                          |     |         |     | thantheentropy |     | measureoftop-5tokens. |     |     |     |     |
|     | Avg. Factuality per Document (0=Factual, +1=Non-Factual) |     |         |     |                |     | H                     |     |     |     |     |
2)ProxyLLMperformnoticeablyworsethan
Figure4:Documentfactualityscoreshistogramplot
|     |     |     |     |     | LLM(GPT-3). |     | TheresultsofproxyLLM(based |             |     |          |     |
| --- | --- | --- | --- | --- | ----------- | --- | -------------------------- | ----------- | --- | -------- | --- |
|     |     |     |     |     | on LLaMA)   |     | show that                  | the entropy |     | measures |     |
H
| 7 Experiments |     |     |     |     | outperform | the | probability | measures. |     | This | sug- |
| ------------- | --- | --- | --- | --- | ---------- | --- | ----------- | --------- | --- | ---- | ---- |
geststhatusingricheruncertaintyinformationcan
ThegenerativeLLMusedtogeneratepassagesfor
improvefactuality/hallucinationdetectionperfor-
ourdatasetisGPT-3(text-davinci-003),thestate-
|     |     |     |     |     | mance, | and that | previously | the | entropy | of  | top-5 |
| --- | --- | --- | --- | --- | ------ | -------- | ---------- | --- | ------- | --- | ----- |
of-the-artsystematthetimeofcreatingandanno- tokensislikelytobeinsufficient. Inaddition,when
| tatingthedataset. |     | Toobtainthemainresponse,we |     |     |             |       |      |      |             |     |     |
| ----------------- | --- | -------------------------- | --- | --- | ----------- | ----- | ---- | ---- | ----------- | --- | --- |
|                   |     |                            |     |     | using other | proxy | LLMs | such | as GPT-NeoX |     | or  |
setthetemperatureto0.0andusestandardbeam
OPT-30B,theperformanceisnearthatoftheran-
| searchdecoding. | Forthestochasticallygenerated |     |     |     |               |     |            |      |      |             |     |
| --------------- | ----------------------------- | --- | --- | --- | ------------- | --- | ---------- | ---- | ---- | ----------- | --- |
|                 |                               |     |     |     | dom baseline. |     | We believe | this | poor | performance |     |
samples,wesetthetemperatureto1.0andgenerate occursasdifferentLLMshavedifferentgenerating
patterns,andsoevencommontokensmayhavea
43-classreferstowhenselectingbetweenaccurate,mi-
| norinaccurate,majorinaccurate. |     |     | 2-classreferstowhenmi- |     |     |     |     |     |     |     |     |
| ------------------------------ | --- | --- | ---------------------- | --- | --- | --- | --- | --- | --- | --- | --- |
nor/majorinaccuraciesarecombinedintoonelabel. 5Thereare206non-factual∗passages(1632sentences).
9009

1.0
| 1.00 |     |     | Random           |     |     | Random           | 1.0 |     |     | Random           |
| ---- | --- | --- | ---------------- | --- | --- | ---------------- | --- | --- | --- | ---------------- |
|      |     |     | GPT-3 Avg(-logP) |     |     | GPT-3 Avg(-logP) |     |     |     | GPT-3 Avg(-logP) |
|      |     |     |                  | 0.9 |     | SelfCk-BERTScore | 0.9 |     |     | SelfCk-BERTScore |
| 0.95 |     |     | SelfCk-BERTScore |     |     | SelfCk-QA        |     |     |     | SelfCk-QA        |
|      |     |     | SelfCk-QA        |     |     |                  | 0.8 |     |     |                  |
|      |     |     | SelfCk-Unigram   | 0.8 |     | SelfCk-Unigram   |     |     |     | SelfCk-Unigram   |
|      |     |     | SelfCk-Prompt    |     |     | SelfCk-Prompt    |     |     |     | SelfCk-Prompt    |
noisicerP 0.90 SelfCk-NLI noisicerP 0.7 SelfCk-NLI noisicerP 0.7 SelfCk-NLI
0.6
| 0.85 |     |     |     | 0.6 |     |     |     |     |     |     |
| ---- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
0.5
| 0.80 |     |     |     | 0.5 |     |     |     |     |     |     |
| ---- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
0.4
0.4
0.75
0.3
0.3
| 0.70 |     |     |     |     |     |     | 0.2 |     |     |     |
| ---- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
0.0 0.2 0.4 0.6 0.8 1.0 0.0 0.2 0.4 0.6 0.8 1.0 0.0 0.2 0.4 0.6 0.8 1.0
|     |     | Recall |     |     |     | Recall |     |     | Recall |     |
| --- | --- | ------ | --- | --- | --- | ------ | --- | --- | ------ | --- |
(a)Non-FactualSentences (b)Non-Factual*Sentences (c)FactualSentences
Figure5:PR-Curveofdetectingnon-factualandfactualsentencesintheGPT-3generatedWikiBiopassages.
|     |     |     |     | Sentence-level(AUC-PR) |     |     | Passage-level(Corr.) |     |     |     |
| --- | --- | --- | --- | ---------------------- | --- | --- | -------------------- | --- | --- | --- |
Method
|     |     |        |                                                 | NonFact | NonFact* | Factual | Pearson | Spearman |     |     |
| --- | --- | ------ | ----------------------------------------------- | ------- | -------- | ------- | ------- | -------- | --- | --- |
|     |     | Random |                                                 | 72.96   | 29.72    | 27.04   | -       |          | -   |     |
|     |     | GPT-3  | (text-davinci-003)’sprobabilities(LLM,grey-box) |         |          |         |         |          |     |     |
|     |     | Avg(   | logp)                                           | 83.21   | 38.89    | 53.97   | 57.04   | 53.93    |     |     |
−
|     |     | Avg( | ) † | 80.73 | 37.09 | 52.07 | 55.52 | 50.87 |     |     |
| --- | --- | ---- | --- | ----- | ----- | ----- | ----- | ----- | --- | --- |
H
|     |     | Max( | logp) | 87.51 | 35.88 | 50.46 | 57.83 | 55.69 |     |     |
| --- | --- | ---- | ----- | ----- | ----- | ----- | ----- | ----- | --- | --- |
−
|     |     | Max( | )   | 85.75 | 32.43 | 50.27 | 52.48 | 49.55 |     |     |
| --- | --- | ---- | --- | ----- | ----- | ----- | ----- | ----- | --- | --- |
†
H
LLaMA-30B’sprobabilities(ProxyLLM,black-box)
|     |     | Avg( | logp) | 75.43 | 30.32 | 41.29 | 21.72 | 20.20 |     |     |
| --- | --- | ---- | ----- | ----- | ----- | ----- | ----- | ----- | --- | --- |
−
|     |     | Avg( | )   | 80.80 | 39.01 | 42.97 | 33.80 | 39.49 |     |     |
| --- | --- | ---- | --- | ----- | ----- | ----- | ----- | ----- | --- | --- |
H
|     |     | Max( | logp) | 74.01 | 27.14 | 31.08 | -22.83 | -22.71 |     |     |
| --- | --- | ---- | ----- | ----- | ----- | ----- | ------ | ------ | --- | --- |
−
|     |     | Max( | )   | 80.92 | 37.32 | 37.90 | 35.57 | 38.94 |     |     |
| --- | --- | ---- | --- | ----- | ----- | ----- | ----- | ----- | --- | --- |
H
SelfCheckGPT(black-box)
|     |     | w/BERTScore    |     | 81.96 | 45.96 | 44.23 | 58.18 | 55.90 |     |     |
| --- | --- | -------------- | --- | ----- | ----- | ----- | ----- | ----- | --- | --- |
|     |     | w/QA           |     | 84.26 | 40.06 | 48.14 | 61.07 | 59.29 |     |     |
|     |     | w/Unigram(max) |     | 85.63 | 41.04 | 58.47 | 64.71 | 64.91 |     |     |
|     |     | w/NLI          |     | 92.50 | 45.17 | 66.08 | 74.14 | 73.78 |     |     |
|     |     | w/Prompt       |     | 93.42 | 53.19 | 67.09 | 78.32 | 78.30 |     |     |
Table2:AUC-PRforsentence-leveldetectiontasks.Passage-levelrankingperformancesaremeasuredbyPearsoncorrelation
coefficientandSpearman’srankcorrelationcoefficientw.r.t.humanjudgements.TheresultsofotherproxyLLMs,inadditionto
LLaMA,canbefoundintheappendix.†GPT-3APIreturnsthetop-5tokens’probabilities,whichareusedtocomputeentropy.
low probability in situations where the response acrossdifferentsetups. Essentially,whenassessing
is dissimilar to the generation style of the proxy a sentence, this method picks up the token with
LLM. We note that a weighted conditional LM thelowestoccurrencegivenallthesamples. This
scoresuchasBARTScore(Yuanetal.,2021)could suggests that if a token only appears a few times
beincorporatedinfutureinvestigations. (oronce)withinthegeneratedsamples(N=20),it
| 3) SelfCheckGPT |     |     | outperforms | grey-box | ap- | islikelynon-factual. |     |     |     |     |
| --------------- | --- | --- | ----------- | -------- | --- | -------------------- | --- | --- | --- | --- |
proaches. It can be seen that SelfCheckGPT- 4) SelfCheckGPT with n-gram. When inves-
Promptconsiderablyoutperformsthegrey-boxap- tigating the n-gram performance from 1-gram to
proaches(includingGPT-3’soutputprobabilities) 5-gram, the results show that simply finding the
aswellasotherblack-boxapproaches. Evenother least likely token/n-gram is more effective than
variantsofSelfCheckGPT,includingBERTScore, computing the average n-gram score of the sen-
|         | n-gram, |     |            |              |     | tence, details | in appendix | Table | 7.  | Additionally, |
| ------- | ------- | --- | ---------- | ------------ | --- | -------------- | ----------- | ----- | --- | ------------- |
| QA, and |         |     | outperform | the grey-box | ap- |                |             |       |     |               |
proachesinmostsetups. Interestingly,despitebe- asnincreases,theperformanceofSelfCheckGPT
ing the least computationally expensive method, withn-gram(max)drops.
SelfCheckGPT with unigram (max) works well 5) SelfCheckGPT with NLI. The NLI-based
9010

0.7
0.6
0.5
0.4
0.3
0.2
0.1
0.0
0.0 0.2 0.4 0.6 0.8 1.0
Human Score (0=Factual, +1=Non-Factual)
erocS
dohteM
25
20
15
10
5
0.0 0.2 0.4 0.6 0.8 1.0
Human Score (0=Factual, +1=Non-Factual)
(a)GPT-3Avg( logp)
−
erocS
dohteM
1.0
0.8
0.6
0.4
0.2
0.0
0.0 0.2 0.4 0.6 0.8 1.0
Human Score (0=Factual, +1=Non-Factual)
(b)LLaMA-30BAvg( )
H
erocS
dohteM
(c)SelfCheckGPT-Prompt
Figure6:Scatterplotofpassage-levelscoreswhereY-axis=Methodscores,X-axis=Humanscores.Correlationsarereported
inTable2.ThescatterplotsofotherSelfCheckGPTvariantsareprovidedinFigure10intheappendix.
method outperforms all black-box and grey-box 7.3 AblationStudies
baselines,anditsperformanceisclosetotheper-
ExternalKnowledge(insteadofSelfCheck)
formance of the Prompt method. As SelfCheck-
Ifexternalknowledgeisavailable,onecanmeasure
GPT with Prompt can be computationally heavy,
the informational consistency between the LLM
SelfCheckGPTwithNLIcouldbethemostpracti-
responseandtheinformationsource. Inthisexper-
calmethodasitprovidesagoodtrade-offbetween
iment,weusethefirstparagraphofeachconcept
performanceandcomputation.
thatisavailableinWikiBio.6
7.2 Passage-levelFactualityRanking
Sent-lvlAUC-PR Passage-lvl
Method
NoFac NoFac* Fact Pear. Spear.
Previous results demonstrate that SelfCheckGPT
is an effective approach for predicting sentence- SelfCk-BERT 81.96 45.96 44.23 58.18 55.90
WikiBio+BERT 81.32 40.62 49.15 58.71 55.80
level factuality. An additional consideration is
whether SelfCheckGPT can also be used to de- SelfCk-QA 84.26 40.06 48.14 61.07 59.29
WikiBio+QA 84.18 45.40 52.03 57.26 53.62
terminetheoverallfactualityofpassages. Passage-
SelfCk-1gm 85.63 41.04 58.47 64.71 64.91
levelfactualityscoresarecalculatedbyaveraging
WikiBio+1gm 80.43 31.47 40.53 28.67 26.70
thesentence-levelscoresoverallsentences.
SelfCk-NLI 92.50 45.17 66.08 74.14 73.78
WikiBio+NLI 91.18 48.14 71.61 78.84 80.00
1
= (i) (12)
S passage R S SelfCk-Prompt 93.42 53.19 67.09 78.32 78.30
| | i WikiBio+Prompt 93.59 65.26 73.11 85.90 86.11
X
where (i) is the sentence-level score, and R Table3:TheperformancewhenusingSelfCheckGPTsamples
S | |
is the number of sentences in the passage. Since versusexternalstoredknowledge.
humanjudgementissomewhatsubjective,averag-
ingthesentence-levellabelswouldleadtoground OurfindingsinTable3showthefollowing. First,
truthswithlessnoise. NotethatforAvg( logp) SelfCheckGPT with BERTScore/QA, using self-
−
and Avg( ), we compute the average over all to- samples,canyieldcomparableorevenbetterper-
H
kensinapassage. WhereasforMax( logp)and formance than when using the reference passage.
Max( ),wefirsttakethemaximumop
−
erationover
Second,SelfCheckGPTwithn-gramshowsalarge
H
tokensatthesentencelevel,andwethenaverage performance drop when using the WikiBio pas-
overallsentencesfollowingEquation12. sages instead of self-samples. This failure is at-
tributedtothefactthattheWikiBioreferencetext
OurresultsinTable2andFigure6showthatall
alone is not sufficient to train an n-gram model.
SelfCheckGPT methods correlate far better with
Third,incontrast,SelfCheckGPTwithNLI/Prompt
human judgements than the other baselines, in-
canbenefitconsiderablywhenaccesstoretrieved
cludingthegrey-boxprobabilityandentropymeth-
informationisavailable. Nevertheless,inpractice,
ods. SelfCheckGPT-Promptisthebest-performing
method,achievingthehighestPearsoncorrelation
of78.32. Unsurprisingly,theproxyLLMapproach
6This method is no longer zero-resource as it requires
againachievesconsiderablylowercorrelations. retrievingrelevantknowledgefromexternaldata.
9011

| itisinfeasibletohaveanexternaldatabaseforev- |     |     |     |     |     |     | 8 Conclusions |     |     |     |     |     |     |
| -------------------------------------------- | --- | --- | --- | --- | --- | --- | ------------- | --- | --- | --- | --- | --- | --- |
erypossibleusecaseofLLMgeneration.
|     |     |     |     |     |     |     | This paper | is  | the first | work | to consider | the | task |
| --- | --- | --- | --- | --- | --- | --- | ---------- | --- | --------- | ---- | ----------- | --- | ---- |
TheImpactoftheNumberofSamples of hallucination detection for general large lan-
|          |              |     |     |         |     |          | guage model |               | responses. | We       | propose | SelfCheck-    |     |
| -------- | ------------ | --- | --- | ------- | --- | -------- | ----------- | ------------- | ---------- | -------- | ------- | ------------- | --- |
| Although | sample-based |     |     | methods | are | expected | to          |               |            |          |         |               |     |
|          |              |     |     |         |     |          | GPT, a      | zero-resource |            | approach | that    | is applicable |     |
performbetterwhenmoresamplesaredrawn,this
|            |             |               |           |        |       |          | to any            | black-box                     | LLM | without     | the | need         | for ex- |
| ---------- | ----------- | ------------- | --------- | ------ | ----- | -------- | ----------------- | ----------------------------- | --- | ----------- | --- | ------------ | ------- |
| has higher |             | computational |           | costs. | Thus, | we       | inves-            |                               |     |             |     |              |         |
|            |             |               |           |        |       |          | ternal resources, |                               | and | demonstrate |     | the efficacy | of      |
| tigate     | performance |               | as the    | number | of    | samples  | is                |                               |     |             |     |              |         |
|            |             |               |           |        |       |          | ourmethod.        | SelfCheckGPToutperformsarange |     |             |     |              |         |
| varied.    | Our         | results       | in Figure | 7      | show  | that the | per-              |                               |     |             |     |              |         |
ofconsideredgrey-boxandblack-boxbaselinede-
formanceofSelfCheckGPTincreasessmoothlyas
tectionmethodsatboththesentenceandpassage
moresamplesareused,withdiminishinggainsas
levels,andwefurtherreleaseanannotateddataset
| moresamplesaregenerated. |          |     |         | SelfCheckGPTwith |     |            |           |               |     |           |     |                |     |
| ------------------------ | -------- | --- | ------- | ---------------- | --- | ---------- | --------- | ------------- | --- | --------- | --- | -------------- | --- |
|                          |          |     |         |                  |     |            | for GPT-3 | hallucination |     | detection |     | with sentence- |     |
| n-gram                   | requires | the | highest | number           |     | of samples |           |               |     |           |     |                |     |
levelfactualitylabels.
beforeitsperformancereachesaplateau.
Limitations
80
70
Inthisstudy,the238GPT-3generatedtextswere
CCknaR s'namraepS predominantly passages about individuals in the
60
|     |     |     |     |     |     |     | WikiBiodataset. |     | Tofurtherinvestigatethenature |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --------------- | --- | ----------------------------- | --- | --- | --- | --- |
50
|     |     |     |     |     |     |     | of LLM’s | hallucination, |       | this         | study | could | be ex-  |
| --- | --- | --- | --- | --- | --- | --- | -------- | -------------- | ----- | ------------ | ----- | ----- | ------- |
|     |     |     |     |     |     |     | tended   | to a wider     | range | of concepts, |       | e.g., | to also |
40
SelfCk-BERTScore
|     |     |     |     |     | SelfCk-QA      |     | consider                                        | generated |     | texts about | locations |     | and ob- |
| --- | --- | --- | --- | --- | -------------- | --- | ----------------------------------------------- | --------- | --- | ----------- | --------- | --- | ------- |
|     | 30  |     |     |     | SelfCk-Unigram |     |                                                 |           |     |             |           |     |         |
|     |     |     |     |     | SelfCk-NLI     |     | jects. Further,thisworkconsidersfactualityatthe |           |     |             |           |     |         |
SelfCk-Prompt
sentencelevel,butwenotethatasinglesentence
|          | 0                                     | 2 4 | 6 8          | 10 12 | 14 16 | 18 20 |                                             |                                  |     |     |     |     |     |
| -------- | ------------------------------------- | --- | ------------ | ----- | ----- | ----- | ------------------------------------------- | -------------------------------- | --- | --- | --- | --- | --- |
|          |                                       |     | Num. samples |       |       |       | mayconsistofbothfactualandnon-factualinfor- |                                  |     |     |     |     |     |
|          |                                       |     |              |       |       |       | mation.                                     | Forexample,thefollowingworkbyMin |     |     |     |     |     |
| Figure7: | TheperformanceofSelfCheckGPTmethodson |     |              |       |       |       |                                             |                                  |     |     |     |     |     |
rankingpassages(Spearman’s)versusthenumberofsamples. etal.(2023)considersafine-grainedfactualityeval-
uationbydecomposingsentencesintoatomicfacts.
|     |     |     |     |     |     |     | Finally, | SelfCheckGPT |     | with | Prompt, | which | was |
| --- | --- | --- | --- | --- | --- | --- | -------- | ------------ | --- | ---- | ------- | ----- | --- |
TheChoiceofLLMforSelfCheckGPT-Prompt convincingly the best selfcheck method, is quite
|                |     |         |     |         |            |     | computationallyheavy. |     |     | Thismightleadtoimpracti- |     |     |     |
| -------------- | --- | ------- | --- | ------- | ---------- | --- | --------------------- | --- | --- | ------------------------ | --- | --- | --- |
| We investigate |     | whether |     | the LLM | generating |     | the                   |     |     |                          |     |     |     |
calcomputationalcosts,whichcouldbeaddressed
| text can | self-check |     | its own | text. | We  | conduct | this |     |     |     |     |     |     |
| -------- | ---------- | --- | ------- | ----- | --- | ------- | ---- | --- | --- | --- | --- | --- | --- |
infutureworktobemademoreefficient.
ablationusingareducedsetofthesamples(N=4).
EthicsStatement
| Text-Gen |     | SelfCk-Prompt |     | N   | Pear. | Spear. |     |     |     |     |     |     |     |
| -------- | --- | ------------- | --- | --- | ----- | ------ | --- | --- | --- | --- | --- | --- | --- |
| GPT-3    |     | ChatGPT       |     | 20  | 78.32 | 78.30  |     |     |     |     |     |     |     |
GPT-3 ChatGPT 4 76.47 76.41 AsthisworkaddressestheissueofLLM’shalluci-
GPT-3 GPT-3 4 73.11 74.69 nation,wenotethatifhallucinatedcontentsarenot
detected,theycouldleadtomisinformation.
| †SelfCheckw/unigram(max) |     |     |     | 20  | 64.71 | 64.91 |     |     |     |     |     |     |     |
| ------------------------ | --- | --- | --- | --- | ----- | ----- | --- | --- | --- | --- | --- | --- | --- |
| †SelfCheckw/NLI          |     |     |     | 20  | 74.14 | 73.78 |     |     |     |     |     |     |     |
Acknowledgments
Table4:ComparisonofGPT-3(text-davinci-003)andChat-
| GPT | (gpt-3.5.turbo) | as  | the prompt-based |     | text | evaluator | in  |     |     |     |     |     |     |
| --- | --------------- | --- | ---------------- | --- | ---- | --------- | --- | --- | --- | --- | --- | --- | --- |
SelfCheckGPT-Prompt.†TakenfromTable2forcomparison.
|     |     |     |     |     |     |     | This work | is supported |     | by Cambridge |     | University |     |
| --- | --- | --- | --- | --- | --- | --- | --------- | ------------ | --- | ------------ | --- | ---------- | --- |
|     |     |     |     |     |     |     | Press &   | Assessment   |     | (CUP&A),     | a   | department | of  |
The results in Table 4 show that GPT-3 can self- TheChancellor,Masters,andScholarsoftheUni-
checkitsowntext,andisbetterthantheunigram versity of Cambridge, and the Cambridge Com-
methodevenwhenusingonly4samples. However, monwealth, European & International Trust. We
ChatGPTshowsaslightimprovementoverGPT-3 wouldliketothanktheanonymousreviewersfor
inevaluatingwhetherthesentenceissupportedby theirhelpfulcomments.
| thecontext. |     | MoredetailsareinAppendixC. |     |     |     |     |     |     |     |     |     |     |     |
| ----------- | --- | -------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
9012

| References  |     |     |           |       |              | Madotto,andPascaleFung.2023.       |     |     |     | Surveyofhalluci- |            |     |
| ----------- | --- | --- | --------- | ----- | ------------ | ---------------------------------- | --- | --- | --- | ---------------- | ---------- | --- |
|             |     |     |           |       |              | nationinnaturallanguagegeneration. |     |     |     |                  | ACMComput. |     |
| Amos Azaria | and | Tom | Mitchell. | 2023. | The internal |                                    |     |     |     |                  |            |     |
Surv.,55(12).
| stateofanllmknowswhenitslying. |     |     |     | arXivpreprint |     |     |     |     |     |     |     |     |
| ------------------------------ | --- | --- | --- | ------------- | --- | --- | --- | --- | --- | --- | --- | --- |
arXiv:2304.13734.
SauravKadavath,TomConerly,AmandaAskell,Tom
|     |     |     |     |     |     | Henighan, | Dawn | Drain, | Ethan | Perez, | Nicholas |     |
| --- | --- | --- | --- | --- | --- | --------- | ---- | ------ | ----- | ------ | -------- | --- |
IzBeltagy,MatthewE.Peters,andArmanCohan.2020.
|             |                              |     |     |     |     | Schiefer,         | Zac | Hatfield | Dodds,    | Nova     | DasSarma, |     |
| ----------- | ---------------------------- | --- | --- | --- | --- | ----------------- | --- | -------- | --------- | -------- | --------- | --- |
| Longformer: | Thelong-documenttransformer. |     |     |     |     |                   |     |          |           |          |           |     |
|             |                              |     |     |     |     | Eli Tran-Johnson, |     | et       | al. 2022. | Language | models    |     |
SidneyBlack,StellaBiderman,EricHallahan,Quentin (mostly) know what they know. arXiv preprint
| Anthony,   | Leo    | Gao, | Laurence  | Golding, | Horace | arXiv:2207.05221. |     |     |     |     |     |     |
| ---------- | ------ | ---- | --------- | -------- | ------ | ----------------- | --- | --- | --- | --- | --- | --- |
| He, Connor | Leahy, | Kyle | McDonell, | Jason    | Phang, |                   |     |     |     |     |     |     |
WojciechKryscinski,BryanMcCann,CaimingXiong,
MichaelPieler,UsvsnSaiPrashanth,ShivanshuPuro-
hit,LariaReynolds,JonathanTow,BenWang,and and Richard Socher. 2020. Evaluating the factual
SamuelWeinbach.2022. GPT-NeoX-20B:Anopen- consistency of abstractive text summarization. In
sourceautoregressivelanguagemodel. InProceed- Proceedings of the 2020 Conference on Empirical
ingsofBigScienceEpisode#5–WorkshoponChal- MethodsinNaturalLanguageProcessing(EMNLP),
pages9332–9346,Online.AssociationforComputa-
lenges&PerspectivesinCreatingLargeLanguage
| Models,pages95–136,virtual+Dublin.Association |     |     |     |     |     | tionalLinguistics. |     |     |     |     |     |     |
| --------------------------------------------- | --- | --- | --- | --- | --- | ------------------ | --- | --- | --- | --- | --- | --- |
forComputationalLinguistics.
LorenzKuhn,YarinGal,andSebastianFarquhar.2023.
Tom Brown, Benjamin Mann, Nick Ryder, Melanie Semanticuncertainty: Linguisticinvariancesforun-
Subbiah,JaredDKaplan,PrafullaDhariwal,Arvind
certaintyestimationinnaturallanguagegeneration.
Neelakantan,PranavShyam,GirishSastry,Amanda
InTheEleventhInternationalConferenceonLearn-
| Askell,etal.2020. |                                       | Languagemodelsarefew-shot |     |     |     | ingRepresentations. |     |     |     |     |     |     |
| ----------------- | ------------------------------------- | ------------------------- | --- | --- | --- | ------------------- | --- | --- | --- | --- | --- | --- |
| learners.         | Advancesinneuralinformationprocessing |                           |     |     |     |                     |     |     |     |     |     |     |
systems,33:1877–1901.
|     |     |     |     |     |     | Guokun              | Lai, Qizhe | Xie, | Hanxiao               | Liu, | Yiming | Yang, |
| --- | --- | --- | --- | --- | --- | ------------------- | ---------- | ---- | --------------------- | ---- | ------ | ----- |
|     |     |     |     |     |     | andEduardHovy.2017. |            |      | RACE:Large-scaleReAd- |      |        |       |
AakankshaChowdhery,SharanNarang,JacobDevlin,
|              |        |        |            |         |          | ing comprehension |     | dataset  |            | from examinations. |              | In  |
| ------------ | ------ | ------ | ---------- | ------- | -------- | ----------------- | --- | -------- | ---------- | ------------------ | ------------ | --- |
| Maarten      | Bosma, | Gaurav | Mishra,    | Adam    | Roberts, |                   |     |          |            |                    |              |     |
|              |        |        |            |         |          | Proceedings       | of  | the 2017 | Conference |                    | on Empirical |     |
| Paul Barham, |        | Hyung  | Won Chung, | Charles | Sutton,  |                   |     |          |            |                    |              |     |
MethodsinNaturalLanguageProcessing,pages785–
| Sebastian | Gehrmann, |     | et al. | 2022. Palm: | Scaling |     |     |     |     |     |     |     |
| --------- | --------- | --- | ------ | ----------- | ------- | --- | --- | --- | --- | --- | --- | --- |
794,Copenhagen,Denmark.AssociationforCompu-
| language | modeling | with | pathways. | arXiv | preprint |     |     |     |     |     |     |     |
| -------- | -------- | ---- | --------- | ----- | -------- | --- | --- | --- | --- | --- | --- | --- |
tationalLinguistics.
arXiv:2204.02311.
RémiLebret,DavidGrangier,andMichaelAuli.2016.
| Jacob Cohen. | 1960. | A   | coefficient | of agreement | for |     |     |     |     |     |     |     |
| ------------ | ----- | --- | ----------- | ------------ | --- | --- | --- | --- | --- | --- | --- | --- |
nominalscales. EducationalandPsychologicalMea- Generatingtextfromstructureddatawithapplication
surement,20:37–46. tothebiographydomain. CoRR,abs/1603.07771.
|     |     |     |     |     |     | Tianyu Liu, | Yizhe | Zhang, | Chris | Brockett, | Yi  | Mao, |
| --- | --- | --- | --- | --- | --- | ----------- | ----- | ------ | ----- | --------- | --- | ---- |
JinlanFu,See-KiongNg,ZhengbaoJiang,andPengfei
Liu.2023. Gptscore: Evaluateasyoudesire. Zhifang Sui, Weizhu Chen, and Bill Dolan. 2022.
Atoken-levelreference-freehallucinationdetection
ZhijiangGuo,MichaelSchlichtkrull,andAndreasVla- benchmarkforfree-formtextgeneration. InProceed-
chos. 2022. A survey on automated fact-checking. ingsofthe60thAnnualMeetingoftheAssociation
TransactionsoftheAssociationforComputational forComputationalLinguistics(Volume1: LongPa-
Linguistics,10:178–206. pers),pages6723–6737,Dublin,Ireland.Association
forComputationalLinguistics.
PengchengHe,JianfengGao,andWeizhuChen.2023.
DeBERTav3: ImprovingdeBERTausingELECTRA- YinhanLiu,MyleOtt,NamanGoyal,JingfeiDu,Man-
stylepre-trainingwithgradient-disentangledembed- dar Joshi, Danqi Chen, Omer Levy, Mike Lewis,
| dingsharing. |     | InTheEleventhInternationalConfer- |     |     |     |      |              |     |             |           |     |       |
| ------------ | --- | --------------------------------- | --- | --- | --- | ---- | ------------ | --- | ----------- | --------- | --- | ----- |
|              |     |                                   |     |     |     | Luke | Zettlemoyer, |     | and Veselin | Stoyanov. |     | 2019. |
enceonLearningRepresentations.
|     |     |     |     |     |     | Roberta: | A robustly                     |     | optimized | bert | pretraining | ap- |
| --- | --- | --- | --- | --- | --- | -------- | ------------------------------ | --- | --------- | ---- | ----------- | --- |
|     |     |     |     |     |     | proach.  | arXivpreprintarXiv:1907.11692. |     |           |      |             |     |
YichongHuang,XiachongFeng,XiaochengFeng,and
| BingQin.2021.                   |     | Thefactualinconsistencyproblem |     |          |     |               |        |        |     |          |        |       |
| ------------------------------- | --- | ------------------------------ | --- | -------- | --- | ------------- | ------ | ------ | --- | -------- | ------ | ----- |
|                                 |     |                                |     |          |     | Adian Liusie, | Vatsal | Raina, |     | and Mark | Gales. | 2023. |
| inabstractivetextsummarization: |     |                                |     | Asurvey. |     |               |        |        |     |          |        |       |
“worldknowledge”inmultiplechoicereadingcom-
|                 |     |        |        |           |         | prehension. | In  | Proceedings |     | of the | Sixth Fact | Ex- |
| --------------- | --- | ------ | ------ | --------- | ------- | ----------- | --- | ----------- | --- | ------ | ---------- | --- |
| Ganesh Jawahar, |     | Benoît | Sagot, | and Djamé | Seddah. |             |     |             |     |        |            |     |
tractionandVERificationWorkshop(FEVER),pages
2019. WhatdoesBERTlearnaboutthestructureof
49–57,Dubrovnik,Croatia.AssociationforCompu-
| language?                                       | InProceedingsofthe57thAnnualMeet- |           |     |                    |     |                      |               |     |      |            |            |     |
| ----------------------------------------------- | --------------------------------- | --------- | --- | ------------------ | --- | -------------------- | ------------- | --- | ---- | ---------- | ---------- | --- |
| ingoftheAssociationforComputationalLinguistics, |                                   |           |     |                    |     | tationalLinguistics. |               |     |      |            |            |     |
| pages 3651–3657,                                |                                   | Florence, |     | Italy. Association | for |                      |               |     |      |            |            |     |
|                                                 |                                   |           |     |                    |     | Zheheng              | Luo, Qianqian |     | Xie, | and Sophia | Ananiadou. |     |
ComputationalLinguistics.
2023. Chatgptasafactualinconsistencyevaluator
ZiweiJi,NayeonLee,RitaFrieske,TiezhengYu,Dan for abstractive text summarization. arXiv preprint
| Su, Yan | Xu, | Etsuko | Ishii, | Ye Jin Bang, | Andrea | arXiv:2303.15621. |     |     |     |     |     |     |
| ------- | --- | ------ | ------ | ------------ | ------ | ----------------- | --- | --- | --- | --- | --- | --- |
9013

Andrey Malinin and Mark Gales. 2021. Uncertainty AnthonyJViera,JoanneMGarrett,etal.2005. Under-
estimationinautoregressivestructuredprediction. In standinginterobserveragreement: thekappastatistic.
International Conference on Learning Representa- Fammed,37(5):360–363.
tions.
|     |     |     |     |     |     | Ben Wang | and         | Aran Komatsuzaki. |     | 2021.          | GPT-J- |
| --- | --- | --- | --- | --- | --- | -------- | ----------- | ----------------- | --- | -------------- | ------ |
|     |     |     |     |     |     | 6B:      | A 6 Billion | Parameter         |     | Autoregressive | Lan-   |
PotsaweeManakul,AdianLiusie,andMarkJFGales.
https://github.com/kingoflolz/
| 2023. MQAG:Multiple-choicequestionanswering |     |     |     |     |     | guageModel. |     |     |     |     |     |
| ------------------------------------------- | --- | --- | --- | --- | --- | ----------- | --- | --- | --- | --- | --- |
andgenerationforassessinginformationconsistency mesh-transformer-jax.
| insummarization. |     | arXivpreprintarXiv:2301.12307. |     |     |     |     |     |     |     |     |     |
| ---------------- | --- | ------------------------------ | --- | --- | --- | --- | --- | --- | --- | --- | --- |
XuezhiWang,JasonWei,DaleSchuurmans,QuocVLe,
Joshua Maynez, Shashi Narayan, Bernd Bohnet, and EdH.Chi,SharanNarang,AakankshaChowdhery,
Ryan McDonald. 2020. On faithfulness and factu- andDennyZhou.2023. Self-consistencyimproves
|                                  |     |     |     |               |     | chainofthoughtreasoninginlanguagemodels. |     |     |     |     | In  |
| -------------------------------- | --- | --- | --- | ------------- | --- | ---------------------------------------- | --- | --- | --- | --- | --- |
| alityinabstractivesummarization. |     |     |     | InProceedings |     |                                          |     |     |     |     |     |
of the 58th Annual Meeting of the Association for TheEleventhInternationalConferenceonLearning
| Computational | Linguistics, |     | pages | 1906–1919, | On- | Representations. |     |     |     |     |     |
| ------------- | ------------ | --- | ----- | ---------- | --- | ---------------- | --- | --- | --- | --- | --- |
line.AssociationforComputationalLinguistics.
AdinaWilliams,NikitaNangia,andSamuelBowman.
Sewon Min, Kalpesh Krishna, Xinxi Lyu, Mike 2018. A broad-coverage challenge corpus for sen-
|                |      |      |          |       |        | tenceunderstandingthroughinference. |     |     |     |     | InProceed- |
| -------------- | ---- | ---- | -------- | ----- | ------ | ----------------------------------- | --- | --- | --- | --- | ---------- |
| Lewis, Wen-tau | Yih, | Pang | Wei Koh, | Mohit | Iyyer, |                                     |     |     |     |     |            |
ingsofthe2018ConferenceoftheNorthAmerican
| Luke Zettlemoyer, |     | and Hannaneh |     | Hajishirzi. | 2023. |     |     |     |     |     |     |
| ----------------- | --- | ------------ | --- | ----------- | ----- | --- | --- | --- | --- | --- | --- |
Factscore: Fine-grainedatomicevaluationoffactual Chapter of the Association for Computational Lin-
precisioninlongformtextgeneration. arXivpreprint guistics: Human Language Technologies, Volume
arXiv:2305.14251. 1 (Long Papers), pages 1112–1122, New Orleans,
Louisiana.AssociationforComputationalLinguis-
| ColinRaffel,NoamShazeer,AdamRoberts,Katherine |     |     |     |     |     | tics. |     |     |     |     |     |
| --------------------------------------------- | --- | --- | --- | --- | --- | ----- | --- | --- | --- | --- | --- |
Lee,SharanNarang,MichaelMatena,YanqiZhou,
|                          |     |     |                    |     |     | Yijun Xiao | and | William | Yang | Wang. 2021. | On hal- |
| ------------------------ | --- | --- | ------------------ | --- | --- | ---------- | --- | ------- | ---- | ----------- | ------- |
| WeiLi,andPeterJLiu.2020. |     |     | Exploringthelimits |     |     |            |     |         |      |             |         |
oftransferlearningwithaunifiedtext-to-texttrans- lucinationandpredictiveuncertaintyinconditional
former. TheJournalofMachineLearningResearch, languagegeneration. InProceedingsofthe16thCon-
| 21(1):5485–5551. |     |     |     |     |     | ferenceoftheEuropeanChapteroftheAssociation |     |     |     |                  |     |
| ---------------- | --- | --- | --- | --- | --- | ------------------------------------------- | --- | --- | --- | ---------------- | --- |
|                  |     |     |     |     |     | forComputationalLinguistics:                |     |     |     | MainVolume,pages |     |
2734–2744,Online.AssociationforComputational
| VatsalRainaandMarkGales.2022. |     |     | Answeruncertainty |     |     |     |     |     |     |     |     |
| ----------------------------- | --- | --- | ----------------- | --- | --- | --- | --- | --- | --- | --- | --- |
Linguistics.
andunanswerabilityinmultiple-choicemachineread-
| ingcomprehension. |     | InFindingsoftheAssociation |     |     |     |     |     |     |     |     |     |
| ----------------- | --- | -------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
WeizheYuan,GrahamNeubig,andPengfeiLiu.2021.
| for Computational |     | Linguistics: | ACL | 2022, | pages |     |     |     |     |     |     |
| ----------------- | --- | ------------ | --- | ----- | ----- | --- | --- | --- | --- | --- | --- |
1020–1034,Dublin,Ireland.AssociationforCompu- Bartscore: Evaluating generated text as text gener-
tationalLinguistics. ation. AdvancesinNeuralInformationProcessing
Systems,34:27263–27277.
PranavRajpurkar,JianZhang,KonstantinLopyrev,and
|                  |     |                            |     |     |     | Susan Zhang, |     | Stephen Roller, |     | Naman Goyal, | Mikel |
| ---------------- | --- | -------------------------- | --- | --- | --- | ------------ | --- | --------------- | --- | ------------ | ----- |
| PercyLiang.2016. |     | SQuAD:100,000+questionsfor |     |     |     |              |     |                 |     |              |       |
Artetxe,MoyaChen,ShuohuiChen,ChristopherDe-
| machinecomprehensionoftext. |     |     | InProceedingsof |     |     |     |     |     |     |     |     |
| --------------------------- | --- | --- | --------------- | --- | --- | --- | --- | --- | --- | --- | --- |
wan,MonaDiab,XianLi,XiVictoriaLin,etal.2022.
the2016ConferenceonEmpiricalMethodsinNatu-
ralLanguageProcessing,pages2383–2392,Austin, Opt: Openpre-trainedtransformerlanguagemodels.
arXivpreprintarXiv:2205.01068.
Texas.AssociationforComputationalLinguistics.
|     |     |     |     |     |     | Zhuosheng | Zhang, | Yuwei | Wu, | Hai Zhao, | Zuchao Li, |
| --- | --- | --- | --- | --- | --- | --------- | ------ | ----- | --- | --------- | ---------- |
KurtShuster,SpencerPoff,MoyaChen,DouweKiela,
ShuailiangZhang,XiZhou,andXiangZhou.2020.
| and Jason             | Weston. | 2021.             | Retrieval | augmentation |     |                                              |     |             |            |     |               |
| --------------------- | ------- | ----------------- | --------- | ------------ | --- | -------------------------------------------- | --- | ----------- | ---------- | --- | ------------- |
|                       |         |                   |           |              |     | Semantics-awarebertforlanguageunderstanding. |     |             |            |     | In            |
| reduces hallucination |         | in conversation.  |           | In Findings  |     |                                              |     |             |            |     |               |
|                       |         |                   |           |              |     | Proceedings                                  |     | of the AAAI | Conference |     | on Artificial |
| of the Association    |         | for Computational |           | Linguistics: |     |                                              |     |             |            |     |               |
EMNLP 2021, pages 3784–3803, Punta Cana, Do- Intelligence,volume34,pages9628–9635.
| minican Republic. |     | Association | for | Computational |     |     |     |     |     |     |     |
| ----------------- | --- | ----------- | --- | ------------- | --- | --- | --- | --- | --- | --- | --- |
WanjunZhong,JingjingXu,DuyuTang,ZenanXu,Nan
Linguistics.
Duan,MingZhou,JiahaiWang,andJianYin.2020.
Reasoningoversemantic-levelgraphforfactcheck-
| James Thorne, | Andreas | Vlachos, | Oana | Cocarascu, |     |     |     |     |     |     |     |
| ------------- | ------- | -------- | ---- | ---------- | --- | --- | --- | --- | --- | --- | --- |
ing. InProceedingsofthe58thAnnualMeetingof
ChristosChristodoulopoulos,andArpitMittal.2018.
theAssociationforComputationalLinguistics,pages
| The Fact | Extraction | and VERification |     | (FEVER) |     |     |     |     |     |     |     |
| -------- | ---------- | ---------------- | --- | ------- | --- | --- | --- | --- | --- | --- | --- |
6170–6180,Online.AssociationforComputational
InProceedingsoftheFirstWorkshopon
sharedtask.
Linguistics.
FactExtractionandVERification(FEVER).
HugoTouvron,ThibautLavril,GautierIzacard,Xavier
Martinet,Marie-AnneLachaux,TimothéeLacroix,
| Baptiste         | Rozière, | Naman            | Goyal, | Eric Hambro, |           |     |     |     |     |     |     |
| ---------------- | -------- | ---------------- | ------ | ------------ | --------- | --- | --- | --- | --- | --- | --- |
| Faisal Azhar,    | et al.   | 2023.            | Llama: | Open         | and effi- |     |     |     |     |     |     |
| cient foundation |          | language models. |        | arXiv        | preprint  |     |     |     |     |     |     |
arXiv:2302.13971.
9014

A ModelsandImplementation unanswerablequestionswhichhaveαlowerthan
|     |     |     |     |     |     |     | athreshold. |     | Next,wederivehowBayes’theorem |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | ----------- | --- | ----------------------------- | --- | --- | --- | --- |
A.1 Entropy
canbeappliedtotakeintoaccountthenumberof
| The | entropy | of the | output | distribution |     | is imple- |     |     |     |     |     |     |     |
| --- | ------- | ------ | ------ | ------------ | --- | --------- | --- | --- | --- | --- | --- | --- | --- |
answerable/unanswerablequestions.
mentedasfollows,
B.1 SelfCheckGPT-QAwithBayes
|       |     |        |        | pij(w˜)log   | pij(w˜) |              |                                              |     |     |     |     |                |     |
| ----- | --- | ------ | ------ | ------------ | ------- | ------------ | -------------------------------------------- | --- | --- | --- | --- | -------------- | --- |
|       |     | = 2    | w˜     |              | 2       | (13)         |                                              |     |     |     |     |                |     |
|       |     | H ij   | − ∈W   |              |         |              | LetP(F)denotetheprobabilityofthei-thsentence |     |     |     |     |                |     |
|       |     |        | P      |              |         |              | beingnon-factual,andP(T)denotetheprobability |     |     |     |     |                |     |
| where |     | is the | set of | all possible |         | words in the |                                              |     |     |     |     |                |     |
|       | W   |        |        |              |         |              | ofthei-thsentencebeingfactual.               |     |     |     |     | Foraquestionq, |     |
vocabulary.
theprobabilityofi-thsentencebeingnon-factual
A.2 ProxyLLMs given a set of matched answers L m and a set of
|                       |                       |              |            |             |                |            | not-matchedanswersL |       |      |            | is:       |           |      |
| --------------------- | --------------------- | ------------ | ---------- | ----------- | -------------- | ---------- | ------------------- | ----- | ---- | ---------- | --------- | --------- | ---- |
| The                   | proxy                 | LLMs         | considered |             | are LLaMA-{7B, |            |                     |       |      |            | n         |           |      |
| 13B,                  | 30B}                  | (Touvron     | et         | al., 2023), |                | OPT-{125m, |                     |       |      |            |           |           |      |
|                       |                       |              |            |             |                |            |                     | P(F L | ,L ) |            |           |           |      |
|                       |                       |              |            |             |                |            |                     | |     | m n  |            |           |           |      |
| 1.3B,                 | 13B,                  | 30B}         | (Zhang     | et al.,     | 2022),         | GPT-J-6B   |                     |       |      |            |           |           |      |
|                       |                       |              |            |             |                |            |                     |       |      | P(L        | ,L F)P(F) |           |      |
|                       |                       |              |            |             |                |            |                     |       |      | m          | n         |           |      |
| (Wang                 | and                   | Komatsuzaki, |            | 2021)       | and            | GPT-NeoX-  |                     | =     |      |            | |         |           |      |
|                       |                       |              |            |             |                |            |                     | P(L   | ,L   | F)P(F)+P(L |           | ,L T)P(T) |      |
| 20B(Blacketal.,2022). |                       |              |            |             |                |            |                     |       | m n  |            |           | m n       |      |
|                       |                       |              |            |             |                |            |                     |       |      | |          |           | |         |      |
|                       |                       |              |            |             |                |            |                     |       | P(L  | ,L         | F)        |           |      |
|                       |                       |              |            |             |                |            |                     |       |      | m          | n         |           |      |
|                       |                       |              |            |             |                |            |                     | =     |      |            | |         |           | (16) |
| A.3                   | SelfCheckGPT’sSystems |              |            |             |                |            |                     | P(L   | ,L   | F)+P(L     | ,L        | T)        |      |
|                       |                       |              |            |             |                |            |                     |       | m n  |            | m         | n         |      |
|                       |                       |              |            |             |                |            |                     |       |      | |          |           | |         |      |
| Question              |                       | Answering:   |            | The         | generation     | systems    |                     |       |      |            |           |           |      |
whereweassumethesentenceisequallylikelyto
| G1         | and G2        | are T5-Large |       | fine-tuned |      | to SQuAD     |                    |     |     |        |                        |                    |     |
| ---------- | ------------- | ------------ | ----- | ---------- | ---- | ------------ | ------------------ | --- | --- | ------ | ---------------------- | ------------------ | --- |
|            |               |              |       |            |      |              | beFalseorTrue,i.e. |     |     | P(F)   | =                      | P(T). Theprobabil- |     |
| (Rajpurkar |               | et al.,      | 2016) | and        | RACE | (Lai et al., |                    |     |     |        |                        |                    |     |
|            |               |              |       |            |      |              | ityofobservingL    |     |     | m ,L n | whenthesentenceisFalse |                    |     |
| 2017),     | respectively. |              | The   | answering  |      | system A is  |                    |     |     |        |                        |                    |     |
(non-factual):
Longformer(Beltagyetal.,2020)fine-tunedtothe
| RACEdataset. |     | TheanswerabilitysystemUisalso |     |     |     |     |     | P(L | ,L F) |     |     |     |     |
| ------------ | --- | ----------------------------- | --- | --- | --- | --- | --- | --- | ----- | --- | --- | --- | --- |
|              |     |                               |     |     |     |     |     | m   | n |   |     |     |     |     |
Longformer,butfine-tunedtoSQuAD2.0.
|        |                    |            |        |             |         |              |                            | =    | P(a   | = a | F)   | P(a ′ =        | a F) |
| ------ | ------------------ | ---------- | ------ | ----------- | ------- | ------------ | -------------------------- | ---- | ----- | --- | ---- | -------------- | ---- |
|        |                    |            |        |             |         |              |                            |      |       | R   | |    | ̸              | R |  |
|        |                    |            |        |             |         |              |                            | a    | Lm    |     | a Ln |                |      |
| LLM    | for                | Prompting: |        | We consider |         | two LLMs,    |                            | Y∈   |       |     | Y′∈  |                |      |
|        |                    |            |        |             |         |              |                            |      | )Nm(β | )Nn |      |                |      |
|        |                    |            |        |             |         |              |                            | = (1 | β 1   | 1   |      |                | (17) |
| GPT-3  | (text-davinci-003) |            |        | and         | ChatGPT | (gpt-3.5-    |                            |      | −     |     |      |                |      |
| turbo) | We                 | note that  | during | the         | data    | creation and |                            |      |       |     |      |                |      |
|        |                    |            |        |             |         |              | andprobabilityofobservingL |      |       |     |      | ,L whenthesen- |      |
m n
annotation,GPT-3(text-davinci-003)wasthestate-
tenceisTrue(factual):
of-the-artLLMavailable;hence,GPT-3wasused
asthemainLLMgeneratingWikiBiopassages.
|     |     |     |     |     |     |     |     | P(L | m ,L n T) |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --------- | --- | --- | --- | --- |
|
|     |                    |     |     |     |     |     |     | =    | P(a | = a | T)       | P(a = | a T) |
| --- | ------------------ | --- | --- | --- | --- | --- | --- | ---- | --- | --- | -------- | ----- | ---- |
| B   | SelfCheckGPTwithQA |     |     |     |     |     |     |      |     | r   |          | ′     | r    |
|     |                    |     |     |     |     |     |     |      |     |     | |        | ̸     | |    |
|     |                    |     |     |     |     |     |     | a Y∈ | Lm  |     | a Y′∈ Ln |       |      |
Previousworkshowedthatimplementingquestion
|                                             |     |     |     |     |     |     |     | = (β | )Nm(1 | β   | )Nn |     | (18) |
| ------------------------------------------- | --- | --- | --- | --- | --- | --- | --- | ---- | ----- | --- | --- | --- | ---- |
|                                             |     |     |     |     |     |     |     |      | 2     | 2   |     |     |      |
| generation(inEquation2)withtwogenerators(G1 |     |     |     |     |     |     |     |      |       | −   |     |     |      |
generatesthequestionandassociatedanswer,and where N and N are the number of matched an-
|     |     |     |     |     |     |     |     | m   |     | n   |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
G2generatesdistractors)yieldshigher-qualitydis-
swersandthenumberofnot-matchedanswers,re-
tractors(Manakuletal.,2023). Thus,atwo-stage spectively. Hence,wecansimplifyEquation16:
generationisadoptedinthisworkasfollows:
γNn
|     |     |           |        |     |         |        |     |     | P(F | L ,L | ) = | 2    |      |
| --- | --- | --------- | ------ | --- | ------- | ------ | --- | --- | --- | ---- | --- | ---- | ---- |
|     |     |           |        |     |         |        |     |     |     | m n  |     |      | (19) |
|     | q,a | P G1 (q,a | r i ); | o   | P G2 (o | q,a,R) |     |     | |   |      | γNm | +γNn |      |
|     | ∼   |           | |      | a ∼ |         | a |    |     |     |     |      | 1   | 2    |      |
|     |     |           |        | \   |         | \ (14) |     |     |     |      |     |      |      |
whereo = a,o = o ,...,o . Inaddition,to whereγ = β2 andγ = β1 . Lastly,instead
|     |     |     | a   | 1   | 4   |     |     | 1   | 1 β |     | 2 1 | β   |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|     |     | { \ | } { |     | }   |     |     |     | −m  | 1   | n−a | 2   |     |
filteroutba d(un a n swer ab le)que s tions,wedefine ofreject ingsa p leshav inga n swerabilityscore
threshold,7
ananswerabilityscore(RainaandGales,2022): below a we find empirically that soft-
|     |     |                   |     |     |            |      | counting     |     | (defined   | below) | improves | the         | detection |
| --- | --- | ----------------- | --- | --- | ---------- | ---- | ------------ | --- | ---------- | ------ | -------- | ----------- | --------- |
|     |     | α = P (answerable |     |     | q,context) | (15) |              |     |            |        |          |             |           |
|     |     | U                 |     |     |            |      | performance. |     | Wesetbothβ |        |          | andβ to0.8. |           |
|     |     |                   |     | |   |            |      |              |     |            |        | 1        | 2           |           |
wherethecontextiseithertheresponseRorsam- 7αisbetween0.0(unanswerable)and1.0(answerable).
|                     |     |     |     |                    |     |     | Standard-countingN                                  |     |     | mandN | ncanbeconsideredasaspecial |     |     |
| ------------------- | --- | --- | --- | ------------------ | --- | --- | --------------------------------------------------- | --- | --- | ----- | -------------------------- | --- | --- |
| pledpassagesSn,andα |     |     |     | 0.0forunanswerable |     |     |                                                     |     |     |       |                            |     |     |
|                     |     |     |     | →                  |     |     | caseofsoft-countingwhereαissetto1.0ifαisgreaterthan |     |     |       |                            |     |     |
andα 1.0foranswerable. Weuseαtofilterout theanswerabilitythresholdandotherwiseαis0.0.
→
9015

| N   | =     | α       | ; N | =          | α (20) |     |        | Sent-lvlAUC-PR |        |      |       | Passage-lvl |
| --- | ----- | ------- | --- | ---------- | ------ | --- | ------ | -------------- | ------ | ---- | ----- | ----------- |
|     | m′    |         | n   | n′         | n      |     | n-gram |                |        |      |       |             |
|     |       |         |     |            |        |     |        | NoFac          | NoFac* | Fact | Pear. | Spear.      |
|     | n s.t | . an Lm |     | n s.t . an | Ln     |     |        |                |        |      |       |             |
|     |       | X ∈     |     | X          | ∈      |     |        |                |        |      |       |             |
Avg( logp)
−
whereα = P (answerable q,Sn). Therefore,the 1-gra m 81.52 40.33 41.76 40.68 39.22
|                          | n   | U   |     |      |     |     |        |       |       |       |       |       |
| ------------------------ | --- | --- | --- | ---- | --- | --- | ------ | ----- | ----- | ----- | ----- | ----- |
|                          |     |     |     | |    |     |     | 2-gram | 82.94 | 44.38 | 52.81 | 58.84 | 58.11 |
| SelfCheckGPTwithQAscore, |     |     |     | ,is: |     |     |        |       |       |       |       |       |
|                          |     |     |     | S QA |     |     | 3-gram | 83.56 | 44.64 | 53.99 | 62.21 | 63.00 |
|                          |     |     |     |      |     |     | 4-gram | 83.80 | 43.55 | 54.25 | 61.98 | 63.64 |
N
|     |     |       |      | γ n′      |      |     | 5-gram | 83.45 | 42.31 | 53.98 | 60.68 | 62.96 |
| --- | --- | ----- | ---- | --------- | ---- | --- | ------ | ----- | ----- | ----- | ----- | ----- |
|     | =   | P(F L | ,L ) | = 2       | (21) |     |        |       |       |       |       |       |
|     | QA  | m     | n    |           |      |     | Max(   | logp) |       |       |       |       |
|     | S   | |     |      | γ N m′ +γ | N n′ |     | −      |       |       |       |       |       |
|     |     |       |      | 1         | 2    |     | 1-gram | 85.63 | 41.04 | 58.47 | 64.71 | 64.91 |
|     |     |       |      |           |      |     | 2-gram | 85.26 | 39.29 | 58.29 | 62.48 | 66.04 |
InTable5,weshowempicallythatapplyingBayes’
|     |     |     |     |     |     |     | 3-gram | 84.97 | 37.10 | 57.08 | 57.34 | 60.49 |
| --- | --- | --- | --- | --- | --- | --- | ------ | ----- | ----- | ----- | ----- | ----- |
theoremandsoftcountingα(inEquation20)im- 4-gram 84.49 36.37 55.96 55.77 57.25
|     |     |     |     |     |     |     | 5-gram | 84.12 | 36.19 | 54.89 | 54.84 | 55.97 |
| --- | --- | --- | --- | --- | --- | --- | ------ | ----- | ----- | ----- | ----- | ----- |
provestheperformanceoftheSelfCheckGPTwith
QAmethod.
Table7:Theperformanceusingdifferentn-grammodelsin
theSelfCheckGPTwithn-grammethod.
|     |     | Sentence-lvl |     |     | Passage-lvl |     |     |     |     |     |     |     |
| --- | --- | ------------ | --- | --- | ----------- | --- | --- | --- | --- | --- | --- | --- |
Varaint
|     |             | NoF   | NoF*  | Fact PCC    | SCC   |     |     |     |     |     |     |     |
| --- | ----------- | ----- | ----- | ----------- | ----- | --- | --- | --- | --- | --- | --- | --- |
|     | SimpleCount | 83.97 | 40.07 | 47.78 57.39 | 55.15 |     |     |     |     |     |     |     |
|     | +Bayes      | 83.04 | 38.58 | 47.41 56.43 | 55.03 |     |     |     |     |     |     |     |
|     | +Bayes+α    | 84.26 | 40.06 | 48.14 61.07 | 59.29 |     |     |     |     |     |     |     |
92.5
Table5:PerformanceofSelfCheckGPT-QA’svariants.
90.0
87.5
| C   | SelfCheckGPTwithPrompt |     |     |     |     |     | RP-CUA |     |     |     |     |     |
| --- | ---------------------- | --- | --- | --- | --- | --- | ------ | --- | --- | --- | --- | --- |
85.0
| Weusetheprompttemplateprovidedinthemain |     |     |     |     |     |     | 82.5 |     |     |     |     |     |
| --------------------------------------- | --- | --- | --- | --- | --- | --- | ---- | --- | --- | --- | --- | --- |
SelfCk-BERTScore
| text(inSection5.5)forbothGPT-3(text-davinci- |     |     |     |     |     |     |     |     |     |     | SelfCk-QA |     |
| -------------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --------- | --- |
80.0
SelfCk-Unigram
| 003)andChatGPT(gpt-3.5-turbo). |     |     |     | ForChatGPT, |     |     |     |     |     |     | SelfCk-NLI |     |
| ------------------------------ | --- | --- | --- | ----------- | --- | --- | --- | --- | --- | --- | ---------- | --- |
77.5
| astandardsystemmessage"You             |     |     |     | are | a helpful |     |     |     |              |       | SelfCk-Prompt |       |
| -------------------------------------- | --- | --- | --- | --- | --------- | --- | --- | --- | ------------ | ----- | ------------- | ----- |
|                                        |     |     |     |     |           |     |     | 0 2 | 4 6 8        | 10 12 | 14 16         | 18 20 |
| assistant."isusedinsettingupthesystem. |     |     |     |     |           |     |     |     | Num. samples |       |               |       |
Atthetimeofconductingexperiments,theAPI
|     |     |     |     |     |     | Figure8: |     | TheperformanceofSelfCheckGPTmethodson |     |     |     |     |
| --- | --- | --- | --- | --- | --- | -------- | --- | ------------------------------------- | --- | --- | --- | --- |
costs per 1,000 tokens are $0.020 for GPT-3 and sentence-level non-factual detection (AUC-PR) versus the
$0.002forChatGPT.Theestimatedcostsforrun- numberofsamples. ThisFigureextendsthepassage-level
resultsinFigure7.
ningthemodelstoanswerYes/Noonall1908sen-
tencesand20samplesarearound$200forGPT-3
and$20forChatGPT.Giventhecost,weconduct
| the | experiments | on  | 4 samples | when | performing |     |     |     |     |     |     |     |
| --- | ----------- | --- | --------- | ---- | ---------- | --- | --- | --- | --- | --- | --- | --- |
theablationaboutLLMchoiceforSelfCheckGPT-
40
| Prompt(Section7.3). |     |     | Table6showsthebreakdown |     |     |     |     |     |     |     |     |     |
| ------------------- | --- | --- | ----------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
30
ofpredictionsmadebyGPT-3andChatGPT.
20
namraepS
|     |     | ChatGPT |     | Yes | No  |     |     |     |     |     |     |     |
| --- | --- | ------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
10
GPT-3
|     |     | Yes |     | 3179 | 1038 |     |     | 0   |     |     |     |     |
| --- | --- | --- | --- | ---- | ---- | --- | --- | --- | --- | --- | --- | --- |
|     |     | No  |     | 367  | 3048 |     |     |     |     |     |     |     |
LLaMA
10
OPT,GPT-J,NeoX
Table6:BreakdownofpredictionsmadebyGPT-3/ChatGPT
|                                                       |     |     |     |     |     |     |     | m .3B | 6B  | 13B | 20B | 30B |
| ----------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- | ----- | --- | --- | --- | --- |
| whenpromptedtoanswerYes(supported)/No(not-supported). |     |     |     |     |     |     |     | 1251  |     |     |     |     |
Model Size
|     |     |     |     |     |     | Figure9:Passage-levelrankingperformanceoftheAvg( |     |     |     |     |     | )   |
| --- | --- | --- | --- | --- | --- | ------------------------------------------------ | --- | --- | --- | --- | --- | --- |
D AdditionalExperimentalResults
|     |     |     |     |     |     | methodusingproxyLLMwherethesizesare:LLaMA={7B, |       |            |       |      |       | H         |
| --- | --- | --- | --- | --- | --- | ---------------------------------------------- | ----- | ---------- | ----- | ---- | ----- | --------- |
|     |     |     |     |     |     | 13B,                                           | 30B}, | OPT={125m, | 1.3B, | 13B, | 30B}, | GPT-J=6B, |
Here,weprovideexperimentalresultsthatarecom-
NeoX=20B.ThefullresultsareprovidedinTable8.
| plementary |     | to those | presented | in the | main paper. |     |     |     |     |     |     |     |
| ---------- | --- | -------- | --------- | ------ | ----------- | --- | --- | --- | --- | --- | --- | --- |
9016

0.8
1.0
| 0.12              |     | 0.7          |     |              | 8.0 |     |              |     |
| ----------------- | --- | ------------ | --- | ------------ | --- | --- | ------------ | --- |
|                   |     | 0.6          |     |              |     |     | 0.8          |     |
| erocS dohteM 0.10 |     | erocS dohteM |     | erocS dohteM | 7.5 |     | erocS dohteM |     |
0.5
|      |     |     |     |     | 7.0 |     | 0.6 |     |
| ---- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0.08 |     | 0.4 |     |     |     |     |     |     |
| 0.06 |     | 0.3 |     |     | 6.5 |     | 0.4 |     |
|      |     | 0.2 |     |     | 6.0 |     |     |     |
| 0.04 |     | 0.1 |     |     |     |     |     |     |
0.2
|     |     | 0.0 | 0.2 0.4 0.6 | 0.8 1.0 | 5.5 0.0 0.2 | 0.4 0.6 | 0.8 1.0 0.0 0.2 | 0.4 0.6 0.8 1.0 |
| --- | --- | --- | ----------- | ------- | ----------- | ------- | --------------- | --------------- |
0.0 Human Score (0=Factual, +1=Non-Factual) 0.2 0.4 0.6 0.8 1.0 Human Score (0=Factual, +1=Non-Factual) Human Score (0=Factual, +1=Non-Factual) Human Score (0=Factual, +1=Non-Factual)
(a)SelfCheckGPT-BERTScore (b)SelfCheckGPT-QA (c)SelfCheckGPT-1gram(max) (d)SelfCheckGPT-NLI
Figure10:Scatterplotofpassage-levelscoreswhereY-axis=Methodscores,X-axis=Humanscores.Correlationsarereported
inTable2.ThisfigureprovidesresultsinadditiontoFigure6.
|     |        |      | Sentence-level(AUC-PR) |          |         | Passage-level(Corr.) |          |     |
| --- | ------ | ---- | ---------------------- | -------- | ------- | -------------------- | -------- | --- |
|     | LLM    | Size |                        |          |         |                      |          |     |
|     |        |      | NonFact                | NonFact* | Factual | Pearson              | Spearman |     |
|     | Random | -    | 72.96                  | 29.72    | 27.04   | -                    | -        |     |
Avg( logp)Method
LLa−MA
|     |       | 30B      | 75.43 | 30.32 | 41.29 | 21.72  | 20.20  |     |
| --- | ----- | -------- | ----- | ----- | ----- | ------ | ------ | --- |
|     | LLaMA | 13B      | 74.16 | 30.01 | 37.36 | 13.33  | 12.89  |     |
|     | LLaMA | 7B       | 71.69 | 27.87 | 31.30 | -2.71  | -2.59  |     |
|     |       | OPT 30B  | 67.70 | 24.43 | 25.04 | -32.07 | -31.45 |     |
|     | NeoX  | 20B      | 69.00 | 24.38 | 26.18 | -31.79 | -34.15 |     |
|     |       | OPT 13B  | 67.46 | 24.39 | 25.20 | -33.05 | -32.79 |     |
|     | GPT-J | 6B       | 67.51 | 24.28 | 24.26 | -38.80 | -40.05 |     |
|     |       | OPT 1.3B | 66.19 | 24.47 | 23.47 | -35.20 | -38.95 |     |
|     |       | OPT 125m | 66.63 | 25.31 | 23.07 | -30.38 | -37.54 |     |
Avg( )Method
LLaHMA
|     |     | 30B | 80.80 | 39.01 | 42.97 | 33.80 | 39.49 |     |
| --- | --- | --- | ----- | ----- | ----- | ----- | ----- | --- |
LLaMA
|     |     | 13B | 80.63 | 38.98 | 40.59 | 29.43 | 33.12 |     |
| --- | --- | --- | ----- | ----- | ----- | ----- | ----- | --- |
LLaMA
|     |     | 7B  | 78.67 | 37.22 | 33.81 | 19.44 | 21.79 |     |
| --- | --- | --- | ----- | ----- | ----- | ----- | ----- | --- |
OPT
|     |     | 30B | 77.13 | 33.67 | 29.55 | -0.43 | 3.43 |     |
| --- | --- | --- | ----- | ----- | ----- | ----- | ---- | --- |
NeoX
|     |     | 20B | 77.40 | 32.78 | 30.13 | 5.41 | 7.43 |     |
| --- | --- | --- | ----- | ----- | ----- | ---- | ---- | --- |
OPT
|     |     | 13B | 76.93 | 33.71 | 29.68 | 0.25 | 1.39 |     |
| --- | --- | --- | ----- | ----- | ----- | ---- | ---- | --- |
GPT-J
|     |     | 6B  | 76.15 | 33.29 | 28.30 | -2.50 | -1.37 |     |
| --- | --- | --- | ----- | ----- | ----- | ----- | ----- | --- |
OPT
|     |     | 1.3B | 74.05 | 31.91 | 26.33 | -10.59 | -10.00 |     |
| --- | --- | ---- | ----- | ----- | ----- | ------ | ------ | --- |
OPT
|     |     | 125m | 71.51 | 30.88 | 25.36 | -14.16 | -13.76 |     |
| --- | --- | ---- | ----- | ----- | ----- | ------ | ------ | --- |
Max( logp)Method
LLa−MA
|     |     | 30B | 74.01 | 27.14 | 31.08 | -22.83 | -22.71 |     |
| --- | --- | --- | ----- | ----- | ----- | ------ | ------ | --- |
LLaMA
|     |     | 13B | 71.12 | 26.78 | 28.82 | -34.93 | -31.70 |     |
| --- | --- | --- | ----- | ----- | ----- | ------ | ------ | --- |
LLaMA
|     |     | 7B  | 69.57 | 25.91 | 26.54 | -42.57 | -38.24 |     |
| --- | --- | --- | ----- | ----- | ----- | ------ | ------ | --- |
OPT
|     |     | 30B | 67.32 | 24.40 | 24.32 | -49.51 | -45.50 |     |
| --- | --- | --- | ----- | ----- | ----- | ------ | ------ | --- |
NeoX
|     |     | 20B | 67.51 | 23.88 | 24.82 | -47.96 | -44.54 |     |
| --- | --- | --- | ----- | ----- | ----- | ------ | ------ | --- |
OPT
|     |     | 13B | 67.36 | 24.67 | 24.46 | -50.15 | -44.42 |     |
| --- | --- | --- | ----- | ----- | ----- | ------ | ------ | --- |
GPT-J
|     |     | 6B  | 67.58 | 23.94 | 23.93 | -51.23 | -47.68 |     |
| --- | --- | --- | ----- | ----- | ----- | ------ | ------ | --- |
OPT
|     |     | 1.3B | 68.16 | 25.85 | 24.66 | -45.60 | -42.39 |     |
| --- | --- | ---- | ----- | ----- | ----- | ------ | ------ | --- |
OPT
|     |     | 125m | 69.23 | 27.66 | 24.14 | -39.22 | -37.18 |     |
| --- | --- | ---- | ----- | ----- | ----- | ------ | ------ | --- |
Max( )Method
LLaHMA
|     |     | 30B | 80.92 | 37.32 | 37.90 | 35.57 | 38.94 |     |
| --- | --- | --- | ----- | ----- | ----- | ----- | ----- | --- |
LLaMA
|     |     | 13B | 80.98 | 37.94 | 36.01 | 32.07 | 34.01 |     |
| --- | --- | --- | ----- | ----- | ----- | ----- | ----- | --- |
LLaMA
|     |     | 7B  | 79.65 | 35.57 | 31.32 | 22.10 | 22.53 |     |
| --- | --- | --- | ----- | ----- | ----- | ----- | ----- | --- |
OPT
|     |     | 30B | 76.58 | 33.44 | 29.31 | 1.63 | 6.41 |     |
| --- | --- | --- | ----- | ----- | ----- | ---- | ---- | --- |
NeoX
|     |       | 20B      | 76.98 | 31.96 | 29.13 | 5.97   | 9.31   |     |
| --- | ----- | -------- | ----- | ----- | ----- | ------ | ------ | --- |
|     |       | OPT 13B  | 76.26 | 32.81 | 29.25 | 1.42   | 2.82   |     |
|     | GPT-J | 6B       | 75.30 | 32.51 | 28.13 | -2.14  | 1.41   |     |
|     |       | OPT 1.3B | 73.79 | 31.42 | 26.38 | -9.84  | -9.80  |     |
|     |       | OPT 125m | 71.32 | 31.65 | 25.36 | -18.05 | -17.37 |     |
Table8:AUC-PRforDetectingNon-FactualandFactualSentencesintheGPT-3generatedWikiBiopassages.Passage-level
PCCandSCCwithLLMsusedtoassessGPT-3responses.ThistableisanextensiontoTable2.
9017