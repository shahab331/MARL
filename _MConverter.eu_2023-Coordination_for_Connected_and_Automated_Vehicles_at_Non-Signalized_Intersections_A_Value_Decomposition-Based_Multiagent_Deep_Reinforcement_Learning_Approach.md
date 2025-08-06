IEEE TRANSACTIONS ON VEHICULAR TECHNOLOGY, VOL. 72, NO. 3, MARCH 2023

3025

Coordination for Connected and Automated Vehicles at Non-Signalized Intersections: A Value

Decomposition-Based Multiagent Deep

Reinforcement Learning Approach

Zihan Guo

, Yan Wu

, Lifang Wang

, and Junzhi Zhang

***Abstract*****—The recent proliferation of the research on multi-the resulting rise in vehicle demands. It has imposed challenges agent deep reinforcement learning \(MDRL\) offers an encourag-to the modern transportation system. In 2014, people in cities ing way to coordinate multiple connected and automated vehicles suffered 6.9 billion hours more wasted time on the road, and \(CAVs\) to pass the intersection. In this paper, we apply a value decomposition-based MDRL approach \(QMIX\) to control various the extra fuel consumption was about 3 billion gallons. \[1\]. For-CAVs in mixed-autonomy traffic of different densities to efficiently tunately, CAVs-related technologies, such as vehicle-to-vehicle and safely pass the non-signalized intersection with fairish fuel communication \(V2V\) and vehicle-to-infrastructure communi-consumption. Implementation tricks including network-level im-cation\(V2I\), empower vehicles to expand their line of sight provements, Q value update by TD \( *λ*\), and reward clipping operato obtain more information about the surroundings, e.g., the tion are added to the pure QMIX framework, which is expected to improve the convergence speed and the asymptotic performance of position, speed of all cars and other road participants within the the original version. The efficacy of our approach is demonstrated communication range of road infrastructures \[2\]. Consequently, by several evaluation metrics: average speed, the number of colli-it is possible and beneficial for vehicles to cooperate with others sions, and average fuel consumption per episode. The experimental to acquire safe and efficient traffic. **
** 
results show that our approach’s convergence speed and asymptotic According to the literature, the most straightforward attempt performance can exceed that of the original QMIX and the proximal policy optimization \(PPO\), a state-of-the-art reinforcement to manage the traffic at an intersection is to build traffic lights. 

learning baseline applied to the non-signalized intersection. More-For instance, the manual \[3\] uses a pre-defined signal phase over, CAVs under the lower traffic flow controlled by our method and timing \(SPaT\) plan to handle steady traffic conditions. P. 

can improve their average speed without collisions and consume the Varaiya \[4\] designs a greedy policy such that the infrastructure least fuel. The training is additionally conducted under the doubled can select the signal phase maximizing the pressure. However, traffic density, where the learning reward converges. Consequently, the model with maximal reward and minimum crashes can still these schemes still have several limitations: 1\) they cannot guarantee low fuel consumption, but slightly reduce the efficiency eliminate the stop delay of vehicles during the red phase; 2\) of vehicles and induce more collisions than the lower-traffic coun-if the traffic of each incoming approach distributes equally, the terpart, implying the difficulty of generalizing RL policy to more overall efficacy could be undermined \[5\]. Therefore, one branch advanced scenarios. 

develops adaptive traffic signal control \(ATSC\) strategies based

## Index

*Terms*—Deep

## reinforcement

learning, 

## intersection

on deep reinforcement learning \(DRL\). H. Wei, et al., \[6\] propose management, multi-agent reinforcement learning. 

a mix of online and offline RL framework based on deep Q

network \(DQN\) with the state defined by queue length, waiting I. INTRODUCTION

time, traffic signal phase, etc., discrete action determining if the traffic light can change its phase, a reward function including THE traffic congestion and potential accidents in urban thesumofqueuelengthanddelay,etc. 

areas result from the growing urbanized population and Another line of work is to forsake traffic signals and employ the RL framework to control one or more vehicles. The authors Manuscript received 10 April 2022; revised 23 September 2022; accepted 1 November 2022. Date of publication 4 November 2022; date of current of the paper \[7\] train an RL agent based on deep Q-learning. 

version 14 March 2023. This work was supported by the Institute of Electrical The goal is to navigate an ego vehicle with limited sensing Engineering Chinese Academy of Sciences under Grant E1553301. The review ability to pass the road. The action space is represented in of this article was coordinated by Prof. Xianbin Cao. *\(Corresponding authors:* *Yan Wu; Lifang Wang.\)*

three different macro ways \(time-to-go, sequential actions, and Zihan Guo, Yan Wu, and Lifang Wang are with the Key Laboratory of creep-and-go\), and the empirical results show that the DQN

Power Electronics and Electric Drives, Institute of Electrical Engineering agent can beat the rule-based time-to-collision \(TTC\) method Chinese Academy of Sciences, Beijing 100190, China, and also with University of Chinese Academy of Sciences, Beijing 100190, China \(e-mail: in most scenarios. Nonetheless, one of the drawbacks is that

zh\_guo97@163.com; wuyan@mail.iee.ac.cn; wlf@mail.iee.ac.cn\). 

a specific car-following model describes the behavior of the Junzhi Zhang is with the State Key Laboratory of Automotive Safety and En-surrounding cars not controlled by DQN, and hence behaviors ergy and Department of Automotive Engineering, Tsinghua University, Beijing 100084, China \(e-mail: jzhzhang@mail.tsinghua.edu.cn\). 

out of the scope of such a model are not well-comprehended Digital Object Identifier 10.1109/TVT.2022.3219428

by RL-controlled vehicles. In research \[5\], a gradient-based 0018-9545 © 2022 IEEE. Personal use is permitted, but republication/redistribution requires IEEE permission. 

See https://www.ieee.org/publications/rights/index.html for more information. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 03,2025 at 13:46:33 UTC from IEEE Xplore. Restrictions apply. 

3026

IEEE TRANSACTIONS ON VEHICULAR TECHNOLOGY, VOL. 72, NO. 3, MARCH 2023

RL agent \(i.e., proximal policy optimization, with abbreviation network-level improvements. 2\) Using modified QMIX

