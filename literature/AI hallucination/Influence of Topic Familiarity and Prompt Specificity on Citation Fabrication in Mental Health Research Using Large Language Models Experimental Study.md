JMIR MENTAL HEALTH Linardon et al
Original Paper
Influence of Topic Familiarity and Prompt Specificity on Citation
Fabrication in Mental Health Research Using Large Language
Models: Experimental Study
Jake Linardon, PhD; Hannah K Jarman, PhD; Zoe McClure, PhD; Cleo Anderson, BA; Claudia Liu, BA; Mariel
Messer, PhD
School of Psychology, Faculty of Health, Deakin University, Geelong, Victoria, Australia
Corresponding Author:
Jake Linardon, PhD
School of Psychology
Faculty of Health
Deakin University
75 Pigdons Road Waurn Ponds
Geelong, Victoria, 3216
Australia
Phone: 61 3 924 46308
Email: jake.linardon@deakin.edu.au
Abstract
Background: Mental health researchers are increasingly using large language models (LLMs) to improve efficiency, yet these
tools can generate fabricated but plausible-sounding content (hallucinations). A notable form of hallucination involves fabricated
bibliographic citations that cannot be traced to real publications. Although previous studies have explored citation fabrication
across disciplines, it remains unclear whether citation accuracy in LLM output systematically varies across topics within the same
field that differ in public visibility, scientific maturity, and specialization.
Objective: This study aims to examine the frequency and nature of citation fabrication and bibliographic errors in GPT-4o
(Omni) outputs when generating literature reviews on mental health topics that varied in public familiarity and scientific maturity.
We also tested whether prompt specificity (general vs specialized) influenced fabrication or accuracy rates.
Methods: In June 2025, GPT-4o was prompted to generate 6 literature reviews (~2000 words; ≥20 citations) on 3 disorders
representing different levels of public awareness and research coverage: major depressive disorder (high), binge eating disorder
(moderate), and body dysmorphic disorder (low). Each disorder was reviewed at 2 levels of specificity: a general overview
(symptoms, impacts, and treatments) and a specialized review (evidence for digital interventions). All citations were extracted
(N=176) and systematically verified using Google Scholar, Scopus, PubMed, WorldCat, and publisher databases. Citations were
classified as fabricated (no identifiable source), real with errors, or fully accurate. Fabrication and accuracy rates were compared
by disorder and review type by using chi-square tests.
Results: Across the 6 reviews, GPT-4o generated 176 citations; 35 (19.9%) were fabricated. Among the 141 real citations, 64
(45.4%) contained errors, most frequently incorrect or invalid digital object identifiers. Fabrication rates differed significantly
by disorder (χ2 =13.7; P=.001), with higher rates for binge eating disorder (17/60, 28%) and body dysmorphic disorder (14/48,
2
29%) than for major depressive disorder (4/68, 6%). While fabrication did not differ overall by review type, stratified analyses
showed higher fabrication for specialized versus general reviews of binge eating disorder (11/24, 46% vs 6/36, 17%; P=.01).
Accuracy rates also varied by disorder (χ2 =11.6; P=.003), being lowest for body dysmorphic disorder (20/34, 59%) and highest
2
for major depressive disorder (41/64, 64%). Accuracy rates differed by review type within some disorders, including higher
accuracy for general reviews of major depressive disorder (26/34, 77% vs 15/30, 50%; P=.03).
Conclusions: Citation fabrication and bibliographic errors remain common in GPT-4o outputs, with nearly two-thirds of citations
being fabricated or inaccurate. Reliability systematically varied by disorder familiarity and prompt specificity, with greater risks
in less visible or specialized mental health topics. These findings highlight the need for careful prompt design, rigorous human
verification of all model-generated references, and stronger journal and institutional safeguards to protect research integrity as
LLMs are integrated into academic practice.
https://mental.jmir.org/2025/1/e80371 JMIR Ment Health 2025 | vol. 12 | e80371 | p. 1
XSL FO (page number not for citation purposes)
•
RenderX

