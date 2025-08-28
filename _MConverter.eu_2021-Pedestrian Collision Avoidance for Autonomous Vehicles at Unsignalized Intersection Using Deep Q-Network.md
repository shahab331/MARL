Pedestrian Collision Avoidance for Autonomous Vehicles at Unsignalized Intersection Using Deep Q-Network Kasra Mokhtari1 and Alan R. Wagner2

Abstract— Prior research has extensively explored Autonomous Vehicle \(AV\) navigation in the presence of other vehicles, however, navigation among pedestrians, who are the most vulnerable element in urban environments, has been less examined. This paper explores AV navigation in crowded, unsignalized intersections. We compare the performance of different deep reinforcement learning methods trained on our reward function and state representation. The performance of these methods and a standard rule-based approach were evaluated in two ways, first at the unsignalized intersection on which the methods were trained, and secondly at an unknown unsignalized intersection with a different topology. For both scenarios, the rule-based method achieves less than 40%

collision-free episodes, whereas our methods result in a performance of approximately 100%. Of the three methods used, DDQN/PER outperforms the other two methods while it also shows the smallest average intersection crossing time, Fig. 1: A bird’s eye view of unsignalized intersection is the greatest average speed, and the greatest distance from depicted. The global axes are presented with the blue the closest pedestrian. 

arrows. The region of interest \(ROI\) is shown by the I. I

green grid. For better visualization, the grid is displayed NTRODUCTION

as larger than was used in the simulation \(best viewed According to the U.S. Federal Highway Administra-in color\). 

tion, approximately 40% of car accidents and almost 70% of fatalities occur at unsignalized intersections \[1\]. 

Driving through urban unsignalized intersections without the guidance of centralized traffic lights and traffic signs This paper explores the potential use of deep rein-is a challenging task for autonomous vehicle \(AV\). In forcement learning methods as a means to design a these scenarios, an AV must autonomously decide when real-time controller for an AV navigation through an and how to navigate an intersection safely and efficiently, unsignalized intersection crowded with pedestrians in accounting for the intention of pedestrians, cyclists, and a high-fidelity simulation such as CARLA. We com-other cars. 

pare three potential methods for deep reinforcement Reinforcement learning \(RL\) combined with deep learning: deep Q Networks \(DQN\) \[8\], Double DQNs arXiv:2105.00153v1 \[cs.RO\] 1 May 2021

learning has achieved outstanding success in various \(DDQN\) \[9\], and DDQNs integrated with prioritized areas such as video games \[2\] and robotics \[3\]. These experience replay \(DDQN/PER\) \[10\]. Our environment advances have inspired the research community to ex-is depicted in Figure 1 using CARLA, an open-source amine the performance of deep reinforcement learning simulator. To the best of our knowledge, using the in autonomous driving \[4\]. Although, prior research 3D state space representation and our unique condi-has extensively explored AV navigation in the presence tional reward function, we have developed the first of other vehicles at unsignalized intersections \[5\], \[6\], decision-making process for autonomous vehicle navi-

\[7\], navigating amongst pedestrians, who are the most gation among crowds that offers safe behavior \(100%

vulnerable element in the urban environment, is under collision-free episodes\) for an AV’s navigation in a explored. 

pedestrians-rich urban setup tested in a high-fidelity autonomous driving simulation. Moreover, our approach 1Department of Mechanical Engineering, The Pennsylvania State can handle different numbers of pedestrians without University, State College, PA 16802, USA kbm5402@psu.edu a noticeable increase in the computation time which 2Department

of

Aerospace

Engineering, 

The

Pennsyl-

vania

State

University, 

State

College, 

PA

16802, 

USA

makes it more suitable for realistic autonomous driving alan.r.wagner@psu.edu

scenarios. 

The remainder of this paper is organized as follows: the environment, and being overly cautious by assuming Section II presents related work, Section III presents the a constant velocity for other cars and pedestrians. 

Markov decision process \(MDP\) framework and deep Reinforcement learning \(RL\) is a promising approach RL \(DRL\) algorithms for three different methods. The for AV navigation around pedestrians. Deshpande et al. 

