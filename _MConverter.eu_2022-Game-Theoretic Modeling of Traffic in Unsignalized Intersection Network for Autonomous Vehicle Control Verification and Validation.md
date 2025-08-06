IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 23, NO. 3, MARCH 2022

2211

Game-Theoretic Modeling of Traffic in

Unsignalized Intersection Network

for Autonomous Vehicle Control

Verification and Validation

Ran Tian , Nan Li , *Member, IEEE*, Ilya Kolmanovsky , *Fellow, IEEE*, Yildiray Yildiz , *Senior Member, IEEE*, and Anouck R. Girard , *Senior Member, IEEE*

***Abstract*****— For a foreseeable future, autonomous vehicles \(AVs\)** in a virtual world so that the overall verification process can **will operate in traffic together with human-driven vehicles. **

be accelerated \[7\], \[8\]. The work of this paper is motivated **Their planning and control systems need extensive testing,** by the need for virtual testing of AV control systems. 

**including early-stage testing in simulations where the interac-In the near to medium term, AVs are expected to operate tions among autonomous/human-driven vehicles are represented. **
** **
**Motivated by the need for such simulation tools, we propose in traffic together with human-driven vehicles. Therefore, a game-theoretic approach to modeling vehicle interactions, accounting for the interactions among autonomous/human-in particular, for urban traffic environments with unsignalized** driven vehicles is important to achieve safe and efficient **intersections. We develop traffic models with heterogeneous \(in** driving behavior of an AV. 

**terms of their driving styles\) and interactive vehicles based on our** Control strategies for AVs that account for vehicle interac-proposed approach, and use them for virtual testing, evaluation, **and calibration of AV control systems. For illustration, we con-tions include the ones based on Markov decision processes sider two AV control approaches, analyze their characteristics**
** 
\[9\]–\[12\], model predictive control \[13\], \[14\], game-theoretic and performance based on the simulation results with our devel-models \[15\]–\[18\], \[18\], \[19\], as well as data-driven approaches oped traffic models, and optimize the parameters of one of them. 

\[20\], \[21\]. To evaluate the effectiveness of these algorithms

*Index Terms*— Autonomous vehicles, decision making, game requires simulation environments that can represent the inter-theory, human factors, multi-agent systems, system testing. 

actions among autonomous/human-driven vehicles. 

In our previous work \[22\], we exploited a game-theoretic I. INTRODUCTION

approach to modeling vehicle interactions in highway traffic. 

AUTONOMOUS driving technologies have greatly Compared to highway traffic, urban traffic environments advanced

in

recent

years

with

the

promise

of

with intersections are considered to be more challenging providing

safer, 

more

efficient, 

environment-friendly, 

for both human drivers and AVs, as they involve more and easily accessible transportation \[1\]–\[3\]. To fulfill such extensive and complex interactions among vehicles. For a commitment requires developing advanced planning and instance, almost 40% of traffic accidents in the U.S. are control algorithms to navigate autonomous vehicles \(AVs\), intersection-related \[23\]. 

as well as comprehensive testing procedures to verify their In this paper, we extend the game-theoretic approach of \[22\]

safety and performance characteristics \[4\]–\[6\]. It is estimated to modeling vehicle interactions in urban traffic. In particular, based on the collision fatalities rate that to confidently verify we consider urban traffic environments with unsignalized inter-an AV control system, hundreds of millions of miles need sections. Firstly, unsignalized intersections may be even more to be driven \[4\], which can be highly time and resource challenging than signalized intersections because, due to the consuming if these driving tests are all conducted in the lack of guidance from traffic signals, a driver/automation needs physical world. Therefore, an alternative solution is to use to decide on its own, whether, when and how to enter and simulation tools to conduct early-stage testing and evaluation drive through the intersection. According to the U.S. Federal Highway Administration’s report, almost 70% of fatalities due Manuscript received October 13, 2019; revised July 12, 2020; accepted to intersection-related traffic accidents happened at unsignal-October 8, 2020. Date of publication November 17, 2020; date of current version March 9, 2022. This work was supported by the National Science ized intersections \[24\]. Thus, well-verified autonomous driving Foundation under Grant CNS 1544844. The Associate Editor for this article systems for unsignalized intersections may deliver significant was N. Geroliminis. *\(Corresponding author: Ran Tian.\)* safety benefits. Indeed, many previous works in the literature Ran Tian, Nan Li, Ilya Kolmanovsky, and Anouck R. Girard are with the Department of Aerospace Engineering, University of Michigan, Ann on AV control for intersections, including \[19\], \[25\]–\[28\], deal Arbor, MI

48109 USA \(e-mail: tianran@umich.edu; nanli@umich.edu; with unsignalized intersections, although they do not always ilya@umich.edu; anouck@umich.edu\). 

explicitly point this out. 

Yildiray Yildiz is with the Department of Mechanical Engineering, Bilkent University, 06800 Ankara, Turkey \(e-mail: yyildiz@bilkent.edu.tr\). 

Our approach formulates the decision-making processes Digital Object Identifier 10.1109/TITS.2020.3035363

of drivers/vehicles as a dynamic game, where each vehicle 1558-0016 © 2020 IEEE. Personal use is permitted, but republication/redistribution requires IEEE permission. 

See https://www.ieee.org/publications/rights/index.html for more information. 

Authorized licensed use limited to: ULAKBIM UASL - Bilkent University. Downloaded on December 26,2022 at 14:48:10 UTC from IEEE Xplore. Restrictions apply. 

2212

IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 23, NO. 3, MARCH 2022

interacts with other vehicles by observing their states, predict-when a vehicle drives through multiple road segments, such as ing their future actions, and then planning its own actions. 

overall travel time, fuel consumption, etc. A road system with In addition to the difference in traffic scenarios being consid-15 intersections and 30 vehicles is illustrated as an example in ered \(i.e., urban traffic in this paper versus highway traffic in Section IV. Furthermore, application of the developed traffic

\[22\]\), this paper contains the following methodological contri-models to verification and validation of AV control systems is bution compared to \[22\]: Due to the much larger state space comprehensively discussed in this paper, but not in \[35\]. 

for urban traffic environments with intersections compared to Preliminary results of this paper have been reported in the that for highway traffic, the reinforcement learning approach conference papers \[38\] and \[39\]. The results modeling the used in \[22\] to solve for control policies is computationally interactions between two vehicles at a four-way intersection prohibitive. Therefore, we develop in this paper an alternative are reported in \[38\] and those for two vehicles at a roundabout approach that uniquely integrates a game-theoretic formalism, intersection are in \[39\]. This paper generalizes the methodol-receding-horizon optimization, and an imitation learning algo-ogy to modeling the interactions among multiple \(more than rithm to obtain control policies. This new approach is shown two\) vehicles and to an additional intersection type – T-shaped to be computationally effective for the large state space of intersection. Constructing larger road systems based on the urban traffic. 

models of these three intersections is reported for the first time Our model representing vehicle interactions falls in-between in this paper. This paper also demonstrates how the developed macroscopic traffic models and microscopic driver behavior traffic models can be used for virtual testing, evaluation, and models. On the one hand, macroscopic traffic models typi-calibration of AV control systems, which is not provided in cally assume a large number \(e.g., hundreds to thousands\) of

\[38\] and \[39\]. 

vehicles and study the average or statistical properties of traffic In summary, the contributions of this paper are: 1\) We flow, such as traffic flux \(vehicles/hour\) versus traffic density describe an approach based on level-k game theory to mod-

\(vehicles/km\) \[29\]–\[31\]. Individual vehicle behavior is usually eling the interactions among vehicles in urban traffic envi-not represented in such models. On the other hand, micro-ronments with unsignalized intersections. 2\) We propose an scopic driver behavior models typically focus on modeling algorithm based on imitation learning to obtain level- *k * control the decision-making as well as control processes of individual policies so that our approach to modeling vehicle interactions drivers \[32\]–\[34\], such as the responses of a human driver is scalable – able to model traffic scenes with many inter-to various traffic situations. The interactions among multiple sections and many vehicles. In particular, this new imitation vehicles are usually not incorporated in such models. Con-learning approach is compared with the supervised learning sequently, neither models are particularly suitable for virtual approach used in our previous work \[39\] and is shown to pro-testing of AV control systems. In contrast, our game-theoretic vide better results. 3\) We demonstrate the use of the developed model represents the interactive decision-making processes traffic models for virtual testing, evaluation, and calibration of multiple drivers/vehicles, where each individual vehicle’s of AV control systems. For illustration purposes, we consider behavior is represented using a kinematic vehicle model. This two AV control approaches, analyze their characteristics and way, we can model traffic scenes with a medium number performance based on the simulation results with our traffic \(e.g., dozens\) of interacting vehicles, suitable as test scenarios models, and optimize the parameters of one of them. 

for AV control systems. 

This paper is organized as follows: The models representing In \[35\], we modeled the interactions among vehicles at vehicle kinematics and driver decision-making processes are unsignalized intersections, but using a different game-theoretic introduced in Section II. The game-theoretic model represent-approach from the one used in this paper. Specifically, in \[35\], ing vehicle interactions and obtaining its explicit approxima-we modeled vehicle interactions based on a formulation of a tion via imitation learning are discussed in Section III. The leader-follower game; while in this paper, we consider the procedure to construct traffic models of larger road systems application of level-k game theory \[36\], \[37\]. The control based on the models of three basic intersection scenarios is strategies of all interacting vehicles modeled using the frame-described in Section IV. We then propose two AV control work of \[35\] are homogeneous; while the control strategies of approaches in Section V, used as case studies to illustrate different vehicles modeled using the scheme of this paper are the application of our developed traffic models to AV control heterogeneous, differentiated by their level- *k * control policies verification and validation. Simulation results are reported in with different *k *= 0 *, * 1 *, * 2 *, . . . * This heterogeneity can be Section VI, and finally, the paper is concluded in Section VII. 

used to represent the different driving styles among different drivers, e.g., aggressive driving versus cautious/conservative II. TRAFFIC DYNAMICS AND DRIVER DECISION-MAKING

driving. In addition, \[35\] models a single intersection with MODELING

up to 10 interacting vehicles; while in this paper, thanks In this section, we describe our models to represent the traf-to the effective application of the aforementioned solution fic dynamics and the decision-making processes of interacting approach integrating game theory, receding-horizon optimiza-drivers. 

tion, and imitation learning to obtain control policies, the *A. Traffic Dynamics*

scheme of this paper can be used to model much larger road systems involving many intersections and many vehicles Firstly, we describe the evolution of a traffic scenario using with manageable online computational effort. This enables a discrete-time model as follows:

the investigation into driving characteristics that are exhibited s *t*\+1 = *F\(*s *t , *u *t \),* \(1\)

Authorized licensed use limited to: ULAKBIM UASL - Bilkent University. Downloaded on December 26,2022 at 14:48:10 UTC from IEEE Xplore. Restrictions apply. 

TIAN *et al. *: GAME-THEORETIC MODELING OF TRAFFIC IN UNSIGNALIZED INTERSECTION NETWORK

2213

where s = *\(s* 1 *, s* 2 *, . . . , sm\) * denotes the traffic state, composed states and actions of the other vehicles *j *∈ *M*, *j *= *i *, i.e., of the states *si *, *i *∈ *M *= \{1 *, * 2 *, . . . , m*\}, of all interacting *j*

*j*

s− *i*

*ο*| = *\(s \)*

= *\(u \)*

*t*

*ο*| *t j*∈ *M, j*= *i * and u− *i* *ο*| *t*