JMIR MENTAL HEALTH Linardon et al
(JMIR Ment Health 2025;12:e80371) doi: 10.2196/80371
KEYWORDS
large language models; artificial intelligence; AI; mental health; psychiatry; citations; academic research
They found that while there were no differences in fabricated
Introduction
citation rates between the 2 disciplines (27.3% vs 23.4%), the
rate of digital object identifier (DOI) hallucinations among the
Researchers today face growing pressure to maintain high levels
generated citations was higher for humanities (89.4%) than for
of productivity to remain competitive for funding, tenure-track
natural sciences (61.8%) [8]. In another study, McGowan et al
positions, academic promotions, and international recognition
[9] used Google’s Bard (now Gemini) to assess citation accuracy
in their fields [1]. This intensifying demand for outputs—which
when prompted to generate references for research topics that
typically spans research, teaching, supervision, and service—has
were broad (ie, evidence for hallucinations in schizophrenia)
led to a need for innovative solutions that can streamline
versus specific (ie, research using natural language processing
administrative and research-related workflows. As the academic
to assess suicidal behavior) in nature. When prompted on the
workload becomes increasingly complex and resource
broader topic, none of the 10 citations generated by Bard were
constrained, tools that can support efficiency without
accurate, with several linking to entirely unrelated papers. In
compromising quality are gaining significant attention.
contrast, when prompted on the specific topic, all 5 citations
Large language models (LLMs) are a class of tools gaining contained misattributed authorship but linked to real papers
traction in academic settings to support researchers. LLMs are with matching titles [9]. These findings collectively demonstrate
advanced artificial intelligence systems trained on vast amounts that both the disciplinary domain and the specificity of the
of textual data to generate coherent and contextually relevant prompt can influence the likelihood and nature of citation
natural language responses [2]. Among the many LLMs hallucinations, highlighting the need for systematic evaluations
available, ChatGPT (OpenAI) has emerged as the most widely of LLM citation reliability across varied research contexts.
used, both in the general population [3] and among researchers
In this study, we provide a more nuanced examination of citation
[4,5]. A recent study showed that nearly 70% of mental health
fabrication in the most recent version of GPT (GPT-4o; Omni)
scientists reported using ChatGPT to assist with research-related
outputs by systematically varying the level of public awareness
tasks, including writing and drafting, coding, and administrative
and depth of existing scientific literature on the topic within the
support [4]. However, while most LLM adopters reported that
domain of mental health. In particular, we prompted GPT-4o
these tools enhanced research efficiency and improved the
to generate academic literature reviews for 3 distinct mental
quality of their work, many also expressed concerns about
disorders that differ in public visibility and research maturity.
inaccuracies, misleading content, and biases in the responses
We selected major depressive disorder, binge eating disorder,
generated by these models [4]. These concerns are not
and body dysmorphic disorder because they reflect varying
unfounded, as one of the most well-documented limitations of
levels of clinical familiarity and scientific development within
LLMs is their tendency to “hallucinate,” which occurs when
the mental health field. Major depressive disorder is widely
the model generates false, fabricated, or unverifiable information
studied and publicly recognized, with a substantial volume of
that appears coherent and credible [6].
research and clinical trial activity. Binge eating disorder
One type of hallucination generated by LLMs that has received occupies an intermediate position in terms of research output
increasing attention among researchers is fabricated and public awareness, whereas body dysmorphic disorder
bibliographic citations that cannot be traced to existing scholarly remains comparatively understudied and less widely known
publications. This is a critical issue reported in LLM output [10]. These classifications are supported by differences in
because citations serve as the foundation of scholarly publication volume, clinical trial prevalence, and general
communication—they guide readers to source evidence; build population familiarity across the 3 disorders. We also varied
cumulative knowledge; and inform research, policy, and clinical the level of prompt specificity, asking GPT-4o to generate either
practice. Fabricated references can mislead readers, distort a general overview of each disorder (including its symptoms,
scientific understanding, and compromise the integrity of societal impacts, and treatment approaches) or a specialized
academic work. review focused on the narrower topic (the evidence base for
digitally delivered interventions).
Recent work has sought to quantify the extent of these
hallucinations, typically by analyzing the citations produced Given that LLMs are trained on large-scale text corpora
when LLMs are prompted to generate academic literature comprising publicly available and licensed content [2], it is
reviews on specific topics. Walters and Wilder [7] prompted plausible that topics with lower online visibility, limited research
GPT-3.5 and GPT-4 to generate short literature reviews on 42 coverage, or highly specialized scope are more prone to
multidisciplinary topics and found that 55% and 18% of the citation-related hallucinations. This may be because such topics
citations, respectively, were fabricated, and 43% (GPT-3.5) and are underrepresented in the training data and often lack readily
24% (GPT-4) of the real citations contained substantive errors. accessible, high-quality academic content in the public domain,
Mugaanyi et al [8] compared citation fabrication rates in thereby reducing the model’s ability to retrieve accurate and
GPT-3.5–generated literature reviews across disciplines by verifiable sources. The novelty of this study is that it goes
analyzing 5 reviews each in the natural sciences and humanities. beyond previous cross-disciplinary examinations of citation
https://mental.jmir.org/2025/1/e80371 JMIR Ment Health 2025 | vol. 12 | e80371 | p. 2
XSL FO (page number not for citation purposes)
•
RenderX

