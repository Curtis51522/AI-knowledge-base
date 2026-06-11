2026/4/16 02:33

Robust dual sourcing inventory routing optimization for disaster relief | PLOS One

Robust dual sourcing inventory routing optimization for
disaster relief

Weibo Zheng, Hong Zhou

Published: April 27, 2023

https://doi.org/10.1371/journal.pone.0284971

Abstract

This paper considers the problem that a depot replenishes several shelters by aerial and land transportation modes for disaster
relief. There are two distinguishing features of our problem: one is routing decisions determine replenishment lead times; the other
is that we introduce dual sourcing policy into the inventory routing problem. A robust optimization model is proposed to determine
the optimal replenishment quantity, replenishment mode, and transportation routes. Then, we decompose the problem into a routing
master-problem and a set of inventory sub-problems. A tractable closed-form solution for sub-problem is derived. We further
develop an adaptive large neighborhood search algorithm to solve the problem. To demonstrate the feasibility of the algorithm, we
conduct a series of numerical experiments on the benchmark test suite with different scales and compare the performance of the
proposed algorithm with a genetic algorithm.

Citation: Zheng W, Zhou H (2023) Robust dual sourcing inventory routing optimization for disaster relief. PLoS ONE 18(4):
e0284971. https://doi.org/10.1371/journal.pone.0284971

Editor: Yossiri Adulyasak, HEC Montréal, CANADA

Received: October 20, 2022; Accepted: April 12, 2023; Published: April 27, 2023

Copyright: © 2023 Zheng, Zhou. This is an open access article distributed under the terms of the Creative Commons
Attribution License, which permits unrestricted use, distribution, and reproduction in any medium, provided the original author
and source are credited.

Data Availability: All relevant data are either within the manuscript, or accessible at the following websites. The test set can
be found at http://vrp.galgos.inf.puc-rio.br/index.php/en/ (accessed on 26 January 2023). The source code of the proposed
ALNS algorithm can be found at https://github.com/WeberZheng/ALNS (accessed on 26 January 2023).

