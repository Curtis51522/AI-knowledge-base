Online path planning for disaster response in
the presence of unknown road disruptions:
a comparison of research and practice

Jannatul Shefa and Ashlea Bennett Milburn
Department of Industrial Engineering, University of Arkansas, Fayetteville, Arkansas, USA, and

Erica Gralla
Department of Engineering Management and Systems Engineering,
The George Washington University, Washington, District of Columbia, USA

Abstract
Purpose – This  paper aims  to  illuminate  gaps between  theory and  practice in  one crucial area of disaster  logistics:  transportation management
between staging areas and final destinations, on uncertain and disrupted road networks. Relevant current practice in federal, state, nonprofit and
private disaster response organizations in the USA is described and compared to pertinent assumptions in the literature on disaster response online
path planning under uncertainty.
Design/methodology/approach – The study uses a qualitative approach. The disaster response routing literature informed the development of an
interview guide used for in-depth interviews with disaster response logistics practitioners. Collected data were coded to identify how path planning
activities were  accomplished.  Interview findings  were then linked  back  to  the literature  to  identify where theory  coincides and/or contrasts  with
practice.
Findings – The study identifies a number of important mismatches between current practice and the assumptions in the modeling literature. Current
practice  likely  would  not  support  online  path  planning  models  in  which  algorithms:  run  within  drivers’  vehicles,  depend  on  knowledge  of  the
probability of roads being open or closed, assume immediate information updates on road status or optimize speed at the expense of reliability. For
research  advancements  to  be  leveraged,  practitioners  must  adopt  formal  systems  for  sharing  information,  and  research  must  adapt  to  the
constraints and goals of response practitioners.
Originality/value – Despite the availability of sophisticated models to support disaster response path planning, few are adopted in practice. This
research  provides  a  better  understanding  of  disaster  transportation  management  and  its  challenges.  The  findings  could  help  bring  research  into
better alignment with the needs of practitioners, thereby improving the speed and effectiveness of the response and reducing the suffering of those
affected by disasters.

Keywords  Disaster relief transportation planning, Uncertain road conditions, Online models for path planning

Paper type Research paper

1.  Introduction

Disasters  are  becoming  more  prevalent,  due  to  the  rapid
environmental  and  socioeconomic  changes  happening  on
multiple  fronts  (Mitra  and  Shaw,  2023;  The  World  Bank,
2023). The number of annual natural disasters has increased
10-fold from 1960 to 2019 (Institute for Economics and Peace,
2020), and could rise from approximately 400 in 2015 to 560
by  2030  [United  Nations  Office  for  Disaster  Risk  Reduction
(UNDRR),  2022].  Economic  consequences  are  also  rising:
over  380  billion-dollar  climate  and  weather  disasters  have
occurred in the USA since 1980, exceeding $2.7tn in total cost
(NCEI, 2024).

The current issue and full text archive of this journal is available on Emerald
Insight at: https://www.emerald.com/insight/2042-6747.htm

Journal of Humanitarian Logistics and Supply Chain Management
16/2 (2026) 121–135
Emerald Publishing Limited [ISSN 2042-6747]
[DOI  10.1108/JHLSCM-05-2023-0046]

Disasters  often  cause  shortages  in  essential  utilities  and
resources like water, food, medical supplies and shelter. They
also  cause  significant  damage  to  buildings  and  critical
infrastructures,  such  as  homes,  hospitals,  power  grids,
bridges,  road  networks  and  water  systems  (FEMA,  2020).
Logistics plays a crucial role in supporting disaster-impacted

© Jannatul Shefa, Ashlea Bennett Milburn and Erica Gralla. Published by
Emerald Publishing Limited. This article is published under the Creative
Commons  Attribution  (CC  BY  4.0)  license.  Anyone  may  reproduce,
distribute,  translate  and  create  derivative  works  of  this  article  (for  both
commercial and non-commercial purposes), subject to full attribution to
the original publication and authors. The full terms of this license may be
seen at http://creativecommons.org/licences/by/4.0/legalcode

This  work  was  supported  by  the  National  Science  Foundation  (NSF)
under  Grant  Number  CMMI  1554412.  The  opinions,  findings  and
conclusions are those of the authors and do not necessarily reflect the views
of the NSF.

Received 31 May 2023
Revised 12 June 2024
23 November 2024
22 February 2025
Accepted 3 March 2025

121

Downloaded from http://www.emerald.com/jhlscm/article-pdf/16/2/121/11452423/jhlscm-05-2023-0046en.pdf by guest on 15 April 2026

Online path planning

Journal of Humanitarian Logistics and Supply Chain Management

Jannatul Shefa, Ashlea Bennett Milburn and Erica Gralla

Volume 16 · Number 2 · 2026 · 121–135

people,  by  providing  critical  supplies  to  affected  areas  and
minimizing detrimental effects on infrastructure and people
(Holguín-Veras et al., 2012). Estimates indicate that 75–80%
of  the  total  investment  in  disaster  response  activities  is
attributed  to  logistics  (Trunick,  2005;  Stumpf  et  al.,  2023)
and 40% of these investments represent waste associated with
duplication  of  efforts  and  lack  of  detailed  planning  and
analysis (Day et al., 2012; Van Wassenhove 2006).

This  paper  studies  one  crucial  area  of  disaster  logistics:
transportation between staging areas and final destinations on
uncertain and damaged road networks. In the USA, a Federal
Staging Area (FSA) serves as the logistical support hub for a
federally-declared disaster. Resources like water, food and mass
care supplies are readied at the FSA for deployment to areas in
need (FEMA, 2022). They are dispatched by the truckload to
intermediate or final destinations in the disaster-affected area,
such as shelters and other sites (FEMA, 2022; FEMA, 2019).
For each load, a path must be planned using the existing road
network from the FSA to the destination. These delivery efforts
are  typically  challenging.  Roads  are  often  closed  due  to  high
water,  debris  or  damaged  infrastructure  (FEMA,  2020),  and
these  disruptions  are  only  discovered  as  the  response
progresses.  The  disaster  response  routing  literature  refers  to
this problem as online path planning. (Here, path planning is
distinguished  from  route  planning,  in  that  the  former  entails
planning  a  path  between  a  prescribed  origin  and  destination
pair, whereas the latter entails planning a route that begins and
ends at a depot and visits multiple destinations in between).

New tools are available to support many aspects of disaster
response  logistics,  including  a  variety  of  optimization  models
(e.g.  Caunhye  et  al.,  2012;  Gutjahr  and  Nolz,  2016),
information technology (e.g. Özdamar and Ertem, 2015) and
analytics  and  artificial  intelligence  (Spencer,  2021; De  Boeck
et  al.,  2023).  However,  major  gaps  remain  between  the
achievements of research and the problems of practice (Besiou
and Van Wassenhove, 2020), and few of these tools are actually
in use (e.g. IFRC, 2013). Better understanding of humanitarian
practice and its challenges could help bring research into better
alignment  with  the  needs  of  practitioners,  thereby  supporting
improvements  in  humanitarian  logistics  (Besiou  and  Van
Wassenhove,  2020;  Kovacs  and  Moshtari,  2019;  de  la  Torre
et al., 2012; Kunz et al., 2017).

This paper aims to investigate and compare how practice handles
and  how  research  models  this  disaster  transportation  problem  –
transportation  between  the  FSA  and  final  destinations  in  the
presence  of  dynamically  evolving  and  uncertain  road  conditions.
Specifically,  interviews  with  practitioners  and  qualitative
analysis techniques are used to identify common practices for
each of the following elements of this problem:
•  who is doing the planning;
•  how those doing the planning think about the network;
•  what objective(s) guide their planning decisions; and
•  how they form and update their knowledge regarding the
uncertain and online problem inputs, namely, the status of
roads.

In  the  case  of  the  latter,  this  paper  discusses  several
dimensions of the road status knowledge dynamics. We begin
with information sources that planners consult to learn about
road  status.  Next,  we  discuss  efforts  to  discover  new

intentional  or
information  about  road  status,  whether
unintentional. Finally, we describe to what extent road status
knowledge is shared between network users. For example, does
the  common  knowledge  base  span  organizations  or  is  it
relegated  within  an  organization?  Is  that  common  knowledge
base updated regularly and with intention, or instead in an ad
hoc fashion?

As we explore each of these problem elements, we provide
evidence from practice as observations of how real world actors
currently operate in this decision space. We also connect those
observations to the online disaster response routing literature,
to illuminate how current models are similar to and different
from practice. Finally, we discuss what implications for practice
and modeling these similarities and differences entail.

This  paper  is  structured  as  follows.  Section  2  discusses
relevant literature and highlights the research gap addressed in
this study. Section 3 elaborates the research design. Section 4
presents  and  discusses  the  findings,  comparing  observations
from practice to the literature on online path planning under
uncertainty. Section 5 discusses the implications of our findings
for  improving  both  theory  and  practice  in  this  area.  Finally,
Section  6  concludes  the  paper  by  summarizing  key  gaps
between path planning models and real-world practice.

2.  Literature review

Two  distinct  streams  of  literature  are  relevant  to  this  paper’s
aims:  the  modeling  literature  that  most  closely  represents  the
planning  problem  at  the  FSAs,  and  previous  attempts  to
compare such theoretical models to practice. Therefore, models
for online path planning in disaster response under road status
uncertainty, the specific area of practice this paper investigates,
are  reviewed  in  subsection  2.1.  The  literature  addressing
comparison of research and practice in humanitarian logistics is
discussed in subsection 2.2. The specific gap that the present
study addresses is summarized in subsection 2.3.

2.1  Online path planning in disaster response under
road status uncertainty
Early  papers  addressing  disaster  relief  routing  assumed
deterministic  planning  environments  (e.g.  Knott,  1987;
Haghani  and  Oh,  1996).  Later  studies  began  to  explicitly
model the uncertainty inherent in disaster response routing. De
La Torre  et al. (2012)  identify papers modeling two types  of
uncertainty in routes: edges that can fail (e.g. Vitoriano et al.,
2009; Ukkusuri  and  Yushimito,  2008)  and  edge  travel  times
that are uncertain (e.g. Van Hentenryck et al., 2010; Mete and
Zabinsky, 2010; Shen et al., 2009; Rawls and Turnquist, 2010;
Salmeron  and  Apte,  2010).  In  those  reviewed  papers,
uncertainty  is  modeled  via  two-stage  stochastic  planning
models,  where  plans  are  developed  in  a  first  stage  and  then
uncertainty  is  revealed  and  plans  adapted  to  account  for  the
uncertainty  in  the  second  stage.  In  contrast,  the  decision
environment motivating this paper is online, with uncertainty
regarding  edge  failures  being  resolved  over  multiple  periods
and plans frequently being revisited to avoid those disruptions.
The application studied in this paper is online path planning
under  road  status  uncertainty.  Online  models  for  uncertain
path planning frameworks first emerged with the introduction
of the Canadian Traveler Problem (CTP) (Papadimitriou and

Downloaded from http://www.emerald.com/jhlscm/article-pdf/16/2/121/11452423/jhlscm-05-2023-0046en.pdf by guest on 15 April 2026

122

Online path planning

Journal of Humanitarian Logistics and Supply Chain Management

Jannatul Shefa, Ashlea Bennett Milburn and Erica Gralla

Volume 16 · Number 2 · 2026 · 121–135

Yannakakis,  1991)  and  the  Bridge  Problem  (Blei  and
Kaelbling,  1999).  The  CTP  and  the  Bridge  Problem  both
model a scenario where one must traverse a network without
the  benefit  of  a  priori  knowledge  of  edge  failures,  though
probabilities of edge failure are assumed to be available in the
latter. In both the CTP and the Bridge Problem, edge failures
are  discovered  in  transit,  as  they  are  encountered,  and  the
traveler  must  plan  a  new  path  to  avoid  them.  Despite  the
scenarios motivating these models, namely, snow on Canadian
roadways and bridges damaged by storms, these models were
relatively slow to be explicitly adopted in the disaster response
routing literature. Instead, papers advancing CTP and related
online  path  or  route  planning  models  mention  motivating
applications  such  as  robot  navigation  (e.g.  Lita  et  al.,  2001;
Guo and Barfoot, 2019), express logistics and delivery routing
in urban networks (e.g. Liao and Huang, 2014; Zhang et al.,
2016) and minefield countermeasures (Aksakalli et al., 2016).
Disaster  relief  distribution  was  mentioned  alongside  other
applications for online path planning models in Yildirim et al.
(2019), and was emphasized in the article title in Akbari and
Shiri (2021). Recent graduate theses and dissertations focused
on  the  application  of  CTP  models  to  disaster  path  planning
problems include Alseth (2020) and Chanchad (2023).

