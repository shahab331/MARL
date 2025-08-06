Downloaded from https://iranpaper.ir https://www.tarjomano.com

https://www.tarjomano.com

**2024 IEEE Intelligent Vehicles Symposium \(IV\)** **June 2-5, 2024. Jeju Island, Korea** Autonomous Intersection Management with Heterogeneous Vehicles: A Multi-Agent Reinforcement Learning Approach

Kaixin Chen, Bing Li, Rongqing Zhang, Member, IEEE, and Xiang Cheng, Fellow, IEEE

Abstract—While

autonomous

intersection

management

\(AIM\) emerges to facilitate signal-free scheduling for connected and autonomous vehicles \(CAVs\), several challenges arise for planning secure and swift trajectories. Existing works mainly focus on addressing the challenge of multi-CAV interaction complexity. In this context, multi-agent reinforcement learning-based \(MARL\) methods exhibit higher scalability and efficiency compared with other traditional methods. However, current AIM methods omit discussions on the practical challenge of CAV heterogeneity. As CAVs exhibit different dynamics features and perception capabilities, it is inappropriate to adapt identical control schemes. Besides, existing MARL

methods that lack heterogeneity adaptability may experience a performance decline. In response, this paper exploits MARL to model the decision-making process among CAVs and proposes a novel heterogeneous-agent attention gated trust region policy Fig. 1. An illustrated AIM scenario with CAV heterogeneity optimization \(HAG-TRPO\) method. The proposed method can accomplish more effective and efficient AIM with CAV

However, it remains several difficulties for resolving vehicu-discrepancies by applying a sequential update schema that lar decision-making in versatile intersection ambiences. 

boosts the algorithm adaptability for MARL tasks with One of the essential challenges is the interaction complex-agent-level heterogeneity. In addition, the proposed method utilizes the attention mechanism to intensify vehicular cognition ity regarding multiple vehicles in the ever-changing intersec-on disordered ambience messages, as well as a gated recurrent tion. To address this challenge, some previous works adopt unit for temporal comprehension on global status. Numerical rule-based methods like the first-come-first-serve protocol experiments verify that our method results in CAVs passing

\[1\] and time-to-collision \(TTC \[2\]\) precaution rule \[3\] to at the intersection with fewer collisions and faster traffic dispatch CAVs under fixed logics, but the traffic efficiency flow, showing the superiority of our method over existing benchmarks in terms of both traffic safety and efficiency. 

of these methods is limited owing to the conservative nature of fixed rules \[4\]. Meanwhile, some other methods seek scheduling plans with minimized passing delays through I. INTRODUCTION

optimization-based methods \[5\] or tree search techniques As an essential scenario in intelligent transportation sys-

\[6\], but these methods encounter bottlenecks in computation tems, autonomous intersection management \(AIM\) enables speed and generalization when AIM involves large numbers efficient and automatic scheduling for connected and au-of CAVs \[7\]. Recently, multi-agent reinforcement learning-tonomous vehicles \(CAVs\) without rigid signal controls. 

based \(MARL\) techniques have been widely applied in the field of vehicular cooperation \[8\] \[9\]. Compared with the 2024 IEEE Intelligent Vehicle Symposium \(IV\) | 979-8-3503-4881-1/24/$31.00 ©2024 IEEE | DOI: 10.1109/IV55156.2024.10588863

This work is supported in part by the National Key R&D Program above methods, MARL is promising to resolve these defects of China under Grant 2021ZD0112700, in part by the National Natural by enabling CAVs to make rapid decisions with respect Science Foundation of China under Grant 62271351, 62125101, 62201390, to the sophisticated ambience \[10\] \[11\] \[12\]. By efficient and 62341101, in part by the Natural Science Foundation of Shanghai under Grant 22ZR1463600, in part by the Chenguang Program of Shanghai inter-vehicle cooperation, MARL-based methods can avoid Education Development Foundation and Shanghai Municipal Education collisions and minimize passing delays with high scalability. 

Commission under Grant 21CGA24, in part by the New Cornerstone Science In addition, CAV heterogeneity is another vital challenge Foundation through the XPLORER PRIZE, and the Fundamental Research Funds for the Central Universities. 

