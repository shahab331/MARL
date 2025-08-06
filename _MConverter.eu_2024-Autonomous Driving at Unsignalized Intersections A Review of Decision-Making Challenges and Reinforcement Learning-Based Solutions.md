IEEE JOURNAL TEMPLATE , VOL. –, NO. –, AUGUST 2023

1

Autonomous Driving at Unsignalized Intersections: A Review of Decision-Making Challenges and Reinforcement Learning-Based Solutions Mohammad Al-Sharman, Member, IEEE, Luc Edes, Bert Sun, Vishal Jayakumar, Mohamed A. Daoud, Derek Rayside, Member, IEEE, and William Melek, Senior Member, IEEE

Abstract—Autonomous driving at unsignalized intersections is agent motion planning, in which the vehicle must react to still considered a challenging application for machine learning various different scenarios including the interaction with other due to the complications associated with handling complex multi-vehicles and traffic signals and signs \[8–10\]. Unlike highway agent scenarios characterized by a high degree of uncertainty. 

autonomous driving \[11–13\], driving in urban environments Automating the decision-making process at these safety-critical environments involves comprehending multiple levels of abstrac-requires effective handling of complex multi-agent scenar-tions associated with learning robust driving behaviors to enable ios with a high level of uncertainty and occlusions \[14–

the vehicle to navigate efficiently. In this survey, we aim at ex-

17\]. More specifically, driving at intersections is considered ploring the state-of-the-art techniques implemented for decision-perilous for most human drivers. This can be justified by making applications, with a focus on algorithms that combine looking at the data reported in \[18\]. The Fatality Analysis Reinforcement Learning \(RL\) and deep learning for learning traversing policies at unsignalized intersections. The reviewed Reporting System \(FARS\) and National Automotive Sampling schemes vary in the proposed driving scenario, in the assumptions System General Estimates System \(NASS-GES\) provide an made for the used intersection model, in the tackled challenges, estimation that 40% of the crashes recorded in the US in and in the learning algorithms that are used. We have presented 2008 occurred at intersections. They reasoned that among comparisons for these techniques to highlight their limitations the factors contributing to these crashes, the most prevalent and strengths. Based on our in-depth investigation, it can be discerned that a robust decision-making scheme for navigating were related to the crash-involved drivers, namely, their age, real-world unsignalized intersection has yet to be developed. 

gender and driving behaviour. Hence, deriving safe policies for Along with our analysis and discussion, we recommend potential autonomous vehicles that allow for safe crossing behaviour at research directions encouraging the interested players to tackle intersections has been a topic of a profound importance as it the highlighted challenges. By adhering to our recommendations, can provide useful guidelines for designing preventive crash-decision-making architectures that are both non-overcautious and safe, yet feasible, can be trained and validated in real-world mitigation schemes. Recently, academia and industrial partners unsignalized intersections environments. 

have been extensively testing the most advanced autonomous technologies on their platform to ensure safe and efficient Index Terms—Autonomous driving, decision-making, unsignalized intersections, deep reinforcement learning, deep learning, urban driving \[19–23\]. 

Driver Intention Inference, model predictive control, transfer Decision-making in autonomous vehicles is represented in a learning. 

hierarchical complex structure \[24\], covering a range of stages and sub-tasks which include the following: \(i\) planning where I. INTRODUCTION

to go next, \(ii\) making decisions in the short and long term arXiv:2409.13144v1 \[cs.RO\] 20 Sep 2024 FOLLOWING the Defense Advanced Research Projects time frames based on the on-board sensors observations, \(iii\) Agency \(DARPA\) Urban Driving Challenge \(UDC\), held decisions influenced by the interaction with other agents in in 2007, the research community has been encouraged to the same environment, \(iv\) ensuring safe and robust vehicle develop novel technologies to address technical and social control, \(v\) learning from the driving history and naturalistic challenges concomitantly with driving in urban settings au-human driving styles, \(vi\) coordinating with other vehicles to tonomously \[1–7\]. These challenges stem from the nature perform certain tasks collectively. However, within the context of urban driving itself, characterized by its complex multi-of urban intersections, enabling an autonomous vehicle to navigate safely and efficiently in such complex environments M. Al-Sharman and D. Rayside are with the Department of Electrical and requires a high degree of autonomy, according to the So-Computer Engineering and with Watonomous \(Waterloo autonomous vehicle ciety of Automotive Engineers \(SAE\) J3016 standard \[25\]. 

team in the SAE AutoDrive Challenge. \(Watonomous.ca\)\), University of Waterloo, Waterloo, ON, N2L 3G1, Canada, e-mail: mkalsharman@uwaterloo.ca, Nonetheless, the current automated vehicles, even the fully drayside@uwaterloo.ca. 

autonomous ones, cannot fully navigate safely at all times, and L. Edes is with David R. Cheriton School of Computer Science and with cannot guarantee crash-free maneuvers due to critical decision-Watonomous\), University of Waterloo, ON, CA. 

B. Sun is with the Faculty of Mathematics in the Department of Combina-making errors \[26, 27\]. 

torics and Optimization, and with Watonomous\), University of Waterloo, ON, Making decisions at unsignalized intersections is a highly CA. 

intractable process. The complex driving behaviour and the Vishal Jayakumar, Mohamed A. Daoud, and W. Melek are with the Department of Mechanical and Mechatronics Engineering and with Watonomous\), disappearance of traffic control signals make the motion infer-University of Waterloo, ON, CA. 

ence of other intersection users highly-challenging \(see Fig.1\)





IEEE JOURNAL TEMPLATE , VOL. –, NO. –, AUGUST 2023

2

Learning \(ML\) approaches \[38\]. Rule-based approaches use safety intersection metrics, namely time-to-collision \(TTC\), to generate distance-based traversing rules. However, engineering such rules to adapt with various possible crossing situations is a tedious process due to the large number of rules which need to be tuned. ML-based approaches, especially reinforcement learning approaches, focus on learning driving policies from the interaction between the vehicle and the intersection environment. 

Applying modern RL-based approaches for learning optimal \(a\) 4-way

\(b\) Junction merge

driving policies at unsignalized intersections has been studied extensively in the literature. Researchers have been motivated to develop these algorithms, owing to their capabilities in handling partially-observable environments by training its data-driven models based on mapping the environmental observations into actions \[39\]. Nevertheless, design challenges behind developing crash-free intersection maneuvers and deploying them in real driving environments still need to be overcome. 

The surveyed schemes still suffer from several problems,i.e, the proposed design assumptions, the scalability of the proposed scheme to deal with more challenging urban driving \(c\) T-junction

\(d\) Roundabout

scenarios, and the experimental validation in real urban driving Fig. 1: Different types of unsignalized intersections. These settings. Hence, motivated by the published works, a review of images are generated using SUMO \(Simulation of Urban the current and emerging trends in aspects related to decision-MObility\) traffic simulation software. 

making in urban unsignalized intersections is recommended to lay the groundwork for potential advancement in this research direction. This survey offers an overview of algorithms and

\[28–30\]. The non-stationary problem, along with the large applications of decision-making in urban autonomous vehicles partially-observable state space of agents dictate designing at unsignalized intersections, with the goal of continuing to robust algorithms for safe intersection-traversal \[31\]. Numer-explore methods to boost automation and enhance safety ous studies have been conducted to investigate algorithms to at these complex environments. Fig.2 highlights the main improve driving safety at unsignalized intersections. These decision-making challenges and their corresponding solutions algorithms have been introduced to tackle two main problems; surveyed in this paper. 

inferring the intention of other intersection users and motion In comparison to existing survey papers on RL for au-planning under uncertainty. We shall be discussing these tonomous vehicles, our review uniquely focuses on RL-algorithms with technical depth in the subsequent sections. 

based decision-making techniques specifically for unsignal-Based on our thorough investigation, we found that the pro-ized intersections-an area that has not been comprehensively posed decision-making algorithms can be classified into three covered in the literature. Previous works, such as those by main categories: cooperative approaches, including game-Irshayyid et al. \[40\], and Aradi \[41\], explore RL applications theoretic, heuristic-based approaches and hybrid approaches in highway control, and motion planning, respectively, but they which combine multiple classes of these algorithms for han-do not address the unique challenges posed by unsignalized dling the unsignalized intersection problem. Cooperative ap-intersections. Other more recent surveys, like those by Chen proaches entail the use of V2V communication technology to et al. \[42\] and Wu et al. \[43\] , focus on RL for path planning exchange the states between the subject vehicle and other in-and for behavior planning, yet they also do not tackle the tersections users \[32–34\]. However, such technology is still an specific decision-making challenges inherent to unsignalized active area of research and has not been sufficiently developed intersections. Additionally, a survey by Zhang et al. \[44\]

to allow its application in existing decision-making schemes. 

provides an overview of RL-based control for signalized Game-Theoretic-Based algorithms were adopted to model the intersections, which involves different complexities compared vehicles’ interactions in unsignalised intersections \[35, 36\]. 

to unsignalized intersections. Our manuscript fills this critical These game-theoretic based approaches assume that the states gap by offering a detailed review of RL-based decision-making of the interacting vehicles are observed by the subject vehicle, approaches for unsignalized intersections, highlighting their which allows for predicting their future trajectories and then limitations, challenges, and potential future research direc-plan its own. However, this assumption is not likely to hold tions. This contribution provides a fresh perspective that is for current real-life decision making at unsignalized inter-valuable for advancing autonomous driving in complex, real-sections. Heuristics-based approaches have been engineered world scenarios. 

to tackle safety-oriented problems associated with traversing To define the theme of this survey clearly, we direct our urban intersections \[37\]. Researchers commonly classify these attention towards various aspects related to behavioral motion approaches into two main groups: rule-based and Machine planning for autonomous vehicles at unsignalized intersec-

IEEE JOURNAL TEMPLATE , VOL. –, NO. –, AUGUST 2023

3

**Challenge1: Unknown driver intentions** driving scenarios. 

To summarize, the rest of this paper is split into five ** Solutions** sections as follows. Section II represents the background of Driver Intention Inference \(DII\) techniques: this work, where we elaborate on aspects related to decision-

- **Index-based**: TTI, TTS, PRT, RDP. 

making in autonomous vehicles and reinforcement learning. 

- **Learning-based**: 

Section III illustrates the challenges and learning-based so-Classical ML: SVM, HMM, GP, DBN. 

lutions decision-making schemes with our observations on **DL**: RNN, LSTM, GNN, Bi-LSTM, 

their inherent logic highlighted. Section IV presents remarks Temporal CNNs. 

on possible future research directions. Finally, Section V

concludes the proposed and future works. 

II. BACKGROUND

**Challenge2: Decision-making design **

A. Overview of decision-making in Autonomous Vehicles A. **Partial Observability. **

Autonomous vehicles \(AVs\) are considered autonomous **Solutions:** 

decision-making systems as they provide continuous decisions Intention-aware algorithms. 

based on processing perceptual observations. Along with these Occlusion-aware algorithms. 

observations and sensor models, the predefined road network DRL Techniques. ** **

data, driving rules and regulations, dynamic behaviour of B. **Training in Continuous action spaces. **

**Solutions: **

the vehicle, are utilized for predicting the vehicle’s motion DDPG,TD3, SAC, 

and generating low-level control commands autonomously. 

MEDDPG, PPO, TRPO

Developing such decision-making systems with a high de-C. **Training in high-dimensional spaces. **

gree of autonomy, is commonly organized by a well-defined **Solutions: **

multi-staged process \[24\]. However, the greatest challenges of HRL, CL, RNN, LSTM, 

motion planning in urban autonomous driving environments Attention-based, GPT-based, LfD

comprise the following factors: i\) restricted sensing capabilities, specifically, vision and proximity in the time-varying environment; ii\) cluttering and occlusions in the scene which Fig. 2: Surveyed decision-making challenges and solutions. 

impede achieving accurate perception; iii\) legal and technical constraints on the vehicle’s response, arising from the driving rules and regulations. 

tions. To be more specific, we focus this review on learning-The hierarchy of the decision-making processes of urban based decision making schemes with a greater attention to autonomous vehicles is introduced in \[48\]. As shown in algorithms that combine the recent advances of RL and deep

Fig.3, it consists of four cascaded layers, starting with the learning for learning driving policies at unsignalized intersec-high-level route planning, followed by the behavioural and tions. However, decision-making based on imitation learning motion planning layers, and the low-level feedback control or vehicle-to-vehicle \(V2V\) communication, in a connected completes the scheme. At the very top layer, given the pre-driving fashion, is out of proposed survey’s scope. Using defined destination, the autonomous decision-making system V2V communications \[45, 46\] can be a potential solution for runs inherent route planning algorithms to compute the optimal anticipating vehicle behaviour and transferring it to the ego path using the road network as a network graph. In this vehicle. However, for this solution to be fully viable, vehicular layer, the edge weights are summed in order to effectively communication and connected vehicle technologies must be solve for the routes with minimum cost. However, as the widely deployed. It should be noted that the vehicle-pedestrian road network becomes larger, its graph network also becomes interaction behavior is not covered in this proposed research. 

more complex making the use of the classical route planning However, the reader is referred to a recent survey on pedestrian schemes, namely Dijkstra \[49\] and A\* \[50\], inefficient as trajectory prediction \[47\]. 

the search time may exceed seconds \[51\]. Intelligent route The main contributions of this survey paper can be stated planning approaches have been introduced for transportation as follows. First, an organised and in-depth state-of-the-art efficiency enhancement. Advanced Deep Learning and Internet literature survey for decision-making at unsignalized inter-of Things \(IoT\) technologies have been employed for efficient sections is proposed, highlighting the main navigational chal-route planning in complex urban transportation \[52, 53\]. Once lenges and cutting-edge learning-based solutions. Second, an the optimal route has been defined, the next layer is focused exploration of the Driver Intention Inference \(DII\) schemes on behavioral path planning. This layer is responsible for at unsignalized intersections is carried out, with the goal of choosing proper driving behaviour based on the observed identifying key remarks for better handling the large partially-behaviour of other road drivers, traffic signals and road surface observable state space of the problem. Finally, based on the conditions. This behavior enables the AV to interact with road in-depth investigation, limitations of the published learning-participants while performing lane changing, lane following, based decision-making frameworks are identified and potential and other more complicated tasks like intersection traversal. 

research directions are suggested to achieve better generaliza-For instance, choosing a cautious behavior for intersection-tion characteristics of the trained traversing policies in real-life traversal maneuvers based on the road conditions is a re-

IEEE JOURNAL TEMPLATE , VOL. –, NO. –, AUGUST 2023

4

Route

Behavioural

Motion

Local

assessment is an estimate used to anticipate the free distance Planning

Path Planning

Planning

Feedback control

between the leading and trailing vehicles. Gap distance-based and time-to-collision \(TTC\) algorithms have been proposed Fig. 3: Decision-making processes in urban autonomous for traversing intersection \[55, 56\]. However, these simple vehicles. 

approaches require laborious parameter-tuning to deal with different intersections scenarios. Given the locations of the sponsibility of the behavioral path planner. The planner will subject vehicle, a threat assessment process is usually con-govern the approach, stopping, creeping and the intersection ducted to anticipate the potential threats of other road par-traversing maneuvers. Moreover, it will take into account ticipants \[57\]. In \[58\], by inferring the intention of the road the uncertainty associated with the intentions of other road participants, threat predictions were obtained using random drivers and pedestrians which may generate multiple possible decision trees and particle filtering. A survey on the threat trajectories. The problem of intention inference and its integra-assessment technologies and state-of-the-art approaches can tion with the behavioral path planning schemes is discussed be found in \[59\]. A risk assessment approach is used to detect in greater detail in III. After the driving behavior has been risky scenarios which are related to the limited capabilities of determined by the behavioral path planner, this behaviour the perception sensors or occluded environment which may has to be mapped into a vehicle’s trajectory which will be result in incorrect decisions \[60\]. Risk assessment is usually tracked by the local feedback controller. Different aspects must coupled with predictions about the intention of other road be taken into account while choosing the proper trajectory participants. Intention-aware risk assessment has been done \(e.g. It must be feasible with safety guarantees given the extensively to evaluate maneuvers at occluded intersections vehicle’s dynamic model constraints\). Finding such trajectory with limited perception capabilities. For detailed risk assessis an inherent component that must be accounted for by the ment at unsignalized intersection, the reader is referred to motion planning layer. Finally, to execute this trajectory, a Section III-B which describes the state-of-the-art approaches feedback controller must be designed to provide the correct of risk assessment for decision-making at urban intersections. 

input to govern the planned motion and compensate for the Based on the environmental observations collected, conflict tracking errors arising from the assumptions made on the assessment is concerned with predicting the potential conflict utilized vehicle dynamic model. For more details related to scenarios of two or more vehicles that are going to collide low-level feedback controllers, the reader is referred to the if their movements remained unchanged \[61\]. Lastly, accident comprehensive survey conducted by Paden et al. \[48\]. 

assessment is based on conducting precise analysis using data B. Modeling the decision-making problem mining and machine learning techniques to make predictions Several research works have envisaged the decision-making that help in preventing crashes \[62\]. 

problem at intersections as a reinforcement learning problem, D. RL Approaches

where the agent and the environment interact continuously to 1\) Preliminaries

