Transportation Research Part C 150 \(2023\) 104109

Contents lists available at ScienceDirect

Transportation Research Part C

journal homepage: www.elsevier.com/locate/trc

Hierarchical and game-theoretic decision-making for connected and

automated vehicles in overtaking scenarios

Kyoungtae Ji a, Nan Li b, Matko Orsag c, Kyoungseok Han a, ∗

a *Department of Mechanical Engineering, Kyungpook National University, Daegu, 41566, South Korea* b *Department of Aerospace Engineering at Auburn University, AL, 36849, USA*

c *Department of Control and Computer Engineering, University of Zagreb, Zagreb, 10000, Croatia* A R T I C L E

I N F O

A B S T R A C T

*Keywords:*

This paper presents a hierarchical and game-theoretic decision-making strategy for connected Connected and automated vehicles

and automated vehicles \(CAVs\). A CAV can receive preview information using vehicle-to-

Game theory

everything \(V2X\) communication systems, and the optimal short- and long-term trajectory can Leader–follower game

be planned using this information. Specifically, in this study, the aggressiveness of all preceding Autonomous driving

vehicles in the car-following scenario can be estimated globally by monitoring the history of their time-series behaviors, before the CAV initiates a particular action, which is performed at the upper layer of the proposed decision-making structure. If it is determined that initiating a specific action is advantageous, the action is initiated, and the CAV then interacts with the vehicles locally to achieve its driving goal in a game-theoretical manner at the lower layer. 

In multiple test scenarios, we demonstrate the usefulness of our approach compared to the conventional decision-making approaches, and it shows a significant improvement in terms of success rates. 

**1. Introduction**

With the increasing penetration of autonomous vehicles \(AVs\), it is expected that AVs will share the road with human-driven vehicles \(HVs\) soon, and their interactions must be considered when making decisions \(Di and Shi, 2021, Yurtsever et al. , 2020\). 

Serious efforts have been pursued to describe the direct interaction between vehicles \(Sankar and Han, 2020; Li et al. , 2020; Sadigh

et al., 2016\), but relatively little attention has been paid to exploiting preview information when making decisions. Here, a preview information is the long-sighted upcoming traffic information, which is not available from the equipped sensors such as camera, lidar, and radar. In general, the Vehicle-to-Everything \(V2X\) technology is employed to get the preview information. For example, in road conditions where multiple choices of maneuvers are available, limited preview information of HVs can lead to ineffective results \(Yan and Radwan, 2007\), but AVs that take advantage of V2X communication to obtain rich preview information can make different decisions, resulting in efficient driving. 

In this paper, we focus on developing a decision-making strategy for AVs in overtaking scenario, which consists of the following three steps \(Petrov and Nashashibi, 2014\): \(1\) Initiating the overtaking through a lane change, \(2\) accelerating until the vehicle arrives at the target vehicle’s position, and \(3\) passing the target vehicle and returning to the original lane. However, because a human driver only has a limited amount of traffic information before starting the overtaking maneuver, the benefit of overtaking in a particular road condition is unclear, and it can sometimes lead to the vehicle being in a worse condition \(e.g., stuck in the traffic\). 

∗ Corresponding author. 

*E-mail address: *kyoungsh@knu.ac.kr \(K. Han\). 

https://doi.org/10.1016/j.trc.2023.104109

Received 21 July 2022; Received in revised form 11 March 2023; Accepted 15 March 2023

Available online 23 March 2023

0968-090X/© 2023 Elsevier Ltd. All rights reserved. 

*K. Ji et al. *

*Transportation Research Part C 150 \(2023\) 104109*

To address the aforementioned issue, we use connected and automated vehicle \(CAV\) technology \[e.g., V2X\] that provides long-term preview information such as traffic volume, road configuration, and trajectories history of the vehicles ahead. Using this information, an improvement in driving safety and efficiency can be achieved \(Xie and Liu, 2022; Vahidi and Sciarretta, 2018\). The decision-making in overtaking scenarios has been treated in Wang et al. \(2021\), Li et al. \(2019\), but only the interactions between directly adjacent vehicles were considered. With this in mind, we propose a hierarchical decision-making strategy in which the upper layer uses CAV technology for coarsely predicting the behaviors of vehicles far away, and the lower layer provides the appropriate action candidate to the CAV based on a game-theoretic strategy. 

Game theory provides a promising approach to modeling the interaction between agents. The basic assumption of game theory is that *all game participants are rational decision-makers who want to maximize their rewards *\(Myerson, 2013\), which means that all interactive agents’ behaviors can be interpreted as if they are participating in a strategic game. 

The decision-making process of human driver was modeled in a simulated driving environment using the level-k framework in Li et al. \(2017\), which is one representative game theory-inspired modeling method that considers the game participant’s depth of thought Backhaus et al. \(2013\). However, because this approach must model the depth of thoughts for all interactive vehicles, the high computational burden is unavoidable \(Tian et al., 2020\). As a result, significant improvements in computation should be further investigated. 

In this paper, we employ a leader–follower game approach which is partly inspired by Stackelberg game to model the interaction of vehicles \(Başar and Olsder, 1998\). The main idea behind this approach is that those game participants are assumed to be hierarchical decision-makers who successively make decisions. In Yu et al. \(2018\), Zhang et al. \(2019\), Yoo and Langari \(2020\), the lane-changing and lane-merging scenarios are modeled based on the Stackelberg game, and the vehicle interaction and decision-making strategy in unsignalized intersection are studied in Li et al. \(2020\), and show the feasibility of the leader–follower game approach in the decision-making of the AV. 

Beyond the leader–follower game approach, we propose a driver aggressiveness estimation method that builds up the estimation result over two layers in our decision-making structure. In this study, ‘‘aggressiveness’’ is defined according to a driver’s preferred behavior without accounting for the other interactive traffic participants \(e.g., desired speed, and headway\) \(Kaysi and Abbany, 

2007\). In most of previous studies, driver aggressiveness is estimated using offline data-driven techniques or drivers’ self-evaluation \(Wang et al. , 2020; Jovanović et al., 2011\), and only a few works estimate real-time aggressiveness for AVs’ use \(Yu

et al. , 2018; Zhang et al., 2019\). However, this real-time aggressiveness estimation algorithm is limited to the direct interacting situations. That is, the response of the potential interactive vehicle cannot be predicted beforehand. In this study, we broaden the range of aggressiveness estimation using V2X information. For example, by accessing the trajectories history of the vehicles ahead, a CAV can globally estimate the potential interactive vehicles’ aggressiveness before interacting with it, then the estimated value is refined during the real local interaction. Specifically, in a car-following scenario, CAV determines whether or not to overtake by monitoring the vehicles ahead, and initiates overtaking if overtaking is determined to be a beneficial decision in a specific condition. 

Once the CAV reaches the position of the target vehicle, an appropriate decision is made in real-time based on the leader–follower game approach to return to the original lane. We have decided to focus on overtaking scenario because overtaking is the most appropriate scenario to show the effectiveness of our approach, where the global aggressive estimation via V2X technology and local interaction should be considered together. 

As compared to the existing studies, our approach has the following distinguishing features: \(1\) We propose a hierarchical and game-theoretic decision-making approach for CAVs in overtaking scenarios taking advantage of the V2X communication system, which has recently become available in the CAV. Specifically, the future trajectory of the CAV

is first globally planned based on the coarsely estimated aggressiveness of potential target preceding vehicles at the upper layer, and the globally estimated aggressiveness is locally refined when the CAV interacts with a specific target vehicle at the lower layer. 

Moreover, in the considered overtaking scenario, our approach enables the CAV to choose to stay in its lane \(i.e, not initiate an overtaking\) when overtaking is expected to be dangerous or beneficial based on the globally estimated aggressiveness of the vehicles ahead. Such a hierarchical decision-making structure is new to the best of the authors’ knowledge is novel/new. 

\(2\) Globally and locally, the aggressiveness of possible interactive vehicles is estimated. The proposed modified car-following model, which assumes a correlation between driver’s aggressiveness and the vehicle time headway, can predict how preceding vehicles will behave based on their past actions and globally estimated their aggressiveness. The effectiveness of the proposed global aggressiveness estimation approach and the correlation between the estimated aggressiveness and the time headway are verified by utilizing the asset of publicly available traffic data set collected at US highways. Also, the coarsely estimated aggressiveness is locally updated during the actual vehicle interaction, and on the basis of this, the game-theoretic decision for lane changing is determined. 

This sequential decision-making demonstrates effectiveness compared to the conventional approaches in terms of driving safety and efficiency. 

\(3\) We demonstrate the effectiveness of our approach in various car-following situations. To confirm the robustness of the proposed method, we run the simulations 10,000 times in three different simulation environments. In terms of success rate, the proposed method consistently outperforms the traditional methods. In addition, the underlying assumption of the proposed car-following model is supported through the verification based on real traffic dataset, which is the basis for the proposed game-theoretic decision-making strategy. 

The rest of the paper is organized as follows. In Section 2, the treated problem, vehicle model, and simulated traffic environment are introduced. The global and local aggressiveness estimation algorithms are presented in Section 3, the hierarchical decision-making strategy is given in Section 4. The simulation-based verification results are shown in Section 5, and the paper is concluded in Section 6. 

2



*K. Ji et al. *

*Transportation Research Part C 150 \(2023\) 104109*

**Fig. 1. **\(a\) Driving scenario in which the red car is lack of preview information, \(b\) overtaking success before the red car reaches the end of the left lane, \(c\) overtaking failure due to insufficient space to change lanes. 

**2. Problem formulation**

In this paper, we address the decision-making problem of CAV in complex traffic situations in which the benefit of carrying out a specific action sequence is not clear a priori. Assume, e.g., that a large commercial bus is in front of the ego vehicle, blocking the ego vehicle’s view, as shown in Fig. 1\(a\). In such a case, traffic conditions \(e.g., traffic volume, road configuration and construction, etc.\) that the ego vehicle may face soon are unknown to the ego vehicle. 

If a human driver encounters situation in Fig. 1\(a\), he/she must decide whether or not to overtake the large bus. Although the human driver can be informed about the existence of the construction site by message signs or lane marking, there is the possibility of misjudging due to the human driver’s inappropriate aggressiveness or lack of the preview information such as the traffic stream ahead. With insufficient preview information, the human driver may sometimes succeed in overtaking the large bus by returning into its original lane before reaching the construction site, as shown in Fig. 1\(b\). However, if the preceding vehicle does not yield to the ego vehicle \(i.e., does not allow it to cut in front\), it is likely that the ego vehicle will get stuck in the left lane for a while. 

In general, the aggressiveness of the bus driver can be used when making the decision. For example, it is expected that a cautious driver typically prefers a large time headway to maintain a safe distance from the front car. An aggressive driver, on the other hand, may tries to keep as close to the front car as possible. Unfortunately, the aggressiveness of the vehicles is not given beforehand and hard to be identified due to its driver-to-driver/situation-to-situation heterogeneity. 

To overcome these problems, this paper considers the global and local interactions hierarchically. V2X communication can provide global preview information that coarsely predicts the potential interactive vehicle behaviors. Using this, the CAV determines whether or not to initiate the overtaking maneuver. Once an overtaking is initiated and CAV reaches the interactive vehicle that is likely to yield, a finer decision \(e.g., whether or not, and how, to return to its original lane\) is made based on local interaction and a game-theoretic strategy. Meanwhile, the aggressiveness estimate of the interactive vehicle is refined during the local interaction, based on which the ego vehicle decides whether to return to its original lane now or to find another vehicle to interact with. 

*2.1. Vehicle kinematic model*

In this study, the following discrete-time point-mass model is used to represent vehicle kinematics \(Han et al., 2020\). 

*𝑥𝑡*\+1 = *𝑥𝑡 *\+ *𝑣𝑡 𝛥𝑡 *\+ 0 *. * 5 *𝑎𝑡 𝛥𝑡* 2 *, *

*𝑥*