Much of the CTP literature emphasizes theoretical analysis.
For example, online algorithms for deterministic variants of k-
CTP are developed and their worst case competitive ratios are
proven;  k-CTP  refers  to  the  special  case  in  which  at  most  k
edges can fail (e.g. Westphal, 2008; Xu et al., 2009; Berg'e &
Salaün,  2019;  Bender  and  Westphal,  2015;  Demaine  et  al.,
2014; Demaine et al., 2021). For the Stochastic CTP, papers
prove  its  complexity  (Fried  et  al.,  2013),  provide  an  exact
algorithm with polynomial runtime for special cases (Nikolova
and Karger, 2008), and also provide an exact algorithm with
nonpolynomial  runtime  (Aksakalli  et  al.,  2016).  Given  the
complexity  of  solving  large  instances  of  the  Stochastic  CTP,
other  literature  develops  heuristic  solution  approaches  and
analyzes  their  performance  via  computational  studies  (e.g.
Eyerich et al., 2010; Sahin and Aksakalli, 2015; Bai et al., 2018;
Alseth, 2020; Chanchad, 2023).

The CTP assumes a single driver traversing a graph between
a single origin and destination pair. Model variants that more
closely approach the planning environment present in FSAs are
emerging. At an FSA, all loads share an origin (i.e. the FSA)
and are being dispatched to multiple destinations via multiple
drivers.  Multiagent  CTP  models  address  multiple  drivers
traversing a graph and possibly sharing discovered information
with  one  another  as  they  go.  In  some  of  these  models,  the
drivers are all trying to reach the same destination (e.g. Zhang
et al., 2013; Shiri and Salman, 2017; Alseth, 2020), whereas in
others, each driver has their own intended destination (e.g. Lita
et  al.,  2001;  Chanchad,  2023).  The  latter  problem,  with
multiple  agents  and  multiple  destinations,  most  closely
resembles  the  real-world  decision  environment  at  the  FSA.
However,  none  of  this  literature  rigorously  compares  these
models to the problems solved in practice.

2.2  Comparisons of research and practice in
humanitarian logistics
It  has  long  been  recognized  that  there  is  a  significant  gap
between research and practice in operations management (e.g.

Sodhi and Tang, 2008, Corbett and Van Wassenhove, 1993),
and  humanitarian  logistics  is  no  exception.  A  number  of
papers note gaps between research and practice; for example,
Kovacs  and  Moshtari  (2019)  argue  for  the  importance  of
understanding real  practical  problems as part of  the  research
process; and others note that few optimization models are used
in  practice  (De  Vries  &  Van  Wassenhove  2020;  Gralla  and
Goentzel, 2018). Many papers have stressed the importance of
working  on  practice-driven  problems  (e.g.  Starr  and  Van
Wassenhove, 2014;  Besiou  and  Van  Wassenhove,  2020)  and
suggested strategies for doing so (e.g. Kunz et al., 2017; Kovacs
and Moshtari, 2019).

However,  only  a  few  papers  directly  compare  research  to
practice,  based  on  empirical  data  on  the  practice  of
humanitarian logistics (as we do in this paper). Besiou and Van
Wassenhove (2020) compared the topics of academic papers in
humanitarian logistics-related special issues to the topics of a
series  of  practitioner  conferences.  They  found  that  research
topics  do  not  align  very  well  with  practitioner  concerns,  and
they  suggest  several  opportunities  to  bring  them  into  better
alignment.  De  la  Torre  et  al.  (2012)  review  the  literature,
review  practitioner  reports  and  conduct  interviews  with
practitioners, to compare the practice of and research on relief
routing. They identify specific areas of mismatch, including the
lack of research on stages beyond immediate relief; a need to
better incorporate uncertainty in supply, vehicle availability and
demand; an opportunity to model risk-averse behavior; and an
opportunity to better demonstrate the value of routing models.
A  few  additional  papers  describe  practice  without  directly
comparing it to research. Recent examples include Lewin et al.
(2018), which uses five case studies on humanitarian logistics
topics,  based  on  40  interviews  with  international  logistics
response  practitioners,  to  demonstrate  the  essential  role  of
supply  chain  management  in  humanitarian  response;  and
Stumpf et al. (2023), which uses interviews and financial data
from practice organizations to examine the importance of and
costs invested in supply chain management in the humanitarian
field.  Both  papers  also  identify  important  opportunities  for
future research to contribute to improvements in humanitarian
practice.  However,  given
the  volume  of  research  on
humanitarian logistics – meriting 43 review papers as of 2018
(Kovacs and Moshtari, 2019) – there have been relatively few
attempts to characterize practice in comparison to research.

2.3  Summary of contribution to literature
The  present  paper  responds  to  the  call  for  better  matches
between  practice  and  research  by  examining  a  particular
problem – online path planning in disaster response under road
status uncertainty – and comparing the assumptions made in
CTP models and variants to the way such problems are dealt
with in practice. The limited literature comparing models with
practice  has  not  addressed  this  problem  nor  made  such  a
detailed and systematic comparison of practice with research in
a single focused setting. We draw on a series of interviews that
enable us to characterize, in detail, how responders in the US
disaster  response  system  accomplish  disaster  relief  path
planning. In drawing heavily from the empirical context, we use
a similar approach to that of de la Torre et al. (2012). However,
our focus is on a narrower problem, online path planning under

Downloaded from http://www.emerald.com/jhlscm/article-pdf/16/2/121/11452423/jhlscm-05-2023-0046en.pdf by guest on 15 April 2026

123

Online path planning

Journal of Humanitarian Logistics and Supply Chain Management

Jannatul Shefa, Ashlea Bennett Milburn and Erica Gralla

Volume 16 · Number 2 · 2026 · 121–135

road status uncertainty, and we provide a deeper understanding
of practice in this area.

3.  Research design

To  understand  current  practices  in  disaster  response  path
planning from FSAs in the USA, which requires an exploratory
approach,  we  adopted  an  inductive  qualitative  research
approach  based  on  grounded  theory  (Corbin  and  Strauss,
2008).  An  overview  of  the  research  approach  is  given  in
Figure 1. Each of the steps in the figure is described in detail in
the remainder of this section.

The  first  step  (see  Figure  1)  was  to  define  the  research
questions, which focused on how disaster responders planned
transportation between  the FSA  and final  destinations in the
presence of uncertain road conditions. A formal interview guide
was  structured  based  on  insights  from  an  initial  literature
review  and  preliminary  conversations  with  emergency
responders. The interview guide is included in the Appendix.
Due to the inductive nature of this study, the guide consisted of
a set of open-ended questions focused on key aspects of disaster
response  transportation  activities,  grounds  that  prompt
changes in transportation planning and factors that influence
achievement of emergency response goals.

interviewees,

following  a  snowball

Next (second step in Figure 1), interviews were conducted
with  personnel  from  entities  at  different  levels  who  actively
participated  in  disaster  logistics  operations,  especially  during
the  2017  and  2018  storm  seasons  in  the  USA.  The  primary
sampling  strategy  was  purposive:  the  goal  was  to  identify
participants from multiple organizations of each of several types
(federal,  state,  private  and  nonprofit).  The  investigators’
professional networks were used to identify initial participants
for  the  interviews.  Those  participants  suggested  additional
possible
technique.
Identification  of  participants  concluded  when  at  least  two
interviews for each organization type were conducted and the
knowledge gained from additional interviews was small. Over
the six-month period from January to June 2019, 14 in-depth
interviews were performed with participants from 14 different
organizations, comprised of five federal-level entities (denoted
F1,  F2,  F3,  F4  and  F5),  three  state-level  organizations
(denoted S1, S2 and S3), four private companies (denoted P1,
P2, P3 and P4) and two nonprofit organizations (denoted N1
and N2). (Two of these interviews, F1 and F5, were on related
but different topics and did not provide information relevant to
path planning within a FSA, so they are not referenced in this
paper.) There were a total of 22 participants, as many of the
interviews
the
participating  organization.  With  different  backgrounds  and
roles, these individuals provide a diverse set of perspectives that

than  one  person

included  more

from

span  the  relevant  organizations  taking  part  in  hurricane
response in 2017 and 2018.

Most of the interviews were conducted by two interviewers.
One primary interviewer asked the questions while the second
interviewer  took  notes  and  ensured  the  flow  of  conversation
remained  on  track  and  conformed  to  the  research  objective.
The duration of the interviews ranged from one to one and a
half hours. Although the interviews were structured by the base
questionnaire,  any  relevant  lead  was  pursued  with  follow-up
questions  to  reveal  additional  information.  In  all  cases,  the
findings  are  presented  in  a  manner  that  does  not  disclose
information that could expose or  be  linked to the identity  or
affiliation of the respondents. Interviewees are identified only
by their scope of engagement and responsibility such as local,
private, state or federal. All the interviews were recorded with
the consent of the interviewees for documentation. This study
was conducted with Institutional Review Board approval.

The  interview  audio  recordings  were  transcribed  into  text
using otter.ai software and checked manually to ensure proper
conversion. The transcription of all interviews was completed
within one month of the last interview and their lengths ranged
from 4,600–14,000 words each. The interview notes and other
relevant  data  were  also  documented.  These  data  were  then
imported into atlas.ti software for qualitative analysis.

The third step (see Figure 1) was data analysis. The first part
of the data analysis was open coding. Labels or “codes” were
attached to the text reflecting a conceptual description of the
corresponding content. For this paper, we coded data related to
how path planning activities were accomplished. This process
was  completed  by  three  researchers  independently;  next,  the
open  codes  were  discussed  among  the  researchers  and  a
consensus reached about an initial set of concepts (codes) and
their  definitions.  Once  the  initial  codes  were  defined  by  the
research  team,  one  author  proceeded  to  re-code  the  data
accordingly.

The  next  step  in  data  analysis  was  to  investigate  the
relationships between codes and identify higher-level categories
that relate them to one another (axial coding). Similarly coded
segments  of  data  were  examined  together,  and  differently
coded segments were compared, to refine the code definitions
and identify relationships between codes. Codes were split or
combined as needed during this refinement process, and new
codes were defined as new concepts emerged.

At  this  stage  (fourth  step  in  Figure  1),  concepts  from  the
literature were also incorporated, either by defining new codes
or  by  identifying  existing  codes  that  referred  to  the  same
concept  as  the  literature.  Through  constant  comparison
between the data, theoretical concepts and emerging codes, we
refined the set of codes and their definitions. The first author
continually re-coded the data with the updated code definitions

Figure 1  Overview of the research approach

Downloaded from http://www.emerald.com/jhlscm/article-pdf/16/2/121/11452423/jhlscm-05-2023-0046en.pdf by guest on 15 April 2026

124

Online path planning

