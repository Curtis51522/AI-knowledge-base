Right for Right Reasons: Large Language Models for Verifiable
|     | Commonsense |     |     |     | Knowledge | Graph | Question |     | Answering |     |     |     |
| --- | ----------- | --- | --- | --- | --------- | ----- | -------- | --- | --------- | --- | --- | --- |
ArminToroghi1,WillisGuo1,MohammadMahdiAbdollahPour1,ScottSanner1,2
1UniversityofToronto,Canada
2VectorInstituteofArtificialIntelligence,Toronto,Canada
|     | {armin.toroghi, |     |     | gwillis.guo,m.abdollahpour}@mail.utoronto.ca |     |     |     |     |     |     |     |     |
| --- | --------------- | --- | --- | -------------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- |
ssanner@mie.utoronto.ca
|           |         | Abstract |          |           |           | such as   | RQL            | (Karvounarakis |          | et            | al., 2002) | and     |
| --------- | ------- | -------- | -------- | --------- | --------- | --------- | -------------- | -------------- | -------- | ------------- | ---------- | ------- |
|           |         |          |          |           |           | SPARQL    | (Prud’hommeaux |                |          | and Seaborne, |            | 2008)   |
| Knowledge |         | Graph    | Question |           | Answering |           |                |                |          |               |            |         |
|           |         |          |          |           |           | have been | developed.     |                | However, |               | writing    | queries |
| (KGQA)    | methods |          | seek     | to answer | Natural   |           |                |                |          |               |            |         |
intheselanguagesrequiresexpertisewhichlimits
| Language    | questions |        | using        | the | relational |                                       |     |     |     |     |     |        |
| ----------- | --------- | ------ | ------------ | --- | ---------- | ------------------------------------- | --- | --- | --- | --- | --- | ------ |
|             |           |        |              |     |            | theaccessibilityofKGstoinexpertusers. |     |     |     |     |     | Knowl- |
| information |           | stored | in Knowledge |     | Graphs     |                                       |     |     |     |     |     |        |
edgeGraphQuestionAnswering(KGQA)(Zheng
| (KGs). | With | the | recent | advancements | of  |     |     |     |     |     |     |     |
| ------ | ---- | --- | ------ | ------------ | --- | --- | --- | --- | --- | --- | --- | --- |
Large Language Models (LLMs) and their etal.,2017;Berantetal.,2013a;Yihetal.,2016)
remarkable reasoning abilities, there is a is an established research field that facilitates ac-
growing trend to leverage them for KGQA. cesstoKGsbyprovidingfactualanswerstonatural
| However, | existing |     | methodologies |     | have only |     |     |     |     |     |     |     |
| -------- | -------- | --- | ------------- | --- | --------- | --- | --- | --- | --- | --- | --- | --- |
language(NL)questionsusingKGs.
| focused   | on answering |         | factual   | questions,   | e.g.,     |           |            |           |       |                      |     |          |
| --------- | ------------ | ------- | --------- | ------------ | --------- | --------- | ---------- | --------- | ----- | -------------------- | --- | -------- |
|           |              |         |           |              |           | Recently, | the        | promising |       | performance          |     | of Large |
| “In which | city         | was     | Silvio    | Berlusconi’s | first     |           |            |           |       |                      |     |          |
|           |              |         |           |              |           | Language  | Models     | (LLMs)    |       | in reasoning-related |     |          |
| wife      | born?”,      | leaving | questions |              | involving |           |            |           |       |                      |     |          |
|           |              |         |           |              |           | tasks has | encouraged |           | their | application          |     | in KGQA  |
commonsensereasoningthatreal-worldusers
mayposemoreoften,e.g.,“DoIneedseparate research(Baeketal.,2023;Guanetal.,2023b;Li
visastoseetheVenusofWillendorfandattend etal.,2023a). Whiletheseworkshavesignificantly
the Olympics this summer?” unaddressed. enhancedtheperformanceofKGQAsystems,their
In this work, we first observe that existing primaryfocushasbeenonaddressingfactoidques-
LLM-basedmethodsforKGQAstrugglewith
tions,suchas"InwhichcitywasSilvioBerlusconi’s
| hallucination  |           | on such       | questions, |            | especially |            |           |         |       |                 |        |          |
| -------------- | --------- | ------------- | ---------- | ---------- | ---------- | ---------- | --------- | ------- | ----- | --------------- | ------ | -------- |
|                |           |               |            |            |            | first wife | born?",   | which   |       | can be answered |        | using    |
| on queries     | targeting |               | long-tail  | entities   | (e.g.,     |            |           |         |       |                 |        |          |
|                |           |               |            |            |            | only the   | knowledge |         | graph | (KG) facts.     |        | However, |
| non-mainstream |           | and           | recent     | entities), | thus       |            |           |         |       |                 |        |          |
|                |           |               |            |            |            | real-world | user      | queries | often | extend          | beyond | the      |
| hindering      | their     | applicability |            | in         | real-world |            |           |         |       |                 |        |          |
applications especially since their reasoning factoidknowledgestoredintheKG.Forexample,
processesarenoteasilyverifiable. Inresponse, answeringaquestionsuchas"DoIneedseparate
(R3),
we propose Right for Right Reasons visastoseetheVenusofWillendorfandattendthe
| a commonsense |     | KGQA |     | methodology | that |     |     |     |     |     |     |     |
| ------------- | --- | ---- | --- | ----------- | ---- | --- | --- | --- | --- | --- | --- | --- |
Olympicsthissummer?"requiresbothKGtriples
allowsforaverifiablereasoningprocedureby
|     |     |     |     |     |     | indicatingthelocationsofVenusofWillendorf |     |     |     |     |     | and |
| --- | --- | --- | --- | --- | --- | ----------------------------------------- | --- | --- | --- | --- | --- | --- |
axiomaticallysurfacingintrinsiccommonsense
theplacewherethissummer’sOlympicsistaking
| knowledge                        |     | of LLMs | and | grounding | every   |         |              |                |         |           |     |          |
| -------------------------------- | --- | ------- | --- | --------- | ------- | ------- | ------------ | -------------- | ------- | --------- | --- | -------- |
|                                  |     |         |     |           |         | place,  | as well      | as commonsense |         | reasoning |     | about    |
| factualreasoningsteponKGtriples. |     |         |     |           | Through |         |              |                |         |           |     |          |
|                                  |     |         |     |           |         | how one | can identify |                | whether | traveling |     | to those |
experimentalevaluationsacrossthreedifferent
tasks—questionanswering,claimverification, countriesrequiresseparatevisasornot.
andpreferencematching—ourfindingsshow- Commonsensereasoningisoneofthemostsig-
caseR3asasuperiorapproach,outperforming
nificantcapabilitiesofferedbyLLMs(ShenandKe-
existingmethodologiesandnotablyreducing jriwal,2021;Zhaoetal.,2024). Therefore,itmay
instancesofhallucinationandreasoningerrors.
seemstraightforwardtoleveragetheLLMstorea-
sonoverasetofretrievedKGfactstoperformcom-
1 Introduction
monsenseKGQA.However,LLMsarestillsuscep-
KnowledgeGraphs(KGs)havebeenwidelyused tibletointroducingungroundedorincorrectinfor-
as a structured format for storing and represent- mationtotheirreasoningprocess–aphenomenon
ing relational information. Efficiently querying calledhallucination(Yeetal.,2023;Tonmoyetal.,
KGs to obtain the required knowledge is a long- 2024). InconductingcommonsenseKGQA,LLMs
standing problem, for which query languages mayexhibithallucinationsbothbyintroducingun-
6601
Proceedingsofthe2024ConferenceonEmpiricalMethodsinNaturalLanguageProcessing,pages6601–6633
November12-16,2024©2024AssociationforComputationalLinguistics

