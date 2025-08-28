Transportation Research Part C 167 \(2024\) 104807 

Contents lists available at ScienceDirect

Transportation Research Part C

journal homepage: www.elsevier.com/locate/trc

Reasoning graph-based reinforcement learning to cooperate mixed

connected and autonomous traffic at unsignalized intersections

Donghao Zhou , Peng Hang , Jian Sun \*

*Department of Traffic Engineering & Key Laboratory of Road and Traffic Engineering, Ministry of Education, Tongji University, Shanghai, China* A R T I C L E I N F O

A B S T R A C T

*Keywords:*

Cooperation at unsignalized intersections in mixed traffic environments, where Connected and Connected and automated vehicle

Autonomous Vehicles \(CAVs\) and Manually Driving Vehicles \(MVs\) coexist, holds promise for Cooperative plan

improving safety, efficiency, and energy savings. However, the mixed traffic at unsignalized in-Unsignalized intersections

tersections present huge challenges like MVs

Mixed traffic system

’ uncertainties, the chain reaction and diverse in-

teractions. Following the thought of the situation-aware cooperation, this paper proposes a Reasoning Graph-based Reinforcement Learning \(RGRL\) method, which integrates a Graph

Neural Network \(GNN\) based policy and an environment providing mixed traffic with uncertain behaviors. Firstly, it graphicly represents the observed scenario as a situation using the interaction graph with connected but uncertain \(bi-directional\) edges. The situation reasoning process is formulated as a Reasoning Graph-based Markov Decision Process which infers the vehicle sequence stage by stage so as to sequentially depict the entire situation. Then, a GNN-based policy is constructed, which uses Graph Convolution Networks \(GCN\) to capture the interrelated chain reactions and Graph Attentions Networks \(GAT\) to measure the attention of diverse interactions. 

Furthermore, an environment block is developed for training the policy, which provides trajectory generators for both CAVs and MVs. A reward function that considers social compliance, collision avoidance, efficiency and energy savings is also provided in this block. Finally, three Reinforcement Learning methods, D3QN, PPO and SAC, are implemented for comparative tests to explore the applicability and strength of the framework. The test results demonstrate that the D3QN outperformed the other two methods with a larger converged reward while maintaining a similar converged speed. Compared to multi-agent RL \(MARL\), the RGRL approach showed superior performance statistically, reduced the number of severe conflicts by 77.78–94.12 %. The RGRL reduced average and maximum travel times by 13.62–16.02 %, and fuel-consumption by 3.38–6.98 % in medium or high Market Penetration Rates \(MPRs\). Hardware-in-the-loop \(HIL\) and Vehicle-in-the-loop \(VehIL\) experiments were conducted to validate the model effectiveness. 

**1. Introduction**

Unsignalized intersections have long been recognized as bottlenecks in urban traffic, contributing to approximately 30 % of accidents and 20 % of Fatalities \(Fedral Highway Administration, 2023; National Center for Statistics Analysis, 2022\). The major concern lies in the large number, diverse nature, and wide distribution of interactions or conflicts. The development of Autonomous

\* Corresponding author. 

*E-mail address: *sunjian@tongji.edu.cn \(J. Sun\). 

https://doi.org/10.1016/j.trc.2024.104807

Received 9 October 2023; Received in revised form 3 August 2024; Accepted 5 August 2024

Available online 22 August 2024 

0968-090X/© 2024 Elsevier Ltd. All rights are reserved, including those for text and data mining, AI training, and similar technologies. 

*D. Zhou et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104807* 

Intersection Management \(AIM\) offers a promising solution by introducing Connected and Autonomous Vehicles \(CAVs\) to manage these interactions, leading to improve the safety, efficiency, and fuel consumption of intersections. However, there is a transition period when both manually driven vehicles \(MVs\) and CAVs coexist, known as mixed traffic environments \(Karimi et al., 2020\). The AIM methods that purely focused on CAVs’ trajectories may result in CAVs’ socially non-compliant driving in mixed traffic environments. Such behavior not only undermines the efficiency of CAVs but also increases the risk of road rage, traffic deadlock, and accidents involving other drivers \(Noh, 2019; Zhan et al., 2016\). 

The critical issue is how to cooperate the CAVs considering both unsignalized intersections and mixed traffic environments. 

Numerous challenges arise in this scenario. Firstly, the inherent uncertainty of MVs leads to multiple possible intentions and trajectories, resulting in multi-modal behavior patterns. Reacting in real-time to these modal changes is a significant challenge. Furthermore, unsignalized intersections witness numerous interactions that trigger a cascade of chain reactions. Numerous interrelated chain reactions form a chain reaction web, making it difficult to track vehicles’ influences because even the slightest change in one vehicle’s behavior can have far-reaching consequences on other vehicles. Last but not least, each CAV has to simultaneously interact with a diverse range of vehicles, including both CAVs and MVs, each with different motion states. How to measure the attention to these diverse interactions further adds to the challenge. 

Previous studies try to tackle the problem using policies, rules, optimization or Reinforcement Learning \(RL\) methods. Firstly, some policies propose to prohibit high-traffic mixed traffic at unsignalized intersections, or strictly define the right-of-way of different traffics. However, they are limited in control precision so that struggle to address the safety risks arising from conflicting interactions in mixed traffic environments. Some studies propose reserving the right of way for upcoming vehicles in conflict areas to ensure collision-free scenarios \(Dresner and Stone, 2008; Huang et al., 2012; Zhang et al., 2015\). However, these reservation-based methods often rely on strategies and may fall short in guaranteeing system optimality. Besides, once a reservation is made, the plan does not adjust to accommodate the uncertain behaviors of manually driving vehicles \(MVs\), which can deviate significantly from expectations. 

Alternatively, other studies aim for systemic optimization by formulating mathematical programming to solve high-level decisions or vehicle trajectories \(Chen et al., 2022; Jiang et al., 2023a; Pan et al., 2023; Yao et al., 2023\). Nonetheless, interactions, especially crossings, introduce higher-order dynamics and nonconvexity to the programming, which make it hard to real-time react to MV’s uncertainties and modal changes. More recently, some studies have explored Reinforcement Learning \(RL\) to achieve real-time optimal solution. However, few studies have specifically addressed the challenges posed by interactions with uncertainties. MVs’

uncertainties will propagate globally through the chain reaction web. The Markov Decision Process \(MDP\) that defines vehicle’s control or passing order is hard to track the uncertainties. Moreover, the social compliance of CAVs’ actions further complicates the problem. 

Our previous work proposed a situation-aware method called Reasoning Graph for the multi-modal problem \(Zhou et al., 2022\). A situation was defined as an all-encompassing set of circumstances that dictate the selection of an applicable behavioral pattern, and in turn, entails the corresponding intention required for that chosen behavior \(Schuldt et al., 2015\). The intention here refers to the vehicle’s decision to either proceed or yield to conflicting vehicles at the unsignalized intersection. Since each vehicle can choose from several possible intentions, the combination of different intentions leads to multiple situations. By considering specific situations, the uncertainty associated with the behavior of MVs can be significantly reduced, while socially compliant mechanism can be integrated into the situation. So the work firstly presented the interaction graph to represent the interactions among vehicles from two platoons. 

By employing graph search, it reasoned about all possible situations through combinations of vehicles’ intentions. Finally, it calculated the utilities of these situations and selected the maximum-utility one as the target plan. 

**Fig. 1. **Overview for Reasoning Graph-based Reinforcement Learning \(RGRL\). 

2 

*D. Zhou et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104807* 

However, our previous study has certain limitations when it comes to unsignalized intersections. Firstly, the wide distributed interactions will exponentially increase the number of situations. The previous method is essentially relied on search algorithms. 

However, the search-based situation reasoner fails to traversal in such a large solution space. Secondly, the chain reaction web happened on unsignalized intersections further complicates the task of quantifying the influence of one vehicle’s behavior on another interacting vehicle, and measuring the attention paid to multiple influences. Last but not least, the original method’s failure to consider historical information leads to limited contextual understanding and an inability to recognize long-term trends, making it less reliable for decision-making over a long-time range. 

This study introduces an innovative framework known as Reasoning Graph Reinforcement Learning \(RGRL\). This framework reformulates situation reasoning as a Reasoning Graph-based Markov Decision Process to enable real-time reasoning. As demonstrated in Fig. 1, the **observation **is graphically represented as a situation in the initial reasoning stage, k = 0, using an interaction graph with connected yet uncertain \(bi-directional\) edges. The **action policy**, constituting of Graph Convolutional Network \(GCN\) and Graph Attention Network \(GAT\) as its backbone, extracts relevant features from the graph and produces an action that selects a target vehicle in the current reasoning stage k. This stage, k, denotes the priority of the target vehicle. As such, the uncertain edges related to the target vehicle are replaced by certain \(directional\) edges, resulting in the **staged situation**. This decision-making process iterates stage by stage until all uncertain edges turn into certain ones, culminating in the completion of situation reasoning. Throughout this process, the action policy undergoes consistent updates based on the reward, which is calculated considering the trajectory of the target vehicle. 

The contributions of this research can be summarized as follows:

\(1\) The study introduces an innovative framework called RGRL, which formulates the situation reasoning process as a Reasoning Graph-based MDP. It integrates the strengths of Reasoning Graphs for addressing multimodal problems with the capabilities of Reinforcement Learning \(RL\) for making real-time decisions, deciding the optimal situation in a space where situation candidates explosive grew in numbers

\(2\) The study integrates GNN with the graph reasoning process. It contributes to capturing the features of the chain reaction patterns, and mitigating the uncertainty inherent in stage-wise decision-making scenarios. 

\(3\) The study utilizes Graph Convolutional Network \(GCN\) to simulate the mechanism of the chain reaction, where each vehicle’s behavior characterized by a node feature will spread to its interactive vehicles. The study uses Graph Attention Network \(GAT\) to designate attention coefficients, which signify the intensity of the interactions considering the varied states and types of interactive vehicles. 

To explore the applicability and strength of the framework, three popular reinforcement learning methods, Double Dueling DQN

\(D3QN\), Proximal Policy Optimization \(PPO\) and Soft Actor-Critic \(SAC\), were implemented. Besides, comparative tests with multiagent RL \(MARL\) were conducted. 

The rest of this paper is organized as follows. Section 2 presents a literature review of existing studies for the CAV cooperation. In

Section 3 we formulate the cooperation problem. Section 4 introduces the methodology in detail. Section 5 presents some tests and analyzes the results. Finally, Section 6 presents a conclusion and a direction for future studies. 

**2. Literature review**

The scale, dimensions, and complexity of cooperation at isolated intersections differ depending on the traffic signal setting \(signalized or unsignalized\) and the control distribution \(centralized or decentralized\). In general, the methods employed for addressing this cooperation can be categorized into three types: reservation-based methods, mathematical programming, and Reinforcement Learning. 

*2.1. Reservation-based methods*

Reservation-based approaches have long been considered as classical methods for cooperation at intersections. The concept was initially introduced by Dresner and Stone \(2008\). In their approach, each vehicle acted as an agent, requesting permission to occupy specific space–time cells within designated time intervals to cross the intersection. The approach followed a first-come-first-serve \(FCFS\) policy, which was straightforward and efficient. However, it had limitations in handling high demand levels and conflicting traffic streams. The fairness-oriented nature of the FCFS policy could lead to performance degradation. 

To address these limitations, Huang et al. \(2012\) proposed an extension to the reservation-based approach by introducing a priority strategy. They centralized the computation of vehicle trajectories to minimize the chances of reservation cancellations. Their approach involved hierarchical processing of reservation requests, assigning different priorities to each request. Another strategy, proposed by

