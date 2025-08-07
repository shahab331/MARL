11360

IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 24, NO. 10, OCTOBER 2023

Human Inspired Autonomous Intersection Handling Using Game Theory

Keqi Shu , Graduate Student Member, IEEE, Reza Valiollahi Mehrizi, Shen Li , Member, IEEE, Mohammad Pirani , Member, IEEE, and Amir Khajepour , Senior Member, IEEE

Abstract— Left turning for autonomous vehicles at intersec-40% of all injury accidents occur at intersections in the tions is challenging due to the various driving behaviors from USA \[2\]. As for autonomous vehicles, most decision-making different human drivers and the strong interaction between and planning algorithms could not guarantee 100% safety the autonomous vehicle and human traffic participants. This paper proposes a planning and decision making framework for because of the complex and quickly-evolving characteristics intersection left-turning which considers the interaction between of intersection scenarios \[3\]. 

autonomous vehicles and human drivers as well as pedestri-Among all the intersection decision-making and planning ans to address this issue. The proposed framework considers scenarios, left-turning is one of the most critical one. Where interactions mathematically by formulating the problem as a interaction among the autonomous vehicle and the surrounding linear quadratic differential game. Through solving the Nash equilibrium of the game, the autonomous vehicle is able to vehicles are very strong due to the rapid-changing right-properly interact with surrounding traffic participants. Under of-way and states. Without the help of a centralized traffic the differential game framework, the accuracy of the interaction management system \[4\], it is a challenging task to estimate formulation is closely related to the behavior model of human the future states of the surrounding vehicles correctly and, drivers. Therefore, real-world human behavior is extracted and at the same time, be able to behave accordingly. 

evaluated from naturalistic driving dataset to help establish more realistic modeling and estimation of various kinds of traffic participants, including aggressive, neutral and conservative traffic B. Literature Review

participants. The simulation results show that the autonomous vehicle is able to properly estimate the types of traffic participants In the literature, researchers try to solve the intersection by observing their behavior using the proposed technique. Then handling problems by considering interaction behaviours as the autonomous vehicle behave according to the types of those one-way or bi-directional interaction \[5\]. 

traffic participants to enable interactive and human-like planning and decision making at intersections. 

One-way interaction approaches consider the oncoming vehicle or pedestrians as obstacles and only consider their Index Terms— Autonomous vehicles, intersection handling, influence on the autonomous vehicle, while the ego vehi-decision making, planning, game theory, real-world data. 

cle behaves passively \[6\]. One popular approach is the network-based reinforcement learning methods \[7\]. Li et al. 

I. INTRODUCTION

proposed inverse reinforcement learning \(IRL\) to perform A. Background

defensive driving at intersections. The heuristics are repre-PLANNING and decision-making of autonomous vehicles sented by deep Q-networks trained from real-world data \[8\]. 

have been widely developed in academia and indus-Hu et al. proposed a deep-IRL framework that improves try. Decision-making plays as one of the most challenging the generalization and effectiveness of dealing with corner part when autonomous vehicles interact with human \[1\]. 

cases \[9\]. However, this approach performs less outstanding Complicate traffic system structure and traffic rules add to in scenarios where driving data is not covered, and needs to this challenge. Hence, safe interaction between the human consider the influence of the ego vehicle on the surrounding and autonomous vehicles becomes crucial in decision-making traffic participants. 

tasks. 

The bi-directional interactive decision-making and planning One of the above-mentioned interaction scenario which is approaches enable the autonomous vehicles not only trying very common in daily driving is intersection scenario. Over to keep safe distances according to the surrounding traffic participants’ behaviours, but at the same time, consider Manuscript received 28 November 2022; revised 19 April 2023; their own behaviour’s influence on the surrounding vehicles’

accepted 17 May 2023. Date of publication 12 June 2023; date of current version 4 October 2023. The Associate Editor for this article was Y. Wiseman. 

strategies. This type of modelling will help the autonomous \(Corresponding author: Keqi Shu.\)

vehicle to better estimate the current scenario and make sound Keqi Shu, Reza Valiollahi Mehrizi, Mohammad Pirani, and Amir decisions. Among all the decision-making frameworks that Khajepour are with the Department of Mechanical and Mechatronics Engineering, University of Waterloo, Waterloo, ON N2L 3G1, Canada consider bi-directional interactive behaviours, one of the most \(e-mail: k3shu@uwaterloo.ca\). 

popular approach is the game-theory-based framework. 

Shen Li is with the Department of Civil Engineering, Tsinghua University, One classical game theory-based decision-making model is Beijing 100084, China. 

Digital Object Identifier 10.1109/TITS.2023.3281390

the Stackelberg game \[10\], \[11\]. This formulation assumes 1558-0016 © 2023 IEEE. Personal use is permitted, but republication/redistribution requires IEEE permission. 

See https://www.ieee.org/publications/rights/index.html for more information. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on February 13,2025 at 07:49:36 UTC from IEEE Xplore. Restrictions apply. 

SHU et al.: HUMAN INSPIRED AUTONOMOUS INTERSECTION HANDLING USING GAME THEORY

## 11361

that two players follow certain priority rules, for example, model but the interactive behaviours might not be fully the right-of-way of vehicles. Li et al. \[12\] formed the vehicles represented. 

with leader-follower pairs based on common traffic rules. 

Reference \[13\] applied Stackelberg game modelling to enable C. Contributions

better unprotected left turns at intersections. These kinds of To overcome the aforementioned problems in the litera-methods are commonly applied in merging or lane-changing ture, this paper proposes a decision-making framework for scenarios \[14\], \[15\], where the right-of-way is clear, and the intersections handling based on the feedback-loop linear interaction is usually simple. However, is less applicable in quadratic game algorithm. Naturalistic real-world driving data strong-interactive scenarios. 

is used to help analytically represent more realistic interaction Another trendy method is the level-k game method \[16\]. 

behaviours between the ego vehicle and surrounding traffic This method finds the Nash equilibrium by updating each participants. This enable autonomous vehicles to find more player’s strategy iteratively and sequentially. Reference \[17\]

applicable and natural solutions in real life. 

applied level-k algorithm in uncontrolled intersection han-The contributions of our paper are as follows: dling with vehicles violating traffic rules. Li et al. \[18\] also

•

we introduced a novel algorithm for intersection handling applied a level-k time-extended, multi-step, and interactive that employs game theory and realistic driving characters decision-making framework that operates at uncontrolled inter-extracted from naturalistic driving data, thus promoting sections. However, these algorithms still solve the problem in a efficiency and reliability under high-interactive scenarios; discrete action space and suffer from the curse of dimensions. 

•

we developed a traffic participant’s driving character To realise intersection handling under continuous space, the estimation model, which enables the autonomous vehicle feedback-loop differential game framework was introduced. 