Journal of Humanitarian Logistics and Supply Chain Management

Jannatul Shefa, Ashlea Bennett Milburn and Erica Gralla

Volume 16 · Number 2 · 2026 · 121–135

throughout this process. Another author then coded portions of
the data with the updated codes, and codes were compared and
discussed  among  all  the  authors  to  ensure  clarity  and
consistency. The final set of codes represent the key concepts
that emerged from the data and that existed in the literature;
they describe current practices in disaster response online path
planning.  Examining  the  code  definitions  and  relationships,
their  frequency,  the  conditions  under  which  they  occur  and
their  content,  provides  insights  that  form  the  basis  for  the
findings described below (last step in Figure 1).

4.  Findings and discussion

In  the  following  sections,  observations  from  practice  and
connections  to  literature  are  provided  for  each  element  of  the
online  path  planning  problem  under  uncertainty  taking  place  at
FSAs. The findings begin with who is doing the planning (4.1),
how those doing the planning think about the network (4.2) and
what objective(s) guide their planning decisions (4.3). Then, how
those  doing  the  planning  form  and  update  their  knowledge
regarding  road  statuses  is  discussed.  This  includes:  information
sources  that  planners  consult  to  learn  about  road  status  (4.4);
efforts  to  discover  new  information  about  road  status,  whether
intentional  or  unintentional  (4.5);  and  sharing  of  road  status
knowledge between network users (4.6). Each subsection begins
by describing the assumptions from CTP models in the literature.
Next,  the  findings  from  the  interview  analysis  are  described.
Finally,  the  last  paragraph  of  each  subsection  compares  these
findings  from  practice  to  the  assumptions  in  the  modeling
literature and identifies insights for modeling and practice.

In keeping with graph theory, which distinguishes between a path
and a route (i.e. multistop cycle or closed loop), this section adopts
the term path planning as defined in subsection 2.2 to describe the
decision  environment.  This  is  because  the  interviewees  are
describing  the  selection  of  a  path  for  a  full  truckload  between  a
single origin and destination pair, though they refer to this as “route
planning.”  We  keep  the  phrase  “route  planning”  in  interviewee
quotations and use path planning in all narrative discussion.

4.1  Responsibility for path planning
Nearly all CTP models implicitly assume the driver (agent) is
doing  their  own  path  planning.  However,  the  interview  data
suggest that the reality is more complex. Most organizations do
their own path planning centrally or leave it to a subcontracted
transportation  company.  The  path  planners  often  coordinate
with their drivers or with other organizations to deal with road
closures  and  blockages.  Table  1  shows  which  interviewees
discussed each of these approaches to path planning.

Table 1  Responsibility for path planning, according to each interviewee

Most  of  the  interviewees  (nine  out  of  ten  who  discussed  the
subject) implied that a person or group within their organization
was responsible for path planning. For example, one interviewee
explained, “[When] helping route that load or that driver [. . .] our
Ops [is] tracking bridges out.” [P3]. However, in most cases, they
did  not  specify  who  within  the  organization  planned  paths,  but
instead simply referred to “we”. For example, “Trying to get 25
[vehicles] turned around in a row, we’re going to re-route them
[. . .]” [S1]; or in a second example, “We will assess every mission
as to where it’s going, which routes to take and dictate the route
until the roads  become more normal” [F4]. It  is clear  from the
interviews that these organizations do their own path planning but
not which part of the organization is tasked with the job. In two of
the  interviews,  it  appeared  that  different  subteams  within  the
organization  do  path  planning  separately.  For  example,  one
interviewee explained:

If we’re doing [one type of mission], the individual responsible for creating
those [. . .] routes is within the [mission] team [. . .] And the other [mission’s]
routing  is  dependent  upon  where  their  assignment  is  [. . .].  So  there’s  no
national level routing methods [N2].

Three organizations noted that a private transportation company
chose the paths for their own vehicles. (Transportation companies
were often contracted by FEMA or other entities to transport their
goods.) For example, a federal interviewee explained that:

[. . .] you would give one of these companies a set of loads and some delivery
deadlines, and then they have the freedom or the authority to figure out the
best way to do that [F3].

Four of the organizations included in the earlier category, in which
path planning was done within the organization, are private entities
themselves: these interviews provide additional evidence that the
private companies often do their own path planning.

Some of the organizations that planned their own paths also
described coordinating with local authorities. For example, one
noted that “we rely heavily on TXDOT, the Texas Department
of  Transportation,  to  tell  us  what  our  options  are”  [S2].
Another  mentioned  coordinating  with  the  state  police  and
FEMA to determine viable paths [P2]. It is not clear from the
interviews  if  these  relationships  mainly  involved  acquiring
information  from  other  organizations  or  if  the  path  planning
decisions  were  a  collaborative  process.  Other  organizations
described  coordinating  with  their  drivers  to  determine  paths.
For example, one explained that when:

[. . .] you get to a road closure [that] was not on the map [or] a high water
situation and you’re trying to determine how high is the water; it’s just at
that point we kind of rely on the driver’s best judgment [P1].

Drivers were not described as determining their own paths, but
rather coordinating with an organizational authority to re-plan
when needed.

Planner

Organization
Transport company
+ Coordination with drivers
+ Coordination with local authorities

F2

F3

F4

✓

S1

✓

S2

✓

S3

✓

✓

✓

P1

✓

✓

P3

✓
✓

P4

✓*

✓

P2

✓

✓
✓

N1

N2

Tot

✓*
✓
✓

9
3
3
2

Note(s): *indicates that the organization plans paths centrally but relies on subteams within the organization to plan paths for different teams
Source(s): Authors’ own work

Downloaded from http://www.emerald.com/jhlscm/article-pdf/16/2/121/11452423/jhlscm-05-2023-0046en.pdf by guest on 15 April 2026

125

Online path planning

Journal of Humanitarian Logistics and Supply Chain Management

Jannatul Shefa, Ashlea Bennett Milburn and Erica Gralla

Volume 16 · Number 2 · 2026 · 121–135

Taken together, these observations suggest several relevant
insights  for  online  path  planning  modeling.  First,  many
organizations  do  plan  their  own  paths,  suggesting  that  they
would be able to make use of a path planning tool. However, a
method for reliably communicating the path to the driver will
be required, as the driver is not the entity that would use the
tool. Second, there are multiple organizations working in any
disaster, and each plans their own paths independently. While
interviewees  mentioned  coordination  with  local  authorities,
there was no mention of coordination with other transporting
organizations,  and  one  interviewee  even  explained  that  such
coordination  did  not  take  place  [P3].  Thus,  there  is  no
overarching  central  authority  planning  paths  for  the  disaster
response as a whole. Third, on a related note, it appears that
decisions on cargo prioritization are often made by a different
authority
those  who  plan  paths.  Transportation
companies  plan  paths  based  on  required  loads  and  delivery
locations,  but  the  decision  about  what  to  send  where  is  not
made  by  these  companies.  Thus,  models  that  couple  these
decisions may be difficult to leverage in practice.

than

4.2  Representation of the transportation network
The  literature  on  online  path  planning  under  road  status
uncertainty typically represents the transportation network as a
graph, with some assumptions regarding what is known about
edge  status  (ES)  and  edge  travel  time  (ETT).  Typical
representations  of  uncertain  edge  status  include:  (ES1)  edge
status as available or blocked is unknown (e.g. Papadimitriou
and Yannakakis, 1991); and (ES2) which extends ES1 with the
assumption  that  a  probability  describing  the  likelihood  each
edge  is  blocked  is  available  (e.g.  Blei  and  Kaelbling,  1999).
Regarding edge travel time (ETT), the CTP literature assumes
edge  travel  times  are  known  (ETT1),  while  other  response
routing models assume uncertain edge travel times described
by either a stochastic distribution or a range (ETT2) (e.g. Mete
and Zabinsky, 2010).

The interview data shed light on whether and how disaster
response practitioners “represent” the network in their work.
Table  2  summarizes  which
interviewees  used  which
representations.  Unsurprisingly,  none  of  the  interviewees
described  transportation  networks  in  mathematical  terms.
Instead,  most  interviewees  seemed  to  (implicitly)  use  road
status representation ES1: they thought of roads as being open,
blocked or unknown. For example, P2 explained, “The drivers
tell them which routes are good and which aren’t.” Similarly,
S2 mentioned talking with the Department of Transportation
representative  to  ask,  “What’s  open?”.  P3  reported  that  if  a
driver found a blocked road, “they call back and tell us and then
our  people  on  the  ground  report  to  FEMA  and  now  there’s
accountability  that  this  road  is  blocked.”  Across  all  the
interviews,  8  of  the  12  respondents  showed  evidence  of  this

representation, and the remaining four did not discuss anything
related to the status of roads, suggesting that this representation
is used universally.

Three respondents also spoke of roads using language similar
to road status representation ES2: the likelihood of a road being
open. For example, P2 described:

[. . .] if you have a road that you can’t rely on, you try not to use it [. . .] you
go on the road you can rely on. [. . .] If roads have a history of having low
passes  and  lots  of  water  [. . .]  they  are  probably  going  to  use  that  tribal
knowledge quickly just to close this area off because this one has a history of
flooding.

Similarly, F4 explained that they:

[. . .] look at the risk to routes, for example a route that is a flood risk [. . .] we
would make the assumption that’s flooded. [. . .] In an earthquake scenario,
we  study  all  the  bridges,  [. . .]  which  bridge  do  we  think  is  not  going  to
survive?

Interestingly, the three respondents using language similar to
ES2  all  spoke  in  terms  of  both  representations  ES1  and  ES2
together:  when  they  identified  a  risky  route,  they  assumed  it
would be closed, as in P2’s quote above. Only one respondent
used  edge  travel  time  representation  ETT2,  describing  how
they might pick a longer-distance route over a shorter one if it
was likely to take less time given the traffic situation [S2].

An  additional  distinction  evident  in  the  interviews  is
whether status as blocked or available is attached to “roads”
or  “routes.”  The  terminology  “road”  appears  roughly
equivalent to an edge in a network graph, whereas a “route” is
similar  to  a  path  from  an  origin  to  a  destination  and  may
comprise  multiple  “roads.”  Table  3  summarizes  which
interviewees used which representations. Some organizations
seem to track status on a road-by-road basis: for example, “If
my driver calls in and says” “This road is a no go road” [. . .]
they’re  marking  it  off”  [P2].  On  the  other  hand,  other
organizations  appear  to  maintain  knowledge  of  “routes”
(paths)  rather  than  roads:  they  track  the  one  or  two  open
paths they are using, and when one is blocked, they look for a
different  path,  rather  than  tracking  the  status  of  each
individual  road  within  them.  For  example,  one  interviewee
explained, “[A driver] would give us a confirmed route. And
then  we  would  start  shoveling  all  the  trucks  through  that
confirmed  [route]  until  something  changed  and  that  route
was no longer good or if we got a better route” [P1]. Another
organization described using “one of those routes as our key
routes to want to get into an area” [S1]. Attaching status to
“routes” rather than “roads” is analogous to route and path
reliability  formulations  in  the  literature  (e.g.  Ukkusuri  and
Yushimito, 2008).

These  results  suggest  that  disaster  response  practitioners
represent  the  transportation  network  by  considering  roads  as
blocked,  open  or  unknown.  This  is  consistent  with  literature
regarding  online  path  planning  problems,  like  the  CTP,  in

Table 2  Number of discussions in each interview that used each network representation

Network representation

F2

F3

F4

S1

S2

S3

P1

P2

P3

P4  N1  N2

Tot

ES1: whether edges available or blocked is unknown
ES2: probability describing edge blockage likelihood is available
ETT2: travel time is unknown and stochastic information is available

1
1

1
1

3

2

1

