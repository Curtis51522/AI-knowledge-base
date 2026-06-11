G-EVAL: NLG Evaluation using GPT-4 with Better Human Alignment
|     |     |     |              | YangLiu |     | DanIter   |     | YichongXu    |     |     |     |     |     |
| --- | --- | --- | ------------ | ------- | --- | --------- | --- | ------------ | --- | --- | --- | --- | --- |
|     |     |     | ShuohangWang |         |     | RuochenXu |     | ChenguangZhu |     |     |     |     |     |
MicrosoftAzureAI
yaliu10@microsoft.com
|     |     | Abstract |     |     |     |     | Moreover, |     | these metrics | require | associated |     | refer- |
| --- | --- | -------- | --- | --- | --- | --- | --------- | --- | ------------- | ------- | ---------- | --- | ------ |
enceoutput,whichiscostlytocollectfornewtasks.
Thequalityoftextsgeneratedbynaturallan-
RecentstudiesproposedirectlyusingLLMsas
| guage | generation |     | (NLG) | systems | is hard | to  |                |     |     |            |     |         |       |
| ----- | ---------- | --- | ----- | ------- | ------- | --- | -------------- | --- | --- | ---------- | --- | ------- | ----- |
|       |            |     |       |         |         |     | reference-free |     | NLG | evaluators | (Fu | et al., | 2023; |
measureautomatically.Conventionalreference-
based metrics, such as BLEU and ROUGE, Wangetal.,2023a). TheideaistousetheLLMsto
have been shown to have relatively low cor- scorethecandidateoutputbasedonitsgeneration
relationwithhumanjudgments,especiallyfor probabilitywithoutanyreferencetarget,underthe
| tasksthatrequirecreativityanddiversity. |     |     |     |     |     | Re- |     |     |     |     |     |     |     |
| --------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
assumptionthattheLLMshavelearnedtoassign
centstudiessuggestusinglargelanguagemod- higherprobabilitiestohigh-qualityandfluenttexts.
els(LLMs)asreference-freemetricsforNLG
|     |     |     |     |     |     |     | Meanwhile, |     | it is becoming |     | popular | to use | more |
| --- | --- | --- | --- | --- | --- | --- | ---------- | --- | -------------- | --- | ------- | ------ | ---- |
evaluation,whichhavethebenefitofbeingap-
powerfulLLMslikeGPT-4toevaluatesmalleror
| plicable | to  | new tasks | that | lack | human | refer- |     |     |     |     |     |     |     |
| -------- | --- | --------- | ---- | ---- | ----- | ------ | --- | --- | --- | --- | --- | --- | --- |
studentmodels,likeinAlpaca(Taorietal.,2023)
| ences. | However,theseLLM-basedevaluators |       |                |     |     |      |     |        |        |         |        |          |     |
| ------ | -------------------------------- | ----- | -------------- | --- | --- | ---- | --- | ------ | ------ | ------- | ------ | -------- | --- |
|        |                                  |       |                |     |     |      | and | Vicuna | (Zheng | et al., | 2023). | However, | the |
| still  | have lower                       | human | correspondence |     |     | than |     |        |        |         |        |          |     |
medium-size neural evaluators. In this work, validityandreliabilityofusingLLMsasNLGeval-
| we present |     | G-EVAL, | a framework |     | of  | using |        |      |          |                |     |               |     |
| ---------- | --- | ------- | ----------- | --- | --- | ----- | ------ | ---- | -------- | -------------- | --- | ------------- | --- |
|            |     |         |             |     |     |       | uators | have | not been | systematically |     | investigated. |     |
largelanguagemodelswithchain-of-thoughts Inaddition,meta-evaluationsshowthattheseLLM-
(CoT)andaform-fillingparadigm,toassessthe
basedevaluatorsstillhavelowerhumancorrespon-
| qualityofNLGoutputs. |     |     | Weexperimentwith |     |     |     |     |     |     |     |     |     |     |
| -------------------- | --- | --- | ---------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
dencethanmedium-sizeneuralevaluators(Zhong
twogenerationtasks,textsummarizationand
|          |             |     |     |      |             |     | et al., | 2022). | Thus, there | is  | a need | for a | more ef- |
| -------- | ----------- | --- | --- | ---- | ----------- | --- | ------- | ------ | ----------- | --- | ------ | ----- | -------- |
| dialogue | generation. |     | We  | show | that G-EVAL |     |         |        |             |     |        |       |          |
fectiveandreliableframeworkforusingLLMsfor
withGPT-4asthebackbonemodelachievesa
| Spearmancorrelationof0.514withhumanon |     |     |     |     |     |     | NLGevaluation. |     |     |     |     |     |     |
| ------------------------------------- | --- | --- | --- | --- | --- | --- | -------------- | --- | --- | --- | --- | --- | --- |
summarizationtask,outperformingallprevious
|                        |     |     |     |               |     |     | Inthispaper,wepropose |     |     |     | G-EVAL,aframework |     |     |
| ---------------------- | --- | --- | --- | ------------- | --- | --- | --------------------- | --- | --- | --- | ----------------- | --- | --- |
| methodsbyalargemargin. |     |     |     | Wealsopropose |     |     |                       |     |     |     |                   |     |     |
ofusingLLMswithchain-of-thoughts(CoT)(Wei
| analysis | on  | the behavior |     | of LLM-based |     | eval- |         |       |             |     |         |              |     |
| -------- | --- | ------------ | --- | ------------ | --- | ----- | ------- | ----- | ----------- | --- | ------- | ------------ | --- |
|          |     |              |     |              |     |       | et al., | 2022) | to evaluate | the | quality | of generated |     |
uators,andhighlightthepotentialconcernof
|     |     |     |     |     |     |     | textsinaform-fillingparadigm. |     |     |     | Byonlyfeeding |     |     |
| --- | --- | --- | --- | --- | --- | --- | ----------------------------- | --- | --- | --- | ------------- | --- | --- |
LLM-basedevaluatorshavingabiastowards
theLLM-generatedtexts. 1 theTaskIntroductionandtheEvaluationCriteria
|                |     |     |     |     |     |     | as a                     | prompt, | we ask | LLMs               | to generate | a   | CoT of |
| -------------- | --- | --- | --- | --- | --- | --- | ------------------------ | ------- | ------ | ------------------ | ----------- | --- | ------ |
| 1 Introduction |     |     |     |     |     |     | detailedEvaluationSteps. |         |        | Thenweusetheprompt |             |     |        |
alongwiththegeneratedCoTtoevaluatetheNLG
Evaluatingthequalityofnaturallanguagegenera-
|     |     |     |     |     |     |     | outputs. | The | evaluator | output | is formatted |     | as a |
| --- | --- | --- | --- | --- | --- | --- | -------- | --- | --------- | ------ | ------------ | --- | ---- |
tionsystemsisachallengingproblemevenwhen
|                    |       |        |               |                   |              |        | form.           | Moreover,  | the        | probabilities |             | of the    | output   |
| ------------------ | ----- | ------ | ------------- | ----------------- | ------------ | ------ | --------------- | ---------- | ---------- | ------------- | ----------- | --------- | -------- |
| large language     |       | models | can           | generate          | high-quality |        |                 |            |            |               |             |           |          |
|                    |       |        |               |                   |              |        | rating          | tokens     | can be     | used to       | refine      | the final | met-     |
| and diverse        | texts | that   | are often     | indistinguishable |              |        |                 |            |            |               |             |           |          |
|                    |       |        |               |                   |              |        | ric.            | We conduct | extensive  |               | experiments |           | on three |
| from human-written |       |        | texts (Ouyang |                   | et al.,      | 2022). |                 |            |            |               |             |           |          |
|                    |       |        |               |                   |              |        | meta-evaluation |            | benchmarks |               | of two      | NLG       | tasks:   |
Traditionalautomaticmetrics,suchasBLEU(Pap-
|     |     |     |     |     |     |     | textsummarizationanddialoguegeneration. |     |     |     |     |     | The |
| --- | --- | --- | --- | --- | --- | --- | --------------------------------------- | --- | --- | --- | --- | --- | --- |
inenietal.,2002),ROUGE(Lin,2004),andME-
resultsshowthatG-EVALcanoutperformexisting
TEOR(BanerjeeandLavie,2005),arewidelyused
NLGevaluatorsbyalargemarginintermsofcorre-
forNLGevaluation,buttheyhavebeenshownto
|                 |     |                 |     |      |       |       | lationwithhumanevaluations. |     |     |     | Finally,weconduct |     |     |
| --------------- | --- | --------------- | --- | ---- | ----- | ----- | --------------------------- | --- | --- | --- | ----------------- | --- | --- |
| have relatively |     | low correlation |     | with | human | judg- |                             |     |     |     |                   |     |     |
analysisonthebehaviorofLLM-basedevaluators,
ments,especiallyforopen-endedgenerationtasks.
|     |     |     |     |     |     |     | and | highlight | the potential |     | issue of | LLM-based |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --------- | ------------- | --- | -------- | --------- | --- |
1https://github.com/nlpyang/geval evaluatorhavingabiastowardstheLLM-generated
2511
Proceedingsofthe2023ConferenceonEmpiricalMethodsinNaturalLanguageProcessing,pages2511–2522
December6-10,2023©2023AssociationforComputationalLinguistics

