|     | HalluMeasure: |     | Fine-grained     |     | Hallucination |     |           | Measurement |     |     | Using |     |
| --- | ------------- | --- | ---------------- | --- | ------------- | --- | --------- | ----------- | --- | --- | ----- | --- |
|     |               |     | Chain-of-Thought |     |               |     | Reasoning |             |     |     |       |     |
ShayanA.Akbar*,MdMosharafHossain ,TessWood ,Si-ChiChin,EricaSalinas,
|     |     |     |     |     |     | ∗   |     | ∗   |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
VictorAlvarez,ErwinCornejo
CustomerExperienceandBusinessTrends,Amazon.com
|     |     | {shayaakb, |     | hosmdmos, |                      | tesswoo,                                    | sichi, |     | erislin, |     |     |           |
| --- | --- | ---------- | --- | --------- | -------------------- | ------------------------------------------- | ------ | --- | -------- | --- | --- | --------- |
|     |     |            |     | miranvi,  | eccornej}@amazon.com |                                             |        |     |          |     |     |           |
|     |     | Abstract   |     |           |                      | inacompany’sstockvalue,wipingout$100billion |        |     |          |     |     |           |
|     |     |            |     |           |                      | inmarketcapitalization(Reuters,2023).       |        |     |          |     |     | Moreover, |
Automatingthemeasurementofhallucinations
misleadinginformationaboutbereavementtravel
inLLM-generatedresponsesisachallenging
taskasitrequirescarefulinvestigationofeach policygeneratedbyanairlinechatbotledtoacourt
|     |                          |     |                   |     |     | order | for partial |     | refund | to a passenger |     | (Technica, |
| --- | ------------------------ | --- | ----------------- | --- | --- | ----- | ----------- | --- | ------ | -------------- | --- | ---------- |
|     | factualclaiminaresponse. |     | Inthispaper,wein- |     |     |       |             |     |        |                |     |            |
troduceHalluMeasure,anewLLM-basedhallu- 2024). Consequently,detectingandmeasuringhal-
cinationdetectionmechanismthatdecomposes lucinationsinLLMshasbecomeacrucialresearch
anLLMresponseintoatomicclaims,andevalu-
areainrecentyearstopreventtheirpotentialharm-
ateseachatomicclaimagainsttheprovidedref-
fuleffects.
|     | erencecontext. | Themodelusesastep-by-step |     |     |     |     |     |     |     |     |     |     |
| --- | -------------- | ------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
WemeasurehallucinationsinLLMresponsesby
Chain-of-Thoughtreasoningprocessandcan
comparingtheclaimsmadeinaresponseagainsta
|     | identify 3 | major categories | of  | hallucinations |     |                           |     |     |     |                    |     |     |
| --- | ---------- | ---------------- | --- | -------------- | --- | ------------------------- | --- | --- | --- | ------------------ | --- | --- |
|     |            |                  |     |                |     | referencecontextdocument. |     |     |     | Sincemanuallyanno- |     |     |
(e.g.,contradiction)aswellas10morespecific
subtypes(e.g.,overgeneralization)whichhelp tating LLM responses against such context docu-
toidentifyreasonsbehindthehallucinationer- mentsistime-consumingandexpensive,thereisa
rors.Specifically,weexplorefourdifferentcon-
needtodevelopautomaticapproachestomeasure
figurationsforHalluMeasure’sclassifier: with hallucinationatscale. Inrecentyears,severalstud-
andwithoutCoTprompting,andusingasingle
ies(Zhaetal.,2023;Huetal.,2023;Vectara,2023;
classifiercalltoclassifyallclaimsversussepa-
Minetal.,2023;Huangetal.,2023)haveproposed
|     | ratecallsforeachclaim. |     | Thebest-performing |     |     |           |     |             |             |     |     |            |
| --- | ---------------------- | --- | ------------------ | --- | --- | --------- | --- | ----------- | ----------- | --- | --- | ---------- |
|     |                        |     |                    |     |     | solutions |     | to automate | measurement |     | of  | hallucina- |
configuration(withCoTandseparatecallsfor
|     |     |     |     |     |     | tionsinLLMresponses. |     |     |     | Thesesolutionsinvolve |     |     |
| --- | --- | --- | --- | --- | --- | -------------------- | --- | --- | --- | --------------------- | --- | --- |
eachclaim)demonstratessignificantimprove-
ments in detecting hallucinations, achieving classifyingpairsofcontextandLLMresponsetexts
|     | a 10-point | increase in | F1 score | on our | Tech- |                      |     |     |                             |     |     |     |
| --- | ---------- | ----------- | -------- | ------ | ----- | -------------------- | --- | --- | --------------------------- | --- | --- | --- |
|     |            |             |          |        |       | intohallucinationvs. |     |     | non-hallucinationclassesus- |     |     |     |
NewsSummdataset,anda3-pointincreasein ingmachinelearningmodels.
AUCROContheSummEvaldataset,compared
Wehighlightkeydifferencesbetweenpriorsolu-
tothreebaselinemodels(RefChecker,Align-
tionsandourHalluMeasuremethodbelow:
Score,andVectaraHHEM).Wefurthershow
reasonableaccuracyondetecting10novelerror
|     |     |     |     |     |     | •   | LLM-based |     | classification |     | approach: | Un- |
| --- | --- | --- | --- | --- | --- | --- | --------- | --- | -------------- | --- | --------- | --- |
subtypesofhallucinations(whereevenhumans like some of the prior works that use tradi-
struggleinclassification)derivedfromlinguis-
|     |     |     |     |     |     |     | tional | machine | learning | models | and | BERT- |
| --- | --- | --- | --- | --- | --- | --- | ------ | ------- | -------- | ------ | --- | ----- |
ticanalysisoftheerrorsmadebytheLLMs.
|     |     |     |     |     |     |     | based | classifiers | (Zha | et  | al., 2023; | Vectara, |
| --- | --- | --- | --- | --- | --- | --- | ----- | ----------- | ---- | --- | ---------- | -------- |
2023),weuseLLMswithpromptengineering
1 Introduction
forhallucinationdetectionandmeasurement,
achievingbetterperformance.
HallucinationsinLargeLanguageModels(LLMs)
areinevitable(Xuetal.,2024)andcancausesignif-
|            |                                    |     |     |     |     | •   | Claim-level |     | classification: |     | Many | studies |
| ---------- | ---------------------------------- | --- | --- | --- | --- | --- | ----------- | --- | --------------- | --- | ---- | ------- |
| icantharm. | Forinstance,non-existentlegalcases |     |     |     |     |     |             |     |                 |     |      |         |
(Zhaetal.,2023;Vectara,2023)proposesolu-
generatedbyanLLMincourtpaperssubmittedby tionsmeasuringhallucinationsattheresponse
alawfirmresultedinsanctionsbyajudge(CNBC,
|        |         |          |          |       |       |     | level, | some | (Kryscinski | et  | al., 2020; | Laban |
| ------ | ------- | -------- | -------- | ----- | ----- | --- | ------ | ---- | ----------- | --- | ---------- | ----- |
| 2023). | Wrongly | claiming | the Webb | Space | Tele- |     |        |      |             |     |            |       |
etal.,2021)segmentresponsesintosentences,
scopewasthefirsttophotographanexoplanetdur-
andafew(Minetal.,2023;Chernetal.,2023)
inganLLM-basedproductdemoledtoa7.7%drop operateattheclaimlevel. Weemployclaim-
*Theseauthorscontributedequallytothiswork. levelclassification,enablingfine-grainedmea-
15020
Proceedingsofthe2024ConferenceonEmpiricalMethodsinNaturalLanguageProcessing,pages15020–15037
November12-16,2024©2024AssociationforComputationalLinguistics

Figure1: HalluMeasureOverview. TheLLMresponsegoesthroughclaimextractionmodeltoproducealistof
claimswhichareclassifiedusingaclaimclassificationmodel. Finallyscoresareaggregatedandreturnedtotheuser.
Figure2:HalluMeasureassignseachclaimathoughtforhallucinationlabeling,thenalabelfrom5labels(supported,
partiallysupported,absent,contradicted,unsupported,unevaluatable). Eachclaimalsogetsathoughtforerrortype
classification,thenanerrortypelabelfrom10labels(seeTable2).
surement. Whenhallucinatedinformationex- agebatchprompting(Chengetal.,2023)and
istswithinlengthyLLMresponses,evaluating demonstrateanLLM-basedclassifierthatclas-
individualextractedclaimsimproveshalluci- sifiesmultipleclaimsextractedfromthesame
nationdetectionaccuracy. responsesimultaneouslywithreasonableac-
|     |     |     |     | curacy. This | approach reduces | LLM calls, |
| --- | --- | --- | --- | ------------ | ---------------- | ---------- |
• Chain-of-ThoughtPrompting: Weleverage associatedlatency,andcosts,enablingmore
few-shotChain-of-Thought(CoT)prompting
|     |     |     |     | scalable hallucination | detection | while main- |
| --- | --- | --- | --- | ---------------------- | --------- | ----------- |
(Weietal.,2022)toteachreasoningabilities
tainingreasonableperformance.
| to our claim | classifier model, | enabling         | it to |                           |                  |     |
| ------------ | ----------------- | ---------------- | ----- | ------------------------- | ---------------- | --- |
|              |                   |                  |       | • Fine-grainederrortypes: | Previousworksof- |     |
| accurately   | classify claims   | through exemplar |       |                           |                  |     |
demonstrations. This enhances claim classi- tenclassifyresultsintobinaryorNLI(ternary)
|                   |            |            |     | classes. Our | study demonstrates | the value |
| ----------------- | ---------- | ---------- | --- | ------------ | ------------------ | --------- |
| fication accuracy | over prior | works that | use |              |                    |           |
ofgranularhallucinationerrortypes(Section
simplefew-shotprompting(Huetal.,2023).
|     |     |     |     | 3.2). By | providing deeper insights | into the |
| --- | --- | --- | --- | -------- | ------------------------- | -------- |
• Single classification call for list of claims: type of hallucinations produced, HalluMea-
Previous studies processed claims individu- sure enables more targeted solutions to en-
ally (Hu et al., 2023). However, we lever- hanceLLMreliability.
15021

