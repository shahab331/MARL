Downloaded from https://iranpaper.ir

https://www.tarjomano.com

https://www.tarjomano.com

5374

IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 25, NO. 6, JUNE 2024

Multi-Agent Constrained Policy Optimization

for Conflict-Free Management of

Connected Autonomous Vehicles

at Unsignalized Intersections

Rui Zhao , Member, IEEE, Yun Li , Member, IEEE, Fei Gao , 

Zhenhai Gao , Member, IEEE, and Tianyao Zhang Abstract— Autonomous Intersection Management \(AIM\) sys-I. INTRODUCTION

tems present a new paradigm for conflict-free cooperation of connected autonomous vehicles \(CAVs\) at road intersections, WITH the significant enhancement of autonomous

the aim of which is to eliminate collisions and improve the driving and internet of vehicles technology, vehicle-traffic efficiency and ride comfort. Given the challenges of infrastructure collaboration has become a promising traffic current centralized coordination methods in balancing high management solution to provide safe, effective and com-computational efficiency and robust safety assurance, this paper fortable transportation experience \[1\], \[2\]. In recent years, proposes an innovative conflict-free management scheme for various vehicle-road collaborative applications have emerged CAVs at unsignalized intersections, leveraging safe multi-agent successively \[3\], \[4\], \[5\]. As the particularly risky areas in deep reinforcement learning \(MADRL\). Firstly, we formulate the safe MADRL problem as a constrained Markov game \(CMG\) urban environments, road intersections have drawn extensive and then transform the AIM problem into a CMG by carefully attentions in dealing with serious traffic accident and severe designing state, action, reward, and cost functions. Subsequently, congestion. Autonomous Intersection Management \(AIM\) we propose the Multi-Agent Constrained Policy Optimization systems are aimed to efficiently manage multi-connected \(MACPO\), specifically tailored to solve the CMG problem. 

autonomous vehicles \(CAVs\) at intersections, eliminate col-MACPO incorporates safety constraints that further restrict the lisions, and optimize overall traffic efficiency as well as trust region formed by the Kullback-Leibler \(KL\) divergence, facilitating reinforcement learning policy updates that maximize ride comfort \[6\]. Traditionally, these AIMs handle poten-performance while keeping constraint costs within their limit tial conflicts based on control strategies such as rule-based, bounds. This leads us to introduce the MACPO-based AIM

optimization-based or machine learning-based methods to pre-Algorithm. Finally, we train an AIM policy and compare its vent anticipated conflicts from occurring \[6\], \[7\], \[8\], \[9\], \[10\], 

computation time, ride comfort, traffic efficiency, and safety with

\[11\], \[12\], \[13\], \[14\], \[15\], \[16\], \[17\], \[18\], \[19\], \[20\], \[21\], 

management schemes based on Model Predictive Control \(MPC\), 

\[22\], \[23\], \[24\], \[25\], \[26\], \[27\], \[28\], \[29\], \[30\], \[31\], \[32\], 

Mixed Integer Programming \(MIP\), and non-safety-aware reinforcement learning. According to the results, compared with the

\[33\], \[34\], \[35\]. 

MPC and MIP methods, our method has increased computational In AIM systems, conflict identification methods typically efficiency by 65.22 times and 731.52 times respectively, and include tile-based, conflict point-based, and vehicle-based has improved traffic efficiency by 2.41 times and 1.80 times approaches. The initial method produces a grid within the respectively. In contrast to the non-safety awareness RL methods, intersection, ensuring vehicles’ trajectories do not coincide our method achieves a zero collision rate for the first time, within the same grid cell simultaneously. This concept while also enhancing ride comfort, highlighting the advantages of using MACPO. 

was advanced by Dresner and Stone \[7\] who introduced a reservation-based approach where each tile in a finely seg-Index Terms— Conflict-free management, connected autono-mented grid could be claimed by only a single vehicle per mous

vehicles, 

safety

reinforcement

learning, 

multi-agent

time unit. Vehicles would request a specified arrival time, constrained policy optimization, unsignalized intersections. 

securing tiles along their intended path. This reservation-based Manuscript received 30 January 2023; revised 25 July 2023 and model was reformulated by Yu et al. \[8\] into an optimization-19 September 2023; accepted 7 November 2023. Date of publication based approach. Concurrently, Dai et al. \[9\] developed an 20 November 2023; date of current version 31 May 2024. This work intersection control model, linearizing the grid cell conflict was supported by the National Science Foundation of China under Grant avoidance constraints. Xu et al. \[10\] focused on determining 52202494 and Grant 52202495. The Associate Editor for this article was G. Wu. \(Corresponding author: Fei Gao.\)

the optimal sequence for vehicle passage in AIM, transforming Rui Zhao is with the College of Automotive Engineering, Jilin University, it into a tree-search problem. Alternatively, Wu et al. \[11\]

Changchun 130025, China \(e-mail: rzhao@jlu.edu.cn\). 

proposed a decentralized coordination approach, promoting Yun Li is with the Graduate School of Information and Science Technology, The University of Tokyo, Tokyo 113-8654, Japan \(e-mail: li-yun@g.ecc. 

safety by limiting the number of grid cells into which a vehicle u-tokyo.ac.jp\). 

could move. 

Fei Gao, Zhenhai Gao, and Tianyao Zhang are with the State Key Labo-A different class of methods substitutes tiles with conflict ratory of Automotive Simulation and Control, Jilin University, Changchun points \(CPs\), representing intersections between varying turn-130025, China \(e-mail: gaofei123284123@jlu.edu.cn; gaozh@jlu.edu.cn; tianyaz@jlu.edu.cn\). 

ing paths. Kamal et al. \[6\] introduced the notion of a CP

Digital Object Identifier 10.1109/TITS.2023.3331723

ensuring vehicles would not reach the CP simultaneously to 1558-0016 © 2023 IEEE. Personal use is permitted, but republication/redistribution requires IEEE permission. 

See https://www.ieee.org/publications/rights/index.html for more information. 

Authorized licensed use limited to: Universitaet Bielefeld. Downloaded on January 22,2025 at 07:06:33 UTC from IEEE Xplore. Restrictions apply. 





Downloaded from https://iranpaper.ir

https://www.tarjomano.com

https://www.tarjomano.com

ZHAO et al.: MULTI-AGENT CONSTRAINED POLICY OPTIMIZATION FOR CONFLICT-FREE MANAGEMENT

5375

enhance vehicular safety. Zhang et al. \[12\] devised a schedul-problem \[8\], \[17\], \[18\], \[19\], \[28\]. Moreover, Choi et al. \[29\]

ing mechanism for autonomous vehicles that is governed by and Xu et al \[30\] employed the genetic algorithm to filter the state transitions. Meanwhile, He et al. \[13\] broadened the optimal vehicle passing order. Xu et al. \[31\] crafted trajectory idea of CPs to encompass regions throughout the routes. 

planning algorithms to determine the optimal passing order Due to the spatial continuity of vehicle trajectories, in the using Monte Carlo tree. However, due to the long inference collision avoidance method consifering CPs, building a math-time associated with such methods, coupled with the fact that ematical prediction model is also more common. For instance, time consumption for solving these problems escalates almost Kamal et al. \[6\] introduced a vehicle-intersection coordination exponentially with increasing complexity, makes it challenging scheme \(VICS\) based on a model predictive control \(MPC\) to meet the real-time control demands when these methods are framework, enforcing CP avoidance constraints. Likewise, deployed at complex intersections under high traffic density Katriniok et al. \[14\] employed a distributed MPC scheme to conditions \[32\]. 

tackle the AIM problem. Chen et al. \[15\] implemented a graph-The latest advancements in machine learning, especially based approach, managing vehicle dispatch from various lanes Deep Reinforcement Learning \(DRL\), are gradually used and preventing simultaneous approaches to CPs. To simplify for optimizing traffic management \[24\], \[32\], \[33\], \[34\], 

scheduling mechanism, Wang et al. \[16\] exploited detecting

\[35\]. Multi-Agent Deep Reinforcement Learning \(MADRL\) zone and control zone for vehicle motion control. Additionally, successfully combines the advantages of Multi-Agent Rein-Yao et al. \[17\] designed a two-stage method to optimize forcement Learning algorithms and Deep Neural Networks, timing schedules and trajectories for CAVs at intersection that has the potential to solve low computation efficiency and combines the tile-based and conflict point-based approaches. 

suboptimal challenges encountered by the current AIM meth-A similar scheme can also be found in \[18\]. 

ods. In view of a reward function that describes the goal of The vehicle-based approach provides complete freedom the problem, RL agents explore their environments to learn of movement within the intersection, allowing vehicles to optimal policies that maximize the sum of future rewards choose their route to their exit lane. Mirheli et al. \[19\]

by trial and error. To enhance travel efficiency and safety at formulated the cooperative trajectory planning problem as signalized intersections, Boukerche et al. \[32\] and Zhou et al. 

mixed-integer non-linear programs that aim to minimize travel

\[33\] employed Deep Q-learning and Deep Deterministic Policy time of each vehicle, while avoiding near-crash conditions. 

Gradient algorithms to realize the optimized signal control, He et al. \[13\] addressed this by formulating the AIM prob-respectively, to achieve optimized signal control. Furthermore, lem as an optimal control model, improving computational Guan et al. \[34\] first used RL algorithm named model acceler-efficiency through discretization and enumeration of variable ated proximal policy optimization \(MA-PPO\) to automatically values. 

manage vehicles at unsignalized intersections, wherein the When conflicts are encountered, various control strategies reward function was formulated as the summation of a substan-intervene by influencing the state of vehicles, such as speed, tial collision penalty for safety considerations, and a stepped acceleration, and route, and manage the right-of-way for penalty coupled with a large passing reward for efficiency. 

vehicles at intersections. These strategies encompass a range The balance between safety and efficiency was modulated by of methods, including rule-based, optimization-based, and adjusting the weighting of their respective rewards. Similarly, machine learning-based approaches. In rule-based methods, Xu et al. \[35\] and Antonio et al. \[24\] employed a non-safety-the vehicle that arrives at the intersection first, fastest, or is in aware DRL approach, driven by a singular reward function, the longest entry queue is given the highest priority, namely to address the AIM problem. 