| texts. |     |     |     |     |     |     | Thepromptshouldalsocontaincustomizedeval- |     |     |     |     |     |     |
| ------ | --- | --- | --- | --- | --- | --- | ----------------------------------------- | --- | --- | --- | --- | --- | --- |
Tosummarize,ourmaincontributionsandfind- uationcriteriafordifferentNLGtasksand,suchas
ingsinthispaperare: coherence,conciseness,orgrammar. Forexample,
forevaluatingcoherenceintextsummarization,we
| 1. G-EVAL |     | generally | outperforms |     | reference- |     |     |     |     |     |     |     |     |
| --------- | --- | --------- | ----------- | --- | ---------- | --- | --- | --- | --- | --- | --- | --- | --- |
addthefollowingcontenttotheprompt:
basedandreference-freebaselinemetricsin
termsofcorrelationwithhumanqualityjudg-
EvaluationCriteria:
ments,especiallyforopen-endedandcreative
Coherence(1-5)-thecollectivequality
NLGtasks,suchasdialogueresponsegenera-
|     |     |     |     |     |     |     | of  | all sentences. |     | We align | this | dimen- |     |
| --- | --- | --- | --- | --- | --- | --- | --- | -------------- | --- | -------- | ---- | ------ | --- |
tion.
|     |     |     |     |     |     |     | sion | with | the DUC | quality | question |     | of  |
| --- | --- | --- | --- | --- | --- | --- | ---- | ---- | ------- | ------- | -------- | --- | --- |
2. Weproposetouseautomaticchain-of-thought structure and coherence whereby "the
summaryshouldbewell-structuredand
| to improve |     | the performance |     | of   | LLM-based |     |                                     |       |                     |          |     |          |     |
| ---------- | --- | --------------- | --- | ---- | --------- | --- | ----------------------------------- | ----- | ------------------- | -------- | --- | -------- | --- |
|            |     |                 |     |      |           |     | well-organized.                     |       | Thesummaryshouldnot |          |     |          |     |
| evaluators |     | by providing    |     | more | context   | and |                                     |       |                     |          |     |          |     |
| guidance.  |     |                 |     |      |           |     | justbeaheapofrelatedinformation,but |       |                     |          |     |          |     |
|            |     |                 |     |      |           |     | should                              | build | from                | sentence | to  | sentence |     |
3. Weproposetore-weightthediscretescoresby toacoherentbodyofinformationabout
| theirrespectivetokenprobabilitiestoprovide |                  |     |            |        |           |           | atopic."               |                 |          |            |               |            |        |
| ------------------------------------------ | ---------------- | --- | ---------- | ------ | --------- | --------- | ---------------------- | --------------- | -------- | ---------- | ------------- | ---------- | ------ |
| a more                                     | fine-grained     |     | continuous |        | score     | for G-    |                        |                 |          |            |               |            |        |
| EVAL.                                      |                  |     |            |        |           |           | Auto Chain-of-Thoughts |                 |          | for        | NLG           | Evaluation |        |
|                                            |                  |     |            |        |           |           | The chain-of-thoughts  |                 |          | (CoT)      | is a sequence |            | of in- |
| 4. We                                      | conduct          | an  | analysis   | of the | potential | is-       |                        |                 |          |            |               |            |        |
|                                            |                  |     |            |        |           |           | termediate             | representations |          | that       | are           | generated  | by     |
| sue                                        | that LLM-based   |     | metrics    |        | have      | a prefer- |                        |                 |          |            |               |            |        |
|                                            |                  |     |            |        |           |           | the LLM                | during          | the text | generation |               | process.   | For    |
| ence                                       | of LLM-generated |     |            | texts  | over      | human-    |                        |                 |          |            |               |            |        |
evaluationtasks,somecriterianeedamoredetailed
| written | texts, | which | may | lead | to  | the self- |     |     |     |     |     |     |     |
| ------- | ------ | ----- | --- | ---- | --- | --------- | --- | --- | --- | --- | --- | --- | --- |
evaluationinstructionbeyondthesimpledefinition,
reinforcementofLLMsifLLM-basedmetrics
anditistime-consumingtomanuallydesignsuch
| are | used | as the reward |     | signal | for improving |     |                             |     |     |     |               |     |     |
| --- | ---- | ------------- | --- | ------ | ------------- | --- | --------------------------- | --- | --- | --- | ------------- | --- | --- |
|     |      |               |     |        |               |     | evaluationstepsforeachtask. |     |     |     | WefindthatLLM |     |     |
themselves.
|     |     |     |     |     |     |     | can generate | such | evaluation |     | steps | by itself. | The |
| --- | --- | --- | --- | --- | --- | --- | ------------ | ---- | ---------- | --- | ----- | ---------- | --- |
CoTcanprovidemorecontextandguidanceforthe
2 Method
|     |     |     |     |     |     |     | LLMtoevaluatethegeneratedtext, |     |     |     |     | andcanalso |     |
| --- | --- | --- | --- | --- | --- | --- | ------------------------------ | --- | --- | --- | --- | ---------- | --- |
G-EVAL is a prompt-based evaluator with three helptoexplaintheevaluationprocessandresults.
maincomponents: 1)apromptthatcontainsthedef- Forexample,forevaluatingcoherenceintextsum-
initionoftheevaluationtaskandthedesiredevalu- marization,weaddalineof“EvaluationSteps:"to
ationcriteria,2)achain-of-thoughts(CoT)thatis thepromptandletLLMtogeneratethefollowing
| asetofintermediateinstructionsgeneratedbythe |     |     |     |     |     |     | CoTautomatically: |     |     |     |     |     |     |
| -------------------------------------------- | --- | --- | --- | --- | --- | --- | ----------------- | --- | --- | --- | --- | --- | --- |
LLMdescribingthedetailedevaluationsteps,and
3)ascoringfunctionthatcallsLLMandcalculates 1. Read the news article carefully and
the score based on the probabilities of the return identifythemaintopicandkeypoints.
tokens.
2. Readthesummaryandcompareitto
|        |         |            |     |     |        |      | thenewsarticle. |     | Checkifthesummary |     |     |     |     |
| ------ | ------- | ---------- | --- | --- | ------ | ---- | --------------- | --- | ----------------- | --- | --- | --- | --- |
| Prompt | for NLG | Evaluation |     | The | prompt | is a |                 |     |                   |     |     |     |     |
coversthemaintopicandkeypointsof
naturallanguageinstructionthatdefinestheevalu-
ationtaskandthedesiredevaluationcriteria. For thenewsarticle,andifitpresentsthem
inaclearandlogicalorder.
| example, | for text | summarization, |     | the | prompt | can |     |        |         |               |     |     |     |
| -------- | -------- | -------------- | --- | --- | ------ | --- | --- | ------ | ------- | ------------- | --- | --- | --- |
| be:      |          |                |     |     |        |     | 3.  | Assign | a score | for coherence |     | on  | a   |
scaleof1to5,where1isthelowestand
| You | will be | given | one summary |     | written |     |     |     |     |     |     |     |     |
| --- | ------- | ----- | ----------- | --- | ------- | --- | --- | --- | --- | --- | --- | --- | --- |
5isthehighestbasedontheEvaluation
| for | a news | article. | Your | task | is to rate |     |     |     |     |     |     |     |     |
| --- | ------ | -------- | ---- | ---- | ---------- | --- | --- | --- | --- | --- | --- | --- | --- |
Criteria.
thesummaryononemetric.
| Please | make | sure | you | read and | under- |     |                 |     |                            |     |     |     |     |
| ------ | ---- | ---- | --- | -------- | ------ | --- | --------------- | --- | -------------------------- | --- | --- | --- | --- |
|        |      |      |     |          |        |     | ScoringFunction |     | Thescoringfunctioncallsthe |     |     |     |     |
standtheseinstructionscarefully. Please LLMwiththedesignedprompt,autoCoT,theinput
keepthisdocumentopenwhilereviewing, context and the target text that needs to be evalu-
andrefertoitasneeded. ated. UnlikeGPTScore(Fuetal.,2023)whichuses
2512

