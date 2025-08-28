Transportation Research Part B 149 \(2021\) 322–346 

Contents lists available at ScienceDirect 

Transportation Research Part B 

journal homepage: www.elsevier.com/locate/trb 

Competitive and cooperative behaviour analysis of connected 

and autonomous vehicles across unsignalised intersections: A 

game-theoretic approach 

Hua Wang a ,  Qiang Meng a , ∗,  Shukai Chen a ,  Xiaoning Zhang b 

a *Department* *of* *Civil* *& * *Environmental* *Engineering, * *National* *University* *of* *Singapore, * *117576* *Singapore* b *School* *of* *Economics* *and* *Management, * *Tongji* *University, * *Shanghai* *20* *0* *092, * *China* a r t i c l e 

i n f o 

a b s t r a c t 

*Article* *history:* 

We in this paper investigate navigation strategies of two cross-moving connected and au- 

Received 25 July 2020 

tonomous vehicles \(CAVs\) at an unsignalised intersection. As highly intelligent and au- 

Revised 10 March 2021 

tomated entities, CAVs could make decisions independently or behave in a cooperative 

Accepted 6 May 2021 

manner. A Nash game with discrete decision strategy is formulated to characterize the 

non-cooperative behaviour and a cooperative game is formulated to model the coopera- 

*Keywords:* 

tive control mechanism. Results show that \(i\) pure-strategy Nash equilibria \(NEs\) for the 

Connected and autonomous vehicles 

non-cooperative game always exist and NEs hold if and only if at least one CAV takes its 

Nash game 

dominant strategy; \(ii\) more than two pure-strategy NE solutions may exist, but at most 

Cooperative behaviour 

two different payoffs could arrive for each player at pure-strategy NEs; \(iii\) the optimal 

Unsignalised intersection 

solution to the cooperative game must be in the NE solution set. These interesting find- 

Branch & bound algorithm 

ings provide useful managerial insights to CAV operators and transport authorities, and 

also enable us to tailor a branch & bound \(B&B\) algorithm to efficiently solve the models. We also extend the proposed methodology to the n-player case \( *n* ≥ 3 \) and give some more generalized insights. Numerical experiments are demonstrated in the end to test the 

computational accuracy and efficiency of the B&B method and show that our models and 

algorithm can be readily incorporated into future real-time CAV decision system to help 

navigate through unsignalised intersections. 

© 2021 Elsevier Ltd. All rights reserved. 

**1. ** **Introduction** 

The concept of connected and autonomous vehicles \(CAVs\) has triggered revolutionary development in automotive industry and transportation field in recent decade. Technology innovations, including vehicle-to-vehicle \(V2V\) communication, vehicle-to-infrastructure \(V2I\) communication and vehicle automation system, continue to propagate a prosperous future for CAVs. Governments, automotive manufacturers, technology companies and research institutes have all invested heavily in the area. As of 2016, seven US states and Washington, DC have passed legislation aimed at regulating CAVs and one state has issued an executive order. China also aims to race ahead of everyone and has ambitious plans for CAVs. According to Ministry of Industry and Information Technology \(MIIT\) of the Chinese government, new cars fitted with driver assistance 

∗ Corresponding author. 

*E-mail* *addresses:* hwang191901@gmail.com \(H. Wang\),  ceemq@nus.edu.sg \(Q. Meng\),  shukai.chen@u.nus.edu \(S. Chen\),  cexzhang@tongji.edu.cn \(X. 

Zhang\). 

https://doi.org/10.1016/j.trb.2021.05.007 

0191-2615/© 2021 Elsevier Ltd. All rights reserved. 

*H. * *Wang, * *Q. * *Meng, * *S. * *Chen* *et* *al. * 

*Transportation* *Research* *Part* *B* *149* *\(2021\)* *322–346* 

\(DA\) and partially automated \(PA\) are to account for 50 percent of sales by 2020; fully autonomous vehicles are expected to feature in 10 percent of sales by 2030. Among the tech giants worldwide, Google and Baidu are two frontiers in CAV 

market. Google started working on its self-driving-car project back in 2009 and has accumulated three million miles in road tests since then. Baidu, a relative newcomer, has released Apollo 1.0 in July 2017, and started testing Apollo-running cars on public roads in late 2017. In academic field, researchers and technicians around the world exhibit magnificent enthusiasm in extending existing theories for the application of CAVs. An explosive number of CAV related studies published in top transportation journals, such as intelligent Transportation System, Transportation Research Part B and Part C, are good indications and signals of such effort. 

There is no doubt that automation will dramatically influence the automotive industry and traffic management. Therefore, it is imperative to put forward innovative ideas to utilize advanced CAVs technologies to improve our transport systems from various aspects and at different scales. If full automation is to come true, travel behaviour and traffic management would be changed completely. Automation and artificial intelligence will lead to signal-free management. This could substantially improve the efficiency of road infrastructure, and at the same time, facilitate greater safety by reducing randomness and human error. 

However, the current fundamental theories are not well established. In one aspect, CAV is a relatively new topic and academic research on this area has just started. Current theories for CAVs are mostly based on long-existing theoretical frameworks, by assuming multiple-time travel capacity for CAV lanes compared to normal lanes. This simplified approach may work on macro level, but it neglects the travel behaviour of CAVs on micro level, as they can be treated as intelligent individuals in the network. At the micro level, there are a few studies on CAV movement strategy at signalized intersections in the existing literature. However, the exploration of CAV navigation strategy at unsignalized intersections has not received sufficient attention. In another aspect, the real traffic environment is far more complex than imagined. Travel decisions are influenced by weather, mixed traffic flow, intersections and etc. Besides academic research effort, in the industry, Google and Baidu mainly use machine learning technique to study travel strategies. The main limitation of this approach is that training samples can hardly cover all scenarios, and accident may occur if the scene is new to the autonomous driving system. 

Given the limitations in current research, this paper aims to focus on the micro level of the problem, and to study the travel strategy of CAVs at an unsignalised intersection. Game theory is applied here, and this OR approach has better applicability compared to machine learning. More specifically, it models the behaviours of two CAVs at an unsignalised intersection under two scenarios: first, two CAVs drive individually to compete for limited road resources; second, two CAVs react based on cooperative strategies. We also extend the game-theoretical analysis to a n-player case where *n* ≥ 3 . 

This work addresses the following issues: how to describe travel behaviours under competing and cooperative scenarios respectively? Is there a system equilibrium under competing driving behaviour? If so, is the equilibrium unique and how to derive travel strategies under such equilibrium? How different are the system efficiencies comparing competing and cooperative scenarios? 

The contributions of this work are threefold. First, it enriches the existing theoretical basis by offering a completely new perspective on micro level. Second, the theoretical analysis of the non-cooperative game sheds some insightful lights on understanding the relationship between the two different CAV operational mechanisms. The theoretical results can help to design tailored solution algorithm to efficiently find out the optimal navigation strategies for both CAV navigation scenarios. 

Third, the results of this work can be directly incorporated into autonomous driving systems as it provides an optimal solution in above situations. It would help to accelerate the realization of CAV technology. In this paper, we firstly formulate a Nash game to model competitive travel strategies between two CAVs at an unsignalised intersection. The competition can be interpreted as a Chicken game. The results show that pure-strategy Nash equilibria \(NEs\) for the noncooperative game always exist and the NEs hold if and only if at least one CAV takes its dominant strategy. Moreover, it is proved that there may exist multiple pure-strategy NE solutions, but at most two different payoffs could arrive for each player at pure-strategy NEs. We also explore the cooperative control mechanism for two CAVs to pass an unsignalised intersection and reveal that the optimal solution to the cooperative game must be in the NE solution set. In addition, we extend to analyze the generalized case with more CAVs \( *n* ≥ 3 \) and tentatively discuss the rolling-horizon approach to incorporate dynamic traffics \(multi-player case with continuously arriving vehicles\). These interesting findings offer CAV operators and transport authorities useful managerial insights and also help to tailor a branch & bound \(B&B\) algorithm to solve the game models. 

**2. ** **Literature** **review** 

Earlier experiments on automating driving can be traced back to 1920s, and some promising trials took place in the 1950s \( Kröger, 2016 \).  In the 1980s, the first truly autonomous prototype cars appeared. They were outcomes of Navlab and ALV projects led by Carnegie Mellon University in 1984 and Eureka Prometheus Project collaborated by Mercedes-Benz and Bundeswehr University Munich in 1987 \( Navlab: The Carnegie Mellon University Navigation Laboratory, 2014 \).  Research on transportation planning with automated guided vehicles quickly kept up with the advancement. Three of the pioneer works were from the operational research perspective \( Krishnamurthy et al., 1993; Thonemann and Brandeau, 1996 \).  The setup of these papers were dispatching and routing on a facility floor with automated guided vehicles.  Krishnamurthy et al. \(1993\) focused on minimising makespan and avoiding conflict while routing.  Thonemann and Brandeau \(1996\) designed a single-vehicle automated guided vehicle system with multiple load capacity operating under a simple “go-when-filled” dispatching rule. 

323 

*H. * *Wang, * *Q. * *Meng, * *S. * *Chen* *et* *al. * 

*Transportation* *Research* *Part* *B* *149* *\(2021\)* *322–346* 

In the past decade, due to various advancement in technology, CAVs have captured attention again. Various works differ from one another in terms of focus, method, scale, and etc., but we broadly categorise them into two groups: planning-level problems and operational-level problems. One kind of planning-level problems falls into the area of network design \(e.g., 

Ghiasi et al., 2017; Chen et al., 2017; Olia et al., 2017 \).For instance,  Ghiasi et al. \(2017\) used Markov chain to quantify mixed traffic capacity and determine optimal number of dedicated CAV lanes on a highway segment.  Chen et al. \(2017\) proposed a framework for designing AV zones in a general transportation network. The operational-level problems can concern the 

whole network and/or individual vehicles \(e.g., Du et al., 2014; Zhou et al., 2017; Ma et al., 2017; Wang et al., 2014a; Wang 

et al., 2014b; Luo et al., 2016; Chen et al., 2021 \). For example, Luo et al. \(2016\) provided a design of dynamic automated 

lane change manoeuvre based on V2V communications that enables potential collision avoidance during the lane change process. Interested readers can refer to the three editorial notes of special issues,  Yang et al. \(2017\) , Xie et al. \(2017\) ,  and 

Qu et al. \(2017\) ,  for updating on the recent theoretical ideas. 

We would like to pay more attention to existing studies that investigated travel strategy of CAVs at intersections. One straightforward strategy is to use the traffic information collected from CAVs for traffic signal optimization. Compared to loop detectors, V2I technologies can provide more accurate and reliable data input \(real-time vehicle arrival and queue length\) for intersection controller \( He et al., 2012 \). Li and Zhou \(2017\) proposed a novel intersection control idea that CAVs sent real-time green-time passing requests, and the controller adaptively assigned green time to serve CAVs based on a machine-scheduling-based model. To exploit advantages of automated driving, some studies integrated trajectory planning 

with signal timing so as to reduce vehicular delays and the number of stops \(e.g., Li et al., 2014; Yu et al., 2018; Rey and 

Levin, 2019; Chen et al., 2020 \). For example, Li et al. \(2014\) developed a traffic signal control algorithm that allowed for 

CAV paths and signal control to be jointly optimized at intersections with two single-lane through entries. Under the traffic environment with mixed CAVs and human-driven vehicles \(HDVs\),  Rey and Levin \(2019\) proposed a restricted signal phase for CAVs for the intersection with dedicated CAV lanes. However, it should be noted that traditional traffic signal timings typically require the minimum green time, which might cause efficiency loss for CAVs \( Guler et al., 2014 \).  To solve this issue, a signal-free control system could be implemented for CAV traffic management at intersections. 

Under a fully automation environment, CAVs could communicate with the signal-free controller and obtain the reserved time slots for passing the intersection. Recently, this reservation-based traffic signal control concept has attracted increasing attention in the literature. An easy-to-implement reservation-based control is the first-come-first-served \(FCFS\) strategy 

\( Dresner and Stone, 2004; Yu et al., 2019 \).  However, such control strategy often work inefficiently in case of heavy traffic demand. As reported by Levin et al. \(2016a\) ,  the FCFS reservation strategy would increase delay if local-road vehicles are prioritized over arterial-road vehicles.  Levin et al. \(2016b\) developed an integer program model to improve the performance of reservation-based control. In addition, a few researchers made extensions to incorporate platooning idea into the reservation-based control.  Amirgholy et al. \(2020\) proposed a cooperative control strategy for a road network with unsignalized intersections where CAV platoons were designed. In their model, it was assumed that CAVs had to stop and wait for the next suitable platooning headway when coordination failures occur. The main difference of our study is that we consider micro-level factors for cooperative control such as vehicle speed and time-to-collision constraint to ensure feasible navigation strategy; whereas Amirgholy et al. \(2020\) focused on deriving the platoon-based intersection capacity taking into account the probability of coordination failure. For network-wide CAV intersection control,  Zhu and Ukkusuri \(2015\) built a novel linear programming model by taking into acount CAV traffic dynamics. However, the above studies have not considered CAVs’ trajectories while approaching intersections where vehicular queues perhaps happen. Therefore, it is worthwhile to make vehicle speed regulation so that vehicles could pass the intersection efficiently and safely. 

Another category of the studies related to our work is the integrated optimization of the signal-free intersection control and vehicle trajectories.  Lee and Park \(2012\) proposed a nonlinear programming model for the cooperative trajectory planning problem with an objective to minimize overlapped vehicle trajectories subject to vehicle kinematic constraints. But the nonlinear kinematic constraints would lead to high intractability.  Yang et al. \(2016b\) proposed a cooperative driving model for unsignalized intersections based on reduplicate dynamic game where weighted-sum objective function was considered to deal with safety, rapidity and comfort indicators. For the mixed CAV-HDV traffic scenario,  Yang et al. \(2016a\) extended to consider CAV trajectory design and switching strategy for different levels of technologies.  Levin and Rey \(2017\) put forward an autonomous intersection manager \(AIM\) protocol where a mixed integer linear program was developed to optimally design the intersection trajectory.  Wu et al. \(2019\) modelled the sequential vehicular movements at unsignalized as multi-agent Markov decision process with discrete speed decisions, and used a decentralzied learning approach to solve the model. 

It is noted that most previous studies have not taken into account switching frequency of vehicle speed in trajectory design, except Yang et al. \(2016a\) .  As demonstrated in our study, the consideration of changing frequency of vehicle acceleration states will not only guarantee driving comfortability, but also help substantially reduce computational burden. 

Based on the literature review, most of previous studies committed from the perspective of cooperative/coordinative controls. In actual, as automation and intelligence further advance, every CAV could evolve into an independent and selfish decision engine that may not follow cooperative rules from a central controller. Cooperative control mechanism might not be favorable for all participants in CAV fleets as some CAVs need to wait longer if following the schedule from a unified central controller. In this sense, passengers would be reluctant to accept the coordination but would prefer a competing mode. Motivated by this, we investigate the competing travel strategy of CAVs at an unsignalised intersection using game theory. Also, an in-depth comparison between competitive and cooperative control mechanisms is made to showcase their relative efficiency. On the other hand, most previous studies attempted to plan CAV trajectories by constructing nonlinear 324 





*H. * *Wang, * *Q. * *Meng, * *S. * *Chen* *et* *al. * 

*Transportation* *Research* *Part* *B* *149* *\(2021\)* *322–346* 

**Fig. ** **1. ** An illustrative example for two cross-moving CAVs at an unsignalised intersection. 

kinematic equations when approaching intersections, which would lead to high computational intractability. In our study, the vehicle trajectories are approximately constructed through discrete speed actions. By this way, the optimal control decisions could be very efficiently obtained through a branch-and-bound solution algorithm by considering the constraints of speed changing frequency. The well computational performance of the developed algorithm makes it possible to implement autonomous intersection management in the near future. 

