1

Cooperative Decision-Making for CAVs at Unsignalized Intersections: A MARL Approach with Attention and Hierarchical Game Priors Jiaqi Liu, Student Member, IEEE, Peng Hang, Member, IEEE, Xiaoxiang Na, Chao Huang, Senior Member, IEEE, and Jian Sun Abstract—The development of autonomous vehicles has shown human drivers \[3\]. Game-based and optimization-based ap-great potential to enhance the efficiency and safety of trans-proaches have been proposed to address this issue \[4\]–\[6\]. 

portation systems. However, the decision-making issue in complex However, these methods prove impractical when handling human-machine mixed traffic scenarios, such as unsignalized scenarios involving multiple agents and complex interaction intersections, remains a challenge for autonomous vehicles. 

While reinforcement learning \(RL\) has been used to solve behaviors \[6\]. Reinforcement learning \(RL\) holds the potential complex decision-making problems, existing RL methods still to overcome these limitations, leveraging data-driven methods have limitations in dealing with cooperative decision-making with its robust learning and efficient reasoning capabilities \[7\]–

of multiple connected autonomous vehicles \(CAVs\), ensuring

\[9\]. 

safety during exploration, and simulating realistic human driver Current

RL

approaches

for

unsignalized

intersection

behaviors. In this paper, a novel and efficient algorithm, Multi-Agent Game-prior Attention Deep Deterministic Policy Gradient decision-making

problems

encounter

several

challenges. 

\(MA-GA-DDPG\), is proposed to address these limitations. Our Firstly, most studies consider a single AV at the intersec-proposed algorithm formulates the decision-making problem of tion, modeling the problem as a single-agent RL problem, CAVs at unsignalized intersections as a decentralized multi-agent whereas cooperative decision-making of multiple connected reinforcement learning problem and incorporates an attention autonomous vehicles \(CAVs\) is a more challenging and less mechanism to capture interaction dependencies between ego CAV

and other agents. The attention weights between the ego vehicle explored problem. Besides, common RL methods rely on and other agents are then used to screen interaction objects exploration to teach CAVs how to decide and act, which and obtain prior hierarchical game relations, based on which may compromise the learning efficiency and policy safety \[1\]. 

a safety inspector module is designed to improve the traffic Safety is the most critical factor when designing the decision-safety. Furthermore, both simulation and hardware-in-the-loop making algorithm. Moreover, the simulation environments’

experiments were conducted, demonstrating that our method outperforms other baseline approaches in terms of driving safety, simplification of human drivers’ behaviors may lead to per-efficiency, and comfort. 

formance gaps between simulation and real-world scenarios. 

Index Terms—Multi-agent reinforcement learning, connected To cope with these challenges, we propose a novel and autonomous vehicles, decision-making, attention mechanism, efficient algorithm, Multi-Agent Game-prior Attention Deep unsignalized intersections

Deterministic Policy Gradient \(MA-GA-DDPG\), which formulates the decision-making problem of CAVs at unsignalized, I. INTRODUCTION

human-machine mixed intersections as a decentralized multi-AUTONOMOUS vehicles \(AVs\) have undergone remark- agent RL problem. In MA-GA-DDPG, each CAV at the able advances in recent years, holding great poten-intersection is modeled as an agent, enabling it to explore the arXiv:2409.05712v1 \[cs.RO\] 9 Sep 2024 tial for enhancing transportation efficiency and safety \[1\], environment, communicate, and cooperate with other agents. 

\[2\]. Nonetheless, decision-making in complex human-machine We use Multi-Agent Deep Deterministic Policy Gradient mixed traffic scenarios, particularly at unsignalized intersec-

\(MADDPG\) as the baseline algorithm, where all agents adopt tions, remains a considerable challenge for both AVs and a strategy of centralized training and distributed execution \(CTDE\). To capture the interaction dependencies between the This work was supported in part by the National Key R&D Program ego CAV and other agents, we incorporate an attention mech-of China \(2023YFB4301900\), the Shanghai Scientific Innovation Foundation \(No.23DZ1203400\), the National Natural Science Foundation of China anism \[10\]. The attention weights between the ego vehicle and \(52302502\), the State Key Laboratory of Intelligent Green Vehicle and other agents are used to screen interaction objects and obtain Mobility under Project No. KFZ2408, and the Fundamental Research Funds prior hierarchical game relations. We then develop a safety for the Central Universities. 

Jiaqi Liu, Peng Hang, and Jian Sun are with the College of Transportation inspector module to predict and detect potential conflicts with and Key Laboratory of Road and Traffic Engineering, Ministry of Education, other agents during CAV exploration and make corrections Tongji University, Shanghai 201804, China. \(e-mail: \{liujiaqi13, hangpeng, in real-time to improve the algorithm’s learning efficiency. 

sunjian\}@tongji.edu.cn\)

Xiaoxiang Na is with the Department of Engineering, University of Cam-We also take into account the heterogeneity of human drivers bridge, Cambridge CB2 1PZ, United Kingdom \(e-mail: xnhn2@cam.ac.uk \) in traffic environments and carry out extensive experiments Chao Huang is with Department of Industrial and System Engineering, using both simulation and hardware-in-loop setups, during The Hong Kong Polytechnical University, Hong Kong 999077. \(e-mail: hchao.huang@polyu.edu.hk\)

which domain controllers are utilized for decision-making and Corresponding author: Peng Hang

planning. The results demonstrate that our approach excels in

2

terms of learning efficiency, driving safety, as well as overall be solved accurately, with good interpretability and con-efficiency and comfort. 

trollability, but the solution efficiency of too large-scale The contributions of this paper are summarized as follows: problems often cannot meet the requirements of real-time applications \[18\]. 

• A novel and efficient algorithm MA-GA-DDPG is proposed to realize cooperative decision-making of CAVs

• Learning-based models, encompassing Neural Networks in complex human-machine mixed traffic scenarios. The \(NN\) \[20\] and Reinforcement Learning \(RL\) \[8\], \[21\], 

heterogeneity of drivers is considered to simulate the real

\[22\], effectively capture interaction dynamics with potent traffic environment and train the algorithm. 

learning and efficient reasoning capabilities \[23\], \[24\]. 

However, addressing challenges related to interpretability, 

• The multi-head attention mechanism is leveraged to capture the complex interactions among CAVs and other convergence, and generalization remains essential \[25\]. 

vehicles in the mixed driving environment. An interaction object filter based on the attention weights is designed to B. Multi-Agent Reinforcement Learning and Attention Mech-facilitate the identification of the most relevant agents for anism

interaction. 

Multi-Agent Reinforcement Learning \(MARL\) is an emerg-

• A hierarchical game framework is utilized to incorporate ing research field that focuses on the optimization problem the traffic priority priors into the interaction process. This of multiple autonomous intelligent agents making sequential framework enables the modeling of the priority informa-decisions in an environment. In recent years, MARL has been tion and its subsequent transmission to the safety inspec-utilized to solve plenty of multi-agent problems, such as traffic tor module, which effectively supervises and adjusts the control \[26\], decision-making of autonomous driving \[23\], 

actions of CAVs to minimize the risk of collisions. 

\[24\], \[27\], games \[28\], etc. 

The rest of the paper is organized as follows: Section II

Some works have modeled the traffic system with multi-summarizes the recent related works. The decision-making vehicle scenarios by MARL, which has shown exciting and problem at the intersection is formulated in section III. In outstanding performance in lane changing \[23\], \[29\], merging section IV, the MA-GA-DDPG model is described. In section

\[24\], intersection \[22\] scenarios. Nevertheless, these algo-

V, the simulation environment and comprehensive experiments rithms still fail to guarantee enough security and reliability, are introduced and the results are analyzed. Finally, this paper which greatly limits further application. To address these is concluded in section VI. 

challenges, recent studies have proposed various approaches. 

For example, some works have incorporated interaction priors in the MARL framework \[24\]. Nevertheless, further research II. RELATED WORKS

is needed to improve the safety and reliability of MARL

A. Decision-Making of CAVs at Intersections algorithms. 

Navigating complex, high-density mixed driving conditions Attention mechanism is a cognitive function that is crucial presents a formidable challenge for CAVs, with intersections for humans. Recently, this mechanism has been introduced ranking among the most intricate and demanding scenarios to many fields, including image caption generation, text clas-for interaction in autonomous driving \[11\], \[12\]. Developing sification, autonomous driving, and recommendation systems an efficient cooperative decision-making algorithm tailored to

\[30\]. It is a newly-emerged technique in neural network intersection scenarios holds paramount importance in enhanc-models and has shown great power in sequence modeling \[10\]. 

ing intersection traffic’s efficiency and safety \[13\]. 

