|     |           |     |                                      |               | Trusting  |       | Your Evidence:  |     |             |            |     |     |     |
| --- | --------- | --- | ------------------------------------ | ------------- | --------- | ----- | --------------- | --- | ----------- | ---------- | --- | --- | --- |
|     |           |     | Hallucinate                          |               | Less      | with  | Context-aware   |     | Decoding    |            |     |     |     |
|     |           |     |                                      | WeijiaShi     |           | 1,2 ∗ | XiaochuangHan   |     |             | 1,2 ∗      |     |     |     |
|     |           |     | 2                                    |               |           |       | 1               |     | 1,2         |            |     | 2   |     |
|     | MikeLewis |     |                                      | YuliaTsvetkov |           |       | LukeZettlemoyer |     |             | Wen-tauYih |     |     |     |
|     |           |     | 1 UniversityofWashington,Seattle,WA, |               |           |       |                 |     | 2 FAIR,Meta |            |     |     |     |
|     |           |     |                                      |               | {swj0419, |       | xhan77}@uw.edu  |     |             |            |     |     |     |
Abstract
Languagemodels(LMs)oftenstruggletopay
enoughattentiontotheinputcontext,andgen-
eratetextsthatareunfaithfulorcontainhallu-
| cinations. |     | To mitigate |     | this issue, | we  | present |     |     |     |     |     |     |     |
| ---------- | --- | ----------- | --- | ----------- | --- | ------- | --- | --- | --- | --- | --- | --- | --- |
context-awaredecoding(CAD),whichfollows
acontrastiveoutputdistributionthatamplifies
| the      | difference | between         |           | the output    | probabili- |         |          |                                        |     |     |     |     |     |
| -------- | ---------- | --------------- | --------- | ------------- | ---------- | ------- | -------- | -------------------------------------- | --- | --- | --- | --- | --- |
| ties     | when       | a model         | is used   | with          | and        | without |          |                                        |     |     |     |     |     |
| context. |            | Our experiments |           | show          | that       | CAD,    |          |                                        |     |     |     |     |     |
|          |            |                 |           |               |            |         | Figure1: | Anillustrationofcontext-awaredecoding. |     |     |     |     |     |
| without  | additional |                 | training, | significantly |            | im-     |          |                                        |     |     |     |     |     |
| proves   | the        | faithfulness    |           | of different  | LM         | fami-   |          |                                        |     |     |     |     |     |
lies,includingOPT,GPT,LLaMAandFLAN- ument. Insufficient attention to context is espe-
|     |     |     |     |     |     |     | cially problematic |     |     | when | the context | knowledge |     |
| --- | --- | --- | --- | --- | --- | --- | ------------------ | --- | --- | ---- | ----------- | --------- | --- |
T5forsummarizationtasks(e.g.,14.3%gain
for LLaMA in factuality metrics). Further- contradicts with the prior knowledge (Longpre
| more, | CAD | is particularly |     | effective |     | in over- |                             |     |     |     |                  |     |     |
| ----- | --- | --------------- | --- | --------- | --- | -------- | --------------------------- | --- | --- | --- | ---------------- | --- | --- |
|       |     |                 |     |           |     |          | etal.,2021;Zhouetal.,2023). |     |     |     | Forinstance,when |     |     |
ridingamodel’spriorknowledgewhenitcon-
LLaMA(Touvronetal.,2023)ispresentedwitha
| tradicts | the | provided | context, |     | leading | to sub- |                 |     |            |     |     |          |       |
| -------- | --- | -------- | -------- | --- | ------- | ------- | --------------- | --- | ---------- | --- | --- | -------- | ----- |
|          |     |          |          |     |         |         | latest document |     | “Argentina |     | won | the FIFA | World |
stantialimprovementsintaskswhereresolving
|                                  |     |     |     |     |         |     | Cups in | 1978, | 1986 | and | 2022 ...” | in  | its context |
| -------------------------------- | --- | --- | --- | --- | ------- | --- | ------- | ----- | ---- | --- | --------- | --- | ----------- |
| theknowledgeconflictisessential. |     |     |     |     | Ourcode |     |         |       |      |     |           |     |             |
ispubliclyreleasedathttps://github.com/ (Figure1),itstillpredicts“Two”inresponsetothe
question“HowmanyWorldCupshaveArgentina
xhan77/context-aware-decoding.
won?”,dueinparttotheoutdatedtrainingdata.
| 1 Introduction |     |     |     |     |     |     | Inthiswork,wepresentasimplecontext-aware |     |     |     |     |     |     |
| -------------- | --- | --- | --- | --- | --- | --- | ---------------------------------------- | --- | --- | --- | --- | --- | --- |
decoding(CAD)methodtoencouragetheLMto
Languagemodels(LMs)areeffectiveingenerating
|     |     |     |     |     |     |     | attendtoitscontextduringgeneration. |     |     |     |     |     | Asshown |
| --- | --- | --- | --- | --- | --- | --- | ----------------------------------- | --- | --- | --- | --- | --- | ------- |
fluentcontinuationsofapromptordocumentpre-
inFigure1,CADsamplesfromanewoutputdis-
fix. Duringgeneration,theyrelyontwosourcesof
tribution,whichamplifiesthedifferencebetween
| knowledge: | (1)priorknowledge,whichislearned |     |     |     |     |     |        |               |     |      |             |     |         |
| ---------- | -------------------------------- | --- | --- | --- | --- | --- | ------ | ------------- | --- | ---- | ----------- | --- | ------- |
|            |                                  |     |     |     |     |     | output | probabilities |     | with | and without | the | context |
duringpretrainingandstoredimplicitlywithinthe
|     |     |     |     |     |     |     | document. | Thisprovidesanewformofcontrastive |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --------- | --------------------------------- | --- | --- | --- | --- | --- |
modelparameters;(2)contextknowledge,whichis
decoding(Lietal.,2023),whicheffectivelydown-
passedasinputsintheprefixcontext(Chanetal.,
|     |     |     |     |     |     |     | weights | theprior | knowledge |     | whenmore |     | relevant |
| --- | --- | --- | --- | --- | --- | --- | ------- | -------- | --------- | --- | -------- | --- | -------- |
2022). However,itremainsanopenquestionhow
|     |     |     |     |     |     |     | contextual | information |     | is  | provided. | CAD | can be |
| --- | --- | --- | --- | --- | --- | --- | ---------- | ----------- | --- | --- | --------- | --- | ------ |
apretrainedLM,particularlyavanillaLMwithout
usedwithoff-the-shelfpretrainedlanguagemodels
task-specificfinetuning,balancesthesetwoknowl-
withoutanyadditionaltraining.
edgesourcesduringgeneration.
Experimentalresultsfromsummarizationtasks
PreviousresearchshowsthatLMscanfailtopay
|          |                  |            |     |             |          |            | show that     | context-aware |            |        | decoding     | significantly |            |
| -------- | ---------------- | ---------- | --- | ----------- | -------- | ---------- | ------------- | ------------- | ---------- | ------ | ------------ | ------------- | ---------- |
| enough   | attention        | to         | new | information |          | introduced |               |               |            |        |              |               |            |
|          |                  |            |     |             |          |            | enhances      | the           | generation |        | faithfulness |               | of vanilla |
| in the   | context          | knowledge. |     | This        | can lead | to hallu-  |               |               |            |        |              |               |            |
|          |                  |            |     |             |          |            | LMs including |               | OPT        | (Zhang | et           | al., 2022),   | GPT-       |
| cination | in summarization |            |     | (Maynez     | et       | al., 2020; |               |               |            |        |              |               |            |
Neo(Blacketal.,2021),LLaMA(Touvronetal.,
| Pagnoni | et al., | 2021), | where | the     | generated | sum-  |                        |                           |     |     |                     |     |         |
| ------- | ------- | ------ | ----- | ------- | --------- | ----- | ---------------------- | ------------------------- | --- | --- | ------------------- | --- | ------- |
|         |         |        |       |         |           |       | 2023)                  | and instruction-finetuned |     |     |                     | LMs | such as |
| maries  | include | facts  | not   | present | in the    | input | doc-                   |                           |     |     |                     |     |         |
|         |         |        |       |         |           |       | FLAN(Chungetal.,2022). |                           |     |     | Forinstance,whenap- |     |         |
∗Equalcontribution.Orderrandomlydetermined.
pliedtoLLaMA-30BinCNN-DM,CADleadsto
783
Proceedingsofthe2024ConferenceoftheNorthAmericanChapteroftheAssociationforComputationalLinguistics:
HumanLanguageTechnologies(Volume2:ShortPapers),pages783–791
June16-21,2024©2024AssociationforComputationalLinguistics

