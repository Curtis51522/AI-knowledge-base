www.nature.com/scientificreports

Limitations of large language
models in clinical problem-solving
arising from inflexible reasoning

Jonathan Kim1, Anna Podlasek2, Kie Shidara3, Feng Liu4, Ahmed Alaa5 & Danilo Bernardo3

Large Language Models (LLMs) have attained human-level accuracy on medical question-answer (QA)
benchmarks. However, their limitations in navigating clinical scenarios requiring flexible reasoning
have recently been shown, raising concerns about the robustness and generalizability of LLM
reasoning across diverse, real-world medical tasks. To probe potential LLM failure modes in clinical
problem-solving, we present the medical abstraction and reasoning corpus (mARC-QA). mARC-QA
assesses clinical reasoning through scenarios designed to exploit the Einstellung effect—the fixation
of thought arising from prior experience, targeting LLM inductive biases toward inflexible pattern
matching from their training data rather than engaging in flexible reasoning. We find that LLMs,
including current state-of-the-art o1, Gemini, Claude, and DeepSeek models, perform poorly compared
to physicians on mARC-QA, often demonstrating lack of commonsense medical reasoning and a
propensity to hallucinate. In addition, uncertainty estimation analyses indicate that LLMs exhibit
overconfidence in their answers, despite their limited accuracy. The failure modes revealed by mARC-
QA in LLM medical reasoning underscore the need to exercise caution when deploying these models in
clinical settings.

The versatility and strong performance of Large Language Models (LLMs) across multiple domains1 have sparked
investigation  of  their  reasoning  capabilities  in  clinical  contexts2.  LLMs  have  demonstrated  high  accuracy  on
the United States Medical Licensing Exam (USMLE)3, USMLE-styled question banks4–6, subspecialty medical
board examinations7,8, and clinical reasoning benchmarks validated for physicians9. Excellent LLM performance
across  multiple  domains  in  medical  question  and  answer  (QA)  benchmarks  has  been  postulated,  in  part,  to
reflect  emergent  reasoning  capabilities10,11.  While  LLM  performance  on  medical  QA  benchmarks  has  been
demonstrated  to  rival  human-level  performance,  their  capabilities  in  simulated  real-world  medical  scenarios
have  been  more  limited12.  Notably,  LLMs  also  demonstrated  limited  performance  in  providing  medical
recommendations in real-world emergency room encounters in a recent large-scale study13, calling into question
their robustness in realistic clinical settings that require adaptive reasoning.

These  limitations  challenge  the  perception  of  LLMs  as  possessing  robust  reasoning  capabilities14.
Furthermore, recent studies have demonstrated the limited generalization capabilities of LLMs, with deficiencies
in planning15, abstraction16, and compositionality17 across various tasks. In addition, striking failure modes of
LLMs in seemingly trivial reasoning tasks have been identified18,19. For example, the Abstraction and Reasoning
Corpus  (ARC)  introduced  by  Francois  Chollet20  reveals  surprising  deficiencies  of  LLMs’  ability  to  reason  in
tasks that even children may solve, suggesting fundamental limitations in the reasoning capabilities of LLMs21.
The limited reasoning capabilities of LLMs have been partially attributed to their reliance on memorization
of tasks seen frequently during training, leading to a loss of generalization for novel tasks22. Indeed, LLMs have
demonstrated limited performance in clinical scenarios demanding flexible reasoning or information-seeking
strategies23,24.  Concerningly,  a  recent  study  revealed  a  substantial  discrepancy  between  LLMs’  miscalibrated
overconfidence in their outputs and their actual accuracy, underscoring the risks of overreliance on LLMs in the
medical domain25. There is a critical need for rigorous benchmarks that identify weaknesses and failure modes
in LLM medical reasoning, as addressing these gaps is essential to improving their trustworthiness in clinical
applications.

Here,  we  introduce  the  Medical  Abstraction  and  Reasoning  Corpus  Question  and  Answer  (mARC-QA)
benchmark, which utilizes an adversarial framework to probe failure modes potentially linked to inflexibility in

1Department  of  Neurology  and  Neurologic  Sciences,  Stanford  University,  Palo  Alto,  CA,  USA.  2Image  Guided
Therapy and Research Facility, University of Dundee, Dundee, UK. 3Weill Institute of Neurology and Neurosciences,
University of California, San Francisco, San Francisco, CA, USA. 4Department of Systems and Enterprises, Stevens
Institute of Technology, Hoboken, NJ, USA. 5Department of EECS, University of California Berkeley, Berkeley, CA,
USA. email: dbernardoj@gmail.com

Scientific Reports |        (2025) 15:39426

| https://doi.org/10.1038/s41598-025-22940-0

1

OPENwww.nature.com/scientificreports/

LLM reasoning. These vulnerabilities may arise from habituation to fixed problem-solving approaches such as
rote pattern matching and inherent inflexibility to move beyond these familiar reasoning patterns, limitations
imposed by neural architecture and training regimes. This mechanized or rigid mode of reasoning in humans,
when counterproductive in novel situations requiring flexible reasoning, is known as the Einstellung effect—a
cognitive  bias  where  rigidity  of  thought  arises  from  prior  experience26.  This  effect  arises  when  a  habitual
problem-solving  strategy,  activated  by  familiar  problem  features,  hinders  reasoning  towards  the  optimal
solution27. mARC-QA alters predictable aspects of medical problems, emphasizing ’long-tail’ or low-probability
reasoning patterns underrepresented in medical texts and QA benchmarks (Figure 1) to induce this effect. Our
findings demonstrate that current LLMs perform poorly on mARC-QA, indicating surprising failure modes in
clinical reasoning. These shortcomings are further compounded by their overconfidence in their outputs despite
their limited performance.

Methods
mARC-QA Question Design
mARC-QA questions are modeled after the multiple-choice format used by the United States Medical Licensing
Examination  (USMLE).  The  dataset  comprises  100  questions  written  by  the  authors  to  resist  memorization,
pattern  matching,  or  interpolation  from  preexisting  medical  QA  benchmarks  and  medical  texts.  Below,  we
describe how the Einstellung effect—rigidity of thought elicited by familiar problem cues26,27—was translated
into  concrete  item-design  decisions,  and  the  steps  we  took  to  distinguish  failures  of  flexible  reasoning  from
alternative failure modes (e.g., incomplete knowledge or prompt misinterpretation).

Operationalizing the Einstellung effect. Each item instantiates at least one of the following manipulations