problem statement and the proposed DRL implementa-explore the use of deep reinforcement learning for navi-tion are discussed in Section IV. Section V introduces gation among pedestrians by training a deep Q-network the simulation setup and the experiment on which we \(DQN\) based on simulation data to cross an intersection examine the performance of the RL approaches. Sec-with pedestrians present \[17\]. They assume a grid-based tion VI demonstrates the performance evaluation results, state-space representation of the environment and an and finally Section VII offers conclusions and directions overly simplified pedestrian model. Unfortunately, the for future work. 

learned policy does not guarantee pedestrian safety. The concept of POMDP planning and reinforcement learning II. RELATED WORK

are integrated in \[18\] to develop efficient policies with Navigation through crowds using small ground vehi-probabilistic safety assurances while also including the cles has been well studied. Museum tour guide robots, AV’s interactions with pedestrians and other vehicles. 

for example, detect and navigate around people who Uncertainty about the other road users’ \(e.g., pedestrians, block the robot’s path \[11\]. The pedestrian dominance cyclists, and other vehicles\) course of action is captured model \(PDM\) proposed in \[12\] is capable of navigat-by the transition model and state uncertainty. Although ing through groups of pedestrians by identifying the this RL method guarantees safe navigation of the AV

dominant characteristics of these groups based on their around the pedestrians, the computation time drastically trajectories. The human-aware motion planner \(HAMP\) grows with the number of existing vehicles and pedes-proposed in \[13\], considers the safety of the robot’s trians in the environment \(due to applying the scene movement as well as the human’s comfort while at-decomposition algorithm on every road user\). Therefore, tempting to keep the robot in front of people and visible this approach is not suitable for real-time autonomous at all times. A constraint-optimizing method for per-driving applications. 

son–acceptable navigation \(COMPANION\) \[14\] models III. TECHNICAL BACKGROUND

human social conventions, including avoiding people’s A. Reinforcement Learning

personal space, as well as task-based constraints such as minimizing distance. 

A reinforcement learning task is typically formulated Although these model-based approaches implemented as a Markov decision process \(MDP\) defined by the 5-on ground robots are capable of navigating through tuple \(S, A, P, R\), characterized by a set of states S, groups of pedestrians, they tend to be computationally a set of actions A, state transition probability P , and expensive and hard to adapt to higher dimensional au-a scalar reward function R \[19\]. In a reinforcement tonomous driving problems where there are multiple learning framework, at each time step t, the agent takes road users in the environment. As an alternative, a model an action at based on a policy π\(a|s\), it receives a scalar for negotiating between an AV and a pedestrian at an reward rt and transitions into the next state st\+1 \[20\]. 

unsignalized intersection using discrete sequential game This interaction continues until the agent reaches a theory was developed in \[15\]. However, game-theory terminal state, at which point it restarts. The goal of the models are overly simplified while attempting to capture agent is to maximize the expected discounted reward R

γkr

complex interactions of AVs and pedestrians. A partially t = PT

t=0

t, where a discount factor γ ∈ \(0, 1\]

observable Markov decision process \(POMDP\) has also emphasizes the importance of the future reward. 

been used to model the interactions between pedestrians To tackle this optimization problem, Q-learning and AVs at intersections \[16\]. Yet POMDP algorithms method is employed where actions are selected using0

are generally intractable preventing their application to state-value function Q\(s, a\) \[21\]. The optimal action a different conditions such as scenarios with additional for a state s is computed as:

road users such as other vehicles and pedestrians. One 0

a = arg max Q\(s, a\)

\(1\)

of the most widely used approaches to address the a∈A

pedestrian collision avoidance problem for an AV is In Deep Q-Network \(DQN\), the Q\(s, a\) is approximated a rule-based method built on time-to-collision \(TTC\). 

using a deep neural network \(called online network\) \[8\]. 

The rule-based method identifies and utilizes a set of A Double Deep Q-Network is a variant of DQN, where relational rules that collectively represents the contextual a separate target network for value estimation is used to knowledge captured by the system. While the rule-based make the learning process more stable \[9\]. The target method is relatively reliable and easily interpretable, it network parameters are periodically updated using the has some limitations such as requiring full knowledge of latest parameter of the online network. 

Vertices

Cartesian Coordinates

To train the DQN and DDQN more effectively, re-Rear Right x

EVx \+ L×cos\(θ\) \+ W ×sin\(θ\)

play memory is employed in which the transition se-5

2

Rear Right y

