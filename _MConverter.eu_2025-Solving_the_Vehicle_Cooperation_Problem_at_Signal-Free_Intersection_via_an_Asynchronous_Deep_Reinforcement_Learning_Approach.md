IEEE INTERNET OF THINGS JOURNAL, VOL. 12, NO. 13, 1 JULY 2025

23357

Solving the Vehicle Cooperation Problem at

Signal-Free Intersection via an Asynchronous

Deep Reinforcement Learning Approach

Shuai Wang , Yuhao Ding , Xiaoqi Ding , and Xiaojun Tan ,  *Senior Member, IEEE*

***Abstract*****—With the rapid development of modern intelli-I. INTRODUCTION**
** 
gent transportation systems, connected and automated vehicles \(CAVs\) have garnered significant attention due to their advanced THE RAPID advancement of connected and automated communication and decision-making capabilities. Intelligent col-vehicle \(CAV\) technology has propelled vehicle coop-laborative decision-making in dynamic traffic scenarios poses eration in dynamic traffic scenarios to an essential research significant challenges in the research of CAV technology. 
**
**frontier within the autonomous driving domain \[1\]. The col-Strategies and methods have been developed to tackle the** laborative management of signal-free intersections represents **collaboration problem toward different scenarios. However, most** significance for CAVs in urban traffic. Intersections without **existing studies have not been fully investigated the performance** **optimization and practicability of the vehicle collaboration** traffic lights have become a critical challenge in modern **at signal-free intersections. Meanwhile, the urban signal-free** intelligent transportation systems \(ITSs\) as the number of **intersections represent a critical application scenario for vehicle** vehicles continues to increase \[2\], \[3\]. In the United States **cooperation, where a thorough study has not been given yet. **

and Europe, over 30% of traffic jams and accidents occur **Therefore, this study intends to solve the vehicle collaboration** at signal-free intersections \[4\], \[5\]. Therefore, it is crucial to **problem utilizing the deep reinforcement learning approach. **

**Initially, the problem is formulated as an elaborated Markov** design an effective signal-free intersection cooperation system **decision process, comprising the state space, the action space, and** to enhance traffic throughput and ensure driving safety. 

**the reward function. Then, a shared advantage actor–critic \(A2C\)** Advances in vehicle-to-infrastructure \(V2I\) technologies **model is proposed to effectively extract temporal and spatial** have mitigated communication constraints \[6\], \[7\], rendering **features through the shared network, thereby improving the** multivehicle collaboration feasible in the intersection man-consistency of feature learning processes between the Actor and **Critic networks. Furthermore, the asynchronous training strategy** agement. It is considered practical for vehicles to cooperate **employed in this study involves multiple training processes** efficiently under the coordination of a centralized system **concurrently, thereby enhancing the model’s convergence speed** deployed along the roadside \[8\], \[9\]. Vehicles can share their **and stability. Finally, the effectiveness of the proposed method** driving states and intentions with the central coordinator. 

**is verified in two typical intersection scenarios. Simulation** Such coordinator can then direct the vehicles to leave the **results reveal that our method exhibits competitive performance** **compared with existing approaches, and an improvement up** intersection safely according to an effective collaborative algo-to 30% and 40% can be achieved in the retreat time and the rithm, thereby optimizing the management of the intersection. 

**averaged delay time. Additionally, the field experiments have** In recent years, significant research efforts have been **been conducted on a miniaturized autonomous driving platform,** expended on addressing the challenges of coordinating with **verifying the considerable potential of the proposed method for** vehicles at intersections \[10\]. These challenges have been for-real-world applications. 

mulated as optimization and game theory problems, employing

***Index Terms*****—Connected and automated vehicles \(CAVs\), deep** optimization techniques to derive vehicle control strategies that **reinforcement learning \(DRL\), miniaturized autonomous driving** achieve a global Nash equilibrium by modeling vehicle inter-platform, signal-free intersections, vehicle cooperation. 

actions \[11\]. Additionally, some researchers have considered the graph theory to graphically model the vehicle road network and facilitate the cooperative decision-making of vehicles Received 5 September 2024; revised 15 December 2024, 9 January 2025, through the analysis and processing of these graphs \[12\]. 

and 18 February 2025; accepted 12 March 2025. Date of publication 18 March 2025; date of current version 27 June 2025. This work was Deep reinforcement learning \(DRL\) methods \[13\], \[14\] have supported in part by the Guangdong Basic and Applied Basic Research been demonstrated to be with efficient learning ability and Foundation under Grant 2024A1515010238; in part by the Shenzhen Science distinct flexible decision-making capability. By learning from and Technology Program under Grant KJZD20231023100204008; and in part by the National Natural Science Foundation of China under Grant 62203477. 

the agent’s interactions with the environment, the coordinator *\(Corresponding author: Xiaojun Tan.\)*

can train effective strategies to guide the vehicle through Shuai Wang, Yuhao Ding, and Xiaojun Tan are with the School of Intelligent collaborative tasks. However, among the existing methods, the Systems Engineering, Sun Yat-sen Univerity \(Shenzhen\), Shenzhen 518107, China \(e-mail: wangsh368@mail.sysu.edu.cn; dingyh26@mail2.sysu.edu.cn; practicality and high performance in intersection management tanxj@mail.sysu.edu.cn\). 

remain a significant challenge. Some methods may struggle Xiaoqi Ding is with the School of Computer Science and Engineering, to provide real-time solutions under complex intersection Sun Yat-sen Univerity \(Guangzhou\), Guangzhou 510000, China \(e-mail: dingxq7@mail2.sysu.edu.cn\). 

environments, while others have performance improvement Digital Object Identifier 10.1109/JIOT.2025.3552058

potential. 

2327-4662 c

2025 IEEE. All rights reserved, including rights for text and data mining, and training of artificial intelligence and similar technologies. Personal use is permitted, but republication/redistribution requires IEEE permission. 

See https://www.ieee.org/publications/rights/index.html for more information. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:40:07 UTC from IEEE Xplore. Restrictions apply. 

23358

IEEE INTERNET OF THINGS JOURNAL, VOL. 12, NO. 13, 1 JULY 2025

Given the aforementioned limitations of existing methods, II. RELATED WORK

this study introduces a DRL approach to enable multive-In the modern ITSs, multivehicle cooperative driving hicle interconnection coordination at intersections. We first enhances the intelligence, safety, and efficiency of traffic man-introduce a hierarchical coordination framework that segments agement \[6\], \[10\], \[15\]. Consequently, the extensive research continuous traffic flow into distinct batches of vehicles. For has focused on developing vehicle coordination strategies for each batch, the cooperation problem is formulated as a various typical collaborative driving scenarios. 

Markov decision process, with a customized state space, action space, and reward function. Subsequently, a shared *A. Methods Based on Optimization or Game Theory* advantage actor–critic \(A2C\) network model is employed to In traffic management, vehicle cooperation problems are effectively learn and extract environmental features through initially modeled as the optimization or game theory problems. 

the shared network architecture. Furthermore, an asynchronous Zhao et al. \[16\] transformed the cooperation problem at training strategy is developed to enhance the speed and signal-free intersections into a multiobjective optimization stability of model training. The simulation results demonstrate problem and developed a privacy policy based on affine that the proposed method significantly reduces retreat time masking to safeguard data privacy. An integrated-oriented and averaged delay time by 30% and 40%, respectively. 

two-layer framework was developed by Li et al. \[8\]. This Field experiments conducted on a miniaturized autonomous framework transformed the intersection coordination problem driving platform further validate our proposed method’s appli-into a sequential linear programming problem and proposed cation potential and practical value in real-world scenarios. 

a low-complexity optimization scheme. Ji et al. \[17\] modeled Additionally, the limitations of communication delay factors and evaluated the aggression of interactive vehicles during on the actual deployment of our method are tested and overtaking tasks and proposed an adaptive decision-making analyzed in detail. 

strategy for overtaking based on game theory. To achieve The contributions of this article are as follows. 

the optimal overtaking strategy in the dynamic environment, 1\) In terms of the problem representative approach. 

Gong et al. \[18\] proposed a game theory algorithm based on an Considering the practical challenges of urban signal-free interactive behavior model to calculate safe overtaking timing intersections, this study proposes a novel paradigm for and reasonable overtaking methods. In the on-ramp merging the intersection vehicle coordination problem, modeling scenario, Yang et al. \[19\] proposed a multivehicle cooperative it as a Markov decision model. The DRL frame-strategy based on cooperative game theory, which considered work is employed, and effective state representations the cost functions of multiple driving factors to determine the are developed for the intersection environment, vehicle optimal confluence sequence of vehicles in different lanes. 

action representations, and reward functions to guide the vehicles’ decision-making. 

*B. Methods Based on Graph Theory*

2\) In terms of the training strategy. To address the performance limitations of existing methods, this study The graph theory effectively represents the communication introduces an elaborate parameter sharing A2C model and interaction relationships between vehicles, leading to the to improve the consistency and effectiveness of feature recent application of graph-based methods in vehicle cooper-learning. The asynchronous training strategy is also ation. Chen et al. \[20\] decomposed the intersection vehicle employed to expand the exploration of the environment, cooperation problem into an optimal sequence determination accelerating the training process. With these strategies, problem, and proposed IDFST method and MCC method the overall performance of the model can be enhanced through optimizing the ergodic search method. Li et al. \[21\]