PPO\) is trained with the help of a fixed environment model. The to control multiple vehicles \(8 vehicles in total\) at the simulation results are more sample efficient and robust to the non-signalized intersection with four road segments and eight environmental noise as appropriate imagination depth is selected lanes in mixed-autonomy traffic, where human-driven vehicles than the pure PPO approach and more computationally efficient \(HDVs\) are simulated by Intelligent Driver Model\(IDM\). 3\) than the conventional centralized optimization-based algorithm. 

Compared to the PPO algorithm, our approach can improve Moreover, E. Vinitsky et al. \[8\] propose a FLOW framework, the average speed, average delayed time, and average fuel a benchmark for applying RL in mixed-autonomy scenarios, consumption and simultaneously assure safety. 

including intersections with and without traffic signals, merging, The rest of this paper is arranged as follows. Section II. gives a and bottleneck scenarios. Furthermore, they also test the perfor-concise introduction of the necessary background knowledge of mances of two RL algorithms, Trust Region Policy Optimization DRL and principles behind the QMIX approach, and Section III. 

\(TRPO\) and PPO, and the other two non-RL baselines. These transforms the coordination problem of multiple CAVs at the RL approaches are better solutions for merging scenarios. B. 

intersection into an RL framework. Section IV. elaborates on Peng et al. \[9\] expand the figure-eight scenario in the FLOW

the control flow of the QMIX algorithm and code-level tricks we benchmark to a two-lane non-signalized intersection and con-employed for fine-tuning. Section V. illustrates the simulation trol two CAVs to reduce the queuing phenomenon. Besides, settings and exhibits the empirical results. Section VI. provides the enthusiasm of researchers applying DRL or deep learning the summary and the works in the future. 

\(DL\) methods to the scenarios beyond the intersection, such as ramp metering and estimating the traffic incident duration, is II. P

growing \[10\], \[11\]. 

RELIMINARIES

However, directly deploying single-agent RL framework to *A. Decentralized POMDP*

multi-agent cooperative setting can cause the non-stationarity The decentralized partially observable Markov decesion problem \[12\]. Intended to conquer this problem, a centralized process\(Dec-POMDP\) \[21\] describes a fully cooperative mul-training and decentralized execution \(CTDE\) framework ap-tiagent setting with partial observation. It is defined as a tuple pears in the field of multi-agent deep reinforcement learning *G *= \( *I, S, \{A*

\(MDRL\). Firstly, the decentralization scheme is easy to im-i\}, T , r, \{ Ω *i\}, O, γ*\), in which *I ∈ * R *N * is the finite set of all agents contained in the problem, *s ∈ S * denotes the plement but brings about instability to learning as the envi-true state of the environment. *A*

ronment is dynamically changing with other agents’ learning *i * is a finite set of actions of agent *i ∈ I*, and the space of joint actions is defined as *A *= *×*

and explorations. On the other hand, it is granted that the *iAi *\( *×*

is the operator of Cartesian product\) and ˆ

*a ∈ A * represents the

centralization architecture can overcome the non-stationarity, joint actions taken by all agents. *T *: *S × A × S → * R is a state splicing all agents’ joint actions and observations impairs its transition probability function, which is defined as *T *\( *s, a, s*\) =

scalability to large-scale applications when thousands of agents Pr\( *s|a, s*\). A reward function *r *: *S × A × S → * R is a scalar are involved \[13\]. The basic procedure of the CTDE framework received by the team of all agents, which means the individual is to use the global states for training and to deploy the learned reward cannot be offered in Dec-POMDP setting. Ω

model in a decentralized fashion when the training has been *i * is denoted

as a finite set of observations for each agent *i ∈ I * and corre-completed. One instantiation of the CTDE framework is to spondingly Ω = *× * Ω

employ the value decomposition mechanism. One mode is to *i*

*i * the set of joint observations. An observation probability function is *O *: *S × A × * Ω *→ *\[0 *, * 1\] with the decompose the total fitted Q value directly into the sum of joint actions and observations \(where *o* each agent’s approximate Q value during training, called the *i ∈ * Ω *i * and *o ∈ * Ω\) as independent variables, which is subtly different from that in value decomposition networks \(VDNs\) \[14\]. However, VDN

POMDP. Hence, *O*\( *o, a, s*\) = Pr\( *o|a, s*\). The last element *γ*

does not fully exploit the benefits of adding global states during is described as the discount factor. 

training, which has potential to increase the representing power of joint action-value functions. Therefore, QMIX \[15\] creatively employs a monotonic constraint to achieve better expressiv-B. Deep Q-Learning

ity of the centralized action-value function. Although a band Deep Q-learning algorithm \[22\] utilizes an approximate func-of research endeavors to relax the monotonicity constraint of tion parameterized by *θ * to represent the action-value function QMIX theoretically \[16\], \[17\], a recent study \[18\] manifests that *Q*\( *·*\) and employs a replay buffer to store the transition data QMIX can gain the state-of-the-art average score at StarCraft \( *s, a, r, s*\) at each time step for the purpose of stabilizing the Multi-agent Challenge \(SMAC\) task \[19\] after fine-tuning with policy training, where the action *a * taken by the agent in state *s* some code-level tricks. Another important work is based on leads to next state *s*. To update the parameter of deep Q networks policy gradient to solve a multi-agent continuous control task \(DQNs\), a mini-batch with size *b * is sampled from the replay \(MADDPG\) \[20\]. However, the computational complexity of buffer, and the following loss function based on TD-error is MADDPG architecture increases with the number of agents, minimized:

which is detrimental to its scalability. 

The key contributions of our work are: 1\) Adding several *b*





implementation tricks to the original QMIX algorithm, *L*\(

target

2

*θ*\) =

*y*

*−*

\(1\)

*i*

*Q*\( *s, a*; *θ*\)

including employing the eligibility traces, reward clipping, and *i*=1

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 03,2025 at 13:46:33 UTC from IEEE Xplore. Restrictions apply. 



GUO et al.: COORDINATION FOR CONNECTED AND AUTOMATED VEHICLES AT NON-SIGNALIZED INTERSECTIONS

3027

where *y* target = *r *\+

*t*

*γ* max *aQ*\( *s, a*; *θ*\). *θ * is the parameter of the target network that replicates the network *θ * for a fixed period and keeps unvarying. 

*C. Independent Q-Learning and VDNs*