3
1

1

2

1

8
3
1

Source(s): Authors’ own work

Downloaded from http://www.emerald.com/jhlscm/article-pdf/16/2/121/11452423/jhlscm-05-2023-0046en.pdf by guest on 15 April 2026

126

Online path planning

Journal of Humanitarian Logistics and Supply Chain Management

Jannatul Shefa, Ashlea Bennett Milburn and Erica Gralla

Volume 16 · Number 2 · 2026 · 121–135

Table 3  Number of discussions in each interview that used each representation

Representation

F2

F3

F4

S1

S2

S3

P1

P2

P3

P4

N1

N2

Tot

Concept of status is attached to roads
Concept of status is attached to routes

Source(s): Authors’ own work

1

1

1
2

1

2
4

which  the  status  of  edges  are  unknown  until  they  have  been
physically  observed  (Papadimitriou  and  Yannakakis,  1991).
Considering  edge  travel  time  as  deterministic  rather  than
stochastic  is  consistent  with  the  CTP  literature  as  well.
Practitioners occasionally rely on additional knowledge, such as
the likelihood of a road to flood, a bridge to fall or a route to
become  congested.  However,  these  likelihoods  are  never
discussed  in  quantitative  terms  (such  as  an  82%  probability
that a road will be flooded), but rather in qualitative language
such  as  “can’t  rely  on”  or  “a  flood  risk”  or  “we  think  is  not
going  to  survive.”  This  is  in  contrast  to  developments  in  the
CTP literature, which assume a numeric probability of failure is
available  for  each  graph  edge  (e.g.  Aksakalli  et  al.,  2016).
Furthermore,  practitioners  seem  to  operationalize  knowledge
of the likelihood of a road to flood by labeling it as closed when
it is only “likely” to be closed or significantly delayed. This too
is in contrast to the CTP literature, in which an edge is only
classified as blocked if someone has observed the blockage from
one of the edge’s endpoints. Finally, a “route-” or path-based
representation  is  also  different  from  the  CTP  literature  and
leads  to  different  planning  options  than  a  “road-”  or  edge-
based representation. In a road-based representation, the status
of multiple roads is understood so that optimal routes can be
identified. A route-based representation, however, significantly
limits  planning  options,  since  planners  appear  to  learn  and
“store” only the status of a handful of routes.

4.3  Goals for path planning: feasibility or optimization
The disaster  response routing  literature typically searches  for
the best, or optimal, path. This is true of models that seek to
minimize  travel  cost  or  time  to  one  destination  (e.g.  Eyerich
et al., 2010; Zhang et al., 2013) and also for those that seek to
minimize other objectives, such as the sum of priority-weighted
distances to multiple nodes (e.g. Akbari and Shiri, 2021).

According to our interviews, this is rarely a goal of response
organizations.  As  Table  4  shows,  only  three  organizations
appeared to be searching for the best path, and one of these was
discussing  a  hypothetical  situation.  Even  in  these  cases,  the
notion of “best”  or “better” was not the focus.  P1 explained
that once they found a path that worked, they would send all
their trucks along it until “that route was no longer good or if we

Table  4  Interviewee  reports  of  optimizing  versus  simply  identifying  a
feasible path

Goal

F2  F3  F4  S1  S2  S3  P1  P2  P3  P4  N1  N2  Tot

Optimize paths
Find a feasible path

✓    *

✓

✓   ✓   ✓   ✓   ✓   ✓   ✓

2
7

Note(s): *  indicates a discussion of a hypothetical practice
Source(s): Authors’ own work

got a better route”, but there was no indication that they were
actually searching for a better path nor what “better” means. S1
similarly  mentioned  a  “best  route,”  but  the  core  of  the
discussion  was  about  finding  a  feasible,  not  better,  path.  S2
discussed  a  hypothetical  idea  to  maintain  maps  that  are
automatically  updated  with  path  status  and  asset  locations
which could support finding “the fastest” path based on traffic
conditions. In contrast, seven of the 12 organizations implied
that their goal was simply to identify a workable – or feasible –
path.  They  described  many  challenges  with  finding  places
where large vehicles could transit, or turn around if necessary,
and identifying roads that were open. They did not mention the
concept of “best” or “better” nor discuss improving paths once
a  feasible  path  had  been  identified  (except  in  the  rare  cases
mentioned earlier).

In summary, then, it appears that response organizations do
not typically think about optimizing or improving their paths.
Their  focus,  instead,  is  on  identifying  a  feasible  path.  Few
mentioned any need to speed up the delivery of aid once it had
been  enabled  at  all.  This  conceptualization  lends  itself  more
naturally to formulations that prioritize path reliability, similar
to  the  most  reliable  path  subproblem  in  the  location  routing
model in Ukkusuri and Yushimito (2008) for example, rather
than the travel cost or time minimization objectives common in
CTP variants. However, it can be observed that CTP solution
approaches  which  plan  a  full  path  and  follow  it  until  a
discovered disruption necessitates re-planning, as opposed to
planning one-step-at-a-time the next node to visit, are already
implicitly  accounting  for  path  reliability.  Those  approaches
typically use an approximation of expected cost to destination to
select a path, where that approximation is based on edge failure
probabilities and travel times (e.g. Shiri and Salman, 2017).

4.4  Information sources for planning
Given  a  required  load  and  delivery  location,  the  information
relevant for planning paths includes the status and travel times
of  graph  edges.  The  literature  does  not  concern  itself  much
with where the relevant data comes from, but simply assumes
that  it  either  is  or  is  not  available.  For  example,  in  the  CTP
literature, travel times are known for all edges and the statuses
of graph edges are initially not available, but become available
once  edge  endpoints  are  visited  and  the  edges  are,  thus,
observed  (e.g.  Papadimitriou  and  Yannakakis,  1991).  In
Stochastic CTP models, edge failure probabilities are available
for all uncertain edges (e.g. Blei and Kaelbling, 1999). In this
section, we explore where information for path planning comes
from, which will shed light on what data could be available for
use by path planning models in disasters and when it could be
available.

Interviewees described a wide variety of information sources
used in path planning and re-planning. Table 5 shows the types
of  information  sources  mentioned  by  each  respondent.  The

Downloaded from http://www.emerald.com/jhlscm/article-pdf/16/2/121/11452423/jhlscm-05-2023-0046en.pdf by guest on 15 April 2026

127

Online path planning

Journal of Humanitarian Logistics and Supply Chain Management

Jannatul Shefa, Ashlea Bennett Milburn and Erica Gralla

Volume 16 · Number 2 · 2026 · 121–135

Table 5  Information sources mentioned by interviewees

Source of info

F2  F3  F4  S1  S2  S3  P1  P2  P3  P4  N1  N2  Tot

Driver network
Maps
Scouts
Weather forecast
Public knowledge
DOT
Local entities
State entities
Private parties
Broadcast

✓  ✓

✓  ✓  ✓  ✓
✓

✓

✓

✓

✓  ✓  ✓  ✓
✓
✓  ✓

✓
✓

✓

✓
✓

✓

✓
✓

✓
✓  ✓
✓  ✓
✓

✓  3
5
2
2
2
5
3
5
3
2

Source(s): Authors’ own work

driver network is an important source of information, although
it was only discussed by three organizations. Drivers who are on
the  road,  regardless  of  their  involvement  in  emergency
response, share information on real-time road status. Drivers
communicate  with  one  another  via  their  radios,  sharing
information about both closed and open roads. For example,
one interviewee explained that when their organization tells a
driver that a route looks closed, the driver might say, “No, I just
talked to this guy [and] he told me that that route is open” [P1].
Another explained that the drivers were “hearing on their CB
radios  [. . .]  that  these  routes  are  no  longer  any  good”  [P2].
Information from the driver network, and information drivers
learn  simply  by  encountering  closures,  is  typically  relayed  to
their organization, so that the organization can re-plan for other
drivers  accordingly.  Scouts,  discussed  by  two  organizations,
serve  a  similar  function  of  relaying real-time  road status,  but
they are sent out purposely to assess the road condition before
deploying  trucks  on  that  path.  They  may  take  the  form  of  a
drone, a person or a team.

include

local  officials,

Other responding organizations are also important sources of
law
information.  Local  entities
enforcement, sheriffs and fire and rescue teams. Similarly, state
entities  include  state  officials,  troopers,  police,  the  highway
patrol, state-level highway officials and environmental officials.
The Department of Transportation is a particularly important
source of information, through its website, maps and deployed
representatives  and  liaison  officers,  who  update  information
about accessible roads to emergency responders. Private parties
such as commercial industries and transporters using the same
roads also collaborate to share information on road conditions.

Public  sources  are  also  essential  sources  of  information,
including maps, weather forecasts, broadcast radio or television
news, social media posts and other sources of public knowledge.
Few of these information sources were described as providing
information  on  the  “probability”  or  “likelihood”  that  a  road  is
open;  instead,  they  largely  provide  real-time  status  updates  on
whether  roads  are  open  or  closed.  In  the  three  cases  in  which
“likelihood”  information  was  used  (see  Table  2,  row  labeled
“ES2”), it came from either historical knowledge or preparedness
work,  such  as  examining  which  bridges  are  likely  to  fail  in  an
earthquake and which roads are likely to flood in a storm.

Organizations  do  not  all  rely  on  the  same  sources  of
information. Table 5 suggests that federal entities primarily rely
on official information from different tiers of organizations. All

128

state entities use maps while supplementing their information
with a variety of sources. Private entities in particular described
a large number and variety of information sources used for path
planning.

In the online path planning literature, road status information
sources other than driver-encountered disruptions are relevant
to  specific  variants  of  the  classic  CTP:  CTP-sensing  and
multiagent  CTP  models.  Information  from  other  responding
organizations,  public  sources  and  scouts  (drone,  person,  etc.)
can be modeled by CTP-sensing variants, where sensing costs
and  budgets  represent  the  costs  associated  with  retrieving
information from those sources and the resources available for
information-gathering efforts (Bnaya et al., 2009). Heterogenous
sensing  costs  that  depend  on  information  source  would  be  a
reasonable  and  practical  extension  to  the  literature.  Sensing
delays may also need to be introduced in models to capture time
required to collect and disseminate remotely sensed information.
Information from driver networks can be modeled by multiagent
CTP variants, where drivers send and receive information to and
from one another (e.g. Zhang et al., 2013).

4.5  Discovering the network status
The  disaster  response  routing  literature  makes  assumptions
about  how  the  network  status  is  discovered.  In  models  for
online  path  planning  along  disrupted  networks,  such  as  the
CTP, network status is initially unknown and is discovered as a
driver  traverses  the  network  and  encounters  roads  (e.g.
Papadimitriou  and  Yannakakis,  1991).  In  CTP  variants  that
allow for communication between drivers, an individual driver
may discover network status via their own observations and also
via communication of information discovered by other drivers
(e.g. Zhang et al., 2013). Other models, such as CTP-sensing,
allow for discovering the status of some network edges without
visiting them, sometimes at a sensing cost (Bnaya et al., 2009;
Zhang  et  al.,  2016).  Finally,  some  models  allow  for  network
status discovery through Bayesian inference, where a driver can
infer the status of an unvisited road based on observations of
correlated roads (Lim et al., 2017).

All papers reviewed in the prior paragraph provide models in
which  drivers  are  not  intentionally  trying  to  learn  about  the
network status; rather, they are simply driving along planned
paths and  they  learn  the  status  of  included  roads as  they  are
encountered. In contrast, one might characterize the model in
Zhang et al. (2015) as intentional exploration of a network to
find  a  fast  and  unblocked  path  to  destination.  Though  the
authors do not frame their model in exactly that light, the idea is
to determine a set of multiple short and dissimilar vehicle paths
between a shared origin and destination that enable at least one
vehicle to reach the destination quickly. A similar formulation is
the  k-Canadian  Travelers  Problem  with  communication,
where  k  drivers  sharing  an  origin  and  destination  share
discovered  information  with  one  another  as  the  network  is
traversed,  and  the  shared  information  can  be  used  to  replan
when blockages are encountered (Zhang et al., 2013).