*ο*| *t j*∈ *M, j*= *i *; *R * is a reward vehicles in the scenario, u = *\(u* 1 *, u* 2 *, . . . , um\) * denotes the function depending on the states and actions of all interacting collection of all vehicles’ actions *ui *, and the subscript *t* vehicles, which will be introduced in detail in the following represents the discrete-time instant. In particular, the state of section; and *λ *∈ *\(* 0 *, * 1\] is a factor discounting future reward. 

a vehicle is composed of two parts, *si *= *\(si, * 1 *, si, * 2 *\)*. The Once an optimal action sequence *\(*u *i \)*∗

*t*

is determined, 

first part *si, * 1 = *\(xi , yi , vi , θi \) * represents the state of vehicle vehicle *i * applies the first element *\(ui \)*∗ for one time step, 0| *t*

kinematics, modeled using the following unicycle model: i.e., *ui *= *\(ui \)*∗. After the states of all vehicles have been

⎡

⎤

⎡



⎤

*t*

0| *t*

*x i*

*x i *\+ *vi*

*θi t*

updated, vehicle *i * repeats this procedure at *t *\+ 1. 

⎢ *t*\+1

*t*

*t * cos

*t*



The fact that *R * depends not only on the ego vehicle’s

⎢ *yi *⎥

⎥

⎢

⎢ *yi *\+ *vi*

*θi t *⎥

⎥

⎣ *t*\+1

*t*

*t * sin

*t*

*v*

*, \) *=

*i*

⎦ = *f \(sit uit*

⎣

*vi *\+

state and action but also on those of the other vehicles deter-ai t

⎦ *, *

\(2\)

*t *\+1

*t*

*t*

*θi*

*θi *\+ *ωi *

mines the interactive nature of the drivers’ decision-making *t*

*t *\+1

*t*

*t*

processes in a multi-vehicle traffic scenario. Note that, due where *\(xi , yi \)*, *vi *, and *θi * represent, respectively, the vehi-to the unknowns u− *i*

*ο*| and s− *i * for *ο *= 0 *, * 1 *, . . . , N *− 1, *t*

*ο*| *t*

cle’s position in the ground-fixed frame, its speed, and its the problem \(3\) has not been well-defined yet and cannot heading angle, the inputs *ai * and *ωi * represent, respectively, be solved. To be able to solve for *\(*u *i \)*∗

*t*

, we will exploit a

the vehicle’s acceleration and heading angle rate, while *t* game-theoretic approach in Section III to predict the values of is the sampling period for decision-making. The second part u− *i*

*ο*| and s− *i *. 

*t*

*ο*| *t*

*si, * 2 = *\(ri , ξi \) * contains additional information related to the vehicle’s decision-making objective, including *r i *= *\(ri , \)* *x r iy *, 

*C. Reward Function*

representing a target/reference position to go, and *ξi *, a feature We use the reward function *R * in \(3\) to represent vehicles’

vector containing key information about the road layout and decision-making objectives in traffic. In this paper, we consider geometry such as the road width, the angle of intersection, *R * defined as follows:

and etc \[35\]. When vehicle *i * is driving toward, in the middle of, or exiting a specific intersection, *si, * 2 stays constant with *r i* *j*

*R\(si , *s− *i , ui , *u− *i \) *= w * si*

*, \(s*

*\)j*∈ *M,j*= *i , *\(4\)

being a point located in the center of the vehicle’s target lane; *ο*| *t*

*ο*| *t*

*ο*| *t*

*ο*| *t*

*ο*\+1| *t*

*ο*\+1| *t*

*si, * 2 gets updated after the vehicle has returned to straight road where * *= \[ *φ* 1 *, φ* 2 *, . . . , φ* 6\] is the feature vector and w ∈ R6\+

and is driving toward the next intersection. 

*j*

*j*

*j*

is the weight vector. Note that *s*

= *f \(s , u \) * for all

We remark that the unicycle model \(2\) is suitable for our *ο*\+1| *t*

*ο*| *t*

*ο*| *t*

*j *∈ *M * based on the kinematic vehicle model \(2\). 

purpose of modeling the interactive decision-making processes The features *φ*

and the resulting dynamic behavior of multiple vehicles in 1 *, φ* 2 *, . . . , φ* 6 are designed to encode common considerations in driving, such as safety, comfort, travel time, intersection traffic scenarios. This model is simple while it etc. They are defined as follows. 

can sufficiently accurately represent vehicle kinematics at low The feature *φ*

to medium vehicle speeds and involving turning behavior \[16\], 1 characterizes the collision status of the

vehicle. In particular, we over-bound the geometric contour of

\[40\]. In Section VI we show that 1\) driving behaviors planned each vehicle by a rectangle, referred to as the collision-zone based on the model \(2\) can be accurately executed by vehicle \( *c*-zone\). Then, *φ*

systems with lower-level control, and 2\) vehicle trajectories 1 = −1 if vehicle *i *’s *c*-zone at the predicted state *si*

overlaps with any of the other vehicles’ *c*-zones extracted from real-world traffic data can be satisfactorily *ο*\+1| *t*

*j*

reproduced by simulating the model \(2\) along with the deci-at their predicted states *sο*\+ , which indicates a danger of 1| *t*

sion logic developed following our approach. 

collision; and *φ* 1 = 0 otherwise. The *c*-zone over-bounds the vehicle’s geometric contour by a small margin to compensate for the effect of perception errors. Note that the size of these *B. Driver Decision-Making*

perception errors is small at low to medium vehicle speeds An action *ui * is a pair of values of the inputs *\(ai , ωi \)*, i.e., when compared to the resolution of the actions. 

*ui *= *\(ai , ωi \)*. We assume that the drivers of the vehicles make The feature *φ* 2 characterizes the on-road status of the sequential decisions based on receding-horizon optimization as vehicle, taking −1 if vehicle *i *’s *c*-zone crosses any of the road follows: At each discrete-time instant *t*, the driver of vehicle boundaries, and 0 otherwise. And similarly, *φ* 3 characterizes *i * solves for



the in-lane status of the vehicle. If vehicle *i *’s *c*-zone crosses *\(*u *i\)*∗ = *\(*

*\)*∗ *, \(*

*\)*∗ *, . . . , \(*

*\)*∗

a lane marking that separates the traffic of opposite directions *t*

*ui*

*ui*

*ui*

0| *t*

1| *t*

*N *−1| *t*

or enters a lane different from its target lane when exiting an *N *−1



∈

intersection, then *φ*

arg max

*λο R\(si*

3 = −1; *φ* 3 = 0 otherwise. 

*ο*| *, *s− *i , ui , *u− *i \),* *t*

*ο*|

\(3\)

*t*

*ο*| *t*

*ο*| *t*
**
**To characterize the status of maintaining a safe and com-u** *i *∈ *U N*

*t*

*ο*=0





fortable separation between vehicles, we further define a where **u** *i *=

*, *

*, . . . , *

*t*

*ui*

*ui*

*ui*

represents a sequence of

0| *t*

1| *t*

*N *−1| *t*

separation-zone \( *s*-zone\) for each vehicle, which over-bounds predicted actions of vehicle *i *, with *uiο*| denoting the predicted the vehicle’s *c*-zone with a separation margin. The feature *t*

action for time step *t *\+ *ο * and taking values in a finite action set *φ* 4 takes −1 if vehicle *i*’s *s*-zone overlaps with any of the *U*; the notations *siο*| , **s**− *i * and **u**− *i * represent, respectively, the other vehicles’ *s*-zones at their predicted states, and takes 0

*t*

*ο*| *t*

*ο*| *t*

predicted state of vehicle *i *, and the collections of predicted otherwise. 

Authorized licensed use limited to: ULAKBIM UASL - Bilkent University. Downloaded on December 26,2022 at 14:48:10 UTC from IEEE Xplore. Restrictions apply. 

2214

IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 23, NO. 3, MARCH 2022

The features *φ* 5 and *φ* 6 characterize the vehicle’s sta-the level-0 decision rule \(for *k *= 1\), and *k* max is the highest tus of driving toward its target lane. They are defined as reasoning level for computation. 

*φ* 5 = − | *ri *−

−

*x*

*x i *| − | *riy*

*yi *| and *φ* 6 = *vi *, so that the vehicle Given a finite action set *U*, the problem \(5\) for every *i *∈ *M*

is encouraged to approach the reference point *r i * in its target and *k *= 1 *, * 2 *, . . . , k* max can be solved with exhaustive search, lane as quickly as it can. 

e.g., based on a tree structure \[43\]. 

The above reward function design reflects common driving objectives in traffic. The weight vector **w **can be tuned to *B. Explicit Level-k Decision-Making via Imitation Learning* achieve reasonable driving behavior, or be calibrated using A level- *k * vehicle drives in traffic by applying *ui *= *\(ui \)k* traffic data and approaches such as inverse reinforcement *t*

0| *t*

at every time step, where *\(ui \)k * is determined according to learning \[41\], \[42\]. 

0| *t*

\(5\) with the current state as the initial condition, i.e., *si*

= *si*

0| *t*

*t*

III. GAME-THEORETIC DECISION-MAKING AND EXPLICIT

and **s**− *i *= **s**− *i*

0| *t*

*t*

. 

REALIZATION VIA IMITATION LEARNING

On the one hand, the problem \(5\) needs to be numerically solved. The required computational effort to solve \(5\) grows Game theory is a useful tool for modeling intelligent agents’

for larger *k * and larger numbers of interacting vehicles, because strategic interactions. In this paper, we exploit the level-k in order to compute the level- *k * decision of vehicle *i *, the game theory \[36\], \[37\] to model vehicles’ interactive decision-level-\( *k *− 1\) decisions of all other vehicles *j *= *i * need making. 

to be determined first, which, in turn, need the prerequisite determination of level-\( *k *− 2\) decisions for *k *≥ 2, and *A. Level-k Reasoning and Decision-Making*

etc. On the other hand, for virtual testing of AV control In level-k game theory, it is assumed that players make systems, fast simulations are desired so that a large number decisions based on finite depths of reasoning, called “level,” 

of test scenarios can be covered within a short period of real and different players may have different reasoning lev-time. To achieve fast simulations, we exploit machine learning els. In particular, a level-0 player makes non-strategic techniques to move the computational tasks associated with \(5\) decisions – decisions without regard to the other players’

offline and obtain explicit level- *k * decision policies for online decisions. Then, a level- *k*, *k *≥ 1, player makes strategic use. 

decisions by assuming that all of the other players are level-In particular, we define a policy as a map from a triple of \( *k *−1\), predicting their decisions based on such an assumption, the ego vehicle’s state *sit *, the other vehicles’ states **s**− *i* *t*

, and

and optimally responding to their predicted decisions. It is the ego vehicle’s reasoning level *k * to the level- *k * action of the verified by experimental results from cognitive science that ego vehicle, i.e. 

such a level-k reasoning process can model human interactions *π*

*, ***s**− *i , k\) *→ *\(ui\)k. *

\(6\)