in practical AIM problems. As shown in Fig. 1, due to the Kaixin Chen, Bing Li, and Rongqing Zhang are with the School of common variations of vehicle models in reality, CAVs usually Software Engineering, Tongji University, Shanghai 200092, China \(e-mail: manifest differences in dynamic features like width, length, 2333108@tongji.edu.cn; lizi@tongji.edu.cn; rongqingz@tongji.edu.cn\). 

Xiang Cheng is with the School of Electronics, Peking University, Beijing acceleration capacity, etc. Moreover, CAVs also exhibit per-100871, China \(e-mail: xiangcheng@pku.edu.cn\). 

ceptual inconsistencies in observation dimensions and messa-979-8-3503-4881-1/24/$31.00 ©2024 IEEE

**2255**

Authorized licensed use limited to: Universidade Estadual da Paraiba \(UEPB\). Downloaded on January 22,2025 at 06:40:40 UTC from IEEE Xplore. Restrictions apply. 





Downloaded from https://iranpaper.ir https://www.tarjomano.com

https://www.tarjomano.com

ge permutation. These heterogeneous factors amplify the with the vehicular control scheme, vehicles can be catego-difficulty of AIM, as the cooperative methods are required rized into two types, including the CAVs controlled by stand-to deliver suitable control schemes for different types of alone decision-making algorithms, and the human-driven CAVs under varying message contexts acquired through connected vehicles \(HCVs\) with actions determined by the instant communications. Most recent works have discussed drivers’ instant reactions. All vehicles are able to acquire the scheduling of heterogeneous CAVs in traffic scenarios their spatial coordinates and kinematics state, subsequently like on-ramp and highway \[13\] \[14\]. But to the authors’

sharing these data with neighboring vehicles through V2V

knowledge, no existing works explore the AIM under the communications within a limited range. In this scenario, each more practical heterogeneous scenario. Current methods on CAV is required to leverage the aggregated information to AIM still follow the homogeneous assumption, wherein all maintain its ego trajectory while collaborating with adjacent CAVs are consistent without model distinctions. However, vehicles for proactively addressing latent conflicts. 

simply adapting identical control methods on diverse CAVs B. Vehicular Kinematics

may cause adverse consequences. 

Taking the heterogeneity of CAVs into consideration, in The fundamental kinematics properties of each vehicle this work, we for the first time investigate the AIM problem are calculated by the kinematic bicycle model \[17\]. For the in a more practical intersection scenario with multiple het-CAVs piloted by the algorithm policy that outputs the high-erogeneous CAVs. To achieve efficient and effective decision-level steering and acceleration action signal, two low-level making in intricate ambiences, we employ MARL to achieve controllers are implemented to obtain vehicular movements at real-time AIM and model the decision-making process of the longitudinal and lateral level. The longitudinal controller each CAV as a partially observable Markov decision process utilizes a simple proportional relationship to manage the \(POMDP\). However, despite the superiority of MARL solu-vehicle’s acceleration:

tions in complex real-time interactions, existing MARL meth-1

a =

\(vr − v\)

\(1\)

ods \[15\] \[16\] may undergo a performance decline owing to τp

the deficiency in structural adaptability in heterogeneous en-where a is the vehicle numerical acceleration, v, vr are the vironments. In response, we propose a novel heterogeneous-vehicle velocity and the reference velocity, respectively, and agent attention gated trust region policy optimization \(HAG-1

is the controller proportional gain. The lateral controller TRPO\) method to achieve an effective cooperative decision-τp

conducts the vehicle’s position control, which can be repre-making among heterogeneous CAVs. Specifically, the pro-sented by:

posed method employs a sequential update schema grounded 1

v

∆

in the multi-agent advantage decomposition lemma during lat,r = −

lat

τp,lat

\(2\)

training to assure heterogeneity elasticity. Additionally, it vlat,r

∆ψ

\)

