This article has been accepted for publication in IEEE Intelligent Systems. This is the author's version which has not been fully edited and
content may change prior to final publication. Citation information: DOI 10.1109/MIS.2026.3660833
Special Issue on Metacognitive Prediction of AI Behavior
Multiple Choice Questions: Reasoning Makes
Large Language Models (LLMs) More
Self-Confident, Especially When They are
Wrong
TairanFu, PolitecnicodiMilano,Milan,Italy
JavierConde, InformationProcessingandTelecommunicationsCenter(IPTC),UniversidadPolitécnicadeMadrid,
Madrid,28040,Spain
GonzaloMartínez, InformationProcessingandTelecommunicationsCenter(IPTC),UniversidadPolitécnicade
Madrid,Madrid,28040,Spain
MaríaGrandury, InformationProcessingandTelecommunicationsCenter(IPTC),UniversidadPolitécnicade
Madrid,Madrid,28040,Spain
PedroReviriego, InformationProcessingandTelecommunicationsCenter(IPTC),UniversidadPolitécnicade
Madrid,Madrid,28040,Spain
Abstract—MultipleChoiceQuestion(MCQ)testsareamongthemostusedmethods
for evaluating large language models (LLMs). Besides checking the correctness
of the selected answer, evaluations often consider the model’s confidence through
the probability assigned to its response. In this work, we investigate how LLM
confidence is influenced by the answering approach when the model answers
directly or reasons before responding. Experiments on a general knowledge
benchmark, covering 57 subjects and seven LLMs, show that models are
systematicallymoreconfidentwhenprovidingreasoningbeforeanswering,andthat
this confidence increase is larger when the selected answer is incorrect than when
it is correct. We hypothesize that the reasoning process alters token probabilities,
as the final answer prediction depends jointly on the question and the model’s
self-generated reasoning, leading to inflated confidence estimates. Using standard
calibration metrics such as Expected Calibration Error and Brier score, we further
show that Chain-of-Thought (CoT) prompting degrades calibration by increasing
the proportion of high-confidence wrong answers. These findings indicate that, in
MCQ evaluation settings with CoT prompting, LLM-estimated probabilities should
be used with caution as a basis for evaluation and metacognitive mechanisms.
T
he evaluation of Large Language Models andevidenceareexpressedinnaturallanguage,com-
(LLMs) is challenging, as in most cases their plicating systematic, scalable assessment. A potential
answersareinnaturallanguageandtheyhave approach is human evaluation, so people evaluate
tobeevaluatedonalargenumberoftopicsandtasks LLM responses. However, this does not scale to tens
[1]. Even when evaluation uses structured or con- of thousands of questions for each model, with new
strained outputs (for example, JSON, or a structured modelsappearingeveryday.Toaddressthisissue,ini-
answer tag as in this work), the question, reasoning tiativessuchasChatbotArena[2]resorttothecommu-
nitytoassesshumanpreferences.However,questions,
answers,andparticipantsarenotcontrolled,sothere-
XXXX-XXX©2025IEEE sultsprovideacomparativerankingofmodels,butnot
DigitalObjectIdentifier10.1109/XXX.0000.0000000
PublishedbytheIEEEComputerSociety IEEEIntelligentSystems 1
This work is licensed under a Creative Commons Attribution 4.0 License. For more information, see https://creativecommons.org/licenses/by/4.0/

This article has been accepted for publication in IEEE Intelligent Systems. This is the author's version which has not been fully edited and
content may change prior to final publication. Citation information: DOI 10.1109/MIS.2026.3660833
Special Issue on Metacognitive Prediction of AI Behavior
adetailedanalysisoftheirspecificcapabilities.Amore when they first provide the reasoning and then the
scalablealternativewouldbetouseanLLMtoevaluate selected answer. The main findings of our evaluation
other LLMs [3]. This method has limitations, as the show that
LLM that is judging may have biases towards its own
1) Models tend to be more confident when they
contentortowardlongresponses,andsomeonehasto
reason before answering.
evaluatethisLLM.Today,themostwidelyusedmethod
2) This increase in self-confidence occurs both
to evaluate LLMs is to run different benchmarks that
when the model response is correct and when
aremostlymadeupofmultiple-choicequestions.This
it is incorrect, and is systematically larger when
enables automation of the process and evaluation of
the response is incorrect.
specifictasks,forexample,mathematics,reasoning,or
3) Chain-of-Thought prompting worsens standard
knowledge of many different topics [4].
calibration metrics for most models by increas-
The results of a Multiple Choice Question (MCQ)
ing the proportion of high-confidence wrong an-
testaretypicallymeasuredintermsofthepercentage
swers.
of correct answers using a given number of examples
4) The increase occurs for practically all cate-
in the prompt to help the model [1]. This accuracy
gories/topics of the questions, but it is larger for
metricdoesnotprovideanyinsightintotheconfidence
topics that require reasoning.
of the LLM in its responses, which is an important
5) All tested models experience similar trends
feature of the LLM [5]. However, as in order to select
across all dimensions.
each new token, an LLM computes estimates of the
probability that each token in its dictionary is the next Inthepaper,theseeffectsarediscussedandlinked
token, these probabilities can be used to develop to the operation of LLMs and also to human cognition
confidence estimates [6]. For example, if there are to try to understand their causes and implications for
four possible options to answer a question, A,B,C,D, the study of metacognition in LLMs.
and the LLM estimated probabilities for each of them
are 0.5,0.3,0.2,0.1, the model does not have much
confidence in its response. However, these are just CONFIDENCE AND REASONING
the estimated probabilities of the LLM and may not
correlatewiththecorrectnessofeachoption,asLLMs Confidence estimation
have limited metacognition capabilities [7]. With the widespread adoption of LLMs across various
The LLM responses depend not only on the ques- tasks, reliably assessing the confidence of their out-
tion but also on the text produced by the LLM before puts has become a critical challenge. This issue is
selectinganoption.Infact,itiswellknownthatinmany closely tied to the practical usability of such models.
casesLLMshavebetterresultswhentheyareaskedto Several methods have been proposed for confidence
think and decompose the problem into several steps, estimation, including: (1) approaches based on token
a technique known as Chain of Thoughts (CoT) [8]. logprobs; (2) prompting-based or fine-tuning-based
This can be done in MCQ tests by asking the LLM to techniques that elicit self-evaluation from the model
first provide the reasoning and then select an option [9]; and (3) strategies involving multiple sampling or
on the prompt. An interesting question is whether collaboration among different models [10].
this reasoning has any impact on the confidence of Among these, methods based on token logprobs
the LLM in its choice. In more detail, are the LLM are particularly popular due to their simplicity, effi-
estimated probabilities for its selected option different ciency, and minimal computational overhead [11]. By
whenthemodelreasonsfromthoseofwhenthemodel analyzing the logpros distribution produced during to-
answersdirectly?Ifthereisadifference,doesitapply kengeneration,theseapproachesquantifythemodel’s
to choices that are correct, wrong, or to both? Is the “hesitation” in forming a response, thereby reflecting
useoflogprobs,thereforearecommendedmeasureto its confidence in the final output. A recent work [12]
evaluatetheconfidencelevelofLLMs?Inwhichcases further advances this direction by disentangling un-
is it recommended? Are logprobs a useful tool for the certainty from the logpros distribution into aleatoric
study of LLM metacognition when answering MCQs? andepistemiccomponents,offeringamoresystematic
In this paper, we focus on the metacognitive be- andinterpretableframeworkforconfidenceevaluation.
havior of LLMs when they solve multiple-choice ques- Additionally, some studies have pointed out that, due
tions presented in natural language. In particular, we to the autoregressive nature of LLMs, their responses
study how the self-confidence of LLMs in their MCQ consist of many sequential tokens, yet a small subset
responses varies when the models answer directly or ofcriticaltokenscandeterminetheoveralldirectionof
2 IEEEIntelligentSystems 2025
This work is licensed under a Creative Commons Attribution 4.0 License. For more information, see https://creativecommons.org/licenses/by/4.0/