User Input
Input Context
Task Introduction Article: Paul Merson has restarted his row with
Andros Townsend after the Tottenham midfielder
You will be given one summary written for a news  was brought on with only seven minutes remaining
article. Your task is to rate the summary on one  in his team 's 0-0 draw with Burnley on ……
metric ……
Input Target
Evaluation Criteria Summary: Paul merson was brought on with only
seven minutes remaining in his team 's 0-0 draw
| Coherence (1-5) -  the collective quality of all  |     |     |     | with burnley …… |     |     |     |     |
| ------------------------------------------------- | --- | --- | --- | --------------- | --- | --- | --- | --- |
sentences. We align this dimension with the DUC
quality question of structure and coherence …… Evaluation Form (scores ONLY):
- Coherence:
Evaluation Steps
1. Read the news article carefully and identify the
Auto
| main topic and key points. |     |     |     |     | 0.6 |     |     |     |
| -------------------------- | --- | --- | --- | --- | --- | --- | --- | --- |
CoT
| 2. Read the summary and compare it to the news       |     |     |     |        | 0.4 |     |     |     |
| ---------------------------------------------------- | --- | --- | --- | ------ | --- | --- | --- | --- |
| article. Check if the summary covers the main topic  |     |     |     | G-EVAL |     |     |     |     |
| and key points of the news article, and if it        |     |     |     |        | 0.2 |     |     |     |
presents them in a clear and logical order.
0
3. Assign a score for coherence on a scale of 1 to
5, where 1 is the lowest and 5 is the highest based  1 2 3 4 5
on the Evaluation Criteria.
Weighted Summed Score: 2.59
Figure1: TheoverallframeworkofG-EVAL. WefirstinputTaskIntroductionandEvaluationCriteriatotheLLM,
andaskittogenerateaCoTofdetailedEvaluationSteps. ThenweusethepromptalongwiththegeneratedCoTto
evaluatetheNLGoutputsinaform-fillingparadigm. Finally,weusetheprobability-weightedsummationofthe
outputscoresasthefinalscore.
the conditional probability of generating the tar- probabilities of output tokens from LLMs to nor-
gettextasanevaluationmetric,G-EVALdirectly malizethescoresandtaketheirweightedsumma-
performs the evaluation task with a form-filling tion as the final results. Formally, given a set of
paradigm. This provides a more flexible way to scores(likefrom1to5)predefinedintheprompt
evaluatethetextasthemodelcanbehavedirectly S = s ,s ,...,s ,theprobabilityofeachscore
|     |     |     |     | { 1 | 2 n } |     |     |     |
| --- | --- | --- | --- | --- | ----- | --- | --- | --- |
basedontheevaluationcriteriaandsteps. Forex- p(s i )iscalculatedbytheLLM,andthefinalscore
| ample,forevaluatingcoherenceintextsummariza- |     |     |     | is: |     |     |     |     |
| -------------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- |
tion,weconcatenatetheprompt,theCoT,thenews
n
| article,  | and the summary, | and  | then call the LLM     |     |         |       |     |     |
| --------- | ---------------- | ---- | --------------------- | --- | ------- | ----- | --- | --- |
|           |                  |      |                       |     | score = | p(s ) | s   | (1) |
| to output | a score from     | 1 to | 5 for each evaluation |     |         | i ×   | i   |     |
|           |                  |      |                       |     |         | X i=1 |     |     |
aspect,basedonthedefinedcriteria.
Thismethodobtainsmorefine-grained,continu-
However,wenoticethisdirectscoringfunction
ousscoresthatbetterreflectthequalityanddiver-
hastwoissues:
sityofthegeneratedtexts.
| 1. For | some evaluation | tasks, | one digit usually |     |     |     |     |     |
| ------ | --------------- | ------ | ----------------- | --- | --- | --- | --- | --- |
3 Experiments
dominatesthedistributionofthescores,such
| as3fora1-5scale. |     | Thismayleadtothelow |     |                            |     |                 |     |     |
| ---------------- | --- | ------------------- | --- | -------------------------- | --- | --------------- | --- | --- |
|                  |     |                     |     | FollowingZhongetal.(2022), |     | wemeta-evaluate |     |     |
varianceofthescoresandthelowcorrelation
|     |     |     |     | our evaluator | on three | benchmarks, | SummEval, |     |
| --- | --- | --- | --- | ------------- | -------- | ----------- | --------- | --- |
withhumanjudgments.
Topical-ChatandQAGS,oftwoNLGtasks,sum-
marizationanddialogueresponsegeneration.
2. LLMsusuallyonlyoutputintegerscores,even
whenthepromptexplicitlyrequestsdecimal
3.1 ImplementationDetails
| values. | Thisleadstomanytiesinevaluation |     |     |     |     |     |     |     |
| ------- | ------------------------------- | --- | --- | --- | --- | --- | --- | --- |
scoreswhichdonotcapturethesubtlediffer- WeuseOpenAI’sGPTfamilyasourLLMs,includ-
|     |     |     |     | ing GPT-3.5 | (text-davinci-003) | and | GPT-4. | For |
| --- | --- | --- | --- | ----------- | ------------------ | --- | ------ | --- |
encebetweengeneratedtexts.
|     |     |     |     | GPT-3.5, | we set decoding | temperature | to  | 0 to in- |
| --- | --- | --- | --- | -------- | --------------- | ----------- | --- | -------- |
To address these issues, we propose using the creasethemodel’sdeterminism. ForGPT-4,asit
2513

|     | Coherence |     | Consistency |     | Fluency |     | Relevance |     |     | AVG |
| --- | --------- | --- | ----------- | --- | ------- | --- | --------- | --- | --- | --- |
Metrics
|     | ρ   | τ   |     | ρ τ | ρ   | τ   | ρ   | τ   | ρ   | τ   |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
ROUGE-1 0.167 0.126 0.160 0.130 0.115 0.094 0.326 0.252 0.192 0.150
ROUGE-2 0.184 0.139 0.187 0.155 0.159 0.128 0.290 0.219 0.205 0.161
ROUGE-L 0.128 0.099 0.115 0.092 0.105 0.084 0.311 0.237 0.165 0.128
BERTScore 0.284 0.211 0.110 0.090 0.193 0.158 0.312 0.243 0.225 0.175
MOVERSscore 0.159 0.118 0.157 0.127 0.129 0.105 0.318 0.244 0.191 0.148
BARTScore 0.448 0.342 0.382 0.315 0.356 0.292 0.356 0.273 0.385 0.305
UniEval 0.575 0.442 0.446 0.371 0.449 0.371 0.426 0.325 0.474 0.377
| GPTScore | 0.434 | –   | 0.449 | –   | 0.403 | –   | 0.381 | –   | 0.417 | –   |
| -------- | ----- | --- | ----- | --- | ----- | --- | ----- | --- | ----- | --- |
G-EVAL-3.5 0.440 0.335 0.386 0.318 0.424 0.347 0.385 0.293 0.401 0.320
-Probs 0.359 0.313 0.361 0.344 0.339 0.323 0.327 0.288 0.346 0.317
G-EVAL-4
|     | 0.582 | 0.457 | 0.507 | 0.425 | 0.506 | 0.455 | 0.547 | 0.433 | 0.514 | 0.418 |
| --- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- |
-Probs 0.560 0.472 0.501 0.459 0.505 0.473 0.511 0.444 0.502 0.446
-CoT 0.564 0.454 0.493 0.413 0.483 0.431 0.538 0.427 0.500 0.407
-Description 0.513 0.424 0.421 0.344 0.447 0.373 0.479 0.388 0.479 0.377
Table1: Summary-levelSpearman(ρ)andKendall-Tau(τ)correlationsofdifferentmetricsonSummEvalbench-
mark. G-EVALwithoutprobabilities(italicized)shouldnotbeconsideredasafaircomparisontoothermetricsonτ,
asitleadstomanytiesinthescores. ThisresultsinahigherKendall-Taucorrelation,butitdoesnotfairlyreflect
| thetrueevaluationability. | MoredetailsareinSection4. |     |     |     |     |     |     |     |     |     |
| ------------------------- | ------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
doesnotsupporttheoutputoftokenprobabilities, task. It aims to measure the consistency
weset‘n = 20,temperature = 1,top_p = 1’to dimensionofsummariesbyaskingandanswering
sample20timestoestimatethetokenprobabilities. questions. Itiscollectedfromtwodifferentnews
WeuseG-EVAL-4toindicateG-EVALwithGPT-4 summarization datasets CNN/DailyMail and
| as the backbone | model, | and G-EVAL-3.5 |     | to indi- | XSum. |     |     |     |     |     |
| --------------- | ------ | -------------- | --- | -------- | ----- | --- | --- | --- | --- | --- |
cateG-EVALwithGPT-3.5asthebackbonemodel.
3.3 Baselines
Examplepromptsforeachtaskareprovidedinthe
| Appendix. |     |     |     |     | We evaluate |     | G-EVAL against |     | various | evaluators |
| --------- | --- | --- | --- | --- | ----------- | --- | -------------- | --- | ------- | ---------- |
thatachievedstate-of-the-artperformance.
| 3.2 Benchmarks |     |     |     |     | BERTScore(Zhangetal.,2019)measuresthe |     |     |     |     |     |
| -------------- | --- | --- | --- | --- | ------------------------------------- | --- | --- | --- | --- | --- |
We adopt three meta-evaluation benchmarks to similaritybetweentwotextsbasedonthecontextu-
measure the correlation between G-EVAL and alizedembeddingfromBERT(Devlinetal.,2019).
| humanjudgments. |     |     |     |     | MoverScore |     | (Zhao       | et al.,    | 2019) | improves |
| --------------- | --- | --- | --- | --- | ---------- | --- | ----------- | ---------- | ----- | -------- |
|                 |     |     |     |     | BERTScore  | by  | adding soft | alignments |       | and new  |
SummEval (Fabbri et al., 2021) is a bench- aggregationmethodstoobtainamorerobustsimi-
| markthatcomparesdifferentevaluationmethods |     |     |     |     | laritymeasure. |     |     |     |     |     |
| ------------------------------------------ | --- | --- | --- | --- | -------------- | --- | --- | --- | --- | --- |
forsummarization. Itgiveshumanratingsforfour BARTScore(Yuanetal.,2021)isaunifiedeval-
aspects of each summary: fluency, coherence, uator which evaluate with the average likelihood
consistency and relevance. It is built on the of the pretrained encoder-decoder model, BART
CNN/DailyMaildataset(Hermannetal.,2015) (Lewisetal.,2020). Itcanpredictdifferentscores
dependingontheformatsofsourceandtarget.
Topical-Chat (Mehri and Eskenazi, 2020) FactCC and QAGS (Krys´cin´ski et al., 2020;
isatestbedformeta-evaluatingdifferentevaluators Wangetal.,2020)aretwoevaluatorsthatmeasure
ondialogueresponsegenerationsystemsthatuse the factual consistency of generated summaries.
knowledge. Wefollow(Zhongetal.,2022)touse FactCC is a BERT-based classifier that predicts
its human ratings on four aspects: naturalness, whether a summary is consistent with the source
coherence,engagingnessandgroundedness.
|     |     |     |     |     | document. | QAGS | is a question-answering |           |      | based    |
| --- | --- | --- | --- | --- | --------- | ---- | ----------------------- | --------- | ---- | -------- |
|     |     |     |     |     | evaluator | that | generates               | questions | from | the sum- |
QAGS (Wang et al., 2020) is a benchmark maryandchecksiftheanswerscanbefoundinthe
| forevaluatinghallucinationsinthesummarization |     |     |     |     | sourcedocument. |     |     |     |     |     |
| --------------------------------------------- | --- | --- | --- | --- | --------------- | --- | --- | --- | --- | --- |
2514