EVy \+ L×sin\(θ\) − W ×cos\(θ\)

5

2

quences are stored in a replay buffer as the 4-tuple Rear Left x

EVx \+ L×cos\(θ\) − W ×sin\(θ\)

5

2

of \(st, at, rt, st\+1\) at every time step \[22\]. The tran-Rear Left y

EVy \+ L×sin\(θ\) \+ W ×cos\(θ\)

5

2

sition includes the current state, the selected action, Front Right x

EVx − 4L×cos\(θ\) \+ W ×sin\(θ\)

5

2

the corresponding received reward, and the subsequent Front Right y

EVy − 4L×sin\(θ\) − W ×cos\(θ\)

5

2

state. Therefore, transitions are uniformly sampled from Front Left x

EVx − L×cos\(θ\) − W ×sin\(θ\)

5

2

Front Left y

EV

\+ W ×cos\(θ\)

replay memory, regardless of their significance. How-y − L×sin\(θ\)

5

2

ever, transitions might vary in their task relevance, and TABLE I: ROI’s Cartesian coordinates therefore, are given different priorities when training the agent. Prioritized experience replay \(PER\) assigns Action

Throttle Value

Description

different sampling weights to each transition based on a0

−1.0

full brake

the calculated Temporal Difference \(TD\) error \[10\]. The a1

−0.4

decelerate

a2

\+0.2

accelerate1

probability of sampling transition i is then defined as: a3

\+1.0

accelerate2

pα

P \(i\) =

i

\(2\)

P

pα

TABLE II: Action Space

k

k

where p\(i\) > 0 is the priority of transition i, k is the total number of transitions in the replay memory l × w as shown in Figure 1. The ROI is constructed and α determines how much priority is desired \(with in such a way that the ego vehicle’s center of gravity α = 0 corresponding to uniform random sampling\). In always lies on a cell with an index \( 4L , W \) and the proportional prioritization, p\(i\) = δ

5l

2w

i \+ , where is a

ROI’s orientation remains the same with respect to the small positive constant. Importance sampling is applied ego vehicle direction. Therefore, given the ego vehicle to avoid the bias in the updated distribution and the location in the global coordinate system \(EVx, EVy\) and importance-sampling \(IS\) weights are computed as: ego vehicle direction EVθ, the ROI vertices Cartesian 1

1

coordinates are shown in Table I. 

w\(i\) = \(

×

\)β

\(3\)

N

P \(i\)

The 3-D tensor state representation contains three 2-where N is the replay memory size, and β determines D grids where the first 2-D grid represents the cells the compensation degree that fully compensates for the that are occupied by the ego vehicle and surrounding non-uniform probabilities P \(i\) if β = 1. In practice, β

pedestrians. Relative speed and relative heading direction linearly anneals from its initial value β

of the corresponding pedestrians with respect to the ego 0 to 1. 

vehicle are captured in the second and the third 2-D

IV. METHODOLOGY

grids, respectively. Speed is expressed in meters per A. Problem Statement

second \(m/s\), and heading direction in degrees. 

We investigate the problem of Autonomous Vehicle We assume that the length and the width of the ego navigation at unsignalized intersection in a structured vehicle are 4.5m and 2.0m, respectively. The ROI’s pedestrian-rich urban setup. A three-way intersection parameters are selected as L = 20m, W = 15m, scenario is considered where the ego vehicle’s goal is l = 0.25m and w = 0.25m. As a result, each 2-D grid to make a left-turn without colliding with pedestrians is an 80 × 60 matrix. The ego vehicle’s center of gravity or violating the speed limit. It is assumed that the occupies cell \(64, 15\) of the first 2-D grid. 

environment is fully observable indicating that pedestrian 2\) Action Space: We control the ego vehicle by information collected by sensors \(such as LIDAR\) is adjusting the throttle value a ∈ \[−1, 1\]. The action space accurate and sufficient to make a decision at every time includes four discrete actions presented in Table II. 

step. The decision-making process is modeled as an 3\) Reward Function: The goal of the ego vehicle is MDP. 

to make a left-turn within a limited time frame \(t =

45 sec\) while avoiding collisions with any pedestrians B. MDP Formulation

