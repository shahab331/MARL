IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 25, NO. 11, NOVEMBER 2024

16235

Heuristic-Based Multi-Agent Deep Reinforcement Learning Approach for Coordinating Connected

and Automated Vehicles at Non-Signalized

Intersection

Zihan Guo , Yan Wu , Lifang Wang , Member, IEEE, and Junzhi Zhang, Member, IEEE

Abstract— One typical application of connected and automated provide opportunities to resolve these challenges, where vehicles \(CAVs\) is to coordinate multiple CAVs at a non-signalized vehicle-to-vehicle communication \(V2V\) can offer immediate intersection in mixed traffic, and it may take advantage of state

information

of

ego

CAV’s

surrounding

vehicles

multi-agent deep reinforcement learning \(MDRL\) approaches to \(e.g., acceleration, velocity, position\), and messages about improve the overall coordination efficiency. This study proposes a heuristic-based MDRL algorithm \(H-QMIX\) developed based neighboring traffic or some driving behavior recommendations on a value-based MDRL algorithm, QMIX. This algorithm can be transmitted to ego CAV via vehicle-to-infrastructure incorporates a heuristic-based action mask module to guide \(V2I\) technologies. Moreover, coordinating multiple CAVs CAVs efficiently and safely through intersections, composed realized by the aforementioned CAV-related technologies of a stimulative passing sequence and safety restrictions on may raise road capacity and thus improve traffic efficiency. 

CAVs’ action space in the junction area. Compared with other MDRL algorithms \(e.g., IPPO, QMIX\), the H-QMIX algorithm In addition, it can reduce the fuel consumption of CAVs, and demonstrates improved training performance in terms of safety simultaneously ensure safety by avoiding potential car crashes. 

and efficiency in two case studies, where the first requires all However, coordinating multiple CAVs at non-signalized CAVs to affix their routes, and another allows CAVs to choose intersections in urban environments remains demanding. 

random routes. Concerning the model’s generalization ability, The coordination under this scenario may be complicated the trained models with the maximal episodic return are then transferred to a more practical scenario with a certain vehicle-to-owing to a three-dimensional collaboration, as discussed in the vehicle \(V2V\) communication delay in a zero-shot manner. The survey \[2\]. One must consider the coordination of longitudinal simulation results illustrate that H-QMIX is robust to a certain and lateral motions and the temporal dimension, including the communication delay. The code for this paper is available at: order of CAVs’ entries. The complexity of coordination makes https://github.com/flammingRaven/heuristic\_based\_qmix. 

advanced communication and autonomous driving modules Index Terms— Non-signalized intersection management, multi-such as sensing, decision-making, planning, and control agent deep reinforcement learning, zero-shot generalization, indispensable. 

communication latency. 

The current research around the coordination of autonomous I. INTRODUCTION

vehicles ranges from cooperative perception to cooperative P

decision-making and motion planning. The former aims to EOPLE’S travel has become more accessible due to the address issues in single-vehicle perception using 3D LiDAR, whirlwind evolution of the transportation system. However, the population growth and the rapidly increasing vehicle such as occlusion and out-of-range problems \[3\]. Our study demand have also brought some safety, traffic efficiency, focuses on the latter, especially the research of cooperative decision-making at signal-free intersections. The related and environmental concerns \[1\]. Fortunately, the advent approaches in recent literature include heuristics or optimiza-of connected and autonomous vehicle \(CAV\) technologies tion techniques \[4\], \[5\], \[6\], game theory \[7\], \[8\], single-agent

Manuscript

received

4

August

2023; 

revised

7

February

2024; 

deep reinforcement learning \(DRL\) \[8\], \[9\], \[10\], \[11\], \[12\], 

accepted 28 May 2024. Date of publication 11 October 2024; date of

\[13\], and the combination of DRL and game theory \[14\], 

current version 1 November 2024. This work was supported in part by the National Key Research and Development Program of China under Grant among which the researches involving deep reinforcement 2022YFB2503105; and in part by the Institute of Electrical Engineering, learning are proliferating. Concerning the heuristic-based Chinese Academy of Sciences under Grant E1553301. The Associate Editor method, some limitations cannot be circumvented. For exam-for this article was K. Dey. \(Corresponding authors: Yan Wu; Lifang Wang.\) Zihan Guo, Yan Wu, and Lifang Wang are with the Key Laboratory of High ple, the classic first-in-first-serve \(FIFS\) policy \[4\] cannot

Density Electromagnetic Power and Systems \(Chinese Academy of Sciences\), tackle the vehicles with higher priority \(e.g., emergency vehi-Institute of Electrical Engineering, Chinese Academy of Sciences, Beijing cles\), and the reservation request sent by one vehicle to this 100190, China, and also with the University of Chinese Academy of Sciences, Beijing 100049, China \(e-mail: zh\_guo97@163.com; wuyan@mail.iee.ac.cn; policy can only be processed after that vehicle enters the wlf@mail.iee.ac.cn\). 

intersection. Further, the researchers developed a centralized Junzhi Zhang is with the State Key Laboratory of Automotive Safety and controller to coordinate the vehicles for optimization-based Energy, Department of Automotive Engineering, Tsinghua University, Beijing 100084, China \(e-mail: jzhzhang@mail.tsinghua.edu.cn\). 

methods \(e.g., iCACC \[6\]\). Consequently, the computation Digital Object Identifier 10.1109/TITS.2024.3407760

demand will likely increase rapidly as the number of managed 1558-0016 © 2024 IEEE. Personal use is permitted, but republication/redistribution requires IEEE permission. 

See https://www.ieee.org/publications/rights/index.html for more information. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:38:48 UTC from IEEE Xplore. Restrictions apply. 

16236

IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 25, NO. 11, NOVEMBER 2024

vehicles increases. Another exciting line of work is based In the first case, the routes of all CAVs are fixed and become on game theory or itself with the combination of DRL

random in the second. The training performances of H-QMIX, \(\[7\], \[8\], \[14\]\), which present the capability to handle the IPPO, and QMIX are compared in the form of convergence possible deadlocks at the intersection zone, but most papers speed and success rate. 3\) transferring the trained models with are only concerned with a small number of controlled CAVs the maximum episodic return in a zero-shot manner to an without investigating the interactions between CAVs and the unseen scenario with an unavoidable communication delay. 

human-driven vehicles \(HDVs\). From a practical point of view, The H-QMIX policy can gain a better success rate than IPPO, studying the behaviors of CAVs under the mixed traffic flow despite the slightly increased traveled time. Collectively, the is necessary since CAVs and HDVs may coexist for decades robustness of H-QMIX to a particular communication delay is in the future transportation system. 

verified. 

Compared with the optimization-based methods, single-The rest of this paper is arranged as follows. Section II

agent DRL algorithms such as MA-PPO proposed in work \[5\], 

reviews the research papers relevant to our study. A brief or approaches developed based on deep Q-learning \[9\], have introduction of necessary background knowledge of DRL

the potential to become more computationally efficient and formulation and fundamental principles behind the QMIX

can reduce the queuing phenomenon to improve the traffic algorithm is given in Section III. Further, Section IV elaborates efficiency at intersections. However, they need to overcome on formulating an RL problem from a target scenario of the dimension explosion introduced by centralized controllers. 

coordinating multiple CAVs. Section V systematically reveals A natural idea is to directly deploy the single-agent DRL

the details of the methods proposed in this study, and then the framework for each agent in the multi-agent environment. 

experimental results are demonstrated in Section VI. In the Nonetheless, the trained policy may vary frequently with the end, Section VII summarizes this study and offers future constantly changing strategies of other agents \[15\]. Further, works. 

the researchers propose a multi-agent reinforcement learning \(MARL\) or multi-agent deep reinforcement learning \(MDRL\) II. RELATED WORK

approach to solve the non-stationarity problem. The centralized training and decentralized execution \(CTDE\) framework A. DRL Approaches for Unsignalized Intersection is one of the famous architectures in this field. The approach The DRL algorithms applied to the scenarios of unsignal-explored in our previous work \[16\] was relied on QMIX \[17\]

ized intersections in recent literature are progressively pop-following the CTDE structure, upon which several code-level ularized. In research \[9\], the authors employed a deep Q

