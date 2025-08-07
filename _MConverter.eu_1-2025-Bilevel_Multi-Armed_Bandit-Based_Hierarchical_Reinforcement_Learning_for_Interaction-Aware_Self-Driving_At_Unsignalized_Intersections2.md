This article has been accepted for publication in IEEE Transactions on Vehicular Technology. This is the author's version which has not been fully edited and content may change prior to final publication. Citation information: DOI 10.1109/TVT.2025.3541401

1

Bilevel Multi-Armed Bandit-Based Hierarchical Reinforcement Learning for Interaction-Aware Self-Driving at Unsignalized Intersections Zengqi Peng, Yubin Wang, Lei Zheng, and Jun Ma, Senior Member, IEEE

Abstract—In this work, we present BiM-ACPPO, a bilevel diversity of road layouts \[4\], \[5\]. Apparently, inaccurate as-multi-armed bandit-based hierarchical reinforcement learning sessments regarding driving intentions of SVs, such as yielding framework for interaction-aware decision-making and planning or not, could significantly potentially lead to traffic accidents at unsignalized intersections. Essentially, it proactively takes the and congestion, thereby hindering the safe and efficient motion uncertainties associated with surrounding vehicles \(SVs\) into consideration, which encompass those stemming from the driver’s of the ego vehicle \(EV\) \[6\]. This is particularly evident at in-intention, interactive behaviors, and the varying number of SVs. 

tersections, where vehicles originating from diverse directions Intermediate decision variables are introduced to enable the high-are required to swiftly traverse a shared central zone to access level RL policy to provide an interaction-aware reference, for their respective target lanes without collisions. The situation guiding low-level model predictive control \(MPC\) and further becomes even more severe in unsignalized intersections which enhancing the generalization ability of the proposed framework. 

By leveraging the structured nature of self-driving at unsignalized generally exhibit unpredictable traffic patterns. Because the intersections, the training problem of the RL policy is modeled EV is required to interact with a varying number of SVs as a bilevel curriculum learning task, which is addressed by arriving from diverse directions simultaneously in the ab-the proposed Exp3.S-based BiMAB algorithm. It is noteworthy sence of traffic signals. Uncertainties arising from the driving that the training curricula are dynamically adjusted, thereby maneuvers and intentions of SVs present serious safety and facilitating the sample efficiency of the RL training process. 

Comparative experiments are conducted in the high-fidelity efficiency concerns in the interaction process. This requires CARLA simulator, and the results indicate that our approach enhancing the capabilities of the EV to prevent potential risks. 

achieves superior performance compared to all baseline methods. 

In this sense, self-driving at unsignalized intersections requires Furthermore, experimental results in two new urban driving advanced decision-making ability and interaction awareness to scenarios clearly demonstrate the commendable generalization interact safely and effectively with SVs exhibiting multi-modal performance of the proposed method. 

behaviors. 

Index Terms—Autonomous driving, hierarchical reinforcement Rule-based and optimization-based methods are two repre-learning, bilevel multi-armed bandit, automated curriculum learning, sample efficiency, generalization. 

sentative approaches for autonomous driving at intersections, both of which have been extensively studied. In general, rule-based methods predefine a series of rules about potential I. INTRODUCTION

traffic situations for autonomous vehicles to select suitable Recently, the autonomous driving community has observed behaviors from the rule base. A set of rules is designed to significant progress and impressive achievements across both regulate the order of vehicles to pass through the unsignalized academic research and industry applications \[1\], \[2\], \[3\]. In intersection complying with the law of road traffic safety \[7\], 

contrast to highway driving tasks, the challenges in urban

\[8\]. Nevertheless, it is difficult for rule-based approaches to driving tasks primarily arise from the complexity of the en-encompass the entire spectrum of traffic situations, typically vironment, including uncertain intentions among surrounding tending to conservative driving behaviors \[9\]. This could vehicles \(SVs\), frequent interactions between vehicles, and the cause traffic congestion and compromise traffic efficiency. 

On the other hand, optimization-based methods formulate the Copyright \(c\) 2025 IEEE. Personal use of this material is permitted. 

self-driving tasks as mathematical optimization problems that However, permission to use this material for any other purposes must be minimize a well-designed cost function subject to a set of obtained from the IEEE by sending a request to pubs-permissions@ieee.org. 

This work was supported in part by the National Natural Science Foundation constraints \[10\], \[11\], \[12\]. A two-stage optimization approach of China under Grant 62303390; in part by the Guangzhou-HKUST\(GZ\) Joint is proposed for self-driving tasks at unsignalized intersections Funding Scheme under Grant 2024A03J0618. \(Corresponding author: Jun by constructing the crossing problem as a mixed-integer linear Ma.\)

Zengqi Peng, Yubin Wang, and Lei Zheng are with the Robotics and programming and linear programming \[13\]. Considering the Autonomous Systems Thrust, The Hong Kong University of Science existence of non-cooperative vehicles, a differential game-and

Technology

\(Guangzhou\), 

Guangzhou

511453, 

China

\(e-mail:

based optimization strategy is proposed to make the con-zpeng940@connect.hkust-gz.edu.cn; 

ywang575@connect.hkust-gz.edu.cn; 

lzheng135@connect.hkust-gz.edu.cn\). 

trolled vehicle coordinate with non-cooperative SVs \[14\]. 

Jun Ma is with the Robotics and Autonomous Systems Thrust, The However, these methods are computationally expensive and Hong Kong University of Science and Technology \(Guangzhou\), Guangzhou time-consuming, and it is difficult to consider unexpected or 511453, China, and also with the Division of Emerging Interdisciplinary Areas, The Hong Kong University of Science and Technology, Hong Kong rapidly changing traffic scenarios. Furthermore, optimization-SAR, China. \(e-mail: jun.ma@ust.hk\). 

based approaches tend to struggle with poor task efficiency in Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on February 23,2025 at 10:55:39 UTC from IEEE Xplore. Restrictions apply. 

© 2025 IEEE. All rights reserved, including rights for text and data mining and training of artificial intelligence and similar technologies. Personal use is permitted, but republication/redistribution requires IEEE permission. See https://www.ieee.org/publications/rights/index.html for more information. 

This article has been accepted for publication in IEEE Transactions on Vehicular Technology. This is the author's version which has not been fully edited and content may change prior to final publication. Citation information: DOI 10.1109/TVT.2025.3541401

2

complex environments, particularly those involving SVs with provides a promising way to alleviate the above problems \[26\], 

diverse interactive behaviors. This could result in decisions

\[27\]. In \[28\], a stage-decaying curriculum learning approach that are potentially hazardous for autonomous vehicles. 

is proposed to guide the training of the RL policy. However, Reinforcement learning \(RL\) technologies have recently since the scheduling of curriculum shifts is predetermined shown significant potential in propelling the development of manually, the effectiveness of the training results relies on the autonomous driving community \[15\], \[16\], \[17\]. A multi-expert experience heavily. 

task DQN algorithm is proposed to control the speed of To address the above issues, diverse automated curriculum vehicles to navigate through intersections \[18\], where the learning methods have been proposed \[29\], \[30\]. An adaptive intersection navigation task is decomposed into several sub-curriculum-based method is utilized for training the RL poli-tasks for the construction of the reward function. However, it cies at single-lane intersections, which models various initial does not consider the difficulty and potential collision risks locations of the EV as curriculum features \[29\]. However, of different types of sub-tasks. A social attention module is the adjustment in the importance of curriculum depends on incorporated into the RL framework to balance the safety their respective weights, which could result in delayed or and efficiency of self-driving at intersections \[19\]. While even potentially failed transitions to curricula with promising RL-based methods have achieved impressive results at in-high rewards in the future. In \[30\], a state drop-out cur-tersection scenarios, most of these works do not consider riculum learning method is developed to learn an RL policy vehicle dynamics and driving comfort. To tackle this issue, at unsignalized intersections. It incrementally trains the RL

a potential solution is to integrate the RL with optimization-policy by omitting information about future states throughout based methods represented by model predictive control \(MPC\) the training process. Nevertheless, these works assume that

\[20\], \[21\]. In this sense, the MPC can consider state and SVs will not respond to the behavior of the EV, and their control constraints under the decisions provided by RL. This future trajectories are known to the EV. These simplifications solution combines their advantages to establish a hierarchical could jeopardize driving safety and degrade the generalization framework. A hybrid decision-making algorithm is designed ability of RL policies. It is worth noting that human drivers for autonomous vehicles at intersections \[22\], where high-would demonstrate diverse driving maneuvers according to level decisions are derived for the reference of a low-level the behaviors of SVs in the real world, which is crucial planning module. However, its action space only takes several for achieving safe and efficient interactions. An interactive basic behaviors, which could lead to poor maneuverability. 

planning framework is proposed for the behavior generation To enhance the maneuverability of the EV, an intuitive action of EV in an intersection scenario \[31\]. However, this work space, consisting of velocity and heading angle, is utilized only considers the intentions related to the task objectives of in \[23\] for unprotected left-turn tasks. However, the driving SVs while ignoring their responses to the behaviors of the intention of the SVs is assumed to not decelerate or yield to EV. Besides, the simple action space impedes the flexible the EV, which could limit the adaptability of the trained policy behaviors of the EV and also the generalization ability into in diverse situations, such as SV driving towards different various driving scenarios. Essentially, as most current studies lanes and giving way to the EV. Furthermore, this work solely do not comprehensively consider the interactive behaviors considers left-turn tasks at unsignalized intersections, which of SVs, these simplifications could limit the applicability of could limit the generalization ability of the trained policy in autonomous driving techniques in real-world scenarios. 

other types of tasks within unsignalized intersections, such Therefore, this paper presents a novel bilevel multias go-straight and right-turn tasks. Besides, go-straight tasks armed bandit-based automated curriculum PPO \(BiM-ACPPO\) at intersections present multiple potential collision points, framework, which integrates a bilevel multi-armed bandit thereby posing a challenge to self-driving vehicles. 

\(BiMAB\) module and a hierarchical RL framework, to im-Additionally, one significant limitation of the RL module prove training efficiency and driving performance. Through the within the hierarchical methods is the poor sample efficiency dynamic assessment and adjustment of the training process, the when it comes to complex driving environments \[24\]. The RL

RL agent will progressively enhance the self-driving strategy agent necessitates considerable training episodes to achieve at unsignalized intersections, starting from simple to more satisfactory performance due to the randomness of exploration. 

