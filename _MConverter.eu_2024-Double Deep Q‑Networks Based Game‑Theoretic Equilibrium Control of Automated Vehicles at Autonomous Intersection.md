Automotive Innovation \(2024\) 7:571–587 

https://doi.org/10.1007/s42154-023-00281-w

**Double Deep Q‑Networks Based Game‑Theoretic Equilibrium Control** **of Automated Vehicles at Autonomous Intersection**

**Haiyang Hu1 · Duanfeng Chu1 · Jianhua Yin1,3 · Liping L****u2**

Received: 30 May 2023 / Accepted: 12 December 2023 / Published online: 19 November 2024 

© China Society of Automotive Engineers \(China SAE\) 2024

**Abstract**

Optimizing the efficiency of traffic flow while minimizing fuel consumption is of significant importance in the context of resource scarcity and environmental preservation. Currently, the two-layer optimization strategy has been employed in autonomous intersection cooperation problems. The traffic efficiency is optimized on the first layer and energy consumption is optimized on the second layer based on an optimal timetable gained in the first layer. This operation prioritizes traffic efficiency over energy consumption, which may present a limitation in terms of equilibrating them. This paper develops an equilibrium control strategy for autonomous intersection. This control strategy includes vehicle schedule and equilibrium control. A schedule algorithm is initially proposed for platoons, in which the most passing sequence is gained when considering platoon formation. Then, a game deep reinforcement learning model is designed, and an equilibrating control algorithm is proposed, in which equilibrium state can be gained between traffic efficiency and energy consumption. Simulation results demonstrate that the proposed method can equilibrate traffic efficiency and energy consumption to an equilibrium state, as well as reducing trip cost compared with existing methods. 

**Keywords** Automated vehicle · Game theory · Deep reinforcement learning · Platoon formation schedule · Equilibrium control

**Abbreviations**

**1 Introduction**

DDQN Double deep q-networks

DRL 

Deep reinforcement learning

The intersection is a crucial element in the field of traffic EDF 

Earliest deadline first

safety and efficiency. It is seen as a manager to solve vehicle FCFS First come and first served

collisions for conflicting traffic flows. However, due to the FIFO 

First in and first out

traffic congestion, the intersection is seen as a bottleneck MILP Mixed-integer linear program

more often in urban roads. Researchers estimate that con-MPC 

Model predictive control

gestion caused urban people to travel an extra 8.8 billion NLP 

Non-linear programming

hours \[1\]. Meanwhile, petroleum and natural gas remain the PPO 

Proximal policy optimization

most-consumed sources of energy in 2050, with the largest QMIX Monotonic value function factorisation for deep consumption of petroleum in transportation \[2\]. Efficient multi-agent reinforcement learning

intersection management can relieve traffic congestion and SAC 

Soft actor critic

improve energy savings. Along with the development of economy, intelligent vehicle technologies and communication technologies are becoming increasingly prevalent, such as self-driving technology, vehicle-to-infrastructure, 

\* Jianhua Yin 

yinjh@whut.edu.cn

and vehicle-to-vehicle communication. These technologies provide more opportunities for intersection management to 1 Intelligent Transportation Systems Research Center, Wuhan improve transportation efficiency further \[3\]. Autonomous University of Technology, Wuhan 430070, China

intersection management has attracted a lot of attention as 2 The School of Computer Science and Artificial Intelligence, it has the potential to eliminate the loss of green time and Wuhan University of Technology, Wuhan 430070, China

inefficiency for schedules \[4\]. 

3 Chongqing Research Institute, Wuhan University 

of Technology, Chongqing, China

Vol.:\(0123456789\)

572



H. Hu et al. 

**1.1 Related Work and Motivation**

introducing some tricks, including the eligibility traces and reward clipping. Then, they trained the improved In an autonomous intersection scenario, vehicles will not QMIX model to solve multiple vehicles passing prob-be prompted to pass by a traffic signal, so how to coordi-lem. The number of vehicles is limited in model. To make nate vehicles efficiently is an important optimization prob-autonomous intersection management systems adapt to 

lem. The two-layer optimization strategy decomposes the complex traffic scenarios, Antonio et al. \[12\] constructed problem into two separate problems: The first problem is an end-to-end multi-agent reinforcement learning model. 

to determine the optimal passing timetable, and the second The above methods focus on single vehicle schedule 

is to plan the vehicle speed trajectory according to this and do not consider the platoon schedule. Lioris et al. \[14\] 

timetable. 

assessed the potential mobility benefits of the platoon ena-To gain optimal passing time for each vehicle, previbled by connected vehicle technology and found that inter-ous research has proposed some heuristic strategies, such section capacity can be doubled or tripled based on the pla-as First Come and First Served \(FCFS\), First in and First toon. Li et al. \[15\] designed a hierarchical reinforcement out \(FIFO\), priority strategy, auction strategy, and batch learning control model to optimize the size and order of the strategy. All vehicles are processed by these fixed rules, platoons, respectively. This research does not consider the thereby the operations cannot adapt to varying traffic con-platoon formation in the platoon schedule process. Deng ditions. Some research proposed optimization strategies to et al. \[16\] designed a traffic schedule model to coordinate improve intersection performance further. Choi et al. \[5\] 

platoons and introduced platoon formation decision vari-designed a reservation-based optimal scheduling method. 

ables in it. Similar research can be found in the Ref. \[17\]. 

The reservation was formulated as an optimization prob-According to the above research, platoon formation need to lem to find the optimal passing sequence of vehicles, be considered in the schedule modeling process to improve which outperformed FCFS strategy. Yu et al. \[6\] adopted traffic efficiency further. The above platoon coordination queueing theory for the theoretical analyses of the reserva-models with numerous constraints and decision variables tion-based control method and introduced the batch strat-are complicated and difficult to be solved. The application egy to construct an optimization model with the goal of may be restricted in some simple scenarios \[16\]. Therefore, optimizing the passing sequence of vehicles. Under vary-model complexity needs to be considered to reduce compu-ing traffic conditions, the model can produce optimal batch tation resource. 

sizes. Cai et al. \[4\] proposed a two-dimensional distribu-After determining the crossing timetable, the vehicle tion calculation method to address the multi-lane unsig-speed trajectory need to be planned. Researchers proposed nalized intersection cooperation problem. Research on various piecewise trajectory planning methods \[18–20\], in Multi-lane unsignalized intersection cooperation can also which the speed trajectory is adjusted in some segments. 

be found in literature \[7\]. To rationally allocate network Other researchers transformed the trajectory planning prob-resources, Wang et al. \[8\] employed the greedy algorithm lems into the optimal control problems \[9, 21–25\]. Based on to optimize the sequence for route planning in network. 

the infinitesimal method, Yao et al. \[9\] proposed a non-linear According to this work, optimal passing sequence of vehi-programming \(NLP\) model to optimize vehicle trajectory cles is extended to the network level. Yao et al. \[9\] pro-for energy consumption. To reduce computational load and posed a mixed-integer linear program \(MILP\) for vehicles model solving difficulty, they also construct a linear trajec-entering scheduling with the big M method. Based on the tory planning model to reduce fuel consumption \[21\] based rolling optimization strategy, the model can be solved in on optimal control theory and linear optimization. Based 1 s on a general laptop computer. Wang et al. \[10\] designed 

on the transient engine operation model, Hadjigeorgiou a convex vehicle schedule model based on negotiation et al. \[25\] employed piecewise affine functions and convex-game theory, which can be solved in the distributed form. 

concave procedure to approximate the proposed trade-off The proposed model not only determined vehicle passing model about fuel consumption and travel time, respectively. 

order but also optimized longitudinal trajectory. 

Subsequently, they gained convex combination relation-Some researchers exploited the application of deep rein-ship between traffic efficiency and energy consumption by forcement learning in vehicle schedule problem \[11–13\]. 

directly setting different weight coefficient about travel time. 

Spatharis et al. \[11\] proposed a multi-agent deep rein-This strategy does not solve the vehicle schedule problem, forcement learning method for multi-intersection scenar-that is, the travel time optimality is not be guaranteed. Deep ios, which can navigate vehicles to their destinations and reinforcement learning and game theory are also exploited to guarantee safety and efficiency. Guo et al. \[13\] improved solve the trajectory planning problem \[10, 26–28\]. Nan et al. 

QMIX \(Monotonic Value Function Factorisation for Deep 

\[29\] proposed a three-stage decision-making framework Multi-Agent Reinforcement Learning\) algorithm through for ego vehicles in the autonomous intersection, including target vehicle’s motion prediction, driving mode decision, 



Double Deep Q‑Networks Based Game‑Theoretic Equilibrium Control of Automated Vehicles at…

573

and motion planning. In the first stage, the target vehicle's driving intention and trajectory are predicted. In the second North

stage, the S-T diagram is used to judge whether the target vehicle and the ego vehicle will collide. If collision exists, Controller

the driving decision-making is made by the Mixed Strategy Platoon

Platoon group

Conflict 

Nash Equilibrium method. In the third stage, based on the zone

driving decision-making, MPC algorithm \(Model Predictive Control\) is used to calculate the optimal acceleration. The Free flow zone

Schedule and game zone

decision-making framework guarantees driving safety and **CAV**

comfort. 

The above research focuses on single vehicle trajectory planning and do not consider the platoon. Han et al. \[30\] 

**Fig. 1 **Studied scenario

proposed to introduce gap feedback control to guarantee that following vehicles track leading vehicle's speed trajectory. 

Deep reinforcement

The tracking performance of the gap feedback control strat-Equilibrium 

learning

Equilibrium 

egy outperforms car following model, because it can reduce state 2

state 1

Varying traffic demand

unnecessary deceleration and acceleration. Feng et al. \[31\] 

proposed the introduction of a deep reinforcement model to Game 2

Game 1