|     |     | Naturalness |     | Coherence |     | Engagingness | Groundedness |     | AVG |     |     |
| --- | --- | ----------- | --- | --------- | --- | ------------ | ------------ | --- | --- | --- | --- |
Metrics
|     |     | r   | ρ   |     | r ρ | r   | ρ r | ρ   | r   | ρ   |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
ROUGE-L 0.176 0.146 0.193 0.203 0.295 0.300 0.310 0.327 0.243 0.244
BLEU-4 0.180 0.175 0.131 0.235 0.232 0.316 0.213 0.310 0.189 0.259
METEOR 0.212 0.191 0.250 0.302 0.367 0.439 0.333 0.391 0.290 0.331
BERTScore 0.226 0.209 0.214 0.233 0.317 0.335 0.291 0.317 0.262 0.273
USR 0.337 0.325 0.416 0.377 0.456 0.465 0.222 0.447 0.358 0.403
UniEval 0.455 0.330 0.602 0.455 0.573 0.430 0.577 0.453 0.552 0.417
G-EVAL-3.5 0.532 0.539 0.519 0.544 0.660 0.691 0.586 0.567 0.574 0.585
G-EVAL-4 0.549 0.565 0.594 0.605 0.627 0.631 0.531 0.551 0.575 0.588
Table2: Turn-levelSpearman(ρ)andKendall-Tau(τ)correlationsofdifferentmetricsonTopical-Chatbenchmark.
USR (Mehri and Eskenazi, 2020) is evaluator InthelastpartofTable1whichcorrespondsto
that assesses dialogue response generation from GPT-basedevaluators,GPTScorealsousesGPTs
differentperspectives. Ithasseveralversionsthat for evaluating summarization texts, but relies on
assigndifferentscorestoeachtargetresponse. GPT’s conditional probabilities of the given tar-
UniEval(Zhongetal.,2022)isaunifiedevalua- get. G-EVAL substantiallysurpassesallprevious
state-of-the-artevaluatorsontheSummEvalbench-
torthatcanevaluatedifferentaspectsoftextgen-
erationasQAtasks. ItusesapretrainedT5model mark. G-EVAL-4 achieved much higher human
(Raffeletal.,2020)toencodetheevaluationtask, correspondence compared with G-EVAL-3.5 on
source and target texts as questions and answers, bothSpearmanandKendall-Taucorrelation,which
|     |     |     |     |     |     | indicates | that the larger | model | size | of GPT-4 | is  |
| --- | --- | --- | --- | --- | --- | --------- | --------------- | ----- | ---- | -------- | --- |
andthencomputestheQAscoreastheevaluation
score. Itcanalsohandledifferentevaluationtasks beneficialforsummarizationevaluation. G-EVAL
bychangingthequestionformat. alsooutperformsGPTScoreonseveraldimension,
demonstratingtheeffectivenessofthesimpleform-
GPTScore(Fuetal.,2023)isanewframework
fillingparadigm.
| that evaluates |             | texts | with generative |      | pre-training |     |     |     |     |     |     |
| -------------- | ----------- | ----- | --------------- | ---- | ------------ | --- | --- | --- | --- | --- | --- |
| models         | like GPT-3. |       | It assumes      | that | a generative |     |     |     |     |     |     |
3.5 ResultsforDialogueGeneration
pre-trainingmodelwillassignahigherprobability
ofhigh-qualitygeneratedtextfollowingagivenin- We use the Topical-chat benchmark from Mehri
| structionandcontext. |     |     | Unlike | G-EVAL,GPTScore |     |              |           |         |     |      |         |
| -------------------- | --- | --- | ------ | --------------- | --- | ------------ | --------- | ------- | --- | ---- | ------- |
|                      |     |     |        |                 |     | and Eskenazi | (2020) to | measure | how | well | differ- |
formulatestheevaluationtaskasaconditionalgen- ent evaluators agree with human ratings on the
erationprobleminsteadofaform-fillingproblem. quality of dialogue responses. We calculate the
WereportthescoreofGPTScorewithGPT3-text- PearsonandSpearmancorrelationforeachturnof
davinci-003astheLLM,whichisalsousuallyre- thedialogue. Table2showsthatsimilarity-based
| ferredasGPT-3.5. |     |     |     |     |     | metricshavegoodagreementwithhumansonhow |     |     |     |     |     |
| ---------------- | --- | --- | --- | --- | --- | --------------------------------------- | --- | --- | --- | --- | --- |
engagingandgroundedtheresponsesare,butnot
3.4 ResultsforSummarization
|     |     |     |     |     |     | ontheotheraspects. | Withrespecttothelearning- |     |     |     |     |
| --- | --- | --- | --- | --- | --- | ------------------ | ------------------------- | --- | --- | --- | --- |
basedevaluators,beforeG-EVAL,UniEvalpredicts
WeadoptthesameapproachasZhongetal.(2022)
|     |     |     |     |     |     | scores | that are most consistent |     | with | human | judg- |
| --- | --- | --- | --- | --- | --- | ------ | ------------------------ | --- | ---- | ----- | ----- |
toevaluatedifferentsummarizationmetricsusing
mentsacrossallaspects.
summary-levelSpearmanandKendall-Taucorre-
lation. The first part of Table 1 shows the results Asshowninthelastpart,G-EVALalsosubstan-
|            |      |         |            |          |            | tially surpasses | all previous     |            | state-of-the-art |          | eval- |
| ---------- | ---- | ------- | ---------- | -------- | ---------- | ---------------- | ---------------- | ---------- | ---------------- | -------- | ----- |
| of metrics | that | compare | the        | semantic | similarity |                  |                  |            |                  |          |       |
|            |      |         |            |          |            | uator on         | the Topical-Chat | benchmark. |                  | Notably, |       |
| between    | the  | model   | output and | the      | reference  | text.            |                  |            |                  |          |       |
Thesemetricsperformpoorlyonmostdimensions. the G-EVAL-3.5 can achieve similar results with
|            |      |       |             |     |         | G-EVAL-4.            | Thisindicatesthatthisbenchmarkis |     |     |     |     |
| ---------- | ---- | ----- | ----------- | --- | ------- | -------------------- | -------------------------------- | --- | --- | --- | --- |
| The second | part | shows | the results | of  | metrics | that                 |                                  |     |     |     |     |
|            |      |       |             |     |         | relativelyeasyforthe | G-EVALmodel.                     |     |     |     |     |
useneuralnetworkstolearnfromhumanratingsof
| summaryquality. |     | Thesemetricshavemuchhigher |     |     |     |     |     |     |     |     |     |
| --------------- | --- | -------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
3.6 ResultsonHallucinations
correlationsthanthesimilarity-basedmetrics,sug-
gestingthattheyaremorereliableforsummariza- AdvancedNLGmodelsoftenproducetextthatdoes
| tionevaluation. |     |     |     |     |     | notmatchthecontextinput(Caoetal.,2018),and |     |     |     |     |     |
| --------------- | --- | --- | --- | --- | --- | ------------------------------------------ | --- | --- | --- | --- | --- |
2515

QAGS-CNN QAGS-XSUM Average
Metrics
r ρ τ r ρ τ r ρ τ
ROUGE-2 0.459 0.418 0.333 0.097 0.083 0.068 0.278 0.250 0.200
ROUGE-L 0.357 0.324 0.254 0.024 -0.011 -0.009 0.190 0.156 0.122
BERTScore 0.576 0.505 0.399 0.024 0.008 0.006 0.300 0.256 0.202
MoverScore 0.414 0.347 0.271 0.054 0.044 0.036 0.234 0.195 0.153
FactCC 0.416 0.484 0.376 0.297 0.259 0.212 0.356 0.371 0.294
QAGS 0.545 - - 0.175 - - 0.375 - -
BARTScore 0.735 0.680 0.557 0.184 0.159 0.130 0.459 0.420 0.343
CTC 0.619 0.564 0.450 0.309 0.295 0.242 0.464 0.430 0.346
UniEval 0.682 0.662 0.532 0.461 0.488 0.399 0.571 0.575 0.465
G-EVAL-3.5 0.477 0.516 0.410 0.211 0.406 0.343 0.344 0.461 0.377
G-EVAL-4 0.631 0.685 0.591 0.558 0.537 0.472 0.599 0.611 0.525
Table3: Pearson(r),Spearman(ρ)andKendall-Tau(τ)correlationsofdifferentmetricsonQAGSbenchmark.
recentstudiesfindevenpowerfulLLMsalsosuffer 4
fromtheproblemofhallucination. Thismotivates 3.95
recentresearchtodesignevaluatorsformeasuring
3.9
theconsistencyaspectinsummarization(Krys´-
cin´ski et al., 2020; Wang et al., 2020; Cao et al., 3.85
2020; Durmus et al., 2020). We test the QAGS
3.8
meta-evaluation benchmark, which includes two
3.75
differentsummarizationdatasets: CNN/DailyMail Human GPT-3.5 Human GPT-3.5 Human GPT-3.5
Summary Summary Summary Summary Summary Summary
and XSum (Narayan et al., 2018) Table 3 shows
Human Summary is Better LLM Summary is Better Equally Good
that BARTScore performs well on the more ex-
tractivesubset(QAGS-CNN),buthaslowcorrela-
Figure 2: Averaged G-EVAL-4’s scores for human-
written summaries and GPT-3.5 summaries, divided
tiononthemoreabstractivesubset(QAGS-Xsum).
byhumanjudges’preference.
UniEval has good correlation on both subsets of
thedata.
Onaverage, G-EVAL-4outperformsallstate-of- generatedsummaries(usingGPT-3.5,text-davinci-
the-art evaluators on QAGS, with a large margin 003).
onQAGS-Xsum. G-EVAL-3.5,ontheotherhand, The dataset can be divided in three categories:
failed to perform well on this benchmark, which 1)human-writtensummariesthatareratedhigher
indicatesthattheconsistencyaspectissensitiveto than GPT-3.5 summaries by human judges, 2)
theLLM’scapacity. Thisresultisconsistentwith human-written summaries that are rated lower
Table1. thanGPT-3.5summariesbyhumanjudges,and3)
human-writtensummariesandGPT-3.5summaries
4 Analysis areratedequallygoodbyhumanjudges. WeuseG-
EVAL-4toevaluatethesummariesineachcategory,
WillG-EVALpreferLLM-basedoutputs? One
andcomparetheaveragedscores. 2
concernaboutusingLLMasanevaluatoristhatit
The results are shown in Figure 2. We can see
mayprefertheoutputsgeneratedbytheLLMitself,
that, G-EVAL-4 assigns higher scores to human-
rather than the high-quality human-written texts.
written summaries when human judges also pre-
To investigate this issue, we conduct an experi-
fer human-written summaries, and assigns lower
ment on the summarization task, where we com-
scores when human judges prefer GPT-3.5 sum-
pare the evaluation scores of the LLM-generated
maries. However,G-EVAL-4alwaysgiveshigher
and the human-written summaries. We use the
scorestoGPT-3.5summariesthanhuman-written
datasetcollectedinZhangetal.(2023),wherethey
firstaskfreelancewriterstowritehigh-qualitysum- 2We use G-EVAL-4 in this experiment, because its su-
periorityinevaluatingsummarizationtasks.Althoughithas
maries for news articles, and then ask annotators
differentdistributionwithwithGPT-3.5,thetwoLLMsshould
to compare human-written summaries and LLM- sharesimilarbehaviorsintermsoftextgeneration.
2516