One straightforward way to solve a multi-agent problem is to transform it into a combination of single-agent problems in which each agent resides in the same environment. One of the earliest methods with this idea is called independent Q-learning \(IQL\) \[23\]. However, the concurrently and constantly changing policies of multiple agents force the IQL to experience the non-stationarity problem, and consequently, the convergence of this algorithm cannot be guaranteed. Nonetheless, the performance Fig. 1. 

Illustration of intersection with four road segments and two lanes. 8

DRL-controlled CAVs are colored in red, and IDM-controlled HDVs in this of IQL is not overshadowed by this risk of divergence, and when scenario are colored in yellow. The ranges of intersection and control zone are researchers tackle with cooperative or competitive games, IQL

also shown in this figure. 

becomes a common benchmark \[24\]. 

Conversely, Sunehag et al. comes up with an MDRL algo-III. PROBLEM STATEMENT AND FORMULATION

rithm called VDNs intended to utilize individual action-value function *Q *\(

; \)

*i τi, ai θi*

with local trajectory *τi*, local action *ai*, *A. Problem Statement*

and parameters *θ*

\(

*i * to estimate a joint value function *Qtot τ , *a\), We construct an isolated and non-signalized intersection with where *τ ∈ T N * is a joint action-observation history trajectory, four ways and two lanes \(composed of left-turn and through and *a ∈ AN * is a joint action. The decomposition formula is movements\) to solve the CAVs coordination problem under shown as follows. 

different mixed-autonomy traffic densities of 150veh/hour/lane *N*



and 300veh/hour/lane. These density values of traffic flow used *Q *\(

\(

; \)

*tot τ , a*\) =

*Qi τi, ai θi*

\(2\)

in our work are referred to as the parameters of the Grid sce-i=1

nario in research. \[8\]. Moreover, we employ modified QMIX to The loss function of VDNs is the same as \(1\) except that *Q * is coordinate 8 CAVs from each lane. When some of the CAVs substituted by *Q*

leave the intersection, the vehicle behind it will be controlled by *tot*. The convenience of the value decomposition mechanism is that it can avoid the combinatorial nature of the MDRL algorithm, and the rest of the HDVs residing in the multi-agent problems since each value function approximator control zone will be simulated by the IDM model. The whole only employs the local trajectory and action of each learning simulation is implemented in open-sourced Simulation of Urban agent \[13\]. 

Mobility \(SUMO\) simulator, as illustrated in Fig. 1. 

IDM is a typical model aiming to control the mixed traffic at the intersection \[25\] and can accurately represent driver behavior *D. The Key Insights of QMIX*

in the real-world \[26\]. This controller sends the acceleration There are two key aspects of the QMIX framework, consist-command as follows, 

ing of the individual-global-max \(IGM\) principle \[16\] and the *δ*

2

monotonicity constraint proposed in QMIX. 

*v*

*s∗*\( *v, * Δ *v*\)

*a*

=

*IDM*

*a * 1 *−*

*−*

\(5\)

The IGM principle states as follows. The optimal joint action *vd*

*s*

derived from the global maximization of the joint action-value where *a * is the acceleration term, *v* function *Q*

*d * is the expected speed, *δ*

jt : *T N × AN → * R \(where *τ ∈ T N * is a joint action-serves as an acceleration exponent, the vehicle’s actual headway observation history trajectory\) of a team of agents is equivalent is denoted by *s*, Δ *v * marks the speed difference between the ego to a collection of individually maximized action-value function and the lead vehicle, and

\[

*s∗*\( *·*\) is a function of the speed and the *Q *:

*i*

*T × A → * R\] *N *. 

*i*=1

speed difference, which is expressed as:

⎛

⎞

arg max

\(

\)





*a Q*

*τ*

1

1

1 *, a* 1

\+ max 0

*√*

\(6\)

arg max

⎜

. 

⎟

*s∗*\( *v, * Δ *v*\) = *s* 0

*, vT *\+ *v* Δ *v*

*Q *\(

*tot τ , a*\) = ⎝

.. 

⎠ \(3\)

2 *ab*

## a

### arg max

\(

\)

*aN QN τN , aN*

In which *s* 0 represents the minimum gap, *T * is a time gap, the comforTable.deceleration is denoted as Δ *v*. The corresponding Moreover, the monotonicity constraint is one sufficient con-parameters adopted in this paper are presented in Table I. 

dition of \(3\)

The lateral movements of all cars are fixed by the routes built

*∂Q *\(

in SUMO, and the longitudinal motion control is given by: *tot τ , *a\) *≥ * 0 *, ∀i ∈ I* \(4\)

*∂Q *\(

\)

*i τi, ai*

*xi*\( *t *\+ 1\) = *xi*\( *t*\) \+ *vi*\( *t*\) *· * Δ \+ 1 *ai*\( *t*\) *· * Δ2

A thorough procedure of QMIX and some implementation 2

tricks added to it in our work is illustrated in Section IV. 

*vi*\( *t *\+ 1\) = *vi*\( *t*\) \+ *ai*\( *t*\) *· * Δ *,* \(7\)

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 03,2025 at 13:46:33 UTC from IEEE Xplore. Restrictions apply. 

3028

IEEE TRANSACTIONS ON VEHICULAR TECHNOLOGY, VOL. 72, NO. 3, MARCH 2023

TABLE I

work \[19\] is incorporated into the design of valid action spaces IDM PARAMETERS

of agents. Specifically, when the vehicle approaches the other within the minimal head-to-tail distance, it must slow down with available discrete deceleration values. 

*2\) Reward Setting: * Designing the reward function in the RL

algorithm is of paramount significance, implicitly influencing the convergence speed and asymptotic performance of the algorithm. Empirically, more negative rewards can stimulate the agent to finish the episode with minimal timesteps due to cumu-where *xi*\( *t*\) is the travelling distance of vehicle *i * at time step *t*, lative punishments. On the other hand, more positive rewards *vi * and *ai * denotes the velocity and acceleration of vehicle *i * at motivate the agents to gather more prizes as they can, hence time step *t*. The discrete time step is Δ. Our approach outputs consuming more timesteps. 

the acceleration of each vehicle. 

In our scenario, the vehicles need maximize their speed, and simultaneously guarantee safety within an episode. As a result, *B. RL Formulation*

our reward function is composed of three macro perspectives: 1\) traffic efficiency; 2\) collision avoidance \(for safety\); The coordination problem has the following assumptions: As for the efficiency, the low-speed and the long waiting time a\) CAVs can communicate perfectly with each other during at the control and intersection zone can be penalized, and the the training process. 