This article has been accepted for publication in IEEE Intelligent Systems. This is the author's version which has not been fully edited and
content may change prior to final publication. Citation information: DOI 10.1109/MIS.2026.3660833
|     |     |     |     |     |     | Special | Issue | on Metacognitive |     |     | Prediction |     | of AI Behavior |     |
| --- | --- | --- | --- | --- | --- | ------- | ----- | ---------------- | --- | --- | ---------- | --- | -------------- | --- |
theoutput[13].Theseobservationsfurtherunderscore “Please think step by step before answering, con-
the need for more fine-grained research into confi- sidering at least three steps. Once you have the so-
denceestimationforLLMsanditsimplicationsforLLM lution, end the response only with the letter of the
metacognition. solution, in the format {‘sol’: ‘solution’}. Here is an
example:
|                  |             |              |         |                   |     |            | Input:    | A car travels | 60         | kilometers   | per      | hour      | for 2 hours |     |
| ---------------- | ----------- | ------------ | ------- | ----------------- | --- | ---------- | --------- | ------------- | ---------- | ------------ | -------- | --------- | ----------- | --- |
| Reasoning:       |             | Chain of     | thought |                   |     |            |           |               |            |              |          |           |             |     |
|                  |             |              |         |                   |     |            | and       | then 80       | kilometers | per          | hour for | 3 hours.  | What is     |     |
| CoT is           | a prompting | strategy     |         | that guides       |     | language   |           |               |            |              |          |           |             |     |
|                  |             |              |         |                   |     |            | the       | average speed | of         | the car      | for the  | entire    | trip? a) 70 |     |
| models           | to generate | intermediate |         | reasoning         |     | steps be-  |           |               |            |              |          |           |             |     |
|                  |             |              |         |                   |     |            | km/h,     | b) 72 km/h,   | c)         | 75 km/h,     | d) 74    | km/h      |             |     |
| fore arriving    | at          | a final      | answer, | thereby           |     | enhancing  |           |               |            |              |          |           |             |     |
|                  |             |              |         |                   |     |            | Output:   | First,        | I need     | to calculate |          | the total | distance    |     |
| their reasoning  |             | capabilities | and     | interpretability. |     | Since      |           |               |            |              |          |           |             |     |
|                  |             |              |         |                   |     |            | traveled. | For           | the first  | part of      | the      | trip, the | car travels |     |
| its introduction |             | [8], CoT     | has     | been widely       |     | applied to |           |               |            |              |          |           |             |     |
at60km/hfor2hours,sothedistanceis60*2=120
| various | tasks | such as | mathematical |     | reasoning | and |             |       |     |            |      |     |               |     |
| ------- | ----- | ------- | ------------ | --- | --------- | --- | ----------- | ----- | --- | ---------- | ---- | --- | ------------- | --- |
|         |       |         |              |     |           |     | kilometers. | Next, | for | the second | part | of  | the trip, the |     |
symbolicreasoning[14]andhassignificantlyimproved
|                 |     |         |     |         |     |            | car  | travels at | 80 km/h     | for 3 | hours, | so the   | distance is |     |
| --------------- | --- | ------- | --- | ------- | --- | ---------- | ---- | ---------- | ----------- | ----- | ------ | -------- | ----------- | --- |
| the performance |     | of LLMs | on  | complex | and | multi-step |      |            |             |       |        |          |             |     |
|                 |     |         |     |         |     |            | 80 * | 3 = 240    | kilometers. | The   | total  | distance | traveled is |     |
problems.
|     |     |     |     |     |     |     | 120 | + 240 = | 360 kilometers. |     | Now, | I need | to calculate |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ------- | --------------- | --- | ---- | ------ | ------------ | --- |
However,alongsidetheseimprovements,CoTalso
|             |         |                  |     |         |        |        | the     | total time  | spent. The | total | time     | is 2 +    | 3 = 5 hours. |     |
| ----------- | ------- | ---------------- | --- | ------- | ------ | ------ | ------- | ----------- | ---------- | ----- | -------- | --------- | ------------ | --- |
| introduces  | certain | challenges.      |     | Studies | have   | shown  |         |             |            |       |          |           |              |     |
|             |         |                  |     |         |        |        | To find | the average | speed,     |       | I divide | the total | distance     |     |
| that it can | lead    | to overthinking, |     | where   | models | expend |         |             |            |       |          |           |              |     |
bythetotaltime:360kilometers÷5hours=72km/h.
unnecessarycomputationalresourcesonsimpleprob-
|           |     |          |        |           |     |           | Therefore, | the | correct | answer | is {‘sol’: | ‘b’}”. |     |     |
| --------- | --- | -------- | ------ | --------- | --- | --------- | ---------- | --- | ------- | ------ | ---------- | ------ | --- | --- |
| lems [15] | and | may even | follow | incorrect |     | reasoning |            |     |         |        |            |        |     |     |
paths that result in wrong answers [16]. While consid- Theformat{‘sol’:‘solution’}isusedonlyforevalua-
erable research has focused on the performance im- tion convenience and does not change the fact that
|            |         |            |     |            |     |            | the | question | and reasoning |     | process | are | in natural |     |
| ---------- | ------- | ---------- | --- | ---------- | --- | ---------- | --- | -------- | ------------- | --- | ------- | --- | ---------- | --- |
| plications | of CoT, | its impact | on  | confidence |     | estimation |     |          |               |     |         |     |            |     |
remains underexplored. language. This format is used to facilitate the parsing
|      |        |              |     |             |     |           | of the | responses | to extract |     | the option | selected | by the |     |
| ---- | ------ | ------------ | --- | ----------- | --- | --------- | ------ | --------- | ---------- | --- | ---------- | -------- | ------ | --- |
| This | gap is | particularly |     | concerning. | A   | logically |        |           |            |     |            |          |        |     |
coherent reasoning process can already be highly model and its estimated probability.
| persuasive  | to        | human users. | If     | a model  | not     | only pro- |     |     |     |     |     |     |     |     |
| ----------- | --------- | ------------ | ------ | -------- | ------- | --------- | --- | --- | --- | --- | --- | --- | --- | --- |
| duces an    | incorrect | conclusion   |        | but also | assigns | it high   |     |     |     |     |     |     |     |     |
| confidence, | the       | erroneous    | output | is more  | likely  | to be     |     |     |     |     |     |     |     |     |
LLMs
| accepted | without | scrutiny. |     |     |     |     |          |           |       |           |         |                    |             |     |
| -------- | ------- | --------- | --- | --- | --- | --- | -------- | --------- | ----- | --------- | ------- | ------------------ | ----------- | --- |
|          |         |           |     |     |     |     | In order | to ensure | that  | the       | results | are representative |             |     |
|          |         |           |     |     |     |     | of the   | current   | LLMs, | we select | open    | and                | proprietary |     |
ESTIMATING CONFIDENCE models from different companies and sizes. In more
|                 |           |         |                 |     |             |        | detail, | we evaluate | the | following  | LLMs. |             |     |     |
| --------------- | --------- | ------- | --------------- | --- | ----------- | ------ | ------- | ----------- | --- | ---------- | ----- | ----------- | --- | --- |
| This section    | describes |         | the methodology |     | used        | in the |         |             |     |            |       |             |     |     |
| evaluation      | including | the     | experimental    |     | procedure,  | the    |         |             |     |            |       |             |     |     |
|                 |           |         |                 |     |             |        | •       | Two models  |     | from Meta: |       | LLama3.1-8B | and |     |
| LLMs evaluated, |           | and the | benchmarks      |     | considered. |        |         |             |     |            |       |             |     |     |
LLama3.2-11B.
|     |     |     |     |     |     |     | •   | One model | from | Mistral: | Mistral-7B. |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --------- | ---- | -------- | ----------- | --- | --- | --- |
Procedure
|     |     |     |     |     |     |     | •   | One model | from | Google: | Gemma-2-9B. |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --------- | ---- | ------- | ----------- | --- | --- | --- |
In our evaluation, we consider two different prompts • One model from 01.AI: Yi-1.5-9B.
whenaskingthequestiontothemodel.Inthefirst,the • Two models from OpenAI: GPT-4o-mini and
| model is | asked | to answer | directly: |     |     |     |     |     |     |     |     |     |     |     |
| -------- | ----- | --------- | --------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
GPT-4o.
“Pleaserespondwithonlytheletterofthesolution,
intheformat{‘sol’:‘solution’}.Donotrespondwithany
| other information. |     | Here | is an | example: |     |     |     |     |     |     |     |     |     |     |
| ------------------ | --- | ---- | ----- | -------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Tests
| Input: A | car travels | 60 kilometers |     | per | hour for | 2 hours |     |     |     |     |     |     |     |     |
| -------- | ----------- | ------------- | --- | --- | -------- | ------- | --- | --- | --- | --- | --- | --- | --- | --- |
and then 80 kilometers per hour for 3 hours. What is The benchmark selected for our experiments is the
the average speed of the car for the entire trip? a) 70 Massive Multitask Language Understanding (MMLU)
km/h, b) 72 km/h, c) 75 km/h, d) 74 km/h [4]asitcoversawiderangeoftopicsandweareinter-
Output: {‘sol’: ‘b’}” ested in evaluating if the self-confidence in the results
In the second prompt, as per CoT, the model is depends on the nature of the question. The dataset
askedtoprovidestep-by-stepreasoningbeforeselect- has 57 categories and more than 15,000 questions in
| ing an option: |     |     |     |     |     |     | total. |     |     |                        |     |     |     |     |
| -------------- | --- | --- | --- | --- | --- | --- | ------ | --- | --- | ---------------------- | --- | --- | --- | --- |
| 2025           |     |     |     |     |     |     |        |     |     | IEEEIntelligentSystems |     |     |     | 3   |
This work is licensed under a Creative Commons Attribution 4.0 License. For more information, see https://creativecommons.org/licenses/by/4.0/