learn an optimal policy that governs the vehicles’ motion. The agent takes an action and the environment responds to this Reinforcement learning is a group of algorithms that focus action and present new scenarios to the agent. A Markov De-at learning optimal policies via performing iterative experi-cision Process \(MDP\) is used to describe the environment for ments and evaluations for the sake of self-teaching overtime the RL problem \[38\], where we assume that the environment to achieve a specific goal. RL can be distinguished from other for this specific problem is fully observable. Technically, MDP

learning techniques such as supervised learning because the is described as a tuple \{S, A, R, T, γ\} in which S represents labels are timely delayed. The aim of RL is to learn an optimal the observed states. These states may include information policy π which in charge of mapping the system states to about the ego vehicle and states of other vehicles crossing control inputs that can maximize the expected reward J \(π\). 

the intersection. Among these states, velocities, position, and In eq. \(1\), the reward rt indicates how successful the agent states related to the geometry of the intersection. A and T

was at a given time step t. For instance, large rt values are represents the set of actions and the transition function that given when the agent is close to the desired trajectory, while maps state-action pairs to a new state. The immediate reward small rt values are given when large deviations occur \[63\]. 

is defined by the reward function R, whereas γ represents the The discounted accumulated reward is given as discount factor for long-term rewards. 

" ∞

\#

In occluded intersections where the environment is not fully X

J \(π\) = E

γtrt | π

\(1\)

observed due to limited sensor range, occlusions in the scene, t=0

or uncertainty related to the pedestrians/ drivers intentions, a Partially-Observable Markov Decision Process \(POMDP\) is The discount factor γ, where γ ∈ \[0, 1\], is used to adjust adopted to model these types of intersections. These cases whether the agent is far-sighted or short-sighted. The desired shall be discussed in more detail in Section III. 

policy can be described as

C. Safety Assessment at Intersections

At high-level decision-making, drivers perform safety as-π∗ = arg max J \(π\)

\(2\)

π

sessment to avoid crashes and potential hazards. Shirazi et al. 

\[54\] introduces five topics pertaining the safety assessment at The value of the state x, is evaluated by calculating the intersections: Gap, Threat, Risk, Conflict and Accident. Gap expected return starting from x and, subsequently, governed





IEEE JOURNAL TEMPLATE , VOL. –, NO. –, AUGUST 2023

5

by policy π

" ∞

\#

Approaching

X

V π\(x\) =

Vehicle

E

γtrt | x0 = x, π

\(3\)

t=0

where V π \(xt\) is defined by \[64\] as the value function. 

Similarly, the action value in state x is evaluated by calculating the expected reward starting from the action u in a state x and, subsequently, following policy π

" ∞

\#

X

Qπ\(x, u\) = E

γtrt | x0 = x, u0 = u, π

\(4\)

t=0

Ego Vehicle

where Qπ \(xt, ut\) is defined as the action-value function. 

Modern machine learning algorithms, driven by advance-Unobservable Driver's Intention

ments in deep learning, have integrated Reinforcement Learn-Longitudinal Uncertainty

ing \(RL\) principles in the form of Deep Reinforcement Learn-Sensor Uncertainty

ing \(DRL\) \[65, 66\]. Model-free RL learners are employed Stochastic interaction 

to sample the MDP to infer information about the unknown model. Given DRL’s strengths in handling partially observable Fig. 4: An intersection-traversal scenario where the ego vehicle environments with large state spaces and providing continuous is required to handle several sorts of uncertainties associated action outputs, several DRL architectures have been developed with the approaching vehicle. 

to learn optimal policies for unsignalized intersection navigation \[67, 68\]. In this review, we examine these approaches in detail and discuss their specific applications in subsequent Considering these uncertainties when designing learning-sections. 

based decision-making schemes in a complex intersection III. U

environment is essential for the ego vehicle to traverse in-NSIGNALIZED INTERSECTION-TRAVERSAL:

C

tersections safely. For example, predicted motion and future HALLENGES AND SOLUTIONS

trajectories of the target vehicles \[73\], which share potential To enhance the AVs’ ability to navigate complex urban conflict points with the ego vehicle need to be incorporated unsignalized intersections, major technical challenges need to while solving for an optimal traversal policy of the ego vehicle. 

be investigated. In this section, we survey these challenges that This policy needs to be optimized for the most probable future arise while designing an automated learning-based decision-scenarios coming from stochastic and interactive motion mod-making algorithm for traversing these safety-critical environ-els of the other target vehicles. Considering these scenarios, ments. 

in real time settings, these policies allow the autonomous A. Autonomous Driving Under Uncertainty vehicle to incorporate the estimated change in future prediction The uncertainty associated with motion prediction of other accuracy in the optimal policy \[74\]. This yields a compact intersections vehicles at unsignalized intersection is caused by representation with reduced-dimensions state-space the following factors \[31\]:

Based on our observation, we found that researchers have

• Unknown intention of intersection users. The motion been mainly focusing at developing learning-based frame-of other intersection participants is highly connected to works to tackle two main technical problems; inferring the the future trajectory of the ego vehicle \[69\]. Hence, for intention of the intersection users and designing the decision safe intersection navigation, precise motion predictions process. Hence, in sections III-B and III-C, we focus on of the intersection users must be obtained. The main exploring the published works on these problems with greater difficulty with inferring intention arises from the intrinsic details. 

uncertainty in the unknown current states and hidden B. Driver Intention Inference Challenge variables, namely, unknown final destinations as well as Accurately inferring and forecasting the intentions of drivers their unforeseeable future longitudinal path \[70\], and their at unsignalized intersections is crucial for addressing the likelihood of interaction with the subject vehicle \[71\]. 

cause of an accident and ensuring road safety in such diverse

• Noise characteristics of sensors’ observations. The multi-agent environments. Several research efforts have been noise associated with the measurements collected from exerted in order to develop algorithms for DII applications. 

the mounted sensors adds another layer of uncertainty to These algorithms tackle the intention inference problem as a the decision-making problem. 

classification problem where intentions are classified based on

• Occluded environments and limited perception. The the driving behaviour \[75, 76\]. These DII approaches can be ability to observe the scene accurately is hindered by classified into two groups: index-based and learning-based. In environmental obstructions and occlusions. \[72\]. 

index-based approaches, safety metrics are utilized to examine

Fig.4 depicts an illustrative example of where these uncer-driving behaviors at intersections in order to formulate risk tainties originate from at a four-way unsignalized intersection. 

assessment schemes. For example, time-to-intersection \(TTI\), 

IEEE JOURNAL TEMPLATE , VOL. –, NO. –, AUGUST 2023

6

time-to-stop \(TTS\), time-to-collision \(TTC\), Perception Re-of the subject vehicle. Girma et al. \[85\] introduced the use of action Time \(PRT\), Required Deceleration Parameter \(RDP\), Bidirectional LSTM with an attention mechanism for intention along with brake application were taken into account for infer-inference at unsignalized intersections based on sequence-toring the driver’s intent at intersections \[77, 78\]. These index-sequence modeling principles \(i.e. Surrounding vehicles tra-based approaches, however, are designed for only frontal-crash jectory analysis with recurrent neural networks\). Bidirectional prevention systems, where, in real driving scenarios, careless LSTM is used due to its capability for exploring information drivers may collide with the ego vehicle from different an-from previous and future time steps. However, the proposed gles. Classical machine learning \(ML\) classification techniques method is agnostic to the decision-making problem. Thus, have been also employed for intention inference applications. 

integrating the proposed method with decision-making scheme For instance, Aoude et al. \[57\] proposed a Support Vector in real-time format is a research direction to be explored. 

Machine-based \(SVM\) intention predictor that was developed More recently, Pourjafari et al. \[86\] proposed a LSTM-based as part of the proposed threat assessor scheme. Subsequently, intended exit predictor that predicts the intended exit path of the developed threat assessor warns the host vehicle with surrounding vehicles as they approach the intersection, given the identified threat level and advises the best escape path. 

their dynamic states, namely position, velocity and heading. 

Hidden Markov Models \(HMM\) were implemented for in-The intended exit predictor is integrated with GNN-based tention inference along with Gaussian Processes which were models to predict the sequence of vehicles traversing each used for collision risks prediction of multiple dynamic agents collision point in the intersection and the approximate time

\[79\]. Lefevre et al. \[80\] reported using a Dynamic Bayesian window the subject vehicle requires to cross the collision Network \(DBN\) for developing a probabilistic motion model point. 

where intentions are estimated from the joint motion of the Table I summarizes the surveyed deep-learning-based inten-vehicles. However, these ML-approaches fall short as they tion inference schemes highlighting their research objectives cannot capture the long-term temporal dependencies in the and significant remarks. 

data. 

Motivated by their efficacy in modelling sequential tasks, researchers have employed deep-structured Recurrent Neural C. Decision Making Challenge

Nets \(RNN\) for determining the intentions of drivers at non-Owing to the strengths of deep-structured neural networks signalized intersection. Zyner et al. \[81\] introduced the use in handling large partially-observable state-action space, ma-of long short-term memory \(LSTM\) for intention inference jor research directions have been followed aiming to de-at unsignalized intersections. Observations on the dynamic velop learning-based schemes for tackling problems related states, namely, position, velocity and heading states, were to traversing unsignalized intersections autonomously. In this captured by the on-board set of sensors and used to train section, we present the main design challenges involved in the network. In \[82\], a group of 104 features were utilized developing learning-based algorithms for decision-making un-from the NGSIM dataset to train the proposed LSTM-based der uncertainty, as well as a review of relevant state-of-the-art intention classifier. These features encompass ego position solutions, emphasising key observations and shortcomings. 

and dynamics, surrounding vehicles and their past states, and 1\) Partial Observability

rule features that highlight what legal actions can be taken In real multi-agent autonomous driving settings, the agents in the current lane. The proposed method demonstrated high have incomplete information about the environment with classification accuracy for intention prediction at intersections which they interact. Therefore, designing a robust decision-with different lanes or shapes. However, these methods rely making framework in such environments is considered an heavily on the mounted on-board positioning/tracking system. 

intractable problem. In practice, such problems are typically This means that tracking data from GPS and Inertial Mea-modelled as \(POMDPs\), in which a driving policy is learned surement Units \(IMUs\) are required in order for the system to provide safe actions while accounting for the stochasticity to operate effectively, restricting their usage to vehicles where inherent in the process of inferring intention and motion streaming from these sensors is available. Zyner et al. \[83\]

planning \[93\]. Numerous works address the problem of mod-proposed a solution to this problem by using data from a eling the decision-making process of the partially-observable Lidar-based tracking system which will be implemented in driving environments at unsignalized intersections. Brechtel et future intelligent vehicles. The proposed model was validated al. \[94\] models the decision-making problem for navigating an using a large naturalistic dataset which was collected from two occluded T-junction intersection as a POMDP. Uncertainties of days of driving at an unsignalized roundabout intersection. 

the driver’s behavior and the limitations of the perception of Recently, Jeong et al. \[84\] proposed an LSTM-based archi-the environment were taken into consideration while solving tecture for predicting the target vehicle’s intention based on the continuous POMDP. Sezer et al. \[95\] develops a mixed their estimated future trajectory at unsignalized intersections. 

observable MDP \(MOMDP\) model, which is a variant of This network was developed to study long-term dependencies POMDP, for intention-aware motion planning at a T-junction between vehicles in complex multi-lane turn intersections, and intersection under the uncertainty of drivers intentions. Along was based on the previous sequential motion of the target with the unknown intentions of other drivers, their unknown vehicles measured by the sensors equipped with the AV. The future predictions in the longitudinal direction and their in-predicted target motion is integrated with Model Predictive teraction with the ego vehicle are modeled in the proposed Control \(MPC\) which is responsible for planning the motion decision scheme in \[31\]. The problem is formulated as a

IEEE JOURNAL TEMPLATE , VOL. –, NO. –, AUGUST 2023

7

TABLE I: Summary of the covered Deep-learning-based intention inference schemes in this section Reference

Objective

Method

Remarks

\[81\]

Intention inference based on the ego ve-RNN

•

100 % classification accuracy on the

hicle’s observations i.e. GPS, IMU and Naturalistic Intersection Driving Dataset Odometry\). 

\[87\]. 

\[82\]

Intention inference at multi-lane intersec-LSTM

• 85% accuracy at intersections with dif-tion based on observations of speed, lanes ferent types and shapes \(NGSIM\) dataset. 

and six adjacent vehicles. 

\[83\]

Intention inference for ego vehicles with-LSTM. 

•

The results indicate that networks fed out tracking data \(GPS, steering wheel with more history up to 0.6 seconds per-encoding\). 

form better. 

• The provided model gives 1.3 sec prediction window prior to any potential conflict. 

\[84\]

Intention inference based on GPS, Lidars LSTM

• Based on the prediction results, longitu-and different types of cameras \(front and dinal motion planning with safety guaran-round views\). 

tees is proposed using MPC . 

\[85\]

Intention Inference based on focusing on Bidirectional

•

Sequence to sequence modeling is

important time-series vehicular data. 

LSTM

with

performed to map the input sequence of attention

observation to a sequence of predicted mechanism. 

driver’s intentions. 

•

Achieved high accuracy on the NDS

dataset. \[88\]

\[89\]

Intention inference for maneuver predic-LSTM

• A prediction window of 3.6s has been tion at intersection based real driving se-achieved on RoadLab dataset \[90\]. 

quences including vehicle dynamics, gaze data as well as head movements. 

\[91\]

Intention inference for Path prediction us-Temporal CNN

• Outperforms ML-LSTM and LSTM-FL

ing dilated convolution networks in con-in terms of accuracy and computational junction with a mixture density network complexity on ACFR dataset. 

\(MDN\) considering the temporal aspects of driving data. 

\[86\]

Intended exit path prediction based on lo-LSTM

• Intended exit predictor achieved 94.4%

cation and speed of vehicles at unsignal-accuracy on INTERACTION dataset \[92\]. 

ized intersection

POMDP where the solution of the POMDP is a policy deter-which can guarantee that the vehicle can traverse urban mining the optimal acceleration of the ego vehicle. However, intersections under multiple occlusions and perception faults. 

the scalability of the proposed scheme to deal with unknown Empirically, an ablation study was conducted showing that intentions of oncoming vehicles from multi-directions has not the proposed approach exhibits superiority over conventional been addressed. 

DQN methods. A Deep Distributional Q-learning algorithm was proposed to deal with uncertainties associated with the Inspired by the strengths of Deep Reinforcement Learning variety of human driving styles \[99\]. The algorithm generates \(DRL\) approaches in learning driving policy without the risk-sensitive actions based on offline distribution learning and necessity to learn the MDP model itself, several works have online risk assessment. During the offline distribution learning, recently adopted these methods to solve the designed MDPs. 

the distributions of the risk-neutral and state–action return are For instance, Isle at el. \[96\] proposed a safe reinforcement learnt from unknown behavior type of a participant sampled learning algorithm for left turn intersection-traversal using from a known environment. While the learned behaviour is action prediction techniques. An optimal policy is trained being executed, the action risks \(collisions\) are quantified using deep Q-learning to minimize disruption to traffic which using distortion risk metrics where the optimal action can be is measured by traffic braking and maximize the distance then selected. Hoel et al. \[74\] introduced a method to evaluate to other vehicles. To solve for an optimal policy in such the uncertain actions \(decisions\) made by the agent in an a multi-agent environment, the problem was formulated as unsignalized intersection environment. A Bayesian reinforce-a Stochastic Game. Deep Q-learning Networks \(DQN\) have ment learning method using an ensemble of neural nets with been used for solving intersection crossing problems modeled Randomized prior Functions \(RPF\) \[100\], has been introduced by POMDPs \[97\]. A thresholded lexicographic Q-learning to estimate the distribution of Q-values which are then utilized scheme was adapted to the deep learning framework. This al-to estimate the action values. This proposed scheme shows gorithm mimics human driving in some challenging scenarios robustness in identifying highly uncertain actions within and where safety is prioritized over traffic rules and ride comfort. 

outside the training set which helps in choosing the safest A factored MDP model was utilized instead of full MDP to actions for safe intersection traversing maneuvers. However, mimic the human driver behaviour and to improve the data these proposed approaches fall short in terms of the proposed efficiency. A SUMO traffic simulator was then used as the hard assumptions and the tailored intersection-traversal sce-simulation environment to validate the proposed experiment. 

narios. 

Given the limitation of the Deep Q-Network, Bouton et al. 

\[98\] introduced an integration of the POMDP planning, model-The development of robust DRL algorithms for better checking and reinforcement learning to derive safe policies handling of POMDP problems has piqued the interest of many

IEEE JOURNAL TEMPLATE , VOL. –, NO. –, AUGUST 2023

8

researchers in the field. Zhu et al. \[101\] introduced a scheme making algorithms were developed to control the motion called Action-specific Deep Recurrent Q-Network \(ADRQN\) under the unknown intentions of intersection participants. For to improve the learning capability in partially-observable en-instance, a continuous Hidden Markov model \(HMM\) was vironments. A fully connected \(FC\) layer is utilized to encode developed to infer the high-level motion intentions including actions which are coupled with their corresponding observa-turning and continuing straight \[105\]. A POMDP was then tions to form action-observation pairs. LSTM is then adopted designed for the general decision-making framework, with to process the time series of action-observation pairs. Similar assumptions and approximations used to solve the POMDP