challenging scenarios. The main contributions are listed as Therefore, it would be challenging for RL agents to thoroughly follows:

explore the environment and learn effective policies within

• A

novel BiM-ACPPO framework is proposed for limited resources if without suitable guidance. To address interaction-aware

decision-making

and

planning

at

this problem, the environment model is incorporated into the unsignalized intersections, which can proactively handle RL algorithm to enhance the sample efficiency, where virtual the uncertainty stemming from the driving intentions of samples are generated to accelerate the training process \[25\]. 

SVs with multi-modal interaction behaviors and traffic However, the effectiveness of the trained policy is heavily density. A special action space is utilized to enhance the dependent on the accuracy of the model. The performance of generalization ability of the framework. 

the policy will be severely compromised if there is a significant

• A Exp3.S-based BiMAB algorithm is devised for auto-discrepancy between the environmental model and the actual mated curriculum selection by leveraging the structured environment. Additionally, directly training the RL agent nature of the self-driving tasks at unsignalized intersec-within complex environments could result in a solution with tions, thereby facilitating efficient sampling and effective limited driving performance. Curriculum learning technique exploration in the RL training process. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on February 23,2025 at 10:55:39 UTC from IEEE Xplore. Restrictions apply. 

© 2025 IEEE. All rights reserved, including rights for text and data mining and training of artificial intelligence and similar technologies. Personal use is permitted, but republication/redistribution requires IEEE permission. See https://www.ieee.org/publications/rights/index.html for more information. 

This article has been accepted for publication in IEEE Transactions on Vehicular Technology. This is the author's version which has not been fully edited and content may change prior to final publication. Citation information: DOI 10.1109/TVT.2025.3541401

3

• We demonstrate the effectiveness of the proposed ap-intentions are unknown. These configurations inject a signifi-proach in the high-fidelity simulator CARLA. The cant level of randomness into the driving scenarios, rendering BiMAB exhibits appropriate curriculum transition timing the tasks challenging but close to real-world situations. 

during the training process, and the proposed framework achieves superior performance and commendable gener-B. Vehicle Model

alization ability compared to all baseline methods. 

Since the EV drives at low speed in the task scenarios, the The rest of the paper is structured as follows. Section dynamic impact of the vehicle is negligible. Therefore, this II presents the problem statement. Section III illustrates the work utilizes the bicycle model \[32\] to describe the dynamics proposed BiMAB approach and hierarchical RL framework. 

of the EV, which is expressed as follows: Section IV demonstrates the experimental results followed by pertinent analysis. Finally, Section V summarizes the



v cos\(ψ \+ δ\) 

conclusion and discusses future works. 

v sin\(ψ \+ δ\)

˙x = f \(x, u\) = 





2v

, 

\(1\)

sin δ





L



II. P

a

ROBLEM STATEMENT

A. Problem Statement

where x = x

y

v

ψT is the state vector of the vehicle

In this work, the task scenario is set as a dual-lane unsignal-in the global coordinate Wg; x and y denote the X-coordinate ized intersection, which is shown in Fig. 1. The start position and Y-coordinate position of the center of the vehicle, respec-and target position of the EV are generated randomly within tively; ψ and v represent the heading angle and the speed, the lower region and the other three regions, respectively, respectively; u = a

δT is the control input vector; a and δ

obeying the traffic rules. A random number of SVs with are the acceleration and steering angle, respectively; L is the diverse interactive styles start from random positions of the inter-axle distance of the vehicle. 

upper, left, and right regions, and they drive towards respective target lanes simultaneously. The goal is to generate a control C. Model Predictive Control

action sequence to guide the EV to safely and swiftly complete First, we discretize \(1\) into the following model: diverse crossing tasks, including unprotected left-turn, go-straight, and right-turn tasks. 

xk\+1 = xk \+ f \(xk, uk\) · dk, 

\(2\)

where xk and uk represent the state vector and the control input vector at the time step k; f is the dynamic function; dk is the sampling interval. Let xg represent the goal state vector for the EV, which consists of the target location and orientation. 

The MPC aims to force the EV system to approach the goal state vector by solving a standard optimization problem as follows:

N

X

min

J = J \(xN , xg\) \+

J \(xk, uk, xg\), 

x1:N ,u0:N−1

s.t. 

xk\+1 = xk \+ f \(xk, uk\) dk, 

\(3\)

G\(x, u\) ≤ 0, 

H\(x, u\) = 0, 

Fig. 1. Overview of the task scenario. The EV is illustrated in red, while x

SVs are illustrated in blue. The uncertainties include the task and intention 0 = x\(k\), 

uncertainty of SVs and the varying number of SVs. All SVs will respond to where J \(x

the behavior of other vehicles. 

N , xg \) and J \(xk , uk , xg \) represent terminal cost and running cost, respectively; N is the length of the horizon; In contrast with \[29\] and \[30\], the behaviors of all vehicles G\(x, u\) ≤ 0 and H\(x, u\) = 0 are inequality constraints within the environment are interdependent, and different SVs and equality constraints, respectively; x0 is the initial state exhibit diverse driving styles, including aggressive, moderate, of the controlled system in the MPC problem. The control and conservative styles. For example, SVs could either yield or objective can be achieved by repeating the solving process and disregard potential collision risks and continue driving when execution in real-time until the system reaches the goal state interacting with other vehicles at conflict points or potential xg. For complex and dynamic environments, MPC with fixed collision points. Hence, the SVs in the target scenarios demon-parameters could encounter issues such as high computational strate multi-modal and interactive behaviors. Additionally, burdens, compromised driving safety, and poor adaptability. In the number of SVs is also not fixed in diverse scenario this work, novel high-level decision variables are introduced configurations. In this context, the EV is required to complete for parameterization of the MPC formulation. Then the output various crossing tasks in the environment with the interactive of the MPC can be modulated to generate diverse behaviors SVs. Here, we assume that the EV can access the position and for the EV to interact with multi-model SVs by leveraging the velocity information of SVs, while their goal tasks and driving decoded value of the high-level decision variables. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on February 23,2025 at 10:55:39 UTC from IEEE Xplore. Restrictions apply. 

© 2025 IEEE. All rights reserved, including rights for text and data mining and training of artificial intelligence and similar technologies. Personal use is permitted, but republication/redistribution requires IEEE permission. See https://www.ieee.org/publications/rights/index.html for more information. 

This article has been accepted for publication in IEEE Transactions on Vehicular Technology. This is the author's version which has not been fully edited and content may change prior to final publication. Citation information: DOI 10.1109/TVT.2025.3541401

4

Fig. 2. Overview of the BiM-ACPPO approach for interaction-aware self-driving at unsignalized intersections with interactive SVs. The EV and SVs are illustrated in red and blue, respectively. The proposed BiMAB framework models the training process as a bilevel clustered structure. The variables within the first layer and the second layer, are the number of SVs and the task type of the EV, respectively. The solid car and the semi-transparent cars within the BiMAB module denote the start position and the target position of the EV, respectively. 

D. Learning Environment

where A1, A2, and A3 represent the waypoint sub-action In this work, the target tasks can be modeled as a Markov space, reference velocity sub-action space, and lane change Decision Process \(MDP\), where all vehicles are located near sub-action space, respectively. The RL agent selects a set the intersection. Here, we express the MDP as a tuple E =

of actions within the A. Then these actions are decoded to

⟨S, A, P, R, γ⟩, where elements S, A, P, R, γ are defined as parameterize the low-level MPC to control the EV. Details follows:

will be illustrated in Section III-C. 

State space S: In this work, S comprises kinematic features State transition dynamics P\(Sk\+1|Sk, ak\): It specifies the of EV and SVs within the observation range of the EV. The changes of environmental state, adhering the Markov property. 

state matrix at time step k is defined as follows: It is implicitly defined by the external environment and cannot be accessed by the RL agent. 

h

N max iT

S

sv

k =

s0 s1 ... s

, 

\(4\)

Reward function R: Here, we assign a positive reward if k

k

k

the RL agent finishes a target task to facilitate the improvement where N max denotes the maximum number of SVs; s0 and sv

k

of the RL policy. A negative reward would be assigned if the si \(i = 1, 2, ..., N max\) represent the state of the EV and the k

sv

agent maintains survival during the task process to incentivize state of the i-th SV, respectively. Specifically, si is defined as k

the RL agent to finish the tasks efficiently. It also penalizes follows:

collisions and frequent lane-changing behaviors. Details will be introduced in Section III-C. 

si = xi

yi

vi

ψi T , 

\(5\)

k

k

k

k

k

Discount factor γ: γ ∈ \(0, 1\) is adopted for accumulated where xi and yi represent the X-axis and Y-axis coordinates discount rewards in the future. 

k

k

of the vehicle i in the world coordinate system, respectively; vi is the speed of the i-th vehicle; ψi denotes the heading k

k

III. METHODOLOGY

angle of the i-th vehicle. 

A. Overview of the Proposed Framework

Action space A: In this work, a multi-discrete action space including three discrete sub-action spaces is adopted for the The workflow of the proposed method is illustrated in Fig. 2. 

RL agent:

Specifically, a novel Exp3.S-based BiMAB module is utilized to select the curricula, which determines the initial settings for A = \{A1, A2, A3\} , 

\(6\)

the training environment of the RL agent. Then the RL agent Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on February 23,2025 at 10:55:39 UTC from IEEE Xplore. Restrictions apply. 

© 2025 IEEE. All rights reserved, including rights for text and data mining and training of artificial intelligence and similar technologies. Personal use is permitted, but republication/redistribution requires IEEE permission. See https://www.ieee.org/publications/rights/index.html for more information. 



This article has been accepted for publication in IEEE Transactions on Vehicular Technology. This is the author's version which has not been fully edited and content may change prior to final publication. Citation information: DOI 10.1109/TVT.2025.3541401

5

selects actions based on its observation, which is then decoded subsets, which are characterized by a progressively increasing and inputted into the MPC as high-level decision variables number of SVs. Each subset consists of N max sub-curricula, sc

for parameterization. Subsequently, the parameterized MPC

representing different task types of EV within the correspond-generates the control inputs based on the defined objective ing subset. Specifically, the bilevel curriculum set is expressed function and constraints, which are applied to the EV. Relevant as follows:

information is recorded in the rollout buffer for updating the BiMAB policy and the RL policy. Details will be discussed Ω = \{Ωij|i = 0, 1, ..., N max, j = 0, 1, ..., N max\} , ss