higher speed than the predefined threshold is encouraged. The b\) Each CAV can only observe its own position, speed. 

expression is shown as:

Moreover, to make this application partially observable, CAVs are set not to observe the information of HDVs *N*



*N*



=

\) \+

surrounded. 

*reff*

*−*

*α* 1 *· * I\( *vi < Vmin* *α* 2 *· vi*

\(9\)

c\) The lateral behaviors of CAV are predefined. 

*i*=1

*i*=1

d\) The behaviors of HDVs are controlled by IDM. 

in which I\( *·*\) is the indicator function denoting that the function The main goal of our distributed controller is to output the value is set to 1 if *vi < Vmin *\(where *vi * is the normalized speed longitudinal acceleration for each vehicle. Depending on those ranging from 0 to 1, *Vmin * is the minimal allowed speed for assumptions, the transform to RL problem is shown as follows. 

vehicles in this scenario\), or 0 otherwise. The rest of parameters: *1\) State, Observation and Action Space: * The observation *α* 1 *, α* 2 are adjustable during the training. 

space of each CAV contains the following information \(the The safety of each vehicle can be guaranteed by the setting of notations are consistent with that in the Dec-POMDP definition\): the reward function such that the collision cases can be severely punished. This part is formulated as follows: *oi *= \[ *x*

\]

*i, yi, vi*

\(8\)

*N*



in which \[ *x*

\]

= *−*

*i, yi, vi*

presents the individual vehicle’s \( *i *=

*rca*

*α* 3 *· * I\(Collision\)

\(10\)

1 *, * 2 *, . . . , * 8\) position in Cartesian coordinated originated at the *i*=1

intersection center and speed respectively. Consequently, the where the collision is detected by the relative distance of ve-global state space is simply the concatenation of all individ-hicles. Compared to enumerating all conflict points at the inual’s observations, i.e., *s *= \[ *oi*\] *N *, where *i*=1

*N * is the number of

tersection, this setup can reduce the computational complexity controlled CAVs. 

and ease the implementation in practice. *α* 3 is also a variable As for the actions taken by the agents, some RL research parameter during the training. 

endeavors to deal with the continuous action to control real-Besides, in our scenario, each episode with a fixed length will world robotic tasks \[20\], \[27\]. However, we construct a discrete record the number of collision times where the collision criterion action space for the purpose of lower computational demand. It is that the relative distance of two vehicles \(head-to-tail distance\) is natural to extend the dimensions of the discrete action space is smaller than the predefined threshold shown in Table II. 

for controlling the agents at a smaller granularity level when applied to real-world scenarios. The definition of action and IV. METHODS

joint action space is shown as follows, the individual action *A. Architecture of QMIX Algorithm*

space is *ai *= \[\[ *a *\] *p*

\] *p *\]

*j*

coded in a one-hot manner, 

*j*=1 *, * 0 *, *\[ *dj j*=1

where *p * denotes the granularity of discretization. Only one The framework of QMIX with a detailed description of input element can be selected at each time step. For example, an and output is shown in Fig. 2. The agent network and mixing action may be \[1,0,0,0,0,0,0\] \(where *p *= 3\), meaning that the network are two pedestals of this approach from the forward agent *i * will accelerate with *a* 1. The acceleration and deceleration perspective and all controlled agents share the same networks is clamped not to surpass the corresponding extremums. The \(i.e., parameter sharing\). The merit of parameter sharing is that joint action space is the concatenation of individual action, it can considerably avoid the scalability issue as the dimension

\[ *ai*\] *N *.To facilitate the policy training, we collect the his- of action space does not explode with the increasing number *i*=1

tory action-observation trajectories as *τ i *= \( *oi × ai*\) for each of learning agents. The input to the agent network is the local agent. Moreover, the action masking mechanism similar to the observation vector of each vehicle plus its identification vector Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 03,2025 at 13:46:33 UTC from IEEE Xplore. Restrictions apply. 



GUO et al.: COORDINATION FOR CONNECTED AND AUTOMATED VEHICLES AT NON-SIGNALIZED INTERSECTIONS

3029

TABLE II

TABLE III

SIMULATION PARAMETERS

RL ENVIRONMENT PARAMETERS

each agent adopts the -greedy policy \( * * controls the balance of exploration and exploitation of each agent, decreasing with the rising number of training steps\) to choose the action. 

*B. Implementation Tricks*

Recent work demonstrates that improving the code-level implementations of QMIX can positively affect its asymptotic performance \[18\]. Therefore, we are inspired to perform the following tricks:

1\) The eligibility traces based on Peng’s Q\( *λ*\) \[30\] method is exploited in our work. This trick empirically enables QMIX to become stable and converge faster and avoids the significant bias against bootstrap returns caused by non-sufficiently trained Q networks \[18\]. The formula of Peng’s Q\( *λ*\) for the mixing network is shown below:

*∞*



*Gλ *˙= \(

*λn−* 1

*l*

1 *− λ*\)

*Gl*: *l*\+ *n*

*n*=1

*l*\+ *n*



Fig. 2. 

The overall architecture of QMIX algorithm with specified input and *G*

˙=

\+

max

\(

; 

\)

*l*: *l*\+ *n*

*γt−lrt*

*γn*\+1

*Qtot τ , a, st θtot*

output using the related definitions of intersection scenario, where FC is short for

## a

fully connected layer, the alphanumeric description after FC aims to distinguish *t*= *l*

each FC layer and GRU for the gated recurrent network. 

\(11\)

coded in one-hot form. It outputs the estimate of action value *Q*

in which *Gλ * replaces the *y* target in \(1\), and *λ * is the *i*

*l*

*t*

of the agent *i * which is fed into the mixing network. The mixing discount factor of traces with the property that *λ *= 1

*l*=1

network then takes as input the global state of the environment when *t *= 0. 

plus the estimate of actions values. It utilizes the hypernetworks 2\) Clipping the reward at each time step to a fixed range can composed of several fully connected network layers with dif-stabilize the training for deep Q learning \[22\]. We regard ferent activation functions such as rectified linear unit \(ReLU\) this range as an adjusTable.parameter, and the value is units \[28\] to compute the weights and biases *W*

shown in Table III . 

1 *, W* 2 *, b* 1 *, b* 2. 

