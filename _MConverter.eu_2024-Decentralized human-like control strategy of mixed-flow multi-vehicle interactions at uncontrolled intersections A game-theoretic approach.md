Transportation Research Part C 167 \(2024\) 104835 

Contents lists available at ScienceDirect

Transportation Research Part C

journal homepage: www.elsevier.com/locate/trc

Decentralized human-like control strategy of mixed-flow

multi-vehicle interactions at uncontrolled intersections: A

game-theoretic approach

Dian Jing , Enjian Yao \*, Rongsheng Chen

*Key Laboratory of Transport Industry of Big Data Application Technologies for Comprehensive Transport, Beijing Jiaotong University, Beijing* *100044, China*

A R T I C L E I N F O

A B S T R A C T

*Keywords:*

A critical challenge that future autonomous driving systems face is improving the ability to cope Connected and autonomous vehicles

with complex real-world interaction scenarios such as uncontrolled intersections. In the near Decentralized control strategies

future, a mixed traffic flow of human-driven vehicles \(HDVs\) and connected autonomous vehicles Game theory

\(CAVs\) will coexist in transport networks, which motivates us to explore the interaction between Human driving styles

Multi-agent systems

HDVs and CAVs to improve traffic efficiency and safety. To help CAVs better interact with HDVs and adapt to the mixed-flow environment, we propose a human-like decentralized control

strategy for CAVs. First, a game-theoretic framework is proposed to model multi-vehicle in-

teractions \(including HDV-CAV, CAV-CAV interactions\) in the mixed-flow environment. The

existence of solutions is proven to ensure the feasibility of the proposed game-theoretic model. 

Next, a driving style recognition algorithm is embedded into the proposed model to help CAVs understand and predict human drivers’ actions. The proposed model is calibrated via a real-world dataset and used to simulate traffic in several testing scenarios. Real-world vehicle trajectories are used to verify the accuracy of generated vehicle trajectories in simulations. Experimental results indicate that 1\) CAVs can take more reasonable actions to determine whether to yield while

ensuring safety when competing for the right of way with HDVs using the proposed method

compared with conservative driving strategies, 2\) a higher penetration rate of CAVs can significantly enhance travel efficiency and lower collision risk at uncontrolled intersections. 

**1. Introduction**

Intersections are one of the major bottlenecks that result in severe accidents and traffic congestion in urban traffic networks. 

According to a report from the Fatality Analysis Reporting System \(FARS\), 54,272 fatal crashes happened across the United States in 2020, while 28.9 % were related to intersections \(NHTSA, 2020\). Besides, frequent intersection congestion occurrences lead to eco-nomic loss and environmental pollution \(Liu et al., 2019; Mu et al., 2021; Wei et al., 2021\). Therefore, many studies have provided solutions to reduce traffic conflicts and achieve better interactions at intersections. By types of traffic control, intersections can be categorized as \(1\) signal-controlled, \(2\) sign-controlled, and \(3\) uncontrolled \(Li et al., 2022\). At signal-controlled intersections, traffic signal phasing and timing \(SPaT\) is mainly used in real-world control to match dynamic traffic demands, such as SCATS \(Sims & 

\* Corresponding author. 

*E-mail addresses: *dian\_jing@bjtu.edu.cn \(D. Jing\), enjyao@bjtu.edu.cn \(E. Yao\), rshchen@bjtu.edu.cn \(R. Chen\). 

https://doi.org/10.1016/j.trc.2024.104835

Received 2 June 2023; Received in revised form 20 July 2024; Accepted 22 August 2024

Available online 1 September 2024 

0968-090X/© 2024 Elsevier Ltd. All rights are reserved, including those for text and data mining, AI training, and similar technologies. 

*D. Jing et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104835* 

Dobinson, 1980\), SCOOT \(Hunt et al., 1982\), RHODES \(Mirchandani & Head, 2001\), OPAC \(Gartner, 1983\), etc. At sign-controlled intersections, a “Stop” or “Yield” sign is in place for drivers to pass through safely. The spatial–temporal conflicts can be reduced by assigning the right-of-way of vehicles in different moving directions at signal/sign-controlled intersections. Another type of intersection is uncontrolled intersections without traffic signals or signs, which are widely distributed in transport systems and are highly complex scenarios for human drivers and autonomous vehicles with more potential conflicts than controlled intersections. 

With the burgeon of autonomous driving technologies, autonomous control is gaining increasing attention in intelligent transportation systems to improve traffic efficiency and safety. There are two existing paths to control vehicles at uncontrolled intersections: \(1\) Vehicle-Infrastructure Cooperative Autonomous Driving \(VICAD\) and \(2\) Autonomous Driving Systems \(ADS\). VICAD is a road management system with a computing center that aims to achieve centralized control for connected and automated vehicles \(CAVs\). It enhances the perception of surrounding environments through vehicle-to-everything \(V2X\) technologies to help CAVs better interact with drivers, vehicles, and roads. The most popular method is Autonomous Intersection Management \(AIM\), which is a centralized intersection control strategy originally tailored for CAVs \(Chen et al., 2020; Levin & Rey, 2017; Wuthishuwong et al., 2015; Zhou et al., 

2022\). On the other hand, ADS is a decentralized single-vehicle control system for CAVs, which requires sensing equipment or V2V

communications to gather real-time data and adopt precise vehicular operation. With the increase in CAV number, it is anticipated that the mixed traffic flow of CAVs and human-driven vehicles \(HDVs\) will exist in the long-term future due to the large number of HDVs currently in use \(Jing et al., 2023; Saha & Motuba, 2023\). In the mixed-flow environment, centralized control \(e.g., AIM\) is not applicable for HDVs since HDVs cannot entirely comply with instructions transmitted by intersection managers. In contrast, decentralized control requires no centralized control facilities and decomposes a complex optimization process into multiple parallel simple decisions, reducing computing time and enhancing the practicality of solving multi-vehicle conflicts at uncontrolled intersections. 

Since the scenario of this study is the mixed-flow environment of HDVs and CAVs, we mainly focus on decentralized methods to model single-vehicle driving behavior and develop control strategies for individual vehicles. 

Interactions among vehicles are inevitable in the mixed-flow environment and should be investigated before designing decentralized control algorithms. Autonomous vehicles should not only perceive surrounding environments but also understand human interaction mechanisms to make socially compatible decisions and form an interaction-intensive and multi-agent system, which helps enhance the efficiency and safety of traffic systems. Since the decision-making of surrounding vehicles is unavailable and the actions are uncontrolled, it is hard to achieve efficient cooperation between CAVs and HDVs. Therefore, the optimal driving decision-making is usually a user equilibrium in mixed-flow interactions, i.e., each vehicle independently makes decisions by predicting the rivals’ future decisions to maximize personal benefit. 

Numerous approaches are proposed to explain and model interaction behavior, such as online verification methods \(Althoff et al., 

2009; Althoff & Dolan, 2014\), learning-based approaches \(Bautista-Montesano et al., 2022; Li et al., 2023\), and game-theoretic approaches \(Li et al., 2022; Rahmati et al., 2022\). Data-driven approaches \(such as online verification, deep learning, and reinforcement learning\) are usually used to generate end-to-end trajectory planning after training \(Bautista-Montesano et al., 2022; Xie et al., 2019\). 

However, data-driven approaches lack interpretability and cannot easily adapt to new driving scenarios \(Li and Pan, 2022\). On the other hand, game theory, as a mechanism-based approach, can treat other traffic participants as mutually dependent intelligent agents and make decisions from an individual perspective, which is widely used to analyze strategic reasoning in multi-agent systems and can provide an explainable explicit solution to model human interactions \(Wang et al., 2022\). 

This study aims to model multi-vehicle interactions and develop human-like decentralized control strategies at uncontrolled intersections in the HDV-CAV mixed-flow environment where “human-like” refers to generating reasonable driving behaviors similar to our human drivers. To achieve this objective, we propose a game-theoretic framework to model the interaction and provide control strategies for CAVs. The main contributions of this study are summarized as follows. 

\(1\) A game of incomplete information model is developed to better adapt to mixed-flow environments where some information might be unavailable. A driving style recognition algorithm is embedded into the proposed game-theoretic model to provide a decision-making basis for CAVs in interactions. 

\(2\) The proposed model can explain the mechanism in multi-vehicle interactions and be applied to future decision-making algorithms in ADS to deal with complex mixed-flow scenarios. Moreover, the existence of solutions has been proven to ensure the feasibility of applications. 

\(3\) The performance and validity of the proposed method are tested in simulations. The simulation results show that CAVs exhibit reasonable behavior expected in traffic and can reproduce real-world driving behavior. 

The remainder of this paper is organized as follows: Section 2 summarizes the relevant studies on uncontrolled intersection strategies with autonomous vehicles \(AVs\) and interaction modeling approaches. Section 3 interprets the proposed game-theoretic framework and formulates the multi-vehicle interactions at uncontrolled intersections. Section 4 conducts simulation experiments at an isolated uncontrolled intersection and analyzes the results. Section 5 summarizes some conclusions and suggestions. 

**2. Literature review**

This section introduces existing studies on uncontrolled intersection control algorithms with AVs and studies on inter-vehicle interaction models. 

2 

*D. Jing et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104835* 

*2.1. Uncontrolled intersection control strategy with AVs*

Multi-vehicle control strategies at an uncontrolled intersection in a CAV environment can be categorized into centralized and decentralized control strategies. In centralized control, decision-making is taken over by the intersection manager \(IM\), and vehicles have to completely conform to the globally optimal decisions made by IM \(de Campos et al., 2017; Levin & Rey, 2017; Liu et al., 2019; 

Wu et al., 2022\). The procedure can be summarized as follows: IM first receives requests from all CAVs, then optimizes trajectories and speed for CAVs, and finally returns control decisions to all CAVs. Notably, the objects of centralized control must be vehicles equipped with vehicle-to-infrastructure \(V2I\) devices. In decentralized control strategies, vehicles make decisions to maximize individual benefits based on some control policies and sensing information \(Rios-Torres & Malikopoulos, 2017\). Compared with centralized control strategies, decentralized control strategies require fewer complex operational settings and reduce significant computing re-sources and time \(Makarem & Gillet, 2013\). Therefore, decentralized control strategies have a higher readiness of technologies for near-future intersection management in the mixed-flow environment. 

Recently, many studies focused on decentralized control strategies for CAVs. For example, Malikopoulos et al. \(2018\) proposed a decentralized approach to control CAVs at uncontrolled intersections and derived conditions under which feasible solutions always satisfy all safety constraints. Zhang & Cassandras \(2018\) embedded dynamic resequencing in a decentralized optimal control framework to maximize traffic throughput. Liu et al. \(2019\) built a bi-level optimization model to plan trajectories for CAVs in the mixed-flow environment. A Lane-Changing Strategy Tree \(LCST\) and a Parallel Monte-Carlo Tree Search \(PMCTS\) algorithm were designed to solve the proposed model. Wu et al. \(2019\) modeled the multi-agent decision process using a reinforcement-learning approach to simulate the driving behavior of mixed-flow traffic. Zhang & Cassandras \(2019\) proposed a decentralized control strategy framework that vehicles solve individual optimal control problems with safety and comfort constraints. Mirheli et al. \(2019\)

developed a decentralized cooperative control method to optimize conflict-free trajectories for CAVs. A model predictive control \(MPC\) strategy was designed to let vehicles make a consensus. Yao & Li \(2020\) proposed a decentralized model to minimize travel time, fuel consumption, and safety risks for a single vehicle. Wang et al. \(2022\) optimized the trajectory in a mixed traffic environment along signalized arterial using a decentralized approach. Xu et al. \(2022\) proposed an approach to convert a multi-lane optimization problem into a decentralized optimal control and used a method combining optimal control and control barrier functions. 

Generally, most existing studies focused on control strategies in a pure CAV environment. However, traffic flow in the near future is more likely to be a mixed flow of CAVs and HDVs. Also, most studies modeled decentralized control strategies as an optimization problem from the individual perspective that lacked the consideration of multi-vehicle interactions \(Asadi & Vahidi, 2011; Huang & 

Peng, 2017; Wu et al., 2015\). However, influential factors in the decision-making process usually include surrounding environments and other vehicles’ decisions. It is hard to achieve precise control by single-vehicle optimization in multi-vehicle interactions. 

*2.2. Interaction modeling approaches*