dramatically. 

divided the intersection area into multiple subareas and 3\) In terms of the test scene. Numerical experiments have developed a heuristic search algorithm based on conflict been conducted to validate that our proposed method can graphs. Shi et al. \[22\] represented the vehicle information for significantly reduce the retreat time and averaged delay on-ramp vehicles and trunk vehicles engaged in collaborative time at signal-free intersections with less computation lane changing within an information space. They introduced a time. Additionally, field experiments have also been dynamic conflict graph and a heuristic search strategy to derive involved to verify the practical applicability under real-the optimal control strategy. Shi et al. \[23\] proposed a vehicle world scenarios. The robustness of our method against final state phase diagram model with flexible junction points specific communication delays has been verified across for ramp convergence. They incorporated heuristic pruning various scenarios. A competitive solver can be offered to rules and rolling time domain optimization methods into the decision-makers to address traffic jams and intersection depth-first search strategy to enhance overall traffic efficiency managements. 

and reduce vehicle delays. 

The remainder of this article is organized as follows. 

Section II reviews and summarizes the related work. 

*C. Methods Based on Deep Reinforcement Learning* Section III is the problem statement. In Section IV, our DRL methods can continuously learn and optimize proposed method is introduced in detail. The simulation results strategies through interactions with the environment, demon-are presented in Section V. Section VI demonstrates the field strating strong adaptive learning capabilities and robustness. 

experiments deployed on the miniaturized autonomous driving Consequently, it has emerged as a prominent research direc-platform. Section VII summarizes this article. 

tion in vehicle cooperation. Guan et al. \[24\] introduced a Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:40:07 UTC from IEEE Xplore. Restrictions apply. 





WANG et al.: SOLVING THE VEHICLE COOPERATION PROBLEM AT SIGNAL-FREE INTERSECTION

23359

graph-based methods offer efficient computing and processing capability, but the simplification of vehicle interaction results in the redundancy of traffic resources and reducing cooperative efficiency. The DRL methods offer several advantages, including adaptability, real-time performance, and enhanced decision accuracy. However, the application of them in the context of intersection management has not been thoroughly explored and demonstrated. A rational and efficient vehicle cooperation strategy for signal-free intersections remains to be addressed. 

Conflict Zone

III. PROBLEM STATEMENT

Preparatory Zone

*A. Signal-Free Intersection Scene*

Vehicle \(First Batch\)

Fig. 1 presents a typical signal-free intersection scenario, Vehicle \(Other Batches\)

which can be divided into preparatory and conflict zones. 

According to the assumption made without loss of general-Central Coordinator

ity \[25\], the preparatory zone is defined as the driving area within a ring with an outer radius of 100 m and an inner Fig. 1. 

Typical signal-free intersection scenario. 

radius of 15 m. The conflict zone is defined as the driving area prior model into the proximal policy optimization \(PPO\) within a circle with a radius of 15 m. Within the preparatory algorithm within the intersection scenario, which acceler-zone, vehicles approach the intersection by driving along lanes ated the training process and enhanced sample efficiency. 

in different directions, ultimately converging into the central Luo et al. \[25\] developed a unified collaborative trajectory conflict zone. In the conflict zone, there are 12 reference planning framework aimed at maximizing traffic throughput. 

driving routes that are spatially blended relative to each They implemented a centralized coordinator based on the twin other. Vehicles engage in continuous and complex interactions delayed deep deterministic policy gradient \(TD3\) algorithm until they leave the zone. Simultaneously, a roadside central for model training. Guo et al. \[26\] combined the vehicle coordinator is deployed near the intersection to assist in conflict graph with DRL to guide CAVs through intersections the collaborative driving of vehicles. According to the V2I efficiently and safely by employing a heuristic action mask. 

communication standard, the optimal communication range Peng et al. \[27\] applied PPO method to optimize traffic between the central coordinator and vehicles is between 300

flow and enhance traffic efficiency at the 8-shaped uncon-and 500 m \[35\], which is sufficient to cover the entire trolled intersection through a leader-follow driving mode. 

intersection area. 

Wu et al. \[28\] combined the artificial potential field with In the decision-making problem at signal-free intersections, the TD3 algorithm to develop a DRL method based on the primary challenge lies in facilitating effective cooperation risk perception in vehicle overtaking and lane change tasks, among vehicles with conflicting routes within the conflict area. 

aiming to reduce the potential driving risks. To enhance To facilitate the analysis, the following assumptions are made the overall efficiency of vehicle collaborative overtaking, without loss of generality \[36\]. 

Qian et al. \[29\] employed a parameterized dueling *Q*-network 1\) In order to ensure the driving safety, overtaking, lane algorithm to learn vehicle driving strategies and designs a change and U-turn of vehicles in the preparatory zone dynamic event-triggering mechanism based on multiple cri-are prohibited. 

teria and confidence intervals. Chen et al. \[30\] developed 2\) In the conflict zone, vehicles are expected to adhere to an efficient and scalable DRL framework for the on-ramp pe-defined driving routes. 

converging task, incorporating parameter sharing and a local 3\) Vehicles and the central coordinator are equipped with reward mechanism to enhance cooperation among vehicles. 

communication systems that yield low-delay and zero-Zhang et al. \[31\] proposed an independent PPO \(IPPO\) packet-loss conditions. Vehicles can share their driving method, significantly improving the decision success rate of state—including speed, position, and driving route—

CAVs in the on-ramp converging task. 

with the central coordinator in real-time. In turn, the In general, research on vehicle cooperation plays a coordinator can broadcast the calculation results to the crucial role in the development of modern ITSs. Signal-vehicles in a timely manner. 

free intersections are a critical component of urban traffic Although favorable communication conditions are assumed networks. The study of collaborative strategies for signal-free in the assumptions, the robustness of the proposed method intersections will facilitate the application and popularization to communication delays is discussed in the experimental of CAV technology, significantly enhancing the intelligence of sections. 

urban traffic systems \[32\], \[33\], \[34\]. In the existing literature, while methods based on optimization and game theory can *B. Vehicle Model*

achieve detailed vehicle interaction modeling, they exhibit In order to improve the confidence of the scene, the significant drawbacks, including low computational efficiency employed vehicle model is the bicycle kinematics model, as and poor real-time performance in complex scenarios. The depicted in Fig. 2. The bicycle model is extensively utilized in Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:40:07 UTC from IEEE Xplore. Restrictions apply. 

23360

IEEE INTERNET OF THINGS JOURNAL, VOL. 12, NO. 13, 1 JULY 2025

TABLE I

SCENE AND CONTROLLER PARAMETERS IN SIMULATION EXPERIMENTS

Route

TABLE II

PROPOSED METHOD PARAMETERS

Preview Point

\(

\)

Fig. 2. 

Bicycle kinematics model. 

research on vehicle cooperative strategies \[37\], \[38\], \[39\], \[40\]

due to its robust physical interpretability and computational efficiency \[41\], which effectively enhance training efficiency TABLE III

and improve the stability of strategies. The state vector of the PPO METHOD PARAMETERS

vehicle is defined as \[ *x, y, θ, v*\] *T *, and the control vector is

\[ *a, δ*\] *T *. The state transition equation is given as follows:

⎡ ⎤

⎡ ⎤ ⎡

⎤

˙ *x*

*x*

cos *\(θ\)*

⎢

⎢˙ *y*⎥

⎢ *y*⎥ ⎢ sin *\(θ\) *⎥

⎣ ⎥

⎢ ⎥ ⎢

⎥

˙ *θ*⎦ = ⎣ *θ*⎦ \+ ⎣tan *\(δ\)/L*⎦ *v* *t* \(1\)

˙ *v*

*v*

*a/v*

where *x * and *y * represent the position of the vehicle, *θ * and *v* denote the heading angle and velocity, *a * and *δ * represent the vertical acceleration and the lateral steering angle, *L * indicates the longitudinal axis length of the model. 

According to assumption 2, vehicles are designed to follow where *α\(t\) * represents the angle between the preview point and the predetermined routes. To achieve precise lateral control, *δ*

the vehicle body, *ld * indicates the previewing distance. 

is calculated by the classic pure pursuit algorithm, which is To enhance the realism of the model, the critical factors frequently integrated with the bicycle model to ensure efficient affecting vehicle dynamics are also considered, and the fol-and smooth path following in autonomous driving \[42\], \[43\]. 

lowing dynamic constraints are incorporated. The relevant As illustrated in Fig. 2, the target route is discrete into a series parameter descriptions are provided in Tables I and VII

of points. At each time step, the preview point on the trajectory

⎧

is determined based on the vehicle’s current position and the

⎪

⎪

⎨ 0 ≤ *v *≤ *v* max

previewing distance. Subsequently, the required steering angle *δ* min ≤ *δ *≤ *δ* max

\(3\)

is calculated using the angle deviation and distance deviation, 

⎪

⎪

⎩ *a* min ≤ *a *≤ *a* max

enabling the vehicle to accurately track the target path. The *δ* min ≤ *δ *≤ *δ* max *. *

calculation formula is as follows:





Since communication delays are inevitable in real-world *δ\(*

2Lsin *\(α\(t\)\)*

scenarios, a redundancy mechanism is introduced to mitigate *t\) *= tan−1

\(2\)

*l*