The attention mechanism enables neural networks to identify Current research in decision-making models for autonomous correlations and inter-dependencies among variable inputs. It driving at unsignalized intersections encompasses several ap-has been applied in the tasks of autonomous driving’s decision-proaches:

making, such as capturing vehicle-to-ego dependencies \[11\], 

\[31\], optimizing interactive behavior strategies \[22\], and en-

• Game-theoretical models, such as Level-k games \[4\], 

hancing the safety of the decision-making algorithm \[23\], \[32\]. 

follower-leader games \[14\], etc. These studies treat each Meanwhile, the attention mechanism faces several challenges, CAV as a rational decision-maker and simulate the reac-including a substantial data requirement \[33\], lengthy training tions and actions of human drivers under rational condi-times \[30\], and other issues. Furthermore, the interpretability tions \[15\]. However, this purely rational situation cannot of the attention mechanism remains to be further explored and fully simulate the real world. Moreover, the efficiency of enhanced \[34\]. 

large-scale game calculations and the scalability of game frameworks are also challenging issues. 

C. Summary of Related Works

• Rule-based

methods, 

such

as

first-come-first-serve

\(FCFS\) \[16\], Buffer Coordination \[17\] etc. These The decision-making process for CAVs at intersections methods are easy to implement and logically clear, but is a highly intricate and formidable undertaking. Scholars as the traffic demand increases, the efficiency of these have proposed various approaches, including game-theoretical methods is poor. 

models, learning-based techniques, and optimization-based

• Optimization-based methods, such as convex optimiza-methods, to model decision-making in autonomous driving tion methods \[6\], \[18\], model predictive control\(MPC\) scenarios, particularly at unsignalized intersections. Notably, 

\[19\] etc. The advantage of this method is that it can Multi-Agent Reinforcement Learning \(MARL\) has emerged as

3

a promising approach for addressing multi-vehicle interaction where ∆lat is the lateral position of the vehicle with respect to and decision-making within complex and densely populated the lane center-line, vlat,r is the lateral velocity command, ∆ψr driving environments. However, current MARL algorithms is a heading variation to apply the lateral velocity command, grapple with issues related to non-stationarity, safety, and scal-ψL is the lane heading, ψr is the target heading to follow the ability, thereby curtailing their broader practical application lane heading and position, ˙

ψr is the yaw rate command, δ is

\[35\]. 

the front-wheel angle control, Kp,lat and Kp,ψ are the position Recognizing the potential of the attention mechanism to and heading control gains. 

enhance the safety and reliability of autonomous driving Vehicle motion is determined by a Kinematic Bicycle Model decision-making algorithms, researchers have begun integrat-

\[36\]

ing this mechanism into their frameworks. However, it is cru-

˙

x = v cos\(ψ \+ β\)

cial to acknowledge that existing research on the application

˙

y = v sin\(ψ \+ β\)

of the attention mechanism still presents certain limitations

˙v = a

\[30\]. 

\(3\)

v

In light of the complex cooperative decision-making chal-

˙

ψ =

sin β

lenges faced by CAVs within intricate human-machine mixed l

β = tan−1\(1/2 tan δ\)

traffic scenarios, this study extends the MARL framework by incorporating interaction priors and introducing a safety where \(x, y\) is the vehicle position, v is forward speed, ψ is inspector to address intersection conflicts. Additionally, we heading, a is the acceleration command, β is the slip angle at explore and leverage the attention mechanism to effectively the center of gravity. 

filter interacting objects in these complex environments. 

In this paper, HVs’ longitudinal behavior is controlled by the Intelligent Driver Model\(IDM\) from \[37\]

III. MARL FOR INTERSECTION DECISION-MAKING

" 

v δ

d∗ 2\#

In this section, the decision-making problem of CAVs is

˙v = a 1 −

−

\(4\)

v

d

formulated as a MARL problem firstly. To establish a base-0

line, the MADDPG algorithm for addressing this problem is proposed. 

v∆v

d∗ = d0 \+ T v \+ √

\(5\)

2 ab

A. Scenario Description and Vehicle Movements where v is the vehicle velocity, d is the distance to its front vehicle, v

1\) Scenario

Description:

We consider a cooperative

0 is the desired velocity, T

is the desired

time headway, d

decision-making problem for CAVs in an intersection sce-0 is the jam distance, a, b are the maximum acceleration and deceleration respectively, ∆v is the velocity nario. A single-lane cross-shaped unsignalized intersection is exponent. 

defined, which may be traversed by a variable number of HVs’ lateral behavior is modeled by the Minimizing Overall human-driven vehicles \(HVs\) arriving from disparate direc-Braking Induced by Lane change\(MOBIL\) model \[38\]. 

tions and locations, each exhibiting diverse driving styles. 

In this scenario, four CAVs are introduced, each entering the intersection via dedicated entrance roads corresponding B. Problem Formulation

to the four cardinal directions. The objective is for all CAVs to traverse the intersection safely and efficiently, ultimately The cooperative decision-making problem for multi-CAVs reaching their respective destinations. Upon the successful can be formulated as a partially observable Markov de-completion of this objective, the episode concludes. CAVs cision process \(POMDP\) \[39\]. We use the tuple MG =

can share the status information with each other for better \(V, S, \[Oi\], \[Ai\], P, \[ri\]\) to define the POMDP, in which V

cooperative decision-making. 

is a finite set of all controlled agents \(CAVs\) and S denotes 2\) Vehicle Movements: The actions of CAVs in our problem the state space describing all agents. Oi denotes the set of are decided by the MARL algorithm and will be translated to observation spaces for agent i ∈ V, Ai is the set of action low-level steering and acceleration signals through a closed-space, and ri represents the reward of CAV i. P denotes the loop PID controller. The vehicle’s position is controlled by transition distribution. Each agent i at a given time receives an individual observation oi : S → Oi and takes an action vlat,r = −Kp,lat∆lat, 

ai ∈ Ai based on a policy πi : Oi × Ai → \[0, 1\]. 

v



\(1\)

∆ψ

lat,r

Then the agent i transits to a new state s′ with probability r = arcsin

i

v

P\(s′|s, a\) : S × A1 × ... × AN → S and obtains a reward The vehicle’s heading is controlled by

ri : S × Ai → R. Each agent aims to maximize its expected return

ψr = ψL \+ ∆ψr, 

Ri = ΣT γtri\(st, ai\)

\(6\)

˙

t=0

t

ψr = Kp,ψ\(ψr − ψ\), 

\(2\)

1 l



where γ represents the discount factor and T represents the δ = arcsin

˙

ψr

2 v

time horizon. 

4

1\) Observation Space: Due to the limitation of the sensor **Agent 1**

**Agent 2**

**Agent N**

hardware, the CAV can only detect the status information of **Distributed Execution**

𝝅𝝅

**…**

surrounding vehicles within a limited distance L. We denote 𝟏𝟏

𝝅𝝅𝟐𝟐

𝝅𝝅𝑵𝑵

**Actor**

the set of all observable vehicles within the perception range of agent i as Ni. And the observation matrix of agent i, denoted **Experience Replay**

as O

𝒐𝒐𝟏𝟏

𝒂𝒂𝟏𝟏

𝒐𝒐𝟐𝟐

𝒂𝒂𝟐𝟐

𝒐𝒐N

𝒂𝒂𝑵𝑵

i, is a matrix with dimensions of |Ni| × |F |, where |Ni| is **Buffer**

the number of all observable vehicles for agent i, and |F | is to 𝑸𝑸

represent the number of features utilized to portray a vehicle’s 𝟏𝟏

𝑸𝑸𝟐𝟐

𝑸𝑸𝑵𝑵

**Critic**

**…**

state. The feature vector of the vehicle k is expressed by **Mini-Batch Transitions**

F

**Actor**

𝛁𝛁 𝓣𝓣 𝝅𝝅

𝝅𝝅

𝑸𝑸𝝅𝝅 𝒙𝒙, 𝒂𝒂𝒊𝒊 , … , 𝒂𝒂𝒊𝒊

k = \[xk , yk , vx, vy , cos ϕ

𝜽𝜽

𝒊𝒊 = 𝔼𝔼𝒙𝒙,𝑎𝑎~𝒟𝒟 𝛁𝛁𝜽𝜽 𝒊𝒊 𝒂𝒂𝒊𝒊|𝒐𝒐𝒊𝒊 𝛁𝛁𝒂𝒂

k

𝒊𝒊

𝟏𝟏

𝑵𝑵

k

k , sin ϕk \]

\(7\)

𝒌𝒌

𝒊𝒊

𝒊𝒊

**Update**

where x

𝝅𝝅

𝒊𝒊

𝒊𝒊

