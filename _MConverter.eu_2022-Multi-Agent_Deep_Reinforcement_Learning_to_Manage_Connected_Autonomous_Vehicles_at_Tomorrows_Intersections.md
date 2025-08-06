IEEE TRANSACTIONS ON VEHICULAR TECHNOLOGY, VOL. 71, NO. 7, JULY 2022

7033

Multi-Agent Deep Reinforcement Learning to Manage Connected Autonomous Vehicles at

Tomorrow’s Intersections

Guillen-Perez Antonio

and Cano Maria-Dolores

*, * *Senior Member, IEEE*

***Abstract*****—In recent years, the growing development of Con-requires knowledge of the state of all actors involved in the nected Autonomous Vehicles \(CAV\), Intelligent Transport Systems traffic system \(vehicles, pedestrians, priority vehicles, etc.\). **
** 
\(ITS\), and 5G communication networks have led to the advent Autonomous Intersection Management \(AIM\) systems are of Autonomous Intersection Management \(AIM\) systems. AIMs present a new paradigm for CAV control in future cities, taking designed to efficiently manage CAVs at urban intersections, control of CAVs in scenarios where cooperation is necessary and eliminating collisions, and optimizing overall traffic flow \[2\]. 

allowing safe and efficient traffic flows, eliminating traffic signals. 

AIMs regulate the flow of vehicles through intersections by So far, the development of AIM algorithms has been based on acting on their state \(speed, acceleration, braking, steering, etc.\). 
**
**basic control algorithms, without the ability to adapt or keep This control is usually based on simple rules and the intersec-learning new situations. To solve this, in this paper we present a new** **advanced AIM approach based on end-to-end Multi-Agent Deep** tion’s current state, without considering other vehicle-specific **Reinforcement Learning \(MADRL\) and trained using Curriculum** parameters, environmental conditions, upcoming events, etc. 

**through *Self-Play*****, called advanced Reinforced AIM \( *adv. *****RAIM\). **

\[3\], \[4\]. 

***adv. *****RAIM enables the control of CAVs at intersections in a col-Deep Reinforcement Learning \(DRL\) successfully connects laborative way, autonomously learning complex real-life traffic Reinforcement Learning \(RL\) algorithms with the strengths of dynamics. In addition, *adv*.RAIM provides a new way to build smarter AIMs capable of proactively controlling CAVs in other Deep Neural Networks \(DNN\), accelerating these RL algo-highly complex scenarios. Results show remarkable improvements** rithms’ training processes and performance. As a consequence **when compared to traffic light control techniques \(reducing travel** of this success \[5\], DRL is being introduced in many areas. 

**time by 59% or reducing time lost due to congestion by 95%\), as well** In Multi-Agent \(MA\) environments, multiple *agents * execute **as outperforming other recently proposed AIMs \(reducing waiting** *actions * and can affect the *states * of other *agents*. Traditional **time by 56%\), highlighting the advantages of using MADRL. **

MA-RL algorithms have recently been successfully extended

***Index Terms*****—Autonomous intersection management, connected** with DNNs for MA DRL learning, giving rise to Multi-Agent **autonomous vehicles, deep reinforcement learning, intelligent** DRL \(MADRL\). The reason lies in the availability of high com-transport systems, intersection traffic management, multi-agent putational power and the efficiency of distributed algorithms, **deep reinforcement learning. **

leading to unexpected impressive results such as those obtained by DeepMind \[6\] and OpenAI \[7\]. 

I. INTRODUCTION

Due to the advantages that MADRL can offer for cleverly **T**RAFFIC control is changing rapidly, as Connected Au- finding a cooperative control policy, we decided to explore tonomous Vehicles \(CAVs\) are bringing new opportunities this path. In this work, we detail a new AIM system based to control and manage vehicular, people, and goods flow in and on MADRL, called advanced Reinforced AIM \( *adv. * RAIM\), around our cities. The new Intelligent Transportation Systems and its performance is extensively evaluated in a variety of \(ITS\) are challenged to provide new ways to control CAVs realistic and complex scenarios. The proposed *adv. * RAIM is to reduce congestion, pollution, or accidents \[1\]. Therefore, trained by DRL and uses end-to-end MADRL, along with improving and introducing new control strategies is imperative other advanced methods such as Curriculum through *Self-Play* for efficient traffic management decisions. In recent years, nu-learning and Prioritized Experience Replay \(PER\), to learn and merous approaches have been developed to implement CAVs model the complex dynamics of the environment in the control control algorithms, however, this task is really complex and of CAVs at urban intersections. The final goal of *adv*.RAIM

is to periodically act on the *speed * of all CAVs collectively at intersections to reduce lost time, by eliminating collisions and Manuscript received May 24, 2021; revised January 25, 2022 and April 18, 2022; accepted April 19, 2022. Date of publication April 25, 2022; traffic lights. To the authors’ knowledge, this paper addresses date of current version July 18, 2022. This work was supported in part by the use of end-to-end MADRL in the field of AIM for the first MCIN/AEI/10.13039/501100011033 under Grant PID2020-116329GB-C22, time. Simulation results show that the performance of *adv. * RAIM

and in part by the Fundación Séneca, Región de Murcia, Spain under Grant 20740/FPI/18. The review of this article was coordinated by Dr. Bilal Akin. 

is remarkably superior to other traditional traffic light control The authors are with the Information Technologies and Communication algorithms \(like Fixed Time \(FT\) or *iREDVD *\[8\]\). Furthermore, Department, Universidad Politécnica de Cartagena, 30203 Murcia, Spain when compared to other recently proposed AIMs \[9\], *adv. * RAIM

\(e-mail: antonio.guillen@edu.upct.es; mdolores.cano@upct.es\). 

Digital Object Identifier 10.1109/TVT.2022.3169907

can reduce waiting time by 88%, and time loss by 55%, among This work is licensed under a Creative Commons Attribution 4.0 License. For more information, see https://creativecommons.org/licenses/by/4.0/

7034

IEEE TRANSACTIONS ON VEHICULAR TECHNOLOGY, VOL. 71, NO. 7, JULY 2022

other metrics. This demonstrates the multiple advantages of MADRL to develop increasingly intelligent AIMs, which can provide advanced control policies and achieve smarter CAVs. 

Moreover, they can greatly surpass in control complexity the currently proposed AIMs, where they usually only allow straight or right turns, single-lane intersections, or very low vehicular flows. 

A tentative version of this work was previously presented in

\[10\], which served as a basis for the development of RAIM and to demonstrate that RL-based AIM could offer advantages over traditional control techniques. The present work adds significant aspects to the initial version. 

