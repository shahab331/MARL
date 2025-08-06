***applied ***

***sciences***

Article

**Cooperative Decision-Making for Mixed Traffic at an**

**Unsignalized Intersection Based on Multi-Agent**

**Reinforcement Learning**

**Huanbiao Zhuang, Chaofan Lei, Yuanhang Chen and Xiaojun Tan \***

School of Intelligent Systems Engineering, Sun Yat-sen University, Shenzhen 518107, China

**\* **Correspondence: tanxj@mail.sysu.edu.cn

**Abstract: **Despite rapid advances in vehicle intelligence and connectivity, there is still a significant period in mixed traffic where connected, automated vehicles and human-driven vehicles coexist. The behavioral uncertainty of human-driven vehicles makes decision-making a challenging task in an unsignalized intersection scenario. In this paper, a decentralized multi-agent proximal policy optimization \(MAPPO\) based on an attention representations algorithm \(Attn-MAPPO\) was developed to make joint decisions at an intersection to avoid collisions and cross the intersection effectively. 

To implement this framework, by exploiting the shared information, the system was modeled as a model-free, fully cooperative, multi-agent system. The vehicle employed an attention module to extract the most valuable information from its neighbors. Based on the observation and traffic rules, a joint policy was identified to work more cooperatively based on the trajectory prediction of all the vehicles. To facilitate the collaboration between the vehicles, a weighted reward assignment scheme was proposed to focus more on the vehicles approaching intersections. The results presented the advantages of the Attn-MAPPO framework and validated the effectiveness of the designed reward function. Ultimately, the comparative experiments were conducted to demonstrate that the proposed approach was more adaptive and generalized than the heuristic rule-based model, which revealed its great potential for reinforcement learning in the decision-making of autonomous driving. 

**Keywords: **cooperative decision-making; connected and automated vehicles; multi-agent reinforce-Citation: Zhuang, H.; Lei, C.; Chen, 

ment learning; unsignalized intersection

Y.; Tan, X. Cooperative

Decision-Making for Mixed Traffic at

an Unsignalized Intersection Based

on Multi-Agent Reinforcement

Learning. Appl. Sci. **2023**, 13, 5018. 

**1. Introduction**

https://doi.org/10.3390/

In recent years, with the development of vehicle-to-everything \(V2X\) and sensor

app13085018

technologies, connected and automated vehicles \(CAVs\) received extensive attention re-Academic Editor: Rosario Pecora

garding their ability to reduce the occurrence of traffic congestion and accidents \[1\]. Using environmental sensing sensors, such as cameras, lidar, and radar, the CAVs are able to Received: 10 March 2023

obtain the state of roads and vehicles around them. The continuous development of V2X

Revised: 5 April 2023

\(vehicle-to-everything\) technology has accelerated the development of the automobile Accepted: 13 April 2023

intelligent network. V2X, including vehicle-to-vehicle \(V2V\), vehicle-to-infrastructure Published: 17 April 2023

\(V2I\), and vehicle-to-pedestrians \(V2P\), enables each CAV to share information about the vehicle position, speed, acceleration, orientation, destination, etc. with any traffic partic-ipating entity, which enhances the range of perception for these vehicles \[2\]. Equipped with perception systems and vehicular communications, a CAV acquires a wider range of **Copyright: **© 2023 by the authors. 

information, which is beneficial for cooperative driving to evade crashes and achieve better Licensee MDPI, Basel, Switzerland. 

This article is an open access article

traffic performance \[3\]. 

distributed under the terms and

According to the intelligent degree of vehicles, vehicles are divided into six levels, conditions of the Creative Commons

from L0 to L5, by the Society of Automotive Engineers \(SAE\). By 2030, 82 million L4/L5

Attribution \(CC BY\) license \(https://

intelligent vehicles will be in operation in China, the United States, and Europe \[4\]. Despite

creativecommons.org/licenses/by/

the dramatic advances in autonomous driving, the predictable transition from purely 4.0/\). 

conventional vehicles to a purely intelligent and connected environment will require a Appl. Sci. **2023**, 13, 5018. https://doi.org/10.3390/app13085018

https://www.mdpi.com/journal/applsci

Appl. Sci. **2023**, 13, 5018

2 of 19

sustained investment in infrastructure and technology development. In the coming years, the transportation environment will exist in a transition stage of mixed transportation where the human-driven vehicles \(HDVs\) and CAVs coexist. 

In general, significant research regarding cooperative decision-making and control is under the assumption that all the vehicles on the road are CAVs \[5,6\]. Cooperative decision-making and control in mixed traffic is a challenge in the field of intelligent transportation systems \(ITSs\) \[7\]. This is the reason why the CAVs need to interact with the HDVs, however the behavior of the HDVs is uncertain. To ensure a safe collaboration in mixed traffic environments, it is more practical to implement strategies for the CAVs that take the driver’s behavior into account than expecting drivers to interact with the CAVs with caution. To imitate the human driving behavior, Treiber et al. developed an intelligent driver model \(IDM\) \[8\]. As a safe distance model, the IDM is able to describe the behavior of vehicles from free flow to congested flow with fewer parameters and reflects the dynamic changes of the vehicle position and speed in real time. Peng et al. \[9\] modeled the HDVs using the IDM, which were guided by the CAVs to avoid collision and congestion and achieved a significant traffic efficiency. Li et al. \[10\] extended the IDM using the Ornstein–

Uhlenbeck process to describe the perceptual error dynamically. Wang et al. \[11\] proposed a model that combined a first principles nominal model with a Gaussian process model to predict human behaviors and then implemented a mixed platoon. However, the HDVs normally follow traffic rules to drive, rather than following the CAVs. Based on this view, the CAVs will anticipate the trajectories of the HDVs and cooperate to upgrade their safety and crossing efficiency in this paper. 

An unsignalized intersection scenario does not have traffic lights to govern it. The existence of conflict areas at the lane interchanges and the changes in the vehicle driving behaviors can easily cause disorder, resulting in traffic safety accidents, such as rear-end collisions and traffic jams, which is where a large number of accidents occur \[12\]. In this paper, we assumed that all the vehicles, including the HDVs, will be given the right of way according to the traffic regulations. Based on this assumption, the CAVs learned to adapt to the HDVs and cooperate with them for safe and efficient crossing. Since multiple CAVs are required for cooperative driving, it is natural to adopt a multi-agent reinforcement learning framework to achieve the cooperative goal. The multi-agent proximal policy optimization \(MAPPO\) in a cooperative setting \[13\], which had a surprising effectiveness, was used as the benchmark algorithm in this paper. The original algorithm directly took the information from the agent’s neighbors as its own observations. As the number of agents increased, learning became more difficult \[14\]. Therefore, an attention representation was utilized to select the most relevant information from the vehicle’s neighbors. In the context of the cooperative multi-agent setting, the reward assignment problem concentrated on how to assign a global return to each agent that accurately reflected the agent’s contribution to the overall behavior. We noted that the distance between a vehicle and the intersection had different effects on the safe operation of the system, and thus proposed a weight reward assignment scheme. 

Therefore, to address the above problems in this paper, a decentralized MAPPO based on the attention representations \(Attn-MAPPO\) is proposed to make joint decisions at the intersection based on the trajectory prediction of all the vehicles. The contributions of this paper are fourfold. 

First, decision-making at the intersection where the CAVs and HDVs coexist was formulated as a decentralized MARL problem. Based on the traffic rules and the most valuable neighbor information extracted by an attention module, the Attn-MAPPO algorithm was developed to allow vehicles to cross the intersection safely and effectively. 

Secondly, a weighted reward assignment scheme was proposed. According to the position of the vehicles, the contribution of each CAV could be measured to enhance the cooperation between the vehicles. 

Appl. Sci. **2023**, 13, 5018

3 of 19

Thirdly, an effective reward function was designed. Due to the uncertain behavior of the HDVs, all the vehicle’s trajectories at every time step were predicted in a forward predictive time horizon, which reflected precisely how well the action was taken. 

Fourthly, we conducted the comparative experiment about the traditional heuristic rule-based and our proposed approaches, and the results showed that our proposed approach was more adaptive and generalized in a complex traffic environment. 

The remainder of the paper is organized as follows. Section 2 briefly reviews several approaches to settle the decision-making problem at an intersection. Section 3 states some of the problems, including the research scenario, the right of way the rules, and the vehicle intersection model. The problem formulation and the proposed MARL framework are described in Section 4. The experiments, results, and discussions are presented in Section 5. 

The paper is concluded, and the future works are discussed in Section 6. 

**2. Literature Review**

Due to the complex interactions, the decisions made by the CAVs at the unsignalized intersections are a critical issue. Several approaches have been recommended for a settlement, namely the rule-based, optimization-based, and data-driven algorithms. 

Earlier research mainly used a rule-based approach, where the main idea was to determine the order of the vehicle passage based on the rules or experience. The most direct approach was to carry out the first-in-first-out rule reservation scheme based on the centralized controller \[15\]. Another distributed approach based on fuzzy logic controllers was proposed. Milanes et al. \[16\] used V2V communication to determine the position and speed of the other vehicles in the intersection and then utilized a fuzzy controller to adjust the speed according to the speed of the vehicles with right of way. The rule-based approach was simple to implement, but not optimal. 

Optimization-based algorithms take the decision factor as the objective and formulate the optimization under the constraints. Bian et al. \[17\] presented a distributed optimization to schedule the arriving times for the trajectory planning and achieved a satisfactory cooperative management with a 8.8–18.1% growth in the average passing times. However, the real-time optimization was limited to a high computational load and could not be achieved. In recent work, the combination of the above two approaches realized the approximations that dealt with the optimization via some heuristic rules, leading to a good trade-off between the performance and the computational complexity. For example, Xu et al. \[18\] solved a nearly globally optimal coordinated decision using the Monte Carlo tree search algorithm based on the feasible passing order that was selected using two heuristic rules. Vaio at el. \[19\] reformulated the vehicle coordination as the equivalent virtual platoon control problem based on the ascending order of the distance to the intersection. Due to the lack of learning and adaptability, these two methods were intractable to effectively tackle the task without accurate models. 

As the field of artificial intelligence evolved, data-driven approaches have been a research hotspot for model-free problems due to their unparalleled data processing and generalization ability. Game theory \[20\] and deep reinforcement learning \(DRL\) \[21\] play a significant role in the decision-making at intersections. DRL addresses the cooperative decision-making tasks depending on the impressive learning capabilities based on the continuous interaction. 

Isele et al. \[22\] used DRL to identify the strategy that outperforms the common approach based on the heuristic rules. Lin et al. \[23\] discovered that when the scenario was modeled inaccurately, the policy trained by DRL performed better than the optimization approach of the interior point optimization \(IPO\). Shi et al. \[24\] proposed a coordinated control method with a proximal policy optimization \(PPO\) to make the CAV adapt to the HDVs. Liu et al. \[25\]

employed a DRL to guide the expected speed and converge to the planned decision. 

