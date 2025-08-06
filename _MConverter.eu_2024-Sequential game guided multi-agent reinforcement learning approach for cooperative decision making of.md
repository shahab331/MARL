Original Article

Proc IMechE Part D:

J Automobile Engineering

1–16

Sequential game guided multi-agent Ó IMechE 2024

Article reuse guidelines:

sagepub.com/journals-permissions

reinforcement learning approach for

DOI: 10.1177/09544070241305663

journals.sagepub.com/home/pid

cooperative decision making of

autonomous vehicles at unsignalized intersections in mixed-autonomy

traffic

Zihan Guo1 , Yan Wu1 , Lifang Wang1 and Junzhi Zhang2

Abstract

The advancement of Connected and Autonomous Vehicle \(CAV\) technology has made the complex cooperation of multiple CAVs feasible, especially at non-signalized intersections. However, challenges remain in the mixed-autonomy traffic scenarios, where collaboration among CAVs and their interactions with human-driven vehicles \(HDVs\) must be resolved simultaneously. Accordingly, this study proposes a new multi-agent reinforcement learning algorithm, SG-QMIX, extending the original QMIX framework by incorporating a sequential game theory-based action filter module. This module integrates the First-Come-First-Served \(FCFS\) strategy with the sequential game and its derived equilibrium to mask out the unavailable actions, in which the FCFS strategy simplifies the ensuing cooperation of multiple CAVs before they enter the intersection, and the equilibrium of the designed sequential game guides the CAVs to learn the interactive strategies with other participants at the junction. Moreover, the experimental results show that the SG-QMIX approach can outperform the existing approaches in terms of episodic return, episodic length, and success rate for cooperative decision-making at an isolated signal-free intersection. Additionally, the trained policy can reduce average fuel consumption, main-tain traffic efficiency, and enable CAVs to interact with surrounding HDVs rationally and altruistically. Furthermore, we also validate the zero-shot transferability of SG-QMIX to an unseen scenario and its applicability to more complex intersections. 

Keywords

Cooperative decision making of autonomous vehicles, multi-agent deep reinforcement learning, zero-shot generalization Date received: 15 April 2024; accepted: 4 November 2024

## Introduction

1Key Laboratory of High Density Electromagnetic Power and Systems, The technology of autonomous driving and Connected Institute of Electrical Engineering Chinese Academy of Sciences, and University of Chinese Academy of Sciences, Beijing, China and Autonomous Vehicles \(CAVs\) have experienced 2Department of Automotive Engineering, State Key Laboratory of significant advancements over the past decades, having Automotive Safety and Energy, Tsinghua University, Beijing, China the power to enhance traffic efficiency, reduce energy consumption and pollutant emissions, and ensure Corresponding author:

Yan Wu, Institute of Electrical Engineering, Chinese Academy of Sciences, safety.1 Nonetheless, some challenging scenarios still Haidian District, Beijing 100190, China, and University of Chinese require three-dimensional collaboration \(lateral, longi-Academy of Sciences, Shijingshan District, Beijing 100049, China. 

tudinal, and temporal dimension\), such as non-Email: wuyan@mail.iee.ac.cn

signalized intersections and on-ramp merging.1,2 This study addresses the conflict resolution of CAVs and Lifang Wang, Key Laboratory of High Density Electromagnetic Power and Systems, Institute of Electrical Engineering, Chinese Academy of Sciences, other traffic participants, such as Human-Driven Haidian District, Beijing 100190, China, and University of Chinese Vehicles \(HDVs\) at signal-free junctions in mixed-Academy of Sciences, Shijingshan District, Beijing 100049, China. 

autonomy traffic. Research in this field can be divided Email: wlf@mail.iee.ac.cn

2

Proc IMechE Part D: J Automobile Engineering 00\(0\) into three main approaches: 1\) heuristic \(e.g. First-encouraging each CAV to learn interactive strate-Come-First-Serve \(FCFS\) strategy3 or optimization-gies at the junction zone, 

based approaches,4,5 2\) deep reinforcement learning 2\)

We propose a new MARL approach \(SG-QMIX\) \(DRL\)-based methods,6–10 such as deep Q network11

that integrates the action filter guided by both the \(DQN\), or proximal policy optimization12 \(PPO\), 3\) FCFS strategy and the equilibrium derived from game theoretic approaches.13–16 However, these meth-the constructed pair-wise sequential games to the ods often employ centralized controllers, leading to low original QMIX framework, facilitating the colla-computational efficiency and poor scalability with the boration among CAVs and their interactions with increasing number of agents. 

HDVs, 

Multi-agent deep reinforcement learning \(MARL\) 3\)

We comprehensively evaluate the performance of offers a promising solution. Instead of directly deploy-SG-QMIX, which includes a comparative study ing DRL on every single agent \(i.e. independent Q-with several benchmark MARL algorithms and an learning17 \(IQL\)\), most MARL algorithms exploit the ablation study with its internal modules, and apply Centralized Training with Decentralized Execution the SG-QMIX algorithm to unseen scenarios, \(CTDE\) architecture,18 combining the advantages of asymmetric 4-way-2-lane intersection for validat-both distributed and centralized approaches, and over-ing its zero-shot transferability, and 4-way-3-lane coming the nonstationarity problem.19 This framework intersection for generalizability. 

assumes agents’ global state information is available during training, while agents can only access their obser-The remainder of this document is structured as fol-vations during the model execution. QMIX20 is one of lows. The section on Related Works provides an overview the baseline MARL algorithms, extending VDNs21 by of studies pertinent to this research. An introduction to employing monotonic constraints to better express the the essential concepts of MARL and the basics of centralized joint action value. Moreover, finetuned sequential game theory is presented in Preliminaries. The QMIX leads the StarCraft Multi-Agent Challenge Problem Formulation section details the conversion of the \(SMAC\), achieving the highest average score.22

coordination of multiple CAVs at signal-free intersec-Additionally, DRL or MARL methods may encoun-tions into a MARL problem. The Methodology section ter several common issues: low sample efficiency and meticulously outlines the proposed approaches, followed poor generalization to unseen tasks.18 This phenom-by the presentation of experimental results in Numerical enon can be detrimental to real-world applications with Experiments. Finally, Conclusions and Future Works sum-expensive data collection. Some studies have validated marizes this research’s findings and suggests further the zero-shot transfer capabilities of proposed models investigation directions. 

