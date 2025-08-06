Dinneweth et al. *Autonomous Intelligent Systems * \(2022\) 2:27 

Autonomous Intelligent

https://doi.org/10.1007/s43684-022-00045-z

Systems

**R E V I E W**

**Open Access**

Multi-agent reinforcement learning for

autonomous vehicles: a survey

Joris Dinneweth1,2\* , Abderrahmane Boubezoul1 , René Mandiau3

and Stéphane Espié1

**Abstract**

In the near future, autonomous vehicles \(AVs\) may cohabit with human drivers in mixed traffic. This cohabitation raises serious challenges, both in terms of traffic flow and individual mobility, as well as from the road safety point of view. Mixed traffic may fail to fulfill expected security requirements due to the heterogeneity and unpredictability of human drivers, and autonomous cars could then monopolize the traffic. Using multi-agent reinforcement learning \(MARL\) algorithms, researchers have attempted to design autonomous vehicles for both scenarios, and this paper investigates their recent advances. We focus on articles tackling decision-making problems and identify four paradigms. While some authors address mixed traffic problems with or without social-desirable AVs, others tackle the case of fully-autonomous traffic. While the latter case is essentially a communication problem, most authors addressing the mixed traffic admit some limitations. The current human driver models found in the literature are too simplistic since they do not cover the heterogeneity of the drivers’ behaviors. As a result, they fail to generalize over the wide range of possible behaviors. For each paper investigated, we analyze how the authors formulated the MARL

problem in terms of observation, action, and rewards to match the paradigm they apply. 

**Keywords: **Multi-agent reinforcement learning, Simulation, Autonomous Vehicles **1 Introduction**

level could make traffic safer. AVs and humans may cohabit According to the world health organization \(WHO1\), road in mixed traffic before reaching full automation. However, accidents kill 1.3 million people and injure 50 million peo-the evidence suggests that accident-free mixed traffic may ple each year. Several technologies have been proposed be impossible \[2\]. Human drivers follow informal and sub-to make driving safer, such as advanced driver assistance jective norms, but autonomous vehicles comply with traf-systems \(ADAS\), adaptative cruise control \(ACC\), and in-fic rules \[3, 4\]. Because of their divergent concerns, AVs are telligent transportation systems \(ITS\). The latter, with the unlikely to be effective in mixed traffic. By contrast, coordi-recent technological advances in communication systems, nating a fully-autonomous fleet is straightforward because paved the way for the deployment of autonomous vehicles. 

AVs act homogeneously and are therefore predictable. AVs Trommer et al. \[1\] described five levels of vehicle au-should be capable of handling all traffic scenarios, whether tomation in their technical report, ranging from superfi-they are driving in mixed traffic or fully autonomous fleets. 

cial assistance \(level 1\) to full automation \(level 5\). With However, because these scenarios are nearly endless, de-effective algorithms that prevent fatal accidents, the latter signing ruled-based models is practically certain to fail. 

With

advances

in

hardware, 

machine

learning

approaches provide new opportunities to generalize driv-

\* Correspondence: joris.dinneweth@univ-eiffel.fr

ing scenarios. Reinforcement learning \(RL\) approaches, in

1 TS2-MOSS, Univ. Gustave Eiffel, 77454, Champs-sur-Marne, France particular, are successful at solving sequential decision-

2 ENS Paris-Saclay, CNRS, SATIE, Université Paris-Saclay, 91190, Gif-sur-Yvette, making problems, such as Go, Chess, arcade games, and France

Full list of author information is available at the end of the article real-time video games \[5–9\]. In RL, an agent learns and 1 https://www.who.int/news-room/fact-sheets/detail/road-traffic-injuries

self-corrects by receiving feedback on the quality of its in-

© The Author\(s\) 2022. **Open Access **This article is licensed under a Creative Commons Attribution 4.0 International License, which permits use, sharing, adaptation, distribution and reproduction in any medium or format, as long as you give appropriate credit to the original author\(s\) and the source, provide a link to the Creative Commons licence, and indicate if changes were made. The images or other third party material in this article are included in the article’s Creative Commons licence, unless indicated otherwise in a credit line to the material. If material is not included in the article’s Creative Commons licence and your intended use is not permitted by statutory regulation or exceeds the permitted use, you will need to obtain permission directly from the copyright holder. To view a copy of this licence, visit http://creativecommons.org/licenses/by/4.0/. 



Dinneweth et al. *Autonomous Intelligent Systems * \(2022\) 2:27 

Page 2 of 12

**Figure 2 **Single-agent reinforcement learning **2 Reinforcement learning**

This section provides a state-of-art of single \(2.1\) and **Figure 1 **Distribution of the reviewed papers multi-agent \(2.2\) reinforcement learning algorithms. 

**2.1 Single-agent reinforcement learning**

teractions within an environment. Multi-agent RL \(MARL\) Reinforcement learning \(RL\) is a trial-and-error learnis a more distributed framework in which several agents ing method where an agent interacts within an environ-simultaneously learn cooperative or competitive behavior. 

ment \[5\] \(Fig. 2\). The agent’s goal is to reach the most Since several decision-makers learn simultaneously and rewarding states of the environment. The agent explores possibly coordinate, more robust and convincing policies the environment, grasping its dynamics and devising an can emerge than with single-agent RL approaches. 

appropriate policy \(behavior\) to discover these states. As Several surveys have investigated relative aspects of RL

a result, the agent gains knowledge from its actions and for AVs more global way. Schmidt et al. \[10\] tackled au-maximizes long-term accumulated rewards. Non-learning tonomous mobility, including traffic management, un-agents who obey stationary policies may be present in the manned aerial vehicles \(UAVs\), AVs, and resource opti-environment. The environment, the state, the actions, and mization using MARL algorithms. Elallid et al. \[11\] sur-the rewards for an autonomous car may correspond to the veyed AVs’ scene understanding, decision-making, plan-roadway, the positions of other vehicles, accelerating or ning, and social behavior using RL approaches. Kiran et al. 

braking, and collision avoidance, respectively. 

\[12\] tackled scene understanding, decision-making, and There are three types of RL learning algorithms: value-planning using RL algorithms. Ye et al. \[13\] tackled mo-based, policy-based, and actor-critic. In value-based meth-tion planning and control using RL approaches. Notwith-ods, the agent implicitly learns a deterministic policy by standing, no reviews investigated the decision-making of picking higher-valued actions via a value function that autonomous vehicles using MARL algorithms. 

maps state-action pairs. Nevertheless, the value function Our survey seeks to fulfill this gap by answering two re-becomes inefficient as the state-action space grows, such search questions: \( *RQ1*\) what is the recent state-of-art of as discrete spaces \[15\]. In policy-based methods, the agent AVs’ decision-making using MARL algorithms; and \( *RQ2*\) explicitly learns a stochastic policy function. However, what are the topic’s primary current limitations. To answer policy-based approaches suffer from high variance, which these questions as concisely as possible while considering slows down the learning process. Actor-critic approaches recent breakthroughs in MARL algorithms, we have re-appear to be a reasonable compromise that combines the stricted this review to sixteen papers published since 2019