to infer the driving characters from observing critical This framework expresses the time-inconsistent interaction features extracted from driving data in real-time and make behaviour in a theoretical way and convert the game into sound decisions accordingly; 

an optimization problem \[19\]. Fridovich-Keil et al. proposed

•

our approach enhances the computational efficiency of an iterative linear quadratic differential game framework uncertain driving character estimation and interactive which decreased the computational time for finding the Nash game-based decision-making in continuous action spaces, equilibrium by linearizing the problem and setting the opti-enabling real-time performance. 

mization functions in a quadratic format \[20\]. They also Our proposed framework represents improvements over solved the problem by projecting the states of the problem existing literature in intersection handling, particularly in to the linearized system space to increased the convergence the following aspects. The proposed framework accounts for rate \[21\]. The closed feedback-loop differential game showed bi-directional interaction, specifically how the ego vehi-promising results in simulations due to its exceptional ability cle’s possible behaviours can influence surrounding vehicles. 

in representing interaction behaviours in an expressive way. 

A realistic driver model was extracted from a naturalistic driv-However, the previous works assume perfect modelling of ing dataset with a high level of interaction, which accurately the surrounding traffic participants’ behaviours. The behaviour represents the bi-directional interaction feature in the driver model of surrounding traffic participants and the way they model. The proposed uncertain driver character estimation interact with each other were set up through driving experience model integrates the extracted driver model into a game-based or common sense as a uniform format. In the real world, decision-making framework. This allows the autonomous vehi-however, human behaviour does not generate from a uniform cle to interact appropriately with different types of drivers. 

model and people usually have different “heuristics.” These Furthermore, the relationship between the critical observation issues make the implementation of feedback-loop differential feature and driving character was extracted from real-world game in the real world less ideal \(optimal\) than in simulation. 

data. By linearizing the problem and utilizing the character Numerous driver models have been proposed to represent estimation model, our framework reduces the computational interaction behaviours at intersections accurately. One popular load, allowing the ego vehicle to find a solution in real time approach is to use neural networks to model driver behaviour. 

for a continuous action space with various traffic participants. 

For instance, Xu et al. used large-Scale video datasets to train the black-box driver model \[22\]. Peng et al. also proposed a back-propagation neural network driver behaviour model to II. INTERSECTION INTERACTIVE LEFT-TURNING

improve the accuracy of the modelling \[23\]. However, these DECISION MAKING FRAMEWORK

models heavily rely on the comprehensiveness of the dataset The overall decision-making framework is presented in and may be difficult to tune for specific drivers. 

Fig. 1. Where sub-figure \(a\) is one typical scenario that Other approaches simulate driver behaviours at intersections the framework could be implemented, that is, a left-turning by proposing parameterized and adaptable driver models. For autonomous vehicle tries to cross the intersection with two example, \[24\] extended the classical Intelligent Driver Model different human-driven vehicles potentially blocking the way. 

\(IDM\) \[25\] into a more generalized format by considering sur-The red vehicle \(AV1\) is the autonomous vehicle and the other rounding traffic participants’ interaction behaviours. Xin et al. 

two blue vehicles are the human-driven vehicle labelled as proposed a predictive IDM based on V2X communication HV1 and HV2. The colour bars in the yellow bounding boxes to reduce idling time at signalized intersections \[26\]. These

help indicate the driving style of the human drivers. The arrow methods could be more accurate than a black-box driver pointing more on the yellow side indicates that the driver is Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on February 13,2025 at 07:49:36 UTC from IEEE Xplore. Restrictions apply. 





## 11362

IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 24, NO. 10, OCTOBER 2023

Fig. 1. 

Naturalistic autonomous intersection handling framework. 

more aggressive and wise versa. The red dashed lines are the computational efficiency in the nonlinear system, the the nominal paths of the human-driven vehicle and the green framework linearizes the players’ dynamics and formulates dashed polynomial is the nominal path of the ego vehicle. 

costs in quadratic form. This approach enables real-time To help the autonomous vehicle to make proper decisions solution finding, but the linearized solution is only valid when considering the interactions with human-driven vehicles, the the states do not deviate significantly from the current states. 

human-driver models are carefully modified. A naturalistic To obtain a solution for the original problem, the solver intersection driving dataset \[27\] had been used to extract considers the possible future states of all players and iteratively realistic human behaviours. As shown in Fig. 1 \(b\), the data searches for a better solution with small steps until it is close was used to extract features of different human drivers and enough to the Nash equilibrium. 

then properly set up the driving style. 

This differential-game-based intersection handling algo-Given the modified driver models and the features of rithm works in a receding horizon format, that the ego vehicle various kinds of human drivers, it is possible to consider makes a decision at each time step considering the actions of different drivers when making decisions. Based on an analysis other traffic participants of a fixed time horizon. Which makes of real-world driving scenarios and driving datasets, it was the proposed framework more applicable. 

discovered that the decision-making process is complicated by the unpredictable driving styles of surrounding drivers and III. ITERATIVE LINEAR QUADRATIC DIFFERENTIAL GAME

rapidly changing situations. Thus, the framework is designed FORMULATION AND SOLVING

to enable the ego vehicle to continuously assess the human driver’s behaviour and make appropriate decisions in real-time. 

To allow the autonomous vehicle to make proper left-turning This function is demonstrated on the left-hand side of decisions in the high-interactive scenario. A framework based Fig. 1 \(c\), where the driving style is estimated through the on iterative linear quadratic differential game that analytically dynamic time to collision \(TTC\) calculated from the latest formulates the interaction into the decision-making process states of all the traffic participants. The dynamic TTC includes was implemented. It tries to reach the best result given the the derivative of the TTC and the TTC itself. After the driving nominal paths of each traffic participant as well as each traffic style is estimated in real-time, the data-extracted features of participant’s heuristics. The formulation and the game solving the utility function that represents various driving styles are method will be explained in further detail in this section. 

updated, and used to solve the differential game. 

Given the up-to-date information on the surrounding human-driven vehicles and also the environment, the ego A. Game Formulation

vehicle would be able to solve the decision-making prob-1\) Dynamics and Utility Functions of Players: the first step lem accordingly. The ego vehicle formulates the interaction in the game formulation is setting up the dynamics of the between the traffic participants in a mathematical and analyti-players in the intersection scenario which include vehicles’ and cal way using a differential game framework. By transferring pedestrians’ dynamics. For autonomous vehicles and human-the game into an optimization problem, the Nash equilibrium driven vehicles, a 5-D kinematic model is implemented. The of the game could be found by finding the optima. 