boosts vehicular cognition of complex ambiences and la-r = arcsin\(

v

tent dependencies by utilizing attention-based observation as well as the vehicle’s heading control represented by: aggregation impervious to shuffled input order, while com-prehending potential historical traffic status with the gate ψr = ψL \+ ∆ψr

recurrent unit \(GRU\). Extensive experiments are conducted

˙

1

ψr =

\(ψr − ψ\)

in general AIM scenarios, including both homogeneous and τ

\(3\)

p,ψ

heterogeneous cases. The numerical results demonstrate that 1 l

δ = arcsin \(

˙

ψ

compared with existing rule-based and MARL-based meth-r \)

2 v

ods, our proposed method facilitates CAVs collaborations at where ∆lat is the lateral position of the vehicle relative to the intersection with fewer collisions and faster traffic flow, the lane center-line, vlat,r is the lateral velocity command, indicating the superiority of our proposed method in both

∆ψr is a heading variation to apply the lateral velocity safety and efficiency. 

command, ψL is the lane heading, ψr is the target heading The rest of the paper is organized as follows. Section II to follow the lane heading and position, ˙

ψr is the yaw rate

illustrates the AIM problem formulation regarding general command, 

1

, 

1

are the position and heading control τ

τ

traffic settings and vehicular kinematics. Section III proposes p,lat

p,ψ

gains, respectively, and δ is the front wheels angle control. 

our MARL-based method for AIM and Section IV verifies the For the HCVs, the intelligent driver model \(IDM\) \[18\] is performance of our method with other benchmarks. Section applied for human-driver-simulated behavior control: V concludes this paper. 



v

d∗



˙v = a 1 − \(

\)δ − \(

\)2

II. PROBLEM FORMULATION

v0

d

\(4\)

A. General Traffic Settings

v∆v

d∗ = d0 \+ T v \+ √

Consider a four-direction unsignalized intersection de-2 ab

picted in Fig. 1. Various vehicles approach the intersection where v is the vehicle velocity vector, d is the distance to its from any of the four driveway at distinct time steps, and front vehicle, v0 is the desired velocity, T is the desired time their exit directions are randomly predefined from options gap, d0 is the jam distance, a, b are the maximum acceleration including left turn, straight-ahead or right turn. In accordance and deceleration, and δ is the velocity exponent. 

**2256**

Authorized licensed use limited to: Universidade Estadual da Paraiba \(UEPB\). Downloaded on January 22,2025 at 06:40:40 UTC from IEEE Xplore. Restrictions apply. 





Downloaded from https://iranpaper.ir https://www.tarjomano.com

https://www.tarjomano.com

Fig. 2. The overview of HAG-TRPO cooperative AIM structure TABLE I

angle, and Vn is a dynamic set representing the vehicles VEHICLE MODELS AND COEFFICIENTS

within the observation radius of agent n at time step t. 

3\) Action: Every CAV selects one action from the action set Model Type

V-T1

V-T2

τ

\{cruise, slower, f aster\}, subsequently processed by low-p \(s\)

0.4

0.8

τp,lat \(s\)

0.4

0.8

level controllers to obtain the steering and acceleration. 

τp,ϕ \(s\)

0.2

0.4

4\) Reward: the reward of CAV n at time step t is: vehicle length \(m\)

5.0

6.5

vehicle width \(m\)

1.8

2.4

vt − v

n

min

\(6\)

max speed \(m/s\)

30

25

rt = η

\+ η

n

1

2et

v

n

max − vmin

max observed vehicle

7

5

where etn is a mutable signal \(1 for arrival reward, -5 for collision penalty, and 0 for other cases\). The reward encourages III. MULTI-AGENT REINFORCEMENT LEARNING-BASED

safe driving while sustaining relatively high speed. 

METHOD FOR AIM

B. Cooperative Strategy for AIM with Heterogeneous CAVs A. POMDP Problem Formulation

1\) Sequential Updating Structure: As general AIM in-Due to the sequential nature of intersection decision-volves cooperation between agents with diverse models, making and the demand of efficient cooperation, we model there necessitates a training schema with strong compatibility the AIM problem as a POMDP. At time step t, agent n for variously-structured agent policies to process sampled receives a localized observation O

messages while acquiring a decent performance. In response, n with a reward signal