JMIR MENTAL HEALTH Linardon et al
hallucinations to provide the first within-domain test of how not implemented, as our study sought to assess citation reliability
topic familiarity and prompt specificity shape LLM reliability. under straightforward prompting conditions that approximate
By manipulating both the disorder under review and the typical researcher use.
granularity of the task, we were able to generate new insights
We asked GPT-4o to simulate an academic researcher and write
into when and why citation hallucinations are more likely to
a literature review of approximately 2000 words, using at least
occur in scientific contexts. Therefore, we aimed to examine
20 citations from peer-reviewed academic sources, preferably
whether citation fabrication and bibliographic accuracy in
within the last 10 years. Two major prompts were used, 1
GPT-4o outputs systematically vary by disorder type and review
generic and 1 specialized, and were held constant across reviews,
specificity.
with only the target disorder substituted in the text. Prompts,
outputs, and citations generated by GPT-4o are presented in
Methods
Multimedia Appendix 1.
Design Data Collection and Analysis
We used GPT-4o to generate brief literature reviews on 6 For the 6 literature reviews generated by GPT-4o, we recorded
different topics and then aggregated data on the citations the number of words generated, number of citations provided,
generated in the papers. We then searched online databases and frequency of sources provided (eg, journal articles and books),
websites to examine the frequency of (1) fabricated citations, and the full bibliographic information. For each citation, we
(2) errors in the citations of nonfabricated sources, and (3) first searched Google Scholar to see whether it was real or
completely accurate citations among the nonfabricated sources. fabricated. If no matching source was found, we then searched
Multimedia Appendix 1 presents the prompts given for the 6 using the full author list to identify any resembling publications.
review topics, the text generated by GPT-4o, and the full If this was also unsuccessful, we searched using the full title of
citations provided in the output. the citation. If the citation still could not be verified, we repeated
the process across other databases, including Google, Scopus,
Review Topics and Prompts
PubMed, and WorldCat. As a final step in verifying potentially
GPT-4o was tasked (June 2025) with generating a short literature
fabricated works, we manually reviewed the relevant journal
review on 6 distinct topics. For each prompt, a new session was
volume and issue and used the publisher’s website search
initiated, and chat history was cleared to eliminate any influence
function to confirm that the cited work did not exist.
from previous interactions. The topics spanned 3 different
mental disorders that varied in public knowledge, volume of We considered a citation to be genuine (not fabricated) if we
scientific research, and the level of specificity of the research could identify a real publication that closely matched both the
questions provided to GPT-4o. For the general overview, title and the authors. In other words, inaccuracies in the citation
GPT-4o was asked to write about the causes, societal and were permitted if the cited work could be reliably traced to an
economic impacts, and available treatment approaches for 1 of actual source. For example, a GPT-4o citation that listed the
the 3 disorders (major depressive disorder vs binge eating correct authors and title but included an incorrect volume
disorder vs body dysmorphic disorder). For the specialized number, page range, or DOI was still considered a real
reviews, GPT-4o was asked to synthesize the evidence base for (nonfabricated) source. For these nonfabricated sources, we
digital interventions and discuss the factors that may influence then compared the GPT-4o citation to the actual citation and
their effectiveness. We selected digital interventions as the recorded whether there were any discrepancies and errors in the
specialized topic because all 3 disorders have a growing yet author list, year, title, journal, volume, issue, page range, and
uneven body of research in this area, making it a suitable test DOI. This did not include formatting errors (eg, italicized journal
case for examining GPT-4o’s ability to retrieve and summarize names). We then recorded the number of GPT-4o real
nuanced evidence across conditions that differ in research (nonfabricated) citations that contained no errors in any of the
maturity. For example, more than 100 clinical trials have bibliographic details.
evaluated digital interventions for depression [11] compared to
Fabrication and accuracy rates were calculated as proportions
approximately a dozen for binge eating disorder [12] and an
and expressed as percentages. These rates were presented
even smaller number for body dysmorphic disorder [13].
descriptively overall and separately by target disorder (major
Prompt development was guided by 2 principles: replicability depressive disorder vs binge eating disorder vs body dysmorphic
and ecological validity. First, we closely mirrored the style of disorder) and review type (general vs specialized).
prompts used in previous studies of LLM-generated literature
To examine whether fabrication and accuracy rates varied by
reviews in other disciplines [7]. Second, we sought to design
disorder and review type, we conducted a series of chi-square
prompts that reflected how researchers might realistically request
tests. Specifically, we tested for main effects by evaluating the
literature reviews from an LLM in practice. Draft prompts were
association between review type and fabrication and accuracy
discussed extensively among all authors and revised to ensure
rates and between disorder and fabrication and accuracy rates
consistency, neutrality of tone, and appropriateness for the study
across all reviews.
aims. Importantly, we did not test these prompts within GPT-4o
during development to avoid introducing previous knowledge Although interaction effects were not formally modeled because
or contamination from earlier runs. While advanced prompt of low expected cell counts in some conditions, we conducted
engineering strategies (eg, chain of thought, few-shot examples, stratified chi-square tests to explore potential group differences
and retrieval-augmented prompts) were considered, these were within each level of the independent variables, that is, we
https://mental.jmir.org/2025/1/e80371 JMIR Ment Health 2025 | vol. 12 | e80371 | p. 3
XSL FO (page number not for citation purposes)
•
RenderX