benefits of the preceding methods. The latter is divided \(distribution in Fig. 1\). We focus our survey on decision-into a critic part which approximates the value function, making problems; nonetheless, interested readers can find while an actor part learns a policy based on critic estima-in \[14\], a recent survey that focuses on autonomous driving tions to alleviate the variance. Because they work effec-policy learning using deep reinforcement learning \(DRL\) tively in real-world contexts with continuous space, actor-and deep imitation learning \(DIL\) techniques. 

critic approaches are widespread within the RL commu-We have organized the remainder of this review as

nity. 

follows. Firstly, we introduce the state-of-art of RL and We briefly describe the single-agent RL algorithms

MARL algorithms \(Sect. 2\). Secondly, we highlight the \(Fig. 3\) addressed in Sect. 5. Deep Q-network \(DQN\) \[16\]

learning schemes and strategies of MARL algorithms

is a value-based agent that builds a deep learning model to \(Sect. 3\). Thirdly, we review the driving simulation envi-estimate future rewards and execute behaviors that lead to ronments \(Sect. 4\). Fourthly, we investigate articles tack-the best outcome. Advantage actor-critic \(A2C\) \[17\] is an ling AVs’ decision-making using MARL algorithms \(Sect. 5\). actor-critic agent that builds a stochastic policy to estimate Lastly, we discuss open challenges and conclude this study the advantage of taking action over others. Deep determin-

\(Sect. 6\). 

istic policy gradient \(DDPG\) \[18\] is an A2C agent with de-

Dinneweth et al. *Autonomous Intelligent Systems * \(2022\) 2:27 

Page 3 of 12

stationarity and partial observability are mitigated by communication. 

Many learning schemes and strategies have been pro-

posed in response to the additional challenges of MARL algorithms, which are exacerbated by the number of agents. 

**3 Learning schemes**

The curse of dimensionality, partial observability, and non-stationarity represent three critical challenges for MARL

development. This section introduces how MARL central-Figure 3 Taxonomy of RL methods

ized or decentralized the learning and its execution \(3.1\)

and what are learning schemes \(3.2\) implemented in the reviewed papers that tackle these challenges. 

terministic off-policy, which means that the present policy **3.1 Centralization and decentralization**

does not guide the learning process. Instead of employing In learning algorithms, an agent learns a policy during a a logarithmic update, proximal policy optimization \(PPO\) training phase and follows it during the execution phase. 

\[19\] is an expansion of the A2C agent that updates the pol-These phases, in MARL algorithms, can be either central-icy based on the ratio between the old and new policies ized or decentralized. In the centralized one, agents share weighted by the advantage. None of them deal with policy-information to improve their policies, whereas, in the de-based methods. 

centralized one, they learn independently with no additional information. Three major learning schemes have **2.2 Multi-agent reinforcement learning**

been proposed depending on whether the training and ex-Multi-agent reinforcement learning \(MARL\) algorithms ecution phases are centralized or decentralized. 

involve several agents learning simultaneously in a shared environment. Agents are either cooperative, competitive, *3.1.1 Centralized training centralized execution *\( *CTCE*\) or have a mixed approach. Cooperative agents possibly In centralized training centralized execution \(CTCE\) communicate to coordinate their actions \(Fig. 4\) and often scheme, a central learner gathers information from agents share a common reward function. Conversely, competitive to learn a joint policy, which mitigates the partial observ-agents play a zero-sum game attempting to outperform ability and non-stationarity issues. However, CTCE suf-their opponents. When agents do not behave fully cooper-fers from centralization, which exacerbates the curse of atively or fully competitively, they follow the mix setting, a dimensionality. Furthermore, agents with competing goals general-sum game without any restrictions on agents’ re-may disrupt each other’s policies, making learning harder. 

lations \[20\]. 

Single-agent RL algorithms may suffice because CTCE

MARL algorithms follow the same taxonomy of single-

does not expressly assume decentralization. In contrast to RL methods introduced in Fig. 3. Multi-agent extensions of CTCE, a fully-decentralized scheme has been proposed. 

single-agent algorithms are often prefixed with *MA*, e.g., MAA2C and MADDPG \[21, 22\]. MARL algorithms are *3.1.2 Decentralized training decentralized execution* more complicated than single-agent RL approaches be-

\( *DTDE*\)

cause several agents learn simultaneously and constantly Decentralized training decentralized execution \(DTDE\) co-adapt their policies. This non-stationarity disrupts the scheme allows each agent to learn independently with-dynamics of the environment and impedes the learn-

out exchanging additional information. As a result, agents ing process \[23\]. Furthermore, as the number of agents are unaware of one another’s existence, and the environ-increases, the space expands exponentially, slowing the ment appears non-stationary from their viewpoints. Fur-learning process. The latter phenomenon is called the thermore, Gupta et al. \[25\] demonstrated that DTDE scales curse of dimensionality. 

poorly with agent number. 

In other environments, agents operate with just partial One last scheme has been proposed as an intermedi-observations of the present state, making learning more ary solution, given the previous limitations of the fully-challenging; for example, it is hard to observe the whole centralized and fully-decentralized approaches. 

traffic flow in road driving. To dispel these obstruction zones, agents can communicate in cooperative tasks \[24\]. 

*3.1.3 Centralized training decentralized execution* Connected autonomous vehicles, for example, could share \( *CTDE*\)

and merge their local observations to better represent traf-Lowe et al. \[22\] introduced the centralized training decen-fic, potentially revealing a vehicle in a blind spot. Non-tralized execution \(CTDE\) method, which overcomes the

Dinneweth et al. *Autonomous Intelligent Systems * \(2022\) 2:27 

Page 4 of 12

**Figure 4 **MARL with two communicative agents

**Figure 5 **CTDE learning schemes

shortcomings

of

the

fully-centralized

and

fully-

schemes, various RL strategies may overcome multi-agent decentralized approaches. During the training phase, challenges. 

agents share additional information to reduce non-

stationarity and partial observability, then discard it during **3.2 Learning strategies**

the execution phase. CTDE scheme includes two popular This subsection presents some RL strategies inspired by strategies that can be used depending on the agents’ nature human cognitive mechanisms that were used in the papers

\[25\]. 

discussed in Sect. 5. 

*Parameter sharing*

Parameter sharing \(PS\) is a well-

*3.2.1 Memory*

known approach for dealing with large-scale environ-Memory is a mechanism allowing humans to analyze dy-ments where several homogeneous agents cooperate \[25\]. 

namics. Because RL approaches deal with sequential prob-PS mitigates the curse of dimensionality by allowing all lems, giving agents memory strengthens their ability to agents to learn simultaneously using a single neural net-figure out the environment’s dynamics \[31\]. Researchers work during the training phase \(Fig. 5\(a\)\). 

designed a Recurrent Neural Network \(RNN\), a memory-Centralized critic decentralized actor

However, when

based neural network with information cycles that remem-agents are heterogeneous, the centralized critic decentral-ber the past inputs and reuse them in subsequent deci-ized actor is more convenient \[22\]. It follows the actor-sions. As a result, RNN reduces non-stationarity by im-critic architecture. Since the critic focuses on assessing the proving the analysis of current dynamics based on these actor, it is no longer helpful for the execution phase. There-experiences. In the case of driving, the memory enables fore, each agent receives a duplicate of the actor after the determining the heading of a vehicle between two lanes training phase \(Fig. 5\(b\)\). 

