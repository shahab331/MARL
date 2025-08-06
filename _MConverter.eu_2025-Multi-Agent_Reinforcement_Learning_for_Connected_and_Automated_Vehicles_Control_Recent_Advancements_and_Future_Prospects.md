16266

IEEE TRANSACTIONS ON AUTOMATION SCIENCE AND ENGINEERING, VOL. 22, 2025

Multi-Agent Reinforcement Learning for Connected and Automated Vehicles Control: Recent

Advancements and Future Prospects

Min Hua , Graduate Student Member, IEEE, Xinda Qi , Member, IEEE, Dong Chen , Member, IEEE, Kun Jiang , Zemin Eitan Liu , Hongyu Sun, Quan Zhou , Member, IEEE, and Hongming Xu

Abstract—Connected and automated vehicles \(CAVs\) have handling dynamic interactions, improving traffic flow, enhancing emerged as a potential solution to the future challenges of safety, and optimizing fuel efficiency. The paper reviews state-developing safe, efficient, and eco-friendly transportation systems. 

of-the-art MARL algorithms and simulation platforms, serving However, CAV control presents significant challenges signifi-as a resource for practitioners looking to implement these cant challenges due to the complexity of interconnectivity and advanced control strategies. However, real-world deployment coordination required among vehicles. Multi-agent reinforcement remains challenging due to communication reliability, real-time learning \(MARL\), which has shown notable advancements in decision-making constraints, and the complexities of mixed traffic addressing complex problems in autonomous driving, robotics, environments involving both automated and human-driven vehi-and human-vehicle interaction, emerges as a promising tool to cles. Future research should focus on ensuring robust inter-agent enhance CAV capabilities. Despite its potential, there is a notable communication, developing safety-aware MARL frameworks, absence of current reviews on mainstream MARL algorithms and addressing the sim-to-real transfer gap. This paper provides for CAVs. To fill this gap, this paper offers a comprehensive insights to help practitioners bridge the gap between research review of MARL’s application in CAV control. The paper and deployment, facilitating the development of more scalable, begins with an introduction to MARL, explaining its unique adaptive, and reliable CAV control. 

advantages in handling complex and multi-agent scenarios. It Index Terms—Connected and automated vehicles, multi-agent then presents a detailed survey of MARL applications across reinforcement learning, intelligent transportation systems, vehicle various control dimensions for CAVs, including critical scenarios control. 

such as platooning control, lane-changing, and unsignalized intersections. Additionally, the paper reviews prominent simulation platforms essential for developing and testing MARL algorithms I. INTRODUCTION

for CAVs. Lastly, it examines the current challenges in deploying MARL for CAV control, including safety, communication, mixed ADVANCEMENTS in automation, artificial intelligence traffic, and sim-to-real challenges. Potential solutions discussed \(AI\), and vehicular communication are transforming include hierarchical MARL, decentralized MARL, adaptive inter-transportation, leading to the emergence of connected and actions, and offline MARL. The work has been summarized in automated vehicles \(CAVs\) \[1\]. By integrating vehicle-to-MARL in CAV Control Repository. 

vehicle \(V2V\) and vehicle-to-infrastructure \(V2I\) communica-Note to Practitioners—This paper explores the application of tion, CAVs enable cooperative perception, real-time decision-MARL for controlling CAVs in complex traffic scenarios such as making, and traffic optimization \[2\]. However, achieving safe, platooning, lane-changing, and intersections. MARL provides an efficient, and scalable CAV control in complex and dynamic adaptive and decentralized control approach, offering advantages environments remains a critical challenge \[3\], \[4\]. 

over traditional rule-based and optimization-based methods in Various control optimization strategies have been explored to enhance the coordination and efficiency of CAVs \[5\], \[6\]. 

Received 30 August 2024; revised 12 February 2025 and 16 May 2025; Among these, conventional methods such as model predictive accepted 25 May 2025. Date of publication 28 May 2025; date of current version 12 June 2025. This article was recommended for publication by control \(MPC\) have been employed to coordinate platoon Associate Editor X. Zhang and Editor J. Yi upon evaluation of the reviewers’

behavior, minimize control delay, and reduce traffic oscilla-comments. \(Corresponding author: Hongming Xu.\) tions \[7\]. Additionally, non-convex optimal control problems, Min Hua, Hongyu Sun, and Hongming Xu are with the School of Engineering, University of Birmingham, B15 2TT Birmingham, U.K. \(e-mail: such as CAV coordination at intersections, have been tackled h.m.xu@bham.ac.uk\). 

with semidefinite relaxation techniques \[8\]. However, these Xinda Qi is with the Department of Electrical and Computer Engineering, approaches often depend on precise system modeling, which is Michigan State University, East Lansing, MI 48824 USA. 

Dong Chen is with the Agricultural and Biological Engineering, Mississippi not always available \[9\], and require substantial computational State University, Starkville, MS 39762 USA. 

resources, making them impractical for real-time control \[10\]. 

Kun Jiang is with the School of Automation, Southeast University, Nanjing Besides, reinforcement learning \(RL\) has gained increasing 210018, China. 

Zemin Eitan Liu is with the Chemical and Petroleum Engineering attention within the research field due to its outstanding Department, University of Pittsburgh, Pittsburgh, PA 15260 USA. 

abilities in addressing sequential decision-making tasks, such Quan Zhou is with the School of Engineering, University of Birmingham, as gaming \[11\], robotics \[12\], behavioral planning \[13\], intelli-B15 2TT Birmingham, U.K., and also with the School of Automotive Studies, Tongji University, Shanghai 201804, China. 

gent energy management \[14\], \[15\]. Similarly, AV control has Digital Object Identifier 10.1109/TASE.2025.3574280

begun exploring the potential of employing RL for various

© 2025 The Authors. This work is licensed under a Creative Commons Attribution 4.0 License. 

For more information, see https://creativecommons.org/licenses/by/4.0/

HUA et al.: MARL FOR CAVs CONTROL: RECENT ADVANCEMENTS AND FUTURE PROSPECTS

16267

traffic scenarios \[16\]. For instance, in \[17\], a deep deter-for single-agent RL cannot be directly applied to MARL

ministic policy gradient \(DDPG\)-based model for platooning scenarios, reinforcing that RL struggles to handle multi-agent control is introduced to enhance fuel economy, driving effi-coordination challenges in safety-critical CAV applications. 

ciency, and safety at signalized intersections through real-time Similarly, in \[28\], MARL-based motion controllers are eval-optimization. This approach featuring an effective reward func-uated against RL approaches for lane-changing, showing tion, demonstrates strong performance under varying traffic that MARL achieves smoother lane changes, lower collision demands and traffic light cycles with different durations. Tak-rates, and better adaptability to dynamic environments. These ing into account the role of HDVs in the control of AVs, Shi et findings confirm that MARL outperforms RL when multiple al. employ a distributed proximal policy optimization \(DPPO\) autonomous agents need to be coordinated in an interactive control strategy that allows them to learn from and respond traffic environment. While MARL offers clear advantages, it to the behavior of the HDVs, optimizing performance at both also introduces additional computational and communication the local subsystem level and the broader mixed traffic context complexity, particularly in terms of information sharing during

\[18\]. Qu et al. introduce a control approach utilizing DDPG

training and execution. A common concern is that MARL

algorithm aimed at reducing traffic fluctuations and enhancing may require excessive connectivity and centralized training, fuel economy. However, these RL-based approaches only making it impractical for real-world deployment. To mitigate consider a single agent \(i.e., AV\), making them poorly suited these challenges, recent works have explored hierarchical for multi-agent coordination and generalization in dense traffic MARL \[18\], graph-based coordination \[20\], and decentralized environments \[19\]. As autonomous driving moves toward training techniques \[29\], ensuring scalability without excessive multi-vehicle interaction and cooperative control, single-agent information-sharing demands. 

RL struggles with scalability, decentralized decision-making, In the context of CAV control, MARL has been increasingly and shared state information, limiting its effectiveness in adopted to optimize collective behaviors, offering a scalable complex, dynamic traffic scenarios. 

and cooperative solution to real-world deployment challenges Multi-agent reinforcement learning \(MARL\) extends single-

\[30\]. Connectivity within this cooperative deployment operates agent RL to settings where multiple agents interact and learn on two levels: V2V communication, which enables direct collectively. This innovative approach has found applications data sharing between vehicles, and V2I communication, which across a broad spectrum of fields. Notably, the gaming and expands connectivity through technologies like vehicular ad simulation industry has utilized MARL to create more com-hoc networks and Ethernet-based systems. Together, these plex and interactive environments \[20\]. Furthermore, within communication channels ensure robust inter-agent communi-the realm of finance, MARL models are employed to simulate cation and situational awareness, both of which are critical the dynamics of markets and the behaviors of agents \[21\]. 

for the scalability and effectiveness of CAVs \[31\]. Fig. 1

In traffic control and management, MARL algorithms have illustrates a comprehensive multi-agent system, i.e., CAVs, been instrumental in optimizing traffic flows and reducing including environmental data from sensors such as GPS/INS, congestion. The realm of AVs and robotics has also ben-cameras, radar, and lidar, along with V2I communication efited greatly, with MARL enabling cooperative navigation channels providing information from traffic signals, roadside and coordination among vehicles and facilitating collaborative units, and cloud systems. This data is fused to create a unified tasks in AVs and robotics \[22\]. Extended to CAV control, environmental representation. Each AV maintains a local data each vehicle acts as an independent agent that learns from its repository while accessing shared V2V and V2I information, interactions with the surrounding environment, which includes enhancing decision-making and situational awareness \[32\]. 

other vehicles, traffic signals, and road conditions. Each CAV

The decision-making and motion-planning modules process learns not only to maneuver safely and efficiently on its own these inputs to generate optimal strategies for safe and efficient but also to cooperate and communicate with other CAVs \[23\]. 

navigation. These strategies are then executed through steering Therefore, MARL offers a valuable strategy for improving the and powertrain control modules. By leveraging both V2V

performance and efficiency of CAVs. 

and V2I communication, the multi-agent system demonstrates Several studies have empirically demonstrated that MARL

how integrated connectivity enables robust coordination and outperforms single-agent RL in scenarios requiring multi-scalability within the CAV ecosystem, ultimately laying the agent interaction, such as mixed traffic and cooperative foundation for smarter and more efficient transportation net-vehicle control \[24\]. Unlike RL, which follows an inde-works. 

pendent decision-making framework, MARL enables policy Despite advancements in MARL for CAV systems, sig-coordination and shared decision-making, resulting in supe-nificant challenges remain in adapting these techniques to rior scalability, efficiency, and safety in dense and dynamic real-world CAV control. Issues such as scalability, robustness environments \[25\]. While \[26\] provides an overview of single-in dynamic environments, and the integration of decentralized agent RL in CAV control, it highlights the limitations of learning frameworks require further investigation. While a few independent decision-making in multi-agent environments, articles describe the potential of MARL in CAVs \[33\], none of where interactions between vehicles significantly impact per-them, to the best of our knowledge, are specifically devoted to formance. These limitations underscore the necessity of the application of MARL for CAV control. This paper is thus MARL for cooperative lane-changing, intersection manage-intended to deliver a comprehensive and systematic review ment, and on-ramps merging optimization. In \[27\], the of MARL within the realm of CAVs, such as lane changing, authors emphasize that existing safe RL methods designed platooning control, traffic signal cooperation, and on-ramp





16268

IEEE TRANSACTIONS ON AUTOMATION SCIENCE AND ENGINEERING, VOL. 22, 2025

Fig. 1. The schematic of the multi-agent system for CAV control. 

merging. Through this review, we not only provide a clear, up-Deep RL methods leverage neural networks to approximate to-date understanding of the current classic MARL algorithms value functions or policies, enabling applications in high-applied in CAV control, but we also outline the potential dimensional control problems such as autonomous driving. 

direction for future work in this area. The main contributions These methods can be broadly categorized into: Value-based of the work presented in this paper are summarized as follows: methods \(e.g., DQN, DDQN\): learn the Q-function Q\(s, a\) to 1\) We survey the recent developments in MARL algo-select actions via maximization; Policy-based methods \(e.g., rithms, discussing their diverse applications in aspects of DDPG\): optimize a parameterized policy πθ directly using CAV control based on the extent of control dimensions. 

gradient ascent; Actor-critic methods \(e.g., Advantage Actor-Furthermore, we provide an extensive examination of Critic \(A2C\) \[35\]\): combine policy and value function learning the leading simulation platforms employed in MARL

to improve stability and reduce variance. 

research for CAV control. 

In multi-agent settings such as CAV control, MARL extends 2\) We highlight and explore the technical challenges that the RL paradigm to systems where multiple agents interact MARL faces in these applications and discuss potential and jointly influence outcomes \[36\]. Agents are modeled as research directions to address these challenges. 

nodes in a communication graph G = \(ν, ε\) and operate under 3\) The work, including a well-classified list of relevant decentralized and partially observable conditions, typically papers, has been presented at the following site: https://

formalized as a partially observable MDP \(POMDP\). 

github.com/huahuaedi/MARL in CAV control review. 

This paper is organized as follows: Section II introduces B. Training and Execution Strategies in MARL

the basics of RL and MARL; A detailed review of MARL

In MARL settings, different approaches and frameworks applied in CAV control from different control dimensions are employed to tackle the complex challenges of coor-and mainstream simulation platforms are described in section dinating and training agents in decentralized environments. 

III. Section IV summarizes the remaining challenges and This subsection explores two fundamental paradigms: Cen-opportunities. Finally, Section V concludes the review. 

tralized Training with Decentralized Execution \(CTDE\) and Decentralized Training with Decentralized Execution \(DTDE\), II. METHODOLOGIES

each offering distinct insights and trade-offs in the pursuit of In this section, we begin with a comprehensive overview effective multi-agent learning \[37\], \[38\], \[39\]. 

of the fundamental principles of RL. We then delve into 1\) Centralized Training With Decentralized Execution various prominent MARL algorithms, establishing the context \(CTDE\): In this framework, the decentralized problem is to enhance the understanding of our review. 

initially transformed into a centralized one, solvable by a central controller, which gathers essential training information, A. Preliminaries of RL and MARL

e.g., observation, reward, and global state information, for the RL, typically formalized as a Markov Decision Process training process. Following this data collection, the centralized \(MDP\), provides a framework for sequential decision-making value functions are learned based on the information of all under uncertainty \[34\]. An agent interacts with the environ-agents, and then the gradient from the centralized value ment by taking actions and receiving rewards, aiming to learn function is used to train the policy of each agent. But in the an optimal policy that maximizes cumulative rewards. The process of execution, each agent outputs action according to MDP is defined as M = \(S, A, P, R\), where S is the state its individual observation \(see Fig. 2\). 

space, A the action space, P the transition probability, and R

It is important to acknowledge the inherent trade-offs of the reward function. 

the CTDE. One significant strength is the enhanced learning





HUA et al.: MARL FOR CAVs CONTROL: RECENT ADVANCEMENTS AND FUTURE PROSPECTS

16269