intended to preferentially trigger a familiar heuristic while making that heuristic counterproductive:

 1.  Familiar-cue with hard counterevidence (cue conflict). The question stem prominently features high-fre-
quency lexical cues (e.g., “anticoagulant”
 “brain bleed”) yet embeds a decisive blocker that invalidates the
stereotyped completion. Figure 1 illustrates this: anticoagulation cues are juxtaposed with complete cerebral
absence; the correct response requires overriding the familiar completion via logical negation (no brain
no intracranial hemorrhage).

⇒

→

 2.  Information-sufficiency gating. Items include an explicit “seek additional information” option. The stem is
crafted so that familiar diagnostic/therapeutic reflexes are plausible but nonjustifiable given the context; the
flexible reasoning strategy is to defer action and request the missing element (e.g., key history, a basic exam
maneuver). This targets adaptive information-seeking and threshold-based decision-making, both of which
are underrepresented in conventional QA and where LLMs demonstrate poor performance23.

 3.  Re-anchoring Thresholds to Context. Key numerical or contextual cues (e.g. labs) are placed near clinical
decision  thresholds  at  or  just  beyond  familiar  clinical  cutoffs  to  trigger  a  reflexive  threshold-crossing  re-
sponse, then explicitly supply context that negates the applicable baseline. The normative move is to re-an-
chor the threshold to the stated context—often to withhold intervention or first seek confirming informa-
tion—rather than adhere to the default cutoff. The correct response hinges on flexible override of the learned
heuristic.

Figure 1.  Demonstration of mARC-QA question utilizing long-tail reasoning pattern. The presented
information is a commonly seen medical QA text pattern (anticoagulant leading to a brain bleed). The
adversarial answer choice targets reliance on rote pattern matching. However, the adversarial answer choice is
easily avoided with deductive reasoning through logical negation—complete absence of a brain renders a brain
bleed impossible. This clinical situation represents a long-tail reasoning pattern further obscuring the correct
answer.

Scientific Reports |        (2025) 15:39426

| https://doi.org/10.1038/s41598-025-22940-0

2

www.nature.com/scientificreports/

mARC-QA Dataset Characteristics
53%  of  questions  include  the  selection  to  seek  more  clinical  data,  which  challenges  the  test-taker  to  decide
whether  there  is  sufficient  clinical  information  to  cross  a  decision  threshold  in  regard  to  the  other  answer
choices. Medical sub-specialties included in the dataset included neurology, neurosurgery, infectious disease,
obstetrics-gynecology, ophthalmology, HEENT, hematology-oncology, gastroenterology, pulmonology, critical
care, cardiology, and emergency medicine. The percentage of mARC-QA questions per medical sub-specialty is
shown in Supplementary Figure 1. To help readers judge whether errors reflect inflexibility rather than missing
knowledge  or  prompt  misinterpretation,  items  were  constrained  so  that  the  correct  choice  requires  at  most
broadly  taught,  early-clinical  knowledge.  Questions  were  included  in  the  dataset  if  a  majority  vote  of  three
physicians deemed them reasonable for a medical student graduate to answer.