grounded factual information as well as making 2023;Songetal.,2023;Clusmannetal.,2023).
incorrect commonsense inferences. Hence, veri-
2.2 CommonsenseQuestionAnswering
fiability of the reasoning process is crucial to en-
sure the reliability of the final answer, especially Thegeneralknowledgeandconceptionaboutthe
in high-stakes applications. Regrettably, none of worldthathumanspossess,andtheirabilitytorea-
theexistingLLM-enhancedKGQAmethodologies sonaboutitiscalledcommonsensereasoningand
answerqueriesfollowingaverifiablescheme. isacrucialcognitiveabilityofhumans. Itisalso
In this paper, we experimentally show that the an important reasoning skill based on which AI
performance of existing KGQA methods is crit- agents are evaluated (Liu et al., 2021; ?; Wang
ically hindered by the hallucination issue when etal.,2023). LLMshaveshownoutstandingcom-
facedwithquestionsinvolvingcommonsenserea- monsense reasoning skills and the gap between
soning. This issue is particularly exacerbated for theirperformanceandhumansonavailabledatasets
questionsaboutlong-tailknowledge,i.e.,questions has narrowed substantially (Guan et al., 2023a;
targetingobscureorrecententities,andpersonal- Bian et al., 2023). Most of these datasets such
ized questions. To address this challenge, we in- as CommonsenseQA (Talmor et al., 2018) and
troduceRightforRightReasons(R3),averifiable PhysicalQA (Bisk et al., 2020) contain questions
methodologyforperformingKGQAusingLLMs. aboutconceptsratherthanentities. Recently,Strat-
R3 makes both aspects of commonsense KGQA egyQA(Gevaetal.,2021a)andCreak(Onoeetal.,
reasoning, factoid steps and commonsense infer- 2021b) have been proposed as datasets for com-
ences,verifiable. Forthecommonsenseinference monsensereasoningaboutentitiesthatcanbeused
aspect,itaxiomaticallysurfacesthecommonsense tointroducecommonsensereasoningtoKGQA.
knowledgerequiredforansweringthequestionthat
2.3 KnowledgeGraphQueryAnswering
is intrinsic to the LLM parameters. Also, it casts
the KGQA task into a tree-structured search in Answeringquestionsusingtherelationalinforma-
which all factual reasoning steps are enforced to tion of KGs has recently gained significant atten-
begroundedonasubsetoftherelevantKGtriples tion(Wangetal.,2024;ToroghiandSanner,2024),
whichenablestheverificationoffactualreasoning withitsapplicationsrangingfromhealthcare(Guo
steps. WecompareR3 againstcurrentLLM-based et al., 2022) to recommendation (Toroghi et al.,
KGQAmethodologiesandpureLLMmethodson 2023). Most existing works on the task of an-
three different tasks: question answering, claim swering NL queries using the KG facts, known
verification, and KG-based preference matching. asKGQA,focusonconvertingtheNLqueryinto
The results demonstrate that R3 leads to a con- a structured formal query in a language such as
siderablereductioninhallucinationandreasoning SPARQL, executing the query to retrieve the re-
errorswhileoftenimprovingaccuracyandoffering quiredknowledge,andfinallyreasoningoverthe
robustnesstoentitypopularity. retrievedfactstoobtainthefinalanswer. Thisidea,
referred to as semantic parsing (Lan et al., 2021;
2 Background Gu and Su, 2022; Cheng et al., 2022), often in-
volvesthedataandcomputationallyexpensivepro-
2.1 ReasoningwithLargeLanguageModels
cessoffine-tuningwiththousandsoflabeledexam-
Despite being originally designed for text gen- ples(Chenetal.,2021;Shuetal.,2022). Recently,
eration, LLMs have shown outstanding perfor- KB-BINDERhassuggestedatraining-freeseman-
mance when applied to several other NLP sub- ticparsingmethodologyusingthein-contextlearn-
fields (Chang et al., 2023). Particularly, the rea- ing ability of LLMs with few-shot examples (Li
soningcapabilityofLLMshasattractedconsider- et al., 2023b). Novel LLM-based methods be-
ableinterestinAIresearch(Aroraetal.,2022;Sun yond semantic parsing approach have also been
etal.,2022;Xuetal.,2023). Severalworkshave proposed. KAPING(Baeketal.,2023)introduced
studieddifferentreasoningskillsofLLMssuchas anefficientLLM-enhancedKGQAmodelthatfinds
arithmetic reasoning (Yuan et al., 2023), logical the relevant sub-graph to the query via dense re-
reasoning(Liuetal.,2023),andcommonsenserea- trieval and uses the LLM to reason over it in a
soning(Bianetal.,2023;ShenandKejriwal,2023). zero-shotmanner. KGR(Guanetal.,2023b)pro-
TheseabilitiesmakeLLMsaptcandidatesforbeing posedtheideaofallowingLLMstomakeclaims,
usedasareasonerinspecializedtasks(Renetal., retrofittingthoseclaimsontheKGfacts,andfinally
6602

reasoningusingthecorrectedclaims. However,all significanceareprovidedinAppendixA.
existingworksonKGQAaredesignedtoanswer
factoidqueries,andnoneofthemhasconsidered 3.2.1 ObtainingRelevantSub-graph
queriesinvolvingcommonsensereasoning.
Thequeryansweringprocessbeginsbyextracting
q
|     |             |     |     |     |     |     | from                    | q. Most | existing       | works                 | perform |     | this ex- |
| --- | ----------- | --- | --- | --- | --- | --- | ----------------------- | ------- | -------------- | --------------------- | ------- | --- | -------- |
| 3   | Methodology |     |     |     |     |     | E                       |         |                |                       |         |     |          |
|     |             |     |     |     |     |     | traction                | using   | entity linking | techniques            |         | (Li | et al.,  |
|     |             |     |     |     |     |     | 2020;Ayoolaetal.,2022). |         |                | However,sinceexisting |         |     |          |
3.1 ProblemFormulation
entitylinkersmayfailtoextractrecentorobscure
| In this | paper, | we propose |     | a methodology |     | for per- |     |     |     |     |     |     |     |
| ------- | ------ | ---------- | --- | ------------- | --- | -------- | --- | --- | --- | --- | --- | --- | --- |
entitiesfromthequery,wealsouseanLLM-based
| forming | commonsense |     | KGQA | that | is easily | ex- |     |     |     |     |     |     |     |
| ------- | ----------- | --- | ---- | ---- | --------- | --- | --- | --- | --- | --- | --- | --- | --- |
modulewithfew-shotexamplestoobtainanother
| tended | to  | other related | tasks | such | as KG-based |     |     |     |     |     |     |     |     |
| ------ | --- | ------------- | ----- | ---- | ----------- | --- | --- | --- | --- | --- | --- | --- | --- |
setofentitynames,andconsidertheunionofthe
| preferencematching. |     |     | Theinputtotheproblemisa |     |     |     |                                 |     |     |     |           |     |     |
| ------------------- | --- | --- | ----------------------- | --- | --- | --- | ------------------------------- | --- | --- | --- | --------- | --- | --- |
|                     |     |     |                         |     |     |     | twosetsasthefinalsetofentities. |     |     |     | Formally, |     |     |
NLsentenceposedbytheuserthatcanbeeithera
questionintheformofaninterrogativesentence,
q
oraclaimorneedexpressedasanimperativesen- = EL(q, ) LLM E (q), (1)
|        |     |              |        |         |     |       |     | E   |     | K ∪ |     |     |     |
| ------ | --- | ------------ | ------ | ------- | --- | ----- | --- | --- | --- | --- | --- | --- | --- |
| tence. | We  | use the term | query, | denoted | by  | q, to |     |     |     |     |     |     |     |
refertotheinputinallcases. Thequerymentions where EL is an entity linker module and LLM E is
a set of anchor entities q. A KG K = ( , ) is theLLM-basedmodulethatidentifiesanchorenti-
|     |     |     | E   |     | E   | R   |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
assumed to be given, where and denote its ties mentioned in q. Once the anchor entities are
|     |     |     |     | E   | R   |     |     |     |     | q   |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
setofentitiesandrelationsrespectively,suchthat identified,weextract ,thesub-graphof
|     |     |     |     |     |     |     |     |     | K   | ⊂ K |     |     | K   |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
q
. Theobjectiveistofollowasequenceof withinthe1-hopneighborhoodof q .
| E         | ⊂ E |         |         |     |        |        |     |     |     |     | E   |     |     |
| --------- | --- | ------- | ------- | --- | ------ | ------ | --- | --- | --- | --- | --- | --- | --- |
| reasoning |     | steps q | to find | aq  | q, the | answer |     |     |     |     |     |     |     |
|           |     | S       |         | ∈   | O      |        |     |     |     |     |     |     |     |
tothequery,suchthatverifyingthecorrectnessof q = (h,r,t) (h,r,t) h q . (2)
|       | q   | q            |     |       | q       |     | K   | {   | |   | ∈   | K∧  | ∈ E } |     |
| ----- | --- | ------------ | --- | ----- | ------- | --- | --- | --- | --- | --- | --- | ----- | --- |
| every | s   | is possible. |     | Here, | denotes | the |     |     |     |     |     |       |     |
|       | i ∈ | S            |     |       | O       |     |     |     |     |     |     |       |     |
setofpossibleoptions.
|     |     |     |     |     |     |     | 3.2.2 SurfacingCommonsenseAxioms |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | -------------------------------- | --- | --- | --- | --- | --- | --- |
3.2 RightforRightReasons
ThecommonsenseknowledgethatLLMshaveob-
|          |          |         |                   |             |         |      | tained during     |     | their training | process  |     | is intrinsic | to     |
| -------- | -------- | ------- | ----------------- | ----------- | ------- | ---- | ----------------- | --- | -------------- | -------- | --- | ------------ | ------ |
| Our      | proposed | method  | casts             | the problem | of      | com- |                   |     |                |          |     |              |        |
|          |          |         |                   |             |         |      | their parameters, |     | and            | they can | use | it to        | answer |
| monsense |          | KGQA as | a tree-structured |             | search, | in   |                   |     |                |          |     |              |        |
whicheveryreasoningstepiseithergroundedon queries given a set of retrieved facts. Existing
KGfacts,orbasedonsurfacedcommonsenseax- LLM-based methods that are designed for tack-
lingthefactoidKGQAproblemcanapproachcom-
ioms,akeypropertythatmakesthereasoningpro-
cedurecompletelyverifiable. monsenseKGQAusingthisintrinsiccapabilityof
Theoverallworkflow
ofR3 foransweringaqueryisshowninFigure1. theirLLMcomponent. However,sincethesetof
commonsenseaxiomsthereasonerhasusedisnot
| Inbrief,R3 |     | firstidentifiestheanchorentitiesofa |     |     |     |     |                                           |     |     |     |     |     |     |
| ---------- | --- | ----------------------------------- | --- | --- | --- | --- | ----------------------------------------- | --- | --- | --- | --- | --- | --- |
|            |     |                                     |     |     |     |     | known,thereasoningprocessisnotverifiable. |     |     |     |     |     | To  |
queryandobtainstherelevantsub-graphforthese
addressthisissue,R3
entities. Next, it surfaces a commonsense axiom axiomaticallysurfacesthis
fromtheLLMthatwillguidethereasoningstepsin intrinsicknowledgeofthereasonerandusesitto
|                            |     |     |     |                  |     |     | guide the | reasoning | process. |     | In other | words, | its |
| -------------------------- | --- | --- | --- | ---------------- | --- | --- | --------- | --------- | -------- | --- | -------- | ------ | --- |
| thatbranchofthesearchtree. |     |     |     | Then,ateachdepth |     |     |           |           |          |     |          |        |     |
level of the tree, it checks whether the common- reasonerisenforcedtostatethepremisesrequired
senseaxiomcanbesatisfiedwiththeavailableKG forconcludingananswerasasetofatomicfactoid
|     |     |     |     |     |     |     | clauses | and try | to find | the answer | by  | identifying |     |
| --- | --- | --- | --- | --- | --- | --- | ------- | ------- | ------- | ---------- | --- | ----------- | --- |
facts,andifpossible,providesananswergrounded
whetherthoseclausesaresatisfiedwhentheirvari-
| onasubsetofthem. |     |     | IftheavailableKGtriplesare |     |     |     |     |     |     |     |     |     |     |
| ---------------- | --- | --- | -------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
insufficient,bybackward-chainingfromtheaxiom, ables are grounded on the KG entities, and their
|     |     |     |     |     |     |     | predicatesandfunctionsonKGrelations. |     |     |     |     |     | Forex- |
| --- | --- | --- | --- | --- | --- | --- | ------------------------------------ | --- | --- | --- | --- | --- | ------ |
itselectsthenextentitytoobtainitsrelevantKG
ample,whengivenaquery"Woulditmakesense
| sub-graphtocontinuethesearch. |     |     |     |     | Eachbranchcan |     |     |     |     |     |     |     |     |
| ----------------------------- | --- | --- | --- | --- | ------------- | --- | --- | --- | --- | --- | --- | --- | --- |
continueuptoamaximumdepth,andifananswer forVirginiaRaggitoaskforaquinceañera?",the
isnotobtainedatitsbottom,anewcommonsense reasonersurfacestheaxiom: "IfVirginiaRaggiisa
girlfromLatinAmericaandherageisnear15,it
axiomwillbesurfacedwhichwillguidesearchin
wouldmakesenseforhertoaskforaquinceañera."
anewbranchuntilthesearchtreereachesitsmax-
|     |     |     |     |     |     |     |     |     |     | q   | q   |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
imum breadth. Components of R3 are explained Formally,given q = e ,...,e ,acommon-
1
|     |     |     |     |     |     |     |     |     | E   | {   | |E q | | }   |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ------ | --- | --- |
here, and a series of analyses on their roles and senseaxiomI isanNLrepresenta tio noftheFirst-
q
6603

Query Obtaining Relevant Sub-graph
v a i D t s o t a f e o t s n W h I t d i o s n i t l e s S h le e e e u n d e m O d t s o h m e ly r e p f e m a V r a r ? p e n a i n t d c e u s s M G N H u r s a i a e s t t u u v o m r r a e y l t o t f ian c c o u l l l t e u c r t e io W n V i e ll n e u n s d i d o o n i f r s s f c t b a o y n v c e e re o d f d e S p z i o c S m t c s b u a lp th tu y re Woman I C n S O t F o e ta m l r r y n a d m m a n e t i p c i t o d i t e c n e e e a o l r l g o a c ni a ze ti r c o o n u O S n u F l t 2 y r m r y 0 m a 2 m n p 4 c i e e c i r n s P tim oi e n m t as 2 I c n o 0 s o t 2 t f a 4 nce Ph O r S y G u l g y a m e m m s m p e e s ic r
Axiom ( ): If visas issued for seeing the Venus of Axiom ( ): If the Venus of Willendorf and 2024 Summer Olympics are in two
Willendorf also provide the permission to attend the countries without mutual border controls, then you don't need separate visas.
Olympics, then you don't need separate visas.
Sub-graph retrieval and pruning
Fact-grounded Answer France u b n o c r o d n e t r r o w l i l t e h d Austria Member of Sc A he r n e g a en
Selection
Missing Evidence Identification:
Missing Evidence Identification: Museum of National History
Venus of Willendorf Visa
Sub-graph retrieval and pruning: Sub-graph retrieval and pruning
Not found in KG Austria Country o M f N us a e t u u m ral City Vienna History Venus of Willendorf is in Museum of National History.
Museum of Natural History is located in Austria.
Fact-grounded Answer 2024 Summer Olympics is held in France.
Selection Austria shares an uncontrolled border with France.
(insufficient facts) Answer:
(insufficient facts) V co e u n n u t s r i o e f s W wi i t l h le o n u d t o m rf u a tu n a d l 2 b 0 o 2 r 4 d e S r u c m on m tr e o r l O s, l s y o m y p o i u cs d a o r n e ' t i n n e tw ed o
separate visas. Failed due to reaching Max depth.
Branch Failed Branch Succeeded
. . .
Sub-graph Pruning :
Sub-graph Pruning : location
o M f H N u is s a t e o t u u r m r y al W V i e ll n e u n s d o o f rf Gravettian S F ta ra d n e c d e e O Su l 2 y m 0 m 2 m p 4 i e c r s coun F tr r y ance o M f H N u is s a t e o t u u r m r y a c l ollectio W n V i e ll n e u n s d o o f rf cultur G e ravettian S F ta ra d n e c d l e o e cation O Su l 2 y m 0 m 2 m p 4 i e c r s count F ry rance
collection culture
Fact-grounded Answer Selection
Fact-grounded Answer
Selection
Sub-graph retrieval and pruning
Country Museum City Austria of Natural Vienna History
Fact-grounded Answer
Selection
Missing Evidence Identification: Branch Austria
Failed
Figure1: WorkflowofcommonsenseKGQAprocedureusingR3. Afterextractingentitiesfromthequeryand
retrievingtheirrelevantsub-graphs,acommonsenseaxiomissurfacedfromtheLLMthatguidesthereasoning
branch. Afterpruningsub-graphstoobtaintheirrelevantfactstotheaxiom,aniterativeprocessusingtheLLMis
executedtoeitherprovideafact-groundedansweroridentifymissinginformationandretrieveitfromtheKG.Ifthe
answerisnotfoundafteracertaindepth,anewaxiomissurfacedtoguideanewbranch.
OrderLogic(FOL)expression havethemostsemanticsimilaritytothecommon-
q
senseaxiomI . Sincefilteringtriplesbyonlycon-
i
sideringsemanticsimilaritymayleadtoahighrisk
|P| |E| |F| |E|
 P i (e j ) ∧ F i (e j ) ⟨ opi j⟩ ei j oflosingsomeusefultriples,wealsouseanLLM
i=1j=1 i=1j=1 module with few-shot examples to pick relevant
^ ^ ^ ^
   = a , (  3) triplestotheaxiomfromasubsetofthesub-graph
q
⇒
triplestoreducethechanceofthisinformationloss.
in which = P ,...,P is the set of predi- FormallywehavetheSub-graphPruningmodule
1 P
cates, = P F { ,...,F | is |} the set of functions, SGPas
1 F
opi F =, { =,<, ,> | , |} isa(dis)equalityop-
⟨ j⟩ ∈ { ̸ ≤ ≥} SGP(I q , q) =
eratororcomparisonoperatorifthefunctionvalue i K
is numeric, ei j is the entity compared to the func- top-k t ∈K q (sim(t,I q i )) ∪ LLM T ( K q,I i q ), (4)
tionevaluation,anda q istheanswertothequeryor q = SGP(I q , q),
Ti i K
claim. Theserelationsandfunctionsareallatomic
clausesthatcanbecheckedagainsttheKGtriples. inwhichsimdenotestheEuclideansimilaritybe-
q
tweentandI ,theembeddingvectorsofthetriple
i
3.2.3 Sub-graphPruning tandtheaxiomI q ,top-k operatorreturnsthefirst
i
Onceacommonsenseaxiomissurfaced,R3 tries k elementsofthesortedlistoftriplesbytheirsim-
toidentifythesatisfiabilityofthepremisesbased ilarity score in descending order, and LLM is an
T
on the KG triples. Since the number of triples in LLM-basedmodulethatreturnsasubsetof q that
q maybelarge,weneedtofirstprunethesetof arerelevanttoI q . K
K i
availableKGtriples. Tothisend,asin (Baeketal.,
2023),weuseoff-the-shelfdenseretrievers(Song 3.2.4 Fact-GroundedAnswerSelection
q
et al., 2020; Karpukhin et al., 2020; Xiong et al., After surfacing the commonsense axiom I , and
i
2020)toobtain q q,thesubsetoftriplesthat obtainingthesetofrelevanttriples q ,R3 triesto
Ti ⊂ K Ti
6604

identifywhetherallpremisesintheaxiomcanbe maximumdepthisreachedforthebranch. Incase
satisfiedbygroundingthemontherelevanttriples, themaximumdepthforabranchisreachedwithout
inwhichcasetheanswertothequeryis"True",or obtainingananswer, anewcommonsenseaxiom
atleastoneofthepremisesisunsatisfied,making willbegeneratedtoformanewbranch.
the answer "False". If the axiom is in a disjunc-
3.3 ComparisontoExistingKGQAMethods
tive form, the answer becomes "True" as soon as
eachdisjunctiveclauseiscompletelysatisfied. In R3 isthefirstKGQAapproachthatsupportscom-
allthesecases,R3 returnstheanswer,andtherea- monsensequeriesinaverifiablemanner,sinceev-
soningprocessisterminated. Formultiple-choice ery factual reasoning step is grounded on partic-
queries, the process is repeated for each option ular KG triples, and its commonsense reasoning
until an option satisfies all premises. However, assumptions are surfaced in the form of axioms.
if the satisfiability of any of the premises is not Although KGR (Guan et al., 2023b) retrofits its
identifiable by the current set of facts, instead of factual claims on the KG, its commonsense rea-
returningaguessedanswerthatencourageshallu- soningprocessisimplicit. Semanticparsingmeth-
cination,theanswerwillremainundetermined. In odsareonlydesignedforfactoidqueriesandcan-
thiscase,thesetofcurrentfactsisinsufficientfor notaddresscommonsensequeries. Finally,KAP-
grounding all premises, so the reasoning process ING(Baeketal.,2023),despiteitsstrongperfor-
must continue to the next depth level. Formally, manceonsingle-hopfactoidqueries,cannotanswer
theansweraq "True","False","Idon’tknow" multi-hop questions because it has no particular
∈ { }
isdeterminedby mechanismfortraversingtheKG.Asummaryof
keypropertiesofexistingKGQAmethodsandtheir
aq = answer(q,I q , q ), (5) comparisontoR3 isprovidedinTable1.
i Ti
whereansweristheLLM-basedmoduledetermin- 4 Experiments
ingthefinalanswer.
WeempiricallyevaluateR3 onthreetasks: Ques-
3.2.5 MissingEvidenceIdentification tionanswering,claimverification,andKG-based
preferencematching. Alltasksarecloselyrelated
The set of retrieved facts may be insufficient in
to KGQA and involve commonsense reasoning.
two cases: either the query targets a different en-
Wereleaseallourimplementationcodesanddata1.
tity,asinmulti-hopquestions,orthefactsrequired
for grounding at least one premise were mistak-
4.1 TaskDescription
enly pruned. In this step, the reasoner is asked
Question Answering. Inthis task, aquestion re-
toconsiderthesetofunsatisfiedpremisesandthe
quiring commonsense reasoning formed around
existingfactstofirstidentifywhatadditionalevi-
someKGentitiesisasked. Thereasonerisrequired
dence must be obtained that is currently missing.
tofindtheanswer,whichiseither"Yes"orNo.
Then, it has to identify the anchor entity e that
m
itstriplescanprovidethemissinginformation. If ClaimVerificationClaimverificationisverysim-
the anchor entity is already in, , the next top k ilar to question answering. Here, an imperative
q
E
relevant facts about it will be picked for the next sentenceincludingaclaimaboutsomeentitiesis
step. Otherwise,thereasonerisaskedtopropose stated. ThereasonerhastousetheKGfactstode-
thenextentityandextractitsnamefrom q. The cidewhethertheclaimis"Correct"or"Incorrect".
K
nextentityisthenaddedto ,andtheprocessof
q KG-based Preference Matching In this task, a
E
sub-graphextractionandpruningisexecutedforit.
query explaining the user’s preference and a per-
Formally,
sonalKGcontainingevidenceabouttheuser’spref-
erencesandrestrictionsispresentedtothereasoner.
em = MEI(q,I q , ), (6)
i T i Thereasonerhastochoosetheitemthatmatches
q = q em ,
Ej+1 Ej ∪{ } boththeuser’squeryandtheirpersonalrestrictions.
q = q (h,r,t) (h,r,t) h em ,
Kj+1 Kj ∪{ | ∈ K∧ ∈ } 4.2 Datasets
= SGP( q ,I q ),
T i T i ∪ Kj+1 i Due to the lack of existing datasets, we modify
three existing datasets to make them suitable for
whereMEIisthemoduleidentifyingentityem. This
procedurecontinuesuntilananswerisfoundorthe 1https://github.com/atoroghi/RRR-release
6605

Method FactoidQA Verifiability Commonsense Notraining Multi-hop
| ClassicalSemanticParsing |     |     |     |     |     |     | ✗   | ✗   |     |     | ✗   |     |     |
| ------------------------ | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|                          |     |     |     |     | ✓   |     |     |     |     |     |     |     | ✓   |
| KB-BINDER                |     |     |     |     | ✓   |     | ✗   | ✗   |     |     | ✓   |     | ✓   |
|                          |     |     |     |     |     |     | ✗   |     |     |     |     |     | ✗   |
| KAPING                   |     |     |     |     | ✓   |     |     | ✓   |     |     | ✓   |     |     |
| KGR                      |     |     |     |     |     |     | ✗   |     |     |     |     |     |     |
|                          |     |     |     |     | ✓   |     |     | ✓   |     |     | ✓   |     | ✓   |
R3
|     |     |         |                                                    |     | ✓   |     | ✓   | ✓   |     |     | ✓   |     | ✓   |
| --- | --- | ------- | -------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|     |     | Table1: | ComparisonofR3propertiesagainstexistingKGQAMethods |     |     |     |     |     |     |     |     |     |     |
ourtasksandmakethempubliclyavailabletoen- claimsandwritetheirlong-tailcounterparts.
courageresearchoncommonsenseKGQA.Exam-
|     |     |     |     |     |     |     | KG-based | Preference |     |     | Matching |     | Recipe- |
| --- | --- | --- | --- | --- | --- | --- | -------- | ---------- | --- | --- | -------- | --- | ------- |
plesofthesemodificationsareshowninTable3. MPR(Zhangetal.,2023)isapreferencematching
datasetthatcontainsNLqueriesexpressingauser’s
QuestionAnsweringEarlyKGQAdatasetscon-
sisted of simple questions that can be answered preference toward recipes and often targeting
usingasingleKGtriple. Recently,datasetscontain- multiple aspects. The reasoner has to choose the
recipethatsatisfiesallaspectsamongfiveoptions.
ingmorecomplexquestionsbyintroducingmulti-
hop reasoning have been proposed (Berant et al., The multi-aspect nature of its queries and the
2013b;Trivedietal.,2017;Guetal.,2021). How- necessity for performing logical reasoning make
|     |     |     |     |     |     |     | it a relevant | dataset |     | to our | work. | However, | its |
| --- | --- | --- | --- | --- | --- | --- | ------------- | ------- | --- | ------ | ----- | -------- | --- |
ever,allKGQAdatasetscontainfactoidquestions,
|          |             |     |             |     |           |     | queries | are not | personalized, |     | meaning | that | the |
| -------- | ----------- | --- | ----------- | --- | --------- | --- | ------- | ------- | ------------- | --- | ------- | ---- | --- |
| which do | not require |     | commonsense |     | reasoning | to  |         |         |               |     |         |      |     |
answer (Guo et al., 2024). Some datasets exclu- correctrecipedoesnotrequirereasoningoverthe
sively focus on evaluating commonsense reason- user’s preferences and restrictions beyond those
|     |     |     |     |     |     |     | statedinthequery. |     | Inreal-worldapplications,the |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | ----------------- | --- | ---------------------------- | --- | --- | --- | --- |
ing(Talmoretal.,2018;Boratkoetal.,2020;Sap
et al., 2019), but their questions target concepts "correct"itemisdifferentforeachuserconsidering
(e.g.,river,mountain,etc.) ratherthanKGentities their personal preferences and restrictions. To
|     |     |     |     |     |     |     | bridge | this gap, | we first | extract | 100 | queries | from |
| --- | --- | --- | --- | --- | --- | --- | ------ | --------- | -------- | ------- | --- | ------- | ---- |
(e.g.,specificpeople,locations,etc.).
|             |     |                |     |     |        |        | Recipe-MPR | dataset |     | that require |     | commonsense |     |
| ----------- | --- | -------------- | --- | --- | ------ | ------ | ---------- | ------- | --- | ------------ | --- | ----------- | --- |
| To overcome |     | this challenge |     | we  | modify | Strat- |            |         |     |              |     |             |     |
egyQA (Geva et al., 2021b), a QA dataset reasoningandaddasyntheticpersonalKGforthe
with Yes/No questions that target entities from userposingthequery. Wealsoaddasixthoption
| Wikipedia2 |           |     |           |          |     |        | thatmatcheseverypreferenceaspectofthequery |     |     |     |     |     |     |
| ---------- | --------- | --- | --------- | -------- | --- | ------ | ------------------------------------------ | --- | --- | --- | --- | --- | --- |
|            | articles. |     | We select | a subset |     | of 150 |                                            |     |     |     |     |     |     |
questions for which the required factual knowl- butviolatesatleastonepersonalrequirementthat
edge for answering them is present in Wikidata3 canbeinferredfromtheuser’spersonalKG.
orthatcanberewrittenassuchqueriesbytarget-
ing them on new entities. The questions mostly 4.3 ExperimentalSetup
targetfamousentitiesthatLLMscananswerusing
R3
|     |     |     |     |     |     |     | We compare |     | against |     | LLM baselines |     | with |
| --- | --- | --- | --- | --- | --- | --- | ---------- | --- | ------- | --- | ------------- | --- | ---- |
theirinternalknowledgewithouthallucinatingor
Chain-of-Thought(CoT)prompting,bothinzero-
| even needing | a   | KG. Since | we  | are particularly |     | in- |              |     |            |     |              |     |      |
| ------------ | --- | --------- | --- | ---------------- | --- | --- | ------------ | --- | ---------- | --- | ------------ | --- | ---- |
|              |     |           |     |                  |     |     | shot (Kojima | et  | al., 2022) |     | and few-shot | (k  | = 2) |
terestedinstudyingthehallucinationbehaviorof
|           |      |         |         |              |               |        | settings | (Wei      | et al., | 2022) | to evaluate | the       | need |
| --------- | ---- | ------- | ------- | ------------ | ------------- | ------ | -------- | --------- | ------- | ----- | ----------- | --------- | ---- |
| LLM-based | KGQA | methods |         | on long-tail |               | knowl- |          |           |         |       |             |           |      |
|           |      |         |         |              |               |        | for a KG | to answer |         | these | queries,    | and three | re-  |
| edge, for | each | query,  | we also | write        | a counterpart |        |          |           |         |       |             |           |      |
centLLM-basedKGQAmodels,KB-BINDER(Li
| targeting | long-tail | knowledge |     | by substituting |     | its |     |     |     |     |     |     |     |
| --------- | --------- | --------- | --- | --------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
etal.,2023a),KGR(Guanetal.,2023b),andKAP-
| entities | with obscure |     | entities | of the | same | types. |           |         |        |     |          |           |     |
| -------- | ------------ | --- | -------- | ------ | ---- | ------ | --------- | ------- | ------ | --- | -------- | --------- | --- |
|          |              |     |          |        |      |        | ING (Baek | et al., | 2023). | For | question | answering |     |
WeusethenumberofWikidatatriplesandGoogle
andclaimverificationtasks,weevaluateallmeth-
Searchresultsasmeasuresofpopularity.
odsonbothoriginalqueries(targetingfamousen-
ClaimVerificationForKG-basedclaimverifica-
tities)andmodifiedqueries(targetinglong-tailen-
tion,weuseCreak(Onoeetal.,2021a),adataset tities)tostudytheirrobustnesstopopularityshift.
containing True/False claims written by crowd WeuseGPT-3.5TurboastheLLMforallmodels.
| workers | using | Wikipedia. |     | We follow | a similar |     |     |     |     |     |     |     |     |
| ------- | ----- | ---------- | --- | --------- | --------- | --- | --- | --- | --- | --- | --- | --- | --- |
Inadditiontoaccuracy,weperformhumanevalua-
procedureappliedtotheQAdatasettoselect150
tiontomeasurefactualandreasoningfaithfulness.
Inparticular,weuseFActScore(Minetal.,2023),
2https://www.wikipedia.org/
3https://www.wikidata.org/ whichmeasuresthepercentageofatomicfactsin
6606

|              |           |          | Accuracy  | FActScore          | Reasoning          |
| ------------ | --------- | -------- | --------- | ------------------ | ------------------ |
| Task         | Model     |          |           |                    |                    |
|              |           | Original | Long-Tail | Original Long-Tail | Original Long-Tail |
|              | 0-shotCoT | 0.70     | 0.32      | 0.63 0.54          | 0.90 0.89          |
|              | 2-shotCoT | 0.70     | 0.43      | 0.64 0.52          | 0.92 0.90          |
| Question     | KAPING    | 0.72     | 0.67      | 0.74 0.59          | 0.86 0.83          |
| Answering    | KB-BINDER | 0.11     | 0.08      | - -                | - -                |
|              | KGR       | 0.39     | 0.13      | 0.61 0.47          | 0.70 0.65          |
|              | R3        | 0.82     | 0.73      | 0.97 0.96          | 0.97 0.95          |
|              | 0-shotCoT | 0.89     | 0.35      | 0.76 0.59          | 0.93 0.91          |
|              | 2-shotCoT | 0.92     | 0.41      | 0.78 0.58          | 0.93 0.92          |
| Claim        | KAPING    | 0.91     | 0.81      | 0.81 0.75          | 0.90 0.88          |
| Verification | KB-BINDER | 0.35     | 0.14      | - -                | - -                |
|              | KGR       | 0.80     | 0.20      | 0.70 0.58          | 0.74 0.71          |
|              | R3        | 0.85     |           |                    |                    |
|              |           |          | 0.85      | 0.98 0.98          | 0.97 0.96          |
Table2: Resultsforallmethodsonthequestionansweringandclaimverificationtaskonboththeoriginaland
modified(long-tail)queries. FaCTScoreandReasoningarehumanevaluatedmetrics.
QuestionAnswering
ExemplarOriginalQuestion DidAlanTuringsufferfromthesamefateasAbrahamLincoln?
DidIvanShuiskysufferfromthesamefateasBennyFrey?
ExemplarModifiedQuestion
ClaimVerification
ExemplarOriginalClaim TheBugsBunnycartoonswereinfluencedbythecartoonRickandMorty.
ExemplarModifiedClaim GiovanniBattistaCasti’sworksmaybeinfluencedbyMariaGraziaLenisa’spoems.
PreferenceMatching
| ExemplarQuery |     | Sam:Ilikeeatingpulledmeats,butnotbeeforchicken. |     |     |     |
| ------------- | --- | ----------------------------------------------- | --- | --- | --- |
✓Shreddedbarbecuedporkshoulder
OriginalOptions
✓Porkchopsmadewithorangejuice,garlic,andthyme
✓ShreddedbarbecuedbeefwithWorcestershiresauce
✓Sandwichesmadewithshreddedbarbecuedchickenthighs
✓Chicken,mushroom,andtomatobakedinasaucemixture
✓PulledPorkinaCrockpotwithgarlicandorangejuice
AddedOption
PersonalKG (Sam,occupation,painter),(Sam,age,29),(Sam,medicalcondition,alliumallergy),...
,(Sam,religion,Christianity),(Sam,medicalcondition,lactoseintolerance).
Table3: ExemplarqueriesformDatasetsusedforeachtaskandmodificationsappliedtothem. Modifiedqueriesin
QuestionansweringandClaimverificationtargetobscureentitiestoevaluaterobustnesstopopularityshift. The
syntheticKGandthenewoptionaddpersonalizationaspecttothePreferenceMatchingtask.
anLLM’sresponsesupportedbyaknowledgebase, KB-BINDER’s performance is much lower than
andReasoningscore,whichmeasuresthepropor- othermethods,becauseKB-BINDERisasemantic
tionofLLMresponsesinwhichtherearenological parsingmethodthatonlysupportsfactoidqueries
reasoningerrors. Forpreferencematching,ourhu- andnotonesthatrequirecommonsensereasoning.
manevaluationconsistsofmeasuringAccuracyof Although 0-shot and few-shot CoT achieve 0.70
Reasons which is the fraction of correct answers accuracyontheoriginalqueries, theiraccuracies
thatwereobtainedfromcorrectreasons. dropsignificantlyinthelong-tailsettingto0.32and
0.43respectively. Wealsoobserveinthelong-tail
| 4.4 Results |     |     |     | settingasharpincreaseinthenumberofquestions |     |
| ----------- | --- | --- | --- | ------------------------------------------- | --- |
forwhichtheLLMresponds“Idon’tknow.”
4.4.1 QuestionAnswering
R3
Theresultsforthequestionansweringtaskarepre- Among all methods, hallucinates the least,
sented in table 2. R3 beats all baselines, achiev- withthehighestFActScores,0.97and0.96,inthe
ing an accuracy of 0.82 and 0.73 in the original original and long-tail settings respectively. KAP-
and long-tail settings respectively. Although the ING’sFActScores,0.74and0.59,aresignificantly
lowerthanR3,despiteleveragingdenseretrieval.
| strongest baseline, | KAPING, | achieves | compara- |     |     |
| ------------------- | ------- | -------- | -------- | --- | --- |
bleaccuracy,humanevaluationrevealsthatKAP- ThisisbecauseKAPING’sretrievalislimitedtoen-
ING’sanswersarefarlessreliablethanthoseofR3. titiesinthequestion,whichworksonlyforsingle-
6607

hop queries. For multihop queries, KAPING re- accuracydropssignificantlyby0.51.
WeobservethatagainR3
sortstotheLLM’sinternalknowledge. Fromour maintainsthehighest
LLM baselines, we observe low FActScores, in- FActScore,0.98,inboththeoriginalandlong-tail
dicatingthatLLM’sinternalknowledgeisinsuffi- settings. Incontrast,similartothequestionanswer-
Incontrast,R3
cient. enforcesstrictgroundingon ing task, all baseline methods have significantly
the KG for reasoning, and has an iterative mech- lowerFActScoresthatalsodecreasesignificantly
anismforidentifyingwhatadditionalfactsarere- in the long-tail setting. The low and decreasing
quired,whichleadstonearperfectFActScores. FActScores in both the question answering and
|          |         |            |     |             |       | claim verification |     | task | crucially | demonstrate |     | that |
| -------- | ------- | ---------- | --- | ----------- | ----- | ------------------ | --- | ---- | --------- | ----------- | --- | ---- |
| Not only | are the | FActScores |     | of baseline | meth- |                    |     |      |           |             |     |      |
ods significantly lower than R3, but we also ob- LLMssufferfromhighratesofhallucinationwhich
serve for all baselines a significant decrease in areexacerbatedinlong-tailsettings.
R3
FActScoreonlong-tailqueries. Forinstance,KAP- also maintains the highest reasoning score
ING’sFActScoredropsby0.15from0.74to0.59. amongallmethods,0.04betterthanthenext-best
Theseresultsshowthatbaselinemethodhallucina- methodwhichisfew-shotCoT.Interestingly,with
tions are exacerbated in the long-tail setting due few-shot CoT, we qualitatively observe that the
|     |     |     |     |     |     | LLM at | times | erroneously | follows |     | the reasoning |     |
| --- | --- | --- | --- | --- | --- | ------ | ----- | ----------- | ------- | --- | ------------- | --- |
toLLMsbeingunabletofaithfullyrecalllong-tail
knowledge. ForKAPING,wealsoobservethatthe strategiesintheexamples. Webelievethatexplic-
entity linker fails more often to identify long-tail itlysurfacingcommonsenseaxiomsiscrucialfor
entities,whichinevitablyleadstoungroundedhal- correctlyguidingthesubsequentreasoning. Again,
lucinatedanswersintheabsenceofrelevanttriples. KAPING’s low precision KG retrieval misleads
Incontrast,R3 maintainsahighFActScoreinboth the LLM, resulting in low reasoning scores, and
theoriginalandlong-tailsettingswithrespective KGR’spoorreasoningleadstosuboptimalinitial
responsesthatKGRhasdifficultyretrofitting.
scoresof0.97and0.96,whichindicateitsrobust-
nesstoshiftsinentitypopularity. Astatisticalanalysisoftheseresultsisprovided
inAppendixB,whichverifiesthatR3
| R3 also | maintains | the | highest | reasoning | score |     |     |     |     |     | statistically |     |
| ------- | --------- | --- | ------- | --------- | ----- | --- | --- | --- | --- | --- | ------------- | --- |
comparedtoallbaselines,achievingascoreof0.97 significantly reduces sources of hallucination on
and 0.95 in the original and long-tail settings re- threeofthestudieddatasets. Wealsoprovideanec-
spectively,comparedtothenextbestmethod,few- dotalexamplesofR3’sperformanceinaddressing
shotCoT,whichachievesreasoningscoresof0.92 LLMmisbeliefsinAppendixC.
R3
| and 0.90. | Because |     | makes | the commonsense |     |     |     |     |     |     |     |     |
| --------- | ------- | --- | ----- | --------------- | --- | --- | --- | --- | --- | --- | --- | --- |
4.4.3 PreferenceMatching
inferenceprocessexplicitbyaxiomaticallysurfac-
|                                    |     |     |     |     |          | Results        | of the | preference                | matching |     | task | are pro- |
| ---------------------------------- | --- | --- | --- | --- | -------- | -------------- | ------ | ------------------------- | -------- | --- | ---- | -------- |
| ingthecommonsenseinferencerules,R3 |     |     |     |     | provides |                |        |                           |          |     |      |          |
|                                    |     |     |     |     |          | videdinTable4. |        | SincethepersonalKGdoesnot |          |     |      |          |
bothmoreverifiableandfaithfulchainsofreason-
supportSPARQLqueries,KB-BINDERcannotbe
| ing with           | less errors. | In                         | contrast, | KAPING | has a |           |     |         |     |          |           |     |
| ------------------ | ------------ | -------------------------- | --------- | ------ | ----- | --------- | --- | ------- | --- | -------- | --------- | --- |
|                    |              |                            |           |        |       | evaluated | on  | it. KGR | and | pure LLM | baselines |     |
| lowreasoningscore. |              | Wequalitativelyobservethat |           |        |       |           |     |         |     |          |           |     |
alsocannotbeevaluatedonthistasksincetheycan
| due to the | low precision |     | of the | facts retrieved | by  |     |     |     |     |     |     |     |
| ---------- | ------------- | --- | ------ | --------------- | --- | --- | --- | --- | --- | --- | --- | --- |
onlymakeclaimsorprovideanswersaboutentities
| KAPING,    | the LLM           | is      | frequently | misled | by the      |                   |     |                              |         |           |       |      |
| ---------- | ----------------- | ------- | ---------- | ------ | ----------- | ----------------- | --- | ---------------------------- | ------- | --------- | ----- | ---- |
|            |                   |         |            |        |             | that LLMs         | are | aware                        | of, and | not about | users | in a |
| irrelevant | facts. Elsewhere, |         | KGR        | has    | the lowest  |                   |     |                              |         |           |       |      |
|            |                   |         |            |        |             | syntheticdataset. |     | So,theonlyrelevantbaselineis |         |           |       |      |
| reasoning  | score.            | Without | CoT,       | KGR’s  | initial re- |                   |     |                              |         |           |       |      |
KAPING.Resultsofthiscomparisonvividlyiden-
sponseoftencontainspoorreasoning,whichthen
|     |     |     |     |     |     | tify that | on the | challenging |     | task of | personalized |     |
| --- | --- | --- | --- | --- | --- | --------- | ------ | ----------- | --- | ------- | ------------ | --- |
leadstopoorretrofittingandthusalowFActScore
|     |     |     |     |     |     | preference | matching, |     | R3 obtains | a   | considerably |     |
| --- | --- | --- | --- | --- | --- | ---------- | --------- | --- | ---------- | --- | ------------ | --- |
aswell. Notethatwedonotperformhumanevalua-
|     |     |     |     |     |     | higher | accuracy. | We  | also observe |     | that the | Accu- |
| --- | --- | --- | --- | --- | --- | ------ | --------- | --- | ------------ | --- | -------- | ----- |
tionforKB-BINDERsinceitisasemanticparsing
racyofreasonsforR3ismorethandoublethenum-
| method that | outputs | SPARQL |     | queries | which are |     |     |     |     |     |     |     |
| ----------- | ------- | ------ | --- | ------- | --------- | --- | --- | --- | --- | --- | --- | --- |
berforKAPING,whichagainreflectsitsstronger
incompatiblewithFActScoreandreasoningscores.
commonsensereasoningabilityduetoitsspecial
4.4.2 ClaimVerification approachforsurfacingcommonsenseaxioms.
Theresultsfortheclaimverificationtaskarepre-
5 Conclusion
| sentedinTable2. |     | Although2-shotCoTbeatsour |     |     |     |     |     |     |     |     |     |     |
| --------------- | --- | ------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
WeproposedR3,anovelframeworkthatenables
| methodontheoriginalqueries, |     |     |     | ourmethodisro- |     |     |     |     |     |     |     |     |
| --------------------------- | --- | --- | --- | -------------- | --- | --- | --- | --- | --- | --- | --- | --- |
bustinthelong-tailsetting,achievingthesameac- answeringKGqueriesinvolvingcommonsenserea-
curacyastheoriginalsettingwhereas2-shotCOT’s soning using LLMs in a verifiable manner by ax-
6608

| Method |     | Accuracy | AccuracyofReasons |     |      |     | 7 EthicsStatement |     |     |     |     |     |
| ------ | --- | -------- | ----------------- | --- | ---- | --- | ----------------- | --- | --- | --- | --- | --- |
| KAPING |     | 44       |                   |     | 31.8 |     |                   |     |     |     |     |     |
Thisworkintendstoprovideasolutionforimprov-
| R3  |     | 57  |     |     | 70.17 |     |                     |     |     |              |     |            |
| --- | --- | --- | --- | --- | ----- | --- | ------------------- | --- | --- | ------------ | --- | ---------- |
|     |     |     |     |     |       |     | ing the correctness |     | and | faithfulness |     | of LLMs in |
Table4: ResultsofAccuracyandAccuracyofreasons thetaskofcommonsenseKGQA.Additionally,it
(%)forpreferencematchingtask
seekstoimprovetheverifiabilityofthegenerated
answers,therebyaidinginthedetectionandmiti-
gationofincorrectorpotentiallyharmfulcontent.
iomaticallysurfacingtheirintrinsiccommonsense
However,itisimportanttoacknowledgethatthis
knowledge. Keyexperimentalresultsexhibittheef- approach(a)reliesonLLMsthatmayhallucinate
ficacyofR3acrossdifferenttasksrelatedtoKGQA
|     |     |     |     |     |     |     | and (b) presumes |     | the accuracy |     | of the | knowledge |
| --- | --- | --- | --- | --- | --- | --- | ---------------- | --- | ------------ | --- | ------ | --------- |
anditssuperiorperformancetoexistingbaselines.
graph(KG)dataandlacksanycapacitytocorrect
ThepromisingperformanceofR3
combinedwith
erroneousornoisyinformationpresentwithinthe
itsverifiabilityandrobustnesstoentitypopularity
KG.Hence,itisimperativetoensureaccuracyof
opensuppossibilitiesforversatilefutureextension
theKGandthatthereasoningstepsintroducedby
toaddressbroaderrangesoftasksandimprovethe R3’sLLMarefreeofbothhallucinationsandoth-
flexibilityandaccessibilityofKGsandreliability
erwiseincorrect,biased,orunethicalconclusions
ofLLM-basedreasoners.
thatmaybeharmfultodownstreamusers.
6 Limitations
References
| While we | believe | this | work | has made | significant |     |     |     |     |     |     |     |
| -------- | ------- | ---- | ---- | -------- | ----------- | --- | --- | --- | --- | --- | --- | --- |
SimranArora,AvanikaNarayan,MayeeFChen,Laurel
forwardprogressinleveragingKGcontentforcom-
Orr,NeelGuha,KushBhatia,InesChami,Frederic
| monsense | question |     | answering | (QA), | our | method |                             |     |     |     |                |     |
| -------- | -------- | --- | --------- | ----- | --- | ------ | --------------------------- | --- | --- | --- | -------------- | --- |
|          |          |     |           |       |     |        | Sala,andChristopherRé.2022. |     |     |     | Askmeanything: |     |
R3
(like any QA method) has natural limitations A simple strategy for prompting language models.
thatwehopewillencouragefurtherinvestigation arXivpreprintarXiv:2210.02441.
andfuturework.
|     |         |        |           |         |     |           | Tom Ayoola,         | Shubhi | Tyagi, | Joseph | Fisher,    | Christos |
| --- | ------- | ------ | --------- | ------- | --- | --------- | ------------------- | ------ | ------ | ------ | ---------- | -------- |
| The | quality | of the | reasoning | process |     | in R3 re- |                     |        |        |        |            |          |
|     |         |        |           |         |     |           | Christodoulopoulos, |        | and    | Andrea | Pierleoni. | 2022.    |
liesonthequalityofthenaturallanguageaxioms Refined: An efficient zero-shot-capable approach
|             |       |          |             |     |             |        | to end-to-end     |     | entity | linking. | arXiv | preprint |
| ----------- | ----- | -------- | ----------- | --- | ----------- | ------ | ----------------- | --- | ------ | -------- | ----- | -------- |
| generated.  | We    | observe  | through     | our | experiments |        |                   |     |        |          |       |          |
| that in     | cases | where    | the quality | of  | axioms      | is in- | arXiv:2207.04108. |     |        |          |       |          |
| sufficient, | the   | reasoner | is misled   |     | resulting   | in an  |                   |     |        |          |       |          |
JinheonBaek,AlhamFikriAji,andAmirSaffari.2023.
undeterminedanswerattheendoftheexploration
Knowledge-augmentedlanguagemodelprompting
| budgetidentified. |     | Furthermore,duetotheimpor- |     |     |     |     |     |     |     |     |     |     |
| ----------------- | --- | -------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
forzero-shotknowledgegraphquestionanswering.
tance of avoiding hallucination, our model takes arXivpreprintarXiv:2306.04136.
| a conservative |     | and | rigorous | approach | to  | ground |     |     |     |     |     |     |
| -------------- | --- | --- | -------- | -------- | --- | ------ | --- | --- | --- | --- | --- | --- |
JonathanBerant,AndrewChou,RoyFrostig,andPercy
| every factual |           | premise | on KG  | triples. | Therefore, |       |                       |        |          |                        |             |      |
| ------------- | --------- | ------- | ------ | -------- | ---------- | ----- | --------------------- | ------ | -------- | ---------------------- | ----------- | ---- |
|               |           |         |        |          |            |       | Liang.                | 2013a. | Semantic | parsing                | on freebase | from |
| our model     | typically |         | leaves | more     | questions  | unan- |                       |        |          |                        |             |      |
|               |           |         |        |          |            |       | question-answerpairs. |        |          | InProceedingsofthe2013 |             |      |
sweredthanotherbaselines(whichweconsidered conferenceonempiricalmethodsinnaturallanguage
processing,pages1533–1544.
anincorrectresponseincalculatingtheaccuracy).
Furthermore,asinmostLLM-basedmodels,for
JonathanBerant,AndrewChou,RoyFrostig,andPercy
havingaproperperformance,LLM-basedcompo- Liang. 2013b. Semantic parsing on freebase from
nentsofourmodelrequireclearexplanationofthe
|     |     |     |     |     |     |     | question-answerpairs. |     |     | InProceedingsofthe2013 |     |     |
| --- | --- | --- | --- | --- | --- | --- | --------------------- | --- | --- | ---------------------- | --- | --- |
taskprovidedinthepromptstothem,aswellasa Conference on Empirical Methods in Natural Lan-
|     |     |     |     |     |     |     | guage | Processing, | EMNLP |     | 2013, 18-21 | October |
| --- | --- | --- | --- | --- | --- | --- | ----- | ----------- | ----- | --- | ----------- | ------- |
numberoffew-shotexamplesthatclarifytheintent
2013,GrandHyattSeattle,Seattle,Washington,USA,
ofthetaskdescriptionfurther.
AmeetingofSIGDAT,aSpecialInterestGroupofthe
Weconsiderfurtherstudiesintotheabovelimi-
ACL,pages1533–1544.ACL.
| tationsasopenareasoffuturework. |     |     |     |     | Studyingthe |     |     |     |     |     |     |     |
| ------------------------------- | --- | --- | --- | --- | ----------- | --- | --- | --- | --- | --- | --- | --- |
NingBian,XianpeiHan,LeSun,HongyuLin,Yaojie
trade-offbetweenrigorandtherateofunanswered
|            |     |           |           |     |            |         | Lu,andBenHe.2023.                     |     |     | Chatgptisaknowledgeable |     |       |
| ---------- | --- | --------- | --------- | --- | ---------- | ------- | ------------------------------------- | --- | --- | ----------------------- | --- | ----- |
| questions, | as  | well as   | studying  | the | robustness | of      |                                       |     |     |                         |     |       |
|            |     |           |           |     |            |         | butinexperiencedsolver:               |     |     | Aninvestigationofcom-   |     |       |
| our model  | to  | different | prompting |     | styles     | are key |                                       |     |     |                         |     |       |
|            |     |           |           |     |            |         | monsenseprobleminlargelanguagemodels. |     |     |                         |     | arXiv |
researchquestionsthatweconsiderforfuture. preprintarXiv:2303.16421.
6609

YonatanBisk,RowanZellers,JianfengGao,YejinChoi, Xin Guan, Biwei Cao, Qingqing Gao, Zheng Yin,
et al. 2020. Piqa: Reasoning about physical com- BoLiu,andJiuxinCao.2023a. Multi-hopcommon-
monsenseinnaturallanguage. InProceedingsofthe senseknowledgeinjectionframeworkforzero-shot
AAAIconferenceonartificialintelligence,volume34, arXiv preprint
|                 |     |     |     |     |     |     | commonsense       |          | question | answering.  |             |     |
| --------------- | --- | --- | --- | --- | --- | --- | ----------------- | -------- | -------- | ----------- | ----------- | --- |
| pages7432–7439. |     |     |     |     |     |     | arXiv:2305.05936. |          |          |             |             |     |
|                 |     |     |     |     |     |     | Xinyan Guan,      | Yanjiang |          | Liu, Hongyu | Lin, Yaojie | Lu, |
MichaelBoratko,XiangLorraineLi,RajarshiDas,Tim
O’Gorman,DanLe,andAndrewMcCallum.2020. BenHe,XianpeiHan,andLeSun.2023b. Mitigating
Protoqa: A question answering dataset for proto- largelanguagemodelhallucinationsviaautonomous
typical common-sense reasoning. arXiv preprint knowledgegraph-basedretrofitting. arXivpreprint
arXiv:2311.13314.
arXiv:2005.00771.
|        |           |       |         |       |      |     | QuanGuo, | ShuaiCao, | andZhangYi.2022. |     |     | Amedi- |
| ------ | --------- | ----- | ------- | ----- | ---- | --- | -------- | --------- | ---------------- | --- | --- | ------ |
| Yupeng | Chang, Xu | Wang, | Jindong | Wang, | Yuan | Wu, |          |           |                  |     |     |        |
calquestionansweringsystemusinglargelanguage
| Linyi                              | Yang, Kaijie | Zhu, | Hao | Chen, | Xiaoyuan | Yi,   |                           |     |     |                      |     |     |
| ---------------------------------- | ------------ | ---- | --- | ----- | -------- | ----- | ------------------------- | --- | --- | -------------------- | --- | --- |
|                                    |              |      |     |       |          |       | modelsandknowledgegraphs. |     |     | InternationalJournal |     |     |
| CunxiangWang,YidongWang,etal.2023. |              |      |     |       |          | Asur- |                           |     |     |                      |     |     |
veyonevaluationoflargelanguagemodels. ACM ofIntelligentSystems,37(11):8548–8564.
TransactionsonIntelligentSystemsandTechnology. Willis Guo, Armin Toroghi, and Scott Sanner. 2024.
|        |            |      |        |     |          |      | Cr-lt-kgqa: | Aknowledgegraphquestionanswering |     |     |     |     |
| ------ | ---------- | ---- | ------ | --- | -------- | ---- | ----------- | -------------------------------- | --- | --- | --- | --- |
| Shuang | Chen, Qian | Liu, | Zhiwei | Yu, | Chin-Yew | Lin, |             |                                  |     |     |     |     |
datasetrequiringcommonsensereasoningandlong-
| Jian-Guang             | Lou, | and       | Feng                   | Jiang. 2021. |               | Retrack: |                |     |                                |     |     |     |
| ---------------------- | ---- | --------- | ---------------------- | ------------ | ------------- | -------- | -------------- | --- | ------------------------------ | --- | --- | --- |
|                        |      |           |                        |              |               |          | tailknowledge. |     | arXivpreprintarXiv:2403.01395. |     |     |     |
| A flexible             | and  | efficient | framework              |              | for knowledge |          |                |     |                                |     |     |     |
| basequestionanswering. |      |           | InProceedingsofthe59th |              |               |          |                |     |                                |     |     |     |
VladimirKarpukhin,BarlasOg˘uz,SewonMin,Patrick
annualmeetingoftheassociationforcomputational
Lewis,LedellWu,SergeyEdunov,DanqiChen,and
linguisticsandthe11thinternationaljointconference Wen-tau Yih. 2020. Dense passage retrieval for
onnaturallanguageprocessing: systemdemonstra- open-domain question answering. arXiv preprint
tions,pages325–336.
arXiv:2004.04906.
Zhoujun Cheng, Tianbao Xie, Peng Shi, Chengzu Gregory Karvounarakis, Sofia Alexaki, Vassilis
| Li, Rahul | Nadkarni, |     | Yushi | Hu, Caiming |     | Xiong, |                |     |          |              |     |        |
| --------- | --------- | --- | ----- | ----------- | --- | ------ | -------------- | --- | -------- | ------------ | --- | ------ |
|           |           |     |       |             |     |        | Christophides, |     | Dimitris | Plexousakis, | and | Michel |
DragomirRadev,MariOstendorf,LukeZettlemoyer, Scholl. 2002. Rql: a declarative query language
et al. 2022. Binding language models in symbolic for rdf. In Proceedings of the 11th international
languages. arXivpreprintarXiv:2210.02875. conferenceonWorldWideWeb,pages592–603.
Jan Clusmann, Fiona R Kolbinger, Hannah Sophie TakeshiKojima,ShixiangShaneGu,MachelReid,Yu-
Muti, Zunamys I Carrero, Jan-Niklas Eckardt, takaMatsuo,andYusukeIwasawa.2022. Largelan-
NarminGhaffariLaleh,ChiaraMariaLaviniaLöffler, guagemodelsarezero-shotreasoners. InAdvances
|     |     |     |     |     |     |     | in Neural | Information |     | Processing | Systems | 35: An- |
| --- | --- | --- | --- | --- | --- | --- | --------- | ----------- | --- | ---------- | ------- | ------- |
Sophie-CarolineSchwarzkopf,MichaelaUnger,Gre-
goryPVeldhuizen,etal.2023. Thefuturelandscape nualConferenceonNeuralInformationProcessing
oflargelanguagemodelsinmedicine. Communica- Systems2022,NeurIPS2022,NewOrleans,LA,USA,
| tionsMedicine,3(1):141. |     |     |     |     |     |     | November28-December9,2022. |     |     |     |     |     |
| ----------------------- | --- | --- | --- | --- | --- | --- | -------------------------- | --- | --- | --- | --- | --- |
MorGeva,DanielKhashabi,EladSegal,TusharKhot, Yunshi Lan, Gaole He, Jinhao Jiang, Jing Jiang,
|                                  |     |     |     |     |              |     | Wayne | Xin Zhao, | and | Ji-Rong Wen. | 2021. | A sur- |
| -------------------------------- | --- | --- | --- | --- | ------------ | --- | ----- | --------- | --- | ------------ | ----- | ------ |
| DanRoth,andJonathanBerant.2021a. |     |     |     |     | Didaristotle |     |       |           |     |              |       |        |
veyoncomplexknowledgebasequestionanswering:
| usealaptop? | aquestionansweringbenchmarkwith |               |     |              |     |        |                   |                         |     |     |               |     |
| ----------- | ------------------------------- | ------------- | --- | ------------ | --- | ------ | ----------------- | ----------------------- | --- | --- | ------------- | --- |
|             |                                 |               |     |              |     |        | Methods,          | challengesandsolutions. |     |     | arXivpreprint |     |
| implicit    | reasoning                       | strategies.   |     | Transactions |     | of the |                   |                         |     |     |               |     |
| Association | for                             | Computational |     | Linguistics, |     | 9:346– | arXiv:2105.11644. |                         |     |     |               |     |
361.
|     |     |     |     |     |     |     | Belinda Z | Li, Sewon | Min,    | Srinivasan | Iyer,     | Yashar |
| --- | --- | --- | --- | --- | --- | --- | --------- | --------- | ------- | ---------- | --------- | ------ |
|     |     |     |     |     |     |     | Mehdad,   | and       | Wen-tau | Yih. 2020. | Efficient | one-   |
MorGeva,DanielKhashabi,EladSegal,TusharKhot,
|                                  |     |     |     |     |              |     | passend-to-endentitylinkingforquestions. |     |     |     |     | arXiv |
| -------------------------------- | --- | --- | --- | --- | ------------ | --- | ---------------------------------------- | --- | --- | --- | --- | ----- |
| DanRoth,andJonathanBerant.2021b. |     |     |     |     | Didaristotle |     |                                          |     |     |     |     |       |
preprintarXiv:2010.02413.
| usealaptop?                  | Aquestionansweringbenchmarkwith |     |     |                     |     |     |     |     |     |     |     |     |
| ---------------------------- | ------------------------------- | --- | --- | ------------------- | --- | --- | --- | --- | --- | --- | --- | --- |
| implicitreasoningstrategies. |                                 |     |     | Trans.Assoc.Comput. |     |     |     |     |     |     |     |     |
TianleLi,XueguangMa,AlexZhuang,YuGu,YuSu,
Linguistics,9:346–361.
|        |           |          |        |       |     |         | andWenhuChen.2023a.                   |     |     | Few-shotin-contextlearn- |     |       |
| ------ | --------- | -------- | ------ | ----- | --- | ------- | ------------------------------------- | --- | --- | ------------------------ | --- | ----- |
|        |           |          |        |       |     |         | ingforknowledgebasequestionanswering. |     |     |                          |     | arXiv |
| Yu Gu, | Sue Kase, | Michelle | Vanni, | Brian | M.  | Sadler, |                                       |     |     |                          |     |       |
preprintarXiv:2305.01750.
| PercyLiang,XifengYan,andYuSu.2021. |     |     |     |     |     | Beyond |     |     |     |     |     |     |
| ---------------------------------- | --- | --- | --- | --- | --- | ------ | --- | --- | --- | --- | --- | --- |
I.I.D.: threelevelsofgeneralizationforquestionan- TianleLi,XueguangMa,AlexZhuang,YuGu,YuSu,
sweringonknowledgebases. InWWW’21: TheWeb andWenhuChen.2023b. Few-shotin-contextlearn-
Conference2021,VirtualEvent/Ljubljana,Slovenia,
|     |     |     |     |     |     |     | ingforknowledgebasequestionanswering. |     |     |     |     | arXiv |
| --- | --- | --- | --- | --- | --- | --- | ------------------------------------- | --- | --- | --- | --- | ----- |
April19-23,2021,pages3477–3488.ACM/IW3C2.
preprintarXiv:2305.01750.
Yu Gu and Yu Su. 2022. Arcaneqa: Dynamic pro- HanmengLiu,RuoxiNing,ZhiyangTeng,JianLiu,Qiji
gram induction and contextualized encoding for Zhou,andYueZhang.2023. Evaluatingthelogical
knowledgebasequestionanswering. arXivpreprint reasoningabilityofchatgptandgpt-4. arXivpreprint
| arXiv:2204.08109. |     |     |     |     |     |     | arXiv:2304.03439. |     |     |     |     |     |
| ----------------- | --- | --- | --- | --- | --- | --- | ----------------- | --- | --- | --- | --- | --- |
6610

JiachengLiu,AlisaLiu,XimingLu,SeanWelleck,Pe- Chan Hee Song, Jiaman Wu, Clayton Washington,
terWest,RonanLeBras,YejinChoi,andHannaneh Brian M Sadler, Wei-Lun Chao, and Yu Su. 2023.
Hajishirzi. 2021. Generated knowledge prompt- Llm-planner: Few-shot grounded planning for em-
|     |     |     |     |     | arXiv preprint |     |     |     |     |     | InPro- |
| --- | --- | --- | --- | --- | -------------- | --- | --- | --- | --- | --- | ------ |
ing for commonsense reasoning. bodiedagentswithlargelanguagemodels.
arXiv:2110.08387. ceedingsoftheIEEE/CVFInternationalConference
onComputerVision,pages2998–3009.
| Sewon Min, | Kalpesh |     | Krishna, | Xinxi | Lyu, Mike |     |     |     |     |     |     |
| ---------- | ------- | --- | -------- | ----- | --------- | --- | --- | --- | --- | --- | --- |
Lewis, Wen-tau Yih, Pang Wei Koh, Mohit Iyyer, KaitaoSong, XuTan, TaoQin, JianfengLu, andTie-
Luke Zettlemoyer, and Hannaneh Hajishirzi. 2023. YanLiu.2020. Mpnet: Maskedandpermutedpre-
|            |                                       |     |     |     |     | training | for language |     | understanding. |     | Advances in |
| ---------- | ------------------------------------- | --- | --- | --- | --- | -------- | ------------ | --- | -------------- | --- | ----------- |
| Factscore: | Fine-grainedatomicevaluationoffactual |     |     |     |     |          |              |     |                |     |             |
precisioninlongformtextgeneration. InProceed- NeuralInformationProcessingSystems,33:16857–
| ingsofthe2023ConferenceonEmpiricalMethods |     |     |     |     |     | 16867. |     |     |     |     |     |
| ----------------------------------------- | --- | --- | --- | --- | --- | ------ | --- | --- | --- | --- | --- |
inNaturalLanguageProcessing,EMNLP2023,Sin-
gapore,December6-10,2023,pages12076–12100. Tian-Xiang Sun, Xiang-Yang Liu, Xi-Peng Qiu, and
|     |     |     |     |     |     | Xuan-JingHuang.2022. |     |     | Paradigmshiftinnatural |     |     |
| --- | --- | --- | --- | --- | --- | -------------------- | --- | --- | ---------------------- | --- | --- |
AssociationforComputationalLinguistics.
|                                              |          |        |        |           |          | languageprocessing. |     | MachineIntelligenceResearch, |     |     |     |
| -------------------------------------------- | -------- | ------ | ------ | --------- | -------- | ------------------- | --- | ---------------------------- | --- | --- | --- |
| YasumasaOnoe,MichaelJ.Q.Zhang,EunsolChoi,and |          |        |        |           |          | 19(3):169–183.      |     |                              |     |     |     |
| Greg                                         | Durrett. | 2021a. | CREAK: | A dataset | for com- |                     |     |                              |     |     |     |
monsensereasoningoverentityknowledge. InPro- Alon Talmor, Jonathan Herzig, Nicholas Lourie, and
|     |     |     |     |     |     | JonathanBerant.2018. |     |     | Commonsenseqa:Aquestion |     |     |
| --- | --- | --- | --- | --- | --- | -------------------- | --- | --- | ----------------------- | --- | --- |
ceedingsoftheNeuralInformationProcessingSys-
answeringchallengetargetingcommonsenseknowl-
temsTrackonDatasetsandBenchmarks1,NeurIPS
edge. arXivpreprintarXiv:1811.00937.
DatasetsandBenchmarks2021,December2021,vir-
tual.
SMTonmoy,SMZaman,VinijaJain,AnkuRani,Vip-
ulaRawte,AmanChadha,andAmitavaDas.2024.
YasumasaOnoe,MichaelJQZhang,EunsolChoi,and
Acomprehensivesurveyofhallucinationmitigation
| Greg     | Durrett.  | 2021b. | Creak: | A dataset  | for com- |                                  |     |     |     |               |     |
| -------- | --------- | ------ | ------ | ---------- | -------- | -------------------------------- | --- | --- | --- | ------------- | --- |
|          |           |        |        |            |          | techniquesinlargelanguagemodels. |     |     |     | arXivpreprint |     |
| monsense | reasoning | over   | entity | knowledge. | arXiv    |                                  |     |     |     |               |     |
arXiv:2401.01313.
preprintarXiv:2109.01653.
ArminToroghi,GriffinFloto,ZhenweiTang,andScott
| EricPrud’hommeauxandAndySeaborne.2008. |     |     |     |     | Sparql |                       |     |                                    |                        |     |     |
| -------------------------------------- | --- | --- | --- | --- | ------ | --------------------- | --- | ---------------------------------- | ---------------------- | --- | --- |
|                                        |     |     |     |     |        | Sanner.2023.          |     | Bayesianknowledge-drivencritiquing |                        |     |     |
| querylanguageforrdf.w3crecommendation. |     |     |     |     | http:  |                       |     |                                    |                        |     |     |
|                                        |     |     |     |     |        | withindirectevidence. |     |                                    | InProceedingsofthe46th |     |     |
//www.w3.org/TR/rdf-sparql-query/.
InternationalACMSIGIRConferenceonResearch
|         |      |         |        |           |          | and Development |     | in  | Information | Retrieval, | pages |
| ------- | ---- | ------- | ------ | --------- | -------- | --------------- | --- | --- | ----------- | ---------- | ----- |
| Allen Z | Ren, | Anushri | Dixit, | Alexandra | Bodrova, |                 |     |     |             |            |       |
1838–1842.
SumeetSingh,StephenTu,NoahBrown,PengXu,
| Leila     | Takayama, | Fei           | Xia, Jake   | Varley, | et al. 2023.   |                                           |     |          |            |       |               |
| --------- | --------- | ------------- | ----------- | ------- | -------------- | ----------------------------------------- | --- | -------- | ---------- | ----- | ------------- |
|           |           |               |             |         |                | Armin Toroghi                             | and | Scott    | Sanner.    | 2024. | Bayesian in-  |
| Robots    | that      | ask for help: | Uncertainty |         | alignment      |                                           |     |          |            |       |               |
|           |           |               |             |         |                | ferencewithcomplexknowledgegraphevidence. |     |          |            |       | In            |
| for large | language  | model         | planners.   |         | arXiv preprint |                                           |     |          |            |       |               |
|           |           |               |             |         |                | Proceedings                               | of  | the AAAI | Conference |       | on Artificial |
arXiv:2307.01928.
Intelligence,volume38,pages20550–20558.
Maarten Sap, Hannah Rashkin, Derek Chen, Ronan PriyanshTrivedi,GauravMaheshwari,MohnishDubey,
| LeBras,                                   | and | Yejin Choi. | 2019. | Socialiqa: | Com-  |          |          |       |          |     |            |
| ----------------------------------------- | --- | ----------- | ----- | ---------- | ----- | -------- | -------- | ----- | -------- | --- | ---------- |
|                                           |     |             |       |            |       | and Jens | Lehmann. | 2017. | Lc-quad: | A   | corpus for |
| monsensereasoningaboutsocialinteractions. |     |             |       |            | arXiv |          |          |       |          |     |            |
complexquestionansweringoverknowledgegraphs.
preprintarXiv:1904.09728.
|     |     |     |     |     |     | In The Semantic |     | Web | - ISWC      | 2017 - 16th | Interna- |
| --- | --- | --- | --- | --- | --- | --------------- | --- | --- | ----------- | ----------- | -------- |
|     |     |     |     |     |     | tional Semantic |     | Web | Conference, | Vienna,     | Austria, |
Ke Shen and Mayank Kejriwal. 2021. On the gener- October21-25,2017,Proceedings,PartII,volume
alization abilities of fine-tuned commonsense lan- 10588ofLectureNotesinComputerScience,pages
| guage | representation |     | models. | In Artificial | Intelli- |     |     |     |     |     |     |
| ----- | -------------- | --- | ------- | ------------- | -------- | --- | --- | --- | --- | --- | --- |
210–218.Springer.
genceXXXVIII:41stSGAIInternationalConference
onArtificialIntelligence,AI2021,Cambridge,UK,
WeiqiWang,TianqingFang,WenxuanDing,Baixuan
December14–16,2021,Proceedings41,pages3–16. Xu, Xin Liu, Yangqiu Song, and Antoine Bosse-
| Springer. |     |     |     |     |     | lut. 2023. | Car: | Conceptualization-augmented |     |     | rea- |
| --------- | --- | --- | --- | --- | --- | ---------- | ---- | --------------------------- | --- | --- | ---- |
sonerforzero-shotcommonsensequestionanswer-
| Ke Shen | and Mayank |     | Kejriwal. | 2023. | An experi- |     |     |     |     |     |     |
| ------- | ---------- | --- | --------- | ----- | ---------- | --- | --- | --- | --- | --- | --- |
ing. arXivpreprintarXiv:2305.14869.
| mental | study | measuring | the generalization |     | of fine- |     |     |     |     |     |     |
| ------ | ----- | --------- | ------------------ | --- | -------- | --- | --- | --- | --- | --- | --- |
tuned language representation models across com- YuWang,NedimLipka,RyanARossi,AlexaSiu,Ruiyi
monsense reasoning benchmarks. Expert Systems, Zhang, and Tyler Derr. 2024. Knowledge graph
| pagee13243. |     |     |     |     |     | promptingformulti-documentquestionanswering. |     |     |     |     |     |
| ----------- | --- | --- | --- | --- | --- | -------------------------------------------- | --- | --- | --- | --- | --- |
InProceedingsoftheAAAIConferenceonArtificial
| Yiheng Shu, | Zhiwei | Yu, | Yuhan Li, | Börje | F Karlsson, |     |     |     |     |     |     |
| ----------- | ------ | --- | --------- | ----- | ----------- | --- | --- | --- | --- | --- | --- |
Intelligence,volume38,pages19206–19214.
TingtingMa,YuzhongQu,andChin-YewLin.2022.
Tiara: Multi-grainedretrievalforrobustquestionan- JasonWei,XuezhiWang,DaleSchuurmans,Maarten
sweringoverlargeknowledgebases. arXivpreprint Bosma,BrianIchter,FeiXia,EdH.Chi,QuocV.Le,
arXiv:2210.12925. andDennyZhou.2022. Chain-of-thoughtprompting
6611

elicits reasoning in large language models. In Ad- ofeachpartandassessitsimpactonoverallperfor-
vancesinNeuralInformationProcessingSystems35:
mance,weconductaseriesofablationstudiesand
AnnualConferenceonNeuralInformationProcess-
|     |     |     |     |     |     | experimentsinthissection. |     |     | Thisanalysiscontrasts |     |     |
| --- | --- | --- | --- | --- | --- | ------------------------- | --- | --- | --------------------- | --- | --- |
ingSystems2022,NeurIPS2022,NewOrleans,LA,
thefunctionalityofeachcomponentagainstalter-
USA,November28-December9,2022.
|     |     |     |     |     |     | native design | choices, | providing |     | deeper insights |     |
| --- | --- | --- | --- | --- | --- | ------------- | -------- | --------- | --- | --------------- | --- |
LeeXiong,ChenyanXiong,YeLi,Kwok-FungTang, intothenecessityofeachelementintheR3 archi-
JialinLiu,PaulBennett,JunaidAhmed,andArnold
tecture.
| Overwijk.2020. |     | Approximatenearestneighborneg- |     |     |     |     |     |     |     |     |     |
| -------------- | --- | ------------------------------ | --- | --- | --- | --- | --- | --- | --- | --- | --- |
ative contrastive learning for dense text retrieval. UtilizingtheKGfactsandgroundingthefacts
arXivpreprintarXiv:2007.00808. usedinreasoningontheKGisacornerstoneofthe
|         |            |                 |           |            |              | R3 framework. | AblatingtheuseofKGeffectively   |     |     |     |     |
| ------- | ---------- | --------------- | --------- | ---------- | ------------ | ------------- | ------------------------------- | --- | --- | --- | --- |
| Yudong  | Xu, Wenhao | Li,             | Pashootan | Vaezipoor, | Scott        |               |                                 |     |     |     |     |
|         |            |                 |           |            |              | reducesR3     | tothefew-shotCoTbaselines,which |     |     |     |     |
| Sanner, | and        | Elias B Khalil. |           | 2023.      | Llms and the |               |                                 |     |     |     |     |
abstractionandreasoningcorpus:Successes,failures, we previously compared in Section 4. There are
andtheimportanceofobject-basedrepresentations. three major steps in answering a commonsense
arXivpreprintarXiv:2305.18354.
querybasedonKG:
| Hongbin | Ye, Tong | Liu, Aijia | Zhang, | Wei | Hua, and |     |     |     |     |     |     |
| ------- | -------- | ---------- | ------ | --- | -------- | --- | --- | --- | --- | --- | --- |
• ExtractingKGentitiesfromthequeryandob-
| Weiqiang | Jia. | 2023. Cognitive |     | mirage: | A review |     |     |     |     |     |     |
| -------- | ---- | --------------- | --- | ------- | -------- | --- | --- | --- | --- | --- | --- |
tainingthesub-graphcontainingthequeries.
| of hallucinations |     | in large | language | models. | arXiv |     |     |     |     |     |     |
| ----------------- | --- | -------- | -------- | ------- | ----- | --- | --- | --- | --- | --- | --- |
preprintarXiv:2309.06794.
• Identifyingthefactsthatarerelevantanduse-
Wen-tauYih,MatthewRichardson,ChristopherMeek,
|                                |     |     |     |     |            | ful in | answering | the | question | from | the ex- |
| ------------------------------ | --- | --- | --- | --- | ---------- | ------ | --------- | --- | -------- | ---- | ------- |
| Ming-WeiChang,andJinaSuh.2016. |     |     |     |     | Thevalueof |        |           |     |          |      |         |
tractedsub-graph.
semanticparselabelingforknowledgebasequestion
| answering. | InProceedingsofthe54thAnnualMeet- |     |     |     |     |     |     |     |     |     |     |
| ---------- | --------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
• Answeringthequestionusingtheserelevant
ingoftheAssociationforComputationalLinguistics
| (Volume2: | ShortPapers),pages201–206. |     |     |     |     | facts. |     |     |     |     |     |
| --------- | -------------------------- | --- | --- | --- | --- | ------ | --- | --- | --- | --- | --- |
Zheng Yuan, Hongyi Yuan, Chuanqi Tan, Wei Wang, R3 adds a critical step that governs its search
| andSongfangHuang.2023. |     |     | Howwelldolargelan- |     |     |     |     |     |     |     |     |
| ---------------------- | --- | --- | ------------------ | --- | --- | --- | --- | --- | --- | --- | --- |
processforansweringthequery,whichissurfacing
| guage | models | perform | in arithmetic |     | tasks? arXiv |                      |     |     |                     |     |     |
| ----- | ------ | ------- | ------------- | --- | ------------ | -------------------- | --- | --- | ------------------- | --- | --- |
|       |        |         |               |     |              | thecommonsenseaxiom. |     |     | Theimportanceofthis |     |     |
preprintarXiv:2304.02015.
stepwasshownthroughexperimentsconductedin
HaochenZhang,AntonKorikov,ParsaFarinneya,Mo- Section4. Removingthesurfacedcommonsense
hammadMahdiAbdollahPour,ManasaBharadwaj,
|     |     |     |     |     |     | axiomsandthetree-structuredsearchthatR3 |     |     |     |     | em- |
| --- | --- | --- | --- | --- | --- | --------------------------------------- | --- | --- | --- | --- | --- |
AliPesaranghader,XiYuHuang,YiXinLok,Zhaoqi
Wang, Nathan Jones, et al. 2023. Recipe-mpr: A ploystoanswerqueriessimplifiesittoKAPING,
oneofthebaselineweevaluatedinSection4and
testcollectionforevaluatingmulti-aspectpreference-
basednaturallanguageretrieval. InProceedingsof showedthatitwasoutperformedbyR3.
| the 46th | International |     | ACM SIGIR | Conference | on  |     |     |     |     |     |     |
| -------- | ------------- | --- | --------- | ---------- | --- | --- | --- | --- | --- | --- | --- |
Inthissection,westudytheoptionsanddesign
ResearchandDevelopmentinInformationRetrieval,
| pages2744–2753. |     |     |     |     |     | choicesthatcanbeconsideredforeachofthethree |     |     |     |     |     |
| --------------- | --- | --- | --- | --- | --- | ------------------------------------------- | --- | --- | --- | --- | --- |
enumeratedstepsandexaminetheinfluenceofab-
ZiruiZhao,WeeSunLee,andDavidHsu.2024. Large latingcomponentsutilizedintheR3 frameworkin
| language | models | as commonsense |     | knowledge | for |     |     |     |     |     |     |
| -------- | ------ | -------------- | --- | --------- | --- | --- | --- | --- | --- | --- | --- |
eachstep.
| large-scaletaskplanning. |     |     | AdvancesinNeuralInfor- |     |     |     |     |     |     |     |     |
| ------------------------ | --- | --- | ---------------------- | --- | --- | --- | --- | --- | --- | --- | --- |
mationProcessingSystems,36.
A.1 ObtainingRelevantSub-graph
WeiguoZheng,HongCheng,LeiZou,JeffreyXuYu, ThefirststepinansweringaqueryintheR3
frame-
| and Kangfei |     | Zhao. 2017. | Natural | language | ques- |     |     |     |     |     |     |
| ----------- | --- | ----------- | ------- | -------- | ----- | --- | --- | --- | --- | --- | --- |
workisextractingtheKGentitiesthataretargeted
| tion/answering: |                                    | Let users | talk | with the | knowledge |                 |           |       |          |           |     |
| --------------- | ---------------------------------- | --------- | ---- | -------- | --------- | --------------- | --------- | ----- | -------- | --------- | --- |
|                 |                                    |           |      |          |           | in the question | to obtain | their | relevant | sub-graph |     |
| graph.          | InProceedingsofthe2017ACMonConfer- |           |      |          |           |                 |           |       |          |           |     |
enceon InformationandKnowledge Management, fromtheKGandanswerthequerybasedonit. We
pages217–226.
considerthreedesignchoicesforthisstep:
AnalysisofR3
| A             |     | Components      |     |         |          | • Usingexistingentity-linkingmethodologies |        |            |     |               |     |
| ------------- | --- | --------------- | --- | ------- | -------- | ------------------------------------------ | ------ | ---------- | --- | ------------- | --- |
| The framework |     | of R3 comprises |     | several | integral |                                            |        |            |     |               |     |
|               |     |                 |     |         |          | • Using                                    | an LLM | to extract |     | entities from | the |
partsandmodulesthatcollectivelyenhanceitsper-
query
| formance. | InSection4,wedelineatedthemotiva- |     |     |     |     |     |     |     |     |     |     |
| --------- | --------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
tionandfunctionofeachcomponentwithintheR3 • Usingacombinedapproachbyunitingentities
framework. Tofurthersubstantiatethesignificance obtainedbythesetwomethods(usedinR3)
6612

|     |     |     |     | QuestionAnswering  | ClaimVerification  |
| --- | --- | --- | --- | ------------------ | ------------------ |
|     |     |     |     | Original Long-Tail | Original Long-Tail |
StandardEntitylinker(Ayoolaetal.,2022) 0.938 0.854 0.974 0.986
|     | LLM-basedEntityextractor |     |     | 0.960 0.979 | 0.928 0.986 |
| --- | ------------------------ | --- | --- | ----------- | ----------- |
R3
|     |     |     |     | 1.00 1.00 | 1.00 1.00 |
| --- | --- | --- | --- | --------- | --------- |
Table5: Successrateofdifferentapproachesinextractingentitiesfromqueriesofeachdatasetsplit. Thesuperior
performanceofR3inextractingtherelevantentitiesfromqueriescomparedtotheablationsshowstheimportance
ofbothentityextractionmodulesintheR3framework.
|     |     |     |     | QuestionAnswering  | ClaimVerification  |
| --- | --- | --- | --- | ------------------ | ------------------ |
|     |     |     |     | Original Long-Tail | Original Long-Tail |
R3withoutEntityLinker
|     |                                   |     |     | 0.807 0.713 | 0.820 0.846 |
| --- | --------------------------------- | --- | --- | ----------- | ----------- |
|     | R3withoutLLM-basedEntityExtractor |     |     | 0.793 0.700 | 0.827 0.753 |
|     | R3                                |     |     | 0.820 0.727 | 0.846 0.853 |
AccuracyofR3comparedtoitsvariantswithablatedentityextractionmodules.
| Table6: |     |     |     |     | Thehighersuccessrateof |
| ------- | --- | --- | --- | --- | ---------------------- |
R3inextractingqueriesalsoresultsinahigheraccuracy.
Existing KGQA methodologies often rely on on every query that one of these methods fails to
entity-linkingtechniques(Lietal.,2020;Ayoola extractthecorrectentity,theothermethodsuccess-
et al., 2022) that efficiently extract well-known fullycompensatesforit. Wenotethatthisperfect
entities. However, since these methods were not entity extraction result that is obtained for R3 is
trainedonsufficientdatafromlong-tailandrecent confinedtothedatasetsthatwestudiedinthispa-
entities that R3 aims to address, they might not perandacrossotherdatasets,theremightbecases
beabletoperformsuccessfulentityextractionfor inwhichbothentityextractionmethodsfail. How-
R3
those queries. To address this possible issue, ever, using both methods considerably increases
also leverages an LLM-based entity extractor. In thechanceofsuccessfulretrieval. Thistablealso
thisanalysis,westudytheroleandimportanceof validates our hypothesis that the standard entity
eachoftheseentityextractiontechniques. linking mythologies may be challenged more in
To this end, we first compare the entity extrac- extractingthelong-tailentities,buttheLLM-based
entityextractorismorerobusttoentities’popular-
| tion performance | of each  | of these entity | linking    |      |     |
| ---------------- | -------- | --------------- | ---------- | ---- | --- |
| methodologies    | by using | each of them    | to extract | ity. |     |
entitiesforallqueriesofallsubsetsofthedataset, To further verify the importance of utilizing
andcomparingthesetsofretrievedentitiesagainst both sub-graph extraction methodologies, we ex-
thesetofgroundtruthentitiesthatarecontainedin amine the role of each method in the overall per-
allqueries. Resultsofthisexperimentareshown formance of R3. We repeat all experiments for
inTable5. Inthefirstrowofthistable,weuseRe- both tasks—question answering and claim verifi-
FinED,astandardentitylinkingmethodologythat cation—while ablating the two entity extraction
isspecializedforWikipediaandWikidataentities, methodologies. Theresultsofthisexperimentare
andinthesecondrow,wejustuseourLLM-based presented in Table 6. These findings underscore
entity extractor. The final row refers to the final thesignificanceoftheentityextractionschemeem-
setofentitiesthatweuseinR3 whichisbasically ployed in R3. In every case, the combined use
theunionoftheentitiesretrievedbyeachofthese ofbothentityextractionmethodologies(asimple-
R3)
methods. From this table, we can verify that al- mented in enhances the accuracy across all
thoughbothentityextractionmethodshaveahigh tasks. Additionally, this table highlights the con-
successrateinextractingtheentities,theyareboth tributionoftheLLM-basedentityextractorintro-
imperfectandfailtoextractafractionoftheentities ducedinthisworktothemethod’soverallperfor-
| fromsomequeries. | However,whentheirunionis |     |     | mance. |     |
| ---------------- | ------------------------ | --- | --- | ------ | --- |
usedinR3,allentitiescanbesuccessfullyretrieved In conclusion, for extracting the relevant sub-
toextracttheirrelevantsub-graph. Thismeansthat graph—acrucialfirststepinansweringcommon-
6613

sensequeriesbasedonthefactualknowledgeofthe andidentifyingmissinginformationatdeeperlev-
KG—thecombinedmethodologyintroducedinR3 ThisiterativeprocessenablesR3
|     |     |     |     |     | elsofthetree. |     |     |     | to  |
| --- | --- | --- | --- | --- | ------------- | --- | --- | --- | --- |
outperforms both the classical specialized entity perform multi-hop reasoning on the KG, thereby
linkersandthestandaloneuseoftheLLM-based providingfact-basedanswers.
entityextractor. Thisconclusionissupportedbyob- In this experiment, we validate the necessity
servationsofboththesuccessrateinentityretrieval
ofthetree-structuredsearchprocessinanswering
andtheoverallquery-answeringperformance. commonsensequeriesforquestionansweringand
|     |     |     |     |     | claimverificationtasks. |     | Toachievethis, | wevary |     |
| --- | --- | --- | --- | --- | ----------------------- | --- | -------------- | ------ | --- |
A.2 Sub-graphPruning
themaximumdepthofthesearchtreeandconduct
Due to the potentially large size of the relevant experimentsonthelong-tailsubsetsofthequestion
sub-graphthatisretrieved,itiscrucialtopruneit answeringandclaimverificationdatasets. Results
to enable the use of an LLM-based reasoner that ofthisexperimentarepresentedinTable8.
| hasalimitedcontextlength. |     | However,itiscrucial |     |     |     |     |     |     |     |
| ------------------------- | --- | ------------------- | --- | --- | --- | --- | --- | --- | --- |
Wefirstcompletelyablatethisiterativeprocess
not to prune out the essential KG facts from the andtrytoanswerqueriesonthefirsttry. Resultsof
relevantsub-graphthatareessentialinanswering thisexperimentareshowninthefirstrow(depth =
| thequery. Weconsidertwopossibleapproachesin |     |     |     |     |     |     |     |     |     |
| ------------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
0)whichshowsaconsiderablyloweraccuracythan
| thisregard: |     |     |     |     |                    | R3          |                          |                  |     |
| ----------- | --- | --- | --- | --- | ------------------ | ----------- | ------------------------ | ---------------- | --- |
|             |     |     |     |     | the original       | performance |                          | that we reported | in  |
|             |     |     |     |     | thepaperusingdepth |             | = 2. Byincreasingthetree |                  |     |
• Truncatingtheretrievedsub-graphtofitinthe
depthwhichisequivalenttoanincreasednumberof
contextlength.
iterationsforperformingmulti-hopreasoning,the
|     |     |     |     |     | accuracy | in both tasks | increases, | until it plateaus |     |
| --- | --- | --- | --- | --- | -------- | ------------- | ---------- | ----------------- | --- |
• Usingmoreintelligentapproachessuchasse-
|     |     |     |     |     | atdepth | = 2astherearelimitedqueriesrequiring |     |     |     |
| --- | --- | --- | --- | --- | ------- | ------------------------------------ | --- | --- | --- |
manticsimilaritytoidentifythemorerelevant
| facts. |     |     |     |     | morereasoningstepsonthesetwodatasets. |     |     |     |     |
| ------ | --- | --- | --- | --- | ------------------------------------- | --- | --- | --- | --- |
Theresultsofthisstudyunderscorethecritical
InR3,weusedanapproachbasedontheseman-
importanceoftheiterativeprocessforeffectively
ticsimilaritybetweenthecommonsenseaxiomand answeringmulti-hopcommonsensequerieswithin
| factsintherelevantsub-graph. |     |     | Inordertoverify |     | theR3 |     |     |     |     |
| ---------------------------- | --- | --- | --------------- | --- | ----- | --- | --- | --- | --- |
framework.
theefficacyofthisapproachinpreservingthees-
sentialKGfactswhilepruningtheirrelevantones, B StatisticalAnalysis
weperformanexperimentinwhichweablatethis
semantic similarity-based approach of sub-graph Inordertoevaluatethestatisticalsignificanceofthe
superiorperformanceofR3
| pruning. However,duetothelargesizeofthere- |     |     |     |     |     |     | incomparisontothe |     |     |
| ------------------------------------------ | --- | --- | --- | --- | --- | --- | ----------------- | --- | --- |
baselinesthatwerereportedinTable2ofSection4,
trievedsub-graph,wetruncatethesetoffactstofit
thecontextsizeoftheLLM. weconductedastatisticaltest. Eachsubsetofthis
The results of comparing the outcome of this datasetcontains150queries,resultinginatotalof
600queriesacrossthetwotaskswiththeoriginal
| sub-graph | pruning method | against | the | semantic |     |     |     |     |     |
| --------- | -------------- | ------- | --- | -------- | --- | --- | --- | --- | --- |
similarity-basedapproachusedinR3 arepresented andlong-tailsettings.
in Table 7. Evidently, truncating the sub-graph In this test, we consider queries of each col-
R3
leads to a significant drop in accuracy across all umn with the responses provided by and an-
swersgivenbythebest-performingbaselineacross
| dataset splits, | as it often | prunes | essential | facts. |     |     |     |     |     |
| --------------- | ----------- | ------ | --------- | ------ | --- | --- | --- | --- | --- |
Theseresultsconfirmthenecessityofthesub-graph all queries per column, resulting in a total of
pruningapproachemployedinR3 forjudiciously 300 query-answer pairs for each column. Since
selectingthefactsthatareusefulinansweringthe FActScoreisanumericalmetric,weemployedthe
queries. paired t-test to obtain the statistical significance,
whilefortheAccuracyandReasoningmetrics,we
A.3 IterativeProcessforAnswering
utilizedMcNemar’stest(alsoforpaireddata)con-
Multi-hopQueries sideringthebinarynatureofthedata. Wealsotried
R3 isequippedwithatree-structuredsearchmech- calculatingtheFisher’sexacttestanditprovided
anismforansweringqueries. Asillustratedinthe muchmorefavorablep-valuesindicatingastronger
|             | R3        |         |        |        | significanceofR3’ssuperiority,butwedonotbe- |     |     |     |     |
| ----------- | --------- | ------- | ------ | ------ | ------------------------------------------- | --- | --- | --- | --- |
| workflow of | in Figure | 1, each | branch | of the |                                             |     |     |     |     |
treeundergoesaniterativeprocessofsub-graphre- lieveitisappropriateforthispairedcomparisonof
trievalandpruning,attemptingtoanswerthequery, eachmethodonthesamequeriesandtherefore,do
6614

|     |                                  |     |     |     | QuestionAnswering  |     | ClaimVerification |           |
| --- | -------------------------------- | --- | --- | --- | ------------------ | --- | ----------------- | --------- |
|     |                                  |     |     |     | Original Long-Tail |     | Original          | Long-Tail |
|     | R3withtruncationinsteadofpruning |     |     |     | 0.527 0.480        |     | 0.726             | 0.800     |
R3
|     |     |     |     |     | 0.820 0.727 |     | 0.846 | 0.853 |
| --- | --- | --- | --- | --- | ----------- | --- | ----- | ----- |
Table7: AccuracyofR3comparedtoitsvariantinwhichsemanticsimilarity-basedsub-graphpruningisreplaced
ThesignificantdropintheperformanceofR3afterablatingthesub-graphpruningapproachisdue
withtruncation.
tothelossofessentialKGfactsduetonaivetruncation.
|     |     | ReasoningTreeDepth |     | QuestionAnswering |       | ClaimVerification |       |     |
| --- | --- | ------------------ | --- | ----------------- | ----- | ----------------- | ----- | --- |
|     |     |                    | 0   |                   | 0.473 |                   | 0.620 |     |
|     |     |                    | 1   |                   | 0.553 |                   | 0.707 |     |
|     |     |                    | 2   |                   | 0.727 |                   | 0.853 |     |
|     |     |                    | 3   |                   | 0.733 |                   | 0.860 |     |
Table8: AccuracyofR3 inquestionansweringandclaimverificationtasksagainstthedepthofreasoningtree
generallyincreaseswiththeincreasedtreedepth. Thesignificantgapbetweenthereasoningdepthof0andthe
reasoningdepthof2whichistheoriginalR3resultsindicatestheimportanceoftheiterativemechanismofR3for
answeringmulti-hopqueries.
|     |              |     | Accuracy |           | FActScore          |         | Reasoning |           |
| --- | ------------ | --- | -------- | --------- | ------------------ | ------- | --------- | --------- |
|     |              |     | Original | Long-Tail | Original Long-Tail |         | Original  | Long-Tail |
|     | p-value      |     | 0.1868   | 0.1443    | 0.0004             | 0.00007 | 0.0290    | 0.0606    |
|     | BestBaseline |     | KAPING   | KAPING    | KAPING KAPING      |         | 2-shotCoT | 2-shotCoT |
Table9: ResultsofthestatisticaltestsbetweentheoutputsofR3andthebest-performingbaselineacrossallqueries
percolumn.
notincludeitsresults. Insummary,thisstatisticalanalysisshowsthat
R3potentiallyoutperformsandatleastmatchesthe
Resultsofthep-valuesreflectingthestatistical
Accuracyofstate-of-the-artmethodsanditstatisti-
| significance | test | are presented | in Table | 9. While |     |     |     |     |
| ------------ | ---- | ------------- | -------- | -------- | --- | --- | --- | --- |
callysignificantlyreducessourcesofhallucination
| the p-values | are | not high | enough to | make strong |     |     |     |     |
| ------------ | --- | -------- | --------- | ----------- | --- | --- | --- | --- |
onthreeoutofthefourdatasets(andalmostsignif-
| statisticalclaimsthatR3 |     |     | performsstatisticallysig- |     |     |     |     |     |
| ----------------------- | --- | --- | ------------------------- | --- | --- | --- | --- | --- |
icantlyonthefourth).
nificantlybetterthanthebestbaselineintermsof
| Accuracy, | we note | that | the purpose | of “Right | for |     |     |     |
| --------- | ------- | ---- | ----------- | --------- | --- | --- | --- | --- |
C OverridingLLMMisbeliefswithKG
| the Right | Reasons” | (R3) | is to maintain | the accu- |     |     |     |     |
| --------- | -------- | ---- | -------------- | --------- | --- | --- | --- | --- |
Facts
racyofexistingstate-of-the-artQAmethodswhile
reducing fact and reasoning hallucinations. Fact Duringtheirtrainingprocess,LLMsacquiresub-
andreasoninghallucinationsarerespectivelymea- stantial factual knowledge about various objects
suredbytheFActScoreandReasoningmetrics. On and entities. However, as observed in the exper-
these metrics, p-value results show very encour- imental results presented in Section 4, utilizing
ReasoningresultsforR3
agingstatisticalresults. their internal knowledge in answering common-
appearsignificantlybetterfortheOriginalversions sensequeriesispronetohallucination,especially
of the datasets (p-value < 0.05) and just miss the in answering queries about long-tail entities. R3
0.05significancelevelfortheLong-tailversionby addressesthischallengebygroundingitsanswers
asmallmargin. Critically, fortheFActScore, R3 onthefactsfromtheKGthataremorereliable. In
outperformsthebestbaselinewithhighstatistical fact,itislikelythattheinternalknowledgeofthe
LLMdisagreeswithafactthatR3obtainsfromthe
significance(p-value<0.001)forboththeOriginal
KG,andinthesecircumstances,R3
and Long-tail variants of our datasets indicating overridesthe
a highly statistically significant reduction in fact LLM’spotentiallymistakenbeliefwithacredible
hallucinationforR3. KGfact,whichresultedinhigheraccuracyandfac-
6615

tualcorrectnessoftheR3’sresponsescomparedto
theLLM-basedbaselines.
| InordertoverifythatR3 |         |        | succeedsinoverriding |            |           |
| --------------------- | ------- | ------ | -------------------- | ---------- | --------- |
| mistaken              | beliefs | of the | LLM                  | by correct | and rele- |
vantfactsfromtheKGandobservethecontribution
ofthisapproachtothesuperiorperformanceofR3,
inthissection,weprovideanecdotalexamplesof
responsesprovidedbyR3andtheLLM-basedbase-
| linesto30queries. |     | Thesequeriesarechosenfrom |     |     |     |
| ----------------- | --- | ------------------------- | --- | --- | --- |
thesubsetsofthebenchmarkdatasetsonwhichR3
| outperforms | the | baselines, | i.e., | question | answer- |
| ----------- | --- | ---------- | ----- | -------- | ------- |
ingtaskinbothoriginalandlong-tailsettingsand
| theclaim  | verification |             | task inthe | long-tailsetting. |              |
| --------- | ------------ | ----------- | ---------- | ----------------- | ------------ |
| We choose | these        | queries     | among      | the               | queries that |
| the LLM   | bases        | its answers | on         | facts             | and does not |
| respond   | by just      | “Yes”,      | “No”,      | or “I             | don’t know”. |
Wealsoprovidethecompletesetsofresponsespro-
videdbyR3
andallbaselinesonallqueriesinour
repository.
| Each | anecdotal | example | is  | provided | in a table |
| ---- | --------- | ------- | --- | -------- | ---------- |
thatcontainsthequery,thecorrectanswer,andthe
setofresponsesprovidedbyeachmethodfollowed
| by a brief | discussion |     | comparing | those | responses.   |
| ---------- | ---------- | --- | --------- | ----- | ------------ |
| Correct    | facts that | are | used in   | each  | response are |
indicatedbygreentextcolourandincorrectones
| areshowninred. |     | Also,incorrectreasoningsteps |     |     |     |
| -------------- | --- | ---------------------------- | --- | --- | --- |
areindicatedbyredunderline.
6616

QuestionAnswering: Long-tail
Query: CouldsomeoneinVaughantakeataxitotheJamjureeArtGallery? (No)
0-Shot CoT: First, let’s find out if there are taxis available in Vaughan. In Vaughan, taxis are
availableforlocaltransportation. Next,let’scheckthelocationoftheJamjureeArtGallerytosee
ifit’swithinareasonabledistancefromVaughan. TheJamjureeArtGalleryislocatedinToronto,
whichisadjacenttoVaughan. Withthisinformation,itisreasonabletoconcludethatsomeonein
VaughancouldtakeataxitotheJamjureeArtGallery,giventheproximityofthelocations. Final
answer: Yes.
2-ShotCoT:TheJamjureeArtGalleryislocatedinBangkok,Thailand. VaughanisacityinOntario,
Canada. Since they are in different countries and continents, it is not feasible to take a taxi from
VaughantotheJamjureeArtGallery. FinalAnswer: No.
R3: Basedonthegeneralrule,theJamjureeArtGallerymustbewithinareasonabledistancefrom
VaughanandaccessiblebyroadforsomeoneinVaughantotakeataxitoit. Fact“(JamjureeArt
Gallery,country,Thailand)”tellsusthattheJamjureeArtGalleryislocatedinThailand,whichis
quitefarfromVaughan,Ontario,Canada. Fact“(Vaughan,is,cityinOntario,Canada)”tellsusthat
VaughanisacityinOntario,Canada. Althoughthefactsdon’tprovideexplicitinformationabout
thedistancebetweenVaughanandtheJamjureeArtGallery,wecanmakeaplausibleassumption
basedongeneralknowledge. ThailandislocatedontheothersideoftheworldfromCanada,andit
isnotwithinareasonabledistanceforsomeoneinVaughantotakeataxitotheJamjureeArtGallery.
Therefore,theansweris: No,someoneinVaughancannottakeataxitotheJamjureeArtGallery.
Inthe0-shotresponse,theLLMhashallucinatedaboutthelocationoftheJamjureeArtGalleryand
believedthatitislocatedinToronto. Althoughthereasoningaboutthepossibilityoftravelingby
taxibetweentwoadjacentcitiesiscorrect,thehallucinatedfacthasledtoanincorrectfinalanswer.
The2-shotresponseiscorrectanddoesnotincludethishallucination. Theresponseprovidedby
R3 iscompletelycorrectandbasedonKGfacts. Also,itpointstothespecificKGfactsusedinits
reasoningwhichallowsforverificationoftheresponse.
Query: Isthe“It’sHyorish”anolderalbumthan“Nasimevasl”? (No)
0-ShotCoT:First,let’sdeterminethereleasedatesofthealbums“It’sHyorish”and“Nasimevasl”.
Oncewehavethisinformation,wecancomparethereleasedatestoseewhichalbumisolder. The
album“It’sHyorish”byNasimevaslwasreleasedonOctober30,2019. Ontheotherhand,“Nasime
vasl”byMarjanFarsadwasreleasedonNovember23,2017. Comparingthereleasedates,“Nasime
vasl” is older than “It’s Hyorish”. Final answer: Yes, “Nasime vasl” is an older album than “It’s
Hyorish”.
2-ShotCoT:Thealbum“It’sHyorish”wasreleasedin1990,while“Nasimevasl”wasreleasedin
1978. Therefore,“It’sHyorish”isnotolderthan“Nasimevasl”. FinalAnswer: No.
R3: Based on the general rule, we need to compare the publication dates of “It’s Hyorish” and
“NasimeVasl”todeterminewhichalbumisolder. Fact“(It’sHyorish,publicationdate,2008)”tells
usthat"It’sHyorish"waspublishedin2008,andFact“(NasimeVasl,publicationdate,2003/05/21)”
tellsusthat“NasimeVasl”wasalsopublishedin2003. Comparingthepublicationdates,wecansee
that“NasimeVasl”waspublishedearlierthan“It’sHyorish”. Therefore,theansweris: No,“Nasime
Vasl”isanolderalbumthan“It’sHyorish”.
6617

Inthe0-shotCoTresponse,theLLMmakesmultiplefactualhallucinations. First,itstatesthat“It’s
Hyorish”isanalbumby“Nasimevasl”,whereassuchsingerdoesnotexistand“Nasimevasl”isthe
nameofanotheralbum. Italsostatesthat“It’sHyorish”wasreleasedonOctober30,2019whichis
incorrect. Italsostatesthat“Nasimevasl”isanalbumby“MarjanFarsad”andthat“Nasimevasl”
wasreleasedonNovember23,2017,whicharebothincorrect. Also,inthe2-shotCoTresponse,the
LLMhallucinatedaboutthedatesthetwoalbumswerereleased. However,R3 correctlyoverrides
themistakenbeliefsoftheLLMbyKGfactsandprovidesthecorrectanswer.
Query: DidIlaryBlasicelebrateasilveranniversarywithFrancescoTotti? (No)
0-Shot CoT: To the best of my knowledge, Ilary Blasi did celebrate a silver anniversary with
Francesco Totti. “Silver anniversary” usually refers to the 25th anniversary, and in this context
couldimplyasignificantmilestoneintheirrelationship. IlaryBlasiandFrancescoTottiareknown
publicfiguresandhavebeenmarriedformanyyears,soitispossiblethattheycelebratedasilver
anniversary.
2-ShotCoT:Yes. IlaryBlasiandFrancescoTotticelebratedtheirsilver(25th)anniversaryin2020.
Finalanswer: Yes.
R3: Accordingtothegeneralruleprovided,IlaryBlasiandFrancescoTottimusthavebeenmarried
for25yearstocelebrateasilveranniversarytogether. Fact“(FrancescoTotti,spouse,IlaryBlasi;
start time, 2005; end cause, divorce; end time, 2022)” states that Ilary Blasi and Francesco Totti
weremarriedfrom2005to2022,whichisatotalof17years,not25years. Therefore,basedonthe
information given, Ilary Blasiand Francesco Totti did notcelebrate a silveranniversary together.
Hence,theansweris: No,IlaryBlasididnotcelebrateasilveranniversarywithFrancescoTotti.
Both0-Shotand2-ShotresponseshallucinateaboutthelengthofIlaryBlasiandFrancescoTotti’s
marriage. However,R3 overridesthemistakenbeliefbygroundingitsresponseontheKGfactabout
theirdivorcewhichleadstocorrectlycalculatingtheirlengthofmarriage.
Query: IsitlikelyforthedirectorofDemitriCantemirtofastduringRamadan? (No)
0-ShotCoT:First,DemitriCantemirwasaMoldavianhistorian,composer,andscholarofOttoman
historyandmusic. ItisknownthathewasofOrthodoxChristianfaith,whichdoesn’trequirefasting
during Ramadan. So, it is unlikely for the director of Demitri Cantemir to fast during Ramadan.
Finalanswer: No.
2-ShotCoT:DemitriCantemirwasaMoldavianphilosopher,historian,composer,andamanofarts.
HewasalsoaconverttoIslamandlivedinConstantinopleforaportionofhislife. SinceRamadan
isanimportantmonthoffastingforMuslims, itislikelythatDemitriCantemir, beingaMuslim,
observedfastingduringRamadan. Finalanswer: Yes.
R3: The general rule states that the likelihood of the director of a film fasting during Ramadan
dependsonwhetherthedirectorobservestheIslamicfaith. Fact“(DemitriCantemir,director,Vlad
Iovi¸ta˘)” tells us that Vlad Iovi¸ta˘ is the director of Demitri Cantemir. Fact “(Vlad Iovi¸ta˘, religion
orworldview,EasternOrthodoxChurch)”tellsusthatVladIovi¸ta˘’sreligionisEasternOrthodox
Church,notIslam. SinceVladIovi¸ta˘ doesnotfollowtheIslamicfaith,itisnotlikelyforhimtofast
duringRamadan. Therefore,theansweris: No,itisnotlikelyforthedirectorofDemitriCantemir
tofastduringRamadan.
6618

The 0-Shot answer includes a reasoning error. Although the facts it provides about who Demitri
Cantemirwasandthereligionthathebelievedinarecorrect,thefactthatDemitriCantemirfollowed
Christianity does not imply that the director of a movie about him is not likely to fast. Also, the
response provided by 2-Shot CoT contains the same reasoning error by using information about
DemitriCantemir’sreligousbeliefstojudgeaboutthereligousbeliefsofthedirectorofthemovie
about him. This response also includes a hallucinated fact about Demitri Cantemir’s conversion
toIslam. TheresponseprovidedbyR3 fixesbotherrors. First,ithasamechanismforidentifying
therequiredmissinginformationthatallowsittoanswermulti-hopquestionssuchasthisone. R3
determinesthatinformationaboutDemitriCantemir’sdirectorisrequiredandcorrectlyretrieves
therequiredinformationfromtheKGandusesittogeneratetheresponse. Second,theresponseis
groundedontheKGfactsanddoesnotcontainhallucinationsastheoneinthe2-shotCoT.
Query: WasDaryaDadvarfromthesamecitythatusedtobeAfsharidEmpire’scenterofpower?
(Yes)
0-ShotCoT:ThecapitaloftheAfsharidEmpirewasMashhad. DaryaDadvarwasborninMashhad.
Therefore,theanswerisYes.
2-ShotCoT:DaryaDadvarwasborninRasht,Iran. ThecenterofpoweroftheAfsharidEmpire
wasinMashhad. SinceRashtandMashhadaredifferentcities,DaryaDadvarisnotfromthesame
citythatusedtobethecenterofpoweroftheAfsharidEmpire. FinalAnswer: No.
R3: BasedonGeneralRule“DaryaDadvarmusthavebeenborninthecitythatusedtobethecenter
ofpoweroftheAfsharidEmpiretobefromthesamecity.”,DaryaDadvarmusthavebeenbornin
thecitythatusedtobethecenterofpoweroftheAfsharidEmpiretobefromthesamecity. Fact
“(DaryaDadvar,placeofbirth,Mashhad)”tellsusthatDaryaDadvarwasborninMashhad. Fact
“(AfsharidEmpire,capital,Mashhad)”tellsusthatMashhadwasthecapitaloftheAfsharidEmpire.
Therefore,theansweris: Yes,DaryaDadvarisfromthesamecitythatusedtobethecenterofpower
oftheAfsharidEmpire,whichisMashhad.
Theresponseprovidedby0-ShotCoTiscorrect,buttheoneprovidedby2-ShotCoT,containsa
factual hallucination about the birthplace of Darya Dadvar which shows that LLM is unreliable
in answering. However, R3 provides a response which is grounded on the KG and overrides the
incorrectbeliefthatwasreflectedin2-ShotCoT’sresponse.
Query: DoesToyoharuTsutsui’salmamaterhavemorehistorythanNewfoundlandandLabrador?
(Yes)
0-Shot CoT: 1. Toyoharu Tsutsui’s alma mater is Seijo University, which was founded in 1943.
2. Newfoundland and Labrador is a province in Canada, known for its rich history dating back
thousandsofyears,includingIndigenouspeoples,Vikingsettlements,andEuropeanexploration.
Basedonthisinformation,itisclearthatNewfoundlandandLabradorhassignificantlymorehistory
thanSeijoUniversity.
2-ShotCoT:ToyoharuTsutsui’salmamaterisTokyoUniversity,whichwasestablishedin1877.
NewfoundlandandLabradorhasalonghistorydatingbackthousandsofyears,includingIndigenous
occupation,Vikingsettlements,andEuropeanexploration. Therefore,NewfoundlandandLabrador
hasalongerhistorythanTokyoUniversity. Finalanswer: No.
6619

R3: TodeterminewhetherToyoharuTsutsui’salmamaterhasmorehistorythanNewfoundlandand
Labrador,weneedtocomparethehistoriesofboth. Fact“(NewfoundlandandLabrador,inception,
1949/03/31)”tellsusthatNewfoundlandandLabradorwasestablishedin1949. Ontheotherhand,
Fact“(HarvardUniversity,inception,1636/09/08)”tellsusthatHarvardUniversitywasfoundedin
1636. Therefore,basedontheinformationprovided,HarvardUniversityhasalongerhistorythan
NewfoundlandandLabrador. Therefore,theansweris: Yes,HarvardUniversityhasmorehistory
thanNewfoundlandandLabrador.
Intheresponseprovidedby0-ShotCoT,theLLMhallucinatesaboutToyoharuTsutsui’salmamater,
and also the date Seijo University was founded. Also, there are hallucinations about Toyoharu
Tsutsui’salmamater,andthedateTokyoUniversitywasfoundedin2-ShotCoT.Intheresponse
providedbyR3,thesehallucinationsarecorrectlyoverriddenbytherespectiveKGfacts,andthe
finalprovidedanswerisalsocorrected.
Query: CouldpeoplehavereadMjegullduringthePerakwar? (No)
0-ShotCoT:Toanswerthequestion,wecantakeastepbystepapproach. First,let’sdeterminethe
timeperiodofthePerakwarandthepublicationdateofMjegull. Thenwecaninvestigateifthere
wereanycircumstancesthatcouldhaveallowedpeopletoreadMjegullduringthePerakwar. The
PerakWaroccurredfrom1875to1876. Meanwhile,Mjegullwaspublishedin1884. Basedonthe
timeline,itisunlikelythatpeoplecouldhavereadMjegullduringthePerakwar,asthepublication
ofMjegullcameafterthewar. Finalanswer: No.
2-ShotCoT:Mjegullisafictionallanguageusedinthevideogame"TheWitcher3: WildHunt". As
thePerakWartookplaceinthelate19thcentury,itisimpossibleforpeopletohavereadMjegull
duringthattimebecauseitisacreationforamodernvideogame. Finalanswer: No.
R3: The general rule states that people during the Perak War must have had access to the novel
Mjegull,whichwaspublishedin2009,inordertohavereaditduringthattime. Fact“(PerakWar,
endtime,1876)”tellsusthatthePerakWarendedin1876,whileFact“(Mjegull,publicationdate,
2009;placeofpublication,Tirana)”statesthatthenovelMjegullwaspublishedin2009. Sincethe
publicationdateofMjegullismuchlaterthanthePerakWar,itisnotpossibleforpeopleduringthe
PerakWartohavereadMjegull. Therefore,theansweris: No,peoplecouldnothavereadMjegull
duringthePerakWar.
The 0-Shot CoT response includes a factual hallucination about the time Mjegull was published.
Also,2-ShotCoTresponseincludesanerrorabouttheMjegullentityandattributesittoafictional
languagewhereasMjegullherereferstoabook. BygroundingtheresponseontheKG,R3 succeeds
inprovidingacorrectanswertothequestionwhichiscorrectintermsofreasoningandfactuality.
Query: DidIvanShuiskysufferthesamefateasBennyFrey? (Yes)
0-ShotCoT:First,let’sidentifythefateofBennyFrey. BennyFreywasacharacterinthetelevision
show"Hannibal"whometatragicend. Now,let’sdeterminethefateofIvanShuisky. IvanShuisky
wasahistoricalfigureinthe16thcenturywhowasakeyfigureinRussianpoliticsandwaseventually
executed. Therefore,thefatesofIvanShuiskyandBennyFreyaredifferent. Finalanswer: No.
2-ShotCoT:IvanShuiskyandBennyFreyarenothistoricalfiguresnoraretheycommonlyknown
individuals. Therefore,Idon’thaveinformationtodetermineiftheysufferedthesamefate. Final
answer: Idon’tknow.
6620

R3: Accordingtothegeneralrule,IvanShuiskyandBennyFreymusthavethesamecauseofdeath
for them to have suffered the same fate. Fact “(Ivan Shuisky, cause of death, carbon monoxide
poisoning)” states that Ivan Shuisky’s cause of death was carbon monoxide poisoning, and Fact
“(BennyFrey,causeofdeath,carbonmonoxidepoisoning)”statesthatBennyFrey’scauseofdeath
was also carbon monoxide poisoning. Therefore, since both Ivan Shuisky and Benny Frey had
thesamecauseofdeath,theysufferedthesamefate. Therefore,theansweris: Yes,IvanShuisky
sufferedthesamefateasBennyFrey.
The0-ShotCoTresponseincludesanerrorinidentifyingwhoBennyFreywas. Althoughitcorrectly
identifieswhoIvanShuiskywas,ithallucinatesaboutIvanShuisky’smannerofdeath. In2-Shot
CoTresponse,theLLMrefrainsfromansweringbystatingthatitisnotfamiliarwiththetwoentities
andtheirfates. TheresponseprovidedbyR3 utilizestheKGtoidentifythetwoentitiesandobtain
informationabouttheirmannerofdeath,thereforeleadingtoacorrectandgroundedresponse.
Query: CouldKakáhaveboughtacarfromJordanMotorCarCompany? (No)
0-ShotCoT:TodetermineifKakácouldhaveboughtacarfromJordanMotorCarCompany,we
needtoconsiderthelocationandtimeline. Kaká,theBrazilianfootballer,playedforOrlandoCity
SCintheMLSfrom2014to2017,andJordanMotorCarCompanyisbasedinJordan. Therefore,it
ispossiblethathecouldhavepurchasedacarfromthiscompanyifhehadbeeninJordanduring
thattime. FinalAnswer: Yes.
2-Shot CoT: Kaká, the Brazilian footballer, could have bought a car from Jordan Motor Car
Companyifthecompanyproducedandsoldcarswhilehewasactiveandinterestedinpurchasing
one. However,asfarasIamaware,thereisnopublicinformationsuggestingKakápurchasedacar
fromJordanMotorCarCompany. Therefore,withoutspecificinformation,Idon’tknowifKaká
couldhaveboughtacarfromJordanMotorCarCompany. FinalAnswer: Idon’tknow.
R3: Based on General Rule “Jordan Motor Car Company must have been active during Kaká’s
lifetimeforhimtohavepotentiallyboughtacarfromthem.",JordanMotorCarCompanymusthave
beenactiveduringKaká’slifetimeforhimtohavepotentiallyboughtacarfromthem. Fact“(Jordan
Motor Car Company, inception, 1916)” tells us that Jordan Motor Car Company was founded in
1916andFact“(JordanMotorCarCompany,dissolved,abolishedordemolisheddate,1931/04/00)”
tells us that it was dissolved in 1931. Fact “(Kaká, is, Brazilian footballer, born 1982)” tells us
thatKakáwasbornin1982, whichmeanshewasbornafterthedissolutionofJordanMotorCar
Company. Therefore,JordanMotorCarCompanywasnotactiveduringKaká’slifetime. Therefore,
theansweris: No,KakácouldnothaveboughtacarfromJordanMotorCarCompany.
Theresponseprovidedby0-ShotCoTincludesafactualhallucinationaboutthelocationofJordan
Motor Car Company which was in fact located in the United States and not Jordan. The 2-Shot
CoTisnotabletogiveacertainanswertothequestionbecauseitisnotawareofthecarcompany’s
activity period. However, R3 succeeds in providing a correct answer by retrieving the required
informationfromtheKGandcorrectlyreasoningovertheobtainedinformation.
Query: Could Liau Hiok-hian and Virginia Raggi have met while they both held the position of
councilmember? (No)
6621

0-Shot CoT: First, let’s establish who Liau Hiok-hian and Virginia Raggi are. Liau Hiok-hian
is a Malaysian economist and politician, known for his involvement with the Malaysian Chinese
Association(MCA).VirginiaRaggiisanItalianpoliticianwhoservedastheMayorofRome. Given
thatLiauHiok-hianisfromMalaysiaandRaggiisfromItaly,itisunlikelythattheywouldhave
metduringtheirtimeascouncilmembers,astheywouldhavebeenholdingpositionsindifferent
countries. Therefore,itisimprobablethattheycouldhavemetwhilebothholdingthepositionof
councilmember. Finalanswer: No.
2-ShotCoT:LiauHiok-hianisacouncilmemberinMalaysia,whileVirginiaRaggiisacouncil
memberinItaly. Sincetheyareindifferentcountries,itisunlikelythattheycouldhavemetwhile
holdingthepositionofcouncilmember. Finalanswer: No.
R3: Based on General Rule “Liau Hiok-hian and Virginia Raggi must have served as council
membersduringoverlappingtimeperiodstohavetheopportunitytomeetwhileholdingtheposition
ofcouncilmember.”todetermineifLiauHiok-hianandVirginiaRaggicouldhavemetwhilethey
bothheldthepositionofcouncilmember,weneedtocheckiftheirtimeperiodsascouncilmembers
overlap. Fact “(Virginia Raggi, position held, council member; start time, 2013/06/10; end time,
2015/10/30;of,Rome)”statesthatVirginiaRaggiheldthepositionofcouncilmemberinRomefrom
June10,2013,toOctober30,2015. Fact“(LiauHiok-hian,positionheld,MemberofYunlinCounty
Council; start time, 2018/12/25; elected in, 2018 Yunlin County Council election; parliamentary
group, New Power Party; electoral district, 1st Constituency of Regional Councilors of Yunlin
County;parliamentaryterm,19thYunlinCountyCouncil;endtime,2022/12/24)”statesthatLiau
Hiok-hian held the position of Member of Yunlin County Council from December 25, 2018, to
December24,2022. Sincetheirtimeperiodsascouncilmembersdonotoverlap,LiauHiok-hianand
VirginiaRaggicouldnothavemetwhiletheybothheldthepositionofcouncilmember. Therefore,
theansweris: No,LiauHiok-hianandVirginiaRaggicouldnothavemetwhiletheybothheldthe
positionofcouncilmember.
Responsesofboth0-ShotCoTand2-ShotCoTcontainfactualhallucinationsaboutLiauHiok-hian.
Theyalsocontainareasoningerrorbystatingthatpoliticiansfromdifferentcountriesareunlikely
tomeet. However,R3 groundsitsreasoningontheKGandoverridestheLLM’sincorrectbeliefs
about Liau Hiok-hian by facts from the KG and also provides a correct commonsense reasoning
performancebysurfacingthecommonsenseaxiomfromtheLLM.
QuestionAnswering: Original
Query: WasDorotheaWendlingfromsameplacePorscheoriginated? (Yes)
0-ShotCoT:TodetermineifDorotheaWendlingwasfromthesameplaceastheoriginofPorsche,
we need to find out where Dorothea Wendling was from and then compare it to the place where
Porscheoriginated. InitialresearchshowsthatDorotheaWendlingwasborninAugsburg,Germany.
Porsche’soriginscanbetracedbacktothecityofMaffersdorf(nowlocatedintheCzechRepublic)
where Ferdinand Porsche founded his company. Therefore, based on this information, Dorothea
WendlingwasnotfromthesameplaceastheoriginofPorsche. Finalanswer: No.
2-ShotCoT:DorotheaWendling,arenownedoperasinger,wasborninReims,France,whilethe
PorschecompanywasfoundedinStuttgart,Germany. Thereisnoapparentconnectionbetweenthe
birthplacesofDorotheaWendlingandtheoriginofPorsche. Finalanswer: No.
6622

R3: Thegeneralrule“DorotheaWendlingmusthavebeenborninthesameplacewherePorsche
originatedforthemtobefromthesameplace.”statesthatDorotheaWendlingmusthavebeenborn
inthesameplacewherePorscheoriginatedforthemtobefromthesameplace. Fact“(Dorothea
Wendling, place of birth, Stuttgart)” tells us that Dorothea Wendling was born in Stuttgart. Fact
“(Porsche,locationofformation,Stuttgart)”tellsusthatPorschewasoriginatedinStuttgartaswell.
Therefore,basedontheinformationprovided,DorotheaWendlingwasindeedfromthesameplace
wherePorscheoriginated. Therefore,theansweris: Yes.
The0-ShotCoTresponsecontainsfactualhallucinationsaboutthebirthplaceofDorotheaWendling
andtheplacewerePorscheoriginatedfrom. Likewise,2-ShotCoTcontainsahallucinationabout
thebirthplaceofDorotheaWendling. Thesehallucinatedfactsarecorrectlyoverriddenbyproper
KGfactsintheresponseprovidedbyR3.
Query: CouldCarlFriedrichGaussspeaktosomeone100milesaway? (No)
0-Shot CoT: To communicate with someone 100 miles away, Carl Friedrich Gauss would have
neededtouseamethodoflong-distancecommunicationsuchasaletter,messenger,oratelegraph,
ashelivedbeforetheinventionofmoderntelecommunications. Gausscouldnothavespokendirectly
tosomeone100milesawaywithouttheaidoftechnology. Finalanswer: No.
2-ShotCoT:CarlFriedrichGauss,amathematicianandscientist,isknownforhisworkinmany
areas,includingmathematics,physics,andastronomy. Whilehemadeimportantcontributionsto
theunderstandingofelectromagnetismandcouldtheoreticallyhavetransmittedmessagesoverlong
distanceswiththerightequipment,thereisnohistoricalrecordofhimactuallydemonstratingthe
abilitytospeaktosomeone100milesaway. Finalanswer: Idon’tknow.
R3: Accordingtothegeneralrule,CarlFriedrichGaussmusthavelivedduringatimewhenlong-
distancecommunicationtechnologyallowedspeakingtosomeone100milesawaytobeabletodo
so. Fact“(CarlFriedrichGauss,is,Germanmathematicianandphysicist(1777–1855))”tellsusthat
CarlFriedrichGausslivedfrom1777to1855. Duringthistimeperiod,long-distancecommunication
technologydidnotexistinawaythatwouldallowspeakingtosomeone100milesaway. Therefore,
basedonthegeneralruleandthetimeperiodinwhichCarlFriedrichGausslived,theansweris: No,
CarlFriedrichGausscouldnotspeaktosomeone100milesaway.
Allthreeresponsesarecorrect. However,theresponseprovidedbyR3ismorespecificbymentioning
theexactusedfact(dateofbirthanddeathofCarlFriedrichGauss)thatmakestheresponseeasily
verifiable.
6623

Query: DoesAdamSandlerskipcelebratingEaster? (Yes)
0-ShotCoT:First,weshouldconsiderwhetherAdamSandlercelebratesEasteratall. Thereisno
publicinformationindicatingthathedoesnotcelebrateEaster. Additionally,manypeopleofvarious
backgroundsandbeliefschoosetocelebrateEasterindifferentways,soitwouldn’tbeaccurateto
assumethathedoesn’tcelebrateit. Therefore,asthereisnoevidencetosuggestthatAdamSandler
skipscelebratingEaster,themostappropriateansweris: No.
2-ShotCoT:AsfarasIknow,thereisnoinformationindicatingthatAdamSandlerskipscelebrating
Easter. It is possible that he may or may not celebrate Easter, but this information is not readily
available. FinalAnswer: Idon’tknow.
R3: ThegeneralruletellsusthattodetermineifAdamSandlerskipscelebratingEaster,weneedto
considerhisreligiousbeliefsandpractices. Fact“(AdamSandler,religionorworldview,Judaism)”
statesthatAdamSandlerisJewish. EasterisaChristianholydaythatcommemoratestheresurrection
ofJesus. BasedonthefactthatAdamSandlerisJewish,itislikelythathedoesnotcelebrateEaster
asitisnotapartoftheJewishreligioustradition. Therefore,theansweris: Yes,AdamSandlermost
likelyskipscelebratingEasterduetohisJewishfaith.
Since LLM is not familiar with Adam Sandler, it cannot provide the correct answer in either the
0-Shotor2-ShotCoTsettings. However,R3 isabletocorrectlyidentifytherelevantKGfactsabout
hisreligiousbeliefsandprovidethecorrectfinalanswer.
Query: DidMelaniaTrumphavesameprofessionasOlgaKurylenko? (Yes)
0-Shot CoT: Melania Trump was a model before becoming the First Lady of the United States,
whileOlgaKurylenkoisanactressknownforherrolesinmovies. So,theydidnothavethesame
profession. FinalAnswer: No.
2-ShotCoT:No,MelaniaTrumpandOlgaKurylenkohavedifferentprofessions. MelaniaTrumpis
aformermodelandtheformerFirstLadyoftheUnitedStates,whileOlgaKurylenkoisanactress.
Finalanswer: No.
R3: According to the general rule, Melania Trump and Olga Kurylenko must share at least one
common profession to have the same profession. Facts “(Melania Trump, occupation, jewelry
designer)”,“(MelaniaTrump,occupation,model)”,“(MelaniaTrump,occupation,celebrity)”,and
“(MelaniaTrump,occupation,businessperson)”tellusthatMelaniaTrump’sprofessionsinclude
jewelrydesigner,model,celebrity,andbusinessperson. Fact“(OlgaKurylenko,occupation,model)”,
Fact“(OlgaKurylenko,occupation,actor)”,Fact“(OlgaKurylenko,occupation,filmactor)”,and
Fact“(OlgaKurylenko,occupation,voiceactor)”tellusthatOlgaKurylenko’sprofessionsinclude
model,actor,filmactor,andvoiceactor. SincebothMelaniaTrumpandOlgaKurylenkosharethe
profession of a model, they have at least one common profession. Therefore, the answer is: Yes,
MelaniaTrumphadthesameprofessionasOlgaKurylenko.
Theanswersprovidedbyboth0-Shotand2-ShotCoTmethodsareincorrectbecausetheLLMdoes
notknowthatOlgaKurylenkoisalsoamodel. Byobtainingthefactsaboutallofheroccupations
fromtheKG,R3 canprovidethecorrectanswer.
Query: CanIholdBinginabasket? (No)
0-Shot CoT: First, we need to clarify what "Bing" refers to. Assuming Bing as a small pet or
object,itwoulddependonthesizeofBingandthetypeofbasket. IfBingissmallandthebasketis
appropriatelysizedandsafeforBing,thenitmightbepossibletoholdBinginabasket. However,
ifBingisanobjectorit’snotsafeorsuitableforBingtobeheldinabasket,thenitwouldn’tbea
goodidea. Finalanswer: Itdepends. IfBingissmallandthebasketissuitable,thenpossibly,yes. If
not,thenno.
6624

2-ShotCoT:BingisasearchengineownedbyMicrosoftandexistsasadigitalplatform. So,no,
youcannotholdBinginabasket. Finalanswer: No.
R3: ThegeneralrulestatesthatBinginthiscontextreferstoMicrosoftBing,whichisanonline
platformandnotaphysicalobjectthatcanbeheldinabasket. Therefore,consideringthenatureof
Bingasanonlineplatform,itisnotpossibletoholdBinginabasket. Thequestionisaskingabout
holdingBing,theonlineplatform,inabasket,whichisnotfeasible. Therefore,theansweris: No,
youcannotholdBinginabasket.
TheLLMisnotabletogiveacertainanswertothequeryinthe0-ShotCoTsettingasitisunsure
aboutwhat“Bing”refersto. Theresponseprovidedbythe2-ShotCoTiscorrect. Also,sinceR3
utilizesthegroundedKGfacts,itisabletocertainlyidentifywhatBingreferstoandprovidethe
correctanswer.
Query: DidEvanderHolyfieldcompeteinanOlympicshostedinthewesternhemisphere? (Yes)
0-Shot CoT: First, we need to establish if Evander Holyfield competed in the Olympics. Yes,
EvanderHolyfieldcompetedinthe1984SummerOlympicsinLosAngeles,California,whichis
inthewesternhemisphere. Therefore,EvanderHolyfieldcompetedinanOlympicshostedinthe
westernhemisphere. Finalanswer: Yes.
2-ShotCoT:Yes,EvanderHolyfieldcompetedinthe1984SummerOlympics,whichwerehosted
inLosAngeles,California,UnitedStates. Finalanswer: Yes.
R3: The general rule states that Evander Holyfield must have competed in the 1984 Summer
OlympicsheldinthewesternhemisphereforhimtohaveparticipatedinanOlympicshostedinthe
westernhemisphere. Fact“(EvanderHolyfield,participantin,1984SummerOlympics)”confirms
thatEvanderHolyfieldparticipatedinthe1984SummerOlympics. Fact“(EvanderHolyfield,country
ofcitizenship,UnitedStatesofAmerica)”statesthatEvanderHolyfieldisacitizenoftheUnited
States of America. Since the 1984 Summer Olympics were held in Los Angeles, USA, which is
inthewesternhemisphere,EvanderHolyfielddidcompeteinanOlympicshostedinthewestern
hemisphere. Therefore,theansweris: Yes,EvanderHolyfieldcompetedinanOlympicshostedin
thewesternhemisphere.
Allthreemethodsareabletoprovidethecorrectanswertothisquery.
Query: CanLarryKing’sex-wivesformawaterpoloteam? (Yes)
0-ShotCoT:First,let’sdeterminehowmanyex-wivesLarryKinghas. Asofmyknowledgecutoff
dateinSeptember2021,LarryKingwasreportedtohavebeenmarriedeighttimestosevendifferent
women,withoneofthemhemarriedtwice. IfallofLarryKing’sex-wivesarephysicallyableand
willingtoparticipate,theycouldtheoreticallyformawaterpoloteam,asthesporthasnorestrictions
basedonmaritalstatus. Therefore,theansweris: Yes.
2-ShotCoT:LarryKinghashadsevenex-wives. Awaterpoloteamconsistsofsevenplayersinthe
waterandonesubstitute. Therefore,technicallyhisex-wivescouldformawaterpoloteam. Final
answer: yes.
R3: According to the general rule, Larry King’s ex-wives must possess the skills and abilities
requiredtoplaywaterpoloinordertoformawaterpoloteam. However,thefactsprovideddonot
giveanyinformationabouttheskillsorabilitiesofLarryKing’sex-wives. Therefore,wecannot
determinewhetherLarryKing’sex-wivescanformawaterpoloteamornot. Theansweris: Idon’t
know.
6625

Theresponseprovidedbyboth0-ShotCoTand2-ShotCoTarecorrect,exceptthat2-ShotCoThas
an error about the number of substitute players in water polo which is in fact 6. Due to using an
impropercommonsenseaxiom,R3failstoprovidethecorrectanswer. However,insteadofproviding
ahallucinatedanswer,R3 refrainsfromansweringandstatesthatitdoesnotknowtheanswer.
Query: WouldJanetJacksonavoidadishwithham? (Yes)
0-ShotCoT:First,weneedtoconsiderifJanetJacksonfollowsadietaryrestrictionthatprohibitsthe
consumptionofporkorham. Ifshefollowsakosherdietorhasotherpersonalreasonsforavoiding
ham, then it’s possible she would avoid a dish with ham. However, without specific information
aboutherdietarychoices,it’sdifficulttosayforcertain. Therefore,Idon’tknow.
2-ShotCoT:AsJanetJacksonisknowntohavefollowedavegetariandietinthepast,itislikely
thatshewouldavoidadishwithham. Finalanswer: yes.
R3: ThegeneralrulestatesthatJanetJacksonmusthaveaspecificdietaryrestrictionorpersonal
preferenceregardinghamtodetermineifshewouldavoidadishwithham. Fact“(JanetJackson,
religion or worldview, Sunni Islam)” tells us that Janet Jackson follows Sunni Islam. In Islam,
consumingpork,includingham,isprohibited. GiventhatJanetJacksonfollowsSunniIslam,itis
highlylikelythatshewouldavoidadishwithhamduetoreligiousdietaryrestrictions. Therefore,
theansweris: Yes,JanetJacksonwouldavoidadishwithham.’
Explanation: 0-Shot CoT is unable to provide a specific response. Although the final response
providedby2-shotCoTiscorrect,itisbasedonanincorrectreason. TheresponseprovidedbyR3
iscorrectandbasedonthecorrectreasonthatisbasedonafactextractedfromtheKG.
Query: WouldtheauthorofLittleWomenhaverememberedratificationofthe13thAmendment?
(Yes)
0-ShotCoT:First,weneedtoestablishwhen“LittleWomen”waspublishedandwhethertheauthor,
LouisaMayAlcott,wasaliveatthetimeoftheratificationofthe13thAmendment. “LittleWomen”
waspublishedin1868,andthe13thAmendmentwasratifiedbythestatesonDecember6,1865.
Giventhetimeframe, itispossiblethattheauthorwouldhaverememberedtheratificationofthe
13thAmendment. Finalanswer: Yes.
2-ShotCoT:LouisaMayAlcott,theauthorofLittleWomen,wasaliveandactivelywritingduring
thetimeoftheAmericanCivilWarandthesubsequentratificationofthe13thAmendment,which
abolishedslavery. Therefore,itislikelythatshewouldhaverememberedtheratificationofthe13th
Amendment. FinalAnswer: Yes.
R3: LouisaMayAlcottwasbornin1832anddiedin1888. TheThirteenthAmendmenttotheUnited
StatesConstitutionwasratifiedin1865. SinceLouisaMayAlcottwasaliveandcognizantduring
thetimeoftheratificationofthe13thAmendment,itisplausiblethatshewouldhaveremembered
it. Therefore, the answer is: Yes, the author of Little Women, Louisa May Alcott, would have
rememberedtheratificationofthe13thAmendment.
Althoughallthreemethodsprovidethecorrectfinalanswertothequery,theresponseprovidedby
R3 ismorefavorable. The0-ShotCoT’sresponsecontainsahallucinationaboutthepublicationdate
ofthe“LittleWomen”book. Inthe2-ShotCoT’sresponse,theexactdatesonwhichthebookwas
publishedandthetimeLouisaMayAlcottlivedarenotmentioned,thereforethefinalresponseisnot
verifiable. However,R3 groundstherequiredfactsontheKGandcorrectlyidentifiesandmentions
thedatesrequiredforfindingtheanswerwhichalsoallowsforverificationofthefinalanswer.
6626

ClaimVerification: Long-Tail
Query: MelahatParsisverylikelytobefamiliarwithDonerkebab.
0-ShotCoT:MelahatParsislikelyfamiliarwithDonerkebab,asitisapopularTurkishdishand
MelahatParsisaTurkishchefknownforherexpertiseinTurkishcuisine. Finalanswer: Yes.
2-ShotCoT:AsMelahatParsisacommonTurkishname,andDönerkebabisapopularTurkish
dish,it’slikelythatMelahatParsisfamiliarwithDönerkebab. FinalAnswer: Yes.
R3: ThegeneralrulestatesthatMelahatPars,beingaTurkishsingerandhavinglivedinTurkey,is
likelytobefamiliarwithDonerkebab,whichisapartofTurkishcuisine. Fact“(MelahatPars,is,
Turkishsinger)”tellsusthatMelahatParsisaTurkishsingerandFact“(MelahatPars,countryof
citizenship,Turkey)”tellsusthatsheisacitizenofTurkey. Fact“(donerkebab,cuisine,Turkish
cuisine)” confirms that Doner kebab is indeed a part of Turkish cuisine. Therefore, based on the
generalruleandthefacts,itisverylikelythatMelahatParsisfamiliarwithDonerkebab. Therefore,
theansweris: Yes,MelahatParsisverylikelytobefamiliarwithDonerkebab.
The0-ShotCoTresponsecontainsafactualhallucinationaboutMelahatPars’occupation,although
thefinalansweriscorrect. The2-ShotCoTresponseisbasedonthejudgmentaboutMelahatPars’
name,thereforereflectingthefactthattheLLMisunfamiliarwiththisentity. Byidentifyingand
utilizingtherelevantKGfacts,R3 isabletoprovideacorrectandgroundedresponsetothequery.
Query: SomepeoplestudybooksaboutXuanxue.
0-ShotCoT:1. WhatisXuanxue? 2. Whoare"somepeople"? 3. Whydo"somepeople"study
booksaboutXuanxue? Finalanswer: Yes.
2-ShotCoT:Xuanxue,alsoknownas"Neo-Daoism",isaphilosophicalmovementinancientChina.
It is still studied and researched by scholars and enthusiasts. Therefore, it is accurate to say that
somepeoplestudybooksaboutXuanxue. Finalanswer: Yes.
R3: ThegeneralrulestatesthatsomepeoplestudybooksaboutXuanxuebecauseitisaphilosophical
movement in post-classical Chinese history that combines Daoist and Confucian beliefs. Facts
“(Xuanxue,is,post-classicalChinesephilosophybringingtogetherDaoistandConfucianbeliefs)”,
“(Xuanxue, instanceof, philosophical movement)”, “(Xuanxue, has part(s), Xuanxue in Wei and
Jindynasties)”,and“(Xuanxue,inception,0300)”provideinformationaboutXuanxuebeingapost-
classicalChinesephilosophythatcombinesDaoistandConfucianbeliefs. Basedonthisinformation,
itisreasonabletoassumethattherearebooksaboutXuanxueavailableforstudy. Therefore,the
answeris: Yes,somepeoplestudybooksaboutXuanxue.
Theanswerprovidedby0-ShotCoTlacksaspacificandcorrectreasoningprocedure,althoughthe
finalansweriscorrect. Theanswersprovidedbyboth2-ShotCoTandR3 arecorrectandbasedon
correctfactsandreasoningprocesses.
6627

Query: OnecanseetheAlaviyanDomeandtheDomeofSoltaniyehatthesametime. (No)
0-ShotCoT:TheAlaviyanDomeislocatedinShiraz,Iran,whiletheDomeofSoltaniyehissituated
in Soltaniyeh, Zanjan, Iran, and they are approximately 500 kilometers apart. Considering the
distanceandthecurvatureoftheEarth,itisnotpossibletoseebothdomesatthesametimewiththe
nakedeye.
2-ShotCoT:TheAlaviyanDomeandtheDomeofSoltaniyeharelocatedindifferentcitiesinIran,
andarequitefarapartfromeachother. Itisnotpossibletoseebothdomesatthesametimedueto
thedistancebetweenthem. FinalAnswer: No.
R3: ThesentenceclaimsthatonecanseetheAlaviyanDomeandtheDomeofSoltaniyehatthe
sametime. Accordingtothegeneralrule,theAlaviyanDomeandtheDomeofSoltaniyehmustbe
locatedinthesameplacetobeseenatthesametime. Fact“(AlaviyanDome,location,Hamadan)”
tellsusthattheAlaviyanDomeislocatedinHamadan,Iran. Fact“(DomeofSoltaniyeh,location,
Soltaniyeh)”tellsusthattheDomeofSoltaniyehisalsolocatedinSoltaniyeh,Iran. SinceHamadan
andSoltaniyeharedifferentlocations,itisnotpossibletoseetheAlaviyanDomeandtheDomeof
Soltaniyehatthesametime. Therefore,theansweris: No,onecannotseetheAlaviyanDomeand
theDomeofSoltaniyehatthesametimebecausetheyarelocatedindifferentplaces.
Thethefinalanswerprovidedby0-ShotCoTiscorrect,itcontainshallucinationaboutthelocation
oftheAlaviyanDome. Although2-ShotCoTcorrectlymentionsthatthetwodomesarelocatedin
differentcities,itdoesnotrefertotheirparticularlocations. However,R3’sresponseisgroundedon
theKGfactsaboutthespecificcitiesthatthedomesarelocatedinandthesurfacedcommonsense
axiom,thereforebeingmorespecificandeasilyverifiable.
Query: MinaAhadiislikelytocelebrateLent. (No)
0-ShotCoT:LentisaChristianobservance,andMinaAhadiisknownforherworkasanactivistin
theareasofsecularismandhumanrights,particularlyfocusingontheplightofatheistsandapostates
inIslamiccountries. Givenheradvocacywork,itisunlikelythatshecelebratesLent. FinalAnswer:
No.
2-Shot CoT: Mina Ahadi is a human rights activist known for her advocacy for secularism and
againstreligiousauthoritarianism. Givenherpublicstance,itisunlikelythatshewouldcelebrate
Lent,whichisaChristianreligiousobservance. Finalanswer: No.
R3: ThegeneralrulestatesthatMinaAhadi,beinganatheist,isunlikelytocelebrateLent. Fact
“(MinaAhadi,religionorworldview,atheism)”confirmsthatMinaAhadiidentifiesasanatheist.
Lent is a Christian observance and is typically celebrated by Christians. Since Mina Ahadi is an
atheist and does not follow any religious worldview, it is unlikely that she would celebrate Lent.
Therefore,theansweris: No,MinaAhadiisunlikelytocelebrateLent.
Allthreemethodsprovidecorrectanswerstothisclaim.
6628

Query: ÁrpádKlatsmányiwaslikelytobeawareofthesecondlawofthermodynamics. (Yes)
0-Shot CoT: Árpád Klatsmányi was a Hungarian linguist and writer, not a physicist or scholar
in the field of thermodynamics. Without any evidence that he had a background in the study of
thermodynamics,itisunlikelythathewasawareofthesecondlawofthermodynamics. Finalanswer:
No.
2-Shot CoT: Árpád Klatsmányi lived in the 19th and 20th centuries, and the second law of ther-
modynamicswaswellestablishedbythattime. Itislikelythathe,asaphysicist,wouldhavebeen
awareofthisscientificprinciple. Therefore,ÁrpádKlatsmányiwaslikelytobeawareofthesecond
lawofthermodynamics. FinalAnswer: Yes.
R3: ThegeneralrulestatesthatÁrpádKlatsmányimusthavespecificknowledgeoreducationinthe
fieldofthermodynamicstobelikelytobeawareofthesecondlawofthermodynamics. Fact“(Árpád
Klatsmányi, occupation, mechanical engineer)” tells us that Árpád Klatsmányi is a mechanical
engineer, and Fact “(Árpád Klatsmányi, educated at, Budapest University of Technology and
Economics;endtime,1947)”tellsusthathewaseducatedatBudapestUniversityofTechnologyand
Economics. Althoughwedon’thaveexplicitinformationabouthisknowledgeinthermodynamics,it
isplausibletoassumethatasamechanicalengineer,hewouldhavebeenexposedtotheprinciples
of thermodynamics during his education. Additionally, the second law of thermodynamics is
a fundamental concept in thermodynamics, and it is likely that someone with a background in
mechanicalengineeringwouldbeawareofit. Therefore,theansweris: Yes,ÁrpádKlatsmányiis
likelytobeawareofthesecondlawofthermodynamics.
The 0-ShotCoT’s responseis incorrect andcontains hallucinationabout ÁrpádKlatsmányi’soc-
cupation. Althoughthe2-ShotCoTproviesacorrectresponse,itcontainshallucinationaboutthe
timeÁrpádKlatsmányilivedin. R3 providesthecorrectresponsebyutilizingtheKGfactsabout
ÁrpádKlatsmányi’soccupationandeducationaswellasthesurfacedcommonsenseaxiomabouthis
familiaritywiththesecondlawofthermodynamics.
Query: MaríaSubíesForcada’shomecountrywasamongthealliedpowers. (No)
0-ShotCoT:First,let’sdetermineMaríaSubíesForcada’shomecountry. MaríaSubíesForcadawas
aSpanishpolitician. DuringWorldWarII,Spainwasofficiallyneutralanddidnotformallyjoin
eithertheAxisorAlliedpowers. Therefore,MaríaSubíesForcada’shomecountrywasnotamong
theAlliedpowers. FinalAnswer: No.
2-ShotCoT:MaríaSubíesForcadawasfromSpain,whichwasamemberoftheAxispowersduring
WorldWarII,anddidnotjointheAlliedpowersuntilafterthewar. Finalanswer: No.
R3: Generalrule“MaríaSubíesForcada’shomecountrymustbeamongtheAlliedPowersduring
WorldWarIItofulfilltheclaim.”tellsusthatMaríaSubíesForcada’shomecountrymustbeamong
theAlliedPowersduringWorldWarII.Fact“(MaríaSubíesForcada,countryofcitizenship,Spain)”
tellsusthatMaríaSubíesForcada’scountryofcitizenshipisSpain. However,thefactsdonotprovide
explicitinformationaboutSpain’sinvolvementinWorldWarII.Wecanmakeplausibleassumptions
basedongeneralknowledge. SpainwasnotamongtheAlliedPowersduringWorldWarII,butit
wasaneutralcountry. Therefore,theansweris: No,MaríaSubíesForcada’shomecountrywasnot
amongtheAlliedPowersduringWorldWarII.
6629

The0-ShotCoTresponsecontainsahallucinationaboutMaríaSubíesForcada’soccupation. The
2-ShotCoTresponsecontainsahallucinationaboutSpain’sinvolvementintheaxispowersduring
WorldWarII.However,R3’sresponsedoesnotcontainanyhallucinationsandgroundstheinforma-
tionaboutMaríaSubíesForcada’snationalityontheKG.Furthermore,itdoesnothallucinateabout
thesideofSpainduringWorldWarII.
Query: NoeliaVargasmustsleeptosurvive. (Yes)
0-ShotCoT:No,NoeliaVargasdoesnotneedtosleeptosurvive.
2-ShotCoT:NoeliaVargas,likeallhumans,requiressleepforsurvival. FinalAnswer: Yes.
R3: Thegeneralrulestatesthatallhumans,includingNoeliaVargas,mustsleeptosurvive. Fact
“(NoeliaVargas,instanceof,human)”tellsusthatNoeliaVargasisahuman. Therefore,basedonthe
generalrule,wecanconcludethatNoeliaVargasmustsleeptosurvive. Therefore,theansweris:
Yes,NoeliaVargasmustsleeptosurvive.
The0-ShotCoTresponseisincorrectandincludesahallucinationaboutNoeliaVargas. The2-Shot
CoTandR3 arebothabletogivethecorrectanswer.
Query: WhenpeoplewantedtoaddressUlrikAntonMotzfeldtinacourt,theysaid,YourHonor.
(Yes)
0-ShotCoT:First,it’simportanttoestablishwhoUlrikAntonMotzfeldtis. UlrikAntonMotzfeldt
wasaNorwegianpoliticianandjudgewholivedinthe19thcentury. Duringhistime,theterm“Your
Honor”wascommonlyusedtoaddressjudgesincourtasasignofrespect. Therefore,itislikely
thatwhenpeoplewantedtoaddressUlrikAntonMotzfeldtinacourt,theysaid"YourHonor."Final
Answer: Yes.
2-Shot CoT: Ulrik Anton Motzfeldt was a Norwegian theologian and politician, and the phrase
“YourHonor”istypicallyusedinreferencetojudges,nottheologiansorpoliticians. Therefore,itis
unlikelythatpeoplewouldaddressUlrikAntonMotzfeldtas“YourHonor”incourt. Finalanswer:
No.
R3: Thegeneralrule“WhenaddressingUlrikAntonMotzfeldtinacourt,peoplesay“YourHonor”
because he is a judge.” states that when addressing Ulrik Anton Motzfeldt in a court, people say
“Your Honor” because he is a judge. Fact “(Ulrik Anton Motzfeldt, position held, Justice in the
SupremeCourtofNorway)”confirmsthatUlrikAntonMotzfeldtheldthepositionofJusticeinthe
SupremeCourtofNorway,whichindicatesthatheisindeedajudge. Therefore,theansweris: Yes,
whenpeoplewantedtoaddressUlrikAntonMotzfeldtinacourt,theysaid"YourHonor".
Inthe2-ShotCoTresponse,theLLMhasneglectedthefactthatUlrikAntonMotzfeldtwasajudge,
butinboth0-ShotCoTandR3 responses,thisfactisconsideredwhichresultsinthecorrectanswer.
6630

Query: JamshidAmouzegar’slifebeganinthethirddecadeofthe20thcentury. (Yes)
0-ShotCoT:Toanswerthequestion,weneedtofindoutwhenthethirddecadeofthe20thcentury
was. Thethirddecadeofacenturyreferstothe1920s. Therefore,ifJamshidAmouzegar’slifebegan
inthethirddecadeofthe20thcentury,itmeanshewasborninthe1920s.
2-ShotCoT:TodeterminewhenJamshidAmouzegar’slifebegan,let’sconsiderthethirddecadeof
the20thcentury. Thethirddecadespansfrom1920to1929. IfJamshidAmouzegar’slifebeganin
thistimeframe,thenthestatementistrue. Finalanswer: Idon’tknow.
R3: Accordingtothegeneralrule,ifaperson’sbirthyearfallswithinthespecifieddecade,then
their life began in that decade. Fact “(Jamshid Amouzegar, date of birth, 1923/06/25)” tells us
that Jamshid Amouzegar was born in 1923, which is within the third decade of the 20th century
(1921-1930). Therefore,wecanconcludethatJamshidAmouzegar’slifebeganinthethirddecadeof
the20thcentury. Therefore,theansweris: Yes,JamshidAmouzegar’slifebeganinthethirddecade
ofthe20thcentury.
SincetheLLMisunfamiliarwithJamshidAmouzegar,itcannotprovideacertainanswerin0-Shot
and 2-Shot settings, but since R3 responds based on grounded KG facts, it correctly answers the
query.
Query: ChiaraGuerraearnsalivingbyportrayingdifferentcharactersinfrontofacamera. (Yes)
0-ShotCoT:First,let’sidentifythekeyelementsofthequestion: -ChiaraGuerra
-Earnsaliving
-Portrayingdifferentcharacters
-Infrontofacamera
Basedontheinformationprovided,itsuggeststhatChiaraGuerra’sprofessioninvolvesportraying
differentcharactersinfrontofacameratoearnaliving. Finalanswer: Yes.
2-ShotCoT:Idon’thavespecificinformationaboutChiaraGuerraandheroccupation. Therefore,I
don’tknow.
R3: The general rule states that Chiara Guerra must be an actor to earn a living by portraying
differentcharactersinfrontofacamera. Fact“(ChiaraGuerra,occupation,actor)”,“(ChiaraGuerra,
is, Italian actress)”, “(Chiara Guerra, instance of, human)”, and “(Chiara Guerra, place of birth,
Camposampiero)”allindicatethatChiaraGuerraisanItalianactress. Therefore,basedonthefacts
and the general rule, we can conclude that Chiara Guerra earns a living by portraying different
characters in front of a camera. Therefore, the answer is: Yes, Chiara Guerra earns a living by
portrayingdifferentcharactersinfrontofacamera.
Theresponseproividedby0-ShotCoTiscompletelyincorrectasitconsiderspiecesoftheclaimas
reliableinformation. SincetheLLMisunfamiliarwithChiaraGuerra,itdoesnotprovideadecisive
answerinthe2-ShotCoTresponse. However,theanswerprovidedbyR3 iscorrectandgrounded
ontheKGfacts.
6631

D LLMUsageinR3 designedtoexplicitlymentiontherequireddesider-
ataofausefulcommonsenseaxiom. Theprompt
Several components of the R3 framework make
usedforthismoduleis:
useofanLLM.Inthissection,weprovideexpla-
Task: You are a helpful assistant trying
nations about the way that LLM is used in each
to give us some guidance about
moduleandprovidethepromptsthatweusedfor
answering a question. A set of
each LLM-based module. Since prompts for the knowledge graph triples called "facts"
are given that may provide some
claimverificationandquestionansweringtasksare
contextual information about the
similar, we provide question answering prompts question. However, if you don't find
here,andalsoreleaseallpromptsfortheclaimver- them useful, just ignore them and
don't say anything about them. We may
ificationaswellaspreferencereasoningwithour
later look for additional facts to
codeanddata. answer the question. Your mission is
to think about how the question could
ObtainingRelevantSub-graph Akeymotiva- be answered using general knowledge
tionoftheKGQAmethodologiessuchasR3 isbe- that people have plus facts like the
ones provided, and then concisely
ingabletoanswerqueriesaboutrecentandobscure
state the most important general rule
entities. However, existing pre-trained entity ex- that would help someone to find the
answer. But, you must not directly
tractorsarelimitedtothemorefamousentitiesthat
answer the question and you must not
theywereexposedtoduringtheirtraining. There- judge whether the question is
fore, they may fail to extract recent entities that answerable or not. Focus on what
general information can help in giving
were not included in the KG at the time of their
a yes/no answer to the question.
trainingorobscureandlong-tailentities. Toover- Your response must follow the following
come this challenge, as explained in Section 3.2, format: "<an explanation> Therefore, a
helpful rule is:\n Rule: <An entity or
R3 usesbothanoff-the-shelfentityextractorand
Something relevant to it> must <have
anLLM-basedentityextractorandunitesthesets some property> to <property identified
of entities both methods return and uses the re- in question>." Try your best to use
your general knowledge. Be smart.
sulting set to extract their relevant subgraphs. In
Don't ask or state conditions on
theablationstudysection,weprovideananalysis obvious information that most average
humans would know. You are in charge
on the roleof each entity extractor and provide a
of helping with such knowledge so try
discussionontheirnecessityinR3’sproperperfor-
to provide it in your rules rather
mance. than asking for it. If you can't
produce a helpful rule or you think
The prompt used in the LLM-based entity ex-
the question is not answerable, just
tractorisasfollows: try to make understanding the question
easier by giving a hint or defining
You are a helpful assistant helping in
terms in the question and don't say
finding the answer to a question. The
anything else.
found answer has to be based on
[Few-shot Examples]
Wikidata Knowledge Graph triples
obtained about entities. Given a
question and a helpful fact, identify
Sub-graph Pruning After surfacing the com-
the least number of entities for which
we need to obtain information to be monsenseaxiom,relevantcandidatefactsfromthe
able to solve the question. sub-graph that can be used to ground the answer
You must only mention the entities and
onthemareobtainedbyusingbothanLLM-based
nothing else.
Write the entities in the following module andalso semanticsimilarity between the
format:
embedding vectors. Prompts used for the LLM-
Selected entity/entities:
entity1 basedsub-graphpruningmoduleisasfollows:
entity2...
Task: You are a helpful assistant that is
[Few-shot Examples]
trying to help us answer a question.
Given the question, a general rule
SurfacingtheCommonsenseAxiom Thecom- that will help us answer the question,
and a list of knowledge graph triples
monsense axioms that guide each branch of the
which we call them facts. Consider the
tree-structuredsearchintheR3frameworkarealso
facts and think about their relation
surfacedfromtheLLM.Theseaxiomsarecritically to the question and general rule and
try to extract the facts that may help
important in successfully answering the queries.
answering the question. The facts may
Thepromptusedforthistaskisthereforecarefully be insufficient to answer the
6632

question, but try your best to extract Task: You are a helpful assistant trying
|     | the | relevant | facts. |     |     |     |     | to help | in finding | the | required |     |
| --- | --- | -------- | ------ | --- | --- | --- | --- | ------- | ---------- | --- | -------- | --- |
Your response must follow this format: information to answer a given
<an explanation> Therefore, the relevant question. A the set of general rules
facts are: <list of relevant facts> and a list of knowledge graph triples,
Just copy the selected facts and don't which we name facts, are already
generate facts on your own or adjust provided. Based on these, an answer
the facts in any way. Try your best to was propsed, but it was not identified
select the relevant facts. If there as being correct and certain. You are
are no relevant facts, just output asked to identify what other facts are
|                              | "None".   |           |     |     |     |              |     | required      | to give     | a certain  | answer      | to      |
| ---------------------------- | --------- | --------- | --- | --- | --- | ------------ | --- | ------------- | ----------- | ---------- | ----------- | ------- |
|                              | [Few-shot | Examples] |     |     |     |              |     | the question. |             | The facts  | you         | ask for |
|                              |           |           |     |     |     |              |     | will be       | obtained    | from       | a knowledge |         |
|                              |           |           |     |     |     |              |     | graph.        | So, try     | to extract | the         | name of |
| Fact-GroundedAnswerSelection |           |           |     |     |     | Inthelightof |     |               |             |            |             |         |
|                              |           |           |     |     |     |              |     | entity        | or entities | about      | which       | we      |
theretrievedrelevantfacts,theLLMtriestoselect should obtain facts and mention it in
|     |         |            |            |      |     |        |         | your answer. | For           | example,   | if        | knowing |
| --- | ------- | ---------- | ---------- | ---- | --- | ------ | ------- | ------------ | ------------- | ---------- | --------- | ------- |
| the | answer. | In         | the prompt | used | for | this   | module, |              |               |            |           |         |
|     |         |            |            |      |     |        |         | about Bill   | Clinton's     | daughter's |           |         |
| we  | aim     | to clarify | for the    | LLM  | to  | try to | answer  |              |               |            |           |         |
|     |         |            |            |      |     |        |         | religion     | is necessary, |            | and among | the     |
the question if the provided facts are sufficient, already provided facts you see ('Bill
|     |           |         |     |         |       |        |     | Clinton',  | 'child', | 'Chelsea |      | Clinton'), |
| --- | --------- | ------- | --- | ------- | ----- | ------ | --- | ---------- | -------- | -------- | ---- | ---------- |
| and | otherwise | respond |     | with “I | don’t | know”. | The |            |          |          |      |            |
|     |           |         |     |         |       |        |     | you should | respond  | "we      | need | to know    |
promptusedforthismoduleisasfollows:
|     |           |           |           |           |             |          |     | Chelsea             | Clinton's    | religion". |            |           |
| --- | --------- | --------- | --------- | --------- | ----------- | -------- | --- | ------------------- | ------------ | ---------- | ---------- | --------- |
|     |           |           |           |           |             |          |     | Finally If          | the provided | facts      | and        | general   |
|     | Task:     | You are   | a helpful | assistant |             | that     | is  |                     |              |            |            |           |
|     |           |           |           |           |             |          |     | rules are           | already      | sufficient |            | to give a |
|     | trying    | to        | help us   | answer    | a question. |          |     |                     |              |            |            |           |
|     |           |           |           |           |             |          |     | certain             | answer       | to the     | question,  | your      |
|     | You       | are given | the       | question, |             | a number |     |                     |              |            |            |           |
|     |           |           |           |           |             |          |     | response            | should       | only be:   | "nothing". |           |
|     | of        | general   | rules,    | and       | a list      | of       |     |                     |              |            |            |           |
|     | knowledge |           | graph     | triples   | which       | we call  |     |                     |              |            |            |           |
|     |           |           |           |           |             |          |     | [Few-shot Examples] |              |            |            |           |
|     | them      | facts     | that      | may be    | helpful     | in       |     |                     |              |            |            |           |
finding the answer. First, go over the Next, we ask the LLM to identify the next entity
|     | facts | and | general | rules | one | by one. |     |     |     |     |     |     |
| --- | ----- | --- | ------- | ----- | --- | ------- | --- | --- | --- | --- | --- | --- |
forwhichweneedtoobtaintherelevantsub-graph
|     | Try | to think | of  | how each | fact | may | help |     |     |     |     |     |
| --- | --- | -------- | --- | -------- | ---- | --- | ---- | --- | --- | --- | --- | --- |
you answer the question. Then, if you to continue the search branch. For this step, the
|     | don't | have | explicit | information |     | about |     |     |     |     |     |     |
| --- | ----- | ---- | -------- | ----------- | --- | ----- | --- | --- | --- | --- | --- | --- |
followingpromptisused:
|     | something |     | or the | general | rule | isn't |     |     |     |     |     |     |
| --- | --------- | --- | ------ | ------- | ---- | ----- | --- | --- | --- | --- | --- | --- |
helpful, try to use your general Task: Considering the provided information
knowledge of the world and make need that is needed to answer the
plausible assumptions to find the question and a set of relevant facts,
answer. Be smart. Don't ask for identify the name of the Wikidata
obvious information that most average entity that facts about it will be
|     | humans | would | know. |     |     |     |     | helpful | in fulfilling |     | the information |     |
| --- | ------ | ----- | ----- | --- | --- | --- | --- | ------- | ------------- | --- | --------------- | --- |
Your response must follow the following need. Try to extract the entity name
|     | format: |     |     |     |     |     |     | from the | relevant | facts. | For | example, |
| --- | ------- | --- | --- | --- | --- | --- | --- | -------- | -------- | ------ | --- | -------- |
Answer: <your reason> Therefore, the if the information need states that we
|     | answer | is: | <your | final |     |     |     | need to | know about | Bill | Clinton's |     |
| --- | ------ | --- | ----- | ----- | --- | --- | --- | ------- | ---------- | ---- | --------- | --- |
answer(beginning with "Yes", "No", or daughter, use the fact ('Bill
|     | "I  | don't | know")> |     |     |     |     | Clinton', | 'child', | 'Chelsea |     | Clinton') |
| --- | --- | ----- | ------- | --- | --- | --- | --- | --------- | -------- | -------- | --- | --------- |
You must only begin your response with and select the entity name Chelsea
|         | "Yes"      | or         | "No" if        | you want    | to      | give      | the      |                     |          |              |            |      |
| ------- | ---------- | ---------- | -------------- | ----------- | ------- | --------- | -------- | ------------------- | -------- | ------------ | ---------- | ---- |
|         |            |            |                |             |         |           |          | Clinton.            | Remember | that         | the entity | name |
|         | answer     | to         | the question.  |             | Try     | your best |          |                     |          |              |            |      |
|         |            |            |                |             |         |           |          | you pick            | must     | be different | from       | all  |
|         | to         | use facts, | general        |             | rules,  | and       |          |                     |          |              |            |      |
|         |            |            |                |             |         |           |          | Previously          | chosen   | entities.    |            |      |
|         | plausible  |            | assumptions    |             | to give | the       |          |                     |          |              |            |      |
|         |            |            |                |             |         |           |          | [Few-shot Examples] |          |              |            |      |
|         | answer.    | If         | using          | the current |         | set of    |          |                     |          |              |            |      |
|         | general    | rules      | and            | facts       | is not  | enough    |          |                     |          |              |            |      |
|         | to         | answer     | the question   |             | even    | with      |          |                     |          |              |            |      |
|         | plausible  |            | assumptions,   |             | in the  |           |          |                     |          |              |            |      |
|         | beginning  |            | of your        | answer,     | you     | must      |          |                     |          |              |            |      |
|         | only       | say        | "I don't       | know".      |         |           |          |                     |          |              |            |      |
|         | [Few-shot  | Examples]  |                |             |         |           |          |                     |          |              |            |      |
| Missing |            | Evidence   | Identification |             |         | In case   | the      |                     |          |              |            |      |
| LLM     | determines |            | the existing   |             | facts   | to be     | insuffi- |                     |          |              |            |      |
cient,weneedtoidentifywhatmissingevidenceis
| required.   |     | Thisperformanceisobtainedintwosteps. |          |             |     |               |         |     |     |     |     |     |
| ----------- | --- | ------------------------------------ | -------- | ----------- | --- | ------------- | ------- | --- | --- | --- | --- | --- |
| First,      | the | LLM                                  | is asked | to identify |     | what          | missing |     |     |     |     |     |
| information |     | is required,                         |          | for which   |     | the following |         |     |     |     |     |     |
promptisused:
6633