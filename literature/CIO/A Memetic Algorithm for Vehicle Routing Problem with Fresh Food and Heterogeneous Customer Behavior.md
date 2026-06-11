A Memetic Algorithm for Vehicle Routing Problem with
Fresh Food and Heterogeneous Customer Behavior
Yankai Zhang, Kaiqi Zhao, Na Liu, Shiyi Xu, Shiwei Liang, Wenxuan Shan*
School of Transportation Science and Engineering, Beihang University, Beijing, China
*shanwenxuan@buaa.edu.cn
Abstract. The online community group-buying of fresh products is becoming
welcomed by the public. Providing customer fresh products with satisfied quality
is concerned by community group-buying distributor, as residents have diverse
requirements for delivery times and freshness, often overlooked in existing re-
search. This paper proposes a delivery route optimization model tailored for
online community group-buying, addressing the heterogeneous behavior of cus-
tomers, multiple delivery time windows, and the freshness decline of various
fresh products. We introduce a memetic algorithm for this non-linear program-
ming problem, incorporating a Split algorithm to handle multi-commodity deliv-
ery and time-varying arc costs. A dynamic allocation scheme for delivery time is
developed for optimal fixed sequences, allowing vehicles to wait within a rea-
sonable timeframe. Experimental results demonstrate that our method achieves
average reductions of 82.01% and 90.92% in comparison to classical algorithms
for instances with 50 and 100 nodes, respectively. Additionally, the proposed al-
gorithm with dynamic allocation shows an average objective function decrease
of 0.44% compared to without dynamic allocation. The allowance for waiting
during delivery enhances refrigeration conditions, offering significant manage-
rial insights into maintaining product freshness.
Keywords: Vehicle routing problem, Perishability, Online community group-
buying, Split delivery
1 Introduction
Online community group-buying has emerged as a primary method for acquiring daily
fresh products. According to a report by the National Bureau of Statistics of China, the
community group-buying market size is projected to reach 1301.74 billion RMB by
2024 [1][2]. The increasing demand and diverse requirements necessitate that online
community group-buying distributors meticulously design their delivery services to
meet the unique characteristics of fresh products and the evolving needs of residents.
The rapid freshness decline of perishable goods often results in residents receiving
less fresh items, thereby diminishing their satisfaction. Consequently, designing a de-
livery solution that transports perishable goods within specified timeframes to enhance
resident satisfaction is crucial for community group-buying. Residents exhibit diverse
© The Author(s) 2024
G. Zhao et al. (eds.), Proceedings of the 2024 7th International Symposium on Traffic Transportation and Civil
Architecture (ISTTCA 2024), Advances in Engineering Research 241,
https://doi.org/10.2991/978-94-6463-514-0_59

A Memetic Algorithm for Vehicle Routing Problem with Fresh Food 609
needs, including preferences for product types, pickup times, and freshness levels. For
instance, office workers typically retrieve purchases between 5 PM and 9 PM after work
and exhibit less concern for freshness, while senior citizens prefer pickups between 10
AM and 2 PM and have higher freshness requirements. These considerations highlight
the importance of tailored delivery solutions to accommodate the varied needs and pref-
erences of community members in community group-buying endeavors.
Since pick-up time windows vary among heterogeneous customers, multiple time
windows are considered in our study. Previous studies have addressed this aspect in
various ways. Wang et al. (2018) [3] established a multi-objective VRP optimization
model with mixed time windows and perishability. Zheng (2020) [4] developed a VRP
model with multiple fuzzy time windows to minimize travel distance and distribution
costs. Belhaiza et al. (2019) [5] proposed three multi-start data-driven evolutionary heu-
ristics.
The freshness decline of fresh products is another critical consideration, as it directly
affects customer satisfaction and incurs potential costs. Li and Li (2022) [6] described
deterioration cost as a linear function of delivery time. Leng et al. (2020) [7] and others
(Chen, 2021; Chen, 2023; Zhang, 2023; Yang, 2023) [8][9][10][11] modeled freshness
decline over delivery time as a negative exponential function. Yang and Tao (2023)
[11] linked freshness to customer satisfaction, dividing freshness decline into three
stages. Deng et al. (2021) [12] considered temperature's effect on deterioration as dif-
ferent decline rates.
Traditional community group-buying approaches have investigated the vehicle rout-
ing problem with multiple time windows and addressed issues concerning freshness
decline. We introduce a memetic algorithm to tackle the nonlinear programming chal-
lenges posed by these factors. This algorithm allows delivery vehicles to wait proac-
tively after serving a community node to optimize delivery times.
2 Problem Description
In contrast to the door-to-door delivery typical of conventional e-commerce platforms,
products in community group-buying are initially delivered to the group-buying lead-
er's location. Customers then pick up their products from the leader at their conven-
ience. The time gap between the delivery to leader and the subsequent pick-up by cus-
tomers can lead to a further decline in quality of fresh products. Customers not only
care about loss of freshness but also expect to collect their products within a convenient
time interval, referred to in this study as pick-up time windows. If fresh products are
delivered to the group-buying leader after a customer's pick-up time window, the cus-
tomer may be unable to collect them that day, significantly increasing penalty costs.
Customers can typically be categorized into several types based on their features.
Each type of customer has different pick-up time windows and requirements for fresh-
ness. Delivering products too early may result in prolonged storage at the group-buying
leader's location, while delivering too late will miss customers' pick-up time windows.
In community group-buying, customers demand multiple types of fresh products, but
the capacity of the delivery vehicle and the types of products it can carry are limited.

610 Y. Zhang et al.
Multiple delivery services may be required with different products delivered each time.
This study aims to determine the types of fresh products loaded on each vehicle and
to optimize the routes of each vehicle to minimize the total cost, which includes trans-
portation and penalty costs for breaches in freshness or pick-up time windows.
Fig. 1. Delivery Routes Fig. 2. The penalty cost at community 5
Figure 1 illustrates an example of online community group-buying involving two
types of fresh products and three types of customers. Among the eight communities,
Communities 1 and 6 require both types of fresh products. Community 1 is served only
once by Route 1, while Community 6 must be served by Routes 2 and 3, each delivering
only one type of product. Figure 2 demonstrates penalty cost at community 5. The hor-
izontal axis is time, and vertical axis represents windows for retirees, housewives, and
office workers. The pick-up time windows are 10:00 to 13:00, 15:00 to 18:00, and 17:00
to 21:00, respectively. For housewives and office workers, fresh products are delivered
earlier than their pick-up time windows, resulting in freshness decline both within the
vehicle and at the leader's location. For retirees, the fresh products are delivered later
than their pick-up time window. They can receive fresh products once delivered, but
the delayed delivery will incur higher return costs.
3 Mathematical Model
3.1 Assumptions
(1) The same type of fresh products in each community is served exclusively by a
single vehicle.
(2) The transportation process is considered uniform, with no additional time con-
sumption throughout the entire delivery process.
(3) The freshness of the delivered fresh products significantly influences residents'
decisions to return the products, with other factors being disregarded.
3.2 Penalty Cost During Delivery
Fresh product delivery in online community group-buying entails additional consider-
ations beyond basic transportation costs, which is divided into three components.