the negative effects as much as possible. Specifically, in *d*

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:40:07 UTC from IEEE Xplore. Restrictions apply. 

WANG et al.: SOLVING THE VEHICLE COOPERATION PROBLEM AT SIGNAL-FREE INTERSECTION

23361

TABLE IV

STATISTICAL RESULTS OF ANOVA

TABLE V

OBB with Safety Redundancy

COMPUTATIONAL TIME OF TESTED METHODS

OBB Projection

preparatory area to the conflict area, need to stop in front of The axis

the conflict area or maintain a safe distance from the vehicle ahead. The initial batch of vehicles departing the conflict Fig. 3. 

OBB collision detection. 

central zone triggers an update to the serial numbers of the subsequent batches, enabling the new first batch to continue vehicle interactions, vehicle positioning information may be entering the conflict zone and coordinate operations. 

inaccurate due to communication delays or noise. To reduce When vehicles operate in the preparatory zone, the intel-the impact of such issues on vehicle cooperation tasks, the ligent driver model \(IDM\) \[44\] is employed for vertical oriented bounding box \(OBB\) algorithm \[25\] is employed control to accurately characterize driver behavior in real-world to model vehicle interactions. As shown in Fig. 3, each scenarios. The control command for IDM is given as follows: vehicle is represented by an OBB, in which appropriate safety *v*

*β*

*s*∗ *\(v, * *v\) * 2

redundancy is added to the box to account for potential noise *a* IDM = *a* max 1 −

−

*v*

*s*

and inaccuracies in the positioning data. The Separation Axis 0





Theorem is employed to determine whether there is an overlap *s*∗ *\(v, * *v\) *= *s*

0 *, vT *\+ *v* *v*

√

\(4\)

between bounding boxes, serving as an accurate and effective 0 \+ max

2 *ab*

vehicle collision detection method. If there exists an axis such where *v*

that the projections of the two OBBs onto the axis do not 0 represents the desired speed of the vehicle, *β*

represents the acceleration index, *b * represents the comfortable overlap, then there is no collision between the two vehicles. 

deceleration, *v * and *s * represent the speed difference and the Safety redundancies *dr* 1 and *dr* 2 for collision detection will be distance between the vehicle and its front vehicle, respectively. 

activated during the training phase and deactivated during the When the vehicle is about to enter the conflict zone, if it is model validation phase. 

not part of the first batch, a virtual vehicle is assumed to exist at the boundary between the conflict zone and the preparatory *C. Hierarchical Coordination Framework*

zone, which ensures that the vehicle can stop smoothly in To reduce the burden on the central coordinator and front of the conflict zone in accordance with IDM method. If improve the computational efficiency, a hierarchical coordi-the vehicle has been updated to the first batch, it may enter nation framework is adopted to facilitate the coordination of the conflict zone at its current speed or restart its maneuver. 

vehicles in a continuous traffic flow. Specifically, the vehicles Given the inherent randomness of the traffic scene, the speed are divided into distinct batches. The vehicles on each lane that at which vehicles enter the conflict zone remains random. In are closest to the conflict zone comprise the first batch, while the conflict zone, vertical control of vehicles is handled by the the remaining vehicles are divided into subsequent batches central coordinator. After completing the collaborative task at based on their lane and distance factors, as shown in Fig. 1. 

intersections, they leave the conflict zone at the natural traffic The first batch of vehicles tend to navigate through the conflict flow speed *v* flow. 

zone cooperatively, with the assistance of the centralized In addition to vertical control commands, lateral control coordinator. The rest of candidate vehicles departing from the commands are derived from \(2\). By integrating the vertical Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:40:07 UTC from IEEE Xplore. Restrictions apply. 

23362

IEEE INTERNET OF THINGS JOURNAL, VOL. 12, NO. 13, 1 JULY 2025

and lateral control algorithms, the overall control vector \[ *a, δ*\] *T*

is transmitted to the vehicle model at each control interval to update the traffic scene. 

IV. METHODOLOGY

*A. Deep Reinforcement Learning Framework*

Reinforcement learning \(RL\) frameworks are typically for-Fig. 4. 

Encoding of *d * for different driving intentions. 

mulated as Markov decision processes \(MDPs\) \[45\]. An MDP

is defined as a quintuple *\(S, A, R, P, γ \)*, which mathematically describes the interaction between the environment and the zone. The observation state space can be defined as a series decision-making of the RL agent. Specifically, *S * represents the of states of the controlled vehicles, i.e., 

observable state space in the environment, and *A * represents the decision action space taken by the RL agent. The reward *s *= \[ *s* 1 *, s* 2 *, . . . , sn*\]

\(8\)

function, *R*, describes the immediate reward obtained after taking action *at *∈ *A * in the state *st *∈ *S*, typically expressed where *n * denotes the number of vehicles in the control batch. 

as *rt\(st, at\) *∈ *R*. *P * is the state transition probability, which Initially, the fundamental status information for each vehi-represents the probability of transitioning to the next state *st*\+1

cle encompasses its position *\(x, y\)*, velocity *v*, and steering after taking action *at * in the current state *st*. *γ * acts as the angle *θ*. The inclusion of state information with varying mean-discount factor to balance the importance of immediate and ings and scales enhances the complexity of the optimization future rewards, within the range of \[0, 1\). 

problem, necessitating the agent to allocate more time to In the intersection scenario, at each time step *t*, the central learn the optimal policy. Consequently, both velocity and coordinator observes the current state *st * and selects an action steering angle variables are incorporated, and the *x * and *y* *at * by executing the policy *π\(at*| *st\)*. The environment then axis projections of the velocity, *v*

transits to the next state *s*

*x * and *vy*, respectively, are

*t*\+1 according to the vehicle model, 

employed to streamline the representation of state information. 

and the coordinator receives a reward *rt\(st, at\)*. Finally, the Then, to effectively capture the driving intention of the vehicle, accumulated experience is utilized to update the policy. The a distance intention code is employed, denoted as *d*, to expected payoff of the policy *π * could be calculated as follows: represent the route intention of the vehicle, as illustrated *Vπ \(s*

in Fig. 4. Finally, the state of each vehicle is expressed as *t\) *= E *τ *∼ *π *\[ *Gt*| *st*\]

\(5\)



*\(x, y, vx, vy, d\)*. 

where *G*

∞

*t *=

*γ i*− *tr*

*i*= *t*

*i * is the discounted return, *τ *∼ *π*

*2\) Action Space: * The action space is defined as the set of denotes the trajectory *\(st, at, st*\+1 *, at*\+1 *, . . .\) * generated by actions available to the vehicles. To reduce the complexity of the agent acts according by the policy *π*. 

training, the vehicle model defined in Section III is employed, The value function formula is commonly used to estimate where the lateral control of the vehicles is handled by the the *Vπ \(st\)*, the objective of RL is to learn the policy *π*∗ that pure pursuit algorithm, and the agent is only responsible for maximizes the expected return across all states *st* the vertical control, i.e., the acceleration of the vehicles. The acceleration settings for each vehicle are defined as a discrete *Qπ \(st, at\) *= *rt *\+ *γ * E *τ*∼ *π Qπ \(st*\+1 *, at*\+1 *\)* \(6\)





set, *a* available = \{−2 *, *−1 *, * 0 *, * 1 *, * 2\}, in *m/s* 2. The action space is *π*∗ = arg max E

*Qπ \(s*

*. *

\(7\)

*π*

*τ*∼ *π*

*t, at\)*

expressed as

To enhance the agents’ understanding, decision-making, *a *= \[ *a* 1 *, a* 2 *, . . . , an*\]

\(9\)

and generalization abilities, the DRL scheme is developed by integrating deep neural networks with RL. This approach where *n * denotes the number of controlled vehicles, *a* leverages neural networks to effectively approximate the pol-k

∈

*a*

icy and value functions, enabling the agent to accurately available, *k *≤ *n*, *k *∈ N\+. 

*3\) Reward Functions: * Reasonable reward function design comprehend the environment’s state. Consequently, the agent is crucial for the effective training of the agent. The reward can learn and make optimal decisions with better efficiency, function can be divided into positive and negative com-thereby achieving superior performance on complicated tasks. 

ponents. Positive rewards provide encouraging signals that incentivize vehicles to collaborate spatiotemporally in the *B. Problem Formulation*

conflict zone, enabling efficient task completion. Conversely, The design of the MDP tuple elements must be tailored to negative rewards serve as deterrents against undesirable vehi-the specific requirements of the task, enabling the DRL agent cle behaviors such as collisions, by introducing penalties. 

to learn the optimal policy *π*∗. In the intersection collaboration Positive rewards in training can be categorized into individ-task, our MDP elements are designed as follows. 

ual and group-based rewards. The individual positive reward *1\) Observation State Space: * According to the hierarchical *r* ind is given to a vehicle when it successfully completes coordination framework, the central coordinator primarily the crossing task by leaving the conflict center area. In concentrates on dispatching vehicles closest to the conflict contrast, group positive reward *r* group represents an overall Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:40:07 UTC from IEEE Xplore. Restrictions apply. 

WANG et al.: SOLVING THE VEHICLE COOPERATION PROBLEM AT SIGNAL-FREE INTERSECTION

23363

Update

synergistic reward provided when all vehicles in the current batch successfully exit the conflict center area Tanh