track the leading vehicle's speed trajectory and the design of a gradient reward function to improve the convergence **Fig. 2 **Equilibrium state

performance of the trained model. According to the above research, the research gaps can be concluded that:

ent traffic conditions on the equilibrium states is a black box problem. 

• Currently, platoon trajectory planning research does not consider the equilibrium state between traffic efficiency **1.3 Organization**

and energy consumption, because the crossing timetable has been determined by the upper schedule. This opera-The rest of this paper is organized as follows. Section 2 

tion considers traffic efficiency with higher priority than defines an equilibrium control problem. Sections 3 and 4 

energy consumption. 

present the platoon scheduling method and the equilibrium 

• Although Hadjigeorgiou et al. \[25\] solved the equilibrium control method, respectively. Section 5 conducts some simu-problem, they did not solve the influence of different traf-lation tests, and Sect. 6 gives a conclusion for this paper. 

fic condition \(i.e., different traffic demand\) on the equilibrium state. On the other hand, the platoon schedule problem is not solved in this research. 

**2 Problem Statement**

To state the problem, an autonomous intersection is consid-1.2 Contribution

ered as the studied scenario, as show in Fig. 1. In this paper, the equilibrium problem between traffic efficiency and fuel To fill the above research gaps, this paper proposes a double consumption needs to be solved. 

deep q-Networks based game-theoretic equilibrium control The above problem can be transformed into a game prob-method. The contributions are summarized as follows: lem and formulate it as

• A platoon scheduling model is proposed that consid-max ∶ \[Θ\( ***u***\) × J\( ***u***\)\]

ers platoon formation on the scheduling process. This s.t. schedule operation, deep reinforement learning operation model is proven mathematically, and more importantly, \(1\)

it is easy to solve without employing other optimization where Θ is the traffic efficiency payoff, J is the fuel con-solvers. 

sumption payoff, and ***u*** is the control input. Game theory 

• An equilibrium control method is proposed based on maximizes each payoff by Nash equilibrium solution, so the game theory and deep reinforcement learning to equili-equilibrium state can be gained by Nash equilibrium solu-brate traffic efficiency and fuel consumption. Deep rein-tion. As shown in Fig. 2, there are two equilibrium states, forcement learning plays an important role to judge the and deep reinforcement learning can help the game find the equilibrium states under different traffic conditions \(i.e., equilibrium state under fixed and varying traffic condition different traffic demand\), because the influence of differ-

\(i.e., different traffic demand\), which is a black box problem. 





574



H. Hu et al. 

*h* min

Platoon group: platoon-a and platoon-b

a-2 a-1

Platoon-a

Stop 

Platoon-b

bar

Free flow zone

b-3

b-2 b-1

**Fig. 4 **Platoon state and platoon group state *p* , and *s*�=1 . Platoon-b does not achieve formation, because the vehicle b-3 does not catch up with the vehicle b-2, so its state is *̃p* and *s*� = 1. 

Based on Eq. \(2\), the platoon group can be denoted as

�

�

⎧ *G*\( *p*\) = *p*\( *s*\)� *p *\( *s*\), *n *≤ 2

⎪

*n*

�

�

**Fig. 3 **Overview of equilibrium control

⎨ *̃G*\( *p*\) = *̃p*\( *s*\)� *̃p *\( *s*\), *n *≤ 2

*n*

\(3\)

⎪

�

�

⎩ *̃G*\( *p*\) = *p*\( *s*\), *̃p*\( *s*\) These equilibrium states will be elaborated in subsequent where *̃*

sections. 

*G* represents the mixed state, which includes compact state and slack state of platoons. For example, from Fig. 4, 

An equilibrium control framework is proposed as shown it can be seen that a platoon group include two platoons, in Fig. 3, which consists of two parts: platoon scheduling platoon-a’s state is 

and equilibrating control. Platoon scheduling is divided into *p* , and platoon-b’s state *̃p* . Therefore, the platoon identification and cooperative schedule. Vehicles are state of platoon group is mixed state *̃G* . If all the platoons’ 

identified as potential platoons, and then the identified pla-states are compact state *p* in a platoon group, this group’s toons are optimally scheduled, which acquires updated infor-state is compact state *G* . If all the platoon’s states are slack mation about location and speed from approaching vehicles. 

state *̃p* in a platoon group, this group’s state is slack state *̃G* . 

Based on the optimal schedule sequence, equilibrium control On the other hand, as shown in Fig. 1, all the platoons in a is conducted in cooperative games, and cooperative opera-group can cross conflict zone simultaneously with different tion is conducted by trained double deep q-learning model. 

directions, so the number of platoons is 2 at most. Group set The control framework is conducted in real time. 

can be denoted as

⎧

�

�

⎪ Γ\( *G*\) = *G*\( *p*\)� *G *\( *p*\), *n *∈

*n*

**ℕ**\+

**3 Optimal Schedule of Vehicle Passing **

⎪

�

�

**Sequence**

⎨ *̃* Γ\( *G*\) = *̃G*\( *p*\)� *̃G *\( *p*\), *n *∈

*n*

**ℕ**\+

\(4\)

⎪

�

�

⎪ *̃* Γ\( *G*\) = *̃G*\( *p*\)� *̃G *\( *p*\), *n *∈

*n*

**ℕ**\+

In this section, a platoon schedule algorithm is proposed to ⎩

gain the optimal vehicle schedule. 

Noted that a platoon group set includes all the platoons Incoming vehicles in the free flow zone will be identi-in schedule and game zone, and there is only one group set fied as platoons in each lane. Combined with their status, in defined studied scenario. For simplicity, platoon, platoon platoons can be denoted as

group and platoon group set are denoted as *p*\( *s*\) , *G*\( *p*\) and 