to a certain extent.23–25 For instance, Candela et al.23

combined PPO architecture with domain randomiza-Related works

tion techniques to address the sim-to-real problem. 

Afterward, they successfully transfer the trained model DRL and MARL approaches for cooperative decision to the real-world Duckietown-based testbed24 in a one-making of CAVs

shot manner. The success of zero-shot transferability Regarding cooperative decision-making of CAVs at lies in the fundamentally identical topological complex-signal-free intersections, Guan et al.7 improved the ity of the source and target task. Otherwise, that gener-PPO algorithm with a kinematics-based model to alization process may fail. 

address the low computational efficiency of centralized Another direction of research explicitly models vehi-optimization-based intersection manager and to further cle interactions with game theoretic frameworks, but improve the sample efficiency of PPO itself with that these studies only cover a few CAVs and rarely investi-model generating virtual samples. Peng et al.26 pro-gate the mixed-autonomy traffic.13–16 Unavoidably, posed a specific altruistic reward function for the PPO

CAVs will coexist with HDVs in the long run, requiring algorithm combined with generalized advantage esti-CAVs to interact with other CAVs and HDVs that mation \(GAE\) to mitigate the low traffic efficiency may feature uncertain and diverse driving behaviors.2

caused by the selfishness of HDVs. The authors then Therefore, the mixed-autonomy traffic brings an extra assessed their methods using a simulation scenario of a complexity dimension to the original three-dimensional figure-eight signal-free intersection based on FLOW27

collaboration problems. 

simulator, and the results showed that the algorithm In terms of the problems above, this study is motivated could significantly reduce the number of cumulative to explicitly decouple the vehicle coordination in mixed-stopped vehicles at the junction. 

autonomy traffic into two parts: 1\) cooperation between An end-to-end deep RL algorithm based on the CAVs and 2\) the interaction between CAVs and HDVs. 

Twin-delayed

DDPG

\(TD3\)

framework, 

called

The main contributions of this study are as follows: adv.RAIM, was designed by Antonio and Maria-Dolores.28 The authors also employed a self-play curri-1\)

We construct pair-wise sequential games from culum that increases the number of vehicles involved in complex interactions between CAVs and HDVs, the simulation to ease and stabilize the training process. 

Guo et al. 

3

Compared with traditional traffic light controllers, the justified on various intersections with different geo-adv.RAIM can reduce travel time \(by 59%\) and pollu-metric parameters and changing numbers of CAVs. 

tion emissions. Furthermore, Wu et al.29 creatively The simulation results demonstrated that it could decomposed the state space of CAVs into the individual reconstruct vehicle interactions similar to real-world and coordination parts for the coordination task. Then, traffic data. 

they proposed a tabular MARL method called the Liu et al.15 built a three-level cooperative decision-decentralized

coordination

multi-agent

learning

making framework based on game theory. The first approach \(DCL-AIM\), which dynamically determined layer and the third layer functioned as safety checkers, whether the ego vehicle needed to coordinate with the and the second layer supervised the ego vehicle to play surrounding vehicles. DCL-AIM numerically exhibited a matrix game with one of its surrounding vehicles, lower intersection delay and per-vehicle average delay where the utilities were parameterized by deliberately at 4-way-3-lane intersection scenarios with various traf-designed deep neural networks and trained with an fic density and discretization levels of intersection space. 

offline-to-online paradigm. Additionally, the driving Further, Peng et al.30 extended this tabular-based style of the surrounding vehicles was characterized dur-algorithm to a deep network-based version, coined as ing the training phase. The numerical results showed CoPo. Specifically, they designed local and global coor-that the proposed model could achieve a 100% success dination layers; the former was inspired by the social rate on intersection crossing and lane-changing scenar-value orientation to enable the individual agents to con-ios involving two CAVs. Li et al.34 outlined a game sider the interests of their neighboring agents, and the theory-based hierarchical decision-making algorithm to latter automatically searched for the optimal coordina-enhance travel efficiency and eliminate conflicts when tion factor by agent-wise QMIX-like decomposition. 

the ego vehicle interacted with vehicles exhibiting The authors retrained and validated their approach on diverse and uncertain behaviors at unsignalized inter-several typical multi-vehicle scenarios, including round-sections. The authors utilized the prospect theory to abouts, intersections, and tollgates, obtaining better transform the collision risk into the utility of the game success rates, traffic efficiency, and emerging more and quantitatively described the driving style of interac-diverse social behaviors than other MARL algorithms. 

tive vehicles using a probabilistic model. The method’s Tackling CAVs involved in on-ramp merging sce-performance was validated on both the two-player and narios is another proliferating sub-field for applying four-player interaction simulations, acquiring a 98%

DRL or MARL algorithm to address the correspond-safety rate and guaranteeing the traveling speed. The ing cooperation challenge. For the diversity of the liter-study of Yuan et al.13 combined the level-k cognitive ature review and the succinctness of this study, we only hierarchy reasoning with D3QN \(a popular approach introduce a few studies targeting the merging scenarios. 

in the DRL domain\) to address the coordination prob-Although Nakka et al.31 did not consider the local or lem, where hierarchical reasoning was employed to pre-global traffic flow in which several CAVs were partici-dict how surrounding vehicles understand the ego pating, they successfully employed the MADDPG

vehicle. Additionally, the authors exploited the curricu-algorithm to coordinate eight CAVs at highway mer-lum learning to grow the reasoning levels when training ging scenario, eliminating the stop-and-go behaviors, the DQN-like networks and tested the trained model hence reducing the travel time. Similarly, Chen et al.32

on a ROS-GAZEBO-based simulation environment constructed a MARL problem and proposed a scalable and equivalent real-world testbed. 

framework in which the authors filtered out the unrea-Concerning the on-ramp merging scenarios, Hang sonable behaviors and presented a priority-based safety et al.35 suggested a coalitional game theoretic model administer to further prevent the CAVs from encoun-predictive control \(MPC\) framework, pre-defining tering the emergency. Moreover, a curriculum with four potential coalition types according to the num-progressive difficulty was proposed to speed up the ber of vehicles involved. Furthermore, an objective training process. 

function considering the motion prediction, driving characteristics of the surrounding vehicles determined by safety, comfort, and efficiency, was constructed to Game theoretic approaches for cooperative decision aid in the following optimization phase. The simula-making of CAVs