implementation tricks modified. Although the modified QMIX

learning method to train the decision policy of the vehicle can obtain better results than the centralized algorithm PPO in with restricted sensing ability, and the trained strategy can the examined scenarios, the scenarios utilized for evaluating drive the ego car to pass the T-intersection safely and effi-the algorithm’s performance were still simplified and ideal-ciently. Precisely, three distinctive high-level representations ized, with CAVs fixing their routes and V2V communication of action space \(i.e., “time-to-go,” sequential actions, and assumed to be perfect. Moreover, one should note that the pre-

“creep-and-go”\) were schemed, where the format of “creep-ceding DRL-based or MDRL-based policies may face several and-go” motivates the action mask design in our work. 

common issues: low sample efficiency and poor generaliz-They demonstrated that the success rate of the “time-to-go”-

ability to unseen data distributions because of over-fitting the based algorithm reached the top compared to all other action existing tasks. These challenges, plus the scenario idealization patterns and rule-based time-to-collision \(TTC\) baseline. 

problem of our previous work being difficult to apply to more Guan et al. \[10\] extended the proximal policy optimization realistic scenarios, motivate the design of our heuristic-based \(PPO\) architecture to control the signal-free intersection in QMIX \(H-QMIX\) in this study. We first enhance the action a centralized manner with an environment model representing mask mechanism in the QMIX algorithm by the proposed the longitudinal behaviors of the vehicles and providing virtual heuristics module composed of two parts, whose primary goal samples to accelerate the training. The simulation results illus-is to speed up the convergence of the MDRL algorithm to trated the suggested methods’ better computation efficiency some extent. The ability of the traffic light model in paper \[4\]

and robustness than the MPC baseline and the original PPO

inspires the first portion to tackle the deadlock situations by algorithm. As for the decision-making of a single vehicle at pre-defining the passing order. The second portion narrows the an unsignalized intersection, Shu et al. \[11\] schemed out three available action space by removing invalid actions that may different driving tasks for the ego car \(left turn, right turn, cause emergencies. 

and going straight\) and then utilized dueling deep Q-learning The key contributions of this paper are: 1\) adding a to train its decision strategy. Afterward, they employed the heuristic-based action mask module based to the baseline, transfer learning of reusing the parameters of neural networks QMIX. This module stimulates CAVs to pass through inter-to transfer the learned policy from the source task to the rest of sections in a pre-set order and imposes safety constraints the predefined driving tasks. The corresponding success rate on CAVs lingering in the intersection area; 2\) building two confirmed the transferability of the decision policy between scenarios under the mixed traffic flow with the aid of the similar driving tasks. Moreover, the traffic efficiency was Simulation of Urban Mobility \(SUMO\) simulator, in which improved. 

our H-QMIX policy controls the speed of CAVs, and HDVs’

Vinitsky et al. \[12\] constructed a benchmark called FLOW

behaviors are defined by the built-in car-following model. 

for applying DRL methods to the various mixed-autonomy Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:38:48 UTC from IEEE Xplore. Restrictions apply. 

GUO et al.: HEURISTIC-BASED MDRL APPROACH FOR COORDINATING CAVs 16237

traffic scenarios, including the merging, bottleneck, single-a decentralized multi-agent learning approach for coordination lane unsignalized intersection of figure-eight shape, a road based on tabular Q-learning. The AIM problem was modeled network composed of multiple traffic signal light-controlled as a multi-agent Markov decision process \(MDP\) with global intersections. Furthermore, they tested two DRL algorithms state space disintegrated into independent and coordinated \(Trust Region Policy Optimization \(TRPO\) and PPO\) on parts and action space represented by discrete accelerations. 

merging scenarios. They illustrated the superiority of DRL

The DCL-AIM method could identify and dynamically deter-methods over evolutionary strategies and augmented random mine whether the current vehicles entering the intersection search. Further, Peng et al. \[13\] applied the generalized advan-zone needed to coordinate with the others and update the tage estimation \(GAE\)-based PPO method to one extended single action value table when there was no necessity for benchmark scenario of FLOW, a double-lane uncontrolled coordination and joint action value table when the possible intersection with figure-eight shape, where two CAVs led the conflict was detected. They compared its performance with traffic flow. The number of cumulative stopped vehicles was traditional AIM baselines and traffic signal light-based meth-reduced after deploying the trained policy, and hence the traffic ods. The results demonstrated that the DCL-AIM method efficiency was enhanced. 

can improve traffic efficiency. For other cooperative driving scenarios, Peng et al. \[27\] applied a novel MDRL method Coordinated Policy Optimization \(CoPO\), whose idea was B. MDRL and Its Applications to Cooperative Autonomous based on the combination of PPO and QMIX to several typi-Driving

cal multi-vehicle scenarios \(roundabout, intersection, tollgate, In this sub-section, the current MDRL research and MDRL’s bottleneck, parking lot\). CoPo was designed as a two-level applications to several typical cooperative autonomous driving algorithm, with the low-level concentrating on the local coor-scenarios, such as non-signalized intersection management dination by using a reward weighted by local coordination and highway merging, are briefly reviewed. The mainstream factor \(LCF\) and the high level automatically searching for framework for MDRL research is the CTDE architecture, the best LCF value by deriving a global value-function-based which can be further categorized into value-based and objective. Compared to the other MDRL methods, such as gradient-based methods. Regarding the former type, value independent PPO, and mean field MARL, CoPo can achieve a decomposition networks \(VDNs\) \[18\] directly decomposed the better success rate among most scenarios and display diverse global action-value function computed from observations of social behaviors. 

all agents into the sum of individual action-value functions. 

However, the simple summation of an individual’s value limits C. Transfer Learning in Autonomous Driving

the representation ability of global function. To overcome One primary problem of reinforcement learning is that this problem, Rashid et al. \[17\] extended the VDNs to the tremendous interactions with the expert-defined environment QMIX framework, in which the proposed monotonic con-are required, which is cost-consuming for real-world scenar-straints replaced the summation to achieve better expressivity. 

ios, such as autonomous driving applications. Therefore, the Although the research \[19\] and \[20\] attempted to unleash researchers propose transfer learning to address this problem, further the representation ability of QMIX, a recent study \[21\]

where the skills learned by an agent in the source task\(s\) can suggested that QMIX after code- or hyperparameter-level fine-be directly or indirectly employed to accelerate the learning tuning can still obtain the state-of-the-art results on StarCraft in the target task \[28\]. Authors of work \[29\] proposed a Multi-agent Challenge \(SMAC\) task \[22\], a commonly used DQN-style \(D3QN\) algorithm \(DQ-GAT\) based on graph benchmark in MDRL community. The second line of the attention that functioned to model the interaction between MDRL study focused on using policy gradient to solve vehicles implicitly. The policies attained from the emulative continuous control problems, such as MADDPG \[23\] and

experiments could be transferred to a real-world traffic dataset M3DDPG \[24\] combining the idea of game theory with without losing real-time processing ability. Candela et al. \[30\]

MADDPG. One hazard of the MADDPG approach is that utilized the MAPPO algorithm to train a multi-agent policy in its computational complexity dramatically increases with the the Duckietown multi-robot testbed. Then the various levels number of agents, and that it is difficult to generalize to more of domain randomization were involved in the policy transfer, complex tasks. 

indicating that the Sim-to-Real gap can be reduced from the As discussed in Section I, the non-stationarity problem \[15\]

experimental results. Moreover, the policy transfer can be may be resolved by the MARL or MDRL methods, which implemented by a motion skill library, which was constructed are constantly emerging in recent academia. For instance, the in the study \[31\], and the motion skills in it were further MADDPG algorithm was exploited in a highway merging distilled into a latent skill space at which the RL algorithm can scenario with three various driving tasks \(rear-end colli-heavily explore. The improvement of the exploration efficiency sion avoidance, lateral collision avoidance, and coordination was validated in three dense-traffic scenarios. 

of eight CAVs\) \[25\]. The trained policy can eliminate III. PRELIMINARIES

the stop-and-go behavior of vehicles. However, besides the problems described above, the authors did not consider A. Decentralized Partially Observable Markov Decision the effects of introducing multiple CAVs into the traffic Process