| JMIR MENTAL HEALTH |     |     |     |     |     |     |     | Linardon et al |
| ------------------ | --- | --- | --- | --- | --- | --- | --- | -------------- |
examined whether review type (general vs specialized) was
Results
associated with fabrication or accuracy rates within each of the
3 diagnostic subgroups and whether diagnostic subgroup was
Overview
associated with fabrication or accuracy rates within each review
The number of words generated by GPT-4o across the 6
type.
literature reviews ranged from 1096 (specialized review for
All chi-square tests were 2 tailed, and pairwise comparisons
binge eating disorder) to 1326 (general review for binge eating
were  conducted  where  omnibus  tests  were  significant. disorder). The total number of references provided by GPT-4o
Significance was set at P<.05.
was 176, which ranged from 17 (specialized review for body
dysmorphic disorder) to 36 (generic review for binge eating
Ethical Considerations
disorder) across the 6 conditions (Table 1). Most citations
This study was exempt from ethical review as no human
provided by GPT-4o were journal articles, with books and book
participants were involved. chapters comprising the rest. Multimedia Appendix 2provides
the citations provided by GPT-4o, along with the correct citation
identified by the author team.
Table 1. Prevalence of fabricated and accurate citations generated by ChatGPT-4o overall and by literature review and diagnostic subtype.
Variable Major depressive disorder, Binge eating disorder, n/N Body dysmorphic disorder, Combined references, n/N (%)
|     | n/N (%) |     | (%) |     | n/N (%) |     |     |     |
| --- | ------- | --- | --- | --- | ------- | --- | --- | --- |
General Specialized General Specialized General Specialized General Specialized Total
(n=35 refer- (n=33 refer- (n=36 refer- (n=24 refer- (n=31 refer- (17 refer- (n=102) (n=74) (N=176)
|     | ences; 1302 | ences; 1146 | ences; 1326 | ences; 1096 | ences; 1225 | ences; 1239 |     |     |
| --- | ----------- | ----------- | ----------- | ----------- | ----------- | ----------- | --- | --- |
|     | words)      | words)      | words)      | words)      | words)      | words)      |     |     |
Fabricated refer- 1/35 (2.9) 3/33 (9.1) 6/36 (16.7) 11/24 (45.8) 10/31 (32.3) 4/17 (23.5) 17/102 18/74 (24.3) 35/176
| ences |     |     |     |     |     |     | (16.7) | (19.9) |
| ----- | --- | --- | --- | --- | --- | --- | ------ | ------ |
Accurate refer- 26/34 (76.5) 15/30 (50) 18/30 (60) 8/13 (61.5) 3/21 (14.3) 7/13 (53.8) 47/85 30/56 (53.3) 77/141
| encesa |     |     |     |     |     |     | (55.3) | (54.6) |
| ------ | --- | --- | --- | --- | --- | --- | ------ | ------ |
Error typeb
Author list 3/34 (8.8) 5/30 (16.7) 3/30 (10) 0 (0) 5/21 (23.8) 5/13 (38.5) 11/85 10/56 (17.9) 21/141
|     |     |     |     |     |     |     | (12.9) | (14.9) |
| --- | --- | --- | --- | --- | --- | --- | ------ | ------ |
Year 5/34 (14.7) 7/30 (23.3) 9/30 (30) 3/13 (23.1) 5/21 (23.8) 4/13 (30.8) 19/85 14/56 (25) 33/141
|     |     |     |     |     |     |     | (22.4) | (23.4) |
| --- | --- | --- | --- | --- | --- | --- | ------ | ------ |
Title 0 (0) 4/30 (13.3) 5/30 (16.7) 1/13 (7.7) 9/21 (42.9) 3/13 (23.1) 14/85 8/56 (14.3) 22/141
|     |     |     |     |     |     |     | (16.5) | (15.6) |
| --- | --- | --- | --- | --- | --- | --- | ------ | ------ |
Journal 0 (0) 7/30 (23.3) 3/28 (10.7) 0/0 (0) 8/18 (44.4) 2/11 (18.2) 11/79 9 /53 (17) 20/132
|     |     |     |     |     |     |     | (13.9) | (15.2) |
| --- | --- | --- | --- | --- | --- | --- | ------ | ------ |
Volume 4/33 (12.1) 10 /30 (33.3) 7/27 (25.9) 3/12 (25) 12/18 (66.7) 3/10 (30) 23/78 16 (30.8) 39/130
|     |     |     |     |     |     |     | (29.2) | (30) |
| --- | --- | --- | --- | --- | --- | --- | ------ | ---- |
Issue 4/32 (12.5) 9/30 (30) 7/27 (25.9) 3/12 (25) 10/18 (55.6) 3/10 (30) 21/77 15/52 (28.8) 36/129
|     |     |     |     |     |     |     | (27.3) | (27.9) |
| --- | --- | --- | --- | --- | --- | --- | ------ | ------ |
Page 5/33 (15.2) 9/30 (30) 7/27 (25.9) 3/12 (25) 11/18 (61.1) 4/11 (36.4) 23/78 16/52 (30.2) 39/131
|     |     |     |     |     |     |     | (29.5) | (29.8) |
| --- | --- | --- | --- | --- | --- | --- | ------ | ------ |
DOIc 6/33 (18.2) 11/30 (37.7) 9/28 (32.1) 5/13 (38.5) 14/19 (73.7) 6/12 (50) 29/80 22/55 (40) 51/135
|     |     |     |     |     |     |     | (36.3) | (37.8) |
| --- | --- | --- | --- | --- | --- | --- | ------ | ------ |
Journal article 34/35 (97.1) 33/33 (100) 33/ 36 (91.7) 23/24 (95.8) 27/31 (87.1) 15/17 (88.2) 94/102 71/74 (95.6) 165/176
|     |     |     |     |     |     |     | (92.2) | (93.8) |
| --- | --- | --- | --- | --- | --- | --- | ------ | ------ |
aPercentage derived for accurate references does not factor in hallucinated references in the denominator. Denominator varies based on whether
information was provided in the citation generated by ChatGPT (eg, missing volume number for one citation was not included in the denominator for
accuracy rate for overall volume numbers).
bError type was only relevant for actual references. Sources that did not include specific information to form an American Psychological Association
reference (eg, volume, issue, journal, and page number for books) were counted as missing and did not contribute to the denominator.
cDOI: digital object identifier.
https://mental.jmir.org/2025/1/e80371 JMIR Ment Health 2025 | vol. 12 | e80371 | p. 4
(page number not for citation purposes)
XSL FO
•
RenderX

