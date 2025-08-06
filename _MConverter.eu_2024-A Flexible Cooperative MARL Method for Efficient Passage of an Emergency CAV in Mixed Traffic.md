8898

IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 25, NO. 8, AUGUST 2024

A Flexible Cooperative MARL Method for Efficient Passage of an Emergency CAV in Mixed Traffic Zhi Li , Qichao Wang, Junbo Wang , Member, IEEE, and Zhaocheng He

Abstract— Connected and autonomous vehicles offer the possi-control \[2\], lane sequence selection advice \[3\] as well as coop-bility to carry out control strategies, thus having great potential erative and semi-cooperative control \[4\], \[5\]. And they have to improve traffic efficiency and road safety. The efficient potential to improve traffic efficiency and road safety \[4\], \[6\], 

passage of an emergency vehicle calls for the collaborative driving decision-making among multiple vehicles in a dynamically which are even more promising for emergency vehicles \[5\]. 

changing local area. However, existing work fails to efficiently During the emergency rescue process of accidents, emergency adapt to dynamic and complex traffic conditions, thus cannot vehicles such as ambulances, police cars and fire engines have well solve the task. For better solution, we propose a flexible the mission to provide timely emergency service, thus playing cooperative multi-agent reinforcement learning approach based an vital role in mitigating the consequences of traffic accidents on value function factorization, called Q-LSTM. Since the traffic environment is partially observable, the centralized training and and improving the operational efficiency of the transportation decentralized execution paradigm is adopted to learn effective system. Therefore, it is important to develop efficient driving cooperative strategies for individual agents. To flexibly adapt strategies for autonomous emergency vehicles with priority in to the changing neighborhood condition around the emergency intelligent transportation system, which is also one of the main vehicle, we introduce a long short-term memory network to objectives of emergency management. 

decompose the learned global value function into local value function of each agent within the neighborhood, whose quantity To realize prioritized traffic control for emergency vehicles, and entities vary over time. To address the credit assignment several kinds of researches have been carried out including problem and realize different roles of the emergency and regular traffic signal priority control \[7\], \[8\], emergency vehicle vehicles, reward mechanism and the way agent-wise Q-networks routing \[9\], \[10\], and cooperative driving control \[5\], \[10\]. 

update are well-designed. Extensive experiments are conducted A routing decision support system based on fuzzy logic infer-on the Simulation of Urban MObility platform. Results show that our Q-LSTM outperforms state-of-the-art value-based MARL

ence is designed to help generate shortest congestion-aware methods. Moreover, the robustness and adaptability of the route \[9\]. To clear a path for the emergency vehicle, optimal Q-LSTM are verified in the cases of increased traffic density. 

merging trajectories for vehicles in front are generated based Index Terms— Connected and autonomous vehicle, motion on A∗ searching algorithm and an integer linear programming planning, cooperative decision-making, multi-agent reinforce-approach \[10\]. A semi-cooperative control strategy for an ment learning. 

autonomous emergency vehicle based on game theory with an iterative best response algorithm is proposed in \[5\] to obtain I. INTRODUCTION

trajectories that satisfy Nash Equilibrium. 

RECENTLY, the rapid advancements of autonomous However, since they are limited by the rules manually driving and wireless communication technologies have designed, the time-consuming computations or the too ideal brought about the emergence of connected and autonomous assumption condition, it is hard for these approaches to handle vehicles \(CAVs\). Meanwhile, it is anticipated that mixed a more complex and changing traffic scenarios. 

traffic of autonomous vehicles \(AVs\), CAVs and human-driven In mixed traffic of HVs and AVs, conventional microscopic vehicles \(HVs\) will exist for a long period of time in the near models involving car-following models \[11\], \[12\], \[13\], \[14\], 

future \[1\]. The CAVs offer the possibility to carry out control

\[15\], \[16\] and lane-changing models \[17\], \[18\], \[19\], \[20\], 

strategies such as variable speed limit control, lane-changing

\[21\], \[22\] have been designed to describe the interactions between vehicles and the resulting traffic flow dynamics \[6\]. 

Manuscript received 5 July 2022; revised 23 July 2023 and 29 March 2024; accepted 20 May 2024. Date of publication 24 June 2024; date of However, the flexibility and accuracy of these methods current version 1 August 2024. This work was supported in part by the based on the fitting of calibration data are limited in AVs National Natural Science Foundation of China under Grant 62072485 and in decision-making. To tackle the aforementioned limitations, part by Shenzhen Science and Technology Research Foundation under Grant JCYJ20230807110802005. The Associate Editor for this article was M. Wang. 

deep reinforcement learning \(DRL\) has been widely applied in \(Corresponding author: Junbo Wang.\)

motion planning for autonomous driving and optimization for Zhi Li, Junbo Wang, and Zhaocheng He are with Guangdong Provincial Key mixed traffic flow. Combining deep neural networks and rein-Laboratory of Intelligent Transportation Systems, Guangdong Provincial Key Laboratory of Fire Science and Intelligent Emergency Technology, School of forcement learning \(RL\) algorithms, DRL enables the agents to Intelligent Systems Engineering, Sun Yat-sen University, Shenzhen 518107, learn decision-making strategies by interacting with complex China \(e-mail: lizh337@mail2.sysu.edu.cn; wangjb33@mail.sysu.edu.cn\). 

environments, thus possessing better generalization capability. 

Qichao Wang is with the School of Computer Science and Engineering, Sun Yat-sen University, Guangzhou 510006, China. 

Considering the interactions among participants, the traffic Digital Object Identifier 10.1109/TITS.2024.3411487

environments can be regarded as multi-agent systems \(MAS\) 1558-0016 © 2024 IEEE. Personal use is permitted, but republication/redistribution requires IEEE permission. 

See https://www.ieee.org/publications/rights/index.html for more information. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:41:57 UTC from IEEE Xplore. Restrictions apply. 

LI et al.: FLEXIBLE COOPERATIVE MARL METHOD FOR EFFICIENT PASSAGE

8899

\[23\], where a variety of multi-agent reinforcement learning

•

A training framework for heterogeneous agents is devel-

\(MARL\) techniques are adopted to handle it. Decentralized oped, where the emergency agent maintains a Q-network control policies are designed by adopting an independent of its own, while regular agents share another Q-network Q-learning \(IQL\) algorithm to increase the throughput of a together. In this way, they can fulfill different roles during bottleneck in \[24\], where all agents share the same controller. 

decentralized execution. 

To deal with multi-agent cooperative decision-making prob-The remainder of this paper is organized as follows. 

lem, many research results \[25\], \[26\], \[27\], \[28\], \[29\], \[30\], 

Section II summarizes the related research work. Section III

\[31\], \[32\], \[33\] have been achieved. However, few of them describes and formulizes the studied cooperative driving prob-have studied dynamic complex interactions among vehicles. 

lem. The MARL model for this problem is introduced in Yu et al. make an initial contribution in adopting dynamic Section IV. Section V presents the proposed MARL method coordination graphs to model the changing topology in traffic by giving the details of the overall architecture and the training and coordinate maneuvers among a group of vehicles \[30\], 

algorithm. Section VI provides the settings of the simulation whereas the multi-agent models are trained in a fixed number experiments and discusses the performance and interpretability of agents. Moreover, these works aim at the problems of of the proposed model. Finally, Section VII concludes the homogeneous vehicles. 

paper. 

Due to the aforementioned shortcomings, the existing approaches are not able to well solve the problem of cooper-II. RELATED WORK

ative decision-making for autonomous driving in emergency The existing related work includes studies on MARL algo-traffic scenarios. From the macro traffic environment point rithms for learning cooperation, MARL approaches for of view, emergency traffic may involve multiple emergency autonomous driving, approaches for handling collaboration vehicles. However, due to the locality of the interaction among among a variable number of agents under centralized train-vehicles, the coordination between an emergency CAV and ing, and aggregating information from a variable quantity of regular CAVs within its neighborhood is the core situation in entities, as well as investigations on lane-changing coupling emergency traffic scenarios. 

process of CAV in mixed traffic environment. 

Therefore in this paper, we focus on the collaborative driving control problem for an emergency CAV’s fast passage. 

Thus the research scenario focuses on the local traffic envi-A. MARL for Learning Cooperation

ronment within the neighborhood of the emergency CAV. This There are mainly three different training paradigms for problem faces the following challenges handled with MARL. 

MARL. One is the centralized control which trains policy

•

It confronts the inherent problems of MARL including network mapping from joint observations to actions of all the non-stationary problem of the environment from each agents \[35\]. Though it avoids the non-stationary problem, agent’s local perspective, and the credit assignment prob-it has difficulty in exploration for the exponential increase lem in the system \[34\]. 

of joint action space dimension as the number of agents

•

Owing to vehicular mobility and dynamic traffic condi-increases. Another is decentralized learning where each agent tion, the number of regular vehicles around the emergency independently learns an individual policy, as in IQL \[36\]. 

vehicle varies over time, which leads to the problem of While it has advantage in terms of scalability, it leads to unfixed input of the neural network during the centralized non-stationary environment and cannot explicitly represent training process. 

interaction between agents \[37\]. Nonetheless, the IQL often

•

The vehicles in mixed traffic flow are heterogeneous, serves as a surprisingly strong baseline in practice \[37\], which

which play different roles, i.e., the emergency CAV is is used as a baseline for comparison in this paper as well. The expected to traverse through the road as quickly as paradigm in between is centralized training with decentralized possible, while regular CAVs in its neighborhood should execution \(CTDE\) \[34\]. Owning to its combination of benefits assist it. Other CAVs and all HVs are considered part of of the other two paradigms, it is adopted in this study to learn the complex changing environment. 

cooperative driving strategy for each CAV agent from global In order to tackle these challenges, this paper proposes perspective in the research scenario. 

a cooperative MARL algorithm, called Q-LSTM, with cen-There are two categories of methods with the frame-tralized training and decentralized execution \(CTDE\) based work of CTDE, involving centralized critic-based and value on value function factorization. The main contributions are decomposition-based methods. With regard to centralized threefold:

critic-based methods, Lowe et al. \[38\] presents a multi-agent

•

A flexible value function factorization method based deep deterministic policy gradient \(MADDPG\) algorithm on long short-term memory \(LSTM\) network, Q-LSTM, which addresses the non-stationarity and the problem of expo-is proposed to integrate information from a variable nential growth of action space. But it suffers from the linear number of agents in the neighborhood of the emergency growth of critic network’s input space with the increase of vehicle for centralized training. 

agents \[38\]. So a remedy of only taking into account agents

•

An effective reward mechanism is well-designed to within a neighborhood of a given agent is advisable in prac-address the credit assignment problem, which enables tice \[38\]. Nonetheless, there are still many models involved in agents to contribute to the fast passage of the emergency MADDPG, which affects training speed. Concerning another vehicle with priority and the smoothness of local traffic. 

inherent challenge of the credit assignment, Foerster et al. \[39\]

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:41:57 UTC from IEEE Xplore. Restrictions apply. 

8900

IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 25, NO. 8, AUGUST 2024

proposes counterfactual multi-agent \(COMA\) policy gradients multi-stage multi-agent \(CM3\) RL. Yu et al. \[30\] focus on to evaluate the contribution of each agent’s action to the modeling the changing topology during vehicle interaction joint-action value function. However, it is not suited to scale to coordinate maneuvers of a group of five vehicles, using because of the often large joint-action spaces. Besides, it is dynamic coordination graphs. Schutera et al. \[31\] consider

sample-inefficient due to on-policy learning. 

the influence of distributed decision-making based on transfer To overcome the constrained scalability issue and better learning and multi-agent learning on traffic flow respectively, utilize CTDE to learn the global optimal policy and make the results of which demonstrate that multi-agent learning it available for the agents to make decisions based on only approach possesses an edge in scenarios with more intelligent their own observations in partially observable environment, traffic agents. In order to tackle the problem of unstable value decomposition-based solutions of learning a centralized training due to the updates of other agents in parameter but factored joint-action value function are proposed. In value sharing which is widely adopted in the above research, decomposition networks \(VDN\) \[40\], the joint-action value Cicek et al. \[32\] present an algorithm of MARL with periodic function is additively decomposed into value functions of parameter sharing \(MARL-PPS\) for highway cooperative nav-agents, and the joint reward is assumed to be the summation igation. Kaushik et al. \[33\] extend parameter sharing to deep of each agent’s counterpart, so as to prevent existence of the deterministic policy gradients \(DDPG\) for continuous control

“lazy agents” and ameliorate cooperative MARL. However, of the vehicles. 

it has limitation in representation complexity of the global However, almost all of these works on autonomous driv-value functions. Therefore, \[37\] further puts forward a QMIX

ing are conditioned on the assumption of homogeneity, and approach which treats the overall action-value function as non-conducted in some way of parameter sharing. Moreover, few linear combination of individual value functions, constrained of them have studied dynamic complex interactions among by monotonicity of the relationship between the two. Nonethe-vehicles, except \[30\]. But the multi-agent models are trained less, it fails to represent more complicated decompositions as in a fixed number of agents in \[30\]. 

well as handle the situations where the numbers of agents do not remain constant. Since the cooperative driving task C. Approaches for Handling a Variable Number of implicates non-monotonic joint action-value function, which Agents or Entities

requires coordination and yielding, and the quantity of agents Though MARL is widely used for AVs’ motion plan-in the neighborhood of the emergency vehicle varies over time, ning, a problem due to the traffic dynamics is found a novel gathering method for global action-value function is under-researched in this area, i.e., cooperative driving within presented in this work. 

a variable number of vehicles via centralized training, which necessitates efforts to seek novel solutions in intelligent trans-B. MARL for Autonomous Driving

portation system. 

MARL algorithms for collaborative settings are widely Nevertheless, from respect of MARL, recent relevant works applied in strategic decision making and motion planning for have been carried out. Iqbal and Sha \[43\] propose an autonomous driving where complex interaction among AVs actor-critic method for effective and scalable learning where a and HVs is involved, for they enable the vehicle agents to shared attention mechanism is used by each agent for selecting learn optimal driving strategies to achieve the goals, and can relevant information from other agents to estimate its value utilize the generalization capability of the neural network, function. Lately, a value decomposition-based approach for thus adaptable for complex traffic scenarios. In unsignalized variable sized groups of agents is presented in \[44\], which

intersection scenario, Chen et al. \[26\] propose a framework is an extension of QMIX \[37\] that incorporates entity-wise to solve the problems of delay of agents and environmental feedforward layers and attention mechanism. QPLEX \[45\] and

non-stationarity based on delay-aware multi-agent deep deter-Qatten \[46\], which are two variants of QMIX, use variants ministic policy gradient \(DAMA-DDPG\) algorithm, where of the attention mechanism as the mixing networks. Finally, continuous longitudinal acceleration of the vehicles is decided in order to handle a variable number of obstacles with different by the policies. On a one-lane roundabout scenario with distance to the agents, an LSTM layer is designed in \[47\]

three entrances, Bacchiani et al. \[27\] model the longitudinal to aggregate the state information of the obstacles in reverse behavior of vehicles taking into account interactions with order of distance. Inspired by these studies, this paper put others through extended asynchronous advantage actor-critic forward a novel value function decomposition-based algorithm \(A3C\) algorithm \[41\]. 

integrated with an LSTM mechanism to develop cooperative There are more works applied to highway scenarios. 

driving strategy in the complex traffic scenario. 

Wang et al. \[25\] propose a harmonious lane-changing mechanism based on deep Q-networks \(DQN\) \[42\] with parameter sharing, which balances individual and overall traveling effi-D. Lane-Changing Coupling Process of CAV in Mixed Traffic ciency. R˘adulescu et al. \[28\] study safe driving strategies of The CAV lane-changing models or merging algorithms a variable number of homogeneous agents via transferring involved in this line include rule-based and RL-based ones. 

knowledge from a single-agent model and further tuning Rule-based lane-changing approaches allow this maneuver the network of multi-agent policy. Yang et al. \[29\] investi-only if relevant constraints are met, which include con-gate cooperative driving decision-making towards individual straints on longitudinal acceleration change \[48\], \[49\], and

goals and collective collaboration under cooperative multi-goal constraints on speed difference and longitudinal spacing \[50\], 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:41:57 UTC from IEEE Xplore. Restrictions apply. 





LI et al.: FLEXIBLE COOPERATIVE MARL METHOD FOR EFFICIENT PASSAGE

8901

etc. Peng et al. \[48\] explore the effect of different types of lane changes conducted by CAV with different types of vehicles around on car-following during the lane changes and optimize the lane-changing model MOBIL for CAVs via the particle swarm algorithm to enable more flexible lane changes and better traffic situation with higher operation speed. Hou et al. \[50\] propose a hierarchical model for Fig. 1. 

Schematic diagram of the system model. Note that for symbolic cooperative on-ramp merging control in multilane freeway representation succinctness, the subscript t are omitted for all symbols except the lane symbol. 

merging areas, where one of the observations made shows the impact of CAV penetration rate on mainline traffic effi-TABLE I

ciency improvement is more significant under higher rates, i.e., 

> 

NOMENCLATURE LIST FOR SYSTEM MODEL

60%. To examine the impacts of CAV in mixed traffic, Ramsahye et al. \[49\] develop a two-dimensional microscopic traffic model by considering different vehicle types of leader and follower, and obtain optimum model parameters by a local search method coupled with a Lipschitizian optimization algorithm, employed on the Waymo dataset. A game theory-based ramp merging algorithm is proposed in \[51\] for CAVs in mixed traffic, which improves system mobility, reduces fuel consumption under different traffic demands and CAV

penetration rates. However, the \(variants of\) rule-based or game theory-based approaches proposed in the above studies do not address the intelligence of CAVs and are not sufficiently flexible in complex environments. 

In contrast, RL is able to learn from interacting with environment and seek optimal actions for longer-term efficiency \[1\]. A cooperative lane-changing strategy based on enhanced Q-learning is developed in \[1\] to improve traffic efficiency on a three-lane highway stretch with an on-ramp and off-ramp, which suggests the presence of CAVs significantly improves traffic flow, average speed, and traffic capacity. 

Intelligent Driver Model \(IDM\) \[11\] is adopted to describe the Nevertheless, the Q-learning with Q table becomes infeasible car-following behavior of them. 

when dealing with large state spaces. In this work, we use Thus the cooperative driving control problem focuses on the neural networks as the Q-value approximators, and develop local traffic within the neighborhood of the emergency CAV. 

an MARL-based cooperative driving strategy involving longi-Each CAV agent in the neighborhood makes a lane-changing tudinal and lateral movements for efficient emergency driving decision whether to switch lane or to keep lane, as well as an in mixed traffic while ensuring road safety and maintaining acceleration decision whether to speed up or to slow down, traffic smoothness. 

at each time step. The task of the problem requires the emergency CAV to move as quickly as possible, with the regular III. PROBLEM FORMULATION

CAVs around it assisting it, while maintaining the smoothness The system model of the studied collaborative driving control of local traffic under the premise of road safety. The planning problem for the emergency CAV’s fast passage is depicted horizon T is the total travel time of the emergency CAV, which in Fig. 1. There are three lanes on the road. The traffic is is discretized into T time steps \(t ∈ \{1, . . . , T \}\) with the a mix of CAVs and HVs. The emergency vehicle and some control/update interval 1t = 0.1s. Other symbols used in the of the regular vehicles are CAVs, the other regular vehicles system model are defined in Table I. 

are HVs. 

Based on the above description, the problem can be for-Since it is unnecessary and impractical to coordinate all mulized as follows. 

vehicles in the system to improve the efficiency of emergency response, we assume that vehicles far away from the emer-A. Objective Function