\(

\)

*n*



Update

Vehicle 1

Flatten

*r*

\(

\)

positive =

*cir* ind \+ *c* all *r* group

\(10\)

Normalization

Tanh

Vehicle 2

Tanh

*i*=1

Calculate

where *r* ind denotes the individual positive reward, *r* group represents the group positive reward, *ci * indicates whether the Update

Update

vehicle *i * has completed its crossing task, *c* all indicates whether all controlled vehicles have completed overall crossing task, Fig. 5. 

Shared actor–critic architecture. 

they are assigned as 1 if the task succeeds, and 0 otherwise. 

The negative reward scheme is structured into time-based and collision-based penalties. The time-based penalty *r* time policy learning with value function estimation to optimize the aims to impose a cost on the duration taken by a batch of parameter learning of the multi networks. 

vehicles to accomplish the cooperative intersection crossing. 

The utilized network architecture is illustrated in Fig. 5, 

Simultaneously, a significant negative reward *r* collision is issued where the shared network component comprises the long-and the mission is immediately aborted upon any collision, short term memory \(LSTM\) layer and the fully connected marking a failure in the collaborative task

layers. In the context of the intersection scenario, gathered experience data is stored as serialized information. Given the *r* negative = *r* time *t *\+ *s* col *r* collision \(11\)

extensive temporal dependencies resulting from environmental where *r*

state changes, the agent’s decisions are influenced by temporal time denotes the time-based penalty, *r* collision denotes the collision-based penalty, *t * represents the time spent, *s* memory. LSTM network can leverage their memory units to col

indicates the signal whether a collision has occurred, which is learn the temporal correlation features inherent in the sequence assigned as 1 if it has occurred, and 0 otherwise. 

data. After normalizing the initial data input, the LSTM layer The design of parameters in the reward function is directly is employed to capture and retain the long-term dependencies associated with the convergence effects and the agent’s present within the observed sequence data. Next, a multilayer behavior patterns. In the context of vehicle cooperation at fully connected network is employed to process input data in intersections, the primary objective is to facilitate effec-a layer-by-layer manner. This hierarchical feature extraction tive vehicle collaboration to exit the intersection safely. 

method allows the network to capture deep patterns and Consequently, *r*

relationships within the data, particularly in high-dimensional group is prioritized above all other parameters, and its absolute value should significantly exceed those of data. The Tanh activation function is utilized to transfer feature parameters *r*

information between network layers. It introduces nonlinear ind and *r* time. For safety considerations, the penalty *r*

characteristics that enable the neural network to learn and collision

is assigned with a substantial negative value to effectively deter and penalize risky vehicle behaviors. The approximate complex nonlinear functions, thereby enhancing parameters *r*

the model’s feature extraction and expression capabilities. 

ind and *r* time are employed to reduce vehicle latency, enhance traffic efficiency, and provide immediate Then, the output of the shared network layers is passed reward feedback. Consequently, they are typically assigned through the Actor and Critic components of the fully con-with smaller values. After meticulously debugging the param-nected layers. The Actor component generates specific vehicle eters, the values for *r*

actions for execution, while the Critic component evaluates the group, *r* collision, *r* ind, and *r* time are set to 100 or 150, −100, 20, and −0.15, respectively, to enhance current intersection environment and provides the policy loss the performance of the method. Further parameter details are calculation that can be utilized to update the Actor component. 

described in Table II. 

Additionally, the reward function supplies the Critic with a Equation \(12\) depicts the ultimate reward function, wherein value function loss calculation for updating. By utilizing the two reward mechanisms synergistically facilitate the agent’s shared network component, the model can reduce the total learning process by balancing exploration and exploitation number of parameters, promote the transmission and sharing of information features, and improve the consistency between *rt *= *r* positive \+ *r* negative *. *

\(12\)

Actor and Critic, enhancing the overall learning performance. 

The network is updated by employing the generalized *C. Shared Advantage Actor–Critic Architecture* advantage estimation \(GAE\), which estimates the advantage function through a weighted combination of multistep advan-The shared A2C network architecture is employed for train-tage estimates. This approach effectively reduces the deviation ing the intersection collaboration model. The model comprises and variance of the advantage estimates, thereby improving three types of neural networks: 1\) a shared network; 2\) an actor the stability of the estimation process. The calculation formula network; and 3\) a critic network. The shared network extracts for GAE is as follows:

significant latent feature information from the traffic scene, while the Actor network generates specific policy actions *δt *= *rt *\+ *γ V\(st*\+1 *\) *− *V\(st\)* based on the shared feature information. The Critic network *T*− *t*−1



evaluates the value of the policy produced by the Actor GAE *\(t\) *=

*\(γ λ\)kδt*\+ *k*

\(13\)

network. During the training process, the model integrates *k*=0

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:40:07 UTC from IEEE Xplore. Restrictions apply. 

23364

IEEE INTERNET OF THINGS JOURNAL, VOL. 12, NO. 13, 1 JULY 2025

where *δt * represents the advantaged estimate at time step **Algorithm 1: **Training Strategy of the Asynchronous *t*, *V\(st\) * indicates the value function estimate at state *st*, *λ*

Shared A2C-Based Coordinator

represents the hyperparameter that controls the tradeoff bias 1: Initialize several training processes, training experience and variance, and *T * denotes the last time step. 

pools, a testing process, a testing experience pool, shared The total training loss is calculated as the weighted sum of Actor-Critic parameters *θ*, a parameter sharing pool, the policy loss and the value function loss, given as follows: parameters *γ *, *λ*, maximum epoch duration *tmax*, Completion signal *s*=false. 

losspolicy =

−log

*\(*

probs *t\) *· GAE *\(t\) *− Entcoe · Ent *\(t\)* 2: **while **not *s ***do**

*t*



3:

**for **each training process **do**

lossvalue =

*\(rt *− *V\(st\)\)* 2

4:

Initialize the intersection environment, termination *t*

sign *done *= false, time *t *= 0. 

losstotal = *w* 1 · losspolicy \+ *w* 2 · lossvalue \(14\)

5:

Load model parameters *θ * from the parameter sharing pool. 

where log

*\(*

probs *t\) * represents the logarithmic probability at 6:

**while **not *done ***do**

time step *t*, Entcoe denotes the coefficient used to control 7:

Observed environment state *s*

the regularization of the policy entropy, Ent *\(t\) * represents the *t*. 

8:

**if ** *t > t*

policy entropy, *w*

*max ***then**

1 and *w* 2 indicate weights. 

9:

Break. 

In this work, the hyperparameter *λ * is set to 1, indicat-10:

## **end if**

ing that the GAE utilizes multistep return estimations on a 11:

Calculate the agent’s decision *a*

more accurate evaluation of long-term returns. This setting *t *= *π\(st\)*. 

12:

Update the environment with *a*

helps effectively capture the long-term dependencies of tasks, *t*, store

*\(s*

particularly at the signal-free intersections where a long-term *t, at, rt, st*\+1 *, done\) * in the training experience pool. 

policy is essential. Simultaneously, in the presence of reward 13:

*t *= *t *\+ 1. 

delays, it facilitates a more stable update of the policy. The 14:

## **end while**

coefficient Entcoe is set to 0.01, which is generally regarded 15:

**if **not obtain the mutex **then**

as a reasonable choice in deep RL. This setting aids the agent 16:

Request and wait for the mutex. 

in achieving a balance between exploration and exploitation, 17:

## **else**

thereby enhancing the robustness of the policy. 

18:

Update the model parameters *θ * in the parameter The gradient of the total loss is computed via backpropaga-sharing pool. 

tion, and then clipped to prevent gradient explosion. The Adam 19:

Release the mutex. 

optimizer is subsequently employed to update the model’s 20:

## **end if**

parameters. 

21:

## **end for**

### 22:

**for **the testing process **do**

*D. Asynchronous Training Strategy*

23:

Evaluate the current model at regular intervals. 

An asynchronous training approach leveraging the multi-24:

**if **the model has converged **then**

process concurrency capabilities of the operating system has 25:

*s*=true. 

been implemented to enhance the training efficiency of A2C. 

26:

## **end if**

By creating parallel environments, multiple processes can 27:

## **end for**

interact with their environment independently, initiate training 28: **end while**

simultaneously, and share model parameters through a parameter synchronization mechanism. This approach effectively enhances data efficiency and improves the effectiveness of exploration. 

state to ensure exclusive access to the sharing pool. This In the asynchronous training strategy, multiple processes blocking prevents other training processes from modifying serve as the training processes, with one designated as the parameters concurrently. Once the update is complete, the testing process, and a parameter sharing pool utilized the mutex is released, allowing other training processes to for facilitating the sharing of model parameters across all continue updating the model parameters. To assess the validity processes. Fig. 6 summarizes the asynchronous shared A2C

and robustness of the model in real-time during the training, structure of the signal-free intersection cooperation model. 

the testing process is initiated to evaluate the A2C model in For each training process, they generate simulated intersection real-time. 

