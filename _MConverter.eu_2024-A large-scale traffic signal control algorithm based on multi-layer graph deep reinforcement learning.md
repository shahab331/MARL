Transportation Research Part C 162 \(2024\) 104582

Contents lists available at ScienceDirect 

Transportation Research Part C 

journal homepage: www.elsevier.com/locate/trc 

A large-scale traffic signal control algorithm based on multi-layer 

graph deep reinforcement learning☆ 

Tao Wang a,e, Zhipeng Zhu a, Jing Zhang b,\*, Junfang Tian c,\*, Wenyi Zhang d,\* 

a *Department of Automation and Electronic Engineering, Qingdao University of Science and Technology, Qingdao 266061, China* b *Department of Mathematics and Physics, Qingdao University of Science and Technology, Qingdao 266061, China* c *College of Management and Economics, Tianjin University, Tianjin 300072, China *

d *School of Traffic and Transportation, Beijing Jiaotong University, Beijing 100044, China* e *Shandong Key Laboratory of Autonomous Landing for Deep Space Exploration, Qingdao 266061, China* A R T I C L E I N F O 

A B S T R A C T 

*Keywords: *

Due to its capability in handling complex urban intersection environments, deep reinforcement Deep reinforcement learning 

learning \(DRL\) has been widely applied in Adaptive Traffic Signal Control \(ATSC\). However, most Adaptive traffic signal control 

existing algorithms are designed for specific road networks or traffic conditions, making it Multi-layer graph structure 

difficult to transfer them to new environments. Moreover, current graph-based algorithms do not Mask-action 

Zero-training transfer 

fully capture the geometric and spatial features of intersections, leading to incomplete embedding of the agent’s environment depiction. Additionally, the actions adopted by these algorithms are inherently based on fixed-cycle phases, limiting the flexibility of traffic signal control. To address the aforementioned issues, this paper proposes a Multi-layer Graph Mask Q-Learning \(MGMQ\) algorithm for multi-intersection ATSC to optimize traffic and reduce delay. Unlike previous graph-based algorithms, this paper introduces a method for computing multi-layer graphs, dividing the traffic environment into upper-level traffic network-layer graphs and lower-level intersection-layer graphs, and employs the graph attention algorithm and an improved GraphSAGE algorithm for computation. This method not only enables the generation of embedded state for intersections that include geometric and spatial features, but also allows the algorithm to adapt to different traffic conditions and road networks. Additionally, we introduce an action masking mechanism, allowing this algorithm can be adapted to different action spaces. As a result, the algorithm uses arbitrary signal phases as actions to achieve flexible traffic flow control, and can be directly applied to intersections with arbitrary geometry. The final test results demonstrate that a model trained solely on synthetic road networks can be directly transferred to other synthetic network configurations or real-world urban road networks, outperforming current state-of-the-art algorithms. 

**1. Introduction **

With the growth of the global population and economy, the number of vehicles has been steadily rising, leading to increasingly severe traffic congestion issues \(Li et al., 2014; Zhang and Batterman, 2013\). Optimizing signal timing at signalized intersections is a 

☆ This article belongs to the Virtual Special Issue on “special issue full title”. 

\* Corresponding authors. 

*E-mail addresses: *zhangjing@qust.edu.cn \(J. Zhang\), jftian@tju.edu.cn \(J. Tian\), wyzhang@bjtu.edu.cn \(W. Zhang\). 

https://doi.org/10.1016/j.trc.2024.104582 

Received 3 August 2023; Received in revised form 16 January 2024; Accepted 19 March 2024 

Available online 29 March 2024

0968-090X/© 2024 Elsevier Ltd. All rights reserved. 

*T. Wang et *

*Transportation Research Part C 162*

*al. \(2024\) 104582*

**Nomenclature **

Variable Description 

*Rt *

The cumulative reward 

*T *

The time of state termination 

*rt *

The instantaneous reward at the current time step *t *

*Sti *

The state of the lane *i * at the time *t *

*WVNti *

The number of vehicles waiting on lane *i * at time *t *

*RVNti *

The traffic volume on the lane *i * at the time *t *

*VWTti *

The cumulative delay time of all waiting vehicles on lane *i * at time *t *

*FVTti *

The cumulative delay time of the first vehicle on lane *i * at time *t *

*Pti *

The signal phase of the lane *i * at the time *t *

*at *

The action at the time *t *

Δ *t *

The execution time of each action 

*ty *

The length of green light 

*ri *

The instantaneous reward of intersection *i *

*rp *

The signal phase of the intersection is switched or not 

*rwn *

The sum of the number of waiting vehicles on all enter lanes of the intersection 

*rpn *

The number of vehicles that have left the intersection since the last action was taken *rwt *

The sum of waiting times for all waiting vehicles on entry lanes of the intersection 

*ε *

The probability of randomly selecting an action from the action set 

*γ *

Subsequent state value attenuation coefficient 

*s *

The state at the time step *t *

*s*′ 

The state at the next time step 

*a*′ 

The action at the next time step 

*ω *

The parameters of the current *Q * network 

*ω*′ 

The parameters of the older *Q*′ network 

*σ *

The activation function, *LeakyReLU * function 

*e* 1 *ij *

The influence factor of node *j * on node *i *

*a*

→1 

The mapping function that maps the concatenated vector to a scalar 

*W* 1 

The shared weight matrix 

*α* 1 *ij *

The attention coefficient between node *i * and node *j *

N *i *

The set of neighbors of node i 

*h*

→1

*i *

The influence of all neighboring nodes on the node *i *

*K *

The number of attention heads 

*gk *

The state embedding of the intersection *k *

*gdk *

The node of the network graph 

N′ *k *

The set of neighboring nodes including node *k * itself. 

*Gk *

The embeddings of the traffic network 

*zk *

The joint embedding representation 

*θ *

All trainable parameters in the algorithm 

*N *

The total number of intersections 

key approach to alleviate traffic congestion and improve traffic efficiency, as signalized intersections serve as major bottlenecks in urban traffic. Traditional signal control methods such as fixed-time control \(Webster, 1958\), SCOOT \(Hunt et al., 1982\), and SCATS 

\(Luk, 1984\) have been widely applied in real-world road networks and have shown favorable results in intersection control. However, the effectiveness of these methods decreases with the increase in vehicle volume and traffic complexity. To respond to the limitations of traditional methods, interdisciplinary techniques such as fuzzy control \(Niittymäki and Pursula, 2000; Trabia et al., 1999\), genetic algorithms \(Ceylan and Bell, 2004; Lee et al., 2005\), and neural networks \(Saito and Fan, 2000; Srinivasan et al., 2006\) have been applied to ATSC and have achieved satisfactory outcomes. Nevertheless, these algorithms still have certain limitations. For instance, fuzzy control struggles to handle complex multi-intersection ATSC, and genetic algorithms require the manual setting of reasonable parameters. In comparison, Reinforcement Learning \(RL\) algorithms are more suitable for the ATSC field \(Liu, 2007\). 

The process of traffic signal control can be regarded as a Markov Decision Process \(MDP\). Based on this perspective, RL can be applied to ATSC without the need for a mathematical model describing the external environment. RL algorithms interact directly with the environment and learn from experience to optimize algorithm parameters. Building upon this, researchers have proposed various RL-based ATSC algorithms \(Abdulhai et al., 2003; Thorpe and Anderson, 1996; El-Tantawy and Abdulhai, 2010\) and achieved good 2

*T. Wang et *

*Transportation Research Part C 162*

*al. \(2024\) 104582*

control results. However, RL algorithms are limited in handling complex and continuous state problems \(Arulkumaran et al., 2017, 

Mousavi et al., 2018\). By leveraging deep neural networks, Deep Reinforcement Learning \(DRL\) algorithms can effectively address this issue \(Mnih et al., 2015\). Researchers have developed various DRL-based ATSC algorithms, applied to both single-intersection ATSC 

scenarios and multi-intersection ATSC scenarios. Multi-intersection ATSC algorithms can be primarily classified into two types: the first type is centralized control, where all intersections share one agent and utilize a combined state and action space \(Casas, 2017; 

Prashanth and Bhatnagar, 2011\). This approach is computationally challenging and difficult to scale. The second type is decentralized control \(Li et al., 2021a; Wu et al., 2020; Wiering, 2000\), where each intersection has its own agent. This approach is widely adopted in current research due to its strong scalability \(Chu et al., 2019; Wang et al., 2021b\). 

The transferability of a model holds significant importance for its practical application, and thus, numerous researchers have dedicated substantial efforts in this realm. Approaches such as \(Norouzi et al., 2021; Van der Pol and Oliehoek, 2016; Zhang et al., 

2023\) have introduced transfer learning techniques. By training models on diverse source data, they enable the models to specialize as domain-specific experts, guiding the training of new models to facilitate their rapid adaptation to new environments. Techniques such as \(Mao et al., 2022; Ge et al., 2021\) have achieved favorable results in arterial and regional signal control by incorporating attention mechanisms and the soft actor-critic algorithm. Additionally, \(Zang et al., 2020\) leverage *meta*-reinforcement learning methods to expedite the model’s adaptation to new traffic scenarios. In recent years, significant progress has been made in the field of Graph Neural Networks \(GNN\) with the emergence of various algorithms such as Graph Convolutional Networks \(GCN\)\(Kipf and Welling, 

2016\) , Graph Attention Networks \(GAT\) \(Veličković et al., 2018\), and GraphSAGE \(Hamilton et al., 2017\). These algorithms have demonstrated their capability to capture dynamic traffic flow characteristics and spatial structural features of traffic networks. 

Capitalizing on these capabilities, some researchers have integrated GNN with DRL and applied them to ATSC \(Devailly et al., 2021, 

Yoon et al., 2021, Wang et al., 2022, Wei et al., 2019\), achieving promising results in terms of model transferability and scalability. 

However, most existing DRL-based ATSC algorithms are designed for specific traffic networks or specific traffic states, making it challenging to transfer them to new road scenarios or scale them up to larger road networks. While integrating GNN algorithms with DRL allows for transferability to new environments, these algorithms often neglect the geometric and spatial features of intersections, leading to incomplete environmental embedding representations for the agents. Additionally, due to the fixed dimensionality of the output in DRL, most DRL-based ATSC algorithms typically employ actions such as transitioning to the next phase or setting green time, which essentially relies on cyclic phase changes. This limitation restricts the flexibility of action selection in DRL and hinders the realization of optimal real-time control of traffic flow in ATSC algorithms. 

