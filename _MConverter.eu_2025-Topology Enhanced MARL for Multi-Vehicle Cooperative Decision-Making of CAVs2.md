Topology Enhanced MARL for Multi-Vehicle Cooperative Decision-Making of CAVs

Ye Han, Lijun Zhang∗, Dejian Meng, Zhuang Zhang Abstract—The exploration-exploitation trade-off constitutes ing \(RL\) empowers vehicles to autonomously learn through one of the fundamental challenges in reinforcement learning environmental interactions, optimizing their policies without \(RL\), which is exacerbated in multi-agent reinforcement learning requiring manually designed complex rules. Deep reinforce-

\(MARL\) due to the exponential growth of joint state-action ment learning \(DRL\) leverages deep neural networks to handle spaces. This paper proposes a topology-enhanced MARL \(TPEMARL\) method for optimizing cooperative decision-making of high-dimensional state information, thereby enabling swift connected and autonomous vehicles \(CAVs\) in mixed traffic. This adaptation to dynamic and uncertain traffic environments. 

work presents two primary contributions: First, we construct In the domain of multi-vehicle cooperative decision-making, a game topology tensor for dynamic traffic flow, effectively a primary challenge lies in effectively processing not only compressing high-dimensional traffic state information and decrease the search space for MARL algorithms. Second, building individual vehicle states \(e.g., position, velocity, acceleration\) upon the designed game topology tensor and using QMIX as but also the intricate dynamics of their interactions. To address the backbone RL algorithm, we establish a topology-enhanced this, we propose a Topology-Enhanced Multi-Agent Rein-MARL framework incorporating visit counts and agent mutual forcement Learning \(TPE-MARL\) algorithm. The proposed information. Extensive simulations across varying traffic den-method abstracts the complex dependencies of vehicular insities and CAV penetration rates demonstrate the effectiveness of TPE-MARL. Evaluations encompassing training dynamics, teractions into a structured nodal feature representation, which exploration patterns, macroscopic traffic performance metrics, we term the game topology of the Connected and Autonomous and microscopic vehicle behaviors reveal that TPE-MARL suc-Vehicle \(CAV\) collective. Central to our method is a metic-cessfully balances exploration and exploitation. Consequently, it ulously designed game topology tensor, which pioneers the exhibits superior performance in terms of traffic efficiency, safety, explicit, semi-structured representation of multi-dimensional decision smoothness, and task completion. Furthermore, the algorithm demonstrates decision-making rationality comparable inter-vehicle dynamics, thereby bridging the gap between to or exceeding that of human drivers in both mixed-autonomy latent representations and physical parameters. By system-and fully autonomous traffic scenarios. Code of our work is atically integrating this tensor into the core components of available at https://github.com/leoPub/tpemarl. 

the MARL framework, TPE-MARL significantly enhances the learning efficiency and coordination performance in complex I. INTRODUCTION

vehicular scenarios. 

Technological

advancements

in

autonomous

driving, 

Vehicle-to-Everything

\(V2X\)

communication, 

and

edge

**Communication topology in other research** computing are driving Connected and Automated Vehicles \(CAVs\) from laboratory prototypes towards large-scale commercial deployment. However, as CAV penetration increases, the intelligent decision-making capabilities of individual vehicles have proven inadequate in meeting the traffic efficiency and safety demands of high-density, dynamic traffic

scenarios

\[1\]. 

Multi-vehicle

cooperative

driving

achieves motion coordination through distributed decision-arXiv:2507.12110v1 \[cs.AI\] 16 Jul 2025 making architectures. Prior research \[2\] has demonstrated that deployed Cooperative Intelligent Transport Systems can enhance traffic flow efficiency by at least 2%-6%. 

Furthermore, even excluding essential infrastructure and operational costs, these systems yield significant net benefits

\[3\]. 

Multi-vehicle cooperative driving is fundamentally a process of mutual negotiation among vehicles to establish desired Fig. 1. Communication topology vs. game topology in multi-vehicle systems. 

relative kinematic states, such as position and velocity. This To avoid confusion, the term topology in this study specifically refers to process can be modeled as a dynamic game with both coop-the topological relationships between vehicle dynamics. Existing research has predominantly focused on communication topologies among vehicles, which erative and competitive characteristics. Reinforcement learn-address information exchange relationships. 

Ye Han, Lijun Zhang, Dejian Meng, Zhuang Zhang are with the School of Automotive Studies, Tongji University, Shanghai 201804, The main contributions of this work are as follows: China. 

\{hanye\_leohancnjs, tjedu\_zhanglijun, 

mengdejian, zhuang\_zhang\}@tongji.edu.cn

• We design and construct a game topology tensor tailored

∗Corresponding author: Lijun Zhang

for dynamic traffic flows. This tensor effectively encodes

both the intrinsic dynamic characteristics of individual ve-ments. Eunjeong et al. developed a multi-agent reinforce-hicles and the complex game-theoretic interactions among ment learning framework using the basic SARSA algorithm them. It enables the compression of high-dimensional, to address consensus decision-making in cooperative driving dynamic observational data into a compact, fixed-length scenarios, achieving 5.5% energy consumption reduction com-feature vector. This process preserves critical information pared to heuristic decision-making \[6\]. J. L. et al. proposed and interpretability, thereby significantly reducing the di-a multi-agent game-theoretic prior attention DDPG method mensionality of the state space for reinforcement learning. 

that incorporates attention mechanisms to capture interactive

• We propose a novel MARL framework, building upon dependencies between the ego CAV and surrounding agents the QMIX architecture, that is fundamentally enhanced

\[7\]. By leveraging attention weights between autonomous by the game topology tensor. The framework leverages vehicles and other agents, this approach filters interaction variational inference to estimate the mutual information targets and extracts prior hierarchical game relationships, between an agent’s local view and the historical observa-thereby optimizing safety, efficiency, and ride comfort. Al-tions of its neighbors. To address partial observability, a though this method employs attention mechanisms to process trajectory reconstruction loss is introduced, compelling vehicle interactions during initial decision phases, it suffers agents to infer a more complete representation of the from limited interpretability. While subsequent game-theoretic traffic topology. This results in a cohesive system where modeling enhances decision safety through analytical meth-the topological information is deeply integrated into the ods, it prolongs the decision-making loop length, potentially agent’s learning process. 

compromising operational efficiency. S. C. et al. introduced

• We conduct extensive simulation experiments across a a dual-vehicle cooperative driving decision framework based range of traffic densities and CAV penetration rates. 

on MARL, utilizing Q-MIX as the backbone network \[8\]. 

The proposed algorithm’s performance is systematically This methodology implement stable estimation techniques to evaluated from multiple perspectives, including training mitigate propagation of overestimated joint Q-values among efficiency, exploration-exploitation patterns, macroscopic agents. But decomposing multi-agent collaborative decisions traffic flow metrics, and microscopic vehicle behavior into dual-vehicle problems fails to capture macroscopic traffic analysis. 

flow dynamics and high-level decision features. 

• TPE-MARL effectively balances exploration and ex-Interaction Enhancement Methods in Autonomous Driv-ploitation, and achieves significant gains in traffic effi-ing: The modeling of vehicular interaction game-theoretic ciency, safety, decision smoothness, and task completion relationships has attracted significant academic and industrial rates. Notably, the algorithm exhibits decision-making attention. Graph Neural Networks \(GNNs\), Transformers, and capabilities that outperform established human driver game theory have been extensively employed for vehicle inter-models in both mixed-autonomy and fully-autonomous action modeling recently \[7\], \[9\]–\[14\]. Chen et al. integrated traffic scenarios, leading to more stable and efficient GNN with Deep Q-Networks to develop an innovative Graph traffic flow. 

Convolutional Q-Network, serving as both an information The organizational structure of this paper is outlined as fusion module and decision-making processor \[9\]. This ap-follows: Section II reviews existing literature in the field. 

proach enhances the rationality of lane-changing decisions Section III rigorously defines the research problem and es-for Connected and Automated Vehicles \(CAVs\). However, tablishes theoretical assumptions. Section IV elaborates on the manually defined message-passing mechanisms in GNNs the proposed technical framework, detailing the core algo-may omit critical interaction details. Cai et al. \[11\] proposed rithmic components, implementation workflow, and innovative a Transformer-based reinforcement learning architecture for technical solutions. Section V conducts empirical analysis via multi-robot decision-making, generating actions through au-simulation experiments. Section VI concludes our work. 

toregressive mechanisms to achieve decentralized coordination while accommodating heterogeneous robot capabilities. Liu et al. \[7\] augmented decision safety by incorporating game-II. RELATED WORKS