substantialimprovementinbothROUGE-L(21%) wheretheoutputprobabilityisaproduct-of-experts
andfactualityevaluationmetrics(14.3%). Moreno- oftheoriginaloutputprobabilityandPMIweighted
tably,CADisespeciallybeneficialforknowledge byα. Essentially,outputsthatbecomemuchmore
conflictingtasks,wherethecontextcontainsinfor- likely when the context is included are preferred
| mation | contradictory |     | to the | model’s | prior | knowl- | (Figure1). |     |     |     |     |     |     |
| ------ | ------------- | --- | ------ | ------- | ----- | ------ | ---------- | --- | --- | --- | --- | --- | --- |
edge. CADbringsa2.9ximprovementtoLLaMA- Thisexpressionisnotavalidprobabilitydistribu-
30BonaknowledgeconflictsQAdataset(Longpre tionandneedstobenormalizedacrossallpossible
et al., 2021). Furthermore, we observe that this valuesofy . Byrearrangingtheterms,weobtain
t
gainbroughtbyCADincreasesasthemodelsize
thefinalform:
| growsinknowledgeconflictstasks. |     |     |     |     | Theseresults |     |       |         |     |       |     |         |     |
| ------------------------------- | --- | --- | --- | --- | ------------ | --- | ----- | ------- | --- | ----- | --- | ------- | --- |
|                                 |     |     |     |     |              |     | y t ∼ | softmax | 1+α | logit | y   | t c,x,y | <t  |
θ
demonstratethepotentialofCADinmitigatinghal-
|                                               |     |     |     |     |     |     |        | −αlogit |      | y      | x,y |                |     |
| --------------------------------------------- | --- | --- | --- | --- | --- | --- | ------ | ------- | ---- | ------ | --- | -------------- | --- |
|                                               |     |     |     |     |     |     |        |         |      | θ t    |     | <t             |     |
| lucinationsintextgenerationandoverridingprior |     |     |     |     |     |     |        |         | [(   | )      | (   | ∣              | )   |
|                                               |     |     |     |     |     |     | Larger | α means | more | weight | on  | our adjustment |     |
knowledgewithreliableandtrustedinformation.
1
|     |     |     |     |     |     |     | (α = 0 | reduces | to regu(lar∣decodin)g]). |     |     | We  | refer |
| --- | --- | --- | --- | --- | --- | --- | ------ | ------- | ------------------------ | --- | --- | --- | ----- |
tothissimplemethodascontext-awaredecoding.
2 Method
|     |            |     |     |     |     |     | From the                                     | adjusted | output | distribution |     | p˜, | we can |
| --- | ---------- | --- | --- | --- | --- | --- | -------------------------------------------- | -------- | ------ | ------------ | --- | --- | ------ |
| 2.1 | Background |     |     |     |     |     | applyvarioussamplingstrategies,suchasnucleus |          |        |              |     |     |        |
Given a LM θ, an input query x, and a context c sampling(Holtzmanetal.,2020).
Essentially,context-awaredecodingisjustacon-
thatcontainssomeexternalknowledgeunfamiliar
orinconflict tothemodel’spriorknowledge, we trastive ensemble between the logits of p y
θ t
askourmodelθ togeneratearesponsey giventhe c,x,y and p y x,y . A similar con-
|     |     |     |     |     |     |     | <t  |     | θ t |     | <t  |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
thequeryandcontext. Theresponsecanbedirectly trastive objective is universal in image ge(nera∣-
|     |     |     |     |     |     |     | tion, wh)ere | classi(fier-∣free |     |     | diff)usion | models | (Ho |
| --- | --- | --- | --- | --- | --- | --- | ------------ | ----------------- | --- | --- | ---------- | ------ | --- |
sampled(autoregressively)fromtheprobabilitydis-
tributionconditionedonqueryxandcontextc: and Salimans, 2022) predict diffusion noise with
|     | y   | p y      | c,x,y |         |     |     | 1+α ϵ     | θ x,c                              | −αϵ θ      | x ,withcbeingacontrolto |      |          |       |
| --- | --- | -------- | ----- | ------- | --- | --- | --------- | ---------------------------------- | ---------- | ----------------------- | ---- | -------- | ----- |
|     | t ∼ | θ        | t     | <t      |     |     |           |                                    |            |                         |      |          |       |
|     |     |          |       |         |     |     | theimage. | Intextgeneration,Malkinetal.(2022) |            |                         |      |          |       |
|     | ∝   | explogit | y     | t c,x,y | <t  |     |           |                                    |            |                         |      |          |       |
|     |     |          | θ     |         |     |     | (propos)e | c(oher)ence                        | b(oos)ting |                         | with | the same | intu- |
|     |     | (        | ∣     | )       |     |     |           |                                    |            |                         |      |          |       |
However,incaseswherethecontextccontains
ition,withafocusoncontrastingthefullinputand
knowledgethatisout-of(-dis∣tributionw)ithrespect
|                |                |         |      |            |               |          | a short    | premise-free |          | input,    | promoting | coherence |          |
| -------------- | -------------- | ------- | ---- | ---------- | ------------- | -------- | ---------- | ------------ | -------- | --------- | --------- | --------- | -------- |
| to θ,          | we hypothesize |         | that | the model  | can           | struggle |            |              |          |           |           |           |          |
|                |                |         |      |            |               |          | w.r.t. the | long         | context. | Instead   | of        | using     | a single |
| to effectively |                | attend  | to c | and overly | rely          | on the   |            |              |          |           |           |           |          |
|                |                |         |      |            |               |          | model θ    | in this      | work,    | different | models    |           | can also |
| prior          | knowledge      | encoded |      | in θ.      | For instance, | as       |            |              |          |           |           |           |          |
beusedinthedistributionadjustmentstodemote
| illustrated | in  | Figure | 1, when | the | context | c states |     |     |     |     |     |     |     |
| ----------- | --- | ------ | ------- | --- | ------- | -------- | --- | --- | --- | --- | --- | --- | --- |
unwantedmodelbehaviorsordistillexpertmodel’s
“ArgentinawontheFIFAWorldCupsin1978,1986
|     |     |     |     |     |     |     | capability | (Liu | et al., | 2021; | Li et | al., 2023). | We  |
| --- | --- | --- | --- | --- | --- | --- | ---------- | ---- | ------- | ----- | ----- | ----------- | --- |
and2022...”,itcontradictstheLM’soutdatedprior
furtherdiscussrelatedworksin§6and§A.2.
knowledgethatArgentinahaswontheWorldCup
| twice. | The language |     | model | may | still incorrectly |     |     |     |     |     |     |     |     |
| ------ | ------------ | --- | ----- | --- | ----------------- | --- | --- | --- | --- | --- | --- | --- | --- |
3 ExperimentalSetup
predict“Two”evenwhenpresentedwiththecon-
WeperformevaluationontasksthatrequireLMsto
textcandthequeryx.
readandreasonovercontextsandproduceoutputs
2.2 Context-awareDecoding
|             |      |         |     |           |     |           | that are    | faithful | to the     | contexts. |     | Following   | prior |
| ----------- | ---- | ------- | --- | --------- | --- | --------- | ----------- | -------- | ---------- | --------- | --- | ----------- | ----- |
|             |      |         |     |           |     |           | work (Zhang | et       | al., 2024; | Zhou      | et  | al., 2023), | we    |
| To mitigate | such | issues, |     | we factor | out | the prior |             |          |            |           |     |             |       |
knowledge from the model’s original output dis- evaluatethemodelsusingprompting.
| tribution | contrastively. |     | Here, | we  | model | the prior |     |     |     |     |     |     |     |
| --------- | -------------- | --- | ----- | --- | ----- | --------- | --- | --- | --- | --- | --- | --- | --- |
3.1 DatasetsandMetrics
| knowledge | as  | p y |     | x,y | and adjust | the |               |     |                           |     |     |     |     |
| --------- | --- | --- | --- | --- | ---------- | --- | ------------- | --- | ------------------------- | --- | --- | --- | --- |
|           |     | θ   | t   | <t  |            |     |               |     |                           |     |     |     |     |
|           |     |     |     |     |            |     | Summarization |     | Weconductsummarizationex- |     |     |     |     |
model’soriginaloutputprobabilitydistributionus-
ing the pointwise(mutu∣al inform) ation (PMI) be- periments on CNN-DM (See et al., 2017) and
tween the context c and the generation y , condi- XSUM (Narayan et al., 2018). We use ROUGE-
t
|             |     |                       |     |     |     |     | L (Lin, | 2004) | to evaluate | summarization |     |     | quality. |
| ----------- | --- | --------------------- | --- | --- | --- | --- | ------- | ----- | ----------- | ------------- | --- | --- | -------- |
| tionedonx,y |     | <t . Formally,wehave: |     |     |     |     |         |       |             |               |     |     |          |
y ∼ p˜ y c,x,y 1Ifweidentifyanexternalknowledgecconditionallyin-
| t   | θ t |     | <t  |     |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
α
p y c ,x ,y de p e n de n t to t h e g e n e r ati on , p y c , x , y = p y
|     |     |     |     | θ t |     | <t  |     |     |     | θ   | t   | <t  | θ t |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
∝ p θ y (t c,x,y <t x , y , e ve n a n o n - ze r o α w o u ld n oth a v e a n imp ac t to t he
|     |     | ∣   | )   | p y | x ,y |     | < t                         |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | ---- | --- | --------------------------- | --- | --- | --- | --- | --- | --- |
|     |     |     |     | θ t | <t   |     | originaloutputdistribution. |     |     |     |     |     |     |
|     |     |     |     |     |      |     |                             |     |     | (   | ∣   | )   | ( ∣ |
|     |     |     |     | ( ∣ |      | )   |                             |     |     |     |     |     |     |
|     | ( ∣ |     | )(  |     |      | )   | )                           |     |     |     |     |     |     |
784
|     |     |     |     | (   | ∣   | )   |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |

Tomeasurethefactualconsistencyofsummaries, XSUM
weadoptstate-of-the-artfactualityevaluationmet-
c Article: Prison LinkCymru had 1,099referrals in
rics: BERT-Precision (Pagnoni et al., 2021) and 2015-16 and said some ex-offenders were living
roughforuptoayearbeforefindingsuitableaccom-
FactKB(Fengetal.,2023),whichhasbeendemon-
modation...
strated to achieve high correlations with human x Summarizethearticleinonesentence.Summary:
judgment on the summarization datasets, outper-
NQ-SWAP
formingothermetricssuchasFACTCC(Kryscin-
c TeslaCEOElonMuskisnowinchargeofTwitter,
skietal.,2020)andSUMMAC(Labanetal.,2022).
CNBChaslearned...
x WhoisTwitterCEOnow?
KnowledgeConflicts Weevaluateperformance MemoTrap
on two knowledge conflict datasets: MemoTrap
c Writeaquotethatendsintheword"early":
(LiuandLiu,2023)andNQ-Swap(Longpreetal., x Betterlatethan
2021). MemoTrapiscreatedtoinvestigatewhether
language models fall into memorization traps. It Table1: AnillustationoftheinputstoCADappliedto
eachdataset. CADupweightsthecontextc(inred)by
comprises instructions that prompt the language
samplingeachtokenfromsoftmax 1+α logit y
modeltocompleteawell-knownproverbwithan θ t
c,x,y −αlogit y x,y .
endingwordthatdeviatesfromthecommonlyused
<t θ t <t
[( ) ( ∣
ending (e.g., Write a quote that ends in the word
tive in t)he knowled(ge∣conflic)t]setting, where the
“early”: Betterlatethan ). NQ-Swapisbasedon
priorknowledgeneedstobefactoredoutmore. We
aQAdataset,naturalquestions(NQ)(Kwiatkowski
investigatetheeffectofαinSection5.
etal.,2019),wheretheobjectiveistoanswerques-
For the baselines, we use the regular decod-
tionsbasedonagolddocument. TogenerateNQ-
ingmethodsfollowingpriorwork(Longpreetal.,
Swap,Longpreetal.(2021)identifyquestionsin
2021; Kwiatkowski et al., 2019): greedy decod-
NQwithnamedentityanswers,findthesupportive
ing for knowledge conflict tasks and top-p sam-
document for each question and replace the gold
pling with p=0.9 for summarization tasks (Holtz-
answerentityinthedocumentwitharandomentity.
man et al., 2020). For CAD, we use the same
AfaithfulLMshouldgeneratethereplacedentity
sampling strategies on top of the adjusted output
as the answer when given the question and mod-
probabilitydistribution.
ified document. We also include the original NQ
datasetwiththequestionandoriginaldocumentfor 4 Results
evaluation. WeuseExactMatch(EM)astheevalu-
Summarization Table 2 reports the results on
ationmetricforNQ-Swap,NQandMemoTrap.
CNN-DM and XSUM. We observe that CAD
InTable1,weshowillustrativeexamplesofthe
outperforms the standard decoding algorithm by
contextsweaimtoupweightforthemodelandthe
a large margin in all eight models across both
queriesacrossdifferentdatasets. WehopeLMspay
datasets. Specifically, when applied to LLaMA-
moreattentiontothesourcedocumentinXSUM
30BinCNN-DM,CADleadsto21%increasein
andNQ-Swap. Ontheotherhand, wehopeLMs
ROUGE-L, 14.3% increase in factKB and 7.8%
focusmoreontheinstructioninMemoTrap.
increaseinBERT-P.Thisresultdemonstratesthat
3.2 ModelsandBaselines CADcouldeffectivelyimprovethequalityandfac-
tualityofthegeneratedsummariesfromadiverse
We apply CAD to pretrained language models
setoflanguagemodels.
including OPT (Zhang et al., 2022), GPT-Neo
(Blacketal.,2021),LLaMA(Touvronetal.,2023) KnowledgeConflicts Ourresultsfortheknowl-
andinstruction-finetunedLMssuchasFLAN-T5 edgeconflictdatasets,NQ-SWAPandMemoTrap,
(Chungetal.,2022). aswellastheoriginalNQaredetailedinTable3.
CADintroducesahyperparameterαtocontrol CADissignificantlybetterthantheregulardecod-
theadjustmentlevel. Wesetα = 0.5forallmod- inginallsettings,withtheexceptionofaminorde-
els evaluated on the summarization datasets and creaseobservedforFLAN-T5onthenon-conflict
2
α = 1forallmodelsevaluatedontheknowledge NQdataset. Despitethis,CADachievesbetterper-
conflict datasets. We observed that α = 0.5 gen-
2Theslightdeclineinperformancecanbeattributedtothe
erallyyieldedgoodresultsacrossallsettingsand
NQdatasetbeingincludedintheinstruction-finetuningsets
all datasets, but a slightly higher α is more effec- usedbyFLAN-T5.
785