With all the explanations above, we shall devote Section 3 to describing the problem. In the succeeding Section 4 ,  we formulate two game models to characterize competitive and cooperative behaviours respectively and explore their mathematical properties. We then pass on to Section 5 to develop the solution algorithm for the models. Numerical studies are presented in Section 6 .  In Section 7 ,  we provide a brief recapitulation of the paper and offer some concluding remarks. 

**3. ** **Problem** **description** 

In this paper, we focus on investigating vehicles’ intelligent control strategies under the case that two CAVs move towards an unsignalised intersection from different directions. It is assumed that a perfect wireless communication among CAVs is provided, and there are no packet loss and communication delay for a long-distance real-time communication between any two approaching CAVs. As shown in Fig. 1 ,  Vehicle A \(orange car\) moves in the vertical direction and Vehicle B \(blue car\) runs along the orthogonal lane from right to left. There exists a conflict point/zone \(red dot in the figure\) for CAV 

movements and accidents may occur if no traffic control strategies/rules are provided. 

As shown in Fig. 1 ,  two CAVs enter into the intersection range at time *t* = 0 when they can detect and “talk” with each other and share instantaneous driving information with the help of an V2V communication support platform. We assume that the control system equipped on each CAV can assess current vehicle state and collect surrounding traffic information \(e.g., position and velocity of the neighboring CAV\). Based on these information, each CAV’s control system will evaluate its driving safety and then decide the operational actions for successive time intervals by taking into account another CAV’s feedback/reaction. At a decision epoch, each CAV is able to change its velocity by accelerating, decelerating or maintaining the current state with no action. Under a prerequisite of safe driving, each CAV then makes an attempt to traverse the intersection as soon as possible and also to ensure a certain level of comfortability for passengers. 

In presence of V2V communication, two CAVs could behave in different attitudes so that different control strategies can be practiced. On one hand, they can make respective driving actions independently which leads to a competitive game. 

On the other hand, two CAVs may act in cooperative manner to make a coordinative driving scheme which generates a cooperative game. Our work aims to develop game-theoretical models to characterize such competitive and cooperative behaviours of two CAVs at an unsignalized intersection, and to reveal some managerial insights. 

**4. ** **V2V** **Control** **strategies:** **Competitive** **and** **cooperative** **mechanisms** In this section, we first formulate the problem using mathematical representations. The terms “vehicle”, “CAV” and 

“player” are used interchangeably throughout this study, unless stated otherwise. Two CAVs, Vehicles A and B, are viewed 325 

*H. * *Wang, * *Q. * *Meng, * *S. * *Chen* *et* *al. * 

*Transportation* *Research* *Part* *B* *149* *\(2021\)* *322–346* 

as two players. Consider a time horizon that is sufficiently long for two CAVs to pass the intersection. Let us partition the time horizon into a set of equal time intervals 0 *, * 1 *, * *. * *. * *. * *, * *K * and define the set of decision epochs \(i.e., sequences of times at which each CAV is required to make a decision\) as *K* := \{ 0 *, * 1 *, * *. * *. * *. * *, * *k, * *. * *. * *. * *, * *K* − 1 \} . Let *t* denote the time interval between two consecutive decision epochs *k* and *k* \+ 1 . 

At every decision epoch *k, * *k* ∈ *K*, each player selects his driving scheme by considering the rival’s reaction. Specifically, the CAV could take one of the following actions — acceleration, no action and deceleration at the beginning of each decision epoch. The set of the three actions can be defined as *A* := \{−1 *, * 0 *, * 1 \} . We here consider the three distinct actions only for simplicity, as multiple acceleration/deceleration levels could be reflected as long as the time interval is shortened. For example, when the time interval is changed from 1s to 0.5s, the number of acceleration/deceleration levels increases from 3 to 5, i.e., \{−2 *v* *, * − *v* *, * 0 *, * *v* *, * 2 *v* \} , where *v* is the unit velocity increment for each acceleration/deceleration action. The following assumptions are made to facilitate the model formulation: 

Assumption 1 It is assumed that the deceleration and/or acceleration actions could be fulfilled instantaneously. 

Assumption 2 When two CAVs detect each other, their distances to the conflict point are greater than a minimal safe clear-ance, i.e. the distances are sufficiently large that at least one vehicle could respond to avoid collision. 

We here explain a bit for the discrete acceleration decisions. Theoretically, it is ideal to model a continuous acceleration decision process, especially when we need to characterize the real-time trajectories \( Wang et al., 2015 \).  However, such treatment would give rise to a solution space with infinite feasible solutions, which makes the problem computationally intractable and hard to explore its mathematical properties, such as the existence and uniqueness of Nash equilibrium. Different from the lane-charging problem that wants to know a detailed polynomial trajectory curve \( Yang et al., 2018 \),  our problem address a straightforward moving case. In reality, there are limited acceleration actions when passing the intersection due to strict lane division in turning direction. Moreover, a continuous acceleration process can be well approximated by the discrete form if the number of time intervals is properly set. 

Let *v* *i,k* −1 denote the velocity of Player *i* at time *k* before taking action. Once an action is made, the velocity during time interval \[ *k, * *k* \+ 1 *\)* will be updated as 

*v* *i,k* = *v* *i,k* −1 \+ *v* *x* *i,k* *, * *k* ∈ *K, * *i* ∈ \{ *A, * *B* \} *,* where *x* *i,k* are the decision variables for Player *i* \(a decision made at decision epoch *k* means a vehicle control operation, either acceleration *v* , deceleration − *v* or keeping unchanged in terms of driving status\) and *x* *i,k* ∈ *A* ; *v* *i, * −1 is Player *i* ’s initial velocity when perceiving the other one at the beginning *k* = 0 ; and *v* is the unit velocity increment for each acceleration or deceleration action. 

Then the travel distance for Player *i* can be calculated by the below recurring function, *s* *i* *\(t\)* = ˇ *s* *i,k* \+ *v* *i,k* *\(t* − *k* *t* *\)* *, * if *t* ∈ \[ *k* *t* *, * *\(k* \+ 1 *\)* *t* *\)* *, * *k* ∈ *K*\\\{ *K* − 1 \} *,* \(1\) 

where the travel distance accumulated from the beginning time 0 up to time *k* *t* , ˇ *s* *i,k* , can be given by 

= *k* 

ˇ *s* *i,k* = 

*v* 

=

*i, * *t* *, * *k* ∈ *K*\\\{ *K* − 1 \} *, * 

0 

and ˇ *s* *i, * 0 = 0 . Note that the travel distance function \(1\) is a piece-wise function in time *t*. 

We can then determine the travel time with respect to travel distance, which is an inverse function of \(1\) : 

*L* 

*t*

*i* − ˇ

*s* 



*i,k* 

*i* = 

\+ *k* 

*v*

*t* *, * if *L* *i* ∈ \[ ˇ

*s* 



*i,k* *, * ˇ

*s* *i,k* \+1 *\)* *, * 

\(2\) 

*i,k* \+ *v* 

where *L* *i* , *i* ∈ \{ *A, * *B* \} is the distance to the potential conflict point when players appear in the intersection, and *v* is a very small positive constant that ensures the function to be well-defined 1 .  

We thus far have formulated the payoff function \(travel time\) for each player. 

1 Here, we want to highlight that Assumption 1 can be relaxed to a more practical scenario with constant acceleration. Under this case, the velocity for Player *i* will be updated by 

*v* *i\(t\)* = *v* *i,k* \+ *\(t* − *k* *t\)* *v* *x* *i,k* *, * *t* ∈ \[ *k* *t, * *\(k* \+ 1 *\)* *t\)* *, * *k* ∈ *K*\\\{ *K*\} *, * *i* ∈ \{ *A, * *B* \} *,* where *v* *i, * 0 = *v* *i, * −1 .Then, the travel distance function given by Eq. \(1\) could be adapted to 1 

*s* *i\(t\)* = ˇ *s* *i,k* \+ *v* *i,k* *\(t* − *k* *t\)* \+ *x* 2 *i,k* *v* *\(t* − *k* *t\)* 2 *, * *t* ∈ \[ *k* *t, * *\(k* \+ 1 *\)* *t\)* *, * *k* ∈ *K*\\\{ *K*\} *,* where ˇ *s* *i,k* = ˇ *s* *i,k* −1 \+ *v* *i,k* −1 *t*\+ 1 

2 *x* 

*i,k* 

−1 

2 

*t* *, * *k* ∈ *K*\\\{ 

*K*\} and ˇ *s* *i, * 0 = 0 Therefore, the travel time could be further determined by 

⎧ 

⎨ *L* *i*−ˇ *s* *i,k* 

*v* 

*i,k* 

\+ *v* \+ *k* *t, * if *L* *i*∈ \[ ˇ *s* *i,k* *, * ˇ *s* *i,k* \+1 *\)* and *x* *i,k* = 0 *,* *t* 



*i* = ⎩ *k* *tx* *i,k* *v* − *v* *i,k* \+ *v* 2 *i,k* \+2 *x* *i,k* *v* *\(L* *i*−ˇ *s* *i,k* *\)* *x* 

*i,k* 

*v* 

*, * if *L* *i*∈ \[ ˇ *s* *i,k* *, * ˇ *s* *i,k* \+1 *\)* and *x* *i,k* = 0 *. * 

326 

*H. * *Wang, * *Q. * *Meng, * *S. * *Chen* *et* *al. * 

*Transportation* *Research* *Part* *B* *149* *\(2021\)* *322–346* 

*4.1. * *The* *game* *model* *for* *competitive* *control* *mechanism* In this section, we investigate the case when two CAVs determine their driving strategies independently. In this case, each of them chooses its operations in all decision epochs by considering the decision information shared by the other one. 

V2V communication enables both players to perfectly perceive rival’s decisions when optimizing respective policies. Such simultaneously decision optimization of two CAVs leads to a competition, which can be characterized as a Nash game. 





Let X *i* := *x* *i,k* *, * *x* *i,k* ∈ *A* *, * *k* ∈ *K* be the vector of multi-period decisions over the entire time horizon for Player *i, * *i* ∈ \{ A, B \} . 

Each player aims to safely and comfortably pass the intersection as soon as possible. Therefore, the payoff for Player *i* is to minimize his time to pass the intersection \(the time from detecting the rival to passing the potential conflict point\) given the rival’s driving strategy. The noncooperative behaviours of the two players can be characterized as the following Nash game: 

\(COMP Model\) 

min *t* *i* *\(* X *i* *, * X *i* − *\)* 

\(3\) 

X *i*

s.t. 

| *t* *i* − *t* *i* −| ≥ *t* avoid *, * ∀ *i* ∈ \{ *A, * *B* \} *, * *i* − ∈ \{ *A, * *B* \}\\\{ *i* \} *,* \(4\) 

*δi,k* ≤ *N* accel 

max *, * 

\(5\) 

*k* ∈ *K*\\\{ *K*−1 \} 

0 ≤ *v* *i,k* ≤ *v* max *, * ∀ *i* ∈ \{ *A, * *B* \} *, * *k* ∈ *K,* \(6\) 

where *t* avoid is the minimal collision avoidance time \( *t* avoid *> * 0 \); *N* accel max is the maximal number of times allowed to change 

driving states; and *v* max is the maximal permitted speed under traffic management policy. It is believed that frequently switching driving states between acceleration and deceleration would make passengers uncomfortable and greatly reduce their satisfaction. The value of *N* accel 

max can be estimated based on the empirical human driving data. Of course, our model 

can be lifted to a generalized case that drops this constraint and the proposed algorithm in Section 5 is still applicable \(see more details in Section 6.2.2 \).  The driving-state switching indicator *δi,k* for Player *i* is defined as *δ*

1 *, * if *x* *i,k* \+1 = *x* *i,k* 

*i,k* = 

*, * ∀ *k* ∈ *K*\\\{ *K* − 1 \} *. * 

0 *, * otherwise 

Constraint \(4\) ensures two CAVs can safely pass the intersection. Constraint \(5\) requires that the switching frequency of driving state is under control to guarantee high driving comfortability. Constraints \(6\) imply that velocities over the entire time horizon are nonnegative and do not exceed an maximal speed. 

To facilitate our presentation, let us define the feasible solution space for Player *i* as *i* | X := \{ *\(* 4 *\)* *, * *\(* 5 *\)* and *\(* 6 *\)* with given X 

*i* 

−

*i* − \} 

*, * 

and define its relaxed form as 

˜ 

*i* := \{ *\(* 5 *\)* and *\(* 6 *\)* \} *. * 

Clearly, each Player *i* has finite discrete strategies defined in ˜ 

*i* and the above Nash game is a game with pure and dis- 





crete strategies. W.l.o.g, let us specify the relaxed strategy space for Player *i* as ˜ 

*i* := X *κ*

. Then, we can 

*i* *, * *κ *= 1 *, * 2 *, * · · · *, * | ˜ 

*i* | 

easily calculate the travel time *t* *i* *\(* X *κi* *\)* . Recall that both players restrain each other’s actions only via the collision avoidance constraint \(4\) .  We here set the payoff as infinite if the collision avoidance constraint \(4\) is violated. Therefore, the payoff for Player *i* under a strategy combination *\(* X *κi* *, * X 

*i* − *\)* can be re-determined by 

*t* *i* *\(* X *κ*

*\)* | ≥ *t* 

*P*

avoid *, * 



*i* *\)* *, * 

if | *t* *i* *\(* X *κi* *\)* − *t* *i* − *\(* X 

*i* −

*i* *\(* X *κ*

*i* *, * X 

*i* − *\)* = \+ ∞ *, * 

otherwise *. * 

Then, the strategic Nash game exhibits two particular properties: 

Property 1 If *P* *i* *\(* X *κi* *, * X 

*i* − *\)* = \+ ∞ , then *P* *i* − *\(* X *κ*

*i* *, * X 

*i* − *\)* = \+ ∞ ; and vice verse. 

Property 2 Suppose Player *i* takes strategy X *κi* . For all feasible strategy combinations \(namely rival’s strategy falls into *i* −| X *i* \), we have *P* *i* *\(* X *κi* *, * X *i* − *\)* = *P* *i* *\(* X *κi* *, * X 

*i* − *\)* . 

The first property reflects the consequence of avoiding constraint \(4\) .  The latter one holds because the payoff function for Player *i* only depends on his own strategy if it is feasible. 

Since the COMP model forms a finite game, mixed-strategy equilibrium necessarily exists according to Nash’s Theorem 

\( Nash, 1951 \).  However, pure-strategy equilibrium may not exist. We next explore the existence of pure-strategy Nash equilibrium \(NE\) for the COMP model. 

**Proposition** **1. ** *Pure-strategy* *Nash* *equilibria* *\(NEs\)* *for* *the* *noncooperative* *game* *\(3\)*  *always* *exist. * 

327 

*H. * *Wang, * *Q. * *Meng, * *S. * *Chen* *et* *al. * 

*Transportation* *Research* *Part* *B* *149* *\(2021\)* *322–346* 

**Fig. ** **2. ** An example to illustrate the acyclicity for the discrete-strategy Nash game \(3\) . 

**Proof. ** The existence of pure-strategy NEs for the noncooperative game can be shown by proof of contradiction. According to Proposition 1 in Mallick \(2011\) ,  a pure-strategy NE always exists if and only if the minimal acyclicity condition is satisfied. 

Therefore, if there is no residual matrix \(a subset of the original strategic Nash game\) that contains cyclic best-response decision trees, NE must exist. 

Suppose that there exists a cyclic best-response decision tree in a residual matrix. W.l.o.g, let the sequence of recurring best responses in the cyclic decision tree be 

*\(* X

player 

player 

player 

player 

0 

−−−→ *\(* X

−−−→ *\(* X

*\) *−−−→ *\(* X

*\) *−−−→ *\(* X

*\)*

*i* *, * X 0 

*i* − *\)* 



*k* 

*i* *, * X 0 

*i* − *\)* 



*k* 

*i* *, * X *j* 



*k* 

*i* *, * X *j* 



*k* 

*i* *, * X *j* 

*i* 

*i* −

*i* −

*i* 

*i* −

*i* −

*i* −

player 

−−−→

player 

player 

· · · player 

−−−→ · · · player 

−−−→ *\(* X *k* 

*\) *−−−→ *\(* X

*\) *−−−→ *\(* X

*i* *, * X *j* 



0 

*i* *, * X *j* 



0 

*i* *, * X 0 

*i* − *\)* 

*i* 

*i* −

*i* −

*i* −

*i* 

*i* −

*i* −

Note that all strategy combinations that appear in the cyclic best-response tree are feasible. From the perspective of player *i* , it follows from **Property** **2** that 

*P* *i* *\(* X 0 

*\)*

*\)*