A Memetic Algorithm for Vehicle Routing Problem with Fresh Food             611
The perishable nature of fresh products leads to damage costs due to freshness de-
cline during delivery. These costs are estimated using the first-order reaction dynamics
model, as described by Hsu et al. (2007) [13]. Freshness decline correlates with both
transportation time and storage duration at leader’s location, which is defined as fol-
lows.
(1)
(cid:2869) (cid:2879)(cid:3080)(cid:3291)(cid:3047)
(cid:1832)(cid:3043)((cid:1872))=(cid:1857) (2)
(cid:2870) (cid:2879)(cid:3081)(cid:3291)(cid:3047)
 and  denote the fresh(cid:1832)(cid:3043)ne(s(cid:1872)s) d=ec(cid:1857)line for product  after transportation time
t a(cid:2869)nd storage (cid:2870)duration t, respectively. The coefficients  and  are the respective
(cid:1832)(cid:3043)((cid:1872)) (cid:1832)(cid:3043)((cid:1872))
(cid:1868)
freshness decline rates. Penalty costs due to freshness decline are calculated as follows:
|     |     |     | (cid:2009)(cid:3043) (cid:2010)(cid:3043) |     |
| --- | --- | --- | ----------------------------------------- | --- |
(3)
|     | (cid:2906) (cid:2903) |     | (cid:2869) (cid:2903) |     |
| --- | --------------------- | --- | --------------------- | --- |
(cid:1834)(cid:3039)(cid:3043)((cid:2028)(cid:3036)(cid:3038))=(cid:2033)(100%−(cid:1832)(cid:3043)((cid:2028)(cid:3036)(cid:3038))) (4)
|     | (cid:2896) (cid:2903) |     | (cid:2870) (cid:2889) (cid:2903) |     |
| --- | --------------------- | --- | -------------------------------- | --- |
where  and (cid:1834)(cid:3039)(cid:3043)((cid:2028)(cid:3036)(cid:3038)) =in(cid:2033)di(c1a0te0 t%he− pe(cid:1832)n(cid:3043)a(l(cid:2018)ty(cid:3036)(cid:3039) c−os(cid:2028)ts(cid:3036)(cid:3038) d)u)ring delivery and storage,
respective(cid:2906)ly.(cid:2903)  is unl(cid:2896)oadi(cid:2903)ng start time of vehicle  at community , which  is
| (cid:1834)(cid:3039)(cid:3043)((cid:2028)(cid:3036)(cid:3038)) | (cid:1834)(cid:3039)(cid:3043)((cid:2028)(cid:3036)(cid:3038)) |     |     |     |
| -------------------------------------------------------------- | -------------------------------------------------------------- | --- | --- | --- |
the penalty cost(cid:2903) related to freshness decline.
(cid:3036) (cid:3038)
Late delive(cid:2028)ri e s decrease customer satisfaction, lead(cid:1863)ing to return cost(cid:1861)s. The pen(cid:2033)alty
cost for late delivery is defined as:
(5)
|     | (cid:2904) | (cid:2903) (cid:2903) | (cid:2896) |     |
| --- | ---------- | --------------------- | ---------- | --- |
where  represents th(cid:1834)e(cid:3039) (cid:3043)p(e(cid:2028)n(cid:3036)(cid:3038)a)lty= c(cid:1853)o(s(cid:2028)t (cid:3036)f(cid:3038)o−r l(cid:2018)at(cid:3036)e(cid:3039)) delivery. If delivery occurs after
the latest (cid:2904)pick(cid:2903)up time , the delay time is , with  being the penalty cost
(cid:1834)(cid:3039)(cid:3043)((cid:2028)(cid:3036)(cid:3038))
| coefficient for delays. | (cid:3013) |     | (cid:2903) (cid:2896) |     |
| ----------------------- | ---------- | --- | --------------------- | --- |
,  a(cid:2018)n (cid:3036)(cid:3039) d  are refer(cid:2028)r (cid:3036) e (cid:3038) d− to(cid:2018)  (cid:3036) a (cid:3039) s Type (cid:1853)I, Type II, and Type III
penal(cid:2906)ty c(cid:2903)osts, re(cid:3013)spe(cid:2903)ctively. To(cid:2904)tal p(cid:2903)enalty cost, , can be computed as follows.
| (cid:1834)(cid:3039)(cid:3043)((cid:2028)(cid:3036)(cid:3038)) (cid:1834)(cid:3039)(cid:3043)((cid:2028)(cid:3036)(cid:3038)) | (cid:1834)(cid:3039)(cid:3043)((cid:2028)(cid:3036)(cid:3038)) |     |     |     |
| ----------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------- | --- | --- | --- |
(cid:2903)
|     |     |            | (cid:1834)(cid:3039)(cid:3043)((cid:2028)(cid:3036)(cid:3038)) ， |            |
| --- | --- | ---------- | ---------------------------------------------------------------- | ---------- |
|     |     | (cid:2903) | (cid:2870)，(cid:2889) (cid:2903) (cid:2903)                      | (cid:2889) |
(cid:2869) (6)
|                                                                           | (cid:2033)(200%−(cid:1832)(cid:3043)((cid:2028)(cid:3036)(cid:3038))−(cid:1832)(cid:3043)((cid:2018)(cid:3036)(cid:3039)−(cid:2028)(cid:3036)(cid:3038))) |                       | (cid:2028)(cid:3036)(cid:3038)                                                                 | <(cid:2018)(cid:3036)(cid:3039) |
| ------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------- | ---------------------------------------------------------------------------------------------- | ------------------------------- |
|                                                                           |                                                                                                                                                           | (cid:2903)            | (cid:2889) (cid:2903)，                                                                         | (cid:2896)                      |
| (cid:2903)                                                                |                                                                                                                                                           | (cid:2869)            |                                                                                                |                                 |
| (cid:1834)(cid:3039)(cid:3043)((cid:2028)(cid:3036)(cid:3038))=(cid:3422) | (cid:2033)(100%−(cid:1832)(cid:3043)((cid:2028)(cid:3036)(cid:3038)))                                                                                     |                       | (cid:2018)(cid:3036)(cid:3039) <(cid:2028)(cid:3036)(cid:3038) <(cid:2018)(cid:3036)(cid:3039) |                                 |
|                                                                           |                                                                                                                                                           | (cid:2869) (cid:2903) | (cid:2903) (cid:2896) (cid:2903)                                                               | (cid:2896)                      |
Figures 3 illustrate the(cid:2033) f(u1n0c0ti%on −cu(cid:1832)r(cid:3043)ve(s(cid:2028) (cid:3036)o(cid:3038)f) T)y+pe(cid:1853) (I,(cid:2028) T(cid:3036)(cid:3038)y−pe(cid:2018) I(cid:3036)I(cid:3039),) and(cid:2028) (cid:3036)T(cid:3038)y>pe(cid:2018) I(cid:3036)I(cid:3039)I penalty costs,
along with the total penalty cost.
(a) Type Ⅰ penalty cost (b) Type Ⅱ penalty cost