|       |          |         | CNN-DM |        |         | XSUM   |        |     |
| ----- | -------- | ------- | ------ | ------ | ------- | ------ | ------ | --- |
| Model | Decoding | ROUGE-L | factKB | BERT-P | ROUGE-L | factKB | BERT-P |     |
|       | Regular  | 22.0    | 77.8   | 86.5   | 16.4    | 47.2   | 85.2   |     |
13B
CAD
| OPT |         | 27.4 | 84.1 | 90.8 | 18.2 | 64.9 | 87.5 |     |
| --- | ------- | ---- | ---- | ---- | ---- | ---- | ---- | --- |
|     | Regular | 22.2 | 81.7 | 87.0 | 17.4 | 38.2 | 86.1 |     |
30B
CAD
|     |         | 28.4 | 87.0 | 90.2 | 19.5 | 45.6 | 89.3 |     |
| --- | ------- | ---- | ---- | ---- | ---- | ---- | ---- | --- |
|     | Regular | 24.3 | 80.5 | 87.5 | 17.6 | 54.0 | 86.6 |     |
3B
|     | CAD | 27.7 | 87.5 | 90.6 | 18.1 | 65.1 | 89.1 |     |
| --- | --- | ---- | ---- | ---- | ---- | ---- | ---- | --- |
GPT-Neo
|     | Regular | 18.7 | 68.3 | 85.2 | 14.9 | 42.2 | 85.7 |     |
| --- | ------- | ---- | ---- | ---- | ---- | ---- | ---- | --- |
20B
|     | CAD     | 24.5 | 77.5 | 89.4 | 19.0 | 63.3 | 90.6 |     |
| --- | ------- | ---- | ---- | ---- | ---- | ---- | ---- | --- |
|     | Regular | 27.1 | 80.2 | 89.5 | 19.0 | 53.5 | 87.8 |     |
13B
|     | CAD | 32.6 | 90.8 | 93.0 | 21.1 | 73.4 | 91.7 |     |
| --- | --- | ---- | ---- | ---- | ---- | ---- | ---- | --- |
LLaMA
|     | Regular | 25.8 | 76.8 | 88.5 | 18.7 | 47.7 | 87.1 |     |
| --- | ------- | ---- | ---- | ---- | ---- | ---- | ---- | --- |
30B
|     | CAD     | 31.8 | 87.8 | 92.2 | 22.0 | 66.4 | 90.3 |     |
| --- | ------- | ---- | ---- | ---- | ---- | ---- | ---- | --- |
|     | Regular | 25.5 | 90.2 | 91.6 | 18.8 | 31.9 | 88.2 |     |
3B
|     | CAD | 26.1 | 93.9 | 92.1 | 19.5 | 35.9 | 88.8 |     |
| --- | --- | ---- | ---- | ---- | ---- | ---- | ---- | --- |
FLAN
|     | Regular | 25.4 | 90.4 | 91.4 | 19.4 | 29.8 | 88.3 |     |
| --- | ------- | ---- | ---- | ---- | ---- | ---- | ---- | --- |
11B
|     | CAD | 27.1 | 93.1 | 92.2 | 20.0 | 35.0 | 88.8 |     |
| --- | --- | ---- | ---- | ---- | ---- | ---- | ---- | --- |
Table2:
CADconsistentlyoutperformtheregulardecodingmethodintermsofbothsummaryqualitymetric
(ROUGE-L)andsummaryfactuality(factKBandBERT-P).Thebestscoresforeachsettingareboldfaced.
FLAN3Band11BrefertoFLAN-T5XLandFLAN-T5XXLrespectively.
Model Decoding Memo. NQ NQ-SWAP CAD is effective in improving language models
|      |           |      | of  | different | sizes. Specifically, |     | we focus | on OPT |
| ---- | --------- | ---- | --- | --------- | -------------------- | --- | -------- | ------ |
| Reg. | 32.5 29.2 | 18.8 |     |           |                      |     |          |        |
13B
CAD 44.5 32.2 36.9 modelsacrossarangeofsizes: 125M,350M,1.3B,
OPT
| Reg. | 28.4 29.4 | 14.7 |                                           |     |     |     |     |     |
| ---- | --------- | ---- | ----------------------------------------- | --- | --- | --- | --- | --- |
| 30B  |           |      | 2.7B,6.7B,13B,30B.Weobservethattheperfor- |     |     |     |     |     |
| CAD  | 41.0 35.5 | 29.0 |                                           |     |     |     |     |     |
mancegainbroughtbyCADstaysconsistentwith
| Reg. | 22.5 31.9 | 19.1 |           |       |       |            |             |     |
| ---- | --------- | ---- | --------- | ----- | ----- | ---------- | ----------- | --- |
| 3B   |           |      | different | model | sizes | in CNN-DM. | In Memotrap |     |
| CAD  | 47.3 39.9 | 41.2 |           |       |       |            |             |     |
GPT.
Reg. 37.1 22.8 16.1 and NQ-SWAP, this gain increases as the model
20B
| CAD | 57.3 32.1 | 36.8 |     |     |     |     |     |     |
| --- | --------- | ---- | --- | --- | --- | --- | --- | --- |
sizegrows,indicatingthatlargerLMscanhavea
Reg. 23.8 22.3 11.7 greatertendencytorelyontheirpriorknowledge
13B
| CAD   | 57.1 33.6 | 36.7 |                                               |     |     |     |     |     |
| ----- | --------- | ---- | --------------------------------------------- | --- | --- | --- | --- | --- |
| LLaMA |           |      | insteadofreadingthecontexts,therebybenefiting |     |     |     |     |     |
| Reg.  | 25.8 23.8 | 9.6  |                                               |     |     |     |     |     |
30B
| CAD | 50.6 34.0 | 37.7 | morefromCAD.InFigure2,weobservethatthe |     |     |     |     |     |
| --- | --------- | ---- | -------------------------------------- | --- | --- | --- | --- | --- |
performancegainbroughtbyCADstaysconsistent
| Reg. | 69.2 81.8 | 71.4 |     |     |     |     |     |     |
| ---- | --------- | ---- | --- | --- | --- | --- | --- | --- |
3B
CAD 72.2 80.3 73.3 with different OPT model sizes in CNN-DM. In
FLAN
| Reg. | 82.0 85.5 | 73.0 |          |        |                  |            |                  |       |
| ---- | --------- | ---- | -------- | ------ | ---------------- | ---------- | ---------------- | ----- |
| 11B  |           |      | Memotrap |        | and NQ-SWAP,     | this       | gain increases   | as    |
| CAD  | 88.7 82.5 | 77.1 |          |        |                  |            |                  |       |
|      |           |      | the      | model  | size grows,      | indicating | that larger      | LMs   |
|      |           |      | can      | have a | greater tendency |            | to rely on their | prior |
Table3:CADoutperformstheregulardecodingmethod
(Reg.) inallsettingsexceptforFLAN-T5onNQ. knowledgeinsteadofreadingthecontexts,thereby
benefitingmorefromCAD.
formanceontheknowledgeconflictdatasets,e.g., Effectofadjustmentlevelα
Wetheninvestigate
CADimproveGPT-Neo20Bby54.4%onMemo- theeffectofdifferentadjustmentlevelα(asmall
trapandby128%onNQ-SWAP.Thissubstantial
αmakesthedistributionclosertotheoriginalnext
improvementsuggeststhatcontext-awaredecoding
|     |     |     | tokendistribution). |     | Weconductexperimentswith |     |     |     |
| --- | --- | --- | ------------------- | --- | ------------------------ | --- | --- | --- |
isparticularlybeneficialforLMstoadheretothe variousvaluesofαandpresenttheresultsinFig-
givencontext,inscenarioswherethemodel’sprior
|     |     |     | ure | 3. Across | all three | datasets, | we find | α = 0.5 |
| --- | --- | --- | --- | --------- | --------- | --------- | ------- | ------- |
knowledgecontradictswiththecontextknowledge.
consistentlyproviderobustimprovementsoverreg-
ulardecoding.
5 Analysis
6 RelatedWork
CAD brings consistent improvement to LMs Summarizationfactuality Summarizationmod-
withdifferentsizes. InTables2and3,weshow elshaveshownatendencytogeneratehallucinated
thatCADcouldbeusedtoenhanceadiversesetof texts (Maynez et al., 2020; Pagnoni et al., 2021).
LMfamilies, includingOPT,GPT-Neo, LLaMA, Thishasledtogrowingeffortstoimprovethefac-
and FLAN-T5. We further investigate whether tualconsistency, includingapplyingattentionsto
786

Figure2: OPTmodelsofvaryingsizesconsistentlybenefitfromCAD.Thex-axisindicatesthesizeoflanguage
modelsandthey-axisistheperformance.
Figure3: Effectoftheadjustmentlevelα. They-axisistheperformanceandthex-axisisα.
facttriplesextractedfromsourcedocuments(Cao tions,ascurrentLMsoftenoverlookthecontexts
et al., 2018; Zhu et al., 2021), optimizing sum- and rely heavily on their prior parametric knowl-
marization models towards a factual consistency edge(Longpreetal.,2021;Chenetal.,2022). Ex-
metrics (Nan et al., 2021; Cao and Wang, 2021), istingapproachesforimprovingmodel’sfaithful-
learningapost-editingerrorcorrector(Dongetal., ness to the context, such as the prompting-based
2020)andremovingnoisytrainingsamples(Kang method (Zhou et al., 2023), are limited in that
and Hashimoto, 2020; Goyal and Durrett, 2021). they could only apply to large-scale instruction-
Thesemethodsrequireadditionalfine-tuningand finetunedLMslikeOpenAI’stext-davinci-003. In
arenotdirectlysuitableforzero-shotandfew-shot contrast,ourworkinvestigatesadecodingstrategy
promptingscenarios. Kingetal.(2022)andSrid- totacklethisproblem,applicabletoanyLM.
harandVisser(2022)proposetoalleviatetheissue
byconstrainingbeamsearchalgorithms.
7 Conclusion
Knowledgeconflicts Whenpresentedwithanup-
dateddocumentwithconflictingknowledge,weex- Language models suffer from an insufficient at-
pectlanguagemodelstogenerateresponsesbased tentiontothegivencontextcomparedtoitsprior
ontheprovidedcontextsratherthanrelyingsolely knowledge, leading to an unfaithful generation
on outdated parametric knowledge. This setting to the input context. We present CAD, a simple
is especially valuable to retrieval-augmented lan- inference-time method that downweights an out-
guagemodels(Khandelwaletal.,2020;Shietal., put probability associated with the model’s prior
2024; Min et al., 2023; Yasunaga et al., 2023), knowledgetopromotemodels’attentiontothecon-
wheredocumentsretrievedfromexternaldatabases text. Weexperimentontwofamiliesoftasksthat
areusedasadditionalinputtoprovideLMsaddi- requireastrongattentiontothecontextandshow
tionalknowledge. However,simplyaddingdocu- that CAD provides more faithful outputs across
ments does not always change the model predic- differentlanguagemodelsofvarioussizes.
787