gency CAV have little impact on it, and the driving cooperation The objective is to optimize the efficiency of the emergency is only required in the neighborhood with a certain radius CAV, while improving the smoothness of local traffic. The centered on the emergency CAV to realize the passing assis-speed of vehicle is used as the measure of both \[52\] to derive tance for it. Owing to dynamics of the traffic flow, the specific the objective function as:

entities and quantity of the regular vehicles moving around T

the emergency CAV change over time. When the CAVs are X

X

max

\(w

\+

w \), 

\(1\)

running within the neighborhood of the emergency CAV \(as 1ve

t

2vit

t =1

−e

shown in Fig. 1\), they are regarded as controllable CAV agents. 

i ∈Nt

As for the CAVs outside the neighborhood and the HVs, the where w1 ≫ w2, making the optimization more targeted. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:41:57 UTC from IEEE Xplore. Restrictions apply. 

8902

IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 25, NO. 8, AUGUST 2024

1

j

j

B. Safety Distance Constraint

pr ec\( j,l \)

j

j, prec\( j,l \)

\+

\(u

t

− u \)\(1t\)2 \+ d

t

, \(g\)

2

t

t

t

To avoid rear-end collisions, vehicles should keep a suf-j

j, prec\( j,l \)

t

ficient distance from their preceding vehicles when traveling, d

≥

\+ v j

t

dC AV

0

t T0, 

\(h\)

whether following or changing lanes, which should not be less t ∈ \{1, . . . , T \}, 

\(i\)

than the safety distance, calculated as follows \[11\]:

i ∈ \{e\} ∪

−e

N

, 

t

\(j\)

dt ≥ dsa f e = d0 \+ vit T0, 

\(2\)

j ∈ N, 

\(k\)

C. Lane Change Constraint

IV. MARL MODEL

The CAV agent can only choose one of the adjacent lanes The above optimization problem is a sequential decision-of its current lane for lane change at each time step, which making problem, and the driving actions performed by the can be expressed as:

vehicles at the current time step will affect the system state at the next time step. Since the RL is a classical method for li ∈ \{

t

0, 1, 2\}, 

\(3\)

sequential decision-making, which has distinct advantages in li −

≤

\+

decision-making optimization, we solve it with a proposed t

1 ≤ li

li

1, 

\(4\)

t \+1

t

MARL method used to control the CAV agents in the emer-where \{0, 1, 2\} represents the set of the three lanes. Further-gency vehicle’s neighborhood. 

more, the agent can only perform the lane change if there is Based on the assumption of Markov property and par-no collision at each time step. 

tial observability of the traffic environment, the cooperative driving task can be formulated as a decentralized partially D. Speed Constraint

observable Markov decision process \(Dec-POMDP\) \[53\], 

The absolute value of the acceleration of a vehicle at each

\[54\], where multiple agents within the neighborhood of the time step should not exceed the maximum acceleration, and emergency agent learn cooperative driving strategies from the speed of a vehicle at each step should not exceed its desired interaction with the environment. At every stage, each vehicle speed, which can be formulated as:

agent takes a driving action only based on its own observation. 

Then the environment responds to these actions, presenting

|ui | ≤

t

amax , 

\(5\)

new state to the agents, as well as giving the reward which vi ≤ v

the agents pursue maximizing over time in the process of t

## 0. 

\(6\)

sequential decision-making. 

The Dec-POMDP can be defined as a tuple G

=

E. State Update

⟨N, S, A, P, O, O, r, γ ⟩, where N = \{1, . . . , n\} denotes the The initial speed of a vehicle is set to 30 km/h. And the set of n vehicle agents in which a CAV is indexed by i ∈ N, update of the vehicle speed and the distance between vehicles s ∈ S indicates the state of the traffic environment, s′ ∈ S

for two consecutive time steps can be calculated as follows: indicates the next state of s, a ∈ A represents the joint actions vi

in which ai represents the action of vehicle i , P describes the

= min\{vi \+ ui 1t, v

t \+1

t

t

0\}, 

\(7\)

conditional transition probabilities between the states, o ∈ O

1

di,i−1 = \(vi−1 − vi \)1t \+ \(ui−1 − ui \)\(1t\)2 \+ di,i−1, \(8\) denotes the joint observations where oi denotes the observation t \+1

t

t

2

t

t

t

of vehicle i , O describes the conditional observation probabil-where i − 1 denotes the preceding vehicle of vehicle i , ities Pr\(o|a, s′\), r indicates immediate reward function shared as illustrated in Fig. 1. 

among the vehicle agents, and γ ∈ \[0, 1\) is the discount factor. 

Therefore, with the above objective function and constraints, The task aims to seek optimal policy, i.e., the optimal action

. 

the problem can be formulated as the following mixed-integer sequence, to maximize the expected discounted return Gt =

j

nonlinear programming \(MINLP\) model, where li PT

t and ut are

γ k−tr

k=t

k . The action-value function for policy π \(a|s\) is defined as the decision variables in the optimization problem. 

Qπ \(s, a\) .= Eπ \[Gt | St = s, At = a\] . 

\(9\)

T

X

X

max

\(w1ve \+

w \), 

And the optimal joint policy maximizes the above action-value t

2vit

\(MINLP\)

t =1

i ∈ −e

function:

Nt

s.t. 

li ∈ \{

t

0, 1, 2\}, 

\(a\)

Q∗\(s, a\) . 

= max Q

π

π \(s, a\). 

\(10\)

li −

≤

\+

t

1 ≤ li

li

1, 

\(b\)

t \+1

t

The state and observation space, action space, as well as i, prec\(i,li

\)

d

t \+1

≥

\+ vi

reward function are illustrated as follows. 

t

dC AV

0

t T0, 

\(c\)

r ear \(i,li

\),i

\)

d

t \+1

≥

t

d0 \+ vrear\(i,lit\+1

t

T0, 

\(d\)

A. State and Observation Space

j

|u | ≤

t

amax , 

\(e\)

The observation space is assumed to be the same as the v j

j

= min\{v j \+ u 1t, v

state space and can be determined from the state. As shown t \+1

t

t

0\}, 

\(f\)

in Fig. 2, the observation of vehicle i at time t with a certain j

j

j, prec\( j,l \)

\)

d

t

= \(v prec\( j,lt − v j \)1t

range is designed as the concatenation of six vectors, a relative t \+1

t

t

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:41:57 UTC from IEEE Xplore. Restrictions apply. 





LI et al.: FLEXIBLE COOPERATIVE MARL METHOD FOR EFFICIENT PASSAGE

8903

change actions are set to be separated from the acceleration or deceleration action, the speed variation involved in the lane change can still be implemented by an action sequence including the speed control decisions made before and after the time step at which the lane change is performed. 

C. Reward

In RL \[54\], the goal of a task or agent is formalized as the reward. The agent learns the optimal policy with the goal of maximizing the expected discounted return \(cumulative reward\). In order for the agents to achieve the joint objective of our research problem \(as shown in Eq. \(1\)\), we need to provide Fig. 2. 

An illustration of the observation of vehicle i . 

them with well-designed rewards. Therefore, according to the theoretical analysis with the reference MINLP model, distance to the emergency vehicle 1di,e

we design the corresponding specific reward function. 

t

, and the speed of

vehicle i . The vectors consist of two one-hot vectors, li The joint reward function formalizes the joint objective t , l e

t , 

indicating the current lanes of vehicle i and the emergency \(Eq. \(1\)\) of the task, as shown in Eq. \(13\). For each r it in i, f

vehicle respectively, two vectors, dl,i

Eq. \(13\), the reward function with linear combination form t

, dt , representing abso-

lute distances to the preceding and the following vehicles on shown in Eq. \(14\) is designed according to the state and/or the three lanes respectively, and two vectors, 1vl,i action of vehicle i at time step t , where the six conditions t

, 1vi, f

t

, 

denoting the relative speeds of vehicle i and its leading, considered and their corresponding rewards are shown in following vehicles respectively. The observation vector is then Table II:

expressed as:

1 X

rt = w1re \+

w , 

t

2r it

\(13\)

h

i, f

i

nt

oi =

, , 

, 

, 1vl,i, 1vi, f , 1

, vi , 

−e

t

lit let dl,i

t

dt

t

t

di,e

t

t

\(11\)

i ∈Nt

r i = σ

\+ σ

\+ σ

\+ σ

\+ σ

\+ σ

, \(14\)

where l and f denote the preceding and following vehicles t

Dr iD

Ar iA

L r iL

Sr iS

P r iP

C r iC

of vehicle i on the three lanes respectively, e indicates the where rt represents the joint reward received at time step t, rit emergency vehicle, p and v represent the longitudinal position \(i ∈ \{e\} ∪

−e

Nt \) represents the reward received by vehicle i at i, f

f

and speed of the vehicle, dl,i =

−

=

−

time step t , n

t

plt

pit , dt

pit

pt , 

t denotes the number of regular CAVs within the 1vl,i = vl − vi

= vi − v f

=

−

emergency CAV’s neighborhood at time step t . The weight for t

t

t , 1vi, f

t

t

t

and 1di,e

t

pit

pet with

positive and negative values indicating that vehicle i is in front the reward term of the emergency vehicle w1 is set much larger of the emergency vehicle and behind it respectively. 

than that of regular ones w2, i.e., w1 ≫ w2. σD, σA, σL , σS, σP

If there is no vehicle in front or at the back of vehicle i and σC are binary variables, which take the value of 1 when within the observation range, the corresponding elements of the conditions corresponding to their subscript symbols \(as distance and relative speed in the state vector are set to the shown in Table II\) are met, and take the value of 0 otherwise. 

length of the observation radius l

r i , r i , r i , r i , r i , r i indicate the rewards or penalties received obs and zero respectively, 

D

A

L

S

P

C

as illustrated in Fig. 2, where there is no vehicle ahead of by vehicle i , the choices of the specific values for which will the vehicle i in the adjacent right lane. The value l be detailed in Subsection VI-B. 

obs for

the distance is set according to the fact that at least there is Since we set w1 ≫ w2, maximizing the expected discounted no vehicle within the observation radius. And the setting for return should enable regular CAVs to make driving decisions the relative speed has little impact on the decision-making of that assist the fast moving of the emergency CAV, for its speed vehicle i while keeping the state definition valid. 

increase brings a greater contribution to the joint reward. 

As for the observation of the emergency vehicle, i = e in In the polynomial, the terms about C and P reflect the Eq. \(11\), and the first two lane indicators are the same vectors safety distance constraint in Eq. \(2\) between the front and rear concatenated together. 

vehicles, the term on S reflects the speed constraint in Eq. \(6\), 

the term on L is designed to reduce unnecessary lane changes, and the term about A and D is designed to encourage vehicles B. Action Space

to increase their speed until the desired speed is reached. 

Considering longitudinal and lateral motions, the action of vehicle i at time step t is one element selected from the action D. State Update

set A, which is described as:

Given the speed, position and action of vehicle agents i at ai ∈

t

A = \{acc, dec, le f t, right, keep\} , 

\(12\)

time step t , the speed and position are updated based on the kinematic point-mass model as follows:

where acc and dec denote acceleration and deceleration respectively, le f t and r ight represent changing to the left vi

= min\{vi \+ ui 1t, vi \}, 

\(15\)

t \+1

t

t

0

lane and right lane with current speed respectively, keep 1

indicates keeping the current lane and speed. Though the lane pi

= pi \+

\(vi \+ vi \)1t, 

\(16\)

t \+1

t

2

t

t \+1

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:41:57 UTC from IEEE Xplore. Restrictions apply. 

8904

IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 25, NO. 8, AUGUST 2024

TABLE II

CONDITION DEFINITIONS AND THE CORRESPONDING REWARDS

where uit denotes the acceleration or deceleration correspond-QMIX \[37\] further puts forward a value function factorization ing to the chosen action of vehicle i at time step t . 

method where a mixing network conditioned on global state information is used to estimate the joint action-value function V. MARL METHODOLOGY

as non-linear monotonic combination of individual action-value functions. However, the network structure limits the Since the existing approaches are hard to quickly adapt to the number of inputs to the mixing network to be fixed \[44\]. More-

complex changing traffic, we propose a flexible cooperative over, it cannot represent non-monotonic functions underlying MARL based on an LSTM network for value function decom-complex coordination tasks. 

position, called Q-LSTM, aiming at addressing collaborative As the number of agents to be controlled by the MARL

driving among a variable number of heterogeneous vehicles. 

model near the emergency vehicle varies over time, and The Q-LSTM adopts the training paradigm of CTDE. And the driving coordination required is complex, a novel value the DQN-style loss with regard to joint reward and joint decomposition method is proposed in this work. The popular action-value is used for the network parameters learning with QMIX and VDN are included in state-of-the-art \(SOTA\) experience replay similar to that in DQN \[42\]. In this section, baselines for comparison with our algorithm in section VI. 

we first introduce the preliminaries required for understanding 3\) LSTM \[55\]: The gated architecture LSTM plays a part our method, and then present the proposed Q-LSTM. 

