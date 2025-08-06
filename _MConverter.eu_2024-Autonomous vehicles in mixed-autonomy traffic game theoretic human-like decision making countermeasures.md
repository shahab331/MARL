Chen *et al*. *Complex Eng Syst * 2024;4:25

**Complex Engineering**

**DOI: **10.20517/ces.2024.69

**Systems**

**Review**

**Open Access**

**Autonomous vehicles in mixed-autonomy traffic: game**

**theoretic human-like decision making countermeasures**

**Qitong Chen1, Dong Zhao1, Congzhi Liu2, Meng Yang3, Yehui Shi3**

1The School of Technology, Beijing Forestry University, Beijing 100083, China. 

2The State Key Laboratory of Mechanical Transmission, College of Mechanical and Vehicle Engineering, Chongqing University, Chongqing 400044, China. 

3Zhiyuan Laboratory, Hangzhou 310020, Zhejiang, China. 

**Correspondence to: **Prof. Congzhi Liu, The State Key Laboratory of Mechanical Transmission, College of Mechanical and Vehicle Engineering, Chongqing University, 174 Shazheng Street, Chongqing 400044, China. E-mail: 15281063684@163.com; ORCID: 0000-0002-2977-1365

**How to cite this article: **Chen Q, Zhao D, Liu C, Yang M, Shi Y. Autonomous vehicles in mixed-autonomy traffic: game theoretic human-like decision making countermeasures. *Complex Eng Syst * 2024;4:25. http://dx.doi.org/10.20517/ces.2024.69

**Received: **9 Oct 2024

**First Decision: **21 Nov 2024

**Revised: **13 Dec 2024

**Accepted: **23 Dec 2024

**Published: **30 Dec 2024

**Academic Editor: **Zhaojing Wu

**Copy Editor: **Fangling Lan

**Production Editor: **Fangling Lan

**Abstract**

Human-like decision-making plays a pivotal role in enhancing the human-likeness of autonomous vehicles and ensuring seamless blending into human-driven vehicles-dominated traffic. Due to the ability to capture the interaction between drivers, it has great potential to apply game theory in the development of human-like decision-making algorithms. However, there are few reviews that systematically focused on the human-like decision-making strategy based on game theory. To this end, this paper is targeted to present a comprehensive and up-to-date summary of game theoretic human-like decision-making methods for autonomous vehicles in mixed-autonomy traffic by review-ing cutting-edge research conducted for various scenarios. The questions discussed in this article include: \(1\) What are the implications of social interactions for human-like decision-making development; and \(2\) How to establish the human-like decision-making algorithm with game theory, satisfying personalized requirements and coping with the uncertainty and randomness of complex traffic environment. To provide sound answers, the pivotal factors influencing decision performance are concluded based on the existing social interaction research and human-like decision methods. Through a comprehensive analysis, the development framework of the human-like game theoretic algorithm is proposed. Finally, the critical academic issues are concluded for indicating the future research directions. 

**Keywords: **Mixed autonomy, social interaction, game theoretic scheme, human-like decision-making, socially compatible

© The Author\(s\) 2024. **Open Access **This article is licensed under a Creative Commons Attribution 4.0