| Limitations |     |     |     |     |     |     | Punta Cana, | Dominican | Republic. | Association |     | for |
| ----------- | --- | --- | --- | --- | --- | --- | ----------- | --------- | --------- | ----------- | --- | --- |
ComputationalLinguistics.
OurproposedCADmethodrequirestheoutputlog-
ZiqiangCao,FuruWei,WenjieLi,andSujianLi.2018.
itsfromlanguagemodelsinordertocontrastively
calculatetheprobabilitydistributionwithandwith- Faithfultotheoriginal: Factawareneuralabstractive
|              |     |                               |     |     |     |     | summarization.  | InProceedingsoftheThirty-Second |            |               |     |        |
| ------------ | --- | ----------------------------- | --- | --- | --- | --- | --------------- | ------------------------------- | ---------- | ------------- | --- | ------ |
| outcontexts. |     | However,API-basedlanguagemod- |     |     |     |     |                 |                                 |            |               |     |        |
|              |     |                               |     |     |     |     | AAAI Conference | on                              | Artificial | Intelligence, |     | (AAAI- |
elslikeChatGPTandGPT-4maynotprovideout- 18), the 30th innovative Applications of Artificial
putlogits. Consequently,itisnotfeasibleforCAD Intelligence(IAAI-18),andthe8thAAAISymposium
tobedirectlyappliedtosuchfullyblack-boxmod- on Educational Advances in Artificial Intelligence
(EAAI-18),NewOrleans,Louisiana,USA,February
els. Furthermore,CADintroducesahyperparam-
2-7,2018,pages4784–4791.AAAIPress.
| eter α, | which | serves | to regulate |     | the level | of con- |     |     |     |     |     |     |
| ------- | ----- | ------ | ----------- | --- | --------- | ------- | --- | --- | --- | --- | --- | --- |
trastiveadjustment. Whilewehaveobservedthat Stephanie Chan, Adam Santoro, Andrew Lampinen,
α = 0.5yieldsconsistentenhancementscompared JaneWang,AadityaSingh,PierreRichemond,James
|            |           |     |           |        |     |            | McClelland, | and Felix | Hill. | 2022. | Data distribu- |     |
| ---------- | --------- | --- | --------- | ------ | --- | ---------- | ----------- | --------- | ----- | ----- | -------------- | --- |
| to regular | decoding, |     | different | models |     | applied to |             |           |       |       |                |     |
tionalpropertiesdriveemergentin-contextlearning
varioustasksmayhavedistinctoptimalvaluesfor
|     |     |     |     |     |     |     | intransformers. | InAdvancesinNeuralInformation |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --------------- | ----------------------------- | --- | --- | --- | --- |
α. Ifthereexistsaverysmalldemonstrationsetof ProcessingSystems,volume35,pages18878–18891.
in-domainexamples,wewouldconsidertheselec- CurranAssociates,Inc.
tionofαsimilartootherdecodingparameterslike
|     |     |     |     |     |     |     | Hung-Ting | Chen, Michael | Zhang, | and | Eunsol | Choi. |
| --- | --- | --- | --- | --- | --- | --- | --------- | ------------- | ------ | --- | ------ | ----- |
thetop-portemperaturevalues.
2022. Richknowledgesourcesbringcomplexknowl-
|                 |     |     |     |     |     |     | edgeconflicts:    | Recalibratingmodelstoreflectcon- |     |     |     |     |
| --------------- | --- | --- | --- | --- | --- | --- | ----------------- | -------------------------------- | --- | --- | --- | --- |
| Acknowledgement |     |     |     |     |     |     | flictingevidence. | InProceedingsofthe2022Con-       |     |     |     |     |
ferenceonEmpiricalMethodsinNaturalLanguage
| We thank | Alisa | Liu | and | Jiacheng | Liu | for pro- |             |                  |     |     |        |        |
| -------- | ----- | --- | --- | -------- | --- | -------- | ----------- | ---------------- | --- | --- | ------ | ------ |
|          |       |     |     |          |     |          | Processing, | pages 2292–2307, |     | Abu | Dhabi, | United |
viding insights during discussions of the project. ArabEmirates.AssociationforComputationalLin-
guistics.
| This research   |     | is supported |     | in part      | by  | the Office |     |     |     |     |     |     |
| --------------- | --- | ------------ | --- | ------------ | --- | ---------- | --- | --- | --- | --- | --- | --- |
| of the Director |     | of National  |     | Intelligence |     | (ODNI),    |     |     |     |     |     |     |
HyungWonChung,LeHou,ShayneLongpre,Barret
| Intelligence | Advanced |     | Research |     | Projects | Activ- |     |     |     |     |     |     |
| ------------ | -------- | --- | -------- | --- | -------- | ------ | --- | --- | --- | --- | --- | --- |
Zoph,YiTay,WilliamFedus,YunxuanLi,Xuezhi
ity (IARPA), via the HIATUS Program contract Wang, Mostafa Dehghani, Siddhartha Brahma, Al-
#2022-22072200004. Thismaterialisalsofunded bert Webson, Shixiang Shane Gu, Zhuyun Dai,
MiracSuzgun,XinyunChen,AakankshaChowdh-
| in part | by the | DARPA |     | Grant | under | Contract |     |     |     |     |     |     |
| ------- | ------ | ----- | --- | ----- | ----- | -------- | --- | --- | --- | --- | --- | --- |
ery,AlexCastro-Ros,MariePellat,KevinRobinson,
| No. HR001120C0124. |     |     |     | We also | gratefully | ac- |     |     |     |     |     |     |
| ------------------ | --- | --- | --- | ------- | ---------- | --- | --- | --- | --- | --- | --- | --- |
DashaValter,SharanNarang,GauravMishra,Adams
knowledge support from NSF CAREER Grant Yu, Vincent Zhao, Yanping Huang, Andrew Dai,
No. IIS2142739, NSF Grants No. IIS2125201, HongkunYu,SlavPetrov,EdH.Chi,JeffDean,Ja-
cobDevlin,AdamRoberts,DennyZhou,QuocV.Le,
| IIS2203097, |                                 | and the | Alfred | P. Sloan | Foundation |     |                   |                               |                              |     |     |     |
| ----------- | ------------------------------- | ------- | ------ | -------- | ---------- | --- | ----------------- | ----------------------------- | ---------------------------- | --- | --- | --- |
|             |                                 |         |        |          |            |     | andJasonWei.2022. |                               | Scalinginstruction-finetuned |     |     |     |
| Fellowship. | Theviewsandconclusionscontained |         |        |          |            |     |                   |                               |                              |     |     |     |
|             |                                 |         |        |          |            |     | languagemodels.   | ArXivpreprint,abs/2210.11416. |                              |     |     |     |
hereinarethoseoftheauthorsandshouldnotbein-
terpreted as necessarily representing the official Joe Davison, Joshua Feldman, and Alexander Rush.
2019. Commonsenseknowledgeminingfrompre-
| policies, | either | expressed |             | or implied, |     | of ODNI,  |                |                               |     |     |     |     |
| --------- | ------ | --------- | ----------- | ----------- | --- | --------- | -------------- | ----------------------------- | --- | --- | --- | --- |
|           |        |           |             |             |     |           | trainedmodels. | InProceedingsofthe2019Confer- |     |     |     |     |
| IARPA,    | or the | U.S.      | Government. |             | The | U.S. Gov- |                |                               |     |     |     |     |
enceonEmpiricalMethodsinNaturalLanguagePro-
ernmentisauthorizedtoreproduceanddistribute
cessingandthe9thInternationalJointConference
reprintsforgovernmentalpurposesnotwithstand- onNaturalLanguageProcessing(EMNLP-IJCNLP),
pages1173–1178,HongKong,China.Association
inganycopyrightannotationtherein.
forComputationalLinguistics.
YueDong,ShuohangWang,ZheGan,YuCheng,Jackie
References
|            |        |           |       |       |          |        | Chi Kit                                       | Cheung, and | Jingjing   | Liu. | 2020.        | Multi- |
| ---------- | ------ | --------- | ----- | ----- | -------- | ------ | --------------------------------------------- | ----------- | ---------- | ---- | ------------ | ------ |
|            |        |           |       |       |          |        | factcorrectioninabstractivetextsummarization. |             |            |      |              | In     |
| Sid Black, | Gao    | Leo,      | Phil  | Wang, | Connor   | Leahy, |                                               |             |            |      |              |        |
|            |        |           |       |       |          |        | Proceedings                                   | of the 2020 | Conference |      | on Empirical |        |
| and        | Stella | Biderman. | 2021. |       | GPT-Neo: | Large  |                                               |             |            |      |              |        |
MethodsinNaturalLanguageProcessing(EMNLP),
ScaleAutoregressiveLanguageModelingwithMesh-
| Tensorflow. |     |     |     |     |     |     | pages9320–9331,Online.AssociationforComputa- |     |     |     |     |     |
| ----------- | --- | --- | --- | --- | --- | --- | -------------------------------------------- | --- | --- | --- | --- | --- |
tionalLinguistics.
| ShuyangCaoandLuWang.2021. |     |     |     | CLIFF:Contrastive |     |     |     |     |     |     |     |     |
| ------------------------- | --- | --- | --- | ----------------- | --- | --- | --- | --- | --- | --- | --- | --- |
learningforimprovingfaithfulnessandfactualityin Shangbin Feng, Vidhisha Balachandran, Yuyang Bai,
abstractive summarization. In Proceedings of the and Yulia Tsvetkov. 2023. FactKB: Generaliz-
2021ConferenceonEmpiricalMethodsinNatural ablefactualityevaluationusinglanguagemodelsen-
LanguageProcessing,pages6633–6649,Onlineand hancedwithfactualknowledge. InProceedingsof
788