In  practice,  a  wide  variety  of  the  above  methods  enable
discovery  of  the  network  status.  Table  6  shows  the  different
types of network discovery approaches identified in the data. By
far the most common is through communication with another
entity, usually either a driver or an organization that aggregates

Downloaded from http://www.emerald.com/jhlscm/article-pdf/16/2/121/11452423/jhlscm-05-2023-0046en.pdf by guest on 15 April 2026

Online path planning

Journal of Humanitarian Logistics and Supply Chain Management

Jannatul Shefa, Ashlea Bennett Milburn and Erica Gralla

Volume 16 · Number 2 · 2026 · 121–135

Table 6  Interviewee reports of learning about the network status

Discovering network status. . .

F2

F3

F4

S1

S2

S3

P1

P2

P3

P4  N1  N2

Tot

By exploring, unintentionally
By exploring, intentionally
Through communication
By sensing at a distance (e.g. . . .)
By inferring based on other information (e.g. history, road type, etc.)

Note(s): *indicates a discussion of a hypothetical practice
Source(s): Authors’ own work

information like DOT or FEMA (see subsection 4.6). Ten of
the 12 organizations mentioned this discovery method.

The  next-most-common  approach (described  by six  of  the
12  organizations)  was  to  learn  from  drivers  who  encounter
closed  roads:  we  term  this  “unintentional  exploration.”  For
example, as an interviewee from P1 described, “you’re coming
down a country road, you’re turning left and [. . .] then you get
to a road closure that was not on the map.” We distinguish this
unintentional  exploration  from  “intentional  exploration,”  in
which an organization sends someone (such as a police officer
or  a  member  of  an  advance  team)  to  drive  the  network  in  a
deliberate attempt to discover the status of roads. Only one of
the 12 organizations described such an approach.

Inferring  road  status  based  on  other  information  was
described by only three organizations. Interviewees described
making assumptions about “which bridge do we think [is] not
going  to  survive”  [F4]  or  to  “close  this  area  off  because  this
[road]  has  a  history  of  flooding”  [P2].  In  all  cases,  the
inferences were based on knowledge of a road’s infrastructure
or history, such as whether it contains bridges or has flooded in
the past.

Learning road status by sensing it at a distance was described
by only three organizations, but was also mentioned by three
additional  organizations  as  a  strategy  they  would  like  to  use.
Many  different  methods  of  sensing  were  mentioned.  Those
already using this strategy described a “social media monitor”
looking for things like “hashtag I-35 is closed” [F3] and visual
imagery  from  aerial  vehicles  [P1  and  S1].  Those  discussing
hypothetical  ideas  talked  about  live  tracking  for  assets  and
infrastructure  status,  informed  by  artificial  intelligence  and
mapping technologies.

In  sum, most  organizations  discover  the  status  of  the  road
network in ad hoc ways: primarily either as a driver explores the
network  or  through  information  communicated  by  other
entities,  discussed  further  in  subsection  4.6.  The  former  is
consistent  with  CTP  models  in  the  literature  that  assume  a
single driver on the network; the latter is consistent with CTP
models  that  assume  multiple  drivers  on  the  network  sharing
information with one another (e.g. Zhang et al., 2013; Shiri and
Salman, 2017). Very few organizations currently leverage the
sensor  capabilities  assumed  in  the  CTP-sensing  model  or
inference  to  estimate  the  network  status  as  assumed  in  the
Bayesian  CTP  (Bnaya  et  al.,  2009;  Zhang  et  al.,  2016;  Lim
et al., 2017).

4.6  Knowledge sharing
In online path planning models in the disaster relief distribution
transportation  literature,  edge  information  is  discovered  as  a

✓  ✓  ✓  ✓
✓

✓

✓  ✓  ✓  ✓  ✓  ✓  ✓  ✓  ✓
✓

✓

✓

*

*

*

✓  ✓

✓

✓

✓

6
1
10
3
3

graph  is  traversed.  For  models  that  include  more  than  one
agent (i.e. driver) moving along the graph, how information is
shared among those agents is addressed. For example, in Berg'e
et  al.  (2019),  agents  communicate  with  one  another  during
planning only at the source node. Zhang et al. (2013) introduce
a multiagent CTP variant with two communication levels – full
communication, in which RS-type agents both receive and send
information as they traverse a graph, and limited communication,
in which R-type agents can only Receive information. Shiri and
Salman  (2017)  introduce  three  communication  protocols  for
RS-type  agents,  which  differentiate  between  only  sharing
discovered  edge  blockages  (CP1),  additionally  sharing  travel
information, which implies traversed edges are confirmed to be
available (CP2) and making decisions for (i.e. planning paths
for)  R-type  agents  (CP3).  Shiri  and  Salman  (2017)  also
differentiate between three intelligence levels, in which an agent
can  only  make  a  decision  about  their  own  next  travel  move
(IL1),  can  plan  their  own  full  path  (IL2)  and  can  plan  and
transmit  another  agent’s  full  path  (IL3).  In  all  of  the  papers
reviewed in this paragraph, any communication that is allowed
is  assumed  to  happen  instantaneously,  as  soon  as  an  agent
reaches an edge endpoint to discover its status. It is implied that
all  information  shared  “out”  or  “up”  by  agents  capable  of
transmitting information is maintained in a central repository
that describes what is globally known about the status of graph
edges  at  any  point  in  time.  In  this  framework,  disruptions
discovered  locally  by  R-type  agents  (who  are  unable  to  send
information)  will  not  be  globally  known.  Lita  et  al.  (2001)
introduces a multiagent, multidestination CTP variant where
information agents, who are trying to reach a destination, send
collected  information  to  a  central  planner,  referred  to  as  a
dispatcher  agent.  The  dispatcher  agent  considers  the  global
repository  of  discovered  information  to  update  plans  and
transmit them to information agents.

As  online  path  planning  models  with  multiple  agents  is  a
developing area in the disaster response literature, this section
is framed in a way to provide insights to model development
from the practitioner perspective.

One  important  question  is  whether  there  is  a  formal
knowledge  repository  and  whether  it  is  maintained  by  an
organization or shared across multiple organizations. The first
two  rows  of  Table  7  summarize  the  results.  Only  one  of  the
interviews describes a formal “common operating picture:” a
map or other information repository that captures information
from many sources about road and infrastructure status. This is
managed  at  the  federal  level  by  the  situational  awareness
branch  [F4],  and  includes  information  from  commercial
providers, states, law enforcement and other sources. However,

Downloaded from http://www.emerald.com/jhlscm/article-pdf/16/2/121/11452423/jhlscm-05-2023-0046en.pdf by guest on 15 April 2026

129

Online path planning

Journal of Humanitarian Logistics and Supply Chain Management

Jannatul Shefa, Ashlea Bennett Milburn and Erica Gralla

Volume 16 · Number 2 · 2026 · 121–135

Table 7  Interviewee reports about road status knowledge repositories

Knowledge repository/update type

F2

F3

F4

S1

S2

S3

P1

P2

P3

P4

N1

Inter-org knowledge
Within org knowledge
Ad hoc updates
Regular updates
Person available
Digital knowledge updates

Source(s): Authors’ own work

✓
✓

✓
✓

✓

✓

✓

✓

✓
✓

✓
✓

✓

✓
✓
✓

✓

N2

✓

Tot

5
3
5
2
3
0

some  evidence  suggests  that  this
knowledge is often too far from the action to be up to date.

federally  maintained

Most of the other interviewees refer informally to knowledge
of road or route status but do not describe any formal repository
in which it is maintained. The two private organizations seem
to  store  and  update  this  information  internally;  for  example,
one interviewee states, “You try to keep an accurate as possible
go  no  go  route,”  [P2]  implying  it  has  an  internal  knowledge
repository, but does not describe how this is accomplished nor
what form it takes. More often, organizations seem to update a
repository  maintained  by  another  organization.  For  example,
the same private organization also describes learning from the
Department  of  Transportation,  drivers  and  state  troopers
about  the  status  of  roads,  and  then  “call  and  tell  [FEMA]
headquarters”  [P2].  Other  interviewees  describe  a  similar
process of updating another organization’s knowledge, but the
repository  is  maintained  by  a  state  entity  [S1]  or  law
enforcement [S3] or a transportation company [N2].

Thus,

it  appears

that  significant

inter-organizational
coordination  takes  place  regarding  a  “common  operating
picture,” but that the process is not systematic nor consistent
across organizations and disasters. There is no single knowledge
repository  that  is  updated  or  used  by  these  organizations,
despite  the  interviews’  focus  on  a  single  geographic  area  and
disaster.  A  federal  entity  maintains  a  central  knowledge
repository, but it is far from the action and may not always be up
to date, and it does not appear that the private organizations,
who  do  much  of  the  path  planning,  rely  heavily  on  it.
Furthermore,  there  is  no  evidence  of  any  kind  of  easily
shareable, digital representation of road status knowledge.

A related question is whether there is a systematic process for
sharing  and  updating  information.  The  last  four  rows  of
Table 7 summarize these results. Many organizations appear to
generate  or  request  updates  in  an  ad  hoc  manner,  driven  by
newly acquired information or an arising need for information.
For example, one interviewee explained, “if my driver calls in
and says this road is a no go road, and I call it in higher” [P2].
Another  noted  that  they  might  be  “looking  at  a  map  and
saying” “it doesn’t look like that’s open” but [someone might
say] “no, I just talked to this guy. And you know, he told me
that that route is open”” [P1]. In many cases, information does
not flow as quickly as it could, because the organizations with
information to share may have “a hundred other battles they’re
trying to work with” [P2]. There was, on the other hand, very
little evidence of regularly scheduled calls or meetings to update
information. Only two organizations described something close
to such a process: the federal entity maintaining the “common
operating  picture”  described  a  goal  of  learning  from  all

knowledgeable  entities  but  did  not  describe  a  systematic
process  for  doing  so  [F4],  and  a  state  entity  mentioned  a
weather forecast authority “feeding us” information, but again
did  not  describe  the  process  itself  [S3].  A  slightly  more
common,  but  still  uncommon,  arrangement  was  a  person
located  within  or  near  the  organization  who  had  access  to
updated knowledge. For example, one organization mentioned
“a  representative  from  the  Department  of  Transportation
sitting here monitoring all the routes and telling us what’s really
open and closed” [F4]. No organizations mentioned any kind
of digital knowledge updates, such as logging into a mapping
tool like Waze or updating a GIS map.

Thus, there is clear evidence of ad hoc knowledge sharing via
calls, particularly driven by the acquisition of new information
or a new need for information. However, new information is
not always shared immediately when acquired, but may only be
shared  when  a  request  is  made.  The  private  and  nonprofit
organizations,  in  particular,  appear  to  rely  on  this  type  of
process.  Outside  of  this  ad  hoc  process,  there  is  almost  no
evidence  of  a  systematic  process  such  as  regularly  scheduled
updates or a digital tool for information sharing. The federal
and state organizations appear to aspire to such a process but
did not  provide  details.  Since  the  private  organizations  make
many of the routing decisions (as discussed above), it appears
that the ad hoc process drives the information available to path
planners.