*\)*

*i* *, * X 0 

*i* − *\)* *> * *P* *i* *\(* X *k* 

*i* *, * X 0 

*i* − *\)* = *P* *i* *\(* X *k* 

*i* *, * X *j* *> * *P* 

= *P* 



*i* −

*i* *\(* X *k* 

*i* *, * X *j* 

*i* −

*i* *\(* X *k* 

*i* *, * X *j* 

*i* −

*> * · · · = *P* *i* *\(* X *k* 

*\)*

*\)*

*i* *, * X *j* *> * *P* 

= *P* 

*i* −

*i* *\(* X 0 

*i* *, * X *j* 

*i* −

*i* *\(* X 0 

*i* *, * X 0 

*i* − *\)* *. * 

\(7\) 

The contradiction of the above inequality implies that the hypothesis of the existence of cyclic best-response trees does not hold. Pure-strategy NEs thus exist. 

Actually,  Eq. \(7\) reveals a direction-preserving property of the response function for the Nash game \(3\) .  Interested readers could also apply the discrete fixed point theorem \(e.g., Theorem 2 in Iimura et al. \(2005\) \) to prove Proposition 1 .  

The example shown in Fig. 2 gives a more intuitive interpretation for the above proof. It follows from Eq. \(7\) that *P* *i* *\(* X 0 

*i* *, * X 0 

*i* − *\)* *> * *P* *i* *\(* X 1 

*i* *, * X 0 

*i* − *\)* = *P* *i* *\(* X 1 

*i* *, * X 1 

*i* − *\)* *> * *P* *i* *\(* X 2 

*i* *, * X 1 

*i* − *\)* = *P* *i* *\(* X 2 

*i* *, * X 2 

*i* − *\)* *> * *P* *i* *\(* X 0 

*i* *, * X 2 

*i* − *\)* = *P* *i* *\(* X 0 

*i* *, * X 0 

*i* − *\)* *. * 

The following proposition tells us a simple method to construct NEs. 

**Proposition** **2. ** *If* *feasible* *solutions* *satisfy* *the* *following* *conditions:* 

*“Player* *i* *always* *takes* *acceleration* *actions* *unless* *reaching* *speed* *limit* *or* *passing* *the* *conflict* *point; * *another* *Player* *i* − *minimizes* *his* *travel* *time* *subject* *to* *the* *rival’s* *decision”,* *then* *they* *are* *pure-strategy* *NE* *solutions. * 

**Proof. ** A constructive proof is applied here. Player *i* takes a set of acceleration actions that satisfy the condition asserted in 

Proposition 2 and thus his strategy can be written as 

˜ 

X *i* := \{ *x* *i,k* = 1 *, * if *v* *i,k* −1 \+ *v* *x* *i,k* ≤ *v* max *, * and *x* *i,k* = 0 *, * otherwise \} *. * 

The above solution offers a dominant strategy for Player *i* such that he can pass the intersection as soon as possible. The shared constraint \(4\) requires both players giving their highest priorities to collision avoidance. Therefore, the rival needs to minimize his travel time subject to Player *i* ’s strategy. Then, the optimal strategy for Player *i* − can be given by 

˜ 

X *i* − = arg min *t* *i* − *\(* X *i* − *\)* 

X *i*− ∈ *i* − | ˜ 

X *i* 

Under Assumption 2, the feasible solution set *i* − | ˜ 

X is nonempty so that Player *i* − has optimal solution\(s\). NE arrives if and 

*i* 

only if the following conditions are satisfied: 

*t* *i* *\(***x** ∗

and

*i* *, * **x** ∗ *i* − *\)* ≤ *t* *i* *\(***x** *i* *, * **x** ∗ *i* − *\)* *, * ∀ **x** *i* ∈ *i* | **x** *t* 

*i* 

−

*i* − *\(***x** ∗ *i* *, * **x** ∗ *i* − *\)* ≤ *t* *i* − *\(***x** ∗ *i* *, * **x** *i* − *\)* *, * ∀ **x** *i* − ∈ *i* − | **x** *i. * 

It is not difficult to verify that NEs can be ensured when combination strategies *\(* ˜ 

X *i* *, * ˜ 

X *i* − *\)* are taken, i.e. no player can be 

better off by unilaterally changing his strategy. 

328 

*H. * *Wang, * *Q. * *Meng, * *S. * *Chen* *et* *al. * 

*Transportation* *Research* *Part* *B* *149* *\(2021\)* *322–346* 

Based on Proposition 2 ,  it is obvious that two possible cases exist for the NEs. 

CASE 1 Both CAVs can move in a continuously accelerating state until reaching speed limit and they pass the intersection without any collision risk. Under this case, both players make independent decisions and are better off in minimizing respective travel time. 

CASE 1 One CAV moves in the ideal state with its dominate strategy and the other one is not able to take its dominant strategy. Then the competition formulated by the COMP model could be interpreted as a Chicken Game \(also known as the Hawk-dove Game or Snowdrift Game\). The principle of the formulated noncooperative game \(3\) is further stated as i\) both players benefit if one player yields to ensure collision avoidance and the other player’s optimal choice; and ii\) if his opponent yields, the player should not. That means the player yields if and only if his opponent fails to yield.  Proposition 2 addresses the case that NEs are arrived if one player thoroughly compromises to adapt to his rival’s dominant strategy. 

**Remark** **1. ** Proposition 2 also tells us that the Nash game can be decentralized into the Stackelberg game where one player takes his dominant strategy and the other one optimizes his decisions as a follower. 

We thus far analyze the existence of NEs for the noncooperative game and propose a tangible method to construct the equilibrium solutions. One may wonder if there exists another NE solution that does not satisfy the condition given in 

Proposition 2 .  The following corollary provides a more in-depth understanding of the NE solution. 

**Corollary** **1. ** *There* *may* *exist* *multiple* *\(more* *than* *two\)* *pure-strategy* *NE* *solutions. * *But* *at* *most* *two* *different* *payoffs* *could* *arrive* *for* *each* *player* *at* *pure-strategy* *NEs. * 

**Proof. ** It is easy to understand the non-uniqueness of NE solutions since different solutions may have identical effect. Consider the following two solutions for Player *i* : 

X 1 

*i* = \{ 1 *, * −1 *, * −1 \} and X 2 

*i* = \{−1 *, * 1 *, * 1 \} *. * 

The vectors of the accumulative distances based on the two solutions are 

**š** 1 = \{ 0 *, * *\(v* *i, * −1 \+ *v* *\)* *t* *, * *\(* 2 *v* *i, * −1 \+ *v* *\)* *t* *, * 3 *v* *i, * −1 *t* \} *,* **š** 2 = \{ 0 *, * *\(v* *i, * −1 − *v* *\)* *t* *, * *\(* 2 *v* *i, * −1 − *v* *\)* *t* *, * 3 *v* *i, * −1 *t* \} *. * 

Clearly, when *L* *i* = 3 *v* *i, * −1 *t* , the above two solutions generate an equal travel time of 3 *t* . 

The second sentence of this corollary asserts that 

\(i\) All NE solutions generate an identical payoff for each player under **CASE** **1** . 

\(ii\) The NEs can be achieved if and only if one player yields under **CASE** **2** . 

It is not difficult to verify that **\(i\)** holds since both players take their dominant strategies. We now turn to prove **\(ii\)** by proof of contradiction. W.l.o.g, let *\(* ˆ 

X *i* *, * ˆ 

X *i* − *\)* be the NE solution that Player *i* − thoroughly compromises, and ˆ *P* *i* and ˆ *P* *i* −

be the corresponding payoffs for Player *i* and Player *i* − respectively. Similarly, let *\(* ˇX *i* *, * ˇX *i* − *\)* be the NE solution that Player *i* thoroughly compromises, and ˇ

*P* *i* and ˇ *P* *i* − be the corresponding payoffs for the two players. 

Suppose that there exists a NE that does not fall into the two cases. Let *\(* X 

*i* *, * X 

*i* − *\)* denote this NE solution, and *P* 

*i* and *P* 

*i* −

be the corresponding payoffs for the two players \( *P* *P* 

*P* 

*i* = ˆ 

*i* , *P* 

*i* = ˇ

*P* *i* ; *P* 

*i* − = ˆ *i* − , *P* 

*i* − = ˇ

*P* *i* −\). We further have 

*P* 

*P*

*i* *> * ˆ 

*i* and *P* 

*i* − *> * ˇ

*P* *i* − *. * 

If the above condition is not satisfied, *\(* X 

*i* *, * X 

*i* − *\)* will be not a NE solution since either the payoff of Player *i* could be better off by taking the strategy of ˆ 

X *i* or Player *i* − could further improve its payoff by switching to take the strategy of ˇX *i* −. 

Note that these three combination strategies are all feasible. It follows from the collision avoidance constraint \(4\) that 

| *P* *i* − *P* *i* −| ≥ *t* avoid *, * where *t* avoid *> * 0 *. * 

When *P* 

*i* *> * *P* 

*i* − , | *P* 

*i* − ˇ

*P* *i* −| ≥ *t* avoid holds and we can construct a new feasible combination strategy *\(* X *i* *, * ˇX *i* − *\)* . In this case, given Player *i* ’s strategy of X 

*i* , Player *i* − would turn to take the strategy of ˇ

X *i* − rather than X *i* −. This implies that the solution 

*\(* X *i* *, * X *i* − *\)* cannot ensure a NE. 

Otherwise, if *P* 

*P* 

*i* *< * *P* 

*i* − , we then have | *P* 

*i* − − ˆ *i* | ≥ *t* avoid . Another feasible combination strategy *\(* ˆ 

X *i* *, * X *i* − *\)* can be also con- 

structed. Now, given Player *i* −’s strategy of X 

*i* − , Player *i* would switch to take the strategy of ˆ 

X *i* rather than X *i* . This in turn 

indicates that NE does not hold for the solution *\(* X 

*i* *, * X 

*i* − *\)* . This completes the proof. 

Corollary 1 explicitly tells us that there are at most two pure-strategy Nash equilibria, though perhaps multiple solutions exist. If there is only one pure-strategy NE \(e.g., **CASE** **1** \), the game is predictable and implementable. When two or more Nash equilibria occur, it is almost impossible to anticipate the game results in reality. To deal with this dilemma, we devote to introducing a cooperative mechanism in the next section. 

329 

*H. * *Wang, * *Q. * *Meng, * *S. * *Chen* *et* *al. * 

*Transportation* *Research* *Part* *B* *149* *\(2021\)* *322–346* 

*4.2. * *The* *game* *model* *for* *cooperative* *control* *mechanism* In Section 4.1 ,  two CAVs behave as independently intelligent agents and their competitive behaviours are characterized. 

In practice, a central control system operated by transport sectors can also connect to the V2V communication platform. 

The system intends to manage the CAVs appearing at the intersection and guide them to follow predetermined driving strategies so as to improve travel efficiency of the transport system. When two CAVs detect each other, they could behave in a cooperative manner in passing the intersection. Their decision processes can be formulated as a cooperative game, which is given below: 

\(COOP Model\) 

min *t* *A* *\(* X *A* *\)* \+ *t* *B* *\(* X *B* *\)* \(8\) 

X *A* *, * X *B* 

s.t. *\(* 4 *\)* *, * *\(* 5 *\)* and *\(* 6 *\)* *. * 

Very interestingly, the above cooperative game has an appealing property, which leads to the following proposition. 

**Proposition** **3. ** *The* *optimal* *solution* *to* *the* *cooperative* *game* *must* *be* *in* *the* *NE* *solution* *set. * 

**Proof. ** We prove Proposition 3 by proof of contradiction. W.l.o.g, let us denote the two optimal payoffs for the cooperative game as *\(P* ∗ *A* *, * *P* ∗ *B* *\)* and, at NE, we have two payoffs of *\(P* ♦ *A* *, * *P* ♦ *B* *\)* \(if two NE solutions exist, then take the one with minimal sum of two payoffs\). Suppose there exists an optimal solution for the COOP model \(8\) which is not a NE solution. It then follows that 

*P* ∗ *A* \+ *P* ∗ *B* *< * *P* ♦

*A* \+ *P* ♦

*B* *. * 

Since both solutions are feasible, the above inequality holds if and only if one of the following conditions is satisfied, Condition 1: *P* ∗ *A* *< * *P* ♦ *A* and *P* ∗ *B* ≤ *P* ♦ *B* *,* \(9\) 

Condition 2: *P* ∗ *A* ≤ *P* ♦

*A* and *P* ∗

*B* *< * *P* ♦

*B* *. * 

According to Proposition 2 ,  the above Condition 1 in \(9\) holds if and only if *P* ∗ *B* = *P* ♦ *B* and Player B takes his dominant strategy. Under such case, there must be *P* ∗ *A* = *P* ♦ *A* according to the NE definition and system optimum defined in COOP 

model. This contradicts with Condition 1. A similar logic can be applied to Condition 2. 

**Remark** **2. ** More lessons can be learned from Proposition 3 .  First, it implies that the cooperative mechanism does not always outperform the competitive case. Mutually compromise strategies might lead to efficiency loss of the transport system. 

Second, the central control system could help/guide two CAVs to select one appealing NE strategy \(if two pure-strategy NEs exist\) via V2V communication without worsening the system efficiency. Last but not least,  Proposition 3 offers an idea to solve the COOP model by taking the best outcome of the COMP model in that the solution space of the former one is far large than the latter one. 

Next remark addresses the generality of the derived results. 

**Remark** **3. ** The above properties concluded in Propositions \( 1 –3 \) and Corollary 1 still hold when lifting Assumption 1 to a generalized situation of constant deceleration and/or acceleration actions \(i.e., the vehicle velocity changes at a constant acceleration/deceleration rate during a time interval when action is taken\). This is due to the fact that **Properties** **1** and **2** 

still hold under the case of constant deceleration and/or acceleration. 

*4.3. * *Extension* *to* *the* *n-player* *case* 

In the above sections, we have analyzed the non-cooperative and cooperative games between 2 players. With no doubt, it is more appealing and of great importance if we can extend our proposed models to address a generalized situation. We here present the extension of 3-player games and also shed light on characterizing a n-player case \( *n* *> * 3 \).  Fig. 3 describes the 3-player case. 

In the 3-player case, there not only exists a Nash game, for example, competition between Vehicles A and B, and competition between vehicles A and C, but also embeds a Stakelberg game between Vehicles B and C. The condition to avoid rear-end crashes between Vehicles B and C is given by 

*L* *C* − *s* *C* *\(k* *t* *\)* − *\(L* *B* − *s* *B* *\(k* *t* *\)\)* ≥ ˜ *t* avoid *\(v* *C,k* − *v* *B,k* *\)* *, * ∀ *k* ∈ *K,* \(10\) 

where ˜ *t* avoid is the minimal time to avoid rear-end crash. The above condition with sufficiently large number of time intervals is an approximation of the continuous form of *L* *C* − *s* *C* *\(t\)* − *\(L* *B* − *s* *B* *\(t\)\)* ≥ ˜ *t* avoid *\(v* *C* *\(t\)* − *v* *B* *\(t\)\)* . 

To facilitate our narrative, we hereafter omit the Constraint \(5\) and Constraints \(6\) .  We can write the 3-player Nash game as 

⎧ 





⎪ 

⎨ min X 

X 

s.t. | *t* 

*A* *t* 

*A* 

*A* | *\(* X 

*B* *, * X 

*C* *\)* 

*A* − *t* 

*B* | ≥ *t* avoid and | 

*t* *A* − *t* 

*C* | ≥ *t* avoid *, * 





⎪min X 

X *B* | X s.t. | *t* *B* − *t* 

\(11\) 



⎩

*B* *t* 

*B* 

*A* 

*A* | ≥ *t* avoid *, * 





min X 

X 

s.t. | *t* 

*C* *t* 

*C* 

*C* | *\(* X 

*A* *, * X 

*B* *\)* 

*C* − *t* 

*A* | ≥ *t* avoid and Constraint \(10\) *, * 

330 





*H. * *Wang, * *Q. * *Meng, * *S. * *Chen* *et* *al. * 

*Transportation* *Research* *Part* *B* *149* *\(2021\)* *322–346* 

**Fig. ** **3. ** The case of three cross-moving CAVs at an unsignalised intersection. 

where Vehicle B only needs to consider the interaction with Vehicle A since the follower’s \(Vehicle C’s\) actions are subject to Vehicle B’ state, but not vice versa. 

There could be three possible navigation situations for the three vehicles to pass the interaction and these situations are mutually exclusive: 

Situation 1 Vehicle A passes the intersection first, followed by Vehicle B and then Vehicle C. 

Situation 2 Vehicle B passes the intersection first, followed by Vehicle C and then Vehicle A. 

Situation 3 Vehicle B passes the intersection first, followed by Vehicle A and then Vehicle C. 

**Proposition** **4. ** *There* *still* *exist* *NE* *solutions* *for* *the* *3-player* *Nash* *game* *and* *there* *might* *be* *more* *than* *three* *NEs. * 

**Proof. ** If **Situation** **1** happens, *t* 

*A* *< * *t* 

*B* *< * *t* 

*C* holds. Under this situation, Player A takes the constantly acceleration actions until up to the speed limit \( X 

*A* \), if needed, and as a result its travel time *t* 

*A* under the dominate strategy is the minimal one. The 

best response of Player B is given by 

X 

*t*

*B* = arg min *B* *\(* X *B* *\)* s.t. *t* *B* ≥ *t* 

X 

*A* \+ *t* avoid *. * 

*B* 

Whether Player B to compromise depends on its initial state speed and *L* *B* . Player C behaves as a pure follower to Player B 

and its best solution is obtained by 

X 

*t*

*C* = arg min 

*C* *\(* X 

*C* *\)* s.t. Constraint \(10\) *. * 

X *C* 

The solution *\(* X 

*A* *, * X 

*B* *, * X 

*C* *\)* gives rise to a NE because no player can be better off anymore. Note that, because there may be multiple optimal solution X 

*B* for Player B, the feasible solution space subject to Constraint \(10\) for Player C might not be unique. This implies there might be multiple NE solutions with different payoffs under **Situation** **1** . 

When **Situation** **2** occurs, *t* 

*B* *< * *t* 

*C* *< * *t* 

*A* holds. Definitely, Player B takes its dominate strategy, ¯

X *B* , and the 3-player game 

turns to be a 2-player game between Vehicles C and A. Player C’s actions is obtained by 

¯

X *C* = arg min *t* *C* *\(* X *C* *\)* s.t. Constraint \(10\) *,* X *C* 

and Player A’s best-response strategy is given by 

¯

X *A* = arg min *t* *A* *\(* X *A* *\)* s.t. *t* *A* ≥ *t* 

X 

*C* \+ *t* avoid *. * 

*A* 

Of course, *\(* ¯X *A* *, * ¯X *B* *, * ¯X *C* *\)* is a NE solution. 

331 

*H. * *Wang, * *Q. * *Meng, * *S. * *Chen* *et* *al. * 

*Transportation* *Research* *Part* *B* *149* *\(2021\)* *322–346* 

Once **Situation** **3** appears, we have *t* 

*B* *< * *t* 

*A* *< * *t* 

*C* . Similar to **Situation** **2** , Player B takes its dominate strategy, ¯

X *B* . Player A’s 

best strategy can be obtained by 

ˇ

X *A* = arg min *t* *A* *\(* X *A* *\)* s.t. *t* *A* ≥ *t* 

X 

*B* \+ *t* avoid *. * 

*A* 

Player C’s best solution is given by 

ˇ

X *C* = arg min *t* *C* *\(* X *C* *\)* s.t. Constraint \(10\) and *t* *C* ≥ *t* 

X 

*A* \+ *t* avoid *, * 

*C* 

The derived solution *\(* ˇX *A* *, * ¯X *B* *, * ˇX *C* *\)* is also a unique NE solution. This completes the proof. 

**Remark** **4. ** There is a unique NE if all the three players have chance to take their dominate strategies \(constant acceleration until reaching the maximal speed\). 

The 3-player cooperative game can be formulated as 

\(COOP-2 Model\) 

min *t* *A* *\(* X *A* *\)* \+ *t* *B* *\(* X *B* *\)* \+ *t* *C* *\(* X *C* *\)* \(12\) 

X *A* *, * X *B* *, * X *C* 

s.t. *\(* 4 *\)* – *\(* 6 *\)* and *\(* 10 *\)* *. * 

**Proposition** **5. ** *Proposition* *3*  *still* *holds* *for* *the* *3-player* *case; * *i.e., * *the* *optimal* *solution* *to* *the* *3-player* *cooperative* *game* *must* *be* *in* *the* *NE* *solution* *set. * 

It is not difficult to prove Proposition 5 because, you know, there would also be one of the three situations under the cooperative mechanism. For each situation, the cooperative game can be separated into three sub-problems that each one is to minimize the travel time subject to corresponding feasibility. To save space, we here omit the proof. Interested readers can also prove it by proof of contradiction. 

We so far analyze the 3-player case and the similar logic could be applied for the n-player case \( *n* *> * 3 \). For one fleet with

*m* 

*m* 

1 

1 CAVs and the crossing-moving fleet with *m* 2 CAVs, there are *C* *m* 

possible situations for the n-player cooperative 

1 \+ 

*m* 2 

game. An easy-to-understand interpretation of this combination number is that *m* 1 vehicles in a *\(m* 1 \+ *m* 2 *\)* -length platoon are selected to form the first fleet and the rest ones reshape the crossing-moving fleet\). For example, there are 15 situations for the 6-player cooperative game \( *m* 1 = 2 and *m* 2 = 4 \). 