sc

\(7\)

in the following sections. 

where i denotes the serial number of the subset, which is equivalent to the number of SVs within corresponding B. Exp3.S-based BiLevel Multi-Armed Bandit Algorithm for curricula; j is the serial number of the sub-curriculum, which Curriculum Learning

means the type of the driving task, and j = 0, 1, 2 represents a Autonomous driving tasks at unsignalized intersections are left-turn task, go-straight task, and right-turn task, respectively. 

typical instances of tasks with clustered structures. The number It is noted that N max is equal to N max. Within this set, each sv

ss

of SVs and the type of crossing task are the two main factors subset can be considered as a cluster, and correspondingly, affecting the complexity of self-driving tasks at unsignalized each sub-curriculum can be regarded as an arm within the intersections. The difficulty level increases rapidly as the context of the BiMAB problem \[33\], \[34\]. Following the above number of SVs grows. This is because the EV needs to interact analysis, the curriculum selection in \(7\) can be considered as with SVs coming from various directions simultaneously, and a sampling process within the BiMAB M, which consists of these SVs have different destinations and driving intentions, N max \+ 1 clusters and N max \+ 1 arms. Therefore, the BiMAB

ss

sc

introducing significant uncertainty into the tasks. 

agent can derive a sample sequence of clusters and arms over Different types of traversal tasks have various levels of T episodes for the training of the RL agent: challenge. The right-turn task, which involves completing a small radius turn along the road boundary and primarily \(CT , AT \) = \{\(cs,1, as,1\), \(cs,2, as,2\), ..., \(cs,T , as,T \)\} , \(8\) dealing with the integration of other SVs into the target lane, where CT and AT are the sampled cluster sequence and arm is deemed the simplest. The go-straight task requires the EV

sequence across the RL training process, respectively; cs,i and to traverse through the central region of the intersection and as,i are the sampled cluster and arm within the BiMAB in potentially interact with SVs from three different directions, the i-th episode. When an episode ends, the rollout buffer which is more complex than the right-turn task. The left-turn of the RL agent returns a final reward. Then the BiMAB

task, in addition to the challenges present in the go-straight agent adjusts the importance weights based on this reward task, necessitates a change in direction and experiences a in conjunction with the historical rewards. Our objective is to longer distance in the central region, thereby rendering it the develop an adaptive strategy to maximize payoffs generated most difficult of the intersection driving tasks. A collision from the sampled cluster and arm sequence \(CT , AT \): point analysis for left-turn, go-straight, and right-turn tasks at a single-lane intersection is shown in Fig. 3. The figure XT

wC∗, wA∗ = arg

max

ˆ

r\(t\), 

\(9\)

enumerates the number of collision points for each task when wC ,wA,\(C

t=1

T ,AT \)

there is one SV in the scenario. As the number of SVs where wC and wA are non-negative importance weight vec-and lanes increases, the complexity of collision situations tors of the clusters and arms in the BiMAB; wC∗ and wA∗

escalates, leading to a geometric growth in the task difficulty. 

denote the optimal importance weight vectors of the clusters and arms in the BiMAB; ˆ

r\(t\) represents the rescaled reward

of the BiMAB, which depends on the reward received from the RL agent. 

2\) Exp3.S-based BiMAB Algorithm for Automated Curriculum Selection: For the BiMAB model M constructed before, the importance weights wC \(t\), wA\(t\) and the probability distributions pC \(t\), pA\(t\) are defined as follows: wC \(t\) = \{wc\(t\)|i = 0, 1, ..., N max\} , 

\(a\) SV from the upper \(b\) SV from the left re- \(c\) SV from the right i

ss

region \(L:2; S:1; R:1\). gion \(L:2; S:2; R:1\). 

region \(L:2; S:3; R:0\). 

pC \(t\) = \{pc\(t\)|i = 0, 1, ..., N max\} , 

i

ss



Fig. 3. Potential collision points for EV \(red car\) crossing the intersection wA\(t\) = wa \(t\)|i = 0, 1, ..., N max, j = 0, 1, ..., N max , ij

ss

sc

with the SV \(blue car\). L, S, and R represent the number of potential collision points when the EV performs diverse tasks. 

pA\(t\) = pa \(t\)|i = 0, 1, ..., N max, j = 0, 1, ..., N max . 

ij

ss

sc

\(10\)

The proposed BiMAB module is shown in Fig. 2, which is In our specific problem, the optimal cluster and optimal arm used for the allocation of training curricula. 

change across various stages of the training process due to 1\) Task Decomposition and Bilevel Curriculum Modelling: the variation in the anticipated rewards, which are related to Based on the above analysis, we model the training process task settings and the improvement of the RL policy during of the RL policy at unsignalized intersections as a bilevel the training process. Drawing inspiration from the Exp3.S

curriculum learning task. Our curriculum set includes N max algorithm \[35\], we can tackle this problem by integrating an ss

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on February 23,2025 at 10:55:39 UTC from IEEE Xplore. Restrictions apply. 

© 2025 IEEE. All rights reserved, including rights for text and data mining and training of artificial intelligence and similar technologies. Personal use is permitted, but republication/redistribution requires IEEE permission. See https://www.ieee.org/publications/rights/index.html for more information. 

This article has been accepted for publication in IEEE Transactions on Vehicular Technology. This is the author's version which has not been fully edited and content may change prior to final publication. Citation information: DOI 10.1109/TVT.2025.3541401

6

additional ε-greedy factor into the probability update mecha-not sampled in the t-th episode is 0. Here, we perform an nism. This ensures that each cluster and arm maintains a non-absolute value operation on the received reward value, aiming zero probability of selection throughout the training duration. 

to enable the BiMAB agent to utilize information related to With the importance weights wC \(t\) and wA\(t\) determined at the courses where the RL policy is currently underperforming. 

the t-th episode, the sampling probabilities of the i-th cluster Additionally, we proportionally scale the normalized reward and j-th arm within the i-th cluster can be calculated as rij

norm\(t\) for the corresponding cluster and arm based on their follows:

selection probability. This allows clusters and arms that could ewc\(t\)

be optimal but currently have low probabilities to be timely i

η

pc\(t\) = \(1 − η\)

\+

, 

i

identified through algorithm updates. Then the importance PN max

ss

ewc \(t\)

N max \+ 1

k

k=0

ss

weights of i-th cluster, and j-th arm within i-th cluster are i = 0, 1, ..., N max, 

ss

adjusted as follows:

\(11\)

ewa \(t\)

ij

η

pa \(t\) = \(1 − η\)

\+

, 

ij

wc\(t \+ 1\) = wc\(t\) \+ αcˆ

ri\(t\) \+ βcWi\(t\), 

PN max

i

i

sc

ewa \(t\)

N max \+ 1

ik

\(16\)

k=0

sc

wa \(t \+ 1\) = wa \(t\) \+ αaˆ

rij\(t\) \+ βaWij\(t\), 

i = 0, 1, ..., N max, j = 0, 1, ..., N max, ij

ij

ss

sc

where η is a positive constant that balances the exploitation where Wi\(t\) = PNmax

ss

wc\(t\), W

wa \(t\); α

i=0

i

ij \(t\) = PN max

sc

j=0

ij

c, 

of obtained experiences and random exploration. Within the αa, βc, and βa are positive constant parameters for adjusting framework where the task exhibits a clustered structure, the the growth rate of importance weights of each cluster and each BiMAB model introduces an equivalent update mechanism for arm, respectively. 

the clusters. We first derive a cluster sample c\(t\) at t-th episode Based on the calculated importance weights, specific cur-according to the distribution pC \(t\) as follows: ricula are sampled for training the RL policy. In practical cM\(t\) ∼ M\(pC \(t\), pA\(t\)\). 

\(12\)

deployment, due to the inherent randomness of sampling and the stochastic generation of SVs, it is difficult to avoid Then the BiMAB agent chooses an arm sample ac\(t\) for inefficient samples completely during the training process. 

the RL agent from the sampled cluster cM\(t\) according to To prevent occasional sampling that leads to misestimation corresponding possibility distribution pA\(t\) as follows: towards the importance of clusters and arms, we utilize a target ac\(t\) ∼ M\(pA\(t\)|cM\(t\)\). 

\(13\)

BiMAB

ˆ

M to stabilize the update process of BiMAB M. 

After receiving the final reward from the RL agent, the target Once the cluster and arm are sampled, the RL environment BiMAB agent updates its parameters based on the rescaled is initialized according to the corresponding curriculum set-rewards. Then, after a certain number of curricula are sampled, tings. The BiMAB agent will obtain a reward rij\(t\) from the the importance weights of the target BiMAB are synchronized RL agent when this episode ends. After the RL agent finishes to the BiMAB to proceed with the selection of curricula for an episode, receiving a positive reward indicates a successful the next phase. Therefore, the update of importance weights interaction with the environment that meets expectations, within the BiMAB can be rewritten as follows: whereas receiving a negative reward suggests the occurrence



of undesired events or dangerous situations such as collisions wc\(t\), if t|N

i

BiM AB ̸= 0, 



during that episode. For the RL policy, negative rewards mean wc\(t \+ 1\) =

i

wc\(t\) \+ Pt

\(α

i

k=t−N

c ˆ

ri\(k\)

BiM AB \+1

poor performance in that scenario, indicating the need for



\+βcWi\(k\)\), otherwise, 

further training. Based on the above analysis, it is essential



wa \(t\), if t|N

ij

BiM AB ̸= 0, 

for the BiMAB module to appropriately modulate the received



wa \(t \+ 1\) =

ij

wa \(t\) \+ Pt

\(α

ij

k=t−N

a ˆ

ri\(k\)

negative rewards to facilitate the training of the RL policy. In BiM AB \+1



\+βaWij\(k\)\), otherwise, 

this work, the rescaled reward for the BiMAB is defined as \(17\)

follows:

where NBiMAB is the update interval for synchronization



ˆ

r

\(t\) , 

between the target BiMAB ˆ

M and the BiMAB M. 



i\(t\) = rij

norm



pi\(t\)



The complete procedure of the proposed Exp3-based ˆ

r

\(t\)

\(14\)

ij \(t\) = rij

norm

, 

pij \(t\)

BiMAB algorithm for automated curriculum selection is sum-







rij

norm\(t\) =

2\(rmd−k0Rmin\(t\)\)

− 1, 