In recent years, many studies \(particularly those concerning CAVs\) focused on inter-vehicle interactions and characterized the interactions using various methods. The main approaches include 1\) online verifications, 2\) learning-based approaches, 3\) partially observable Markov decision process \(POMDP\), and 4\) game-theoretic approaches. Online verification aims to predict the potential behavior of all objects in transport systems considering safety \(Althoff & Dolan, 2014\). As for learning-based approaches, 1\) deep learning uses vast amounts of historical data to generate end-to-end trajectory planning, and 2\) reinforcement learning trains an agent that best responds to various scenarios by interacting with the environment. Learning-based algorithms pursue better performance but lack an explanation of interaction mechanisms. POMDP models an agent decision process in which it is assumed that the system dynamics are determined by a Markov decision process with partially observed underlying states \(Sun et al., 2024\). POMDP’s policy builds a mapping between the history of observations \(or belief states\) and the actions. However, POMDP usually has high computational complexity \(Papadimitriou & Tsitsiklis, 1987\). 

Another approach to studying interactions is mechanism-based methods, such as game theory, which focuses more on explaining interaction behavior. Game theory is widely applied in various disciplines to reason and model the strategies of intelligent decision-makers, which is suitable for modeling the interaction between human drivers and CAVs \(Arbis et al., 2016; Liu & Zheng, 2010; 

Smirnov et al., 2021; Tian et al., 2022\). Game-theoretic approaches can model and provide an explainable, explicit, fast solution for interactions \(Wang et al., 2022\), which can be easily integrated with other optimization or learning-based models to enhance performance. 

Game-theoretic approaches are widely used in many studies to model the interaction at uncontrolled or signalized intersections. It can be classified into non-cooperative and cooperative games, with the key distinction being the absence or presence of binding agreements on optimal joint actions \(Bauso, 2014\). Players strive independently to find the best strategies and have no communication in non-cooperative games. For instance, Yang et al. \(2016\) built a multiple Nash Equilibrium to analyze the reduplicate dynamic game and used a genetic algorithm to solve the game at non-signalized intersections. Arbis et al. \(2016\) investigated the behavioral norm of interactions based on a non-cooperative game at a signalized intersection. They conducted a laboratory experiment to study the impact of risk attitudes and perceptions in crossing behavior. Chen et al. \(2020\) built an inference model for multi-type interactions by fuzzy logic at unsignalized intersections. They proposed a decision-making model based on a non-cooperative game that considered safety, efficiency, and comfort. Wang et al. \(2021\) modeled the competition as a Chicken game and proved the existence of pure-strategy Nash equilibria \(NE\) in non-cooperative games at unsignalized intersections. The proofs are instrumental in analyzing interactions in the mixed-flow environment. Rahmati et al. \(2022\) developed a dynamic non-cooperative game to model human decision-making to deal with the conflict with left-turning vehicles at intersections. The proposed models were calibrated and validated using a real-world 3 





*D. Jing et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104835* 

**Fig. 1. **Illustrations of three types of interactions \(CAV-CAV, HDV-CAV, and HDV-HDV interactions\). 

**Fig. 2. **Flowchart of the proposed game-theoretic framework. 

dataset. Li et al. \(2022\) proposed a framework of dynamic games based on a modified Nash Equilibrium model with multiple coexistent leader–follower pairs at uncontrolled intersections. A novel algorithm is proposed to fix the problem of collisions and deadlocks in failed interactions. Some studies also combined game-theoretic principles with learning-based models. For example, Albaba and Yildiz

\(2019, 2022\) proposed a framework combining hierarchical game theory with reinforcement learning to model the interaction of multiple human decision-makers. The proposed methods can be used in traffic simulators to test the planning and control algorithms of AVs.In brief, most existing studies characterized interactions as a dynamic game of complete information. However, CAVs are often unaware of other human drivers’ driving styles in interactions, leading to an inaccurate estimation of HDVs’ intentions. Real-time interaction data can be utilized to estimate human driving styles to help CAVs understand the decisions of surrounding agents

\(Koprulu & Yildiz, 2021\). Moreover, many studies recognized driving styles by learning-based approaches using historical interaction data, in which the input is unilateral driving characteristics. However, the driving style reflected in interaction decision-making has not been investigated thoroughly. 

4 



*D. Jing et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104835* 

**Fig. 3. **\(a\) Pseudocode of generating a leader–follower relationship for vehicles at intersections. \(b\) Example of sorting algorithm. 

**3. Mathematical models**

This study mainly aims to model the multi-vehicle interaction mechanism and develop optimal control strategies for CAVs at an uncontrolled intersection in the mixed-flow environment of CAVs and HDVs. Three distinct types of potential conflicts may occur in mixed-flow scenarios: \(1\) between two CAVs, \(2\) between a CAV and an HDV, and \(3\) between two HDVs, as shown in Fig. 1. 

Therefore, this study develops three types of models for different interaction environments. Although state information \(such as speed, position, etc.\) can be perceived or detected by sensing equipment, individual future decisions are unclear to other vehicles due to time delays or information confidentiality. In other words, each agent \(HDV or CAV\) decides to maximize the unilateral benefit considering the rivals’ possible decisions in multi-vehicle interactions, which can be regarded as a non-cooperative game. Moreover, vehicles at uncontrolled intersections should determine the right-of-way to reduce deadlocks and collisions, so we first design an interaction mechanism to model this process. 

The proposed game-theoretic method has three stages, as shown in Fig. 2:

1. The leader–follower relationship identification stage: The roles of leaders and followers at the intersection are first determined in the leader–follower game during the interaction stage. 

2. The interaction decision stage: The interaction decision stage includes CAV-CAV, HDV-CAV, and HDV-HDV interactions. In the decision stage, CAVs can dynamically recognize HDVs’ driving styles based on the information collected during the interaction. 

3. The control stage: The control variable is acceleration. 

In the model, some basic assumptions need to be satisfied. 

\(1\) CAVs with a low autonomy level and connected vehicles \(CVs\) are regarded as HDVs in the proposed model for simplicity since low-level CAVs are hard to handle complex interactions, and CVs are still entirely controlled by human drivers even if CVs are equipped with communication devices at uncontrolled intersections. 

5 

*D. Jing et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104835* 

\(2\) This study assumes that each vehicle pursues traffic efficiency and avoids collisions or deadlocks when a multi-vehicle conflict occurs. Thus, we model the interaction by a game-theoretic approach and optimize individual decision-making in complex dynamic interactions. 

\(3\) This study assumes that HDVs are conservative and pursue the maximum personal benefits considering the worst case. 

\(4\) This study assumes that CAVs’ driving styles can be adjusted manually by passengers and HDVs have inherent styles. Both can be generated by a uniform distribution in simulations. 

\(5\) This study assumes that the paths of vehicles inside the intersection are determined in advance according to the intersection’s geometry and the vehicles’ turning directions. 

*3.1. Leader-follower identification*

Section 3.1 introduces a leader–follower identification algorithm to model the passing priority in multi-vehicle interactions. 

Human drivers usually determine the passing priority through the First-Come-First-Served \(FCFS\) policy to solve potential conflicts at an intersection. Inspired by FCFS policy, this study develops a leader–follower identification algorithm for CAVs to determine the dominating relationship of pairwise vehicles in the game. Each CAV can collect information on other vehicles’ states and execute the leader–follower identification algorithm simultaneously with on-board devices. 

Define a pair of vehicles \( *i, j*\). The leader is *i * and the follower is *j *\(denoted as *i *≻ *j*\) if vehicle *i * is closer to the conflict zone than *j * or in the conflict zone. In multi-vehicle interaction scenarios, a vehicle might be both a leader and a follower in several pairwise relationships, so the global leader–follower relationship in the multi-vehicle interaction should be determined first to avoid collisions or deadlocks. For example, three vehicles *i*, *j*, *k * and the leader–follower relationships between two vehicles are *i *≻ *j*, *j *≻ *k*, *k *≻ *i*, which form a cyclic sequence. The cyclic sequence denotes a deadlock and should be eliminated to generate an acyclic sequence. Therefore, we design an algorithm to make a multi-vehicle consensus to determine the leader–follower relationship for all vehicles, which is shown in Fig. 3. 

The leader–follower role of each vehicle is rearranged in a global system. It implies that a leader in a leader–follower relationship might be a follower in another, and it must take actions that yield to the leader. For example, there are three pairs of interactions: A ≻ B, B ≻ C, and A ≻ C, and the relationship is A ≻ B ≻ C. For B, there exist two conflicts A ≻ B and B ≻ C. B considers the decisions in twice games and choose the action to ensure the follower role in A ≻ B. 

In Fig. 3 \(a\), L denotes a set of all leaders in each leader–follower pair, F denotes a set of all followers in each leader–follower pair, R

denotes the global leader–follower relationship, and r denotes a temporary leader–follower relationship in each iteration. The main idea of the pseudocode is as follows. First, extract all leaders in each leader–follower pair into set L, and all followers into set F. If a leader *li * is in L and is not in set F, and will be added in r. If the pairwise follower *fi * is not in L and not in r, it will be added in r. If r is an \(

\)

empty set, which denotes that the passing priority for each vehicle is equal, a random leader–follower pair *li, fi * will be added in r. 

Then eliminate all leader–follower pairs involved *li * from Q. Finally, add r in a set of leader–follower relationship R. Repeat the procedure until Q is empty. Fig. 3\(b\) shows a simple example of the leader–follower sorting algorithm. The initial set of leader-

–follower pair is \{\(1,3\), \(2,3\), \(2,1\)\}, so L is \{1, 2\}, and F is \{3, 1\}. For the element in L, 1 is in F, and 2 is not, so r is \{2\}. Then, eliminate the leader–follower pair that leader is 2 \(\(2,3\) and \(2,1\)\) from Q. Now Q is \(1,3\), and r is \{2, 1\}. The final global leader–follower relationship R is \{2, 1, 3\}. 

*3.2. Interaction mechanisms*

Section 3.2 explains the interaction mechanisms, including HDV-CAV and CAV-CAV interactions. The following sections interpret three components in the interaction mechanism models: the kinematic models \(Section 3.3\), payoff functions \(Section 3.4\), and driving style recognition algorithms \(Section 3.5\). 

*3.2.1. HDV-CAV interactions*

Payoff functions \(which denote the mathematical representation of the goals of a driver\) and driving styles in HDV-CAV interactions are unclear because there is no communication between CAVs and HDVs. Therefore, HDV-CAV interactions can be regarded as a game of incomplete information. The optimal actions for CAVs are the solutions of leader–follower games \(Stackelberg equilibrium\) with incomplete information. 

We assume HDVs make decisions by maximizing the worst-case reward, which is called a maximin strategy \(Li et al., 2022\). Let *i *∈

**N **be the index of a vehicle, and − *i * be all vehicles excluding *i*. Let *ai *∈ **A ** *i * be the action of vehicle *i *\(**A ** *i * is a set of all possible actions of vehicles\), and *s *∈ **S **be the current state of the two vehicles. HDVs’ decision-making can be modeled as equations \(1\)-\(3\). 

*a*\* *i *∈ argmax *u* ʹ *i*\( *s, ai*\)

\(1\)

*ai*∈**A ** *i*

\(

\)

*u* ʹ *i*\( *s, ai*\) = min *ui s, ai, a* ʹ *, *∀ *a* ʹ

− *i*

− *i *∈ *B*− *i*\( *s*\)

\(2\)

\{

⃒

\(

\)

\}

*B*

*a* ʹ

⃒ *u* ʹ *s*

\(3\)

− *i*\( *s*\) =

*, a* ʹ

≥ *u* ʹ

− *i *∈ **A **− *i*

− *i*

− *i*

− *i*\( *s, a*− *i*\) *, *∀ *a*− *i *∈ **A **− *i*

where *u* ʹ *i * is utility function with the prediction of the worst case for vehicle *i*, *B*− *i*\( *s*\) is the best response set for the rivals − *i*. Since the 6 



*D. Jing et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104835* 

**Fig. 4. **Extensive game with imperfect information. 

action of the rivals are unclear to vehicle *i * due to reaction delays or other reasons, vehicle *i * cannot immediately respond to the rivals’

actions. Therefore, we assume that vehicle *i * considers the worst case produced by the rivals to secure the utility \(so-called maximin strategy\). 

Similarly, HDVs’ actions in HDV-HDV interactions obey the rules in equations \(1\)-\(3\). 