In order to address these issues, this paper proposes a multi-layer graph masking Q-Learning \(MGMQ\) algorithm based on decentralized multi-agent DRL, which is applicable to ATSC. The algorithm designs a computation method using multi-layer graphs, dividing the traffic environment into lower-layer intersection graphs and upper-layer traffic network graphs. The intersection graphs consist of individual intersections, where lanes are treated as nodes and the relationships between lanes are regarded as edges. The traffic network graphs encompass the entire traffic network, where individual intersections are divided into multiple nodes and the links between intersections are considered as edges. For the intersection graphs, the GAT algorithm, combined with a multi-head attention mechanism, is employed to learn the embedding of nodes. For the traffic network graphs, the initial node vector is calculated by using the embedding of the intersection graphs, and an improved GraphSAGE algorithm is proposed to learn the embedding of nodes in the transportation network graphs. Finally, the embedding of the intersection graphs and traffic network graphs is connected and input into DQN, calculating the Q value of each action and selecting the optimal action. Due to the varying configurations of intersections, such as T-intersections and crossroads, the size of the signal phase space differs. To accommodate different sizes of signal phase spaces, an action masking mechanism \(Zahavy et al., 2018; Huang and Onta˜nón, 2020\) is introduced, making the actions in this algorithm can be any signal phase. This enables the optimal real-time control of traffic flow during traffic signal timing and facilitates the application of the algorithm to intersections with different phase spaces. Furthermore, a parameter-sharing mechanism is implemented among all intersection agents, reducing the number of model training parameters and enabling the model to be transferred to new road networks without additional training \(zero-shot learning\). To explore the transferability and scalability of the algorithm, the proposed algorithm is tested on a synthetic road network as well as real road networks in Jinan and Qingdao. The main contributions of this paper are as follows: 

\(1\) A multi-layer graph mask Q-Learning \(MGMQ\) algorithm is proposed for ATSC based on decentralized multi-agent DRL. The algorithm generates state representation embeddings for intersections that contain both geometric and spatial features resulting in more complete environmental embedding representations for agents. 

\(2\) By introducing the action masking mechanism, allowing this algorithm can be adapted to different action spaces. The algorithm uses arbitrary signal phases as actions, realization of optimal real-time regulation of traffic flow direction during traffic signal timing. 

Furthermore, it facilitates the seamless application of the algorithm to intersections with diverse configurations. 

\(3\) The proposed algorithm demonstrates strong generalization ability and scalability, as the model trained on a synthetic road network can be directly applied to synthetic or real-world urban road networks without additional training. 

The upcoming sections of this paper are organized as follows: Section 2 provides an overview of related work in the field of reinforcement learning-based traffic signal control. Section 3 details the basic settings of intersections and the relevant definitions in reinforcement learning adopted in this paper. Section 4 presents the structure and computational process of the proposed MGMQ 

algorithm. Section 5 offers experimental results from various aspects to assess and analyze the performance of the proposed method. 

Finally, Section 6 concludes the paper and outlines potential future research directions. 

3

*T. Wang et *

*Transportation Research Part C 162*

*al. \(2024\) 104582*

**2. Related work **

The process of traffic signal control can be regarded as a Markov decision process, where RL algorithms based on this process do not require a mathematical model of the external environment. Instead, RL algorithms interact directly with the environment and learn from experience to optimize algorithm parameters. Therefore, RL algorithms are suitable for complex traffic signal control environments and have experienced rapid development in the field of ATSC. Existing research efforts primarily focus on RL-based ATSC, DRL-based ATSC, and DRL-based ATSC combining GNN. 

The SARSA algorithm was first applied in traffic signal control as an RL method \(Thorpe and Anderson, 1996\). It is a temporal difference-based reinforcement learning algorithm used for traffic signal control at individual intersections, and it has shown better performance than some traditional algorithms. Following that, researchers have proposed various RL-based traffic signal control algorithms, such as improved SARSA algorithm and Q-learning algorithm \(Abdulhai et al., 2003; El-Tantawy and Abdulhai, 2010\). These algorithms have achieved promising results in reducing vehicle delay and mitigating traffic congestion. 

Unfortunately, although RL-based ATSC algorithms have achieved promising results, the limitations of RL algorithms in handling complex and continuous state spaces \(Arulkumaran et al., 2017, Mousavi et al., 2018\) have restricted the performance of ATSC algorithms. With the development of deep neural networks, DeepMind proposed the Deep Q Network \(DQN\) algorithm, which addressed the issue of RL’s inability to handle complex and continuous states \(Mnih et al., 2015\). Researchers began applying DRL to ATSC and achieved good control effects in more complex intersection environments. Based on different application scenarios, DRL-based ATSC 

algorithms can be divided into single-intersection ATSC algorithms and regional multi-intersection ATSC algorithms. For single-intersection ATSC algorithms, they mainly adopt value-based DQN algorithms and policy-based Deep Deterministic Policy Gradient \(DDPG\) or Proximal Policy Optimization \(PPO\) algorithms \(Fang et al., 2019; Li et al., 2021b; Pang and Gao, 2019; Wei et al., 2018\). 

These DRL-based algorithms have shown superior performance over RL algorithms in reducing vehicle delay and alleviating traffic congestion. Regarding regional multi-intersection ATSC algorithms, they can be categorized into centralized single-agent DRL algorithms and decentralized multi-agent DRL algorithms based on the different approaches to agent configuration. The centralized single-agent DRL algorithms refer to using a single agent shared by all intersections, which makes this type of algorithm difficult to scale massively due to the use of combined state action spaces in this approach \(Casas, 2017\). On the other hand, the decentralized multi-agent DRL algorithms, in which each intersection has an independent agent, exhibit strong scalability and have become the main research direction in ATSC. Based on the communication between agents, the decentralized multi-agent DRL algorithms for ATSC can be classified into three types. The first type is non-communicative among agents \(Wiering, 2000\), which offers strong scalability but cannot achieve global optimization compared to algorithms with communication among agents. The second type is global communication, where each agent communicates with all other agents \(Li et al., 2021a; Wu et al., 2020\). This type allows individual agents to obtain global state information, make the optimal action selection, and optimize the entire transportation network. However, this approach requires communication among all agents, resulting in a significant communication burden. The third type is local communication \(Chu et al., 2019; Wang et al., 2021a\), where each agent communicates only with neighboring agents. With a reduced communication burden, this approach allows agents to obtain the state of adjacent intersections, leading to a more reasonable action selection. 

In the past, ATSC algorithms have typically employed convolutional neural networks and similar approaches to capture the spatial features of traffic networks \(Wu et al., 2020\). However, these algorithms are generally designed for Euclidean spatial data and may not be suitable for the complex topological structures of urban road networks \(Zhao et al., 2019; Yang et al., 2021\). In recent years, graph-based neural networks have rapidly evolved. Graphs consist of nodes and edges, where each data sample \(node\) is connected by edges to other data samples \(nodes\), capturing the dependencies between data samples. Therefore, graph neural networks based on graph structures can aggregate non-Euclidean spatial data effectively \(Zhou et al., 2020\). Various algorithms such as Graph Convolutional Networks \(GCNs\) \(Kipf and Welling, 2016\), Graph Attention Network \(GAT\) \(Veličković et al., 2018\), and GraphSAGE \(Hamilton et al., 

2017\) have been developed. Research has demonstrated that, owing to the capability of GNNs to capture dynamic traffic flow characteristics and the spatial structural features of traffic networks, modeling traffic networks as graphs is more effective in extracting information from adjacent nodes compared to aggregating locations within the network using convolutional networks \(Nishi et al., 

2018; Peng et al., 2021\). Many researchers have applied GNNs in the field of adaptive traffic signal control by integrating them with DRL to enable agents to obtain a more comprehensive embedded state representation. For instance, some studies treat intersections as nodes and utilize algorithms like GCN and GAT to extract influence information between adjacent intersections \(Wei et al., 2019, Ma 

et al., 2023\), facilitating cooperation among intersection agents. Others regard lanes as nodes and employ GNN algorithms to extract mutual influence information between different lanes within the same intersection \(Yoon et al., 2021\), aiming to enhance the algorithm’s adaptability to varying levels of traffic flow. Additionally, some works utilize a multi-layer graph approach, treating vehicles, lanes, connections between lanes, and traffic signals as nodes, allocating them to different graph layers \(Devailly et al., 2021\). This design allows the model to be transferred to new networks without requiring retraining. However, although this algorithm constructs a multi-layer graph structure, the same GCN algorithm is used for node aggregation, making it unable to extract the characteristics of different types of nodes. Some studies adopt a heterogeneous graph construction approach \(Yang, 2023; Yang et al., 2021; Yang and 

Yang, 2022\), employing different aggregation algorithms across layers to comprehensively extract environmental features for intersection agents. However, their action settings are based on cyclic phases, limiting their ability to promptly and flexibly control traffic flow. 

In contrast to prior works, this paper introduces a computation method using multi-layer graphs, dividing the traffic environment into lower-layer intersection graphs and upper-layer traffic network graphs. In the intersection graphs, the GAT algorithm is employed to aggregate lane information within each intersection. On the other hand, in the traffic network graphs, an improved version of the 4



*T. Wang et *

*Transportation Research Part C 162*

*al. \(2024\) 104582*

GraphSAGE algorithm is utilized to aggregate information from neighboring intersections, ensuring the comprehensive extraction of environmental information for intersection agents. Additionally, this paper configures the algorithm’s actions as arbitrary signal phases, allowing for more flexible traffic flow control. The introduction of an action masking mechanism enables the algorithm to adapt to intersection spaces with different signal phases, enabling the algorithm to adapt to intersections with different signal phase spaces. 

**3. Problem definition **

This section introduces the relevant definitions of standard intersections and the setting of the RL environment. 

*3.1. Definitions of standard intersections *

A large city transportation network is connected by multiple independent standard intersections. The shape and signal light phases of a single intersection are as follows: 

**Shape of Intersection: **As shown in Fig. 1, a standard cross intersection consists of four edges from different directions, named N, E, S, and W according to their orientation. Each direction has three entrance lanes, including one left turn lane, one right turn lane, and one straight lane. For T-junction, it can be considered as a cross intersection with some lanes removed. 