𝟐𝟐

k , yk , vx, vy are the longitudinal position, lateral po-Critic

𝑳𝑳 𝜽𝜽

𝒙𝒙, 𝒂𝒂 , … , 𝒂𝒂

k

k

𝒊𝒊 = 𝔼𝔼𝒙𝒙,𝑎𝑎,𝑟𝑟,𝒙𝒙′

𝒚𝒚 − 𝑸𝑸𝒊𝒊

𝟏𝟏

𝑵𝑵

sition, longitudinal speed, and lateral speed, cos ϕk, sin ϕk are the sine and cosine of the vehicle heading angle ϕk, respec-Fig. 1. The framework of the Multi-Agent Deep Deterministic Policy Gradient tively. The whole observation space of the system is the com-

\(MADDPG\). 

bined observation of all CAVs, i.e., O = O1 ×O2 ×· · ·×O|V|. 

2\) Action Space: In our research, we pay more attention to the decision-making actions of CAVs rather than the vehicle C. MADDPG For Decision-Making of CAVs

control level. Specifically, when traversing an intersection, we In our work, a model-free MARL algorithm, MADDPG, is establish a pre-determined driving route. Within this context, utilized as the baseline algorithm. 

the CAV must make decisions regarding acceleration or decel-In Deep Reinforcement Learning \(DRL\), a deep neural eration in order to execute a left turn at the intersection and network \(DNN\) serves as a non-linear approximator to obtain ultimately arrive at its intended destination. After selecting a optimal policies π∗ for CAVs \(agents\). The agents interact high-level decision, lower-level controllers generate the cor-with the environment and receive feedback in the form of responding steering and throttle control signals to control the rewards, which are used to update the agent’s policy. Let CAVs’ movement. The overall action space is the combined π = π



1, · · · , πN

denote the set of all CAVs’ policies and actions of all CAVs, i.e., A = A



1 × A2 × · · · × A|V|. 

θ = θ1, · · · , θN

denote the parameter set of corresponding 3\) Reward Function: The reward function has a great effect policy, where N = |V| is the number of CAVs. CAVs update on the final performance of the algorithm. In order to make their policies based on the estimation of the Q-function for agents pass the intersection safely and effectively, the reward each possible action using the off-policy actor-critic algorithm of ith agent at the time step t is defined as MADDPG \[40\]. The objective function for MADDPG is the r

expected reward J \(θ\), i.e., J \(θ

i,t =

wcrc

\+

were

\+

wara

\(8\)

i\) = E\[Ωi\(t\)\]. The optimal

| \{z \}

| \{z \}

| \{z \}

policy of each CAV is represented as π∗ = arg maxπ J \(θi\). 

Collision reward

Efficiency reward

Arrival reward

θi

θi

Then the algorithm calculates the gradient of the objective where wc,we, and wa are the weight coefficients of collision function with respect to θi as

reward rc, efficiency reward re, and arrival reward ra, respectively. These evaluation terms are defined as follows:

∇θ J \(π

π

Qπ\(x, a

i

i\) = Ex,a∼D\[∇θi i\(ai|oi\)∇ai

i

1, · · · , aN \)\], 

• Collision reward rc: Safety is the most important criterion \(12\)

for a vehicle. In order to make the agent learn to drive where x = O = \(o1, · · · , oN \), Qπ\(x, a i

1, · · · , aN \) is a

safely, we give it a greater penalty when a collision centralized action-value funciton, and D is the replay buffer. D

happens. 

contains transition tuples \(x, a, r, x′\), where a = \(a1, · · · , aN \)



−10

if agent

and r = \(r1, · · · , rN \). To minimize the loss function \(13\), the r

i collide

c =

\(9\)

0

otherwise

centralized action-value function Qπ is updated for i

• Efficiency reward re: The speed range \[vmin, vmax\] for L\(θi\) = Ex,a,r,x′\[\(y − Qπ\(x, a

i

1, · · · , aN \)\)2\], 

\(13\)

the agents passing the intersection is set based on real-world traffic rules. The agent is not recommended to drive where y

=

ri \+ γQπ′ \(x′, a′ , · · · , a′ \)|

i

1

N

a′ =π′ \(o

j

j

j \) . 

π′

=

at a speed outside this range, and we encourage the agent π



θ′ , · · · , π ′

stands for the target policies with delayed 1

θN

to pass as efficiently as possible within the speed range. 

′

parameters θ . The schematic diagram is shown in Fig. 1

i

And a constant Ce is used to adjust the maximum speed bonus. 

n

vi − vmin o

r

IV. GAME-PRIOR ATTENTION MODEL

e = Ce × min

\(10\)

vmax − vmin

In this section, the whole framework of our MA-GA-

• Arrival reward ra: When any agent completes its ultimate goal to reach the end, they will obtain an arrival reward. 

DDPG model is first outlined. Then we introduce an attention mechanism-based policy network and an interaction filter ap-5

if agent

r

i reaches destination

proach. Furthermore, a safety inspector based on the attention a =

\(11\)

0

otherwise

weights and the level-k game is applied to enhance the safety where T is the total time steps for one episode. 

performance of the algorithm. 





5

**Attention-MADDPG**

**Observation **𝓞𝓞

**Decision Network**

𝒊𝒊

Action 1

**Observation **𝓞𝓞𝒊𝒊

**Decision Network**

**Agent 2**

Action 2

…

…

…

**Agent 1**

**Agent 3**

**Level-k Priority-Based Safety Inspector** **Action **

**Agent 4**

**Correction**

Action 1∗

CAV

Action 2∗

…

Level-k Prior

Attention Matrix

Conflict Predictor

∗

HV

a = arg 𝑚𝑚𝑚𝑚𝑚𝑚 𝑆𝑆𝑆𝑆𝐷𝐷

Motion Corrector

t

𝑎𝑎

𝑎𝑎𝜖𝜖𝐴𝐴𝑖𝑖

Fig. 2. The overview of our MA-GA-DDPG Model. 

A. Model Overview

Inspired by \[11\], we design an attention-based policy network for each agent in a decentralized training process, as The schematic representation of our model is depicted in shown in Fig. 3. The network contains three modules: encoder Figure 2. Initially, we devise an innovative policy network block, attention block, and decoder block. In the encoder employing the attention mechanism for each agent within block, the features F

the MADDPG algorithm. This network adopts an encoder-i of the agent i and its observation matrix O

decoder framework, incorporating a multi-head attention layer i are encoded as high-dimension vectors by a Multilayer Perceptron \(MLP\), whose weights are shared between all to comprehensively capture interaction relationships among vehicles. 

agents. Subsequently, attention weights for each Connected X

and Autonomous Vehicle \(CAV\) in relation to all surrounding i = M LP \(Fi, Oi\)

\(14\)

traffic participants are computed based on the attention-based And then the feature matrix is fed to the attention block, policy network. We then introduce a filtering rule employing composed of Nhead attention heads stacked together. Unlike these attention weights to effectively screen strongly interact-the attention layer in the Transformer model \[10\], this block ing participants. 

produces only the query results \(attention weights\) of agent Simultaneously, the attention degree acquired by the policy i, which indicate how much attention it should pay to the network for each vehicle in the scenario is construed as the surrounding vehicles. 

priority weight for the vehicle’s passage through the intersec-In the attention block, the ego vehicle emits a single query tion. Leveraging the concept of a level-k game \(hierarchical Qi = \[q0\] ∈ R1×dk to select a subset of vehicles based on the game\), these priority weights are transformed into a level environment, where dk is the output dimension of the encoder prior. Subsequently, a safety inspector is defined to oversee layer. This query is then projected linearly and compared to the safety aspect. Utilizing the input game prior, the safety a set of keys Ki = \[k0, k1, · · · , kN \] ∈ R\(N\+1\)×dk containing i

i

i

inspector proficiently anticipates, evaluates, and rectifies high-descriptive features for each vehicle, using dot product q0kT

i

risk actions in a timely manner, thereby mitigating or resolving to calculate the similarity. The Qi, Ki and Vi are calculated conflicts for each CAV. The subsequent presentation of the as follows. 

safety inspector demonstrates its efficacy in enhancing the Qi = W QXi

safety of the RL algorithm. 

Ki = W K Xi

\(15\)

Vi = W V Xi

B. Attention-Based Policy Network

where the dimensions of W Q and W K are \(dk × dN \), and The attention mechanism has been well-documented to W V ’s is \(dv × dh\). 

enable neural networks to discover interdependencies among The attention matrix is obtained by scaling the dot product a variable number of inputs and has been applied in the social with the inverse-square-root-dimension

1

√

and normalizing it

dk

interaction research of autonomous vehicles \[11\], \[22\]. 