theoretic interaction modeling in the policy refinement stage of MARL in Multi-Vehicle Decision Making \(MVDM\): RL, albeit at the cost of increased decision-making loop length MARL is a promising method in addressing interaction rela-and potential efficiency degradation. Yan et al. developed a tionships in multi-vehicle coordination \[4\], \[5\]. From the train-game-theoretic trajectory planning framework featuring two ing paradigm perspective, the Centralized Training with De-analytical game formulations that account for longitudinal centralized Execution \(CTDE\) architecture has been predom-and lateral interaction characteristics in mixed traffic \[14\]. 

inantly adopted in existing research. This framework learns a The method demonstrates superior performance under varying centralized value function based on global agent information, driving styles and human driver response delays. Neverthe-then utilizes gradients from this centralized value function less, the analytical game structure suffers from computational to train individual agent policies. Despite its limitations in complexity that escalates exponentially with participant count, sensitive information sharing and high computational costs and primarily addresses CAV-human interactions rather than during centralized training, CTDE remains widely employed cooperative CAV-CAV behaviors. 

due to its robust policy learning capabilities. 

In summary, optimization-based methods, game-theoretic Across various decision-making hierarchies of autonomous approaches, and multi-agent reinforcement learning \(MARL\) vehicles \(AVs\), MARL demonstrates performance improve-methodologies have been proposed to address this challenge

\[15\], \[16\]. The first two approaches demonstrate superior perAt each timestep, agent i ∈ N receives observation oi ∈ Ω

formance and interpretability in small-scale agent interactions via O\(s, i\), selects action ai ∈ A according to its policy, with but struggle to manage large-scale scenarios due to the well-joint observations and actions denoted as o and a respectively. 

known ”curse of dimensionality”. Multi-agent reinforcement After action execution, the system transitions to state s′ via learning algorithms, on the other hand, face difficulties in P \(s′|s, a\) and receives global reward r = R\(s, a\). Each agent

. 

addressing the dynamic complexity of interactive scenario. 

maintains an action-observation history τi ∈ Ti = \(Ω × A\)∗. 

Balancing exploration of new strategies against exploitation Due to partial observability, agents derive their policies of established policies within complex operational contexts re-πi\(ai|τi\) from historical observations. The joint policy π

mains a fundamental challenge for RL. In multi-vehicle coop-induces an action-value function:

erative decision-making frameworks, insufficient exploration

" ∞

\#

X

not only induces system instability but may also precipitate Qπ \(s, a\) =

γtr

. 

\(1\)

tot

Es0:∞,a0:∞

t | s0, a0, π

risks and safety hazards. 

t=0

B. Continuous Traffic Flow Settings

Based upon the work \[18\], we formalize a problem with fixed traffic scenarios but variable agent populations. Given the potential fluctuation of agent counts at each timestep, the agent set N becomes time-varying, and Nt = NCAV,t∪NHDV,t. 

Here, NCAV,t and NHDV,t respectively denote the sets of CAVs and Human-Driven Vehicles \(HDVs\) in the traffic flow at timestep t. Consequently, both the global observation o and joint action a defined in Section III-A exhibit time-dependent dimensionalities. 

It should be noted that the primary objective of our current formulation can be characterized as efficiently guiding vehi-Fig. 2. Schematic diagram of a typical environment for lifelong cooperative cles into their target lanes. Decision-making performance is driving in mixed traffic. It highlights the spatial distribution of HDVs evaluated based on vehicles’ initial and terminal states within and CAVs within the coordinating zone, CAV observation, communication infrastructure, and traffic flow directions. 

the designated corridor, along with trajectory characteristics during traversal, as illustrated in the dashed bounding box of Fig. 2. 

III. PROBLEM FORMULATION

C. World Model

This paper addresses a lifelong MARL problems. The term

”lifelong” is commonly adopted in Multi-Agent Path Finding We consider a unidirectional branch of a bidirectional 8-

\(MAPF\) contexts, as defined in \[17\]. Specifically, in scenario-lane arterial road. All vehicles in the 4 lanes are randomly as-centralized multi-vehicle cooperative decision-making prob-signed one of the 3 movement objectives: proceeding straight, lems, agents may depart and new agents with distinct ob-turning left, or turning right, with destination positions set jectives may enter the decision-making scenario at each time to the middle 2 lanes, the lefmost lane, and the rightmost step. Unlike conventional multi-vehicle coordination problems, lane, respectively. We employ the Intelligent Driver Model the lifelong variant features a dynamic agent population rather \(IDM, \[19\]\) as the car-following model for HDVs. The IDM

than a fixed number of participants. 

incorporates 5 principal parameters: desired time headway Tdes, maximum acceleration amax, minimum following gap d0, comfortable deceleration b, and acceleration exponent δ. The A. Partially Observable Markov Decision Process IDM aims to maintain a desired following distance given by In most cases, agents cannot perceive global state infor-d∗

\(t\) =

n−1

mation. Therefore, we model the multi-vehicle cooperative v



decision-making problem as a Partially Observable Markov n−1\(t\) \(vn\(t\) − vn−1\(t\)\)

d0 \+ max 0, vn−1\(t\)Tdes −

√

, 

Decision Process \(POMDP\). 

2 amaxb

\(2\)

A decentralized POMDP can be defined by a tuple and longitudinal acceleration given by

G = ⟨N , S, A, P, R, O, Ω, γ⟩, where N denotes the set of agents, specifically representing CAVs engaged in cooperative aIDM\(t\) =

decision-making \(henceforth, ”agent” refers exclusively to

" 

v

δ



2 \#

n−1\(t\)

d∗

\(t\)

\(3\)

n−1

CAVs unless otherwise specified\), S represents the global state amax 1 −

−

. 

v0\(t\)

d\(t\)

space encompassing all agents and environmental states, A constitutes the joint action space of all agents, P , R, and O

The lane-changing model for HDVs follows the configura-correspond to the state transition function, reward function, tion established in \[20\]. 

and observation function respectively, γ ∈ \[0, 1\) is the discount For CAVs, as illustrated in Fig. 2, each vehicle has percep-factor. 

tion of its own position, velocity, target lane, and vehicle type, 

as well as those of surrounding vehicles within its detection Right \(RC\). In the longitudinal dimension, 3 maneuvers are range. This perceptual data can be shared via infrastructure-available: Acceleration \(AC\), Maintain Speed \(MT\), and De-mediated communication protocols. 

celeration \(DC\). The action space for an individual agent We denote the HDV lane-changing state transition dynam-constitutes the Cartesian product of lateral and longitudinal ics governed by Equations \(2\) and \(3\) as uHDV. The state actions, expressed as:

transitions of CAVs are controlled by reinforcement learning A

× Along, 

\(8\)

algorithms, denoted as u

i = Alat

i

i

CAV. 

In this context, the world model, focusing on the system’s where Alat = \{LC, LK, RC\} denotes the lateral action set and i

state transition dynamics, can be formally expressed as: Along = \{AC, MT, DC\} represents the longitudinal action set. 

i