and maintaining a speed below the speed limit \(10

1\) State Space: We use a similar approach to \[17\], m/s\). To this end, we designed a conditional reward where the grid-based state space representation is in the function inspired by \[23\] where the switching criteria form of a 3-D tensor which is used to describe the are based on the distance of the ego vehicle’s right and state of the ego vehicle and the pedestrians. A region left bumpers to the closest pedestrians denoted by dright of interest \(ROI\) of the environment around the ego and dleft, respectively. Therefore, at each time step, if vehicle with the length L and the width W is discretized both distances are greater than a threshold d1, the ego into multiple grids each with the grid discretization vehicle receives rewards only based on its distance to





Fig. 2: A reward Function flow chart. 

Hyperprameter

Value

Hyperprameter

Value

d1

7\(m\)

r2

\+0.005

d2

25\(m\)

r3

−0.25

d3

1\(m\)

r4

\+0.25

d4

2\(m\)

r5

−5.0

v1

1.5\(m/s\)

r6

−1.5

v2

10\(m/s\)

r7

−0.25

r1

\+0.005

TABLE III: Reward function hyperparameters the target position \(Xt\) and its velocity \(V \). Otherwise, the ego vehicle receives rewards according to dright and d

Fig. 3: Decision-making process architecture. 

lef t as depicted in Figure 2. The hyperparameters of the reward function are shown in Table III. Since the reward function is designed such that the agent receives the highest reward at the end of the navigation task, vehicle and pedestrian data generated by the CARLA it is not necessary to assign excessive reward when API are then fed into the interface component of the the agent reaches the goal. The ego vehicle reaches a OpenAI Gym toolkit \[25\]. OpenAI Gym is an open-terminal state when it completes the left-turn, collides source library for developing reinforcement learning with a pedestrian, or it runs out of time, and then the algorithms. At every time step, this module calculates episode restarts. The total amount of reward that the ego the grid-based state space representation, the assigned vehicle receives for every episode is the summation of rewards to the ego vehicle, and action mapping as all reward over all of the time steps. 

discussed in Section IV-B. To complete the control loop, a fourth component, the reinforcement learning module V. EXPERIMENTS

constructed using the Tensorflow library selects the best possible discrete action and returns it to the simulation. 

A. Simulation Setup

The system consists of the four components shown in B. Reinforcement Learning Architecture Figure 3. High-level control \(a throttle value\) is generated by the method and low-level control is executed We examine and compare the performance of three by CARLA \[24\], which is an open-source simulator different reinforcement learning methods for our prob-for autonomous driving scenario development. The ego lem. 



Layer

Activation Function

Filters

Units

Kernel Size

stride

Conv1

ReLU

64

-

3 × 3

1 × 1

AVGP1

-

1

-

5 × 5

3 × 3

Conv2

ReLU

64

-

3 × 3

1 × 1

AVGP2

-

1

-

5 × 5

3 × 3

Conv3

ReLU

64

-

3 × 3

1 × 1

AVGP3

-

1

-

5 × 5

3 × 3

FC1

ReLU

-

512

-

-

FC2

ReLU

-

256

-

-

FC3

ReLU

-

64

-

-

FC4

ReLU

-

4

-

-

TABLE IV: Parameters of the RL architecture. 

Fig. 4: Deep Q-network architecture. 

1\) DQN Method: A DQN architecture is shown in Figure 4. The input x1 to the DQN is the 3-D tenor discussed in Section IV-B.1 and the input x to a minimum value of 0.05 using the decay value of 0.99

2 is the ego

vehicle velocity. Three convolutional layers followed by in order to limit the exploratory behavior towards the end an ReLU activation function and an Averagepooling2D

of the training process. For the DDQN/PER method, the layer are used to extract the low-level features of the 3D-prioritization rate α was set to 0.6 and the compensation tensor. The output of the convolutional layers is then rate β was initialized to 0.4 linearly annealing to 1. 

fed into a flatten layer and is concatenated with the D. Scenario

ego vehicle velocity. The new vector is then propagated through four fully connected layers. The parameters of The simulator ran on synchronous mode \(15 FPS\) the network are described in Table IV. 