r First, RAIM has been enhanced with a recurrent module Fig. 1. AIM basic operation. AIM includes a *Conflict module * and a *Priority* \(LSTM\) to eliminate the problem of variation in the shape *module * to control AV \[10\]. 

of the variable observations as a function of the number of vehicles. In addition, thanks to the nature of LSTMs, we can capture the long-term spatial and temporal dynamics and control CAVs’ state \(speed, acceleration, steering, etc.\) at of traffic conditions in the network. With this recurrent intersections to provide the highest security level, increasing module, the speed calculation for each vehicle considers flow while increasing flow and decreasing time loss \[12\]. Tradi-all other vehicles at the intersection. 

tionally, these AIMs are based on two modules, one dealing with r Secondly, the complexity of the simulation scenario has conflict prediction and the other with the resolution of expected been considerably increased from a maximum flow of 450

conflicts. 

veh/h/lane to 1200 veh/h/lane and from 2 lanes to 3 lanes per direction, which increases exponentially the complex-A. Conflict Module

ity and training time, but allows maximizing the advantages offered by RL over traditional and other AIM techniques. 

This module is responsible for deciding whether, or not, there In addition, each simulated vehicle had different charac-will be conflicts between two vehicles when approaching or teristics within a random range of acceleration, shape, fuel crossing the intersection. It follows a series of rules so that it can consumption, etc., which offered additional complexity in predict the routes that vehicles will take within the intersection learning how to model the simulated environment. 

r

along space-time and check if there are conflicts. That is, when Finally, the comparison of results is extended to more two or more vehicles coincide temporally and spatially, this recently published algorithms, such as an intelligent traffic component identifies a conflict. The basic operation of AIM with light control system \( *iREDVD *\[8\]\) and an already proposed the conflict module and priority module can be seen in Fig. 1. 

AIM \[9\], and we confirm that our model continues to This module can follow several approaches to conflict identi-outperform existing approaches using different evaluation fication: *i\) intersection-based *\[12\]–\[14\], *ii\) tile-based *\[15\]–\[18\], metrics. Furthermore, considerable new analysis and in-iii\) conflict point-based \[9\], \[19\]–\[22\], and *iv\) vehicle-based* tuitive explanations are added to the training curves and

\[23\]–\[26\]. A representation of each approach can be seen in testing results. 

Fig. 2. 

The rest of this paper is organized as follows. Section II pro-The first proposed approach laid the foundation for AIM \[12\]. 

vides an overview of the operating principles of AIM. Section III This approach \( *intersection-based*\) does not allow more than one shows the state of the art of AIM. Section IV describes the system vehicle to be inside the intersection at the same time, regardless proposed in this paper. The simulator and parameters used are of the route the vehicles take. This option, while very simple, shown in Section V. Section VI includes the performance results has multiple obvious disadvantages. 

obtained both in the training process and in a test scenario. 

A more elaborated approach is the *tile-based *\[18\], which cre-Finally, the conclusions are summarized in Section VII. 

ates a mesh within the intersection, and vehicles cannot coincide in the same mesh cell simultaneously along their trajectory. 

The *conflict point-based *\[9\] only takes into account the spots II. AUTONOMOUS INTERSECTION MANAGEMENT

where the trajectories of the vehicles within the intersection Intersections are responsible for regulating the right-of-way overlap. This dramatically reduces the complexity of optimiza-of vehicles to control traffic flow, reduce accidents, and improve tion tasks, but due to the variable geometry of the vehicles, travel time, which is usually done with traffic lights, or traffic unexpected accidents may occur, a situation that can never occur. 

signals, in urban areas. With the arrival of CAVs, it requires a new Finally, the *vehicle-based *\[26\] approach offers vehicles total way of controlling vehicles as a whole \[11\], more efficient and freedom of movement within the intersection. Here, vehicles are sophisticated than traditional techniques, allowing inefficient free to choose the route they take to reach their exit lane. The traffic lights to be eliminated. 

latter option is undoubtedly the one that offers the most freedom, AIM emerges as a new approach to building intelligent but it requires enormous computing power since it becomes a systems that can deal with the complex dynamics of real-life multidimensional and multiagent problem of vast complexity. 



ANTONIO AND MARIA-DOLORES: MULTI-AGENT DEEP REINFORCEMENT LEARNING TO MANAGE CAVs AT TOMORROWS INTERSECTIONS

7035

following a policy based on FCFS, and began the development of these systems, which demonstrated that, in certain situations, the control protocol they proposed outperformed the traditional traffic light control protocols. Further, multiple variants of this work were presented that allowed the incorporation of non-autonomous vehicles \(FCFS-light\) \[2\], \[35\], as well as emergency vehicles such as ambulances or police cars \(FCFS-EMERG\) \[36\]. The advantages offered by FCFS were a reduction in travel time of up to 80% compared to traffic lights and stop signals. 

Another interesting work on AIM was proposed by \[13\], where it presented an auction-based reserve approach. These auctions were used to determine the order in which vehicles pass through, that is, within the priority module. The vehicles that bid the most were passed first. The results shown in four urban cities showed superior performance in three of the four simulated road networks when compared to traditional mechanisms, as well as when compared to FCFS. However, this mechanism presents several serious problems. The main problem is that the intrinsic problem of any auction mechanism is vehicle starvation, in the Fig. 2. 

Approaches developed for the conflict module of AIM. 

sense that the auction strategy may prevent others from winning, with the risk that they will experience indefinitely long waiting *B. Priority Module*

times, as well as generate a market economy of the currency When conflicts are encountered, the priority module resolves used, inflation, discrimination, etc. 

them by acting on the vehicles’ state \(e.g., speed, acceleration, Using DRL, an AIM was presented in \[17\] where DRL is route, etc.\) and managing the vehicles’ right-of-way. This mod-used in the priority module to create a *Q*-table with all possible ule is responsible for ensuring that the travel time of the vehicles combinations of vehicles per entrance and the best car to pass. 

is reduced most fairly, ensuring that no vehicle is stuck infinitely. 

This work offers improvements of more than 30% compared to Seeking to assign priorities to vehicles when crossing, this mod-FCFS and LQF, but however, very extensive training is required. 

ule can give the right-of-way of vehicles in several manners: *i\)* Aside from creating all possible combinations of vehicles in the based on the order of arrival at the intersection, with First-Come entry, you must find the best vehicle for each case, something First-Served \(FCFS\) \[12\], \[19\], \[27\], \[28\]; *ii\) * assigning priorities that, for real situations, can take an enormous amount of training based on vehicle/intersection status, such as Fast First Service time. Nevertheless, the advantage of RL is that when such a \(FFS\) \[9\] where vehicles arriving at the intersection fastest are policy has been found, the inference is extremely fast. However, given the highest priority, or Long Queue First \(LQF\) \[17\] where in the work proposed by Levin *et al. *\[37\] it was shown that those vehicles with the longest entry queue have the highest AIM has much room for improvement, since, in realistic ex-priority; *iii\) * using some heuristics like Dynamic Programming amples, conventional traffic systems were able to outperform \(DP\) or Linear Mixed Integer Programming \(MILP\) where given the reservation-based systems proposed to date. To test this, a series of equations and conditions is used to solving them FCFS was compared with a traditional traffic light system. 