| LLM-in-testresponse |     |     |     | Atomicclaims |     |     |     |     |     |     |
| ------------------- | --- | --- | --- | ------------ | --- | --- | --- | --- | --- | --- |
1.SamsunghasaproductcalledGearBlink.
2.GearBlinkcouldhaveaprojectedkeyboard.
Samsung’sGearBlinkcouldhaveaprojected
3.GearBlink’sprojectedkeyboardwouldallowtypinginair.
keyboardthatallowsyoutotypeintheair.
4.RalphLaurenhasaproductcalledPoloTechShirt.
| Ralph | Lauren’s | Polo Tech | Shirt uses bio- |     |     |     |     |     |     |     |
| ----- | -------- | --------- | --------------- | --- | --- | --- | --- | --- | --- | --- |
5.PoloTechShirtusesbio-sensingfabrics.
sensingfabricstomonitorphysicalactivity.
6.PoloTechShirtbio-sensingfabricsmonitorphysicalactivity.
Hushearplugsfilteroutunwelcomesounds
7.ThereisaproductcalledHushearplugs.
whileallowingphonecallsandalarmstoin-
8.Hushearplugsfilteroutunwelcomesounds.
trude.
9.Hushearplugsallowphonecallstobeheard.
10.Hushearplugsallowalarmstobeheard.
Table1: Anexamplesummarytextofanewsarticle&extractedatomicclaimsbyourclaimextractor.
OurHalluMeasuremethodworksbyfirstdecom- • RQ4: Can HalluMeasure effectively detect
posingtheLLMresponseintoasetofclaimsusing fine-grainedhallucinationerrortypes?
| a claim | extraction | model. | Then, we classify | the |        |     |          |     |        |           |
| ------- | ---------- | ------ | ----------------- | --- | ------ | --- | -------- | --- | ------ | --------- |
|         |            |        |                   |     | • RQ5: |     | Does the | use | of CoT | prompting |
claimsinto5keyclasses(e.g.,supported,absent,
|                |     |                      |                |     | improve |     | hallucination |     | measurement | perfor- |
| -------------- | --- | -------------------- | -------------- | --- | ------- | --- | ------------- | --- | ----------- | ------- |
| contradiction, |     | partially supported, | and unevaluat- |     |         |     |               |     |             |         |
mance?
| able) by | comparing | them | against the contexts | us- |     |     |     |     |     |     |
| -------- | --------- | ---- | -------------------- | --- | --- | --- | --- | --- | --- | --- |
ing our claim classification model. Additionally, • RQ6: How effectively can HalluMeasure’s
weclassifytheclaimsinto10noveldistincterror method generalize to different underlying
| types (e.g., | entity, | temporal, | over-generalization, |     |     |     |     |     |     |     |
| ------------ | ------- | --------- | -------------------- | --- | --- | --- | --- | --- | --- | --- |
LLMsforhallucinationclassification?
etc.) thatprovideafine-grainedanalysisofhallu-
Ourkeycontributionsare(1)anovelHalluMea-
| cinationerrors. |     | Finally,weproduceanaggregated |     |     |     |     |     |     |     |     |
| --------------- | --- | ----------------------------- | --- | --- | --- | --- | --- | --- | --- | --- |
hallucination score by measuring the rate of un- suremethodthatautomaticallymeasureshallucina-
tionsusingfine-grainedanalysisofLLMresponses
supportedclaims(i.e.,thoseassignedclassesother
usingChain-of-Thoughtreasoning,(2)experimen-
| than supported), |     | and calculate | the distribution | of  |     |     |     |     |     |     |
| ---------------- | --- | ------------- | ---------------- | --- | --- | --- | --- | --- | --- | --- |
talresultsofourHalluMeasuremethodthatoutper-
| fine-grainederrortypes. |     | Thisdistributionprovides |     |     |     |     |     |     |     |     |
| ----------------------- | --- | ------------------------ | --- | --- | --- | --- | --- | --- | --- | --- |
formsexistingsolutions(RefChecker,AlignScore,
LLMbuilderswithvaluableinsightsintothenature
|     |     |     |     |     | and Vectara | HHEM), |     | and (3) | a novel | TechNews- |
| --- | --- | --- | --- | --- | ----------- | ------ | --- | ------- | ------- | --------- |
oferrorstheirLLMismaking,facilitatingtargeted
Summdatasetcontainingfine-grainedclaimlevel
| improvements. |     | Figure1illustratesthemaincom- |     |     |     |     |     |     |     |     |
| ------------- | --- | ----------------------------- | --- | --- | --- | --- | --- | --- | --- | --- |
labelsfornewssummarizationtaskwithtechnews
ponentsandprocessbehindHalluMeasure.
articlestakenfromCNN/DailyMaildataset.
OurresultsdemonstratethatHalluMeasureout-
| performs | existing | solutions | in terms of | F1 score |     |     |     |     |     |     |
| -------- | -------- | --------- | ----------- | -------- | --- | --- | --- | --- | --- | --- |
2 RelatedWork
| andAUCROCmetricontwodatasets: |     |     | TechNews- |     |     |     |     |     |     |     |
| ----------------------------- | --- | --- | --------- | --- | --- | --- | --- | --- | --- | --- |
Summ (our own curated dataset) and a popular Hallucinationisatopicofgrowingresearchinter-
publicbenchmarkdatasetSummEval(Fabbrietal., est, and a range of prior studies have addressed
|     |     |     |     |     | its identification |     | and measurement. |     |     | Several sur- |
| --- | --- | --- | --- | --- | ------------------ | --- | ---------------- | --- | --- | ------------ |
2021). WeattributeHalluMeasure’ssuperiorper-
formanceto(1)ourimprovedpromptingstrategy veypapersprovideausefuloverviewandanalysis
that utilizes Chain-of-Thought (CoT) reasoning, (Huangetal.,2023;Wangetal.,2024;Rawteetal.,
2023). Anumberofworksprovideeitherahallu-
and(2)ourclaim-levelclassificationapproachthat
measureshallucinationbasedonfine-grainedinfor- cinationmeasurementdataset(Lietal.,2023;Lin
mationpresentintheresponsetext. etal.,2022;Tametal.,2023),anautomaticevalu-
We attempt to answer the following 6 key re- ationmetric(Zhaetal.,2023;Chernetal.,2023;
|     |     |     |     |     | Min et | al., 2023; | Manakul | et  | al., 2023; | Mündler |
| --- | --- | --- | --- | --- | ------ | ---------- | ------- | --- | ---------- | ------- |
searchquestionsaspartofthisstudy:
etal.,2024;Gekhmanetal.,2023;Krys´cin´skietal.,
| • RQ1: | HoweffectivelycanHalluMeasureex- |     |     |     |     |     |     |     |     |     |
| ------ | -------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
2019)orameta-evaluation(i.e.,evaluationofdif-
tractclaimsfromLLMresponses? ferent hallucination metric performances) (Hon-
|        |                               |     |     |     | ovich et   | al.,  | 2022; Gabriel |       | et al., 2021). | Many       |
| ------ | ----------------------------- | --- | --- | --- | ---------- | ----- | ------------- | ----- | -------------- | ---------- |
| • RQ2: | HowdoesHalluMeasuremethodcom- |     |     |     |            |       |               |       |                |            |
|        |                               |     |     |     | of the use | cases | addressed     | focus | on             | summariza- |
pareagainststate-of-the-artmethods?
|     |     |     |     |     | tion (e.g., | news | summarization |     | or headline | gen- |
| --- | --- | --- | --- | --- | ----------- | ---- | ------------- | --- | ----------- | ---- |
• RQ3: Is a single call to classify all claims eration) and use popular news datasets for test-
effectiveforhallucinationclassification? ing (CNN/DailyMail news articles corpus (See
15022

et al., 2017), or XSUM news headline dataset 3.1 ExtractingClaimsfromLLMResponses
| (Narayanetal.,2018)). |     | Anotherpopularusecase |     |     |     |     |     |     |
| --------------------- | --- | --------------------- | --- | --- | --- | --- | --- | --- |
Asnotedabove,ourapproachdecomposesanLLM
isWikipedia-stylebiographygeneration(e.g.,asin
|                                    |     |     |             | responseintoasetofclaims. |                  | Anintuitivedefinition |             |      |
| ---------------------------------- | --- | --- | ----------- | ------------------------- | ---------------- | --------------------- | ----------- | ---- |
| WikiBiodataset(Lebretetal.,2016)). |     |     | Previousap- |                           |                  |                       |             |      |
|                                    |     |     |             | of claim                  | is ‘the smallest | unit of               | information | that |
proachestomeasurementincludeusingpretrained
canbeevaluatedagainstacontext’;intheprototyp-
orfinetunedmodelsorNLI-andQuestion-Answer-
icalcase,thisconsistsofasinglepredicatewitha
| Generation                            | (QAG)-based | metrics. | More recent |                                 |     |     |               |     |
| ------------------------------------- | ----------- | -------- | ----------- | ------------------------------- | --- | --- | ------------- | --- |
|                                       |             |          |             | subjectand(optionally)anobject. |     |     | Severalrecent |     |
| studiesemployLLMstoclassifyresponses. |             |          | Most        |                                 |     |     |               |     |
ofthese(Zhaetal.,2023;Vectara,2023)classifyat worksonhallucinationandfactualitydecompose
|     |     |     |     | sentencesintoclaimsforevaluation; |     |     | however, | as  |
| --- | --- | --- | --- | --------------------------------- | --- | --- | -------- | --- |
theresponselevelwhileasmallernumberclassify
|     |     |     |     | noted by | Wanner et al. | (2024), | the method | of de- |
| --- | --- | --- | --- | -------- | ------------- | ------- | ---------- | ------ |
atthesentence(Kryscinskietal.,2020;Labanetal.,
compositionaffectsthenumberofclaimsextracted
2021)orfine-grainedclaimlevel(Minetal.,2023;
fromagivenmodelresponse,andthereforeimpacts
| Chernetal.,2023). | Further,theydifferinwhether |     |     |               |          |             |        |         |
| ----------------- | --------------------------- | --- | --- | ------------- | -------- | ----------- | ------ | ------- |
|                   |                             |     |     | hallucination | metrics. | In general, | higher | atomic- |
theyuseabinaryhallucination/non-hallucination
ityofclaimsallowsformoreprecisemeasurement
| classification, | ternary        | NLI classes | (Chern et al., |                                  |     |     |             |     |
| --------------- | -------------- | ----------- | -------------- | -------------------------------- | --- | --- | ----------- | --- |
|                 |                |             |                | andlocalizationofhallucinations. |     |     | Table1shows |     |
| 2023; Min       | et al., 2023), | or perform  | fine-grained   |                                  |     |     |             |     |
anexampleresponsewiththeclaimsextractedby
| multi-class | classification | to divide | hallucination |     |     |     |     |     |
| ----------- | -------------- | --------- | ------------- | --- | --- | --- | --- | --- |
ourclaimextractor.
intodifferenterrortypes(e.g.,negationerror,num-
|                            |     |                    |     | We develop | a claim | extraction | model | which, |
| -------------------------- | --- | ------------------ | --- | ---------- | ------- | ---------- | ----- | ------ |
| berswap,orentityswap,etc.) |     | (Rawteetal.,2023). |     |            |         |            |       |        |
A number of different taxonomies of hallucina- givenanLLMresponse,decomposesthatresponse
tion error types have been proposed (Tang et al., intoclaimstobeevaluated. Weprompttheclaim
extractionmodelusingasmallsetofdemoexample
| 2023; Zhu | et al., 2023; | Tang et | al., 2024). We |     |     |     |     |     |
| --------- | ------------- | ------- | -------------- | --- | --- | --- | --- | --- |
build on these earlier approaches by combining responseswithmanuallyextractedclaims,which
claim-levelanalysiswithfine-grainederrortypes have been judged to be both atomic and compre-
|     |     |     |     | hensive | (i.e., the claims | list covers | all | significant |
| --- | --- | --- | --- | ------- | ----------------- | ----------- | --- | ----------- |
(distinguishedbasedontheirimpactandpotential
|     |     |     |     | informationfromtheresponsetext). |     |     | Notethatun- |     |
| --- | --- | --- | --- | -------------------------------- | --- | --- | ----------- | --- |
causesormitigations),andbyusingcurrentLLMs
withfew-shotlearningandCoTpromptingtopro- like some existing approaches (Min et al., 2023),
wedon’tusesentencesinresponsestodecompose
ducestrongresultsinmeasuringhallucinationsat
|     |     |     |     | intoclaims. | Rather,wedirectlyextractthelistof |     |     |     |
| --- | --- | --- | --- | ----------- | --------------------------------- | --- | --- | --- |
boththeclaimandresponselevels.
|     |     |     |     | claims | from the full | response text | since | a single |
| --- | --- | --- | --- | ------ | ------------- | ------------- | ----- | -------- |
claimmayincorporateinformationfrommorethan
| 3 Method |     |     |     | onesentence(e.g. | entityresolution,reasoning). |     |     |     |
| -------- | --- | --- | --- | ---------------- | ---------------------------- | --- | --- | --- |
WeutilizetheAmazonBedrockhostedClaude
In this section we present methodology for Hal- 2.1model(withtemperature=0.8andtop_p=0.9)
| luMeasure. | Weuseaclaim-levelhallucinationmea- |     |     |     |     |     |     |     |
| ---------- | ---------------------------------- | --- | --- | --- | --- | --- | --- | --- |
(AmazonWebServices)todevelopourclaimex-
surementapproachinspiredbyChernetal.(2023),
tractor. Theprocessinvolvesdevelopingaprompt
Huetal.(2023),andMinetal.(2023). Wedecom- that enables the model to learn how to extract
poseLLMresponsesintosmallerunits(‘claims’)
|     |     |     |     | claimsfromanLLMresponse. |     |     | Thepromptstruc- |     |
| --- | --- | --- | --- | ------------------------ | --- | --- | --------------- | --- |
formoreprecisemeasurementusingourclaimex-
turebeginswithaninitialinstruction,followedby
traction model based on Claude 2.1. Then, we a set of rules outlining the task requirements. It
classifyclaimsandassignhigh-levellabels,further alsoincludesaselectionofexampletextsaccom-
identifying10morespecifictypesofhallucination
|     |     |     |     | paniedbytheirmanuallyextractedclaims. |     |     |     | Finally, |
| --- | --- | --- | --- | ------------------------------------- | --- | --- | --- | -------- |
errorsforunsupportedclaimsusingCoTreasoning
thepromptendswiththetargetresponse(i.e.,LLM
withClaude3Sonnet(SeeTable9). responseunderevaluation)fromwhichthemodel
HalluMeasurecalculatesthepercentageofhal- needs to extract the relevant claims. By provid-
lucinations at both the claim and response level, ing this comprehensive prompt, we aim to effec-
andprovidesthedistributionofhallucinationtypes tivelyteach(withoutupdatingweights)Claudeto
identified. Below, we discuss specific compo- accuratelyextractclaimsfromanygivenresponse.
nents of our hallucination measurement method Once Claude returns the claims as a text string,
that takes in context and response pairs as input weconvertitintoaPythonlisttostoreasalistof
andproduceshallucinationscoresasoutput. Fig- claimsassociatedwiththeresponse. Figure3inthe
ure1showstheHalluMeasureprocess. appendixprovidesthepromptforclaimextraction.
15023