This article has been accepted for publication in IEEE Intelligent Systems. This is the author's version which has not been fully edited and
content may change prior to final publication. Citation information: DOI 10.1109/MIS.2026.3660833
| Special | Issue | on Metacognitive |     |     | Prediction | of AI Behavior |     |     |     |     |     |     |
| ------- | ----- | ---------------- | --- | --- | ---------- | -------------- | --- | --- | --- | --- | --- | --- |
EVALUATION
|     | The 57         | categories | of       | MMLU questions |              | were run on     |     |     |     |     |     |     |
| --- | -------------- | ---------- | -------- | -------------- | ------------ | --------------- | --- | --- | --- | --- | --- | --- |
|     | the selected   | models     | with     | the direct     | and          | CoT prompts     |     |     |     |     |     |     |
|     | described      | in the     | previous | section1.      | First,       | we look at      |     |     |     |     |     |     |
|     | the aggregated |            | results  | in terms       | of accuracy. | The ac-         |     |     |     |     |     |     |
|     | curacies       | with both  | prompts  | are            | shown        | in Figure 1 for |     |     |     |     |     |     |
|     | the different  | models.    |          | It can be      | seen         | that accuracy   |     |     |     |     |     |     |
increaseswhenthemodelsreasonbeforeselectingthe
|     | option, | as reported | in  | the literature | [17]. |     |        |            |               |             |        |        |
| --- | ------- | ----------- | --- | -------------- | ----- | --- | ------ | ---------- | ------------- | ----------- | ------ | ------ |
|     |         |             |     |                |       |     | FIGURE | 2. Average | Probabilities | of Selected | Option | Across |
ModelsonMMLUwithDirectandCoTPrompts
|     |     |     |     |     |     |     | Expected     | Calibration | Error (ECE)      | and | the Brier | score      |
| --- | --- | --- | --- | --- | --- | --- | ------------ | ----------- | ---------------- | --- | --------- | ---------- |
|     |     |     |     |     |     |     | under Direct | and         | CoT prompting2.  |     | The       | values are |
|     |     |     |     |     |     |     | presentedin  | Table1.On   | allquestions,CoT |     |           | increases  |
|     |     |     |     |     |     |     | ECE for      | five of the | seven models     | and | increases | Brier      |
scoresforseveralofthem,indicatingworsecalibration.
Toisolatetheeffectofanswerchanges,weperformed
FIGURE 1. Accuracy Comparison Across Models on MMLU an ablation study by restricting the analysis to the
CategorieswithDirectandCoTPrompts subset of questions where Direct and CoT select the
sameoption.Inthiscase,ECEincreasesforallseven
|     |     |     |     |     |     |     | models, | and Brier | scores increase |     | for six, | showing |
| --- | --- | --- | --- | --- | --- | --- | ------- | --------- | --------------- | --- | -------- | ------- |
The next step is to examine the confidence that that the overconfidence effect is driven by the pres-
LLMs have in their responses. This is illustrated in ence of reasoning itself rather than by CoT merely
Figure 2 which shows the average probability of the choosing different options. In summary, these results
selectedoptionforbothdirectandCoTprompts.Itcan indicate that the higher probabilities assigned to the
beobservedthatallLLMsincreasetheirconfidencein selected options under CoT do not generally translate
the selected option under CoT prompting. To assess intobetter-calibratedpredictionsandoftenexacerbate
whether there was a statistically significant difference overconfidence, particularly on wrong answers.
between the results of direct and CoT prompts, we To better understand this increase in the models’
conducted paired t-tests on the log probabilities of self-confidence we first analyze the distribution of the
the selected options across samples. The results for probabilitiesinFigures3and4forcorrectandincorrect
all models indicated a significant difference between answers.Inbothcases,thereisacleareffectofvalues
the two conditions, with p < 1×10−10. Overall, this concentratingclosertoonewiththeCoTprompt,which
increase in confidence may be partially explained by is consistent with the results obtained for the average
the improved accuracy under CoT prompting, which and reported in previous figures. Moreover, this right-
leads to more correct answers and thus higher model ward shift is more pronounced for incorrect answers
confidence. However, when we separately analyze than for correct ones, indicating that CoT amplifies
correct and incorrect answers, it is worth noting that high-confidencepredictionsespeciallywhenthemodel
|     | while | models are | generally | more | confident | when the | is wrong. |     |     |     |     |     |
| --- | ----- | ---------- | --------- | ---- | --------- | -------- | --------- | --- | --- | --- | --- | --- |
selected answer is correct, the increase in confidence It is of interest to see if this effect is consistent
is actually larger for incorrect answers. Therefore, the across the different categories in MMLU or if it only
observed increase in confidence cannot be fully at- appliestoafew,forexample,thoseinwhichreasoning
tributed to improved accuracy under CoT prompts. helps more. To visualize this, the increment in self-
To quantify how these confidence changes affect confidence and accuracy for each of the 57 subjects
calibration, we next computed, for each model, the with CoT instead of direct answering is shown as a
1Theresultsandscriptsusedareavailableathttps://github. 2Additional reliability diagrams are included in the public
com/aMa2210/LLM_MCQ_LogProbs repositoryunder/Figure/reliability_figure.
| 4   |     | IEEEIntelligentSystems |     |     |     |     |     |     |     |     |     | 2025 |
| --- | --- | ---------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ---- |
This work is licensed under a Creative Commons Attribution 4.0 License. For more information, see https://creativecommons.org/licenses/by/4.0/

