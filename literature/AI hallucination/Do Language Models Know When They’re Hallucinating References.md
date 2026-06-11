Do Language Models Know When They’re Hallucinating References?
|     |                           | AyushAgrawal      |     |     |     |     |                                               | MiracSuzgun        |     |     |
| --- | ------------------------- | ----------------- | --- | --- | --- | --- | --------------------------------------------- | ------------------ | --- | --- |
|     |                           | MicrosoftResearch |     |     |     |     |                                               | StanfordUniversity |     |     |
|     | t-agrawalay@microsoft.com |                   |     |     |     |     | msuzgun@stanford.edu                          |                    |     |     |
|     |                           | LesterMackey      |     |     |     |     |                                               | AdamTaumanKalai    |     |     |
|     |                           | MicrosoftResearch |     |     |     |     |                                               | OpenAI             | ∗   |     |
|     | lmackey@microsoft.com     |                   |     |     |     |     |                                               | adam@kal.ai        |     |     |
|     |                           | Abstract          |     |     |     |     | onemightimagine,theramificationsofthesehallu- |                    |     |     |
cinationgenerationscanbeprofoundlydetrimental
| State-of-the-art |     | language    |     | models     | (LMs)    | are |            |         |                |                 |
| ---------------- | --- | ----------- | --- | ---------- | -------- | --- | ---------- | ------- | -------------- | --------------- |
|                  |     |             |     |            |          |     | when these | outputs | find their way | to critical do- |
| notoriously      |     | susceptible | to  | generating | halluci- |     |            |         |                |                 |
mainssuchashealthcare,finance,law,oracademic
| natedinformation. |     | Suchinaccurateoutputsnot |     |     |     |     |     |     |     |     |
| ----------------- | --- | ------------------------ | --- | --- | --- | --- | --- | --- | --- | --- |
publications,wherefactualityisessentialandnon-
onlyunderminethereliabilityofthesemodels
but also limit their use and raise serious con- negotiable. In fact, a recent example underlining
thegravityofthisissueinvolvedaU.S.judgeim-
| cerns | about | misinformation |     | and | propaganda. |     |     |     |     |     |
| ----- | ----- | -------------- | --- | --- | ----------- | --- | --- | --- | --- | --- |
In this work, we focus on hallucinated book posingsanctionsontwoNewYorklawyersforsub-
andarticlereferencesandpresentthemasthe mittingalegalbriefthatincludedseveralfictitious
“model organism” of language model hallu- casecitationsthatweregeneratedbyChatGPT.2
| cination | research, |     | due to | their frequent |     | and |     |     |     |     |
| -------- | --------- | --- | ------ | -------------- | --- | --- | --- | --- | --- | --- |
Thearetwoprimarychallengesaheadforboth
| easy-to-discernnature. |     |     | Wepositthatifalan- |     |     |     |     |     |     |     |
| ---------------------- | --- | --- | ------------------ | --- | --- | --- | --- | --- | --- | --- |
researchersandpractitionerswithintheNLPcom-
| guage       | model | cites          | a particular |         | reference | in   |         |                                      |     |     |
| ----------- | ----- | -------------- | ------------ | ------- | --------- | ---- | ------- | ------------------------------------ | --- | --- |
|             |       |                |              |         |           |      | munity. | Thefirstrequiresdevelopingadeeperun- |     |     |
| its output, |       | then it should |              | ideally | possess   | suf- |         |                                      |     |     |
ficientinformationaboutitsauthorsandcon- derstandingofwhytheselanguagemodelsresortto
tent,amongotherrelevantdetails. Usingthis fabricatinginformation,whiletheseconddemands
basic insight, we illustrate that one can iden- creating mechanisms that can not only promptly
tifyhallucinatedreferenceswithoutevercon-
detectbutalsomitigate,ifnotcompletelyprevent,
sultinganyexternalresources,byaskingaset
|           |     |          |         |        |          |     | inaccurate | information | in model outputs. | To that |
| --------- | --- | -------- | ------- | ------ | -------- | --- | ---------- | ----------- | ----------------- | ------- |
| of direct | or  | indirect | queries | to the | language |     |            |             |                   |         |
effect,inthiswork,westudytheproblemofhallu-
| modelaboutthereferences. |     |                 |     | Thesequeriescan |     |     |         |                  |            |                |
| ------------------------ | --- | --------------- | --- | --------------- | --- | --- | ------- | ---------------- | ---------- | -------------- |
|                          |     |                 |     |                 |     |     | cinated | book and article | references | related to the |
| be considered            |     | as “consistency |     | checks.”        |     | Our |         |                  |            |                |
findings highlight that while LMs, including fieldofcomputerscienceandpresentasimpleyet
GPT-4,oftenproduceinconsistentauthorlists effectivemethodtodetecthallucinatedreferences
forhallucinatedreferences,theyalsooftenac- withoutrelyingonexternaltools.
| curately | recall | the    | authors | of real | references. |     |         |             |               |              |
| -------- | ------ | ------ | ------- | ------- | ----------- | --- | ------- | ----------- | ------------- | ------------ |
|          |        |        |         |         |             |     | Drawing | inspiration | from the role | of the fruit |
| In this  | sense, | the LM | can     | be said | to “know”   |     |         |             |               |              |
fly,Drosophilamelanogaster,asamodelorganism
| when | it is | hallucinating | references. |     | Further- |     |     |     |     |     |
| ---- | ----- | ------------- | ----------- | --- | -------- | --- | --- | --- | --- | --- |
more, these findings show how hallucinated in biological research, we suggest that the NLP
communityfocusonthestudyofhallucinatedref-
| references |     | can be dissected |     | to shed | light | on  |     |     |     |     |
| ---------- | --- | ---------------- | --- | ------- | ----- | --- | --- | --- | --- | --- |
theirnature. Replicationcodeandresultscan erences to better understand and mitigate wider
befoundatgithub.com/microsoft/hallucinated- hallucination challenges. These hallucinated ref-
| references. |     |     |     |     |     |     | erencespresentdistinctcharacteristicsthatrender |     |                           |     |
| ----------- | --- | --- | --- | --- | --- | --- | ----------------------------------------------- | --- | ------------------------- | --- |
|             |     |     |     |     |     |     | themsuitableforstudy.                           |     | First,theirautomaticclas- |     |
1 Introduction
sificationismorestraightforwardthanotherhallu-
cinationvarieties.3
Despitetheirunparalleledcapabilities,recentlarge Asanillustration,ourmethod
thatleveragesasearchengineAPIcloselymatches
| language | models | (LLMs) | still | exhibit | a tendency |     |     |     |     |     |
| -------- | ------ | ------ | ----- | ------- | ---------- | --- | --- | --- | --- | --- |
togenerateseeminglycredibleyetincorrectorun-
founded information. This phenomenon is often ofmeaning(Wittgenstein,1953). Additionally,weusethe
termshallucinateandfabricateinterchangeablythroughout
| referred | to as | the “hallucination” |     |     | problem | in the |     |     |     |     |
| -------- | ----- | ------------------- | --- | --- | ------- | ------ | --- | --- | --- | --- |
thepaper.
|          |                  |     |            |     | (NLP).1 |     | 2Theoriginalnewspaperarticledetailingthisincidentcan |     |     |     |
| -------- | ---------------- | --- | ---------- | --- | ------- | --- | ---------------------------------------------------- | --- | --- | --- |
| field of | natural-language |     | processing |     |         | As  |                                                      |     |     |     |
befoundatthislink.(Merken,2023)
∗WorkdonewhileatMicrosoftResearch. 3Incontrast,hallucinationslikefactoidsposeclassification
1Thoughitisananthropomorphism,weusethetermhallu- challengesduetotheirnuancedphrasingandtheuncertainty
cinateduetoitswidespreadadoption,followingtheuse-theory regardingtheirpresenceintrainingdatasets.
912
FindingsoftheAssociationforComputationalLinguistics:EACL2024,pages912–928
March17-22,2024(cid:13)c2024AssociationforComputationalLinguistics