CAVs’ decision-making in HDV-CAV interactions can be modeled as a game of incomplete information. Let Θ *i *\(Θ− *i*\) be a set of types for vehicle *i *\(or the rival vehicle − *i*.\), including two driving styles \(aggressive or cautious\). Let *p*\( *θi*\) be a joint probability distribution over driving styles. *ui *: S × Θ→R are payoff functions of all strategies with different driving styles for driver *i*. In the game of incomplete information, CAVs correct the probability of rivals’ types by observing HDVs’ actions in the previous decision epoch since the aggressiveness of HDVs is unknown. Let **K **be a time horizon that is sufficient for a pair of vehicles to pass through the interaction. The time horizon can be discretized as a set of equal time intervals: 0, 1, …, K, and the set of decision epochs is defined as **K **=

\(0 *, *… *, k, *… *, * K\). Let *pi*\( *θ*− *i*| *θi *\) be the prior joint probability distribution in the current belief of *i * for all drivers excluding *i*, *ak*− 1

− *i*

be an

\(

⃒

\)

action of the rival − *i * in previous decision epoch *k *− 1. ̃ *pi θ *⃒

− *i ak*− 1

represents the probability distribution that driver *i * considers other

− *i*

drivers belong to type *θ*− *i * by information *ak*− 1

− *i *. Thus, the optimal solution of the game of incomplete information *a*\* *i*\( *ai, θi*\) can be represented as equations \(4\)-\(5\). 

∑

\(

⃒

\)

*a*\*

⃒

*i *\( *ai, θi*\) ∈ argmax

̃

*pi θ ak*− 1 *u*

− *i*

− *i*

*i*\( *s, ai, a*− *i, θi*\)

\(4\)

*ai*∈**A ** *i θ*− *i*∈Θ− *i*

\(

\)

\(

⃒

\)

*pi ak*− 1

*pi*\( *θ*

̃

*p*

⃒

− *i *| *θ*− *i*

− *i*\)

*i θ*

*ak*− 1

\(

\)

\(5\)

− *i*

= ∑

− *i*

*p ak*− 1

*p*

*θ*

*i*

*i*\( *θ*− *i*\)

− *i *∈Θ− *i*

− *i *| *θ*− *i*

We adopt the Harsanyi transformation \(Harsanyi, 1967\) to transform the game of incomplete information into a game of complete but imperfect information, as shown in Fig. 4. In the Harsanyi transformation, a player named “nature” is introduced into a game of imperfect information to make the first move that chooses a type of driver in this game, and not everyone observes nature’s move. 

Since the driving style of HDVs is unclear to CAVs, two styles of HDVs might occur in the game. Aggressive styles will be chosen by nature with probability *p*, and cautious styles will be chosen with probability 1 − *p*. Assuming drivers have the same beliefs about the probabilities, only HDVs observes nature’s action. CAVs should respond to the two types of HDVs with different payoffs and take optimal actions. 

The existence of solutions in the proposed model can be ensured according to the propositions shown below, and detailed proofs are in Appendix section. 

**Proposition 1**. Pure-strategy Nash Equilibria \(NE\) for the noncooperative game always exists. 

The proof is in the Appendix section. 

**Proposition 2**. The solutions of a game of incomplete information with discrete strategy always exist if the number of player types is finite. 

The proof is in the Appendix section. 

*3.2.2. CAV-CAV interactions*

This study proposes a game of complete information to model CAV-CAV interactions, whose payoff functions are clear, and information is shared among connected autonomous vehicles \(CAVs\). We use the Stackelberg game to characterize the interaction, 7 





*D. Jing et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104835* 

**Fig. 5. **Illustration of two approaching vehicles at the potential conflict area. 

**Fig. 6. **Illustration of two types of conflict at an intersection: a LT conflict and a LL conflict. 

which assumes the existence of a hierarchical structure in the game. The follower establishes the best response set that optimizes the utility based on the leader’s action, after which the leader adjusts actions to maximize the utility based on the follower’s anticipated behavior. 

It is assumed that leaders take the best action with the consideration of the rational reaction of followers. The Stackelberg equi-

\(

\)

librium solution is *a*\* *i, a*\* , which can be represented as equations \(6\)-\(8\). 

− *i*

\(

\)

*a*\* *i *∈ argmax *ui s, ai, a* ʹ *, *∀ *a* ʹ

− *i*

− *i *∈ *B*− *i*\( *s*\)

\(6\)

*ai*∈**A ** *i*

\(

\)

*a*\*

*u s, a*\*

\(7\)

− *i *∈ argmax − *i*

*i , a*− *i*

*a*− *i*∈ *B*− *i*\( *s*\)

\{

⃒

\(

\)

\}

*B*

*a* ʹ

⃒ *u s*

\(8\)

− *i*\( *s*\) =

*, a* ʹ

≥ *u*

− *i *∈ **A **− *i*

− *i*

− *i*

− *i*\( *s, a*− *i*\) *, *∀ *a*− *i *∈ **A **− *i*

where *B*− *i*\( *s*\) is the best response set of followers − *i*. Followers can take actions to maximize the utility of possible actions of leaders. 

The following proposition should be proved to ensure the existence of solutions in the proposed model. 

**Proposition 3**. The solutions of Stackelberg Equilibrium \(SE\) are pure-strategy NE solutions if such condition is satisfied: the leader always takes acceleration actions unless reaching the speed limit, and the follower takes the best actions subject to the leader’s decision. 

8 

*D. Jing et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104835* 

The proof is in the Appendix section. 

*3.3. Kinematic models*

Section 3.3 interprets the kinematic model governing the movements of real-world vehicles, including speed, acceleration, and angle when passing through an intersection. 

Based on real-world traffic rules and laws, a vehicle’s movement is fixed once it travels in one lane. For example, HDVs in lane one will turn left but will not change lanes. CAVs can determine HDVs’ movements and find potential conflict points. Since vehicles travel on fixed paths, the decision variable is the acceleration in each decision epoch *k *∈ **K **. In this study, we take a two-lane uncontrolled intersection composed of a left-turning lane and a through-movement lane as an example to apply the proposed method, as shown in

Fig. 6. Let *a *∈ **A **= \{1 *, * 0 *, *− 1\} be the action, denoting that accelerating, taking no action, and decelerating, respectively. The speed update formula is as equation \(9\). 

\(

\(

\)

\)

*vki *= max min *vk*− 1

*i*

\+ *aki* Δ *vi* Δ *t, v* max *, * 0

\(9\)

where Δ *v * is the unit of variation of speed, this study is 2 m/s2 referred to \(Bokare & Maurya, 2017\). Term *aki* Δ *vi* Δ *t * represents the acceleration. For simplicity, we construct different speed by three distinct actions, as multiple acceleration/deceleration levels could be reflected as long as the time interval is shortened. For example, if the decision-epoch interval is 1 s, the acceleration space is \{ −

Δ *v, * 0 *, * Δ *v*\} in the future one second. If the decision-epoch interval is 0.5 s, the acceleration space is \{ − Δ *v, *− 0 *. * 5Δ *v, * 0 *, * 0 *. * 5Δ *v, * Δ *v*\} in the future one second. 

Let *sk*

∑ *k*− 1

*i *= *di *−

*l*=0 *vli* Δ *t, i *∈ **N ** *, l *∈ **K **be the clearance between vehicle *i * and the edge of the potential conflict area. *di * represent the length from the bumper at the initial position to the edge of the potential conflict area, as shown in Fig. 5. ∑ *k*− 1

*l*=0 *vli* Δ *t * represents the total

travel distance in decision epochs from zero to *k *− 1. We introduce an indicator to estimate average travel speed *vki * based on the decision in epoch *k * as equations \(10\)-\(11\). 

*tk*

*ski*

*i *= *vk*

\+ *k *⋅ Δ *t, i *∈ **N ** *, k, l *∈ **K**

\(10\)

*i *\+ *ε*

*vk di*

*i *= *t*

\(11\)

*ki*

where *tki * denotes the total travel time if the speed is *vki * at epoch *k*, *vki * denotes the average speed when vehicle *i * moves at speed *vki*, *ε * is a very small number. 

Three types of turning conflict points exist at intersections: \(1\) conflicts between through movements and through movements \(TT

conflicts for short, and as shown in Fig. 5\), \(2\) conflicts between left-turning movements and through movements \(LT conflicts for short\) and \(3\) conflicts between left-turning movements and left-turning movements \(LL conflict for short\). The turning trajectory is a quadrant in Fig. 6, the clearance of vehicle *i * from the conflict point can be calculated as equation \(12\). 

\(

\)

*ski *= *πr θ* 0 − *θki /* 180

\(12\)

where *θ* 0 is the maximum angle that vehicles can turn when the left-turning conflict occurs. *θki *∈ \(0 *, * 0 *. * 5 *π*\] is the current angle of vehicle *i * at epoch *k*. 

In the case of LT conflict in Fig. 6, *θ* 0 is calculated as equation \(13\). 

\(\(⃒

⃒

\)

\)

⃒

⃒

*θ* 0 = arcsin

⃒ *y* o − *y*

*/*\( *r *\+ 0 *. * 5 *w*

\(13\)

*i*

c *ij *⃒ − 0 *. * 5 *wj*

*i*\)

where *wi * and *wj * is the width of vehicle *i * and *j*, respectively. 

\(

\)

Let o *i *∈ O be the center of the quadrant of vehicle *i*’s trajectory, with *x* o *, y * be its coordinate. Let c *i*

o *i*

*ij *∈ C be the conflict point, with

\(

\)

\(

\)

*x* c *, y*

be its coordinate. Let

*e*

be the maximum angle of left-turning vehicle *i * on its edge *e*

*ij*

c *ij*

*θ* 0 *i, ej*

*i * from the conflict point formed by

\(

\)

trajectory *ei * and trajectory *ej*. *θ* 0 *ei, ej * can be represented when *j * moves in east–west direction as equation \(14\). 

⎧

\(\(⃒

⃒

\)

\)

⎪

⎪

⃒

⃒

⎪ arccos

⎪

⃒ *y* o − *y*

*/*\( *r *− 0 *. * 5 *w*

*, *

*i*

c *ij *⃒ \+ 0 *. * 5 *wj*

*i*\)

\(

\)

⎨

*θ*

if *i * is northeastward

\(\(⃒

⃒

or southwestward

\)

\)

0 *ei, ej *=

\(14\)

⎪

⃒

⃒

⎪ arcsin

⎪

⃒ *y* o − *y* c ⃒ − 0 *. * 5 *wj /*\( *r *\+ 0 *. * 5 *wi*\) *, *

⎪

*i*

*ij*

⎩

otherwise

\(

\)

*θ* 0 *ei, ej * can be represented when *j * moves in north–south direction as equation \(15\). 

9 

*D. Jing et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104835* 

⎧

\(\(

\)

\)

⎪

⃒

⃒

⎪

⎪ arcsin

⃒ *x*

⃒

⎪

o − *x*

− 0 *. * 5 *w /*\( *r *\+ 0 *. * 5 *w*

*, *

*i*

c *ij*

*j*

*i*\)

\(

\)

⎨

*θ*

if *i * is northeastward

\(\(⃒

⃒

or southwestward

\)

\)

0 *ei, ej *=

\(15\)

⎪

⎪ arccos

⃒ *x*

⃒

⎪

o − *x* c

\+ 0 *. * 5 *wj /*\( *r *− 0 *. * 5 *wi*\) *, *

⎪

*i*

*ij*

⎩

otherwise

\(

\)

\(

\)

Let *d* sg *i ei, ej * be the clearance of through-movement vehicle *i * on its edge *ei * from the conflict point formed by *ei * and *ej*. *d* sg *i ei, ej * can be calculated as equation \(16\) when *i * moves in east–west direction. 

̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅

√

̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅

\(

\)

\(

\)

\( \)

\(

\( \)

\)

\(

\( \)

\)2

*d* sg

2

*i*

*ei, ej *= *ψ*\( *ei*\) *x* o − *x *− 0 *. * 5 *l*

*e*

*r *− *ψ e * 0 *. * 5 *w*

−

*y *− *y*

*e * 0 *. * 5 *w*

\(16\)

*j*

*i*

*i *\+ *ψ*

*j*

*j*

*j*

o *j*

*i *\+ *ψ*

*j*

*i*

\( \)

\( \)

where *ψ*\( *ei*\) = 1, if *ei * is eastward; otherwise, *ψ*\( *ei*\) = − 1. *ψ ej *= 1, if *ej * is northeastward or southeastward, otherwise, *ψ ej *= − 1. 

\(

\)

Similarly, *d* sg *i ei, ej * can be calculated as equation \(17\) when *i * moves in the north–south direction. 

̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅

√

̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅̅

\(

\)

\(

\)

\( \)

\(

\( \)

\)

\(

\( \)

\)2

*d* sg

2

*i*

*ei, ej *= *ψ*\( *ei*\) *y* o − *y *− 0 *. * 5 *l*

*e*

*r *− 0 *. * 5 *ψ e w*

−

*x *− *x*

*e w*

\(17\)

*j*

*i*

*i *\+ *ψ*

*j*

*j*

*j*

o *j*

*i *\+ 0 *. * 5 *ψ*

*j*

*i*

\( \)

\( \)

where *ψ*\( *ei*\) = 1, if *ei * is northward, otherwise, *ψ*\( *ei*\) = − 1. *ψ ej *= 1, if *ej * is northeastward or southeastward, otherwise, *ψ ej *= − 1. 

In the case of LL conflict in Fig. 6, the maximum angle can be denoted as equation \(18\). 

\(⃒

⃒

\)

⃒

⃒ ⃒

⃒

\(

\)

*θ*

⃒

⃒

0 = arctan ⃒ *y* c − *y*

*x *− *x*

− arctan 0 *. * 5 *w*

\(18\)

*ij*

o *i *⃒ */ * c *ij*