This article has been accepted for publication in IEEE Intelligent Systems. This is the author's version which has not been fully edited and
content may change prior to final publication. Citation information: DOI 10.1109/MIS.2026.3660833
|     |     |     |     |     | Special | Issue | on  | Metacognitive |     |     | Prediction | of  | AI Behavior |     |
| --- | --- | --- | --- | --- | ------- | ----- | --- | ------------- | --- | --- | ---------- | --- | ----------- | --- |
TABLE1. ExpectedCalibrationError(ECE)andBrierscoresonMMLUunderDirectandCoTprompting.Eachcellshowsthe
valueonallquestions,withthevalueontheconsistentsubset(sameanswerunderDirectandCoT)inparentheses.
|                                                                             |     | Model        |     |            | ECE |            |            | Brier  |            |     |     |     |     |     |
| --------------------------------------------------------------------------- | --- | ------------ | --- | ---------- | --- | ---------- | ---------- | ------ | ---------- | --- | --- | --- | --- | --- |
|                                                                             |     |              |     | Direct     |     | CoT        |            | Direct | CoT        |     |     |     |     |     |
|                                                                             |     | LLaMA3.1-8B  |     | 0.11(0.06) |     | 0.28(0.21) | 0.51(0.36) |        | 0.60(0.44) |     |     |     |     |     |
|                                                                             |     | LLaMA3.2-11B |     | 0.11(0.06) |     | 0.29(0.21) | 0.51(0.36) |        | 0.61(0.44) |     |     |     |     |     |
|                                                                             |     | Mistral-7B   |     | 0.31(0.22) |     | 0.38(0.29) | 0.74(0.56) |        | 0.80(0.61) |     |     |     |     |     |
|                                                                             |     | Gemma-2-9B   |     | 0.23(0.17) |     | 0.24(0.19) | 0.53(0.39) |        | 0.50(0.41) |     |     |     |     |     |
|                                                                             |     | Yi-1.5-9B    |     | 0.22(0.14) |     | 0.30(0.23) | 0.57(0.41) |        | 0.62(0.47) |     |     |     |     |     |
|                                                                             |     | GPT-4o-mini  |     | 0.21(0.12) |     | 0.18(0.14) | 0.46(0.27) |        | 0.37(0.28) |     |     |     |     |     |
|                                                                             |     | GPT-4o       |     | 0.13(0.07) |     | 0.11(0.09) | 0.28(0.17) |        | 0.22(0.17) |     |     |     |     |     |
| FIGURE3. ProbabilityDistributionofCorrectlySelectedOptionAcrossModelsinMMLU |     |              |     |            |     |            |            |        |            |     |     |     |     |     |
heatmapinFigure5.TheMMLUsubjectsaredisplayed this effect has also been observed to some extent in
in growing order of the estimated probability of the humanswhenansweringMCQ[18].Itshouldbenoted
selected answer when incorrect, averaged over the thatintherestofthediscussion,human–LLMparallels
sevenmodels3.Itcanbeobservedthatanincreasein
areusedonlyasqualitativeanalogiesandinterpretive
self-confidence occurs for all categories in practically context; we do not conduct human experiments or
all models. The subjects with larger gains are mostly quantitative human–LLM comparisons in this work.
relatedtoscienceexceptforglobalfactsthatareinthe Furthermore, as shown in Figure 5, for questions
topten(bottomteninthefigure).Therealsoseemsto
|                            |     |         |           |          |     | such   | as      | those related |            | to history | or             | moral  | disputes, |     |
| -------------------------- | --- | ------- | --------- | -------- | --- | ------ | ------- | ------------- | ---------- | ---------- | -------------- | ------ | --------- | --- |
| be some correlation        |     | between | increased | accuracy | and |        |         |               |            |            |                |        |           |     |
|                            |     |         |           |          |     | which  | require | minimal       | reasoning, |            | the            | impact | of rea-   |     |
| increased self-confidence. |     |         |           |          |     |        |         |               |            |            |                |        |           |     |
|                            |     |         |           |          |     | soning | on      | the accuracy  |            | of LLMs    | is negligible, |        | and in    |     |
|                            |     |         |           |          |     | many   | cases,  | accuracy      |            | actually   | decreases.     |        | However,  |     |
simultaneously,theconfidenceofthemodelwhenpro-
DISCUSSION
|     |     |     |     |     |     | viding | incorrect | answers |     | increases | significantly. |     | This |     |
| --- | --- | --- | --- | --- | --- | ------ | --------- | ------- | --- | --------- | -------------- | --- | ---- | --- |
TheresultsinFigure4showthatwhenLLMsgenerate
|                      |                |               |            |               |              | suggests    |      | that LLMs      | generating |            | more  | reasoning | in-       |     |
| -------------------- | -------------- | ------------- | ---------- | ------------- | ------------ | ----------- | ---- | -------------- | ---------- | ---------- | ----- | --------- | --------- | --- |
| incorrect responses, |                | the frequency |            | of the "wrong | and          |             |      |                |            |            |       |           |           |     |
|                      |                |               |            |               |              | formation   |      | may actually   |            | be harmful | in    | some      | cases.    |     |
| confident" scenario  |                | significantly | exceeds    |               | that of      | the         |      |                |            |            |       |           |           |     |
|                      |                |               |            |               |              | Experiments |      | on MCQ         |            | in medical | exams | [19]      | have      |     |
| "wrong and           | not confident" | scenario,     |            | particularly  | when         |             |      |                |            |            |       |           |           |     |
|                      |                |               |            |               |              | shown       | that | non-analytical |            | reasoning, |       | which     | relies on |     |
| LLMs are required    |                | to reason,    | suggesting |               | a limitation |             |      |                |            |            |       |           |           |     |
intuitiontoquicklyanswerquestions,ledtothecorrect
| of the metacognitive |     | capabilities | of  | LLMs. | However, |     |     |     |     |     |     |     |     |     |
| -------------------- | --- | ------------ | --- | ----- | -------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
answerevenmoreeffectivelythananalyticalreasoning.
Thisisprimarilybecausenon-analyticalreasoningcan
|            |             |                  |     |               |     | more | efficiently | utilize    | the     | test | taker’s prior | experience |     |     |
| ---------- | ----------- | ---------------- | --- | ------------- | --- | ---- | ----------- | ---------- | ------- | ---- | ------------- | ---------- | --- | --- |
| 3The exact | computation | first normalizes |     | the increment |     | by   |             |            |         |      |               |            |     |     |
|            |             |                  |     |               |     | with | similar     | questions, | whereas |      | reasoning     | processes  |     |     |
themeanonthemodelsandcomputestheaverageoverthe
sevenmodelsexcludingthelowestandhighestvalues. maycausethisexperiencetobecomeineffective,thus
| 2025 |     |     |     |     |     |     |     |     | IEEEIntelligentSystems |     |     |     |     | 5   |
| ---- | --- | --- | --- | --- | --- | --- | --- | --- | ---------------------- | --- | --- | --- | --- | --- |
This work is licensed under a Creative Commons Attribution 4.0 License. For more information, see https://creativecommons.org/licenses/by/4.0/