eachoffourhumanexpertevaluations,inatleast 2 PreliminariesandBackground
| 99outofasampleof100references. |     |     |     |     | Moreover,the |     |     |     |     |     |     |     |     |
| ------------------------------ | --- | --- | --- | --- | ------------ | --- | --- | --- | --- | --- | --- | --- | --- |
FollowingJietal.(2023),wedefine“hallucination”
staticnatureofacademicreferencetitles,combined
|            |       |        |              |     |     |           | as fabricated   | text  | that | has little | or no  | grounding |     |
| ---------- | ----- | ------ | ------------ | --- | --- | --------- | --------------- | ----- | ---- | ---------- | ------ | --------- | --- |
| with their | broad | online | availability |     | (on | platforms |                 |       |      |            |        |           |     |
|            |       |        |              |     |     |           | in the training | data. | It   | is worth   | noting | that this | is  |
likeGoogleScholar,SemanticSearch,andarXiv),
sometimesreferredtoasopen-domainhallucina-
| suggests | they | frequently | appear |     | in large, | popular |     |     |     |     |     |     |     |
| -------- | ---- | ---------- | ------ | --- | --------- | ------- | --- | --- | --- | --- | --- | --- | --- |
tiontodistinguishitfromclosed-domainhalluci-
| language | modeling     | corpora. |        | Additionally, |         | many |                            |     |     |                   |     |     |     |
| -------- | ------------ | -------- | ------ | ------------- | ------- | ---- | -------------------------- | --- | --- | ----------------- | --- | --- | --- |
|          |              |          |        |               |         |      | nation(see:Jietal.,2023).4 |     |     | Ourusageoftheterm |     |     |     |
| within   | the research |          | domain | already       | possess | the  |                            |     |     |                   |     |     |     |
hallucinationalignswiththeopen-domainvariant.
| skills and | knowledge |     | pertinent | to  | studying | these |     |     |     |     |     |     |     |
| ---------- | --------- | --- | --------- | --- | -------- | ----- | --- | --- | --- | --- | --- | --- | --- |
DistinguishingGroundednessfromCorrect-
| hallucinations. |     | We therefore |     | believe | that | just as |     |     |     |     |     |     |     |
| --------------- | --- | ------------ | --- | ------- | ---- | ------- | --- | --- | --- | --- | --- | --- | --- |
ness. Themeasureofcorrectness(orfactuality)re-
| fruit fly | studies | have | enriched | our | understanding |     |     |     |     |     |     |     |     |
| --------- | ------- | ---- | -------- | --- | ------------- | --- | --- | --- | --- | --- | --- | --- | --- |
liesuponacomparisonwithground-truthanswers.
| of biology, | focusing |     | on these | specific |     | reference |     |     |     |     |     |     |     |
| ----------- | -------- | --- | -------- | -------- | --- | --------- | --- | --- | --- | --- | --- | --- | --- |
Previousworkonhallucinationhasblurredtheline
| hallucinations |     | can pave | the | way | for insights | and |                                   |     |     |     |     |            |     |
| -------------- | --- | -------- | --- | --- | ------------ | --- | --------------------------------- | --- | --- | --- | --- | ---------- | --- |
|                |     |          |     |     |              |     | betweengroundednessandfactuality. |     |     |     |     | (Sometimes |     |
solutionsformorecomplexandchallenginghallu-
thisdistinctionisalsoreferredtoashonestyversus
cinationforms.
|                                      |     |                  |     |      |     |          | truthfulness(Evansetal.,2021)). |               |              |              | Forexample,the |         |       |
| ------------------------------------ | --- | ---------------- | --- | ---- | --- | -------- | ------------------------------- | ------------- | ------------ | ------------ | -------------- | ------- | ----- |
|                                      |     |                  |     |      |     |          | common                          | misconception |              | that “people |                | use 10% | of    |
|                                      |     |                  |     |      |     |          | their brains”                   | might         | be           | considered   | grounded       |         | if it |
| Weoutlinetherestofthisworkasfollows. |     |                  |     |      |     | We       |                                 |               |              |              |                |         |       |
|                                      |     |                  |     |      |     |          | is mentioned                    | in            | the training | data         | and            | assumed | to    |
| are interested                       |     | in investigating |     | when | and | why lan- |                                 |               |              |              |                |         |       |
|                                      |     |                  |     |      |     |          | be a true                       | statement;    | however,     |              | this does      | not     | mean  |
guagemodelsproducehallucinatedreferencesand
thatitisfactual,asitisnotascientificallycorrect
| what can | be  | done to | prevent | them. | We  | explore |     |     |     |     |     |     |     |
| -------- | --- | ------- | ------- | ----- | --- | ------- | --- | --- | --- | --- | --- | --- | --- |
statement.
whetherLLMssuchasGPT-4canrecognizetheir
|                  |     |                               |         |     |         |        | Evaluatinggroundedness. |          |           |     | Perfectlyevaluating |     |      |
| ---------------- | --- | ----------------------------- | ------- | --- | ------- | ------ | ----------------------- | -------- | --------- | --- | ------------------- | --- | ---- |
| own hallucinated |     | outputs                       | without |     | relying | on any |                         |          |           |     |                     |     |      |
|                  |     |                               |         |     |         |        | hallucinations          | would    | require   |     | access to           | the | LM’s |
| externaltools.   |     | Whilethisapproachdoesnotfully |         |     |         |        |                         |          |           |     |                     |     |      |
|                  |     |                               |         |     |         |        | training                | data. An | advantage |     | of the hallucinated |     |      |
unravelthereasonsbehindandsolutionstohalluci-
referenceproblemiseaseof(approximate)evalua-
| nations,itaddsvaluableperspective. |     |     |     |     | Specifically, |     |     |     |     |     |     |     |     |
| ---------------------------------- | --- | --- | --- | --- | ------------- | --- | --- | --- | --- | --- | --- | --- | --- |
tioninthatexact-matchWebsearchisareasonable
| if LLMs | can | identify | their | own | hallucinations, | it  |                           |     |     |                      |     |     |     |
| ------- | --- | -------- | ----- | --- | --------------- | --- | ------------------------- | --- | --- | -------------------- | --- | --- | --- |
|         |     |          |       |     |                 |     | heuristicforgroundedness. |     |     | Thisisbecausethevast |     |     |     |
impliestherootoftheissuemaynotlieintraining
majorityofarticletitlespresentinthetrainingdata
orrepresentation,butratherinthegeneration(i.e.,
|           |          |       |      |        |     |            | are included | in  | Web search | results—articles |     |     | are |
| --------- | -------- | ----- | ---- | ------ | --- | ---------- | ------------ | --- | ---------- | ---------------- | --- | --- | --- |
| decoding) | process, | given | that | models |     | inherently |              |     |            |                  |     |     |     |
meanttobepublishedandshared,andpublishers
possessenoughdatatopotentiallylowertherateof
|                 |     |                               |     |     |     |     | aimtomaketheirworkdiscoverablebysearch. |     |     |     |     |     | Fur- |
| --------------- | --- | ----------------------------- | --- | --- | --- | --- | --------------------------------------- | --- | --- | --- | --- | --- | ---- |
| hallucinations. |     | Ourexperimentscompareddiffer- |     |     |     |     |                                         |     |     |     |     |     |      |
thermore,referencesgenerallyhavetitlesthatare
entquestioningstrategiestousetheLMtodetect
specificenoughnottospuriouslyoccurontheWeb.
itsownhallucinationsacrossGPTandLlamabased
|     |     |     |     |     |     |     | Regarding | other | types | of hallucinations, |     | besides |     |
| --- | --- | --- | --- | --- | --- | --- | --------- | ----- | ----- | ------------------ | --- | ------- | --- |
LM’s.
articlenames,whichcannotbeaseasilyevaluated,
|     |     |     |     |     |     |     | we still hope | that | our methodology |     | and | findings |     |
| --- | --- | --- | --- | --- | --- | --- | ------------- | ---- | --------------- | --- | --- | -------- | --- |
wouldapply,evenifevaluatingthosetypesofhal-
| Contributions. |     | Thereareseveralcontributions |     |     |     |     |     |     |     |     |     |     |     |
| -------------- | --- | ---------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
ofthiswork. First,weproposetheproblemofhallu- lucinations would require access to the training
data.
cinatedcomputersciencereferencesasamodelin-
|                                     |     |     |     |     |     |           | Direct | queries | (DQs). | Our | work | builds | upon |
| ----------------------------------- | --- | --- | --- | --- | --- | --------- | ------ | ------- | ------ | --- | ---- | ------ | ---- |
| stanceworthstudying,likeDrosophila. |     |     |     |     |     | Second,we |        |         |        |     |      |        |      |
andisinspiredbytworecentworksthatshowhow
demonstratethattheycanbereliablyandautomat-
|                    |     |        |     |         |     |            | to use black-box |              | generative | LMs     | to         | assess | con-   |
| ------------------ | --- | ------ | --- | ------- | --- | ---------- | ---------------- | ------------ | ---------- | ------- | ---------- | ------ | ------ |
| ically classified. |     | Third, | we  | perform | a   | systematic |                  |              |            |         |            |        |        |
|                    |     |        |     |         |     |            | fidence in       | generations, |            | without | consulting |        | exter- |
LMstudyofhallucinatedreferences,enablingus
|                                       |     |     |     |     |     |         | nalreferencesorinspectingweights. |        |        |           | Inparticular, |     |        |
| ------------------------------------- | --- | --- | --- | --- | --- | ------- | --------------------------------- | ------ | ------ | --------- | ------------- | --- | ------ |
| tocomparehallucinationratesacrossLMs. |     |     |     |     |     | Fourth, |                                   |        |        |           |               |     |        |
|                                       |     |     |     |     |     |         | Kadavath                          | et al. | (2022) | introduce | multiple      |     | direct |
weintroduceindirectqueriesforevaluatinghalluci-
black-boxstrategiesforusinganLMtoextractcon-
nations. Finally,wecomparethesetodirectqueries
|                            |     |     |     |     |             |     | fidence estimates |     | by querying |     | the language |     | mod- |
| -------------------------- | --- | --- | --- | --- | ----------- | --- | ----------------- | --- | ----------- | --- | ------------ | --- | ---- |
| acrossGPTandLlamabasedLMs. |     |     |     |     | Aconclusion |     |                   |     |             |     |              |     |      |
ofourworkforreducinghallucinationistherecog- 4Closed-domainhallucinationistypicallystudiedinareas
nition that changing the generation pipeline can likeabstractivesummarizationandmachinetranslation,where
theoutputsarecomparedrelativetoaspecificsourcedocu-
| certainly | help, | while | it is less | clear | if  | training or |     |     |     |     |     |     |     |
| --------- | ----- | ----- | ---------- | ----- | --- | ----------- | --- | --- | --- | --- | --- | --- | --- |
menttobesummarizedortranslatedasopposedtotheentirety
| representationchangesarenecessary. |     |     |     |     |     |     | ofthetrainingdata. |     |     |     |     |     |     |
| ---------------------------------- | --- | --- | --- | --- | --- | --- | ------------------ | --- | --- | --- | --- | --- | --- |
913

Figure 1: Example direct vs. indirect LM queries for predicting whether a given paper title is hallucinated or
grounded. Directqueriesarebinary,repeatedmultipletimestoestimateaprobability. Indirectqueriesareopen-
ended,andtheiranswersarecomparedtooneanother,usingtheLM,tooutputanagreementfraction. Language
modelgenerationsareindicatedinboldface. Promptsinthisfigurehavebeenshortenedforillustrativepurposes.
els on question-answer problems. Manakul et al. search,includingsearchesandinformationgather-
(2023)applyasimilardirectself-consistencycheck ingoutsideofthesession.” Yet,ourworkprovides
called SelfCheckGPT to identify relative halluci- evidencethataddressingthesehallucinationscan
nationsinasummarizationcontext. Thesequeries beachievedwithoutturningtoexternalresources.
are direct true/false correctness queries. We test Asmentioned,therearemultipledefinitionsof
similar approaches in the context of hallucinated hallucination. Inthiswork,weusethetermhalluci-
references. Black-boxgenerativeapproachesstand nationstomeanfabricatedtextthatisnotgrounded
in contrast to the work that either introspects the inthetrainingdata. Factuallyincorrectgenerations
weightsonLMs(AzariaandMitchell,2023)orthat canbedecomposedintotwotypesoferrors(Evans
consultsexistingdatabases(Guoetal.,2022). etal.,2021): groundederrorswhichmaybedueto
Indirectqueries(IQs). Inaddition,wesuggest fallaciesinthetrainingdata(e.g.,thatpeopleuse
anewapproachusingwhatwecallindirectqueries. only 10% of their brains) and ungrounded errors.
A direct query may ask, Is the following paper Thesetwotypesoferrorsmayneeddifferenttech-
real? whileanindirectquerymayask,Whoarethe niques for remedy. The grounded errors may be
authors of this paper?, as illustrated in Figure 1. reducedbycuratingatrainingsetwithfewererrors
Answersarethengeneratedtotheindirectqueryin orothertechniquessuchasRLHF(Ouyangetal.,
i > 1independentsessions,andtestedforconsis- 2022). However, the ungrounded errors which
tency. The motivation for indirect queries comes we study5 are a fascinating curiosity which still
frominvestigativeinterviews,wheredetectivesare challengetheAIcommunityandonewhichisnot
advisedtointerviewindividualsseparatelyandask clearlyaddressablebyimprovingtrainingdata.
open-ended questions. For instance, consistency Thereiscomparativelylittlepriorworkstudying
may be better evaluated by asking multiple wit- open-domaingroundednesslikeours. Somework
nessesto“Describeindetailwhatthesuspectwas (e.g.,Guuetal.,2023)inattributionaimstounder-
holding”ratherthanasking,“Wasthesuspecthold- standwhichtrainingexamplesaremostinfluential
ingagunintheirrighthand?” (Vredeveldtetal., in a given output. In recent independent work in
2014). In the context of reference hallucination, thehealthspace,Athalurietal.(2023)didanem-
our hypothesis is that the likelihood of multiple piricalevaluationofhallucinatedreferenceswithin
generations agreeing on the same authors for a themedicaldomain. Similartoourapproach,they
hallucinated reference would be smaller than the used a Google search for exact string match as a
likelihoodofmultipleresponsestoadirectquery heuristicforevaluatinghallucinations. Ourstudy
indicatingthatthereferenceexists. of hallucinated references enables us to estimate
thehallucinationratesofdifferentmodels,and,as
3 RelatedWork
discussedinpriorwork,thehallucinationproblem
Open-domainhallucinations,inthecontextofGPT- interestinglybecomesmorepressingasmodelsbe-
4discussions(OpenAI,2023;Bubecketal.,2023), comemoreaccuratebecauseuserstrustthemmore
havegarneredattentiongiventheirprevalenceand (OpenAI,2023).
associated hazards. Bubeck et al. (2023, pg. 82)
5Onecanalsoimagineungroundedcorrectgenerations,
comment: “Opendomainhallucinationsposemore
such as a generated paper title that exists but is not in the
difficultchallenges,perrequiringmoreextensivere- trainingdata,butwefindthesetobequiterare.
914