International License \(https://creativecommons.org/licenses/by/4.0/\), which permits unrestricted use, shar-ing, adaptation, distribution and reproduction in any medium or format, for any purpose, even commercially, as long as you give appropriate credit to the original author\(s\) and the source, provide a link to the Creative Commons license, and indicate if changes were made. 

www.oaepublish.com/comengsys

Page 2 of 27

Chen *et al*. *Complex Eng Syst * 2024;4:25

**I**

http://dx.doi.org/10.20517/ces.2024.69

**1. INTRODUCTION**

Statistics about traffic safety have indicated that 94% of crashes are provoked by human errors, for example, inattention, distractions, and decision errors\[1\]. With the rapid development of vehicle automation, autonomous vehicles \(AVs\) have shown great promise to eliminate human error-induced accidents due to accurate and timely execution, further improving traffic safety\[2\]. However, before fully automated driving becomes widespread, AVs will blend into roads populated with human-driven vehicles \(HDVs\) in the near future which results in a mixed-autonomy traffic context. Similar to HDV-HDV social interaction, AVs will interact with surrounding vehicles \(SVs\), either AVs or HDVs, forming different configurations. AV-HDV

interaction is more complex owing to human uncertainty. Also, driven by the personalized needs of passengers, human-like decision-making considering social interaction is proposed to enable AVs to make more informed and human-like decisions. However, humans, vehicles, and traffic environments are closely inter-twined in reality which makes social interaction exhibit dynamicity and continuity, uncertainty and variability, interdependence and mutual influence. Thus, qualitatively understanding the social interaction mechanism and evolution law contributes to developing high-fidelity interactive models and making human-like decisions. Based on the interaction mechanism, how to develop a human-like decision-making algorithm is the core problem discussed in this paper. Human-like decision-making algorithms are supposed to be equipped with at least one of the following characteristics: \(1\) scene adaptation; \(2\) personalized adjustment; \(3\) decision interpretability; and \(4\) reasoning and learning abilities\[2\]. Additionally, the close linkage nature increases the computational complexity, which poses a new challenge to the real-time performance of the decision-making algorithm. Achieving real-time receding horizon optimization and adjustment is pivotal to ensuring safe driving. 

Game theory, possessing an inherent ability to analyze decision dependence among entities, has exhibited a superior understanding of complex interactive decisions and uncertain behaviors. Motivated by this, it has been widely introduced into the transportation field to tackle conflict or coordination problems\[3,4\]. Article\[5\] reviewed the use of game theory for autonomous system decisions from a risk perspective, but lacked a specific approach to self-driving vehicles. In contrast, reviews\[6,7\] concluded applications of game theory in transportation for security assessment and traffic congestion resolution, respectively. In recent years, game theory has been adopted to develop AVs’ decision-making algorithms, aiming to mimic the dynamic and interactive decision-making process of human drivers. In this sense, game theoretic decision methods hold significant potential for augmenting the social decision-making prowess of AVs, and further facilitating a seamless blending of AVs into the HDV-populated traffic. It should be noted that the interactive vehicles are referred to as “agents” 

or “players” in the game theoretic framework, which is applicable in this paper. Di and Shi\[8\] overviewed the effective control models from artificial intelligence in the domain of transportation engineering in the era of mixed autonomy, but did not give a systematic discussion of game-based control. The ref. \[9\] reviews the game theory-based methods for modeling driver behavior, but focuses only on the lane-changing \(LC\) process and does not investigate the decision-making methods in more complex scenarios, such as roundabouts and unsignalized intersections. The ref.\[10\] reviewed the game theoretic models for explaining road user behavior, but neglected the influence of heterogeneous factors, such as gender, age and experience, on different driving behaviors. However, the application of the models in multi-vehicles and their scalability in other scenarios are limited. While they address the issues outlined in the abstract, they fail to account for the dynamics and uncertainty of interactions. Moreover, real-time solutions are not discussed. In practice, AVs are expected to make distinguished behavior responses to HDVs with diverse driving characteristics. The fast and accurate recognition of the driving characteristics of the interactive objects is also a significant component of human-like decision-making strategies. 

In conclusion, given the complexity of AV-HDV interaction, it is expected that AVs will be equipped with well-designed human-like decision-making strategies with adaptation and learning capabilities. Hence, this paper reviews and analyzes the latest research in the field of game theoretic decision-making of AVs. Particularly, we

Chen *et al*. *Complex Eng Syst * 2024;4:25

**I**

http://dx.doi.org/10.20517/ces.2024.69

Page 3 of 27

Safe and Socially Compatible Autonomous Driving

**Game theoretic decision-making **

**Social interaction**

**Methods in determined environments**

Dynamics

Measurement

Decision

Multi-agent

Time-varying

Real-time

Uncertain

One-shot games type

interaction attributions

non-zero-

mixed-motive 

normal-

sum game

games

form game

**Human-like game theoretic decision **

**Game theoretic dynamic interaction models**

**making and control with adaptation**

Interactive 

Stackelb

differenti

potential level-k 

Time-varying

decision making

erg game

al game

game

game

control

Games with driving 

Games integrated 

motion

Multi-agent 

prediction

Receding horizon 

characteristics 

with learning 

game

control

evaluation

methods

One-step utility function

game

consider

Driving style

Level-k game 

driving 

traveling 

ride 

Multi-move 

action

Model prediction 

primitives 

uncertainty

safety

efficiency

comfort

games

decision 

control

Markov game

Intent 

traffic 

driving 

Cumulative 

Linear-quadratic 

sociality 

Reinforcement

rules

characteristics

utility function

control

Sociality

learning

**Figure 1. **Paper framework. 

explore game theory-based human-like methods considering the dynamic and uncertain interaction among on-road vehicles including AVs and/or HDVs. The human-like decision strategy could be broken down into two main components: social interaction understanding and game theoretic interaction modeling. These components give rise to two critical questions: The first is what the implications of social interactions are for the development of human-like decision-making. The second concerns how to establish a human-like decision-making algorithm with game theory, satisfying personalized requirements and coping with the uncertainty and randomness of complex traffic environments. The contributions of this paper lie in twofold: \(1\) With a view to AV-HV interaction in mixed-autonomy traffic, we comprehensively review the game theoretic human-like decision-making methods, presenting the results of this review and future research directions; and \(2\) The influencing factors considered in game theoretic decision-making methods are summarized systematically. 

To provide more reasoned answers to these questions, we review the status quo of related studies according to the logic structure shown in Figure 1. Firstly, we investigate the existing definitions of social interaction and explore its intrinsic properties in section 2. Building upon these attributions, pivotal factors affecting the human-like performance of the AV decision-making algorithm are analyzed and summarized in section

3. Then, starting with the definition of deterministic environment, section 4 discusses the game theoretic decision-making algorithms in deterministic environments including the existing design methods of utility function. The overview of game theoretic decision frameworks in deterministic environments provides fundamental knowledge for the development of more complex interactive decision strategies. section 5 covers state-of-the-art dynamic game theoretic techniques used for dynamic interaction modeling and the integrated methods of decision making and control considering time-varying characteristics in dynamic interaction scenarios. In section 6, we review human-like decision-making and control methods with adaptation, such as those employing Markov or level-k games and reinforcement learning \(RL\), along with estimation methods of incomplete information such as driving style, driving intentions, and social factors. Finally, in section 7, we conclude by summarizing the challenges and insights from existing human-like game theoretic decision and control methods, and suggest future research directions. 

**2. DEFINITION AND ATTRIBUTES OF SOCIAL INTERACTION IN ROAD TRAFFIC**

Human driving behaviors generally involve both social interactions among drivers and their physical interactions with the driving environment\[11\]. Rational human drivers can make socially compatible decisions in dynamically complex scenes by performing efficient negotiation with their neighbors using non-linguistic communications such as gesture language \(e.g., waving hands to the other car to give way\), deictics \(e.g., using turn signals to indicate intentions\), and motion cues \(e.g., accelerating/decelerating/turning\)\[12\]. Due to the





Page 4 of 27

Chen *et al*. *Complex Eng Syst * 2024;4:25

**I**

http://dx.doi.org/10.20517/ces.2024.69

Agent 1

Agent 2

Delivery

Measurement Perception

n

on

rizo

ho

ng

Multi-move game

State

Utility

die

ding horize

Utility

Perception

Delivery

State

ec

ce

R

action

Measurement

action

R

motive

Motive

Decision

Decision

**Figure 2. **Illustration of Interaction attribute-oriented game theoretic decision-making process. 

uncertainties and continuous closed-loop feedback among human drivers, social interactions are more intri-cate to quantify than physical interactions. Markkula *et al*. pointed out that the conceptual understanding of social interaction would facilitate the development of accurate theoretical models, high-fidelity simulation tools, and stringent technical requirements for vehicle automation\[13\]. Thus, a review of mainstream definitions of social interaction is undertaken first. 

**2.1 Definition and attribution of social interaction**

The research about interaction covers multiple academic disciplines, each with varying definitions. In the fields of artificial intelligence and robotics, the study of interactions in transportation has attracted significant academic attention and effort. Review\[13\] provided a general understanding and interpretation of road traffic interaction in a cross-theoretical sense, which emphasized the interactive objectives, condition of interaction occurrence and the reciprocality of coordination, but at a loss to reveal the underlying dynamic process of road traffic interaction. Many scholars hold that road traffic interactions share fundamental features similar to human interactions, such as coordination, collaboration, competition, negotiation, \[10, 14,15\] and communication\[16\]. Inspired by this, three fundamental characteristics of social interaction, i.e., dynamics, measurement, and decision, were excavated\[11\]. Revolving around these interaction attributes, we illustrate the two-agent interaction process from the perspective of game theory in Figure 2, with reference to the closed-loop formalism of interaction\[11\]. Each attribute provides irreplaceably constructive guidance for mimicking real-world social interaction with high fidelity. 

**Dynamics: **As shown in Figure 2, every road user continuously adjusts their actions based on social perception of neighbors’ current and future reactions and then conveys their state in a recognizable manner. The mutual dependence during interactions forms a continuous closed-loop feedback system, where each road user contributes to and is affected by the aggregated dynamics of the traffic system. Furthermore, each road user could be treated as a closed-loop feedback optimizer, where each alternative action would facilitate a corresponding update in the motion state, resulting in a specific reward or cost that further guides strategy selection. The review\[11\] argues that comprehending the principles and mechanisms of the dynamic interaction among human drivers in complex traffic scenarios would allow \(1\) generating various social driving behaviors that leverage beliefs and expectations about others’ actions or reactions\[17\]; \(2\) predicting the future states of the aggregated system involving moving obstacles is essential to enhance safety by detecting potential collisions\[18\]; and \(3\) devising realistic driving simulators and virtual testing platforms\[19,20\]. In conclusion, understanding and modeling dynamic social interactions in mixed-traffic environments are pivotal for predicting scene dynamics and ensuring safe AV behavior decisions\[21\]. Moreover, it is widely acknowledged that model-based methods outperform implicit modeling approaches, such as learning-based algorithms, in terms of interpretability. Consequently, the main challenge in human-like decision algorithms is how to explicitly

Chen *et al*. *Complex Eng Syst * 2024;4:25

**I**

http://dx.doi.org/10.20517/ces.2024.69

Page 5 of 27

model the dynamic interaction between multi-vehicles while fully considering the evolution of dynamics over a temporal horizon. 

**Measurement: **Interaction uncertainty is a critical factor influencing the safety and human-like performance of autonomous driving. Motivated by internal social driving characteristics, road users may respond with various reactions and actions through both explicit and implicit communication. Due to the bidirectional nature of information exchange, the road user not only acts as a deliver, but also as a receiver, which requires the information to be recognizable and measurable. Quantitative evaluation of social driving characteristics helps mitigate the impact of interaction uncertainty and address the “incompleteness” of game information. 

**Decision**: Based on dynamics and measurements, road users are regarded as rational agents who make decisions by maximizing/minimizing their utility/cost. What needs to be considered is how to incorporate information such as physical interactions, social interactions and driving characteristics into computational models while ensuring their fidelity. Additionally, the decision-making algorithms should maintain manageable computational complexity when applied to multi-vehicle interaction problems. 

**2.2 Summary**

In conclusion, a unified definition of social interaction in road traffic has been presented by Wang\[11\], which provides a computational framework that connects the fields of psychology and robotics. In terms of communication among human drivers, implicit signals such as vehicle kinematics are widely accepted, pervasive, common, and reliable communication methods; their critical roles cannot be ignored\[22\]. Although researchers have made initial attempts to influence HDVs by manipulating implicit signals, such as vehicle deceleration rate and a lateral move\[23, 24\], these efforts are insufficient to ensure safe and efficient communication. These communication methods lack relevant theoretical support to demonstrate the accurate and effective delivery of communication information. 

**3. OVERVIEW OF PIVOTAL FACTORS IN GAME THEORETIC DECISION-MAKING AND CONTROL**

**ALGORITHMS**

The realm of AV decision-making strategies based on game theory has witnessed extensive exploration, ranging from the discrete decision procedure modeling methods during the interaction only by game theory to the integrated decision-making and control strategies by combining other control theories and learning methods. 

We collect the latest research progress and systematically summarize the key factors affecting the human-like performance of the game theoretic decision-making system of AVs in Table 1. The factors are divided into three broad categories: interaction-related, game theory-related and control-related. 

In reality, human drivers mostly react to the physical environment without interacting with the other road users in most driving cases. Generally speaking, the interactions occur in scenes without explicit traffic lights for guiding, such as unprotected left turns, ramp merging, passing through roundabouts, and lane changing \(LC\) in a multilane highway or urban environment. Road users need to negotiate among themselves to determine the right-of-way, which is a challenge for AVs due to the partially observable environmental states. Also, there are various uncertainties in the interactive environment that can exert influences on driving behaviors, including multifarious road types, unpredictable speed and direction of HDVs, unknown intentions and dispositions of the interactive agents and uncertain perception\[19\]. The interactive environments with uncertainty could be called stochastic environments. 

Among all kinds of uncertainties, the social driving characteristics of other agents directly influence the cooperativeness of HDVs. The ref. \[25\] pointed out that individual social driving features could be sorted into long-term style features and short-term interactive characteristics. Personal traits and behavioral styles are pre-

Page 6 of 27

Chen *et al*. *Complex Eng Syst * 2024;4:25

**I**

http://dx.doi.org/10.20517/ces.2024.69

**Table 1. Pivotal factors in game theoretic decision-making and control algorithms** **Interaction-related factors**

**Algorithm function**

**Interactive scene**

**Uncertainty**

**Environment**

**Social driving feature**

Model discrete decision

Left turn in uncontrolled intersection

Road types

Intention

Determined

Process during interaction

Merging on highway on-ramps

Speed and direction

Driving style

Mimic entire decision and

LC in highway or urban environment

Intention

Stochastic

control of interaction

Passing through roundabout

Perception

Sociality

**Game theory-related factors**

**Control-related**

**Interaction**

**Role assignment**

**Reward**

**Incomplete information**

**Adaptation**

**Factors**

Two-agent

One-step

Irrational agent

One-step

Rational follower

Asynchronous

Multi-agent

Cumulative

Social driving feature

Receding-

One-shot

Rule-based formulation

Reward of HDVs

Horizon

Mutual-dependence actor

Synchronous

Multi-move

Demonstration learning

Partially available states

Uncertainty

dominant in the former’s formation while the latter is influenced by the interactive environment and driving behaviors of other agents. The long-term style of drivers can be characterized by driving style on a behavioral level\[26–28\] or captured by social value orientation \(SVO\) from the view of sociality\[17, 29\]. As for the short-term interactive features, certain characteristic variables \(e.g., reference acceleration\[30\], impact intensity related to acceleration, and kinematic indicators related to acceleration and speed\) are usually presented to reflect the real-time traits of other agents\[31\]. Evaluating the social driving characteristics of other agents quantitatively helps AVs augment the interaction understanding abilities and enhance the social decision-making prowess of AVs\[32\]. 

Through a comprehensive literature analysis, the development process of game theoretic decision-making methods is illustrated in Figure 3. The horizontal axis represents the randomness of the interactive environment while the vertical one indicates the number of interactive agents. The evolution of game theoretic models is fundamentally driven by control theory and learning methods, based on which the development process is roughly divided into three stages as represented by the differently colored areas in Figure 3. In the first stage, researchers focus on high-fidelity decision-making modeling by exploring various types of game theory and integrating social driving characteristics into computational models. Usually, the following assumptions are made: for example, the interactive environment is treated as deterministic; \(2\) the interaction takes place only once; \(3\) the game played by AVs and HDVs has complete information. As research progresses, more realistic factors are considered. To address the computational complexity problem arising from the multi-agent coupling relationships, real-time methods for solving combinatorial optimization problems have also been investigated. Considering the dynamics of social interaction and time-varying control, a multi-move dynamic game scheme is presented by combining control theories to enable AVs to make decisions based on predictions of SVs’ motion. Furthermore, to handle the incomplete information induced by uncertain driving intentions, social driving characteristics are quantitatively assessed based on the observed trajectories. Driven by the rise of artificial intelligence, learning methods are incorporated into the game theoretic scheme, equipping AVs with the ability to learn from interactions and further enhancing the adaptability of the autonomous decision-making system. 

**4. GAME THEORY-BASED DECISION-MAKING STRATEGY IN DETERMINISTIC ENVIRONMENT**

In mixed-autonomy traffic, if AVs are driving in certain scenarios such as in a vehicle platoon or in a closed environment, a deterministic environment is usually assumed. Also, the common scenarios in reality, namely highways or urban streets, become deterministic under the assumption that the stochasticity of human driving behavior is ignored and all states of HDVs are fully observable. Therefore, without considering randomness and uncertainty, early research primarily focuses on constructing game theoretic decision-making frameworks, 

Real-time solution to the equilibrium

Chen *et al*. *Complex Eng Syst * 2024;4:25

**I**

http://dx.doi.org/10.20517/ces.2024.69

Page 7 of 27

a multiple concurrent leader-follower pairs game; 

a communication-enabled conflict resolution

1 AV\+ n HDVs

**Real-time solving method**

**Dynamic interaction modeling**

**Uncertainty modeling**

Computational complexity

Time-varying 

Dynamics

Measurement

Uncertainty

control

a sequence of 

a combinatorial 

Multi-agent

one-shot games

optimization problem

incomplete 

multi-

dynamic 

dynamic 

stochastic

move 

game 

social

determined

**High-fidelity decision model**

game 

dynamic 

scheme 

driving 

a bilevel optimization 

scheme 

sequence game

game with 

with 

character

Role 

problem

with 

cumulative 

control 

estimation

assignment

reinforcem

a coupling 

utility

theory

simultaneous game

ent learning

optimization problem

Sociality 

1 AV\+1 HDV

modeling

**Figure 3. **Development process of game theoretic decision-making and control methods driven by influencing factors. 

Learning to 

interact with other 

drivers

particularly the selection of game-theory types based on a different understanding of interactive agents’ impact and the design of utility functions that account for human driving behavior. Additionally, under a deterministic environment, vehicle states are updated according to a deterministic kinematic state-space model, which is in charge of calculating the change of positions, velocities, and accelerations. Considering the complexity of the vehicle dynamics model, the point-mass \(which treats a car as a particle\) and bicycle or front wheel steering how to leverage social driving 

characteristics into computational 

\(which treats a car as a 2D\) models are commonly used\[33\]. 

The complexity in parameter 

models and ensure their 

**Simultaneous game**

non-zero-sum game

selection for game models, which 

Nash game

struggle to adapt to the diverse 

Essentially, the driving behavior decision of human drivers is a game theoretical problem where drivers make mixed-motive game

range of interaction partners and 

real-time decisions by considering the effects of mutual interaction\[34\]. Game theory has been a mature field scenarios due to reliance on 

manually set parameters. 

for modeling strategic interactions of rational players and can offer versatile and adaptive solutions for interactive decision problems in various scenarios without relying on specific data distributions\[21, 35\]. The game theoretic decision-making methods establish the mapping relationship from the driving environment to driving behavior. Human driving behaviors or actions are theoretically the optimal or approximate optimal solution that maximizes certain rewards/utility related to the driving environment\[36\]. Toward this point, researchers formulate the social interactions as optimization problems by integrating the vehicle states-related information into the reward/cost function, where the game equilibrium is exactly the optimal outcome\[37\]. 

**4.1 One-shot games in determined environment**

The most commonly encountered interactive scenarios in our daily traffic are car-following, merge-in/out, and lane change in urban environments and highways, which is assumed as determined in the early studies. Without considering interaction uncertainty, researchers focus on modeling the decision-making process during the one-stage interaction by one-shot games. Without loss of generality, the one-stage interaction could be regarded as one turn of the dynamic interaction. Studying the behavioral decision during one-stage interaction helps to facilitate a deeper exploration of the dynamic interaction process imitation. Additionally, either simultaneous one-shot games or multi-move games could be viewed as a combination of one-shot games. Therefore, the typical one-shot game-based methods \(e.g., Stackelberg game and simultaneous game\) are discussed here-inafter, followed by the approaches of game reward/utility function construction. 

For the case that an AV interacts with only one HDV in a determined environment, game theoretic models are developed based on a one-shot game to delineate the strategic actions of both vehicles at a single step. For instance, driver behavior of merging\[38, 39\], LC\[23, 40–47\] and unprotected left-turning\[48\] is modeled as either a two-person non-zero-sum non-cooperative game\[49,50\], a normal-form game\[28\], a Stackelberg game\[23,26, 38,39, 43–47\] or a simultaneous game\[27,32, 40\] depending on the role assignment of the other agent and game equilibrium. The outcome of simultaneous games can be a pure or mixed-strategy Nash equilibrium, derived from the utility function maximization/minimization. The optimization problem built based on one-shot

Page 8 of 27

Chen *et al*. *Complex Eng Syst * 2024;4:25

**I**

http://dx.doi.org/10.20517/ces.2024.69

games with two agents could be solved using the off-the-shelf dynamic and linear programming algorithms. If the mixed-traffic environment is assumed to be deterministic and multiple vehicles interact with each other in a game theoretic framework, a simultaneous one-shot game or a differential game would be modeled between one AV and multiple HDVs. 

In games, how the ego AV accounts for the influence of interactive HDVs would impact the decision-making capability of game theoretic models. The role of other agents could be categorized as moving obstacles, rational followers, or mutual-influence actors, each of which follows a progressive logic. The interaction with moving obstacles is one-way, where obstacles are deemed to be unaffected by AVs. In the ref. \[39\], vehicles on the main road were assumed to move along the current lane at a constant speed. The trajectories of interactive vehicles predicted on this assumption were fed into the planning level. This simplification works in a one-shot game due to longer reaction time of HDVs. However, human driver heterogeneous characteristics may give rise to conservative action of AVs or even risky situations in reality. To avoid this, the roles of rational followers and further mutual-dependency actors are assigned to HDVs, facilitating Stackelberg game theoretic methods and simultaneous game theoretic methods, respectively, as detailed below. 

*4.1.1 Stackelberg game theoretic decision-making*

In Stackelberg games, HDVs are regarded as rational followers who would respond rather than influence the leader AV. The leader-follower relationship entails a bi-level optimization where a lower-level optimization is contained in an optimization for the leader’s objective on the higher level. Yoo and Langari\[38,39\] presented an interaction model between vehicles during LC and lane merging based on a Stackelberg game, where the ego AV was assumed to know the cost function of the competing vehicle beforehand. Based on the same assumption, Hang\[26\] modeled the lane-change decision-making procedure using a Stackelberg game, considering two-agent interaction. The upper layer was to optimize the follower’s behavior decision grounded on predictions about the follower’s strategy while the lower layer optimized the decision-making process of the follower given the leader’s choice. 

To address the challenge in modeling a large amount of HDVs simultaneously, Liu and Tomizuka\[51, 52\] combined multiple HDVs as one effective agent and assumed a sequential game in which HDVs led and the AV

played reactive strategies. By mapping a baseline control law to a set of safe controls, an online algorithm was developed for the AV controller to incorporate human intentions as safety constraints. Coskun and Zhang\[41,43, 46\] exploited a sequence of one-shot Stackelberg games to deal with multi-vehicle interaction in the HDV-dominated mixed-traffic environment. The goal was to train autonomous driving with human-like performance in gap acceptance and lane change. We noticed that the ego AV was regarded as the leader in the above works while the leader-follower role was determined based on the right-of-way in\[19\]. There is no doubt that the role allocation of leader and follower deserves more discussion due to its importance in applications. 

One effective method is to directly assign the leader role to the ego AV\[23, 26,39,46, 47\], which is valid because the AV deserves to be endowed with the advantage of active pursuit as the initiator of the LC interaction. Also for the LC scenarios, the pairwise leader-follower relationships were dealt with as a priori uncertain and modeled as latent variables, which were estimated online predicated on observed trajectories\[53\]. Another alternative logic to determine the sequence order is based on traffic rules. For instance, Li *et al*. applied the “right-of-way” 

rules to artificially formulate role assignment rules at uncontrolled intersections\[19\]. So far, a unified method for leader-follower role allocation has not been proposed for various interactive scenarios. Besides, a rational follower could only derive the best response to the leader passively instead of actively exerting influence on it\[54, 55\], which might cause an inevitable shortcoming that dynamic mutual influences between the AVs and HDVs are neglected. 

Chen *et al*. *Complex Eng Syst * 2024;4:25

**I**

http://dx.doi.org/10.20517/ces.2024.69

Page 9 of 27

*4.1.2 Simultaneous game theoretic decision-making*

To consider the coupling influence among agents, simultaneous games are used to capture their dependence\[27,32, 40\], where every agent makes decisions simultaneously without knowing the others. Usually, a two-agent interaction problem is modeled as a coupling optimization problem\[27\]. Hang\[27\] adopted Nash game to handle the non-cooperative decision-making problem in common LC scenarios by combining with the potential field method to provide a collision-free reference path. Under the scheme of a simultaneous game, Nash equilibrium was derived for the pure strategy by solving the optimization problem. A deterministic strategy provides a complete plan of how a player will take action in a game. However, a deterministic strategy is not always feasible, consequently necessitating a probabilistic analysis of all the likely responses. If each player selects the optimal strategy probability distribution given the fixed strategies of others, a mixed-strategy Nash equilibrium would be computed as the game outcome\[32,40\]. Meanwhile, multi-vehicle decision-making is formulated as a combinatorial optimization problem in the distributed or centralized form\[56\]. Under the distributed frame, only the closest *𝑛 * SVs in the neighborhood are considered. In the centralized formulation, the objective function is a weighted sum of the cost functions for every participant\[11\]. Directly solving the optimization problem might lead to a trapped situation where all vehicles decide to slow down to yield. To solve this problem, Liu *et* *al*. proposed a communication-enabled conflict resolution\[57\]. 

**4.2 Utility function construction**

The game theoretic models for interaction problems formulate various optimization problems, which require specified objective functions \(also known as utility/reward/payoff\) to be optimized. The utility value represents the outcome obtained by selecting a particular action. To guarantee the complete information of the game, the assumption that the ego AV has access to others’ utility functions has been made\[17,23, 53, 58–60\]. Generally, utility functions of AVs and HDVs are contrivedly designed to realize human-like driving performance according to the prior domain knowledge of traffic regulation and driving tasks\[26,27, 61–63\]. However, the interaction among human drivers in natural traffic environments suffers not only physical \(e.g., kinematics and geometry\) but also social \(e.g., driving style, intention, and social preference\) constraints. For example, driving safety can always be guaranteed by a safe gap ideally. Nevertheless, it is difficult for the ego AV to perfectly predict the actions of the interactive vehicles due to their uncertain driving intentions. As traffic psychologists held that the social interaction of human drivers was characterized by the orientation of social habits and values, social preferences and social interaction patterns\[64,65\], which could be collectively called social driving characteristics\[11\]. These representation parameters could be parameterized and then embedded into the cost functions of interactive agents involved in a game, which would help improve the adaptation of AV’s decision. Herein, how social driving characteristics are considered in utility function design is primarily introduced, and how to quantify them would be discussed later. The mainstream individual utility functions can be summed up as three categories, as shown in Figure 4. 

In LC environments, Hang\[26, 27\] formulated the cost function of LC behavior as a linear weighted sum of tri-partite costs on driving safety, ride comfort and travel efficiency. The cost of driving safety was calculated by a function of gap and relative velocity, while the ride comfort and travel efficiency were evaluated by the jerk-related expression and relative velocity, respectively. The HDV was supposed to be an optimizer with the same formulation principle for cost function as an AV, based on which the integrated decision-making and motion planning framework was established as a two-level multi-objective optimization problem through Stackelberg game and model predictive controller \(MPC\). Similarly, a multi-factor-enabled interactive decision-making method was presented to align decision-making with human logic while ensuring driving safety\[66\]. The multiple complementary factors included driving performance requirements - such as safety, smoothness, comfort, speed and available space - as well as diverse driving styles suitable for different driver groups. The driver’s driving style was incorporated into the goal function by assigning different weights, although it was assumed as a priori and fixed variable. In contrast, the aggressive level was deemed to follow the Gaussian distribution and there was a one-to-one mapping between the driver’s aggressiveness and weight\[23, 67\]. Through the cumu-





Page 10 of 27

Chen *et al*. *Complex Eng Syst * 2024;4:25

**I**

http://dx.doi.org/10.20517/ces.2024.69

One-

Rule-

Demonstration 

Driving 

Social 

Cumulative

step

based 

learning

style

preference

\[39,69,20,19,26,27,66\]

\[58,53,67,23\]

\[17,70\]

Literature：

*R *\(

0

1

*s *, *u *, *u*

= *w r*

*g ***x u u**

 =



*i *\(

, 

, 

, 

*i*

 *i*

*i *\)

1

*t*

*t*

*t *\)

*T*

, 

−

*r*

*m * 1

*U *=    \( *r*

*S *\) −  \( *r*

*J*

*i*

*i*

*i *\)

*r *= 

*T*

*r *, *r *, *r *, *r *, *r*

, 

, 



 cos\( *r ***x u u **\+  *r ***x u u **

*i *\) *i*



\( , , *i j *\) sin\( *i*\) *j *\( , , *j i*\) , 

1

2

3

4

5 

5

Utility：

\+





− \( *r*

*j* *i*

*T *\) \+  \( *r*

*D*

*i*

*i *\) . 

−

*N * 1

−

**R**

 

=  

*G ***x u ** =  *g ***x u ** \+ *g ***x **

*i *\(

0 , , \)

*i *\(

*k *, *k *, *i *\)

*N*

*i*

\( *N*, *i*\)

 \(

*N*



*s *, 

, 

*R*

*s*

*u*

*u*

. 

*t*

*l t*

*f t *\)

1

, 

, 

. 

, 

, 

 \( *t *

\+

*l *, *t *

\+

*f *, *t *

\+ \)

 =0

*k *=0

**Figure 4. **Mainstream utility functions classification. 

lative distribution function of aggressiveness, the safety and space payoffs were linearly combined as the total optimization objective\[23\]. 

Due to the uniqueness of each driving task, additional considerations were represented in utility functions. As for merging scenarios, Langari\[39,41\] considered the limitations of on-ramps’ length and driver’s visibility in addition to the factors of speed advantage and unacceptable collision risk. Also, different drivers with varying levels of sensibility were distinguished by introducing a parameter called “aggressiveness” into the utility functions. With the utilities that originated from drivers’ intentions, a driver merging model was established that can judge the merging instant and acceleration/deceleration according to the driver’s aggressiveness\[39\]. In unsignalized intersections \(e.g., four-way and roundabout\), traffic rules were introduced to motivate vehicles to drive into the right lane\[19,20, 68, 69\]. Driving styles were reflected by choosing distinct weighting coefficients. 

Liu *et al*. formulated the reward function accounting for safety and the adherence to or violation of “soft” 

traffic rules\[28\]. 

Similarly, payoffs developed in\[28\] consisted of safety utility and traffic rule-related rewards. But differently, the parameters used to adjust the ego AV’s behaviors were designed to rely on the driving style of the counterpart based on supervised learning mechanisms. Furthermore, the multi-vehicle interaction was modeled based on a normal-form game, facilitating a clear representation of players’ strategy space and payoff. Coincidentally, SVO can be learned from observed trajectories using inverse RL \(IRL\)\[17,70\]. As an effective tool to quantify the social preferences of human drivers, SVO can assess how one driver weights its rewards against the rewards of other agents\[71\]. Many researchers have adopted the SVO concept to conduct extensive investigations about human-like decision-making of autonomous driving\[17, 72–74\]. By introducing human-like elements into utility functions, mainly indicated by intention, driving style and social preference, AVs are promised to generate socially-compatible driving behaviors. 

**4.3 Summary**

Naturally, game theory has exhibited great superiority in modeling the interdependence of actions and some exact real-time solutions exist for a limited number of problems. Research on game theoretic decision-making in a deterministic environment emphasizes the construction of decision schemes with game theory. This mainly involves game type selection considering the role of HDVs during the interaction process, as well as the number of interactive agents and the design of individual and total utility functions. Concretely, depending on whether HDVs are followers or mutual influencing agents, either a sequential or simultaneous game is employed to model the interaction. Besides, a deterministic kinematic state-space model is specified to update states, based on which the utility function is constructed focusing more on individual driving performance than traffic performance. The effectiveness of the proposed methods in a deterministic environment has been verified in simulations and hardware-in-loop experiments. However, game theoretic approaches in a deterministic environment suffer from the following issues: \(1\) it is assumed that the AV can access the utility

Chen *et al*. *Complex Eng Syst * 2024;4:25

**I**

http://dx.doi.org/10.20517/ces.2024.69

Page 11 of 27

function that justifies other agents’ actions and that the players act rationally according to those contrived goal functions. Nevertheless, the assumption is too ideal to come true in realistic traffic; \(2\) the numerical computation complexity expands exponentially in the number of players and with the growing temporal horizon; and \(3\) the HDVs’ behavior might be stochastic which makes the computations of solving for mixed or behavioral strategies even more intractable. Consequently, to alleviate those issues, many papers in the field of game theoretic autonomous driving try to simulate the dynamic interaction and handle the stochasticity of human behavior in the development of decision-making algorithms. 

**5. HUMAN-LIKE DECISION-MAKING CONSIDERING DYNAMIC INTERACTION MODELING**

Human drivers handle interactions not only considering immediate benefits related to driving performance such as safety and comfort efficiency but also involving reasoning about future states. Moreover, Lee *et al*. 

argued that the interaction among human drivers should gain an optimal accumulated utility over a short future horizon\[75\]. As exhibited in Figure 2, the dynamics of interaction can be summed up in two aspects: \(1\) the multi-turn closed-loop feature; and \(2\) dynamic evolution of each agent’s state over time. The evolution and update of system states lead to the accumulation of each-step utility over the future horizon\[19, 53, 68, 69\]. However, the abovementioned one-shot games cannot model drivers’ dynamic driving actions; by contrast, multi-move games considering the mutual dependence among interactive agents have exhibited great potential in dynamic interaction modeling. Thus, most of the current works switch on multi-move games with cumulative utility by translating interactive behavior into an iterative optimization problem\[17, 43, 53\]. Considering the dynamic and uncertainty of the interaction process, as well as the potential reasoning of human drivers about future risks and situation evolution, Liu\[32\] first modeled the future state extrapolation of environmental risks and incorporated efficiency, safety, and stochastic disturbance benefits into the payoff function. If the game involves multiple decisions where the order is important, it is dynamic. Furthermore, it becomes non-cooperative if each player pursues their own utility partly conflicting with the utilities of others. 

Another method capable of capturing dynamic mutual dependence is the hierarchical game theoretic planning where the AV’s planning and its predictions of HDVs’ behaviors are decoupled\[76\]. The higher strategic planner level was featured by a long-horizon feedback Stackelberg game with simplified dynamics and full information structure. By successive application of dynamic programming, driving actions of interactive agents were recursively solved. The optimal *𝑄*-value was utilized to inform the tactical planner, who applied a short-horizon “tactical” game with full dynamics and a simplified information structure. The trajectory of the AV

was output by iteratively solving a nested optimization problem, i.e., estimating the human’s best trajectory response to each candidate plan in the short-term planning horizon. 

**5.1 Human likeness evaluation metrics**

The review\[2\] suggested that human-like decision-making could empower automated systems to make correct judgments and decisions in complex traffic scenes. Achieving human-like performance requires algorithms to manage diverse uncertain factors in dynamic traffic environments, meet the demands of passengers and other road users, and guarantee efficiency and safety. Therefore, the human similarity of decision-making algorithms can be assessed from two perspectives: the algorithm’s principles and its driving performance. In terms of the former, the human likeness evaluation methods include \(1\) a combination of deterministic and fuzzy logic; \(2\) capability to unknown scenes; \(3\) consideration of randomness; \(4\) learning ability; and \(5\) interpretability. 

Driving performance metrics, i.e., driving comfort, driving safety, similarity with human demonstration trajectories, and characteristics relative to other traffic participants, are used to directly compare human driving data with intelligent decision-making algorithms, demonstrating their similarity. 

Page 12 of 27

Chen *et al*. *Complex Eng Syst * 2024;4:25

**I**

http://dx.doi.org/10.20517/ces.2024.69

**Table 2. Typical human-like decision methods combining dynamic game and control** **Ref. **

**Scenes**

**Game theory**

**Control**

**Contributions**

Mandatory

Stackelberg

Development of game theoretic model predictive

\[43,47\]

MPC

Merging

Game

Controller with online aggressiveness estimation

Lane change

Stackelberg

MPC with

Integration of decision and motion

\[26,27\]

In highways

Game

Potential filed

Planning considering social behaviors

Uncontrolled

Differential

Enable real-time decision in

\[79\]

LQ

Intersections

Game

Continuous action spaces

Uncontrolled

Leader-follower

Application to various interactions

\[19\]

RHC

Intersections

Game

With up to 10 vehicles

Diverse multi-

Potential

Computationally scalable and actual NE

\[77, 83\]

RHC

Agent scenarios

Game

Approximation despite unknown others’ cost

**5.2 Human-like decision-making methods considering time-varying controls**

In general, the game theoretic models could accomplish an expected performance in similar scenarios with elaborative parameter tuning, yet have low generalization capability in the unseen traffic scenarios. Therefore, model predictive control \(MPC\)\[26, 27, 42,53\], receding horizon control \(RHC\)\[19, 20,77,78\] and linear quadratic \(LQ\)\[79–81\] techniques have been introduced to solve time-varying control problems. The main research and their contributions are summarized in Table 2. 

Real traffic environments are characterized by highly dynamic variations, meaning that actions computed at the current time step may become obsolete by the next time step. In order to avoid this issue, the idea of RHC\[42\], widely implemented in MPC theory, was borrowed into game theoretic decision-making methods. 

Coskun *et al*.\[41\] developed a dynamic decision strategy combining Markov games with a receding horizon approach to handle new information received as time progresses. The human-in-the-loop \(HIL\) experiment results demonstrated that the proposed receding horizon Markov game could determine a safe gap in multi-move traffic. Moreover, Li *et al*. \[19, 20, 53, 58, 82\] have carried out much research focused on interaction problems in various unsignalized intersections by combining game theory with receding horizon optimal control. In these works, the rewards were an accumulation of the one-step reward constructed in\[61,62,68, 69\]. Particularly, Tian *et al*. \[20\] presented a general interaction modeling method with level-k game and receding-horizon optimization, which could be scalable in urban environments with many intersections and vehicles. To resolve the computation challenges posed by large state space of urban traffic, an imitation learning \(IL\) algorithm was used to obtain control policies. 

In the integrated framework of decision-making and motion planning\[26\], MPC was used to predict the state over the future horizon. Based on the idea of optimization, the decision-making and motion planning problem was transformed into a closed-loop iterative optimization process with multiple constraints by combining Stackelberg game theory, potential field method and MPC. Since only current states were considered in the game theoretic decision process, the multi-constraint interactive optimization could be iteratively solved with an evolutionary algorithm in real time. To handle constraints in different lanes during instantaneous LC, hybrid MPC was introduced into the development of behavioral decision methods\[43,46, 47\]. The higher-level controller evaluated the proper times to initiate/complete a lane-change maneuver by continuously playing a Stackelberg game with surrounding HDVs. The four-stage hybrid MPC in the lower controller was responsible for prediction and update of HDV’s longitudinal position and lane decision. The pure equilibrium was readily obtained by a sweeping search of all the solution candidates because of the small scale of the game. 

**5.3 Real-time solution for multi-vehicle dynamic interactive decision making**

The game theoretic framework has been proven to provide an explainable explicit solution to model the dynamic interactions among human drivers. However, if the AV could predict the actions of HDVs in the entire planning horizon, it would optimize its own objective function based on both current and future strategies to bring about a continuous sequence of control strategies to implement. The same process holds for HDVs. 

Due to dynamic coupling, it remains a challenge to satisfy the real-time constraint regarding computational

Chen *et al*. *Complex Eng Syst * 2024;4:25

**I**

http://dx.doi.org/10.20517/ces.2024.69

Page 13 of 27

**Global Sorting**

\( \* \*

**Π **, **T**

**Π T**

, 

**seq **\) = arg min *J *\(

, **seq **\)

**Π**, s

**T **eq 

Ego II

*J *\(

*n*

**Π**, **T**

, 

**seq **\) = *w t*

\+ *w * *t*

− *t*

1  , seq 

2



*n*

\( , seq 

*i*

*i *\)2

Front 

rear 

IV

I

III

*i * 1

=

s.t. *t*

− *t*

 *t *, *t*

 *t*

. 

*i * 1

\+ , *seq*

*i*, *seq*

*safe*

 , *seq*

*i*,min

*i*

assigned 

to vehicle control

*R *=  *r *\+  *r *\+  *r *\+  *r *\+  *r *，

sequences & 

*i*

1 *o*

2 *e*

3 *c*

4 *r*

5 *f*

arrival time

\*

2

2

*r *= −\( *t*

− *t*

\) , *r *= *t*

−

, *r *= −\( *t*

− *t *\) , 

\*

*o*

*i*, *tar*



*e*

*i*, *tar*

*c*

*i*, 

, 

*tar*

*i*

*i seq*

2

2

= −



−

−



Speed Planner

*r*

*t*

*exp*\( \( *t*

*t*

\) / *t*

\) *t*

. 

*r */ *f*

*safe*

*i*, *tar*

*r */ *f *, *tar*

*safe*

*r */ *f *, *tar*

reward

target time

0

*c*

0

*c*

0

*c*

*t*

= *t *\+  *t *, 

*i*

*i*

*i*

*RIV*

*c*

*R*

*IV*

0

*c*, *i*

*III*

 *t *=  *f *\( *ct*

*i*

*dstb*

*NVc *\) , 

*c C*

 /

*R*

*i*

0

*c*

*R*

*II*

*c*, *i*

*I*

*f*

\( *c*

*c*

*c*

**t**

=

*t*

− *t*

*dstb*

*N c*

*V *\)

max \(

, 0 . 

*i*, *inter*

*i*, *free*

\)

Nash 

**Local Gaming of EV**

**Final Decision & Safety Check**

solution

**Figure 5. **The decision framework of global sorting and local gaming \(GLOSO-LOGA\) \[86\]. 

tractability although progress has been made with simplified system dynamics and information structures\[76\]. 

With such restrictions, most of the current game theoretic interactive decision-making and control methods have difficulty in algorithm scalability, thus being trapped in two-vehicle settings and simulation tests or handling multi-agent interaction pairwisely\[17, 43, 55, 70, 84, 85\]. For instance, dynamic games with concurrent pairwise leaders/followers were adopted to capture dynamic interaction among multiple agents at uncontrolled intersections\[19\]. Each pair of lead-follower games formed a bi-level optimization problem, which could be computed in real time by \(1\) reformulating it as a local single-level optimization problem\[17, 86\]; \(2\) approximating an optimal solution of the follower\[54, 87\]; and \(3\) setting assumptions on the uniqueness of each optimizer that maximizes rewards\[19\]. Simulation results indicated that the interactive model demonstrated reasonable behavior and manageable computational complexity. As displayed in Figure 5, Li *et al*. proposed a global sorting-local gaming framework to solve the complex multi-vehicle interactions with comprehensive consideration of the advantages of multi-vehicle collaboration and single-vehicle intelligence approaches\[86\]. Moreover, an interaction disturbance function is used to quantify the impact of indirect interactions on ego vehicles. 

Additionally, Schwarting *et al*. developed a game theoretic control policy for AVs by solving a locally equiva-lent formulation\[17\]. The two-agent Stackelberg game created a constrained bi-level optimization, which was then reformulated as a local single-level optimization problem using Karush-Kuhn-Tucker \(KKT\) stationarity conditions, allowing the solving method to propagate the constraints. However, it may be desirable to have back-and-forth tacit negotiation even if two agents interact, which removes the leader-follower dynamics and entails a simultaneous game. Regarding the constrained multi-agent Nash equilibrium, Schwarting *et al*. reformulated the multi-level optimization problem with KKT condition and applied existing nonlinear optimizer to solve it, as shown in Figure 6\[17\]. 

As pointed out in the ref. \[78\], a differential game arises when two interacting agents with conflicting goals solve their own optimal control problems. The classical differential game basically concerns two agents and gets intractable for an equilibrium of more than two agents. Sadigh\[87\] predigested the original two-agent differential game to a Stackelberg game played at discretized time steps. This framework was extended to a multi-agent Stackelberg game, but with assumptions that the ego AV only affected one HDV and the actions of other HDVs were fixed\[88\]. In order to facilitate interactive decision-making in continuous action spaces, iterative LQ technique was blended with differential games to compute a discrete-time linear dynamics approximation





Page 14 of 27

Chen *et al*. *Complex Eng Syst * 2024;4:25

**I**

http://dx.doi.org/10.20517/ces.2024.69

**Stackelberg Game Formulation**

**Real-time solution**

a bilevel optimization problem

a local single-level optimization problem

\*

0

\*

\*

0

0

**2 **

**u **= arg max *G *\(**x **, **u **, **u **\(**u **\), \), 

**u **= arg max *G *\(**x **, **u **, **u **, \) \+ *G *\(**x **, **u **, **u **, \), 1

1

1

2

1

1

1

1

1

2

1

2

1

2

2

1

**u**

1

**u **, **u**2 , **k**

**agent **

*k * 1

\+

*k*

*k*



KKT

**x**

= \(**x **, **u **\), 

*k * 1

\+

**x **= \( *k*

**x **, *k*

**u **\), 

1

1

1

1





**case**

\*

*c *\( , 

**x u **, **u **\(**u **\)\)  0, 



 *c *\( , 

**x u**\)  0, *c *\( , 

**x u**\)  0, 

1

1

2

1

1

2

s.t.

s.t.

\*

0

**u **\(**u **\) = arg max *G *\(**x **, **u **, **u **, \), 

0

 *G *\(**x **, **u **, **u **, \) \+ **k ** *c *\( , 

**x u**\) = 0, 

2

1

2

1

2

2



 **u **2

1

2

2

**u**

2

**u**

2

2

2





*k * 1

\+

**x**

=

\( *k*

**x **, *k*

**u **\), *c *\( , 

**x u**\)  0. 



**k ** *c *\( , 

**x u**\) = 0, **k ** 0. 



2

2

2

2

2

2

a recursive optimization problem

iterative best response



0

**u **= arg max *G *\(**x **, **u **, 

**u **\(**u **\), \), 

1

1

1

1



1

1

**u**1



0

s.t. **u **\(**u **\) = arg max *G *\(**x **, **u **, 

**u**

\(**u **\), \), 

2

1

2

1,2

1

 ,2

1,2

2

**u**2



0

s.t. **u **\(**u **\) = arg max *G *\(**x **, **u**

, 

**u**

\(**u**

\), \), 

3

1,2

3

1,2,3

1

 ,2,3

1,2,3

3

**u**3

**Multi-**



0

s.t. **u **\(**u **\) = arg max *G *\(**x **, **u **, **u **, \). 

*m*

¬ *m*

*m*

¬ *m*

*m*

*m*

**agent **

**u** *m*

constraints

**case**

*m*





0

0

**u **\(**u **\) = arg max *G *\(**x **, 

**u **\(**u **\), **u **, \), 

**u **= arg max *G *\(**x **, **u**, \), 

*i*

*i*



*i*

− *i*

*i*

*i*

*i*

*i*

*i*

**u**, **k**

**u**

=

*i*

*i * 1

*k * 1

\+

*k*

*k*

KKT

**x **= \(**x **, **u **\), 

 *k * 1\+

**x**

= \( *k*

**x **, *k*

**u **\), *c *\( , 

**x u**\)  0



*j*



s.t.

0

*c *\( , 

**x u **, 

**u **\(**u **\)\)  0, 

s.t. *G *\(**x **, **u**, \) \+ **k ** *c *\( , 

**x u**\) = 0, 

*i*

*i*

 *i*

*i*

**u**

*j*

*j*

*j*

**u**

*j*



*j*

*j*



 *i*

  . 

*m*

**k ** *c *\( , 

**x u**\) = 0, **k ** 0, 

*j*

  . 

*m*

 *j j*

*j*

**Figure 6. **Real-time solving methods for multi-agent interactive decision-making problems \[17\]. 

and quadratic cost approximation\[79–81\]. Fridovich\[80,81\] developed an efficient iterative LQ approximation for nonlinear multi-agent general-sum differential games. Based on the feedback-loop LQ differential game, a planning and decision-making framework was built for unprotected left-turning handling\[79\]. To enhance the accuracy of the interaction model, real-world human behavior was extracted and evaluated from a naturalistic driving dataset to help construct a more realistic behavior model. 

Another special class of multi-player games, called potential games, has also been integrated with receding horizon optimization to address decision-making\[77, 83\]. Motivated by the need for real-time solutions, Liu *et* *al*. performed an in-depth investigation on finite and continuous potential game frameworks and formulated practical and reliable models with adaptation to specific traffic scenarios\[83\]. Additionally, a potential game consisting of Predictor and Corrector was investigated\[77\], where the former was responsible for heuristically predefining agents’ cost functions, and the latter handled action deviation measurement, feedback and correction. This framework successfully fulfilled the requirements of interpretability, computational scalability, applicability to distinct scenarios, and human-like intelligence. 

**5.4 Summary**

In this section, dynamic interaction modeling over the receding horizon is achieved by applying multi-move game or potential game and control methods. To ensure tractable computation, researchers have put forth several strategies to enhance game theoretic solutions. However, these solutions might be inaccurate in environments with high clutter or uncertainty. Uncertainty seeps in from unpredictable behaviors in surrounding traffic participants, as well as sensor noise and vehicle models\[21\]. In particular, the diversity and unpredictabil-

Chen *et al*. *Complex Eng Syst * 2024;4:25

**I**

http://dx.doi.org/10.20517/ces.2024.69

Page 15 of 27

ity of human driver behaviors present a major challenge for adapting decision-making algorithms\[24\]. 

**6. GAME THEORETIC DECISION-MAKING AND CONTROL METHODS WITH ADAPTATION**

To enhance human-like performance, AVs should be equipped with the capabilities to handle unseen scenarios, adapt to various human drivers, and even manage potential accidents. However, game theoretic decision-making methods that just consider the dynamics of social interaction may not address the uncertainties resulting from the actions of other drivers. Additionally, most game theoretic methods mentioned above assume a complete-information framework, where \(1\) all HDVs are rational agents; and \(2\) each agent has full knowledge of others’ information, such as states, intentions and utility/cost functions. However, this symmetric information structure is too idealistic to be realized in practice, as it overlooks the uncertainties that naturally exist in complex interactive environments. 

The uncertainties influencing human drivers’ driving behaviors mainly include \(1\) multifarious road types\[20\]; \(2\) uncertain prediction caused by noisy sensor data and directly unmeasured intention of HDVs\[89\]; \(3\) interaction uncertainties due to varied cooperation intents and dispositions of other vehicles\[58\]; \(4\) unpredictable of speed and direction of HDVs\[30\]; and \(5\) perception uncertainty\[39, 90\]. Essentially speaking, the uncertainty that has the greatest impact on social interaction ultimately stems from unknown driving/cooperation intent. 

Without prior information about intentions, incomplete games are formulated. Most works deal with incomplete information by converting them to complete ones based on estimations of driving intentions or social cooperation level of HDVs\[23\]. Another effective train of thought for uncertainty resolution is to combine game theory with other learning methods, such as RL and Markov decision process \(MDP\). In the following subsections, we will provide an in-depth discussion of methods integrating dynamic games and learning techniques, and dynamic incomplete game theoretic methods considering the estimation of social driving characteristics. 

**6.1 Game theoretic decision-making and control methods combining reinforcement learning** Thanks to the ability to handle uncertainties, RL has become a powerful tool to help AVs realize socially compatible autonomous driving. Details on the principle of RL control can be found in\[11, 91\]. Herein, we focus on the application of RL on game theoretic human-like decisions. In recent years, the application of AI technology has allowed AVs to break through the assumption that interactive agents are “rational”. Algorithms such as RL\[92\] and IL could be utilized to directly learn driving policies from driving datasets or environmental interactions. Instead of treating every individual HDV as an intelligent agent, researchers regard all these HDVs as part of the stochastic environment in the RL scheme, which produces two types of game formulations of modeling interactions, i.e., synchronous Markov/stochastic scheme and asynchronous level- *𝑘 * scheme\[11\]. We summarize a list of typical game theoretic decision-making methods combining RL in Table 3. 

*6.1.1 Integrated methods of Markov/stochastic game and RL*

Markov models can represent uncertainty in a stochastic manner\[89\]. In mixed-autonomy traffic, the driving strategy selection of an AV can be regarded as a sequence of decision-making processes in a fully or partially observable random environment. MDP makes an assumption that the state dynamics is fully observable to the ego agent\[97\]. Zhang\[47\] made an assumption that the ego vehicle had access to the full information and system state of other vehicles through vehicle-to-vehicle \(V2V\) communication. Based on this, a fuzzy Markov chain was used to predict the future motion of SVs to deal with the uncertainties in their behavior. As demonstrated in Figure 7, Li *et al*. combined MDP and matrix game with deep neural network \(DNN\) and a deep maximum entropy-IRL to model the behavior of background vehicles for simulating the game and interaction processes\[95\]. In the proposed scheme, a standard MDP with states of horizontal and vertical coordinates, velocity and acceleration was used to describe the merging decision process. The comparative results denoted that the data-driven method accurately reflected human driving behavior in real-world scenes. 

Page 16 of 27

Chen *et al*. *Complex Eng Syst * 2024;4:25

**I**

http://dx.doi.org/10.20517/ces.2024.69

**Table 3. Typical game theoretic decision-making methods combining RL**

**Interactive**

**Theories of**

**Computational**

**Ref. **

**Uncertainty**

**Verification**

**scene**

**game and RL**

**complexity**

n , 

POMDP, Bayesian

A priori uncertain

Tractable

Simulation, 

\[53\]

Merging

Inference, LFG, IL

Driving intentions

Computation

NGSIM data

10, 

Matrix game

Unknown cost

A tailored

Using real

\[93\]

LC

BMPC

Functions

Numerical solver

Traffic data

n,multimodal, 

Bayesian game

Incomplete

Proportional

HIL, 

\[24\]

Merging

Markov

Information

To n

Turing tests

2,UI, 

Markov game

Trains a

Fastest

\[94\]

Simulation

Highway

DQN, WolF-PHC

Stochastic policy

Convergence

n

MDP, matrix

The impact of indirect

Simulation

\[95\]

Merging

Game, DQN

Interactions on ego vehicles

-

NGSIM data

Complex

Markov game, 

Infer SV’s

Increase by

Simulation, 

\[96\]

Traffic

Level-k reasoning, 

Decision-making

12 *. * 8% in

Real-world

Scenarios

TSA-DQN

Ability

Efficiency

Hardware test

Note: n refers to multiple vehicles; LFG and UI indicate leader-follower game and unsignalized intersection, respectively. 

**Vehicle Decision Process Formulation**

**Reward Function **

**Identification for **

Highway on-

Game 

**Background Vehicle**

ramp data

game gain matrix

modelling

background vehicle 

Reward function 

Interaction 

action space

identification based 

data between 

MDP 

on IRL algorithm

main road and 

modelling

background vehicle 

on-ramp 

state space

DNN-based reward 

vehicles

vehicle interactive driving behavior trajectories

functions

Background vehicle 

DQN-based gaming 

simulated driving behaviors

interactive driving strategic

**Background Vehicle Driving Behavior Simulation**

**Figure 7. **Data-driven game theoretic model framework with the integration of MDP, DQN, DNN, and IRL \[95\]. 

More realistically, human drivers can only observe a partial state of the traffic around them\[51, 52,63, 98\]. For example, they can observe locations and orientations, and occasionally the velocity of other vehicles, but acceleration remains unobservable. In addition, direct identification of other agents’ driving intentions is still a challenge. As a result, the ego agent holds a belief state space over all alternative states in partially observable Markov decision process \(POMDP\). A stochastic predictive control algorithm for POMDP with time-joint chance constraints was proposed for behavior planning of AVs in dynamic and uncertain environments\[99\]. 

Hubmann\[89\] considered perception uncertainty caused by the unmeasured intentions in POMDP. In the studies\[53, 58\], the interactions between the autonomous ego vehicle and other vehicles with a priori uncertain driving intentions were modeled as a partially observable leader-follower game. Additionally, the interaction uncertainty led by varied cooperation intentions was modeled as latent variables in the POMDP framework and an online estimation was conducted based on observed trajectories. 

It has been found that POMDP is suitable for autonomous driving to make real-time decisions\[100\]. Compared with the study\[58\], a continuous state space was assumed in\[53\] where vehicle motion was predicted and planned using two much larger sets of trajectories instead of a small number of actions \(or motion primitives\) to represent vehicle behavior. A game theoretical traffic model considering human behavior was developed to provide a computationally tractable solution for a POMDP by using hierarchical reasoning and RL\[61\]. How-

Chen *et al*. *Complex Eng Syst * 2024;4:25

**I**

http://dx.doi.org/10.20517/ces.2024.69

Page 17 of 27

ever, obtaining a general solution to a specific problem is difficult with the original POMDP. Therefore, the multi-policy decision-making method has received extensive attention\[101,102\]. 

In a stochastic environment with adversarial risks, an adversarial learning game has been used to model human-robotic interaction and train robust AV controllers. Assuming that the HV was an adversary attempting to falsify the AV’s actions, Sadigh *et al*. first learned the HV’s reward underlying its actions using maximum entropy IRL and then computed sequential AV controls with nested optimization\[103\]. 

*6.1.2 Integrated methods of Level-k game and RL*

The multi-agent interaction can be captured by the level-k reasoning on the strength of its easy extensibility to multiple vehicles. Level-k game theory relies on a hierarchical cognitive structure to model human reasoning in games\[77\]. Hierarchical reasoning for multi-agent interaction modeling has been applied in a series of time-extended and interactive scenarios, ranging from three-lane highways\[61–63, 104\], unsignalized intersection networks \(e.g., the most common types of three/four/five-way, T-shaped, and roundabout\)\[19, 20\] to forced merging scenarios\[53, 58, 82\]. 

In highways, an adaptive robust level- *𝑘 * reasoning was combined with game theory to develop the decision-making strategy in order to avoid undesirable behavior induced by uncertainties, such as dynamic model mismatch and improper agent classification\[104\]. Besides, the evolving of the dynamic scenario with multiple actions was taken into account in the level- *𝑘 * game-based interaction model\[61–63\]. The underlying aggregated dynamics of the traffic system conformed to Markov characteristics. However, the studied problem was formulated as a POMDP because not all of the system states were observable to the agents. Therefore, Jaakkola RL was adopted to simulate the time-extended scenario, with the preponderance of convergence to at least a local maximum in POMDP. Based on the theoretical frame constructed in\[61,62\], the research\[63\] enhanced the fidelity of the interaction model by two improvements: \(1\) designing a more realistic action space containing harder brakes and faster accelerations; and \(2\) exploiting a more realistic traffic model with the consideration of more representative constraint violation. With the designed simulator, two AV control algorithms were tested and quantitatively evaluated for their safety and performance. 

Compared with highway scenarios, urban unsignalized intersections are more challenging since much larger state space brings difficulty in real-time policy resolution\[20, 68, 69\]. One approach to achieving real-time resolution is to make reasonable simplifications. In\[69\], the action sequence of the level-\( *𝑘*-1\) agent was assumed to be independent of that of the level- *𝑘 * ego vehicle, which eliminated the need for nested back-and-forth calculations and made the computation more manageable. Another alternative approach is IL\[105\], a method for autonomous agents to imitate expert’s behavior by learning a control policy from pre-collected expert demonstrations. For example, Tian *et al*. proposed an explicit online implementation scheme to acquire an explicit approximation of expert policy\[68\]. With the function approximation techniques, the computations required for solving the optimization problems could be moved from online to offline. However, the control policy entirely relies on the expert policy, which would generate a sampling bias, further probably inducing the propagation of error between policy and expert policy in time. To avoid this, an iterative algorithm called DAgger was developed to train the policy under its induced state distribution\[20\]. Benefiting from the DAgger algorithm, the level- *𝑘 * game theoretic formalism was successfully generalized to model the multi-vehicle dynamic interactions, and to larger urban road systems \(including four-way, roundabout, and T-shaped intersections\) with manageable online computational effort. To ensure the safe and efficient navigation of AVs in complex traffic scenarios, Zhou *et al*. proposed a game theoretic driver model based on level-k reasoning, which is characterized by mixed decision levels. Compared with the widely used intelligent driver model \(IDM\)\[33, 43, 106\], the proposed driver model could effectively capture the behaviors of diverse drivers\[96\]. Following this, a temporal-spatial attention-based deep Q-learning \(TSA-DQN\) algorithm was developed to approximate the optimal policy for interactive agents, whose outperformance in success rate, efficiency, and safety in driving





Page 18 of 27

Chen *et al*. *Complex Eng Syst * 2024;4:25

**I**

http://dx.doi.org/10.20517/ces.2024.69

Driving Scenario

**Decision-Making with TSA-DQN**

Direct Observation

Observation Buffer

Observation

Spatial Attention Module

Temporal Attention Module

Action

Prior Information:

SV:Level-0~Level- *k* Policy

*k*

Initialize with rule-based Level-0 Policy

Level - *k* Policy  \( *b *\)\( *k *= 1, 2,..., *k*

\)

max

**Game-Theoretic Modeling of Driver Model**

Environment with SVs at 

Environment with SVs at 

Environment with SVs at 

Decision Level - 0

Decision Level - 1

Decision Level–\( *k*-1\)

Observation

Train

Action

Observation

Action

Observation

Action

Train

Train

···

EV: Level - 1 Policy

EV: Level - 2 Policy

EV: Level - *k* Policy

Level - 1 Driving Policy

Level - 2 Driving Policy

Level - *k* Driving Policy

**Figure 8. **Overview of the decision-making framework based on level- *𝑘 * game theoretic driver model for autonomous driving \[96\]. 

tasks has been validated. The framework of the TSA-DQN decision-making method is shown in Figure 8. 

There is no doubt that the level- *𝑘 * reasoning framework contributes a lot to formulating a dynamically-evolving interactive decision strategy. However, this type of cognitive hierarchy theory has a strong dependence on the accuracy of the \( *𝑘*-1\)-assumption about the interactive environment’s cognitive level. To avoid poor decision performance, cognitive hierarchy framework, Bayesian inference of cognitive level and receding-horizon optimization were introduced to formulate a constrained partially observable MDP\[82\]. The Bayesian network not only utilizes the probability description of the time-space relationship between vehicles but also incorporates the uncertainty of input data into the threat assessment of vehicles. It can efficiently represent uncertain events, such as estimating the probability of a vehicle collision\[82, 107\]. 

**6.2 Dynamic games with incomplete information**

In the safety-paramount transportation system, AVs are expected to assimilate seamlessly into HDVs, which necessitates AVs to better understand HDVs’ driving intention for a human-like interactive performance. In early studies, Talebpour *et al*. have considered the concept of incomplete information as part of the game formulation process, and developed a two-person non-zero-sum non-cooperative model that could cope with the stochastic nature of LC maneuver\[50, 108\]. In the study\[23\], the incomplete information, i.e., the aggressiveness of interactive HDVs, was estimated and updated, further prompting the transformation from incomplete game to complete game. Motivated by the fact that quantifying the driving intention contributes to the reduction of interaction uncertainties, social driving characteristics estimation methods are necessary to be investigated. 

Modeling and quantifying the driving characteristics of interactive agents is critical for AVs to better discern these agents and dynamically adjust their actions based on these characteristics, thereby enhancing the social decision-making capabilities of AVs in mixed-traffic environments. A great deal of endeavor has been devoted to embedding social driving characteristics in game theory-based decision-making models as recommended in Section 4.2. However, the fly in the ointment is that driving characteristics of other agents are usually known and fixed which removes the ‘incompleteness’ of games. Therefore, the main methods for recognizing and evaluating driving characteristics are presented here. Social driving characteristics are typically captured through intention, driving style and social preference, along with their evaluation metrics, as shown in Table

4. 

Chen *et al*. *Complex Eng Syst * 2024;4:25

**I**

http://dx.doi.org/10.20517/ces.2024.69

Page 19 of 27

**Table 4. Methods for estimating social driving characteristics**

**Social driving**

**Ref. **

**Metric**

**Measure method**

**characteristics**

Driving

\[23, 43, 109\]

By online observation of real-time behavior in tentative interaction

Aggressiveness

\[79\]

A behavior model estimation based on accepted time gap

Style

\[30\]

Weightings on safety and speed

Compare actual acceleration with predicted acceleration

A posterior belief of

Leader-follower game theoretic behavioral model

\[53, 58\]

HDV’s leader or follower role

With latent variables indicating the intention uncertainties

Intention

\[110\]

Politeness

Based on observed actual acceleration of HDV

\[32\]

IO

Based on environmental factors and trajectory characteristics

\[111\]

Courteous and rude

Quantitatively analyzing the interaction process based on dataset

Sociality

Compare a candidate trajectory to the actual observed

\[71,112,113\]

SVO

Trajectory for the most likely SVO

*6.2.1 Dynamic games with driving style estimation*

With the integration of driver’s psychological thinking and behavioral mode, driving style reflects comparatively stable, long-term, and intrinsic behavioral tendencies\[2\]. Under the optimization scheme, human drivers make decisions by balancing the different utility terms over the future. Depending on the driving tasks and incentives, different drivers may concentrate more on different terms, thus exhibiting disparate interactive styles with their surroundings, such as aggressive, conservative, courtesy, and selfishness\[111\]. Aggressive driving style takes some risks to pursue the driving goal with violent or frequent acceleration and deceleration, and exhibits relatively more radical driving behavior for the right-of-way. In a conservative driving style, safety takes precedence over driving goals in this style, resulting in more conservative acceleration and deceleration. 

This style usually shows a tendency to stay in the current lane or give way to other vehicles. Moderate driving style lies somewhere in between. For this reason, the interactive styles can be formulated as the weighted outcomes of different features in generating trajectories. When human driving behavior is modeled, driver data is collected to rank objective functions from trajectories\[75\], or learn the weights of such features, using IRL\[55, 70\], bi-level optimization\[49\], simulated moments\[50\], and maximum likelihood\[114\]. 

To model mathematical interaction accurately, real-world human behavior was extracted from a naturalistic driving dataset, based on which the driving style of the human participant was estimated\[79\]. Further, a planning and decision-making framework was proposed by formulating the problem as a LQ differential game. A human-like game theoretic controller was developed to determine the optimal timing and acceleration for LC

where AVs interacted with HVs by a small lateral move to imitate human behavior\[23\]. To ensure the complete information of the game, the aggressiveness of HVs was estimated first based on their reaction. Considering the several SVs within the game scope, Stackelberg games were constantly built and solved by the proposed game-based MPC to select the interactive vehicle. The vehicle’s aggressiveness was then estimated online according to its interactive behavior, followed by the execution of LC maneuvers through MPC\[43\]. Regarding the time and effort spent on real-world driving tests, a game theoretic traffic model with reasonable fidelity was presented, incorporating interaction to test performance and calibrate parameters of various AV decision-making and control systems\[63\]. Additionally, a game theoretic traffic model with heterogeneous driving styles was designed to model interactions at unsignalized intersections for virtual testing, performance evaluation, and parameter calibration of AV automation systems\[20\]. 

*6.2.2 Dynamic games with intention estimation*

In addition to driving styles, driving behavior is also affected by the short-term interactive features usually represented by certain parameters related to acceleration or speed\[30,31, 58\]. For the lane-merging task in dense traffic, the HDVs’ intentions were inferred from their behaviors, such as speed changes of the human driver in the next lane. The predicted reaction of the interacting HDV was then introduced in the Stackelberg-based decision-making strategy to determine whether the AV should merge or not\[110\]. Due to the priori uncertain driving intentions, the interaction between vehicles was modeled as a partially observable Stackelberg game. SVs’ intentions were recognized online by observed trajectories; thus, their desired trajectories were

Page 20 of 27

Chen *et al*. *Complex Eng Syst * 2024;4:25

**I**

http://dx.doi.org/10.20517/ces.2024.69

predicted\[53\]. Under the framework of Markov, intent uncertainties were modeled as latent variables. Furthermore, a novel decision-making algorithm based on a partially observable leader-follower game was presented to model the interaction and a receding-horizon optimization-based control strategy was proposed to simultaneously achieve safety and liveness with the adaptation to online estimated other vehicles’ driving intents\[58\]. 

Nash game theoretical structure was created to predict the trajectories of human actors\[115\]. 

*6.2.3 Dynamic games with sociality estimation*

Recent studies have begun integrating social interaction concepts from human sociology into AV-HV interactions. Wang *et al*. performed a quantitative analysis of merging behavior to extract courteous and rude social interaction scenarios by virtue of the social preference of other agents\[111\]. Building on this, two instructive mechanisms for developing an interactive decision-making approach were identified: incorporating social preferences and selecting relevant variables during the decision-making process. In order to realize smooth interaction and the consequent human-expected driving decision, social compatibility was represented by social fitness and reciprocal altruism in the proposed game theory-based decision method\[90\]. As one of the social preferences, Social Value Orientation \(SVO\) reflects the preference of utility assignment between the ego agent and the other agents, which could be used to anticipate cooperative motives and negotiation strategies\[17,71–74, 112, 113\]. In\[17\], SVO was represented in angular notation and regarded as the one that best matched predicted trajectories to the actual human driver trajectories. The recognized SVO was then combined with a human-imitating control policy to improve social compliance of AVs in mixed transportation. To adeptly and dynamically measure surrounding agents’ social tendencies during interaction, a novel metric named interaction orientation \(IO\) was defined as a quantified prediction of the probability that an interaction object will exhibit certain behaviors\[32\]. IO was predicated on environmental contexts and trajectory motion characteristics observed over a time period, based on which a mixed-strategy game model combined with a dynamic optimization framework was deployed to learn from expert human driving policies and make informed, social coherent decisions. 

**6.3 Summary**

To address uncertainties and enhance the learning capabilities of AVs, MDP and level- *𝑘 * reasoning are incorporated with game theory. Although more advanced Multi-Agent Reinforcement Learning \(MARL\) algorithms have been explored, most researchers still rely on basic deep RL algorithms such as deep Q networks\[94–96\]. 

Obviously, the application of MARL to the autonomous driving domain has lagged behind the fast evolving technique, which may affect the algorithm’s performance in more complex problems involving multiple agents. 

To integrate seamlessly into human-dominated traffic, it is essential for AVs to understand HDVs’ intentions correctly and make human-like decisions. Quantifying and modeling personal social characteristics in the decision-making and control algorithms is expected to improve autonomous driving safety and passenger acceptance\[116\]. 

**7. CONCLUSION AND OUTLOOK**

This paper discusses the definition of social interaction in road traffic and reviews the game theoretic decision-making and control methods considering social interaction. Based on the above systematic analysis, the dominant implications of social interactions can be summarized as the following attributes, i.e., \(1\) dynamics; \(2\) measurability; \(3\) time-varying nature; \(4\) uncertainty; \(5\) real time considerations; and \(6\) decision-making. 

Instructed by these features, we construct the development framework for human-like game theoretic decision-making methods with adaptation in Figure 9. 

The method development begins with the social driving features estimation module, which performs online measurements of social features based on observed trajectories. The representation parameters are then trans-mitted to the planning and prediction module for further behavior prediction and motion control. Then, the





Chen *et al*. *Complex*

*R * ˆ

*H*



*Eng*

, *a*

 *R * ˆ

 *Syst*

*H*

2024;4:25

**I**

http://dx.doi.org/10.20517/ces.2024.69

Page 21 of 27

\(

*a*

*real *\)

\( , *predicted *\)

**Social driving features estimation**

**Game theoretic decision-making model**

**Real-time solution**

**Utility design with expert **

**Coupling optimization model**

a multi-agent iterative best 

response game：

**mode learning calibration**

*n*

\*



*i*

 = arg min *R *= arg min

*i*

*i*

*r*

 *r*

*A*

*A*

*A*

*r *= *f *\(, , 

**x ** , \)





*A*

*A*

*i * 1

= *n*

\*

 = arg min *R *= arg min

*i*

*i*

 *r*

*H*

*H*

*H*

reward term





*H*

*H*

*i * 1

=

*r*

, *r*

, *r*

, ... 

*safe*

*comfort*

*efficiency*

lim

lim

s.t.   

, **x ** **x**



representation parameters 

optimization reformulation 

vehicle states \(**x\)**

predicted path\(x,y\)

reasoning

with KKT constraints：

**Motion planning and prediction**

**MDP**

**Level-k**

state *S*

action *A*

*t*

*t*

Expected 

Agent 

Behavioral 

reward 

reward *Rt*

probability

calculation

*Rt * 1

\+

Environment 

collision free path \(x，y\)

*St * 1

\+

**Figure 9. **Development framework of human-like decision-making and control methods. Methods for estimating social driving features and providing real-time solutions \[17\]. *𝛼*, x, Γ, *𝜉 * and *𝛾 * denote characterization parameters for social interaction, the vehicle state matrix, strategy set for game, stochastic disturbance, and the future discount factor, respectively. 

utility function is designed based on the information of predicted vehicle states and social driving features considering safety, comfort and traveling efficiency. Usually, expert mode learning is adopted to derive driving patterns from real expert data for high fidelity. Additionally, MDP and learning methods could be combined with game theory to model interaction uncertainties and cognitive reasoning, respectively. Finally, to resolve the high computational complexity induced by multi-agent interdependence and continuous state space, a real-time calculation method is required for the complex optimization model, further guaranteeing the real-time decision. With these function modules, the automated decision-making system developed based on game theory and learning methods achieves a certain level of humanness, but has not yet reached the performance level of an experienced driver. Despite the progress made, some unresolved issues remain, and the corresponding future study directions are presented. 

**\(1\) Implicit interaction mechanism: **In dynamic traffic environments, human drivers intentionally or unin-tentionally convey signaling information to one another through their movements and spatial cues, giving rise to both explicit and implicit communication\[12, 117\]. However, current implicit communication methods lack relevant theoretical support to demonstrate the accurate and effective delivery of communication information. 

Besides, the decision-making and behavioral patterns of human drivers are influenced by the diversity of interaction situations and traffic environments. However, existing studies often focus on specific interaction scenarios. Consequently, aiming to discover insights that may facilitate the development of human-like decision algorithms, the future investigation can explore the theoretical models of implicit communication and the adequate understanding of the underlying mechanisms of human interactive behavior. 

**\(2\) Social optima-based decision and control framework: **Game theoretical models have solid psychological and behavioral foundations, and their behavioral decision-making logic is clear and interpretable. Nevertheless, algorithmic designers tend to program AVs for individual welfare, such as the ride comfort and traveling efficiency of the ego vehicle, with no incentive for improved traffic performance. These individualistic control models may induce suboptimal traffic flow or even traffic safety issues\[118\]. Thus, a socially optimal control scheme needs to be devised for city planners to guide autonomous driving technology toward social optima. 

**\(3\) Real-time cluster decision-making considering interaction: **A key advantage of game theoretic solutions for decision-making problems is the ability to address planning and prediction for agents in a given situation. 

However, as the number of agents and the time horizon grow, the computational burden increases, which necessitates a trade-off in terms of computation. To scale the decision-making methods to scenarios involving

Page 22 of 27

Chen *et al*. *Complex Eng Syst * 2024;4:25

**I**

http://dx.doi.org/10.20517/ces.2024.69

a large number of AVs, real-time solving algorithms need to be developed. 

**\(4\) Personalized and human-like decision-making: **The existing game theoretic decision model could account for a single heterogeneous factor. However, drivers are highly heterogeneous because of personal preference, randomness or aggressiveness, and driving experience. For human drivers, the heterogeneities are manifested in different capabilities and risk profiles while in varied acceleration/braking capacities and manufacturer’s choice of risk tolerance in the case of self-driving cars\[119\]. To achieve personalized requirements, an accurate and real-time estimation of SVs’ driving characteristics is needed. Besides, a robust model with comprehensive consideration of heterogeneous features needs further development for predicting a distribution of actions that is consistent with real-world observations. 

**\(5\) Self-learning and self-evolving interactive decision-making for real-world applications: **The mixed transportation, composed of AVs, HDVs, other road users and road traffic environments, is a dynamically coupled system, which exhibits dynamicity and randomness. However, most of the existing interactive models have only been validated on limited datasets or are still in the stage of laboratory validation, lacking extensive engineering practice. Hence, the game theoretic models need to be further refined and extensively verified on a large number of real datasets in the future. Additionally, as for a multi-agent system, a social learning scheme allows independent agents to learn through interactions with agents randomly selected from a pool\[94, 120\]. 

Such a scheme is vital for AVs to navigate complex traffic environments with numerous road users, which deserves more exploration. 

**DECLARATIONS**

**Authors’ contributions**

Performed references search, research and analysis, and article writing: Chen Q

Provided technical support: Zhao D, Yang M, Shi Y

Made substantial contributions to conception and design of the study: Liu C

**Availability of data and materials**

Not applicable. 

**Financial support and sponsorship**

The authors greatly appreciate the National Natural Science Foundation of China \(Grant No. 52102444\), the Open Foundation of National Key Laboratory of Multi-perch Vehicle Driving Systems \(Grant No. QDXT-WY-202407-16\), the Zhiyuan Laboratory \(Grant No. ZYL2024019\), the Major Program of University Natural Research Program of Anhui Province \(Grant No. 2022AH040278\), and the Central Guidance on Local Science and Technology Development Fund of Hebei Province \(Grant No. 226Z2204G\). 

**Conflicts of interest**

Liu C is a Junior Editorial Board Member of the journal *Complex Engineering Systems * and Guest Editor of the Special Issue of ”Generalized Dynamics Modeling and Dynamics Control of Autonomous Driving Vehicle”. He is not involved in any steps of editorial processing, notably including reviewers’ selection, manuscript handling and decision-making, while the other authors have declared that they have no conflicts of interest. 

**Ethical approval and consent to participate**

Not applicable. 

Chen *et al*. *Complex Eng Syst * 2024;4:25

**I**

http://dx.doi.org/10.20517/ces.2024.69

Page 23 of 27

**Consent for publication**

Not applicable. 

**Copyright**

© The Author\(s\) 2024. 

**REFERENCES**

1. 

NHTSA. Critical Reasons for Crashes Investigated in the National Motor Vehicle Crash Causation Survey; 2018. Available from: https:

//crashstats.nhtsa.dot.gov/Api/Public/ViewPublication/812506. 

2. 

Zhang T, Zhan J, Shi J, Xin J, Zheng N. Human-like decision-making of autonomous vehicles in dynamic traffic scenarios. *IEEE-CAA* *J Automatic * 2023;10:1905–17. DOI Pubmed

3. 

Hafner MR, Cunningham D, Caminiti L, Del Vecchio D. Cooperative collision avoidance at intersections: algorithms and experiments. 

*IEEE Trans Intell Transp Syst * 2013;14:1162–75. DOI Pubmed

4. 

Dario B. Game theory: models, numerical methods and applications. *Found Trends Syst Co * 2014;1:379–522. DOI Pubmed

5. 

Ramos M, Moura M, Lins I, Ramos F. The Use of Game Theory for Autonomous Systems Safety: An Overview. In: Castanier B, Cepin M, Bigaud D, Berenguer C, editors. ESREL 2021: Proceedings of the 31st European Safety and Reliability Conference; 2021 Sep;

Angers, Ireland. Singapore: Research Publishing; 2021. pp. 2494–501. 

6. 

Qurashi JM, Ikram MJ, Jambi K, Eassa FE, Khemakhem M. Autonomous Vehicles: Security Challenges and Game theory-based Countermeasures. In: 2023 1st International Conference on Advanced Innovations in Smart Cities \(ICAISC\); 2023 Jan 23-25; Jeddah, Saudi Arabia. USA: IEEE; 2023. pp. 1–6. 

7. 

Li Y. A review of how game theory is applied in transportation analysis. In: Proceedinds of 2022 5th International Conference on Financial Management, Education and Social Science \(FMESS 2022\); 2022 Sep 3-5; Hohhot, China. UK: Cambridge Scholars Publishing; 2022. 

pp. 321–29. 

8. 

Di X, Shi R. A survey on autonomous vehicle control in the era of mixed-autonomy: From physics-based to AI-guided driving policy learning. *Transport Res Part C: Emerg Technol * 2021;125:103008. DOI Pubmed

9. 

Ji A, Levinson D. A review of game theory models of lane changing. *Transportmetrica A * 2020;16:1628–47. DOI

10. 

Rune E. A review of game-theoretic models of road user behavior. *Accid Anal Prev * 2014;62:388–96. DOI Pubmed

11. 

Wang W, Wang L, Zhang C, Liu C, Sun L. Social interactions for autonomous driving: A review and perspectives. *Foundations and* *Trends in Robotics * 2022;10:198–376. DOI Pubmed

12. 

Kauffmann N, Winkler F, Naujoks F, Vollrath M. What Makes a Cooperative Driver?” Identifying parameters of implicit and explicit forms of communication in a lane change scenario. *Transport Res Part F: traffic psychology and behavior * 2018;58:1031–42. DOI

13. 

Markkula G, Madigan R, Nathanael D, Portouli E, Lee Y, et al. Defining interactions: a conceptual framework for understanding interactive behavior in human and automated road traffic. *Theor Iss Ergon Sci * 2020;21:728–52. DOI

14. 

Choudhury CF, Ben-Akiva ME, Toledo T, Lee G, Rao A. Modeling cooperative lane changing and forced merging behavior. In: 86th Annual Meeting of the Transportation Research Board; 2007 Jan; Washington, DC; 2007. pp. 1–23. 

15. 

Risser R. Behavior in traffic conflict situations. *Accid Anal Prev * 1985;17:179–97. DOI

16. 

Domeyer J, Dinparastdjadid A, Lee JD, Douglas G, Alsaid A, et al. Proxemics and kinesics in automated vehicle–pedestrian communication: Representing ethnographic observations. *Accid Anal Prev * 2019;2673:70–81. DOI

17. 

Schwarting W, Pierson A, Alonso-Mora J, Karaman S, Rus D. Social behavior for autonomous vehicles. *Proceedings of the National* *Academy of Sciences * 2019;116:24972–78. DOI

18. 

Roy D, Winkler D, Mohan C, Fukuda A. Detection of Collision-Prone Vehicle Behavior at Intersections using Siamese Interaction LSTM. 

*IEEE Transactions on Intelligent Transportation Systems * 2022;23:1031–42. DOI

19. 

Li N, Yao Y, Kolmanovsky I, Atkins E, Girard AR. Game-theoretic modeling of multi-vehicle interactions at uncontrolled intersections. 

*IEEE Trans Intell Transp Syst * 2020;23:1428–42. DOI

20. 

Tian R, Li N, Kolmanovsky I, Yildiz Y, Girard AR. Game-theoretic modeling of traffic in unsignalized intersection network for autonomous vehicle control verification and validation. *IEEE Trans Intell Transp Syst * 2020;23:2211–26. DOI

21. 

Crosato L, Tian K, Shum H, Shum H, Ho E. Social Interaction-Aware Dynamical Models and Decision-Making for Autonomous Vehicles. 

*Adv Intell Syst * 2024;6:2300575. DOI

22. 

Tabone W, de Winter J, Ackermann C, Bärgman J, Baumann M, et al. Vulnerable road users and the coming wave of automated vehicles: Expert perspectives. *Transp Res Interdiscip Persp * 2021;9:100293. DOI

23. 

Yu H, Tseng HE, Langari R. 

A human-like game theory-based controller for automatic lane changing. 

*Transport Res C-EMER*

2018;88:140–58. DOI

24. 

Zhang Y, Hang P, Huang C, Lv C. Human-Like Interactive Behavior Generation for Autonomous Vehicles: A Bayesian Game-Theoretic Approach with Turing Test. *Adv Intell Syst * 2022;4:2100211. DOI

25. 

Chen X, Sun J, Ma Z, Sun J, Zheng Z. Investigating the long-and short-term driving characteristics and incorporating them into car-following models. *Transport Res Part C: Emerg Technol * 2020;117:102698. DOI Pubmed

26. 

Hang P, Lv C, Huang C, Cai J, Hu Z, et al. An integrated framework of decision making and motion planning for autonomous vehicles considering social behaviors. *IEEE Trans Veh Technol * 2020;69:14458–69. DOI

Page 24 of 27

Chen *et al*. *Complex Eng Syst * 2024;4:25

**I**

http://dx.doi.org/10.20517/ces.2024.69

27. 

Hang P, Lv C, Xing Y, Huang C, Hu Z. Human-like decision making for autonomous driving: A noncooperative game theoretic approach. 

*IEEE Trans Intell Transp Syst * 2020;22:2076–87. DOI

28. 

Liu M, Wan Y, Lewis FL, Nageshrao S, Filev D. A three-level game-theoretic decision-making framework for autonomous vehicles. 

*IEEE Trans Intell Transp Syst * 2022;23:20298–308. DOI

29. 

Hang P, Huang C, Hu Z, Lv C. Decision Making for Connected Automated Vehicles at Urban Intersections Considering Social and Individual Benefits. *IEEE Trans Intell Transp Syst * 2022;23:22549–62. DOI Pubmed

30. 

Li D, Liu G, Xiao B. 

Human-like driving decision at unsignalized intersections based on game theory. *P I Mech Eng D-J Aut* 2023;237:159–73. DOI

31. 

Sagberg F, Selpi, Bianchi Piccinini GF, Engström J. A review of research on driving styles and road safety. *Human factors * 2015;57:1248–

75. DOI

32. 

Liu J, Qi X, Hang P, Sun J. Enhancing Social Decision-making of autonomous vehicles: A mixed-strategy game approach with interaction orientation identification. *IEEE Trans Veh Technol * 2024;73:12385–98. DOI

33. 

Negash N, Yang J. Driver Behavior Modeling Toward Autonomous Vehicles: Comprehensive Review. *IEEE Access * 2023;11:22788–

821. DOI

34. 

Qin Z, Ji A, Sun Z, Wu G, Hao P, et al. Game Theoretic Application to Intersection Management: A Literature Review. *IEEE Transactions* *on Intelligent Vehicles * 2024:1–19. DOI

35. 

Farooqui AD, Niazi MA. Game theory models for communication between agents: a review. *Complex Adapt Syst Model * 2016;4:1–

31. DOI

36. 

Li J, Niazi D, Zhang M. Equilibrium modeling of mixed autonomy traffic flow based on game theory. *Transportation Research Part B:* *Methodological * 2022;166:110–27. DOI

37. 

Nan J, Deng W, Zheng B. Intention Prediction and Mixed Strategy Nash Equilibrium-Based Decision-Making Framework for Autonomous Driving in Uncontrolled Intersection. *IEEE Transactions on Vehicular Technology * 2022;71:10316–26. DOI

38. 

Yoo JH, Langari R. Stackelberg game based model of highway driving. In: ASME 2012 5th Annual Dynamic Systems and Control Conference joint with the JSME 2012 11th Motion and Vibration Conference; 2012 Oct 17–19; Florida, USA. USA: ASME; 2012. pp. 

499–508. 

39. 

Yoo JH, Langari R. A stackelberg game theoretic driver model for merging. In: Proceedings of the ASME 2013 Dynamic Systems and Control Conference; 2013 Oct 21-23; Palo Alto, California, USA. USA: ASME; 2013. p. V002T30A003. 

40. 

Kim C, Langari R. Game theory based autonomous vehicles operation. *Int J Vehicle Des * 2014;65:360–83. DOI

41. 

Coskun S, Zhang Q, Langari R. Receding horizon markov game autonomous driving strategy. In: 2019 American Control Conference \(ACC\); 2019 Jul 10-12; Philadelphia, PA, USA. USA: IEEE; 2019. pp. 1367–1374. 

42. 

Yoo J, Langari R. A predictive perception model and control strategy for collision-free autonomous driving. *IEEE Trans Intell Transp* *Syst * 2019;20:4078–91. DOI

43. 

Zhang Q, Langari R, Tseng HE, Filev D, Szwabowski S, et al. A game theoretic model predictive controller with aggressiveness estimation for mandatory lane change. *IEEE Trans Intelligent Vehicles * 2019;5:75–89. DOI

44. 

Yoo J, Langari R. A game-theoretic model of human driving and application to discretionary lane-changes; 2020. ArXiv preprint arXiv:2003.09783. 

45. 

Yoo J, Langari R. A Stackelberg Game Theoretic Model of Lane-Merging; 2020. 10.48550/arXiv.2003.09786. 

46. 

Zhang Q, Filev D, Tseng HE, Szwabowski S, Langari R. A game theoretic four-stage model predictive controller for highway driving. 

In: 2019 American Control Conference \(ACC\); 2019 Jul 10-12; Philadelphia, PA, USA. USA: IEEE; 2019. pp. 1375–1381. 

47. 

Zhang Q, Filev D, Tseng HE, Szwabowski S, Langari R. Addressing Mandatory Lane Change Problem with Game Theoretic Model Predictive Control and Fuzzy Markov Chain. In: 2018 Annual American Control Conference \(ACC\); 2010 Jun 27-29; Milwaukee, WI, USA. USA: IEEE; 2018. pp. 4764–71. 

48. 

Banjanovic-Mehmedovic L, Halilovic E, Bosankic I, Kantardzic M, Kasapovic S. Autonomous vehicle-to-Vehicle \(V2V\) decision making in roundabout using game theory. *International journal of advanced computer science and applications * 2016;7. DOI

49. 

Liu H, Xin W, Adam Z, Ban J. A game theoretical approach for modeling merging and yielding behavior at freeway on-ramp sections. 

*Transport Traffic Theory * 2007;3:197–211. 

50. 

Talebpour A, Mahmassani HS, Hamdar SH. Modeling lane-changing behavior in a connected environment: A game theory approach. 

*Transport Res Procedia * 2015;7:420–40. DOI

51. 

Liu C, Tomizuka M. Safe exploration: Addressing various uncertainty levels in human robot interactions. In: 2015 American Control Conference \(ACC\); 2015 Jul 01-03; Chicago, IL, USA. USA: IEEE; 2015. pp. 465–70. 

52. 

Liu C, Tomizuka M. Enabling safe freeway driving for automated vehicles. In: American Control Conference \(ACC\); 2016 Jul 06-08;

Boston, MA, USA. USA: IEEE; 2016. pp. 3461–3467. 

53. 

Liu K, Li N, Tseng HE, Kolmanovsky I, Girard A. Interaction-aware trajectory prediction and planning for autonomous vehicles in forced merge scenarios. *IEEE Trans Intell Transp Syst * 2022;24:474–88. DOI

54. 

Sadigh D, Landolfi N, Sastry SS, Seshia SA, Dragan AD. *Planning for cars that coordinate with people: leveraging effects on human* *actions for planning and active information gathering over human internal state * 2018;42:1405–1426. DOI

55. 

Sun L, Zhan W, Tomizuka M, Dragan AD. Courteous autonomous cars. In: 2018 IEEE/RSJ International Conference on Intelligent Robots and Systems \(IROS\); 2018 Oct 01-05; Madrid, Spain. USA: IEEE; 2018. pp. 663–670. 

56. 

Murgovski N, de Campos G, Sjoberg J. Convex modeling of conflict resolution at traffic intersections. In: 2015 54th IEEE conference on decision and control \(CDC\); 2015 Dec 15-18; Osaka, Japan. USA: IEEE; 2015. pp. 4708–13. 

Chen *et al*. *Complex Eng Syst * 2024;4:25

**I**

http://dx.doi.org/10.20517/ces.2024.69

Page 25 of 27

57. 

Liu C, Lin CW, Shiraishi S, Tomizuka M. Distributed conflict resolution for connected autonomous vehicles. *IEEE Trans Veh Technol* 2017;3:18–29. DOI

58. 

Liu K, Li N, Tseng HE, Kolmanovsky I, Girard A, et al. Cooperation-aware decision making for autonomous vehicles in merge scenarios. 

In: 2021 60th IEEE Conference on Decision and Control \(CDC\); 2021 Dec 14-17; Austin, TX, USA. USA: IEEE; 2021. pp. 5006–12. 

59. 

Espinoza JLV, Liniger A, Schwarting W, Rus D, Van Gool L. Deep Interactive Motion Prediction and Planning: Playing Games with Motion Prediction Models. In: Proceedings of The 4th Annual Learning for Dynamics and Control Conference; 2022 Jun 23-24. New York: PMLR; 2022. pp. 1006–1019. 

60. 

Ozkan MF, Ma Y. 

Socially Compatible Control Design of Automated Vehicle in Mixed Traffic. 

*IEEE Control Systems Letters*

2022;6:1730–35. DOI Pubmed

61. 

Oyler DW, Yildiz Y, Girard AR, Li NI, Kolmanovsky IV. A game theoretical model of traffic with multiple interacting drivers for use in autonomous vehicle development. In: 2016 American Control Conference \(ACC\); 2016 July 6-8; Boston, MA, USA. USA: IEEE; 2016. 

pp. 1705–10. 

62. 

Li N, Oyler D, Zhang M, Yildiz Y, Girard A, et al. Hierarchical reasoning game theory based approach for evaluation and testing of autonomous vehicle control systems. In: 2016 IEEE 55th Conference on Decision and Control \(CDC\); 2016 Dec 12-14; Las Vegas, NV, USA. USA: IEEE; 2016. pp. 727–33. 

63. 

Li N, Oyler DW, Zhang M, Yildiz Y, Kolmanovsky I, et al. Game theoretic modeling of driver and vehicle interactions for verification and validation of autonomous vehicle control systems. *IEEE Trans Contr Syst Technol * 2017;26:1782–97. DOI

64. 

Wilde GJ. Social interaction patterns in driver behavior: An introductory review. *Human factors * 1976;18:477–92. DOI

65. 

Wilde GS. Immediate and delayed social interaction in road user behaviour. *Applied Psychology * 1980;29:439–60. DOI

66. 

Jia S, Zhang Y, Li X, Na X, Wang Y, et al. Interactive Decision-Making With Switchable Game Modes for Automated Vehicles at Intersections. *IEEE Transactions on Intelligent Transportation Systems * 2023;24:11785–99. DOI

67. 

Huang S, Chan S, Ren W. Mixed traffic control involving manually-controlled and automatically-controlled vehicles in IVHS. *Advances* *in Intelligent Autonomous Systems * 1999;18:507–528. DOI

68. 

Tian R, Li S, Li N, Kolmanovsky I, Girard A, et al. Adaptive Game-Theoretic Decision Making for Autonomous Vehicle Control at Roundabouts. In: 2018 IEEE Conference on Decision and Control \(CDC\); 2018 Dec 17-19; Miami, FL, USA. USA: IEEE; 2018. pp. 

321–26. 

69. 

Li N, Kolmanovsky I, Girard A, Yildiz Y. Game theoretic modeling of vehicle interactions at unsignalized intersections and application to autonomous vehicle control. In: 2018 Annual American Control Conference \(ACC\); 2018 Jun 27-29; Milwaukee, WI, USA. USA: IEEE; 2018. p. V002T30A003. 

70. 

Sun L, Zhan W, Tomizuka M. Probabilistic prediction of interactive driving behavior via hierarchical inverse reinforcement learning. In: 2018 21st International Conference on Intelligent Transportation Systems \(ITSC\); 2018 Nov 04-07; Maui, HI, USA. USA: IEEE; 2018. 

pp. 2111–17. 

71. 

McClintock CG, Allison ST. Social value orientation and helping behavior. *J Appl Soc Psychol * 1989;19:353–62. DOI

72. 

Zhao X, Tian Y, Sun J. Yield or Rush? Social-Preference-Aware Driving Interaction Modeling Using Game-Theoretic Framework. In: 2021 IEEE International Intelligent Transportation Systems Conference \(ITSC\); 2021 Sep 19-22; Indianapolis, IN, USA. USA: IEEE;

2021. p. 453–459. 

73. 

Toghi B, Valiente R, Sadigh D, Pedarsani R, Fallah YP. Social Coordination and Altruism in Autonomous Driving. *IEEE Trans Intell* *Transp Syst * 2022;23:24791–804. DOI Pubmed

74. 

Toghi B, Valiente R, Sadigh D, Pedarsani R, Fallah Y. Altruistic Maneuver Planning for Cooperative Autonomous Vehicles Using Multi-agent Advantage Actor-Critic; 2021. ArXiv preprint arXiv:2107.05664. 

75. 

Lee N, Choi W, Vernaza P, Choy CB, Torr PH, et al. Desire: Distant future prediction in dynamic scenes with interacting agents. In: Proceedings of the IEEE conference on computer vision and pattern recognition\(CVPR\); 2017; Honolulu, HI, USA. USA: IEEE; 2017. 

pp. 336–45. 

76. 

Fisac JF, Bronstein E, Stefansson E, Sadigh D, Sastry SS, et al. Hierarchical game-theoretic planning for autonomous vehicles. In: 2019 International Conference on Robotics and Automation \(ICRA\); 2010 May 20-24; Montreal, QC, Canada. USA: IEEE; 2019. pp. 

9590–9596. 

77. 

Liu M, Tseng HE, Filev D, Girard A, Kolmanovsky I. Safe and human-like autonomous driving: A predictor-corrector potential game approach. *IEEE Trans Contr Syst Technol * 2024;32:834–48. DOI

78. 

Wang M, Hoogendoorn SP, Daamen W, van Arem B, Happee R. *Game theoretic approach for predictive lane-changing and car-following* *control *. 

79. 

Shu K, Mehrizi RV, Li S, Pirani M, Khajepour A. Human inspired autonomous intersection handling using game theory. *IEEE Trans* *Intell Transp Syst * 2023;24:11360–71. DOI

80. 

Fridovich-Keil D, Ratner E, Peters L, Dragan AD, Tomlin CJ. Efficient iterative linear-quadratic approximations for nonlinear multi-player general-sum differential games. In: 2020 IEEE Int. Conf. Robot. Autom. \(ICRA\); 2020 May 31; Paris, France. USA: IEEE; 2020. 

pp. 1475–81. 

81. 

Fridovich-Keil D, Ratner E, Peters L, Tomlin CJ. An iterative quadratic method for general-sum differential games with feedback linearizable dynamics. In: 2020 IEEE Int. Conf. Robot. Autom. \(ICRA\); 2020 May 31; Paris, France. USA: IEEE; 2020. p. 2216–2222. 

82. 

Li S, Li N, Girard A, Kolmanovsky I. Decision making in dynamic and interactive environments based on cognitive hierarchy theory, Bayesian inference, and predictive control. In: 2019 IEEE 58th Conference on Decision and Control \(CDC\); 2019 December 11-13;

Nice, France. USA: IEEE; 2019. pp. 2181–87. 

Page 26 of 27

Chen *et al*. *Complex Eng Syst * 2024;4:25

**I**

http://dx.doi.org/10.20517/ces.2024.69

83. 

Liu M, Kolmanovsky I, Tseng HE, Huang S, Filev D, et al. Potential Game-based decision-making for autonomous driving. *IEEE Trans* *Intell Transp Syst * 2023;24:8014–27. DOI

84. 

Ozkan MF, Ma Y. Socially-compatible behavior design of autonomous vehicles with verification on real human data. *IEEE Robotics* *and Automation Letters * 2021;6:3421–28. DOI Pubmed

85. 

Lopez VG, Lewis FL, Liu M, Wan Y, Nageshrao S, et al. Game-Theoretic Lane-Changing Decision Making and Payoff Learning for Autonomous Vehicles. *IEEE Trans Veh Technol * 2022;71:3609–20. DOI Pubmed

86. 

Li D, Zhang J, Liu G. Autonomous Driving Decision Algorithm for Complex Multi-Vehicle Interactions: An Efficient Approach Based on Global Sorting and Local Gaming. *IEEE Transactions on Intelligent Transportation Systems * 2024;25:6927–37. DOI

87. 

Sadigh D, Sastry S, Seshia SA, Dragan AD. Planning for autonomous cars that leverage effects on human actions. *Robotics: Science* *and systems * 2016;2:1–9. 

88. 

Lazar DA, Pedarsani R, Chandrasekher K, Sadigh D. Maximizing road capacity using cars that influence people. In: 2018 IEEE

Conference on Decision and Control \(CDC\); 2018 Dec 17–19; Miami, FL, USA. USA: IEEE; 2018. pp. 1801–8. 

89. 

Hubmann C, Becker M, Althoff D, Lenz D, Stiller C. Decision making for autonomous driving considering interaction and uncertain prediction of surrounding vehicles. In: Proc. 2017 IEEE Intelligent Vehicles Symposium; 2017 Jun 11-14; Los Angeles, CA, USA. USA: IEEE; 2017. pp. 1671–78. 

90. 

Li D, Liu A, Pan H, Chen W. Safe, efficient and socially-compatible decision of automated vehicles: A case study of unsignalized intersection driving. *Automotive Innovation * 2023;6:281–96. DOI

91. 

Jain G, Kumar A, Bhat SA. Recent developments of game theory and reinforcement learning approaches: A systematic review. *IEEE*

*Access * 2024;12:9999–0011. DOI Pubmed

92. 

Sutton R, Barto A. Introduction to Reinforcement Learning. 1st ed. Cambridge: MIT Press; 1998. 

93. 

Zhang L, Han S, Grammatico S. Automated Lane Merging via Game Theory and Branch Model Predictive Control. *IEEE Transactions* *on Control Systems Technology * 2024:1–12. DOI

94. 

Chen X, Li Z, Di X. Social Learning In Markov Games: Empowering Autonomous Driving. In: 2022 IEEE Intelligent Vehicles Symposium \(IV\). USA: IEEE; 2022. pp. 78–483. 

95. 

Li W, Qiu F, Li L, Zhang Y, Wang K. Simulation of Vehicle Interaction Behavior in Merging Scenarios: A Deep Maximum Entropy-Inverse Reinforcement Learning Method Combined With Game Theory. *IEEE Transactions on Intelligent Vehicles * 2024;9:1079–93. DOI

96. 

Zhou X, Peng Z, Xie Y, Liu M, Ma J. Game-Theoretic Driver Modeling and Decision-Making for Autonomous Driving with Temporal-Spatial Attention-Based Deep Q-Learning. *IEEE Transactions on Intelligent Vehicles * 2024:1–17. DOI

97. 

Littman ML. Markov games as a framework for multi-agent reinforcement learning. In: Machine learning proceedings. Amsterdam: Elsevier; 1994. pp. 157–63. 

98. 

Liu C, Lin CW, Shiraishi S, Tomizuka M. Improving efficiency of autonomous vehicles by v2v communication. In: 2018 Annual American Control Conference \(ACC\); 2018 Jun 27-29; Milwaukee, WI, USA. USA: IEEE; 2018. pp. 4778–4783. 

99. 

Li N, Girard A, Kolmanovsky I. Stochastic predictive control for partially observable markov decision processes with time-joint chance constraints and application to autonomous vehicle control. *J Dyn Sys, Meas, Control * 2019;141:071007. DOI

100. Qiao Z, Muelling K, Dolan J, PNovalanisamy P, Mudalige P. Pomdp and hierarchical options MDP with continuous actions for autonomous driving at intersections. In: Proc. 21st Int. Conf. Intelligent Transportation Systems; 2018 Nov 04-07; Maui, HI, USA. USA: IEEE; 2018. pp. 2377–82. 

101. Cunningham AG, Galceran E, Mehta D, Ferrer G, Eustice RM, et al. Mpdm: Multi-policy decision-making from autonomous driving to social robot navigation. 1st ed. Cham: Springer International Publishing; 2019. 

102. Nishi T, Doshi P, Prokhorov D. Merging in congested freeway traffic using multipolicy decision making and passive actor-critic learning. 

*IEEE Trans Intelligent Vehicles * 2019;4:287–97. DOI

103. Sadigh D, Sastry SS, Seshia SA. Verifying robustness of human-aware autonomous cars. *IFAC-PapersOnLine * 2019;51:131–38. DOI

104. Sankar GS, Han K. Adaptive robust game-theoretic decision making strategy for autonomous vehicles in highway. *IEEE Trans Veh* *Technol * 2020;69:14484–93. DOI

105. Ho J, Ermon S. Generative Adversarial Imitation Learning. In: Lee D, Sugiyama M, Luxburg U, Guyon I, Garnett R, editors. Advances in Neural Information Processing Systems. Curran Associates, Inc.; 2016. . 

106. Treiber M, Hennecke A, Helbing D. Congested traffic states in empirical observations and microscopic simulations. *Physical Rev E*

2000;62:1805–24. DOI

107. Makaba T, Doorsamy W, Paul B. Bayesian network-based framework for cost-implication assessment of road traffic collisions. *Int J ITS*

*Res * 2021;19:240–53. DOI

108. Talebpour A, Mahmassani HS, Hamdar SH. Multiregime sequential risk-taking model of car-following behavior: Specification, calibration, and sensitivity analysis. *Transportation research record * 2011;2260:60–66. DOI

109. Wei C, He Y, Tian H, Lv Y. Game theoretic merging behavior control for autonomous vehicle at highway on-ramp. *IEEE Transactions* *on Intelligent Transportation Systems * 2022;23:21127–36. DOI

110. Ji K, Orsag M, Han K. Lane-Merging Strategy for a Self-driving car in dense traffic using the stackelberg game approach. *Electronics* 2021;10:894. DOI

111. Wang H, Wang W, Yuan S, Li X, Sun L. On social interactions of merging behaviors at highway on-ramps in congested traffic. *IEEE*

*Trans Intell Transp Syst * 2021;23:11237–48. DOI

112. De Dreu CK, Van Lange PA. The impact of social value orientations on negotiator cognition and behavior. *Pers Soc Psychol B*

1995;21:1178–88. DOI

Chen *et al*. *Complex Eng Syst * 2024;4:25

**I**

http://dx.doi.org/10.20517/ces.2024.69

Page 27 of 27

113. Pletzer JL, Balliet D, Joireman J, Kuhlman DM, Voelpel SC, et al. Socal value orientation, expectations, and cooperation in social dilemmas: A meta-analysis. *Eur J Personality * 2018;32:62–83. DOI

114. Rahmati Y, Talebpour A. Towards a collaborative connected, automated driving environment: A game theory based decision framework for unprotected left turn maneuvers. In: 2017 IEEE Intelligent Vehicles Symposium \(IV\); 2017 Jun 11–14; Los Angeles, CA, USA. USA: IEEE; 2017. pp. 1316–21. 

115. Rahmati Y, Talebpour A, Mittal A, Fishelson J. Game Theory-Based Framework for Modeling Human–Vehicle Interactions on the Road. 

*Transportation research record * 2020;2674:701–13. DOI

116. Gkartzonikas C, Gkritza K. What have we learned? A review of stated preference and choice studies on autonomous vehicles. *Transport* *Res Part C: Emerg Technol * 2019;98:323–37. DOI

117. Lemmer M, Shu J, S S, Hohmann S. Maneuver Based Modeling of Driver Decision Making using Game-Theoretic Planning. In: 2021

IEEE International Conference on Systems Man, and Cybernetics \(SMC\). USA: IEEE; 2021. p. 1332–1338. 

118. Zhu L, Yang D, Cheng Z, Yu X, Zheng B. A Model to Manage the Lane-Changing Conflict for Automated Vehicles Based on Game Theory. *Sustainability * 2023;15:3063. DOI

119. Huang H, Zheng X, Liu Y, Zhao S, Wang Y, et al. Intelligent Adaptive Decision-Making for Autonomous Vehicles: A Learning-Enhanced Game-Theoretic Approach in Interactive Scenarios. In: 2023 3rd International Conference on Digital Society and Intelligent Systems \(DSInS\). USA: IEEE; 2023. pp. 258–64. 

120. Dai S, Bae S, Isele D. *Game Theoretic Decision Making by Actively Learning Human Intentions Applied on Autonomous Driving* 2023:1–6. DOI


# Document Outline

+ 1. Introduction 
+ 2. Definition and Attributes of Social Interaction in Road Traffic  
	+ 2.1 Definition and attribution of social interaction 
	+ 2.2 Summary 

+ 3. Overview of pivotal factors in game theoretic decision-making and control algorithms 
+ 4. Game Theory-based Decision-Making Strategy in Deterministic Environment  
	+ 4.1 One-shot games in determined environment  
		+ 4.1.1 Stackelberg game theoretic decision-making 
		+ 4.1.2 Simultaneous game theoretic decision-making 

	+ 4.2 Utility function construction 
	+ 4.3 Summary 

+ 5. Human-Like Decision-Making Considering Dynamic Interaction Modeling  
	+ 5.1 Human likeness evaluation metrics 
	+ 5.2 Human-like decision-making methods considering time-varying controls 
	+ 5.3 Real-time solution for multi-vehicle dynamic interactive decision making 
	+ 5.4 Summary 

+ 6. Game theoretic decision-making and control methods with adaptation  
	+ 6.1 Game theoretic decision-making and control methods combining reinforcement learning  
		+ 6.1.1 Integrated methods of Markov/stochastic game and RL 
		+ 6.1.2 Integrated methods of Level-k game and RL 

	+ 6.2 Dynamic games with incomplete information  
		+ 6.2.1 Dynamic games with driving style estimation 
		+ 6.2.2 Dynamic games with intention estimation 
		+ 6.2.3 Dynamic games with sociality estimation 

	+ 6.3 Summary 

+ 7. Conclusion and outlook 
+ Declarations  
	+ Authors’ contributions 
	+ Availability of data and materials 
	+ Financial support and sponsorship 
	+ Conflicts of interest 
	+ Ethical approval and consent to participate 
	+ Consent for publication 
	+ Copyright