k

marized in Algorithm 1. 

1 Rmax \(t\)−k0 Rmin \(t\)

where



r

r

ij \(t\), if

rij\(t\) ≥ 0, 

md =

\(15\)

−α

C. High-Level PPO for Decision-Making

mdrij \(t\), otherwise, 

where ˆ

ri\(t\) and ˆ

rij\(t\) represent the rescaled reward for i-th Within the proposed framework, the RL policy is employed cluster and corresponding j-th arm within the i-th cluster ob-to generate high-level decision variables, which account for tained in t-th episode, respectively; Rmax\(t\) and Rmin\(t\) are the trade-off between safety and efficiency throughout the the maximum and minimum absolute values of the unscaled autonomous driving task process. Specifically, the RL agent rewards in the history up to the current episode, respectively; aims to decide a sequence of the intermediate points as the k0, k1, and αmd denote positive constants for the rescaling reference of low-level MPC. We use the notation of subscript procedure. The reward for both cluster and arm that are k to represent the k-th time step within an episode. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on February 23,2025 at 10:55:39 UTC from IEEE Xplore. Restrictions apply. 

© 2025 IEEE. All rights reserved, including rights for text and data mining and training of artificial intelligence and similar technologies. Personal use is permitted, but republication/redistribution requires IEEE permission. See https://www.ieee.org/publications/rights/index.html for more information. 

This article has been accepted for publication in IEEE Transactions on Vehicular Technology. This is the author's version which has not been fully edited and content may change prior to final publication. Citation information: DOI 10.1109/TVT.2025.3541401

7

Algorithm 1: Exp3.S-based BiMAB Algorithm The specific definitions of the sub-action spaces in \(6\)

Input: Curriculum set Ω, BiMAB update frequency are introduced as follows. The waypoint sub-action space is N

defined as:

BiM AB

Output: Selected cluster cM, selected arm ac A1 = \{WP0, WP1, ..., WP4\} , 

\(22\)

1 Initialize the BiMAB and target BiMAB with weights where WPi in A1 represents the i-th waypoint, which can be

\{wc\}, \{ ˆ

wc\}, wa , and ˆ

wa , where

i

i

ij

ij

represented as follows:

i = 0, 1, ..., N max, j = 0, 1, ..., N max; ss

sc

2 while t ≤ t

WP

yWP ψWP\]T , 

\(23\)

max do

i = \[xWP

i

i

i

3

Compute probability distributions of clusters pc\(t\) where xWP, yWP, and ψWP denote the reference information from \(11\); 

i

i

i

about the X-axis, Y-axis coordinates, and heading angle of 4

Derive a sample cluster cM\(t\) from \(12\); 

the waypoint, respectively. Waypoints are provided by a pre-5

Compute probability distributions of arms pC \(t\) a

in

defined road map and several path-searching methods, such cluster cM\(t\) from \(11\); 

as A∗ search algorithm. The visualization of the sub-action 6

Derive a sample arm ac\(t\) from \(13\); 

space A1 is shown in Fig. 4\(a\), where the EV drives from the 7

Play arm ac\(t\) and apply corresponding Ω\(t\) to lower region towards the central zone. A reference waypoint the RL environment for initialization; 

set is generated using A\* search at the beginning of the task. 

8

Receive the terminal reward rij\(t\) from the RL

When the EV is in the lower area, the 5 waypoints closest agent; 

to the EV \(WP′ , i = 0, 1, ..., 4

i

\) are added to the A1. Before

9

Compute the rescaled reward ˆ

ri\(t\) and ˆ

rij\(t\) from

each decision-making process, the RL agent checks the relative

\(14\); 

positions of all waypoints in the reference waypoint set against 10

Update the corresponding cluster and arm weight the position of the EV, and updates the sub-action space A within the target BiMAB from \(16\); 

1. 

Specifically, any waypoints located behind the current position 11

if t | NBiMAB = 0 then

of the EV are removed from the reference waypoint set. Then 12

wi\(t\) = ˆ

wi\(t\), i = 0, 1, ..., N max; 

ss

the 5 waypoints closest to the EV \(WPi, i = 0, 1, ..., 4\) in the 13

wij\(t\) = ˆ

wij\(t\), i = 0, 1, ..., N max, j =

ss

new updated reference waypoint set comprise A 0, 1, ..., N max; 

1. The RL

sc

agent then selects the appropriate action from this updated 14

end

sub-action space A1. It is worth noting that both the reference 15 end

waypoint set and A1 are consistently checked and updated throughout the task. Specifically, the first waypoint WP0 is the waypoint closest to the EV, thereby enabling the functionality 1\) Observation and Action Generation: Here, we define the for stopping and yielding. Distant waypoints guide the EV

observations for the RL agent as follows: towards the target position in diverse modes. According to

\[36\], \[37\], the maximum reference speed is set to 8 m/s. The h

N max iT

O

sv

reference velocity sub-action space is defined as: k =

o0 o1 ... o

, 

\(18\)

k

k

k

A2 = \{0, 2, 4, 6, 8\} , 

\(24\)

where o0 = \[˜

x0 ˜

y0 v0 ˜

ψ0\]T ; ˜

x0 and ˜

y0 represent the absolute

k

k

k

k

k

k

k

differences between the current X-axis and Y-axis coordinates where the unit of the elements is m/s. The lane change sub-of the EV and these of the goal location, respectively; v0

action space is defined as:

k

denotes the current speed of the EV; ˜

ψ0 is the difference

k

A3 = \{−1, 0, 1\} , 

\(25\)

between the current heading angle and the goal heading angle. 

oi \(i = 1, 2, ..., N max\) is defined as follows: where −1, 0, and 1 represent left lane change, lane keeping, k

ss

and right lane change maneuvers, respectively. The visualiza-o

T

tion of A3 can be referred to in Fig. 4\(b\). In Fig. 4\(b\), the EV

k = dxi

dyi

dvi

dψi

, 

\(19\)

k

k

k

k

detects an SV ahead, so it changes lanes to the left to avoid where

a potential collision and prepares for the left-turn maneuver. 



dxi = clip\(|x0 − xi |, 0, 7.5\), 

By configuring the action space in this manner, the RL agent



k

k

k





dyi = clip\(|y0 − yi |, 0, 7.5\), 

is not only equipped with navigation and obstacle avoidance k

k

k

\(20\)

dvi = v0 − vi , 

capabilities but also can be generalized to various driving



k

k

k





dψi = ψ0 − ψi , 

scenarios that feature regular road structures and waypoints. 

k

k

k

Remark 1: By constructing an action space composed of where clip\(·\) is a clip function to pre-process the correspond-

\(22\), \(24\), and \(25\), we can facilitate flexible motion pat-ing elements to constrain them within a predefined range. 

terns for the EV to interact with SVs exhibiting multi-modal In this work, the RL policy is represented by a neural behaviors. When the EV needs to drive towards the target network π parameterized by θ. Given the RL observation O

location rapidly, the RL agent can select the most distant k

at time step k, the action of the RL agent is generated by: waypoint and a high reference speed. Conversely, when the EV

requires an emergency brake to yield, the RL agent can choose aRL = π

k

θ \(Ok \)

\(21\)

the nearest waypoint and a low reference speed. Moreover, Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on February 23,2025 at 10:55:39 UTC from IEEE Xplore. Restrictions apply. 

© 2025 IEEE. All rights reserved, including rights for text and data mining and training of artificial intelligence and similar technologies. Personal use is permitted, but republication/redistribution requires IEEE permission. See https://www.ieee.org/publications/rights/index.html for more information. 

This article has been accepted for publication in IEEE Transactions on Vehicular Technology. This is the author's version which has not been fully edited and content may change prior to final publication. Citation information: DOI 10.1109/TVT.2025.3541401

8

collision penalty rC are designed as follows: rS\(IS\) = IS · \(α1 · Nsv \+ α2 · Npcp\), 

−1

rF\(¬IS\) = min\(rF,max, ¬IS · α3 · dF

\), 

\(28\)

e2g

rC\(IC\) = IC · α4 · Nsv · vEV, 

where Npcp denotes the number of potential collision points; rF,max is the maximum reward for the failed episodes; αi are constant parameters, where i = 1, 2, · · · , 4. The remaining reward terms are assigned constant values. 

3\) Training with BiM-ACPPO: After sampling a cluster and \(a\) Update process of A1. 

\(b\) Lane-changing behavior. 

a corresponding arm in the BiMAB, the RL agent explores Fig. 4. Visualization of designed action space of RL agent. 

the environment set by the configuration of the selected curriculum. Relevant observations, actions, and rewards within respective episodes are recorded in the replay buffer. Once the introduction of a lane-changing sub-action space further a certain number of episodes have been gathered, the RL

enhances the flexibility of motion for the EV. When the RL

policy undergoes training to optimize the cumulative objective agent decides to change lanes to the left or right, the selected function that is associated with the sequence of sampled waypoint will be replaced by the corresponding waypoint on cluster-arm pairs \(CT , AT \) as follows: the adjacent lane. Choosing a closer waypoint on the adjacent θ∗ = arg

max

J \(θ\), 

\(29\)

lane indicates an urgent lane change to avoid collisions, while θ,\(CT ,AT \)

picking a further waypoint on the adjacent lane means a where J \(θ\) denotes the objective function for the RL policy smooth lane change for collision avoidance or overtaking. 

with parameter θ. Here, the clipped objective function of the 2\) Reward Function: The reward function is crucial for PPO algorithm \[38\] is utilized for the update of the RL policy: motivating RL agents to explore the environment. Therefore, h



i

it is essential to design an appropriate reward function that Jk\(θ\) = Ek min ρk\(θ\) Âk, clip \(ρk\(θ\), 1 − ϵ, 1 \+ ϵ\) Âk

, 

is able to guide the RL agent to balance driving safety and \(30\)

efficiency during the training process. Taking into account the where ρk\(θ\) represents the probability ratio of the new policy specific characteristics of the target scenarios addressed in this to the old policy; Âk denotes the estimator of the advantage study, the reward function is designed as follows: function at time step k; ϵ is the clip parameter. To reduce the variance of the long-term return estimation, the generalized r\(k\) = r

advantage estimation \(GAE\) is adopted. Furthermore, to bal-S\(IS\) \+ rF\(¬IS\) \+ rC\(IC\) \+ rTO\(ITO\)

\(26\)

\+ r