First-Come First-Served \(FCFS\) \[20\], \[21\], \[22\], Fast First Nonetheless, RL policies that are purely optimised for Service \[23\], or Long Queue Priority \[11\]. However, such reward maximization are rarely applicable to safety-critical predefined policies are usually difficult to obtain optimal autonomous driving applications. This presents two issues: solutions for a highly dynamic AIM system where the traf-i \) There is no perfect trade-off between “desired safety fic environment changes over time \[24\]. As pointed out by requirements” and “optimized system performance”, and it Levin et al. \[25\], FCFS based AIM may not outperform traffic can not be checked before running an RL algorithm. If the signals in terms of travel time and emission. 

penalty is designed to be very small, the agent will learn The optimization-based method emerged to bridge the lim-unsafe actions. If the penalty is designed to be very severe, itations of rule-based methods and also changed the way the agent may fail to learn anything. ii\) A fixed trade-off, of the reservation to the assignment. These methods using even one that leads to the best hazard-avoiding policy, does some heuristics like Dynamic Programming or Mixed Integer not account for a requirement to satisfy safety requirements Programming \(MIP\) where given a series of equations and throughout training and deployment. In the AIM system, conditions is used to solving AIM problem \[6\], \[8\], \[13\], 

the collaboration of CAVs should optimize other non-safety

\[14\], \[15\], \[16\], \[17\], \[18\], \[19\], \[26\], \[27\], \[28\], \[29\], \[30\], 

performances such as efficiency and comfort under the premise

\[31\]. In the context of optimal control theory, Bichiou et al. 

of ensuring safety, instead of combining safety and non-safety

\[26\] crafted an intersection control system that assigns time performance metrics into the same reward function to seek slots to each vehicle, adhering to both dynamic and static its maximization. Namely, safety is a prerequisite constraint, system constraints. Lu et al. \[27\] proposed a MIP-based rather than an aspect of system performance. 

Intersection Coordination Algorithm \(MICA\) to obtain the In order to bridge the aforementioned gap, we propose fastest crossing discrete-time trajectories for the CAVs at a conflict-free management scheme for CAVs at unsignal-intersection. To enhance solution efficiency, the AIM prob-ized intersections using safe MADRL. Firstly, we formu-lem is framed as a Mixed Integer Linear Programming late the safe MADRL problem as a Constrained Markov Authorized licensed use limited to: Universitaet Bielefeld. Downloaded on January 22,2025 at 07:06:33 UTC from IEEE Xplore. Restrictions apply. 





Downloaded from https://iranpaper.ir

https://www.tarjomano.com

https://www.tarjomano.com

5376

IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 25, NO. 6, JUNE 2024

Fig. 1. Structure of the proposed MACPO-based AIM system, comprised of two parts - EIS and PEO, designed for the monotonic improvement of intersection throughput performance including safety, efficiency, and comfort, while concurrently satisfying safety cost constraints. 

Game \(CMG\), and then present the design of state, action, 3\) Thirdly, extensive simulation is conducted and compar-reward, and cost to shape AIM into a CMG problem. 

isons with classical control methods VICS \[6\], MIP \[27\] and

Subsequently, we introduce multi-agent constrained policy non-safety aware RL method MAPPO \[34\], showcasing the optimization \(MACPO\) to tackle it. Inspired by the single-superiority of our method. 

agent-oriented constrained policy optimization \(CPO\) \[36\], our

The structure of this paper is as follows: Section II clar-approach integrates a safety constraint-satisfying eare, ensur-ifies our system model and problem statement for AIM. 

ing policy updates maximize performance without violating Section III explicates the framework of the MACPO-based safety constraints. Lastly, we train a collaborative management AIM approach. Section IV introduces how to formulate the policy in a simulation environment and benchmark its com-AIM problem via the CMG framework. Section V delves puting time, ride comfort, traffic efficiency, and safety against into the detailed exposition of the MACPO strategy and its management schemes based on MPC and MIP methods, application to the AIM system. Section VI details experimental as well as a non-safety-aware RL method. Results indicate settings and results. Lastly, Section VII concludes and dis-that, compared to MPC and MIP methods, our approach cusses research future directions. 

achieves 65.22 and 731.52 times higher computational effi-II. SYSTEM MODEL AND PROBLEM STATEMENT

ciency, respectively, and traffic efficiency increases by 2.41 and 1.80 times. Additionally, in contrast to the non-safety-aware The considered unsignalized road intersection scenario is RL method, our method attains a zero collision rate along with depicted in Fig. 1, and its topology is a typical four-way inter-enhanced passenger comfort. 

section with multiple lanes. The intersection is systematically The main contributions of this paper are summarized as divided into three distinct zones: entry area, control area, and follows:

departure area. The AIM system exerts control over vehicles 1\) Firstly, we introduce CMG, an extension of standard within a specified distance from the entrance of the intersection Markov Games, with embedded safety constraints restricting \(i.e., the control area\). The origin O \(X0, Y0\) of the intersec-the set of acceptable policies. This framework serves as a tion coordinate system is positioned at the southwest corner, formulation for the MADRL problem, necessitating safety and the road width is denoted by D. Vehicles approaching the considerations. We convert the AIM problem into a CMG one intersection have three maneuver options: continue straight, by defining CMG’s essential elements. The reward function make a right turn, or make a left turn. Fig. 2 graphically aims to improve traffic efficiency, comfort, and safety, while illustrates all conceivable conflict relationships which can be the cost function focuses on reducing potential collision risks categorized into three types: crossing conflicts \(indicated by and improving traffic safety. 

dark red dots\), merging conflicts \(represented by red dots\), 2\) Secondly, we present MACPO, a safety-aware MADRL

and diverging conflicts \(marked by yellow dots\). 

approach, to solve the CMG problem. It incorporates safety-Each vehicle i i ≤ Na, i ∈ N \+ periodically transmits its T

constrained to further constrain the trust region formed by dynamic driving data si = xi , yi , vi

to the AIM via V2I

Kullback-Leibler \(KL\) divergence, thus facilitating RL policy wireless communication. Here, \(xi , yi \) ∈ R × R represents updates that maximize performance while keeping constraint the vehicle’s position coordinates, while vi ∈ R denotes costs within their limit bounds. Subsequently, we introduce the the current velocity. Imbued with a safety-aware MADRL

MACPO-based AIM algorithm to ensure the safety, efficiency, algorithm, MACPO, the AIM system modulates the timing and ride comfort of CAVs’ cooperative traffic behavior. 

of vehicles traversing road intersections by controlling each Authorized licensed use limited to: Universitaet Bielefeld. Downloaded on January 22,2025 at 07:06:33 UTC from IEEE Xplore. Restrictions apply. 





Downloaded from https://iranpaper.ir

https://www.tarjomano.com

https://www.tarjomano.com

ZHAO et al.: MULTI-AGENT CONSTRAINED POLICY OPTIMIZATION FOR CONFLICT-FREE MANAGEMENT

5377

Fig. 2. 

Collision style. 

Fig. 3. CMG paradigm, including global state space, joint action space, joint vehicle’s velocity v′ in real-time within the range \[v reward function, and safety cost function set. 

i

mi n , vmax \], 

where vmin and vmax are the minimum and maximum veloc-policy updates to maximize AIM performance while ensuring ities, respectively. Then, the motion control layer of each that constraint costs are kept within pre-defined cost bounds. 

vehicle can generate the accelerator throttle opening and brake pad force required for the vehicle to travel according to the desired velocity v′ given by the AIM system. 

IV. TRANSFORMING AIM INTO A SAFE MADRL

i

The problem is defined as follows: At each time step, given PROBLEM FOR ENVIRONMENT INTERACTION SAMPLING

the static road information of the intersection and the dynamic This section initially formulates the safe MADRL problem states of all vehicles, including positions and velocities, the as the CMGs, and then transforms the AIM problem into MACPO-based AIM system determines the joint action \(i.e., a CMG problem by defining the fundamental elements of desired velocities\) of the vehicles in the control area in CMG, which includes the global state space, joint action space, real-time. This system aims to coordinate a collision-free joint reward function, and safety cost function. Consequently, and efficient traffic flow for all vehicles at the intersection, the proposed safety-aware MADRL method, MACPO, can be simultaneously enhancing occupant comfort. 

effectively deployed to address the AIM problem. 

III. F

A. Constrained Markov Games

RAMEWORK OF THE AUTONOMOUS INTERSECTION

MANAGEMENT BASED ON MACPO

Markov games \(MGs\), widely recognized for formally expressing the process by which multiple agents traverse The proposed MACPO-based AIM approach sets up three the environment, fundamentally fall under the category of a neural networks: the policy neural network, along with the discrete-time decision-making architecture. Within the MG

reward and cost-based value neural networks. The policy framework, multiple agents engage in gameplay for cooper-network is employed to map the local states of all vehicles at ative or competitive objectives within the global environment, the current time step to the joint action probability distribution aiming to achieve the maximum total expected rewards. How-of the vehicles at the next time step, while the reward and ever, when safety constraints are introduced, a standard MG

cost-based value networks are used to evaluate the expected proves inadequate for describing the environment. Therefore, performance of reward and safety cost under the current policy. 

this section introduces the concept of CMGs. This represents Fig. 1 illustrates the MACPO-based AIM framework, which an extension of MGs, integrated with constraints that restrict is comprised of two parts: Environment Interaction Sampling the set of allowable policies, as illustrated in Fig. 3. A CMG

\(EIS\) and Policy Evaluation Optimization \(PEO\). 

for Na agents is defined by a tuple \{S, A, R, C, P, µ\}, where The EIS is tasked with acquiring updated RL policy

• S represents the global state space, consisting of the and value network neural parameters, then employing these concatenation of the local states observed by all agents and parameters to sample experience data from a road intersec-an optional global non-redundant state; 

tion environment. This component employs a CMG, a safe

• A = \(A1, A2, . . . AN \) represents the set of joint action MADRL formulation, to formally express the process where a

space of all agents, where each agent i performs an action multiple vehicles with safety constraints explore within the ai ∈ Ai at the discrete time step t ; 

AIM system’s environment. This process subsequently gent

• R : S × A1 × A2 × . . . × AN × S → R represents the erates discrete time-series trajectory data, inclusive of states, a

joint reward function that describes the instant reward from a actions, rewards, and safety costs. Such data serve as the state st by taking a joint action at to the next state st\+1; foundation for optimizing the policy neural network and the j

• C = \{C \}

represents the set of cost

reward and cost-based value neural networks. 

i

i =1,...,Na , j=1,...,Ni,c