states of the vehicles are \(x, y, v, θ, φ\). x and y are the Carte-The differential game formalization of the ego vehicle is sian positions of the vehicles, v is the speed, θ is the heading demonstrated on the right-hand side of Fig. 1 \(c\). To improve angle, and φ is the steering angle of the vehicle. The dynamics Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on February 13,2025 at 07:49:36 UTC from IEEE Xplore. Restrictions apply. 

SHU et al.: HUMAN INSPIRED AUTONOMOUS INTERSECTION HANDLING USING GAME THEORY

## 11363

of the vehicles could be demonstrated as follows: where pi = \(xi , yi \) and p j = \(x j , y j \) are the positions of the



ego vehicle and the traffic participants around it in the Carte-

˙

x = v cos θ





sian space. N is the total number of players in the intersection





 ˙

y = v sin θ



scenario, where j indicates any traffic participant around traffic

 ˙θ = \(v tan φ\)/l

\(1\)

participant i . dm stands for the minimum distance between the



 ˙

φ =

vehicle and the other traffic participants. dis\(·\) represents the



## u1







distance between the two traffic participants. If dis\(·\) is smaller

 ˙

v = u2, 

than the safety distance dm, then an exponential cost will be where u

assigned to the vehicle. 

1 and u2 are the inputs of the vehicle, that is, the inputs are the steering rate and acceleration. The inputs of the The minimum gap feature Rg is also a safety feature, which vehicles can be expressed as u = \(u

ensures the left-turning ego vehicle maintains a “turning-safe” 

1, u2\)

For pedestrians, due to the all-directional moving nature gap with the oncoming vehicle. This safe gap is the l1-norm and the smaller size, the kinematic model is simplified as a distance between the left-turning vehicle and the oncoming point-mass model in which the states of the pedestrian could vehicle in the oncoming vehicle’s 1D direction, which is be expressed as x, y, v, θ, that x and y are the positions and v proposed inspired by the accepted gap concept \[28\]. The dg is and θ are the velocity and the humans’ facing-direction angle positively proportional to the oncoming vehicle’s speed, and accordingly. Thus the dynamics for pedestrians are: a penalty is given if the l1-norm safe gap is smaller than dg. 

The nominal speed and path feature Rnom could be

 ˙x = v cos θ

expressed as:







 ˙

y = v sin θ

R 

\(2\)

R

s

, 

˙

θ

\(6\)

= u

nom =

R



## 1

### l





 ˙

v = u2, 

where Rl and Rs are the heuristics for keeping the traffic participants moving along the nominal path with the nominal where the inputs u1 and u2 are the turning rate and acceleration speed profile. Rl could be expressed as:

accordingly. 



The next step is to set up proper behaviour models for the kn| pr oj \( pi \(x, y\), l poly\)|, 





players in the game. To analytically formulate the behaviours





if di s\( pi \(x, y\), l poly\) < lb

of the players, various features have been used in the utility Rl =

\(7\)

k



b\( pr o j \( pi \(x , y\), l pol y \) − lb\)2, 

functions. For vehicles, including autonomous vehicles and







if di s\( p

human-driven vehicles, the utility functions are defined as the i \(x , y\), l pol y \) ≥ lb, 

affine combination of different heuristics as: where l poly represents the polynomial nominal trajectory that is generated using road geometry. l



b is half of the road width. 

R



sa f e

proj\(·\) is a distance projection function that calculates the gi \(t, x\(t\), u1:N \(t\)\) = \[Ksa f e, Knom, Kcom f \]

, 

 Rnom



\(3\)

closest distance from the vehicle’s planned future trajectory Rcom f

to the center line of the given nominal path. Finally, kn and where g

kb are constants which scale the utilities. Rl is designed to i \(·\) represents the utilities of the i th traffic participant. 

The features of the vehicles could be divided into three main provide a huge penalty for vehicles that are off the road and a categories: the safety feature R

relatively small penalty for off-setting from the nominal path. 

sa f e, the nominal path and

speed feature R

Therefore, kb shall be much larger than kn. 

nom , and the riding comfort feature Rcom f . 

K

R

\(

s is designed for the vehicle to follow the nominal speed

·\) is the coefficient of each of these features. These features with their coefficients together describe how a vehicle would and does not violate speed limits. This heuristic could be behave in a given scenario. A more detailed description of the expressed as:

features is described as follows. 

 kv \(s



m

v−smax \)2, 

if sv > smax

The safety feature R



sa f e could be expressed as:

Rs =

kv|

\(8\)

n sv −sn |, 

if 0 ≤ sv ≤ smax



R 

 kv \(s

i

v\)2, 

if sv < 0, 

R

d

sa f e =

, 

\(4\)

Rg

where sv is the current speed of the ego vehicle, smax is the speed limit of the intersection and s

where R

n is the nominal speed

d is the heuristic such that vehicles need to keep a profile of the vehicle. kv

are constant ratio. The

minimum safe distance from all other traffic participants, and m , kv

n and kv

i

heuristics are designed to give a huge penalty if the vehicle Rg is the accepted gap feature to ensure the left-turning vehicle is driving over the speed limit or going backwards, therefore, has enough time and space to make the left turn. More specific kv

are relatively much larger than kv

explanation of R

m and kv

i

n . 

d and Rg are made as follows. 

Finally, a smooth feature is defined as R

The minimum distance heuristic R

com f , which repre-

d could be written as:

sents the behaviour of drivers tended to accelerate, decelerate



and steer as less as possible. The expression of this feature is: N −1

## 0

if di s\( p



i , p j \) ≥ dm

X 

R





d =

\(dm − dis\(pi\(x, y\), pj\(x, y\)\)\)2 i ̸= j, \(5\) R

R

a

com f =

, 

\(9\)

j =1 



if di s\( p

Rw

i , p j \) < dm

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on February 13,2025 at 07:49:36 UTC from IEEE Xplore. Restrictions apply. 

11364

IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 24, NO. 10, OCTOBER 2023

where

Given gi represents the utility functions of the traffic participants, some variable is the first partial derivable of g R

i :

a/w = \(a/w\)2. 

\(10\)

∂

∂

## ∂2

### l

gi

gi

gi

i = ∂ , r

, and some are the Hessian: Q

and

¯

s

i j = ∂ ¯

u

i = ∂ ¯s∂ ¯s

a and w are the acceleration and steering angle of the vehicle. 

j

## ∂2gi

Since the driving behavior features R

Ri j =

. The L , Q, R matrices are obtained to solve sa f e, Rnom and Rcom f

∂u j ∂u j

are written in an array format. The coefficients of the features: the linear quadratic differential game. 

Ksa f e, Knom, Kcom f are also in a array format: Ksa f e =

\[Kd , Kg\]T , Knom = \[Ks, Kl \]T , and Kcom f = \[Ka, Kw\]T . 

B. Solving the Game