Related recent works include black-box tech- tion2)bydividingthenumberofcompletionscon-
niques for measuring confidence in LM genera- tainingtheword“yes”bythetotalnumberofcom-
tions. Althoughtheseworksaretargetedatfactual pletions.8 We also consider an ensemble direct
confidence,theapproachesarehighlyrelatedtoour query, denoted by DQ, that simply averages the
work. WhileKadavathetal.(2022)useprobability scoresofDQ1,DQ2,andDQ3.
| estimates | drawn | from | LMs, | it is | straightforward |     |                     |     |     |     |     |     |
| --------- | ----- | ---- | ---- | ----- | --------------- | --- | ------------------- | --- | --- | --- | --- | --- |
|           |       |      |      |       |                 |     | 4.2 IndirectQueries |     |     |     |     |     |
toextendtheirprocedurestogeneration-onlyLMs
like ChatGPT using sampling. Lin et al. (2022) Theindirectquery(IQ)methodinvolvestwomain
showthatLMscanbeusedtoarticulateestimates steps: interrogationandoverlapestimation.
bygeneratingnumbersorwordsaswedo. Finally, Step1: Interrogation. Foreachreference,we
Manakul et al. (2023) perform self-checks in the firstposej indirectqueriestotheLM,askingabout
theauthorsofthegeneratedreference,forinstance,
| contextofsummarizingadocument. |     |     |     |     | Allofthese |     |     |     |     |     |     |     |
| ------------------------------ | --- | --- | --- | --- | ---------- | --- | --- | --- | --- | --- | --- | --- |
worksusedirectquerieswhichinfluencedthede- asshowninFigure3(top).
signofourdirectqueries. Step2: Overlapestimation.. Next,weassesthe
degreeofsimilarity(overlap)betweenthemodelre-
Duetospacelimitations,wedonotdiscussthe
sponsesfromthepreviousstepbyusingaseparate
| work studying |     | closed-domain |     | hallucination |     | (e.g., |     |     |     |     |     |     |
| ------------- | --- | ------------- | --- | ------------- | --- | ------ | --- | --- | --- | --- | --- | --- |
intranslationorsummarization)butinsteadrefer querytemplate,asshowninFigure3(bottom). We
thereadertorecentsurveyofJietal.(2023). initially tested string-matching techniques which
|     |     |     |     |     |     |     | we found | to be inaccurate | and | required | hyperpa- |     |
| --- | --- | --- | --- | --- | --- | --- | -------- | ---------------- | --- | -------- | -------- | --- |
4 Methodology: ConsistencyChecks rameters. Namematchingisknowntobeathorny
|     |     |     |     |     |     |     | problem | and one which | we  | found could |     | be per- |
| --- | --- | --- | --- | --- | --- | --- | ------- | ------------- | --- | ----------- | --- | ------- |
We now provide an overview of our simple yet formedaccuratelywhenusingpretrainedLMsto
effectiveconsistencycheckmethodology,explain-
compareinpairs.9
inghowweperformaseriesofdirectandindirect
|     |     |     |     |     |     |     | Theintuitionbehindourapproachissimple: |     |     |     |     | If  |
| --- | --- | --- | --- | --- | --- | --- | -------------------------------------- | --- | --- | --- | --- | --- |
queriestodetecthallucinatedreferences.6
alanguagemodelprovidessimilar(thatis,consis-
tent)responsestomultipleindirectqueries,itcan
4.1 DirectQueries
|     |     |     |     |     |     |     | then be | assumed that | the model | is most | likely | fa- |
| --- | --- | --- | --- | --- | --- | --- | ------- | ------------ | --------- | ------- | ------ | --- |
Thedirectquery(DQ)methodexaminesifapartic-
|     |     |     |     |     |     |     | miliar with | the reference | and | that it | has seen | the |
| --- | --- | --- | --- | --- | --- | --- | ----------- | ------------- | --- | ------- | -------- | --- |
ulartitleexistsusingaformatillustratedinFigure2. referenceduringitstraining;suchareferencecould
We use three simple DQ templates (DQ1, DQ2, thereforebedeemedgrounded. Ontheotherhand,
| and DQ3), | drawing |     | insights | from | Kadavath | et al. |     |     |     |     |     |     |
| --------- | ------- | --- | -------- | ---- | -------- | ------ | --- | --- | --- | --- | --- | --- |
variedresponsesmightsignalthatthemodeldoes
| (2022);Manakuletal.(2023). |     |     |     | Ineachcase,anLM |     |     |                   |         |           |     |       |         |
| -------------------------- | --- | --- | --- | --------------- | --- | --- | ----------------- | ------- | --------- | --- | ----- | ------- |
|                            |     |     |     |                 |     |     | not intrinsically | possess | knowledge |     | about | the au- |
toexpectedtoanswer“yes”ifitbelievesthatthe thor(s)andcontentofthereference;hence,itcan
referenceactuallyexistsand“no”otherwise.
|     |     |     |     |     |     |     | be speculated | that the | model | has presumably |     | not |
| --- | --- | --- | --- | --- | --- | --- | ------------- | -------- | ----- | -------------- | --- | --- |
DQ1asksoutrightifthereferencedoesindeed
seenthereferenceduringitstrainingandthatthe
exist. Whilebeingsimple,thisapproachcansome- referenceismostlylikelyfabricated.
timesbeproblematicassomechat-bot-basedLMs WealsoconsideranensembleIQ+DQcheckthat
| have strong | biases |     | in answering | questions |     | when |     |     |     |     |     |     |
| ----------- | ------ | --- | ------------ | --------- | --- | ---- | --- | --- | --- | --- | --- | --- |
averagesthescoresofIQandtheDQensemble.
| phrased | in a | particular | way | (without | any | proper |     |     |     |     |     |     |
| ------- | ---- | ---------- | --- | -------- | --- | ------ | --- | --- | --- | --- | --- | --- |
Finally,wehighlightthatourconsistencycheck-
context) (Lu et al., 2022). DQ2 and DQ3, on the ingmethodsdonotrelyonexternalresourcessuch
otherhand,incorporatecontextbystatingthatthe asGoogleScholarorSemanticSearch. Itinstead
referencewasgeneratedbyanLMoranassistant.
|     |     |     |     |     |     |     | aturerateof1whenj | >1(i.e.,generatingmultiplecomple- |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | ----------------- | --------------------------------- | --- | --- | --- | --- |
Moreover,DQ3takesitastepfurtherbyproviding
|     |     |     |     |     |     |     | tions)and0whenj | =1(i.e.,generatingasinglecompletion). |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --------------- | ------------------------------------- | --- | --- | --- | --- |
additionalreferencesforcomparison,anapproach Thechoiceof0isintendedtocapturethemodel’stoppickif
| advocatedinKadavathetal.(2022). |     |     |     |     |     |     | asingleoutputisgenerated. |     |     |     |     |     |
| ------------------------------- | --- | --- | --- | --- | --- | --- | ------------------------- | --- | --- | --- | --- | --- |
8Thismeansthatemptyorotherwiseinvalidanswersare
| Foreachquery,wegeneratej |     |     |     |     | 1completions |     |     |     |     |     |     |     |
| ------------------------ | --- | --- | --- | --- | ------------ | --- | --- | --- | --- | --- | --- | --- |
assigned“no.”Wedonotassumethatthisscoreiscalibrated
≥
toapproximatetheprobabilitydistributionofthe asouranalysisconsidersarbitraryprobabilitythresholds.
9ItisworthnotingthatLMssometimesreturnresponses
| model | about | the existence |     | of the generated |     | refer- |     |     |     |     |     |     |
| ----- | ----- | ------------- | --- | ---------------- | --- | ------ | --- | --- | --- | --- | --- | --- |
thatdonotconsistofalistofauthors(e.g.,alongresponse
ence.7 Wemeasurethegroundednessrate(seeSec-
beginningwith“Icouldnotfindaspecificreferencetitled...”.
|     |     |     |     |     |     |     | Insuchcases,wesimplysettheoverlaprateto0. |     |     |     |     | Wealso |
| --- | --- | --- | --- | --- | --- | --- | ----------------------------------------- | --- | --- | --- | --- | ------ |
6Notethatthispipelineisrunseparatelyforeachofour
notethattraditionalparsingandstring-matchingtechniques
LMs,sothereisnomixingacrossLMs. couldbeleveragedasanalternativetoLMsinthisoverlap
| 7Forbothdirectandindirectqueries,weemployatemper- |     |     |     |     |     |     | estimationphase. |     |     |     |     |     |
| ------------------------------------------------- | --- | --- | --- | --- | --- | --- | ---------------- | --- | --- | --- | --- | --- |
915

Figure2: Examplesofthethreedirectprompttemplatesusedforthedirectqueries,instantiatedwithcandidate
referencetitles.
Figure3: Top: ExampleoftheIndirectQueryprompttemplatesinstantiatedwithacandidatetitle. Bottom: An
exampleofhowweestimateoverlapbetweenapairofanswersusingtheLM.
| usesthesamelanguagemodelthroughoutthehal- |     |     |     | asshowninFigure4. |     |     |     |
| ----------------------------------------- | --- | --- | --- | ----------------- | --- | --- | --- |
lucinationdetectionprocess.
|     |     |     |     | 5.2 AutomaticLabelingandVerification |     |     |     |
| --- | --- | --- | --- | ------------------------------------ | --- | --- | --- |
5 ExperimentalDetails
Next,weemployedtheBingsearchengineAPI10
Here, we describe the steps taken to build a cor- as an automatic labeling heuristic, labeling each
|                |                     |            |     | of the 1,000              | reference titles | generated         | in the pre- |
| -------------- | ------------------- | ---------- | --- | ------------------------- | ---------------- | ----------------- | ----------- |
| pus of article | and book references | pertaining | to  |                           |                  |                   |             |
|                |                     |            |     | viousstepaseithergrounded |                  | (G)orhallucinated |             |
computersciencetopicsforeachlanguagemodel,
aswellastheautomaticlabelingheuristicusedto (H) based on exact matches. The reference title
annotatethesegeneratedreferences. surroundedbyquotesissearchedintheweb(e.g.,
|     |     |     |     | “LMs are | few-shot learners”). | We  | label the refer- |
| --- | --- | --- | --- | -------- | -------------------- | --- | ---------------- |
5.1 DatasetConstructionUsingACMCCS enceashallucinatedifnoresultsareretrievedand
Toensurethatourcorpusofreferencesisrepresen- asgroundedotherwise.
tativeofabroadspectrumofthetopicsincomputer Toassesstheefficacyofthisautomatedpipeline,
weaskedfourexpertannotators(allcomputersci-
science,weusedtheACMComputingClassifica-
tionSystem(CCS;Rous,2012)asourmainsource. entists familiar with academic writing and pub-
TheCCSprovidesastructuredtaxonomyforcom- lication) to manually label 10% of the GPT-4-
|     |     |     |     | generatedreferences. | Oneoftheannotatorsagreed |     |     |
| --- | --- | --- | --- | -------------------- | ------------------------ | --- | --- |
puterscience,rangingfrom12high-levelsubjects
downto543specifictopics. with Bing on 100% of the labels, and the other
From the 543 topics, we selected a uniformly threeeachhad99%agreementwithBing,indicat-
|     |     |     |     | ing strong | support for the | reliability | of the auto- |
| --- | --- | --- | --- | ---------- | --------------- | ----------- | ------------ |
randomsubsetof200topics,eachdenotedasarea:
topic Information retrieval: Retrieval mod- maticlabelingpipeline. SeeAppendixAformore
(e.g.,
| elsandranking). | Foreachchosentopic,wethen |              |        | details. |     |     |     |
| --------------- | ------------------------- | ------------ | ------ | -------- | --- | --- | --- |
| prompted        | each LM to generate       | five related | refer- |          |     |     |     |
10https://www.microsoft.com/en-us/bing/
encetitles,amountingto1,000totaltitlesperLM apis/bing-web-search-api
916

Figure4: Thepromptusedtogenerate5referencetitles. Thismethodgeneratesbothgroundedandhallucinated
references. TopicsarechosenfromtheACMComputingClassificationSystem.
5.3 ModelsandParameters certainrateoftoleranceforhallucinations,andone
would like to maximize the number of generated
WeevaluatetheOpenAILMsGPT-3(text-davinci-
referencessubjecttothatconstraint.
003),ChatGPT(gpt-35-turbo),andGPT-4(gpt-4)
usingtheAzureOpenAIAPIandtheopen-source
6 ResultsandDiscussion
Llama 2 Chat llama-2-*-chat series LMs abbre-
viated as L2-7B, L2-13B, and L2-70B (Touvron Inthissection,wediscusstheperformanceofthe
etal.,2023). indirectanddirectmethodsusingquantitativemet-
Weselecti = 3indirectqueryresultsandtake rics,andpresentinterestingqualitativefindings.
theaverageoftheoverlappingevaluationstocom-
6.1 QuantitativeAnalysis
putethefinalscoreforeachindirectqueryexper-
iment. For direct query experiments, we sample Table1showstheratesofhallucinationforthesix
j = 10 judgments at temperature 1.0 and report modelsstudied. Asexpected,referencesproduced
thefractionofyesresponsesasafinalscore. bythenewermodels(whichachievehigherscores
onotherbenchmarks(Srivastavaetal.,2022))also
5.4 Metrics exhibitahighergroundingrateor,equivalently,a
Receiver Operating Characteristic (ROC) lowerhallucinationrate.
Curves. Sinceeachofourqueryingstrategiesout-
LLM GPT-4 ChatGPT GPT-3 L2-70B L2-13B L2-7B
putsareal-valuedscore,onecantradeoffaccuracy
H% 46.8% 59.6% 73.6% 66.2% 76.7% 68.3%
onG(i.e.,howoftentrulygroundedreferencesare
labeledG)andH(howoftentrulyhallucinatedref- Table1: Thehallucinationrate(outof1000generated
erences are labeled H) by thresholding the score titles), as determined by ground-truthlabels assigned
toformaGorHclassification. Wevisualizethis usingtheBingsearchAPI.
trade-offusingastandardreceiveroperatingchar-
acteristic(ROC)curve(Fawcett,2006)andsumma- Duetospacelimitations,weshowtheROCand
rizeoveralldetectionperformanceusingthearea FDRcurvesforGPT-4,ChatGPT,andL2-70Band
undertheROCcurve(AUC). deferadditionalLMresultstoAppendixB.
False Discovery Rate (FDR) Curves. Each The ROC curves are shown for each approach
groundednessclassifiercanalsobeusedasafilter andmodelinFigure5. Thesefiguresenableoneto
togeneratealistoflikelygroundedreferencesfora explore different points on this trade off for each
literaturereviewbasedontherawgenerationsofan classifier. For the L2-70B and ChatGPT models,
LM.Asidefromrelevance,whichwedonotstudy the IQ procedure performs best overall as quan-
inthiswork,twoprimaryquantitiesofinteresttoa tified via AUC. For GPT-4 (Figure 5c), both the
userofthisfilterwouldbethefractionofreferences IQ and DQ approaches work well for classifying
preserved (more references provide a more com- hallucinationandgroundednesswiththeIQ(AUC:
prehensive review) and the fraction of preserved 0.878)andDQ1(AUC:0.887)performingthebest.
references which are actually hallucinations. We Theperformanceofeachproceduregenerallyim-
show how these two quantities can be traded off provesasthemodelsizeincreases.
using false discovery rate (FDR) curves. As one Figure 6 shows FDR curves for the three mod-
varies the threshold of G/H classification and re- els. For L2-70B and ChatGPT, the IQ method
turnsonlythosereferencesclassifiedasgrounded, achieves significantly lower FDR and a provides
the FDR captures the fraction of references pro- asubstantiallybetterFDR-preservationratetrade-
ducedwhicharehallucinations. Usersmayhavea offthantheotherapproaches. ForGPT-4,bothIQ
917

IQ, AUC: 0.658 ± 0.04 DQ1, AUC: 0.504 ± 0.00 DQ2, AUC: 0.631 ± 0.04 DQ3, AUC: 0.572 ± 0.02 DQ, AUC: 0.658 ± 0.04 IQ+DQ, AUC: 0.702 ± 0.03
| 1.0            | 1.0 |     | 1.0 | 1.0 | 1.0 | 1.0 |     |
| -------------- | --- | --- | --- | --- | --- | --- | --- |
| ycarucca H 0.8 | 0.8 |     | 0.8 | 0.8 | 0.8 | 0.8 |     |
| 0.6            | 0.6 |     | 0.6 | 0.6 | 0.6 | 0.6 |     |
| 0.4            | 0.4 |     | 0.4 | 0.4 | 0.4 | 0.4 |     |
| 0.2            | 0.2 |     | 0.2 | 0.2 | 0.2 | 0.2 |     |
| 0.0            | 0.0 |     | 0.0 | 0.0 | 0.0 | 0.0 |     |
0.00 0.25 0.50 0.75 1.00 0.00 0.25 0.50 0.75 1.00 0.00 0.25 0.50 0.75 1.00 0.00 0.25 0.50 0.75 1.00 0.00 0.25 0.50 0.75 1.00 0.00 0.25 0.50 0.75 1.00
1 - G accuracy 1 - G accuracy 1 - G accuracy 1 - G accuracy 1 - G accuracy 1 - G accuracy
(a)Llama-2-70b-chat
IQ, AUC: 0.782 ± 0.03 DQ1, AUC: 0.540 ± 0.01 DQ2, AUC: 0.610 ± 0.03 DQ3, AUC: 0.528 ± 0.01 DQ, AUC: 0.624 ± 0.03 IQ+DQ, AUC: 0.792 ± 0.03
| 1.0            | 1.0 |     | 1.0 | 1.0 | 1.0 | 1.0 |     |
| -------------- | --- | --- | --- | --- | --- | --- | --- |
| ycarucca H 0.8 | 0.8 |     | 0.8 | 0.8 | 0.8 | 0.8 |     |
| 0.6            | 0.6 |     | 0.6 | 0.6 | 0.6 | 0.6 |     |
| 0.4            | 0.4 |     | 0.4 | 0.4 | 0.4 | 0.4 |     |
| 0.2            | 0.2 |     | 0.2 | 0.2 | 0.2 | 0.2 |     |
| 0.0            | 0.0 |     | 0.0 | 0.0 | 0.0 | 0.0 |     |
0.00 0.25 0.50 0.75 1.00 0.00 0.25 0.50 0.75 1.00 0.00 0.25 0.50 0.75 1.00 0.00 0.25 0.50 0.75 1.00 0.00 0.25 0.50 0.75 1.00 0.00 0.25 0.50 0.75 1.00
1 - G accuracy 1 - G accuracy 1 - G accuracy 1 - G accuracy 1 - G accuracy 1 - G accuracy
(b)ChatGPT
IQ, AUC: 0.877 ± 0.02 DQ1, AUC: 0.885 ± 0.02 DQ2, AUC: 0.842 ± 0.02 DQ3, AUC: 0.859 ± 0.02 DQ, AUC: 0.915 ± 0.02 IQ+DQ, AUC: 0.927 ± 0.01
| 1.0 | 1.0 |     | 1.0 | 1.0 | 1.0 | 1.0 |     |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 0.8 | 0.8 |     | 0.8 | 0.8 | 0.8 | 0.8 |     |
ycarucca H
| 0.6 | 0.6 |     | 0.6 | 0.6 | 0.6 | 0.6 |     |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 0.4 | 0.4 |     | 0.4 | 0.4 | 0.4 | 0.4 |     |
| 0.2 | 0.2 |     | 0.2 | 0.2 | 0.2 | 0.2 |     |
0.0 0.00 0.25 0.50 0.75 1.00 0.0 0.00 0.25 0.50 0.75 1.00 0.0 0.00 0.25 0.50 0.75 1.00 0.0 0.00 0.25 0.50 0.75 1.00 0.0 0.00 0.25 0.50 0.75 1.00 0.0 0.00 0.25 0.50 0.75 1.00
1 - G accuracy 1 - G accuracy 1 - G accuracy 1 - G accuracy 1 - G accuracy 1 - G accuracy
(c)GPT-4
Figure5: Foreachindividual(IQ,DQ1-3)andensemble(DQ,IQ+DQ)consistencycheck,wedisplaythetrade-off
betweenaccuracyongroundedandhallucinatedreferenceswith95%confidencebandsbasedon100bootstrap
replicatesanda95%confidenceintervalfortheAUCusingtheDeLongetal.(1988)estimateofstandarderror.
andDQmethodsofferlowFDRwithcomparable heuristic is more lenient than exact match, ignor-
| trade-offs. |     |     |     | ingmorethanjustcapitalizationandpunctuation. |     |     |     |
| ----------- | --- | --- | --- | -------------------------------------------- | --- | --- | --- |
However,presumablysinceBingquotedsearchis
| Overall, | IQ appears | to be more | accurate | than |     |     |     |
| -------- | ---------- | ---------- | -------- | ---- | --- | --- | --- |
DQ1-3forChatGPTandL2-70B,whileforGPT-4 designedtofacilitatetitlesearches,itworkswell. 3)
DQ1-3andIQweresimilarlyeffective. Foreach Deceptiveplausibility: Somehallucinationswere
LM,ensemblingfurtherboostsclassificationper- “plausiblesounding”suchasAsurveyonXfortopic
|     |     |     |     | X,evenwhensuchasurveydidnotexist. |     |     | 4)DQ’s |
| --- | --- | --- | --- | --------------------------------- | --- | --- | ------ |
formancewiththeIQ+DQensembleobtainingthe
bestAUCandlowerFDRcurvesforeachLM. falsepositives: Directmethodsmayfailtoidentify
Thecomputecosts,whichinvolve 6.6million hallucinationson“plausiblesounding”titlessuch
|     |     |     | ≈   | assurveysorbookchapters. |     | Theindirectmethod |     |
| --- | --- | --- | --- | ------------------------ | --- | ----------------- | --- |
tokensand$412,arediscussedinSectionD.
alsosometimesfailedtoidentifyahallucinationbe-
causetheLMwouldconsistentlyproducea“likely
6.2 QualitativeFindings
author”basedonthetitle,foragivennon-existent
Aqualitativeexaminationofthetitlesgeneratedby paper. For example, GPT-4 hallucinated the title
theLMsandtheirclassificationsaccordingtothe IntroductiontoOperationsResearchandDecision
BingsearchAPIrevealedseveralinterestingobser-
|     |     |     |     | Making, | but there is a real | book called | Introduc- |
| --- | --- | --- | --- | ------- | ------------------- | ----------- | --------- |
vations: 1)Titlemashups: Manyhallucinatedtitles tiontoOperationsResearch. Inallthreeindirect
werecombinationsofmultipleexistingtitles. For queries, it hallucinated the authors of the exist-
example,ahallucinatedtitle“Privacy-Preserving
ingbook,HillierFrederickS.,LiebermanGerald
Attribute-Based Access Control in Cloud Com- J.. Similarly,forthehallucinatedtitleExploratory
puting" could be “fabricated" from (of the many DataAnalysisandtheRoleofVisualization,2of3
possibilities) existing titles “Privacy-Preserving indirectqueriesproducedJohnW.Tukey,theauthor
Attribute-BasedAccessControlforGridComput-
|     |     |     |     | oftheclassic,ExploratoryDataAnalysis. |     |     | 5)IQ’s |
| --- | --- | --- | --- | ------------------------------------- | --- | --- | ------ |
ing"and“AccessControlinCloudComputing". 2). falsenegatives: Theindirectmethodmaysome-
| Bing’ssearchflexibility: |     | TheBingquotedsearch |     |     |     |     |     |
| ------------------------ | --- | ------------------- | --- | --- | --- | --- | --- |
918