with a softmax function σ. The attention matrix is then used

6

to gather a set of output values Vi = \[v0, · · · , vN \], where agents have level-0 reasoning and decides the best response to i

i

each vj is a feature computed using a shared linear projection such actions. Similarly, a level-2 agent assumes all other agents i

Lv ∈ Rdx×dk . The attention computation for each head can are level-1 and makes decisions based on this assumption. This be written as

hierarchy continues for higher levels. However, due to bounded QiKT 

Atm = σ

i

√

V

rationality for the agents \[41\], this assumption may not always i

i

\(16\)

dk

hold true. The experiments reveal that humans generally have Then the output from all M heads will be combined with at most level-3 reasoning \[4\], but this may vary depending on a linear layer:

the game being played. 

M

The level of the agent is obtained based on the attention X

Ati =

Atm

i

\(17\)

mechanism and is considered as important prior knowledge. 

m=1

As shown in Fig. 4, our method mainly includes two steps: The

final

attention

vector

is

denoted

by

At

Interactive Object Selection and Level Prior Determination. 

i

=

At



The detailed process is summarized in Algorithm 1. 

i,1, Ati,2, · · · , Ati,|N

, where At

i |

i,j \(j

∈ Ni\) denotes

the weight of the agent i’s attention to the surrounding

• Step 1 : Interactive Object Selection. Similar to human vehicle j, satisfying the cumulative summation relationship: attention, we set an attention radius dis0 and an attention P|Ni | At

weight threshold δ

j=1

i,j = 1. The vector Ati will be fed to the decoder 0 for each CAV to select potential

block along with the encoding result of agent i. Finally, the interaction objects. At each moment, when a surrounding value of the agent i’s action at the next time step will be vehicle j satisfies the condition that the distance disij assessed. 

between j and CAV i is less than dis0 and the attention weight Ati,j is greater than δ0, and the interaction limit Q

**Encoder**

**Attention**

**Decoder**

has not been reached, it is included in the set of Potential q

interaction Objects P Ointer. 

k

• Step 2 : Level Prior Determination. The interaction CAV

v

V

importance is determined based on the attention weight. 

Q

k

In the interaction environment, a vehicle that receives K

Vehicle 1

v

more attention is believed to be more important to the

**…**

**…**

**…**

Action

CAV, and vice versa. In an environment with only one QKT

k

σ\(

\)V

CAV, the interaction importance of the environment ve-𝑑𝑑𝑘𝑘

Vehicle N

v

hicle with the highest attention weight \(i.e., the most attention received\) is ranked highest, followed by the Fig. 3. The attention-based policy network for every single agent. 

others in descending order of attention weight. Finally, we obtain a list of interaction importance Ranki between Overall, the attention-based policy network has the fol-the CAV and all surrounding vehicles. In a multi-CAVs lowing significant advantages: \(1\) It can handle the variable environment, since each CAV can calculate the attention amount of observation information inputs; \(2\) It has permuta-weight for all vehicles, the global attention weight of tion invariant outputs that are independent of the sequence of vehicle j is the sum of the attention weight given by surrounding agents; \(3\) It has good interactive interpretability all CAVs:

V

based on the attention matrix. In the next subsection, we will X

BAtj =

At

screen the interactive objects based on the interpretable feature i,j

\(18\)

i=1

of the attention mechanism and obtain the intersection traffic prior based on the hierarchical game. 

The environment vehicle with the highest attention weight and priority is ranked highest, followed by the others in descending order of attention weight. If the interaction C. Hierarchical Game Prior From Agent’s Attention object limit Q of the CAV is reached, the top Q objects The interpretability of the attention network allows us to in the sorted set P Ointer are selected. 

further utilize the learned attention weight information. In the real world, in order to pass through intersections, both CAVs and HVs will have competitive or cooperative game D. Safety Inspector Based On Hierarchical Game Prior relationships with each other. If this game relationship can be During vehicular passage through an intersection, the preva-learned and sent to the algorithm as prior information, it will lent assumption is that a vehicle garnering more attention is greatly help the algorithm explore and learn more efficiently. 

considered to hold greater significance or pose an increased To capture the strategic decision-making process of HVs, a degree of risk. Consequently, we contend that vehicles charac-game-theoretical concept named level-k reasoning is used \[14\]. 

terized by higher attention weights should be afforded a higher This approach assumes that humans have different levels of priority or right of way at intersections. This established right-reasoning, with level-0 being the lowest. A level-0 agent is a of-way hierarchy can serve as foundational information to ex-non-strategic agent that makes predetermined moves without pedite the learning of action strategies by the RL algorithm that considering the possible actions of other agents. On the other align with real-world logical constructs. With this objective in hand, a level-1 agent is a strategic agent that assumes all other mind, we have architected a safety inspector module based on



7

**Encoder**

**Attention**

Attention Weight

q

𝐴𝐴𝑖𝑖𝑖𝑖

k

**Attention Matrix **𝑨𝑨

**Level-3**

CAV

v

V

**Level-1**

Q

k

**Level-2**

Vehicle 1

v

K

**…**

**…**

**…**

**Level-0**

QKT

k

σ\(

\)V

𝑑𝑑𝑘𝑘

Attention Radius 

**Level-3**

𝑟𝑟

Vehicle N

v

Fig. 4. Attention-based interactive object selection for each CAV. 

Algorithm 1: Obtain Hierarchical Level Priors Based nuity and stability. The safety supervisor, founded on the level-On Attention Mechanism

k priority-based framework, is visually represented in Figure Inputs : At, dis0, δ0, Q

5. 

Outputs: P Ointer, Rank

1 Step 1:

2 for i = 1 to |V |\(i ∈ V \) do

3

Calculate Attention vector Ati by Eq.16 and Eq.17; 

4

for j = 1 to |V \+ Ni| \(j ∈ |V| ∪ Ni\) do 5

Calculate the Euclidean Distance between agent i and j : Dis\(i, j\); 

6

if Dis\(i, j\) > dis0 and Ati,j > δ0 then 7

P Oi

= P Oi

∪ j

inter

inter

8

if |P Oi

| > Q then

inter

9

Remove P Oi

\[−1\] from P Oi

; 

inter

inter

10

end

11

end

12

Sort P Oi

in descending order based on

inter

CAV

Ati,j; 

13

end

14 end

HV

Safety Check Area

15 Step 2:

16 for j = 1 to |V \+ Ni|\(j ∈ |V | ∪ Ni\) do Fig. 5. Trajectory prediction of surrounding agents and conflict checking for 17

BAtj = PV

σAt

i=0

i,j ; 



CAV i at the intersection

1 if j ∈ P Oiinter

18

σ =

0 else

The specific calculation process of the safety inspector 19 end

module is as follows:

20 Sort BAt in descending order; 

21 for j = 1 to |V \+ Ni| \(j ∈ |V | ∪ Ni\) do

• Step 1: Agent Trajectory Prediction and Conflict Check-22

Update: Ranki,j = Index\(BAtj\); 

ing. Through the communication between CAVs, the 23 end

safety inspector obtains the state information O of all perceived vehicles in the intersection at any time step t0, and the current action decision set At of all CAVs. Then 0

based on the level-k prior information, it selects agent i the level-k priority principle. Analogous to the Critic network from the CAV set V in descending order to carry out within the RL algorithm, this safety inspector module operates active prediction of agent risk. For agent i, let ki denote independently of the policy network. 

its prior level, and T denote the forward prediction step The safety inspector module functions as an active conflict size. Obtain the future trajectory sequences of agent i : regulator, embodying two primary components: the Proactive Predictor of Agent Risk and the Assisted Corrector of Agent trai ki = xi

, yi

ki , xi

, yi

ki , · · · , 

Motion. These elements are instrumental in assisting and recti-t0 a

t

t

t

t

t

0 \+1

0 \+1

0 \+2

0 \+2

0

fying the agent’s exploratory behavior during the initial stages, xi

, yi

ki \(a ∈ A \)

t

t

t

0 \+T

t0\+T

0

0

thereby ensuring the algorithm’s performance maintains conti-

\(19\)

8

Algorithm 2: Level-k Priority-based Safety Inspector Degree SED function to measure the degree of conflict Inputs : t

mitigation brought about by agent action correction: 0, T , At , O, S

0

Output: A∗t0

SED\(a, a′, T ra\) = CI\(a, T ra\) − CI\(a′, T ra\) \(22\)

1 for i = 1 to |V | \(i ∈ V \) do

where T ra is the future trajectories set of all vehicles, a 2

Obtain the output action at of policy network and 0

and a′ are the origin action and corrected action of agent level Prior ki by Alg. 1; 

i, respectively, and T raa′ is the future trajectories set of 3