Funding: This work is supported by the National Natural Science Foundation of China (https://www.nsfc.gov.cn/) under Grant
No.71971011. The recipient is Professor Hong Zhou. The funders had no role in study design, data collection and analysis,
decision to publish, or preparation of the manuscript.

Competing interests: The authors have declared that no competing interests exist.

1 Introduction

With the intensification of human activities, natural disasters, epidemics, and wars have led to many humanitarian disasters.
Disasters lead to large-scale casualties, material shortages, and poor rescue environments. For example, an earthquake
magnitude of 8.0 on the Richter scale struck Sichuan Province, China, on May 12, 2008 [1]. Thousands of damage incidents occur
to roads, bridges, railways, and other basic infrastructures. In the early stages of relief operations, helicopters and trucks were used
to deliver humanitarian supplies. In the critical first 72 hours, helicopters proved crucial in the affected area with poor road
conditions. Multi-modal transport also minimizes the risk of emergency supplies failing to reach the affected area or breaking down
emergency evacuation procedures [2].

Temporary shelters in the affected area play an essential role in disaster relief, that for accommodating patients and refugees, and
providing food, water, and simple medical services. Governments and humanitarian organizations usually enhance their
preparedness for disasters by pre-positioning inventory. However, storing large quantities of humanitarian relief supplies in shelters
is unrealistic because of the poor storage conditions and the risk of secondary disaster. Emergency supplies are usually properly
housed in one or more permanent or semi-permanent central depots. In emergency rescue, one crucial problem is delivering
humanitarian relief from the central depot to shelters in the right amount and at the right time. However, structuring a post-disaster
humanitarian relief distribution network to support emergency rescue for sudden-onset disasters is challenging because of demand
uncertainty.

Due to secondary disasters and unpredictable accidents, shelters demand information in post-disaster areas is uncertain. It is
difficult to deduce a specific distribution of demand. Robust optimization is a powerful approach to uncertainty problems. Compared
to stochastic optimization, robust optimization doesn’t require knowledge of the distribution of uncertain information. Therefore,
robust optimization is widely used in emergency rescue problems with uncertain demand. In addition, disasters like earthquakes
lead to deteriorated transportation situations, such as road damage. It increases the difficulties of rescue. Road damage also
results in a longer delivery time, even more than a few days when using land transportation. To ensure relief’s timeliness, combing
aerial and land replenishment is an essential strategy in emergency logistics [3].

In emergency rescue, the inventory management and material deployment of shelters are usually taken over by a unified manager,
such as the Red Cross organization. The joint optimization of inventory and routing mobilizes resources more timely and effectively
to aid people affected by natural disasters and crises. Inventory routing problem (IRP) is first studied by Bell et al. (1983) under the
context of vendor-managed inventory (VMI) [4]. Traditional IRP studies a distribution system including one supplier and several
customers. The objective is to design an inventory policy and a set of vehicle routes to minimize the total cost of inventory and
delivery. Traditional IRP assumes that the lead time is not impacted by route decisions. However, this assumption is not always

https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0284971

1/14

2026/4/16 02:33

Robust dual sourcing inventory routing optimization for disaster relief | PLOS One

reasonable, especially in disaster relief. The lead time for replenishment from the central depot to shelters is almost only composed
of transportation. The different delivery routes affect the replenishment arrival time and, thus, the lead time of shelters. It links the
inventory policy and the route decision much tighter and more complex.

This paper addresses a joint optimization problem of distributing humanitarian relief supplies from a central depot to several
temporary shelters. Under the highly uncertain situation in post-disaster, planning a long-term policy is very difficult. We focus on a
single-period inventory routing problem. A robust dual sourcing inventory routing problem (RDSIRP) model is proposed, which
considers the impact of routing decisions on lead times. Dual-sourcing inventory policy uses two replenishment sources, where the
regular one is cheaper but slower than the other one. We introduce the dual sourcing policy to IRP, which uses an aerial
replenishment mode (usually by helicopter) and a land replenishment mode (usually by truck). For each shelter, there are four
replenishment policies: the shelter is replenished by truck, by helicopter, by both, or by no replenishment. In this problem, three
decisions are made: first, the selection of shelters to be replenished and the corresponding mode, second, the amount of delivered
supplies, and third, the sequence of the shelters’ replenishment. They belong to three kinds of problems: assignment problems,
inventory policies, and routing problems. We derive a closed-form solution of the optimal replenishment quantity under different
lead times for the inventory policy. Then an adaptive large neighborhood search (ALNS) algorithm is developed to solve the
assignment and routing problems.

The remainder of the paper is organized as follows: In section 2, the relevant investigations are reviewed and summarized. Section
3 describes the RDSIRP and presents mixed-integer programming formulations for the problem. In section 4, we derive a closed-
form solution for the inventory policy and present our ALNS, followed by numerical experiment results in section 5 and our
conclusions in section 6.

2 Literature review

Humanitarian logistics is essential because unavailability or slowness in mobilizing supplies causes increased human suffering and
loss of life when a disaster strikes. Despite humanitarian logistics’ importance, the literature is limited in this area [5]. In recent
years, humanitarian logistics has been studied in many aspects. Awan and Shafiq (2015) proposed a supply chain management
framework for humanitarian logistics and explain how to overcome logistics difficulties during relief operations [6]. For the
humanitarian relief inventory management aspect, Balcik et al. (2016) made a literature review on pre-disaster and post-disaster
inventory management in humanitarian [7]. For the humanitarian relief delivery aspect, Holguín-Veras et al. (2013) proposed an
exponential function to estimate the economic value of human suffering resulting from the lack of access to goods or service [8].
Then Çankaya et al. (2019) proposed an objective to minimize human suffering by minimizing the maximum length of the shortage
duration [9]. Zhang et al. (2017) proposed a programming model for the vehicle routing problem (VRP), which combines air and
ground transportation for emergency logistics [3]. Then Zheng and Zhou (2018) studied an air-ground transportation routing
problem considering road damage in disasters [10]. Balcik and Yanıkoğlu (2020) studied a robust routing problem under travel time
uncertainty in post-disaster, they used an evaluation function to choose which customer should be visited [11]. Yang et al. (2018)
studied an inventory slack routing problem that applied to relief distributions [12]. Qiu et al. (2015) studied the time uncertainty in
emergency logistics based on the grey theory optimization model [13].

In emergencies, the distribution information of demands is hard to estimate. Robust optimization is a powerful methodology for
uncertain problems with unknown distribution. Soyster and Allen (1973) first studied robust optimization for solving linear
programming problems with uncertain parameters, considering their worst case values under the uncertainty set [14]. The
assumption that all uncertain parameters will get their worst case values is too conservative. To overcome the solution over-
conservativeness, Ben-Tal and Nemirovski (1998) developed the ellipsoidal uncertainty set for uncertain convex optimization
problems [15]. However, the ellipsoidal uncertainty set increases the problem’s complexity. Then Bertsimas and Thiele (2006)
developed a robust optimization approach based on budget uncertainty set to inventory theory [16]. Based on the dual balance
policy (see [17]), Mamani et al. (2017) derived a closed-form order size for robust inventory problem [18]. Then, Sun and van
Mieghem (2019) provided a closed-form robust dual-sourcing policy for inventory problems by normalizing the slow ordering cost
and fast lead time to 0 [19]. Ji et al. (2022) proposed three stochastic models to study uncertain factors and apply the L-shaped
algorithm to achieve an optimal solution [20]. Qu et al. (2023) applied robust optimization to studying uncertainties in decision-
making and propose four robust models based on the box, ellipsoidal, box-ellipsoidal, and box-polyhedral uncertainty sets,
respectively [21].

The inventory routing problem is a joint optimization of inventory policies and routing decisions. It mobilizes resources timelier and
more effectively, reducing human suffering and loss of life in emergencies. After the earlier works by Bell et al., Dror and Ball (1987)
extended IRP to the multi-period finite horizon and proposed the first definition of the standard IRP [22]. Based on this framework,
lots of variants based on the demand (deterministic or stochastic) and the planning horizon (finite or infinite) were studied. The
stochastic demand IRP is a difficult challenge. Archetti et al. (2007) considered a finite planning horizon IRP with stochastic demand
[23]. Hvattum et al. (2009) proposed a cyclic distribution strategy and points out that a finite scenario tree can capture most
stochasticity, which means stochastic IRP can be solved by solving a scenario tree [24]. These IRP models did not consider
transportation time consumption in lead times. Li et al. (2016) first studied a stochastic demand IRP with considering the
replenishment routes affect lead times [25]. Then Zheng and Zhou (2019) presented a robust optimization model to deal with the
uncertain demand and analyzed the influence between route decisions and order size [26]. Sanada et al. (2021) studied the
inventory routing problem considering road closures in disaster [27].

Compared to other metaheuristics, the large neighborhood search (LNS) framework mainly employs insertion operators, which is
very suitable for joint optimization of assignment and routing problems. The LNS framework was first introduced by Shaw (1998)
and was applied to VRP with time windows [28]. It used a destroy-repair mechanism to search very large-scale neighborhoods.
Shaw proposed a highly flexible removal operator called Shaw removal operator. In the LNS framework, operators can be highly
customized by the problem. Then Røpke et al. (2006) proposed an adaptive large neighborhood search (ALNS) algorithm by
introducing the adaptive mechanism to select removal and insertion operators [29]. Coelho et al. (2012) introduced the ALNS
framework to IRP and developed a periodic post-optimization procedure to improve development ability [30]. Liu et al. (2020)
studied a blood products inventory routing problem and proposed a decomposition-based algorithm [31]. The inventory sub-
problem is solved by mixed-integer linear programming, and ALNS solves the routing sub-problem.

In general, current research on humanitarian logistics IRP is insufficient. IRP in an emergency context has many new challenges
that need to be addressed. This paper is a novel attempt to consider transportation time as the lead time in inventory and routing
joint optimization for emergency logistics.

3 Problem description and formulations

https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0284971

2/14

2026/4/16 02:33

Robust dual sourcing inventory routing optimization for disaster relief | PLOS One

2

1

In post-disasters, several shelters are open for people in the affected area. The humanitarian relief central depot is responsible for
choosing optimal routes and managing the inventory of the shelters. We consider the impact of delivery routes on the
replenishment quantity in this paper. The following example illustrates why different arrival times lead to different replenishment
quantities (as shown in Fig 1). For clarity and convenience, let us consider a simplified inventory problem and make the following
assumptions: 1) the initial inventory level is 0; 2) the unit holding cost and the unit shortage cost are the same; 3) the demand per
unit time is constant. The objective is to minimize the holding cost and the shortage cost by deciding the optimal replenishment
quantity. l  and l  indicate two different possible lead times of a shelter. The replenishment quantity cannot impact the inventory cost
before the replenishment arrival (s ). If we make the decision based on the lead time of l , the optimal replenishment quantity would
be q , and the out-of-stock point is t , where in the middle of l  to T. As shown in sub-figure (a). Similarly, when we make the
1
decision based on the lead time of l , the optimal replenishment quantity would be q , and the out-of-stock point is t . As shown in
sub-figure (b). Assuming l  is the normal arrival time of replenishment, and l  is the delayed arrival time. If the replenishment delay
to l  and still replenish q , then the out-of-stock point is t . It leads to a larger shortage cost and a smaller holding cost than the
normal arrival time. As shown in sub-figure (c). The sub-figure (d) shows the extra cost of q  than q  when the replenishment is
delayed. An extreme example is that if the supplies arrive after t , and we still replenish q  according to the lead time l , then the
1
shelter keeps out-of-stock throughout the planning horizon. Apparently, the later arrival time leads to a larger replenishment
quantity. The larger replenishment quantity reduces inventory costs after replenishment arrival. But replenishment delays still incur
higher inventory cost for the entire planning horizon.