r

we implement the multi-agent trust region optimization algo-n, subsequently executing an action an through its policy module π

rithm \(TRPO\) \[19\] shown in Fig. 2. It provides a sequential n to interact with the environment. The elementary definition of the system is as follows: updating method during sampling, and promotes an MARL

1\) Agent: Each CAV is designated as an agent in the system cooperative structure ensuring monotone improvement. The to pass the intersection. We consider two types of CAVs multi-agent TRPO method is theoretically supported by the \(named V-T1 and V-T2\) that differ in dynamic property and multi-agent advantage decomposition lemma: perception input to discuss vehicular heterogeneity. The ve-n

X

hicular dynamics and perception coefficients regarding model Ai1:n \(s, ai1:n \) =

Aim \(s, ai1:m−1 , aim \)

π

π

\(7\)

V-T1 and V-T2 are displayed in Table I. Compared with V-m=1

T1, V-T2 exhibits larger size, bulkier speed and acceleration where i1:n is the agent subset \{i1, i2, ..., in\} in a specific control, as well as relatively weaker perceptual capability. 

order, Ai1:n

π

is the advantage function taking the form of the 2\) Observation: During each time step, each CAV observes generalized advantage estimation \(GAE\) \[20\], and ai1:n is its pose and kinematic information through sensors and V2V

the joint actions taken by agents from number 1 to n. After messages transmitted by adjacent vehicles. The observation the buffer collects T steps of trajectory data at episode e, Ot

the advantage estimator of agent n can be calculated in a n of the CAV n at the time step t can be expressed as: sequential manner:

Ot = \{ty

, vt , headt , tyt , loct , vt , headt \}

n

n, loctn

n

n

V

\(5\)

n

Vn

Vn

Vn

 Â



s,a \(s, a\) , 

n = 1

where tyn is the integer descriptor of the vehicle model type Mi1:n \(s, a\) =

πn−1 \(an−1|sn−1\)

θe\+1

t

t

of agent n, loct

Mi1:n−1 \(s, a\)

n > 1



n is the location coordinates at time step t, vt n

πn−1\(an−1|sn−1\)

θe

t

t

is the velocity vector, headtn denotes the vehicular heading \(8\)

**2257**

Authorized licensed use limited to: Universidade Estadual da Paraiba \(UEPB\). Downloaded on January 22,2025 at 06:40:40 UTC from IEEE Xplore. Restrictions apply. 





Downloaded from https://iranpaper.ir https://www.tarjomano.com

https://www.tarjomano.com

where π

, π

is the origin and updated policy of agent agent-heterogeneous AIM \(abbreviated to HET\), two V-T1

θn−1

e

θn−1

e\+1

n − 1, respectively. Then the gradient of agent n’s policy g agents and two V-T2 agents are employed. For both scenarios, can be estimated by:

the system randomly generates a set of HCVs, each with an intended destination, to pass through the intersection. The B

T

1 X X

ˆ

gin =

∇

log π

ain |oin Mi1:n \(s

experiment parameters is showed in Table II. 

e

t,at\)

\(9\)

B

θin

t

t

e

θin

e

b=1 t=1

B. Performance Benchmark

where B is the batch size. To conduct a TRPO step, the Hes-1\) TTC: Rule-based baseline \[2\]. Assuming that all obsian matrix of the average Kullback-Leibler \(KL\) divergence served vehicles maintain their trajectories with constant DKL from the old policy H should be computed so as to speed and heading, each CAV predicts the duration of obtain the update direction:

the upcoming collision, enabling them to decelerate B

T

when TTC falls below a safe threshold and speed up în

1 X X





H

= ∇2

D

π

·|oin , π

·|oin 

e

θin

KL

otherwise. 

BT

θin

t

θin

t

e

b=1 t=1

2\) C-MAPPO: Multi-agent proximal policy optimization \(10\)

\(MAPPO\) under the cooperative centralized training The policy parameters of agent n is finally updated with: and decentralized execution \(CTDE\) schema \[12\]. 

v

u

2δ



i

CAVs update the policy individually through PPO \[?\]

