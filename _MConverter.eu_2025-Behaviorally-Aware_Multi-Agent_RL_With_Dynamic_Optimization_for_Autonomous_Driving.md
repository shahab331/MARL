10672

IEEE TRANSACTIONS ON AUTOMATION SCIENCE AND ENGINEERING, VOL. 22, 2025

Behaviorally-Aware Multi-Agent RL With Dynamic Optimization for Autonomous Driving

Hamid Taghavifar , Senior Member, IEEE, Chuan Hu , Chongfeng Wei , Member, IEEE, Ardashir Mohammadzadeh , and Chunwei Zhang

Abstract— This study presents a novel Multi-Agent Reinforce-between multiple autonomous agents, spanning a continuum from ment Learning \(MURL\) architecture for autonomous vehicle \(AV\) self-interested to entirely cooperative behaviors. This allows AVs navigation in complex urban traffic environments. By integrating to make decisions socially and cooperatively. This framework a Social Value Orientation \(SVO\) model into a model-free SARSA significantly influences the AV navigation sector by contributing reinforcement learning framework, our approach effectively to the development of secure, human-centric, and reliable trans-balances individual agents’ social preferences with safety and per-portation systems. Its multi-agent focus and the incorporation formance objectives. A logistic regression-based risk assessment of dynamic optimization emphasize its potential to facilitate module evaluates collision probabilities in real time by analyz-a network of AVs that interact with diverse road users, thus ing spatiotemporal dynamics such as distances and velocities. 

improving scalability. The robustness and adaptability of this Additionally, a dynamic optimizer adapts the learning rate and machine learning-powered solution are crucial for navigating the exploration strategies of the SARSA algorithm to provide efficient varied scenarios that characterize urban driving, ensuring that convergence to optimal policies. Extensive simulation experiments AVs can adapt to changing conditions and make decisions that demonstrate that the proposed method significantly enhances benefit all road users. 

safety and efficiency, achieving a 55.6% reduction in collision Index Terms— Automated vehicles, collision avoidance, rein-risk and increasing average rewards per episode by 2.1 compared forcement learning, path planning. 

to traditional SARSA without SVO. Furthermore, the optimized policy reduces average episode length, indicating the framework’s I. I

effectiveness in providing robust decision-making and adaptabil-NTRODUCTION

ity across various traffic scenarios. 

ACCORDING to the World Health Organization \(WHO\), there are approximately 1.19 million casualties per year Note to Practitioners—The proposed framework in this paper due to road traffic accidents \[1\]. The primary cause of fatalities is driven by the demand for comprehensive navigation systems in for individuals between 5 and 29 years of age is road traffic the rapidly evolving field of connected and autonomous vehicles \(CAVs\), especially within complex and unpredictable urban injuries. Furthermore, 92% of road fatalities worldwide happen environments and mixed traffic scenarios. As AVs are getting in low-income and middle-income countries, despite having more and more attention, the capacity to navigate effectively only around 60% of the vehicles. In addition, road traffic acci-among many road users, including other AVs, pedestrians, and dents result in a 3% loss of GDP for most countries. AVs are human-driven vehicles, is essential. Our framework builds upon expected to make a transformative change to the existing trans-the SARSA algorithm to produce an optimal policy for the AV

and integrates a dynamic optimization method that represents portation system by improving traffic efficiency \[2\], increasing

the concept of risk as the inverse logistic of potential collisions. 

driving safety \[3\], reducing environmental impact \[4\], and

Distinctive to our proposed model is a finely-tuned Social Value facilitating driving for the elderly and vulnerable road users Orientation \(SVO\) that captures the nuanced social dynamics or people with disabilities \[5\]. Therefore, there has been much attention in the last couple of decades on improving Received 14 October 2024; revised 3 December 2024; accepted 3 January 2025. Date of publication 8 January 2025; date of current version 8 April the performance of AVs and their reliability for mass com-2025. This article was recommended for publication by Associate Editor mercialization. Despite improved automotive technologies and W. Zhang and Editor P. Rocco upon evaluation of the reviewers’ comments. 

driver assistance systems \(ADAS\), road accidents still occur This work was supported in part by the Natural Sciences and Engineering Research Council of Canada \(NSERC\) under Grant RGPIN-2023-04816. 

frequently, resulting in injuries and fatalities \[6\]. 

\(Corresponding authors: Hamid Taghavifar; Ardashir Mohammadzadeh; A range of complex challenges has emerged since trans-Chunwei Zhang.\)

forming into intelligent transportation systems in which AVs Hamid Taghavifar is with the Department of Mechanical, Industrial and Aerospace Engineering, Concordia University, Montreal, QC H3G 1M8, are an integral part of its ecosystem. These challenges include Canada \(e-mail: hamid.taghavifar@concordia.ca\). 

the technical complexities of autonomous navigation and the Chuan Hu is with the School of Mechanical Engineering, Shanghai Jiao intricate interplay of social and ethical considerations that Tong University, Shanghai 200240, China. 

Chongfeng Wei is with the James Watt School of Engineering, University influence every driving decision \[7\], \[8\]. Indeed, a primary of Glasgow, G12 8QQ Glasgow, U.K. 

concern in creating trustworthiness in AVs is the ability to Ardashir Mohammadzadeh is with the Department of Electrical and Elec-make socially interpretable and intuitive judgments in the tronics Engineering, Sakarya University, 54050 Sakarya, Türkiye \(e-mail: ardashir@skarya.edu.tr\). 

face of complex obstacles \[9\]. However, it is known that AV

Chunwei Zhang is with the Multidisciplinary Center for Infrastructure navigation relies on pre-defined decision-making algorithms Engineering, Shenyang University of Technology, Shenyang 110870, China \(e-mail: zhangchunwei@sut.edu.cn\). 

for safe and efficient travel, while human drivers make intrin-Digital Object Identifier 10.1109/TASE.2025.3527327

sically intuitive decisions based on their instincts and intuitive 1558-3783 © 2025 IEEE. All rights reserved, including rights for text and data mining, and training of artificial intelligence and similar technologies. Personal use is permitted, but republication/redistribution requires IEEE permission. 

See https://www.ieee.org/publications/rights/index.html for more information. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:43:43 UTC from IEEE Xplore. Restrictions apply. 

TAGHAVIFAR et al.: BEHAVIORALLY-AWARE MURL WITH DYNAMIC OPTIMIZATION FOR AUTONOMOUS DRIVING

10673

adaptability \[10\]. Consequently, designing AVs that coexist Reward-State-Action\), a method of RL, can be effectively with human-driven vehicles, as well as with other cars with utilized due to its balance of exploration and exploitation, multi-level autonomy, cyclists, and pedestrians, has become enabling real-time decision-making while addressing some increasingly essential and challenging \[11\]. In this complex of the limitations inherent in IRL \[15\]. SARSA is an RL

system of interactions, the capacity to compute the ideal route algorithm that can significantly enhance the decision-making from the current position to the final destination while adhering task for AVs by being trained for optimal policies and updating to kinetic dynamics and physical limitations of the vehicle Q-values considering the rewards as a result of the actions needs to be considered for safe autonomous driving \[12\]. 

taken \[28\]. SARSA is less prone to overfitting and train-Traditional navigation schemes for AVs have two main ing instability than deep learning models, and its ability to limitations. They tend to be overly cautious in design, leading manage high-order state-action spaces is useful in navigating to unpredictable driving that contrasts with human drivers’

the complexities of AV decision-making \[29\]. Despite their intuitive behavior \[13\], \[14\]. This over-cautious approach can ability to optimize the reward function, RL algorithms cannot adversely impact traffic flow and trigger confusion among inherently ensure safety and ethical behavior as well as the other road users. Secondly, these systems encounter challenges social interactions between the agents and, thus, often can in adapting to unforeseen scenes, which is a critical issue con-overlook the potential risks and broader consequences \[28\]. 

sidering the number of potential scenarios encountered on the To achieve this purpose, the incorporation of advanced frame-road \[10\]. This limitation can result in hesitation or inappropri-works that are behaviorally and socially aware is required. 