for t = 1 to T do

all vehicles based on the corrected action a′. 

4

Sample future trajectories based on at by 0

M DP

So our objective function for agent i is derived by

: \(xi

, yi

\) = M DP \(xi , yi \)

k\+1

k\+1

k

k



5

end

ai∗ = arg max SED a, a′, \(trai ki , \(traj \)kj , t

t

t

ki

0

0

0

6

trai

=

a′∈A

t

i

\(23\)

0

at0



n

o

xi

, yi

ki , . . . , xi

, yi

ki

· · · , \(tram\)km

t

t

; 

0

0 \+1

t0\+1

t0\+T

t0\+T

7

for j = 1 to |V| \(j ∈ V and j ̸= i\) do

• Step 3: Output the optimal actions. 

kj

8

Get traj

Judging whether all agents have completed the above t

by V2V communication; 

0

9

end

process, if all have been completed, execute all agent-10

for m = 1 to |Ni| \(m ∈ Ni\) do

corrected security actions A∗t . 

0

11

Predict future trajectories based on Oi by The operational procedure of the safety inspector is algo-IDM : tramkm = IDM \(xm, ym\)

rithmically described in Algorithm 2. 

t0

k

k

12

end

Much like the MADDPG algorithm, the MA-GA-DDPG

13

Calculate the number of conflict points algorithm is grounded in the actor-critic model. Within this CI\(a, T ra\) \(a ∈ At \); 

framework, the actor assumes the role of decision-maker over 0

14

for a′ ∈ Ai do

time, while the critic evaluates the actor’s behavior. Each 15

Calculate CI\(a′, T ra\); 

agent within the system is equipped with both an actor and 16

Get SED\(a, a′, T ra\) by Eq. 22; 

a critic, encompassing behavior and target networks. CAVs 17

end

strive to enhance their own policy to maximize rewards, 18

Solve Eq.23 and get ai∗

simultaneously updating their critic’s Q-function to evaluate t ; 

0

19

Update A∗ = A∗ ∪ ai∗

actions effectively. The primary objective is to adapt the target t

; 

0

t0

t0

20 end

network’s parameters θ for CAVs to learn optimal action strategies. The comprehensive representation of our refined model is encapsulated in Algorithm 3. 

by sampling T steps through the MDP process, and obtain the future T step trajectories of other CAV j through V. SIMULATION AND PERFORMANCE EVALUATION

communication:

This section commences by introducing the simulation en-traj kj = xj

, yj

kj , xj

, yj

kj , · · · , 

vironment, providing an overview of the defined environment, t0

t0\+1

t0\+1

t0\+2

t0\+2

followed by a detailed description of the training experiments xj

, yj

kj \(j ∈ V\)

t

and associated hyperparameters. Subsequently, the experimen-0 \+T

t0\+T

\(20\)

tal results are presented, and a thorough analysis of various And for all HV m within the observation range of i, use cases is conducted. 

the IDM model to predict their future trajectories : tramkm = xm

, ym

km , xm

, ym

km , · · · , 

t

A. Simulation Environment

0

t0\+1

t0\+1

t0\+2

t0\+2

xm

, ym

km \(m ∈ N

Building upon the foundation of an OpenAI Gym envi-t

i\)

0 \+T

t0\+T

\(21\)

ronment \[42\], we have formulated a RL training simulator Then judge whether there is a conflict between the future conducive to multi-agent centralized training and distributed trajectories of agent i and all other vehicles. If there is a execution. The simulator currently offers the flexibility to conflict, jump to Step 2, otherwise, the output action of tailor the intersection environment to specific requirements, the agent is safe, and the safety check of agent i at time accommodating both CAVs and HVs. It is designed to extend step t ends. 

its applicability to diverse scenarios beyond intersections. 

• Step 2: Action Correction For Agent’s Decision-making. 

Within this simulator, actions prescribed by specific policies If the future trajectory of agent i conflicts with other undergo translation into low-level steering and acceleration vehicles, the optimal alternative action needs to be found signals via a closed-loop PID controller. Additionally, the to minimize the conflict in the intersection. We use the longitudinal and lateral decisions of HVs are governed by the number of conflict points of all vehicles in the scenario IDM and the MOBIL model, respectively, as explicated in as the conflicting index CI to measure the danger de-Section III-A2. 

gree of the scenario at each timestamp. Based on the Moreover, to emulate the perception and prediction capa-conflicting index CI, we define the Safety Enhancement bilities of human drivers regarding the movement of other

9

Algorithm 3: MA-GA-DDPG for CAVs

as defined by Zhang et al. \[43\]. The corresponding parameters Inputs : T

for each driving style are outlined in Table I. 

M ax, M, dis0, δ0, Q

Output: θ

TABLE I

1 for episode = 1 to M do

THE PARAMETERS OF DIFFERENT DRIVING STYLES. 

2

Initialize D ← ∅, a random process G for action exploration; 

J amDistance

DesiredT ime

M aximum

M aximum

Driving Style

\(d0\)\(m\)

Headway\(T \)\(s\)

Acceleration\(a0\)\(m/s2\)

Deceleration\(b0\)\(m/s2\)

3

Receive initial state x; 

Aggressive

3.38

0.86

1.35

2.07

Normal

3.67

1.14

1.34

2.06

4

for t = 1 to Tmax do

Timid

3.69

1.27

1.36

1.99

5

for CAV i = 1 ∈ V do

6

Get observation oi,t; 

Overall, we have configured three progressively challenging 7

Update action ai = πθ \(o

scenarios:

i

i,t\) \+ Gt; 

8

end

\(a\) Scenario with only CAVs, each entering from a separate 9

for i = 1 ∈ V do

lane. 

10

Get attention weights Ati by Alg. 1; 

\(b\) Scenario with four CAVs and a varying number of 11

Get corrected actions a∗ by At

i,t

i and

homogeneous HVs, wherein all HVs exhibit the same Alg. 2; 

driving style. 

12

Execute a∗ and update a

; 

i,t

i,t ← a∗

i,t

\(c\) Scenario with four CAVs and a varying number of het-13

Observe reward ri,t and new observation erogeneous HVs, wherein each HV possesses a distinct x′ ; 

i,t

randomly generated driving style. 

14

Update Di ← \(xi,t, a∗ , r

\); 

i,t

i,t, x′i,t

In addition, we have employed two baseline algorithms, 15

end

namely MADDPG and Attention-MADDPG \(MADDPG Al-16

x ← x′; 

gorithm with attention-based policy network\), for comparative 17

for CAV i = 1 ∈ V do

evaluation. 

18

Sample a random minibatch of S samples

2\) Implementation Details: The hyperparameter of the \(xi,t, a∗ , r

\) from D

i,t

i,t, x′i,t

i; 

model during the training is shown in Table II. The speed 19

Set yj = rj \+ γQπ′ \(x′j , a′ , . . . , a′

\); 

i

i

1,t

N,t

range: \[vmin, vmax\] is \[3.0, 9.0\]. In the attention-based policy 20

Update critic by minimizing the loss

network, the Encoder and Decoder both are MLP, which has L\(θi\) =

two linear layers and the layer size is 64 × 64. The Attention 2

1 P

yj − Qπ\(xj , aj , . . . , aj \)

; 

Layer contains two heads and the feature size is set as 128. 

S

j

i

1

N

When selecting the interaction with attention weights, we set 21

Update actor using the sampled policy

dis

gradient:

0 = 40, δ0 = 0.5, and Q = 5. In the safety inspector module, we predict T = 5 steps feature trajectories for each 22

∇θ \(π

i

i\) ≈

1

vehicle. All the experiments are conducted in a platform with P

∇ π

\)∇ Qπ\(xj , aj , . . . , aj \)

S

j

θi i\(oji

ai

i

1

N

Intel Core i7-12700 CPU, NVIDIA GeForce RTX 3070 Ti 23

end

GPU, and 32G memory. 

24

Update target network parameters for each CAV i:

TABLE II

25

θ′ ← τ θ

i

i \+ \(1 − τ \)θ′i

THE HYPERPARAMETER OF THE MODEL FOR TRAINING. 

26

end

27 end

Symbol

Definition

Value

Nt

Training Episodes

2000

Su

Steps Per Update

100

Ψ

Buffer Length

10000

traffic participants, all HVs are endowed with constant-speed λ

Learning Rate

0.01

motion prediction and collision avoidance functions looking B

Batch of Transitions

128

γ

Discount factor

0.95

Th seconds into the future. For each simulation episode, τ

Target update rate

0.01

we introduce randomized initial states for all agents, thereby wc

Weight for rc

1

preventing the policy network from memorizing specific action we

Weight for re

1

wa

Weight for ra

1

sequences and instead fostering the acquisition of generalized dis0

Maximum interaction distance of CAV

40m

policies. 

δ0

Attention threshold of CAV

0.05

Q

Maximum number of interactive objects for a CAV

5

B. Simulation Settings

1\) Training Scenarios Design: We have designed a mixed C. Performance Evaluation