to the conventional DQNs settings, the FC layer calculates the by calculating a policy to perform the optimal actions. Online Q-Values based on the latent states learnt by the LSTM net-solvers have also been used to solve the formulated POMDPs work. Another LSTM-based Deep Recurrent Policy Inference of the decision-making. In \[106\], an improved variant of the Q-networks \(DRPIQN\) was also introduced to handle partial POMCP solver which is called The Adaptive Belief Tree observability caused by imperfect and noisy state information \(ABT\) is used to solve the proposed POMDP of an intention-in real-world settings \[102\]. Both ADRQN and DRPIQN net-aware left turning problem. The proposed decision-making works outperform other deep Q-learning techniques in terms problem is based on mimicking the human behavior of creep-of learning capabilities and stability when applied to a number ing slowly, upon reaching the stop line, to better understand the of games. As an application to unsignalized intersection, Qiao driver’s intention. The left-turn trajectory is simply assumed et al. \[103\] proposed a network based on the design concepts as a straight line with quarter circle curve. However, the of ADRQN and other deterministic gradient policy approaches intentions of the oncoming vehicles from only one direction is for generating continuous time actions from the previous ob-taken into consideration. In \[107\], the uncertainties associated servations of the earlier steps. Observations from the previous with human behavior of other drivers on the road in the context 20 steps were used as inputs for the LSTM Network. Figure of an intersection have been modeled as a POMDP. An online

5 exhibits the developed LSTM-Network which handles the solver has been utilized to find the optimal action that can be POMDP and represents the decision-making problem of a taken by the vehicle to react to uncertain situations \[107\]. 

four-way stop unsignalized intersection. The action output for However, aside from a lack of real-world experimentation, each time step is obtained based on the observation inputs using online solvers to solve is impractical because they only to the first LSTM and FC layers of the network at each work for relatively small state spaces, and the complexity of individual time step. Subsequently, the Q-values are generated solving the POMDP scales fairly quickly. Deep Reinforcement by taking the action of the previous step at−1 along with Learning, on the other hand, can work with much larger, or observation of the current step Ot as an input to the second even large and continuous spaces, such as Atari \[104\]. 

LSTM and FC layers. However, these approaches are entirely Recently, Wang et al. \[108\] employ Monte Carlo simula-model-free as they rely heavily on the LSTM network to tions within a Deep Reinforcement Learning \(DRL\) frame-remember the past instead of having true belief states. Igl et work to replicate human decision-making at unsignalized al. \[104\] proposed a Deep Variational Reinforcement Learning intersections. The DRL agent, learning from diverse scenarios, approach \(DVRL\), which relies less on a black box than the is aided by a detailed environment model that includes state aforementioned DRPIQN and ADRQN, for learning optimal uncertainty, behavior modeling, and intention estimation for policies for POMDPs. Applying DVRL concepts for learning traffic participants like vehicles, pedestrians, and cyclists. 

driving policy in partially-observable unsignalized intersection This model accounts for varying driving styles and uses the environments is still an area of research to be explored. 

Intelligent Driver Model \[109\] for movement and intersection policies. By integrating human-like driving behaviors, the autonomous system adapts to various real-world conditions. 

The study also features a behavior cloning technique from L

F

L

S

F

C

*O*

S

F

human driving data, using Monte Carlo-generated training *t-1*

*a*

*Q*

*a*

T

*t-1*

C

*t-1*

*t-1*

F

T

C

M

data to train a linear model for action quality prediction. 

C

M

This approach balances efficiency and safety, offering more interpretability than some neural network methods. The frame-L

F

L

S

F

C

work’s effectiveness in achieving human-like behavior at *O*

S

F

*t*

*a*

*Q*

*a*

T

*t*

C

*t*

*t*

F

T

C

unsignalized intersections is validated through simulations. 

M

C

M

Occlusion-aware schemes. As previously mentioned in

III-A, due to environmental uncertainties and the limited capaL

F

L

bilities of the sensors on the autonomous vehicle, occlusions S

F

C

*O*

S

F

*t\+1*

*a*

*Q*

*a*

T

*t\+1*

C

*t\+1*

*t\+1*

can pose significant challenges to safely traverse an urban F

T

C

M

C

M

unsignalized intersection. Hence, many research papers have addressed this problem while integrating risk assessors into the decision-making schemes. For example, an occlusion-aware Fig. 5: LSTM for solving the formulated POMDP of algorithm for left turn maneuver risk assessment at four-way intersection-traversal problem. 

unsignalized intersections was developed \[110\]. A particle filter paradigm was utilized to represent the distribution of Intention-aware schemes. These probabilistic decision-the possible unobserved potential locations \(particles\) of the

IEEE JOURNAL TEMPLATE , VOL. –, NO. –, AUGUST 2023

9

vehicle. However, this algorithm is not representative of how TABLE II: Classes of decision-making schemes under partial-the vehicle can make decisions, but can be coupled with any observability at unsignalized intersection POMDP or any other decision-making algorithm. The same Class

Contribution

References

group, based on the forward and background reachability, Occlusion-aware

•

Navigation through static

\[114\] \[38\] \[94\] \[115\]

developed a probabilistic risk assessment and planning algo-and dynamic occlusions. 

rithm for a four-way intersection. The algorithm borders the

• Navigating under perception

\[98\] \[112\] \[96\]

errors due to occlusions

risk-inducting regions arising from the occlusions of the ego-

•

Navigating with Limited

\[116\] \[103\] \[110\]

perception sensors that can be used to generate collision-free sensor range

routes \[111\]. However, none of these algorithms were tested

• A creeping behavior is learnt

\[113\]

to better comprehend the envi-

in real-world environments. McGill et al. \[112\] addressed ronment. 

the problem of navigating unsignalized intersections in the Intention-aware

•

SVM-based motion plan-

\[117\]

presence of occlusions and faulty perception \[112\]. A risk ning. 

• Target motion-based behav-

\[61\]

model was proposed to assess the unsafe \(risky\) left turn across ioral planning. 

traffic at an intersection. Their model accounts for the traffic

•

Navigation through un-

\[31\]

density, sensor noise and physical occlusions that hinder the known intention and noisy perception. 

view of other vehicles. By representing the intersection as a

•

Inferring High-level mo-

\[105, 118\]

junction node with lanes entering and exiting the node, the risk tion intentions including turn-assessment is used to determine a ‘go’ and ‘no-go’ decision ing and going straight. 

at an intersection. The risk is modeled by defining near-miss braking incidents, collision incidents, traffic conflicts and small gap spacing. The risk is defined as the expected number of agent decision-making including urban intersections, we have incidents that will occur if the ego-car enters an intersection. 

high-dimensional continuous action spaces. Discretizing these The overall risk is the sum of all expected incidents in all spaces to use conventional DQN schemes is not always an lanes and for all segments. In \[113\], the occluded intersection-effective idea due to the exponential number of action values traversal problem was viewed as a reinforcement learning which might lead to the Curse of Dimensionality. Hence, to problem. A deep Q-learning approach was utilized to traverse a ensure convergence of the used model and capability, these partially observed four-way intersection. A creeping behavior continuous spaces must be handled in a robust way. Deep De-upon reaching the intersection is learnt where the agent terministic Policy Gradient \(DDPG\) was adopted in \[103, 119\]

must perform an exploratory action to better comprehend the for generating continuous actions rather than discrete actions environment. Three action representations were studied: Time-for driving in four-way unsignalized intersection settings. 

to-Go, Sequential Actions and Creep-and-Go. In the Time-to-Xiong et al. \[120\] presented an integration between Deep Re-Go representation, the desired path is known for the agent, inforcement Learning and safety-based continuous control for and the agent decides whether to go or to wait at every learning optimal policy for self-driving and collision avoidance point in time. While in the latter scenarios, the agent can applications. DDPG, which adopts the actor-critic concepts determine whether to accelerate or decelerate progressively. 

\(see Fig.6\), is implemented to output the steering commands However, a bird’s eye view image space is used to describe along with an Artificial Potential Field \(APF\) method for the position of the vehicles in the space using Cartesian collision avoidance and path planning applications. As this coordinates. This makes the implementation of the proposed integration proves its usefulness for learning collision-free DQN method inefficient for urban driving environments which driving policies at highways, integrating such high-level DRL

require continuous actions rather than discrete ones. Moreover, schemes with control laws can be vital for solving continuin real AVs, it is infeasible to have a ”bird’s eye view’” for ous control problems within the framework of unsignalized acquiring the vehicle’s state for decision-making applications. 

intersections. 

Table II summarizes the major classes of decision-making TD3. While the DDPG algorithm provides a solid founda-schemes under partial-observability. 

tion for handling continuous action spaces, it is often sensitive to hyperparameters and can fail due to overestimation of Q-values. To mitigate these issues, Twin Delayed DDPG \(TD3\) 2\) Training in Continuous Action Space introduces key improvements that result in more robust and DQNs and DDPG. In real autonomous driving, a contin-efficient learning \[121\]. In contrast to conventional DDPG

uous action of the autonomous agent is required for safe and algorithms, which use a single Q-function to represent the efficient navigational tasks. DQNs, which are mostly adopted quality or the utility of taking a specific action in a particular in the reviewed decision-making schemes, are used to learn state, TD3 employs two Q-functions, Qϕ

and Q

, and

1

ϕ2

an optimal policy for safety-oriented decision-making in a utilizes the smaller of the two Q-values to form the targets discrete action space domain. However, adapting such schemes in the Bellman error loss functions. This method, known to continuous domains, i.e. autonomous driving, is consid-as ”Clipped Double-Q Learning,” mitigates the issue of Q-ered challenging, and in some instances, sample inefficient. 

value overestimation. Further, in TD3, the policy and the Practically speaking, DQNs determine an action that has the associated target networks are updated less frequently than highest action-value through an iterative optimization process the Q-function. Specifically, for every two updates to the Q-at every step in the continuous action. For complex multi-function, a single policy update is performed. This ”delayed” 

IEEE JOURNAL TEMPLATE , VOL. –, NO. –, AUGUST 2023

10

policy update reduces the volatility that typically arises in understanding the motion trends of surrounding vehicles. The DDPG, enhancing the stability of the training process. Finally, use of LSTMs allows the model to dynamically adapt to TD3 introduces ”Target Policy Smoothing,” a regularization the environment and predict actions based on the history of technique that adds noise to the target action, which in effect states, rather than just the current state. Consequently, the T-smooths the Q-function along the changes in action space. 

TD3 algorithm provides a more robust and real-time decision-This additional layer of complexity prevents the exploitation of making mechanism for autonomous driving at unsignalized erroneous sharp peaks in the Q-function, improving the robust-intersections, marking a significant step forward compared to ness of the learned policy. Xu et al. \[122\] showed TD3 to be existing MDP-based methods. 

particularly well-suited for the high-dimensional, continuous Soft-actor-critic \(SAC\). Recently, soft-actor-critic \(SAC\) nature of autonomous driving at unsignalized intersections, algorithm has shown better performance in learning policies outperforming DDPG in simulated unsignalized intersection in continuous domains and stability characteristics than other traversal scenarios. 

deep deterministic algorithms including DDPG \[125\]. For MEDDPG. Another common pitfall of conventional DDPG

autonomous driving applications, SAC has demonstrated re-algorithms is their limited scope in exploring the state and markable ability in learning optimal policies for overtaking and action space, often resulting in local optima. This issue has maneuvering at roundabouts \[126, 127\]. Hence, applying soft-been addressed by employing meta-learning techniques to actor-critic \(SAC\) principles for learning traversing policies in adaptively learn exploration policies, as initially proposed complex driving scenarios can be a significant research avenue by Xu et al. \[123\]. This foundational work introduced the to be pursued. 

concept of using a meta-policy gradient to allow for more Safety, Efficiency, Comfort, Energy-saving. Yuan et al. 

flexible and global exploration that is independent of the actor

\[128\] investigate the applicability of various DRL algorithms policy, thereby increasing the sample efficiency in DDPG

\(DDPG, PPO, TRPO\) for autonomous driving at unsignal-training. Building on this approach, Xu et al. \[122\] developed ized roundabouts. Specifically, they design a comprehensive the Meta Exploration Deep Deterministic Policy Gradient reward function that amalgamates aspects of safety, such as \(MEDDPG\) algorithm specifically for the high-dimensional lane adherence and time-to-collision, with the efficiency of and complex nature of autonomous driving at unsignalized movement, comfort through smooth vehicular control, and intersections. MEDDPG incorporates the adaptive exploration energy consumption gauged by Vehicle Specific Power \(VSP\). 

techniques from the original meta-policy gradient framework, The authors adopt a 7-feature representation that encompasses but refines and optimizes them for the specific challenges both vehicle and environmental parameters and a hybrid action posed by autonomous driving scenarios. By employing an space that blends both discrete meta-actions for behavioral independent meta-exploration policy that uses a stochastic patterns and continuous actions for precise throttle and steering policy gradient, MEDDPG aims to improve the learning rate controls. The empirical assessment of the DRL algorithms of both the actor and critic networks, thereby facilitating underlines the nuanced balance of the reward function, with more effective decision-making at unsignalized intersections. 

the TRPO algorithm excelling in safety and efficiency, while The algorithm outperforms conventional DDPG methods on PPO emerges as the superior choice for comfort and energy unsignalized intersection traversal tasks by allowing for a consumption. Moreover, the adaptability of the TRPO-trained more comprehensive exploration of the state and action space, model is validated through its commendable performance thereby leading to faster convergence and more robust policies. 

in additional driving scenarios like highway navigation and T-TD3. Traditional Markov Decision Processes \(MDPs\) merging. 

operate on the premise that the future state is dependent 3\) Training in high-dimensional state-action space solely on the current state and action, disregarding any past As mentioned earlier in II-D, DRL is centered on per-states. This assumption becomes questionable in the context forming iterative optimization processes to learn a policy of autonomous driving at unsignalized intersections. Traffic for a specific task. However, the number of iterations grows dynamics are inherently temporal, and past states often provide exponentially as the state-action space becomes larger. One crucial information for optimal decision-making. Ignoring discernible shortcoming of adopting DQN and DDPG is that previous states thus appears as an unreasonable simplification extensive training has to be performed in order to achieve for this application, given that the decision-making of an optimal behaviour. 

autonomous vehicle \(AV\) often depends on the temporal trends Curriculum Learning. To accelerate the training process, of its surrounding environment. Building upon the work of Curriculum Learning \(CL\) approaches can be employed \[129\]. 

DeepMind \[124\], Xu et al. \[122\] also developed a specialized Qiao et al. \[38\] utilizes Curriculum Learning for reducing approach for autonomous driving termed Time Twin Delayed the training time and improving the performance of the agent Deep Deterministic Policy Gradient \(T-TD3\). This algorithm in unsignalized intersection approaching and one-dimensional expands the traditional state space S to incorporate past states, crossing behavior. However, applying CL concepts for other thereby giving a richer context for decision-making. This en-more complex scenarios. i.e. two-dimensional left-turn was not hancement allows the model to be more aware of the temporal investigated. 

intricacies in the driving environment, thus overcoming the Khaitan et al. \[130\] propose a state dropout-based curricu-limitations inherent to traditional MDPs. In addition to this, lum for PPO to further improve agent performance. Their T-TD3 employs Long Short-Term Memory \(LSTM\) cells to methodology introduces two distinct curricula aimed at over-better account for time-series data, which is essential for coming the issue of suboptimal policies that often plague





IEEE JOURNAL TEMPLATE , VOL. –, NO. –, AUGUST 2023

11

**Environment**

eter allows broad exploration, followed by a reduced parameter for refined policy search. Integrating curriculum learning, CPPO progressively increases training scenario complexity, improving the agent’s adaptability and generalization. The framework utilizes a multi-objective reward function, varying rewards and penalties based on scenario complexity and traffic density, encouraging safer and more efficient driving strategies. 

**Reward** ***r**t*

**Action** ***a**t*

**States**

Comparative simulations show CPPO’s superior adaptability

***s**t*

**Agent**

and faster training convergence than baseline PPO methods. 

However, its validation has been limited to simulations, with **Value Function**

future research needed in sim-to-real transfer. 

****

**Critic**

Reward Function 

Scenario 1 \(

\)

Scenario 1 \(

\)

Scenario 3 \(

\)

**TD Error**

Reward

Action

Reward

Action

Reward

Action

**Policy**

> 

> 

\(s\)

Proximal Policy Optimization

**Actor**

Fig. 6: An illustrative sketch of Actor-Critic approaches. 

Agent Policy

Actor-critic algorithms implement both the value-based approaches and the policy-based approaches. It comprises a couple of estimators: the actor network estimator which is based on Q-value, whereas the critic network utilizes the state-value function estimation. 

Fig. 7: Curriculum learning pipeline

RL agents in unsignalized intersections by adopting an un-RNN and LSTM. In \[103\], Qiao et al. proposed a DRL

conventional approach: unlike traditional curriculum learning learning algorithm to traverse a four-way intersection with a strategies that transition from simpler tasks to more complex two-way stop sign by taking into account the uncertainties ones, Khaitan et al. start with the full complexity of the task that exist in the urban environment. This DRL algorithm is but provide the agent with additional, privileged information. 

developed to utilize the preserved state-action values and the In the first curriculum, training begins by providing the agent current LIDAR information along with the ego car’s state with complete future state information for surrounding vehi-information for designing the decision process. For efficient cles for N time-steps. As the agent progresses through subse-training in a high-dimensional space, a combination of LSTM