We explain a bit here for the real operational scenario, the implication of our findings and possible exploration of dynamic control over a long-term horizon. First, it is worth noting that there are only a few CAVs appearing at the same time at an unsignalized intersection. It implies there are limited number of possible situations for the cooperative game under realistic environment. Second, although it looks like hundreds of possible situations are needed to be examined, our findings \( Propositions 4 and 5 \) help to greatly reduce the computational complexity of solving the n-player cooperative game. 

Based on these findings, the optimal solution of cooperative game could be obtained by solving the best NE solution and the dimension of solution space of the cooperative game is far larger than the summed dimension of each sub-problems in the n-player Nash game \(see more details at the beginning of Section 5 \).  Third, the traffic flow is dynamic and thus the arrivals of CAV fleets are variable over time. At the meantime, there might exist some external disturbance at the intersection, such as a sudden invading pedestrian, which will affect the safe driving of the vehicles. A rolling-horizon approach can be established based on the fundamental models proposed in this paper. At each decision epoch, the components of CAVs fleets and optimal navigation strategies would be updated to accommodate traffic dynamics and possible external disturbance. 

**5. ** **Solution** **algorithm** 

In this section, we focus on developing the solution algorithm for the 2-player case and the proposed algorithm could be tailored to solve the n-player games as well. It is in essence difficult to find a Nash equilibrium \(NE\) with an extremely large number of discrete strategies, especially for a pure-strategy NE. The key challenge is that it is computationally intractable due to the multidimensional nature of the combination strategy space. Take the decision process of 20 time intervals for example. For each player, there are more than 3 20 game strategies \(infeasible ones included\) and the number of strategy combinations reaches 3 20 × 3 20 , which is incredible. Therefore, the traditional approaches, including explicit enumeration method and heuristic method with iterations, would be impossible to solve such game models. 

Fortunately,  Proposition 2 and Remark 1 shed novel light on developing an efficient solution algorithm. The philosophy of our algorithm is elaborated as follows. We can easily construct the dominant strategy for each player without considering the rival’s reaction, denoted by X 

*A* and X 

*B* . 

If | *t* *A* *\(* X 

*A* *\)* − *t* *B* *\(* X 

*B* *\)* | ≥ *t* avoid , then *\(* X 

*A* *, * X 

*B* *\)* is the unique NE solution for the noncooperative game model \(3\) .  In accordance with Proposition 3 ,  *\(* X 

*A* *, * X 

*B* *\)* would also be the optimal solution for the cooperative game model \(8\) .  

Once | *t* *A* *\(* X 

*A* *\)* − *t* *B* *\(* X 

*B* *\)* | *< * *t* avoid , there exist two Nash equilibria. The problem of solving a two-player Nash game is reduced to solve a pure mathematical programming model: 

332 





*H. * *Wang, * *Q. * *Meng, * *S. * *Chen* *et* *al. * 

*Transportation* *Research* *Part* *B* *149* *\(2021\)* *322–346* 

\(MP Model\) 

min *t* *i* *\(* X *i* *\)* 

\(13\) 

X *i*

s.t. *\(* 5 *\)* and *\(* 6 *\)* *, * 

*t* *i* *\(* X *i* *\)* ≥ *t* *i* − *\(* X 

*i* − *\)* \+ *t* avoid *, * ∀ *i* ∈ \{ *A, * *B* \} *, * *i* − ∈ \{ *A, * *B* \}\\\{ *i* \} *,* \(14\) 

where collision avoidance constraint \(4\) is replaced by a equivalent bound constraint \(14\) .  Once two NE solutions are obtained, the one with minimal sum of two payoffs is the solution of the cooperative game. 

The above MP model is a nonlinear integer optimization model. Note that the payoff function *t* *i* is a piecewise nonlinear function and critical segment thresholds also depend on the decisions taken by the player. This leads to a challenge to write the payoff function \(2\) as a closed-form expression, which also lifts the difficulty in finding a global optimal solution for the MP model. 

Solving NP-hard discrete optimization problems is usually an immense job requiring very efficient and robust algorithms. 

The branch and bound \(B&B\) paradigm is one of the prevailing tools in construction of such algorithms \( Androulakis et al., 

1995 \). However, a classical B&B algorithm might be inapplicable to solve the MP model since it is almost impossible to 

construct a promising convex relaxation or duality for the original problem. We in this study design a tailored B&B method to solve the MP model. The main procedures for the tailored B&B method are listed below: 

\(1\) **Bounding** **functions. ** The bound constraint \(14\) provides an ideal and fixed lower bound, *t* low = *t* *i* − *\(* X 

*i* − *\)* \+ *t* avoid . 

Therefore, we only need to update upper bound in searching process. A simple but easy-to-implement way is to take the best result out of all traversed samples/branches as the upper bound *t* up . 

\(2\) **Re-branching** **procedure. ** Since convex subproblems for the MP model cannot be formulated, a brute-forced branching approach would produce more than 3 *T* branches. Fortunately, Constraint \(5\) grants us an extra chance to re-branch the solution space. In practice, only limited number of changes in operational state \(empirically, *N* accel max ≤ 5 \) are allowed in order to ensure passenger comfortability, improve stability of manoeuvre and reduce energy consumption. 

This constraint enables us to decompose the whole solution space into a set of subtrees and remove a majority of infeasible ones. In detail, the sequence of decision variables would be partitioned into several consecutive subsequences \(the number of subsequences is no more than *N* accel 

max \+ 1 \). Each subsequence, called solution gene chain, consists of 

decision variables over several consecutive time intervals \(at least one\). All decision variables contained in a solution gene chain take the same value and are different from those contained in its neighboring solution gene chains. 

Fig. 4 provides an example to illustrate a subsequence division when *N* accel max = 3 . The first solution gene chain 

contains *κ* 1 decision variables with, for instance, acceleration action; the second one has *κ* 2 decision variables with, for instance, no action; and the third one takes a consecutive of *κ* 3 decision variables with, for instance, acceleration action; in the last solution gene chain, the player could decelerate over all remaining time intervals. 

One may wonder to what extent this re-branching can reduce the number of traversal branches. Take the case with *T* = 20 and *N* accel 

max = 3 as an example. The solution space can be further specified as *C* 3 

19 \+ *C* 2 

19 \+ *C* 1 

19 \+ *C* 0 

19 = 969 \+ 171 \+ 

**Fig. ** **4. ** An example to illustrate the re-branching and pruning procedures. 

333 

*H. * *Wang, * *Q. * *Meng, * *S. * *Chen* *et* *al. * 

*Transportation* *Research* *Part* *B* *149* *\(2021\)* *322–346* 

19 \+ 1 = 1160 subtrees. Each subtree would be expanded into different branch structure. As shown in Fig. 4 ,  for each four-layer subtree, there exist 3 × 2 3 = 24 branches. As a result, the number of branches is exponentially reduced from 3 20 ≈ 3 *. * 5 billions to only 25,425 via the re-branching procedure *\(* 969 × 3 × 2 3 \+ 171 × 3 × 2 2 \+ 19 × 3 × 2 \+ 1 × 3 = 

25 *, * 425 *\)* . 

\(3\) **Pruning** **rules. ** Theoretically, all regenerated branches should be traversed and compared to guarantee a global optimality. Given a subtree *g* ∈ *G*, a branch would contain a few hierarchical nodes. Let node 0 represent the root node, and node *m* 

*κ * denote the node at *κ* th layer and linked with the *m* th previous branch, where *m* ∈ \{ \+ *, * ◦ *, * −\} . The following pruning principles are used. 

\(i\) *The* *cut* *of* *the* *speed* *limit* *constraint. * If the current solution gene chain between node *m* *κ * and node *m* 

*κ*\+1 violates the 

speed limit constraint \(6\) ,  then all subbranches that contain the above solution gene chain will be pruned. Take the subtree in Fig. 4 as an example. When *v* *\(* node \+ 

1 *\)* *< * 0 or *v* *\(* node \+ 

1 *\)* *> * *v* max , node \+ 

1 will be removed from the 

subtree and eight branches behind this root will be pruned. 

\(ii\) *The* *cuts* *of* *the* *lower* *and* *upper* *bounds. * Several pruning conditions can be prescribed based on the constraints of the lower and upper bounds. In detail, when the accumulative distance *L* accum 

*i* 

is greater than or equal to *L* *i* , 

let us calculate the travel time *t* *i* and check whether it is between the lower and upper bounds. If | *t* *i* − *t* low | ≤ 

then terminate; else if *t* low *< * *t* *i* *< * *t* up , then update *t* up = *t* *i* and return to the tail node to examine other branches; otherwise, eliminate the current head node and prune all related branches. When *L* accum *i* 

*< * *L* *i* , we then move to 

the node in the next layer and repeat all above examinations until successfully pruning or traversing all branches in the subtree. 

Based on the above analysis, the following cuts for pruning and bounding are specified: 

*• The* *speed-limit* *cut* : the solution \(gene chain\) violates the speed limit constraint \(6\) .  

*• The* *first* *upper-bound* *cut* : *L* accum *< * *L* *i* and *t* accum ≥ *t* up . 

*• The* *second* *upper-bound* *cut* : *L* accum ≥ *L* *i* and *t* *i* ≥ *t* up . 