the environment. A key challenge in DTDE is maintaining learning stability due to non-stationarity, as agents’ policies evolve independently over time. Traditional independent Q-learning \(IQL\) \[44\] and independent advantage actor-critic \(IA2C\) \[45\] are widely used but often struggle with convergence due to the lack of inter-agent coordination \[46\]. To mitigate non-stationarity, Zhang et al. proposed a fully decentralized MARL framework, where agents exchange messages with neighboring agents, improving coordination and offering theoretical convergence guarantees \[47\]. Fig. 3 illustrates the DTDE framework based on the actor-critic architecture, where each agent independently updates its policy and critic function based on local interactions with the environment. 

Fig. 2. 

Illustration of centralized training with decentralized execution 3\) Offline Reinforcement Learning: Beyond CTDE and \(CTDE\) in MARL. 

DTDE, Offline RL provides an alternative learning paradigm that relies exclusively on pre-collected datasets, eliminating the need for continuous environment interaction during training. 

Unlike traditional online RL, which explores and updates policies dynamically, Offline RL learns solely from fixed datasets, making it particularly useful in scenarios where real-time exploration is expensive, unsafe, or impractical \[48\]. However, a major challenge in Offline RL is the issue of distributional shift, when the learned policy encounters states or actions that are insufficiently represented in the dataset, leading to suboptimal or unsafe decision-making. To address this, various techniques, such as policy regularization \[49\], conservative Q-learning \[50\], and behavior cloning \[51\], have been proposed to improve policy robustness and generalization. Given its potential for leveraging large-scale offline data, Offline RL

Fig. 3. 

Illustration of decentralized training with decentralized execution continues to be an active research area with broad applications \(DTDE\) in MARL. 

across different domains. 

stability enabled by centralized training, which can result C. MARL Algorithm Variants

in more robust policies \[40\]. However, it is crucial to rec-ognize that maintaining a centralized controller comes with In this subsection, we have exclusively reviewed the com-its own set of challenges. Firstly, it can be prohibitively mon MARL algorithms that find utility in CAV applications. 

expensive and infeasible in certain scenarios, particularly in Further, the MARL algorithms are divided into four categories: large-scale or resource-constrained environments. For exam-value function decomposition, learning to communicate, hier-ple, in large-scale CAV networks such as urban traffic control archical structure, and causal inference, which are rooted in

\[41\] or highway platooning \[42\], maintaining a centralized the inherent complexity and diverse requirements of multi-critic requires high bandwidth and computational resources, agent environments, particularly in CAV control. Table I

making real-time learning impractical. Similarly, resource offers an extensive overview of key works from four distinct constraints in edge-computing environments limit the fea-perspectives within various settings. 

sibility of processing global information centrally, favoring 1\) Value Function Decomposition: The challenge of credit decentralized approaches \[43\]. Additionally, the centralized assignment in cooperative settings has emerged as a significant controller introduces privacy concerns, as it necessitates the area of research interest. The shared rewards in a fully sharing of sensitive information among agents. Moreover, the cooperative environment make it difficult to distinguish the central controller becomes a single point of failure, rendering contribution of each agent, some agents tend to be lazy \[72\]. 

the whole system vulnerable to disruptions. These trade-offs To solve the above problem, some studies learn different value highlight the need for careful consideration of the CTDE

functions to distinguish the contribution of each agent. Foerster framework’s suitability in specific MARL applications, taking et al. \[73\] and Guo et al. \[74\] introduced the counterfactual into account the advantages and drawbacks it presents. 

baseline principle to learn different value functions by central-2\) Decentralized Training With Decentralized Execution ized learning method in the context of a shared team reward \(DTDE\): In DTDE, each agent learns and acts independently, environment. Additionally, Hou et al. have developed a credit relying solely on local observations and policy updates without allocation mechanism based on role attention, which facilitates a central controller. Unlike centralized or partially centralized the learning process of role policies in multi-agent systems frameworks, DTDE agents do not require global state informa-by managing how credit is allocated among agents \[75\]. Liu tion but instead learn through trial-and-error interactions with et al. construct the causal effect of the agent’s actions on the

16270

IEEE TRANSACTIONS ON AUTOMATION SCIENCE AND ENGINEERING, VOL. 22, 2025

TABLE I

AN OVERVIEW OF THE PRIMARY WORKS FOR MARL ALGORITHMS

external state from the perspective of a causal diagram, solving by sharing low-dimensional policy fingerprints among agents. 

the problem of lazy agents \[70\]. 

DIAL \[80\] enables differentiable communication by having Among the above methods to solve credit assignment, DQN-based agents simultaneously generate and process mes-value function decomposition has remained a key approach sages via backpropagation. Further advancements have sought for addressing credit assignment challenges in cooperative to optimize communication efficiency and reduce redundant MARL by decomposing the joint value function into indi-message exchange. NeurComm \[58\] proposes that encoding vidual components. Building upon foundational methods like and concatenating communication signals, rather than simply VDN \[76\] and QMIX \[77\], several advanced algorithms aggregating them, effectively mitigates information loss and have been developed to tackle increasingly complex sce-enhances coordination among agents. This approach allows narios. For instance, the Value Decomposition with Graph for structured message processing, improving decision-making Attention Networks \(VGN\) method employs graph attention in dynamic environments. Similarly, IMAC \[59\] formulates networks to dynamically model agent relationships, improving an efficient communication protocol based on the information coordination in cooperative tasks \[55\]. Similarly, the MA-bottleneck principle, ensuring that agents only transmit the MIX algorithm integrates a multi-head attention mechanism to most relevant information to their peers. The framework devel-enhance information exchange and cooperation among agents ops a differentiable communication strategy, incorporating

\[57\]. These advancements underscore the ongoing evolution state, policy, and encoded neighboring information, which is of value function decomposition techniques, further improving then concatenated into the state space of nearby agents. 

agent coordination, communication efficiency, and adaptability More recent works have further expanded communication in increasingly complex environments. 

capabilities to improve interpretability, adaptivity, and robust-2\) Learning to Communicate: Research in MARL can be ness in MARL. Verco \[60\] integrates large language models categorized into two distinct groups according to their methods \(LLMs\) into MARL agents, enabling human-readable verbal of communication \[58\]. The first group operates without com-communication that enhances coordination and transparency. 

munication among agents and centers its efforts on stabilizing Meanwhile, AsynCoMARL \[61\] introduces graph transformer-training by employing advanced value estimation methods. For based learning to dynamically adjust communication protocols example, MADDPG \[78\] extends DDPG to the MARL setting in real time. By leveraging dynamic graph structures, agents by employing a centralized critic network to enable the global can learn when and how to communicate, ensuring scalable value estimate. Similarly, COMA \[73\] modifies the actor-critic and adaptive multi-agent cooperation. These developments method for use in MARL, calculating the advantage function mark a shift towards structured, efficient, and learnable comfor each agent by employing a centralized critic in conjunction munication mechanisms. Instead of relying on predefined with a counterfactual baseline. The second group investigates message-passing rules, modern approaches prioritize adaptive explicit communication mechanisms, which can be predefined protocols, minimal yet effective communication, and scalable heuristic protocols or learnable communication strategies. Fin-coordination strategies, improving MARL performance in gerPrint \[79\] stabilizes learning under non-stationary policies complex, multi-agent environments. 

HUA et al.: MARL FOR CAVs CONTROL: RECENT ADVANCEMENTS AND FUTURE PROSPECTS

16271

3\) Hierarchical Structure: In MARL, hierarchical struc-by counterfactual reasoning \[88\]. Pina et al proposed the tures play a crucial role in addressing challenges such as sparse independent causal learning \(ICL\) algorithm to evaluate the rewards, complex decision-making, and limited transferability. 

causal effect of each agent’s observations on team collabora-Hierarchical MARL enables agents to learn decision-making tion performance and solve the credit allocation problem in strategies across different levels of temporal abstraction, mak-the independent learning framework \[69\]. 

ing it particularly beneficial for large-scale coordination tasks. 

There are also other works that combine causal inference Existing hierarchical MARL methods can be broadly catego-from different perspectives under the framework of MARL. 

rized into option-based hierarchies \[81\], \[82\] and goal-based LAIES mathematically define the concept of fully lazy agents hierarchies \[83\], \[84\], both of which have been successfully and teams by calculating the causal effect of their actions on applied to multi-agent cooperation. 

external states using the do-calculus process, which solved Several hierarchical MARL frameworks have been intro-the sparse reward problem in MARL \[70\]. FD-MARL allows duced to enhance scalability, coordination, and efficiency. 

agents to modify communication messages by choosing the Hierarchical Skill Discovery \(HSD\) trains decentralized counterfactual that bears the most significant influence on policies for high-level skill selection while simultaneously others, the continuous communication based on causal analysis learning low-level execution policies, improving adaptability enables efficient information transformation in a fully decen-in dynamic environments \[62\]. Role-based Decomposition tralized manner \[67\]. The deconfounded value decomposition \(RODE\) further refines action space partitioning through \(DVD\) method investigates value function decomposition from action clustering, ensuring that each action corresponds to the perspective of causal inference, which cuts off the back-a distinct subspace, thereby reducing the need for extensive door confounding path from the global state to the joint parameter tuning \[63\]. Hierarchical Multi-Agent Reinforce-value function \[68\]. Additionally, deep motor system \[71\]

ment Learning with PER-QMIX \(H-MARL-PQ\) combines introduces individual intention inference and causal reasoning multi-agent and single-agent RL through a hierarchical frame-to enable fully decentralized coordination, allowing agents to work, integrating macro-operations and prioritized experience disentangle other agents from their environment and improve replay to accelerate learning in complex wargames with sparse cooperative behavior without relying on CTDE. Causal infer-rewards \[64\]. To further improve hierarchical coordination, ence has also applied to some practical application scenarios, HierArchical Value dEcompositioN \(HAVEN\) introduces a such as traffic signal control \[89\] and human-computer inter-dual-coordination mechanism that operates both within hierar-action decision-making \[90\]. 

chical layers and across agents, optimizing strategy execution at multiple levels and enhancing policy stability \[65\]. Mean-III. TOWARDS APPLICATIONS OF MARL IN CAV

while, Hierarchical Multi-Agent Skill Discovery \(HMASD\) CONTROL

employs a transformer-based structure for sequential skill assignment, allowing low-level policies to autonomously dis-CAV control has obtained substantial interest for its abil-cover and refine agent-specific skills, enhancing flexibility in ity to reshape modern transportation, enhancing efficiency, cooperative decision-making \[66\]. 

safety, and sustainability. CAVs interact with multiple agents, Despite these advancements, hierarchical MARL faces enabling cooperative driving strategies such as platooning, key challenges in designing dynamic hierarchical structures. 

merging, and intersection navigation, which collectively opti-Unlike static hierarchies with predefined roles, dynamic struc-mize traffic flow and reduce congestion \[102\]. As CAV

tures evolve based on task complexity, agent interactions, and technology advances, the integration of MARL has become environmental changes, enabling adaptive role assignment, increasingly important, allowing vehicles to develop adaptive, flexible coordination, and scalable policy learning \[85\]. The cooperative policies for dynamic traffic scenarios. 

primary challenges lie in optimizing inter-level coordination, To systematically explore how MARL contributes to CAV

ensuring efficient policy transfer, and balancing local and control, we categorize cooperative driving tasks based on the global decision-making. Addressing these issues is crucial extent of required coordination, forming a taxonomy aligned for improving MARL adaptability in large-scale, complex with fundamental principles of CAV control. Coordination environments. 

in CAV environments typically involves three key factors: 4\) Causal Inference: There are multiple complex variables longitudinal control, lateral control, and timing constraints. 

in MARL, and it is usually difficult to directly discover their These aspects define the complexity of interaction, shaping internal relationships. Therefore, some recent research has how vehicles learn and adapt to shared environments. There-begun to combine MARL with causal inference to discover fore, we define three levels of cooperation complexity in the causal relationships between agents or variables, and MARL-driven CAV control. 

further understand the operating mechanism of agents through

• One-dimensional cooperation focuses on longitudinal intervention and inference, thereby motivating the agent to control, where vehicles primarily regulate speed and fol-conduct more targeted learning \[86\]. Pearl’s three-level causal lowing distances, as seen in car-following and platooning model is considered a powerful tool for constructing causal tasks. 

relationships between variables \[87\]. Causal influence reward

• Two-dimensional cooperation extends this by introduc-methods promote the collaborative performance of agents by ing lateral control, requiring inter-agent negotiation for rewarding those agents that have a causal influence on the lane changes, merging, and overtaking, which increases actions of other agents, where this causal influence is evaluated the complexity of coordination. 



16272

IEEE TRANSACTIONS ON AUTOMATION SCIENCE AND ENGINEERING, VOL. 22, 2025

TABLE II

AN OVERVIEW OF THE PRIMARY WORKS FROM 1-D AND 2-D COOPERATION FOR MARL APPLIED IN CAV CONTROL

• Three-dimensional cooperation incorporates time constraints, encompassing tasks such as traffic signal coordination, intersection management, and on-ramp merging, where spatial and temporal synchronization becomes essential. 

We categorize MARL advancements by control components and review key simulation platforms for CAV applications, with a focus on cooperative control. 

A. One-Dimensional Cooperation

Fig. 4. One-dimensional cooperation scenarios: the case of platooning control. 

In this subsection, we provide a detailed review of one-dimensional cooperation applications, primarily focusing on longitudinal control. A key example is platooning control, communication channels. This setup aims to ensure safe, fuel-where CAVs operate in tightly coordinated formations to efficient, and smooth vehicle following operations, while also improve efficiency, safety, and fuel economy. By minimizing maximizing the advantages of driving in close formation \[103\]. 

aerodynamic drag and optimizing traffic flow through syn-Given N vehicles in a platoon, the control objective is to chronized control and inter-vehicle coordination, platooning maintain a desired spacing Li and ensure velocity matching. 

exemplifies how MARL enhances the capabilities of CAVs. 

The state vector for each vehicle i at time t is: 1\) Application Scenarios: As shown in Fig. 4, the problem of platooning control is commonly addressed through a model-0 1 

## 0 

free, multi-agent network approach \[58\]. In this framework, 

˙xi\(t\) =

x

k

## 0 0

i\(t\) \+

1

p \(\(xi−1\(t\) − xi\(t\)\) − Li\)

each agent, symbolizing an AV, has the ability to communicate with both preceding and following vehicles via V2V

\+kd \(vi−1\(t\) − vi\(t\)\)\)

\(1\)

HUA et al.: MARL FOR CAVs CONTROL: RECENT ADVANCEMENTS AND FUTURE PROSPECTS

16273

where xi\(t\) is the position of the ith vehicle at time t, vi\(t\) is Additionally, Relative Position Encoding Multi-Actor Atten-the velocity of the ith vehicle at time t, Li is the desired inter-tion Critic \(RPE-MAAC\) \[96\] introduces relative position vehicle distance \(spacing\) between vehicle i and i \+ 1, xi\(t\) =

encoding to enhance spatial awareness and cooperative control

\[xi\(t\), vi\(t\)\]T is the state vector, kp and kd are the proportional in mixed CAV-HDV platoons. Integrated with the Intelligent gain for position error and the derivative gain for velocity Driver Model-Informer \(IDM-Informer\), RPE-MAAC gener-error respectively. To optimize the platoon control, an objective ates realistic HDV trajectories, mitigating error propagation function J can be defined, incorporating both spacing error and while improving fuel consumption, stability, and overall traffic velocity error over a time horizon T:

throughput. In vehicular environments characterized by high N