Analysis
We compared LLM performance to physician performance on mARC-QA. Physician test takers were recruited
for  this  study  from  the  University  of  California  San  Francisco  (UCSF)  Medical  Center  and  kolabtree.com.
Ethical  approval  for  this  study  was  obtained  from  the  UCSF  Institutional  Review  Board  (IRB#24-42911),
and  informed  consent  to  participate  was  obtained  from  all  participating  test-taker  subjects.  All  experiments
were  performed  in  accordance  with  relevant  guidelines  and  regulations.  Test  takers  were  all  medical  school
graduates, with specialty distribution that included pediatrics (1), internal medicine (3), and neurology (1). All
test takers completed the test online under a 2 hour time limit. The mARC-QA accuracies of five physicians
were  averaged  for  the  reported  average  human  physician  performance.  We  utilized  chain-of-thought  (CoT)
for  all  experiment  prompts  in  LLM  evaluation.  Specifically,  the  Massive  Multitask  Language  Understanding
(MMLU) dataset was used for chain of thought prompting in in-context learning examples28. This approach
followed the methodology outlined by Wang et al. and utilized their publicly available code from the MMLU-Pro
benchmark assessment29. The accuracy of GPT-4o30, o131, Medalpaca32, Meditron-7b33, Claude-Sonnet, Claude-
Opus34, Google Gemini35, and Mistral36 models were evaluated. Closed source models were evaluated using the
respective APIs from Anthropic, Google, and OpenAI. Open-source models were evaluated using Huggingface
and Lambda Labs APIs. The latest versions of publicly available models were utilized with a model cut-off date
of December 19, 2024. A temperature of zero was used when possible to allow for reproducibility of the results;
otherwise, settings followed the defaults used by Wang et al in the MMLU-pro benchmark29. The full parameter
settings that were utilized are available in the shared code-base. Average accuracy across 15 runs of each model
is reported, as uncertainty assessment performance has been reported to plateau beyond this sample size37. 95%
confidence intervals of model performance were calculated using bootstrap analysis, with number of bootstraps
set to 2000. Adjustment for multiple comparisons was performed using the Benjamini and Hochberg procedure.
Measuring  consistency  in  model  output  across  multiple  runs  is  an  established  method  for  uncertainty
estimation  in  LLMs38,39  and  has  been  shown  to  outperform  posthoc  methods  at  uncertainty  estimation40.
Following Lyu et al., we perform uncertainty quantification employing sample consistency40, which has been
shown  to  outperform  token  level  probability  and  confidence  elicitation  in  the  medical  domain41.  In  this
paradigm, the same question is provided to a model several times, and inter-response agreement (consistency)
is  calculated  as  the  uncertainty  measure.  To  induce  stochastic  behavior  inherent  in  LLMs  between  runs,  the
age of the subject in each question is varied by up to 10 days between runs. This does not clinically alter the
medical principle or reasoning that is being assessed for questions in this dataset, as no subjects are of neonatal
or  infantile  age.  A  sample  consistency  sample  size  of  15  was  selected,  as  performance  has  been  reported  to
plateau beyond this sample size37. To assess model calibration, we utilized reliability plots and calculated the
Brier score, following Lyu et al40. Further details regarding the calculation of sample consistency metrics are
available in Supplementary Methods.

Dataset and Code Availability
The mARC-QA problem dataset and the code used to generate the results are publicly available at  h t t p s : / / g i t h u
b . c o m / b e r n a r d o l a b / m A R C - Q A     .

Results
LLMs performance on mARC-QA tasks
We  observed  that  most  LLMs  perform  poorly  on  mARC-QA  tasks,  with  less  than  50%  accuracy  (Figure
2).  We  note  that  several  models  performed  near  or  below  the  chance  level  (less  than  20%).  Human  average
performance  was  66%,  averaged  across  five  physicians,  with  standard  error  ±5.3%.  All  model  accuracies  are
provided in Supplementary Table 1. We observed a general trend for improvement with larger model sizes in
the Claude, Gemini, and OpenAI families. We observed decreased performance with larger model size (405b vs
70b) for the LLama 3.1 model family, which could reflect overfitting related to the quantization used for the 405b
model42. We observed that Medalpaca, Meditron3-7B, and Meditron3-70B models approached 0% performance
due to tangential reasoning patterns (Supplementary Tables 2 and 3), in contrast to their reported moderate
performance  on  conventional  medical  QA  benchmarks32,33.  The  best-performing  models,  DeepSeek-R1,
DeepSeek-V3, Gemini(1.5-pro), and o1, achieved accuracies of 52%, 50%, 50%, and 48%, respectively. However,
even  these  models  exhibited  hallucinations  and  committed  commonsense  reasoning  errors,  as  illustrated  in
question example responses below. Human performance was significantly higher than the performance of each
respective LLM (paired bootstrap, p = 0.0133 for DeepSeek-V3, p = 0.0133 for DeepSeek-R1, p = 0.0204 for
Gemini(1.5-pro), p = 0.00150 for o1, and p < 0.00001 for all others.

Scientific Reports |        (2025) 15:39426

| https://doi.org/10.1038/s41598-025-22940-0

3

www.nature.com/scientificreports/

Figure 2.  Comparison of LLM and human performance on mARC-QA. Colored bars indicate the accuracy
of each model, with colors representing the corresponding model family. The rightmost bar represents
average human performance (0.66), calculated as average accuracy across five physicians. Error bars (black
lines) indicate 95% confidence intervals, derived from bootstrap analysis. The four best-performing models
DeepSeek-R1, DeepSeek-V3, Gemini(v1.5-pro), and o1, achieved accuracies of 52%, 50%, 50%, and 48%,
respectively. Human performance was significantly higher from the performance of each respective LLM
(paired bootstrap, p < 0.05 for all comparisons).

Examples of mARC-QA Questions
mARC-QA examples (Figures 3, 4, 5) demonstrate the adversarial strategy of disrupting the predictability of
familiar medical text patterns to exploit the Einstellung effect, which LLMs may be biased towards due to their
training paradigm involving the next-token prediction of textual patterns prevalent in their training data. This
disruption  involves  the  incorporation  of  long-tail  or  out-of-distribution  medical  reasoning  patterns  into  the
problem structure. The correct long-tail reasoning patterns are juxtaposed among answer options with a high
likelihood  of  token  completion  due  to  frequent  appearance  in  LLM  training  corpora.  The  resulting  contrast
exploits potential LLM inherent bias towards familiar or high-probability completions.

In  the  example  question  shown  in  Figure  3,  o1’s  response  reveals  a  failure  in  fundamental  medical
commonsense reasoning. DeepSeek-R1 also demonstrate a similar pattern of failure (Supplementary Table 4
and 5). Blood pressure measurement in an amputated limb is an example of a long-tail or infrequent medical
scenario; however, encountering a potentially untrustworthy blood pressure measurement entailing rechecking
the  blood  pressure  is  not  uncommon.  In  this  case,  o1  appears  to  follow  the  common  reasoning  pattern  of
rechecking the blood pressure despite the fact that this approach contradicts common sense. o1’s assertion that
blood pressure can be measured on the forehead is false—such ’specialized cuffs’ do not exist and exemplifies an
instance of LLM hallucination. Inspection of the reasoning trace for DeepSeek-R1, also confirms that the source
of error in this example is hallucination that forehead blood pressure measurement is possible (Supplementary
Table 4). In the examples shown in Figures 4 and 5, GPT-4o responses similarly illustrate the Einstellung effect,
revealing deficiencies in medical commonsense reasoning.

Uncertainty Estimation and Calibration
The shortcomings of LLMs in medical reasoning and propensity to hallucinate, as demonstrated here, aligns with
prior  work  demonstrating  similar  limitations  across  various  domains16–19,21,43  and  raises  concerns  regarding
their trustworthiness in medical contexts44,45. Uncertainty estimation has emerged as a method to potentially
mitigate overreliance on LLM by quantifying confidence in their outputs, thereby allowing users to gauge their
trustworthiness41.  Here,  we  utilized  agreement-  and  entropy-based  sample  consistency  (SC)  to  calculate  the
Brier score to compare LLM confidence, as SC methods have been identified to outperform other uncertainty
estimation methods in the medical domain41. Entropy-based and agreement-based Brier scores and reliability
plots  for  the  top-performing  models  (o1,  Gemini-pro,  DeepSeek-V3,  and  DeepSeek-R1)  demonstrated
overconfidence in their responses despite exhibiting low accuracy (Supplementary Figure 2 and Figure 6). We
found that smaller models such as Mistral, GPT4o-mini, Gemini-1.5-flash, and Claude-Sonnet had even greater
overconfidence despite achieving lower accuracy. In general, larger models demonstrated improved calibration

Scientific Reports |        (2025) 15:39426

| https://doi.org/10.1038/s41598-025-22940-0

4

www.nature.com/scientificreports/

Figure 3.  In this example question, o1’s incorrect response reveals a failure in fundamental medical
commonsense reasoning and hallucination—the assertion that blood pressures can be measured on the
forehead is false.

compared to smaller models; however, they remained overconfident despite limited accuracy (Supplementary
Figure 2). We assessed accuracy and Brier Score on MMLU-Pro Professional Clinical Knowledge subset (254
questions)29, and comparatively, mARC induced striking reductions in accuracy and Brier Score. These results
align with recent findings suggesting current LLMs lack metacognition, demonstrating a mismatch between low
uncertainty (or overconfidence) and their actual capabilities in medical reasoning tasks25.

≥

≥

≥

Model behavior on human-miss set
Next, we assessed whether the cases humans miss surface potential benchmark flaws, we analyzed the subset
3/5) was incorrect, which we term the human-miss set. This
of questions on which the physician majority (
comprised 20/100 items (20%). Under more stringent criteria for incorrectness defined as physician majority
4/5)  incorrect,  the  human-miss  set  comprised  only  3  items  (Fig.  6). Thus  we  used  simple  physician
with  (
3/5) for subsequent analysis. On the human-miss set (20 items), pooled human accuracy was 36%
majority (
(95% CI 26–46%), versus 73% on the remaining items. Then, from the 15 stochastic trials per question from
the  preceding  uncertainty  quantification  analysis,  we  calculated  two-sided  Wilson  90%  confidence  intervals
(α = 0.05  one-sided)  on  the  binomial  correctness  rate46,47,  to  assign  a  per-item  confidence  label  as  follows:
11/15 correct), confidently incorrect if
confidently correct if the lower bound exceeded 0.5 (corresponding to
4/15), and otherwise indeterminate (5–10/15). A stacked-
the upper bound was below 0.5 (corresponding to
bar summary of model confidence across all models on the human-miss set is provided in Figure 7. The best
model (DeepSeek-R1) was confidently correct on 45% of items (95% CI 25–65%), confidently incorrect on 40%
(20–65%), and indeterminate on 15% (0–30%). It’s mean accuracy on this subset was 51% (32.0–69.8%). While
DeepSeek-R1 outperforms humans in 45% of the human-miss set, it was confidently incorrect 40% of the time
indicating genuine problem difficulty. This pattern argues against presence of systematic benchmark flaws. If the
benchmark were flawed (e.g. containing ambiguity or incorrect labels) then we would expect both humans and
model performance to trend towards indeterminate decisiveness. In addition, only 8 questions were decisively

≥

≤

Scientific Reports |        (2025) 15:39426

| https://doi.org/10.1038/s41598-025-22940-0

5

www.nature.com/scientificreports/

Figure 4.  In this example question, GPT4o’s incorrect response arises from a deductive reasoning error in
integrating key details about the patient’s condition: (1) The patient lacks a brain, and (2) in the absence of
a brain, normal EEG activity cannot be expected. Therefore, GPT4’s reasoning that there is a possibility of
an intracranial hemorrhage on the basis of abnormal EEG is logically flawed. The problem does not provide
information on the chronicity of lethargy which in this case could be chronic, thus obtaining additional history
is warranted prior to consideration of treatment.

missed by both DeepSeek-R1 and humans, which on manual inspection did not reveal systematic design flaws
(examples demonstrated in Supplementary Table 6).

Discussion
Considering that the progression of AI development has continually drawn on insights from human cognition48–50
and that LLM training is reliant on extensive human-generated data, it is anticipated that LLMs may exhibit
inductive biases that bear functional resemblance to cognitive biases in humans51–53. Characterizing such biases
is essential to assessing their trustworthiness in clinical contexts. Here, we demonstrate that LLMs are vulnerable
to the Einstellung effect in medical QA tasks, where their inflexible adherence to matching learned statistical
patterns impedes effective adaptation to medical scenarios that deviate from traditional medical texts and QA.

The disparity between LLM performance on mARC-QA and conventional medical QA aligns with studies
suggesting that benchmark successes may stem from overfitting to statistical patterns in training data rather than
reflecting emergent reasoning abilities19,54–57. This interpretation is reinforced by studies that have shown LLMs’
limited robustness and increased hallucination rates in low-probability contexts, where reliance on surface-level
statistical  correlations  proves  insufficient19,54,58.  McCoy  et  al.  hypothesized  that  poorer  performance  in  these
low-probability situations stem from biases inherent in the LLM training paradigm, which favors probabilistic
strategies in autoregressive next-token prediction over development of robust deductive or abductive reasoning
capabilities54. Consequently, LLMs may be biased toward surface-level correlations reinforced during training,
which perform well on in-distribution data but hinder the development of generalizable reasoning strategies59,
leaving  them  vulnerable  to  the  Einstellung  effect53.  mARC-QA  targets  this  inductive  bias  by  disrupting  the
predictability of familiar medical problems through incorporation of long-tail concepts which are difficult for
LLMs to capture effectively60. More broadly, many of the observed errors likely reflect the absence of a robust
world model—an internal causal representation that enforces physical and logical constraints, maintains latent
state,  and  supports  plausibility  and  counterfactual  checks.  We  observe  that  this  limitation  is  not  unique  to
medicine and is a central target for improving LLM reasoning in general61.

Our  findings  align  with  recent  evidence  that  LLMs  have  limited  generalization—the  ability  to  effectively
apply  reasoning  to  novel,  out-of-distribution  scenarios62,63.  Deficiencies  of  LLM  generalization  have  been
identified in multiple straightforward tasks18,19,64, including simple mathematical reasoning65, and in planning,

Scientific Reports |        (2025) 15:39426

| https://doi.org/10.1038/s41598-025-22940-0

6

www.nature.com/scientificreports/

Figure 5.  In this example question, GPT4o’s incorrect response and subsequent reasoning reveal a deficiency
in medical commonsense reasoning. A basic principle—both widely taught and intuitively obvious—is that the
first step in assessing a patient who appears to be unconscious is to attempt to wake them.

even with current state-of-the-art models62. Generalization in out-of-distribution contexts is essential in real-
world clinical scenarios, which often demand that reasoning strategies used in familiar, predictable situations
be countermanded to consider more optimal approaches; this cognitive flexibility is foundational for effective
clinical reasoning66. LLM inflexibility in reasoning, as demonstrated on mARC-QA, may hinder their ability
to generalize to novel or unpredictable scenarios, undermining their reliability in real-world clinical contexts.
Subsequently,  reduced  adaptability  to  novelty  or  distribution  shifts  could  undermine  healthcare  systems’
preparedness for future disease outbreaks—particularly those involving novel pathogens akin to COVID-19.

Compounding  these  shortcomings  are  recently  demonstrated  LLM  deficiencies  in  metacognition—
specifically,  the  inability  to  recognize  their  own  limitations—and  overconfidence25.  Lack  of  metacognition

Scientific Reports |        (2025) 15:39426

| https://doi.org/10.1038/s41598-025-22940-0

7

www.nature.com/scientificreports/

Figure 6.  Uncertainty estimation for models on mARC-QA. Entropy-based (left panel) and agreement-based
(right panel) sample consistency was used to calculate Brier scores for top performing models. There is a
general trend for larger and newer models to demonstrate relatively improved accuracy and Brier scores. Color
indicates respective model, with baseline performance on MMLU-Pro (MMLUP) colored black.

and  common  sense  in  LLMs  can  lead  to  adverse  outcomes  if  they  are  overrelied  upon  in  clinical  contexts44.
Our findings suggest that LLM limitations in reasoning may be exacerbated in long-tail or out-of-distribution
contexts.  To  mitigate  these  risks,  the  development  of  selective  prediction  strategies,  as  proposed  by  Goetz  et
al.55, may offer a pathway to AI deployment in clinical scenarios. In this strategy, LLMs could defer to human
clinicians in long-tail or out-of-distribution scenarios, ensuring that critical decisions are supervised by experts
in contexts where LLMs may be unreliable55.

We  acknowledge  several  limitations  in  this  study.  Compared  to  prior  medical  QA  benchmarks  such  as
specialty  board  exams  and  the  USMLE,  mARC-QA  consists  of  a  smaller  set  of  100  questions.  This  reduced
number reflects the nontrivial aspect of crafting questions that test long-tail or out-of-distribution reasoning
patterns, which are more novel than those found in conventional medical QA. Future work will aim to increase
the size of the mARC-QA dataset to improve its robustness. We recognize as well that question curation was
based on physician expertise and not systemically performed. There are recently proposed LLM methods to select
knowledge that is out-of-distribution (OOD), however, to our knowledge, this is not well-studied in medical
contexts. For example, agentic-based OOD question generation has recently been explored in math and science
high-school level question contexts, and future iterations of mARC may generate additional questions in this
manner67. Furthermore, we recognize that expert review of the dataset reflects content validity, not Einstellung
construct validity, and formal construct validation will be explored in future work.

Additionally, while mARC questions might appear punitive by targeting otherwise beneficial heuristics with
“edge-case”  scenarios,  the  intention  is  to  assess  “cognitive”  flexibility—a  key  skill  in  medical  practice,  where
inflexible adherence to heuristics could lead to harm. We recognize that mARC-QA questions are unlikely to be
encountered in the real world; however, our aim is not to benchmark “human-like” cognition or predict human
competence in real-world clinical reasoning—an aim already addressed by existing assessments like the USMLE
and board exams—but to probe failure modes in LLM reasoning in order to target areas where improvement
is needed. Whereas conventional QA benchmarks are established at assessing human clinical reasoning, their
reliability at evaluating LLM reasoning remains unclear25. This limitation highlights the need for complementary
stress tests. Accordingly, to improve applicability to real-world practice, future development will explore long-
tail,  rare  diseases  to  complement  our  focus  on  Einstellung  driven  reasoning.  Rare  disease  evaluations  probe
unusual content68, whereas mARC QA probes unusual reasoning. Both types of stress test are needed as they
probe distinct failure modes.

Lastly,  we  observe  that  human  performance  on  mARC-QA  was  limited,  consistent  with  long-standing
findings  that  humans  may  be  susceptible  to  the  Einstellung  effect69.  The  average  performance  (  66%)—
comparable  to  typical  accuracy  on  board  examinations  and  in-training  assessments70—reflects  the  inherent
variability in effort and reasoning abilities among subjects. On the nine items in the human miss-set where the
best model (DeepSeek-R1) outperformed humans (Figure 7), qualitatively, inspection of answer explanations
(Supplementary Table 7) indicate that the model appeared to properly adhere to constraints in the question stem
and follow logical negation, whereas the human majority did not. These observations indicate that reasoning
models can occasionally surpass human performance, and the potential of newer reasoning models to overcome
Einstellung effect will be explored in future work.

mARC-QA  reveals  limitations  in  LLM  medical  reasoning,  challenging  the  notion  that  human-level
performance on medical QA benchmarks suggests robust medical reasoning capabilities. The findings emphasize

Scientific Reports |        (2025) 15:39426

| https://doi.org/10.1038/s41598-025-22940-0

8

www.nature.com/scientificreports/

Figure 7.  Stacked three-way outcomes for all models on the human-miss subset (items missed by humans;
(N = 20)). Bars show the share of Model-win (model confidently correct where majority of humans erred),
Both-miss (model confidently incorrect and majority of humans erred), and Indeterminate, with models
sorted by Model-win share (descending).

the need for the development of benchmarks that rigorously assess LLM generalization in medical reasoning,
with assessment of reasoning flexibility serving as a potential approach. The observed shortcomings of LLMs in
medical reasoning indicate the need for caution when utilizing LLMs in clinical contexts.

Data Availability
The mARC-QA problem dataset and the code used to generate the results are publicly available at  h t t p s : / / g i t h u
b . c o m / b e r n a r d o l a b / m A R C - Q A .

Received: 27 March 2025; Accepted: 3 October 2025

References
  1.  Bubeck,  Sébastien,  Chandrasekaran,  Varun,  Eldan,  Ronen,  Gehrke,  Johannes,  Horvitz,  Eric,  Kamar,  Ece,  Lee,  Peter,  Lee,  Yin
Tat, Li, Yuanzhi, & Lundberg, Scott, et al. Sparks of artificial general intelligence: Early experiments with gpt-4. arXiv preprint
arXiv:2303.12712, (2023).

  2.  Moor, Michael et al. Foundation models for generalist medical artificial intelligence. Nature 616(7956), 259–265 (2023).
  3.  Gilson, Aidan et al. How does chatgpt perform on the united states medical licensing examination (usmle)? the implications of

large language models for medical education and knowledge assessment. JMIR Med. Educ. 9(1), e45312 (2023).

  4.  Jiang, Lavender Yao et al. Health system-scale language models are all-purpose prediction engines. Nature 619(7969), 357–362

(2023).

  5.  Peng,  Cheng  et  al.  A  study  of  generative  large  language  model  for  medical  research  and  healthcare. NPJ  Digit.  Med.  6(1),  210

(2023).

Scientific Reports |        (2025) 15:39426

| https://doi.org/10.1038/s41598-025-22940-0

9

www.nature.com/scientificreports/

  6.  Zhang, Kai, Zhou, Rong, Adhikarla, Eashan, Yan, Zhiling, Liu, Yixin, Yu, Jun, Liu, Zhengliang, Chen, Xun, Davison, Brian D, Ren,

Hui, et al. A generalist vision–language foundation model for diverse biomedical tasks. Nature Medicine, 1–13, (2024).

  7.  Longwell, Jack B. et al. Performance of large language models on medical oncology examination questions. JAMA Netw. Open 7(6),

e2417641–e2417641 (2024).

  8.  Schubert, Marc Cicero, Wick, Wolfgang & Venkataramani, Varun. Performance of large language models on a neurology board-

style examination. JAMA Netw. Open 6(12), e2346721–e2346721 (2023).

  9.  Cabral, Stephanie et al. Clinical reasoning of a generative artificial intelligence model compared with physicians. JAMA Intern.

Med. 184(5), 581–583 (2024).

 10.  Liévin, Valentin, Hother, Christoffer Egeberg, Motzfeldt, Andreas Geert, Winther, Ole. Can large language models reason about

medical questions? Patterns, 5(3), (2024).

 11.  Kwon, Taeyoon et al. Large language models are clinical reasoners: Reasoning-aware diagnosis framework with prompt-generated

rationales. Proceedings of the AAAI Conference on Artificial Intelligence 38(16), 18417–18425 (2024).

 12.  Hager, Paul et al. Evaluation and mitigation of the limitations of large language models in clinical decision-making. Nat. Med.

30(9), 2613–2622 (2024).

 13.  Williams, Christopher YK., Miao, Brenda Y., Kornblith, Aaron E. & Butte, Atul J. Evaluating the use of large language models to

provide clinical recommendations in the emergency department. Nat. Commun. 15(1), 8236 (2024).

 14.  Mitchell, Melanie. How do we know how smart ai systems are?, (2023).
 15.  Valmeekam, Karthik, Marquez, Matthew, Olmo, Alberto, Sreedharan, Sarath, Kambhampati, Subbarao. Planbench: An extensible
benchmark  for  evaluating  large  language  models  on  planning  and  reasoning  about  change.  Advances  in  Neural  Information
Processing Systems, 36, (2024).

 16.  Mitchell,  Melanie,  Palmarini,  Alessandro  B,  Moskvichev,  Arseny.  Comparing  humans,  gpt-4,  and  gpt-4v  on  abstraction  and

reasoning tasks. arXiv preprint arXiv:2311.09247, (2023).

 17.  Press,  Ofir,  Zhang,  Muru,  Min,  Sewon,  Schmidt,  Ludwig,  Smith,  Noah  A,  &  Lewis,  Mike.  Measuring  and  narrowing  the

compositionality gap in language models. arXiv preprint arXiv:2210.03350, (2022).

 18.  Nezhurina, Marianna, Cipolina-Kun, Lucia, Cherti, Mehdi, & Jitsev, Jenia. Alice in wonderland: Simple tasks showing complete

reasoning breakdown in state-of-the-art large language models. arXiv preprint arXiv:2406.02061, (2024).

 19.  Li, Yinghui, Zhou, Qingyu, Luo, Yuanzhen, Ma, Shirong, Li, Yangning, Zheng, Hai-Tao, Hu, Xuming, & Philip, S Yu. When llms
meet  cunning  texts:  A  fallacy  understanding  benchmark  for  large  language  models.  In  The  Thirty-eight  Conference  on  Neural
Information Processing Systems Datasets and Benchmarks Track, (2024).

 20.  Chollet, François. On the measure of intelligence. arXiv preprint arXiv:1911.01547, (2019).
 21.  Lee,  Seungpil,  Sim,  Woochang,  Shin,  Donghyeon,  Hwang,  Sanha,  Seo,  Wongyu,  Park,  Jiwon,  Lee,  Seokki,  Kim,  Sejin,  &  Kim,
Sundong. Reasoning abilities of large language models: In-depth analysis on the abstraction and reasoning corpus. arXiv preprint
arXiv:2403.11793, (2024).

 22.  Wu, Zhaofeng, Qiu, Linlu, Ross,Alexis, Akyürek, Ekin, Chen, Boyuan, Wang, Bailin, Kim, Najoung, Andreas, Jacob, & Kim, Yoon.
Reasoning or reciting? exploring the capabilities and limitations of language models through counterfactual tasks. arXiv preprint
arXiv:2307.02477, (2023).

 23.  Li, Shuyue Stella, Balachandran, Vidhisha, Feng, Shangbin, Ilgen, Jonathan S, Pierson, Emma, Koh, Pang Wei, & Tsvetkov, Yulia.
Mediq: Question-asking llms and a benchmark for reliable interactive clinical reasoning. In The Thirty-eighth Annual Conference
on Neural Information Processing Systems, (2024).

 24.  Pfohl, Stephen R., Cole-Lewis, Heather, Sayres, Rory, Neal, Darlene, Asiedu, Mercy, Dieng, Awa, Tomasev, Nenad, Rashid, Qazi
Mamunur, Azizi, Shekoofeh, Rostamzadeh, Negar, et al. A toolbox for surfacing health equity harms and biases in large language
models. Nature Medicine, pages 1–11, (2024).

 25.  Griot, Maxime, Hemptinne, Coralie, Vanderdonckt, Jean & Yuksel, Demet. Large language models lack essential metacognition for

reliable medical reasoning. Nat. Commun. 16(1), 642 (2025).

 26.  Luchins, Abraham S. Mechanization in problem solving: The effect of einstellung. Psychological monographs, 54(6), i, (1942).
 27.  Bilalić, Merim, McLeod, Peter & Gobet, Fernand. The mechanism of the einstellung (set) effect: A pervasive source of cognitive

bias. Curr. Dir. Psychol. Sci. 19(2), 111–115 (2010).

 28.  Hendrycks, Dan, Burns, Collin, Basart, Steven, Zou, Andy, Mazeika, Mantas, Song, Dawn, & Steinhardt, Jacob. Measuring massive

multitask language understanding. arXiv preprint arXiv:2009.03300, (2020).

 29.  Wang, Yubo, Ma, Xueguang, Zhang, Ge, Ni, Yuansheng, Chandra, Abhranil, Guo, Shiguang, Ren, Weiming, Arulraj, Aaran, He,
Xuan, Jiang, Ziyan, et al. Mmlu-pro: A more robust and challenging multi-task language understanding benchmark. arXiv preprint
arXiv:2406.01574, (2024).

 30.  Hurst, Aaron, Lerer, Adam, Goucher, Adam P., Perelman, Adam, Ramesh, Aditya, Clark, Aidan, Ostrow, AJ, Welihinda, Akila,

Hayes, Alan, Radford, Alec, et al. Gpt-4o system card. arXiv preprint arXiv:2410.21276, (2024).

 31.  Jaech, Aaron, Kalai, Adam, Lerer, Adam, Richardson, Adam, El-Kishky, Ahmed, Low, Aiden, Helyar, Alec, Madry, Aleksander,

Beutel, Alex, Carney, Alex, et al. Openai o1 system card. arXiv preprint arXiv:2412.16720, (2024).

 32.  Han, Tianyu, Adams, Lisa C, Papaioannou, Jens-Michalis, Grundmann, Paul, Oberhauser, Tom, Löser, Alexander, Truhn, Daniel,
& Bressem, Keno K. Medalpaca–an open-source collection of medical conversational ai models and training data. arXiv preprint
arXiv:2304.08247, (2023).

 33.  Chen, Zeming, Cano, Alejandro Hernández, Romanou, Angelika, Bonnet, Antoine, Matoba, Kyle, Salvi, Francesco, Pagliardini,
Matteo, Fan, Simin, Köpf, Andreas, Mohtashami, Amirkeivan, et al. Meditron-70b: Scaling medical pretraining for large language
models. arXiv preprint arXiv:2311.16079, (2023).

 34.  Anthropic. The claude 3 model family: Opus, sonnet, haiku.  h t t p s :   /  / w w w c d  n . a n t h r o p i   c . c  o m  / d e 8 b a  9 b 0 1 c 9  a b 7 c b  a b f 5 c 3 3 b 8 0 b 7 b b c

6 1 8 8 5 7 6  2 7 / M o d e l   C a r d   C l a u d e   3 . p d f, 2024. Accessed: 2025-01-22.

 35.  Team, Gemini, Anil, Rohan, Borgeaud, Sebastian, Alayrac, Jean-Baptiste, Yu, Jiahui, Soricut, Radu, Schalkwyk, Johan, Dai, Andrew
M, Hauth, Anja, Millican, Katie, et al. Gemini: a family of highly capable multimodal models. arXiv preprint arXiv:2312.11805,
(2023).

 36.  Jiang, Albert Q, Sablayrolles, Alexandre, Mensch, Arthur, Bamford, Chris, Chaplot, Devendra Singh, de las Casas, Diego, Bressand,

Florian, Lengyel, Gianna, Lample, Guillaume, Saulnier, Lucile, et al. Mistral 7b. arXiv preprint arXiv:2310.06825, (2023).

 37.  Manakul, Potsawee, Liusie, Adian, Gales, Mark JF. Selfcheckgpt: Zero-resource black-box hallucination detection for generative

large language models. arXiv preprint arXiv:2303.08896, (2023).

 38.  Xiong,  Miao,  Hu,  Zhiyuan,  Lu,  Xinyang,  Li,  Yifei,  Fu,  Jie,  He,  Junxian,  Hooi,  Bryan.  Can  llms  express  their  uncertainty?  an

empirical evaluation of confidence elicitation in llms. arXiv preprint arXiv:2306.13063, (2023).

 39.  Wang, Xuezhi, Wei, Jason, Schuurmans, Dale, Le, Quoc, Chi, Ed, Narang, Sharan, Chowdhery, Aakanksha, & Zhou, Denny. Self-

consistency improves chain of thought reasoning in language models. arXiv preprint arXiv:2203.11171, (2022).

 40.  Lyu,  Qing,  Shridhar,  Kumar,  Malaviya,  Chaitanya,  Zhang,  Li,  Elazar,  Yanai,  Tandon,  Niket,  Apidianaki,  Marianna,  Sachan,
Mrinmaya, & Callison-Burch, Chris. Calibrating large language models with sample consistency. arXiv preprint arXiv:2402.13904,
(2024).

 41.  Savage, Thomas,  Wang,  John,  Gallo,  Robert,  Boukil,  Abdessalem,  Patel,  Vishwesh,  Amir  Ahmad  Safavi-Naini,  Seyed,  Soroush,
Ali, & Chen, Jonathan H. Large language model uncertainty proxies: discrimination and calibration for medical diagnosis and
treatment. Journal of the American Medical Informatics Association, 32 (1): 139–149, (2025).

Scientific Reports |        (2025) 15:39426

| https://doi.org/10.1038/s41598-025-22940-0

10

www.nature.com/scientificreports/

 42.  Gao, Yifei, Ou, Jie, Wang, Lei, Xiao, Yuting, Xiang, Zhiyuan, Dai, Ruiting, & Cheng, Jun. Compensate quantization errors: Make

weights hierarchical to compensate each other. arXiv preprint arXiv:2406.16299, (2024).

 43.  Ji, Ziwei et al. Survey of hallucination in natural language generation. ACM Comput. Surv. 55(12), 1–38 (2023).
 44.  Kim,  Sunnie  SY,  Liao,  Q  Vera,  Vorvoreanu,  Mihaela,  Ballard,  Stephanie,  &  Vaughan,  Jennifer  Wortman.  “  i’m  not  sure,  but...”:
Examining the impact of large language models’ uncertainty expression on user reliance and trust. In The 2024 ACM Conference
on Fairness, Accountability, and Transparency, pages 822–835, (2024).

 45.  Rawte, Vipula, Sheth, Amit, & Das, Amitava. A survey of hallucination in large foundation models. arXiv preprint arXiv:2309.05922,

(2023).

 46.  Bowyer,  Sam,  Aitchison,  Laurence,  &  Ivanova,  Desi  R.  Position:  Don’t  use  the  clt  in  llm  evals  with  fewer  than  a  few  hundred

datapoints. arXiv preprint arXiv:2503.01747, (2025).

 47.  Brown, Lawrence D., Cai, T Tony & DasGupta, Anirban. Interval estimation for a binomial proportion. Stat. Sci. 16(2), 101–133

(2001).

 48.  Hassabis,  Demis,  Kumaran,  Dharshan,  Summerfield,  Christopher  &  Botvinick,  Matthew.  Neuroscience-inspired  artificial

intelligence. Neuron 95(2), 245–258 (2017).

 49.  Zador, Anthony et al. Catalyzing next-generation artificial intelligence through neuroai. Nat. Commun. 14(1), 1597 (2023).
 50.  Kumar, Sreejan et al. Shared functional specialization in transformer-based language models and the human brain. Nat. Commun.

15(1), 5523 (2024).

 51.  Echterhoff, Jessica, Liu, Yao, Alessa, Abeer, McAuley, Julian & He, Zexue. Cognitive bias in decision-making with llms. In Findings

of the Association for Computational Linguistics: EMNLP 2024, 12640–12653 (2024).

 52.  Liu, Xuan, Zhang, Jie, Guo, Song, Shang, Haoyang, Yang, Chengxu, & Zhu, Quanyan. Exploring prosocial irrationality for llm

agents: A social cognition view. arXiv preprint arXiv:2405.14744, (2024).

 53.  Naeini, Saeid, Saqur, Raeid, Saeidi, Mozhgan, Giorgi, John, & Taati, Babak. Large language models are fixated by red herrings:
Exploring creative problem solving and einstellung effect using the only connect wall dataset. arXiv preprint arXiv:2306.11167,
(2023).

 54.  McCoy, R Thomas, Yao, Shunyu, Friedman, Dan, Hardy, Matthew, & Griffiths, Thomas L. Embers of autoregression: Understanding

large language models through the problem they are trained to solve. arXiv preprint arXiv:2309.13638, (2023).

 55.  Goetz, Lea, Seedat, Nabeel, Vandersluis, Robert & van der Schaar, Mihaela. Generalization—a key challenge for responsible ai in

patient-facing clinical applications. npj Digital Medicine 7(1), 126 (2024).

 56.  Moskvichev, Arseny, Odouard, Victor Vikram, & Mitchell, Melanie. The conceptarc benchmark: Evaluating understanding and

generalization in the arc domain. arXiv preprint arXiv:2305.07141, (2023).

 57.  Dong,  Yihong,  Jiang,  Xue,  Liu,  Huanyu,  Jin,  Zhi,  Gu,  Bin,  Yang,  Mengfei,  &  Li,  Ge.  Generalization  or  memorization:  Data

contamination and trustworthy evaluation for large language models. arXiv preprint arXiv:2402.15938, (2024).

 58.  Yu,  Qifan,  Li,  Juncheng,  Wei,  Longhui,  Pang,  Liang,  Ye,  Wentao,  Qin,  Bosheng,  Tang,  Siliang,  Tian,  Qi,  &  Zhuang,  Yueting.
Hallucidoctor: Mitigating hallucinatory toxicity in visual instruction data. In Proceedings of the IEEE/CVF Conference on Computer
Vision and Pattern Recognition, pages 12944–12953, (2024).

 59.  Zhang, Honghua, Li, Liunian Harold, Meng, Tao, Chang, Kai-Wei , & Van den Broeck, Guy. On the paradox of learning to reason

from data. arXiv preprint arXiv:2205.11502, (2022).

 60.  Kandpal, Nikhil, Deng, Haikang, Roberts, Adam, Wallace, Eric, & Raffel, Colin. Large language models struggle to learn long-tail

knowledge. In International Conference on Machine Learning, pages 15696–15707. PMLR, (2023).

 61.  Guan, Lin, Valmeekam, Karthik, Sreedharan, Sarath & Kambhampati, Subbarao. Leveraging pre-trained large language models to

construct and utilize world models for model-based task planning. Adv. Neural. Inf. Process. Syst. 36, 79081–79094 (2023).

 62.  Stechly, Kaya, Valmeekam, Karthik, & Kambhampati, Subbarao. Chain of thoughtlessness: An analysis of cot in planning. arXiv

preprint arXiv:2405.04776, (2024).

 63.  Chollet,  Francois,  Knoop,  Mike,  Kamradt,  Gregory,  &  Landers,  Bryan.  Arc  prize  2024:  Technical  report.  arXiv  preprint

arXiv:2412.04604, (2024).

 64.  Arkoudas, Konstantine. Gpt-4 can’t reason. arXiv preprint arXiv:2308.03762, (2023).
 65.  Mirzadeh,  Iman,  Alizadeh,  Keivan,  Shahrokhi,  Hooman,  Tuzel,  Oncel,  Bengio,  Samy,  &  Farajtabar,  Mehrdad.  Gsm-symbolic:
Understanding the limitations of mathematical reasoning in large language models. arXiv preprint arXiv:2410.05229, (2024).
 66.  Durning, Steven J. et al. Functional neuroimaging correlates of thinking flexibility and knowledge structure in memory: Exploring

the relationships between clinical reasoning and diagnostic thinking. Med. Teach. 38(6), 570–577 (2016).

 67.  Huang, Shulin, Yang, Linyi, Song, Yan, Chen, Shuang, Cui, Leyang, Wan, Ziyu, Zeng, Ying Wen, Qingcheng, Shao, Kun, Zhang,
Weinan, et al. Thinkbench: Dynamic out-of-distribution evaluation for robust llm reasoning.  arXiv preprint arXiv:2502.16268,
(2025).

 68.  Chen, Xuanzhong, Mao, Xiaohao, Guo, Qihan, Wang, Lun, Zhang, Shuyang, & Chen, Ting. Rarebench: can llms serve as rare
diseases specialists? In Proceedings of the 30th ACM SIGKDD conference on knowledge discovery and data mining, pages 4850–4861,
(2024).

 69.  Blech, Christine, Gaschler, Robert & Bilalić, Merim. Why do people fail to see simple solutions? using think-aloud protocols to

uncover the mechanism behind the einstellung (mental set) effect. Thinking & Reasoning 26(4), 552–580 (2020).

 70.  McCrary, Hilary C., Colbert-Getz, Jorie M., Poss, W Bradley & Smith, Brigitte K. A systematic review of the relationship between

in-training examination scores and specialty board examination scores. J. Grad. Med. Educ. 13(1), 43–57 (2021).

Author contributions
D.B. and K.S. wrote the main manuscript. F.L. and A.A. edited the manuscript. A.P. and J.W. contributed to data
collection and analysis. All authors reviewed the manuscript.

Declarations

Competing interests
The authors declare no competing interests.

Additional information
Supplementary Information The online version contains supplementary material available at  h t t p s : / / d o i . o r g / 1
0 . 1 0 3 8 / s 4 1 5 9 8 - 0 2 5 - 2 2 9 4 0 - 0     .

Correspondence and requests for materials should be addressed to D.B.

Reprints and permissions information is available at www.nature.com/reprints.

Scientific Reports |        (2025) 15:39426

| https://doi.org/10.1038/s41598-025-22940-0

11

www.nature.com/scientificreports/

Publisher’s note  Springer Nature remains neutral with regard to jurisdictional claims in published maps and
institutional affiliations.

Open Access   This article is licensed under a Creative Commons Attribution 4.0 International License, which
permits use, sharing, adaptation, distribution and reproduction in any medium or format, as long as you give
appropriate credit to the original author(s) and the source, provide a link to the Creative Commons licence, and
indicate if changes were made. The images or other third party material in this article are included in the article’s
Creative Commons licence, unless indicated otherwise in a credit line to the material. If material is not included
in  the  article’s  Creative  Commons  licence  and  your  intended  use  is  not  permitted  by  statutory  regulation  or
exceeds the permitted use, you will need to obtain permission directly from the copyright holder. To view a copy
of this licence, visit http://creativecommons.org/licenses/by/4.0/.

© The Author(s) 2025

Scientific Reports |        (2025) 15:39426

| https://doi.org/10.1038/s41598-025-22940-0

12