\[15\], \[22\], \[26\], \[29\]–\[32\]; however, this method requires a huge In situations where vehicle flow is low, FCFS provided better computational load every time a solution is required, and when performance, but when traffic is high \( *> * 800 veh/h\) traffic light sudden changes occur, a solution has to be obtained again from control provided better performance. In addition, when traffic scratch, which increases the complexity to solve the problem in is asymmetric, in bursts, or there is a main avenue and streets an almost exponential way and the complexity is not acceptable connecting to it, the performance of FCFS was worse than that for real-time systems; *iv\) * by auctions \[13\], \[33\] with higher of traffic light control. 

priority being given to those vehicles with the highest bids, It’s evident that having more control over autonomous ve-creating a market economy with the currency used for auctioning hicles, both individually and collectively, gives these systems and generating problems of equality; *v\) * or through artificial a huge advantage over traditional control techniques in terms intelligence mechanisms such as genetic algorithms \[34\] or RL

of increasing vehicle flow, avoiding accidents, and shortening

\[17\]. 

vehicle travel times. However, the functioning of these modules can have serious disadvantages compared to traditional traffic light control techniques as they are based on simple control III. STATE OF THE ART

techniques. These disadvantages have been previously detailed Having seen the principle of operation of the different AIMs, in \[37\], where it is demonstrated that in the case of unstudied in this section we will look at the proposed works, as well as situations, the systems’ behavior becomes unstable and obtains their benefits, drawbacks, and performance. The work presented unexpected results. Furthermore, these techniques are incapable by Stone *et al. *\[12\] was based on right-of-way reservations, of considering past events or anticipating future ones. 

7036

IEEE TRANSACTIONS ON VEHICULAR TECHNOLOGY, VOL. 71, NO. 7, JULY 2022

Fig. 3. 

New advanced RAIM \( *adv. * RAIM\) network. The action to be performed by the *ego * vehicle is calculated in the Policy. The output is the normalized speed that the *ego * vehicle must follow in the next timestep. Note that there is only one *LSTM cell * that is iteratively fed with the features of each vehicle \(14\), starting with the *ego * vehicle’s state, and continuing with other vehicles’ state. The State/Conflict Encoder output \( *hx*\) was set to 256 hidden parameters. 

restricting the information learned. This is the first time we have IV. ADVANCED REINFORCED AIM – ADV.RAIM

used an LSTM cell in a RAIM approach, and it is also a novel Considering the enormous potential offered by AIM and the approach to conflict-based controller design. 

challenges that MADRL can address, in this work we proposed As for the order in which the module is fed, the state variables advanced Reinforced AIM \( *adv. * RAIM\). This new approach of the ego vehicle are fed first, followed by those of the other brings together the properties of the MADRL field with those of vehicles, in the order of their distance from the center of the AIM. *adv. * RAIM can offer a new approach within AIM, opening intersection. This allows learning the state variables in the local an original path for the development of other advanced AIM

neighborhood when a conflict occurs \(fed by the reward signal\). 

solutions. 

The motivation for learning in this way is that it is easier to feed Our prior work \[10\] showed that RAIM offers a great advan-the data in a way that considers the different states in which there tage over the previously proposed AIM in simple scenarios. In would be a conflict, or in which there would be a large impact on addition, RAIM was able to adapt to the different conditions the RL information about a given vehicle state, thus increasing that may arise as well as, once trained, being able to infer a the reward for learning to encode conflicts. 

result extremely quickly. Furthermore, the preliminary findings After the *State/Conflict encoder * module, *adv. * RAIM presents a suggested that RAIM could outperform other traffic control set of fully connected layers, which compose the Motion Planner systems in more realistic scenarios than those shown in the module, see Fig. 3. This module decides the normalized speed to previous. 

be carried by each CAV at the next timestep based on its features However, the main problem of RAIM was that it could only and the output of the state/conflict encoder to avoid collisions and take into account 32 vehicles at a time, using a zero-filling optimize the traffic flow. This module was composed of 4 layers approach when faced with fewer vehicles and ignoring them of fully connected neurons with ReLU activation functions and when there were more than 32 vehicles. To solve this problem, the number of neurons in each layer is shown in Fig. 3. *adv. * RAIM

the proposal we made is to use a recurrent network \(Long-Short is termed as an *ego-centric * multi-agent system, having to deal Term Memory, LSTM\) in which the features of each vehicle with all the CAVs at the intersection simultaneously, but con-are fed into the input and encoding of the conflicts between trolling each CAV individually. That is, *adv. * RAIM considers the vehicle to be controlled and the other vehicles is obtained at the current state of the vehicle \( *ego*\) and the other vehicles to the output. This module is called *State/Conflict encoder * and can obtain the normalized speed of the *ego * vehicle at the next time be seen in Fig. 3, where an LSTM cell is used to which all the step. 

vehicle states are recurrently input, and an encoded value of the The action space is the normalized speed between 0 and 1

conflicts is learned during the training process. 

that the *ego*-vehicle must follow in the following time interval The LSTM cell has the advantage of being able to learn \(labeled *ego*-action in Fig. 3\). The speed was denormalized long-term dependencies \[38\], i.e., between different vehicles considering a maximum road speed of 13.9 m/s \( = 50 Km/h\). 

depending on their state, since the feedback mechanism allows Each CAV has internal constraints of maximum accelerations it to remember previous states of the vehicles. In addition, the and decelerations given by the simulation tool that it will be output of the LSTM is a fixed-dimensional vector, eliminating employed \(typical values of 2.6 and 4.5 m/s2\), so each vehicle the problem that RAIM had. An output size of 256 variables was performs the indicated actions considering these speed change used to allow encoding as much information as possible without constraints. 

ANTONIO AND MARIA-DOLORES: MULTI-AGENT DEEP REINFORCEMENT LEARNING TO MANAGE CAVs AT TOMORROWS INTERSECTIONS

7037

TABLE I

INPUT FEATURES AND MEANING

**Algorithm 1: **adv.RAIM. 

**Input**: State of all vehicles

**Output**: Speed of each vehicle in the following timestep 1

\# Reset the environment. 

2