However, these studies involved only a single vehicle, disregarding the fact that concur-rent interaction cooperative decision-making is a typical multi-agent system \(MAS\). Hence, it was logical to extend to a multi-agent reinforcement learning \(MARL\) framework. The decision at the intersection can be articulated as a fully cooperative MARL problem. MARL

has already been used for research in the field of intelligent transportation, such as traffic





Appl. Sci. **2023**, 13, 5018

4 of 19

signal control \[26\] and highway decision-making \[27\]. Decision-making at the intersection can be articulated as a fully cooperative MARL problem, for which very few works exist, even though it is still a new area of research \[21\]. Based on the model accelerated proximal policy optimization \(PPO\), Guan et al. \[28\] proposed a centralized coordination method to globally coordinate the CAVs approaching the intersection by considering their states altogether, which achieved an increased efficiency. Zhou et al. \[29\] applied a centralized control for all CAVs that shared the same learned controller and then enabled the CAVs to form an appropriate behavior using the deep deterministic policy gradient \(DDPG\) algorithm. Antonio et al. \[30\]

used MARL to identify complex real-life traffic scenarios and collaboratively regulate the CAVs at the intersection, which reduced 59% of the travel time and 95% of the congestion time compared to the traffic light control method. However, some issues in the MARL settings were not considered in the aforementioned works. The first issue was how to learn the most relevant information from other agents in a partially observable environment. The second was the reward assignment problem. In this study, we attempt to address the abovementioned issues by adopting a multi-agent reinforcement learning-based approach. 

**3. Problem Statement**

3.1. Scenario Description

The management of an unsignalized intersection is a challenging problem due to the multiple vehicles with potential conflicts and variable driving behavior. We focused on a traffic scenario at an intersection where the CAVs and HDVs coexisted and interacted with the surrounding vehicles to cross safely and efficiently. 

As shown in Figure 1, a typical single-lane four-way unsignalized intersection consisting of four entrances and four exits was introduced. The areas upstream of the entrances and downstream of the exits were combined with a straight lane of the distance Ls, where only a rear-end collision was possible since overtaking was not feasible. When the vehicle reached the end of the entrance lane, it reached the stop line, indicating that the vehicle was about to enter the intersection. Inside the intersection, there could be a head-on collision, a rear-end collision, or other hidden dangers. Suppose that a vehicle pre-plans a path p based on its initial lane and target lane before entering the intersection and follows this path to cross the intersection. Accordingly, there are 12 paths in total at the intersection, excluding the U-turn. 

There are a total of 20 conflicting points on these paths, including 16 crossing points and four converging points. The possibility of overtaking does not exist at the intersection, hence the diverging points are not the critical conflicting points. Assume that the preset path can be tracked perfectly by the vehicle, and thus only the longitudinal velocity along the path needs *Appl. Sci. ***2021**, *11*, x FOR PEER R

to b

EVIEW e adapted. Our objective was to select the actions about the acceleration 5 at

of ev

20 ery time step



for the CAVs to cross the intersection safely and efficiently. 

Exit Lane

Entrance Lane

Crossing 

points

Converging 

points

Path



**Figure 1. **Illustration of the considered single-lane four-way unsignalized intersection scenario. 

**Figure 1. **Illustration of the considered single-lane four-way unsignalized intersection scenario. 

*3.2. Right of Way Rules *

Human drivers mainly avoid crash conflicts by following the traffic rules at unsignalized intersections, which helps drivers determine how they should proceed to pass through successively, i.e., the right of way assignment. In this paper, the traffic rules in China were used to regulate the vehicles at the intersections. More specifically, each vehicle *i* that is about to enter the intersection should yield to the vehicle *j* that conforms to any of the following conditions \(in order of priority\): \(a\) vehicle *j* is already engaged in the intersection or significantly closer to the intersection; \(b\) vehicle *j* is on the right side of vehicle *i*; \(c\) vehicle *j* is proceeding straight and encounters the turning vehicle *i*; \(d\) vehicle *j* is about to turn and interacts with the vehicle *i* to turn right, when in the opposite direction. 

According to the aforementioned rules, if vehicle *i* goes before vehicle *j*, it means *i*

*j *. *psi,j* is used to represent the passage order. Thus, a priority state between these two vehicles can be defined as follows. 

1

 , *i*

*j*, 



*ps*

= −1, *i j*, 



*i*, *j*

\(1\) 

0,otherwise, 



If there is no potential collision risk between vehicles *i* and *j*, the two vehicles have the same priority, that is, the priority state is 0. 

*3.3. Vehicle Interaction Model *

In the considered scenario, the modeling of the CAV-to-CAV and the CAV-to-HDV 

interactions were developed in this paper. The CAVs equipped with V2X communication devices could exchange information, including the vehicle position, speed, acceleration, orientation, destination with the vehicles within the communication range, and road infrastructure, i.e., vehicle-to-vehicle \(V2V\) and vehicle-to-infrastructure \(V2I\) communication. Based on the road infrastructure, the HDVs’ state information could be observed and transferred to the CAVs \[31\]. Unlike the CAVs, the HDVs have the liberty to maneuver themselves under the premise of obeying the traffic regulations. However, they cannot send any acknowledgment of their interactions. In this paper, the HDVs were modeled as cautious drivers and they slowed in response to the dangerous movements of the vehicle ahead. The intelligent driver model \(IDM\), which imitates human driving behavior, was 

Appl. Sci. **2023**, 13, 5018

5 of 19

3.2. Right of Way Rules

Human drivers mainly avoid crash conflicts by following the traffic rules at unsignalized intersections, which helps drivers determine how they should proceed to pass through successively, i.e., the right of way assignment. In this paper, the traffic rules in China were used to regulate the vehicles at the intersections. More specifically, each vehicle i that is about to enter the intersection should yield to the vehicle j that conforms to any of the following conditions \(in order of priority\): \(a\) vehicle j is already engaged in the intersection or significantly closer to the intersection; \(b\) vehicle j is on the right side of vehicle i; \(c\) vehicle j is proceeding straight and encounters the turning vehicle i; \(d\) vehicle j is about to turn and interacts with the vehicle i to turn right, when in the opposite direction. 

According to the aforementioned rules, if vehicle i goes before vehicle j, it means i ≺ j. 

psi,j is used to represent the passage order. Thus, a priority state between these two vehicles can be defined as follows. 



1, i j, 



psi,j =

−1, i ≺ j, 

\(1\)



0, otherwise, 

If there is no potential collision risk between vehicles i and j, the two vehicles have the same priority, that is, the priority state is 0. 

3.3. Vehicle Interaction Model

In the considered scenario, the modeling of the CAV-to-CAV and the CAV-to-HDV

interactions were developed in this paper. The CAVs equipped with V2X communication devices could exchange information, including the vehicle position, speed, acceleration, orientation, destination with the vehicles within the communication range, and road infrastructure, i.e., vehicle-to-vehicle \(V2V\) and vehicle-to-infrastructure \(V2I\) communication. 

Based on the road infrastructure, the HDVs’ state information could be observed and transferred to the CAVs \[31\]. Unlike the CAVs, the HDVs have the liberty to maneuver themselves under the premise of obeying the traffic regulations. However, they cannot send any acknowledgment of their interactions. In this paper, the HDVs were modeled as cautious drivers and they slowed in response to the dangerous movements of the vehicle ahead. The intelligent driver model \(IDM\), which imitates human driving behavior, was used to control the HDVs. Consequently, the acceleration of an HDV could be anticipated based on its current speed and headway distance. 

**4. Cooperative Decision-Making in a Multi-Vehicle Cooperative Task** 4.1. Problem Formulation

In this paper, the unsignalized intersection environment, where the CAVs and HDVs coexist, was modeled as a model-free multi-agent system to solve the cooperative decision-making and control problems. 

The system was described as G = \(V, E\), where

V = \{v1, v2, . . . , vN\} represents a non-empty finite with N CAVs and the edge set E ⊆ V × V represents the connections among the CAVs. The CAVi makes decisions based on its observations of the local sensors, such as cameras and lidars, and its commu-

. 

nication with its neighbors, denoted as Ni = j *ε* i,j ∈ E, i 6= j , to enhance the range of perception. Considering that the decisions of N CAVs are interactive, the problem was considered a fully cooperative multi-agent task, which was modeled as a partially observed Markov decision process \(POMDP\). For the POMDP, each agent received a partial observation oi ∈ Oi from the global state s ∈ S. Based on the observation, the agents took joint

. 

action, a1, a2, · · · , aN ∈ A from the action set A = ×i∈V Ai to interact with the environment and receive a reward from all the agents R = \{r

N

1, r2, . . . , rN \} : S × A1 × . . . AN → R . The

goal was that the agents would attempt to learn an optimal joint policy *π* i : Oi → Ai to h

i

maximize the expected return G =

t

E ∑T

t=0 *γ * rit

in the interaction with the environment, 

where *γ *∈ \(0, 1\] is the accumulated discount factor to quantify the importance of the





*Appl. Sci. ***2021**, *11*, x FOR PEER REVIEW 

6 of 20 



used to control the HDVs. Consequently, the acceleration of an HDV could be anticipated based on its current speed and headway distance. 

**4. Cooperative Decision-Making in a Multi-Vehicle Cooperative Task** *4.1. Problem Formulation *

In this paper, the unsignalized intersection environment, where the CAVs and HDVs coexist, was modeled as a model-free multi-agent system to solve the cooperative decision-making and control problems. The system was described as *G *= \( *V *, *E*\), where *V *= \{ *v *, *v *, 

, *v *\} represents a non-empty finite with *N * CAVs and the edge set *E * *V V*

 

1

2

*N*

represents the connections among the CAVs. The CAV *i* makes decisions based on its observations of the local sensors, such as cameras and lidars, and its communication with its neighbors, denoted as *N*

\{ *j *|   , 

*E i * \}

*j *, to enhance the range of perception. Consid-

*i*

*i*, *j*

ering that the decisions of *N* CAVs are interactive, the problem was considered a fully cooperative multi-agent task, which was modeled as a partially observed Markov decision process \(POMDP\). For the POMDP, each agent received a partial observation *o * *O * from *i*

*i*

the global state *s * *S *. Based on the observation, the agents took joint action, *a *, *a *, 

, *a * *A * from the action set *A*

 *A * to interact with the environment and re-

1

2

*N*

*i V*



*i*

ceive a reward from all the agents *R *= \{ *r *, *r *, 

, *r *\}:

*N*

*S * *A *

*A *→

. The goal was that 

1

2

*N*

1

*N*

the agents would attempt to learn an optimal joint policy  : *O *→ *A * to maximize the *i*

*i*

*i*

Appl. Sci. **2023**, 13, 5018

*T*

*t*

*i*

= 



6 of 19

expected return *G*

  *r * in the interaction with the environment, where 

=0

*t*