612 Y. Zhang et al.
(c) Type Ⅲ penalty cost (d) Total penalty cost
Fig. 3. The function curves of penalty costs
3.3 Mathematical Model
Table 1. Notations in the proposed model
Type Notation Description
, a complete undirected network, denotes the set of nodes and
represents the set of arcs in the network
(cid:1833)Se=t o{f(cid:1848) co,(cid:1827)m}munities, , r(cid:1848)epresents the number of commu-
(cid:1833)
(cid:1827)nities
Set of nodes including(cid:1840) th=e {d1e,p⋯ot ,a|n(cid:1840)d| }com|(cid:1840)m|unities, ,
(cid:1840)
where 0 and represent the depot for vehicles depart and return, re-
spectively, the remaining nodes represent communit(cid:1848)ies={0,1,⋯,|(cid:1840)|+1}
Sets (cid:1848) Set of custom|e(cid:1840)rs|,+1 , represents the number of customer
types
Set of fresh produc(cid:1829)ts,={1,⋯,|(cid:1838)|} |(cid:1838)|, represents the number of fresh
(cid:1829)
product types
(cid:1842)={1,⋯,|(cid:1842)|} |(cid:1842)|
(cid:1842) Set of arcs,
Set of vehicles, , represents the maximum number of
(cid:1827) (cid:1827)={((cid:1861),(cid:1862))|∀(cid:1861),(cid:1862)∈(cid:1848)}
vehicles
(cid:1837)={1,⋯,|(cid:1837)|} |(cid:1837)|
(cid:1837) Earliest service start time of the group-buying leader at community ,
(cid:1857)(cid:3036) Latest service start time of the group-buying leader at community ,(cid:1861) (cid:1861)∈(cid:1840)
(cid:1864)(cid:3036) Service time at community , where (cid:1861) (cid:1861)∈(cid:1840)
(cid:1871)(cid:3036) Demand of customer for p (cid:1861) roduct (cid:1861)∈ at (cid:1840) community , , ,
Parame- (cid:1869)(cid:3036)(cid:3039)(cid:3043) Travel cost along arc (cid:1864) , where (cid:1868) (cid:1861) (cid:1861)∈(cid:1840) (cid:1864)∈(cid:1829) (cid:1868)∈
ters (cid:1842)
(cid:1855)(cid:3036)(cid:3037) Maximum fresh produ(c(cid:1861)t ,t(cid:1862)y)pes that v(e(cid:1861)h,(cid:1862)ic)le∈(cid:1827) can load,
(cid:2025)(cid:3038) Travel time from community to , (cid:1863) (cid:1863)∈(cid:1837)
(cid:1872)(cid:3036)(cid:3037) Earliest pickup time for custom(cid:1861)er (cid:1862)at(cid:1861) c,o(cid:1862)m∈m(cid:1848)u:n(cid:1861)i≠ty(cid:1862), ,
(cid:2889)
(cid:2018)(cid:3036)(cid:3039) Latest pickup time for customer (cid:1864)at community ,(cid:1861) (cid:1861)∈(cid:1840), (cid:1864)∈(cid:1829)
(cid:2896)
(cid:2018)(cid:3036)(cid:3039) (cid:1864) (cid:1861) (cid:1861)∈(cid:1840) (cid:1864)∈(cid:1829)