| 0.8 | Llama-2-70b-chat |     | 0.7 | ChatGPT |     | 0.5 | GPT-4 |     |
| --- | ---------------- | --- | --- | ------- | --- | --- | ----- | --- |
IQ
| 0.7 |     |     | 0.6 |     |     | DQ1 |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
0.4
| etar yrevocsid eslaF 0.6 |     |     | etar yrevocsid eslaF |     |     | etar yrevocsid eslaF DQ2 |     |     |
| ------------------------ | --- | --- | -------------------- | --- | --- | ------------------------ | --- | --- |
|                          |     |     | 0.5                  |     |     | DQ3                      |     |     |
0.5
|     |     |     | 0.4 |     |     | 0.3 IQ+DQ |     |     |
| --- | --- | --- | --- | --- | --- | --------- | --- | --- |
0.4
|     |     | IQ  | 0.3 |     | IQ  |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0.3 |     |     |     |     |     | 0.2 |     |     |
|     |     | DQ1 |     |     | DQ1 |     |     |     |
0.2
| 0.2 |     | DQ2   |     |     | DQ2   | 0.1 |     |     |
| --- | --- | ----- | --- | --- | ----- | --- | --- | --- |
|     |     | DQ3   |     |     | DQ3   |     |     |     |
| 0.1 |     |       | 0.1 |     |       |     |     |     |
|     |     | IQ+DQ |     |     | IQ+DQ |     |     |     |
| 0.0 |     |       | 0.0 |     |       | 0.0 |     |     |
0.0 0.2 0.4 0.6 0.8 1.0 0.0 0.2 0.4 0.6 0.8 1.0 0.0 0.2 0.4 0.6 0.8 1.0
Fraction of references preserved Fraction of references preserved Fraction of references preserved
Figure6: Falsediscoveryrate(FDR)vs.fractionofreferencespreservedforeachgroundednessfilterandLM.We
compute95%confidenceintervalsfroma100-replicatebootstrapmean 1.96timesthebootstrapstandarderror.
±
timesfailtoidentifyagroundedpapertitlewhich futurework. 2)Additionalindirectquestions: One
itcanrecognize/generate,asitmaysimplynotbe may improve accuracy by adding more indirect
abletogenerateauthorsnotencodedinitsweights. questionssuchasyearorvenue. Theseposeaddi-
Since,inmanyapplications,identifyingpotential tionalchallengesasapaperwiththesametitleand
hallucinationsismoreimportantthanrecognizing authorsmayoftenappearinmultiplevenues(e.g.,
allgroundedcitations,errorsduetofalselymark- arXiv, a workshop, a conference, and a journal)
inganHasaGarearguablymoreproblematicthan in different years. 3) Generalisability: It would
classifyingaGasanH.Amanualexaminationof be very interesting to see if the methods we em-
120examplesisgiveninAppendixE. ploycouldbeusedtoidentifyothertypesofopen-
|     |     |     |     | domain | hallucinations | beyond | references. | Even |
| --- | --- | --- | --- | ------ | -------------- | ------ | ----------- | ---- |
7 Conclusions
thoughhallucinatedreferencesareoftengivenasa
blatantexampleofhallucination,perhapsduetothe
Open-domainhallucinationisanimportantbutslip-
easewithwhichtheycanbedebunked,theseother
| peryconceptthatisdifficulttomeasure. |     |     | Bystudy- |                                       |     |     |     |         |
| ------------------------------------ | --- | --- | -------- | ------------------------------------- | --- | --- | --- | ------- |
|                                      |     |     |          | typesofhallucinationarealsoimportant. |     |     |     | Follow- |
ingitinthecontextofreferencesusingsearchen-
ingtheinvestigativeinterviewinganalogy,oneway
gineresults,wecanquantitativelycomparehalluci-
toaimtodiscovergeneralhallucinationswouldbe
nationsacrossLMsandwecanalsoquantitatively
toquerytheLMfor“notable,distinguishingdetails”
| comparedifferentblack-boxdetectionmethods. |     |     |     | Of                      |     |     |                   |     |
| ------------------------------------------ | --- | --- | --- | ----------------------- | --- | --- | ----------------- | --- |
|                                            |     |     |     | abouttheiteminquestion. |     |     | Onecouldthenusean |     |
course,forthesolepurposeofdetection,onecould
LMtoestimatetheconsistencybetweenmultiple
achievehigheraccuracybydirectlyconsultingcu-
|                          |     |                    |     | answers. | However,asmentionedforotherdomains |     |     |     |
| ------------------------ | --- | ------------------ | --- | -------- | ---------------------------------- | --- | --- | --- |
| ratedpublicationindexes. |     | However,wehopethat |     |          |                                    |     |     |     |
besidesreferences,itmaybeimpossibletodeter-
| our study | of black-box self-detection |     | of halluci- |     |     |     |     |     |
| --------- | --------------------------- | --- | ----------- | --- | --- | --- | --- | --- |
minewhetherornotagenerationisahallucination
natedreferencesshedslightonthenatureofopen-
withoutaccesstothetrainingset(anduncleareven
domainhallucinationmorebroadly,wheredetect-
withsuchaccess).
| inghallucinationsismorechallenging. |     |     | Itsuggests |     |     |     |     |     |
| ----------------------------------- | --- | --- | ---------- | --- | --- | --- | --- | --- |
thathallucinationisnotentirelyaproblemoftrain-
8 Limitations
ingbutratheronethatcanbeaddressedusingonly
thesameinternalmodelrepresentationwithdiffer- Thereareseverallimitationsofthiswork: 1)Inac-
ent generation procedures. While our direct and cessibletrainingdata: Weconsiderwebasacon-
indirectquerymethodsareonlypartiallyreliable
|     |     |     |     | tendingproxyforthemodels’trainingdata. |     |     |     | How- |
| --- | --- | --- | --- | -------------------------------------- | --- | --- | --- | ---- |
and impractically expensive, we hope they may ever, we cannot conclude what is truly grounded
pavethewaytowardsmoreefficientmethodsthat versus hallucination since we do not have access
generatetextwithfewerhallucinationsandthereby to the training data. 2) Hallucination spectrum:
reducepotentialharmsoflanguagemodels. The notion of hallucination is not entirely black
Thereareseveraldirectionsforfuturework. 1) andwhiteasconsideredinthisworkandinprior
Improveddecodingtechniques: Animportantcon- works. Forexample,ageneratedreferencethatisa
sequenceofourworkistherecognitionthatreduc- substringorsuperstringofanexistingtitleishard
inghallucinationmaybeaproblematgeneration toclassifywiththebinaryscheme. 3)Promptsen-
time. Thus, inventing improved (non-black-box) sitivity: LMs are notoriously sensitive to prompt
generationproceduresisthusacrucialdirectionfor wording (Lu et al., 2022; Jiang et al., 2020; Shin
919

etal.,2020;Gaoetal.,2021). Thus,someofour Tianyu Gao, Adam Fisch, and Danqi Chen. 2021.
Makingpre-trainedlanguagemodelsbetterfew-shot
findingscomparingdirectandindirectqueriesmay
|     |     |     |     |     |     |     | learners. | In Proceedings |     | of  | the 59th | Annual | Meet- |
| --- | --- | --- | --- | --- | --- | --- | --------- | -------------- | --- | --- | -------- | ------ | ----- |
besensitivetothespecificwordingintheprompt.
ingoftheAssociationforComputationalLinguistics
| 4) Domain-specific |     | reference |     | bias: | Since we | use |     |     |     |     |     |     |     |
| ------------------ | --- | --------- | --- | ----- | -------- | --- | --- | --- | --- | --- | --- | --- | --- |
andthe11thInternationalJointConferenceonNatu-
ACMComputingClassificationSystemforourtop- ralLanguageProcessing(Volume1: LongPapers),
| ics,theresultsarebiasedtowardscomputerscience |     |     |     |     |     |     | pages3816–3830. |     |     |     |     |     |     |
| --------------------------------------------- | --- | --- | --- | --- | --- | --- | --------------- | --- | --- | --- | --- | --- | --- |
references,thoughitwouldbestraightforwardto
ZhijiangGuo,MichaelSchlichtkrull,andAndreasVla-
re-runtheprocedureonanygivenlistoftopics. 5) chos.2022. ASurveyonAutomatedFact-Checking.
Genderandracialbiases: LMshavebeenshown TransactionsoftheAssociationforComputational
toexhibitgenderandracialbiases(Swingeretal., Linguistics,10:178–206.
2019)whichmaybereflectedinourprocedure–in Kelvin Guu, Albert Webson, Ellie Pavlick, Lucas
particular: ourproceduremaynotrecognizecertain Dixon, Ian Tenney, and Tolga Bolukbasi. 2023.
namesaslikelyauthors,oritmayperformworseat Simfluence: Modeling the Influence of Individual
|     |     |     |     |     |     |     | Training | Examples | by  | Simulating |     | Training | Runs. |
| --- | --- | --- | --- | --- | --- | --- | -------- | -------- | --- | ---------- | --- | -------- | ----- |
matchingnamesofpeopleincertainracialgroups
ArXiv:2303.08114[cs].
| wherethereislessvariabilityinnames. |     |     |     |     | Sinceour |     |     |     |     |     |     |     |     |
| ----------------------------------- | --- | --- | --- | --- | -------- | --- | --- | --- | --- | --- | --- | --- | --- |
workcomparesLMsandhallucinationestimation ZiweiJi,NayeonLee,RitaFrieske,TiezhengYu,Dan
|     |     |     |     |     |     |     | Su, Yan | Xu, | Etsuko | Ishii, | Ye Jin | Bang, Andrea |     |
| --- | --- | --- | --- | --- | --- | --- | ------- | --- | ------ | ------ | ------ | ------------ | --- |
procedures,theriskislowercomparedtoasystem
|            |     |          |       |                |     |     | Madotto,   | and        | Pascale | Fung.    | 2023.       | Survey of | Hal- |
| ---------- | --- | -------- | ----- | -------------- | --- | --- | ---------- | ---------- | ------- | -------- | ----------- | --------- | ---- |
| that might | be  | deployed | using | our procedures |     | to  |            |            |         |          |             |           |      |
|            |     |          |       |                |     |     | lucination | in Natural |         | Language | Generation. |           | ACM  |
reduce hallucination. Before deploying any such ComputingSurveys,55(12):1–38.
system,oneshouldperformamorethoroughexam-
ZhengbaoJiang,FrankFXu,JunAraki,andGraham
inationofpotentialbiasesagainstsensitivegroups
|     |     |     |     |     |     |     | Neubig. | 2020. | How | can we | know | what language |     |
| --- | --- | --- | --- | --- | --- | --- | ------- | ----- | --- | ------ | ---- | ------------- | --- |
andaccuracyacrossdifferentresearchareas. modelsknow? TransactionsoftheAssociationfor
ComputationalLinguistics,8:423–438.
SauravKadavath,TomConerly,AmandaAskell,Tom
References
|     |     |     |     |     |     |     | Henighan, | Dawn | Drain, | Ethan | Perez, | Nicholas |     |
| --- | --- | --- | --- | --- | --- | --- | --------- | ---- | ------ | ----- | ------ | -------- | --- |
SaiAnirudhAthaluri,SandeepVarmaManthena,VS Schiefer,ZacHatfield-Dodds,NovaDasSarma,Eli
RKrishnaManojKesapragada,VineelYarlagadda, Tran-Johnson, Scott Johnston, Sheer El-Showk,
TirthDave,andRamaTulasiSiriDuddumpudi.2023. Andy Jones, Nelson Elhage, Tristan Hume, Anna
ExploringtheBoundariesofReality: Investigating Chen, Yuntao Bai, Sam Bowman, Stanislav Fort,
thePhenomenonofArtificialIntelligenceHallucina-
|     |     |     |     |     |     |     | Deep Ganguli, |     | Danny | Hernandez, |     | Josh Jacobson, |     |
| --- | --- | --- | --- | --- | --- | --- | ------------- | --- | ----- | ---------- | --- | -------------- | --- |
tioninScientificWritingThroughChatGPTRefer- JacksonKernion,ShaunaKravec,LianeLovitt,Ka-
| ences. | Cureus. |     |     |     |     |     | malNdousse,CatherineOlsson,SamRinger,Dario |     |     |     |     |     |     |
| ------ | ------- | --- | --- | --- | --- | --- | ------------------------------------------ | --- | --- | --- | --- | --- | --- |
Amodei,TomBrown,JackClark,NicholasJoseph,
Amos Azaria and Tom Mitchell. 2023. The In- BenMann,SamMcCandlish,ChrisOlah,andJared
ternal State of an LLM Knows When its Lying. Kaplan. 2022. Language Models (Mostly) Know
ArXiv:2304.13734[cs].
|           |         |       |                 |     |       |     | WhatTheyKnow. |     | ArXiv:2207.05221[cs]. |     |     |     |     |
| --------- | ------- | ----- | --------------- | --- | ----- | --- | ------------- | --- | --------------------- | --- | --- | --- | --- |
| Sébastien | Bubeck, | Varun | Chandrasekaran, |     | Ronen | El- |               |     |                       |     |     |     |     |
StephanieLin,JacobHilton,andOwainEvans.2022.
| dan,  | Johannes | Gehrke, | Eric           | Horvitz, | Ece   | Kamar, |                              |        |     |         |       |             |     |
| ----- | -------- | ------- | -------------- | -------- | ----- | ------ | ---------------------------- | ------ | --- | ------- | ----- | ----------- | --- |
|       |          |         |                |          |       |        | Teaching                     | Models | to  | Express | Their | Uncertainty | in  |
| Peter | Lee,     | Yin Tat | Lee, Yuanzhi   | Li,      | Scott | Lund-  |                              |        |     |         |       |             |     |
|       |          |         |                |          |       |        | Words. ArXiv:2205.14334[cs]. |        |     |         |       |             |     |
| berg, | Harsha   | Nori,   | Hamid Palangi, |          | Marco | Tulio  |                              |        |     |         |       |             |     |
Ribeiro, and Yi Zhang. 2023. Sparks of Artificial YaoLu,MaxBartolo,AlastairMoore,SebastianRiedel,
GeneralIntelligence: EarlyexperimentswithGPT-4. and Pontus Stenetorp. 2022. Fantastically ordered
ArXiv:2303.12712[cs]. promptsandwheretofindthem: Overcomingfew-
|     |     |     |     |     |     |     | shotpromptordersensitivity. |     |     |     | InProceedingsofthe |     |     |
| --- | --- | --- | --- | --- | --- | --- | --------------------------- | --- | --- | --- | ------------------ | --- | --- |
ElizabethRDeLong,DavidMDeLong,andDanielL
60thAnnualMeetingoftheAssociationforCompu-
| Clarke-Pearson.                                |     | 1988.                   | Comparing | the | areas       | under |                                               |     |     |               |                   |           |     |
| ---------------------------------------------- | --- | ----------------------- | --------- | --- | ----------- | ----- | --------------------------------------------- | --- | --- | ------------- | ----------------- | --------- | --- |
|                                                |     |                         |           |     |             |       | tationalLinguistics(Volume1:                  |     |     |               | LongPapers),pages |           |     |
| twoormorecorrelatedreceiveroperatingcharacter- |     |                         |           |     |             |       | 8086–8098.                                    |     |     |               |                   |           |     |
| isticcurves:                                   |     | anonparametricapproach. |           |     | Biometrics, |       |                                               |     |     |               |                   |           |     |
| pages837–845.                                  |     |                         |           |     |             |       | PotsaweeManakul,AdianLiusie,andMarkJ.F.Gales. |     |     |               |                   |           |     |
|                                                |     |                         |           |     |             |       | 2023. SelfCheckGPT:                           |     |     | Zero-Resource |                   | Black-Box |     |
Owain Evans, Owen Cotton-Barratt, Lukas Finnve- Hallucination Detection for Generative Large Lan-
den,AdamBales,AvitalBalwit,PeterWills,Luca
|           |     |         |           |       |          |     | guageModels. |     | ArXiv:2303.08896[cs]. |     |     |     |     |
| --------- | --- | ------- | --------- | ----- | -------- | --- | ------------ | --- | --------------------- | --- | --- | --- | --- |
| Righetti, | and | William | Saunders. | 2021. | Truthful |     |              |     |                       |     |     |     |     |
AI:DevelopingandgoverningAIthatdoesnotlie. MaryLMcHugh.2012. Interraterreliability: thekappa
ArXiv:2110.06674[cs]. statistic. Biochemiamedica,22(3):276–282.
Tom Fawcett. 2006. An introduction to roc analysis. SaraMerken.2023. Newyorklawyerssanctionedfor
Patternrecognitionletters,27(8):861–874. usingfakechatgptcasesinlegalbrief. Reuters.
920