ate responses in complex or novel traffic conditions, potentially Such a framework should evaluate and mitigate risks by compromising safety and efficiency \[15\]. A spectrum of considering social behaviors and contextual cues within the decision-making methods has emerged to address these limi-driving environment \[30\]. 

tations, from model-based approaches to advanced data-driven Social and behavioral-aware planning and decision-making tools \[14\]. Model-based approaches develop according to algorithms mixed with DRL and multi-agent reinforcement predefined relationships and heuristics that provide trans-learning \(MURL\) have been studied in various urban driving parency and simplicity \[16\]. However, such methods can conditions \[31\], \[32\], \[33\], \[34\]. In \[32\], Valiente et al. 

face problems in the events of the dynamic nature of traffic proposed a decentralized MARL framework for cooperative environments \[15\]. On the other hand, AI-enabled decision-AVs in mixed-autonomy traffic. For this purpose, a Double making approaches, such as reinforcement learning \(RL\), Deep Q-Network \(DDQN\) was utilized to enable AVs to learn have demonstrated great promise for decision-making tasks of from experience and optimize social utility and, accordingly, AVs \[17\]. These algorithms can comprehend interactions with to improve safety in the presence of human-driven vehicles the environment and adapt to changing scenarios. However, \(HVs\) with varying behaviors. In \[33\], a DRL-based decision-one limitation is that significant data and training may only making approach was proposed for AVs at unsignalized sometimes be generalized to other environments or those deci-intersections, in which the Twin Delayed Deep Determin-sions that are humanly interpretable \[18\]. RL approaches may istic Policy Gradient \(TD3\) method with an ego-attention also encounter the credit assignment issue, which challenges mechanism was used to enable AVs to interact with social learning long-term temporal correlations between decisions vehicles and make efficient right-turn decisions. Also, in \[34\], 

and the agent’s overall performance \[18\], \[19\]. 

a prediction-aware and RL-based altruistic, cooperative driving The deep reinforcement learning \(DRL\) approach in AV

framework for AVs in mixed-autonomy traffic was studied. 

decision-making effectively handles complex state and action A Hybrid Predictive Network \(HPN\) and a value function spaces using neural networks for Q-value function estima-network \(VFN\) were used to anticipate future states and to tion in RL frameworks \[20\]. However, challenges, such as optimize for social utility, respectively. 

overfitting and training instability, can affect performance in However, existing social and behavioral-aware navigation real-world scenarios \[21\]. Other recent advancements in this techniques often fail to dynamically adapt to real-time inter-field include combining game theory for strategic multi-agent actions and effectively balance individual objectives with interactions and the development of human-centered strate-collective safety. Our BSI framework addresses this by integies \[22\], \[23\]. These strategies are designed to emulate grating dynamic Social Value Orientation \(SVO\) with RL. 

human decision-making processes in AVs, thereby enhancing The proposed BSI framework in our paper includes a com-safety and predictability in various traffic conditions. Inverse prehensive analysis of the interactions between AVs and their Reinforcement Learning \(IRL\) has also been proven as a surrounding environment. It focuses on human behavior, social capable method for enhancing the navigation systems for dynamics, and contextual factors to identify and assess poten-AVs by learning from the behavior of human drivers \[24\], 

tial hazards. By incorporating this BSI algorithm into RL, AVs

\[25\]. IRL aims to infer the underlying reward function that can enhance their decision-making processes, ensuring that a human driver optimizes, allowing AVs to replicate human-they act safely, ethically, and socially compliant by adhering like decision-making in complex driving environments \[26\]. 

to identified risks and constraints. Additionally, our model By leveraging data from human drivers, IRL can provide more includes an advanced SVO framework to assess individuals’

intuitive and acceptable driving strategies. However, IRL also preferences for balancing personal well-being with the welfare has significant drawbacks, including the complexity of accu-of others. These preferences are categorized as altruistic and rately modeling human driving behavior and the computational egocentric. By combining the SVO architecture and learning-intensity of the learning process \[27\]. SARSA \(State-Action-based model-free RL, our goal is to enhance all road users’

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:43:43 UTC from IEEE Xplore. Restrictions apply. 



10674

IEEE TRANSACTIONS ON AUTOMATION SCIENCE AND ENGINEERING, VOL. 22, 2025

safety and comfort and prioritize AVs’ operational objectives. 

This integration helps create trustworthy and human-like navigation for AVs, ultimately improving autonomous driving technologies’ overall reliability and acceptance. Hence, this study is conducted based on the following considerations and objectives:

1\) Our proposed architecture prioritizes promoting trust and acceptance among road users in shared spaces and multi-agent environments. It ensures that potential risks and constraints are considered during decision-making and autonomous navigation for the ego vehicle. 

Fig. 1. Urban Traffic Scenario with AV and Multiple Pedestrians and Cyclists, 2\) This architecture attempts to effectively interpret and Highlighting Interaction Points for Behavioral Analysis \[35\]. 

react to social and behavioral cues from other road users. The existing navigation structures usually need II. PROBLEM FORMULATION

more adaptability to deal effectively with unpredictable A. State Representation

or unexpected circumstances. Our presented architecture In our multi-agent system, we have a number of cars enables AVs to navigate intuitively and reliably by and pedestrians interacting in a complex and shared urban considering other traffic participants’ social cues and environment. Fig. 1 shows an urban traffic scenario involving actions. 

an ego car, multiple pedestrians, and a cyclist, illustrating the A primary contribution of this study lies in integrating an critical interaction points that are essential for analyzing the advanced social intelligence scheme in a MURL environment, behavioral dynamics in the proposed reinforcement learning thereby refining the reward mechanisms of the Q-learning framework. Each car is denoted as Ci \(for i = 1, 2, . . . , n\) scheme to promote more human-like and ethically logical and each pedestrian as Pj \(for j = 1, 2, . . . , m \). The state of vehicle behaviors. Hence, a reward structure is proposed that the system at any given time t is described by a vector x\(t\) : discourages actions detrimental to other traffic participants x\(t\)

while incentivizing those that enhance the safety of other agents in the shared spaces. This reward system ensures AVs

= xC \(t\), x \(t\), . . . , x \(t\), x \(t\), x \(t\), . . . , x \(t\)T

1

C2

Cn

P1

P2

Pm

navigate complex traffic efficiently and responsibly according \(1\)

to human logic and intuitions. Given the above motivations, the present study makes these contributions: where xC \(t\) = p \(t\), v \(t\)T represents the state of car i

C

C

i

i

i , and p \(t\) and v \(t\) are its position and velocity vectors, 1\) In this study, a new hybrid socially and behaviorally C

C

i

i

h

intelligent model-free RL scheme is presented, which respectively. Similarly, x P \(t\) = p \(t\), v \(t\)iT represents j

P

P

j

j

considers the interplay dynamics among the AVs and the state of pedestrian j . The dynamics of each car and other agents in complex traffic by combining the SARSA pedestrian are expressed through their positional and velocity scheme to discover the best policy for the AV. In addi-changes over time:

tion, we also design and include a risk cost as an 1

indicator of the likelihood of collisions. 

p \(t \+ 1\) = p \(t\) \+ v \(t\)1t \+ a \(t\)1t2

C

C

C

i

Ci

i

i

2\) A new and modified social psychology model according 2

to the principle of value orientation is presented. This vC \(t \+ 1\) = v \(t\) \+ a \(t\)1t

i

Ci

Ci

architecture continuously quantifies various cues based 1

p \(t \+ 1\) = p \(t\) \+ vP \(t\)1t \+ aP \(t\)1t2

on the system’s states and outputs a value of social Pj

Pj

j

2

j

preferences ranging from altruistic to egocentric to the vP \(t \+ 1\) = v \(t\) \+ a \(t\)1t

\(2\)

j

Pj

Pj

agents in the shared traffic space. 

where a \(t\) and a \(t\) represent the acceleration vectors 3\) Our presented architecture employs a dynamic optimiza-Ci

Pj