N \(

The joint action space of the system constitutes the Carte-

\[

u

P \(s\(t\)\) =

HDV

oi\(t\)

if i in NHDV,t, 

\(4\)

sian product of all agents’ individual action spaces: u

i=1

CAV

s\(t\), oi\(t\)

if i in NCAV,t. 

A = A1 × A2 × · · · × AN . 

\(9\)

D. Observation

The observation of agent i is

F. Reward Function

oi = si , si , 

\(5\)

ego

nbr

The reward introduced in this section corresponds to the where both the ego vehicle’s state si

and neighboring vehicle

environmental feedback \(hereafter referred to as the environ-ego

states si

are included. Ego vehicle’s state

mental reward throughout this paper\). Total reward function nbr

is detailed in Section IV-B. 

si

= xi, yi, vi, i

, i , Hi , Hi, Hi , 

\(6\)

ego

Itype Itarg

L

R

Given the variable agent population setting, our framework where xi, yi, vi, i

i

precludes direct summation of local rewards across agents. 

I

, 

, Hi , Hi, and Hi respectively

type

Itarg

L

R

denote vehicle i’s longitudinal position, lane index, longitu-This necessitates a novel metric for holistic traffic quality dinal velocity, vehicle type indicator \( i assessment in coordinating zones. We therefore design the I

∈ \{0, 1\}\), target

type

lane indicator \( i

following environmental reward function:

I

∈ \{0, 1, 2, 3\}\), left headway distance, 

targ

front headway distance, and right headway distance. The 1

X

r

ω

\+ ω

\+ω

neighboring vehicle states:

env = |N

1ria

2rip

3rflow \+ ω4rsafe, \(10\)

CAV| i∈NCAV

h

i

si

= concat xi − xj, yi − yj, vi − vj, j

j

, 

\(7\)

nbr

Itype, Itarg

where ri

j∈nbri

a and rip denote the action reward and positional reward for CAV i, rflow evaluates the overall traffic velocity, where, nbri comprises up to 6 nearest vehicles within 100

and rsafe represents the safety reward. The terms ω1,2,3,4 cor-meters ahead and behind across three lanes: the ego vehicle’s respond to weighting coefficients for each reward component. 

current lane and adjacent left/right lanes. These vehicles pose Specifically:

direct right-of-way conflicts with the ego vehicle, as illustrated \(

in Fig. 3. Consequently, the observation space has dimension-1

if accelerating or keeping highspeed, 

ra =

\(11\)

ality do = 38. Null vehicle positions are zero-padded when 0

otherwise. 

fewer than 6 neighboring vehicles are present. 

We design a potential field based on vehicles’ longitudinal positions and lane allocations to evaluate the positional value of vehicle i relative to its target:

e− \(l−x\)2

2σ2

f i \(x, y\) =

, 

p

\(12\)

ζ yi

−

targ

y \+ 1

where, σ and ζ denote the longitudinal and lateral attenuation coefficients, respectively. 

Based on differentiated reward method \[21\], we formulate the positional reward as:

ri = vi · ∇f i \(x, y\) , 

p

p

\(13\)

Fig. 3. Observation of a single vehicle. When the number of vehicles within where vi = \[vi , vi \]

∈ \{−1, 0, 1\}

x

y . In our work, vi

y

, so we

the observation range exceeds 6, we only consider vehicles with direct right-have:

of-way conflicts with the ego vehicle \(dark-colored vehicles in the figure\) and

" 

\#

ignore others. 

ζviysign y − yitarg

ri = vi \(l − x\) \+

f i \(x, y\) . 

p

x

\(14\)

ζ 

p

yi

− y

tar

\+ 1

E. Action Space

We stipulate that when yi = yi , the sign function satisfies targ

Each agent can select from 3 lateral maneuvers: Lane sign y − yi = −vi

targ

y . It can be observed that the terms ω1ria Change Left \(LC\), Lane Keeping \(LK\), and Lane Change and ω2rip occasionally exhibit congruent reward implications. 

We therefore interpret them collectively as an augmented actions. When the IGM principle is satisfied, agents can action reward mechanism without further differentiation. 

obtain the optimal global policy by simply selecting local greedy actions that maximize their individual utility functions \(a\) position field

Qi. QMIX \[22\] represents a canonical value decomposition method, operating under the following formulation:



argmax



a1 Q1

τ 1, a1

. 

argmaxQ





tot\(τ , a\) =

. 

, 

\(17\)



. 



a

argmaxan Qn \(τ n, an\)

where τ

=

\(τ0, · · · , τn−1\) represents the joint action-observation trajectory. Additionally, the Individual-Global-Max \(IGM\) principle must be satisfied to maintain consistency between local and global greedy behaviors. 

QMIX introduces a mixing network that aggregates individual agents’ local Q-values into a global Q-value, effectively modeling cooperative relationships among agents. The mixing network takes global state information as input and ensures the global Q-value is a monotonic non-decreasing function of each agent’s local Q-values, enabling separable joint policy optimization to enhance training stability and efficiency. 

QMIX has demonstrated superior performance in multi-agent cooperative tasks and is widely applied in scenarios requiring agent coordination, such as team games and task decomposition problems. 

Fig. 4. 

Visualization of the positional reward. This figure depicts the reward distribution for a vehicle tasked with executing a right turn at an upcoming intersection. Panel \(a\) shows the base reward field as defined in IV. METHODOLOGY

Equation \(12\). Panels \(b\), \(c\), and \(d\) then illustrate the rewards realized when performing straight, left-turn, and right-turn maneuvers, respectively. In these heatmaps, each pixel’s value corresponds to the reward obtained for a specific A. Construction of Dynamic Traffic Topology maneuver at that spatial coordinate. Notably, the reward distribution along the approaching roadway segment is invariant to the vehicle’s lane assignment. 

In dynamic traffic flows within fixed scenarios, let N ∈

\[Nmin, Nmax\] denote the variable vehicle count. The obser-We evaluate traffic flow effiency using the collective velocity vation space cardinality can be expressed as PNmax

|o|N , 

N =Nmin

of the vehicle stream:

though practical implementations typically define observation 1

vectors using maximum capacity: |o|Nmax . This exponential X

vi

rflow =

. 

\(15\)

|N |

v

scaling arises because each vehicle’s influence manifests max

i∈N

through inter-agent relative relationships rather than isolated For the safety metric, given the sparse occurrence of behaviors. 

accidents and their severe consequences on overall traffic To reduce search space complexity, we construct a game integrity, we employ summation instead of averaging in the topology based on observation discrepancies between CAV i computation:

and CAV j, defined as oi −oj . For effective feature extraction, rsafe = PiIcoll\(i\), 

\(16\)

we map these observation differences to 2D vectors through: where Icoll\(i\) denotes the indicator function that takes the value Dij := \(||oi − oj ||2, oi − oj\) ∈ R × Z, 

\(18\)

1 if vehicle i experiences a collision, and 0 otherwise. 

where, || · ||2 denotes the L2-norm of vectors, representing the Euclidean distance between two observations. The angular G. CTDE and QMIX

mapping operator ⟨·⟩ :

d

R → Z is implemented via SimHash

Our methodology adopts the Centralized Training with to measure angular proximity between observations \[23\]. The Decentralized Execution \(CTDE\) paradigm for multi-agent hash vector:

reinforcement learning. This framework employs decentralized oi − oj



control to address the exponentially growing joint action h = sign

vhash ·

, 

\(19\)

∥oi − oj∥

space while leveraging centralized training to learn cooperative 2

behaviors. Agents learn in a centralized manner with access to where v

m×do

hash ∈ R

denotes pre-generated random vectors, 

global information, but execute policies based on their local and sign\(x\) represents the sign function that takes the value action-observation histories. 

1 if x ≥ 0 and 0 otherwise. Concatenating all elements of h A prevalent approach to realizing CTDE is value function sequentially yields a binary number, which is then converted decomposition. The individual-global-max \(IGM\) principle to a decimal integer hint ∈ \{0, . . . , 2m − 1\} to quantify the ensures consistency between local and globally optimal greedy angular measurement of observation discrepancies. 

Fig. 5. The overall architecture of the TPE-MARL method for lifelong cooperative driving. Based on the traffic environment constructed in SUMO, the operational flow outputs actions through the action selector using environmental observations and traffic topology information. The training process stores experience trajectories in the replay buffer, explicitly models traffic topology relationships using state observations and TopologyNet, and integrates them into the reinforcement learning algorithm to achieve cooperative policy learning and optimization. 

In the POMDP framework, the system state is constituted by the joint observations of all agents, expressed as: se = \(o0, · · · , on−1\) ∈ Se, 

\(20\)

Within the current traffic, the local topology of agent i is formulated as:

T i = \(Dij0 , · · · , Dijk−1 \)

\(21\)

where \{j0, · · · , jk−1\} represents agent i’s local interaction set, denoted as ci. The centralized coordinator enables ci selection beyond individual agents’ observation constraints. To minimize exploration space while preserving decision efficacy, we adopt minimal-dimensional ci configurations within the coordinating zone under performance guarantees, which is detailed in Section V-C3. 

Fig. 6. 

The generation process of the traffic game topology tensor. All Building upon Equation \(21\), we derive the game topology observations and interaction information of the connected and automated vehicle in the scenario are uniformly integrated into the game topology tensor tensor as:

to comprehensively characterize the current traffic game situation. 

T \(se\) = \(T 0, · · · , T n−1\). 

\(22\)

Here, the topology T exhibits dimensionality n · k, whereas First, inspired by the UCT method \[24\], we constructed the search space dimensionality is n · do. Although k is a count-based exploration heuristic reward, which explicitly contingent upon the selection of c, the observation dimen-records the visitation counts of the reduced-dimensional states sionality do generally exceeds k in most practical scenarios. 

to avoid the curse of dimensionality in high-dimensional This dimensional reduction mechanism consequently enables state spaces while retaining the advantages of count-based significant compression of the search space, facilitating more exploration. The count-based exploration heuristic reward is: efficient exploration. 

1

rvis,t =

, 

\(23\)

p

B. Game Topology Enhanced Reward Function visit\(Tt\)

Based on the game topology tensor constructed from Equa-It can be seen that if the agent system visits an uncommon tion \(22\), we have improved the reward function in Section traffic topology, it will receive a higher reward. 

III-F. 

The reward term rvis acts on the entire system. For each

Fig. 7. Topology-enhanced network. The topology-enhanced network is a VAE-like neural network. The network samples historical observations of all agents in the current traffic from the replay buffer. For each agent, the encoder qϕ extracts the latent variable zit based on its trajectory τ it. The decoder pθ2

reconstructs the original observed trajectory from the latent variable zit. The decoder pθ takes as input the latent variable set zci\+ of agent i itself and all 1

t

agents in its topology attention set ci, and outputs the predicted topological state ˆ

T i

. 

t\+1

agent i, we define its local topology in Equation \(21\). To i to understand its future local state. 

quantify the effectiveness of the interaction between the agent and the system, here, we focus on how much information the However, direct computation of Equation \(24\) is challeng-neighboring agents j of agent i can provide for agent i to ing. Following \[25\], \[26\], we use a variational lower bound to understand its own local topological state T i approximate the mutual information. Let X = T i t\+1 at the next

t\+1, Y = zj

t , 

time step t\+1. This ”information-providing” capability can be ci\+\\\{j\}

and the condition C = \(τ ci\+ , z

\)

t

t

\(hereafter abbreviated

quantified by mutual information. Here, neighboring agents are as Cij\). The mutual information can be expanded in terms of not limited to those directly observed by the agent; we extend entropy:

it to a topological attention agent set ci. This set includes I\(X; Y |C\) = H\(X|C\) − H\(X|Y, C\). 

agents that have a significant topological influence on agent i, \(25\)

even if they may not be within i’s observation range. 

Further, it can be expressed as the expected log-likelihood Specifically, we compute the conditional mutual information difference:

between the next-time-step local topological state T i I\(X; Y |C\) =

t\+1 of

Ep\(x,y,c\) \[log p \(x|y, c\)\] −

agent i and a certain agent j in its topological attention set. 

\(26\)

Ep\(x,c\) \[log p \(x|c\)\] . 

Since we may not have direct access to the complete state of agent j, we introduce its latent variable zjt as a compact To obtain the conditional probabilities p\(x|y, c\) and p\(x|c\), representation of its state at time t. 

we designed a VAE-like neural network, as shown in Fig. 5, 

Now, we can use Mutual Information \(MI\) to measure the to assist in the computation. 

degree of information sharing between the latent variable zjt of agent j and the next-time-step local topological vector T i First, we designed a trajectory conditional encoder q t\+1

ϕ to

of agent i. Specifically, we compute the conditional mutual process the historical observation trajectory τ it of the agent information

up to the current moment. This encoder compresses high-I

ci\+\\\{j\}

\(T i ; zj |τ ci\+ , z

\), 

dimensional, sequential trajectory data into a compact latent t\+1

t

t

t

\(24\)

state representation zi

I

t . Subsequently, based on zt, the model

quantifies how much additional information the latent performs two main tasks. The first task involves using the variable zjt of agent j can provide for predicting the next decoder pθ for topology prediction, where the input is the set local topological state T i

1

t\+1 of agent i, given the historical

of latent variables zci\+

t

for the agent i itself and all agents in

trajectories τ ci\+

t

of all agents in the attention set and the latent its topological attention set ci, and the output is the predicted ci\+\\\{j\}

variables z

ci\+

t

of other agents excluding j. We denote the topological state ˆ

T i

∼ p \(· | z

\)

t\+1

θ

. The other task uses the

1

t

ci\+\\\{j\}

condition C = \(τ ci\+ , z

\)

t

t

as Cij for simplicity. A higher

decoder pθ to reconstruct the original observation trajectory 2

mutual information indicates that zj

ˆ

τ i ∼ p \(· | zi\)

t is more valuable for agent

t

θ

from the latent variable zi

2

t

t . 

We define the topology prediction loss: obtain an estimate Î of the conditional mutual information: h



i

n−1

1

Î\(T i ; zj | C

log p

T i

| zci\+

−

X

t\+1

t

ij \) ≈E

θ1

t\+1

t

LTP\(ϕ, θ1\) =

MSE\(T i , ˆ

T i \), 

\(27\)

\(34\)

n

t\+1

t\+1

h



i

i=0

E log pθ

T i

| zpartial

, 

1

t\+1

t

trajectory reconstruction loss:

where the first expectation is with respect to p\(T i , zj , C

t\+1

t

ij \), 

n−1

1 X

and the second expectation is with respect to p\(T i , C

L

t\+1

ij \). 

RG\(ϕ, θ2\) =

MSE\(τ i, ˆ

τ i\), 

\(28\)

n

t

t

In the implementation, these expectations are estimated by i=0

sampling from the data and utilizing Monte Carlo methods. 

and Kullback-Leibler divergence loss:

To obtain a comprehensive evaluation, we normalize the L

total information to derive the final reward term: KL\(ϕ\) = DKL\(qϕ\(·|τ i\)||N \(0, I\)\), 

t

\(29\)

n−1

where MSE\(x, y\) =

1

E\[\(x−y\)2\] is the mean squared error loss, X

X

ci\+\\\{j\}

r

ˆ

topo,t =

I\(T i ; zj|τ ci\+ , z

\). 

t\+1

t

t

t

\(35\)

and N \(0, I\) is the multivariate standard normal distribution n · |ci\+| i=0 j∈ci\+

with the identity matrix I as its parameter. Based on these loss functions, we can update the encoder-decoder parameters The reward term rtopo,t encourages the agent to take actions ϕ, θ

that not only enable it to visit new states but also maximize 1, θ2 according to Equation \(30\):

the acquisition of information about its future local environ-ϕ ← \(1 − α\)ϕ − α · ∇ϕ\(LTP \+ LKL − λGFLRG\), mental structure from topologically related neighbors \(even θ1 ← \(1 − α\)θ1 − α · ∇θ L

\(30\)

if indirectly perceived\). This effectively compensates for the 1

TP, 

θ

limitations of individual observation capabilities, promoting 2 ← \(1 − α\)θ2 − α · ∇θ L

2

RG, 

more intelligent and purposeful exploration. 

where λGF is a hyperparameter. Note the negative sign before Finally, by combining the direct reward from the environ-the gradient term of LRG with respect to ϕ, which indicates ment renv,t with the traffic topology-associated rewards rvis,t that the training objective of the encoder is to ensure the latent and rtopo,t, the total reward can be obtained. 

variables are beneficial for topology prediction and conform to the prior distribution, while not entirely relying on precise rtot,t = renv,t \+ β1rvis,t \+ β2rtopo,t. 

\(36\)

trajectory reconstruction. This encourages the latent variables The TD loss can be expressed as:

to learn more abstract features. 

Next, we utilize the trained network to estimate the LTD\(θ\) = \(rtot,t \+ γ max Qθ−\(st\+1, a′\) − Qθ\(st, at\)\)2, \(37\) a′

two components of mutual information. For the first term where θ and θ− are the parameters of the Q-network and the Ep\(x,y,c\)\[log p\(x | y, c\)\] in Equation \(26\), we approximate the true p\(T i

| zj, C

target Q-network, respectively. 

t\+1

t

ij \)

with the decoder pθ

output

1

pθ \(T i

| zci\+ \). That is:

1

t\+1

t

h



i

V. CASE STUDY

Ep\(x,y,c\)\[log p\(x | y, c\)\] ≈ E log pθ

T i

| zci

. 

\(31\)

1

t\+1

t

A. Case Settings

In fact, pθ \(T i

| zci \) serves as a variational lower bound 1

t\+1

t

The mixed traffic flow simulation environment is imple-for p\(T i

| zj, C

\(·\)\]

t\+1

t

ij \). Maximizing E\[log pθ

is one of the

1

mented using the Flow simulation framework \[27\], where objectives of the LTP loss. 

a customized bidirectional 4-lane highway scenario is con-Next, we estimate p\(x|c\) = p\(T i |C

t\+1

ij \), which predicts

structed through the built-in highway network. The roadway T i

ci\+\\\{j\}

configuration features a 250-meter main road with unidi-t\+1 given the latent variables zt

of other agents in the

attention set excluding j, along with all relevant history τ ci\+

rectional four lanes, operating under a speed limit of 23

t

, 

but without explicitly using the specific latent variable zj m/s \(approximately 82.8 km/h\). The topological structure t of

agent j. To achieve this without altering the structure of p comprises five critical nodes: 2 as the start and end points θ , 

1

we can modify the combination of latent variables input to of the main road, along with 3 branch endpoints forming a p

trifurcation structure. Full lane connectivity between the main θ

by removing the specific information contributed by zj 1

t . 

We construct a new latent variable zpartial road and branches is achieved via 12 lane-level connectors, t

as the input to pθ . 

1

In zpartial

enabling vehicles to transition from any main road lane to t

, the portion originally contributed by zjt is replaced with a sample ˜

zj

arbitrary branch directions through designated connectors. A t drawn from the prior distribution N \(0, I\), probabilistic route selection mechanism governs vehicle path ci\+\\\{j\}

zpartial =

, z

\). 

t

Aggregate\(˜

zjt t

\(32\)

planning at the mai road endpoint node, where vehicles have a 25% probability to divert to either left or right, and a 50%

Then, we use this modified set of latent variables to make probability to proceed straight. We initialize vehicles with predictions:

randomized spawn positions. 

h



i

E

HDVs employ classical control models. The acceleration p\(x,c\)\[log p\(x | c\)\] ≈ E log pθ

T i

| zpartial

. 

\(33\)

1

t\+1

t

control module, implemented with configurations detailed in Substituting these approximations into Equation \(26\), we Section III-C, generates longitudinal motion commands via

IDM model. The lane-changing decision module utilizes built-settings would impact the overall performance of the algo-in lane change controller to execute strategically aggres-rithm. 

sive lane-changing policies, constrained to route-planning-4\) Q-MIX: As described in Section III-G. 

related maneuvers \(e.g., ramp transitions, overtaking\) while In addition to these RL algorithms, we implement the deliberately deactivating collision avoidance and safety dis-previously described HDV model to control all vehicles in tance constraints, thereby simulating human drivers’ risk-scenarios simulating fully human-operated traffic. 

prone decision-making in complex scenarios. Road network navigation is achieved through continuous router detailed in C. Implementation Details

the code documentation of the Flow project. 

During the initial training phase, frequent lane changes Autonomous vehicle controls for acceleration/deceleration and abnormal deceleration behaviors caused by stochastic and lane-changing are exclusively governed by algorithmic action selection often induce traffic congestion. To maintain regulation, with complete deactivation of all collision avoid-normative traffic flow dynamics, we implement a stepwise ance mechanisms and safety distance constraints. This config-monitoring mechanism that detects vehicles decelerating be-uration aims to optimally demonstrate the algorithm’s inherent low a predefined velocity threshold at each time step, followed capabilities by eliminating external behavioral interference. 

by systematic removal of non-compliant vehicles from the simulation environment. 

1\) Observation: In the problem formulation of continuous TABLE I

PARAMETERS SETTINGS FOR THE EXPERIMENTS

traffic flow, the stochastic generation of new vehicles at the road origin during each time step necessitates robust compen-Param Type

Params

Value

sation mechanisms for road topology prediction. To address Sim Step

0.1 s

this inherent randomness, we explicitly integrate per-time-HDV departure speed

10 m/s

step vehicle generation metadata into the observational inputs CAV departure speed

10 m/s

Simulator

Max HDV speed

20 m/s

of autonomous agents. This augmentation enables proactive and

Max CAV speed

20 m/s

anticipation of evolving traffic patterns while maintaining Environment

a

deterministic prediction constraints. 

max

3.5 m/s2

d0

2 m

2\) Reward funcion: We construct the reward function using b