human-machine environment to rigorously evaluate our algo-1\) Overall Performance: The average and cumulative re-rithm. To enhance the realism of the environment, we have wards of the agent during training are shown in Fig. 6. In the taken into account the heterogeneity of drivers, incorporating environment just having CAVs, the performance of Attention-three distinct driving styles: Aggressive, Normal, and Timid, MADDPG and MA-GA-DDPG are both significantly better





10

\(a\)

\(b\)

\(c\)

\(d\)

\(e\)

\(f\)

Fig. 6. The mean reward and cumulative reward of our model and other baselines in different environments, \(a\) and \(d\): just CAVs; \(b\) and \(e\): CAVs and homogeneous HVs; \(c\) and \(d\): CAVs and heterogeneous HVs. 

than that of MADDPG, which proves that the Attention complex environments. By contrast, although the performance mechanism can effectively improve the performance of the of MA-GA-DDPG decreases when faced with heterogeneous algorithm. 

agents, its overall performance still surpasses that of Attention-In the CAV-HV mixed driving environment, MA-GA-DDPG

MADDPG and MADDPG. 

shows more obvious advantages. In the mixed driving environ-3\) Safety Analysis: Safety is the most critical factor to ment of CAVs and homogeneous HVs, Attention-MADDPG

consider when designing CAV decision-making algorithms. 

has shown more powerful performance than MADDPG, while We first conduct 100 random scenario tests on three algorithms the stability and convergence of MA-GA-DDPG are further and count the success rate. When all the CAVs in the scenario better than Attention-MADDPG. MA-GA-DDPG obtains the do not collide and reach the destination smoothly, we record it most cumulative rewards during training, indicating that the as a success. After simulation, the success rate of MADDPG, model agent learns a policy function that can drive safely in A-MADDPG, and MA-GA-DDPG are 44.0% , 72.0%, 86.0%

traffic for a longer period of time. 

respectively. 

In the CAVs and heterogeneous HVs mixed driving envi-Meanwhile, to evaluate security during interactions, we ronment, HVs with different driving styles will bring more employ the post-encroachment time \(PET\) metric \[44\]. Fig. 8

complex and diverse interactive behaviors, which puts forward illustrates the PETs of different algorithms in various scenarios higher requirements for the learning ability of the model. MA-involving interactions between CAVs and other CAVs as well GA-DDPG still shows the best learning ability, and the average as all HVs. The average PET of MADDPG in CAH-HV

reward and cumulative reward are significantly better than \(homogeneous\) and CAV-HV \(heterogeneous\) is 1.30s and the two baselines. Our proposed model exhibits significant 1.72s respectively, and the average PET of A-MADDPG

performance improvement in these difficult scenarios. 

in CAH-HV \(homogeneous\) and CAV-HV \(heterogeneous\) 2\) Performance in Different Scenarios: At the same time, is 1.80s and 1.96s respectively. In contrast, MA-GA-DDPG

we compared the performance of the algorithms in differ-yields results of 3.61s and 3.59s, representing a 64.0% and ent mixed driving environments to analyze the impact and 52.1% increase over MADDPG. 

challenges of heterogeneous HVs on model learning. As Additionally, we found that different algorithms exhibit shown in Fig. 7, in the presence of heterogeneous agents, the varying levels of stability when the heterogeneity of the HVs performance of the three algorithms varies to different degrees. 

changes. Compared to the homogeneous HV environment, Specifically, MADDPG displays a certain degree of degrada-the average PET of MADDPG and A-MADDPG in the tion in performance, whereas Attention-MADDPG shows no heterogeneous HV environment increased by 32.3% and 8.9%, significant decline. This indicates that incorporating attention-respectively, while the performance of MA-GA-DDPG was based policy networks can enhance algorithm performance in more stable, with an average PET fluctuation of only 0.5%. 





11

\(a\)

\(b\)

\(c\)

Fig. 7. The influence of human driving characteristics on performance of different models :\(a\) MADDPG, \(b\) Attention-MADDPG, \(c\) MA-GA-DDPG. 

\(a\)

\(b\)

\(a\)

\(b\)

Fig. 8. CAVs’ PET statistics of different algorithms in different scenarios: Fig. 9. The average speed of CAVs from different algorithms: \(a\) CAVs and \(a\)CAVs and homogeneous HVs; \(b\) CAVs and heterogeneous HVs. 

homogeneous HVs; \(b\) CAVs and heterogeneous HVs. 

Overall, our simulation results and analysis indicate that MADDPG is the most aggressive in the interaction process, with the poorest safety performance, while our algorithm is safer and more stable. 

4\) Efficiency and Comfort Analysis: We expect that CAVs can maintain both efficiency and comfort while prioritizing safety. To gauge the effectiveness of CAVs, we examine the \(a\)

\(b\)

speed variation curve of CAVs in testing scenarios, while assessing driving comfort by analyzing longitudinal acceleration. 

Fig. 10. The average action acceleration of CAVs from different algorithms: As depicted in Fig. 9, the MADDPG algorithm exhibits the \(a\) CAVs and homogeneous HVs; \(b\) CAVs and heterogeneous HVs. 

highest average speed in both mixed driving environments; however, its aggressive driving behavior leads to dangerous interactions and frequent collisions, as previously analyzed. The feature more complex traffic conflicts and traffic flows, proA-MADDPG algorithm registers the lowest average speed, viding a robust test of our algorithm. 

but it passes through intersections at a slow pace, resulting Our

experiments

demonstrated

that

in

the

two-lane

in decreased efficiency. On the other hand, our MA-GA-and three-lane intersections, our MA-GA-DDPG algorithm DDPG algorithm can promptly decelerate to ensure interaction achieved passage success rates of 84.5% and 82.0%, respec-safety when approaching the intersection and then accelerate tively. These results highlight the effectiveness and scalability appropriately after passing the conflict point, striking a balance of our algorithm across different scenarios. 

between safety and efficiency. 

On the other hand, to explore the micro-behavioral inter-The acceleration curve, shown in Fig. 10, highlights that actions of CAVs, we selected interaction cases from these MADDPG has an excessive amplitude of acceleration and three scenarios for detailed analysis. Fig. 11 illustrates the deceleration when navigating through intersections, causing key moments in the interaction processes of three cases. In significant discomfort. In contrast, the A-MADDPG and MA-all cases, the CAVs from the south, west, north, and east GA-DDPG algorithms exhibit gentler acceleration and decel-approaches are labeled as CAV1, CAV2, CAV3, and CAV4, eration amplitudes, ensuring improved comfort. 

respectively. The animated version of three cases can be accessed at the site.1

Case 1

D. Algorithm Extension Testing and Case Analysis involved four CAVs and six HVs from different approaches. As the CAVs slowed down to yield, most HVs had To further test the effectiveness of our algorithm, in addition already left the vicinity by the time the vehicles approached to the basic single-lane cross-shaped unsignalized intersection, the intersection. At Timestep = 30, CAV4 from the south we designed two more complex intersection scenarios: a two-lane unsignalized intersection and a three-lane unsignalized 1See

https://drive.google.com/drive/folders/

intersection, as shown in Fig. 11 \(b\) and \(c\). These scenarios

1v8wtHtBeGzpuh3E-qNiGBQKEXMtn2G3K?usp=sharing





12

attempted a left turn but faced a potential conflict with **Actions**

a northbound straight-moving HV. After assessing the risk, CAV4 decided to stop and yield. Following the HV’s passage, **E**

CAV3 from the north made the first left turn through the **nvi**

intersection \(Timestep = 50\). Subsequently, the remaining **ronme**

**Scenario **

**Design**

three CAVs negotiated and sequentially passed the conflict **n**

point at the intersection \(Timestep = 90\). 

**t**

**MADCU**

Case 2 saw CAV1 at Timestep = 20 observing an on-Traffic Flow

coming straight-moving HV and beginning to decelerate. By **Multi-agent **

Timestep = 33, CAV1 stopped to wait for the HV to pass **Observations**

before accelerating through the intersection. At Timestep =

60, CAV

Fig. 12. The framework of ADCU-in-loop experiment. 

2, 

noticing a potential conflict with CAV1, also decelerated and waited for CAV1 to clear the conflict point before accelerating through. 

\(ADCU\), also known as the domain controller, into the entire Case 3 involved CAV2 decelerating at Timestep = 21