A Memetic Algorithm for Vehicle Routing Problem with Fresh Food             613
Penalty cost coefficient between freshness decline and incurred costs
|     | (cid:2033) Freshness decline coefficient of product |     |  in vehicle,  |                         |
| --- | --------------------------------------------------- | --- | ------------- | ----------------------- |
|     | Freshness decline coefficient of product            |     |  at group-buy | in g  leader, where     |
|     | α(cid:3043)                                         |     | (cid:1868)    | (cid:1868) ∈ (cid:1842) |
β(cid:3043) Penalty cost coefficient between the part e(cid:1868)xceeding the time window of
(cid:1868)gro∈u(cid:1842)p-buying leaders andincurred costs
Penalty cost coefficient between exceeding vehicle capacity and incurred
γ
costs
δ Maximum capacity of vehicles
(cid:1843) Maximum running time of vehicles on a delivery route
(cid:1830) A sufficiently large positive constant
|     | Load capacity of vehicle |  for product |  when departing from the depot, |     |
| --- | ------------------------ | ------------ | ------------------------------- | --- |
(cid:1839)
,
(cid:1875)(cid:3043)(cid:3038) if vehicle  trave(cid:1863)rses arc ,(cid:1868) otherwise , ,
(cid:1863)∈(cid:1837) (cid:1868)∈(cid:1842)
(cid:1876)Se (cid:3036)(cid:3037) (cid:3038) vi=ce1 start time o(cid:1863)f vehicle  at co((cid:1861)m,(cid:1862)m)unity (cid:1876)(cid:3036)(cid:3037)(cid:3038) =0 ((cid:1861),(cid:1862))∈(cid:1827) (cid:1863)∈
| Decision | (cid:1876)(cid:3036)(cid:3037)(cid:3038) r |     | ,   | ,   |
| -------- | ------------------------------------------ | --- | --- | --- |
variables
(cid:1837)
|     | (cid:2903) Total load of vehicle |  when(cid:1863) arriving at comm(cid:1861)un(cid:1861)it∈y(cid:1840), |     | (cid:1863)∈(cid:1837), |
| --- | -------------------------------- | --------------------------------------------------------------------- | --- | ---------------------- |
(cid:2028)(cid:3036) (cid:3038)
(cid:1874)(cid:3036)(cid:3038)  if vehicle (cid:1863) loads product  for communit(cid:1861)y (cid:1861), ∈ot(cid:1840)herw(cid:1863)is∈e(cid:1837)
|     | , , , |     |     |     |
| --- | ----- | --- | --- | --- |
(cid:1838)(cid:3036)(cid:3043)(cid:3038)=1 (cid:1863) (cid:1868) (cid:1861) (cid:1838)(cid:3036)(cid:3043)(cid:3038)=
| [P] | (cid:1838)(cid:3036)(cid:3043)(cid:3038)      |                       |     |     |
| --- | --------------------------------------------- | --------------------- | --- | --- |
|     | 0 (cid:1861)∈(cid:1840) (cid:1863)∈(cid:1837) | (cid:1868)∈(cid:1842) |     |     |
(7)
(cid:2903)
min(cid:3435)∑(cid:3038)∈(cid:3012)∑(cid:3036)∈(cid:3023)∑(cid:3037)∈(cid:3023)(cid:1855)(cid:3036)(cid:3037)(cid:1876)(cid:3036)(cid:3037)(cid:3038)+∑(cid:3038)∈(cid:3012)∑(cid:3036)∈(cid:3015)∑(cid:3039)∈(cid:3004)∑(cid:3043)∈(cid:3017)(cid:1834)(cid:3039)(cid:3043)(cid:3435)(cid:2028)(cid:3036)(cid:3038)(cid:3439)(cid:1869)(cid:3036)(cid:3039)(cid:3043)(cid:3439) (8)
∑(cid:3037)∈(cid:3023)(cid:1876)(cid:2868)(cid:3037)(cid:3038)
=1    ∀(cid:1863) ∈(cid:1837) (9)
∑(cid:3037)∈(cid:3023)(cid:1876)(cid:3037),|(cid:3015)|(cid:2878)(cid:2869),(cid:3038)
|     |     | =1    ∀(cid:1863) | ∈(cid:1837) | (10) |
| --- | --- | ----------------- | ----------- | ---- |
∑(cid:3037)∈(cid:3023)(cid:1876)(cid:3037)(cid:3036)(cid:3038) =∑(cid:3037)∈(cid:3023)(cid:1876)(cid:3036)(cid:3037)(cid:3038)    ∀(cid:1861) ∈(cid:1840),∀(cid:1863)∈(cid:1837) (11)
∑(cid:3038)∈(cid:3012)∑(cid:3037)∈(cid:3023)(cid:1876)(cid:3037)(cid:3036)(cid:3038) =∑(cid:3038)∈(cid:3012)∑(cid:3037)∈(cid:3023)(cid:1876)(cid:3036)(cid:3037)(cid:3038) ≥1    ∀(cid:1861) ∈(cid:1840) (12)
(cid:1838)(cid:3036)(cid:3043)(cid:3038) ≤∑(cid:3037)∈(cid:3023)(cid:1876)(cid:3036)(cid:3037)(cid:3038)    ∀(cid:1861)  (13)
∈(cid:1840),∀(cid:1868)∈(cid:1842),∀(cid:1863)∈(cid:1837)
∑(cid:3043)∈(cid:3017)min(cid:3419)1,∑(cid:3036)∈(cid:3023)(cid:1838)(cid:3036)(cid:3043)(cid:3038)(cid:3423)≤(cid:2025)(cid:3038)    ∀(cid:1863)∈(cid:1837)
(14)
min(cid:3419)1,∑(cid:3039)∈(cid:3004)(cid:1869)(cid:3036)(cid:3039)(cid:3043)(cid:3423)≤∑(cid:3038)∈(cid:3012)(cid:1838)(cid:3036)(cid:3043)(cid:3038)  ∀(cid:1861) ∈(cid:1840),∀(cid:1868) ∈(cid:1842) (15)
∑(cid:3037)∈(cid:3023)(cid:1876)(cid:3036)(cid:3037)(cid:3038) ≤∑(cid:3043)∈(cid:3017)(cid:1838)(cid:3036)(cid:3043)(cid:3038)    ∀(cid:1863) ∈(cid:1837),∀(cid:1861) ∈(cid:1840) (16)
(cid:1875)(cid:3043)(cid:3038) =∑(cid:3036)∈(cid:3015)∑(cid:3039)∈(cid:3004)(cid:1869)(cid:3036)(cid:3039)(cid:3043)(cid:1838)(cid:3036)(cid:3043)(cid:3038)    ∀(cid:1868)∈(cid:1842),∀(cid:1863)∈(cid:1837) (17)
∑(cid:3043)∈(cid:3017)(cid:1875)(cid:3043)(cid:3038)
|     |     | ≤(cid:1843)    ∀(cid:1863)∈(cid:1837) |     |   (18) |
| --- | --- | ------------------------------------- | --- | ------ |
(cid:1874)(cid:3036)(cid:3038)−∑(cid:3039)∈(cid:3004)∑(cid:3043)∈(cid:3017)(cid:1869)(cid:3036)(cid:3039)(cid:3043)(cid:1838)(cid:3036)(cid:3043)(cid:3038)+(cid:1839)(cid:3435)1−(cid:1876)(cid:3036)(cid:3037)(cid:3038)(cid:3439)≥(cid:1874)(cid:3037)(cid:3038)    ∀(cid:1861) ∈(cid:1840),∀(cid:1862)∈(cid:1840),∀(cid:1863)∈(cid:1837) (19)
(cid:1874)|(cid:3015)|(cid:2878)(cid:2869),(cid:3038) =0    ∀(cid:1863) ∈(cid:1837)

614             Y. Zhang et al.
 (20)