1.5 m/s2

Equations \(10\)-\(16\), \(23\), and \(36\). As a supplement to Equa-δ

4

tion \(10\), we introduce a task completion reward ω5rcomplete to σ, ζ

60.0, 1.0

encourage vehicles to accomplish driving tasks, where rcomplete Reward Function

w1, w2, w3, 

10.0, 2.0, 1.0, 

denotes the number of vehicles in the target lane and within w4, w5

-50.0, 8.0

the last 20-meter zone of the road at the current step, with β1, β2

0.1, 0.2

each vehicle counted at most once. The parameters used in Optimizer

RMSProp

the algorithm are detailed in TABLE I. 

Replay Buffer Size

10000

3\) Topology set: We compared the episodic returns after RL Algorithm

Batch Size

32

Hyper Parameter

Target Update Interval

200

stable convergence of the algorithm under different topology Discount Factor γ

0.99

sets c shown in Fig. 8, across varying autonomous vehicle Learning Rate

5e-4

penetration rates, to determine the most suitable topology set for the algorithm. The results are presented in Fig. 9. The findings indicate that topology sets considering too many surrounding vehicles perform poorly, especially under high traffic B. Compared Methods

flow conditions. On one hand, larger topology sets increase To objectively evaluate the proposed method, we compare the dimensionality of the topological vectors, significantly ex-the TPE-MARL approach with state-of-the-art reinforcement panding the search space and leading to excessive exploration learning decision-making methods, including: that fails to converge to an optimal policy. On the other hand, 1\) MADQN \(Multi-Agent Deep Q-Network\): DQN is a enlarging the topology set also increases computational cost. 