flow. The research \[26\] employed the DCL-AIM to handle An MDP denoted by a tuple \(S, A, T, r, γ \) provides a the autonomous intersection management \(AIM\) problem, supportive theoretical tool to characterize the reinforcement Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:38:48 UTC from IEEE Xplore. Restrictions apply. 

16238

IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 25, NO. 11, NOVEMBER 2024

learning problem, whose state and action space are expressed B. Deep Q-Learning and QMIX

by S ∈

n

m

R

and A ∈ R

with the dimensionality of n and

The traditional tabular Q-learning is overshadowed by the m, respectively. The function of state transition is symbolized flourish of Deep Q-learning \[34\], in which the action-value as T : S × A × S → R. r : S × A × S → R is the function becomes parameterized as Q\(·; θ\) implemented by reward function based on a tuple of the current state and deep neural networks, and the replay memory composed of action plus the following state information \(st , at , st\+1\), and batches of transition data \(s, a, r, s′\) is creatively employed the last element in this tuple is discount factor, γ ∈ \(0, 1\). 

to facilitate the stability of the training process. The goal of At each time step, the action based on the agent’s policy: the training process is to minimize the following loss function π : S × A → \[0, 1\] is executed. The core of the RL problem based on TD error, during which the parameter θ of deep Q

is to optimize the agent’s policy π by searching the maximum networks \(DQNs\) are updated:

state-values from the value function V π \(s\) via traversing all b

states s



t ∈ S, where V π \(s\) is interpreted as the expectation of X



L\(θ\)

target

=

y

− Q\(s, a; θ\)2

\(3\)

discounted cumulative reward from a state s:

i

i =1

" ∞

\#

where ytarget = r

X

t \+ γ maxa′ Q\(s′, a′; θ ′\). Another innovative V π \(s\) = Ea

γ l−tr

\(1\)

t ,st\+1,... 

t |st = s

trick is to replicate the parameters of network θ to those of l=t

the target network \(θ′\). The target network keeps unvarying at a fixed frequency. 

where

at

and

st\+1

are

sampled

from

π\(at|st\) and

When attempting to address a multi-agent problem, one may T \(st\+1|st , at \), respectively, and rt is short for r\(st , at , st\+1\). 

utilize Independent Q-learning \(IQL\) \[35\] to transform the Another value function Qπ \(s, a\) is particularly served for the whole problem combined with several single-agent scenarios. 

state-action value, which is defined in a similar fashion: However, IQL theoretically cannot resolve the aforementioned non-stationarity problem. Nevertheless, IQL is still one of

" ∞

\#

X

Qπ \(s, a\) =

the baselines for researchers to tackle some games with Es

γ l−tr

\(2\)

t \+1,at\+1... 

t |st = s, at = a

cooperation and competition \[36\]. 

l=t

VDNs are investigated based on IQL, in which the joint However, in some real-world applications, an agent value function Qtot \(τ , a\) is simply decomposed by the indi-equipped with physical sensors may have restricted perception vidual action-value function Qi \(τi , ai ; θi \), where τi , ai , θi , capabilities resulting from particular sensors’ intrinsic nar-a ∈ AN denote local trajectory, local action, parameters row line of sight or some occlusions. A popular framework of individual state-action value function, and joint action under this presumption is called partially observable MDP

respectively, and τ ∈ T N symbolizes a history trajectory of \(POMDP\) \[32\], whose definition is similar to that of MDP

joint action-observation. The following equation demonstrates except that the observation function is introduced. A tuple this decomposition rule:

\(S, A, , T, O, r, γ \) is used to describe the POMDP model, N

in which the additional term is  denoting the observation set. 

X

Qtot \(τ , a\) =

Qi \(τi , ai ; θi \)

\(4\)

The probability function of emitting observations is defined as i =1

O : S × A ×  → \[0, 1\]. 

The loss function of DQN, Q in eq. \(3\), is substituted by Qtot Furthermore, the decentralized partially observable Markov in VDNs. 

decision process \(Dec-POMDP\) \[33\] is proposed to extend However, one problem of VDNs is that the additive nature POMDP to a fully cooperative multi-agent setting. The tuple of value decomposition restricts the representation capability in POMDP is modified as G = \(I, S, \{Ai \}, T, r, \{i \}, O, γ \), of the value function. QMIX algorithm proposes a monotonic where I ∈

N

R

contains all agents in the problem, s ∈ S

value decomposition mechanism established on the individual-symbolizes the ground-truth state from which the observations global-max \(IGM\) principle \[19\] to avoid this limitation. 

are derived. The individual action set of agent i ∈ I is The following equation interprets the core of the IGM

denoted by Ai , and the joint action space is defined as a principle:

Cartesian product of individual action space: A = ×i Ai . 





a ∈ A specify one joint action executed by the entire group arg maxa Q

1

1\(τ1, a1\)

. 

of agents. T is similar to the definition of a state transition arg max Q



. 



t ot \(τ , a\) =

. 

\(5\)





probability function in MDP formulation, except that a joint a

arg maxa Q

N

N \(τN , aN \)

action space replaces the action space. One should note that the reward function r in Dec-POMDP only produces a scalar where the optimization of individual agent’s value function \(e.g., dimension is 1\). Additionally, a set of joint observations denoted by \[Qi : T × A → R\]N

is equivalent to the

i =1

is denoted by  = ×

global optimal joint action derived from the corresponding i i , where i describes the individual

observation space for agent i ∈ I . O : S × A ×  → \[0, 1\] is joint action-value function Qtot : T N × AN → R

similar to its counterpart in POMDP except that the joint state, Furthermore, it is sufficient to enforce the monotonicity action, and observation become the independent variables for constraint to fulfill the IGM principle, as shown in eq. \(5\)

one specific function, that is, O\(o, a, s′\) = Pr\(o|a, s′\). The

∂ Qtot\(τ, a\) ≥ 0, ∀i ∈ I

\(6\)

meaning of the discount factor γ remains the same. 

∂ Qi\(τi, ai\)

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:38:48 UTC from IEEE Xplore. Restrictions apply. 





GUO et al.: HEURISTIC-BASED MDRL APPROACH FOR COORDINATING CAVs 16239

IV. TRAINING SCENARIO AND RL PROBLEM

FORMULATION

A. Training Scenario

A signal-free isolated junction scenario with four road segments, each containing four lanes \(two for outgoing and two for incoming\) under mixed-autonomy traffic of 300veh/hour/lane are constructed, as illustrated in Fig. 1

\(detailed information about two case studies refers to Section VI\). The traffic density value follows the parameter settings of the Grid scenario in research \[12\]. In our training scenario, H-QMIX policy is employed to control a fixed number of CAVs \(i.e., 8 CAVs\), which is consistent with the number of incoming lanes in each road arm. The HDVs’

behaviors can be represented by a specific car-following model. The background knowledge of car-following models may refer to the research \[37\]. The criterion of task accomplishment is that each CAV leaves the intersection without collisions with HDVs or other CAVs. 

In general, the trajectories of all vehicles are generated by the route definitions defined with the SUMO configuration file, and the following kinematic equations can describe the longitudinal motion of each CAV:

1

xi \(t \+ 1\) = xi \(t\) \+ vi \(t\) · 1 \+ ai \(t\) · 12

2

vi\(t \+ 1\) = vi\(t\) \+ ai\(t\) · 1, 

\(7\)

where the position of vehicle i at time step t is denoted by xi \(t\), the velocity and acceleration of vehicle i are recorded by vi and ai , respectively. The decision period is set to 1. 

Fig. 1. Illustrations of typical intersection scenarios for case studies 1 and 2, where the junction comprises four road segments and two lanes. a\) Scenario for case 1 sets each CAV only to hold stationary route, 2\) scenario for B. RL Formulation

case 2 allows each CAV to select routes randomly. Moreover, the number of CAVs is fixed to equal the number of lanes. CAVs controlled by the MDRL

The following assumptions are made to handle the CAVs algorithm are colored in red, and HDVs in this scenario are colored in yellow. 

coordination problem:

The intersection and control zone ranges are also shown in this figure. 