| (cid:2903) |     | (cid:2903) |     |     |     |
| ---------- | --- | ---------- | --- | --- | --- |
(cid:2028)(cid:3036)(cid:3038)+(cid:1871)(cid:3036) +(cid:1872)(cid:3036)(cid:3037)−(cid:1839)(cid:3435)1−(cid:1876)(cid:3036)(cid:3037)(cid:3038)(cid:3439)≤(cid:2028)(cid:3037)(cid:3038)    ∀(cid:1861)
|     |     |     | ∈(cid:1840),∀(cid:1862)∈(cid:1848),∀(cid:1863) | ∈(cid:1837) | (21) |
| --- | --- | --- | ---------------------------------------------- | ----------- | ---- |
(cid:2903)
(cid:2028)(cid:3036)(cid:3038) ≤(cid:1864)(cid:3036)+(cid:1839)(cid:3435)1−∑(cid:3037)∈(cid:3023)(cid:1876)(cid:3036)(cid:3037)(cid:3038)(cid:3439)    ∀(cid:1861) ∈(cid:1840),∀(cid:1863) ∈(cid:1837) (22)
(cid:3020)
(cid:2028)(cid:3036)(cid:3038) ≥(cid:1857)(cid:3036)−(cid:1839)(cid:3435)1−∑(cid:3037)∈(cid:3023)(cid:1876)(cid:3036)(cid:3037)(cid:3038)(cid:3439)    ∀(cid:1861) (23)
∈(cid:1840),∀(cid:1863) ∈(cid:1837)
|     | ∑(cid:3038)∈(cid:3012)∑(cid:3036)∈(cid:3023)(cid:1876)(cid:2868)(cid:3036)(cid:3038) |                              | ，                                |                       |     |
| --- | ------------------------------------------------------------------------------------ | ---------------------------- | -------------------------------- | --------------------- | --- |
|     |                                                                                      | ≤|(cid:1837)|    ∀(cid:1863) | ∈(cid:1837)                      |                       |     |
|     |                                                                                      | (cid:2869) (cid:2903)        | (cid:2870)，(cid:2889) (cid:2903) | (cid:2903) (cid:2889) |     |
(24)
| (cid:2033)(200%−(cid:1832)(cid:3043)((cid:2028)(cid:3036)(cid:3038))−(cid:1832)(cid:3043)((cid:2018)(cid:3036)(cid:3039)−(cid:2028)(cid:3036)(cid:3038))) |                                                                       |                       |                                                                                                | (cid:2028)(cid:3036)(cid:3038) <(cid:2018)(cid:3036)(cid:3039) |     |
| --------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------- | --------------------- | ---------------------------------------------------------------------------------------------- | -------------------------------------------------------------- | --- |
| (cid:2903)                                                                                                                                                |                                                                       | (cid:2869) (cid:2903) | (cid:2889) (cid:2903)，                                                                         | (cid:2896)                                                     |     |
| (cid:1834)(cid:3039)(cid:3043)((cid:2028)(cid:3036)(cid:3038))=(cid:3422)                                                                                 | (cid:2033)(100%−(cid:1832)(cid:3043)((cid:2028)(cid:3036)(cid:3038))) |                       | (cid:2018)(cid:3036)(cid:3039) <(cid:2028)(cid:3036)(cid:3038) <(cid:2018)(cid:3036)(cid:3039) |                                                                |     |
|                                                                                                                                                           |                                                                       | (cid:2869) (cid:2903) | (cid:2903) (cid:2896)                                                                          | (cid:2903) (cid:2896)                                          |     |
The notations in the p(cid:2033)r(o1p0os0e%d m−o(cid:1832)d(cid:3043)e(l (cid:2028)i(cid:3036)s(cid:3038) s)h)o+w(cid:1853)n (i(cid:2028)n(cid:3036) (cid:3038)T−ab(cid:2018)le(cid:3036) (cid:3039)1). T(cid:2028)h(cid:3036)e(cid:3038) m>o(cid:2018)d(cid:3036)e(cid:3039)l is mathemati-
cally represented using the arc-flow model [P]. The objective function aims to minimize
the total cost, which comprises both basic travel costs and total penalty costs. Con-
straints ensure that each vehicle departs from and returns to the depot (Constraints 8-
9). Each vehicle must arrive at and leave a community after service is completed (Con-
straint 10), and each community must be served by at least one vehicle (Constraint 11).
Vehicles serve a community only if they pass through it (Constraint 12). Constraints on
product types include limiting the number of product types each vehicle can load (Con-
straint 13), ensuring product delivery when there is demand in a community (Constraint
14), and requiring vehicles to deliver at least one type of product if they pass through a
community (Constraint 15). The total load must match the demand (Constraint 16),
within vehicle capacity limits (Constraint 17). The model calculates vehicle loads at
each community (Constraint 18) and mandates complete unloading before returning to
the depot (Constraint 19). Arrival times are calculated (Constraint 20), and time win-
dows are enforced (Constraints 21-22). The number of vehicles is capped (Constraint
23), and the penalty cost function is included (Constraint 24).
4 Algorithm
4.1 Overview
The classical algorithm is introduced by Christian Prins (2004)14. Our proposed me-
metic algorithm incorporates three enhancements into the foundational framework of
the traditional approach. First, it considers three types of penalty costs. Second, the split
algorithm network is constructed following the addition of cloned points, with the for-
mulation of arc costs in the split network provided. Third, the dynamic allocation pro-
cess is conducted to optimize delivery times. Algorithm 1 illustrates the entire process
of the tailored memetic algorithm, with individual components detailed in the following
sections.
Algorithm 1. VRPTWMTMC
1: Initialize population according to the greedy strategy
2: Split each solution (route allocation procedure)
3: while number of iterations without improvement , and time < do
|     |     |     | <(cid:1835)(cid:3031) | (cid:1846)(cid:3040)(cid:3028)(cid:3051) |     |
| --- | --- | --- | --------------------- | ---------------------------------------- | --- |

A Memetic Algorithm for Vehicle Routing Problem with Fresh Food 615
4: Select parent solutions and using elite selection
5: Generate offspring from and (crossover)
(cid:1842)(cid:2869) (cid:1842)(cid:2870)
6: Split (route allocation procedure)
C (cid:1842)(cid:2869) (cid:1842)(cid:2870)
7: Educate (local search procedure)
C
8: Allocation C (delivery time optimization procedure)
C
9: if infeasible then
Assign into infeasible subpopulation,
C
Repair with probability
C
10: if C feasiblethen
(cid:1842)(cid:3045)(cid:3032)(cid:3043)
Insert into feasible subpopulation
11: if reaching maximum subpopulationthen
C
Select survivors
12: if best solution not improved for iterations,then
Diversify population
(cid:1835)(cid:3031)
13: end while
14: Return best feasible solution
4.2 Solution Representation
A chromosome is a series of unseparated nodes, each containing information about a
community and the demand for a specific product within that community. Given the
order of nodes in a chromosome, the corresponding optimal solution can always be
obtained using the Split algorithm.
An example is shown in Figure xx, where the solution representation is divided into
four steps. In Figure 4, all the routes for delivering each commodity are indicated. If a
community is regarded as multiple nodes based on commodity types, the multiple sim-
ultaneous delivery route solutions of Figure 4 (a) can be combined and transformed into
Figure 4 (b). Figure 4 (c) represents the corresponding delivery pattern. The final solu-
tion representation with separators is shown in Figure 4 (d).
(a) Delivery Routes (b) Delivery solution
(c) Delivery Pattern (d) Solution Representation
Fig. 4.Theexample of solution representation

616             Y. Zhang et al.
4.3 Split Algorithm
The split algorithm requires the sequential order of all nodes and determines the costs
associated  with  any  segment  of .  The  cost  associated  with
 is formulated as follows:
|     |     | arc((cid:1861),(cid:1862)),(cid:1861),(cid:1862) | ∈V  |     |
| --- | --- | ------------------------------------------------ | --- | --- |
arc((cid:1861),(cid:1862)),(cid:1861),(cid:1862)ϵV
(25)
|     |     | (cid:3037)(cid:2879)(cid:2869) | (cid:3037) |     |
| --- | --- | ------------------------------ | ---------- | --- |
(cid:1858)(cid:3036)(cid:3037) =(cid:1855)(cid:2868),(cid:3036)(cid:2878)(cid:2869)+(cid:1855)(cid:3037),(cid:2868)+∑(cid:3035)(cid:2880)(cid:3036)(cid:2878)(cid:2869)(cid:1855)(cid:3035),(cid:3035)(cid:2878)(cid:2869)+∑(cid:3035)(cid:2880)(cid:3036)(cid:2878)(cid:2869)∑(cid:3039)∈(cid:3004)∑(cid:3043)∈(cid:3017)(cid:1834)(cid:3039)(cid:3043)((cid:2028)(cid:3035)(cid:3038))(cid:1869)(cid:3035)(cid:3039)(cid:3043)+
(cid:3037)
∑(cid:3035)(cid:2880)(cid:3036)(cid:2878)(cid:2869)γmax((cid:2028)(cid:3035)(cid:3038)−(cid:1864)(cid:3035),0)+δmax(∑(cid:3043)∈(cid:3017)(cid:1875)(cid:3043)(cid:3038)−(cid:1843),0),(cid:1863)
∈(cid:1837)
(26)
|     | (cid:2903) |     | (cid:2903) |     |
| --- | ---------- | --- | ---------- | --- |
 repre(cid:2028)s(cid:3036)e(cid:3038)n+ts (cid:1871)th(cid:3036)e+ to(cid:1872)t(cid:3036)a(cid:3037)l− co(cid:1839)st(cid:3435) o1f −a d(cid:1876)e(cid:3036)(cid:3037)l(cid:3038)iv(cid:3439)e≤ry (cid:2028)r(cid:3037)o(cid:3038)u,t(cid:1863)e ∈vis(cid:1837)it(i2ng5 )communities from