**for **timestep *t ∈ \{* 0 *, . . . , M axepisodie\} ***do**: 3

\# Obtain the vehicles currently being simulated. 

4

*vehicles *= *sim.get* \_ *current* \_ *vehicles*\(\) 5

\# For each vehicle, the desired speed for the next timestep is obtained. 

6

\# This loop is repeated for each vehicle in the intersection. 

7

\# Clear *input* \_ *params*. 

8

**for **vehicle *ego* \_ *veh ∈ * vehicles **do**: 9

\# Obtain the params of *ego* \_ *veh *\(position, speed, lane, etc.\) and append them to *input* \_ *params*. 

10

*vehicles* \_ *added *= 0

TABLE II

SUMMARY OF THE SIMULATION SETUP AND RAIM PARAMETERS

11

\# Obtain the params of the other vehicles. 

12

**for **vehicle *veh ∈ * vehicles **do**: 13

\# Obtain the params of *veh * and add to *input* \_ *params*. 

14

## **end for**

### 15

\# Obtain new speed of *ego* \_ *veh * using *input* \_ *params * and actor net of TD3 and set *new* \_ *speed. *

16

*new* \_ *speed *= *actor* \_ *net*\( *input* \_ *params*\) 17

*sim.set* \_ *veh* \_ *speed*\( *ego* \_ *veh, new* \_ *speed*\) 18

## **end for**

### 19

**end for**

Therefore, the observation space for the entire control policy, Fig. 3 \(Policy\), is formed by the 14 characteristics of the *ego*-

vehicle plus the *n × * 14 characteristics of the other vehicles, where *n * is the number of other vehicles with which the *ego*-

TABLE III

vehicle must cooperate to ensure the safety and smooth flow of TESTING SCENARIO 1 \(FIXED 200 VEH/H/LANE\) RESULTS

traffic. 

The control timestep was set to 250 ms, considering that it is a sufficient time interval for efficient control without overloading the processing and allowing real-time control. This means that every 250 ms *adv*.RAIM updates the speed that all vehicles at the intersection must follow to ensure safety and maximum flow, considering the updated status of all vehicles. The pseudocode of RAIM is shown in Algorithm 1 and the new *adv. * RAIM network can be seen in Fig. 3. To optimize the controller, we use Twin Delayed Deep Deterministic Policy Gradients \(TD3\) \[39\]. TD3

is an improvement of the Deep Deterministic Policy Gradient No collisions were recorded. \[ *mean ± std*. of 10 simulations\]. 

\(DDPG\) algorithm, based on Actor/Critic control approach. It has become one of the most popular algorithms for continuous The state variables of each vehicle used as input parameters control problems within robotics and autonomous driving fields. 

to *adv. * RAIM are shown in Table I. After coding the input In this approach, there are two types of neural networks, one parameters, each vehicle provides *14 * features. The parameters that aims to predict the action to be taken \(in this case, the with a continuous range \(such as position, speed, and angle\) are normalized speed of *ego * vehicle\) based on the state \( *Actor*, learn normalized within the range of \[-1, 1\], and the parameters with the policy\) and another that seeks to predict the expected reward discrete values \(i.e., lane, way, queue\) are encoded with one-hot of performing that action \( *Critic*, learn the *action-value function*, encoding. 

*Q*-function\). 

7038

IEEE TRANSACTIONS ON VEHICULAR TECHNOLOGY, VOL. 71, NO. 7, JULY 2022

TABLE IV

TESTING SCENARIO 1 \(FIXED 200 VEH/H/LANE\) ADDITIONAL RESULTS

No collisions were recorded. \[ *mean ± std*. of 10 simulations\]. 

TABLE V

complexity. First, the agent is trained in simple tasks, TESTING SCENARIO 2 \(FIXED 600 VEH/H/LANE\) RESULTS

and once the agent is capable of completing them, the complexity of the tasks to be performed is gradually increased \[41\]. Compared to training without it, the adoption of the curriculum is expected to accelerate the speed of convergence and may improve the final performance of the model. Designing an efficient and effective curriculum is not an easy task. A bad curriculum can even make learning more difficult. In this work, curriculum-based learning through *Self-Play * is used. With this approach, the number of simulated vehicles was increased when a No collisions were recorded. \[ *mean ± std*. of 10 simulations\]. 

stable solution was reached after several simulations, i.e., when after a certain time, the system could not improve the solution found. Then, more vehicles were added to the As a reward signal, each vehicle \( *agent*\) received at each simulation so that the controller could learn to work in a timestep:

r

real multi-agent environment with multiple simultaneous

*−100 *\(strong negative reward\) if there was a collision. 

r

vehicles. 

\+ *100 *\(strong positive reward\) if the intersection was crossed. 

r *−timestep *\(weak negative reward\) to encourage crossing V. S

as fast as possible. 

IMULATION SETUP

Two main techniques are followed to achieve a more stable We employed the microscopic traffic simulation tool SUMO

and fast training:

\[42\]. With this simulator, each vehicle is explicitly modeled. Py-i\) *Prioritized Experience Replay: *\(PER\) \[40\]. In DRL, a torch 1.5.0 and Python 3.7 were also used to develop *adv. * RAIM. 

*replay buffer * is added to store past experiences and proA 16-core processor was used together with an Nvidia 2080TI. 

vide more stability during the training process. These The overall training process required 14 days \(336 hours\) due to past experiences are known as transition tuples, usually the increasing complexity of the scenario and the convergence denoted as \( *st, at, rt, st*\+ *1*\) with states, actions, rewards, time of the DRL algorithm. Once adv.RAIM is trained, the and next states. Using this *replay buffer*, it is possible size of the actor architecture is 20.3 MB, which any current to remember the past experiences, not forget them, and GPU with more than 4 GB of memory can handle. In addition, thus approximate in a faster way *Q*-values of the DNN. 

adv.RAIM has an inference time of 1.89 *± * 0.08 ms \(mean However, not all actions provide the same information, 

*± * est. dev. of 10,000 runs\), so, during the 250 ms control and there are experiences where the *critic * can learn more. 

period \(the selected control time interval\), a single adv.RAIM

The experiences that PER considers the most “*learnable*” 

instance could control up to 106 vehicles in real-time. To control are those where the error committed between the predicted more vehicles simultaneously, several instances could be run in *Q*-value \( *Q\(s,a*\)\) and the actual *Q*-value \( *Q∗\(s,a*\)\) is high. 

parallel, multiplying the control capacity. 

This error is known as the Temporal Difference \( *TD*\) error The setup was divided into two parts: *i\) * a training scenario, and measures the uncertainty that the DNN possesses, where the optimization of *adv. * RAIM was performed; and *ii\) * four being low when the error is low and high when it is testing scenarios, three with a fixed flow rate and one closer to a high. Therefore, the higher this error is, the more likely