For pedestrians behaviour modelling, the features are similar After the linear approximated dynamic system and the to the vehicle’s modelling which also have utilities in three p

p

p

quadratic approximated cost is obtained, the modified problem aspects, R

R

. However, there are still

sa f e

nom

and Rcom f

now follows the definition of a differential game. In other p

p

some minor differences. For R

, the minimum gap R

sa f e

g

words, it is possible to be transformed into an optimization p

is not considered. For R

, since a point-mass model is

com f

problem. The Nash equilibrium of the game could then be being implemented for the pedestrians modelling, instead of calculated by finding the optima iteratively \[20\]. 

considering minimizing acceleration and steering angle, this The problem is assumed to follow a feedback information model considers minimizing the acceleration in the x and y structure, where the optima is in the following format \[20\]:

p

axis. Finally, similar to driver’s utility function \(3\), K\(·\) is the coefficient of the pedestrians’ features. 

δu∗\(k\) = −P∗\(k\)δs\(k\) − δα∗\(k\), 

\(14\)

i

i

i

2\) Dynamic Linearization and Costs Quadratization: sub-where δu∗\(k\) = ˜

γ o\(k, s\(k\)\)− ûi\(k\), and ˜γo\(k, s\(k\)\) represents section III-A1 describes the state space and action space of i

i

i

the feedback strategy generated for player i after oth itera-traffic participants and their behaviour heuristics. This subsection to come to a feedback Nash equilibrium. The feedback tion describes how to transfer the problem into a differential parameter Pi \(k\) are matrices with size mi × n and αi \(k\) is the game. 

additional term. These variables can be calculated by solving The nonlinear dynamics of the players is:

\(15\) and \(16\) assuming strong convexity \[30\]. The two sets of

˙

s\(t\) = f \(s\(t\), u

equations are obtained by setting the gradients of the quadratic 1:N \(t \)\) , 

\(11\)

utility functions to zero:

where s\(t\), u1:N \(t\) are the state and inputs of each traffic participant accordingly at time t . This nonlinear formulation X

Ro \+ Bo T Z o\+1 Bo Po \+ Bo T Z o\+1

Bo Po

i i

i

i

i

i

i

i

j

j

makes the dynamics model closer to reality but increase the j ̸=i

computational load. To improve real-time performance, the

= Bo T Z o\+1 Ao, 

\(15\)

dynamics needs to be linearized. 

i

i





X

This linearization is realised through making a Jacobian Ro \+ Bo T Z o\+1 Bo αo \+ Bo T Z o\+1

Boαo

i i

i

i

i

i

i

i

j

j

linearization \[29\] over the offsets of arbitrary states and inputs j ̸=i

to the nominal ones:

= Bo T ζ o\+1. 

\(16\)

i

i

˙

δ

X

s \(t \) = A\(t \)δs \(t \) \+

Bi \(t\)δu\(t\), 

\(12\)

Ro is the Hessian matrix after oth iteration calculated in \(13\)

i i

i ∈\[N \]

and Z o can be calculated recursively by:

i

where the offset is δs\(t\) = s\(t\) − ¯s\(t\) and δu\(t\) = u\(t\) − ¯

u\(t\), 

X

=

\+

, 

¯

s and ¯

u represent the nominal states and inputs. The dynamic Z o

F o T Z o\+1 F o \+

Po T Ro Po

Qo

\(17\)

i

i

j

i j

j

i

∂ 

j ∈N

matrices could be expressed as A =

f 

∂

∈ Rn×n and

s x=¯s

u= ¯

u

∂ 

where Z O\+1

=

Q O\+1, \(i ∈ N\) and Fo ≜ Ao −

B

f 

i

i

i = ∂

\(t\) ∈ Rn×m. 

u

P

i s=¯s

Bo Po \(k ∈ O\). O is the total number of iteration. 

u= ¯

u

i ∈N

i

i

It is demonstrated in \[29\] that when δs and δu is “small” 

ζo\(i ∈ N\) can also be calculated by recursively solving: i

enough, the linearization holds. Without the loss of generality X

and to make the problem easier to handle, the system is ζo = Fo T ζo\+1 \+ Zo\+1βo \+

Po T Ro αo, 

\(18\)

i

i

i

j

i j

j

discretized, where the states s transfer from time step k to j ∈N

k \+ 1. Now, the new “ A” is “ A∗ = eAT ” and the new “B” is where ζ O\+1 = 0, i ∈ N and βo ≜ co −P

Bo T αo \(k ∈ K\). 

B∗ = A−1 eAT − I B. 

i

j ∈N

j

j

Finally, the Nash equilibrium of the game could be found The next major procedure to increase the real time perfor-using \(14\) given the calculated Pi \(k\) and αi \(k\). 

mance is converting the cost into quadratic form. Given the o

o

heuristics of each player presented in subsection III-A1, the quadratic approximation of the cost could be rewritten as: IV. REALISTIC BEHAVIOURAL MODELLING

AND ESTIMATION

g\(s \+ δs, u1:N \(k\) \+ δu1:N \(k\), k\) − g\(s, u1:N \(k\), k\) In the proposed framework, the autonomous vehicle makes 1

≈

δs\(k\)T Qi\(t\)δs\(k\) \+ δs\(k\)T li\(k\)

decisions on the assumption of how the other traffic partici-2

pants might behave given their behaviour models. To achieve 1 X

\+

δu j\(k\)T Rij\(k\)δu j\(k\) \+ 2rij\(k\) . 

\(13\)

good performance of the framework, a realistic interactive 2 j∈\[N\]

behavioural model and its estimation model are proposed. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on February 13,2025 at 07:49:36 UTC from IEEE Xplore. Restrictions apply. 





## 11366

IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 24, NO. 10, OCTOBER 2023

Fig. 5. 

Relative distance and speed of left-turning vehicle and oncoming Fig. 6. 

Left-turning time gap distribution. 

vehicle at turning-decision point. 

frame indicator with the unit as ms. The pointers along the trajectory’s polynomials indicate the direction that the vehicle is driving. 

Fig. 4 \(a\) and \(b\) are typical intersection left-turning scenarios, which are left-turning and oncoming vehicle passes the intersection first accordingly. All the related information such as the vehicles’ speed, acceleration, heading angle, etc. are extracted from all these scenarios. 

The decision-making points are extracted from the sce-Fig. 7. 

Traffic participants’ minimum distances distribution. 

narios, defined as the places where the left-turning vehicle starts to accelerate or decelerate before the heading angle starts to change to the left. The states information of these value \(in this case 13 meters\) are extracted. Then the minimum decision-making points is processed and presented in Fig. 5, 

distances of these scenarios are extracted and their distribution which are the relative distance and speed between the ego are presented in Fig. 7. Where the x-axis is the minimum vehicle and the oncoming vehicle. 