environments using distinct random seeds to enhance the Algorithm 1 illustrates the whole process of the proposed exploration toward intricate environments. Upon resetting the method. Intersection scenarios are constructed concurrently by environments, they load the A2C model parameters from the multiple training processes. These processes load the latest sharing pool and engage with the environments to collect A2C model from the parameter sharing pool and interact with experience. The parameter sharing pool employs a mutual their environments to collect experience. Each training process exclusion mechanism to manage update to the model param-continuously requests and releases the mutex. Upon acquiring eters during the entire training process. When a training the mutex, it extracts the experience to calculate the total loss process requires an update operation, it enters a blocked of the A2C network model for updating the model parameters Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:40:07 UTC from IEEE Xplore. Restrictions apply. 



WANG et al.: SOLVING THE VEHICLE COOPERATION PROBLEM AT SIGNAL-FREE INTERSECTION

23365

Create

Interact

Process 1

\[\( , 

, 

, 

, 

\)\]

Initialize

Process 2

\[\( , 

, 

, 

, 

\)\]

Process n

\[\( , 

, 

, 

, 

\)\]

Create

Process 1

Evaluation

Initialize

Release 

Mutex

Policy 

Multi-process execution

Loss

Request 

Update 

Training

Mutex 

Load

Completed

Model

Value 

Parameter 

Loss

Asynchronous Update

Fig. 6. 

Asynchronous shared A2C structure of the signal-free intersection cooperation model. 

benchmark algorithms based on optimization and graph theory principles. The scene parameters and controller parameters are shown in Table I, and the parameters of the deep RL

algorithms are shown in Tables II and III. 

To reasonably evaluate the scheduling performance between strategies, two metrics are considered: 1\) retreat time and 2\) averaged delay time, which can represent the traffic efficiency and smoothness of traffic scenarios. Assuming there are *N*

vehicles in the scenario, *tin * represents the time point at which *i*

vehicle *i * enters the conflict zone, *t* out represents the time *i*

point at which vehicle *i * leaves the conflict central zone, and Fig. 7. 

\(a\) and \(b\) represent the T-shaped intersection and the Cross *t* flow represents the time from entering the preparatory zone intersection in SUMO, yellow vehicles represent the first batch of vehicles, *i*

and green vehicles represent other batches of vehicles. 

to leaving the conflict central zone assuming that it has been using the natural traffic flow speed. 

1\) *Retreat Time: * It is defined as the latest time for all before releasing the mutex. The testing process is employed vehicles to leave the conflict central zone

to monitor the training convergence of the model. The testing *T* ret = max *t* out *, *

*i*

*i *≤ *N, i *∈ N\+ *. *

\(15\)

process is employed to monitor the model’s convergence and to issue the termination signal. 

2\) *Averaged Delay Time: * It is defined as the average of the difference between the actual travel time and the ideal travel time for all vehicles

V. EMPIRICAL ANALYSIS

*N*





¯

*A. Experimental Settings*

*T* delay = 1

*t* out − *t* in − *t* flow *, i *≤ *N, i *∈ N\+ *. *\(16\) *N*

*i*

*i*

*i*

*i*=1

The simulation experiments are conducted on a personal computer with an Intel i7 CPU and 16GB RAM, using Meanwhile, the metric of computational time, which the Python language. Two typical intersection scenarios are quantifies the duration required for average execution constructed in the SUMO software \[46\], which is dedicated to of the algorithm, has been employed to assess the traffic simulation, as illustrated in Fig. 7. To facilitate compar-implementation performance. 

ison with the mainstream methods, the two intersection scenes 3\) *Computational Time: * It is defined as the averaged are restricted to single-lane configurations. The extensibility execution duration of the algorithm. 

of our method in the multilane intersection scenario is also discussed in Section V-E. 

*B. Ablation Experiments*

Our proposed method is compared with several main-To effectively evaluate the contributions of each component stream methods, including the PPO method \[24\], the DFST

of the proposed method, a series of ablation experiments have method \[47\], the MCC method \[20\], and the CGTS

been conducted to compare the training performance. 

method \[21\] which are recently-proposed. The PPO method is To verify the effectiveness of asynchronous training strategy, a popular deep RL approach, while the remaining methods are Fig. 8\(a\) and \(b\) illustrates the reward curves for various Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:40:07 UTC from IEEE Xplore. Restrictions apply. 

23366

IEEE INTERNET OF THINGS JOURNAL, VOL. 12, NO. 13, 1 JULY 2025

Fig. 8. 

Training curves of different number of processes. \(a\) T-shaped Fig. 9. 

Ablation experiments of the designed network. \(a\) T-shaped intersection. \(b\) Cross intersection. 

intersection. \(b\) Cross intersection. 

which is referred to as Method 1. Additionally, the shared training processes. The results indicate that, in terms of network layer is substituted with isolated Actor and Critic convergence speed, the agent with 2 training processes at network architectures, which are designated as Method 2. 

the T-shaped intersection gradually converges to the optimal Fig. 9\(a\) and \(b\) indicates their reward curves during train-policy after approximately 1000 episodes \(300 s\), while the ing \(8 training processes\). Regarding training speed, the agent with 8 training processes converges to the optimal policy original method employs an LSTM layer, which increases after about 600 episodes \(80 s\). At the Cross Intersection, computational overhead, resulting in a longer elapsed time. 

the agent with 2 training processes converges to the optimal However, given the same number of episodes, the original policy after approximately 2000 episodes \(680 s\), whereas method achieves convergence the fastest, while Method 2

the agent with 8 training processes converges to the optimal exhibits the slowest convergence rate. In terms of performance, policy after about 1000 episodes \(140 s\). In terms of sta-both Method 1 and Method 2 exhibit slightly decreased bility, an increased number of training processes results in expected reward values than the original method. The observed reduced oscillation of the reward curve, leading to improved performance indicates that the addition of the LSTM layer is smoothness and enhanced stability. In terms of performance, beneficial for capturing the significant long-term dependencies the expected reward value of the optimal policy with a greater of decisions in driving scenarios. Additionally, the design number of training processes is slightly higher than that of of the shared network allows both the Actor and Critic to the policy with fewer training processes. This indicates that learn a more unified and consistent representation of envi-increasing the number of training processes contributes to ronmental features, rather than developing features that are improved performance. The results presented above can be independent of one another. Together, these elements included attributed to the asynchronous training strategy, where the in the designed network can accelerate the convergence of the agent’s exploration behavior across multiple training processes training strategy and improve the overall performance of the complements one another, enabling the model to achieve a model. 

better balance between exploration and exploitation. As the The contrast between the PPO method and our method is number of training processes increases, the model becomes illustrated in Fig. 10\(a\) and \(b\). In the PPO method, the Actor more adept at learning the dynamic characteristics of the and Critic networks with fully connected layers are trained environment, thereby optimizing its policy learning and allow-independently. Our method achieves a faster convergence rate, ing for the acquisition of superior strategies in a reduced a smoother reward curve, and a higher expected reward. This timeframe and with fewer episodes. 

further demonstrates that the developed network facilitates a The ablation experiments have been conducted on the better collaboration between policy learning and value function designed network components. In the original network archi-estimation, thereby enhancing the training performance of the tecture, the LSTM layer is replaced by a fully connected layer, method. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:40:07 UTC from IEEE Xplore. Restrictions apply. 

WANG et al.: SOLVING THE VEHICLE COOPERATION PROBLEM AT SIGNAL-FREE INTERSECTION

23367

Fig. 11. Comparison of scheduling metrics performance between our method Fig. 10. 

Training curve comparison between our method and PPO method. 

and benchmark algorithms at the T-shaped intersection. 

\(a\) T-shaped intersection. \(b\) Cross intersection. 

*C. Metrics Performance*

In the simulation, different traffic densities are modeled by adjusting the number of vehicles in the scene as indicated in \[20\]. For the T-shaped intersection, 6, 9, and 12 vehicles are generated in each lane to represent low, medium, and high densities, respectively. In the case of the cross intersection, we generate 5, 8, and 11 vehicles. The vehicle arrival rate on the road is set to 1200 vehicles per hour, and the initial positions and speeds of the vehicles are randomized to simulate a more realistic traffic scenario. The hierarchical coordination framework is adopted to coordinate continuous traffic flow, and the scheduling performance of the proposed method is measured by two metrics. 

The experimental results are shown in the Figs. 11 and 12, 

which demonstrate that our method consistently achieves better operational performance over the baseline approaches. 

At the T-shaped intersection, our method reduces retreat time by 27.71%, 29.99%, 23.92%, 14.41%, and averaged delay time by 35.06%, 32.21%, 24.75%, 8.95% compared with methods DFST, MCC, CGTS, and PPO at low traffic density. Under high traffic density, the reduction in retreat time increases to 33.60%, 35.72%, 28.79%, 11.55%, and the reduction in averaged delay time increases to 32.15%, 28.22%, 21.65%, Fig. 12. Comparison of scheduling metrics performance between our method and benchmark algorithms at the cross intersection. 

12.23%. At the cross intersection, under the low density, our method reduces retreat time by 28.30%, 23.96%, 19.01%, 11.07%, and averaged time by 43.34%, 21.32%, 20.85%, conducted across different traffic conditions, with analysis 16.91%. Under the high density, the reduction in retreat of variance \(ANOVA\) employed for statistical significance time increases to 32.53%, 27.86%, 17.29%, 11.23%, and the analysis. Statistical results have been reported in Table IV. 

reduction in average delay time increases to 42.96%, 24.59%, *AT* ret, *AT*

, *AC*

represent the ANOVA statistics of

delay

ret and *AC*

delay

20.59%, 16.24%. 