o *i*

*j/r*

*3.4. Payoff functions*

Section 3.4 explains the designed payoff functions. The main factors that drivers and passengers care about are efficiency and safety in payoff functions. Therefore, a weighted-sum function considering efficiency and safety is used to evaluate the benefit of each action. 

Efficiency is reflected in the average speed when vehicles pass through the intersection, and a higher speed denotes greater efficiency. To distinguish aggressive drivers and cautious drivers, we assume that aggressive drivers have a convex utility function, while cautious drivers have a concave utility function \(Maschler et al., 2021\). It can make the utility of aggressive drivers higher than that of cautious drivers under the same average speed. We also set different parameters in equation \(19\) to distinguish two styles. 

\(

\)

\(

\)

U

*α* 1

speed *aki *= *λ* 1 1 \+ *vk*

\(19\)

*i /v* cri

where Uspeed is the utility of speed, which denotes the satisfaction of speed. *α* 1 *> * 0 is a preset sensitivity parameter to measure the utility of speed. This study defines *α* 1 *, * agg and *α* 1 *, * cau to represent aggressive and cautious styles, respectively. If the driver is aggressive, *α* 1 = *α* 1 *, * agg; otherwise, *α* 1 = *α* 1 *, * cau. The term 1 \+ *vki/v* cri in the exponential function is always greater than 1, which can avoid the case that the utility of aggressive drivers is less than a cautious driver if *vki/v* cri *< * 1. *λ* 1 *> * 0 is a scaled factor to magnify the value of Uspeed, which reflects the degree of preference in benefit. *v* cri is an expected speed. *vki * is the average travel speed which represents in equation \(11\). 

One commonly used indicator for quantifying safety is time to collision \(TTC\) \(Arvin et al., 2020; Bonela & Kadali, 2022\). TTC

represents the level of the imminent danger of collisions and a higher TTC denotes a safer driving environment. In the scenario of intersections, TTC is the time to potential conflict point of each vehicle. TTC of vehicle *i * at epoch *k * can be calculated as equation \(20\). 

⎧

⎪

⎪

*sk*

*sk*

*sk*

⎨

*ski*

*j*

*sk*

*j *\+ *wi*

*j*

*sk*

*, * if

*< *

*i*

*< *

or *ski < *

*< i *\+ *wj*

TTC *k*

*vk*

*vk*

*vk*

*vk*

*vk*

*vk*

*vk*

*i *=

\(20\)

⎪ *i *\+ *ε*

*j *\+ *ε*

*i *\+ *ε*

*j *\+ *ε*

*i *\+ *ε*

*j *\+ *ε*

*i *\+ *ε*

⎪

⎩

M *, * otherwise

where *ski * is the clearance of vehicle *i * in decision epoch *k * to the conflict point. *wi * is the width of vehicle *i*. *vkj * is the speed of leader *j*. M is a very large positive value. *ε * is a very small positive value to avoid a zero denominator. The upper formula in equation \(20\) corresponds to the cases that potential conflicts exist, and the lower formula corresponds to the cases without conflicts. 

We design a safety payoff function using an exponential function to capture sensitivity as equation \(21\). 

\(

\)

Usafe *aki *= *λ* 2 *e*\(TTCmin− TTC *ki*\)

\(21\)

where Usafe is the utility of safety, which denotes the satisfaction of safety.TTCmin is the minimum time-to-collision, which denotes the safety threshold. If TTC *ki * is less than TTCmin, it is regarded as a “dangerous” case for drivers; otherwise, it is considered as a “safe” case. 

*λ* 2 is a negative number as an amplification coefficient and can reflect different driving styles, i.e., *λ* 2 of aggressive drivers is higher than cautious drivers. This study defines *λ* 2 *, * agg and *λ* 2 *, * cau to represent aggressive and cautious styles, respectively. If the driver is aggressive, *λ* 2 = *λ* 2 *, * agg; otherwise, *λ* 2 = *λ* 2 *, * cau. 

We use a weighting factor representing driving styles to combine efficiency and safety utility. Driving styles significantly impact 10 



*D. Jing et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104835* 

**Fig. 7. **Total utility of the leader’s three kinds of actions \(acc., no., dec.\) under different weighting factors \(the red dotted line denotes the highest utility under different actions\). \(For interpretation of the references to colour in this figure legend, the reader is referred to the web version of this article.\)

driving decisions and maneuvers, representing individual instantaneous preferences or long-term driving habits \(Elander et al., 1993; 

Ishibashi et al., 2007\). Depending on aggressiveness or cautiousness, driving styles are predominantly categorized into two or three types: aggressive, cautious, and neutral \(Ma et al., 2021; Mohammadnazar et al., 2021\). This study classifies driving styles into two types: aggressive and cautious. Aggressive drivers focus more on efficiency during travel at intersections, while cautious drivers focus more on safety. 

The total utility function represents as equation \(22\). 

\(

\)

\(

\)

\(

\)

U *aki *= *ωi* Uspeed *aki *\+ \(1 − *ωi*\)Usafe *aki*

\(22\)

where *ωi *∈ \(0 *, * 1\) is the weighting factor to measure the importance of the two indicators \(efficiency or safety\) of vehicle *i*. Drivers with a larger value of *ωi * care about efficiency more and can be considered more aggressive; otherwise, they can be considered cautious. 

*3.5. Driving style recognition*

Section 3.5 introduces a driving style recognition algorithm to help CAVs infer rivals’ possible driving styles in HDV-CAV interactions. CAVs can estimate the probability of different styles of HDVs \(i.e., aggressive or cautious\) using the driving style recognition algorithm with the information on HDVs’ actions collected in inter-vehicle interactions. 

Kinematic characteristics such as speed and acceleration can reflect human driving styles \(de Zepeda et al., 2021; Ma et al., 2021\). 

This study proposes an approach to infer human driving styles based on the game-theoretic model with real-time collected action information. Since the perception and computing power of CAVs is usually stronger than that of human drivers, we assume that CAVs can utilize the real-time actions of HDVs to recognize driving styles. In contrast, human drivers do not have the ability. HDVs calculate the utility based on specified weights and take the actions with the highest total utility. CAVs estimate weights ̃ *ωki * in epoch *k * based on HDVs’ action in the previous decision epoch *k *− 1 and HDV’s utility functions. The estimation procedure is based on the proposed game-theoretic framework \(represented as equation \(23\)\) and can be described as follows. 

\(1\) Collect the real-time actions of surrounding vehicles. 

\(2\) Infer the upper and lower bounds of HDVs’ possible driving styles using the collected information. 

\(3\) Correct the weighted factor using Bayesian theory. 

\{

\(

⃒

\) \}

̃

*ωk*

⃒

*i *∈ argmax U *i ωi ak*− 1

*, *∀ *ak*− 1

− *i*

− *i*

∈ **A **− *i*

\(23\)

*ωi*

\(

⃒

\)

where U *i ωi*⃒ *ak*− 1 is utility function with *ω*

− *i*

*i *∈ \(0 *, * 1\) based on action *ak*− 1

− *i*

in decision epoch *k *− 1. The utility functions with different *ωi*

are compared, and drivers finally take actions with maximum utility. Therefore, the upper and lower bound of *ωi * can be inferred with the maximum-utility theory. Since multiple CAVs can collect the information from an HDV simultaneously, ̃ *ωki * estimated by information *ak*− 1

− *i*

is shared in CAVs, and the upper and lower bound of *ωi * in decision epoch *k * can be updated as equations \(24\)-\(25\). 

\[

\(

\{

\}

\{

\} \)

\(

\{

\}

\{

\} \) \]

̃

*ωki *∈ max inf ̃ *ωki , * inf ̃ *ωk*− 1

*i*

*, * min sup ̃

*ωki , * sup ̃ *ωk*− 1

*i*

\(24\)

̃

*ω* 0 *i *∈ \[0 *, * 1\]

\(25\)

where inf\{ ⋅ \} denotes the infimum of ⋅, and sup\{ ⋅ \} denotes the supremum of ⋅. ̃ *ω* 0 *i * denotes the range of the initial weighting factor. 

11 

*D. Jing et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104835* 

Then, we use equation \(5\) to estimate the probability of aggressive style. Fig. 7 illustrates the utility functions of three actions \(acc., dec., no actions\) under all possible weighting factors \(0 ~ 1\). The neutral weighting factor *ω*\* is set as 0.5. *ωi *≤ *ω*\* denotes that the driving style is cautious, and *ωi > ω*\* denotes that the driving style is aggressive. If a CAV observes an HDV takes no actions, the HDV’s weighting factor must fall into the range of 0.43 ~ 0.67. The probability of cautious style is 0.5–0.43 = 0.07, and the probability of aggressive style is 0.67–0.5 = 0.17. The prior probability distribution of the leader *pi * is set as 0.5. Therefore, the posterior probability ̂ *pi* is 0.17\*0.5/ \(0.17\*0.5 \+ 0.07\*0.5\) = 0.71 according to equation \(5\), which means CAVs correct the probability of aggressiveness of the HDV from 0.5 to 0.71 based on the information in the previous decision epoch. 

**4. Experiments and results**

In Section 4, we first calibrate the parameters and design several simulation tests to verify the performance of the proposed model. 

Next, the reproduction of real-world trajectory is verified. Finally, several simulations are conducted to test the performance of human-like driving strategies in the mixed-flow environment. 

The simulation scenario is an isolated two-lane uncontrolled intersection, and the traffic is simulated using Simulation of Urban Mobility \(SUMO\), an open-source microscopic traffic simulation software \(Lopez et al., 2018\). The control area of CAVs is a circle whose center is the geometric center of the intersection, and the radius is rc = 20m, as shown in Fig. 1. The length and width of vehicles are 6 m and 1.6 m, respectively. Since human perception has limitations, we set the perception range of HDVs to be 5 m in this study

\(Nemchinov et al., 2020\). 

*4.1. Parameter calibration*

The parameters in payoff functions are calibrated based on the INTERACTION dataset \(Zhan et al., 2019\) to capture human characteristics and help CAVs take human-like actions. We extract 49,494 pieces of interaction data, including speed, clearance, and action, from the raw dataset. The parameters are estimated using the Bayesian Optimization \(BO\) approach, which optimizes black-box functions using probabilistic surrogate models commonly used for setting hyperparameters \(Boender & Mockus, 1991\). It considers the problem as equation \(26\). 

***x***\* = argmax *f*\( ***x***\)

\(26\)

***x***∈ ***X***

where *f * is a function to evaluate any arbitrary parameter vector ***x ***∈ ***X***, which leads to noise-corrupted observations as equation \(27\). 

***y ***= *f*\( ***x***\) \+ ***ε***

\(27\)

\(

where ***ε ***∼ ***N *** 0 *, σ* 2\) is the zero-mean Gaussian distributed noise. BO places a surrogate model on *f * and generates an acquisition \(

\)

