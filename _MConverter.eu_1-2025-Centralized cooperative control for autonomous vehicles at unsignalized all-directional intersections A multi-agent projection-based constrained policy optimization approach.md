Downloaded from https://iranpaper.ir

https://www.tarjomano.com

https://www.tarjomano.com

Expert Systems With Applications 267 \(2025\) 126153 

Contents lists available at ScienceDirect

Expert Systems With Applications

journal homepage: www.elsevier.com/locate/eswa

Centralized cooperative control for autonomous vehicles at unsignalized

all-directional intersections: A multi-agent projection-based constrained

policy optimization approach✩

Rui Zhao a

, Kui Wang b

, Yun Li c, Yuze Fan a

, Fei Gao d

, ∗, Zhenhai Gao d

a *College of Automotive Engineering, JiLin University, Changchun, 130025, China* b *School of Mechanical Engineering, Beijing Institute of Technology, Beijing, 10008, China* c *Department of Information and Communications Engineering, Tokyo Institute of Technology, Tokyo 152-8550, Japan* d *State Key Laboratory of Automotive Simulation and Control, Jilin University, Changhun, 130025, China* A R T I C L E

I N F O

A B S T R A C T

*Keywords:*

The interest in real-time cooperative control at urban unsignalized intersections has surged recently, with a Connected and automated vehicles

focus on enhancing the driving safety and traffic throughput for connected and automated vehicles \(CAVs\). 

Safe reinforcement learning

Nonetheless, most existing studies either struggle with computational complexity in high-density traffic Intersection cooperative control

scenarios or fail to ensure robust safety for distributions outside of training. To tackle these issues, this Multi-agent reinforcement learning

study introduces a novel multi-agent Safe Reinforcement Learning framework, SRL-CLCADI, designed for Cross-Constrained Markov Games

Longitudinal cooperative Control of CAVs at All-Directional Intersections. Approaching vehicles communicate their kinematic data to the central controller in real-time, hand over their control authorities, and comply with the instructions from the central controller. Specifically, to address the significant computational challenges of existing optimization control methods and the robust safety issues of deep learning methods in practical applications, we reformulate the intricate multi-objective decision-making process into a model-free Constrained Markov Game and introduce a Multi-Agent Projection-based Constrained Policy Optimization \(MAPCPO\) approach within the framework of safe Reinforcement Learning \(RL\). The policy neural network features an innovative queue-based dynamic state input design to handle dynamic traffic scenarios at intersections, and the MAPCPO method incrementally optimizes updates within the Kullback–Leibler divergence trust region to enhance performance before projecting them onto the safety constraint boundaries to ensure safety. In simulations across various traffic densities at unsignalized intersections, our method significantly outperformed Model Predictive Control and Mixed Integer Programming methods, improving computational efficiency by 72.79% and 63.16%, traffic efficiency by 36.84% and 32.38%, and energy consumption by 8.22% and 5.48%, respectively. Unlike non-safety-aware RL methods, our approach achieved a zero collision rate, also enhancing ride comfort. 

**1. ** **Introduction**

visual obstructions, are notably difficult. Studies indicate that even human drivers find it challenging to navigate these intersections safely

Autonomous driving is growing rapidly and shows excellent applica-

and efficiently, leading to frequent accidents \(Li, Gong, Lu, & Yi, 2021; tion potential in road traffic provides to improve safety, efficiency, and

Zhao, Knoop, & Wang, 2023\).  Therefore, researching safe and efficient comfort \(Hang, Huang, Hu, & Lv, 2022; Hu et al. , 2022; Kuwata et al., 

passage for autonomous vehicles at unsignalized intersections is of

2009; Li, Sun, Cao, He, & Zhu, 2015\). However, due to the intricacy paramount importance for the broader acceptance and adoption of

of the environment and the unpredictability of anticipated vehicular

autonomous driving technology. In recent years, Vehicle-to-Everything

actions, urban settings present significant challenges for autonomous

\(V2X\) communication has significantly addressed the perception limita-

driving. Among these, unsignalized intersections, which converge mul-

tions at these intersections. Vehicle-Infrastructure Collaborative driving

tiple directional lanes and lack traffic signal guidance coupled with

✩ This work was supported by the National Natural Science Foundation of China under Grant 52202495 and Grant 52202494. 

∗ Corresponding author. 

*E-mail* *addresses: *rzhao@jlu.edu.cn \(R. Zhao\), 3120230321@bit.edu.cn \(K. Wang\), li-yun@g.ecc.u-tokyo.ac.jp \(Y. Li\), fanyz23@mails.jlu.edu.cn \(Y. Fan\), 

gaofei123284123@jlu.edu.cn \(F. Gao\), gaozh@jlu.edu.cn \(Z. Gao\). 

https://doi.org/10.1016/j.eswa.2024.126153

Received 11 February 2024; Received in revised form 15 November 2024; Accepted 10 December 2024

Available online 16 December 2024 

0957-4174/© 2024 Elsevier Ltd. All rights are reserved, including those for text and data mining, AI training, and similar technologies. 





Downloaded from https://iranpaper.ir

https://www.tarjomano.com

https://www.tarjomano.com

*R. * *Zhao* *et* *al. *

*Expert* *Systems* *With* *Applications* *267* *\(2025\)* *126153* 

**Fig. ** **1. **Signal-Free Intersection Environment and Vehicle-to-Infrastructure Cooperative Control Method. 

methods for unsignalized intersections, based on V2X communication, 

Game-theory-based control methods are also employed for cooper-

are emerging and represent a significant advancement towards safer

ative control at intersections. Here, vehicles act as strategic players in

and more efficient autonomous intersection management \(Abboud, 

a game seeking to reach Nash equilibria for decision-making. These

Omar, & Zhuang, 2016; Hafner, Cunningham, Caminiti, & Del Vecchio, 

methods simulate interactions between vehicles at unsignalized inter-

2013; Wu, Chen, & Zhu, 2019\). The vehicle-road collaboration process sections, aiming to improve intersection adaptability and efficiency \(Li, 

is depicted in Fig. 1, where each connected and automated vehicle

Yao, Kolmanovsky, Atkins, & Girard, 2020; Tian, Li, Kolmanovsky, 

\(CAV\) periodically engages in wireless communication with roadside

Yildiz, & Girard, 2020\). However, with increasing traffic, the computa-units \(RSUs\) to transmit its dynamic form data. The roadside then

tional load on coordinating servers surges, posing challenges for their

adjusts the flow of vehicles through the intersection based on the application at busy intersections. 

embedded collaborative control policy, affecting various state variables

The rapidly evolving Deep Reinforcement Learning \(RL\) meth-

such as speed, acceleration, and trajectory. The motion control layer of

ods \(Isele, Rahimi, Cosgun, Subramanian, & Fujimura, 2018\) rep-each CAV controls its movement at the intersection in accordance with

resent significant learning-based approaches and have the potential

the decision-making instructions from the roadside. 

to tackle computational demand issues while ensuring excellent in-

Initially, rule-based collaborative control policies were developed. 

tersection control performance. Deep RL studies vehicle-environment

These methods utilized traffic rules engineered to schedule vehicles interactions to learn optimal cooperative control policies at inter-efficiently and orderly. Commonly adopted methods included First

Come, First Serve \(FCFS\) \(Dresner & Stone, 2006; Lukose, Levin, & 

sections by maximizing rewards. Unlike rule-based methods, which

Boyles, 2019; Wu et al. , 2019\), which prioritized vehicles based on their presume a well-understood environment, Deep RL-based techniques

arrival sequence at intersections; Fastest First Service \(FFS\) \(Fajardo, 

train models to map environmental states to actions, adapting to

Au, Waller, Stone, & Yang, 2011\),  which prioritized vehicles according changing conditions. Typical Deep RL algorithms like Proximal Policy

to shorter traversal times; and Long Queue First Service \(LQF\) \(Qian, 

Optimization \(PPO\) \(Guan et al. , 2020\), Deep Deterministic Policy

Altché, Grégoire, & de La Fortelle, 2017\), which aimed to improve Gradient \(DDPG\) \(Antonio & Maria-Dolores, 2022\) and Soft Actor–

intersection throughput by prioritizing the longest queues. While ef-

Critic \(SAC\) \(Al-Sharman et al. , 2023\) are employed for unsignalized fective in simple scenarios, these methods’ limited adaptability and intersection automation training. The reward function balances the

coarse temporal granularity can lead to significant performance issues

scores of performance in safety, comfort, and efficiency. Introducing

in real and complex intersections. Thus, managing intersections with

Deep RL to this domain has yielded promising training outcomes, 

high traffic density and variability effectively remains a challenging addressing computational efficiency in high-traffic scenarios and is-task. 

sues with coarse granularity and suboptimality, yet several challenges

As control optimization control methods have demonstrated out-

remain. 

standing performance, research has been focused on modeling, identify-

First and foremost, single-reward policy updating methods are in-

ing conflict constraints, and coordinating vehicle passages at unsignal-

adequate for safety-critical applications in autonomous driving, where

ized intersections using optimization approaches. The formulation of

Preventing accidents is the premise and foundation for optimizing ride

conflict constraints involves grid-based, point-based, and vehicle-based

comfort and traffic efficiency. Simply combining safety, comfort, and

approaches; then methods like Dynamic Programming \(Guo et al., 

efficiency into one reward function may not correctly prioritize the

2019\), Mixed Integer Programming \(MIP\), Mixed Integer Linear Pro-safety elements for the learning agent. To tackle this, various safe gramming \(MILP\) \(Lu & Kim, 2018\), and Model Predictive Control Deep RL methods, such as the Constrained Policy Optimization algo-

\(MPC\) \(Kamal, Imura, Hayakawa, Ohata, & Aihara, 2014\) have been rithm \(Achiam, Held, Tamar, & Abbeel, 2017\) and the Projection-based used to compute real-time vehicle control commands that meet these

Constrained Policy Optimization algorithm \(Yang, Rosca, Narasimhan, 

constraints. The conflict-tile method \(Bichiou & Rakha, 2018; Dai et al., 

& Ramadge, 2020\), have been proposed. However, these algorithms, in-

2016; Xu, Zhang, Li, & Li, 2019\) prevents collisions by limiting vehicle numbers in designated grid areas, although it may underutilize

cluding their distributed versions, are not yet suitable for real-world de-

space. The conflict-point method \(Kamal et al. , 2014; Mirheli, Ha-

ployment at intersections. Distributed methods lack global awareness, 

jibabai, & Hajbabaie, 2018\) controls vehicles near potential collision potentially leading to safety risks and inconsistent decision-making. 

points, which requires a delicate balance between efficiency and safety. 

Due to the complex nature of coordinating multiple vehicles and the

Vehicle-based methods \(He, Zheng, Lu, & Guan, 2018; Li & Zhang, 

necessity for prompt synchronization, centralized safe reinforcement

2018; Li, Zhang, Zhang, Jia, & Ge, 2018; Mirheli, Tajalli, Hajibabai, 

learning becomes crucial for ensuring traffic safety and efficiency. 

& Hajbabaie, 2019\),  while coordinating vehicles across the whole in-Furthermore, adaptive policy update methods are advised to manage

tersection, may yield less than optimal outcomes due to computational

the complexity of diverse hazardous situations at intersections, striking

intensity. 

a balance between learning efficacy and safety. However, there are

2 





Downloaded from https://iranpaper.ir

https://www.tarjomano.com

https://www.tarjomano.com

*R. * *Zhao* *et* *al. *

*Expert* *Systems* *With* *Applications* *267* *\(2025\)* *126153* 

currently no centralized safe Deep RL extension algorithms available

reward and risk functions. Section 4 offers a detailed exposition on the that adequately fulfill these requirements. 

update process of the SRL-CLCADI algorithm based on the MAPCPO

Secondly, the use of static input neural networks in developing

algorithm. Section 5 evaluates the performance of various control multi-vehicle cooperative control policies poses significant challenges

algorithms within training scenarios. Lastly, Section 6 concludes the to effective continuous learning. Limiting the input quantity results in

paper and discusses future research directions and prospects. 

shortened episodes, complicating the application in real-world intersec-

tions where traffic flow is continuous. Increasing the input quantity, on

**2. ** **Problem** **definition** **and** **method** **framework** the other hand, leads to an excessive number of network parameters, 

making learning more difficult. Additionally, the inclusion of blank *2.1. * *Problem* *definition*

feature inputs from vehicles that have already passed adversely impacts

the model’s ability to understand and learn. 

The scenario of an unsignalized road intersection, as shown in

Thirdly, regarding training scenarios, current intersection cooper-

Fig. 1,  represents a standard four-way intersection with several lanes. 

ative control methods based on Deep RL often assume the presence

The intersection is systematically divided into two distinct areas: the

of specific-direction turn lanes \(SDTL\), a presumption that does not control area and the departure area. The intersection control system

match many real-world scenarios, thereby limiting the ability to effec-

exerts lateral and longitudinal cooperative control over CAVs within a

tively manage intersection traffic. Moreover, employing discontinuous

specified distance from the entrance of the intersection \(i.e., the control

episodic settings, where new episodes begin at initialized positions, is

area\). CAVs approaching an intersection are capable of maneuvers in

not conducive to policy applications in intersections with continuous

any direction: proceeding straight, turning right, or turning left, and

traffic flow. 

are permitted to change lanes at any time, provided they adhere to

Fourthly, existing Deep RL or other methodologies have not yet

traffic regulations. All potential vehicle conflict relationships can be

integrated lateral vehicle control, focusing solely on the longitudinal

categorized into three types: crossing conflicts, merging conflicts, and

control of vehicles. This limitation restricts the potential for optimiz-

diverging conflicts. Each CAV *𝑖 * transmits dynamic data in real-time ing traffic flow, as comprehensive control over both longitudinal and

⎡ *𝑥𝑖 *⎤

lateral movements is crucial for enhancing overall traffic efficiency and

⎢ *𝑦𝑖 *⎥

safety. 

⎢

⎥

*𝑠𝑖 *= ⎢ *𝑣𝑖 *⎥

This paper proposes a novel multi-agent Safe Reinforcement Learn-

⎢ *𝜄𝑖 *⎥

ing framework designed for Cross-Longitudinal coordination Control

⎢

⎥

⎣ *𝜅𝑖 *⎦

of CAVs within All-Directional Intersections \(SRL-CLCADI\), thereby

addressing the previously identified deficiencies. 

to vehicle-road cooperative control system via V2I wireless communi-

The primary contributions of this paper can be summarized as:

cation. Here, \{ *𝑥𝑖, * *𝑦𝑖*\} ∈

*𝑡*

*𝑡*

R × R represents the CAV’s position coordinates

\(1\) Firstly, we formulate the cross-longitudinal cooperative control

at time step *𝑡*; *𝑣𝑖 * denotes the velocity, *𝜄𝑖 *∈  ∶= \{left *, * straight *, * right\}

*𝑡*

*𝑡*

process of CAVs at intersections with all-directional turn lanes \(ADTL\)

indicates the anticipated direction of travel at the intersection; *𝜅𝑖 *∈ R\+

into a model-free Constrained Markov Game \(CMG\), an extension

represents the sum of the communication delay time from CAV to RSU

of standard Markov Game \(MG\), with embedded safety constraints

and from RSU to CAV at last time step. Influenced by factors such as

restricting the set of acceptable policies. The improved Impact Reg-vehicle speed, distance to RSU and flow density, communication delay

ularization \(IR\) for cooperative control reward and cost functions is

times dynamically change in real-time. 

employed, with the goal of preventing irreversible or harmful changes

Equipped with the safety-aware multi-agent deep reinforcement

to the environment caused by CAVs when their actions deviate from a

learning algorithm SRL-CLCADI, the centralized cooperative control

baseline state. Additionally, the definition of the state space takes into

system modulates the timing of CAVs traversing road intersections by

account communication delays, closely mirroring real-world scenarios. 