a\) V2V communication is perfect during the training phase and may become latent with a certain time delay when the trained models are evaluated. 

1\) State, Observation and Action Space: The following b\) The local observation of each CAV includes its position, information fills the observation space:

speed, and some binary flag information, such as the oi = \[x

, tw, f i

, f i , f i

\]

\(8\)

waiting time of the lane on which the CAV resides and i , yi , vi , dimin

ent er

out

r out e

the minimum distance between the neighboring vehicles, In which \[xi , yi , vi \] corresponds to the Cartesian coordinates excluding those CAVs from non-conflicted directions. 

of each CAV \(i = 1, 2, . . . , 8\) relative to the junction origin Moreover, to implement partial observability, all con-and speed, respectively. di

suggests the minimum relative

mi n

trolled CAVs cannot explicitly acquire the position and distance between the i -th and its closest vehicle, tw records speed of other HDVs surrounding them. 

the waiting time in ego vehicle i ’s driving lane. Moreover, c\) All CAVs’ lateral behaviors are predefined by SUMO

the binary flag f ienter represents whether one CAV enters the routes, and the HDVs are not allowed to perform intersection \(set to 1\) or not \(set to 0\). The same applies to f iout lane-changing according to their predefined route. 

when the vehicle leaves the intersection. The last binary flag The H-QMIX policy provides the acceleration value for f iroute is set to 0 when a CAV chooses the primary route, and each CAV’s interaction with the environment. Then the target 1 for the secondary route, the specific probability of selecting speed is naturally derived from these acceleration values. The one route is shown in Section VI. The global state space RL problem is basically similar to that in our previous work, concatenates each CAV’s observation vector, i.e., s = \[oi \]N . 

i =1

except that more variables and binary flags are added to the The action space representation is equivalent to that in our observation space and that the reward function considers more previous work, except that the acceleration granularity in this terms, as introduced in the next two paragraphs: study is modified a bit to ease the design of the heuristic-based Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:38:48 UTC from IEEE Xplore. Restrictions apply. 

16240

IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 25, NO. 11, NOVEMBER 2024

action mask module, whose particular values are revealed in V. METHODS

Section VI. The motivation for discretizing action space with A. Algorithm Architecture

the appropriately chosen granularity is to shrink the larger The basic procedures of training an H-QMIX policy are search space if one alternatively considers the continuous shown in Fig. 2, composed of an H-QMIX learner and action space. Moreover, the granularity value can be adjusted several SUMO-based parallel workers used to collect batches according to how stringent the accuracy requirement of an of episodic data. The H-QMIX learner generally has three application is. 

significant modules: the agent network, the mixing network, 2\) Reward Function Design: Our reward design obeys one and the heuristic-based action mask. The agent network is built rule of thumb in RL application: one large positive reward with the aid of the parameter-sharing mechanism. Specifically, when the task is accomplished and multiple minor negative only one agent network is employed to serve all controlled punishments. To be consistent with the goal of one successful agents. The input of the shared agent network is just the local episode that each CAV needs to cooperate with others to maxi-information of one single agent, and similarly, the output of mize their traffic efficiency and keep safe, we incorporate three this network is the Q value of this agent. However, one should macro aspects into the reward function: 1\) traffic efficiency, notice that this technique may destabilize the training process. 

2\) collision avoidance, and 3\) rewarding the successfully The advantage of parameter-sharing mechanism lies in the explored joint action sequences. 

fact that it may resolve the scalability issue when the input For traffic efficiency, CAVs driving with speed lower than dimension is exponentially spanned due to the rising number the predefined minimum speed and waiting for a long time at of learning agents. Regarding the input and output of the agent the control or junction zone would be punished, as shown in network, it is fed with data comprised of each CAV’s local the following expression:

observations concatenated with its unique vector identifying N

Nl

itself coded in one-hot form, and yields action values Qi of X

X

ref f = −

α1 · I\(vi < Vmin\) −

α2 · t jw − α3 \(9\) the agent i for all possible discrete actions. These action values i =1

j =1

are one part of the intake of the hypernetworks constituting the in which the indicator function

downstream mixing network module, such as W

I\(·\) is set to 1 given that

1, W2, b1, b2. 

v

Eventually, the mixing network outputs Q

i < Vmi n , or 0 otherwise, where Vmi n is the minimum speed t ot , an estimate of

for all CAVs in the scenario. N

the scalar reward when agents execute their joint actions. 

l signifies the total number

of lanes. The rest of the parameters α

The parameters of the hypernetworks are produced via fully 1, α2, α3 are of minor

value and adjustable before the training. α

connected networks conditioning on the global state s 3 functions as a

t and

small stimulus to push each vehicle to accomplish the task as various activation layers such as rectified linear unit \(ReLU\) fast as possible. 

units \[38\]. Notably, an absolution operation is utilized to create Moreover, one way to emphasize the safety issue is to weights of W1, W2 to enforce the monotonicity constraint of punish severely the CAVs whose collision with other vehicles the IGM principle as discussed in Section III. 

cannot be avoided, which is expressed as r

The last important module is the heuristic-based action ca . 

mask, whose procedures are elaborated in the following sub-N

X

section. In essence, this module functions as a decision-maker rca = −

α4 · I\(Collision\)

\(10\)

providing macro action for agents. Besides, it bridges the i =1

learner and the parallel workers. These multiple workers are Fortunately, the SUMO simulator can automatically detect responsible for applying the updated joint actions derived from the occurred collisions, and α4 is also an adjustable parameter the ε-greedy policy with decreasing ε to the SUMO simulator. 

before the training. 

Subsequently, they should collect the resultant episodic tran-The last part of the reward function is to award the suc-sitions consisting of pre-transition and post-transition data in cessful explorations. A small reward is given to a partially parallel, push them back into the replay memory, and return completed task to encourage the subsequent compelling explo-those cached data to the upstream learner. The number of total ration and a large reward to the eventually successful decision workers is adjustable and may be matched with the perfor-making, which is shown as:

mance limit of related hardware. As for the backpropogation, the gradient descent algorithm serves to update the parameters rsuccess = \(l0 − lcur \) · I\(success\) \+ C \+ α5 · npass \(11\)

of each network, where the gradient is computed correspond-l0 denotes the maximal episode length set before the training ing to the loss function L\(θ\) introduced in Section III. The process, lcur represents the episode length of the current H-QMIX is implemented based on PyMARL framework \[22\], 

successful episode, and C is a constant. n pass logs the number an MDRL algorithm suite. 

of vehicles that left the intersection without collision, and α5 is another adjustable parameter. The condition of task B. Heuristic-Based Action Mask accomplishment depends on the following criteria: The pseudo-code of the heuristic-based action mask is a\) There are not any vehicles colliding with the others, shown in algorithm 1. The motivation of the heuristic-based including HDVs and CAVs; 

action mask module is to shrink the size of available b\) The CAVs has passed the intersection without any colli-action space by removing the invalid actions that may cause sions \(i.e., f ienter and f iout are both set to 1\). 

safety-related issues and hence boost the searching efficiency Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:38:48 UTC from IEEE Xplore. Restrictions apply. 





GUO et al.: HEURISTIC-BASED MDRL APPROACH FOR COORDINATING CAVs 16241

Fig. 2. 

The overall architecture of the H-QMIX algorithm contains two portions, 1\) H-QMIX learner consisting of an agent network with parameter sharing mechanism, mixing network constructed by hypernetworks and heuristic-based action mask bridging the learner and workers, and 2\) multiple parallel workers, who are responsible for collecting batches of episodic data from SUMO-based environment. 

of the MDRL algorithm to some extent. We incorporate two intersection, or otherwise, it is warned to decelerate or keep aspects of considerations into this action mask module. First, the current speed. 

the order of traffic before all CAVs enter the junction is defined Second, all CAVs are supervised by the action mask mod-inspired by light models in research \[4\], corresponding to the ule to avoid emergencies during the coordination stage at list H defined in algorithm 1. It can drive all CAVs to enter the the intersection area, demonstrated by lines 10-16. Specif-intersection with a predefined order based on the priorities of ically, one CAV can observe the minimal distance between each direction at non-signalized intersections. For example, the itself and the surrounding vehicles excluding CAVs from the vehicles turning left should yield to ones going through. As a non-conflicting area \(i.e., the same group defined in list H \) result, the first element of H is composed of going-through and and must decelerate with maximal deceleration given that such right-turning routes and then left-turning routes in the same distance is lower than the predefined threshold ds and current direction. The rest of the elements follow the same alternation. 