which involved a constant time interval between each 2\) DDQN Method: For the DDQN, the action selec-step taken by the ego vehicle in the simulation. At the tion and action evaluation tasks are handled with two beginning of every episode, the ego vehicle and a random separate networks, the online network and the target number of pedestrians \(between five and thirty\) were network. Therefore, a DDQN consists of two networks spawned at an unsignalized intersection as shown in where each one shares the DQN structure. The target Figure 1. Five more pedestrians were spawned every ten network parameters are updated after 5000 time steps seconds after the start of the episode. The pedestrians using the latest parameters of the online network. 

moved to random destination points with a random 3\) DDQN/PER Method: This approach combines the velocity between 0.2 − 1.8 m/s. A trajectory was defined DDQN method and PER implementation. To conduct for the ego vehicle by automatically placing a hundred a fair comparison, we use exactly the same DDQN

waypoints between the start point to the endpoint. The architecture as the previous Section V-B.2. 

goal of the ego vehicle was to make a left turn within the specific time while avoiding collision with any pedes-C. Networks Training

trian and not violating the speed limit. Forty-five seconds To generate training data, the unsignalized intersection were allotted for each episode. The speed limit for the left turn scenario was constructed and simulated in ego vehicle was 10 m/s. At each time step, the action CARLA. The networks were trained for 450 episodes. 

generated by the network was executed in the simulator Each step generated a transition and the experience and the network was trained. The ego vehicle reached replay memory buffer stored up to 10,000 transitions. 

the terminal state when it either completes the left-turn, The learning process began when the experience replay collides with a pedestrian, or runs out of time, at which memory reached a threshold of 750 transitions. The point the episode restarts. 

DQN and DDQN methods randomly selected a mini-VI. R

batch of size 32 transitions from the replay memory ESULTS AND DISCUSSION

and then updated the weights of the networks accord-The training performance of the three type of networks ingly. However, the DDQN/PER approach instead used on the unsignalized intersection task is compared in a stochastic sampling method \(Eq. 9\) to choose the same Figure 5. The maximum reward, the minimum reward, size mini-batch of data for training its network. All and the average reward of 10 episodes are compared methods used the RMSprop optimization \[26\] algorithm and the depicted rewards are normalized and smoothed. 

with a learning rate of 0.00025. 

Due to substantial overestimation associated with the During the training process, a discount factor of 0.95

DQN \[9\], it was outperformed by the other two networks. 

was applied to discount future rewards. The greedy Because the DDQN/PER employs a stochastic sampling approach was followed in order to allow the networks to method instead of random sampling to select the training explore at each time step, an action was chosen randomly batch, it trains the most efficiently and exhibits the with a probability of , otherwise, an action is selected by highest normalized maximum, minimum and average the networks. The value was initialized to 1. It annealed reward during the training phase. At the end of the





Fig. 5: RL networks training performance comparison. 

TABLE V: Comparison of test performance results \(a\) The intersection that the DRL networks are trained on method

Collision-free

Successful

episodes

episodes

Rule-based

38%

38%

DQN

99%

82%

DDQN

100%

92%

DDQN/PER

100%

93%

\(b\) An unseen intersection with a different topology method

Collision-free

Successful

episodes

episodes

Rule-based

35%

35%

Fig. 6: Histogram plot of average intersection crossing DQN

99%

85%

time for the rule-based and RL methods. 

DDQN

100%

92%

DDQN/PER

100%

94%

on exactly the same unsignalized intersection on which training process, the average normalized reward for the the networks were trained. For the second experiment, DDQN/PER was 0.07 and 0.13 greater than that of the networks were tested on an unseen unsignalized the DDQN and DQN, respectively. The ascending trend intersection with different topology. The networks were in the normalized maximum, minimum, and average trained on a 25 × 25 three-way unsignalized intersection rewards for all networks suggests that the networks are while the unseen intersection was a 26 × 17 four-way improving. To evaluate the system’s learning, the ability unsignalized intersection. For each experiment, the fol-of each network to navigate the intersection without lowing metrics were used to evaluate the methods’ per-speeding and timing out was examined. 

formance: the percentage of collision-free and successful The different method’s performance was compared in episodes. The successful episodes are the episodes that two experiments. Each experiment included 250 episodes the autonomous vehicle neither had a collision with and used the same definition of the terminal state as used pedestrians, nor ran out of time, nor violated the speed for the training process. The same method for spawning limit. Moreover, we compared the histogram plots of av-the pedestrians at the target unsignalized intersection was erage intersection crossing time \(sec\) \(Figure 6\), average followed. Both experiments compared our methods to a interaction crossing speed \(m/s\) \(Figure 7\), and average rule-based method. The rule-based method is provided distance of ego vehicle from the closest pedestrian \(m\) by CARLA which executes a policy based on a hand-