in facilitating learning over sequence data of different lengths. 

Having a sequential network structure with gate units, the A. Preliminaries

network can store input information in memory cell and 1\) CTDE: On the one hand, centralized training has access transmits it along the chain. Therefore, LSTM possesses the to the global information, thus overcoming the non-stationary function of gathering information, which is utilized in this environment problem of MARL, improving the learning effi-work for aggregating the action-value functions. Since later ciency, and helping the agents learn better cooperative driving input information is more likely to have a greater influence on strategy from interaction with the traffic environment. More-the final output of the hidden state, and agents with different over, in order to evaluate the overall effect of the driving spacings from the emergency vehicle have different influence behaviors of each agent, a global joint action-value function on it, relating the order of inputs to the different spacings Qtot for all agents within the neighborhood of the emergency enables the spacing to be taken into account in the aggregation vehicle is needed during centralized training, which conditions of the action-value functions. 

on the global state and the joint action. On the other hand, due 4\) DQN \[42\]: Combining RL with deep learning \(DL\), to the partial observability of the traffic environment, and to DQN utilizes deep neural networks as the action-value func-avoid the exponential growth of the joint action space with tion approximators. There are two key approaches introduced. 

the increase of the agents, decentralized driving policies of The first is the utilization of replay memory, storing expe-the agents are required for their selecting only the individ-riences \(st , at , rt , st\+1\) at each time step t. During learning, ual actions, which are conditioned on the local individual experience replay is performed by randomly sampling mini-observations only. Therefore, a value function factorization batches of experiences from the replay memory to update algorithm under CTDE is required for the solution of the parameters θ of the network Q. The correlations between the studied problem. 

samples are then broken and sample efficiency is improved. 

2\) Value Factorization: In order to learn the decentralized The second is the use of target network ˆ

Q parameterised by θ−

Q-networks in a centralized way under the paradigm of to compute the target values for Q. ˆ

Q is periodically updated

CTDE, value decomposition networks are proposed. VDN \[40\]

by the network Q, thus enhancing stability of the algorithm. 

evaluates the joint action-value function Qtot \(τ, a\) assuming During training, the network Q is updated via optimizing the that it is the summation of individual action-value functions loss function as:

Qi \(τ i , ai \), which can be expressed as:

L\(θ\) = E\[\(r \+ γ max Q\(st\+1, at\+1; θ−\) − Q\(st , at ; θ\)\)2\]. 

n

at\+1

X

Qtot \(τ, a\) =

Qi \(τ i , ai ; θi \), 

\(17\)

\(18\)

i =1

where τ = τ 1, . . . , τ n represents a joint action-observation B. Overall Architecture

history. While it is able to scale across a variable number Based on the aforementioned work, we put forward a of agents, its function representation capability is limited. 

flexible value decomposition network architecture Q-LSTM

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:41:57 UTC from IEEE Xplore. Restrictions apply. 





LI et al.: FLEXIBLE COOPERATIVE MARL METHOD FOR EFFICIENT PASSAGE

8905

Fig. 3. 

Architecture of the proposed Q-LSTM method for MARL in emergency fast passing. Note that for symbolic representation succinctness, some time subscripts are omitted and the superscript ′ is used to denote time step t \+ 1. 

Second, regarding the training for the overall Q-LSTM

model, we adopt the technique of experience replay and the idea of setting separate target Q-network similar to that in DQN \[37\], \[42\] to stabilize the training. A replay memory is used to store experiences \(ot , at , rt , ot\+1\), where the joint observation ot\+1 is observed after the agents perform the action at under the observation ot and receive the joint reward rt . The network parameters are learned by randomly sampling minibatches of K experiences from the replay memory and minimizing the squared TD error during end-to-end training: K

X

L\(θ\) =

\(ytot − Q

k

t ot \(ot , at ; θ \)\)2, 

\(19\)

k=1

where ytot = r

ˆ

t \+ γ maxa

Q

t \+1

t ot \(ot\+1, at\+1; θ −\). θ − are the

parameters of a target network, which are periodically copied Fig. 4. 

The relationship among CTDE, DQN and LSTM. 

from those of the evaluate network θ. Eq. \(19\) is similar to the standard DQN loss of Eq. \(18\). 

Third, different from the existing relevant work, we take for cooperative MARL under the paradigm of CTDE. The advantage of the flexibility of LSTM network in process-proposed architecture is built on decentralized agents with ing variable-length sequence data and propose the flexible Q-networks, enhanced with a flexible LSTM network for Q-LSTM method based on value function decomposition individual action value aggregation to estimate the joint action-under CTDE to solve cooperative driving problem involving values, thus being adaptive to the coordination among a a varying number of vehicle agents over time. The LSTM

variable number of agents within the emergency vehicle’s network plays a role in aggregating the information of agents neighborhood. The overall architecture is shown in Fig. 3, 

with unfixed number to form the global joint action-values which consists of the SUMO \[56\] simulation environment of Qtot at each time step. 

the research scenario and the proposed MARL model. 

On the whole, the proposed Q-LSTM represents the cen-1\) The Relationship Among CTDE, DQN, and LSTM in Q-tralized joint action-value function Qtot \(o, a\) with a value LSTM: The relationship among the three concepts involved in factorization network architecture consisting of agent-wise the proposed Q-LSTM algorithm is illustrated in Fig. 4. 

Q-networks and an LSTM network, conditioned on agent-wise First, the proposed Q-LSTM algorithm adopts the popular individual observations. 

framework for cooperative MARL, CTDE. In this framework, 2\) Agent-Wise Q-Network: The Q-network of each agent, agent-wise decentralized policies based only on their local containing three fully connected layers, takes only local observations are learned in a centralized way, where global observation as input and outputs individual action-value func-information, including joint reward and joint action-value of tion corresponding to each action Qi \(oi , ai \). Decentralized all agents, can be leveraged for more effective training. 

policies are extracted from the learned action-value function Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:41:57 UTC from IEEE Xplore. Restrictions apply. 





8906

IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 25, NO. 8, AUGUST 2024

Qtot \(o, a\), which derives from the agents’ performing greedy action selections with respect to their individual action-value functions, i.e. choosing the actions that maximize the action-value functions. 

3\) The LSTM Network: At each training step, the LSTM

network with four hidden layers \(64 neurons for each layer\) takes as input sequences of agent-wise information vectors

\[x1, x2, . . . , xn\], where each vector xi is obtained by concatenating the local observation and the local action value of a controlled CAV agent, i.e. concat\(\[oi , Qi \]\), and outputs total action values Qtot . The LSTM also takes local observations Fig. 5. 

An example illustrates the input sequence of the LSTM network. 

as input, which is to consider the influence of agent-wise observations on the aggregation of individual action values. 

The length of the above-mentioned input sequences is In LSTM block, the forget gate and the output activation variable because the number of CAV agents within the emer-function are the most critical components \[57\]. The ability the gency CAV’s neighborhood in different states may vary \(take forget gate possesses to forget old information appears to be the experimental statistics shown in Fig. 6 as an example\). 