speed more significant than a specific value. Additionally, The declaration of those four phases is similar to those in the traffic efficiency is another significant metric to evaluate the traffic signal light system, except that each cycle holds for coordination task of multiple CAVs. Therefore, the module is far fewer timesteps and acts as a deadlock-breaker. Lines 4-9

designed to encourage one CAVs to drive as fast as possible show that if one CAV stays in one period of a particular with no worries about the surrounding participants if it is in phase, it should accelerate with greater values to approach the a safe area, as shown in lines 14-16. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:38:48 UTC from IEEE Xplore. Restrictions apply. 

16242

IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 25, NO. 11, NOVEMBER 2024

Algorithm 1 Heuritics-Based Action Mask

TABLE I

Data: The ego vehicle’s identification: i , A list H

PARAMETERS OF SCENARIOS AND RL ENVIRONMENT

consisted of four groups of potential routes: \{\(NS, NW, SN, SE\), \(SW, NE\), \(WE, WS, EW, EN\), \(WN, ES\)\}. For instance, NS denotes a route going from north to south. Current time t , Time period for each phase Tp, Ego i’s route Ri , Minimum relative distance between the ego and the other vehicles dm, Ego vehicle’s current speed vc, Maximum

speed constraint vmax

Result: Available actions with dimension K

1 Set the status of the binary flag denoting ego i coming into the intersection f ienter , another binary flag f iout denoting ego i driving out of the intersection, and binary flag f iroute denoting ego i’s specific route 2 Set the distance thresholds for the safety ds and the efficient passing dq

3 Set two speed ratios σ1, σ2, where σ1 < σ2

4 if \! f i

then

ent er and \! f i

out

5

for j = 1, . . . , 4 do

6

if Ri is in H \[ j\] and \( j − 1\) · Tp <= t < j · Tp then

7

Allow ego i to accelerate with greater values 8

else

9

Warn ego i to decelerate or keep the current

speed

10 if f i

then

ent er and \! f i

out

in which ytarget in eq. \(3\) is replaced by Gλ, and λ, the l

11

Compute the minimum relative distance dm between discount factor of traces is satisfied with the condition of the ego i and the other vehicles excluding ones from Qt

λ = 1 when t = 0. 

l=1

the non-conflicting routes

2\) Improving the network-level techniques. Altering the 12

if dm <= ds and vc > σ1 · vm then

optimizer of the original QMIX from RMSProp \[17\] to

13

Warn ego i to decelerate with maximum

Adam \[40\] can make a positive impact on the training process. 

deceleration

14

else if dm <= dq and vc < σ2 · vm then

VI. SIMULATION AND ANALYSIS

15

Allow ego i to drive with maximum acceleration 16

else Allow ego i to accelerate ; 

A. Experimental Settings

Two case studies are designed to illustrate the efficacy of our H-QMIX algorithm, where we conduct the several coordination tasks of multiple CAVs at the signal-free isolated C. Implementation Tricks

intersection with four ways and two lanes in this section. 

The asymptotic performance of the QMIX algorithm can be Table.I shows the parameters applied in each case study. For enhanced by code-level implementation tricks, as illustrated in the basic information of constructed scenario, each road seg-paper \[21\]. Consequently, some tricks are selectively applied ment is set to 100m with a traffic density of 300veh/hour/lane, as follows:

and CAVs start at 3m/s and cannot surpass 15m/s. Moreover, 1\) Exploiting the eligibility traces based on Peng’s Q\(λ\) the granularity of acceleration and deceleration values are

\[39\]. Authors in research \[21\] state that the training process set to \[0.3, 2.5, 3.5\] m/s2, and \[−0.3, −2.5, −3.5\] m/s2, of QMIX may show stability with faster convergence aided respectively. Regarding the training processes for various by this technique. This trick can also prevent the Q networks algorithms, they are run under three random seeds to erad-trained insufficiently from bringing substantial bias against icate the effect of randomness, and the metrics including the bootstrap returns. Peng’s Q\(λ\) can be formulated as: change of episodic return, episode length, and success rates are engaged to evaluate their performances. The collection

∞

of these metrics is guided by the following procedure: the X

Gλ ˙

=\(1 − λ\)

λn−1G

l

l:l\+n

pause happens every 2000 timesteps during the training, and n=1

then five individual episodes are run to evaluate the model l\+n

at that moment, with each agent selecting action according X

Gl:l\+n ˙

=

γ t−lrt \+ γn\+1 max Qtot\(τ, a, st; θtot\)

\(12\)

to the greedy decentralized policy. Further, each algorithm’s a

t =l

trained models with the maximum episodic return are stored. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:38:48 UTC from IEEE Xplore. Restrictions apply. 

GUO et al.: HEURISTIC-BASED MDRL APPROACH FOR COORDINATING CAVs 16243

TABLE II

scenario with 600ms communication time delay in a zero-shot HYPERPARAMETERS OF ALGORITHMS

manner, in which each model accomplishing the coordination task being tested for 100 episodes. It should be pointed out that setting the V2V time delay to a maximum of 600ms is inspired by the survey about V2V communication \[43\], 

where the authors claim that the worst-case time delay for applications based on V2V communication will not be more significant than 500ms. 

2\) Case Study 2 \(CAVs Possessing Random Routes in Mixed Traffic Scenario\): Generalizability is another significant metric for evaluating the MDRL algorithm’s performance. Hence, we proceed with the scenario where all CAVs can select random routes in their resided lane, as shown in Fig. 1b. 

The available routes include \{\(NS, NW\), \(NE, NS\)\}, \{\(SN, SE\), \(SW, SN\)\}, \{\(WE, WS\), \(WN, WE\)\}, \{\(EW, EN\), \(ES, EW\)\}. One CAV from a specific direction can choose its route following the probability vector defined by \[ p1, p2\], where p1, p2 denote the probabilities of choosing the main route and the secondary route, respectively, and are set to \[0.7, 0.3\] in this experiment. In the training process run under three random seeds, the same metrics as case 1 are employed to evaluate the training performances of various candidate algorithms. The same applies to the communication conditions. 

B. Case Study 1: Training Performance & Model Evaluation 1\) Training Performance: The changes of episodic return, episode length, and success rate over training timesteps are collected as shown in three sub-figures in Fig.3, used to assess the training performance of three candidate algorithms \(H-QMIX, QMIX, IPPO\). The shaded area implies the variance, and the solid line implies the average value. As Fig.3a

illustrates, H-QMIX can converge to the highest value with relatively low variance in comparison with the others but carry two evident ditches along the process owing to the active explorations of multiple agents. Eventually, H-QMIX

The hyperparameters of the H-QMIX and IPPO algorithm are completes the coordination task since its success rate stays jointly summarized in Table.II. Besides, implementing V2V

at 1.0, which can be seen from Fig.3c. Besides, from these communication delay relies on the open-source cooperative two figures, the learning process of IPPO is most unstable, driving framework, OpenCDA \[41\]. All experiments were deduced from its tremendous variance, and cannot learn the conducted on a single PC with 3.7GHz Intel\(R\) Core\(TM\) coordination policy at the end of the training. Unfortunately, i7-8700K CPU and NVIDIA GeForce RTX 2080 GPU. The although the QMIX method converges with minimal variance, following two paragraphs elaborate on the settings of these its mean value is still below the zero baseline, indicating that two case studies. 

CAVs fail to complete the coordination task, which can also 1\) Case Study 1 \(CAVs Possessing Stationary Routes in be verified by the corresponding success rate change in Fig.3c. 

Mixed Traffic Scenario\): The routes of all CAVs in case Regarding the episode length, it may be counter-intuitive study 1 are established as stationary, as shown in Fig. 1a, 

at first glance that H-QMIX acquiring the best asymptotic which includes \(NS, NE\), \(SN, SW\), \(WE, WN\), \(EW, ES\) performance demonstrates the most extended episode length. 