the two metrics, while *hT* ret, *hT*

, *hC*

indicate the

delay

ret and *hC*

delay

To more effectively highlight the performance disparity test values of ANOVA under the two intersection scenarios. 

between our method and others, 40 simulations have been The experiments assume the null hypothesis that our method Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:40:07 UTC from IEEE Xplore. Restrictions apply. 

23368

IEEE INTERNET OF THINGS JOURNAL, VOL. 12, NO. 13, 1 JULY 2025

TABLE VI

SUCCESS AND ACCIDENT RATES UNDER DIFFERENT DELAYS AND NOISE

is not significantly different from other algorithms. However, delays. Some studies \[48\], \[49\] suggest that the communica-with the significance level set at 0.05, all test values equal 1, tion delay for V2I and V2V in the future is unlikely to exceed indicating that the statistical analyses reject the hypothesis 500 ms. Consequently, the communication delays have been in every case. Significant statistics reveal that our method set to 0, 100, 200, 300, 400, and 500 ms, respectively. 

significantly outperforms other methods. Based on the afore-The employed strategy has been trained under the optimal mentioned statistical analyses, it can be concluded that the communication condition \(without delay or noise\) and subse-disparities in results between our method and other algorithms quently test it under various delay scenarios. The double-ended are not due to mere chance, but rather attributed to the queue data structure is utilized to store vehicle information distinctive properties of the algorithms. 

during the simulation, which is often used to model This performance is attributed to the incentive strategy information lag during communication \[50\]. Real-time vehicle for both collision risks and travel time costs, aiming to information is stored at the front of the queue, while historical enabling each batch of vehicles to exit the intersection quickly information is retrieved from the back to update the current without collision, thereby achieving optimal collaboration state. By controlling the length of the queue and the simula-among the vehicles. Compared to the PPO method, our tion frequency, varying degrees of communication delay can method designs a more comprehensive representation of envi-be simulated. Additionally, Gaussian noise is introduced to ronmental features and employs the asynchronous training the vehicle’s position and speed information to more accu-strategy that enables multiple agents to operate independently rately simulate the uncertainty present in real-world scenarios. 

in different environments. This diversified experience col-The probability density function of noise and the vehicle lection method effectively reduces the correlation between information following noise processing are presented in samples, enhances the generalization ability and mitigates

− *\(x*− *μ\)* 2

overfitting. Consequently, this leads to higher expected returns *P\(x\) *=

1

√

*e*

2 *σ * 2

and improved task performance compared to the PPO method. 

*σ * 2 *π*





Other methods, including DFST, MCC, and CGTS, although Pos *n *= Postrue \+ *N μp, σ * 2 *p* planning for a large number of vehicles simultaneously, such methods prioritize absolute safety redundancy in the *Vn *= *V* true \+ *N μv, σ * 2 *v* \(17\)

central conflict zone and do not adequately consider the where Pos *n * and *Vn * represent the information after noise spatiotemporal nonoverlap of vehicle trajectories. In contrast, processing, *μp * and *μv * denote the mean value in the noise with our approach, which employs the hierarchical coordination the value of 0, *σp * and *σv * indicate the standard deviations, with framework, enables vehicles to learn strategies for generat-values of 1 and 0.5, respectively. 

ing conflict-free space-time trajectories, thereby reducing the Under varying communication conditions, 100 experiments retreat time and average delay time at the intersection. 

have been conducted to evaluate the cooperation success The computational time of various methods is presented rate and accident rate of vehicles at intersections. Results of in Table V. The calculation time of our method and the these experiments are presented in Table VI. Communication PPO method is at the submillisecond level, in contrast to the delays and noise introduce uncertainty and unreliability in millisecond level observed for other methods. This discrepancy decision-making information, which can significantly impact can be attributed to the advanced reasoning and computational the accident rate in vehicle cooperation. This effect becomes capabilities of deep neural networks, which allows for direct more pronounced under complex scenarios and greater delays. 

end-to-end processing of input data without the need for At the T-shaped intersection, our approach attained a 100%

additional processing steps. Consequently, our method is well-success rate and a 0% accident rate with a delay of less than suited to meet the real-time requirements of applications. 

300 ms, as well as a success rate of 96% and an accident rate In general, our method achieves better collaborative vehicle of 4% at a delay of 500 ms. At the cross intersection with more performance in intersection scenarios than other algorithms complexity, our method achieved a success rate of 93% and an with fewer computational resources, proving the effectiveness accident rate of 7% with a delay of 500 ms. Communication and superiority. 

delays and noise can hinder vehicles’ ability to respond in a timely and accurate manner during collaborative efforts, thereby increasing the risk of collisions. Nevertheless, our *D. Communication Delay and Noise Robustness* method demonstrates significant robustness in the presence of In real-world scenarios, communication conditions are often high latency and noise, effectively reducing the accident rate to less than the ideal situation. Therefore, this section discusses 7% or lower. This effectiveness primarily stems from the safety the robustness of our method in relation to communication redundancy mechanism designed for the vehicle, along with Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:40:07 UTC from IEEE Xplore. Restrictions apply. 





WANG et al.: SOLVING THE VEHICLE COOPERATION PROBLEM AT SIGNAL-FREE INTERSECTION

23369

\(a\)

\(b\)

Fig. 13. 

\(a\) and \(b\) represent the multilane scenario constructed in SUMO

and the training performance of our method, respectively. 

the incorporation of stringent penalties for collisions within the reward function. In the presence of communication delays and noise, OBBs can alleviate the effects of inaccurate positioning information and elevate the safety threshold for vehicle distance. Furthermore, the imposition of severe collision penalties Fig. 14. 

Components of the miniaturized autonomous driving platform. 

encourages learning the policy that avoid aggressive, low-safety maneuvers. 

Since this work focuses on the effectiveness and efficiency of vehicle coordination strategies, the safety redundancy utilized is a fixed value. In future work, incorporating flexible security redundancy \[51\] and the delay indicator into the algorithm design is anticipated to further enhance the algorithm’s robustness against communication delays and noise, thereby reducing the accident rate. 

*E. Multilane Scenario*

For other types of methods, increasing the number of lanes may lead to an exponential increase in computational complexity. However, our method can be adapted for multilane intersections with straightforward adjustments. We designed Fig. 15. 

Intersection site used in the field experiments, where the dashed line area is the conflict zone, and the rest is the preparatory zone. 

an intersection with multiple lanes, as illustrated in Fig. 13\(a\). 

By adjusting the input and output dimensions of the neural network, our collaborative strategy can be effectively extended PC, a communication unit, autonomous vehicles, and position-to multilane scenarios. Fig. 13\(b\) presents the convergence ing modules. 

performance of our method. 

The positioning modules simulates GPS functionality, In summary, the proposed method demonstrates effective enabling the acquisition and broadcasting of vehicle driving operation at intersections of various shapes and lane con-information. The autonomous vehicle is powered by the figurations. It can adapt to different traffic environments RK3399 core board running the robot operating system \(ROS\), and requirements, showcasing its significant flexibility and which facilitates the deployment and operation of control algo-adaptability. 

rithms. The upper PC emulates the central coordinator, which can accept the vehicle information and make decisions through VI. FIELD EXPERIMENTS

the trained vehicle cooperation model. The communication A miniaturized autonomous driving platform has been unit utilizes a WIFI link to facilitate real-time communication developed to evaluate the effectiveness and feasibility of between the vehicle and the upper PC. Equipped with which, the proposed method in real-world scenarios. Section VI-A

the information transmission from vehicle to PC, and the outlines the infrastructure of the platform. Section VI-B details subsequent vehicles’ feedback on the executing decisions can the specific experimental settings, and Section VI-C analyzes be realized. 

the experimental results. 

*B. Experimental Settings*

*A. Infrastructure of the Miniaturized Autonomous Vehicle* In the field experiments, the intersection scenario utilized is *Platform*

depicted in Fig. 15. A total of four autonomous vehicles are As illustrated in Fig. 14, our platform constitutes an deployed in this scenario, starting simultaneously from various autonomous driving system scaled 10:1, comprising an upper locations within the preparatory zone and entering the conflict Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:40:07 UTC from IEEE Xplore. Restrictions apply. 



23370

IEEE INTERNET OF THINGS JOURNAL, VOL. 12, NO. 13, 1 JULY 2025

TABLE VII

SCENE AND CONTROLLER PARAMETERS IN FIELD EXPERIMENTS

Fig. 16. 

Experimental snapshots of our platform. 

zone. Throughout this process, all infrastructure components within the intersection cooperated fully to facilitate the vehicles’ crossing maneuvers without incidents. 

The experimental parameters are presented in Table VII. 

Given the scaling characteristics of the autonomous driving platform, the relevant parameters have been appropriately scaled to maintain consistency with the real-world environment. 

*C. Experimental Results*

Various collaborative algorithms are deployed on the upper computer, while the underlying control is handled by the vehicle’s core board. The retreat time and averaged delay time of four vehicles are recorded, controlled by different collaborative algorithms, in completing the cooperative task. Fig. 16 presents a series of experimen-Fig. 17. Retreat time and averaged delay time results in the field experiments. 

tal snapshots. Some demo videos can be accessed at https://github.com/Dingyh26/DRL\_Cooperation\_Demos. 