This article has been accepted for publication in IEEE Intelligent Systems. This is the author's version which has not been fully edited and
content may change prior to final publication. Citation information: DOI 10.1109/MIS.2026.3660833
| Special | Issue    | on                                                                   | Metacognitive |     | Prediction |     | of AI Behavior |     |     |     |     |     |     |
| ------- | -------- | -------------------------------------------------------------------- | ------------- | --- | ---------- | --- | -------------- | --- | --- | --- | --- | --- | --- |
|         | FIGURE4. | ProbabilityDistributionofIncorrectlySelectedOptionAcrossModelsinMMLU |               |     |            |     |                |     |     |     |     |     |     |
leading to incorrect choices. This provides a poten- answer without reasoning. In contrast, the example in
tial explanation for our findings. For questions involv- Figure7showsacasewheretheLLMselectsanincor-
ing common sense, LLMs undoubtedly possess vast rectoptionafterareasoningthatwaslogicallycoherent
amounts of experience during their training process. butincorrect.Althoughthemodelwasseeminglycom-
When reasoning is required before answering, the pelled to select option ‘c’, the probability assigned to
influenceofthisexperienceisdiminished,causingthe the token ‘c’ was only 94%, noticeably lower than the
model to potentially rely on its erroneous reasoning over 99% observed when LLMs performed a correct
based on faulty premises, resulting in incorrect an- reasoning.Theseexamplesrevealtwokeyinsights:(1)
|     | swers. |          |     |     |                 |      |         | confidencecanstillincreaseevenwhenthereasoning |     |          |     |                  |            |
| --- | ------ | -------- | --- | --- | --------------- | ---- | ------- | ---------------------------------------------- | --- | -------- | --- | ---------------- | ---------- |
|     |        |          |     |     |                 |      |         | fails to effectively                           |     | guide    | the | choice; and      | (2) in the |
|     | The    | increase | in  | LLM | self-confidence | when | it pro- |                                                |     |          |     |                  |            |
|     |        |          |     |     |                 |      |         | context of                                     | CoT | prompts, | the | final confidence | in the     |
videsreasoningbeforeansweringcanberelatedtothe
auto-regressivenatureofthesemodelsthatpredictthe selected option still carries potential value. Therefore,
|     |            |       |     |     |                |      |       | it seems | that more | studies | are | needed to | see if the |
| --- | ---------- | ----- | --- | --- | -------------- | ---- | ----- | -------- | --------- | ------- | --- | --------- | ---------- |
|     | next token | based | on  | the | previous ones. | This | means |          |           |         |     |           |            |
confidenceofthemodelsfollowsthesamepatternsas
|     | that if | the reasoning |     | is convincing | and | supports | the |            |         |        |       |                  |         |
| --- | ------- | ------------- | --- | ------------- | --- | -------- | --- | ---------- | ------- | ------ | ----- | ---------------- | ------- |
|     |         |               |     |               |     |          |     | in humans. | If that | is the | case, | it could provide | insight |
selectionofagivenoption,themodelwouldtendtoas-
|     |     |     |     |     |     |     |     | into how | LLMs | work. |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | -------- | ---- | ----- | --- | --- | --- |
signitalargerprobabilityasthenexttoken.Infact,this
behavior has been consistently observed in humans, In summary, the results show how the confidence
|     |     |     |     |     |     |     |     | of the model | is, | as in humans, |     | highly dependent | on  |
| --- | --- | --- | --- | --- | --- | --- | --- | ------------ | --- | ------------- | --- | ---------------- | --- |
whentheyexplaintheanswer,theirconfidenceintheir
|     |          |            |     |           |          |             |     | several    | factors | and therefore |     | should be    | used with |
| --- | -------- | ---------- | --- | --------- | -------- | ----------- | --- | ---------- | ------- | ------------- | --- | ------------ | --------- |
|     | response | increases, |     | as stated | in [20], | "explaining | is  |            |         |               |     |              |           |
|     |          |            |     |           |          |             |     | caution as | a tool  | to evaluate   | LLM | performance. | More      |
believing".
|     |     |     |     |     |     |     |     | research | is needed | to understand |     | when confidence | is  |
| --- | --- | --- | --- | --- | --- | --- | --- | -------- | --------- | ------------- | --- | --------------- | --- |
However,itremainsanopenquestionwhetherthis
|     |          |               |     |     |                 |     |           | a valid performance |     | indicator |     | and can be | used as a |
| --- | -------- | ------------- | --- | --- | --------------- | --- | --------- | ------------------- | --- | --------- | --- | ---------- | --------- |
|     | increase | in confidence |     | is  | entirely driven | by  | the auto- |                     |     |           |     |            |           |
metacognitiontoolforLLMs.Existingstudiesonhuman
regressive nature of these models and whether this behavior with regard to confidence provide valuable
|     | implies                                           | that  | the confidence |          | of these       | models   | becomes |             |      |        |         |          |          |
| --- | ------------------------------------------------- | ----- | -------------- | -------- | -------------- | -------- | ------- | ----------- | ---- | ------ | ------- | -------- | -------- |
|     |                                                   |       |                |          |                |          |         | information | that | should | be used | in these | research |
|     | completelyunreliableinthelatterstagesofreasoning. |       |                |          |                |          |         | efforts.    |      |        |         |          |          |
|     | To explore                                        | this, | we             | examined | the responses  |          | of the  |             |      |        |         |          |          |
|     | models                                            | and   | selected       | two      | representative | samples. | In      |             |      |        |         |          |          |
CONCLUSION
|     | the example |     | shown | in Figure | 6, the | LLM performed | a   |     |     |     |     |     |     |
| --- | ----------- | --- | ----- | --------- | ------ | ------------- | --- | --- | --- | --- | --- | --- | --- |
flawed reasoning process that did not introduce any This paper has studied how the self-confidence of
new useful information to support the final choice. LLMs in their answers to multiple choice questions
However,themodelstillselectedthecorrectoptionand depends on whether the models answer directly with
itsconfidenceincreasedbyapproximately10percent- theselectedoptionsoriftheyprovidefirststep-by-step
age points compared to when it provided the correct reasoningandthenselectanoption.Theresultsforthe
| 6   |     | IEEEIntelligentSystems |     |     |     |     |     |     |     |     |     |     | 2025 |
| --- | --- | ---------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ---- |
This work is licensed under a Creative Commons Attribution 4.0 License. For more information, see https://creativecommons.org/licenses/by/4.0/