simple yet effective value iteration reinforcement learning al-Therefore, we select the topology set illustrated in Fig. 9-\(a\)

gorithm. We adopt the graph neural network-integrated double-as the algorithm configuration. 

DQN method proposed in \[28\]. 

D. Evaluation Metrics

2\) Multi-Agent Proximal Policy Optimization \(MAPPO\): PPO is a policy iteration-based multi-agent reinforcement We primarily consider the following 6 evaluation metrics: learning algorithm that demonstrates strong performance on 1\) Traffic Efficiency: Quantified by measuring improve-classical challenges such as StarCraft and predator-prey sce-ments in roadway utilization and reduction of traffic delays narios. 

through average flow speed, vehicle throughput rate, or mean 3\) Multi-Agent Deep Deterministic Policy Gradient travel time. Specifically, we select Average Velocity \(Avg. 

\(MADDPG\): MADDPG is a multi-agent reinforcement learn-Vel.\) as the primary metric, defined as:

ing algorithm designed for continuous action space scenar-





T

ios, making it suitable for high-precision control tasks. This 1 X

1

X

¯

v =

vi\(t\)

, 





\(38\)

method was selected to investigate whether continuous space T

|NCAV,t|

t=0

i∈NCAV,t

Intvl.\) ¯

Tlc, mean temporal duration between consecutive lane-change actions, and Average Acceleration Jerk \(Jerk\) ¯

jac, 

denotes the rate of acceleration change, which is quantified using the following formulation, 

1 Z T da



¯

i\(t\)

j





ac =



dt, 

\(40\)

T

0



dt



where ai\(t\) denotes the acceleration of vehicle i, with its discretized form being employed in practical computations. 

Both the average lane-change interval ¯

Tlc and the average

jerk rate ¯

jac are statistically aggregated over the entire testing duration. 

4\) Velocity Variance \(Var. Velo.\)

N

1

Z

T

X 1

σ2 =

v

2 dt, 

v

i\(t\) − ¯

vi

\(41\)

N

T

i=1

0

Fig. 8. Illustration of the 3 topology sets we compared. The blue vehicle where ¯

v

is ego CAV, c

i represents the mean velocity of vehicle i over the ego includes the following quantities and types of vehicles respectively: \(a\). 2 vehicles, selecting the two CAVs with the maximum and evaluation period. 

minimum differences between their observations \(as shown in equations \(5\)-

5\) Cooperation Efficiency: Assessed by evaluating the

\(7\)\) and the ego vehicle’s observations within the coordinating zone. \(b\). 

multi-vehicle task completion rate \(Succ. Rate\) to quantify 4 vehicles, selecting the two CAVs with the maximum and the two with the minimum differences between their observations and the ego vehicle’s collaborative coordination among agents:

observations within the coordinating zone. \(c\). All other CAVs within the N

coordinating zone. 

R

success

task =

, 

\(42\)

Ntotal

Topology set \(a\)

where Nsuccess denotes the number of vehicles that successfully 60

completed cooperative tasks, and N

n

Topology set \(b\)

total represents the total

Topology set \(c\)

number of vehicles. Both quantities are statistically aggregated etur 55

over the entire testing duration. 

50

Episodic R

Traffic Topology Vector

45

v ∈

100

R

150

250

350

Flow Rate / vehicles/\(h·lane\)

Hash Encoding

H = \(h

Fig. 9. Comparison of episodic return values upon convergence of the TPE-1, ..., h64\)

QMIX method under different topology sets. The comparative experiments were conducted at 100% CAV penetration rate. 

Coordination Mapping

x = Xint , y =

Yint

where vi denotes the average velocity of the i-th vehicle 232−1

232−1

\(in km/h\), and T indicates the statistical time horizon for performance evaluation. 

Grid Density Caculting