crucial to the LSTM \[57\]. The agent-wise information input Since the LSTM network is incorporated in the Q-LSTM for to the LSTM block at the later timestamps undergoes fewer individual Q-value mixing, the Q-LSTM is capable of handling times of selective information filtering by the forget gate in collaborative driving among a variable number of CAV agents, the forward pass, so it is easier to be retained in the memory which is a flexible model. 

cell state. Finally, the cell state is output under the action of To distinguish different influences of different agents with the output gate, which should have captured the information distinct distances from the emergency vehicle on the collab-inputs at the later timestamps relatively efficiently. 

orative decision-making process, we consider the input order Based on the above understanding towards the LSTM archi-of the agent-wise information for the LSTM elaborated in the tecture, we input the agent-wise information of the regular following subsection. The process of the LSTM network is CAVs closer to the emergency CAV into the LSTM later, expressed as follows:

so that the process of generating global Qtot can capture it more easily and pay more attention to it. 

 x



i ′ = concat\(\[oi ′ , Qi ′ \]\)

To summarize, the agent-wise data is fed in reverse order of







 z = tanh\(W · \[x

the distance, which is analogous to the idea in \[47\]. And the



i ′ , hi ′−1\]\)







data of the emergency vehicle is fed last as it should be taken

 zi = σ \(W i · \[xi ′ , hi ′−1\]\)







into account the most. An example is shown in Fig. 5, where

 z f = σ \(W f · \[xi′ , hi′−1\]\)

\(20\)

the vehicles are sorted by the distance from the emergency zo = σ \(W o · \[x



i ′ , hi ′−1\]\)



vehicle, and the agent-wise information input sequence is from





 c



i ′ = z f · ci ′−1 \+ zi · z

the one of vehicle No. 5 to that of vehicle No. 1. 







 h



i ′ = zo · tanh \(ci ′ \)







 Qtot = W ′hn′ , 

D. Training Algorithm

The optimization of the networks’ parameters is conducted where i ′ ∈

′

N = 1, . . . , n′ indicates the order of input, xi′

by minimizing the loss, as shown in line 24 of Algorithm 1, 

represents the input of vehicle agent i ′, concatenating its local during end-to-end training. 

observation oi′ and its action-value function Qi′ , h indicates Since the driving strategy and objective of the emergency the hidden state, tanh and σ represent tanh and sigmoid CAV is to pass as fast as possible, and that of regular CAVs is activation functions, z is obtained through transformation of to assist the fast passage of the emergency CAV with a certain the input using tanh activation function, zi , z f and zo denote tolerance for the loss of their own speed, we apply a training the gated states of the input gate, forget gate and output gate, approach to learn two sets of network parameters to achieve respectively, c is the cell state, hn′ indicates the last hidden the heterogeneity, where the emergency CAV updates its own state, which is fed into a fully connected layer to generate the agent Q-network by itself while regular ones share the agent joint action-value function Qtot . 

Q-network parameters together in the proposed algorithm. 

The full algorithm for training is shown in Algorithm 1. 

C. Input Order of the LSTM

We adopt the technique of experience replay and the idea of Since the CAV agents closer to the emergency CAV have a setting separate target Q-network similar to that in DQN \[42\]. 

greater impact on it in terms of driving behavior decision-We first initialize the agent Q-network Qem for the emer-making, more information of them needs to be considered gency vehicle and Qreg for regular vehicles, as well as the when generating the global joint action-value function Qtot LSTM network Qtot with random parameters θem, θreg and with the LSTM network for centralized training, which is the θtot respectively \(line 1-2\). The target networks of them are final output of the network. In other words, the hidden state initialized with the same parameters as their counterparts of the last timestamp in the LSTM needs to contain more \(line 3\). The replay memory D is initialized with capacity information about them. 

M \(line 4\). For each episode, the state of the environment Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:41:57 UTC from IEEE Xplore. Restrictions apply. 

LI et al.: FLEXIBLE COOPERATIVE MARL METHOD FOR EFFICIENT PASSAGE

8907

Algorithm 1 Q-LSTM Algorithm for MARL

a minibatch of K experiences is randomly sampled for the 1: Initialize emergency agent’s and regular agents’ action-optimization of the networks via minimizing the loss function value functions Qem and Qreg with random parameters with regard to the joint action-value function with gradient θem and θreg

descent \(line 18-25\). And we adopt soft target updates \[58\]

2: Initialize LSTM network Qlstm with random parameters for the target networks’ parameter updates \(line 26\). The joint θlstm

action-value function is obtained from the LSTM network 3: Set θ = \{θem , θreg, θlstm \}, and initialize target agent which takes concatenations of each agent’s observation and Q-network ˆ

Qem, ˆ

Qreg and target LSTM network ˆ

Qlstm

its scalar Q-value as inputs \(line 20-21\). 

with parameters θ− = θ

VI. E

## 4: Initialize replay memory D with capacity M

### VALUATION AND DISCUSSIONS

5: for episode=1,. . . ,E do

Extensive experiments are carried out on a three-lane highway 6:

Initialize state of environment st = s1 and get observa-simulation environment in Flow \[59\] based on SUMO \[56\] to

tions of agents oi =

t

oi

evaluate the performance of our proposed Q-LSTM algorithm, 1

## 7:

for t = 1, . . . , T do

and demonstrate the effectiveness of our approach to achieve 8:

for i = 1, . . . , n do

reliable and adaptive cooperative driving decision-making 9:

With veh\[i\]=emergency veh. set Qi = Qem

among a variable number of CAVs for an emergency CAV’s 10:

Otherwise set Qi = Qreg

fast moving in mixed traffic flow. 

## 11:

Randomly select an action ait with probability ϵ

## 12:

Otherwise select ai =

, 

A. Experimental Settings

t

arg maxQi \(oit ai \)

ai

The surrounding environment of the emergency vehicle is 13:

Execute ait

taken into account the neighborhood with the radius of 300 m. 

## 14:

### end for

As cooperative decision-making control is required to imple-15:

Observe reward rt , state st\+1 and get observation ment within the neighborhood only, the CAVs running out of ot\+1

the local area are distinguished from the ones inside, which are 16:

Store experience \(ot , at , rt , ot\+1\) in D

not controlled by the MARL model. In the following, we refer 17:

if len\(D\) = M then

to the CAVs outside the neighborhood and the HVs along the 18:

Randomly sample a minibatch of K experiences \(

road as non-RL vehicles. Note that the driving mode of a ot , at , rt , ot\+1\) from D

CAV will switch when it drives into or out of the emergency 19:

for each time step t in each experience in mini-vehicle’s neighborhood. 

batch K do

In this subsection, the driving behavior modeling for 20:

xi =

, 

\]\)

t

concat\(\[oit Qit , 

non-RL vehicles is first presented, followed by the settings of ˆ

xi

= concat\(\[oi

, Qi \]\)

t \+1

t \+1

t \+1

vehicle model parameters and vehicle generation. Then details 21:

Qtot \(ot , at ; θ\) = LSTM\(x1, . . . , 

\)

t

x n

t

, 

of the elements in the proposed MARL model and the training ˆ

Qtot \(ot\+1, at\+1; θ−\) = LSTM\( ˆx1 , . . . , ˆxn \) t \+1

t \+1

settings are elaborated. 



 rt

if t = T

1\) Car-Following Models for Non-RL Mode: The IDM \[11\]

## 22:

ytot =

r

îs employed to model the car-following behavior of non-RL

t \+ γ max Qtot

otherwise. 



at\+1

vehicles, which is mathematically described as follows: 23:

end for

## 24:

Loss L\(θ\) = PK \(ytot − Q

vn

, 1vn−1,n\)

k=1

k

t ot \(ot , at ; θ \)\)2

un = a

t

t

max \[1 − \(

\)δ − \(d∗\(vnt

\)2\], 

\(21\)

## 25:

Perform a gradient descent step on L\(θ\) w.r.t. θ: t

v0

dn−1,n

θ

t

← θ − η∇θ L\(θ\)

where δ represents acceleration exponent, dn−1,n 26:

Update target network parameters:

t

indicates the

θ− ← \(1 − α\)θ− \+ αθ

spacing between vehicle n and its leading vehicle n − 1, and d∗\(vn, 1vn,n−1\) denotes the desired gap between the vehicles 27:

end if

t

t

which is defined by:

## 28:

### end for

## 29: end for

vn1vn,n−1

d∗\(vn, 1vn,n−1\) =

t

t

√

\), 

t

t

d0 \+ max\(0, vntT0 \+

\(22\)

2 amax b

where

b

represents

the

comfortable

deceleration. 

The

is first initialized, and each agent gets its observation oi at car-following dynamics of the CAVs and the HVs are dis-1

the beginning \(line 6\). Then the procedure is divided into two tinguished by the minimum gap d0, which takes the value of parts: sampling and learning. An ϵ-greedy policy is employed dC AV for the CAVs and d H V for the HVs. 

0

0

for each agent’s selecting and executing an action ait at 2\) Vehicle Model Parameters: The values of parameters each time step to balance exploitation with some degree of taken for the vehicle models are listed in Table III. 

exploration \(line 8-13\). Subsequently, the environment emits 3\) Vehicle Generation and Distribution: With regard to a reward and transfers to a new state from which the agents the generation of vehicles, the initial speed of a vehicle is receive new observations \(line 15\). The experiences at each set to 30 km/h. We set three traffic densities of 20 veh/km, time step et = \(ot , at , rt , ot\+1\) are then stored in the replay 30 veh/km and 40 veh/km. In addition to an emergency CAV, memory D \(line 16\). After the experience pool is filled, the ratio of the other CAVs to the HVs is three to two. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:41:57 UTC from IEEE Xplore. Restrictions apply. 



8908

IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 25, NO. 8, AUGUST 2024

TABLE III

PARAMETERS OF VEHICLE MODELS

Fig. 7. 