distance value, and the y-axis indicates the distribution. The The yellow and blue colours correspond to scenarios of figure showed that most vehicles keep a minimum distance of left-turning or oncoming vehicles passing the intersection around 4 meters to 9 meters. 

first accordingly. The deep-blue shaded area is where most left-turning vehicles yield to the oncoming vehicle, and the deep yellow shaded area is where most left-turning vehicles B. Behavior Model Estimation

make the left turn first. The light-coloured middle area is The proposed behavioral model allows the planning and where both behaviours happen. The figure showed that the decision making framework represent various kinds of driving dataset includes rich and well-distributed interaction scenarios. 

styles, However, in the real-world application, traffic partici-As proposed in section IV, the accepted time gap is one of pants do not know the driving style of each other. Therefore the major indicators of the driver’s behaviour style. Therefore, the autonomous vehicle has to properly estimate the driving the left-turning and oncoming trajectory sets are extracted style of other traffic participants to enable sound interaction. 

and the time difference between the two vehicles to reach One very distinct feature that indicates different kinds of the potential collision point \(also known as the TTC\) are drivers is the accepted time gap \(TTC\). For example, if one calculated and presented in Fig. 6. The orange bars represent left-turning vehicle makes a left turn under a 5-second gap, the case when the left-turning vehicle yield to the oncoming and another vehicle yields to the oncoming vehicle under a vehicle and the blue bars represent the case where the oncom-5-second gap, then the first vehicle is more aggressive than ing vehicle yield to the left-turning vehicle. It can be seen the second vehicle. This also works for the oncoming vehicle. 

that a left-turning vehicle would make a left turn before the Therefore, two features that are closely related to the oncoming vehicle if the time gap is around 10 s \(±3 s\) or accepted time gap T T C are considered for driving style larger. When the time gap is less than 4 s the left-turning estimation. The autonomous ego vehicle takes in the speed and would yield, and if the gap is between 4 s - 8 s, the two kinds positions of the surrounding traffic participants, and calculates of driving behaviours both occur. This figure demonstrated that the TTC, then makes an estimation based on this feature as: different drivers would accept various minimum time gaps, M

˙

s = kt tt t c \+ k ˙tt t c

if tmin < tttc < tmax , 

\(19\)

which nicely represents the driving style of different drivers. 

t

Another very important interactive feature is the minimum where Ms is the estimated driving style, tttc and ˙tttc are the distance that each vehicle keeps between other vehicles. Which TTC and the change of TTC respectively, kt and k˙t are the is also a key representation of different kinds of drivers. All constant coefficients, tmax and tmin are the estimation threshold the scenarios with vehicles’ relative distance less than a certain of the TTC. If the TTC is out of the estimating range \(too small Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on February 13,2025 at 07:49:36 UTC from IEEE Xplore. Restrictions apply. 

SHU et al.: HUMAN INSPIRED AUTONOMOUS INTERSECTION HANDLING USING GAME THEORY

## 11367

### TABLE I

could be obtained by calculating the Hessian matrix and INTERVALS OF DRIVING CHARACTERS FOR VARIOUS DRIVERS

partial derivative vectors \(L, Q, R\). This transforms the game-based decision making problem into a optimal control problem, and the optimal control policy is proven to be the Nash equilibrium of the game \[30\]. Thus, by applying the calculated L, Q, R into \(14\) - \(18\), the Nash equilibrium could be found iteratively, which leads to optimal actions ûi \(k\) = ˜

γ o\(k, s\(k\)\) − δu∗\(k\) of the ego vehicle. 

or too large\), e.g. if the TTC is too small, then no matter what i

i

The simulation is operated in a receding horizon format with the driver’s character is, the autonomous vehicle needs to yield a 0.25s time step and 5s horizon. In each simulation scenario, to the human driver. 

the surrounding traffic participants will have a pre-defined Thus, the autonomous vehicle only estimates the human driving style that is unknown to the autonomous vehicle. The driver’s driving style if tttc ∈ \(tmin, tmax \). Which decreases various driving style of human drivers are represented by the computational load of the algorithm. The value of Ms behaving differently \(more aggressive or conservative\) as the decides the aggressiveness of the human driver, the smaller autonomous vehicle’s expected. 

the value is, the more aggressive the driver is, and vice versa. 

For example, if the TTC \(tttc\) is very large, and is increasing \(˙tttc > 0\) throughout the left-turning process, which means Ms A. Two Vehicle Interaction Scenario

is increasing, this indicates that the oncoming human driver To evaluate the performance of the proposed framework, is conservative. Then the driving style characters mentioned a left-turning scenario with only one oncoming vehicle and above such as dm, dg, etc. will change continuously according one left-turning autonomous vehicle is designed. Three kinds to Ms. 

of driving styles are tested where all the vehicles start from the same position, speed and initial strategy. The only difference V. SIMULATION AND RESULTS

is the driving style of the oncoming vehicles, which is defined The proposed framework is tested at an intersection sim-by adding a N \(0.5, 0.5\) \(aggressive\), N \(0.0, 0.5\) \(neutral\), ulation scenario with various kinds of traffic participants N \(−0.5, 0.5\) \(conservative\) on acceleration to the oncoming to test the feasibility and evaluate the performance of the vehicle at each time step. 

framework. It is assumed that the ego vehicle have perfect per-The simulation results are shown in Fig. 8. The sub-figures ception information from the surrounding traffic participants, from left to right represent the scenario with aggressive, including the speed, position, acceleration, etc. However, the neutral and conservative oncoming human-driven vehicles. 

driving-behaviour character \(driving style\) is unknown. 

The black lines indicate the boundaries of the road and Before the simulation starts, the driving characteristics of median strip. The coloured lines indicate the trajectories of the each human traffic participant as well as the autonomous vehi-vehicles, whereas the colour indicates the speed of the vehicle cle are defined through \(3\). To consider more realistic driving along the trajectory. The relation between the speed and colour behaviours during intersection left turns, the parameters are set is indicated in the colour bar on the right. The orange dots as closely as possible with real-world traffic rules and natural-along the vehicles’ trajectory are time stamps which provide istic driving behaviours. For example, the maximum speed is time-state information. The red car in the sub-figures is the extracted from the traffic rule and regulations, minimum time autonomous ego vehicle, the blue vehicle is the oncoming gap are defined through human driving behaviours extracted vehicle. The light-green-colour arrow at the beginning of the from real-world driving data in section IV-A. 

red vehicle’s trajectory is the direction of the autonomous Table I demonstrates the applied parameters’ intervals, vehicle travelling. Finally, the red arrows are the travelling which are the minimum distance the minimum time gap and direction of the oncoming human-driven vehicle. 