the2023ConferenceonEmpiricalMethodsinNatu- MethodsinNaturalLanguageProcessing(EMNLP),
ralLanguageProcessing,pages933–952,Singapore. pages9332–9346,Online.AssociationforComputa-
| AssociationforComputationalLinguistics. |     |     |               |     | tionalLinguistics. |     |                     |     |     |            |
| --------------------------------------- | --- | --- | ------------- | --- | ------------------ | --- | ------------------- | --- | --- | ---------- |
| TanyaGoyalandGregDurrett.2021.          |     |     | Annotatingand |     |                    |     |                     |     |     |            |
|                                         |     |     |               |     | TomKwiatkowski,    |     | JennimariaPalomaki, |     |     | OliviaRed- |
modeling fine-grained factuality in summarization. field,MichaelCollins,AnkurParikh,ChrisAlberti,
InProceedingsofthe2021ConferenceoftheNorth DanielleEpstein,IlliaPolosukhin,JacobDevlin,Ken-
AmericanChapteroftheAssociationforComputa-
tonLee,KristinaToutanova,LlionJones,Matthew
| tionalLinguistics: |     | HumanLanguageTechnologies, |     |     |         |          |        |        |     |            |
| ------------------ | --- | -------------------------- | --- | --- | ------- | -------- | ------ | ------ | --- | ---------- |
|                    |     |                            |     |     | Kelcey, | Ming-Wei | Chang, | Andrew | M.  | Dai, Jakob |
pages1449–1462,Online.AssociationforComputa-
|     |     |     |     |     | Uszkoreit, | Quoc | Le, and | Slav Petrov. |     | 2019. Natu- |
| --- | --- | --- | --- | --- | ---------- | ---- | ------- | ------------ | --- | ----------- |
tionalLinguistics. ralquestions: Abenchmarkforquestionanswering
|     |     |     |     |     | research. | TransactionsoftheAssociationforCompu- |     |     |     |     |
| --- | --- | --- | --- | --- | --------- | ------------------------------------- | --- | --- | --- | --- |
MeiqiGuo,RebeccaHwa,andAdrianaKovashka.2023. tationalLinguistics,7:452–466.
| Decoding | symbolism | in language | models. | In Pro- |     |     |     |     |     |     |
| -------- | --------- | ----------- | ------- | ------- | --- | --- | --- | --- | --- | --- |
ceedingsofthe61stAnnualMeetingoftheAssocia-
PhilippeLaban,TobiasSchnabel,PaulN.Bennett,and
| tionforComputationalLinguistics(Volume1: |     |     |     | Long |                     |     |     |                        |     |     |
| ---------------------------------------- | --- | --- | --- | ---- | ------------------- | --- | --- | ---------------------- | --- | --- |
|                                          |     |     |     |      | MartiA.Hearst.2022. |     |     | SummaC:Re-visitingNLI- |     |     |
Papers),pages3311–3324,Toronto,Canada.Associ-
basedmodelsforinconsistencydetectioninsumma-
ationforComputationalLinguistics.
|     |     |     |     |     | rization. | TransactionsoftheAssociationforCompu- |     |     |     |     |
| --- | --- | --- | --- | --- | --------- | ------------------------------------- | --- | --- | --- | --- |
tationalLinguistics,10:163–177.
| JonathanHoandTimSalimans.2022. |     |                               |     | Classifier-free |     |     |     |     |     |     |
| ------------------------------ | --- | ----------------------------- | --- | --------------- | --- | --- | --- | --- | --- | --- |
| diffusionguidance.             |     | ArXivpreprint,abs/2207.12598. |     |                 |     |     |     |     |     |     |
JiweiLi,MichelGalley,ChrisBrockett,JianfengGao,
AriHoltzman,JanBuys,LiDu,MaxwellForbes,and and Bill Dolan. 2016. A diversity-promoting ob-
Yejin Choi. 2020. The curious case of neural text jectivefunctionforneuralconversationmodels. In
degeneration. In 8th International Conference on Proceedings of the 2016 Conference of the North
AmericanChapteroftheAssociationforComputa-
LearningRepresentations,ICLR2020,AddisAbaba,
|     |     |     |     |     | tionalLinguistics: |     | HumanLanguageTechnologies, |     |     |     |
| --- | --- | --- | --- | --- | ------------------ | --- | -------------------------- | --- | --- | --- |
Ethiopia,April26-30,2020.OpenReview.net.
pages110–119,SanDiego,California.Association
AriHoltzman,PeterWest,VeredShwartz,YejinChoi, forComputationalLinguistics.
| and Luke | Zettlemoyer. | 2021. | Surface | form com- |     |     |     |     |     |     |
| -------- | ------------ | ----- | ------- | --------- | --- | --- | --- | --- | --- | --- |
petition: Why the highest probability answer isn’t XiangLisaLi,AriHoltzman,DanielFried,PercyLiang,
alwaysright. InProceedingsofthe2021Conference Jason Eisner, Tatsunori Hashimoto, Luke Zettle-
onEmpiricalMethodsinNaturalLanguageProcess- moyer, and Mike Lewis. 2023. Contrastive decod-
ing,pages7038–7051,OnlineandPuntaCana,Do- ing: Open-endedtextgenerationasoptimization. In
minican Republic. Association for Computational Proceedings of the 61st Annual Meeting of the As-
| Linguistics. |     |     |     |     | sociationforComputationalLinguistics(Volume1: |     |     |     |     |     |
| ------------ | --- | --- | --- | --- | --------------------------------------------- | --- | --- | --- | --- | --- |
LongPapers),pages12286–12312,Toronto,Canada.
| Daniel Kang | and | Tatsunori B. | Hashimoto. | 2020. Im- |     |     |     |     |     |     |
| ----------- | --- | ------------ | ---------- | --------- | --- | --- | --- | --- | --- | --- |
AssociationforComputationalLinguistics.
provednaturallanguagegenerationvialosstrunca-
tion. InProceedingsofthe58thAnnualMeetingof Chin-Yew Lin. 2004. ROUGE: A package for auto-
theAssociationforComputationalLinguistics,pages
|     |     |     |     |     | maticevaluationofsummaries. |     |     |     | InTextSummariza- |     |
| --- | --- | --- | --- | --- | --------------------------- | --- | --- | --- | ---------------- | --- |
718–731,Online.AssociationforComputationalLin-
tionBranchesOut,pages74–81,Barcelona,Spain.
guistics.
AssociationforComputationalLinguistics.
UrvashiKhandelwal,OmerLevy,DanJurafsky,Luke
|                                |     |                         |     |                | Alisa Liu | and | Jiacheng | Liu. | 2023.           | The |
| ------------------------------ | --- | ----------------------- | --- | -------------- | --------- | --- | -------- | ---- | --------------- | --- |
| Zettlemoyer,andMikeLewis.2020. |     |                         |     | Generalization |           |     |          |      |                 |     |
|                                |     |                         |     |                | memotrap  |     | dataset. |      | https://github. |     |
| throughmemorization:           |     | Nearestneighborlanguage |     |                |           |     |          |      |                 |     |
com/inverse-scaling/prize/blob/main/
| models. | In8thInternationalConferenceonLearning |     |     |     |     |     |     |     |     |     |
| ------- | -------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
data-release/README.md.
Representations,ICLR2020,AddisAbaba,Ethiopia,
April26-30,2020.OpenReview.net.
|     |     |     |     |     | Alisa Liu, | Maarten | Sap, | Ximing | Lu, | Swabha |
| --- | --- | --- | --- | --- | ---------- | ------- | ---- | ------ | --- | ------ |
Swayamdipta,ChandraBhagavatula,NoahA.Smith,
| Daniel King, | Zejiang | Shen, | Nishant | Subramani, |                    |     |                            |     |     |     |
| ------------ | ------- | ----- | ------- | ---------- | ------------------ | --- | -------------------------- | --- | --- | --- |
|              |         |       |         |            | andYejinChoi.2021. |     | DExperts:Decoding-timecon- |     |     |     |
DanielS.Weld,IzBeltagy,andDougDowney.2022.
trolledtextgenerationwithexpertsandanti-experts.
| Don’tsaywhatyoudon’tknow: |     |     | Improvingthecon- |     |     |     |     |     |     |     |
| ------------------------- | --- | --- | ---------------- | --- | --- | --- | --- | --- | --- | --- |
sistencyofabstractivesummarizationbyconstraining In Proceedings of the 59th Annual Meeting of the
beamsearch. InProceedingsofthe2ndWorkshopon Association for Computational Linguistics and the
NaturalLanguageGeneration,Evaluation,andMet- 11thInternationalJointConferenceonNaturalLan-
|     |     |     |     |     | guageProcessing(Volume1: |     |     | LongPapers),pages |     |     |
| --- | --- | --- | --- | --- | ------------------------ | --- | --- | ----------------- | --- | --- |
rics(GEM),pages555–571,AbuDhabi,UnitedArab
6691–6706,Online.AssociationforComputational
| Emirates     | (Hybrid). | Association | for | Computational |              |     |     |     |     |     |
| ------------ | --------- | ----------- | --- | ------------- | ------------ | --- | --- | --- | --- | --- |
| Linguistics. |           |             |     |               | Linguistics. |     |     |     |     |     |
WojciechKryscinski,BryanMcCann,CaimingXiong, Shayne Longpre, Kartik Perisetla, Anthony Chen,
and Richard Socher. 2020. Evaluating the factual Nikhil Ramesh, Chris DuBois, and Sameer Singh.
consistency of abstractive text summarization. In 2021. Entity-basedknowledgeconflictsinquestion
Proceedings of the 2020 Conference on Empirical answering. InProceedingsofthe2021Conference
789