“real-world scenario” with a variable flow rate. In all the testing it is to select an experience from the *replay buffe* r in the scenarios, *adv. * RAIM was compared with 1\) traditional traffic optimization process. 

light control \(Fixed Time, FT\) with different cycle lengths \(40, ii\) *Learning by curriculum *\[41\] *: * Curriculum learning con-60, 80, and 120 seconds, FT10, FT15, FT20, and FT30\), 2\) an sists of training an intelligent agent in tasks with increasing advanced traffic-light control mechanism based on queue theory

ANTONIO AND MARIA-DOLORES: MULTI-AGENT DEEP REINFORCEMENT LEARNING TO MANAGE CAVs AT TOMORROWS INTERSECTIONS

7039

TABLE VI

TESTING SCENARIO 2 \(FIXED 600 VEH/H/LANE\) ADDITIONAL RESULTS

No collisions were recorded. \[ *mean ± std*. of 10 simulations\]. 

TABLE VII

*adv. * RAIM was able to learn to deal with a variety of different TESTING SCENARIO 3 \(FIXED 1200 VEH/H/LANE\) RESULTS

input states and obtain a stable model. 

Each simulation represented a 5-minute time-lapse, where the flow of vehicles increased \(\+150 veh/h\) when a series of conditions were met \(the variance of the reward in the last *150*

simulations was less than 0.005 *× * the total simulated flow\), following the curriculum methodology through *Self-Play * previously explained. This allowed us to train both the State/Conflict Encoder module and the Motion Planner simply and progressively, allowing the TD3 algorithm to find a stable control policy that allows it to instruct the speed of each autonomous vehicle No collisions were recorded. \[ *mean ± std*. of 10 simulations\]. 

at a busy intersection. 

The metrics analyzed in the training scenario were global reward, number of collisions, and time loss \(due to congestion\). 

Time loss is due to having to drive slower than desired \(below the desired speed\), and includes waiting time. 

The system took control of the vehicles when they were less than *100 * m from the center of the intersection. A summary of the parameters used in the simulation can be seen in Table II. 

Therefore, the main objective of *adv. * RAIM was to maximize the total individual reward of each vehicle and to do so it strived to eliminate collisions \(since it is a large penalty\), as well as to reduce the travel time of the vehicles \(since it will penalize each time step that the vehicles are within the intersection\). 

*B. Testing Scenarios*

The test scenarios provide a clear comparison of the perfor-Fig. 4. 

Simulated intersection with 4 approaches and 3 lanes/approach, where mance offered by *adv*.RAIM and other traffic control algorithms the movements go straight, turn right, and turn left are allowed. 

in a more realistic scenario with conditions similar to reality. 

The simulated scenario consisted of an intersection with 4

called *iREDVD *\[8\], and 3\) an AIM previously proposed by Qian approaches, and 3 lanes per approach as in the training scenario. 

*et al. *\[9\] *. *

Each simulation was run 10 times and represented a time span of 14 hours. To simulate various conditions, the simulated flow was separated into flow with vertical origin, and flow with horizontal *A. Training Scenario*

origin. These flows could go in a straight line, turn right, or The training scenario consisted of an intersection with *4*

turn left. Four different scenarios were simulated, 3 with a fixed branches of *3 * lanes per direction, where left turns, right turns, and flow and one with a variable flow, shown in Fig. 5. The fixed straight ahead were allowed. In our opinion, this is an important flow scenarios were: one with low flow \(200 veh/h/lane\), one feature, as it offers a great variety of routes and possible collision with medium flow \(600 veh/h/lane\), and one with high flow zones, and very few AIMs allow it due to its high control \(1200 veh/h/lane\). In the fourth variable flow test scenario, complexity. A representation of the simulated intersection can Fig. 5 shows that there were multiple different situations, with be seen in Fig. 4. In each simulation, the *random seed * used low \(200 veh/h/lane\), medium \(600 veh/h/lane\), and high \(1200

was changed, to obtain a wider set of experiences. In this way, veh/h/lane\) flows, asymmetric and symmetric flows, and slow



7040

IEEE TRANSACTIONS ON VEHICULAR TECHNOLOGY, VOL. 71, NO. 7, JULY 2022

TABLE VIII

TESTING SCENARIO 3 \(FIXED 1200 VEH/H/LANE\) ADDITIONAL RESULTS

No collisions were recorded. \[ *mean ± std*. of 10 simulations\]. 

TABLE IX

in addition to the reduction in travel time and congestion. The TESTING SCENARIO 4 \(VARIABLE FLOW RATE\) RESULTS

traditional traffic light algorithms used for comparison were: fixed time algorithm *\(FT\) * and *iREDVD * algorithm \[8\]. 

The FT algorithm sets a fixed passing priority time for each of the branches of an intersection and only allows vehicles from one branch to pass at a time. Several passing priority times were tested, 10, 15, 20, and 30 seconds \(total cycle lengths of 40, 60, 80, and 120 seconds\). They were named FT10, FT15, FT20, and FT30. *iREDVD * is an adaptive algorithm based on queuing theory and traffic lights. RAIM was also compared with the AIM

approach developed by Qian *et al. *\[9\]. The vehicle distribution No collisions were recorded. \[ *mean ± std*. of 10 simulations\]. 

used was: 35% of diesel cars, 35% of gasoline cars, and 30% of electric cars with zero emissions. 

VI. RESULTS

The following section highlights the results obtained in the test scenario, along with a detailed comparative analysis of the test scenario results. 

*A. Training Scenario*

Fig. 6 shows the results obtained in the training scenario in the studied metrics \(number of collisions, reward, and time loss\) versus the simulated vehicle flow throughout all simulations. 

One of the main quick observations is the stability of the system. 

This is especially noticeable at the peak of the first simulations in the average number of collisions metric \(Fig. 6a\) and is mitigated Fig. 5. 

Vehicle flow rate per lane used in the testing scenario. 

by the automatic *Self-Play * curriculum and RL nature. There are some outliers in the metrics as the flow increases. However, they and fast flow variations. This allowed us to test *adv. * RAIM in eventually converge to stable values, demonstrating that TD3

a large number of conditions as close to reality as possible, as and PER allow training to converge with increasing complexity. 

well as to see the evolution of performance in different isolated In addition, it is worth noting that the number of collisions shows scenarios. 

a downward trend from the peak in the initial 750 simulations Several metrics were studied. Due to the optimization tech-approximately, due in part, to the large negative reward when a nique, the metrics directly optimized and studied were travel collision occurs. Finally, the number of collisions can be seen to time, waiting time, and time loss due to congestion. Waiting trend to 0 and presents a very low value from simulation 7000