where  to
.  is the fundamental delivery cost from the depot to the first community , and
 is t(cid:1858)h (cid:3036) (cid:3037)  is the basic (cid:1861)cost
| e   |  cost from the last community |     |  back to the depot. |     |
| --- | ----------------------------- | --- | ------------------- | --- |
(cid:1855)(cid:2868),(cid:3036)(cid:2878)(cid:2869)
(cid:1862) (cid:1861)
from community  to community . Therefore,  represents the total
(cid:1855)(cid:3037),(cid:2868) (cid:1862) (cid:1855)(cid:3035),(cid:3035)(cid:2878)(cid:2869)
delivery cost for a vehicle to deliver between communitie(cid:3037)(cid:2879)s.(cid:2869)
|               | ℎ   |  inℎc+lud1es the penalty | ∑ (cid:3035) (cid:2880) (cid:3036) s(cid:1855)t  (cid:3035) ,(cid:3035) (cid:2878) | (cid:2869)           |
| ------------- | --- | ------------------------ | ---------------------------------------------------------------------------------- | -------------------- |
| Additionally, |     |                          |   c o a s s                                                                        | ociated with serving |
different customers in different communities.  denotes the penalty cost
 foarr cp(r(cid:1861)o,d(cid:1862)u),c(cid:1861)t,(cid:1862)∈ aVt community
| for customer |     |     | . Consequently, the total penalty cost |     |
| ------------ | --- | --- | -------------------------------------- | --- |
(cid:1834)(cid:3039)(cid:3043)((cid:2028)(cid:3035)(cid:3038))(cid:1869)(cid:3035)(cid:3039)(cid:3043)
| can be expressed as |            |            | . If |  does not satisfy |
| ------------------- | ---------- | ---------- | ---- | ----------------- |
|                     | (cid:1864) | (cid:1868) | ℎ    |                   |
the time window cons(cid:3037)traint or the capacity constraint, a corresponding penalty cost
∑(cid:3035)(cid:2880)(cid:3036)∑(cid:3039)∈(cid:3004)∑(cid:3043)∈(cid:3017)(cid:1834)(cid:3039)(cid:3043)((cid:2028)(cid:3035)(cid:3038))(cid:1869)(cid:3035)(cid:3039)(cid:3043)
arc((cid:1861),(cid:1862)),(cid:1861),(cid:1862)∈V
|     |     |  or |  is incurred, respectively. |     |
| --- | --- | --- | --------------------------- | --- |
(cid:3037)Figure 5 illustrates an example of the split algorithm. Figure 5 (a) depicts solutions
∑ (cid:3035) (cid:2880) (cid:3036) (cid:2878) (cid:2869)  aγnmd a4x d ( e(cid:2028)l (cid:3035) (cid:3038) ve−ry(cid:1864)  (cid:3035) ro,0ut ) es, reδspmeacxti(v ∑ (cid:3043) ∈ (cid:3017)  T(cid:1875)h (cid:3043) (cid:3038) se− tw(cid:1843)o, s0o)lutions can be transformed into
| w i t h   3 | i   | el y . | e   |     |
| ----------- | --- | ------ | --- | --- |
the directed acyclic graph shown in Figure 5 (b). In this graph, each arc cost is calcu-
lated by summing all the costs along the arc. For a fixed sequence order of nodes, the
corresponding optimal solution with separators can be obtained using Bellman’s algo-
rithm (Prins, C., 2004). In this example, the optimal solution is shown in Figure 5 (c).
|     |     | (a) Split network |     |     |
| --- | --- | ----------------- | --- | --- |
(b) Directed acyclic graph

A Memetic Algorithm for Vehicle Routing Problem with Fresh Food 617
(c) Vehicle routing solution after split
Fig. 5. The example of Split algorithm
4.4 Crossover
Two parents are randomly selected from the population, and Ox crossover (Prins, C.,
2004) is used in our algorithm. Ox crossover is advantageous as it can inherit favorable
access sequences from both parents and rearrange the sequence of community nodes.
4.5 Education
After the crossover process, a local search method shown in Figure 6 is employed in
place of mutation operators to improve solutions. Each operation traverses all possible
pairs (u,v) within the routes. Let x and y denote the next nodes of u and v. T(u) is the
route of node u.
M1. If u is a client node, remove u then insert it after v,
M2. If u and x are clients, remove them then insert (u, x) after v,
M3. If u and x are clients, remove them then insert (x, u) after v,
M4. If u and v are clients, swap u and v,
M5. If u, x and v are clients, swap (u, x) and v,
M6. If (u, x) and (v, y) are clients, swap (u, x) and (v, y),
M7. If T(u) T(v), replace (u, x) and (v, y) by (u, v) and (x, y),
M8. If T(u) T(v), replace (u, x) and (v, y) by (u, v) and (x, y),
M9. If T(u) = T(v), replace (u, x) and (v, y) by (u, y) and (x, v).
≠
≠
(a) M1 (b) M2 (c) M3
(d) M4 (e) M5 (f) M6

618 Y. Zhang et al.
(g) M7 (h) M8 (i) M9
Fig. 6. Education operators
4.6 Dynamic Allocation of Delivery Time
For a sequence of fixed-order nodes optimized by education, the delivery time of each
community node is uniquely determined for continuous delivery by vehicles. However,
poor refrigeration equipment at some group-buying leaders leads to greater freshness
decline during storage. If there is a large gap between the customer pickup time and the
delivery time, a more optimal delivery solution involves vehicles pausing the delivery,
waiting until it is closer to the customer pickup time, and then unloading, ensuring a
better storage environment while waiting for pickup. Therefore, we propose a dynamic
allocation of delivery time to enable proactive waiting by vehicles.
During the dynamic allocation process, the delivery time of each community node
can be shifted backward within a reasonable range to allow for vehicle waiting. The
wait cannot exceed the latest time window at the group-buying leader of this node,
ensuring time window compliance. The allowable adjustment also cannot exceed the
minimum of the interval between delivery time and the latest time window at the group-
buying leader for all subsequent nodes in the route. This satisfies the time window con-
straints for the subsequent nodes. After determining the adjustable time range, a greedy
algorithm optimizes the delivery time to minimize the penalty cost of each node.
Fig. 7. The example of delivery time dynamic allocation
As shown in Figure 7, the black and red lines represent solutions before and after
dynamic allocation, respectively. For community node 1, the range of allowed adjust-
ment is small because the time window at the head of node 2 is narrow and needs to
satisfy the time window constraints at node 2. For node 2, it has been forced to be
delayed to the latest pickup time of the node, and no adjustment can be made. For node