JMIR MENTAL HEALTH Linardon et al
Fabrication Rates eating disorder (P=.71). When conducting stratified analyses
by review type, significant overall differences in accuracy rates
Of the 176 citations provided by GPT-4o, 35 (19.9%) were
between diagnostic subtypes emerged only for generic reviews
fabricated. When GPT-4o provided a DOI for a fabricated
(P<.001). Specifically, accuracy rates within generic reviews
citation, 64% (21/33) of the DOIs were valid but linked to
were significantly lower for body dysmorphic disorder compared
irrelevant and unrelated journal articles, whereas 36% (12/33)
to both major depressive disorder (P<.001) and binge eating
were completely invalid or nonfunctional.
disorder (P=.001).
The number of fabricated sources overall did not significantly
Citation Errors
differ between general (17/102, 16.7%) and specialized (18/74,
24%) literature reviews (χ2 =1.6; P=.21). However, when Table 1also provides the percentage of specific errors observed
1
across real (nonfabricated) citations overall and by condition.
conducting stratified analyses by diagnostic subgroup, a
Combined, the highest error rate was observed for DOIs for
significant association between literature review type and
journal articles (51/141, 36.2%), and the lowest error rate was
fabrication rate emerged only for binge eating disorder:
observed for the author list (21/141, 14.9%). Similar trends
fabrication rate was significantly higher for specialized (11/24,
were observed when inspecting error rates across the 6 study
46%) compared to generic (6/36, 17%) reviews on binge eating
conditions (Table 1).
disorder produced by GPT-4o (P=.01).
When comparing the number of fabricated sources overall Discussion
between the 3 diagnostic subtypes, a significant overall
difference was observed (major depressive disorder: 4/68, 6%; Principal Findings
binge eating disorder: 17/60, 28%; body dysmorphic disorder:
This study examined whether citation fabrication and
14/48, 29%; χ2 =13.7; P=.001). Pairwise comparisons show bibliographic accuracy in GPT-4o output systematically vary
2
that the fabrication rate was significantly higher for binge eating across topic areas of different public visibility, scientific
disorder compared to major depressive disorder (P=.001) and development, and specialization. We prompted GPT-4o to
for body dysmorphic disorder compared to major depressive generate literature reviews on 3 psychiatric conditions (ie, major
disorder (P=.001), but no difference emerged when comparing depressive disorder, binge eating disorder, and body dysmorphic
binge eating disorder to body dysmorphic disorder (P=.92). disorder) that vary in public knowledge and research maturity.
When conducting stratified analyses by review type, significant The literature reviews generated by GPT-4o also varied in scope,
differences in fabrication rates were found between the 3 comprising both general overviews of each disorder (including
diagnostic subtypes for both general (P=.006) and specialized symptoms, impacts, and treatment approaches) and highly
(P=.006) reviews. Within generic reviews, fabrication rates specific reviews focused on the efficacy and moderators of
were significantly lower for major depressive disorder than for digitally delivered interventions for these disorders. Given that
body dysmorphic disorder (P=.001). Within specialized reviews, LLMs are trained on large-scale text corpora comprising
fabrication rates were significantly higher for binge eating publicly available content [2], we expected that literature
disorder than for major depressive disorder (P<.001). reviews focused on more widely recognized disorders (ie, major
depressive disorder) and those addressing general topics would
Accuracy Rates
yield lower rates of citation fabrication and bibliographic errors
Only 77 (54.6%) of the 141 real (nonfabricated) citations compared to reviews on less familiar disorders or more
provided by GPT-4o were accurate and contained no errors. specialized subfields.
The number of accurate citations overall did not significantly
Our expectations were mostly supported. Overall, GPT-4o
differ between general (47/85, 55%) and specialized (30/56,
generated 176 citations from 6 literature reviews. A total of 35
54%) literature reviews (χ2 =0.4; P=.84). However, when
1 (19.9%) citations were fabricated, and among the 141
conducting stratified analyses by diagnostic subtype, differences
nonfabricated citations, 77 (54.6%) contained bibliographic
in accuracy rates between review types did emerge. Within
errors, with incorrect DOIs being the most prevalent error type.
major depressive disorder, accuracy was significantly higher
Fabrication and accuracy rates varied by disorder, with the
for generic (26/34, 77%) compared to specialized (15/30, 50%)
lowest fabrication rates observed in reviews on major depressive
reviews (P=.03), whereas within body dysmorphic disorder,
disorder and the lowest citation accuracy rates found in reviews
accuracy was significantly higher for specialized (7/13, 54%)
on body dysmorphic disorder. While citation fabrication and
compared to generic (3/21, 14%) reviews (P=.01).
accuracy rates did not differ overall by review type, stratified
When comparing accuracy rates overall between the 3 diagnostic analyses revealed important within-disorder differences. First,
subtypes, a significant overall difference was observed (major fabrication rates were higher in specialized than general reviews
depressive disorder: 41/64, 64%; binge eating disorder: 26/43, within binge eating disorder. Second, citation accuracy was
60%; body dysmorphic disorder: 10/34, 29%; χ2 =11.6; higher for general than specialized reviews within major
2 depressive disorder. Third, accuracy was unexpectedly higher
P=.003). Pairwise comparisons show rates of accurate citations
in specialized than general reviews within body dysmorphic
were significantly higher for major depressive disorder
disorder. Collectively, these findings demonstrate that both the
compared to body dysmorphic disorder (P=.001) and for binge
subject area and prompt granularity can influence the likelihood
eating disorder compared to body dysmorphic disorder (P=.007)
and nature of citation hallucinations and the accuracy generated
but not when comparing major depressive disorder to binge
by LLMs.
https://mental.jmir.org/2025/1/e80371 JMIR Ment Health 2025 | vol. 12 | e80371 | p. 5
XSL FO (page number not for citation purposes)
•
RenderX