with higher accuracy than traditional analytic methods in many k : *\(sit*

*t*

*t*

cases \[37\]. 

This map is algorithmically determined by solving the problem To incorporate level-k reasoning in our decision-making \(5\) and letting *\(ui \)k *= *\(*

*\)k*

*t*

*ui*

. In what follows, we pursue an

0| *t*

model \(3\), we start with defining a level-0 decision rule. 

explicit approximation of *π* k, denoted by ˆ *π* k, exploiting the According to the non-strategic assumption on level-0 players, approach called “imitation learning.” 

we let a level-0 decision of a vehicle *i *, *i *∈ *M*, depend Imitation learning is an approach for an autonomous agent only on the traffic state **s** *t *, including its own state *sit * and to learn a control policy from expert demonstrations to imitate the other vehicles’ states **s**− *i*

*t*

, but not on the other vehi-

expert’s behavior. The expert can be a human expert \[44\] or a cles’ actions **u**− *i*

*t*

. In this paper, a level-0 decision, *\(***u** *i \)* 0 =

*t*





well-behaved artificial intelligence \[45\]. In this paper, we treat *\(ui \)* 0 *, \(ui \)* 0 *, . . . , \(ui*

*\)* 0 , is a sequence of predicted

0| *t*

1| *t*

*N *−1| *t*

the algorithmically determined map *π* k as the expert. 

actions that maximizes the cumulative reward in \(3\) with Imitation learning can be formulated as a standard super-treating all of the other vehicles as stationary obstacles over vised learning problem, in which case it is also commonly the planning horizon, i.e., *v jο*| = 0, *ω j *= 0 for all *j *= *i*, *t*

*ο*| *t*

referred to as “behavioral cloning,” where the learning objec-ο = 0 *, * 1 *, . . . , N*. This way, a level-0 vehicle represents an tive is to obtain a policy from a pre-collected dataset of expert aggressive vehicle which assumes that all of the other vehicles demonstrations that best approximates the expert’s behavior at will yield the right of way to it. 

the states contained in the dataset. Such a procedure can be On the basis of the formulated level-0 decision rule, the described as

level- *k * decisions of the vehicles are obtained based on ˆ *π* k ∈ argmin E ¯**s**∼P *\(*¯**s**| *π L\(π* k *\(*¯**s** *\), πθ\(*¯**s** *\)\) ,* \(7\)

*\(*

k *\)*

**u** *i \)k *= *\(*

*\)k, \(*

*\)k, . . . , \(*

*\)k*

*πθ*

*t*

*ui*

*ui*

*ui*

0| *t*

1| *t*

*N *−1| *t*

*N *−1





where ¯**s **denotes the triple *\(si , ***s**− *i , k\)*, *π* k denotes the

∈ arg max

*λο R siο*| *, ***s**− *i , ui , \(***u**− *i \)k*−1 *,* *t*

*ο*|

\(5\)

*t*

*ο*| *t*

*ο*| *t*

expert policy \(6\), *πθ * denotes a policy parameterized by *θ*

**u** *i *∈ *U N*

*t*

*ο*=0

\(e.g., the weights of a neural network\) that is being evalu-for every *i *∈ *M*, and for every *k *= 1 *, * 2 *, . . . , k* ated and optimized, *L * is a loss function, and the notation max through

sequential, iterated computations, where *\(***u**− *i* E

*ο*| *\)k*−1 denotes the

¯**s**∼P *\(*¯**s**| *π*

*t*

k *\)\(*· *\) * is defined as



level-\( *k *− 1\) decisions of the other vehicles *j *= *i *, which have been determined either in the previous iteration or based on E ¯**s**∼P *\(*¯**s**| *π*

*\(*· *\) * dP *\(*¯**s**| *π*

k *\)\(*· *\) *=

k *\). *

\(8\)

Authorized licensed use limited to: ULAKBIM UASL - Bilkent University. Downloaded on December 26,2022 at 14:48:10 UTC from IEEE Xplore. Restrictions apply. 





TIAN *et al. *: GAME-THEORETIC MODELING OF TRAFFIC IN UNSIGNALIZED INTERSECTION NETWORK

2215

We remark that a key feature of the procedure \(7\) is that **Algorithm 1 **Imitation Learning Algorithm to Obtain the expectation is with respect to the probability distribution Explicit Level- *k * Decision Policies

P *\(*¯**s**| *π* k *\) * of the data ¯**s **determined by the expert policy *π* k, which **1 **Initialize ˆ

*π* 0 to an arbitrary policy; 

is essentially the empirical distribution of ¯**s **in the pre-collected k

**2 **Initialize dataset *D *← ∅; 

dataset. 

**3 for ** *n *= 1 : *n* max **do** In our previous work \[39\], we have explored the procedure **4**

Initialize the simulation environment; 

\(7\) to obtain an explicit policy that imitates level- *k * decisions **5**

**for ** *i *∈ *M ***do**

for an autonomous vehicle to drive through a roundabout **6**

Initialize vehicle *i *; 

intersection. 

**7**

## **end for**

Using \(7\) to train the policy ˆ *π* k has a drawback in that **8**

**for ** *t *= 0 : *t* max − 1 **do** only the states that can be reached by executing the expert **9**

**for ** *i *∈ *M ***do**

policy *π* k will be included in the dataset, and such a sampling **10**

**if ** *vehicle i fails or succeeds ***then** bias may cause the error between ˆ *π* k and *π* k to propagate **11**

Re-initialize vehicle *i *; 

in time. In particular, a small error may cause the vehicle to **12**

## **end if**

reach a state that is not exactly included in the dataset and, **13**

**for ** *k *= 1 : *k* max **do**

consequently, a large error may occur at the next time step. 

## **14**

**if **ˆ *πn*−1 *\(si , ***s**− *i , k\) *= *π* k *\(si , ***s**− *i , k\) ***then** Therefore, in this paper we consider an alternative approach, k

*t*

*t*

*t*

*t*





## **15**

*D *← *D *∪ *\(si, ***s**− *i, k\), π*

*, ***s**− *i, k\)*

based on the “Dataset Aggregation” \(DAgger\) algorithm, *t*

*t*

k *\(sit*

*t*

**16**

## **end if**

### to train the policy ˆ

*π* k. DAgger is an iterative algorithm that **17**

## **end for**

optimizes the policy under its induced state distribution \[46\]. 

## **18**

Randomly generate *k*

The learning objective of DAgger can be described as *t *∈ \{1 *, . . . , k* max\}; 





## **19**

### ***si***

= *f si, * ˆ *πn*−1 *\(si, ***s**− *i, k *; *t *\+1

*t*

k

*t*

*t*

*t \)*

ˆ *π* k ∈ argmin E ¯**s**∼P *\(*¯**s**| *π L\(π* k *\(*¯**s** *\), πθ\(*¯**s** *\)\) ,* \(9\)

**20**

## **end for**

### ***π***

*θ \)*

*θ*



**21**

## **end for**

E ¯

## **22**

Train classifier ˆ *πn * on *D*; 

**s**∼P *\(*¯**s**| *π*

*\(*· *\)*

*θ \)\(*· *\) *=

dP *\(*¯**s**| *πθ \), *

\(10\)

k

## **23 end for**

where the distinguishing feature from \(7\) is that the expec-24 Output ˆ

*π* k = ˆ *πn* max. 

k

tation is with respect to the probability distribution P *\(*¯**s**| *πθ \)* induced from the policy *πθ * that is being evaluated and optimized. DAgger can effectively resolve the aforementioned issue with regard to the propagation of error in time, since there will be data points *\(*¯**s** *, π* k *\(*¯**s** *\)\) * for states ¯**s **reached by executing ˆ

*π* k. 

The procedure to obtain explicit level- *k * decision policies based on an improved version of DAgger algorithm \[45\] is presented as Algorithm 1. In Algorithm 1, *n* max denotes the maximum number of simulation episodes and *t* max represents the length of a simulation episode. By “initialize the simulation Fig. 1. Unsignalized intersections to be modeled: \(a\) four-way, \(b\) T-shaped, environment,” we mean constructing a traffic scene, including and \(c\) roundabout. 

specifying the road layout and geometry as well as the number of vehicles. By “initialize vehicle *i *,” we mean putting the virtual testing of AV control systems, which will be introduced vehicle in a lane entering the scene while satisfying a minin Section V. 

imum separation distance constraint from the other vehicles, The three unsignalized intersections to be modeled are illus-and specifying a sequence of target lanes for the vehicle to trated in Fig. 1. A vehicle can come from any of the entrance traverse and finally leave the scene. By “vehicle *i * fails,” we lanes \(marked by green arrows\) to enter an intersection and mean the occurrence of 1\) vehicle *i *’s *c*-zone overlapping with go to any of the exit lanes \(marked by red arrows\) to leave it, any of the other vehicles’ *c*-zones, 2\) crossing any of the road except that U-turns are not allowed for four-way and T-shaped boundaries, or 3\) crossing a lane marking that separates the intersections. 

traffic of opposite directions. And, by “vehicle *i * succeeds,” 

When training the level-k policy ˆ

*π* k using Algorithm 1, 

we mean vehicle *i * gets to the last target lane in its target we treat these three unsignalized intersections separately. 

lane sequence so that it can leave the scene without further Specifically, when initializing the simulation environment in interactions with the other vehicles. 

step 4, we select one of these three unsignalized intersections as the traffic scene for the current simulation episode. 

IV. TRAFFIC IN UNSIGNALIZED INTERSECTION NETWORK

In addition, since in this paper we only consider these three We model urban traffic where the road system is composed unsignalized intersections, their layout and geometry features of straight roads and three most common types of unsignalized can be characterized and distinguished using a label *ξ *∈

intersections: four-way, T-shaped, and roundabout \[47\]. Such

\{1 *, * 2 *, * 3\}, i.e., the state *ξi * of vehicle *i * takes the value 1 when traffic models can be used as simulation environments for vehicle *i * operates in the area of the four-way intersection, Authorized licensed use limited to: ULAKBIM UASL - Bilkent University. Downloaded on December 26,2022 at 14:48:10 UTC from IEEE Xplore. Restrictions apply. 





2216

IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 23, NO. 3, MARCH 2022

solves for





*\(***u** *i\)a *= *\(*

*\)a, \(*

*\)a, . . . , \(*

*\)a*

*t*

*ui*

*ui*

*ui*

0| *t*

1| *t*

*N *−1| *t*

*N *−1





∈ arg max

*λο R siο*| *, ***s**− *i , ui , \(***u**− *i \)*˜ *k ,* *t*

*ο*|

\(12\)

*t*

*ο*| *t*

*ο*| *t*

**u** *i *∈ *U N*

*t*

*ο*=0





*j*

*j*

where *\(***u**− *i*

*ο*| *\)*˜ *k *= *\(u*

*\)*˜ *kt*

denotes the collection of

*t*

*ο*| *t*

*j *∈ *M, j *= *i*

predicted actions of the other vehicles. In particular, the actions *j*

of vehicle *j *, *uο*| , *ο *= 0 *, * 1 *, . . . , N *− 1, are predicted by *t*

*j*

modeling vehicle *j * as level- ˜ *kt * and are solved for according *j*

to \(5\), where ˜ *kt * is determined according to the following maximum likelihood principle:

Fig. 2. An urban traffic scenario with 15 level-1 cars \(yellow\) and 15 level-2

˜ *j*

*kt *∈ arg max P *i \(k j *= *k*| *t\),* \(13\)

cars \(red\). 

*k*∈ *K*

in which P *i \(k j *= *k*| *t\) * represents vehicle *i *’s belief at time *t * in 2 for the T-shaped intersection, and 3 for the roundabout. 

that vehicle *j * can be modeled as level- *k*, with *k * taking values For more intersection types with various layout and geometry in a model set *K*. The beliefs P *i \(k j *= *k*| *t\) * get updated after features, a higher dimensional vector *ξ * may be used \(e.g., see each time step according to the following algorithm: If there *j*

− *j*

*j*

− *j*

the intersection model in \[35\]\). 