A Memetic Algorithm for Vehicle Routing Problem with Fresh Food 619
3, to satisfy the current node's head of the node's time window, it can only be allowed
to be adjusted up to the lower bound of the time window. For node 4, since there is no
other node and the time window range of this node is larger, the adjustment range is
larger. Each node takes the optimal delivery time within the allowed adjustment range
to minimize the penalty cost of the node.
5 Experiment Results
5.1 Instance Generation
The instances used for the experiments are generated based on Solomon benchmark
instances, encompassing 50 and 100 community nodes. These instances include types
R (Random), C (Clustered), and RC (Random-Clustered). For each type, we generate
two combinations based on two product types (2 and 4), resulting in a total of 54 in-
stances for both the 50-node and 100-node scenarios.
Our proposed algorithm is programmed in Java language and subjected to a compar-
ative experiment using CPLEX 12.8. All experiments are conducted on a laptop featur-
ing an AMD Ryzen 7 5800H with Radeon Graphics, 3.20 GHz 8-core 16-thread Pro-
cessor, and Windows 10 operating system. All computational times in experiments are
reported in CPU seconds. The overall execution time limit for each run of the algorithm
is set to 21600s.
5.2 Instance Results
After generating the instances, each type is solved using three different methods: a clas-
sical memetic algorithm, our proposed method without dynamic allocation, and our
proposed method with dynamic allocation. The results for the two combinations of each
instance type are averaged. The comparison of the results for the instances with 50 and
100 nodes, obtained from the three solving methods, is presented in the table below.
Table 2. Experimental results of the instances with 50 nodes
classical memetic algorithm our method
Name
cpu In. Obj. ADF Vin. cpu. In. Obj. ObjDA. ADF. Vin. gap.
C201 10830 313 13073 6.36 58 7253 142 4771 4700 24.35 62 -1.48%
C202 9985 309 5233 6.31 34 7232 197 3939 3842 9.67 153 -2.46%
C203 10254 314 24591 5.87 63 6641 395 3362 3282 4.41 235 -2.39%
C204 10815 324 17613 5.12 108 5252 474 2229 2178 2.73 132 -2.29%
C205 10828 313 16809 6.12 25 7209 234 4271 4216 13.13 134 -1.30%
C206 10830 327 3927 5.73 134 7209 238 3908 3857 11.18 97 -1.30%
C207 9023 314 10309 6.29 34 6981 345 3894 3871 6.00 266 -0.60%
C208 10839 316 25496 6.25 41 7225 206 4315 4284 12.52 114 -0.72%
R201 10815 319 86457 5.60 110 5360 398 1887 1851 3.79 235 -1.92%
R202 10820 328 25351 4.73 266 5303 434 1631 1621 3.25 303 -0.61%
R203 9290 337 44062 3.85 98 5075 474 1439 1470 2.68 281 2.11%

620 Y. Zhang et al.
R204 10819 354 54475 3.64 280 4473 479 1172 1165 2.73 239 -0.57%
R205 10844 213 66208 8.70 121 5279 363 1804 1819 5.40 185 0.84%
R206 10796 312 32132 5.65 160 4886 429 1471 1460 3.17 251 -0.77%
R207 8609 328 21188 4.36 125 4822 500 1284 1258 2.42 338 -2.01%
R208 9340 348 14348 3.63 146 4711 478 1130 1131 2.46 459 0.10%
R209 10828 278 43669 7.97 85 5358 427 1672 1673 3.28 248 0.02%
R210 10832 304 3787 7.22 47 5365 353 1623 1593 5.63 179 -1.90%
R211 10850 287 29032 7.62 173 5063 488 1455 1477 2.49 364 1.54%
RC201 10838 311 84061 10.92 34 6105 361 2241 2236 9.48 342 -0.22%
RC202 8954 341 38567 7.38 31 6057 370 2008 2051 7.86 224 2.15%
RC203 10215 374 31291 5.68 11 6043 329 1710 1734 11.16 107 1.45%
RC204 9246 376 83928 5.10 31 5801 375 1369 1387 7.60 158 1.33%
RC205 10830 278 67019 11.90 165 5519 388 2051 2028 7.16 286 -1.11%
RC206 10373 302 16744 11.95 150 6223 399 1975 1995 6.99 265 1.04%
RC207 9029 292 3818 14.16 44 6106 356 1836 1926 8.46 113 4.87%
RC208 9807 310 27001 11.37 148 5409 346 1659 1655 9.75 132 -0.25%
Legend: In: Iteration number; ADF: Average discriminate of fitness; Vin: Valid iteration number;ObjDA:
objective function with dynamic allocation
Table 3. Experimental results of the instances with 100 nodes
classical memetic algorithm our method
Name
cpu In. Obj. ADF Vin. cpu. In. Obj. ObjDA. ADF. Vin. gap.
C201 21990 155 331062 74.81 23 14487 33 8973 8892 227.38 27 -0.90%
C202 21955 168 384974 134.42 13 14602 84 7408 7328 81.72 72 -1.08%
C203 21951 55 84285 160.19 29 14517 112 5595 5494 51.98 107 -1.81%
C204 22022 65 321276 127.26 29 14470 226 4359 4383 29.59 67 0.54%
C205 21814 80 16985 138.49 23 14460 38 8236 8172 167.66 35 -0.78%
C206 21775 102 76543 127.94 21 14532 37 8042 8045 174.28 32 0.03%
C207 21853 144 32754 133.32 24 14727 47 7551 7475 114.58 46 -1.01%
C208 21845 75 46202 117.47 32 14551 69 7846 7792 104.35 68 -0.69%
R201 21910 62 165112 84.55 37 14423 100 3542 3569 49.52 63 0.74%
R202 21736 71 140236 75.90 20 14561 118 3038 3043 48.49 78 0.16%
R203 21702 87 45971 62.25 28 14574 123 2814 2766 39.22 51 -1.72%
R204 21834 188 70843 41.11 98 14440 173 2216 2204 20.65 140 -0.57%
R205 21888 75 107167 89.80 58 14520 122 3145 3092 33.90 91 -1.69%
R206 21902 90 91154 78.91 28 14458 113 2859 2855 44.25 90 -0.14%
R207 21772 65 35663 70.40 19 14454 161 2551 2500 29.42 153 -2.03%
R208 21939 225 37198 40.56 110 14428 258 2104 2147 17.15 207 2.03%
R209 22210 66 70783 110.95 27 14457 184 3030 2970 21.05 170 -1.98%
R210 22198 69 40531 101.13 24 14482 206 2939 2940 20.24 199 0.04%
R211 22292 62 39510 112.12 7 14436 243 2801 2800 24.53 193 -0.01%
RC201 22157 64 179106 170.12 37 14504 98 4162 4120 75.73 89 -0.99%
RC202 22126 132 107478 126.61 47 14492 119 3742 3780 54.92 115 0.99%
RC203 21959 105 54465 99.23 65 14486 130 3186 3176 55.97 100 -0.30%
RC204 21813 105 67927 89.24 69 14454 150 2703 2648 47.14 140 -2.04%