ance the exploration and exploitation, and also stabilize the LC\(ILC\) \+ rl, 

policy update, a temporary policy network is utilized for the implementation. 

where rS and rF denote the rewards for task completion and failure by the RL agent, respectively; rC, rTO, rLC, and rl denote the penalty for collisions, time-out situations, laneD. Low-Level RL-Guided Model Predictive Control changing behaviors, and surviving in the task, respectively. 

Upon receiving the current observation, the RL policy Ievent serves as an indicator function, marking the occurrence chooses high-level decision variables, which are then decoded of diverse events. It is defined as follows: and passed into the low-level MPC to generate control actions. 

The MPC is utilized for the motion control of the EV at 1, if event occurs, 

I

the low level of the proposed framework. Typically, MPC

event =

\(27\)

0, otherwise, 

uses the target location as the reference state in the receding horizons to force the EV to reach its destination swiftly. How-To facilitate curriculum switching, the success reward term ever, incorporating highly non-convex and nonlinear collision r

avoidance constraints into the MPC formulation is necessary S is configured to depend on the number of SVs and potential collision points, which can encourage the RL agent to explore to ensure the safety of the EV, which significantly increases the the tasks with high difficulty levels. To assist the RL agent in computational burden, especially in complex driving scenarios learning from failed episodes, we set the failure reward r such as unsignalized intersections. In this work, we introduce F to

be related to the distance dF

of the EV from the goal location

an intermediate reference state to guide the EV to avoid e2g

when the episode ends. Furthermore, to improve the interaction collisions, which is determined by RL policy. This replaces the awareness of the RL agent, the penalty for collisions r target location as the reference state of the MPC formulation. 

C is

structured to have a positive correlation with both the speed The intermediate reference state vector is defined as follows: of the EV vEV and the count of SVs. Furthermore, the penalty x

T

IMR = xIMR

yIMR

vIMR

ψIMR

\(31\)

for lane-changing maneuvers is added to avoid non-compliant and frequent lane-changing behaviors. Among these reward where xIMR and yIMR are the intermediate reference X-axis and terms, the success reward rS, the failure reward rF, and the Y-axis coordinates of the EV in the world coordinate system, Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on February 23,2025 at 10:55:39 UTC from IEEE Xplore. Restrictions apply. 

© 2025 IEEE. All rights reserved, including rights for text and data mining and training of artificial intelligence and similar technologies. Personal use is permitted, but republication/redistribution requires IEEE permission. See https://www.ieee.org/publications/rights/index.html for more information. 

This article has been accepted for publication in IEEE Transactions on Vehicular Technology. This is the author's version which has not been fully edited and content may change prior to final publication. Citation information: DOI 10.1109/TVT.2025.3541401

9

respectively; vIMR is the intermediate reference speed of the Algorithm 2: BiM-ACPPO

EV; ψIMR denotes the intermediate reference heading angle of Input: Environmental state Sk, RL policy update the EV. Here, we replace the goal point xg in \(3\) with the frequency NRL

intermediate point which is determined by the RL agent. 

Output: πθ∗ = f \(θ∗\)

In the proposed framework, the MPC is tasked with tracking 1 Initialize the policy network and the temporary policy the intermediate reference states generated by the RL policy, network with parameter θ0, θt0; 

while ensuring both the reduction of vehicle energy consump-2 Derive a sample Ω\(t\) according to Algorithm 1; 

tion and the maintenance of driving comfort. Given the high-3 Initialize the RL environment based on the sampled level decision variable xIMR and the current state of the EV

curriculum Ω\(t\); 

xk = \[xk yk vk ψk\]T , the autonomous driving task can be 4 while t ≤ tmax do

formulated as an MPC problem over the receding horizon N . 

5

while not done do

Considering the non-holonomic dynamics constraint and box 6

RL agent chooses high-level decision variables constraints of the velocity and control commands of the EV, from \(21\); 

a nonlinear and nonconvex-constrained optimization problem 7

Decode the high-level decision variables to can be formulated as follows:

obtain the intermediate reference vector xIMR; N −1

8

Parameterize the MPC \(32\) and calculate the X

min

Jx \+

\(Jx \+ Ju \+ J∆u \)

control action; 

x

N

k

k

k

1:N ,u0:N −1

k=0

9

Apply the control action to the EV, obtain the s.t. 

xk\+1 = xk \+ f \(xk, uk\) dk, 

reward rk\(t\) and the next state sk\+1\(t\); u

\(32\)

10

end

min ≤ uk ≤ umax, 

11

Record related information of episodes experienced vmin ≤ vk ≤ vmax, 

by the RL agent, including the history of states, x0 = xcurrent, 

actions, and rewards; 

12

Update the temporary policy network by \(29\); 

13

Feed the reward at the end of the t-th episode to where

BiMAB in Algorithm 1; 

Jx = \(x

N

N − xIMR\)T Qx\(xN − xIMR\), 

14

if t | NRL = 0 then

J

15

Synchronize the parameters of the temporary x

= \(x

k

k − xIMR\)T Qx\(xk − xIMR\), 

\(33\)

policy network to the current policy network; Ju = uT Q

k

k

uuk , 

16

end

J∆u = ∆uT Q

k

k

∆u∆uk , 

17

Derive a sample Ω\(t\) according to Algorithm 1; 

where ∆u

18

Reset the unsignalized intersection based on the k = uk −uk−1 is the variation of control commands; x

sampled curriculum Ω\(t\); 

current represents the current state vector of the EV; Qx, Qu, and Q

19 end

∆u are positive semi-definite diagonal weighting matrices for corresponding terms. 

20 Save the final policy network π∗ = f \(θ∗\). 

θ

The complete procedure of the proposed BiM-ACPPO

framework is summarized in Algorithm 2. 

problem is solved by CasADi \[40\], with the IPOPT option and IV. EXPERIMENTS

single-shooting approach. The weighting matrices Qx, Qu, A. Experimental Setup

and Q∆u are set to diag \(\[100, 100, 100, 20\]\), diag \(\[10, 10\]\), and diag \(\[1, 1\]\), respectively. In this work, the proposed In this section, we implement the BiM-ACPPO approach framework is compared with four baseline approaches as in two different unsignalized intersections and an overtaking follows:

scenario. The experiments are carried out on the Ubuntu 18.04 system with 2.60GHz Intel\(R\) Xeon\(R\) Platinum 8358P

• Fixed PPO: the RL policy is directly trained by PPO

CPU and NVIDIA GeForce RTX 4090 GPU. All self-driving approach \[38\] in the target scenario with Nsv = N max. 

sv

scenarios involved in experiments are constructed on the

• Random CPPO: the probability distributions of all clus-CARLA simulator \[39\]. Here, we set the Tesla Model 3 as ters and arms in the curriculum set are equal. 

the self-driving vehicle. The actor-critic architecture is adopted

• Manual CPPO: the RL policy is trained by a simplified to implement the proposed method. The action network and implementation of \[28\] with a fixed ϵ. 

critic network are set as fully connected networks with 2

• RD-ACPPO: implementation of the approach in \[41\] with hidden layers of 256 units and 128 units by PyTorch and MPC as the low-level controller. 

trained with the Adam optimizer. The number of epochs is For the sake of fairness, we set the clip parameters of all set to 20. The learning rates of the action network and critic methods to ϵ = 0.2. The SVs are in built-in autopilot mode network are set to 5 × 10−4 and 1 × 10−3, respectively. γ is which is provided by the CARLA simulator. We first train the set to 0.99. The initial weights of BiMAB are set to wc\(0\) =

RL policy in the unsignalized intersection scenario. Then the i

1, wa \(0\), i = 0, 1, ..., N max, j = 0, 1, ..., N max. η is set to test of all trained RL policies at unsignalized intersections with ij

ss

sc

0.2. NBiMAB is set to 1000. The low-level MPC optimization different numbers of SVs Nsv = 0, 1, ..., N max and diverse sv

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on February 23,2025 at 10:55:39 UTC from IEEE Xplore. Restrictions apply. 

© 2025 IEEE. All rights reserved, including rights for text and data mining and training of artificial intelligence and similar technologies. Personal use is permitted, but republication/redistribution requires IEEE permission. See https://www.ieee.org/publications/rights/index.html for more information. 

This article has been accepted for publication in IEEE Transactions on Vehicular Technology. This is the author's version which has not been fully edited and content may change prior to final publication. Citation information: DOI 10.1109/TVT.2025.3541401

10

\(a\) Arms in first cluster. 

\(b\) Arms in second cluster. 

\(c\) Arms in third cluster. 

\(d\) Arms in fourth cluster. 

Fig. 6. Weight updates of three arms in respective clusters during the training process. 

TABLE I

SAMPLED TIMES OF CLUSTERS AND ARMS WITHIN BIMAB

Nss

0

1

2

3

Sampled Times

456

536

1291

2718

Nsc

0

1

2

0

1

2

0

1

2

0

1

2

Sampled Times

268

90

98

193

278

65

627

489

175

1788

666

264

driving tasks are conducted. 

More details about the weight evolutions in BiMAB are illustrated in Figs. 5-6. It is observable that as training progresses, the weights in the first layer of BiMAB gradually B. Dual-Lane Unsignalized Intersections

shift from cluster Nss = 0 to cluster Nss = 3. This indicates We select a dual-lane intersection from the Town05 map that BiMAB dynamically assesses the learning progress of for the deployment, where the traffic lights are deactivated to the strategy and executes a timely shift in the curriculum. 

create an unsignalized intersection scenario. In this case, the Specifically, as the performance of the RL policy improves, the maximum number of SVs is set to N max = 3. The start and sv

BiMAB allocates increasingly challenging training episodes to target positions of the EV and SVs are randomly generated the RL agent. This strategic allocation enables the RL agent to while complying with traffic rules, as described in Section II. 

master complex driving skills step by step, thereby allowing 1\) Training Results: The trend of weight changes for each it to achieve higher rewards in more challenging scenarios. 

cluster \(subset\) and arm \(sub-curriculum\) of the BiMAB

Furthermore, because right-turn tasks are relatively simpler within the proposed method during the training process is compared to the other two types of crossing tasks, the weights illustrated in Figs. 5-6 and Table I. According to Table I, we associated with the arm for right-turn tasks decrease as training can find that the sampling times of the four clusters increase progresses across all clusters. In contrast, the weights for left-with the number of SVs throughout the entire training process. 