\(Fig. 6\). 

MARL research is still in its infancy, and we have barely skimmed its surface. Interested readers may find compre-3.2.2 Masking

hensive reviews dedicated to MARL algorithms and chal-Masking prevents humans from performing undesirable lenges \[20, 26–30\]. In addition to these MARL learning actions, making the environment safer and decision-





Dinneweth et al. *Autonomous Intelligent Systems * \(2022\) 2:27 

Page 5 of 12

**Figure 6 **The benefit of memory. It is impossible to figure out the car’s heading without memory \(6\(a\)\), while it becomes straightforward with memory \(6\(b\)\)

**Figure 7 **Masking prevents from undertaking undesirable actions \(red\) **Figure 8 **Curriculum Learning for driving. From left to right, agents start in light traffic, increase the complexity, and become more robust in dense traffic

making straightforward \[31\]. When a designer knows *a* lenging. Another way to ease learning is to consider it hi-priori that an action is counterproductive, he or she can erarchically. 

prevent the agents from undertaking it. For example, when a road is under construction, barriers prevent us from tak-3.2.4 Hierarchical reinforcement learning \( *HRL*\) ing it \(Fig. 7\). Masking speeds up the training and alleviates Hierarchical reinforcement learning are “divide and con-the curse of dimensionality by narrowing the action space. 

quer” algorithms \[33\]. Dividing the main policy into lower-Another way to ease learning is to reduce exploration. 

level sub-policies make problems more manageable since these sub-policies can be reused in related tasks \(Fig. 9\). 

*3.2.3 Curriculum learning*

For example, a left lane change on a highway can reuse Curriculum learning \[32\] refers to a learning method that the knowledge acquired from a similar task on a country gradually increases the difficulty. For example, when peo-road. Sub-tasks are sometimes less resource-intensive than ple learn to drive, they usually start in low-traffic areas, and global tasks; because they can operate in a narrowed state-when they master it, they move on to denser areas \(Fig. 8\). 

action space, thus alleviating the curse of dimensionality. 

In MARL, agents often fail to learn practical policies be-We showed in this section that centralized and decen-cause of the non-stationarity. With curriculum learning, tralized schemes suffer from many problems that learning agents start learning in stationary environments and grad-strategies can alleviate. The following section will describe ually remove this stationarity, making the task more chal-the MARL-based driving simulation environments. 

Dinneweth et al. *Autonomous Intelligent Systems * \(2022\) 2:27 

Page 6 of 12

**Figure 9 **Hierarchical reinforcement learning \(inspired from Chen et al. \[34\]\). A higher-level policy \(orange\) selects a subtask \(blue\) to perform a sub-policy on a narrow action space \(green\)

**4 MARL-based driving simulation environments**

\(MACAD\) allows the implementation of

Coordinating a fully-autonomous fleet, i.e., without hu-communicative agents. 

man drivers, is more tractable than driving in mixed traffic All these simulation environments support the design of because of the predictable nature of homogeneous agents. 

different scenario types. 

Furthermore, to keep traffic flowing, AVs share information and coordinate within short reaction times. Most **4.2 Driving scenarios**

MARL training use simulation environments \(4.1\) to learn Most papers focus on narrow scenarios instead of consid-these features on various scenarios \(4.2\) and with human ering overall traffic. We present the traffic scenarios ac-driver models \(4.3\). 

cording to their complexity. 

1. *Highway driving*. This scenario is commonly **4.1 Simulation environments**

accepted as the most straightforward scenario and

Simulation environments provide tools to simulate traf-considers two maneuvers: car-following and lane

fic and develop learning algorithms for AVs. They allow changing. Mastering these maneuvers, which

benchmarking of the effectiveness of the suggested algo-account for 98% of driver actions, is crucial for safe rithms before shifting to a real-world implementation. We driving. Robust AVs mastering highway driving

briefly introduce, in alphabetic order, four simulation en-should avoid collisions and frequent lane changes, 

vironments used in the papers introduced in Sect. 5. 

which will affect traffic flow. 

• CARLA \[35\] is an open-source road environment 2. *Merging and exiting*. These maneuvers are similar to based on Unreal Engine.2 It provides assets to model lane change but are constrained in space and time. 

the road environment and implement perception, 

Robust AVs must anticipate gaps in traffic to merge planning, and control modules. 

smoothly within the traffic flow and space-time

• Flow3 \[36\] is a framework combining the SUMO

constraints. Inference capabilities should also

traffic simulator \[37\] and a deep RL library Rllab \[38\]. 

determine whether a driver is inclined to engage in It provides many traffic scenarios and supports

an altruistic behavior by leaving a gap, which is not training involving a fixed number of vehicles. 

straightforward since AVs are agnostic about

• Highway-env4 is an open-source Gym-based platform. 

informal rules. 

It provides road scenarios designed to train AVs’

3. *Intersections and roundabouts*. There are decision-making in mixed traffic. According to

heterogeneous configurations of intersection, and

Schmidt et al. \[10\], its performance decreases with the apprehending them can be challenging. For

number of vehicles. 

instance, designers failed to generalize them via

• MACAD-Gym5 \[39\] is a Gym-based training rules-based models and designed a decision graph

environment based on CARLA. As its name implies, 

for each one, which is tedious. Robust AVs should

multi-agent connected autonomous driving

generalize them and figure out the singularities of each. 

Because designing a generic model of intersections is dif-2 www.unrealengine.com

ficult, most research concentrate on the first two levels. Re-3 https://github.com/flow-project

gardless of the scenario, robust AVs should have an advan-4 https://github.com/eleurent/highway-env

tage by avoiding more collisions if they can predict human 5 https://github.com/praveen-palanisamy/macad-gym

driver behavior. 

Dinneweth et al. *Autonomous Intelligent Systems * \(2022\) 2:27 

Page 7 of 12

**4.3 Human driver models**

way of the leading and following vehicles. AVs communi-AVs have difficulty adapting to the heterogeneity of human cate local observations with other AVs within range. The behavior because it produces additional uncertainty and ego-agent’s actions are constrained within predefined dis-forces caution. To overcome uncertainty, humans make as-crete acceleration values, and its reward function pro-sumptions based on experience, informal rules, and be-motes safety and efficiency. 

havioral cues, which are sometimes biased or stereotyped Dong et al. \[31\] tackled a challenging environment where

\[40, 41\]. It is impossible to replicate the entire human cog-AVs have to exit by one of the two off-ramps on a three-nitive process, and therefore, AVs often learn with over-lane highway. The agent’s observations contain the relative simplified human models. 

speeds, longitudinal locations, lane positions, and inten-Human-driven vehicle \(HDV\) models simulate car-

tions of surrounding AVs, as well as an adjacency matrix following and lane-changing maneuvers \[42–44\]. The and a mask. AVs pick up high-level actions: lane change or well-known intelligent driver model \(IDM\) describes lane keeping. Functions reward when each AV reaches the speed and acceleration based on the driver’s preferences desired off-ramp indicated by the intention and penalizes for speed and headway \[45\]. The IDM is often combined collision and lane changes to prevent versatility. 