Left: Average speed of the emergency vehicle under different reward parameter combinations for collision and acceleration. Right: Average speed of the emergency vehicle under different penalty values for lane changing. 

TABLE IV

Note that the figure is plotted using mean and standard deviation with 95%

HYPER-PARAMETERS FOR MARL MODEL

confidence interval on five episodes. 

avoiding collisions and speeding, we reward the acceleration \(A\) action by setting its reward value to a positive value. 

In order to encourage vehicles to travel as fast as possible at the desired speed and to give it the maximum speed reward when it reaches the desired speed, the reward on speed r i is set to D

be related to vi − vi

t

, where vi

0

t is the actual speed of vehicle

i at time t , vi is its desired speed. For the penalties, we first 0

analyze their relative magnitude for it is more important compared to the absolute size of each value. Specifically, for collision \(C\), potential rear-end collision \(P\) and speeding \(S\), we set |r i | > |ri | > |ri | according to their severity. Lane C

P

S

changing \(L\) is allowed, but frequent lane changes may reduce the efficiency of the traffic flow \[25\]. So we consider setting a smaller penalty for it. 

We then explore the approximate choices of the values Fig. 6. 

Number of CAVs within the emergency CAV’s neighborhood under in the reward function through preliminary experiments. Due the traffic density of 30 veh/km from the Q-LSTM implementation. 

to the many reward terms involved, we first set the values for 4\) Settings of the Proposed MARL Model: For the CAVs the two less severe situations as: −0.8 for P and −0.6 for in the neighborhood, the acceleration and deceleration for the S, before determining the values for C, L and A via multiple actions acc and dec available are set to 2 m/s2 and −2 m/s2, experiments. A grid search is then carried out for the optimal respectively. And the weights in the joint reward function are combination of the penalties for C and L, and the reward for A. 

set as w

The search step used is initially larger, and then it is reduced 1 = 30 and w2 = 1 for the emergency CAV and

regular CAVs respectively. As for the hyper-parameters of the around the current optimum for further search. The average MARL model, details are shown in Table IV. 

speed of the emergency vehicle over five episodes in the 5\) Comparative Experiments: We compare our proposed inference phase is taken as the criterion for the choice, which Q-LSTM with the strong baseline IQL \[36\] and the SOTA is primarily optimized in our problem. Results are shown in value decomposition-based methods including VDN \[40\], 

subfigures in Fig. 7 for clear presentation, where the values in QMIX \[37\], QPLEX \[45\] and Qatten \[46\]. 

the sets of r i = \{−2.00, −1.75, −1.50, −1.25, −1.00, −0.75, C

Note that as mentioned earlier, since the mixing network

−0.50, −0.25, 0.00\}, r i = \{1.000, 1.375, 1.750, 2.125, 2.500, A

structure of QMIX limits the number of agent-wise inputs to 2.875, 3.250, 3.625, 4.000\}, and r i = \{−0.50, −0.40, −0.30, L

a fixed one, based on the statistical results of the changing

−0.20, −0.15, -0.10, −0.05, 0.00\} are evaluated. Based on number of CAVs in the neighborhood from the Q-LSTM

the experimental results, approximate optimal values of −1, implementation under the traffic density of 30 veh/km, shown

\+2.5, −0.1 are selected for C, A, L. 

in Fig. 6, we set the number of controlled CAVs in the Thus, proper values for the reward terms are determined, neighborhood to 15 for QMIX training, so as to include the as presented in Table II. Note that the denominator vi in ri 0

D

CAVs involved under different states as much as possible. 

for the speed difference is used to scale the value so that it is Other experimental settings are consistent with those of the consistent with others in magnitude. 

Q-LSTM. 

C. Validation of the Need to Control Rear Vehicles B. Choices of Specific Reward Values

Although controlling only the regular CAVs ahead of the Since the goal of the problem is to maximize the speed of emergency CAV may further reduce the complexity of our CAVs within the neighborhood of the emergency vehicle while problem, we consider the CAVs behind the emergency CAV

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:41:57 UTC from IEEE Xplore. Restrictions apply. 

LI et al.: FLEXIBLE COOPERATIVE MARL METHOD FOR EFFICIENT PASSAGE

8909

Fig. 9. 

Average single-step reward \(left\) and action value Q \(right\) under the traffic density of 20 veh/km. 

Fig. 8. 

Average speed of the emergency vehicle, and the number of lane changes it performs over 20 epochs, in the settings of controlling and not controlling rear CAVs under the traffic densities of 30 veh/km and 40 veh/km. 

around slightly above 14, the algorithm can be considered to Note that the bold lines indicate the average speeds, and the thin lines indicate converge after about 200 episodes. The rewards of the other the lane-changing frequencies. 

methods grow rather slowly and are just able to reach lower in its neighborhood because of some special cases, such as levels, especially the poorest IQL, which does not involve the following. Suppose the emergency CAV is located in the cooperation mechanism. 

middle lane, and there are HVs traveling in front of it in the Seeing that the reward curves are somewhat noisy, we use middle lane and the right lane, resulting in its inability to a more stable metric, the estimated action-value function Q, pass more quickly, while there is a CAV approaching from to evaluate the algorithm performance and stability of the behind in the left lane within the neighborhood, which is able learning process, as done in \[60\]. Q estimates how much to be controlled by the proposed MARL-based control model. 

expected discounted return the agents can get by following In this case, since the HVs are not controlled by the MARL

their policies from any given state. We randomly select a model, the CAV behind the emergency one in the left lane state and fix it. Then the corresponding fixed observations needs to make a collaborative deceleration action to assist the are fed into the MARL model, which estimate the joint-emergency CAV in passing with priority, so that the emergency action values, after the parameter updates of each episode. 

CAV can quickly change lanes and overtake to get out of the We track the maximum predicted value for the state at each predicament and achieve accelerated passage. 

episode and plot them in the right subfigure in Fig. 9. The We conduct the comparison pre-experiments with the set-results show that Q-LSTM outperforms other methods in tings of controlling and not controlling rear CAVs in the the model performance. Compared to the average reward the neighborhood. Fig. 8 compares the two settings in terms of agents obtain, the predicted Q-value soars in the early stage, the average speed and the lane-changing frequency of the then increases and converges in a much more smooth way emergency CAV under the traffic densities of 30 veh/km and without noticeable fluctuations, indicating the algorithm is 40 veh/km. The results show that with the CAVs behind stable during training. 

the emergency vehicle controlled, the moving speed of the The results of the reward and the action-value both suggest emergency CAV increases, and its lane-changing frequency is that the proposed Q-LSTM significantly outperforms other reduced. The above demonstrates the need for the proposed SOTA methods in terms of the convergence rate and the MARL model to consider the cooperation of the rear CAVs effectiveness of the algorithm. 

in the emergency CAV neighborhood. 

2\) Value Function Visualization: We select a ten-step segment of the cooperative driving task during testing for the D. Result Analysis

visualization of the learned global action-value function, Comparative experiments are conducted under different traf-as exhibited in Fig. 10. It shows that the predicted joint-action fic densities to verify the advantages of our proposed Q-LSTM

value surges when there is a large gap in front of the in terms of the learning performance and the convergence emergency vehicle \(point A\). As the regular vehicle ahead rate of the algorithm. We first carry out experiments under changes lane to yield, the predicted value rises \(point B\). 

the traffic density of 20 veh/km, and make detailed analysis The emergency vehicle is thus able to continue accelerating of convergence, stability, interpretability and learning perfor-forward, and the value peaks when the traffic efficiency in the mance of the algorithm. On this basis, we further conduct neighborhood of the emergency vehicle reaches the maximum experiments at greater traffic densities of 30 veh/km and \(point C\). Fig. 10 demonstrates that our method manages to 40 veh/km to verify the robustness and adaptability of the learn the evolution mechanism of the action-value function for proposed model. Results are analyzed as follows. 

a complex event sequence in the cooperative driving task, and 1\) Convergency and Stability: The left subfigure in Fig. 9

the proposed model is interpretable. 

presents the single-step reward the agents receive averaged 3\) Learning Performance: The left plot in Fig. 11 depicts over all time steps within the episode during training under the the average speed of the emergency vehicle. The experimental six methods. The reward of our proposed Q-LSTM increases results show that Q-LSTM is superior to other methods in rapidly in the first 200 or so episodes, and maintains at goal attainment of the task. As can be seen from the figure, a much higher level afterwards compared to the other five the emergency vehicle travels at the much higher speed in approaches. Since the value fluctuates with limited amplitude Q-LSTM compared to other methods. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:41:57 UTC from IEEE Xplore. Restrictions apply. 



8910

IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 25, NO. 8, AUGUST 2024

Fig. 12. 

Action value Q under increased traffic densities of 30 veh/km and 40 veh/km. 

environments, we further conduct experiments under the traffic densities of 30 veh/km and 40 veh/km. It is evident from Fig. 9 and Fig. 12 that our proposed algorithm is always able to achieve the best performance among the six methods under the condition of increasing traffic density, verifying the strong robustness and adaptability of our proposed Q-LSTM. 

E. Discussions

1\) Discussion on the Markov Property: In the Dec-POMDP

of the problem, CAV agents make driving decisions based on their local observations via individual Q-networks. 

In the proposed MARL learner model, although the number Fig. 10. The top plot shows the predicted global action value Q for a ten-step segment of the driving task. The following three screenshots correspond to of CAV agents within the emergency vehicle’s neighborhood the state moments labeled by A, B and C respectively. 

varies over time, the CAV agents controlled by the model are always classified into two types, i.e., the emergency CAV

and regular CAVs. Since these two types of CAVs should present different driving strategies \(i.e., the emergency CAV is expected to travel quickly, and regular CAVs around it should assist it with its passage while having a certain tolerance for their speed loss\), while regular CAVs are assumed to have homogeneous driving behavior, we create a separate Q-network for the emergency CAV, and let all other regular CAVs in the neighborhood share another Q-network. Thus, Fig. 11. 

Left: Average speed of the emergency vehicle under 20 veh/km. 