turn and go-straight tasks exhibit diverse trends of change This is because as the number of SVs increases, the difficulty across different clusters, yet both types of tasks experience of the task also increases, requiring more training episodes periods of high weight in various stages of training. This for RL agents to learn and update strategies. This process is pattern is also evident from Table I, which shows that right-automatically assigned through real-time evaluation of the RL

turn tasks have the fewest training instances. Despite the policy during training by BiMAB. Within specific clusters, potential collision points being equal for both left-turn and the sampling frequency of arms corresponding to left-turn and go-straight tasks, the left-turn tasks involve a longer distance go-straight tasks surpasses that of right-turn tasks, and the through the central region of the unsignalized intersections, difference in sampling frequency increases significantly with leading to a higher potential frequency of interaction with SVs. 

the increase in the number of SVs. This phenomenon occurs Consequently, BiMAB allocates a higher number of instances because the first two tasks are more challenging than right-turn to left-turn tasks compared to go-straight tasks. 

tasks, thereby resulting in such allocation results. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on February 23,2025 at 10:55:39 UTC from IEEE Xplore. Restrictions apply. 

© 2025 IEEE. All rights reserved, including rights for text and data mining and training of artificial intelligence and similar technologies. Personal use is permitted, but republication/redistribution requires IEEE permission. See https://www.ieee.org/publications/rights/index.html for more information. 

This article has been accepted for publication in IEEE Transactions on Vehicular Technology. This is the author's version which has not been fully edited and content may change prior to final publication. Citation information: DOI 10.1109/TVT.2025.3541401

11

TABLE II

PERFORMANCE COMPARISON AT DUAL-LANE UNSIGNALIZED INTERSECTIONS AMONG DIFFERENT METHODS. 

N

Methods

sv =0

Nsv=1

Nsv=2

Nsv=3

S\(%\)

C\(%\)

TO\(%\)

S\(%\)

C\(%\)

TO\(%\)

S\(%\)

C\(%\)

TO\(%\)

S\(%\)

C\(%\)

TO\(%\)

Left Turn

98

0

2

76

24

0

64

36

0

36

64

0

Fixed PPO

Go Straight

92

0

8

79

18

3

72

24

4

48

52

0

Right Turn

100

0

0

98

1

1

98

2

0

96

4

0

Left Turn

100

0

0

83

17

0

60

40

0

54

46

0

Manual CPPO

Go Straight

100

0

0

84

16

0

78

22

0

66

34

0

Right Turn

100

0

0

100

0

0

98

2

0

97

3

0

Left Turn

100

0

0

82

18

0

66

34

0

44

56

0

Random CPPO

Go Straight

100

0

0

84

16

0

70

30

0

62

38

0

Right Turn

100

0

0

100

0

0

96

1 4

0

84

16

0

Left Turn

100

0

0

86

14

0

79

21

0

69

31

0

RD-ACPPO

Go Straight

100

0

0

86

14

0

77

23

0

73

27

0

Right Turn

100

0

0

100

0

0

100

0

0

98

2

0

Left Turn

100

0

0

94

6

0

85

15

0

80

20

0

BiM-ACPPO

Go Straight

100

0

0

93

7

0

87

13

0

84

16

0

Right Turn

100

0

0

100

0

0

100

0

0

100

0

0

Note: S, C, and TO represent success rate, collision rate, and timeout rate, respectively. 

2\) Performance Evaluation: To quantitatively compare the can assist in enhancing the generalization performance of the performance of the BiM-ACPPO with the baseline methods, RL policy across different scenario settings. 

we conduct tests on RL policies trained by all methods in the Among all testing results attained by the BiM-ACPPO

dual-lane unsignalized intersection with the number of SVs approach, we pick up one result from each of the three ranging from 0 to 3. Each policy undergoes 100 repeated tests different crossing tasks at the unsignalized intersection for in each type of crossing task. The test results are summarized demonstration. The snapshots of these three examples are in Table II. 

presented in Fig. 7. 

According to this table, it is evident that the proposed

• Left-turn task: At 0.4 s, the RL policy outputs an approach achieves the highest success rate in all testing tasks intermediate waypoint in the left lane to guide the EV

and settings, although the success rate decreases as the number to change lanes in preparation for the left-turn crossing of SVs increases. This result indicates the effectiveness of task. Subsequently, at 2.3 s, the RL policy detects an SV

BiMAB in improving the training outcomes of the RL policy. 

approaching from the left region to execute a go-straight Besides, we can find that the performance of RL policies crossing task without showing any intention to yield. 

trained across various scenario settings generally surpasses that Therefore, the RL policy selects the nearest waypoint and of Fixed PPO, with RL policies utilizing curriculum learning a low reference speed to perform the yield behavior. Once outperforming Random PPO. Furthermore, the success rate the SV has passed and is no longer in front of the EV, of RL policies that automatically allocate curricula based the RL policy then chooses a distant waypoint along with solely on the number of SVs is higher than that of manually a high reference speed to rapidly direct the EV towards assigned curricula, while lower than that of proposed BiMAB. 

the target region at 3.2 s. Ultimately, the EV finishes the It is noteworthy that the success rate of the RL policy based left-turn task under the guidance of the RL policy. 

on BiMAB significantly exceeds that of RD-ACPPO. This

• Go-straight task: Because there are no SVs in the central highlights the efficacy of leveraging the structured nature of region, the RL policy chooses a distant waypoint and a unsignalized intersection tasks for curriculum modeling, as high reference speed as an intermediate point to guide the well as the effectiveness of the Algorithm 1. 

EV for rapid transit from 0 s to 2.2 s. At 2.8 s, the RL

Meanwhile, the success rates of BiM-ACPPO in left-turn policy observes two SVs entering the central region from and go-straight tasks are similar across different numbers of the right region, posing a potential collision risk. Thus, it SVs, while they are lower than that of right-turn tasks, which selects the nearest waypoint and a low reference speed to corroborates the analysis presented in Section III-B regarding prevent potential collisions. Between 2.8 s and 3.9 s, the the three types of crossing tasks at unsignalized intersections. 

two SVs from the right region, with the SV in the right This discrepancy is due to the significantly higher number of lane indicating an intent to turn right and the SV in the potential collision points in the latter two tasks compared to left lane showing an intention to yield, prompt the RL

right-turn tasks, necessitating more interactions with SVs that policy to choose a distant waypoint to swiftly guide the exhibit uncertain driving intentions. The complexity of these EV through the central region. Finally, the EV completes interactive processes exponentially increases with the number the go-straight task. 

of SVs. Additionally, the Fixed PPO policy experiences time-

• Right-turn task: The EV is initialized in the left lane, out results in testing scenarios where the number of SVs with its destination being the left lane of the right region ranged from 0 to 2. This reveals that directly training the RL

of the unsignalized intersection. Between 0 s and 1.1

agent in complex environments could lead to poor generaliza-s, the RL policy selects a waypoint in the right lane tion to unseen scenarios, while curriculum learning techniques to guide the EV to change lanes in preparation for a Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on February 23,2025 at 10:55:39 UTC from IEEE Xplore. Restrictions apply. 

© 2025 IEEE. All rights reserved, including rights for text and data mining and training of artificial intelligence and similar technologies. Personal use is permitted, but republication/redistribution requires IEEE permission. See https://www.ieee.org/publications/rights/index.html for more information. 

This article has been accepted for publication in IEEE Transactions on Vehicular Technology. This is the author's version which has not been fully edited and content may change prior to final publication. Citation information: DOI 10.1109/TVT.2025.3541401

12

\(a\) Left-turn task. The EV is initialized in the right lane, and its target position is set to the left lane of the left region. 

\(b\) Go-straight task. The EV is initialized in the left lane, and its target position is set to the left lane of the upper region. 

\(c\) Right-turn task. The EV is initialized in the left lane, and its target position is set to the left lane of the right region. 

Fig. 7. Key frames of the three demonstrations with our method in an unsignalized intersection within CARLA. The upper and lower side of the sub-figures shows the third-person views of the EV and the bird-eye views. The green rectangles in the third-person sub-figures denote the intermediate point determined by the RL policy. The red rectangle and the green rectangles in the bird-eye sub-figures represent the EV and SVs, respectively. 

right turn. From 2 s to 2.7 s, the RL policy observes the 1\) Zero-Shot

Generalization

Ability

Into

Single-Lane

SVs that come from the left region are at a sufficiently Unsignalized Intersections: In this experiment, we choose safe distance, which poses no potential collision risk. 

a single-lane unsignalized intersection in the map Town03

Therefore, it outputs a sub-nearest waypoint to direct the of the CARLA simulator as the testing scenario. Other test EV through a tight turn with a small radius into the right settings are similar to dual-lane unsignalized intersections in lane of the right region of the unsignalized intersection. 

Section IV-B. During testing, RL policies trained by Fixed At 4.9 s, the EV successfully enters the target region PPO, Manual CPPO, and Random CPPO are almost incapable under the guidance of the RL policy and changes lanes of completing intersection crossing tasks in this new scenario. 

to reach its target location. 

Therefore, we present the results of 100 repeated tests on RD-ACPPO and the proposed framework, which are shown in Table III. 

C. Generalization Ability Into New Scenarios Since the BiMAB automatically modulates the curricu-To demonstrate the generalization ability of the proposed lum in line with the training progress of the RL policy, framework, we deploy the RL policies obtained in IV-B to it can effectively guide the RL agent towards an enhanced conduct tests in two new driving scenarios for validation. 

exploration of the environment. This enables the trained RL

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on February 23,2025 at 10:55:39 UTC from IEEE Xplore. Restrictions apply. 

© 2025 IEEE. All rights reserved, including rights for text and data mining and training of artificial intelligence and similar technologies. Personal use is permitted, but republication/redistribution requires IEEE permission. See https://www.ieee.org/publications/rights/index.html for more information. 

This article has been accepted for publication in IEEE Transactions on Vehicular Technology. This is the author's version which has not been fully edited and content may change prior to final publication. Citation information: DOI 10.1109/TVT.2025.3541401

13

TABLE III

PERFORMANCE COMPARISON AT SINGLE-LANE UNSIGNALIZED INTERSECTIONS AMONG DIFFERENT METHODS. 

N

Methods

sv =0

Nsv=1

Nsv=2

Nsv=3

S\(%\)

C\(%\)

TO\(%\)

S\(%\)

C\(%\)

TO\(%\)

S\(%\)

C\(%\)

TO\(%\)