2\) Safety: Average Minimum Time-to-Collision \(TTC\), Cij = P I\(xk ∈ ∆xi, yk ∈ ∆yj\)

defined as the mean value of the smallest collision-free time intervals recorded across all vehicles in all experimental episodes during testing. The TTC metric calculates the minimum time Topology Distribution Heatmap

required for two vehicles to collide if maintaining their current H\(Cij\)

velocities and trajectories:

T

1





X

Hi\(t\)

Fig. 10. Generating flow of topology distribution heatmap. 

TTC =

min

, 

\(39\)

T

i∈Nh,t vi\(t\) − vi \(t\)

t=0

h

6\) Policy Diversity: Having defined the traffic topology where Nh,t denotes the set of vehicles that possess a leading in Equation \(18\)-\(22\), we employ 2D heatmaps to visualize vehicle and exhibit velocities exceeding those of their respec-clustering characteristics of high-dimensional traffic patterns, tive leading vehicles. 

thereby evaluating the diversity of formalized policies. Due 3\) Decision Smoothness: Reflecting the algorithm’s perfor-to the dynamic nature of traffic scenarios, traffic topology mance in driving comfort and operational stability. Two key vectors exhibit variable dimensionality. These vectors are first metrics are employed: Average Lane-Change Interval \(LC. 

uniformly expanded to a maximum dimension v ∈

100

R

. The

Fig. 11. Training comparasion. This figure presents the comparative returns of five reinforcement learning algorithms across varying traffic flow rates \(150, 250, 350 vehicles/\(h·lane\)\) and Connected and Automated Vehicle \(CAV\) penetration rates \(25%, 50%, 75%, 100%\). It should be noted that the QMIX

and TPE-QMIX algorithms originally incorporated auxiliary intrinsic rewards during training. For equitable comparison, these supplemental rewards have been systematically excluded in our analysis. Consequently, all reward values displayed in the figure adhere to a uniform evaluation framework, consisting exclusively of environmental reward components calculated through identical computational protocols. 

SimHash algorithm is then employed to project them into a where ∆x





i = i−1 , i

and ∆y

, j

denote grid

32

32

j = j−1

32

32

64-bit hash space:

partitioning intervals, and I\(·\) represents the indicator function \(

that equals 1 when the condition · is satisfied. The topological 1

v · rk ≥ 0

h

distribution can then be effectively visualized through heatmap k =

, 

\(43\)

0

otherwise

representation, with the generation workflow illustrated in Fig. 10. 

where rk ∈ \{−1, 1\}100 denotes random projection vectors for k = 1, . . . , 64. The resultant hash code H = \(h1, . . . , h64\) E. Results

is decomposed into two 32-bit segments and subsequently transformed into normalized coordinates:

1\) Comparison of training progress: We evaluated the performance of the proposed algorithm against other reinforce-32

X

X

ment learning approaches under varying traffic flow densities int =

hi · 232−i, 

and Connected and Automated Vehicle \(CAV\) penetration i=1

64

rates. Specifically, Traffic flow density: low, moderate, and X

Y

\(44\)

high \(corresponding to 150, 250, and 350 vehicles/hour respec-int =

hj · 264−j, 

j=33

tively\), and CAV penetration rate: 25%, 50%, 75%, 100%. 



X

Y



The reward performance during algorithm training is shown \(x, y\) =

int

, 

int

∈ \[0, 1\]2. 

232 − 1

232 − 1

in Fig. 11. Different algorithms exhibit variations in convergence speed and final rewards across various testing environments. Overall, value decomposition methods demonstrate For n samples with normalized two-dimensional coordi-significant advantages in all scenarios. This is because QMIX’s nates, spatial density statistics are computed by defining grid value decomposition approach dynamically adjusts the weights cell counts as:

of different vehicle policies, avoiding performance degradation n

X

C

caused by conflicts in local policies \[reference\]. Notably, at the ij =

I \(xk ∈ ∆xi, yk ∈ ∆yj \) , 

\(45\)

same autonomous vehicle penetration rate, as traffic density k=1

Fig. 12. Topology distribution gradually increases, traditional methods show varying degrees superior performance in practical applications. 

of reward decline. Combined with the collision frequency Additionally, overall, the maximum reward value shows analysis in Fig. 13, this can be attributed to the escalating an upward trend as the autonomous vehicle penetration rate severity of local policy conflicts. 

increases. This indicates that higher autonomous vehicle penetration rates have a positive effect on improving traffic flow In terms of convergence speed, the value decomposition quality. We also observe that as traffic flow density rises, method achieves the fastest convergence in nearly all scenarios the peak reward similarly exhibits an increasing trend, which due to its centralized value function design. In contrast, is caused by the growing number of vehicles reaching their traditional DQN value iteration methods exhibit high vari-destinations. 

ance in reward values during training and poor consistency 2\) Analysis of exploration patterns: According to Section across multiple runs \(e.g., Flow Rate 150, Pene. 75%\). In

V-D-6, we visualized the policy diversity during training for some cases, policies even become unusable \(Flow Rate 250, both TPE-QMIX and GAT-MADQN methods. Specifically, Pene. 25%\), with significant fluctuations in the overall reward within the first 400,000 selected steps, we recorded traffic trend during training. As environmental dynamics intensify topologies every 4 steps. Following the flowchart of Fig. 10, 

\(increased traffic flow\), Q-learning’s off-policy nature exac-we generated the visualization shown in Fig. 12. 

erbates the coupling of state-action spaces in multi-vehicle The dynamic changes in the heatmap visually demonstrate coordination, aggravating Q-value overestimation and leading significant differences in exploration behavior between TPE-to lower rewards. For policy iteration methods like MAPPO, QMIX and GAT-MADQN. The yellow high-visitation regions overall performance is slightly inferior to value decomposition of TPE-QMIX exhibit rapid expansion characteristics as train-approaches. While the algorithm generally converges stably to ing progresses from 20% to 100% completion. In the early locally optimal policies in most cases, its exploration strategy stages, due to the relatively large absolute value of the r lacks physics-informed optimization, resulting in multi-phase vis

reward term, the algorithm encourages the multi-agent system learning phenomena \(particularly noticeable at Pene. 75% and to explore as many states as possible. At 20% and 40% training 100%\). This indicates susceptibility to local optima under progress, no distinct hotspots were formed, with exploration strong interaction conditions. 

extending through large state spaces at an approximately The benefits of topology enhancement are particularly pro-uniform rate. After 60% training progress, hotspots gradually nounced in strongly interactive scenarios. Analyzing the differ-emerged. This expansive exploration pattern indicates that ences between QMIX and TPE methods along the traffic flow the topology enhancement mechanism can guide agents to dimension reveals that TPE’s advantages become increasingly systematically investigate adjacent or topologically related evident as traffic flow grows. Similarly, with higher penetration unknown regions based on already explored areas. 

rates, TPE’s reward values gradually demonstrate greater supe-In contrast, the heatmap of GAT-MADQN exhibits dis-riority compared to QMIX. Topology enhancement preserves tinctly different characteristics. Several hotspots emerge as the fundamental framework of value decomposition methods early as 20% progress, but their spatial distribution shows no while improving algorithmic interpretability through the incor-significant expansion or change during subsequent training, poration of physical node relationships. Compared to graph remaining concentrated in initial core regions even at 100%

neural networks’ simple adjacency-based node information completion. This pattern likely stems from the graph attention processing, the game topology integration approach delivers network’s excessive focus on critical states, causing explo-

Fig. 13. Test evaluation metrics. The figure presents the performance metrics of five reinforcement learning algorithms in test cases under different traffic flow rates \(150, 250, 350 vehicles/\(h·lane\)\) and varying autonomous vehicle penetration rates \(25%, 50%, 75%, 100%\). 

ration incentives to gradually diminish during policy updates mechanism, underperforms compared to TPE and QMIX in and posing a risk of convergence to local optima. 

most test scenarios in terms of Succ. Rate and Avg.Velo.. 

The evolution of the heatmaps further reflects the dynamic At low penetration rates \(especially under low traffic flow adjustment capabilities of the two algorithms’ exploration conditions\), it often exhibits higher Min. HW., reflecting more strategies. TPE-QMIX continues to access new grid cells conservative or less coordinated behavior among agents. This even at 80% progress, demonstrating sustained policy explo-observation suggests that, in the current application context, ration capability. In contrast, GAT-MADQN shows stagnating graph neural networks may be less effective than value decom-exploration of new regions after 60% progress, suggesting position strategies in perceiving global traffic conditions. How-potential design flaws in its exploration-exploitation balancing ever, it is noteworthy that MADQN occasionally records the mechanism. 