1
2

2

1

2

1

2

1

1

0

1

1

1

2

2

1

Fig 1. Later arrival time lead to a bigger replenishment quantity.
https://doi.org/10.1371/journal.pone.0284971.g001

3.1 Problem definitions

In this problem, we define a directed graph G = (V, A), where V = {0, …, n} is the vertex set and A = {(i, j) ∈ V, i ≠ j} is the arc set.
Vertex 0 represents the depot and the vertexes of V′ = V∖{0} represent shelters. Arc (i, j) represents the shortest route between
vertex i and vertex j. The planning horizon is T. The initial inventory level is revealed at the beginning of the planning horizon. Then,
a truck and a helicopter depart from the central depot and return to the depot in the planning horizon. The helicopter’s unit time
shipping cost is f , and the truck’s unit time shipping cost is f . where f  > f . γ represents replenishment modes, where γ ∈ {0, 1},
0 represents the land replenishment mode, and 1 represents the aerial replenishment mode. We assume the lead time of each
shelter in each replenishment mode is the time consumption of transport. The truck may arrive earlier than the helicopter for a
shelter because of the delivery sequence. Define l  = min {l , l } and l  = max {l , l } as the lead time of the faster one and the lead
time of the slower one, respectively. Similarly, q  and q  are the replenishment quantity of the faster one and the slower one,
respectively.

0 1

0 1

0

0

1

1

s

s

f

f

Due to the affected area’s incomplete information, demands are highly uncertain. We assume the distribution of demands is
unknown. Demands are independent, and values are in the positive symmetric interval , where  is the estimated demand of shelter i
at time unit t, and  is the maximum deviation for the demand of shelter i at time unit t. At the time unit t, the demand of the shelter i
is deducted from the total amount of the on-holding stock. If the total amount available is unmet demand, the unmet demand is
backlogged to be satisfied in the future and causes a shortage cost. Otherwise, excess inventories are carried over at shelter i to
satisfy future demands and cause a holding cost. Every shelter has a unit holding cost h and a unit shortage cost s, where s > h.
When s ≫ h, out-of-stock will be avoided as much as possible.

To understand this problem intuitively, a set of possible delivery routes shows in Fig 2. Unlike traditional TSPs, each delivery route
in this problem does not necessarily need to serve all shelters. Due to each shelter’s inventory cost, the optimal delivery route may
not be the shortest.

Fig 2. Illustration of the dual sourcing inventory routing problem.

https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0284971

3/14

2026/4/16 02:33

Robust dual sourcing inventory routing optimization for disaster relief | PLOS One

https://doi.org/10.1371/journal.pone.0284971.g002

3.2 Dual sourcing inventory routing model

An inventory routing model considering the replenishment lead time is proposed. Notations not mentioned in the problem definitions
are listed as follows:

: The time cost of transportation from vertex i to vertex j by mode γ.

M: A big enough positive constant.

I : The initial inventory level of shelter i at the beginning of the planning horizon.
i

n : On-holding stock of shelter i at time t.

it

: 1 if the route of replenishment mode γ visits vertex j immediately from vertex i; 0 otherwise.

The objective function is the logistic cost within the planning horizon. The first item is the transportation cost of the two
replenishment modes, and the second item is the inventory cost of all shelters.

(1)

(2)

(3)

(4)

(5)

(6)

(7)

(8)

(9)

(10)

Constraint (2) is inventory balance equation, where  is the cumulative demand of shelter i at time t. sgn{} is an indicator function,
sgn {A} = 1 if A > 0, and sgn {A} = 0, otherwise; constraint (3) guaranteeing the replenishment quantity is zero if no replenishment
mode service the customer j; constraint (4) is used to determine the arrival time which equals to the replenishment lead time, and it
also eliminates subtours; constraint (5) ensures each shelter only be serviced no more than once; constraint (6) is the flow
conservation constraint; constraint (7) ensures truck and helicopter back to the depot within the planning horizon; (8) and (9) are
integer constraints; (10) is the non-negativity constraint.