Zhang et al. \(2015\), was the BATCH strategy, which grouped vehicles in each traffic stream into batches. These batches were then served at the intersection following the FCFS strategy. In a similar vein, Huang et al. \(2023\) developed an algorithm that integrated the occupation of intersections by both CAVs and MVs into a space–time resource description framework. This framework generated energy-efficient trajectories for vehicles while minimizing individual delays. Despite the various strategies employed in reservation-based approaches, the rule-based nature of these methods meant that vehicle trajectories were not optimized, and therefore, system optimality was not guaranteed \(Levin and Rey, 2017\). 

The virtual lane method can be seen as a form of reservation implemented at a virtual lane. This approach involves projecting approaching vehicles from various traffic streams onto a virtual lane. For instance, Hu et al. \(2021\) introduced a constraint tree to 3 

*D. Zhou et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104807* 

describe the geometric topology of approaching vehicles. This tree formulated the collision-free passing sequence and incorporated two different driving modes. By forming local virtual platoons, these methods determined whether to create a platoon and how to navigate towards the intersection. However, it is important to note that these approaches still relied on a FCFS policy to a certain extent. While this policy was effective and easy to implement, it may result in a loss of systematic efficiency. Therefore, despite their effectiveness, these approaches may not guarantee optimal system performance. 

*2.2. Mathematical programming*

Another widely used method is mathematical programming algorithms which transfer the whole problem into an analytical formula-based optimization. Regarding cooperation at signalized intersections, the focal point is the behavior at the entrance before the intersection, where the car-following behavior is widely concerned. Chen et al. \(2021\) formulated a high-order nonlinear optimization for “1 \+ n” mixed platoon considering velocity deviation, fuel consumption and terminal speed. Yu and Long \(2022\) proposed a real-time eco-driving strategy by adopting model predictive control. The optimization tied to minimize the total fuel consumption, where Pontryagin’s minimum principle was employed to derive necessary optimality conditions under different scenarios. Khan and

Chowdhury \(2021\) proposed a situation-aware module that enabled CAV to identify the following MV’s intension and adjust its decision. 

Besides car-following, lane-changing-aware cooperations are also developed in some studies. Ma et al. \(2021\) firstly optimized lateral lane-changing strategies, then optimized longitudinal acceleration profiles based on the lane-changing strategies. A Lane-Changing Strategy Tree and a Parallel Monte-Carlo Tree Search algorithm were designed to solve the optimization model. Yao and

Li \(2021\) proposed a decentralized lane-change-aware trajectory optimization model including discretionary lane change restraining and mandatory lane change yielding strategies with the object considering Riding comfort and traffic mobility. The complex non-linear lane-change-aware constraints are linearized and the proposed problem is converted to a quadratic optimization problem. 

Regarding unsignalized intersections, besides car-following, crossing is another concerned behavior. There are two mainstream paths to handle the collision caused by crossing. The first path divides the cooperation into bi-level optimization problem. The high-level decides the optimal passing order \(Pan et al., 2023\) or arrival time \(Yao et al., 2023\) or passing priority \(Jiang et al., 2023a\), while the low-level achieves the optimal control of CAVs. Chen et al. \(2022\) firstly solved target assignment and path planning problems, and then established a graph-based minimum clique cover method to obtain the optimal scheduling plan. Some works solved the high-level decision using search-based method instead of mathematical programming, such as the Monte Carlo Tree Search \(Xu

et al., 2019\). To tackle the a coordination problem for CAVs with an unpredictable behavior of MVs, Faris et al. \(2022\) proposed a timeslot-based strategy, utilizing CAVs as both sensors and actuators in mixed platoons. They incorporated a bi-level optimization structure within a Model Predictive Control \(MPC\) framework to manage vehicle crossing orders and commands. The paper further illustrated that the choice of the MV prediction model profoundly impacts coordination. 

The other path for cooperation at unsignalized intersections seeks to achieve the optimal control by formulating an optimization directly. The bottleneck is the nonconvexity due to the collision avoidance constraints. How to overcome the nonconvexity is the highlight of these methods. Katriniok et al. \(2022\) built on a fully distributed model predictive control. They applied the penalty convex-concave procedure to accommodate a fast solution of the high-order and nonconvex optimization. Xu et al. \(2022\) proposed a general framework that first converted a multi-lane intersection problem into a decentralized optimal control problem with less conservative safety constraints. An Optimal Control and Barrier Function \(OCBF\) controller was designed for solving the problem efficiently. Amouzadi et al. \(2023\) formulated the crossing of intersections as a multi-objective optimal control problem \(OCP\) that minimized the overall crossing time, as well as the energy consumption due to the acceleration of CAVs. The constraints that avoid collision of vehicles with each other and with road boundaries were smoothed by applying the dual problem theory of convex optimization. Hadjigeorgiou and Timotheou \(2023\) achieved coordinated control by generating an acceleration profile for each CAV to simultaneously optimize fuel consumption and travel time. Facing the challenging non-convex problem caused by collision avoidance, the authors first created a relaxed reformulation of the problem by ignoring certain safety constraints, thus eliminating the interde-pendence between trajectories of the CAVs on the same lane. Then, they developed a custom convex-concave procedure that calculates each CAV’s travel time to cross the intersection without lateral collisions. 

The limitation of the mathematical programming method, no matter which path is applied, lies on the analytical description and solution. It is hard to construct the analytical formula of the scenario with complex interactions, such as unsignalized intersection under mixed traffic environments. Even if it is formulated analytically, solving the high-order and nonconvex program is still inefficient. 

*2.3. Reinforcement Learning \(RL\)*

To overcome the limitations of optimization on analytical description and solution, the Reinforcement Learning is widely applied recently. It models the problem by a Markov Decision Process \(MDP\) and find the optimal action-selection strategy that maximizes long-term rewards. 

Regarding the cooperation at signalized intersection, Zhou et al. \(2020b\) trained a car following model by Deep Deterministic Policy Gradient \(DDPG\) to improve travel efficiency, fuel consumption and safety at signalized intersections in real-time. Jiang et al. 

\(2023b\) took into account the interaction between CAV and MVs. A delayed reward Markov Decision Process \(MDP\) is formulated to model the longitudinal motion control process of the platoon. 

Regarding the cooperation at unsignalized intersection, Deep Q-network \(DQN\) is adopted to determine platoon sizes and passing 4 



*D. Zhou et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104807* 

priorities respectively \(Li et al., 2023\). The model comprehensively considers multiple objectives \(i.e., efficiency, fairness and energy saving\) when making decisions. Besides, an unified optimization problem has been formulated to maximize traffic throughput while ensuring driving safety \(Luo et al., 2023\). The optimization problem was solved by the Twin Delayed DDPG \(TD3\). Zhang et al. \(2023\)

introduced an algorithm named AlphaOrder that built a pointer network model \(trained by REINFORCE\) to generate near-optimal passing orders instantaneously for new scenarios. These methods model an agent as a centralized cooperator to make high-level decisions. However, few of them consider both the complex interaction and the mixed traffic scenarios. The uncertain and diverse behaviors of MVs bring issues like numerous and unpredictable interactive relationships, and the social compliance of CAV’s behaviors. 

In conclusion, reservation-based method seeks a feasible solution but usually not the optimal or near-optimal one. Mathematical programming-based method is hard to formulate and solve the cooperation for complex interactions like crossing. The RL-based methods that model a single vehicle as the agent fail to achieve the systemic improvement. Some RL methods treat the agent as a centralized cooperator to make high-level decisions but are restricted to the multiple and uncertain interaction and social compliance of CAVs. The cooperation considering both complex interactions and mixed traffic requires further improvement. 

**3. Problem statement**

This paper focuses on the analysis of isolated unsignalized intersections within a mixed traffic environment. Fig. 2 illustrates a typical intersection configuration consisting of four arms: North, West, South, and East, denoted as *N*, *W*, *S*, and *E * respectively. Each entrance at the intersection is characterized by a single lane, which is shared by vehicles traveling straight and vehicles making left turns from the same entrance. 

We define ***PD ***= \[ *D* 1 *, D* 2 *, *⋯\], where ***PD *** is the platoon from the entrance’s direction *D*, and *D *∈ \{ *N,W,S,E*\}. The subscript *i * denotes the *i*-th vehicle at the platoon. Each platoon consists of two types of vehicles: MVs and CAVs. Each vehicle has two intended direction alternatives: going straight or turning left. The vehicle numbers of the left-turning platoon and the oncoming platoon are random where the vehicle type \(CAV or MV\) is random too. Notably, the platoon in this study does not highlight on the formation of vehicles, but groups vehicles according to the lane they are traveling or coming. This is because the formation of vehicles is just one special form among our potential solutions, special consideration or emphasis on formation is not required. 

There are several assumptions for CAVs and MVs. \(1\) We assume the state \(i.e., position, speed, acceleration and heading of CAVs and MVs\) can be perfectly known to serve for state-sharing. MVs are conventional vehicles that are not equipped with additional devices for perception and state-sharing. Instead, the roadside unit can accomplish the perception of MVs and disseminate these identified states to all CAVs. \(2\) MVs’ behaviors are controlled by human drivers. Their trajectories are not made accessible to the CAVs, nor do they accept any information regarding the trajectories or intention of the CAVs. \(3\) All CAVs are based on the Class D, prescriptive cooperation, according to SAE J3216 standard \(SAE, 2020\). 

The cooperation/communication range is the area formed by the sections located h meters from the stop line of each entrance at the intersection, as shown in Fig. 2. According to the experimental practice, h is set to 55 m. The cooperation process starts the instant a CAV enters the effective communication range and lasts until all CAVs leave this range. Such decision-making is real-time executed to update vehicles’ intention. 

Certain existing studies approach intersection cooperation as a passing order seeking problem. The passing order is a result of vehicle behavior. Focusing only on passing order in cooperating pure CAV traffic at unsignalized intersections is reasonable and efficient. This is because all participants will be governed by the passing order to determine their vehicle’s behaviors. However, in a mixed human–machine driving environment, since human-driven cars have their own behavioral patterns, the passing order on the **Fig. 2. **A typical scenario at an unsignalized intersection with four arms. 

5 

*D. Zhou et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104807* 

behavioral level struggles to reflect features on the intention level, that is, the uncertainty and the social adaptability of intentions. 

On one hand, the social compliance of a passing order must be judged from the perspective of individual vehicle intentions. The passing order merely results from a combination of relevant vehicles’ intentions. For instance, consider the interaction scenario shown in Fig. 2 between MV N1 and CAV E1. There exist two passing orders for N1 and E1: N1 precedes E1 or E1 precedes N1. However, both passing orders may not necessarily be socially compliant. For instance, if N1 is particularly close to the conflict zone, N1 preceding E1

is socially compliant, while E1 preceding N1 is not. Even though E1 proceeding first might result in overall better benefits, E1 should yield as per societal interaction norms. 

On the other hand, the diversity of passing order stems from the uncertainties of intention. Firstly, the intentions of MVs are uncertain, which may lead to radically different passing order. For instance, consider the interaction scenario shown in Fig. 2 between MV N1 and CAV E1. The uncertainty of intention stems from uncontrollable MV behaviors: N1 might choose to be aggressive or yield. 

This uncertainty of intention contributes to the subsequent uncertainty in both vehicles’ passing order. Furthermore, uncertainty in MV’s intention could trigger a chain reaction. The intention of N1 to go first or afterward will significantly impact both vehicles’

behavior patterns and, through interactions, further influence all other vehicles, leading to drastic alterations in the overall passing order. 

As an extension of the passing order, this paper proposed a situation-based perspective, which additionally the features of uncertainties and social compliance on the intention level \(Zhou et al., 2022\). The situation notion is a more informative description because it includes rather the passing order, but also each vehicle’s states and potential intentions. First, the interaction graph was introduced to represent the scenario with the uncertain and diverse interactions. Fig. 3 shows the graph-based description. 

***G ***= \( ***V**, **E***\)

\(1\)

***V ***= ***P***

\(2\)