OpenAI. 2023. GPT-4 Technical Report. linkasshowninTable2. Forconsistency,thehu-
ArXiv:2303.08774[cs].
manlabelersalsoagreedonthelabelsforthefour
exemplarsshowninFigure8.
LongOuyang,JeffWu,XuJiang,DiogoAlmeida,Car-
rollL.Wainwright,PamelaMishkin,ChongZhang, Weshowinter-raterreliabilityagreementcom-
SandhiniAgarwal,KatarinaSlama,AlexRay,John putedusingCohen’sκscore(McHugh,2012)be-
Schulman,JacobHilton,FraserKelton,LukeMiller, tweenthelabelersandtheautomatedBinglabels
| Maddie           | Simens, | Amanda |        | Askell,  | Peter | Welinder, |          |                |             |     |              |
| ---------------- | ------- | ------ | ------ | -------- | ----- | --------- | -------- | -------------- | ----------- | --- | ------------ |
|                  |         |        |        |          |       |           | in Table | 3. The results | demonstrate |     | that the au- |
| Paul Christiano, |         | Jan    | Leike, | and Ryan | Lowe. | 2022.     |          |                |             |     |              |
Traininglanguagemodelstofollowinstructionswith tomatedlabelinggeneratedviaBingsearchexact
|                |     |                       |     |     |     |     | match reliably | matches | the | judgments | of human |
| -------------- | --- | --------------------- | --- | --- | --- | --- | -------------- | ------- | --- | --------- | -------- |
| humanfeedback. |     | ArXiv:2203.02155[cs]. |     |     |     |     |                |         |     |           |          |
experts.
| BernardRous.2012.  |     | MajorupdatetoACM’sComput- |     |                |     |        |                                    |     |     |     |     |
| ------------------ | --- | ------------------------- | --- | -------------- | --- | ------ | ---------------------------------- | --- | --- | --- | --- |
| ing Classification |     | System.                   |     | Communications |     | of the |                                    |     |     |     |     |
|                    |     |                           |     |                |     |        | B SupplementaryExperimentalDetails |     |     |     |     |
ACM,55(11):12.
WeshowROCandFDRmetricsforL2-13B,L2-
| Taylor Shin, | Yasaman |     | Razeghi, | Robert | L Logan | IV, |     |     |     |     |     |
| ------------ | ------- | --- | -------- | ------ | ------- | --- | --- | --- | --- | --- | --- |
EricWallace,andSameerSingh.2020. Autoprompt: 7B and GPT-3 models in Figure 9 and Figure 10
Elicitingknowledgefromlanguagemodelswithau-
|     |     |     |     |     |     |     | respectively. | We find | that the | procedures | are not |
| --- | --- | --- | --- | --- | --- | --- | ------------- | ------- | -------- | ---------- | ------- |
tomaticallygeneratedprompts. InProceedingsofthe effective in detecting hallucinations, performing
2020ConferenceonEmpiricalMethodsinNatural
theworstfortheL2-7B.ThoughIQhelpsthemost
LanguageProcessing(EMNLP),pages4222–4235.
|     |     |     |     |     |     |     | for GPT-3, | DQ2 approach | helps | the most | for L2- |
| --- | --- | --- | --- | --- | --- | --- | ---------- | ------------ | ----- | -------- | ------- |
Aarohi Srivastava, Abhinav Rastogi, Abhishek Rao, 13B and L2-7B. Consistent with our findings of
AbuAwalMdShoeb,AbubakarAbid,AdamFisch,
othermodels,IQ+DQensembleapproachperforms
| Adam | R. Brown, | Adam |     | Santoro, | Aditya | Gupta, |     |     |     |     |     |
| ---- | --------- | ---- | --- | -------- | ------ | ------ | --- | --- | --- | --- | --- |
thebest.
| Adrià | Garriga-Alonso, |     | Agnieszka |     | Kluska, | Aitor |     |     |     |     |     |
| ----- | --------------- | --- | --------- | --- | ------- | ----- | --- | --- | --- | --- | --- |
Lewkowycz,AkshatAgarwal,AletheaPower,Alex
|     |     |     |     |     |     |     | C LicensesandTermsofUse |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | ----------------------- | --- | --- | --- | --- |
Ray,AlexWarstadt,AlexanderW.Kocurek,...(421-
| others), | and Ziyi | Wu. | 2022. | Beyond | the | imitation |     |     |     |     |     |
| -------- | -------- | --- | ----- | ------ | --- | --------- | --- | --- | --- | --- | --- |
game: Quantifyingandextrapolatingthecapabilities AccordingtotheOpenAItermsofuseSharingand
|     |     |     |     |     |     |     | Publicationpolicy,11 |     | they“welcomeresearchpub- |     |     |
| --- | --- | --- | --- | --- | --- | --- | -------------------- | --- | ------------------------ | --- | --- |
oflanguagemodels.
|     |     |     |     |     |     |     | lications | related to the | OpenAI | API.” | Following |
| --- | --- | --- | --- | --- | --- | --- | --------- | -------------- | ------ | ----- | --------- |
Nathaniel Swinger, Maria De-Arteaga, Neil Thomas Information12,
|     |     |     |     |     |     |     | the Bing | Search API | Legal |     | we do |
| --- | --- | --- | --- | --- | --- | --- | -------- | ---------- | ----- | --- | ----- |
HeffernanIV,MarkDMLeiserson,andAdamTau-
manKalai.2019. Whatarethebiasesinmyword notstoretheresultsofthesearchqueriesbutrather
embedding? InProceedingsofthe2019AAAI/ACM only whether or not there were any results. Ac-
| Conference | on  | AI, Ethics, |     | and Society, | pages | 305– |     |     |     |     |     |
| ---------- | --- | ----------- | --- | ------------ | ----- | ---- | --- | --- | --- | --- | --- |
cordingtotheACM,13“ThefullCCSclassification
311.
treeisfreelyavailableforeducationalandresearch
|               |     |       |         |       |        |           | purposes.” | (Thissectionwillbeincludedwithany |     |     |     |
| ------------- | --- | ----- | ------- | ----- | ------ | --------- | ---------- | --------------------------------- | --- | --- | --- |
| Hugo Touvron, |     | Louis | Martin, | Kevin | Stone, | Peter Al- |            |                                   |     |     |     |
bert, Amjad Almahairi, Yasmine Babaei, Nikolay publishedversionofourpaper.)
Bashlykov,SoumyaBatra,PrajjwalBhargava,Shruti
| Bhosale,          | et         | al. 2023. | Llama        | 2:  | Open  | founda-  |                                        |     |     |              |     |
| ----------------- | ---------- | --------- | ------------ | --- | ----- | -------- | -------------------------------------- | --- | --- | ------------ | --- |
|                   |            |           |              |     |       |          | D ComputationandCost                   |     |     |              |     |
| tion and          | fine-tuned |           | chat models. |     | arXiv | preprint |                                        |     |     |              |     |
| arXiv:2307.09288. |            |           |              |     |       |          | WeuseOpenAIAPIforrunningtheexperiments |     |     |              |     |
|                   |            |           |              |     |       |          | onGPT-4,ChatGPTandGPT-3.               |     |     | Weshowtheav- |     |
AnneliesVredeveldt,PeterJ.vanKoppen,andPärAn-
eragetokensconsumedforpromptandcompletion
| ders Granhag. |     | 2014. | The | Inconsistent | Suspect: | A   |     |     |     |     |     |
| ------------- | --- | ----- | --- | ------------ | -------- | --- | --- | --- | --- | --- | --- |
SystematicReviewofDifferentTypesofConsistency foreachoftheapproachesanddatagenerationper
| inTruthTellersandLiars. |     |     | InRayBull,editor,Inves- |     |     |     |                             |     |     |               |     |
| ----------------------- | --- | --- | ----------------------- | --- | --- | --- | --------------------------- | --- | --- | ------------- | --- |
|                         |     |     |                         |     |     |     | candidatequeryinTables4to6. |     |     | Weestimatethe |     |
tigativeInterviewing,pages183–207.Springer,New
|     |     |     |     |     |     |     | cost based | on the pricing | details | available | as of |
| --- | --- | --- | --- | --- | --- | --- | ---------- | -------------- | ------- | --------- | ----- |
York,NY.
|     |     |     |     |     |     |     | May2023.14 | ForGPT-4,around2.2Mtokenswere |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | ---------- | ----------------------------- | --- | --- | --- |
Ludwig Wittgenstein. 1953. Philosophical Investiga- usedamountingtoroughly$74toevaluateallap-
tions. Wiley-Blackwell,NewYork,NY,USA.
|     |     |     |     |     |     |     | proaches.                 | ForChatGPT,around2.3Mtokenswere |     |                 |     |
| --- | --- | --- | --- | --- | --- | --- | ------------------------- | ------------------------------- | --- | --------------- | --- |
|     |     |     |     |     |     |     | usedamountingtoroughly$5. |                                 |     | ForGPT-3,around |     |
A BingSearchReliability
11https://openai.com/policies/
Beforeassigningmanualgroundedorhallucination sharing-publication-policy
12https://www.microsoft.com/en-us/bing/
| labels to | each  | reference        | title, | each  | expert | annota-   |            |     |     |     |     |
| --------- | ----- | ---------------- | ------ | ----- | ------ | --------- | ---------- | --- | --- | --- | --- |
| tor was   | given | the instructions |        | shown | in     | Figure 7. | apis/legal |     |     |     |     |
13https://www.acm.org/publications/
Alongwithagivenreferencetitle,theannotators
class-2012
wereprovidedwithacorrespondingGooglesearch 14https://openai.com/pricing
921