One further significant remark is that the hypernetwork uses 3\) Network-level improvements: after tweaking the compo-an absolution operation to generate weights *W*

nents at the network level, we find out that it is useful to 1 *, W* 2 such that

the monotonicity constraint can be properly enforced and hence alter the optimizer of the QMIX from RMSProp \[15\] to makes it a sufficient condition for IGM principle. 

Adam \[31\] with exponentially decaying learning rate \[32\], 

The eventual output of the mixing network is *Q*

improve the initialization of network parameters from *tot*, a rough

estimate of the immediate team reward after the joint actions a uniform distribution to the Xavier normal distribu-are taken by agents. The parameters of all networks are updated tion \[33\], and employ the orthogonal initialization for by the gradient descent algorithm by computing the gradient of GRU. The experimental results in section V show the im-the loss function. The full implementation of QMIX is based on proved efficacy of QMIX with our implementation tricks Pytorch \[29\], a machine learning library. During the training, compared to the original one. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 03,2025 at 13:46:33 UTC from IEEE Xplore. Restrictions apply. 



3030

IEEE TRANSACTIONS ON VEHICULAR TECHNOLOGY, VOL. 72, NO. 3, MARCH 2023

TABLE IV

HYPERPARAMETERS IN QMIX TRAINING

TABLE V

PARAMETERS OF PPO

Fig. 3. 

The training process of the modified QMIX, the original QMIX and PPO. including \(a\) the change of episode reward, and \(b\) records of the change of the number of collisions per episode. The experiments are conducted under three random seeds. \(a\) Episode Reward versus Episodes. \(b\) Collision Times vs Episodes. 

V. SIMULATION AND ANALYSIS

*A. Experimental Settings*

the density 150veh/hour/lane. Afterward, the density of traffic flow is doubled to 300veh/hour/lane, and on which the modified For clarity, Fig. 1 illustrates the DRL-controlled CAVs colored QMIX policy is trained. Furthermore, all training processes are in red and IDM-controlled HDVs colored in yellow, and Table II

conducted under three random seeds to exclude the influence shows the parameters of our simulation environment established of randomness. During the training phase, the policy with the on SUMO 1.10.0. To ease the implementation and environment maximum reward and the minimum number of collisions is construction, we set the lane length of each road segment to stored and evaluated by average speed and fuel consumption 100 m, and vehicles in traffic flow with different density val-metrics. Besides, the hyperparameters of the QMIX algorithm ues \(150 and 300veh/hour/lane\) approach the intersection at and some tricks-related parameters throughout the training stage random speeds. Moreover, the absolution value of discretiza-are jointly summarized in Table IV. All simulations were con-tion granularity of acceleration and deceleration is symmetric, 

\[

ducted on a single computer with 3.7 GHz Intel\(R\) Core\(TM\) 1 *. * 5 *, * 2 *. * 5 *, * 3 *. * 5\] m/s2. 

i7-8700 K CPU and NVIDIA GeForce RTX 2080 GPU. 

Table III summarizes all parameters related to the RL problem, specifying the dimensions of state, action space, and max-B. Comparison of QMIX Policy and PPO Under a Fixed imum steps of one episode. 

*Traffic Density*

To the best of our knowledge,PPO is the most commonly used DRL algorithm applied to the non-signalized intersection \[5\], 

We first compare the learning performance comprising the

\[8\], \[9\], \[25\]. The parameters of the PPO we implement are change of episode reward and the number of collisions in one shown in Table V. Hence, we first train two MDRL algorithms, episode, as shown in Fig. 3, in which the maximal and minimal including the original and modified QMIX and one single-agent values determine the shaded area implying the variance in each DRL algorithm PPO, in the scenario with the traffic flow of subplot. In Fig. 3\(a\), the episode reward of the modified QMIX

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 03,2025 at 13:46:33 UTC from IEEE Xplore. Restrictions apply. 



GUO et al.: COORDINATION FOR CONNECTED AND AUTOMATED VEHICLES AT NON-SIGNALIZED INTERSECTIONS

3031

Fig. 4. 

A set of snapshots produced by SUMO-GUI at different timesteps with several illustrative marks aims to demonstrate the efficacy of the modified QMIX

policy to coordinate vehicles at a non-signalized intersection under the traffic flow of 150veh/hour/lane. The color of each vehicle marks its current speed. 

\(a\) At Timestep 3.7 s. \(b\) At Timestep 6.5 s. \(c\) At Timestep 9.2 s. \(d\) At Timestep 12.1 s. 

first climbs quickly to nearly the maximum value under the effect of Xavier normal and orthogonal initialization schemes introduced in section IV. As the progress of active exploration, agents may first fall into poor decisions, in which the episode reward collapses. Then they learn from their erratic experiences and gradually find the correct action, as they change the strategy from exploration to exploitation. In the end, the episode reward for the modified QMIX converges with the minimum variance compared to the other two methods. The variance of episode reward for the original QMIX is monstrous, which may be Fig. 5. 

\(a\) The average speed of all vehicles on the road, where CAVs are caused by the lack of reward clipping, the absence of eligibil-controlled by the stored policies \(the modified QMIX, the original QMIX, and PPO\) in one episode. \(b\) The average fuel consumption of all vehicles on the ity traces, and network-level improvements. Moreover, it does road, in which CAVs are controlled by stored policies \(the modified QMIX, not converge, and the mean of its asymptotic performance is the original QMIX, and PPO\) in one episode. \(a\) Average Speed vs Timestep. 

significantly lower than the modified counterpart. 

\(b\) Average Fuel Consumption vs Timestep. 

Moreover, although the learning performance of PPO stays superior at the beginning of the training, it becomes weakened with the exploration progress, and its final mean of the episode 3.7 s, CAV 5 enters the junction with a maximal speed of 15 m/s, reward declines and becomes lower than that of the modified and the rest of the vehicles on the road attempt to accelerate. 

QMIX with more variance. In Fig. 3\(b\), the number of collisions Afterward, at 6.5 s, vehicle 4 leaves the intersection zone with of modified QMIX finally converges to nearly zero with slight maximum speed, and vehicles 0, 2, and 6 speed up to enter the fluctuation. Unsurprisingly, the values in the curves of the other junction. Only one vehicle \(with index 1\) enters the intersection two intend to diverge as the progress of training, which raises the at 9.2 s. Finally, vehicles 3 and 7 enter the zone, and the others safety issue and indicates the divergence of these two algorithms. 