tion results guarantee the safety of CAVs and boost Game theoretic approaches are another burgeoning traffic efficiency. Lopez et al.14 combined the well-line of research to address the CAV cooperation chal-known actor-critic framework in DRL with a pair-lenge, although these methods generally handle lim-wise decomposed multi-player game to avoid the inef-ited number of CAVs without considering the traffic ficient search for global optimum, where the payoff flow. Dynamic games containing several concurrent values of the game were designed by expert-defined leader-follower pairs derived from basic traffic rules rules and further fine-tuned by deep neural networks. 

were designed by Li et al.33 to simplify the interaction The approach can help CAVs make rational decisions modeling of multiple CAVs at uncontrolled intersec-in a 2-lane lane-changing simulated scenario, com-tions. The performance of the proposed methods was pared with traditional DQN. 

4

Proc IMechE Part D: J Automobile Engineering 00\(0\) Preliminaries

It should be noted that QtotðÞ is conditioned on the global state s in equation \(3\), being consistent with the fact Decentralized partially observable Markov decision that the hypernetwork of QMIX is fed with the global process \(Dec-POMDP\)

state to generate its non-negative parameters. 

Dec-POMDP36 is the distributed multi-agent extension of the partially observable Markov decision process Sequential games \(extensive form games\) \(POMDP\), a commonly used model for representing the single-agent sequential decision-making problems Being different from the standard form game where all with partial observability that is suitable for applica-players simultaneously act according to the current situ-tions where agents only possess limited sensing capabil-ation, the decision-making of participants in sequential ities. Dec-POMDP can be defined by the tuple games hold a pre-defined order; that is, one cannot G = ðI, S, fA

make a decision until its temporally precedent player ig, T, r, fOig, O, gÞ, where I 2 RN is the set containing all distributed decision-makers, S denotes has already made a choice.38 The purpose of utilizing the overall state space underpinning the information the sequential games in this study is to encourage CAVs each agent can partially observe. The individual’s to interact with HDVs pro-socially and avoid interac-action space is defined by A

tion deadlock between CAVs. 

i, and the joint action space

is represented by the Cartesian product of the action Intuitively, Nash Equilibrium \(NE\), specifically pure space of each agent, A = 3

strategy NE, is a pure strategy profile for a normal iAi. a 2 A instantiates one

possible overall action taken by the population. T char-form game where no agent has the incentive to deviate. 

acterizes the joint state transition probability function. 

However, NE is insufficient for sequential games since The reward function is denoted by r, generating only a one may encounter the non-credible threat problem.39

scalar. The tuple also explicitly denotes a set of joint Fortunately, 

Subgame

Perfect

Nash

Equilibrium

observations by O = 3

\(SPNE\) provides an opportunity to tackle this problem iOi, constructed by the individual observation space O

and a more robust solution for sequential games. A i for agent i 2 I. The element

O : S3A3O \! ½0, 1, 

describes

the

probabilistic

subgame is a part of the sequential game composed of observation-emitting function, and the last element, g, a particular non-terminal node and all subsequent deci-denotes the discount factor. 

sion outcomes made from that node. SPNE means that QMIX can be seen as an extension of deep Q-learn-the strategy profiles of all participants form a NE in ing11 in the multi-agent cooperative setting with CTDE

every single subgame of the original game, and strate-architecture. The essence of QMIX is to derive the total gies must be credible and optimal at every stage of the Q value from the individual Q values following the game. The modeling of the pairwise sequential game Individual-Global-Max \(IGM\) principle,37 stating that established by CAVs and conflicting game opponents the greedy action selection of individual agents can lead in mixed-autonomy traffic is expanded in Methodology to the global optimal joint action. The corresponding section. 

formula shows in equation \(1\):

0

1

argmax

Problem formulation

a Q1ðt1, a1Þ

1

B

. 

C

argmax

An isolated non-signalized intersection scenario, featur-aQtotðt, aÞ =

. 

@

. 

A

ð1Þ

ing four road segments and each segment comprising argmaxa QNðtN, aNÞ

N

four lanes \(two dedicated for outgoing traffic and two for incoming traffic\), is established with a mixed-Moreover, the IGM principle should be strictly autonomy traffic flow of HDVs \(300 veh/h/lane\), as enforced by one that

follows

the

monotonicity

depicted in Figure 1. The traffic density value is referred constraint:

to the corresponding parameters from the study of Vinitsky et al.27 The SG-QMIX policy supervises a pre-

∂Qtotðt, aÞ ø 0, 8i 2 I

ð2Þ

determined number of CAVs \(8 CAVs\) and their longi-

∂Qiðti, aiÞ

tudinal acceleration, with each controlled CAV aligning with one incoming lane on each road arm. The lateral The loss function of QMIX is defined in the follow-trajectories of CAVs are kept unchanging. The primary ing equation:

focus of this paper is on the cooperative decision-making of CAVs in locally dense mixed traffic flows, X

b



h

i

where CAVs interact with other CAVs and HDVs. 

2

LðuÞ =

ytot Q ð

Þ

ð3Þ

i

tot t, a, s; u

Therefore, controlling the leading CAV in each lane is i = 1

typical of this complex scenario. Naturally, one can extend the methods examined in this study to cases where b denotes the batch size when executing mini-where an HDV is present ahead of each CAV. In such batch gradient descent to update the parameters of the situations, the CAV’s behavior can be determined by 0

0

0

networks, ytot = r \+ g max

, a , s ; u , and u

combining the car-following and sequential game mod-a0 Qtot t

describes the target Q networks similar to that in DQN. 

els. The task’s success rate is set to 100% when each



Guo et al. 

5

between the i-th vehicle and its non-conflicting neighbors is denoted by di

. The auxiliary observations, 

min

fi

and fi , describe the binary state that one CAV

enter

out

enters or drives out of the intersection \(set to 1\) or not \(set to 0\). Consequently, the global state space is s = ½oiN

. 

i = 1

Regarding the reward function, the following three facets are considered: 1\) efficiency reward, 2\) collision penalty, and 3\) reward for entirely and partially successful trajectories. To sum up, the overall reward function is formulated as follows:

r = reff \+ rcol \+ rsucc

ð5Þ

where reff denotes the traffic efficiency, CAVs are Figure 1. Illustrations of an isolated symmetric 4-way-2-lane encouraged to drive faster than the predetermined intersection scenarios used for this study, where CAVs speed threshold. Additionally, they are slightly pushed controlled by SG-QMIX algorithm are colored in red, and HDVs colored in yellow. 