\(Figure 8\) for the RL methods. 

engineered strategy for navigating around pedestrians. 

The results for the two experiments are presented in The policy mainly relies on a time to collision approach Table V. During both experiments \(according to the to decide when to cross the intersections. 

histogram plots\), although the average speed and the In the first experiment, these methods were tested average intersection crossing time for the rule-based





intersection crossing time \(30.08 sec for experiment one and 27.86 sec for experiment two\), the greatest average speed \(3.38 m/s for experiment one and 3.35 m/s for experiment two\), and the greatest distance from the closest pedestrian \(7.8 m for experiment one and 6.9

m for experiment two\) as depicted in Table V. Overall, the DDQN and DDQN/PER methods are capable of safely navigating through crowds and following the traffic rules for different unsignalized intersections after being trained on one topology and then tested on another topology. 

The related work and their limitations for the problem Fig. 7: Histogram plot of average intersection crossing of autonomous vehicle navigation among pedestrians speed for the rule-based and RL methods. 

are presented in Table VI. Prior approaches to this problem that utilized deep reinforcement learning either have not resulted in a collision-free control of the vehicle, or have not been tested in a pedestrian-rich environment in a high-fidelity autonomous driving simulation, or they are not suitable for the real-time applications. Our method shows that by employing the 3D state space representation of the environment and our innovative conditional reward function combined with the DDQN and DDQN/PER training methods, to the best of our knowledge, we have developed the reinforcement learning-based decision-making process for an AV that is not only safe \(100% collision-free episodes\) but also capable of successfully \(92 − 94% completed navigation tasks episodes\) navigating at unisignalized intersections Fig. 8: Histogram plot of average distance from the in a pedestrian-rich urban environment regardless of closest pedestrian for the rule-based and RL methods. 

the intersection topology. Moreover, due to the small computation time required by the networks, we believe that these methods can be used in real-time. 

method outperforms our methods, 62% and 65% of VII. CONCLUSION

the episodes result in collisions with pedestrians for experiment one and experiment two, respectively. Given This paper has examined three different deep rein-a success rate of only 35% − 40% success rate for forcement learning approaches for controlling an au-completing the left turn, the rule-based method is not a tonomous vehicle as it navigates through an unsignal-viable solution to this problem. Compared to a rule-based ized intersection crowded with pedestrians. Of the three approach, our methods clearly show better performance approaches, the DDQN/PER outperforms the other two with 99%, 100% and 100% collision-free episodes for methods. Comparing these deep reinforcement learning the DQN, DDQN, and DDQN/PER methods, respec-methods to a rule-based method, given the 3D state space tively. Qualitatively, we see that these methods learn to representation and our innovative conditional reward decrease their speed and wait for pedestrians to cross function, we find that the methods: 1\) drastically increase in order to avoid a collision with a pedestrian. These safety during navigation, 2\) are much better at obeying methods are also more successful at completing the the speed limit and 3\) achieve much higher success rate navigation task than rule-based methods. We therefore in a navigation task. We also consider how these methods conclude that our methods are safer then the standard trained on one intersection topology perform on another, rule-based method. 

different topology. The results reveal that our methods According to the histogram plots and their average maintain almost the same performance. 

value for intersection crossing time \(sec\), interaction We have assumed that the environment is fully ob-crossing speed \(m/s\), and distance of ego vehicle from servable and the pedestrian information collected by the the closest pedestrian \(m\), among the three methods, AVs sensors is accurate. Our future work will explore similar to the training results, DDQN/PER outperforms the use of safe deep reinforcement learning \(SDRL\) ap-the other two. This method has the fastest average proaches for the same scenario using a partially observ-

Authors

Results

Limitations

Scenario

Simulation Environment

Did not Use a high-fidelity autonomous Intersection crossing among

Deshpande et al. \[17\]

No collision

driving simulation and the method was SUMO \[27\]

only two pedestrians. 

not tested in a pedestrian-rich environment. 

Used a very simplistic simulated environment and the computation time for this method grows Intersection crossing \(left turn\) They created their