only two sets of Q-network model parameters need to be Note that the figure is plotted using mean and standard deviation with 95%

learned during the entire training period. 

confidence interval on five random seeds. Right: The number of lane changes In the LSTM network that generates the global joint the emergency vehicle performs over 20 epochs under 20 veh/km. 

action-value function Qtot for centralized training, each cell that receives the agent-wise input of each timestamp shares the The right plot in Fig. 11 shows the number of lane changes same set of parameters. Therefore, the number of parameters the emergency vehicle performs per epoch. As the training in the overall network architecture to be learned is fixed and progresses, the lane-changing frequency under Q-LSTM drops does not reduce or increase with the exit of existing agents dramatically to roughly below 800 times, which means that or the addition of new agents, indicating the whole training the CAVs around the emergency vehicle successfully learn to process is continuous. 

assist it, providing it with sufficient space for fast moving. 

Therefore, the Markov property holds in the studied system. 

However, it illustrates that training with VDN or IQL makes 2\) Discussion on the Generalization of the Reward: The relatively limited progress, where the emergency vehicle has vehicle conditions considered for the reward are the basic to change lanes more frequently. This suggests that they fail ubiquitous in traffic flow environments. Different environments to learn a more effective cooperation mechanism. 

or research problems involve different traffic operation objec-These figures suggest that our proposed reward mechanism tives. According to different objectives, combining the rewards \(detailed in Section IV\) is able to address the credit assignment corresponding to the conditions proposed in different ways, problem by enabling the emergency vehicle to gain priority or fine-tuning the specific values, can obtain different reward and fast passage with the assistance of the surrounding regular functions for different environments or tasks. The difference CAVs. Moreover, the training framework designed for hetero-between our research scenario and the general environment geneous vehicles can effectively realize different roles played mainly lies in the presence or absence of the emergency by the emergency CAV and regular CAVs. 

vehicle with the priority. If the general environment is con-4\) Robustness and Adaptability:

To examine the per-

sidered, assuming that the task objective is improving overall formance of the proposed algorithm in more challenging traffic efficiency, the joint reward function can be adjusted as Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:41:57 UTC from IEEE Xplore. Restrictions apply. 

LI et al.: FLEXIBLE COOPERATIVE MARL METHOD FOR EFFICIENT PASSAGE

8911

rt = P

r i

= σ

\+ σ

\+ σ

\+

i ∈

\[12\] W. J. Schakel, B. van Arem, and B. D. Netten, “Effects of cooperative N t , where r it

D wDr iD

Aw Ar iA

L r iL

σ

adaptive cruise control on traffic flow stability,” in Proc. 13th Int. IEEE

Sr i \+ σ

\+ σ

, w

S

P r iP

C r iC

D and w A represent the additional

Conf. Intell. Transp. Syst., Aug. 2010, pp. 759–764. 

weights given to the reward term concerning the conditions

\[13\] P. G. Gipps, “A behavioural car-following model for computer simula-D and A, N denoted the set of all vehicles in the traffic flow tion,” Transp. Res. B, Methodol., vol. 15, no. 2, pp. 105–111, 1981. 

being optimized, and the reward term corresponding to each

\[14\] L. Li, X. Peng, F.-Y. Wang, D. Cao, and L. Li, “A situation-aware collision avoidance strategy for car-following,” IEEE/CAA J. Autom. 

condition is simply the one designed in this work. 

Sinica, vol. 5, no. 5, pp. 1012–1016, Sep. 2018. 

\[15\] M. Bando, K. Hasebe, A. Nakayama, A. Shibata, and Y. Sugiyama, 

“Dynamical model of traffic congestion and numerical simulation,” Phys. 

VII. CONCLUSION

Rev. E, Stat. Phys. Plasmas Fluids Relat. Interdiscip. Top., vol. 51, no. 2, p. 1035, 1995. 

In this paper, we propose a flexible cooperative MARL

\[16\] D.-F. Xie, X.-M. Zhao, and Z. He, “Heterogeneous traffic mixing regular framework based on value function factorization using an and connected vehicles: Modeling and stabilization,” IEEE Trans. Intell. 

LSTM network for efficient passage of an emergency CAV in Transp. Syst., vol. 20, no. 6, pp. 2060–2071, Jun. 2019. 

complex, dynamic mixed traffic environment, which involves

\[17\] A. Kesting, M. Treiber, and D. Helbing, “General lane-changing model MOBIL for car-following models,” Transp. Res. Rec., J. Transp. Res. 

heterogeneous vehicles with varying quantities within local Board, vol. 1999, no. 1, pp. 86–94, Jan. 2007. 

controlled area centered by the emergency CAV. Training and

\[18\] P. G. Gipps, “A model for the structure of lane-changing decisions,” 

testing results indicate that, compared with the SOTA methods, Transp. Res. B, Methodol., vol. 20, no. 5, pp. 403–414, Oct. 1986. 

\[19\] M. Rahman, M. Chowdhury, Y. Xie, and Y. He, “Review of microscopic the proposed Q-LSTM is able to learn more effective coop-lane-changing models and future research opportunities,” IEEE Trans. 

erative driving strategy for the emergency CAV and regular Intell. Transp. Syst., vol. 14, no. 4, pp. 1942–1956, Dec. 2013. 

CAVs, which play different roles in the task. 

\[20\] T. Toledo, C. F. Choudhury, and M. E. Ben-Akiva, “Lane-changing model with explicit target lane choice,” Transp. Res. Rec., vol. 1934, Future work may cover the following directions. First, it is no. 1, pp. 157–165, Jan. 2005. 

worthwhile to investigate an adaptive mechanism for adjusting

\[21\] H. Kita, “A merging–giveway interaction model of cars in a merging the range of the controlled neighborhood of the emergency section: A game theoretic analysis,” Transp. Res. A, Policy Pract., vol. 33, nos. 3–4, pp. 305–312, 1999. 

vehicle, so that the model can dynamically adapt to changeable

\[22\] Y. Ali, Z. Zheng, M. M. Haque, and M. Wang, “A game theory-traffic conditions better. Besides, the MARL model proposed based approach for modelling mandatory lane-changing behaviour in in this paper has the potential to be extended to scenarios a connected environment,” Transp. Res. C, Emerg. Technol., vol. 106, involving multiple emergency vehicles. 

pp. 220–242, Sep. 2019. 

\[23\] S. Aradi, “Survey of deep reinforcement learning for motion planning of autonomous vehicles,” IEEE Trans. Intell. Transp. Syst., vol. 23, no. 2, pp. 740–759, Feb. 2022. 

REFERENCES

\[24\] E. Vinitsky, N. Lichtle, K. Parvate, and A. Bayen, “Optimizing mixed autonomy traffic flow with decentralized autonomous vehicles and multi-

\[1\] J. Guo, S. Cheng, and Y. Liu, “Merging and diverging impact on mixed agent RL,” 2020, arXiv:2011.00120. 

traffic of regular and autonomous vehicles,” IEEE Trans. Intell. Transp. 

\[25\] G. Wang, J. Hu, Z. Li, and L. Li, “Harmonious lane changing via deep Syst., vol. 22, no. 3, pp. 1639–1649, Mar. 2021. 

reinforcement learning,” IEEE Trans. Intell. Transp. Syst., vol. 23, no. 5, 

\[2\] T. Pan, R. Guo, W. H. K. Lam, R. Zhong, W. Wang, and B. He, pp. 4642–4650, May 2022. 

“Integrated optimal control strategies for freeway traffic mixed with

\[26\] B. Chen, M. Xu, Z. Liu, L. Li, and D. Zhao, “Delay-aware multi-agent connected automated vehicles: A model-based reinforcement learning reinforcement learning for cooperative and competitive environments,” 

approach,” Transp. Res. C, Emerg. Technol., vol. 123, Feb. 2021, 2020, arXiv:2005.05441. 

Art. no. 102987. 

\[27\] G. Bacchiani, D. Molinari, and M. Patander, “Microscopic traffic sim-

\[3\] D. Tian, G. Wu, P. Hao, K. Boriboonsomsin, and M. J. Barth, “Con-ulation by cooperative multi-agent deep reinforcement learning,” 2019, nected vehicle-based lane selection assistance application,” IEEE Trans. 

arXiv:1903.01365. 

Intell. Transp. Syst., vol. 20, no. 7, pp. 2630–2643, Jul. 2019. 

\[28\] R. R˘adulescu, M. Legrand, K. Efthymiadis, D. M. Roijers, and A. Nowé, 

\[4\] K. Li, J. Wang, and Y. Zheng, “Cooperative formation of autonomous

“Deep multi-agent reinforcement learning in a homogeneous open vehicles in mixed traffic flow: Beyond platooning,” IEEE Trans. Intell. 

population,” in Proc. Benelux Conf. Artif. Intell. Cham, Switzerland: Transp. Syst., vol. 23, no. 9, pp. 15951–15966, Sep. 2022. 

Springer, 2018, pp. 90–105. 

\[5\] N. Buckman, W. Schwarting, S. Karaman, and D. Rus, “Semi-

\[29\] J. Yang, A. Nakhaei, D. Isele, K. Fujimura, and H. Zha, “CM3: cooperative control for autonomous emergency vehicles,” in Proc. 

Cooperative multi-goal multi-stage multi-agent reinforcement learning,” 

IEEE/RSJ

Int. 

Conf. 

Intell. 

Robots

Syst. 

\(IROS\), 

Sep. 

2021, 

2018, arXiv:1809.05188. 

pp. 7052–7059. 

\[30\] C. Yu et al., “Distributed multiagent coordinated learning for

\[6\] H. Yu et al., “Automated vehicle-involved traffic flow studies: A survey autonomous driving in highways based on dynamic coordination of assumptions, models, speculations, and perspectives,” Transp. Res. C, graphs,” IEEE Trans. Intell. Transp. Syst., vol. 21, no. 2, pp. 735–748, Emerg. Technol., vol. 127, Jun. 2021, Art. no. 103101. 

Feb. 2020. 