JMIR MENTAL HEALTH Linardon et al
Comparisons With Prior Work directly test whether such prompt engineering methods reduce
hallucination and error rates.
The findings of this study align with previous research across
various disciplines showing that citation fabrication and Fourth, we analyzed a single output per prompt and did not
bibliographic inaccuracies are common in LLM-generated assess intraprompt variability across multiple generations. As
outputs [7-9,14]. However, this study extends this work in LLMs such as GPT-4o produce outputs stochastically, it is
several important ways. First, while previous research has possible that replication of the same prompt would produce
compared model outputs across distinct disciplines [7,8], which different citation fabrication or accuracy rates. Future work
has made it difficult to draw conclusions about relative should examine multiple generations per prompt to assess the
performance across topics of differing complexity within the consistency and reproducibility of results.
same field, we examined how citation reliability varies within
Broader Implications
the same domain by systematically manipulating public
familiarity, scientific visibility, and prompt granularity. This This research has broader implications for the conduct of
approach enabled a more fine-grained analysis of how topic scientific research. First, researchers and students should be
characteristics influence LLM performance, revealing aware of the risks associated with relying on LLMs for literature
meaningful variation even within a single area of research. generation and ensure that all outputs are subjected to careful
Second, while most earlier studies evaluated older versions of human oversight. This includes systematically checking,
GPT [8,15,16], our use of GPT-4o allowed us to assess whether validating, and verifying the accuracy and authenticity of any
citation reliability has improved in newer iterations. Despite citations or claims produced by models. Without such oversight,
expectations of enhanced accuracy, we found no clear evidence the field risks the proliferation of fabricated or inaccurate
of reduced hallucination rates, although cross-study comparisons references, which can erode scientific integrity and mislead
are inherently limited due to variation in topic selection, task readers, reviewers, and the public.
framing, and evaluation methods.
Second, journal editors and publishers have a critical role to
A key novelty of this work in comparison to previous literature play in maintaining scholarly standards by ensuring that
lies in its design. Rather than contrasting different disciplines LLM-generated citations do not make their way into published
or older model versions, we systematically manipulated topic outputs unchecked. One practical strategy is to use plagiarism
familiarity and review specificity within the same research field. detection software that flags whether citations appear in known
This approach revealed important topic-level differences in published sources. If a citation is identified by such software
citation reliability that would have been obscured in as plagiarized or matching existing content, this can serve as a
cross-disciplinary comparisons. Thus, this study not only extends positive indicator that the reference is real. Conversely, if a
existing evidence on LLM hallucinations but also introduces a citation does not trigger any match, it may signal that the source
new framework for evaluating how characteristics of the does not exist and was potentially hallucinated by the LLM,
research question itself influence model performance. warranting closer inspection and manual verification.
Limitations Third, academic institutions and research organizations should
develop clear policies and training guidelines around the
This study has several limitations that should be acknowledged.
responsible use of LLMs in scientific writing. As these tools
First, although a key strength of this study was the manipulation
become more deeply integrated into research workflows [5], it
of topic complexity and public familiarity within a single
is essential to equip users with the knowledge and skills to
domain, the findings may not generalize to other psychiatric
critically assess model-generated outputs. This includes
disorders or specialized subfields not examined here. Future
instruction on how to identify hallucinated citations, validate
research should assess whether similar patterns of citation
bibliographic content, and appropriately disclose the use of
fabrication and bibliographic errors are observed across a
generative artificial intelligence in scholarly outputs.
broader range of mental health topics and other academic
disciplines. Conclusions
Second, our findings are specific to GPT-4o and may not In conclusion, this research offers novel insights into how the
generalize to outputs generated by other LLMs. We selected characteristics of a topic influence the reliability of citations
GPT-4o because it is the most recent and widely adopted LLM produced by LLMs. While we found that citation fabrication
among academic researchers [4], making our results relevant and error rates are common overall, these inaccuracies were
to a significant proportion of users. Nevertheless, further studies less frequent when prompts addressed topics with greater public
should investigate whether different LLMs exhibit comparable awareness, an established evidence base, and a broad scientific
patterns or whether model-specific factors influence citation consensus. This suggests that the reliability of LLM-generated
reliability. citations is not fixed but contingent on the informational terrain
they are asked to navigate. Importantly, these findings have
Third, we did not use prompt engineering strategies; instead,
broader implications for the integration of LLMs into scholarly
we used standardized but straightforward prompts to reflect
workflows. They indicate that improving citation accuracy is
typical researcher use. It is possible that performance could be
not solely a technical challenge but also a matter of strategic
improved through techniques such as citation verification
prompt design and topic selection. Researchers can leverage
prompts or structured reference formatting. Future studies should
this insight using LLMs preferentially for well-established
domains while exercising caution and implementing verification
https://mental.jmir.org/2025/1/e80371 JMIR Ment Health 2025 | vol. 12 | e80371 | p. 6
XSL FO (page number not for citation purposes)
•
RenderX