Number Aclaimhasadifferentnumberthantheoriginalcontext(e.g. 20%vs. 0.7%). Any
number,includingyear,dimensions,ages,etc.
Entity Aclaimincludesswapped, incorrectlyspecified, orinsertednounphrases(e.g. one
namedentityusedinacontextwhereanotherwordisexpected).
FalseConcatenation Aclaimincorrectlycombinesinformationaboutmultipleentitiesorevents.
AttributionFailure Aclaimlacksproperattribution,eithercreditingthewrongsourceorpresentinginforma-
tionasfactwithoutcitation.
Overgeneralization Aclaimisbasedonaccuratecontextualinformationbutistoobroadortoogeneraltobe
supportedbythecontext.
ReasoningError Aclaimisbasedonaccuratecontextualinformationbutcontainsareasoningerroror
makesanunsupportedconclusion.
Hyperbole Aclaimisbasedonaccurateinformationbutexaggeratedoroverstated.
Temporal Aclaimdoesnotaccuratelyincorporatetense,modality(e.g. mightvs. will),ortime
referenceinrelationtothecontext.
Context-basedmeaningerror Aclaimincludesincorrectinterpretationofidiomaticlanguage,homonyms,orwords
withmultiplemeanings,thereforefailingtocapturetheintendedmeaning.
Other Allothertypesoferrorsarecapturedinthiscategory.Thisincludestoo-farinferences,
circumstantialerrors,orincoherentsentencesorparagraphs.
|     |     |     |     | Table2: | Specificsubtypesofhallucinations. |     |     |     |     |     |     |     |
| --- | --- | --- | --- | ------- | --------------------------------- | --- | --- | --- | --- | --- | --- | --- |
3.2 ClassifyingClaimsintoHallucination IdentifyingPartiallySupportedclaimsisuniqueto
|     |     |     |     |     |     |     | ourapproach. |     | Examplesinclude: |     | missing/incorrect |     |
| --- | --- | --- | --- | --- | --- | --- | ------------ | --- | ---------------- | --- | ----------------- | --- |
Labels
attribution,number/conjunctionmisinterpretation,
| When comparing |     | claims | against | a   | reference | con- |     |      |            |              |                |     |
| -------------- | --- | ------ | ------- | --- | --------- | ---- | --- | ---- | ---------- | ------------ | -------------- | --- |
|                |     |        |         |     |           |      | and | mild | hyperbole. | For example, | if the context |     |
text,ourprimarydistinctionisbetweenclaimsthat
|     |     |     |     |     |     |     |     | "According |     | to the company, | their revenue |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ---------- | --- | --------------- | ------------- | --- |
states,
| are supported |     | vs. unsupported |     | by  | the context. | A   |     |     |     |     |     |     |
| ------------- | --- | --------------- | --- | --- | ------------ | --- | --- | --- | --- | --- | --- | --- |
increased"thentheclaim"Thecompany’srevenue
| claimissupported |       | if,undernormalcircumstances, |           |     |         |       |                                      |     |     |     |         |     |
| ---------------- | ----- | ---------------------------- | --------- | --- | ------- | ----- | ------------------------------------ | --- | --- | --- | ------- | --- |
|                  |       |                              |           |     |         |       | increased"wouldbePartiallySupported. |     |     |     | Inaddi- |     |
| a reader         | would | believe                      | the claim | to  | be true | given |                                      |     |     |     |         |     |
tiontotheaboveclaimtypes,wehaveanUneval-
| the context. |     | We divide | unsupported |     | claims | into |     |     |     |     |     |     |
| ------------ | --- | --------- | ----------- | --- | ------ | ---- | --- | --- | --- | --- | --- | --- |
uatableclasslabelforclaimsthatdonotfallinto
| three main | types: |                 |     |     | claims: | the |     |     |     |     |     |     |
| ---------- | ------ | --------------- | --- | --- | ------- | --- | --- | --- | --- | --- | --- | --- |
|            |        | 1. Contradicted |     |     |         |     |     |     |     |     |     |     |
anyofthehigh-leveltypes(e.g.,questions).
| context | contains | information |     | which | is explicitly |     |     |     |     |     |     |     |
| ------- | -------- | ----------- | --- | ----- | ------------- | --- | --- | --- | --- | --- | --- | --- |
Withinunsupportedclaims,weidentifyspecific
| inconsistent | with          | the claim |                     | (‘intrinsic | hallucina- |     |          |     |                  |         |               |     |
| ------------ | ------------- | --------- | ------------------- | ----------- | ---------- | --- | -------- | --- | ---------------- | ------- | ------------- | --- |
|              |               |           |                     |             |            |     | subtypes |     | ofhallucinations | inorder | to understand |     |
| tion’). 2.   | Absentclaims: |           | thereisnoevidencein |             |            |     |          |     |                  |         |               |     |
thecontexttosupportorrefutetheclaim(‘extrin- andcomparehallucinationsfromspecificmodels
|                      |     |     |              |     |           |     | in  | more detail, | and | to potentially | apply such | in- |
| -------------------- | --- | --- | ------------ | --- | --------- | --- | --- | ------------ | --- | -------------- | ---------- | --- |
| sic hallucination’), |     | and | 3. Partially |     | Supported |     |     |              |     |                |            |     |
formationtostrategiesforreducingormitigating
claims: theclaimisalmostfullysupportedbythe
contextbuthasaminorerror. Wenotethatthecat- LLMhallucinations. Wecurrentlydistinguish10
egories Supported, Contradicted, and Absent are subtypes(seeTable2),thoughwewillcontinueto
refineourcategorizationbasedonemergingdataas
| similar | to Entailed, | Contradicted, |     | and | Neutral | in  |     |     |     |     |     |     |
| ------- | ------------ | ------------- | --- | --- | ------- | --- | --- | --- | --- | --- | --- | --- |
NLIterminology. However,theNLIlabelsmayim- partofourfuturework. Subtypesofhallucination
plyacontinuumfromentailmenttocontradiction, areexemplifiedinTable9intheappendix.
inwhichneutralappearstobealessererror-yet UnlikethetraditionalBERT-basedapproaches
manyofthemoststereotypicalandmostproblem- in some recent studies (Zha et al., 2023; Vec-
aticexamplesofhallucinationarethoseinwhicha tara, 2023), we leverage in-context prompting
modeladdscompletelynew,unsupportedcontent anddeveloptheclaimclassifierwiththeAmazon
initsoutput. Atthesametime,werecognizethat Bedrock-hostedClaude3Sonnetmodel(withtem-
thereareinfactdegreesofseverityoferrors,and perature 0.1 for reproducibility). Notably, our
≈
we therefore distinguish a class of Partially Sup- classifier not only detects the main hallucination
portedclaims. Distinguishingtheseclaimswhich labelsbutalsoidentifiesspecificsubtypes(aselab-
are unsupported in subtle ways allows us to both oratedinTable9),andprovidesanexplanationfor
quantifythepresenceofhallucinationerrors,and, the claim label. To analyze the effectiveness of
at least at a basic level, distinguish their severity. ourapproach,wehavedevelopedfourprompting
15024