with the MOBIL or LC2013 lane-changing model, which Han and Wang \[49\] trained AVs to drive on a three-lane considers the utility and risk associated with this maneuver freeway. Each AV observes its position, velocity, accelera-

\[46, 47\]. Although the literature refers to them as human-tion, and data captured from an onboard camera and LI-driven models, they lack human traits such as psychology DAR sensors. Additionally, AVs share their states, actions, or intrinsic motivation. 

and observations with each other. AVs select high-level ac-Designing AVs for mixed traffic is challenging because tions such as lane keeping, lane change, or emergency stop of the fundamental differences between humans and ma-and are rewarded according to their velocities and passen-chines. Although inferring human social behavior helps gers’ comfort. The reward system deals with the credit as-AVs’ decision-making, the following section shows that signment problem, i.e., how to fairly reallocate a shared this approach is not widespread in the literature. 

global reward by marginalizing rewards using the Shapley value. In the cooperative game theory, the Shapley value is **5 MARL algorithms for AVs**

a solution concept that distributes fair payoffs to players proportionally to their contribution. Since the complex-We have identified four research paradigms throughout ity of the Shapley value is polynomial with the number of the MARL decision-making for AVs literature. Some au-agents, the authors estimated via a neural network and ex-thors focused on mixed traffic where AVs drive in a self-tended it to sequential problems. 

concern way \(5.1\), while others attempted to incorporate AVs decision-making in mixed traffic is significantly im-social abilities into their decision-making \(5.2\). In both pacted by the absence of other AVs in their vicinities. As cases, the authors realized that the current HDV mod-AVs communicate local observations within range, mean-els do not fulfill their objectives since they are oversim-ing the uncertainty about the environment grows as the plified and fail at providing a heterogeneity of behaviors. 

number of surrounding AVs decreases. To overcome this As a result, researchers designed a more sophisticated challenge, some researchers envision AVs that are more HDV model endowed with social capabilities \(5.3\). The aware of their surroundings and propose algorithms with last paradigm tackles the fully autonomous traffic case social capabilities. 

where no human driver can disturb AVs’ coordination \(5.4\). Finally, we present the formulation of the authors **5.2 Socially desirable AVs**

\(5.5\). For each paradigm introduced, we present the au-Socially desirable AVs will likely include the concept of thors’ formulation of the MARL problem in terms of ob-altruism. In psychology, social value orientation \(SVO\) servation, action, and reward function. 

quantifies an individual’s level of altruism, i.e., how much importance to place on others. Lower SVO levels denote **5.1 Mixed traffic**

selfish behavior, while higher levels denote true altruism. 

Before reaching the full automation level, AVs will poten-In their first paper, Toghi et al. \[50\] tackled the merg-tially cohabit with human drivers in mixed traffic, which is ing and exiting scenarios with socially desirable AVs. AVs no easy feat. AVs follow homogeneous policies, while hu-observe the kinematics of their neighboring vehicles as mans are sometimes erratic and irrational. Here, we focus well as their last high-level actions to extract the tempo-on papers suggesting self-concern AVs driving in mixed ral information giving their current trajectories. They per-traffic. 

form meta-actions, including lane change, acceleration, Wang et al. \[48\] trained AVs on three scenarios: a ring and deceleration. The socially desirable behavior is in-network, a figure-of-eight network, and a mini-city with duced through a reward function acting as a trade-off be-intersections and roundabouts. The ego-agent state com-tween egoistic and altruistic behavior, differentiating altru-prises its position, speed, and the distance and speed head-ism towards AVs and human-driven vehicles. The SVO of

Dinneweth et al. *Autonomous Intelligent Systems * \(2022\) 2:27 

Page 8 of 12

the AV weighs this trade-off and the distance of the sur-speed, and the distances and velocities of four neighboring rounding vehicles considered. 

vehicles. Actions comprise driving in the driving lane at a In their second paper, Toghi et al. \[51\] enhanced their suboptimal speed or driving in the overtaking lane with a approach using a 3D convolution network with the rela-higher velocity. The reward function exclusively promotes tive vehicle speeds as channels. Further experiments have safety and is shared among a local group of AVs depicted identified an optimal level of SVO that improves overall by coordination graphs. 

traffic flow and show that overly altruistic AVs reduce per-Bhalla et al. \[59\] learned AVs to better communicate formance. Their third paper achieves better results using a and coordinate on a highway. They measure them against multi-agent actor-critic algorithm \[52\]. 

DIAL, a benchmark algorithm that focuses on learning to Chen et al. \[53\] trained AVs to avoid collisions in a merg-communicate in cooperative tasks \[60\]. Unlike DIAL, their ing scenario using a supervisor prioritizing vehicles that method does not require past experiences, which mitigates merge because their situation is time-critical. AVs observe non-stationarity and stabilizes learning. AVs’ actions in-lateral and longitudinal positions and velocities of sur-clude sending messages, accelerating, decelerating, and di-rounding vehicles and pick up meta-action among lane rection change. The reward function does not provide ex-change, accelerating or decelerating. A reward function plicit rewards for cooperation between the agents but pro-promotes fast merging, high velocity, and safe time head-motes safety distance and penalizes crashes. 

way and penalizes collisions. This function is a global re-Liu et al. \[15\] proposed a framework for fleet control ward shared by all the AVs in the simulation for encourag-where each vehicle learns to maintain a constant headway ing coordination among AVs. 

with the vehicles ahead and behind on a highway. Each As the results of these articles noticed, socially desir-AV observes its position and speed, as well as those of able AVs improve the success rate of merging and exiting front and rear vehicles. To maintain the homogeneity of maneuvers. Nonetheless, this coordination is facilitated the fleet, a reward function penalizes the AVs which are because human-driven vehicles are all controlled by the not at equidistance to the front and rear vehicles or AVs IDM model and thus are easily predictable. Designing ro-whose velocity and acceleration differ from the group. 

bust AVs that cope with heterogeneous driver behavior and Palanisamy \[39\] designed MACAD, a simulation envi-traffic simulations will require comprehensive driver mod-ronment to simulate AV’s perception, decision-making, els. 

and control. In an intersection scenario, AVs’ observations are images captured from an onboard camera, and they **5.3 Heterogeneous HDVs**

can pick up one of the eight discrete actions controlling Robust AVs inevitably will have to be trained to drive steering angle, throttle, and brake. The function rewards in complex mixed traffic composed of heterogeneous

AVs crossing the intersection while maintaining a high human-driven vehicles \(HDV\). Some researchers \[54\] at-speed and avoiding collisions. Optionally a factor encour-tempted to learn an HDV model via inverse RL \(IRL\), a ages/discourages cooperativeness/competitiveness among technique for figuring out an agent’s reward function given the agents. 

its policy; but this approach is highly dependent on the Nakka et al. \[61\] tackled the coordination problem in a quality of the extracted data and the studied scenario. As merging scenario. The merging AV observes the distances a consequence, there is a need for a “realistic” and hetero-and velocities of the surrounding vehicles and the distance geneous HDV model. 

from the end of the merging zone. Actions allow the AV to Valiente et al. \[55\] extended the research of Toghi et al. 