*t*





 \(0,1\] is the accumulated discount factor to quantify the importance of the future reward and T denotes the total steps of an episode. It can be defined by a tuple future reward and T denotes the total steps of an episode. It can be defined by a tuple \( *S*, , 

*A*

, 

*P*

, 

*R*

, 

*O N*, \), where *P * denotes a state transition function. 

\(S, A, P, R, O, N, *γ*\), where P denotes a state transition function. 

Action: In this paper

Act , the

ion: In contr

this ol system

paper, the of

c the vehicle

ontrol systemwas

of t split

he 

into

veh

two

icle wa levels, 

s split the

into two levels, the 

high-level decision-making

high-level and

de

the

cision- low-level

making contr

and th oller

e 

, 

low as

-

depicted

level c

in

ontro

Figur

ller, as e

d 2. Accor

epicted ding

in Figure 2. Accord-

to the local observation, 

ing to the the

loc high-level

al observat decision-making

ion, the high-level selected

decision- an

m action

aking se in the

lected action

an action in the action 

space A

space *A * defined as *A * = \{ *hard acceleration, acceleration, idle, deceleration and hard decelera-i defined as Ai = i \{hard acceleration, *
* 
i

acceleration, idle, deceleration and hard deceleration\}. 

Then, based on the decision

tion\}. Then, taken, 

based the

on lower

the d level

ecis

contr

ion 

olle

taken, t r, i.e., 

he 

a PID

lower le contr

vel 

oller

contro, generated

ller, i.e., a PID controller, 

the corresponding throttle

generated signals

the

to maneuver

corresponding t the

hrottl CA

e si V. 

gnals to maneuver the CAV. 

Local sensors

**V2V**

Information including 

position, speed.. 

**V2I**

High level decision-

making

Action

**δ**

Low-level controller

**a**

Control signals

CAVs \(Within the communication range\)

CAV



**Figure 2. **

**Figure **

Schematic

**2. **Sc

diagramhem

of ati

the c diagram

decision of the 

control dec

for ision contr

multiple ol for mu

intelligent ltiple intel

vehicles. ligent vehicles. 

Observation:

Ob

The servation: Th

observation oe 

i

ob

of serv

the ation 

vehicle o vi of the veh

included

icl

the e v  include

information d

r the 

equir in

ed formation re-

i

i

to make

quired 

decisions eff to make 

ectively. deci

It

sions 

was

effective

assumed

ly. 

that It wa

each s assumed 

vehicle

tha

couldt each 

senseveh

its icle 

stat ceould

and sense its state 

exchange

and exch

information

an

with ge

its information

neighbors, with

which its

is neighbo

denoted rs, 

as wh

Ni. ich 

The is denoted

neighbors as 

of a N . The 

vehicle neighbors of 

i

were defined as the vehicles that were within L

a vehicle were defined as the veh

c meters and with the potential of a collision, 

icles that were within L  meters and with the potential c

i.e., a different priority on their respective routes. The observation oi was defined as a matrix of a collision, i.e., a different priority on their respective routes. The observation o  was i

of b × W, where b denotes the upper bound of the number of its neighbors and W is the number of features ci representing the state of a vehicle. Specifically, the observation feature is defined as ci = \[ispresent, x, y, vx, vy, h, ps\]T, where ispresent is a binary flag denoting whether a vehicle can be observable. x, y, vx, vy represent the absolute longitudinal position, the lateral position, the longitudinal speed, and the lateral speed for the ego vehicle, while the relative to the ego vehicle for observed vehicles; h denotes the heading; and ps represents the priority of crossing the intersection. The entire state of the system is the Cartesian product of the individual observation, that is, S = O1 × O2 × · · · × ON.. 

Reward: The basic goals of a vehicle at the intersection include driving safely, crossing the intersection, and reaching its target lane under the right of way rules and in a timely manner. Several rewards are specified as follows. 

\(a\)

The occurrence of a collision is detected by the body circle model. It reduces the vehicle to a circle with the center of the vehicle as the center and the diagonal of the vehicle as the diameter. When two vehicles are tangent to each other, a collision is considered to have occurred. The collision reward rc is defined to penalize the occurrence of a collision and reward the successful pass, expressed as follows. 



−1, if a collision happens, 



rc =

1, if all CAVs pass successful, 

\(2\)



0, otherwise

\(b\)

For safety, the vehicle is penalized when the minimum time headway th with other vehicles is less than desired time headway td. In this paper, td was set to 2 s. Our study scenario was a mixed traffic scenario where the HDVs and CAVs coexisted. The uncertain behavior of the HDVs prevented us from directly calculating the time to

Appl. Sci. **2023**, 13, 5018

7 of 19

collision \(TTC\). Therefore, within a prediction horizon Th, all the vehicles’ trajectories are predicted. The trajectories of the CAVs are predicted via the execution of the current action, while the HDVs are estimated from the IDM model. At each step of the prediction, the collision of vehicle i is detected according to the body circle model. If a collision occurs at step t, the time headway th is determined according to th = t/ f , where f represents the control frequency of the vehicle. When no collisions are detected, rh is set to 1. Thus, the headway reward rh is defined as follows. 

\(

ln th , if collisions are detected, 

r

t

h =

d

. 

\(3\)

1, otherwise

\(c\)

To pass though the intersection safely and effectively, the speed should be considered as appropriate and is punished too low. The speed reward is defined as follows. 



v



r

t − vmin

s = min

, 1 , 

\(4\)

vmax − vmin

where vt, vmin, vmax are the current speed and the minimum and maximum speeds to be rewarded. 

\(d\)

For the vehicle to make decisions under the rules demonstrated in Section 3.2 the rule reward rr is set to 1 if the rule is obeyed, otherwise rr = −1. 

Based on these definitions above, the total reward for the vi at time step t is defined as follows. 

rit = ω crc \+ ω hrh \+ ω srs \+ ω rrr, \(5\)

where ω c, ω s, ω h, and ω r are all weighting factors that account for each part of the reward. 

4.2. Wighted Reward Assignment

In the fully cooperative MARL setting, each agent was provided with the same goal and assigned the same reward after executing the action at every step. The same reward can be represented by the average global reward as rt = 1 ∑N

N

i=1 ri,t. However, the shared

rewards scheme is intricate in order to infer each vehicle’s contributions to the system cooperation. Further, instead of embracing a global reward, a local reward assignment strategy could alleviate the issue of the credit assignment problem. Specifically, each host vehicle only focuses on its surrounding vehicles, which considerably impacts the smooth interaction between the vehicles. Thus, the reward for the ego vehicle vi at the step t is defined as follows. 

1

ri,t =

∑ r

|T

j∈T

j,t, 

\(6\)

i |

i

where Ti = i ∪ Ni is a set whose elements include the ego vehicle vi and its neighbor vehicles and |·| represents the cardinality operator of the set. The local reward assignment has two advantages. First, the communication burden can be reduced by focusing only on the nearby vehicles, establishing a more real-time system. Second, the contribution of the vehicles to their cooperation can be indicated more accurately. 

Nevertheless, the regional reward assignment strategy still doesn’t accurately differ-entiate between the contributions of each ego vehicle at different positions on the road. 

Collisions are more likely to occur inside the intersection than outside it, meaning that a vehicle closer to the intersection should be assigned more rewards, i.e., a weighted reward assignment according to the vehicle’s position. A weight factor η  was defined to measure the contribution for crossing the intersection safely and efficiently, as shown in Equation \(7\). 

Ls − di

η i =

, 

\(7\)

∑j∈T \(L

i

s − dj\)

where di denotes the distance from the vehicle vi not entering the intersection to the entrance or from vi not exiting the intersection to the exit, and Ls is the length of the entrance or exit





Appl. Sci. **2023**, 13, 5018

8 of 19

straight lane. When vi enters the intersection, di = 0. Thus, the reward for the ego vehicle vi at the step t is as follows. 

ri,t = ∑j∈T η irj,t. 

\(8\)

i

When a vehicle and its neighbors are in the intersection, Equation \(8\) will degenerate to the local reward assignment strategy, i.e., Equation \(6\). 

4.3. Cooperative Learning Algorithm for Multi-Agent Task

The MARL method was leveraged to deal with the unsignalized intersection management due to the fact that it could produce an optimal policy through a continuous interaction with the traffic environment. A cooperative PPO-based decision-making method Appl. Sci. **2021**, 11, x FOR PEER R

\(Attn-MAPPO\)

EVIEW 

is proposed in this section, as shown in Figure 3. The algorithm was based 9 of 20 



on a centralized training decentralized execution \(CTDE\) framework to reduce the environmental instability; that is, all the information of the agents was utilized during training and the

t

agents

raining 

only

and th made

e agen decisions

ts only ma accor

de d ding

ecisi to

ons their own

according local

to theobservation

ir own local after

ob

the

serv

training. 

ation after 

Specifically

the train

, after

ing. 

choosing

Specifically, the

afteractions

choos from

ing t the

he policy

actions fto inte

rom t ract

he with

policy the

to envir

inter onment, 

act with t all

he 

the

env vehicles

ironmen executed

t, all the them

veh

and

icles 

reached

executed th a new

em 

stat

and 

e. 

reac Based

hed a non the

ew s

new

tate. B observation, 

ased on the an

new 

attention

observat module

ion, an 

was

atten used

tion 

to

mo aggr

dule egate

was 

the

used t information

o aggregate tfrom

he 

the

infor neighbors

mation 

of

from t a vehicle. 

he neigh-

Then, 

bors the

of a output

vehicle. of

T the

hen, module

the out was

put used

of the to update

module the

was critic

used t network. 

o update The

the ccritic

ritic net

net work

work. 

evaluated

The critic the taken

netw

actions

ork evaluate and

d th the

e takagent

en 

network

actions and was updated. 

the agent network was updated. 

Vehicle i

Vehicle j

\(Neighbor of vehicle i \)

ai

aj

Actor

Env

Actor

ci

cj

oi

Attention module

mi

Vi\(o\)

Critic



**Figure **

**Figure3. **

**3. **The f

The ramework 

frameworkof 

ofthe propos

the pr

ed 

oposedAttn-MAPPO 

Attn-MAPPO algorithm. 

algorithm. 

In this paper, each vehicle could observe its neighbors and collect their state infor-In this paper, each vehicle could observe its neighbors and collect their state information to make decisions. Although the relevant vehicle was selected as the focus, the mation to make decisions. Although the relevant vehicle was selected as the focus, the aggregated information was not the most valuable information. For example, the state aggregated information was not the most valuable information. For example, the state information of the neighbors which were more likely to collide required more attention. 

information of the neighbors which were more likely to collide required more attention. 

The attention mechanism was introduced in this paper to selectively pay attention to the The attention mechanism was introduced in this paper to selectively pay attention to the neighbors’ observations. 

neighbors’ observations. 

More specifically, the structure of the attention representation is defined as Figure 4. 

More specifically, the structure of the attention representation is defined as Figure 4. 

The relevant message from other vehicles, mi

The relevant message from other vehicles,t, is summed by assigning the attention weights i

m , is summed by assigning the attention 

t

to the embedding of each agent, which is mathematically expressed as the following. 

weights to the embedding of each agent, which is mathematically expressed as the following. 

i

j

mi

,j

t = ∑j6=i α t Wvet, 

\(9\)

i

i, j

j

m =

j

  W e , 

t

t

v t

\(9\) 

j  i

where e =

\)