In summary, information sharing in practice does not seem
to be as thorough as multiagent online path planning models
assume. That is, there is evidence of some edge blockages being
shared ad hoc, but there are not systems in place to ensure every
discovered  blockage  is  communicated  to  all  graph  users  nor
stored in a central repository for all graph users to access. This
mimics  the  partial  communication  scenario  in  Zhang  et  al.
(2013) where not all agents traversing the network are able to
transmit discovered information. Furthermore, the sharing of
new
the  graph  does  not  happen
instantaneously  as  multiple  models  assume  (e.g.  Lita  et  al.,
2001; Zhang et al., 2013; Shiri and Salman, 2017). Instead, a
series of delays impact information sharing, as the driver must
relay  the  information,  it  must  be  updated  to  a  central
repository, and then another graph user eventually accesses the
information.

information  about

5.  Implications for research and practice

This  section  considers  the  implications  of  key  observations
comparing  path  planning  practices  at  FSAs  to  modeling  for
online  path  planning  on  uncertain  road  networks.  Section  4

Downloaded from http://www.emerald.com/jhlscm/article-pdf/16/2/121/11452423/jhlscm-05-2023-0046en.pdf by guest on 15 April 2026

130

Online path planning

Journal of Humanitarian Logistics and Supply Chain Management

Jannatul Shefa, Ashlea Bennett Milburn and Erica Gralla

Volume 16 · Number 2 · 2026 · 121–135

developed these observations. To summarize, first, while most
CTP models assume the driver does their own path planning,
our  evidence  shows  that  a  central  authority  within  each
organization typically plans paths (4.1). Second, while research
and  practice  both  represent  the  transportation  network  by
labeling  roads  as  blocked,  open  or  unknown,  they  represent
uncertainty  in  very  different  terms  (4.2).  Third,  researchers
typically  seek  the  fastest  feasible  paths,  while  response
organizations typically seek feasible and/or reliable paths (4.3).
Fourth,  the  information  sources  used  in  practice  vary  widely,
and  researchers  have  modeled  many  of  them  (4.4).  Fifth,
models have captured multiple ways that response organizations
discover  the  status  of  the  transportation  network,  as  well  as
some  methods  that  are  not  used  in  practice  (4.5).  Sixth,
information sharing in practice is ad hoc, whereas models tend to
assume  information  is  shared  thoroughly  and  instantaneously
(4.6). Based on these gaps, the following discussion elucidates
both how models can better meet practitioners where they are
and opportunities for practice to leverage modeling advances.

on

path

planning

centralization

5.1  Network status
For  researchers,  our  findings  suggest  a  need  for  changes  in
assumptions
and
communication.  State  of  the  practice  does  not  support  that
algorithms for planning would be adopted at the driver level, via
onboard computing systems available in the vehicle. Rather, it
is more likely that any algorithm for planning would be used by
a  central  planner  in  the  driver’s  organization.  Therefore,
researchers  should  assume  centralized  planning  by  each
organization, not by spatially distributed drivers nor across the
entire  multiorganization  response.  In  addition,  our  findings
suggest that communication between the driver and planner is
reliable but basic (i.e. voice-based). While the disaster response
literature establishes the unreliability of some communication
channels during a response, such as cellular and wi-fi (e.g. Ali
et  al.,  2015),  our  data  show  that  the  use  of  more  primitive
technologies  such  as  CB  radio  fill  the  communication  gap.
Therefore,  algorithms  should  not  assume  rich  technical
communication between drivers and central planners.

For researchers, our findings highlight the partial or delayed
sharing of network information in practice. CTP variants either
use  a  driver-as-planner  framework  that  does  not  require
communication at all, as in the single agent models, or make
assumptions  regarding  communication  that  are  unrealistic
when  compared  with  current  practice,  as  is  the  case  with
multiple agent model variants. Regardless of where the degree
of communication in a multiple agent CTP model falls on the
limited-to-full spectrum, the communication that does occur is
assumed  to  be  instantaneous.  That  is,  a  driver  transmits
information regarding a failed edge as soon as they arrive at an
endpoint of the edge, and that information becomes available
to other drivers as soon as they have a need to replan. Some
models additionally assume information for edges confirmed to
be available is also communicated with this level of immediacy.
In reality, there are delays associated with a driver calling in a
failure to a central planner. And, not all drivers on the network
have  access  to  the  knowledge  newly  acquired  by  the  central
planner, especially if they are part of a different organization.
Whether drivers from a second organization can benefit from
the new knowledge depends on:

•  hearing it directly in channels among driver networks (e.g.

•

CB radios) and calling it in to their own planner; or
the  knowledge  is  conveyed  by  the  first  organization  to  a
higher-level  authority,  e.g.  the  state  DOT,  and  that
authority disseminates the information back out in a way
the planner at the second organization can access it.

To more closely resemble practice, researchers should model
this  partial  sharing  of  information  more  explicitly  in  CTP
variants, and should also introduce delays for diffusion of new
road status  knowledge.  Models  such  as  CTP-Sensing  should
also  be  further  developed  to  account  for  new  road  status
knowledge being made available over time from sources other
than driver updates alone, such as from drone surveillance and
news reports.

For  practitioners,  our  findings  demonstrate  the  need  for  a
common  operating  picture  of  network  information.  To
facilitate  faster  and  more  complete  diffusion  of  road  status
updates to all network users, systems and processes governing
the formation of a common operating picture for road status are
required.  Furthermore,  any  adoption  of  planning  algorithms
from  the  literature  would  require  reliable  communication  of
such information between the driver and the planner – for the
driver to send road status updates to the planner, and for the
planner  to  send  path  updates  to  the  driver.  The  disaster
management literature has long recognized the need for real-
time communication and shared collections of data available to
all organizations operating in response (Mendonca et al., 2000;
Lettieri et al., 2009). Relational databases could be used to link
the road status information available to various organizations
(Lettieri et al., 2009). A visual representation of the collected
data, for example, in a geographic information system (GIS),
would  be  especially  useful  (Mendonca  et  al.,  2000).  Current
GIS  systems  (e.g.  Google  Maps)  do  provide  a  “sunny-day”
snapshot of road infrastructure in an area. What is missing from
these systems is layers describing edge failure probabilities and
up-to-date  road  status  information,  shared  across  all  system
users. Furthermore, if the road attribute layers are to be used in
a central path planning algorithm, the GIS and any planning
algorithms should be interoperable.

that

5.2  Stochastic information pertaining to network status
For researchers, our findings demonstrate a need for alternative
models  of  uncertainty  in  network  edge  status.  Much  of  the
CTP literature focuses on the development of stochastic rather
the
than  deterministic  models  and  demonstrates
consideration of edge failure probabilities improves travel cost,
i.e.  reduces  the  time  required  for  a  driver  to  reach  their
destination. For example, the best stochastic policy in Eyerich
et al. (2010) outperforms the deterministic policy included in
the  paper  by  17%  to  20%  for  test  instances  in  their
computational study.  In contrast to the online path planning
literature, our evidence shows that current planning practice is
deterministic  in  most  cases;  the  exceptions  are  when  an
organization considers failure likelihoods for only some edges,
and further, completely excludes those “possible-to-fail” roads
from planned paths. No models in the literature capture this
particular  treatment  of  stochastic  information,  where  edge
probabilities are only available for some edges, and edges which
can  fail  are  assumed  to  be  failed  until  proven  otherwise.

Downloaded from http://www.emerald.com/jhlscm/article-pdf/16/2/121/11452423/jhlscm-05-2023-0046en.pdf by guest on 15 April 2026

131

Online path planning

Journal of Humanitarian Logistics and Supply Chain Management

Jannatul Shefa, Ashlea Bennett Milburn and Erica Gralla

Volume 16 · Number 2 · 2026 · 121–135

to

Development of such models would allow for a comparison of
stochastic  models.
current  practice
state-of-the-art
Probabilistic  approaches  show  potential,
though  more
evaluation on real-world case studies is needed.
For  practice,  our  findings  suggest  the

importance  of
integrating  probabilistic  data  for  network  edges  into  GIS
systems. Stochastic models require failure probabilities for all
edges that are subject to failure. Practice suggests that failure
probabilities are only available for some edges, and may not be
precisely quantified. That is, rather than describing an edge as
having an 82% chance of failure, edges might be described as
having a history of flooding. Realizing the potential benefits of
existing  stochastic  models  will  require  quantifying  uncertain
edge inputs, such as measuring a road’s propensity for flooding
or a bridge’s likelihood of falling on a continuous [0,1] scale.
Data are available to support numerical modeling efforts, such
as the general condition data in the National Bridge Inventory
and inundation predictions from the Super-Fast INundation of
CoastS  compound  flooding  model  (U.S.  Department  of
Transportation (USDOT), 2008; Leijnse et al., 2021). As the
work  of  integrating  these  probabilistic  data  into  shared  GIS
systems is time-intensive, the integration should be completed
pre-disaster if the data is to be leveraged in a response.

5.3  Goals for path planning
For  researchers,  our  findings  suggest  the  need  to  model
responders’  reliability  goals  for  planned  paths.  The  results
presented  in  this  paper  indicate  that  planners  currently
prioritize  path  reliability  over  travel  cost  or  time.  Existing
stochastic  models  for  CTP  indirectly  address  reliability  with
their  minimization  of  expected  travel  cost.  This  objective
function will bias against selection of paths that include edges
with  high probabilities  of  failure,  as  any  encountered  failures
require  some  backtracking  (and,  thus,  increased  travel)  on
behalf of the driver. However, the focus in practice on reliability
suggests  online  path  planning  models  should  treat  reliability
more explicitly in future research.

in  other  countries,  or

5.4  Limitations
This study’s primary limitation stems from our focus on a single
set of organizations encountering the CTP-like problem in the
context of FSAs for hurricanes in the USA. It is possible that
responders
international
humanitarian community, approach this problem differently or
have different goals, tools or capacities. Future work could use
similar  methods  to  explore  how  practitioners  in  different
settings  approach  the  same  problem,  or  examine  different
logistics  problems  within  the  broader  humanitarian  logistics
space.

in  the

6.  Conclusions

The  differences  between  the  practices  at  FSAs  and  the
assumptions  in  online  path  planning  models  explain  why
practice  has  not  been  able  to  leverage  the  relevant  research.
First, the models assume information is available which is not
actually  available.  For  example,  there  are  no  edge  failure
probabilities available from the start of the response. Moreover,
there do not appear to be formal (e.g. digitized) repositories of
edge  status  information  at  all,  which  would  be  necessary  to

132

provide  inputs  to  any  of  the  path  planning  models.  Second,
models often assume a planning scenario that does not match
that  of  practice.  That  is,  most  models  assume  the  driver
independently plans and re-plans their own paths, which was
never  the  case  in  the  organizations  with  whom  we  spoke.
Instead, authorities within each organization plan paths for the
drivers and support any required re-planning. Third, the goals
of disaster responders appear different from those represented
in models: they do not appear to seek improvements but rather
to identify a reliable path.

To better leverage the advances of research, practice could
adopt  processes  and  technologies  for  sharing  real-time  road
status  information  and  incorporate  edge  failure  probabilities
from  preparedness  efforts  in  those  systems.  Currently,  while
road  status  information  is  shared,  it  is  done  in  an  ad  hoc
manner, and does not appear to be maintained in a database or
system  which  could  provide  the  data  needed  to  leverage
modeling advances.

To  enable  adoption  of  innovations  in  practice,  researchers
could  model
information  diffusion  delays  and  evaluate
alternative treatments of reliability and stochastic  edge status
information. Such adaptations could bring research into better
alignment with the constraints and goals of disaster response
practitioners.  Research  must  acknowledge  and  adapt  to  the
limitations of data availability, communication and the human
and technological capacity to run sophisticated models during a
disaster response, and ensure that models align with the goals of
response planners in focusing on reliability before speed.