Bouton et al. \[18\]

No collision

drastically with the number of pedestrians around among pedestrians and cars. 

own simulated environment. 

the ego vehicle. 

Did not generate a safe behavior for navigating Intersection crossing when

Deshpande et al. \[28\]

70% collision-free

CARLA

around pedestrians. 

the pedestrians might jaywalk. 

TABLE VI: The related work and the summary of approach for the problem of autonomous vehicle navigation among pedestrians. Unfortunately, because different authors have used different simulation environments and different actions spaces, direct comparison of our approach to these prior methods is not feasible. 

able Markov decision process \(POMDP\) formulation. 

\[15\] C. Fox, F. Camara, G. Markkula, R. Romano, R. Madigan, N. Merat, et al., “When should the chicken cross the road?: Game R

theory for autonomous vehicle-human interactions,” 2018. 

EFERENCES

\[16\] M. Barbier, C. Laugier, O. Simonin, and J. Iba˜nez-Guzmán, 

“Probabilistic decision-making at road intersections: Formulation

\[1\] R. C. Coakley and E. Stollof, “Intersection safety needs iden-and quantitative evaluation,” in 2018 15th International Confer-tification report,” Prepared for Federal Highway Administration ence on Control, Automation, Robotics and Vision \(ICARCV\). 

\(DTFH61-05-D-00026\), 2009. 

IEEE, 2018, pp. 795–802. 

\[2\] R. R. Torrado, P. Bontrager, J. Togelius, J. Liu, and D. Perez-

\[17\] N. Deshpande and A. Spalanzani, “Deep reinforcement learning Liebana, “Deep reinforcement learning for general video game based vehicle navigation amongst pedestrians using a grid-based ai,” in 2018 IEEE Conference on Computational Intelligence and state representation,” in 2019 IEEE Intelligent Transportation Games \(CIG\). 

IEEE, 2018, pp. 1–8. 

Systems Conference \(ITSC\). 

IEEE, 2019, pp. 2081–2086. 

\[3\] J. Kober, J. A. Bagnell, and J. Peters, “Reinforcement learning

\[18\] M. Bouton, A. Nakhaei, K. Fujimura, and M. J. Kochenderfer, in robotics: A survey,” The International Journal of Robotics

“Safe reinforcement learning with scene decomposition for nav-Research, vol. 32, no. 11, pp. 1238–1274, 2013. 

igating complex urban environments,” in 2019 IEEE Intelligent

\[4\] T. Tram, A. Jansson, R. Grönberg, M. Ali, and J. Sjöberg, Vehicles Symposium \(IV\). 

IEEE, 2019, pp. 1469–1476. 

“Learning negotiating behavior between cars in intersections

\[19\] R. S. Sutton and A. G. Barto, Reinforcement learning: An using deep q-learning,” in 2018 21st International Conference introduction. 

MIT press, 2018. 

on Intelligent Transportation Systems \(ITSC\). 

IEEE, 2018, pp. 

\[20\] L. P. Kaelbling, M. L. Littman, and A. W. Moore, “Reinforcement 3169–3174. 

learning: A survey,” Journal of artificial intelligence research, 

\[5\] D. Isele, R. Rahimi, A. Cosgun, K. Subramanian, and K. Fu-vol. 4, pp. 237–285, 1996. 

jimura, “Navigating occluded intersections with autonomous ve-

\[21\] C. J. Watkins and P. Dayan, “Q-learning,” Machine learning, hicles using deep reinforcement learning,” in 2018 IEEE Interna-vol. 8, no. 3-4, pp. 279–292, 1992. 

tional Conference on Robotics and Automation \(ICRA\). 

IEEE, 

\[22\] L.-J. Lin, “Self-improving reactive agents based on reinforcement 2018, pp. 2034–2039. 

learning, planning and teaching,” Machine learning, vol. 8, no. 

\[6\] D. Isele, A. Nakhaei, and K. Fujimura, “Safe reinforcement learn-3-4, pp. 293–321, 1992. 

ing on autonomous vehicles,” in 2018 IEEE/RSJ International

\[23\] M. Everett, Y. F. Chen, and J. P. How, “Collision avoidance in Conference on Intelligent Robots and Systems \(IROS\). 

IEEE, 

pedestrian-rich environments with deep reinforcement learning,” 