t

fj\(oit is the embedding where a multi-layer perceptron \(MLP\) fj\(·\) is used as where j

j

the

e = f \( i

o

embedding \) is the 

functionembedding 

and W

where a multi-layer perceptron \(MLP\) f \( \)

 is used 

t

j

t

v is a matrix to linearly transform e

j

t into a “value”. The

as the embedding function and W  is a matrix to linearly transform j e  into a “value”. 

v

t

The attention weight 

i, j
*
* between the vehicles i and j was calculated using a softmax funct*

tion, as shown in the following. 

*i*, 

exp\(

*j*

 \)

*i*, *j*

*t*

 =

, 

*t*

*i*, 





\(10\) 

exp\(

*j*

 \)

*t*

*j * *i*

*i*, *j*

*i*

 = *W e *\(

*j*

*W e *\) *T *, 

*t*

*q t*

*k t*

\(11\) 

where 

*i*, *j*

 computes the correlation between the vehicles *i* and *j*, the matrix *W * linearly *t*

*q*

transforms *i*

*e * into a “query”, and *W * transforms *j* *e * into a “key”. 

*t*

*k*

*t*





Appl. Sci. **2023**, 13, 5018

9 of 19

i,j

attention weight *α* t between the vehicles i and j was calculated using a softmax function, as shown in the following. 

i,j

i,j

exp\( *β *\)

t

*α*

=

t

, 

\(10\)

∑

i,j

j6=i exp\( *β*

\)

t

i,j

j T

*β*

=

\)

t