summaries,evenwhenhumanjudgespreferhuman- scoringwithoutprobabilitiescanleadtomanyties,
writtensummaries. Weproposetwopotentialrea- whicharenotcountedaseitherconcordantordis-
sonsforthisphenomenon: cordant. ThismayresultinahigherKendall-Tau
correlation,butitdoesnotreflectthemodel’strue
| 1. NLG                        | outputs  | from       | high-quality  | systems              | are |                                        |             |            |               |         |           |        |
| ----------------------------- | -------- | ---------- | ------------- | -------------------- | --- | -------------------------------------- | ----------- | ---------- | ------------- | ------- | --------- | ------ |
|                               |          |            |               |                      |     | capacityofevaluatingthegeneratedtexts. |             |            |               |         |           | Onthe  |
| innaturaldifficulttoevaluate. |          |            |               | Theauthorsof         |     |                                        |             |            |               |         |           |        |
|                               |          |            |               |                      |     | other hand,                            | probability |            | normalization |         | can       | obtain |
| the                           | original | paper      | found         | that inter-annotator |     |                                        |             |            |               |         |           |        |
|                               |          |            |               |                      |     | more fine-grained,                     |             | continuous |               | scores  | that      | better |
| agreement                     |          | on judging | human-written |                      | and |                                        |             |            |               |         |           |        |
|                               |          |            |               |                      |     | capture                                | the subtle  | difference |               | between | generated |        |
LLM-generatedsummariesisverylow,with
texts. ThisisreflectedbythehigherSpearmancor-
Krippendorff’salphaat0.07.
|     |     |     |     |     |     | relationof | G-EVAL-4withprobabilities,whichis |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | ---------- | --------------------------------- | --- | --- | --- | --- | --- |
2. G-EVAL may have abias towardsthe LLM- basedontherankorderofthescores.
generatedsummariesbecausethemodelcould
We compare
|     |     |     |     |     |     | The Effect | of  | Different | LLMs |     |     |     |
| --- | --- | --- | --- | --- | --- | ---------- | --- | --------- | ---- | --- | --- | --- |
sharethesameconceptofevaluationcriteria
|     |     |     |     |     |     | theperformanceof |     | G-EVALwithdifferentLLMs |     |     |     |     |
| --- | --- | --- | --- | --- | --- | ---------------- | --- | ----------------------- | --- | --- | --- | --- |
duringgenerationandevaluation.
|     |     |     |     |     |     | on the SummEval |     | and | QAGS | benchmarks. |     | Ta- |
| --- | --- | --- | --- | --- | --- | --------------- | --- | --- | ---- | ----------- | --- | --- |
Ourworkshouldbeconsideredasapreliminary ble 1 and Table 3 show that G-EVAL-4 has
|          |      |            |      |          |           | higher correlation |     | than | G-EVAL-3.5 |     | on most | di- |
| -------- | ---- | ---------- | ---- | -------- | --------- | ------------------ | --- | ---- | ---------- | --- | ------- | --- |
| study on | this | issue, and | more | research | is needed |                    |     |      |            |     |         |     |
to fully understand the behavior of LLM-based mensionsanddatasets, exceptforengagingness
groundedness
evaluatorstoreduceitsinherentbiastowardsLLM- and on the Topical-Chat bench-
|           |                |              |            |              |         | mark. This | demonstrates    |     | that | a better | LLM        | can |
| --------- | -------------- | ------------ | ---------- | ------------ | ------- | ---------- | --------------- | --- | ---- | -------- | ---------- | --- |
| generated | text.          | We highlight |            | this concern | in the  |            |                 |     |      |          |            |     |
|           |                |              |            |              |         | improve    | the performance |     | of   | G-EVAL,  | especially |     |
| context   | that LLM-based |              | evaluators | may          | lead to |            |                 |     |      |          |            |     |
self-reinforcementofLLMsiftheevaluationscore formorechallengingandcomplexevaluationtasks,
suchasconsistencyandrelevance.
| isusedasarewardsignalforfurthertuning. |     |     |     |     | And |     |     |     |     |     |     |     |
| -------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
thiscouldresultintheover-fittingoftheLLMsto
| their own | evaluation |     | criteria, | rather than | the true | 5 RelatedWork |     |     |     |     |     |     |
| --------- | ---------- | --- | --------- | ----------- | -------- | ------------- | --- | --- | --- | --- | --- | --- |
evaluationcriteriaoftheNLGtasks.
|     |     |     |     |     |     | Ngram-basedMetrics |     |     | Ngram-basedmetricsre- |     |     |     |
| --- | --- | --- | --- | --- | --- | ------------------ | --- | --- | --------------------- | --- | --- | --- |
TheEffectofChain-of-Thoughts Wecompare fertothescoresforevaluatingtheNLGmodelsby
measuringthelexicaloverlapbetweenagenerated
| the performance |     | of  | G-EVAL | with and | without |          |             |       |      |           |     |         |
| --------------- | --- | --- | ------ | -------- | ------- | -------- | ----------- | ----- | ---- | --------- | --- | ------- |
|                 |     |     |        |          |         | text and | a reference | text. | BLEU | (Papineni |     | et al., |
chain-of-thoughts(CoT)ontheSummEvalbench-
mark. Table1showsthat G-EVAL-4withCoThas 2002)isthemostwidelyusedmetricformachine
higher correlation than G-EVAL-4 without CoT translationevaluation,whichcalculatesthegeomet-
ricmeanofmodifiedn-gramprecisionandabrevity
| on all dimensions, |     | especially |     | for fluency. | This |     |     |     |     |     |     |     |
| ------------------ | --- | ---------- | --- | ------------ | ---- | --- | --- | --- | --- | --- | --- | --- |
suggests that CoT can provide more context and penalty. ROUGE (Lin, 2004) is a recall-oriented
guidance for the LLM to evaluate the generated metricforsummarizationevaluation,whichmea-
suresthen-gramoverlapbetweenageneratedsum-
| text, and | can          | also help | to explain | the   | evaluation  |                                  |     |     |     |     |           |     |
| --------- | ------------ | --------- | ---------- | ----- | ----------- | -------------------------------- | --- | --- | --- | --- | --------- | --- |
|           |              |           |            |       |             | maryandasetofreferencesummaries. |     |     |     |     | Ithasbeen |     |
| process   | and results. | And       | it is      | shown | that CoT is |                                  |     |     |     |     |           |     |
moreusefulonconsistencyandfluencydimen- shown that more than 60% of recent papers on
sions. We also provide results of G-EVAL with NLG only rely on ROUGE or BLEU to evaluate
|     |     |     |     |     |     | theirsystems(Kasaietal.,2022). |     |     |     | However,these |     |     |
| --- | --- | --- | --- | --- | --- | ------------------------------ | --- | --- | --- | ------------- | --- | --- |
asimplepromptingbaselineonSummEval(only
asking GPT-4 to score a summary from 1-5 on metricsfailtomeasurecontentquality(Reiterand
eachdimension,withoutdetailedtaskintroduction, Belz,2009)orcapturesyntacticerrors(Stentetal.,
2005),andthereforedonotreflectthereliabilityof
evaluationcriteriaandCoT).
NLGsystemsaccurately.
| The Effect | of  | Probability | Normalization |     | We  |     |     |     |     |     |     |     |
| ---------- | --- | ----------- | ------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
compare the performance of G-EVAL with and Embedding-based Metrics Embedding-based
without probability normalization on the Sum- metricsrefertothescoresforevaluatingtheNLG
mEvalbenchmark. Table1showsthat,onKendall- models by measuring the semantic similarity be-
Tau correlation, G-EVAL-4 with probabilities is tweenageneratedtextandareferencetextbased
inferiortoG-EVAL-4withoutprobabilitiesonSum- onthewordorsentenceembeddings. WMD(Kus-
mEval. Webelievethisisrelatedtothecalculation neretal.,2015)isametricthatmeasuresthedis-
ofKendall-Taucorrelation,whichisbasedonthe tancebetweentwotextsbasedonthewordembed-
numberofconcordantanddiscordantpairs. Direct dings. BERTScore(Zhangetal.,2019)measures
2517