by minor penalty at each timestep: CAV passes through the junction with no collisions and X

N

0% otherwise. To sum up, the following assumptions reff = 

a1 Iðvi \\ VminÞ a2

ð6Þ

are made in the scenario design:

i = 1

a\)

The

training

phase

requires

perfect

V2V

communication. 

IðÞ denotes the indicator function, which takes b\)

Each CAV can only observe its position, speed, the value of 1 when the condition inside the parenth-and some auxiliary observations, such as the mini-eses is satisfied and 0 otherwise. Moreover, a1 repre-mum center-to-center distance from its nonsents the penalty of slow passing speed, and a2 is a conflicting neighbor. The proposed sequential small value motivating CAVs to drive faster at each game-guided actor filter can access information of timestep. The collision penalty implicitly depresses all CAVs. 

the aggressive behaviors of CAVs, and the SUMO

c\)

All CAVs have predetermined routes, and all \(Simulation of Urban MObility\) simulator can auto-vehicles involved cannot change their lanes at the matically detect crashes. This part of the reward is signal-free junction zone. 

shown as follows:

Action and observation space and reward function X

N

design are the three main components of RL problem rcol = 

a3 IðCollisionÞ

ð7Þ

formulation. In this study, the action space is defined i = 1

by the joint acceleration values of each CAV. The discretization level of the action space can be generalized where a

according to the complexity of the specific problem. 

3 denotes a significant negative penalty assigned to the whole team after a collision occurs at an intersec-Although deep Q-learning framework like DQN strug-tion. The purpose of this penalty is to strictly discou-gles with continuous action spaces, directly handling rage decisions that lead to such collisions. 

continuous action spaces introduces an infinite solution Moreover, the partially and wholly accomplished space. In practical applications, discretizing the contin-trajectories designated by the number of CAVs that uous action space and fine-tuning the discretization have already safely passed through the junction are level is one effective way of narrowing the solution provided with modest \(a

space, and improving convergence speed. Afterward, 4\) and significant reward \(the

difference between the maximum episodic length and the simulator will determine the target speed of each current timesteps elapsed\), respectively: vehicle at the next time step. The observation space comprises the following elements: rsucc = ðl0 lcurÞ IðsuccessÞ \+ a4 npass ð8Þ

oi = ½xi, yi, vi, di , fi

, fi 

ð4Þ

min

enter

out

where l0 denotes the maximum episodic length, the in which the relative position of each CAV to the center length of successfully fulfilling the task is expressed by of the junction zone and the speed is represented by lcur. The number of CAVs safely driving out of the junc-½xi, yi, vi \(i = 1, 2, . . . , 8\). The minimum distance tion is recorded by npass. 



6

Proc IMechE Part D: J Automobile Engineering 00\(0\) Figure 2. The general architecture of the SG-QMIX approach is composed of two phases: 1\) A Pairwise FCFS stimulus is employed in the preparation zone to produce a specific passing order for CAVs, facilitating subsequent collaboration, and 2\) A sequential game-guided action filter module masks out unavailable actions that are not consistent with the equilibrium of the designed sequential game. Specifically, the target game participant is first identified for the current CAV, with each vehicle having two possible actions: acceleration or deceleration. Each combination of their actions corresponds to a pair of utilities, such as h ð 12, c12Þ. 

Afterward, the available strategy pi, t for vehicle i at time t i

i output by the action filter \(algorithmically implemented by the agent network in the original QMIX\) then determines the joint action ut by the e-greedy algorithm. Then, the interactions between the i

joint actions and the environment occur, providing the state oi, t of each CAV and the team reward r at the current timestep. 

i

ti

Methodology

traffic efficiency. On the other hand, when CAVs enter into the coordination zone \(i.e. intense interaction General architecture

phase\), each CAV needs to determine the potentially The architecture of SG-QMIX illustrated in Figure 2

conflicting game opponent according to the their rela-can be divided into two phases according to the zone at tive distance, and the consequent SPNE of this estab-which CAVs are located. The motivation is to decouple lished sequential game is derived and executed through the entire problem into the collaboration among multi-backward induction introduced in the Preliminaries ple CAVs and the interaction between CAVs and section. 

HDVs. Moreover, the introduction of sequential game Regarding the neural networks in the architecture, theory enables the CAVs with interactive ability, accel-the GRU network is utilized following the original ver-erating the training speed and improving the interpret-sion of QMIX. One challenge with GRU networks is ability of the strategies to some extent. When CAVs their difficulty in capturing long-term dependencies. 

enter the preparation zone \(i.e. weak interaction phase\), Another limitation is that GRUs’ representational the priority of each CAV is determined by their initial power is less potent than LSTMs, although they have spawning conditions \(i.e. initial speed and initial dis-fewer parameters and are easier to train.40 However, tance to the junction center\). Subsequently, the CAV

since the state space in this study consists of a low-with the higher priority is temporarily triggered to enter dimensional vector composed of vehicle positions, velo-the following coordination zone first, which is inspired cities, and some auxiliary information, these limitations by the FCFS strategy \(coined as pairwise FCFS stimu-do not significantly impact the experimental results. 

lus in this study\). With the aid of the preparation zone, the coordination of CAVs at the junction could be sim-Sequential game guided action filter plified and become more efficient. It should be noted that the duration of the FCFS strategy cannot be too In this subsection, we first elaborate on how to design long. Otherwise, the stop-and-go behavior in the signa-a sequential game composed of the CAV and its game lized intersections may emerge, leading to a loss of opponent and analyze the SPNE for this game using

Guo et al. 

7

backward induction. Then, we explain the pseudo-code of the Sequential Game-Guided Action Filter. 

Algorithm 1: Sequential Game-Guided Action Filter As mentioned, the CAV needs to identify a possibly Data: The number of CAVs: N, A list H consisted of sorted conflicting game opponent \(HDV or another CAV\) four groups of potential routes \(e.g. \{\(NS, NW, SN, SE\), according to the relative distance when it enters the \(SW, NE\), \(WE, WS, EW, EN\), \(WN, ES\)\}\). Current time coordination zone. Supposed that the game opponent is t, Stimulus time for each phase Ts. Ego vehicle’s current one HDV, each player’s actions are ‘‘pass’’ and ‘‘yield,’’