mobility, the use of traditional centralized optimization meth-Z

T

X

J =

αe2 \(t\) \+ βe2 \(t\) dt

\(2\)

ods that rely on global channel information can be impractical. 

x,i

v,i

i=1

0

In \[108\], the authors model each CAV as an individual where α and β are weighting factors that balance the impor-agent, which makes decisions based on local information and tance of position and velocity errors. Thus, cooperative communication with neighboring vehicles, without relying on strategies would be developed to achieve the collective goal, a centralized controller. 

adapting their behaviors in response to the actions of other 2\) Optimization Goals: One critical goal of platooning vehicles within the network. 

control is to achieve string stability, which refers to the Mixed platooning control refers to scenarios where mul-ability of a line of CAVs to maintain a stable and orderly tiple vehicle platoons coexist within a network, requiring formation \(e.g., stable distance and speed\) as they travel in sophisticated coordination and communication both within close proximity to each other \[109\]. Notably, MARL has \(intra-platoon\) and between \(inter-platoon\) these formations been proposed to address and enhance the achievement of

\[104\]. To address these challenges, Parvini et al. introduced string stability in the platooning control scenario, contributing two advanced MARL-based algorithms specifically designed to the development of more efficient and coordinated pla-for mixed platooning control. One of these, Modified MAD-tooning control strategies. For instance, in \[110\], a MARL

DPG, along with its task decomposition variant, improves approach based on a robust communication protocol with Long resource allocation in platoon-based cellular V2X \(C-V2X\) Short-Term Memory \(LSTM\) \[111\] is introduced, resulting in networks. By employing task-wise value function decom-stable platooning control. In addition, Li et al. introduce the position and adaptive agent-specific policies, this method Communication Proximal Policy Optimization \(CommPPO\) effectively reduces communication latency and optimizes algorithm to enhance stability, which adapts to varying agent network throughput, leading to more efficient vehicular coor-numbers and supports different dynamics of platooning control dination \[94\]. In these frameworks, platoon leaders function

\[112\]. CommPPO incorporates a predecessor-leader-follower as independent agents that interact with the environment to communication protocol to facilitate the transmission of both determine optimal policies for platoon management. These global and local state information among agents. Notably, algorithms leverage multiple critics to estimate both global and CommPPO introduces a novel reward communication channel, local rewards, fostering cooperative behavior among agents. 

effectively mitigating issues related to spurious rewards and Additionally, the task decomposition variant further refines mitigating the problem of “lazy agents”, which are com-individual reward structures, breaking them down into task-monly encountered in other MARL approaches. Similarly, specific sub-reward functions to enhance coordination and Multi-Agent Reinforcement Learning with Proximal Policy policy learning, as demonstrated in \[94\]. 

Optimization \(MARL-PPO\) \[95\] enhances highway platoon-Even though CAVs have made significant advancements, ing stability through decentralized learning and an adaptive there will be an extended period during which CAVs will reward mechanism, dynamically adjusting inter-vehicle dis-coexist with human-driven vehicles \(HDVs\), a situation com-tances based on velocity and lane positioning to improve monly referred to as mixed-traffic scenarios \[45\]. Different safety, traffic efficiency, and merging success rates in dynamic penetration rates can be assessed to understand the impact traffic conditions. In \[58\], the platooning control problem is of mixed traffic. In the study presented in \[105\], the impact formulated as a spatiotemporal MDP. They enhance system of the penetration rate of CAVs on the energy efficiency of stability by introducing a spatial discount factor for local the traffic network is examined, with a specific emphasis agents. 

on a cooperative eco-driving system that utilizes longitudinal Efficient communication among CAVs in platooning con-control. Lu et al. enhance the evaluation by integrating several trol also poses a fundamental task in achieving seamless key elements, including altruism control, a quantitative car-coordination and maintaining the desired following proper-following strategy, a refined platoon reward function, and a ties, such as precise inter-vehicle spacing and synchronized collision avoidance method, as outlined in their work \[106\]. 

maneuvers. For instance, Liu et al. introduce a Multi-Agent In \[93\], the authors introduce the concept of characteriz-Hierarchical Attention RL \(MAHARL\) framework, which ing consecutive HDVs as a collective entity, referred to leverages hierarchical Graph Attention Networks to model as AHDV, to minimize stochastic variability and leverage inter-agent influence and enhance long-term decision-making macroscopic characteristics for the control of following CAVs. 

without immediate rewards \[91\]. Additionally, in scenarios They employ a control strategy built on distributed proximal where complete information is lacking, Li et al. \[92\] develop a policy optimization \(DPPO\) \[107\] to anticipate disturbances game-theoretic framework to capture the strategic interactions and downstream traffic conditions in mixed traffic scenarios. 

between the leading vehicle and the following vehicles. To



16274

IEEE TRANSACTIONS ON AUTOMATION SCIENCE AND ENGINEERING, VOL. 22, 2025

And the constraints are expressed as:

xi−1\(t\) − xi\(t\) ≥ Li \+ ∆xsafe

xi\(t\) − xi\+1\(t\) ≥ Li\+1 \+ ∆xsafe

yi\(t\) ∈ \{current lane, target lane\}

0 ≤ yi\(t\) ≤ wlane

\(5\)

Hou et al. devise a decentralized cooperative lane-changing controller employing a multi-agent Proximal Policy Optimization \(MAPPO\) \[115\] approach, which empowers each vehicle to independently learn and assess its policy and action rewards Fig. 5. Two-dimensional cooperation scenario. 

based on local information, while still having access to global state data. The trained policies can be effectively transferred overcome the absence of full information, the equilibrium and applied across various traffic conditions, achieving a solution in platooning control is identified through backward safe, efficient, and comfortable lane-change maneuver \[116\]. 

induction, coupled with information collection from the fol-Dubey et al. \[29\] introduce FAIRLANE, a MARL-based lowing vehicles. 

framework designed to manage priority lanes in mixed-autonomy traffic. By utilizing multi-policy bootstrapping and decentralized decision-making, the framework dynamically B. Two-Dimensional Cooperation

optimizes lane allocation to enhance traffic efficiency, safety, Compared

to

one-dimensional

cooperation, 

two-

and fairness. This method ensures equitable access to priority dimensional

cooperation

addresses

problems

related

to

lanes while adapting to real-time traffic conditions. Zhang both longitudinal and lateral control, with its most typical et al. \[101\] propose a Multi-Agent Reinforcement Learning application being cooperative lane changing. 

\(MARL\) framework that incorporates a Prioritized Action 1\) Application Scenarios: As shown in Fig. 5, CAVs Extrapolation \(PAE\) mechanism. This approach dynamically communicate and coordinate through V2V and V2I communi-updates lane-changing decision priorities, enabling smoother cation channels, enabling them to make decisions and acquire coordination, improved safety, and faster policy convergence effective lane-changing strategies within shared driving envi-in high-density traffic scenarios. 

ronments \[113\]. Generally, the lane-changing mathematical In \[97\], the authors put forth a multi-vehicle coopera-problem \[114\] can be expressed as follows: tive driving approach, leveraging the QMIX algorithm. Their method applies RL to dynamically adapt to changing con-Z

t f 



ditions on highways, aiming to find an optimal balance min J =

α1 \(xi−1\(t\) − xi\(t\) − Li − ∆xsafe\)2

u

between autonomous decision-making and cooperative interac-i \(t\)

t0

tion among the vehicles. This algorithm allows each vehicle in

\+ x

## 2 

i\(t\) − xi\+1\(t\) − Li\+1 − ∆xsafe

\+ α2 t f − t0

the pair to independently perform lane changes and overtaking 2



d

maneuvers, even in dense traffic scenarios, while maintaining

\+ α3 ux,i\(t\)2 \+ uy,i\(t\)2 \+

ux,i\(t\)

dt

a predetermined formation between them. An enhanced QMIX

algorithm \[117\] is further proposed to enhance the flexibility d

2





\+

u

and effectiveness of the collaborative lane-changing system. 

y,i\(t\)

dt

\(3\)

dt

They implement a stable estimation method to mitigate the Subject to the vehicle dynamics:

problem of overestimated joint Q-values among agents. This approach strikes a fine balance between maintaining formation

˙xi\(t\) = Axi\(t\) \+ Bui\(t\)

\(4\)

and allowing for smooth overtaking, thus facilitating intelligent adaptation to a variety of scenarios, including heavy traffic, where α1, α2, and α3 are the corresponding weights for safety, light traffic, and emergencies. In an effort to enhance mobility efficiency, and comfort, respectively. Other objectives may within complex traffic environments, in \[118\], instead of 2 0 0 1 0 3

## 2 0 0 3

relying on relative distance and semantic maps, the authors 6 0 0 0 1 7

## 6 0 0 7

also be considered; A =

, 

suggest the utilization of traffic states that encapsulate the 6

7

B = 6

7, xi\(t\) =

4 0 0 0 0 5

## 4 1 0 5

spatio-temporal interactions between neighboring vehicles. 

0 0 0 0

## 0 1

Within the MADRL framework, three prediction models, xi\(t\), yi\(t\), vx,i\(t\), vy,i\(t\)T is the state vector for vehicle i; xi\(t\) namely the transformer-based \(TS-Transformer\), generative and yi\(t\) are the longitudinal and lateral position of the ith adversarial network-based \(TS-GAN\), and conditional varia-vehicle at time t; vx,i\(t\) and vy,i\(t\) are longitudinal and lateral tional autoencoder-based \(TS-CVAE\) models, are developed velocity of the ith vehicle at time t. ui\(t\) = ux,i\(t\), uy,i\(t\)T

and compared for traffic state prediction. 

is the control input vector for vehicle i, ux,i\(t\) and uy,i\(t\) 2\) Optimization Goals: Safety is of paramount importance are the control input for longitudinal and lateral acceleration in the context of CAV scenarios. In \[119\], the authors respectively; Li is the length of the ith vehicle; ∆xsafe is the have introduced a safety-enhancing actor-critic algorithm that safety distance to avoid collision; wlane is the width of the lane. 

incorporates two innovative techniques. The first technique is



HUA et al.: MARL FOR CAVs CONTROL: RECENT ADVANCEMENTS AND FUTURE PROSPECTS

16275

Fig. 6. Three-dimensional cooperation scenarios: \(a\) Traffic Signal Coordination; \(b\) Merging on-ramps;\(c\) Unsignalized intersections. 

the ‘truncated Q-function’, which effectively leverages shared design and parameter-sharing scheme for cooperative lane information from neighboring CAVs, ensuring scalability for changing in mixed traffic scenarios. They also present a multi-large-scale CAV systems. The second technique, “safe action objective reward function that considers factors such as fuel mapping”, provides safety guarantees throughout both the efficiency, driving comfort, and safety to facilitate successful training and execution phases by utilizing control barrier and efficient lane changing. In \[124\], a MARL approach is functions. Additionally, a bi-level strategy is proposed in \[98\]

explored in which agents collaborate to reach a zero-sum game to further enhance safety and efficiency. At the upper level, state. In contrast to cooperative driving, this approach, known the MADQN model is utilized for making decisions about as harmonious driving, places emphasis on achieving a bal-lane changes. This approach acknowledges the cooperative ance between overall and individual efficiency while utilizing aspect of driving by factoring in the intentions of surrounding limited sensing data from individual vehicles. They design a vehicles, enabling implicit negotiation for right-of-way. At the reward function that promotes harmony by considering both lower level, a right-of-way assignment model is utilized to individual and overall efficiency, as opposed to competitive ensure safety. A novel reward function is further proposed strategies that solely prioritize individual interests. 

to encourage coordination and account for traffic impact. 

Moreover, Li et al. have introduced MetaDrive, a platform that C. Three-Dimensional Cooperation

focuses on safe driving by addressing generalizability, safety Three-dimensional cooperation involves the intricate coor-awareness, and multi-agent decision-making. It offers diverse dination of longitudinal and lateral movements along with driving scenarios for benchmarking single and multi-agent RL

timing, across a variety of traffic scenarios such as traffic tasks \[120\]. 

signal coordination, on-ramp merging, and navigating through Graph neural networks \(GNNs\) \[121\] have gained sig-unsignalized intersections, as depicted in Fig. 6. To ensure nificant attention in MARL settings, particularly for traffic safe, efficient, and effective cooperation, CAVs need to rapidly flow optimization. Chen et al. introduce a novel algorithm learn longitudinal and lateral maneuvers within tight time based on MADQN, which combines a GCN with a deep Q-constraints. The three-dimensional cooperation problem can network \[122\]. This approach facilitates effective information also be described by Eq. 3–Eq. 5, with the added time fusion and decision-making within the MARL framework, constraints ti, start ≤ t ≤ ti, end . 

thereby enhancing both safety and traffic flow in various 1\) Traffic Signal Control \(TSC\): TSC plays a critical traffic scenarios. Moreover, in \[123\], the authors leverage role in shaping vehicle interactions by introducing time-GNN in conjunction with MADDPG in their work for based constraints at intersections \(see Fig. 6 \(a\)\). Traditional multi-agent training, addressing the complexity of real-world optimization-based TSC methods focus on traffic management, inputs and aiding in congestion mitigation efforts. Guo et adjusting signal timings to regulate flow, but they treat vehicles al. introduce deep Q-Network with Request-Respond Mechas passive entities responding to fixed control policies \[45\]. In anism \(DQNRR\), which enhances lane-changing coordination contrast, when considering MARL in CAV control, TSC is not through a request-respond mechanism. This method hierar-the primary research target but rather an external constraint chically structures lane-change decisions, allowing vehicles to that impacts how CAVs cooperate to navigate intersections negotiate merging and overtaking maneuvers more efficiently, efficiently. CAVs, unlike human-driven vehicles, can actively thus reducing computational complexity while improving lane-communicate and coordinate their movements under these changing efficiency in congested urban traffic \[100\]. 

constraints, optimizing their joint decision-making to minimize Thoughtful reward function design is paramount for the congestion, delays, and energy consumption. MARL provides adaptivity and efficiency of lane-changing strategies. In \[99\], 

a natural framework for CAVs to learn cooperative policies the authors introduce the multi-agent advantage actor-critic in response to signal timings, ensuring efficient merging, \(MA2C\) framework, which integrates a novel local reward gap acceptance, and right-of-way negotiation. The challenge

16276

IEEE TRANSACTIONS ON AUTOMATION SCIENCE AND ENGINEERING, VOL. 22, 2025

lies not in optimizing TSC itself but in understanding how structure fosters global coordination while ensuring the system CAVs interact under these time-dependent traffic conditions scalability. 

to improve overall system efficiency. TSC can be viewed as Efficient communication is crucial in applying MARL

a multi-objective optimization problem and Markov/Stochastic to TSC as it enables coordinated decision-making, optimal Games with cooperative settings, which require agents to coor-resource allocation, adaptation to dynamic environments, scal-dinate with each other. Therefore, the learning-based method ability, conflict resolution, and efficient learning, all of which can show better performance without prior knowledge about contribute to effective traffic management \[132\]. Liu et al. 

the given environment. In multi-agent-based algorithms, all present a novel algorithm that enhances communication effi-traffic light controllers within a traffic grid need to coordinate ciency through a new message exchange method and improves to address traffic congestion. 