|     | Figure7: | Labelinginstructionsshowntotheexperthumanannotators. |     |     |     |     |     |     |     |
| --- | -------- | ---------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
Table2: Sampleof2titlesoutof100titlesgiventotheexperthumanannotatorsforlabeling.
|     |     |     | ReferenceTitle |     |     |     | SearchUrl | (H/G) |     |
| --- | --- | --- | -------------- | --- | --- | --- | --------- | ----- | --- |
IntroductiontoAutonomousRobots:Mechanisms,Sensors,Actuators,andAlgorithms link ?
|     | TimingAwarePlacementandRoutinginFPGAs |     |     |     |     |     | link |     | ?   |
| --- | ------------------------------------- | --- | --- | --- | --- | --- | ---- | --- | --- |
Figure8: Exemplarlabelsuponwhichallexperthumanannotatorsagreedpriortoassigningmanuallabels.
2.1Mtokenswereusedamountingtoroughly$258. E ExamplesofHallucinationsand
| ForBingSearch,weuseanS1instanceoftheBing |     |     |     | References |     |     |     |     |     |
| ---------------------------------------- | --- | --- | --- | ---------- | --- | --- | --- | --- | --- |
SearchAPI15.Wemade3,000queriesinalltothis
Tables7to10eachdisplayacarefulinspectionof
| endpointamountingto$75. |                          | Summingthesecosts |     |           |           |     |              |            |      |
| ----------------------- | ------------------------ | ----------------- | --- | --------- | --------- | --- | ------------ | ---------- | ---- |
|                         |                          |                   |     | 30 random | candidate |     | paper titles | classified | as H |
| givesatotalof$412.      | Thecomputerequirementsof |                   |     |           |           |     |              |            |      |
andGasdeterminedbywhethertheBingSearch
| combiningtheseresultswerenegligible. |     |     | Whilethe |                        |     |     |                      |     |     |
| ------------------------------------ | --- | --- | -------- | ---------------------- | --- | --- | -------------------- | --- | --- |
|                                      |     |     |          | APIreturnedanyresults. |     |     | Amanualsearchforeach |     |     |
exactmodelsizesandfloatingpointoperationsare
|              |           |           |                   | suggested | title | indicated | that the | vast majority | of  |
| ------------ | --------- | --------- | ----------------- | --------- | ----- | --------- | -------- | ------------- | --- |
| not publicly | available | for these | models, the total |           |       |           |          |               |     |
Hsareinfacthallucinationsandthevastmajority
costgivesaroughideaontheorderofmagnitudeof
|     |     |     |     | ofGsareinfactrealreferences. |     |     |     | Weshowthetitles |     |
| --- | --- | --- | --- | ---------------------------- | --- | --- | --- | --------------- | --- |
computationrequiredincomparisontothehourly
classifiedasHbyBingsearchalongwithclosest
costof,say,aGPUontheAzureplatform.
manuallydiscoveredmatchforChatGPT(Table7)
| For running | the experiments |     | on Llama-2-chat |           |        |     |         |            |         |
| ----------- | --------------- | --- | --------------- | --------- | ------ | --- | ------- | ---------- | ------- |
|             |                 |     |                 | and GPT-4 | (Table | 9). | We show | the titles | classi- |
series,weusedanodewith8V100GPUs.
fiedasGbyBingsearchalongwiththeweblinks
|     |     |     |     | to the matched |     | titles for | ChatGPT | (Table | 8) and |
| --- | --- | --- | --- | -------------- | --- | ---------- | ------- | ------ | ------ |
15https://www.microsoft.com/en-us/bing/
| apis/pricing |     |     |     | GPT-4(Table10). |     | Wealsolistthescoreassigned |     |     |     |
| ------------ | --- | --- | --- | --------------- | --- | -------------------------- | --- | --- | --- |
922