accelerate to maximum speed to leave the control zone. 

During the training process, we store the model of each Then we evaluate the stored models of these three algorithms DRL or MDRL algorithm with the highest reward and the under three metrics: \(1\) The change of average speed of all lowest number of crashes. Moreover, we take the snapshots of vehicles in the scenario with timestep in one episode. \(2\) The the trained QMIX policy with implementation tricks to intu-change of average fuel consumption of all vehicles with timestep itively illustrate its emergent behaviors under the traffic flow of per episode. \(3\) The number of collisions per episode for these 150veh/hour/lane, as shown in Fig. 4. Since this traffic density is three algorithms. These experimental results are recorded as relatively low, each road segment for a particular time duration

Fig. 5 and Table VI. In Fig. 5\(a\), the speed pattern of the modified only contains CAVs, and after they pass through the intersection QMIX model first moves up from the initial speed value and safely, a time period in which there are no vehicles exists. At swiftly reaches nearly the maximum speed. The climbing phase Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 03,2025 at 13:46:33 UTC from IEEE Xplore. Restrictions apply. 



3032

IEEE TRANSACTIONS ON VEHICULAR TECHNOLOGY, VOL. 72, NO. 3, MARCH 2023

TABLE VI

COMPARISON OF QMIX AND PPO

and plateau of speed correspond to the time duration when vehicles enter and leave the intersection and finally leave the control zone, respectively. The zero average speed afterward in this curve represents a period where no vehicle is on the road since one group of CAVs controlled by QMIX efficiently leaves the intersection, and the next group is awaiting to be generated by the SUMO simulator. The longer this period becomes, the more efficient the traffic can be under lower traffic density. This phenomenon will disappear when the traffic density increases, as shown in the next subsection. The line graph of fuel consumption follows an approximate opposite trend with some spikes as shown in 5\(b\). The average fuel consumed by all vehicles on the road decrease with fluctuations as they speed up, and the spikes appear when vehicles drive to their maximum speed or constantly change their decisions of accelerating or slowing down. 

However, the other two methods’ speed and fuel consumption patterns are not as clear as the modified QMIX. Concerning the speed profile of vehicles controlled by the pure QMIX model, the speed-increasing rate and the duration of zero speed are lower than the modified one. Vehicles frequently change their speed, leading to variations during the climbing phase. The behavior of more frequent alternation between the acceleration and deceleration emerges in the baseline case \(PPO\), causing the Fig. 6. 

The training process of applying the modified QMIX algorithm to traffic inefficiency and more consumption of fuels shown in 5\(b\). 

different traffic densities with values 150veh/hour/lane and 300veh/hour/lane under three random seeds. \(a\) The change of episode reward under two different As summarized in Table VI, vehicles controlled by the modified traffic densities, and \(b\) the change of the number of collisions under two QMIX can drive with the most significant average speed at different traffic densities. \(a\) Episode Reward versus Episodes. \(b\) Collisions 13.52 m/s and consume the least average fuel of 2.06 ml/s Times versus Episodes. 

among these three approaches. Noticeably, these values are computed by wiping out the zero-speed duration. Moreover, these two QMIX methods can eliminate the phenomenon of agents explore the environment, the reward signal may dra-vehicle crashes, but PPO cannot. 

matically fall due to the wrong decision sequences of different acceleration or deceleration values, despite the problem formulation containing the action masking mechanism described in *C. Comparison of Results on Different Scenario Cases* the previous section. Seemingly, the task of coordinating fewer In this part, we double traffic density to 300veh/hour/lane vehicles on the road may cripple policy training. The reason and retrain our modified QMIX algorithm for this scenario. 

may be that this circumstance brings more local optima to the The influence of more vehicles on the training process is first learning process and confuses the algorithm not to find the global demonstrated, where the randomness of learning is eliminated optimum, obtaining the maximal reward and lowest collisions. 

by training on three random seeds, similar to the previous subsec-Further, the reward under the scenario with more dense traffic tion. Then we evaluate the average speed, fuel consumption, and asymptotically exceeds the counterpart of lower traffic flow since the number of collisions of the stored model with the maximum more vehicles with high speed can accumulate more rewards reward and the minimum crashes during the training stage and during one episode \(9\). The convergence of our modified QMIX

compare it with its counterpart in the 150veh/hour/lane scenario. 

applied to both scenarios validates its efficacy. In Fig. 6\(b\), at the Some insights can be obtained from the learning curves in beginning, the car crashes is substantially higher than the period

Fig. 6 under different traffic densities. In general, the reward-afterward. Although these values under both scenarios tend to learning processes under both scenarios \(Fig. 6\(a\)\) eventually converge as the learning rewards, the scenario of more vehicles converge. Both demonstrate substantial variances \(as shown in on the road eventually demonstrates slightly more crashes than the shaded area\) during the early heavy exploration period. When the lower traffic scene. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 03,2025 at 13:46:33 UTC from IEEE Xplore. Restrictions apply. 

GUO et al.: COORDINATION FOR CONNECTED AND AUTOMATED VEHICLES AT NON-SIGNALIZED INTERSECTIONS

3033

TABLE VII

COMPARISON UNDER DIFFERENT DENSITIES

safety constraints. In Fig. 7\(b\), the pattern of average fuel consumption becomes noisy in the case of more dense traffic. The spikes with high instantaneous fuel consumption are reduced, resulting from a lower speed-increasing rate and a small gap between the accelerations at consecutive steps. 

Table VII summarizes the metrics of comparative study between two scenarios. Although the overall average speed decreases when the traffic density doubles, the average fuel consumption is reduced. Unfortunately, few crashes emerge in the dense traffic scenario under the control of our modified QMIX, reflecting the difficulty of generalizing the DRL policy to more realistic traffic scenarios with a large number of vehicles. We leave it to the focus of our future work. 

VI. CONCLUSIONS AND FUTURE WORKS

This paper applies the QMIX algorithm with implementation tricks to coordinate several CAVs at a non-signalized intersection under different densities of mixed-autonomy traffic. First, we conduct a comparative study using the state-of-the-art DRL

algorithm, PPO, applied in this area and the original QMIX

method under the lower traffic density. The results show that our approach’s convergence rate and asymptotic performance beat the others. The model obtained by our algorithm improves the average speed without collisions and coordinates vehicles to leave the intersection with the least fuel consumption. Further, Fig. 7. 