time refers to the time in which the vehicle speed was less than onwards. 

or equal to 0.1 m/s. This time can be due to a variety of factors, The average reward per vehicle metric \(Fig. 6b\) also shows including congestion. Although the travel time and time loss due a negative trend, but acceptable stability within the confidence to congestion metrics are directly related, we left both to show in intervals. This negative trend is because the number of simulated perspective the time loss due to congestion in relation to the total vehicles increases over time, making the intersection increas-travel time. Indirectly, pollution and consumption metrics \(CO, ingly congested. This causes vehicles \(on average\) to drive CO2, HC, PMx, NOx, and fuel and electricity\) were analyzed progressively slower, but optimally to maximize the average to show the environmental benefits that these systems can offer, reward received by each vehicle. 



ANTONIO AND MARIA-DOLORES: MULTI-AGENT DEEP REINFORCEMENT LEARNING TO MANAGE CAVs AT TOMORROWS INTERSECTIONS

7041

TABLE X

TESTING SCENARIO 4 \(VARIABLE FLOW RATE\) ADDITIONAL RESULTS

No collisions were recorded. \[ *mean ± std*. of 10 simulations\]. 

Fig. 6. 

Training results. We plot the smoothed mean with an exponential moving average and 90% confidence interval across 3 seeds. The red vertical axis on the right and the red curve show the flow of vehicles \(veh/hour\). The blue vertical axis on the left and the blue curve show each of the metrics studied: a\) Average number of collisions; b\) Average reward per vehicle; c\) Average Time Loss. 

Finally, if we look at the average time loss \(Fig. 6c\), it follows This behavior is because when the vehicular flow rate is low, a trend inversely proportional to that of the reward received by the use of traffic light-based control algorithms to control an each vehicle. As the number of simulated vehicles increases, the intersection is very inefficient since the use of the intersection average time loss per vehicle also increases. In this metric, it is is considerably reduced. Alternatively, if vehicles are allowed observed that as the flow increases, there are very abrupt changes to circulate freely, taking into account safety regulations, the in the trend, and after a few simulations, they stabilize. All the throughput they experience is superior, eliminating waiting metrics analyzed remain stable within the confidence intervals, times when there are almost no vehicles. However, this is not the which confirms the good performance of the algorithms used. 

case for high traffic flow rate scenarios, where traffic lights show The three figures show the convergence offered by TD3 and good performance. In this case, the AIM algorithms behave like PER when the flow of vehicles increases. For all metrics, when traffic light-based control algorithms. 

the flow increases, some values break the trend they have \(e.g., Finally, Table IX includes the results obtained by the different the number of collisions increases\), but after a few simulations, algorithms in the fourth test scenario. This scenario is the closest the system can handle more vehicles and learns to deal with to reality since it presents a wide variety of flows and conditions. 

them to further optimize each metric. 

If we focus on traditional traffic light control \(FT and *iREDVD*\), for all metrics under study, *adv. * RAIM shows its superiority. 

Using *adv. * RAIM, travel time is reduced by up to 59%. In turn, *B. Testing Scenarios*

time loss is decreased by up to 95%. Another key result is The results obtained in the fixed scenarios are shown in Tables achieved indirectly. The emissions of polluting gases \(CO, CO2, III–VIII. 

HC, PMx, and NOx\) and consumption \(fuel and electricity\) are As can be seen, the advantage of not having traffic lights for the reduced, showing significant reductions of up to 37%, 13%, control of autonomous vehicles increases when traffic density 28%, 37%, 50%, 21%, and 27%, respectively. 

is lower, particularly in the low traffic scenario \(200 veh/h/lane, If we look at the additional results tables \(Tables IV, VI, VIII, Tables III and IV\), where the improvement in metrics is more and X\), we can see that *adv*.RAIM offers an improvement over significant in all cases. 

the other methods. This can be explained because *adv*.RAIM is For the medium flow scenario, the performance of the AIM

optimized to find a control policy that ensures that vehicles cross approaches still outperforms that offered by the traffic lights-an intersection as fast as possible while guaranteeing safety. 

based approaches \(Tables V and VI\). Lastly, if we look at the That is, vehicles spend as little time as possible within the high flow scenario \(Tables VII and VIII\), all algorithms present intersection. Thus, since vehicles rarely stop at intersections similar performance. 

\(reducing waiting time and wasted time\), vehicles do not have to

7042

IEEE TRANSACTIONS ON VEHICULAR TECHNOLOGY, VOL. 71, NO. 7, JULY 2022

brake and then accelerate, but rather find the appropriate speed such as fuel/energy consumption or pollutant gas emissions, for each vehicle with which each vehicle crosses the intersection due to the smaller number of accelerations/decelerations of the in the shortest possible time without collision. By not having to CAVs. Furthermore, the modularity of *adv*.RAIM could be an accelerate, other metrics such as fuel/energy consumption and advantage to explore its use in other scenarios such as highways pollutant emissions are reduced since it is at these times that or sub-urban areas. 

higher consumption is realized. 

As future work, we will address some improvements such On the other hand, if we compare the results obtained by as incorporating a Transformer-based attention mechanism to *adv. * RAIM with the AIM algorithm proposed by Qian *et al. * in identify conflicts, the crossing order of vehicles, or the exchange

\[9\], we can observe similar results. However, if we focus on the of information between intersections to increase collective in-operation of \[9\], we can see that this algorithm must have in telligence. 

advance the planning of all the vehicles. Then, employing FFS, it can organize the vehicles in a suboptimal way. In the event that there is a new vehicle or if the vehicles cannot adjust their speeds REFERENCES

to those imposed by \[9\], the system must recalculate all vehicles’

\[1\] S. Djahel, R. Doolan, G. M. Muntean, and J. Murphy, “A communications-routes. Consequently, this prevents it from easily adapting to oriented perspective on traffic management systems for smart cities: changing environmental conditions, which is very common at Challenges and innovative approaches,” *IEEE Commun. Surv. Tut. *, vol. 17, no. 1, pp. 125–151, Jan.–Mar. 2015. 

intersections where accidents, emergency vehicles, pedestrians, 

\[2\] K. Dresner and P. Stone, “A multiagent approach to autonomous intersec-etc., may occur. With *adv. * RAIM, this does not happen because tion management,” *J. Artif. Intell. Res. *, vol. 31, pp. 591–656, Mar. 2008. 

it can be trained to take into account these incidents and offer

\[3\] N. Aloufi and A. Chatterjee, “Autonomous vehicle scheduling at intersections based on production line technique,” in *Proc. IEEE Veh. Technol. *