While  this  investigation  focused  on  a  narrowly  defined
situation  –  path  planning  from  a  staging  area  to  a  final
destination during a disaster response – the conclusions may be
more  broadly  applicable.  Disaster  response  logistics  is  often
plagued  by  uncertainty  about  infrastructure,  supply  and
demand, such that planning must be updated continuously as
information  evolves.  Practitioners  often  lack  systems  for
collecting,  maintaining  and  sharing  data  in  real  time,  which
inhibits not only the response but also the potential to leverage
decision  support  tools  based  on  optimization  or  artificial
intelligence.  Thus,  in  a  wide  variety  of  disaster  response
logistics  problems,  researchers  should  be  cautious  to  ensure
that models align with practice goals and work within data and
limitations  –  or  demonstrate  the  potential
technology
improvements  from  making  an  investment  in  easing  these
limitations.  Better  alignment  between  practice  and  research
could lead to significant improvements in response speed and
effectiveness, easing the suffering of those affected by disasters.

References

Akbari, V. and Shiri, D. (2021), “Weighted online minimum
latency problem with edge uncertainty”, European Journal of
Operational Research, Vol. 295 No. 1, pp. 51-65.

Aksakalli, V., Sahin, O.F. and Ari, I. (2016), “An AO*  based
exact  algorithm  for  the  Canadian  traveler  problem”,
INFORMS Journal on Computing, Vol. 28 No. 1, pp. 96-111.
Ali,  K.,  Nguyen,  H.X.,  Vien,  Q.T.  and  Shah,  P.  (2015),
“Disaster management communication networks: challenges
and architecture design”, 2015 IEEE International Conference
on  Pervasive  Computing  and  Communication  Workshops
(PerCom Workshops), IEEE, pp. 537-542.

Downloaded from http://www.emerald.com/jhlscm/article-pdf/16/2/121/11452423/jhlscm-05-2023-0046en.pdf by guest on 15 April 2026

Online path planning

Journal of Humanitarian Logistics and Supply Chain Management

Jannatul Shefa, Ashlea Bennett Milburn and Erica Gralla

Volume 16 · Number 2 · 2026 · 121–135

Alseth,  A.  (2020),  “‘-CTP:  Utilizing  multiple  agents  to  find
efficient routes in disrupted networks”, (MS thesis, University
of Arkansas).

Bai, A., Wu, F. and Chen, X. (2018), “Posterior sampling for
Monte  Carlo  planning  under  uncertainty”,  Applied
Intelligence, Vol. 48 No. 12, pp. 4998-5018.

Bender, M. and Westphal, S. (2015), “An optimal randomized
online  algorithm  for  the  k-Canadian  traveller  problem  on
node-disjoint paths”, Journal of Combinatorial Optimization,
Vol. 30 No. 1, pp. 87-96.

Berg'e,  P.  and  Salaün,  L.  (2019),  “Improved  deterministic
strategy for the Canadian traveller problem exploiting small
max-(s, t)-cuts”, International Workshop on Approximation
and  Online  Algorithms,  Springer  International  Publishing:
Cham, pp. 29-42.

Berg'e, P., Desmarchelier, J., Guo, W., Lefebvre, A., Rimmel, A.
and  Tomasik,  J.  (2019),  “Multiple  Canadians  on  the  road:
minimizing  the  distance  competitive  ratio”,  Journal  of
Combinatorial Optimization, Vol. 38 No. 4, pp. 1086-1100.
Besiou, M. and Van Wassenhove, L.N. (2020), “Humanitarian
operations: a world of opportunity for relevant and impactful
research”, Manufacturing & Service Operations Management,
Vol. 22 No. 1, pp. 135-145, doi: 10.1287/msom.2019.0799.
Blei,  D.M.  and  Kaelbling,  L.P.  (1999),  “Shortest  paths  in  a
dynamic uncertain domain”, In IJCAI Workshop on Adaptive
Spatial Representations of Dynamic Environments, Vol. 4, p. 2.
Bnaya, Z.,  Felner,  A.  and Shimony, S.E. (2009), “Canadian
IJCAI,

remote  sensing”,

In

traveler  problem  with
pp. 437-442.

Caunhye,  A.M.,  Nie,  X.  and  Pokharel,  S.  (2012),
“Optimization  models  in  emergency  logistics:  a  literature
review”,  Socio-Economic  Planning  Sciences,  Vol.  46  No.  1,
pp. 4-13, doi: 10.1016/j.seps.2011.04.004.

Chanchad, N. (2023), “Efficient routing for disaster scenarios
in  uncertain  networks:  a  computational  study  of  adaptive
algorithms for the stochastic Canadian traveler problem with
multiple  agents  and  destinations”,  (Doctoral  dissertation,
University of Arkansas).

Corbin, J. and Strauss, A. (2008), Basics of Qualitative Research:
Techniques  and  Procedures  for  Developing  Grounded  Theory,
Third Edit. ed Sage, Thousand Oaks, CA.

Corbett, C.J. and Van Wassenhove, L.N. (1993), “The natural
drift:  what  happened  to  operations  research?”,  Operations
Research,  Vol.  41  No.  4,  pp.  625-640,  doi:  10.1287/
opre.41.4.625.

Day,  J.M.,  Melnyk,  S.A.,  Larson,  P.D.,  Davis,  E.W.  and
Whybark,  D.C.  (2012),  “Humanitarian  and  disaster  relief
supply chains: a matter of life and death”, Journal of Supply
Chain Management, Vol. 48 No. 2, pp. 21-36, doi: 10.1111/
j.1745-493X.2012.03267.x.

De  la  Torre,  L.E.,  Dolinskaya,  I.S.  and  Smilowitz,  K.R.
(2012),  “Disaster  relief  routing:  integrating  research  and
practice”,  Socio-Economic  Planning  Sciences,  Vol.  46  No.  1,
pp. 88-97, doi: 10.1016/j.seps.2011.06.001.

De Boeck, K., Besiou, M., Decouttere, C., Rafter, S., Vandaele,
N.,  Van  Wassenhove,  L.N.  and  Yadav,  P.  (2023),  “Data,
analytical techniques and collaboration between researchers
and  practitioners  in  humanitarian  health  supply  chains:  a
forward”,  Journal  of
challenging  but  necessary  way

Humanitarian Logistics and Supply Chain Management, Vol. 13
No. 3, pp. 237-248, doi: 10.1108/JHLSCM-07-2022-0078.
Demaine,  E.D.,  Huang,  Y.,  Liao,  C.S.  and  Sadakane,  K.
(2014), “Canadians should travel randomly”, International
Colloquium  on  Automata,  Languages,  and  Programming,
Springer  Berlin  Heidelberg:  Berlin,  Heidelberg,
(pp. 380-391).

Demaine,  E.D.,  Huang,  Y.,  Liao,  C.S.  and  Sadakane,  K.
(2021),  “Approximating  the  Canadian  traveller  problem
with  online  randomization”,  Algorithmica,  Vol.  83  No.  5,
pp. 1524-1543.

Eyerich, P., Keller, T. and Helmert, M. (2010), “High-quality
policies for the Canadian traveler’s problem”, In Proceedings
of the AAAI Conference on Artificial Intelligence, Vol. 24, No. 1,
pp. 51-58.

Federal  Emergency  Management  Agency  (FEMA)  (2019),
“Region  X  logistics  branch  briefing:  request  to  establish
FEMA staging area at Bremerton national airport”, available
www.portofbremerton.org/media/dynamic/files/
at:
765_Info_Item_1-BNA_ISB_Briefing.pdf  (accessed  7  June
2024).

Federal  Emergency  Management  Agency  (FEMA)  (2020),
“Preliminary damage  assessment  guide.  Technical report”,
at:  www.fema.gov/sites/default/files/2020-07/
available
fema_preliminary-disaster-assessment_guide.pdf  (accessed
7 June 2024).

Federal  Emergency  Management  Agency  (FEMA)  (2022),
“Distribution  management  plan  guide  2.0”,  available  at:
www.fema.gov/sites/default/files/documents/
fema_distribution-management-plan-guide-2.0.pdf (accessed
7 June 2024).

Fried,  D.,  Shimony,  S.E.,  Benbassat,  A.  and  Wenner,  C.
traveler  problem

(2013),  “Complexity  of  Canadian
variants”, Theoretical Computer Science, Vol. 487, pp. 1-16.
Gralla, E. and Goentzel, J. (2018), “Humanitarian transportation
planning:  evaluation  of  practice-based  heuristics  and
recommendations  for  improvement”,  European  Journal  of
Operational  Research,  Vol.  269  No.  2,  pp.  436-450,  doi:
10.1016/j.ejor.2018.02.012.

Guo,  H.  and  Barfoot,  T.D.  (2019),  “The  robust  Canadian
traveler problem applied to robot routing”, 2019 International
Conference  on  Robotics  and  Automation  (ICRA),  IEEE,
pp. 5523-5529.

Gutjahr,  W.J.  and  Nolz,  P.C.  (2016),  “Multicriteria
optimization  in  humanitarian  aid”,  European  Journal  of
Operational  Research,  Vol.  252  No.  2,  pp.  351-366,  doi:
10.1016/j.ejor.2015.12.035.

Haghani, A. and Oh, S.C. (1996), “Formulation and solution
of a multi-commodity, multi-modal network flow model for
disaster  relief  operations”,  Transportation  Research  Part  A:
Policy and Practice, Vol. 30 No. 3, pp. 231-250.

Holguín-Veras, J., Jaller, M., Van Wassenhove, L.N., P'erez, N.
and  Wachtendorf,  T.  (2012),  “On  the  unique  features  of
post-disaster  humanitarian  logistics”,  Journal  of  Operations
Management, Vol. 30 Nos 7/8, pp. 494-506.

IFRC  (2013),  “World  disasters  report:  focus  on  technology
and  the  future  of  humanitarian  action.  International
federation of red cross and red crescent societies”, available
at: www.ifrc.org/en/publications-and-reports/world-
disasters-report/world-disasters-report-2013/

Downloaded from http://www.emerald.com/jhlscm/article-pdf/16/2/121/11452423/jhlscm-05-2023-0046en.pdf by guest on 15 April 2026

133

Online path planning

Journal of Humanitarian Logistics and Supply Chain Management

Jannatul Shefa, Ashlea Bennett Milburn and Erica Gralla

Volume 16 · Number 2 · 2026 · 121–135

Institute  for  Economics  &  Peace.  Ecological  Threat  Register
(2020),  “Understanding  ecological  threats,  resilience  and
peace”,  Sydney,  September  2020,  available  at:  http://
visionofhumanity.org/reports (accessed 7 June 2024).

Knott,  R.  (1987),  “The  logistics  of  bulk  relief  supplies”,

Disasters, Vol. 11 No. 2, pp. 113-115.

quality

Kovacs, G. and Moshtari, M. (2019), “A roadmap for higher
a
research
methodological perspective”, European Journal of Operational
Research,  Vol.  276  No.  2,  pp.  395-408,  doi:  10.1016/j.
ejor.2018.07.052.

humanitarian

operations:

in

Kunz, N., Van Wassenhove, L.N., Besiou, M., Hambye, C. and
Kov'acs,  G.  (2017),  “Relevance  of  humanitarian  logistics
research: best practices and way forward”, International Journal
of  Operations  &  Production  Management,  Vol.  37  No.  11,
pp. 1585-1599, doi: 10.1108/IJOPM-04-2016-0202.

Leijnse, T., van Ormondt, M., Nederhoff, K. and van Dongeren,
A.  (2021),  “Modeling  compound  flooding  in  coastal  systems
using  a  computationally  efficient  reduced-physics  solver:
including  fluvial,  pluvial,
tidal,  wind-and  wave-driven
processes”, Coastal Engineering, Vol. 163, p. 103796.