2018, pp. 1–6. 

arXiv preprint arXiv:1910.11689, 2019. 

\[7\] T. Liu, X. Mu, B. Huang, X. Tang, F. Zhao, X. Wang, and D. Cao, 

\[24\] A. Dosovitskiy, G. Ros, F. Codevilla, A. Lopez, and V. Koltun, 

“Decision-making at unsignalized intersection for autonomous

“Carla: An open urban driving simulator,” arXiv preprint vehicles: Left-turn maneuver with deep reinforcement learning,” 

arXiv:1711.03938, 2017. 

arXiv preprint arXiv:2008.06595, 2020. 

\[25\] G. Brockman, V. Cheung, L. Pettersson, J. Schneider, J. Schul-

\[8\] V. Mnih, K. Kavukcuoglu, D. Silver, A. A. Rusu, J. Veness, M. G. 

man, J. Tang, and W. Zaremba, “Openai gym,” arXiv preprint Bellemare, A. Graves, M. Riedmiller, A. K. Fidjeland, G. Ostro-arXiv:1606.01540, 2016. 

vski, et al., “Human-level control through deep reinforcement

\[26\] A. Karparthy, “A peek at trends in machine learning,” Medium. 

learning,” nature, vol. 518, no. 7540, pp. 529–533, 2015. 

com, 2017. 

\[9\] H. Van Hasselt, A. Guez, and D. Silver, “Deep rein-

\[27\] P. A. Lopez, M. Behrisch, L. Bieker-Walz, J. Erdmann, Y.-

forcement learning with double q-learning,” arXiv preprint P. Flötteröd, R. Hilbrich, L. Lücken, J. Rummel, P. Wagner, arXiv:1509.06461, 2015. 

and E. Wießner, “Microscopic traffic simulation using sumo,” in

\[10\] T. Schaul, J. Quan, I. Antonoglou, and D. Silver, “Prioritized 2018 21st International Conference on Intelligent Transportation experience replay,” arXiv preprint arXiv:1511.05952, 2015. 

Systems \(ITSC\). 

IEEE, 2018, pp. 2575–2582. 

\[11\] S. Thrun, M. Bennewitz, W. Burgard, A. B. Cremers, F. Dellaert, 

\[28\] N. Deshpande, D. Vaufreydaz, and A. Spalanzani, “Behavioral D. Fox, D. Hahnel, C. Rosenberg, N. Roy, J. Schulte, et al., decision-making for urban autonomous driving in the presence

“Minerva: A second-generation museum tour-guide robot,” in of pedestrians using deep recurrent q-network,” in 2020 16th Proceedings 1999 IEEE International Conference on Robotics International Conference on Control, Automation, Robotics and and Automation \(Cat. No. 99CH36288C\), vol. 3. 

IEEE, 1999. 

Vision \(ICARCV\). 

IEEE, 2020, pp. 428–433. 

\[12\] T. Randhavane, A. Bera, E. Kubin, A. Wang, K. Gray, and D. Manocha, “Pedestrian dominance modeling for socially-aware robot navigation,” in 2019 International Conference on Robotics and Automation \(ICRA\). 

IEEE, 2019, pp. 5621–5628. 

\[13\] E. A. Sisbot, L. F. Marin-Urias, R. Alami, and T. Simeon, “A human aware mobile robot motion planner,” IEEE Transactions on Robotics, vol. 23, no. 5, pp. 874–883, 2007. 

\[14\] R. Kirby, “Social robot navigation,” Ph.D. dissertation, figshare, 2010. 


# Document Outline

+ I Introduction 
+ II Related Work 
+ III Technical Background  
	+ III-A Reinforcement Learning 

+ IV Methodology  
	+ IV-A Problem Statement 
	+ IV-B MDP Formulation  
		+ IV-B.1 State Space 
		+ IV-B.2 Action Space 
		+ IV-B.3 Reward Function 


+ V Experiments  
	+ V-A Simulation Setup 
	+ V-B Reinforcement Learning Architecture  
		+ V-B.1 DQN Method 
		+ V-B.2 DDQN Method 
		+ V-B.3 DDQN/PER Method 

	+ V-C Networks Training 
	+ V-D Scenario 

+ VI Results and Discussion 
+ VII Conclusion 
+ References