In constraint (2),  is relevant to the variable , which means the inventory policy and the routing decision have a strong correlation by
the lead time. So, we divide the model into the master-problem and a set of sub-problems. The master problem is a routing problem
with constraints (3–10), considering inventory cost in the objective function. The sub-problem is an inventory problem with
constraints (2, and 10), and the objective is to minimize the shortage cost and the holding cost. For the sub-problem, the lead time
depends on the routing problem constraints (4), which is an exogenous variable. The optimal inventory policy is to determine the
replenishment quantity under the trade-off between holding cost and shortage cost. For the master problem, which route be chosen
depends on the objective function value that includes the objective value of the sub-problem. Fig 3 shows the interaction between
the master problem and sub-problems. The master problem determines the replenishment routes by the decision variable . When
the route is determined, the replenishment arrival time (lead time ) of each shelter is revealed. Then the sub-problem determines
the optimal replenishment quantities  based on lead times. The solution of the master problem and sub-problems determines the
routing cost and the inventory cost. Then the master problem is searching for better replenishment routes to optimize the logistic
cost.

https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0284971

4/14

2026/4/16 02:33

Robust dual sourcing inventory routing optimization for disaster relief | PLOS One

Fig 3. Interactions between the master-problem and sub-problems.
https://doi.org/10.1371/journal.pone.0284971.g003

3.3 Robust formulations

Given a set of replenishment routes, lead times are exogenous for sub-problems. The optimal inventory policy is to find an optimal
replenishment quantity under the given lead time. The decision would be over conservativeness when we consider the worst case
of the demand in the interval . A budget of uncertainty is imposed to ensure the total variation of the uncertainty parameters cannot
exceed some threshold Γ. For the shelter i, we define the vector of future demands is contained in a non-negative bounded budget
uncertainty set

where Γ  is a non-decreasing threshold in t to control the total variation of demands under an assumption that uncertainty increases
with the number of periods considered [16]. We define Γ
t

t

(11)

Where λ = (s − h)/(s + h). For each shelter and any possible lead time, a sub-problem is formulated as follows:

(12)

(13)

where  is a parameter determined by replenishment routes. We solve the robust optimization problem for each shelter that
minimizes the worst case cost. To describe the worst case, we first define the minimum and maximum cumulative demands.

Assuming the cumulative demand is non-decreasing (for all d  ≥ 0), for any uncertainty set U, the worst case of cumulative demand
 and  can be denoted as  and , respectively. Under the budget uncertainty set , the worst case of cumulative demand is formulated
as follows:

iδ

and

Where .

(14)

(15)

We introduce the auxiliary variables z , called the maximum mismatch (holding or shortage) cost of shelter i at time unit t. Then the
it
robust dual sourcing (RDS) optimization sub-problem is formulated as follows:

For any I and l, the robust optimization problem has an optimal solution, denoted by . when the initial inventory level and the
replenishment lead time are determined at the beginning of the planning horizon, the corresponding optimal inventory cost is

(16)

(17)

4 Methodologies

In this section, we derive a closed-form robust optimal solution to the sub-problem. Then we develop an adaptive large
neighborhood search algorithm to solve the master problem.

4.1 Closed-form sub-problem solution

During the iteration, RDS sub-problems need to be solved many times. A closed-form sub-problem solution would accelerate
algorithms and make the inventory policy much easier to understand. The following proposition presents optimality conditions that
RDS with exogenous lead time and initial inventory level.

https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0284971

5/14

2026/4/16 02:33

Robust dual sourcing inventory routing optimization for disaster relief | PLOS One

Proposition 1 (optimality conditions) For any uncertainty set U, and in any time unit t = 1, ⋯, T, since  is non-negative and non-
decreasing in t, the robust optimal replenishment quantity in the planning cycle of each mode satisfy:

(1) For any shelter replenished by single mode, the optimal replenishment quantity is

where , and

(2) For any shelter replenished by both two modes, the optimal replenishment quantity of the faster arrival one is

and the slower one is

where  and , respectively.

(18)

(19)

(20)

(21)

The proof of Proposition 1 is in S1 Appendix. When a shelter is replenished by single mode, for out-of-stock point t , we solve the
optimal replenishment quantity by Eq (18). The point corresponding to the smallest inventory cost is . When both two modes
replenish a shelter, the optimal replenishment quantity q  and q  is solved by the combination of  and  by (20) and (21).

s*

f*

i

4.2 Adaptive large neighborhood search algorithm

The problem we considered is NP-hard since the problem contains two TSPs. Developing a heuristic to deal with realistic size
instances is necessary. The ALNS algorithm is suitable for the joint optimization of routing and assignment problems. It can handle
the situation that only partial shelters are visited in a single replenishment mode. We describe our ALNS heuristic under the
framework of [29, 30]: The algorithm begins with an initial solution S , which is generated by the initial solution generator. One
solution consists of two parts: the land replenishment mode and the aerial replenishment mode. Each replenishment mode
corresponds to a route and a pool. Shelters not served by the replenishment mode will be placed in the reinsert pool. The roulette-
wheel mechanism selects a pair of removal and insertion operators in each iteration and generates a neighborhood solution S′. The
removal operator removes shelters from their current route, and the insertion operator inserts shelters into the way from the reinsert
pool. The removal rate ρ controls the number of shelters removed by the removal operator in each iteration. The insertion operator
inserts shelters into the route as much as possible until the logistic cost is no longer reduced. The current solution will be updated
according to the simulated annealing (SA) mechanism which is based on the performance of S′. Search procedures are divided into
several segments, and each segment contains ξ iterations. At the end of each segment, the selection probability of each operator is
updated based on their performance in this segment, and we apply a 2-opt procedure to each mode as a periodic post-optimization.
This process repeats until the termination criteria are satisfied. The framework is illustrated in Fig 4.

0

https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0284971

6/14

2026/4/16 02:33

Robust dual sourcing inventory routing optimization for disaster relief | PLOS One

Fig 4. An illustration of the ALNS algorithm.
https://doi.org/10.1371/journal.pone.0284971.g004

1. Initial solution generator

The initial solution generator begins by adding all the shelters to reinsert pools, then alternately select a replenishment mode and adds the shelter with the
lowest insertion cost to the end of the route until the insertion cost becomes positive. The insertion cost is defined as the difference in the objective value after
inserting one shelter into the current route. Let f(S) represent the objective value of the current solution S, and f(S′) represent the objective value after the
shelter i is inserted into a position of the route. The insertion cost for shelter i is f(S′) − f(S).

2. Removal operators