congestion measurement by introducing a more comprehensive Value-based MARL algorithms have been extensively inves-reward calculation method. Then a clear and simple represen-tigated for TSC challenges. For instance, to alleviate the tation of traffic conditions is provided, and the synchronization curse of dimensionality and environmental nonstationarity between agents at different intersections with varying cycle problems, a decentralized coordination MADQN approach lengths needs to be addressed \[133\]. To incorporate spatial is proposed in \[125\] to explicitly identify and dynamically and temporal dependencies, Wang et al. introduce STMARL

adapt agent coordination needs during the learning process. 

\[134\], which models traffic lights using a traffic light adjacency Similarly, in \[126\], the complex TSC problem is decomposed graph and recurrent neural networks. This approach optimizes into simpler subproblems and tackled using multiple regional coordination across intersections by merging historical and agents and a centralized global agent. Each regional agent real-time traffic data. Recognizing the importance of shared learns its RL policy for smaller regions with reduced action information, Jiang et al. propose UniComm \[135\], which spaces, while the centralized global agent combines the RL

predicts the impact of local observations on neighboring contributions from various regional agents to form a final intersections, improving communication efficiency. 

Q-function for the entire large-scale traffic grid. Notably, Graph-based MARL provides advantages such as scalability, QMIX, an extension of VDN, was investigated in \[127\]

efficient message passing, global coordination, and adapt-for TSC, achieving promising results. Additionally, Liu et ability, making it particularly suitable for multi-agent traffic al. introduce a multi-agent dueling-double-deep Q network signal control \(TSC\) problems \[136\]. CoLight \[137\] intro-

\(MAD3QN\) for TSC \[128\]. This framework features an duces a graph-attentional MARL model that enables traffic innovative γ-reward design, which combines the traditional signals to communicate using temporal and spatial data from γ-reward with a novel γ-attention-reward. By employing a neighboring intersections. By achieving index-free modeling spatial differentiation method for agent coordination, their of intersections, it enhances adaptability and efficiency. Sim-approach enables decentralized control and decoupling of road ilarly, Yang et al. propose Inductive Heterogeneous Graph networks, enhancing scalability and convergence. In \[129\], 

Multi-agent Actor-Critic \(IHG-MA\) \[138\], which leverages an a cooperative group-based multi-agent Q-learning for ATSC

inductive heterogeneous graph neural network to encode traffic \(CGB-MATSC\) is proposed. This method enhances the learn-network structures and a multi-agent actor-critic framework ing process by incorporating a k-nearest-neighbor approach for for policy learning, allowing real-time adaptation to previ-state representation, a pheromone-based strategy for creating ously unseen intersections. Further enhancing MARL-based regional green-wave traffic flows, and a spatially discounted intersection control, Antonio et al. \[139\] integrate multi-agent reward system. 

TD3 with LSTM to manage varying observation sizes due to On the other hand, policy-based MARL algorithms have fluctuating vehicle numbers. Their method employs curriculum also been widely studied for TSC. In \[36\], a fully scalable and learning through self-play to optimize collaborative CAV con-decentralized Multi-Agent Actor-Critic \(MA2C\) algorithm is trol at intersections, improving traffic efficiency and safety. In introduced, which incorporates an advanced discount factor to contrast, Ren et al. highlight potential security vulnerabilities mitigate the effects of remote agents. This approach demon-in MARL-based traffic signal control by proposing a stealthy strates significant advantages over random and independent opaque-model attack strategy. Their method selectively per-controllers. Wu et al. introduced the multi-agent recurrent turbs critical states to increase congestion and delays while deep deterministic policy gradient \(MARDDPG\) algorithm, remaining undetectable, underscoring the need for robust secu-specifically designed for TSC in vehicular networks \[130\]. 

rity mechanisms in intelligent transportation systems \[140\]. 

They utilize a strategy of CTDE, enhancing the efficiency 2\) On-Ramps Merging: The on-ramp merging task requires of the training process through parameter sharing among CAVs to integrate into the main traffic flow while maintain-the actor networks. Furthermore, the integration of LSTM

ing safety and efficiency \(see Fig. 6 \(b\)\). This maneuver networks enables the algorithm to utilize historical data for involves both spatial and temporal coordination, as vehicles more effective control decisions. In \[131\], a MA2C approach must dynamically adjust their speeds and trajectories to avoid with a feudal hierarchy concept for TSC is presented. This conflicts. CAVs in the through lane proactively modify their approach segments the traffic network into several regions, velocities—either accelerating or decelerating—to create suf-each monitored by a manager agent, with traffic signal agents ficient gaps for merging vehicles. Meanwhile, CAVs on the acting as workers. The managers are responsible for high-level ramp must regulate their speeds and make timely lane-change coordination and setting objectives for the workers, who then decisions to merge smoothly without causing congestion. 

adjust traffic signals to meet these objectives. This hierarchical The success of this process depends on precise multi-agent

HUA et al.: MARL FOR CAVs CONTROL: RECENT ADVANCEMENTS AND FUTURE PROSPECTS

16277

TABLE III

AN OVERVIEW OF THE PRIMARY WORKS FROM FOUR PERSPECTIVES IN DIFFERENT SETTINGS

coordination, where vehicles anticipate and adapt to each improvement is contingent on the optimality of the traffic other’s actions, ensuring safe and efficient merging under real-vehicle’s behavior in the target lane. Zhou et al. introduce time traffic constraints \[141\]. 

a cooperative merging control strategy for CAVs using a In \[142\], a simplified mathematical formulation for an distributed MADDPG approach, which accounts for safe on-ramp merging scenario is presented to model the funda-merging distances, acceleration limits, and factors like rear-mental interactions and solved with a MADQN algorithm end safety, lateral safety, and energy consumption \[143\]. To that accounts for the interaction between an on-ramp merging address the challenge of a dynamic environment resulting vehicle and a traffic vehicle in the target lane. The results from the decentralized learning of CAVs, a decentralized indicate that a multi-agent approach can result in reduced framework employing MADDPG is presented to coordinate collision rates compared to a single-agent approach, but this CAVs during highway merging \[144\]. This framework enables

16278

IEEE TRANSACTIONS ON AUTOMATION SCIENCE AND ENGINEERING, VOL. 22, 2025

policies learned from a small group of trained CAVs to be Spatharis et al. propose a multi-agent double DQN frame-transferred and applied to any number of CAVs, with a reward work for unsignalized intersections, integrating an efficient function that promotes high-speed travel, resulting in smoother reward function to balance safety and traffic efficiency while traffic flow while maintaining safety in terms of rear-end and enabling transfer learning for adaptability \[19\]. Capasso et lateral collisions. 

al. develop a MAD-A3C model using model-free DRL to Some studies also examine the influence of human predict vehicle actions, allowing CAVs to autonomously learn drivers in on-ramp merging scenarios emphasizing adaptive intersection navigation while ensuring safety \[150\]. Yan et decision-making and cooperative control between connected al. introduce a DQN-based policy decomposition strategy and automated vehicles \(CAVs\) and human-driven vehicles for decentralized CAV coordination, achieving near-optimal \(HDVs\). Hu et al. propose Interaction-aware Decision-making throughput without reward shaping and demonstrating strong with Adaptive Strategies \(IDAS\), which leverages a modified generalizability across traffic conditions \[151\]. 

Multi-Agent Advantage Actor-Critic \(MA2C\) method and Effective coordination among CAVs is essential to ensure curriculum learning to train AVs to adapt to varying driver safe and efficient maneuvers at unsignalized intersections. In behaviors by assessing their level of cooperativeness \[145\]. 

\[152\], a decentralized MADQN algorithm is adopted and Similarly, Chen et al. introduce a multi-agent cooperative learned to make decisions for CAVs. To enable effective merging framework using MA2C, enabling CAVs on both coordination among agents, the intent trajectories of other the merge and through lanes to jointly develop policies that neighboring agents are incorporated into each agent’s state optimize traffic flow and adapt to HDV dynamics \[30\]. Their space. Furthermore, a decentralized and conflict-free coordina-framework ensures scalability in dynamic traffic scenarios tion scheme designed for CAVs at unsignalized intersections is through parameter sharing, local rewards, and action mask-proposed in \[153\], with the objective of enhancing intersection ing, promoting inter-agent cooperation while incorporating a management precision. They frame the challenge of safely priority-based safety supervisor to reduce collision risks and guiding multiple vehicles through unsignalized intersections accelerate learning. 

as a partially observable stochastic game \(POSG\). To facilitate Beyond RL approaches, game-theoretic strategies have also collaborative decision-making in a distributed fashion, they been explored to enhance safety. Chandra et al. propose introduce a cooperative multi-agent proximal optimization GAMEPLAN, a game-theoretic multi-agent planning approach algorithm \(CMAPPO\). In \[154\], a multi-layer coordination that integrates both CAVs and human drivers in merging strategy is proposed for the management of unsignalized scenarios \[146\]. This method utilizes game theory and an intersections. This architecture comprises two layers: a low-auction-based mechanism to compute optimal driving actions level layer that employs a dynamics-based algorithm to control while inferring driving styles from sensor data. By assigning individual CAVs, and a high-level layer that integrates a priority based on driver aggressiveness or patience, GAME-TD3 algorithm, trained in a centralized manner but executed PLAN optimally balances safety and efficiency, preventing in a decentralized fashion by multiple agents for decision-both collisions and deadlocks. 

making. Their findings reveal a successful training process, To tackle the complexities of multilane on-ramp merging, with the MATD3 algorithm achieving a remarkable 100%

Liu et al. introduce Graph Convolutional Proximal Policy success rate in preventing intersection collisions. Addressing Optimization \(GCAV-CPO\), a graph-based MARL framework adjacent intersection coordination, Xu et al. propose a multi-that integrates vehicle graph structures with an eco-friendly agent deep reinforcement learning scheduling \(MA-DRLS\) Markov decision process to enhance coordination, safety, algorithm, allowing each intersection agent to independently and energy efficiency in mixed-autonomy traffic \[20\]. Their optimize traffic scheduling via information exchange, using approach generalizes well across varying traffic densities and DQN networks for stable training \[155\]. Additionally, Tal-CAV penetration rates, demonstrating superior performance lapragada et al. introduce a multi-agent joint-action DDPG

over existing baselines. 

\(MAJA-DDPG\), a framework integrating RL with sequential optimization. It first learns a shared policy for determin-3\) Unsignalized Intersections: Intersections serve as pivotal ing vehicle crossing orders based on traffic states, followed nodes in urban road networks but can also become major by trajectory optimization, ensuring scalable and distributed bottlenecks if not managed efficiently. However, managing coordination \[156\]. 

vehicular interactions in the absence of traffic signals, as To enhance coordination in bandwidth-constrained multi-illustrated in Fig. 6 \(b\), introduces significant challenges due agent settings, Li et al. introduce the Efficient Communication to the need for decentralized decision-making, right-of-way Method \(ECM\)-MA2C algorithm \[157\]. By integrating a negotiation, and collision avoidance \[19\]. Unlike TSC, where variational auto-encoder with a multi-head attention mech-vehicles follow fixed timing rules, unsignalized intersections anism, ECM-MA2C selectively extracts and retains critical require real-time adaptive cooperation among multiple CAVs. 

information from neighboring agents, thereby optimizing com-Many conventional approaches, such as rule-based \[148\], 

munication efficiency. Experimental results demonstrate that planning-based \[149\], and single-agent RL methods \[147\], 

this approach significantly outperforms baseline methods, often treat intersection management as a single-agent problem, ensuring effective coordination with minimal communication which can not capture the complex interactions among CAVs. 

overhead. While ECM-MA2C focuses on efficient information Recently, MARL has emerged as a promising and effective sharing, Guo et al. \[158\] tackle decision-making challenges at tool for managing traffic at unsignalized intersections. 

unsignalized intersections using a value decomposition-based





HUA et al.: MARL FOR CAVs CONTROL: RECENT ADVANCEMENTS AND FUTURE PROSPECTS

16279

Fig. 7. Representative scenarios in different simulators: \(a\) SUMO \[159\]; \(b\) CityFlow \[160\]; \(c\) SMARTS \[161\]; \(d\) MetaDrive \[120\]; \(e\) CARLA \[162\]; 

\(f\) MACAD \[163\]. 

MARL framework, QMIX. Their enhanced QMIX implemen-SUMO \(Simulation of Urban MObility\) is an opentation introduces network-level optimizations, TD updates with source, large-scale traffic simulator widely used for studying discount factor γ, and reward clipping techniques, all of which platooning \(1D\), lane coordination \(2D\), and traffic flow opti-contribute to improved learning stability and more reliable mization \(3D\) \[159\]. It supports customizable road networks, cooperative control. To further improve learning efficiency real-time traffic data integration, and reinforcement learning in complex intersection scenarios, Spatharis et al. \[19\] pro-experiments, making it a versatile tool for evaluating CAV

posed a Route-Agent Cooperative Multi-Agent Reinforcement interactions. 

Learning \(RA-CoMARL\) framework for autonomous driving CityFlow is a high-performance traffic simulator designed at unsignalized intersections, which introduces route agents as for large-scale, city-wide coordination \[160\]. With its efficient a scalable decision-making structure and a collision prediction data structures and multi-agent RL compatibility, it excels in mechanism to enhance traffic coordination, reduce congestion, optimizing TSC \(3D\) and large-scale intersection coordination and improve safety. Building upon these advancements, Liu while maintaining computational efficiency. 

et al. \[18\] introduce the Multi-Agent Game-prior Attention SMARTS \(Scalable Multi-Agent RL Training School\) is a DDPG \(MA-GA-DDPG\) algorithm. This framework integrates multi-agent RL platform tailored for cooperative CAV learn-an attention mechanism to capture inter-vehicle dependencies ing \[161\]. It provides realistic traffic behaviors, customizable while incorporating a hierarchical game-theoretic structure to scenarios, and benchmark tasks, making it ideal for studying enhance safety, efficiency, and learning stability. By leveraging CAV interactions at intersections \(3D\) and lane coordination these mechanisms, MA-GA-DDPG ensures robust and scal-

\(2D\) under mixed-traffic conditions. 

able cooperative decision-making for CAVs at unsignalized MetaDrive offers infinite procedurally generated driving intersections, paving the way for more adaptive and resilient environments, balancing realism with efficiency \[120\]. It is intersection management strategies. 

particularly well-suited for studying generalizable RL in highway merging \(2D\) and intersection scenarios \(3D\) while maintaining lightweight computational requirements. 

D. Simulation Platforms

CARLA, is a high-fidelity 3D driving simulator with realis-The simulation platforms, which act as the training/learning tic physics and sensor modeling, enabling MARL research in environments, play an important role in the performance and complex urban settings \[162\]. It supports CAV coordination adaptability of the autonomous agents. The learning platforms under dynamic environments, making it ideal for advanced provide different challenges for CAV control by considering intersection management \(3D\) and adaptive lane merging \(2D\). 

different traffic scenarios and different characters of agents MACAD \(Multi-Agent Connected and Autonomous Driv-

\(Fig. 7\). The traffic ecosystem/simulation platform incorpo-ing\) provides a multi-agent RL testbed for CAVs based on rates realistic models, physics-based simulations, and efficient partially observable Markov games \[163\]. It supports cooper-numerical solvers, providing a controllable environment to ative intersection navigation \(3D\) and deep RL-based vehicle accelerate the development of CAVs \[164\]. Comparisons of interaction studies, making it a valuable tool for high-level different simulation platforms for CAVs are shown in Table IV. 