for car i and pedestrian j at time t , respectively, and 1t tion method to iteratively refine the learning rate and represents the time step between states. Additionally, the exploration strategies of the SARSA algorithm. This position vectors of car i and pedestrian j at time t are typically advanced policy derivation process ensures the conver-in a two-dimensional plane representing a map or urban area, gence to an optimal strategy that balances all agents’

and the velocity vectors of car i and pedestrian j indicate safety, efficiency, and social preferences. 

their speed and direction of movement. These vectors can be The rest of this paper is structured as follows: Section II

influenced by factors like the agent’s decision-making, road outlines the problem formulation, Section III describes the conditions, and interactions with other agents. The accelera-integration of the SARSA Algorithm with SVO, Section IV

tions of cars and pedestrians are influenced by their control details the Optimal Policy Derivation framework, Section V

inputs and external factors, modeled as disturbances as: explains the Dynamic SVO in the multi-agent complex environment, Section VI presents and analyzes the results, and aC \(t\) = u \(t\) \+ w \(t\), 

i

Ci

Ci

Section VII provides the conclusions. 

aP \(t\) = u \(t\) \+ w \(t\), 

\(3\)

j

Pj

Pj

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:43:43 UTC from IEEE Xplore. Restrictions apply. 



TAGHAVIFAR et al.: BEHAVIORALLY-AWARE MURL WITH DYNAMIC OPTIMIZATION FOR AUTONOMOUS DRIVING

10675



\! 

1

×

\(4\)

1 \+ exp 

\(

\( 

vC

t \) − v

t \)

i

Pj





where p \(t\) − p \(t\) is the Euclidean distance between Ci

Pj



car i and pedestrian j , and v \(

\(



C

t \) − v

t \)

i

Pj

is the relative

velocity that indicates how fast the distance between the entities is closing. The coefficients in Eq. 4 are determined through logistic regression using this historical interaction data, which enables the model to accurately reflect the influence of distance and relative velocity on collision probability. Additionally, the logistic regression model in Eq. 4 computes collision risk by leveraging both distance and relative velocity as key indicators Fig. 2. 

Illustration of the multi-agent scenario in the SVO-reshaped SARSA environment, which depicts the interaction between two ego cars and two of potential collision. The exponential decay based on distance pedestrians. Each agent \(car or pedestrian\) is characterized by its position \( p\), reflects how quickly collision risk decreases as the car and velocity \(v\), and acceleration \(a\). The predefined path of ego car 1 indicates pedestrian move further apart, while the logistic function on the decision-making process influenced by the actions A = \{a1, a2, a3\}. 

velocity captures how faster relative speeds increase collision where u

likelihood. This combination provides a well-rounded measure C \(t \) and u

\(t\) represent the control inputs for car

i

Pj

i and pedestrian j at time t , respectively. These inputs are of risk. 

decisions the agents \(or the driver/pedestrian in a real-world Logistic regression has several advantages over the Bayesian scenario\) make based on their current state and objectives. 

approach \[37\]. Firstly, it is straightforward to implement and Additionally, the terms w

computationally less demanding, making it ideal for systems C \(t \) and w

\(t\) are disturbance

i

Pj

vectors for car i and pedestrian j , accounting for unexpected that require real-time decision-making. Secondly, it does not motion influences. These disturbances can include environ-require extensive prior data or a complex process of updating mental conditions \(e.g., slippery roads, wind\), unmodeled beliefs based on new evidence, making it less data-dependent. 

dynamics, or random fluctuations in the agent’s behavior. 

Lastly, the model coefficients directly reflect the influence of Fig. 2 illustrates the MURL in the SVO-reshaped SARSA each feature on the collision probability by providing direct environment and shows the interaction between two ego cars interpretability. 

and two pedestrians. Each agent \(car or pedestrian\) is charac-C. Experience-Driven SVO Dynamics

terized by its position \( p\), velocity \(v\), and acceleration \(a\). 

The predefined path of ego car 1 indicates the decision-making In the MURL context of urban traffic systems, the SVO

process influenced by the actions A = \{a

for car i and pedestrian j are defined as SV OC and SV OP , 1, a2, a3\}, where a1, 

i

j

a

respectively. These are modeled as continuous variables in the 2, and a3 represent acceleration, deceleration, and maintain speed based on if the path is clear if needed to yield to

\[−1, 1\] range, where −1 indicates completely competitive and pedestrians or avoid collisions, and to keep the agent’s velocity 1 indicates fully cooperative behavior. SVO is modeled as a constant in stable traffic conditions. 

continuous spectrum where each agent’s preference for coop-These actions directly influence the agent’s state transitions erative or competitive behavior is quantified. The SVO range as described by Eqs. 2 and 3. For example, selecting Action is limited to \[-1,1\] to ensure that all agents’ behaviors lie on a

a spectrum from fully competitive to fully cooperative, which 1 results in an increase in velocity \(vC \(t \+ 1\) = v \(t\) \+

i

Ci

a

provides a controlled and interpretable behavior adjustment C \(t \)1t \), affecting the agent’s position and interactions with i

other agents. Fig. 2 illustrates how these actions guide ego mechanism. This range allows for clear transitions between cars’ paths and interactions with pedestrians. For instance, different social behaviors, where -1 represents selfish behavior, Action a

and 1 indicates altruistic behavior. For cars Ci , SV OC might 2 \(Decelerate\) allows an AV to yield to a crossing i

pedestrian, enhancing safety, while Action a be influenced by the programmed driving style \(e.g., cautious, 1 \(Accelerate\)

enables the AV to proceed when clear to optimize traffic flow. 

aggressive\), and for pedestrians Pj , SV OP could reflect their j

current behavior, like hurried crossing or attentive walking. 

The SVO of each agent can dynamically change based on B. Logistic Regression-Based Collision Risk Assessment their experiences. For car i :

The logistic regression model offers a direct and computa-SVO \(t \+ 1\) = SVO \(t\) \+ η1SVO \(t\)

\(5\)

tionally efficient method for estimating collision probabilities Ci

Ci

Ci

in our MURL architecture. Unlike the Bayesian approach, where η is a learning rate and 1SVOC \(t\) is the change in SVO

i

which requires prior knowledge and Bayesian updating, this based on interactions and outcomes at time t . 1SVOC \(t\) is i

logistic regression can provide a fast estimation based on calculated by evaluating the difference in utility gained from observable features, such as distances and velocities \[37\]. As a cooperative versus competitive actions during interactions. 

result, this approach can be suitable for real-time applications. 

This adjustment allows the agent to adapt its social preferences The collision risk model Pc,i j between cars i and pedestrians dynamically based on the effectiveness and outcomes of its j in the MURL can be defined as:

previous decisions. 

Remark 1: Dynamic SVO allows agents to adapt their social 2

Pc,i j \(t\) = exp −

\(

\(

pC

t \) − p

t \)

preferences based on real-time experiences, which is crucial i

Pj



Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:43:43 UTC from IEEE Xplore. Restrictions apply. 

10676

IEEE TRANSACTIONS ON AUTOMATION SCIENCE AND ENGINEERING, VOL. 22, 2025

for achieving optimal performance in complex and dynamic where the differences in SVO values between the interacting environments. This adaptability enables agents to become agents and their interaction potential are considered, and there-more cooperative or competitive depending on the observed fore, both behavioral and positional aspects are incorporated outcomes of their interactions. Additionally, dynamic SVOs into the risk assessment. Furthermore, interaction potential enhance social learning, allowing agents to learn from their function Vi j \(t\) models the influence between car i and interactions with others and adjust their behavior to improve pedestrian j :

collective outcomes. This social learning process can lead





2 

to emergent cooperative behaviors that static SVOs cannot p \(t\) − p \(t\)



Ci

Pj







achieve. 

Vi j \(t\) = exp −

\(9\)



2σ 2



Remark 2: The concept of dynamic SVOs reflects the idea of agents evolving their strategies over time to maximize their utility, similar to evolutionary processes \[38\]. This approach where p \(t\) − p \(t\) measures the Euclidean distance Ci

Pj