A Memetic Algorithm for Vehicle Routing Problem with Fresh Food 621
RC205 22032 41 139594 217.92 4 14431 107 4134 4124 74.32 87 -0.24%
RC206 21924 87 82628 178.92 47 14528 112 3671 3630 58.34 87 -1.10%
RC207 22143 73 27871 208.50 9 14435 129 3662 3613 48.96 111 -1.35%
RC208 22066 53 6634 255.74 47 14455 158 3214 3164 43.28 115 -1.56%
Legend:In: Iteration number; ADF: Average discriminate of fitness; Vin: Valid iteration number; ObjDA:
objective function with dynamic allocation
The proposed Split algorithm in our method enhances solution time and increases
the ratio of valid iterations compared to the classical memetic algorithm. The average
computation times for the classical memetic algorithm on instances with 50 and 100
nodes are 10,242 seconds and 21,956 seconds, respectively. Our algorithm solves in-
stances with 50 and 100 nodes in 5,850 seconds and 14,495 seconds, respectively, re-
ducing computation time by 36.81%.
From Table 2 and 3, our method shows a significant improvement in the percentage
of valid iterations relative to the total number of iterations. Specifically, our method
increases this percentage by 79.39% and 107.82% for instances with 50 and 100 nodes,
respectively, compared to the classical memetic algorithm. The objective function value
obtained by our method is consistently lower than that obtained by the classical me-
metic algorithm. This improvement is attributed to our method's consideration of time
windows for different customer types at each community node, which reduces penalty
costs for both early and late deliveries of fresh products. For instances with 50 and 100
nodes, our algorithm achieves average gaps of -82.01% and -90.92%, respectively,
compared to the classical memetic algorithm.
Additionally, our algorithm achieves an average gap of -0.44% compared to our pro-
posed method without dynamic allocation. This is because the dynamic allocation pro-
cess in our algorithm optimizes the delivery time of each community node, catering to
the requirements for multiple types of customers. The optimization of the delivery time
also allows fresh products to be stored in refrigerated vehicles longer, reducing the stor-
age time at group-buying leaders and thereby minimizing freshness decline.
6 Conclusion
This paper investigates the multi-commodity delivery problem in community group-
buying considering heterogeneous customer behaviors. Delivering fresh products to a
leader introduces a time gap between delivery and customer retrieval, which will result
a potential freshness decline and returns.
We develop a vehicle routing problem with multiple time windows and multiple
commodities. To solve this model, we propose a memetic algorithm based on a split
algorithm, which considers time-varying arc costs. Since waiting time has an impact on
the penalty cost, we incorporate dynamic allocation for delivery time, optimizing de-
livery schedules under fixed sequences by determining the optimized waiting time. We
validate the algorithm using 108 test instances derived from Solomon's benchmarks.
Experimental results demonstrate that our algorithm outperforms the classical memetic
algorithm in terms of solution time, objective function value, number of iterations, and
average discrimination. Specifically, it achieves average gaps of -82.01% and -90.92%

622 Y. Zhang et al.
relative to the classical memetic algorithm for instances with 50 and 100 nodes, respec-
tively, and an improvement of 0.44% with the proposed dynamic allocation.
Our proposed algorithm is limited by the independent execution of dynamic delivery
time allocation and route optimization, which are not currently integrated. Future en-
hancements could address this coupling, enabling our model and algorithm to be appli-
cable across various vehicle routing optimization scenarios with time windows.
Acknowledgments
This research was supported by the National Natural Science Foundation of China
(72201017); This work was also supported by The 17th College Students' Innovation
and Entrepreneurship Training Program.
References
1. National Bureau of Statistics, 2023. Statistical Bulletin on National Economic and Social
Development of the People's Republic of China in 2023. Accessed 22nd May, 2024,
https://www.stats.gov.cn/sj/zxfb/202402/t20240228_1947915.html.
2. Online Economic and Social Affairs, 2024. Fresh Agricultural Products and Community
Group Purchasing Market Data Report of China in 2023. Accessed 22nd May, 2024,
https://www.100ec.cn/zt/2023sxsqscbg/.
3. Wang, X. P., Wang, M., Ruan, J. H., Li, Y., 2018. Multi-objective optimization for deliver-
ing perishable products with mixed time windows. Advances in Production Engineering &
Management, 13(3): 321-332.
4. Zheng, J., 2020. A vehicle routing problem model with multiple fuzzy windows based on
time-varying traffic flow. IEEE access, 8: 39439-39444.
5. Belhaiza, S., M’Hallah, R., Ben Brahim, G., Laporte, G., 2019. Three multi-start data-driven
evolutionary heuristics for the vehicle routing problem with multiple time windows. Journal
of Heuristics, 25(3): 485-515.
6. Li, N., Li, G., 2022. Hybrid partheno-genetic algorithm for multi-depot perishable food de-
livery problem with mixed time windows. Annals of Operations Research: 1-32.
7. Leng, L., Zhang, J., Zhang, C., Zhao, Y., Wang, W., Li, G., 2020. A novel bi-objective
model of cold chain logistics considering location-routing decision and environmental ef-
fects. Plos one, 15(4): e0230867.
8. Chen, J., Liao, W., Yu, C., 2021. Route optimization for cold chain logistics of front ware-
houses based on traffic congestion and carbon emission. Computers & Industrial Engineer-
ing, 161: 107663.
9. Chen, W., Zhang, D., Van Woensel, T., Xu, G., Guo, J., 2023. Green vehicle routing using
mixed fleets for cold chain distribution. Expert Systems with Applications, 233: 120979.
10. Zhang, G., Dai, L., Yin, X., Leng, L., Chen, H., 2023. Optimization of multipath cold-chain
logistics network. Soft Computing, 27(23): 18041-18059.
11. Yang, F., Tao, F., 2023. A Bi-Objective Optimization VRP Model for Cold Chain Logistics:
Enhancing Cost Efficiency and Customer Satisfaction. IEEE Access, 11: 127043-127056.
12. Deng, H., Wang, M., Hu, Y., Ouyang, J., Li, B., 2021. An Improved Distribution Cost Model
Considering Various Temperatures and Random Demands: A Case Study of Harbin Cold-
Chain Logistics. IEEE Access, 9: 105521-105531.

A Memetic Algorithm for Vehicle Routing Problem with Fresh Food 623
13. Hsu, C. I., Hung, S. F., Li, H. C., 2007. Vehicle routing problem with time-windows for
perishable food delivery. Journal of food engineering, 80(2): 465-475.
14. Prins, C., 2004. A simple and effective evolutionary algorithm for the vehicle routing prob-
lem. Computers & operations research, 31(12): 1985-2002.
Open Access This chapter is licensed under the terms of the Creative Commons Attribution-
NonCommercial 4.0 International License (http://creativecommons.org/licenses/by-nc/4.0/),
which permits any noncommercial use, sharing, adaptation, distribution and reproduction in any
medium or format, as long as you give appropriate credit to the original author(s) and the
source, provide a link to the Creative Commons license and indicate if changes were made.
The images or other third party material in this chapter are included in the chapter's
Creative Commons license, unless indicated otherwise in a credit line to the material. If material
is not included in the chapter's Creative Commons license and your intended use is not
permitted by statutory regulation or exceeds the permitted use, you will need to obtain
permission directly from the copyright holder.