Ten independent realizations have been conducted to obtain uncertainties—including communication delay, processing averaged values. As shown in Fig. 17, a comparative anal-delay, and device response delay—have been evaluated on the ysis between different algorithms indicates that our method platform, with the total delay remaining at 300 ms or less. 

maintains outstanding performance in the practical scenario. 

Our method successfully completes the cooperation task even Specifically, our method reduces the retreat time by 37.83%, under the maximum delay of 300 ms, demonstrating its robust 37.03%, 34.06%, and 22.98%, respectively, and the averaged ability to mitigate delay risks in real-world scenarios. 

delay time by 50.82%, 44.65%, 27.18%, and 18.26% respectively, compared to methods including DFST, MCC, CGTS, and PPO. The experiments conducted on the autonomous driv-VII. CONCLUSION

ing platform further demonstrate the potential and superiority In this article, a deep RL approach has been devised of our proposed method in the collaborative application of to facilitate vehicle collaboration at signal-free intersections. 

intelligent vehicles in real-world scenarios. 

The cooperative problem is first modeled as the Markov Additionally, since the experiments have been con-decision process, and the mathematical formulation of the ducted using real physical components, various environmental model is meticulously tailored to meet the task’s requirements. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:40:07 UTC from IEEE Xplore. Restrictions apply. 

WANG et al.: SOLVING THE VEHICLE COOPERATION PROBLEM AT SIGNAL-FREE INTERSECTION

23371

The framework of DRL has been rectified, a shared A2C

\[11\] F. Ahmad, O. Almarri, Z. Shah, and L. Al-Fagih, “Game theory network architecture that employs LSTM and fully connected applications in traffic management: A review of authority-based travel modelling,” *Travel Behav. Soc. *, vol. 32, Jul. 2023, Art. no. 100585. 

layers is introduced to efficiently capture the spatial-temporal

\[12\] C. Chen et al., “A graph-based conflict-free cooperation method for characteristics of the involved states. The design of partially intelligent electric vehicles at unsignalized intersections,” in *Proc. IEEE*

shared Actor and Critic enhances the consistency of fea-Int. Intell. Transp. Syst. Conf. \(ITSC\), 2021, pp. 52–57. 

\[13\] N. P. Farazi, B. Zou, T. Ahamed, and L. Barua, “Deep reinforcement ture learning processes, promotes more efficient collaboration learning in transportation research: A review,” *Transp. Res. Interdiscipl. *

between policy learning and value function estimation, thereby *Perspect. *, vol. 11, Sep. 2021, Art. no. 100425. 

improving the model’s performance. To enhance the speed

\[14\] A. Haydari and Y. Yılmaz, “Deep reinforcement learning for intelligent and stability of the model training procedure, an asynchronous transportation systems: A survey,” *IEEE Trans. Intell. Transp. Syst. *, vol. 23, no. 1, pp. 11–32, Jan. 2020. 

training strategy that simultaneously drives multiple training

\[15\] C. Creß, Z. Bing, and A. C. Knoll, “Intelligent transportation systems processes to share and train the network model is considered. 

using roadside infrastructure: A literature survey,” *IEEE Trans. Intell. *

Simulation results demonstrate that the proposed method can *Transp. Syst. *, vol. 25, no. 7, pp. 6309–6327, Jul. 2024. 

\[16\] Y. Zhao, D. Gong, S. Wen, L. Ding, and G. Guo, “A privacy-preserving-be effectively applied to common intersection scenarios, with based distributed collaborative scheme for connected autonomous a significantly reduction on vehicle retreat time and averaged vehicles at multi-lane signal-free intersections,” *IEEE Trans. Intell. *

delay time compared to other benchmark algorithms, consum-Transp. Syst. , vol. 25, no. 7, pp. 6824–6835, Jul. 2024. 

\[17\] K. Ji, N. Li, M. Orsag, and K. Han, “Hierarchical and game-theoretic ing less computational budget. Furthermore, field experiments decision-making for connected and automated vehicles in overtaking conducted through a miniaturized autonomous driving plat-scenarios,” *Transp. Res. Part-C, Emerg. Technol. *, vol. 150, May 2023, form have further proven the potential and practical value of Art. no. 104109. 

\[18\] X. Gong, S. Liang, B. Wang, and W. Zhang, “Game theory-based the proposed method in real-world applications. Finally, to decision-making and iterative predictive lateral control for coopera-account for the uncertainties present in the real world, the tive obstacle avoidance of guided vehicle platoon,” *IEEE Trans. Veh. *

effects of communication delay on our vehicle collaboration *Technol. *, vol. 72, no. 6, pp. 7051–7066, Jun. 2023. 

\[19\] L. Yang et al., “Multi-lane coordinated control strategy of connected method are also tested and analyzed. 

and automated vehicles for on-ramp merging area based on coop-In the future, the design of flexible security redundancies erative game,” *IEEE Trans. Intell. Transp. Syst. *, vol. 24, no. 11, and constraints will be further explored to mitigate uncertain pp. 13448–13461, Nov. 2023. 

communication delays and reduce the accident rate. Further

\[20\] C. Chen, Q. Xu, M. Cai, J. Wang, J. Wang, and K. Li, “Conflict-free cooperation method for connected and automated vehicles at unsignal-investigation is worthy to expanding the environmental con-ized intersections: Graph-based modeling and optimality analysis,” *IEEE*

figurations and to be better aligned with practical conditions. 

*Trans. Intell. Transp. Syst. *, vol. 23, no. 11, pp. 21897–21914, Nov. 2022. 

We will delve deeper into the potential challenges of actual

\[21\] Y. Li, M. Liu, Q. Yang, Z. Shen, and W. Wu, “Collision-free autonomous scheduling at unsignalized intersection using conflict graph tree search,” 

deployment, including more complex environmental uncer-IEEE Internet Things J. , vol. 11, no. 8, pp. 14563–14578, Apr. 2024. 

tainties and interactions with non-CAV traffic, to expand the

\[22\] J. Shi, Y. Luo, P. Li, J. Wang, and K. Li, “Collaborative multi-proposed method to full-size vehicles in real world. 

lane on-ramp merging strategy for connected and automated vehicles using dynamic conflict graph,” *J. Intell. Connected Veh. *, vol. 7, no. 1, pp. 38–51, 2024. 

\[23\] J. Shi, K. Li, C. Chen, W. Kong, and Y. Luo, “Cooperative merging REFERENCES

strategy in mixed traffic based on optimal final-state phase diagram with flexible highway merging points,” *IEEE Trans. Intell. Transp. Syst. *, 

\[1\] S. 

E. 

Shladover, 

“Connected

and

automated

vehicle

systems:

vol. 24, no. 10, pp. 11185–11197, Oct. 2023. 

Introduction and overview,” *J. Intell. Transp. Syst. *, vol. 22, no. 3, 

\[24\] Y. Guan, Y. Ren, S. E. Li, Q. Sun, L. Luo, and K. Li, “Centralized pp. 190–200, 2018. 

cooperation for connected and automated vehicles at intersections by

\[2\] S. E. Li, S. Xu, X. Huang, B. Cheng, and H. Peng, “Eco-proximal policy optimization,” *IEEE Trans. Veh. Technol. *, vol. 69, departure

of

connected

vehicles

with

V2X

communication

at

no. 11, pp. 12597–12608, Nov. 2020. 

signalized intersections,” *IEEE Trans. Veh. Technol. *, vol. 64, no. 12, 

\[25\] J. Luo et al., “Real-time cooperative vehicle coordination at unsignalized pp. 5439–5449, Dec. 2015. 

road intersections,” *IEEE Trans. Intell. Transp. Syst. *, vol. 24, no. 5, 

\[3\] Q. Guo, L. Li, and X. J. Ban, “Urban traffic signal control with pp. 5390–5405, May 2023. 

connected and automated vehicles: A survey,” *Transp. Res. Part-C, *

\[26\] Z. Guo, Y. Wu, L. Wang, and J. Zhang, “Heuristic-based multi-agent *Emerg. Technol. *, vol. 101, pp. 313–334, Apr. 2019. 

deep reinforcement learning approach for coordinating connected and

\[4\] R. Azimi, G. Bhatia, R. R. Rajkumar, and P. Mudalige, “STIP: Spatio-automated vehicles at non-signalized intersection,” *IEEE Trans. Intell. *

temporal intersection protocols for autonomous vehicles,” in *Proc. *

*Transp. Syst. *, vol. 25, no. 11, pp. 16235–16248, Nov. 2024. 

*ACM/IEEE Int. Conf. Cyber-Phys. Syst. \(ICCPS\)*, 2014, pp. 1–12. 

\[27\] B. Peng, M. F. Keskin, B. Kulcsár, and H. Wymeersch, “Connected

\[5\] S. Wang, J. Zhang, and X. Tan, “PDLC-LIO: A precise and direct autonomous vehicles for improving mixed traffic efficiency in unsignal-SLAM system toward large-scale environments with loop closures,” 

ized intersections with deep reinforcement learning,” *Commun. Transp. *

*IEEE Trans. Intell. Transp. Syst. *, vol. 25, no. 1, pp. 626–637, Jan. 2024. 

*Res. *, vol. 1, Dec. 2021, Art. no. 100017. 

\[6\] C. Wu, Z. Cai, Y. He, and X. Lu, “A review of vehicle group intelligence