This article has been accepted for publication in IEEE Intelligent Systems. This is the author's version which has not been fully edited and
content may change prior to final publication. Citation information: DOI 10.1109/MIS.2026.3660833
|     | Special Issue | on Metacognitive | Prediction | of AI Behavior |     |
| --- | ------------- | ---------------- | ---------- | -------------- | --- |
FIGURE5. Incrementsinaccuracy,intheprobabilityoftheselectedoption,intheprobabilityoftheselectedoptionforcorrect
answers and in the probability of the selected option for incorrect answers for the different subjects in MMLU across models
withCoTinsteadofDirectanswers.
| 2025 |     |     | IEEEIntelligentSystems |     | 7   |
| ---- | --- | --- | ---------------------- | --- | --- |
This work is licensed under a Creative Commons Attribution 4.0 License. For more information, see https://creativecommons.org/licenses/by/4.0/

This article has been accepted for publication in IEEE Intelligent Systems. This is the author's version which has not been fully edited and
content may change prior to final publication. Citation information: DOI 10.1109/MIS.2026.3660833
| Special | Issue | on Metacognitive | Prediction | of AI Behavior |               |                |                 |             |            |            |           |
| ------- | ----- | ---------------- | ---------- | -------------- | ------------- | -------------- | --------------- | ----------- | ---------- | ---------- | --------- |
|         |       |                  |            |                | such as       | ECE            | and Brier       | score,      | we further |            | show that |
|         |       |                  |            |                | CoT prompting |                | worsens         | calibration | by         | increasing | the       |
|         |       |                  |            |                | proportion    | of             | high-confidence |             | wrong      | answers.   | These     |
|         |       |                  |            |                | results       | are consistent |                 | with human  | studies    |            | on confi- |
dence,andsuggestthatfurtherresearchisneededto
|     |     |     |     |     | understand | when | and | how LLM | confidence |     | estimates |
| --- | --- | --- | --- | --- | ---------- | ---- | --- | ------- | ---------- | --- | --------- |
canbeusedforevaluationortoassessmetacognition
|     |     |     |     |     | in LLMs. | In particular, |     | our findings |     | indicate | that in |
| --- | --- | --- | --- | --- | -------- | -------------- | --- | ------------ | --- | -------- | ------- |
MCQevaluationsettingswithCoTprompting,logprob-
|     |     |     |     |     | based confidence |     | should  | be  | used with | caution | as a |
| --- | --- | --- | --- | --- | ---------------- | --- | ------- | --- | --------- | ------- | ---- |
|     |     |     |     |     | metacognitive    |     | signal. |     |           |         |      |
Althoughthispaperanalyzestheimpactofdifferent
|     |        |               |                        |        | prompts       | on the | confidence   | of            | LLMs,          | several    | limita-   |
| --- | ------ | ------------- | ---------------------- | ------ | ------------- | ------ | ------------ | ------------- | -------------- | ---------- | --------- |
|     |        |               |                        |        | tions remain. |        | First, in    | terms         | of model       | selection, | only      |
|     |        |               |                        |        | relatively    | small  | open-weights |               | models         | were       | included. |
|     |        |               |                        |        | Although      | larger | models       | such          | as GPT-4o-mini |            | and       |
|     |        |               |                        |        | GPT-4o        | were   | also used,   | incorporating |                | a wider    | range     |
|     | FIGURE | 6. An example | where the LLM performs | flawed |               |        |              |               |                |            |           |
|     |        |               |                        |        | of models     | with   | varying      | sizes         | could          | help       | determine |
reasoningbutstillselectsthecorrectanswer whether model size influences the extent to which
|     |     |     |     |     | CoT prompting |     | affects | confidence. | Second, |     | the study |
| --- | --- | --- | --- | --- | ------------- | --- | ------- | ----------- | ------- | --- | --------- |
reliessolelyontheMMLUbenchmark;usingadditional
benchmarkscouldstrengthenthefindingsandbroaden
theresearchscope.WechoseMMLUbecauseitspans
57diversesubjects,includingbothreasoning-intensive
|     |     |     |     |     | and more | fact-based |     | categories, | but | extending | this |
| --- | --- | --- | --- | --- | -------- | ---------- | --- | ----------- | --- | --------- | ---- |
analysistootherbenchmarksandtaskformats(includ-
|     |     |     |     |     | ing open-ended |     | generation) | is  | an important |     | direction |
| --- | --- | --- | --- | --- | -------------- | --- | ----------- | --- | ------------ | --- | --------- |
forfuturework.However,atthesametime,morerobust
confidenceestimationmethodsareneededtoaddress
|     |     |     |     |     | potential       | issues     | related     | to differences |         | in         | response |
| --- | --- | --- | --- | --- | --------------- | ---------- | ----------- | -------------- | ------- | ---------- | -------- |
|     |     |     |     |     | lengths.        | Future     | work should | also           | explore | more       | robust   |
|     |     |     |     |     | confidence      | estimation |             | methods        | that    | explicitly | account  |
|     |     |     |     |     | for differences |            | in response |                | length  | and CoT    | depth,   |
|     |     |     |     |     | rather than     | relying    | solely      | on             | logprob | values.    | Lastly,  |
althoughthestudynotesthatLLMbehavioralignswith
humanpatterns,itlacksaquantitativemeasuretoas-
|     |     |     |     |     | sess this   | similarity. | Human      | experiments     |              | could    | provide    |
| --- | --- | --- | --- | --- | ----------- | ----------- | ---------- | --------------- | ------------ | -------- | ---------- |
|     |     |     |     |     | further     | insight     | into these | characteristics |              | in       | LLMs. A    |
|     |     |     |     |     | systematic, | matched     | human–LLM  |                 | study        | of       | confidence |
|     |     |     |     |     | reports     | on MCQs     | would      | be              | particularly | valuable | to         |
FIGURE7.AnexamplewheretheLLMperformsincorrectbut better understand the similarities and differences in
|     |     |     |     |     | metacognitive |     | behavior. |     |     |     |     |
| --- | --- | --- | --- | --- | ------------- | --- | --------- | --- | --- | --- | --- |
coherentreasoning,leadingtoawronganswer
57subjectsoftheMMLUbenchmarkandinsevendif-
ACKNOWLEDGMENTS
|     | ferentLLMs | showthatthe | estimatedprobabilityof | the |     |     |     |     |     |     |     |
| --- | ---------- | ----------- | ---------------------- | --- | --- | --- | --- | --- | --- | --- | --- |
selectedresponseincreaseswhenthemodelsprovide This work was supported by the Agencia Estatal
reasoning before answering. This occurs regardless de Investigación (AEI) (doi:10.13039/501100011033)
of whether the option selected by the LLM is correct. under Grants FUN4DATE (PID2022-136684OB-C22)
In fact, the increase in self-confidence is systemati- andSMARTY(PCI2024-153434)andbytheEuropean
cally larger when the selected option is incorrect than Commission through the Chips Act Joint Undertaking
when it is correct. Using standard calibration metrics project SMARTY (Grant 101140087).
| 8   |     | IEEEIntelligentSystems |     |     |     |     |     |     |     |     | 2025 |
| --- | --- | ---------------------- | --- | --- | --- | --- | --- | --- | --- | --- | ---- |
This work is licensed under a Creative Commons Attribution 4.0 License. For more information, see https://creativecommons.org/licenses/by/4.0/