speed vc, route Ri. Maximum speed constraint vmax. 

Action space with dimension K

where the former means that one chooses to speed up Result: Available actions with shield first within the relative distance threshold, and the latter 1 Set the pair-wise priorities P for all controlled CAVs, a corresponds to the fact that one starts to keep the speed permutation of H, in terms of their initial conditions \(i.e. 

or decelerate for yielding. Moreover, the utility design speed, distance to the junction center\) of the established sequential game follows several intui-2 Initialize the available actions A = ½Ai for all CAVs by

i = 1, ..., N

unmasking all elements

tive rules: 1\) Both players may encounter a substantial 3 fori = 1, . . . , Ndo

penalty if they both choose to proceed first within a 4

Determine the current zone at which ego vehicle potentially dangerous range due to the high risk of col-Vi is located, preparation zone or coordination lision; 2\) Both players may encounter minor penalty if zone

both of them choose to yield to the other within the 5

if Vi is at preparation zone then 6

forj = 1, . . . , 4do

interaction range, since the traffic efficiency may be 7

if Ri is in P½j and

compromised; 3\) The utility obtained by the vehicle j

ð 1Þ Ts \\ = t \\ j Tsthen

proceeding first is higher than the one driving through 8

Allow Vi to accelerate with greater values later. Therefore, the specific utility relationships are 9

else

10

Warn V

demonstrated in equation \(9\) supposed that the player i to decelerate or keep the

current speed

opponent is one HDV:

11

else if Vi is at coordination zone then 12

Search the target vehicle of sequential game UH \\ UH \\ UH \\ UH

11

22

21

12

Vtarget from multiple candidates, according UC \\ UC \\ UC \\ UC

to the relative distance and the zone at which 11

22

12

21

ð9Þ

UH = UC , UH = UC

candidates locate. 

11

11

22

22

UH = UC , UH = UC

13

if Vtarget is another CAV then

12

21

21

12

14

Stop updating Vtarget’s available actions at this timestep t

15

Shield the unavailable action in A A simple instance enforced by this relationship is: i deviated from

the equilibrium of the sequential game 16

else if Vtarget is HDV then

UH = UC = 10, UH = UC = 5

11

11

22

22

ð10Þ

17

Shield the unavailable action in Ai deviated from UH = UC = 5, UH = UC = 3

12

21

21

12

the equilibrium of the sequential game 18

else Shield the deceleration values speed-keeping action in Ai; 

Further, we can derive that UH , UC

is the SPNE

19

else continue; 

12

12

through backward induction, indicating that the HDV

20 return Available actions A

will always pass first when interacts with its opponent. 

However, there is a possibility that HDV yields to the conflicting CAV since HDV’s behavior is uncertain which is near OðNMÞ, where N is the total number of and diverse in real-world. Thus, both UH , UC

and

12

12





CAVs, and M is the number of potential game candi-UH , UC

are considered when this module is imple-21

21

dates around each CAV \(M4N\). Nonetheless, the mented. When the game opponent is another CAV, its sequential-based action filter may eliminate half of the action should remain unchanged in the next time step illegal actions in the action space of the original QMIX

to ensure the stationarity of the environment. In this at each timestep, consequently offsetting the extra com-case, both CAVs determine their priority based on their putations required. 

exit order from the preparation zone, and the vehicle with higher priority should pass first. In the pseudo-code shown in Algorithm 1, lines 5–10 correspond to Numerical experiments

the traffic situation of the CAV in the preparation zone Experiment settings

mentioned earlier, while lines 11–19 correspond to the action filter mechanism designed for the CAV entering Concerning the numerical experiments of this study, we into the intersection area based on the SPNE derived first train the SG-QMIX algorithm on a symmetric iso-from the simple sequential game. 

lated non-signalized intersection with four arms and Concerning the computational complexity, SG-two incoming lanes \(each arm length set to 100 m\) for QMIX is higher than the original QMIX because the each arm in SUMO. SUMO is an open-source platform additional calculations are required to decompose the for microscopic traffic simulation,41 capable of addres-entire complex interaction into pairwise sequential sing challenges related to route choice, traffic light algo-games and specify the corresponding game target, rithms, and traffic management. Additionally, the



8

Proc IMechE Part D: J Automobile Engineering 00\(0\) Table 1. Parameters of scenarios and environment. 

Parameters

Value

Scenario

Lane length

100 m

Lane width

3.2 m

Length of CAV

5 m

Maximal allowed speed of CAV

12 m/s

Initial speed of CAVs

Random

Minimal allowed speed of CAV

2 m/s

Acceleration granularity

\[0.3, 2.5, 3.5\] m/s 2

Deceleration granularity

\[20.3, 22.5, 23.5\] m/s 2

RL environment

The number of controlled CAVs

8

Discrete time step

0.2 s

Maximum episode timesteps l0

500

a1

0.5

a2

0.005

Figure 3. The simple instance of a sequential game established a3

5

by CAV and HDV, where both players have two available actions, a4

0.1

pass the junction or yield to the other participant with the C

20

designed utilities UH, UC . 

ij

ij

Table 2. Hyperparameters of algorithms. 

SUMO map of ‘‘Town05’’ provided by the CARLA simulator. The hyperparameters used in this study fol-Parameters

Value

low the commonly used MARL code framework SG-QMIX

PyMARL.45 These values are well established in exist-Total training timesteps

2,000,000

ing MARL algorithm research. All numerical experi-Optimizer

Adam

ments were conducted using a workstation with Learning rate

13103

Intel\(R\) Core\(TM\) i7-8700K CPU and NVIDIA Initial value of e in e-greedy policy 1.0

GeForce RTX 2080 GPU. As for the real-time effi-Terminate value of e

0.05

Annealing steps for e

100,000

ciency, the total time during the training phase ranges Batch size

128

from 8 to 9 h for 2,000,000 timesteps \(simultaneously The number of parallel workers

8

collecting the decision trajectories of eight processes\) in l in Q\(l\)

0.6

the workstation. Moreover, for model inference, the Target update cycle

200

time elapsed is slightly shorter than 0.001 s, and for executing an entire timestep in the SUMO simulator, the computational time is approximately 0.025 s, less Traffic Control Interface \(TraCI\) provided by SUMO

than the decision period we set \(0.2 s\). 