optimal solutions, considering all vehicles in each time interval *Conf. *, 2018, pp. 1–5. 

and obtaining for each one the optimal speed that guarantees the

\[4\] S. Mariani, G. Cabri, and F. Zambonelli, “Coordination of autonomous greatest expected reward. 

vehicles: Taxonomy and survey,” *ACM Comput. Surv. *, vol. 54, pp. 1–33, 2020. 

\[5\] V. Mnih *et al. *, “Human-level control through deep reinforcement learning,” *Nature*, vol. 518, no. 7540, pp. 529–533, Feb. 2015. 

VII. CONCLUSION AND FUTURE WORK

\[6\] O. Vinyals *et al. *, “Grandmaster level in starcraft II using multi-agent reinforcement learning,” *Nature*, vol. 575, no. 7782, pp. 350–354, Nov. 2019. 

The fields of robotics, CAVs, and ITS are advancing rapidly

\[7\] B. Baker *et al. *, “Emergent tool use from multi-agent autocurricula,” 2019, by virtue of MADRL, which provides a flexible and efficient *arxiv.org/abs/1909.07528*. 

way to solve complex and extreme optimization problems in

\[8\] A. Guillen-Perez and M. Cano, “Intelligent IoT systems for traffic management: A practical application,” *IET Intell. Transp. Syst. *, vol. 15, no. 2, these areas. This paper presents and evaluates *adv. * RAIM, a new pp. 273–285, Feb. 2021. 

and inspiring approach in AIM based on MADRL. *adv*.RAIM

\[9\] X. Qian, F. Altché, J. Grégoire, and A. Fortelle, “Autonomous intersection periodically controls the speed of CAVs passing through an management systems: Criteria, implementation and evaluation,” *IET Intell. *

*Transp. Syst. *, vol. 11, no. 3, pp. 182–189, Apr. 2017. 

intersection in a cooperative and decentralized manner, ensuring

\[10\] A. Guillen-Perez and M.-D. Cano, “RAIM: Reinforced autonomous in-safety and maximum fluidity. *adv*.RAIM presents an architecture tersection management - AIM based on MADRL,” in *Proc. Workshop* with an LSTM capable of capturing the long-term spatial and *Challenges Real-World RL*, 2020, pp. 1–12. 

\[11\] Y. Guo, J. Ma, C. Xiong, X. Li, F. Zhou, and W. Hao, “Joint optimization temporal dynamics of traffic conditions in the network. This of vehicle trajectories and intersection controllers with connected auto-allows it to better understand and encode possible collisions mated vehicles: Combined dynamic programming and shooting heuristic in space/time between different CAVs passing through an in-approach,” *Transp. Res. Part C: Emerg. Technol. *, vol. 98, pp. 54–72, Jan. 2019. 

tersection and thus act proactively. In addition, apart from the

\[12\] K. Dresner and P. Stone, “Multiagent traffic management: A reservation-LSTM module, it presents a module composed of deep neural based intersection control mechanism,” in *Proc. Third Int. Joint Conf. *

networks in charge of crossing the collision information encoded *Auton. Agents Multiagent Syst. *, 2004, vol. 2, pp. 530–537. 

\[13\] D. Carlino, S. D. Boyles, and P. Stone, “Auction-based autonomous by the LSTM module and the state of the CAV to be controlled, intersection management,” in *Proc. 16th Int. IEEE Conf. Intell. Transp. *

obtaining the speed at which the CAV should circulate during *Syst. *, 2013, pp. 529–534. 

the following time interval. The control process is performed

\[14\] M. Bashiri, H. Jafarzadeh, and C. H. Fleming, “PAIM: Platoon-based autonomous intersection management,” in *Proc. 21st Int. Conf. Intell. *

sequentially and periodically for all CAVs. 

*Transp. Syst. *, 2018, pp. 374–380. 

The results show that *adv. * RAIM is able to overcome some

\[15\] Y. Bichiou and H. A. Rakha, “Developing an optimal intersection control important disadvantages of traditional AIMs \(performance loss system for automated connected vehicles,” *IEEE Trans. Intell. Transp. *

*Syst. *, vol. 20, no. 5, pp. 1908–1916, May 2019. 

when the vehicular flow is heavy\), controlling challenging sce-

\[16\] P. Dai, K. Liu, Q. Zhuge, E. H. M. Sha, V. C. S. Lee, and S. H. 

narios and achieving robust results through the coexistence of RL

Son, “Quality-of-Experience-Oriented autonomous intersection control techniques such as TD3, PER, and *Self-Play * curriculum-based in vehicular networks,” *IEEE Trans. Intell. Transp. Syst. *, vol. 17, no. 7, pp. 1956–1967, Jul. 2016. 

training techniques. 

\[17\] Y. Wu, H. Chen, and F. Zhu, “DCL-AIM: Decentralized coordination learn-Quantitatively, the results show an improvement in several ing of autonomous intersection management for connected and automated metrics, such as a reduction in travel time by 59%, or a reduction vehicles,” *Transp. Res. Part C: Emerg. Technol. *, vol. 103, pp. 246–260, Jun. 2019. 

in time loss by 95% in the most complex scenario. The intensive

\[18\] H. Xu, Y. Zhang, L. Li, and W. Li, “Cooperative driving at unsignalized training and the capability of operating proactively can explain intersections using tree search,” *IEEE Trans. Intell. Transp. Syst. *, vol. 21, the good outcomes obtained. Moreover, thanks to the nature of no. 11, pp. 4563–4571, Nov. 2020. 

\[19\] D. Fajardo, T.-C. Au, S. T. Waller, P. Stone, and D. Yang, “Automated the optimization, *adv*.RAIM is able to obtain a control policy intersection control,” *Transp. Res. Rec. J. Transp. Res. Board*, vol. 2259, capable of indirectly optimizing other very important metrics no. 1, pp. 223–232, Jan. 2011. 





ANTONIO AND MARIA-DOLORES: MULTI-AGENT DEEP REINFORCEMENT LEARNING TO MANAGE CAVs AT TOMORROWS INTERSECTIONS

7043

\[20\] M. A. S. Kamal, J. Imura, T. Hayakawa, A. Ohata, and K. Aihara, 

\[37\] M. W. Levin, S. D. Boyles, and R. Patel, “Paradoxes of reservation-based

“A vehicle-intersection coordination scheme for smooth flows of traffic intersection controls in traffic networks,” *Transp. Res. Part A: Policy* without using traffic lights,” *IEEE Trans. Intell. Transp. Syst. *, vol. 16, *Pract. *, vol. 90, pp. 14–25, Aug. 2016. 

no. 3, pp. 1136–1147, Jun. 2015. 