*𝑥*

*𝑣𝑡*\+1 = *𝑣𝑡 *\+ *𝑎𝑡 𝛥𝑡, *

\(1\)

*𝑥*

*𝑥*

*𝑥*

*𝑦𝑡*\+1 = *𝑦𝑡 *\+ *𝑣𝑡 𝛥𝑡. *

*𝑦*

where *𝑥 * is longitudinal position, *𝑣𝑥 * is longitudinal velocity, and *𝑎𝑥 * is longitudinal acceleration; the lateral position and velocity are represented by *𝑦 * and *𝑣𝑦*, respectively, and the vehicle positions *𝑥 * and *𝑦 * are at the vehicle’s center of gravity. The superscript *𝑡*

denotes the time instant, and *𝛥𝑡 *= 0 *. * 5 s is the sampling time period, *𝑢 *= \[ *𝑎𝑥, 𝑣𝑦*\] *⊤ * is the control input. 

*2.2. Action set*

This study assumes that the vehicles can take the following discrete actions \(Garzón and Spalanzani, 2019; Li et al., 2017\): 1. *𝜅𝑚 *: Maintaining speed

2. *𝜅𝑎 *: Acceleration at *𝑎𝑥 *= 1 *. * 25 m/s2

3. *𝜅𝑑 *: Deceleration at *𝑎𝑥 *= −1 m/s2

3



*K. Ji et al. *

*Transportation Research Part C 150 \(2023\) 104109*

**Fig. 2. **Comparison of the observation spaces \(a\) when the CAV can receive the V2X information, and \(b\) when the HV has a narrow field of view. 

4. *𝜅ℎ𝑎 *: Hard acceleration at *𝑎𝑥 *= 2 *. * 5 m/s2

5. *𝜅ℎ𝑑 *: Hard deceleration at *𝑎𝑥 *= −2 m/s2

6. *𝜅𝑐𝑙 *: Lateral motion to left at *𝑣𝑦 *= 2 m/s

7. *𝜅𝑐𝑟 *: Lateral motion to right at *𝑣𝑦 *= −2 m/s

The actions from \(1\) to \(5\) are related to vehicle longitudinal motion where the vehicle speed is limited by *𝑣* max = 30 m∕s, and the actions in \(6\) and \(7\) change the vehicle lateral position, assuming with constant longitudinal vehicle speed. These seven actions can model the common behaviors of a vehicle on a highway. Now, the action set that includes all possible actions is as follows: *𝛤𝑖 *= \{ *𝜅𝑚, 𝜅𝑎, 𝜅𝑑 , 𝜅ℎ𝑎, 𝜅ℎ𝑑 , 𝜅𝑐𝑙, 𝜅𝑐𝑟*\} *, *

*𝑖 *∈ \{ *𝑙, 𝑓 *\} *, *

\(2\)

where *𝛤𝑙 * and *𝛤𝑓 * denote the action set of the leader and follower, respectively, in the leader–follower game setting, which will be discussed in the following sections. Note that from the real-vehicle standpoint, the decision-making and upper-level controller determine the rough action sequence, and the lower-level controller is used to track the control commands from the upper-level controller. Therefore, only the upper-level control is considered in this study. It should be noted that more precise movements of the vehicle cannot be realized by our approach, but to design the scalable interaction-aware decision-making approach we assume the discrete action and the accurate vehicle kinematics/dynamics are not considered. 

*2.3. Observation space*

In this subsection, we compare the observation spaces between CAV and HV, and discuss how this distinction helps CAV making better decisions. 

A CAV receives useful long-range preview information, such as road conditions and traffic volume, based on V2X communication, as illustrated in Fig. 2\(a\), thereby being able to leverage this information to improve its driving safety and efficiency. For example, in Fig. 2\(a\), CAV is not likely to overtake the commercial bus even though the bus drives slowly since CAV knows in advance that the left lane will close soon. In contrast, HV only uses short-term information when planning its near-future trajectory, so HV may decide to overtake the large bus trying to reduce the trip time in the situation depicted in Fig. 2\(b\). However, it is expected that this overtaking decision eventually causes the HV to get stuck in front of the construction place, leading to an increase in the trip time. In this paper, we assume that the ego vehicle is a CAV that can access the state of other vehicles in real-time by exploiting the V2X information, while others are HVs that lack the ability to receive information from other vehicles. Therefore, the speeds and positions of HVs are known to the ego vehicle. 

*2.4. Simulated traffic environment*

We model HVs in car-following scenarios in this subsection. With some modifications, the widely accepted collision-free car-following model, i.e., intelligent driver model \(IDM\), is used \(Treiber et al. , 2000; Bae et al. , 2020; Liu et al. , 2022\):

\{

\( \)

\}

*𝛿*

\(

\)2

*𝑑𝑣*

*𝑣*

*𝑠*∗\( *𝑣, *△ *𝑣, 𝜇*\)

*̇𝑣 *=

= *𝑎*

1 −

−

*, *

\(3\)

*𝑑𝑡*

*𝑣* 0

*𝑠*

where *𝑎 * is the maximum acceleration, *𝑣 * is the vehicle speed, *𝑣* 0 is the desired speed, *𝛿 * is the acceleration exponent, *𝑠 *= *𝑥𝑖*−1 − *𝑥𝑖 *− *𝑙*

is the net distance, where *𝑖 *− 1 refers to the vehicle directly in front of *𝑖* th vehicle and *𝑙 * is the vehicle length, △ *𝑣 *= *𝑣𝑖 *− *𝑣𝑖*−1 is velocity difference with the preceding vehicle, *𝜇 * is the driver’s aggressiveness, and *𝑠*∗ is the desired net distance. 

The desired net distance *𝑠*∗ is defined as

*𝑣 *△ *𝑣*

*𝑠*∗\( *𝑣, *△ *𝑣, 𝜇*\) = *𝑠* 0 \+ *𝑣𝑇 *\( *𝜇*\) \+ √

*, *

\(4\)

2

*𝑎𝑏*

where *𝑠* 0 is a minimum desired gap between vehicles, *𝑏 * is the desired comfort deceleration, and *𝑇 *\( *𝜇*\) is the time headway. 

4

*K. Ji et al. *

*Transportation Research Part C 150 \(2023\) 104109*

**Table 1**

Parameter values for the IDM. 

Parameters

Values

Target speed, *𝑣*

25 m∕s

0

Maximum acceleration, *𝑎*

3.6 m∕s2

Desired deceleration, *𝑏*

1.67 m∕s2

Acceleration exponent, *𝛿*

4

Jam distance, *𝑠*

2 m

0

**Fig. 3. **\(a\) Speed profiles of the vehicles modeled by conventional intelligent driver model \(IDM, i.e., time headway is constant\), \(b\) speed profiles of the vehicles modeled by modified IDM \(i.e, time headway is a function of aggressiveness\). 

For explanation, we define the augmented state *𝑧𝑖 *= \[ *𝑥𝑖, 𝑣𝑖*\] that is consisted of the position and speed of *𝑖* th vehicle, and the proposed IDM is expressed as follows. 

*̇𝑣𝑖 *= *𝑓* IDM\( *𝑧𝑖*−1 *, 𝑧𝑖, 𝜇𝑖*\) *. *

\(5\)

where subscript *𝑖 *− 1 indicates the \( *𝑖 *− 1\)th vehicle in front of the *𝑖* th vehicle, and *𝜇𝑖 * is the aggressiveness of the *𝑖* th vehicle. 

Given the augmented states of the *𝑖* th and its preceding vehicles, as well as the *𝑖* th driver’s aggressiveness, the *𝑖* th vehicle’s behavior in the car-following scenario can now be described using \(5\). 

In this study, the time headway *𝑇 *\( *𝜇*\) is assumed to be a function of the driver’s aggressiveness *𝜇 *∈ \[0 *, * 1\]. For instance, on the one hand, if *𝜇 * is close to 1, such an aggressive driver may prefer to reduce the distance gap with the preceding car. A cautious driver characterized by a small *𝜇*, on the other hand, exhibits different behavior, i.e., increasing the headway. Keeping this in mind, we will use the linear time headway model as shown below:

*𝑇 *\( *𝜇*\) = *𝑇* min \+ *𝑇* 0\(1 − *𝜇*\) *. *

\(6\)

where *𝑇* min = 1 s is the minimum time headway to keep the minimum safe distance, and *𝑇* 0 = 1 *. * 5 s is an adjustable parameter that determines the gradient of the linear time headway model, which gives the reasonable time headway on the highway \(i.e., *𝑇 *\( *𝜇*\) ∈ \[1 *, * 2 *. * 5\]\). Here, we assume the driver aggressiveness depends on time headway, and the other parameters are assumed to be fixed. It is because, in dense traffic, driver behavior most depends on desired headway, and the other parameter such as the desired velocity is dependent on the traffic stream \(Ayres et al., 2001\). The verification of this assumption is performed in Section 5.1. 

The remaining IDM parameters are described in Table 1, which have been calibrated to the collision-free car-following scenarios \(Hyeon et al. , 2019\). Although IDM provides rational vehicle behaviors in the car-following scenario, the heterogeneity in human drivers’ behaviors must be considered. Thus, in this study, the aggressiveness *𝜇 * is reflected in the time headway, influencing the desired net distance *𝑠*∗ in \(4\). 

To demonstrate the modified IDM, we compare the speed profiles of the vehicles that follow the leading car, as shown in Fig. 3. 

In this case, the speed profile of the leading car is the US06 driving cycle, and the rest of the vehicles follow the leading car in a row. 

In Fig. 3\(a\), the following vehicles are modeled by conventional IDM \(i.e., time headway is constant\), resulting in similar shapes of the speed profiles to maintain the same desired gap between vehicles, which is not true in reality. In contrast, Fig. 3\(b\) depicts the heterogeneity of human drivers using the proposed linear time headway model. The differences are highlighted in the magnified plots in Figs. 3\(a\) and \(b\). The significant difference in speed deviation demonstrates the difference in driving patterns of the vehicles in the second case \(i.e., when the vehicles are modeled by our proposed modified IDM\). 

In the conventional IDM, the ego vehicle follows a fixed leader, i.e., does not take into account the interaction with vehicles in other lanes. In reality, when there is a vehicle in an adjacent lane pursuing cutting in front of it, the ego vehicle needs to select 5

*K. Ji et al. *

*Transportation Research Part C 150 \(2023\) 104109*

**Algorithm 1: **Global Aggressiveness Estimation and Vehicle Trajectory Prediction **1 **Input  −, 

**2 for ** *𝑖 *∈  **do**

**3**

**for ** *𝑘 *∈ *𝑡 *− *𝑁𝑙 *\+ 1 ∶ *𝑡 ***do**

**4**

*̂*

*𝜇𝑘 *← *𝑓 *−1 \( *𝑧𝑘 , 𝑧𝑘, ̇𝑣𝑘*\)

*𝑖*

IDM

*𝑖*−1

*𝑖*

*𝑖*

**5**

**end**

\(|

\(

\) \)

|

|

1

∑ *𝑡*

|

**6**

*̄*

*𝜇𝑡 *← argmin

*𝜇𝑣 *−

⋅

*̂*

*𝜇𝑘*

*𝑖*

|

*𝑁*

*𝑘*= *𝑡*− *𝑁*

*𝑖*

|

*𝜇𝑣*∈ *𝑀 𝑣*

|

*𝑙*

*𝑙 *\+1

|

**7**

 *𝑡 *← \[ *𝑡, ̄𝜇𝑡*\]

*𝑖*

**8 end**

**9 for ** *𝑘 *∈ *𝑡 *∶ *𝑡 *\+ *𝑁𝑝 *− 1 **do**

**10**

**for ** *𝑖 *∈  **do**

**11**

*̇𝑣𝑘 *← *𝑓*

*, 𝑧𝑘, ̄*

*𝜇𝑡*\)

*𝑖*