lowest Jerk values under high traffic flow and high penetration 3\) Analysis of macroscopic traffic flow statistical data: rates, likely due to the overall degradation of autonomous Statistical data is shown in Fig. 13. We present performance driving strategies in high-density traffic, which may indicate metric statistics for each algorithm during continuous deploy-potential failure modes of the MADQN algorithm. 

ment over 5 hours \(1000 episodes\) in the simulation scenario. 

The MADDPG algorithm’s overall performance falls be-The TPE-QMIX algorithm demonstrates significant advan-tween MADQN and QMIX/TPE. While it outperforms tages across all traffic flow density conditions. This superiority MADQN in some aspects of success rate and average velocity, is particularly evident in the metrics of Avg.Velo. and Succ. 

it does not reach the levels achieved by QMIX or TPE. Its Rate. Regardless of penetration rate or traffic flow variations, performance across metrics is moderate, with no standout TPE consistently achieves the highest success rate, indicating strengths or weaknesses compared to the leading algorithms. 

its enhanced capability to handle complex traffic scenarios. 

The longitudinal action space of MADDPG is continuous The TPE method also maintains higher Avg.Velo. and longer \(ranging between maximum/minimum acceleration\), theoret-LC. Itv. \(especially as penetration rates increase\), suggesting ically enabling finer control. However, in testing, MAD-that its topology-enhanced mechanism provides agents with DPG does not consistently demonstrate superior smoothness a more comprehensive understanding of the environment, in all low-density conditions. Although its Jerk values are enabling more efficient coordination in speed regulation and acceptable, they are not always optimal compared to other path selection, thereby leading to smoother and more stable algorithms. This may be because the reward function does overall traffic flow. As the back-bone framework for TPE, not explicitly guide agents to optimize action smoothness, the QMIX algorithm delivers robust performance, typically preventing the algorithm from fully realizing its potential. 

ranking second in both success rate and average velocity, As traffic flow density increases from 150 to 350

highlighting the advantages of its value decomposition method veh/\(hour·lane\), the following trends emerge: due to increased in multi-vehicle cooperative decision-making. 

congestion, Avg.Velo. generally declines; Succ. Rate de-The MADQN algorithm, which employs a graph attention creases overall \(particularly for MADDPG and MADQN\), 

though TPE maintains its lead even under high traffic flow follow HDV 2 until making a right turn. If the speed is too \(despite some performance degradation\); and Min. HW. val-high at this point, it might alternatively opt to decelerate and ues decrease or approach critical thresholds as density rises, change lanes between HDV 2 and HDV 3 . The TPE-MARL

reflecting the shrinking available space between vehicles. 

agent, however, chooses to maintain high-speed driving and changes lanes ahead of HDV 3 , thereby ensuring both driving efficiency and task completion. In fact, the TPE-MARL agent predominantly selects routes with maximum acceleration or high-speed driving space ahead in most scenarios. This also explains the high average speed of TPE-MARL observed in Fig. 13. The corresponding space-time diagram is shown in Fig. 15. To avoid the complexity and visual occlusion inherent in three-dimensional \(3D\) multi-lane representations, we adopt a two-dimensional \(2D\) visualization method. In this diagram, for any given time t, the horizontal axis represents the longitudinal position across all four lanes. Specifically, each lane is mapped to a distinct, adjacent segment on the axis, allowing for simultaneous visualization of traffic states in all lanes. 

Fig. 14. Typical intelligent vehicle behaviors from a microscopic perspective. 

4\) Microscopic vehicle behavior analysis: First, for each scenario, we observed the complete operational process through video recordings. In the initial road segment, we noted frequent lane-changing behaviors by CAVs. Analysis indicates this occurs because during the initial phase, vehicle dynamics undergo significant changes, and newly entering vehicles appear within the CAVs’ observation range. This leads to drastic fluctuations in the dynamic topological relationships between vehicles, consequently triggering frequent action changes \(which could be one direction for algorithm optimization\). This phenomenon does not occur in the latter Fig. 16. The space-time trajectory diagram for the traffic flow in case \(b\). 

half of the road section because, at this stage, vehicle rewards Scenario setting for this case: Flow rate: 250 vehicles/\(h·lane\), Penetration: 75%. 

are primarily governed by position rewards \(Equation \(14\)\)

and intention rewards \(as described in Section V-C\). Thus, In Fig. 14, case \(b\), CAV 1 intends to change lanes to the they are less affected by topological variations, resulting in right, with the target lane being the rightmost lane. CAV 2

more stable actions. 

aims to proceed straight, and both middle lanes are available Additionally, we observed intelligent vehicle behaviors in for passage. Since the right lane is occupied by the low-speed certain challenging scenarios, as illustrated in Fig. 14. 

HDV 3 , if CAV 1 were to decelerate and change lanes to follow HDV 3 , it would significantly reduce efficiency. In this scenario, the TPE-MARL agent CAV 2 opts to change lanes to the right, while CAV 1 accelerates to overtake, successfully merging into the right lane. This case demonstrates that TPEMARL agents possess the capability for cooperative driving and exhibit a clear understanding of road conditions and the characteristics of surrounding vehicles. The corresponding space-time diagram is shown in Fig. 16. 

VI. CONCLUSION

This paper proposes a topology-enhanced multi-agent reinforcement learning method for cooperative multi-vehicle decision-making. We developed a traffic topology construction Fig. 15. The space-time trajectory diagram for the traffic flow in case \(a\). 

method that reduces the high-dimensional traffic state space Scenario setting for this case: Flow rate: 350 vehicles/\(h·lane\), Penetration: to a manageable feature space, significantly improving the 50%. 

performance of cooperative driving strategy exploration. Using In Fig. 14, case \(a\), CAV 1 has an intention to turn right. 

QMIX as the backbone reinforcement learning framework, we During interactions with HDV 2 and HDV 3 , it would deeply integrated traffic topology information with state repre-typically choose to decelerate and change lanes rightward, then sentation and reward functions in QMIX through visit counts

and variational autoencoders, constructing a multi-agent re-

\[8\] C. S., W. M., S. W., Y. Y., and F. M., “Multi-agent reinforcement inforcement learning decision architecture that fully utilizes learning-based decision making for twin-vehicles cooperative driving in stochastic dynamic highway environments,” IEEE Transactions on CAV node features and traffic flow topological characteristics. 

Vehicular Technology, vol. 72, no. 10, pp. 12 615–12 627, 2023, iEEE

Compared with mainstream reinforcement learning algorithms, Transactions on Vehicular Technology. 

extensive simulation experiments were conducted under differ-

\[9\] S. Chen, J. Dong, P. Y. J. Ha, Y. Li, and S. Labi, “Graph neural network and reinforcement learning for multi-agent cooperative control of con-ent traffic densities and CAV penetration rates, with in-depth nected autonomous vehicles,” Computer-Aided Civil and Infrastructure analysis of algorithm performance from multiple perspectives: Engineering, vol. 36, no. 7, pp. 838–857, 2021, computer-Aided Civil metric training processes, exploration patterns, macroscopic and Infrastructure Engineering 2025/04/29. 

\[10\] X. B., L. R., W. F., P. C., W. J., Z. Z., and Z. H., “Stochastic graph neural traffic flow performance statistics, and microscopic vehicle network-based value decomposition for marl in internet of vehicles,” 

behaviors. The analysis demonstrates that our proposed multi-IEEE Transactions on Vehicular Technology, vol. 73, no. 2, pp. 1582–

agent reinforcement learning algorithm effectively balances 1596, 2024, iEEE Transactions on Vehicular Technology. 

exploration and exploitation, exhibiting outstanding perfor-

\[11\] C. Y., H. X., G. H., Y. Y. W., and L. C., “Transformer-based multi-agent reinforcement learning for generalization of heterogeneous multi-robot mance in efficiency, safety, decision smoothness, and task cooperation,” in 2024 IEEE/RSJ International Conference on Intelligent completion rates. The algorithm shows rationality surpassing Robots and Systems \(IROS\), ser. 2024 IEEE/RSJ International Con-human drivers in both mixed autonomy traffic flows and fully ference on Intelligent Robots and Systems \(IROS\), 2024, pp. 13 695–

13 702. 

autonomous traffic flows. 

\[12\] F. W., L. Y., Y. Z., and L. Q., “Decision making for autonomous Our work has limitations. While the simhash encoding driving via multimodal transformer and deep reinforcement learning,” 

method can distinguish the exploration capabilities of different in 2022 IEEE International Conference on Real-time Computing and Robotics \(RCAR\), ser. 2022 IEEE International Conference on Real-time algorithms regarding traffic state topology, Fig. 12 reveals that Computing and Robotics \(RCAR\), 2022, pp. 481–486. 