|     | PromptingLLMwithCoT |     |     |     |     |     |     | PromptingLLMwithoutCoT |     |
| --- | ------------------- | --- | --- | --- | --- | --- | --- | ---------------------- | --- |
Step 1: Read and fully understand the claim. It is a short, Step1:Readandfullyunderstandtheclaim.
standalone sentence containing a single piece of information Itisashort,standalonesentencecontaining
relatedtothesourcetext. asinglepieceofinformationrelatedtothe
sourcetext.
Step2:Thoroughlyanalyzehowtheclaimrelatestotheinfor- Step2:Writethemostappropriatelabelfor
mationinthesourcetext. Then, writeyourreasoningin1-3 theclaimbasedonthesourcetext.
sentencestodeterminethemostappropriatelabeltodescribethe
claim’struthfulnessbasedonthesourcetext.
Step3:Writethelabelfortheclaimbasedonyourreasoningin Step 3: If the label in Step 2 is ’contra-
|     | Step2. |     |     |     |     |     |     | dicted’, ’absent’, | or ’partially supported’, |
| --- | ------ | --- | --- | --- | --- | --- | --- | ------------------ | ------------------------- |
thenwritethespecificerrortype(i.e.,subla-
bel)fortheclaim.
|     |     | 4: If the | label | in Step | 3 is ’contradicted’, |     | ’absent’, | or  |     |
| --- | --- | --------- | ----- | ------- | -------------------- | --- | --------- | --- | --- |
Step
’partiallysupported’,thenthoroughlyanalyzethespecificerrors
(i.e.,sublabels)presentintheclaimbasedonprovidedsource
text.Then,provideyourreasoningin1-3sentencestodetermine
theerror.However,ifthelabelinStep3is’supported’,simply
write’None-claimissupported’,andsetthesublabelto’None’.
Step5:WritesublabelbasedonyourreasoninginStep4.
|     |     |     | Table3: | InstructionstepsforpromptingLLMwithandwithoutCoT. |     |     |     |     |     |
| --- | --- | --- | ------- | ------------------------------------------------- | --- | --- | --- | --- | --- |
strategiestoinvestigatetwokeyaspects: 1)thepo- (dependingonthenumberofclaimsinaresponse).
tentialbenefitsofincorporatingChain-of-Thought Thesecondapproachincludesalltheclaimsinthe
(CoT)reasoning(Weietal.,2022),and2)whether samepromptandmakesasingleAPIcalltoClaude.
evaluatingclaimsindividually(requiringmultiple Werefertotheformerasone-claim-evalandthelat-
ClaudeAPIcalls)offersadvantagesoverevaluat- terasall-claims-eval. Whileall-claims-evalisbet-
ingallclaimstogether(requiringasingleAPIcall). terforreducinglatency,one-claim-evalperforms
Weprovidethefourpromptsetupsbelow. betterasitallowsthemodeltofocusononlyone
|                                   |     |     |     |     |     |     | claimatthetimeofevaluation. |     | SeeFigures6and |
| --------------------------------- | --- | --- | --- | --- | --- | --- | --------------------------- | --- | -------------- |
| (1)Withand(2)WithoutCoTReasoning. |     |     |     |     |     |     | We                          |     |                |
7forprompttemplates.
checkifaskingthemodeltothinkandanalyzebe-
|     |     |     |     |     |     |     | 3.3 | AggregatingScoresforHallucination |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --------------------------------- | --- |
foredecidingthelabelsandspecificerrorsubtypes
| (i.e., | sublabels) | is  | beneficial. |     | By following |     | Wei | Measurement |     |
| ------ | ---------- | --- | ----------- | --- | ------------ | --- | --- | ----------- | --- |
etal.(2022),wedevelopa5stepCoTprompt,in- After classifying claims, each claim has a label
cludingstepstothoroughlyexamineeachclaim’s (outof5labels)andanerrortype(outof10types)
| faithfulness |     | to the    | reference | context, |           | and writing |               |                                 |     |
| ------------ | --- | --------- | --------- | -------- | --------- | ----------- | ------------- | ------------------------------- | --- |
|              |     |           |           |          |           |             | assignedtoit. | Now,weassignascoreforhallucina- |     |
| down         | the | reasoning | behind    | the      | thoughts. |             | Simi-         |                                 |     |
tionandforeacherrortypebyaggregatingacross
lar to other reasoning tasks where CoT is useful allclaimsintheresponsesinthedataset. Wepro-
(Weietal.,2022)likemathematicalandcommon- duce two scores: 1) Response hallucination rate,
sensereasoning,wehypothesizethatthesewritten
calculatedbydividingthenumberofunsupported
thoughtsprovideinsightsintothemodel’sreason- claims(combiningdifferenterrortypes)bytheto-
ingprocesspriortoselectingthefinalhallucination talnumberofclaimsfortheresponse. 2)Errortype
| label | for | each claim. | Table | 3   | shows | the steps | for |     |     |
| ----- | --- | ----------- | ----- | --- | ----- | --------- | --- | --- | --- |
distribution,calculatedbyscoringsubtypeorclass
| with | and | without | CoT prompting |     | strategies. |     | See |     |     |
| ---- | --- | ------- | ------------- | --- | ----------- | --- | --- | --- | --- |
errorsseparately.
| Figures |     | 5 and 4 | for prompt | templates. |     | Figure | 2   |     |     |
| ------- | --- | ------- | ---------- | ---------- | --- | ------ | --- | --- | --- |
showsCoTmodeloutputwithThoughtsgenerated 4 ExperimentsandResults
forhallucinationlabelanderrortypesublabels.
|     |     |     |     |     |     |     | 4.1 | Dataset |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ------- | --- |
(3)One-claim-evaland(4)All-claims-eval. We We present the datasets used to evaluate our Hal-
checkifevaluatingeachclaimseparatelyisbetter luMeasure approach and compare with existing
than evaluating all claims together. The first ap- models. We create the first dataset, TechNews-
proachevaluateseachclaimindependentlyagainst Summ,bysampling30technewsarticlesfromthe
thecontextbymakingmultipleAPIcallstoClaude CNN/Dailymaildataset,collectingsummaries(20
15025

|     |                               | Response-level |        |      | Claim-level |           |
| --- | ----------------------------- | -------------- | ------ | ---- | ----------- | --------- |
|     |                               | Precision      | Recall | F1   | Precision   | Recall F1 |
|     | VectaraHHEM                   | 0.75           | 0.15   | 0.25 | -           | - -       |
|     | AlignScore                    | 0.57           | 0.20   | 0.30 | -           | - -       |
|     | RefChecker(AlignScoreChecker) | 0.68           | 0.75   | 0.71 | -           | - -       |
|     | RefChecker(NLIChecker)        | 0.75           | 0.75   | 0.75 | -           | - -       |
|     | RefChecker(ClaudeChecker)     | 0.79           | 0.75   | 0.77 | -           | - -       |
|     | W/oCoT+all-claims-eval(ours)  | 0.73           | 0.80   | 0.76 | 0.72        | 0.59 0.65 |
|     | W/CoT+all-claims-eval(ours)   | 0.85           |        | 0.85 | 0.73        | 0.70      |
|     |                               |                | 0.85   |      |             | 0.67      |
|     | W/oCoT+one-claim-eval(ours)   | 0.83           | 0.75   | 0.79 | 0.86        | 0.56 0.68 |
|     | W/CoT+one-claim-eval(ours)    | 0.89           | 0.85   | 0.87 | 0.87        | 0.66 0.75 |
Table4: ResultsonTechNewsSummDataset: Response-andclaim-levelevaluationmetricsfortheunsupported
labelobtainedwiththeexistingmethodsandthefoursettingsofourapproach. Forafaircomparison,weconvert
ourfourmainlabelsintobinarylabels(i.e.,supportedandunsupported).
|     |                        | APICallTime | #PromptTokens(K) |        | #OutputTokens(K) |      |
| --- | ---------------------- | ----------- | ---------------- | ------ | ---------------- | ---- |
|     | W/oCoT+all-claims-eval | 9.45        |                  | 6.27   |                  | 0.51 |
|     | W/oCoT+one-claim-eval  | 42.24       |                  | 81.51  |                  | 0.52 |
|     | W/CoT+all-claims-eval  | 40.21       |                  | 10.14  |                  | 1.27 |
|     | W/CoT+one-claim-eval   | 77.17       |                  | 133.10 |                  | 1.58 |
Table5: LatencyandTokenStatsonTechNewsSummExperiments: ClaudeAPIcalldurationandInput/Output
tokensforHalluMeasure’sClaimClassifier. Durationinseconds,tokencountsinthousands(K).Forone-claim-eval
setups,promptandoutputtokensfromallAPIcallsforasingleresponsearesummed.
fromtheCohereCommandmodeland10human- checker(GPT4,Claude2,NLI,orAlignScore). It
written), extracting atomic claims (400 claims) produceshallucinationscoresbasedonstrict(any
fromthesummariesusingourclaimextractor(Sec- contradicted claim means the response is labeled
tion2),andmanuallyevaluatingtheclaimsagainst as hallucination), soft (ratio of contradicted and
thereferencecontexttoidentifythreemaintypes neutralclaims),ormajorityvotingcriteria. Weuse
and10specifictypes(i.e.,subtypes)ofhallucina- the soft criteria for hallucination score and strict
| tions(Table9).                        | Weobservemoderateagreementbe- |       | forlabelassignment. |     |     |     |
| ------------------------------------- | ----------------------------- | ----- | ------------------- | --- | --- | --- |
| tweentheannotatorsinmainlabels(Kappa: |                               | 0.44) |                     |     |     |     |
andsubtypesannotations(Kappa: 0.45). Oursec- 4.3 HallucinationMeasurementExperiments
onddatasetistheSummEvaldataset(Fabbrietal., Weprovideexperimentalresultsforthesefourhal-
2021)with1600annotatedsamples(hallucination lucination measurement approaches (HalluMea-
vs. non-hallucination) at the response level from sure, RefChecker, AlignScore, and Vectara
theTRUEbenchmark(Honovichetal.,2022). HHEM).Tables4and6presentevaluationresults
onbinaryclassificationanderrorsubtypeclassifi-
4.2 Baselines
cationonourowncuratedTechNewsSummdataset.
WecompareHalluMeasurewiththreestate-of-the- Table7showsresultsontheSummEvaldataset.
art hallucination measurement approaches: Vec- Throughourexperiments,weattempttoanswer
taraHHEM(Vectara,2023)outputsafactualcon- ourresearchquestions(RQs)below:
sistencyscore(0-1)usingafinetunedcross-encoder RQ1: How effectively can HalluMeasure ex-
model. We use 1 - factual consistency score as tractclaimsfromLLMresponses?
hallucinationscoreandthresholdat0.5forlabelas- We validate our claim extractor’s accuracy by
signment. AlignScore(Zhaetal.,2023)classifies evaluating its performance on 25 tech news arti-
claims against contexts into aligned/not-aligned clesfromtheCNN/DailyMaildataset. Wegener-
classesusingaRoBERTamodeltrainedon7NLP ate summaries using Cohere’s Command model
tasks. We use 1 - aligned class score as halluci- and extract claims from these summaries. Four
nation score and threshold at 0.5. RefChecker researchers manually annotated the claims; each
(Huetal.,2023)splitsresponsesintoclaim-triplets claim was annotated by two annotators, with dis-
andchecksthemagainstreferencesusingaclaim agreements adjudicated. The rate of claims with
15026