quent training phases, it gradually loses access to this future and FC neural networks were designed to store the state-action state information, compelling the agent to adapt and learn from pairs and generate continuous actions. Bouton et al. proposed increasingly incomplete data. A second curriculum takes a a DRL algorithm for navigating urban intersections using the more dynamic approach: it augments the agent’s action space scene decomposition method \[98\] to improve training and to with an additional ”prediction” action. This allows the agent scale to a large number of agents. The decision-making under to choose when to discard future state information, thereby faulty perception is modeled as a POMDP. An extra state gaining a more nuanced understanding of its environment. 

variable has been integrated to the global state vector to model Importantly, the reward structure is also adapted to incentivize the potential incoming traffic participant which is not present the agent to drop more future state information as it becomes in the scene. A probabilistic model checker was adopted to more competent, rewarding the agent with higher scores for compute the probability of reaching the goal safely for each predicting the behavior of surrounding vehicles without the state-action pair prior to learning a policy. Subsequently, a aid of future state information \(See II-B on Driver Intention belief updater algorithm was developed to update the state’s Inference algorithms\). Both curricula outperformed standard uncertainties. Given the prior belief value and the current PPO and rule-based TTC methods at traversing unsignalized observations, the algorithm can integrate the perception error intersections. 

into the planning theme. It uses an ensemble of 50 Recurrent Zengqi Peng et al. \[131\] have developed the Curriculum Neural Networks \(RNN\) to store the observation history. The Proximal Policy Optimization \(CPPO\) framework, enhanc-training process was done using a synthetic dataset generated ing the standard PPO algorithm for autonomous vehicles at from a simulation environment. These techniques, however, unsignalized intersections \(see Fig.7\). CPPO introduces stage-have not been evaluated in real-world driving scenarios, where decaying clipping to balance exploration and exploitation convergence of the proposed models is not guaranteed due during training, adapting its clipping parameter in stages for to the breadth of possible crossing behaviors or directions of optimal policy convergence. Initially, a higher clipping param-agents at unsignalized intersections. 





IEEE JOURNAL TEMPLATE , VOL. –, NO. –, AUGUST 2023

12

Attention-based Schemes. Traditional driving policies of-and its users, unlike traditional graphs that may not capture ten struggle with high-dimensional state-action spaces and the full scope and rely on static, handcrafted features. This have limited ability to focus on the most pertinent features graph is then adeptly transformed into a simpler vehicle graph within a driving scenario. To overcome these challenges, with learnable edges, representing the routes connecting the Seong et al. \[132\] propose an attention-based driving policy vehicles. This allows for the reinforcement learning algorithm that leverages deep reinforcement learning. The model’s state to operate on a simplified but effective representation of the representation comprises three components: a pseudo-scan of environment, focusing on the dynamic interactions of vehicles surrounding vehicles, a local trajectory related to the vehicle’s while navigating the roads. Their experimental validation in path, and the vehicle’s dynamic state. The action space is SUMO demonstrated a significant improvement in the perfor-defined in terms of the vehicle’s target velocity in a continuous mance of the proposed scheme with learnable edge features. 

space. Critically, the model integrates spatial and temporal This enhancement indicates a more effective representation of attention mechanisms into its policy network, allowing it to vehicle relations. 

focus on the most relevant spatial and temporal features in the driving environment. This focused attention makes the model’s decisions both safe and efficient across a range of complex intersection scenarios and varying traffic densities. The model’s performance is quantified through extensive experiments that show it outperforms baseline policies. Moreover, the attention-based design lends itself to interpretability, an often sought but rarely achieved attribute in deep learning models. Importantly, the authors validate the real-world applicability of their model Road node

by successfully transferring it to a full-scale vehicle system, demonstrating its robustness even in the presence of sensory Vehicle node

noise and delayed responses. 

Drivable edge

Graph Networks. Graph Attention Networks \(GATs\) \[133\]

Right-of-way edge

are increasingly used for modeling environments in au-Vehicle-road edge

tonomous driving, especially at unsignalized intersections. The DQ-GAT \[134\] method combines deep Q-learning with GATs Fig. 8: Example heterogeneous direct graph representation of and noisy networks for efficient exploration, automatically road topology and vehicles used in \[137\]

adjusting exploration noise. It leverages noisy linear layers

\[135\] for balance in exploration and exploitation, supporting stable policy deployment. Asynchronous training using the GPT-based Approaches. Liu et al. \[138\] propose their Deep Q-Network \(DQN\) algorithm enhances training effi-MTD-GPT model to harness the synergy of reinforcement ciency by generating diverse experiences simultaneously. The learning \(RL\) and the transformative sequence modeling capa-model uses semantic abstraction with Bird’s Eye View \(BEV\) bilities of Generative Pre-trained Transformers \(GPT\), setting images for dimensionality reduction, providing a geometrically a new stage for managing complex driving tasks. They first consistent perspective that aids in learning and generalization, develop single-task RL expert models using Proximal Policy but also presents a limitation in real-world driving scenarios Optimization \(PPO\) combined with an attention mechanism. 

where a Bird’s Eye View \(BEV\) is not naturally available. 

These experts were trained to excel in specific driving tasks The graph model captures interactions among traffic agents such as turning left, moving straight, or turning right. After using a two-layer GAT with multi-head attention, representing training, the experts’ decision-making, embodied in state-each agent as a graph node. DQ-GAT outperforms other DRL

action-reward sequences, was captured as data. This expert methods in training comparisons, with visual analyses showing data served as a foundational guide for the MTD-GPT. The its effectiveness in real scenarios like complex intersections. 

data was tokenized, akin to how text is prepared for natural Enhanced by policy visualizations, the model’s transparency is language processing, to fit the GPT model’s input format. The evident. Its successful application on the openDD dataset \[136\]

MTD-GPT was then trained offline in an autoregressive fash-and high inference speed suitable for real-time applications ion to predict actions, drawing on this mixed multi-task dataset underscore its effectiveness and practical utility. 

for learning. The training of MTD-GPT involved embedding In \[137\], Schier et al. highlight the limitations of current the tokenized state-action-reward sequences, adding positional graph-based approaches which fail to encompass the entire encodings, and feeding them through a Transformer architec-road network and overly depend on handcrafted features for ture. The self-attention mechanism within the Transformer was vehicle-to-vehicle interaction modeling as shown in Fig.8. To key to focusing on relevant parts of the input sequence for address these shortcomings, the authors propose a framework making decisions. The model was tuned to predict actions that captures the complexity of road networks and traffic based on the input sequence, effectively learning from the participants within a heterogeneous directed graph. This repre-collected expert demonstrations. Upon evaluation, the MTD-sentation can handle different elements \(e.g., various types of GPT model demonstrated its robustness by performing on par vehicles, pedestrians, cyclists, traffic signs\) and their distinct with or even surpassing dedicated single-task RL models. This properties, thus capturing the complexity of the road network indicates that the model can abstract the multi-task decision-

IEEE JOURNAL TEMPLATE , VOL. –, NO. –, AUGUST 2023

13

making problem into a sequence prediction task, providing a imitative expert priors from expert demonstrations for learning promising research direction. 

driving policies in urban environments. In this approach, the Learning from Demonstrators \(LfD\). Learning from priors are learned using IL and an uncertainty quantification demonstrators has been introduced to enhance the learning ca-method, which helps balance exploration and exploitation pabilities, yielding a significant decrease in the total time of the during training. This integration highlights the complementary training process by leveraging training sets with small demon-nature of IL and RL: while IL provides a more stable and safer strations. Hester et al. \[139\] introduced Deep Q-learning from foundation by leveraging expert demonstrations, RL enables demonstrations \(DQfD\) to significantly accelerate the training further refinement through exploration, allowing the agent to process through leveraging sets with small demonstrations. A adapt to unseen scenarios. 

prioritised replay mechanism was adopted for assessing the In brief, Table III epitomizes the limitations of the most rel-required data-sets ratio automatically. Nair et al. \[140\] pro-evant research works on decision-making using reinforcement posed a technique based on DDPG and Hindsight Experience learning-based schemes. 

Replay for enhancing the training policies while learning the optimal policy for solving complex tasks using RL. Although, the proposed work has one major limitation which is the IV. DISCUSSION AND RESEARCH DIRECTIONS

sample efficiency, a significant speed-up of the training process was recorded. These works have led to other modifications of the training process of RL-based motion planning schemes. 

Based on our thorough investigation, we conclude that the For instance, Hierarchical Reinforcement Learning \(HRL\) state-of-art decision-making schemes focused on the high-architecture was developed based on the inclusion of heuristic-level decision making layers, i.e high-level reasoning for based rules-enumeration policy to enhance agent’s exploration behavioral path planning, neglecting other low-level layers for behavioral planning at intersections \[141\]. 

proposed earlier, including low-level motion planning and Incorporating Imitation Learning \(IL\) approaches can ac-control \[156, 157\]. Furthermore, implementation and testing celerate training and improve safety by reducing the reliance in real-world driving environments is not investigated. In on random exploration \[142\], which is particularly crucial in practice, convergence of the RL-models in simulation-based complex, multi-agent environments like unsignalized intersec-environments does not necessarily ensure generalizability in tions \[\]. However, IL alone may struggle with generalization real-life scenarios due to the domains mismatch. Real-world

\[143\], as it heavily depends on the quality and diversity observations differ in terms of the associated noise sequences of the expert demonstrations. On the other hand, RL-based and vehicle dynamics response. Therefore, in this section, we approaches, while more autonomous and capable of handling suggest avenues for research built upon these insights with the novel scenarios, often require extensive interaction with the aim of progressing the field of study. 

environment, making them computationally expensive and A. Motion planning and Low-level control integration potentially unsafe during the early stages of training \[144\]. 

Model Predictive Control \(MPC\) Employment. Numer-Despite these strengths, RL-based decision-making remains ous research papers have addressed the motion planning challenging for real-world applications, particularly in safety-problem and control at urban unsignalized intersections using critical environments such as unsignalized intersections. One MPC principles. For instance, Hu et al. \[158\], proposed an significant issue is the sample inefficiency of RL, where event-triggered model predictive adaptive dynamic program-learning robust policies requires a massive amount of data ming technique for motion planning at urban intersections. 

and interactions. This is compounded by the difficulty in The method takes urban speed, vehicle kinematics and road designing appropriate reward functions that align with safe constraints into consideration while solving multi-objective driving behavior, as poorly designed rewards can lead to optimization problem. Recently, in \[159\], an integrated control unintended or unsafe actions \[145\]. Furthermore, real-world technique combines reinforcement learning and model pre-deployment of RL-based systems is hindered by difficulties dictive control is proposed for motion planning at unsignal-in simulating edge cases and handling unexpected situations, ized T-intersections. The integration envelops two independent which are crucial for ensuring safety in autonomous driving control systems: one that involves nominal RL longitudinal

\[146\]. 

control and path selection, and another for reactive MPC

By integrating IL techniques with RL, the agent can benefit longitudinal cruise control and lateral path tracking. These from expert knowledge while still exploring and adapting to systems are capable of independently managing the vehicle’s new situations, addressing some of the key challenges in RL. 

lateral and longitudinal dynamics. This coupled RL/MPC

This combination can also improve the safety and efficiency architecture serves as a backup mechanism to enhance nav-of training in high-risk environments like unsignalized in-igation safety. The two algorithms run concurrently, and a tersections. However, this integration introduces challenges, discrete selector focused on safety considerations determines such as the potential for overfitting to expert demonstrations the control output. Nevertheless, this proposed scheme focuses or difficulties in determining when to switch from imitation on the motion planning an control without considering the to reinforcement learning. Addressing these issues will be behavioral path planning layer. Additionally, the proposed crucial for developing decision-making architectures that are solution is computationally intensive due to the independent both effective and safe in real-world unsignalized intersections. 

functioning of the MPC model and reinforcement learning-Recently, Huang et al. \[147\] developed an integration between based control mechanisms, along with a supervisory system

IEEE JOURNAL TEMPLATE , VOL. –, NO. –, AUGUST 2023

14

TABLE III: Overview of the reviewed Reinforcement learning-based decision-making schemes at unsignalized intersection Ref. 

Intersection Type

Method

Data Collected

Remarks

Limitations

\[38\]

4-way

Unsignalized

DRL using automatic genera-

Simulation-based

• A more realistic 4-way intersection driving

• Environmental uncertainties, which cause errors in \(stop-sign\)

tion of curriculum for training

scenario is proposed where vehicles are pro-perception were not considered while collecting Ob-enhancement

grammed not to yield to ego vehicle if it is in servations from simulated sensor \(LIDAR \+ Cameras\) their FOV

\[113\]

T-junction

DQN

SUMO simulator \[148\]

• A creeping behavior upon reaching the inter-

•

A god-view state space is used to describe the section is learnt where the agent must perform motion of vehicles at intersection \(Not true for real-an exploratory action to better comprehend the life driving\)

environment

\[97\]

Multi-lane

4-way

Multi-objective

RL

Collected Via SUMO

• Learning safe crossing with the presence of

• A full knowledge of other vehicles based on a bird’s intersections

and

\(Thresholded

lexicographic

simulator

faulty perception and occlusion

eye view representation of state space \(not realistic for roundabouts. 

Q-learning\)

• The trained policy is scalable across a range of real-world\)

urban roads with different shapes

• Not tested in real-world environments

• Learning human behavior of looking at vehicles at area of interest

\[103\]

4-way

Unsignalized

RL-based approach using hi-

Collected Via SUMO

• Learning an optimal policy for robust travers-

• No guarantees for possible scalability at more com-

\(stop-sign\)

erarchical option

simulator

ing under environmental uncertainties

plex intersections with multi-lanes

• Results shows superiority over the rule-based

• Not tested in real-world environments techniques and classical approaches

\[98\]

T-junction

Integration of model-checker

Simulation-based

• Learning safe crossing with the presence of

• The proposed method was not validated through real and RL

faulty perception and occlusion

testing to show the validity of the simulated POMDP-based simulated values of the perception errors

\[141\]

Multi-lane 4-way inter-

Hierarchical

reinforcement

MSC’s

VIRES

VTD

• Better convergence capabilities and sample-

• Focus on mimicking human driving in limited go-section

learning with hybrid reward

\(Virtual

Test

Drive\)

efficiency compared to the classical RL Methods straight and left-turn maneuvers

mechanism

simulator

• Not tested in real-world environments

\[115\]

Multi-lane 4-way inter-

DQN

Collected Via CARLA

• DQN shows less overcautious behavior under

• DQN is utilized for learning the driving policy. How-section. 

Simulator \[149\]\)

limited sensor range and faulty perception com-ever, DQN is restricted to the discrete action domain pared to the rule-based algorithms

• Not tested in real-life environments

\[150\]

4-way

DQL and DDQL

Simulation-based

• The proposed results show safe and repeatable

• Training based on simulated sensor observations. 

Left-turn maneuver is learnt where the collision

• The proposed scheme is restricted to discrete action rate is significantly reduced

space. 

\[74\]

4-way

Bayesian RL-based scheme

Simulation-based

• The Uncertainty of the RL agent’s actions is

• Lacks real-world testing

using an ensemble of NN with

estimated. 

•

Assumptions related to the formulated decision-Randomized Prior Functions

making problem have been made, i.e. the environment \(RPF\)

is assumed to be fully observable \(MDP\)

\[151\]

T-junction

RL with stochastic guarantees

Simulation-based

• Traversing with safety guarantees

•

The proposed scheme deals with discrete action space only

• Assumptions made for the vehicle and the pedestrians motion

\[152\]

4-way

DQL and DDQ

Simulation-based

• RL-enabled control framework is built using

• RL scheme deals with discrete action space only. 

transfer rules

• The proposed geometric controller does not represent actual vehicle constraints, e.g. max steering rate. 

\[130\]

Multi-lane 4-way inter-

State Dropout-Based Curricu-

Simulation-based

• State dropout-based curriculum learning ap-

• RL scheme deals with discrete action space only. 

section & Unsignalized

lum Reinforcement Learning

\(CommonRoad\)

proach with PPO

• Lacks real-world testing

T-junction

\[131\]

Multi-lane 4-way inter-

Curriculum Proximal Policy

Simulation-based

• Rapid policy search and optimal convergence

• RL scheme deals with discrete action space only. 

section

Optimization

through adjustable clipping in PPO

• Lacks real-world testing

• Improved generalization and speed via stage-based curriculum learning. 

\[122\]

Multi-lane 4-way inter-

DDPG, MEDDPG, TD3 & T-

Simulation-based

• Novel time twin delayed DDPG algorithm to

• Lacks real-world testing

section

TD3

mitigate overestimation bias in value approxi-

•

Assumptions made about other vehicles’ motion mation and improve training stability

\(fixed speed\)

•

Novel Meta Exploration Deep Deterministic Policy Gradient \(MEDDPG\) algorithm combines meta-learning principles with exploration strategies to allow for more global exploration

\[134\]

Multi-lane 4-way inter-

DQ-GAT: DQN and GATs

Simulation-based

• GATs to model interactions in dynamic traffic, 

• RL scheme deals with discrete action space only. 

section \(unprotected left

\(CARLA\)

and

real-

and DQN for learning scheme

• Proposed scheme relies on BEV images turn\), Unsignalized T-world dataset openDD

junction & Unsignal-

ized roundabout

\[137\]

Multi-lane

4-

High-Level

Heterogeneous

Simulation-based

• Use of heterogeneous directed graph to model