n −1

θin

= θin \+ αj

û

H

gin

e\+1

e

e

e

t



i

\(11\)

under the guidance of the centralized value network n −1

gin

ê

H

gin

e

e

during training. In the execution stage, CAVs can act independently with their policy networks without value where α is a positive backtracking coefficient determined by instructions. 

line search, and δ is the threshold value of KL-divergence 3\) A-MAPPO: MAPPO with the attention mechanism in constraint. Meanwhile, The global critic network ϕ that policy modules. CAVs aggregate the received messages outputs the value of current state V is updated by minimizing through the attention layer to extract the latent relations the optimization objective function. It is shown as: of neighboring vehicles. 

B

T

1 X X 

2

ϕe\+1 = arg min

Vϕ\(st\) − ˆ

Rt

\(12\)

ϕ

BT

TABLE II

b=1 t=0

EXPERIMENT PARAMETERS

2\) Attention Mechanism for Policy Module: To enhance CAV’s capability in perceiving latent intentions of varying Parameter

Value

clip threshold

0.2

nearby vehicles from disordered V2V messages, we employ discount factor γ

0.99

self-attention mechanism to the actor network πθin of each learning rate \(actor\)

0.005

CAV. As displayed in Fig. 2, the attention layer takes in learning rate \(critic\)

0.005

number of steps per episode

2000

the observation embedding and trains the matrices of ego time step limit per round

120

query WQ, collective key WK and collective value WV . The simulation frequency \(Hz\)

5

weighted attention atti of agent i can be obtained by: Nh

X

\(WQei\)\(WK eh\)T

att

Algorithm 1 HAG-TRPO

i =

softmax\(

√

\)h\(WV eh\)

\(13\)

d

h=1

k

Initialize actor and critic network parameters θi1:N , ϕ. 

where N

Initialize total training episodes E, replay buffer B. 

h

is the number of attention heads, dk is the embedding dimension, e

Initialize the time step limit per round T . 

h is the embedding and h\(·\) is the activate function. 

for episode e = 0, 1, ..., E − 1 do 3\) Temporal Module for Critic Network: As the potential for step t = 0, 1, ..., T − 1 do

conflicts among vehicles can be inferred from historical Get observation Ot from the environment and vehicular pose information sequentially, we implement a light actions At from attention-based policies. 

gate recurrent unit \(GRU\) into the global critic network ϕ to Get changed observation ˜

Ot and reward Rt. 

capture the temporal correlation within vehicles efficiently. 

Store tuple \(Ot, At, Rt, ˜

Ot\) into buffer B. 

end for

IV. SIMULATION AND RESULTS

Retrieve a minibatch of experience B from buffer B. 

A. Scenario Setups

Calculate initial advantage function M i1:1 with \(8\). 

for agent i

Based on the traffic settings illustrated in II-A and the n = i1, ..., iN do

Obtain the Hessian of KL-divergence with \(10\). 

vehicle settings illustrated in Table I, the AIM simulation Update the actor network π

is constructed utilizing an intersection gym-based simulator θin with \(11\). 

Compute M i1:n\+1 with \(8\). 

\[21\]. The scenarios are categorized into two types contingent end for

upon the model configurations of the four CAV agents. In Update the critic value network V

the agent-homogeneous AIM \(abbreviated to HOM\), all four ϕ with \(12\). 

end for

CAVs are modeled as V-T1 consistently. Whereas for the **2258**

Authorized licensed use limited to: Universidade Estadual da Paraiba \(UEPB\). Downloaded on January 22,2025 at 06:40:40 UTC from IEEE Xplore. Restrictions apply. 





Downloaded from https://iranpaper.ir https://www.tarjomano.com

https://www.tarjomano.com

C. Performance Evaluation

the strong assumption that observed vehicles maintain their \(1\) Reward: Fig. 3 depicts the convergence of the episode current velocity and heading, thus struggles to predict others’

reward among all learning-based methods under HOM and intentions when multiple vehicles interact simultaneously. 