CAV coordination research. 

16280

IEEE TRANSACTIONS ON AUTOMATION SCIENCE AND ENGINEERING, VOL. 22, 2025

TABLE IV

COMPARISONS BETWEEN SOME TYPICAL CAV CONTROL SIMULATION PLATFORMS

More simulators for CAVs have been designed to consider signaling an optimistic trajectory for the marriage of MARL

more detailed characters and versatile scenarios, which pro-and CAVs. 

vides more tools to mitigate the gaps between the simulation and reality. 

A. Safety Challenges

A PCMA \(pedestrian crash avoidance mitigation\) system is a MARL-based system designed to study CAV-pedestrian 1\) Current Progress: Safety is a fundamental concern in interactions in unmarked crosswalks \[165\]. By modeling the deployment of MARL for CAVs, as it directly affects pedestrian behaviors with both predefined and DRL-based public trust, regulatory approval, and real-world applicabil-adaptive strategies, it evaluates collision rates, traffic flow ity. Current research has explored various safety-enhancing efficiency, and observation uncertainty, enabling safer and strategies, including safety-constrained policy training, coop-more adaptive CAV decision-making. 

erative decision-making frameworks, and hierarchical MARL

Nocturne is a 2D driving simulator specifically designed methods \[168\]. Some approaches enforce hard constraints or for studying partial observability in multi-agent driving \[166\]. 

incorporate barrier functions into MARL training to restrict It incorporates real-world data-driven scenarios and efficiently unsafe actions, while others modify reward functions to simulates the limited visibility conditions that CAVs encounter, penalize high-risk behaviors \[169\]. Additionally, graph-based such as occlusions at intersections or sensor limitations. 

learning has been leveraged to enhance inter-vehicle coordi-Generally speaking, the simulation-based evaluations are nation, reducing the risk of conflicts in dense traffic scenarios. 

simpler to implement, reproduce, and scale compared with Safe MARL frameworks have also been introduced for specific real experiments for learning. However, simulations may not driving situations, such as lane merging, intersection coordina-capture all the challenges associated with an actual deploy-tion, and emergency braking scenarios, where explicit safety ment. For example, factors such as network delay, vehicle constraints can be embedded into agent interactions. However, model discrepancies, computation time, and the necessity despite these advancements, the majority of existing methods of implementing clock synchronization and fail-safe routines rely on empirical safety validation rather than theoretical pose challenges in real-world implementations. 

guarantees, making their applicability to real-world traffic conditions uncertain. Furthermore, the challenge of generalization to diverse and unseen scenarios persists, as most safety mech-IV. DISCUSSION & FUTURE WORK

anisms are designed and evaluated in constrained simulation CAVs leveraging MARL algorithms present a promising settings rather than in open-ended, adversarial, or extreme frontier in the evolution of transportation. As urban cen-conditions \[170\]. 

ters grapple with traffic congestion and road safety, the 2\) Research Gaps: Despite the progress in safety-aware nuanced and adaptive behaviors offered by MARL algo-MARL for CAVs, several fundamental challenges remain unre-rithms can enable CAVs to respond more fluidly to the solved. First, formal safety guarantees are largely absent, as actions of other road participants. The dynamism of MARL

most existing safety frameworks rely on heuristic-based reward allows these vehicles to cooperatively optimize traffic flows, shaping, risk-sensitive training, or pre-defined constraints that potentially alleviating congestion and reducing transit times. 

do not provide mathematically rigorous assurances of policy Nevertheless, the journey to this future is not without its safety. To achieve provable safety, future research must explore challenges. Interactions with unpredictable human drivers, control-theoretic safety verification, distributionally robust managing the delicate balance between exploration and safety optimization, and formal methods that can certify MARL

in learning, and navigating a complex regulatory land-policies under worst-case scenarios. Second, uncertainty in scape are just a few of the hurdles. Yet, with ongoing real-world driving environments—including stochastic traffic collaborations among tech giants, startups, and academic cir-behaviors, sensor noise, adversarial interactions, and rare cles, there is a collective push to overcome these barriers, edge cases—poses a major obstacle to safe MARL policy

HUA et al.: MARL FOR CAVs CONTROL: RECENT ADVANCEMENTS AND FUTURE PROSPECTS

16281

learning \[171\]. While some methods incorporate robust train-garnered extensive attention \[176\]. However, in the context of ing techniques, they often struggle with out-of-distribution MARL, and similarly in the domain of CAVs, these areas have generalization when deployed in novel, high-risk traffic sce-remained relatively unexplored. This suggests a promising area narios. Third, safe exploration remains a significant open for future research that merits exploration. 

challenge, as conventional RL exploration strategies may lead to high-risk behaviors during training, potentially resulting in C. Mixed-Traffic Challenges

catastrophic failures. Safe RL techniques, such as conserva-1\) Current Progress: One of the formidable challenges tive policy learning, shielding mechanisms, and risk-aware posed by CAVs stems from navigating the intricate dynamics exploration strategies, require further refinement to balance of mixed traffic, wherein CAVs share the road with various exploration efficiency and safety constraints. Future research other road users, including human-driven vehicles, bicycles, e-should focus on developing provably safe MARL frameworks, scooters, and an array of other modes of transportation \[177\], 

improving robustness to real-world uncertainties, and advanc-

\[178\]. This multifaceted coexistence necessitates advanced ing risk-sensitive training methods that enable MARL agents MARL algorithms to ensure seamless and safe interactions to operate reliably in diverse, dynamic, and unpredictable among these diverse road users. Current research into MARL

traffic conditions. 

algorithms for CAV applications primarily concentrates on B. Communication Challenges

integrating the prediction of human behavior into the decision-making process \[179\]. For instance, in \[30\], the authors 1\) Current Progress: Effective communication is pivotal in introduce a novel MARL framework with a priority-based MARL for CAVs, enabling collaboration, information sharing, safety supervisor designed to preempt potential collisions. This and coordinated decision-making through reliable protocols is achieved by predicting future trajectories, encompassing

\[172\]. First, the development of advanced communication both CAVs and HDVs and then the unsafe actions generated protocols tailored specifically for CAVs is a pressing need. 

by MARL agents will be replaced with safe actions, thereby Existing research focuses on protocols that enable efficient contributing to the enhancement of safety in mixed traffic data sharing \[173\]. For instance, research endeavors have scenarios. However, it is important to note that human-driven delved into the utilization of graph-based MARL algorithms vehicles can introduce an additional layer of unpredictability

\[122\], such as those explored in \[136\] and \[138\], to enable effi-into the traffic environment, since mixed traffic involves a cient and adaptive message exchange among agents. Second, diverse range of road users, presenting unique challenges the challenge of ensuring robust communication in dynam-for the seamless integration of CAVs into the existing road ically evolving traffic scenarios represents another critical ecosystem. 

aspect that deserves meticulous attention \[174\]. For exam-2\) Research Gaps: Given the diverse spectrum of road ple, in \[157\], a variational auto-encoder algorithm combined users, future research endeavors will encompass the develop-with advanced multi-head attention mechanisms is proposed ment of real-time, adaptive safety assessment and intervention to extract and retain valuable information from neighboring strategies capable of responding to the dynamic nature agents while making efficient use of constrained communi-of traffic conditions. Another significant aspect entails the cation resources. Last but not least, it is worth noting that establishment of novel coordination and communication mech-managing unstable communication channels, particularly in anisms between CAVs and other road users. For instance, terms of latency, emerges as a particularly intriguing consid-as the presence of e-scooters on the roads continues to eration in the context of MARL for CAVs \[108\]. In \[108\], 

surge, there is a growing imperative to develop efficient the double deep Q-learning algorithm is proposed to jointly methods for coordinating the interactions between CAVs and train the agents to maximize the sum rate of V2N links while e-scooters \[180\]. Furthermore, the existing MARL algorithms ensuring the desired packet delivery probability for each V2V

are typically trained within specific scenarios, underscoring link within specified latency constraints. 

the necessity for research aimed at enhancing their capacity 2\) Research Gaps: While communication in MARL is a to generalize across a wide range of mixed traffic conditions well-explored domain, its adaptation and application within and environmental contexts. 

CAVs present distinctive research gaps, which necessitate further exploration \[132\]. For instance, existing works often overlook pressing real-world concerns in the realm of CAVs, D. Sim-to-Real Challenges

such as communication costs and the challenges posed by 1\) Current Progress: The transition from simulated training noisy environments. These critical factors, when ignored, can environments to real-world deployment remains a fundamental introduce substantial obstacles to the practical deployment challenge in MARL-based CAV control. While deep MARL

of CAV technology. MARL algorithms applied in computer has achieved significant breakthroughs in simulation environ-science domains are expected to be explored for use in ments \(see Sec. III-D\), models often suffer from performance CAV applications within challenging environments marked by degradation in real-world traffic due to discrepancies in traf-limited bandwidth \[59\] and noisy communication channels fic dynamics, sensor uncertainties, and unforeseen driving

\[175\]. Moreover, the majority of current MARL algorithms in behaviors. To mitigate this sim-to-real gap, researchers have CAVs rely on CTDE \(Sec. II\), potentially posing a significant explored domain adaptation techniques, risk-sensitive training privacy threat within the realm of communication. In the frameworks, and hybrid offline-online RL approaches. Offline field of single-agent RL, security and privacy issues have RL, which trains policies using pre-collected datasets, has

16282

IEEE TRANSACTIONS ON AUTOMATION SCIENCE AND ENGINEERING, VOL. 22, 2025

also been considered to improve safety and data efficiency. 

traffic signal coordination, and unsignalized intersec-However, its applicability to MARL-based CAVs remains an tions, among others. 

open challenge. Another emerging approach for enhancing 3\) We highlighted significant challenges in designing and generalization and policy transfer is Transformer RL \(TRL\). 

evaluating MARL methods within the CAV. Striking Unlike traditional RL architectures that rely on recurrent net-a balance between performance, scalability, and safety works like LSTMs, TRL leverages self-attention mechanisms remains a complex challenge. 

to capture long-range dependencies in sequential decision-This review serves as a crucial resource, aimed at encour-making. This enables MARL agents to better process complex aging further research and the practical application of MARL

traffic patterns, adapt to diverse driving scenarios, and improve within the field of CAVs. 

multi-agent coordination. Moreover, TRL scales efficiently with large interaction datasets, making it a promising tool for REFERENCES

handling the high-dimensional decision-making required for real-world CAV deployment. 

\[1\]

G. Wang, X. Wang, and S. Li, “A guidance module based forma-2\) Research Gaps: The primary challenge in sim-to-real tion control scheme for multi-mobile robot systems with collision avoidance,” IEEE Trans. Autom. Sci. Eng., vol. 21, no. 1, pp. 382–393, transfer lies in the inherent unpredictability of real-world Jan. 2022. 

environments, where traffic behaviors, adversarial interac-

\[2\]

K. Wu, J. Hu, Z. Ding, and F. Arvin, “Finite-time fault-tolerant tions, and rare safety-critical events deviate from synthetic formation control for distributed multi-vehicle networks with bear-ing measurements,” IEEE Trans. Autom. Sci. Eng., vol. 21, no. 2, training data \[181\]. Most MARL policies struggle to gen-pp. 1346–1357, Feb. 2023. 

eralize beyond controlled simulation settings, as existing

\[3\]

B. Li et al., “Traffic-aware ecological cruising control for connected domain adaptation techniques fail to account for com-electric vehicle,” IEEE Trans. Transport. Electrific., vol. 10, no. 3, pp. 5225–5240, Sep. 2024. 

plex, evolving dynamics. Real-world uncertainties, including

\[4\]

M. Hua, G. Chen, C. Zong, and L. He, “Research on synchronous sensor noise, connectivity disruptions, and multi-agent coor-control strategy of steer-by-wire system with dual steering actu-dination failures, further degrade performance. Additionally, ator motors,” Int. J. Veh. Auton. Syst., vol. 15, no. 1, pp. 50–76, 2020. 

the lack of real-world benchmarks and standardized test-

\[5\]

T. Garg and G. Kaur, “A systematic review on intelligent transport ing frameworks hinders objective evaluation, making it systems,” J. Comput. Cognit. Eng., vol. 2, no. 3, pp. 175–188, Jun. 

difficult to measure and compare progress in sim-to-real 2022. 

\[6\]

M. Hua, G. Chen, B. Zhang, and Y. Huang, “A hierarchical energy adaptation \[182\]. Ethical, legal, and regulatory constraints efficiency optimization control strategy for distributed drive electric further complicate direct deployment, as autonomous decision-vehicles,” Proc. Inst. Mech. Eng. D, J. Automobile Eng., vol. 233, making in safety-critical scenarios demands a high level no. 3, pp. 605–621, 2019. 

\[7\]

Y. Lin, J. McPhee, and N. L. Azad, “Comparison of deep rein-of explainability, accountability, and formal safety guaran-forcement learning and model predictive control for adaptive cruise tees. Future research must focus on developing adaptive, control,” IEEE Trans. Intell. Vehicles, vol. 6, no. 2, pp. 221–231, risk-aware policies, leveraging real-time learning frame-Jun. 2021. 

\[8\]

A. Katriniok, B. Rosarius, and P. Mähönen, “Fully distributed model works, improving uncertainty quantification, and establishing predictive control of connected automated vehicles in intersections: regulatory-compliant evaluation methodologies to ensure the Theory and vehicle experiments,” IEEE Trans. Intell. Transp. Syst., scalable and responsible deployment of MARL-based CAV

vol. 23, no. 10, pp. 18288–18300, Oct. 2022. 

\[9\]

D. Chen, K. Zhang, Y. Wang, X. Yin, Z. Li, and D. Filev, control. 

“Communication-efficient decentralized multi-agent reinforcement learning for cooperative adaptive cruise control,” IEEE Trans. Intell. 

V. CONCLUSION

Vehicles, early access, Feb. 21, 2024, doi: 10.1109/TIV.2024.3368025. 

\[10\]

W. Liu et al., “A systematic survey of control techniques and applica-Recently, MARL has emerged as a focal point of interest tions in connected and automated vehicles,” IEEE Internet Things J., within the realm of CAVs. The capability of MARL to tackle vol. 10, no. 24, pp. 21892–21916, Dec. 2023. 

intricate control and coordination challenges in CAVs has

\[11\]

D. Guo, H. Ding, L. Tang, X. Zhang, L. Yang, and Y.-C. Liang, 

“A proactive eavesdropping game in MIMO systems based on mul-unlocked new horizons for the development of intelligent and tiagent deep reinforcement learning,” IEEE Trans. Wireless Commun., efficient next-generation transportation systems. This review vol. 21, no. 11, pp. 8889–8904, Nov. 2022. 

has undertaken a comprehensive exploration of the applica-

\[12\]

X. Bai, A. Fielbaum, M. Kronmuller, L. Knoedler, and J. Alonso-Mora, “Group-based distributed auction algorithms for multi-robot tions of MARL in the control of CAVs. 

task assignment,” IEEE Trans. Autom. Sci. Eng., vol. 20, no. 2, 1\) The review began with an overview of single-agent pp. 1292–1303, Apr. 2023. 

\[13\]