• RL scheme deals with discrete action space only. 

way

intersection, 

Graph Representations

\(SUMO\)

full complexity of driving scenarios at unsignal-

• Lacks real-world testing

Skewed

Multi-lane

ized intersections

4-way

intersection, 

• Transformation into a simpler vehicle graph Unsignalized

with learnable edges for better integration with Merge

Junction, 

DRL scheme

& 

Unsignalized

roundabout

\[132\]

Multi-lane 3, 4, 5-way

Attention-based Deep Rein-

Simulation-based

• Use of spatial and temporal attention focus

• The developed DRL technique is agnostic to motion intersection, Unsignal-forcement Learning

\(CARLA\) & real-world

mechanism

planning and control layers

ized roundabout

deployment

\[138\]

Multi-lane 4-way inter-

MTD-GPT

Simulation-based \(Ope-

• GPT-based model based on single-task DRL

• Lacks real-world testing

section

nAI Gym\)

expert models \(PPO\)

\[153\]

Multi-lane 4-way inter-

Safe and Rule-Aware Deep

Simulation \(SUMO & 

• DRL framework w/ traffic rule monitor to en-

• RL scheme deals with discrete action space only. 

section

Reinforcement Learning

CARLA\)

sure compliance with intersection right-of-way

• Lacks real-world testing

rules

• RSS-based safety checker used to identify and react to unsafe situations

responsible for output selection. Another integration has been distributed—a situation that has not yet been realized. 

done for intersection-management applications, where central-In practical terms, achieving precise decision-making in ur-ized reference signals being distributed to the intersections ban autonomous driving necessitates the integration of motion agents via V2V communication \[160, 161\]. Hamouda et al., planning and low-level control layers that consider vehicle developed an integration between high-level decision-making dynamics with the RL-based behavioral planners. This integra-layers and low-level MPC-based motion planing layer has been tion is essential to ensure that the RL-based behavioral planner proposed for learning supervisory intersection-management actions are feasible. Therefore, incorporating the motion plan-policy in connected driving fashion. Nonetheless, for this ning layer while learning intersection-traversal policies would solution to be completely workable, it is crucial that vehicular ensure from feasible actions and with high fidelity, taking into communication and connected vehicle technologies are widely account lateral and longitudinal dynamics. To illustrate the

IEEE JOURNAL TEMPLATE , VOL. –, NO. –, AUGUST 2023

15

TABLE IV: Performance evaluations

based planning with MPC-based motion control, surpasses Ref. 

Intersection

Maneuver

Success

Collision

these baseline methods, including TD3 and PPO, in terms of Type

rate

Rate\(%\)

training efficiency and navigation performance. Furthermore, \(%\)

\[38\]

4-way intersec-

Straight

82.1

13.5

the training results highlight the effectiveness of our method tion

in terms of performance and sample efficiency. The testing

\[103\]

4-way intersec-

L. Turn

97.3

2.6

tion

R. Turn

99.8

0.2

results showcase the efficiency and safety of the learned Straight

98.3

1.7

left-turn behaviors, with a success rate of 97.8% over 1000

\[97\]

Multi-lane

Turning

N/A

3.5

testing episodes. Notably, despite the inherent challenges of intersections

Yielding

\[132\]

Multi-lane

L. Turn

87

5

navigating a complex two-dimensional left-turn intersection, intersections

R. Turn

97

2

the integration of the SAC-based behavioral path planning Straight

92

3

\[141\]

4-way intersec-

Straight

95.6

4.2

layer with the MPC-based motion planning layer leads to faster tion

convergence and a higher success rate compared to existing

\[130\]

4-way intersec-

L. Turn

93.83

N/A

tion

N/A

literature \(see Table IV\). 

\[134\]

3, 4, 5-way in-

L. Turn

96.67

N/A

As we emphasized the significance of hierarchical decision-tersection

\[153\]

4-way intersec-

Straight

98.6

N/A

making, which integrates decision-making layers for learning tion

traversing policies in complex multi-agent environments, such

\[154\]

Roundabout

L. Turn

93

5

\[152\]

4-way intersec-

L. Turn

90

N/A

principles can be applied to tackle the challenges posed by tion

R. Turn

92.5

more intricate unsignalized intersection environments, char-Straight

94

\[137\]

4-way intersec-

L. Turn

90

10

acterized by occlusions and environmental obstructions that tion

impede the attainment of accurate perception. Additionally, 

\[131\]

4-way intersec-

L. Turn

90.5

N/A

tion

there is potential for enhancing the model’s accuracy and

\[155\]

4-way intersec-

L. Turn

94.7

N/A

navigation capabilities in the context of intersections with tion

diverse shapes and geometries. 

\[144\]

4-way intersec-

L. Turn

97.8

1

tion

Incorporating High-fidelity Vehicle Dynamic Models. 

In connection with autonomous driving problem in adverse weather environments \[162–164\], incorporating high-fidelity importance of the proposed research direction, we developed vehicle dynamic models is also critical for longitudinal and recently a novel hierarchical reinforcement learning-based lateral motion planning. For instance, learning safety-oriented decision-making architecture for learning left-turn policies at policies for intersection-approaching behavior at unsignalized unsignalized intersections with feasibility guarantees \[144\]. 

intersection, where braking is applied to decelerate smoothly This hierarchical architecture is comprised of two distinct for precise stopping, is a prerequisite condition for safe in-layers; a high-level learning-based behavioral planning layer tersection navigation. Hence, learning an optimal deceleration which adopts soft actor-critic \(SAC\) principles to learn non-profile \(curve\) ax,optimal, which ensures a comfortable ride conservative, yet safe, driving behaviors and a low-level while remaining efficient, requires an inclusion of longitudi-motion planning layer that uses Model Predictive Control nal vehicle dynamic models and braking performance which \(MPC\) framework to ensure feasibility of the two-dimensional is coupled with the road surface conditions represented by left-turn maneuver. The high-level layer is responsible for friction coefficients \(see rough curves in Fig. 10\). 

generating reference signals of velocity and yaw angles for the B. Real-world experimental validation

ego vehicle taking into account safety and collision avoidance As can be seen from Table, III, most of the reviewed behaviors with the intersection vehicles, whereas the low-level schemes have been tested in simulation-based environments. 

motion planning layer solves an optimization problem to track This can be valid, as RL techniques require collecting a these reference commands taking into account vehicle dynamic large amount of real-world based training data which would constraints and ride comfort. We conducted several simulation be costly in terms of effort and time. Practically speaking, experiments to demonstrate the significance of the proposed simulated observations, which are streamed from modelled decision-making hierarchy. We observed that when utilizing sensors, have different data distributions compared to real MPC \(refer to Fig. 9\), the policy begins to converge after 200k data which may lead to failure in generalization on \(unseen\) training steps, achieving a high rate of successful traversals. In real data \[165\]. This difference between simulated and real contrast, the standalone SAC, when MPC disabled, converges data distributions, such as inaccuracies in synthetic image at around 500k training steps which demonstrates significant generation or in vehicle dynamics, has been coined the ”reality sample efficiency. This difference can be attributed to the gap” \(RG\) \[166, 167\]. It is known that agents trained in optimization of control inputs by the MPC, which already simulation transfer poorly to real-world environments without accounts for real-life driving constraints when interacting with explicit regard for RG \[168\]. To rectify this, sim-to-real the environment. 

transfer learning techniques have been introduced to further We evaluated the suggested decision-making approach promote training RL approaches in real environments \[169\]. 

within simulated environments and performed a compara-This survey highlights some proposed techniques which tive analysis against alternative model-free Reinforcement have been validated in real-world scenarios, and others which Learning \(RL\) baseline methods. Our findings demonstrate the authors believe to be promising theoretically or in other that the proposed integrated approach, which combines SAC-areas of robotics but require experimental validation in real-





IEEE JOURNAL TEMPLATE , VOL. –, NO. –, AUGUST 2023

16

**\(MPC Disabled\)**

**\(MPC Enabled\)**

**Perceptual**

**Perceptual**

**Observations**

**Observations**

**Behavioral Planner \(SAC-based\)**

**Behavioral Planner \(SAC-based\)**

**"Main Road" **

**"Intersection Zone" **

***dleft, stop***

***dbuffer***

***vx, ego***

**Motion planning and**

***ax, ego***

**control \(MPC-based\) **

**Region A**

**Region B**

**Region C**

***ax***

***ax, optimal***

***dleft, stop***

Fig. 9: An illustrative sketch on the integration of Model Fig. 10: An illustrative sketch of the intersection-approach Predictive Control with the SAC-based behavioral planning phase scheme. As shown, the vehicle enters Region A with layer. When MPC is not integrated, the decision-maker \(agent\) the standard speed Vx,ego of \(40–50 km/h\). In Region B, receives perceptual observations from the intersection driv-the vehicle is assumed to start decelerating with rate ax,ego ing environment and maps them directly into throttle v and to reach the stop-line. Region C represents the safety buffer steering θ commands executed by the environment. As a dbuffer. 

standalone RL setting, the traversing policy is trained through these interactions with the driving environment to provide actions to maximize the future rewards, regardless whether intersection angle and approaching car velocities may provide they are feasible or not. On the other hand, when the MPC

increased robustness of a proposed model traversing unsignalis enabled, the policy is trained with the SAC algorithm to ized intersections. Pouyanfar et al. also demonstrate that DR

output reference velocity vref and heading signals θref . The provides resilience to sensor noise and sub-optimal operating motion planning layer takes these reference signals as inputs conditions. \[174\] We note that this is of particular importance to the two-dimensional tracking control problem, solving the to driving at unsignalized intersections due to the variety formulated optimization problem while accounting for real-of sensor occlusion patterns which may occur. In addition, world constraints related to vehicle dynamics, urban traffic Amini et al. \[175\] introduced a training engine for transfer rules, and ride comfort. The optimized, feasible, control inputs learning of end-to-end autonomous driving policies using are then produced to drive the vehicle’s physical model in the sparsely-sampled trajectories from human drivers. Utilizing simulated driving environment. 

these trajectories has yielded robustness in performing real driving tests in unseen complex and near-crash environments. 

Using CARLA, the performance of the proposed method has world scenarios using real-sized vehicles. Of those with val-been evaluated in comparison with the DA and DR approaches. 

idated results, we introduce Domain Randomization \(DR\) The results exhibited superiority of the proposed approach and Domain Adaptation \(DA\). While not tested outside of over the conventional transfer learning approaches in terms simulation, Adversarial RL techniques demonstrate improved of recovery from hazardous near-crash situation. 

robustness to environmental perturbations. 

Adversarial RL. Taking inspiration from GANs, one may Domain Randomization. In utilizing DR methods, the even adversarially perturb the environment as to mislead and agent is exposed to stochastic perturbations in the environment destabilize the agent. Training an agent and adversary in in simulation to improve robustness in real-world deployment this manner is similarly inspired by H∞ control methods

\[170, 171\]. Inspired by H∞ control, such perturbations aim and is known as Robust Adversarial Reinforcement Learning to provide robust control under \(non\) parametric uncertainty \(RARL\) \[176\]. Presented with the task of merging onto high-

\[172\], and allow the agent to be less sensitive to environ-way lanes, a constrained adversarial RL policy consistently ment parameter perturbations. Kontes et al. utilize domain outperforms baselines in terms of speed and collision rates randomization to design a high-speed collision avoidance con-

\[177\]. As a further improvement, rather than optimizing for troller for autonomous cars which, utilizing DR achieves near-the highest expected reward it is better to reduce the worst-perfect collision avoidance performance across all environment case outcome in safety oriented applications. A limitation of parameters than its peers trained using specific environment RARL in this consideration is that only the expected reward parameters \[173\]. This suggests that utilizing DR to vary is optimized without a modeling of risk. To address this, 





IEEE JOURNAL TEMPLATE , VOL. –, NO. –, AUGUST 2023

17

Pan et al. propose a risk-adverse RARL scheme where an adversarial agent explores states with high variance in value function to force the agent into risky scenarios \[178\]. The resulting agent experiences substantially fewer collisions and safety-adverse events compared to previous baselines. This risk-adverse behavior, outlined graphically in figure 11 is ex-ceptionally notable in autonomous driving where autonomous actors are expected to error at rates well below human errors. 

Furthermore, autonomous drivers must act in a way humans \(a\) Simulation setup of turn-

\(b\) Simulation evolution of

find agreeable from a high-level decision making standpoint. 

ing at an unsignalized inter-

baseline RL models success-

As such, risk-adverse algorithms are necessary to avoid what section

fully turning in simulation

may be perceived as unnecessary risk and endangerment. As seen in figure 11b, baseline algorithms will favour riskier driving habits due to reward discounting. With the introduction of RARL schemes, the trained agent perform more inline with human behaviours and decision-making as seen in figures 11d

and 11e. In addition, risk-adversity is especially important at unsignalized intersections to prevent trained models from crossing or turning when the guarantee of safety is low with high occlusion of passing cars. As previously noted, while \(d\) Risk-adverse algorithm

the above RARL applications in AD indeed demonstrate learns to delay crossing to

\(c\) Irrecoverable adversarial

allow for spacing between

improved robustness in environmental perturbations, further perturbation causing crash

cars before crossing

experimentation is required to validate the transfer into the real world. 

Domain Adaptation. Domain Adaptation \(DA\) techniques have also been proposed to enhance the generalization capabilities of ML-based models on a target domain. Feature-level DA methods are designed to learn domain-invariant features which cannot discriminate between the source and the target domains, whereas pixel-level DA techniques focuses on shaping images from the source domain to be analogous \(f\) An adversarial perturba-to the target domain’s images using Generative Adversarial tion causing a lane invasion, 

Networks \(GANs\) \[179, 180\]. Ganin et al. \[181\] describe a but because the ego vehicle

\(e\) RARL agent turns only

is no longer adjacent to an-

domain-adversarial training of neural networks for Feature-after first vehicle is a safe

other vehicle this perturba-

level domain adaptation. This model is based on features distance away

tion is recoverable

that are discriminative for the central learning process, but Fig. 11: Demonstration of a risk-adverse algorithm learning to indiscriminative with the translation between these domains. 

delay rewards slightly in favour of less risky driving behaviour. 

In \[182\], an end-to end \(i.e., perception to control\) transfer The agent learns to avoid system states which are easily learning using image-to-image translation for domain transfer perturbed to a state of catastrophic failure, and prefers safer was applied for autonomous driving. Although the lane fol-states where perturbed states are still safely recoverable from. 

lowing driving policy was learnt from the simulation domain with control labels, the model was able to provide control from real images due to the shared latent space between the two domains. 

RL approaches in real-world driving settings is an active area An inherent limitation of the autonomous driving sector is of research. Inspired by the presented sim-to-real techniques the cost associated with any real-world experimental testing which prove its robustness in learning optimal policies for such as vehicle and sensor replacement. Especially with tasks end-to-end autonomous driving, the real-world experimental associated with non-negligible and unavoidable catastrophic validation of the simulation-based decision-making approaches failure rates such as high speed obstacle avoidance, there is would be further facilitated by creating real-life intersection often little incentive to test safety critical applications in a real driving scenarios. 

world setting to experimentally gauge the transfer of learning V. CONCLUSION

from simulation to the real world. However, there have been many promising sim-to-real transfer techniques proposed and Unsignalized intersections are safety-critical areas in urban tested in the real-world. Indeed, many others improving on environments due to the complex driving behavior and the previous techniques have not been validated. The authors hope lack of traffic control signals. Consequently, developing robust that new sim-to-real techniques can be inspired by the experi-decision-making and motion-planning for these multi-agent mental design of these techniques and demonstrate robustness environments is highly intractable due to the complexities extending to real-world applications. In short, validating the associated with the partially observable multi-agent driving

IEEE JOURNAL TEMPLATE , VOL. –, NO. –, AUGUST 2023

18

environment and the environmental uncertainties. With the estimation for a safety-oriented cyber-physical system in urban driving: resurgence of deep learning, modern RL techniques have deep learning approach. 

IEEE/CAA Journal of Automatica Sinica, 8\(1\):169–178, 2020. 

been utilized to handle such problems with a large space of

\[5\] Md Abdus Samad Kamal, Kotaro Hashikura, Tomohisa Hayakawa, Kou observations to learn safe driving policies. 

Yamada, and Jun-ichi Imura. Look-ahead driving schemes for efficient This survey reviews various aspects related to challenges control of automated vehicles on urban roads. IEEE Transactions on Vehicular Technology, 71\(2\):1280–1292, 2021. 

associated with decision-making at unsignalized intersections

\[6\] Hong Wang, Yanjun Huang, Amir Khajepour, Dongpu Cao, and Chen with a focus on learning-based schemes. We discuss these Lv. Ethical decision-making platform in autonomous vehicles with schemes in terms of the tackled driving scenario, the involved lexicographic optimization based model predictive controller. IEEE

transactions on vehicular technology, 69\(8\):8164–8175, 2020. 

challenges, the proposed learning-based designs and the val-

\[7\] Eddy Zhou, Alex Zhuang, Alikasim Budhwani, Rowan Dempster, idation in simulations and real-world environments. Based Quanquan Li, Mohammad Al-Sharman, Derek Rayside, and William on our discussion and investigation, we found that research Melek. 

Ralacs: Action recognition in autonomous vehicles using interaction encoding and optical flow, 2023. 

efforts are still required to tackle the real-world challenges of