functions defined by the specific environment safety con-The PEO operates in tandem with the EIS, utilizing the data j :

×

×

collected from the EIS to update the policy and value neural straints \(each agent has Ni,c cost functions\), C

St

At

i

i

i

networks. It then synchronizes the updated parameters with St\+1 →

i

R maps the transition tuples to safety cost with N

the EIS for the next iteration of sampling and optimizing in a thresholds d1, d2, . . . , d i,c ; 

i

i

i

cyclical process that continues until the desired intersection

• P : S × A1 × A2 × . . . × AN × S → \[0, 1\] represents a

traffic performance is attained. This component features a the transition probability distribution from a state st ∈ S by MACPO method that solves the CMG problem by incorpo-taking a joint action at ∈ A to the next state st\+1 ∈ S at the rating safety-constrained costs to further constrain the trust discrete time step t ; 

region formed by KL divergence. This approach facilitates

• µ: S → \[1,0\] represents the initial state distribution. 

Authorized licensed use limited to: Universitaet Bielefeld. Downloaded on January 22,2025 at 07:06:33 UTC from IEEE Xplore. Restrictions apply. 





Downloaded from https://iranpaper.ir

https://www.tarjomano.com

https://www.tarjomano.com

5378

IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 25, NO. 6, JUNE 2024

Following the CMG model, the agents interact with the environment in discrete time steps. At each time step t , the agents produce state st ∈ S by interacting with the environment, and each agent i performs an action ai ∼ π\(·|

t

st \) according to the

joint policy π. After all agents have taken their joint action a

Na

t = \(a1, 

, . . . , 

\)

t

a2t

at

, they receive a reward R\(st , at , st\+1\)

j

and their respective cost C \(s

, s

i

t , ait

t \+1\). The environment

then transits to a new state st\+1 ∼ P\(·|st , at \). Upon reaching a terminal state, the agents start a new episode with an arbitrary state s0 ∼ µ. When the trajectory τ = \(s0, a0, s1, . . .\) from an epoch is gathered, the policy undergoes an update, subsequently enabling the agents to continue interaction with the environment utilizing this newly updated policy. The purpose of safety MADRL is to enable the agents to learn the opimal policy π∗ that maximizes the expected return of rewards while keeping constraint costs within their limit bounds, through continuous policy updates. 

Let J j \(π\) denotes the expected discounted return J j \(π\) C

C

i

i

j

of policy π with respect to cost function C is: i

X

j

J j \(π\) = Eτ

γ tC \(s

C

∼π \[

i

t , at , st\+1\)\]

\(1\)

i

t

where γ ∈ \[0, 1\) is the discount factor. With the above conditions, the feasible policy set of the CMG model is: 5

n

j o

C ≜

π ∈ 5 : ∀i, j, J j \(π\) ≤ d

\(2\)

C

i

i

Given that the expected discounted return of policy π

with respect to reward function is J \(π\)

=

E

P

τ∼π t

Fig. 4. 

Distances from the exit point of the intersection for vehicles γ t R\(st, at, st\+1\), the optimal policy π∗ with the largest expec- with different driving directions. \(a\)-\(b\) Left Turn Situation; \(b\)-\(c\) Straight tation value of the reward function under the CMG model is: Situation; \(c\)-\(d\) Right Turn Situation. 

π∗ = arg maxπ∈5 J\(π\)

\(3\)

C

where dent represents the distance from the vehicle’s current B. Transforming AIM Into a Safe MADRL Formulation via location to the entrance point of the intersection, and dturn CMG

represents the distance from the entrance point of the intersec-1\) State and Action Space: Given the dynamic driving tion to the exit point of the intersection. Y0 the y-coordinate of information of multiple vehicles entering the intersection, the the origin, yi is the location of vehicle i in y-axis. When the AIM system determines the desired velocities of vehicles in vehicle has entered the intersection, as shown in Fig. 4 \(b\), 

real time. Intuitively, the state space needs to include the speed the distance d2

from the vehicle to the exit point of the

le f t

information of each vehicle and its position information at intersection can be expressed as:

the intersection, usually marked by the horizontal and vertical 8 \(x



i − X 0\)

5D

coordinates \(x

=

×

i , yi \), i ∈ \[1, . . . , Na \]. In the intersection sce-d2

d

\(5\)

le f t

t ur n = ar csi n

5D

8

nario, each vehicle has a fixed lateral trajectory corresponding to its traffic pattern, and reducing the redundant state space For the Straight Situation: When the vehicle has not yet dimension can help improve the efficiency and stability of entered the intersection, as shown in Fig. 4 \(c\), the distance RL. Thus, this paper sets the state space of the vehicles as d1

str from the vehicle to the exit point of the intersection can S = \[d1, d2, . . . , dN , v

\], where d

be expressed as:

a

1, v2, . . . , vNa

i represents the

distance of the i -th vehicle to the exit point of the intersection, and vi represents the vehicle’s velocity. Beyond that, the action d1 = d

space is set to the desired velocities A = v′ , v′ , . . . , v′ of str

ent \+ dstr = Y0 − yi \+ D

\(6\)

1

2

N

all vehicles. 

where dstr represents the distance from the entrance point of In order to obtain more accurate environmental information, the intersection to the exit point of the intersection. When the this paper calculates the distance from the exit point of the vehicle has entered the intersection, as shown in Fig. 4 \(d\), 

intersection for vehicles with different driving directions. 

the distance d2

str from the vehicle to the exit point of the

For the Left Turn Situation: When the vehicle has not yet intersection can be expressed as:

entered the intersection, as shown in Fig. 4 \(a\), the distance d1

from the vehicle to the exit point of the intersection can le f t

d2 = d

be expressed as:

str

str = Y0 − yi \+ D

\(7\)

π

5D

For the Right Turn Situation: When the vehicle has not yet d1

= d

×

\(4\)

le f t

ent \+ dt ur n = Y0 − yi \+ 2

8

entered the intersection, as shown in Fig. 4 \(e\), the distance Authorized licensed use limited to: Universitaet Bielefeld. Downloaded on January 22,2025 at 07:06:33 UTC from IEEE Xplore. Restrictions apply. 





Downloaded from https://iranpaper.ir

https://www.tarjomano.com

https://www.tarjomano.com

ZHAO et al.: MULTI-AGENT CONSTRAINED POLICY OPTIMIZATION FOR CONFLICT-FREE MANAGEMENT

5379

d1

from the vehicle to the exit point of the intersection can where v

r i g

t,i and at,i represent the velocity and absolute accel-be expressed as:

eration of the i -th vehicle at time step t , respectively, and εv π

D

and εa represent weights. The sparse reward function Rs is d1

= d

×

\(8\)

r i g

ent \+ dt ur n = Y0 − yi \+

defined as:

2

8

X Na

When the vehicle has entered the intersection, as shown in Rs =

ε1 δpass\_single \+ ε2 δpass\_all

\(14\)

i =1

p

p

Fig. 4 \(f\) the distance d2

from the vehicle to the exit point

r i g

of the intersection can be expressed as:

where δpass\_single = 1 indicates that one single vehicle passes successfully, otherwise δpass\_single = 0; δpass\_all = 1 indi-8 \(X



0 \+ D − xi \)

D

d2

= d

×

\(9\)

cates that all vehicles pass successfully, otherwise δpass\_all =

r i g

t ur n = ar csi n

D

8

0, and ε1p and ε2p are weights. The total reward function where X

R

0 is the location of point O in x -axis and xi is the M AC P O is set as:

location of vehicle i in x-axis. 

RM AC P O = Rd \+ Rs − CM AC P O

\(15\)

2\) Reward and Cost Settings: Following the CMG framework, we set up not only reward function that characterizes After transforming AIM into a safe MADRL formula-the degree of overall performance optimization but also cost tion via CMG, in the road intersection environment as function that characterizes the degree of system safety per-shown in Fig. 1, multiple vehicles obtain the mapping from formance to ensure that policy updates could improve overall state S = \[d1, d2, . . . , dN , v

\] to action A =

a

1, v2, . . . , vNa

performance most without violating safety constraints of each v′ , v′ , . . . , v′ so as to continuously explore the environ-1

2

N

individual CAV and their joint traffic behaviour. 

ment. Furthermore, the policy neural network as well as the In order to better evaluate the quality of the policy, reward and cost-based value neural networks can be updated we comprehensively consider dense and sparse evaluation by collecting the entire epoch trajectory in the PEO component items, including dense and sparse reward functions as well until the expected intersection traffic performance is achieved. 

as dense and sparse cost functions. The dense evaluation item is used to evaluate the performance at each timestep, like the V. AUTONOMOUS INTERSECTION MANAGEMENT

velocities, accelerations of CAVs. While the sparse evaluation BASED ON MACPO

item is used to evaluate the performance of the vehicle at each In this section, we first introduce MACPO, a safety-aware episode, and it is only triggered when some special events MADRL policy optimization method designed to solve the occur. For instance, in a case of collision \(terminal state\), all CMG problem. We further propose the MACPO-based AIM

vehicles pass through the intersection successfully \(terminal algorithm, where MACPO, as the core of the PEO component, state\) or a certain vehicle passes through the intersection optimizes the policy neural network based on the CMG-style \(intermediate state\). 

trajectory data of multiple vehicles collected by the EIS

The cost function emphasizes the traffic safety and the component. This ensures that policy updates can maximize potential collision risk. For this reason, this paper designs AIM performance with minimum safety constraints violations. 

the collision safety distance threshold cs. When the distance between two vehicles with the possibility of collision is less A. Multi-Agent Constrained Policy Optimization

than cs, the value of the cost function is increased by εR. 

Policy optimization algorithm solves the CMG problem by Therefore, the dense loss function Cd can be defined as: searching for the optimal feasible policy within a set 5θ of X Nt

X Na

X Na −1

C

parametrized policies with neural network parameters θ, and d =

εRδrisk

\(10\)

t =1

i =1

i ′=1

t,i,i′

the policy is iteratively updated by maximizing the expected where δrisk

= 1 indicates that there is a collision risk

discounted reward return J \(π\) over a local neighborhood 5θ ∩

t,i,i′

between the i -th vehicle and the i’-th vehicle at the t -th time 5C of the most recent iteration πk:

step, otherwise δrisk

= 0. At the same time, the value of

t,i,i′

π

J \(π\)

the cost function is increased by ε

k\+1 = ar gmax π∈5