X. Wang, D. Ye, L. Zhang, and X. Zhao, “Prescribed performance RL techniques and an extensive survey of the diverse tracking control for nonlinear multiagent systems with distributed landscape of MARL architectural variants, facilitating a observation errors compensation,” IEEE Trans. Autom. Sci. Eng., deeper understanding of applications to both individual vol. 22, pp. 5182–5192, 2024. 

\[14\]

Z. E. Liu, Q. Zhou, Y. Li, S. Shuai, and H. Xu, “Safe deep rein-and collective agent behaviors. 

forcement learning-based constrained optimal control scheme for HEV

2\) Our analysis categorized these contributions based energy management,” IEEE Trans. Transport. Electrific., vol. 9, no. 3, on different degrees of control, ranging from one-pp. 4278–4293, Sep. 2023. 

\[15\]

Z. E. Liu et al., “Deep reinforcement learning-based energy man-dimensional to two-dimensional and three-dimensional agement for heavy duty HEV considering discrete-continuous hybrid collaboration. Within this multifaceted arena, MARL

action space,” IEEE Trans. Transport. Electrific., vol. 10, no. 4, has exhibited remarkable prowess, demonstrating its pp. 9864–9876, Dec. 2024. 

promising performance in various CAV control tasks. 

\[16\]

H. Shu, T. Liu, X. Mu, and D. Cao, “Driving tasks transfer using deep reinforcement learning for decision-making of autonomous vehicles in These include cooperative endeavors such as platooning unsignalized intersection,” IEEE Trans. Veh. Technol., vol. 71, no. 1, control, lane-changing maneuvers, on-ramp merging, pp. 41–52, Jan. 2022. 

HUA et al.: MARL FOR CAVs CONTROL: RECENT ADVANCEMENTS AND FUTURE PROSPECTS

16283

\[17\]

M. Zhou, Y. Yu, and X. Qu, “Development of an efficient driving strat-

\[38\]

A. Mahajan, T. Rashid, M. Samvelyan, and S. Whiteson, “MAVEN: egy for connected and automated vehicles at signalized intersections: Multi-agent variational exploration,” in Proc. Adv. Neural Inf. Process. 

A reinforcement learning approach,” IEEE Trans. Intell. Transport. 

Syst., Jan. 2019, pp. 7611–7622. 

Syst., vol. 21, no. 1, pp. 433–443, Jan. 2020. 

\[39\]

W. Li et al., “Multi-agent evolution reinforcement learning method

\[18\]

J. Liu, P. Hang, X. Na, C. Huang, and J. Sun, “Cooperative for machining parameters optimization based on bootstrap aggregating decision-making

for

CAVs

at

unsignalized

intersections:

A

graph attention network simulated environment,” J. Manuf. Syst., Marl

approach

with

attention

and

hierarchical

game

priors,” 

vol. 67, pp. 424–438, Apr. 2023. 

IEEE Trans. Intell. Transport. Syst., vol. 26, no. 1, pp. 443–456, 

\[40\]

D. Qiu, J. Wang, Z. Dong, Y. Wang, and G. Strbac, “Mean-field multi-Jan. 2025. 

agent reinforcement learning for peer-to-peer multi-energy trading,” 

\[19\]

C. Spatharis and K. Blekas, “Multiagent reinforcement learning for IEEE Trans. Power Syst., vol. 38, no. 5, pp. 4853–4866, Sep. 2022. 

autonomous driving in traffic zones with unsignalized intersections,” 

\[41\]

Z. Wang, Y. Xue, L. Liu, H. Zhang, C. Qu, and C. Fang, “Multi-agent J. Intell. Transp. Syst., vol. 28, no. 1, pp. 103–119, Jan. 2024. 

DRL-controlled connected and automated vehicles in mixed traffic

\[20\]

L. Liu, X. Li, Y. Li, J. Li, and Z. Liu, “Reinforcement-Learning-Based with time delays,” IEEE Trans. Intell. Transport. Syst., vol. 25, no. 11, multilane cooperative control for on-ramp merging in mixed-autonomy pp. 17676–17688, Nov. 2024. 

traffic,” IEEE Internet Things J., vol. 11, no. 24, pp. 39809–39819, 

\[42\]

Z. Yan and C. Wu, “Scalability of platoon-based coordination for mixed Dec. 2024. 

autonomy intersections,” in Proc. IEEE/RSJ Int. Conf. Intell. Robots

\[21\]

Q. Hou and J. Dong, “Distributed dynamic event-triggered consensus Syst. \(IROS\), Oct. 2024, pp. 10304–10311. 

control for multiagent systems with guaranteed performance and pos-

\[43\]

Y. Xiao, Y. Song, and J. Liu, “Collaborative multi-agent deep reinforce-itive inter-event times,” IEEE Trans. Autom. Sci. Eng., vol. 21, no. 1, ment learning for energy-efficient resource allocation in heterogeneous pp. 746–757, Jan. 2022. 

mobile edge computing networks,” IEEE Trans. Wireless Commun., 

\[22\]

J. Yang, J. Ni, M. Xi, J. Wen, and Y. Li, “Intelligent path vol. 23, no. 6, pp. 6653–6668, Jun. 2024. 

planning of underwater robot based on reinforcement learning,” 

\[44\]

M. Tan, “Multi-agent reinforcement learning: Independent vs. coopera-IEEE Trans. Autom. Sci. Eng., vol. 20, no. 3, pp. 1983–1996, tive agents,” in Proc. 10th Int. Conf. Mach. Learn., 1993, pp. 330–337. 

Mar. 2022. 

\[45\]

T. Chu and U. Kalabić, “Model-based deep reinforcement learning for

\[23\]

E. Palacios-Morocho, S. Inca, and J. F. Monserrat, “Enhancing CACC in mixed-autonomy vehicle platoon,” in Proc. IEEE 58th Conf. 

cooperative multi-agent systems with self-advice and near-neighbor Decis. Control \(CDC\), Dec. 2019, pp. 4079–4084. 

priority collision control,” IEEE Trans. Intell. Vehicles, vol. 9, no. 1, 

\[46\]

T. T. Nguyen, N. D. Nguyen, and S. Nahavandi, “Deep reinforcement pp. 2864–2877, Jan. 2023. 

learning for multiagent systems: A review of challenges, solutions, 

\[24\]

K. Zhang, Z. Yang, and T. Bas¸ar, “Multi-agent reinforcement learning: and applications,” IEEE Trans. Cybern., vol. 50, no. 9, pp. 3826–3839, A selective overview of theories and algorithms,” in Handbook of Sep. 2020. 

Reinforcement Learning and Control. Cham, Switzerland: Springer, 

\[47\]

K. Zhang, Z. Yang, H. Liu, T. Zhang, and T. Basar, “Fully decentralized Jun. 2021, pp. 321–384. 

multi-agent reinforcement learning with networked agents,” in Proc. 

\[25\]

M. Bettini, R. Kortvelesy, J. Blumenkamp, and A. Prorok, “VMAS: Int. Conf. Mach. Learn., 2018, pp. 5872–5881. 

A vectorized multi-agent simulator for collective robot learning,” in

\[48\]

R. F. Prudencio, M. R. O. A. Maximo, and E. L. Colombini, “A sur-Proc. Int. Symp. Distrib. Auto. Robotic Syst. Cham, Switzerland: vey on offline reinforcement learning: Taxonomy, review, and open Springer, Jan. 2024, pp. 42–56. 

problems,” IEEE Trans. Neural Netw. Learn. Syst., vol. 35, no. 8, pp. 10237–10257, Aug. 2023. 

\[26\]

A. Irshayyid, J. Chen, and G. Xiong, “A review on reinforcement

\[49\]

Y. Ran, Y.-C. Li, F. Zhang, Z. Zhang, and Y. Yu, “Policy regularization learning-based highway autonomous vehicle control,” Green Energy with dataset constraint for offline reinforcement learning,” in Proc. Int. 

Intell. Transp., vol. 3, no. 4, Aug. 2024, Art. no. 100156. 

Conf. Mach. Learn., Jan. 2023, pp. 28701–28717. 

\[27\]

S. Han et al., “A multi-agent reinforcement learning approach for safe

\[50\]

A. Kumar, A. Zhou, G. Tucker, and S. Levine, “Conservative and efficient behavior planning of connected autonomous vehicles,” 

Q-learning for offline reinforcement learning,” in Proc. Int. Conf. Adv. 

IEEE Trans. Intell. Transport. Syst., vol. 25, no. 5, pp. 3654–3670, Neural Inf. Process. Syst., vol. 33, 2020, pp. 1179–1191. 

May 2024. 

\[51\]

Q. Wang et al., “Identifying expert behavior in offline training datasets

\[28\]

B. 

Hegde

and

M. 

Bouroche, 

“Multi-agent

reinforcement

improves behavioral cloning of robotic manipulation policies,” IEEE

learning for safe lane changes by connected and autonomous Robot. Autom. Lett., vol. 9, no. 2, pp. 1294–1301, Feb. 2024. 

vehicles: A survey,” AI Commun., vol. 37, no. 2, pp. 203–222, 

\[52\]

T. Rashid, G. Farquhar, B. Peng, and S. Whiteson, “Weighted QMIX: Apr. 2024. 

Expanding monotonic value function factorisation for deep multi-

\[29\]

R. K. Dubey, D. Dailisan, J. Argota Sánchez–Vaquerizo, and agent reinforcement learning,” in Proc. Adv. Neural Inf. Process. Syst., D. Helbing, “FAIRLANE: A multi-agent approach to priority lane Jan. 2020, pp. 10199–10210. 

management in diverse traffic composition,” Transp. Res. C, Emerg. 

\[53\]

Y. Zhang, H. Ma, and Y. Wang, “AVD-net: Attention value decompo-Technol., vol. 171, Feb. 2025, Art. no. 104919. 

sition network for deep multi-agent reinforcement learning,” in Proc. 

\[30\]

D. Chen et al., “Deep multi-agent reinforcement learning for highway 25th Int. Conf. Pattern Recognit. \(ICPR\), Jan. 2021, pp. 7810–7816. 

on-ramp merging in mixed traffic,” IEEE Trans. Intell. Transp. Syst., 

\[54\]

T. Phan, L. Belzner, T. Gabor, A. Sedlmeier, F. Ritz, and vol. 24, no. 11, pp. 11623–11638, Nov. 2023. 

C. Linnhoff–Popien, “Resilient multi-agent reinforcement learning with

\[31\]

P.-M. Liu, X.-G. Guo, J.-L. Wang, X.-P. Xie, and F.-W. Yang, adversarial value decomposition,” in Proc. AAAI Conf. Artif. Intell., 

“Fully distributed hierarchical et intrusion-and fault-tolerant group vol. 35, May 2021, pp. 11308–11316. 

control

for

mass

with

application

to

robotic

manipulators,” 

\[55\]

Q. Wei, Y. Li, J. Zhang, and F.-Y. Wang, “VGN: Value decomposition IEEE Trans. Autom. Sci. Eng., vol. 21, no. 3, pp. 2868–2881, with graph attention networks for multiagent reinforcement learning,” 

Jul. 2023. 

IEEE Trans. Neural Netw. Learn. Syst., vol. 35, no. 1, pp. 182–195, 

\[32\]

Z. Chen et al., “Data-driven methods applied to soft robot model-Jan. 2024. 

ing and control: A review,” IEEE Trans. Autom. Sci. Eng., vol. 22, 

\[56\]

S. Liu et al., “Learning multi-agent cooperation via considering actions pp. 2241–2256, 2025. 

of teammates,” IEEE Trans. Neural Netw. Learn. Syst., vol. 35, no. 8, 

\[33\]

P. Yadav, A. Mishra, and S. Kim, “A comprehensive survey on multi-pp. 11553–11564, Aug. 2023. 

agent reinforcement learning for connected and automated vehicles,” 

\[57\]

Y. Niu, H. Zhao, and L. Yu, “MA-MIX: Value function decomposition Sensors, vol. 23, no. 10, p. 4710, May 2023. 

for cooperative multiagent reinforcement learning based on multi-head

\[34\]

L. P. Kaelbling, M. L. Littman, and A. W. Moore, “Reinforcement attention mechanism,” in Proc. 23rd Int. Conf. Auto. Agents Multiagent learning: A survey,” J. Artif. Intell. Res., vol. 4, no. 1, pp. 237–285, Syst., 2024, pp. 2402–2404. 

Jan. 1996. 

\[58\]

T. Chu, S. Chinchali, and S. Katti, “Multi-agent reinforcement learning

\[35\]

V. Mnih et al., “Asynchronous methods for deep reinforcement for networked system control,” in Proc. Int. Conf. Learn. Repre-learning,” in Proc. Int. Conf. Mach. Learn., 2016, pp. 1928–1937. 

sent., Jan. 2020, pp. 1–16. \[Online\]. Available: https://openreview.net/

\[36\]

T. Chu, J. Wang, L. Codecà, and Z. Li, “Multi-agent deep reinforcement

forum?id=Syx7A3NFvH

learning for large-scale traffic signal control,” IEEE Trans. Intell. 

\[59\]

R. Wang, X. He, R. Yu, W. Qiu, B. An, and Z. Rabinovich, “Learning Transp. Syst., vol. 21, no. 3, pp. 1086–1095, May 2019. 

efficient multi-agent communication: An information bottleneck

\[37\]

J. Wang, M. Yuan, Y. Li, and Z. Zhao, “Hierarchical attention approach,” in Proc. Int. Conf. Mach. Learn., 2020, pp. 9908–9918. 

Master–Slave for heterogeneous multi-agent reinforcement learning,” 

\[60\]

D. Li et al., “Verco: Learning coordinated verbal communication for Neural Netw., vol. 162, pp. 359–368, May 2023. 

multi-agent reinforcement learning,” 2024, arXiv:2404.17780. 

16284

IEEE TRANSACTIONS ON AUTOMATION SCIENCE AND ENGINEERING, VOL. 22, 2025

\[61\]

S. Dolan, S. Nayak, J. J. Aloor, and H. Balakrishnan, “Asynchronous

\[86\]

S. John Grimbly, J. Shock, and A. Pretorius, “Causal multi-cooperative

multi-agent

reinforcement

learning

with

limited

agent reinforcement learning: Review and open problems,” 2021, communication,” 2025, arXiv:2502.00558. 

arXiv:2111.06721. 

\[62\]

J. Yang, I. Borovikov, and H. Zha, “Hierarchical cooperative

\[87\]

J. Pearl, “Theoretical impediments to machine learning with seven multi-agent reinforcement learning with skill discovery,” 2019, sparks from the causal revolution,” 2018, arXiv:1801.04016. 

arXiv:1912.03558. 

\[88\]

N. Jaques et al.. \(2018\). Intrinsic Social Motivation Via Causal Influ-

\[63\]

T. Wang, T. Gupta, A. Mahajan, B. Peng, S. Whiteson, and C. Zhang, ence in Multi-agent RL. \[Online\]. Available: https://openreview.net/

“RODE: Learning roles to decompose multi-agent tasks,” 2020, 

forum?id=B1lG42C9Km

arXiv:2010.01523. 

\[89\]

S. Yang, B. Yang, Z. Zeng, and Z. Kang, “Causal inference multi-agent

\[64\]

B. Li, “Hierarchical architecture for multi-agent reinforcement learning reinforcement learning for traffic signal control,” Inf. Fusion, vol. 94, in intelligent game,” in Proc. Int. Joint Conf. Neural Netw. \(IJCNN\), pp. 243–256, Jun. 2023. 