**Traffic Signal Phases**: A traffic signal phase combination consisting of four phases has been developed based on the vehicle’s movement route. Table 1 shows the phase and lanes allowed to pass. In Fig. 1, the phase combination is also represented by lane colors, with the same color indicating the same phase. Since vehicles on right-turn lanes do not affect vehicles on other lanes, the default right-turn lane is always green. 

*3.2. Reinforcement learning environment *

We define traffic signal control as a Markov decision process \(MDP\). Generally, an MDP consists of a state space *S*, an action space *A*, rewards *r*, state transition probabilities *P*, and a discount factor *γ*. The agent selects actions based on the observed states, receives rewards while changing the environment, and optimizes the policy through iterative training to maximize the cumulative reward *Rt*, as shown in the following equation: 

∑

*T*

*Rt *=

*γτ*− *trτ*

\(1\) 

*τ*= *t*

Wherein, *T * denotes the time of state termination, and *rt * represents the instantaneous reward at the current time step *t*. 

**State:**In this study, to better represent the actual situation of the current intersection, we consider multiple traffic features as the state representation for a single lane. Considering the ease of obtaining these traffic features, we ultimately select five features to represent the current lane’s state. These features include the number of vehicles waiting in the lane, the traffic volume of the lane, the total cumulative waiting time of vehicles in the lane, the cumulative waiting time of the first vehicle in the lane, and the current phase of the lane. The number of vehicles waiting on lane *i * at time *t * is denoted by *WVNti*. The traffic volume on the lane *i * at the time *t*, **Fig. 1. **Standard intersection. 

5

*T. Wang et *

*Transportation Research Part C 162*

*al. \(2024\) 104582*

**Table 1 **

Signal phase combination. 

Phase 

Lane 

A 

2, 8 

B 

5, 11 

C 

3, 9 

D 

6, 12 

represented by *RVNti*, includes both stationary and moving vehicles on the lane. The cumulative delay time of all waiting vehicles on lane *i * at time *t * is denoted by *VWTti*. The cumulative delay time of the first vehicle on lane *i * at time *t * is represented by *FVTti*. The signal phase of the lane *i * at the time *t * is indicated by *Pti*, consisting of two values 0, 1, where 0 represents a red light indicating no passage and 1 represents a green light indicating passage. Finally, the state of the lane *i * at the time *t * is denoted by *Sti*, the expressions as follows: \(

\)

*St *= *WVNt, RVNt, VWTt, FVTt, Pt*

\(2\) 

*i*

*i*

*i*

*i*

*i*

*i*

**Action: **In this paper, the action space A is defined as all feasible signal phases. At time t, action a *t * is any feasible signal phase. The execution time of each action is fixed to Δ *t*. If the next action is not the same as the current signal phase, a *ty * yellow light is added before the new action is executed, which allows the vehicles that have already entered the intersection to pass safely. A recent work \(Aslani 

et al., 2017; Wang et al., 2022\) proposes Δ *t *= 10 *s*, *ty *= 5 *s*, we fix Δ *t *= 10 s, *ty *= 3 *s * in this paper. 

**Reward: **To make the agent learn how to make reasonable actions faster and better, it is necessary to choose appropriate features as rewards. In this paper, in order to represent the actual feedback of the intersection more reasonably, considering the difficulty of feature acquisition, multiple rewards are defined. Similar to Wu’s work \(Wu et al., 2020\), we define *rp * as whether the signal phase of the intersection is switched or not. The formula is as follows: 