Shaw removal: Shaw (1998) suggests that removing a set of shelters that are related is logical and useful [28]. We modified the operator to fit this problem.
The relatedness between shelter i and j is described by R(i, j) as

(22)

The relatedness measure consists of the distance d and the optimal replenishment lead time l*. We set the weight φ = 0.5. d  and  are normalized. The smaller
R(i, j) represents the higher relatedness. A shelter is randomly chosen from a removal pool of a replenishment mode. If the removal pool is empty, randomly
remove a shelter in the route. Then the relatedness between a set of shelters in the current route and the already removed one is calculated. The highest
relatedness shelter is removed from the current route. Check for the removed shelter. If both two replenishment modes replenish it, remove it from the route of
another replenishment mode together. The complexity of this operator is O(n).
Distance removal: Similar to the Shaw removal operator, the closest shelters are removed from the current route, where φ = 1. But the operator does not
remove the same shelter in the route of another replenishment mode. The complexity is O(n).
Worst removal: Let f(S) represents the objective value of the current solution S, and f(S′) represents the objective value after the shelter i removed from a
route. The removed cost of shelter i is defined as f(S′) − f(S). This operator removes the shelter with the lowest removal cost, and the complexity is O(n).
Worst replenishment time removal: If a shelter is replenished by one mode, we use replenishment time gap g to measure the gap between the arrival and
optimal replenishment times. This operator removes the shelter with the highest g. The complexity of this operator is O(n).
Random removal: This operator randomly removes a shelter from a route. The complexity of this operator is O(1).

ij

3. Insertion operators

Greedy insertion: The insertion cost for inserting each shelter in the removal pool into every feasible position is calculated. The insertion cost is defined as
the same as the initial solution generator. Then insert the shelter with the minimum insertion cost to the insertion position. The complexity of this operator is
2
O(n )
2-regret insertion: The regret insertion tries to use a kind of look-ahead information when selecting the shelter. For a replenishment mode γ, let  be the
insertion cost that the shelter i inserts the k’th position of the route. Then rank  for every insert position k,  represents the regret value which is the difference in
the cost of inserting the shelter in its best position and its second-best position. In each iteration, insert the shelter with the maximum regret value to the best
insertion position accordingly, and the complexity is O(n ).
Random Shaw insertions: First, put all shelters which not inserted any route into a candidate pool. Then select a shelter randomly from the candidate pool
and calculate the relatedness between the chosen shelter and the others in the pool. Finally, a pair of shelters with the highest relatedness is selected and
inserted into an adjacent position of a route with the lowest insertion cost. The complexity of this operator is O(n).

2

4. SA acceptance criterion

We use an acceptance criterion based on the simulated annealing mechanism. Given a solution S, a neighbour solution S′ is accepted if f(S′) < f(S) and with

[f(S′) f(S)]/

https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0284971

7/14

2026/4/16 02:33

Robust dual sourcing inventory routing optimization for disaster relief | PLOS One

−[f(S′)−f(S)]/τ

probability e
iteration, where 0 < ϕ < 1.

 otherwise, where τ > 0 is the current temperature. The temperature starts at τ

 and is decreased by a cooling rate factor ϕ at each

start

5. Adaptive mechanism

The choice of which operator to apply at an iteration is adapted by the roulette-wheel mechanism. Each operator has a weight and a score. The probability of
each operator is based on its weight, depending on its past performance. Let θ  is the weight of operator i, then operator j be selected with probability θ /∑  θ .
j ∀i
i
i
As mentioned before, the search progress is divided into segments of ξ iterations each. In each segment, initially, the score is equal to 0. At each iteration, if
the neighbor solution S′ is better than the best solution, the score of operators used in the iteration is increased by σ ; if S′ is better than the current solution S,
the score is increased by σ ; if S′ is accepted by the SA acceptance criterion, the score is increased by σ ; if S′ is not accepted, the score is increased by 0.
After the last iteration of the current segment, update the weights of operators based on their score. We use π  to represent the score of the operator i at the
end of the current segment, and κ  is the number of times has been used in the segment of the operator i. Then the weight in the next segment is updated by

1

3

2

i

i

where η = [0, 1] is called the reaction factor, controlling the adjustment speed.

6. Periodic post-optimization

LNS mainly adopts insertion heuristics, which makes the development ability of this algorithm insufficient. In the improved heuristic, 2-opt performs well in
inner route local search. We apply a 2-opt procedure at the end of each segment to optimize the current best solution. The 2-opt operation randomly selects
two shelters in the route of a mode and then swaps the route between them. This operation repeats until the current best solution has no improvement times
more than periodic iterations limits , where the complexity is O(n) in the once 2-opt operation.

7. Termination criteria

We limit the running time to 1h, maximum iterations Iter

max

 = 3000, and when the temperature is reached, the cut-off threshold τ

 = 0.01.

cut

8. Parameter settings

(23)

We test different parameter combinations in a tuning phase to three randomly generated instances, including a small instance with 10 shelters, a middle
instance with 50 shelters, and a large instance with 100 shelters, respectively. In addition, the selection of parameters also partially refers to the settings of
[30]. The starting temperature τ
 is set to 30,000 and the cooling rate ϕ is 0.995. For large instances, more computing time per iteration is required, which
leads to the temperature being too high when the time limit is reached. So, if the running time is more than 1/3 of the running time limit and the iterations are
less than 1/3 maximum iterations, then the cooling rate is set to (τ
less than 1/2 maximum iterations, then the cooling rate is set to (τ
iterations is 3000 or the running time is 1 hour. The removal rate ρ = 20%. The segment capacity ξ = 50 and the reaction factor η = 0.2. Scores are updated
with σ  = 10, σ  = 5, and σ  = 2. The periodic iterations limits .

; if the running time is more than 2/3 of the running time limit and the iterations are
. This mechanism makes the temperature closer to τ

 when the number of

(1/2Iter)

/τ)
/τ)

(1/Iter)

start

cut

cut

cut

1

2

3

5 Numerical experiments