\(a\) The comparison of the average speed of all vehicles on the road, the modified QMIX is trained under the doubled traffic density, where CAVs are controlled by the modified QMIX policy, under different where the reward signal eventually converges. Consequently, densities of traffic flow. \(b\) The comparison of the average fuel consumption the stored model can still keep the fuel consumption low, al-of all vehicles on the road, where CAVs are controlled by the modified QMIX

policy, under different densities of traffic flow. 

though slightly reducing the efficiency of vehicles and creating marginally more collisions than the lower-traffic counterpart, implying the difficulty of generalizing RL policy to more advanced scenarios. 

We store the model with the maximum reward and the mini-In the future, we will attempt to assign more explicit credits to mum crashes during the training stage as the previous subsection each vehicle when they are approaching the intersection by the does and compare it with the model under the traffic flow Shapley value in coalitional game theory, inadvertently improve of 150veh/hour/lane using the same three metrics. First, from the interpretability of our algorithm. Second, to avoid crashes, 

Fig. 7\(a\) and \(b\), both of the zero plateaus under the traffic den-we will allow agents to safely explore the environment with sity of 150veh/hour/lane disappear since the speed of simulator higher traffic density, which is consistent with the requirements \(SUMO\) generating vehicles becomes faster due to the doubled of real-world applications. 

traffic density. However, the speed pattern of more dense traffic is not the same as the scenario with fewer vehicles. Especially in this figure, the rate of speeding becomes lower. The average REFERENCES

speed tends to grow from the initial speed to a value slightly

\[1\] J. Rios-Torres and A. A. Malikopoulos, “A survey on the coordination of lower than the maximum speed of 15 m/s and infrequently strikes connected and automated vehicles at intersections and merging at highway this maximum value. Subsequently, when there are no vehicles on-ramps,” *IEEE Trans. Intell. Transp. Syst. *, vol. 18, no. 5, pp. 1066–1077, May 2017. 

on the road, the average speed value decreases to the random

\[2\] L. Chen and C. Englund, “Cooperative intersection management: A initial speed for the next group of vehicles. Afterward, it rises survey,” *IEEE Trans. Intell. Transp. Syst. *, vol. 17, no. 2, pp. 570–586, again, corresponding to the fact that these vehicles coordinate to Feb. 2016. 

\[3\] P. Koonce and L. Rodegerdts, “Traffic signal timing manual,” United pass the intersection. Moreover, the vehicles may occasionally States. Federal Highway Administration, Washington, D.C., USA, Tech. 

decelerate to avoid crashes due to the reward function imposing Rep., FHWA-HOP-08-024, 2008. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 03,2025 at 13:46:33 UTC from IEEE Xplore. Restrictions apply. 





3034

IEEE TRANSACTIONS ON VEHICULAR TECHNOLOGY, VOL. 72, NO. 3, MARCH 2023

\[4\] P. Varaiya, “The max-pressure controller for arbitrary networks of signal-

\[29\] A. Paszke et al., “Pytorch: An imperative style, high-performance deep ized intersections,” in *Advances in Dynamic Network Modeling in Complex* learning library,” in *Proc. Adv. Neural Inf. Process. Syst. *, 2019, vol. 32, *Transportation Systems*. Berlin, Germany: Springer, 2013, pp. 27–66. 

pp. 8026–8037. 

\[5\] Y. Guan, Y. Ren, S. E. Li, Q. Sun, and K. Li, “Centralized cooperation for

\[30\] J. Peng and R. J. Williams, *Incremental Multi-Step Q-Learning*. Amster-connected and automated vehicles at intersections by proximal policy op-dam, The Netherlands: Elsevier, 1994. 

timization,” *IEEE Trans. Veh. Technol. *, vol. 69, no. 11, pp. 12597–12608, 

\[31\] D. P. Kingma and J. Ba, “Adam: A method for stochastic optimization,” 

Nov. 2020. 

in *Proc. Int. Conf. Learn. Representations*, 2015, pp. 1051–1060. 

\[6\] H. Wei, G. Zheng, H. Yao, and Z. Li, “Intellilight: A reinforcement learning

\[32\] A. Senior, G. Heigold, M. Ranzato, and K. Yang, “An empirical study of approach for intelligent traffic light control,” in *Proc. 24th ACM SIGKDD*

learning rates in deep neural networks for speech recognition,” in *Proc. *

*Int. Conf. *, 2018, pp. 2496–2505. 

*IEEE Int. Conf. Acoust., Speech, Signal Process. *, 2013, pp. 6724–6728. 

\[7\] D. Isele, R. Rahimi, A. Cosgun, K. Subramanian, and K. Fujimura, 

\[33\] X. Glorot and Y. Bengio, “Understanding the difficulty of training deep

“Navigating occluded intersections with autonomous vehicles using deep feedforward neural networks,” in *Proc. 13th Int. Conf. Artif. Intell. Statist. *

reinforcement learning,” in *Proc. IEEE Int. Conf. Robot. Automat. *, 2018, *Workshop Conf. Proc. *, 2010, pp. 249–256. 

pp. 2034–2039. 

\[8\] E. Vinitsky et al., “Benchmarks for reinforcement learning in mixed-autonomy traffic,” in *Proc. Conf. Robot Learn. *, 2018, pp. 399–409. 

\[9\] B. Peng, M. F. Keskin, B. Kulcsár, and H. Wymeersch, “Connected Zihan Guo received the B.S. degree from the Glas-autonomous vehicles for improving mixed traffic efficiency in unsignalized gow College, University of Electronic Science and intersections with deep reinforcement learning,” *Commun. Transp. Res. *, Technology, Chengdu, China, in 2019. He is currently vol. 1, no. 1, 2021, Art. no. 100017. 

working toward the Ph.D. degree with the Institute

\[10\] W. Zhu, J. Wu, T. Fu, J. Wang, J. Zhang, and Q. Shangguan, “Dynamic of Electrical Engineering, Chinese Academy of Sci-prediction of traffic incident duration on urban expressways: A deep ences, Beijing, China. His research interests include learning approach based on LSTM and MLP,” *J. Intell. Connected Veh. *, multiagent reinforcement learning and autonomous vol. 4 no. 2, pp. 80–91, 2021. 

driving. 