accelerate or decelerate, and the reward function encour-by incorporating an SVO factor into the IDM model used ages agents to maintain their speed within a predefined for controlled HDVs. Similarly, Zhou et al. \[56\] endowed range and penalizes rear-end collisions. 

HDVs with a politeness factor, and Hu et al. \[57\] designed a social HDV model with different levels of cooperation. 

**5.5 Synthesis**

All the mentioned authors took advantage of their new We synthesize the previous papers according to the con-HDV models by enabling AVs to infer this SVO and thus cepts introduced in this survey \(Table 1\). Most authors anticipated which driver is prone to act altruistically or used single-agent RL methods, especially those based on not. 

DQN, to address MARL problems \(12 out of 16\) and

mainly adopted the CTDE scheme for MARL approaches

**5.4 Fully-autonomous fleet**

\(3 out of 4\). The action space’s nature seems to guide the When AVs reach the fifth level of automation, human motivations for using value-based or actor-critic methods drivers might be considered the main threat to road safety since the latter better deal with continuous action space. In and therefore be banned from driving. In this context, all addition, few articles used learning strategies or explicitly traffic will be composed of fully-autonomous fleets. 

mentioned them. 

Yu et al. \[58\] addressed the problem of coordination Interestingly, most papers \(12 out of 16\) focused their on the highway. AVs observe their current lane position, study on simulations involving few agents \(≤ 10\). This

Dinneweth et al. *Autonomous Intelligent Systems * \(2022\) 2:27 

Page 9 of 12

**Table 1 **Summary of papers according to the problem addressed and simulation settings. Scenarios include merging \(M\), exiting \(E\), highway \(H\) without merging nor exiting, urban navigation comprising intersections and roundabouts \(U\), and intersection \(I\). Learning strategies include Hierarchical Reinforcement Learning \(HRL\), Curriculum Learning \(CL\), Memory module \(Mem\), and Masking \(Mask\) Article

Class

Algorithm

Scheme

No. AVs

HDV model

Scenario

Simulator

Learning strat. 

Yu et al. \[58\]

Fleet

DQN

DTDE

≤ 20

–

H

–

–

Bhalla et al. \[59\]

Fleet

DQN

CTDE / DTDE

≤ 10

–

H

Gym-based

Mem, HRL

Liu et al. \[15\]

Fleet

DQN

–

≤ 10

–

H

–

–

Palanisamy \[39\]

Fleet

IMPALA1

CTDE

≤ 5

–

I

MACAD

–

Nakka et al. \[61\]

Fleet

DDPG

CTDE

≤ 10

–

M

–

–

Wang et al. \[48\]

Mixed

PPO

–

≤ 10

IDM

U

Flow

–

Dong et al. \[31\]

Mixed

DQN

CTDE

≤ 20

IDM-LC2013

E

Flow

Mem, Mask

Han and Wang \[49\]

Mixed

MADDPG

CTDE

≤ 30

CARLA-autopilot

H

CARLA

–

Toghi et al. \[50\]

Social

DQN

DTDE

≤ 5

IDM-MOBIL

M

Highway-env

–

Toghi et al. \[51\]

Social

DQN

DTDE

≤ 5

IDM-MOBIL

M

Highway-env

–

Toghi et al. \[52\]

Social

MA2C

DTDE

≤ 5

IDM-MOBIL

M / E

Highway-env

–

Chen et al. \[53\]

Social

MA2C

CTDE

≤ 5

IDM-MOBIL

M

Highway-env

CL, Mask

Valiente et al. \[55\]

HDV

DQN

DTDE

≤ 5

IDM-MOBIL2

M / E

Highway-env

–

Zhou et al. \[56\]

HDV

A2C

DTDE

≤ 5

IDM-MOBIL2

H

Highway-env

–

Hu et al. \[57\]

HDV

MA2C

CTDE

≤ 10

IDM2

M

–

CL

1 Single-agent actor-critic algorithm designed for multi-task RL \[63\]. 

2 Modified version. 

choice is presumably motivated by the MARL challenges, models into real-world traffic would likely result in acci-notably the curse of dimensionality \[62\]. 

dents. 

Most studies investigated highway driving and merging Therefore, developing convincing driver models for safe scenarios \(13 out of 16\), as these critical maneuvers involve driving is critical, as driving styles vary among countries anticipation and often cause accidents to AVs. For their and cultures \[65\]. Attempts have been made using in-simulations, Gym-based environments prevail due to their verse reinforcement learning \(IRL\), but these algorithms manageable API for RL. Similarly, IDM prevails because of are overly dependent on the situations under study and fre-its efficiency and computational simplicity. 

quently fail to generalize. Others have proposed utilizing Since 2019, few papers have addressed AVs’ decision-MARL algorithms to learn social norms, which may be a making using MARL compared to those using single-agent new field of research \[66\]. 

RL. Due to the limited number of articles dealing with Another way to prepare AVs for real-world traffic is to MARL, our conclusions may be biased, so we invite read-make them trustworthy by incorporating interpretability. 

ers to consider this. 

Explainable artificial intelligence \(EAI\) is an important research topic gaining interest over the years, mainly be-6 Open challenges and conclusion

cause lawmakers require AI to be interpretable, as in Eu-Overall, most studies focus on simulations rather than ad-rope with the general data protection regulation \(GDPR6\). 

dressing transferability to real traffic scenarios. The needs Therefore, robust AVs should incorporate interpretable al-for “realistic” driver models, safe and interpretable models gorithms providing security and robustness guarantees. 

are two significant problems for AV simulation discussed Interpreting MARL policies involves explaining short- and in this section. 

long-term decision-making and interactions of multiple Safety is undoubtedly the critical point of the develop-agents. This may be accomplished via Causal MARL \[67\]. 

ment of AV algorithms. In MARL, designing a safe policy is Since multi-agent simulations, and MARL algorithms

a real challenge that implies considering safety constraints in a broader way, enable the emergence of organizational at the agent and group levels. The constrained markov de-structures, it might be interesting to investigate how self-cision process \(CMDP\) framework provides tools for de-organization occurs in a fully autonomous fleet with no signing such safe RL \[64\] algorithms. 

predetermined rules. While researchers tend to incorpo-Most studies agree that existing HDV models are unre-rate standards into AVs’ decision-making, they do not rule alistic because they disregard human characteristics such them out for the fully-autonomous fleets. These emergent as psychological and biological traits. Although some re-organizations may be more appropriate for AVs than cur-searchers tried to provide heterogeneity in HDV models, rent regulations based on humans’ limitations. 

their models are still limited to a single SVO trait. Besides, despite their differences, HDV and AV models behave deterministically. Introducing AVs trained with these HDV

6 https://gdpr-info.eu/



Dinneweth et al. *Autonomous Intelligent Systems * \(2022\) 2:27 

Page 10 of 12

We posed two research questions in the introduction \(1\), **Author details**

1

which we now address. 

TS2-MOSS, Univ. Gustave Eiffel, 77454, Champs-sur-Marne, France. 2ENS

Paris-Saclay, CNRS, SATIE, Université Paris-Saclay, 91190, Gif-sur-Yvette, France. 

• *RQ1*. Recent AVs’ decision-making research focused 3 CNRS, UMR 8201—LAMIH, Univ. Polytechnique Hauts-de-France, F-59313, on two paradigms. On the one hand, since