\[7\] Q. He, K. L. Head, and J. Ding, “Multi-modal traffic signal control

\[31\] M. Schutera, N. Goby, D. Neumann, and M. Reischl, “Transfer learning with priority, signal actuation and coordination,” Transp. Res. C, Emerg. 

versus multi-agent learning regarding distributed decision-making in Technol., vol. 46, pp. 65–82, Sep. 2014. 

highway traffic,” 2018, arXiv:1810.08515. 

\[8\] N. Kumar, S. S. Rahman, and N. Dhakad, “Fuzzy inference enabled

\[32\] S. Cicek, A. Nakhaei, S. Soatto, and K. Fujimura, “MARL-PPS: Multi-deep reinforcement learning-based traffic light control for intelligent agent reinforcement learning with periodic parameter sharing,” in Proc. 

transportation system,” IEEE Trans. Intell. Transp. Syst., vol. 22, no. 8, 18th Int. Conf. Auto. Agents MultiAgent Syst., 2019, pp. 1883–1885. 

pp. 4919–4928, Aug. 2021. 

\[33\] M. Kaushik, N. Singhania, P. S., and K. M. Krishna, “Parameter sharing

\[9\] R. R. Rout, S. Vemireddy, S. K. Raul, and D. V. L. N. Somayajulu, reinforcement learning architecture for multi agent driving,” in Proc. 

“Fuzzy logic-based emergency vehicle routing: An IoT system devel-Adv. Robot., Jul. 2019, pp. 1–7. 

opment for smart city applications,” Comput. Electr. Eng., vol. 88, 

\[34\] P. Hernandez-Leal, B. Kartal, and M. E. Taylor, “A survey and critique Dec. 2020, Art. no. 106839. 

of multiagent deep reinforcement learning,” Auto. Agents Multi-Agent

\[10\] J. Wu, B. Kulcsár, S. Ahn, and X. Qu, “Emergency vehicle lane pre-Syst., vol. 33, no. 6, pp. 750–797, Nov. 2019. 

clearing: From microscopic cooperation to routing decision making,” 

\[35\] M. J. Hausknecht, “Cooperation and communication in multiagent Transp. Res. B, Methodol., vol. 141, pp. 223–239, Nov. 2020. 

deep reinforcement learning,” Ph.D. dissertation, Graduate School Univ. 

\[11\] M. Treiber and A. Kesting, “Traffic flow dynamics,” in Traffic Flow Texas Austin, 2016. 

Dynamics: Data, Models and Simulation. Berlin, Germany: Springer, 

\[36\] M. Tan, “Multi-agent reinforcement learning: Independent vs. coopera-2013, pp. 983–1000. 

tive agents,” in Proc. 10th Int. Conf. Mach. Learn., 1993, pp. 330–337. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:41:57 UTC from IEEE Xplore. Restrictions apply. 





8912

IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 25, NO. 8, AUGUST 2024

\[37\] T. Rashid, M. Samvelyan, C. S. De Witt, G. Farquhar, J. Foerster, and Zhi Li received the B.S. degree from the School S. Whiteson, “Monotonic value function factorisation for deep multi-of Traffic and Transportation, Beijing Jiaotong Uni-agent reinforcement learning,” J. Mach. Learn. Res., vol. 21, no. 1, versity, in 2019. She is currently pursuing the pp. 7234–7284, 2020. 

Ph.D. degree with the School of Intelligent Systems

\[38\] R. Lowe, Y. I. Wu, A. Tamar, J. Harb, O. P. Abbeel, and I. Mordatch, Engineering, Sun Yat-sen University. Her research

“Multi-agent actor-critic for mixed cooperative-competitive environ-interests include multi-agent systems, intelligent ments,” in Proc. 31st Int. Conf. Neural Inf. Process. Syst., 2017, transportation systems, and multi-agent reinforce-pp. 6382–6393. 

ment learning. 

\[39\] J. Foerster, G. Farquhar, T. Afouras, N. Nardelli, and S. Whiteson, 

“Counterfactual multi-agent policy gradients,” Proc. 32nd AAAI Conf. 

Artif. Intell., 30th Innov. Appl. Artif. Intell. Conf., 8th AAAI Symp. Educ. 

Adv. Artif. Intell., 2018, pp. 2974–2982. 

\[40\] P. Sunehag et al., “Value-decomposition networks for cooperative multiagent learning,” 2017, arXiv:1706.05296. 

\[41\] V. Mnih et al., “Asynchronous methods for deep reinforcement learning,” 

in Proc. Int. Conf. Mach. Learn., 2016, pp. 1928–1937. 

\[42\] V. Mnih, “Human-level control through deep reinforcement learning,” 

Nature, vol. 518, pp. 529–533, Feb. 2015. 

\[43\] S. Iqbal and F. Sha, “Actor-attention-critic for multi-agent reinforcement Qichao Wang received the B.S. degree in traffic learning,” in Proc. 36th Int. Conf. Mach. Learn. K. Chaudhuri and engineering from the School of Intelligent Systems R. Salakhutdinov, Eds., vol. 97, Jun. 2019, pp. 2961–2970. 

Engineering, Sun Yat-sen University, in 2022. He is

\[44\] S. Iqbal, C. A. S. D. Witt, B. Peng, W. Böhmer, S. Whiteson, and F. Sha, currently pursuing the master’s degree with the

“Randomized entity-wise factorization for multi-agent reinforcement School of Computer Science and Engineering. His learning,” in Proc. Int. Conf. Mach. Learn., 2021, pp. 4596–4606. 

research interests include reinforcement learning and

\[45\] J. Wang, Z. Ren, T. Liu, Y. Yu, and C. Zhang, “QPLEX: Duplex dueling graph neural networks. 

multi-agent Q-learning,” in Proc. Int. Conf. Learn. Represent., 2021. 

\[Online\]. Available: https://openreview.net/forum?id=Rcmk0xxIQV

\[46\] Y. Yang et al., “Qatten: A general framework for cooperative multiagent reinforcement learning,” 2020, arXiv:2002.03939. 

\[47\] H. Wang, T. Qiu, Z. Liu, Z. Pu, and J. Yi, “Multi-agent formation control with obstacles avoidance under restricted communication through graph reinforcement learning,” IFAC-PapersOnLine, vol. 53, no. 2, pp. 8150–8156, 2020. 

\[48\] J. Peng, W. Shangguan, and L. Chai, “Strategy of lane-changing coupling process for connected and automated vehicles in mixed traffic environment,” Transportmetrica B, Transp. Dyn., vol. 11, no. 1, pp. 979–995, Dec. 2023. 

\[49\] P. Ramsahye, S. Susilawati, C. P. Tan, and M. A. S. Kamal, “Influence Junbo Wang \(Member, IEEE\) received the B.S. and of connected automated vehicles on traffic performance at an on-ramp M.S. degrees in electrical and electronic engineer-bottleneck in the era of mixed autonomy,” Available SSRN, 2023. 

ing from Yanshan University, China, and the Ph.D. 

\[50\] K. Hou, F. Zheng, X. Liu, and G. Guo, “Cooperative on-ramp merging degree in computer science and engineering from control model for mixed traffic on multi-lane freeways,” IEEE Trans. 

The University of Aizu, Japan, in 2011. He was a Intell. Transp. Syst., 2023. 

Post-Doctoral Scholar and an Associate Professor

\[51\] X. Liao et al., “Game theory-based ramp merging for mixed traffic with The University of Aizu. He is currently an with unity-SUMO co-simulation,” IEEE Trans. Syst. Man, Cybern. Syst., Associate Professor with the School of Intelligent vol. 52, no. 9, pp. 5746–5757, Sep. 2022. 

Systems Engineering, Sun Yat-sen University, China. 

\[52\] R. P. Roess, Traffic Engineering. Washington, DC, USA: United States His research interests include collaborative ML, fed-of America, 2004. 

erated learning, fog computing, big data, and privacy. 

\[53\] F. A. Oliehoek and C. Amato, A Concise Introduction to Decentralized POMDPs. Cham, Switzerland: Springer, 2016. 

\[54\] R. S. Sutton and A. G. Barto, Reinforcement learning: An introduction. 

Cambridge, MA, USA: MIT Press, 2018. 

\[55\] S. Hochreiter and J. Schmidhuber, “Long short-term memory,” Neural Comput., vol. 9, no. 8, pp. 1735–1780, 1997. 

\[56\] M. Behrisch, L. Bieker, J. Erdmann, and D. Krajzewicz, “Sumo–

simulation of urban mobility: An overview,” in Proc. Simul 3rd Int. 

Conf. Adv. Syst. Simulation, 2011. 

Zhaocheng He received the B.S. and Ph.D. degrees

\[57\] K. Greff, R. K. Srivastava, J. Koutník, B. R. Steunebrink, and from Sun Yat-sen University, Guangzhou, China, J. Schmidhuber, “LSTM: A search space Odyssey,” IEEE Trans. Neural in 2000 and 2005, respectively. He is currently a Netw. Learn. Syst., vol. 28, no. 10, pp. 2222–2232, Oct. 2016. 

Professor with the School of Intelligent Systems

\[58\] T. P. Lillicrap et al., “Continuous control with deep reinforcement Engineering, Sun Yat-sen University, and also a learning,” 2015, arXiv:1509.02971. 

part-time Professor with the Peng Cheng Laboratory, 

\[59\] C. Wu, A. Kreidieh, K. Parvate, E. Vinitsky, and A. M. Bayen, “Flow: China. He is the Director of Guangdong Provincial A modular learning framework for mixed autonomy traffic,” 2017, Key Laboratory of Intelligent Transportation Sys-arXiv:1710.05465. 

tems. His research interests include traffic signal

\[60\] V. Mnih et al., “Playing Atari with deep reinforcement learning,” 2013, control in CVIS, multi-scale traffic flow modeling, arXiv:1312.5602. 

public transportation, and traffic big data analysis. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:41:57 UTC from IEEE Xplore. Restrictions apply.