for the north\(N\), south\(S\), west\(W\) and east\(E\) directions, However, the reason is that one single episode is automatically respectively. The vehicles with orange color represent the terminated if any collisions occur, as introduced in Section IV, 

MDRL-controlled CAVs, and the grey vehicles characterize and it proves again that the training processes of IPPO and the HDVs. The comparative study for case 1 involves three QMIX are inferior. Their policies struggle to finish the task. 

candidate algorithms, H-QMIX, QMIX, and IPPO. To the best 2\) Model Evaluation Under the Perfect and Latent Commu-of our knowledge, PPO and its distributed version, IPPO, nication: First, models trained by three competitor algorithms are the most common \(M\)DRL algorithms applied to an with the maximal episodic return are evaluated under the isolated signal-free junction \[10\], \[12\], \[13\], \[42\]. We assume perfect V2V communication \(or with 0ms communication that the V2V communication between each CAV is perfect delay\). Since QMIX converges to 0 success rate, we only during training, which is not practical in a real-world scenario. 

present sets of snapshots generated from H-QMIX, IPPO

Therefore, these trained models are then transferred to the to intuitively demonstrate the emergent behaviors of various Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:38:48 UTC from IEEE Xplore. Restrictions apply. 





16244

IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 25, NO. 11, NOVEMBER 2024

Fig. 3. 

This figure demonstrates the training process of three candidate algorithms \(H-QMIX, the original QMIX, and IPPO\) under case 1 in which all CAVs possess stationary routes in mixed traffic with a density of 300veh/hour/lane, which includes \(a\) the change of episode return, and \(b\) the change of episode length, \(c\) the variation of success rate. The experiments are conducted with three random seeds to eradicate the randomness where the shaded areas and the solid lines denote the variance and average value, respectively. 

Fig. 4. 

The figure contains \(a\) a set of snapshots at various typical moments generated from the trained H-QMIX policy, where the CAVs are colored in red and HDVs colored in yellow. Besides, the two tiny circles at the end of the vehicle icon denote the deceleration behavior, and two tiny circles at the lateral represent the turning behavior. \(b\) speed profiles, \(c\) acceleration profiles, \(d\) traveled distance, and \(e\) fuel consumption for each CAV produced from a successful episode under the conditions of case 1. 

policies and provide the speed, acceleration, traveled distance, The behaviors of each pair of CAVs are nearly symmetric. 

and fuel consumption profiles for the model accomplishing Moreover, it should be noted that V1, V3 decelerate from a the task, as shown in Fig.4-Fig. 5. It can be found out that higher speed in comparison with the previous pair of CAVs the passing order obeys strictly the order predefined in the list V0V2, which may lead to more fuel consumption as shown in H of the heuristic-based action mask module, from the speed

Fig.4e. 

and traveled distance profiles of these figures \(Fig.4b, Fig.5b, 

Concerning evaluating the trained IPPO model, one can

Fig.4d, Fig.5d\). 

observe that more deceleration behaviors emerge in the accel-Specifically, the snapshots in Fig.4a witness the quali-eration profiles \(Fig.5c\). However, more CAVs can reach the tative performance of the trained H-QMIX model, where speed limit \(Fig.5b\), and the CAVs’ behaviors in one pair V5, V7 directly accelerate to exit the junction before 9.4s, and become gradually asymmetric. From the snapshots in Fig.5a, 

then V4, V6 prepare to drive out of the zone with medium speed and acceleration profiles, CAV V4 always drives faster deceleration to yield to the HDVs deciding to drive through. 

than v6, which is slightly different compared to their peers Afterward, V0, V2 takes the passing priority to pass the inter-from the H-QMIX model. The behaviors of the subsequent section with instant conservative deceleration near the moment pair of CAVs are similar to that in the H-QMIX case. However, of 12.2s to react with incoming HDVs turning left. Then they CAVs with IPPO policy consume more fuel due to more speed up to the maximal speed limit. The last pair of CAVs, frequent speed changes. Collectively, it could be concluded V1, V3, also decelerate according to the surrounding HDVs’

that the IPPO policy demonstrates more aggressiveness than behavior and leave the intersection at the maximum speed. 

the H-QMIX model. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:38:48 UTC from IEEE Xplore. Restrictions apply. 





GUO et al.: HEURISTIC-BASED MDRL APPROACH FOR COORDINATING CAVs 16245

Fig. 5. 

The figure contains \(a\) a set of snapshots at various typical moments generated from the trained IPPO policy, \(b\) speed profiles, \(c\) acceleration profiles, \(d\) traveled distance, and \(e\) fuel consumption for each CAV produced from a successful episode under the conditions of case 1. 

Fig. 6. 

This figure demonstrates the training process of two candidate algorithm \(H-QMIX and IPPO\) under case 2 in which all CAVs possess random routes in mixed traffic with a density of 300veh/hour/lane, which includes \(a\) the change of episode return, and \(b\) the change of episode length, \(c\) the variation in success rate. The experiments are conducted under three random seeds to eradicate the randomness where the shaded areas and the solid lines denote the variance and average value, respectively. 

TABLE III

AVERAGE SUCCESS RATE OF DIFFERENT ALGORITHMS UNDER DIFFERENT SCENARIOS

Second, models accomplishing the task under the station-C. Case Study 2: Training Performance & Model Evaluation ary route scenario with perfect communication conditions 1\) Training Performance: In this paragraph, H-QMIX and are transferred in a zero-shot manner to the scenario with IPPO are selected as the foundation of the comparative study communication latency holding a 600ms time delay. In order to since QMIX cannot even obtain reliable results for more reduce space, the snapshots and profiles will not be exhibited. 

straightforward stationary route scenarios, as shown in case Only the necessary experimental results, including the average study 1. The training performances of these two candidates are success rate and traveled time of the entire episode, will be assessed as usual via the changes of episodic return, episode displayed in Table.III and Table.IV. It shows that the success length, and success rate over timesteps, as illustrated in three rate using both candidates\(H-QMIX, IPPO\) stays unchanged sub-figures in Fig.6. The learning process of IPPO becomes at 100% for all 100 testing episodes. Noticeably, it implies that unstable compared to the results in case study 1. Although its those two MDRL models are robust to specific communication episodic return appears to converge in Fig.6a, the divergence latency. 

shown in Fig.6c verifies this phenomenon where the success Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:38:48 UTC from IEEE Xplore. Restrictions apply. 





16246

IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 25, NO. 11, NOVEMBER 2024

Fig. 7. 

The figure contains \(a\) a set of snapshots at various typical moments generated from the trained H-QMIX policy, \(b\) speed profiles, \(c\) acceleration profiles, \(d\) traveled distance, and \(e\) fuel consumption for each CAV produced from a successful episode under the conditions of case 2. 

TABLE IV

AVERAGE TRAVELLED TIME OF DIFFERENT ALGORITHMS UNDER DIFFERENT SCENARIOS

rate of IPPO keeps oscillating, and the same applies to the straight. V2, V0 demonstrate nearly symmetric behavior with outcome of episode length. On the contrary, it can be seen V2 turning right and V0 driving through, and both decelerate that H-QMIX can still converge to the highest value with to keep a certain distance from the neighbor HDVs. Since relatively low variance compared with the IPPO but carry more V1 chooses to go straight, it is encouraged to behave similarly fluctuations. One interpretation is that when the agents interact to V0, V2 determined by the passing order, and V3 is the with the environment and decide to explore heavily, they last one to drive into the junction, yielding to the HDV

may be punished dramatically due to their mistaken decision going straight. V3 consumes the most fuel \(Fig.7e\) poten-sequences of accelerations or decelerations. Eventually, the tially because of decelerating from a higher speed. On the success rate of H-QMIX converges to 1.0, as shown in Fig.6c, 

contrary, the trained IPPO model cannot fulfill the task and it can be concluded that H-QMIX acquires the best for case 2. 

training efficacy and stability compared to the IPPO in the Second, models trained by H-QMIX and IPPO algorithms random route scenario. 