\{

Γ\( *G*\) , respectively, in the following sections if its state is not *p s*� = *s *− 1

\(2\)

explicitly illustrated. 

*̃p s*� *< s *− 1

The affinity propagation clustering \(AP\) method is introduced to identify potential platoons 

where 

*p*\( *s*\) based on the current 

*p* represents the compact state, which means the pla-speed and location information of vehicles. The length of free toon can achieve formation before arriving at the intersec-flow zone is 200 m. AP method is an unsupervised learning tion, *̃p* represents the slack state, which means the platoon method and more details can be found in the Ref. \[32\]. On 

cannot achieve formation when arriving at the intersection, the other hand, the platoon identification is conducted over *s* is the maximum platoon size, and *s*′ is the number of vehi-the planning horizon \[

\+ \(Δ

\+ Δ

\+

cles that can catch up with the leading vehicle. To make it *t *, *t*

*T*

*T*

...\)\] to continu-

0

0

1

2

ally process newly arriving vehicles. Several potential platoons easier to understand Eq. \(2\), an example in Fig. 4 is given. 

are identified by the AP method in the free flow zone, and only In Fig. 4, the platoon-a achieves formation, because the the first platoon in each lane is adopted for scheduling. The headway between a-2 and a-1 is minimum, so its state is 

Double Deep Q‑Networks Based Game‑Theoretic Equilibrium Control of Automated Vehicles at…

575

unserved vehicles and newly arriving vehicles are identified intersection, *T *− *T* l is the delay time of the leading vehi-again when the served platoons discharge from the free flow b

arr

cle, and *F* is the delay time difference. In fact, *F* means the zone. Δ *T* is varying because of the platoons’ size and speed. 

rate of the platoon forming process, so the smaller value of Jackson \[33\] showed that the optimal solution for the *F* is, the slower the forming speed of platoon is. *T *− *T* l *< * 0 

job-shop scheduling problem can be gained by scheduling b

arr

means that the leading vehicle fails to arrive at intersection jobs in non-decreasing order of their deadline, based on the on time. 

Earliest Deadline First principle \(EDF\). Inspired by their According to Eqs. \(6\) and \(7\), the judgment function research, the scheduling platoon groups problem can be can also be written as transformed into a job-shop scheduling problem, and the EDF principle can be used to search for optimal passing *F *= *F*\( *T *, *s*�\), s.t. *s*� ≤ *s *− 1

b

\(8\)

sequence. The platoon group *G*\( *p*\) can be described as a job, so job-shop scheduling is to calculate 

Equation \(8\) can judge whether each following vehicle *G*\( *p*\) passing sequence. 

The deadline can be denoted as 

can catch up the leading vehicle for the given *T * . Noted *D* , and optimal sequence can 

b

be denoted as

that *T * needs to be updated when a platoon passes the con-b

flict zone, and updated is used to evaluate whether the 

\{

\}

*T* b

*𝛿 *= *D*|∀ *D *≥ *D*

, *n *∈

next platoon can achieve formation. Therefore, the pass-n

*n*\+1

**ℕ**\+

\(5\)

ing time of each platoon is important for the platoon state How to define and calculate the deadline of each group judgment and evaluated by is important in this problem. To address this problem, state judgment for the platoon needs to be discussed. If all the *d *∕\(\( *v *\+ *v *\)∕2\) cz

min

max

\(9\)

potential platoons form compact platoons to pass the inter-

\(

\)

where *v *\+ *v*

∕2 is the average speed of the leading 

section, intersection space can be utilized fully. In general, min

max

vehicle and the following vehicle, and *d * is the conflict to avoid collision, all the vehicles need to adjust crossing cz

zone distance. In fact, the passing speed is unavailable at intersection time through adjusting the speed. Following the schedule stage. 

vehicles in a platoon catch up with the leading vehicle only To reduce the time loss and utilize intersection space when the leading vehicle delays the crossing time through resources fully, the deadline of each group is defined under adjust its speed, such as slowing down, slowing down and different states, which considers the platoon formation. 

then speeding up. Moreover, the leading vehicle delays the crossing intersection time only when the delay time exists. 

**Definition 1** If state of *G*\( *p*\) is compact state *G* , for given The passing sequence of each platoon can affect its delay parameters *T * and *s*,the deadline is time, so the delay time should be large enough to make sure b

\{

\}

that each platoon forms the compact platoon. For example, *D *= min *F *\( *T *, *s *− 1\), *F *\( *T *, *s *− 1\) 1

b

1

2

b

2

\(10\)

if a platoon needs large delay time to form the platoon, the platoon should pass the conflict zone late. The minimum To illustrate the Definition 1 further, an example in delay time for platoon formation can be calculated by Fig. 5 is given. In Fig. 5, there are time axis *t* and distance axis *d* . *d * , *d * and *d * are arriving positions for each vehicle. 

1

2

3

f

*T*

= *T * s - 1 − *T* l − *h*

× \( *s *− 1\)

The platoon 1 completes formation earlier than platoon 2, d-min

arr

arr

min

\(6\)

because the vehicle 1-2 catches up with its leading vehicle where 

f

*T*

is the minimum delay time, *T * s-1 is the arrival d-min

arr

earlier than the vehicle 2-3 under the same *T * and free flow time of the last following vehicle at free speed, 

b

*T* l is the 

arr

speed. According to Eq. \(7\), *F*

can be obtained, so 

arrival time of the leading vehicle, and 

2 *< F* 1

*h*

is the minimum 

min

the deadline mainly depends on the formation of platoon headway. 

2. Noted that leading vehicles 1-1 and 1-2 will adjust the According to Eq. \(6\), it is easy to imagine that if the last crossing intersection time through adjusting the speed following vehicle can catch up with the leading vehicle, when entering the schedule and game zone. 

other following vehicles can also catch up with it. In fact, whether the platoon formation process can be achieved or not mainly depends on the delay time allocated for the leading vehicle. State judgment function can be formulated as

\{

*d* 3

*d* 2

*d* 1

≥

*d*

0 ∶ *p*

=0

*F *= *T *− *T* l − *T*

1-2 1-1 Stop

b

arr

\(7\)

d - min

*< * 0 ∶ *̃p*

2-3 2-2 2-1

bar

Free flow zone

*h* min

*t*= *T* b

where *T * is passing beginning time, which is related to b

the passing time of the groups that have been passed **Fig. 5 **An example about Definition 1

576



H. Hu et al. 

*d* 1

*d* 2

*d*

Based on the above definition, the following theorem and 

=0

2-2

2

Stop

proof are presented, respectively. 

1-3

1

bar

Free flow zone

*t*= *T* b

**Theorem 1** * 𝛿 * is an optimal schedule sequence in minimizing the travel delay for * * Γ\( *G *\). 

*n*≥2

**Fig. 6 **An example about situation 1

***Proof*** The time loss function is defined as follow. 

�

*d* 1

*d* 2

if *x *− *y *≤ 0 ∶ *z *= 0

*d*=0

⟨ *x *− *y*⟩ =

\(13\)

1

Stop

else : *z *= *x *− *y*

bar

2

*T* map

*t=T* b

where *x* and *y* represent periods. ⟨⋅⟩ is to calculate time loss, and *x *− *y *≤ 0 means time loss is 0. 

**Fig. 7 **An example about situation 2

According to Eq. \(8\) and deadline definitions, *D* is the **Definition 2** If state of 

delay time difference which is redeeming the delay time *G*\( *p*\) is slack state *̃G* or mixed state *̃G* , the deadline needs to be discussed by following situations: required for completing the platoon formation. In fact, *D* is Situation 1: If platoon size 

also a time loss when *D *≤ 0 , but *D *≥ 0 means that the pla-s ≥ *s * and current platoon 

1

2

position 

toon formation is achieved and the time loss does not exist. 

*d *≥ *d * in *G*\( *p*\) , for given parameters *T * and *s* , the 1

2

b

deadline is

It will be proved in three different cases. ∀ *D * is selected in *n*

the deadline set *𝛿* and have *D *≥ *D * . The authors denote *a*

*a*\+1

*D *= *F *\( *T *, *s *− 1\)

the ideal passing time of \(

\(

and 

, 

1

b

1

\(11\)

*G p*\) and *G*

*p*\) as *t* ideal

*t* ideal

*a*

*a*\+1

*a*

*a*\+1

respectively, while this paper denotes the current timestamp Platoon position *d* is the distance from location of the as *t*. 

last following vehicle to the stop bar. In Fig. 6,  *d *≥ *d * and 1

2

*s *≥ *s * means that the formation condition of platoon 1 

1

2

**Case 1** *D*

is only considered, even though the formation of platoon *a < * 0 and *Da*\+1 *< * 0 are assumed, and the optimal departure time of *G *\( *p*\) and *G *\( *p*\) are gained by Eqs. \(14\) 2 does not achieve, so the value of 

*a*

*a*\+1

*F * is selected as the 

1

and \(15\), respectively, 

deadline. 

Situation 2: If platoon size *s*

and current platoon 

=

\+

\+

| |

1 *< s* 2

*t*

*t*

*t* ideal

*a*

| *Da*|

position 

*⏟⏟⏟*

*a*

*d*

in *G*\( *p*\) , for given parameters *T * and *s* the 

*⏟⏟⏟*

\(14\)

1 *> d* 2

b

deadline is

timestamp

time loss

and

*D *= *F *\( *T *, *s *− 1\) − *T* map 2

b

2

d - min

⟨

⟩

f

f

\(12\)

*t*

= *t *\+ *t* ideal \+

| *D *| \+ *t* ideal \+ | *D *| − \( *t* ideal \+ | *D *|\)

= *F *\( *T *, *s *− 1\) − \( *T * s1−1 − *T * s2−1 \) *a*\+1

*a*

*a*

*a*\+1

*a*\+1

*a*

*a*

2

b

2

arr

arr

*⏟⏞⏞⏞⏞⏞⏞⏞⏞⏞⏟⏞⏞⏞⏞⏞⏞⏞⏞⏞⏟*

*⏟⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏟⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏟*

where f

timestamp

time loss

*T * s1−1 is the arrival time of the last following vehicle arr

\(15\)

in 

f

*p *\( *s*\) , and *T * s2−1 is the arrival time of the last following 1

arr

where || *D *|| is the absolute value of *D * . In addition, it is vehicle in 

f

f

*a*

*a*

*p *\( *s*\) . The term *T * s1−1 − *T * s2−1 is the time difference 2

arr

arr

assumed that *G *\( *p*\) pass the conflict zone before *G *\( *p*\) , so by which the last following vehicle in 

*a*\+1

*a*

*p *\( *s*\) takes to catch up 

1

with the last following vehicle in 

|

*p *\( *s*\) in map direction 

*t*�

=

*t*

\+

*t* ideal \+ |

2

*a*\+1

*a*\+1

| *Da*\+1|

before the last following vehicle in 

*⏟⏟⏟*

*⏟⏟⏟*

\(16\)

*p *\( *s*\) enters conflict zone, 

2

timestamp

as shown in Fig. 7. Extra delay 

time loss

*T* map needs to be add to *D*. 

d - min

and

***Remark 1*** *D* is defined as the deadline, but it is not the 

⟨

⟩

timestamp. The larger 

=

\+ |

| \+

\+

| | − \(

\+ |

|\)

*D* is, the earlier *G*\( *p*\) completes the *t*�

*t *\+ *t* ideal

*D*

*t* ideal

*D*

*t* ideal

*D*

*a*

*a*\+1

*a*\+1

*a*

*a*

*a*\+1

*a*\+1

platoon formation, so 

*⏟⏞⏞⏞⏞⏞⏞⏞⏞⏟⏞⏞⏞⏞⏞⏞⏞⏞⏟*

*⏟⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏟⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏟*

*𝛿* denotes a sequence in which the 

timestamp

time loss

platoon formation is completed. Noted that *𝛿* is a decrease \(17\)

sequence about the value of *D* , but the decrease sequence is meaningless. 

Double Deep Q‑Networks Based Game‑Theoretic Equilibrium Control of Automated Vehicles at…

577

Noted that

⟨

⟩

*t*

− *t*� = | *D *| \+ | *D*

| − \( *t* ideal \+ | *D *|\) −| *D *|

*a*\+1

*a*

*a*

*a*\+1

*a*

*a*

*a*\+1

*⏟⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏟⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏟*

time loss

⟨

⟩

−

| *D *| − \( *t* ideal \+ | *D *|\)

*a*

*a*\+1

*a*\+1

*⏟⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏟⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏟*

time loss

⟨

⟩ ⟨

⟩

= | *D *| − | *D*

| \+ | *D *| − | *D *| − *t* ideal − | *D *| − | *D *| − *t* ideal *a*

*a*\+1

*a*\+1

*a*

*a*

*a*

*a*\+1

*a*\+1

*⏟⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏟⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏟*

*⏟⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏟⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏟*

\(18\)

time loss

time loss

According to defined operation in Eq. \(13\) and assump-Equation \(18\) can be written as

tion condition: *Da < * 0 and *Da*\+1 *< * 0 , because of *t* ideal *> * 0 

*a*\+1

⟨

⟩

the following equations be obtained:

*t*

− *t*� = | *D*

| − *t* ideal −| *D *|

*a*\+1

*a*

*a*\+1

*a*

*a*\+1

⟨

⟩

*⏟⏞⏞⏞⏞⏞⏞⏞⏞⏟⏞⏞⏞⏞⏞⏞⏞⏞⏟*

\(24\)

| *D *| − | *D *| − *t* ideal = 0

time loss

*a*

*a*\+1

*a*\+1

*⏟⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏟⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏟*

\(19\)

No matter what | *D *| − *t* ideal *> * 0 or | *D *| − *t* ideal *< * 0 , time loss

*a*\+1

*a*

*a*\+1

*a*

⟨

⟩

| *D *| − *t* ideal *< *| *D *| exists. Therefore, and

*a*\+1

*a*

*a*\+1

*�������������������*

⟨

⟩

time loss

| *D *| − | *D *| − *t* ideal

| − | *D *|

*a*\+1

*a*

*< *| *D*

−

*a*

*a*\+1

*a*

*t* p

*t*�p *< * 0

*a*\+1

*a*

\(25\)

*�������������������������������*

\(20\)

time loss

**Case 3** *D *≥ *D*

*a*

*a*\+1 *> * 0 is assumed. According to the above According to Eqs. \(19\) and \(20\), Eq. \(18\) can be writ-analysis about *D* , the departure time of *G *\( *p*\) and *G *\( *p*\) *a*

*a*\+1

ten as

can be gained in above sequence, respectively, 

⟨

⟩

*t*

− *t*� = | *D*

| − | *D *| − *t* ideal

⎧

*a*\+1

*t *=

*t*

\+ *t* ideal

*a*

*a*\+1

*a*

*a*

*a*

*a*

*�������������������������������*

⎪

*⏟⏟⏟*

⎪

time loss

\(21\)

timestamp

⎪

−\(| *D*

| − | *D *|\)

*t*

= *t *\+ *t* ideal \+ *t* ideal

*a*\+1

*a*

*< * 0

⎪ *a*\+1

⎪

*a*

*a*\+1

*⏟⏟⏟*

Therefore, 

⎪

timestamp

⎨

\(26\)

⎪ *t*� =

*t*

\+ *t* ideal

*t*

− *t*�

*a*\+1

*⏟⏟⏟*

*a*\+1

*a*\+1

*< * 0

*a*

\(22\)

⎪⎪

timestamp

⎪ *t*� = *t *\+ *t* ideal \+ *t* ideal **Case 2** 

*a*

*a*\+1

*a*

*D*

⎪

*a*\+1 *< * 0 and *Da > * 0 are assumed, which means that 

*⏟⏟⏟*

the time loss of 

⎪

*G *\( *p*\) is 0, and departure time of *G *\( *p*\) and 

⎩

timestamp

*a*

*a*

*G*

\( *p*\) can be gained, respectively, 

*a*\+1

It can be found that

⎧

*t *=

*t*

\+ *t* ideal

⎪

*a*

*⏟⏟⏟*

*a*

*t*

− *t*� = *t *\+ *t* ideal \+ *t* ideal − *t *− *t* ideal − *t* ideal

⎪

*a*\+1

*a*

*a*

*a*\+1

*a*\+1

*a*

\(27\)

timestamp

⎪

�

�

= 0

⎪ *t*

= *t *\+ *t* ideal \+ *t* ideal \+ � *D*

� − *t* ideal

*a*\+1

*a*

*a*\+1

*a*\+1

*a*

⎪

*⏟⏟⏟*

*⏟⏞⏞⏞⏞⏞⏞⏞⏞⏟⏞⏞⏞⏞⏞⏞⏞⏞⏟*

Therefore, Eq. \(27\) meet

⎪

timestamp

time loss

⎨

\(23\)

*t*

− *t*� = 0

*a*\+1

*a*

\(28\)

⎪

*t*�

=

*t*

\+ *t* ideal \+ �

�

*a*\+1

*a*\+1

� *Da*\+1�

⎪

*⏟⏟⏟*

*⏟⏟⏟*

⎪

timestamp

time loss

⎪

=

\+

\+

⎪

*t*�

*t *\+ *t* ideal

� *D *� *t* ideal

*a*

*a*\+1

*a*\+1

*a*

⎪

*⏟⏞⏞⏞⏞⏞⏞⏞⏞⏟⏞⏞⏞⏞⏞⏞⏞⏞⏟*

⎩

timestamp

578



H. Hu et al. 

**Algorithm 1 **Platoon schedule algorithm

Game1

Game2

Gamer1-1

Gamer2-1

Gamer1-2

Gamer2-2

Platoon-c

Stop

Platoon-b

Platoon-a

bar

Gamer3-1

schedule and game zone

The payoff of gamerX-1:traffic efficiency

Gamer3-2

The payoff of gamerX-2:fuel consumption

Game3

**Fig. 8 **Gamers and platoons

**4.1 Dynamic Game**

Game theory focuses on decision-making by several gamers in an interdependent situation and addresses the gamers' 

conflict of interests by Nash equilibrium. A game consists of three parts:

1. Game: In a game, gamers are assumed to be rational, and each gamer’s decisions can influence other gamer’s payoff and also influence the performance of the whole game. 

From the above proof of Theorem 1, the optimal schedule 2. Strategy: Strategies are actions that gamers take in a is related to the deadline. Han \[30\] proposed to introduce game to gain a payoff for themselves. The strategy set is the gap feedback control to guarantee that following vehian action sequence and each gamer has its own strategy cles track the leading vehicle's speed trajectory in a platoon. 

set. 

Inspired by their research, a consensus control method is 3. Payoff: Payoff is the maximum benefit that each gamer introduced \[34\] to control following vehicles. The method gains in a game. 

ensures the speed and position of the consensus of the leading vehicle and following vehicles. Noted that the speed **4.2 Game Deep Reinforcement Learning** of the leading vehicle can be gained by the equilibrium control method that will be presented in the next section. 

**4.2.1 Bargaining Game I**

The platoon schedule algorithm is summarized in Algorithm 1 below. At every time step, Algorithm 1 needs to Equilibrating traffic efficiency and fuel consumption is a check and update the platoon group passing sequence based macro problem for the studied scenario including multion the updated vehicle speed and position, The purpose is ple platoons. The macro problem can be transformed into to decrease the longitudinal and lateral headway between a microcosmic problem for the single platoon, that is, the vehicles in conflict zone and guarantee that the intersection above Equilibrium problem for each platoon can be solved space resource is fully utilized. Different from the existing based on game. 

research, Algorithm 1 does not compute the timetable but Next, gamers are defined as

the most efficient passing sequence. That is, passing time of 

\{

\}

each platoon is floating. 

*gamers *= *g *, *g*

1

2

\(29\)

To illustrate the relationship of games, gamers and platoons in the studied scenario, an example is given in Fig. 8. 

**4 Equilibrium Control of Traffic Efficiency **

There are some platoons in the studied scenario. Each pla-and Fuel Consumption

toon has two gamers: gamerX-1 and gamerX-2, and the platoon is medium. The payoff of gamerX-1 is traffic efficiency In this section, an equilibrium control method is proposed and the payoff of gamerX-2 is fuel consumption. There-to equilibrate traffic efficiency and fuel consumption based fore, several games are going to happen for all approach-on the game theory and deep reinforcement learning, which ing platoons at all schedule and game zones. On the other also elaborate how it works. 

hand, since these games have the same number of gamer 

Double Deep Q‑Networks Based Game‑Theoretic Equilibrium Control of Automated Vehicles at…

579

participates, same game actions and same payoff, only one ⎧

game model needs to be constructed for them. 

⎪ *u *= *bt *\+ *c*

Each gamer is rational, and the interaction between them 

⎪

1

*v *=

*bt* 2 \+ *ct *\+ *d*

is existing, so the strategy set is defined as

⎪⎨ 2

\(33\)

\{

\}

⎪

1

1

*x *=

*bt* 3 \+

*ct* 2 \+ *dt *\+ *e*

*S *= *v*| *v*

≤ *v *≤ *v*

⎪

6

2

t

max

cz

min

\(30\)

⎪

�

�

*t *∈ *t *, *t*

sg

cz

where 

⎩

*v * is the vehicle speed at which the vehicles enter cz

conflict zone. The payoff of *g * is the delay time and can be 1

where *b*, *c*, *d*, *e* are integration constants. Initial state and ter-calculated by

minal state can be computed to gain integration constants and gain the control input sequence of the leading vehicle 

⎧

\[

\]

⎪ \( *s *− 1\) *h*

\+ *t* l − *t*

if *p*

min

sg

vf

in *t *, *t * by computing Eq. \(33\). 

sg

cz

Θ = ⎨

*s*

∑

\(31\)

\{

⎪ *s*� *h *\+

*h *\+ *t* l − *t*

else

*i*

sg

vf

\[

\]

⎩ min

***v ***= ***v ***, ***x ***= ***x***

*s*�\+1

f

sg

\(34\)

\[ ***v ***= ***v ***, 

\]

cz ***x ***= ***x*** cz

where *t* l is the time that the leading vehicle takes to pass the sg

schedule and game zone, and *t * is the time that the platoon On the other hand, the control input sequence of each vf

\{

\}

takes to pass the intersection at free-flow speed. *h * is the following vehicles *u* f , *u* f , *u* f , ... can be gained based on min

1

2

3

minimum headway between vehicles of which the number the consensus control method. Therefore, the payoff of *g * 2

is *s *− 1 or *s*′ . *h * is the headway between the vehicles that is evaluated by *i*

cannot catch up with the leading vehicle, and the number of *s*−1

*s*

*t* cz

∑ *t* cz

the vehicles is 

∑

*s *− *s*� . The term \( *s *− 1\) *h * and *s*� *h*

\+

*h * 

*J *=

*u* l\( *t*\)d *t *\+

*u* f\( *t*\)d *t*

*i*

\(35\)

min

min

*i*

∫

∫

*s*�\+1

*t* sg

*i*=2

*t* sg

represent the time following vehicles takes to pass the inters

section. The term ∑

The purpose of solving Hamiltonian formulation of 

*h * represents the time took by the fol-

*i*

Eq. \(32\) is to calculate the first term in Eq. \(35\), and *s*�\+1

lowing vehicles that cannot catch up with the leading acquiring the consensus control input is to calculate the vehicles. 

second term in Eq. \(35\). Recall that the consensus con-The payoff of *g * is fuel consumption which the pla-trol strategy ensures the speed and position of the con-2

toon consumes in the schedule and game zone and conflict sensus of the leading vehicle and following vehicles. On zone. According to Eq. \(30\), the gamer needs to determine the other hand, using the Hamiltonian method ensures that *v * . For the given initial state and terminal state \(i.e., posi-the equilibrium effect is only influenced by the passing cz

tion, speed and timestamp\), the different terminal speed *v* speed, because for a given initial velocity and final veloc-cz

has an effect on fuel consumption. If the terminal speed ity, the results obtained using the Hamiltonian formulation *v * is determined, the acceleration sequence of the leading are optimal in terms of fuel consumption. 

cz

vehicle can be derived by employing Hamiltonian formu-According to bargaining theory, disagreement may exist lation. It is worth stressing here that solving the termi-between rational gamers and means that they cannot make nal speed *v * for the leading vehicle is ultimate goal in an agreement for bargaining, when at least one gamer can-cz

bargaining game. To evaluate the fuel consumption, the 

\{

\}

not gain the satisfactory payoff from the current mode. 

control input sequence *u* l , *u* l , *u* l , ... can be gained for The disagreement strategy can solve the two special cases: 1

2

3

the leading vehicle by solving Hamiltonian formulation. 

**Case1:** The gamers can gain critical payoff about traffic 1

*H*\( *t*, *x*\( *t*\), *u*\( *t*\)\) =

*u* 2\( *t*\) \+ *𝜆xv*\( *t*\) \+ *𝜆vu*\( *t*\) \(32\)

efficiency, that is, the members in the platoon can pass the 2

intersection at free speed with no delay, so the bargaining where *u*\( *t*\) is the control input, *𝜆x* and *𝜆v* are costate. *t * and is not necessary, and a disagreement occurs. 

sg

*t * are timestamps when the platoon enters into schedule and **Case2**: The gamers can gain critical payoff about fuel cz

game zone and conflict zone. Therefore, 

consumption, and the platoon can continually decelerate without accelerating when approaching the intersection. 

In the above cases gamers need to obey *T* opt and does not table

participate in the bargaining game. 

580



H. Hu et al. 

Game

passing speed *v * of a platoon is only maximized, the payoff cz

Game participants: The payoff of each gamer:

Pl

of other platoons may be reduced. *s*′ may be small based Platoon-a Platoon-b Traffic efficiency

at

North

Platoon-c Platoon-d

oo

on the short passing time of the preceding platoon, which n

Platoon-e

-e

prolongs the passing time of following platoons, so Nash equilibrium state can maximize the crossing efficiency of Platoon-d

each platoon. 

Platoon-a

The instantaneous fuel consumption model \[30\] is Platoon-b

Pl

used to evaluate vehicles' fuel consumption. This model atoo

is expressed as

n-c

⎧

*R *\( *t*\) \+ *R *\( *t*\)

⎪ *𝜆*, *a*\( *t*\) ≤ − a

r

⎪

*M* a

�

�

⎪

*R *\( *t*\) \+ *R *\( *t*\)

**Fig. 9 **Gamers in bargaining game II

*f *= ⎨ *𝜆 *\+ *𝜃 R *\( *t*\) *v*\( *t*\), *a*\( *t*\) ∈ − a r

, 0

1

T

\(39\)

⎪

*M* a

According to bargaining theory \[35\], each wishes to 

⎪⎪

*𝜃 M a*\( *t*\)2 *v*\( *t*\)

\(

2

a

maximize payoff to itself of the ultimate bargain, the game 

⎩ *𝜆 *\+ *𝜃 R t*\) *v*\( *t*\) \+

, *a*\( *t*\) ≥ 0

1

T

1000

problem can be formulated as

where *f * is fuel consumption, *𝜆* is the vehicle idling fuel *i*= *n*

∑

consumption rate, *𝜃 * and are power parameters, *M * is the 1

*𝜃* 2

a

min\[Θ *i*\( *v *\) × *Ji*\( *u*\)\]

cz

average vehicle body mass, *R * is the air resistance, *R * is the a

r

*i*=1 *T* opt

table

\(36\)

rolling resistance during the vehicle operation, and *R * is the T

s.t. *v*

≤ *v *≤ *v*

max

cz

min

vehicle force. *R * can be calculated by

a

*a*

≤ *u *≤ *a*

min

max

*𝜌*

*R *\( *t*\) =

*D F v*\( *t*\)2

a

c

a

\(40\)

The solutions maximize the payoff in the traffic efficiency 2

and fuel saving, respectively, and equilibrate them in real where *𝜌* is the air density, *D * is the air resistance coefficient, time. 

c

and *F * is the average frontal vehicle cross-sectional area. *R * 

a

r

can be calculated by

**4.2.2 Bargaining Game II**

1 \+ *v*\( *t*\)

*R *\( *t*\) = 0.01

*M g*

r

a

\(41\)

In bargaining game II, the gamers are different from bargain-44.73

ing game I and defined as

where *g* is the gravitational acceleration, and *R * can be cal-

\{

\}

T

culated by

*gamers *= *g*| *g *= *p*\( *s*\) , *n *∈

*n*

*n*

**ℕ**\+

\(37\)

Only one game is going to happen in the studied scenario *R *\( *t*\) = *M a*\( *t*\) \+ *R *\( *t*\) \+ *R *\( *t*\) \+ *R *\( *t*\) T

a

a

r

g

\(42\)

and all approaching platoons are gamers in this one game. 

Noted that this paper only considers vehicles driving on To illustrate the gamers of this game, an example in Fig. 9 

flat roads and does not take into account the impact of road is given. Noted that the payoff of each gamer is the traffic gradients on the vehicle fuel consumption, so *R *\( *t*\)=0. 

efficiency. 

g

Ma et al. \[36\] and Yu et al. \[37\] quantify the average Strategy set is same as Eq. \(30\) in bargaining game I. cost of vehicle delay by dollar \(6 $/h\) in their research. 

In bargaining game II, the efficiency is only considered, Inspired by their research, 6 $/h and 1.5 $/L are considered so the payoff of gamers can be formulated as

as the basic unit cost of the vehicle delay and vehicle fuel 

⎧

consumption in Eqs. \(31\) and \(35\). The payoff about safety 

⎪ max\( *v *\)

if ∀ *p * is *p * under *v* s

or *v* l

cz

max

max

in bargaining models is not considered, so the minimum min ⎨ *i*= *n*

∏

headway is preset to avoid collisions between platoons. If 

⎪

Θ \( *v *, *s*�\) else

*i*

cz

⎩ *i*=1

\(38\)

the headway between platoons is less than the minimum, bargaining games will be not conducted. 

s.t. *v*

≤ *v *≤ *v*

max

cz

min

This paper focuses on an equilibrium problem rather than *a*

≤ *u *≤ *a*

min

max

an optimization problem about traffic efficiency and fuel where 

consumption. Assuming a fixed group of individuals and *v* s

and *v* l are the maximum straight speed and 

max

max

maximum left turn speed. In this bargaining game process, if allocable resources, there is a condition in which a change from one allocation to another results in making at least one 

Double Deep Q‑Networks Based Game‑Theoretic Equilibrium Control of Automated Vehicles at…

581

person better off without making anyone else worse off. This **Action Space:** Action space is a discrete space and is change is known as Pareto improvement. The necessary con-defined as \[0,1\]. \[0\] represents conducting bargaining game dition of Pareto optimality is that there is no possibility for I, and \[1\] represents conducting bargaining game II. 

any further Pareto improvements. Nash equilibrium is dif-Reward: Reward is to provide feedback to the model ferent from Pareto optimality, and the definition is that any about the performance of the previous action, appropriately player changing their strategy unilaterally under this strategy defined reward helps to take the best action, which guaran-combination, will not increase their own payoff, while keep-tees the convergence of the learning process. The reward ing the strategies of other players unchanged. The definition is sum of average delay time cost *r* dc and average fuel con-is the necessary condition of Nash equilibrium. The game sumption cost *r* fc of each episode and is denoted as focuses on equilibrium utility between gamers and maximiz-ing individual utility. 

*R *= − *r* dc − *r* fc

\(44\)

where *R* is non-decreasing with iteration, and the overall **4.2.3 Game Deep Reinforcement Learning**

reward is always negative. The reward can identify the threat and determine the current game mode. 

Wang \[38\] states a basic principle that the fisherman takes It is necessary to use a deep reinforcement learning advantage of the fight between the snipe and the clam. The method to select a game from two bargaining games. The principle can be considered that when two persons continue main reasons can be attributed to two aspects:

to quarrel, a third person may profit from it and can be considered as a threat for the other two persons. When consider-

• Through the tests, the performance of bargaining game I ing the threat, how to equilibrate traffic efficiency and fuel is subpar under the changing traffic demand in each direc-consumption is important for the game process. Therefore, tion. On the other hand, the equilibrium is achieved by based on the above principle, a cooperation strategy between bargaining game I, but the payoff of gamers is reduced. 

bargaining games is proposed. When a threat appears, bar-For some examples, the traffic efficiency is satisfactory, gaining game II is conducted, and when the threat disap-but the fuel consumption is higher; the traffic efficiency pears, bargaining game I is conducted. The threats can be is lower, and the fuel consumption is higher. The goal is considered as varying traffic conditions \(i.e., varying traffic not only to equilibrate the traffic efficiency and fuel con-demand\), but it is not known whether current traffic condi-sumption \(i.e., the payoff of gamers\), but also to ensure tions can be considered a threat. Therefore, it is a black box that the payoff of each gamer cannot be too low. The problem, and deep reinforcement learning is a good choice reason for the decrease in payoff is the changing traffic to identify the threat. 

demand, that is, the threat is existing in the equilibrium This paper introduces the double deep q-networks 

problem, according to the experiment test results listed \(DDQN\) model and train it to implement the cooperation in the Table 9. Meanwhile, from the training results, it operation. The DDQN algorithm employs two neural net-can be seen that the decisions regarding threats have a works to choose actions and compute values, respectively, significant impact on rewards. 

and can address discrete problems well. More details can • How to identify the threat \(i.e., the changing traffic be found in the Ref. \[39\]. The DDQN model is constructed demand in each direction\) in advance is so important. 

from three aspects: states, actions, and rewards. The training If the threat cannot be accurately identified, the pay-environment and parameter set ings are given in the experi-off of each gamer will be reduced, and the equilibrium ment test part. 

operation will be meaningless. The relationship between **State:** State is defined based on the fact that the DDQN 

the changing traffic demand and Eq. \(36\) is difficult to model needs to know current traffic conditions, so the instant express, so this problem is a black box problem, and the traffic demand is chosen as the observation input. According deep reinforcement learning method is a good choice. 

to the position and speed of vehicles of each entrance lane, the instant traffic demand is evaluated by

In bargaining game I, the macro equilibration problem *n*

∑

is transformed into the microcosmic equilibration problem, *o *= 3600∕\(

\( *t* arr − *t* arr \)∕ *N*\)

and there are some ego games in the scenario. However, *i*

*n*

*n*−1

\(43\)

2

the ego game only focuses on the ego platoon, which does where 

not consider the varying traffic demand, that is, the equi-t arr is the arrival time of the vehicle, and *N* is the vehi-n

cle counter. Therefore, the 8-dimension state space can be libration is executed at the vehicle level. The cooperation 

\{

\}

written as 

strategy between two bargaining games is designed based *O *= *o *, *o *, *o *, *o *, *o *, *o *, *o *, *o *,which reflects *p*

1

2

3

4

5

6

7

8

the current traffic demand. 

on the aforementioned threat principle to cope with the influence caused by varying traffic demand. The trained 

582



H. Hu et al. 

**Table 1 **Simulation parameters

**Algorithm 2 **Equilibrating algorithm

Simulation time

500 s

Schedule and game zone

300–500 m

Free flow speed

15 m/s

Maximum acceleration

1.8 m/s2

Minimum acceleration

− 6 m/s2

Maximum left turning speed

10 m/s

Maximum straight speed

15 m/s

Minimum speed

5 m/s

Maximum traffic demand

700 veh/l/h

Minimum traffic demand

100 veh/l/h

**Table 2 **Instantaneous fuel consumption model parameters Idling fuel consumption rate *𝜆*

0.0375 mL∕s

Power parameter *𝜃*

0.09 mL∕KJ

1

Power parameter 

\(

\)

*𝜃* 2

0.03 mL∕ KJ ⋅ m∕s2

Average vehicle body mass *M*

1400 kg

a

Air density *𝜌*

1.2256 kg∕m3

Air resistance coefficient *D*

0.54

c

Average frontal vehicle cross-sectional area *F* a 2.1m2

Gravitational acceleration *g*

9.8m∕s2

DDQN model can identify the threats and implement the cooperation operation. Noted that the DDQN model does not implement a cooperation operation at every time step but implements a cooperation operation for all observed **5 Simulation Test**

vehicles in the free flow zone. The equilibrating control algorithm is summarized in Algorithm 2 below. 

In this section, the simulation test is implemented with SUMO software and compared with some existing methods 

***Remark 2*** Equilibrium state 2 can be gained from the bar-to show the validity of the proposed methods. Simulation gaining game II according to Fig. 2. Under equilibrium state parameters and fuel consumption model parameters are 2, optimal traffic efficiency can be guaranteed. It implies that listed in Tables 1 and 2. The simulation tests are conducted optimal energy consumption can be gained under optimal for 500 s for each compared method. The length of schedule traffic efficiency. Schedule operation guarantees optimal and game zone is from 300 to 500 m. 

traffic efficiency but does not determine a timetable. The To demonstrate the performance, the proposed methods bargaining game II compensates for the deficiency. 

are compared with some existing methods in the paper. 

Noted that A1 is Algorithm 1, A2 is Algorithm 2, and 

***Remark 3*** In the bargaining theory in Refs. \[35\] and \[40\], B1 is Bargaining game I. The Pw method represents the the gamers can threaten each other and terminate bargain-piece-wise speed trajectory planning method in the Ref. 

ing. The above threat is different from the bargaining theory 

\[41\]. The Par method is the multi-objective optimization and can reduce the payoff of each gamer simultaneously. method. 

On the other hand, only the dynamic game is considered in this paper. 

• ASC method: The ASC method is an adaptive signal control method, which is used to schedule vehicles. Vehicles 

***Remark 4*** Interaction between gamers is a key part in game are not allowed to cross intersection as platoons, and the theory, so communication between gamers is necessary. In speed trajectories are not controlled. 

this paper, the communication delay is not considered. 

• FCFS method: Vehicles are permitted to pass the intersection as platoons, and the FCFS method \[42\] is used to schedule platoons. The consensus control algorithm 





Double Deep Q‑Networks Based Game‑Theoretic Equilibrium Control of Automated Vehicles at…

583

**Table 3 **Training parameters

Parameter

Value

Gamma

0.9

Initial episode

0.5

Final episode

0.1

Steps from initial episode to final episode

10,000

Memory buffer size

20,000

Minibatch size

64

Frequency to update target Q network

1

Learning rate

0.001

Pre-training episodes

5000

\(a\) Average reward of DDQN method

• A1-A2 method: The proposed Algorithm 1 and Algo-

rithm 2 are both used to schedule platoons and control the vehicle speed. 

• A1-Par method: The proposed Algorithm 1 is used to schedule platoons and the multi-optimization method is used to optimize two objectives. 

The deep reinforcement learning model learned optimal action based on collected data about states and rewards. The model stored states, actions, and rewards into a memory buffer, where a mini-batch of data used in training will be \(b\) Average reward of PPO method

sampled. The model uses mini-batch data to update neural networks in order to achieve optimal action and higher rewards for continuing training. Model training and data collection are implemented simultaneously. A training environment needs to be built: Algorithms 1 and 2 are implemented, based on the equilibrium control framework proposed in Sect. 2 and simulation parameters in Table 1. Each episode will be implemented for 3500 s, and the time step is 1 s. 

Traffic demand, for each episode, at the initialization point, can vary from 100 to 700 veh/l/lane. 

To illustrate the DDQN method is more suitable for solving this problem, the DDQN method, the Proximal Policy Optimization method \[43\] \(PPO\) and the Soft Actor Critic \(c\) Average reward of SAC method

method \[44\] \(SAC\) are tested and compared. Test results are presented in Fig. 10, and it is evident that the reward range **Fig. 10 **Average reward during training episodes for the PPO method is around − 2100 and is lower than that of the DDQN method. The reward for SAC can reach to 

is used to guarantee consensus of the speed and location 1950, but its reward range is large, which results in a lack of between the leading vehicle and following vehicles. 

stability. The DDQN method has shown good performance. 

• A1-Pw method: Vehicles are permitted to cross the inter-The reason for this test result is that the DQN series of meth-section as platoons, and Algorithm 1 is used to schedule ods excel at solving discrete action problems, whereas PPO 

platoons. The Pw method \[41\] is used to optimize the and SAC excel at solving continuous action problems. 

fuel consumption for vehicles. 

In the DDQN model, both the current network and the 

• A1-B1 method: Bargaining game I is used to control the target network contain a two-layer neural network with 128 

vehicle speed instead of the Piece-wise speed planning neurons for each layer. The training parameters are set in method, and Algorithm 1 is used to schedule platoons. 

Table 3. The average reward converges to optimum gradually during training, as shown in Fig. 7. 

584



H. Hu et al. 

**Table 4 **Simulation result of 6 

Methods

Demand \(veh/h/lane\)

methods under different traffic 

demand

100

200

300

400

500

ASC method

Delay\(s\)

5.25

5.86

12.94

42.77

54.26

Fuel \(mL\)

28.22

28.04

31.18

45.67

51.56

FCFS method

Delay\(s\)

3.71

3.75

16.44

16.08

16.24

Fuel \(mL\)

19.20

19.20

24.57

25.93

36.06

A1-Pw method

Delay\(s\)

3.84

3.81

7.63

8.19

19.17

Fuel \(mL\)

25.75

25.76

29.10

29.87

36.99

A1-B1 method

Delay\(s\)

3.76

3.80

8.97

9.11

28.65

Fuel \(mL\)

19.29

19.22

20.79

20.71

44.10

A1-A2 method

Delay\(s\)

3.72

3.80

8.98

9.10

17.16

Fuel \(mL\)

19.17

19.21

20.81

20.88

33.55

A1-Par method

Delay\(s\)

3.41

3.38

9.49

8.77

22.49

Fuel \(mL\)

23.30

23.40

21.08

28.25

30.33

**Table 5 **Comparison of ASC method and A1-A2 method The simulation is ran for 500 s and the performance of the A1-A2 method with other methods under the fixed traffic Demand 

Delay \(%\) Fuel \(%\) ASC 

A1-A2 method 

\(veh/h/lane\)

method cost cost \($/h%\)

demand are compared. Simulation results and comparison \($/h\)

results are summarized in Tables 4, 5, 6 and 7, respectively. 

The A1-A2 method outperforms the ASC method under 

100

− 29.14% − 32.07% 182.63

124.95 − 31.58%

different demand level, since vehicles may stop at the stop 200

− 35.15% − 31.49% 185.17

125.62 − 32.16%

bar to wait for the green light, which prolongs the idle state 300

− 30.60% − 33.26% 242.91

164.10 − 32.44%

and reduces the passing speed. The A1-A2 method reduces 400

− 78.72% − 54.28% 492.97

165.17 − 66.49%

the average delay time by 78.72% and fuel consumption by 500

− 68.37% − 34.93% 590.96

280.01 − 52.62%

54.28%, especially under 400 veh/h/lane. The cost of FCFS 

and A1–A2 is similar when traffic demand is below 200 

veh/h/lane, and the reason is that under FCFS policy, vehicles slow down to delay the arrival time according to the **Table 6 **Comparison of FCFS method and A1-A2 method time table. This operation can reduce fuel consumption and average delay. As the increasing of the demand level, the Demand 

Delay \(%\)

Fuel \(%\)

FCFS method A1-A2 

\(veh/h/lane\)

cost \($/h\)

method 

average delay and fuel consumption increased in an obvi-cost \(%\)

ous trend. 

The reduction of the A1–A2 method in fuel consumption 100

\+ 0.27%

− 0.16%

125.05

− 0.08%

is up to 25.55%, compared with the A1-Pw method. How-200

**\+ 1.33%**

**\+ 0.05%**

125.28

**\+ 0.27%**

ever, the traffic efficiency is similar, when traffic demand is 300

− 45.38%

− 15.30%

227.37

− 27.83%

below 200 veh/h/lane. It means that Eq. \(36\) can equilibrate 400

− 43.41%

− 19.48%

232.64

− 29.00%

them by the multiplication of the payoff when game hap-500

**\+ 5.67%**

− 6.96%

288.26

− 2.86%

pens. The equilibrium phenomenon also appears under 300 

and 400 veh/h/lane, we can see that the gamers also consider each other's payoff compared with the A1-Pw method. 

Although the purpose of Algorithm 2 maximizes the pay-Table 7 Comparison of A1-Pw method and A1-A2 method off of each gamer, from the comparison of results shown in Tables 5, 6, 7, it can be seen that the A1-A2 method can Demand 

Delay \(%\)

Fuel \(%\)

A1-Pw 

A1-A2 

\(veh/h/lane\)

reduced the average cost obviously, which indicates that it method 

method 

cost\($/h\)

cost \(%\)

also can improve the comprehensive performance of the intersection \(Table 8\). 

100

− 3.12%

− 25.55%

161.17

− 22.47%

The performance of the A1–A2 method is similar with 

200

− 0.26%

− 25.43%

161.05

− 22.00%

the A1–B1 method under the fixed demand of 1–4, so the 300

**\+ 17.69%**

− 28.49%

201.09

− 18.39%

comparison result is not given. This phenomenon means 400

**\+ 11.11%**

− 30.10%

208.47

− 20.77%

that the bargaining game II is not conducted by the DDQN 

500

− 10.49%

− 9.30%

310.16

− 9.72%

model. To test the performance of Algorithm 2 further, four 

Double Deep Q‑Networks Based Game‑Theoretic Equilibrium Control of Automated Vehicles at…

585

**Table 8 **Varying traffic demand

Traffic demand

1

Period \(s\)

\[0, 100\]

\[100, 400\]

\[400, 500\]

N/A

N/A

Demand \(veh/h/lane\)

100

500

200

N/A

N/A

2

Period \(s\)

\[0, 50\]

\[50, 200\]

\[200, 500\]

N/A

N/A

Demand \(veh/h/lane\)

200

100

300

N/A

N/A

3

Period \(s\)

\[0, 100\]

\[100, 150\]

\[150, 200\]

\[200, 450\]

\[450, 500\]

Demand \(veh/h/lane\)

200

100

400

300

700

4

Period \(s\)

\[0, 100\]

\[100, 200\]

\[200, 250\]

\[250, 350\]

\[350, 500\]

Demand \(veh/h/lane\)

300

200

500

600

200

**Table 9 **Simulation results 

Demand 1

Demand 2

Demand 3

Demand 4

under varying traffic demand

A1-B1 method

Delay \(s\)

29.86

7.55

13.65

33.40

Fuel \(mL\)

30.04

20.74

23.64

31.97

A1-A2 method

Delay \(s\)

7.80

7.53

10.87

19.72

Fuel \(mL\)

26.34

20.65

24.49

30.50

**Table 10 **Comparison of A1-B1 

Demand level

Delay \(%\)

Fuel \(%\)

A1-B1 method 

A1-A2 method cost 

method and A1-A2 method

cost \($/h\)

\($/h %\)

Demand 1

− 73.88%

− 12.32%

334.21

187.16

− 44.00%

Demand 2

N/A

N/A

N/A

N/A

N/A

Demand 3

− 20.37%

**\+ 3.60%**

206.28

194.86

− 5.54%

Demand 4

− 40.96%

− 4.60%

365.02

278.29

− 23.76%

varying demands are considered in the A1–B1 and A1–A2 

This observation can be made from Fig. 10. In terms of the methods. The simulation results and comparison results are average reward for each agent, the minimum reward reaches summarized in Tables 9 and 10, respectively. 

as low as − 2400. 

Three evaluation criteria of two methods are similar In fact, bargaining game I between two virtual gamers is under demand 2, that is, the bargaining game II is not con-meaningless under threat, because the payoff of each gamer ducted and the threat does not exist. The A1–A2 method is reduced. All gamers need to participate in bargaining shows satisfactory performance under demand 1 and reduces game II to cope with the threat. On the other hand, if the the average delay time and fuel consumption by 73.88% threat disappears and bargaining game II is still conducted, and 12.32%, respectively. From the comparison results the payoff of gamers is also reduced. Therefore, game rein-under other demands, the trained DDQN model identifies forcement learning outperforms bargaining games in terms the threats and considers bargaining game II as the current of the performance. 

game mode becomingly. Under demand 3–4 delay difference With regard to the Pareto optimality solution, it becomes between them is obvious. The reason is that the bargaining readily apparent that the equilibrium phenomenon is dis-game II sacrifices the payoff about fuel consumption under cernible. Specifically, under the traffic demand of 100 and the threats, but bargaining game I is thoughtful when there 200 veh/h/lane, the Nash equilibrium solution leads to an is no threat. 

improvement in traffic delay while appropriately reducing In Table 8, when employing the A1–B1 method, it effec-fuel consumption. This effect is attributed to the fact that tively reduces fuel consumption, but simultaneously, it leads low traffic demand does not necessitate high passing speeds. 

to an increase in time delays under Demand 3. Regrettably, Moreover, at a traffic demand of 500 veh/h/lane, the Nash under Demand 1, Demand 2, and Demand 4, the A1-B1 equilibrium solution results in a decrease in the traffic delay method results in both increased fuel consumption and time and an improvement in the fuel consumption. In the range delays. Moreover, if a threat is mistakenly identified, the of 300–400 veh/h/lane, the utility of Pareto optimality and performance of the A1–A2 method is also unsatisfactory. Nash equilibrium solutions exhibits a notable similarity. 

586



H. Hu et al. 

**6 Conclusion**

This paper first proposes an equilibrium control framework consisting of two parts. In the first part, a platoon scheduling method is proposed that considers platoon formation in the schedule process. Moreover, mathematical proof of the method is given. In the second part, a game reinforcement learning model is designed and an equilibrating control method is proposed. The simulation experiment shows that the proposed methods can equilibrate traffic efficiency and fuel consumption to an equilibrium state. while also reducing vehicle trip costs. In fact, the state can be divided **Fig. 11 **Position curve

into equilibrium state 1 and equilibrium state 2, which can be achieved by bargaining game I and bargaining game II, respectively, according to the occurrence of threat. In fact, the assessment of the threat is considered as a black box problem, and thus the trained deep reinforcement learning model plays an important role. In the future, communication delay factor and driving style will be considered in the studied scenario. 

**Acknowledgements** This work is supported in part by the National Key R&D Program of China \(2022YFB2502904\), the Natural Science Foundation of Hubei Province for Distinguished Young Schol-ars \(2022CFA091\), the Key R&D Program of Hubei Province \(2021BAA020 2021BAA181\), and Wuhan Science and Technology Major Project \(2022013702025184\), the Natural Science Foundation of Chongqing, China \(CSTB2023NSCQ-MSX0932\). 

**Fig. 12 **Speed curve

**Declarations **

The position and speed curves of vehicles in a platoon at **Conflict of Interest** On behalf of all the authors, the corresponding au-the schedule and game zone are shown in Figs. 11 and 12. 

thor states that there is no conflict of interest. 

Several observations can be made from the results:

**References**

• The speed curve indicates that the platoon continuously changes the speed. The speed curve of the following 1. Schrank, D., Eisele, B., Lomax, T.: Urban mobility report 2019. 

vehicle indicates that the following vehicles run after \(2019\)

the leading vehicle at a maximum speed before the 30th 2. Nalley, S., LaRose, A.: Annual energy outlook 2022 \(AEO2022\). 

second, and the consensus state converges at the 32nd Energy Information Agency, 23, \(2022\)

second. Based on this fact, the definitions of the deadline 3. Du, Y., ShangGuan, W., Chai, L.: A coupled vehicle-signal control method at signalized intersections in mixed traffic environment. 

of schedule task is given, propose Theorem 1 and prove IEEE Trans. Veh. Technol. **70**\(3\), 2089–2100 \(2021\) it in different cases. 

4. Cai, M., et al.: Multi-lane unsignalized intersection cooperation 

• The passing speed of a platoon at the conflict zone is with flexible lane direction based on multi-vehicle formation con-about 7.5 m/s, which is a game result of bargaining game trol. IEEE Trans. Veh. Technol. **71**\(6\), 5787–5798 \(2022\) 5. Choi, M., Rubenecia, A., Choi, H.H.: Reservation-based traffic I. In bargaining game I, gamers bargain with each other management for autonomous intersection crossing. Int. J. Distrib. 

to gain individual payoff, so *v * is less than the maximum Sens. Netw. **15**\(12\), 1550147719895956 \(2019\)

cz

speed. If the threat occurs, 

6. Yu, C., et al.: Managing connected and automated vehicles at *v * may be larger according to 

cz

bargaining game II. 

isolated intersections: from reservation- to optimization-based methods. Transp. Res. Pt. B Methodol. **122**, 416–435 \(2019\)

• Based on the introduced consensus control algorithm, 7. Xu, H., et al.: A general framework for decentralized safe opti-after 30 s, two following vehicles keep up with the lead-mal control of connected and automated vehicles in multi-lane ing vehicle, and the arrival time and fuel consumption of signal-free intersections. IEEE Trans. Intell. Transp. Syst. **23**\(10\), them in game I can be evaluated. 

17382–17396 \(2022\)

8. Wang, Y., Cai, P., Lu, G.: Cooperative autonomous traffic organization method for connected automated vehicles in 

Double Deep Q‑Networks Based Game‑Theoretic Equilibrium Control of Automated Vehicles at…

587

multi-intersection road networks. Transp. Res. Pt. C-Emerg. 

27. Bai, Z., et al.: Hybrid reinforcement learning-based eco-driving Technol. **111**, 458–476 \(2020\)

strategy for connected and automated vehicles at signalized intersec-9. Yao, Z., et al.: Integrated schedule and trajectory optimization tions. IEEE Trans. Intell. Transp. Syst. **23**\(9\), 15850–15863 \(2022\) for connected automated vehicles in a conflict zone. IEEE Trans. 

28. Liu, B., et al.: Adaptive speed planning of connected and automated Intell. Transp. Syst. **23**\(3\), 1841–1851 \(2022\) vehicles using multi-light trained deep reinforcement learning. IEEE 

10. Wang, K., et al.: Game-theory-inspired hierarchical distributed Trans. Veh. Technol. **71**\(4\), 3533–3546 \(2021\)

control strategy for cooperative intersection considering priority 29. Nan, J., Deng, W., Zheng, B.: Intention prediction and mixed negotiation. IEEE Trans. Veh. Technol. **70**\(7\), 6438–6449 \(2021\) strategy nash equilibrium-based decision-making framework for 11. Spatharis, C., Blekas, K.: Multiagent reinforcement learning for autonomous driving in uncontrolled intersection. IEEE Trans. Veh. 

autonomous driving in traffic zones with unsignalized intersec-Technol. **71**\(10\), 10316–10326 \(2022\)

tions. J. Intell. Transport. Syst. **2022**, 1–17 \(2022\) 30. Han, X., Ma, R., Zhang, H.M.: Energy-aware trajectory optimization 12. Antonio, G.-P., Maria-Dolores, C.: Multi-agent deep reinforce-of CAV platoons through a signalized intersection. Transp. Res. Pt. 

ment learning to manage connected autonomous vehicles at C-Emerg. Technol. **118**, 102652 \(2020\)

tomorrow’s intersections. IEEE Trans. Veh. Technol. **71**\(7\), 31. Feng, Y., He, D., Guan, Y.: Composite platoon trajectory planning 7033–7043 \(2022\)

strategy for intersection throughput maximization. IEEE Trans. Veh. 

13. Guo, Z., et al.: Coordination for connected and automated vehi-Technol. **68**\(7\), 6305–6319 \(2019\)

cles at non-signalized intersections: a value decomposition-based 32. Frey, B.J., Dueck, D.: Clustering by passing messages between data multiagent deep reinforcement learning approach. IEEE Trans. 

points. Science **315**\(5814\), 972–976 \(2007\)

Veh. Technol. **72**\(3\), 3025–3034 \(2022\)

33. Jackson, J.R.: Scheduling a production line to minimize maxi-14. Lioris, J., et al.: Platoons of connected vehicles can double mum tardiness. California Univ Los Angeles Numerical Analysis throughput in urban roads. Transp. Res. Pt. C-Emerg. Technol. 

Research. \(1955\)

**77**, 292–305 \(2017\)

34. Ren, W., Atkins, E.: Distributed multi-vehicle coordinated control-15. Li, D., et al.: COOR-PLT: a hierarchical control model for coor-via local information exchange. Int. J. Robust Nonlinear Control dinating adaptive platoons of connected and autonomous vehicles **17**\(10–11\), 1002–1033 \(2007\)

at signal-free intersections based on deep reinforcement learning. 

35. Nash, Jr, J.F.: The bargaining problem. Econom. J. Econom. Soc. 

Transp. Res. Pt. C-Emerg. Technol. **146**, 103933 \(2023\) 155–162 \(1950\)

16. Deng, Z., et al.: Cooperative platoon formation of connected and 36. Ma, W., et al.: Optimization of pedestrian phase patterns and signal autonomous vehicles: toward efficient merging coordination at timings for isolated intersection. Transp. Res. Pt. C Emerg. Technol. 

unsignalized intersections. IEEE Trans. Intell. Transp. Syst. **24**\(5\), **58**, 502–514 \(2015\)

5625–5639 \(2023\)

37. Yu, C., et al.: Optimization of vehicle and pedestrian signals at 17. Jiang, S., et al.: Coordination of mixed platoons and eco-driving isolated intersections. Transp. Res. Pt. B-Methodol. **98**, 135–153 

strategy for a signal-free intersection. IEEE Trans. Intell. Transp. 

\(2017\)

Syst. **24**\(6\), 6597–6613 \(2022\)

38. Wang, J.: The economic consequences of the epidemic: preliminary 18. Li, L., Wang, F.-Y.: Cooperative driving at blind crossings using forecasts of china’s economic response to the epidemic’s end based intervehicle communication. IEEE Trans. Veh. Technol. **55**\(6\), on china. In: 2022 7th International Conference on Social Sciences 1712–1724 \(2006\)

and Economic Development \(ICSSED 2022\). 2022. Atlantis Press. 

19. Lin, P., et al.: Autonomous vehicle-intersection coordination 39. Van Hasselt, H., Guez, A., Silver, D.: Deep reinforcement learning method in a connected vehicle environment. IEEE Intel . Transp. 

with double q-learning. In: Proceedings of the AAAI conference on Syst. Mag. **9**\(4\), 37–47 \(2017\)

artificial intelligence \(2016\)

20. Yang, H., Almutairi, F., Rakha, H.: Eco-driving at signalized 40. Nash, J.: Two-person cooperative games. Econom. J. Econom. Soc., intersections: a multiple signal optimization approach. IEEE 

128–140 \(1953\)

Trans. Intell. Transp. Syst. **22**\(5\), 2943–2955 \(2020\) 41. Feng, Y., Yu, C., Liu, H.X.: Spatiotemporal intersection control in 21. Yao, Z., et al.: A two-stage optimization method for schedule and a connected and automated vehicle environment. Transp. Res. Pt. 

trajectory of CAVs at an isolated autonomous intersection. IEEE 

C-Emerg. Technol. **89**, 364–383 \(2018\)

Trans. Intell. Transp. Syst. **24**\(3\), 3263–3281 \(2023\) 42. Jin, Q., Wu, G., Boriboonsomsin, K., Barth, M.: Platoon-based 22. Xu, H., et al.: Comparison of cooperative driving strategies for multi-agent intersection management for connected vehicle. In CAVs at signal-free intersections. IEEE Trans. Intell. Transp. 

16th International IEEE Conference on Intel igent Transportation Syst. **23**\(7\), 7614–7627 \(2021\)

Systems \(ITSC 2013\), pp. 1462–1467, IEEE, 2013. 

23. Chalaki, B., Malikopoulos, A.A.: Optimal control of connected and 43. Schulman, J., et al., Proximal policy optimization algorithms. arXiv automated vehicles at multiple adjacent intersections. IEEE Trans. 

preprint arXiv:.06347, 2017. 

Control Syst. Technol. **30**\(3\), 972–984 \(2021\)

44. Haarnoja, T., et al. Soft actor-critic: Off-policy maximum entropy 24. Ard, T., et al.: Energy-efficient driving in connected corridors via deep reinforcement learning with a stochastic actor. In: International minimum principle control: vehicle-in-the-loop experimental veri-conference on machine learning. 2018. PMLR. 

fication in mixed fleets. IEEE T. Intell. Veh. **8**\(2\), 1279–1291 \(2023\) 25. Hadjigeorgiou, A., Timotheou, S.: Real-time optimization of fuel-Springer Nature or its licensor \(e.g. a society or other partner\) holds consumption and travel-time of CAVs for cooperative intersection exclusive rights to this article under a publishing agreement with the crossing. IEEE T. Intell. Veh. **8**\(1\), 313–329 \(2022\) author\(s\) or other rightsholder\(s\); author self-archiving of the accepted 26. Guo, Q., et al.: Hybrid deep reinforcement learning based eco-driv-manuscript version of this article is solely governed by the terms of ing for low-level connected and automated vehicles along signalized such publishing agreement and applicable law. 

corridors. Transp. Res. Pt. C-Emerg. Technol. **124**, 102980 \(2021\)



# Document Outline

+ Double Deep Q-Networks Based Game-Theoretic Equilibrium Control of Automated Vehicles at Autonomous Intersection  
	+ Abstract 
	+ 1 Introduction  
		+ 1.1 Related Work and Motivation 
		+ 1.2 Contribution 
		+ 1.3 Organization 

	+ 2 Problem Statement 
	+ 3 Optimal Schedule of Vehicle Passing Sequence 
	+ 4 Equilibrium Control of Traffic Efficiency and Fuel Consumption  
		+ 4.1 Dynamic Game 
		+ 4.2 Game Deep Reinforcement Learning  
			+ 4.2.1 Bargaining Game I 
			+ 4.2.2 Bargaining Game II 
			+ 4.2.3 Game Deep Reinforcement Learning 


	+ 5 Simulation Test 
	+ 6 Conclusion 
	+ Acknowledgements  
	+ References