\[28\] S. Wu, D. Tian, X. Duan, J. Zhou, D. Zhao, and D. Cao, “Continuous in a connected environment,” *IEEE Trans. Intell. Veh. *, vol. 9, no. 1, decision-making in lane changing and overtaking maneuvers for pp. 1865–1889, Jan. 2024. 

unmanned vehicles: A risk-aware reinforcement learning approach with

\[7\] B. Ji et al., “Survey on the Internet of Vehicles: Network architectures task decomposition,” *IEEE Trans. Intell. Veh. *, vol. 9, no. 4, pp. 4657–

and applications,” *IEEE Commun. Stand. Mag. *, vol. 4, no. 1, pp. 34–41, 4674, Apr. 2024. 

Mar. 2020. 

\[29\] H. Qian et al., “Collaborative overtaking strategy for enhancing overall

\[8\] D. Li et al., “A tightly coupled bi-level coordination framework for CAVs effectiveness of mixed connected and connectionless vehicles,” *IEEE*

at road intersections,” *IEEE Trans. Intell. Transp. Syst. *, vol. 25, no. 7, *Trans. Mobile Comput. *, vol. 23, no. 12, pp. 13556–13572, Dec. 2024. 

pp. 7832–7847, Jul. 2024. 

\[30\] D. Chen et al., “Deep multi-agent reinforcement learning for highway

\[9\] P. Cai, J. He, and Y. Li, “Hybrid cooperative intersection management on-ramp merging in mixed traffic,” *IEEE Trans. Intell. Transp. Syst. *, for connected automated vehicles and pedestrians,” *J. Intell. Connected* vol. 24, no. 11, pp. 11623–11638, Nov. 2023. 

*Veh. *, vol. 6, no. 2, pp. 91–101, Jun. 2023. 

\[31\] X. Zhang, L. Wu, H. Liu, Y. Wang, H. Li, and B. Xu, “High-speed

\[10\] W. Liu et al., “A systematic survey of control techniques and applications ramp merging behavior decision for autonomous vehicles based on in connected and automated vehicles,” *IEEE Internet Things J. *, vol. 10, multiagent reinforcement learning,” *IEEE Internet Things J. *, vol. 10, no. 24, pp. 21892–21916, Dec. 2023. 

no. 24, pp. 22664–22672, Dec. 2023. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:40:07 UTC from IEEE Xplore. Restrictions apply. 





23372

IEEE INTERNET OF THINGS JOURNAL, VOL. 12, NO. 13, 1 JULY 2025

\[32\] X. Gao et al., “A survey of collaborative perception in intelligent vehicles

\[51\] H. Xu, W. Xiao, C. G. Cassandras, Y. Zhang, and L. Li, “A general at intersections,” *IEEE Trans. Intell. Veh. *, early access, May 1, 2024, framework for decentralized safe optimal control of connected and doi: 10.1109/TIV.2024.3395783. 

automated vehicles in multi-lane signal-free intersections,” *IEEE Trans. *

\[33\] S. Chen, X. Hu, J. Zhao, R. Wang, and M. Qiao, “A review of *Intell. Transp. Syst. *, vol. 23, no. 10, pp. 17382–17396, Oct. 2022. 

decision-making and planning for autonomous vehicles in intersection environments,” *World Elect. Veh. J. *, vol. 15, no. 3, p. 99, 2024. 

\[34\] K. Zhang, Z. Cui, and W. Ma, “A survey on reinforcement learning-based control for signalized intersections with connected automated vehicles,” *Transp. Rev. *, vol. 44, no. 6, pp. 1187–1208, 2024. 

**Shuai Wang **received the B.S. and Ph.D. degrees

\[35\] V. Iordache, M. Minea, R. A. Gheorghiu, F. Badau, V. Stoica, and from Xidian University, Xi’an, China, in 2015 and V. A. Stan, “Assessing performance of long-range ZigBee for road 2020, respectively. 

infrastructure communications,” in *Proc. 16th Int. Conf. Electron.,* He is currently with the School of Intelligent

*Comput. Artif. Intell. \(ECAI\)*, 2024, pp. 1–5. 

Systems

Engineering, 

Sun

Yat-sen

University, 

\[36\] A. A. Malikopoulos, C. G. Cassandras, and Y. J. Zhang, “A decentralized Shenzhen, Guangdong, China. His research interests energy-optimal control framework for connected automated vehicles at include complex networks and intelligent systems. 

signal-free intersections,” *Automatica*, vol. 93, pp. 244–256, Jul. 2018. 

\[37\] P. Hang, C. Huang, Z. Hu, and C. Lv, “Driving conflict resolution of autonomous vehicles at unsignalized intersections: A differential game approach,” *IEEE/ASME Trans. Mechatronics*, vol. 27, no. 6, pp. 5136–5146, Dec. 2022. 

\[38\] W. Xiao et al., “Decision-making for autonomous vehicles in random task scenarios at unsignalized intersection using deep reinforcement learning,” *IEEE Trans. Veh. Technol. *, vol. 73, no. 6, pp. 7812–7825, **Yuhao Ding **received the B.E. degree from the Jun. 2024. 

School of Intelligent Engineering with Sun Yat-sen

\[39\] R. Chen and Z. Yang, “Cooperative ramp merging strategy at multi-lane University, Shenzhen, China, in 2023, where he is area for automated vehicles,” *IEEE Trans. Veh. Technol. *, vol. 73, no. 10, currently pursuing the master’s degree. 

pp. 14326–14340, Oct. 2024. 

His research interests include connected and

\[40\] Y. Li, Z. Chen, T. Wang, X. Zeng, and Z. Yin, “Data-driven hierar-autonomous vehicles and intelligent transportation. 

chical model predictive control for automated overtaking maneuver via gaussian process regression,” *IEEE Trans. Veh. Technol. *, vol. 74, no. 1, pp. 263–278, Jan. 2025. 

\[41\] Y. Kebbati, N. Ait-Oufroukh, D. Ichalal, and V. Vigneron, “Lateral control for autonomous wheeled vehicles: A technical review,” *Asian J. *

*Control*, vol. 25, no. 4, pp. 2539–2563, 2023. 

\[42\] X. Chen, P. Li, Q. Zhang, and Z. Jin, “Research and application of improved pure pursuit algorithm in low-speed driverless vehicle system,” 

in *Proc. IEEE Int. Conf. Adv. Elect. Eng. Comput. Appl. \(AEECA\)*, 2022, pp. 1483–1488. 

**Xiaoqi**

## **Ding**

is currently pursuing the B.E. 

\[43\] S. Kim, J. Lee, K. Han, and S. B. Choi, “Vehicle path tracking control degree with the School of Computer Science and

using pure pursuit with MPC-based look-ahead distance optimization,” 

Engineering, Sun Yat-sen University, Guangzhou, *IEEE Trans. Veh. Technol. *, vol. 73, no. 1, pp. 53–66, Jan. 2024. 

China. 

\[44\] M. Treiber, A. Hennecke, and D. Helbing, “Congested traffic states Her research interests include robot cluster col-in empirical observations and microscopic simulations,” *Phys. Rev. E*, laboration and decision making. 

vol. 62, no. 2, p. 1805, 2000. 

\[45\] O. Sigaud and O. Buffet, *Markov Decision Processes in Artificial* *Intelligence*. Hoboken, NJ, USA: Wiley, 2013. 

\[46\] P. A. Lopez et al., “Microscopic traffic simulation using SUMO,” in *Proc. 21st IEEE Int. Conf. Intell. Transp. Syst. *, 2018, pp. 2575–2582. 

\[Online\]. Available: https://elib.dlr.de/124092/

\[47\] B. Xu et al., “Distributed conflict-free cooperation for multiple connected vehicles at unsignalized intersections,” *Transp. Res. Part-C,* *Emerg. Technol. *, vol. 93, pp. 322–334, Aug. 2018. 

**Xiaojun Tan **\(Senior Member, IEEE\) received the

\[48\] S. Zeadally, J. Guerrero, and J. Contreras, “A tutorial survey on Ph.D. degree from the Department of Electronic

vehicle-to-vehicle communications,” *Telecommun. Syst. *, vol. 73, no. 3, Engineering, Sun Yat-sen University, Shenzhen, 

pp. 469–489, 2020. 

China, in 2005. 

\[49\] C. Sun, Y. Cui, N.-D. Ðào, W. Shi, and A. Khajepour, “Delay He had been serving with the School of

mitigation for V2I-based cooperative autonomous driving applica-Engineering, Sun Yat-sen University since July

tions,” in *Proc. IAVSD Int. Symp. Dyn. Veh. Roads Tracks*, 2023, 2005, where he is with the School of Intelligent pp. 502–510. 

Systems Engineering from 2017, he has been the

\[50\] R. Xu, Y. Guo, X. Han, X. Xia, H. Xiang, and J. Ma, “OpenCDA: Head of the New Energy Vehicles Research Center. 

An open cooperative driving automation framework integrated with co-Meanwhile, he acts also as the core member of

simulation,” in *Proc. IEEE Int. Intell. Transp. Syst. Conf. \(ITSC\)*, 2021, innovation team of Southern Marine Science and

pp. 1155–1162. 

Engineering Guangdong Laboratory, Zhuhai, China. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:40:07 UTC from IEEE Xplore. Restrictions apply.