under the random route scenario with perfect communication 2\) Model Evaluation Under the Perfect and Latent Commu-condition is transferred in a zero-shot manner to the scenario nication: Following the experimental results in case study 1, with 600ms V2V time delay. The corresponding experimental the models trained by H-QMIX and IPPO with the maximal results are also shown in the last two columns in Table.III

episodic return are first evaluated under perfect communication and Table.IV, including the average success rate and traveled and then transferred to latent communication scenario. From time of the entire episode. It can be seen that IPPO can still snapshots in Fig.7 and speed profiles in Fig.7b, one can find achieve a 34% success rate. However, this value diminishes out that the passing order of CAVs keeps the same except to 29% when we transfer this policy to an unseen scenario. 

that several CAVs select their secondary routes. However, the Nonetheless, the average traveled time of the IPPO policy speed patterns for CAVs do not comply with the symmetry \(only collected successful episodes\) is shorter than that of the that occurred in case 1. For example, at 7.8s, V7 chooses to H-QMIX policy, implying that the IPPO policy may introduce turn right at a higher speed before entering the intersection, some degree of aggressiveness, which is consistent with the and V5 remains going straight, whose speed surpasses V7’s analysis in the previous case. It is worth noting that H-QMIX

speed at the intersection. The next pair of CAVs V4, V6 pick can still obtain a 100% success rate when communication the same route as usual, but the speed of V6 is initially latency is considered. Consequently, the H-QMIX model is greater than V5 and decelerates to yield the HDVs going robust to specific communication latency. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:38:48 UTC from IEEE Xplore. Restrictions apply. 

GUO et al.: HEURISTIC-BASED MDRL APPROACH FOR COORDINATING CAVs 16247

VII. CONCLUSION AND FUTURE WORKS

\[14\] M. Yuan, J. Shan, and K. Mi, “Deep reinforcement learning based This study proposes the H-QMIX approach to coordi-game-theoretic decision-making for autonomous vehicles,” IEEE Robot. 

Autom. Lett., vol. 7, no. 2, pp. 818–825, Apr. 2022. 

nate several CAVs at an isolated non-signalized intersection

\[15\] P. Hernandez-Leal, B. Kartal, and M. E. Taylor, “A survey and critique in mixed-autonomy traffic with perfect and latent commu-of multiagent deep reinforcement learning,” Auton. Agents Multiagent nication, where the heuristic in the H-QMIX approach is Syst., vol. 33, no. 6, pp. 750–797, 2019. 

implemented by improving the action mask module to enforce

\[16\] Z. Guo, Y. Wu, L. Wang, and J. Zhang, “Coordination for connected and automated vehicles at non-signalized intersections: A value passing order and safety constraint. From the simulation decomposition-based multiagent deep reinforcement learning approach,” 

results, H-QMIX can converge faster and and perform asymp-IEEE Trans. Veh. Technol., vol. 72, no. 3, pp. 3025–3034, Mar. 2023. 

totically better than the IPPO and QMIX for each case study. 

\[17\] T. Rashid, M. Samvelyan, C. Schroeder, G. Farquhar, J. Foerster, and S. Whiteson, “Monotonic value function factorisation for deep multi-Additionally, the coordination task is well aided by H-QMIX

agent reinforcement learning,” in Proc. Int. Conf. Mach. Learn., 2020, policy regarding the relevant snapshots, speed, acceleration, pp. 4295–4304. 

and fuel consumption profiles, even when CAVs possess ran-

\[18\] P. Sunehag et al., “Value-decomposition networks for cooperative multiagent learning based on team reward,” in Proc. AAMAS, 2018, pp. 1–17. 

dom routes under a certain amount of communication latency. 

\[19\] K. Son, D. Kim, W. J. Kang, D. E. Hostallero, and Y. Yi, “QTRAN: Collectively, it may imply that the H-QMIX policy gains Learning to factorize with transformation for cooperative multi-agent reliable results and is robust to unavoidable communicative reinforcement learning,” in Proc. ICML, 2019, pp. 5887–5896. 

time delays. 

\[20\] Y. Yang, Y. Wen, and J. Wang, “Multi-agent determinantal Q-learning,” 

in Proc. 37th Int. Conf. Mach. Learn. \(ICML\), 2020, pp. 10757–10766. 

In the future, we will evaluate further the performance of

\[21\] J. Hu, S. Jiang, S. A. Harding, H. Wu, and S.-W. Liao, “Rethinking the H-QMIX algorithm applied to more realistic scenarios the implementation tricks and monotonicity constraint in cooperative using a physically rendered simulator \(e.g., CARLA\) with multi-agent reinforcement learning,” 2021, arXiv:2102.03479. 

more random interactions between CAVs and HDVs. At that

\[22\] M. Samvelyan et al., “The StarCraft multi-agent challenge,” 2019, arXiv:1902.04043. 

moment, the H-QMIX algorithm may be improved based on

\[23\] R. Lowe, Y. I. Wu, A. Tamar, J. Harb, O. P. Abbeel, and I. Mordatch, game theory and offline RL. 

“Multi-agent actor-critic for mixed cooperative-competitive environments,” in Proc. NIPS, 2017, pp. 6379–6390. 

REFERENCES

\[24\] S. Li, Y. Wu, X. Cui, H. Dong, F. Fang, and S. Russell, “Robust multiagent reinforcement learning via minimax deep deterministic policy

\[1\] Z. Wang, Y. Bian, S. E. Shladover, G. Wu, S. E. Li, and M. J. Barth, gradient,” in Proc. AAAI Conf. Artif. Intell., 2019, vol. 33, no. 1, 

“A survey on cooperative longitudinal motion control of multiple con-pp. 4213–4220. 

nected and automated vehicles,” IEEE Intell. Transp. Syst. Mag., vol. 12, 

\[25\] S. K. S. Nakka, B. Chalaki, and A. A. Malikopoulos, “A multi-agent no. 1, pp. 4–24, Spring. 2020. 

deep reinforcement learning coordination framework for connected and

\[2\] W. Liu et al., “A systematic survey of control techniques and applications automated vehicles at merging roadways,” in Proc. Amer. Control Conf. 

in connected and automated vehicles,” 2023, arXiv:2303.05665. 

\(ACC\), Jun. 2022, pp. 3297–3302. 

\[3\] Z. Meng, X. Xia, R. Xu, W. Liu, and J. Ma, “HYDRO-3D: Hybrid object

\[26\] Y. Wu, H. Chen, and F. Zhu, “DCL-AIM: Decentralized coordina-detection and tracking for cooperative perception using 3D LiDAR,” 

tion learning of autonomous intersection management for connected IEEE Trans. Intell. Veh., vol. 8, no. 8, pp. 4069–4080, Aug. 2023, doi: and automated vehicles,” Transp. Res. C, Emerg. Technol., vol. 103, 

10.1109/TIV.2023.3282567. 

pp. 246–260, Jun. 2019. 

\[4\] K. Dresner and P. Stone, “A multiagent approach to autonomous intersection management,” J. Artif. Intell. Res., vol. 31, pp. 591–656, 

\[27\] Z. Peng, Q. Li, K. M. Hui, C. Liu, and B. Zhou, “Learning to simulate Mar. 2008. 

self-driven particles system with coordinated policy optimization,” in

\[5\] J. Ding, H. Xu, J. Hu, and Y. Zhang, “Centralized cooperative inter-Proc. Adv. Neural Inf. Process. Syst., vol. 34, 2021, pp. 10784–10797. 

section control under automated vehicle environment,” in Proc. IEEE

\[28\] F. L. D. Silva and A. H. R. Costa, “A survey on transfer learning for Intell. Vehicles Symp. \(IV\), Jun. 2017, pp. 972–977. 

multiagent reinforcement learning systems,” J. Artif. Intell. Res., vol. 64, 

\[6\] I. H. Zohdy and H. A. Rakha, “Intersection management via vehicle pp. 645–703, Mar. 2019. 

connectivity: The intersection cooperative adaptive cruise control system

\[29\] P. Cai, H. Wang, Y. Sun, and M. Liu, “DQ-GAT: Towards safe and concept,” J. Intell. Transp. Syst., vol. 20, no. 1, pp. 1–16, 2014. 

efficient autonomous driving with deep Q-learning and graph atten-