HET scenarios. All algorithms are initialized with random Both HAG-TRPO and A-MAPPO benefit from the atten-parameters, and their initial rewards tend to gather around low tion mechanism in learning the inter-vehicle weighted rele-values indicating frequent collisions and few success cases. 

vance and improving traffic safety, as their non-collision rates generally surpass those of C-MAPPO and TTC. Specifically, HAG-TRPO yields a 76.7% non-collision rate in HOM-AIM, similar to A-MAPPO \(75.6%\). Whereas in HET-AIM, HAG-TRPO achieves the highest non-collision rate \(75.1%\), and exhibits the minimal performance degradation while other learning-based methods encounter an evident decrease. This proves that our proposed method exhibits its elasticity in handling complex scenarios by learning from prerequisite advantages for the current agent. 

Fig. 3. The total reward per episode of all MARL-based methods As their reward curve converge, it can be observed that HAG-TRPO and A-MAPPO exhibit similar performances in HOM-AIM, and both of them outperform C-MAPPO with higher rewards. This shows that agents equipped with the attention module have enhanced performance in sensing latent conflicts through disordered messages to avoid collisions through reasonable actions. 

Compared with HOM-AIM, we notice an overall decrease of reward in HET-AIM due to its intricacy introduced by the vehicular divergence in dynamics and perception. Nonetheless, the HAG-TRPO method still achieves the highest reward with an obvious positive performance gap compared with the other MARL-based methods, as agents can update their Fig. 5. CAV’s non-collision rate of all methods in Heterogeneous AIM

policies with previous advantages considering heterogeneity. 

For the individual safety, we assess the non-collision rate of \(2\) Safety: We proceed 30 rounds of fixed-time experi-a single CAV concerning various vehicle types in HET-AIM

ments for all mentioned methods. Within each round, we to verify the algorithmic coverage on account of vehicular conduct a 10000-step traffic simulation, wherein CAVs and variability. Through Fig. 5, we observe a general decline on HCVs interact to resolve conflicts and reach their desired exit V-T2 non-collision rate for learning-based methods compar-lane. The general traffic safety metric is depicted from both ing to V-T1 due to the bulkiness in size, kinematic control holistic and individual perspectives. 

and perception capacity of V-T2 agents, along with the challenges posed by optimizing heterogeneous agents. Under the CTDE schema, C-MAPPO and A-MAPPO demonstrate the effectiveness of RL-based methods in learning to cooper-ate by achieving 80.3% and 90.3%. However, they conduct the policy-update tactics without specialized adaptation to heterogeneous agents, leading to their performance drop by 22.2% and 17.3% in V-T2 non-collision rate. Nonetheless, V-T2 agents driven by HAG-TRPO are able to leverage pre-ordinal advantage from V-T1 agents. This helps minimize the heterogeneity learning defect, leading to a superior performance compared to A-MAPPO, C-MAPPO, and TTC, with Fig. 4. The intersection holistic non-collision rate of all methods respective improvements of 10.5%, 25.4%, and 39.3%. 

The holistic intersection safety is described numerically \(3\) Efficiency: We record the total passing delays for 1500

with the overall non-collision rate, which represents the CAVs to pass through the intersection. Within each episode, proportion of episodes in which all CAVs successfully pass the arrival time cost of each vehicle is added to the total de-the intersection without collisions, relative to the total number lays elapsed since the previous episode. In addition, episodes of episodes. As shown in Fig. 4, the average non-collision with collisions are assigned a time penalty equivalent to the rate of TTC stands at merely 28.5% for HOM-AIM and maximum time step of a testing round to punish vehicular 26.1% for HET-AIM. The reason is that TTC relies on hastiness. The maximum time step is set to 100000. 

**2259**

Authorized licensed use limited to: Universidade Estadual da Paraiba \(UEPB\). Downloaded on January 22,2025 at 06:40:40 UTC from IEEE Xplore. Restrictions apply. 





Downloaded from https://iranpaper.ir https://www.tarjomano.com

https://www.tarjomano.com

\[2\] R. Van der Horst and J. Hogema, “Time-to-collision and collision avoidance systems,” Verkeersgedrag in Onderzoek, pp. 59–66, Jan. 

1994. 