realtime control of each CAV’s speed *𝑣𝑖 *∈ \[ *𝑣* min *, * *𝑣* max\] and steering \(2\) Secondly, we introduce a centralized Multi-Agent Projection-angle variation *𝛥𝜓𝑖 *∈ \[ *𝜓* min *, * *𝜓* max\], where *𝑣* min and *𝑣* max represent based Constrained Policy Optimization algorithm \(MAPCPO\) to solve

the minimum and maximum velocities, *𝜓* min and *𝜓* max represent the the CMG problem. This method incorporates safety constraints to fur-minimum and maximum steering angle, respectively. Subsequently, the

ther constrain the trust region formed by Kullback–Leibler \(KL\) di-

motion control layer of each CAV is capable of generating the required

vergence, thereby facilitating policy updates that maximize perfor-

throttle opening and brake pad force for longitudinal control of the

mance while keeping constraint costs within their specified limits

CAV. The unaltered steering angle *𝜓𝑖 * is determined by advanced trajec-across different quantified safe levels. 

tory planning and trackers based on the CAV’s positional coordinates. 

\(3\) Thirdly, we design the policy neural network architecture, aim-

The true steering angle *𝜓*′ *𝑖 *= *𝜓𝑖 *\+ *𝛥𝜓𝑖 * is then derived by adding ing to enhance control performance and flexibility. The policy input

the steering angle variation to this, allowing the CAV to maintain utilizes an innovative queue-based dynamic update mechanism to han-its original trajectory as much as possible while also possessing the dle dynamic traffic scenarios at intersections. The network neurons

capability to avoid collisions through lateral movement. 

employ Long Short-Term Memory \(LSTM\) units, enhancing its ability

to capture vehicular social interactions and historical state information. 

*2.2. * *Method* *framework*

The policy output encompasses coupled lateral and longitudinal control

of CAVs, providing a broader space for optimization control. 

The proposed SRL-CLCADI method sets up three neural networks:

\(4\) Extensive simulation across various traffic densities at unsignal-

the centralized policy neural network, along with the reward and safety

ized intersections is conducted and comparisons with classical con-

cost value neural networks. The policy network is employed to map the

trol methods Vehicle-Intersection Coordination Scheme \(VICS\) \(Kamal

local states of all vehicles at the current time step to the joint action

et al., 2014\),  Mixed integer programming based Intersection Coor-probability distribution of the vehicles at the next time step, while the

dination Algorithm \(MICA\) \(Lu & Kim, 2018\) and non-safety aware reward and safety cost-based value networks are used to evaluate the

RL method Model Accelerated Proximal Policy Optimization \(MAPPO\)

expected performance reward and safety cost under the current policy. 

\(Guan et al., 2020\),  showcasing the superiority of our method. 

Fig. 2 illustrates the SRL-CLCADI method framework, comprising the The structure of this paper is organized as follows: Section 2 pro-Sampler Module and Learner Module. 

vides an overview of the algorithmic framework of the SRL-CLCADI al-

The task of the SRL-CLCADI sampler is to acquire updated neu-

gorithm. In Section 3,  we present the design aspects of the SRL-CLCADI ral parameters for the policy and value networks, and then to use algorithm, including the state space, action space, and the design of

these parameters to sample experience data from the road intersection

3 





Downloaded from https://iranpaper.ir

https://www.tarjomano.com

https://www.tarjomano.com

*R. * *Zhao* *et* *al. *

*Expert* *Systems* *With* *Applications* *267* *\(2025\)* *126153* 

**Fig. ** **2. **Structure of the proposed vehicle-road cooperative control system based on SRL-CLCADI, comprised of two parts — Sampler and Learner, designed for the monotonic improvement of intersection throughput performance including safety, efficiency, and comfort, while concurrently satisfying safety cost constraints. The SRL-CLCADI structural framework diagram encompasses three neural networks: the policy neural network, the reward value neural network, and the safety costs value neural network. The Sampler module is responsible for interacting with the environment, collecting state space data from it, and obtaining action space data from the policy neural network. The Learner module is tasked with updating the parameters of three neural networks based on the collected data and two evaluation functions in the update method. 

**Fig. ** **3. **Structural Framework of the CMG. 

environment. This module employs a safe multi-agent RL formula-

*3.1. * *Safe* *multi-agent* *reinforcement* *learning* *formulation* tion, CMG, to formally articulate the exploration process of multiple

CAVs with safety constraints within the intersection cooperative control

By incorporating additional constraints to the traditional MG, a

system environment. This process subsequently produces discrete time-

CMG model is constructed, which is then used for the safe multi-agent

series trajectory data, which includes states, actions, rewards, and RL problem, as depicted in Fig. 3.  The CMG model is defined as a tuple safety costs. This data provides the basis for optimizing the policy \( *, * *, * *, * *𝑃* *, * *𝑅, * *𝐶* *, * *𝜌* 0 *, * *𝛾*\), where: neural network and the reward and cost value neural networks. 

The SRL-CLCADI learner works in conjunction with the sampler, uti-

•  = \{1 *, *… *, * *𝑛*\} represents a set of *𝑛 * agents; 

∏ *𝑛*

lizing the data collected by the sampler to update the policy and value

• *𝑆 *=

*𝑆𝑖 * denotes the global state space, which is the cartesian

*𝑖*=1

neural networks. It then synchronizes the updated parameters with the

product of the state spaces of each agent *𝑖*; 

∏ *𝑛*

sampler to facilitate the next iteration of sampling and optimization in a

• ** **=

*𝐴𝑖 * represents the global action space, which is the

*𝑖*=1

cyclical process until the desired traffic performance at the intersection

cartesian product of the action spaces of each agent, where the

is reached. This module employs a MAPCPO method that solves the

agents perform the joint action *𝐴𝑡 *= \( *𝑎* 1 *, * *𝑎* 2 *, *… *, * *𝑎𝑛*\) at the discrete *𝑡*

*𝑡*

*𝑡*

CMG problem by incorporating safety costs-constrained into the trust

time step *𝑡*; 

region formed by KL divergence. It first maximizes the policy reward

• *𝑃 *∶ *𝑆 *× ** **× *𝑆 *→ \[0 *, * 1\] denotes the state transition probability value, then projects the policy into the constrained range of safety costs

function from a state *𝑠𝑡 *∈ *𝑆 * and joint action *𝑎𝑡 *∈ ** **to the next to realize a safe and efficient policy, aiming to optimize intersection

state *𝑠𝑡*\+1 ∈ ; 

cooperative control performance while ensuring that the constrained

• *𝑅 *∶  × ** **→ R represents the joint reward function; 

safety costs remain within predefined boundaries. 

• ***𝑪 ***= \{ *𝐶𝑖*\} *𝑖*∈ denotes the set of safety cost functions for the *𝑗 𝑗*≤ *𝑚𝑖*

agents *𝑐𝑖 *∶  × **** *𝑖 *→

cost functions\), 

*𝑗*