Valenciennes, France. 

autonomous vehicles may soon coexist with human

drivers, mixed traffic received much attention. Some **Publisher’s Note**

studies concentrated on improving traffic safety and Springer Nature remains neutral with regard to jurisdictional claims in throughput, while others proposed empowering AVs

published maps and institutional affiliations. 

with social abilities. Some attempted to design HDV

Received: 31 May 2022 Revised: 26 October 2022

models that mimic driver altruism to robustify AVs’

Accepted: 30 October 2022

policies. On the other hand, since human drivers

**References**

might be banned from traffic, some researchers

1. S. Trommer, V. Kolarova, E. Fraedrich, L. Kröger, B. Kickhöfer, T. Kuhnimhof, B. 

devised fully-autonomous fleets that should enhance Lenz, P. Phleps, The Impact of Vehicle Automation on Mobility Behaviour. 

Auton. Driv. 94, \(2016\)

the overall traffic flow and security. 

2. D. Petrović, R. Mijailović, D. Pešić, Traffic accidents with autonomous

• *RQ2*. Designing traffic simulations with adequate vehicles: type of collisions, manoeuvres and errors of conventional HDV models is challenging, and despite the proposed vehicles’ drivers. Transp. Res. Proc. 45, 161–168 \(2020\). 

https://doi.org/10.1016/j.trpro.2020.03.003

models, none covered the heterogeneity of human

3. G.J. Wilde, Social interaction patterns in driver behavior: an introductory behavior. Given the current limitations, it seems

review. Hum. Factors 18\(5\), 477–492 \(1976\)

involved to consider mixed traffic, and future research 4. M. Haglund, L. Åberg, Speed choice in relation to speed limit and influences from other drivers. Transp. Res., Part F Traffic Psychol. Behav. 

will likely pay more attention to this problem. In

3\(1\), 39–51 \(2000\)

addition, since intersections and roundabouts are

5. R.S. Sutton, A.G. Barto, *Reinforcement Learning: An Introduction*, Adaptive manifolds, most studies concentrated on the most

Computation and Machine Learning Series, 2nd edn. \(MIT Press, Cambridge, 2018\)

straightforward scenarios, such as highway driving, 6. D. Silver, A. Huang, C.J. Maddison, A. Guez, L. Sifre, G. Van Den Driessche, J. 

merging, and exiting. Finally, most experiments

Schrittwieser, I. Antonoglou, V. Panneershelvam, M. Lanctot et al., involved few agents due to the aforementioned MARL

Mastering the game of go with deep neural networks and tree search. 

Nature 529\(7587\), 484–489 \(2016\)

challenges \[62\]. 

7. D. Silver, T. Hubert, J. Schrittwieser, I. Antonoglou, M. Lai, A. Guez, M. 

In conclusion, RL and MARL algorithms have recently Lanctot, L. Sifre, D. Kumaran, T. Graepel et al., Mastering chess and shogi by self-play with a general reinforcement learning algorithm \(2017\). arXiv received interest due to their recent achievements and preprint. arXiv:1712.01815

generalization capabilities. They provide a practical ap-8. J. Schrittwieser, I. Antonoglou, T. Hubert, K. Simonyan, L. Sifre, S. Schmitt, A. 

proach for learning complex policies involving real-time Guez, E. Lockhart, D. Hassabis, T. Graepel, T. Lillicrap, D. Silver, Mastering atari, go, chess and shogi by planning with a learned model. Nature decision-making in stochastic environments. However, 588\(7839\), 604–609 \(2020\). https://doi.org/10.1038/s41586-020-03051-4

many challenges remain in mitigating the scalability when 9. O. Vinyals, I. Babuschkin, W.M. Czarnecki, M. Mathieu, A. Dudzik, J. Chung, involving numerous agents. Furthermore, mixed traffic D.H. Choi, R. Powell, T. Ewalds, P. Georgiev et al., Grandmaster level in starcraft ii using multi-agent reinforcement learning. Nature 575\(7782\), does not meet the security standards in the current simu-350–354 \(2019\)

lations. Recent papers attempted to mimic human behav-10. L.M. Schmidt, J. Brosig, A. Plinge, B.M. Eskofier, C. Mutschler, An ior, particularly social capabilities, to enforce AVs’ policies. 

introduction to multi-agent reinforcement learning and review of its application to autonomous mobility \(2022\). arXiv preprint. 

Given current AVs’ algorithms, future research will most

arXiv:2203.07676

likely continue to design less deterministic driver models. 

11. B.B. Elallid, N. Benamar, A.S. Hafid, T. Rachidi, N. Mrani, A comprehensive survey on the application of deep and reinforcement learning approaches in autonomous driving. J. King Saud Univ, Comput. Inf. Sci. \(2022\). 

https://doi.org/10.1016/j.jksuci.2022.03.013

**Funding**

12. B.R. Kiran, I. Sobh, V. Talpaert, P. Mannion, A.A. Al Sallab, S. Yogamani, P. 

This manuscript was funded by the European Union’s Horizon 2020 research Pérez, Deep reinforcement learning for autonomous driving: a survey. IEEE

and innovation programme under grant agreement No 815001 \(project Trans. Intell. Transp. Syst. \(2021\). https://doi.org/10.1109/TITS.2021.3054625

DriveToTheFuture\). 

13. F. Ye, S. Zhang, P. Wang, C.-Y. Chan, A survey of deep reinforcement learning algorithms for motion planning and control of autonomous **Availability of data and materials**

vehicles, in *2021 IEEE Intelligent Vehicles Symposium \(IV\) *\(IEEE Press, New Not applicable. 

York, 2021\), pp. 1073–1080

14. Z. Zhu, H. Zhao, A survey of deep rl and il for autonomous driving policy learning. IEEE Trans. Intell. Transp. Syst. \(2021\). 

**Declarations**

https://doi.org/10.1109/TITS.2021.3134702

15. B. Liu, Z. Ding, C. Lv, Platoon control of connected autonomous vehicles: a **Competing interests**

distributed reinforcement learning method by consensus. 

The authors declare that they have no competing interests. 

IFAC-PapersOnLine 53\(2\), 15241–15246 \(2020\)

16. C.J. Watkins, P. Dayan, Q-learning. Mach. Learn. 8\(3\), 279–292 \(1992\) **Author contribution**

17. V. Mnih, A.P. Badia, M. Mirza, A. Graves, T. Lillicrap, T. Harley, D. Silver, K. 

Original draft preparation, JD; writing—review and editing, JD, AB, SE and RM. 

Kavukcuoglu, Asynchronous methods for deep reinforcement learning, in All authors have read and agreed to the published version of the manuscript. 

*International Conference on Machine Learning *\(PMLR, 2016\), pp. 1928–1937

Dinneweth et al. *Autonomous Intelligent Systems * \(2022\) 2:27 

Page 11 of 12

18. T.P. Lillicrap, J.J. Hunt, A. Pritzel, N. Heess, T. Erez, Y. Tassa, D. Silver, D. 

40. C. Munduteguy, Reconnaissance d’intention et prédiction d’action pour la Wierstra, Continuous control with deep reinforcement learning \(2015\). 