|     |                      | #Adj. #Pred. | Precision Recall | F1   |
| --- | -------------------- | ------------ | ---------------- | ---- |
|     | Number               | 1 0          | 0.00 0.00        | 0.00 |
|     | Entity               | 3 9          | 0.11 0.50        | 0.18 |
|     | FalseConcatenation   | 6 1          | 0.00 0.00        | 0.00 |
|     | AttributionFailure   | 1 0          | 0.00 0.00        | 0.00 |
|     | Overgeneralization   | 6 13         | 0.15 0.50        | 0.24 |
|     | ReasoningError       | 10 7         | 0.14 0.17        | 0.15 |
|     | Hyperbole            | 3 2          | 1.00 1.00        | 1.00 |
|     | Temporal             | 3 4          | 0.50 1.00        | 0.67 |
|     | Context-basedmeaning | 6 0          | 0.00 0.00        | 0.00 |
|     | Other                | 48 28        | 0.93 0.58        | 0.71 |
|     | Macro-average        |              | 0.32 0.47        | 0.33 |
|     | Weighted-average     |              | 0.71 0.52        | 0.58 |
Table6: ErrorSubtypesClassificationPerformanceonTechNewsSummDataset: Evaluationresultsonthespecific
subtypesofhallucinationsobtainedwithourbestsetupofHalluMeasuremodel(i.e.,W/CoT+one-claim-eval).
#Adj. denotesthecountofadjudicatedsubtypes,and#Pred. denotesthecountofpredictedsubtypes.
disagreements is 6.5% (12/185). The adjusted pointson1600samplesofSummEval. Thebase-
Cohen’s kappa (PABAK) score of 0.87 indicates linemodels’AUCROCvaluesare: VectaraHHEM:
strongannotatoragreement. Usingtheadjudicated 0.77, AlignScore: 0.71, RefChecker (Alignscore
claims as ground truth, the claim extractor’s pre- checker): 0.75, RefChecker (NLI checker): 0.75,
cision is 0.96. Since there is no definitive gold andRefChecker(Claude2): 0.74. Ourresultson
setofclaims,wecomputearevisedrecallmetric SummEvalshowthatHalluMeasuresignificantly
ascorrectlyextractedclaims/(correctlyextracted outperformsseveralexistingbaselinemodels. So,
claims+missingcorrectclaims). Therevisedrecall results on two datasets show that HalluMeasure
and F1-score of 0.97 indicate the claim extractor outperformsexistingstate-of-the-artmodels.
accuratelyextractsclaimsfromresponses. RQ3: Isasinglecalltoclassifyallclaimseffec-
RQ2: How does HalluMeasure method com- tiveforhallucinationclassification?
pareagainststate-of-the-artmethods? We answer this question by comparing the re-
We answer this question by comparing our sults for one-claim-eval vs. all-claims-eval from
methodwithRefChecker,AlignScore,andVectara Table4. Evaluatingoneclaimatatimeisbeneficial
HHEM.Outofthesethreemethods,RefChecker’s overevaluatingallclaimstogetherbasedonresults
onbothresponseandclaimlevelevaluations(e.g.,
| approach | is similar to HalluMeasure | with a key |     |     |
| -------- | -------------------------- | ---------- | --- | --- |
distinction that we use CoT few-shot prompting F1: 0.75vs. 0.70). However,all-claims-evalcomes
insteadofsimplefew-shotpromptingemployedby withbenefitofimprovedlatencyandcostcompared
RefChecker. Theremainingtwomethods(Align- toone-claim-eval(9.45secsvs. 42.24secsforW/o
ScoreandVectaraHHEM)arespecificallytrained CoTprompt;40.21secsvs. 77.71secsforW/CoT
tomeasurehallucinationsusingBERT-basedmod- prompt). SeeTable5fordetails.
els. While RefChecker performs similarly to RQ4: CanHalluMeasureeffectivelydetectfine-
someofourpromptingsetups(e.g. withoutCoT), grainedhallucinationerrortypes?
HHEMandAlignScoreachievelowerperformance While HalluMeasure’s best setup shows excel-
on our TechNewsSumm dataset. Our best setup lentoverallresults,itstrugglestoaccuratelyclas-
(HalluMeasureW/CoT+one-claim-eval)outper- sify the specific error types, with macro-F1 and
formsexistingmodelsbyatleast13%F1scoreon
weighted-F1scoresofonly0.33and0.58,respec-
TechNewsSummdataset(SeeTable4). tively(Table6). Thisislikelyduetohaving10dif-
Todemonstrateperformanceonapublicbench- ferenterrortypes,withsimilarclassificationissues
mark dataset, we show experimental results on demonstrated by low human agreement (Kappa:
the popular SummEval dataset in Table 7. Note 0.45)asmentionedinSection4.1. Moreover,some
thatwereportAUCROCscoresontheSummEval errortypesarehardtodistinguishandmaynotin
dataset as computed using the TRUE benchmark factbemutuallyexclusive,suchasreasoningerror
softwarepackage(Honovichetal.,2022). OurHal- vs. context-based meaning, and false concatena-
luMeasuremodelachievesanAUCROCvalueof tionvs. overgeneralization. Improvingtheaccurate
0.80,outperformingthebaselinemodelsby3to9 identificationofthesespecificerrortypesremains
15027

|             |     |     |     | AUCROC |      |     |                       |     |     | Precision | Recall | F1   |
| ----------- | --- | --- | --- | ------ | ---- | --- | --------------------- | --- | --- | --------- | ------ | ---- |
| VectaraHHEM |     |     |     |        | 0.77 |     | Cohere’sCommandR+     |     |     |           |        |      |
| AlignScore  |     |     |     |        | 0.71 |     | W/oCoT+one-claim-eval |     |     | 0.79      | 0.75   | 0.77 |
RefChecker(AlignScoreChecker) 0.75 W/CoT+one-claim-eval 0.76 0.80 0.78
| RefChecker(NLIChecker) |     |     |     |     | 0.75 |     |     |     |     |     |     |     |
| ---------------------- | --- | --- | --- | --- | ---- | --- | --- | --- | --- | --- | --- | --- |
Mistrallarge
| RefChecker(ClaudeChecker) |     |     |     |     | 0.74 |     |                       |     |     |      |      |      |
| ------------------------- | --- | --- | --- | --- | ---- | --- | --------------------- | --- | --- | ---- | ---- | ---- |
|                           |     |     |     |     |      |     | W/oCoT+one-claim-eval |     |     | 0.68 | 0.95 | 0.79 |
HalluMeasure(ours;W/oCoT) 0.78 W/CoT+one-claim-eval 0.69 0.90 0.78
| HalluMeasure(ours;W/CoT) |     |     |     |     | 0.80 |     |          |                |         |      |          |      |
| ------------------------ | --- | --- | --- | --- | ---- | --- | -------- | -------------- | ------- | ---- | -------- | ---- |
|                          |     |     |     |     |      |     | Table 8: | Response-level | results | from | Cohere’s | Com- |
Table7:PerformanceComparisononSummEvalBench- mandR+andMistralLargeLLMsonTechNewsSumm.
mark: AUCROCscoresobtainedwithexistingmodels
andHalluMeasure(W/CoTandW/oCoT+one-claim-
| eval)ontheSummEvaldataset(Fabbrietal.,2021). |     |     |     |     |     |     | 5 Conclusion |     |     |     |     |     |
| -------------------------------------------- | --- | --- | --- | --- | --- | --- | ------------ | --- | --- | --- | --- | --- |
WeintroduceHalluMeasure,anovelapproachto
|     |     |     |     |     |     |     | automatically | measure | hallucinations |     | in  | LLM re- |
| --- | --- | --- | --- | --- | --- | --- | ------------- | ------- | -------------- | --- | --- | ------- |
apriorityforfuturework.
|           |          |     |     |           |         |     | sponses. | HalluMeasure |     | decomposes | an  | LLM re- |
| --------- | -------- | --- | --- | --------- | ------- | --- | -------- | ------------ | --- | ---------- | --- | ------- |
| RQ5: Does | few-shot |     | CoT | prompting | improve |     |          |              |     |            |     |         |
sponseintosetofclaimsusingaclaimextraction
thehallucinationmeasurementperformance? modelbasedonClaudewithfew-shotprompting.
|     |     |     |     |     |     |     | It compares | the extracted |     | claims | against | a con- |
| --- | --- | --- | --- | --- | --- | --- | ----------- | ------------- | --- | ------ | ------- | ------ |
Weanswerthisquestionbycomparingtheper-
formance of our claim classifier model with and text document using a claim classification model
without CoT prompting. Table 4 shows that in leveragingfew-shotChain-of-Thoughtprompting
withClaudetoenhanceclassificationperformance.
| both one-claim-eval |     | and      | all-claims-eval |             | settings, |     |               |                |     |     |          |          |
| ------------------- | --- | -------- | --------------- | ----------- | --------- | --- | ------------- | -------------- | --- | --- | -------- | -------- |
|                     |     |          |                 |             |           |     | An aggregated | response-level |     |     | score is | produced |
| CoT prompting       |     | improves | model           | performance |           | on  |               |                |     |     |          |          |
ourTechNewsSummdatasetatbothresponse-level by measuring the rate of unsupported claims and
|              |                            |     |     |     |     |        | distribution                            | of specific | error | types. | We  | demon- |
| ------------ | -------------------------- | --- | --- | --- | --- | ------ | --------------------------------------- | ----------- | ----- | ------ | --- | ------ |
| (F1: 0.85vs. | 0.76)andclaim-level(0.7vs. |     |     |     |     | 0.65). |                                         |             |       |        |     |        |
|              |                            |     |     |     |     |        | stratetheeffectivenessofHalluMeasureon: |             |       |        |     | Tech-  |
Table7alsoshowsthatCoTpromptingimproves
model performance on SummEval public bench- NewsSumm(ourowncurateddatasetwithdetailed
markdataset(AUCROC:0.78vs. 0.80). claim-levelerrorlabels)andSummEval(apopular
|                   |     |              |     |                |     |        | benchmarkdataset). |          | OurresultsdemonstrateHal- |     |      |          |
| ----------------- | --- | ------------ | --- | -------------- | --- | ------ | ------------------ | -------- | ------------------------- | --- | ---- | -------- |
| RQ6:              | How | effectively  | can | HalluMeasure’s |     |        |                    |          |                           |     |      |          |
|                   |     |              |     |                |     |        | luMeasure’s        | superior | performance               |     | over | baseline |
| method generalize |     | to different |     | LLMs           | for | hallu- |                    |          |                           |     |      |          |
models,withatleasta10-pointF1scoreimprove-
cinationclassification?
mentonTechNewsSummanda3-pointAUCROC
We present additional results with Cohere’s increaseonSummEval. Forfuturework,weplan
Command R+ and Mistral Large models on the to employ dynamic few-shot prompting and use
| TechNewsSumm |     | dataset | in Table | 8.  | We only | ex- |     |     |     |     |     |     |
| ------------ | --- | ------- | -------- | --- | ------- | --- | --- | --- | --- | --- | --- | --- |
optimizedpromptswithfast-inferenceLLMs.
perimentwiththeone-claim-evalsetupduetoread
| timeoutissueswiththeall-claims-evalsetup;and |     |     |     |     |     |     | Limitations |     |     |     |     |     |
| -------------------------------------------- | --- | --- | --- | --- | --- | --- | ----------- | --- | --- | --- | --- | --- |
weobtainonlyresponse-levelresultsduetothead-
Ourstudydetects10hallucinationerrortypes,in-
ditionalannotationeffortrequiredforclaim-level
|           |                                     |     |     |     |     |     | cludinganOtherclass. |     | Weplantofurtherexplore |     |     |     |
| --------- | ----------------------------------- | --- | --- | --- | --- | --- | -------------------- | --- | ---------------------- | --- | --- | --- |
| analysis. | Theresultsshowthat,unlikeClaudeSon- |     |     |     |     |     |                      |     |                        |     |     |     |
andrefineerrorcategorizationforbetterdetection
| net 3.0, Command |     | R+  | and Mistral | Large |     | exhibit |                |             |     |               |     |         |
| ---------------- | --- | --- | ----------- | ----- | --- | ------- | -------------- | ----------- | --- | ------------- | --- | ------- |
|                  |     |     |             |       |     |         | and to support | mitigation. |     | Additionally, |     | we have |
similarresultsforbothwithandwithoutCoTap-
focusedmainlyonhallucinationdetectioninplain
proaches,withF1scoresrangingfrom0.77to0.79.
|     |     |     |     |     |     |     | text responses, | and | have | yet to | explore | detecting |
| --- | --- | --- | --- | --- | --- | --- | --------------- | --- | ---- | ------ | ------- | --------- |
However,thesescoresaresignificantlylowerthan
andmeasuringhallucinationsinotherformatslike
| the best results |     | we achieved |     | with Claude |     | Sonnet |                |                            |     |     |     |     |
| ---------------- | --- | ----------- | --- | ----------- | --- | ------ | -------------- | -------------------------- | --- | --- | --- | --- |
|                  |     |             |     |             |     |        | tablesandcode. | Whileourfocustodatehasbeen |     |     |     |     |
(0.87). WealsocheckHalluMeasure’sperformance
onnewsarticlebenchmarks,weaimtoincludespe-
| with these | LLMs | on the | SummEval |     | dataset. | Sur- |     |     |     |     |     |     |
| ---------- | ---- | ------ | -------- | --- | -------- | ---- | --- | --- | --- | --- | --- | --- |
cializeddomainslikemedicine,law,andfinance.
| prisingly, | Mistral | Large | performs | slightly |     | better |     |     |     |     |     |     |
| ---------- | ------- | ----- | -------- | -------- | --- | ------ | --- | --- | --- | --- | --- | --- |
thanClaude,achievinganAUCROCscoreof0.81,
Acknowledgement
| while Command |     | R+ scores |     | 0.73. These |     | results |     |     |     |     |     |     |
| ------------- | --- | --------- | --- | ----------- | --- | ------- | --- | --- | --- | --- | --- | --- |
showthatperformancemaybesensitivetocharac- TheauthorswouldliketothankLisaBaytler,UX
teristics of the dataset, and proprietary LLMs do designer,forherassistanceincreatingfiguresfor
| notalwaysout-performopensourcemodels. |     |     |     |     |     |     | thispaper. |     |     |     |     |     |
| ------------------------------------- | --- | --- | --- | --- | --- | --- | ---------- | --- | --- | --- | --- | --- |
15028