JMIR MENTAL HEALTH Linardon et al
protocols when working in specialized areas where training data reliability rather than treating citation errors as random or
may be sparse or inconsistent. More broadly, our results inevitable. By embedding such practices, the academic
highlight the need for institutional guidance and training that community can harness LLMs’efficiencies while safeguarding
explicitly addresses the contextual factors influencing LLM the integrity of scholarly work.
Acknowledgments
The authors confirm that no content of this manuscript was generated by large language models. Large language models were
used only for minor proofreading purposes. JL is supported by a National Health and Medical Research Council investigator
grant (APP1196948).
Data Availability
The datasets generated or analyzed during this study are available from the corresponding author on reasonable request.
Authors' Contributions
Conceptualization: JL, HKJ, ZM, CA, CL, MM
Data analysis: JL
Data curation: JL, ZM, MM
Writing—original draft: JL, HKJ, MM
Writing—review and editing: JL, HKJ, ZM, CA, CL, MM
Conflicts of Interest
None declared.
Multimedia Appendix 1
ChatGPT prompts and outputs across the 3 disorders and prompt specificity.
[DOCX File , 79 KB-Multimedia Appendix 1]
Multimedia Appendix 2
Comparison of GPT citation outputs with actual citations.
[DOCX File , 70 KB-Multimedia Appendix 2]
References
1. Miller A, Taylor SG, Bedeian AG. Publish or perish: academic life as management faculty live it. Career Dev Int. Sep 20,
2011;16(5):422-445. [doi: 10.1108/13620431111167751]
2. Naveed H, Khan AU, Qiu S, Saqib M, Anwar S, Usman M, et al. A comprehensive overview of large language models.
ArXiv. Preprint posted online on July 12, 2023. [FREE Full text] [doi: 10.48550/arXiv.2307.06435]
3. Trajcheva B. ChatGPT usage statistics: 40+ insights on engagement, adoption, and business impact. DesignRush. Jul 01,
2025. URL: https://www.designrush.com/agency/ai-companies/trends/chatgpt-usage-statistics?[accessed 2025-07-07]
4. Linardon J, Messer M, Anderson C, Liu C, McClure Z, Jarman HK, et al. Role of large language models in mental health
research: an international survey of researchers' practices and perspectives. BMJ Ment Health. Jun 12, 2025;28(1):e301787.
[FREE Full text] [doi: 10.1136/bmjment-2025-301787] [Medline: 40514050]
5. Van Noorden R, Perkel JM. AI and science: what 1,600 researchers think. Nature. Sep 27, 2023;621(7980):672-675. [doi:
10.1038/d41586-023-02980-0] [Medline: 37758894]
6. Huang L, Yu W, Ma W, Zhong W, Feng Z, Wang H, et al. A survey on hallucination in large language models: principles,
taxonomy, challenges, and open questions. ACM Trans Inf Syst. Jan 24, 2025;43(2):1-55. [doi: 10.1145/3703155]
7. Walters WH, Wilder EI. Fabrication and errors in the bibliographic citations generated by ChatGPT. Sci Rep. Sep 07,
2023;13(1):14045. [FREE Full text] [doi: 10.1038/s41598-023-41032-5] [Medline: 37679503]
8. Mugaanyi J, Cai L, Cheng S, Lu C, Huang J. Evaluation of large language model performance and reliability for citations
and references in scholarly writing: cross-disciplinary study. J Med Internet Res. Apr 05, 2024;26:e52935. [FREE Full
text] [doi: 10.2196/52935] [Medline: 38578685]
9. McGowan A, Gui Y, Dobbs M, Shuster S, Cotter M, Selloni A, et al. ChatGPT and Bard exhibit spontaneous citation
fabrication during psychiatry literature search. Psychiatry Res. Aug 2023;326:115334. [doi: 10.1016/j.psychres.2023.115334]
[Medline: 37499282]
10. Krebs G, Fernández de la Cruz L, Mataix-Cols D. Recent advances in understanding and managing body dysmorphic
disorder. Evid Based Ment Health. Aug 2017;20(3):71-75. [FREE Full text] [doi: 10.1136/eb-2017-102702] [Medline:
28729345]
https://mental.jmir.org/2025/1/e80371 JMIR Ment Health 2025 | vol. 12 | e80371 | p. 7
XSL FO (page number not for citation purposes)
•
RenderX