Lettieri,  E.,  Masella,  C.  and  Radaelli,  G.  (2009),  “Disaster
management:  findings  from  a  systematic  review”,  Disaster
Prevention and Management: An International Journal, Vol. 18
No. 2, pp. 117-136, doi: 10.1108/09653560910953207.
Lewin,  R.,  Besiou,  M.,  Lamarche,  J.-B.,  Cahill,  S.  and
Guerrero-Garcia,  S.  (2018),  “Delivering  in  a  moving
world. . .looking to our supply chains to meet the increasing
scale, cost and complexity of humanitarian needs”, Journal of
Humanitarian Logistics and Supply Chain Management, Vol. 8
No. 4, pp. 518-532, doi: 10.1108/JHLSCM-10-2017-0048.
Liao,  C.S.  and  Huang,  Y.  (2014),  “The  covering  Canadian
traveller  problem”,  Theoretical  Computer  Science,  Vol.  530,
pp. 80-88.

Lim, Z.W., Hsu, D., Lee, W.S. and Sun, W. (2017), “Shortest
path  under  uncertainty:  exploration  versus  exploitation.  In
UAI”.

Lita,  L.V.,  Schulte,  J.  and  Thrun,  S.  (2001),  “A  system  for
multi-agent  coordination
in  uncertain  environments”,
Proceedings of the fifth international conference on Autonomous
agents, pp. 21-22.

Mendonca, D., Rush, R. and Wallace, W.A. (2000), “Timely
knowledge  elicitation  from  geographically  separate  mobile
experts during emergency response”, Safety Science, Vol. 35
Nos 1/3, pp. 193-208.

Mete, H.O. and Zabinsky, Z.B. (2010), “Stochastic optimization
of  medical  supply  location  and  distribution  in  disaster
management”,  International  Journal  of  Production  Economics,
Vol. 126 No. 1, pp. 76-84, doi: 10.1016/j.ijpe.2009.10.004.
Mitra, A. and Shaw, R. (2023), “Systemic risk from a disaster
management  perspective:  a  review  of  current  research”,
Environmental Science & Policy, Vol. 140, pp. 122-133.

Nikolova, E. and Karger, D.R. (2008), “Route planning under
uncertainty:  the  Canadian  traveller  problem.  In  AAAI”,
pp. 969-974.

NOAA  National  Centers  for  Environmental  Information
(NCEI)  (2024),  “U.S.  Billion-Dollar  weather  and  climate
disasters”,  available  at:  www.ncei.noaa.gov/access/billions/
10.25921/stkw-7w73 (accessed 7 June 2024).

Özdamar, L. and Ertem, M.A. (2015), “Models, solutions and
enabling  technologies  in  humanitarian  logistics”,  European
Journal of Operational Research, Vol. 244 No. 1, pp. 55-65,
doi: 10.1016/j.ejor.2014.11.030.

Papadimitriou,  C.H.  and  Yannakakis,  M.  (1991),  “Shortest
paths without a map”, Theoretical Computer Science, Vol. 84
No. 1, pp. 127-150.

Rawls, C.G. and Turnquist, M.A. (2010), “Pre-positioning of
emergency  supplies  for  disaster  response”,  Transportation
Research Part B: Methodological, Vol. 44 No. 4, pp. 521-534.
Sahin, O.F. and Aksakalli, V. (2015), “A comparison of penalty
and  rollout-based  algorithms  for  the  Canadian  traveler
problem”,  International  Journal  of  Machine  Learning  and
Computing, Vol. 5 No. 4, p. 319.

Salmeron, J. and Apte, A. (2010), “Stochastic optimization for
natural  disaster  asset  prepositioning”,  Production  and
Operations Management, Vol. 19 No. 5.

Shen, Z., Dessouky, M. and Ordonez, F. (2009), “A two-stage
large-scale  bioterrorism

vehicle
emergencies”, Networks, Vol. 54 No. 4, pp. 255-269.

routing  model

for

Shiri, D. and Salman, F.S. (2017), “On the online multi-agent
O–D k-Canadian traveler problem”, Journal of Combinatorial
Optimization, Vol. 34 No. 2, pp. 453-461.

Sodhi, M.S. and Tang, C.S. (2008), “The or/MS ecosystem:
strengths,  weaknesses,  opportunities,
threats”,
Operations  Research,  Vol.  56  No.  2,  pp.  267-277,  doi:
10.1287/opre.1080.0519.

and

Spencer, S.W. (2021), “Humanitarian AI : the hype, the hope and
the future (No. 85)”, Humanitarian Practice Network Paper.
Starr, M.K. and Van Wassenhove, L.N. (2014), “Introduction
to  the  special  issue  on  humanitarian  operations  and  crisis
management”,  Production  and  Operations  Management,
Vol. 23 No. 6, pp. 925-937, doi: 10.1111/poms.12227.

Stumpf, J., Besiou, M. and Wakolbinger, T. (2023), “Assessing
the value of supply chain management in the humanitarian
context  –  an  evidence-based  research approach”,  Journal of
Humanitarian Logistics and Supply Chain Management, Vol. 13
No. 1, pp. 1-9, doi: 10.1108/JHLSCM-03-2022-0039.

The World Bank (2023), “Global facility for disaster reduction
and  recovery  (GFDRR)  annual  report  2023  –  Bringing
resilience to scale”, available at: https://documents1.
worldbank.org/curated/en/099836402122412500/pdf/
IDU1296966181302414785188c41e3492095ce66.pdf
(accessed 7 June 2024).

Trunick,  P.A.  (2005),  “Logistics  when  it  counts”,  Logistics

Today, Vol. 46 No. 2, p. 38.

Ukkusuri,  S.V.  and  Yushimito,  W.F.  (2008),  “Location
routing  approach  for  the  humanitarian  prepositioning
problem”,  Transportation  Research  Record:  Journal  of  the
Transportation Research Board, Vol. 2089 No. 1, pp. 18-25.
United Nations Office for Disaster Risk Reduction (UNDRR)
(2022), “Global assessment report on disaster risk reduction
2022: our world at risk: transforming governance for a resilient
future”,  Geneva,  available  at:  www.undrr.org/media/79595/
download?startDownload=20240607 (accessed 7 June 2024).
U.S.  Department  of  Transportation  (USDOT)  (2008),
“Federal  highway  administration  (FHWA);  bureau  of
transportation statistics (BTS) [distributor] (2020). National
bridge  inventory  2008-Present[datasets]”,  doi:  10.21949/
1519015.

Downloaded from http://www.emerald.com/jhlscm/article-pdf/16/2/121/11452423/jhlscm-05-2023-0046en.pdf by guest on 15 April 2026

134

Online path planning

Journal of Humanitarian Logistics and Supply Chain Management

Jannatul Shefa, Ashlea Bennett Milburn and Erica Gralla

Volume 16 · Number 2 · 2026 · 121–135

Van  Hentenryck,  P.,  Bent,  R.  and  Coffrin,  C.  (2010),
“Strategic planning for disaster recovery with stochastic last
mile  distribution”,  Integration  of  AI  and  or  Techniques  in
Constraint  Programming
for  Combinatorial  Optimization
Problems, Springer, Berlin, Heidelberg, pp. 318-33.

Van  Wassenhove,  L.N.  (2006),  “Humanitarian  aid  logistics:
supply  chain  management  in  high  gear”,  Journal  of  the
Operational research Society, Vol. 57 No. 5, pp. 475-489, doi:
10.1057/palgrave.jors.2602125.

Vitoriano, B., Ortuno, T. and Tirado, G. (2009), “HADS, a
goal  programming-based  humanitarian  aid  distribution
system”,  Journal of  Multi-Criteria Decision  Analysis, Vol. 16
Nos 1/2, pp. 55-64.

Westphal,  S.  (2008),  “A  note  on  the  k-Canadian  traveller
problem”,  Information  Processing  Letters,  Vol.  106  No.  3,
pp. 87-89.

Xu,  Y.,  Hu,  M.,  Su,  B.,  Zhu,  B.  and  Zhu,  Z.  (2009),  “The
Canadian traveller problem and its competitive analysis”, Journal
of Combinatorial Optimization, Vol. 18 No. 2, pp. 195-205.

Yildirim, S., Aksakalli, V. and Alkaya, A.F. (2019), “Canadian
traveler  problem  with  neutralizations”,  Expert  Systems  with
Applications, Vol. 132, pp. 151-165.

Zhang,  H.,  Xu,  Y.  and  Qin,  L.  (2013),  “The  k-Canadian
travelers  problem  with  communication”,  Journal  of
Combinatorial Optimization, Vol. 26 No. 2, pp. 251-265.

Zhang, H., Xu, Y. and Wen, X. (2015), “Optimal shortest path
set problem in undirected graphs”, Journal of Combinatorial
Optimization, Vol. 29 No. 3, pp. 511-530.

Zhang, H., Tong, W., Xu, Y. and Lin, G. (2016), “The Steiner
traveling  salesman  problem  with  online  advanced  edge
blockages”,  Computers  &  Operations  Research,  Vol.  70,
pp. 26-38.

Further reading

Campbell,  A.M.,  Vandenbussche,  D.  and  Hermann,  W.
(2008),  “Routing  for  relief  efforts”,  Transportation  Science,
Vol. 42 No. 2, pp. 127-145.

Appendix. Interview guide

•  When responding to  disasters, what is  the scope of your
organization’s responsibilities and the authority you have
to deploy resources?

•  What are the three most recent events that you have needed
to  respond  to,  and  their  relative  magnitudes?  Please

elaborate  on  level  of  resources  (personnel,  equipment,
supplies, capital, etc.) deployed in response to this event.
•  What  type  of  transportation  activities  were  required  to
achieve your response goals in the events described in the
prior  questions?  Please  summarize  different  types  of
vehicles and personnel required.

•  What  type  of  transportation  plans  were  developed  in
advance of this event to achieve your response goals?
•  How often were transportation plans revisited, before and

during the event (hourly/daily/weekly)?

•  What types of changes were made to transportation plans

•

(Routes, loads delivered, etc.)?
In the course of responding to this event, how did plans
need  to  be  modified  in  light  of  the  situation?  For
example, were roads blocked by traffic or event related
damage?

•  Which response goals were accomplished? Please describe

how your transportation plan enabled this outcome.

•  What  tools  or  information  increased  your  capacity  to
respond to the events? Would you change these in any way?
•  Are  there  any  tools  or  information  which,  if  you  had  or
were  more  effective,  could  have  helped  achieve  your
response goals?

•  What  constraints  restricted  your  organization’s  response
in  terms  of  overall  capacity,  delays  in  deployment  or
increased response times?

•  How did you overcome these constraints?
•  Where  are  the  demand  points,  how  many  of  the  points
exist, how many shipments were each receiving, etc.?
•  On what timeline are truckload shipments to the demand
points  happening  (24  hours  after?  48?)  How  did
uncertainty  (especially  on  road  status)  impact  these
shipments which group makes decisions in terms of what
demand  points  needed  shipments  and  the  relative
priorities among them?

•  Once  a  decision  was  made  to  send  a  shipment  to  a
demand point, what operational details made that happen
(e.g. how were trucks and drivers matched to loads, who
“owned” the transportation resources, etc.)
Is there anything else you would like to add?

•

Corresponding author
Ashlea Bennett Milburn can be contacted at: ashlea@uark.
edu

For instructions on how to order reprints of this article, please visit our website:
www.emeraldgrouppublishing.com/licensing/reprints.htm
Or contact us for further details: permissions@emeraldinsight.com

135

Downloaded from http://www.emerald.com/jhlscm/article-pdf/16/2/121/11452423/jhlscm-05-2023-0046en.pdf by guest on 15 April 2026