| References |     |     |     |     |     | PhilippeLaban,TobiasSchnabel,PaulN.Bennett,and |         |       |         |             |      |
| ---------- | --- | --- | --- | --- | --- | ---------------------------------------------- | ------- | ----- | ------- | ----------- | ---- |
|            |     |     |     |     |     | Marti A.                                       | Hearst. | 2021. | Summac: | Re-visiting | nli- |
Amazon Web Services. Amazon bedrock. basedmodelsforinconsistencydetectioninsumma-
https://aws.amazon.com/bedrock/?refid= Preprint,arXiv:2111.09525.
rization.
36201f68-a9b0-45cc-849b-8ab260660e1c.
| Accessed: | 05-30-2024. |     |     |     |     |                                     |     |     |     |     |            |
| --------- | ----------- | --- | --- | --- | --- | ----------------------------------- | --- | --- | --- | --- | ---------- |
|           |             |     |     |     |     | R.Lebret,D.Grangier,andM.Auli.2016. |     |     |     |     | NeuralText |
GenerationfromStructuredDatawithApplication
| ZhoujunCheng,JungoKasai,andTaoYu.2023. |     |     |     |     | Batch |                  |     |        |      |             |        |
| -------------------------------------- | --- | --- | --- | --- | ----- | ---------------- | --- | ------ | ---- | ----------- | ------ |
|                                        |     |     |     |     |       | to the Biography |     | Domain | . In | Proceedings | of the |
prompting: Efficientinferencewithlargelanguage 2016ConferenceonEmpiricalMethodsinNatural
modelapis. arXivpreprintarXiv:2301.08721. LanguageProcessing(EMNLP).
I-ChunChern,SteffiChern,ShiqiChen,WeizheYuan, JunyiLi,XiaoxueCheng,WayneXinZhao,Jian-Yun
KehuaFeng,ChuntingZhou,JunxianHe,Graham Nie, and Ji-Rong Wen. 2023. Halueval: A large-
| Neubig, | and Pengfei | Liu. | 2023. | Factool: | Factual- |                    |     |                     |     |     |          |
| ------- | ----------- | ---- | ----- | -------- | -------- | ------------------ | --- | ------------------- | --- | --- | -------- |
|         |             |      |       |          |          | scalehallucination |     | evaluationbenchmark |     |     | forlarge |
ity detection in generative ai – a tool augmented languagemodels. Preprint,arXiv:2305.11747.
frameworkformulti-taskandmulti-domainscenar-
ios. Preprint,arXiv:2307.13528. StephanieLin,JacobHilton,andOwainEvans.2022.
|     |     |     |     |     |     | Truthfulqa: | Measuring |     | how models | mimic | human |
| --- | --- | --- | --- | --- | --- | ----------- | --------- | --- | ---------- | ----- | ----- |
CNBC.2023. Judgesanctionslawyersforbriefwritten falsehoods. Preprint,arXiv:2109.07958.
bya.i.withfakecitations.
PotsaweeManakul,AdianLiusie,andMarkJ.F.Gales.
|     |     |     |     |     |     | 2023. Selfcheckgpt: |     | Zero-resource |     | black-box | hal- |
| --- | --- | --- | --- | --- | --- | ------------------- | --- | ------------- | --- | --------- | ---- |
AlexanderR.Fabbri,WojciechKrys´cin´ski,BryanMc-
Cann,CaimingXiong,RichardSocher,andDragomir lucination detection for generative large language
Radev.2021. Summeval: Re-evaluatingsummariza- models. Preprint,arXiv:2303.08896.
| tionevaluation. |     | Preprint,arXiv:2007.12626. |     |     |     |     |     |     |     |     |     |
| --------------- | --- | -------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
SewonMin,KalpeshKrishna,XinxiLyu,MikeLewis,
|                 |          |              |       |            |            | Wen-tau                           | Yih, Pang | Koh, | Mohit | Iyyer, | Luke Zettle- |
| --------------- | -------- | ------------ | ----- | ---------- | ---------- | --------------------------------- | --------- | ---- | ----- | ------ | ------------ |
| Saadia Gabriel, | Asli     | Celikyilmaz, |       | Rahul      | Jha, Yejin |                                   |           |      |       |        |              |
|                 |          |              |       |            |            | moyer,andHannanehHajishirzi.2023. |           |      |       |        | FActScore:   |
| Choi, and       | Jianfeng | Gao.         | 2021. | Go figure: | A meta     |                                   |           |      |       |        |              |
Fine-grainedatomicevaluationoffactualprecision
| evaluationoffactualityinsummarization. |     |     |     |     | Preprint, |     |     |     |     |     |     |
| -------------------------------------- | --- | --- | --- | --- | --------- | --- | --- | --- | --- | --- | --- |
arXiv:2010.12834. inlongformtextgeneration. InProceedingsofthe
2023ConferenceonEmpiricalMethodsinNatural
ZorikGekhman,JonathanHerzig,RoeeAharoni,Chen Language Processing, pages 12076–12100, Singa-
pore.AssociationforComputationalLinguistics.
| Elkind,andIdanSzpektor.2023. |             |     |            | Trueteacher:Learn- |            |     |     |     |     |     |     |
| ---------------------------- | ----------- | --- | ---------- | ------------------ | ---------- | --- | --- | --- | --- | --- | --- |
| ing factual                  | consistency |     | evaluation | with               | large lan- |     |     |     |     |     |     |
NielsMündler,JingxuanHe,SlobodanJenko,andMar-
| guagemodels. |     | Preprint,arXiv:2305.11171. |     |     |     |                 |     |                                  |     |     |     |
| ------------ | --- | -------------------------- | --- | --- | --- | --------------- | --- | -------------------------------- | --- | --- | --- |
|              |     |                            |     |     |     | tinVechev.2024. |     | Self-contradictoryhallucinations |     |     |     |
OrHonovich, RoeeAharoni, JonathanHerzig, Hagai oflargelanguagemodels: Evaluation,detectionand
Taitelbaum,DoronKukliansy,VeredCohen,Thomas mitigation. Preprint,arXiv:2305.15852.
| Scialom,          | Idan | Szpektor, | Avinatan                 | Hassidim, | and |                 |     |         |        |             |         |
| ----------------- | ---- | --------- | ------------------------ | --------- | --- | --------------- | --- | ------- | ------ | ----------- | ------- |
|                   |      |           |                          |           |     | Shashi Narayan, |     | Shay B. | Cohen, | and Mirella | Lapata. |
| YossiMatias.2022. |      | True:     | Re-evaluatingfactualcon- |           |     |                 |     |         |        |             |         |
2018. Don’tgivemethedetails,justthesummary!
| sistencyevaluation. |     | Preprint,arXiv:2204.04991. |     |     |     |                     |               |                       |        |          |         |
| ------------------- | --- | -------------------------- | --- | --- | --- | ------------------- | ------------- | --------------------- | ------ | -------- | ------- |
|                     |     |                            |     |     |     | topic-aware         | convolutional |                       | neural | networks | for ex- |
|                     |     |                            |     |     |     | tremesummarization. |               | ArXiv,abs/1808.08745. |        |          |         |
XiangkunHu,DongyuRu,QipengGuo,LinQiu,and
| Zheng Zhang. |     | 2023. | Refchecker | for | fine-grained |               |         |              |     |        |         |
| ------------ | --- | ----- | ---------- | --- | ------------ | ------------- | ------- | ------------ | --- | ------ | ------- |
|              |     |       |            |     |              | Vipula Rawte, | Swagata | Chakraborty, |     | Agnibh | Pathak, |
hallucinationdetection. Anubhav Sarkar, S. M Towhidul Islam Tonmoy,
|     |     |     |     |     |     | Aman Chadha, |     | Amit | P. Sheth, | and | Amitava Das. |
| --- | --- | --- | --- | --- | --- | ------------ | --- | ---- | --------- | --- | ------------ |
LeiHuang,WeijiangYu,WeitaoMa,WeihongZhong,
2023. Thetroublingemergenceofhallucinationin
| Zhangyin | Feng, | Haotian | Wang, | Qianglong | Chen, |     |     |     |     |     |     |
| -------- | ----- | ------- | ----- | --------- | ----- | --- | --- | --- | --- | --- | --- |
largelanguagemodels–anextensivedefinition,quan-
WeihuaPeng,XiaochengFeng,BingQin,andTing
|              |                                    |     |                  |     |               | tification,       | and | prescriptive | remediations. |     | Preprint, |
| ------------ | ---------------------------------- | --- | ---------------- | --- | ------------- | ----------------- | --- | ------------ | ------------- | --- | --------- |
| Liu. 2023.   | A survey                           |     | on hallucination |     | in large lan- | arXiv:2310.04988. |     |              |               |     |           |
| guagemodels: | Principles,taxonomy,challenges,and |     |                  |     |               |                   |     |              |               |     |           |
openquestions. Preprint,arXiv:2311.05232. Reuters. 2023. Alphabet shares dive after google ai
chatbotbardflubsanswerinad.
WojciechKryscinski,BryanMcCann,CaimingXiong,
| and Richard | Socher. | 2020. |     | Evaluating | the factual |     |     |     |     |     |     |
| ----------- | ------- | ----- | --- | ---------- | ----------- | --- | --- | --- | --- | --- | --- |
AbigailSee,PeterJ.Liu,andChristopherD.Manning.
consistency of abstractive text summarization. In 2017. Gettothepoint: Summarizationwithpointer-
Proceedings of the 2020 Conference on Empirical generatornetworks. InProceedingsofthe55thAn-
MethodsinNaturalLanguageProcessing(EMNLP), nualMeetingoftheAssociationforComputational
pages9332–9346,Online.AssociationforComputa- Linguistics (Volume 1: Long Papers), pages 1073–
tionalLinguistics.
1083,Vancouver,Canada.AssociationforComputa-
tionalLinguistics.
WojciechKrys´cin´ski,BryanMcCann,CaimingXiong,
andRichardSocher.2019. Evaluatingthefactualcon- DerekTam,AnishaMascarenhas,ShiyueZhang,Sarah
sistencyofabstractivetextsummarization. Preprint, Kwan,MohitBansal,andColinRaffel.2023. Eval-
arXiv:1910.12840. uating the factual consistency of large language
15029