function. Define the historical data set at iteration *t * as ***D**t *= \{\( ***x**τ, **y***

***x***

will be

*τ *\)| *τ *∈ \{0 *, * 1 *, *… *, t *− 1 *, t*\} \}. Then, a new solution *t*\+1 *, **y**t*\+1

selected in the function as equation \(28\). 

***x**t*

*f* ʹ

\+1 = argmax \( ***x***; ***D**t *\)

\(28\)

***x***∈ ***X***

\(

\)

The action space \(acc., no., dec.\) is converted into a probability distribution vector ***p ***= *pa , p , p *. If a human driver chooses one 1

*a* 2

*a* 3

of the actions in the action space, the probability of the action is 1; otherwise, it is 0. For example, the probability distribution is ***p ***=

\(1 *, * 0 *, * 0\) if a driver decides to accelerate. The probability with the estimated parameters ̂ *pa * can be calculated by a Logit Model, *n*

represented as equation \(29\). 

*e* ˆ *uan*\( ***x***\)

̂

*pa*

∑

\(29\)

*n *=

*a*

*e* ˆ *uan*\( ***x***\)

*n*∈**A**

The accuracy of the probability with the estimated parameters can be calculated as equation \(30\). 

\(

\)

1 ∑

M

∑

|**A **| \(

\)2

*η *= M

1 - 1

̂

*pa*

\(30\)

*n,m *−

*pan,m*

*m*

|**A **|

=1

*n*=1

where *η * is the accuracy of the probability with the estimated parameters, *n * is the index of actions, and |**A **| is the size of the action space. 

*m * is the index of data, and M is the size of the testing dataset. ̂ *pan,m * is the estimated probability of *an * while *pan,m * is the true probability in data *m*. 

\(

\)

The parameter vector ***x ***= *λ* 1 *, λ* 2 *, * agg *, λ* 2 *, * cau *, α* 1 *, * agg *, α* 1 *, * cau *, v* cri *, * TTCmin is calibrated based on the BO approach. The value of each element in ***x *** is set in a reasonable range. 80 % of the data is randomly extracted as a training dataset, and the rest is used to form the corresponding testing dataset. The total number of iterations is set as 200. The final optimal parameter vector is \(9 *. * 79 *, *− 2 *. * 45 *, *− 3 *. * 82 *, * 1 *. * 77 *, * 0 *. * 98 *, * 1 *. * 03 *, * 8 *. * 86\). Also, we record the action at each timestep calculated by the calibrated model and calculate the matching rate between the action at each timestep in simulations and the testing dataset using equation \(30\). The average accuracy *η * is 82.6 %, which verifies that the calibrated model can help CAVs take human-like actions. 

12 



*D. Jing et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104835* 

**Fig. 8. **Reproducing real-world multi-vehicle interactions at intersections using the calibrated model. Subfigures a1-a4 \(b1-b4\) are simulations in a TT \(LT\) conflict scenario, and subfigures A1-A4 \(B1-B4\) are real-world trajectories in a TT \(LT\) conflict scenario. 

*4.2. Simulation and analysis*

In simulations, vehicles are placed at the beginning of road segments, and the initial speed is set as 0 m/s. Then, we simulate traffic under different travel demands, penetration rates of CAVs, and lane arrival symmetry. We also test the performance of the proposed driving style recognition algorithm. 

*4.2.1. Reproducing real-world scenarios*

We verify whether the calibrated model can reproduce and model real-world human driving behavior. The positions of vehicles in simulations are plotted in Fig. 8, which includes two scenarios: TT conflict \(a1-a4\) and LT conflict \(b1-b4\). The real-world trajectories are plotted: A1-A4 denote TT conflict, and B1-B4 denote LT conflict. The key features in simulations are consistent with those in the real-world dataset. Fig. 8 shows vehicles can make a consensus in multi-vehicle interactions and yield to the leader. In the TT conflict scenario, car 3 prepares to cross the intersection and moves quickly. Car 1 and car 2 move at a low speed. Then car 3 keeps moving, and cars 1 and 2 are waiting at the entry to let car 3 pass first. In the LT scenario, car 2 decelerates and lets car 1 pass first. No collisions or deadlocks happen in this process, which indicates that vehicles can interact efficiently when potential conflict occurs. 

Comparative results imply that the calibrated model can reproduce human-like actions in real-world interactions at an acceptable

∑M

accuracy. The matching rate is calculated with formular *p* match = *m*=1 *κm*

M

⋅ 100% where *κm * is an indicator \( *κm*=1 if the error between

13 





*D. Jing et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104835* 

**Fig. 9. **Demonstration of five-vehicle interactions. 

**Fig. 10. **Speed and acceleration in five-vehicle interaction. 

14 





*D. Jing et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104835* 

**Fig. 11. **Space-time diagram of vehicles on two potentially conflict directions. 

**Fig. 12. **Case of aggressiveness estimation and driving style recognition. 

simulation and real-world data is lower than 5 %; else, *κm*=0\). The matching rate is about 80 %, which verifies the effectiveness of the proposed model. Consequently, we apply the calibrated model to other scenarios. 

*4.2.2. Multi-vehicle interactions*

Next, we test the performance of the proposed algorithm in dealing with complex multi-vehicle interactions. We record the kinematic states of five vehicles, as illustrated in Figs. 9 and 10. 

Fig. 9\(a\) shows five potential conflict points at the intersection. We record the conflict pair denoted by pairs of vehicle IDs: 1–2, 1–5, 2–3, 3–4, and 4–5. In the multi-vehicle system, cars 2 and 5 are leaders so they can pass through the intersection first. Cars 1, 3, and 4 have to yield to cars 2 and 5. The interaction is reproduced in Fig. 9\(a\)-\(d\). 

When cars 2 and 5 exit the intersection, cars 1, 3, and 4 can determine the right-of-way again. Since car 4 is closer to the conflict point than car 3, car 4 is the leader and can pass first. Car 3 slows down and waits for car 4 to pass first. The interaction is reproduced as

Fig. 9\(e\)-\(g\). 

In Fig. 9\(h\)-\(i\), no potential conflict points are at the intersection, so cars 1, 3, and 4 can drive freely. 

In Fig. 10, the upper subfigure shows the variation in speed, while the lower subfigure represents the variation in acceleration, 15 



*D. Jing et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104835* 

**Fig. 13. **Driving style recognition accuracy and action prediction accuracy. 

corresponding to the decisions in Fig. 9. Car 2 and 5 are leaders, so the speed is not affected. Car 3 continues to decelerate from 130 to 170 timesteps, which indicates that car 3 is the follower, and the speed is affected by other vehicles. Figs. 9 and 10 show that the proposed method can enhance traffic efficiency and ensure safety in a multi-vehicle interaction. 

*4.2.3. Space-time diagrams*

To test the safety performance of the proposed method, we record the clearance of vehicles from two conflict directions in 3000

timesteps. In Fig. 11, the solid green lines denote the trajectories of vehicles in lane 4, the solid blue lines denote the trajectories of vehicles in lane 7, and the shadow area \(width is 3 m\) denotes the conflict zone at point 2 \(as shown in Fig. 7\). 

The initial distance to the conflict point on lane 7 is − 20 m, and on lane 4 is 20 m. Vehicles on two lanes will move towards the conflict point \(y = 0\). If the point of intersection of the trajectories of two vehicles is in the conflict zone \(shadow area\), a collision will happen; otherwise, no collisions will happen. In Fig. 11, no points of intersection are in the conflict zone, which means no collision happens at the conflict point. CAVs can take reasonable actions to avoid collisions based on the proposed method. 

*4.2.4. Algorithm performances*

\(1\) Style recognition performance

To test the performance of the proposed driving style recognition approach, we record HDVs’ aggressiveness captured by CAVs and the probability of aggressive style, as shown in Fig. 12. For example, cars 1 and 2 are both cautious in Fig. 12 \(a\). The true aggressiveness of cars 1 and 2 is 0.45 and 0.25, respectively. The estimated upper bound of car 1′s aggressiveness drops to under 0.5, and the lower bound rises to more than 0.4. The true aggressiveness is between the estimated upper bound and lower bound. The probability of aggressive style drops to about 10 % at the fifth timestep, which means the probability that the target vehicle is aggressive is about 10

%. Similarly, the estimated upper bound of car 2 drops to about 0.5, and the probability of aggressive style drops to about 30 %. 

Fig. 12\(b\) shows a case of two aggressive HDVs. The true aggressiveness of cars 1 and 2 is 0.81 and 0.9, respectively. The estimated lower bound of car 1′s aggressiveness rises to above 0.8, and the estimated lower bound of car 2′s rises to above 0.75. The probability of aggressive style rises to about 90 %, which means the probability of aggressive style is about 90 %. Similarly, the estimated upper bound of car 2 rises to about 0.75, and the probability of aggressive style rises to about 90 %. 

The results indicate that the proposed approach can recognize the driving style and estimate HDVs’ aggressiveness after several epochs of interactions. 

We set the probability of aggressive style in the population at 50 % and simulate traffic in an hour. Fig. 13 shows the accuracy of driving style recognition and action prediction. In the top subfigure in Fig. 13, we compare the estimation accuracy of the proposed recognition approach with that of no recognition. It is judged as correct if the estimated probability of aggressive style is higher than *ω*\*

and the aggressiveness is higher than *ω*\*. The results show that the accuracy of the proposed algorithm is about 95 %, while that of no recognition is about 50 %. In the bottom subfigure, the accuracy of action prediction is about 90 %, while that of no recognition is 16 





*D. Jing et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104835* 

**Fig. 14. **Comparison among the proposed method, signal control, and sign control. \(a\) Low-demand scenario. \(b\) High-demand scenario. 

**Fig. 15. **Statistic at intersections under different levels of penetration rate of CAVs. 

about 60 %. 

\(2\) Control strategy performance

The control strategy performance is compared in different scenarios: 1\) CAVs equipped with the proposed control strategy, 2\) all vehicles follow the control of traffic signals, and 3\) all vehicles follow the control of stop signs. The traffic demand is set as 300vph/lane \(low demand\) and 600vph/lane \(high demand\). For the scenario with traffic signals \(scenario 2\), one cycle of traffic signal includes four phases \(North-South directions: \(1\) through and \(2\) left-turning movement; West-East directions: \(3\) through and \(4\) left-turning movement\). The cycle time is 65 or 112 s, and the green signal time is 14 or 25 s in each direction in low or high-demand scenarios calculated using Webster’s methods \(Webster, 1958\). The scenario with stop signs \(scenario 3\) follows the rule that vehicles on sub-arterial roads \(West-East directions\) yield to those on arterial roads \(North-South directions\), and CAVs yield to HDVs. The total simulation time in each simulation run is 15 minutes and the penetration rate of CAVs is set as 50 %. 

The average travel speed and throughput are recorded, as shown in Fig. 14. In Fig. 14\(a\), the average speed of vehicles at intersections is about 10 m/s, 5 m/s, and 3 m/s with the proposed method, sign control, and signal control, respectively. In Fig.14\(b\), the average speed of vehicles at intersections is about 5 m/s, 2 m/s, and 2 m/s with the proposed method, signal control, and sign control, respectively. The throughput per minute is about 80veh, 50veh, and 40veh with the proposed method, signal control, and sign control. 

The result indicates that: \(1\) CAVs can utilize the spacing more efficiently in interactions using the proposed method. \(2\) Signal control might bring a longer waiting time than sign control in low-demand scenarios, leading to a waste of traffic capacity. \(3\) Sign control cannot deal with heavy traffic since many conflicts occur in high-demand scenarios, which is more suitable for low-demand 17 





*D. Jing et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104835* 

**Fig. 16. **Statistic at intersections under different levels of traffic demand. 

**Fig. 17. **Statistic at intersections under different lane arrival symmetry of traffic. 

scenarios. 

Overall, the proposed algorithm outperforms the other two methods. The comparison results imply that the proposed method can improve the multi-vehicle interaction and help CAVs adjust speed more reasonably. 

*4.2.5. Sensitivity analysis*

In this section, we investigate how variable parameters, such as the penetration rate of CAVs, vehicle arrival on each lane, and lane arrival symmetry, affect macroscopic traffic flow. 

In the scenarios of different penetration rates of CAVs, we set the vehicle arrival rate as 900 vph/lane. In Fig. 15, speed and throughput increase, whereas delay and queue length decrease as the penetration rate increases. In 100 % CAV scenarios, the average speed reaches about 8 m/s, and the throughput is 120 vehicles per minute \(7200 vph\), much higher than in other scenarios. On the other hand, delay and queue length are zero. The result shows that a higher penetration rate of CAVs can enhance traffic efficiency and achieve an efficient interaction with HDVs. 