*• The* *lower-bound* *cut* : *L* accum ≥ *L* *i* and *t* *i* *< * *t* low . 

*• The* *updated* *upper* *bound* *cut* : *L* accum ≥ *L* *i* and *t* *i* *< * *t* up . 

*• The* *feasibility* *cut* *for* *the* *enumeration* *method* : if the solution violates the speed limit constraint \(6\) or maximal state switching constraint \(5\) .  

\(4\) **Initial** **upper** **bound** **and** **convergence** **criterion. ** Although often not explicitly mentioned, an important factor in efficiently solving the integer nonlinear optimization by B&B is to construct a good upper bound at initial stage so as to facilitate the pruning. A series of heuristics could be used to determine the initial upper bound, such as simulated annealing method and genetic algorithm. Regarding the convergence criterion, we should note that the lower bound may be unreachable. Therefore, the algorithm will be terminated when either the bound gap condition is satisfied or the re-branching solution space is ergodic. 

**6. ** **Numerical** **examples** 

In this section, we provide several numerical experiments to shed light on how well the two game models work, validate the analytical results and assess the computational efficiency of the developed algorithm. First of all, we provide a simple numerical experiment \(Case I\) with a small number of decision epochs, *T* = 5 , and *N* accel max = 1 for gaining some initial 

insights. In Case I, we implement enumeration method to obtain the optimal solutions for the two game models. Second, Case II offers a few numerical experiments to assess the computation efficiency of the proposed solution algorithm. Case III and Case IV are presented to test the models’ scalability, and to showcase the possibility of relaxing Assumption 1, where replacing instantaneous acceleration with a more practical scenario of constant acceleration. Case III demonstrates a 3-player case, while Case IV illustrates how to extend our proposed models to form a rolling horizon decision system. Algorithms 1 is compiled with g\+\+ on a Dell Workstation with an Intel Xeon 3.0GHz ×2 CPU and a virtual Linux operating system \(64-bit Ubuntu with 16GB RAM\). 

*6.1. * *Case* *I* *for* *assessing* *the* *consistency* *between* *theoretical* *and* *numerical* *results* We look into the consistency between theoretical and numerical results in this section. The input data for two CAVs are given below: initial speeds of *v* −1 *,A* = 6 m/s and *v* −1 *,B* = 10 m/s , unit velocity increment *v* = 4 m/s , unit time interval *t* = 4 s , *t* avoid = 4 s , *v* max = 20 m/s , *L* *A* = 100 m and *L* *B* = 120 m . After re-branching, there are 27 possible solutions in total. 

Table 1 lists the feasible ones that satisfy the driving-state switching constraint \(5\) and speed limit constraint \(6\) for each player. 

The payoff table is presented below \( Table 3 \).  All the three Propositions and the Corollary are examined and verified against the numerical results obtained under Cases I.  Table 2 summarizes the consistency validation results. Some details of the validation are elaborated here. 

\(1\) Proposition 1 asserts that pure-strategy NEs always exist. It follows from Table 3 that there exist 4 pure-strategy NEs. 

334 

*H. * *Wang, * *Q. * *Meng, * *S. * *Chen* *et* *al. * 

*Transportation* *Research* *Part* *B* *149* *\(2021\)* *322–346* 

**Table** **1** 

The feasible solutions for each player. 

Strategy X *κA* 

Specification 

Strategy X *κB* 

Specification 

X 1 

*A* 

\{ 0 *, * 0 *, * 0 *, * 0 *, * 0 \} 

X 1 

*B* 

\{ 0 *, * 0 *, * 0 *, * 0 *, * 0 \} 

X 2 

*A* 

\{−1 *, * 1 *, * 1 *, * 1 *, * 1 \} 

X 2 

*B* 

\{−1 *, * 0 *, * 0 *, * 0 *, * 0 \} 

X 3 

*A* 

\{ 1 *, * 0 *, * 0 *, * 0 *, * 0 \} 

X 3 

*B* 

\{ 1 *, * 0 *, * 0 *, * 0 *, * 0 \} 

X 4 

*A* 

\{ 0 *, * 0 *, * 0 *, * 0 *, * −1 \} 

X 4 

*B* 

\{ 0 *, * 0 *, * 0 *, * 0 *, * −1 \} 

X 5 

*A* 

\{ 0 *, * 0 *, * 0 *, * 0 *, * 1 \} 

X 5 

*B* 

\{ 0 *, * 0 *, * 0 *, * 0 *, * 1 \} 

X 6 

*A* 

\{ 0 *, * 0 *, * 1 *, * 1 *, * 1 \} 

X 6 

*B* 

\{−1 *, * −1 *, * 1 *, * 1 *, * 1 \} 

X 7 

*A* 

\{ 1 *, * 1 *, * 0 *, * 0 *, * 0 \} 

X 7 

*B* 

\{ 1 *, * 1 *, * 0 *, * 0 *, * 0 \} 

X 8 

*A* 

\{ 1 *, * 1 *, * −1 *, * −1 *, * −1 \} 

X 8 

*B* 

\{ 1 *, * 1 *, * −1 *, * −1 *, * −1 \} 

X 9 

*A* 

\{ 0 *, * 0 *, * 0 *, * 1 *, * 1 \} 

X 9 

*B* 

\{ 0 *, * 0 *, * 0 *, * −1 *, * −1 \} 

X 10 

*A* 

\{ 1 *, * 1 *, * 1 *, * 0 *, * 0 \} 

X 10 

*B* 

\{ 0 *, * 0 *, * 0 *, * 1 *, * 1 \} 

X 11 

*A* 

\{ 1 *, * 1 *, * 1 *, * −1 *, * −1 \} 

- 

- 

**Table** **2** 

The consistency between theoretical and numerical results. 

Proposition 

Consistent with computational results? 

√ 

Proposition 1 

√ 

Proposition 2 

√ 

Corollary 1 

√ 

Proposition 3 

\(2\) Proposition 2 states that the pure-strategy NE solutions *\(* X 

*A* *, * X 

*B* *\)* contain at least one player’s dominant strategy. It 

follows from Tables 1 and 3 that the four NE solutions are 

⎧ 

⎪ 

⎪solution 1: *\(* X 6 



⎨

*A* *, * X 7 

*B* *\)* *, * 

that player *B* takes his dominant strategy *, * 

solution

*\(*

2: *\(* X 6 

X 

*A* *, * X 8 

*B* *\)* *, * 

that player *B* takes his dominant strategy *, * 

*A* *, * X 

*B* *\)* = ⎪ 

⎪ 

⎩solution 3: *\(* X 10 



*A* *, * X 6 

*B* *\)* *, * 

that player *A* takes his dominant strategy *, * 

solution 4: *\(* X 11 

*A* *, * X 6 

*B* *\)* *, * 

that player *A* takes his dominant strategy *. * 

All the four solutions satisfy the condition given in Proposition 2 .  Specifically, the former two NE solutions drive Player *B* to pass the intersection as soon as possible before reaching the highest speed of 18 m/s . Similarly, the latter two NE solutions let Player *A* move as fast as possible and achieve the highest speed of 18 m/s . 

\(3\) Corollary 1 claims that there may be more than two NEs, but at most two different payoffs for each player among all NEs. The first part clearly holds. The second assertion is also consistent with the numerical results. It is not difficult to verify that, under Solution 1 and 2, CAV B has already passed the conflict point before the third action. Therefore, the succeeding actions after time interval *k* = 2 have no impact on the game results \(the game terminates after that time and no interaction risk between two CAVs exists\). As a result, Solutions 1 and 2 contribute the identical payoff for each player that *P* *A* = 12 6 

7 and *P* *B* = 7 5 

9 . In turn, a similar situation applies to Solutions 3 and 4 in which *P* *A* = 8 2 

9 

and *P* *B* = 17 5 

7 . 

\(4\) Proposition 3 states that the optimal solution for the cooperative game must be one of NE solutions. It can be observed from Table 3 \(the last row\) that the cooperative game model arrives its optimal objective value of 20 26 

63 when 

Solution 1 or Solution 2 is taken. Both are NE solutions, and the consistency between Proposition 3 and computed results is demonstrated. 

*6.2. * *Case* *II* *for* *assessing* *the* *computational* *efficiency* *of* *the* *developed* *algorithm* The input data for the experiments in Case II are given below: *T* = 20 , *v* *A, * −1 = 6 m/s , *v* *B, * −1 = 10 m/s , unit velocity increment *v* = 1 m/s , unit time interval *t* = 1 s , *t* avoid = 4 s , *v* max = 16 m/s , *L* *A* = 100 m and *L* *B* = 120 m . The convergence gap is * *= 10 −5 . The maximal permitted switching frequency of driving state, *N* accel max , changes from 4 to 20. The dominant 

strategies for two players are 

˜ X *A* := \{ *x* *A,k* = 1 *, * if *k* ≤ 9 *, * and *x* *A,k* = 0 *, * otherwise \} *, * 

˜ 

X *B* := \{ *x* *B,k* = 1 *, * if *k* ≤ 6 *, * and *x* *B,k* = 0 *, * otherwise \} 

and the respective payoffs are *t* *A* *\(* ˜ 

X *A* *\)* = 9 1 

16 s and *t* *B* *\(* ˜ 

X *B* *\)* = 8 7 

16 s . Then the two lower bounds for two players are, respec- 

tively, *t* *A* 

low = 12 7 

16 s and *t* *B* 

low = 13 1 

16 s . 

The proposed B&B algorithm and enumeration method are both implemented to solve the MP model. In solving the MP 

model by enumeration method, a recursive function is coded to generate all possible solutions \(the number of solutions traversed is 3 20 = 3 *, * 486 *, * 784 *, * 401 \). When using the developed B&B algorithm, another recursive function is tailored for the re-branching procedure. 

335 

*H. * *Wa*

*ng, * *Q. * *Meng, *

*S. * *Chen*

*et* *al. * 

**Table** **3** 





The payoff table *P* *A* *\(* X *κ*

f or the strategic Nash game. 

*A* *, * X 

*κB* *\)* *, * *P* *B* *\(* X *κA* *, * X *κB* *\)* X *κA* \\ payoffs \\ X *κB* X 1 

*B* 

X 2 

*B* 

X 3 

*B* 

X 4 

*B* 

X 5 

*B* 

X 6 

*B* 

X 7 

*B* 

X 8 

*B* 

X 9 

*B* 

X 10 

*B* 

1 

−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−→ −−−−−−−−−−−−−−→ 

X 1 

*\(* 16 2 

*\(* 16 2 

*A* 

*\(* 16 2 

3 *, * 12 *\)* 

*\(*∞ *, * ∞ *\)* 

*\(* 16 2 

3 *, * 8 4 

7 *\)* 

*\(* 16 2 

3 *, * 12 *\)* 

*\(* 16 2 

3 *, * 12 *\)* 

*\(*∞ *, * ∞ *\)* 

3 *, * 7 5 

9 *\)* 

3 *, * 7 5 

9 *\)* 

*\(* 16 2 

3 *, * 12 *\)* 

*\(* 16 2 

3 *, * 12 *\)* 

X 2 

*A* 

*\(*∞ *, * ∞ *\)* 

*\(* 14 *, * 20 *\)* 

2 



*\(* 14 *, * 8 4 

7 *\)* 

*\(*∞ *, * ∞ *\)* 

*\(*∞ *, * ∞ *\)* 

*\(*∞ *, * ∞ *\)* 

*\(* 14 *, * 7 5 

9 *\)* 

*\(* 14 *, * 7 5 

9 *\)* 

*\(*∞ *, * ∞ *\)* 

*\(*∞ *, * ∞ *\)* 

X 3 

*\(*∞ *, * ∞ *\)* 

*\(*∞ *, * ∞ *\)* 

*\(*∞ *, * ∞ *\)* 

*\(* 10 *, * 17 5 

*A* 

*\(*∞ *, * ∞ *\)* 

*\(* 10 *, * 20 *\)* 

7 *\)* 

*\(*∞ *, * ∞ *\)* 

*\(*∞ *, * ∞ *\)* 

*\(*∞ *, * ∞ *\)* 

*\(*∞ *, * ∞ *\)* 

X 4 

*A* 

*\(* 18 *, * 12 *\)* 

*\(*∞ *, * ∞ *\)* 

*\(* 18 *, * 8 4 

7 *\)* 

*\(* 18 *, * 12 *\)* 

*\(* 18 *, * 12 *\)* 

*\(*∞ *, * ∞ *\)* 

*\(* 18 *, * 7 5 

9 *\)* 

*\(* 18 *, * 7 5 

9 *\)* 

*\(* 18 *, * 12 *\)* 

*\(* 18 *, * 12 *\)* 

X 5 

*A* 

*\(* 16 2 

5 *, * 12 *\)* 

*\(*∞ *, * ∞ *\)* 

*\(* 16 2 

5 *, * 8 4 

7 *\)* 

*\(* 16 2 

5 *, * 12 *\)* 

*\(* 16 2 

5 *, * 12 *\)* 

*\(*∞ *, * ∞ *\)* 

*\(* 16 2 

5 *, * 7 5 

9 *\)* 

*\(* 16 2 

5 *, * 7 5 

9 *\)* 

*\(* 16 2 

5 *, * 12 *\)* 

*\(* 16 2 

5 *, * 12 *\)* 

33

X 6 

*A* 

*\(*∞ *, * ∞ *\)* 

*\(* 12 6 

7 *, * 20 *\)* 

*\(* 12 6 

7 *, * 8 4 

7 *\)* 

*\(*∞ *, * ∞ *\)* 

*\(*∞ *, * ∞ *\)* 

*\(* 12 6 

7 *, * 17 5 

7 *\)* 



*\(***12** **6** 

6

↓

**7** *, * **7** **5** 

**9** *\)* 



*\(***12** **6** 

**7** *, * **7** **5** 

**9** *\)* 

*\(*∞ *, * ∞ *\)* 

*\(*∞ *, * ∞ *\)* 



X 7 



↓ 

*A* 

*\(*∞ *, * ∞ *\)* 

*\(* 8 2 

7 *, * 20 *\)* 

*\(*∞ *, * ∞ *\)* 

*\(*∞ *, * ∞ *\)* 

*\(*∞ *, * ∞ *\)* 

*\(* 8 2 

7 *, * 17 5 

7 *\)* 

*\(*∞ *, * ∞ *\)* 

*\(*∞ *, * ∞ *\)* 

*\(*∞ *, * ∞ *\)* 

*\(*∞ *, * ∞ *\)* 

X 8 

*A* 

*\(*∞ *, * ∞ *\)* 

*\(* 8 2 

5 *, * 20 *\)* 

*\(*∞ *, * ∞ *\)* 

*\(*∞ *, * ∞ *\)* 

*\(*∞ *, * ∞ *\)* 

*\(* 8 2 

5 *, * 17 5 

7 *\)* 

*\(*∞ *, * ∞ *\)* 

*\(*∞ *, * ∞ *\)* 

*\(*∞ *, * ∞ *\)* 

*\(*∞ *, * ∞ *\)* 

X 9 

*A* 

*\(*∞ *, * ∞ *\)* 

*\(* 15 4 

5 *, * 20 *\)* 

*\(* 15 4 

5 *, * 8 4 

7 *\)* 

*\(*∞ *, * ∞ *\)* 

*\(*∞ *, * ∞ *\)* 

*\(*∞ *, * ∞ *\)* 

*\(* 15 4 

5 *, * 7 5 

9 *\)* 

*\(* 15 4 

5 *, * 7 5 

9 *\)* 

*\(*∞ *, * ∞ *\)* 

*\(*∞ *, * ∞ *\)* 

−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−→ 

↓ 

X 10 

*A* 

*\(*∞ *, * ∞ *\)* 

*\(* 8 2 

9 *, * 20 *\)* 

↓ 

*\(*∞ *, * ∞ *\)* 

*\(*∞ *, * ∞ *\)* 