onEmpiricalMethodsinNaturalLanguageProcess- WentauYih.2024. REPLUG:Retrieval-augmented
ing,pages7052–7063,OnlineandPuntaCana,Do- black-boxlanguagemodels. InProceedingsofthe
minican Republic. Association for Computational 2024ConferenceoftheNorthAmericanChapterof
|     |     |     |     |     |     | theAssociationforComputationalLinguistics: |     |     |     |     | Hu- |
| --- | --- | --- | --- | --- | --- | ------------------------------------------ | --- | --- | --- | --- | --- |
Linguistics.
manLanguageTechnologies.
NikolayMalkin,ZhenWang,andNebojsaJojic.2022.
Coherenceboosting: Whenyourpretrainedlanguage Arvind Krishna Sridhar and Erik Visser. 2022. Im-
modelisnotpayingenoughattention. InProceedings proved beam search for hallucination mitigation
of the 60th Annual Meeting of the Association for in abstractive summarization. ArXiv preprint,
| ComputationalLinguistics(Volume1: |     |     |     | LongPapers), |     | abs/2212.02712. |     |     |     |     |     |
| --------------------------------- | --- | --- | --- | ------------ | --- | --------------- | --- | --- | --- | --- | --- |
pages8214–8236,Dublin,Ireland.Associationfor
ComputationalLinguistics. HugoTouvron,ThibautLavril,GautierIzacard,Xavier
Martinet,Marie-AnneLachaux,TimothéeLacroix,
| Joshua Maynez, | Shashi | Narayan, |                 | Bernd Bohnet, | and    |          |          |              |        |      |         |
| -------------- | ------ | -------- | --------------- | ------------- | ------ | -------- | -------- | ------------ | ------ | ---- | ------- |
|                |        |          |                 |               |        | Baptiste | Rozière, | Naman        | Goyal, | Eric | Hambro, |
| Ryan McDonald. |        | 2020.    | On faithfulness | and           | factu- |          |          |              |        |      |         |
|                |        |          |                 |               |        | Faisal   | Azhar,   | et al. 2023. | LLaMA: | Open | and ef- |
alityinabstractivesummarization. InProceedings ficientfoundationlanguagemodels. ArXivpreprint,
| of the 58th   | Annual | Meeting      | of    | the Association | for | abs/2302.13971. |     |     |     |     |     |
| ------------- | ------ | ------------ | ----- | --------------- | --- | --------------- | --- | --- | --- | --- | --- |
| Computational |        | Linguistics, | pages | 1906–1919,      | On- |                 |     |     |     |     |     |
line.AssociationforComputationalLinguistics. Liam van der Poel, Ryan Cotterell, and Clara Meis-
|     |     |     |     |     |     | ter. 2022. | Mutual | information | alleviates |     | hallucina- |
| --- | --- | --- | --- | --- | --- | ---------- | ------ | ----------- | ---------- | --- | ---------- |
SewonMin,WeijiaShi,MikeLewis,XilunChen,Wen-
|     |     |     |     |     |     | tionsinabstractivesummarization. |     |     |     | InProceedings |     |
| --- | --- | --- | --- | --- | --- | -------------------------------- | --- | --- | --- | ------------- | --- |
tauYih,HannanehHajishirzi,andLukeZettlemoyer.
ofthe2022ConferenceonEmpiricalMethodsinNat-
| 2023. Nonparametric |     | masked |     | language modeling. |     |     |     |     |     |     |     |
| ------------------- | --- | ------ | --- | ------------------ | --- | --- | --- | --- | --- | --- | --- |
uralLanguageProcessing,pages5956–5965,Abu
In Findings of the Association for Computational Dhabi,UnitedArabEmirates.AssociationforCom-
| Linguistics: | ACL2023,pages2097–2118,Toronto, |     |     |     |     | putationalLinguistics. |     |     |     |     |     |
| ------------ | ------------------------------- | --- | --- | --- | --- | ---------------------- | --- | --- | --- | --- | --- |
Canada.AssociationforComputationalLinguistics.
|     |     |     |     |     |     | MichihiroYasunaga, |     | ArmenAghajanyan, |     |     | WeijiaShi, |
| --- | --- | --- | --- | --- | --- | ------------------ | --- | ---------------- | --- | --- | ---------- |
FengNan,CiceroNogueiradosSantos,HenghuiZhu,
RichJames,JureLeskovec,PercyLiang,MikeLewis,
PatrickNg,KathleenMcKeown,RameshNallapati,
|     |     |     |     |     |     | LukeZettlemoyer,andWen-tauYih.2023. |     |     |     |     | Retrieval- |
| --- | --- | --- | --- | --- | --- | ----------------------------------- | --- | --- | --- | --- | ---------- |
DejiaoZhang,ZhiguoWang,AndrewO.Arnold,and
|             |       |           |     |                     |     | augmentedmultimodallanguagemodeling. |     |     |     |     | InInter- |
| ----------- | ----- | --------- | --- | ------------------- | --- | ------------------------------------ | --- | --- | --- | --- | -------- |
| Bing Xiang. | 2021. | Improving |     | factual consistency |     |                                      |     |     |     |     |          |
nationalConferenceonMachineLearning(ICML).
ofabstractivesummarizationviaquestionanswering.
In Proceedings of the 59th Annual Meeting of the Susan Zhang, Stephen Roller, Naman Goyal, Mikel
Association for Computational Linguistics and the Artetxe,MoyaChen,ShuohuiChen,ChristopherDe-
11thInternationalJointConferenceonNaturalLan- wan,MonaDiab,XianLi,XiVictoriaLin,etal.2022.
| guageProcessing(Volume1: |     |     | LongPapers),pages |     |     |     |     |     |     |     |     |
| ------------------------ | --- | --- | ----------------- | --- | --- | --- | --- | --- | --- | --- | --- |
Opt: Openpre-trainedtransformerlanguagemodels.
6881–6894,Online.AssociationforComputational ArXivpreprint,abs/2205.01068.
Linguistics.
TianyiZhang,FaisalLadhak,EsinDurmus,PercyLiang,
Shashi Narayan, Shay B. Cohen, and Mirella Lapata. Kathleen McKeown, and Tatsunori B. Hashimoto.
2018. Don’tgivemethedetails,justthesummary! 2024. Benchmarking Large Language Models for
topic-aware convolutional neural networks for ex- NewsSummarization. TransactionsoftheAssocia-
| treme summarization. |     |     | In Proceedings | of the | 2018 |     |     |     |     |     |     |
| -------------------- | --- | --- | -------------- | ------ | ---- | --- | --- | --- | --- | --- | --- |
tionforComputationalLinguistics,12:39–57.
| Conference | on  | Empirical | Methods | in Natural | Lan- |     |     |     |     |     |     |
| ---------- | --- | --------- | ------- | ---------- | ---- | --- | --- | --- | --- | --- | --- |
guageProcessing,pages1797–1807,Brussels,Bel-
|     |     |     |     |     |     | Wenxuan | Zhou, | Sheng | Zhang, Hoifung |     | Poon, and |
| --- | --- | --- | --- | --- | --- | ------- | ----- | ----- | -------------- | --- | --------- |
gium.AssociationforComputationalLinguistics. Muhao Chen. 2023. Context-faithful prompting
|                   |     |          |               |     |       | for large | language | models.       | In Findings  |     | of the As- |
| ----------------- | --- | -------- | ------------- | --- | ----- | --------- | -------- | ------------- | ------------ | --- | ---------- |
| Artidoro Pagnoni, |     | Vidhisha | Balachandran, | and | Yulia |           |          |               |              |     |            |
|                   |     |          |               |     |       | sociation | for      | Computational | Linguistics: |     | EMNLP      |
Tsvetkov.2021. Understandingfactualityinabstrac- 2023,pages14544–14556,Singapore.Association
tivesummarizationwithFRANK:Abenchmarkfor
forComputationalLinguistics.
| factualitymetrics. |     | InProceedingsofthe2021Con- |     |     |     |     |     |     |     |     |     |
| ------------------ | --- | -------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
ferenceoftheNorthAmericanChapteroftheAsso-
|                                     |     |     |     |           |     | Chenguang | Zhu, | William | Hinthorn, | Ruochen | Xu, |
| ----------------------------------- | --- | --- | --- | --------- | --- | --------- | ---- | ------- | --------- | ------- | --- |
| ciationforComputationalLinguistics: |     |     |     | HumanLan- |     |           |      |         |           |         |     |
QingkaiZeng,MichaelZeng,XuedongHuang,and
guageTechnologies,pages4812–4829,Online.As- Meng Jiang. 2021. Enhancing factual consistency
sociationforComputationalLinguistics. ofabstractivesummarization. InProceedingsofthe
2021ConferenceoftheNorthAmericanChapterof
AbigailSee,PeterJ.Liu,andChristopherD.Manning. theAssociationforComputationalLinguistics: Hu-
| 2017. Gettothepoint: |     | Summarizationwithpointer- |     |     |     |     |     |     |     |     |     |
| -------------------- | --- | ------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
manLanguageTechnologies,pages718–733,Online.
| generatornetworks. |     | InProceedingsofthe55thAn- |     |     |     |     |     |     |     |     |     |
| ------------------ | --- | ------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
AssociationforComputationalLinguistics.
nualMeetingoftheAssociationforComputational
| Linguistics | (Volume | 1:  | Long Papers), | pages | 1073– |     |     |     |     |     |     |
| ----------- | ------- | --- | ------------- | ----- | ----- | --- | --- | --- | --- | --- | --- |
1083,Vancouver,Canada.AssociationforComputa-
tionalLinguistics.
WeijiaShi,SewonMin,MichihiroYasunaga,Minjoon
Seo,RichJames,MikeLewis,LukeZettlemoyer,and
790