R \(each agent has *𝑁 𝑖𝑗*

**3. ** **Sampler** **module** **following** **the** **CMG** **formulation** with the corresponding safety cost constraint values represented

by ***𝒅 ***= \{ *𝑑𝑖 *\} *𝑖*∈

; 

*𝑗 * 1

This section introduces a safe Multi-Agent Deep Reinforcement

≤ *𝑗*≤ *𝑚𝑖*

• *𝜌* 0 ∶ *𝑆 *→ \[0 *, * 1\] is the starting state distribution; Learning \(MADRL\) formulation, namely CMG, and transforms the

• *𝛾 *∶ *𝑆 *→ \[0 *, * 1\] is the discount factor. 

unsignalized Intersection Control issue into a CMG problem by defining

the fundamental elements of CMG, including the global state space, 

According to the CMG model, agents interact with the environment

joint action space, joint reward function, and a series of safety cost

in discrete time steps. At each time step *𝑡*, agents receive all the functions for CAVs to safely share the road with each other. This process

information of the current state *𝑠𝑡 *∈ ** **of the environment, with each yields discrete time-series trajectory data, including states, actions, agent performing an action ***𝒂**𝑡 *= \( *𝑎* 1 *, *… *, * *𝑎𝑛*\). After all agents have taken *𝑡*

*𝑡*

rewards, and safety costs, used for optimizing the policy, reward value, 

their joint actions, they receive a joint reward *𝑅*\( *𝑠𝑡, **𝒂**𝑡*\), and each incurs and safety cost neural networks. 

their respective costs *𝐶𝑖*\( *𝑠*

\) *, *∀ *𝑗 *= 1 *, *… *, * *𝑚𝑖*. The environment then *𝑗*

*𝑡, * *𝑎𝑖𝑡*

4 





Downloaded from https://iranpaper.ir

https://www.tarjomano.com

https://www.tarjomano.com

*R. * *Zhao* *et* *al. *

*Expert* *Systems* *With* *Applications* *267* *\(2025\)* *126153* 

**Table** **1**

Global state space and joint action space. 

Notation

Description

Data format

Range

*𝑑𝑖*

The distance of vehicle *𝑖 * from the target location

\[ *𝑓* *𝑙* *𝑜𝑎𝑡*\]

\[0, 15\] m

*𝑣𝑖*

Current velocity of vehicle *𝑖*

\[ *𝑓* *𝑙* *𝑜𝑎𝑡*\]

\[0, 10\] m/s

*𝜁 𝑖*

Current lane of vehicle *𝑖*

\[ *𝑏𝑜𝑜𝑙 , * *𝑏𝑜𝑜𝑙 , *… *, * *𝑏𝑜𝑜𝑙 , *…\]

0 or 1

1

2

*𝑙*

*𝑙𝑖*

Current driving direction of vehicle *𝑖*

\[ *𝑏𝑜𝑜𝑙 , * *𝑏𝑜𝑜𝑙 , * *𝑏𝑜𝑜𝑙 *\]

0 or 1

0

1

2

*𝜅𝑖*

The sum of the bidirectional communication delay time

\[ *𝑓* *𝑙* *𝑜𝑎𝑡*\]

\(0, \+∞\) s

*𝑣*′ *𝑖*

Expected velocity of vehicle *𝑖*

\[ *𝑓* *𝑙* *𝑜𝑎𝑡*\]

\[2, 10\] m/s

*𝜓 *′ *𝑖*

Expected steering angle of vehicle *𝑖*

\[ *𝑓* *𝑙* *𝑜𝑎𝑡*\]

\[−0.65, 0.65\] rad

transitions to a new state *𝑠𝑡*\+1 with probability *𝑃 *\( *𝑠𝑡*\+1| *𝑠𝑡, * *𝑎𝑡*\). RL utilizes sample trajectory data obtained from multi-agent interactions with the

environment. The purpose of RL is to teach agents to learn a policy *𝜋*

that maximizes the expected return of rewards. 

\[

\]

∞

∑

*𝐽 *\( *𝜋*\) = E

*𝛾𝑡𝑅*\( *𝑠*

\(1\)

*𝑠* 0∼ *𝜌* 0 *, **𝒂***∼ *𝜋* *,𝑠* 1∶∞∼ ***𝑷***

*𝑡, **𝒂**𝑡*\)

*𝑡*=0

Simultaneously, it also needs to satisfy the expected discounted return

*𝐽 *\( *𝜋*\) for each safety cost function *𝐶𝑖 * under the threshold *𝑐𝑖 *: *𝑐𝑖*

*𝑗*

*𝑗*

*𝑗*

\[

\]

∞

∑

*𝐽 *\( *𝜋*\) =

*𝛾𝑡𝐶𝑖*\( *𝑠 , **𝒂 ***\)

∀ *𝑖 *= 1 *, *… *, * *𝑚*; *𝑗 *= 1 *, *… *, * *𝑛*

*𝐶𝑖*

E *𝑠*

*𝑡*

*𝑡*

≤ *𝑑𝑖*

*𝑗*

0 ∼ *𝜌* 0 *, **𝒂***∼ *𝜋* 

*,𝑠* 1∶∞∼ ***𝑷***

*𝑗*

*𝑗*

*𝑡*=0

\(2\)

*3.2. * *Representing* *the* *collaborative* *control* *problem* *of* *CAVs* *as* *a* *safe* *MARL* *formulation* *in* *CMG*

*3.2.1. * *State* *space* *and* *joint* *action* *space* The global state space is used to describe the observation information during the interaction between multi-agent and the environment. 

**Fig. ** **4. **The intuitive representation of the subitems characterizing intersection through-A reasonable state space is crucial for efficient RL. For the MADRL-

put performance in the reward and cost functions. 

based vehicle-road cooperative control system, the ability to effectively

extract and reconstruct observation information from the vehicle driv-

ing environment in highly complex and dynamic road intersections

action space is established as the ordered concatenation of each CAV’s

determines its capability to accurately output appropriate actions \(see

∏

action ***𝑨 ***=

*𝑛*

***𝑨**𝑖*, with the action space is defined as ***𝑨**𝑖 *= \[ *𝑣*′ *𝑖, * *𝛥𝜓𝑖*\]. 

Table 1\). 

*𝑖*=1

The motion control layer of each CAV generates acceleration throttle

To align with the realistic and complex scenario of randomized free

opening and deceleration braking force to control the longitudinal

movement of vehicles at road intersections, the state space compre-

movement of the CAV based on the desired speed provided by the

hensively considers both the fluid characteristics of the intersections

vehicle-road cooperative control system. Additionally, it combines the

and the randomness of vehicle driving paths. In this work, the state

∏

steering angle differential information provided by the system with the

space is defined as ** **= \[

*𝑛*

\( *𝑑𝑖, * *𝑣𝑖, * *𝜁 𝑖, * *𝜄𝑖, * *𝜅𝑖*\)\]. Here, *𝑑𝑖 * represents *𝑖*=1

current steering angle of the CAV for lateral control. 

the distance that the CAV *𝑖 * needs to travel to leave the intersection, *𝑣𝑖 * denotes its real-time speed, *𝜁 𝑖 * represents the road information for CAV *𝑖 * where each lane of every road occupies a distinct indicator *3.2.2. * *Reward* *function* *and* *safety* *cost* *function* position, employing one-hot encoding, *𝜄𝑖 * indicates the driving direction Reward and safety cost functions serve as the quantitative feedback

of agent *𝑖*, including left-turn, straight, and right-turn, also using one-received by multi-agent systems from the environment following the

hot encoding where each direction occupies a distinct indicator position

execution of joint actions. These functions guide agents in persis-

and *𝜅𝑖 * indicates the bidirectional communication delay. The initial tently learning policies focused on maximizing rewards within cost

value of *𝜅𝑖 > * 0 for each vehicle is set to *𝜅𝑖, * 0. The velocity, turning constraints, thereby progressively enhancing the asymptotic perfor-information and communication delay information from the previous

mance and convergence speed of reinforcement learning algorithms. 

time step of the CAV are transmitted in real-time to the road segment by

We have comprehensively and finely designed the reward and safety

the CAV, while the distance information and lane data are calculated in

cost functions for vehicle-road cooperative control system based on, 

real-time based on the coordinates sent by the CAV. By combining the

thereby achieving safe, efficient, and comfortable passage for multiple

information \( *𝑑𝑖, * *𝜁 𝑖, * *𝜄𝑖*\), the specific position of a CAV at an intersection CAVs at intersections. 

can be encoded. The aforementioned state space representation is ca-

In traditional RL methods, reward functions are instrumental in

pable of adapting to complex and random intersection traffic scenarios, 

guiding agents towards achieving predefined objectives. However, 

effectively and dynamically characterizing the variable number of pass-

these methods frequently fail to account for the intricate nuances

ing CAVs, diverse traffic intentions, and dynamic motion information

present in complex real-world situations. This oversight can inadver-

at the intersection. 

tently prompt agents to exhibit behaviors that were not intended, 

The action space mapped by the policy neural network is the action

favor less-than-ideal solutions, or even compromise the integrity of command explored by CAVs in a complex intersection environment. 

the system in an effort to maximize the specified rewards. To address

This algorithm achieves coordinated passage of CAVs through real-time

these challenges and instill finer-grained behaviors or constraints, we

control of the expected speed *𝑣*′ *𝑖 * and steering angle variation *𝛥𝜓𝑖 * of introduce the principle of reward regularization. By augmenting the

CAVs in next time steps. Similar to the global state space, the joint

original reward signal with penalty values from a safety cost function, 

5 





Downloaded from https://iranpaper.ir

https://www.tarjomano.com

https://www.tarjomano.com

*R. * *Zhao* *et* *al. *

*Expert* *Systems* *With* *Applications* *267* *\(2025\)* *126153* 

our objective is to not only guide the agent towards primary safety

where the Boolean variable *𝜀𝑐* *𝑜𝑙* *𝑙* *𝑖𝑠𝑖𝑜𝑛*

indicates the presence of a

*𝑡,𝑖,𝑖*′

goals but also to comply with secondary criteria that ensure efficiency

collision between CAV *𝑖 * and CAV *𝑖*′ at time step *𝑡*. If a collision occurs, and comfort. This method is really effective for dealing with different

*𝜀𝑐* *𝑜𝑙* *𝑙* *𝑖𝑠𝑖𝑜𝑛*

is set to 1; otherwise, it is set to 0. 

*𝑡,𝑖,𝑖*′

situations and problems in smart transportation systems and other

The total cost function ***𝑪**𝑡𝑜𝑡𝑎𝑙 * is defined as the sum of the dense cost systems that have a bunch of performance needs. 

sub-items ***𝑪**𝑐* *𝑙* *𝑜𝑠𝑒*, ***𝑪**𝑠𝑘𝑖𝑑*, and the sparse cost sub-item ***𝑪**𝑐* *𝑜𝑙* *𝑙* *𝑖𝑠𝑖𝑜𝑛*: In the design of integrated reward and cost functions, indifference

***𝑪**𝑡𝑜𝑡𝑎𝑙 *= *𝛿𝑟**𝑪**𝑐* *𝑙* *𝑜𝑠𝑒 *\+ *𝛿𝑐**𝑪**𝑠𝑘𝑖𝑑 *\+ *𝛿𝑠**𝑪**𝑐* *𝑜𝑙* *𝑙* *𝑖𝑠𝑖𝑜𝑛*

\(6\)

points are often difficult to determine. The selection of coefficients for

various performance sub-items is usually dependent on the designer’s

where *𝛿𝑟*, *𝛿𝑐 * and *𝛿𝑠 * refer to the hyper-parameters to balance the safety personal preferences, making it challenging to balance relationships

factor. In SRL-CLCADI system, we use MAPCPO to measure the global

among multiple performance metrics. Additionally, reward functions

influence on the environment caused by multiple CAVs. Such a factor

that are overly optimized for a specific scenario may lead to overfitting

is optimized via a separate safety cost value neural network. 

problems, rendering the trained model less adaptable to new scenarios. 

This paper aims to avoid any form of shaping rewards, which

As a general rule, it is better to design performance metrics according to

include guidance on behaviors that deviate from merely measuring

what one actually wants to be achieved in the environment, rather than

expected outcomes, in order to prevent agents from learning poten-

according to how one thinks the agent should behave. Therefore, this

tially risky behaviors \(Hu et al., 2020\).  To comprehensively depict the study separately considers the cost sub-items arising from violations of

environment, the reward function emphasizes on holistically improving

safety distances ***𝑪***

traffic efficiency, ride comfort, adherence to the original trajectory, and

*𝑐* *𝑙* *𝑜𝑠𝑒*, safety skidding events ***𝑪 **𝑠𝑘𝑖𝑑 *, and safety collision events ***𝑪***

safety at intersections. 

*𝑐* *𝑜𝑙* *𝑙* *𝑖𝑠𝑖𝑜𝑛*. They reflect the true utility function *𝐽𝐶 *\( *𝜋*\) without *𝑖,𝑗*

intermediate shaping factors, as shown in Fig.  4. The first two are For the traffic efficiency sub-component ***𝑹**𝑒𝑓* *𝑓* *𝑖𝑐* *𝑖𝑒𝑛𝑡*, we linearly in-dense cost evaluation items triggered at each time step, while the last

crease the dense reward *𝛿𝑣𝑣𝑖*\( *𝑡*\) corresponding to each CAV’s speed and is a sparse cost evaluation item triggered by each event or specific subtract the time-intensive dense reward *𝛿𝑡 * at each time step. Addi-occurrence, representing a delayed value that encapsulates the global

tionally, when a CAV successfully navigates through an intersection, 

collision of the entire event. 

we augment the sparse reward by a value of *𝛿𝑝*, and when all CAVs

pass through the intersection smoothly, we increase the sparse reward

In the traffic environment, when the Time to Collision \(TTC\) be-

by a value of *𝛿*′ . The reward sub-component ***𝑹***

tween any two vehicles with potential collision risk falls below the *𝑝*

*𝑒𝑓* *𝑓* *𝑖𝑐* *𝑖𝑒𝑛𝑡 * can be expressed

as:

preset safety threshold ***𝒕**𝑠 * at a given time step, the value of the cost

∑ *𝑛*

∑

∑

*𝑛*

∑

sub-item ***𝑪**𝑟𝑖𝑠𝑘 * can be calculated as

***𝑹**𝑒𝑓* *𝑓* *𝑖𝑐* *𝑖𝑒𝑛𝑡 *=

*𝛿𝑣𝑣𝑖*\( *𝑡*\) −

*𝛿𝑡 *\+

*𝜀𝑝𝑎𝑠𝑠* \_ *𝑠𝑖𝑛𝑔* *𝑙* *𝑒 𝛿*

\(7\)

*𝑖*

*𝑝 *\+ *𝜀𝑝𝑎𝑠𝑠* \_ *𝑎𝑙* *𝑙𝛿*′ *𝑝*

∑ *𝑛*

∑ *𝑛*−1

∑

*𝑡*=1 *𝑖*=1

*𝑡*=1

*𝑖*=1

***𝑪**𝑐* *𝑙* *𝑜𝑠𝑒 *=

*𝜀𝑐* *𝑙* *𝑜𝑠𝑒*

\(3\)

*𝑡,𝑖,𝑖*′

where the Boolean variable *𝜀*

= 1 indicates that CAV *𝑖 * passes

*𝑡*=1 *𝑖*=1 *𝑖*′≠ *𝑖*

*𝑝𝑎𝑠𝑠* \_ *𝑠𝑖𝑛𝑔* *𝑙* *𝑒𝑖*

successfully, and *𝜀𝑝𝑎𝑠𝑠* \_ *𝑎𝑙* *𝑙 *= 1 indicates that all CAVs pass successfully. 

where the Boolean variable *𝜀*

where the Boolean variable *𝜀𝑝𝑎𝑠𝑠* \_ *𝑠𝑖𝑛𝑔* *𝑙* *𝑒 *= 1 indicates that CAV *𝑖 * passes *𝑐* *𝑙* *𝑜𝑠𝑒*

indicates the presence of a collision

*𝑖*

*𝑡,𝑖,𝑖*′

risk between CAV *𝑖 * and CAV *𝑖*′ at time step *𝑡*. The calculation of successfully, and *𝜀𝑝𝑎𝑠𝑠* \_ *𝑎𝑙* *𝑙 *= 1 indicates that all CAVs pass successfully. 

distance and TTC takes into account three different scenarios. Initially, 

Moreover, the speed difference \(i.e., acceleration\) between adjacent

for vehicles not yet within the intersection area and traveling on the

time steps of the CAV is used to quantify the occupant comfort reward

same lane, the focus is on longitudinal safety. distance *𝑑*

sub-item ***𝑹**𝑐* *𝑜𝑚𝑓* *𝑜𝑟𝑡*:

*𝑖,𝑖*′ = | *𝑥𝑖 *− *𝑥𝑖*′ |. 

*𝑑*

∑ *𝑛*

∑ |

The longitudinal TTC is *𝑇* *𝑇* *𝐶*

*𝑖,𝑖*′

| *𝑣𝑖*\( *𝑡*\) − *𝑣𝑖*\( *𝑡 *− 1\)||

*𝑙* *𝑜𝑛 *=

, where *𝑣*

*𝑣*

*𝑥,𝑖 * and *𝑣𝑥,𝑖*′ represent

***𝑹***

*𝛿*

\(8\)

*𝑥,𝑖 *− *𝑣𝑥,𝑖*′

*𝑐* *𝑜𝑚𝑓* *𝑜𝑟𝑡 *=

*𝑎*

*𝜏*

the longitudinal speeds of vehicles *𝑖 * and *𝑖*′, respectively. If the vehicles *𝑡*=1 *𝑖*=1

are on different lanes before entering the intersection, emphasis shifts

where *𝛿𝑎 * represents the score weight of this item and *𝜏 * represents the to the lateral safety distance *𝑑𝑖,𝑖*′ = | *𝑦𝑖 *− *𝑦𝑖*′ |, with the lateral TTC

time interval between two time steps. 

*𝑑*

defined as *𝑇* *𝑇* *𝐶*

*𝑖,𝑖*′

The reward function incorporates a trajectory tracking reward. The

*𝑙* *𝑎𝑡 *=

, where *𝑣*

*𝑣*

*𝑦,𝑖 * and *𝑣𝑦,𝑖*′ denote the lateral

*𝑦,𝑖 *− *𝑣𝑦,𝑖*′

speeds of vehicles *𝑖 * and *𝑖*′, respectively. Upon a vehicle’s entry into the policy neural network coordinates both the lateral and longitudinal

intersection area, the distance calculation must consider both lateral

controls of each vehicle to allow them to pass through intersections

√

and longitudinal components, where *𝑑*

comfortably and efficiently without collisions. Given that the policy *𝑖,𝑖*′

=

\( *𝑥𝑖 *− *𝑥𝑖*′ \)2 \+ \( *𝑦𝑖 *− *𝑦𝑖*′ \)2. 

*𝑑*

neural network has the authority to control the steering angle of the

The corresponding TTC is then established as *𝑇* *𝑇* *𝐶*

*𝑖,𝑖*′

*𝑐* *𝑜𝑟 *=

, where

*𝑣𝑖*− *𝑣𝑖*′

vehicle, it is imperative to add a reward ***𝑹***

*𝑣*

*𝑑* *𝑒𝑣𝑖𝑎𝑡𝑖𝑜𝑛*, to ensure that the

*𝑖 * and *𝑣𝑖*′ denote the speeds of vehicles *𝑖 * and *𝑖*′ along their respective vehicle adheres as closely as possible to the trajectory dictated by the

directions of travel. If there is any situation where the TTC is below the

higher-level autonomous driving decision. Assuming that at time step *𝑡*, threshold, the risk indicator *𝜀𝑐* *𝑙* *𝑜𝑠𝑒,𝑡,𝑖,𝑖*′ is set to 1. Otherwise, *𝜀𝑐* *𝑙* *𝑜𝑠𝑒,𝑡,𝑖,𝑖*′ is the CAV’s steering angle following the higher-level autonomous driving

set to 0. 

decision is *𝜗 * and the steering angle controlled by the policy neural After a skid occurs, the value of the cost sub-item ***𝑪**𝑠𝑘𝑖𝑑 * can be network is *𝜗*′, the trajectory tracking reward is defined as:

calculated:

*𝑇*

∑ *𝑛*

∑

∑ *𝑛*

∑ *𝑛*−1

∑

***𝑹***

|

|

*𝑑* *𝑒𝑣𝑖𝑎𝑡𝑖𝑜𝑛 *= −

*𝛿𝑑 *| *𝜗𝑖 *− *𝜗*′ *𝑖*|

\(9\)

***𝑪**𝑠𝑘𝑖𝑑 *=

*𝜀𝑠𝑘𝑖𝑑*

\(4\)

*𝑡*=1 *𝑖*=1

*𝑡,𝑖,𝑖*′

*𝑡*=1 *𝑖*=1 *𝑖*′

The safety reward sub-item ***𝑹**𝑠𝑎𝑓* *𝑒𝑡𝑦 * is quantified directly by the negative value of the cost function ***𝑪***

Here, *𝜀*

*𝑡𝑜𝑡𝑎𝑙 *. In summary, the total reward

*𝑠𝑘𝑖𝑑*

is a Boolean variable representing whether a CAV under-

*𝑡,𝑖,𝑖*′

function ***𝑹**𝑡𝑜𝑡𝑎𝑙 * can be articulated as:

goes sideslip. When *𝑣* 2 *> * *𝐹*

2 *𝑟*

*𝑓 * indicates that the CAV is experiencing

***𝑹***

sideslip, *𝜀*

*𝑡𝑜𝑡𝑎𝑙 *= ***𝑹**𝑒𝑓* *𝑓* *𝑖𝑐* *𝑖𝑒𝑛𝑡 *\+ ***𝑹**𝑐* *𝑜𝑚𝑓* *𝑜𝑟𝑡 *\+ ***𝑹**𝑑* *𝑒𝑣𝑖𝑎𝑡𝑖𝑜𝑛 *\+ ***𝑹**𝑠𝑎𝑓* *𝑒𝑡𝑦*

\(10\)

*𝑠𝑘𝑖𝑑*

is set to 1, otherwise it is 0. The turning radius *𝑟 * of the

*𝑡,𝑖,𝑖*′

CAV, calculated from the vehicle’s current steering angle, represents

the vehicle’s maneuverability, while *𝐹𝑓 * signifies the maximum friction **4. ** **Learner** **module** **based** **on** **safety** **situation** **awareness** **MAPCPO**

force that the CAV’s tires can provide. 

Then, the value of the cost sub-item ***𝑪***

The SRL-CLCADI learner operates in parallel with the sampler, 

*𝑐* *𝑜𝑙* *𝑙* *𝑖𝑠𝑖𝑜𝑛 * can be calculated:

*𝑛*

∑ *𝑛*−1

∑

utilizing the data collected from the sampler to update both the pol-

***𝑪**𝑐* *𝑜𝑙* *𝑙* *𝑖𝑠𝑖𝑜𝑛 *=

*𝜀𝑐* *𝑜𝑙* *𝑙* *𝑖𝑠𝑖𝑜𝑛*

\(5\)

icy and the value neural networks. Subsequently, it synchronizes the

*𝑡,𝑖,𝑖*′

*𝑖*=1

*𝑖*

6 





Downloaded from https://iranpaper.ir

https://www.tarjomano.com

https://www.tarjomano.com

*R. * *Zhao* *et* *al. *

*Expert* *Systems* *With* *Applications* *267* *\(2025\)* *126153* 

**Fig. ** **5. **Policy neural network structure diagram. 

**Fig. ** **6. **LSTM unit structure diagram. 

updated parameters back to the learner, preparing for the next epoch

of CAVs. This requirement is pivotal as the maximum learning capacity

of sampling and optimization. This iterative process continues until of the policy directly sets the performance boundaries for collaborative

the desired performance in intersection traffic is achieved. This section

control in intersection scenarios. To effectively address this challenge, 

describes the core methodology of the learner module for addressing

the SRL-CLCADI approach integrates LSTM neural network structures

the CMG problem, including the design of the DRL network architecture

into the policy neural network, thereby enhancing its capability to with one actor and two critics, and the Safety Situation Awareness process and learn from the complex and dynamic information associ-Projection-based Multi-Agent Constrained Policy Optimization Method-

ated with CAVs. As shown in Fig. 5, the structure of the policy neural ology. 

network consists of a state encoder and a decoder. The main function

of the encoder, which is composed of multiple LSTM units, is to model

*4.1. * *DRL* *architecture* *design*

the current dynamic information of the vehicles. The primary function

of the decoder is to adjust the range of the output tensor from the state

The SRL-CLCADI system comprises three neural networks: the policy

encoder. Due to the small range of changes in the tensor output by the

neural network, the reward value neural network, and the cost value

LSTM, it is not conducive to capturing the differences before and after

neural network. The policy neural network is responsible for providing

the policy update in safe RL. This also leads to a slow speed of the agent

collaborative control decision-making for CAV passing through the

in exploring the action space, ultimately resulting in a high time cost

intersection, mapping the local states of all CAVs at the current time

in learning effective policies. Therefore, a range adjustment module has

step to their joint actions at the next moment. Meanwhile, as shown

been added to amplify the changing characteristics of the tensor, thus

in Fig. 2, the reward and cost value networks are used to evaluate the accelerating the exploration and learning speed of the policy neural

expected reward and safety cost values under the current policy. 

network. 

In contrast to traditional RL policy neural networks that utilize

The structure of LSTM neurons is shown in Fig. 6, which consists MLP architectures, the collaborative control policy necessitates the

of five parts: the cell state, hidden state, forget gate, input gate, and

acquisition of both historical motion data and social interaction data

output gate. When LSTM unit is working, initially, the forget gate 7 





Downloaded from https://iranpaper.ir

https://www.tarjomano.com

https://www.tarjomano.com

*R. * *Zhao* *et* *al. *

*Expert* *Systems* *With* *Applications* *267* *\(2025\)* *126153* 

of the LSTM determines which previous state information should be

*4.2.1. * *Policy* *optimization* *problem* *description* retained and which should be discarded. This is achieved by observing

The purpose of policy optimization is to continually update the

the hidden state from the previous time step *ℎ𝑡*−1 and the current input policy *𝜋 * based on the trajectories  *𝑡 *= \( *𝑠𝑡, * *𝑎𝑡, * *𝑟𝑡, * *𝑐𝑡, * *𝑠𝑡*\+1\) of multi-agent *𝑠𝑡 * and applying a Sigmoid function to generate a forget gate activation interactions with the environment sampled by the sampler, enabling

value *𝐹𝑡 * ranging between 0 and 1. This value is then multiplied by

the multi-agents to learn to maximize the expected rewards while

the previous cell state *𝑐𝑡*−1 to decide the extent to which each state maintaining the function below a threshold for the optimal policy. For

information is retained. Subsequently, the input gate decides which

details, refer to Eqs. \(1\) and \(2\). 

new information from the current step will be saved in the cell state. 

The state–action value function *𝑄𝜋 *\( *𝑠, **𝒂***\) with respect to reward This also involves two parts: a Sigmoid function determines which

indicates the quality of taking action ***𝒂 *** in state *𝑠*, while the state value information to update, generating an input gate activation value *𝐼𝑡*; function *𝑉 𝜋 *\( *𝑠*\) intuitively represents the quality of state *𝑠*. Which can a Tanh function creates a candidate state vector *𝑇𝑡*, which provides be respectively defined as:\[

\]

the new information that might be added to the cell state. Then, the

∞

∑

element-wise product *𝐼*

*𝑄𝜋 *\( *𝑠, **𝒂***\) = E

*𝛾𝑡𝑅*\( *𝑠*

\(12\)

*𝑡 *× *𝑇𝑡 * represents the new information that will

*𝑠* 1∶∞∼ *𝑃* *, **𝒂*** 0∶∞∼ *𝜋*

*𝑡, * *𝑎𝑡*\)| *𝑠* 0 = *𝑠, **𝒂*** 0 = *𝑎*

be added to the cell state. Following this, the cell state *𝑐*

*𝑡*=0

*𝑡 * is updated by

combining the outputs from the forget and input gates. The specific

*𝑉 𝜋 *\( *𝑠*\) = E ***𝒂***∼ *𝜋 *\[ *𝑄*\( *𝑠, **𝒂***\)\]

\(13\)

update formula is *𝑐𝑡 *= *𝐹𝑡 *× *𝑐𝑡*−1 \+ *𝐼𝑡 *× *𝑇𝑡 * which indicates that the current cell state is composed of partially forgotten previous states On this basis, the concept of the advantage function *𝐴𝜋 *\( *𝑠, **𝒂***\) is and newly added information. Lastly, the output gate controls the

established, which represents the advantage of taking action ***𝒂 *** relative output generated based on the current cell state *𝑐𝑡*. A Sigmoid function to the average reward of all actions. It is defined as:

determines which part of the cell state should be outputted, and a Tanh

function normalizes the cell state to a range of −1 to 1. This output is

*𝐴𝜋 *\( *𝑠, **𝒂***\) = *𝑄𝜋*\( *𝑠, **𝒂***\) − *𝑉𝜋*\( *𝑠*\) \(14\)

then produced through an element-wise multiplication with the output

of the Sigmoid function, generating the hidden state output *ℎ𝑡*. 

In practical computation, the Generalized Advantage Estimation

In the considered multi-agent system, the neural network’s input

\(GAE\) method is commonly used for calculation. Similarly, the state–

*𝑆𝑡 * represents the set of states of CAVs at time step *𝑡*. Given that the action Value function and state value function concerning the *𝑗* th cost behavior of CAVs in the intersection scenario is dynamic, the update

constraint value of agent *𝑖 * are respectively defined as:

of the state set inevitably includes the incorporation of new CAVs and

\[

\]

∞

∑

the departure of existing CAVs. To achieve this dynamic feature, this

*𝑄𝜋 *\( *𝑠, **𝒂**𝑖*\) = E *𝑠*

*𝛾𝑡𝐶𝑖 *\( *𝑠*

\(15\)

*𝑗*

*𝑡, **𝒂**𝑡*\)| *𝑠* 0 = *𝑠, **𝒂*** 0 = ***𝒂***

work introduces a circular queue mechanism, where the neural network

*𝑐𝑖*

1 ∶∞∼ *𝑃* *, **𝒂*** 0 ∶∞∼ *𝜋*

*𝑗*

*𝑡*=0

\[

\]

updates the input in a rolling manner. Fig. 5 exemplifies the operation *𝑉 𝜋 *\( *𝑠*\) =

*𝑄𝜋 *\( *𝑠, **𝒂**𝑖*\)

\(16\)

of the circular queue mechanism using a single north-south lane. The

E

*𝐶𝑖*

***𝒂***∼ *𝜋*

*𝐶𝑖*

*𝑗*

*𝑗*

upper part of Fig. 5 shows the lane with one CAV about to enter the control area and three CAVs within the control area. The lower

The cost advantage function for agent *𝑖 * and cost index *𝑗 * is defined part depicts the subsequent movement: the CAV at the head of the

as:

queue departs the control area, followed by each CAV in the control

*𝐴𝜋 *\( *𝑠, **𝒂**𝑖*\) = *𝑄𝜋 *\( *𝑠, **𝒂**𝑖*\) − *𝑉 𝜋 *\( *𝑠*\) \(17\)

area advancing forward by one position, with the newly entered CAV

*𝐶𝑖*

*𝐶𝑖*

*𝐶𝑖*

*𝑗*

*𝑗*

*𝑗*

occupying the rear of the queue. 

Specifically, the state space of lane *𝑙 * is predefined with *𝑁𝑙 * positions, which measures the improvement of cost function after taking ac-where *𝑁𝑙 * is greater than the maximum capacity of the control area

tions under the current state and follow policy *𝜋*. To achieve more sta-of that lane at the intersection under high-density traffic conditions. 

ble and efficient learning, practically, it is calculated by GAE method, 

Assume at time step *𝑡*, there are *𝑢𝑙 * CAVs in the queue *𝑃𝑙*. In future which is obtained as\(

\)

time steps when a CAV departs, the position at the head of the queue, 

∑

*𝐴𝜋 *\( *𝑠, **𝒂**𝑖*\) =

\( *𝛾* *𝜆*\) *𝑘*

− *𝐶𝑖*\( *𝑠*

\) \+ *𝛾* *𝑉 𝜋 *\( *𝑠*

\( *𝑠*

\(18\)

*𝑃*

*𝑗*

*𝑡*\+ *𝑘, **𝒂**𝑡*\+ *𝑘*

*𝑖*

*𝑡*\+ *𝑘*\+1\) − *𝑉 𝜋*

*𝑡*\+ *𝑘*\)

*𝑙 *\[0\], will be vacated. Subsequently, all CAVs within the queue move *𝐶𝑖*

*𝐶𝑖*

*𝐶𝑖*

*𝑗*

*𝑘*=0

*𝑗*

*𝑗*

forward sequentially by one position, leaving the last position empty. 

where *𝜆 * is a parameter about GAE, we use it to balance the accuracy When a new CAV enters the controlled area, it will occupy the rear

of measurements and variance. 

position of the queue, *𝑃𝑙*\[ *𝑢𝑙*\]. This method facilitates the maintenance of a distance-ordered arrangement of CAVs within the state space, from

*4.2.2. * *Policy* *network* *optimization* *method* farthest to nearest to the intersection, aiding the neural network in The MAPCPO method, presented in this section, addresses the CMG

understanding the current environmental state. The rule for updating

problem by searching for the optimal feasible policy within the region

the position within the state space can be formalized as:

satisfying pre-set KL divergence and safety cost constraints. In the

⎧Dequeued Element = *𝑃*

⎪

*𝑙 *\[0\]

multi-agent environment, each agent has its local KL-divergence trust

⎨ *𝑃*

\(11\)

*𝑙 *\[ *𝑗*\] = *𝑃𝑙 *\[ *𝑗 *\+ 1\]

for *𝑗 *= 0 to *𝑢𝑙 *− 2

region, denoted as  *𝑖*. The global KL-divergence trust region,  , is the

⎪

⋂ *𝑛*

⎩ *𝑃*

intersection of all local KL-divergence trust regions:  =

 *𝑖*. Under

*𝑙 *\[ *𝑢𝑙 *\] = Enqueued Element

*𝑖*=1

a centralized policy framework, the global KL-divergence trust region

The reward value neural network and cost value neural network

is defined as the local neighborhood of the most recent iteration *𝜋𝑘*

mainly serve to evaluate the current policy neural network’s strengths

that satisfies the expected KL-divergence being less than a specified step

and weaknesses, mapping dynamic state information into expected

size. 

reward values and expected safety cost values, respectively. Given their

 = \{ *𝜋 *∶ \( *𝜋 *∥ *𝜋𝑘*\) ≤ *𝛿*\}

\(19\)

lower task complexity, to conserve computational and training data

resources, fully connected layer structures are chosen for the reward

value neural network and safety costs value neural network structures. 

Moreover, the policy update must satisfy safety constraints *𝑐𝑖 *. Thus, *𝑗*

the safety constraint trust region for policy *𝜋𝑘 * is:

\{

\}

1

*4.2. * *Policy* *neural* *network* *optimization*

** **=

*𝜋 *∶ *𝐽*

\( *𝜋*\) \+

\)