*\(*∞ *, * ∞ *\)* 

*\(***8** **2** 

**9** *, * **17** **5** 

**7** *\)* 

*\(*∞ *, * ∞ *\)* 

*\(*∞ *, * ∞ *\)* 

*\(*∞ *, * ∞ *\)* 

*\(*∞ *, * ∞ *\)* 

−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−→ 

X 11 

*A* 

*\(*∞ *, * ∞ *\)* 

*\(* 8 2 

9 *, * 20 *\)* 

*\(*∞ *, * ∞ *\)* 

*\(*∞ *, * ∞ *\)* 

*\(*∞ *, * ∞ *\)* 

*\(***8** **2** 

**9** *, * **17** **5** 

**7** *\)* 

*\(*∞ *, * ∞ *\)* 

*\(*∞ *, * ∞ *\)* 

*\(*∞ *, * ∞ *\)* 

*\(*∞ *, * ∞ *\)* 

min \{ *P* *A* \+ *P* *B* \} 

28 2 

5 

28 2 

9 

21 3 

7 

28 2 

5 

28 2 

5 

25 59 

63 

**20** **26** 

**63** 

**20** **26** 

**63** 

28 2 

5 

28 2 

5 

*Transport*

Note: 1 

– the game evolves from Player *B * given the rival’s strategy of X 1 

*A* ; 2 

– the game starts from Player *A* given the rival’s strategy of X 2 

*B* . 

*ation*

*Resear*

*ch* *Pa*

*rt* *B* *14*

*9* *\(202*

*1\)* *322–346*





*H. * *Wang, * *Q. * *Meng, * *S. * *Chen* *et* *al. * 

*Transportation* *Research* *Part* *B* *149* *\(2021\)* *322–346* 

**Table** **4** 

The computed results for Case II when *N* accel 

max = 4 and Player B takes his dominant strategy. 

Performance item 

B&B algorithm 

Enumeration method 

computation time \(s\) 

0.09 

1,077.653 

*N* tree 

5036 

5036 

*N* bran 

211,473 

3,486,784,401 

*N* cut 

81,623 

3,486,658,051 

cut 

*N* speed 

23,796 

3,282,746,961 

details 

*N* switch 

- 

203,911,090 

*N* 1 

upper 

24,099 

- 

*N* 2 

upper 

18,408 

- 

*N* lower 

15,320 

- 

*N* update 

8 

3 

optimal payoffs 

*\(t* 

*A* *, * *t* 

*B* *\)* = *\(* 12 4 

9 *, * 8 7 

16 *\)* 

*\(t* 

*A* *, * *t* 

*B* *\)* = *\(* 12 4 

9 *, * 8 7 

16 *\)* 

optimal solution for 

0,1,0,0,0,1,1,0,0,0, 

0,0,0,0,0,1,1,1,1,1,0,-1, 

Player A \( X 

*A* \) 

0,0,0,0,0,0,0,0,0,0 

-1,-1,-1,-1,-1,-1,-1,-1 

**Fig. ** **5. ** The convergence of solving the MP model by the developed B&B algorithm \( *N* accel max = 4 and Player B takes his dominant strategy\). 

Some notations are defined to facilitate the following narration: 

*N* tree 

the number of subtrees; 

*N* bran 

the number of re-branched branches; 

*N* cut 

the total number of active cuts; 

*N* update 

the number of updated upper bounds; 

*N* speed 

the number of speed-limit cuts; 

*N* 1 

upper 

the number of 1st upper-bound cuts; 

*N* lower 

the number of lower-bound cuts; 

*N* 2 

upper 

the number of 2nd upper-bound cuts; 

*N* switch 

the number of solutions violates Constraint \(5\) ;  

*N* feas 

the number of feasible solutions filtered by Constraints \(5\) and \(6\) ;  

*t* bb 

computation time for B&B algorithm; 

*t* enum 

computation time for enumeration method; 

*6.2.1. * *Experiments* *when* *player* *B* *takes* *his* *dominant* *strategy* We first look at the experiment with *N* accel 

max = 4 when Player B takes his dominant strategy. The computed results are 

presented in Table 4 .  It can be observed that two solution algorithms generate identical payoffs for two players at NE, although different optimal strategies are obtained by the two methods. This implies that both solution methods find global optimal solutions and Corrollay 1 is validated here as there are at least two NE solutions. 

For B&B algorithm, 5036 subtrees and 211,473 branches \(solutions\) are obtained after running the re-branching procedure. 

In solving the model, 81,623 cuts are activated for pruning. The convergence \(bounding process\) is plotted in Fig. 5 .  The upper bound is updated eight times in the execution of B&B algorithm and the gap between the lower and upper bounds is reduced from \+ ∞ to 1 

144 s \( 1 

144 = 12 4 

9 − 12 7 

16 \).  Fig. 6 gives an intuitive illustration on the distribution of different types 337 

*H. * *Wang, * *Q. * *Meng, * *S. * *Chen* *et* *al. * 

*Transportation* *Research* *Part* *B* *149* *\(2021\)* *322–346* 

**Fig. ** **6. ** The distribution of the former 1500 cuts in solving Player A’s optimal strategy. 

of cuts for pruning and bounding. On the other hand, enumeration method creates more than 3 billions of cuts and finally generates 126,350 feasible solutions. After updating the upper bound 3 times, the optimal solution is found. 

As expected, B&B algorithm outperforms enumeration method tremendously in terms of computation time. Specifically, it only needs 0.09s to solve the MP model via B&B algorithm, while enumeration method spends more than one thousand seconds. The excellent computational efficiency of B&B algorithm attributes to two aspects: \(1\) **Re-branching** **technique** : The re-branching procedure embedded in B&B algorithm effectively filters solutions that are infeasible under Constraint \(5\) and vastly reduces the solution space \(from 3 20 to 211,473\). When using enumeration method, computer has to check each solution for its feasibility. Such inflexible examination is inefficient. 

\(2\) **Pruning** **technique** : Enumeration method compares feasible solutions one by one and eliminates at most one solution at a time. In contrast, the pruning of B&B algorithm is more advanced and efficient. As shown in Table 4 ,  the amount of 211,473 branches are traversed with only 81,623 cuts \(i.e., pruning actions\). On average, 2.59 branches are compared and cut off each time. This efficiently accelerates the searching procedure. 

*6.2.2. * *Sensitivity* *analysis* *of* *N* *accel* 

*max* *on* *computational* *efficiency* 

The maximal permitted switching frequency of driving state, *N* accel 

max , exerts vital impact on numbers of subtrees and 

branches for B&B algorithm and on number of feasibility cuts for enumeration method. In this section, we conduct a sensi-tivity analysis on computational efficiency by changing *N* accel 

max from 4 to 20 when Player A takes its dominant strategy. 

Table 5 summarizes the results for the experiments with different *N* accel max using B&B algorithm. The variations of computation time, number of updated upper bounds and a ratio index are plotted in the figure for an easy illustration. Some observations are shared below. 

\(1\) As shown in Fig. 7 ,  computation time steadily climbs up as *N* accel max increases since the feasible solution space \(the 

number of branches\) is explosively expanded. Number of updated upper bounds exhibits a similar trend, except for the case with *N* accel 

max = 9 . As feasible solution space expands when *N* accel 

max increases, number of updated upper bounds 

is expected to increase. However, the increase may no be monotonic as the order of generated subtrees \(the traversed sequence of solution space\) plays a part in when and where to locate the improved solutions and the NEs. 

\(2\) More than two optimal strategies exist for the non-cooperative game model. It can be observed that, when *N* accel max = 10 , 

all the five solutions listed in Table 5 are optimal strategies for Player B. This is consistent with Corrollay 1 .  

\(3\) A performance index *γ* prun is defined to measure the efficiency of pruning, 

*γ*

*N* bran 

prun := 

*. * 

*N* cut 

The greater the value of *γ* prun is, the better the pruning effect is.  Fig. 7 shows that the pruning becomes increasingly efficient as *N* accel 

max increments. This is intuitive since the number of layers for the re-branched subtrees raises when relaxing Constraint \(5\) .  As a result, a cut for the same solution gene chain may remove more infeasible and/or inferior branches. 

338 

*H. * *Wa*

*ng, * *Q. * *Meng, *

*S. * *Chen*

*et* *al. * 

**Table** **5** 

The results for experiments with different *N* accel 

max using the developed B&B algorithm. 

computation 

*γ* prun = 

*N* accel 

time \( *t* bb 

*N*

com



*N* 

bran 

max 

tree

\) 



*N* bran 

*N* cut 

*N* speed 

*N* 1 

upper 

*N* 2 

upper 

*N* lower 

*N* update 

*N* 

cut 

4 

0.088 

5036 

211,473 

84,011 

22,957 

16,012 

17,098 

27,944 

7 

2.517 

5 

0.335 

16,664 

1,327,761 

428,540 

87,115 

92,409 

95,135 

153,881 

7 

3.098 

6 

1.037 

43,796 

6,537,105 

1,709,529 

251,480 

403,578 

403,319 

651,152 

9 

3.824 

7 

3.067 

94,184 

25,886,097 

5,479,545 

570,220 

1,376,608 

1,351,150 

2,181,567 

10 

4.724 

33

8 

7.771 

169,766 

83,933,073 

14,394,927 

1,038,728 

3,769,139 

3,668,142 

5,918,918 

13 

5.831 

9 

9 

16.83 

262,144 

225,825,681 

31,484,121 

1,559,867 

8,456,030 

8,224,255 

13,243,969 

10 

7.173 

10 

31.449 

354,522 

509,610,897 

58,139,653 

1,995,940 

15,828,061 

15,476,659 

24,838,993 

17 

8.765 

15 

96.361 

523,128 

3,212,516,241 

183,476,200 

2,443,720 

49,790,230 

50,912,025 

80,330,225 

53 

17,509 

20 

98.873 

524,288 

3,486,784,401 

188,089,222 

2,443,850 

50,933,150 

52,287,046 

82,425,176 

69 

18.538 

optimal payoffs at NE: 

*t* *A* = 9 1 

16 *, * *t* 

*B* = 13 1 

14 . 

optimal solution for Player A: 

X 

*A* = ˜ 

X *A* for all tested experiments. 

*N* accel 

max 

optimal solution for Player B \( X 

*B* \) 

*N* accel 

max 

optimal solution for Player B \( X 

*B* \) 

4 

\{−1 *, * 1 *, * −1 *, * −1 *, * −1 *, * −1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 \} 

5, 6 

\{ 0 *, * −1 *, * 0 *, * −1 *, * −1 *, * −1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 \} 

7 

\{−1 *, * 0 *, * −1 *, * 0 *, * 0 *, * −1 *, * 0 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 \} 

8 

\{−1 *, * 0 *, * −1 *, * 0 *, * −1 *, * 1 *, * −1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 \} 

9, 10, 15, 20 

\{−1 *, * 0 *, * −1 *, * 0 *, * −1 *, * 0 *, * 1 *, * 0 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 \} 

*Transport*

*ation*

*Resear*

*ch* *Pa*

*rt* *B* *14*

*9* *\(202*

*1\)* *322–346*



*H. * *Wang, * *Q. * *Meng, * *S. * *Chen* *et* *al. * 

*Transportation* *Research* *Part* *B* *149* *\(2021\)* *322–346* 

**Fig. ** **7. ** The performance of B&B algorithm with increasing *N* accel 

max . 

**Table** **6** 

The results for experiments with different *N* accel 

max using enumeration method. 

*γ*

computation 

com = 

*t* 

enum 

*N* accel 

time \( *t* enum 

*N*

com



com 

max 

feas

\) 



*N* update 

*t* 

bb 

com 

4 

1,084.839 

126,350 

9 

12,327.716 

5 

1,091.809 

879,096 

9 

3,259.131 

6 

1,114.766 

4,697,890 

9 

1,074.991 

7 

1,149.826 

19,836,501 

9 

374.903 

8 

1,169.382 

67,708,954 

9 

150.480 

9 

1,209.526 

189,790,771 

9 

71.867 

10 

1,263.646 

442,519,665 

9 

40.181 

15 

1,441.082 

3,011,367,419 

9 

14.955 

20 

1,523.828 

3,282,746,961 

9 

15.412 

optimal payoffs at NE: *t* *A* = 9 1 

16 *, * *t* 

*B* = 13 1 

14 . optimal solutions: X 



*A* = ˜ 

X *A* and X 

*B* = 

\{−1 *, * −1 *, * −1 *, * −1 *, * 0 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 0 *, * 1 *, * −1 *, * −1 *, * −1 *, * −1 *, * −1 *, * −1 \} . 

\(4\) When a CAV is allowed to switch its driving state within a permitted level, e.g., *N* accel max = 4 , the very small computation 

time \( *< * 100 ms\) of the developed B&B algorithm indicates that the model and algorithm can be readily deployed in future online CAV decision system to help CAVs navigate through unsignalised intersections. 

The results generated by enumeration methods are provided in Table 6 .  The variations of computation time and number of feasible solutions with increasing *N* accel 

max are displayed in Fig. 8 .  It seems that computation time increases linearly while number of feasible solutions exponentially expands. Specifically, the computation time is 1084.84s when *N* accel max = 4 and becomes 1,523.83s when *N* accel 

max = 20 . The increment is about 40%, which is far less than the case for B&B algorithm. This is because no matter what the setting of *N* accel 

max is, all 3 20 solutions are examined and/or compared according to the feasibility 

cuts and updated upper bound. 

We now compare the performance of the two solution methods. Firstly, both methods can find the global optimal solution for the MP model, although their optimal solutions may be different. Secondly, a computational efficiency index is defined as 

*γ*

*t* enum 

com 

com := 

*. * 

*t* bb 

com 

Fig. 9 plots the variation of *γ* com as *N* accel 

max increases from 4 to 20. B&B algorithm outperforms enumeration method 

substantially, especially when *N* accel 

max is relatively small. For example, when *N* accel 

max = 4 , the computation time *t* enum 

com is more 

than ten thousand times as compared to *t* bb 

com \( *γ* com = 12 *, * 327 *. * 72 \). 

340 

*H. * *Wang, * *Q. * *Meng, * *S. * *Chen* *et* *al. * 

*Transportation* *Research* *Part* *B* *149* *\(2021\)* *322–346* 

**Fig. ** **8. ** The performance of enumeration method with increasing *N* accel 

max . 

**Fig. ** **9. ** The computational efficiency comparison between two solution algorithms. 

In Section 6.2.1 ,  we have discussed the merit of the B&B algorithm stemming from double-effect of re-branching and pruning. It is not surprising that the role of re-branching weakens as *N* accel 

max increases, and would lose effect once *N* accel 

max ≥ *T* 

\(i.e. Constraint \(5\) becomes inactive\). In contrast, the power of pruning is strengthened with the increase of *N* accel max ; i.e. *γ* prun 

increases from 2.517 to 18.538 \(see the last column in Table 5 \).  Overall, the advantage of B&B on computational efficiency gradually deceases with *N* accel 

max ; *γ* com goes down from 12,327.72 to 15.41, as shown in Fig. 9 .  Nonetheless, when *N* accel max = 20 

\(even though re-branching does not work\), B&B algorithm still saves much computation time. 

It is apparent that B&B algorithm is more appealing even if re-branching does not substantially reduce the solution space when *N* accel 

max is close to the number of decision epochs. This is not to deny the importance of re-branching. In fact, we have done a larger experiment with *T* = 30 and *N* accel 

max = 10 . It needs 22 minutes and 50.021 seconds to obtain a global optimal 

341 

*H. * *Wang, * *Q. * *Meng, * *S. * *Chen* *et* *al. * 

*Transportation* *Research* *Part* *B* *149* *\(2021\)* *322–346* 

**Algorithm** **1** The B&B algorithm developed to compute pure-strategy NEs. 