\[8\] Yoshiaki Kuwata, Justin Teo, Gaston Fiore, Sertac Karaman, Emilio unsignalized intersection-traversal problem with guarantees of Frazzoli, and Jonathan P How. 

Real-time motion planning with

safety and feasibility. 

applications to autonomous urban driving. 

IEEE Transactions on

control systems technology, 17\(5\):1105–1118, 2009. 

Ultimately, the decision making schemes that were reviewed

\[9\] Shashwat Verma, You Hong Eng, Hai Xun Kong, Hans Andersen, have been proposed to tackle uncertainties associated with Malika Meghjani, Wei Kang Leong, Xiaotong Shen, Chen Zhang, traversing the unsignalized intersection problem. This is com-Marcelo H Ang, and Daniela Rus. Vehicle detection, tracking and behavior analysis in urban driving environments using road context. 

monly modeled as a POMDP due to the unknown intention In 2018 IEEE International Conference on Robotics and Automation and future trajectories of intersection users. Environmental \(ICRA\), pages 1413–1420. IEEE, 2018. 

uncertainties due to limited sensor range and faulty perception

\[10\] Ransalu Senanayake, Maneekwan Toyungyernsub, Mingyu Wang, Mykel J Kochenderfer, and Mac Schwager. 

Directional primitives

are taken into account while designing occlusion-aware deci-for uncertainty-aware motion estimation in urban environments. In sion making schemes. Furthermore, uncertainties of different 2020 IEEE 23rd International Conference on Intelligent Transportation driving styles are also considered in developing decision-Systems \(ITSC\), pages 1–6. IEEE, 2020. 

\[11\] Kai Yang, Xiaolin Tang, Sen Qiu, Shufeng Jin, Zichun Wei, and Hong making schemes for learning optimal crossing policy in multi-Wang. Towards robust decision-making for autonomous driving on agent environments. However, we have observed that specific highway. IEEE Transactions on Vehicular Technology, 2023. 

critical areas have been overlooked, lacking in-depth research. 

\[12\] Xiaolin Tang, Bing Huang, Teng Liu, and Xianke Lin. 

Highway

decision-making and motion planning for autonomous driving via soft These areas focus on integrating the high-level reasoning actor-critic. IEEE Transactions on Vehicular Technology, 2022. 

principles from the behavioral planning layer with motion

\[13\] Can Xu, Wanzhong Zhao, Jinqiang Liu, Chunyan Wang, and Chen Lv. 

planning and control layers, utilizing high-fidelity models to An integrated decision-making framework for highway autonomous driving using combined learning and rule-based algorithm. 

IEEE

ensure the feasibility of commanded actions. Additionally, Transactions on Vehicular Technology, 2022. 

there is a need for employing advanced sim-to-real transfer

\[14\] Xiaohui Li, Zhenping Sun, Dongpu Cao, Zhen He, and Qi Zhu. Real-learning techniques to facilitate experimental validation and time trajectory planning for autonomous urban driving: Framework, algorithms, and verifications. IEEE/ASME Transactions on mechatron-testing in real-world unsignalized intersection environments. 

ics, 21\(2\):740–753, 2015. 

Consequently, we underscored the importance of developing

\[15\] Shane Gilroy, Edward Jones, and Martin Glavin. Overcoming occlu-hierarchical decision-making architectures to ensure safety and sion in the automotive environment-a review. IEEE Transactions on Intelligent Transportation Systems, 2019. 

feasibility. Moreover, we provided suggestions for methods

\[16\] Xin Huang, Stephen G McGill, Brian C Williams, Luke Fletcher, and heuristics that can facilitate real-world driving for testing and Guy Rosman. Uncertainty-aware driver trajectory prediction at and validating RL-based models. By incorporating our recom-urban intersections. In 2019 International Conference on Robotics and Automation \(ICRA\), pages 9718–9724. IEEE, 2019. 

mendations, precise and feasible learning-based models can be

\[17\] Rowan Dempster, Mohammad Al-Sharman, Yeshu Jain, Jeffery Li, trained and validated in real-world urban settings. 

Derek Rayside, and William Melek. Drg: A dynamic relation graph for unified prior-online environment modeling in urban autonomous ACKNOWLEDGMENT

driving. In 2022 International Conference on Robotics and Automation \(ICRA\), pages 8054–8060. IEEE, 2022. 

This work was supported by NSERC CRD 537104-18, 

\[18\] Eun-Ha Choi. Crash factors in intersection-related crashes: An on-in partnership with General Motors Canada and the SAE

scene perspective. Technical report, 2010. 

\[19\] Michael Wayland. Gm’s cruise begins testing autonomous vehicles AutoDrive Challenge. We would like to thank Dr. Naser without human drivers in san francisco, 2020. 

Lashgarian Azad and Rowan Dempster for their insightful

\[20\] Yihan Hu, Jiazhi Yang, Li Chen, Keyu Li, Chonghao Sima, Xizhou discussions. 

Zhu, Siqi Chai, Senyao Du, Tianwei Lin, Wenhai Wang, Lewei Lu, Xiaosong Jia, Qiang Liu, Jifeng Dai, Yu Qiao, and Hongyang REFERENCES

Li. 

Planning-oriented autonomous driving. 

In Proceedings of the

IEEE/CVF Conference on Computer Vision and Pattern Recognition

\[1\] Martin Buehler, Karl Iagnemma, and Sanjiv Singh. The DARPA urban \(CVPR\), pages 17853–17862, June 2023. 

challenge: autonomous vehicles in city traffic, volume 56. springer, 

\[21\] Kashyap Chitta, Aditya Prakash, Bernhard Jaeger, Zehao Yu, Katrin 2009. 

Renz, and Andreas Geiger. Transfuser: Imitation with transformer-

\[2\] Murat Dikmen and Catherine M Burns. Autonomous driving in the real based sensor fusion for autonomous driving. IEEE Transactions on world: Experiences with tesla autopilot and summon. In Proceedings Pattern Analysis and Machine Intelligence, 2022. 

of the 8th international conference on automotive user interfaces and

\[22\] Yimin Chen, Jingqiang Zha, and Junmin Wang. An autonomous t-interactive vehicular applications, pages 225–228, 2016. 

intersection driving strategy considering oncoming vehicles based on

\[3\] Hong Wang, Amir Khajepour, Dongpu Cao, and Teng Liu. Ethical connected vehicle technology. IEEE/ASME Transactions on Mecha-decision making in autonomous vehicles: Challenges and research tronics, 24\(6\):2779–2790, 2019. 

progress. IEEE Intelligent Transportation Systems Magazine, 2020. 

\[23\] Jeffrey Hawke, Richard Shen, Corina Gurau, Siddharth Sharma, 

\[4\] Mohammad Al-Sharman, David Murdoch, Dongpu Cao, Chen Lv, Daniele Reda, Nikolay Nikolov, Przemysław Mazur, Sean Mickleth-Yahya Zweiri, Derek Rayside, and William Melek. A sensorless state waite, Nicolas Griffiths, Amar Shah, et al. 

Urban driving with

IEEE JOURNAL TEMPLATE , VOL. –, NO. –, AUGUST 2023

19

conditional imitation learning. In 2020 IEEE International Conference Research Part C: Emerging Technologies, 164:104654, 2024. 

on Robotics and Automation \(ICRA\), pages 251–257. IEEE, 2020. 

\[44\] Kaiwen Zhang, Zhiyong Cui, and Wanjing Ma. A survey on reinforce-

\[24\] Wilko Schwarting, Javier Alonso-Mora, and Daniela Rus. Planning and ment learning-based control for signalized intersections with connected decision-making for autonomous vehicles. Annual Review of Control, automated vehicles. Transport Reviews, pages 1–22, 2024. 

Robotics, and Autonomous Systems, 2018. 

\[45\] Johannes Müller, Jan Strohbeck, Martin Herrmann, and Michael Buch-

\[25\] Taxonomy and definitions for terms related to driving automation holz. Motion planning for connected automated vehicles at occluded systems for on-road motor vehicles. SAE, 2016. 

intersections with infrastructure sensors. IEEE Transactions on Intel-

\[26\] Zulqarnain H Khattak, Michael D Fontaine, and Brian L Smith. Ex-ligent Transportation Systems, 2022. 

ploratory investigation of disengagements and crashes in autonomous

\[46\] Shen Li, Keqi Shu, Chaoyi Chen, and Dongpu Cao. Planning and vehicles under mixed traffic: An endogenous switching regime frame-decision-making for connected autonomous vehicles at road intersec-work. IEEE Transactions on Intelligent Transportation Systems, 2020. 

tions: A review. Chinese Journal of Mechanical Engineering, 34\(1\):1–

\[27\] Hong Wang, Yanjun Huang, Amir Khajepour, Yubiao Zhang, Yadollah 18, 2021. 

Rasekhipour, and Dongpu Cao. Crash mitigation in motion planning for

\[47\] Mahsa Golchoubian, Moojan Ghafurian, Kerstin Dautenhahn, and autonomous vehicles. IEEE Transactions on Intelligent Transportation Nasser Lashgarian Azad. Pedestrian trajectory prediction in pedestrian-Systems, 20\(9\):3313–3323, 2019. 

vehicle mixed environments: A systematic review. IEEE Transactions

\[28\] Sasinee Pruekprasert, Jérémy Dubut, Xiaoyi Zhang, Chao Huang, and on Intelligent Transportation Systems, 2023. 

Masako Kishida. A game theoretic approach to decision making for

\[48\] Brian Paden, Michal Čáp, Sze Zheng Yong, Dmitry Yershov, and multiple vehicles at roundabout. 

arXiv preprint arXiv:1904.06224, 

Emilio Frazzoli. A survey of motion planning and control techniques 2019. 

for self-driving urban vehicles. 

IEEE Transactions on intelligent

\[29\] Guofa Li, Shenglong Li, Shen Li, Yechen Qin, Dongpu Cao, Xingda vehicles, 1\(1\):33–55, 2016. 

Qu, and Bo Cheng. Deep reinforcement learning enabled decision-

\[49\] Said Broumi, Assia Bakal, Mohamed Talea, Florentin Smarandache, making for autonomous driving at intersections. Automotive Innovation, and Luige Vladareanu. Applying dijkstra algorithm for solving neu-3\(4\):374–385, 2020. 

trosophic shortest path problem. 

In 2016 International conference

\[30\] Xin Huang, Stephen G McGill, Jonathan A DeCastro, Luke Fletcher, on advanced mechatronic systems \(ICAMechS\), pages 412–416. IEEE, John J Leonard, Brian C Williams, and Guy Rosman. Diversitygan: 2016. 

Diversity-aware vehicle motion prediction via latent semantic sampling. 

\[50\] Steven M LaValle. Planning algorithms. Cambridge university press, IEEE Robotics and Automation Letters, 5\(4\):5089–5096, 2020. 

2006. 

\[31\] Constantin Hubmann, Jens Schulz, Marvin Becker, Daniel Althoff, 

\[51\] Qin Liu, Panlin Hou, Guojun Wang, Tao Peng, and Shaobo Zhang. 

and Christoph Stiller. Automated driving in uncertain environments: Intelligent route planning on large road networks with efficiency and Planning with interaction and uncertain maneuver prediction. IEEE

privacy. Journal of Parallel and Distributed Computing, 133:93–106, Transactions on Intelligent Vehicles, 3\(1\):5–17, 2018. 

2019. 

\[32\] Michael R Hafner, Drew Cunningham, Lorenzo Caminiti, and Domi-

\[52\] Jinglin Li, Dawei Fu, Quan Yuan, Haohan Zhang, Kaihui Chen, tilla Del Vecchio. 

Cooperative collision avoidance at intersections: Shu Yang, and Fangchun Yang. A traffic prediction enabled double Algorithms and experiments. IEEE Transactions on Intelligent Trans-rewarded value iteration network for route planning. IEEE Transactions portation Systems, 14\(3\):1162–1175, 2013. 

on Vehicular Technology, 68\(5\):4170–4181, 2019. 

\[33\] Tianhao Wu, Mingzhi Jiang, and Lin Zhang. Cooperative multiagent

\[53\] Awais Ahmad, Sadia Din, Anand Paul, Gwanggil Jeon, Moayad deep deterministic policy gradient \(comaddpg\) for intelligent connected Aloqaily, and Mudassar Ahmad. Real-time route planning and data transportation with unsignalized intersection. Mathematical Problems dissemination for urban scenarios using the internet of things. IEEE

in Engineering, 2020, 2020. 

Wireless Communications, 26\(6\):50–55, 2019. 

\[34\] Ziran Wang, Kyungtae Han, and Prashant Tiwari. Digital twin-assisted

\[54\] Mohammad Shokrolah Shirazi and Brendan Tran Morris. 

Looking

cooperative driving at non-signalized intersections. 

arXiv preprint

at intersections: a survey of intersection monitoring, behavior and arXiv:2105.01357, 2021. 

safety analysis of recent studies. 

IEEE Transactions on Intelligent

\[35\] Ran Tian, Nan Li, Ilya Kolmanovsky, Yildiray Yildiz, and Anouck R

Transportation Systems, 18\(1\):4–24, 2016. 

Girard. Game-theoretic modeling of traffic in unsignalized intersection

\[55\] Kurt M Dresner and Peter Stone. 

Sharing the road: Autonomous

network for autonomous vehicle control verification and validation. 

vehicles meet human drivers. In Ijcai, volume 7, pages 1263–1268, IEEE Transactions on Intelligent Transportation Systems, 2020. 

2007. 

\[36\] Nan Li, Yu Yao, Ilya Kolmanovsky, Ella Atkins, and Anouck R Girard. 

\[56\] Javier Alonso, Vicente Milanés, Joshué Pérez, Enrique Onieva, Carlos Game-theoretic modeling of multi-vehicle interactions at uncontrolled González, and Teresa De Pedro. Autonomous vehicle control systems intersections. IEEE Transactions on Intelligent Transportation Systems, for safe crossroads. Transportation research part C: emerging tech-2020. 

nologies, 19\(6\):1095–1110, 2011. 

\[37\] Constantin Hubmann, Marvin Becker, Daniel Althoff, David Lenz, and

\[57\] Georges S Aoude, Brandon D Luders, Kenneth KH Lee, Daniel S

Christoph Stiller. Decision making for autonomous driving considering Levine, and Jonathan P How. Threat assessment design for driver as-interaction and uncertain prediction of surrounding vehicles. In 2017

sistance system at intersections. In 13th International IEEE Conference IEEE Intelligent Vehicles Symposium \(IV\), pages 1671–1678. IEEE, on Intelligent Transportation Systems, pages 1855–1862. IEEE, 2010. 

2017. 

\[58\] Kazuhide Okamoto, Karl Berntorp, and Stefano Di Cairano. Driver

\[38\] Zhiqian Qiao, Katharina Muelling, John M Dolan, Praveen Palanisamy, intention-based vehicle threat assessment using random forests and and Priyantha Mudalige. Automatically generated curriculum based particle filtering. IFAC-PapersOnLine, 50\(1\):13860–13865, 2017. 

reinforcement learning for autonomous vehicles in urban environment. 

\[59\] Yang Li, Yang Zheng, Bernhard Morys, Shuyue Pan, Jianqiang Wang, In 2018 IEEE Intelligent Vehicles Symposium \(IV\), pages 1233–1238. 

and Keqiang Li. Threat assessment techniques in intelligent vehicles: IEEE, 2018. 

A comparative survey. IEEE Intelligent Transportation Systems Mag-

\[39\] David

Silver, 

Thomas

Hubert, 

Julian

Schrittwieser, 

Ioannis

azine, 2020. 

Antonoglou, Matthew Lai, Arthur Guez, Marc Lanctot, Laurent Sifre, 

\[60\] Piotr F Orzechowski, Annika Meyer, and Martin Lauer. 

Tackling

Dharshan Kumaran, Thore Graepel, et al. A general reinforcement occlusions & limited sensor range with set-based safety verification. 

learning algorithm that masters chess, shogi, and go through self-play. 

In 2018 21st International Conference on Intelligent Transportation Science, 362\(6419\):1140–1144, 2018. 

Systems \(ITSC\), pages 1729–1736. IEEE, 2018. 

\[40\] Ali Irshayyid, Jun Chen, and Guojiang Xiong. 

A review on rein-

\[61\] Yonghwan Jeong and Kyongsu Yi. Target vehicle motion prediction-forcement learning-based highway autonomous vehicle control. Green based motion planning framework for autonomous driving in uncon-Energy and Intelligent Transportation, page 100156, 2024. 

trolled intersections. IEEE Transactions on Intelligent Transportation

\[41\] Szilárd Aradi. 

Survey of deep reinforcement learning for motion Systems, 2019. 

planning of autonomous vehicles. IEEE Transactions on Intelligent

\[62\] Amirfarrokh Iranitalab and Aemal Khattak. 

Comparison of four

Transportation Systems, 23\(2\):740–759, 2020. 

statistical and machine learning methods for crash severity prediction. 

\[42\] Yiyang Chen, Chao Ji, Yunrui Cai, Tong Yan, and Bo Su. 

Deep

Accident Analysis & Prevention, 108:27–36, 2017. 

reinforcement learning in autonomous car path planning and control:

\[63\] Takayuki Osa, Joni Pajarinen, Gerhard Neumann, J Andrew Bagnell, A survey. arXiv preprint arXiv:2404.00340, 2024. 