experimental setup as hardware. The ADCU replicates the to allow CAV3 to pass first and then accelerating after the computational environment of a real vehicle, which not only conflict cleared at Timestep = 32. At Timestep = 91, CAV4

avoids the safety risks associated with on-road testing but also also identified a potential conflict with CAV1, decelerated to closely approximates the effects of real-vehicle tests. 

yield, and waited for CAV1 to pass the conflict point before Experimental Framework: Our domain controller-in-loop accelerating through the intersection, ensuring all CAVs passed simulation framework is depicted in Fig.12. We designed safely. 

the simulation environment using the Carla simulator \[45\], 

Overall, the CAVs exhibited robust and cautious driving configuring and injecting HVs as background traffic flow styles. Upon approaching an intersection, they would typically based on the highway simulator \[42\]. Several ADCUs control slow down to observe the surroundings and predict the driving CAVs, with each ADCU controlling one CAV. CAVs can behaviors and future trajectories of nearby traffic participants. 

communicate with each other. The Carla simulator publishes Based on the conflict situation, they made various driving all agents’ perception data through the ROS system \[46\], 

decisions such as accelerating, stopping to yield, or forcefully and each ADCU subscribes to its environmental perception accelerating, balancing safety and efficiency while demonstrat-information as state input. The policy network processes these ing strong interaction capabilities to smoothly navigate through inputs to produce decision actions for each CAV. These actions the intersection. 

are then transmitted back to the Carla simulator via ROS

messages for action execution and the simulation of the next **Time**

CAV

HV

timestep. 

Hardware Platform and Experimental Setup: Our testing platform, as shown in Fig.13, includes four ADCUs, a com-

（a）

putational host, broadcasting and routing units, and several monitors. We set up a two-lane unsignalized intersection Step=1

Step=30

Step=50

Step=90

environment with four CAVs, each entering the intersection from one of four directions. 

Experimental Validation Results: In real tests, the decision

（b）

algorithms deployed on the ADCUs were capable of responding and computing at a frequency of 20Hz, fully meeting the Step=1

Step=20

Step=33

Step=60

real-time computational requirements of actual vehicles. Moreover, in the hardware-in-the-loop experiments, our method achieved a passage success rate of 83.1%. The computational accuracy and the error margin compared to pure simulation

（c）

experiments were maintained within 2%, demonstrating the Step=1

Step=21

Step=32

Step=91

efficiency and precision of our experiments. The animated version of the field experiment can be accessed at the site.2

Fig. 11. Snapshots at critical moments of three interaction cases, \(a\) case 1,single-lane intersection; \(b\) case 2, two-lane intersection; \(c\) case 3, three-VI. CONCLUSIONS

lane intersection. 

Cooperative decision-making for CAVs in complex human-machine environments remains a significant challenge. This paper addresses these issues by defining a decentralized E. Hardware-in-loop Experiment

MARL problem for navigating such intersections and introduces a novel algorithm, Multi-Agent Game-Aware Deep To validate the effectiveness and practicality of our approach, we designed a hardware-in-the-loop \(HIL\) experi-2See

https://drive.google.com/drive/folders/150 D ZEmzhSum

ment. We incorporated the Autonomous Driving Control Unit

fGo-uslcm9bYz4 5Qh?usp=drive link





13

**Broadcasting unit**

\[8\] C. Zhang, K. Kacem, G. Hinz, and A. Knoll, “Safe and rule-aware deep reinforcement learning for autonomous driving at intersections,” in 2022 IEEE 25th International Conference on Intelligent Transportation Systems \(ITSC\). 

IEEE, 2022, pp. 2708–2715. 

\[9\] J. Liu, P. Hang, X. Qi, J. Wang, and J. Sun, “Mtd-gpt: A multi-task decision-making gpt model for autonomous driving at unsignalized intersections,” in 2023 IEEE 26th International Conference on Intelligent Transportation Systems \(ITSC\). 

IEEE, 2023, pp. 5154–5161. 

\[10\] A. Vaswani, N. Shazeer, N. Parmar, J. Uszkoreit, L. Jones, A. N. Gomez, Ł. Kaiser, and I. Polosukhin, “Attention is all you need,” Advances in neural information processing systems, vol. 30, 2017. 

**Autonomous Driving Control Units \(ADCU\)**

\[11\] E. Leurent and J. Mercat, “Social attention for autonomous decision-making in dense traffic,” arXiv preprint arXiv:1911.12250, 2019. 

**Simulation Platform**

\[12\] L. Wei, Z. Li, J. Gong, C. Gong, and J. Li, “Autonomous driving strategies at intersections: Scenarios, state-of-the-art, and future outlooks,” in 2021 IEEE International Intelligent Transportation Systems Conference \(ITSC\). 

IEEE, 2021, pp. 44–51. 

Fig. 13. The field test of ADCU-in-loop experiment. 

\[13\] A. Guillen-Perez and M.-D. Cano, “Raim: Reinforced autonomous intersection management—aim based on madrl,” Proceedings of the NeurIPS, 2020. 

\[14\] N. Li, Y. Yao, I. Kolmanovsky, E. Atkins, and A. R. Girard, “Game-Deterministic Policy Gradient \(MA-GA-DDPG\). This algo-theoretic modeling of multi-vehicle interactions at uncontrolled intersec-rithm integrates an attention mechanism with level-k game tions,” IEEE Transactions on Intelligent Transportation Systems, vol. 23, no. 2, pp. 1428–1442, 2020. 

priors, enhancing the safety and efficiency of CAVs. The

\[15\] P. Hang, C. Huang, Z. Hu, and C. Lv, “Driving conflict resolution of attention-based policy network improves learning efficiency autonomous vehicles at unsignalized intersections: A differential game and captures complex interactions between the ego CAV and approach,” IEEE/ASME Transactions on Mechatronics, vol. 27, no. 6, pp. 5136–5146, 2022. 

other agents, using attention weights as interaction priors

\[16\] K. Dresner and P. Stone, “Multiagent traffic management: A reservation-in a hierarchical game framework, which includes a safety based intersection control mechanism,” in Autonomous Agents and inspector module to enhance CAV safety. Comprehensive Multiagent Systems, International Joint Conference on, vol. 3. Citeseer, 2004, pp. 530–537. 

experiments, including simulation and ADCU-in-loop testing

\[17\] P. Lin, J. Liu, P. J. Jin, and B. Ran, “Autonomous vehicle-intersection that consider human driver heterogeneity, demonstrate that coordination method in a connected vehicle environment,” IEEE Intelli-MA-GA-DDPG significantly improves safety, efficiency, and gent Transportation Systems Magazine, vol. 9, no. 4, pp. 37–47, 2017. 

\[18\] M. A. S. Kamal, J.-i. Imura, T. Hayakawa, A. Ohata, and K. Aihara, comfort. 

“A vehicle-intersection coordination scheme for smooth flows of traffic In the future, our research will focus on expanding our without using traffic lights,” IEEE Transactions on Intelligent Trans-algorithm to more complex and realistic scenarios. We will portation Systems, vol. 16, no. 3, pp. 1136–1147, 2014. 

\[19\] G. Schildbach, M. Soppert, and F. Borrelli, “A collision avoidance also extend the prediction horizon and develop a more so-system at intersections using robust model predictive control,” in 2016

phisticated conflict resolution module to enhance performance. 

IEEE Intelligent Vehicles Symposium \(IV\). 

IEEE, 2016, pp. 233–238. 

Additionally, we will thoroughly explore the social dynamics

\[20\] S. Hecker, D. Dai, and L. Van Gool, “End-to-end learning of driving models with surround-view cameras and route planners,” in Proceedings between CAVs and human-driven vehicles, aiming to ensure of the european conference on computer vision \(eccv\), 2018, pp. 435–

that CAVs emulate human driving behaviors while prioritizing 453. 

safety and efficiency. 

\[21\] J. Xue, B. Li, and R. Zhang, “Multi-agent reinforcement learning-based autonomous intersection management protocol with attention mechanism,” in 2022 IEEE 25th International Conference on Computer Supported Cooperative Work in Design \(CSCWD\). 

IEEE, 2022, pp. 

REFERENCES

1132–1137. 

\[22\] Z. Dai, T. Zhou, K. Shao, D. H. Mguni, B. Wang, and H. Jianye, 

“Socially-attentive policy optimization in multi-agent self-driving sys-

\[1\] S. Aradi, “Survey of deep reinforcement learning for motion planning of tem,” in 6th Annual Conference on Robot Learning. 

autonomous vehicles,” IEEE Transactions on Intelligent Transportation

\[23\] J. Wang, Q. Zhang, and D. Zhao, “Highway lane change decision-Systems, vol. 23, no. 2, pp. 740–759, 2020. 