models through news summarization. Preprint, prompt in Figure 7. Note that we have truncated
arXiv:2211.08412.
theexamplesfromthepromptstosavespace.
LiyanTang,TanyaGoyal,AlexanderR.Fabbri,Philippe
|     |     |     |     |     |     |     | B ErrorTypeClassificationExamples |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --------------------------------- | --- | --- | --- | --- | --- |
Laban,JiachengXu,SemihYavuz,WojciechKrys´-
cin´ski,JustinF.Rousseau,andGregDurrett.2023.
SeeTable9forerrortypeexamples.
| Understandingfactualerrorsinsummarization: |     |     |     |     |           | Er- |                      |     |     |     |     |     |
| ------------------------------------------ | --- | --- | --- | --- | --------- | --- | -------------------- | --- | --- | --- | --- | --- |
| rors,summarizers,datasets,errordetectors.  |     |     |     |     | Preprint, |     |                      |     |     |     |     |     |
|                                            |     |     |     |     |           |     | C QualitativeExample |     |     |     |     |     |
arXiv:2205.12854.
|            |                 |     |                 |     |     |     | Weshowexample#1inTable10. |     |     |     | Notethatnews |     |
| ---------- | --------------- | --- | --------------- | --- | --- | --- | ------------------------- | --- | --- | --- | ------------ | --- |
| LiyanTang, | IgorShalyminov, |     | AmyWingmeiWong, |     |     |     |                           |     |     |     |              |     |
Jon Burnsky, Jake W. Vincent, Yu’an Yang, Siffi articleisthecontextinputdocument,andCohere
| Singh, | Song | Feng, Hwanjun | Song, | Hang | Su, | Lijia |     |     |     |     |     |     |
| ------ | ---- | ------------- | ----- | ---- | --- | ----- | --- | --- | --- | --- | --- | --- |
Commandoutputsummaryistheresponseunder
Sun,YiZhang,SaabMansour,andKathleenMcK-
|         |                  |           |            |                |     |     | evaluation.  | We  | show      | one claim | extracted | from      |
| ------- | ---------------- | --------- | ---------- | -------------- | --- | --- | ------------ | --- | --------- | --------- | --------- | --------- |
| eown.   | 2024.            | Tofueval: | Evaluating | hallucinations |     |     |              |     |           |           |           |           |
|         |                  |           |            |                |     |     | the response | for | analysis. | Note      | that      | the human |
| of llms | on topic-focused |           | dialogue   | summarization. |     |     |              |     |           |           |           |           |
Preprint,arXiv:2402.13249. annotated label for the claim is "Absent" since
|               |       |     |        |      |       |        | the news          | article | does     | not mention  | the | status of |
| ------------- | ----- | --- | ------ | ---- | ----- | ------ | ----------------- | ------- | -------- | ------------ | --- | --------- |
| Ars Technica. | 2024. | Air | canada | must | honor | refund |                   |         |          |              |     |           |
|               |       |     |        |      |       |        | "Chris Hadfield". |         | However, | HalluMeasure |     | W/o       |
policyinventedbyairline’schatbot.
|               |                                      |     |     |     |     |     | CoTmodellabelstheclaimas"Supported". |     |     |     |     | This |
| ------------- | ------------------------------------ | --- | --- | --- | --- | --- | ------------------------------------ | --- | --- | --- | --- | ---- |
| Vectara.2023. | Vectarahugheshallucinationevaluation |     |     |     |     |     |                                      |     |     |     |     |      |
couldbebecausethemodeldoesnotreasonprop-
model.
|     |     |     |     |     |     |     | erly when | generating |     | the class | label for | a claim. |
| --- | --- | --- | --- | --- | --- | --- | --------- | ---------- | --- | --------- | --------- | -------- |
Yuxia Wang, Minghan Wang, Muhammad Arslan WhenHalluMeasureisexecutedW/CoTprompt-
Manzoor, Fei Liu, Georgi Georgiev, Rocktim Jy- ing,theclaimiscorrectlylabeledas"Absent". In
| oti Das, | and      | Preslav Nakov. |        | 2024.      | Factuality | of  |           |         |       |             |               |          |
| -------- | -------- | -------------- | ------ | ---------- | ---------- | --- | --------- | ------- | ----- | ----------- | ------------- | -------- |
|          |          |                |        |            |            |     | addition, | we show | the   | explanation | automatically |          |
| large    | language | models         | in the | year 2024. | Preprint,  |     |           |         |       |             |               |          |
|          |          |                |        |            |            |     | generated | by our  | model | about       | why the       | claim is |
arXiv:2402.02420.
labeled"Absent".
| Miriam  | Wanner, | Seth Ebner, | Zhengping |        | Jiang, | Mark |     |     |     |     |     |     |
| ------- | ------- | ----------- | --------- | ------ | ------ | ---- | --- | --- | --- | --- | --- | --- |
| Dredze, | and     | Benjamin    | Van       | Durme. | 2024.  | A    |     |     |     |     |     |     |
arXivpreprint
closerlookatclaimdecomposition.
arXiv:2403.11903.
JasonWei,XuezhiWang,DaleSchuurmans,Maarten
Bosma,FeiXia,EdChi,QuocVLe,DennyZhou,
| etal.2022.                   | Chain-of-thoughtpromptingelicitsrea- |     |     |                  |     |     |     |     |     |     |     |     |
| ---------------------------- | ------------------------------------ | --- | --- | ---------------- | --- | --- | --- | --- | --- | --- | --- | --- |
| soninginlargelanguagemodels. |                                      |     |     | Advancesinneural |     |     |     |     |     |     |     |     |
informationprocessingsystems,35:24824–24837.
ZiweiXu,SanjayJain,andMohanKankanhalli.2024.
| Hallucinationisinevitable: |     |     | Aninnatelimitationof       |     |     |     |     |     |     |     |     |     |
| -------------------------- | --- | --- | -------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| largelanguagemodels.       |     |     | Preprint,arXiv:2401.11817. |     |     |     |     |     |     |     |     |     |
YuhengZha,YichiYang,RuichenLi,andZhitingHu.
| 2023.                             | AlignScore: | Evaluating |           | factual         | consistency  |     |     |     |     |     |     |     |
| --------------------------------- | ----------- | ---------- | --------- | --------------- | ------------ | --- | --- | --- | --- | --- | --- | --- |
| with a                            | unified     | alignment  | function. | In              | Proceedings  |     |     |     |     |     |     |     |
| of the                            | 61st Annual | Meeting    | of        | the Association |              | for |     |     |     |     |     |     |
| ComputationalLinguistics(Volume1: |             |            |           |                 | LongPapers), |     |     |     |     |     |     |     |
pages11328–11348,Toronto,Canada.Association
forComputationalLinguistics.
| Rongxin     | Zhu,       | Jianzhong | Qi,            | and Jey      | Han       | Lau. |     |     |     |     |     |     |
| ----------- | ---------- | --------- | -------------- | ------------ | --------- | ---- | --- | --- | --- | --- | --- | --- |
| 2023.       | Annotating | and       | detecting      | fine-grained |           | fac- |     |     |     |     |     |     |
| tual errors | for        | dialogue  | summarization. |              | Preprint, |      |     |     |     |     |     |     |
arXiv:2305.16548.
A Prompts
| Weshowthefollowingprompts: |     |     |     | claimextraction |     |     |     |     |     |     |     |     |
| -------------------------- | --- | --- | --- | --------------- | --- | --- | --- | --- | --- | --- | --- | --- |
inFigure3;claimclassificationwithoutCoT+all-
claims-evalinFigure4;withCoT+all-claims-eval
promptinFigure5;withoutCoT+one-claim-eval
| prompt | in Figure | 6; with | CoT | + one-claim-eval |     |     |     |     |     |     |     |     |
| ------ | --------- | ------- | --- | ---------------- | --- | --- | --- | --- | --- | --- | --- | --- |
15030

Errortype Examplecontext Exampleclaimwitherror
Number Thecompany’sdroneswillbegindeliveringprod- The company’s drone deliveries will begin in
uctsinSydneyinearly2014. 2013.
Entity NewZealandcompanyMartinJetpack... MartinJetpackisbasedinSydney.
FalseConcatenation Thecompanywillbelistedonthestockexchange Theproductwillbereleasedwithinthenextfew
withinthenextfewmonths....Theirproductwill months.
bereleasedearlynextyear.
AttributionFailure According to Cooper, drone technology is cur- Dronetechnologyisunder-regulated.
rentlyunder-regulated...
Overgeneralization Thisproductisdesignedwithteachersandstu- Thisproductdevelopsmathskills.
dentsofSTEMinmind...
ReasoningError WedependontheAtlasVrocket,whichcarries WerelyonRussia’sAtlasVrocket
manyofourmostimportantsatellitesandispow-
eredbytheRussian-madeRD-180rocketengine.
Hyperbole Thetechnologywillsignificantlyimprovedriver Thetechnologywillrevolutionizedriversafety.
safety.
Temporal Thecompanywillusedronestodeliverpackages. Thecompanyusesdrones.
Context-basedmean- ThepackageincludesaBluetoothsystemthatlets DJscaninstructtherobot.
ingerror usersturntheirRoombaintoaDJ.
Other [Contextcontainsnoinformationaboutthearmy ThearmypreviouslyunveiledtheAtlasrobot.
unveilingarobotcalledAtlas.]
Table9: Examplesofspecificsubtypesofhallucinations.
15031