IQ, AUC: 0.517 ± 0.03 DQ1, AUC: 0.500 ± nan DQ2, AUC: 0.574 ± 0.03 DQ3, AUC: 0.501 ± 0.01 DQ, AUC: 0.573 ± 0.03 IQ+DQ, AUC: 0.575 ± 0.04
| 1.0            | 1.0 | 1.0 | 1.0 | 1.0 | 1.0 |
| -------------- | --- | --- | --- | --- | --- |
| ycarucca H 0.8 | 0.8 | 0.8 | 0.8 | 0.8 | 0.8 |
| 0.6            | 0.6 | 0.6 | 0.6 | 0.6 | 0.6 |
| 0.4            | 0.4 | 0.4 | 0.4 | 0.4 | 0.4 |
| 0.2            | 0.2 | 0.2 | 0.2 | 0.2 | 0.2 |
| 0.0            | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 |
0.00 0.25 0.50 0.75 1.00 0.00 0.25 0.50 0.75 1.00 0.00 0.25 0.50 0.75 1.00 0.00 0.25 0.50 0.75 1.00 0.00 0.25 0.50 0.75 1.00 0.00 0.25 0.50 0.75 1.00
1 - G accuracy 1 - G accuracy 1 - G accuracy 1 - G accuracy 1 - G accuracy 1 - G accuracy
(a)Llama-2-7b-chat
IQ, AUC: 0.657 ± 0.04 DQ1, AUC: 0.500 ± nan DQ2, AUC: 0.686 ± 0.04 DQ3, AUC: 0.546 ± 0.03 DQ, AUC: 0.696 ± 0.04 IQ+DQ, AUC: 0.723 ± 0.04
| 1.0            | 1.0 | 1.0 | 1.0 | 1.0 | 1.0 |
| -------------- | --- | --- | --- | --- | --- |
| ycarucca H 0.8 | 0.8 | 0.8 | 0.8 | 0.8 | 0.8 |
| 0.6            | 0.6 | 0.6 | 0.6 | 0.6 | 0.6 |
| 0.4            | 0.4 | 0.4 | 0.4 | 0.4 | 0.4 |
| 0.2            | 0.2 | 0.2 | 0.2 | 0.2 | 0.2 |
| 0.0            | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 |
0.00 0.25 0.50 0.75 1.00 0.00 0.25 0.50 0.75 1.00 0.00 0.25 0.50 0.75 1.00 0.00 0.25 0.50 0.75 1.00 0.00 0.25 0.50 0.75 1.00 0.00 0.25 0.50 0.75 1.00
1 - G accuracy 1 - G accuracy 1 - G accuracy 1 - G accuracy 1 - G accuracy 1 - G accuracy
(b)Llama-2-13b-chat
IQ, AUC: 0.695 ± 0.03 DQ1, AUC: 0.555 ± 0.03 DQ2, AUC: 0.588 ± 0.03 DQ3, AUC: 0.534 ± 0.02 DQ, AUC: 0.621 ± 0.04 IQ+DQ, AUC: 0.710 ± 0.04
| 1.0 | 1.0 | 1.0 | 1.0 | 1.0 | 1.0 |
| --- | --- | --- | --- | --- | --- |
| 0.8 | 0.8 | 0.8 | 0.8 | 0.8 | 0.8 |
ycarucca H
| 0.6 | 0.6 | 0.6 | 0.6 | 0.6 | 0.6 |
| --- | --- | --- | --- | --- | --- |
| 0.4 | 0.4 | 0.4 | 0.4 | 0.4 | 0.4 |
| 0.2 | 0.2 | 0.2 | 0.2 | 0.2 | 0.2 |
0.0 0.00 0.25 0.50 0.75 1.00 0.0 0.00 0.25 0.50 0.75 1.00 0.0 0.00 0.25 0.50 0.75 1.00 0.0 0.00 0.25 0.50 0.75 1.00 0.0 0.00 0.25 0.50 0.75 1.00 0.0 0.00 0.25 0.50 0.75 1.00
1 - G accuracy 1 - G accuracy 1 - G accuracy 1 - G accuracy 1 - G accuracy 1 - G accuracy
(c)GPT-3
Figure9: ROCCurvesfortheIQandDQapproachesalongwiththeensembleapproaches
| by the IQ method       | for all the sampled | candidate |     |     |     |
| ---------------------- | ------------------- | --------- | --- | --- | --- |
| titles. Interestingly, | for both models     | there was | a   |     |     |
caseinwhichtheIQmethodassignedthescoreof
| 1toanHtitle.                    | TheseHtitleswereDesignandIm- |               |                                                    |     |     |
| ------------------------------- | ---------------------------- | ------------- | -------------------------------------------------- | --- | --- |
|                                 |                              |               | Table3: Cohen’sκmeasureofinter-raterreliabilitybe- |     |     |
| plementationofDigitalLibraries: |                              | Technological |                                                    |     |     |
tweeneachpairofexperthumanevaluatorsandbetween
Challenges and Solutions for ChatGPT (Table 7) eachexpertandtheautomatedBinglabelingdescribed
| andEnterpriseModeling: | TacklingBusinessChal- |     |               |                       |           |
| ---------------------- | --------------------- | --- | ------------- | --------------------- | --------- |
|                        |                       |     | inSection5.2. | TherangeofCohen’sκis[ | 1,1]witha |
−
lengeswiththe4EMApproachforGPT-4(Table9). valueof1indicatingperfectagreement. Avalueabove
0.9isconsidered”almostperfect”agreement(McHugh,
Inbothofthesecases,thetitleswereverysimilar
| totheclosestmanuallydiscoveredmatchedtitles |     |     | 2012). |     |     |
| ------------------------------------------- | --- | --- | ------ | --- | --- |
-DesignandImplementationofDigitalLibraries
Cohen’skappa(κ)
andEnterpriseModelingwith4EM:Perspectives
andMethod,respectively.
|     |     |     | personAandpersonB |     | 0.96 |
| --- | --- | --- | ----------------- | --- | ---- |
|     |     |     | personAandpersonC |     | 0.98 |
0.98
personBandpersonC
|     |     |     | personDandpersonA |     | 0.96 |
| --- | --- | --- | ----------------- | --- | ---- |
|     |     |     | personDandpersonB |     | 1.0  |
|     |     |     | personDandpersonC |     | 0.98 |
|     |     |     | personAandBing    |     | 0.98 |
|     |     |     | personBandBing    |     | 0.98 |
|     |     |     | personCandBing    |     | 1.0  |
|     |     |     | personDandBing    |     | 0.98 |
923

|     | Llama-2-7b-chat |     |     | Llama-2-13b-chat |     |     | Text-davinci-003 |     |
| --- | --------------- | --- | --- | ---------------- | --- | --- | ---------------- | --- |
| 0.8 |                 |     |     |                  |     | 0.9 |                  |     |
0.8
0.8
0.7
| etar yrevocsid eslaF |     |     | etar yrevocsid eslaF 0.7 |     |     | etar yrevocsid eslaF 0.7 |     |     |
| -------------------- | --- | --- | ------------------------ | --- | --- | ------------------------ | --- | --- |
| 0.6                  |     |     | 0.6                      |     |     | 0.6                      |     |     |
0.5
| 0.5 |     |     | 0.5 |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
0.4
|     |     | IQ    | 0.4 |     | IQ    |     |     | IQ    |
| --- | --- | ----- | --- | --- | ----- | --- | --- | ----- |
| 0.4 |     | DQ1   |     |     | DQ1   | 0.3 |     | DQ1   |
|     |     | DQ2   | 0.3 |     | DQ2   | 0.2 |     | DQ2   |
|     |     | DQ3   |     |     | DQ3   |     |     | DQ3   |
| 0.3 |     |       | 0.2 |     |       |     |     |       |
|     |     | IQ+DQ |     |     | IQ+DQ | 0.1 |     | IQ+DQ |
0.2 0.0 0.2 0.4 0.6 0.8 1.0 0.1 0.0 0.2 0.4 0.6 0.8 1.0 0.0 0.0 0.2 0.4 0.6 0.8 1.0
Fraction of references preserved Fraction of references preserved Fraction of references preserved
Figure10: Falsediscoveryrate(FDR)vs.fractionofreferencespreservedforeachgroundednessfilterandLM.
Thepreservationrateindicatesthefractionofreferencespreservedwhenagroundednessfilterisappliedtotheraw
generationsofaLM.TheFDRrepresentsthefractionofpreservedreferencesthatareactuallyhallucinations. For
unachievablevaluesofthefractionofreferencespreserved(belowtheminimalfractionachievablebythresholding),
weextrapolateeachcurvebyuniformlysubsamplingreferenceswithmaximalscores. Wecompute95%confidence
intervalsfroma100-replicatebootstrapmean 1.96timesthebootstrapstandarderror.
±
|     |     | Table4: | GPT-4: Averagenumberoftokensconsumed |       |       |             |     |     |
| --- | --- | ------- | ------------------------------------ | ----- | ----- | ----------- | --- | --- |
|     |     |         | DS                                   | IQ    | DQ1   | DQ2 DQ3     |     |     |
|     |     |         | 40.1                                 | 443.4 | 221.2 | 299.6 946.1 |     |     |
Prompt
|     |     | Completion | 64.8                                  | 140.1 | 67.2        | 12.2 30.3 |     |     |
| --- | --- | ---------- | ------------------------------------- | ----- | ----------- | --------- | --- | --- |
|     |     | Table5:    | ChatGPT:Averagenumberoftokensconsumed |       |             |           |     |     |
|     |     |            | DS                                    | IQ    | DQ1 DQ2     | DQ3       |     |     |
|     |     | Prompt     | 40.1                                  | 437.3 | 224.1 302.2 | 1009.6    |     |     |
|     |     |            | 71.8                                  | 144.9 | 28.8        | 45.5 75.8 |     |     |
Completion
|     |     | Table6:    | GPT-3: Averagenumberoftokensconsumed |        |        |             |     |     |
| --- | --- | ---------- | ------------------------------------ | ------ | ------ | ----------- | --- | --- |
|     |     |            | DS                                   | IQ     | DQ1    | DQ2 DQ3     |     |     |
|     |     | Prompt     | 39.7                                 | 399.53 | 232.36 | 332.4 995.1 |     |     |
|     |     | Completion | 68.4                                 | 90.6   | 30.3   | 21.8 30.4   |     |     |
924

