Original Article

The International Journal of

Robotics Research

2024, Vol. 0\(0\) 1–21

Learning to control and coordinate mixed traffic © The Author\(s\) 2024

Article reuse guidelines:

through robot vehicles at complex and

sagepub.com/journals-permissions

DOI: 10.1177/02783649241284069

unsignalized intersections

journals.sagepub.com/home/ijr

Dawei Wang1, Weizi Li2, Lei Zhu3 and Jia Pan1

Abstract

Intersections are essential road infrastructures for traffic in modern metropolises. However, they can also be the bottleneck of traffic flows as a result of traffic incidents or the absence of traffic coordination mechanisms such as traffic lights. 

Recently, various control and coordination mechanisms that are beyond traditional control methods have been proposed to improve the efficiency of intersection traffic by leveraging the ability of autonomous vehicles. Among these methods, the control of foreseeable mixed traffic that consists of human-driven vehicles \(HVs\) and robot vehicles \(RVs\) has emerged. We propose a decentralized multi-agent reinforcement learning approach for the control and coordination of mixed traffic by RVs at real-world, complex intersections—an open challenge to date. We design comprehensive experiments to evaluate the effectiveness, robustness, generalizablility, and adaptability of our approach. In particular, our method can prevent congestion formation via merely 5% RVs under a real-world traffic demand of 700 vehicles per hour. In contrast, without RVs, congestion will form when the traffic demand reaches as low as 200 vehicles per hour. Moreover, when the RV

penetration rate exceeds 60%, our method starts to outperform traffic signal control in terms of the average waiting time of all vehicles. Our method is not only robust against blackout events, sudden RV percentage drops, and V2V communication error, but also enjoys excellent generalizablility, evidenced by its successful deployment in five unseen intersections. Lastly, our method performs well under various traffic rules, demonstrating its adaptability to diverse scenarios. Videos and code of our work are available at https://sites.google.com/view/mixedtrafficcontrol. 

Keywords

Robot vehicles, multi-agent reinforcement learning, mixed traffic control, intelligent transportation systems, future mobility Received 26 December 2023; Revised 8 June 2024; Accepted 18 August 2024

1. Introduction

raises the question: How can we ensure uninterrupted

traffic flows at intersections? 

Traffic flow is the beating heart of a city, driving eco-While current transport control methods have limited

nomic growth and ensuring daily lives. Despite the im-

effectiveness in mitigating traffic delays and congestion, plementation

of

various

traffic control methods, 

connected and autonomous vehicles \(CAVs\) \(Spielberg

including traffic signals, ramp meters, and tolls, traffic

et al., 2019; Feng et al., 2023; Pek et al., 2020\) offer congestion continues to be a global issue, with external new opportunities. Recent studies \(Sharon and Stone, 2017; expenses amounting to over $100 billion annually

Yang and Oguchi, 2020\) have demonstrated the possibilities \(Schrank et al., 2021\). Modern urban road networks of using autonomous vehicles to enhance intersection traffic largely consist of linearly-coupled roads interconnected by intersections. The key to this design’s functionality is the intersection, which enables traffic flows to inter-1

change and disperse. Any intersection blockage can

Department of Computer Science, The University of Hong Kong, Hong disrupt traffic from all directions, leading to traffic Kong, China

2Department of Electrical Engineering and Computer Science, The spillover and even city-wide gridlock. Unfortunately, 

University of Tennessee, Knoxville, TN, USA

intersections are vulnerable to traffic incidents with more 3Department of Industrial and Systems Engineering, The University of than 45% of all crashes taking place at intersections in the North Carolina at Charlotte, Charlotte, NC, USA

U.S. \(Choi, 2010\) and are susceptible to extreme weather Corresponding author:

and energy shortages, which can leave intersections

Jia Pan, Department of Computer Science, The University of Hong without control for days or even weeks, paralyzing the

Kong, Rm 410 Chow Yei Ching Building, Hong Kong, China. 

traffic \(Press, 2022; Winck, 2022; Ramirez, 2022\). This Email: jpan@cs.hku.hk



2

The International Journal of Robotics Research 0\(0\)

throughput. However, these studies presume universal

should enter or not enter the intersection independently connectivity and centralized control of all autonomous

from other RVs. Our approach falls into the paradigm of vehicles, a scenario that may not materialize soon. The centralized training and decentralized execution. RVs are transition to varying levels of autonomous vehicles will be centrally trained with a shared policy and reward function, gradual, with a prolonged period of mixed traffic comprised which accounts for traffic efficiency and potential conflicts. 

of both human-driven vehicles \(HVs\) and robot vehicles

During execution, all RVs make independent decisions

\(RVs\). Despite the challenge in modeling and controlling while collectively ensuring smooth traffic flow at the in-mixed traffic due to the diversity and suboptimality of tersection without explicit coordination. We also design a human drivers, mixed traffic control is possible through conflict resolution mechanism for eliminating potential algorithmically determining the behaviors of RVs to reg-conflicts at the intersection, which significantly boosts ulate HVs \(Wu et al., 2022\). While progress has been made training efficiency and road safety. 

\(see Section 2 for details\), no evidence exists to demonstrate We conduct comprehensive experiments under high-the feasibility of controlling mixed traffic through RVs at fidelity traffic reconstruction and simulation. The real-real-world, complex intersections where a large number of world traffic data provided by the city of Colorado

vehicles may potentially conflict. However, being able to Spring, CO, USA is used to reconstruct the simulated traffic control traffic at real-world intersections is an essential step flow, validating that our training environments and evalu-toward citywide traffic control and unveiling full societal ation experiments closely resemble real-world conditions. 

benefits of autonomous vehicles \(Urmson and Whittaker, 

Our overall results show that, with 60% or more RVs, our

2008\). 

method outperforms traditional traffic light control in terms In this project, we study mixed traffic control at real-of traffic efficiency in most scenarios. For example, the world intersections through RVs. The intersection layouts average waiting time of all vehicles is reduced by 25.9% and and reconstructed traffic are shown in Figure 1 LEFT. To 40.7% compared to employing traffic lights at intersection I, test the limit of mixed traffic control and explore the en-when the RV penetration rate is 70% and 90%, respectively. 

visioned benefits of RVs to our traffic system, we further With 100% RVs, our method reduces the average waiting

assume these intersections are unsignalized, with the flow of time of the entire intersection traffic up to 42% compared to traffic entirely and solely controlled by RVs. Numerous traffic light control and 89% compared to the traffic light challenges abound under such an assumption, such as

absence baseline. We further explore the relationship be-modeling mixed traffic behavior and designing a repre-

tween traffic demands, congestion, and RV penetration

sentation of traffic conditions that encompasses diverse rates. We find with just 5% RVs, our method can prevent topologies and dynamically fluctuating real-world traffic congestion from developing under the actual traffic demand demands. 

of 700 vehicles per hour \(v/h\). In contrast, without RVs, We propose a model-free reinforcement learning \(RL\)

congestion will form at an \(unsignalized\) intersection when approach for mixed traffic control at complex intersections. 

traffic demand reaches as low as 200 v/h. 

When approaching an intersection, an RV will first observe Besides effectiveness, we also desire robustness, gen-the traffic condition via local perception and vehicle-to-eralizablility, and adaptability of our method. For robust-vehicle \(V2V\) communication, and then encode the ob-

ness, we conduct a “blackout” experiment to show the

servation as input to a mixed traffic control policy. The ability of our approach to stabilize the traffic flow when policy will output a high-level decision of whether the RV

traffic lights suddenly stop working and traffic control Figure 1. LEFT: We study real-world, complex intersections located at Colorado Springs, CO, USA. The traffic is reconstructed using the actual traffic data collected at these intersections \(more details of these intersections are in Table 2\). RIGHT: Comparison of state-of-the-art studies on intersection traffic control. The references can be found in Section 2 related work. 

Wang et al. 

3

transitions to our system. During the blackout, the RVs act and then decentrally coordinate those platoons at the in-as self-organized “traffic lights” coordinating the traffic at a tersection. DASMC

\(Zhou et

al., 2022\)

combines

high throughput. We also examine the impact of sudden RV

microscropic-level virtual platooning and macroscopic-

rate drops. The results show that even with 40% drop \(from level traffic flow regulation to coordinate RVs across un-90% to 50%\), our method still maintains stable and efficient signalized intersections. Yang and Oguchi \(2020\) propose traffic flows at the intersection. Next, we analyze the impact an intersection delay model that predicts total vehicle delay of observation errors on traffic conditions due to varied V2V

and assigns optimally-controlled actions to RVs to minimize connectivities and range settings, simulated through multi-the delay. Malikopoulos et al. \(2018\) define the control of hop communication and packet error events. As a result, our intersection traffic as an energy minimization program. By method is robust even under extreme situations, such as 3-solving the program, lower fuel consumption and travel

hop communication and a 20% packet error rate \(PER\). This times are achieved. Mirheli et al. \(2019\) define a cooperative hints the practicality of our method in real-world deploy-trajectory planning to control and coordinate RVs through ment. For generalizablility, we deploy our method without unsignalized intersections. Chen et al. \(2022\) consider local any modification or tuning at five unseen intersections: Not conflicts among RVs at unsignalized intersections. Yan and

only does our method eliminate congestion, but with 60–

Wu \(2021\) use RL to control mixed traffic through RVs at 70% RVs, it also surpasses traffic light control in reducing two-way/four-way unsignalized intersections. Miculescu

the average waiting time for all vehicles. For adaptability, 

and Karaman \(2019\) define a polling systems-based algo-our method can adapt to various traffic rules, such as left-rithm that provides safe and efficient coordination. Spatharis

hand traffic, by incorporating and regulating the right-turn