\[3\] F. D. Salim, L. Cai, M. Indrawan, and S. W. Loke, “Road intersections as pervasive computing environments: towards a multiagent real-time collision warning system,” in Proc. 6th Annu. IEEE Int. Conf. Pervasive Comput. Commun. \(PerCom\), Hong Kong, China, Mar. 2008, pp. 621–

626. 

\[4\] M. Cai, Q. Xu, C. Chen, J. Wang, K. Li, J. Wang, and X. Wu, “Multi-lane unsignalized intersection cooperation with flexible lane direction based on multi-vehicle formation control,” IEEE Trans. Veh. Technol., vol. 71, no. 6, pp. 5787–5798, Jun. 2022. 

\[5\] X. Pan, B. Chen, S. Timotheou, and S. A. Evangelou, “A convex optimal control framework for autonomous vehicle intersection crossing,” 

IEEE Trans. Intel. Transp., vol. 24, no. 1, pp. 163–177, Jan. 2023. 

\[6\] H. Xu, Y. Zhang, L. Li, and W. Li, “Cooperative driving at unsignalized intersections using tree search,” IEEE Trans. Intel. Transp., vol. 21, no. 11, pp. 4563–4571, Nov. 2020. 

\[7\] A. Mirheli, M. Tajalli, L. Hajibabai, and A. Hajbabaie, “A consensus-Fig. 6. Total passing delays for successful passage of vehicles based distributed trajectory control in a signal-free intersection,” 

Transp. Res. Part C Emerg. Technol., vol. 100, pp. 161–176, Mar. 

2019. 

The experiments are carried out in the same initial state

\[8\] Y. Hou, Z. Wei, R. Zhang, X. Cheng, and L. Yang, “Hierarchical with zero CAVs arrival count. As CAVs gradually arrive, the task offloading for vehicular fog computing based on multi-agent deep reinforcement learning,” IEEE Trans. Wireless Commun., pp. 1–1, 01

accumulate traffic delay increases in each algorithm, reveal-2023. 

ing their performance disparities. As shown in Fig 6, the TTC

\[9\] Z. Wei, B. Li, R. Zhang, X. Cheng, and L. Yang, “Many-to-many task method fails to complete 1500 CAVs’ scheduling within a offloading in vehicular fog computing: A multi-agent deep reinforcement learning approach,” IEEE Trans. Mobile Comput., vol. 23, no. 3, limited time steps of 100000 as it frequently causes collisions pp. 2107–2122, 2024. 

that encumber the traffic efficiency. In HOM-AIM cases, 

\[10\] G.-P. Antonio and C. Maria-Dolores, “Multi-agent deep reinforcement HAG-TRPO and A-MAPPO finish 1500 CAVs’ passings learning to manage connected autonomous vehicles at tomorrow’s intersections,” IEEE Trans. Veh. Technol., vol. 71, no. 7, pp. 7033–

in 40848 and 41115 time steps, respectively, both superior 7043, Jul. 2022. 

to C-MAPPO. However, in HET-AIM caes, A-MAPPO’s

\[11\] C. Huang, J. Zhao, H. Zhou, H. Zhang, X. Zhang, and C. Ye, “Multi-performance is degraded due to the complexity in scenarios agent decision-making at unsignalized intersections with reinforcement learning from demonstrations,” in Proc. 34th IEEE Intell Veh Symp with agent-level disparities, resulting in a time-consuming \(IV\), Anchorage, AK, United states, Jun. 2023, pp. 1–6. 

passage of 56032 for total passing delays. Whereas, HAG-

\[12\] J. Zheng, K. Zhu, and R. Wang, “Deep reinforcement learning for TRPO achieves merely 45450 passing delays in HET-AIM, autonomous vehicles collaboration at unsignalized intersections,” in Proc. IEEE Glob. Commun. Conf. \(GLOBECOMM\), Virtual, Online, indicating an efficiency increase of 23.3% over A-MAPPO. 

Brazil, Dec. 2022, pp. 1115–1120. 

This is attributed by the advanced cooperation of HAG-