Jul. 2022, pp. 1–8. 

\[90\]

J. W. K. Ho and C. Wang, “Human-centered AI using ethical causal-

\[65\]

Z. Xu, Y. Bai, B. Zhang, D. Li, and G. Fan, “HAVEN: Hierarchical ity and learning representation for multi-agent deep reinforcement cooperative multi-agent reinforcement learning with dual coordination learning,” in Proc. IEEE 2nd Int. Conf. Hum.-Mach. Syst. \(ICHMS\), mechanism,” in Proc. AAAI Conf. Artif. Intell., Jun. 2023, vol. 37, vol. 37, Sep. 2021, pp. 1–6. 

no. 10, pp. 11735–11743. 

\[91\]

B. Liu et al., “An efficient message dissemination scheme for coop-

\[66\]

M. Yang, Y. Yang, Z. Lu, W. Zhou, and H. Li, “Hierarchical multi-erative drivings via multi-agent hierarchical attention reinforcement agent skill discovery,” in Proc. Adv. Neural Inf. Process. Syst., vol. 36, learning,” in Proc. IEEE 41st Int. Conf. Distrib. Comput. Syst. \(ICDCS\), 2024, pp. 1–15. 

Jul. 2021, pp. 326–336. 

\[67\]

H. Wang, Y. Yu, and Y. Jiang, “Fully decentralized multiagent commu-

\[92\]

B. Li, K. Xie, X. Huang, Y. Wu, and S. Xie, “Deep reinforcement nication via causal inference,” IEEE Trans. Neural Netw. Learn. Syst., learning based incentive mechanism design for platoon autonomous vol. 34, no. 12, pp. 10193–10202, Dec. 2023. 

driving with social effect,” IEEE Trans. Veh. Technol., vol. 71, no. 7, 

\[68\]

J. Li et al., “Deconfounded value decomposition for multi-agent pp. 7719–7729, Jul. 2022. 

reinforcement learning,” in Proc. Int. Conf. Mach. Learn., 2022, 

\[93\]

H. Shi, D. Chen, N. Zheng, X. Wang, Y. Zhou, and B. Ran, “A deep pp. 12843–12856. 

reinforcement learning based distributed control strategy for connected

\[69\]

R. Pina, V. De Silva, and C. Artaud, “Discovering causality for efficient automated vehicles in mixed traffic platoon,” Transp. Res. C, Emerg. 

cooperation in multi-agent environments,” 2023, arXiv:2306.11846. 

Technol., vol. 148, Mar. 2023, Art. no. 104019. 

\[70\]

B. Liu, Z. Pu, Y. Pan, J. Yi, Y. Liang, and D. Zhang, “Lazy agents:

\[94\]

M. Parvini, M. R. Javan, N. Mokari, B. Abbasi, and E. A. Jorswieck, A new perspective on solving sparse reward problem in multi-agent

“AoI-aware resource allocation for platoon-based C-V2X networks reinforcement learning,” in Proc. Int. Conf. Mach. Learn., 2023, via multi-agent multi-task reinforcement learning,” IEEE Trans. Veh. 

pp. 21937–21950. 

Technol., vol. 72, no. 8, pp. 9880–9896, Aug. 2023. 

\[71\]

Z. Li et al., “Coordination as inference in multi-agent reinforcement

\[95\]

M. Kolat and T. Bécsi, “Cooperative MARL-PPO approach for auto-learning,” Neural Netw., vol. 172, Apr. 2024, Art. no. 106101. 

mated highway platoon merging,” Electronics, vol. 13, no. 15, p. 3102, Aug. 2024. 

\[72\]

K. Jiang, W. Liu, Y. Wang, L. Dong, and C. Sun, “Credit assignment in

\[96\]

Y. Xu, Y. Shi, X. Tong, S. Chen, and Y. Ge, “A multi-agent heterogeneous multi-agent reinforcement learning for fully cooperative reinforcement learning based control method for cavs in a mixed tasks,” Int. J. Speech Technol., vol. 53, no. 23, pp. 29205–29222, platoon,” IEEE Trans. Veh. Technol., vol. 73, no. 11, pp. 16160–16172, Dec. 2023. 

Nov. 2024. 

\[73\]

J. N. Foerster, G. Farquhar, T. Afouras, N. Nardelli, and S. Whiteson, 

\[97\]

S. Chen, M. Wang, W. Song, Y. Yang, and M. Fu, “Multi-agent

“Counterfactual multi-agent policy gradients,” in Proc. AAAI, 2018, reinforcement learning-based twin-vehicle fair cooperative driving in pp. 2974–2982. 

dynamic highway scenarios,” in Proc. IEEE 25th Int. Conf. Intell. 

\[74\]

D. Guo, L. Tang, X. Zhang, and Y. Liang, “Joint optimization of Transp. Syst. \(ITSC\), Oct. 2022, pp. 730–736. 

handover control and power allocation based on multi-agent deep

\[98\]

J. Zhang, C. Chang, X. Zeng, and L. Li, “Multi-agent DRL-reinforcement learning,” IEEE Trans. Veh. Technol., vol. 69, no. 11, based lane change with right-of-way collaboration awareness,” 

pp. 13124–13138, Nov. 2020. 

IEEE Trans. Intell. Transport. Syst., vol. 24, no. 1, pp. 854–869, 

\[75\]

Y. Hou et al., “A multi-agent cooperative learning system with evo-Jan. 2023. 

lution of social roles,” IEEE Trans. Evol. Comput., vol. 28, no. 2, 

\[99\]

W. Zhou, D. Chen, J. Yan, Z. Li, H. Yin, and W. Ge, “Multi-agent pp. 531–543, Apr. 2023. 

reinforcement learning for cooperative lane changing of connected and

\[76\]

P. Sunehag et al., “Value-decomposition networks for cooperative autonomous vehicles in mixed traffic,” Auto. Intell. Syst., vol. 2, no. 1, multi-agent learning based on team reward,” in Proc. AAMAS, 2018, p. 5, Dec. 2022. 

pp. 2085–2087. 

\[100\] J. Guo and I. Harmati, “Lane-changing system based on deep q-

\[77\]

K. Son, D. Kim, W. J. Kang, D. E. Hostallero, and Y. Yi, “QTRAN: learning with a request–respond mechanism,” Expert Syst. Appl., Learning to factorize with transformation for cooperative multi-agent vol. 235, Jun. 2024, Art. no. 121242. 

reinforcement learning,” in Proc. ICML, 2019, pp. 5887–5896. 

\[101\] X. Zhang, S. Li, B. Wang, M. Xue, Z. Li, and H. Liu, “Multi-

\[78\]

R. Lowe, Y. Wu, A. Tamar, J. Harb, P. Abbeel, and I. Mordatch, “Multi-vehicle collaborative lane changing based on multi-agent reinforcement agent actor-critic for mixed cooperative-competitive environments,” in learning,” in Proc. IEEE Intell. Vehicles Symp. \(IV\), Jun. 2024, Proc. Adv. Neural Inf. Process. Syst., Jan. 2017, pp. 1–19. 

pp. 1214–1221. 

\[79\]

J. Foerster et al., “Stabilising experience replay for deep multi-agent

\[102\] H. Wang, W. Hao, J. So, Z. Chen, and J. Hu, “A faster coop-reinforcement learning,” in Proc. ICML, 2017, pp. 1146–1155. 

erative lane change controller enabled by formulating in spatial

\[80\]

J. Foerster, Y. Assael, N. D. Freitas, and S. Whiteson, “Learning to domain,” IEEE Trans. Intell. Vehicles, vol. 8, no. 12, pp. 4685–4695, communicate with deep multi-agent reinforcement learning,” in Proc. 

Dec. 2023. 

Adv. Neural Inf. Process. Syst., Jan. 2016, pp. 1–16. 

\[103\] S. Tsugawa, S. Jeschke, and S. E. Shladover, “A review of truck

\[81\]

P.-L. Bacon, J. Harb, and D. Precup, “The option-critic architecture,” 

platooning projects for energy savings,” IEEE Trans. Intell. Veh., vol. 1, in Proc. AAAI Conf. Artif. Intell., Feb. 2017, vol. 31, no. 1, pp. 1–18. 

no. 1, pp. 68–77, Mar. 2016. 

\[82\]

J. Harb, P.-L. Bacon, M. Klissarov, and D. Precup, “When waiting

\[104\] Y. Xu, K. Zhu, H. Xu, and J. Ji, “Deep reinforcement learning is not an option: Learning options with a deliberation cost,” in Proc. 

for multi-objective resource allocation in multi-platoon cooperative AAAI Conf. Artif. Intell., Apr. 2018, vol. 32, no. 1, pp. 1–16. 

vehicular networks,” IEEE Trans. Wireless Commun., vol. 22, no. 9, 

\[83\]

A. S. Vezhnevets et al., “Feudal networks for hierarchical reinforce-pp. 6185–6198, Sep. 2023. 

ment learning,” in Proc. Int. Conf. Mach. Learn. \(ICML\), 2017, 

\[105\] Z. Wang, G. Wu, and M. J. Barth, “Cooperative eco-driving at pp. 3540–3549. 

signalized intersections in a partially connected and automated vehi-

\[84\]

O. Nachum, S. Gu, H. Lee, and S. Levine, “Data-efficient hierarchical cle environment,” IEEE Trans. Intell. Transp. Syst., vol. 21, no. 5, reinforcement learning,” in Proc. Adv. Neural Inf. Process. Syst., pp. 2029–2038, May 2020. 

May 2018, pp. 1–11. 

\[106\] S. Lu, Y. Cai, L. Chen, H. Wang, X. Sun, and H. Gao, “Altruistic

\[85\]

S. Pateria, B. Subagdja, A.-H. Tan, and C. Quek, “Hierarchical rein-cooperative adaptive cruise control of mixed traffic platoon based on forcement learning: A comprehensive survey,” ACM Comput. Surveys, deep reinforcement learning,” IET Intell. Transp. Syst., vol. 17, no. 10, vol. 54, no. 5, pp. 1–35, 2021. 

pp. 1951–1963, Oct. 2023. 

HUA et al.: MARL FOR CAVs CONTROL: RECENT ADVANCEMENTS AND FUTURE PROSPECTS

16285

\[107\] N. Heess et al., “Emergence of locomotion behaviours in rich

\[129\] T. Wang, J. Cao, and A. Hussain, “Adaptive traffic signal control environments,” 2017, arXiv:1707.02286. 

for large-scale scenario with cooperative group-based multi-agent

\[108\] H. V. Vu, M. Farzanullah, Z. Liu, D. H. N. Nguyen, R. Morawski, reinforcement learning,” Transp. Res. C, Emerg. Technol., vol. 125, and T. Le-Ngoc, “Multi-agent reinforcement learning for channel Apr. 2021, Art. no. 103046. 

assignment and power allocation in platoon-based C-V2X systems,” 

\[130\] T. Wu et al., “Multi-agent deep reinforcement learning for urban traffic 2020, arXiv:2011.04555. 

light control in vehicular networks,” IEEE Trans. Veh. Technol., vol. 69, 

\[109\] S. Feng, Y. Zhang, S. E. Li, Z. Cao, H. X. Liu, and L. Li, “String sta-no. 8, pp. 8243–8256, Aug. 2020. 

bility for vehicular platoon control: Definitions and analysis methods,” 

\[131\] J. Ma and F. Wu, “Feudal multi-agent deep reinforcement learning for Annu. Rev. Control, vol. 47, pp. 81–97, Aug. 2019. 

traffic signal control,” in Proc. 19th Int. Conf. Auto. Agents Multiagent

\[110\] A. Peake, J. McCalmon, B. Raiford, T. Liu, and S. Alqahtani, “Multi-Syst. \(AAMAS\), May 2020, pp. 816–824. 

agent reinforcement learning for cooperative adaptive cruise control,” 

\[132\] C. Zhu, M. Dastani, and S. Wang, “A survey of multi-agent deep in Proc. IEEE 32nd Int. Conf. Tools Artif. Intell. \(ICTAI\), Nov. 2020, reinforcement learning with communication,” 2022, arXiv:2203.08975. 

pp. 15–22. 

\[133\] D. Liu and L. Li, “A traffic light control method based on multi-

\[111\] S. Hochreiter and J. Schmidhuber, “Long short-term memory,” Neural agent deep reinforcement learning algorithm,” Sci. Rep., vol. 13, no. 1, Comput., vol. 9, no. 8, pp. 1735–1780, 1997. 

p. 9396, Jun. 2023. 

\[112\] M. Li, Z. Cao, and Z. Li, “A reinforcement learning-based vehicle

\[134\] Y. Wang, T. Xu, X. Niu, C. Tan, E. Chen, and H. Xiong, “STMARL: platoon control strategy for reducing energy consumption in traffic A spatio-temporal multi-agent reinforcement learning approach for oscillations,” IEEE Trans. Neural Netw. Learn. Syst., vol. 32, no. 12, cooperative traffic light control,” IEEE Trans. Mobile Comput., vol. 21, pp. 5309–5322, Dec. 2021. 

no. 6, pp. 2228–2242, Jun. 2022. 

\[113\] X. He, H. Yang, Z. Hu, and C. Lv, “Robust lane change decision

\[135\] Q. Jiang, M. Qin, S. Shi, W. Sun, and B. Zheng, “Multi-agent making for autonomous vehicles: An observation adversarial reinforce-reinforcement learning for traffic signal control through universal ment learning approach,” IEEE Trans. Intell. Vehicles, vol. 8, no. 1, communication method,” 2022, arXiv:2204.12190. 

pp. 184–193, Jan. 2023. 

\[136\] Q. Liu, X. Li, Y. Tang, X. Gao, F. Yang, and Z. Li, “Graph reinforce-

\[114\] G. Chen, Z. Gao, M. Hua, B. Shuai, and Z. Gao, “Lane ment learning-based decision-making technology for connected and change trajectory prediction considering driving style uncertainty for autonomous vehicles: Framework, review, and future trends,” Sensors, autonomous vehicles,” Mech. Syst. Signal Process., vol. 206, Jan. 2024, vol. 23, no. 19, p. 8229, Oct. 2023. 

Art. no. 110854. 

\[137\] H. Wei et al., “CoLight: Learning network-level cooperation for traffic

\[115\] C. Yu et al., “The surprising effectiveness of PPO in cooperative signal control,” in Proc. 28th ACM Int. Conf. Inf. Knowl. Manag., 2019, multi-agent games,” in Proc. Adv. Neural Inf. Process. Syst., vol. 35, pp. 1913–1922. 

Nov. 2022, pp. 24611–24624. 

\[138\] S. Yang, B. Yang, Z. Kang, and L. Deng, “IHG-MA: Inductive hetero-

\[116\] Y. Hou and P. Graf, “Decentralized cooperative lane changing at geneous graph multi-agent reinforcement learning for multi-intersection freeway weaving areas using multi-agent deep reinforcement learning,” 

traffic signal control,” Neural Netw., vol. 139, pp. 265–277, Jul. 2021. 

2021, arXiv:2110.08124. 

\[139\] G. Antonio and C. Maria-Dolores, “Multi-agent deep reinforce-