In the scenarios of different traffic demands, the penetration rate of CAVs is set at 50 %. As shown in Fig. 16, a higher traffic demand leads to a decrease in speed and throughput and an increase in delay and queue length. In the 300 vph/lane \(2400vph\) demand scenario, the average speed is about 10 m/s, and throughput is 40 vehicles per minute. In the 400 vph/lane \(3200vph\) scenario, the average speed fluctuates between 10 m/s and 3 m/s, which indicates that a synchronized flow occurs now. When the demand is higher than 400vph/lane, the average speed remains at about 2.5 m/s, which indicates that a large-scale congestion occurs at intersections. 

Furthermore, we simulate traffic under different lane arrival symmetry. The total traffic arrival is 600 vph/lane, and the 18 



*D. Jing et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104835* 

**Fig. 18. **Degree of collision risks vs. CAV penetration under different traffic demand. 

penetration rate of CAVs is 50 %. Fig. 17 shows the simulation results. E25-S25-W25-N25 means the arrival on each incoming lane occupies 25 % of the total arrival. We also test E35-S15-W35-N15 and E50-S25-W15-N10 scenarios. The traffic efficiency in scenario E50-S25-W15-N10 is higher than others, implying that asymmetric arrivals could reduce delays and queue length and improve traffic efficiency at uncontrolled intersections. 

*4.2.6. Safety evaluation*

A quantitative indicator called degree of collision risks *d* risk is defined to evaluate safety in simulations, as equation \(31\). A smaller value of *d* risk denotes a lower risk of collisions. 

∑

∑

*d*

*i*

*ν*

∈

*k*∈

*i,k*

risk =

**N**

**K**

K

\(31\)

total

where *νi,k *= 1 if vehicle *i * will collide potentially with other vehicles in decision epoch *k*; otherwise, *νi,k *= 0. Ktotal is the total number of decision epochs of all vehicles in the simulation. 

In Fig. 18, the statistics show that collision risk decreases with decreasing traffic demands and increasing CAV penetration rates, which indicates that the proposed algorithm can improve the safety and performance of interactions at intersections. 

**5. Conclusions**

This study proposes a non-cooperative game-theoretic framework to model the interaction behavior at an isolated uncontrolled intersection. The proposed model can be used to provide decentralized control strategies for CAVs in the decision-making process to achieve better interaction and explain human driving behavior, which is practical in future uncontrolled intersection management of mixed traffic flow. Compared with the conservative control strategy \(i.e., CAVs yield to HDVs\), the proposed control can help CAVs utilize the gap and take more human-like actions to enhance traffic efficiency while ensuring safety. 

A leader–follower identification algorithm is first developed for CAVs to assign a hierarchical passing priority and prevent deadlocks and collisions based on FCFS rules. Different interaction mechanisms \(HDV-CAV, CAV-CAV, and HDV-HDV interactions\) are designed to provide control strategies and are more adaptative in mixed-flow environments. A non-cooperative leader–follower game of incomplete information framework is applied in HDV-CAV interactions to tackle the uncertainty of human driving styles and help CAVs predict human actions accurately. A driving style recognition approach is also proposed to estimate the aggressiveness of HDVs based on kinematic information collected during interactions. CAV-CAV interaction is modeled as a non-cooperative leader–follower game of complete information, and HDV-HDV interaction is modeled as a Nash game. The existence of NE and SE is proved to ensure the feasibility of the proposed method in real-world applications. 

A simulation platform based on SUMO is built to verify and test the control performance of the proposed model. Parameters are calibrated in payoff functions based on a real-world dataset, guiding CAVs to take human-like actions. Traffic is simulated at an isolated two-lane intersection, a typical scenario in urban transport systems. The simulated trajectories are close to true trajectories, which indicates that the proposed model can reproduce real-world scenarios. Then, the sensitivity of different parameters is analyzed, including the penetration rate of CAVs, traffic demand, and lane arrival symmetry. The results show that \(1\) CAVs can more reasonably determine whether to yield or not while ensuring safety when competing for the right of way with HDVs using the proposed human-like strategies compared with conservative strategies, \(2\) a higher penetration rate of CAVs can improve traffic efficiency and safety at uncontrolled intersections, and \(3\) asymmetric lane arrival is helpful for vehicles to solve conflicts. 

In the future, we will extend the current study, including the following three aspects. \(1\) The current simulation scenario is an isolated two-lane intersection with separate left-turning and through lanes, which limits the realistic applications. In future work, more 19 

*D. Jing et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104835* 

real-world scenarios can be simulated to test the performance of the proposed model. \(2\) The interaction between CAVs is assumed to be a non-cooperative game. With the development of wireless communication and autonomous driving technologies, inter-vehicle interactions can be modeled as a cooperative game framework. \(3\) This study only provides individual decision-making strategies, and future studies can investigate the decision-making of CAV platoons. 

**CRediT authorship contribution statement**

**Dian Jing: **Writing – review & editing, Writing – original draft, Software, Methodology, Investigation, Formal analysis. **Enjian** **Yao: **Writing – review & editing, Writing – original draft, Supervision, Project administration, Methodology, Funding acquisition. 

**Rongsheng Chen: **Writing – review & editing, Writing – original draft, Methodology, Conceptualization. 

**Declaration of competing interest**

The authors declare that they have no known competing financial interests or personal relationships that could have appeared to influence the work reported in this paper. 

**Acknowledgments**

The authors gratefully acknowledge the support of the Talent Fund of Beijing Jiaotong University \(2022RC020\). 

**Appendix**

**Proposition 1**. Pure-strategy Nash Equilibria \(NE\) for the noncooperative game always exists. 

**Proof**. The payoff function in the game is composed of two terms related to the running speed of vehicles and traffic safety, as shown in equation \(32\). 

\(

\)

\(

\)

\(

\)

U *aki *= *ω*

*ak *\+ \(1 − *ω*

*ak*

\(32\)

*,f*

*i* Uspeed

*i,f*

*i*\)Usafe

*i,f*

\(

\)

In equation \(32\), *f *= \{1 *, *… *, *|**A ** *i*| \} is the action index in strategy space, U *i, * speed *ai,f * is the speed utility of action *ai,f * for vehicle *i*, and \(

\)

\(

\)

U *i, * safe *ai,f * is the safety utility. The design of U *i, * safe *ai,f * consists of two cases: \(1\) the case of potential conflict and \(2\) the case of no potential conflict, corresponding to equation \(20\). 

\(

\)

\(

\)

Define *F* 1 = *ωi* Uspeed *aki *, *F*

*ak *. The derivative of *F*

*,f*

2 = \(1 − *ωi*\)Usafe

*i,f*

1 for *vki * is:

⎛

⎞ *α* 1− 1

*dF*

⎜

⎟

\(\(

\)

\)

1

⎜

*di*

⎟

*ski*

\(

\)− 2

*dv*

1

*vk*

\(33\)

*k *= *ωiλ* 1 *α* 1 *diski/v* cri⎜ \+ \(

\)

⎟

⋅

\+ *k* Δ *t /v* cri

⋅

*i *\+ *ε*

*i*

⎝

*sk*

⎠

*vk*

*i*

*i *\+ *ε*

*vk*

\+ *k* Δ *t /v* cri

*i *\+ *ε*

We can notice that the derivative is always greater than zero, so the speed payoff function is monotonically increasing. The upper bound is *λ* 1\(1 \+ *v* max */v* cri\) *α* 1, and the lower bound is *λ* 1. 

The derivative of *F* 2 for *vki * is:

\(

\)

*sk*

*dF*

TTC

*i*

2

min− *vk*

\(

\)

*i *\+ *ε*

− 2

*dv*

*vk*

\(34\)

*k *= \(1 − *ωi*\) *λ* 2 *ski *⋅ *e*

⋅

*i *\+ *ε*

*i*

Notice that the derivative is always less than zero, so the safety payoff function is monotonically decreasing. The upper bound is \(

\)

\(

\)

*sk*

*sk*

TTC

*j*

*j*

min−

TTC

*ε*

min− *v* max\+ *ε*

*λ* 2 *e*

, and the lower bound is *λ* 2 *e*

. 

\(

\)

\(

\)

Therefore, U *aki * is continuous and there is only one U *ak * corresponding to *ak*

*,f*

*i,f*

*i,f *. 

\(

\)

The utility under the action combination *ai,f, a*− *i,g * from the perspective of vehicle *i * in equation \(35\)