\[11\] F. Belletti, D. Haziza, G. Gomes, and A. M. Bayen, “Expert level control of ramp metering based on multi-task deep reinforcement learning,” *IEEE*

*Trans. Intell. Transp. Syst. *, vol. 19, no. 4, pp. 1198–1207, Apr. 2018. 

\[12\] P. Hernandez-Leal, B. Kartal, and M. E. Taylor, “A survey and critique of multiagent deep reinforcement learning,” *Auton. Agents Multi-Agent Syst. *, Yan Wu received the Ph.D. degree in power electron-vol. 33, no. 6, pp. 750–797, 2019. 

ics and electric drives from the Institute of Electrical

\[13\] Y. Yang and J. Wang, “An overview of multi-agent reinforcement learning Engineering, Chinese Academy of Sciences, Beijing, from game theoretical perspective,” 2020, *arXiv:2011.00583*. 

China, in 2019. She is currently an Associate Profes-

\[14\] P. Sunehag et al., “Value-decomposition networks for cooperative multi-sor with the Department of Vehicle Energy System agent learning based on team reward,” in *Proc. 17th Int. Conf. Auton. *

and Control Technology, Institute of Electrical Engi-Agents MultiAgent Syst. , 2018, pp. 2085–2087. 

neering, Chinese Academy of Sciences. Her research

\[15\] T. Rashid, M. Samvelyan, C. Schroeder, G. Farquhar, J. Foerster, and interests include vehicle network information secu-S. Whiteson, “QMIX: Monotonic value function factorisation for deep rity, X-by-wire systems, vehicle motion control, and multi-agent reinforcement learning,” in *Proc. Int. Conf. Mach. Learn. *, intelligent vehicle technology. 

2018, pp. 4295–4304. 

\[16\] K. Son, D. Kim, W. J. Kang, D. E. Hostallero, and Y. Yi, “QTRAN, Learning to factorize with transformation for cooperative multi-agent reinforcement learning,” in *Proc. Int. Conf. Mach. Learn., * 2019, Lifang Wang received the Ph.D. degree in automo-pp. 5887–5896. 

bile engineering from Jilin University, Jilin, China, 

\[17\] Y. Yang et al., “Multi-agent determinantal Q-learning,” in *Proc. Int. Conf. *

in 1997. Then, she joined the Institute of Electrical *Mach. Learn. *, 2020, pp. 10757–10766. 

Engineering, Chinese Academy of Sciences, Beijing, 

\[18\] J. Hu, S. Jiang, S. A. Harding, H. Wu, and S.-w. Liao, “RIIT: Rethinking China. During the Chinese tenth five-year plan \(2001–

the importance of implementation tricks in multi-agent reinforcement 2005\), she was a Member of the National Specialist learning,” 2021, *arXiv:2102.03479*. 

Group of the Key Special Electric Vehicle Project of

\[19\] M. Samvelyan et al., “The starcraft multi-agent challenge,” in *Proc. 18th* the National 863 Program, and she was the Head of *Int. Conf. Auton. Agents MultiAgent Syst. *, 2019, pp. 2186–2188. 

the 863 Special EV Project Office. She is currently the

\[20\] R. Lowe, Y. WU, A. Tamar, J. Harb, O. Pieter Abbeel, and I. Mor-Director of the Department of Vehicle Energy System datch, “Multi-agent actor-critic for mixed cooperative-competitive en-and Control Technology, Institute of Electrical Engi-vironments,” in *Proc. Adv. Neural Inf. Process. Syst. *, 2017, vol. 30, neering, Chinese Academy of Sciences. She is also the Vice Director of the pp. 6379–6390. 

Key Laboratory of Power Electronics and Electric Drives, Chinese Academy of

\[21\] C. Amato, G. Chowdhary, A. Geramifard, N. K. Üre, and M. J. Kochender-Sciences. She has authored or coauthred more than 60 papers and 30 patents fer, “Decentralized control of partially observable Markov decision pro-and directed more than 15 projects in her research field, which include electric cesses,” in *Proc. 52nd IEEE Conf. Decis. Control*, 2013, pp. 2398–2405. 

vehicle control systems, EV battery management systems, wireless charging

\[22\] V. Mnih et al., “Human-level control through deep reinforcement learning,” 

systems for EVs, electromagnetic compatibility, and smart electricity use. 

*Nature*, vol. 518, no. 7540, pp. 529–533, 2015. 

\[23\] M. Tan, “Multi-agent reinforcement learning: Independent vs. cooperative agents,” in *Proc. 10th Int. Conf. Mach. Learn. *, 1993, pp. 330–337. 

\[24\] A. Tampuu et al., “Multiagent cooperation and competition with deep Junzhi Zhang received the Ph.D. degree in automo-reinforcement learning,” *PLoS One*, vol. 12, no. 4, 2017, Art. no. e0172395. 

bile engineering from Jilin University, Jilin, China, 

\[25\] D. Quang Tran and S.-H. Bae, “Proximal policy optimization through a in 1997. Since 1998, he has been working with the deep reinforcement learning framework for multiple autonomous vehi-Department of Automotive Engineering, Tsinghua cles at a non-signalized intersection,” *Appl. Sci. *, vol. 10, no. 16, 2020, University, Beijing, China. He is the Chairman of the Art. no. 5722. 

International Electric Vehicle Conference Commit-

\[26\] M. Treiber, A. Hennecke, and D. Helbing, “Congested traffic states in tee, the Expert of the National Energy Conservation empirical observations and microscopic simulations,” *Phys. Rev. E*, vol. 62, and New Energy Vehicle 863 Project Planning Group, no. 2, 2000, Art. no. 1805. 

and the Director of the Electric Vehicle Industry Tech-

\[27\] T. P. Lillicrap et al., “Continuous control with deep reinforcement learn-nology Innovation Alliance. His research interests ing,” in *Proc. Int. Conf. Learn. Representations*, 2016, pp. 834–843. 

include braking energy feedback and dynamic control

\[28\] V. Nair and G. E. Hinton, “Rectified linear units improve restricted of the electric vehicle, energy management and control of hybrid electric boltzmann machines,” in *Proc. 27th Int. Conf. Int. Conf. Mach. Learn. *, vehicles, matching the design of the hybrid electric vehicle, and design and 2010, pp. 807–814. 

control of the hybrid transmission. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on August 03,2025 at 13:46:33 UTC from IEEE Xplore. Restrictions apply. 


**