This section provides the computational results related to our model solved by the ALNS. The ALNS is implemented on Python 3.9
and on a PC with Intel i9 10900 CPU @ 4.0GHz processor and 16 GB RAM. All numerical results reported in tables are the
average of running five times. (The test set can be found at http://vrp.galgos.inf.puc-rio.br/index.php/en/. And the source code of the
proposed ALNS algorithm can be found at https://github.com/WeberZheng/ALNS.)

5.1 Benchmark instances

There is no available benchmark instance in the literature that fits the problem we proposed. So, we adapt Augerat’s CVRP
benchmark instance Set A and Set B to this problem. Node coordinates in the instance set A are generated in the range 100 × 100
randomly, and demands are generated in the interval [1, 30]. The node coordinates and demand information in the instance set B
come from some practical application scenarios. The first node is the depot, and the other nodes are shelters. We use the demands
information as the initial inventory level to fit our problem. We set the scale is 1:1km, the truck travels at a speed of 60km/h, and the
helicopter travels at a speed of 260km/h. The typical trailer consumes 29.9 L/100km of fuel and the Sikorsky S-76C helicopter with
260km/h consumes 143 L/100 km. It is justifiable that we set the truck unit cost of use as 200 and the helicopter unit cost of use as
1000, which is similar to the fuel consumption ratio. We also set the unit holding cost as 2 and the unit shortage cost as 20. For
convenience, we set all shelters to have the same predicted demand per unit time with . and . Considering the master problem is
NP-hard, and the complexity of solving a sub-problem by the method we proposed is O(T). The planning horizon T to contain 8 time
units to simulate 8 hours of working time and reduce the computational cost of experiments.

Under these instance parameter settings, these instances simulate two situations: The small-scale instances simulate the situation
when the land replenishment mode can service all shelters within the time limit. The large-scale instances simulate the situation
when the land replenishment mode cannot service all shelters within the planning horizon.

5.2 Model analysis

We first compare the logistic cost gaps of dual-sourcing to only land replenishment mode and only aerial replenishment mode. As
shown in Table 1, the baseline of gaps is the dual-sourcing, where all Gaps in this paper are calculated by

(24)

https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0284971

8/14

2026/4/16 02:33

Robust dual sourcing inventory routing optimization for disaster relief | PLOS One

Table 1. Logistic cost gaps between dual-sourcing and single replenishment modes.
https://doi.org/10.1371/journal.pone.0284971.t001

The results show that the dual sourcing policy significantly reduces costs than only one replenishment mode policy. Only the land
replenishment mode performs significantly poorly because only using the truck exceeds the planning horizon on large-scale
instances. Moreover, in the case of only using the land replenishment mode, many shelters cannot be replenished in the planning
horizon, leading to a higher inventory cost than the other two situations.

In addition, we compare the logistic costs between routing decisions with and without considering inventory cost (IC) under only
one replenishment mode, and the baseline is routing considering inventory cost. The dual replenishment mode problem without
considering inventory cost is not studied because the replenishment mode selection is highly related to inventory cost. For the
routing solution without considering inventory cost, the shortest route is found by solving the mixed-integer linear programming of
TSP. Gaps are reported in Table 2. The logistic cost considering the inventory cost is better than without considering the inventory
cost when making the routing decision, where gaps are 21.04% and 4.98%, respectively.

Table 2. Logistic cost gaps between routing with/without considering inventory cost.
https://doi.org/10.1371/journal.pone.0284971.t002

In this paper, we use the budget uncertainty set to describe the uncertain demand. Compare to the box uncertainty set, the budget
uncertainty set can overcome the solution over-conservativeness. Table 3 shows the logistic cost and replenishment quantity gaps
between budget and box uncertainty sets, where the baseline is the budget uncertainty set. Using budget uncertainty sets can save
21.12% of the cost than using box uncertainty sets. Because the box uncertainty set is too conservative, the depot will provide
more supplies to the shelter to avoid the shortage in extreme cases.

https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0284971

9/14

2026/4/16 02:33

Robust dual sourcing inventory routing optimization for disaster relief | PLOS One

Table 3. Logistic cost and replenishment quantity gaps between budget and box uncertainty sets.
https://doi.org/10.1371/journal.pone.0284971.t003

Furthermore, we analyze the inventory-routing policy on instances A-n32 and B-n78, where the nodes in instance A-n32 is are
uniformly distributed and the nodes in instance A-n32 is are clustered. For the small instance A-n32, the truck has the ability to
service all shelters in the planning horizon. On the contrary, the instance B-n78 is big enough to simulate the situation that some
shelters cannot be serviced by land replenishment mode. For humanitarian considerations, we did not analyze the situation that
some shelters must be abandoned due to time inability in dual replenishment mode on very-large-scale instances. Usually,
additional working time and vehicles can support these shelters.

Fig 5 shows the best route solved by the proposed ALNS algorithm. Where shelters with a low initial inventory level (LILs with 0 ≤ I
0
≤ 10) are marked as red points, with a middle initial inventory level (MILs, with 10 < I  ≤ 20) are marked as black points, with a high
initial inventory level (HILs, with 20 < I  ≤ 30) are marked as green points, and the central depot is marked as a black triangle.
Results show that on the small-scale instance A-n32, most shelters are replenished by the land replenishment mode and the aerial
replenishment mode only as a means of quickly replenishing ways. On the large-scale instance B-n78, most shelters are
replenished by helicopter. Some shelters far from the depot are abandoned by the land replenishment mode. In both instances,
almost all LILs are replenished with priority and considered the distance factor.

0

0

Fig 5. Routing decisions.
(a) Routing decisions on A-n32. (b) Routing decisions on B-n78.
https://doi.org/10.1371/journal.pone.0284971.g005

5.3 Sensitivity analysis

The two most important parameters that affect the performance of ALNS are the removal rate ρ and the reaction factor η. We now
analyze the value selection of these two parameters based on tuning phase solutions. The removal rate ρ is selected from 10%,
15%, 20%, 25%, and 30%. The reaction factor η is selected from 0.1, 0.15, 0.2, 0.25, 0.3. We use each combination to test
instances A-n32 and B-78 for comparing the best objective value. Tables 4 and 5 shows the logistic cost of the ALNS algorithm with
different removal rates and reaction factor tests on instance A-n32 and B-n78, respectively. The results validate the parameter
settings we got during the tuning phase that setting the removal rate ρ = 20% and the reaction factor η = 0.2 have a better
performance.

Table 4. Logistic cost on instance A-n32 with different removal rate and reaction factor.
https://doi.org/10.1371/journal.pone.0284971.t004

Table 5. Logistic cost on instance B-n78 with different removal rate and reaction factor.
https://doi.org/10.1371/journal.pone.0284971.t005

5.4 Performance of operators

We study the computational performance of all operators. Generally speaking, the weights of operators reflect the ability of an
operator to find an acceptable/better solution than the current/best solution. Fig 6 shows the weight of different operators in 3000
iterations on instance A-n32. For removal operators, it is easier to accept the current solution when the temperature is high, which

https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0284971

10/14

2026/4/16 02:33

Robust dual sourcing inventory routing optimization for disaster relief | PLOS One

means operators get scores more easily. So that weights are not significantly different in the early stage. When the temperature is
low, only finding a better solution can have scored, so the weights begin to difference obvious. The Shaw removal operator
outperforms other operators in obtaining better solutions, and the distance removal operator performs the worst. For insertion
operators, the greedy insertion operator is significantly better than 2-regret and random Shaw from the start.

Fig 6. Weight of removal/insertion operators in 3000 iterations on instance A-n32.
https://doi.org/10.1371/journal.pone.0284971.g006

However, both the new accepted solution and the new better solution are rewarded in the adaptive mechanism. The highest weight
operator may not have a better performance for getting the new best solution. We use %IBest/%Usage to measure operators’
performance for getting a new best solution, where %IBest is the percentage of the best solution updated times of an operator to
the total best solution updated times, and %Usage is the percentage of an operator used times to the iteration times. Table 6 shows
which operator is more likely to update the best solution.

Table 6. Performance of operators (%IBest/%Usage).
https://doi.org/10.1371/journal.pone.0284971.t006

For removal operators, Shaw and random removal operators have a better performance, but the difference between each removal
operator is insignificant. On the other hand, for insertion operators, the greedy insertion operator significantly outperforms the
others. However, it does not mean that worse-performance operators are unnecessary. Table 7 shows the performance of ALNS
without one operator (short for no*). The baseline is ALNS.

Table 7. Performance of ALNS without * operator (Gaps).
https://doi.org/10.1371/journal.pone.0284971.t007

It shows that the ALNS with all operators has a better objective value, although fewer operators reduce computation time. This is
because although 2-regret and random Shaw insertion operators have insufficient ability to find new optimal solutions, they
contribute to exploration ability. In LNS, finding and accepting sub-optimal solutions helps prevent the algorithm from getting stuck
in local optima. The result also shows the periodic post-optimization procedure improves the objective by 0.64% on average.

5.5 Comparing ALNS with GA

Genetic algorithm (GA) is also a classic algorithm for solving combinatorial optimization problems. Zheng and Zhou (2019) propose
a GA for the robust inventory routing problem [26]. The problem they studied considers the effect of routing decisions on lead time
but with only one replenishment mode. We compare the results between ALNS and GA on all instances of the Augerat set in Table
8. The baseline is ALNS.

https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0284971

11/14

2026/4/16 02:33

Robust dual sourcing inventory routing optimization for disaster relief | PLOS One

Table 8. Comparing ALNS with GA.
https://doi.org/10.1371/journal.pone.0284971.t008

Due to the obvious difference in the efficiency and improvement of the solution in a single iteration of GA and ALNS, for fairness, we
only use 1h running time as the termination criteria. The results show that the average performance of ALNS is 16.31% better than
that of GA, and ALNS performed better than GA in all instances.

6 Conclusions

This paper studies a dual-sourcing inventory routing problem and proposes a robust model. By taking the transportation time as the
replenishment lead time, the model considers the problem that the arrival time is highly related to the replenishment quantity in the
context of disaster relief. Through air-land transportation, each shelter has two replenishment modes. There are four situations:
replenished by truck, by helicopter, by both, and by no replenishment. The mode selection depends on the trade-off between the
routing cost and the inventory cost instead of the predetermined. According to the worst case of cumulative demand under the
uncertainty set of budget, we derive the closed-form solution of the optimal replenishment quantity. In addition, our optimality
conditions do not require any specific uncertainty set. An adaptive large neighborhood search algorithm is developed for the
problem.

The numerical experiments examine the proposed model and algorithm on the benchmark instance set. Results show that the
logistic cost is effectively reduced when considering the impact of transportation time on lead time. In addition, the dual-sourcing
policy is significantly better than only using one replenishment mode. We further test the developed algorithm and show the
proposed operators improve the performance of the adaptive large neighborhood search algorithm on the problem. Finally, the
comparative experiment validates the proposed algorithm has a better performance than the genetic algorithm.

As with any research, ours begs for further extensions. Considering the impact of routing decisions on replenishment quantity,
capacity-constrained multi-vehicle problem is a challenge. Additionally, considering the impact of routing decisions on lead time in a
multi-period inventory policy helps address some practical issues in perishables supply chains.

Supporting information

S1 Appendix. Proof of proposition.
https://doi.org/10.1371/journal.pone.0284971.s001
(DOCX)

Acknowledgments

This work is supported by the National Natural Science Foundation of China under Grant No.71971011.

References

1.

Zhang L, Liu X, Li Y, Liu Y, Liu Z, Lin J, et al. Emergency medical rescue efforts after a major earthquake: lessons from the 2008 Wenchuan earthquake.
The Lancet. 2012;379(9818):853–861.
View Article

Google Scholar

2.

Beresford A, Pettit S. Humanitarian aid logistics: the Wenchuan and Haiti earthquakes compared. In: Supply Chain Management: Concepts,
Methodologies, Tools, and Applications. IGI Global; 2013. p. 666–687.

https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0284971

12/14

2026/4/16 02:33

Robust dual sourcing inventory routing optimization for disaster relief | PLOS One

3.

Zhang M, Yu J, Zhang Y, Yu H. Programming model of emergency scheduling with combined air–ground transportation. Advances in Mechanical
Engineering. 2017;9(11):168781401773951.
View Article

Google Scholar

4.

Bell WJ, Dalberto LM, Fisher ML, Greenfield AJ, Jaikumar R, Kedia P, et al. Improving the distribution of industrial gases with an on-line computerized
routing and scheduling optimizer. Interfaces. 1983;13(6):4–23.
View Article

Google Scholar

5.

Van Wassenhove LN. Humanitarian aid logistics: supply chain management in high gear. Journal of the Operational Research Society. 2006;57(5):475–
489.
View Article

Google Scholar

6.

Awan AG, Shafiq M. Supply chain management in humanitarian relief logistics. Industrial Engineering Letters;5(10):12–22.
View Article

Google Scholar

7.

Balcik B, Bozkir CDC, Kundakcioglu OE. A literature review on inventory management in humanitarian supply chains. Surveys in Operations Research
and Management Science. 2016;21(2):101–116.
View Article
Google Scholar

8.

Holguín-Veras J, Pérez N, Jaller M, Van Wassenhove LN, Aros-Vera F. On the appropriate objective function for post-disaster humanitarian logistics
models. Journal of Operations Management. 2013;31(5):262–280.
View Article

Google Scholar

9.

Çankaya E, Ekici A, Özener OÖ. Humanitarian relief supplies distribution: An application of inventory routing problem. Annals of Operations Research.
2019;283:119–141.
View Article

Google Scholar

10.

Zheng W, Zhou H. Routing problem with multiple transportation modes considering road damage. In: Proceedings of the 2018 International Conference on
Computer Modeling, Simulation and Algorithm (CMSA 2018); 2018. p. 250–253.

11.

Balcik B, Yanıkoğlu İ. A robust optimization approach for humanitarian needs assessment planning under travel time uncertainty. European Journal of
Operational Research. 2020;282(1):40–57.
View Article

Google Scholar

12.

13.

Yang X, Hao W, Lu Y. Inventory slack routing application in emergency logistics and relief distributions. PloS One. 2018;13(6):e0198443. pmid:29902196
View Article

Google Scholar

PubMed/NCBI

Qiu BJ, Zhang JH, Qi YT, Liu Y. Grey-theory-based optimization model of emergency logistics considering time uncertainty. PLoS One.
2015;10(9):e0139132. pmid:26417946
View Article

Google Scholar

PubMed/NCBI

14.

Soyster AL. Convex programming with set-inclusive constraints and applications to inexact linear programming. Operations Research. 1973;21(5):1154–
1157.
View Article

Google Scholar

15.

Ben-Tal A, Nemirovski A. Robust convex optimization. Mathematics of Operations Research. 1998;23(4):769–805.
View Article

Google Scholar

16.

Bertsimas D, Thiele A. A robust optimization approach to inventory theory. Operations Research. 2006;54(1):150–168.
View Article

Google Scholar

17.

Levi R, Pál M, Roundy RO, Shmoys DB. Approximation algorithms for stochastic inventory control models. Mathematics of Operations Research.
2007;32(2):284–302.
View Article

Google Scholar

18.

Mamani H, Nassiri S, Wagner MR. Closed-form solutions for robust inventory management. Management Science. 2017;63(5):1625–1643.
View Article

Google Scholar

19.

Sun J, Van Mieghem JA. Robust dual sourcing inventory management: optimality of capped dual index policies and smoothing. Manufacturing & Service
Operations Management. 2019;21(4):912–931.
View Article
Google Scholar

20.

Ji Y, Li H, Zhang H. Risk-averse two-stage stochastic minimum cost consensus models with asymmetric adjustment cost. Group Decision and
Negotiation. 2022;31(2):261–291. pmid:34334953
View Article
Google Scholar

PubMed/NCBI

21.

Qu S, Wei J, Wang Q, Li Y, Jin X, Chaib L. Robust minimum cost consensus models with various individual preference scenarios under unit adjustment
cost uncertainty. Information Fusion. 2023;89:510–526.
View Article

Google Scholar

22.

Dror M, Ball M. Inventory/routing: reduction from an annual to a short-period problem. Naval Research Logistics (NRL). 1987;34(6):891–905.

https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0284971

13/14

2026/4/16 02:33

Robust dual sourcing inventory routing optimization for disaster relief | PLOS One

View Article

Google Scholar

23.

Archetti C, Bertazzi L, Laporte G, Speranza MG. A branch-and-cut algorithm for a vendor-managed inventory-routing problem. Transportation Science.
2007;41(3):382–391.
View Article

Google Scholar

24.

Hvattum LM, Løkketangen A, Laporte G. Scenario tree-based heuristics for stochastic inventory-routing problems. INFORMS Journal on Computing.
2009;21(2):268–285.
View Article

Google Scholar

25.

Li M, Wang Z, Chan FT. An inventory routing policy under replenishment lead time. IEEE Transactions on Systems, Man, and Cybernetics: Systems.
2016;47(12):3150–3164.
View Article

Google Scholar

26.

Zheng W, Zhou H. Robust inventory routing problem with replenishment lead time. In: 2019 IEEE International Conference on Industrial Engineering and
Engineering Management (IEEM); 2019. p. 825–829.

27.

Sanada T, Ishigaki A, Yaginuma H. Modeling of inventory routing problem considering road closures. In: 2021 IEEE 12th International Workshop on
Computational Intelligence and Applications (IWCIA); 2021. p. 1–6.

28.

Shaw P. Using constraint programming and local search methods to solve vehicle routing problems. In: International Conference on Principles and
Practice of Constraint Programming; 1998. p. 417–431.

29.

Ropke S, Pisinger D. An adaptive large neighborhood search heuristic for the pickup and delivery problem with time windows. Transportation Science.
2006;40(4):455–472.
View Article

Google Scholar

30.

Coelho LC, Cordeau JF, Laporte G. The inventory-routing problem with transshipment. Computers and Operations Research. 2012;39(11):2537–2548.
View Article

Google Scholar

31.

Liu W, Ke GY, Chen J, Zhang L. Scheduling the distribution of blood products: A vendor-managed inventory routing approach. Transportation Research
Part E: Logistics and Transportation Review. 2020;140:101964.
View Article

Google Scholar

https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0284971

14/14