thesimilaritybetweentwotextsbasedonthecon- extensiveexperimentsontwoNLGtasks,textsum-
textualizedembeddingfromBERT(Devlinetal., marizationanddialoguegeneration,andshowthat
2019). MoverScore (Zhao et al., 2019) improves G-EVAL canoutperformstate-of-the-artevaluators
BERTScore by adding soft alignments and new and achieve higher human correspondence. We
aggregationmethodstoobtainamorerobustsimi- alsoproposepreliminaryanalysisonthebehavior
laritymeasure. (Clarketal.,2019)proposeametric ofLLM-basedevaluators,andhighlightthepoten-
that evaluates multi-sentence texts by computing tial issue of LLM-based evaluator having a bias
the similarity between the generated text and the towards the LLM-generated texts. We hope our
referencetextbasedonthesentenceembeddings. workcaninspiremoreresearchonusingLLMsfor
|                         |            |                      |     |          | NLG evaluation, |     | and also   | raise awareness |            | of the |
| ----------------------- | ---------- | -------------------- | --- | -------- | --------------- | --- | ---------- | --------------- | ---------- | ------ |
| Task-specificEvaluators |            | Task-specificmetrics |     |          |                 |     |            |                 |            |        |
|                         |            |                      |     |          | potential risks | and | challenges | of              | using LLMs | as     |
| refer to                | the scores | for evaluating       | the | NLG mod- |                 |     |            |                 |            |        |
evaluators.
elsbymeasuringthequalityofthegeneratedtexts
| based on | the specific  | task requirements. |         | For ex-    | Limitations |     |     |     |     |     |
| -------- | ------------- | ------------------ | ------- | ---------- | ----------- | --- | --- | --- | --- | --- |
| ample,   | summarization | tasks              | need to | assess the |             |     |     |     |     |     |
consistency of the generated summaries (Krys´- G-EVALisaframeworkthatusesLLMstoevaluate
|            |            |              |       |             | thequalityofgeneratedtexts. |     |     | However,italsohas |     |     |
| ---------- | ---------- | ------------ | ----- | ----------- | --------------------------- | --- | --- | ----------------- | --- | --- |
| cin´ski et | al., 2020; | Wang et al., | 2020; | Cao et al., |                             |     |     |                   |     |     |
somelimitationsthatneedtobeaddressedinfuture
2020;Durmusetal.,2020),anddialogueresponse
| generationtasksneedtoassessthecoherenceof |     |     |     |     | work. |     |     |     |     |     |
| ----------------------------------------- | --- | --- | --- | --- | ----- | --- | --- | --- | --- | --- |
thegeneratedresponses(Dzirietal.,2019;Yeetal.,
1. Aswealreadydiscussedinthepaper,G-EVAL
| 2021;Ghazarianetal.,2019). |     | However,thesemet- |     |     |     |     |     |     |     |     |
| -------------------------- | --- | ----------------- | --- | --- | --- | --- | --- | --- | --- | --- |
mayhaveabiastowardstheLLM-generated
ricsarenotgeneralizabletootherNLGtasks,and
|     |     |     |     |     | texts. | Thismayleadtotheself-reinforcement |     |     |     |     |
| --- | --- | --- | --- | --- | ------ | ---------------------------------- | --- | --- | --- | --- |
theyarenotabletomeasuretheoverallqualityof
|     |     |     |     |     | of LLMs | if  | the evaluation | score | is used | as  |
| --- | --- | --- | --- | --- | ------- | --- | -------------- | ----- | ------- | --- |
thegeneratedtexts.
|     |     |     |     |     | a reward | signal | for further | tuning. | And | this |
| --- | --- | --- | --- | --- | -------- | ------ | ----------- | ------- | --- | ---- |
Unified Evaluators Recently, some evaluators couldresultintheover-fittingoftheLLMsto
have been developed to assess text quality from their own evaluation criteria, rather than the
multipledimensionsbyvaryingtheinputandout-
trueevaluationcriteriaoftheNLGtasks.
putcontents(Yuanetal.,2021)orthemodelvari-
2. G-EVALislimitedbytheavailabilityandac-
| ants(MehriandEskenazi,2020)theyuse. |     |     |     | UniEval |             |     |       |            |      |      |
| ----------------------------------- | --- | --- | --- | ------- | ----------- | --- | ----- | ---------- | ---- | ---- |
|                                     |     |     |     |         | cessibility | of  | LLMs. | Currently, | most | LLMs |
(Zhongetal.,2022)isaunifiedevaluatorthatcan
evaluatedifferentaspectsoftextgenerationasQA arenotpubliclyavailable,andrequirespecial
|     |     |     |     |     | accessorpaymenttouse. |     |     | Thismaylimitthe |     |     |
| --- | --- | --- | --- | --- | --------------------- | --- | --- | --------------- | --- | --- |
tasks. Bychangingthequestionformat,itcanhan-
applicabilityandreproducibilityofG-EVAL.
dledifferentevaluationtasks.
Moreover,theLLMsareconstantlyupdated,
LLM-basedEvaluators Fuetal.(2023)propose whichmayleadtoinconsistentevaluationre-
GPTScore, anewframeworkthatevaluatedtexts sultsacrossdifferentversionsoftheLLMs.
| withgenerativepre-trainingmodelslikeGPT-3. |     |     |     | It  |     |     |     |     |     |     |
| ------------------------------------------ | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
assumesthatagenerativepre-trainingmodelwill 3. Wemeta-evaluateG-EVALontwoNLGtasks,
textsummarizationanddialoguegeneration.
| assign a | higher probability | of  | high-quality | gener- |     |     |     |     |     |     |
| -------- | ------------------ | --- | ------------ | ------ | --- | --- | --- | --- | --- | --- |
atedtextfollowingagiveninstructionandcontext. However,therearesomeemergingNLGtasks
Wangetal.(2023a)conductapreliminarysurvey intheLLMerawhereuserspromptwithfree-
ofusingChatGPTasaNLGevaluator. Kocmiand form natural language instructions. In this
|           |         |                  |          |     | case, | the evaluation | criteria |     | may need | to be |
| --------- | ------- | ---------------- | -------- | --- | ----- | -------------- | -------- | --- | -------- | ----- |
| Federmann | (2023); | Lu et al. (2023) | proposed | to  |       |                |          |     |          |       |
useGPTmodelsforevaluatingmachinetranslation moreflexibleandadaptivetotheuser’sinten-
tasks. Very recently, Wang et al. (2023b) investi- tionandpreference. Therefore,moreresearch
|     |     |     |     |     | isneededtoexplorehowtouse |     |     |     | G-EVAL | for |
| --- | --- | --- | --- | --- | ------------------------- | --- | --- | --- | ------ | --- |
gatedtheproblemofunfairnesswhenusinglarge
modelsinevaluatingdialogueresponses. evaluatingthesenewtypesofNLGtasks.
| 6 Conclusion |     |     |     |     | EthicsStatement |     |     |     |     |     |
| ------------ | --- | --- | --- | --- | --------------- | --- | --- | --- | --- | --- |
Inthispaper,weproposeG-EVAL,aframeworkof The G-EVAL frameworkweproposedisdesigned
usingLLMwithchain-of-thoughts(CoT)toeval- to offer a more effective and reliable method for
uate the quality of generated texts. We conduct assessingnaturallanguagegenerationsystems. Its
2518