\[13\] J. Liu, W. Zhao, C. Wang, C. Xu, L. Li, Q. Chen, and Y. Lian, TRPO, wherein CAVs notice inter-agent latent discrepan-

“Eco-friendly on-ramp merging strategy for connected and automated vehicles in heterogeneous traffic,” IEEE Trans. Veh. Technol., vol. 72, cies on current velocity and acceleration capacity through no. 11, pp. 13 888–13 900, 2023. 

advantage-based sequential update. This enables them to

\[14\] A. Coppola, D. G. Lui, A. Petrillo, and S. Santini, “Eco-driving determine a viable plan for conducting an efficient passing. 

control architecture for platoons of uncertain heterogeneous nonlinear connected autonomous electric vehicles,” IEEE Trans. Intel. Transp., V. CONCLUSION

vol. 23, no. 12, pp. 24 220–24 234, 2022. 

\[15\] T. Rashid, M. Samvelyan, C. Schroeder, G. Farquhar, J. Foerster, and In this paper, our study addressed the challenge of ve-S. Whiteson, “Qmix: Monotonic value function factorisation for deep hicle heterogeneity in AIM with multiple heterogeneous multi-agent reinforcement learning,” in Proc. 35th Int. Conf. Mach. 

Learn. \(ICML\). 

Stockholm, Sweden: PMLR, 2018, pp. 4295–4304. 

CAVs. To collaborate effectively under agent heterogene-

\[16\] C. Yu, A. Velu, E. Vinitsky, J. Gao, Y. Wang, A. Bayen, and ity, we proposed an MARL-based cooperation method that Y. Wu, “The surprising effectiveness of PPO in cooperative multi-exploits the sequential update schema for policy networks agent games,” 36th Adv. Neural Inf. Proces. Syst. \(NIPS\), vol. 35, pp. 

24 611–24 624, Dec. 2022. 

based on the multi-agent advantage decomposition lemma

\[17\] P. Polack, F. Altché, B. d’Andréa-Novel, and A. de La Fortelle, “The to boost flexibility on heterogeneous AIM, while applying kinematic bicycle model: A consistent model for planning feasible the attention mechanism to reinforce vehicular perception trajectories for autonomous vehicles,” in Proc. 28th IEEE Intell Veh Symp \(IV\), Redondo Beach, CA, United states, Jun. 2017, pp. 812–818. 

on complicated surroundings. In addition, we implemented

\[18\] M. Treiber, A. Hennecke, and D. Helbing, “Congested traffic states a temporal module to capture the implicit relevance for en-in empirical observations and microscopic simulations,” Phys. Rev. E, hanced comprehension of the global status. Numerical results Stat. Phys. Plasmas Fluids Relat., vol. 62, no. 2, p. 1805, Aug. 2000. 

\[19\] J. G. Kuba, R. Chen, M. Wen, Y. Wen, F. Sun, J. Wang, and affirmed that our proposed method proceeds intersection tasks Y. Yang, “Trust region policy optimisation in multi-agent reinforcement with faster traffic flow and high safety standard in both learning,” in Proc. 10th Int. Conf. Learn. Represent. \(ICLR\), Virtual, homogeneous and heterogeneous scenarios. 

Online, Apr. 2022, p. 1046. 

\[20\] J. Schulman, P. Moritz, S. Levine, M. Jordan, and P. Abbeel, “High-REFERENCES

dimensional continuous control using generalized advantage estimation,” in Proc. 4th Int. Conf. Learn. Represent. \(ICLR\), San Juan, Puerto

\[1\] K. Dresner and P. Stone, “Multiagent traffic management: A rico, May 2016. 

reservation-based intersection control mechanism,” in Proc. 3rd Int. 

\[21\] E. Leurent, “An environment for autonomous driving decision-Jt. Conf. Auton. Agents Multiagent Syst. \(AAMAS\), New York, NY, making,” GitHub repository, 2018. 

United states, Jul. 2004, pp. 530–537. 

**2260**

Authorized licensed use limited to: Universidade Estadual da Paraiba \(UEPB\). Downloaded on January 22,2025 at 06:40:40 UTC from IEEE Xplore. Restrictions apply.