c after collision, and the

θ

sparse cost function C

j

s can be defined as:

s.t. J j \(π\) ≤ d , i = 1, . . . , N

C

i

a , j = 0, . . . , Ni,c

i

Cs = εcδcollision

\(11\)

DK L \(π||πk\) ≤ δ. 

\(16\)

where δcollision = 1 indicates that collision occurs, otherwise This update is difficult to implement in practice, as the δcollision = 0. The total cost function CM AC PO is defined as safety constraint functions need to be evaluated to determine the summation of the dense cost function Cd and the sparse whether a policy π is feasible. The off-policy evaluation is cost function Cs. 

known to be challenging when constrained policy updates are computed using samples collected over π

C

k . In this work, 

M AC P O = Cd \+ Cs

\(12\)

we have replaced the objective and safety constraints with The reward function focuses on comprehensively measuring easy-to-evaluate surrogate functions developed by CPO \[36\]

the traffic efficiency, safety and comfort of drivers and pas-so as to obtain a good local approximation to Equation \(16\). 

sengers at intersections. The reward function of AIM consists The on-policy value function for reward, expressed as of two parts: dense and sparse rewards. The dense reward V π \(s\) = Eτ∼π \[R \(τπ \) |s0 = s\], represents the expected function Rd is set as:

return starting from state s under policy π. The action-value function, denoted as Qπ \(s, a\) = E



τ∼π R \(τπ \) |s0 = s, 

X Nt

X Na

Rd =

εvvt,i − εaat,i

\(13\)

a

t =1

i =1

0 = a, represents the expected return starting from state s, Authorized licensed use limited to: Universitaet Bielefeld. Downloaded on January 22,2025 at 07:06:33 UTC from IEEE Xplore. Restrictions apply. 





Downloaded from https://iranpaper.ir

https://www.tarjomano.com

https://www.tarjomano.com

5380

IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 25, NO. 6, JUNE 2024

taking the joint action a, and following policy π thereafter. 

the total number of cost function is Nm = P N

i

i,c. When the

The advantage function, denoted as Aπ \(s, a\), measures the number of constraints is small by comparison to the dimension advantage of taking action a relative to the mean. It is of neural network parameters θ, this is much easier to solve defined as the difference between the action-value function and than \(17\). If λ∗, v∗ are a solution to the dual, the solution to the value function: Aπ \(s, a\)Qπ \(s, a\) − V π \(s\). Similarly, the the primal is:

on-policy value functions, action-value functions, and advan-1

v∗

N

tage functions for the auxiliary costs are defined as V π , Qπ , θ

H−1g −

H−1 hb1, b2, . . . , b 1,c , b1, b2, 

j

j

k\+1 = θk \+

C

C

λ∗

λ∗

1

1

1

2

2

i

i

Aπ , respectively. Let dπ denote the discounted future state N

N

i

j

2,c

Na ,c

C

. . . , b

, . . . , b1 , b2 , . . . , b

i

2

Na

Na

Na

distribution, defined by dπ \(s\) = \(1 − γ \) P γ t P\(s t

t = s|π \). 



j

\! 

Equation \(16\) is thus approximated as: λ∗c − r

v∗ =

i

π

S



k\+1 = ar gmax π

\+

∈5 E

Aπk \(s, a\)

θ

s∼dπk

a∼π





\! 

1





π

1

r 2

λ cJ2

j



i

s.t. J

k



−

\+

−δ

j \(π

A

\(s, a\) ≤ d

∀i, j

 fa \(λ\) ≜

q

c

k \) \+

j

i



i

1 − γ Es∼dπk

a∼π

c



2λ

S

2

S

i



¯



D \(π∥π



j

k \) ≤ δ

\(17\)





λ∗

r c

= ar gmax

i

j

λ≥0

−

, 

i f λc − r > 0

The above formula can increase the expected reward return S

i



j



1 q

and satisfy the specified constraints C . However, for neural





i

 f

\+ λδ , 



b\(λ\) ≜ −

network based policies with high-dimensional parameter



2

λ







else

spaces, Equation \(17\) may be impractical to solve directly due to the computational cost. Given that for a small step \(20\)

size δ, the objectives and safety constraints of policy π can After acquisition of v∗ and λ∗, the conjugate gradient be well approximated by a linear function around the current method can be used to calculate the policy update direction policy πk, and the KL divergence constraint can be well x

approximated by a second-order expansion, Equation \(17\) is k :



approximated as:

xk = H−1 g − ˆbv∗

\(21\)

θk\+1 = arg maxθ gT \(θ − θk\)

The current policy can be updated by the following formula: j

j T

s.t. c \+ b

\(θ − θ

i

i

k \) ≤ 0, 

∀i, j

1 \(θ

α

− θk\)T H \(θ − θk\) ≤ δ

\(18\)

θ

x

2

k\+1 = θk \+ λ∗ k

\(22\)

where g ≜ ∇θ E \[Aπk \(s, a\)\] represents the gradient of the where α is obtained by backtracking linear search. 

j

π

objective, b

k \(s, a\)\] represents the gradient

When the convex optimization problem is infeasible, it indi-i