Pieter Abbeel, and Jan Peters. An algorithmic perspective on imitation

\[43\] Jingda Wu, Chao Huang, Hailong Huang, Chen Lv, Yuntong Wang, learning. arXiv preprint arXiv:1811.06711, 2018. 

and Fei-Yue Wang. Recent advances in reinforcement learning-based

\[64\] Richard S Sutton and Andrew G Barto. Reinforcement learning: An autonomous driving behavior planning: A survey. 

Transportation

introduction. MIT press, 2018. 

IEEE JOURNAL TEMPLATE , VOL. –, NO. –, AUGUST 2023

20

\[65\] Yuanda Wang, Jia Sun, Haibo He, and Changyin Sun. Deterministic Intelligent Transportation Systems, 1:2–14, 2020. 

policy gradient with integral compensator for robust quadrotor control. 

\[85\] Abenezer Girma, Seifemichael Amsalu, Abrham Workineh, Mubbashar IEEE Transactions on Systems, Man, and Cybernetics: Systems, 2019. 

Khan, and Abdollah Homaifar. Deep learning with attention mech-

\[66\] K. Zhou, S. Song, A. Xue, K. You, and H. Wu. Smart train operation anism for predicting driver intention at intersection. arXiv preprint algorithms based on expert knowledge and reinforcement learning. 

arXiv:2006.05918, 2020. 

IEEE Transactions on Systems, Man, and Cybernetics: Systems, pages

\[86\] Niusha Pourjafari, Amir Ghafari, and Ali Ghaffari. 

Navigating

1–12, 2020. 

unsignalized intersections: A predictive approach for safe and cautious

\[67\] Tim de Bruin, Jens Kober, Karl Tuyls, and Robert Babuška. Integrating autonomous driving. IEEE Transactions on Intelligent Vehicles, 2023. 

state representation learning into deep reinforcement learning. IEEE

\[87\] Asher Bender, James R Ward, Stewart Worrall, and Eduardo M

Robotics and Automation Letters, 3\(3\):1394–1401, 2018. 

Nebot. Predicting driver intent from models of naturalistic driving. In

\[68\] Jiahong Chen, Tongxin Shu, Teng Li, and Clarence W de Silva. Deep 2015 IEEE 18th International Conference on Intelligent Transportation reinforced learning tree for spatiotemporal monitoring with mobile Systems, pages 1609–1615. IEEE, 2015. 

robotic wireless sensor networks. IEEE Transactions on Systems, Man, 

\[88\] Vijay Gadepally, Ashok Krishnamurthy, and Umit Ozguner. A frame-and Cybernetics: Systems, 2019. 

work for estimating driver decisions near intersections. IEEE Transac-

\[69\] Jinxin Liu, Yugong Luo, Hui Xiong, Tinghan Wang, Heye Huang, tions on Intelligent Transportation Systems, 15\(2\):637–646, 2013. 

and Zhihua Zhong. An integrated approach to probabilistic vehicle

\[89\] Nima Khairdoost, Mohsen Shirpour, Michael A Bauer, and Steven S

trajectory prediction via driver characteristic and intention estimation. 

Beauchemin. Real-time driver maneuver prediction using lstm. IEEE

In 2019 IEEE Intelligent Transportation Systems Conference \(ITSC\), Transactions on Intelligent Vehicles, 5\(4\):714–724, 2020. 

pages 3526–3532. IEEE, 2019. 

\[90\] Steven Beauchemin, M Bauer, Denis Laurendeau, T Kowsari, J Cho, 

\[70\] Yijing Wang, Zhengxuan Liu, Zhiqiang Zuo, Zheng Li, Li Wang, M Hunter, and O McCarthy. Roadlab: An in-vehicle laboratory for and Xiaoyuan Luo. 

Trajectory planning and safety assessment of developing cognitive cars. In Proc. 23rd Int. Conf. CAINE, 2010. 

autonomous vehicles based on motion prediction and model predictive

\[91\] Mozhgan Nasr Azadani and Azzedine Boukerche. A novel multimodal control. IEEE Transactions on Vehicular Technology, 68\(9\):8546–8556, vehicle path prediction method based on temporal convolutional net-2019. 

works. IEEE Transactions on Intelligent Transportation Systems, 2022. 

\[71\] Vinicius Trentin, Antonio Artu˜nedo, Jorge Godoy, and Jorge Villagra. 

\[92\] Wei Zhan, Liting Sun, Di Wang, Haojie Shi, Aubrey Clausse, Max-Interaction-aware intention estimation at roundabouts. IEEE Access, imilian Naumann, Julius Kummerle, Hendrik Konigshof, Christoph 9:123088–123102, 2021. 

Stiller, Arnaud de La Fortelle, and Masayoshi Tomizuka. Interaction

\[72\] Shun Yang, Wenshuo Wang, Chang Liu, and Weiwen Deng. Scene dataset: An international, adversarial and cooperative motion dataset in understanding in deep learning-based end-to-end controllers for au-interactive driving scenarios with semantic maps, 2019. 

tonomous vehicles. IEEE Transactions on Systems, Man, and Cyber-

\[93\] Atri Sarkar, Krzysztof Czarnecki, Matt Angus, Changjian Li, and netics: Systems, 49\(1\):53–63, 2018. 

Steven Waslander. Trajectory prediction of traffic agents at urban inter-

\[73\] Jinsoo Michael Yoo, Yonghwan Jeong, and Kyongsu Yi. Virtual target-sections through learned interactions. In 2017 IEEE 20th International based longitudinal motion planning of autonomous vehicles at urban Conference on Intelligent Transportation Systems \(ITSC\), pages 1–8. 

intersections: Determining control inputs of acceleration with human IEEE, 2017. 

driving characteristic-based constraints. IEEE Vehicular Technology

\[94\] Sebastian Brechtel, Tobias Gindele, and Rüdiger Dillmann. 

Prob-

Magazine, 16\(3\):38–46, 2021. 

abilistic decision-making under uncertainty for autonomous driving

\[74\] Carl-Johan Hoel, Tommy Tram, and Jonas Sjöberg. Reinforcement using continuous pomdps. In 17th international IEEE conference on learning with uncertainty estimation for tactical decision-making in intelligent transportation systems \(ITSC\), pages 392–399. IEEE, 2014. 

intersections. In 2020 IEEE 23rd international conference on intelligent

\[95\] Volkan Sezer, Tirthankar Bandyopadhyay, Daniela Rus, Emilio Fraz-transportation systems \(ITSC\), pages 1–7. IEEE, 2020. 

zoli, and David Hsu. Towards autonomous navigation of unsignalized

\[75\] Yonggang Liu, Pan Zhao, Datong Qin, Guang Li, Zheng Chen, and intersections under uncertainty of human driver intent. 

In 2015

Yi Zhang. Driving intention identification based on long short-term IEEE/RSJ International Conference on Intelligent Robots and Systems memory and a case study in shifting strategy optimization. 

IEEE

\(IROS\), pages 3578–3585. IEEE, 2015. 

Access, 7:128593–128605, 2019. 

\[96\] David Isele, Alireza Nakhaei, and Kikuo Fujimura. Safe reinforcement

\[76\] Alexander Trende, Anirudh Unni, Jochem Rieger, and Martin Fraenzle. 

learning on autonomous vehicles. 

In 2018 IEEE/RSJ International

Modelling turning intention in unsignalized intersections with bayesian Conference on Intelligent Robots and Systems \(IROS\), pages 1–6. IEEE, networks. In International Conference on Human-Computer Interac-2018. 

tion, pages 289–296. Springer, 2021. 

\[97\] Changjian Li and Krzysztof Czarnecki. 

Urban driving with multi-

\[77\] John M Scanlon, Rini Sherony, and Hampton C Gabler. Predicting objective deep reinforcement learning. In Proceedings of the 18th Inter-crash-relevant violations at stop sign–controlled intersections for the national Conference on Autonomous Agents and MultiAgent Systems, development of an intersection driver assistance system. Traffic injury pages 359–367. International Foundation for Autonomous Agents and prevention, 17\(sup1\):59–65, 2016. 

Multiagent Systems, 2019. 

\[78\] Zachary Richard Doerzaph. 

Development of a threat assessment

\[98\] Maxime Bouton, Alireza Nakhaei, Kikuo Fujimura, and Mykel J

algorithm for intersection collision avoidance systems. PhD thesis, Kochenderfer. Safe reinforcement learning with scene decomposition Virginia Tech, 2007. 

for navigating complex urban environments. In 2019 IEEE Intelligent

\[79\] Christian Laugier, Igor E Paromtchik, Mathias Perrollaz, Mao Yong, Vehicles Symposium \(IV\), pages 1469–1476. IEEE, 2019. 

John-David Yoder, Christopher Tay, Kamel Mekhnacha, and Amaury

\[99\] Julian Bernhard, Stefan Pollok, and Alois Knoll. Addressing inherent Nègre. Probabilistic analysis of dynamic scenes and collision risks uncertainty: Risk-sensitive behavior generation for automated driving assessment to improve driving safety. IEEE Intelligent Transportation using distributional reinforcement learning. In 2019 IEEE Intelligent Systems Magazine, 3\(4\):4–19, 2011. 

Vehicles Symposium \(IV\), pages 2148–2155. IEEE, 2019. 

\[80\] Stéphanie Lefèvre, Christian Laugier, and Javier Iba˜nez-Guzmán. Eval-

\[100\] Ian Osband, John Aslanides, and Albin Cassirer. Randomized prior uating risk at road intersections by detecting conflicting intentions. In functions for deep reinforcement learning. 

In Advances in Neural

2012 IEEE/RSJ International Conference on Intelligent Robots and Information Processing Systems, pages 8617–8629, 2018. 

Systems, pages 4841–4846. IEEE, 2012. 

\[101\] Pengfei Zhu, Xin Li, Pascal Poupart, and Guanghui Miao. 

On

\[81\] Alex Zyner, Stewart Worrall, James Ward, and Eduardo Nebot. Long improving deep reinforcement learning for pomdps. arXiv preprint short term memory for driver intent prediction. In 2017 IEEE Intelligent arXiv:1704.07978, 2017. 

Vehicles Symposium \(IV\), pages 1484–1489. IEEE, 2017. 

\[102\] Zhang-Wei Hong, Shih-Yang Su, Tzu-Yun Shann, Yi-Hsiang Chang, 

\[82\] Derek J Phillips, Tim A Wheeler, and Mykel J Kochenderfer. Gener-and Chun-Yi Lee. A deep policy inference q-network for multi-agent alizable intention prediction of human drivers at intersections. In 2017

systems. arXiv preprint arXiv:1712.07893, 2017. 

IEEE Intelligent Vehicles Symposium \(IV\), pages 1665–1670. IEEE, 

\[103\] Zhiqian Qiao, Katharina Muelling, John Dolan, Praveen Palanisamy, 2017. 

and Priyantha Mudalige. Pomdp and hierarchical options mdp with

\[83\] Alex Zyner, Stewart Worrall, and Eduardo Nebot. A recurrent neural continuous actions for autonomous driving at intersections. In 2018

network solution for predicting driver intention at unsignalized intersec-21st International Conference on Intelligent Transportation Systems tions. IEEE Robotics and Automation Letters, 3\(3\):1759–1764, 2018. 

\(ITSC\), pages 2377–2382. IEEE, 2018. 

\[84\] Yonghwan Jeong, Seonwook Kim, and Kyongsu Yi. Surround vehicle

\[104\] Maximilian Igl, Luisa Zintgraf, Tuan Anh Le, Frank Wood, and Shimon motion prediction using lstm-rnn for motion planning of autonomous Whiteson. Deep variational reinforcement learning for pomdps. In vehicles at multi-lane turn intersections. 

IEEE Open Journal of

International Conference on Machine Learning, pages 2117–2126. 

IEEE JOURNAL TEMPLATE , VOL. –, NO. –, AUGUST 2023

21

PMLR, 2018. 

learning, pages 1861–1870. PMLR, 2018. 

\[105\] Weilong Song, Guangming Xiong, and Huiyan Chen. Intention-aware

\[126\] Yunlong Song, HaoChih Lin, Elia Kaufmann, Peter Duerr, and Davide autonomous driving decision-making in an uncontrolled intersection. 

Scaramuzza. 

Autonomous overtaking in gran turismo sport using Mathematical Problems in Engineering, 2016, 2016. 

curriculum reinforcement learning. arXiv preprint arXiv:2103.14666, 

\[106\] Keqi Shu, Huilong Yu, Xingxin Chen, Shen Li, Long Chen, Qi Wang, 2021. 

Li Li, and Dongpu Cao. 

Autonomous driving at intersections: A

\[127\] Haochen Liu, Zhiyu Huang, and Chen Lv. 

Improved deep rein-

behavior-oriented critical-turning-point approach for decision making. 

forcement learning with expert demonstrations for urban autonomous IEEE/ASME Transactions on Mechatronics, 2021. 

driving. arXiv preprint arXiv:2102.09243, 2021. 

\[107\] Mathieu Barbier, Christian Laugier, Olivier Simonin, and Javier Iba˜nez-

\[128\] Henan Yuan, Penghui Li, Bart van Arem, Liujiang Kang, and Yongqi Guzmán. Probabilistic decision-making at road intersections: Formula-Dong. Safe, efficient, comfort, and energy-saving automated driving tion and quantitative evaluation. In 2018 15th International Conference through roundabout based on deep reinforcement learning. 

arXiv

on Control, Automation, Robotics and Vision \(ICARCV\), pages 795–

preprint arXiv:2306.11465, 2023. 

802. IEEE, 2018. 

\[129\] Yoshua Bengio, Jérôme Louradour, Ronan Collobert, and Jason We-

\[108\] Lingguang Wang, Carlos Fernandez, and Christoph Stiller. Learning ston. 

Curriculum learning. 

In Proceedings of the 26th annual

safe and human-like high-level decisions for unsignalized intersections international conference on machine learning, pages 41–48, 2009. 

from naturalistic human driving trajectories. IEEE Transactions on

\[130\] Shivesh Khaitan and John M. Dolan. State dropout-based curriculum Intelligent Transportation Systems, 2023. 

reinforcement learning for self-driving at unsignalized intersections. 

\[109\] Martin Treiber, Ansgar Hennecke, and Dirk Helbing. Congested traffic In 2022 IEEE/RSJ International Conference on Intelligent Robots and states in empirical observations and microscopic simulations. Physical Systems \(IROS\), pages 12219–12224, 2022. 

Review E, 62\(2\):1805–1824, August 2000. 

\[131\] Zengqi Peng, Xiao Zhou, Yubin Wang, Lei Zheng, Ming Liu, and

\[110\] Ming-Yuan Yu, Ram Vasudevan, and Matthew Johnson-Roberson. 

Jun Ma. Curriculum proximal policy optimization with stage-decaying Occlusion-aware risk assessment for autonomous driving in urban clipping for self-driving at unsignalized intersections, 2023. 

environments. IEEE Robotics and Automation Letters, 4\(2\):2235–2241, 

\[132\] Hyunki Seong, Chanyoung Jung, Seungwook Lee, and David Hyunchul 2019. 

Shim. Learning to drive at unsignalized intersections using attention-

\[111\] Ming-Yuan Yu, Ram Vasudevan, and Matthew Johnson-Roberson. Risk based deep reinforcement learning. 

In 2021 IEEE International

assessment and planning with bidirectional reachability for autonomous Intelligent Transportation Systems Conference \(ITSC\), pages 559–566, driving. arXiv preprint arXiv:1909.08059, 2019. 

2021. 

\[112\] Stephen G McGill, Guy Rosman, Teddy Ort, Alyssa Pierson, Igor

\[133\] Petar Veličković, Guillem Cucurull, Arantxa Casanova, Adriana Gilitschenski, Brandon Araki, Luke Fletcher, Sertac Karaman, Daniela Romero, Pietro Liò, and Yoshua Bengio. Graph attention networks, Rus, and John J Leonard. 

Probabilistic risk metrics for navigat-2018. 

ing occluded intersections. IEEE Robotics and Automation Letters, 

\[134\] Peide Cai, Hengli Wang, Yuxiang Sun, and Ming Liu. Dq-gat: Towards 4\(4\):4322–4329, 2019. 

safe and efficient autonomous driving with deep q-learning and graph

\[113\] David Isele, Reza Rahimi, Akansel Cosgun, Kaushik Subramanian, and attention networks. IEEE Transactions on Intelligent Transportation Kikuo Fujimura. Navigating occluded intersections with autonomous Systems, 23\(11\):21102–21112, 2022. 

vehicles using deep reinforcement learning. In 2018 IEEE International

\[135\] Meire Fortunato, Mohammad Gheshlaghi Azar, Bilal Piot, Jacob Conference on Robotics and Automation \(ICRA\), pages 2034–2039. 

Menick, Ian Osband, Alex Graves, Vlad Mnih, Remi Munos, Demis IEEE, 2018. 

Hassabis, Olivier Pietquin, Charles Blundell, and Shane Legg. Noisy

\[114\] Xiao Lin, Jiucai Zhang, Jin Shang, Yi Wang, Hongkai Yu, and networks for exploration, 2019. 

Xiaoli Zhang. 

Decision making through occluded intersections for

\[136\] Antonia Breuer, Jan-Aike Termöhlen, Silviu Homoceanu, and Tim autonomous driving. In 2019 IEEE Intelligent Transportation Systems Fingscheidt. opendd: A large-scale roundabout drone dataset, 2020. 