**Input:** initial states for two AVs, e.g. initial velocities *v* −1 *,A* and *v* −1 *,B* , and initial distances *L* *A* and *L* *B* , initial upper bound *t* up and tolerance value . 

**Output:** optimal strategies for two players *\(* X 

*i* *, * X 

*i* − *\)* and corresponding payoffs *P* *i* and *P* *i* − . 

1: **Initialization** : Construct the dominant strategy X 

*i* − of Player *i* − and obtain the lower bound 

*t* low = *t* *i* − *\(* X 

*i* − *\)* \+ *t* avoid for 

Player *i* . Partition the solution space *i* | X based on Constraint~\(5\) into feasible subtrees, *g* ∈ *G* \(re-branching\). 

*i* 

−

2: **B&B** **Procedure** : Search the pure-strategy NE via B&B and let *m* = 0 ; 3: **for** each subtree *g* ∈ *G* **do** 

4: Traverse the tree by *depth* *first* *search* *\(DFS\)* according to the following principles: 5: **if** solution gene chain between node *m* 

*κ * and node *m* 

*κ*\+1 violates Constraint~\(6\) \( **Examination** **of** **the** **speed-limit** **cut** \) 6: remove all subbranches originated from node *m* 

*κ *, and let *m* = *m* \+ 1 and repeat the **Examination** **of** **the** **speed-limit** **cut** ; 7: **else** 

8: 

**if** *L* accum *< * *L* *i* **then** 

9: calculate accumulative time *t* accum ; 

10: 

**if** *t* accum ≥ *t* up **then** 

11: eliminate all subbranches rooted from node *m* 

*κ * and, let *m* = *m* \+ 1 and return to node *m* 

*κ * to examine other branches; 

12: 

**else** 

13: let *κ *= *κ *\+ 1 , *m* = 0 and go to the **Examination** **of** **the** **speed-limit** **cut** ; 14: 

**end** **if** 

15: **else** 

16: compute *t* *i* based on the realized solution genes; 

17: 

**if** *t* *i* *< * *t* low or *t* *i* *> * *t* up **then** 18: eliminate all subbranches rooted from node *m* 

*κ * and, let *m* = *m* \+ 1 and return to node *m* 

*κ * to examine other branches; 

19: 

**else** 

20: 

**if** | *t* *i* − *t* low | ≤ * ***then** 

21: terminate and report the solution; 

22: 

**else** 

23: update *t* up = *t* *i* and record current solution, let *m* = *m* \+ 1 and go to the **Examination** **of** **the** **speed-limit** **cut** to repeat-edly traverse other branches from node *m* 

*κ *; 

24: 

**end** **if** 

25: 

**end** **if** 

26: 

**end** **if** 

27: 

**end** **if** 

28: **end** **for** 

solution by the developed B&B algorithm. Nonetheless, enumeration method is unable to give us a result \(the execution was terminated after 48 hours\). This justifies the value of re-branching. 

*6.3. * *Case* *III* *for* *illustrating* *the* *3-player* *games* In Case III, we add one more player, Vehicle C, into the system, and consider constant acceleration rather than instantaneous acceleration to characterize vehicle movements. The input data for vehicles A and B are the same as those used in Case II. Vehicle C follows Vehicle A with an initial speed *v* *C, * 0 = 6 m/s and *L* *C* = 120 m . The time to avoid rear-end collision is set as ˜ *t* avoid = 2 *. * 5 s and *N* accel 

max = 4 . Suppose these three vehicles arrive at the intersection \(V2V control area\) in the following order \(upon their distances to the conflict point and their initial speeds\): Vehicle A, Vehicle B, and Vehicle C.  Table 7 

summarizes the results for the 3-player case. 

*6.3.1. * *The* *effect* *of* *relaxing* *Assumption* *1* *to* *use* *constant* *acceleration* We firstly examine the estimation error in terms of travel time between the instantaneous-acceleration driving and constant-acceleration driving. It is intuitive that travel time under instantaneous-acceleration driving is shorter than that under constant-acceleration driving, but we wish to examine the extent of the difference here. Let the optimal travel time under the constant-acceleration scenario be the benchmark. When Player A adopts its dominate strategy, the average relative estimation error is 





1 | 9 1 

| 13 1 

*P* 

16 − 9 *. * 362291 | 

14 − 13 *. * 36 6 6 | 

error = 

\+ 

= 1 *. * 834% *. * 

2 

9 *. * 362291 

13 *. * 36 6 6 

342 

*H. * *Wang, * *Q. * *Meng, * *S. * *Chen* *et* *al. * 

*Transportation* *Research* *Part* *B* *149* *\(2021\)* *322–346* 

**Table** **7** 

The computed results for Case III when *N* accel 

max = 4 

. 

Situation 

Optimal solution 

Optimal payoffs 

Computation time \(s\) 

Situation 1: 

X *, * 1 

*B* = ˜ 

X *B* 

8.625 

- 

C → A → B 

X *, * 1 

*A* = \{ 

1 *, * 1 *, * 1 *, * 1 *, * 1 *, * −1 *, * −1 *, * −1 *, * −1 *, * −1 *, * −1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 \} 

12.63325 

0.088 

X *, * 1 

*C* = \{ 

1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * −1 *, * −1 *, * −1 *, * 0 *, * −1 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 \} 

13.125 

0.092 

Total travel time of the three vehicles = 34.38325s. 

Situation 2: 

X *, * 2 

*A* = ˜ 

X *A* 

9.362291 

- 

C → B → A 

X *, * 2 

*B* = \{ 

0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * −1 *, * −1 *, * −1 *, * 0 *, * 0 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 \} 

13.3666 

0.089 

X *, * 2 

*C* = \{ 

0 *, * 0 *, * 1 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 1 *, * 1 *, * 1 *, * 1 \} 

17.3666 

0.094 

Total travel time of the three vehicles = 40.095492s. 

Situation 3: 

X *, * 3 

*A* = ˜ 

X *A* 

9.362291 

- 

B → C → A 

X *, * 3 

*C* = \{ 

1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 \} 

10.625 

0.093 

X *, * 3 

*B* = \{ 

0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * −1 *, * −1 *, * −1 *, * −1 *, * 0 *, * 0 *, * 0 *, * 0 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 \} 

14.63325 

0.088 

Total travel time of the three vehicles = 34.620541s. 

When Player B takes its dominate strategy, the average relative estimation error is 





1 | 12 4 

| 8 7 

*P* 

9 − 12 *. * 63325 | 

16 − 8 *. * 625 | 

error = 

\+ 

= 2 *. * 705% *. * 

2 

12 *. * 63325 

8 *. * 625 

The above analyses point out that it would be better to consider a more realistic driving scenario of constant acceleration to minimize estimation error of the travel time. 

*6.3.2. * *The* *computational* *efficiency* *of* *the* *proposed* *algorithm* *for* *3-player* *case* As shown in Table 7 ,  there are three possible navigation situations for the 3-player case. For each situation, the 3-player competitive game could be decomposed into two 2-player Nash games. It takes about 1.8h 1 *. * 8 h = 3 ×2 ×1080 s to find out 3600 

the optimal solution of the cooperative control strategies by using the enumeration method. The computation time of the proposed B&B method is between 0.273s and 0.544s, depending on the searching order of the situations. 

\(i\) If the searching process starts from Situation 1, we obtain the total travel time of 34.38325s. It is updated as the upper bound of the 3-player game. For Situation 2, the lower bound of the total travel time is 40.087s 

⎛ 

⎞ 

⎝ 40 *. * 087 = 9 *. * 362291 



\+

\+

⎠ . 

9 *. * 362291 \+ 4 *. * 0 



9 *. * 362291 \+ 4 *. * 0 \+ 4 *. * 0 Since it is greater than the renewed upper bound, Vehicle A 

Vehicle B 

Vehicle C 

there is no need to search the branches in Situation 2. The B&B searching moves to Situation 3. Once the 2-player game between Vehicle C and Vehicle A under Situation 3 is done, the lower bound of total travel time is determined as 34.612291s \(34.612291 = 9.362291\+10.625\+10.625\+4\). As the result, the other branches in Situation 3 is cut as its lower bound of total travel time is greater than the upper bound of 34.38325. Therefore, the computation time is about 0.273s \(0.273 = 0.088\+0.092\+0.093\). 

\(ii\) In a similar manner, when the searching process begins from Situation 3, there is no need to traverse the branches in Situation 2. The computation time is thus 0.361s \(0.361 = 0.093\+0.088\+0.088\+0.092\). 

\(iii\) The longest computation time is required when the B&B searching begins from Situation 2, followed Situation 3 and then Situation 1. In this search order, all three situations are fully proceeded with a total time of 0.544s. 

To sum up, the computation time of the B&B algorithm is far less than that of the enumeration method. We here recog-nize the fact that such computational efficiency in centisecond may not meet the requirement of a real-time V2V navigation at the unsignalized intersection. In addition, it will take longer time if more vehicles coexist in the intersection. However, in general, traffic at an unsignalized intersection should be relatively sparse; otherwise, some form of control should be implemented to guide the vehicles at this point. At the same time, the B&B algorithm should be further improved, probably by integrating with parallel computing techniques. 

*6.3.3. * *Comparison* *between* *the* *proposed* *control* *strategy* *and* *the* *first-come-first-served* *policy* In Case III, we also want to compare the vehicle control effect between our proposed navigation strategy and the first-come-first-served \(FCFS\) policy. As mentioned above, Vehicle A arrives first, followed Vehicle B and Vehicle C. As shown in 

Table 7 ,  once these vehicles follow the FCFS principle to pass the intersection \(Situation 2\), the total travel time is 40.0955s. 

It could be reduced to 34.38255s using our proposed strategy, about 14.25% of reduction. 

A more concrete comparison can be made by using the maximal throughput at the intersection. When the FCFS policy is implemented, in our example, three vehicles could pass the intersection after 17.366s. Therefore, the maximal throughput is 622 ≈ 3600 

17 *. * 366 × 3 . It becomes 823 ≈ 3600 

13 *. * 125 × 3 when our proposed strategy is adopted, indicating a more than 30% increase in the maximal throughput \( 32 *. * 23% = 823 −622 

622 \). 

343 

*H. * *Wang, * *Q. * *Meng, * *S. * *Chen* *et* *al. * 

*Transportation* *Research* *Part* *B* *149* *\(2021\)* *322–346* 

**Table** **8** 

The computed results for Case IV when *N* accel 

max = 4 at time *t* = 4 

. 

Situation 

Optimal solution 

Optimal payoffs 

Computation time \(s\) 





Situation 1: 

X *, * 1 



*B* *t*

=4 ⊂ X *, * 1 

*B* *t*

=0 = ˜ 

X *B* 

4.625 

- 

D → C → A → B 

X *, * 1 



*A* *t*

=4 ⊂ X *, * 1 

*A* *t*

=0 = \{ 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * −1 *, * −1 *, * −1 *, * −1 *, * −1 *, * −1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 \} 8.63325 

0.088 

X *, * 1 



*C* *t*

=4 ⊂ X *, * 1 

*C* *t*=0 = \{ 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * −1 *, * −1 *, * −1 *, * 0 *, * −1 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 \} 

9.125 

0.092 

X *, * 1 

*D* *t*=4 = \{−1 *, * −1 *, * −1 *, * −1 *, * −1 *, * 0 *, * 1 *, * 1 *, * 1 *, * 1 *, * −1 *, * −1 *, * −1 *, * −1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 \} 

13.1260 

0.094 

Vehicles A, B and C stick to the decisions made at *t* = 0 ; Total travel time of the four vehicles = 35.509s. 





Situation 2: 

X *, * 2 



*B* *t*

=4 ⊂ X *, * 2 

*B* *t*

=0 = ˜ 

X *B* 

4.625 

- 

C → D → A → B 

X *, * 2 



*A* *t*

=4 ⊂ X *, * 2 

*A* *t*=0 = \{ 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * −1 *, * −1 *, * −1 *, * −1 *, * −1 *, * −1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 \} 

8.63325 

0.088 

X *, * 2 

*D* *t*

=4 = \{−1 *, * −1 *, * −1 *, * −1 *, * −1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 0 *, * −1 *, * −1 *, * −1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 \} 

12.6334 

0.093 

X *, * 2 

*C* *t*=4 = \{−1 *, * −1 *, * −1 *, * −1 *, * −1 *, * −1 *, * −1 *, * −1 *, * 1 *, * 0 *, * 0 *, * 1 *, * 1 *, * 1 *, * 1 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 \} 

16.64286 

0.096 

Vehicles A and B stick to the decisions made at *t* = 0 ; Total travel time of the four vehicles = 42.535s. 





Situation 3: 

X *, * 3 



*B* *t*=4 ⊂ X *, * 3 

*B* *t*=0 = ˜ 

X *B* 

4.625 

- 

C → A → D → B 

X *, * 3 

*D* = \{ 

1 *, * 1 *, * 1 *, * 1 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 \} 

8.00 

0.091 

X *, * 3 

*A* = \{−1 

*, * 0 *, * −1 *, * −1 *, * −1 *, * −1 *, * −1 *, * −1 *, * −1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 *, * 1 \} 

12.099 

0.090 

X *, * 3 

*C* = \{ 

0 *, * 0 *, * 0 *, * −1 *, * −1 *, * −1 *, * −1 *, * −1 *, * −1 *, * 0 *, * 1 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 *, * 0 \} 

12.50 

0.093 

Vehicle B remains its decisions made at *t* = 0 ; Total travel time of the four vehicles = 37.224s. 

Situation 4: D → B → C → A, infeasible solution. 

Situation 5: D → C → B → A, infeasible solution. 

Situation 6: C → D → B → A, infeasible solution. 

Note: the payoffs for the vehicles and the total travel time are counted from *t* = 4 to the time passing the intersection. 

*6.4. * *Case* *IV* *for* *illustrating* *the* *rolling-horizon* *approach* In this section, we introduce how to implement a rolling-horizon control mechanism to accommodate traffic dynamics, such as new arriving vehicles at the intersection. On top of Case III, a new vehicle \(Vehicle D\) comes to the intersection at time *t* = 4 , following Vehicle B, with the initial speed *v* *D, * 0 = 12 m/s and *L* *D* = 120 m. 

Under this testing scenario, there are one 3-player game \(A, B and C\) at time *t* = 0 and one 4-player game \(A, B, C and D\) at time *t* = 4 over the time horizon. At time *t* = 0 , we have obtained the optimal navigation strategies for Case III. We now focus on solving the 4-player game, which depends on the historical decisions at *t* = 0 for Vehicles A, B and C.  Table 8 

summarizes the computed results for the 4-player case at time *t* = 4 . 

The searching process of the B&B algorithm starts from Situation 1 shown in Table 8 ,  as an optimal solution of *\(* X *, * 1 

*B* *, * X *, * 1 

*A* *, * X *, * 1 

*C* *\)* is provided at time *t* = 0 \(the optimal control strategies in Case III\). The computation time for the cooperative 4-player game model at time *t* = 4 is about 0.185s, even less than that for the 3-player case at time *t* = 0 . In the following, we briefly explore the reasons behind it and illustrate how B&B algorithm works. 

\(i\) Under Situation 1, Vehicles A, B and C stick to the decisions made at *t* = 0 ; i.e., there is no need to update their navigation policies. We only need to solve the MP model \(a 2-player game\) for Vehicle D by taking into account the updated system state of its leader \(Vehicle B\) from *t* = 4 onward and the minimal time to avoid collision with Vehicle C. The total travel time of the four vehicles from *t* = 4 onward is 35.509s, which is recorded as the upper bound of the 4-player game. 

\(ii\) As for Situation 2, Vehicles A and B continue with the navigation strategies suggested at *t* = 0 , and we determine the new strategies for Vehicles C and D at *t* = 4 . In this situation, the lower bound of the total travel time is 42 *. * 525 = 4 *. * 625 \+ 8 *. * 63325 \+ *\(* 8 *. * 63325 \+ 4 *\)* \+ *\(* 8 *. * 63325 \+ 4 \+ 4 *\)* , which is greater than the upper bound of 35.509. 