exist *k, k* ∈ *K * such that *π* k *\(s , *

*, *

*, *

*, *

*t*

**s** *t*

*k\) *= *π* k *\(st ***s** *t* *k* *\)*, then

Once the policy ˆ *π* k for each of these three unsignalized intersections has been obtained, we can model larger road P *i\(k j *= *k*| *t *\+ 1 *\) *=

*pi \(k j *= *k*| *t *\+ 1 *\)*



*, *

systems using these three unsignalized intersections as mod-k∈ *K pi \(k j *= *k*| *t *\+ 1 *\)* *j*

ules and assembling them in arbitrary ways. Fig. 2 shows *\(* 1 − *β\)* P *i\(k j *= *k*| *t\) *\+ *β * if *k *= ˆ *k* *pi \(k j *= *k*| *t *\+ 1 *\) *=

*t , *

an example of assembly. When a vehicle operates at/nearest P *i\(k j *= *k*| *t\), *

otherwise *, *

to a specific intersection, it uses a local coordinate system, \(14\)

accounts for its interactions with only the vehicles in an immediate vicinity, and applies the ˆ

*π*

where *β *∈ \[0 *, * 1\] represents an update step size, and k corresponding to this

intersection. 

ˆ





*j*

*j*

*j*

*k*

dist *u*

*, *

To model the heterogeneity in driving styles of different *t*

∈ argmin

*t , \(ut \)k*

*k*∈ *K*

drivers, we let different vehicles be of different reasoning *j*

*j*

levels. Specifically, a level- *k * vehicle is controlled by the

= *\(a *− *\( \)k\)* 2 \+ *\(ω j *− *\(ω j\)k\)* 2 ; *t*

*at*

*t*

*t*

\(15\)

policy:

*j*

− *j*

*j*

− *j*

if *π* k *\(s , *

*, *

*, *

*, *

*t*

**s** *t*

*k\) *= *π* k *\(st ***s** *t* *k* *\) * for all *k, k* ∈ *K*, then ˆ *π*

P *i\(k j *= *k*| *t *\+ 1 *\) *= P *i\(k j *= *k*| *t\) * for all *k *∈ *K*. 

*k *= ˆ

*π* k *\(*· *, *· *, k\) *: *\(si, *

*\) *→ *\( \)k. *

*t ***s**− *i*

*t*

*uit*

\(11\)

The level estimation algorithm \(13\)-\(15\) has the following For instance, in Fig. 2 the 15 yellow cars are level-1 and the three features: 1\) If the actions predicted by all of the models 15 red cars are level-2. 

in *K * are the same, then the autonomous ego vehicle has no information to distinguish their relative accuracy and thus maintains its previous beliefs. 2\) Otherwise, the ego vehicle V. AUTONOMOUS VEHICLE CONTROL APPROACHES

*j*

identifies the model\(s\) in *K * whose prediction *\(u \)k* *t*

matches

*j*

In this section, we describe two AV control approaches vehicle *j *’s actually applied action *ut * for time *t * with the for urban traffic environments with unsignalized intersections. 

highest accuracy. 3\) The ego vehicle improves its belief\(s\) These approaches will be tested and calibrated using our traffic in that model\(s\) from its previous beliefs. This way, it takes model, thereby demonstrating its utility for verification and into account both its previous estimates and the current, latest validation. 

estimate. 

Similar to \(6\) defined by \(5\), we can define a policy to represent the control determined by \(12\) as follows: *A. Adaptive Control Based on Level-k Models* *π* a : *\(si, *

*, *˜ *\) *→ *\( \)a, *

*t ***s**− *i*

*t*

**k**− *i*

*t*

*uit*

\(16\)

In this approach, the autonomous ego vehicle treats the other *j*

drivers as level- *k * drivers. As different drivers may behave where ˜**k**− *i *= *\( *˜ *\)*

*t*

*kt j*∈ *M, j*= *i * denotes the collection of level esti-corresponding to different reasoning levels, the ego vehicle mates of the other vehicles and *\(ui \)a *= *\(*

*\)a*

*t*

*ui*

is determined

0| *t*

estimates their levels and adapts its own control strategy based by \(12\). Furthermore, we can train an explicit approximation on the estimation results. 

ˆ *π* a to *π* a using a similar imitation learning procedure as that The control strategy of the autonomous ego vehicle, *i *, can for training the explicit approximation ˆ *π* k to *π* k. This way, be described as: At each discrete-time instant *t*, vehicle *i* together with replacing *π* k with ˆ *π* k in the level estimation Authorized licensed use limited to: ULAKBIM UASL - Bilkent University. Downloaded on December 26,2022 at 14:48:10 UTC from IEEE Xplore. Restrictions apply. 





TIAN *et al. *: GAME-THEORETIC MODELING OF TRAFFIC IN UNSIGNALIZED INTERSECTION NETWORK

2217

In Algorithm 2, *Mc * represents the set of vehicles that are in conflict with the ego vehicle. In particular, the ego vehicle estimates each of the other vehicles’ future paths based on their current positions and their target lanes and using the same path planning algorithm that is used by the ego vehicle to create its own path. If the estimated future path of a vehicle *j * intersects with the ego vehicle’s own future path and the current distance between these two vehicles is smaller than a threshold value *R*

Fig. 3. 

Reference paths for the autonomous ego vehicle to drive through *c*, then vehicle *j * is identified as a vehicle in conflict, i.e., \(a\) four-way, \(b\) T-shaped, and \(c\) roundabout intersections. 

*j *∈ *Mc*. In particular, the distance function dist *\(*· *, *· *\) * measures the Euclidean distance. 

If there are vehicles in conflict, *Mc *= ∅, then the algorithm \(13\)-\(15\), we can move the major computational ego vehicle maximizes the minimum among the predicted tasks involved in this adaptive control approach \(12\)-\(15\) distances from these vehicles to improve safety. In step 8, offline, and thus, render its online computational feasibility. 

*\(xi , yi \) * represents the predicted position of the ego vehicle 1| *t*

1| *t*

The algorithm to train ˆ

*π* a using DAgger with *π* a as the *i * by driving along its reference path for one step with the speed expert policy is similar to Algorithm 1 and is omitted. 

*j*

*j*

after applying the acceleration *a*, and *\(x , y \) * represents the 1| *t*

1| *t*

predicted position of vehicle *j * by driving along its current heading direction with its current speed. If there is no vehicle *B. Rule-Based control*

in conflict, *Mc *= ∅, then the ego vehicle maximizes its speed. 

The second AV control approach that we consider is a Note that the key parameter for this rule-based control rule-based solution. Compared to many other approaches, approach is the threshold value *Rc*. It determines both whether rule-based control has the advantage of interpretability and can a vehicle will be identified as in conflict with the ego vehicle often be calibrated by tuning a small number of parameters. 

and the separation distance that the ego vehicle tries to keep In this approach, the autonomous ego vehicle drives by from other vehicles. We will utilize our traffic model to following a pre-planned reference path and accounts for its calibrate *Rc * in Section VI-C. 

interactions with other vehicles by adjusting its speed along the path correspondingly. Examples of reference paths for VI. RESULTS

the autonomous ego vehicle to drive through intersections are In this section, we show simulation results of our level-k illustrated by the green dotted curves in Fig. 3. 

game theory-based vehicle interaction model, and illustrate its The basic control rules can be explained as follows: The application to the verification, validation and calibration of AV

autonomous ego vehicle pursues a higher speed along the control systems. 

reference path if there is no other vehicle in conflict with it. If there are other vehicles in conflict with it, then the *A. Level-k Vehicle Models*

autonomous ego vehicle yields to them by maximizing distances from them. Specifically, at each discrete-time instant *t*, We consider a sampling period *t *= 0 *. * 25\[s\] and an the autonomous ego vehicle, *i *, selects and applies for one time action set *U * consisting of 6 actions representing common step an acceleration value from a finite set of accelerations, driving maneuvers in urban traffic, listed in Table I. The *A*, according to Algorithm 2. 

weight vector, the planning horizon, and the discount factor for the reward function \(4\) are **w **= \[1000 *, * 500 *, * 50 *, * 100 *, * 5 *, * 1\], *N *= 4, and *λ *= 0 *. * 8. When evaluating the features *φ* 1 and **Algorithm 2 **Rule-Based Autonomous Vehicle Control *φ* 4, we consider the *c*-zone of a vehicle as a 5\[m\] × 2\[m\]

Algorithm

rectangle centered at the vehicle’s position *\(x, y\) * and stretched **1 **Initialize *Mc *← ∅; 

along its heading direction *θ*, and the *s*-zone of a vehicle as **2 for ** *j *∈ *M, j *= *i ***do** a rectangle concentric with its *c*-zone and 8\[m\] × 2 *. * 4\[m\] in **3**

**if ** *the estimated future path of j intersects with i ’s* size. Furthermore, we consider a speed range \[ *v* min *, v* max\] =

*j*

*j*

*future path and dist \(xi , *

*\), \( , \) *≤

\[0 *, * 5\]\[m/s\]. When the speed calculated based on the model *t*

*yit*

*xt yt*

*Rc ***then**

## **4**

*Mc *← *Mc *∪ \{ *j*\}; 

\(2\) gets outside \[ *v* min *, v* max\], it is saturated to this range. We **5**

## **end if**

note that \[ *v* min *, v* max\] = \[0 *, * 5\]\[m/s\] is a reasonable range **6 end for**

to represent common speeds for vehicles to drive through **7 if ** *Mc *= ∅ **then**

unsignalized intersections. For instance, in California it is **8**

*\(ai\)r *=

suggested to maintain the vehicle speed below 15\[mph\] when *t*





*j*

*j*

arg max

*\(*

*, *

*\), \(*

*, *

*\)*

traversing an uncontrolled highway intersection \[48\]. 

*a*∈ *A * min *j *∈ *M * dist *x i* *yi*

*x*

*y*

; 

*c*

1| *t*

1| *t*

1| *t*

1| *t*

Experimental studies \[37\], \[49\] suggest that humans are **9 else**

most commonly level-1 and -2 reasoners in their interactions. 

## **10**

*\(ai\)r *=

*t*

max\{ *a *∈ *A*\}; 

Therefore, we model vehicles in traffic using level-1 and -2

## **11 end if**

policies in this paper. In particular, on the basis of our level-0

**12 **Output *\(ai \)r*

*t*

. 

decision rule \(see Section III-A\), a level-1 vehicle represents a Authorized licensed use limited to: ULAKBIM UASL - Bilkent University. Downloaded on December 26,2022 at 14:48:10 UTC from IEEE Xplore. Restrictions apply. 





2218

IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 23, NO. 3, MARCH 2022

TABLE I

ACTION SET *U*

Fig. 5. \(a-1\)-\(a-3\) show three sequential steps in a simulation where the blue vehicle controlled by ˆ *π* k trained using standard supervised learning fails in making an adequate right turn to get around the central island of a roundabout; \(b-1\)-\(b-3\) show steps in a similar simulation where the blue vehicle controlled by ˆ

*π* k trained using DAgger succeeds in making a proper right turn. 

Fig. 4. 

Architecture of the neural network. 

cautious/conservative vehicle and a level-2 vehicle represents an aggressive vehicle. Indeed, as level-0 and level-2 vehicles both represent aggressive vehicles, they behave similarly in many situations. 