could help identify new, more efficient strategies for managing between the ego car and the other agents, indicating their prox-traffic and avoiding collisions. Research in social psychol-imity. The parameter σ scales the influence of this distance ogy and behavioral economics suggests that human social on the interaction potential, with a larger σ leading to a more preferences are not fixed but evolve through interactions and gradual change in the potential over distance. 

feedback \[39\]. Furthermore, dynamic SVOs improve robustness and flexibility, allowing agents to handle varying traffic E. Modified Utility Functions Under SVO

conditions and unforeseen events better. By continuously The utility functions in the decision-making process can be updating their SVOs, agents can respond more effectively to modeled as:

unexpected scenarios, such as sudden pedestrian crossings. 

X

Remark 3: The mathematical modeling of dynamic SVOs UC \(x\) = w

\+ w

− w

R

i

1i vCi

2i aCi

3i

f Pj \(x \), 

involves the learning rate \(η\) and the change in SVO \(1SVO\). 

j

The learning rate controls the speed of adaptation, where a X

UP \(x\) = w4 j vP \+ w5 j aP − w6 j

R f Ci \(x\). 

\(10\)

higher learning rate leads to faster adaptation but may cause j

j

j

i

instability, while a lower learning rate ensures stability but slower adaptation. The change in SVO captures the influence where the velocity and acceleration components \(v and a\) of recent interactions on the agent’s social preferences and reflect the dynamic state of the agents, according to Eqs. 2

can be modeled based on rewards, penalties, and observed and 3. The weighting factors w1i , w2i , . . . , w6 j are scaling behaviors of other agents. The goal is to balance individual parameters that balance the importance of velocity, accel-utility and collective welfare, fostering a harmonious and effi-eration, and risk in the utility function for each agent. 

cient traffic environment. Dynamic SVOs provide a promising Additionally, the risk function components R f C and R

for

i

f Pj

framework for achieving this balance by considering uncer-cars and pedestrians are based on Eq. 6 and represent the tainties in the representation of social cues for other agents in impact of each agent’s actions on others, adjusted by their the environment. 

respective SVOs. We modify the utility function for the ego car to incorporate their SVO and risk functions directly: D. Enhanced Risk Functions and SVO Formulations U





C

x, SV O

= β

R \(x\) \+ β

\(11\)

i

Ci

1 S V OCi

Ci

2 1 − S V OCi 

The risk function R f is a composite measure that accounts where β

for both physical and social risks:

1 and β2 are the scaling factors obtained by trial and error. 

R f = RSVO,i j \(t\) \+ λS

\(6\)

III. OPTIMAL POLICY DERIVATION UNDER SVO

where RSVO,i j \(t\) represents the physical risk, calculated based on proximity to collision, speed, and other safety metrics. 

For obtaining the optimal policy π∗ using SARSA in a Furthermore, S denotes the social risk, reflecting the potential dynamic environment, we start with the definition of the value negative impact of an agent’s actions on others, calculated function under policy π :

from the SVOs of the involved agents, and λ is a weighting

" ∞

\#

X

factor, determining the balance between physical and social V π \(x, S V O\) = Eπ

γ kU\(xk, π\(xk\), S V O\) | x0 = x

risks. On this basis, the risk function, incorporating the SVO

k=0

of agents, is given by:

\(12\)



RSVO,i j \(t\) = λ1 Pc,i j \(t\) \+ λ2

\(

\(

where

S V OC

t \) − SV O

t \)

Eπ denotes the expectation with respect to policy π . 

i

Pj



\(7\)

Additionally, U \(xk, π\(xk\), S V O\) is the utility at step k, where λ1 and λ2 are weighting factors for collision probability based on Eq. 10, given state xk and SVO. The optimal policy and SVO difference, respectively. Additionally, the social risk π∗ maximizes this value function for all states: function can be further detailed based on the interaction potential and SVO differences:

π∗ = arg max V π\(x, S V O\) ∀x ∈ X

\(13\)

π

X



S =

S V OC − S V O

where Eq. 13 identifies the policy π∗ that yields the highest i

Pj Vi j \(t \)

\(8\)

i, j

expected utility, considering the influence of SVO in each Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:43:43 UTC from IEEE Xplore. Restrictions apply. 

TAGHAVIFAR et al.: BEHAVIORALLY-AWARE MURL WITH DYNAMIC OPTIMIZATION FOR AUTONOMOUS DRIVING

10677

state. Subsequently, the Bellman equation for SARSA, incor-If policy improvement stops, then πnew = π. Hence, for porating SVO, is given by:

all a:

Q\(x, a, S V O\) = U \(x, a, S V O\) \+ γ 

E Q x′, a′, S V O

Q\(x, π\(x\)\) = Q\(x, a\). 

\(20\)

\(14\)

This implies π is an optimal policy since no other policy can achieve higher expected utility. 

where Q\(x, a, S V O\) is the action-value function, giving the The policy improvement process guarantees monotonic expected utility of taking action a in state x and following improvement and converges to an optimal policy after a policy π thereafter. The convergence for SARSA with SVO

finite number of iterations. In practice, soft policy improve-can be assessed in the following steps:

ment methods like epsilon-greedy are often used to handle The Q-value is updated using this the temporal-difference exploration-exploitation trade-offs in continuous state spaces. 

\(TD\) error:

This section provides a mathematical foundation for under-Q\(x

standing how SARSA refines the policy towards optimality t , at , S V O \) ← Q\(xt , at , S V O \) \+ αδt \(15\)

and ensures convergence to the optimal policy in a dynamic Then, the TD error for SARSA is defined as:

optimization context. 

δt = U\(xt, at, SV O\) \+ γ Q\(xt\+1, at\+1, SV O\) V. DYNAMIC SVO IN THE MULTI-AGENT CONTEXT

− Q\(xt , at , SV O\)

\(16\)

The SARSA algorithm is applied to a multi-agent system Finally, this update rule converges to the optimal Q-values comprising cars and pedestrians. This approach is enhanced under standard learning rate decay and policy improvement by integrating SVO, reflecting each agent’s preference for conditions. The Robbins-Monro conditions for stochastic collaboration or competition. In our urban environment model, approximation \[36\] guarantee this convergence. 

each agent \(car or pedestrian\) at each time step t observes the current state st , takes action at , and receives a reward rt . The IV. SARSA A

objective is to learn a policy π : S → A maximizing expected LGORITHM WITH SVO INTEGRATION

cumulative reward:

The SARSA learning algorithm, considering SVO, is for-

" ∞

\#

malized as follows: First, we initialize Q\(x, a, SV O\) arbi-X

J \(π\) = Eπ

γ trt

\(21\)

trarily for all x ∈ X , a ∈ A, and SVO values. Then, for each t =0

episode we:

where γ is the discount factor. The SARSA algorithm a. Initialize x0 and choose a0 from x0 using policy π derived updates Q-values, representing expected cumulative rewards from Q \(e.g., ϵ-greedy\). 

for actions in given states, using the rule: b. For each step of the episode: i. 

1\) Take action at , observe the reward U , and transition to Q\(st , at \) ← Q\(st , at \) \+ α\(rt \+ γ Q\(st\+1, at\+1\) − Q\(st , at \)\) the next state xt\+1. 

\(22\)

2\) Choose the next action at\+1 from xt\+1 using the current policy π. 

where α is the learning rate. The algorithm utilizes an 3\) Update the Q-value Q\(x

ϵ-greedy policy for action selection. Then, SVO is integrated t , at , S V O \) using the SARSA

update rule based on the observed transition. 

into SARSA to model agents’ cooperative or competitive 4\) Set the current state and action to the next state and preferences. We modify the reward function R\(s, a, s′\) to action: x

include SVO terms by considering the utilities for both cars t ← xt \+1; at ← at \+1. 

and pedestrians as follows:

Then we perform policy improvement in SARSA iteratively with the policy π refined based on the updated action-value R\(s, a, s′\) = θC · U \(s, a, s′\) \+ \(1 − θ \) · U \(s, a, s′\) i

Ci

Pj

Pj

function Q. The policy π is updated using the action-values \(23\)