Therefore, Situation 2 is cut off in the B&B searching. 

\(iii\) For Situation 3, all the four vehicles except Vehicle B update their strategies at *t* = 4 . Once the optimal solution and payoff for Vehicle D are determined by solving the 2-player game between Vehicle D and Vehicle B, we get the lower bound of total travel time, 36 *. * 625 = 4 *. * 625 \+ 8 *. * 0 \+ *\(* 8 *. * 0 \+ 4 *\)* \+ *\(* 8 *. * 0 \+ 4 *\)* . The remaining branches under Situation 3 are also pruned. 

\(iv\) Situations 4–6 imply the leading vehicle will be replaced by Vehicle A at *t* = 4 . These situations are all infeasible for the following reason. Once Vehicle A becomes the leading vehicle, it takes its dominate strategy and the time to pass the intersection is 5.3623s at *t* = 4 . At the same time, the speed and remaining travel distance for Vehicle B are, respectively, 14m/s and 72m. Even Vehicle B takes the continuous deceleration strategy immediately, it only spends 6.789s to pass the conflict point at the intersection. In this case, the minimal time to avoid collision between Vehicles A and B cannot be guaranteed. Thus, all the branches under the three situations are infeasible solutions and are pruned directly. 

With above, we get the computation time for the 4-player game at *t* = 4 to be 0 *. * 185 s = 0 *. * 094 \+ 0 *. * 091 . The computation efficiency is much superior to the enumeration method \(its computation time is estimated to be longer than 3h even based on historical strategies obtained from the 3-player case at *t* = 0 \). It is worth clarifying that the computation time for a 4-player game is not always less than a 3-player game. The above findings indicate that, for a rolling-horizon CAV navigation mechanism, there are more effective cuts that could be applied to improve the computational efficiency of the B&B algorithm 344 

*H. * *Wang, * *Q. * *Meng, * *S. * *Chen* *et* *al. * 

*Transportation* *Research* *Part* *B* *149* *\(2021\)* *322–346* 

significantly. In addition, it demonstrates that the rolling-horizon approach could well incorporate the traffic dynamics into CAV navigation controlling at an unsignalized intersection based on our developed models and algorithms. 

At last, we also look at the difference of vehicle control effect between the FCFS strategy and our proposed strategy with the rolling-horizon decision mechanism. The FCFS principle is satisfied under Situation 4, where the total travel time of four vehicles to pass the intersection is 57.4622s and the last one, Vehicle D, passes the conflict point at time *t* = 21 *. * 36675 . The optimal total travel time obtained by the rolling-horizon approach is 47.509s and the last individual passes the intersection at time *t* = 17 *. * 126 . Compared to the FCFS strategy, our proposed vehicle navigation strategy could reduce the total travel time by 17.32% and increase the maximal throughput by 19.85%, from 674 vehs/h to 841 vehs/h, under Case IV. 

**7. ** **Conclusions** 

Owing to various advancements in technology, the future of CAVs becomes increasingly promising. In academic field, the way to implement signal-less traffic management has been paving gradually. In this paper, we first investigate the travel strategies of two CAVs for passing an unsignalised intersection from crossing directions by means of game theory. CAVs, as highly intelligent and automated entities, could act as independent individuals or behave in a cooperative manner. A Nash game model is formulated to capture the behaviour for competitive case, and a cooperative game model is used for cooperative case. We then extend the game models to analyze the n-player case where *n* ≥ 3 . Based on derived properties of the game models, we develop a tailored B&B algorithm to find solutions to the two games. 

The competitive model can be further interpreted as a Chicken game. Model solutions show that pure-strategy NEs always exist, and NE is achieved when at least one player is taking his dominant strategy. We also find that the optimal strategy under cooperative mechanism belongs to the NE solution set. These insights enable us to design efficient solution algorithms for the two game models and find respective travel strategies of CAVs. Due to computational accuracy and efficiency of the designed B&B algorithm, our models and algorithm can be readily incorporated into future real-time CAV 

decision system to help navigate through unsignalised intersections. 

Although the models are motivated by current practice/prospect in CAV transport system, there are some limitations that deserve further investigation. First, our paper considers an elemental system with two/three cross-moving CAVs, which simplifies the complicated situation in real world. On top of our extension from the single-stage problem to a rolling-horizon decision problem, it would be more interesting and practical to consider more control options \(acceleration/deceleration actions\), especially the option of emergency brake, so as to tackle possible external disturbance and/or occasional incidents near the intersection. Second, in our paper, a perfect and stable V2V communication is assumed, which does not experience any information package loss. Our model could be extended to take into account random interruptions in V2V communication at the unsignalised intersection. 

**Declaration** **of** **Competing** **Interest** 

There are no any conflicts of interest for this study. 

**CRediT** **authorship** **contribution** **statement** 

**Hua** **Wang:** Conceptualization, Funding acquisition, Investigation, Methodology, Writing - original draft, Writing – review 

& editing. **Qiang** **Meng:** Conceptualization, Methodology, Supervision, Writing - original draft, Writing – review & editing. 

**Shukai** **Chen:** Investigation, Methodology, Validation, Writing - original draft, Writing – review & editing. **Xiaoning** **Zhang:** Funding acquisition, Writing - original draft, Writing – review & editing. 

**Acknowledgments** 

We are indebted to the editors and our three anonymous referees for their thoughtful comments that have helped sub- 

stantially improve this work. This study has been substantially supported by the research grants from the National Natural 

Science Foundation of China \( 71601142 , 72021002 and 71890973 \). 

**References** 

Amirgholy, M. , Nourinejad, M. , Gao, H.O. , 2020. Optimal traffic control at smart intersections: automated network fundamental diagram. Transportation 

Research Part B 137, 2–18 . 

Androulakis, I.P. ,Maranas, C.D. ,Floudas, C.A. ,1995. *α* BB: A global optimization method for general constrained nonconvex problems. J. Global Optim. 7 \(4\), 

337–363 . 

Chen, R. ,Hu, J. ,Levin, M.W. ,Rey, D. ,2020. Stability-based analysis of autonomous intersection management with pedestrians. Transportation Research Part 

C 114, 463–483 . 

Chen, S. , Wang, H. , Meng, Q. , 2021. An optimal dynamic lane reversal and traffic control strategy for autonomous vehicles. IEEE Trans. Intell. Transp. Syst. 

DOI:10.1109/TITS.2021.3074011 . 

Chen, Z. ,He, F. ,Yin, Y. ,Du, Y. ,2017. Optimal design of autonomous vehicle zones in transportation networks. Transportation Research Part B 99, 44–61 . 

Dresner, K. ,Stone, P. ,2004. Multiagent traffic management: A reservation-based intersection control mechanism. In: Proceedings of the Third International 

Joint Conference on Autonomous Agents and Multiagent Systems-Volume 2, pp. 530–537 . 

345 

*H. * *Wang, * *Q. * *Meng, * *S. * *Chen* *et* *al. * 

*Transportation* *Research* *Part* *B* *149* *\(2021\)* *322–346* 

Du, L. , Han, L. , Li, X.-Y. , 2014. Distributed coordinated in-vehicle online routing using mixed-strategy congestion game. Transportation Research Part B 67, 

1–17 . 

Ghiasi, A. , Hussain, O. , Qian, Z.S. , Li, X. , 2017. A mixed traffic capacity analysis and lane management model for connected automated vehicles: a markov 

chain method. Transportation Research Part B 106, 266–292 . 

Guler, S.I. ,Menendez, M. ,Meier, L. ,2014. Using connected vehicle technology to improve the efficiency of intersections. Transportation Research Part C 46, 

121–131 . 

He, Q. , Head, K.L. , Ding, J. , 2012. Pamscod: platoon-based arterial multi-modal signal control with online data. Transportation Research Part C 20 \(1\), 

164–184 . 

Iimura, T. ,Murota, K. ,Tamura, A. ,2005. Discrete fixed point theorem reconsidered. Journal of Mathematical Economics 41 \(8\), 1030–1036 . 

Krishnamurthy, N.N. ,Batta, R. ,Karwan, M.H. ,1993. Developing conflict-free routes for automated guided vehicles. Oper. Res. 41 \(6\), 1077–1090 . 

Kröger, F. ,2016. Automated Driving in Its Social, Historical and Cultural Contexts. In: Autonomous Driving. Springer, pp. 41–68 . 

Lee, J. ,Park, B. ,2012. Development and evaluation of a cooperative vehicle intersection control algorithm under the connected vehicles environment. IEEE 

Trans. Intell. Transp. Syst. 13 \(1\), 81–90 . 

Levin, M.W. ,Boyles, S.D. ,Patel, R. ,2016. Paradoxes of reservation-based intersection controls in traffic networks. Transportation Research Part A 90, 14–25 . 

Levin, M.W. ,Fritz, H. ,Boyles, S.D. ,2016. On optimizing reservation-based intersection controls. IEEE Trans. Intell. Transp. Syst. 18 \(3\), 505–515 . 

Levin, M.W. ,Rey, D. ,2017. Conflict-point formulation of intersection control for autonomous vehicles. Transportation Research Part C 85, 528–547 . 

Li, P. , Zhou, X. , 2017. Recasting and optimizing intersection automation as a connected-and-automated-vehicle \(CAV\) scheduling problem: a sequential 

branch-and-bound search approach in phase-time-traffic hypernetwork. Transportation Research Part B 105, 479–506 . 

Li, Z. , Elefteriadou, L. , Ranka, S. , 2014. Signal control optimization for automated vehicles at isolated signalized intersections. Transportation Research Part 

C 49, 1–18 . 

Luo, Y. , Xiang, Y. , Cao, K. , Li, K. , 2016. A dynamic automated lane change maneuver based on vehicle-to-vehicle communication. Transportation Research 

Part C 62, 87–102 . 

Ma, J. , Li, X. , Zhou, F. , Hu, J. , Park, B.B. , 2017. Parsimonious shooting heuristic for trajectory design of connected automated traffic part II: computational 

issues and optimization. Transportation Research Part B 95, 421–441 . 

Mallick, I. ,2011. On the existence of pure strategy nash equilibria in two person discrete games. Econ. Lett. 111 \(2\), 144–146 . 

Nash, J. ,1951. Non-cooperative games. The Annals of Mathematics 54 \(2\), 286–295 . 

Navlab: The Carnegie Mellon University Navigation Laboratory ,2014. Carnegie Mellon. Technical Report. The Robotics Institute .Retrieved 2014-12-20 

Olia, A. ,Abdelgawad, H. ,Abdulhai, B. ,Razavi, S.N. ,2017. Optimizing the number and locations of freeway roadside equipment units for travel time estima- 

tion in a connected vehicle environment. Journal of Intelligent Transportation Systems 21 \(4\), 296–309 . 

Qu, X., Li, X., Wang, M., Dixit, V., 2017. Advances in modelling connected and automated vehicles. Journal of Advanced Transportation vol. 2017. doi: 10.1155/ 

2017/3268371 . 

Rey, D. ,Levin, M.W. ,2019. Blue phase: optimal network traffic control for legacy and autonomous vehicles. Transportation Research Part B 130, 105–129 . 

Thonemann, U.W. , Brandeau, M.L. , 1996. Designing a single-vehicle automated guided vehicle system with multiple load capacity. Transportation Science 

30 \(4\), 351–363 . 

Wang, M. , Daamen, W. , Hoogendoorn, S.P. , van Arem, B. , 2014. Rolling horizon control framework for driver assistance systems. part i: mathematical for- 

mulation and non-cooperative systems. Transportation Research Part C 40, 271–289 . 

Wang, M. ,Daamen, W. ,Hoogendoorn, S.P. ,van Arem, B. ,2014. Rolling horizon control framework for driver assistance systems. part II: cooperative sensing 

and cooperative control. Transportation Research Part C 40, 290–311 . 

Wang, M. ,Hoogendoorn, S.P. ,Daamen, W. ,van Arem, B. ,Happee, R. ,2015. Game theoretic approach for predictive lane-changing and car-following control. 

Transportation Research Part C 58, 73–92 . 

Wu, Y. ,Chen, H. ,Zhu, F. ,2019. DCL-AIM: Decentralized coordination learning of autonomous intersection management for connected and automated vehi- 

cles. Transportation Research Part C 103, 246–260 . 

Xie, Y. ,Gartner, N.H. ,Chowdhury, M. ,2017. Editors’ Notes: special issue on connected and autonomous vehicles. Transportation Research Part C 78, 34–36 . 

Yang, C.Y.D. ,Ozbay, K. ,Ban, X.J. ,2017. Developments in connected and automated vehicles. Journal of Intelligent Transportation Systems 21 \(4\), 251–254 . 

Yang, D. ,Zheng, S. ,Wen, C. ,Jin, P.J. ,Ran, B. ,2018. A dynamic lane-changing trajectory planning model for automated vehicles. Transportation Research Part 

C 95, 228–247 . 

Yang, K. , Guler, S.I. , Menendez, M. , 2016. Isolated intersection control for various levels of vehicle technology: conventional, connected, and automated 

vehicles. Transportation Research Part C 72, 109–129 . 

Yang, Z. ,Huang, H. ,Yao, D. ,Zhang, Y. ,2016. Cooperative driving model for non-signalized intersections based on reduplicate dynamic game. In: 2016 IEEE 

19th International Conference on Intelligent Transportation Systems \(ITSC\), pp. 1366–1371 . 

Yu, C. ,Feng, Y. ,Liu, H.X. ,Ma, W. ,Yang, X. ,2018. Integrated optimization of traffic signals and vehicle trajectories at isolated urban intersections. Transporta- 

tion Research Part B 112, 89–112 . 

Yu, C. , Sun, W. , Liu, H.X. , Yang, X. , 2019. Managing connected and automated vehicles at isolated intersections: from reservation-to optimization-based 

methods. Transportation Research Part B 122, 416–435 . 

Zhou, F. ,Li, X. ,Ma, J. ,2017. Parsimonious shooting heuristic for trajectory design of connected automated traffic part i: theoretical analysis with generalized 

time geography. Transportation Research Part B 95, 394–420 . 

Zhu, F. , Ukkusuri, S.V. , 2015. A linear programming formulation for autonomous intersection control within a dynamic traffic assignment and connected 

vehicle environment. Transportation Research Part C 55, 363–378 . 

346 


# Document Outline

+ Competitive and cooperative behaviour analysis of connected and autonomous vehicles across unsignalised intersections: A game-theoretic approach  
	+ 1 Introduction 
	+ 2 Literature review 
	+ 3 Problem description 
	+ 4 V2V Control strategies: Competitive and cooperative mechanisms  
		+ 4.1 The game model for competitive control mechanism 
		+ 4.2 The game model for cooperative control mechanism 
		+ 4.3 Extension to the n-player case 

	+ 5 Solution algorithm 
	+ 6 Numerical examples  
		+ 6.1 Case I for assessing the consistency between theoretical and numerical results 
		+ 6.2 Case II for assessing the computational efficiency of the developed algorithm  
			+ 6.2.1 Experiments when player B takes his dominant strategy 
			+ 6.2.2 Sensitivity analysis of on computational efficiency 

		+ 6.3 Case III for illustrating the 3-player games  
			+ 6.3.1 The effect of relaxing Assumption 1 to use constant acceleration 
			+ 6.3.2 The computational efficiency of the proposed algorithm for 3-player case 
			+ 6.3.3 Comparison between the proposed control strategy and the first-come-first-served policy 

		+ 6.4 Case IV for illustrating the rolling-horizon approach 

	+ 7 Conclusions 
	+ Declaration of Competing Interest 
	+ CRediT authorship contribution statement 
	+ Acknowledgments 
	+ References