\{ ***N***∪ ***W***∪ ***S***∪ ***E***\}

***E ***= **R *P ***∪ **R *L***

\(3\)

where the vector ***V *** denotes the vertices that represent all vehicles, and the vector ***E *** denotes edges that represent the relationships among agents pointing from the downstream one to the upstream one. The relationship that A being primitive to B is denoted as *A*→ *B*. 

The relationship involves two types: the physical relationship **R ** *P * and the logical relationship **R ** *L*. The physical relationship represents the following interaction by highlighting the passing order of vehicles of one platoon. Since physical relationships are observable and determined, they are represented by directional lines. The logical relationship represents the conflicting interaction by indicating the passing of vehicles of different platoons. Since the logical relationships are undetermined, they are represented by dashed bidirectional lines. Notably, two vehicles with the same intended direction but from opposite entrances have no interaction with each other. For example, in Fig. 2, no relationship exists between vehicle N1 and S1. 

Given the interaction graph, the decision-making is to determine each vehicles’ intention, that is, transferring the bi-directional **Fig. 3. **The interaction graph to represent the typical scenario. 

6 

*D. Zhou et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104807* 

edges to unidirectional edges. The problem is solved through a Markov Decision Process \(MDP\)-based decision-making process. It develops a stage-wise decision while one target vehicle’s intentions are determined through the policy network at each stage. Finally, all bi-directional edges are eliminated which means all vehicles’ intentions are determined. 

The situation-based perspective highlights the uncertainty inherent in interactional intention. This captures the diversity of potential intention combinations among vehicles. By integrating situation-based reasoning with Markov Decision Processes \(MDPs\), we can select a globally optimized intent combination amidst a multitude of intent possibilities. During solving, the staged decision-making process pinpoints each vehicle’s intention, eliminating the uncertain relationships within the situation’s interactive intent. 

This step aids subsequent decision-making stages and eventually leads to the derivation of an optimal intention combination. 

**4. Methodology**

*4.1. Framework*

This paper tries to formulate a centralized cooperator and makes high-level decisions. However, instead of decision on all CAVs intentions to determine the situation directly, this paper proposes a sequential situation reasoning process. 

The process is formulated as a Markov Decision Process \(MDP\). The MDP includes three critical elements: the state *s, * the action *a*, the policy *π*. The state *s * is defined as the interaction graph ***G ***= \( ***V**, **E***\), where ***V *** is the set of all vehicles’ states, ***E *** represents the relationships among agents which is described by the interaction graph. The action *a * is defined as the entrance where the next passing priority is assigned. So *a *∈ *A*, where *A * is the action set and *A *= \[ *N, W, S, E*\]. The policy *π * is a mapping from the state to the action. 

A typical MDP for situation reasoning is illustrated in Fig. 4. We denote *k * as the step of the decision process. When *k *= 0, the initial state *s* 0 corresponds to the origin interaction graph given the scenario shown in Fig. 2. Then the policy *π * can map the state to an action *a* 0 which, in this case, is *N*. It means that the first vehicle from the north entrance N1 is allowed to pass through the intersection first. 

Moving on to the next step, when *k *= 1, the interaction graph ***G*** 1 is updated. Since the vehicle N1 is preemptive to all the conflicting vehicles, we can establish logical relationships, i. e., N1→W1，N1→S2 and N1→E1. Consequently, these corresponding edges are added to ***G*** 1. Notably, N1 also precedes the physical lag vehicles of W1, S2, and E1, such as W2, S3, E2 and so on . However, for clarity purposes, these additional edges are not presented in Fig. 4. 

After determining the interaction graph for k = 1, and considering the policy denoted by π which generates the action *South*, it signifies that the first car “S1″ from the south enters the intersection at this step. Given that there is no conflict between S1 and N1, these two vehicles can pass through the intersection simultaneously. Consequently, the interaction graph for *k *= 2 is updated to reflect S1 preceding all the other vehicles excluding the preceding vehicle N1. This update involves adding three new logical relationships: *S* 1→ *W* 1, *S* 1→ *N* 2 and *S* 1→ *E* 1 and the edges to the rear vehicles. With the updated interaction graph, the next action can be determined. 

This reasoning process can be iterated forward to continue the sequence of stages. 

The Reasoning Graph-based reinforcement learning framework, as depicted in Fig. 5, is developed based on the aforementioned MDP. In this framework, the agent determines its action by following the policy provided the current state. The environment, in turn, **Fig. 4. **A typical MDP of situation reasoning. 

7 

*D. Zhou et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104807* 

produces the next state based on the current state. Additionally, a reward is generated to update the policy and motivate it to select actions that result in high cumulative rewards over time. The ultimate goal is to improve the overall utility of the intersection. 

In the agent block, the first step involves describing the scenario through an interaction graph that encompasses the motion states of each vehicle and the interaction relationships between them. The current state at stage *k * comprises the interaction graph and the sequential feature. Subsequently, a policy network *πθ * is employed to model the policy *π*, with *θ * denoting the parameters of the network. The structure of *πθ * is composed of graph neural networks \(GNNs\). For more detailed information, please refer to Section 4.2. 

The action *a * and the stage feature ***fs *** can be therefore produced based on the policy network: \( *a, **fs***\) ∼ *πθ*\( *G, PT*\)

\(4\)

In the environment block, the initial step involves identifying the target vehicle to which the action pertains. Then, we generate the trajectory of the vehicles, taking into account their interactions with both logical and physical vehicles. During this process, the social compliance of the interactions and potential collisions will be checked. Once the trajectory is determined, we calculate and output the reward associated with the target vehicle. Please see Section 4.3 for details. 

The framework also incorporates a sequential feature embedding block, consisting of a stage embedding part and a temporal embedding part. Initially, we gather the stage features ***fs *** starting from the initial stage 0 up to the current stage *k*. These stage features are then embedded into a temporal feature, which captures the characteristics of all stages at the current time *T*. Subsequently, these temporal vectors are further embedded into the sequential vector ***fT***. The sequential vector serves as a component of the states, extracting features from both past stages and the situations of previous time steps. Both the stage embedding and the temporal embedding blocks are implemented using a Transformer Encoder block. 

Overall, at every update interval, the central cooperator first receives the vehicle state information. It then executes the RGRL, which generates the vehicle intentions and trajectories. After that, the central coordinator publishes the computed trajectories to the corresponding CAVs. Finally, each CAV executes vehicle control according to the received trajectory. 

*4.2. The policy network*

The policy *π*\( *a*| *s*\) denotes the probability density of selecting action *a * given the state *s*. In this section, our objective is to utilize neural network architectures to model this probability density and establish a mapping from the current state \(represented as an interaction graph\) to the probability density of actions. An essential challenge lies in extracting features from unstructured graph data, taking into account the motion state features of each vehicle and the interaction relationship features between vehicles, to derive comprehensive system-level features. We design the policy network whose overall architecture is shown in Fig. 6. 

This paper uses Graph Neural Networks \(GNN\) to address this challenge. GNN is a method that effectively transforms all aspects of a graph, including nodes, edges, and global properties while preserving the symmetry of the graph, such as permutation invariance. To construct the GNN, we will use the “message passing neural network” framework proposed by Gilmer et al. \(2017\) and the graph **Fig. 5. **Reasoning Graph-based reinforcement learning framework. 

8 

*D. Zhou et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104807* 

**Fig. 6. **The overall architecture and hyperparameters of the policy network. 

network architecture principles introduced by Battaglia et al. \(2018\). GNN follows a “graph input, graph output” architecture, which means that these model types accept a graph as input, load information into its nodes, edges, and global context, and progressively transform this information without altering the connectivity of the input graph. 

Compared with the widely used self-attention/cross-attention mechanism, the GNN-based policy network is more effective in capturing the systemic features by appropriately formulating the interactions within the system. GNN incorporates interconnected object connections that define the mutual influence between objects based on domain knowledge. On the other hand, self-attention/

cross-attention involve complete mutual connections between objects, regardless of whether the interactions exist or not. Although the extent of influence can be adaptively learned, these approaches may lead to redundant feature updates. 

*4.2.1. The input layer*

The input includes a graph ***G*** ʹ = \( ***V*** ʹ *, **E*** ʹ\) and a sequential vector. The graph ***G*** ʹ is transformed from the nodes ***V *** and interaction relationships ***E *** of the interaction graph ***G***. ***V*** ʹ is a set composed of the feature vectors of each node in the graph. ***V*** ʹ and ***V *** have the similar definition, that is:

***V*** ʹ = \[ *d, v, a, Ent, Int, vehType*\]

\(5\)

Where *d * is the distance from the stop line of the entrance lane to the intersection. *v, a * are the speed and acceleration respectively. *Ent* denotes the direction of the entrance \(i.e., N, E, S and W\), which is one-hot encoded. *Int * denotes the direction of the entrance \(i.e., turning left or going straight\), which is also onehot encoded. *vehType * marks whether the vehicle is CAV \(equal to 1\) or MV \(equal to 0\). 

To enhance the adaptability of the action strategy network across different intersections, the absolute position coordinates are converted into relative position coordinates denoted as *d*. Furthermore, when considering the parameters in the transformed state *V* ʹ, only the position and longitudinal motion parameters of the vehicles are included, while the direction angle is excluded. This choice is based on the assumption that vehicles move along the centerline of the lane leading up to the entrance lane in the environment. As a result, the direction angle can be directly calculated from the vehicle’s position, rendering its explicit inclusion unnecessary. 

The edges ***E*** ʹ signify the directional influence between nodes, which are analogous to the edges ***E *** in the interaction graph. For example, in cases where the relationship is bi-directional, ***E*** ʹ is represented by two opposite edges connecting the two vehicles. This accounts for the possibility of mutual influence between the vehicles. 

\(

\)

The relationships between edges in GNN are represented by the adjacency matrix ***A ***= *eij n*× *n*. If *eij *= 1, there is an edge pointing from node *vi * to node *vj*, which means that the motion state of node *vi * can significantly affect the state of node *vj*. The value of *eij * can be obtained through the edges in the interaction graph, and its relationship with the interaction relationship in the interaction graph is as follows:

\{

*e*

0 *, if vi*← *vj*

*ij *=

1

\(6\)

*, if vi*→ *vj or vi *↔ *vj*

If node *vi * is primitive to *vj*, then *eij *= 1. If node *vi * yields to *vj*, then *eij *= 1. If the leading-following relationship between nodes *vi * and *vj * is uncertain \(i.e., the bidirectional edge\), then *eij *= *eji *= 1. 

The sequential vector is generated by extracting the historical features, which consists of two steps, as shown in Fig. 7. Firstly, the 9 

*D. Zhou et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104807* 

embedding is performed on the inferred sequence of interaction graphs at each time step T = t, resulting in the global feature *fstK * at *e*

time t. The global features *fsT*− *w*: *T*

*K*

from each historical time step within the range \[T-w, T\] are collected and embedded again to obtain *e*

the system’s historical features, which are then inputted into the policy network. This input facilitates better coupling of the historical information of each vehicle. More importantly, it enables capturing the global features of the system, thereby encouraging the policy network to generate higher-quality decisions at the system level. 

By integrating multi-step historical state information into a single state, we create an “expanded” or “enhanced” state. In this case, the new state eliminates the direct dependence on these previous states. In other words, the future state transitions of the system depend only on this enhanced current state, not on its past states. This meets the conditions of the Markov property. 

*4.2.2. The graph Convolution network \(GCN\) layer*

Graph convolutional networks can aggregate node features along the direction of information propagation within the input graph. 

The relationship between node features in the next layer and those in the current layer can be determined by:

∑

*x* ʹ

*ej,i*

*i *= ***WT***

̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅

√

̅ *xj*

\(7\)

*j*∈**N **\( *i*\)∪ *i*

*degidegj*

∑

*degi *= 1 \+

*ej,i*

\(8\)

*j*∈**N **\( *i*\)

where *xi * represents the feature of the node *i * in the current layer. *x* ʹ *i * represents the feature of the node in the next layer. *xj * represents the feature of the adjacent node *j * to the node *i*. ***W *** is a trainable parameter matrix that enables integration and dimensionality changes of node features. *ej,i * is the value in the j-th row and i-th column of the adjacency matrix, and *degi * is the degree of node *i * in the graph. 

Taking the interaction graph at the stage *k *= 2 in Fig. 4 as an example, N1 is the first vehicle to pass through the intersection. Its movement will affect the interactive vehicles like W1, S2, and E1 and so on. When updating the node features of W1, S2, and E1

through the GCN layer, their features are aggregated with those of N1. Furthermore, when updating the features of W2, the following vehicle of W1, both the feature of its physical front vehicle W1, and the conflicting vehicles like N1, S1, etc. should be considered. This information propagation mechanism effectively captures the complex dynamics of interactive systems with chain reactions, making it suitable for feature extraction in the scenario with chain reactions. 

By stacking several layers of GCN, the features of each node can inherit the features of its neighboring nodes. The receptive field of each node will continue to expand with the increase of GCN layers. However, due to the rapid diffusion of the GCN receptive field and **Fig. 7. **The input of the policy network. 

10 

*D. Zhou et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104807* 

the fact that features from distant nodes are often diluted when transmitted to the current node, too many GCN layers are usually not stacked. In this section, we only take the two-layer GCN structure. 

*4.2.3. The graph attention \(GAT\) network*

While the GCNs facilitate the propagation of features between adjacent nodes, the coefficients of feature propagation are influenced

̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅

√

̅

solely by the connectivity of the nodes, specifically by the value of 1 */ degidegj*. As a result, the influence between nodes is determined solely based on the degrees of the two nodes, without considering their individual states. 

Taking the scenario in stage *k *= 2 in Fig. 4 as an example, N1 serves as the first vehicle and has an impact on S2, which is heading straight from the south. S1 serves as the second vehicle, and also has an impact on S2 as it is preemptive to S2. Since N1 and S1 have the same degree, S2 will be equally influenced by N1 and S1 in GCN layers. However, in reality, the influence of the two vehicles on S2 may not be equal and could be closely related to the states of all three vehicles. For example, if S2 is very close to its physical front vehicle S1, and far away from N1, then S2 will obviously be more influenced by S1. 

To address the heterogeneous impact of different node states on the current node, the Graph Attention layer is introduced. The purpose of this layer is to calculate heterogeneous coefficients for each node, enabling the distinction of their respective influences on the current node while considering their diverse states. The update method for the features of the current node is as follows. 

∑

*x* ʹ *i *= ***WT***

*αi,jxj*

\(9\)

*j*∈**N **\( *i*\)∪ *i*

The core of this method is to assign different weight coefficients α *i,j * to the current node and each neighboring node, and the method for solving these weight coefficients is as follows:

\(

\(

\)

\)

*e* ʹ *i*

*concat **Kx***

• ***Q***

\(10\)

*,j *= *LeakyReLU*

***i**, **Kxj***

*e*

*α*

*i,j* ʹ

*i*

\(

\)

\(11\)

*,j *= ∑

*j*

*e* ʹ

∈**N **\( *i*\)∪ *iexp*

*i,j*

The weight coefficient α *i,j * is defined as the importance of node *j * feature ***xj *** to the feature ***xi *** of the current node *i*. Firstly, the trainable parameter matrix *K * is left-multiplied to both ***xi *** and ***xj***, in order to map the two feature vectors to higher dimensional space. Then, the two high-dimensional vectors are concatenated into one vector and multiplied by a trainable parameter vector *Q * with the same dimension, resulting in a value. This value is then passed through a *LeakyReLU * activation function to obtain the final importance value. 

Finally, a *softmax * function is applied in Eq. \(10\) to the importance values of all neighboring nodes, including the current node itself, to normalize the values into weights that sum up to one. 

*4.2.4. The output layer*

After propagating the features of each node through the GCN and GAT layers, it is necessary to obtain global features that encompass all node features. We use the global average pooling to achieve this goal, which calculates the average value of all node features in the graph. Specifically, we integrate the features *xi * of multiple nodes into a single feature vector xG by taking the mean of all node features in the graph:

*xG *= *mean*\( *xi*\) *, xi *∈ ***V*** ʹ

\(12\)

Finally, the global features are transformed into a *n*-dimensional vector through fully connected \(FC\) layers. If a linear activation function is applied and *n * is equal to 4, the Q-values of the four actions are outputted. If a linear activation function is applied and *n * is equal to 64, the stage feature is obtained. If the *softmax * activation function is applied, the probabilities of the four actions are obtained. 

Then the action with the highest probability is selected and outputted. 

*4.3. Environment*

The environment defines the rules and dynamics of the system in which the agent operates. It generates the next state *st*\+1 given the action *at * and provides a corresponding reward of the action to the agent for updating the policy network. 

After determining the subjective vehicle at stage t, obtaining the next state *st*\+1, is straightforward. The logical relationships associated to the subjective vehicle in the interaction graph *Gt*\+1 should take precedence over those that have not yet been assigned the right of way. 

Besides, the trajectory of the subjective vehicle should be generated. Then the reward function is defined in terms of the safety, efficiency, energy-saving and social compliance performance of the subjective vehicle:

\{

*reward*

− 1 *, if error action or collision or not socially compliant*

=

1 − \[ *ω***z**\( *Ttrav*\) \+ \(1 − *ω*\)**z**\( *F*\) \] *, otherwise* \(13\)

The error action refers to a situation where the generated action does not correspond to any vehicle at the target entrance. In addition, it is necessary to check whether the trajectory adheres to collision-free and social compliance criteria. If either condition is not met, a strong negative reward of − 1 is assigned. Alternatively, if the trajectory satisfies the collision-free and social compliance 11 

*D. Zhou et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104807* 

requirements, the reward is calculated as a tradeoff between efficiency and energy-saving. This is done by summing up two surrogate indices: travel time \( *Ttrav*\) and the time integral of fuel consumption \( *F*\). VT-micro fuel consumption model is employed for fuel consumption formulation \(Zegeye et al., 2013\). To balance the optimization bias, a weight ω is introduced, set to 0.5 in this paper to evenly consider efficiency and energy-saving. The function **z**\( • \) represents a min–max normalization. 

*4.3.1. Speed profile generator*

This paper generates the speed profile of CAVs *s*\( *t*\) by quintic spline. The quintic spline is defined as a series of piecewise quintic polynomials *Qi*\( *t*\):

*s*\( *t*\) = *Qi*\( *t*\) *, ti*− 1 *< t < ti, i *= 1 *, * 2 *, *⋯ *, n* \(14\)

*Qi*\( *t*\) = *ai, * 0 \+ *ai, * 1 *t *\+ *ai, * 2 *t* 2 \+ *ai, * 3 *t* 3 \+ *ai, * 4 *t* 4 \+ *ai, * 5 *t* 5

\(15\)

\[

\]

We denote ***A ***= *ai*

as the coefficients of the quintic spline. It can be solved by the following optimization \(Takahashi

*,k i*=1: *n,k*=0:5

et al., 1989\):

∫ *te*

*A *= argmin

*s* ʹʹ\( *t*\) *dt*

\(16.a\)

0

*s.t. Qi*− 1\( *ti*\) = *Qi*\( *ti*\) *, i *= 2 *, * 3 *, *⋯ *, n* \(16.b\)

*Q* ʹ *i*− 1\( *ti*\) = *Q* ʹ *i*\( *ti*\) *, i *= 2 *, * 3 *, *⋯ *, n* \(16.c\)

*Q* ʹ *i*− 1\( *ti*\) = *Q* ʹ *i*\( *ti*\) *, i *= 2 *, * 3 *, *⋯ *, n* \(16.d\)

*Q* 0\( *t* 0\) = *s* 0

\(16.e\)

*Qn*\( *te*\) = *se*

\(16.f\)

*Q* ʹ0\( *t* 0\) = *v* 0

\(16.g\)

*tc *≥ *tc,LFV *\+ *tsafe*

\(16.i\)

*tc < tc,LLV*

\(16.j\)

*s*\( *t*\) ≤ *sPFV*\( *t*\) − *ssafety*

\(16.k\)

where *s* 0 and *v* 0 denote the initial longitude position and speed, *se * is the longitude position of the destination, *te * is the arrival time to the destination. *tc,LFV * is the maximum excepted arrival time of logical front vehicles. *tc,LLV * is the minimum excepted arrival time of logical lag vehicles. *sPFV * is the space profile of the physical front vehicle. *tsafe * and *ssafety * is time and distance interval for safety. Eqs. \(16.b\)-\(16. 

d\) constrain the equal position, speed and acceleration at the intersect points \(i.e., konts\) between each two adjacent polynomials. Eqs. 

\(16.e\)-\(16.h\) impose constraints on the position, speed at the start and end point. Eqs. \(16.i\)-\(16.j\) constrain the arrival time at the conflict point. 

Car-following modeling is widely employed to model the speed profile of MVs in the mixed traffic system, such as Wiedemann model \(Wang et al., 2020\), Gipps model \(Rios-Torres and Malikopoulos, 2018\), Intelligent Decision Model \(IDM\) model \(Jiang et al., 

2017\). Among various car-following models, IDM performs overall best in depicting the car-following behavior of MVs, as well as in various driving styles and traffic flow \(Zhang et al., 2021\). So, this paper utilizes the IDM to represent the behavior of MVs and generate the speed profile of them. So he rate of speed change *af*\( *t*\) is determined by the equation as follows:

\[

\( \)

\(

\) \]

*δ*

2

*a*

*v*

*s*\*\( *v, * Δ *v*\)

*f *\( *s, v, * Δ *v*\) = *a* max 1 −

*v*

−

\(17\)

d

*s*

*s*\*

*v* Δ *v*

\( *v, * Δ *v*\) = *s* 0 \+ *vTg *\+ 2 ̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅

*a*

√

\(18\)

max *a* dd

where *af*\( *s, v, * Δ *v*\) is acceleration, *v * is speed. *v* d is the desired speed. Δ *v * is the speed difference between the physical front vehicle and the subject vehicle. *s * is the distance to the physical front vehicle. *s* 0 is the minimum stopping distance. *Tg * is the desired time gap to the physical front vehicle. *a* max is the maximum acceleration. *a* dd is the desired deceleration. 

Furthermore, in order to develop a policy that can handle uncertainties, it is necessary to incorporate the uncertainties associated with the behavior of the MVs into the Environment block. Therefore, throughout the training and testing process, MVs’ behavior was driven by a continuous stochastic car-following model proposed by Ngoduy et al. \(2019\). We added a stochastic deviation in the car-following model in case we can precisely predict MVs’ movements:

12 

*D. Zhou et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104807* 

̅̅

√ ̅

*a*

*dW*\( *t*\)

*sim *= *af *\( *s, v, * Δ *v*\) \+ *σ* 0 *v*

*dt*

\(19\)

where *W*\( *t*\) follows a Wiener process modelling the random deviations from the mean speed, *σ* 0 is a positive speed dependent dissipation parameter describing the noise strength whose value is 0.88 in this paper. 

*4.3.2. Social compliance and collision checkers*

This section introduces two checkers which contributes to the social compliance and the safety of the reasoned situations. The checkers have been incorporated into the reward function Eq. \(13\). 

*4.3.2.1. Social compliance checker. * The social interaction checker is to judge whether a logical relationship is socially compliant. It models MVs’ reactions to other MVs’ behavior, which helps determine MV-MV logical relationships. It also contributes to judging the social compliance of CAV-MV logical relationships: whether the interacting MV would accept the reasoned CAV-MV logical relationship. 

The social compliance checker is based on the social interaction custom in our previous work \(Zhou et al., 2022\). We firstly defined the cooperative acceleration *ac * as the maximum acceleration of the interacting vehicle to avoid collision with the subjective vehicle The cooperative acceleration *ac * can be calculated by the following equation:

*a*

2\( *d *− *vsTl*\)

*c *=

*T * 2

\(20\)

*l*

where *Tl * is the arrival time of the ego vehicle at the conflict point, *d * is the distance between the interacting vehicle and the conflict point, *vs * is the speed of the interacting vehicle. Cooperative acceleration is an anticipated measurement to indicate the comfort loss of vehicle *S*. The cooperative acceleration reflects the comfort loss of the interacting vehicle, which indicates the intention tendency of the interacting vehicle given the arrival time of the ego vehicle. There exists a threshold *H * that can help distinguish the intention of the interacting vehicle. 

Based on the cooperative acceleration-based rules for intention recognition, vehicles can recognize how the interacting agents would react to their behavior. Another concern is that the CAV should move in a way that enables the MV to move complying with the assumed logical relationship. Two propositions for socially compliant driving were therefore proposed by mapping the cooperative acceleration-based criteria to the time range of motion planning. 

**Proposition 1**. \( *\(socially compliant preempting\)*\)

If there is a feasible AV’s motion plan based on which AVs arrive at the conflict

point within the cooperation time range *Tp*, the cooperating agent is willing to yield to the AV, and the AV can preempt the conflict point. 

**Proposition 2**. \( *\(socially compliant yielding\)*\)

If there exists no feasible AV’s motion plan to ensure the AV to arrive at the conflict point within the cooperation time range *Tp*, the cooperating agent would preempt and the AV should yield to the cooperating agent. 

The cooperating time range *Tp * in the propositions refers to the time the cooperating vehicle takes to arrive at the conflict point given the acceleration value of the threshold *H*. *Tp * can be solved by the following equation: *v*

1

2

*sTp *\+ 2 *HTp *= *d*

\(21\)

Propositions 1 and 2 reflect that the intentions of cooperating agents are influenced by the states of themselves and AVs’ planning simultaneously. The CAV-MV logical interactions can be implemented based on Propositions 1 and 2 by planning the CAV’s trajectory. 

In other words, a CAV can adjust its speed profile to indirectly influence the interacting vehicle and elicit the expected reaction on a reasonable scale. CAV can accordingly choose to preempt or yield to the interacting agent following the given situation on a reasonable scale. However, in some cases the logical relationships are so impracticable that no matter how CAV adjusts, it still cannot elicit the expected logical relationship. These logical relationship as inapplicable ones. Once we find an inapplicable logical relationship, the situations it belongs to should be crossed out. 

*4.3.2.2. Collision checker. * A collision checker is developed here to check whether the reasoned situation would lead to collision: *TTC *≥ *TTCmin, *∀ *k *∈ *K*

\(22\)

where *TTC * is the time to collision to the left-turning vehicle and *TTCmin * is the minimal value for security insurance. If the motion plan fails to pass the checker, the plan is deemed irrational. The cooperator should adapt the *te * in Eq. \(16.a\) and Eq. \(16.f\) and replan speed profiles. 

*4.4. Reinforcement Learning methods*

The choice of the optimal RL method can vary depending on the specific problem at hand. Therefore, conducting tests is necessary to select the most suitable one. Three methods are candidates: **Double Dueling DQN \(D3QN\) **\(Xie et al., 2017\), **Proximal Policy** **Optimization \(PPO\) **\(Schulman et al., 2017\) and **Soft Actor-Critic \(SAC\) **\(Christodoulou, 2019; Haarnoja et al., 2018; Haarnoja et al., 

13 

*D. Zhou et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104807* 

2019\). 

**D3QN **is an extension of the Deep Q-Network \(DQN\) algorithm that combines the concepts of both double Q-learning \(Van Hasselt

et al., 2016\) and dueling networks \(Wang et al., 2016\). Double Q-learning uses two separate Q-networks: one for selecting actions \(the

“online network”\) and another for evaluating the selected actions \(the “target network”\) to mitigate the overestimation bias and leads to more accurate Q-value estimates. The dueling network architecture separates the estimation of the state value function \(V-function\) and the advantage function \(A-function\), which allows for more efficient learning and better generalization across actions. 

**PPO **updates policies iteratively based on experience. It employs a surrogate objective function, ensuring policy updates stay within a trust region. PPO maximizes performance improvements by balancing old and new policy probabilities weighted by advantages. It has gained popularity due to its simplicity, stability, and effectiveness in various domains. PPO’s key components include trust region optimization, proximal policy updates, multiple epochs, and clipped surrogate objectives. Considering specific problem characteristics, PPO enhances training effectiveness and performance. 

**SAC **is a cutting-edge reinforcement learning algorithm for continuous control tasks. It combines the benefits of policy gradient methods and Q-learning. SAC utilizes a stochastic policy to encourage exploration and maximize entropy. It learns both a policy and a Q-function to estimate action-values. The value function regularization stabilizes training, while soft policy updates ensure smooth learning. SAC excels in handling high-dimensional state and action spaces, achieves good sample efficiency, and strikes a balance between exploration and exploitation. Since the SAC is originally used for continuous-action issues, we adopt the discrete-action version, i.e., SAC for discrete \(Christodoulou, 2019\). 

**5. Case study**

*5.1. Setup*

*5.1.1. Basic parameter settings*

The study site was a typical unsignalized intersection measuring 30 m × 30 m. The entrance and exit lanes had a length of 55 m. The entrance and exit lanes of the four branches within the intersection were included in the study area. The study area encompassed the intersection itself as well as the entrance and exit lanes of the four branches. To examine the intersection’s performance in handling high-density traffic scenarios with frequent interactions, the traffic volume for the entrances was randomly set between 600 and 1200

vehicles per hour. To evaluate the effectiveness of Cooperative Autonomous Vehicles \(CAVs\) in this context, five different CAV market penetration rates \(MPRs\) were tested: 0 %, 25 %, 50 %, 75 %, and 100 %. The vehicle type \(CAV or manually driven vehicle\) for each vehicle was assigned randomly. 

The values of parameters in the proposed method are enumerated in Table 1. These parameters were finely tuned employing a genetic algorithm and are based on empirical trajectory data gathered from the Xianxia-Jianhe intersection in Shanghai, China \(Zhou

et al., 2020a\). Besides, the hyperparameters of the policy network are marked in Fig. 6. 

Notably, the selection of the reward discount rate is tailored to the specific problem. In our case, each decision step corresponds to determining a priority to a vehicle. Therefore, the number of decision steps aligns with the quantity of vehicles engaged in the cooperation. Given that we have set the cooperation range to a 55-meter area in front of the intersection’s stop line, the maximum number of participating vehicles that can be accommodated in the largest cooperative region is 20. Consequently, the decision sequence spans up to 20 steps at most. Given the limited number of decision-making steps required, ensuring convergence during training becomes manageable. This condition allows us to leverage the most substantial reward discount factor that closely approaches 1. Ultimately, we decided upon a factor of 0.99. 

*5.1.2. Methods for comparison*

We choose two methods for comparative benchmarks. These methods will be tested using the same scenarios. 

\(1\) comparative method 1: the Multi-Agent Reinforcement Learning \(MARL\)

MARL has gained popularity in CAV cooperation and intersection management research \(Antonio and Maria-Dolores, 2022; 

**Table 1**

The values of critical parameters. 

Parameter

Meaning

Value

Eq. Num. 

***tsafe***

Desired time gap to the logical front vehicle

1 *. * 5s

\(16.i\)

***ssafety***

Minimum safe distance to the leading vehicle when following it

5 m

\(16.k\)

***a*****max**

Maximum acceleration

5 m */* s2

\(17\)

***v*****d**

Desired speed

10 m */* s

\(17\)

*δ*

Coefficient in the IDM model

4

\(17\)

***s*** 0

Minimum stopping distance

2 m

\(18\)

***add***

Desired deceleration value

3 m */* s2

\(18\)

***σ*** 0

a positive speed dependent dissipation

0.88

\(19\)

***H***

The threshold of cooperative acceleration *ac*

− 0 *. * 15 m */* s2

\(21\)

***γ***

Reward discount rate

0.99

—

14 

*D. Zhou et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104807* 

Gunarathna et al., 2022; Guo et al., 2023\). Specifically, we employed the MA-TD3 method proposed in \(Antonio and Maria-Dolores, 

2022\) for comparison. In this approach, each CAV within the intersection is treated as an independent agent: each agent has its own policy network and, all policy networks are updated simultaneously. The state of each agent is described by the relative position, speed, heading, intended direction, and entrance direction of the ego vehicle and other vehicles. The action taken by each agent is the speed. The reward function used in this research is designed to consider both collision avoidance and efficiency. It returns a strong negative reward if there was a collision, a strong positive reward if the agent successfully crossed the intersection, and − *timestep * to encourage crossing as fast as possible. 

Notably, the original MARL method utilizes Long-Short Term Memory \(LSTM\) cells for interaction /conflict encoder. In this paper, for better comparison, we proposed a version that replaced the LSTM cells with the GNN layers, that is, two GCN layers and one GAT

layer, for interaction encoding. The states also translated into graph-based states where each node embodied various aspects such as relative position, speed, heading, intended direction, and entrance direction. 

\(2\) comparative method 2: the method based on the optimization \(Optim\)

Optim-based methods are recently widely used methods for cooperating CAVs at intersections. We chose the method developed by

Yu et al. \(2019\), which formulated a mixed integer linear programming \(MILP\) model for the optimal service sequence of CAVs. To apply the method in solving our studied problem, we applied this method to generate the desired passing order and vehicles arrival time at the conflict point. Vehicles’ speed profiles were planned based on the speed profile generator proposed in this paper. 

*5.2. Training curves of different RL methods*

Firstly, we employed three reinforcement learning methods, namely D3QN, PPO, and SAC, to seek for the optimal training method. 

The average returns achieved by these methods are presented in Fig. 8. Both PPO and SAC exhibited slightly faster convergence compared to D3QN, but D3QN ultimately achieved a higher converged return while maintaining a reasonable convergence speed. 

Specifically, the converged return of D3QN reached a value of 3, which is 1.5 times larger than the converged returns of PPO and SAC. 

The relatively underperforming results of PPO and SAC may be attributed to the discrete action space utilized in the study. PPO

relies on optimizing continuous mathematical functions through gradient computations, which may not be as effective when applied to discrete action spaces. On the other hand, SAC incorporates an entropy regularization term to encourage exploration. In continuous action spaces, this regularization promotes exploration by introducing stochasticity to the action selection process. However, in discrete action spaces, the entropy regularization may not have the same impact since actions are already discrete and deterministic. 

Consequently, this discrepancy in the effect of entropy regularization in discrete action environments can potentially lead to subop-timal exploration and impede learning. 

Besides, we introduce four additional benchmarks for comparative experiments: \(1\) D3QN with three GAT layers, denoted as D3QN

**Fig. 8. **Training curves on continuous control benchmarks. 

15 

*D. Zhou et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104807* 

\(GAT\), \(2\) D3QN with three GCN layers, denoted as D3QN\(GCN\), \(3\) D3QN with two GCN layer and one GAT layer, denoted as D3QN

\(GCN\+GAT\), and \(4\) D3QN with three layers MLP, denoted as D3QN\(MLP\). The former three benchmarks use the graph-based input as we introduced in this paper. The D3QN\(MLP\) stacks vehicles’ state vectors and utilizes the stacked vector as the input. The evolution of training rewards over time is shown in Fig. 8. Firstly, all the graph-based policies achieve a reward that is fourfold of the reward gained by the MLP-based policy, although they use the same D3QN to train the network. Secondly, upon comparing the benchmarks that exclusively use either GAT or GCN, the policy network structure incorporates both GCN and GAT achieves the highest reward upon convergence. Without GCN, the policy network cannot capture the chain reaction evident in this multiple interaction scenario. Without GAT, the policy network fails to efficiently weight each vehicle’s attentions to its interacting vehicles. Hence, a combination of GCN

and GAT proves to be essential to more effectively capture interaction features, and consequently improve the system performance. 

Furthermore, we also compared the two version of MARL: the MARL with LSTM, denoted as MARL\(LSTM\), and the MARL with GNN, denoted as MARL\(GNN\). As shown in Fig. 9, The MARL\(GNN\) method turned out to yield a higher reward upon convergence. 

This stems from the fact that while MARL\(LSTM\) employs LSTM cells to transmit vehicular interaction information, this information tends to degrade as the number of vehicles increases. This leads to a situation where vehicles inputted later in the sequence struggle to consider the interaction of the vehicles inputted earlier. Besides, the LSTM did not distinguish between conflicting interactions and following interactions, which also leads to inefficient extraction of scenario interaction features. On the other hand, MARL\(GNN\) employs an interaction graph to directly depict vehicular interactions. It simultaneously considers the one-way transfer of features when intentions are definite and bidirectional transfer when intentions are not certain. 

In a word, these two additional sets of experiments shows that GCN and GAT can bring reward increasing for both RGRL and MARL. 

As a result of the superior performance and higher converged return achieved by the D3QN method, we decided to utilize the policy with both GCN and GAT trained by D3QN as the final version. Because of the outperformance of the MARL with GNN, we choose this method as a benchmark of the following typical case and the statistical analysis. 

*5.3. Typical case*

To compare the effectiveness of the RGRL, MARL and Optim methods, we conducted an analysis using a typical case. The system’s origin point was set at the center of the intersection. On each of the approaches, there are two cars present, which are straight-going and left-turning respectively, and are CAV and MV respectively. Detailed information regarding these vehicles is provided in Table 2. 

Fig. 10 illustrates the trajectories of the vehicles in the two systems. In the RGRL-based system, as depicted in Fig. 10 \(a\), *MV-20 * was able to pass through the conflict area first because *CAV-0 * yielded, demonstrating social compliance. Subsequently, *CAV-0 * and its follower, *MV-1*, proceeded through the intersection. An interesting observation was that *CAV-21 * managed to precede *MV-11*. 

Consequently, the two conflict-free vehicles, *MV-11 * and *MV-30*, were able to pass through the intersection simultaneously. 

In the MARL-based system, the situation was not predetermined. Instead, each vehicle independently determined its own action. 

The passing sequence roughly followed the First-Come-First-Served \(FCFS\) strategy, where the leading vehicles from the four **Fig. 9. **Training curves on two versions of MARL. 

16 

*D. Zhou et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104807* 

**Table 2**

Vehicle attributes and initial states. 

ID

Entr. 

Turns

Veh type

position

speed

0

North

Straight

CAV

\(− 2.5,15\)

8

1

North

Left

MV

\(− 2.5,30\)

5

10

West

Straight

CAV

\(− 18,− 2.5\)

10

11

West

Left

MV

\(–32,− 2.5\)

5

20

South

Left

MV

\(2.5,− 15\)

10

21

South

Straight

CAV

\(2.5,− 30\)

5

30

East

Left

MV

\(18,2.5\)

10

31

East

Straight

CAV

\(32,2.5\)

5

entrances proceeded first, followed by their respective followers, as Fig. 10\(c\) shows. However, the specific passing order of the first four vehicles and the latter four vehicles seemed hard to fathom. 

In the Optim-based system, with a goal to minimize the total travel time, *CAV-0 * rushed to the intersection. As a result, *MV-1 * and *MV-20*, both being non-conflicting, were enabled to traverse the intersection simultaneously. This action enhanced the intersection utilization to its maximum, thereby increasing the overall efficiency. However, the hasty intention of *CAV-0 * to seize priority over *MV-20 * was not socially compliant. That meant that *MV-20 * might not readily concede to *CAV-0*, although such a yielding action from *MV-20*

would contribute positively towards systemic utility. 

The performance comparison of the three systems is presented in Table 3. In this case, RGRL generated the best solution regarding the systemic utilities. The RGRL and fuel generated PETs larger than 1.5 s, while MARL caused a sever conflict resulting in PET less than 1.5 s. Regarding efficiency, RGRL outperformed by producing the lowest average and max travel times. Regarding fuel consumption, RGRL also proved more economical as it resulted in both the lowest average and max fuel consumption. The reason for this is that more harsh acceleration and deceleration were experienced with the use of the MARL and the Optim. CAVs in MARL tried to maximum their own benefits, ignoring the impact on the MVs. 

*5.4. Statistical analysis of performances*

We conducted comparative tests to statistically compare the individual performance of vehicles in the RGRL, MARL and Optim systems. 50 scenarios with varied vehicle types, intentions and initial states, were randomly generated and provided to these three systems respectively. Then we did some statistical analyses based on the trajectories of participants collected in these tests. The indices, Post-Encroachment Time \(PET\), travel time and fuel emissions, were determined to reflect AVs’ performances of safety, efficiency and energy-saving respectively. PET can reflect the safety performance when interacting with other vehicles. Travel time can reflect the efficiency of mobility. Jerk is a fundamental index that indicates the comfort. The statistical parameters of the indexes, means, standard deviations \(SDs\) and the difference are presented in Table 4. 

\(1\) Post-Encroachment Time \(PET\)

Post-Encroachment Time \(PET\) is a measure that quantifies the severity of conflicts during crossing events. It represents the time difference between the moment a vehicle leaves the potential collision point and when the other vehicle arrives at the collision point. 

As shown in Fig. 11, all these three cooperation methods were effective in reducing PETs within the system. By utilizing cooperative behaviors, vehicles were not required to maintain overly conservative gaps for crossing, resulting in decreased PET values. Moreover, the PETs were found to be sensitive to the Market Penetration Rate \(MPR\) of Cooperative Autonomous Vehicles \(CAVs\). As the MPR

increased, the PETs decreased, indicating that a higher presence of CAVs led to shorter time intervals between potential conflicts. 

However, the key difference between the two methods was the frequency of severe conflicts, characterized by PET values less than 1.5 s. The RGRL-based system caused fewer severe conflicts compared to the MARL-based and Optim-based system at all CAV

penetration rates. The reason behind this discrepancy lied in the purpose each method orientated. The RGRL-based system considered the systemic utility of the searched situations, taking into account potential collisions between vehicles. On the other hand, in the MARL-based system, each individual vehicle sought to maximize its own utility rather than the global utility. In the Optim-based system, although the collision-avoidance constraint ensures that the PET remains greater than 1 s, the focus on an efficiency-oriented objective tends to minimize the PET as much as possible. As a result, both the RGRL-based and the Optim-based system had strong performance in ensuring safety. However, the vehicles in the MARL-based system tended to exhibit more aggressive behavior, leading to conflicts with other vehicles and an increased frequency of severe conflicts. 

\(2\) Travel time

Travel time serves as a fundamental indicator to assess efficiency, reflecting both the overall delay and the vehicle’s mobility at the intersection. We utilize travel time as a measure of efficiency, as it provides insights into both the time spent by vehicles at the intersection and their ability to move smoothly through it. 

Fig. 12 displays the distributions of travel time for the RGRL-based and MARL-based systems. At all penetration rates, the travel time of the RGRL-based system showed no significant difference compared to the MARL-based and the Optim-based system. Table 4

17 



*D. Zhou et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104807* 

**Fig. 10. **Longitude position and speed profile in three systems. 

further reveals that the RGRL-based system achieved a decrease in travel time ranging from 0.46 % to 16.02 % compared to the MARL-based method. Compared to the Optim-based method, the RGRL resulted in a decrease in travel time in low and medium scenarios \(under 75 % MPR\), but caused a slight increase in travel time in pure CAV environments. This improvement could be attributed to the RGRL-based system’s ability to classify future behaviors of MVs into different situations, allowing for consideration of their reactions and reducing the adverse effects caused by uncertainties in MV behavior. However, in pure CAV environments, all vehicle were controllable. In such cases, the Optim-based system is capable of generating an optimal solution without the distribution of MVs. 

Additionally, the RGRL-based system exhibited a lower frequency of large travel times compared to the MARL-based system and the 18 

*D. Zhou et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104807* 

**Table 3**

The performance of RGRL and MARL in the typical case. 

PET

Travel time

fuel

avg

min

max

avg

min

max

avg

min

max

RGRL

3.89

1.60

6.40

**13.41**

8.50

**21.40**

**22.00**

9.47

**31.29**

MARL

3.35

0.60

7.70

17.50

8.40

25.50

33.67

9.36

47.19

Optim

4.86

**2.0**

7.50

17.65

8.40

26.50

26.28

9.39

43.48

**Table 4**

Statistical analysis of the key performance indicators. 

**CAV rate**

**Strategy**

**PET\(s\)**

**Travel Time\(s\)**

**Fuel Consumption\(mL\)**

Mean

SD

diff. to RGRL

Mean

SD

diff. to RGRL

Mean

SD

diff. to RGRL

**0**

**RGRL/MARL/Optim**

3.82

2.18

—

10.41

5.35

—

32.01

11.01

—

**25**

**RGRL**

**3.69**

1.12

0

**19.68**

8.94

0

42.00

11.24

0

**MARL**

2.77

1.13

− 24.93 %

19.77

10.95

0.46 %

**39.37**

8.77

− 10.52 %

**Optim**

3.65

1.31

− 1.08 %

23.34

11.93

18.60 %

42.55

11.07

1.31 %

**50**

**RGRL**

**3.49**

1.13

0

**17.48**

7.58

0

**35.72**

12.74

0

**MARL**

2.72

1.25

–22.06 %

19.86

12.20

13.62 %

37.41

8.59

4.73 %

**Optim**

3.22

1.28

− 7.74 %

20.46

10.29

17.05 %

38.15

12.59

6.80 %

**75**

**RGRL**

**2.99**

1.17

0

**16.92**

6.64

0

**33.52**

13.37

0

**MARL**

2.53

1.21

− 15.38 %

19.63

12.81

16.02 %

35.56

8.10

6.09 %

**Optim**

2.84

1.18

− 5.02 %

18.15

7.87

7.27 %

35.38

12.03

5.55 %

**100**

**RGRL**

**2.70**

1.04

0

17.09

6.02

0

**31.66**

12.45

0

**MARL**

2.63

1.30

− 2.59 %

19.43

13.88

13.69 %

33.87

7.96

6.98 %

**Optim**

2.58

1.04

− 4.44 %

**16.66**

5.89

− 2.52 %

33.65

11.07

6.29 %

**Fig. 11. **Distribution of PETs under different methods. 

Optim-based system. This disparity stemmed from the fact that MARL-based CAVs prioritized self-benefit and were less affected by delays caused by trailing vehicles. In contrast, RGRL-based CAVs operated under the guidance of a central coordinator, making them more susceptible to the influence of trailing vehicles, thereby mitigating potential disruptions in the behavior of upcoming vehicles. 

Comparing the no-CAVs group with the high-MPR group, we observed that the inclusion of cooperative controlled CAVs with higher MPR contributed to improved system efficiency, regardless of the method employed. As the penetration rate of CAVs increased, 19 

*D. Zhou et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104807* 

**Fig. 12. **Distribution of travel times under different methods. 

more CAVs can cooperate and follow optimal control inputs, leading to an overall reduction in travel time. 

\(3\) Fuel consumption

Fig. 13 illustrates the distributions of fuel consumption when applying the three methods. Comparing the no CAVs group with the high penetration rate CAV group, it is evident that the inclusion of cooperative controlled CAVs, regardless of the method used, contributes to energy savings within the system. 

However, in the RGRL-based system at low CAV penetration rates \(25 %\), there were minimal changes in fuel consumption. This can be attributed to the fact that CAVs played a minor role in the system and were influenced by the behavior of manually driven vehicles. 

As the Market Penetration Rate \(MPR\) of CAVs exceeded 50 %, more CAVs in the RGRL-based system were able to move in a coordinated manner following desired situations, resulting in reduced overall fuel consumption. On the other hand, the MARL-based systems, which primarily assigned arrival times for vehicles, might yield feasible solutions but not necessarily an energy-saving schedule. For the Optim-based system, since the fuel consumption estimation is non-convex, considering it in planning would lead to a non-convex optimization problem. The optimization method chosen in this study did not take fuel consumption as the objective term, thus resulting in higher energy consumption than the RGRL method. Consequently, the difference in energy savings became more pronounced at higher CAV penetration rates. 

Overall speaking, the RGRL outperform in the tests because it introduces an iterative decision process that reduces the decision-space size, and avoids the expansion of uncertainty. Because of the chain reaction, the uncertainties of MV will affect all other vehicles’ actions, which yields an exponentially expanding space of action sequences. Directly searching the optimal action sequence for each CAV in such a larger action space, like what MARL does, is neither efficient, nor effective. RGRL reduces the decision-space size by dividing all sequential actions into several situations. The space for vehicle’s candidate intentions is a relative smaller decision space. 

Besides, RGRL eliminates the uncertain relationships based on the graph reasoning process. The iterative decision make decision per iteration before triggering the chain reaction. These two points allow RGRL to better address the multi-modal interactions and the uncertainties introduced by human drivers in the unsignalized intersection scenarios. Therefore it leads to better performance in terms 20 



*D. Zhou et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104807* 

**Fig. 13. **Distribution of fuel consumptions under different methods. 

of safety, efficiency and energy-saving. 

*5.5. Hardware-in-the-loop \(HIL\) experiment*

This paper conducted Hardware-in-the-loop \(HIL\) experiments to validate the model effectiveness. The overview of the HIL

experiment is presented in Fig. 14. Firstly, the high definition \(HD\) map of the test intersection was collected, and inputted into the **Fig. 14. **Overview of the HIL and VehIL experiment. 

21 

*D. Zhou et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104807* 

CAV domain controller and the MV simulation software. So MVs in this experiment is variable and unpredictable. The domain control unit \(DCU\) incorporates vehicle control algorithms and dynamic models. Each domain controller is equipped with a Jetson AGX Orin 32 GB processor, with a maximum computing power of up to 200 TOPS. MV simulation was based on a commercial software, TESS NG, while the MV driving model is a black box to us. In addition, a communication mechanism was developed to realize the state broadcast among CAVs and the state transmission between CAVs and the MV simulation software. Finally, during the process of scene operation, the information and state of each vehicle was sent to the visualization platform in real-time to achieve scenario visualization. 

The proposed method, and two comparative methods, were applied in the Domain Control Unit respectively. Fig. 15 \(a\) shows the Post Encroachment Time \(PET\) distribution under different cooperative methods and for different types of vehicles. On average, the PET is highest for the Optim cooperative system, followed by RGRL, with MARL being the smallest. Due to the hard constraints on the time difference passing through the conflict zone when establishing optimization, PET of Optim consistently surpasses 2 s, ensuring safety but leading to a certain degree of over-conservatism. Under the RGRL method, the variance of PET is smaller for CAV and bigger for MV. This suggests that under the MARL method, due to the clear rules of right-of-way, the movement of MV is less affected by CAV. 

On the other hand, under RGRL, MV is more affected by CAV, which corroborates the earlier argument that RGRL indirectly affects the movement of MV through the movement of CAV. Overall, all three cooperative methods meet safety requirements. 

Fig. 15 \(b\) presents the distribution of travel time under different methods and for different types of vehicles. The average values of travel time for three methods are close. From another perspective, it’s worth noting the proportion of long travel times \(travel time *>* 25\). The MARL method caused incidents of long travel times, while RGRL did not. This suggests that there’s no need for one or a few vehicles to excessively sacrifice their individual benefits for the overall efficiency under the RGRL method. 

The time consumption for one step updating was shown in Fig. 16. In the three methods, MARL consumes the least computational time for a single update, because it only needs to calculate the next action for each vehicle, while RGRL and Optim determine the order in which each vehicle passes and obtain the trajectories of the vehicles. However, the computation time for all three methods is less than 100 ms, therefore it can meet the real-time updates under the frequency of 10 Hz. 

*5.6. Vehicle-in-the-loop \(VehIL\) experiment*

Although the HIL experiments can test control strategies based on real hardware, they are still unable to fully simulate the complex dynamic behavior of actual vehicles. Therefore, we also conducted VehIL experiment, where actual vehicles are incorporated into the test system, to verify the effectiveness of the proposed method for dynamic traffic. 

Compared with the HIL testing platform, there were two main upgrades. The domain controllers were coupled to the empirical CAV

as the decision planning control unit, as Fig. 17 shows. The virtual test site was upgraded to a real test site. A typical crossroads intersection at the CAV Test Field of in Tongji University is selected as the studied site. 

We designed a typical scenario involving three actual CAVs and eight virtual MVs. Record of the scenario has been uploaded:

https://1drv.ms/f/s\!AvaECMkIADawhAzTOwPpfpL1BmXl?e=YnrOkG. Fig. 18 shows the snapshot of the scenario. 

The scenario operation outcome shows that, under the control of the proposed method, each CAV passes through once in a safe and orderly manner. Furthermore, since the operation of the MVs is driven by simulation software and their patterns are undisclosed to us, there exist uncertainties in their movements. Nonetheless, the proposed method can adapt to these uncertainties in the MVs’ behavior, thus ensuring the safe operation of the scenario. 

**6. Conclusion**

The paper addresses the challenges associated with cooperation for mixed traffic at unsignalized intersections. These challenges include MVs’ uncertainties, the chain reaction web and, the interaction diversity. To tackle these challenges, the paper proposes a Reasoning Graph-based Reinforcement Learning \(RGRL\) method that encodes complex interactions using a graph representation and trains a policy network to produce optimal situations. The following conclusions are drawn from the study: \(1\) The RGRL framework combines the advantages of graph reasoning MDP, RL, and GNN on muti-modal resolving, real-time decision, and interaction feature capturing, outperformed in the multi-interaction and mixed-traffic scenarios. The framework explores how to handle the conflicts between multiple mixed-traffic flows, which indicates its broader applicability in other conflicting-flow scenarios such as roundabouts, on-ramps, and the like. 

\(2\) The utilization of Graph Neural Networks \(GNNs\), specifically Graph Convolutional Networks \(GCN\) and Graph Attention Networks \(GAT\), allows for simulating chain reactions by aggregating simultaneous and diverse information among interactions. This enables the extraction of both individual and global features, facilitating improved problem-solving and faster training of the policy network. 

\(3\) The RGRL method establishes a mapping from vehicle intentions to systemic utilities at the situation level and individual utilities at the trajectory level. This approach not only considers instant control and arrival times of vehicles but also analyzes interaction outcomes and seeks optimal forms of interaction. Comparative tests with the Multi-Agent Reinforcement Learning \(MARL\) and Optimization-based methods across different CAV penetration rates demonstrate that the RGRL-coordinator significantly outperforms in terms of Post-Encroachment Time \(PET\) and efficiency. Hardware-in-the-loop \(HIL\) and Vehicle-in-the-loop \(VehIL\) experiments further validated the effectiveness of RGRL. 

One major concern in the paper is the flexible behavior of manually driven vehicles \(MVs\). The authors suggest integrating more 22 

*D. Zhou et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104807* 

**Fig. 15. **The distributions of PET and travel time. 

**Fig. 16. **Time consumption for one step updating. 

advanced motion prediction models into the RL training environment to account for this behavior. Additionally, future work can explore the applicability of the proposed method in different intersections, where the road structures and infrastructure are further encoded. Ongoing research is being conducted in these areas. 

**CRediT authorship contribution statement**

**Donghao Zhou: **Writing – review & editing, Writing – original draft, Visualization, Methodology, Conceptualization. **Peng Hang:** Writing – review & editing. **Jian Sun: **Writing – review & editing, Supervision, Project administration, Funding acquisition, Conceptualization. 

**Declaration of competing interest**

The authors declare that they have no known competing financial interests or personal relationships that could have appeared to influence the work reported in this paper. 

23 

*D. Zhou et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104807* 

**Fig. 17. **The retrofitted CAVs. 

**Fig. 18. **Scenario operation record. 

**Data availability**

Data will be made available on request. 

**Acknowledgement**

This research was sponsored by the National Natural Science Foundation of China \(52125208, 52232015\), Fundamental Research Funds for the Central Universities \(2022-5-ZD-02\) and the Shanghai Scientific Innovation Foundation \(No. 23DZ1203400\). 

**References**

Amouzadi, M., Orisatoki, M.O., Dizqah, A.M., 2023. Optimal lane-free crossing of CAVs through intersections. IEEE Trans. Veh. Technol. 72 \(2\), 1488–1500. 

Antonio, G.-P., Maria-Dolores, C., 2022. Multi-agent deep reinforcement learning to manage connected autonomous vehicles at tomorrow’s intersections. IEEE Trans. 

Veh. Technol. 71 \(7\), 7033–7043. 

Battaglia, P.W., Hamrick, J.B., Bapst, V., Sanchez-Gonzalez, A., Zambaldi, V., Malinowski, M., Tacchetti, A., Raposo, D., Santoro, A., Faulkner, R., Gulcehre, C., Song, F., Ballard, A., Gilmer, J., Dahl, G., Vaswani, A., Allen, K., Nash, C., Langston, V., Dyer, C., Heess, N., Wierstra, D., Kohli, P., Botvinick, M., Vinyals, O., Li, Y., Pascanu, R., 2018. Relational inductive biases, deep learning, and graph networks. *arXiv preprint arXiv:1806.01261*. 

Chen, C., Wang, J., Xu, Q., Wang, J., Li, K., 2021. Mixed platoon control of automated and human-driven vehicles at a signalized intersection: dynamical analysis and

optimal control. Transport. Res. Part C: Emerg. Technol. 127, 103138. 

Chen, C., Cai, M., Wang, J., Li, K., Xu, Q., Wang, J., Li, K., 2022. Cooperation method of connected and automated vehicles at unsignalized intersections: lane

changing and arrival scheduling. IEEE Trans. Veh. Technol. 71 \(11\), 11351–11366. 

Christodoulou, P., 2019. Soft Actor-Critic for Discrete Action Settings. *arXiv preprint arXiv:1910.07207*. 

Dresner, K., Stone, P., 2008. A multiagent approach to autonomous intersection management. J. Artif. Intell. Res. 31, 591–656. 

Faris, M., Falcone, P., Sjöberg, J., 2022. Optimization-Based Coordination of Mixed Traffic at Unsignalized Intersections Based on Platooning Strategy. In: 2022 IEEE

Intelligent Vehicles Symposium \(IV\), pp. 977–983. 

Fedral Highway Administration, 2023. About Intersection Safety, pp. https://highways.dot.gov/safety/intersection-safety/about. 

Gilmer, J., Schoenholz, S.S., Riley, P.F., Vinyals, O., Dahl, G.E., 2017. Neural Message Passing for Quantum Chemistry, *International Conference on Machine Learning*. 

PMLR, pp. 1263-1272. 

Gunarathna, U., Karunasekera, S., Borovica-Gajic, R., Tanin, E., 2022. Real-Time Intelligent Autonomous Intersection Management Using Reinforcement Learning, *2022 IEEE Intelligent Vehicles Symposium \(IV\)*, pp. 135-144. 

Guo, Z., Wu, Y., Wang, L., Zhang, J., 2023. Coordination for connected and automated vehicles at non-signalized intersections: A value decomposition-based

multiagent deep reinforcement learning approach. IEEE Trans. Veh. Technol. 72 \(3\), 3025–3034. 

24 

*D. Zhou et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104807* 

Haarnoja, T., Zhou, A., Abbeel, P., Levine, S., 2018. Soft Actor-Critic: Off-Policy Maximum Entropy Deep Reinforcement Learning with a Stochastic Actor, *International* *Conference on Machine Learning*. PMLR, pp. 1861-1870. 

Haarnoja, T., Zhou, A., Hartikainen, K., Tucker, G., Ha, S., Tan, J., Kumar, V., Zhu, H., Gupta, A., Abbeel, P., Levine, S., 2019. Soft Actor-Critic Algorithms and Applications. 

Hadjigeorgiou, A., Timotheou, S., 2023. Real-time optimization of fuel-consumption and travel-time of CAVs for cooperative intersection crossing. IEEE Trans. Intell. 

Veh. 8 \(1\), 313–329. 

Hu, Z., Huang, J., Yang, D., Zhong, Z., 2021. Constraint-tree-driven modeling and distributed robust control for multi-vehicle cooperation at unsignalized

intersections. Transport. Res. Part C: Emerg. Technol. 131, 103353. 

Huang, X., Lin, P., Pei, M., Ran, B., Tan, M., 2023. Reservation-Based Cooperative Ecodriving Model for Mixed Autonomous and Manual Vehicles at Intersections. IEEE

Trans. Intell. Transp. Syst. 1–17. 

Huang, S., Sadek, A.W., Zhao, Y., 2012. Assessing the mobility and environmental benefits of reservation-based intelligent intersections using an integrated simulator. 

IEEE Trans. Intell. Transp. Syst. 13 \(3\), 1201–1214. 

Jiang, H., Hu, J., An, S., Wang, M., Park, B.B., 2017. Eco approaching at an isolated signalized intersection under partially connected and automated vehicles

environment. Transport. Res. Part C Emerg. Technol. 79 \(JUN.\), 290–307. 

Jiang, S., Pan, T., Zhong, R., Chen, C., Li, X.-A., Wang, S., 2023a. Coordination of mixed platoons and eco-driving strategy for a signal-free intersection. IEEE Trans. 

Intell. Transp. Syst. 24 \(6\), 6597–6613. 

Jiang, X., Zhang, J., Shi, X., Cheng, J., 2023b. Learning the policy for mixed electric platoon control of automated and human-driven vehicles at signalized

intersection: a random search approach. IEEE Trans. Intell. Transp. Syst. 24 \(5\), 5131–5143. 

Karimi, M., Roncoli, C., Alecsandru, C., Papageorgiou, M., 2020. Cooperative merging control via trajectory optimization in mixed vehicular traffic. Transport. Res. 

Part C: Emerg. Technol. 116, 102663. 

Katriniok, A., Rosarius, B., Mähönen, P., 2022. Fully distributed model predictive control of connected automated vehicles in intersections: theory and vehicle

experiments. IEEE Trans. Intell. Transp. Syst. 23 \(10\), 18288–18300. 

Khan, S.M., Chowdhury, M., 2021. Situation-aware left-turning connected and automated vehicle operation at signalized intersections. IEEE Internet Things J. 8 \(16\), 

13077–13094. 

Levin, M.W., Rey, D., 2017. Conflict-point formulation of intersection control for autonomous vehicles. Transport. Res. Part C: Emerg. Technol. 85, 528–547. 

Li, D., Zhu, F., Chen, T., Wong, Y.D., Zhu, C., Wu, J., 2023. COOR-PLT: A hierarchical control model for coordinating adaptive platoons of connected and autonomous

vehicles at signal-free intersections based on deep reinforcement learning. Transport. Res. Part C: Emerg. Technol. 146, 103933. 

Luo, J., Zhang, T., Hao, R., Li, D., Chen, C., Na, Z., Zhang, Q., 2023. Real-time cooperative vehicle coordination at unsignalized road intersections. IEEE Trans. Intell. 

Transp. Syst. 24 \(5\), 5390–5405. 

Ma, C., Yu, C., Yang, X., 2021. Trajectory planning for connected and automated vehicles at isolated signalized intersections under mixed traffic environment. 

Transport. Res. Part C: Emerg. Technol. 130, 103309. 

National Center for Statistics Analysis, 2022. Traffic Safety Facts 2020: A Compilation of Motor Vehicle Crash Data. National Highway Traffic Safety Administration, 

Washington, DC. 

Ngoduy, D., Lee, S., Treiber, M., Keyvan-Ekbatani, M., Vu, H., 2019. Langevin method for a continuous stochastic car-following model and its stability conditions. 

Transport. Res. Part C: Emerg. Technol. 105, 599–610. 

Noh, S., 2019. Decision-making framework for autonomous driving at road intersections: safeguarding against collision, overly conservative behavior, and violation

vehicles. IEEE Trans. Ind. Electron. 66 \(4\), 3275–3286. 

Pan, X., Chen, B., Timotheou, S., Evangelou, S.A., 2023. A convex optimal control framework for autonomous vehicle intersection crossing. IEEE Trans. Intell. Transp. 

Syst. 24 \(1\), 163–177. 

Rios-Torres, J., Malikopoulos, A.A., 2018. Impact of partial penetrations of connected and automated vehicles on fuel consumption and traffic flow. IEEE Trans. Intell. 

Veh. 3 \(4\), 453–462. 

SAE, 2020. Taxonomy and Definitions for Terms Related to Cooperative Driving Automation for On-Road Motor Vehicles \(J3216\_202005\). 

Schuldt, F., Ulbrich, S., Menzel, T., Reschka, A., Maurer, M., 2015. Defining and Substantiating the Terms Scene, Situation, and Scenario for Automated Driving. IEEE

International Conference on Intelligent Transportation Systems. 

Schulman, J., Wolski, F., Dhariwal, P., Radford, A., Klimov, O., 2017. Proximal Policy Optimization Algorithms. *arXiv preprint arXiv:1707.06347*. 

Van Hasselt, H., Guez, A., Silver, D., 2016. Deep reinforcement learning with double Q-learning. AAAI 30 \(1\). 

Wang, Z., Schaul, T., Hessel, M., Hasselt, H., Lanctot, M., Freitas, N., 2016. Dueling Network Architectures for Deep Reinforcement Learning, *International Conference* *on Machine Learning*. PMLR, pp. 1995-2003. 

Wang, J., Zheng, Y., Xu, Q., Wang, J., Li, K., 2020. Controllability analysis and optimal control of mixed traffic flow with human-driven and autonomous vehicles. 

IEEE Trans. Intell. Transp. Syst. 

Xie, L., Wang, S., Markham, A., Trigoni, N., 2017. Towards Monocular Vision based Obstacle Avoidance through Deep Reinforcement Learning. *arXiv preprint arXiv:* *1706.09829*. 

Xu, H., Zhang, Y., Li, L., Li, W., 2019. Cooperative driving at unsignalized intersections using tree search. IEEE Trans. Intell. Transp. Syst. 21 \(11\), 4563–4571. 

Xu, H., Xiao, W., Cassandras, C.G., Zhang, Y., Li, L., 2022. A general framework for decentralized safe optimal control of connected and automated vehicles in multi-

lane signal-free intersections. IEEE Trans. Intell. Transp. Syst. 23 \(10\), 17382–17396. 

Yao, Z., Jiang, H., Jiang, Y., Ran, B., 2023. A two-stage optimization method for schedule and trajectory of CAVs at an isolated autonomous intersection. IEEE Trans. 

Intell. Transp. Syst. 24 \(3\), 3263–3281. 

Yao, H., Li, X., 2021. Lane-change-aware connected automated vehicle trajectory optimization at a signalized intersection with multi-lane roads. Transport. Res. Part

C: Emerg. Technol. 129, 103182. 

Yu, M., Long, J., 2022. An eco-driving strategy for partially connected automated vehicles at a signalized intersection. IEEE Trans. Intell. Transp. Syst. 23 \(9\), 

15780–15793. 

Yu, C., Sun, W., Liu, H.X., Yang, X., 2019. Managing connected and automated vehicles at isolated intersections: From reservation-to optimization-based methods. 

Transp. Res. B Methodol. 122, 416–435. 

Zegeye, S., De Schutter, B., Hellendoorn, J., Breunesse, E., Hegyi, A., 2013. Integrated macroscopic traffic flow, emission, and fuel consumption model for control

purposes. Transport. Res. Part C: Emerg. Technol. 31, 158–171. 

Zhan, W., Liu, C., Chan, C.Y., Tomizuka, M., 2016. A non-conservatively defensive strategy for urban autonomous driving. In: *2016 IEEE 19th International Conference* *on Intelligent Transportation Systems \(ITSC\)*. 

Zhang, D., Chen, X., Wang, J., Wang, Y., Sun, J., 2021. A comprehensive comparison study of four classical car-following models based on the large-scale naturalistic

driving experiment. Simul. Model. Pract. Theory 113, 102383. 

Zhang, J., Li, S., Li, L., 2023. Coordinating CAV swarms at intersections with a deep learning model. IEEE Trans. Intell. Transp. Syst. 24 \(6\), 6280–6291. 

Zhang, K., Zhang, D., de La Fortelle, A., Wu, X., Gregoire, J., 2015. State-driven priority scheduling mechanisms for driverless vehicles approaching intersections. IEEE

Trans. Intell. Transp. Syst. 16 \(5\), 2487–2500. 

Zhou, D., Ma, Z., Sun, J., 2020a. Autonomous vehicles’ turning motion planning for conflict areas at mixed-flow intersections. IEEE Trans. Intell. Veh. 5 \(2\), 204–216. 

Zhou, D., Ma, Z., Zhao, X., Sun, J., 2022. Reasoning Graph: A Situation-aware framework for cooperating unprotected turns under mixed connected and autonomous

traffic environments. Transport. Res. Part C: Emerg. Technol. 143, 103815. 

Zhou, M., Yu, Y., Qu, X., 2020b. Development of an efficient driving strategy for connected and automated vehicles at signalized intersections: a reinforcement

learning approach. IEEE Trans. Intell. Transp. Syst. 21 \(1\), 433–443. 

25 


# Document Outline

+ Reasoning graph-based reinforcement learning to cooperate mixed connected and autonomous traffic at unsignalized intersections  
	+ 1 Introduction 
	+ 2 Literature review  
		+ 2.1 Reservation-based methods 
		+ 2.2 Mathematical programming 
		+ 2.3 Reinforcement Learning \(RL\) 

	+ 3 Problem statement 
	+ 4 Methodology  
		+ 4.1 Framework 
		+ 4.2 The policy network  
			+ 4.2.1 The input layer 
			+ 4.2.2 The graph Convolution network \(GCN\) layer 
			+ 4.2.3 The graph attention \(GAT\) network 
			+ 4.2.4 The output layer 

		+ 4.3 Environment  
			+ 4.3.1 Speed profile generator 
			+ 4.3.2 Social compliance and collision checkers  
				+ 4.3.2.1 Social compliance checker 
				+ 4.3.2.2 Collision checker 


		+ 4.4 Reinforcement Learning methods 

	+ 5 Case study  
		+ 5.1 Setup  
			+ 5.1.1 Basic parameter settings 
			+ 5.1.2 Methods for comparison 

		+ 5.2 Training curves of different RL methods 
		+ 5.3 Typical case 
		+ 5.4 Statistical analysis of performances 
		+ 5.5 Hardware-in-the-loop \(HIL\) experiment 
		+ 5.6 Vehicle-in-the-loop \(VehIL\) experiment 

	+ 6 Conclusion 
	+ CRediT authorship contribution statement 
	+ Declaration of competing interest 
	+ Data availability 
	+ Acknowledgement 
	+ References