\(20\)

*𝐶𝑖*

E\( *𝐴𝜋*

≤ *𝑑𝑖𝑗*

*𝑗*

1 − *𝛾*

*𝑐𝑖𝑗*

8 





Downloaded from https://iranpaper.ir

https://www.tarjomano.com

https://www.tarjomano.com

*R. * *Zhao* *et* *al. *

*Expert* *Systems* *With* *Applications* *267* *\(2025\)* *126153* 

**Fig. ** **7. **Policy updating method oriented towards different safety postures. 

Constrained by the KL-divergence-based trust region ** **and the

√

safety The cost-based constraint region ****, the objective of policy op-2 *𝛿*

timization is to ensure that the policy remains within both constraint

*𝜃𝑘*\+1 = *𝜃𝑘 *\+

***𝑯 **𝑖*−1 *𝑔*

\(23\)

*⋆*

*𝑗*

*𝑔𝑇 **𝑯 **𝑖*−1 *𝑔*

regions while obtaining a higher reward function value. As illustrated in

*𝑗*

\(2\) Medium Safety

Fig. 7, the updated policy is ensured, as much as possible, to maximize the expected reward value within the constraints of safety costs. 

Fig. 7 \(b\) illustrates the scenario with medium safety level, the accessible region constrained by KL divergence intersects with the

*𝜋𝑘*\+1 = ar g max E\[ *𝐴𝜋*\( *𝑠, **𝒂***\)\] *, * *𝜋𝑘*\+1 ∈ ** **∩ ****

\(21\)

constraint region of safety costs. In this scenario, maximizing expected

*𝜋*

rewards might lead to the policy being in a risky state. After the Based on the relative positions of the trust region ** **and the con-initial step of maximizing rewards, the policy update results in a state

straint region ****, the likelihood of policy updates affecting the safety where the safety cost value exceeds the threshold, necessitating a

levels of multi-agents can be categorized as high safety level, medium

safety cost value projection step to address the constraint violation. The

safety level, and low safety level. 

intersection of the KL divergence constraint range and the safety cost

constraint range can be denoted as:

Let the parameters of the policy neural network be *𝜃*, the Hessian

matrix 

of 

the 

average 

KL 

divergence 

be

***𝑯 **𝑖*

=

** ** *𝑚𝑒𝑑* *𝑖𝑢𝑚 *≜ ** **∩ ** **≠ ∅ and ** ** *𝑚𝑒𝑑* *𝑖𝑢𝑚 *≠ ****

\(24\)

*𝑗*

\[

\]

*𝜕* 2E



*𝑠*

*𝐾* *𝐿*\( *𝜋*∥ *𝜋𝑘*\)\[ *𝑠*\]

0 ∼ *𝜌* 0 *,𝑠* 1∶∞ ∼ *𝑃𝜋𝑘*

, and *𝑔 * denote the policy gradient of the

which can be further expressed as:

*𝜕* *𝜃*

\{

*𝑖 𝜕* 

*𝜃𝑗*

advantage function. The update methods under three different safety

** ** *𝑚𝑒𝑑* *𝑖𝑢𝑚 *≜ KL\( *𝜋 *∥ *𝜋⋆*\) ≤ *𝛿*

situations are as follows. 

\}

1

\(1\) High-Safety

and

*𝐽*

\( *𝜋*\) \+

*𝐴𝜋 *\( *𝑠, **𝒂**𝑖*\)

\(25\)

*𝐶𝑖*

E *𝑠*

≤ *𝑑𝑗*

*𝑗*

1 − *𝛾*

*𝑜 *∼ *𝜌* 0 *, **𝒂***∼ *𝜋𝑘 ,𝑠* 1∶∞ ∼ ***𝑷 **𝜋𝑘*

*𝐶𝑖𝑗*

Fig. 7 \(a\) illustrates the scenario with high safety level, the reward-Under this safety situation the policy update using the MAPCPO

guided updatable policies are entirely in the intersection of the trust

algorithm is divided into two steps: reward enhancement and constraint

region and the constraint region, indicating that the overall safety of the

projection. Initially, the TRPO method is used to maximize the reward

current policy is at a high level. At this time, even without imposing

*𝑘*\+ 12

safety cost constraints, updating policies within KL divergence-based

of policy *𝜋 * into policy *𝜋*

without considering safety constraints, 

*⋆*

trust region will not lead to a dangerous situation while maximizing

which is represented as follows:

\[

\]

the reward. The policy region can be denoted as:

*𝑘*\+ 1

*𝜋*

2 = ar g max

*𝐴𝜋 *\( *𝑠, **𝒂***\)

\(26\)

*⋆*

E *𝑠𝑜*∼ *𝜌* 0 *, **𝒂***∼ *𝜋𝑘,𝑠* 1∶∞∼ ***𝑷 **𝜋𝑘*

** ** *ℎ𝑖𝑔* *ℎ *≜  ∩ ** **= ****

\(22\)

\[

\]

s.t. 

E *𝑠*



≤ *𝛿*

*𝑜 *∼ *𝜌* 0 *, **𝒂***∼ *𝜋𝑘 ,𝑠* 1∶∞ ∼ ***𝑷 **𝜋*

KL\( *𝜋 *∥ *𝜋𝑘*\+ 12 \)\[ *𝑠*\]

*𝑘*

Policies within this trust region comply with the safety cost con-

Subsequently, policy *𝜋𝑘*\+ 12 is projected into the safety constraint straints; hence, a situation without an optimal solution is not antici-set, transforming into policy *𝜋𝑘*\+1, to ensure the safety of the policy

*⋆*

pated. The traditional Trust Region Policy Optimization \(TRPO\) updat-

optimization process. 

ing method is employed. For detailed proof, please refer to Schulman

*𝜋𝑘*\+1 = ar g min\( *𝜋* *, * *𝜋𝑘*\+ 12 \)

\(27\)

\(2015\). 

*⋆*

9 





Downloaded from https://iranpaper.ir

https://www.tarjomano.com

https://www.tarjomano.com

*R. * *Zhao* *et* *al. *

*Expert* *Systems* *With* *Applications* *267* *\(2025\)* *126153* 

\[

\]

s.t. 

*𝐽*

\( *𝜋𝑘*\+1\) \+ 1

*𝐴𝜋 *\( *𝑠, **𝒂**𝑖*\)

where *𝑒 * represents the policy gradient of the safety value function, *𝐶𝑖*

E *𝑠*

≤ *𝑑𝑖𝑗*

∑ ∑

*𝑗*

1− *𝛾*

0 ∼ *𝜌* 0 *, **𝒂***∼ *𝜋𝑘 ,𝑠* 1∶∞ ∼ ***𝑷 **𝜋𝑘*

*𝐶𝑖𝑗*

defined as *̂𝑒 *≈

∇

\( *𝜋*\) and *̂𝑐 * represents the proximity of the

*𝑖*

*𝑗*

*𝜃 𝐽𝑐𝑖𝑗*

current policy’s safety level to the safety cost threshold, which is \(

\)

**Reward** **enhancement**

∑ ∑

*̂*

*𝑐*

defined as *̂𝑐 *≈

*𝐽*

\( *𝜋*\) −

*𝑗*

, ∀ *𝑗 *= 1 *, *… *, * *ℎ*. 

*𝑖*

*𝑗*

*𝐶𝑖𝑗*

1− *𝛾*

*𝑘*\+ 1

Similar to the reward enhancement step, the Eq. \(35\) can be solved Let *𝜃*

2

represent the optimal advantage function’s largest policy

*⋆*

using the dual approach:

neural network parameters within the KL-divergence trust region. The

1

objective function is linearized within the KL-divergence trust region

\( *𝜃𝑘*\+1 *, * *𝜆𝑘*\+ 12 \) =

\( *𝜃 *− *𝜃𝑘*\+ 12 \) *𝑇 **𝑯 **𝑖 *\( *𝜃 *− *𝜃𝑘*\+ 12 \) \+ *𝜆*\( *̂𝑒𝑇 *\( *𝜃 *− *𝜃𝑘*\) \+ *̂𝑐*\) \(36\)

2

*𝑗*

using a second-order approximation method. 

*𝑘*\+ 1

*𝜃*

2 = ar g max *𝑔𝑇 *\( *𝜃 *− *𝜃𝑘*\)

\(28\)

With *𝜆𝑘*\+1 denoting the optimal solution to the dual problem, 

*⋆*

*⋆*

Eq. \(36\) can be efficiently addressed using the KKT conditions. 

s.t. 

1 \( *𝜃 *− *𝜃𝑘*\) *𝑇 **𝑯**𝑖 *\( *𝜃 *− *𝜃𝑘*\) ≤ *𝛿*

2

*𝑗*

⎧ *𝜃𝑘*\+1 −  *𝜃𝑘*\+ 12 \+ *𝜆𝑘*\+1 *̂𝑏 *= 0

As the Hessian matrix is always positive semi-definite, \(28\) ex-

⎪

\(37\)

pression represents a convex optimization problem with quadratic in-

⎨∇

⎪ *𝜃*\( *𝜃𝑘*\+1 *, * *𝜆𝑘*\+1\) = 0

equality constraints. If this optimization problem has a feasible solu-

⎩∇ *𝜆*\( *𝜃𝑘*\+1 *, * *𝜆𝑘*\+1\) = 0

tion, it satisfies the Slater’s condition, and strong duality exists. The

\{ *̂𝑒𝑇*\( *𝜃𝑘*\+1 − *𝜃𝑘*\) \+ *̂𝑐 *= 0

dual problem can be more efficiently solved using the following dual

\(38\)

formulation:

∇ *𝜆*\( *𝜃𝑘*\+1 *, * *𝜆𝑘*\+1\) = 0

\(

\)

1

\( *𝜃𝑘*\+ 12 *, * *𝜆𝑘*\+ 12 \) = − *𝑔𝑇 *\( *𝜃 *− *𝜃𝑘*\) \+ *𝜆*

\( *𝜃 *− *𝜃𝑘*\) *𝑇 **𝑯 **𝑖 *\( *𝜃 *− *𝜃𝑘*\) − *𝛿*

\(29\)

2

*𝑗*

Eqs. \(37\) and \(38\) must satisfy the primal constraints, dual constraints, and complementary slackness from the KKT conditions, as

Considering the continuously differentiable nature of the original

shown:

objective function, it can be established that the Karush–Kuhn–Tucker

*̂*

*𝑒𝑇 *\( *𝜃𝑘*\+1 − *𝜃𝑘*\) \+ *̂𝑐 *≤ 0

\(39\)

\(KKT\) conditions serve as both necessary and sufficient criteria for *𝑘*\+ 1

determining the optimal solution *𝜃*

2

for the primal problem, and

*⋆*

*𝑘*\+ 1

*𝜆𝑘*\+1 ≥ 0

\(40\)

*𝜆*

2 for the dual problem. Consequently, Eq. \(28\) can be proficiently

*⋆*

addressed by employing the KKT conditions:

*𝜆𝑘*\+1\( *̂*

*𝑒𝑇 *\( *𝜃𝑘*\+1 − *𝜃𝑘*\) \+ *̂𝑐*\) = 0

\(41\)

− *𝑔 *\+ *𝜆𝑘*\+ 12 ***𝑯 **𝑖 𝜃𝑘*\+ 12 − *𝜆𝑘*\+ 12 ***𝑯 **𝑖 𝜃𝑘 *= 0 

∇

*𝑗*

*𝑗*

*𝜃 *\( *𝜃𝑘*\+ 12 *, * *𝜆𝑘*\+ 12 \) = 0

\(30\)

*𝑘*\+ 1

Deriving from Eq. \(41\), it follows that *𝜃𝑘*\+1 = *𝜃𝑘*\+ 12 \+ *𝜆*

2 *̂𝑒*. Consider-

*⋆*

*⋆*

\(

\)

\(

\)

1

*𝑇*

ing the constraints imposed by Eqs. \(39\) and \(40\), the optimal solution \(

\)

\( *𝜃𝑘*\+ 12 − *𝜃𝑘*\)

***𝑯 **𝑖*

*𝜃𝑘*\+ 12 − *𝜃𝑘*

− *𝛿 *= 0

1

*𝑘*\+

2

*𝑗*

2

for the dual problem can be expressed as *𝜆𝑘*\+1 = max 0 *, ̂𝑒𝑇 *\( *𝜃*

− *𝜃𝑘*\)\+ *̂*

*𝑐*

. 

*⋆*

*̂*

*𝑒𝐿*−1 *̂*

*𝑒*

∇ *𝜆*\( *𝜃𝑘*\+ 12 *, * *𝜆𝑘*\+ 12 \) = 0

\(31\)

Therefore, the optimization outcomes that satisfy Eqs. \(39\) and \(41\) are:

To satisfy the KKT conditions, the primal constraints, dual con-

−1

*𝜃𝑘*\+1 = *𝜃𝑘*\+ 12 − *𝜆𝑘*\+1 ***𝑯 **𝑖*

*̂*

*𝑒*

\(42\)

*⋆*

*⋆*

*𝑗*

straints, and complementary slackness must be met respectively in

Eqs. \(30\) and \(31\). 

1

Finally, combining the reward enhancement step with the cost

\( *𝜃𝑘*\+ 12 − *𝜃𝑘*\) *𝑇 **𝑯 **𝑖 *\( *𝜃𝑘*\+ 12 − *𝜃𝑘*\) − *𝛿 *≤ 0

\(32\)

2

*𝑗*

provides the optimized result:

√

√

√

−1

*𝜆𝑘*\+ 12 ≥ 0

\(33\)

*𝜃𝑘*\+1 = *𝜃𝑘 *\+ √

2 *𝛿*

***𝑯 **𝑖*

*𝑔 *− *𝜆𝑘*\+1 ***𝑯 ***−1 *̂*

*𝑒*

\(43\)

*⋆*

−1

*𝑗*

*⋆*

*𝑔𝑇 **𝑯 **𝑖*

*𝑔*

\(

\)

*𝑗*

1

*𝜆𝑘*\+ 12

\( *𝜃𝑘*\+ 12 − *𝜃𝑘*\) *𝑇 **𝑯 **𝑖 *\( *𝜃𝑘*\+ 12 − *𝜃𝑘*\) − *𝛿 *= 0

\(34\)

2

*𝑗*

The analysis of the worst-case performance degradation of the system

during policy iteration, through the aforementioned two steps of policy

Ensuring the constraints from the Eqs. \(32\), \(33\) and \(34\) are met, update, is as follows. 

*𝑘*\+ 1

*𝑘*\+ 1

−1

*𝜃*

2 can be derived as *𝜃*

2 = *𝜃𝑘 *\+

1

***𝑯 **𝑖*

*𝑔 * from Eq. \(39\). 

When the current policy meets the safety cost constraints, given

*⋆*

*⋆*

1

*𝑘*\+

*𝑗*

*𝜆*

2

a current policy *𝜋𝑘 * that satisfies these constraints, under the KL-𝑘\+ 1

Subsequently, merging *𝜃*

2 into the Eq. \(30\), the optimal solution

divergence projection, the upper bounds for reward improvement and

*⋆*

√

−1

constraint violation for each policy update are given as follows \(Yang

*𝑘*\+ 1

*𝑔𝑇 **𝑯 **𝑖*

*𝑔*

is *𝜆*

2 =

*𝑗*

et al., 2020\):

*⋆*

2 *𝛿*

√

⎧

2 *𝛿* *𝛾* *𝜗𝑘*\+1

*𝐽 *\( *𝜋𝑘*\+1\) − *𝐽 *\( *𝜋𝑘*\)

≥ −

*𝑅*

**Cost** **projection**

⎪

1− *𝛾* 2

⎨

√

\(44\)

⎪

2 *𝛿* *𝛾* *𝜗𝑘*\+1

⎩ *𝐽 *\( *𝜋𝑘*\+1\)

*𝐶*

*𝑐𝑖*

≤ *𝑑𝑗 *\+

Subsequently, the MAPCPO method projects the intermediate pol-

*𝑗*

1− *𝛾* 2

icy *𝜃𝑘*\+ 12 into the safety cost constrained domain by minimizing the where

distance between current policy and the safety cost constrained set. 

\[

\]

*𝜗𝑘*\+1 = max |E

*𝐴𝜋𝑘 *\( *𝑠, **𝒂***\) | *, *

The distance between the current policy and the safety cost con-

*𝑅*

*𝑠* 0∼ *𝜌* 0 *, **𝒂***∼ *𝜋𝑘,𝑠* 1∶∞∼ ***𝒑**𝜋𝑘 *\[

\]

strained set is measured using the KL divergence. Using a second-order

*𝜗𝑘*\+1 = max |

*𝐴𝜋 *\( *𝑠, **𝒂**𝑖*\) | *. *

*𝐶*

E *𝑠*

approximation, the objective function can be linearized:

0 ∼ *𝜌* 0 *, **𝒂***∼ *𝜋𝑘 ,𝑠* 1∶∞ ∼ ***𝒑**𝜋𝑘*

*𝐶𝑖𝑗*

1

*𝜃𝑘*\+1 = arg min

\( *𝜃 *− *𝜃𝑘*\+ 12 \) *𝑇 **𝑯 **𝑖 *\( *𝜃 *− *𝜃𝑘*\+ 12 \) \(35\)

*⋆*

*𝑗*

When the current policy does not satisfy the safety cost con-

*𝜃*

2

straints, given a current policy *𝜋𝑘 * that meets the constraints, under s.t. 

*̂*

*𝑒𝑇 *\( *𝜃 *− *𝜃𝑘*\+ 12 \) \+ *̂𝑐 *≤ 0

KL-divergence projection, the upper bounds for reward improvements

10 





Downloaded from https://iranpaper.ir

https://www.tarjomano.com

https://www.tarjomano.com

*R. * *Zhao* *et* *al. *

*Expert* *Systems* *With* *Applications* *267* *\(2025\)* *126153* 

**Table** **2**

**Algorithm** **1 **SRL-CLCADI

Main parameters of the experiments. 

∏

**Require: **Global state ***𝑺 *** from environment: ***𝑺 ***= \[ *𝑛 *\( *𝑑𝑖, * *𝑣𝑖, * *𝜁𝑖, * *𝜄𝑖, * *𝜅𝑖*\)\]

Parameters

Value

*𝑖*=1

**Ensure: **Expected velocity and steer of each vehicle in the environment: ***𝑨 ***=

**Scenario** **Parameters**

∏

\[

*𝑛*

\( *𝑣*′ *𝑡, * *𝜓𝑡*\)\]

Time-step

0.1 s

*𝑖*=1

*𝑖*

*𝑖*

1: Initialize hyper-parameters: *𝜃 *, *𝜃 *, *𝜃*

, ***𝑵***

Control distance length

60 m

*𝑅*

*𝐶*

*𝜋𝑘 *, set training parameter ***𝑵 **𝑒*

*𝑡*

Road width

14.2 m

2: **for ** *𝑒 *= 1 *, * 2 *, *… *, * *𝑁 ***do** *𝑒*

Network bandwidth

20 MHz

3:

**for ** *𝑡 *= 1 *, * 2 *, *… *, * *𝑁 ***do**

*𝑡*

RSU Tx power

50 dBm

4:

**for **each vehicle *𝑖 *= 1 *, * 2 *, *… *, * *𝑛 ***do** RSU antenna gain

12 dB

5:

chose action ** **according to the current policy. 

*𝑡*

∏

CAV antenna gain

3 dB

6:

Execute global actions ** **=

*𝑛*

\( *𝑣*′ *𝑡, * *𝜓𝑡*\), get reward ***𝑹 ***, cost ***𝑪***

*𝑡*

*𝑖*=1

*𝑖*

*𝑖*

*𝑡*

*𝑡*

∏ *𝑛*

**SRL-CLCADI**

and next state *𝑠*

\( *𝑡*\) = \[

\( *𝑑𝑖, * *𝑣𝑖, * *𝜁𝑖, * *𝜄𝑖, * *𝜅𝑖*\)\]

*𝑡*\+1

*𝑖*=1

Discount factor

0.99

7:

*𝑆 *= *𝑆*

*𝑡*

*𝑡*\+1

Learning rate

1 × 10−3 → 0 \(linearly\)

8:

**end** **for**

Max KL divergence

0.001

9:

**end** **for**

Damping coefficient

0.01

10:

Collect trajectories ***𝝉***

= \( *𝑆 , **𝒂 **, * *𝑟 , **𝒄 **, * *𝑠*

\)

*𝜋*

*𝑡*

*𝑡*

*𝑡*

*𝑡*

*𝑡*\+1

*𝑘*

Cost limit

1

11:

Calculate advantage function of reward and risk function: *𝐴𝜋𝑘 *\( *𝑠, **𝒂***\), Policy std *𝜎*

1 → 0 \(exponentially\)

*𝜋*

*𝜃*

*𝐴 𝑘 *\( *𝑠, **𝒂***\)

Policy std decrease index *𝜗*

−1 *. * 5 *𝑒 *− 6

*𝐶𝑖𝑗*

Coefficient of std *𝜁*

1

12:

Calculate *̂*

*𝑔*, *̂*

*𝑒*, *̂*

*𝑐*

Collision safety threshold

8 m

13:

Update policy network as:

GAE coefficient *𝜌*

0.97

14:

**if  ** *ℎ𝑖𝑔* *ℎ *≜ ** **∩ ***𝑪 ***= ** then**

√

***𝑵 **, **𝑵 **, **𝑵***

2000, 2000, 500

*𝑒*

*𝑡*

*𝑎*

−1

15:

*𝜃𝑘*\+1 = *𝜃𝑘 *\+

2 *𝛿*

***𝑯 **𝑖*

*𝑔*

*𝑐𝑖*

1 *. * 5 × *𝑒*−4

*⋆*

−1

*𝑗*

*𝑗*

*𝑔𝑇 **𝑯 **𝑖*

*𝑔*

*𝑗*

*𝛿 , * *𝛿 , * *𝛿 , * *𝛿 , * *𝛿 , * *𝛿 , * *𝛿*

15, 125, 20, 15, 125, 0.05, 0.05, 0.4

*𝑟*

*𝑐*

*𝑠*

*𝑝*

*𝑎*

*𝑣*

*𝑎𝑡*

16:

**else** **if ** *𝑇𝑚𝑒𝑑* *𝑖𝑢𝑚 *≜ *𝑇 *∩ *𝐶 *= ∅ and ** ** *𝑚𝑒𝑑* *𝑖𝑢𝑚 *≠ *𝑇 ***then** Dimension of ***𝑺**, **𝑨***

252, 48

√

−1

17:

*𝜃𝑘*\+1 = *𝜃𝑘 *\+

2 *𝛿*

***𝑯 **𝑖*

*𝑔 *− *𝜆𝑘*\+1

*⋆*

−1

*𝑗*

*⋆*

**MAPPO**

*𝑔𝑇 **𝑯 **𝑖*

*𝑔*

*𝑗*

Learning rate

3 × 10−4 → 0 \(linearly\)

18:

**else**

√

Clip range *𝜀*

0.2

−1

19:

*𝜃𝑘*\+1 = *𝜃𝑘 *−

2 *𝛿*

***𝑯 **𝑖*

*̂*

*𝑒𝑇*

*⋆*

−1

*𝑗*

Minibatch size

64

*̂*

*𝑒𝑇 **𝑯 **𝑖*

*̂*

*𝑒*

*𝑗*

20:

**end** **if**

**VICS** **and** **MICA**

21:

Update *𝜙𝑘 *, *𝜙𝑘 * as:

Predictive horizon

5

*𝑅*

*𝐶*

\[\(

\) \]

2

Target velocity *𝑣*

15 m/s

*𝑡*

22:

*𝜃𝑘*\+1 = ar g min *𝐸*

*𝑉*

\( *𝑠 *\) − *̂*

*𝑅*

*𝑅*

*𝜃*

*𝜙𝑘*

*𝑡*

*𝑡*

*𝑅*

\[\(

\) \]

2

23:

*𝜃𝑘*\+1 = ar g min *𝐸*

*𝑉*

\( *𝑠 *\) − *̂*

*𝐶*

*𝐶*

*𝜃*

*𝜙𝑘*

*𝑡*

*𝑡*

*𝐶*

24: **end** **for**

and constraint violation for each policy update are given by Yang et al. 

\(2020\):

⎧

√

⎪

2\( *𝛿*\+ *𝑏*\+2 *𝛼𝐾* *𝐿*\) *𝛾* *𝜗𝑘*\+1

*𝑅*

⎪ *𝐽*\( *𝜋𝑘*\+1\) − *𝐽*\( *𝜋𝑘*\) ≥ −

neural network, with their current network parameters denoted as *𝜃𝑘*\+1

1− *𝛾* 2

*𝑅*

⎨

√

\(45\)

and *𝜃𝑘*\+1, respectively. They calculate the loss based on the discrepancy

⎪

*𝐶*

2\( *𝛿*\+ *𝑏*\+2 *𝛼𝐾* *𝐿*\) *𝛾* *𝜗𝑘*\+1

⎪ *𝐽 *\( *𝜋𝑘*\+1\)

*𝐶*

between the estimated and actual values of reward and safety cost, and

*𝑐𝑖*

≤ *𝑑𝑗 *\+

⎩ *𝑗*

1− *𝛾* 2

subsequently update to obtain new network parameters *𝜙𝑘 * and *𝜙𝑘 *. 

*𝑅*

*𝐶*

\[\(

\) \]

2

These theoretical outcomes provide mathematical assurances for

*𝜃𝑘*\+1 = ar g min *𝐸*

*𝑉*

\( *𝑠*

\(48\)

*𝑅*

*𝑡*\) − *̂*

*𝑅𝑡*

*𝜃*

*𝜙𝑘*

*𝑅*

satisfying safety cost constraints during policy iteration. Concurrently, 

\[\(

\) \]

2

they establish explicit limits for potential performance degradation

*𝜃𝑘*\+1 = ar g min *𝐸*

*𝑉*

\( *𝑠*

\(49\)

*𝐶*

*𝑡*\) − *̂*

*𝐶𝑡*

*𝜃*

*𝜙𝑘*

during policy updates, thereby ensuring the enhancement of algo-

*𝐶*

rithmic performance through the policy update process. where *𝑏*\+ =

where *̂*

*𝑅𝑡 * represents the true reward value, and *̂*

*𝐶𝑡 * represents the true

max\(0 *, * *𝐽 𝑖*\( *𝜋𝑘*\) − *𝑐𝑖 *\) and *𝛼*

. Here, *𝑞 * represents the gradient

*𝑗*

*𝑗*

*𝐾* *𝐿 *=

1

−1

safety cost value. 

2 *𝑞𝑇 **𝑯 **𝑖*

*𝑞*

*𝑗*

of the safety cost advantage function. 

\(3\) Low Safety

*4.3. * *SRL-CLCADI* *algorithm* *overview*

Fig. 7 \(c\) illustrates the scenario with low safety level, the reward-driven updatable policy lies entirely outside the constraint region. 

This section introduces SRL-CLCADI algorithm, based on the

There is no intersection between the trust and constraint regions, 

MAPCPO algorithm, which includes three safety situation update rules

suggesting the current policy’s overall safety is critically low. Thus, any

for addressing the cooperative control problem at intersections. This

policy update will not return to the constraint region, satisfying the

algorithm ensures both monotonic reward performance improvement

safety cost. The policy region can be represented as:

and safety cost constraints satisfaction, as presented in Algorithm 1. The

first line of the algorithm initializes network and algorithm parameters, 

** ** *𝑙* *𝑜𝑤 *≜ ** **∩ ***𝑪 ***= ∅

\(46\)

including the random reward-based value network *𝜃𝑅*, the safety cost-

based value network *𝜃𝐶 *, and the policy network *𝜃𝑘*. It also sets the total When the policy is in a low safety posture, a backtrack search

number of training iterations ***𝑵**𝑒 * and the maximum number of time method is utilized to discover updates aimed at finding suitable param-steps per iteration ***𝑵**𝑡*. The main loop of the algorithm starts from the eters for the policy update:

√

second line. It first constructs a trajectory ***𝝉***

√

*𝜋𝑘 * consisting of state–action

√

−1

pairs for multiple vehicles, along with the associated reward ***𝑨**𝜋 *\( *𝑠, **𝒂***\) *𝜃𝑘*\+1 = *𝜃𝑘 *− √

2 *𝛿*

***𝑯 **𝑖*

*̂*

*𝑒𝑇*

\(47\)

*𝑅*

*⋆*

−1

*𝑗*

and safety cost values ***𝑨**𝜋 *\( *𝑠, **𝒂**𝑖*\) within the environment \(lines 2–12\). 

*̂*

*𝑒𝑇 **𝑯 **𝑖*

*̂*

*𝑒*

*𝑗*

*𝐶𝑖𝑗*

The algorithm then evaluates and updates the policy network and

*4.2.3. * *Value* *neural* *network* *optimization* the reward and safety cost-based value networks independently \(lines

The reward value neural network and the safety costs value neural

13–23\). When updating the policy network, the algorithm considers

network function to assess the efficacy of the newly updated policy

both the current policy’s constraint satisfaction and the feasibility of

11 





Downloaded from https://iranpaper.ir

https://www.tarjomano.com

https://www.tarjomano.com

*R. * *Zhao* *et* *al. *

*Expert* *Systems* *With* *Applications* *267* *\(2025\)* *126153* 

subsequent policies. It estimates the likelihood of a policy update

et al. , 2014\) and the MIP-based method MICA \(Lu & Kim, 2018\) in leading to a safe scenario for the multi-agent system and proposes terms of safety, ride comfort, computational time, and traffic efficiency. 

an appropriate update solution \(lines 13–20\). Regarding the reward

VICS represents a coordination scheme in the MPC framework. The

and safety cost-based value networks, their respective gradients are scheme efficiently utilizes the intersection area by preventing each employed to update the network parameters \(line 21–23\). 

pair of conflicting vehicles from approaching their cross collision point

\(CCP\) at the same time, where the CCP is the intersection of their **5. ** **Experiments**

trajectories. A risk function is proposed to quantify the risk of a collision of a pair of vehicles around their CCP, which is given by

This section describes the experiments conducted to assess the

−\( *𝛼*

\+ *𝛼*

\)

*𝑅*

*𝑖 𝑑* 2

*𝑖*

*𝑖*′ *𝑑* 2

*𝑖*′

*𝑖,𝑖*′ \( *𝑡*\) = *𝐻* *𝛿𝑖,𝑗 *\( *𝑡*\) *𝑒*

\(50\)

performance of the proposed method. First, the models and parameters

where *𝐻 * is a positive constant indicating the highest possible risk of used in the experiment are elaborated. Then, the acquired training and

collision, and *𝛿*

testing results are analyzed. Additionally, a sensitivity analysis of the

*𝑖,𝑖*′ is a binary variable to state whether the vehicles *𝑖*

and *𝑖*′ have a CCP. Besides, *𝑑*

hyperparameters in the cost function is performed, and the vehicle

*𝑖 * and *𝑑𝑖*′ are the distances of the CCP from

current position of vehicles *𝑖 * and *𝑖*′ along their trajectories, and *𝛼*

scheduling process at intersections is visualized. 

*𝑖 * and

*𝛼𝑖*′ are positive constants. At any time, if two conflicting vehicles are very close to their CCP, the risk function returns a high value, and if

*5.1. * *Experiments* *setting*

at least one vehicle is far from the CCP, it returns a low value. Based

on that, a constrained nonlinear optimization problem is constructed as

The simulation tools used in this experiment include CARLA, SUMO, 

follows:

and NS3. The hardware environment consists of a high-performance

*𝑇 *−1 *𝑁*

*𝑇 *−1 *𝑁*

*𝑇 *−1 *𝑁*

*𝑁*

computer equipped with an i9-13700KF CPU and an NVIDIA GeForce

∑ ∑

∑ ∑

∑ ∑ ∑

*𝐽 *=

*𝑤𝑣*\( *𝑣𝑖*\( *𝑡 *\+ 1\) − *𝑣𝑑 *\)2 \+

*𝑤𝑎*\( *𝑎𝑖*\( *𝑡*\)\)2 \+

*𝑤𝑅𝑅𝑖,𝑖*′ \( *𝑡*\)

RTX 3090 GPU, running Ubuntu 18.04 as the operating system. In

*𝑡*=0 *𝑖*=0

*𝑡*=0 *𝑖*=0

*𝑡*=0 *𝑖*=0 *𝑖*′= *𝑖*\+1

the simulation setup, CARLA and SUMO are integrated through their

\(51\)

respective Python API to perform joint traffic simulation, enabling

*𝑠.𝑡.𝑣* min ≤ *𝑣𝑖 *≤ *𝑣* max *, *

coordinated modeling of complex traffic scenarios. The RL methods

were implemented using the PyTorch framework and network simula-

*𝑎* min ≤ *𝑎𝑖 *≤ *𝑎* max *. *

tion was conducted in NS3 using C\+\+ to accurately emulate vehicular

network protocols and network traffic. Additionally, CARLA’s built-in

where *𝑇 * is the length of the prediction horizon, *𝑣𝑑 * is the desired sensors were utilized to transmit real-time vehicle status information, 

velocity, and *𝑤𝑣*, *𝑤𝑎*, and *𝑤𝑅 * are weight coefficients. There are three including speed, position, and orientation. To generate vehicle traffic

cost terms in total. The first term denotes the cost related to velocity

trajectories at intersections, we used the BasicAgent class in CARLA, 

deviation from the desired value *𝑣𝑑*. The second term denotes the cost which allows for dynamic movement of multiple autonomous vehicles

of acceleration. Minimizing these two terms means comfortable and

through the intersection area. For detailed configurations of the inter-

smooth flow of vehicles. The third term denotes the cost related to section scenario and network simulation parameters, please refer to

the risk of collisions as defined in the risk Eq. \(51\), which sums up

Table 2. 

quantified risks at all CCPs for all possible pairs of vehicles considering

Vehicle speed and turning angle control signals provided by the

their predicted trajectories in the horizon. 

policy neural network were converted into throttle and brake signals

MICA represents a control scheme within the MIP framework. De-

via a PID controller within the simulator. In this experiment, a four-way

fine an objective function:

∑

dual-lane signal-free intersection in CARLA TOWN05 was chosen as the

*𝐽 *=

*𝑡𝑖,𝑜𝑢𝑡*

\(52\)

training and testing scenario for the RL model. The road width was 14.2

*𝑖*

m, with the East–West and North–South lanes measuring 65 m and 50

*𝑠.𝑡.𝑡𝑖 *\+ *𝑀 *× *𝑏𝑖,𝑖*′ ≤ *𝑡𝑖*′ *,𝑖𝑛, * if *𝑏𝑖,𝑖*′ = 1 *,* m in length, respectively. Taking into account the road characteristics

in the CARLA map and the V2I communication range, the control area

*𝑡𝑖 *≥ *𝑡𝑖*′ *,𝑜𝑢𝑡 *\+ *𝑀 *× \(1 − *𝑏𝑖,𝑖*′ \) *, * if *𝑏𝑖,𝑖*′ = 0 *. *

length was fixed at 70 m. Various vehicle types were selected for the

simulation to emulate genuine traffic flow, with vehicle dimensions

where *𝑡𝑖 * denotes the crossing time for vehicle *𝑖*, *𝑀 * represents a suf-ranging from 3.6–5.4 m in length, 1.8–2.2 m in width, and 1.5–2 m

ficiently large number, and *𝑏𝑖,𝑖*′ is a binary variable. *𝑡𝑖*′ *,𝑖𝑛 * and *𝑡𝑖*′ *,𝑜𝑢𝑡*

in height. Vehicle arrivals followed a Poisson distribution, and the respectively denote the times at which vehicle *𝑖*′ enters and exits the traffic flow in the scenario was continuous. Vehicle turning intentions

conflict area. 

at intersections \(left turn, straight, and right turn\) are determined In the SRL-CLCADI algorithm, the policy function employs three

randomly, ensuring a more realistic and varied traffic flow within the

hidden layers, comprising two fully connected layers and one LSTM

simulated environment. The time step was set to 0.1 s, consistent with

layer, each containing 512 units. The value function utilizes two fully

the actual vehicle control cycle. 

connected layers, each with 128 units. Both the MAPPO and MAPPO-

To evaluate the performance of the proposed SRL-CLCADI algo-

SC algorithms use a multi-layer perceptron with two hidden layers as

rithm in experimental tests, two sets of experiments were conducted

approximations for the policy and value functions, each layer contain-

in this section. Specifically, the first set of experiments showcased ing 128 units. Policy iteration is performed every 2000 timesteps, with

the RL-Based training process of SRL-CLCADI, MAPPO \(Guan et al., 

the Adam optimizer used for policy updates. The learning rate linearly

2020\) and MAPPO-SC, the latter having the same safety constraints as decreases from 1 × 10−3 to 0, while the standard deviation exponentially

SRL-CLCADI but utilizing reward function penalties. The experiment

decays from 1 to 0, and training stops after 2000 epochs. Moreover, 

compared the variations in rewards, costs, collision rates, number of

the parameter settings for MAPPO, VICS and MICA algorithms are

safety distance violations, and acceleration during the training process

consistent with those in the original paper. The main parameters of the

of the SRL-CLCADI with those during the training processes of MAPPO

experiments are referenced in Table 2. 

and MAPPO-SC methods. And results demonstrate that our algorithm

achieves superior overall performance, particularly in terms of safety, 

*5.2. * *Performance* *comparison* *during* *training* *process* successfully reaching zero collisions for the first time. The second set

of experiments compares the performance of the SRL-CLCADI-trained

We compared the training performance of cooperative control

policy with MAPPO, MAPPO-SC, the MPC-based method VICS \(Kamal

method at Intersections based on RL: SRL-CLCADI, MAPPO, and

12 





Downloaded from https://iranpaper.ir

https://www.tarjomano.com

https://www.tarjomano.com

*R. * *Zhao* *et* *al. *

*Expert* *Systems* *With* *Applications* *267* *\(2025\)* *126153* 

**Fig. ** **8. **Performance comparison of SRL-CLCADI policy with MAPPO, MAPPO-SC during training process: \(a\) shows the variation in average episode rewards, \(b\) represents the changes in average episode risk values, \(d\) illustrates the changes in average episode collision rates, and \(e\) demonstrates the variation in the number of times average episode safety distances are violated. 

MAPPO-SC. The MAPPO-SC method features the same reward and

safety, comfort, and efficiency\), their performance does not show a safety cost functions as SRL-CLCADI, facilitating the comparison of

significant increase during iterations. This is due to three highly chal-

the performance differences between the two policy updates under

lenging factors in the training scenario. First, the strong correlation identical settings. To achieve optimal training results, each episode between consecutive time steps in intersection scenarios means that

was set at *𝑡 *= 2000 time steps. Too short episode lengths could lead future policy choices heavily depend on current decisions, and ordinary

to trajectory information with high specificity, thereby compromising

fully connected layer neural networks lack the capability to capture

the robustness of the policy neural network. Conversely, excessively

historical vehicle state information. Next, as vehicle collisions directly

long episode durations demand significant computational and time

lead to the interruption of the training and truncation of the acquired

resources. Additionally, these methods could yield policies with di-

rewards, and since they do not employ risk-constrained policies during

minished responsiveness to terminal rewards, potentially leading to

performance optimization, the policies are highly prone to local optima. 

decreased efficiency in learning environments driven by rewards. 

Finally, the training scenario is a dynamic intersection scenario where

Performance metrics included average episodic reward, average

the timing of vehicles entering the intersection and their directions after

episodic cost, average episodic collision rate, average episodic safety

entering are random, and the large dimensionality of the state space

distance violation occurrences and average episodic acceleration. The

presents significant training challenges. 

average episodic reward value represents the overall performance of

the policy. The average episodic cost represents the comprehensive

Fig. 8\(b\) represents the global safety level in the highly stochastic safety performance. The average episodic acceleration illustrates the

traffic environment established for this study. The safety cost value policy’s comfort performance. The average episodic collision rate offers

represents the risks of collision and skidding present in the traffic a direct insight into the policy’s safety, and the average episodic environment. The red dashed line parallel to the *𝑥*-axis signifies the safety distance violation occurrences denote potential collision risks. 

cost function limit of the SRL-CLCADI algorithm, serving as a guide for

These metrics are calculated as the average over the four attempts per

updating the safety cost value network. Given that this limit is a very

episode. 

small value, if the safety cost function falls below it, it can be assumed

From Fig.  8\(a\), it can be observed that the SRL-CLCADI algorithm that there are virtually no risks of collision or skidding in the traffic

\(represented by the bright red line\) converges after approximately 1250

environment, and almost no likelihood of CAVs coming dangerously

iterations. Post-convergence, its variance is relatively small, indicating

close or being prone to skidding. It can be observed that the red curve, 

good stability of the SRL-CLCADI algorithm. Due to the presence of

representing the SRL-CLCADI algorithm, successfully converges below

stochastic delays in communication between vehicles, fluctuations in-

the limit line after approximately 1250 policy iterations. It then main-

creased during the training process and minor fluctuations persisted

tains the safety of the traffic scenario with excellent stability, which is

after convergence, yet the overall performance remained stable.The

noteworthy in intersection scenarios where all vehicles exhibit random

successful convergence of the SRL-CLCADI algorithm is attributed to

turning behaviors. The outstanding performance of the SRL-CLCADI

its design, which integrates dual-value networks based on the reward

algorithm can be attributed to two key features: an independent safety

function and safety expenditure, coupled with risk-aware constrained

cost value network and safety cost-constrained policy optimization. 

policy optimization. This enables it to balance optimization objec-

These elements guide the policy, gradually enhancing the overall per-

tives with potential risks in addressing complex and uncertain road formance while simultaneously improving the system’s safety. The

intersection control problems, thereby demonstrating robust perfor-

MAPPO algorithm, which lacks safety risk reward penalties, and the

mance. As for the MAPPO algorithm \(represented by the dark red line\)

MAPPO-SC algorithm, which incorporates such penalties, did not show

and the MAPPO-SC algorithm \(represented by the yellow line\), which

a significant reduction in safety cost values even after repeated fluc-

adopt the same reward function design as SRL-CLCADI \(considering

tuations. This reflects the limitations of traditional reward-driven RL

13 





Downloaded from https://iranpaper.ir

https://www.tarjomano.com

https://www.tarjomano.com

*R. * *Zhao* *et* *al. *

*Expert* *Systems* *With* *Applications* *267* *\(2025\)* *126153* 

**Fig. ** **9. **Different traffic flow simulation scenarios: sparse, normal, and dense. 

algorithms in safety-critical road intersection scenarios lacking safety

each policy-environment interaction, and inference time indicates the

awareness. 

computational demand and real-time performance of the algorithm. 

Fig.  8\(c\) provides a detailed depiction of the mean collision rate Each method undergoes six sets of experiments, with the average of

curve across multiple training iterations, directly reflecting the policy’s

ten trials taken as the result for each set. 

safety performance. Fig.  8\(d\) shows the curve for the average num-

Fig. 10 presents the results for the low traffic flow scenario. As ber of safety distance violations, a lateral indicator of policy safety, 

shown in the first two box plots of Fig. 10, in terms of safety, all where fewer violations indicate lower potential collision risks. The methods except MAPPO and MAPPO-SC achieve a zero collision rate. 

SRL-CLCADI algorithm, represented by the red curve, achieves both

This further underscores the inability of RL algorithms without ex-

a zero collision rate and zero safety distance violations in the traffic

plicit safety constraints to be implemented in safety-critical domains. 

scenarios after approximately 1250 policy iterations, maintaining this

Similarly, all but MAPPO and MAPPO-SC register zero safe distance

performance in subsequent iterations. In contrast, the MAPPO-SC and

violations, with MAPPO-SC showing less variation than MAPPO. This

MAPPO algorithms, relying solely on a single-value network based on

reflects the inherent safety risks of reinforcement learning methods rewards, exhibit considerable fluctuation during training, but without

without individual risk constraints, while SRL-CLCADI meets the safety

a significant downward trend in collision rates and safety distance requirements of autonomous driving. 

violations. This highlights the outstanding performance of SRL-CLCADI

in longitudinal and lateral safety aspects of autonomous driving, and

The third box plots in Fig. 10 represent the policy’s ride comfort. 

the inadequacy of traditional single-value, reward-based networks in

For the average acceleration per episode, the SRL-CLCADI algorithm ex-

handling complex scenarios at dynamic intersections. 

hibits the lowest median and the smallest variance, indicating superior

Fig.  8\(e\) shows the curve of the mean acceleration per episode comfort performance through small and stable accelerations. Simi-over multiple training iterations, a metric reflecting the comfort of larly, in terms of average jerk per episode, the SRL-CLCADI algorithm

passengers during the driving process. A lower value indicates higher

demonstrates a comparable level of excellence. The fourth box plots

comfort. It is observed that the strategy of the SRL-CLCADI algorithm

in Fig. 10 represent the policy’s Fuel Consumption Per 100 kilometers. 

converges to a high level of comfort and maintains this elevated level

The SRL-CLCADI method generally exhibits lower energy consumption, 

with low variance after convergence. Initially, due to safety constraints

benefiting from its smoother acceleration control. The average energy

on its policy space, SRL-CLCADI could not maintain a high level of consumption of the MAPPO-SC method is similar to that of the SRL-comfort. However, once the safety level of the environment is ele-

CLCADI method, but MAPPO-SC exhibits a larger variance, indicating

vated, the policy network becomes more capable of optimizing driving

that SRL-CLCADI has better stability in terms of energy consumption. 

comfort. In contrast, the MAPPO-SC and MAPPO algorithms exhibit

As shown in the fifth box plot of Fig. 10,  in terms of efficiency, considerable fluctuation during training, and their acceleration rates

SRL-CLCADI possesses the highest single-pass count and the highest

do not show a significant downward trend. This is attributed to the

average pass count, which can be attributed to its design of regularized

excessive complexity of the scenario and the lack of a separate safety

rewards and its excellent safety performance. MAPPO-SC has a slightly

cost value evaluation network, leading the policies to become trapped

lower maximum single-pass count than the SRL-CLCADI method, but a

in local optima and unable to explore the optimal policy. 

significantly lower average pass count, due to its high inconsistency. If

a collision occurs, the trial is interrupted, resulting in fewer vehicles

*5.3. * *Performance* *comparison* *after* *deployment* *policy* passing during those trials. This inconsistency further highlights the higher safety risks associated with MAPPO-SC. The MPC-based VICS

method and the MIP-based MICA method exhibit fluctuations similar

In this study, the performance at intersections of five methods –

to those of the SRL-CLCADI method, but their traffic efficiency is SRL-CLCADI, MAPPO, MAPPO-SC, VICS, and MICA – is compared. The

significantly lower than that of the SRL-CLCADI method. 

first three methods deploy trained policies into models. VICS, based on

the MPC control method, serves as a performance baseline for inter-

As shown in the sixth box plot of Fig. 10, a key advantage of section coordination control, whereas MICA, based on the MIP control

SRL-CLCADI lies in its shorter inference time, reducing the average method, is a classic approach for intersection coordination control. In

inference time by approximately 65% compared to traditional control

the experimental scenario, the continuous flow of vehicles arriving at

methods. This exceptional performance can largely be attributed to the

the intersection follows a Poisson distribution. As shown in Fig. 9, 

RL methods’ ability to directly correlate traffic scenario states with ac-

three intersection scenarios are selected, characterized by low traffic

tions via neural pathways, thereby eliminating the need for exhaustive

flow *𝜆* 1 = 600 veh∕h∕lane, medium traffic flow *𝜆* 2 = 1200 veh∕h∕lane, or extensive computational demands required for solving optimization

and high traffic flow *𝜆* 3 = 1800 veh∕h∕lane, where *𝜆 * represents the constraints. The computational power at the endpoint of autonomous

Poisson number. Performance metrics include collision rate, number of

driving vehicles is extremely limited, and the high computational de-

safe distance violations, acceleration, fuel consumption per 100 kilo-

mand of traditional methods may lead to the failure to find the optimal

meters, the number of vehicles passing during each policy-environment

solution or the application of suboptimal solutions, potentially causing

interaction attempt, and inference time. Collision rate and safe distance

safety incidents or poor collaborative control effects. This has limited

violations indicate safety, while acceleration measure comfort. Fuel

the application of optimization methods in vehicle-road cooperative

consumption per 100 kilometers represents energy consumption. The

control system. Our method significantly reduces the inference time

efficiency is reflected through the number of vehicles passing during

required for intersection cooperative control policies, further advancing

14 





Downloaded from https://iranpaper.ir

https://www.tarjomano.com

https://www.tarjomano.com

*R. * *Zhao* *et* *al. *

*Expert* *Systems* *With* *Applications* *267* *\(2025\)* *126153* 

**Fig. ** **10. **Performance comparison of SRL-CLCADI policy with MAPPO, MAPPO-SC policies, VICS and MICA after deployment under sparse scenarios. 

**Fig. ** **11. **Performance comparison of SRL-CLCADI policy with MAPPO, MAPPO-SC policies, VICS and MICA after deployment under normal scenarios. 

the application of RL methods in vehicle-road cooperative control

volumes, indicating its superiority in terms of ride comfort. As traffic

system. 

volume increases, energy consumption also rises for all five methods, 

Fig.  11 and Fig. 12 depict scenarios with medium and high traf-which is attributable to higher traffic densities implying a certain fic flow, respectively. These scenarios demonstrate that SRL-CLCADI

degree of congestion and greater fluctuations in vehicle acceleration. 

maintains consistent performance characteristics akin to those in low

Regarding inference time, compared to the VICS and MICA methods, 

traffic conditions, highlighting its robustness. Even with increased traf-

SRL-CLCADI shows a significant reduction in both medium and high

fic flow, SRL-CLCADI does not exhibit a decline in performance. In both

traffic scenarios, with a greater decrease as the complexity of the medium and high traffic conditions, SRL-CLCADI effectively sustains

scenario increases. The MAPPO method and the MAPPO-SC method

a zero collision rate, proving its efficacy in maintaining safety across

have a slightly shorter inference time than the SRL-CLCADI method, 

varying traffic scenarios. In contrast, the MAPPO-SC algorithm, lacking

which is attributed to the larger parameter size of the LSTM neural

specific safety constraints, exhibits a higher collision rate, underscoring

network in the SRL-CLCADI method. SRL-CLCADI has the highest traffic

the importance of limited safety cost constraints in RL-based vehicle-

efficiency and the least fluctuation, while the MAPPO and MAPPO-

road cooperative control system. The collision rate of the MAPPO-SC

SC algorithms exhibit higher peaks but greater variability, due to the

method is slightly lower than that of the MAPPO method, which can

lack of safety-related constraints in their update strategies. The VICS

be attributed to an appropriate reward function. The MPC-based VICS

and MICA methods show smaller fluctuations, but their mean values

and MICA methods, like the SRL-CLCADI method, maintained a zero

are lower. This suggests that optimization-based methods experience a

collision rate. From the perspective of riding comfort, SRL-CLCADI

rapid increase in computational demand as traffic, and particularly the

achieves the lowest median and minimal variance across all three traffic

number of CAVs, increases, whereas SRL-CLCADI efficiently manages

15 





Downloaded from https://iranpaper.ir

https://www.tarjomano.com

https://www.tarjomano.com

*R. * *Zhao* *et* *al. *

*Expert* *Systems* *With* *Applications* *267* *\(2025\)* *126153* 

**Fig. ** **12. **Performance comparison of SRL-CLCADI policy with MAPPO, MAPPO-SC policies, VICS and MICA after deployment under dense scenarios. 

shown in Fig. 13.  The *𝑥*-axis shows different parameter combinations, and the y-axes represent the collision rate and the number of safety

distance violations per episode. The analysis indicates that adjusting the

weight of each term – safety distance violation, sideslip, and collision

– affects these performance metrics distinctly. First, when the safety

distance violation term weight is reduced \(with sideslip and collision

weights constant\), both the collision rate and safety distance violations

increase. This result stems from the model’s reduced penalty for safety

distance violations during training, limiting the cost function’s ability

to guide the model towards safer outcomes. Consequently, an increase

in safety distance violations also raises the collision rate. Conversely, 

when this weight is increased, the model places excessive focus on minimizing safety distance violations, which weakens the impact of

the collision penalty. This narrow focus on safety distance violations

paradoxically results in a higher collision frequency. A similar pat-Fig. **13. **Sensitivity analysis of safety distance violation, sideslip, and collision term weights. Bars represent: current parameters \(1st\), ±50% for safety distance violation tern occurs with adjustments to the sideslip weight. Reducing this

term *𝛿 *\(2nd, 3rd\), ±50% for sideslip term *𝛿 *\(4th, 5th\), and ±50 units for collision weight leads to more frequent sideslip events, causing additional safety

*𝑟*

*𝑐*

term *𝛿 *\(6th, 7th\). 

*𝑠*

distance violations between vehicles, especially in adjacent lanes or intersections, which in turn raises the collision rate. Increasing the sideslip weight likewise causes both metrics to rise due to the di-these demands. The experimental results in medium and high traffic

minished relative weight of the collision penalty. Lastly, reducing the

conditions further prove the method’s ability to handle increased traf-

collision penalty weight drives both metrics higher, as the collision fic without impacting key performance and safety metrics. Balancing

penalty’s diminished importance limits its effectiveness. When the col-

inference time and safety in high-density traffic scenarios is crucial, 

lision penalty weight is maximized, the collision rate drops to zero, but

further highlighting SRL-CLCADI’s advanced capabilities in managing

due to a relative decrease in penalties for safety distance violations complex traffic conditions. 

and sideslip, the frequency of safety distance violations rises. Based In summary, SRL-CLCADI offers the most suitable comprehensive

on these sensitivity analysis results, we selected the current parameter

performance in the autonomous driving and intelligent transportation

combination to achieve an optimal balance among the various safety

domain. In high traffic flow scenarios, RL methods without individ-

cost metrics. 

ual safety constraints struggle to cope. When deployed in models, 

SRL-CLCADI, based on RL, provides a significant advantage in in-

*5.5. * *Traffic* *dynamic* *flow* *analysis*

tersection coordination. Compared to traditional control methods, it

delivers similar or even superior performance. However, traditional

This section provides a traffic dynamics flow analysis. Two traffic

control policies require high computational power and longer inference

scenarios were selected for trajectory and speed visualization, one with

times. In contrast, SRL-CLCADI demands minimal computational power

slightly below-average difficulty and one with slightly above-average

and significantly shorter resolution times, representing a considerable

difficulty. The difficulty considerations for the scenarios include factors

improvement in computational efficiency. 

such as traffic flow and the number of left-turning vehicles. Fig. 14

presents the visualization for the slightly below-average difficulty sce-

*5.4. * *Cost* *hyperparameter* *sensitivity* *analysis* nario, while Fig. 15 presents the visualization for the slightly above-average difficulty scenario. As shown in Fig. 14 \(b\), in the slightly To evaluate how cost weight hyperparameters affect algorithm per-below-average difficulty traffic scenario, only VEH2 decelerates and

formance, we conducted a sensitivity analysis of these weights, as

waits to pass at the initial stage, and the deceleration process is 16 





Downloaded from https://iranpaper.ir

https://www.tarjomano.com

https://www.tarjomano.com

*R. * *Zhao* *et* *al. *

*Expert* *Systems* *With* *Applications* *267* *\(2025\)* *126153* 

**Fig. ** **14. **Visualization of slightly below-average difficulty traffic scenario: \(a\) represents the traffic trajectory of vehicles, and \(b\) represents the speed curve of vehicles. 

**Fig. ** **15. **Visualization of slightly above-average difficulty traffic scenario: \(a\) represents the traffic trajectory of vehicles, and \(b\) represents the speed curve of vehicles. 

minimal. After the other vehicles have passed and the collision risk

incorporates cost value projection steps in corresponding safety levels

is eliminated, VEH2 accelerates and passes through while maintaining

to coordinate the constraints of cost values. Additionally, the policy

a safe TTC. As shown in Fig. 15 \(b\), in the slightly above-average neural network in this paper adopts dynamic inputs to more closely

difficulty scenario with many conflict points, at the beginning, all resemble real-world intersection scenarios and includes lateral control

vehicles, except for VEH1 and VEH10 which decelerate to avoid col-

of vehicles in its output, thereby enhancing the algorithm’s perfor-lision risks, maintain relatively high speeds while passing through the

mance ceiling. Experiments demonstrate that the proposed SRL-CLCADI

intersection. After VEH1 and VEH10 eliminate collision risks with other

outperforms both traditional baseline methods and current state-of-

vehicles, they begin to accelerate and pass through the intersection the-art reinforcement learning approaches in terms of performance. 

quickly, while maintaining a safe TTC. From Fig. 15 \(a\), it can be While our system exhibits superior performance, the development of

observed that VEH10 decelerates to avoid left-turning vehicles coming

cooperative control policies for intersections still holds significant po-

from the south to the west, while VEH1 decelerates to avoid left-

tential. In the future, we aim to improve the structure of the policy

turning vehicles coming from the east to the south. As VEH4 reaches

neural network to enhance its capability in capturing historical state

the intersection last, it decelerates and waits before passing through, 

information and social interaction data, thereby raising its performance

and after eliminating collision risks with other vehicles, VEH4 quickly

ceiling. Furthermore, we will explore more rational update methods to

passes the intersection. Multiple scenario verifications confirm that the

increase the efficiency and potential of policy updates. 

SRL-CLCADI method demonstrates a high road utilization rate, further

validating the efficiency and safety of the SRL-CLCADI method. 

**Declaration** **of** **competing** **interest**

**6. ** **Conclusion** **and** **future** **outlook**

The corresponding author, on behalf of all authors of this submis-

This paper introduces the SRL-CLCADI system, a safety reinforce-

sion, hereby declares that there are no financial or personal relation-

ment learning-based approach for vehicle-road cooperative control sys-

ships with other people or organizations that could inappropriately

tem. This system collects trajectory information through interaction

influence our work. This declaration encompasses but is not limited

with the intersection environment and updates the cooperative control

to employment, consultancies, stock ownership, honoraria, paid ex-

policy using the proposed MAPCPO algorithm. Notably, the paper

pert testimony, patent applications/registrations, and grants or other

categorizes the conditions of policy updates based on safety levels and

funding. The authors declare that they have no competing interests. 

17 





Downloaded from https://iranpaper.ir

https://www.tarjomano.com

https://www.tarjomano.com

*R. * *Zhao* *et* *al. *

*Expert* *Systems* *With* *Applications* *267* *\(2025\)* *126153* 

**Acknowledgment**

Isele, D., Rahimi, R., Cosgun, A., Subramanian, K., & Fujimura, K. \(2018\). Navigating

occluded intersections with autonomous vehicles using deep reinforcement learning. 

All authors approved the final version of the manuscript. 

In *2018* *IEEE* *international* *conference* *on* *robotics* *and* *automation *\(pp. 2034–2039\). 

IEEE. 

Kamal, M. A. S., Imura, J.-i., Hayakawa, T., Ohata, A., & Aihara, K. \(2014\). A vehicle-

**Data** **availability**

intersection coordination scheme for smooth flows of traffic without using traffic

lights. *IEEE* *Transactions* *on* *Intelligent* *Transportation* *Systems*, *16*\(3\), 1136–1147. 

Data will be made available on request. 

Kuwata, Y., Teo, J., Fiore, G., Karaman, S., Frazzoli, E., & How, J. P. \(2009\). Real-time

motion planning with applications to autonomous urban driving. *IEEE* *Transactions*

*on* *Control* *Systems* *Technology*, *17*\(5\), 1105–1118. 

**References**

Li, Z., Gong, J., Lu, C., & Yi, Y. \(2021\). Interactive behavior prediction for het-

erogeneous traffic participants in the urban road: A graph-neural-network-based

multitask learning framework. *IEEE/ASME* *Transactions* *on* *Mechatronics*, *26*\(3\), 

Abboud, K., Omar, H. A., & Zhuang, W. \(2016\). Interworking of DSRC and cellular

1339–1349. 

network technologies for V2x communications: A survey. *IEEE* *Transactions* *on*

Li, X., Sun, Z., Cao, D., He, Z., & Zhu, Q. \(2015\). Real-time trajectory planning for

*Vehicular* *Technology*, *65*\(12\), 9457–9470. 

autonomous urban driving: Framework, algorithms, and verifications. *IEEE/ASME*

Achiam, J., Held, D., Tamar, A., & Abbeel, P. \(2017\). Constrained policy optimization. 

*Transactions* *on* *Mechatronics*, *21*\(2\), 740–753. 

In *International* *conference* *on* *machine* *learning *\(pp. 22–31\). PMLR. 

Li, N., Yao, Y., Kolmanovsky, I., Atkins, E., & Girard, A. R. \(2020\). Game-theoretic mod-

Al-Sharman, M., Dempster, R., Daoud, M. A., Nasr, M., Rayside, D., & Melek, W. 

eling of multi-vehicle interactions at uncontrolled intersections. *IEEE* *Transactions*

\(2023\). Self-learned autonomous driving at unsignalized intersections: A hierar-

*on* *Intelligent* *Transportation* *Systems*, *23*\(2\), 1428–1442. 

chical reinforced learning approach for feasible decision-making. *IEEE* *Transactions*

Li, B., & Zhang, Y. \(2018\). Fault-tolerant cooperative motion planning of connected and

*on* *Intelligent* *Transportation* *Systems*, *24*\(11\), 12345–12356. 

automated vehicles at a signal-free and lane-free intersection. *IFAC-PapersOnLine*, 

Antonio, G.-P., & Maria-Dolores, C. \(2022\). Multi-agent deep reinforcement learning

to manage connected autonomous vehicles at tomorrow’s intersections. *IEEE*

*51*\(24\), 60–67. 

*Transactions* *on* *Vehicular* *Technology*, *71*\(7\), 7033–7043. 

Li, B., Zhang, Y., Zhang, Y., Jia, N., & Ge, Y. \(2018\). Near-optimal online motion

Bichiou, Y., & Rakha, H. A. \(2018\). Developing an optimal intersection control system

planning of connected and automated vehicles at a signal-free and lane-free

for automated connected vehicles. *IEEE* *Transactions* *on* *Intelligent* *Transportation*

intersection. In *2018* *IEEE* *intelligent* *vehicles* *symposium *\(pp. 1432–1437\). IEEE. 

*Systems*, *20*\(5\), 1908–1916. 

Lu, Q., & Kim, K.-D. \(2018\). A mixed integer programming approach for autonomous

Dai, P., Liu, K., Zhuge, Q., Sha, E. H.-M., Lee, V. C. S., & Son, S. H. \(2016\). Quality-

and connected intersection crossing traffic control. In *2018* *IEEE* *88th* *vehicular*

of-experience-oriented autonomous intersection control in vehicular networks. *IEEE*

*technology* *conference* *\(VTC-fall\) *\(pp. 1–6\). IEEE. 

*Transactions* *on* *Intelligent* *Transportation* *Systems*, *17*\(7\), 1956–1967. 

Lukose, E., Levin, M. W., & Boyles, S. D. \(2019\). Incorporating insights from signal

Dresner, K., & Stone, P. \(2006\). Human-usable and emergency vehicle-aware control

optimization into reservation-based intersection controls. *Journal* *of* *Intelligent*

policies for autonomous intersection management. In *Fourth* *international* *workshop*

*Transportation* *Systems*, *23*\(3\), 250–264. 

*on* *agents* *in* *traffic* *and* *transportation* *\(ATT\), * *Hakodate, * *Japan, * *vol. * *12 *\(p. 14\). 

Mirheli, A., Hajibabai, L., & Hajbabaie, A. \(2018\). Development of a signal-head-free

Fajardo, D., Au, T.-C., Waller, S. T., Stone, P., & Yang, D. \(2011\). Automated

intersection control logic in a fully connected and autonomous vehicle environment. 

intersection control: Performance of future innovation versus current traffic signal

*Transportation* *Research* *Part* *C* *\(Emerging* *Technologies\)*, *92*, 412–425. 

control. *Transportation* *Research* *Record*, *2259*\(1\), 223–232. 

Mirheli, A., Tajalli, M., Hajibabai, L., & Hajbabaie, A. \(2019\). A consensus-based

Guan, Y., Ren, Y., Li, S. E., Sun, Q., Luo, L., & Li, K. \(2020\). Centralized cooperation for

distributed trajectory control in a signal-free intersection. *Transportation* *Research*

connected and automated vehicles at intersections by proximal policy optimization. 

*Part* *C:* *Emerging* *Technologies*, *100*, 161–176. 

*IEEE* *Transactions* *on* *Vehicular* *Technology*, *69*\(11\), 12597–12608. 

Qian, X., Altché, F., Grégoire, J., & de La Fortelle, A. \(2017\). Autonomous intersec-

Guo, Y., Ma, J., Xiong, C., Li, X., Zhou, F., & Hao, W. \(2019\). Joint optimization of

tion management systems: Criteria, implementation and evaluation. *IET* *Intelligent*

vehicle trajectories and intersection controllers with connected automated vehicles:

*Transport* *Systems*, *11*\(3\), 182–189. 

Combined dynamic programming and shooting heuristic approach. *Transportation*

Schulman, J. \(2015\). Trust region policy optimization. arXiv preprint arXiv:1502.05477. 

*Research* *Part* *C:* *Emerging* *Technologies*, *98*, 54–72. 

Tian, R., Li, N., Kolmanovsky, I., Yildiz, Y., & Girard, A. R. \(2020\). Game-theoretic

Hafner, M. R., Cunningham, D., Caminiti, L., & Del Vecchio, D. \(2013\). Cooperative

modeling of traffic in unsignalized intersection network for autonomous vehicle

collision avoidance at intersections: Algorithms and experiments. *IEEE* *Transactions*

control verification and validation. *IEEE* *Transactions* *on* *Intelligent* *Transportation*

*on* *Intelligent* *Transportation* *Systems*, *14*\(3\), 1162–1175. 

*Systems*, *23*\(3\), 2211–2226. 

Hang, P., Huang, C., Hu, Z., & Lv, C. \(2022\). Driving conflict resolution of autonomous

Wu, Y., Chen, H., & Zhu, F. \(2019\). DCL-AIM: Decentralized coordination learning

vehicles at unsignalized intersections: A differential game approach. *IEEE/ASME*

of autonomous intersection management for connected and automated vehicles. 

*Transactions* *on* *Mechatronics*, *27*\(6\), 5136–5146. 

*Transportation* *Research* *Part* *C* *\(Emerging* *Technologies\)*, *103*, 246–260. 

He, Z., Zheng, L., Lu, L., & Guan, W. \(2018\). Erasing lane changes from roads: A design

Xu, H., Zhang, Y., Li, L., & Li, W. \(2019\). Cooperative driving at unsignalized inter-

of future road intersections. *IEEE* *Transactions* *on* *Intelligent* *Vehicles*, *3*\(2\), 173–184. 

sections using tree search. *IEEE* *Transactions* *on* *Intelligent* *Transportation* *Systems*, 

Hu, C., Hudson, S., Ethier, M., Al-Sharman, M., Rayside, D., & Melek, W. \(2022\). 

*21*\(11\), 4563–4571. 

Sim-to-real domain adaptation for lane detection and classification in autonomous

Yang, T.-Y., Rosca, J., Narasimhan, K., & Ramadge, P. J. \(2020\). Projection-based

driving. In *2022* *IEEE* *intelligent* *vehicles* *symposium *\(pp. 457–463\). IEEE. 

constrained policy optimization. arXiv preprint arXiv:2010.03152. 

Hu, Y., Wang, W., Jia, H., Wang, Y., Chen, Y., Hao, J., et al. \(2020\). Learning to

Zhao, J., Knoop, V. L., & Wang, M. \(2023\). Microscopic traffic modeling inside

utilize shaping rewards: A new approach of reward shaping. *Advances* *in* *Neural*

intersections: interactions between drivers. *Transportation* *Science*, *57*\(1\), 135–155. 

*Information* *Processing* *Systems*, *33*, 15931–15941. 

18 



# Document Outline

+ Centralized cooperative control for autonomous vehicles at unsignalized all-directional intersections: A multi-agent projection-based constrained policy optimization approach  
	+ Introduction 
	+ Problem Definition and Method Framework  
		+ Problem Definition 
		+ Method Framework 

	+ Sampler Module Following the CMG Formulation  
		+ Safe Multi-Agent Reinforcement Learning Formulation 
		+ Representing the Collaborative Control Problem of CAVs as a Safe MARL Formulation in CMG  
			+ State space and joint action space 
			+ Reward function and safety cost function 


	+ Learner Module based on Safety Situation Awareness MAPCPO  
		+ DRL Architecture Design 
		+ Policy Neural Network Optimization  
			+ Policy Optimization Problem Description 
			+ Policy Network Optimization Method 


	+ Reward Enhancement 
	+ Cost Projection  
		+ Value Neural Network Optimization 
		+ SRL-CLCADI Algorithm Overview 

	+ Experiments  
		+ Experiments setting 
		+ Performance Comparison during Training Process 
		+ Performance Comparison after Deployment Policy 
		+ Cost Hyperparameter Sensitivity Analysis 
		+ Traffic Dynamic Flow Analysis 

	+ Conclusion and Future Outlook 
	+ Declaration of competing interest 
	+ Acknowledgment 
	+ Data availability 
	+ References