We use a neural network with the architecture shown in Fig. 4 to represent a policy *πθ * and train its weights *θ * using Algorithm 1 to obtain an explicit approximation ˆ *π* k to the level-k policy *π* k, which is algorithmically determined based on \(5\). The accuracy of the obtained ˆ *π* k in terms of matching *π* k on the training dataset is 98 *. * 3%. Then, we generate 30%





more data points of

*\(si, *

*, *

*, *

*, *

*t ***s**− *i*

*t*

*k\), π* k *\(sit ***s**− *i*

*t*

*k\) * for testing. 

The accuracy of ˆ *π* k in terms of matching *π* k on the test dataset is 97 *. * 8%. As has been discussed at the beginning of Section III-B, the reason for generating ˆ

*π* k is to move the

numerical computations for determining the level- *k * decisions through \(5\) offline. With ˆ *π* k, the interactive decision-making processes of vehicles are reduced to function evaluations \(here, the function is expressed as a neural network\). This way, the online simulations of traffic scenarios, used as environments for virtual testing of AV control systems, can be significantly accelerated. 

To show the advantage of using the DAgger algorithm Fig. 6. Interactions of level- *k * vehicles at the four-way intersection. \(a-1\)-\(a-3\) \(9\) over using a standard supervised learning procedure \(7\) show three sequential steps in a simulation where three level-1 vehicles interact with each other; \(b-1\)-\(b-3\) show steps of three level-2 vehicles to obtain the policy ˆ

*π* k, we show a case observed in our interacting with each other; \(c-1\)-\(c-3\) show steps of a level-2 vehicle \(blue\) simulations where the policy trained using standard supervised interacting with two level-1 vehicles \(yellow and red\); *v* 1, *v* 2 and *v* 3 are the learning fails but the one trained using DAgger succeeds. 

speeds of the blue, yellow and red vehicles, respectively. 

In Fig. 5\(a-3\), the blue vehicle controlled by ˆ

*π* k trained using

standard supervised learning fails in making an adequate right turn to get around the central island. This is due to a significant In what follows we show the interactions between level- *k* error of ˆ *π*

vehicles at the four-way, T-shaped, and roundabout intersec-k from *π* k at certain states encountered by the blue vehicle when entering the roundabout, and the encounter tions. In particular, we let three vehicles be controlled by with such states results from the issue of error propagation different level- *k * policies and show how the traffic scenarios in time that has been discussed in Section III-B. In contrast, evolve differently depending on the different combinations of the blue vehicle in Fig. 5\(b-3\) controlled by ˆ *π*

level- *k * policies. 

k trained using

DAgger succeeds in making a proper right turn, illustrating It can be observed from Figs. 6-8 that, in general, when the effectiveness of DAgger in avoiding such an issue. 

level-1 and level-2 vehicles interact with each other, the Authorized licensed use limited to: ULAKBIM UASL - Bilkent University. Downloaded on December 26,2022 at 14:48:10 UTC from IEEE Xplore. Restrictions apply. 





TIAN *et al. *: GAME-THEORETIC MODELING OF TRAFFIC IN UNSIGNALIZED INTERSECTION NETWORK

2219

Fig. 7. Interactions of level- *k * vehicles at the T-shaped intersection. \(a-1\)-\(a-3\) show three sequential steps in a simulation where three level-1 vehicles interact with each other; \(b-1\)-\(b-3\) show steps of three level-2 vehicles interacting with each other; \(c-1\)-\(c-3\) show steps of a level-2 vehicle \(blue\) interacting with two level-1 vehicles \(yellow and red\); *v* 1, *v* 2 and *v* 3 are the speeds of the blue, yellow and red vehicles, respectively. 

Fig. 8. 

Interactions of level- *k * vehicles at the roundabout intersection. 

\(a-1\)-\(a-3\) show three sequential steps in a simulation where three level-1

vehicles interact with each other; \(b-1\)-\(b-3\) show steps of three level-2

vehicles interacting with each other; \(c-1\)-\(c-3\) show steps of a level-2

conflicts between them can be resolved. This is expected since vehicle \(blue\) interacting with two level-1 vehicles \(yellow and red\); *v* 1, *v* 2

level-1 vehicles, representing cautious/conservative vehicles, and *v* 3 are the speeds of the blue, yellow and red vehicles, respectively. 

will yield the right of way and level-2 vehicles, representing aggressive vehicles, will proceed ahead. In contrast, when likely to occur. 3\) Among the results of the three intersection level-1 vehicles interact with level-1 vehicles, deadlocks may types, the rates of success for the roundabout intersection occur, such as the one being observed in the T-shaped inter-are the highest. This illustrates the effective functionality of section in Fig. 7\(a\), because everyone yields to the others. 

roundabouts in reducing traffic conflicts. 

When level-2 vehicles interact with level-2 vehicles, collisions We further remark that although the high rates of failure of may occur, such as the ones being observed in panel \(b\) of

“level-2 versus level-2” are not desired in real-world traffic, Figs. 6-8, because everyone assumes the others would yield. 

it is important for a simulation environment for AV control We remark that deadlocks \(collisions\) do not always occur testing to include such cases that represent rational interactions in level-1 \(level-2\) interactions. The initial conditions of between aggressive vehicles. Note that a level-2 vehicle is Figs. 6-8 are chosen to show such situations. For randomized a rational decision maker that behaves aggressively, which initial conditions, the rates of success, defined as the pro-is fundamentally different from a driver/vehicle model that portion of 2000 simulation episodes where neither deadlocks acts aggressively but in an irrational way, e.g., taking actions nor collisions occur to the ego vehicle, for different numbers randomly. The cases of level-2 vehicle interactions provide of interacting vehicles and different combinations of level- *k* challenging test scenarios for AV control systems, which can policies at the three intersections are shown in Fig. 9. In Fig. 9, be more realistic than those provided by some worst-case

“L- *k * car in L- *k* Env.” shows the rate of success of a level- *k* \(i.e., not necessarily rational\) models \[50\]. 

ego vehicle interacting with other vehicles that are all level- *k*; 

“L- *k * car in Mix Env.” shows the rate of success of a level-k ego vehicle interacting with other vehicles whose control *B. Model Validation*

policies are randomly chosen between level-1 and level-2 with We validate our level- *k * vehicle models before illustrating equal probability. 

how to use them for AV control testing. 

The following observations can be made: 1\) As the number *1\) Feasibility Validation: * The unicycle model \(2\) has been of interacting vehicles increases, the rate of success decreases used to represent vehicle kinematics and the action set *U * in for all the cases. This is reasonable since a larger number of Table I has been used to represent common driving maneuvers. 

interacting vehicles represents a more complex traffic scenario. 

We now show that the trajectories generated by \(2\) with 2\) The rates of success of a level-2 ego vehicle interacting actions from *U * are feasible trajectories for vehicle systems. 

with other vehicles that are also level-2 are the lowest among For this, we use a hybrid kinematic/dynamic bicycle model the results of all combinations of level- *k * policies. This is with the brush tire model \[51\] to represent high-fidelity vehicle also reasonable since when all the vehicles are aggressive dynamics, and we use a PID-based controller \[52\] to control and assume the others would yield, traffic accidents are more the vehicle dynamics to execute the trajectory generated by \(2\) Authorized licensed use limited to: ULAKBIM UASL - Bilkent University. Downloaded on December 26,2022 at 14:48:10 UTC from IEEE Xplore. Restrictions apply. 





2220

IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 23, NO. 3, MARCH 2022

Fig. 10. Feasibility validation of the unicycle model \(2\) and the action set *U *. 

\(a-1\)-\(a-2\) show an example of path and speed tracking result at a T-shaped intersection; \(b-1\)-\(b-2\) show that at a roundabout intersection. 

T-shaped intersections. The average speeds versus the numbers of interacting vehicles are plotted in Fig. 12, where the 95%

confidence intervals of data are indicated by the vertical error bars. It can be seen that the average speeds of our level- *k* vehicle models are lower than the average speeds of actual Fig. 9. 

The rates of success of level- *k * policies. \(a-1\)-\(a-3\) show the rates vehicles. This is because some vehicles in the dataset drive at a of success of a level-1 ego vehicle operating in various traffic environments speed that is higher than the speed upper bound *v* max = 5\[m/s\]

\(various in the numbers and policies of interacting vehicles\) at the four-way, of our models, and is also due to some differences in the road T-shaped, and roundabout intersections; \(b-1\)-\(b-3\) show those of a level-2

ego vehicle; the bars in dark color represent the rates of success. 

layout and geometry \(e.g., three-lane versus two-lane on the left, see Fig. 11\). Also, only 56 scenarios at this T-shaped intersection are contained in the dataset and used to compute and *U*. Specifically, at each discrete-time instant *t * the level-the average speed results of the red curve. This causes the *k * decision policy selects an action from *U*, which defines a relatively large error bars. In contrast, we run 2000 simulation desired state *st*\+1 for the vehicle system through the unicycle episodes with randomized level- *k * policy combinations and model \(2\). Then, over the continuous-time interval from *t * to initial conditions to compute the average speed results of the *t *\+ 1, the PID-based controller controls the vehicle dynamics blue curve. So the error bars are relatively small. In summary, to track the desired state *st*\+1. 

similar trends of average speeds versus numbers of interacting Two examples of tracking results for the T-shaped and the vehicles are exhibited between the simulation results of our roundabout intersections are shown in Fig. 10, where the level- *k * vehicle models and the traffic data. Also note that the red solid curves represent the trajectories generated by \(2\) 95% confidence intervals of our models are contained in the \(referred to as “reference trajectories”\) and the black dotted 95% confidence intervals of the traffic data. 

curves represent the tracking trajectories. It can be observed that the tracking trajectories closely match the reference trajectories. This justifies the feasibility of trajectories generated *C. Evaluation and Calibration of Autonomous Vehicle* by the unicycle model \(2\) and the action set *U*. 

*Control Approaches*

*2\) Comparison to Traffic Data: * We next validate our level- *k* We test the two AV control approaches described in vehicle models using real-world traffic data. 

Section V using a simulation environment constructed based In Fig. 11, we show two traffic scenarios at a T-shaped on level- *k * vehicle models. 

intersection extracted from the INTERACTION dataset \[53\]

For the first approach of adaptive control based on level-and their reproduction by simulating our level- *k * vehicle mod-k models, we use the same sampling period *t*, action set els. Specifically, we initialize the states of our level- *k * vehicle *U*, reward function including the weight vector **w**, planning models according to the initial scene of the scenario, and horizon *N *, and discount factor *λ * as those used for the level- *k* compare the evolution of the scenario simulated by our models vehicle models. In the level estimation algorithm \(13\)-\(15\), to the actual one from data. It can be seen that the simulated we consider the model set *K *= \{1 *, * 2\} and the update step size evolution accurately matches the actual evolution for both *β *= 0 *. * 6. 

cases. 

When training the explicit approximation ˆ

*π* a to the policy *π* a

We also compare the average speeds of our level- *k * vehicle that is algorithmically determined by \(12\), we use the same models and of actual vehicles in the dataset when traversing neural network architecture shown in Fig. 4. The accuracy Authorized licensed use limited to: ULAKBIM UASL - Bilkent University. Downloaded on December 26,2022 at 14:48:10 UTC from IEEE Xplore. Restrictions apply. 





TIAN *et al. *: GAME-THEORETIC MODELING OF TRAFFIC IN UNSIGNALIZED INTERSECTION NETWORK

2221