This article has been accepted for publication in IEEE Intelligent Systems. This is the author's version which has not been fully edited and
content may change prior to final publication. Citation information: DOI 10.1109/MIS.2026.3660833
|     |     |     |     |     | Special | Issue on Metacognitive |     | Prediction |     | of AI Behavior |     |
| --- | --- | --- | --- | --- | ------- | ---------------------- | --- | ---------- | --- | -------------- | --- |
REFERENCES dez, J. Jacobson, J. Kernion, S. Kravec, L. Lovitt,
|     |     |     |     |     |     | K. Ndousse, |     | C. Olsson, | S. Ringer, | D. Amodei, |     |
| --- | --- | --- | --- | --- | --- | ----------- | --- | ---------- | ---------- | ---------- | --- |
1. Z.Guo,R.Jin,C.Liu,Y.Huang,D.Shi,L.Yu,Y.Liu,
|     |     |     |     |     |     | T. Brown, | J. Clark, | N. Joseph, | B. Mann, | S. McCan- |     |
| --- | --- | --- | --- | --- | --- | --------- | --------- | ---------- | -------- | --------- | --- |
J. Li, B. Xiong, D. Xiong et al., “Evaluating large dlish, C. Olah, and J. Kaplan, “Language Models
language models: A comprehensive survey,” arXiv (Mostly) Know What They Know,” arXiv e-prints, p.
|     | preprintarXiv:2310.19736,2023. |     |     |     |     | arXiv:2207.05221,Jul.2022. |     |     |     |     |     |
| --- | ------------------------------ | --- | --- | --- | --- | -------------------------- | --- | --- | --- | --- | --- |
2. W.-L.Chiang,L.Zheng,Y.Sheng,A.N.Angelopou- 10. P. Wang, Y. Wang, M. Diao, K. He, G. Dong,
|     | los, T. Li, | D. Li, | B. Zhu, | H. Zhang, | M. Jordan, |     |     |     |     |     |     |
| --- | ----------- | ------ | ------- | --------- | ---------- | --- | --- | --- | --- | --- | --- |
andW.Xu,“Multi-perspectiveconsistencyenhances
J. E. Gonzalez, and I. Stoica, “Chatbot arena: An confidence estimation in large language models,”
open platform for evaluating LLMs by human pref- ArXiv,vol.abs/2402.11279,2024.[Online].Available:
erence,” in Proceedings of the 41st International https://api.semanticscholar.org/CorpusID:267750237
Conference on Machine Learning, ser. Proceedings 11. C.Guo,G.Pleiss,Y.Sun,andK.Q.Weinberger,“On
|     | of Machine | Learning | Research, | R.  | Salakhutdinov, |             |           |        |            |             |     |
| --- | ---------- | -------- | --------- | --- | -------------- | ----------- | --------- | ------ | ---------- | ----------- | --- |
|     |            |          |           |     |                | calibration | of modern | neural | networks,” | in Proceed- |     |
Z. Kolter, K. Heller, A. Weller, N. Oliver, J. Scarlett, ingsofthe34thInternationalConferenceonMachine
and F. Berkenkamp, Eds., vol. 235. PMLR, 21–27 Learning - Volume 70, ser. ICML’17. JMLR.org,
|     | Jul2024,pp.8359–8388. |     |     |     |     | 2017,p.1321–1330. |     |     |     |     |     |
| --- | --------------------- | --- | --- | --- | --- | ----------------- | --- | --- | --- | --- | --- |
3. L.Zheng,W.-L.Chiang,Y.Sheng,S.Zhuang,Z.Wu, 12. H. Ma, J. Chen, J. Tianyi Zhou, G. Wang, and
Y.Zhuang,Z.Lin,Z.Li,D.Li,E.Xingetal.,“Judging
|     |     |     |     |     |     | C. Zhang, | “Estimating | LLM | Uncertainty | with Ev- |     |
| --- | --- | --- | --- | --- | --- | --------- | ----------- | --- | ----------- | -------- | --- |
llm-as-a-judge with mt-bench and chatbot arena,” idence,” arXiv e-prints, p. arXiv:2502.00290, Feb.
AdvancesinNeuralInformationProcessingSystems,
2025.
vol.36,2024. 13. E. J. Bigelow, A. Holtzman, H. Tanaka, and T. Ull-
4. D. Hendrycks, C. Burns, S. Basart, A. Zou, man, “Forking paths in neural text generation,” in
M.Mazeika,D.Song,andJ.Steinhardt,“Measuring TheThirteenthInternationalConferenceonLearning
|     | massivemultitasklanguageunderstanding,”inInter- |     |             |                  |     | Representations,2025. |     |     |     |     |     |
| --- | ----------------------------------------------- | --- | ----------- | ---------------- | --- | --------------------- | --- | --- | --- | --- | --- |
|     | national Conference                             |     | on Learning | Representations, |     |                       |     |     |     |     |     |
14. T.Kojima,S.S.Gu,M.Reid,Y.Matsuo,andY.Iwa-
|     | 2021. |     |     |     |     | sawa,“Largelanguagemodelsarezero-shotreason- |     |     |     |     |     |
| --- | ----- | --- | --- | --- | --- | -------------------------------------------- | --- | --- | --- | --- | --- |
5. J. Geng, F. Cai, Y. Wang, H. Koeppl, P. Nakov, and ers,”inProceedingsofthe36thInternationalConfer-
I.Gurevych,“Asurveyofconfidenceestimationand enceonNeuralInformationProcessingSystems,ser.
calibrationinlargelanguagemodels,”inProceedings NIPS’22. RedHook,NY,USA:CurranAssociates
ofthe2024ConferenceoftheNorthAmericanChap-
Inc.,2022.
ter of the Association for Computational Linguistics: 15. X. Chen, J. Xu, T. Liang, Z. He, J. Pang, D. Yu,
Human Language Technologies (Volume 1: Long L. Song, Q. Liu, M. Zhou, Z. Zhang, R. Wang,
Papers),2024,pp.6577–6595. Z. Tu, H. Mi, and D. Yu, “Do not think that
6. F.Ye,M.Yang,J.Pang,L.Wang,D.Wong,E.Yilmaz, much for 2+3=? on the overthinking of o1-like llms,”
S.Shi,andZ.Tu,“Benchmarkingllmsviauncertainty ArXiv,vol.abs/2412.21187,2024.[Online].Available:
quantification,” Advances in Neural Information Pro- https://api.semanticscholar.org/CorpusID:275133600
cessingSystems,vol.37,pp.15356–15385,2024.
|     |     |     |     |     |     | 16. Y. Zhu, | G.  | Li, X. Jiang, | J.  | Li, H. Mei, |     |
| --- | --- | --- | --- | --- | --- | ----------- | --- | ------------- | --- | ----------- | --- |
7. M. Steyvers and M. A. Peters, “Metacognition and Z. Jin, and Y. Dong, “Uncertainty-guided chain-
uncertainty communication in humans and large of-thought for code generation with llms,” ArXiv,
language models,” arXiv preprint arXiv:2504.14045, vol. abs/2503.15341, 2025. [Online]. Available:
|     | 2025. |     |     |     |     | https://api.semanticscholar.org/CorpusID:277113033 |     |     |     |     |     |
| --- | ----- | --- | --- | --- | --- | -------------------------------------------------- | --- | --- | --- | --- | --- |
8. J. Wei, X. Wang, D. Schuurmans, M. Bosma, 17. Z. Chu, J. Chen, Q. Chen, W. Yu, T. He, H. Wang,
B. Ichter, F. Xia, E. H. Chi, Q. V. Le, and D. Zhou, W. Peng, M. Liu, B. Qin, and T. Liu, “Navigate
“Chain-of-thoughtpromptingelicitsreasoninginlarge through enigmatic labyrinth a survey of chain of
language models,” in Proceedings of the 36th Inter- thought reasoning: Advances, frontiers and future,”
nationalConferenceonNeuralInformationProcess- in Proceedings of the 62nd Annual Meeting of the
|     | ing Systems, | ser. | NIPS ’22. | Red | Hook, NY, USA: |     |     |     |     |     |     |
| --- | ------------ | ---- | --------- | --- | -------------- | --- | --- | --- | --- | --- | --- |
AssociationforComputationalLinguistics(Volume1:
|     | CurranAssociatesInc.,2022. |     |     |     |     | LongPapers),2024,pp.1173–1203. |     |     |     |     |     |
| --- | -------------------------- | --- | --- | --- | --- | ------------------------------ | --- | --- | --- | --- | --- |
9. S. Kadavath, T. Conerly, A. Askell, T. Henighan, 18. D. A. Curtis, S. L. Lind, C. K. Boscardin, and
D. Drain, E. Perez, N. Schiefer, Z. Hatfield-Dodds, M.Dellinges,“Doesstudentconfidenceonmultiple-
N. DasSarma, E. Tran-Johnson, S. Johnston, S. El- choicequestionassessmentsprovideusefulinforma-
Showk, A. Jones, N. Elhage, T. Hume, A. Chen, tion?”Medicaleducation,vol.47,no.6,pp.578–584,
|      | Y. Bai, S. | Bowman, | S. Fort, | D. Ganguli, | D. Hernan- | 2013. |     |                        |     |     |     |
| ---- | ---------- | ------- | -------- | ----------- | ---------- | ----- | --- | ---------------------- | --- | --- | --- |
| 2025 |            |         |          |             |            |       |     | IEEEIntelligentSystems |     |     | 9   |
This work is licensed under a Creative Commons Attribution 4.0 License. For more information, see https://creativecommons.org/licenses/by/4.0/