Conference \(ITSC\), pages 2449–2455. IEEE, 2019. 

\[137\] Maximilian Schier, Christoph Reinders, and Bodo Rosenhahn. Deep

\[115\] Danial Kamran, Carlos Fernandez Lopez, Martin Lauer, and Christoph reinforcement learning for autonomous driving using high-level hetero-Stiller. 

Risk-aware high-level decisions for automated driving at geneous graph representations. In 2023 IEEE International Conference occluded intersections with reinforcement learning. 

arXiv preprint

on Robotics and Automation \(ICRA\), pages 7147–7153, 2023. 

arXiv:2004.04450, 2020. 

\[138\] Jiaqi Liu, Peng Hang, Xiao Qi, Jianqiang Wang, and Jian Sun. Mtd-

\[116\] Maximilian

Naumann, 

Hendrik

Konigshof, 

Martin

Lauer, 

and

gpt: A multi-task decision-making gpt model for autonomous driving at Christoph Stiller. Safe but not overcautious motion planning under unsignalized intersections. In 2023 IEEE 26th International Conference occlusions and limited sensor range. In 2019 IEEE Intelligent Vehicles on Intelligent Transportation Systems \(ITSC\), pages 5154–5161. IEEE, Symposium \(IV\), pages 140–145. IEEE, 2019. 

2023. 

\[117\] Yonghwan Jeong, Kyongsu Yi, and Sungmin Park. Svm based intention

\[139\] Todd Hester, Matej Vecerik, Olivier Pietquin, Marc Lanctot, Tom inference and motion planning at uncontrolled intersection. 

IFAC-

Schaul, Bilal Piot, Dan Horgan, John Quan, Andrew Sendonaris, PapersOnLine, 52\(8\):356–361, 2019. 

Gabriel Dulac-Arnold, et al. Deep q-learning from demonstrations. 

\[118\] Keqi Shu, Huilong Yu, Xingxin Chen, Long Chen, Qi Wang, Li Li, and arXiv preprint arXiv:1704.03732, 2017. 

Dongpu Cao. Autonomous driving at intersections: A critical-turning-

\[140\] Ashvin Nair, Bob McGrew, Marcin Andrychowicz, Wojciech Zaremba, point approach for left turns. arXiv preprint arXiv:2003.02409, 2020. 

and Pieter Abbeel. Overcoming exploration in reinforcement learning

\[119\] Guofa Li, Shenglong Li, Shen Li, and Xingda Qu. 

Continuous

with demonstrations. 

In 2018 IEEE International Conference on decision-making for autonomous driving at intersections using deep Robotics and Automation \(ICRA\), pages 6292–6299. IEEE, 2018. 

deterministic policy gradient. IET Intelligent Transport Systems, 2021. 

\[141\] Zhiqian Qiao, Jeff Schneider, and John M Dolan. Behavior planning

\[120\] Xi Xiong, Jianqiang Wang, Fang Zhang, and Keqiang Li. Combining at urban intersections through hierarchical reinforcement learning. In deep reinforcement learning and safety based control for autonomous 2021 IEEE International Conference on Robotics and Automation driving. arXiv preprint arXiv:1612.00147, 2016. 

\(ICRA\), pages 2667–2673. IEEE, 2021. 

\[121\] Scott Fujimoto, Herke van Hoof, and David Meger. 

Addressing

\[142\] Maryam Zare, Parham M Kebria, Abbas Khosravi, and Saeid Naha-function approximation error in actor-critic methods, 2018. 

vandi. A survey of imitation learning: Algorithms, recent developments, 

\[122\] Shu-Yuan Xu, Xue-Mei Chen, Zi-Jia Wang, Yu-Hui Hu, and Xin-Tong and challenges. IEEE Transactions on Cybernetics, 2024. 

Han. Decision-making models for autonomous vehicles at unsignalized

\[143\] Jie Cheng, Yingbing Chen, Xiaodong Mei, Bowen Yang, Bo Li, and intersections based on deep reinforcement learning. In 2022 Interna-Ming Liu. Rethinking imitation-based planners for autonomous driving. 

tional Conference on Advanced Robotics and Mechatronics \(ICARM\), In 2024 IEEE International Conference on Robotics and Automation pages 672–677, 2022. 

\(ICRA\), pages 14123–14130. IEEE, 2024. 

\[123\] Tianbing Xu, Qiang Liu, Liang Zhao, and Jian Peng. Learning to

\[144\] Mohammad Al-Sharman, Rowan Dempster, Mohamed A Daoud, Mah-explore with meta-policy gradient, 2018. 

moud Nasr, Derek Rayside, and William Melek. 

Self-learned au-

\[124\] Volodymyr Mnih, Koray Kavukcuoglu, David Silver, Alex Graves, tonomous driving at unsignalized intersections: A hierarchical rein-Ioannis Antonoglou, Daan Wierstra, and Martin Riedmiller. 

Play-

forced learning approach for feasible decision-making. IEEE Transac-ing atari with deep reinforcement learning. 

arXiv

preprint

tions on Intelligent Transportation Systems, 2023. 

arXiv:1312.5602, 2013. 

\[145\] Zeyu Zhu and Huijing Zhao. 

A survey of deep rl and il for

\[125\] Tuomas Haarnoja, Aurick Zhou, Pieter Abbeel, and Sergey Levine. 

autonomous driving policy learning. IEEE Transactions on Intelligent Soft actor-critic: Off-policy maximum entropy deep reinforcement Transportation Systems, 23\(9\):14043–14065, 2021. 

learning with a stochastic actor. In International conference on machine

\[146\] Luc Le Mero, Dewei Yi, Mehrdad Dianati, and Alexandros Mouzakitis. 

IEEE JOURNAL TEMPLATE , VOL. –, NO. –, AUGUST 2023

22

A survey on imitation learning techniques for end-to-end autonomous Sensing, 196:146–177, 2023. 

vehicles. 

IEEE Transactions on Intelligent Transportation Systems, 

\[165\] B Ravi Kiran, Ibrahim Sobh, Victor Talpaert, Patrick Mannion, Ahmad 23\(9\):14128–14147, 2022. 

A Al Sallab, Senthil Yogamani, and Patrick Pérez. Deep reinforce-

\[147\] Zhiyu Huang, Jingda Wu, and Chen Lv. Efficient deep reinforcement ment learning for autonomous driving: A survey. 

arXiv preprint

learning with imitative expert priors for autonomous driving. IEEE

arXiv:2002.00444, 2020. 

Transactions on Neural Networks and Learning Systems, 2022. 

\[166\] Xuemin Hu, Shen Li, Tingyu Huang, Bo Tang, Rouxing Huai, and

\[148\] Daniel Krajzewicz, Jakob Erdmann, Michael Behrisch, and Laura Long Chen. How simulation helps autonomous driving: A survey of Bieker. Recent development and applications of sumo-simulation of sim2real, digital twins, and parallel intelligence. IEEE Transactions on urban mobility. 

International journal on advances in systems and Intelligent Vehicles, pages 1–20, 2023. 

measurements, 5\(3&4\), 2012. 

\[167\] Erica Salvato, Gianfranco Fenu, Eric Medvet, and Felice Andrea Pelle-

\[149\] Alexey Dosovitskiy, German Ros, Felipe Codevilla, Antonio Lopez, grino. Crossing the reality gap: A survey on sim-to-real transferability and Vladlen Koltun. Carla: An open urban driving simulator. arXiv of robot controllers in reinforcement learning. IEEE Access, 9:153171–

preprint arXiv:1711.03938, 2017. 

153187, 2021. 

\[150\] Teng Liu, Xingyu Mu, Bing Huang, Xiaolin Tang, Fuqing Zhao, Xiao

\[168\] Błażej Osiński, Adam Jakubowski, Paweł Ziecina, Piotr Miłoś, Christo-Wang, and Dongpu Cao. Decision-making at unsignalized intersection pher Galias, Silviu Homoceanu, and Henryk Michalewski. Simulation-for autonomous vehicles: Left-turn maneuver with deep reinforcement based reinforcement learning for real-world autonomous driving. In learning. arXiv preprint arXiv:2008.06595, 2020. 

2020 IEEE international conference on robotics and automation

\[151\] Maxime Bouton, Jesper Karlsson, Alireza Nakhaei, Kikuo Fujimura, \(ICRA\), pages 6411–6418. IEEE, 2020. 

Mykel J Kochenderfer, and Jana Tumova. 

Reinforcement learning

\[169\] Xinlei Pan, Yurong You, Ziyan Wang, and Cewu Lu. 

Virtual to

with probabilistic guarantees for autonomous driving. arXiv preprint real reinforcement learning for autonomous driving. arXiv preprint arXiv:1904.07189, 2019. 

arXiv:1704.03952, 2017. 

\[152\] Hong Shu, Teng Liu, Xingyu Mu, and Dongpu Cao. Driving tasks

\[170\] Xue Bin Peng, Marcin Andrychowicz, Wojciech Zaremba, and Pieter transfer using deep reinforcement learning for decision-making of Abbeel. Sim-to-real transfer of robotic control with dynamics ran-autonomous vehicles in unsignalized intersection. IEEE Transactions domization. In 2018 IEEE international conference on robotics and on Vehicular Technology, 2022. 

automation \(ICRA\), pages 1–8. IEEE, 2018. 

\[153\] Chi Zhang, Kais Kacem, Gereon Hinz, and Alois Knoll. Safe and

\[171\] Josh Tobin, Rachel Fong, Alex Ray, Jonas Schneider, Wojciech rule-aware deep reinforcement learning for autonomous driving at in-Zaremba, and Pieter Abbeel. Domain randomization for transferring tersections. In 2022 IEEE 25th International Conference on Intelligent deep neural networks from simulation to the real world. 

In 2017

Transportation Systems \(ITSC\), pages 2708–2715, 2022. 

IEEE/RSJ International Conference on Intelligent Robots and Systems

\[154\] Haochen Liu, Zhiyu Huang, Jingda Wu, and Chen Lv. 

Improved

\(IROS\), pages 23–30, 2017. 

deep reinforcement learning with expert demonstrations for urban

\[172\] S.P. Bhattacharyya. Robust control under parametric uncertainty: An autonomous driving. In 2022 IEEE intelligent vehicles symposium \(IV\), overview and recent results. Annual Reviews in Control, 44:45–77, pages 921–928. IEEE, 2022. 

2017. 

\[155\] Yingfeng Cai, Rong Zhou, Hai Wang, Xiaoqiang Sun, Long Chen, 

\[173\] Georgios D. Kontes, Daniel D. Scherer, Tim Nisslbeck, Janina Fischer, Yicheng Li, Qingchao Liu, and Youguo He. Rule-constrained reinforce-and Christopher Mutschler. 

High-speed collision avoidance using

ment learning control for autonomous vehicle left turn at unsignalized deep reinforcement learning and domain randomization for autonomous intersection. 

IET Intelligent Transport Systems, 17\(11\):2143–2153, vehicles. In 2020 IEEE 23rd International Conference on Intelligent 2023. 

Transportation Systems \(ITSC\), pages 1–8, 2020. 

\[156\] Mohamed A Daoud, Mohamed W Mehrez, Derek Rayside, and

\[174\] Samira Pouyanfar, Muneeb Saleem, Nikhil George, and Shu-Ching William W Melek. Simultaneous feasible local planning and path-Chen. Roads: Randomization for obstacle avoidance and driving in following control for autonomous driving. 

IEEE Transactions on

simulation. In Proceedings of the IEEE/CVF Conference on Computer Intelligent Transportation Systems, 2022. 

Vision and Pattern Recognition \(CVPR\) Workshops, June 2019. 

\[157\] Rowan Dempster, Mohammad Al-Sharman, Derek Rayside, and

\[175\] Alexander Amini, Igor Gilitschenski, Jacob Phillips, Julia Moseyko, William Melek. 

Real-time unified trajectory planning and optimal Rohan Banerjee, Sertac Karaman, and Daniela Rus. Learning robust control for urban autonomous driving under static and dynamic obstacle control policies for end-to-end autonomous driving from data-driven constraints. In 2023 IEEE International Conference on Robotics and simulation. IEEE Robotics and Automation Letters, 5\(2\):1143–1150, Automation \(ICRA\), pages 10139–10145. IEEE, 2023. 

2020. 

\[158\] Chaofang Hu, Lingxue Zhao, and Ge Qu. 

Event-triggered model

\[176\] Lerrel Pinto, James Davidson, Rahul Sukthankar, and Abhinav Gupta. 

predictive adaptive dynamic programming for road intersection path Robust adversarial reinforcement learning. 

In Doina Precup and

planning of unmanned ground vehicle. IEEE Transactions on Vehicular Yee Whye Teh, editors, Proceedings of the 34th International Con-Technology, 70\(11\):11228–11243, 2021. 

ference on Machine Learning, volume 70 of Proceedings of Machine

\[159\] Rolando Bautista-Montesano, Renato Galluzzi, Kangrui Ruan, Yongjie Learning Research, pages 2817–2826. PMLR, 06–11 Aug 2017. 

Fu, and Xuan Di. Autonomous navigation at unsignalized intersec-

\[177\] Xiangkun He, Baichuan Lou, Haohan Yang, and Chen Lv. Robust tions: A coupled reinforcement learning and model predictive control decision making for autonomous vehicles at highway on-ramps: A approach. 

Transportation research part C: emerging technologies, constrained adversarial reinforcement learning approach. IEEE Trans-139:103662, 2022. 

actions on Intelligent Transportation Systems, 24\(4\):4103–4113, 2023. 

\[160\] Kaizheng Wang, Yafei Wang, Lin Wang, Haiping Du, and Kanghyun

\[178\] Xinlei Pan, Daniel Seita, Yang Gao, and John Canny. Risk averse robust Nam. Distributed intersection conflict resolution for multiple vehicles adversarial reinforcement learning. In 2019 International Conference considering longitudinal-lateral dynamics. IEEE Transactions on Ve-on Robotics and Automation \(ICRA\), pages 8522–8528, 2019. 

hicular Technology, 70\(5\):4166–4177, 2021. 

\[179\] Konstantinos Bousmalis, Nathan Silberman, David Dohan, Dumitru

\[161\] Ahmed H Hamouda, Dalia M Mahfouz, Catherine M Elias, and Erhan, and Dilip Krishnan. Unsupervised pixel-level domain adaptation Omar M Shehata. Multi-layer control architecture for unsignalized with generative adversarial networks. 

In Proceedings of the IEEE

intersection management via nonlinear mpc and deep reinforcement conference on computer vision and pattern recognition, pages 3722–

learning. In 2021 IEEE International Intelligent Transportation Systems 3731, 2017. 

Conference \(ITSC\), pages 1990–1996. IEEE, 2021. 

\[180\] Chuqing Hu, Sinclair Hudson, Martin Ethier, Mohammad Al-Sharman, 

\[162\] Florian Heidecker, Jasmin Breitenstein, Kevin Rösch, Jonas Löhdefink, Derek Rayside, and William Melek. Sim-to-real domain adaptation for Maarten Bieshaar, Christoph Stiller, Tim Fingscheidt, and Bernhard lane detection and classification in autonomous driving. arXiv preprint Sick. 

An application-driven conceptualization of corner cases for arXiv:2202.07133, 2022. 

perception in highly automated driving. 

In 2021 IEEE Intelligent

\[181\] Yaroslav Ganin, Evgeniya Ustinova, Hana Ajakan, Pascal Germain, Vehicles Symposium \(IV\), pages 644–651. IEEE, 2021. 

Hugo Larochelle, Franc¸ois Laviolette, Mario Marchand, and Victor

\[163\] Matthew Pitropov, Danson Evan Garcia, Jason Rebello, Michael Smart, Lempitsky. 

Domain-adversarial training of neural networks. 

The

Carlos Wang, Krzysztof Czarnecki, and Steven Waslander. Canadian Journal of Machine Learning Research, 17\(1\):2096–2030, 2016. 

adverse driving conditions dataset. 

The International Journal of

\[182\] Alex Bewley, Jessica Rigley, Yuxuan Liu, Jeffrey Hawke, Richard Robotics Research, 40\(4-5\):681–690, 2021. 

Shen, Vinh-Dieu Lam, and Alex Kendall. 

Learning to drive from

\[164\] Yuxiao Zhang, Alexander Carballo, Hanting Yang, and Kazuya Takeda. 

simulation without real world labels. In 2019 International Conference Perception and sensing for autonomous vehicles under adverse weather on Robotics and Automation \(ICRA\), pages 4818–4824. IEEE, 2019. 

conditions: A survey. ISPRS Journal of Photogrammetry and Remote



# Document Outline

+ Introduction 
+ Background  
	+ Overview of decision-making in Autonomous Vehicles 
	+ Modeling the decision-making problem 
	+ Safety Assessment at Intersections 
	+ RL Approaches  
		+ Preliminaries 


+ Unsignalized Intersection-Traversal: Challenges and Solutions   
	+ Autonomous Driving Under Uncertainty 
	+ Driver Intention Inference Challenge 
	+ Decision Making Challenge  
		+ Partial Observability 
		+ Training in Continuous Action Space 
		+ Training in high-dimensional state-action space 


+ Discussion and Research Directions  
	+ Motion planning and Low-level control integration 
	+ Real-world experimental validation 

+ Conclusion