| A Appendix |     |     |     | Wealsoextensivelyexperimentthesetupwithadi- |     |     |          |
| ---------- | --- | --- | --- | ------------------------------------------- | --- | --- | -------- |
|            |     |     |     | versesetoflanguagemodelsandscales.          |     |     | DExperts |
A.1 QualitativeAnalyais
(Liuetal.,2021)demotestheoutputdistributionof
ananti-expert(e.g.,exposedtotoxiclanguage)to
XSUM
helpleadthegenerationsfreefromtheunwanted
Article HepassedawaypeacefullyinhospitalonTues- attributes. Contrastive decoding (Li et al., 2023)
dayafterashortillness.BorninTourmakeady,
|     |     |     |     | demotes | an amateur model | (e.g., models | with a |
| --- | --- | --- | --- | ------- | ---------------- | ------------- | ------ |
CountyMayo,heworkedasateacherbefore
securing a part in the premiere of the Brian verysmallnumberofparameters)tohelpdistillthe
FrielplayTranslationsin1980.Lallybecame expertknowledgelearnedinthelarger,morecom-
|     | a household name | in Ireland | for his role as |          |                     |             |          |
| --- | ---------------- | ---------- | --------------- | -------- | ------------------- | ----------- | -------- |
|     |                  |            |                 | petitive | models. In general, | contrastive | decoding |
MileyByrneintheRTEsoapoperaGlenroe
andlaterstarredintheBBCseriesBallykissan- has shown to be a general way to control model
gel.HealsoappearedintheHollywoodmovie
outputs,whichwereinforcebyconsideringthenew
AlexanderandprovidedthevoicefortheOscar-
caseoffactualconsistencywiththetextualcontext.
nominated,animatedIrishfilm,TheSecretof
Kells. AsafluentIrishspeakerandadvocate
ofthelanguage,LallyhadrolesinseveralIrish Pointwisemutualinformationintextclassifica-
|     | languagefilms... |     |     | tion TheconceptofPointwiseMutualInforma- |     |     |     |
| --- | ---------------- | --- | --- | ---------------------------------------- | --- | --- | --- |
Regular WestministeractorPat Lallydiedinhospital tion(PMI)isextensivelyexaminedintextclassifi-
|     | onTuesdaynight | aged82 |     |     |     |     |     |
| --- | -------------- | ------ | --- | --- | --- | --- | --- |
cationandreranking,servingtoadjusttheweight-
CAD ActorLally,bestknownforGlenroeandBal- ingofvariousclassificationchoicesbasedonthe
lykissangel,hasdiedinhospitalonTuesday
increasedlikelihoodofananswergivenaquestion
MemoTrap
|     |     |     |     | within a | specific task domain. | Past | research has |
| --- | --- | --- | --- | -------- | --------------------- | ---- | ------------ |
Input Write a quote that ends in the word “early”. appliedittozero-shotmultiple-choicetasks(Holtz-
Betterlatethan
manetal.,2021),aswellasthererankingofcandi-
| Regular | never |     |     |                                         |     |     |     |
| ------- | ----- | --- | --- | --------------------------------------- | --- | --- | --- |
| CAD     | early |     |     | datesforcommonsenseandsymbolicknowledge |     |     |     |
extraction(Guoetal.,2023;Davisonetal.,2019).
Table4: Qualitativeexamplesofcontrast-awaredecod-
ing. Thenonfactualorinconsistenttextsarehighlighted
inyellow.
WeprovidequalitativeexamplesforXSUMand
| Memotrap | in Table 4. | In XSUM, | the regular de- |     |     |     |     |
| -------- | ----------- | -------- | --------------- | --- | --- | --- | --- |
codinggeneratestextsthatisnotmentionedinthe
article,whereasCADproducesoutputexclusively
| basedontheinformationintheinputarticle. |     |     | For |     |     |     |     |
| --------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
MemoTrap,thestandarddecodingdisregardsthe
| instruction | and generates  | the memorized   | ending,    |     |     |     |     |
| ----------- | -------------- | --------------- | ---------- | --- | --- | --- | --- |
| while       | CAD adheres to | the instruction | within the |     |     |     |     |
givencontextandproducesthedesiredoutput.
A.2 AdditionalRelatedWork
| Contrastivedecodingmethods |     |     | Contrastivede- |     |     |     |     |
| -------------------------- | --- | --- | -------------- | --- | --- | --- | --- |
codingmethodshavebeenextensivelyexploredfor
| textgeneration. | Coherenceboosting(Malkinetal., |     |     |     |     |     |     |
| --------------- | ------------------------------ | --- | --- | --- | --- | --- | --- |
2022)andCPMI(vanderPoeletal.,2022)demote
| a short                     | context from | a full context,   | focusing on |     |     |     |     |
| --------------------------- | ------------ | ----------------- | ----------- | --- | --- | --- | --- |
| the longer-range            | context      | for coherence     | and over-   |     |     |     |     |
| allbettergenerationquality. |              | MMI-baseddecoding |             |     |     |     |     |
(Lietal.,2016)usesacontrastiveformulationto
| improveoutputdiversityindialoggeneration. |     |     | In  |     |     |     |     |
| ----------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
thiswork,weadoptasameintuitionandfocuson
analyzingtheknowledgeconflictscenarioswhere
thefaithfulnesstothecontextisparticularlyimpor-
tantbutdifficultfortheregulardecodingmethods.
791