certain areas in the heatmap are unreachable by vehicles. This

\[13\] H. Y., Z. L., M. D., H. X., and L. Y., “Spformer: A transformer based indicates that the topological representation can be further drl decision making method for connected automated vehicles,” in 2024

IEEE 27th International Conference on Intelligent Transportation Sys-improved. In terms of experimental setup, this paper conducted tems \(ITSC\), ser. 2024 IEEE 27th International Conference on Intelligent simulation experiments in a simple mixed traffic flow scenario Transportation Systems \(ITSC\), 2024, pp. 1223–1230. 

to preliminarily explore the potential of the TPE-MARL

\[14\] Y. Y., P. L., S. T., W. J., P. D., C. D., and Y. G., “A multi-vehicle game-theoretic framework for decision making and planning of autonomous algorithm for cooperative multi-vehicle decision-making. The vehicles in mixed traffic,” IEEE Transactions on Intelligent Vehicles, experiments employed homogeneous HDV and CAV models, vol. 8, no. 11, pp. 4572–4587, 2023, iEEE Transactions on Intelligent which still differ from real-world traffic scenarios. Natural Vehicles. 

driving vehicles in actual traffic flows exhibit more diverse and

\[15\] F. Sana, N. L. Azad, and K. Raahemifar, “Autonomous vehicle decision-making and control in complex and unconventional scenarios—a re-uncertain behavioral characteristics, posing significant chal-view,” 2023-01-01 2023. 

lenges for reinforcement learning based MVDM algorithms. 

\[16\] A. J. M. Muzahid, S. F. Kamarulzaman, M. A. Rahman, S. A. Murad, Future directions include further rationalization of traffic M. A. S. Kamal, and A. H. Alenezi, “Multiple vehicle cooperation and collision avoidance in automated vehicles: survey and an ai-enabled topology representation, where works in pattern recognition conceptual framework,” Scientific Reports, vol. 13, no. 1, p. 603, 2023. 

may provide potential approaches. Further refinement of world

\[17\] A. Skrynnik, A. Andreychuk, M. Nesterova, K. Yakovlev, and A. Panov, models and agent models remains necessary to better align

“Learn to follow: Decentralized lifelong multi-agent pathfinding via planning and learning,” Proceedings of the AAAI Conference on Artificial with real-world traffic scenarios. 

Intelligence, vol. 38, no. 16, pp. 17 541–17 549, 2024, aAAI 2025/04/29. 

\[18\] Y. Han, L. Zhang, D. Meng, X. Hu, and S. Weng, “A value based REFERENCES

parallel update mcts method for multi-agent cooperative decision making of connected and automated vehicles,” arXiv preprint arXiv:2409.13783, 

\[1\] N. Goulet and B. Ayalew, “Distributed maneuver planning with con-2024. 

nected and automated vehicles for boosting traffic efficiency,” IEEE

Transactions on Intelligent Transportation Systems, vol. 23, no. 8, pp. 

\[19\] M. Treiber, A. Hennecke, and D. Helbing, “Congested traffic 10 887–10 901, 2022. 

states in empirical observations and microscopic simulations,” Phys. 

\[2\] S. Edwards, G. Hill, P. Goodman, P. Blythe, P. Mitchell, and Y. Huebner, Rev. E, vol. 62, pp. 1805–1824, Aug 2000. \[Online\]. Available:

“Quantifying the impact of a real world cooperative-its deployment

https://link.aps.org/doi/10.1103/PhysRevE.62.1805

across multiple cities,” Transportation Research Part A: Policy and

\[20\] J. Erdmann, “Sumo’s lane-changing model,” in Modeling Mobility with Practice, vol. 115, pp. 102–113, 2018. 

Open Data: 2nd SUMO Conference 2014 Berlin, Germany, May 15-16, 

\[3\] X. Wang, L. Lu, Z. Zhang, Y. Wang, and H. Li, “Introducing the vehicle-2014, ser. Modeling Mobility with Open Data: 2nd SUMO Conference infrastructure cooperative control system by quantifying the benefits for 2014 Berlin, Germany, May 15-16, 2014. Springer, 2015, pp. 105–123. 

the scenario of signalized intersections,” Transportation Research Part

\[21\] Y. Han, L. Zhang, and D. Meng, “A differentiated reward method for A: Policy and Practice, vol. 192, p. 104378, 2025. 

reinforcement learning based multi-vehicle cooperative decision-making

\[4\] M. Hua, D. Chen, X. Qi, K. Jiang, Z. E. Liu, Q. Zhou, and H. Xu, “Multi-algorithms,” 2025. \[Online\]. Available: https://arxiv.org/abs/2502.00352

agent reinforcement learning for connected and automated vehicles

\[22\] T. Rashid, M. Samvelyan, C. S. de Witt, G. Farquhar, J. Foerster, and control: Recent advancements and future prospects,” arXiv preprint S. Whiteson, “Monotonic value function factorisation for deep multi-arXiv:2312.11084, 2023. 

agent reinforcement learning,” Journal of Machine Learning Research, 

\[5\] J. Dinneweth, A. Boubezoul, R. Mandiau, and S. Espié, “Multi-agent vol. 21, no. 178, pp. 1–51, 2020. 

reinforcement learning for autonomous vehicles: a survey,” Autonomous

\[23\] H. Tang, R. Houthooft, D. Foote, A. Stooke, O. Xi Chen, Y. Duan, Intelligent Systems, vol. 2, no. 1, p. 27, 2022. 

J. Schulman, F. DeTurck, and P. Abbeel, “Hash exploration: A study of

\[6\] H. E., K. D., and R. A., “Decision-making strategy using multi-count-based exploration for deep reinforcement learning,” Advances in agent reinforcement learning for platoon formation in agreement-seeking neural information processing systems, vol. 30, 2017. 

cooperation,” in 2023 IEEE Intelligent Vehicles Symposium \(IV\), ser. 

\[24\] L. Kocsis and C. Szepesvári, “Bandit based monte-carlo planning,” in 2023 IEEE Intelligent Vehicles Symposium \(IV\), 2023, pp. 1–6. 

European conference on machine learning. 

Springer, 2006, pp. 282–

\[7\] L. J., H. P., N. X., H. C., and S. J., “Cooperative decision-making for 293. 

cavs at unsignalized intersections: A marl approach with attention and

\[25\] F. Agakov and D. Barber, “Variational information maximization for hierarchical game priors,” IEEE Transactions on Intelligent Transporta-neural coding,” in Neural Information Processing, N. R. Pal, N. Kasabov, tion Systems, vol. 26, no. 1, pp. 443–456, 2025, iEEE Transactions on R. K. Mudi, S. Pal, and S. K. Parui, Eds. Berlin, Heidelberg: Springer Intelligent Transportation Systems. 

Berlin Heidelberg, 2004, pp. 543–548. 

\[26\] C. Li, T. Wang, C. Wu, Q. Zhao, J. Yang, and C. Zhang, “Celebrating diversity in shared multi-agent reinforcement learning,” Advances in Neural Information Processing Systems, vol. 34, pp. 3991–4002, 2021. 

\[27\] C. Wu, A. Kreidieh, K. Parvate, E. Vinitsky, A. M. Bayen, et al., 

“Flow: Architecture and benchmarking for reinforcement learning in traffic control,” arXiv preprint arXiv:1710.05465, vol. 10, 2017. 

\[28\] Q. Liu, Z. Li, X. Li, J. Wu, and S. Yuan, “Graph convolution-based deep reinforcement learning for multi-agent decision-making in interactive traffic scenarios,” in 2022 IEEE 25th International Conference on Intelligent Transportation Systems \(ITSC\), 2022, pp. 4074–4081. 


# Document Outline

+ Introduction 
+ Related Works 
+ Problem Formulation  
	+ Partially Observable Markov Decision Process 
	+ Continuous Traffic Flow Settings 
	+ World Model 
	+ Observation 
	+ Action Space 
	+ Reward Function 
	+ CTDE and QMIX 

+ Methodology  
	+ Construction of Dynamic Traffic Topology 
	+ Game Topology Enhanced Reward Function 

+ Case study  
	+ Case Settings 
	+ Compared Methods 
	+ Implementation Details  
		+ Observation 
		+ Reward funcion 
		+ Topology set 

	+ Evaluation Metrics 
	+ Results  
		+ Comparison of training progress 
		+ Analysis of exploration patterns 
		+ Analysis of macroscopic traffic flow statistical data 
		+ Microscopic vehicle behavior analysis 


+ Conclusion 
+ References