gestion des interactions en environnement dynamique. PhD thesis, Paris, arXiv preprint. arXiv:1509.02971

CNAM \(2001\)

19. J. Schulman, S. Levine, P. Abbeel, M. Jordan, P. Moritz, Trust region policy 41. C. Munduteguy, F. Darses, Perception et anticipation du comportement optimization, in *International Conference on Machine Learning *\(PMLR, 2015\), d’autrui en situation simulée de conduite automobile. Le Trav. Hum. 70\(1\), pp. 1889–1897

1–32 \(2007\)

20. K. Zhang, Z. Yang, T. Ba¸sar, Multi-agent reinforcement learning: a selective 42. Q. Chao, H. Bi, W. Li, T. Mao, Z. Wang, M.C. Lin, Z. Deng, A survey on visual overview of theories and algorithms. Handb. Reinf. Learn. Control, 321–384

traffic simulation: models, evaluations, and applications in autonomous \(2021\)

driving, in *Computer Graphics Forum*, vol. 39 \(Wiley, New York, 2020\), pp. 

21. T. Chu, J. Wang, L. Codecà, Z. Li, Multi-agent deep reinforcement learning 287–308

for large-scale traffic signal control. IEEE Trans. Intell. Transp. Syst. 21\(3\), 43. S.P. Hoogendoorn, P.H. Bovy, State-of-the-art of vehicular traffic flow 1086–1095 \(2019\)

modelling. Proc. Inst. Mech. Eng., Part I, J. Syst. Control Eng. 215\(4\), 22. R. Lowe, Y.I. Wu, A. Tamar, J. Harb, O. Pieter Abbeel, I. Mordatch, Multi-agent 283–303 \(2001\)

actor-critic for mixed cooperative-competitive environments. Adv. Neural 44. S. Moridpour, M. Sarvi, G. Rose, Lane changing models: a critical review. 

Inf. Process. Syst. 30, \(2017\). https://doi.org/10.5555/3295222.3295385

Transp. Lett. 2\(3\), 157–173 \(2010\). 

23. P. Hernandez-Leal, M. Kaisers, T. Baarslag, E.M. de Cote, A Survey of

https://doi.org/10.3328/TL.2010.02.03.157-173

Learning in Multiagent Environments: Dealing with Non-Stationarity 45. M. Treiber, A. Hennecke, D. Helbing, Congested traffic states in empirical \(2019\). arXiv:1707.09183 \[cs\]

observations and microscopic simulations. Phys. Rev. E 62\(2\), 1805–1824

24. Y. Shoham, K. Leyton-Brown, *Multiagent Systems: Algorithmic,* \(2000\). https://doi.org/10.1103/PhysRevE.62.1805

*Game-Theoretic, and Logical Foundations *\(Cambridge University Press, USA, 46. A. Kesting, M. Treiber, D. Helbing, General lane-changing model MOBIL for 2008\)

car-following models. Transp. Res. Rec. 1999\(1\), 86–94 \(2007\). 

25. J.K. Gupta, M. Egorov, M. Kochenderfer, Cooperative multi-agent control

https://doi.org/10.3141/1999-10

using deep reinforcement learning, in *International Conference on* 47. J. Erdmann, Lane-changing model in sumo. Proc. SUMO2014 Model. 

*Autonomous Agents and Multiagent Systems *\(Springer, Berlin, 2017\), pp. 

Mobil. Open Data 24, 77–88 \(2014\)

66–83

48. J. Wang, T. Shi, Y. Wu, L. Miranda-Moreno, L. Sun, Multi-agent graph 26. P. Hernandez-Leal, B. Kartal, M.E. Taylor, A survey and critique of multiagent reinforcement learning for connected automated driving, in *Conference:* deep reinforcement learning. Auton. Agents Multi-Agent Syst. 33\(6\), *ICML Workshop on AI for Autonomous Driving *\(2020\), p. 7

49. S. Han, H. Wang, Stable and efficient Shapley value-based reward 750–797 \(2019\)

reallocation for multi-agent reinforcement learning of autonomous 27. T.T. Nguyen, N.D. Nguyen, S. Nahavandi, Deep reinforcement learning for vehicles, in *2022 IEEE International Conference on Robotics and Automation* multiagent systems: a review of challenges, solutions, and applications. 

\(2022\)

IEEE Trans. Cybern. 50\(9\), 3826–3839 \(2020\). 

50. B. Toghi, R. Valiente, D. Sadigh, R. Pedarsani, Y.P. Fallah, Social Coordination

https://doi.org/10.1109/TCYB.2020.2977374

and Altruism in Autonomous Driving. IEEE Trans. Intell. Veh. \(2022\). 

28. L. Canese, G.C. Cardarilli, L. Di Nunzio, R. Fazzolari, D. Giardino, M. Re, S. 

https://doi.org/10.1109/TITS.2022.3207872

Spanò, Multi-agent reinforcement learning: a review of challenges and 51. B. Toghi, R. Valiente, D. Sadigh, R. Pedarsani, Y.P. Fallah, Cooperative applications. Appl. Sci. 11\(11\), 4948 \(2021\). 

autonomous vehicles that sympathize with human drivers, in *2021*

https://doi.org/10.3390/app11114948

*IEEE/RSJ International Conference on Intelligent Robots and Systems \(IROS\)* 29. S. Gronauer, K. Diepold, Multi-agent deep reinforcement learning: a survey. 

\(2021\), pp. 4517–4524. https://doi.org/10.1109/IROS51168.2021.9636151

Artif. Intell. Rev. 55\(2\), 895–943 \(2022\). 

52. B. Toghi, R. Valiente, D. Sadigh, R. Pedarsani, Y.P. Fallah, Altruistic maneuver

https://doi.org/10.1007/s10462-021-09996-w

planning for cooperative autonomous vehicles using multi-agent 30. A. OroojlooyJadid, D. Hajinezhad, A Review of Cooperative Multi-Agent advantage actor-critic, in *2021 IEEE/CVF Conference on Computer Vision and* Deep Reinforcement Learning \(2021\) arXiv:1908.03963 \[cs, math, stat\]

*Pattern Recognition \(CVPR 2021\) *\(2021\)

31. J. Dong, S. Chen, P.Y.J. Ha, Y. Li, S. Labi, A drl-based multiagent cooperative 53. D. Chen, Z. Li, M. Hajidavalloo, K. Chen, Y. Wang, L. Jiang, Y. Wang, Deep control framework for cav networks: a graphic convolution q network Multi-agent Reinforcement Learning for Highway On-Ramp Merging in \(2020\). arXiv preprint. arXiv:2010.05437

Mixed Traffic \(2022\). arXiv:2105.05701 \[cs, eess\]

32. Y. Bengio, J. Louradour, R. Collobert, J. Weston, Curriculum learning, in 54. W. Schwarting, A. Pierson, J. Alonso-Mora, S. Karaman, D. Rus, Social *Proceedings of the 26th Annual International Conference on Machine* behavior for autonomous vehicles. Proc. Natl. Acad. Sci. 116\(50\), *Learning—ICML’09 *\(ACM Press, Montreal, 2009\), pp. 1–8. 

24972–24978 \(2019\)