exhibits a convenient way to control individual vehicles within the simulation. The traffic density of HDVs is set to 300 veh/h/lane, and CAVs are initialized with Training performance and model evaluation random speed. The related parameters of this scenario The episodic return, episodic length and the success are shown in Table 1. 

rate are employed as three main metrics for compara-We compare SG-QMIX with other MARL state-oftive study. In Figure 4, these three metrics of SG-the-art and baseline algorithms, MAPPO,42 MAD

QMIX progressively converge with reducing variance. 

DPG,43 IPPO,44 and the original QMIX algorithm dur-Noticeably, the performance at the initial stage is pro-ing the training phase. The training process pauses mising even when the Q-value estimates are inaccurate every 2500 steps for five independent evaluations of the \(Figure 5\) due to the effectiveness derived from the current trained policy. To eliminate the randomness, combination of FCFS strategy and SG-guided action we train all algorithms under three random seeds. 

filter that incorporates some prior knowledge. This Afterward, the model evaluation phase assesses the phenomenon implies that SG-QMIX can quickly find trained model obtaining the maximum episodic reward. 

high-quality decision-making trajectories, increasing The parameters related to the SG-QMIX algorithm are the convergence rate. However, as the exploration goes summarized in Table 2. The second part of the experi-deep, the delayed negative impact of the current subop-ments focuses on the generalizability of SG-QMIX. 

timal decision may lead to crashes between vehicles at Hence, an isolated intersection with asymmetric road intersections, leading to a significant performance drop. 

length is introduced, with a geometry table characteriz-Moreover, it can be seen that SG-QMIX significantly ing each road arm: fNorth : 63:6m, South : 63:49m, outperforms the other approaches, where these coun-West : 54:91m, East : 46:42mg. It should be noticed that terparts all fail to fulfill the training phase except that the determination of these scenario values follows the the original QMIX exhibits signs of learning. 





Guo et al. 

9

Figure 4. The training performance of SG-QMIX and other baseline candidates \(IPPO, QMIX, MADDPG, MAPPO\), including the following metrics: \(a\) episodic return, \(b\) success rate, \(c\) episodic length. Three random seeds are utilized to overcome the randomness, where the shaded areas and the solid lines denote the variance and mean value, respectively. 

based action filter during the coordination zone. From Figure 6 \(with three random seeds are utilized to overcome the randomness\), one can see that the asymptotic performance of sgqmix\_only\_fcfs is already close to that of the complete SGQMIX algorithm, although it exhibits considerable variance. On the other hand, while sgqmix\_only\_game shows the slowest training speed and the worst asymptotic performance, it continues to learn a better strategy over time. Ultimately, the SG-QMIX algorithm achieves the best results by combining the FCFS and SPNE of established pairwise sequential games. 

The trained SG-QMIX policy is then evaluated on this scenario to supervise the speed, acceleration profiles, and fuel consumption of the controlled CAVs and Figure 5. The loss curve of SG-QMIX defined in equation \(3\). 

qualitatively determine their emergent behaviors, as shown in Figures 7 and 8. Specifically, the pair of V5

Further, we conduct an ablation study on the SG-and V7 passes the intersection first, consistent with their QMIX algorithm, where sgqmix\_only\_fcfs refers to the prioritized initial speed defined by the FCFS passing SG-QMIX algorithm that includes only the FCFS

order in the preparation phase. Then, the rest of the strategy, and sgqmix\_only\_game represents the SG-CAVs sequentially accelerate and enter into the coordi-QMIX algorithm that includes only sequential game-nation zone. At 9.4 s, V4 and V6 individually yield to





10

Proc IMechE Part D: J Automobile Engineering 00\(0\) Figure 6. The ablation study of SG-QMIX, with FCFS and sequential-game based action filter alternatively disabled, where sgqmix\_only\_fcfs refers to the SG-QMIX algorithm that includes only the FCFS strategy, and sgqmix\_only\_game represents the SGQMIX algorithm that includes only sequential game-based action filter during the coordination zone. \(a\) episodic return, \(b\) success rate, \(c\) episodic length. 

Figure 7. This figure illustrates the performance of evaluating the trained SG-QMIX Model with the maximal episodic return, containing \(a\) speed profiles, \(b\) acceleration profiles, and \(c\) fuel consumption of each CAV. 



Guo et al. 

11

Figure 8. A set of snapshots for 4-way-2-lane intersection at various timesteps illustrating the trained SG-QMIX policy. 

the target HDVs at this timestep, according to the pair-dive into the behavioral details of CAVs by combin-wise sequential game-guided filter. The interactive ing the results shown in both Figures 10 and 11. The behaviors also emerge at 11.6 s and the several conse-emergent behaviors are similar to those demon-quent timesteps \(at 14.8 s\), where the CAV pair ðV0, V2Þ

strated in the symmetric intersection, except the traf-and ðV1, V3Þ also altruistically yield to the correspond-fic efficiency is slightly reduced. 

ing game opponents. Furthermore, the last passing pair 2\)

More Complex Intersection. Zero-shot transferabil-ðV1, V3Þ chooses to accelerate with maximum value for ity or generalization is a standard limitation of a while to strive for traffic efficiency due to their signifi-reinforcement learning algorithms.46 To the best of cant ‘‘sacrifice’’ during the cooperation period, leading our knowledge, it is considerably challenging in to higher fuel consumption than other CAVs. On the the field of MARL that one can transfer without contrary, the properly achieved QMIX policy retains a further retraining models to scenarios with differ-more noisy behavior with frequent alternation of accel-ent topology, for example, a 4-way-3-lane intersec-eration and deceleration in consecutive timesteps, illu-tion scenario that includes right-turn lanes and strated in Figure 9. Additionally, one can observe that corresponding vehicles. In this case, the varied SG-QMIX policy consumes lower fuel without loss of input of the agent network for each CAV due to traffic efficiency, as shown in Table 3. 

the change in coordinates may lead to a significant gap in the output. Nevertheless, we retrained our Application to unseen scenarios

SG-QMIX approach on this scenario and recorded the model completing the coordination task as shown in Figure 12. 

1\)

Zero-Shot Transferability. To determine the zero-shot transferability of the trained SG-QMIX policy, Conclusions and future works

we deploy it on an asymmetric isolated intersection with four variously valued arm lengths, where CAVs In this study, we combine the power of FCFS strat-carry the equivalent order of initial speeds. One can egy and the equilibrium of the sequential game to