and Blekas \(2024\) present a multi-agent RL method to traffic streams. The results show comparable performance to control traffic at intersections. Xu et al. \(2021\) introduce a the original policy, illustrating the flexibility of our method centralized scheme for scheduling autonomous vehicles

and its applicability across different countries. 

under signal-free conditions. Zheng et al. \(2022\) propose a In summary, our work is the first to demonstrate the fea-cooperative multi-agent proximal optimization algorithm sibility of controlling and coordinating mixed traffic at un-for

coordinating

connected

autonomous

vehicles. 

signalized intersections with complex topologies and real-

Mavrogiannis et al. \(2023\) present a method for abstracting world traffic demands. As many challenges are addressed road traffic to aid in traffic analysis and vehicle control at for the first time in mixed traffic control, we hope that our intersections. Wu et al. \(2023\) achieve unsignalized inter-design can provide insights into these challenges and stimulate section control using mixed integer nonlinear programming. 

future endeavors in the field. Our code can be found at https://

Yan et al. \(2021\) propose an RL method to optimize mixed

github.com/daweidavidwang/MixedTrafficControl. 

traffic flow at three-way intersections. Our work differen-tiates from all studies mentioned above, as we specifically address intersection scenarios with complex topologies and 2. Related work

real-world traffic demands—an open challenge to date. 

2.1. Unsignalized intersection control

2.2. Mixed traffic control

There are two common approaches to control and coordi-

nate traffic at intersections \(Rios-Torres and Malikopoulos, 

Traditional mathematical approaches, such as defining and

2016\). The first and extensively studied is traffic signal solving an optimization or control problem, are common

control \(Wei et al., 2019; Mohamed and Radwan, 2022; 

solutions presented for mixed traffic control problems

J´acome et al., 2018\). Our work differs from this line of