https://doi.org/10.1145/1553374.1553380

55. R. Valiente, B. Toghi, R. Pedarsani, Y.P. Fallah, Robustness and adaptability of 33. S. Pateria, B. Subagdja, A.-H. Tan, C. Quek, Hierarchical reinforcement reinforcement learning-based cooperative autonomous driving in learning: a comprehensive survey. ACM Comput. Surv. \(CSUR\) 54\(5\), 1–35

mixed-autonomy traffic. IEEE Open J. Intell. Transp. Syst. 3, 397–410 \(2022\) \(2021\)

56. W. Zhou, D. Chen, J. Yan, Z. Li, H. Yin, W. Ge, Multi-agent reinforcement 34. Y. Chen, C. Dong, P. Palanisamy, P. Mudalige, K. Muelling, J.M. Dolan, learning for cooperative lane changing of connected and autonomous Attention-based hierarchical deep reinforcement learning for lane change vehicles in mixed traffic. Auton. Intell. Syst. 2\(1\), 5 \(2022\). 

behaviors in autonomous driving, in *2019 IEEE/CVF Conference on Computer*

https://doi.org/10.1007/s43684-022-00023-5

*Vision and Pattern Recognition Workshops \(CVPRW\) *\(2019\), pp. 1326–1334. 

57. Y. Hu, A. Nakhaei, M. Tomizuka, K. Fujimura, Interaction-aware decision

https://doi.org/10.1109/CVPRW.2019.00172

making with adaptive strategies under merging scenarios, in *2019 IEEE/RSJ*

35. A. Dosovitskiy, G. Ros, F. Codevilla, A. Lopez, V. Koltun, Carla: an open urban *International Conference on Intelligent Robots and Systems \(IROS\) *\(IEEE Press, driving simulator, in *Conference on Robot Learning *\(PMLR, 2017\), pp. 1–16

New York, 2019\), pp. 151–158

36. C. Wu, A. Kreidieh, K. Parvate, E. Vinitsky, A.M. Bayen, Flow: architecture and 58. C. Yu, X. Wang, X. Xu, M. Zhang, H. Ge, J. Ren, L. Sun, B. Chen, G. Tan, benchmarking for reinforcement learning in traffic control \(2017\). arXiv Distributed multiagent coordinated learning for autonomous driving in preprint. arXiv:1710.05465

highways based on dynamic coordination graphs. IEEE Trans. Intell. Transp. 

37. M. Behrisch, L. Bieker, J. Erdmann, D. Krajzewicz, Sumo–simulation of urban Syst. 21\(2\), 735–748 \(2020\). https://doi.org/10.1109/TITS.2019.2893683

mobility: an overview, in *Proceedings of SIMUL 2011, The Third International* 59. S. Bhalla, S. Ganapathi Subramanian, M. Crowley, Deep multi agent *Conference on Advances in System Simulation *\(ThinkMind, 2011\) reinforcement learning for autonomous driving, in *Canadian Conference on* 38. Y. Duan, X. Chen, R. Houthooft, J. Schulman, P. Abbeel, Benchmarking deep *Artificial Intelligence *\(Springer, Berlin, 2020\), pp. 67–78. 

reinforcement learning for continuous control, in *International Conference*

https://doi.org/10.1007/978-3-030-47358-7\_7

*on Machine Learning *\(PMLR, 2016\), pp. 1329–1338

60. J. Foerster, I.A. Assael, N. De Freitas, S. Whiteson, Learning to communicate 39. P. Palanisamy, Multi-agent connected autonomous driving using deep with deep multi-agent reinforcement learning. Adv. Neural Inf. Process. 

reinforcement learning, in *2020 International Joint Conference on Neural* Syst. 29, \(2016\). https://doi.org/10.5555/3157096.3157336

*Networks \(IJCNN\) *\(IEEE, Glasgow, 2020\), pp. 1–7. 

61. S.K.S. Nakka, B. Chalaki, A.A. Malikopoulos, A multi-agent deep

https://doi.org/10.1109/IJCNN48605.2020.9207663

reinforcement learning coordination framework for connected and

Dinneweth et al. *Autonomous Intelligent Systems * \(2022\) 2:27 

Page 12 of 12

automated vehicles at merging roadways, in *2022 American Control* *Conference \(ACC\) *\(IEEE, New York, 2022\), pp. 3297–3302

62. L. Wang, Z. Yang, Z. Wang, Breaking the curse of many agents: provable mean embedding q-iteration for mean-field reinforcement learning, in *International Conference on Machine Learning *\(PMLR, 2020\), pp. 

10092–10103

63. L. Espeholt, H. Soyer, R. Munos, K. Simonyan, V. Mnih, T. Ward, Y. Doron, V. 

Firoiu, T. Harley, I. Dunning, S. Legg, K. Kavukcuoglu, Impala: scalable distributed deep-rl with importance weighted actor-learner architectures, in *International Conference on Machine Learning*, vol. 80 \(PMLR, 2018\), pp. 

1407–1416

64. J. Garcıa, F. Fernández, A comprehensive survey on safe reinforcement learning. J. Mach. Learn. Res. 16\(1\), 1437–1480 \(2015\) 65. T. Özkan, T. Lajunen, J.E. Chliaoutakis, D. Parker, H. Summala, Cross-cultural differences in driving behaviours: a comparison of six countries. Transp. 

Res., Part F Traffic Psychol. Behav. 9\(3\), 227–242 \(2006\) 66. E. Vinitsky, R. Köster, J.P. Agapiou, E. Duéñez-Guzmán, A.S. Vezhnevets, J.Z. 

Leibo, A learning agent that acquires social norms from public sanctions in decentralized multi-agent settings \(2021\). arXiv preprint. arXiv:2106.09012

67. S.J. Grimbly, J. Shock, A. Pretorius, Causal Multi-Agent Reinforcement Learning: Review and Open Problems \(2021\). arXiv:2111.06721 \[cs, stat\]



# Document Outline

+ Multi-agent reinforcement learning for autonomous vehicles: a survey  
	+ Abstract  
		+ Keywords 

	+ Introduction 
	+ Reinforcement learning  
		+ Single-agent reinforcement learning 
		+ Multi-agent reinforcement learning 

	+ Learning schemes  
		+ Centralization and decentralization  
			+ Centralized training centralized execution \(CTCE\) 
			+ Decentralized training decentralized execution \(DTDE\) 
			+ Centralized training decentralized execution \(CTDE\)  
				+ Parameter sharing 
				+ Centralized critic decentralized actor 


		+ Learning strategies  
			+ Memory 
			+ Masking 
			+ Curriculum learning 
			+ Hierarchical reinforcement learning \(HRL\) 


	+ MARL-based driving simulation environments  
		+ Simulation environments 
		+ Driving scenarios 
		+ Human driver models 

	+ MARL algorithms for AVs  
		+ Mixed traffic 
		+ Socially desirable AVs 
		+ Heterogeneous HDVs 
		+ Fully-autonomous fleet 
		+ Synthesis 

	+ Open challenges and conclusion 
	+ Funding 
	+ Availability of data and materials 
	+ Declarations 
	+ Competing interests 
	+ Author contribution 
	+ Author details 
	+ Publisher's Note 
	+ References