IDM\( *𝑧𝑘*

*𝑖*−1

*𝑖*

*𝑖*

**12**

 *𝑘*\+1 ← \[ *𝑘*\+1 *, 𝑓*\(1\)\( *𝑧𝑘, ̇𝑣𝑘*\)\]

*𝑖*

*𝑖*

**13**

**end**

**14**

\+ ← \[\+ *, * *𝑘*\+1\]

**15 end**

**16 **Output  \+ *, * *𝑡*

between its original leader \(i.e., ignoring the cutting-in vehicle\) and the cutting-in vehicle \(i.e., yielding to the cutting-in vehicle\) as its new leader. We now propose a model that represents a strategy for the ego vehicle to select its leader depending on the ego driver’s aggressiveness:

*̇𝑣𝑖 *= *𝜇𝑖 *⋅ *𝑓* IDM\( *𝑧𝑖*−1 *, 𝑧𝑖, 𝜇𝑖*\) \+ \(1 − *𝜇𝑖*\) ⋅ *𝑓* IDM\( *𝑧* cav *, 𝑧𝑖, 𝜇𝑖*\) *. *

\(7\)

where *̇𝑣𝑖 * is *𝑖* th vehicle’s acceleration, *𝜇𝑖 * is *𝑖* th vehicle’s aggressiveness, and *𝑧* cav denotes the state of the vehicle pursuing cutting-in, i.e., the ego CAV in our setting. 

When CAV arrives near the *𝑖* th vehicle and shows the lane-change signal to the *𝑖* th vehicle, *𝑖* th vehicle’s behavior is determined depending on its aggressiveness. For example, an aggressive driver \(i.e, *𝜇𝑖 *≈ 1\) keeps following its original leader \(i.e., \( *𝑖 *− 1\)th vehicle\) while ignoring the lane-change signal of CAV. In contrast, a cautious driver \(i.e, *𝜇𝑖 *≈ 0\) is likely to yield to the CAV and, thus, treats the CAV as its new leader according to \(7\). When the aggressiveness is between 0 and 1, then *𝑖* th vehicle accounts for both CAV and \( *𝑖 *− 1\)th vehicle, and its acceleration is determined as a linear combination of acceleration values for following each of them weighted by its aggressiveness. 

The above model will be further verified using the real driving dataset in Section 3.1. 

**3. Drivers’ aggressiveness estimation**

In previous sections, we defined ‘‘aggressiveness’’ and related it to time headway in car-following scenarios. In this section, we propose a hierarchical strategy for estimating the aggressiveness of a driver. 

Since CAV can receive the driving information of the vehicles far away, it can coarsely estimate their aggressiveness based on their historical trajectories, this procedure is referred to as the global aggressiveness estimation in this study. When the CAV arrives at the vicinity of an interactive vehicle, the aggressiveness estimate of the interactive vehicle is locally refined by monitoring the interactive vehicle’s reaction to the CAV’s action, which is referred to as the local aggressiveness estimation in this study. 

*3.1. Global aggressiveness estimation*

The global aggressiveness estimation strategy is proposed in this subsection under the assumption that CAV can monitor the behaviors of distant vehicles in real-time through V2V/V2X technology. 

Using the modified IDM, the acceleration at time instant *𝑡 * is as follows. 

*𝑎𝑡 *= *̇𝑣𝑡 *= *𝑓*

*, 𝑧𝑡, 𝜇*

*𝑖*

*𝑖*

IDM\( *𝑧𝑡𝑖*−1

*𝑖*

*𝑖*\) *. *

\(8\)

We can extract the driver’s aggressiveness at time instant *𝑡 * from \(8\), and explicitly express the aggressiveness by taking the inverse of the model \(Zhang et al., 2019\):

*̂*

*𝜇𝑡 *= *𝑓 *−1 \( *𝑧𝑡*

*, 𝑧𝑡, ̇𝑣𝑡*\) *. *

\(9\)

*𝑖*

IDM

*𝑖*−1

*𝑖*

*𝑖*

The procedure of the global aggressiveness estimation is described in Algorithm 1 where the inputs are the traffic state tuple history from *𝑁𝑙 * steps ago to the current time instant *𝑡*, 

− = \[ *𝑡*− *𝑁𝑙*\+1 *, * *𝑡*− *𝑁𝑙*\+2 *, *… *, * *𝑡*\] *. *

\(10\)

6

*K. Ji et al. *

*Transportation Research Part C 150 \(2023\) 104109*

**Fig. 4. **Comparison of root-mean-square error \(RMSE\) of position and velocity predictions between our approach and conventional approaches. 

and indices of preceding vehicles  = \[1 *, * 2 *, *… *, 𝑛*\] \(Line 1\), where index 1 denotes the farthest vehicle that CAV can monitor, index *𝑛 * denotes the last vehicle modeled by the IDM \(i.e., the immediate preceding vehicle of CAV\),  *𝑡 *= \[ *𝑧𝑡 , 𝑧𝑡 , *… *, 𝑧𝑡 *\] denotes the states 1

2

*𝑛*

of all preceding vehicles, and *𝑁𝑙 * is the look-back horizon, which means the length of the time history \(Han et al.\). 

Using inverse IDM, the aggressiveness at each instant from time step *𝑡 *− *𝑁𝑙 *\+ 1 to *𝑡 * can be computed \(Line 4\), and these computations are used to determine the estimate of aggressiveness at the current moment *𝑡*, i.e., *̄*

*𝜇𝑡 *\(Line 6\). In this study, we

*𝑖*

take the mean value of the estimated aggressiveness at each time instant over the past window, premised on the idea that a driver’s aggressiveness typically remains constant or at most varies slowly over a short time period, and a global estimate is classified into six aggressiveness levels, i.e., *𝜇𝑣 *∈ *𝑀𝑣 *= \{0 *, * 0 *. * 2 *, * 0 *. * 4 *, * 0 *. * 6 *, * 0 *. * 8 *, * 1\}. Since the objective of the global aggressiveness estimation is to obtain a coarse value, only finite values in *𝑀𝑣 * are considered. Specifically, CAV compares the mean aggressiveness value over the past window to the values in *𝑀𝑣 * and picks the closest value in *𝑀𝑣 * as the vehicle’s aggressiveness level, *̄*

*𝜇𝑡*. Then, each vehicle’s

*𝑖*

*̄*

*𝜇𝑡 * is stored in the buffer  *𝑡 *= \{ *̄*

*𝜇𝑡 , *… *, ̄*

*𝜇𝑡 *\} \(Line 7\). This finite classification strategy can improve the estimate’s robustness to *𝑖*

1

*𝑛*

measurement noises and data outliers. 

Using the globally estimated vehicle’s aggressiveness *̄*

*𝜇𝑡*, the future trajectories of potential interactive vehicles can be predicted *𝑖*

using IDM \(Line 11–12\). Here, the state update is based on the discrete-time model in \(1\) \(i.e., *𝑓*\(1\)\(⋅\)\), and the predicted states of all preceding vehicles for the next *𝑁𝑝 * step are aggregated as follows \(Line 14\). 

\+ = \[ *𝑡*\+1 *, * *𝑡*\+2 *, *… *, * *𝑡*\+ *𝑁𝑝 *\] *. *

\(11\)

To validate our global aggressiveness estimator, we perform some simulation-based tests using the Next Generation Simulation \(NGSIM\) dataset where the vehicle trajectories are collected on US Highway 101 \(Colyar and Halkias, 2007\). We randomly pick 1000 vehicles from the dataset that follow their leading vehicles with no lane changes. Based on the proposed method, we estimate their drivers’ aggressiveness and predict their future positions and velocities for the next 5s, as shown in Fig. 4. Our approach is compared with alternative prediction methods that are based on constant velocity or acceleration assumption which is better than constant IDM parameters \(Bhattacharyya et al., 2020\), to show the feasibility of IDM-based coarse prediction estimation. As a result, we can observe that our approach exhibits the smallest root-mean-square errors \(RMSEs\). 

We note that some other state-of-the-art while more complex motion prediction techniques, including the neural network-based approaches in Liu et al. \(2019\), Altché and de La Fortelle \(2017\), may be able to achieve even smaller position and velocity prediction RMSEs. However, recall that the goal of our global estimation process is to obtain a coarse estimate of each preceding vehicle’s aggressiveness, which will be used as the initial value for the subsequent local aggressiveness estimation \(thus, will be refined\). For this purpose, our approach is simple while sufficient, as will be illustrated in our simulations in Section 5. Therefore, other more complex motion prediction methods are not considered in this paper. To show the correlation between the willingness of yield and the aggressiveness that estimated in our global aggressiveness estimation, the detail verification is performed in Section 5.1. 

A few examples of real-time estimating drivers’ aggressiveness using the above-described approach are illustrated in Fig. 5. The drivers in Fig. 5 are arbitrarily selected from the US Highway 101 of NGSIM dataset, to show the clear cases and fluctuation cases about global aggressiveness estimation. Fig. 5\(a\) shows two cases where the driver’s aggressiveness is clearly identified. After a sufficient dataset has been collected \(indicated by the gray area\), the drivers’ aggressiveness estimates are classified into six levels according to Algorithm 1 \(indicated by the red and blue lines\). Because the vehicles in these two cases primarily exhibit aggressive or cautious behavior, the aggressiveness estimates converge quickly. In contrast, Fig. 5\(b\) shows two cases where the estimates fluctuate. In such cases, the aggressiveness estimate will be refined at the lower layer, which will be discussed in the next subsection. 

*3.2. Local aggressiveness estimation*

In this subsection, the globally estimated aggressiveness is refined based on the local interactions between vehicles. Although global estimation results provide coarse information on the potential interactive vehicles, this does not guarantee that interactive 7

*K. Ji et al. *

*Transportation Research Part C 150 \(2023\) 104109*

**Fig. 5. **Globally estimated vehicle’s aggressiveness, whose \(a\) aggressiveness is clearly identified, and \(b\) aggressiveness estimate fluctuates. 

vehicles necessarily behave as the globally estimated aggressiveness value suggests. That is, during the local interaction, there is a possibility that the interactive vehicle exhibits a different level of aggressiveness. For this, we propose the following interaction-based local aggressiveness estimation strategy \(Ji et al., 2021\). 

*̄*

*𝜇𝑡 *\+ *𝛽𝑡*

*̄*

*𝜇𝑡*\+1 ←

*. *

\(12\)

1 \+ *𝛼𝑡*

where *𝛼𝑡 *∈ \(0 *, *∞\] and *𝛽𝑡 *∈ \[0 *, 𝛼𝑡*\] are tunable parameters that update the aggressiveness estimate of the interactive vehicle for every time step. 

The initial aggressiveness is set to the last value of the global estimation, and the local estimation begins once the ego vehicle reaches a neighborhood of the interactive vehicle. Thanks to this hierarchical structure, the time needed to build up a reasonable local aggressiveness estimate is reduced by using the global estimate as the initial value compared to using a random value as initial aggressiveness \(e.g., *̄*

*𝜇* 0 = 0 *. * 5\). In particular, if an interactive vehicle yields to the ego vehicle, *𝛽𝑡 * is set to 0, resulting in a decrease in aggressiveness. Similarly, if the interactive vehicle ignores the ego vehicle’s intention to change lanes, we assign identical values to *𝛽𝑡 * and *𝛼𝑡 * to increase aggressiveness. 

It should be noted that global and local aggressiveness estimations occur hierarchically, and while the local aggressiveness is being estimated, behaviors of the other vehicles that could be future interactive vehicles continue to be monitored, and their global aggressiveness estimations are kept being performed. 

**4. Hierarchical decision-making strategy for CAV**

In this section, on the basis of the estimated aggressiveness of drivers, a hierarchical and game-theoretic decision-making approach in the overtaking scenario is proposed. 

*4.1. Reward function design*

A reward function is a mathematical representation of the goal of a driver in a certain driving scenario. In this study, we design the following reward function consisting of several terms for the ego vehicle to maximize in the overtaking scenario \(Li et al., 2018\):

*𝑅 *= *𝑤*

*̂*

1 *̂*

*𝑠 *\+ *𝑤* 2 *̂𝑣 *\+ *𝑤* 3 *ℎ *\+ *𝑤* 4 *̂𝑜 *\+ *̂𝑐. *

\(13\)

where *𝑅 * is the reward function, *̂𝑠, ̂*

*𝑣, ̂ℎ*, *̂*

*𝑜*, and *̂*

*𝑐 * represent ‘‘safety’’, ‘‘velocity’’, ‘‘headway’’, ‘‘overtaking’’, and ‘‘comfort’’ rewards respectively, *𝑤* 1 *, * 2 *, * 3 *, * 4 *> * 1 are the weighting factors expressing the importance of each reward term. 

It should be noted that the weighting factors for each term are assigned with different values based on their importance in common driving scenarios. For example, ‘‘safety’’, i.e., collision avoidance, should be considered to be the most important criterion, and ‘‘headway’’ reward can be the second most important criterion. Next, since overtaking is typically performed as a means to achieve increased travel speed, the ‘‘overtaking’’ reward should be less than ‘‘velocity’’ reward. Finally, the ‘‘comfort’’ reward can be considered last and used to avoid sudden changes of vehicle accelerations. Based on these relationships, the values of the weighting factors are as follows: *𝑤* 1 = 200 *, 𝑤* 2 = 4 *, 𝑤* 3 = 6 *, 𝑤* 4 = 2, and the weighting factor of comfort reward is set as 1. Also, we assume HVs do not change their lane by assigning *𝑤* 4 = 0 when computing the reward of HV from the perspective of CAV. Since the goal of CAV

is to overtake quickly, the reward design does not consider traffic disturbance, and only the individual reward for each vehicle is considered in this study. 

The reward terms are now explained as follows: The term *̂𝑠 *∈ \{−1 *, * 0\} represents the safety of the vehicle, taking the value of −1

if a vehicle collision accident occurs, and 0 otherwise. The safety term is required because although collision event may not occur 8

*K. Ji et al. *

*Transportation Research Part C 150 \(2023\) 104109*

in the real scenarios, it can occur in the prediction side. The collision is computed by detecting the overlap of the vehicles by using the Matlab command *polybool\(\). *

The term *̂*

*𝑣 * penalizes the difference between the desired and current speeds:

| *𝑣 *− *𝑣 *|

*̂*

*𝑣 *= − |

0

|

| *. *

\(14\)

| *𝑣*

|

0

|

Since *̂*

*𝑣 * is always negative if vehicle speed *𝑣 * differs from desired vehicle speed *𝑣* 0, the vehicle tries to make \(14\) as close to 0 as possible by controlling the vehicle speed *𝑣 * towards *𝑣* 0. 

The headway reward term *̂ℎ * is dependent on the net distance from the immediately preceding vehicles:

\{−1 if *𝑠 < 𝑠*∗

*̂ℎ *=

\(15\)

0

otherwise. 

where desired headway *𝑠*∗ is computed based on \(4\). It is set as the binary to simplify the vehicle motivation that vehicle does not accelerate when it is expected to violate the desired headway distance. 

The overtaking reward term *̂𝑜 * motivates the CAV to return to its original lane to complete the overtaking maneuver, as follows:

\{0

if CAV is in the original lane

*̂*

*𝑜 *=

\(16\)

−1

if CAV is in the overtaking lane. 

In \(16\), the CAV prefers to maintaining its original lane as much as possible since it receives negative rewards otherwise. For example, if CAV changes lanes, it tries to return to its original lane as soon as possible to avoid negative rewards. 

The comfort reward term *̂𝑐 * is included to minimize the jerk of the vehicle so that passengers can feel comfortable. 

| *̇𝑣𝑡 *− *̇𝑣𝑡*−1 |

*̂*

*𝑐 *= − ||

| *. *

\(17\)

|

*𝛥𝑡*

||

Based on this, the vehicle prefers not to changing speeds rapidly. 

We consider a receding-horizon optimization-based strategy: We let the CAV chooses an action sequence in a way that maximizes the following cumulative reward \(Han et al., 2020\):

*𝑁𝑝*−1

∑

 *𝑡*\( *𝐾𝑡 *\) =

*𝜆𝑘𝑅𝑡*\+ *𝑘*\( *𝜅𝑡*\+ *𝑘*| *𝑡*\+ *𝑘, 𝑧𝑡*\+ *𝑘*\) *, *

\(18\)

*𝑐𝑎𝑣*

*𝑐𝑎𝑣*

*𝑐𝑎𝑣*

*𝑘*=0

where  *𝑡*\( *𝐾𝑡 *\) is the cumulative reward over the planning horizon, given the predicted behaviors of the CAV *𝑧𝑡*\+ *𝑘 * and the other *𝑐𝑎𝑣*

*𝑐𝑎𝑣*

vehicles  *𝑡*\+ *𝑘*, *𝑁𝑝 * is a prediction horizon, and *𝜆 *∈ \(0 *, * 1\) is a discount factor to account for the uncertainties in the future, and *𝑡*| *𝑡*

*𝑡*\+1| *𝑡*

*𝑡*\+ *𝑁*

*𝐾𝑡*

= \( *𝜅*

*𝑝 *−1| *𝑡*

*𝑐𝑎𝑣*

*𝑐𝑎𝑣, 𝜅𝑐𝑎𝑣 , *… *, 𝜅𝑐𝑎𝑣*

\) is the optimized action sequence computed at the time instant *𝑡 * as shown below: *𝐾𝑡*

∈ argmax  *𝑡*\( *𝐾𝑡 *\) *, *

\(19\)

*𝑐𝑎𝑣*

*𝑐𝑎𝑣*

*𝑡*\+ *𝑘*| *𝑡*

*𝜅𝑐𝑎𝑣 *∈ *𝛤𝑙*

*𝑘 *= 0 *, *… *, 𝑁𝑝 *− 1 *. *

In the receding-horizon control, we take the first element in \(19\) as the optimal action \(i.e., *𝑡*| *𝑡*

*𝜅𝑡, *∗

*𝑐𝑎𝑣 *= *𝜅𝑐𝑎𝑣*\), which is applied to the

vehicle. 

*4.2. Global decision-making strategy*

As previously discussed, even if the preceding vehicle drives slowly in comparison to other adjacent vehicles, initiating an overtaking maneuver is not always the best option, and staying in the original lane is preferable in some cases. In this subsection, how the CAV decides to initiate an overtaking is explained \(see Algorithm 2\). 

The main idea is to compare the expected cumulative rewards for staying in the original lane versus overtaking a certain vehicle ahead in the car following situation. The inputs of Algorithm 2 are \+, ,  *𝑡*, *𝑧𝑡*

and *𝛤*

*𝑐𝑎𝑣*

*𝑐𝑎𝑣 *\(Line 1\). First, CAV evaluates the

expected cumulative reward when keeping the original lane for the next *𝑁𝑝 * steps \(Lines 3–9\). For this, the lateral actions \(i.e., *𝜅𝑐𝑟*, *𝜅𝑐𝑙*\) are excluded from the available action set \(Line 3\), and the action set is recovered after estimating the cumulative reward \(Line 9\). The optimal action of CAV at each time instant *𝑘 * is determined by \(19\) \(Line 5\) and the state of the CAV is updated \(Line 6\). For each time step, the reward  *𝑚 * is calculated based on \(13\) \(Line 7\). 

Then, the cumulative reward  *𝑜 * when the CAV overtakes a certain vehicle *𝑖 *∈  is calculated \(Lines 10–20\). We assume that *𝑖*

the target vehicle *𝑖 * is driven by a cautious driver that allows the CAV to cut in its front, so vehicle *𝑖 * is assumed to always choose to decelerate \(i.e., action *𝜅𝑑*\) when the CAV arrives at the parallel position of vehicle *𝑖 *\(Lines 12–15\). 

To reduce computation complexity, instead of relying on the optimization problem \(19\), the actions of the CAV are determined based on the following rules \(Line 16\):

⎧ *𝜅*

⎪ *𝑐𝑙*

if *𝑥𝑐𝑎𝑣 *≤ *𝑥𝑖 * and *𝑦𝑐𝑎𝑣 < * middle of left lane

*𝜅𝑐𝑎𝑣 *= ⎨ *𝜅*

\(20\)

*𝑐𝑟*

if *𝑥𝑐𝑎𝑣 > 𝑥𝑖*

⎪⎩ *𝜅𝑎*

otherwise. 

9

*K. Ji et al. *

*Transportation Research Part C 150 \(2023\) 104109*

**Algorithm 2: **Overtaking Decision-making Strategy Based on Traffic Prediction and Aggressiveness **1 **Input  \+, ,  *𝑡*, *𝑧𝑡*

*, 𝛤*

*𝑐𝑎𝑣*

*𝑐𝑎𝑣*

**2 **Initialize  *𝑚, * *𝑜 *← 0 *, *∀ *𝑖 *∈ 

*𝑖*

**3 ** *𝛤𝑐𝑎𝑣 *= *𝛤𝑐𝑎𝑣 *− \{ *𝜅𝑐𝑟, 𝜅𝑐𝑙*\}

**4 for ** *𝑘 *∈ *𝑡 *∶ *𝑡 *\+ *𝑁𝑝 *− 1 **do**

**5**

*𝜅𝑘, *∗

*𝑐𝑎𝑣 *← *𝑓*\(19\)\( *𝑘, 𝑧𝑘*

\)

*𝑐𝑎𝑣*

**6**

*𝑧𝑘*\+1 ← *𝑓*

*, 𝜅𝑘, *∗

*𝑐𝑎𝑣*

\(1\)\( *𝑧𝑘*

*𝑐𝑎𝑣*

*𝑐𝑎𝑣*\)

**7**

 *𝑚 *←  *𝑚 *\+ *𝜆𝑘*− *𝑡 *× *𝑓*\(13\)\( *𝑘*\+1 *, 𝑧𝑘*\+1\) *𝑐𝑎𝑣*

**8 end**

**9 ** *𝛤𝑐𝑎𝑣 *= *𝛤𝑐𝑎𝑣 *\+ \{ *𝜅𝑐𝑟, 𝜅𝑐𝑙*\}

**10 foreach ** *𝑖 *∈  **do**

**11**

**for ** *𝑘 *∈ *𝑡 *∶ *𝑡 *\+ *𝑁𝑝 *− 1 **do**

**12**

**if ** *𝑥𝑐𝑎𝑣 > 𝑥𝑖 ***then**

**13**

*𝜅𝑖 *← *𝜅𝑑*

**14**

 *𝑘*\+1 ← *𝑓*\(1\)\( *𝑘, 𝜅𝑖*\)

**15**

**end**

**16**

*𝜅𝑘, *∗

*𝑐𝑎𝑣 *← *𝑓*\(20\)\( *𝑘, 𝑧𝑘*

\)

*𝑐𝑎𝑣*

**17**

*𝑧𝑘*\+1 ← *𝑓*

*, 𝜅𝑘, *∗

*𝑐𝑎𝑣*

\(1\)\( *𝑧𝑘*

*𝑐𝑎𝑣*

*𝑐𝑎𝑣*\)

**18**

 *𝑜 *←  *𝑜 *\+ *𝜆𝑘*− *𝑡 *× *̄𝜇*

\)

*𝑖*

*𝑖*

*𝑖 *× *𝑓*\(13\)\( *𝑘*\+1 *, 𝑧𝑘*\+1

*𝑐𝑎𝑣*

**19**

**end**

**20 end**

**21 if ** *𝑜 *≤  *𝑚, *∀ *𝑖 *∈  **then**

*𝑖*

**22**

F *𝑜 *← 0

**23 else**

**24**

F *𝑜 *← 1

**25 end**

**26 **Output F *𝑜*

In \(20\), the CAV always initiates the overtaking, so it chooses *𝜅𝑐𝑙 * until the lane change to the left lane is completed \( *𝜅𝑐𝑎𝑣 *← *𝜅𝑐𝑙*\). 

Once the CAV arrives at the parallel position of the target vehicle *𝑖 *\(i.e., *𝑥𝑐𝑎𝑣 > 𝑥𝑖*\), the action to return to the original lane \( *𝜅𝑐𝑟*\) is selected. Otherwise, the CAV accelerates until it reaches *𝑣𝑚𝑎𝑥 * in the left lane to reach the target position quickly. The cumulative reward  *𝑜 * of overtaking the vehicle *𝑖 * is evaluated \(Line 18\), which also considers the globally estimated aggressiveness *̄*

*𝜇*

*𝑖*

*𝑖*. For

example, if *̄*

*𝜇𝑖 * is close to 1, indicating an aggressive driver,  *𝑜 < * 0 scaled by *̄*

*𝜇*

*𝑖*

*𝑖 * is even smaller, and overtaking the *𝑖* th vehicle is

unlikely to be initiated. 

By comparing  *𝑚 * and  *𝑜*, the overtaking decision flag F

*𝑖*

*𝑜 * is determined \(Lines 21–26\). If F *𝑜 * is determined as zero, the CAV does not initiate an overtaking, while an overtaking is initiated when F *𝑜 *= 1. 

It should be noted that the actual position of the CAV \( *𝑥𝑐𝑎𝑣*\) is always in the original lane while Algorithm 2 is being processed. 

Trajectories of overtaking each preceding vehicle *𝑖 * are predicted through Algorithm 2 to compare the benefit of the overtaking over the lane keeping in terms of expected cumulative reward. 

*4.3. Local decision-making strategy*

Once the overtaking flag F *𝑜 * is determined as 1 from Algorithm 2, the CAV initiates an overtaking. After the CAV reaches the position of the target interactive vehicle, it tries to return to the original lane by interacting with that vehicle. In this subsection, a leader–follower game approach is employed to model such interactions \(Başar and Olsder, 1998\). In our game formulation, the CAV is regarded as the leader and the interactive vehicle is regarded as the follower, while CAV selects its action sequence that maximizes the cumulative reward in \(18\). 

Specifically, when CAV begins to overtake, the potential target vehicle is chosen based on the overall aggressiveness of all preceding vehicles. For example, it is assumed that a vehicle with a low aggressiveness will yield if the CAV indicates a lane-change intention and tries to cut in front of such vehicles. 

In this study, the interaction between the CAV and target vehicle is modeled using a leader–follower game strategy. It is assumed in the conventional leader–follower game that the leader acts first, and the follower acts after observing the leader’s action. As a result, to maximize its cumulative reward, the leader should predict the follower’s reaction to the leader’s specific action. In the overtaking scenario, the CAV \(leader\) sends out the lane-change signal first, followed by the target vehicle \(follower\)’s response. 

The follower’s reaction to leader’s specific action sequence *𝐾𝑡, *∗ is given as follows: *𝑙*

\(

\(

\)\)

*𝐾𝑡, *∗ ∈

argmax



*𝐾𝑡, *∗ *, 𝐾𝑡*

*. *

\(21\)

*𝑓*

*𝑓*

*𝑙*

*𝑓*

*𝐾𝑡 *∈ *𝛤*

*𝑓*

*𝑓 *×⋯× *𝛤𝑓*

10

*K. Ji et al. *

*Transportation Research Part C 150 \(2023\) 104109*

When the leader’s action sequence *𝐾𝑡, *∗ is given, the follower chooses the optimal action sequence *𝐾𝑡, *∗ in *𝛤*

*𝑙*

*𝑓*

*𝑓 *× ⋯ × *𝛤𝑓 * that

maximizes her own cumulative reward. 

Based on this, the conventional leader–follower equilibrium can be expressed as follows \(Başar and Olsder, 1998\): \(

\(

\)\)

*𝐾𝑡, *∗ ∈

argmax

min

 *𝐾𝑡, 𝐾𝑡, *∗

*, *

\(22\)

*𝑙*

*𝑙*

*𝑡, *∗

*𝑡, *∗

*𝑙*

*𝑓*

*𝐾𝑡*∈ *𝛤*

*𝐾*

∈ *̃*

*𝛤*

\( *𝐾𝑡*\)

*𝑙*

*𝑙 *×⋯× *𝛤𝑙*

*𝑓*

*𝑓*

*𝑙*

\(

\)

where the leader’s optimal action sequence *𝐾𝑡, *∗ maximizes the cumulative reward 

*𝐾𝑡, 𝐾𝑡*

, which is affected by both leader

*𝑙*

*𝑙*

*𝑙*

*𝑓*

and follower. 

Here, the set of rational reactions of the follower is computed based on the leader’s action sequence *𝐾𝑡*: *𝑙*

\{

\}

*̃*

*𝛤 𝑡, *∗\( *𝐾𝑡*\) =

*𝐾𝑡, *∗ ∈ *𝛤*

*, 𝐾𝑡, *∗\) ≥ 

*, 𝐾𝑡 *\) *, *∀ *𝐾𝑓 *∈ *𝛤*

*. *

\(23\)

*𝑓*

*𝑙*

*𝑓*

*𝑓 *× ⋯ × *𝛤𝑓 *∶  *𝑓 *\( *𝐾 𝑡𝑙*

*𝑓*

*𝑓 *\( *𝐾 𝑡𝑙*

*𝑓*

*𝑓 *× ⋯ × *𝛤𝑓*

If the follower’s optimal action sequence corresponding to given leader’s action is unique, i.e., *̃*

*𝛤 𝑡, *∗\( *𝐾𝑡*\) is a singleton, then

*𝑓*

*𝑙*

the leader chooses the action that is expected to maximize the reward by predicting follower’s response as *𝐾𝑡, *∗ ∈ *̃*

*𝛤 𝑡, *∗\( *𝐾𝑡*\). If the

*𝑓*

*𝑓*

*𝑙*

follower’s optimal action sequences under a leader’s specific action sequence are determined as more than a single action sequence, the leader’s prediction of the follower’s response is uncertain. In that case, the leader assumes that the follower may take any action in *̃*

*𝛤 𝑡, *∗\( *𝐾𝑡*\), and the leader chooses the optimal action sequence *𝐾𝑡, *∗ that maximizes her worst-case reward due to the uncertain *𝑓*

*𝑙*

*𝑙*

follower’s action \(i.e., maximin method\). 

As described above, the conventional leader–follower game \(also called the Stackelberg game\) assumes a sequential reasoning and acting structure where the follower acts \(and reacts\) immediately after she observes the leader’s selected action sequence, which is an unrealistic assumption for human decision-making in real-world driving scenarios \(e.g., due to gradual reveal of the leader’s action sequence over time, human driver reaction delay, etc.\). As a result, we consider a modified version of leader–follower game structure to model the leader’s and follower’s simultaneous decision-making \(Li et al., 2020\). The modified structure is shown below: \(

\(

\)\)

*𝐾𝑡, *∗ ∈

argmax

min



*𝐾𝑡, 𝐾𝑡*

*. *

\(24\)

*𝑓*

*𝑓*

*𝑙*

*𝑓*

*𝐾𝑡 *∈ *𝛤*

*𝐾𝑡*∈ *𝛤𝑙*×⋯× *𝛤𝑙*

*𝑓*

*𝑓 *×⋯× *𝛤𝑓*

*𝑙*

In \(24\), it is assumed that the follower is not able to immediately observe the leader’s selected action sequence. Therefore, the follower assumes the worst-case scenario by considering the minimum cumulative reward caused by the leader’s action sequence and chooses the action sequence that maximizes this minimum reward. 

Now, the modified leader–follower equilibrium is formulated as follows:

\(

\(

\)\)

*𝐾𝑡, *∗ ∈

argmax

min 

*𝐾𝑡, 𝐾𝑡, *∗

*, *

\(25\)

*𝑙*

*𝑙*

*𝑡, *∗

*𝑡, *∗

*𝑙*

*𝑓*

*𝐾𝑡*∈ *𝛤*

*𝐾*

∈ *̃*

*𝛤*

*𝑙*

*𝑙 *×⋯× *𝛤𝑙*

*𝑓*

*𝑓*

\{

\}

*̃*

*𝛤 𝑡, *∗ ∈

*𝐾𝑡, *∗ ∈ *𝛤*

\(

*, 𝐾𝑡, *∗\)\) ≥

min

\(

*, 𝐾𝑡 *\)\) *, *∀ *𝐾𝑓 *∈ *𝛤*

\(26\)

*𝑓*

*𝑓*

*𝑓 *× ⋯ × *𝛤𝑓 *∶

min

*𝑓 *\( *𝐾 𝑡𝑙*

*𝑓*

*𝑓 *\( *𝐾 𝑡𝑙*

*𝑓*

*𝑓 *× ⋯ × *𝛤𝑓*

*𝐾𝑡*∈ *𝛤*

*𝐾𝑡*∈ *𝛤*

*𝑙*

*𝑙 *×⋯× *𝛤𝑙*

*𝑙*

*𝑙 *×⋯× *𝛤𝑙*

where *𝐾𝑡, *∗ is the leader’s optimal action sequence that maximizes her cumulative reward under the assumption that the follower *𝑙*

takes actions in *̃*

*𝛤 𝑡, *∗, which denotes the set of action sequences for the follower to maximize her reward under the maximin strategy *𝑓*

in \(24\). The effectiveness of this modified leader–follower game structure for modeling driver interaction in multi-vehicle traffic scenarios has been validated in multiple previous works \(Li et al., 2020, Liu et al. , 2022, 2021b.\) In \(24\)–\(26\), the cumulative rewards  *𝑙*\( *𝐾𝑡, 𝐾𝑡 *\) and 

*, 𝐾𝑡 *\) corresponding to predicted action sequences of the leader and

*𝑙*

*𝑓*

*𝑓 *\( *𝐾 𝑡𝑙*

*𝑓*

follower, *𝐾𝑡 * and *𝐾𝑡 *, can be computed according to an expression similar to \(18\), where the subscript ‘‘cav’’ is replaced with ‘‘hv’’

*𝑙*

*𝑓*

when the ego vehicle is a human-driven vehicle \(follower\) and in this case the  denotes the other vehicle’s \(leader’s\) behaviors. 

Note that the desired headway *𝑠*∗ of a human-driven vehicle, computed according to \(4\), depends on its driver’s aggressiveness *𝜇*. 

Therefore, when evaluating a human-driven vehicle’s \(follower’s\) cumulative reward and solving for both parties’ optimal action sequences, the CAV needs to use the estimated follower’s aggressiveness *̄*

*𝜇𝑡*. During their interactions, the local aggressiveness

estimation method in \(12\) is used to refine *̄*

*𝜇𝑡 * at each time instant *𝑡 * by comparing the predicted and observed follower’s actions. 

Thanks to this game-theoretic approach, CAV can ensure safety even if it fails to overtake. 

As in conventional receding-horizon control method, the first element of the computed action sequence \(i.e., *𝜅𝑡*| *𝑡*\) is applied to the vehicle, and the same procedure is repeated at each time instant to account for varying driving condition. In addition, to further reduce the computational complexity of the CAV decision-making process, when computing the expected cumulative reward in \(18\), we assume that the follower holds a constant action over the prediction horizon. The optimal action sequence of the leader corresponding to constant action of the follower is solved for using a tree search method, a widely-adopted technique for solving sequential decision-making problems with a finite decision set \(Sun et al., 2020; Claussmann et al., 2015\). 

*4.4. Overall architecture of the proposed method*

The overall structure of the proposed hierarchical decision-making strategy is depicted in Fig. 6. Using the global traffic information from the V2X communication system, CAV coarsely estimates the aggressiveness of the vehicles ahead and predicts their behaviors using Algorithm 1. Following that, CAV assesses the benefit of overtaking to determine whether or not to perform 11



*K. Ji et al. *

*Transportation Research Part C 150 \(2023\) 104109*

**Fig. 6. **Proposed structure of the hierarchical decision-making. 

an overtaking maneuver based on Algorithm 2. If CAV determines that overtaking is more advantageous than staying in the current lane, it initiates an overtaking by changing lanes. This procedure is performed at the upper layer. 

If an overtaking has been initiated and the CAV reaches the position of the target interactive vehicle, it sends out a lane-change signal. Because the globally estimated aggressiveness is coarse, CAV locally refines the interacting vehicle’s aggressiveness estimate while attempting to cut in front of the target vehicle. The leader–follower game is employed to make the best decisions during the local interactions. If the predicted action of the target vehicle does not disrupt the CAV and there is enough room to change lanes, the CAV returns to the original lane. In contrast, if the target vehicle’s predicted action is to ignore the CAV according to its estimated aggressiveness, the CAV determines that cutting in front of the target vehicle is not possible. In that case, CAV changes the target vehicle to the vehicle further ahead in the original lane, and interacts with the new target vehicle at the lower layer. 

This procedure is repeated until the CAV succeeds in returning to the original lane. Since CAV’s optimal action sequence *𝐾𝑡, *∗ is to *𝑙*

maximize his/her reward for some future steps, and the reward is designed to include a safety reward with the largest weighting factor, the safety is prioritized, even if CAV initiates the overtaking and fails to come back to its original lane. That is the collision between CAV and the interacting vehicle is avoided. 

**5. Case studies**

In this section, we verify the correlation between the driver’s aggressiveness and the willingness to yield using real-world driving data. Next, we validate the efficacy of our game-theoretic hierarchical decision-making strategy in a variety of test scenarios, and the results are compared to those obtained when using the alternative conventional methods. 

*5.1. Correlation between driver aggressiveness and willingness of yield*

In this paper, we assume there exists a correlation between drivers’ aggressiveness, which is related to longitudinal behavior, and willingness to yield. to confirm the above assumption \(i.e. correlation between aggressiveness and time headway\), the real-data-based analysis using the US Highway 101 of NGSIM dataset has been performed \(Colyar and Halkias, 2007\). Specifically, we randomly choose 10 drivers who yielded to a vehicle that attempts to change the lane, and 10 drivers who prevent the lane change of the vehicle in the next lane. Here, the driver preventing the lane change means that there is a lateral movement of the vehicle in the next lane, but the vehicle in the next lane fails to change the lane in the end. As proposed in this paper, before the vehicle interaction, the global aggressiveness is estimated for 10 s immediately before interaction. First, we analyze the representative 12



*K. Ji et al. *

*Transportation Research Part C 150 \(2023\) 104109*

**Fig. 7. **Snapshots of three interacting vehicles of NGSIM dataset, and the globally estimated aggressiveness of the following vehicles \(blue car\) before interaction with the vehicle that attempts the lane-changing \(red car\). \(a\) The case that the following vehicle yield the lane change \(vehicle labeled 103 in NGSIM dataset\), and \(b\) the case that the following vehicle prevents the lane change \(vehicle labeled 137 in NGSIM dataset\). 

cases of yielding and preventing lane-changing cases, and the snapshots and aggressiveness of each following vehicle are shown in Fig. 7. The snapshots of three interacting vehicles are depicted for every 2.5 s, and the globally estimated aggressiveness of the following vehicle is also illustrated below. The following driver’s estimated aggressiveness at the single step and classified cumulated aggressiveness according to Algorithm 1 are indicated by the red dashed line and blue lines. The vehicle that yields the lane change of the interacting vehicle is described in Fig. 7\(a\). In this case, the following vehicle maintains enough gap between the front vehicle, and the interacting vehicle succeeds to change the lane at 10 s through yielding to the following vehicle. The estimated global aggressiveness of the following vehicle is computed to be generally low, as illustrated in Fig. 7\(a\). Contrary to this, the case when lane changing is prevented by the following vehicle is described in Fig. 7\(b\). In this case, the vehicle that tries the lane change around 5 s, but came back to the original lane because the following vehicle does not give enough space by maintaining a relatively short gap between the vehicle in front. Obviously, the estimated aggressiveness of the following vehicle shows a relatively high value. 

In addition to these representative case studies, the mean and standard deviation of two types of drivers in lane change scenarios \(i.e. yielding drivers and preventing drivers recorded in US highway\) are analyzed in Fig. 8. Here, the vertical line segment gives the standard deviation, and it shows a relatively large value. It is because the drivers have individual aggressiveness in reality. 

Nevertheless, the aggressiveness tendency is overall high for preventing vehicles and low for yielding vehicles. It should be noted that the aggressiveness in our paper depends on IDM parameters, so a specific value may not show the correlation between aggressiveness and the willingness of yield clearly. To overcome this problem, we compare time headway using the recorded NGSIM dataset, which gives the time headway of the vehicles. After filtering out the foremost vehicle and the vehicle whose speed is zero, the average time headway of yielding vehicles is 5 *. * 06 s, and 3 *. * 99 s for preventing vehicles. It is reasonable that lane-changing vehicles take an action when there is enough room in the next lane, meaning the following vehicle maintains a large headway distance \(large time headway\). Therefore, although the aggressiveness of the driver in the real world can be affected by other IDM parameters, the results can support our approach to a certain degree, which assumes that the correlation between aggressiveness and time headway can explain the variety of drivers’ characteristics in the longitudinal motion. 

13



*K. Ji et al. *

*Transportation Research Part C 150 \(2023\) 104109*

**Fig. 8. **The mean and standard deviation of two types of drivers in lane change scenarios. 

**Fig. 9. **Simulation environment: road configuration, and approximated vehicle model. 

*5.2. Simulation environment*

The simulations are performed in the two-lane road where there are four preceding vehicles behave based on modified IDM, as described in Section 2.4. The CAV starts from the fixed position \(i.e., −180 m\) and all preceding vehicles are placed in the same lane with random gaps between vehicles. The Initial velocities of the ego CAV and the vehicles ahead are assumed to be 25 m/s, excluding the 20 m/s of the directly in front, which cause the CAV to overtake it. As shown in Fig. 9, the size of the vehicle is approximated to 5 m × 2 m rectangular box, the lane width is set to 4 m, and the road speed limit is assumed to be 30 m/s. The CAV chooses an action sequence in a receding horizon optimization manner in \(18\)–\(19\) while considering vehicle interaction in

\(25\)–\(26\). 

Since CAV’s desired headway distance and velocity is not satisfied in the initial state, he/she initiate overtaking behavior to go to change lane if overtaking is expected to be possible. We assume the left lane is overtaking lane and that overtaking vehicles need to come back to the original lane after passing the original leading vehicles. Regarding the foremost vehicle that does not follow any vehicle, we assign the neutral aggressiveness value \(i.e., *𝜇 *= 0 *. * 5\) for simulation purpose. Because if there is no vehicle ahead, the desired net distance in \(3\) is set to zero, so \(9\) cannot compute aggressiveness. In this study, we specify the *𝑁𝑙 *= 10 to reflect the recent behaviors of the target vehicles, and *𝑁𝑝 *= 4 for the optimized action sequence. These values are determined by trial and error considering the trade-off between the control performance and the computation complexity, and we found that the computation times for each time step are less than the sampling period *𝛥𝑡*. 

To determine whether the CAV success in overtaking or not, we place a virtual obstacle in the next lane. If the CAV returns to the original lane before hitting the virtual obstacle, the case is considered a success case. 

To show the robustness of our approach, we perform the simulations in three different conditions as follows: 1. *Hard*: It is hard to succeed in overtaking due to the small gaps between vehicles and virtual obstacles placed close by. 

2. *Normal*: The scenario in which the likelihood of overtaking is uncertain \(the gaps between vehicles and position of the virtual obstacle are appropriate\). 

3. *Relaxed*: It is easy to succeed in overtaking due to the large gaps between vehicles and virtual obstacles placed far away. 

Table 2 summarizes the values used in the three scenarios. In hard conditions, e.g., the vehicles are randomly placed at narrow intervals between 25 m and 40 m, and the virtual obstacle is placed close to the CAV \(i.e., 0 m\). In addition, the aggressiveness for each HV is randomly assigned between 0 and 1, which are unknown to CAV. Note that the random values of aggressiveness \( *𝜇 *= \[0 *, * 1\]\) are assigned for preceding vehicles in each episode to reflect real-world stochasticity. It means that drivers basically follow the IDM, but they behave depending on their aggressiveness. 

To verify the success rate of the overtaking in various scenarios, the simulations were performed 10,000 times for every three scenarios. The test platform is built on Matlab R2021a under the desktop specification \(Intel i5-9500 CPU, Ram 16 GB, Windows 10\). For fair comparisons, the same seed was assigned to reproduce each scenario using the Matlab command *rng\(\)*. 

14

*K. Ji et al. *

*Transportation Research Part C 150 \(2023\) 104109*

**Table 2**

Utilized values for each scenarios. 

Scenario

Gap \[m\]

Obstacle position \[m\]

Hard

\[25, 40\]

0

Normal

\[30, 45\]

100

Relaxed

\[35, 50\]

200

*5.3. Alternative decision-making strategies*

In this subsection, two alternative decision-making strategies are introduced for comparison purposes. 

The first alternative approach is rule-based decision-making using the time-to-collision \(TTC\) concept where a TTC value is defined as the time that remains until a collision occurs \(Minderhoud and Bovy, 2001\). After initiating the overtaking, the vehicle decides whether to return to its original lane based on the relative distance gap and speed of two vehicles in the next lane, which is similar to human driving behavior. 

*𝑥𝑡 *− *𝑥𝑡*

− *𝑙*

cav

TTC

*𝑙*

cav =

*. *

\(27\)

*𝑣𝑡* cav − *𝑣𝑡𝑙*

where *𝑣𝑙 * is the speed of the leading vehicle in front of the CAV if the lane change occurs, *𝑥𝑙 * is the position of the leading vehicle, *𝑙 * denotes the length of a vehicle and *𝑥* cav is the position of the CAV. 

A positive TTCcav indicates that a collision between the front vehicle and CAV is likely to happen after TTC if the relative speed between CAV and front vehicle remains constant. For example, if the TTCcav is determined to 1 s, the collision between CAV and preceding car is expected after 1 s. In contrast, the negative TTC means that the gap between the front vehicle and CAV increases if the relative speed is maintained, so no collision is expected after TTC *𝑠 *\(i.e., the forward vehicle is faster than CAV\). Furthermore, to avoid the rear-end collision, TTC value between ego CAV and following HV in the original lane is also considered. 

To sum up, a rule-based lane-change decision-making of the CAV is designed as follows. 

\{ *𝜅*

*𝜅*

*𝑐𝑟*

if TTCcav *> * 5s and TTC *𝑓 > * 5s *, *

cav =

\(28\)

*𝜅𝑎*

otherwise *, *

here, TTC *𝑓 * is computed using \(27\) while CAV as a leader. If CAV is faster than the following vehicle, TTC *𝑓 * is considered as infinity. 

The appropriate TTC threshold for forward collision warning system is 2.4 s \(Zhang et al., 2006\) and the vehicle in common driving situation shall not decelerate while changing lanes when there is a rear vehicle to avoid the risk of a rear-end collision. In this respect, even if TTC at the start of a lane change is more than 2.4 s, it may be less than the warning threshold when the CAV

completes the lane change. Furthermore, a too short lane-changing threshold compromises safety, and might lead to the aggressive behavior of CAV. So we specify the lane-changing threshold as TTCcav = 5 s considering the safety margin. However, depending on the drivers, this threshold may vary. If there is enough space between the CAV and front car, the CAV will attempt to change lanes; otherwise, the CAV will accelerate to find the next target vehicle. 

The second alternative strategy is a general lane change model \(minimizing overall braking induced by lane change,. 

MOBIL\) \(Kesting et al. , 2007\). Using MOBIL, the vehicle decides to change the lanes when it is expected to give a positive impact on the overall traffic. For example, the ‘‘politeness’’ of the ego vehicle, which denotes a degree of altruism, is considered as follows. 

\(

\)

*̄*

*𝑎𝑐𝑎𝑣 *− *𝑎𝑐𝑎𝑣 *\+ *𝑝 ̄𝑎𝑛 *− *𝑎𝑛 *\+ *̄𝑎𝑜 *− *𝑎𝑜 > 𝛥𝑎* th \(29\)

where *̄*

*𝑎𝑐𝑎𝑣 * denotes the expected acceleration of CAV after changing the lane, and *𝑎𝑐𝑎𝑣 * is a current CAV acceleration, *𝑝 *= 1 is the politeness of CAV, *𝛥𝑎* th = 0 *. * 1 m∕s2 is the switching threshold, *̄𝑎𝑛 * denotes the expected acceleration of a new follower \(target vehicle in next lane\) after CAV changes the lane, *𝑎𝑛 * is the current acceleration of the target vehicle, *̄𝑎𝑜 * denotes predicted acceleration of a current follower after CAV changes the lane, and *𝑎𝑜 * is the current acceleration of a follower in the overtaking lane. In our simulation setting, since there is no follower in the overtaking lane, *̄*

*𝑎𝑜 * and *𝑎𝑜 * are zeros. Here, the expected vehicle accelerations \(i.e., *̄𝑎𝑐𝑎𝑣*, *̄𝑎𝑛*\) are obtained from the IDM, and the current vehicle accelerations \(i.e., *𝑎𝑐𝑎𝑣*, *𝑎𝑜*\) are assumed to be given. In addition, by placing the virtual vehicle in the overtaking lane, the CAV is motivated to return to the original lane when it drives in the overtaking lane. 

For the alternative driving strategies that cannot access to V2X communication, the only available information at the start of the simulation is the preceding vehicle’s position and velocity, as well as the closing position of the overtaking lane. Using this information, alternative strategies can determine whether to initiate overtaking. A TTC-based lane-changing decision-making approach is employed for all strategies. For example, if the TTC between CAV and the obstacle at the overtaking lane is larger than the TTC between CAV and the preceding vehicle at the current lane, then CAV initiates overtaking. Otherwise, CAV maintains the lane. In summary, all strategies decide whether to overtake based on TTC, and our approach requires the additional condition based on Algorithm 2 since it has additional long-sighted preview information. 

15



*K. Ji et al. *

*Transportation Research Part C 150 \(2023\) 104109*

**Fig. 10. **Snapshots of overtaking success case, and the estimated aggressiveness of the interactive vehicle \(Car 3\). 

*5.4. Test results*

The simulation results are described in Figs. 10–13, where the CAV is controlled based on the proposed method. Every 3 s, the snapshots describe the positions of all vehicles, and the plot below the snapshot shows the interactive vehicle’s estimated aggressiveness. The global aggressiveness is estimated first, and the estimate is confirmed when the target vehicle interacts with it. 

For each plot, the interacting moment is denoted by a vertical dotted line. The red box labeled by 0 represents the CAV, and the blue boxes labeled as 1–4 are the preceding HVs in the snapshots. The average computation time to estimate the global aggressiveness of four vehicles is 60 ms, and local aggressiveness estimation takes 3 ms. The average computation to determine whether overtake or not is 20 ms \(i.e., the computation time for global decision-making\), and the average computation for local decision-making takes 300 ms, so the sum of computations is less than the sampling time 0.5 s. Therefore, no computational burden was found, at least at the simulation level. It is left to our future work to further investigate the real-time feasibility. Also, for the real-time implementation, we expected improved computational efficiency by converting Matlab to C language. 

Figs. 10 and 11 describe the situations in which the overtaking is successful. In these cases, the globally estimated aggressiveness of a target vehicle is low, so the CAV initiates the overtaking process \(See the globally estimated low *𝜇 * before beginning the local interactions in Figs. 10 and 11\). Here, the initial value at 0 s is determined in the same way as in Fig. 5. Depending on the globally estimated *𝜇*, the target vehicle is chosen and its aggressiveness is locally confirmed. Since the update of *𝜇 * during interaction is based on the executed actions of the interactive vehicle in \(12\), it is difficult to accurately estimate the assigned aggressiveness \(See blue lines in Figs. 10 and 11\). However, we can see that the locally estimated aggressiveness is moving in the right direction, even if it sometimes deviates from the actual value due to the unexpected actions of the human driver, which is normal in practice. Based on these estimates, the CAV should be able to return to its original lane before reaching the virtual obstacle. 

Fig. 12 shows the case where the CAV cannot return to its original lane due to the incorrectly estimated aggressiveness. For some reason, Car 3 exhibits conservative behavior for several seconds, resulting in a decrease in the globally estimated aggressiveness, prompting the overtaking to begin. However, it has been assigned a neutral \(0.5\) value in actual, and Car 3 does not provide enough space for the CAV to change lanes \(See the third snapshot\). During the local interaction, the CAV increases the aggressiveness of Car 3, so the lane-change action is prohibited, and CAV reaches the virtual obstacle. Note that we model the human driver based on the modified IDM \(Eq. 2.4\), including aggressiveness, which can show vague behavior when the assigned aggressiveness is neutral value. When the CAV locally interacts with the Car 3 to return to the original lane, the CAV adjusts the Car 3’s aggressiveness based on the observed behaviors \(i.e., ‘‘yield’’ or ‘‘not yield’’\). In this case, the Car 3 that has a neutral aggressiveness value reacts to CAV

based on Eq. \(7\), and CAV judges the Car 3’s intention as ‘‘not yield’’ \( *𝜇 *≈ 1\). In the real world, it is natural that the driver who has neutral aggressiveness may or may not yield, and this is why the CAV fails to overtake. 

The snapshots in Fig. 13 is the case where the CAV does not attempt the overtaking since explicit benefit is not expected in terms of the reward if the overtaking is initiated, and CAV maintains its lane. In this case, the globally estimated aggressiveness of all preceding vehicles are quite high. For clarity, we only show the globally estimated aggressiveness of Car 4, and it is determined that 16





*K. Ji et al. *

*Transportation Research Part C 150 \(2023\) 104109*

**Fig. 11. **Snapshots of overtaking success case, and the estimated aggressiveness of the interactive vehicle \(Car 4\). 

**Fig. 12. **Snapshots of overtaking failure case, and the estimated aggressiveness of the interactive vehicle \(Car 3\). 

Car 4 is likely the aggressive driver. Indeed, we intentionally assign the relatively high *𝜇 * to all preceding vehicles, and ‘maintaining lane’ decision is appropriate rather than initiating the overtaking. 

Fig. 14 shows the simulation numbers of overtaking success, failure, and maintaining the lane under 10,000 different scenarios for the proposed method \(Game\), rule-based method \(Rule\), and common lane change model \(MOBIL\) in the three different conditions \(Hard, Normal, and Relaxed\). Here we can see the maintaining decision of rule-based and MOBIL approach is only performed in hard 17



*K. Ji et al. *

*Transportation Research Part C 150 \(2023\) 104109*

**Fig. 13. **Snapshots of maintaining the lane case, and the estimated aggressiveness of the closest vehicle \(Car 4\). 

**Fig. 14. **Simulation numbers of overtaking success, failure, and maintaining lane under various scenarios for the proposed- and rule-based methods. 

scenarios. It is because the initial conditions of normal and relaxed scenarios always satisfy the TTC-based overtaking condition. In a normal scenario, while the number of successful overtakes using alternative driving strategies is higher than our approach, the number of failure is much higher than ours. This is because the CAV does not initiate the overtaking if the benefit in terms of the reward is not expected even if the TTC-based overtaking initiating condition is satisfied, and maintains the lane \(see the green bar in Fig. 14\). In the hard scenarios, the number of successful overtakes is similar for all three approaches, but the number of failed overtakes is significantly higher for the rule-based approach and MOBIL. Since we applied the TTC-based overtaking decision to all strategies, the number of the maintaining decisions of the alternative driving strategies are same. 

18

*K. Ji et al. *

*Transportation Research Part C 150 \(2023\) 104109*

**Fig. 15. **Overtaking attempt and success rates under various scenarios for the proposed and rule-based methods. 

The results of the relaxed scenario show that the numbers of overtake successes for all approaches are nearly same, but the number of overtake failures for the rule-based approach and MOBIL are comparable to the number of maintain-decisions in our approach. It means that our approach does not attempt to overtake when overtaking failure is expected based on the global aggressive estimates of preceding vehicles. Although our approach’s maintain-decision in ambiguous situations can be a weakness, not attempting to overtake is better than failing to overtake. 

In terms of overtaking attempts and success rates, Fig. 15 illustrates the results of Fig. 14. As discussed, the attempt rates with the alternative decision-making strategies are always 100% in normal and relaxed scenarios and 70% in hard scenarios, but rates using our approach are quite low in harsh conditions \(i.e., Hard\). As expected, the success rates using our approach are much larger than those of the rule-based method and MOBIL for all cases. This is because there is a limitation that only considers the immediately preceding vehicle and the lane closing position in the overtaking lane, without the traffic state of multiple preceding vehicles. A bit higher success rate of the rule-based approach, when compared with the MOBIL, is due to the switching threshold *𝛥𝑎* th that makes MOBIL more conservative than the rule-based approach. 

**6. Conclusion**

This study proposes a hierarchical and game-theoretic decision-making approach for CAVs, with a focus on highway overtaking scenarios. In the proposed approach, the CAV globally estimates the driver aggressiveness of the preceding vehicles based on their historical trajectories obtained via V2X technologies at the upper layer, and refines the estimated driver aggressiveness during local interaction with a selected target vehicle at the lower layer. Moreover, during local interaction, a leader–follower game approach is employed to model and predict the target vehicle’s behavior. Through this hierarchical structure, appropriate overtaking decisions can be made when the benefit of an overtaking maneuver is not clear a priori. In simulation-based case studies of various scenarios, our approach outperforms rule-based decision-making in terms of success rates. As vehicle communication systems are increasingly adopted in recent years, it is expected that the proposed approach can be implemented in commercial CAVs and lead to improved CAV decision-making. 

Because actual human drivers are not involved in the simulation-based tests in this study, our future work will include the testing of the proposed decision-making approach in a human-in-the-loop environment. Meanwhile, the robustness of the proposed approach against various human drivers will be further investigated. 

**CRediT authorship contribution statement**

**Kyoungtae Ji: **Investigation, Methodology, Visualization, Writing – original draft, Writing – review & editing. **Nan Li:** Methodology, Investigation, Writing – review & editing. **Matko Orsag: **Writing review & editing, Methodology. **Kyoungseok Han:** Conceptualization, Funding acquisition, Project administration, Supervision, Writing review & editing. 

19

*K. Ji et al. *

*Transportation Research Part C 150 \(2023\) 104109*

**Declaration of competing interest**

The authors declare that they have no known competing financial interests or personal relationships that could have appeared to influence the work reported in this paper. 

**Acknowledgments**

This research was supported in part by Basic Science Research Program through the National Research Foundation of Korea \(NRF\), funded by the Ministry of Education \(NRF-2021R1A6A1A03043144\); in part by the NRF grant, funded by the Korean government \(MSIT\) \(NRF-2020K1A3A1A39112277 and NRF-2021R1C1C1003464\). 

**References**

Altché, F., de La Fortelle, A., 2017. An LSTM network for highway trajectory prediction. In: 2017 IEEE 20th International Conference on Intelligent Transportation

Systems. ITSC, IEEE, pp. 353–359. 

Ayres, T., Li, L., Schleuning, D., Young, D., 2001. Preferred time-headway of highway drivers. In: ITSC 2001. 2001 IEEE Intelligent Transportation Systems. 

Proceedings \(Cat. No. 01TH8585\). IEEE, pp. 826–829. 

Backhaus, S., Bent, R., Bono, J., Lee, R., Tracey, B., Wolpert, D., Xie, D., Yildiz, Y., 2013. Cyber-physical security: A game theory model of humans interacting

over control systems. IEEE Trans. Smart Grid 4 \(4\), 2320–2327. 

Bae, S., Saxena, D., Nakhaei, A., Choi, C., Fujimura, K., Moura, S., 2020. Cooperation-aware lane change maneuver in dense traffic based on model predictive

control with recurrent neural network. In: 2020 American Control Conference. ACC, IEEE, pp. 1209–1216. 

Başar, T., Olsder, G.J., 1998. Dynamic Noncooperative Game Theory. SIAM. 

Bhattacharyya, R.P., Senanayake, R., Brown, K., Kochenderfer, M.J., 2020. Online parameter estimation for human driver behavior prediction. In: 2020 American

Control Conference. ACC, IEEE, pp. 301–306. 

Claussmann, L., Carvalho, A., Schildbach, G., 2015. A path planner for autonomous driving on highways using a human mimicry approach with binary decision

diagrams. In: 2015 European Control Conference. ECC, IEEE, pp. 2976–2982. 

Colyar, J., Halkias, J., 2007. US Highway 101 Dataset. Technical Report FHWA-HRT-07-030, Federal Highway Administration \(FHWA\). 

Di, X., Shi, R., 2021. A survey on autonomous vehicle control in the era of mixed-autonomy: From physics-based to AI-guided driving policy learning. Transp. 

Res. C 125, 103008. 

Garzón, M., Spalanzani, A., 2019. Game theoretic decision making for autonomous vehicles’ merge manoeuvre in high traffic scenarios. In: 2019 IEEE Intelligent

Transportation Systems Conference. ITSC, IEEE, pp. 3448–3453. 

Han, K., Li, N., Tseng, E., Filev, D., Kolmanovsky, I., Girard, A., Improving autonomous vehicle in-traffic safety using learning-based action governor. Adv. 

Control Appl.: Eng. Ind. Syst. e101. 

Han, K., Nguyen, T.W., Nam, K., 2020. Battery energy management of autonomous electric vehicles using computationally inexpensive model predictive control. 

Electronics 9 \(8\), 1277. 

Hyeon, E., Kim, Y., Prakash, N., Stefanopoulou, A.G., 2019. Short-term speed forecasting using vehicle wireless communications. In: 2019 American Control

Conference. ACC, IEEE, pp. 736–741. 

Ji, K., Orsag, M., Han, K., 2021. Lane-merging strategy for a self-driving car in dense traffic using the stackelberg game approach. Electronics 10 \(8\), 894. 

Jovanović, D., Lipovac, K., Stanojević, P., Stanojević, D., 2011. The effects of personality traits on driving-related anger and aggressive behaviour in traffic among

Serbian drivers. Transp. Res. F 14 \(1\), 43–53. 

Kaysi, I.A., Abbany, A.S., 2007. Modeling aggressive driver behavior at unsignalized intersections. Accid. Anal. Prev. 39 \(4\), 671–678. 

Kesting, A., Treiber, M., Helbing, D., 2007. General lane-changing model MOBIL for car-following models. Transp. Res. Rec. 1999 \(1\), 86–94. 

Li, N., Girard, A., Kolmanovsky, I., 2019. Stochastic predictive control for partially observable Markov decision processes with time-joint chance constraints and

application to autonomous vehicle control. J. Dyn. Syst. Meas. Control 141 \(7\). 

Li, N., Kolmanovsky, I., Girard, A., Yildiz, Y., 2018. Game theoretic modeling of vehicle interactions at unsignalized intersections and application to autonomous

vehicle control. In: 2018 Annual American Control Conference. ACC, IEEE, pp. 3215–3220. 

Li, N., Oyler, D.W., Zhang, M., Yildiz, Y., Kolmanovsky, I., Girard, A.R., 2017. Game theoretic modeling of driver and vehicle interactions for verification and

validation of autonomous vehicle control systems. IEEE Trans. Control Syst. Technol. 26 \(5\), 1782–1797. 

Li, N., Yao, Y., Kolmanovsky, I., Atkins, E., Girard, A.R., 2020. Game-theoretic modeling of multi-vehicle interactions at uncontrolled intersections. IEEE Trans. 

Intell. Transp. Syst.. 

Liu, K., Asher, Z., Gong, X., Huang, M., Kolmanovsky, I., 2019. Vehicle Velocity Prediction and Energy Management Strategy Part 1: Deterministic and Stochastic

Vehicle Velocity Prediction Using Machine Learning. Technical Report, SAE Technical Paper. 

Liu, K., Li, N., Tseng, H.E., Kolmanovsky, I., Girard, A., 2022. Interaction-aware trajectory prediction and planning for autonomous vehicles in forced merge

scenarios. IEEE Trans. Intell. Transp. Syst.. 

Liu, K., Li, N., Tseng, H.E., Kolmanovsky, I., Girard, A., Filev, D., 2021b. Cooperation-aware decision making for autonomous vehicles in merge scenarios. In:

2021 60th IEEE Conference on Decision and Control. CDC, IEEE, pp. 5006–5012. 

Minderhoud, M.M., Bovy, P.H., 2001. Extended time-to-collision measures for road traffic safety assessment. Accid. Anal. Prev. 33 \(1\), 89–97. 

Myerson, R.B., 2013. Game Theory. Harvard University Press. 

Petrov, P., Nashashibi, F., 2014. Modeling and nonlinear adaptive control for autonomous vehicle overtaking. IEEE Trans. Intell. Transp. Syst. 15 \(4\), 1643–1656. 

Sadigh, D., Sastry, S., Seshia, S.A., Dragan, A.D., 2016. Planning for autonomous cars that leverage effects on human actions. In: Robotics: Science and Systems, 

Vol. 2. Ann Arbor, MI, USA, pp. 1–9. 

Sankar, G.S., Han, K., 2020. Adaptive robust game-theoretic decision making strategy for autonomous vehicles in highway. IEEE Trans. Veh. Technol. 69 \(12\), 

14484–14493. 

Sun, L., Cai, M., Zhan, W., Tomizuka, M., 2020. A game-theoretic strategy-aware interaction algorithm with validation on real traffic data. In: 2020 IEEE/RSJ

International Conference on Intelligent Robots and Systems. IROS, IEEE, pp. 11038–11044. 

Tian, R., Li, N., Kolmanovsky, I., Yildiz, Y., Girard, A.R., 2020. Game-theoretic modeling of traffic in unsignalized intersection network for autonomous vehicle

control verification and validation. IEEE Trans. Intell. Transp. Syst.. 

Treiber, M., Hennecke, A., Helbing, D., 2000. Congested traffic states in empirical observations and microscopic simulations. Phys. Rev. E 62 \(2\), 1805. 

Vahidi, A., Sciarretta, A., 2018. Energy saving potentials of connected and automated vehicles. Transp. Res. C 95, 822–843. 

Wang, Y., Gunter, G., Nice, M., Delle Monache, M.L., Work, D.B., 2020. Online parameter estimation methods for adaptive cruise control systems. IEEE Trans. 

Intell. Veh. 6 \(2\), 288–298. 

20





*K. Ji et al. *

*Transportation Research Part C 150 \(2023\) 104109*

Wang, M., Wang, Z., Talbot, J., Gerdes, J.C., Schwager, M., 2021. Game-theoretic planning for self-driving cars in multivehicle competitive scenarios. IEEE Trans. 

Robot. 37 \(4\), 1313–1325. 

Xie, T., Liu, Y., 2022. Heterogeneous traffic information provision on road networks with competitive or cooperative information providers. Transp. Res. C 142, 

103762. 

Yan, X., Radwan, E., 2007. Effect of restricted sight distances on driver behaviors during unprotected left-turn phase at signalized intersections. Transp. Res. F

10 \(4\), 330–344. 

Yoo, J., Langari, R., 2020. A stackelberg game theoretic model of lane-merging. arXiv preprint arXiv:2003.09786. 

Yu, H., Tseng, H.E., Langari, R., 2018. A human-like game theory-based controller for automatic lane changing. Transp. Res. C 88, 140–158. 

Yurtsever, E., Lambert, J., Carballo, A., Takeda, K., 2020. A survey of autonomous driving: Common practices and emerging technologies. IEEE Access 8, 

58443–58469. 

Zhang, Y., Antonsson, E.K., Grote, K., 2006. A new threat assessment measure for collision avoidance systems. In: 2006 IEEE Intelligent Transportation Systems

Conference. IEEE, pp. 968–975. 

Zhang, Q., Langari, R., Tseng, H.E., Filev, D., Szwabowski, S., Coskun, S., 2019. A game theoretic model predictive controller with aggressiveness estimation for

mandatory lane change. IEEE Trans. Intell. Veh. 5 \(1\), 75–89. 

**Kyoungtae Ji **received the B.S. degree in School of Mechanical Engineering at Kyungpook National University, where he is currently pursuing the master’s degree. He has strong research interest in the game theory, decision-making strategy of autonomous vehicles, and optimal path planning. 

**Nan Li **received the Ph.D. degree in Aerospace Engineering and the M.S. degree in Mathematics from the University of Michigan, Ann Arbor, MI, USA, in 2021 and 2020, respectively. He is currently an Assistant Professor with the Department of Aerospace Engineering at Auburn University, AL, USA. Prior to joining Auburn University, he was a Postdoctoral Research Fellow at the University of Michigan from 2021 to 2022. His research interests are in control and learning for safe autonomy, multi-agent systems, and intelligent transportation. 

**Matko Orsag **received his Ph.D. in 2015, M.S.E.E. in 2010 and B.S.E.E. in 2008 at the University of Zagreb, Croatia. He is currently an assistant professor at the University of Zagreb Faculty of Electrical Engineering and Computing \(UNIZG-FER\). 

As a researcher, he participated in several national and international research projects in the field of robotics, control, and automation. In 2011/2012, he worked as a visiting researcher at the Drexel University, Philadelphia, USA as a recipient of the Fulbright exchange grant. He authored and coauthored over 30 scientific and professional papers, including journal and conference papers, as well as a monograph and a book chapter in the field of unmanned aerial systems and robotics. His main areas of interest are autonomous systems, robotics and intelligent control systems. 

**Kyoungseok Han **received the B.S. degree in civil engineering \(minor in mechanical engineering\) from Hanyang University, Seoul, Korea in 2013 and the M.S. and Ph.D. degrees in mechanical engineering from the Korea Advanced Institute of Science and Technology \(KAIST\), Daejeon, Korea in 2015 and 2018. 

He was a research fellow at the University of Michigan from June 2018 to February 2020, and in March 2020 he was appointed assistant professor in the School of Mechanical Engineering at Kyungpook National University. His current research interests include modeling and control of autonomous vehicle, energy-efficient control of electrified vehicle, autonomy, and optimization techniques. 

21


# Document Outline

+ Hierarchical and game-theoretic decision-making for connected and automated vehicles in overtaking scenarios  
	+ Introduction 
	+ Problem Formulation  
		+ Vehicle Kinematic Model 
		+ Action Set 
		+ Observation Space 
		+ Simulated Traffic Environment 

	+ Drivers' Aggressiveness Estimation  
		+ Global Aggressiveness Estimation 
		+ Local Aggressiveness Estimation 

	+ Hierarchical Decision-Making Strategy for CAV  
		+ Reward Function Design 
		+ Global Decision-Making Strategy 
		+ Local Decision-Making Strategy 
		+ Overall Architecture of the Proposed Method 

	+ Case Studies  
		+ Correlation Between Driver Aggressiveness and Willingness of Yield 
		+ Simulation Environment 
		+ Alternative Decision-Making Strategies 
		+ Test Results 

	+ Conclusion 
	+ CRediT authorship contribution statement 
	+ Declaration of Competing Interest 
	+ Acknowledgments 
	+ References