\[117\] S. Chen, M. Wang, W. Song, Y. Yang, and M. Fu, “Multi-ment learning to manage connected autonomous vehicles at tomor-agent reinforcement learning-based decision making for twin-vehicles row’s intersections,” IEEE Trans. Veh. Technol., vol. 71, no. 7, cooperative driving in stochastic dynamic highway environments,” 

pp. 7033–7043, Jul. 2022. 

IEEE

Trans. 

Veh. 

Technol., 

vol. 72, 

no. 10, 

pp. 12615–12627, 

\[140\] Y. Ren, H. Zhang, L. Du, Z. Zhang, J. Zhang, and H. Li, “Stealthy Oct. 2023. 

black-box attack with dynamic threshold against MARL-based traffic

\[118\] C. Vishnu, V. Abhinav, D. Roy, C. K. Mohan, and C. S. Babu, signal control system,” IEEE Trans. Ind. Informat., vol. 20, no. 10, 

“Improving multi-agent trajectory prediction using traffic states on pp. 12021–12031, Oct. 2024. 

interactive driving scenarios,” IEEE Robot. Autom. Lett., vol. 8, no. 5, pp. 2708–2715, May 2023. 

\[141\] Y. Yan et al., “A multi-vehicle game-theoretic framework for decision making and planning of autonomous vehicles in mixed traffic,” IEEE

\[119\] S. Han et al., “A multi-agent reinforcement learning approach for safe Trans. Intell. Vehicles, vol. 8, no. 11, pp. 4572–4587, Nov. 2023. 

and efficient behavior planning of connected autonomous vehicles,” 

2020, arXiv:2003.04371. 

\[142\] L. Schester and L. E. Ortiz, “Longitudinal position control for

\[120\] Q. Li, Z. Peng, L. Feng, Q. Zhang, Z. Xue, and B. Zhou, “MetaDrive: highway on-ramp merging: A multi-agent approach to automated Composing diverse driving scenarios for generalizable reinforcement driving,” in Proc. IEEE Intell. Transp. Syst. Conf. \(ITSC\), Oct. 2019, learning,” IEEE Trans. Pattern Anal. Mach. Intell., vol. 45, no. 3, pp. 3461–3468. 

pp. 3461–3475, Mar. 2023. 

\[143\] S. Zhou, W. Zhuang, G. Yin, H. Liu, and C. Qiu, “Cooperative on-

\[121\] J. Zhou et al., “Graph neural networks: A review of methods and ramp merging control of connected and automated vehicles: Distributed applications,” AI Open, vol. 1, pp. 57–81, Jun. 2020. 

multi-agent deep reinforcement learning approach,” in Proc. IEEE 25th

\[122\] S. Chen, J. Dong, P. J. Ha, Y. Li, and S. Labi, “Graph neural Int. Conf. Intell. Transp. Syst. \(ITSC\), Jul. 2022, pp. 402–408. 

network and reinforcement learning for multi-agent cooperative control

\[144\] S. K. Sumanth Nakka, B. Chalaki, and A. A. Malikopoulos, of connected autonomous vehicles,” Comput.-Aided Civil Infrastruct. 

“A multi-agent deep reinforcement learning coordination framework Eng., vol. 36, no. 7, pp. 838–857, Jul. 2021. 

for connected and automated vehicles at merging roadways,” in Proc. 

\[123\] P. Young Joun Ha, S. Chen, J. Dong, R. Du, Y. Li, and S. Labi, Amer. Control Conf. \(ACC\), Jun. 2022, pp. 3297–3302. 

“Leveraging the capabilities of connected and autonomous vehicles

\[145\] Y. Hu, A. Nakhaei, M. Tomizuka, and K. Fujimura, “Interaction-aware and multi-agent reinforcement learning to mitigate highway bottleneck decision making with adaptive strategies under merging scenarios,” 

congestion,” 2020, arXiv:2010.05436. 

in Proc. IEEE/RSJ Int. Conf. Intell. Robots Syst. \(IROS\), Nov. 2019, 

\[124\] G. Wang, J. Hu, Z. Li, and L. Li, “Harmonious lane changing via pp. 151–158. 

deep reinforcement learning,” IEEE Trans. Intell. Transp. Syst., vol. 23, 

\[146\] R. Chandra and D. Manocha, “GamePlan: Game-theoretic multi-no. 5, pp. 4642–4650, May 2022. 

agent planning with human drivers at intersections, roundabouts, and

\[125\] Y. Wu, H. Chen, and F. Zhu, “DCL-AIM: Decentralized coordina-merging,” IEEE Robot. Autom. Lett., vol. 7, no. 2, pp. 2676–2683, tion learning of autonomous intersection management for connected Apr. 2022. 

and automated vehicles,” Transp. Res. C, Emerg. Technol., vol. 103, 

\[147\] C. Huang, J. Zhao, H. Zhou, H. Zhang, X. Zhang, and C. Ye, “Multi-pp. 246–260, Jun. 2019. 

agent decision-making at unsignalized intersections with reinforcement

\[126\] T. Tan, F. Bao, Y. Deng, A. Jin, Q. Dai, and J. Wang, learning from demonstrations,” in Proc. IEEE Intell. Vehicles Symp., 

“Cooperative deep reinforcement learning for large-scale traffic grid Jun. 2023, pp. 1–6. 

signal control,” IEEE Trans. Cybern., vol. 50, no. 6, pp. 2687–2700, 

\[148\] A. Aksjonov and V. Kyrki, “Rule-based decision-making system for Jun. 2020. 

autonomous vehicles at intersections with mixed traffic environment,” 

\[127\] E. Van der Pol and F. A. Oliehoek, “Coordinated deep reinforcement in Proc. IEEE Int. Intell. Transp. Syst. Conf. \(ITSC\), Sep. 2021, learners for traffic light control,” in Proc. Learn., Inference Control pp. 660–666. 

Multi-Agent Syst. \(NIPS\), vol. 8, 2016, pp. 21–38. 

\[149\] Y. Gu, Y. Hashimoto, L.-T. Hsu, and S. Kamijo, “Motion planning

\[128\] J. Liu, H. Zhang, Z. Fu, and Y. Wang, “Learning scalable multi-agent based on learning models of pedestrian and driver behaviors,” in coordination by spatial differentiation for traffic signal control,” Eng. 

Proc. IEEE 19th Int. Conf. Intell. Transp. Syst. \(ITSC\), Nov. 2016, Appl. Artif. Intell., vol. 100, Apr. 2021, Art. no. 104165. 

pp. 808–813. 

16286

IEEE TRANSACTIONS ON AUTOMATION SCIENCE AND ENGINEERING, VOL. 22, 2025

\[150\] A. P. Capasso, P. Maramotti, A. Dell’Eva, and A. Broggi, “End-to-end

\[167\] E. Leurent. \(2018\). An Environment for Autonomous Driving Decision-intersection handling using multi-agent deep reinforcement learning,” 

making. \[Online\]. Available: https://github.com/eleurent/highway-env

in Proc. IEEE Intell. Vehicles Symp. \(IV\), Jul. 2021, pp. 443–450. 

\[168\] S. Gu et al., “A review of safe reinforcement learning: Methods, 

\[151\] Z. Yan and C. Wu, “Reinforcement learning for mixed autonomy theories, and applications,” IEEE Trans. Pattern Anal. Mach. Intell., intersections,” in Proc. IEEE Int. Intell. Transp. Syst. Conf. \(ITSC\), vol. 46, no. 12, pp. 11216–11235, Dec. 2024. 

Oct. 2021, pp. 2089–2094. 

\[169\] Q. Yang, T. D. Sim˜ao, S. H. Tindemans, and M. T. J. Spaan, 

\[152\] C. Mavrogiannis, J. A. DeCastro, and S. S. Srinivasa, “Implicit

“Safety-constrained reinforcement learning with a distributional multiagent coordination at unsignalized intersections via multimodal safety

critic,” 

Mach. 

Learn., 

vol. 112, 

no. 3, 

pp. 859–887, 

inference enabled by topological braids,” 2020, arXiv:2004.05205. 

Mar. 2023. 

\[153\] J. X. Zheng, K. Zhu, and R. Wang, “Deep reinforcement learning for

\[170\] S. Gu et al., “Safe multi-agent reinforcement learning for multi-robot autonomous vehicles collaboration at unsignalized intersections,” in control,” Artif. Intell., vol. 319, Jun. 2023, Art. no. 103905. 

Proc. IEEE Global Commun. Conf., Dec. 2022, pp. 1115–1120. 

\[171\] C. Hou, C. Zhou, C.-G. Wu, R. Cong, and K. Li, “Optimization of

\[154\] A. H. Hamouda, D. M. Mahfouz, C. M. Elias, and O. M. Shehata, cloud-based multi-agent system for trade-off between trustworthiness

“Multi-layer control architecture for unsignalized intersection manage-of data and cost of data usage,” IEEE Trans. Autom. Sci. Eng., vol. 21, ment via nonlinear MPC and deep reinforcement learning,” in Proc. 

no. 1, pp. 106–122, Jan. 2022. 

IEEE Int. Intell. Transp. Syst. Conf. \(ITSC\), Sep. 2021, pp. 1990–1996. 

\[172\] M. H. Rahman, M. Abdel-Aty, and Y. Wu, “A multi-vehicle com-

\[155\] Y. Xu, H. Zhou, T. Ma, J. Zhao, B. Qian, and X. Shen, munication system to assess the safety and mobility of connected

“Leveraging multiagent learning for automated vehicles scheduling at and automated vehicles,” Transp. Res. C, Emerg. Technol., vol. 124, nonsignalized intersections,” IEEE Internet Things J., vol. 8, no. 14, Mar. 2021, Art. no. 102887. 

pp. 11427–11439, Jul. 2021. 

\[173\] Y. Cheng, L. Shi, J. Shao, L. Bai, and K. Chen, “Emergent dynamics

\[156\] N. Hoysal and P. Tallapragada, “Reinforcement learning aided sequen-of asynchronous multiagent systems under signed networks and limited tial optimization for unsignalized intersection management of robot communication resources,” IEEE Trans. Netw. Sci. Eng., vol. 10, no. 1, traffic,” 2023, arXiv:2302.05082. 

pp. 477–488, Jan. 2023. 

\[157\] Z. Li, Q. Yuan, G. Luo, and J. Li, “Learning effective multi-vehicle

\[174\] R. Valiente, B. Toghi, R. Pedarsani, and Y. P. Fallah, “Robustness and cooperation at unsignalized intersection via bandwidth-constrained adaptability of reinforcement learning-based cooperative autonomous communication,” in Proc. IEEE 94th Veh. Technol. Conf., Sep. 2021, driving in mixed-autonomy traffic,” IEEE Open J. Intell. Transp. Syst., pp. 1–7. 

vol. 3, pp. 397–410, 2022. 

\[158\] Z. Guo, Y. Wu, L. Wang, and J. Zhang, “Coordination for

\[175\] B. Freed, G. Sartoretti, J. Hu, and H. Choset, “Communication learn-connected and automated vehicles at non-signalized intersections: ing via backpropagation in discrete channels with unknown noise,” 

A value decomposition-based multiagent deep reinforcement learning in Proc. AAAI Conf. Artif. Intell., vol. 34, no. 5, pp. 7160–7168, approach,” IEEE Trans. Veh. Technol., vol. 72, no. 3, pp. 3025–3034, Apr. 2020. 

Mar. 2023. 

\[176\] Y. Lei, D. Ye, S. Shen, Y. Sui, T. Zhu, and W. Zhou, “New challenges

\[159\] P. Á. López et al., “Microscopic traffic simulation using SUMO,” 

in reinforcement learning: A survey of security and privacy,” Artif. 

in Proc. 21st Int. Conf. Intell. Transp. Syst. \(ITSC\), Nov. 2018, Intell. Rev., vol. 56, no. 7, pp. 7195–7236, 2023. 

pp. 2575–2582. 

\[177\] R. Valiente, B. Toghi, M. Razzaghpour, R. Pedarsani, and Y. P. Fallah, 

\[160\] H. Zhang et al., “CityFlow: A multi-agent reinforcement learning

“Learning-based social coordination to improve safety and robustness environment for large scale city traffic scenario,” in Proc. World Wide of cooperative autonomous vehicles in mixed traffic,” in Machine Web Conf., 2019, pp. 3620–3624. 

Learning and Optimization Techniques for Automotive Cyber-Physical

\[161\] M. Zhou et al., “SMARTS: Scalable multi-agent reinforcement learning Systems. Cham, Switzerland: Springer, 2023, pp. 671–707. 

training school for autonomous driving,” 2020, arXiv:2010.09776. 

\[178\] S. Zhao, G. Chen, M. Hua, and C. Zong, “An identification algorithm

\[162\] A. Dosovitskiy, G. Ros, F. Codevilla, A. Lopez, and V. Koltun, of driver steering characteristics based on backpropagation neural

“CARLA: An open urban driving simulator,” in Proc. 1st Annu. Conf. 

network,” Proc. Inst. Mech. Eng. D, J. Automobile Eng., vol. 233, Robot Learn., vol. 78, 2017, pp. 1–16. 

no. 9, pp. 2333–2342, 2019. 

\[163\] P. Palanisamy, “Multi-agent connected autonomous driving using

\[179\] C. Dai, C. Zong, D. Zhang, M. Hua, H. Zheng, and K. Chuyo, deep reinforcement learning,” in Proc. Int. Joint Conf. Neural Netw. 

“A bargaining game-based human–machine shared driving control \(IJCNN\), Jul. 2020, pp. 1–7. 

authority allocation strategy,” IEEE Trans. Intell. Transp. Syst., vol. 24, 

\[164\] S. Chen, Y. Chen, S. Zhang, and N. Zheng, “A novel integrated no. 10, pp. 10572–10586, Oct. 2023. 

simulation and testing platform for self-driving cars with hardware

\[180\] S. Gilroy, D. Mullins, E. Jones, A. Parsi, and M. Glavin, “E-scooter in the loop,” IEEE Trans. Intell. Veh., vol. 4, no. 3, pp. 425–436, rider detection and classification in dense urban environments,” Results Sep. 2019. 

Eng., vol. 16, Dec. 2022, Art. no. 100677. 

\[165\] R. Trumpp, H. Bayerlein, and D. Gesbert, “Modeling interactions of

\[181\] X. Guo, D. Zhang, J. Wang, J. Park, and L. Guo, “Observer-based autonomous vehicles and pedestrians with deep multi-agent reinforce-event-triggered composite anti-disturbance control for multi-agent ment learning for collision avoidance,” in Proc. IEEE Intell. Vehicles systems under multiple disturbances and stochastic FDIAs,” IEEE

Symp. \(IV\), Jun. 2022, pp. 331–336. 

Trans. Autom. Sci. Eng., vol. 20, no. 1, pp. 528–540, Mar. 31, 

\[166\] E. Vinitsky, N. Lichtlé, X. Yang, B. Amos, and J. Foerster, “Nocturne: 2022. 

A scalable driving benchmark for bringing multi-agent learning one

\[182\] N. Lichtlé et al., “From sim to real: A pipeline for training and step closer to the real world,” in Proc. Adv. Neural Inf. Process. Syst., deploying traffic smoothing cruise controllers,” IEEE Trans. Robot., Jan. 2022, pp. 3962–3974. 

vol. 40, pp. 4490–4505, 2024.