\[38\] B. Bakker, “Reinforcement learning memory,” in *Proc. Int. Conf. Neural*

\[21\] M. W. Levin, H. Fritz, and S. D. Boyles, “On optimizing reservation-based *Inf. Process. Syst. *, 2002, pp. 1475–1482. 

intersection controls,” *IEEE Trans. Intell. Transp. Syst. *, vol. 18, no. 3, 

\[39\] S. Fujimoto, H. Van Hoof, and D. Meger, “Addressing function approxi-pp. 505–515, Mar. 2017. 

mation error in actor-critic methods,” in *Proc. 35th Int. Conf. Mach. Learn. *, 

\[22\] A. Mirheli, L. Hajibabai, and A. Hajbabaie, “Development of a signal-2018, pp. 2587–2601. 

head-free intersection control logic in a fully connected and autonomous

\[40\] T. Schaul, J. Quan, I. Antonoglou, and D. Silver, “Prioritized experience vehicle environment,” *Transp. Res. Part C: Emerg. Technol. *, vol. 92, replay,” in *Proc. 4th Int. Conf. Learn. Representations*, 2016, pp. 1–21. 

pp. 412–425, Jul. 2018. 

\[41\] Y. Bengio, J. Louradour, R. Collobert, and J. Weston, “Curriculum learn-

\[23\] Z. He, L. Zheng, L. Lu, and W. Guan, “Erasing lane changes from roads: A ing,” in *Proc. 26th Annu. Int. Conf. Mach. Learn. *, 2009, pp. 1–8. 

design of future road intersections,” *IEEE Trans. Intell. Veh. *, vol. 3, no. 2, 

\[42\] D. Krajzewicz, M. Bonert, and P. Wagner, “The open source traffic pp. 173–184, Jun. 2018. 

simulation package SUMO,” in *Proc. RoboCup Infrastructure Simul. *

\[24\] B. Li, Y. Zhang, Y. Zhang, N. Jia, and Y. Ge, “Near-Optimal online motion *Competition*, 2006, pp. 1–5. 

planning of connected and automated vehicles at a signal-free and lane-free intersection,” in *Proc. IEEE Intell. Veh. Symp. *, 2018, pp. 1432–1437. 

\[25\] B. Li and Y. Zhang, “Fault-Tolerant cooperative motion planning of connected and automated vehicles at a signal-free and lane-free intersection,” 

**Antonio Guillen-Perez **received the B.Sc. degree in *IFAC-PapersOnLine*, vol. 51, no. 24, pp. 60–67, 2018. 

telecommunication engineering and the M.Sc. degree

\[26\] A. Mirheli, M. Tajalli, L. Hajibabai, and A. Hajbabaie, “A consensus-based in information and communication technologies in distributed trajectory control in a signal-free intersection,” *Transp. Res. *

2016 and 2018, respectively, from the Universidad *Part C: Emerg. Technol. *, vol. 100, pp. 161–176, Mar. 2019. 

Politécnica de Cartagena, Cartagena, Spain, where

\[27\] L. Chen and C. Englund, “Cooperative intersection management: A he is currently working toward the Ph.D. Degree with survey,” *IEEE Trans. Intell. Transp. Syst. *, vol. 17, no. 2, pp. 570–586, the Department of Information and Communication Feb. 2016. 

Technologies. His main research interests include

\[28\] X. Zhao, J. Wang, Y. Chen, and G. Yin, “Multi-objective cooperative intelligent transport systems, artificial intelligence, scheduling of CAVs at non-signalized intersection,” in *Proc. 21st Int. Conf. *

deep learning, multiagent systems, multiagent deep *Intell. Transp. Syst. *, 2018, pp. 3314–3319. 

reinforcement learning, autonomous cars, IoT and

\[29\] M. W. Levin and D. Rey, “Conflict-point formulation of intersection smart cities. He has authored or coauthored several papers in national and control for autonomous vehicles,” *Transp. Res. Part C: Emerg. Technol. *, international conferences and journals. He has collaborated as a Reviewer for vol. 85, pp. 528–547, Dec. 2017. 

international conferences and is a Member of many IEEE technical committees. 

\[30\] L. Li and F.-Y. Wang, “Cooperative driving at blind crossings using intervehicle communication,” *IEEE Trans. Veh. Technol. *, vol. 55, no. 6, pp. 1712–1724, Nov. 2006. 

\[31\] J. Wu, A. Abbas-Turki, A. Correia, and A. El Moudni, “Discrete intersection signal control,” in *Proc. IEEE Int. Conf. Service Operations Logistics* **Maria-Dolores Cano **\(Senior Member, IEEE\) *Inform. *, 2007, pp. 1–6. 

received the Telecommunications Engineering degree

\[32\] F. Zhu and S. V. Ukkusuri, “A linear programming formulation for au-from Universidad Politécnica de Valencia, Valencia, tonomous intersection control within a dynamic traffic assignment and Spain, in 2000, and the Ph.D. degree from the connected vehicle environment,” *Transp. Res. Part C: Emerg. Technol. *, Universidad Politécnica de Cartagena \(UPCT\), vol. 55, pp. 363–378, Jun. 2015. 

Cartagena, Spain, in 2004. In 2000, she joined UPCT, 

\[33\] M. Vasirani and S. Ossowski, “A market-inspired approach to reservation-where she is currently an Associate Professor with the based urban road traffic management,” in *Proc. Int. Joint Conf. Auton. *

Department of Technologies and Communications. 

*Agents Multiagent Syst. *, 2009, pp. 617–624. 

She has authored or coauthored numerous research

\[34\] J. Wu, A. Abbas-Turki, and A. El Moudni, “Cooperative driving: An ant works in international journals and conferences, in the colony system for autonomous intersection management,” *Appl. Intell. *, areas of quality of service, quality of user experience, vol. 37, no. 2, pp. 207–222, Sep. 2012. 

intelligent transportation systems, IoT, and cybersecurity. Dr. Cano was awarded

\[35\] K. Dresner and P. Stone, “Sharing the road: Autonomous vehicles a Fulbright grant as a Postdoctoral Researcher in 2006 at Columbia University, meet human drivers,” in *Proc. 20th Int. Joint Conf. Artif. Intell. *, 2007, New York, NY, USA. She was the recipient of the Best Paper Award at the 10th pp. 1263–1268. 

IEEE International Symposium on Computers and Communications in 2005 and

\[36\] P. Stone and Kurt Dresner, “Human-usable and emergency vehicle–aware the Exemplary Reviewer Recognition by IEEE Communication Letters in 2010, control policies for autonomous intersection management,” in *Proc. 4th* among other recognitions. 

*Int. Workshop Agents Traffic Transp. *, 2016, pp. 17–25.