\[7\] N. Li, Y. Yao, I. Kolmanovsky, E. Atkins, and A. R. Girard, tion networks,” IEEE Trans. Intell. Transp. Syst., vol. 23, no. 11, 

“Game-theoretic modeling of multi-vehicle interactions at uncontrolled pp. 21102–21112, Nov. 2022. 

intersections,” IEEE Trans. Intell. Transp. Syst., vol. 23, no. 2, 

\[30\] E. Candela, L. Parada, L. Marques, T. Georgescu, Y. Demiris, and pp. 1428–1442, Feb. 2022. 

P. Angeloudis, “Transferring multi-agent reinforcement learning policies

\[8\] R. Chandra and D. Manocha, “GamePlan: Game-theoretic multi-agent for autonomous driving using sim-to-real,” in Proc. IEEE/RSJ Int. Conf. 

planning with human drivers at intersections, roundabouts, and merging,” 

Intell. Robots Syst. \(IROS\), Oct. 2022, pp. 8814–8820. 

IEEE Robot. Autom. Lett., vol. 7, no. 2, pp. 2676–2683, Apr. 2022. 

\[31\] T. Zhou, L. Wang, R. Chen, W. Wang, and Y. Liu, “Accelerating

\[9\] D. Isele, R. Rahimi, A. Cosgun, K. Subramanian, and K. Fujimura, reinforcement learning for autonomous driving using task-agnostic and

“Navigating occluded intersections with autonomous vehicles using deep ego-centric motion skills,” 2022, arXiv:2209.12072. 

reinforcement learning,” in Proc. IEEE Int. Conf. Robot. Autom. \(ICRA\), 

\[32\] F. A. Oliehoek and C. Amato, A Concise Introduction to Decentralized May 2018, pp. 2034–2039. 

Pomdps. Berlin, Germany: Springer, 2016. 

\[10\] Y. Guan, Y. Ren, S. E. Li, Q. Sun, L. Luo, and K. Li, “Centralized

\[33\] C. 

Amato, 

G. 

Chowdhary, 

A. 

Geramifard, 

N. 

K. 

Üre, 

and

cooperation for connected and automated vehicles at intersections by M. J. Kochenderfer, “Decentralized control of partially observable proximal policy optimization,” IEEE Trans. Veh. Technol., vol. 69, Markov decision processes,” in Proc. 52nd IEEE Conf. Decis. Control, no. 11, pp. 12597–12608, Nov. 2020. 

Dec. 2013, pp. 2398–2405. 

\[11\] H. Shu, T. Liu, X. Mu, and D. Cao, “Driving tasks transfer using deep

\[34\] V. Mnih, “Human-level control through deep reinforcement learning,” 

reinforcement learning for decision-making of autonomous vehicles in Nature, vol. 518, pp. 529–533, Feb. 2015. 

unsignalized intersection,” IEEE Trans. Veh. Technol., vol. 71, no. 1, 

\[35\] M. Tan, “Multi-agent reinforcement learning: Independent vs. coopera-pp. 41–52, Jan. 2022. 

tive agents,” in Proc. 10th Int. Conf. Mach. Learn., 1993, pp. 330–337. 

\[12\] E. Vinitsky et al., “Benchmarks for reinforcement learning in mixed-

\[36\] A. Tampuu et al., “Multiagent cooperation and competition with autonomy traffic,” in Proc. 2nd Conf. Robot Learn., Oct. 2018, deep reinforcement learning,” PLoS ONE, vol. 12, no. 4, 2017, pp. 399–409. 

Art. no. e0172395. 

\[13\] B. Peng, M. F. Keskin, B. Kulcsár, and H. Wymeersch, “Connected

\[37\] M. Treiber, A. Hennecke, and D. Helbing, “Congested traffic states in autonomous vehicles for improving mixed traffic efficiency in unsignal-empirical observations and microscopic simulations,” Phys. Rev. E, Stat. 

ized intersections with deep reinforcement learning,” Commun. Transp. 

Phys. Plasmas Fluids Relat. Interdiscip. Top., vol. 62, no. 2, p. 1805, Res., vol. 1, no. 1, 2021, Art. no. 100017. 

## 2000. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:38:48 UTC from IEEE Xplore. Restrictions apply. 





16248

IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 25, NO. 11, NOVEMBER 2024

\[38\] V. Nair and G. E. Hinton, “Rectified linear units improve restricted Lifang Wang \(Member, IEEE\) received the Ph.D. 

Boltzmann machines,” in Proc. 27th Int. Conf. Mach. Learn., 2010, degree in automobile engineering from Jilin Uni-pp. 807–814. 

versity, Jilin, China, in 1997. Then, she joined

\[39\] J. Peng and R. J. Williams, Incremental Multi-Step Q-Learning. Ams-the Institute of Electrical Engineering, Chinese terdam, The Netherlands: Elsevier, 1994, pp. 226–232. 

Academy of Sciences, Beijing, China. During the

\[40\] D. P. Kingma and J. Ba, “Adam: A method for stochastic optimization,” 

Chinese tenth five-year plan \(2001–2005\), she was in Proc. ICLR, 2015, pp. 1051–1060. 

a member of the National Specialist Group of

\[41\] R. Xu, Y. Guo, X. Han, X. Xia, H. Xiang, and J. Ma, “OpenCDA: the Key Special Electric Vehicle Project of the An open cooperative driving automation framework integrated with National 863 Program and the Head of the 863 Spe-co-simulation,” in Proc. IEEE Int. Intell. Transp. Syst. Conf. \(ITSC\), cial EV Project Office. She is currently the Director Sep. 2021, pp. 1155–1162. 

of the Department of Vehicle Energy System and

\[42\] D. Q. Tran and S.-H. Bae, “Proximal policy optimization through a deep Control Technology, Institute of Electrical Engineering, Chinese Academy reinforcement learning framework for multiple autonomous vehicles at of Sciences. She is also the Vice Director of the Key Laboratory of Power a non-signalized intersection,” Appl. Sci., vol. 10, no. 16, p. 5722, 2020. 

Electronics and Electric Drives, Chinese Academy of Sciences. Her research interests include electric vehicle control systems, EV battery management

\[43\] S. Zeadally, J. Guerrero, and J. Contreras, “A tutorial survey on systems, wireless charging systems for EVs, electromagnetic compatibility, vehicle-to-vehicle communications,” Telecommun. Syst., vol. 73, no. 3, and smart electricity use. She has directed more than 15 projects in these pp. 469–489, Mar. 2020. 

fields and published over 60 articles and 30 patents. 

Zihan Guo received the B.Eng. degree from

Glasgow College, University of Electronic Science and Technology \(UESTC\), Chengdu, China, and the B.Eng. degree \(Hons.\) in electronics and electrical engineering from the University of Glasgow, in 2019. He is currently pursuing the Ph.D. degree with the Institute of Electrical Engineering, Chinese Academy of Sciences. His research interests include the applications of multi-agent reinforcement learning, game theory-based decision-making, and motion planning for autonomous driving. 

Junzhi Zhang \(Member, IEEE\) received the Ph.D. 

degree in automobile engineering from Jilin University, Jilin, China, in 1997. Since 1998, he has been with the Department of Automotive Engi-Yan Wu received the Ph.D. degree in power elec-neering, Tsinghua University, Beijing, China. His tronics and electric drives from the Institute of research interests include braking energy feedback Electrical Engineering, Chinese Academy of Sci-and dynamic control of the electric vehicle, energy ences, Beijing, China, in 2019. She is currently an management and control of hybrid electric vehicles, Associate Professor with the Department of Vehicle matching the design of the hybrid electric vehicle, Energy System and Control Technology, Institute and the design and control of the hybrid trans-of Electrical Engineering, Chinese Academy of Sci-mission. He is the Chairperson of the International ences. Her research interests include vehicle network Electric Vehicle Conference Committee, the Expert of the National Energy information security, X-by-wire systems, vehicle Conservation and New Energy Vehicle 863 Project Planning Group, and the motion control, and intelligent vehicle technology. 

Director of the Electric Vehicle Industry Technology Innovation Alliance. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:38:48 UTC from IEEE Xplore. Restrictions apply.