Fig. 11. Reproduction of real-world traffic scenarios using our level- *k * vehicle models. \(a-1\)-\(a-3\) visualize a traffic scenario with two interacting vehicles extracted from the dataset \[53\] at three sequential time instants; \(a-4\)-\(a-6\) show the simulation results of a level-2 vehicle \(blue\) interacting with a level-1

vehicle \(yellow\) in a similar scenario. \(b-1\)-\(b-3\) visualize a traffic scenario with three interacting vehicles extracted from the same dataset; \(b-4\)-\(b-6\) show the simulation results of a level-2 vehicle \(blue\) interacting with two level-1 vehicles \(yellow and red\) in a similar scenario. 

Fig. 13. 

Interactions of the autonomous ego vehicle \(blue\) controlled by the adaptive control approach with level- *k * vehicles at the four-way intersection. 

\(a-1\)-\(a-3\) show three sequential steps in a simulation where the autonomous ego vehicle interacts with two level-1 vehicles, and \(a-4\) shows the time histories of the two vehicles’ level estimates where P *\(* 2 *\) *= P *\(k *= 2 *\) * denotes the ego vehicle’s belief in the level-2 model; \(b-1\)-\(b-4\) show those of the autonomous ego vehicle interacting with two level-2 vehicles; \(c-1\)-\(c-4\) show those of the autonomous ego vehicle interacting with a level-1 vehicle \(red\) and a level-2 vehicle \(yellow\); *v* 1, *v* 2 and *v* 3 are the speeds of the blue, yellow and red vehicles, respectively. 

Fig. 12. Average speeds versus numbers of interacting vehicles for traversing T-shaped intersections of level- *k * vehicle models and traffic data. 

significance in AV control of intention recognition and action prediction for the other vehicles. Note that these two steps are of the obtained ˆ *π* a in terms of matching *π* a is 98 *. * 8% on achieved in our adaptive control approach through the level the training dataset and is 98 *. * 6% on a test dataset of 30%

estimates and the level- *k * models of the other vehicles. 

additional data points that are not used for training. 

We then statistically evaluate and compare the two AV con-Firstly, we simulate similar scenarios as those shown in trol approaches. For the second approach of rule-based control, Figs. 6-8, but let the autonomous ego vehicle \(blue\) be we consider an acceleration set *A *= \{−5 *, *−2 *. * 5 *, * 0 *, * 2 *. * 5\}\[m/s2\]

controlled by the adaptive control approach instead of level- *k* and an initial design of the threshold value *Rc *= 14\[m\]. 

policies. Figs. 13-15 show snapshots of the simulations. It can In order to cover a rich set of scenarios, we construct a larger be observed that the autonomous ego vehicle can resolve traffic scene shown in Fig. 16, which models the road system the conflicts with the other two vehicles and safely drive of an urban area in Los Angeles and consists of one four-way through the intersections although the other two vehicles are intersection, one roundabout, and two T-shaped intersections. 

controlled by varying policies. The bottom panels show the We let an autonomous ego vehicle controlled by the adaptive level estimation histories of the simulations. It can be observed control approach or the rule-based control approach drive that the autonomous ego vehicle can resolve the conflicts through this traffic scene. Apart from the autonomous ego because it successfully identifies the level- *k * models of the vehicle, we also put multiple other vehicles controlled by other two vehicles. Recall that vehicle *j * is identified as level-1

level- *k * policies in the scene and let them drive through the \(level-2\) when P *\(k j *= 2 *\) < * 0 *. * 5 \(P *\(k j *= 2 *\) *≥ 0 *. * 5\). 

scene repeatedly. Their initial positions, lanes entering the The success of the adaptive control approach in situations scene, and sequences of target lanes to traverse the scene are where level- *k * control policies with fixed *k * fail suggests the all randomly chosen. 

Authorized licensed use limited to: ULAKBIM UASL - Bilkent University. Downloaded on December 26,2022 at 14:48:10 UTC from IEEE Xplore. Restrictions apply. 





2222

IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 23, NO. 3, MARCH 2022

Fig. 14. 

Interactions of the autonomous ego vehicle \(blue\) controlled by the adaptive control approach with level- *k * vehicles at the T-shaped intersection. 

\(a-1\)-\(a-3\) show three sequential steps in a simulation where the autonomous ego vehicle interacts with two level-1 vehicles, and \(a-4\) shows the time histories of the two vehicles’ level estimates where P *\(* 2 *\) *= P *\(k *= 2 *\) * denotes the ego vehicle’s belief in the level-2 model; \(b-1\)-\(b-4\) show those of the Fig. 15. 

Interactions of the autonomous ego vehicle \(blue\) controlled by the autonomous ego vehicle interacting with two level-2 vehicles; \(c-1\)-\(c-4\) show adaptive control approach with level- *k * vehicles at the roundabout intersection. 

those of the autonomous ego vehicle interacting with a level-1 vehicle \(red\) \(a-1\)-\(a-3\) show three sequential steps in a simulation where the autonomous and a level-2 vehicle \(yellow\); *v* 1, *v* 2 and *v* 3 are the speeds of the blue, yellow ego vehicle interacts with two level-1 vehicles, and \(a-4\) shows the time and red vehicles, respectively. 

histories of the two vehicles’ level estimates where P *\(* 2 *\) *= P *\(k *= 2 *\) * denotes the ego vehicle’s belief in the level-2 model; \(b-1\)-\(b-4\) show those of the autonomous ego vehicle interacting with two level-2 vehicles; \(c-1\)-\(c-4\) show those of the autonomous ego vehicle interacting with a level-1 vehicle \(red\) We evaluate the two control approaches based on two and a level-2 vehicle \(yellow\); *v* 1, *v* 2 and *v* 3 are the speeds of the blue, yellow statistical metrics: the rate of collision \(CR\) and the rate and red vehicles, respectively. 

of deadlock \(DR\). The rate of collision is defined as the proportion of 2000 simulation episodes where the autonomous ego vehicle collides with another vehicle or with the road boundaries. The rate of deadlock is defined as the proportion of 2000 simulation episodes where no collision occurs to the autonomous ego vehicle but it fails to drive through the scene in 300\[s\] of simulation time. We consider three traffic models: 1\) all of the other vehicles are level-1, called a “level-1

environment,” 2\) all of the other vehicles are level-2, called a

“level-2 environment,” and 3\) the control policy of each of the other vehicles is randomly chosen between level-1 and level-2

with equal probability, called a “mixed environment.” 

The CR and DR results of the adaptive control approach and the rule-based control approach for different numbers of Fig. 16. Traffic scene for evaluating autonomous vehicle control approaches. 

other vehicles in the scene are shown in Figs. 17 and 18. 

\(a\) shows an urban area in Los Angeles \(provided by Google Maps\) and \(b\) shows the model of the road system in \(a\). 

The number of other vehicles, *nv *, represents traffic density, roughly, 2 *. * 87 *nv *\[vehicles/mile\] \(the total length of the roads is about 560 \[m\]\). 

for the level-1 environment are the lowest and those for the From Fig. 17 it can be observed that, for the adaptive level-2 environment are the highest. This is also reasonable control approach, the CR and DR increase as the traffic density since the level-1 environment, composed of level-1 vehicles, increases, which is reasonable. In particular, the increase in CR

represents a cautious/conservative traffic model, the level-2

slows down as the number of other vehicles goes beyond 20. 

environment represents an aggressive traffic model and is thus Among the results for different traffic models, the CR and DR

most challenging for the autonomous ego vehicle, while the Authorized licensed use limited to: ULAKBIM UASL - Bilkent University. Downloaded on December 26,2022 at 14:48:10 UTC from IEEE Xplore. Restrictions apply. 





TIAN *et al. *: GAME-THEORETIC MODELING OF TRAFFIC IN UNSIGNALIZED INTERSECTION NETWORK

2223

Fig. 17. 

Evaluation results of the adaptive control approach: \(a\) the rate of collision \(CR\) and \(b\) the rate of deadlock \(DR\) versus different numbers of environmental vehicles and different traffic models. 

Fig. 19. 

Failure cases. \(a\) shows a scenario where the autonomous ego vehicle \(blue\) controlled by the adaptive control approach gets stuck at the entrance of the roundabout due to the level-1 vehicle \(yellow\) on its left. 

\(b\) shows a scenario where the autonomous ego vehicle \(blue\) controlled by the rule-based control approach gets hit by the level-2 vehicle \(red\) on its left. 

achieved through a larger update step size *β*. In the second case in Fig. 19\(b\), the autonomous ego vehicle controlled by Fig. 18. 

Evaluation results of the rule-based control approach with *Rc *=

14 \[m\]: \(a\) the rate of collision \(CR\) and \(b\) the rate of deadlock \(DR\) versus the rule-based control approach stops in the roundabout to different numbers of environmental vehicles and different traffic models. 

yield to the yellow vehicle on its right and within the critical distance *Rc *\(marked by the red dashed circle\). However, because the gap between the autonomous ego vehicle and the mixed environment lies in between. Furthermore, the results yellow vehicle is still quite large, the red vehicle on the left of for the adaptive control approach are less sensitive to changes the autonomous ego vehicle expects it to proceed and thus does in traffic models than those for level- *k * policies with fixed *k* not slow down, which causes a collision. This scenario shows shown in Fig. 9. This shows again the significance of adap-that a larger critical distance *Rc * may not always correspond to tation of AV control strategy to other vehicles’ intentions and a safer driving behavior. We remark that failure/corner cases actions. Note that the rate of success for a single intersection identified by our simulations, such as the above two cases, of the adaptive control approach, if estimated as 1 − *C R*\+ *DR *, 4

can also inform the design of specific test trajectories for AV

is close to that of “L-1 car in L-2 Env.” and that of “L-2 car control systems. 

in L-1 Env.,” which represent the best performance of level- *k* We now optimize the threshold value *Rc * in the rule-based policies. 

control approach to achieve better performance defined by a For the rule-based control approach, it can be observed performance index as follows:

from Fig. 18 that as the traffic density increases, the CR first *n*





increases and then decreases, while the DR keeps increasing. 

max



*φs\(Sn\)*

*J *=

1

*w*

*, *

The decrease in CR when the traffic becomes very dense is *c φc\(Sn \) *\+ *wd φd \(Sn \) *\+ *wv* *n* max

¯ *v\(Sn\) *\+ 

*n*=1

due to the constant yielding of the autonomous ego vehicle to \(17\)

other vehicles, which causes the dramatic increase in DR. 

Comparing the results of the two approaches, the adaptive where *Sn * denotes the *n* th simulation episode; the *φc\(Sn\)*, control approach performs better than the rule-based control *φd\(Sn\)*, and *φs\(Sn\) * are indicator functions, taking 1 if, approach in the above experiments. This is attributed to the respectively, a collision occurs to the autonomous ego vehi-more sophisticated and complicated algorithm behind the cle, no collision but a deadlock occurs to the autonomous adaptive control approach. However, the rule-based control is ego vehicle, and neither collision nor deadlock occur and more interpretable \(e.g., the reason for the decrease in CR is the autonomous ego vehicle successfully drives through the easily understood\), and is easier to calibrate. 

scene in 300\[s\] of simulation time in the *n* th simulation In Fig. 19, we show two informative cases observed in our episode, and taking 0 otherwise; ¯ *v\(Sn\) * is the average speed simulations. In the first case in Fig. 19\(a\), the autonomous of the autonomous ego vehicle in the *n* th simulation episode; ego vehicle \(blue\) controlled by the adaptive control approach *wc, wd, wv *≥ 0 are weighting factors, and * > * 0 is a constant and the level-1 vehicle \(yellow\) on its left both yield to to adjust the shape of the function with respect to the average the other and cause a deadlock. Note that a level-1 vehicle speed ¯ *v\(Sn\) * and to avoid the denominator being 0. 