≜ ∇θ E\[A j

Ci

cates that it is impossible to find suitable neural network j

of safety constraint C , H represents Hessian of the KL-i

parameters to make the value of the safety cost function less j

j

divergence, and c

\(π

represents the difference

than the preset limit while improving the reward value. There-i ≜ J j

c

k \) − di

i

between the expectation of the j -th safety constraint function fore, we turn to find the semi-optimal policy that minimize the j

C of the i -th agent under the policy π

safety cost. In order to obtain the global minimum safety cost i

k and its corresponding

j

function, we ignore the effects of the reward function during limit d . 

i

the policy updating:

Due to the fact that the Hessian matrix H in the formula is always positive semi-definite, the policy optimization problem h

is a convex. When the convex optimization problem is feasible, θ

j

j T

k\+1 = ar g mi nθ c \+ b

\(θ − θ

i

i

k \)i

Equation \(18\) can be solved efficiently using duality: 1

s.t. 1 \(θ − θ



λδ

k \)T H \(θ − θk \) ≤ δ

\(23\)

maxλ

2

≥0,v≥0 −

gT H−1g − 2r T v \+ vT Sv \+ vT c −

2λ

2

Let the policy change x = θ − θk, the dual function of for-

\(19\)

j

j

mula \(23\) is given by L \(x, λ\) = c \+b T x \+λ 1 x T H x − δ. 

i

i

2

where

The optimal solution for policy update is obtained when the partial derivative of the dual function with respect to policy r ≜ gT H−1 hb1, b2, . . . , 

1

1

change is 0:

N

N

N

i

b 1,c , b1, b2, . . . , b 2,c , . . . , b1 , b2 , . . . , b Na,c , 1

2

2

2

N

L

a

Na

Na

j

= b T \+ λ \(H x\) = 0

\(24\)

h

i

N

N

∂x

S ≜ b1, b2, . . . , b 1,c , b1, b2, . . . , b 2,c , . . . , b1 , 1

1

1

2

2

2

Na

j

The obtained x = − 1

T above should satisfy the

N

iT

λ H−1bi

b2 , . . . , b Na,c

N

trust-region constraint determined by KL-divergence: a

Na

N

N

× H−1 hb1, b2, . . . , b 1,c , b1, b2, . . . , b 2,c , . . . , b1 , 1

1

1

2

2

2

Na

1 

1

T





j

1

T

j T

N

i

−

H

−

≤ δ

\(25\)

b2 , . . . , b Na,c , 

λ H−1bi

λ H−1bi

N

2

a

Na

Authorized licensed use limited to: Universitaet Bielefeld. Downloaded on January 22,2025 at 07:06:33 UTC from IEEE Xplore. Restrictions apply. 





Downloaded from https://iranpaper.ir

https://www.tarjomano.com

https://www.tarjomano.com

ZHAO et al.: MULTI-AGENT CONSTRAINED POLICY OPTIMIZATION FOR CONFLICT-FREE MANAGEMENT

5381

r

j

j

b T H −1b

the vehicle control parameters belong to the continuous action Therefore, we have

i

i

2δ

≤ λ, and the update rule in

space, we adopt a diagonal Gaussian policy whose output is case of in-feasibility is:

the mean µθ \(s\) of the vehicles’ actions. In the early stage s

of training, the exploratory requirements of the policy are θ

2δ

j T

k\+1 = θk −

H−1b

\(26\)

stronger, and the stability requirement of the policy is stronger j

j

i

b T H −1b

i

i

as the number of training iterations increases. Therefore, Equations \(22\) and \(26\) are used to implement MACPO. 

we define the dynamic attenuation standard deviation σθ to obtain better training effect and faster convergence speed: Algorithm 1 MACPO-based AIM

σθ = ζ × eϑ×z, z = 1, 2, . . . , NT

\(27\)

## 1:

Initialize φR, φC , π, set costd , γ , klmax , ρ, lrr , lrc, where ζ and ϑ represent the coefficient and decrease index Nb, Ne, Nt , Nm, ζ , ϑ. 

of the standard deviation σθ , repectively, z is the time 2:

for epoch k = 1, 2, . . . , Ne do

step index, and NT is the total number of time steps. 

## 3:

for t = 1, 2, . . . , Nt do

Consequently, the joint action of the multi-agent is a =

## 4:

For each vehicle i = 1, 2, . . . , Na, receive state

\[µθ \(s1\) \+ σθ , µθ \(s2\) \+ σθ , . . . , µθ \(sN \) \+ σθ \]. Our algorithm st = \[di , vi \], choose an action at = \[v′\] according i

evaluates the performance of the current policy according to to current policy πk. 

the reward and cost-based value network. Apart from that, a 5:

Execute global actions at, get reward rt , cost linear decay learning rate is used to update the reward and ct, next state st\+1, w.r.t. current policy and

cost-based value networks:

exploration in EIS. 

i , 

## 6:

### s

lrr = lrr0 ×

i = \[1, NE \]

t = st \+1

E

## 7:

### end for

i , 

## 8:

### Collect trajectories τ

lr

i = \[1, N

π = \(s

c = lr c0 ×

E \]

\(28\)

k

t ,at,rt , ct, st\+1\)

E

## 9:

Calculate advantage function of reward and cost where NE represents the number of epochs. In the process function: Âπ \(st , at\) , Âπ \(s

j

t , at\)

of continuously updating the reward and cost-based value Ci

network through the gradient descent, the policy is updated 10:

Calculate ˆ

g, ˆ

b, ˆ

c, B:

j

toward increasing the reward and decreasing the cost, and ˆ

g = ∇

P

θ J \(π \), ˆb = ∇θ J j \(π \), ˆc = P

ˆ

c , 

C

i

j

i

i

finally achieving the desired performance. 

B = δ −

ˆ

c2

MACPO-based AIM algorithm is presented in algorithm 1. 

ˆ

bT H−1 ˆ

b

## 11:

if case 1 or case 2 then

The first line of the algorithm is used to initialize network 12:

update policy network as:

parameters and algorithm parameters, including the random θ

q

2δ

reward-based value network φR, cost-based value network φC , k\+1 = θk −

H−1 ˆ

g

ˆ

gT H−1 ˆ

g

and policy network π with θ, set cost

## 13:

elseif case 3 or case 4 then

d , γ , maximum KL

divergence klmax , GAE coefficient ρ, value function learning 14:

solve convex dual problem, get v∗, λ∗

rate lrr , cost value function learning rate lr c, batch size Nb, 15:

solve α by backtracking line search, update

epoch Ne, total steps per batch Nt , total cost functions Nm, policy network as:

policy std ζ , policy std decrease index ϑ. 

θ





k\+1 = θk \+ α

λ

ˆ

∗ H −1

g − ˆ

bv∗

The main loop of the algorithm begins at the second line, 16:

else update policy network as:

which initially gathers trajectory data composed of state-action θ

q

2δ

pairs for the multiple vehicles, as well as the reward and k\+1 = θk −

H−1 ˆ

b

ˆ

bT H−1 ˆ

b

cost values in the EIS component \(lines 2-8\). Subsequently, 17:

end if

within the PEO component \(lines 9-19\), the policy network 18:

Update φR, φC as: 

and the reward and cost-based value networks are evaluated φ



2 

R = ar gmi nφ E

Vφ \(s

R

t \) − ˆ

Rt

and updated separately. 



For the policy network, in order to further improve the φ



2 

C = ar gmi nφ E

Vφ \(s

computational efficiency, our algorithm comprehensively conC

t \) − ˆ

Ct

siders the constraint satisfaction of current policy as well as 19:

end for

the feasibility of the next policy, estimates the possibility of a policy update that causes the CAVs to be in a dangerous situation, and proposes the corresponding update solution B. MACPO-Based AIM Algorithm

\(lines 9-17\). More specifically, we define all feasible policies Based on the multi-agent constrained policy update method, around the current policy πk that satisfy the preset KL diver-we provide the following algorithm that guarantees both gence and the safety constraints as the local policies to be AIM monotonic performance improvement and safety cost searched \(see the light blue ellipse area in Fig. 5\). During constraints satisfaction. As shown in Fig. 1, the algorithm sets the local policy search process, our algorithm decides how to up three neural networks: the policy neural network and the update the policy by calculating the gradient of the safety reward and cost-based value neural networks. The input of the constraint cost function, so that the policy can obtain the algorithm refers to the local states of all vehicles at the current maximum reward function value as much as possible while sat-time step. After mapping by the policy network, the output is isfying both the safety constraint and the KL divergence conj

j

the joint actions of the vehicles at the next time step. Given that straint. Let ˆ

b = ∇

\(π

γ tC \(st, at, st\+1\)\], 

i

θ J j

C

k \) = ∇θ E \[Pt

i

i

i

i

i

Authorized licensed use limited to: Universitaet Bielefeld. Downloaded on January 22,2025 at 07:06:33 UTC from IEEE Xplore. Restrictions apply. 





Downloaded from https://iranpaper.ir

https://www.tarjomano.com

https://www.tarjomano.com

5382

IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 25, NO. 6, JUNE 2024

an area with high dangerous potential energy, but the updated policy may return to a region with low dangerous potential energy, which is labeled as Case 4. 

Case 5: If F < 0 and ˆc > 0, and there is no feasible policy region that satisfies both KL divergence constraints and safety constraint, it indicates that the overall dangerous potential energy of the current policy is at a high level, the updated policy cannot return to the region with low dangerous potential energy, which is labeled as Case 5. 

Our algorithm performs corresponding policy updates for the above different cases. When case 1 or 2 is detected, given that none of the local policies in the trust region constrained by the KL-divergence will cause the agent to fall into a dangerous situation, the policy update can directly adopt the traditional Trust region policy optimization \(TRPO\) \[37\] method:

s

θ

2δ

k\+1 = θk −

H−1 ˆ

g

\(29\)

ˆ

gT H−1 ˆ

g

Fig. 5. 

Judgement of constraint satisfaction of current policy as well as the feasibility of the next step policy when updating the MACPO-based AIM

When case 3 or 4 is detected, the policy update needs to algorithm. 

satisfy both KL-divergence and safety constraints and there is a feasible policy region that satisfies both constraints. Therefore, Equation \(22\) derived above is used to update the current i ∈ \[1, . . . , Na\], j ∈ \[0, . . . , Ni,c\] denotes the policy gra-policy. When case 5 is detected, there is no feasible policy j

j

dient estimation of the safety constraint function C , ˆ

c

=

i

i

region that satisfies both KL divergence constraints and safety j

j

d

E \[P γ t C \(st , at , st\+1\)\] −

i

constraints. Hence, Equation \(26\) derived above is used to t

i

i

i

i

1−γ denote the proximity of the

j

j

update the current policy. 

agents’ safety cost on constraint C

to its limit d

following

i

i

For the reward and cost-based value networks, their gra-current policy \(also known as the dangerous potential energy\), j

dients are used to update the respective network parameters we define the overall estimations as ˆ

b = P P ˆ

b

and ˆ

c =

i

j

i

\(line 18\):

P

P

j

ˆ

c , and use F = δ −

ˆ

c2

to measure whether the

i

j

i

ˆ

bT H−1 ˆ

b

next step policy of the current policy πk is feasible \(line 10\). 



2 

Based on the parameters ˆ

b, ˆ

c and F , as shown in Fig. 5, the φR = argminφ E Vφ \(s

R

t \) − ˆ

Rt

situation of a policy update that whether causes the CAVs to 2 

be in a dangerous situation is divided into the following cases: φC = argminφ E Vφ \(s

\(30\)

C

t \) − ˆ

Ct

Case 1: If the value of the safety gradient ˆ

b is extremely

small \( ˆ

b < 1e − 8\), it indicates that the overall dangerous After updating the three neural networks, the algorithm potential energy of the current policy is at an extremely employs the new policy network to collect trajectories in the low level. At this time, even without imposing safety cost environment again, and then evaluates and updates the neural constraints, updating policies within KL divergence-based trust networks until Ne epochs are completed. 

region will not lead to a dangerous situation, which is labeled as Case 1. 

VI. PERFORMANCE EVALUATION

Case 2: If F < 0 and ˆc < 0, the trust region constrained by the KL divergence is completely in the safety region, A. Experiment Settings

it indicates that the overall dangerous potential energy of In order to evaluate the proposed AIM system based on the current policy is at a low to medium level \(i.e. the MACPO in experimental tests, two sets of experiments are overall safety cost is lower than the given threshold to varying performed in this section. To be specific, the first experiment degrees\), but updating policies within KL divergence based illustrates the training process of MACPO, MAPPO proposed trust region will not lead to a dangerous situation, which is by Guan et al. \[34\] and MAPPO-SC with the same safety labeled as Case 2. 

constraints as MACPO but in the form of reward function Case 3: If F > 0 and ˆc < 0, and the trust region constrained penalties, which shows that our algorithm has better overall by the KL divergence is divided into safe and non-safe parts performance, especially in terms of safety, and reaches zero by the safety constraints, it indicates that the policy update collision for the first time. The second experiment compares without safety constraints \(the direction of the dotted line in the performance of MACPO-trained policy with MAPPO, the figure\) will make the dangerous potential energy be at the MAPPO-SC, MPC-based method VICS \[6\] and MIP-based high level, causing cost value exceeding the limit value and MICA \[27\] in terms of computation time, ride comfort, traffic entering a dangerous situation, which is labeled as Case 3. 

efficiency, and safety. 

Case 4: If F > 0 and ˆc > 0, and the there is an intersection All the experiments are performed in a simulation envi-between trust domains satisfying KL divergence and safety ronment, in which Carla 0.9.12 is used to build the road constraints, it indicates that the current policy is already in intersection scenarios and the MADRL model is built based Authorized licensed use limited to: Universitaet Bielefeld. Downloaded on January 22,2025 at 07:06:33 UTC from IEEE Xplore. Restrictions apply. 





Downloaded from https://iranpaper.ir

https://www.tarjomano.com

https://www.tarjomano.com

ZHAO et al.: MULTI-AGENT CONSTRAINED POLICY OPTIMIZATION FOR CONFLICT-FREE MANAGEMENT

5383

TABLE I

MAIN PARAMETERS OF THE EXPERIMENTS

Fig. 6. 

Simulation Scenario. 

on the PyTorch framework. Apart from that, CARLA’s built-in sensors are used to transmit vehicle status information in real time, and the class BasicAgent is adopted to generate vehicle traffic trajectories at intersections. The expected vehicle speed output by the policy neural network is converted into the throttle control signal and brake control signal for controlling the vehicle through the built-in PID controller of CARLA. 

In addition, the GPU is NVIDIA GeForce RTX 3090, and the operating system is Ubuntu 18.04. 

In this experiment, the four-way dual-lane signal-free intersection in CARLA TOWN 05 is chosen as the training and testing scenario for the RL model, as shown in Fig. 6. The road width and lane width are 14.2 meters and 3.5 meters, and the lengths of the East-West and North-South lanes \(i.e., the departure areas\) are 65 meters and 50 meters, respectively. Considering the characteristics of the roads in the CARLA map and the range of V2I communication, the lengths of the East-West and North-South control areas are set to 70 meters and 60 meters, respectively. To simulate real traffic flow, this experiment selects a variety of vehicle types in the simulation environment. The length range of the vehicles is 3.6-5.4 meters, the width range is 1.8-2.2 meters, the height range is 1.5-2 meters, and the arrival of vehicles is assumed to follow a Poisson distribution. Based on the set average traffic flow λ per hour for a single lane, a random number λ’ is generated using the Poisson function in the numpy package. This number is used to calculate the time interval Adam optimizer is used for policy update. The learning rate at which vehicles enter the intersection on this lane. Further, decays linearly from 1e-3 to 0, the standard deviation decays considering the free-driving speed of vehicles before they enter exponentially from 1 to 0, and the training algorithm stops the control area, the distance between two adjacent vehicles after 1024 epochs. Furthermore, the parameter settings of the is obtained. Subsequently, vehicle position coordinates are MPC-based VICS algorithm and MIP-based MICA algorithms generated continuously, enabling the creation of a continuous are the same as those in their original papers. The main traffic flow in CARLA that adheres to a Poisson distribution. 

parameters of the experiments are presented in Table I. 

Consistent with the actual vehicle control cycle, the time step is set to 0.1 s. We all employ multiple-layer perceptron with two hidden layers as the approximate functions of the B. Performance Comparison of MACPO, MAPPO, 

policy and the value functions for MACPO, MAPPO and MAPPO-SC Algorithms During Training Process

MAPPO-SC algorithms, all of which have 128 units in each In this experiment, we have not only trained three policies hidden layer. For the MACPO algorithm, we additionally through MACPO, MAPPO and MAPPO-SC algorithms, but employ a four-layer neural network with two hidden layers also compared their performance in terms of traffic effi-with 128 neurons as the cost function. The structure of the ciency, safety, and ride comfort. Among them, MACPO is policy network is 2Na × 128 × 128 × Na, where Na the algorithm proposed in this paper, and MAPPO is the RL

represents the number of vehicles that the AIM system needs algorithm for the cooperative control of vehicles at intersec-to coordinate simultaneously, with this study supporting up tions presented in \[34\]. Although MAPPO-SC has the same to 60 vehicles. Beyond that, the structures of the reward and safety-related constraints as MACPO, it uses MAPPO’s policy cost value networks are both 2Na × 128 × 128 × 1. For update method and parameters. Namely, the constraints guide each policy iteration, 2048 timesteps are collected, and the the policy update in the form of reward function penalty items Authorized licensed use limited to: Universitaet Bielefeld. Downloaded on January 22,2025 at 07:06:33 UTC from IEEE Xplore. Restrictions apply. 





Downloaded from https://iranpaper.ir

https://www.tarjomano.com

https://www.tarjomano.com

5384

IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 25, NO. 6, JUNE 2024

Fig. 7. 

Performance Comparison of MACPO policy with MAPPO, MAPPO-SC during training process. \(a\) Mean episode reward. \(b\) Mean episode cost. 

\(c\) Mean episode collision rate. \(d\) Mean episode length. \(e\) Mean episode acceleration. 

together with other reward items, rather than as the separate \(potential collision risk\) and sparse \(direct collision\) costs constraints that must be satisfied. Fig. 7 dipits the performance associated with safe passage at intersections. The lack of comparison of three algorithms during training, in which the cost neural network makes the MAPPO-SC and the MAPPO

solid line represents the average value of the training curves, algorithm unable to obtain the ideal safety cost value. Due and the shaded part represents the variance. 

to the fact that the safety penalty is considered in the reward The episode rewards of the three algorithms are shown in function, the cost function value of the MAPPO-SC algorithm Fig. 7 \(a\). In terms of reward value, due to the different after convergence is smaller than that of the MAPPO algorithm reward function settings, the reward function value of the without safety considerations. Using the cost constraint neural MAPPO algorithm is generally low, and after convergence, network and constraint satisfaction policy update, the MACPO

the reward value of the MACPO algorithm with the same algorithm can always constrain the cost function value near reward function setting is higher than that of MAPPO-SC. 

the preset threshold in this paper. In this way, the potential The reason for this gap lies in that the MACPO algorithm can collision risk in the traffic scene is significantly less than that keep the safety overhead value at 0, whereas the MAPPO-SC

of the MAPPO-SC and MAPPO algorithms. 

algorithm is difficult to control the safety penalty item in the The episode collision rate, as the most direct indicator for reward function to 0 due to the lack of a separate safety evaluating the safety of the algorithms, is shown in Fig. 7\(c\). 

cost neural network and policy update method satisfying Corresponding to the cost function value that characterizes the safety constraints. Regarding the stability of the policy after collision risk, the algorithm with a lower cost function value convergence, the MACPO algorithm can keep the value of curve tends to have a lower episode average collision rate. 

the reward function stable at a high level after convergence, The MACPO algorithm uses the cost function to constrain the thanks to the strict restriction of the safety cost function collision risk in the traffic scene, which achieves zero collision on the potential collision risk. However, the reward value rate after convergence, and keeps it from the 500th update to obtained by the MAPPO-SC algorithm based on the same the end of the policy update. The collision rate of MAPPO-SC

safety considerations but without constrained policy updates is smaller than that of MAPPO algorithm. Obviously, even fluctuates greatly when the policy is updated about 300 times. 

with safety constraints, the MAPPO-SC algorithm cannot At the same time, the reward value of the MAPPO algorithm achieve zero collision rate during the entire training process, that does not consider safety constraints also fluctuates greatly which further proves the safety limitations of the traditional \(the shaded area representing the variance of its reward value single reward function-driven type RL algorithm. 

is the largest\). Both of them are difficult to meet people’s Fig. 7 \(d\) shows the episode length, which reflects the needs for stability and safety of driverless and intelligent traffic efficiency of each algorithm in road intersection, and the transportation systems. 

lower the value, the higher the traffic efficiency. The MAPPO

Fig. 7 \(b\) shows the episode safety cost that represents the algorithm without safety constraints obtains the highest traf-potential collision risk of the traffic environment, in which fic efficiency, and the traffic efficiency of MAPPO-SC and the red dotted line represents the safety cost function thresh-MACPO algorithms with safety constraints is relatively low. 

old preset in this paper. The cost function includes dense The reason is that the policy trained by the MACPO algorithm Authorized licensed use limited to: Universitaet Bielefeld. Downloaded on January 22,2025 at 07:06:33 UTC from IEEE Xplore. Restrictions apply. 





Downloaded from https://iranpaper.ir

https://www.tarjomano.com

https://www.tarjomano.com

ZHAO et al.: MULTI-AGENT CONSTRAINED POLICY OPTIMIZATION FOR CONFLICT-FREE MANAGEMENT

5385

TABLE II

PERFORMANCE COMPARISON OF MACPO POLICY WITH MAPPO, MAPPO-SC POLICIES,VICS AND MICA AFTER DEPLOYMENT

controls each vehicle to strictly maintain the safe distance from and high traffic flow λ3 = 1800veh/ h/lane. The results are the surrounding vehicles, so as to limit the risky and aggressive presented in Table II. 

traffic of the vehicles and reduce the potential collision risk In terms of travel efficiency, the neural network-based in the traffic scene. It can also be observed that the traffic MACPO, MAPPO, and MAPPO-SC algorithms performed efficiency of the MACPO algorithm is not far behind that of within the same order of magnitude in mean episode length. 

the MAPPO-SC and MAPPO algorithms, but it achieves high In contrast, the optimization-based VICS and MICA methods safety by sacrificing a small amount of traffic time \(around lagged significantly behind in this same metric. As traffic 3 seconds\). 

complexity increased, these optimization-based methods take Fig. 7 \(e\) shows the episode acceleration, which reflects the longer to solve problems, consuming more time and resources riding comfort of the occupants. A lower average acceleration without necessarily obtaining a globally optimal solution. 

value indicates that the occupants in the car have higher riding Regarding the MPC-based VICS algorithm specifically, main-comfort. Obviously, the acceleration value of the MACPO

taining continuous control proved challenging due to the heavy algorithm is still at a relatively low level after about 600 policy computational demands. Therefore, we reduced the prediction updates. At the same time, as the number of training increases, length to 5 to ensure that vehicles have available input to the acceleration fluctuation value remains small. The average maintain continuous control before the next set of solutions acceleration values of MAPPO and MAPPO-SC algorithms are is generated. 

at a high value, and the average acceleration values fluctuate In terms of safety, indicated by safety distance violation greatly. According to the results, the MACPO algorithm, and collision rate, the optimization-based VICS and MICA which separates the reward function from the cost function, algorithms achieved high safety, however, this heightened can achieve high ride comfort and ensure driving safety. 

safety comes at the expense of significantly reduced traffic efficiency. Among the three neural network-based algorithms, only MACPO achieves a zero collision rate and no safety C. Performance Comparison of MACPO Policy With

distance violations, indicating a significantly reduced or even MAPPO, MAPPO-SC Policies, MPC-Based VICS and

minimized collision risk. In contrast, MAPPO-SC, which MIP-Based MICA After Deployment

incorporates safety constraints into the reward function, has In this experiment, we implement the policies trained by a higher collision rate and safety distance violation than MACPO, MAPPO, MAPPO-SC, MPC-based VICS and MIP-MACPO but is safer than MAPPO, which does not consider based MICA. To evaluate the performance of these different safety at all. 

algorithms under varying traffic complexities, we conduct In terms of ride comfort, indicated by mean episode acceler-experiments focusing on various metrics: Mean Episode ation and mean jerk, the optimization-based methods such as Length, Safety Distance Violation, Collision Rate, Mean VICS and MICA recorded relatively high performance, and Episode Acceleration, Mean Jerk, and Mean Inference Time. 

the performance of MICA is higher than VICS algorithm. 

These evaluations are done in low, medium, and high-density The superior performance of the MICA algorithm is due to traffic

scenarios, 

specifically, 

low

traffic

flow

λ

its simultaneous control over the leading vehicle in a lane, 1

=

600veh/ h/lane, medium traffic flow λ

with subsequent vehicles following in a platoon mode, which 2 = 1200veh/ h/ lane, 

Authorized licensed use limited to: Universitaet Bielefeld. Downloaded on January 22,2025 at 07:06:33 UTC from IEEE Xplore. Restrictions apply. 





Downloaded from https://iranpaper.ir

https://www.tarjomano.com

https://www.tarjomano.com

5386

IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 25, NO. 6, JUNE 2024

Fig. 8. 

Traffic Trajectories vs Timestep. \(a\) MACPO, \(b\) MAPPO, \(c\) MAPPO-SC \(d\) MPC-based VICS, \(e\) MIP-based MICA. 

reduces the acceleration. Conversely, the VICS algorithm comfort performance, but extremely low computational effi-independently controls each vehicle in the traffic scenario. 

ciency, making them difficult to be widely applied in complex In cases where a global optimal solution cannot be guaranteed and dynamic traffic scenarios. The MAPPO algorithm that for all vehicles, substantial fluctuations in acceleration may does not consider safety constraints has the highest traffic occur. Among the three neural network-based algorithms, the efficiency, but its safety performance is poor, so that it is not MACPO algorithm, due to its additional safety constraint suitable for safety-critical autonomous driving and intelligent network, possesses the smallest action space, resulting in transportation fields. The MAPPO-SC algorithm adds safety less variation in vehicle speeds in the traffic environment. 

constraints to the reward function in the form of penalty items, This ensures ride comfort while maintaining safety and effi-which slightly improves its safety performance. Nonetheless, ciency. The MAPPO-SC algorithm, lacking the additional there is still a large collision risk, and the traffic efficiency neural network constraint, has a larger action space and hence is slightly lower than that of MAPPO. Given that MACPO

shows relatively greater acceleration than MACPO. On the algorithm uses the separate cost neural network and constraint other hand, the MAPPO algorithm, which does not have any satisfaction policy update approach, it can not only take safety constraints, exhibits the most randomness in behavior, account of traffic efficiency and ride comfort but also eliminate resulting in the highest acceleration values and thereby leading potential collision risks as much as possible. In contrast, to a comparatively less comfortable riding experience. 

it is more suitable for autonomous driving and intelligent In the aspect of computation time, symbolized by mean transportation system. 

inference time, the RL methods greatly outperform the Moreover, the proposed algorithm possesses certain gener-optimization-based methods, reducing computation time by alization capabilities and can be extended to other intersection several orders of magnitude. This is mainly attributed to scenarios, such as three-way intersections \(T or Y type\) and the ability of RL methods to map traffic environment states roundabouts, as well as other irregular environments. Prior to to actions directly through neural connections, bypassing applying the algorithm to a new environment, it is necessary the need for extensive calculations. On the other hand, to fine-tune the hyper-parameters of the model, re-adjust the optimization-based methods require solving multiple con-coefficients of the reward and cost functions, vehicle turning strained optimization problems given the input states, which formulas, and control area size, among other environment-demand a substantial amount of computational resources. 

specific parameters. For scenarios with significantly increased Finally, Fig. 8 presents the temporal scatter plots of vehi-complexity, more state variables \(such as heading angle, cle passage within the range controlled by these methods. 

travel direction, etc.\) may be introduced to describe more By recording the real-time position of vehicles in the simu-complete traffic conditions, and more action options \(such as lation environment at each simulation step, we can observe passage permissions, routes, etc.\) to achieve more optimized the pattern Overall, according to the results, MPC-based traffic flow control. Simultaneously, increasing the number of VICS algorithm and MIP-based MICA algorithm have high neural network layers and the number of neurons in each safety performance and MIP-based MICA algorithm has high layer can enhance model flexibility to accommodate more Authorized licensed use limited to: Universitaet Bielefeld. Downloaded on January 22,2025 at 07:06:33 UTC from IEEE Xplore. Restrictions apply. 





Downloaded from https://iranpaper.ir

https://www.tarjomano.com

https://www.tarjomano.com

ZHAO et al.: MULTI-AGENT CONSTRAINED POLICY OPTIMIZATION FOR CONFLICT-FREE MANAGEMENT

5387

complex problems. While these expansions may lead to longer

\[3\] K. C. Dey et al., “A review of communication, driver characteristics, and model learning times, they will not significantly increase the controls aspects of cooperative adaptive cruise control \(CACC\),” IEEE

Trans. Intell. Transp. Syst., vol. 17, no. 2, pp. 491–509, Feb. 2016, doi: actual computation time after model deployment. Thus, with

10.1109/TITS.2015.2483063. 

thoughtful design and reasonable optimization, the proposed

\[4\] F. Navas, V. Milanés, C. Flores, and F. Nashashibi, “Multi-method holds the promise of delivering superior performance model adaptive control for CACC applications,” IEEE Trans. Intell. 

even in more complex situations. 

Transp. Syst., vol. 22, no. 2, pp. 1206–1216, Feb. 2021, doi:

10.1109/TITS.2020.2964320. 

\[5\] Y. Zhu, D. Zhao, and Z. Zhong, “Adaptive optimal control of het-erogeneous CACC system with uncertain dynamics,” IEEE Trans. 

VII. CONCLUSION

Control Syst. Technol., vol. 27, no. 4, pp. 1772–1779, Jul. 2019, doi: In this paper, a conflict-free management scheme of CAVs

10.1109/TCST.2018.2811376. 

\[6\] M. A. S. Kamal, J.-I. Imura, T. Hayakawa, A. Ohata, and K. Aihara, at unsignalized intersection has been proposed by using safe

“A vehicle-intersection coordination scheme for smooth flows of traffic multi-agent deep reinforcement learning \(MADRL\) so as without using traffic lights,” IEEE Trans. Intell. Transp. Syst., vol. 16, to address the challenges of current centralized coordina-no. 3, pp. 1136–1147, Jun. 2015, doi: 10.1109/TITS.2014.2354380. 

tion methods in balancing high computational efficiency and

\[7\] K. Dresner and P. Stone, “Multiagent traffic management: An improved intersection control mechanism,” in Proc. 4th Int. Joint Conf. Auton. 

robust safety assurance. Firstly, we have approached the safe Agents Multiagent Syst., vol. 3, Jul. 2005, pp. 530–537. 

MADRL problem by formulating it as a constrained Markov

\[8\] C. Yu, W. Sun, H. X. Liu, and X. Yang, “Managing connected game \(CMG\), and have further transformed the AIM problem and automated vehicles at isolated intersections: From reservation-into a CMG. Following this, we introduced the Multi-Agent to optimization-based methods,” Transp. Res. B, Methodol., vol. 122, pp. 416–435, Apr. 2019, doi: 10.1016/j.trb.2019.03.002. 

Constrained Policy Optimization \(MACPO\), a methodology

\[9\] P. Dai, K. Liu, Q. Zhuge, E. H.-M. Sha, V. C. S. Lee, and S. H. Son, specifically developed to address the CMG problem. MACPO

“Quality-of-experience-oriented autonomous intersection control in is notable for its integration of safety constraints, which serve vehicular networks,” IEEE Trans. Intell. Transp. Syst., vol. 17, no. 7, to further limit the trust region defined by the Kullback-Leibler pp. 1956–1967, Jul. 2016, doi: 10.1109/TITS.2016.2514271. 

\(KL\) divergence, thereby facilitating reinforcement learning

\[10\] H. Xu, Y. Zhang, C. G. Cassandras, L. Li, and S. Feng, “A bi-level cooperative driving strategy allowing lane changes,” Transp. 

policy updates that strive for maximum performance while still Res. C, Emerg. Technol., vol. 120, Nov. 2020, Art. no. 102773, doi: maintaining constraint costs within pre-defined bounds. Sub-

10.1016/j.trc.2020.102773. 

sequently, we introduced the MACPO-based AIM Algorithm

\[11\] Y. Wu, H. Chen, and F. Zhu, “DCL-AIM: Decentralized coordina-to ensure the safety, efficiency, and occupant comfort of tion learning of autonomous intersection management for connected and automated vehicles,” Transp. Res. C, Emerg. Technol., vol. 103, CAVs’ cooperative traffic behavior. Finally, we implemented pp. 246–260, Jun. 2019, doi: 10.1016/j.trc.2019.04.012. 

the policies trained by MACPO, MAPPO and MAPPO-SC as

\[12\] K. Zhang, D. Zhang, A. de La Fortelle, X. Wu, and J. Grégoire, well as the coordination schemes based on MPC and MIP

“State-driven priority scheduling mechanisms for driverless vehicles methods, and compare their performance. According to the approaching intersections,” IEEE Trans. Intell. Transp. Syst., vol. 16, no. 5, pp. 2487–2500, Oct. 2015, doi: 10.1109/TITS.2015.2411619. 

results, compared with the MPC and MIP methods, our method

\[13\] Z. He, L. Zheng, L. Lu, and W. Guan, “Erasing lane changes from roads: has increased computational efficiency by 65.22 times and A design of future road intersections,” IEEE Trans. Intell. Vehicles, 731.52 times respectively, and has improved traffic efficiency vol. 3, no. 2, pp. 173–184, Jun. 2018, doi: 10.1109/TIV.2018.2804164. 

by 2.41 times and 1.80 times respectively. In comparison to

\[14\] A. Katriniok, B. Rosarius, and P. Mähönen, “Fully distributed model the non-safety awareness RL methods, our method achieves predictive control of connected automated vehicles in intersections: Theory and vehicle experiments,” IEEE Trans. Intell. Transp. Syst., vol. 23, not only zero collision rate for the first time but also better no. 10, pp. 18288–18300, Oct. 2022, doi: 10.1109/TITS.2022.3162038. 

passenger comfort. 

\[15\] C. Chen, Q. Xu, M. Cai, J. Wang, J. Wang, and K. Li, “Conflict-free However, our work still needs to be improved. Firstly, only cooperation method for connected and automated vehicles at unsignal-the longitudinal dynamics of vehicles is considered, but in the ized intersections: Graph-based modeling and optimality analysis,” IEEE

Trans. on Intell. Transp. Syst., vol. 23, no. 11, pp. 21897–21914, real world, the lateral and longitudinal dynamics are coupled, Jun. 2022, doi: 10.1109/TITS.2022.3182403. 

which will lead to unsatisfactory driving stability. Secondly, 

\[16\] J. Wang, X. Zhao, and G. Yin, “Multi-objective optimal cooperative the dynamic change of the vehicle’s expected driving direction driving for connected and automated vehicles at non-signalised interin the control area is not considered, yet there may be a section,” IET Intell. Transp. Syst., vol. 13, no. 1, pp. 79–89, Jan. 2019, doi: 10.1049/iet-its.2018.5100. 

temporary change of driving intention in the actual intersection

\[17\] Z. Yao, H. Jiang, Y. Jiang, and B. Ran, “A two-stage optimiza-scene. In order to solve these problems, we will introduce tion method for schedule and trajectory of CAVs at an isolated stability constraints and states representing driving intent into autonomous intersection,” IEEE Trans. Intell. Transp. Syst., vol. 24, the original problems in the future work, so as to enable the no. 3, pp. 3263–3281, Mar. 2023, doi: 10.1109/TITS.2022.3230682. 

\[18\] H. Jiang, Z. Yao, Y. Jiang, and Z. He, “Is all-direction turn lane a policy to improve driving stability and adapt to the intention good choice for autonomous intersections? A study of method devel-dynamics. 

opment and comparisons,” IEEE Trans. Veh. Technol., vol. 72, no. 7, pp. 8510–8525, Mar. 2023, doi: 10.1109/TVT.2023.3250957. 

\[19\] A. Mirheli, M. Tajalli, L. Hajibabai, and A. Hajbabaie, “A consensus-REFERENCES

based distributed trajectory control in a signal-free intersection,” Transp. 

Res. C, Emerg. Technol., vol. 100, pp. 161–176, Mar. 2019, doi:

\[1\] S. E. Li, S. Xu, X. Huang, B. Cheng, and H. Peng, “Eco-departure

10.1016/j.trc.2019.01.004. 

of connected vehicles with V2X communication at signalized inter-

\[20\] E. Lukose, M. W. Levin, and S. D. Boyles, “Incorporating insights sections,” IEEE Trans. Veh. Technol., vol. 64, no. 12, pp. 5439–5449, from signal optimization into reservation-based intersection controls,” 

Dec. 2015, doi: 10.1109/TVT.2015.2483779. 

J. Intell. Transp. Syst., vol. 23, no. 3, pp. 250–264, May 2019, doi:

\[2\] S. 

Djahel, 

R. 

Doolan, 

G. 

M. 

Muntean, 

and

J. 

Murphy, 

10.1080/15472450.2018.1519706. 

“A

communications-oriented

perspective

on

traffic

management

\[21\] K. Dresner and P. Stone, “Human-usable and emergency vehicle-aware systems for smart cities: Challenges and innovative approaches,” IEEE

control policies for autonomous intersection management,” in Proc. 

Commun. Surveys Tuts., vol. 17, no. 1, pp. 125–151, Jan./Mar. 2015, 4th Int. Work. Agents Traffic Transp. \(ATT\), Hakodate, Japan, vol. 12, doi: 10.1109/COMST.2014.2339817. 

May 2006, p. 14. 

Authorized licensed use limited to: Universitaet Bielefeld. Downloaded on January 22,2025 at 07:06:33 UTC from IEEE Xplore. Restrictions apply. 





Downloaded from https://iranpaper.ir

https://www.tarjomano.com

https://www.tarjomano.com

5388

IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 25, NO. 6, JUNE 2024

\[22\] D. Fajardo, T.-C. Au, S. T. Waller, P. Stone, and D. Yang, “Automated Yun Li \(Member, IEEE\) received the B.S. degree

intersection control,” Transp. Res. Rec., J. Transp. Res. Board, vol. 2259, in vehicle engineering from Jilin University in no. 1, pp. 223–232, Jan. 2011, doi: 10.3141/2259-21. 

2021 and the M.S. degree from the Department

\[23\] X. Qian, F. Altché, J. Grégoire, and A. Fortelle, “Autonomous inter-of Information and Communications Engineering, 

section management systems: Criteria, implementation and evaluation,” 

Tokyo Institute of Technology, in 2023. He is cur-IET Intell. Transp. Syst., vol. 11, no. 3, pp. 182–189, Apr. 2017, doi: rently pursuing the Ph.D. degree with the Graduate

10.1049/iet-its.2016.0043. 

School of Information and Science Technology, The

\[24\] G.-P. Antonio and C. Maria-Dolores, “Multi-agent deep reinforcement University of Tokyo. 

learning to manage connected autonomous vehicles at tomorrow’s inter-He completed a Progressive Graduate Minor in

sections,” IEEE Trans. Veh. Technol., vol. 71, no. 7, pp. 7033–7043, data science and artificial intelligence with the Jul. 2022, doi: 10.1109/TVT.2022.3169907. 

Department of Information and Communications

\[25\] M. W. Levin, S. D. Boyles, and R. Patel, “Paradoxes of reservation-Engineering, Tokyo Institute of Technology. He has gained practical research based intersection controls in traffic networks,” Transp. Res. A, Policy experience through an internship with Japan Data Science Research Labo-Pract., vol. 90, pp. 14–25, Aug. 2016, doi: 10.1016/j.tra.2016.05.013. 

ratories, NEC Corporation. He has contributed to the field with a patent

\[26\] Y. Bichiou and H. A. Rakha, “Developing an optimal intersec-submission and a paper presented at the IEEE Vehicular Technology tion control system for automated connected vehicles,” IEEE Trans. 

Conference \(VTC\). His research interests include reinforcement learning, Intell. Transp. Syst., vol. 20, no. 5, pp. 1908–1916, May 2019, doi: autonomous driving, large language models, and wireless communications. 

10.1109/TITS.2018.2850335. 

\[27\] Q. Lu and K.-D. Kim, “A mixed integer programming approach for autonomous and connected intersection crossing traffic control,” in Proc. 

IEEE 88th Veh. Technol. Conf. \(VTC-Fall\), Aug. 2018, pp. 1–6, doi:

10.1109/VTCFall.2018.8690681. 

\[28\] G. Lu, Z. Shen, X. Liu, Y. M. Nie, and Z. Xiong, “Are autonomous vehicles better off without signals at intersections? A comparative computational study,” Transp. Res. B, Methodol., vol. 155, pp. 26–46, Jan. 2022, doi: 10.2139/ssrn.3812649. 

Fei Gao received the Ph.D. degree in automotive

\[29\] M. Choi, A. Rubenecia, and H. H. Choi, “Reservation-based traffic engineering from Jilin University, China, in 2017. 

management for autonomous intersection crossing,” Int. J. Distrib. 

From 2014 to 2015, she was a Visiting Stu-

Sensor Netw., vol. 15, no. 12, Dec. 2019, Art. no. 1550147719895956, dent with the University of California at Berkeley, doi: 10.1177/1550147719895956. 

Berkeley, CA, USA. She is currently an Asso-

\[30\] L. Xu, J. Lu, B. Ran, F. Yang, and J. Zhang, “Cooperative merg-ciate Professor with the State Key Laboratory of ing strategy for connected vehicles at highway on-ramps,” J. Transp. 

Automotive Simulation and Control Automotive

Eng., A, Syst., vol. 145, no. 6, Jun. 2019, Art. no. 04019022, doi: Engineering, Jilin University. Her research interests

10.1061/jtepbs.0000243. 

include automotive human engineering. 

\[31\] H. Xu, Y. Zhang, L. Li, and W. Li, “Cooperative driving at unsignalized intersections using tree search,” IEEE Trans. Intell. Transp. Syst., vol. 21, no. 11, pp. 4563–4571, Nov. 2020, doi: 10.1109/TITS.2019.2940641. 

\[32\] A. Boukerche, D. Zhong, and P. Sun, “A novel reinforcement learning-based cooperative traffic signal system through max-pressure control,” 

IEEE Trans. Veh. Technol., vol. 71, no. 2, pp. 1187–1198, Feb. 2022, doi: 10.1109/TVT.2021.3069921. 

\[33\] M. Zhou, Y. Yu, and X. Qu, “Development of an efficient driving strategy for connected and automated vehicles at signalized intersections: A rein-Zhenhai

Gao

\(Member, IEEE\) was born in

forcement learning approach,” IEEE Trans. Intell. Transp. Syst., vol. 21, Changchun, Jilin, China, in 1973. He received the no. 1, pp. 433–443, Jan. 2020, doi: 10.1109/TITS.2019.2942014. 

Ph.D. degree in automotive engineering from Jilin

\[34\] Y. Guan, Y. Ren, S. E. Li, Q. Sun, L. Luo, and K. Li, “Centralized University. 

cooperation for connected and automated vehicles at intersections by He is currently the Deputy Dean of automo-proximal policy optimization,” IEEE Trans. Veh. Technol., vol. 69, tive engineering and the Director of the State Key no. 11, pp. 12597–12608, Nov. 2020, doi: 10.1109/TVT.2020.3026111. 

Laboratory of Automotive Simulation and Control

\[35\] Y. Xu, H. Zhou, T. Ma, J. Zhao, B. Qian, and X. Shen, “Leveraging Automotive Engineering, Jilin University. He is the multiagent learning for automated vehicles scheduling at nonsignalized coauthor of three books. More than 100 papers have intersections,” IEEE Internet Things J., vol. 8, no. 14, pp. 11427–11439, been published and 20 invention patents have been Jul. 2021, doi: 10.1109/JIOT.2021.3054649. 

authorized. His research interests include autopilot

\[36\] J. Achiam, D. Held, A. Tamar, and P. Abbeel, “Constrained policy technology and human engineering. 

optimization,” in Proc. Int. Conf. Mach. Learn., Aug. 2017, pp. 22–31. 

Prof. Gao is a Distinguished Member of the Expert Committee Intelligent

\[37\] J. Schulman, S. Levine, P. Abbeel, M. Jordan, and P. Moritz, “Trust Connected Vehicle Innovation Alliance, the Chairperson of the Industrial region policy optimization,” in Proc. Int. Conf. Mach. Learn., Lille, Design Association in Jilin Province, and an Editorial Board Member of France, Jul. 2015, pp. 1889–1897. 

International Journal of Human Factors Modelling and Simulation. 

Rui Zhao \(Member, IEEE\) was born in Liaoyuan, 

Jilin, China, in 1986. She received the B.S. degree in computer science and technology from Northeast Normal University in 2009 and the Ph.D. degree in Tianyao Zhang was born in Changchun, Jilin, 

computer science and technology from Jilin Univer-China. She received the bachelor’s degree from

sity, Changchun, China, in 2017. 

Jilin University in 2016 and the master’s degree in She is currently an Associate Professor with the automotive engineering from Clemson University in College of Automotive Engineering, Jilin University. 

2018. She is currently an Engineer with the National She has authored about 30 journal articles and ten Key Laboratory of Vehicle Simulation and Control, patents in China. She authored the monograph Cyber Jilin University. Her research interests include the Security Technology for Intelligent Automotive. Her HMI design of intelligent cockpits. 

research interests include cooperative control, functional safety, cybersecurity, and safety reinforcement learning for connected and automated vehicles. 

Prof. Zhao is a member of the Society of Automotive Engineers. 

Authorized licensed use limited to: Universitaet Bielefeld. Downloaded on January 22,2025 at 07:06:33 UTC from IEEE Xplore. Restrictions apply.