Figure3: Claimextractorprompt.
15032

Figure4: ClaimclassifierpromptforwithoutCoT+all-claim-evalsetup.
15033

Figure5: ClaimclassifierpromptforwithCoT+all-claims-evalsetup.
15034

Figure6: ClaimclassifierpromptforwithoutCoT+one-claim-evalsetup.
15035

Figure7: ClaimclassifierpromptforwithCoT+one-claim-evalsetup.
15036

Context(NewsArticle):(CNN)ElonMuskhasbuilta$12billioncompanyinanendeavortopavethewaytoMarsforhumanity.HeinsiststhatMarsisa¨long-term
insurancepolicy¨for¨thelightofconsciousnessïnthefaceofclimatechange,extinctionevents,andourrecklessnesswithtechnology.Ontheotherhand,astronautChris
Hadfieldisskeptical:H¨umanityisnotgoingextinct,h¨etoldme.Headded:T¨here’snogreatcompellingreasontogo,apartfromcuriosity,andthat’snotgoingtobeenoughto
sustaintheimmensecostnecessarywiththetechnologythatexistsrightnow.B¨utIquestionourfuture,stuckhereonEarth.Ourenvironmentisahighlybalancedsystemand
wearethedestabilizingelement.Pursuingg¨reenïnitiativesisnolong-termsolutiontothewallwe’rehurtlingtowards,they’respeedbumps.Ifthisiswherehumankindis
destinedtoremain,thenweshallfindourselvesfightingoverwhateverisleftofit.Politicallyspeaking,sendinghumansintospacebringsnationstogether–theInternational
SpaceStationstoodasthephysicalmanifestationofthereunificationoftheUSAandRussiaandisnowaplatformforbroaderinternationalcooperation.Spaceexploration
isalsoinspiring:duringNASA’sApolloprogramtotheMoon,thenumberofgraduatesinmathematics,engineeringandthesciencesintheUSdoubled.Ignitingthe
imaginationofthatgenerationhelpedpropeltheUSintothedominantpositionit’sheldsincethe1960s.WhatcouldaMarsprogramdo?Wouldn’ttheMoon,somuch
nearerthanMars,beabetterfirststep?Actually,no–it’sjusttoodifferent.It’sbettertotesthardwareandtrainpeopleinanalogsonEarth,suchasthegeologicallysimilar
high-altitudedesertinUtahorthecoldanddryCanadianArcticdesert.WhytheEuropeanSpaceAgencyhasdeclaredtheMoonastepping-stonetoMarsisbeyondme,as
doingsoincreasesthecostofaMarsprogramhugely.Ittakesabout50%moreenergytoputsomethingonthesurfaceoftheMoonthanitdoesonMars.TheMartian
atmospherecanbeusedtoslowdownapproachingspacecraft,insteadoftheneedforextrafueltoslowthedescent.Itwouldalsomeandevelopingtwodifferentsetsof
landingtechniquesandhardware.TherearereasonstogototheMoon,justnotifyourultimatedestinationisMars.EvencolonizingtheMoonisquestionable:itsimply
hasn’ttheresourcestosustainanadvancedcolony.Marshasfertilesoil,anabundanceofwater(asice),acarbon-dioxiderichatmosphereanda24-and-a-halfhourday.The
Moon’ssoilisnotfertile,waterisasrare,ithasnoeffectiveatmosphere,anda708-hourday.It’sfeasibletointroducebiologicallifetoMars,butnottheMoon.Withonlya
relativelysmallpush,Marscouldbereturnedtoitsformerwarm,wet,hospitablestate.RaisingthetemperatureatthesouthpolebyafewdegreeswouldseefrozenCO2in
thesoilbegintogasify.Asagreenhousegas,itwouldfurtherraisethetemperature,gasifyingmoreCO2inaself-sustainedglobal-warmingprocess.Eventually,waterfrozen
intothesoilwouldliquefy,coveringhalfoftheplanet.Afteraboutacentury,MarswouldsettledownwithanatmosphereaboutasdenseasthelowlandHimalayasanda
climatesuitableforT-shirts.Hadfieldwarnsthatw¨eneedtoinventalotofthingsb¨eforegoingtoMars,andthat¨there’snogreatadvantagetobeingtheearlyexplorerswho
die¨.Fewwoulddisagreewiththat,butwhatarethechallengesacrewedmissiontoMarsfaces?Radiation:Anastronautwouldreceivealifetimeallowabledoseofradiation
inasingle30-monthround-trip,including18monthsonthesurface.Butthisisonlyequivalenttoincreasingthelifetimecancerriskfromabout20%to23%.Asthemajority
ofthisisreceivedintransitbetweenplanets,withproperradiologicalprotectionontheship,itwouldactuallybe(radiologicallyspeaking)healthierforanastronauttoliveon
Marswitharadiationdoseof0.10sievertsperyearthantosmokeonEarthat0.16sievertsperyear.Thereisnosinglepracticalsolutiontotheradiationproblem.One
strategyIhelpeddevelopwastooptimisetheinternallayoutoftheequipmentandstructuresintheMarshabitatmoduletominimiseexposure–placingexistingbulkinall
therightplaces.Thisreducedexposurebyabout20%,withoutaddinganymass.Eventakingemptysandbags,packingthemwithMartiansoilandputtingthemontheroof
wouldbeasimpleandeffectivemeasureonMars.Radiationisanissuetotackle,butit’snotadeal-breaker.Power:W¨eneedacompactenergysource,s¨aysHadfield.W¨e
cannotberelyingonthetinybitofsolarpowerthathappenstoarriveatthatlocation.W¨hilethesolarenergyreachingthesurfaceofMarsisabouthalfthatonEarth,this
isn’tashow-stopper.Aquickback-of-the-envelopecalculationshowsthattopowertheequivalentofanaverageU.S.householdonMars,eventhroughduststorms,one
wouldneedanarrayofsolarpanelstotallingsixmetressquare–veryachievable.Reducedgravity:Theeffectsofmicrogravityonastronauts’healthhavebeenstudiedfor
decades,andarangeoftechniqueshavebeendevelopedtomitigatethewastingeffectsonmuscleandbone.WithMartiangravityaroundathirdofthatonEarth,itwould
takeastronautsacoupleofdaystoacclimatize,andperhapsafewmonthstofullyadapt.NASAandESAhavebeendevelopinganunder-suitthatcompressesthebody
toovercomethenegativeeffectsofareductioninpressureandgravity.However,biologicaladaptioncouldbemadeeasierifmicrogravitywereavoidedaltogether.The
spacecraftcouldbespunin-transittogenerateanartificialgravitythatslowlydecayed,simulatingatransitionfromEarthtoMarsgravity(andviceversa)overthesix-month
journey.Ultimately,untilhumansareactuallylivingonotherplanetsit’sunlikelywe’llsolveorevenrecogniseallthesubtlelong-termhealthproblemsassociatedwith
reducedgravity.Andwho’stosaywhattheadvancesinbio-engineeringandtechnologywillmakethehumanbodycapableofwhenthattimecomes?LifeonMars:Ifthere’s
lifeonMars,evenifit’smicrobial,shouldwebeallowedtospreadtotheplanet,potentiallyriskingitsextinction?Ifindthisquestionstrange–asChrisMcKayputit:W¨e
commitmicrobialgenocideeverytimewewashourhands¨.Weengineerandfarmthecomplexlifearoundusassystematicallyandascheaplyaspossible.Billionsofpeople
eatthecarcassesoforganismsthatwerethinkingandbreathingonlydaysbefore.Why,allofasudden,shouldMartianmicrobesbegivensuchsanctity?Itshouldcertainlybe
studied,butitshouldn’tpreventourspreading.Backcontamination:Conversely,thequestionofwhethersomeMartianplaguemightaccidentallybeintroducedtoEarth
shouldbetakenseriously–butnotblownoutofproportion.There’sonlyaremotechancethatMartianlifemightbehazardous.Thethingsthatkillusdosobecausethey’ve
evolvedinlock-stepwithusinacontinualevolutionaryarmsrace.AnyMartianlifewillhaveevolvedindependentlyandisunlikelytobecapableevenofinteractingwith
Earthlifeonamolecularlevel.AsRobertZubrinputit:T¨reesdon’tgetcoldsandhumansdon’tgetDutchElmDisease.P¨sychology:Dependingonrelativeorbits,sendinga
messagebetweenEarthandMarscantakebetweenthreeand22minutes.Thislossofreal-timecommunicationwillleaveastronautsfeelingcut-offandalone.Hadfieldsays
thatit’svitaltokeepupcrewmoraleandmotivation:Önceyougetanydistanceawayonanysortofvoyage,theepic-nessdisappears,therealitybecomestheforeground,and
theapplauseislonggone.C¨ost:AcrewedMarsprogramwouldcosttheequivalentofafewweeksoftheU.S.defensebudget.TheUSplansonspendingabout10timesmore
onnuclearweaponsthanonspaceexplorationoverthecomingdecade.TheUKgovernmentspendsaboutasmuchongastricbandsurgerythroughtheNHSasitdoesonits
spaceactivities.SowhileaMarsprogramcertainlyhaschallengestoovercome,thetechnologicalgapbetweenusandMarsisfarsmallerthanitwasfortheMoonprogramin
the1960s.AndtheprospectstheRedPlanetholdsforhumanityarefargreater.Copyright2015TheConversation.Somerightsreserved."
Response(CohereSummary):TheConversationarticlepresentsanargumentinfavorofpursuingspaceexploration,specificallyamannedmissiontoMars.Itexplainsthat
whileChrisHadfield,aretiredastronaut,isskepticalaboutthenecessityofsuchanendeavor,theauthorbelievesthatitisimperativeforhumanitytoexplorespace.The
authorpointsoutthatEarth’senvironmentisdelicatelybalancedandthathumanactivityhasthepotentialtodisruptitsignificantly.Therefore,humansshouldlooktoexpand
theirpresencebeyondEarthinordertoensuretheirlong-termsurvival.Inaddition,thearticleaddressescommonconcernsandchallengesofaMarsmission,suchasthehigh
cost,potentialdangers,andlackofpracticalbenefits.However,itarguesthatthesechallengesarenotinsurmountable,andthatthebenefitsofexploringMarsareimmense.
Ultimately,theauthorconcludesthatwhileMarsmayseemlikeadistantandimpracticalgoal,itisaworthwhileendeavorthathasthepotentialtopropelhumanityintoanew
eraofinnovationandprogress.
HalluMeasureExtractedClaim:ChrisHadfieldisaretiredastronaut.
HumanAnnotatedLabel:Absent
HalluMeasureW/oCoTLabel:Supported
HalluMeasureW/CoTLabel:Absent
HalluMeasureW/CoTLabelExplanation:ThesourcetextreferstoChrisHadfieldasanastronautandquoteshimdirectly,butdoesnotexplicitlystatewhetherheis
currentlyactiveorretired.
Table 10: Sample Result: HalluMeasure W/ and W/o CoT comparison on a claim from news article context
documentinTechNewsSummdataset.
15037