\{

\(

\)

\(

\)

\(

\)

U

*ωi* U *i*

*a*

\(

\) *a*

*, * speed

*i,f *\+ \(1 − *ωi*\)U *i, * safe

*i,f , * if have potential conflicts

*i ai,f , a*− *i,g *=

*ωi* U *i*

*a*

*, * speed

*i,f *\+ M *, * otherwise

\(35\)

The following properties can be inferred:

\(

\) \(

\)

**Case 1**. If vehicle *i * takes action *ai,f*, and the rival − *i * take \( *a*− *i,g *, *a*

, 

*a*

, *a*

, 

1

− *i,g* 2 …\). Under any action combination

*i,f , a*− *i,g* 1

*i,f , a*− *i,g* 2 …, *i*

has potential conflicts with the rival. We have \(36\):

20 





*D. Jing et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104835* 

\(

\)

\(

\)

U *i ai*

*a*

*,f , a*− *i,g*

= U

= *... *

\(36\)

1

*i*

*i,f , a*− *i,g* 2

\(

\)

**Case 2**. If under an action combination *ai,f, a*− *i,g *, vehicle *i * has no potential conflicts with the rival. We have \(37\): \(

\)

\(

\)

U *i*

*a*

*a*

*, * safe

*i,f , a*− *i,g *= U− *i, * safe

*i,f , a*− *i,g *= M

\(37\)

According to Proposition 1 in \(Mallick, 2011\), a pure-strategy Nash Equilibrium \(NE\) in two-person discrete games exists if the minimal acyclicity condition is satisfied. In other words, NE exists if no residual matrix \(a subset of an original Nash game matrix\) contains a cyclic best-response sequence. An example is shown in Figure 19 to illustrate it. 

**Fig. 19. **Illustration of acyclicity for the pure-strategy noncooperative game. 

Note that in the game above, there is no pure-strategy NE since the persistence of incentives deviates unilaterally from any candidate solution, which forms a cycle depicted by four arrows. Therefore, if no such cycle in the game matrix \(satisfies the minimal acyclicity condition\), pure-strategy NE exists. Next, we consider the two abovementioned cases. 

**Case 1**. Assume a cycle exists in the residual matrix, we use a sequence to represent the transition from one action combination to another like this:

\(

\)

\(

\)

\(

\)

\(

\)

\(

\)

*ai*

*a*

*a*

*a*

*a*

\(38\)

*, * 0 *, a*− *i, * 0 →

*i, * 1 *, a*− *i, * 0 →

*i, * 1 *, a*− *i, * 1 →

*i, * 0 *, a*− *i, * 1 →

*i, * 0 *, a*− *i, * 0

According to equation \(32\), the payoff can be written from the perspective of *i*: \(

\)

\(

\)

\(

\)

\(

\)

\(

\)

U *i ai*

*a*

*a*

*a*

*a*

\(39\)

*, * 0 *, a*− *i, * 0

*< * U *i i, * 1 *, a*− *i, * 0 = U *i i, * 1 *, a*− *i, * 1 *< * U *i i, * 0 *, a*− *i, * 1 = U *i i, * 0 *, a*− *i, * 0

There is a contradiction in the above inequality, and the hypothesis of the existence of a cyclic best-response sequence does not hold. Therefore, pure-strategy NE exists. 

**Case 2**. The payoff of at least one action combination is infinite, calculated by equation \(35\). For example, define a game matrix in \(

\)

\(

\)

\(

\)

Figure 20, let the payoff of vehicle *i * under strategy combination *ai, * 1 *, a*− *i, * 1 be U *i ai, * 1 *, a*− *i, * 1 = *ωi* Uspeed *ai,f *\+ M. According to \(

\)

equation \(35\), the payoff U *i, * safe *ai, * 1 *, a*− *i, * 1 = U− *i, * safe\( *ai, a*− *i*\) = M. If there is only one action combination containing M, the payoff \(

\(

\)

\(

\)

\)

*ωi* U *i, * speed *ai,f *\+ M *, ω*− *i* U− *i, * speed *a*− *i,g *\+ M must be a pure-strategy NE since no vehicle can enhance his payoff by changing his action unilaterally. 

**Fig. 20. **An illustration of acyclicity in the case of no potential conflicts. 

\(

\)

\(

\)

The arrow from *ai, * 1 *, a*− *i, * 2 to *ai, * 1 *, a*− *i, * 1 denotes that vehicle − *i * will change the action from *a*− *i, * 2 \(payoff is 1 \+ M\) to *a*− *i, * 1 \(payoff is 1.5 \+ M\). Similarly, other arrows have the same property. 

If several points contain M, these points can be compared separately because the NE must exist in these points. 

Assume a cycle exists in the subset matrix, we have \(40\):

\(

\)

\(

\)

\(

\)

\(

\)

\(

\)

*ai*

*a*

*a*

*a*

*a*

\(40\)

*, * 1 *, a*− *i, * 1 →

*i, * 0 *, a*− *i, * 1 →

*i, * 0 *, a*− *i, * 2 →

*i, * 1 *, a*− *i, * 2 →

*i, * 1 *, a*− *i, * 1

Now consider the subset of points containing M, circled by the dotted line. In this subset, the payoff may have two values \(Uspeed or Uspeed \+ M\). The payoff of *i * for action *ai * is as \(41\):

21 

*D. Jing et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104835* 

\(

\)

U *i ai, a*

= U

− *i*

*i, * speed \+ U *i, * safe or U *i, * speed \+ M ≤ U *i, * speed \+ M

\(41\)

\(

\)

\(

\)

If *ai*

*a*

, we have inequality as \(42\):

*,f , a*

*, a*

1

− *i,g* 1 →

*i,f* 1

− *i,g* 2

\(

\)

\(

\)

U *i ai*

*a*

*,f , a*

≤ U

*, a*

≤ U

1

− *i,g* 1

*i*

*i,f* 1

− *i,g* 2

*i, * speed \+ M

\(42\)

From the perspective of *i*, we have the following inequality \(43\):

\(

\)

\(

\)

\(

\)

\(

\)

\(

\)

U *i ai*

*a*

*a*

*a*

*a*

\(43\)

*, * 1 *, a*− *i, * 1

*< * U *i i, * 0 *, a*− *i, * 1 ≤ U *i i, * 0 *, a*− *i, * 2

*< * U *i i, * 1 *, a*− *i, * 2 ≤ U *i i, * 1 *, a*− *i, * 1

Notice a contradiction in the above inequality, and the hypothesis of a cyclic best-response sequence does not hold. Therefore, pure-strategy NE exists. 

**Proposition 2**. The solutions of a game of incomplete information with discrete strategy always exist if the number of player types is finite. 

**Definitions**. Let *σ*\( *i, θi*\) be the pure strategy of vehicle *i * with driving style *θi*. *σ*\( *i, θi*\) is a possible action of vehicle *i*. A pure strategy vector *σ *= \( *σ*\( *i, θi*\) \)

*σ*\( *i, *

*θ*

*θ*

*i*∈Θ *i*

*i*\) is equal to the set of strategy vectors in mixed strategy vectors. 

**Lemma 1**. All games with incomplete information in which the set of types is finite, and the set of actions of each type is finite has a Bayesian equilibrium. 

\(

\)

**Proof**. Let *σ*\* be a Bayesian equilibrium. Then, we have *ui*\( *σ*\*| *θi *\) ≥ *ui ai, σ*\*

. For each pure strategy *s*

− *i*| *θi*

*i*, we have \(44\):

\(

\)

∑

\(

\)

∑

\(

\)

*ui si, σ*\* =

*p*\( *θ*

*s*

≤

*p*\( *θ*

*σ*\*

= *u*

− *i*

*i*\) *ui i*\( *θi*\) *, σ*\*− *i*| *θi*

*i*\) *ui*

− *i*| *θi*

*i*\( *σ*\*\)

\(44\)

*θi*∈Θ *i*

*θi*∈Θ *i*

The inequality holds for each pure strategy of vehicle *i*, and also holds for his mixed strategy. Here we have *σ*\* *i * is a best response to *σ*\*− *i * and *σ*\* is a NE. 

**Proposition 3**. The solutions of Stackelberg Equilibrium \(SE\) are pure-strategy NE solutions if such condition is satisfied: the leader always takes acceleration actions unless reaching the speed limit, and the follower takes the best actions subject to the leader’s decision. 

**Assumption 1**. If two vehicles have a conflict, at least one vehicle can detect the rival’s position and take action to avoid collisions. 

**Proof**. The best strategy combination can be represented as equations \(6\)-\(8\). From the perspective of *i*, *i * will choose the optimal action in strategy space. According to Assumption 1, the best response set for vehicle − *i * is nonempty, so − *i * has an optimal solution. 

\(

\)

\(

\)

The solution of SE is the best strategy combination *a*\* *i, a*\* . According to the proof in Proposition 1, *a*\*

is a NE since no vehicle

− *i*

*i , a*\*− *i*

can enhance his payoff by changing his strategy unilaterally. 

**References**

Albaba, B.M., Yildiz, Y., 2019. Modeling cyber-physical human systems via an interplay between reinforcement learning and game theory. Annu. Rev. Control. 48, 1–21. https://doi.org/10.1016/J.ARCONTROL.2019.10.002. 

Albaba, B.M., Yildiz, Y., 2022. Driver modeling through deep reinforcement learning and behavioral game theory. IEEE Trans. Control Syst. Technol. 30 \(2\), 885–892. 

https://doi.org/10.1109/TCST.2021.3075557. 

Althoff, M., Dolan, J.M., 2014. Online verification of automated road vehicles using reachability analysis. IEEE Trans. Rob. 30 \(4\) https://doi.org/10.1109/

TRO.2014.2312453. 

Althoff, M., Stursberg, O., Buss, M., 2009. Model-based probabilistic collision detection in autonomous driving. IEEE Trans. Intell. Transp. Syst. 10 \(2\) https://doi.org/

10.1109/TITS.2009.2018966. 

Arbis, D., Dixit, V.V., Rashidi, T.H., 2016. Impact of risk attitudes and perception on game theoretic driving interactions and safety. Accid. Anal. Prev. 94 https://doi. 

org/10.1016/j.aap.2016.05.027. 

Arvin, R., Khattak, A.J., Kamrani, M., Rio-Torres, J., 2020. Safety evaluation of connected and automated vehicles in mixed traffic with conventional vehicles at intersections. J. Intell. Transp. Syst. Technol. Plann. Oper. 25 \(2\), 170–187. https://doi.org/10.1080/15472450.2020.1834392. 

Asadi, B., Vahidi, A., 2011. Predictive cruise control: Utilizing upcoming traffic signal information for improving fuel economy and reducing trip time. IEEE Trans. 

Control Syst. Technol. 19 \(3\) https://doi.org/10.1109/TCST.2010.2047860. 

Bauso, D., 2014. Game theory: Models, numerical methods and applications. Foundations and Trends® in Systems and Control 1 \(4\), 379–522. https://doi.org/

10.1561/2600000003. 

Bautista-Montesano, R., Galluzzi, R., Ruan, K., Fu, Y., Di, X., 2022. Autonomous navigation at unsignalized intersections: A coupled reinforcement learning and model predictive control approach. Transp. Res. Part C: Emerg. Technol. 139, 103662 https://doi.org/10.1016/j.trc.2022.103662. 

Boender, C.G.E., Mockus, J., 1991. Bayesian approach to global optimization-theory and applications. Math. Comput. 56 \(194\) https://doi.org/10.2307/2008419. 

Bokare, P.S., Maurya, A.K., 2017. Acceleration-deceleration behaviour of various vehicle types. Transp. Res. Procedia 25, 4733–4749. https://doi.org/10.1016/J. 

TRPRO.2017.05.486. 

Bonela, S.R., Kadali, B.R., 2022. Review of traffic safety evaluation at T-intersections using surrogate safety measures in developing countries context. IATSS Research 46 \(3\), 307–321. https://doi.org/10.1016/j.iatssr.2022.03.001. 

Chen, R., Hu, J., Levin, M.W., Rey, D., 2020. Stability-based analysis of autonomous intersection management with pedestrians. Transp. Res. C 114 \(February\), 463–483. https://doi.org/10.1016/j.trc.2020.01.016. 

Chen, X., Sun, Y., Ou, Y., Zheng, X., Wang, Z., Li, M., 2020. A conflict decision model based on game theory for intelligent vehicles at urban unsignalized intersections. 

IEEE Access 8, 189546–189555. https://doi.org/10.1109/ACCESS.2020.3031674. 

22 

*D. Jing et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104835* 

De Campos, G.R., Falcone, P., Hult, R., Wymeersch, H., Sjöberg, J., 2017. Traffic coordination at road intersections: autonomous decision-making algorithms using model-based heuristics. IEEE Intell. Transp. Syst. Mag. 9 \(1\) https://doi.org/10.1109/MITS.2016.2630585. 

de Zepeda, M.V.N., Meng, F., Su, J., Zeng, X.J., Wang, Q., 2021. Dynamic clustering analysis for driving styles identification. Eng. Appl. Artif. Intel. 97, 104096

https://doi.org/10.1016/j.engappai.2020.104096. 

Elander, J., West, R., French, D., 1993. Behavioral correlates of individual differences in road-traffic crash risk: An examination of methods and findings. Psychol. Bull. 

113 \(2\) https://doi.org/10.1037/0033-2909.113.2.279. 

Gartner, N. H. \(1983\). OPAC: A demand-responsive strategy for traffic signal control. Transportation Research Record, 1983\(906\). 

Harsanyi, J.C., 1967. Games with incomplete information played by “Bayesian” players, I-III Part I. The basic model. Manag. Sci. 14 \(3\) https://doi.org/10.1287/

mnsc.14.3.159. 

Huang, X., Peng, H., 2017. Speed trajectory planning at signalized intersections using sequential convex optimization. In: 2017 American Control Conference \(ACC\). 

IEEE, pp. 2992–2997. https://doi.org/10.23919/ACC.2017.7963406. 

Hunt, P.B., Robertson, D.I., Bretherton, R.D., 1982. The SCOOT on-line traffic signal optimisation technique \(Glasgow\). Traffic Eng. Control 23 \(4\). 

Ishibashi, M., Okuwa, M., Doi, S.I., Akamatsu, M., 2007. Indices for characterizing driving style and their relevance to car following behavior. In: SICE annual conference 2007. IEEE, pp. 1132–1137. https://doi.org/10.1109/SICE.2007.4421155. 

Jing, D., Yao, E., Chen, R., 2023. Moving characteristics analysis of mixed traffic flow of CAVs and HVs around accident zones. Phys. A: Stat. Mech. Applic. 626, 129085 https://doi.org/10.1016/J.PHYSA.2023.129085. 

Koprulu, C., Yildiz, Y., 2021. Act to reason: A dynamic game theoretical driving model for highway merging applications. In: 2021 IEEE Conference on Control Technology and Applications \(CCTA\). IEEE, pp. 747–752. https://doi.org/10.1109/CCTA48906.2021.9658815. 

Levin, M.W., Rey, D., 2017. Conflict-point formulation of intersection control for autonomous vehicles. Transp. Res. Part C: Emerg. Technol. 85, 528–547. https://doi. 

org/10.1016/j.trc.2017.09.025. 

Li, D., Pan, H., 2022. Two-lane two-way overtaking decision model with driving style awareness based on a game-theoretic framework. Transportmetrica A Transport Science. https://doi.org/10.1080/23249935.2022.2076755. 

Li, N., Yao, Y., Kolmanovsky, I., Atkins, E., Girard, A.R., 2022. Game-theoretic modeling of multi-vehicle interactions at uncontrolled intersections. IEEE Trans. Intell. 

Transp. Syst. 23 \(2\), 1428–1442. https://doi.org/10.1109/TITS.2020.3026160. 

Li, D., Zhu, F., Chen, T., Wong, Y.D., Zhu, C., Wu, J., 2023. COOR-PLT: A hierarchical control model for coordinating adaptive platoons of connected and autonomous vehicles at signal-free intersections based on deep reinforcement learning. Transp. Res. Part C: Emerg. Technol. 146, 103933 https://doi.org/10.1016/j. 

trc.2022.103933. 

Liu, X., Zheng, S., 2010. Study of vehicle-cross action model for unsignalized intersection based on dynamic game. In: 2010 International Conference on Mechanic Automation and Control Engineering. IEEE, pp. 1297–1302. https://doi.org/10.1109/MACE.2010.5536337. 

Liu, B., Shi, Q., Song, Z., El Kamel, A., 2019. Trajectory planning for autonomous intersection management of connected vehicles. Simul. Model. Pract. Theory 90, 16–30. https://doi.org/10.1016/j.simpat.2018.10.002. 

Lopez, P.A., Behrisch, M., Bieker-Walz, L., Erdmann, J., Flotterod, Y.P., Hilbrich, R., Lucken, L., Rummel, J., Wagner, P., Wiebner, E., 2018. Microscopic traffic simulation using SUMO. In: 2019 IEEE intelligent transportation systems conference \(ITSC\). IEEE, pp. 2575–2582. https://doi.org/10.1109/ITSC.2018.8569938. 

Ma, Y., Li, W., Tang, K., Zhang, Z., Chen, S., 2021. Driving style recognition and comparisons among driving tasks based on driver behavior in the online car-hailing industry. Accid. Anal. Prev. 154, 106096 https://doi.org/10.1016/j.aap.2021.106096. 

Makarem, L., Gillet, D., 2013. Model predictive coordination of autonomous vehicles crossing intersections. In: 16th International IEEE Conference on Intelligent Transportation Systems \(ITSC 2013\). IEEE, pp. 1799–1804. https://doi.org/10.1109/ITSC.2013.6728489. 

Malikopoulos, A.A., Cassandras, C.G., Zhang, Y.J., 2018. A decentralized energy-optimal control framework for connected automated vehicles at signal-free intersections. Automatica 93. https://doi.org/10.1016/j.automatica.2018.03.056. 

Mallick, I., 2011. On the existence of pure strategy Nash equilibria in two person discrete games. Econ. Lett. 111 \(2\), 144–146. https://doi.org/10.1016/j. 

econlet.2011.02.017. 

Maschler, M., Solan, E., Zamir, S., 2021. Utility theory. In: Game Theory. https://doi.org/10.1017/9781108636049.004. 

Mirchandani, P., Head, L., 2001. A real-time traffic signal control system: Architecture, algorithms, and analysis. Transp. Res. Part C: Emerg. Technol. 9 \(6\) https://

doi.org/10.1016/S0968-090X\(00\)00047-4. 

Mirheli, A., Tajalli, M., Hajibabai, L., Hajbabaie, A., 2019. A consensus-based distributed trajectory control in a signal-free intersection. Transp. Res. Part C: Emerg. 

Technol. 100, 161–176. https://doi.org/10.1016/j.trc.2019.01.004. 

Mohammadnazar, A., Arvin, R., Khattak, A.J., 2021. Classifying travelers’ driving style using basic safety messages generated by connected vehicles: Application of unsupervised machine learning. Transp. Res. Part C: Emerg. Technol. 122, 102917 https://doi.org/10.1016/j.trc.2020.102917. 

Mu, C., Du, L., Zhao, X., 2021. Event triggered rolling horizon based systematical trajectory planning for merging platoons at mainline-ramp intersection. Transp. Res. 

Part C: Emerg. Technol. 125 https://doi.org/10.1016/J.TRC.2021.103006. 

Nemchinov, D., Martiyahin, D., Mikhailov, A., Kostsov, A., Nemchinov, M., 2020. Research of accepted headways and visibility conditions on intersections. Transp. 

Res. Procedia 45 \(2019\), 13–20. https://doi.org/10.1016/j.trpro.2020.02.057. 

NHTSA. \(2020\). Query of fatality analysis reporting system \(FARS\). 

Papadimitriou, C.H., Tsitsiklis, J.N., 1987. The complexity of markov decision processes. Math. Oper. Res. 12 \(3\), 441–450. https://doi.org/10.1287/MOOR.12.3.441. 

Rahmati, Y., Hosseini, M.K., Talebpour, A., 2022. Helping automated vehicles with left-turn maneuvers: A game theory-based decision framework for conflicting Maneuvers at intersections. IEEE Trans. Intell. Transp. Syst. 23 \(8\), 11877–11890. https://doi.org/10.1109/TITS.2021.3108409. 

Rios-Torres, J., Malikopoulos, A.A., 2017. A survey on the coordination of connected and automated vehicles at intersections and merging at highway on-ramps. IEEE

Trans. Intell. Transp. Syst. 18 \(5\) https://doi.org/10.1109/TITS.2016.2600504. 

Saha, N., Motuba, D., 2023. Estimating the impacts of AV and CAV and technologies transportation systems for medium, long, and buildout transportation planning horizons. Future Transp. 3 \(2\), 457–478. https://doi.org/10.3390/FUTURETRANSP3020027. 

Sims, A.G., Dobinson, K.W., 1980. The Sydney Coordinated Adaptive Traffic \(SCAT\) system philosophy and benefits. IEEE Trans. Veh. Technol. 29 \(2\) https://doi.org/

10.1109/T-VT.1980.23833. 

Smirnov, N., Liu, Y., Validi, A., Morales-Alvarez, W., Olaverri-Monreal, C., 2021. A game theory-based approach for modeling autonomous vehicle behavior in congested, urban lane-changing scenarios. Sensors 21 \(4\). https://doi.org/10.3390/s21041523. 

Sun, C., Leng, J., Lu, B., 2024. Interactive left-turning of autonomous vehicles at uncontrolled intersections. IEEE Trans. Autom. Sci. Eng. 21 \(1\), 204–214. https://doi. 

org/10.1109/TASE.2022.3227964. 

Tian, R., Li, N., Kolmanovsky, I., Yildiz, Y., Girard, A.R., 2022. Game-theoretic modeling of traffic in unsignalized intersection network for autonomous vehicle control verification and validation. IEEE Trans. Intell. Transp. Syst. 23 \(3\) https://doi.org/10.1109/TITS.2020.3035363. 

Wang, Q., Gong, Y., Yang, X., 2022. Connected automated vehicle trajectory optimization along signalized arterial: A decentralized approach under mixed traffic environment. Transp. Res. Part C: Emerg. Technol. 145, 103918 https://doi.org/10.1016/j.trc.2022.103918. 

Wang, W., Wang, L., Zhang, C., Liu, C., Sun, L., 2022. Social interactions for autonomous driving: A review and perspectives. Foundations and Trends® in Robotics 10

\(3–4\), 198–376. http://arxiv.org/abs/2208.07541. 

Wang, H., Meng, Q., Chen, S., Zhang, X., 2021. Competitive and cooperative behaviour analysis of connected and autonomous vehicles across unsignalised intersections: A game-theoretic approach. Transp. Res. B Methodol. 149, 322–346. https://doi.org/10.1016/j.trb.2021.05.007. 

Webster, F. V. \(1958\). Traffic signal settings. undefined-undefined. https://www.mendeley.com/catalogue/49587d06-1c66-3cd0-8e7c-b62680367d72/. 

Wei, L., Li, Z., Gong, J., Gong, C., Li, J., 2021. Autonomous driving strategies at intersections: Scenarios, state-of-the-art, and future outlooks. In: 2021 IEEE

International Intelligent Transportation Systems Conference \(ITSC\). IEEE, pp. 44–51. https://doi.org/10.1109/ITSC48978.2021.9564518. 

Wu, Y., Chen, H., Zhu, F., 2019. DCL-AIM: Decentralized coordination learning of autonomous intersection management for connected and automated vehicles. 

Transp. Res. Part C: Emerg. Technol. 103, 246–260. https://doi.org/10.1016/j.trc.2019.04.012. 

23 

*D. Jing et al. *

*Transportation* *Research* *Part* *C* *167* *\(2024\)* *104835* 

Wu, X., He, X., Yu, G., Harmandayan, A., Wang, Y., 2015. Energy-optimal speed control for electric vehicles on signalized arterials. IEEE Trans. Intell. Transp. Syst. 16

\(5\) https://doi.org/10.1109/TITS.2015.2422778. 

Wu, W., Liu, Y., Hao, W., Giannopoulos, G.A., Byon, Y.J., 2022. Autonomous intersection management with pedestrians crossing. Transp. Res. Part C: Emerg. Technol. 

135 https://doi.org/10.1016/j.trc.2021.103521. 

Wuthishuwong, C., Traechtler, A., Bruns, T., 2015. Safe trajectory planning for autonomous intersection management by using vehicle to infrastructure communication. EURASIP J. Wirel. Commun. Netw. 2015 \(1\), 1–12. https://doi.org/10.1186/s13638-015-0243-3. 

Xie, D.F., Fang, Z.Z., Jia, B., He, Z., 2019. A data-driven lane-changing model based on deep learning. Transp. Res. Part C: Emerg. Technol. 106, 41–60. https://doi. 

org/10.1016/j.trc.2019.07.002. 

Xu, H., Xiao, W., Cassandras, C.G., Zhang, Y., Li, L., 2022. A general framework for decentralized safe optimal control of connected and automated vehicles in multi-lane signal-free intersections. IEEE Trans. Intell. Transp. Syst. 23 \(10\) https://doi.org/10.1109/TITS.2022.3151080. 

Yang, Z., Huang, H., Yao, D., Zhang, Y., 2016. Cooperative driving model for non-signalized intersections based on reduplicate dynamic game. In: 2016 IEEE 19th International Conference on Intelligent Transportation Systems \(ITSC\). IEEE, pp. 1366–1371. https://doi.org/10.1109/ITSC.2016.7795735. 

Yao, H., Li, X., 2020. Decentralized control of connected automated vehicle trajectories in mixed traffic at an isolated signalized intersection. Transp. Res. Part C: Emerg. Technol. 121, 102846 https://doi.org/10.1016/j.trc.2020.102846. 

Zhan, W., Sun, L., Wang, D., Shi, H., Clausse, A., Naumann, M., Kummerle, J., Konigshof, H., Stiller, C., de La Fortelle, A., & Tomizuka, M. \(2019\). INTERACTION

Dataset: An INTERnational, Adversarial and Cooperative moTION Dataset in Interactive Driving Scenarios with Semantic Maps. http://arxiv.org/abs/1910. 

03088. 

Zhang, Y., Cassandras, C.G., 2018. A decentralized optimal control framework for connected automated vehicles at urban intersections with dynamic resequencing. In: 2018 IEEE Conference on Decision and Control \(CDC\). IEEE, pp. 217–222. https://doi.org/10.1109/CDC.2018.8618871. 

Zhang, Y., Cassandras, C.G., 2019. Decentralized optimal control of Connected Automated Vehicles at signal-free intersections including comfort-constrained turns and safety guarantees. Automatica 109, 108563. https://doi.org/10.1016/j.automatica.2019.108563. 

Zhou, A., Peeta, S., Yang, M., Wang, J., 2022. Cooperative signal-free intersection control using virtual platooning and traffic flow regulation. Transp. Res. Part C: Emerg. Technol. 138 https://doi.org/10.1016/j.trc.2022.103610. 

24 


# Document Outline

+ Decentralized human-like control strategy of mixed-flow multi-vehicle interactions at uncontrolled intersections: A game-th ...   
	+ 1 Introduction 
	+ 2 Literature review  
		+ 2.1 Uncontrolled intersection control strategy with AVs 
		+ 2.2 Interaction modeling approaches 

	+ 3 Mathematical models  
		+ 3.1 Leader-follower identification 
		+ 3.2 Interaction mechanisms  
			+ 3.2.1 HDV-CAV interactions 
			+ 3.2.2 CAV-CAV interactions 

		+ 3.3 Kinematic models 
		+ 3.4 Payoff functions 
		+ 3.5 Driving style recognition 

	+ 4 Experiments and results  
		+ 4.1 Parameter calibration 
		+ 4.2 Simulation and analysis  
			+ 4.2.1 Reproducing real-world scenarios 
			+ 4.2.2 Multi-vehicle interactions 
			+ 4.2.3 Space-time diagrams 
			+ 4.2.4 Algorithm performances 
			+ 4.2.5 Sensitivity analysis 
			+ 4.2.6 Safety evaluation 


	+ 5 Conclusions 
	+ CRediT authorship contribution statement 
	+ Declaration of competing interest 
	+ Acknowledgments 
	+ Appendix Acknowledgments 
	+ References