the nominal speed. The features are designed in a continuous The autonomous vehicles in the sub-figures behave differ-way. The word “Neutral” here does not mean purely neutral ently when interacting with different human drivers. When but indicates that the driver is “in-between” the most aggres-interacting with neutral and aggressive human drivers, the sive and conservative styles. 

autonomous vehicle yield to the oncoming vehicle. Which can Finally, the ratio parameters K ∗

∗ can also represent various

be observed by comparing the positions of the two vehicles driving behaviours, however, they are implicitly presented in on the 6th timestamp for Fig. 8 \(a\) and \(b\). When cooperating driving data and would be very difficult to find the exact values with conservative human drivers, autonomous vehicles drive that represent fully natural driving characters. Therefore, these through the intersection earlier than the oncoming vehicle. 

parameters are defined through common knowledge and expert Fig. 8 shows that the proposed framework enables the driver experience. The safety feature ratios are set to the ego vehicle to adjust its trajectory and speed in different highest values because safety should be the first priority while scenarios. The trajectories and speeds of the ego vehicle in driving. The ratios for nominal path and speed cost features Fig. 8 \(a\) and \(b\) are different from the ones in Fig. 8 \(c\). 

are set to smaller values. The ratios for comfort riding features Fig. 8 also presents the different behaviours of various human are defined on the smallest scale. 

drivers. The neutral and aggressive human drivers adjust their Given the various utility functions representing different speed slightly, while the conservative driver decreases their traffic participants, the corresponding quadratic approximation speed before pulling into the intersection. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on February 13,2025 at 07:49:36 UTC from IEEE Xplore. Restrictions apply. 





## 11368

IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 24, NO. 10, OCTOBER 2023

Fig. 8. 

Typical left-turning scenarios and simulation results. 

Fig. 9. Speed profiles along trajectories of left-turning and oncoming vehicles in typical left-turning scenarios. 

Fig. 10. 

Accepted time gap distribution in simulation. 

The colour bar in Fig. 8 provides a very rough representation of the speed profile along the trajectories of each vehicle. The vehicle takes. Similar scenarios as scenarios in Fig. 8 were more detailed speed profiles of the two vehicles are plotted tested in simulation with various initial speeds and positions. 

in Fig. 9. Where Fig. 9 \(a\) and Fig. 9 \(b\) correspond to the The scenarios where the left-turning vehicle pulls through the scenario in Fig. 8 \(a\) and Fig. 8 \(c\). Which are the scenarios intersection first were extracted, where the TTC is calculated with aggressive and conservative vehicles accordingly. 

and presented as the histogram shown in Fig. 10. 

The blue and orange lines are the speed of the oncoming The x-axis represents the TTC, and the y-axis represents the vehicle and autonomous vehicle respectfully. When interacting frequency of the corresponding TTC. From the figure, it can be with the aggressive human driver, the left-turning autonomous seen that in most of the interactive scenarios, the left-turning vehicle estimates the human driver’s behaviour in real-time, vehicle takes a time gap of around 4.5s. The real-world driving then decrease its speed and yield to the oncoming traffic TTC distribution presented in Fig. 6 shows that the left bound accordingly. When interacting with more conservative human is around 5s. 

drivers, the ego vehicle increases its speed and tries to pass The major difference between the simulation and real-world the intersection as quickly as possible, before getting back to driving behaviour is due to the intensity of the scenario. The its normal driving speed at intersections. 

recorded dataset has various kinds of scenarios where the From these results, the proposed framework is shown to be oncoming lane is very empty. In our testing simulations, able to properly interact with various types of human drivers. 

the scenarios were set to be much more interactive, which At the same time, estimates the aggressiveness of the sur-might not be very common in the real world. Therefore, the rounding vehicle and interact with them accordingly. Another simulation results have larger portions over the 5s side and feature of the proposed framework is also tested, which is how fewer portions over the 10s side. However, the simulation similar dose autonomous vehicles behave like experienced-results of the accepted gap lie within the range of real-world human drivers. One of the key features that influence the driving data, which shows that the autonomous vehicle is riding experience as well as the receptivity of the surrounding able to perform like humans in this aspect. To evaluate human drivers is the accepted time gap that the left-turning the effectiveness of our proposed framework in enabling the Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on February 13,2025 at 07:49:36 UTC from IEEE Xplore. Restrictions apply. 





SHU et al.: HUMAN INSPIRED AUTONOMOUS INTERSECTION HANDLING USING GAME THEORY

## 11369

Fig. 12. 

Scenario simulation result of left-turning at a intersection with the presence of human-driven vehicle and pedestrians. 

While the driving style is the same as the one in Fig. 8 \(c\). 

The pedestrian is set to cross the intersection with a nominal speed of 1 m/s and a minimum safety gap of 3 m. Without the loss of generality, the human driver’s driving style is neutral, and all the pedestrians are set with a static driving style. The trajectories of the traffic participants are plotted in Fig. 12 \(a\), 

Fig. 11. 

Comparison between proposed framework with a baseline method. 

with time information as time stamps \(orange dots\) along the trajectory. The trajectories for the autonomous vehicle \(red\), human-driven vehicle \(blue\) and pedestrians are represented autonomous vehicle to make sound decisions considering as orange, blue and green lines accordingly. 

various driving characteristics, a comparison experiment has From Fig. 8 \(c\) and Fig. 12 \(a\) it can be found in a been done between our proposed method and a baseline scenario with conservative drivers and no pedestrians, the decision-making framework that considers a uniform driver left-turning vehicle makes the left turn before the oncoming model while making decisions. 

vehicle. However, in the same scenario with a pedestrian, the The

testing

scenario

is

selected

as

a

left-turning

autonomous vehicle yield to the oncoming vehicle due to the autonomous vehicle interacting with a conservative oncoming left-turning path was temporarily blocked by the pedestrian. 

human-driven vehicle and the results are presented in Fig. 11. 

A more detailed speed profile of each traffic participant Fig. 11\(a\) and Fig. 11\(b\) represent the baseline and our could be found in Fig. 12 \(b\) where the colour of the speed proposed framework accordingly. 

profiles match the colour of the trajectories. It could be found Trajectories of the vehicles of each scenario are presented that the conservative human driver decreases its speed first, on the left of Fig. 11, the colour indicates the speed, and while the autonomous vehicle also decreases the speed too to the dots are the time stamps. More specific speed profiles are yield to the pedestrian and the oncoming vehicle. Then the presented on the right. The testing result shows that when oncoming vehicle feels safe and pulls through the intersection dealing with drivers other than neutral drivers, the proposed at its nominal speed. The pedestrian, on the other hand, tries framework enables the ego vehicle to adapt appropriately to to increase the speed and pass as quickly as possible. The the surrounding driver. At the same time, it maintains a higher simulation results show that the autonomous vehicle is able speed to ensure higher travel efficiency while keeping a safe to consider the interaction with both drivers and pedestrians. 