S\(%\)

C\(%\)

TO\(%\)

Left Turn

100

0

0

77

23

0

75

25

0

56

44

0

RD-ACPPO

Go Straight

100

0

0

75

25

0

65

35

0

53

47

0

Right Turn

100

0

0

88

12

0

84

16

0

82

18

0

Left Turn

100

0

0

91

9

0

85

15

0

80

20

0

BiM-ACPPO

Go Straight

100

0

0

96

4

0

89

11

0

82

18

0

Right Turn

100

0

0

100

0

0

100

0

0

97

3

0

Note: S, C, and TO represent success rate, collision rate, and timeout rate, respectively. 

Fig. 8. Key frames of the demonstration with our method in the overtaking task. SVs in the left lane and middle lane are set to low-speed mode. 

policy to gain an improved comprehension of the environment, observes that the SV ahead is moving slower than the EV, handle uncertainty in the environment well, and demonstrate prompting it to change lanes to the right at a low reference enhanced generalization capabilities. Additionally, comprehen-speed to guide the EV into the middle lane to achieve safe sive utilization of the inherent task structure at unsignalized in-and efficient driving behavior. At 1.3 s, the RL agent notices tersections within the BiMAB framework facilitates a superior that the SVs in the left and middle lanes showed no intention success rate in the novel single-lane unsignalized intersection of accelerating, while an SV in the right lane is accelerating. 

scenarios compared to RD-ACPPO. 

Therefore, between 1.3 s and 1.8 s, the RL policy guides the 2\) Few-Shot Generalization Ability Into Overtaking Driving EV to change lanes to the right one. Finally, at 4.4 s, the EV

Scenarios: To further validate the generalization of the pro-completes the overtaking task and continues driving forward. 

posed method, we also conduct tests on the overtaking task in Based on the experimental results, we can observe that an urban driving scenario. Here, we select the long outer ring the proposed framework demonstrates commendable general-road with 3 lanes in the map Town05 of the CARLA simulator ization ability across different test scenarios, which can be as the testbed. The RL policy trained by the BiM-ACPPO

attributed to the design of the overall framework. Firstly, the approach is fine-tuned and then applied in the constructed automatic curriculum learning mechanism based on BiMAB

overtaking scenario. Here, we consider 3 SVs with the Tesla enables the RL policy to interact with the environment from Model 3. All SVs are in built-in autopilot mode and initialized easy to difficult during training, thereby enhancing the training in random positions. During the fine-tuning stage, a random efficiency and the performance of the trained policy. Secondly, number of SVs \(Nsv = 0, 1, 2\) is set to a low-speed mode the introduction of the hierarchical RL structure along with a with different speed limits. During the testing phase, several multi-discrete action space allows the trained RL policy to SVs are randomly set to low-speed mode to block traffic to achieve a high success rate and perform well in scenarios not verify the overtaking ability of the RL policy. Several SVs are encountered during training. 

randomly set to low-speed mode to block traffic to verify the overtaking ability of the RL policy. We conduct 100 repeated V. CONCLUSION

tests on the proposed framework, which achieves a success rate In this work, we present a novel BiMAB-based hierarchical of 97%. The results indicate the commendable generalization RL framework for interaction-aware self-driving at unsignal-ability of the proposed method in overtaking tasks. 

ized intersections, which aims to address the uncertainties Among all the results attained by the proposed method, we arising from multi-modal behaviors and varying number of pick up one result for demonstration, which is shown in Fig. 

SVs. The training problem of the RL policy in target sce-

8. In this example, the EV is initialized in the left lane, with narios is modeled as a bilevel curriculum learning task and the SVs in the left and middle lanes set to low-speed mode. 

is addressed by the proposed BiMAB algorithm. Experimen-Specifically, the speed limits for the SVs on the left and in tal results demonstrate that our BiMAB could automatically the middle are set to 10% and 20% of the normal speed evaluate the learning progress and adaptively assign suitable limit, respectively. Between 0.5 s and 1.3 s, the RL policy curricula for the RL agent throughout the training process. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on February 23,2025 at 10:55:39 UTC from IEEE Xplore. Restrictions apply. 

© 2025 IEEE. All rights reserved, including rights for text and data mining and training of artificial intelligence and similar technologies. Personal use is permitted, but republication/redistribution requires IEEE permission. See https://www.ieee.org/publications/rights/index.html for more information. 

This article has been accepted for publication in IEEE Transactions on Vehicular Technology. This is the author's version which has not been fully edited and content may change prior to final publication. Citation information: DOI 10.1109/TVT.2025.3541401

14

Our approach achieves the highest success rates compared

\[18\] S. Kai, B. Wang, D. Chen, J. Hao, H. Zhang, and W. Liu, “A multi-task to all baseline methods in statistical testing experiments. 

reinforcement learning approach for navigating unsignalized intersections,” in Proceedings of the Intelligent Vehicles Symposium. 

IEEE, 

Furthermore, the proposed method showcases commendable 2020, pp. 1583–1588. 

generalization ability in new scenarios. Demonstrations in dif-

\[19\] Y. Liu, Y. Gao, Q. Zhang, D. Ding, and D. Zhao, “Multi-task safe ferent driving scenarios highlight the interaction-aware ability reinforcement learning for navigating intersections in dense traffic,” 

Journal of the Franklin Institute, vol. 360, no. 17, pp. 13 737–13 760, of the proposed method with multi-modal SVs. 

2023. 

REFERENCES

\[20\] Y. Song and D. Scaramuzza, “Policy search for model predictive control with application to agile drone flight,” IEEE Transactions on Robotics, 

\[1\] Y. Xing, C. Lv, H. Wang, H. Wang, Y. Ai, D. Cao, E. Velenis, and F.-Y. 

vol. 38, no. 4, pp. 2114–2130, 2022. 

Wang, “Driver lane change intention inference for intelligent vehicles:

\[21\] Y. Wang, Y. Li, Z. Peng, H. Ghazzai, and J. Ma, “Chance-aware lane Framework, survey, and challenges,” IEEE Transactions on Vehicular change with high-level model predictive control through curriculum Technology, vol. 68, no. 5, pp. 4377–4390, 2019. 

reinforcement learning,” in Proceedings of the International Conference

\[2\] S. Mozaffari, O. Y. Al-Jarrah, M. Dianati, P. Jennings, and A. Mouza-on Robotics and Automation. 

IEEE, 2024. 

kitis, “Deep learning-based vehicle behavior prediction for autonomous

\[22\] T. Tram, I. Batkovic, M. Ali, and J. Sjöberg, “Learning when to drive in driving applications: A review,” IEEE Transactions on Intelligent Trans-intersections by combining reinforcement learning and model predictive portation Systems, vol. 23, no. 1, pp. 33–47, 2020. 

control,” in Proceedings of the International Intelligent Transportation

\[3\] X. Lu, H. Zhao, C. Li, B. Gao, and H. Chen, “A game-theoretic Systems Conference. 

IEEE, 2019, pp. 3263–3268. 

approach on conflict resolution of autonomous vehicles at unsignalized

\[23\] M. Al-Sharman, R. Dempster, M. A. Daoud, M. Nasr, D. Rayside, and intersections,” IEEE Transactions on Intelligent Transportation Systems, W. Melek, “Self-learned autonomous driving at unsignalized intersec-vol. 24, no. 11, pp. 12 535–12 548, 2023. 

tions: A hierarchical reinforced learning approach for feasible decision-

\[4\] B. Paden, M. Čáp, S. Z. Yong, D. Yershov, and E. Frazzoli, “A survey of making,” IEEE Transactions on Intelligent Transportation Systems, motion planning and control techniques for self-driving urban vehicles,” 

vol. 24, no. 11, pp. 12 345–12 356, 2023. 

IEEE Transactions on Intelligent Vehicles, vol. 1, no. 1, pp. 33–55, 2016. 

\[24\] Y. Huang, S. Yang, L. Wang, K. Yuan, H. Zheng, and H. Chen, “An

\[5\] L. Zheng, R. Yang, Z. Peng, M. Y. Wang, and J. Ma, “Spatiotemporal efficient self-evolution method of autonomous driving for any given receding horizon control with proactive interaction towards autonomous algorithm,” IEEE Transactions on Intelligent Transportation Systems, driving in dense traffic,” IEEE Transactions on Intelligent Vehicles, 2024. 

vol. 25, no. 1, pp. 602–612, 2024. 

\[6\] J. Nan, W. Deng, and B. Zheng, “Intention prediction and mixed strategy

\[25\] Y. Guan, Y. Ren, S. E. Li, Q. Sun, L. Luo, and K. Li, “Centralized nash equilibrium-based decision-making framework for autonomous cooperation for connected and automated vehicles at intersections by driving in uncontrolled intersection,” IEEE Transactions on Vehicular proximal policy optimization,” IEEE Transactions on Vehicular Tech-Technology, vol. 71, no. 10, pp. 10 316–10 326, 2022. 

nology, vol. 69, no. 11, pp. 12 597–12 608, 2020. 

\[7\] G. Lu, L. Li, Y. Wang, R. Zhang, Z. Bao, and H. Chen, “A rule based

\[26\] Y. Bengio, J. Louradour, R. Collobert, and J. Weston, “Curriculum control algorithm of connected vehicles in uncontrolled intersection,” 

learning,” in Proceedings of the International Conference on Machine in Proceedings of the International Intelligent Transportation Systems Learning. 

ACM, 2009, pp. 41–48. 

Conference. 

IEEE, 2014, pp. 115–120. 

\[27\] Y. Song, H. Lin, E. Kaufmann, P. Dürr, and D. Scaramuzza, “Au-

\[8\] A. Aksjonov and V. Kyrki, “Rule-based decision-making system for tonomous overtaking in Gran Turismo sport using curriculum rein-autonomous vehicles at intersections with mixed traffic environment,” 

forcement learning,” in Proceedings of the International Conference on in Proceedings of the International Intelligent Transportation Systems Robotics and Automation. 

IEEE, 2021, pp. 9403–9409. 

Conference. 

IEEE, 2021, pp. 660–666. 

\[28\] Z. Peng, X. Zhou, Y. Wang, L. Zheng, M. Liu, and J. Ma, “Curriculum