12

Proc IMechE Part D: J Automobile Engineering 00\(0\) Figure 9. This figure illustrates the performance of evaluating the trained QMIX Model with maximal episodic return, containing \(a\) speed profiles, \(b\) acceleration profiles, and \(c\) fuel consumption of each CAV. 

length, success rate, and training stability and conTable 3. Comparison between the trained SG-QMIX and vergence. The experimental results demonstrate that QMIX policies. 

the CAVs can interact with the surrounding game Method

Average

Average fuel

opponents rationally and altruistically and consume speed \(m/s\)

consumption \(mg/s\)

lower mean fuel with a negligible speed slow-down. 

Further, the generalizability of the trained SGQMIX

8.3

1055.3

SG-QMIX

8.1

990.6

QMIX policy is assessed on the signal-free intersection with various topologies. The results show that our approach can still successfully achieve the coop-filter out the invalid actions generated by the origi-eration task. 

nal QMIX algorithm as the cooperation of multiple In the future, we may continually improve the per-agents proceeds. Afterward, the proposed algorithm formance of this approach on the cooperation task by is trained on a complex cooperative decision-implicitly embedding the sequential game-guided filter making task at an isolated symmetric non-signalized into the whole architecture instead of hardcoding it. 

intersection, in which our approach beats the other Then, the more advanced policy may emerge with the baselines in terms of episodic return, episodic aid of offline MARL algorithms. 





Guo et al. 

13

Figure 10. This figure demonstrates the performance of transferring the trained SG-QMIX Model to an isolated asymmetric intersection with various lengths of road arms, containing \(a\) speed profiles of each CAV, \(b\) acceleration profiles, and \(c\) fuel consumption. 

Figure 11. A set of snapshots illustrating the zero-shot transferability of the trained SG-QMIX policy to an isolated asymmetric intersection with various lengths of road arms. 



14

Proc IMechE Part D: J Automobile Engineering 00\(0\) Figure 12. A set of snapshots for 4-way-3-lane intersection at various timesteps illustrating the trained SG-QMIX policy. 

Declaration of conflicting interests and automated vehicles. IEEE Intell Transp Syst Mag 2019; 12\(1\): 4–24. 

The author\(s\) declared no potential conflicts of interest 2. Liu W, Hua M, Deng Z, et al. A systematic survey of with respect to the research, authorship, and/or publi-control techniques and applications: From autonomous cation of this article. 

vehicles to connected and automated vehicles. IEEE

Internet Things J 2023; arXiv:230305665 2023. 

Funding

3. Dresner K and Stone P. A multiagent approach to autonomous intersection management. J Artif Intell Res The author\(s\) disclosed receipt of the following finan-2008; 31: 591–656. 

cial support for the research, authorship, and/or publi-4. Ding J, Xu H, Hu J, et al. Centralized cooperative inter-cation of this article: This work is financially supported section control under automated vehicle environment. In: by National Key Research and Development Program 2017 IEEE intelligent vehicles symposium \(IV\), pp. 972–

of China \(2022YFB2503105\) and the Institute of 977. IEEE. 

Electrical Engineering Chinese Academy of Sciences 5. Zohdy IH and Rakha HA. Intersection management via \(E1553301\). 

vehicle connectivity: The intersection cooperative adap-tive cruise control system concept. J Intell Transp Syst 2016; 20\(1\): 17–32. 

ORCID iDs

6. Isele D, Rahimi R, Cosgun A, et al. Navigating occluded Zihan Guo

https://orcid.org/0000-0003-1403-0502

intersections with autonomous vehicles using deep rein-Yan Wu

https://orcid.org/0000-0001-5185-9948

forcement learning. In: 2018 IEEE international conference on robotics and automation \(ICRA\), pp. 2034–2039. 

IEEE. ISBN 1538630818. 

7. Guan Y, Ren Y, Li SE, et al. Centralized cooperation References

for connected and automated vehicles at intersections by 1. Wang Z, Bian Y, Shladover SE, et al. A survey on coop-proximal policy optimization. IEEE Trans Veh Technol erative longitudinal motion control of multiple connected 2020; PP\(99\): 1. 

Guo et al. 

15

8. Shu H, Liu T, Mu X, et al. Driving tasks transfer using and research. In 2017 IEEE international conference on deep reinforcement learning for decision-making of robotics and automation \(ICRA\), pp. 1497–1504. IEEE. 

autonomous vehicles in unsignalized intersection. IEEE

25. Cai P, Wang H, Sun Y, et al. Dq-gat: Towards safe and Trans Veh Technol 2021; 71\(1\): 41–52. 

efficient autonomous driving with deep q-learning and 9. Wang Z, Zhuang Y, Gu Q, et al. Reinforcement learning graph attention networks. IEEE Trans Intell Transp Syst based negotiation-aware motion planning of autonomous 2022; 23\(11\): 21102–21112. 

vehicles. In: 2021 IEEE/RSJ international conference on 26. Peng B, Keskin MF, Kulcsaŕ B, et al. Connected autono-intelligent robots and systems \(IROS\), pp. 4532–4537. 

mous vehicles for improving mixed traffic efficiency in IEEE. 

unsignalized intersections with deep reinforcement learn-10. Li M, Cao Z and Li Z. A reinforcement learning-based ing. Commun Transp Res 2021; 1\(1\): 100017–100017. 

vehicle platoon control strategy for reducing energy con-27. Vinitsky E, Kreidieh A, Le Flem L, et al. Benchmarks sumption in traffic oscillations. IEEE Trans Neural Netw for reinforcement learning in mixed-autonomy traffic. In Learn Syst 2021; 32\(12\): 5309–5322. 

Conference on robot learning. PMLR, pp. 399–409. 

11. Mnih V, Kavukcuoglu K, Silver D, et al. Human-level 28. Antonio GP and Maria-Dolores C. Multi-agent deep control through deep reinforcement learning. Nature reinforcement learning to manage connected autonomous 2015; 518\(7540\): 529–533. 

vehicles at tomorrow’s intersections. IEEE Trans Veh 12. Schulman J, Wolski F, Dhariwal P, et al. Proximal policy Technol 2022; 71\(7\): 7033–7043. 

optimization algorithms. 20 July 2017. arXiv preprint 29. Wu Y, Chen H and Zhu F. Dcl-aim: decentralized coordi-arXiv:170706347. 