distance from human-driven vehicles. 

The real-time performance of the decision-making algorithm is also tested. The computational time used for each time B. Two Vehicles and a Pedestrian Interaction Scenario step is recorded at each simulation. The computational time The framework is also tested in an intersection scenario with over the length of one single time step is calculated and its both oncoming vehicles and pedestrians. Which is demon-distribution is presented in Fig. 13. This figure shows that strated in Fig. 12 \(a\). The blue pedestrian icon is the starting in most of the cases, the algorithm is able to use less that point of the pedestrian and the pink arrow indicates the 10% of the time in one time cycle, and in severe cases, still direction that the pedestrian is walking at. 

be able to operate in real-time. Thus, the simulation results All the vehicles in the new pedestrian-evolved scenario have show that the proposed framework is feasible in real-world a similar starting position and speed as the scenario in Fig. 8. 

application with respect to timing perspective. It is also worth Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on February 13,2025 at 07:49:36 UTC from IEEE Xplore. Restrictions apply. 

11370

IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS, VOL. 24, NO. 10, OCTOBER 2023

\[6\] S. Li, K. Shu, Y. Zhou, D. Cao, and B. Ran, “Cooperative critical turning point-based decision-making and planning for CAVH intersection management system,” IEEE Trans. Intell. Transp. Syst., vol. 23, no. 8, pp. 11062–11072, Aug. 2022. 

\[7\] T. Fernando, S. Denman, S. Sridharan, and C. Fookes, “Deep inverse reinforcement learning for behavior prediction in autonomous driving: Accurate forecasts of vehicle motion,” IEEE Signal Process. Mag., vol. 38, no. 1, pp. 87–96, Jan. 2021. 

\[8\] G. Li et al., “Deep reinforcement learning enabled decision-making for autonomous driving at intersections,” Automot. Innov., vol. 3, no. 4, pp. 374–385, Dec. 2020. 

\[9\] W. Hu et al., “A rear anti-collision decision-making methodology based on deep reinforcement learning for autonomous commercial vehicles,” 

IEEE Sensors J., vol. 22, no. 16, pp. 16370–16380, Aug. 2022. 

Fig. 13. 

Real-time performance evaluation. 

\[10\] P. Hang, C. Lv, Y. Xing, C. Huang, and Z. Hu, “Human-like decision making for autonomous driving: A noncooperative game theoretic approach,” IEEE Trans. Intell. Transp. Syst., vol. 22, no. 4, pp. 2076–2087, Apr. 2021. 

noting that though the simulation scenarios are autonomous

\[11\] A. Turnwald, D. Althoff, D. Wollherr, and M. Buss, “Understanding vehicles making left turns, the proposed framework could also human avoidance behavior: Interaction-aware decision making based on be applied in other operating conditions, such as right-turning game theory,” Int. J. Social Robot., vol. 8, no. 2, pp. 331–351, Apr. 2016. 

\[12\] N. Li, Y. Yao, I. Kolmanovsky, E. Atkins, and A. R. Girard, “Game-scenarios by modifying the autonomous vehicle’s nominal path theoretic modeling of multi-vehicle interactions at uncontrolled intersec-and speed profile in the decision-making process. 

tions,” IEEE Trans. Intell. Transp. Syst., vol. 23, no. 2, pp. 1428–1442, Feb. 2022. 

\[13\] Y. Rahmati, M. K. Hosseini, and A. Talebpour, “Helping automated vehi-VI. CONCLUSION

cles with left-turn maneuvers: A game theory-based decision framework for conflicting maneuvers at intersections,” IEEE Trans. Intell. Transp. 

We proposed a game-theory-based intersection handling Syst., vol. 23, no. 8, pp. 11877–11890, Aug. 2022. 

method considering the presence of traffic participants with

\[14\] K. Liu, N. Li, H. E. Tseng, I. Kolmanovsky, and A. Girard, “Interaction-different driving styles. The autonomous vehicle is able to aware trajectory prediction and planning for autonomous vehicles in forced merge scenarios,” 2021, arXiv:2112.07624. 

properly estimate the driving style of a human driver and

\[15\] M. Bouton, A. Nakhaei, K. Fujimura, and M. J. Kochenderfer, then interact with it accordingly. The simulation results show

“Cooperation-aware reinforcement learning for merging in dense traf-that the autonomous vehicle’s behaviour is close to real-world fic,” in Proc. IEEE Intell. Transp. Syst. Conf. \(ITSC\), Oct. 2019, pp. 3441–3447. 

drivers, which shows that the interaction modelling as well

\[16\] S. Karimi and A. Vahidi, “Receding horizon motion planning for as the driving style estimation works accordingly. Also, the automated lane change and merge using Monte Carlo tree search and framework is able to operate in real-time which increases the level-K game theory,” in Proc. Amer. Control Conf. \(ACC\), Jul. 2020, pp. 1223–1228. 

feasibility of the proposed framework. 

\[17\] S. Pruekprasert, X. Zhang, J. Dubut, C. Huang, and M. Kishida, The proposed framework is able to find a Nash equilibrium

“Decision making for autonomous vehicles at unsignalized intersection \(optimal solution\) of the formulated decision-making game in presence of malicious vehicles,” in Proc. IEEE Intell. Transp. Syst. 

in real time in most cases. However, finding the global Nash Conf. \(ITSC\), Oct. 2019, pp. 2299–2304. 

\[18\] N. Li, I. Kolmanovsky, A. Girard, and Y. Yildiz, “Game theoretic model-equilibrium is challenging for differential games, and it cannot ing of vehicle interactions at unsignalized intersections and application be guaranteed \[20\]. One reason for this is that the linear to autonomous vehicle control,” in Proc. Annu. Amer. Control Conf. 

approximation may not hold if the new iterated states deviate \(ACC\), Jun. 2018, pp. 3215–3220. 

\[19\] P. Hang, C. Huang, Z. Hu, and C. Lv, “Driving conflict resolution too much from the previous states. Therefore, our future work of autonomous vehicles at unsignalized intersections: A differential will focus on improving the framework to better preserve game approach,” IEEE/ASME Trans. Mechatronics, vol. 27, no. 6, the linearity and guarantee that the vehicle finds a Nash pp. 5136–5146, Dec. 2022. 

equilibrium. One possible solution is to implement a planner

\[20\] D. Fridovich-Keil, E. Ratner, L. Peters, A. D. Dragan, and C. J. Tomlin, 

“Efficient iterative linear-quadratic approximations for nonlinear multi-before solving the game, which can help decrease the deviation player general-sum differential games,” in Proc. IEEE Int. Conf. Robot. 

of the states’ offsets and improve the accuracy of the solution. 