Table7: ReferencetitlesclassifiedasH(hallucination)byBinggeneratedfromChatGPT.30randomlysampled
titlesareshown.
Referencetitlegenerated(ClosestMatch,iffound) IQProb
Quantumsensingforhealthcare(NA) 0
ChallengesandSolutionsinManagingElectronicRecordsinStorageSystems(ElectronicRecords 0
ManagementChallenges)
HardwareVerificationUsingPhysicalDesignTechniques(NA) 0
A Framework for Verifying Recursive Programs with Pointers using Automata over Infinite Trees 0
(Verificationofrecursivemethodsontree-likedatastructures)
RobustControlforNonlinearTime-DelaySystemswithFaults(RobustControlforNonlinearTime- 0
DelaySystems)
IntelligentSchedulingforAutonomousUAVsusingDiscreteArtificialIntelligencePlanningTechniques 0
(NA)
AnOverviewofDatabaseManagementSystemEnginesforDistributedComputing(NA) 0
TheAestheticsofDigitalArtsandMedia(VOICE:VocalAestheticsinDigitalArtsandMedia) 0
ImprovingHuman-RobotTeamPerformancethroughIntegratedTaskPlanningandSchedulingina 0
ComplexEnvironment(Improvedhuman–robotteamperformancethroughcross-training,anapproach
inspiredbyhumanteamtrainingpractices)
WebApplicationSecurity:FromConcepttoPractice(WebApplicationSecurity) 0
A28nmhigh-densityandlow-powerstandardcelllibrarywithhalf-VDDpower-gatingcells(NA) 0
AnAcousticInterfaceforTouchlessHuman-ComputerInteraction(NA) 0
AdvancesinSolidStateLasersDevelopmentandApplications: Proceedingsofthe42ndPolishCon- 0
ference on Laser Technology and Applications (Advances in Solid State Lasers Development and
Applications)
Designingmobileinformationsystemsforhealthcare(DesignandImplementationofMobile-Based 0
TechnologyinStrengtheningHealthInformationSystem)
Fault-toleranceandReliabilityTechniquesforDependableDistributedSystems(ReliabilityandReplica- 0
tionTechniquesforImprovedFaultToleranceinDistributedSystems)
Cyber-physicalsystems:ASurveyandFutureResearchDirectionsonSensorandActuatorIntegration 0
(Cyber-physicalsystems:Asurvey)
Performanceevaluationofwirelesssensornetworksusingnetworksimulator-3(NA) 0
Communication-BasedDesignforVLSICircuitsandSystems(NA) 0
DigitalMedia:TheIntersectionofArtandTechnology(NA) 0
Towardatool-supportedsoftwareevolutionmethodology(NA) 0
Performanceevaluationoftemperature-awareroutingprotocolsinwirelesssensornetworks(Performance 0
EvaluationofRoutingProtocolsinWirelessSensorNetworks)
Computer-managedinstructionandstudentlearningoutcomes:ameta-analysis(EffectsofComputer- 0
AssistedInstructiononCognitiveOutcomes:AMeta-Analysis)
AnEmpiricalAnalysisofEnterpriseResourcePlanning(ERP)SystemsImplementationinService 0
OrganizationsinJordan(ContributionsofERPSystemsinJordan)
Optimizationofproductionplanninginconsumerproductsindustry(Optimizingproductionplanningat 0.01
aconsumergoodscompany)
EfficientTextDocumentRetrievalUsinganInvertedIndexwithCacheEnhancement(NA) 0.11
ServiceOAMinCarrierEthernetNetworks 0.13
IntroductiontoLogic:AbstractioninContemporaryLogic(IntroductiontoLogic) 0.17
QueryProcessingandOptimizationforInformationRetrievalSystems(QueryOptimizationinInforma- 0.33
tionRetrieval)
Cross-PlatformVerificationofWebApplications(Cross-platformfeaturematchingforwebapplications) 0.33
DesignandImplementationofDigitalLibraries:TechnologicalChallengesandSolutions(Designand 1
ImplementationofDigitalLibraries)
925

Table8: ReferencetitlesclassifiedasG(grounded)byBing,generatedfromChatGPT.30randomlysampledtitles
areshown.
| Referencetitlegenerated(Matchedtitle)                |                                    | IQProb |
| ---------------------------------------------------- | ---------------------------------- | ------ |
| JavaScript:                                          | TheGoodParts(exactmatch)           | 1      |
| EssentialsofManagementInformationSystems(exactmatch) |                                    | 1      |
| VisualizationAnalysisandDesign(exactmatch)           |                                    | 1      |
| Forecasting:                                         | MethodsandApplications(exactmatch) | 1      |
| PythonforDataAnalysis(exactmatch)                    |                                    | 1      |
IntroductiontoParallelAlgorithmsandArchitectures: ArraysTreesHypercubes 1
(exactmatch)
Linearlogicanditsapplications(TemporalLinearLogicandItsApplications) 1
| CodingandInformationTheory(exactmatch)     |     | 1   |
| ------------------------------------------ | --- | --- |
| IntroductiontoElectricCircuits(exactmatch) |     | 1   |
ConcurrentProgramminginJava: DesignPrinciplesandPatterns(exactmatch) 1
| Cross-PlatformGUIProgrammingwithwxWidgets(exactmatch) |     | 1   |
| ----------------------------------------------------- | --- | --- |
EmbeddedComputingandMechatronicswiththePIC32Microcontroller(exact 0.87
match)
Quantum entanglement for secure communication (Quantum entanglement 0.78
breakthroughcouldboostencryption,securecommunications)
AnIntroductiontoTopologyanditsApplications(Anintroductiontotopology 0.67
| anditsapplications:                            | Anewapproach)                                 |      |
| ---------------------------------------------- | --------------------------------------------- | ---- |
| SQLServerQueryPerformanceTuning(exactmatch)    |                                               | 0.67 |
| WCAG2.1:                                       | WebContentAccessibilityGuidelines(exactmatch) | 0.61 |
| SessionAnnouncementProtocol(SAP)(exactmatch)   |                                               | 0.5  |
| IntroductiontoAtmosphericChemistry(exactmatch) |                                               | 0.33 |
Data modeling and database design: Using access to build a database (exact 0.33
match)
IntroductoryDigitalElectronics: FromTruthTablestoMicroprocessors(exact 0.33
match)
Trust Management: First International Conference, iTrust 2003, Heraklion, 0.25
Crete,Greece(exactmatch)
| Randomgeometricgraphs(exactmatch)                 |                                  | 0.08 |
| ------------------------------------------------- | -------------------------------- | ---- |
| StatisticalInference:                             | AnIntegratedApproach(exactmatch) | 0    |
| NetworkServiceAssurance(exactmatch)               |                                  | 0    |
| HigherOrderEquationalLogicProgramming(exactmatch) |                                  | 0    |
NetworkMobilityRouteOptimizationRequirements(NetworkMobilityRoute 0
Optimization Requirements for Operational Use in Aeronautics and Space
ExplorationMobileNetworks)
Thermalmanagementofelectricvehiclebatterysystems(exactmatch) 0
| HandbookofImagingMaterials(exactmatch) |     | 0   |
| -------------------------------------- | --- | --- |
The Secure Online Business Handbook: E-commerce, IT Functionality and 0
BusinessContinuity(exactmatch)
| AdvancedLogicSynthesis(exactmatch) |     | 0   |
| ---------------------------------- | --- | --- |
926

Table9: ReferencetitlesclassifiedasH(hallucination)byBinggeneratedfromGPT-4. 30randomlysampledtitles
areshown.
Referencetitlegenerated(ClosestMatch,iffound) IQProb
Privacy-PreservingAttribute-BasedAccessControlinCloudComputing(Accountableprivacypre- 0
servingattribute-basedaccesscontrolforcloudservicesenforcedusingblockchain)
PolicyMeasuresforCombatingOnlinePrivacyIssues(NA) 0
StorageSecurity: ProtectingSanitizedDataAttestation(NA) 0
DesignofScalableParallelAlgorithmsforGraphProblems(NA) 0
VeryLargeScaleIntegration(VLSI)DesignwithStandardCells: LayoutDesignandPerformance 0
Analysis(NA)
Object-OrientedModelingandSimulationofComplexSystems(Modellingandsimulationofcomplex 0
systems)
OverviewofElectronicDesignAutomation(EDA)Tools&Methodologies(TheElectronicDesign 0
AutomationHandbook)
PrintersandModernStorageSolutions: TheRoleoftheCloudandMobileDevices(NA) 0
AlgebraicAlgorithmsandSymbolicAnalysisTechniquesinComputerAlgebraSystems(Computer 0
algebrasystemsandalgorithmsforalgebraiccomputation)
MeasuringSoftwarePerformanceinCross-platformMobileApplications(NA) 0
AComparativeStudyofOAMProtocolsinEthernetNetworks(CarrierEthernetOAM:anoverview 0
andcomparisontoIPOAM)
BestPracticesinBoard-andSystem-levelHardwareTestDevelopment(NA) 0
AlgorithmsforSymbolicandAlgebraicComputationsinScienceandEngineering(NA) 0
CryptographyandSecureE-CommerceTransactions:Methods,Frameworks,andBestPractices(NA) 0
Quantum Computing: A Primer for Understanding and Implementation ( A primer on quantum 0
computing)
UnderstandingNetworkManagement: Concepts, Standards, andModels(Networkmanagement: 0
principlesandpractice)
Assessingnetworkreliability: Ananalyticalapproachbasedongraphentropy(NA) 0
LanguageModelsandtheirApplicationstoInformationRetrieval(Languagemodelsforinformation 0
retrieval)
AutomatedSupportforLegacySoftwareMaintenanceandEvolution(NA) 0
In-NetworkTrafficProcessing: AdvancementsandPerspectives(NA) 0
IntellectualPropertyLawandPolicyintheDigitalEconomy(IntellectualPropertyLawandPolicyin 0
theDigitalEconomy)
The Art and Science of Survey Research: A Guide to Best Practices (The Art and Science of 0
Reviewing(andWriting)SurveyResearch)
ReviewofNetworkMobilityProtocols: SolutionsandChallenges(AReviewofNetworkMobility 0
ProtocolsforFullyElectricalVehiclesServices)
ProgramSemantics,Higher-OrderTypes,andStepCounting(NA) 0
NetworkServices: ManagementStrategiesandTechniques(NA) 0
MachineLearning-BasedPowerEstimationandManagementinEnergyHarvestingSystems(NA) 0
TheEvolutionofDistanceEducation: HistoricalandTheoreticalPerspectives(DistanceEducation: 0.17
HistoricalPerspective)
TheEconomicsofVLSIManufacturing: ACostAnalysisApproach(NA) 0.5
DigitalDecisions: TheIntersectionofe-GovernmentandAmericanFederalism(NA) 0.78
EnterpriseModeling: TacklingBusinessChallengeswiththe4EMApproach(EnterpriseModeling 1
with4EM:PerspectivesandMethod)
927

Table10: ReferencetitlesclassifiedasG(grounded)byBinggeneratedfromGPT-4. 30randomlysampledtitlesare
shown.
| Referencetitlegenerated(Matchedtitle)    |     |     | IQProb |
| ---------------------------------------- | --- | --- | ------ |
| ArtandElectronicMedia(exactmatch)        |     |     | 1      |
| Network+GuidetoNetworks(exactmatch)      |     |     | 1      |
| HandbookofAutomatedReasoning(exactmatch) |     |     | 1      |
SystemDynamics: Modeling,Simulation,andControlofMechatronicSystems(exact 1
match)
| InformationVisualization: | PerceptionforDesign(exactmatch) |     | 1   |
| ------------------------- | ------------------------------- | --- | --- |
TheEmperor’sNewMind: ConcerningComputers,MindsandtheLawsofPhysics 1
(exactmatch)
| ComputerNetworks:                                  | ASystemsApproach(exactmatch) |     | 1   |
| -------------------------------------------------- | ---------------------------- | --- | --- |
| DNSandBIND:HelpforSystemAdministrators(exactmatch) |                              |     | 1   |
| IntroductiontoModernCryptography(exactmatch)       |                              |     | 1   |
Beyond Software Architecture: Creating and Sustaining Winning Solutions (exact 1
match)
PracticalByzantineFaultToleranceandProactiveRecovery(exactmatch) 1
Real-TimeSystems: Scheduling,Analysis,andVerification(exactmatch) 1
| ComputationalComplexity: | AModernApproach(exactmatch) |     | 1   |
| ------------------------ | --------------------------- | --- | --- |
TheFoundationsofCryptography: Volume1,BasicTechniques(exactmatch) 1
DigitalLibraryUse: SocialPracticeinDesignandEvaluation(exactmatch) 1
TransactionalInformationSystems: Theory,Algorithms,andthePracticeofConcur- 1
rencyControlandRecovery(exactmatch)
| DatabaseSystemConcepts(exactmatch)               |     |     | 1   |
| ------------------------------------------------ | --- | --- | --- |
| PatternRecognitionandMachineLearning(exactmatch) |     |     | 1   |
| FileSystemForensicAnalysis(exactmatch)           |     |     | 1   |
The Archaeology of Science: Studying the Creation of Useful Knowledge (exact 0.78
match)
WebDataMining: ExploringHyperlinks,Contents,andUsageData(exactmatch) 0.67
ElectronicDesignAutomationforIntegratedCircuitsHandbook(exactmatch) 0.47
| ModernVLSIDesign: | IP-BasedDesign(exactmatch) |     | 0.39 |
| ----------------- | -------------------------- | --- | ---- |
ComputationalComplexityandStatisticalPhysics(exactmatch) 0.33
ProbabilisticMethodsforAlgorithmicDiscreteMathematics(exactmatch) 0.33
DigitalRightsManagement: ProtectingandMonetizingContent(exactmatch) 0.08
| DeepLearningforComputerVision:                   |     | ABriefReview(exactmatch) | 0.08 |
| ------------------------------------------------ | --- | ------------------------ | ---- |
| RandomGeometricGraphsandApplications(exactmatch) |     |                          | 0.07 |
ConcurrentSeparationLogicforPipelinedParallelization(exactmatch) 0
High-LevelSynthesisforReal-timeDigitalSignalProcessing(exactmatch) 0
928