Wqeit · \(Wket , 

\(11\)

*Appl. Sci. ***2021**, *11*, x FOR PEER REVIEW 

i,j

where

10 of 20 



*β* t computes the correlation between the vehicles i and j, the matrix Wq linearly j

transforms eit into a “query”, and Wk transforms et into a “key”. 

*mi*

\+ 

×

×

Softmax



*βi1*

*βij*



*q*

*ki* 1

*v*

*i*

*i* 1

*kij*

*vij*

*WK*

*WV*

*W*

*W*

*K*

*WV*

*Q*



Embedding

*f*

Neighbors of 

*i*

*f*

*f*

*i, * 1

*i,j*

vehiclei

Observation *oi*

*ci*

*cj*



**Figure 4. **

**Figure **Flow

**4. **

charts of

Flowcharts the at

of the tention represe

attention repr ntation. 

esentation. 

In t

In he coo

the

perative m

cooperative ulti-agent 

multi-agent setting, 

setting, each 

each agent 

agent shar

shar ed

ed an

an actor

actor network

network \(i.e

\(i.e.,., pol-

policy\)

icy\) and 

and a a cri

critictic networ

network k \(i.e. 

\(i.e., , policy 

policy evaluati

evalu

on\), 

ation\), which 

which were 

were trained 

trained using 

usingthe in

the dividual 

individual

trajectory 

trajectory \(\( *i*

*o* oi, *i*

\)

t, *a* ai, *i*

t, *r* ri\)

t .. The 

The actor

actor network 

network

wa

was s trained

trained 

to to maximize

maximize



the the expected

expected r

ret

eturn.urn. 

Each

*t*

*t*

*t*

agent generated its action ai

based on its local observations oi

Each agen



t generated its action

t from the policy *π*

*i*

*a * from the policy

*θ *  based on its local observationst \(i.e., 

*i*

*o * 

*t*



*t*

*π*\(atioit; *θ*\) at the time slot t. The most valuable information which an attention representa-

\(i.e.,  \( *t*

*a *| *i*

*o *;\)

tion aggr



egated at 

fr the

om time 

the

slot *t*. T

neighborshe

of mo

an st valuabl

agent was e inform

access ation

to the which

input 

ofan at

the tenti

critic on rep-

*i*

*t*

network. 

resen

An tation aggreg

episodic

ate

setting d fro

was m the neig

consider hb

ed ors o

with f an 

eachagent wa

vehicle s acces

until a s to the

crash input

occurr of 

ed the 

or critic 

until it

network

pr

. An

oceeded episod

T

ic s

seconds. ettin

Our g was con

objective sidered 

was to

with 

obtain each 

the

vehicl

optimale until 

joint

a cras

policy h o

thatccurred or 

maximized

until

the it proceeded

accumulated r *T* secon

eward. ds. Our objective was to obtain the optimal joint policy that maximize

Thed the a

PPO ccumulate

algorithm d rew

based ard. 

on 

the actor–critic framework was an improvement of the

Th

policy e PPO alg

gradient orithm

\(PG\)

based o

algorithm. n the a

The

ctor–cr

objectiveitic 

f

framewor

unction of

k 

the was

PG an improv

algorithm emen

is

t

expr of th

essed e 

as

policy 

the

gradient 

following. \(PG\) algorithm. The objective function of the PG algorithm is expressed as the following. 

∇J\( *θ*\) = E



\(s

\[∇ log *π *\(a s

\(s

t,ot \)∼ *π*

*θ*

*θ*

t

t\)A *π*

t, at\)\], 

\(12\)

*θ*



*θ*

*J*

 \(\) =

\[ log \( *a *| *s *\) *A *\( *s *, *a *\) , 

\] 

where

\( *s *, *o *\)~



\(12\) 

*t*

*t*

*t*

*t*

*t*

*t*







A \(st, at\) = Q \(st, at\) − V \(st\)

\(13\)

where 

*πθ*

*πθ*

*φ*

is an estimation of the advantage function at the step t and *θ*, *φ * are the parameters for *A *\( *s *, *a *\) = *Q *\( *s *, *a *\) − *V *\( *s *\)





*t*

*t*



*t*

*t*



*t*





\(13\) 

identifying the policy and state value functions, respectively. 

By modifying the objective, the PPO constructs a clipped surrogate objective function is an estimation of the advantage function at the step *t* and  , are the parameters for to confine the policy updates to a small scope of around 1. The objective and update identifying the policy and state value functions, respectively. 

functions are illustrated as the following. 

By modifying the objective, the PPO constructs a clipped surrogate objective function to confine the policy updates to a small scope of aroun

\[ d 1. 

i The objective and update func-

JPPO\( *θ*\) = E

, Ai

\(oi

\)∼

*ψ*\( *ρ*

*π*

*θ*

t\)\], 

\(14\)

tions are illustrated as the following. 

t,ait

*θ* old

*PPO*

*J*

\( \)

*i*

*i*

=

  *A*



*i*

*i*

\[ \(

, 

\)\], 

\( *o *, *a *\)~



*t*

\(14\) 

*t*

*t*

*o*

 *ld*

*PPO*

 = \+ *l* *J*

\(\), 

\(15\) 

*t * 1

\+

*t*



 \( *i*

*a *| *i*

*o *\)

where *l* is the learning rate and *i*



*t*

*t*

 =



specifies the probability ratio of the old 

 \( *i*

*a *| *i*

*o *\)

 *old*

*t*

*t*

and new policies to select the action and 

\( *i*

 , *i*

*A *\) = min\( *i i*

 *A *,clip\( *i*

 ,1−,1\+\) *i*

*A *\), 





\(16\) 

*t*

 *t*



*t*

Appl. Sci. **2023**, 13, 5018

10 of 19

*θ* t\+1 = *θ* t \+ l∇ JPPO\(

*θ*

*θ*\), 

\(15\)

\(ai |oi \)

where l is the learning rate and i

t

t

*ρ *=

*πθ*



specifies the probability ratio of the old and

*θ*

*π*

\(ai oi \)

*θ* old

t t

new policies to select the action and

i

i

i

*ψ*\( *ρ *, Ai

Ai

, 1 − *ε*, 1 \+ *ε*\)Ai

*θ*

t\) = min\( *ρθ*

t, clip\( *ρθ*

t\), 

\(16\)

where *ε * is the penalty factor to prevent the policy from changing extremely. When A ≥ 0, the return for taking the action ait is greater than the expected observation oit. Therefore, the updated policy should increase the probability of the action, but the increase amplitude should be restrained to \(1 \+



*ε*\) *π*

\(ai

\) . The opposite is true when A < 0. 

*θ*

oi

old

t

t

To decrease the variance, the advantage function A

in Equation \(13\) is replaced by

*πθ*

the generalized advantage estimation \(GAE\), which is expressed as the following. 

Âi

i

i

t = *δ* t \+ ∑T

\(

l=t\+1 *γλ*\)l−t *δ* l , 

\(17\)

where i

*δ *\(

\+

\(

\) −

\( \)

t *γ*\) = rit

*γ* V

oi

V oi is the TD error and

*φ*

t\+1

*φ*

t

*λ * is a factor that balances the

variance and bias of the estimation. When *λ *= 0, Âi =

\+

\(

\) −

\( \)

t

rit

*γ* V

oi

V oi , which is

*φ*

t\+1

*φ*

t

unbiased with a high variance. The GAE achieves both a low bias and a low variance by linearly integrating the n-step bootstrapping. The critic network V \(·\) is updated using the *φ*

loss function as follows. 

2

J\( *φ*\) = minE

\[ri

\(oi

\) − V \(oi

, 

\(18\)

\(oi

\)∼

t \+ *γ* V *φ*

t\+1

*φ*

t\)\]

t,ait

*πθ* old

*φ* t\+1 = *φ* t \+ l∇ J\(

*φ*

*φ*\). 

\(19\)

The whole pseudo-code for the proposed method is presented in Algorithm 1. 

**Algorithm 1**: Attn-MAPPO

1: Initialize the actor network and target the actor network using the parameters

−

*θ * and *θ *; 

2: Initialize the critic network and target the critic network using the parameters

−

*φ * and *φ *; 

3: Initialize the memory buffer Di and hyper-parameters lr, *τ*, *e*. 

4: **for **episode = 1, . . . , M **do**

5:

**for **t ≤ T and not terminal **do**

6:

**for **i ∈ V **do**

7:

Observe oi and select an action ai ∼ *π *− using the -greedy strategy. 

*θ*

8:

All agents execute the actions and receive their own reward ri. 

9:

Store trajectories \(oi, ai, ri\) in Di. 

10:

**end for**

11:

**for **i ∈ V **do**

12:

Obtain the attention representation of each agent using Equation \(9\). 

13:

Update the critic network *θ * and the actor network *θ * using a randomly sampled mini batch from Di in Equations \(15\) and \(19\), respectively. 

14:

Update the target networks: −

−

−

−

*φ*

= *τφ *\+ \(1 − *τ*\) *φ *, *θ*

= *τθ *\+ \(1 − *τ*\) *θ *. 

15:

**end for**

16:

**end for**

17:

Initialize Di ← ∅, and reset the environment. 

18: **end for**

**5. Results and Discussion**

In this section, the proposed Attn-MAPPO algorithm was evaluated at the unsignalized intersection on an open source platform, called highway-env \[32\]. A total of 30 episodes of the evaluation for each contrast were executed using 30 various seeds. Two metrics were used for the performance of the algorithm, namely the collision rate and the average



*Appl. Sci. ***2021**, *11*, x FOR PEER REVIEW 

12 of 20 



In this section, the proposed Attn-MAPPO algorithm was evaluated at the unsignalized intersection on an open source platform, called highway-env \[32\]. A total of 30 episodes of the evaluation for each contrast were executed using 30 various seeds. Two metrics were used for the performance of the algorithm, namely the collision rate and the average speed. The collision rate was defined as the ratio of the number of episodes where the collision occurred to the total number of the test episodes. The average speed was defined as the average speed of all the vehicles in all the episodes. In the scenario, a straight lane had a distance of *Ls* = 200 m, the right turn radius was 9 m , and the left turn radius was 13 m. The vehicle’s policy frequency was set to 5 Hz, i.e., the CAVs took an action every 0.2 s. The speed range of receiving a reward was \[8,10\] m/s. For the actions, the normal acceleration and deceleration were to add or subtract 1.5 m/s from the current speed, as the desired speed and the hard were 3 m/s. The PID algorithm was used as the low-level controller to change the current speed to the expected speed. To avoid the ex-Appl. Sci. **2023**, 13, 5018

11 of 19

cessive speed, the maximum speed of CAVs was set to 10 m/s. The HDVs’ desired speed was set to 10 m/s. The communication range *Lc* was set to 120 m *. * The setting of the training speed. The

process was collision rate

presented was

as defined as the ratio

follows. The 

of the

model number

was of episodes

evaluated wher

eve e

r the

y 20 episodes during the 

collision occurred to the total number of the test episodes. The average speed was defined training. ADAM was used as the optimizer and the learning rate was set to 8 × 10−5. The as the average speed of all the vehicles in all the episodes. In the scenario, a straight lane soft had a distance

update we of L

ighting factor *τ* was set to 0.001. The trade-off coefficient of the GAE λ was s = 200 m, the right turn radius was 9 m, and the left turn radius was 13 m. The vehicle’s policy frequency was set to 5 Hz, i.e., the CAVs took an action every set to 0.95 and the discounting factor was set to 0.99. 

0.2 s. The speed range of receiving a reward was \[8,10\] m/s. For the actions, the normal acceleration and deceleration were to add or subtract 1.5 m/s from the current speed, as *5.1. * the desired speed

*Performanc*

and

*e Com* the

*p * hard wer

*arison*

e 3 m/s. 

* between * The

*the * PID

*Pr * algorithm

*oposed*

was used as the low-level

* Attn-MAPPO Algorithm and *

controller to change the current speed to the expected speed. To avoid the excessive speed, *the Benchmark *

the maximum speed of CAVs was set to 10 m/s. The HDVs’ desired speed was set to 10 m/s. The communication range Lc was set to 120 m. The setting of the training process In this subsection, we compared the proposed Attn-MAPPO approach with the was presented as follows. The model was evaluated every 20 episodes during the training. 

ADAM was

MAPPO be used

nchm as the

arks\[ optimizer

13\]. Th and the

e archi learning

tectu rate

re w was

as set to

the s 8

a ×

me10−5. 

for The

bo soft

th, but the Attn-MAPPO 

update weighting factor *τ * was set to 0.001. The trade-off coefficient of the GAE λ was set to used an attention mechanism to extract the most valuable information as the input for the 0.95 and the discounting factor was set to 0.99. 

network. To validate the performance of the proposed Attn-MAPPO algorithm, two traffic 5.1. Performance Comparison between the Proposed Attn-MAPPO Algorithm and the Benchmark scenarios were set up with \(1\) two CAVs and three HDVs, and \(2\) four CAVs and five In this subsection, we compared the proposed Attn-MAPPO approach with the HDVs. The first setting was simple due to the sparse traffic density, while the second was MAPPO benchmarks \[13\]. The architecture was the same for both, but the Attn-MAPPO

used an attention

complex. The

mechanism

compar

to

ison extract

resu the

lt

most

s of valuable

the

information

episode rew as

a the

rd input

in th for

e the

training is illustrated in 

network. To validate the performance of the proposed Attn-MAPPO algorithm, two traffic Figure 5. The results showed that in the simple setting, namely with the two CAVs, three scenarios were set up with \(1\) two CAVs and three HDVs, and \(2\) four CAVs and five HDVs. 

The

HDVs, first

bo setting

th th was

e 

simple

algori due

thmsto the

pe sparse

rform traf

ed fic

c density

omp , while

arablythe

b second

ut mo was

dercomplex. 

ately better than the bench-

ma The

rk comparison

. Yet, as th results

e nu of the episode

mber of

rewar

vehicl d in

es inthe training

crea

is illustrated in Figure 5. The

sed, the benchmark performance declined sig-results showed that in the simple setting, namely with the two CAVs, three HDVs, both nificantly and the Attn-MAPPO algorithm showed a stronger performance. In the 30 tests, the algorithms performed comparably but moderately better than the benchmark. Yet, as the number

one collision of

vehicles incr

occurred eased, 

usin the

g th benchmark

e propos performance

ed metho declined

d an

significantly

d four col and

lisions occurred using the 

the Attn-MAPPO algorithm showed a stronger performance. In the 30 tests, one collision benchmark in the complex setting. Table 1 shows that for the proposed algorithm, the occurred using the proposed method and four collisions occurred using the benchmark coll in the

ision complex

rate 

setting. Table

could be con1s shows

ider that for

ably di the

mi proposed

nished algorithm, 

in the 

the collision

complex tr rate

affic setting. This implies 

could be considerably diminished in the complex traffic setting. This implies that the added that the added attention module was able to extract the critical information for decision-attention module was able to extract the critical information for decision-making, whereas the

makin benchmark

g, wher did not

eas th have this

e benc capability

hmark . 

did not have this capability. 



**Figure 5. **

**Figure**Comparison of

**5. **Comparison of the the 

ep

episode

isode reward rewar

in the

d in

training

the 

between trainin

the

g between the 

benchmark and the pr

benchmark and the

oposed

pro-

Attn-MAPPO \(proposed\) algorithm. 

posed Attn-MAPPO \(proposed\) algorithm. 





*Appl. Sci. ***2021**, *11*, x FOR PEER REVIEW 

13 of 20 



Appl. Sci. **2023**, 13, 5018

12 of 19

**Table 1. **Performance comparison between the benchmark and the proposed Attn-MAPPO \(proposed\) algorithm. 

**Table 1. **

Performance comparison between the benchmark and the proposed Attn-MAPPO

**Algorithm and Settings **

\(proposed\) algorithm. 

**Metrics **

**Benchmark **

**Benchmark **

**Attn-MAPPO **

**Attn-MAPPO **

**\+2C3Algorithm**

**H **

**and Settings**

**\+4C5H **

**\+2C3H **

**\+4C5H **

**Metrics**

Collision 

rate 

0 0.13 0 0.03 

**Benchmark \+2C3H**

**Benchmark \+4C5H**

**Attn-MAPPO \+2C3H**

**Attn-MAPPO \+4C5H**

Average speed 

Collision rate

0

0.13

10.08 8.77

0

9.91

0.03

8.95 

\(m/s\) 

Average speed \(m/s\)

10.08

8.77

9.91

8.95

*5.2. Performance of the Proposed Reward Scheme Designs *

5.2. Performance of the Proposed Reward Scheme Designs

In this paper, the setting of the reward mechanism had two main aspects. The first In

was this

th

paper

e design , the

of

setting

the rewa of

rd the r

func ewar

tion d

an mechanism

d the secon had

d wa two

s themain

de

aspects. 

sign of the The

re

first

ward as-

was the design

signment scheof the

me. 

reward function and the second was the design of the reward

assignment scheme. 

There were four components in the reward function, including the collision evalua-Ther

tion, 

e

he wer

adw e

a four

y eva components

luation, sp in the

eed ev r

al ewar

uati d function, 

on, and ru including

le evaluati the collision

on. In order evaluation, 

to validate the 

headway

effect

evaluation, 

iveness of the speed

reward evaluation, 

function 

and

for 

r

decisule

i

evaluation. 

on-making, we In

se or

t u der

p 

to

an in validate the

tersection cross-

effectiveness

ing scenar of the

io. 

reward function

There were 

for de

three vehicl cision-making, 

es in this scenarwe set up

io, wher an intersection

e one HDV 

crossing

shown in blue 

scenario. 

was

Ther

going e

str wer

aighe

t thr

an ee

d vehicles

two CAVs in this

shownscenario, 

in gree

wher

n were e

tuone

rn HDV

ing left, shown

deno

in

ted ablue

s CA was

V1 and 

going straight

CAV2, re

and

spec

two

tive

CAVs

ly. In ord shown

e

in

r to pres green

ent th were

e spatturning

ial relat left, 

i

denoted

onship of th as CAV1

e vehicle and

s m CA

o

V

re in2, 

tui-

respectively

tively, 

. In

the p or

osider to pr

tions of esent

the v the

e

spatial

hicles

relationship

were represen of

ted the

by vehicles

the dist mor

an

e intuitively

ce from the st , the

op line 

positions of the vehicles were represented by the distance from the stop line along their path, along their path, rather than their world coordinates. The positions were negative when rather than their world coordinates. The positions were negative when the vehicles crossed the vehicles crossed the stop line. The position and speed curves of all the vehicles during the stop line. The position and speed curves of all the vehicles during the whole process the whole process are shown in Figure 6. Figure 7 shows a sequence of the time slices for are shown in Figure 6. Figure 7 shows a sequence of the time slices for demonstrating the demonstrating the inter-vehicle interaction. Apparently, all the vehicles crossed through inter-vehicle interaction. Apparently, all the vehicles crossed through the conflict zone the conflict zone safely. As shown in Figure 6a, when there was no interaction between safely. As shown in Figure 6a, when there was no interaction between vehicles, they could vehicles, they could accelerate to the maximum speed of 10m/s to obtain a higher reward. 

accelerate to the maximum speed of 10m/s to obtain a higher reward. In accordance with In accordance with the traffic rules introduced in Section 3.2, the vehicle going straight the traffic rules introduced in Section 3.2, the vehicle going straight goes first, and the one goes first, and the one on the right has the right of way. Thereby, the passage sequence of on the right has the right of way. Thereby, the passage sequence of the three vehicles was the three vehicles was HDV, CAV1, and CAV2, which was exactly what is shown in Figure HDV, CAV1, and CAV2, which was exactly what is shown in Figure 7. There were two 7. There were two interactions during the crossing. CAV1 and the HDV first interacted in interactions during the crossing. CAV1 and the HDV first interacted in the same lane, where the same lane, where CAV1 slowed down and pulled away from the HDV ahead of it. The CAV1 slowed down and pulled away from the HDV ahead of it. The second interaction second interaction took place between the two CAVs. Since CAV2 should have crossed took place between the two CAVs. Since CAV2 should have crossed later than CAV1, CAV2

later than CAV1, CAV2 decelerated to make way at 12.4 s. All the above analyses demon-decelerated to make way at 12.4 s. All the above analyses demonstrated that the designed strated that the designed reward function was qualified for the effective decision-making reward function was qualified for the effective decision-making for the CAVs. 

for the CAVs. 



**Figure 6. **

**Figure 6. **

The

The

speed and

speed and

position curves of

position curves of al

all l th

the e vehicle

vehicles s during

during the whole cro

the whole cr

ssing

ossing; \( ; \(

**a**\) **a**\) th

the e spee

speed,d, 

\(**b **\(\)**b**\) the po

the

sition. 

position. 



*Appl. Sci. ***2021**, *11*, x FOR PEER REVIEW 

14 of 20 

Appl. Sci. **2023**, 13, 5018

13 of 19





**Figure 7. **The frames of the time slices showing the interactions performed by the simulation platform **Figure 7. **The frames of the time slices showing the interactions performed by the simulation plat-

\(blue: HDV; green: CAVs\); \(**a**\) 9 s, \(**b**\) 12 s, \(**c**\) 15 s, and \(**d**\) 18 s. 

form \(blue: HDV; green: CAVs\); \(**a**\) 9 s, \(**b**\) 12 s, \(**c**\) 15 s, and \(**d**\) 18 s. 

To validate the performance of the proposed reward assignment scheme, the global To validate 

reward, local the perform

reward, and the an

pr ce of 

oposed the prop

weighted os

r

ed rew

eward

ar

schemed assignment scheme, 

were used for the training

the global 

in the simple setting, i.e., the two CAVs and three HDVs. As many people are aware, reward, local reward, and the proposed weighted reward scheme were used for the train-collisions are more likely to occur in the areas within the intersections than in the straight ing in the s

lanes. imple se

When the tting, 

system i.e., the 

was

two C

penalized, A

the Vs and thre

vehicle near e 

est HDVs

the

. As m

intersection any p

shouldeople are awar

have

e, 

collisions 

been are more 

assigned

like

more ly to occur

penalties to in the

help it

area

execute s wi

the thin

corr t

ect he inter

decision. sectio

The

ns than

same went in the

for

straight 

lanes. rWhen 

eceivingthe sy

a r

stem

eward. 

was penalized

The results are shown, the ve

in Figurehic

8. le ne

As

arest 

excepted, the

the in

r

tersection 

esults

should h

confirmed

ave 

that the proposed weighted assignment outperformed the other two assignment schemes. 

been assi

T

gne

able 2

d more pen

shows a clear

al

impr ties to he

ovement in lp 

the it execute

collision

the

rates and co

therrect dec

average

isio

speed n. The 

metrics. same

This

went for 

receiving 

was a reward. The re

because the global r sults 

eward are

was show

not an n in F

accurateig

r ure 

epr

8. As excep

esentation of the ted, the results co

contribution of a

nfirmed 

that the p

CAVr.oposed we

Although the ight

local erd as

ewar sdignm

impr ent

oved outp

on

er

this, form

the r

ed

ewar the

d

o

couldther 

not tw

be

o assignm

assigned

e

based nt schemes. 

Table 2 shows a clear improvement in the collision rates and the average speed metrics. 

This was because the global reward was not an accurate representation of the contribution of a CAV. Although the local reward improved on this, the reward could not be assigned based on an agent’s location. The weight reward assignment scheme assigned more rewards to the vehicles closer to the intersection, which facilitated the cooperation between the agents. 

**Table 2. **Performance comparison using the different reward assignment schemes. 

**Reward Assignment Scheme **

**Metrics **

**Global **

**Local **

**Proposed **

Collision rate 

0. 07 

0.03 

0 



*Appl. Sci. ***2021**, *11*, x FOR PEER REVIEW 

15 of 20 



Appl. Sci. **2023**, 13, 5018

14 of 19

on an agent’s location. The weight reward assignment scheme assigned more rewards to Average Speed \(m/s\) 

9.06 

9.04 

9.91 

the vehicles closer to the intersection, which facilitated the cooperation between the agents. 



**Figure 8. **

**Figure 8. **ComComparison of the

parison of the episode reward iepisode

n the trainin reward in 

g using the differe the trai

nt reward as nin

sign g

me using the diff

nt schemes. 

erent reward assignment 

schemes. 

**Table 2. **Performance comparison using the different reward assignment schemes. 

**Reward Assignment Scheme**

*5.3. Performan*

**Metrics**

*ce Comparison*

**Global**

* of the Differen*

**Local**

*t Forward Predictive Horizo*

**Proposed**

*ns *

Our r

Collision

ese

rate

arch scenar

0. 07 io was a mixed

0.03 traffic scenar

0 io where the HDVs and CAVs coex-

Average Speed \(m/s\)

9.06

9.04

9.91

isted. In this paper, the CAVs made decisions based on the predicted trajectories of all the ve

5.3.hicles ov

Performance er time

Comparison. T

of o

the vali

Differ da

ent te the 

Forward

im

Pr

pa

edictive ct of the d

Horizons

ifferent time horizon for predicting the 

trajecto

Our r ries

esear o

ch f all the v

scenario was a ehic

mixed les, 

traf 

ficthree se

scenario

tti

wher ngs

e the were

HDVs

us

and

ed 

CAVs for 

coex- the training. The results are 

isted. In this paper, the CAVs made decisions based on the predicted trajectories of all the shown 

vehicles

in Fi

over

g

time. u

T re 9 and the p

o validate the

e

impact rform

of the dif a

f nc

er

e m

ent time etrics 

horizon are pr

for pr

esented in

edicting the

Table 3. The results indi-

cated th

trajectories at

of a

all larger

the v

pr

ehicles, ed

thr ic

ee tion t

settings ime

were hori

used z

foron 

the did no

training. t im

The r ply 

esults a better

are

performance. Although 

shown in Figure 9 and the performance metrics are presented in Table 3. The results indi-a larger

cated that pred

a larger ictive

pr

time ho

ediction time

rizon

horizon did could

not imply r

a educe

better

the colli

performance. 

sion ra

Although

te, it would significantly re-

duce 

a larger the metrics o

predictive time

f the 

horizon c average 

ould reduce speed

the

. The performance depende

collision rate, it would significantly

d on the design of the 

reduce the metrics of the average speed. The performance depended on the design of the headw

headway ay eval

evaluation ua

in tion in 

the reward the reward func

function and the desir ti

ed on and the d

headway time, as

esired he

introduced

adway time, as introduced 

in Sec

in

t

Sectionion 

4.1. 4.1

The . The de

desired

sire

headway d headw

time td was ay

set t

to i2me 

s

*t*

during the training. When

T

*d * was set to 2 s during the training. When 

h = 1 s, even though the current headway time was less than td, the vehicle agent still *T*

r

=1 

eceived sa positive reward because no collision was detected within the predictive horizon. 

*t*

*h*

, even though the current headway time was less than *d *, the vehicle agent still This could easily result in the vehicle anticipating a collision when the brakes would not received

be able to

a

pr

po

event asitive rew

collision. 

ard

Compar beca

ed to Th use

= 3 no c

s, the

o

pr llision

ediction

was

horizon detec

of Th = t

5 ed

s

within the predictive hori-

was conservative for the decision-making of the vehicle. As long as the collision was not zon. Thi

detected

s coul

within 3 s, d ea

the

sily result

vehicle received a i

r n th

ewarde vehi

of one cle 

with a a

3 n

s ti

prcipati

ediction ng a coll

horizon. In ision when the brakes would 

not be able to prevent a collision. Compared to *T *= 3 s *T *=

*h*

, the prediction horizon of 

5 s

*h*



was conservative for the decision-making of the vehicle. As long as the collision was not detected within 3 s, the vehicle received a reward of one with a 3 s prediction horizon. In the case of *T *= 5 s

< 

*h*

, the vehicle would be rewarded with the value of ln\(5 2\) 1 , even though the collision was predicted at 5 s. This indicated that a suitable prediction time horizon could achieve a better performance. *T *= 3 s

*h*

achieved a good trade-off between 

the collision rate and the prediction efficiency. 

**Table 3. **Performance comparison for the different forward predictive horizons. 

**Horizon Time * ***

**Metrics **

***Th = *****1 s * ***

***Th = *****3 s * ***

***Th = *****5 s * ***

Collision rate 

0.03 

0 

0 

Average 

9.10 9.91 8.67 

Speed \(m/s\) 





Appl. Sci. **2023**, 13, 5018

15 of 19

the case of Th = 5 s, the vehicle would be rewarded with the value of ln\(5/2\) < 1, even though the collision was predicted at 5 s. This indicated that a suitable prediction time *Appl. Sci. ***2021**, *11*, x FOR PEER RE horizon VIEW 

could achieve a better performance. T

16 of 20 

h = 3 s achieved a good trade-off between



the collision rate and the prediction efficiency. 



**Figure 9. **

**Figure 9. **C Comparison of the

omparison of the epis 

o episode

de rewar reward in 

d in the train the tr

ing forainin

the d g

if for the differ

ferent forward e

prnt forward predict

edictive horizons. 

ive 

horizons. 

**Table 3. **Performance comparison for the different forward predictive horizons. 

*5.4. Performance Comparison of the Proposed and Heuristic Rule-Based Algorithm* **Horizon Time**

In this sub

**Metrics **section, we verified the adaptability of our proposed algorithm by com-Th = 1 s

**Th = 3 s**

**Th = 5 s**

paring it with the heuristic rule-based algorithm using the same scenario in Section 5.2. 

Collision rate

0.03

0

0

The traditional ruled-based or model-based decision control approaches were capable of generating 

Average

stable decision resu

Speed \(m/s\)

lts, accu

9.10

rate control cu

9.91 rves, and were easy 

8.67

to implement. 

For example, the vehicles coordination of negotiating the access in an intersection was reformulate

5.4. 

d

Performance as a virtual 

Comparison of platoon con

the Proposed

tr

andol problem in 

Heuristic

\[9\]. Accord

Rule-Based

ing to

Algorithm

the passage se-

quenc

In e, the HDV acted 

this subsection, we as the le

verified ader and 

the

the two 

adaptability of CA

our Vs kept the

proposed

desire

algorithm d fo

by llowing 

com-

dis-

tance. 

paring F

it igure 10 shows the resu

with the heuristic r

lts u

ule-based sing a vir

algorithmtual p

usinglato

the on. The HDV 

same scenario trave

in

led at th

Section 5.2 e desired

. 



The traditional ruled-based or model-based decision control approaches were capable of speed of 10 m/s. CAV1 adjusted its speed to keep the desired distance from the HDV and generating stable decision results, accurate control curves, and were easy to implement. 

CAV2 followed CAV1. 

For example, the vehicles coordination of negotiating the access in an intersection was reformulated as a virtual platoon control problem in \[9\]. According to the passage sequence, the HDV acted as the leader and the two CAVs kept the desired following distance. 

Figure 10 shows the results using a virtual platoon. The HDV traveled at the desired speed of 10 m/s. CAV1 adjusted its speed to keep the desired distance from the HDV and CAV2

followed CAV1. 



**Figure 10. **The speed and position curves of all the vehicles in the ideal traffic using the heuristic rule-based algorithm; \(**a**\) the speed, \(**b**\) the position. 





*Appl. Sci. ***2021**, *11*, x FOR PEER REVIEW 

16 of 20 





**Figure 9. **Comparison of the episode reward in the training for the different forward predictive horizons. 

*5.4. Performance Comparison of the Proposed and Heuristic Rule-Based Algorithm* In this subsection, we verified the adaptability of our proposed algorithm by comparing it with the heuristic rule-based algorithm using the same scenario in Section 5.2. 

The traditional ruled-based or model-based decision control approaches were capable of generating stable decision results, accurate control curves, and were easy to implement. 

For example, the vehicles coordination of negotiating the access in an intersection was reformulated as a virtual platoon control problem in \[9\]. According to the passage sequence, the HDV acted as the leader and the two CAVs kept the desired following distance. Figure 10 shows the results using a virtual platoon. The HDV traveled at the desired Appl. Sci. **2023**, 13, 5018

speed of 10 m/s. CAV1 adjusted its speed to keep the desired dist 16 of

ance fr 19

om the HDV and 

CAV2 followed CAV1. 



*Appl. Sci. ***2021**, *11*, x FOR PEER REVIEW 

17 of 20 



**Figure 10. **The **Figure 10. **

speed and The speed

position

and posi

curves of tion cu

all the

rves of 

vehicles all

in the 

the vehi

ideal cles in

traffic the idea

using

l 

the traffic using

heuristic

the heuristic 

rule-based

rule-based algorithm; \(

algorithm; \(**a**\) the speed, \(**b**\) **a**\) the 

the

speed, \(

position. **b**\) the position. 

Although the vehicles

Al

could

though the cooperatively

vehicles coul and ef

d coopficiently

erativel cr

y oss the

and effi intersections

ciently cross under

the intersections un-

the ideal traffic conditions

der the ideal using

traffic the heuristic

conditions us rule-based

in

model, 

g the heuristic rul some

e-bas of

ed the idealized

model, some of the idealized 

condition assumptions

condit

wer

ion ass e

u dif

mpficult

tion to

s wesatisfy

re diff in

icu many

lt to

cases. 

satisfy Generally

in many ca speaking, 

ses. Ge

the

nerally speaking, the 

traffic scenarios involvi

traffic

ng

scen the

arioHDVs

s invo were

lving mor



e

the complex

HDVs weand uncertain

re more co

for the

mplex 

uncontr

and un

olled

certain for the uncon-

human driving. For

trol

example, 

led huma some

n driv drivers

ing. Fo were

r exam conserv

ple, so ative

me

and

driver traveled

s we

at a

re conserlow

vati speed

ve and traveled at a 

for fear of getting scratched

low speed for in intersections. 

fear of getting scr The

atche speed and

d in inte

position

rsection

curves

s. The spee of

d all the

and position curves of 

vehicles when the HDV traveled

all the vehi

at a low

cles when the speed

HDV using

travele a

d heuristic

at a 

rule-based

low speed us

algorithm

ing a heuristi ar

c e

rule-based algo-

shown as Figure

rit 11

h . 

m In or

are der to form

shown as Fi a virtual

gure 11

platoon, 

. In order the

to fo speed

rm

of

a vi both

rtual p CA

lat Vs converged

oon, the speed of both CAVs 

to that of the leading HDV. Practically, the CAV

converged to that of the lead

2 was not in the same lane as the HDV, so it

ing HDV. Practically, the CAV2 was not in the same lane as 

did not need to keep up with the speed of the HDV, which could greatly enhance the road the HDV, so it did not need to keep up with the speed of the HDV, which could greatly efficiency. The results demonstrated that the heuristic rule-based approaches, while easy to enhance the road efficiency. The results demonstrated that the heuristic rule-based ap-implement, were not adaptive to some special cases. 

proaches, while easy to implement, were not adaptive to some special cases. 



**Figure 11. **The **Figure 11. **

speed and The speed and

position

posi

curves of tion curves of

all the vehicles all the v

when

e

thehicles 

HDV when the HDV traveled

traveled at a low speed at a low speed 

using the

using

heuristic r the heur

ule-based istic rule-base

algorithm; \(**a**\) d alg

the orithm

speed, \(; \(

**b a**

\) \) th

the e speed, \(

position. **b**\) the position. 

A

A le

learning-based arning

appr -based 

oach

approach

enabled mor enab

e effi led mor

cient

e efficient decision

decision-making. The -ma

r

kin

esults g. The

are

results are 

presented in presented in Fig

Figure 12 using ure

the 12 using the 

proposed

propos

algorithm ed algori

when

th

the m when 

HDV

the HDV

traveled at a trav

low eled at a low 

speed. Based speed. B

on the ased on the 

trajectory pr trajectory pred

ediction of the ictio

othern of the o

vehicles, ther vehicles, CAV

CAV2 predicted that the

2 predicted that the 

slow speed ofslow spee

the HDVd of the 

would HDV w

not

o

cause uld no

a

t cause a collision

collision. CAV2 made . CAV

the decision to breaks

2 made the decision to breaks 

traffic rules

traffic r

and pass ules and pass 

first, since the firs

r

t, since 

eward

the rew

for

ard 

following for fo

the

llow

traffic irng th

ules e tra

was ffic rule

smaller s wa

than s smaller than 

the penalty

the penalty fo

for crossing the r crossing th

intersection e 

atinter

a

sec

low tion at a 

speed. 

low speed

Thus, if no

. Thus, if no co

collision was pr llision w

edicted, as predicted, 

the HDV

the HD

only af

V on

fected

ly affec

the

ted

decision th

of e decision o

CAV1

f C

behind A

it V

in the same lane but not CAV2’s

1 behind it in the same lane but not CAV2′s in 

other lane. As shown in Figure 12b, after the HDV crossed the stop line, that is, when its position was less than 0, the CAV began to accelerate. This accounted for the fact that the proposed approach could deal with some special cases, which were more adaptive and generalized. 





Appl. Sci. **2023**, 13, 5018

17 of 19

in other lane. As shown in Figure 12b, after the HDV crossed the stop line, that is, when its position was less than 0, the CAV began to accelerate. This accounted for the fact that *Appl. Sci. ***2021**, *11 * the

, x FO proposed

R PEER RE appr

VIEW oach could deal with some special cases, which were more adaptive 18 of 20 



and generalized. 



**Figure 12. **The **Figure 12. **

speed and The speed and

position

posi

curves of tion curves of

all the vehicles all the v

when

e

the hicles 

HDV when the HDV traveled

traveled at a low speed at a low speed 

using the pr

usin

oposed g the propos

algorithm; \(**a**ed al

\) the gorithm; 

speed, \( \(

**b**\)**a**\) th

the e speed, 

position. \(**b**\) the position. 

**6. Conclusions6. Conclusions **

In this paper, we modeled the decision-making at the intersection of the CAVs and In this paper, we modeled the decision-making at the intersection of the CAVs and HDVs in coexistence as a model-free and fully cooperative multi-agent system. Based on HDVs in coexistence as a model-free and fully cooperative multi-agent system. Based on this, we presented the design of the observation, action, and reward functions to formulate this, we presented the design of the observation, action, and reward functions to formulate the cooperative decision-making as a MARL problem. Then, a decentralized MAPPO based the cooperative decision-making as a MARL problem. Then, a decentralized MAPPO 

on the attention representations algorithm \(Attn-MAPPO\) was developed to make joint based on the attention representations algorithm \(Attn-MAPPO\) was developed to make decisions to avoid collisions and cross the intersection effectively. Finally, the policy was joint decisions to avoid collisions and cross the intersection effectively. Finally, the policy trained and evaluated via an open source simulation platform. The results showed the was trained and evaluated via an open source simulation platform. The results showed advantages of our proposed algorithm and the designed reward scheme. In addition, the the advantages of our proposed algorithm and the designed reward scheme. In addition, comparison of the results using the three prediction time horizons also suggested that a the comparison of the results using the three prediction time horizons also suggested that suitable horizon could achieve a better performance. We compared the performance of the a suitable horizon could achieve a better performance. We compared the performance of Attn-MAPPO to an equivalent virtual platoon control, a heuristic rule-based method, which the Attn-MAPPO to an equivalent virtual platoon control, a heuristic rule-based method, indicated that the proposed approach could deal with some special cases more adaptively which indicated that the proposed approach could deal with some special cases more and generically. 

adaptively and generically. 

However, there were still some unsolved problems in this paper. The driving behavior However, there were still some unsolved problems in this paper. The driving behav-of the HDVs was modeled using the IDM model. In practice, more accurate models may be ior of the HDVs was modeled using the IDM model. In practice, more accurate models needed. Moreover, the scalability of the algorithm needs to be improved, i.e., increasing may be needed. Moreover, the scalability of the algorithm needs to be improved, i.e., inthe number of CAVs. At the same time, in this paper, only the full cooperation between the vehicles was creasing 

consider the 

ed. 

number of C

In fact, there AVs. A

was also t the 

a

same time, in 

competition

this

between paper, o

the

nly th

vehicles at e fu

the ll cooperation 

intersection. between the

In future

vehicle

works, we s w

will as consider

pay more ed. In fact

attention , there was also a 

to these issues and competition

continue to between the 

expand from vehicle

this

s a

study. t the intersection. In future works, we will pay more attention to these issues and continue to expand from this study. 

**Author Contributions: **Conceptualization, H.Z.; methodology, H.Z.; software, H.Z.; validation, C.L.; formal

**Autho**

analysis, C.L.; **r Contributions**

investigation, **: **

Y Conc

.C.; r eptu

esour alization, 

ces, X.T.; H.Z. 

data ; methodo

curation, logy

H.Z , 

.; H.Z.; software, H.Z

writing—original

.; validation, 

draft pr

C.L.; formal an

eparation, H.Z.; 

alysis, 

writing—r

C.L. 

eview ; inv

and estigation, 

editing, 

Y.C

C.L. 

.; resou

and Y.C.; rces, X.T.; data cu

visualization, 

ration, 

C.L.; 

H.Z.; writing

supervision, 

—original 

X.T.; project

draft preparation, 

administration, X.T.; H.Z.; writ

funding ing—review and 

acquisition, X.T. 

editing

All

, C

authors .L. and Y.C. 

have read ; vi

andsualiz

agr ation, C. 

eed to the L.; supervision, 

published

X.T. 

version ; project

of the

administration, X

manuscript. 

.T.; funding acquisition, X.T. All authors have read and agreed to the published version of the manuscript. ** **

**Funding: **This research was funded by the Key-Area Research and Development Program of Guangdong Province **Fund**

under **ing:** Thi

Grant

s research was

2020B0909030005 funded

and

by the Key-

2020B090921003. Area Research and Development Program of 

Guangdong Province under Grant 2020B0909030005 and 2020B090921003. 

**Institutional Review Board Statement: **Not applicable. 

**Institutional Review Board Statement: **Not applicable. 

**Informed Consent Statement: **Not applicable. 

**Informed Consent Statement: **Not applicable. 

**Data Availability Statement: **Data sharing not applicable. No new data were created or analyzed in this study. Data sharing is not applicable to this article. 

**Conflicts of Interest: **The authors declare no conflict of interest. 

Appl. Sci. **2023**, 13, 5018

18 of 19

**Data Availability Statement: **Data sharing not applicable. No new data were created or analyzed in this study. Data sharing is not applicable to this article. 

**Conflicts of Interest: **The authors declare no conflict of interest. 

**References**

1. 

Eskandarian, A.; Wu, C.; Sun, C. Research Advances and Challenges of Autonomous and Connected Ground Vehicles. IEEE

Trans. Intell. Transp. Syst. **2021**, 22, 683–711. \[CrossRef\]

2. 

Ghorai, E.A.P.; Kim, Y.K.; Mehr, G. State Estimation and Motion Prediction of Vehicles and Vulnerable Road Users for Cooperative Autonomous Driving: A Survey. IEEE Trans. Intell. Transp. Syst. **2022**, 23, 16983–17002. \[CrossRef\]

3. 

Loke, S.W. Cooperative Automated Vehicles: A Review of Opportunities and Challenges in Socially Intelligent Vehicles Beyond Networking. IEEE Trans. Intell. Veh. **2019**, 4, 509–518. \[CrossRef\]

4. 

Chen, L.; Li, Y.; Huang, C.; Li, B.; Xing, Y.; Tian, D.; Li, L.; Hu, Z.; Na, X.; Li, Z.; et al. Milestones in Autonomous Driving and Intelligent Vehicles: Survey of Surveys. IEEE Trans. Intell. Veh. **2023**, 8, 1046–1056. \[CrossRef\]

5. 

Wang, H.; Meng, Q.; Chen, S.; Zhang, X. Competitive and cooperative behaviour analysis of connected and autonomous vehicles across unsignalised intersections: A game-theoretic approach. Transp. Res. Part B Methodol. **2021**, 149, 322–346. \[CrossRef\]

6. 

Xue, Y.; Zhang, X.; Cui, Z.; Yu, B.; Gao, K. A platoon-based cooperative optimal control for connected autonomous vehicles at highway on-ramps under heavy traffic. Transp. Res. Part C Emerg. Technol. **2023**, 150, 104083. \[CrossRef\]

7. 

Aoki, S.; Lin, C.W.; Rajkumar, R. Human-Robot Cooperation for Autonomous Vehicles and Human Drivers: Challenges and Solutions. IEEE Commun. Mag. **2021**, 59, 35–41. \[CrossRef\]

8. 

Treiber, M.; Hennecke, A.; Helbing, D. Congested traffic states in empirical observations and microscopic simulations. Phys. Rev. 

E **2000**, 62 Pt A, 1805–1824. \[CrossRef\]

9. 

Peng, B.; Keskin, M.F.; Kulcsár, B.; Wymeersch, H. Connected autonomous vehicles for improving mixed traffic efficiency in unsignalized intersections with deep reinforcement learning. Commun. Transp. Res. **2021**, 1, 100017. \[CrossRef\]

10. 

Li, C.; Hu, Z.; Lu, Z.; Wen, X. Cooperative Intersection with Misperception in Partially Connected and Automated Traffic. Sensors **2021**, 21, 5003. \[CrossRef\] \[PubMed\]

11. 

Jie, W.; Zhihao, J.; Vardhan, P.Y. Improving Safety in Mixed Traffic: A Learning-based Model Predictive Control for Autonomous and Human-Driven Vehicle Platooning. arXiv **2023**, arXiv:2211.04665. 

12. 

Chen, L.; Englund, C. Cooperative Intersection Management: A Survey. IEEE Trans. Intell. Transp. Syst. **2016**, 17, 570–586. 

\[CrossRef\]

13. 

Yu, C.; Velu, A.; Vinitsky, E.; Wang, Y.; Bayen, A.; Wu, Y. The surprising effectiveness of ppo in cooperative, multi-agent games. 

arXiv **2021**, arXiv:2103.01955. 

14. 

Long, Q.; Zhou, Z.; Gupta, A.; Fang, F.; Wu, Y.; Wang, X. Evolutionary Population Curriculum for Scaling Multi-Agent Reinforcement Learning. arXiv **2020**, arXiv:2003.10423. 

15. 

Dresner, K.; Stone, P. A multiagent approach to autonomous intersection management. J. Artif. Intell. Res. **2008**, 31, 591–656. 

\[CrossRef\]

16. 

Milanes, V.; Perez, J.; Onieva, E.; Gonzalez, C. Controller for Urban Intersections Based on Wireless Communications and Fuzzy Logic. IEEE Trans. Intell. Transp. Syst. **2010**, 11, 243–248. \[CrossRef\]

17. 

Bian, Y.; Li, S.E.; Ren, W.; Wang, J.; Li, K.; Liu, H.X. Cooperation of Multiple Connected Vehicles at Unsignalized Intersections: Distributed Observation, Optimization, and Control. IEEE Trans. Ind. Electron. **2020**, 67, 10744–10754. \[CrossRef\]

18. 

Xu, H.; Zhang, Y.; Li, L.; Li, W. Cooperative Driving at Unsignalized Intersections Using Tree Search. IEEE Trans. Intell. Transp. 

Syst. **2020**, 21, 4563–4571. \[CrossRef\]

19. 

Vaio, M.D.; Falcone, P.; Hult, R.; Petrillo, A.; Salvi, A.; Santini, S. Design and Experimental Validation of a Distributed Interaction Protocol for Connected Autonomous Vehicles at a Road Intersection. IEEE Trans. Veh. Technol. **2019**, 68, 9451–9465. \[CrossRef\]

20. 

Nan, J.; Deng, W.; Zheng, B. Intention Prediction and Mixed Strategy Nash Equilibrium-Based Decision-Making Framework for Autonomous Driving in Uncontrolled Intersection. IEEE Trans. Veh. Technol. **2022**, 71, 10316–10326. \[CrossRef\]

21. 

Aradi, S. Survey of deep reinforcement learning for motion planning of autonomous vehicles. IEEE Trans. Intell. Transp. Syst. 

**2020**, 23, 740–759. \[CrossRef\]

22. 

Isele, D.; Rahimi, R.; Cosgun, A.; Subramanian, K.; Fujimura, K. Navigating Occluded Intersections with Autonomous Vehicles Using Deep Reinforcement Learning. In Proceedings of the 2018 IEEE International Conference on Robotics and Automation \(ICRA\), Brisbane, QLD, Australia, 21–25 May 2018; pp. 2034–2039. 

23. 

Lin, Y.; McPhee, J.; Azad, N.L. Comparison of Deep Reinforcement Learning and Model Predictive Control for Adaptive Cruise Control. IEEE Trans. Intell. Veh. **2021**, 6, 221–231. \[CrossRef\]

24. 

Shi, Y.; Liu, Y.; Qi, Y.; Han, Q. A Control Method with Reinforcement Learning for Urban Un-Signalized Intersection in Hybrid Traffic Environment. Sensors **2022**, 22, 779. \[CrossRef\]

25. 

Liu, Y.; Liu, G.; Wu, Y.; He, W.; Zhang, Y.; Chen, Z. Reinforcement-Learning-Based Decision and Control for Autonomous Vehicle at Two-Way Single-Lane Unsignalized Intersection. Electronics **2022**, 11, 1203. \[CrossRef\]

26. 

Mao, F.; Li, Z.; Lin, Y.; Li, L. Mastering Arterial Traffic Signal Control with Multi-Agent Attention-Based Soft Actor-Critic Model. 

IEEE Trans. Intell. Transp. Syst. **2022**, 24, 3129–3144. \[CrossRef\]

Appl. Sci. **2023**, 13, 5018

19 of 19

27. 

Chen, D.; Li, Z.; Wang, Y.; Jiang, L.; Wang, Y. Deep multi-agent reinforcement learning for highway on-ramp merging in mixed traffic. arXiv **2021**, arXiv:2105.05701. 

28. 

Guan, Y.; Ren, Y.; Li, S.E.; Sun, Q.; Luo, L.; Li, K. Centralized Cooperation for Connected and Automated Vehicles at Intersections by Proximal Policy Optimization. IEEE Trans. Veh. Technol. **2020**, 69, 12597–12608. \[CrossRef\]

29. 

Zhou, M.; Yu, Y.; Qu, X. Development of an efficient driving strategy for connected and automated vehicles at signalized intersections: A reinforcement learning approach. IEEE Trans. Intell. Transp. Syst. **2019**, 21, 433–443. \[CrossRef\]

30. 

Antonio, G.P.; Maria-Dolores, C. Multi-Agent Deep Reinforcement Learning to Manage Connected Autonomous Vehicles at Tomorrows Intersections. IEEE Trans. Veh. Technol. **2022**, 71, 7033–7043. \[CrossRef\]

31. 

Duan, X.; Jiang, H.; Tian, D.; Zou, T.; Zhou, J.; Cao, Y. V2I based environment perception for autonomous vehicles at intersections. 

China Commun. **2021**, 18, 1–12. \[CrossRef\]

32. 

Leurent, E. An Environment for Autonomous Driving Decision-Making. GitHub Repository. 2018. Available online: https:

//github.com/eleurent/highway-env \(accessed on 31 December 2018\). 

**Disclaimer/Publisher’s Note: **The statements, opinions and data contained in all publications are solely those of the individual author\(s\) and contributor\(s\) and not of MDPI and/or the editor\(s\). MDPI and/or the editor\(s\) disclaim responsibility for any injury to people or property resulting from any ideas, methods, instructions or products referred to in the content. 



# Document Outline

+ Introduction  
+ Literature Review  
+ Problem Statement   
	+ Scenario Description  
	+ Right of Way Rules  
	+ Vehicle Interaction Model  

+ Cooperative Decision-Making in a Multi-Vehicle Cooperative Task   
	+ Problem Formulation  
	+ Wighted Reward Assignment  
	+ Cooperative Learning Algorithm for Multi-Agent Task  

+ Results and Discussion   
	+ Performance Comparison between the Proposed Attn-MAPPO Algorithm and the Benchmark  
	+ Performance of the Proposed Reward Scheme Designs  
	+ Performance Comparison of the Different Forward Predictive Horizons  
	+ Performance Comparison of the Proposed and Heuristic Rule-Based Algorithm  

+ Conclusions  
+ References