making via attention-based deep reinforcement learning,” IEEE/CAA

\[2\] H. Lu, C. Lu, Y. Yu, G. Xiong, and J. Gong, “Autonomous overtaking for Journal of Automatica Sinica, vol. 9, no. 3, pp. 567–569, 2021. 

intelligent vehicles considering social preference based on hierarchical

\[24\] D. Chen, Z. Li, Y. Wang, L. Jiang, and Y. Wang, “Deep multi-agent reinforcement learning,” Automotive Innovation, vol. 5, no. 2, pp. 195–

reinforcement learning for highway on-ramp merging in mixed traffic,” 

208, 2022. 

arXiv preprint arXiv:2105.05701, 2021. 

\[3\] Y. Rahmati, M. K. Hosseini, and A. Talebpour, “Helping automated

\[25\] A. Oroojlooy and D. Hajinezhad, “A review of cooperative multi-agent vehicles with left-turn maneuvers: a game theory-based decision frame-deep reinforcement learning,” Applied Intelligence, pp. 1–46, 2022. 

work for conflicting maneuvers at intersections,” IEEE Transactions on

\[26\] H. Zhang, S. Feng, C. Liu, Y. Ding, Y. Zhu, Z. Zhou, W. Zhang, Intelligent Transportation Systems, 2021. 

Y. Yu, H. Jin, and Z. Li, “Cityflow: A multi-agent reinforcement learning

\[4\] M. Yuan, J. Shan, and K. Mi, “Deep reinforcement learning based game-environment for large scale city traffic scenario,” in The world wide web theoretic decision-making for autonomous vehicles,” IEEE Robotics and conference, 2019, pp. 3620–3624. 

Automation Letters, vol. 7, no. 2, pp. 818–825, 2021. 

\[27\] B. Toghi, R. Valiente, D. Sadigh, R. Pedarsani, and Y. P. Fallah, “Social

\[5\] P. Hang, C. Huang, Z. Hu, and C. Lv, “Decision making for connected coordination and altruism in autonomous driving,” IEEE Transactions on automated vehicles at urban intersections considering social and indi-Intelligent Transportation Systems, vol. 23, no. 12, pp. 24 791–24 804, vidual benefits,” IEEE transactions on intelligent transportation systems, 2022. 

vol. 23, no. 11, pp. 22 549–22 562, 2022. 

\[28\] N. Bard, J. N. Foerster, S. Chandar, N. Burch, M. Lanctot, H. F. Song, 

\[6\] X. Pan, B. Chen, S. Timotheou, and S. A. Evangelou, “A convex optimal E. Parisotto, V. Dumoulin, S. Moitra, E. Hughes et al., “The hanabi control framework for autonomous vehicle intersection crossing,” IEEE

challenge: A new frontier for ai research,” Artificial Intelligence, vol. 

Transactions on Intelligent Transportation Systems, 2022. 

280, p. 103216, 2020. 

\[7\] C. Wu, A. R. Kreidieh, K. Parvate, E. Vinitsky, and A. M. Bayen, 

\[29\] J. Zhang, C. Chang, X. Zeng, and L. Li, “Multi-agent drl-based lane

“Flow: A modular learning framework for mixed autonomy traffic,” 

change with right-of-way collaboration awareness,” IEEE Transactions IEEE Transactions on Robotics, vol. 38, no. 2, pp. 1270–1286, 2021. 

on Intelligent Transportation Systems, 2022. 

14

\[30\] Z. Niu, G. Zhong, and H. Yu, “A review on the attention mechanism of deep learning,” Neurocomputing, vol. 452, pp. 48–62, 2021. 

\[31\] Z. Zhang, S. Han, J. Wang, and F. Miao, “Spatial-temporal-aware safe multi-agent reinforcement learning of connected autonomous vehicles in challenging scenarios,” arXiv preprint arXiv:2210.02300, 2022. 

\[32\] Z. Cao and J. Yun, “Self-awareness safety of deep reinforcement learning in road traffic junction driving,” arXiv preprint arXiv:2201.08116, 2022. 

\[33\] A. M. Hafiz, S. A. Parah, and R. U. A. Bhat, “Attention mechanisms and deep learning for machine vision: A survey of the state of the art,” 

arXiv preprint arXiv:2106.07550, 2021. 

\[34\] S. Chaudhari, V. Mithal, G. Polatkan, and R. Ramanath, “An attentive survey of attention models,” ACM Transactions on Intelligent Systems and Technology \(TIST\), vol. 12, no. 5, pp. 1–32, 2021. 

\[35\] K. Zhang, Z. Yang, and T. Bas¸ar, “Multi-agent reinforcement learning: A selective overview of theories and algorithms,” Handbook of reinforcement learning and control, pp. 321–384, 2021. 

\[36\] P. Polack, F. Altché, B. d’Andréa Novel, and A. de La Fortelle, “The kinematic bicycle model: A consistent model for planning feasible trajectories for autonomous vehicles?” in 2017 IEEE intelligent vehicles symposium \(IV\). 

IEEE, 2017, pp. 812–818. 

\[37\] A. Kesting, M. Treiber, and D. Helbing, “Enhanced intelligent driver model to access the impact of driving strategies on traffic capacity,” 

Philosophical Transactions of the Royal Society A: Mathematical, Phys-ical and Engineering Sciences, vol. 368, no. 1928, pp. 4585–4605, 2010. 

\[38\] ——, “General lane-changing model mobil for car-following models,” 

Transportation Research Record, vol. 1999, no. 1, pp. 86–94, 2007. 

\[39\] M. T. Spaan, “Partially observable markov decision processes,” Reinforcement learning: State-of-the-art, pp. 387–414, 2012. 

\[40\] R. Lowe, Y. I. Wu, A. Tamar, J. Harb, O. Pieter Abbeel, and I. Mordatch, 

“Multi-agent actor-critic for mixed cooperative-competitive environments,” Advances in neural information processing systems, vol. 30, 2017. 

\[41\] Y. Wen, Y. Yang, and J. Wang, “Modelling bounded rationality in multi-agent interactions by generalized recursive reasoning,” in Proceedings of the Twenty-Ninth International Conference on International Joint Conferences on Artificial Intelligence, 2021, pp. 414–421. 

\[42\] E. Leurent, “An environment for autonomous driving decision-making,” 

https://github.com/eleurent/highway-env, 2018. 

\[43\] D. Zhang, X. Chen, J. Wang, Y. Wang, and J. Sun, “A comprehensive comparison study of four classical car-following models based on the large-scale naturalistic driving experiment,” Simulation Modelling Practice and Theory, vol. 113, p. 102383, 2021. 

\[44\] Z. Ma, J. Sun, and Y. Wang, “A two-dimensional simulation model for modelling turning vehicles at mixed-flow intersections,” Transportation Research Part C: Emerging Technologies, vol. 75, pp. 103–119, 2017. 

\[45\] A. Dosovitskiy, G. Ros, F. Codevilla, A. Lopez, and V. Koltun, “Carla: An open urban driving simulator,” in Conference on robot learning. 

PMLR, 2017, pp. 1–16. 

\[46\] M. Quigley, K. Conley, B. Gerkey, J. Faust, T. Foote, J. Leibs, R. Wheeler, A. Y. Ng et al., “Ros: an open-source robot operating system,” in ICRA workshop on open source software, vol. 3, no. 3.2. 

Kobe, Japan, 2009, p. 5. 



# Document Outline

+ Introduction 
+ Related Works  
	+ Decision-Making of CAVs at Intersections 
	+ Multi-Agent Reinforcement Learning and Attention Mechanism 
	+ Summary of Related Works 

+ MARL for Intersection Decision-Making  
	+ Scenario Description and Vehicle Movements  
		+ Scenario Description 
		+ Vehicle Movements 

	+ Problem Formulation  
		+ Observation Space 
		+ Action Space 
		+ Reward Function 

	+ MADDPG For Decision-Making of CAVs 

+ Game-prior Attention Model  
	+ Model Overview 
	+ Attention-Based Policy Network 
	+ Hierarchical Game Prior From Agent's Attention 
	+ Safety Inspector Based On Hierarchical Game Prior 

+ Simulation and Performance Evaluation  
	+ Simulation Environment 
	+ Simulation Settings  
		+ Training Scenarios Design 
		+ Implementation Details 

	+ Performance Evaluation  
		+ Overall Performance 
		+ Performance in Different Scenarios 
		+ Safety Analysis 
		+ Efficiency and Comfort Analysis 

	+ Algorithm Extension Testing and Case Analysis 
	+ Hardware-in-loop Experiment 

+ Conclusions 
+ References