Q by selecting actions that maximize the expected utility: where U \(s, a, s′\) and U \(s, a, s′\) are the utilities for car i \(

C

P

1

if a = arg max Q\(x, a′, SV O\), 

i

j

π

and pedestrian j respectively. The SVO parameters θ

and

a′

C

new \(a | x\) =

i

0

otherwise. 

θP balance the importance of each agent’s utility. 

j

Furthermore, the utility functions are defined as: \(17\)

UC \(s, a, s′\) = α1Safety \(s, a, s′\)

By definition, for all a:

i

Ci

\+ α2Efficiency \(s, a, s′\) − α

\(s, a, s′\)

C

3RiskC

i

i

Q\(x, πnew\(x\)\) ≥ Q\(x, a\). 

\(18\)

UP \(s, a, s′\) = β

\(s, a, s′\)

j

1SafetyPj

Therefore, the expected utility of the new policy is greater

\+ β2ConvenienceP \(s, a, s′\)−β

\(s, a, s′\)

j

3RiskPj

than or equal to that of the old policy:

\(24\)

X

V πnew \(x\) =

π

α

new\(a | x\) Q\(x, a\) ≥ V π \(x\). 

\(19\)

1, 

α2, α3 are user-defined weighting factors for the a

car’s utility components and β1, β2, β3 are scaling factors Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:43:43 UTC from IEEE Xplore. Restrictions apply. 

10678

IEEE TRANSACTIONS ON AUTOMATION SCIENCE AND ENGINEERING, VOL. 22, 2025

for the pedestrian’s utility. The selection of αi values is based on empirical tuning and domain-specific knowledge to reflect the priorities of the AVs in navigation strategy. For instance, higher values of α1 emphasize safety, while higher values of α2 and α3 prioritize efficiency and risk minimization respectively. Furthermore, Safety \(s, a, s′\) Ci

and Safety \(s, a, s′\) represent the safety component of the Pj

utility for the car and pedestrian, respectively. Moreover, Efficiency \(s, a, s′\) represents the efficiency aspect of the Ci

car, such as minimizing travel time or adhering to optimal routes. ConvenienceP \(s, a, s′\) could represent factors such j

as minimizing waiting time at crosswalks for pedestrians. 

RiskC \(s, a, s′\) and Risk \(s, a, s′\) quantify the risk or cost i

Pj

associated with a particular state-action transition for cars and pedestrians, such as the risk of an accident or violating traffic rules. 

The Q-value function, considering the state-action pairs, becomes:

Q\(s, a\) = 

E Rt\+1 \+ γ Q\(s′, a′\) | s, a

\(25\)

Updated using:

Q\(st , at \)

← Q\(st , at \) \+ α\(Rt\+1 \+ γ Q\(st\+1, at\+1\) − Q\(st , at \)\) \(26\) Fig. 3. 

The outline of an SVO-based SARSA-RL framework for the The overall objective is to find the policy that maximizes socially intelligent interaction between ego vehicle and a dynamic multi-agent environment. 

the expected cumulative reward, defined as:

∞

TABLE I

X

J \(π\) = Eπ \[

γ t Rt\+1\]

\(27\)

HYPERPARAMETERS USED IN SVO-BASED SARSA

t =0

where π represents the policy, mapping states to actions. 

By employing the SARSA algorithm, the Q-function of a given policy π can be assessed, and the action associated with the highest Q-value in each state is chosen to determine the optimal policy. Fig. 3 gives an overview of the presented SARSA-RL framework incorporating SVO. This architecture enables considering the interplay between AVs and other agents in the environment through SVO. Furthermore, Algorithm 1 outlines the detailed steps of the framework using pseudo-code. 

VI. RESULTS AND DISCUSSION

The earlier sections of the paper detailed a MURL

time step size, and the total number of simulations. Our simu-decision-making model designed for dynamic urban traffic lation results validate the model’s capability to navigate urban contexts, focusing on interactions between AVs and pedestri-traffic efficiently and reduce collision risks with pedestrians ans at intersections. Central to our model is using spatial data, while optimizing vehicular travel efficiency. Comparative anal-such as the distances between cars and pedestrians, combined ysis demonstrates our model’s enhanced ability to balance with pedestrians’ SVO and vehicles’ collision risk assessments safety and efficiency. 

to facilitate effective decision-making in urban traffic settings. 

Fig. 4 shows the collision risk surface as a function of rel-Table I lists the hyperparameters used in our SVO-integrated ative velocity and distance between the ego vehicle and other SARSA algorithm, tailored for the urban multi-agent envi-objects. The horizontal axis represents the relative velocity, ronment. These parameters include separate learning rates while the vertical axis shows the distance norm to the other for vehicles and pedestrians, a discount factor for evaluating objects. The vertical axis illustrates the collision risk, which future states, a weighting parameter for the SVO model, and is highest when the distance is zero and the relative velocity diverse reward values for different actions. Additionally, the decreases \(indicating approaching agents\). Fig. 4 demonstrates hyperparameters account for the range of pedestrian velocities, the critical points where collision risk is most significant. 

Gaussian noise standard deviation, simulation time horizon, It also illustrates how both speed and proximity impact safety. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:43:43 UTC from IEEE Xplore. Restrictions apply. 





TAGHAVIFAR et al.: BEHAVIORALLY-AWARE MURL WITH DYNAMIC OPTIMIZATION FOR AUTONOMOUS DRIVING

10679

Algorithm 1 Multi-Agent System Interaction and Learning in Urban Environments

1: Input: Number of cars n, number of pedestrians m, time step 1t, parameters α1, α2, α3, β1, β2, γ , λ, η, σ

2: Initialize: State vectors xC \(0\) and x \(0\), SVO values i

Pj

SV OC , SV O , Q-values Q\(x, a, SV O\) for all i ∈

i

Pj

\{1, . . . , n\} and j ∈ \{1, . . . , m\}

3: for each time step t do

## 4:

for i = 1 to n do

▷ Update for each car

p \(t\) \+ v



C \(t \)1t \+ 1 aC \(t \)1t 2

## 5:

### x

Ci

i

2

i

C \(t \+ 1\) ←

i

vC \(t\) \+ a \(t\)1t

i

Ci

## 6:

### end for

## 7:

for j = 1 to m do

▷ Update for each pedestrian

p \(t\) \+ v \(t\)1t \+ 1 a \(t\)1t2

P

P

P

## 8:

### x

j

j

2

j

P \(t \+ 1\) ←

j

vP \(t\) \+ a \(t\)1t

j

Pj

## 9:

### end for

## 10:

for all pairs \(Ci , Pj \) do

▷ Interaction and Risk

Assessment 

Fig. 5. 

Interaction potential function visualizing the influence of distance 2 \! 

p

\(t\)− p \(t\)

and relative velocity on interaction dynamics. Higher interaction potential is Ci

P j



## 11:

Vi j \(t\) ← exp −

2σ 2

observed at closer distances and higher relative velocities. 

## 12:

### end for

## 13:

for all pairs \(Ci , Pj \) do

▷ Interaction and Risk

Assessment





2

## 14:

Pc,i j \(t\)

←

exp −

\(

\(

pC

t \) − p

t \)

×

i

Pj





1





1\+exp v



C \(t \)−vP \(t \)



i

j



## 15:

### end for

## 16:

### for each agent a do

▷ Policy Learning with SVO

## 17:

Update SVO based on interactions: SV Oa\(t \+

1\) = SV Oa\(t\) \+ η1SV Oa\(t\)

## 18:

Compute utility Ua\(x, SV Oa\)

## 19:

### Update

policy

π using SARSA: π∗

=

arg maxπ V π \(x, SV Oa\)

## 20:

Update Q-values using Bellman equation for

SARSA

Fig. 6. 

Dynamic adaptation of the SVO of the ego vehicle over time. The SVO changes based on interactions and outcomes, balancing egoistic and 21:

end for

prosocial behaviors. 

## 22: end for

23: Output: Optimized policies π ∗ for all agents rear-end scenarios, which also emphasizes how maintaining safe distances and appropriate speeds minimize collision risks. 

In Fig. 5, the interaction potential function is depicted to illustrate the influence of distance and relative velocity on the interaction dynamics between the ego vehicle and pedestrians or other vehicles. The horizontal axis represents the distance, the vertical axis represents the relative velocity, and the color gradient represents the interaction potential. Fig. 5 emphasizes the decrease in interaction potential as distance increases, especially at closer distances and higher relative velocities. 

Fig. 6 shows the dynamic adaptation of the SVO of the ego vehicle over time, indicating how the SVO dynamically changes based on the interactions and outcomes experienced by the ego vehicle. This adaptation allows the ego vehicle to adjust its social preferences, balancing egoistic and prosocial behaviors to optimize performance in varying traffic scenarios. 

Fig. 6 shows how the SVO stabilizes after initial fluctuations, Fig. 4. 

Collision risk surface as a function of relative velocity and distance between the ego vehicle and other agents. 

indicating the learning process and eventual convergence to a stable behavior pattern. Fig. 7 illustrates the average reward per The symmetry in the results, with both positive and negative episode for different SVO values spanning egoistical to proso-values for relative velocity, highlights the risk in head-on and cial in terms of the number of episodes. Fig. 7 also compares Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:43:43 UTC from IEEE Xplore. Restrictions apply. 





10680

IEEE TRANSACTIONS ON AUTOMATION SCIENCE AND ENGINEERING, VOL. 22, 2025

Fig. 7. Average Reward per Episode for Different SVOs. comparing the aver-Fig. 9. 

Heatmap of Q-values for State-Action Pairs in the SVO-Reshaped age reward progression for egoistic \(SV O = 0\), intermediate \(SV O = 0.7\), SARSA Algorithm. 

and prosocial \(SV O = 1\) orientations over time. 

Fig. 10. 

Learning curve and state visitation frequency over time using SVO-reshaped SARSA with proposed dynamic optimization algorithm. 

Fig. 8. 

Exploration Rate Decay and Policy Change Frequency over the number of episodes. 

are highly valued in those states. For instance, the highest the performance of three SVO settings: egoistic \(SV O = 0\), Q-values are observed for states 3 and 4 with actions 2 and 3, intermediate \(SV O = 0.7\), and prosocial \(SV O = 1\), and it respectively, suggesting that yielding and stopping lanes are is shown that intermediate agents achieve the highest average the most rewarding when the vehicle is in those states. 

rewards over time, followed by the prosocial and egoistic Fig. 10 presents the multi-agent system’s learning process agents. The shaded regions represent the confidence intervals, and state visitation dynamics using the SVO-reshaped SARSA indicating the variability in rewards across different runs. 

algorithm with dynamic optimization. Fig. 10 a graph shows Additionally, it is demonstrated how varying the SVO impacts the learning curve, represented by the average reward per the agents’ learning efficiency and reward optimization in a episode, which indicates a rapid initial increase in reward, fol-MURL environment. The overall trend in Fig. 7 demonstrates lowed by a plateau as the system approaches an optimal policy. 

that agents with higher SVO values learn more effective This trend suggests that the ego AV quickly learns effective strategies by considering the welfare of others. 

pedestrian interaction strategies and improves its performance Fig. 8 shows the changes in our MURL framework’s stratin the simulated environment. Fig. 10b demonstrates the state egy exploration behavior and policy over time. Initially, a high visitation frequency over time for three distinct states, with exploration and frequent policy adjustment is pronounced, each line tracking how often a particular state is visited. The but as the policy improves, exploration decreases, and policy convergence of state visitation frequencies over time reflects a changes slow down. This indicates a move towards policy sta-balanced exploration of state space, critical for ensuring robust bilization and convergence. Fig. 9 shows the Q-values heatmap policy learning. The parallel increase of all curves indicates generated from the SVO-reshaped SARSA algorithm with that the algorithm does not overly focus on any single state, dynamic optimization. This heatmap illustrates the learned which can prevent overfitting and ensure a generalized policy. 

Q-values for each state-action pair, where states are defined Fig. 11 illustrates the adaptability and stability of the by specific positions \(1-6\), and actions are defined by specific learning process in the SVO-reshaped SARSA algorithm with maneuvers \(1-6\). The intensity of the colors represents the dynamic optimization. Fig. 11a depicts the fluctuations in magnitude of the Q-values, with red representing lower values Q-value changes over time for different state-action pairs, and blue showing higher values. The high Q-values \(red represented as Q\(s1, a1\), Q\(s1, a2\), etc. A high degree of regions\) in certain state-action pairs indicate that these actions fluctuation indicates the algorithm’s exploration mechanism, Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:43:43 UTC from IEEE Xplore. Restrictions apply. 



TAGHAVIFAR et al.: BEHAVIORALLY-AWARE MURL WITH DYNAMIC OPTIMIZATION FOR AUTONOMOUS DRIVING

10681

Fig. 11. 

Temporal analysis of Q-value adjustments and convergence in the SVO-reshaped SARSA with proposed dynamic optimization algorithm. 

Fig. 13. 3D Surface Plots of Q-Values across State-Action Space: \(a\) Contour plot of the action-state space and \(b\) 3D surface plot representing the learned Q-values in the SVO-reshaped SARSA algorithm. 

TABLE II

EVALUATING PERFORMANCE WITH AND WITHOUT SVO CONSIDERING

COLLISION RISK AND AVERAGE EPISODE LENGTH

contour plot of the action-state space, revealing the geometric relationship between state-action pairs and their Q-values. 

Fig. 13b provides a 3D representation of the learned Q-values Fig. 12. 

Distribution of states visited and actions taken by the AV in and shows the policy’s behavior, indicating the algorithm’s the SVO-reshaped SARSA environment with proposed dynamic optimization preferences for state-action combinations. Higher Q-values are algorithm. 

represented by warmer colors, suggesting more favorable state-action pairs. Fig. 13 b implies that the algorithm has learned while the gradual decrease in fluctuation suggests the stabiliza-to assign higher Q-values to certain actions in specific states. 

tion of the learning process as the policy converges. Fig. 11b

Table II presents the integration of SVO into the SARSA presents the sum of squared Q-value differences. Initially, algorithm with a significant improvement in system per-large variances are observed, reflecting the system’s learning formance compared to traditional reinforcement learning and adaptation phase. Over time, these differences diminish, approaches. The proposed method substantially reduces the signifying that the algorithm is approaching an optimal set of collision risk to 0.08, compared to 0.18 for SARSA without Q-values. This convergence is a fundamental attribute of the SVO and 0.11 for the Deep Q-Network. This reduction in SVO-reshaped SARSA algorithm, demonstrating its capacity collision risk by 55.6% from the traditional SARSA and by to systematically reduce uncertainty and enhance precision. 

27.3% from the Deep Q-Network highlights the efficacy of Fig. 12 illustrates the distribution of states visited and actions the SVO framework in enhancing the safety of autonomous taken by the AV in the SVO-reshaped SARSA environment systems. Furthermore, the average reward per episode for the with the proposed dynamic optimization algorithm. Fig.12a

proposed method stands at 2.1, significantly higher than the shows the frequency of visits to each state, while the bottom 1.1 achieved by SARSA without SVO and the 1.6 achieved histogram displays the frequency of each action taken. Fig.12 b

by the Deep Q-Network. This enhancement indicates that shows that ‘Stop’ is the most frequently taken action, followed the suggested approach improves safety without sacrificing by ’Accelerate’ and ’Yield’. This distribution reflects the strate-the reward, which often represents system objectives such gic decision-making process influenced by the SVO-reshaped as speed, efficiency, or compliance with traffic regulations. 

SARSA algorithm. The higher frequency of ’Stop’ actions The most evident disparity is in the average episode length, indicates a strong emphasis on safety, likely to avoid collisions where the proposed method delivers an episode length of 435, in complex traffic scenarios. The frequencies of ’Accelerate’

significantly lower than the 754 and 954 steps required for and ’Yield’ suggest that the vehicle also maintains efficient SARSA without SVO and the Deep Q-Network, respectively. 

traffic flow and responds to dynamic changes. 

This substantial reduction signifies a more efficient policy as Fig. 13 illustrates the 3D surface plots mapping out the system reaches its goal state more swiftly. Figure 14 shows Q-values as a function of state and action indices within our the speed profiles of the ego vehicle, pedestrian, and another SVO-reshaped SARSA learning framework. Fig. 13a shows a vehicle across different SVO values. For an SVO of 0, the ego Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:43:43 UTC from IEEE Xplore. Restrictions apply. 

10682

IEEE TRANSACTIONS ON AUTOMATION SCIENCE AND ENGINEERING, VOL. 22, 2025

regression-based risk assessment to evaluate collision probabilities in real-time. The results of our simulation experiments showed a significant reduction in collision risk, an increase in average rewards per episode, and an efficient convergence to an optimal policy. Looking ahead, future work could focus on the integration of comprehensive psychological models, such as the Theory of Planned Behavior, to better comprehend the diversity of human behaviors in urban settings. Additionally, it is possible to extend the proposed framework to other complex traffic scenarios, such as multi-lane interactions and varying pedestrian dynamics, which would further improve its Fig. 14. 

Tempo-spatial analysis of the speed profile for the ego car, pedestrian, and other vehicle under different SVO values from SV O = 0 to generalization. 

SV O = 1 representing ego-centric to altruistic. 

REFERENCES

\[1\] World Health Org. \(Dec. 2023\). Road Traffic Injuries. \[Online\]. Available:

https://www.who.int/news-room/fact-sheets/detail/road-traffic-injuries\#:~: text=Approximately

\[2\] J. Zhu, L. Wang, I. Tasic, and X. Qu, “Improving freeway merging efficiency via flow-level coordination of connected and autonomous vehicles,” IEEE Trans. Intell. Transp. Syst., vol. 25, no. 7, pp. 6703–6715, Jul. 2024. 

\[3\] M. Garg and M. Bouroche, “Can connected autonomous vehicles improve mixed traffic safety without compromising efficiency in real-istic scenarios?” IEEE Trans. Intell. Transp. Syst., vol. 25, no. 6, pp. 6674–6689, Jun. 2023. 

\[4\] S. Zhong et al., “Energy and environmental impacts of shared autonomous vehicles under different pricing strategies,” NPJ Urban Fig. 15. 

Spatial analysis of the ego car, pedestrian, and other vehicle trajec-Sustainability, vol. 3, no. 1, p. 8, Feb. 2023. 

tories under different SVO values from SV O = 0 to SV O = 1 representing ego-centric to altruistic. 

\[5\] J. Hwang and S. Kim, “Autonomous vehicle transportation service for people with disabilities: Policy recommendations based on the evidence from hybrid choice model,” J. Transp. Geography, vol. 106, Jan. 2023, Art. no. 103499. 

vehicle keeps higher speeds with infrequent reductions, which

\[6\] J. Schoner, R. Sanders, and T. Goddard, “Effects of advanced driver prioritizes its own progress and shows a self-centered driving assistance systems on impact velocity and injury severity: An exploration of data from the crash investigation sampling system,” Transp. Res. Rec., behavior. As the SVO value increases to 0.7, the ego vehicle J. Transp. Res. Board, vol. 2678, no. 5, pp. 451–462, May 2024. 

reduces its speed earlier, adopting a more cautious approach

\[7\] V. Dubljevic et al., “Toward a rational and ethical sociotechnical system to ensure safer interactions with the pedestrian and the other of autonomous vehicles: A novel application of multi-criteria decision analysis,” PLoS ONE, vol. 16, no. 8, Aug. 2021, Art. no. e0256224. 

vehicle. With an SVO of 1, the ego vehicle maintains its speed

\[8\] H. Taghavifar and A. Mohammadzadeh, “Integrating deep reinforce-longer before braking, relying on precise risk assessments to ment learning and social-behavioral cues: A new human-centric decide when to reduce speed. This behavior is suggestive of a cyber-physical approach in automated vehicle decision-making,” Proc. 

Inst. Mech. Eng., D, J. Automobile Eng., vol. 2024, Feb. 2024, fully prosocial strategy that can aim to optimize overall traffic Art. no. 09544070241230126. 

flow and minimize unnecessary interventions. In this scenario, 

\[9\] B. Toghi, R. Valiente, D. Sadigh, R. Pedarsani, and Y. P. Fallah, “Social the SVO 0.7 agent demonstrates a safer driving strategy by coordination and altruism in autonomous driving,” IEEE Trans. Intell. 

initiating braking sooner. This suggests that an intermediate Transp. Syst., vol. 23, no. 12, pp. 24791–24804, Dec. 2022. 

\[10\] L. Crosato, H. P. H. Shum, E. S. L. Ho, and C. Wei, “Interaction-aware SVO value can lead to more cautious behavior, allowing the decision-making for automated vehicles using social value orientation,” 

agent to proactively mitigate potential risks, as also seen in IEEE Trans. Intell. Vehicles, vol. 8, no. 2, pp. 1339–1349, Feb. 2023. 

Fig. 7. Finally, Figure 15 shows the spatial trajectories of the

\[11\] A. Balachandran et al., “Human-centric intelligent driving: Collaborat-ing with the driver to improve safety,” Road Vehicle Autom., vol. 9, ego vehicle, pedestrian, and another vehicle under different pp. 85–109, Jul. 2022. 

SVO values \(SVO = 0, 0.7, and 1\). These trajectories show

\[12\] K. Tian et al., “Impacts of visual and cognitive distractions and time the paths each agent takes to reach their intended destinations. 

pressure on pedestrian crossing behaviour: A simulator study,” Accident While the spatial paths are similar across all SVO valuessince Anal. Prevention, vol. 174, Sep. 2022, Art. no. 106770. 

\[13\] W. Liu et al., “A systematic survey of control techniques and applications all agents ultimately reach their goalsthe key differences lie in connected and automated vehicles,” 2023, arXiv:2303.05665. 

in the timing of actions along these trajectories, such as when

\[14\] S. A. Bagloee, M. Tavana, M. Asadi, and T. Oliver, “Autonomous vehi-braking or acceleration occurs. 

cles: Challenges, opportunities, and future implications for transportation policies,” J. Mod. Transp., vol. 24, no. 4, pp. 284–303, Aug. 2016. 

\[15\] H. Taghavifar, C. Wei, and L. Taghavifar, “Socially intelligent rein-VII. CONCLUSION

forcement learning for optimal automated vehicle control in traffic scenarios,” IEEE Trans. Autom. Sci. Eng., early access, Jan. 29, 2024, In this paper, we proposed an innovative MURL archi-doi: 10.1109/TASE.2023.3347264. 

tecture for AV navigation in urban environments using a

\[16\] T. Liu et al., “Heuristics-oriented overtaking decision making for SARSA learning algorithm enriched with a dynamic opti-autonomous vehicles using reinforcement learning,” IET Electr. Syst. 

Transp., vol. 10, no. 4, pp. 417–424, Dec. 2020. 

mization technique and integrating SVO. Our approach

\[17\] Z. Cao et al., “Reinforcement learning based control of imitative policies incorporates individual agents’ social preferences and logistic for near-accident driving,” 2020, arXiv:2007.00178. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:43:43 UTC from IEEE Xplore. Restrictions apply. 





TAGHAVIFAR et al.: BEHAVIORALLY-AWARE MURL WITH DYNAMIC OPTIMIZATION FOR AUTONOMOUS DRIVING

10683

\[18\] C.-J. 

Hoel, 

K. 

Driggs-Campbell, 

K. 

Wolff, 

L. 

Laine, 

and

\[39\] J. Liu, X. Qi, P. Hang, and J. Sun, “Enhancing social decision-making of M. J. Kochenderfer, “Combining planning and deep reinforcement autonomous vehicles: A mixed-strategy game approach with interaction learning in tactical decision making for autonomous driving,” IEEE

orientation identification,” IEEE Trans. Intell. Transp. Syst., vol. 25, Trans. Intell. Vehicles, vol. 5, no. 2, pp. 294–305, Jun. 2020. 

no. 3, pp. 1234–1245, Mar. 2024, doi: 10.1109/TITS.2023.1234567. 

\[19\] B. Andrew and R. S. Sutton, Reinforcement Learning: An Introduction. 

MIT Press, 2018. 

\[20\] J. Wu, Z. Song, and C. Lv, “Deep reinforcement learning based energy-efficient decision-making for autonomous electric vehicle in dynamic Hamid Taghavifar \(Senior Member, IEEE\) is cur-traffic environments,” IEEE Trans. Transp. Electrific., vol. 10, no. 1, rently an Assistant Professor with the Department pp. 875–887, Mar. 2024. 

of Mechanical, Industrial and Aerospace Engineer-

\[21\] C. Zhang, O. Vinyals, R. Munos, and S. Bengio, “A study on overfitting ing, Concordia University, Montreal, Canada. His in deep reinforcement learning,” 2018, arXiv:1804.06893. 

research interests include control theory and applica-

\[22\] P. Hang, C. Lv, Y. Xing, C. Huang, and Z. Hu, “Human-like tions, automated driving, mechatronics, and robotics. 

decision making for autonomous driving: A noncooperative game the-oretic approach,” IEEE Trans. Intell. Transp. Syst., vol. 22, no. 4, pp. 2076–2087, Apr. 2021. 

\[23\] P. Hang, C. Lv, C. Huang, Y. Xing, and Z. Hu, “Cooperative decision making of connected automated vehicles at multi-lane merging zone: A coalitional game approach,” IEEE Trans. Intell. Transp. Syst., vol. 23, no. 4, pp. 3829–3841, Apr. 2022. 

Chuan Hu received the B.S. degree in automo-

\[24\] Z. Huang, J. Wu, and C. Lv, “Driving behavior modeling using natu-tive engineering from Tsinghua University, Beijing, ralistic human driving data with inverse reinforcement learning,” IEEE

China, in 2010, and the Ph.D. degree in mechanical Trans. Intell. Transp. Syst., vol. 23, no. 8, pp. 10239–10251, Aug. 2022. 

engineering from McMaster University, Hamilton, 

\[25\] Z. Huang, H. Liu, J. Wu, and C. Lv, “Conditional predictive behavior Canada, in 2017. He is currently an Associate Pro-planning with inverse reinforcement learning for human-like autonomous fessor at the School of Mechanical Engineering, driving,” IEEE Trans. Intell. Transp. Syst., vol. 24, no. 7, pp. 7244–7258, Shanghai Jiao Tong University, Shanghai, China. 

Jul. 2023. 

His research interests include perception, predic-

\[26\] Z. Wu, F. Qu, L. Yang, and J. Gong, “Human-like decision making tion, decision-making, path planning, motion control for autonomous vehicles at the intersection using inverse reinforcement of intelligent vehicles, eco-driving, human–machine learning,” Sensors, vol. 22, no. 12, p. 4500, Jun. 2022. 

interaction, and shared control. He has published

\[27\] S. Adams, T. Cody, and P. A. Beling, “A survey of inverse reinforcement more than 80 articles in these research areas. He is currently an associate learning,” Artif. Intell. Rev., vol. 55, no. 6, pp. 4307–4346, 2022. 

editor of several leading IEEE TRANSACTIONS/journals. 

\[28\] M. S. Rais, R. Boudour, K. Zouaidia, and L. Bougueroua, “Decision making for autonomous vehicles in highway scenarios using harmonic SK deep SARSA,” Appl. Intell., vol. 53, no. 3, pp. 2488–2505, Feb. 2023. 

Chongfeng Wei \(Member, IEEE\) received the B.S. 

\[29\] C.-C. Lin, K.-Y. Chen, and L.-T. Hsieh, “Real-time charging scheduling degree in computational and applied mathematics of automated guided vehicles in cyber-physical smart factories using and the M.S. degree in vehicle engineering from feature-based reinforcement learning,” IEEE Trans. Intell. Transp. Syst., Southwest Jiaotong University, Chengdu, China, in vol. 24, no. 4, pp. 4016–4026, Apr. 2023. 

2009 and 2011, respectively, and the Ph.D. degree

\[30\] L. Crosato, K. Tian, H. P. H. Shum, E. S. L. Ho, Y. Wang, and in mechanical engineering from the University of C. Wei, “Social interaction-aware dynamical models and decision-Birmingham, Birmingham, U.K., in 2015. He is making for autonomous vehicles,” Adv. Intell. Syst., vol. 6, no. 3, currently a Senior Lecturer \(an Associate Professor\) Mar. 2024, Art. no. 2300575. 

at the University of Glasgow, U.K. His current research interests include decision-making and con-

\[31\] B. Toghi, R. Valiente, D. Sadigh, R. Pedarsani, and Y. P. Fallah, trol of intelligent vehicles, cooperative autonomy, 

“Altruistic maneuver planning for cooperative autonomous vehicles and robotic system dynamics and control. He is serving as an associate editor using multi-agent advantage actor-critic,” 2021, arXiv:2107.05664. 

for several peer-reviewed IEEE journals. 

\[32\] R. Valiente, B. Toghi, R. Pedarsani, and Y. P. Fallah, “Robustness and adaptability of reinforcement learning-based cooperative autonomous driving in mixed-autonomy traffic,” IEEE Open J. Intell. Transp. Syst., vol. 3, pp. 397–410, 2022. 

Ardashir Mohammadzadeh received the B.Sc. 

\[33\] S. Li, K. Peng, F. Hui, Z. Li, C. Wei, and W. Wang, “A decision-making degree from the Sahand University of Technology, approach for complex unsignalized intersection by deep reinforcement Iran, the M.Sc. degree from the K. N. Toosi Univer-learning,” IEEE Trans. Veh. Technol., vol. 73, no. 11, pp. 16134–16147, sity of Technology, Iran, and the Ph.D. degree from Nov. 2024. 

the University of Tabriz. He is currently a Professor

\[34\] R. Valiente, M. Razzaghpour, B. Toghi, G. Shah, and Y. P. Fallah, with the Department of Electrical and Electronics

“Prediction-aware and reinforcement learning-based altruistic coop-Engineering, Sakarya University, Sakarya, Türkiye. 

erative driving,” IEEE Trans. Intell. Transp. Syst., vol. 25, no. 3, His research interests include control theory, fuzzy pp. 2450–2465, Mar. 2024. 

logic

systems, 

machine

learning, 

and

electric

\[35\] NVIDIA Metropolis. Transforming the Future of Mobility at ITS

vehicles. 

America With NVIDIA Metropolis Partners. Accessed: Jun. 13, 2024. 

\[Online\]. Available: https://developer.nvidia.com/blog/transforming-the-future-of-mobility-at-its-america-with-nvidia-metropolis-partners/

\[36\] S. Dereich and T. Müller-Gronbach, “General multilevel adapta-tions for stochastic approximation algorithms of Robbins–Monro and Chunwei Zhang received the degree from Harbin Polyak–Ruppert type,” Numerische Math., vol. 142, no. 2, pp. 279–328, Institute of Technology in 2005. He is currently Jun. 2019. 

the Chair Distinguished Professor and a Ph.D. 

\[37\] X. Kavelaars, J. Mulder, and M. Kaptein, “Bayesian multilevel multivari-Supervisor with Shenyang University of Technology ate logistic regression for superiority decision-making under observable \(SUT\), China. His research interests include struc-treatment heterogeneity,” BMC Med. Res. Methodol., vol. 23, no. 1, tural control, structural health monitoring, AI, smart p. 220, Oct. 2023. 

materials, and structures. 

\[38\] M. Zhang, D. Chu, Z. Deng, and C. Zhao, “Game theory-based lane change decision-making considering vehicle’s social value orientation,” 

SAE, Warrendale, PA, USA, Tech. Rep. 2023-01-7109, 2023. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 02,2025 at 10:43:43 UTC from IEEE Xplore. Restrictions apply.