Autom. \(ICRA\), May 2020, pp. 1475–1481. 

\[21\] D. Fridovich-Keil, V. Rubies-Royo, and C. J. Tomlin, “An iterative quadratic method for general-sum differential games with feedback REFERENCES

linearizable dynamics,” in Proc. IEEE Int. Conf. Robot. Autom. \(ICRA\), May 2020, pp. 2216–2222. 

\[1\] K. Shu et al., “Autonomous driving at intersections: A behavior-oriented

\[22\] H. Xu, Y. Gao, F. Yu, and T. Darrell, “End-to-end learning of driving critical-turning-point approach for decision making,” IEEE/ASME Trans. 

models from large-scale video datasets,” in Proc. IEEE Conf. Comput. 

Mechatronics, vol. 27, no. 1, pp. 234–244, Feb. 2022. 

Vis. Pattern Recognit. \(CVPR\), Jul. 2017, pp. 3530–3538. 

\[2\] K. Shu et al., “Autonomous driving at intersections: A critical-turning-

\[23\] J. Peng, Y. Guo, R. Fu, W. Yuan, and C. Wang, “Multi-parameter point approach for left turns,” in Proc. IEEE 23rd Int. Conf. Intell. 

prediction of drivers’ lane-changing behaviour with neural network Transp. Syst. \(ITSC\), Sep. 2020, pp. 1–6. 

model,” Appl. Ergonom., vol. 50, pp. 207–217, Sep. 2015. 

\[3\] M. S. Shirazi and B. T. Morris, “Looking at intersections: A survey of

\[24\] K. Kreutz and J. Eggert, “Analysis of the generalized intelligent driver intersection monitoring, behavior and safety analysis of recent studies,” 

model \(GIDM\) for uncontrolled intersections,” in Proc. IEEE Int. Intell. 

IEEE Trans. Intell. Transp. Syst., vol. 18, no. 1, pp. 4–24, Jan. 2017. 

Transp. Syst. Conf. \(ITSC\), Sep. 2021, pp. 3223–3230. 

\[4\] Y. Wiseman, “Autonomous vehicles,” in Research Anthology on Cross-

\[25\] S. Albeaik et al., “Limitations and improvements of the intelligent driver Disciplinary Designs and Applications of Automation. Hershey, PA, model \(IDM\),” SIAM J. Appl. Dyn. Syst., vol. 21, no. 3, pp. 1862–1892, USA: IGI Global, 2022, pp. 878–889. 

Sep. 2022. 

\[5\] S. Li, K. Shu, C. Chen, and D. Cao, “Planning and decision-making for

\[26\] Q. Xin, R. Fu, W. Yuan, Q. Liu, and S. Yu, “Predictive intelligent connected autonomous vehicles at road intersections: A review,” Chin. 

driver model for eco-driving using upcoming traffic signal information,” 

J. Mech. Eng., vol. 34, no. 1, pp. 1–18, Dec. 2021. 

Phys. A, Stat. Mech. Appl., vol. 508, pp. 806–823, Oct. 2018. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on February 13,2025 at 07:49:36 UTC from IEEE Xplore. Restrictions apply. 





SHU et al.: HUMAN INSPIRED AUTONOMOUS INTERSECTION HANDLING USING GAME THEORY

## 11371

\[27\] W. Zhan et al., “INTERACTION dataset: An international, adversarial Shen Li \(Member, IEEE\) received the Ph.D. 

and cooperative motion dataset in interactive driving scenarios with degree from the University of Wisconsin Madison, semantic maps,” 2019, arXiv:1910.03088. 

Madison, WI, USA, in 2018. He is currently

\[28\] F. R. Faye, “Modelling of driver’s gap acceptance for evaluation of traffic a Research Associate with Tsinghua University, flow characteristics at unsignalized intersection in urban area, Ethiopia,” 

Beijing, China. His research interests include intel-Amer. J. Traffic Transp. Eng., vol. 5, no. 5, pp. 57–64, 2020. 

ligent transportation systems, architecture design

\[29\] F. Grognard, R. Sepulchre, and G. Bastin, “Global stabilization of of CAVH system, vehicle-infrastructure cooperative feedforward systems with exponentially unstable Jacobian linearization,” 

planning and decision method, traffic data mining Syst. Control Lett., vol. 37, no. 2, pp. 107–115, Jun. 1999. 

based on cellular data, and traffic operations and

\[30\] T. Ba¸sar and G. J. Olsder, Dynamic Noncooperative Game Theory. 

management. 

Philadelphia, PA, USA: SIAM, 1998. 

Mohammad Pirani \(Member, IEEE\) received the B.Sc. degree in mechanical engineering from the Keqi

Shu

\(Graduate Student Member, IEEE\)

Amirkabir University of Technology in 2011 and received the B.Sc. degree from Northwestern Poly-the M.A.Sc. degree in electrical and computer technical University, Xi’an, Shaanxi, China, and the engineering and the Ph.D. degree in mechanical master’s degree in mechanical and mechatronics and mechatronics engineering from the Univer-engineering with the University of Waterloo, ON, sity of Waterloo in 2014 and 2017, respectively. 

Canada, where he is currently pursuing the Ph.D. 

He held a post-doctoral researcher positions with degree in mechanical and mechatronics engineering. 

the KTH Royal Institute of Technology, Sweden, His research interests include interactive planning from 2018 to 2019, and the University of Toronto and decision-making of autonomous vehicles. 

from 2019 to 2021. He is currently a Research Assis-tant Professor with the Department of Mechanical and Mechatronics Engineering, University of Waterloo. His research interests include resilient and fault-tolerant control, networked control systems, and multi-agent systems. 

Reza Valiollahi Mehrizi received the M.Sc. and Amir Khajepour \(Senior Member, IEEE\) is cur-Ph.D. degrees in statistics from the University of rently a Professor of mechanical and mechatron-Waterloo, ON, Canada, in 2017 and 2021, respec-ics engineering with the University of Waterloo, tively. He is currently employed as a Data Scien-Waterloo, ON, Canada, where he is also with the tist and a Statistical Researcher with the Mecha-Canada Research Chair of mechatronic vehicle sys-tronic Vehicular System Laboratory, University of tems. He has developed an Extensive Research Waterloo. His research interests include building Program that applies his expertise in several key and developing predictive models using machine multidisciplinary areas. He is a fellow of the Engi-learning methods, deep learning object detection and neering Institute of Canada, the American Society semantic image segmentation, experimental designs, of Mechanical Engineers, and the Canadian Society and survival analysis. 

of Mechanical Engineering. 

Authorized licensed use limited to: Universita degli Studi di Napoli Federico II. Downloaded on February 13,2025 at 07:49:36 UTC from IEEE Xplore. Restrictions apply.