JMIR MENTAL HEALTH Linardon et al
11. Plessen CY, Panagiotopoulou OM, Tong L, Cuijpers P, Karyotaki E. Digital mental health interventions for the treatment
of depression: a multiverse meta-analysis. J Affect Disord. Jan 15, 2025;369:1031-1044. [FREE Full text] [doi:
10.1016/j.jad.2024.10.018] [Medline: 39419189]
12. Linardon J, Shatte A, Messer M, Firth J, Fuller-Tyszkiewicz M. E-mental health interventions for the treatment and
prevention of eating disorders: an updated systematic review and meta-analysis. J Consult Clin Psychol. Nov
2020;88(11):994-1007. [doi: 10.1037/ccp0000575] [Medline: 32852971]
13. Schmidt M, Schoenenberg K, Engelkamp JE, Staufenbiel T, Martin A, Ebert DD, et al. Efficacy of an internet-based,
therapist-guided cognitive behavioral therapy intervention for adolescents and young adults with body dysmorphic disorder:
a randomized controlled trial. BMC Psychiatry. Apr 14, 2025;25(1):374. [FREE Full text] [doi: 10.1186/s12888-025-06797-1]
[Medline: 40229798]
14. Lehr SA, Caliskan A, Liyanage S, Banaji MR. ChatGPT as research scientist: probing GPT's capabilities as a research
librarian, research ethicist, data generator, and data predictor. Proc Natl Acad Sci U S A. Aug 27, 2024;121(35):e2404328121.
[doi: 10.1073/pnas.2404328121] [Medline: 39163339]
15. Wagner MW, Ertl-Wagner BB. Accuracy of information and references using ChatGPT-3 for retrieval of clinical radiological
information. Can Assoc Radiol J. Feb 20, 2024;75(1):69-73. [FREE Full text] [doi: 10.1177/08465371231171125] [Medline:
37078489]
16. Gravel J, D'Amours-Gravel M, Osmanlliu E. Learning to fake it: limited responses and fabricated references provided by
ChatGPT for medical questions. Mayo Clin Proc Digit Health. Sep 2023;1(3):226-234. [FREE Full text] [doi:
10.1016/j.mcpdig.2023.05.004] [Medline: 40206627]
Abbreviations
DOI: digital object identifier
LLM: large language model
Edited by A Stone; submitted 09.Jul.2025; peer-reviewed by VG Jansari, T Oami; comments to author 22.Aug.2025; revised version
received 24.Aug.2025; accepted 15.Sep.2025; published 12.Nov.2025
Please cite as:
Linardon J, Jarman HK, McClure Z, Anderson C, Liu C, Messer M
Influence of Topic Familiarity and Prompt Specificity on Citation Fabrication in Mental Health Research Using Large Language
Models: Experimental Study
JMIR Ment Health 2025;12:e80371
URL: https://mental.jmir.org/2025/1/e80371
doi: 10.2196/80371
PMID:
©Jake Linardon, Hannah K Jarman, Zoe McClure, Cleo Anderson, Claudia Liu, Mariel Messer. Originally published in JMIR
Mental Health (https://mental.jmir.org), 12.Nov.2025. This is an open-access article distributed under the terms of the Creative
Commons Attribution License (https://creativecommons.org/licenses/by/4.0/), which permits unrestricted use, distribution, and
reproduction in any medium, provided the original work, first published in JMIR Mental Health, is properly cited. The complete
bibliographic information, a link to the original publication on https://mental.jmir.org/, as well as this copyright and license
information must be included.
https://mental.jmir.org/2025/1/e80371 JMIR Ment Health 2025 | vol. 12 | e80371 | p. 8
XSL FO (page number not for citation purposes)
•
RenderX