represents a vehicle with a cautious/conservative driver, and The performance index function \(17\) imposes penalties for accordingly, yields to the autonomous ego vehicle. Although collisions and deadlocks through the first two terms, and the autonomous ego vehicle eventually decides to proceed rewards higher average speeds through the last term. Note ahead and successfully drives through the roundabout, it takes that the last term is designed in such a way that the penalty too long for such a conflict to be resolved, and thus this increases fast for decrease in speed values that are already scenario falls into our DR category. To avoid such deadlock very low, and decreases slowly for increase in speed values scenarios, the autonomous ego vehicle may need to identify that are already very high. In obtaining the following results, the driving style of the opponent vehicle faster, which may be we run simulations in the same scene shown in Fig. 16 with Authorized licensed use limited to: ULAKBIM UASL - Bilkent University. Downloaded on December 26,2022 at 14:48:10 UTC from IEEE Xplore. Restrictions apply. 

2224

IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 23, NO. 3, MARCH 2022

control systems. In particular, we considered two autonomous vehicle control approaches as case studies: an adaptive control approach based on level- *k * vehicle models and a rule-based control approach. We analyzed their characteristics and evaluated their performance based on their testing results with our traffic models, and then optimized the parameters of the rule-based approach based on a performance index. 

We envision that traffic models developed using the framework proposed in this paper can also be integrated with urban traffic/driving simulators with higher-fidelity car dynamics and Fig. 20. 

Performance index *J * as function of *R*

environmental representations, such as CARLA \[54\], using an *c * of the rule-based control

approach with different traffic models. 

approach similar to that of \[55\], to create more realistic urban traffic simulations and support autonomous driving system development. 

15 other vehicles, and we use *wc *= 10, *wd *= 5, *wv *= 1, and

* *= 0 *. * 1. 

REFERENCES

We plot the values of \(17\) for different values of *Rc * in

\[1\] D. 

J. 

Fagnant

and

K. 

Kockelman, 

“Preparing

a

nation

for

Fig. 20. Specifically, for each value of *R*

autonomous vehicles: Opportunities, barriers and policy recommen-c , we run *n* max = 2000

dations,” *Transp. Res. A, Policy Pract. *, vol. 77, pp. 167–181, simulation episodes and calculate the value of \(17\) based on Jul. 2015. \[Online\]. Available: http://www.sciencedirect.com/science/

the simulation results. Lower values of \(17\) represent better article/pii/S0965856415000804

performance in terms of having less collisions, less deadlocks, 

\[2\] U.S. 

Department

of

Transportation’s

National

Highway

Traffic

Safety Administration. *Automated Vehicles for Safety*. Accessed: and higher average travel speeds. 

Jun. 18, 2019. \[Online\]. Available: https://www.nhtsa.gov/technology-In Fig. 20, the blue curve represents the result when the innovation/automated-vehicles-safety

autonomous ego vehicle operates in the level-1 environment. 

\[3\] J. Meyer, H. Becker, P. M. Bösch, and K. W. Axhausen, “Autonomous vehicles: The next jump in accessibilities?” *Res. Transp. Econ. *, It can be observed that the performance is good when *Rc* vol. 62, pp. 80–91, Jun. 2017. \[Online\]. Available: http://www. 

takes very small values, i.e., in the range of \[6 *, * 7 *. * 5\]\[m\]. 

sciencedirect.com/science/article/pii/S0739885917300021

This is because small *R*

\[4\] N. Kalra and S. M. Paddock, “Driving to safety: How many miles of *c * corresponds to aggressive behav-driving would it take to demonstrate autonomous vehicle reliability?” 

ior and the level-1 environment represents a conservative *Transp. Res. A, Policy Pract. *, vol. 94, pp. 182–193, Dec. 2016. 

traffic model, thus, the other vehicles almost always yield

\[5\] J. Zhou and L. del Re, “Reduced complexity safety testing for ADAS

to the autonomous ego vehicle when there is a conflict. 

& ADF,” *IFAC-PapersOnLine*, vol. 50, no. 1, pp. 5985–5990, 2017. 

\[6\] H. Waschl, I. Kolmanovsky, and F. Willems, *Control Strategies for* Since the autonomous ego vehicle proceeds ahead while the *Advanced Driver Assistance Systems and Autonomous Driving Func-other vehicles yield, collisions and deadlocks are avoided. *
* 
tions. Cham, Switzerland: Springer, 2019. 

However, when operating in the level-2 or mixed environment, 

\[7\] D. Zhao et al. , “Accelerated evaluation of automated vehicles safety in lane-change scenarios based on importance sampling techniques,” IEEE

small Rc  leads to poor performance. This is because both Trans. Intell. Transp. Syst. , vol. 18, no. 3, pp. 595–607, Mar. 2017. 

the autonomous ego vehicle and the other vehicles behave

\[8\] H. Waschl, R. Schmied, D. Reischl, and M. Stolz, “A virtual develop-aggressively and cause many collisions. When R

ment and evaluation framework for ADAS—Case study of a P-ACC in c  takes values

a connected environment,” in Control Strategies for Advanced Driver in the range of \[7 .  5 ,  11\]\[m\], the performance is the worst Assistance Systems and Autonomous Driving Functions. New York, NY, for all of the three traffic models. This is because such USA: Springer, 2019, pp. 107–131. 

R
*
*\[9\] C. Hubmann, J. Schulz, M. Becker, D. Althoff, and C. Stiller, “Auto-c * values correspond to behaviors between aggressive and mated driving in uncertain environments: Planning with interaction and conservative, which can cause collisions with both aggressive uncertain maneuver prediction,” *IEEE Trans. Intell. Vehicles*, vol. 3, and conservative interacting vehicles. The range \[11 *. * 5 *, * 13\]\[m\]

no. 1, pp. 5–17, Mar. 2018. 

is suitable for choosing the value of *R*

\[10\] T. Bandyopadhyay, K. S. Won, E. Frazzoli, D. Hsu, W. S. Lee, and *c*, where the performance

D. Rus, “Intention-aware motion planning,” in *Algorithmic Foundations* is good and insensitive to changes in the traffic models. For *of Robotics X*, E. Frazzoli, T. Lozano-Perez, N. Roy, and D. Rus, Eds. 

larger *Rc * values, the autonomous ego vehicle becomes overly Berlin, Germany: Springer, 2013, pp. 475–491. 

conservative and almost always yields to the other vehicles, 

\[11\] C. Hubmann, J. Schulz, G. Xu, D. Althoff, and C. Stiller, “A belief state planner for interactive merge maneuvers in congested traffic,” in *Proc. *

which causes it difficulties to enter the intersections and leads *21st Int. Conf. Intell. Transp. Syst. \(ITSC\)*, Nov. 2018, pp. 1617–1624. 

to many deadlocks. 

\[12\] N. Li, A. Girard, and I. Kolmanovsky, “Stochastic predictive control for partially observable Markov decision processes with time-joint chance constraints and application to autonomous vehicle control,” *J. Dyn. Syst.,* VII. CONCLUSION

*Meas., Control*, vol. 141, no. 7, Jul. 2019, Art. no. 071007. 

In this paper, we described a framework based on level-k

\[13\] W. Schwarting, J. Alonso-Mora, L. Paull, S. Karaman, and D. Rus, 

“Safe nonlinear trajectory generation for parallel autonomy with a game theory for modeling traffic consisting of heteroge-dynamic vehicle model,” *IEEE Trans. Intell. Transp. Syst. *, vol. 19, no. 9, neous \(in terms of their driving styles\) and interactive vehi-pp. 2994–3008, Sep. 2018. 

cles in urban environments with unsignalized intersections. 

\[14\] G. Cesari, G. Schildbach, A. Carvalho, and F. Borrelli, “Scenario model predictive control for lane change assistance and autonomous driving An algorithm integrating the level-k decision-making formal-on highways,” *IEEE Intell. Transp. Syst. Mag. *, vol. 9, no. 3, pp. 23–35, ism, receding-horizon optimization, and imitation learning was Fall 2017. 

proposed and used to solve for level- *k * control policies. 

\[15\] M. Bahram, A. Lawitzky, J. Friedrichs, M. Aeberhard, and D. Wollherr, 

“A game-theoretic approach to replanning-aware interactive scene pre-The developed traffic models are useful as simulation envi-diction and planning,” *IEEE Trans. Veh. Technol. *, vol. 65, no. 6, ronments for verification and validation of autonomous vehicle pp. 3981–3992, Jun. 2016. 

Authorized licensed use limited to: ULAKBIM UASL - Bilkent University. Downloaded on December 26,2022 at 14:48:10 UTC from IEEE Xplore. Restrictions apply. 



TIAN *et al. *: GAME-THEORETIC MODELING OF TRAFFIC IN UNSIGNALIZED INTERSECTION NETWORK

2225

\[16\] D. Sadigh, S. Sastry, S. A. Seshia, and A. D. Dragan, “Planning for

\[39\] R. Tian, S. Li, N. Li, I. Kolmanovsky, A. Girard, and Y. Yildiz, “Adaptive autonomous cars that leverage effects on human actions,” in *Robotics:* game-theoretic decision making for autonomous vehicle control at *Science and Systems*, vol. 2, 2016. 

roundabouts,” in *Proc. IEEE Conf. Decis. Control \(CDC\)*, Dec. 2018, 

\[17\] J. F. Fisac, E. Bronstein, E. Stefansson, D. Sadigh, S. S. Sastry, and pp. 321–326. 

A. D. Dragan, “Hierarchical game-theoretic planning for autonomous

\[40\] S. Karimi and A. Vahidi, “Receding horizon motion planning for vehicles,” in *Proc. Int. Conf. Robot. Autom. \(ICRA\)*, May 2019, automated lane change and merge using Monte Carlo tree search and pp. 9590–9596. 

level-K game theory,” in *Proc. Amer. Control Conf. \(ACC\)*, Jul. 2020. 

\[18\] H. Yu, H. E. Tseng, and R. Langari, “A human-like game theory-based

\[41\] A. Y. Ng and S. J. Russell, “Algorithms for inverse reinforcement controller for automatic lane changing,” *Transp. Res. C, Emerg. Technol. *, learning,” in *Proc. Int. Conf. Mach. Learn. *, 2000, p. 2. 

vol. 88, pp. 140–158, Mar. 2018. 

\[42\] B. D. Ziebart, A. Maas, J. A. Bagnell, and A. K. Dey, “Maximum

\[19\] A. Dreves and M. Gerdts, “A generalized Nash equilibrium approach for entropy inverse reinforcement learning,” in *Proc. AAAI Conf. Artif. *

optimal control problems of autonomous cars,” *Optim. Control Appl. *

*Intell. *, 2008, pp. 1433–1438. 

*Methods*, vol. 39, no. 1, pp. 326–342, Jan. 2018. \[Online\]. Available:

\[43\] L. Claussmann, A. Carvalho, and G. Schildbach, “A path planner for https://onlinelibrary.wiley.com/doi/abs/10.1002/oca.2348

autonomous driving on highways using a human mimicry approach with

\[20\] C. Vallon, Z. Ercan, A. Carvalho, and F. Borrelli, “A machine binary decision diagrams,” in *Proc. Eur. Control Conf. \(ECC\)*, Jul. 2015, learning approach for personalized autonomous lane change initiation pp. 2976–2982. 