purposeistoaidresearchers,developers,andother AlexanderRFabbri,WojciechKrys´cin´ski,BryanMc-
Cann,CaimingXiong,RichardSocher,andDragomir
interestedpartiesinevaluatingthequalityoftext
|          |        |          |                |       | Radev.2021. | Summeval: |     | Re-evaluatingsummariza- |     |     |
| -------- | ------ | -------- | -------------- | ----- | ----------- | --------- | --- | ----------------------- | --- | --- |
| produced | by NLG | systems. | Possible risks | could |             |           |     |                         |     |     |
TransactionsoftheAssociationfor
tionevaluation.
existifG-EVALisunabletopreciselyevaluatethe
ComputationalLinguistics,9:391–409.
qualityofproducedtextsorshowsapreferencefor
LLM-createdtexts. Thiscouldleadtodevelopers JinlanFu,See-KiongNg,ZhengbaoJiang,andPengfei
|                |     |             |          |         | Liu.2023. | Gptscore: | Evaluateasyoudesire. |     |     | arXiv |
| -------------- | --- | ----------- | -------- | ------- | --------- | --------- | -------------------- | --- | --- | ----- |
| overestimating | the | performance | of their | systems |           |           |                      |     |     |       |
preprintarXiv:2302.04166.
orunintentionallyreinforcingbiasesintheirmod-
els. Furthermore,usersdependingonthegenerated
|     |     |     |     |     | Sarik Ghazarian, |     | Johnny | Wei, Aram | Galstyan, | and |
| --- | --- | --- | --- | --- | ---------------- | --- | ------ | --------- | --------- | --- |
material may receive low-quality or biased infor- Nanyun Peng. 2019. Better automatic evaluation
|     |     |     |     |     | of open-domain |     | dialogue | systems | with | contextual- |
| --- | --- | --- | --- | --- | -------------- | --- | -------- | ------- | ---- | ----------- |
mation.
|     |     |     |     |     | izedembeddings. |     | InProceedingsoftheWorkshop |     |     |     |
| --- | --- | --- | --- | --- | --------------- | --- | -------------------------- | --- | --- | --- |
onMethodsforOptimizingandEvaluatingNeural
|     |     |     |     |     | Language | Generation, |     | pages | 82–89, Minneapolis, |     |
| --- | --- | --- | --- | --- | -------- | ----------- | --- | ----- | ------------------- | --- |
References
Minnesota.AssociationforComputationalLinguis-
tics.
| SatanjeevBanerjeeandAlonLavie.2005. |     |     | Meteor: | An  |     |     |     |     |     |     |
| ----------------------------------- | --- | --- | ------- | --- | --- | --- | --- | --- | --- | --- |
automaticmetricformtevaluationwithimprovedcor-
KarlMoritzHermann,TomasKocisky,EdwardGrefen-
| relationwithhumanjudgments. |     |     | InProceedingsof |     |     |     |     |     |     |     |
| --------------------------- | --- | --- | --------------- | --- | --- | --- | --- | --- | --- | --- |
stette,LasseEspeholt,WillKay,MustafaSuleyman,
theaclworkshoponintrinsicandextrinsicevaluation
|     |     |     |     |     | andPhilBlunsom.2015. |     |     | Teachingmachinestoread |     |     |
| --- | --- | --- | --- | --- | -------------------- | --- | --- | ---------------------- | --- | --- |
measuresformachinetranslationand/orsummariza-
|     |     |     |     |     | and comprehend. |     | Advances | in  | neural | information |
| --- | --- | --- | --- | --- | --------------- | --- | -------- | --- | ------ | ----------- |
tion,pages65–72.
processingsystems,28.
MengCao,YueDong,JiapengWu,andJackieChiKit
Cheung.2020. Factualerrorcorrectionforabstrac- Jungo Kasai, Keisuke Sakaguchi, Ronan Le Bras,
LaviniaDunagan,JacobMorrison,AlexanderFabbri,
| tive summarization |     | models. | In Proceedings | of the |                                |     |     |     |               |     |
| ------------------ | --- | ------- | -------------- | ------ | ------------------------------ | --- | --- | --- | ------------- | --- |
|                    |     |         |                |        | YejinChoi,andNoahA.Smith.2022. |     |     |     | Bidimensional |     |
2020ConferenceonEmpiricalMethodsinNatural
|     |     |     |     |     | leaderboards: |     | Generateandevaluatelanguagehand |     |     |     |
| --- | --- | --- | --- | --- | ------------- | --- | ------------------------------- | --- | --- | --- |
LanguageProcessing(EMNLP),pages6251–6258.
|     |     |     |     |     | inhand. | InProceedingsofthe2022Conferenceof |     |     |     |     |
| --- | --- | --- | --- | --- | ------- | ---------------------------------- | --- | --- | --- | --- |
ZiqiangCao,FuruWei,WenjieLi,andSujianLi.2018. theNorthAmericanChapteroftheAssociationfor
Faithfultotheoriginal: Factawareneuralabstractive ComputationalLinguistics: HumanLanguageTech-
|                |     |                                 |     |     | nologies, | pages | 3540–3557, | Seattle, | United | States. |
| -------------- | --- | ------------------------------- | --- | --- | --------- | ----- | ---------- | -------- | ------ | ------- |
| summarization. |     | Inthirty-secondAAAIconferenceon |     |     |           |       |            |          |        |         |
AssociationforComputationalLinguistics.
artificialintelligence.
ElizabethClark,AsliCelikyilmaz,andNoahASmith. Tom Kocmi and Christian Federmann. 2023. Large
2019. Sentencemover’ssimilarity: Automaticevalu- language models are state-of-the-art evaluators of
ationformulti-sentencetexts. InProceedingsofthe translationquality. arXivpreprintarXiv:2302.14520.
57thAnnualMeetingoftheAssociationforCompu-
WojciechKrys´cin´ski,BryanMcCann,CaimingXiong,
tationalLinguistics,pages2748–2760.
|     |     |     |     |     | and Richard | Socher. | 2020. | Evaluating |     | the factual |
| --- | --- | --- | --- | --- | ----------- | ------- | ----- | ---------- | --- | ----------- |
Jacob Devlin, Ming-Wei Chang, Kenton Lee, and consistency of abstractive text summarization. In
KristinaToutanova.2019. Bert: Pre-trainingofdeep Proceedings of the 2020 Conference on Empirical
bidirectionaltransformersforlanguageunderstand- MethodsinNaturalLanguageProcessing(EMNLP),
pages9332–9346.
ing. InProceedingsofthe2019Conferenceofthe
NorthAmericanChapteroftheAssociationforCom-
putationalLinguistics: HumanLanguageTechnolo- MattKusner,YuSun,NicholasKolkin,andKilianWein-
gies,Volume1(LongandShortPapers),pages4171– berger.2015. Fromwordembeddingstodocument
| 4186. |     |     |     |     | distances. | InInternationalconferenceonmachine |     |     |     |     |
| ----- | --- | --- | --- | --- | ---------- | ---------------------------------- | --- | --- | --- | --- |
learning,pages957–966.PMLR.
| EsinDurmus,HeHe,andMonaDiab.2020. |     |     |     | Feqa: A |             |        |      |       |        |        |
| --------------------------------- | --- | --- | --- | ------- | ----------- | ------ | ---- | ----- | ------ | ------ |
|                                   |     |     |     |         | Mike Lewis, | Yinhan | Liu, | Naman | Goyal, | Marjan |
questionansweringevaluationframeworkforfaith-
fulnessassessmentinabstractivesummarization. In Ghazvininejad,AbdelrahmanMohamed,OmerLevy,
Proceedingsofthe58thAnnualMeetingoftheAsso- Veselin Stoyanov, and Luke Zettlemoyer. 2020.
ciationforComputationalLinguistics,pages5055– BART:denoisingsequence-to-sequencepre-training
| 5070. |     |     |     |     | fornaturallanguagegeneration,translation,andcom- |                                   |     |     |     |     |
| ----- | --- | --- | --- | --- | ------------------------------------------------ | --------------------------------- | --- | --- | --- | --- |
|       |     |     |     |     | prehension.                                      | InProceedingsofthe58thAnnualMeet- |     |     |     |     |
NouhaDziri,EhsanKamalloo,KoryMathewson,and ingoftheAssociationforComputationalLinguistics,
OsmarRZaiane.2019. Evaluatingcoherenceindi- ACL2020,Online,July5-10,2020,pages7871–7880.
aloguesystemsusingentailment. InProceedingsof AssociationforComputationalLinguistics.
the2019ConferenceoftheNorthAmericanChap-
teroftheAssociationforComputationalLinguistics: Chin-YewLin.2004. Rouge: Apackageforautomatic
HumanLanguageTechnologies,Volume1(Longand evaluation of summaries. In Text summarization
| ShortPapers),pages3806–3812. |     |     |     |     | branchesout,pages74–81. |     |     |     |     |     |
| ---------------------------- | --- | --- | --- | --- | ----------------------- | --- | --- | --- | --- | --- |
2519