\{ 1 *,if a*

*r*

*t *= *at*− 1

*p *=

\(3\) 

− 1 *, if at *∕

= *at*− 1

Our choice of this feature is to prevent frequent phase switching, which may cause vehicles to frequently start and stop, resulting in a decrease in the traffic efficiency at the intersection, and may also lead to traffic accidents. We use *rwn * to represent the sum of the number of waiting vehicles on all enter lanes of the intersection, as shown below: 

∑

*rwn *=

*rl*

\(4\) 

*wn*

*l*∈ *Li*

Here, *Li * represents the set of all entry lanes of the intersection *i*, *rlwn * represents the number of vehicles with zero speed on the lane *l*. 

Using *rwt * to represent the sum of waiting times for all waiting vehicles on entry lanes of the intersection, as shown below: 

∑∑

*rwt *=

*rv*

\(5\) 

*wt*

*l*∈ *Li v*∈ *Vl*

Here, *Li * represents the set of all entry lanes at intersection *i*, *Vl * represents the set of vehicles with zero speed on lane *l*, *rvwt * represents the cumulative waiting time of vehicle *v*. Using *rpn * to represent the number of vehicles that have left the intersection since the last action was taken, as shown below: 

∑

*rpn *=

*rl*

\(6\) 

*pn*

*l*∈ *Li*

Where, *Li * represents the set of all entry lanes at the intersection *i*, *rlpn * represents the number of vehicles leaving the lane *l * since the last action was taken. To balance the weight of each reward, the reward *r * is calculated as a weighted sum, as follows: *ri *= *rp *− *rwn *\+ *rp* n − *rwt/k*

\(7\) 

Due to the magnitude of the waiting time being greater than that of other rewards, for the purpose of balancing waiting time with other reward values, we rescale it. Following the literature \(Chu et al., 2019, Tan et al., 2019\) and considering the 10 s action interval we employ, we set k = 10. For the other rewards, we have not reduced or enlarged them because their values are close to the comparisons. 

This paper employs the Double DQN \(DDQN\) algorithm, which is an improvement on the DQN. The DQN selects actions by calculating the Q values of state-action pairs using a Q network. The formula is shown below: *Q*\( *s, a, ω*\) = *Qπ*\( *s, a*\)

\(8\) 

We use *ε *− *greedy * policy to select actions, which means selecting the action with the highest Q-value with probability 1 − *ε*, and selecting a random action from the action set with probability *ε*. 

DQN uses two *Q*-networks, one is the current *Q*-network and the other is the Older *Q*′ network. The current *Q*-network is used to calculate the *Q*-value and select the action, the Older *Q*′ network is used to update the current *Q*-network by computing the *Q*′ value. 

The loss function is defined as follows: 

6



*T. Wang et *

*Transportation Research Part C 162*

*al. \(2024\) 104582*

\[

\]

*L*\( *θ*\) = *E *\( *y*

\(9\) 

*i *−

*Q*\( *s, a, ω*\) \)2

\(

\)

*yi *= *ri *\+ *γ* max *Q*′ *s*′ *, a*′ *, w*′

\(10\) 

*i*

*i*

*a*′

where, *s*′ is the state at the next time step, and *a*′ is the action at the next time step. 

Double DQN is similar to DQN in that both have two *Q*-networks \(Van Hasselt et al., 2016\). In the DDQN algorithm, the action *a*′ in the formula \(10\) is not calculated by the older *Q*′ network, but is obtained by selecting the action with the maximum *Q * value in the current *Q * network, as shown in the formula \(11\). 

\(

\)

\(

\)

*a* max *s*′ *, ω *= max *Q s*′ *, a*′ *, ω*

\(11\) 

*i*

*i*

*a*′

Then the action selected by the formula \(11\) is introduced into the formula \(12\), i.e. 

\(

\(

\)

\)

*yi *= *ri *\+ *γQ*′ *s*′ *, a* max *s*′ *, w , ω*′

\(12\) 

*i*

*i*

The loss is calculated according to the loss function \(9\) to update the parameters of the current *Q * network. The parameters of the older *Q*′ network are copied from the current *Q * network at regular intervals. 

Decentralized reinforcement learning \(Dec-RL\) is an approach to control, based on the idea that the global Q function can be broken down \(Busoniu et al., 2006\). IQL \(Independent Q-learning\) is a processing algorithm of Dec-RL \(Devailly et al., 2021\), where the global MDP is divided into decentralized MDPs, and each is solved by a single Q Network. 

**4. Model **

*4.1. Overall framework *

This study proposes the MGMQ algorithm based on DQL, and the overall framework is illustrated in Fig. 2. We represent the traffic network as a two-layer graph structure comprising the intersection layer and the traffic network layer. Initially, we employ GAT for embedding representation learning on the intersection layer, generating intersection embedding vectors for individual intersections. 

Subsequently, the improved GraphSAGE algorithm is applied to learn representations on the traffic network layer, producing network embedding vectors that incorporate neighboring features. Finally, the two embedding vectors are concatenated to form a joint embedding vector. This joint embedding vector is then input into the DQN network to compute Q-values for various actions, facilitating the selection of the optimal action. 

*4.2. Intersection embedding *

The purpose of setting the intersection layer is to extract information from individual intersections, aggregating information from different lanes within the same intersection. Different lanes within the same intersection influence each other, and this mutual influence changes over time. Therefore, we consider using the GAT algorithm to extract the influence information between them. We first transform the intersection into a graph structure, and then a GAT can extract information about the influence between connected nodes. It can aggregate information from adjacent nodes based on the calculated weights. Hence, we use the GAT algorithm as the **Fig. 2. **MGMQ Structure Diagram. 

7



*T. Wang et *

*Transportation Research Part C 162*

*al. \(2024\) 104582*

aggregation algorithm for the intersection layer. This approach allows the model to extract internal structural information from intersections and adapt to different traffic flow conditions. 

Expressed as a graphical data structure *G*\( *t*\), as shown in Fig. 3, the intersection is composed of nodes *N * and edges *E*. The entry lanes of the intersection are regarded as nodes *Vt*, according to the state defined by Equation \(2\), *V*\( *t*\) = \{ *St* 1⋯ *StN*\}, where *N * is the number of lanes. The color classification of the nodes in the figure represents the phase grouping of the lanes, with the same color representing the same group. As mentioned earlier, the right-turning lane can always be considered a green light, so it can be regarded as the same group as any other node. 

Considering the viewpoint of reference \(Yoon et al., 2021\), we define the connections between lanes as edges *E*, which can be divided into two categories based on the phase relationship between the lanes. One category is for two lanes in the same signal group, denoted as *E* 1. The other is for two lanes not in the same signal group, denoted as *E* 2. As shown in Fig. 3, due to the complexity of node connections, only the node for lane 3 is used as an example. The green edges represent two lanes in the same signal group, and the red edges represent those not in the same signal group. 

We divide *G*\( *t*\) into two subgraphs, *g* 1\( *t*\) and *g* 2\( *t*\), according to the type of edges. One subgraph *g* 1\( *t*\) is composed of nodes *Vt * and edges *E* 1, and the other subgraph *g* 2\( *t*\) is composed of nodes *Vt * and edges *E* 2. 

We use the GAT algorithms to aggregate the nodes of the intersection graphs, using a multi-head attention mechanism. First, we use a fully connected layer to process the node state *Si*, as follows: 

*hi *= *σ*\( *Dense*\( *Si*\)\)

\(13\) 

In the equation, *Dense * represents a fully connected layer, *σ * is the activation function, and the *LeakyReLU * function is used, which is an improvement over *Relu * and has a negative slope coefficient of 0.05. 

The following will perform calculations on the graph *g* 1\( *t*\). 

\(

\[

\] \)

→

→

*e* 1 = *σ a*

→1 *T W* 1 *h*

\(14\) 

*ij*

*i*‖ *W * 1 *h j*

\( \)

\( \) ∑

\( \)

*α* 1 = *soft* max *e* 1 = exp *e* 1 */*

exp *e* 1

\(15\) 

*ij*

*ij*

*ij*

*ij*

*j*∈N *i*

→1

1 ∑

*K*

∑

*h *=

*α* 1 *kW* 1 *kh*

*i*

*K*

*ij*

*j*

\(16\) 

*k*=1 *j*∈N *i*

**Fig. 3. **Intersection graph representation. 

8



*T. Wang et *

*Transportation Research Part C 162*

*al. \(2024\) 104582*

We calculate the influence factor of node *j * on node *i * through equation \(14\), where *W* 1 is the shared weight matrix, *W* 1 ∈ R *F*′\* *F*, and *a*

→1 is the mapping function that maps the concatenated vector to a scalar, *a*→1 ∈ R2 *F*′\*1, *T * represents transpose. The attention coefficient *αij * between node *i * and node *j * is calculated by equation \(15\) using the mask attention mechanism, which only calculates the nodes connected to node *i*, where N *i * is the set of neighbors of node *i*. Finally, the equation \(16\) is used to aggregate the influence of all neighboring nodes on the node *i * through weighted summation. *K * is the number of attention heads, and the aggregation is performed by taking the average. The calculated *h*

→1

*i * represents the influence of neighbors in the same signal group on node *i*. 

Using the same approach, we process *g* 2\( *t*\) and compute *h*→2 *i*, which represents the influence of neighbors in different signal groups on the node *i*. 

Then the node information is updated as follows: 

\(

\)

→1 →2

*h*′ = *f h*

*, h *; *ψ*

\(17\) 

*i*

*i, h i*

*i*

Here, *f * represents the node update function and *ψ * represents the parameters. 

**Fig. 4. **Traffic network graph representation. 

9



*T. Wang et *

*Transportation Research Part C 162*

*al. \(2024\) 104582*

Finally, all nodes of a single intersection are connected to form the state embedding g *k * of the intersection *k*, as shown in the following equation: 

\(

\)

g = connect *h*′ *, h*′ *, ..., h*′

\(18\) 

*k*

1

2

*N*

connect represents vector concatenation operation. 

*4.3. Network embedding *

We similarly model the traffic network as graph-structured data. Considering that the nodes formed by intersections possess location-specific attributes, it is imperative to account for the location information of intersections when creating the graph and aggregating information from neighboring intersections. Consequently, in the construction of the graph, we comprehensively incorporate the positional characteristics of intersections, with specific details elaborated in subsequent sections. In order to extract influence information between adjacent intersections, we chose the GraspSAGE algorithm. However, the traditional GraspSAGE 

algorithm does not have the capability to extract location features. Therefore, we have made modifications to the original algorithm to include position information in the influence information between neighboring intersections and the local intersection. We adapted the original aggregation layer to a bidirectional GRU \(Bi\_GRU\), which is capable of capturing relationships between preceding and succeeding inputs, making it particularly suitable for extracting position information. This enables the model to facilitate effective communication between intersection agents and also allows the model to adapt to traffic networks of different sizes. 

Based on the structure of the traffic road network, we created graph-structured data for the traffic network layer. The nodes in the graph consist of exit lane nodes and current intersection nodes. As exit lanes have directionality, we have defined four types of exit lane nodes based on their direction. The node vector is calculated from the current intersection state embedding *gk * using five different functions, as shown below: 

\(

\)

*gd *= *σ Densed*\( *g*

\(19\) 

*k*

*k *\)

*Dense * represents a fully connected layer, *d *∈ \{ *N, E, S, W, Self*\} represents the direction of exit lanes of the current intersection *k * and the intersection *k * itself, *σ * is the activation function. 

As shown in Fig. 4, taking the middle intersection *k * as an example, the red node represents the current intersection node *gSelf* *k *, and 

the green, gold, blue, and purple nodes represent the four exit lane nodes *gNk*, *gEk*, *gSk*, *gWk * respectively. Other intersections are represented using the same color-coding rule. 

The exit lane nodes contain information regarding the influence on adjacent intersections. To acquire the influence information of adjacent intersections on the local intersection, we establish edges connecting the exit lane nodes of neighboring intersections with the current lane nodes of the local intersection. As the exit lanes of adjacent intersections correspond to the entry lanes of the current intersection, we define four types of edges based on the direction of the entering lanes of the current intersection. These four types of edges are represented with different colors in Fig. 5. 

**Fig. 5. **Bi-GRU structure diagram. 

10

*T. Wang et *

*Transportation Research Part C 162*

*al. \(2024\) 104582*

We then proceed to compute the graph. First, we perform neighbor node sampling. Unlike the general GraphSAGE sampling method, we only collect neighbor nodes for the *gSelf * node. We take into consideration that if there are two or more adjacent intersections that flow into the local intersection, sharing an entering lane, this can result in the existence of two or more edges of the same type. Because choosing only one is sufficient to represent the impact of neighboring intersections in that direction, selecting multiple ones would lead to confusion instead. If the connected node of a certain type of edge does not exist, it is replaced by a vector approaching zero. The collected neighbor nodes are placed into a neighbor node set N *k*. We then perform aggregation on the neighbor nodes. To fully utilize the positional information, we improve the aggregation layer using the Bi-GRU algorithm, as shown in the following equation: 

\(̅̅̅→\( \) ←̅̅̅\( \) \)

*Gk *= *Connect GRU gd *‖ *GRU gd*

\(20\) 

*k*′

*k*′

In the equation, *k*′ ∈ N′ *k*, where N′ *k * represents the set of neighboring nodes including node *k * itself. The output of Bi-GRU is concatenated together and *Gk * represents the total influence of neighboring intersections on the current intersection *k*. *GRU*

̅̅→ represents 

forward *GRU*, *GRU*

←̅̅ represents reverse *GRU * calculation, ‖ represents connection operation, *Connect * represents connecting the outputs of all Bi-GRUs. The calculation process of Bi-GRU is shown in Fig. 5, and a GRU’s calculation formula is as follows: *rk *= *σ*\( *wrXk *\+ *Urhk*− 1\)

\(21\) 

*zk *= *σ*\( *wzXk *\+ *Uzhk*− 1\)

\(22\) 

*hk *= *zk *⊙ ̃ *hk *\+ \(1 − *zk*\) ⊙ *hk*− 1

\(23\) 

̃

*hk *= tanh\( *w*˜ *X*

\( *r*

*h*

*k *\+ *U*˜

*h*

*k *⊙ *hk*− 1 \)\)

\(24\) 

Where *Xk * is the input vector, *hk * is the output hidden state, ̃ *hk * is the new memory cell, ⊙ indicates Hadamard product, *w * and *U * are learnable parameters, *rk * and *zk * are reset gate vector and update gate vector of the Kth feature, respectively. 

Finally, we concatenate the embeddings of the intersection graph *gk * and the traffic network graph *Gk * to form the final embedding representation *zk * of the intersection, as shown in the following formula: 

*zk *= *Connect*\( *gk, Gk*\)

\(25\) 

*Connect * represents vector connections. 

*4.4. Q-network *

By the previous computations, we obtain the final state representation *zk * of the intersection. Our Q-Network consists of two fully connected layers, as shown in the following equation: 

*Q*′ = *σ*\( *Dense*\( *zk*\)\)

\(26\) 

*Q *= *Dense*\( *Q*′\)

*Dense * represents a fully connected layer, *σ * is the activation function, and the *LeakyReLU * function is used. According to the loss function described in Equation \(9\), the loss function of this paper is as follows: 

∑

*N*

*L*\( *θ*\) =

*E*\[\( *yi *− *Q*\( *si, ai*; *θ*\) \) \]

\(27\) 

*i*=1

\(

\)

\(

\)

*yi *= *ri *\+ *γQ*′ *s*′ *, * argmax *Q s*′ *, a*′; *θ , θ*′

\(28\) 

*i*

*i*

*a*′

Where *N * represents the total number of intersections and *θ * represents all trainable parameters in the algorithm. We summarize the training process of the MGMQ algorithm in Algorithm 1. 

**Algorithm 1: **MGMQ for traffic signal control 

**Input: **replay memory size *M*, minibatch size *B*, current network update rate *α*, target network update rate *β*, discount factor *γ*, greedy ∊, current network parameters *θ*, older network parameters *θ*′. 

**Output: **Optimized parameters *θ * in MGMQ 

**Initialize: **total step *s κ *= 0 *, * replay memory buffer *Dmemory *= ∅ 

**for **training episode = 1→ *N ***do **

Initialize the environment 

\( *continued on next page*\) 

11



*T. Wang et *

*Transportation Research Part C 162*

*al. \(2024\) 104582*

\( *continued*\) 

**Algorithm 1: **MGMQ for traffic signal control 

**for ** *t *= 1 *, * 2 *, *⋯ *, T ***do **

Get State *St * and choose *At * according to the *γ * greedy. 

Execute action *At * in the environment. 

Get next step State *St*\+1 and the reward *rt. *

**if ** *m > M ***then **// *m*: the size of *Dmemory *

Remove the oldest experiences in the *Dmemory*. 

**end if **

store \{ *St, At, rt, St*\+1\} into *D memory*, *κ *= *κ *\+ 1 

**If ** *κ*% *α *= 0 and *m > B ***then **

Randomly sample a minibatch of size *B * from *Dmemory*. 

calculate loss **L **\( *θ*\) in Equation \(23\) with *γ*. 

update *θ * by Adam algorithm with *α*. 

**end if **

**If ** *κ*% *β *= 0 **then **

update *θ*′ by copying *θ*. 

**end if **

**end for **

**end for **

*4.5. Action mask *

Due to the different shapes of cross intersections and T intersections, the dimension of the signal phase combination space is different. The cross intersection has four phase combinations, while the T intersection has three phase combinations. In this paper, the size of the action space for the agent is set to four based on the cross intersection. Therefore, for the T intersection, we use a mask operation on the output action values to change the output action values. For the Q values of unreasonable actions, they are set to negative infinity, so that the agent will not choose these actions. The equation is as follows: **Fig. 6. **Methodology framework. 

12



*T. Wang et *

*Transportation Research Part C 162*

*al. \(2024\) 104582*

*Q*\( *s, ai*; *θ*\) = − ∞ *, if * a *inotin * A *j*

\(29\) 

where *Aj * is the phase space of intersection *j*. Similarly, when calculating the loss, we also made modifications. When selecting action *a*′ in the formula \(28\), according to formula \(29\), we replaced the Q value of the unreasonable action with an infinite decimal. 

*4.6. Overview of MGMQ algorithm *

In the preceding sections, we systematically introduced the MGMQ algorithm proposed in this paper. In this section, we provide an overview of the algorithm, as illustrated in Fig. 6. 

We categorize the traffic environment into two layers: the intersection layer and the traffic network layer, as shown on the left side 

of Fig. 6. In Section 4.2, intersections are modeled as graph-structured data, and the state representation of individual intersections is learned using the graph attention mechanism. Subsequently, in Section 4.3, the state embedding vectors of individual intersections are processed to form node vectors in the traffic network layer. An improved GraphSAGE algorithm is employed for aggregating neighboring nodes, consolidating the influence information from adjacent intersections to the local intersection. Finally, in Section 4.4, a Q-network is constructed through two fully connected layers. The embedding vector of the local intersection is connected to the embedding vector containing the influence information from neighboring intersections and used as input. The Q-values for various actions are then outputted. In Section 4.5, utilizing the action masking mechanism employed in this study, the Q-values of actions are further processed to select appropriate phases for traffic signal lights. 

*4.7. Parameter sharing *

Our proposed algorithm is designed for large-scale traffic networks, which have a large number of intersections that require numerous agents to control traffic signals. If each agent has its independent parameters, the number of required parameters will be significantly increased, and the model will be difficult to transfer to a new network. Therefore, we adopt a parameter-sharing method, i.e., the model parameters used by each agent are the same. 

Parameter sharing reduces the number of training parameters of the model, lowers the computational requirements of the training process, and improves the model’s transferability and scalability. It provides a foundation for directly transferring the model to new networks. 

*4.8. T-intersection Setting *

In the previous sections, we used an intersection as an example to analyze and compute the traffic signal control. However, the shape and number of lanes at a T-intersection are different from those at an intersection. We mentioned earlier that a T-intersection can be viewed as an intersection with some lanes missing. Therefore, when calculating the T-intersection, we add missing lanes to expand it into an intersection, and the observation *S * of the added lanes is the state where there are no cars on normal lanes. 

**Fig. 7. **Synthetic road network\(a\) and the shape of a crossroads and a T-junction \(b\)\(c\). 

13



*T. Wang et *

*Transportation Research Part C 162*

*al. \(2024\) 104582*

**5. Experiment **

We trained and tested our algorithm on Simulation of Urban Mobility \(SUMO\), which provides a Python interface and rich functionality for real-time traffic status acquisition and traffic signal control. Our algorithm was trained on a small synthetic road network and tested on one synthetic road network and two real urban road networks. 

*5.1. General settings *

In this section, we will introduce some general settings for training and testing the algorithm. 

*5.1.1. Synthetic road network settings *

We set up a synthetic road network containing 45 intersections, as shown in Fig. 7\(a\), which includes 25 crossroads and 20 T-junctions. In this road network, each intersection is a standard intersection as described earlier, and the shapes of the crossroad and T-junction are shown in Fig. 7\(b\) and Fig. 7\(c\), respectively. The phase space defined in the previous section is used to define the signal phase combinations for each intersection, and there is a 3-second yellow light time after each phase switch. 

In order to simulate a real urban environment, we set the vehicles to generate at any point in the traffic network and move along a randomly generated route. To reflect different real-world scenarios, we set three different vehicle generation rates: one is the normal traffic flow with a rate of 3.33 vehicles/s, the other is the moderate traffic flow with a rate of 5 vehicles/s, and the last with a heavy traffic flow rate of 7 vehicles/s. The vehicle generation time is set between 0 and 3600 s. 

*5.1.2. Real-world urban road network setting *

We selected two road networks from different cities: Dongfeng Street in Jinan and Laoshan District in Qingdao. 

For Dongfeng Street, as shown in Fig. 8\(a\), we selected 12 adjacent intersections of crossroads in Dongfeng Street, Jinan City. 

Vehicles can be randomly generated at any location with a vehicle generation rate of 3 vehicles/s. The vehicle generation time is set to 0–3600 s. 

For Laoshan District, as shown in Fig. 8\(b\), we selected 57 adjacent intersections of the road network in Laoshan District, Qingdao City, including 33 crossroads and 24 T-junction. Vehicles can be randomly generated at any location with a vehicle generation rate of 5 

vehicles/s. The vehicle generation time is set to 0–3600 s. 

We made some adjustments to the real road network. In the road networks of two actual cities, we did not consider certain sec-ondary roads with very low traffic volume. Regarding lanes shared by turning and straight-moving vehicles, it is challenging to obtain traffic flow information when they use the same lane. To facilitate information retrieval, we separated them into standard intersection formats. 

**Fig. 8. **Jinan Road Network\(a\) and Qingdao Road Network\(b\). Red dots represent crossroad intersections, and blue dots represent T-junction intersections. \(For interpretation of the references to color in this figure legend, the reader is referred to the web version of this article.\) 14



*T. Wang et *

*Transportation Research Part C 162*

*al. \(2024\) 104582*

*5.1.3. Training settings *

We conducted model training on the synthetic road network using normal traffic flow. The model started at 0 s and continued until all vehicles arrived, constituting one round of training. The model was trained for a total of 120 rounds. The current Q network of the model was trained every four steps, with a learning rate of 0.001, a batch size of 32 for training samples, and the older Q network copied from the current Q network every 200 steps. 

*5.1.4. Assessment settings *

We used three metrics, namely Number of vehicles, Average waiting length, and Average delay time, to comprehensively evaluate the performance of the model. 

Number of vehicles: The number of vehicles present on the road network at the current time. As the same traffic flow file was used for testing, the time and location of vehicle generation were the same. Therefore, fewer vehicles on the road network indicate that more vehicles have completed their journeys, indicating better algorithm performance. 

Average waiting length: The average number of vehicles waiting per lane at the current time. The fewer waiting vehicles, the better the algorithm performance. 

Average delay time: The average delay time of vehicles on the road network at the current time. The shorter the average delay time, the better the algorithm’s performance. 

In addition, in order to make the evaluation more accurate, we repeated the evaluation experiments for each model five times using different random seeds to eliminate the effect of unexpected situations. We set each evaluation experiment to run for 3800 s to avoid the existence of some vehicle routes traveling for too long, which would cause the experiment to be extended indefinitely. 

*5.1.5. Comparison algorithm *

In order to verify the effectiveness of our proposed algorithm, we compared it with other advanced algorithms. 

Longest queue priority \(LQP\): It selects the traffic signal phases to maximize the number of vehicles to the entry lanes of intersections. 

Maxpress \(Mercader et al., 2020\): The state-of-the-art approach in the transportation field, for multi-intersection TSC. It selects the traffic signal phases to maximize the number of vehicles to the entry lanes of intersections. 

Independent Q Learning \(IQL\): This algorithm uses DQN, and each intersection uses a separate agent, with no communication between adjacent intersections. 

CoLight \(Wei et al., 2019\): This algorithm is based on Q-Learning and uses GAT to obtain information about adjacent intersections and promote cooperation between agents. 

IG\_RL \(Devailly et al., 2021\): This algorithm is an advanced graph-based algorithm that constructs the entire traffic environment as graph-structured data, with lanes, links, intersections, and traffic lights as nodes, and all using GCN algorithms for embedding representation, allowing for the transfer of the algorithm. 

*5.2. Analysis of comparative results *

In this section, we will present the training outcomes of the algorithm, results from testing on multiple road networks, and various analyses of these tests. 

**Fig. 9. **Training curve. 

15



*T. Wang et *

*Transportation Research Part C 162*

*al. \(2024\) 104582*

*5.2.1. Training results *

In this section, we will present the training curves for the MGMQ algorithm and other reinforcement learning-based algorithms. 

Due to variations in reward settings among different algorithms, using rewards as a sole evaluation criterion may not be entirely reasonable. Therefore, we employ the negative value of the average intersection delay as an evaluation metric, as depicted in Fig. 9. 

We can observe that the MGMQ algorithm outperforms other algorithms, as its curve rises rapidly and quickly stabilizes, hovering around − 80. This suggests that our MGMQ algorithm achieves fast convergence. In contrast, the IG\_RL algorithm, while initially showing similar performance to the MGMQ algorithm, experiences lower performance after stabilization, likely due to its use of the same graph neural network for intersection information extraction. The poorest performance is observed in the IQL algorithm, which exhibits significant oscillations in the early stages and converges later than other algorithms. Even after convergence, its curve remains lower than the comparative algorithms and displays fluctuations. 

*5.2.2. Synthetic road network results analysis *

In this section, we present the test results of various algorithms on synthetic road networks, as well as the micro-level intersection behavior under the control of the MGMQ algorithm. 

\(1\) Test Results on Synthetic Road Networks. 

On the synthetic road network, we conducted tests using heavy traffic flow. we give the resultant plots of the curves of the number of vehicles, the average waiting time, and the average waiting length in Fig. 10. Where the solid line indicates the mean and the shading indicates the standard deviation. 

Regarding the current number of existing vehicles, as shown in Fig. 10 \(a\), all curves exhibit an upward trend and then a decline after the cessation of vehicle generation. The MGMQ algorithm has the lowest peak at 3820, and its standard deviation remains relatively small, indicating stable performance. IG\_RL performs the best among the comparison algorithms, showing a slow increase after rapid early growth, with a maximum value of 4593. The curves for CoLight, IQL, and Maxpress are relatively close, with peak values of 5182, 5779, and 6098, respectively. The LQP algorithm performs the worst, with a rapidly increasing curve that only shows a slight downward trend when vehicle generation stops, reaching a peak of 8444. 

For the average queue length, as shown in Fig. 10 \(b\), similar to Fig. 10 \(a\), all curves exhibit an increasing trend in the early stage. 

The curve for the MGMQ algorithm is the lowest, growing slowly with a small standard deviation, indicating stable performance, and reaching a peak of 5.98. Among the comparative algorithms, the IG\_RL algorithm performs the best with a maximum value of 8.09. The CoLight, IQL, and Maxpress algorithms perform slightly worse than the first two, with higher peaks and larger standard deviations. The LQP algorithm performs the worst, with a rapidly increasing curve and a large standard deviation. Moreover, after vehicle generation stops, it does not show a downward trend. 

For the average delay time, as shown in Fig. 10 \(c\), similar to the previous two figures, all algorithm curves exhibit an increasing trend in the early stage. The curve for the MGMQ algorithm grows relatively slowly and tends to stabilize after vehicle generation stops, with a peak value of 121.763. In contrast, the curves for the remaining algorithms grow more rapidly. The IG\_RL curve stops growing after vehicle generation stops, with a peak value of 207.567. However, the other curves continue to show a sustained growth trend. Combining the analysis with Fig. 8\(b\), the increasing queue lengths of waiting vehicles lead to a continuous increase in the delay time for vehicles. 

Through the three presented result figures, it is evident that the proposed MGMQ algorithm outperforms the comparative algorithms in reducing vehicle delay time, queue length, and other relevant aspects. This demonstrates that the MGMQ algorithm can be trained on road networks with light traffic flow and can be directly transferred to road networks with different traffic flows without the need for additional training while maintaining satisfactory control performance. Moreover, other reinforcement learning-based algorithms also alleviated traffic congestion to varying degrees, reducing vehicle delay and queue length. 

\(2\) Micro-level Intersection Behavior. 

In this section, we will showcase the micro-level behavior at intersections. We have chosen an intersection denoted as “J0″ as our focal point, which is located at the center of the synthetic road network with a vehicle arrival rate of 5021 Vehicles/s. Therefore, the selection of this intersection is highly representative. 

**Fig. 10. **Results in a synthetic network. 

16



*T. Wang et *

*Transportation Research Part C 162*

*al. \(2024\) 104582*

Due to the overall complexity of the curves, we have extracted the period from 3000 s to 3500 s for a detailed explanation. As shown 

in Fig. 11, we have grouped lanes that release vehicles during the same signal phase together in the same graph. The graph displays the variation of intersection signal phases and the queue lengths of vehicles in different lanes. In this context, E\_1 represents the eastbound left-turn lane, E\_2 represents the eastbound through lane, and the same naming convention applies to other graphs. The right-turn lane, which has a relatively low queue length, is not displayed in the graph. 

From the graph, we can observe that the average number of waiting vehicles at the intersection remains relatively stable. When certain lanes have an excessive number of vehicles queuing, the algorithm promptly switches to the corresponding signal phase, alleviating traffic congestion. Moreover, it maintains this phase for a relatively extended duration, ensuring the smooth flow of vehicles. For lanes with fewer vehicles, it doesn’t unnecessarily delay their release, which would lead to longer waiting times. Instead, it ensures equitable treatment of all lanes, preserving their rights of passage. It is evident that allowing any phase as an action, as proposed in this study, enhances the flexibility of traffic flow control at intersections. 

*5.2.3. Real-world urban road network results analysis *

This section will demonstrate the results analysis of our proposed MGMQ algorithm and other comparative algorithms on two real road networks. 

\(1\) Laoshan District, Qingdao Road. 

For the testing on the road network in the Laoshan District of Qingdao City, we present the result curves in Fig. 12. MGMQ\_S 

represents the model of the MGMQ algorithm trained on the road network of Laoshan District, Qingdao City, serving to validate the model’s transferability. 

For the existing number of vehicles, as shown in Fig. 12\(a\), all algorithms exhibit an initial increasing trend followed by a decreasing trend after the cessation of vehicle generation. MGMQ\_S and MGMQ curves closely resemble each other, with MGMQ\_S 

slightly outperforming MGMQ. Both are significantly lower than the other curves and exhibit smaller standard deviations, with peak values of 3799.6 and 3868.8, respectively. For IG\_RL and CoLight algorithms, their curves are higher than the first two algorithms, with peak values of 4550 and 4984. In contrast to the performance of the previous road network, the IQL algorithm’s curve is higher than that of the Maxpress algorithm, indicating that the road network may be more complex, and thus, IQL struggles to handle this complexity. The peak values for Maxpress and IQL are 5766.6 and 6631.6, respectively. 

For the average waiting length, as shown in Fig. 12\(b\), all algorithmic curves exhibit an initial upward trend. MGMQ\_S and MGMQ 

curves closely resemble each other, both showing an increasing trend initially and a subsequent decline after the cessation of vehicle generation. In the initial phase, the MGMQ curve is lower than the MGMQ\_S curve, but in the later phase, it surpasses the MGMQ\_S 

curve, with respective peak values of 6.243 and 6.36. Other algorithms show an upward trend in the initial phase, but IG\_RL and CoLight exhibit a distinct downward trend in the later phase, while IQL and Maxpress curves remain relatively close, showing only a slight downward trend towards the end. 

**Fig. 11. **Intersection Microscopic Behavior. 

17





*T. Wang et *

*Transportation Research Part C 162*

*al. \(2024\) 104582*

**Fig. 12. **Results in the Laoshan District network of Qingdao City. 

For the average delay time, as depicted in Fig. 12\(c\), all curves exhibit an initial growth phase. However, apart from the MGMQ and MGMQ\_S algorithms showing a subsequent downward trend in the later phase, other algorithmic curves continue to show a sustained upward trend. The MGMQ and MGMQ\_S curves follow a similar trend as in Fig. 10\(b\), with respective peak values of 156 and 172. The remaining curves all demonstrate a continuous upward trend, with IQL and Maxpress showing a faster rate of increase. 

\(2\) Jinan City Dongfeng Street Road. 

For the test on the road network of Dongfeng Street in Jinan City, the result curves are shown in Fig. 13. MGMQ\_S represents the model trained by the MGMQ algorithm on the road network of Dongfeng Street in Jinan City, serving as a means to validate the model’s transferability. Given the inability of the LQP algorithm to adapt to this environment, we have excluded it from comparative analysis. 

For the current vehicle count, as analyzed from Fig. 13\(a\), all curves exhibit an initial increasing trend followed by a decreasing trend after the cessation of vehicle generation. The MGMQ algorithm and MGMQ\_S algorithm show remarkably similar behaviors, with peak values of 948 and 933, respectively. However, in the later stages, the MGMQ\_S algorithm experiences a faster decline. In the case of IG\_RL and CoLight, both exhibit a similar pattern in the early stages, with CoLight slightly outperforming IG\_RL. However, after 3000 s, CoLight experiences a rapid increase surpassing IG\_RL, with peak values of 1190 and 1310, respectively. Concerning the IQL 

algorithm, its curve surpasses those of the aforementioned algorithms, steadily increasing until reaching a peak of 1458. As for the Maxpress algorithm, it initially performs well, but with an increase in the number of vehicles, its control effectiveness gradually di-minishes, showing a rapid rise in the number of vehicles, with a peak value of 1636. 

Regarding the average waiting length, illustrated in Fig. 13\(b\), the MGMQ\_S algorithm exhibits the optimal curve, with the MGMQ 

curve closely resembling it. Both show a gradual increase, and the peak values for MGMQ\_S and MGMQ are 4.26 and 4.83, respectively. 

For the IG\_RL, CoLight, and IQL algorithms, their curves consistently rise. As for the Maxpress algorithm, it demonstrates a slow increase in the early stages, but with the overall growth in the number of vehicles, its curve undergoes rapid escalation in the later stages, reaching a peak of 9.93. 

For the average delay time, as shown in Fig. 13\(c\), the overall trend is similar to the previous two graphs. The curves for MGMQ\_S 

and MGMQ are comparable, both exhibiting a slow rise followed by a decline, with peak values of 80.911 and 87.978, respectively. The IG\_RL curve rises more rapidly compared to the first two algorithms but shows a trend of plateauing towards the end. The remaining algorithms demonstrate a sustained upward trend, with CoLight rising at a slower pace, and Maxpress having the fastest rise. 

In the testing results on two real road networks, our proposed MGMQ algorithm achieved favorable performance in all three metrics. This demonstrates that the MGMQ algorithm shows excellent adaptability to irregular traffic networks and varying traffic flow conditions. Additionally, when compared to models trained on real urban road networks, the algorithm trained on the synthetic road network also performed well. This suggests that the proposed algorithm exhibits good transferability. 

**Fig. 13. **Results in the Dongfeng Street network of Jinan City. 

18

*T. Wang et *

*Transportation Research Part C 162*

*al. \(2024\) 104582*

*5.3. Ablation study *

The MGMQ algorithm proposed in this paper includes structures such as GAT and improved GraphSAGE. In order to verify the rationality of adding these algorithms, we made partial changes to the MGMQ algorithm and conducted ablation studies. 

*5.3.1. Ablation study algorithm *

No-GAT-MGMQ \(NG\_MGMQ\): This algorithm replaces the GAT algorithm in the MGMQ algorithm with a fully connected layer while other parts remain unchanged. 

Bi-LSTM-MGMQ \(BL\_MGMQ\): This algorithm replaces the improved GraphSAGE aggregation layer in the MGMQ algorithm with a bi-directional LSTM \(Bi-LSTM\), while other parts remain unchanged. 

GraphSAGE-MGMQ\(G\_MGMQ\): This algorithm replaces the improved GraphSAGE aggregation layer in the MGMQ algorithm with a MEAN aggregator, while other parts remain unchanged. 

Cyclic Phase-MGMQ \(CP\_MGMQ\): This algorithm changes the action output to whether or not to switch phases, it becomes a cyclic phase. Other parts remain unchanged. 

We use the same training settings for these variant algorithms as we did for MGMQ, and test them on synthetic road networks using vehicle generation rates of 5 vehicles/s. 

*5.3.2. Analysis of the ablation study results *

In Table 2, we present the average results for the number of existing vehicles, average waiting time, and average waiting length under different ablation study scenarios. Comparing MGMQ with BL\_MGMQ and G\_MGMQL algorithms, it can be observed that utilizing Bi-GRU allows for better aggregation of information from neighboring intersections, enabling the current intersection agent to make optimal decisions. Compared to the CP\_MGMQ algorithm, the ability to use arbitrary phases as actions highlights the flexibility in controlling traffic flow and alleviating traffic congestion at intersections. Contrasting with the NG\_MGMQ algorithm, the adoption of the GAT algorithm emphasizes its capability to aggregate traffic flow information among different lanes within the same intersection, enabling the model to adapt to varying traffic flow levels. These results demonstrate the effectiveness of our proposed model, utilizing the GAT algorithm to aggregate intra-intersection information and an improved GraphSAGE for inter-intersection information in traffic signal control. This leads to significant enhancements in algorithm performance. 

*5.4. Sensitivity analysis of * Δ *t value *

Through an analysis of the relevant literature \(Aslani et al., 2017; Wang et al., 2022\), we found that parameter Δ *t * is typically set to values such as 5 or 10 s. In this study, we have set it to 10 s. We conducted a sensitivity analysis on this parameter in a synthetic road network with a vehicle generation rate of 5 vehicles/s. The results of the analysis for different values of Δ *t * are shown in the Fig. 14. 

We can observe that all three metrics exhibit a trend of initially decreasing and then increasing. At Δ *t *= 5 *s*, the control performance is not very favorable. We found that, due to our setting of a 3 s yellow time, when Δ *t * is too small, the green time becomes excessively short, leading to a decrease in intersection throughput efficiency. The reduction in phase-switching frequency, while having a limited impact on the current intersection throughput, can nevertheless exert a notable influence on the overall traffic efficiency of the entire road network. The optimal value is achieved at Δ *t *= 10 *s*, making it a reasonably suitable choice in this study. 

*5.5. Attention head impact analysis *

We used the multi-head attention mechanism in the GAT algorithm of the MGMQ algorithm. In order to explore the impact of attention head numbers on the algorithm, we conducted comparative experiments on a synthetic network with a vehicle generation rate of 5 vehicles/s. 

The test results in Fig. 15 illustrate the number of existing vehicles, average vehicle delay time, and average waiting vehicles per lane under different numbers of attention heads. It can be observed that as the number of attention heads increases, the average vehicle delay time gradually decreases, and the average number of waiting vehicles per lane also decreases. However, when the number of attention heads exceeds 4, there is no further reduction in these metrics, and instead, they exhibit an increasing trend. Therefore, it can be inferred that the model performs optimally when the number of attention heads is 4. Regarding the number of existing vehicles, it reaches its lowest value when the number of attention heads is 5. However, considering the other two metrics and model complexity, an overall consideration suggests that the number of attention heads equal to 4 is the most reasonable choice. 

**6. Conclusion **

In this paper, we propose the MGMQ algorithm, which is based on a multi-layer graph and the Deep Q Learning algorithm, for ATSC. Specifically, we introduce a computation method using multi-layer graphs, dividing the traffic environment into lower-layer intersection graphs and upper-layer traffic network graphs. At the intersection graphs, we employ the GAT algorithm to aggregate lane information within each intersection. For the traffic network graphs, we propose an improved GraphSAGE algorithm to aggregate information from neighboring intersections. This computational approach generates state representation embeddings for intersections that contain both geometric and spatial features. This algorithm can be applied to different traffic states and networks, providing effective algorithm support for complex regional traffic signal control. To accommodate diverse intersection structures \(such as T-19





*T. Wang et *

*Transportation Research Part C 162*

*al. \(2024\) 104582*

**Table 2 **

Results of ablation study. 

NG\_MGMQ 

CP\_MGMQ 

G\_MGMQ 

BL\_MGMQ 

MGMQ 

Number of vehicles 

1799.568 

1743.282 

1680.316 

1628.216 

1588.908 

Average waiting length 

1.178 

1.125 

1.032 

0.943 

0.785 

Average delay time 

21.665 

20.416 

14.569 

13.786 

13.034 

**Fig. 14. **Sensitivity analysis of Δ *t * value. 

**Fig. 15. **Results of comparing different attentional heads. 

intersections and intersections\), we utilize a mask-action mechanism, allowing the algorithm to choose actions as any signal phase, enabling optimal real-time control of traffic flow during traffic signal timing. Additionally, we implement parameter sharing among agents, reducing the training parameters and enabling the algorithm to transfer seamlessly between different intersections without retraining. We conduct experiments on both a heavy traffic state synthetic network and real road networks in Qingdao and Jinan. The test results show significant improvements compared to other benchmark algorithms, demonstrating the MGMQ algorithm’s excellent transferability and scalability. 

This paper also has certain limitations. For intersections with more than four directions, we have chosen to treat them as four-way intersections for computation, which may result in issues such as confusion among lanes and vehicles. In future work, we will address these limitations and propose improvements. Furthermore, in our future research, we plan to consider more detailed graph layers, such as a lane graph, where vehicles are treated as nodes, and suitable aggregation algorithms are employed, such as GAT, GCN, etc. 

Additionally, in our current work, we have focused solely on vehicular traffic, but we intend to incorporate pedestrian information into the ATSC algorithm to facilitate fairer passage for all participants at intersections. 

**CRediT authorship contribution statement **

**Tao Wang: **Methodology, Investigation, Conceptualization. **Zhipeng Zhu: **Writing – review & editing, Software, Methodology, Investigation. **Jing Zhang: **Writing – review & editing, Investigation. **Junfang Tian: **Writing – review & editing, Supervision, Methodology, Investigation. **Wenyi Zhang: **Writing – review & editing, Methodology. 

20

*T. Wang et *

*Transportation Research Part C 162*

*al. \(2024\) 104582*

**Declaration of Competing Interest **

The authors declare that they have no known competing financial interests or personal relationships that could have appeared to influence the work reported in this paper. 

**Acknowledgments **

This research was funded by the National Natural Science Foundation of China. 

\(Grant 71971125, 72222021\), and the Natural Science Foundation of ShandongProvince \(Grant ZR2021MG026\). 

**References **

Abdulhai, B., Pringle, R., Karakoulas, G.J., 2003. Reinforcement learning for true adaptive traffic signal control. Journal of Transportation Engineering 129 \(3\), 

278–285. 

Arulkumaran, K., Deisenroth, M.P., Brundage, M., Bharath, A.A., 2017. Deep reinforcement learning: A brief survey. IEEE Signal Processing Magazine 34 \(6\), 26–38. 

Aslani, M., Mesgari, M.S., Wiering, M., 2017. Adaptive traffic signal control with actor-critic methods in a real-world traffic network with different traffic disruption 

events. Transportation Research Part c: Emerging Technologies 85, 732–752. 

Busoniu, L., De Schutter, B., Babuska, R., 2006. Decentralized reinforcement learning control of a robotic manipulator. In: 2006 9th International Conference on 

Control. Automation, Robotics and Vision, pp. 1–6. 

Casas, N., 2017. Deep deterministic policy gradient for urban traffic light control. arXiv preprint arXiv:1703.09035. 

Ceylan, H., Bell, M.G., 2004. Traffic signal timing optimisation based on genetic algorithm approach, including drivers’ routing. Transportation Research Part b: 

Methodological 38 \(4\), 329–342. 

Chu, T., Wang, J., Codecà, L., Li, Z., 2019. Multi-agent deep reinforcement learning for large-scale traffic signal control. IEEE Transactions on Intelligent 

Transportation Systems 21 \(3\), 1086–1095. 

Devailly, F.X., Larocque, D., Charlin, L., 2021. IG-RL: Inductive graph reinforcement learning for massive-scale traffic signal control. IEEE Transactions on Intelligent 

Transportation Systems 23 \(7\), 7496–7507. 

El-Tantawy, S., Abdulhai, B., 2010. An agent-based learning towards decentralized and coordinated traffic signal control. In: Proceedings of the 13th International IEEE Conference on Intelligent Transportation Systems, pp. 665-670. 

Fang, S., Chen, F., Liu, H., 2019. Dueling Double Deep Q-Network for Adaptive Traffic Signal Control with Low Exhaust Emissions in A Single Intersection. In: In: 

Proceedings of the IOP Conference Series: Materials Science and Engineering, p. 612 \(5\). . 

Ge, H., Gao, D., Sun, L., Hou, Y., Yu, C., Wang, Y., Tan, G., 2021. Multi-agent transfer reinforcement learning with multi-view encoder for adaptive traffic signal 

control. IEEE Transactions on Intelligent Transportation Systems 23 \(8\), 12572–12587. 

Hamilton, W., Ying, Z., Leskovec, J., 2017. Inductive representation learning on large graphs. In: In: Proceedings of the 31st International Conference on Neural 

Information Processing Systems, pp. 1025–1035. 

Hasselt, H.V., Guez, A., Silver, D., 2016. Deep reinforcement learning with double q-learning. In: Proceedings of the AAAI Conference on Artificial Intelligence, 30 \(1\). 

Huang, S., Onta˜nón, S., 2020. A closer look at invalid action masking in policy gradient algorithms. arXiv preprint arXiv:2006.14171. 

Hunt, P.B., Robertson, D.I., Bretherton, R.D., Royle, M.C., 1982. The SCOOT on-line traffic signal optimisation technique. Traffic Engineering and Control 23 \(4\). 

Kipf, T.N., Welling, M., 2016. Semi-supervised classification with graph convolutional networks. arXiv preprint arXiv:1609.02907. 

Lee, J., Abdulhai, B., Shalaby, A., Chung, E.H., 2005. Real-time optimization for adaptive traffic signal control using genetic algorithms. Journal of Intelligent 

Transportation Systems 9 \(3\), 111–122. 

Li, X., Cui, J., An, S., Parsafard, M., 2014. Stop-and-go traffic analysis: Theoretical properties, environmental impacts and oscillation mitigation. Transportation 

Research Part b: Methodological 70, 319–339. 

Li, Y., He, J., Gao, Y., 2021b. Intelligent traffic signal control with deep reinforcement learning at single intersection. In: In: Proceedings of the 2021 7th International 

Conference on Computing and Artificial Intelligence, pp. 399–406. 

Li, Z., Yu, H., Zhang, G., Dong, S., Xu, C., 2021a. Network-wide traffic signal control optimization using a multi-agent deep reinforcement learning. Transportation 

Research Part c: Emerging Technologies 125, 103059. 

Liu, Z., 2007. A survey of intelligence methods in urban traffic signal control. IJCSNS International Journal of Computer Science and Network Security 7 \(7\), 105–112. 

Luk, J.Y.K., 1984. Two traffic-responsive area traffic control methods: SCAT and SCOOT. Traffic Engineering and Control 25 \(1\), 14–22. 

Ma, T., Peng, K., Rong, H., Qian, Y., 2023. AGRCNet: communicate by attentional graph relations in multi-agent reinforcement learning for traffic signal control. 

Neural Computing and Applications 35 \(28\), 21007–21022. 

Mao, F., Li, Z., Lin, Y., Li, L., 2022. Mastering arterial traffic signal control with multi-agent attention-based soft actor-critic model. IEEE Transactions on Intelligent 

Transportation Systems 24 \(3\), 3129–3144. 

Mercader, P., Uwayid, W., Haddad, J., 2020. Max-pressure traffic controller based on travel times: An experimental analysis. Transportation Research Part c: 

Emerging Technologies 110, 275–290. 

Mnih, V., Kavukcuoglu, K., Silver, D., Rusu, A.A., Veness, J., Bellemare, M.G., Graves, A., Riedmiller, M., Fidjeland, A.K., Ostrovski, G., Petersen, S., Beattie, C., 

Sadik, A., Antonoglou, I., King, H., Kumaran, D., Wierstra, D., Legg, S., Hassabis, D., 2015. Human-level control through deep reinforcement learning. Nature 518 

\(7540\), 529–533. 

Mousavi, S.S., Schukat, M., Howley, E., 2018. Deep reinforcement learning: an overview. In: Proceedings of the SAI Intelligent Systems Conference, pp. 426-440. 

Niittymäki, J., Pursula, M., 2000. Signal control using fuzzy logic. Fuzzy Sets and Systems 116 \(1\), 11–22. 

Nishi, T., Otaki, K., Hayakawa, K., Yoshimura, T., 2018. Traffic signal control based on reinforcement learning with graph convolutional neural nets. In: In 2018 21st 

International Conference on Intelligent Transportation Systems, pp. 877–883. 

Norouzi, M., Abdoos, M., Bazzan, A.L., 2021. Experience classification for transfer learning in traffic signal control. The Journal of Supercomputing 77, 780–795. 

Pang, H., Gao, W., 2019. Deep deterministic policy gradient for traffic signal control of single intersection. In: In: Proceedings of the 2019 Chinese Control and 

Decision Conference, pp. 5861–5866. 

Peng, H., Du, B., Liu, M., Liu, M., Ji, S., Wang, S., Zhang, X., He, L., 2021. Dynamic graph convolutional network for long-term traffic flow prediction with 

reinforcement learning. Information Sciences 578, 401–416. 

Prashanth, L.A., Bhatnagar, S., 2011. Reinforcement learning with average cost for adaptive control of traffic lights at intersections. In: Proceedings of the 2011 14th International IEEE Conference on Intelligent Transportation Systems, pp. 1640-1645. 

Saito, M., Fan, J., 2000. Artificial neural network–based heuristic optimal traffic signal timing. Computer-Aided Civil and Infrastructure Engineering 15 \(4\), 293–307. 

Srinivasan, D., Choy, M.C., Cheu, R.L., 2006. Neural networks for real-time traffic signal control. IEEE Transactions on Intelligent Transportation Systems 7 \(3\), 

261–272. 

Tan, T., Bao, F., Deng, Y., Jin, A., Dai, Q., Wang, J., 2019. Cooperative deep reinforcement learning for large-scale traffic grid signal control. IEEE Transactions on 

Cybernetics 50 \(6\), 2687–2700. 

Thorpe, T.L., Anderson, C.W., 1996. Traffic light control using sarsa with three state representations. IBM Corporation. Technical report. 

Trabia, M.B., Kaseko, M.S., Ande, M., 1999. A two-stage fuzzy logic controller for traffic signals. Transportation Research Part c: Emerging Technologies 7 \(6\), 

353–367. 

21

*T. Wang et *

*Transportation Research Part C 162*

*al. \(2024\) 104582*

Van der Pol, E., Oliehoek, F.A., 2016. Coordinated deep reinforcement learners for traffic light control. Proceedings of Learning, Inference and Control of Multi-Agent 

Systems 8, 21–38. 

Veličković, P., Casanova, A., Liò, P., Cucurull, G., Romero, A., Bengio, Y., 2018. Graph attention networks. In: Proceedings of the 6th International Conference on 

Learning Representations. 

Wang, T., Cao, J., Hussain, A., 2021a. Adaptive Traffic Signal Control for large-scale scenario with Cooperative Group-based multi-agent reinforcement learning. 

Transportation Research Part c: Emerging Technologies 125, 103046. 

Wang, M., Wu, L., Li, J., He, L., 2021b. Traffic signal control with reinforcement learning based on region-aware cooperative strategy. IEEE Transactions on Intelligent 

Transportation Systems 23 \(7\), 6774–6785. 

Wang, M., Wu, L., Li, M., Wu, D., Shi, X., Ma, C., 2022. Meta-learning based spatial-temporal graph attention network for traffic signal control. Knowledge-Based 

Systems 250, 109166. 

Webster, F.V., 1958. Traffic signal settings. Road Research Technical Paper No. 39, HMSO, London. 

Wei, H., Zheng, G., Yao, H., Li, Z., 2018. Intellilight: A reinforcement learning approach for intelligent traffic light control. In: In: Proceedings of the 24th ACM 

SIGKDD International Conference on Knowledge Discovery and Data Mining, pp. 2496–2505. 

Wei, H., Xu, N., Zhang, H., Zheng, G., Zang, X., Chen, C., Zhang, W., Zhu, Y., Xu, K., Li, Z., 2019. Colight: Learning network-level cooperation for traffic signal control. 

In: In: Proceedings of the 28th ACM International Conference on Information and Knowledge Management, pp. 1913–1922. 

Wiering, M., 2000. Multi-agent reinforcement learning for traffic light control. In: Proceedings of the Machine Learning: Proceedings of the Seventeenth International Conference, pp. 1151-1158. 

Wu, T., Zhou, P., Liu, K., Yuan, Y., Wang, X., Huang, H., Wu, D.O., 2020. Multi-agent deep reinforcement learning for urban traffic light control in vehicular networks. 

IEEE Transactions on Vehicular Technology 69 \(8\), 8243–8256. 

Yang, S., 2023. Hierarchical graph multi-agent reinforcement learning for traffic signal control. Information Sciences 634, 55–72. 

Yang, S., Yang, B., Kang, Z., Deng, L., 2021. IHG-MA: Inductive heterogeneous graph multi-agent reinforcement learning for multi-intersection traffic signal control. 

Neural Networks 139, 265–277. 

Yang, S., Yang, B., 2022. An inductive heterogeneous graph attention-based multi-agent deep graph infomax algorithm for adaptive traffic signal control. Information 

Fusion 88, 249–262. 

Yoon, J., Ahn, K., Park, J., Yeo, H., 2021. Transferable traffic signal control: Reinforcement learning with graph centric state representation. Transportation Research 

Part c: Emerging Technologies 130, 103321. 

Zahavy, T., Haroush, M., Merlis, N., Mankowitz, D.J., Mannor, S., 2018. Learn what not to learn: Action elimination with deep reinforcement learning. In: In: 

Proceedings of the Advances in Neural Information Processing Systems, pp. 3562–3573. 

Zang, X., Yao, H., Zheng, G., Xu, N., Xu, K., Li, Z., 2020. Metalight: Value-based meta-reinforcement learning for traffic signal control. In Proceedings of the AAAI Conference on Artificial Intelligence, pp. 1153-1160. 

Zhang, K., Batterman, S., 2013. Air pollution and health risks due to vehicle traffic. Science of the Total Environment 450, 307–316. 

Zhang, J., Li, S., Li, L., 2023. Coordinating CAV swarms at intersections with a deep learning model. IEEE Transactions on Intelligent Transportation Systems 24 \(6\), 

6280–6291. 

Zhao, L., Song, Y., Zhang, C., Liu, Y., Wang, P., Lin, T., Deng, M., Li, H., 2019. T-gcn: A temporal graph convolutional network for traffic prediction. IEEE Transactions 

on Intelligent Transportation Systems 21 \(9\), 3848–3858. 

Zhou, J., Cui, G., Hu, S., Zhang, Z., Yang, C., Liu, Z., Wang, L., Li, C., Sun, M., 2020. Graph neural networks: A review of methods and applications. AI Open 1, 57–81. 

22


# Document Outline

+ A large-scale traffic signal control algorithm based on multi-layer graph deep reinforcement learning  
	+ 1 Introduction 
	+ 2 Related work 
	+ 3 Problem definition  
		+ 3.1 Definitions of standard intersections 
		+ 3.2 Reinforcement learning environment 

	+ 4 Model  
		+ 4.1 Overall framework 
		+ 4.2 Intersection embedding 
		+ 4.3 Network embedding 
		+ 4.4 Q-network 
		+ 4.5 Action mask 
		+ 4.6 Overview of MGMQ algorithm 
		+ 4.7 Parameter sharing 
		+ 4.8 T-intersection Setting 

	+ 5 Experiment  
		+ 5.1 General settings  
			+ 5.1.1 Synthetic road network settings 
			+ 5.1.2 Real-world urban road network setting 
			+ 5.1.3 Training settings 
			+ 5.1.4 Assessment settings 
			+ 5.1.5 Comparison algorithm 

		+ 5.2 Analysis of comparative results  
			+ 5.2.1 Training results 
			+ 5.2.2 Synthetic road network results analysis 
			+ 5.2.3 Real-world urban road network results analysis 

		+ 5.3 Ablation study  
			+ 5.3.1 Ablation study algorithm 
			+ 5.3.2 Analysis of the ablation study results 

		+ 5.4 Sensitivity analysis of Δt value 
		+ 5.5 Attention head impact analysis 

	+ 6 Conclusion 
	+ CRediT authorship contribution statement 
	+ Declaration of Competing Interest 
	+ Acknowledgments 
	+ References