This article has been accepted for publication in IEEE Intelligent Systems. This is the author's version which has not been fully edited and
content may change prior to final publication. Citation information: DOI 10.1109/MIS.2026.3660833
| Special | Issue | on Metacognitive |          |                 | Prediction    | of          | AI Behavior |     |
| ------- | ----- | ---------------- | -------- | --------------- | ------------- | ----------- | ----------- | --- |
|         | 19.   | S. J. Durning,   | T.       | Dong,           | A. R. Artino, | C.          | van der     |     |
|         |       | Vleuten, E.      | Holmboe, | and             | L. Schuwirth, | “Dual       | pro-        |     |
|         |       | cessing theory   | and      | experts’        | reasoning:    | exploring   |             |     |
|         |       | thinking on      | national | multiple-choice |               | questions,” | Per-        |     |
spectivesonmedicalEducation,vol.4,pp.168–175,
2015.
|     | 20. | D. J. Koehler, | “Explanation, |     | imagination, | and | confi- |     |
| --- | --- | -------------- | ------------- | --- | ------------ | --- | ------ | --- |
denceinjudgment.”Psychologicalbulletin,vol.110,
no.3,p.499,1991.
| 10  |     | IEEEIntelligentSystems |     |     |     |     |     | 2025 |
| --- | --- | ---------------------- | --- | --- | --- | --- | --- | ---- |
This work is licensed under a Creative Commons Attribution 4.0 License. For more information, see https://creativecommons.org/licenses/by/4.0/