\[9\] R. Tian, N. Li, I. Kolmanovsky, Y. Yildiz, and A. R. Girard, “Game-proximal policy optimization with stage-decaying clipping for self-theoretic modeling of traffic in unsignalized intersection network for driving at unsignalized intersections,” in Proceedings of the International autonomous vehicle control verification and validation,” IEEE Transac-Intelligent Transportation Systems Conference. IEEE, 2023, pp. 5027–

tions on Intelligent Transportation Systems, vol. 23, no. 3, pp. 2211–

5033. 

2226, 2020. 

\[29\] Z. Qiao, K. Muelling, J. M. Dolan, P. Palanisamy, and P. Mudalige, 

\[10\] L. Riegger, M. Carlander, N. Lidander, N. Murgovski, and J. Sjöberg, 

“Automatically generated curriculum based reinforcement learning for

“Centralized MPC for autonomous intersection crossing,” in Proceedings autonomous vehicles in urban environment,” in Proceedings of the of the International on Intelligent Transportation Systems Conference. 

Intelligent Vehicles Symposium. 

IEEE, 2018, pp. 1233–1238. 

IEEE, 2016, pp. 1372–1377. 

\[30\] S. Khaitan and J. M. Dolan, “State dropout-based curriculum reinforce-

\[11\] M. Kneissl, A. Molin, H. Esen, and S. Hirche, “A feasible MPC-ment learning for self-driving at unsignalized intersections,” in 2022

based negotiation algorithm for automated intersection crossing,” in IEEE/RSJ International Conference on Intelligent Robots and Systems. 

Proceedings of the European Control Conference. 

IEEE, 2018, pp. 

IEEE, 2022, pp. 12 219–12 224. 

1282–1288. 

\[12\] Z. Huang, S. Shen, and J. Ma, “Decentralized iLQR for cooperative

\[31\] C. Xia, M. Xing, and S. He, “Interactive planning for autonomous driv-trajectory planning of connected autonomous vehicles via dual consensus ing in intersection scenarios without traffic signs,” IEEE Transactions on ADMM,” IEEE Transactions on Intelligent Transportation Systems, Intelligent Transportation Systems, vol. 23, no. 12, pp. 24 818–24 828, vol. 24, no. 11, pp. 12 754–12 766, 2023. 

2022. 

\[13\] Z. Yao, H. Jiang, Y. Jiang, and B. Ran, “A two-stage optimization

\[32\] F. Eiras, M. Hawasly, S. V. Albrecht, and S. Ramamoorthy, “A two-method for schedule and trajectory of CAVs at an isolated autonomous stage optimization-based motion planner for safe urban driving,” IEEE

intersection,” IEEE Transactions on Intelligent Transportation Systems, Transactions on Robotics, vol. 38, no. 2, pp. 822–834, 2021. 

vol. 24, no. 3, pp. 3263–3281, 2023. 

\[33\] A. Slivkins et al., “Introduction to multi-armed bandits,” Foundations

\[14\] J. Huang, Z. Wu, W. Xue, D. Lin, and Y. Chen, “Non-cooperative and and Trends® in Machine Learning, vol. 12, no. 1-2, pp. 1–286, 2019. 

cooperative driving strategies at unsignalized intersections: A robust

\[34\] E. Carlsson, D. Dubhashi, and F. D. Johansson, “Thompson sampling for differential game approach,” IEEE Transactions on Intelligent Trans-bandits with clustered arms,” in Proceedings of the International Joint portation Systems, pp. 1–15, 2024. 

Conference on Artificial Intelligence. 

IJCAI, 2021, pp. 2212–2218. 

\[15\] H. Shu, T. Liu, X. Mu, and D. Cao, “Driving tasks transfer using deep

\[35\] P. Auer, N. Cesa-Bianchi, Y. Freund, and R. E. Schapire, “The non-reinforcement learning for decision-making of autonomous vehicles in stochastic multiarmed bandit problem,” SIAM Journal on Computing, unsignalized intersection,” IEEE Transactions on Vehicular Technology, vol. 32, no. 1, pp. 48–77, 2002. 

vol. 71, no. 1, pp. 41–52, 2021. 

\[36\] Analysis of the role of speeding-related fatal crashes at intersections

\[16\] Z. Qiao, J. Schneider, and J. M. Dolan, “Behavior planning at urban in-using fars data. 2016. \[Online\]. Available: https://safety.fhwa.dot.gov/

tersections through hierarchical reinforcement learning,” in Proceedings

speedmgt/ref mats/fhwasa16017/app a ch3.cfm

of the International Conference on Robotics and Automation. 

IEEE, 

\[37\] G. R. Patil and D. S. Pawar, “Microscopic analysis of traffic behavior at 2021, pp. 2667–2673. 

unsignalized intersections in developing world,” Transportation Letters, 

\[17\] Y. Liao, G. Yu, P. Chen, B. Zhou, and H. Li, “Integration of decision-vol. 8, no. 3, pp. 158–166, 2016. 

making and motion planning for autonomous driving based on double-

\[38\] J. Schulman, F. Wolski, P. Dhariwal, A. Radford, and O. Klimov, “Prox-layer reinforcement learning framework,” IEEE Transactions on Vehic-imal policy optimization algorithms,” arXiv preprint arXiv:1707.06347, ular Technology, vol. 73, no. 3, pp. 3142–3158, 2024. 

2017. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on February 23,2025 at 10:55:39 UTC from IEEE Xplore. Restrictions apply. 

© 2025 IEEE. All rights reserved, including rights for text and data mining and training of artificial intelligence and similar technologies. Personal use is permitted, but republication/redistribution requires IEEE permission. See https://www.ieee.org/publications/rights/index.html for more information. 

This article has been accepted for publication in IEEE Transactions on Vehicular Technology. This is the author's version which has not been fully edited and content may change prior to final publication. Citation information: DOI 10.1109/TVT.2025.3541401

15

\[39\] A. Dosovitskiy, G. Ros, F. Codevilla, A. Lopez, and V. Koltun, “Carla: An open urban driving simulator,” in Conference on Robot Learning. 

PMLR, 2017, pp. 1–16. 

\[40\] J. A. Andersson, J. Gillis, G. Horn, J. B. Rawlings, and M. Diehl, 

“Casadi: a software framework for nonlinear optimization and optimal control,” Mathematical Programming Computation, vol. 11, pp. 1–36, 2019. 

\[41\] Z. Peng, X. Zhou, L. Zheng, Y. Wang, and J. Ma, “Reward-driven automated curriculum learning for interaction-aware self-driving at unsignalized intersections,” arXiv preprint arXiv:2403.13674, 2024. 

Zengqi Peng received the B.Eng. degree in automation and the M.Phil. degree in artificial intelligence and automation from Huazhong University of Science and Technology, Wuhan, China, in 2019

and 2022, respectively. He is currently pursuing the Ph.D. degree in Robotics and Autonomous Systems at The Hong Kong University of Science and Technology \(Guangzhou\), Guangzhou, China. His research interests include reinforcement learning, optimization, decision-making and motion planning with applications to robotics and autonomous driving. 

Yubin Wang received the B.Eng. degree in automation from Northeastern University, Shenyang, China, in 2022, and the M.Phil. degree in Robotics and Autonomous Systems from The Hong Kong University of Science and Technology \(Guangzhou\), Guangzhou, China, in 2024. He was a visiting student at King Abdullah University of Science and Technology. His research interests include integrated learning and planning for autonomous robots. 

Lei Zheng received the B.Eng. degree in automation from Nanchang University, Nanchang, China, in 2018, and the M.Phil. degree in pattern recognition and intelligent systems from Sun Yat-sen University, Guangzhou, China, in 2021. From 2021 to 2022, he worked as a senior robotics algorithms engineer at XAG, China. He is currently pursuing the Ph.D. 

degree in Robotics and Autonomous Systems at The Hong Kong University of Science and Technology \(Guangzhou\), Guangzhou, China. His research interests include optimal control, optimization, motion planning, and nonparametric Bayesian learning with applications to robotics and autonomous driving. 

Jun Ma \(Senior Member, IEEE\) received the B.Eng. 

degree with First Class Honours in electrical and electronic engineering from Nanyang Technological University, Singapore, in 2014, and the Ph.D. degree in electrical and computer engineering from the National University of Singapore, Singapore, in 2018. From 2018 to 2021, he held several positions at the National University of Singapore; University College London, London, U.K.; University of Cali-fornia, Berkeley, Berkeley, CA, USA; and Harvard University, Cambridge, MA, USA. He is currently an Assistant Professor with the Robotics and Autonomous Systems Thrust, The Hong Kong University of Science and Technology \(Guangzhou\), Guangzhou, China, and also with the Division of Emerging Interdisciplinary Areas, The Hong Kong University of Science and Technology, Hong Kong SAR, China. 

He is also the Director of Intelligent Autonomous Driving Center, The Hong Kong University of Science and Technology \(Guangzhou\), Guangzhou, China. 

His research interests include motion planning and control for robotics and autonomous driving. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on February 23,2025 at 10:55:39 UTC from IEEE Xplore. Restrictions apply. 

© 2025 IEEE. All rights reserved, including rights for text and data mining and training of artificial intelligence and similar technologies. Personal use is permitted, but republication/redistribution requires IEEE permission. See https://www.ieee.org/publications/rights/index.html for more information. 


# Document Outline

+ Introduction 
+ Problem Statement  
	+ Problem Statement 
	+ Vehicle Model 
	+ Model Predictive Control 
	+ Learning Environment 

+ Methodology  
	+ Overview of the Proposed Framework 
	+ Exp3.S-based BiLevel Multi-Armed Bandit Algorithm for Curriculum Learning  
		+ Task Decomposition and Bilevel Curriculum Modelling 
		+ Exp3.S-based BiMAB Algorithm for Automated Curriculum Selection 

	+ High-Level PPO for Decision-Making  
		+ Observation and Action Generation 
		+ Reward Function 
		+ Training with BiM-ACPPO 

	+ Low-Level RL-Guided Model Predictive Control 

+ Experiments  
	+ Experimental Setup 
	+ Dual-Lane Unsignalized Intersections  
		+ Training Results 
		+ Performance Evaluation 

	+ Generalization Ability Into New Scenarios  
		+ Zero-Shot Generalization Ability Into Single-Lane Unsignalized Intersections 
		+ Few-Shot Generalization Ability Into Overtaking Driving Scenarios 


+ Conclusion 
+ References 
+ Biographies  
	+ Zengqi Peng 
	+ Yubin Wang 
	+ Lei Zheng 
	+ Jun Ma