nation learning of autonomous intersection management 13. Yuan M, Shan J and Mi K. Deep reinforcement learning for connected and automated vehicles. Transp Res Part C

based game-theoretic decision-making for autonomous Emerg Technol 2019; 103: 246–260. 

vehicles. IEEE Robot Automat Lett 2021; 7\(2\): 818–825. 

30. Peng Z, Li Q, Hui KM, et al. Learning to simulate self-14. Lopez VG, Lewis FL, Liu M, et al. Game-theoretic lane-driven particles system with coordinated policy optimiza-changing decision making and payoff learning for auton-tion. Adv Neural Inform Process Syst 2021; 34: 10784–

omous vehicles. IEEE Trans Veh Technol 2022; 71\(4\): 10797. 

3609–3620. 

31. Nakka SKS, Chalaki B and Malikopoulos AA. A multi-15. Liu M, Wan Y, Lewis FL, et al. A three-level game-theo-agent deep reinforcement learning coordination frame-retic decision-making framework for autonomous vehi-work for connected and automated vehicles at merging cles. IEEE Trans Intell Transp Syst 2022; 23\(11\): 20298–

roadways. In: 2022 American control conference \(ACC\), 20308. 

pp. 3297–3302. IEEE. 

16. Chandra R and Manocha D. Gameplan: Game-theoretic 32. Chen D, Hajidavalloo MR, Li Z, et al. Deep multi-agent multi-agent planning with human drivers at intersections, reinforcement learning for highway on-ramp merging in roundabouts, and merging. IEEE Robot Automat Lett mixed traffic. IEEE Trans Intell Transp Syst 2023; 24: 2022; 7\(2\): 2676–2683. 

11623–11638. 

17. Tan M. Multi-agent reinforcement learning: independent 33. Li N, Yao Y, Kolmanovsky I, et al. Game-theoretic vs. cooperative agents. In: Proceedings of the tenth inter-modeling of multi-vehicle interactions at uncontrolled national conference on machine learning. pp. 330–337. 

intersections. IEEE Trans Intell Transp Syst 2020; 23\(2\): 18. Hernandez-Leal P, Kartal B and Taylor ME. A survey 1428–1442. 

and critique of multiagent deep reinforcement learning. 

34. Li D, Liu G and Xiao B. Human-like driving decision at Autonom Agents Multi-Agent Syst 2019; 33\(6\): 750–797. 

unsignalized intersections based on game theory. Proc Inst 19. Papoudakis G, Christianos F, Rahman A, et al. Dealing Mech Eng Part D J Autom Eng 2023; 237\(1\): 159–173. 

with non-stationarity in multi-agent deep reinforcement 35. Hang P, Lv C, Huang C, et al. Cooperative decision mak-learning. 11 June 2019. arXiv preprint arXiv:1906.04737. 

ing of connected automated vehicles at multi-lane mer-20. Rashid T, Samvelyan M, Schroeder C, et al. Qmix: mono-ging zone: a coalitional game approach. IEEE Trans tonic value function factorisation for deep multi-agent rein-Intell Transp Syst 2021; 23\(4\): 3829–3841. 

forcement learning. In International conference on machine 36. Amato C, Chowdhary G, Geramifard A, et al. Decentra-learning, pp. 4295–4304. PMLR. ISBN 2640–3498. 

lized control of partially observable markov decision pro-21. Sunehag P, Lever G, Gruslys A, et al. Value-decomposi-cesses. In: 52nd IEEE conference on decision and control, tion networks for cooperative multi-agent learning based pp. 2398–2405. IEEE. ISBN 1467357170. 

on team reward. In: AAMAS ’18: Proceedings of the 17th 37. Son K, Kim D, Kang WJ, et al. Qtran: Learning to factor-international conference on autonomous agents and multia-ize with transformation for cooperative multi-agent reinfor-gent systems, pp. 2085–2087. 

cement learning. In: International conference on machine 22. Hu J, Jiang S, Harding SA, et al. Riit: Rethinking the learning, pp. 5887–5896. PMLR. ISBN 2640-3498. 

importance of implementation tricks in multi-agent rein-38. Gibbons R, et al. A primer in game theory. New York: forcement learning. The Second Blogpost Track at ICLR

Harvester Wheatsheaf, 1992. 

2023. arXiv preprint arXiv:210203479 2021. 

39. Leyton-Brown K and Shoham Y. Essentials of game the-23. Candela E, Parada L, Marques L, et al. Transferring ory: a concise multidisciplinary introduction. Springer multi-agent reinforcement learning policies for autono-Nature, 2022. 

mous driving using sim-to-real. In: 2022 IEEE/RSJ inter-40. Chung J. Empirical evaluation of gated recurrent neural national conference on intelligent robots and systems networks on sequence modeling. 

11 December 2014. 

\(IROS\), pp. 8814–8820. IEEE. 

arXiv preprint arXiv:1412.3555. 

24. Paull L, Tani J, Ahn H, et al. Duckietown: an open, inex-41. Lopez PA, Behrisch M, Bieker-Walz L, et al. Microscopic pensive and flexible platform for autonomy education traffic simulation using sumo. In: 2018 21st international

16

Proc IMechE Part D: J Automobile Engineering 00\(0\) conference on intelligent transportation systems \(ITSC\), agent challenge? arXiv preprint arXiv:2011.09533. 18

pp. 2575–2582. IEEE. 

November 2020. 

42. Yu C, Velu A, Vinitsky E, et al. The surprising effec-45. Samvelyan M, Rashid T, de Witt CS, et al. The starcraft tiveness of PPO in cooperative multi-agent games. 

multi-agent challenge. In: AAMAS ’19: Proceedings of the Adv Neural Inform Process Syst 2022; 35: 24611–

18th international conference on autonomous agents and 24624. 

multiagent systems, pp. 2186–2188. 

43. Lowe R, Wu YI, Tamar A, et al. Multi-agent actor-critic 46. Dulac-Arnold G, Levine N, Mankowitz DJ, et al. Chal-for mixed cooperative-competitive environments. Adv lenges of real-world reinforcement learning: definitions, Neural Inform Process Syst 2017; 30: 6382–6393. 

benchmarks and analysis. Mach Learn 2021; 110\(9\): 44. De Witt CS, Gupta T, Makoviichuk D, et al. Is inde-2419–2468. 

pendent learning all you need in the starcraft multi-