QingyuLu, BaopuQiu, LiangDing, LipingXie, and PeiyiWang,LeiLi,LiangChen,DaweiZhu,Binghuai
Dacheng Tao. 2023. Error analysis prompting en- Lin,YunboCao,QiLiu,TianyuLiu,andZhifangSui.
ableshuman-liketranslationevaluationinlargelan- 2023b. Largelanguagemodelsarenotfairevaluators.
|       |         |        |       |             | arXiv | arXivpreprintarXiv:2305.17926. |     |     |     |     |     |     |
| ----- | ------- | ------ | ----- | ----------- | ----- | ------------------------------ | --- | --- | --- | --- | --- | --- |
| guage | models: | A case | study | on chatgpt. |       |                                |     |     |     |     |     |     |
preprintarXiv:2303.13809.
JasonWei,XuezhiWang,DaleSchuurmans,Maarten
| Shikib Mehri | and | Maxine | Eskenazi. | 2020. | USR: An |        |         |      |         |       |       |       |
| ------------ | --- | ------ | --------- | ----- | ------- | ------ | ------- | ---- | ------- | ----- | ----- | ----- |
|              |     |        |           |       |         | Bosma, | Ed Chi, | Quoc | Le, and | Denny | Zhou. | 2022. |
unsupervised and reference free evaluation metric Chainofthoughtpromptingelicitsreasoninginlarge
for dialog generation. In Proceedings of the 58th language models. Advances in neural information
AnnualMeetingoftheAssociationforComputational processingsystems,28.
Linguistics,pages681–707,Online.Associationfor
ComputationalLinguistics.
|                 |     |        |        |             |         | ZhengYe,             | LiucunLu, | LishanHuang,              |                             |     | LiangLin, | and |
| --------------- | --- | ------ | ------ | ----------- | ------- | -------------------- | --------- | ------------------------- | --------------------------- | --- | --------- | --- |
|                 |     |        |        |             |         | XiaodanLiang.2021.   |           |                           | Towardsquantifiabledialogue |     |           |     |
| Shashi Narayan, |     | Shay B | Cohen, | and Mirella | Lapata. |                      |           |                           |                             |     |           |     |
|                 |     |        |        |             |         | coherenceevaluation. |           | InProceedingsofthe59thAn- |                             |     |           |     |
2018. Don’tgivemethedetails,justthesummary!
nualMeetingoftheAssociationforComputational
| topic-aware | convolutional |     | neural | networks | for ex- |     |     |     |     |     |     |     |
| ----------- | ------------- | --- | ------ | -------- | ------- | --- | --- | --- | --- | --- | --- | --- |
Linguisticsandthe11thInternationalJointConfer-
| treme summarization. |     |           | In Proceedings |            | of the 2018 |         |         |          |            |     |         |     |
| -------------------- | --- | --------- | -------------- | ---------- | ----------- | ------- | ------- | -------- | ---------- | --- | ------- | --- |
|                      |     |           |                |            |             | ence on | Natural | Language | Processing |     | (Volume | 1:  |
| Conference           | on  | Empirical | Methods        | in Natural | Lan-        |         |         |          |            |     |         |     |
LongPapers),pages2718–2729.
guageProcessing,pages1797–1807.
WeizheYuan,GrahamNeubig,andPengfeiLiu.2021.
LongOuyang,JeffreyWu,XuJiang,DiogoAlmeida,
|     |     |     |     |     |     | Bartscore: | Evaluating |     | generated | text | as text | gener- |
| --- | --- | --- | --- | --- | --- | ---------- | ---------- | --- | --------- | ---- | ------- | ------ |
CarrollWainwright,PamelaMishkin,ChongZhang,
ation. AdvancesinNeuralInformationProcessing
SandhiniAgarwal,KatarinaSlama,AlexRay,etal.
| 2022.      | Training | languagemodelsto |     | followinstruc- |           | Systems,34.   |        |          |     |       |            |     |
| ---------- | -------- | ---------------- | --- | -------------- | --------- | ------------- | ------ | -------- | --- | ----- | ---------- | --- |
| tions with | human    | feedback.        |     | Advances       | in Neural |               |        |          |     |       |            |     |
|            |          |                  |     |                |           | Tianyi Zhang, | Varsha | Kishore, |     | Felix | Wu, Kilian | Q   |
InformationProcessingSystems,35:27730–27744.
|     |     |     |     |     |     | Weinberger,andYoavArtzi.2019. |     |     |     | Bertscore: |     | Eval- |
| --- | --- | --- | --- | --- | --- | ----------------------------- | --- | --- | --- | ---------- | --- | ----- |
KishorePapineni,SalimRoukos,ToddWard,andWei- uating text generation with bert. arXiv preprint
arXiv:1904.09675.
| JingZhu.2002.              |     | Bleu: | amethodforautomaticevalu- |     |     |     |     |     |     |     |     |     |
| -------------------------- | --- | ----- | ------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ationofmachinetranslation. |     |       | InProceedingsofthe        |     |     |     |     |     |     |     |     |     |
40thannualmeetingoftheAssociationforComputa- TianyiZhang,FaisalLadhak,EsinDurmus,PercyLiang,
tionalLinguistics,pages311–318. Kathleen McKeown, and Tatsunori B. Hashimoto.
2023. Benchmarkinglargelanguagemodelsfornews
| ColinRaffel,NoamShazeer,AdamRoberts,Katherine |     |     |     |     |     | summarization. |     |     |     |     |     |     |
| --------------------------------------------- | --- | --- | --- | --- | --- | -------------- | --- | --- | --- | --- | --- | --- |
Lee,SharanNarang,MichaelMatena,YanqiZhou,
WeiLi,andPeterJLiu.2020. Exploringthelimits WeiZhao,MaximePeyrard,FeiLiu,YangGao,Chris-
oftransferlearningwithaunifiedtext-to-texttrans- tianMMeyer,andSteffenEger.2019. Moverscore:
former. JournalofMachineLearningResearch,21:1– Textgenerationevaluatingwithcontextualizedem-
| 67. |     |     |     |     |     | beddingsandearthmoverdistance. |     |     |     |     | InProceedings |     |
| --- | --- | --- | --- | --- | --- | ------------------------------ | --- | --- | --- | --- | ------------- | --- |
ofthe2019ConferenceonEmpiricalMethodsinNat-
EhudReiterandAnjaBelz.2009. Aninvestigationinto uralLanguageProcessingandthe9thInternational
thevalidityofsomemetricsforautomaticallyevalu- JointConferenceonNaturalLanguageProcessing
| atingnaturallanguagegenerationsystems. |     |     |     |     | Computa- |     |     |     |     |     |     |     |
| -------------------------------------- | --- | --- | --- | --- | -------- | --- | --- | --- | --- | --- | --- | --- |
(EMNLP-IJCNLP),pages563–578.
tionalLinguistics,35(4):529–558.
LianminZheng,Wei-LinChiang,YingSheng,Siyuan
| Amanda | Stent, Matthew |     | Marge, | and Mohit | Singhai. |         |          |     |         |         |     |         |
| ------ | -------------- | --- | ------ | --------- | -------- | ------- | -------- | --- | ------- | ------- | --- | ------- |
|        |                |     |        |           |          | Zhuang, | Zhanghao | Wu, | Yonghao | Zhuang, |     | Zi Lin, |
2005. Evaluatingevaluationmethodsforgeneration
ZhuohanLi,DachengLi,Eric.PXing,HaoZhang,
| inthepresenceofvariation. |     |     | InProceedingsofthe6th |     |     |                                     |     |     |     |     |     |         |
| ------------------------- | --- | --- | --------------------- | --- | --- | ----------------------------------- | --- | --- | --- | --- | --- | ------- |
|                           |     |     |                       |     |     | JosephE.Gonzalez,andIonStoica.2023. |     |     |     |     |     | Judging |
internationalconferenceonComputationalLinguis-
llm-as-a-judgewithmt-benchandchatbotarena.
ticsandIntelligentTextProcessing,pages341–351.
Rohan Taori, Ishaan Gulrajani, Tianyi Zhang, Yann Ming Zhong, Yang Liu, Da Yin, Yuning Mao, Yizhu
Dubois,XuechenLi,CarlosGuestrin,PercyLiang, Jiao, Pengfei Liu, Chenguang Zhu, Heng Ji, and
|                               |     |     |       |                 |          | Jiawei Han. | 2022.     |     | Towards  | a           | unified | multi-  |
| ----------------------------- | --- | --- | ----- | --------------- | -------- | ----------- | --------- | --- | -------- | ----------- | ------- | ------- |
| andTatsunoriB.Hashimoto.2023. |     |     |       | Stanfordalpaca: |          |             |           |     |          |             |         |         |
|                               |     |     |       |                 |          | dimensional | evaluator |     | for text | generation. |         | In Pro- |
| An instruction-following      |     |     | llama | model.          | https:// |             |           |     |          |             |         |         |
github.com/tatsu-lab/stanford_alpaca. ceedingsofthe2022ConferenceonEmpiricalMeth-
|     |     |     |     |     |     | ods in Natural |     | Language | Processing, |     | pages | 2023– |
| --- | --- | --- | --- | --- | --- | -------------- | --- | -------- | ----------- | --- | ----- | ----- |
AlexWang, KyunghyunCho, andMikeLewis.2020. 2038,AbuDhabi,UnitedArabEmirates.
Askingandansweringquestionstoevaluatethefac-
| tualconsistencyofsummaries. |     |     | InProceedingsofthe |     |     |     |     |     |     |     |     |     |
| --------------------------- | --- | --- | ------------------ | --- | --- | --- | --- | --- | --- | --- | --- | --- |
58thAnnualMeetingoftheAssociationforCompu-
A ExamplePrompts
tationalLinguistics,pages5008–5020.
EvaluateCoherenceintheSummarizationTask
JiaanWang,YunlongLiang,FandongMeng,Haoxiang
Shi,ZhixuLi,JinanXu,JianfengQu,andJieZhou.
|        |                                         |     |     |     |     | You will         | be  | given | one summary |     | written |     |
| ------ | --------------------------------------- | --- | --- | --- | --- | ---------------- | --- | ----- | ----------- | --- | ------- | --- |
| 2023a. | Ischatgptagoodnlgevaluator?apreliminary |     |     |     |     |                  |     |       |             |     |         |     |
| study. | arXivpreprintarXiv:2303.04048.          |     |     |     |     | foranewsarticle. |     |       |             |     |         |     |
2520

Yourtaskistoratethesummaryonone Yourtaskistoratetheresponsesonone
| metric. |     |     |     | metric. |     |     |     |
| ------- | --- | --- | --- | ------- | --- | --- | --- |
Please make sure you read and under- Please make sure you read and under-
standtheseinstructionscarefully. Please standtheseinstructionscarefully. Please
keepthisdocumentopenwhilereviewing, keepthisdocumentopenwhilereviewing,
| andrefertoitasneeded. |     |     |     | andrefertoitasneeded. |     |     |     |
| --------------------- | --- | --- | --- | --------------------- | --- | --- | --- |
| EvaluationCriteria:   |     |     |     | EvaluationCrieteria:  |     |     |     |
Coherence(1-5)-thecollectivequality Engagingness (1-3) Is the response
| ofallsentences. | Wealignthisdimension |                  |      | dull/interesting? |             |       |              |
| --------------- | -------------------- | ---------------- | ---- | ----------------- | ----------- | ----- | ------------ |
| with the        | DUC                  | quality question | of   |                   |             |       |              |
|                 |                      |                  |      | - A score         | of 1 (dull) | means | that the re- |
| structure       | and coherence        | whereby          | "the |                   |             |       |              |
sponseisgenericanddull.
summaryshouldbewell-structuredand
|                 |                     |     |     | - A score | of 2 (somewhat |             | interesting) |
| --------------- | ------------------- | --- | --- | --------- | -------------- | ----------- | ------------ |
| well-organized. | Thesummaryshouldnot |     |     |           |                |             |              |
|                 |                     |     |     | means the | response       | is somewhat | inter-       |
justbeaheapofrelatedinformation,but
estingandcouldengageyouinthecon-
| should build | from | sentence to sentence |     |     |     |     |     |
| ------------ | ---- | -------------------- | --- | --- | --- | --- | --- |
versation(e.g.,anopinion,thought)
toacoherentbodyofinformationabout
| atopic."         |          |                   |     | - A score         | of 3 (interesting) |             | means the   |
| ---------------- | -------- | ----------------- | --- | ----------------- | ------------------ | ----------- | ----------- |
|                  |          |                   |     | response          | is very            | interesting | or presents |
| EvaluationSteps: |          |                   |     | aninterestingfact |                    |             |             |
| 1. Read          | the news | article carefully | and |                   |                    |             |             |
EvaluationSteps:
identifythemaintopicandkeypoints.
1. Readtheconversation,thecorrespond-
2. Readthesummaryandcompareitto
ingfactandtheresponsecarefully.
| thenewsarticle. |     | Checkifthesummary |     |     |     |     |     |
| --------------- | --- | ----------------- | --- | --- | --- | --- | --- |
coversthemaintopicandkeypointsof 2. Ratetheresponseonascaleof1-3for
thenewsarticle,andifitpresentsthem engagingness,accordingtothecriteria
| inaclearandlogicalorder. |     |     |     | above. |     |     |     |
| ------------------------ | --- | --- | --- | ------ | --- | --- | --- |
3. Assign a score for coherence on a 3. Provide a brief explanation for your
scaleof1to5,where1isthelowestand rating, referring to specific aspects of
5isthehighestbasedontheEvaluation theresponseandtheconversation.
Criteria.
Example:
Example:
ConversationHistory:
SourceText:
{{Document}}
{{Document}}
CorrespondingFact:
Summary:
{{Fact}}
{{Summary}}
Response:
{{Response}}
EvaluationForm(scoresONLY):
-Coherence:
EvaluationForm(scoresONLY):
| EvaluateEngagingnessintheDialogueGenera- |     |     |     | -Engagingness: |     |     |     |
| ---------------------------------------- | --- | --- | --- | -------------- | --- | --- | --- |
tionTask
EvaluateHallucinations
Youwillbegivenaconversationbetween
two individuals. You will then be given Human Evaluation of Text Summariza-
| onepotentialresponseforthenextturn |     |              |      | tionSystems: |     |     |     |
| ---------------------------------- | --- | ------------ | ---- | ------------ | --- | --- | --- |
| in the conversation.               |     | The response | con- |              |     |     |     |
cerns an interesting fact, which will be Factual Consistency: Does the
| providedaswell. |     |     |     | summaryuntruthfulormisleadingfacts |     |     |     |
| --------------- | --- | --- | --- | ---------------------------------- | --- | --- | --- |
2521

thatarenotsupportedbythesourcetext?
SourceText:
{{Document}}
Summary:
{{Summary}}
Does the summary contain factual
inconsistency?
Answer:
2522