\(Wang et al., 2019; Karimi et al., \(2020; Cai et al., 2020; Dai

research by considering intersections unsignalized. The second

et al., 2021; Wang et al., 2023b; Lu et al., 2023; Hickert

is the intersection management system \(Miculescu and

et al., 2023\). For example, Yang and Oguchi \(2020\) solve an

Karaman, 2019; Malikopoulos et al., 2018\), which com-optimization problem for controlling and coordinating

monly requires the central control of all vehicles. This is not mixed traffic through an unsignalized intersection, while applicable to mixed traffic given the flexibility of HVs. Re-work by Zhao et al. \(2018\) solve an optimization problem cently, there has been growing research on using reinforcement for coordinating mixed traffic at roundabouts. Wu et al. 

learning \(RL\) to control and coordinate traffic due to RL’s

\(2018\) introduce an optimal linear controller to stabilize model-free nature and its ability to test a diverse range of traffic flow on freeways. However, there are issues with scenarios through simulation without jeopardizing the safety of solving mixed traffic control problems through traditional participants \(Yan and Wu, 2021; Yan et al., 2022\). 

approaches as they typically require explicit modeling of the We analyze the complexity of scenarios utilized in

system’s traffic flow or do not holistically capture the un-previous methods for controlling unsignalized intersections. 

derlying traffic dynamics. As such, recent studies explore The comparison of our work and example studies is pre-using RL as an alternative, given RL’s ability to handle sented in Figure 1 RIGHT. As these studies do not provide mixed traffic’s complex behaviors without making the same all measurements, we offer our best estimates. To provide traffic flow/dynamic assumptions. 

some details, COOR-PLT \(Li et al., 2023a\) uses a two-layer Recent studies have demonstrated the potential of mixed hierarchical RL approach that centrally forms RV platoons, traffic control via RL in scenarios such as ring roads, figure-



4

The International Journal of Robotics Research 0\(0\)

eight roads \(Wu et al., 2022; Poudel et al., 2024\), highway conflicts: E-L, E-C, W-L, W-C, N-L, N-C, S-L, and S-C; 

bottleneck and merge \(Vinitsky et al., 2018; Feng et al., 

and we define the conflict-free set C as \(S-C, N-C\), \(W-C, 

2021\), two-way intersections \(Yan and Wu, 2021; Villarreal

E-C\), \(S-L, N-L\), \(E-L, W-L\), \(S-C, S-L\), \(E-C, E-L\), \(N-C, 

et al., 2024\), and roundabouts \(Jang et al., 2019; Chinchali

N-L\), and \(W-C, W-L\). Conflicts may arise for the pairs of

et al., 2019\). However, these scenarios typically lack real-traffic streams that are not in C. 

world complexity and only involve a limited number of

Our design retains flexibility to accommodate various

conflicting vehicles, which contrast to our work where we traffic rules, including left-hand driving countries, or instances ensure both are present. 

where both right-turn and left-turn directions require control. 

The definition of the eight traffic streams and conflict-free set allow seamless adherence to a specific traffic regulation. To 3. Methodology

demonstrate that, we extend our approach to control 12

The pipeline of our approach is shown in Figure 2. Each RV

moving directions at four-way intersections. The experiments entering the control zone employs our method and observes in Section 4.11 show that the 12-direction policy achieves the traffic condition within the zone. The RV subsequently similar performance to our baseline policy. 

encodes the traffic condition into a fixed-length representation \(as shown in Figure 2\(a\) and elaborated in Section 3.2. Decentralized RL for mixed traffic

3.2.2\), and then uses it to make a high-level decision \(Stop or Go\) at the intersection entrance \(as shown in Figure 2\(b\)

We formulate mixed traffic control as a partially observable and elaborated in Section 3.2.1\). 

Markov decision process \(POMDP\), which consists of a

seven-tuple ðS, A, T , R, V, O, γÞ, where S is a set of states ð

3.1. Intersection traffic

s 2 SÞ, A is a set of actions ða 2 AÞ, T is the transition probabilities between states T ðs0 j s, aÞ, R is the reward A standard four-way intersection comprises four moving

function ðS × A → RÞ, V is a set of observations o 2 V, O is directions: eastbound \(E\), westbound \(W\), northbound \(N\), the set of partial observations, and γ 2 \[0, 1\) is a discount and southbound \(S\); and three turning options: left \(L\), right factor. At each time t, when the ith RV enters the control \(R\), and cross \(C\). As an example, we use E-L and E-C to zone, its action at is determined based on the current traffic i

denote left-turning traffic and crossing traffic that travel condition ot, which is a partial observation of the traffic state i

eastbound, respectively. The complete notation is shown in st of the intersection. We present the policy π

i

θ as a neural

Figure 2\(a\). We further define “conflict” as two moving network trained using the following loss:

directions intersecting each other, for example, E-C and 2

N-C. In most right-hand driving countries, such as the U.S. 

Rtþ1 þ γ

q

qθðOtþ1,a0Þ qθðOt,AtÞ

, 

and China, right-turning vehicles are typically not required tþ1 θ

Otþ1,arg max

a0

to wait for the green light. Hence, it is less important to \(1\)

coordinate right-turning traffic, which has minimal impact on intersection traffic flow. To accommodate this obser-where q denotes the output from the value network; θ and θ

vation, we consider eight traffic streams that may lead to respectively represent the value network and the target Figure 2. The pipeline of our approach. \(a\) Each RV within the control zone encodes the intersection traffic condition as a fixed-length representation, including both macroscopic traffic features such as queue length and microscopic traffic features such as vehicle locations. E, W, N, and S represent east, west, north, and south, respectively; C means crossing and L means left-turning. \(b\) The encoded traffic condition is then used by each RV to decide Stop or Go at the intersection entrance to manage mixed traffic. 

Wang et al. 

5

network \(Hessel et al., 2018\). The target network is a pe-ot ¼ ÅJ hlt, j, wt, ji ÅJ hmt, ji Å hdti, 

\(2\)

i

j

j

i

riodic copy of the value network. 

where Å is the concatenation operator and J = 8 is the total 3.2.1. Action space. As our focus is exploring mixed traffic number of traffic moving directions. 

control via RVs over traffic lights, we restrict the action space of RV to high-level decisions A = \{Stop, Go\}. An

3.2.3. Traffic condition estimation. To obtain the traffic RV’s action at 2 A determines whether the RV i should enter i

condition outside the intersection \(but within the control the intersection or stop at the intersection entrance to hold its zone\), we use a decentralized approach: the ith RV stops following vehicles. 

inside the control zone, it will compute its waiting time egowti The longitudinal acceleration of an RV is computed

and the queue length of its direction egolt ≈ dt=v

i

i

len. Here, dti

using intelligent driver model \(IDM\) \(Treiber et al., 2000\)

represents the distance from the current position of the ith when the vehicle is outside the control zone. Within the RV to the intersection, and vlen is the vehicle length plus the control zone, if the RV decides Go, it accelerates using the distance between cars, which is set to 5 m. The waiting time maximum acceleration at = amax; conversely, if the RV

and queue length are propagated to all RVs in the control decides Stop, it decelerates and comes to a halt via at = v2/

zone and aggregated to form the overall traffic condition 2dfront, where dfront is the distance to the intersection. In the along each moving direction. 

event of a potential collision, the emergency brake is au-The traffic condition estimation can be subject to mul-

tomatically engaged via the built-in collision avoidance tiple errors. First, the uniform 5 m vehicle length may lead to mechanism \(Krauss, 1998\) of the RV, overriding the re-inaccurate estimations of the queue length. Second, only quested acceleration. Further discussion of the RV is pro-RVs within the control zone broadcast their observations. 

vided in Section 3.4. 

Therefore, if most vehicles inside the control zone are HVs, wt,j and lt,j may be underestimated. Third, the lack of the 3.2.2. Observation space. To empower an RL policy to

contribution of RVs outside the control zone can result in generalize across diverse intersection topologies, we encode estimation bias. Lastly, communication issues such as poor the traffic condition observed by each RV into a fixed-length wireless connectivity can deteriorate the estimation results. 

representation. The observation for each RV within the

Thanks to our reward design and conflict resolution

control zone \(commencing from 30 m before the inter-

mechanism, our method is robust against these issues. See section\) has three elements. 

details in Section 4.10. 

· The status of RV: The distance from RV i’s current 3.2.4. Conflict-aware reward. To encourage the RV to position to the intersection, denoted as dt. 

i

consider not only its own efficiency but also the conflicts

· Traffic conditions within the control zone but outside within the intersection, we design a conflict-aware reward the intersection: The queue length lt,j and the average function for the RV:

waiting time wt,j of each of the eight traffic moving

directions that are defined in Section 3.1. These fea-

rðst, at, stþ1Þ ¼ λ

þ

LrL

pc, 

\(3\)

tures quantify the anisotropic congestion levels of an

intersection. In simulation, lt,j is computed as the

where rL is the local reward, pc is the conflict punishment, number of vehicles before the last RV in the control

and λL is the coefficient. 

zone along direction j, and wt,j is computed as the

The local reward rL is

average waiting time of RVs in the control zone along



direction j. Note that the values of lt,j and wt,j can be wtþ1,j, 

if at ¼ Stop; 

\(4\)

smaller than the actual values when RV’s penetration

wtþ1, j, 

otherwise:

rate is low. In real world, these features can be esti-

wt\+1,j is the average waiting time of all vehicles in the jth mated by each RV through V2V communication

direction, which is normalized using wt\+1,j/w

\(Cheng et al., 2015\). More discussion can be found in max and wmax =

200. p

the next section. 

c denotes the punishment for conflicts. If the RV

·

decides Stop, the local reward is the negative waiting time Traffic condition inside the intersection: We design an wt\+1,j; otherwise, it is positive wt\+1,j. 

occupancy map mt,j for each moving direction. As

The conflict punishment p

depicted in Figure 3 LEFT, we divide the inner lane c is



along a moving direction into 10 equally-sized seg-

1, 

if conflict; 

ments. A segment is labeled “occupied” with 1 if a

\(5\)

0, 

otherwise:

vehicle’s position is located within it, or labeled “free” 

with 0 if otherwise. This information is observed

If the RV’s movement conflicts with other vehicles in the through the RV’s local perception system \(Li et al., 

intersection, it incurs a penalty of 1. 

2023b\). 

The reward design is inspired by the observation that

waiting time \(Zhang et al., 2020; Greguri´c et al., 2020\) has Overall, the observation space of RV i at t is

been a popular choice in measuring traffic congestion. We



6

The International Journal of Robotics Research 0\(0\)

Figure 3. LEFT: The occupancy map along the moving direction W-L. Each of the 10 segments is labeled with either free \(green dot\) or occupied \(red dot\). MIDDLE: As learning progresses, the frequency of conflicting decisions decreases and stabilizes at a low level over all three RV penetration rates. RIGHT: Regardless of the RV penetration rate, the conflict rate \(calculated as the number of conflict decisions divided by the total number of RVs’ decisions\) stays low, for example, ∼6% for 60%, < 4% for 80% RVs, and < 3% for 100%

RVs. 

demonstrate the effectiveness of our reward design in im-Table 1. Hyperparameters of our RL algorithm. 

proving intersection traffic through extensive experimentation in Section 4.8. 

Parameters

Value

λL

1

3.2.5. RL algorithm. We employ Rainbow DQN \(Hessel

Acceleration

2.6 m/s2

et al., 2018\), a state-of-the-art RL algorithm for discrete Deceleration

4.5 m/s2

action tasks. It combines six extensions of the original DQN

Prioritized replay buffer α

0.5

algorithm \(Mnih et al., 2015\). We equip it with our reward Replay buffer capacity

50,000

function to centrally train all RVs. During execution, each Number of atoms

51

RV makes independent decisions using the shared policy, Hidden layers

\[512, 512, 512\]

structured as a neural network with three fully connected Discount factor

0.99

\(FC\) layers and each FC layer contains 512 hidden units Minibatch size

32

with ReLU as the activation function. Training takes around Learning rate

0.0005

48 h using Intel i9-13900K and NVIDIA GeForce RTX

Control zone radius

30 m

4090. Other hyperparameters are listed in Table 1. 

We choose Rainbow DQN for its outstanding perfor-

mance on discrete action tasks. However, we have explored ego RV, the ego RV is not permitted to enter the intersection. 

other RL algorithms for comparison. As shown in

When multiple RVs on conflicting streams arrive at the

Figure 19, both Rainbow DQN \(Hessel et al., 2018\) and intersection entrance and all decide Go, the RV with the PPO \(Schulman et al., 2017\) yield similar results, while highest priority score \(calculated by averaging waiting time SAC \(Haarnoja et al., 2018\) lags slightly. This result shows and queue length\) is granted entry, while the others must that our novelty and contribution are not hinged on a

wait. 

specific RL algorithm. 

We evaluate the effectiveness of the conflict resolution mechanism in Section 4.9. The results not only demonstrate the effectiveness of our approach, but also justify the ne-3.3. Conflict resolution mechanism

cessity of the mechanism. 

The fundamental cause of intersection congestion and accidents is the conflicting directions of movement. Although 3.4. Assumptions of robot vehicles

we penalize RVs for conflicting decisions, our reward

function may not completely eliminate conflicts, that is, Go Our method focuses on high-level decisions \(Stop/Go\) and decisions of RVs from conflicting directions. 

requires only basic V2V communication to obtain the

Effective learning can only take place if less conflicts positions and decisions of other RVs. It can be integrated occur during training: Conflicts will lead to congestion, into autonomous driving software, comprising other mod-which further hinders sampling and training. To avoid

ules such as perception, planning, and control to achieve the congestion, we incorporate a conflict resolution mechanism full self-driving capability. Within the pipeline of self-to post-process the RL outputs. If there are no vehicles on driving software, various components bear distinct re-conflicting streams or inside the intersection, and no con-sponsibilities for overall safety \(Muhammad et al., 2020; flicting decisions among the RVs, an ego RV who decides Shao et al., 2023\). High-level modules positioned upstream, Go will enter the intersection. If there are vehicles inside the such as perception and decision-making, are not directly intersection, particularly on the conflicting streams of the accountable for safety outcomes in most self-driving

Wang et al. 

7

vehicles to date. Downstream modules like planning and

Vehicles are routed using jtcrouter2 based on the turning control \(PnC\), on the other hand, assume greater respon-count data. By default, jtcrouter will select edges that are sibility as they need to navigate the vehicle through envi-close to the intersection as the starting and ending edges of a ronmental

uncertainties

and

ensure

collision-free

route. This can result in extremely short routes and affect the trajectories. We prioritize safety by minimizing potential simulation fidelity. To mitigate this issue, we adjust vehicle conflicts within the intersection, thereby inherently en-routes by proposing more suitable edges for vehicles’ arrival hancing the safety of the entire system. Additionally, our and departure on the network. Specifically, for traffic policy is not designed to handle physical collisions as it does streams on the main road that connects the four intersections not control the vehicle’s acceleration. When facing such an used in training the RL policy, we assign the starting and event, the PnC module should engage emergency braking to ending edges of a vehicle to be the boundary of the main avoid a collision. 

road. For traffic streams on other roads, the starting edges However, despite advancements, accidents involving

are moved to the upstream intersection and the ending edges autonomous vehicles in the U.S. have led to lingering

are moved to the downstream intersection. The route

doubts about their reliability. To navigate the landscape and planning of a vehicle is determined during traffic

tap into the L2/L3 dominated market, our method can serve reconstruction. 

as a plugin for L2/L3 driving software, acting as a sug-After re-assigning the starting edge and ending edge of gestive component. Human drivers retain responsibility for each route, duplicate traffic counts can occur. For example, a the vehicle’s safety, with the option to override suggestions vehicle traveling through intersection IV from northbound or assume direct control. As demonstrated in Section 4.5, can also travel through intersections I, II, and III, con-our method exhibits robust coordination of mixed traffic tributing to the northbound count for all four intersections. 

even when some RVs revert to HVs. These features make

To avoid duplicated counts, we consider the coordination of our method adaptable and practical across all levels of traffic flows among adjacent intersections and refine the vehicle autonomy in mixed traffic. 

number of routes for ensuring matching turning counts in For low-level control of the RV, we employ the traffic

simulation and actual data. 

simulator simulation of urban mobility \(SUMO\) \(Behrisch

We use Geoffrey E. Havers Statistic \(GEH\), a widely

et al., 2011\). It includes human driving models, configurable used metric to assess the similarity between simulated traffic traffic networks and flows, and mechanisms for enforcing flow and real-world traffic flow:

traffic rules, safety rules, and physical constraints. The built-sffiffiffiffiffiffiffiffiffiffiffiffiffiffiffiffiffiffiffiffiffiffi in collision avoidance mechanism \(Krauss, 1998\) and human 2ðM CÞ2

driving model \(Treiber et al., 2000\) will act as the down-GEH ¼

, 

\(6\)

M þ C

stream modules of self-driving software and the human

driver, respectively. These mechanisms and models will

where M and C represent the turning counts of simulated ensure collision-free driving of a vehicle. This assumption traffic flow and observed traffic flow, respectively. In has been widely adopted by previous studies \(Yan and Wu, 

transportation engineering, it is generally accepted that

2021; Wu et al., 2022; Zhang et al., 2023; Cui et al., 2021\). 

simulated traffic resembles real-world traffic when GEH <5

\(Timothy and Marzenna, 2005; El Esawey and Sayed, 

2011\). We compute the average GEH using all turning 4. Experiments and results

counts at all six intersections. The resulting values are 1.97, 1.49, 1.84, 2.34, 1.87, and 2.19, indicating our simulation’s 4.1. Mixed traffic

high fidelity. 

4.1.1. Reconstruction and simulation. In order for RVs to interact with HVs under real-world traffic conditions, we 4.1.2. Mixed traffic generation. To create mixed traffic, a need to first reconstruct traffic using actual traffic data and newly spawned vehicle will be randomly assigned to be

then pursue high-fidelity simulations. We reconstruct the either RVor HV according to a pre-specified RV penetration intersection traffic using turning count data at each inter-rate. For HV, the longitudinal acceleration is computed section provided by the city of Colorado Springs, CO, 

using intelligent driver model \(IDM\) \(Treiber et al., 2000\). 

USA.1 The turning count data records the number of ve-For RV, when it is outside the control zone, IDM is used to hicles moving in a particular direction at the intersection and determine the longitudinal acceleration; when it is inside the is collected via in-road sensors such as infrastructure-control zone, the high-level decisions Stop/Go are deter-mounted radars. We have in total six intersections’ data mined by the RL policy, while the low-level longitudinal and we label these intersections I, II, III, IV, V, and VI, acceleration is determined by the formulas introduced in respectively. We use intersections I–IV to train the RL

Section 3.2.1. 

policy. Given the GIS data \(traffic data and digital map\), we pursue traffic simulations in SUMO. A directed graph is 4.2. Experiment set-up

used to describe the simulation area: Each edge of the graph represents a road segment with an ID and a vehicle’s route is Our evaluation metric is the average waiting time \(Zhang

defined by a list of edge IDs. 

et al., 2020; Greguri´c et al., 2020\) of all vehicles. We define

8

The International Journal of Robotics Research 0\(0\)

the waiting time of each vehicle as the total consecutive time 4.4. Individual intersection performance

it remains still in the control zone. The average waiting time for a moving direction is the mean of the waiting times of all In Figure 5, we show the detailed performance of our vehicles in that direction, while the average waiting time for method at intersection I. The results include two parts. The an intersection is the mean of the waiting times of all ve-LEFT sub-figure reports the influence of different RV

hicles at the intersection. 

penetration rates on the average waiting time. The RIGHT

sub-figure displays the zoomed-in version of the LEFT sub-We evaluate our method by comparing it to four

fi

baselines: \(1\)

gure by excluding the NoTL and Yan methods because of

TL: the traffic signal program deployed in

the city of Colorado Spring, CO; \(2\)

their subpar performance. We can see that the average

NoTL: no traffic

lights; \(3\)

waiting time continuously reduces when the RV penetration Yan: the state-of-the-art RL traffic controller

with 100% RV penetration rate \(Yan and Wu, 2021\); 3 and rate increases from 20% to 100%. In general, our method \(4\)

starts to outperform TL and Yang when the RV penetration Yang: the state-of-the-art CAV control method for

unsignalized intersections \(Yang and Oguchi, 2020\). Our rate is 60% or higher. 

RVs are trained at intersections I, II, III, and IV. We We further show traffic congestion levels of intersection I in Figure 4. The congestion level CL is defined as CL = min evaluate RVs’ performance at all six intersections, including the unseen, three-way intersection VI. All inter-

\(AWT/Threshold, 1.0\), where AWT is the average waiting

sections are described in Table 2. Furthermore, we evaluate time of all vehicles in a specific direction, which is nor-our method on three manually-generated intersections with malized by the median value of the average waiting time of different topologies \(3-Lane, 4-Lane, and 7-Lane\) and

the baseline TL at the intersection, that is, Threshold. The traffic demands. The details of these scenarios are intro-Threshold is 46.5 for intersection I. As a result, traffic duced in Table 4. 

controlled via our method achieves much lower congestion levels than TL. In addition, our method can flexibly coordinate conflicting moving directions based on varied

4.3. Overall performance

traffic conditions, which is different from TL that employs fi

Table 3 shows the main results measured with reduced xed-phase coordination. 

average waiting time in percentage at intersections I, II, III, 

Figures 6–8 show the detailed performance of our method and IV. We test RV penetration rates from 20% to 100%, 

at intersections II, III, and IV, respectively. Similar results are conducting 10 experiments at each rate and reporting the observed: Our method significantly overtakes Yang and TL

averaged results. Each experiment lasts 1000 steps \(1000 s with 20%, 70%, and 50% RV penetration rates. 

in simulation\) and is repeated 100 times. The location and behaviors of HVs are stochastic. The performance of our 4.5. Blackout

method varies at different intersections. With only 20%

RVs, our method can surpass the traffic light control at To demonstrate our approach’s robustness, we simulate

intersection II where we perform best. At other intersec-blackout events in which all traffic signals are suddenly off. 

tions, our method with 60% can outperform the traffic signal

Figure 9 shows the results of no RV and 50% RVs. In case of control baseline. An example comparing our approach with no RV, a gridlock will form at the intersection within 15 min using traffic lights on all moving directions at intersection I after the traffic lights are off \(starting from the 5th minute\). In is shown in Figure 4. In the absence of traffic lights and with contrast, with 50% RVs, no congestion is observed. See

100% RVs, we can achieve up to 89% reduction in average

Figure 9 for demonstrations. More results are shown in waiting time. These findings show that our approach can

Figure 10. The blackouts occur at the 100th step. Without scale to various RV penetration rates while efficiently co-RVs, the absence of traffic lights leads to significant increases ordinating mixed traffic. 

in average waiting time due to gradually formed congestion. 

However, with the presence of 50% RVs, the average waiting time remains stable during the blackouts. Essentially, our Table 2. Real-world intersections used in training and testing \(see method enables RVs to act as “self-organized traffic lights,” 

I, II, III, and IV in Figure 1 and V and VI in Figure 14\). Actual which effectively coordinate traffic at the intersection. 

traffic demand is provided. We also list the number of non-empty We also examine the impact of sudden RV rate drops on

lanes since some lanes do not show traveling vehicles. 

our approach. The sudden drops could occur due to unstable V2V communication, software failures, humans taking over Num. incoming Num. non-Traffic demand

Intersection lanes

empty lanes

\(v/h \* lane\)

the control, and more. The “offline” RVs are simulated

using the IDM model \(Treiber et al., 2000\). The results are I

21

19

1157

shown in Figure 11. All drops occur at the 100th step. Our II

19

18

1089

method has significantly reduced the waiting time compared III

18

17

928

to NoTL. The trials using NoTL display exponential in-

IV

16

14

789

creases in average waiting time, indicating the form of V

24

24

987

traffic deadlocks. In contrast, at intersection II, our approach VI

10

10

1115

effectively stabilizes the system and avoids congestion by





Wang et al. 

9

Table 3. Reduced average waiting time in percentage at each intersection under different RV penetration rates. Our method outperforms traffic signals in all cases when the RV penetration rate ≥ 70%. More time is saved with higher RV penetration rates. Compared to scenarios without traffic lights, our method can achieve up to 89% reduction in average waiting time with 100% RVs. 

Reduced average waiting time \(%\)

Compared to TL \(%\)

Compared to NoTL \(%\)

Intersection I

15.04

0.34

25.98

32.60

40.75

42.01

89.91

Intersection II

41.78

48.77

48.90

51.84

53.46

52.80

61.46

Intersection III

40.53

2.83

2.75

13.39

10.60

22.33

66.72

Intersection IV

15.91

8.20

9.70

44.47

52.19

66.63

81.73

RV rate

50

60

70

80

90

100

100

Figure 4. Traffic congestion levels at intersection I under different control mechanisms. Our approach with 80% RVs consistently achieves lower congestion levels than Yang and TL. Unlike Yang and TL, which control intersection traffic using fixed phases, our method learns to use adaptive phases in control. 

Figure 5. The overall results in average waiting time at intersection I. The RIGHT sub-figure displays zoomed-in version of the LEFT

sub-figure, excluding the NoTL and Yan methods. When the RV penetration rate reaches or exceeds 60%, our method consistently outperforms the other four baselines. 

maintaining a low average waiting time. At the other three observe an overall increase in average waiting time as in-intersections, our method stabilizes the system when the RV

coming traffic flows continue. We analyze the slope of the penetration rate reaches 90%, with no significant increase in average waiting time curves to identify the rising trend of waiting time. Considering other RV penetration rates, we congestion levels. As shown in Figure 12, if the slope





10

The International Journal of Robotics Research 0\(0\)

Figure 6. The overall results in average waiting time at intersection II. The RIGHT sub-figure displays zoomed-in version of the LEFT

sub-figure, excluding NoTL and Yan. With 20% or more RVs, our method consistently outperforms all other baselines. 

Figure 7. The overall results in average waiting time at intersection III. The RIGHT sub-figure displays zoomed-in version of the LEFT

sub-figure, excluding NoTL and Yan, which perform significantly worse than our method. Our method begins to outperform TL and Yang when the RV penetration rate reaches 60–70% or higher. 

approaches 1, there is a higher likelihood of deadlock. 

observe congestion starting to form at 200 v/h, indicated by However, in scenarios where our method is deployed, the a low average speed of all vehicles at the intersection \(we rising trend plateaus below 0.4 after 2000 simulation steps define congestion when average vehicle speed < 1 m/s. 

show effective congestion management. In comparison, 

In contrast, with the actual traffic demand 700 v/h, 

NoTL’s AWT trend approaches nearly 0.8, hinting severe

congestion does not form with just 5% RVs in mixed

congestion. 

traffic controlled by our algorithm. Figure 13 also demonstrates that the minimum RV penetration rate required to avoid congestion under the real-world traffic demand is 5%. 

4.6. Traffic demands and congestion

We further analyze the relationship of traffic demands and 4.7. Generalization

congestion. The results using intersection I as the testbed are shown in Figure 13. By increasing the traffic demand from To evaluate the generalizability of our approach, we first test it 150 v/h to 300 v/h with no traffic lights and no RVs, we on two previously unseen real-world intersections shown in





Wang et al. 

11

Figure 8. The overall results in average waiting time at intersection IV. The RIGHT sub-figure displays zoomed-in version of the LEFT

sub-figure, excluding NoTL and Yan. Our method with 60% RVs or more outperforms all four baselines. 

Figure 9. Comparison between traffic conditions with and without RVs during a blackout event at intersection I. The blackout event occurs at the 5-min mark. Congestion forms rapidly within 15 min in traffic without RVs. Conversely, traffic regulated with 50% RVs does not result in congestion. 

Figure 10. Blackout experiments. We simulate blackout events \(traffic signals off\) at intersections I, II, III, and IV \(from left to right\) since the 100th step. Without any RV, a gridlock will form at the intersection causing the average waiting time of all vehicles to increase rapidly. In contrast, with 50% RVs, no gridlock appears and the waiting time of all vehicles remains low and stable. 





12

The International Journal of Robotics Research 0\(0\)

Figure 11. Our method ensures stable and uncongested traffic, even when the RV penetration rate abruptly drops. The sub-figures from left to right correspond to intersections I, II, III, and IV. NoTL displays exponential increases in average waiting time, indicative of traffic deadlocks. 

Figure 12. The slope of average waiting time \(AWT\) when the RV penetration rate suddenly drops. The sub-figures from left to right correspond to intersections I, II, III, and IV. The slope of AWT successfully plateaus when our method is activated, indicating effective congestion management. 

Figure 13. LEFT: The solid lines represent no traffic lights and no RVs. The congestion starts to form when the demand is over 200 v/h. 

The real-world demand denoted using the dashed line, which is about 700 v/h, does not build congestion because 5% RVs are deployed in traffic. RIGHT: Analyzing the influence of low RV penetration rates on traffic. As a result, 5% is the minimum to prevent congestion. 

For both figures, the study subject is intersection I. 



Wang et al. 

13

Figure 14, one of which is a three-way intersection. We The designed reward should promptly reflect the se-apply our policy directly to the unseen four-way inter-

verity of congestion and traffic conditions at an intersection without refinement, and it functions well. As

section. Figure 18 illustrates the traffic conditions during shown in Figure 15\(a\), our policy can achieve comparable NoTL \(no traffic lights and 100% HVs\) and average

performance to conventional traffic signal baseline when vehicle speed of using our reward and Yan and Wu

the RV penetration rate is 60% or higher. Our policy is also

\(2021\)’s reward. The average vehicle speed is used to deployed without refinement at the unseen three-way

indicate congestion severity. We consider an intersection intersection, which requires coordination among only

congested if the average speed is < 1 m/s. In Figure 18, 

four directions: S-C, S-L, W-L, and N-C. Our policy

congestion arises when there are no traffic lights and

adapts to this case by setting the input values of other 100% HVs, resulting in a rapid decrease in the average

directions to zero. Despite never encountering this to-

speed of all vehicles \(orange curve\). Our reward \(blue

pology and the corresponding traffic demand, our policy curve\) promptly captures this trend, making it an effective coordinates traffic well. As shown in Figure 15\(b\), our indicator for the learning process. In contrast, the reward approach outperforms the traffic light baseline when RV

of the state-of-the-art method by Yan and Wu \(2021\) fails penetration is at 40% or higher. At 90% RV penetration, to do so. 

our method reduces the average waiting time by ap-

The reward function by Yan and Wu \(2021\) takes the proximately 62.5% compared to using traffic lights. These format RY an ¼ outflowðst,stþ1Þ collisionðst,stþ1Þ, 

results demonstrate the excellent generalizablility of our where outflowðst, stþ1Þ denotes the number of vehicles

approach. 

exiting the network from t to t \+ 1, and collisionðst, stþ1Þ

We further investigate the generalizability by testing our is the number of collisions in the network from t to t \+ 1. We approach at three manually-created intersections, each with record this reward during the evaluation of NoTL to analyze a distinct topology and traffic demand. The intersections its characteristics. As anticipated, the absence of traffic lights have different numbers of incoming lanes per direction, leads to intersection congestion, evidenced by the average allowing us to simulate a wide range of traffic scenarios, as speed of all vehicles rapidly approaching zero. However, shown in Figure 16. Traffic flows are generated using the Yan’s reward fails to capture changes in traffic conditions profiles detailed in Table 4. The results, presented in promptly. This is due to the outflow of a network being a

Figure 17, demonstrate that our method can effectively delayed indicator; congestion within the intersection does not coordinate traffic at these unseen environments as well. 

prevent previously cleared vehicles from contributing to the With approximately 70% of RVs, our approach outperforms outflow. Consequently, the delayed reward hinders the

traditional traffic light control. 

learning process, with episodes often terminating due to congestion before the reward can manifest it. In contrast, our reward function captures the immediate impact of traffic 4.8. Evaluation of reward function

conditions by incorporating the waiting time of traffic streams. 

This provides the RL agent with an explicit optimization Designing effective rewards for controlling mixed traffic at objective. 

complex intersections is an open problem to date. Varied intersection topology, conflicting traffic streams, and the use of real-world traffic data that can lead to unpredictable and 4.9. Evaluation of conflict resolution

unstable inflow/outflow all complicate the task. To address conflicts within intersections and prevent traffic conges-Our algorithm and reward design aim to minimize potential tions, our insight is to consider the impact of each RV’s conflicts within the intersection, which not only improves actions on traffic flow in its own direction, while penalizing the effectiveness of RL training, but also implicitly im-conflicting decisions among RVs. 

proves the road safety inside the intersection. To evaluate Figure 14. Two unseen real-world intersections used in our test. LEFT: Intersection V, four-leg. RIGHT: Intersection VI, three-leg. 





14

The International Journal of Robotics Research 0\(0\)

Figure 15. Overall results in the average waiting time at the intersection V and VI. Starting from 60–70% RVs, our method outperforms the traffic lights \(TL\) baseline at the intersection V. Additionally, our approach starts to outperform the TL baseline when RVs are 40%

or more at the intersection VI. \(a\) Intersection V. \(b\) Intersection VI. 

Figure 16. Three manually-created intersections in SUMO to further investigate our method’s generalization capability. Each intersection has different topologies and traffic demands. \(a\) 3-lane scenario. \(b\) 4-lane scenario. \(c\) 7-lane scenario. 

Table 4. The traffic demand profiles of the manually-generated indicates that the policy successfully learns to prevent intersections. 

conflicting movements. In Figure 3 RIGHT, the conflict rate for 80% RVs converges around 4%, while the conflict rate Scenario

Num. incoming lanes

Traffic demand \(v/h \* lane\)

for 100% RVs is less than 3% after 500 steps during

3-Lane

12

550

evaluation. These results demonstrate that our trained RL

4-Lane

16

412

policy successfully learns to avoid conflicts, thereby en-7-Lane

28

235

hancing traffic safety. 

To justify the effectiveness and necessity of conflict

resolution mechanism in training, we conduct ablation

studies. As depicted in Figure 19, the absence of the conflict the effectiveness of our reward function in avoiding conflict, resolution mechanism \(PPO w/o Mech, SAC w/o Mech and

we calculate the conflict rate as the ratio of conflicts to the R. DQN w/o Mech\) leads to no reduction in waiting time, number of RVs within the control zone. As shown in

indicating ineffective learning. In contrast, with the conflict

Figure 3 MIDDLE, the number of conflicts decreases as resolution mechanism, all RL algorithms demonstrate rapid training progresses and stabilizes at a low level. This learning and convergence. 





Wang et al. 

15

Figure 17. From left to right, our results at manually-generated 3-lane, 4-lane, and 7-lane intersections shown in Figure 16. Our method successfully regulates traffic in these unseen intersections without fine-tuning. 

4.10. Robustness in potential real-world

deployment

Our method is designed for decentralized execution. As we discussed in Section 3.2.2, the input to our policy requires both V2V information and local perception. The inference process is described in Alg. 1. 

Figure 18. When congestion occurs during the NoTL setup, the average speed within the intersection decreases to nearly zero \(orange curve\). Our reward can promptly respond to congestion, indicated by the decreasing negative reward curve in the LEFT

sub-figure. In contrast, the reward from Yan and Wu \(2021\)

incorrectly increases as congestion worsens, as shown in the RIGHT sub-figure. 

Our method can be potentially applied to real-world RVs which are equipped with V2V capabilities and self-driving Figure 19. Visualization of the cumulative waiting time per software. However, conducting real-world experiments for rollout when training various RL algorithms, such as SAC, PPO, mixed traffic control can be expensive. Therefore, we

R. DQN \(Rainbow DQN\), R. DQN w/o Mech \(Rainbow DQN

without conflict resolution mechanism\), SAC w/o Mech, and PPO

validate our approach through simulation. In particular, w/o Mech. PPO and Rainbow DQN demonstrate similar

whether the decision-making of the RV described in Alg. 1

convergence. However, without our conflict resolution

is robust to traffic conditions estimated from real-world mechanism \(Mech\), all algorithms fail to learn, indicated by a high observations. 

As

discussed

in

Section

3.2.2, 

RL

waiting time after 500 epochs of training. 



16

The International Journal of Robotics Research 0\(0\)

observations are estimated from local perception and V2V

communication using technologies such as LTE, WiMax, or Bluetooth. Due to the variability in connectivity quality and range, multi-hop communication and potential packet errors or losses are inevitable \(Vegni and Little, 2010\). Hence, it is crucial to assess our method under different communication conditions. To achieve this, we simulate two types of

connectivity protocols:

· Long-range connectivity \(e.g., LTE and WiMax\): In

this protocol, vehicles within 150

m can directly

communicate and exchange information with each other

Figure 20. Two distinct real-world deployment setups, long-range using a single hop, without the need for intermediary

connectivity and short-range connectivity. LEFT: Long-range nodes. See Figure 20 LEFT. 

connectivity enables seamless broadcasting of vehicle

· Short-range connectivity \(e.g., Bluetooth\): This pro- information, accessible to all nearby vehicles around the intersection. RIGHT: With short-range connectivity, messages tocol uses short-range communication techniques, al-necessitate up to three hops before reaching their destinations. 

lowing vehicles to communicate around an intersection

with up to three hops, each spanning up to 50

m. The

communication process involves four steps: \(1\) Vehicles in where PER denotes the package error rate, and \#hops

the same direction form clusters, with the leading vehicle denotes the number of hops on the connectivity link. To designated as the master node; \(2\) each vehicle transmits its examine the impact of different connectivity conditions local information to the master node of its cluster; \(3\) on our estimated traffic, we calculate the relative esti-master nodes exchange gathered information with master

mation error \(%\) as follows:

nodes of other clusters; and \(4\) the master node distributes the information from other directions back to the slave estimation error ¼ actual value estimated value



×100%:

nodes within its cluster. See Figure 20 RIGHT. 

actual value

This calculation is performed for both estimated queue length Simulating these two distinct connectivity protocols

and waiting time. The estimation is obtained from the infor-allows us to evaluate the robustness and efficiency of our mation received from the V2V communication, while the

method. The long-range connectivity ensures minimal

actual value is determined using the ground-truth traffic latency through direct communication, while the short-condition. Based on the relative estimation error visualized in range connectivity assesses performance in a more

Figures 21\(a\) and \(b\), we observe that the error increases with complex, multi-hop, high-latency communication envi-

\#hops and packet error rate \(PER\). This leads to increased ronment. As the message to be shared among vehicles is

observation uncertainty for the policy during experiments. For brief and can be swiftly exchanged, we assume that the

instance, when PER reaches 20% in short-range connectivity, communication process between vehicles is rapid, with

the estimation error of queue length exceeds 20%. This sig-all communication completed within 1 s, including both

nificant error makes decentralized traffic coordination more one-hop and multi-hop connectivity. This aligns with the challenging. However, as shown in Figure 22, our method fact that our proposed policy operates at 1 Hz. 

demonstrates robustness to varying V2V conditions, including In addition to connectivity range, the reliability of

multi-hop communication \(one-hop and three-hop\) and dif-connectivity is another critical factor in real-world

ferent PER assumptions \(1%, 5%, 10%, 15%, and 20%\). 

wireless

communication. 

For

example, 

the

IEEE

Remarkably, our method maintains robust performance even 802.11a standard specifies a maximum tolerable package

under extreme conditions, such as three-hops and 20% PER. 

error rate \(PER\) of 10% \(IEEE Standards Association, 

When the probability of connectivity is low, such as one-hop

1999\). Despite the integration of sophisticated network communication with 1% PER, our method achieves perfor-protocols equipped with various error mitigation mech-

mance similar to the RL policy with precise observation. 

anisms, it is essential to evaluate the impact of connec-However, as observation uncertainty increases, the coordi-tivity errors on our system. Therefore, we conduct

nation performance diminishes but is still acceptable. These multiple experiments to simulate various package error

experiments highlight the robustness of our method and

rates, ranging from 1% to 20%. In these simulations, we showcase its potential for real-world deployment. 

assume that each V2V connection operates indepen-

dently, with an equal chance of encountering connectivity 4.11. Extension to right-turn traffic

errors. If a connectivity error occurs, the shared information becomes inaccessible to the affected receivers. As Our simulation is constructed using Geographic Informa-a result, the probability of successfully receiving shared tion System \(GIS\) data sourced from the U.S., a country information can be calculated as Pinfo = \(1 PER\)\#hops, 

with right-hand traffic norms. However, traffic regulations





Wang et al. 

17

vary across nations; for instance, in left-hand traffic accommodating right turns, achieves performance compa-countries, right-turn traffic requires control. Our method rable to our original policy. Notably, the average waiting maintains adaptability to accommodate diverse scenarios time of the right-turn traffic is significantly shorter com-with varying traffic rules. By adjusting traffic streams and pared to other directions, which also demonstrates that the conflict-free movements, our methods can seamlessly ad-right-turn traffic has minimal impact within the traffic here to specific requirements, for example, incorporating scenarios analyzed in this study. This experiment illustrates and regulating the right-turn traffic. 

the flexibility of our method and its potential applicability To showcase this adaptability, we have retrained the

across various traffic rules. 

policy to include right turns, with 70% RVs and tested it at intersection V. This particular intersection does not have a 5. Discussion

right-turn ramp, meaning that vehicles from all four incoming directions can enter the intersection. As indicated in While our approach demonstrates promising results in

Table 5, we report the average waiting time of all vehicles large-scale mixed traffic control at complex intersections, across all 12 moving directions. The new policy, now

we acknowledge several inherent limitations that are worth further exploration. 

First, our current learning framework lacks a hierar-

chical structure, which could be supplemented by low-

level sub-policies such as longitudinal and lateral de/

accelerations, as well as lane changes. This deficiency can hinder the granularity and responsiveness of traffic regulation, potentially compromising the efficiency and safety of both RVs and HVs. For example, when the

penetration rate of RVs is low, the absence of lane change functionality in RVs can result in congestion and deadlock, as HVs can simply bypass RV regulations by changing

lanes frequently. To address this issue, RVs should be able to change lanes or decelerate to influence nearby HVs, 

encouraging them to comply with RV’s regulations for

more efficient traffic. Additionally, RVs should actively regulate traffic flow within intersections, rather than simply acting as mobile traffic lights. While this concept offers greater regulation potential, it also presents significant challenges in complex intersectional traffic

scenarios. 

Second, our method employs a relatively rigid conflict

Figure 21. The relative error of traffic condition estimation under resolution mechanism, in terms of a pre-defined if-else rule different V2V communication protocols and PER \(package

that restricts vehicle movement at intersections. Though the error rate\) levels. \(a\) The estimation error of one-hop V2V

communication. \(b\) The estimation error of three-hop V2V

constrained exploration space is beneficial for training ef-communication. 

ficiency and safety \(Alshiekh et al., 2018\), it is still possible Figure 22. From left to right, evaluation of our method in simulated V2V communication experiments with 60% RVs at intersections I, II, III, and IV. The results demonstrate that our method can effectively address the communication uncertainty arising from multi-hop communication and low-quality connection. 

18

The International Journal of Robotics Research 0\(0\)

Table 5. Result of right-turning experiments. We report the average waiting time of all vehicles along each moving direction. 

Directions

S-C

S-L

S-R

W-C

W-L

W-R

N-C

N-L

N-R

E-C

E-L

E-R

All

Right-turn-enabled

27.4

12.0

1.79

20.9

11.0

0.23

31.7

14.0

0.77

19.8

9.67

0.67

18.3

Baseline

15.4

18.7

N/A

16.6

18.8

N/A

21.1

16.8

N/A

26.8

15.8

N/A

19.9

that the optimal solution lies beyond the exploration

intricate mixed traffic intersection scenarios when com-boundaries set by this mechanism. Therefore, future ex-

pared to existing literature, encompassing diverse inter-ploration could consider relaxing these constraints, for section capacities, topologies, and fluctuating traffic example using real-world demonstration data \(Leung et al., 

demands. Our approach encompasses numerous inno-

2023\), which could improve overall traffic efficiency vative designs tailored for mixed traffic control. To ad-without compromising safety. 

dress the diverse range of road topologies and traffic

Third, our traffic status encoder is currently designed for demands, we introduce a generic representation for en-intersections with a maximum of four ways, and it must be coding intersection traffic conditions, ensuring enhanced expanded to accommodate other topologies, such as multi-generalizability. To optimize traffic efficiency and min-way intersections and roundabouts. Addressing this limi-imize conflicting movements, we devise a conflict-aware tation is crucial to broaden the usability and adaptability of reward function specifically for coordinating large-scale the proposed method. One possible solution is to use a graph mixed traffic at intersections. This function not only

convolutional network \(GCN\) to model the intersection. 

serves as a timely incentive for the RL agent but also

However, existing GCN methods like Bai et al. \(2020\) only boosts the training performance. We also introduce a

model the topology of the intersection and cannot capture conflict resolution mechanism aimed at preventing con-the complex geometric details inside the intersection that is flicts as well as improving training efficiency. Lastly, we necessary for real-world intersection traffic regulation. 

provide a high-fidelity traffic simulation reconstructed Fourth, we use IDM \(Treiber et al., 2000\) to simulate using real traffic data for robust training and testing. 

interactions between RVs and HVs. However, IDM can be

Our method is the first to control mixed traffic under real-replaced by other advanced methods, such as learning-based world traffic conditions at complex intersections. Various simulations for autonomous driving and traffic \(Guo et al., 

experiments are conducted to show the effectiveness, ro-

2024\), to capture the accurate interaction between HVs and bustness, generalizablility, and adaptability of our approach. 

RVs. Nevertheless, these learning-based models may some-Detailed analyses are also pursued to justify the design of times be unstable, leading to erroneous outputs that could the components of our method. Our method can serve as an negatively impact the RL agent. Additionally, most of the inspiration for mixed traffic control via model-free RL at traffic data used in these methods are based on HVs’ regular large-scale and complex scenarios, paving the way for next-trajectories in stable traffic, lacking the active responses of generation traffic control strategies. 

HVs to mixed traffic conditions. Therefore, an important next step would be to collect real-world traffic data in complex Declaration of conflicting interests

intersections with dynamic and rich HV–RV interaction. 

The author\(s\) declared no potential conflicts of interest with re-Finally, we currently rely solely on RV information within spect to the research, authorship, and/or publication of this article. 

the control zone to estimate traffic conditions, which may lead to significant errors. Although HVs in mixed traffic Funding

cannot be directly controlled like RVs, they can still provide valuable traffic information. For example, by utilizing on-The author\(s\) disclosed receipt of the following financial board GPS or Google Map APIs, HVs can measure their ego support for the research, authorship, and/or publication of this queue lengths and waiting times in the direction they are article: Dawei Wang and Jia Pan are partially supported by the moving. This data can enhance the accuracy of traffic con-Innovation and Technology Commission of the HKSAR

dition estimation, resulting in improved traffic regulation Government under the InnoHK initiative, and Research Grant performance within our RL framework. However, it also

Council \(Ref: 17200924\), Hong Kong. National Science

brings additional challenges, including privacy concerns and Foundation; IIS-2153426 and Innovation and Technology

the need for standardized communication protocols. These Fund; GHP/126/21GD. 

challenges can be addressed by implementing privacy-

preserving crowdsourcing techniques \(Wang et al., 2023a\). 

ORCID iD

Jia Pan  https://orcid.org/0000-0001-9003-2054

6. Conclusion

We propose a decentralized RL approach for the control

Notes

and coordination of mixed traffic at real-world and un-

1. https://coloradosprings.gov/. 

signalized intersections. Our method tackles the most

2. https://sumo.dlr.de/docs/jtrrouter.html. 

Wang et al. 

19

3. To apply this approach, we extend the network input to the Gregurić M, Vujić M, Alexopoulos C, et al. \(2020\) Application of maximum number of incoming lanes to accommodate a real-deep reinforcement learning in traffic signal control: an world intersection. 

overview and impact of open traffic data. Applied Sciences 10\(11\): 4011. 

References

Guo K, Miao Z, Jing W, et al. \(2024\) Lasil: learner-aware su-Alshiekh M, Bloem R, Ehlers R, et al. \(2018\) Safe reinforcement pervised imitation learning for long-term microscopic traffic learning via shielding. In: Proceedings of the thirty-second simulation. ArXiv preprint arXiv:2403.17601. 

AAAI conference on artificial intelligence and thirtieth in-Haarnoja T, Zhou A, Abbeel P, et al. \(2018\) Soft actor-critic: off-novative applications of artificial intelligence conference and policy maximum entropy deep reinforcement learning with a eighth AAAI symposium on educational advances in artificial stochastic actor. In: International conference on machine intelligence, AAAI’18/IAAI’18/EAAI’18, New Orleans, LA, learning, Stockholm, Sweden, 10–15 July 2018, 1861–1870. 

2–7 February 2018, 2669–2678. AAAI Press. 

PMLR. 

Bai L, Yao L, Li C, et al \(2020\) Adaptive graph convolutional Hessel M, Modayil J, Van Hasselt H, et al \(2018\) Rainbow: recurrent network for traffic forecasting. In: Proceedings of the combining improvements in deep reinforcement learning. In: 34th international conference on neural information processing Proceedings of the AAAI conference on artificial intelligence, systems, NIPS’ 20, Vancouver, BC, 6-12, December, 2020, New Orleans, Louisiana, USA, February 2-7, 2018, pp. 

17804–17815. Curran Associates Inc. 

3215–3222. 

Behrisch M, Bieker L, Erdmann J, et al. \(2011\) Sumo–simulation Hickert C, Li S and Wu C \(2023\) Cooperation for scalable su-of urban mobility: an overview. In: Proceedings of interna-pervision of autonomy in mixed traffic. IEEE Transactions on tional conference on advances in system simulation, Barce-Robotics 39\(4\): 2751–2769. 

lona, Spain, 23–29 October 2011, 63–68. ThinkMind. 

IEEE Standards Association \(1999\) Wireless LAN Medium Access Cai P, Lee Y, Luo Y, et al. \(2020\) Summit: a simulator for urban Control \(MAC\) and Physical Layer \(PHY\) Specifications:

driving in massive mixed traffic. In: IEEE international High-Speed Physical Layer in the 5 GHz Band. New York, 

conference on robotics and automation \(ICRA\), Paris, France, NY: IEEE. 

31 May 2020–31 August 2020, pp. 4023–4029. 

Jácome L, Benavides L, Jara D, et al. \(2018\) A survey on intel-Chen X, Hu M, Xu B, et al. \(2022\) Improved reservation-based ligent traffic lights. In: 2018 IEEE international conference on method with controllable gap strategy for vehicle coordina-automation/XXIII congress of the Chilean association of tion at non-signalized intersections. Physica A: Statistical automatic control \(ICA-ACCA\), Concepcion, Chile, 17–19

Mechanics and Its Applications 604: 127953. 

October 2018, 1–6. IEEE. 

Cheng X, Yang L and Shen X \(2015\) D2d for intelligent trans-Jang K, Vinitsky E, Chalaki B, et al. \(2019\) Simulation to scaled city: portation systems: a feasibility study. IEEE Transactions on zero-shot policy transfer for traffic control via autonomous ve-Intelligent Transportation Systems 16\(4\): 1784–1793. 

hicles. In: ACM/IEEE international conference on cyber-physical Chinchali SP, Livingston SC, Chen M, et al. \(2019\) Multi-systems, Montreal, QC, 16–18 April 2019, pp. 291–300. 

objective optimal control for proactive decision making Karimi M, Roncoli C, Alecsandru C, et al. \(2020\) Cooperative with temporal logic models. The International Journal of merging control via trajectory optimization in mixed vehic-Robotics Research 38\(12–13\): 1490–1512. 

ular traffic. Transportation Research Part C: Emerging

Choi EH \(2010\) Crash Factors in Intersection-Related Crashes: An Technologies 116: 102663. 

On-Scene Perspective. Washington, DC: National Highway

Krauss S \(1998\) Microscopic modeling of traffic flow: investi-Traffic Safety Administration, U.S. Department of Transportation. 

gation of collision free vehicle dynamics. Research Report Cui J, Macke W, Yedidsion H, et al. \(2021\) Scalable multiagent 98-08, German Aerospace Center 1998. 

driving policies for reducing traffic congestion. In: Pro-Leung K, Veer S, Schmerling E, et al. \(2023\) Learning autonomous ceedings of the 20th international conference on autonomous vehicle safety concepts from demonstrations. In: American agents and multiagent systems \(AAMAS\), Online, 3–7 May

control conference, San Diego, CA, 31 May 2023–02 June

2021, pp. 386–394. 

2023, pp. 3193–3200. 

Dai Q, Xu X, Guo W, et al. \(2021\) Towards a systematic com-Li H, Sima C, Dai J, et al. \(2023b\) Delving into the devils of bird’s-putational framework for modeling multi-agent decision-

eye-view perception: a review, evaluation and recipe. IEEE

making at micro level for smart vehicles in a smart world. 

Transactions on Pattern Analysis and Machine Intelligence Robotics and Autonomous Systems 144: 103859. 

46\(4\): 2151–2170. 

El Esawey M and Sayed T \(2011\) Calibration and validation of Li D, Zhu F, Chen T, et al. \(2023a\) Coor-plt: a hierarchical control micro-simulation of medium-size networks. Advances in

model for coordinating adaptive platoons of connected and Transportation Studies 24: 97888548415126. 

autonomous vehicles at signal-free intersections based on Feng S, Yan X, Sun H, et al. \(2021\) Intelligent driving intelligence deep reinforcement learning. Transportation Research Part test for autonomous vehicles with naturalistic and adversarial C: Emerging Technologies 146: 103933. 

environment. Nature Communications 12\(1\): 1–14. 

Lu J, Hossain S, Sheng W, et al. \(2023\) Cooperative driving in Feng S, Sun H, Yan X, et al. \(2023\) Dense reinforcement learning mixed traffic of manned and unmanned vehicles based on

for safety validation of autonomous vehicles. Nature

human driving behavior understanding. In: IEEE inter-

615\(7953\): 620–627. 

national conference on robotics and automation \(ICRA\), 

20

The International Journal of Robotics Research 0\(0\)

London, UK, 29 May 2023–2 June 2023. IEEE, 

Shao H, Wang L, Chen R, et al. \(2023\) Safety-enhanced auton-3532–3538. 

omous driving using interpretable sensor fusion transformer. 

Malikopoulos AA, Cassandras CG and Zhang YJ \(2018\) A de-In: Conference on robot learning, Atlanta, GA, 6 November centralized energy-optimal control framework for connected 2023, 726–737. PMLR. 

automated vehicles at signal-free intersections. Automatica Sharon G and Stone P \(2017\) A protocol for mixed autonomous 93: 244–256. 

and human-operated vehicles at intersections. In: Interna-Mavrogiannis C, DeCastro JA and Srinivasa SS \(2023\) Ab-

tional conference on autonomous agents and multiagent

stracting road traffic via topological braids: applications to systems, São Paulo, Brazil, 8–12 May 2017, pp. 151–167. 

traffic flow analysis and distributed control. The International Spatharis C and Blekas K \(2024\) Multiagent reinforcement Journal of Robotics Research 43\(9\): 1299–1321. 

learning for autonomous driving in traffic zones with un-Miculescu D and Karaman S \(2019\) Polling-systems-based au-signalized intersections. Journal of Intelligent Transportation tonomous vehicle coordination in traffic intersections with no Systems 28\(1\): 103–119. 

traffic signals. IEEE Transactions on Automatic Control Spielberg NA, Brown M, Kapania NR, et al. \(2019\) Neural net-65\(2\): 680–694. 

work vehicle models for high-performance automated driv-Mirheli A, Tajalli M, Hajibabai L, et al. \(2019\) A consensus-based ing. Science Robotics 4\(28\): eaaw1975. 

distributed trajectory control in a signal-free intersection. 

Timothy O and Marzenna C \(2005\) Calibration and validation of a Transportation Research Part C: Emerging Technologies

micro-simulation model in network analysis. In: Presentation at 100: 161–176. 

the TRB annual meeting and included in the compendium of Mnih V, Kavukcuoglu K, Silver D, et al. \(2015\) Human-level papers CD-ROM, 05-1938, Washington, DC, January 2005. 

control

through

deep

reinforcement

learning. 

Nature

Treiber M, Hennecke A and Helbing D \(2000\) Congested traffic 518\(7540\): 529–533. 

states in empirical observations and microscopic simulations. 

Mohamed NE and Radwan II \(2022\) Traffic light control design Physical Review 62\(2\): 1805–1824. 

approaches: a systematic literature review. International Urmson C and Whittaker W \(2008\) Self-driving cars and the urban Journal of Electrical and Computer Engineering 12\(5\):

challenge. IEEE Intelligent Systems 23\(2\): 66–68. 

5355–8708. 

Vegni AM and Little TD \(2010\) A message propagation model for Muhammad K, Ullah A, Lloret J, et al. \(2020\) Deep learning for hybrid vehicular communication protocols. In: 2010 7th in-safe autonomous driving: current challenges and future di-ternational symposium on communication systems, networks rections. IEEE Transactions on Intelligent Transportation

& digital signal processing \(CSNDSP 2010\), Newcastle upon Systems 22\(7\): 4316–4336. 

Tyne, UK, 21–23 July 2010, 382–386. IEEE. 

Pek C, Manzinger S, Koschi M, et al. \(2020\) Using online veri-Villarreal M, Poudel B, Pan J, et al. \(2024\) Mixed traffic control fication to prevent autonomous vehicles from causing acci-and coordination from pixels. In: 2024 IEEE international dents. Nature Machine Intelligence 2\(9\): 518–528. 

conference on robotics and automation \(ICRA\), Yokohama, Poudel B, Li W and Heaslip K \(2024\) Endurl: enhancing safety, Japan, 13–17 May 2024, pp. 4488–4494. DOI: 10.1109/

stability, and efficiency of mixed traffic under real-world

ICRA57147.2024.10610517. 

perturbations via reinforcement learning. In: 2024 IEEE/

Vinitsky E, Parvate K, Kreidieh A, et al. \(2018\) Lagrangian control RSJ international conference on intelligent robots and sys-through deep-rl: applications to bottleneck decongestion. In: tems \(IROS\), Abu Dhabi, UAE, 14–18 October 2024. 

IEEE international conference on intelligent transportation Press A \(2022\) Power still out to 50k customers, days after systems, Edmonton, AB, 24–27 September 2024, pp. 759–765. 

memphis storm. https://www.usnews.com/news/best-states/

Wang J, Zheng Y, Xu Q, et al. \(2019\) Controllability analysis and

tennessee/articles/2022-02-07/power-still-out-to-60k-

optimal controller synthesis of mixed traffic systems. In:

customers-days-after-memphis-storm

IEEE intelligent vehicles symposium \(IV\), Paris, France, 9–

Ramirez R \(2022\) Power outages are on the rise, led by Texas, 12 June 2019. IEEE, 1041–1047. 

Michigan and California. here’s what’s to blame. https://

Wang D, Li W and Pan J \(2023a\) Large-scale mixed traffic control

www.cnn.com/2022/09/14/us/power-outages-rising-

using dynamic vehicle routing and privacy-preserving crowd-

extreme-weather-climate/index.html

sourcing. IEEE Internet of Things Journal 11\(2\): 1981–1989. 

Rios-Torres J and Malikopoulos AA \(2016\) A survey on the Wang S, Shang M, Levin MW, et al. \(2023b\) A general approach to coordination of connected and automated vehicles at inter-smoothing nonlinear mixed traffic via control of autonomous sections and merging at highway on-ramps. IEEE Transac-vehicles. Transportation Research Part C: Emerging Tech-tions

on

Intelligent

Transportation

Systems

18\(5\):

nologies 146: 103967. 

1066–1077. 

Wei H, Zheng G, Gayah V, et al. \(2019\) A survey on traffic signal Schrank D, Eisele B, Lomax T, et al. \(2021\) Urban Mobility control methods. ArXiv preprint arXiv:1904.08117. 

Scorecard. College Station, TX: Texas A&M Transportation Winck B \(2022\) Get ready for blackouts from london to la, as the Institute and INRIX. 

global energy crisis overwhelms grids and sends energy

Schulman J, Wolski F, Dhariwal P, et al. \(2017\) Proximal prices skyrocketing. https://www.businessinsider.com/

policy optimization algorithms. ArXiv preprint arXiv:

global-europe-energy-crisis-power-electricity-outages-

1707.06347. 

blackouts-energy-grid-2022-9?op=1

Wang et al. 

21

Wu C, Bayen AM and Mehta A \(2018\) Stabilizing traffic with IEEE Transactions on Automation Science and Engineering autonomous vehicles. In: IEEE international conference on 20\(2\): 789–804. 

robotics and automation \(ICRA\), Brisbane, QLD, 21–25 May Yang H and Oguchi K \(2020\) Intelligent vehicle control at signal-2018, 6012–6018. IEEE. 

free intersection under mixed connected environment. IET

Wu C, Kreidieh AR, Parvate K, et al. \(2022\) Flow: a modular Intelligent Transport Systems 14\(2\): 82–90. 

learning framework for mixed autonomy traffic. IEEE

Zhang R, Ishikawa A, Wang W, et al. \(2020\) Using reinforcement Transactions on Robotics 38\(2\): 1270–1286. 

learning with partial vehicle detection for intelligent traffic Wu X, Wei Y and Zou L \(2023\) Optimizing cooperative con-signal control. IEEE Transactions on Intelligent Trans-

trol algorithms for vehicles and roads at unsignalized in-portation Systems 22\(1\): 404–415. 

tersections considering communication performance. In:

Zhang Y, Macke W, Cui J, et al. \(2023\) Learning a robust mul-International conference on robotics, intelligent control tiagent driving policy for traffic congestion reduction. Neural and artificial intelligence \(RICAI\), Zhangjiajie, China, 24–

Computing & Applications, Special Issue on Adaptive and 26 November 2023. IEEE, 423–428. 

Learning Agents 2022 1–14. 

Xu Y, Zhou H, Ma T, et al. \(2021\) Leveraging multiagent learning Zhao L, Malikopoulos A and Rios-Torres J \(2018\) Optimal control for automated vehicles scheduling at nonsignalized intersec-of connected and automated vehicles at roundabouts: an

tions. IEEE Internet of Things Journal 8\(14\): 11427–11439. 

investigation in a mixed-traffic environment. IFAC-Paper-Yan Z and Wu C \(2021\) Reinforcement learning for mixed au-sOnLine 51\(9\): 73–78. 

tonomy intersections. In: IEEE international intelligent Zheng J, Zhu K and Wang R \(2022\) Deep reinforcement learning transportation systems conference, Indianapolis, IN, 19–22

for autonomous vehicles collaboration at unsignalized in-September 2021, pp. 2089–2094. 

tersections. In: IEEE global communications conference

Yan S, Welschehold T, Büscher D, et al. \(2021\) Courteous behavior \(GLOBECOM\), Rio de Janeiro, Brazil, 4–8 December 2022, 

of automated vehicles at unsignalized intersections via re-pp. 1115–1120. 

inforcement learning. IEEE Robotics and Automation Letters Zhou A, Peeta S, Yang M, et al. \(2022\) Cooperative signal-free 7\(1\): 191–198. 

intersection control using virtual platooning and traffic flow Yan Z, Kreidieh AR, Vinitsky E, et al. \(2022\) Unified automatic regulation. Transportation Research Part C: Emerging

control of vehicular systems with reinforcement learning. 

Technologies 138: 103610. 


# Document Outline

+ Learning to control and coordinate mixed traffic through robot vehicles at complex and unsignalized intersections  
	+ 1. Introduction 
	+ 2. Related work  
		+ 2.1. Unsignalized intersection control 
		+ 2.2. Mixed traffic control 

	+ 3. Methodology  
		+ 3.1. Intersection traffic 
		+ 3.2. Decentralized RL for mixed traffic  
			+ 3.2.1. Action space 
			+ 3.2.2. Observation space 
			+ 3.2.3. Traffic condition estimation 
			+ 3.2.4. Conflict-aware reward 
			+ 3.2.5. RL algorithm 

		+ 3.3. Conflict resolution mechanism 
		+ 3.4. Assumptions of robot vehicles 

	+ 4. Experiments and results  
		+ 4.1. Mixed traffic  
			+ 4.1.1. Reconstruction and simulation 
			+ 4.1.2. Mixed traffic generation 

		+ 4.2. Experiment set-up 
		+ 4.3. Overall performance 
		+ 4.4. Individual intersection performance 
		+ 4.5. Blackout 
		+ 4.6. Traffic demands and congestion 
		+ 4.7. Generalization 
		+ 4.8. Evaluation of reward function 
		+ 4.9. Evaluation of conflict resolution 
		+ 4.10. Robustness in potential real-world deployment 
		+ 4.11. Extension to right-turn traffic 

	+ 5. Discussion 
	+ 6. Conclusion 
	+ Declaration of conflicting interests 
	+ Funding 
	+ ORCID iD 
	+ Notes 
	+ References