and control,” in *Proc. IEEE Intell. Vehicles Symp. \(IV\)*, Jun. 2017, 

\[44\] F. Codevilla, M. Muller, A. López, V. Koltun, and A. Dosovitskiy, “End-pp. 1590–1595. 

to-End driving via conditional imitation learning,” in *Proc. IEEE Int. *

*Conf. Robot. Autom. \(ICRA\)*, May 2018, pp. 1–9. 

\[21\] H. Xu, Y. Gao, F. Yu, and T. Darrell, “End-to-end learning of driving

\[45\] L. Sun, C. Peng, W. Zhan, and M. Tomizuka, “A fast integrated planning models from large-scale video datasets,” in *Proc. IEEE Conf. Comput. *

and control framework for autonomous driving via imitation learning,” 

*Vis. Pattern Recognit. \(CVPR\)*, Jul. 2017, pp. 3530–3538. 

in *Proc. ASME Dyn. Syst. Control Conf. *, 2018, Art. no. V003T37A012. 

\[22\] N. Li, D. W. Oyler, M. Zhang, Y. Yildiz, I. Kolmanovsky, and

\[46\] S. Ross, G. Gordon, and D. Bagnell, “A reduction of imitation learning A. R. Girard, “Game theoretic modeling of driver and vehicle interac-and structured prediction to no-regret online learning,” in *Proc. 14th Int. *

tions for verification and validation of autonomous vehicle control sys-Conf. Artif. Intell. Statist. , 2011, pp. 627–635. 

tems,” *IEEE Trans. Control Syst. Technol. *, vol. 26, no. 5, pp. 1782–1797, 

\[47\] K. Fitzpatrick, M. D. Wooldridge, and J. D. Blaschke, *Urban Intersec-Sep. 2018. *
* 
tion Design Guide: Guidelines, vol. 1. Feb. 2005. 

\[23\] Federal Highway Administration. Intersection Safety Needs Identifica-

\[48\] California Department of Transportation. California Manual for tion Report. Accessed: Jun. 20, 2019. \[Online\]. Available: https://safety. 

Setting Speed Limits. Accessed: Jun. 10, 2020. \[Online\]. Available: fhwa.dot.gov/intersection/other\_topics/needsidrpt/needsidrpt.pdf https://dot.ca.gov/-/media/dot-media/programs/traffic-operations/

\[24\] Unsignalized Intersections. Accessed: Jun. 20, 2019. \[Online\]. Available: documents/2019-california-manual-for-setting-speed-limits-a11y.pdf https:// safety.fhwa.dot.gov/intersection/conventional/unsignalized/

\[49\] M. A. Costa-Gomes, V. P. Crawford, and N. Iriberri, “Comparing models

\[25\] M. Bouton, A. Cosgun, and M. J. Kochenderfer, “Belief state planning of strategic thinking in van huyck, battalio, and Beil’s coordination for autonomously navigating urban intersections,” in Proc. IEEE Intell. 

games,” J. Eur. Econ. Assoc. , vol. 7, nos. 2–3, pp. 365–376, Apr. 2009. 

Vehicles Symp. \(IV\), Jun. 2017, pp. 825–830. 

\[50\] G. Chou, Y. E. Sahin, L. Yang, K. J. Rutledge, P. Nilsson, and

\[26\] D. Isele, R. Rahimi, A. Cosgun, K. Subramanian, and K. Fujimura, N. Ozay, “Using control synthesis to generate corner cases: A case study

“Navigating occluded intersections with autonomous vehicles using deep on autonomous driving,” IEEE Trans. Comput.-Aided Design Integr. 

reinforcement learning,” in Proc. IEEE Int. Conf. Robot. Autom. \(ICRA\), Circuits Syst. , vol. 37, no. 11, pp. 2906–2917, Nov. 2018. 

May 2018, pp. 2034–2039. 

\[51\] J. Kong, M. Pfeiffer, G. Schildbach, and F. Borrelli, “Kinematic and

\[27\] S. Pruekprasert, J. Dubut, X. Zhang, C. Huang, and M. Kishida, dynamic vehicle models for autonomous driving control design,” in Proc. 
*
*“A game-theoretic approach to decision making for multiple vehi-IEEE Intell. Vehicles Symp. \(IV\)*, Jun. 2015, pp. 1094–1099. 

cles at roundabout,” 2019, *arXiv:1904.06224*. \[Online\]. Available:

\[52\] R. Rajamani, *Vehicle Dynamics and Control*. New York, NY, USA: http://arxiv.org/abs/1904.06224

Springer, 2011. 

\[28\] S. Pruekprasert, X. Zhang, J. Dubut, C. Huang, and M. Kishida, 

\[53\] W. Zhan *et al. *, “Interaction dataset: An international, adversarial

“Decision making for autonomous vehicles at unsignalized intersection and cooperative motion dataset in interactive driving scenarios with in presence of malicious vehicles,” in *Proc. IEEE Intell. Transp. Syst. *

semantic maps,” Sep. 2019, *arXiv:1910.03088*. \[Online\]. Available: *Conf. \(ITSC\)*, Oct. 2019, pp. 2299–2304. 

http://arxiv.org/abs/1910.03088

\[29\] M. J. Lighthill and G. B. Whitham, “On kinematic waves II. A theory

\[54\] A. Dosovitskiy, G. Ros, F. Codevilla, A. Lopez, and V. Koltun, of traffic flow on long crowded roads,” *Proc. Roy. Soc. London. Ser. A. *

“CARLA: An open urban driving simulator,” in *Proc. 1st Annu. Conf. *

*Math. Phys. Sci. *, vol. 229, no. 1178, pp. 317–345, 1955. 

*Robot Learn. *, 2017, pp. 1–16. 

\[30\] A. D. May, *Traffic Flow Fundamentals*. Englewood Cliffs, NJ, USA:

\[55\] G. Su, N. Li, Y. Yildiz, A. Girard, and I. Kolmanovsky, “A traffic sim-Prentice-Hall, 1990. 

ulation model with interactive drivers and high-fidelity car dynamics,” 

\[31\] C. F. Daganzo, “The cell transmission model, part II: Network traffic,” 

*IFAC-PapersOnLine*, vol. 51, no. 34, pp. 384–389, 2019. 

*Transp. Res. B, Methodol. *, vol. 29, no. 2, pp. 79–93, Apr. 1995. 

\[32\] P. G. Gipps, “A behavioural car-following model for computer simulation,” *Transp. Res. B, Methodol. *, vol. 15, no. 2, pp. 105–111, Apr. 1981. 

\[33\] M. Brackstone and M. McDonald, “Car-following: A historical review,” 

*Transp. Res. F, Traffic Psychol. Behaviour*, vol. 2, no. 4, pp. 181–196, Dec. 1999. 

\[34\] D. D. Salvucci, “Modeling driver behavior in a cognitive architecture,” *Hum. Factors: J. Hum. Factors Ergonom. Soc. *, vol. 48, no. 2, pp. 362–380, Jun. 2006. 

\[35\] N. Li, Y. Yao, I. Kolmanovsky, E. Atkins, and A. R. Girard, 

“Game-theoretic modeling of multi-vehicle interactions at uncontrolled intersections,” *IEEE Trans. Intell. Transp. Syst. *, pp. 1–15, 2020, doi: 10.1109/TITS.2020.3026160. 

**Ran Tian **received the B.S. degree in aerospace

\[36\] D. O. Stahl and P. W. Wilson, “On players’ models of other players: engineering from the University of Michigan, Ann Theory and experimental evidence,” *Games Econ. Behav. *, vol. 10, no. 1, Arbor, MI, USA, in 2016, the B.S. degree in

pp. 218–254, 1995. 

mechanical engineering from Shanghai Jiao Tong

\[37\] M. A. Costa-Gomes and V. P. Crawford, “Cognition and behavior in University, Shanghai, China, in 2017, and the M.S. 

two-person guessing games: An experimental study,” *Amer. Econ. Rev. *, degree in robotics from the University of Michi-vol. 96, no. 5, pp. 1737–1768, Nov. 2006. 

gan, in 2019. He is currently pursuing the Ph.D. 

\[38\] N. Li, I. Kolmanovsky, A. Girard, and Y. Yildiz, “Game theoretic model-degree with the University of California, Berkeley, ing of vehicle interactions at unsignalized intersections and application CA, USA. His current research interests include to autonomous vehicle control,” in *Proc. Annu. Amer. Control Conf. *

decision-making under uncertainty and human–robot *\(ACC\)*, Jun. 2018, pp. 3215–3220. 

interaction. 

Authorized licensed use limited to: ULAKBIM UASL - Bilkent University. Downloaded on December 26,2022 at 14:48:10 UTC from IEEE Xplore. Restrictions apply. 





2226

IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 23, NO. 3, MARCH 2022

**Nan Li **\(Member, IEEE\) received the B.S. degree **Yildiray Yildiz **\(Senior Member, IEEE\) received the in automotive engineering from Tongji University, B.S. degree \(valedictorian\) in mechanical engineer-Shanghai, China, in 2014, and the M.S. degrees in ing from Middle East Technical University, Ankara, mechanical engineering and in mathematics from

in 2002, the M.S. degree in mechatronics from

the University of Michigan, Ann Arbor, MI, USA, Sabanci University, Istanbul, in 2004, and the Ph.D. 

in 2016 and 2020, respectively, where he is currently degree in mechanical engineering with a mathemat-pursuing the Ph.D. degree in aerospace engineering. 

ics minor from MIT in 2009. He is currently an

His research interests are stochastic control and Assistant Professor with Bilkent University, Ankara. 

multiagent systems. 

He held postdoctoral associate and associate scientist positions with the NASA Ames Research

Center, California, employed by the University of California, Santa Cruz, through its University Affiliated Research Center, from 2009 to 2010 and from 2010 to 2014, respectively. He was a recipient of NASA Honor Award, Young Scientist Award from Science Academy of Turkey, Young Scientist Award from Turkish Academy of Sciences, Research Incentive Award from Prof. Mustafa Parlar Education and Research Foundation, and best student conference paper award from ASME. He is currently serving as an Associate Editor of the *IEEE Control Systems Magazine * and *European Journal of Control*. His research interests include control, machine learning, game theory, and applications of these fields for modeling and control of automotive and aerospace systems. 

**Anouck R. Girard **\(Senior Member, IEEE\) received the Ph.D. degree in ocean engineering from the Uni-Ilya Kolmanovsky \(Fellow, IEEE\) received the versity of California, Berkeley, CA, USA, in 2002. 

Ph.D. degree from the University of Michigan

She has been with the University of Michigan, 

in 1995. He is currently a Professor with the

Ann Arbor, MI, USA, since 2006, where she is

Department of Aerospace Engineering, University of currently an Associate Professor of aerospace engi-Michigan, with research interests in control theory neering. She has coauthored the book *Fundamentals* for systems with state and control constraints, and *of Aerospace Navigation and Guidance *\(Cambridge in control applications to aerospace and automotive University Press, 2014\). Her current research inter-systems. 

ests include flight dynamics and control systems. She was a recipient of the Silver Shaft Teaching Award from the University of Michigan and a Best Student Paper Award from the American Society of Mechanical Engineers. 

Authorized licensed use limited to: ULAKBIM UASL - Bilkent University. Downloaded on December 26,2022 at 14:48:10 UTC from IEEE Xplore. Restrictions apply.



