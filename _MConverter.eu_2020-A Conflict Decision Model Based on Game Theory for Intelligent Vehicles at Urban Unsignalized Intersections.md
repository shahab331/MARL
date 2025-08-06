Received September 19, 2020, accepted October 5, 2020, date of publication October 19, 2020, date of current version October 28, 2020. 

*Digital Object Identifier 10.1109/ACCESS.2020.3031674*

A Conflict Decision Model Based on Game

Theory for Intelligent Vehicles at Urban

Unsignalized Intersections

XUEMEI CHEN , YUFAN SUN , YANGJIAXIN OU, XUELONG ZHENG , 

ZIJIA WANG , AND MENGXI LI Intelligent Vehicle Research Center, School of Mechanical Engineering, Beijing Institute of Technology, Beijing 100081, China Corresponding author: Xuemei Chen \(chenxue781@126.com\) This work was supported in part by the Youth Science Fund under Grant 51705021, in part by the Automobile Industry Joint Fund of the National Natural Science Foundation of China under Grant U1764261, in part by the Beijing Municipal Science and Technology Project under Grant Z191100007419010, and in part by the Key Laboratory for New Technology Application of Road Conveyance of Jiangsu Province under Grant BM20082061706. 

**ABSTRACT **This article proposed a novel conflict decision model for intelligent vehicles based on game theory with analyzing the interaction behaviors between vehicles at urban unsignalized intersections. 

The proposed model can help intelligent vehicles cross intersections safely and more efficiently. Firstly, we developed an inference model for types of interactions among vehicles based on fuzzy logic. Then, the driving data was collected at urban unsignalized intersections by subgrade sensors and a retrofit intelligent vehicle and it was used in verifying the proposed inference model. After that, a conflict decision model considering safety, efficiency and comfort for intelligent vehicles based on game theory, was proposed to select the optimal driving strategies. Finally, a simulation and verification platform was built using Matlab/Simulink & Prescan. And the validity and effectiveness of the model were proved by simulation experiments. The results show the decision model can effectively help vehicles avoid conflicts and save their time spent in crossing intersections by 15 percent. 

**INDEX TERMS **Intelligent vehicle, urban unsignalized intersection, decision-making model, game theory, conflict resolution. 

**I. INTRODUCTION**

decision-making model of intelligent vehicles based on Finite Intelligent vehicles have drawn increasing attentions in recent State Machine \(FSM\) to predict the vehicle behaviors in years and many researchers have made great achievements scenarios of intersection. Zyner *et al. *\[2\] proposed a system about them. Due to the complexity of traffic at urban envi-with Recurrent Neural Network to infer drivers’ intentions at ronments, it is of great significance to resolve conflicts the roundabout. Xiong *et al. *\[3\] and Song *et al. *\[4\] proposed a among traffic participants at urban unsignalized intersec-prediction method of driving intentions of surrounding vehi-tions. Nowadays, researchers have employed methods like cles based on HMM to realize the cooperative control among gap acceptance model, conflict table algorithm and vector vehicles at intersections. In these researches, the accuracy of graph algorithm to solve the conflicts. However, these models predicting drivers’ intentions is limited by the quality of the just explained the passing priorities of vehicles crossing the collected data and the decision-making process of vehicles intersections, ignoring the interactions between intelligent has not been quantified. 

vehicles and other traffic participants. 

With the good performance in solving complex problems, Scholars at home and abroad have put more focus on game theory is widely used in conflict resolution among the interactions between intelligent vehicles and human-vehicles. It can quantify vehicles’ decision-making process driving vehicles recently. Arda *et al. *\[1\] established a to ensure that they could always select optimal actions at each moment. Wang *et al. *\[5\] developed a prediction method The associate editor coordinating the review of this manuscript and for lane-changing and car-following based on optimal con-approving it for publication was Francisco J. Garcia-Penalvo

. 

trol and dynamic game theory in the scenarios of highway. 

189546

This work is licensed under a Creative Commons Attribution 4.0 License. For more information, see https://creativecommons.org/licenses/by/4.0/

VOLUME 8, 2020





X. Chen *et al. *: Conflict Decision Model Based on Game Theory for Intelligent Vehicles at Urban Unsignalized Intersections Bouderba and Moussa \[6\] applied a dilemma game in unsignalized intersections and studied the impacts of the adopted method on the traffic capacity. This model employed game theory to study the microscopic traffic flow in intersections. Sasinee *et al. *\[7\] established a decision-making model in a unsignalized intersection in presence of selfish and irrational vehicles. In this article, the opponent vehicle is preset to be aggressive, ignoring the diversity of drivers. 

In \[8\], \[9\], we have conducted researches on the decision-making process of intelligent vehicles in complex urban environments. To overcome the problems mentioned above, This **FIGURE 1. **The elements of game theory. 

article proposed a decision-making model based on game theory for intelligent vehicles to resolve conflicts, the con-the advantage of considering the information interactions tributions are listed as:

between players, it is suitable for the decision making of

\(1\) A decision-making model based on game theory for intelligent vehicles at urban intersections. A game process intelligent vehicles at urban unsignalized intersections is pro-consists of players, actions, information, strategies, payoffs, posed with the considerations of driving safety, efficiency and results, and equilibrium. And players, strategies and payoffs comfort. 

are three basic elements \(Fig. 1\). 

\(2\) The validity and effectiveness of the model are verified

\(1\) Players: The decision makers in the game. Players by Matlab/Simulink & Prescan. The results show the model maximize their utility values by choosing optimal actions or can provide help intelligent vehicles pass through intersec-strategies. 

tions more efficiently. 

\(2\) Actions: The decision variables of a player at a certain The remainder of this article is organized as follows: moment in the game. Generally, *ai * represents a specific action Section II describes the methodologies and the data acqui-of the *i* th player, and *Ai *= \{ *ai*\} represents a set of all actions sition process in this article. Section III analyzes the inter-available for the *i* th player to choose. 

action behaviors between vehicles at urban intersections and \(3\) Information: The understandings of game-related proposes a decision-making model for intelligent vehicles knowledge obtained by players in the game. 

based on game theory. The simulation verification platform

\(4\) Strategies: The action rules of players with given infor-to evaluate the effectiveness and reliability of the proposed mation. Generally, *si * represents a specific strategy of the model is introduced in Section IV. In Section V, conclusions *i* th player, and *Si *= \{ *si*\} represents the set of all strategies and future works are presented. 

available for the *i* th player to choose. 

\(5\) Payoffs: The utility values obtained by a player under **II. METHODS AND DATA**

specific strategies, commonly known as the revenue function. 

A. METHODS

\(6\) Results: The indicators that can draw the interests of 1\) FUZZY LOGIC INFERENCE

game analysts, such as balanced strategy combinations, bal-Fuzzy logic inference is a classical method that can imitate anced action combinations, balanced payoff combinations. 

the inference modes of the human brain to deal with uncertain \(7\) Equilibrium: The optimal strategies of all players, systems by using fuzzy sets and fuzzy rules, which is widely which is generally represented as: *S*∗ = *s*∗, *s*∗, . . . , *s*∗, . . . , 1

2

*i*

applied in logic control modeling, software engineering and *s*∗ 

*n *. where, *s*∗ is the optimal strategy of the *i* th player. 

*i*

computer science researches. A fuzzy logic inference controller consists of inputs, outputs, membership functions and 3\) NASH EQUILIBRIUM

fuzzy control rules:

Generally, the solution of a static game with complete infor-F = \( *I *, *O*, *M *, *R*\) \(1\)

mation is called Nash equilibrium, which is a strategy set that cannot achieve a better situation by changing the players’

where: *I * and *O * refer to the input variables and output vari-actions in the game \[10\]–\[12\]. This means that there is no ables of uncertain systems, respectively, *M * refers to the strategy set superior to the Nash equilibrium. In a game *G*

membership functions, which can convert the inputs *I * into with *n * players, *s* 0 and *s* 00 refer to the two strategies can be the fuzzy variables which can be recognized by the system, *i*

*i*

selected by a player, *s*

*R * refers to the fuzzy reference rules, which are mapping

− *i * refers to the strategies of other players. When \(2\) is satisfied, we call that strategy *s* 0 is obviously relationships from inputs to outputs based on the experience *i*

better than strategy *s* 00. When \(3\) is satisfied, the strategy set of experts. 

*i*

*S*∗ = *s*∗, *s*∗, . . . , *s*∗, . . . , *s*∗ is called a Nash equilibrium 1

2

*i*

*n*

of *G*. 

2\) GAME THEORY

Game theory is a mathematical method to study the competitive phenomena and it considers the predictive behaviors and *ui*\( *s* 0, 

, 

*i s*− *i*\) > *ui*\( *s* 00

*i*

*s*− *i*\)

\(2\)

actual behaviors of individuals in the game \[10\]–\[12\]. With *ui*\( *s*∗, 

\) > 

\), 

∀

*i*

*s*∗− *i*

*ui*\( *si*, *s*∗− *i*

*si *∈ *Si*, ∀ *i*

\(3\)

VOLUME 8, 2020

189547





X. Chen *et al. *: Conflict Decision Model Based on Game Theory for Intelligent Vehicles at Urban Unsignalized Intersections including longitudinal and lateral coordinates, velocities, accelerations. 

2\) VEHICLE DATA ACQUISITION

The vehicle data were collected by the FORD referee vehicle, which was equipped with several kinds of sensors \(Fig. 2\(b\)\). 

The binocular cameras and LIDAR can detect, track and localize dynamic objects. The outputs of the fusion algorithm are positions of vehicles. 

**III. THE DECISION-MAING MODEL BASED**

**ON GAME THEORY**

A. RESEARCH ON INTERACTION BEHAVIORS

BETWEEN VEHICLES

Researching interaction behaviors between vehicles is helpful for understanding dynamic traffic scenarios and can further improve the legitimacy of decision-making models for intelligent vehicles. The interaction types between intelligent vehicles \(IV\) and human-driving vehicles \(HD\) are determined by the crossing intentions of IV and the driving types of HD. 

1\) CROSSING INTENTIONS

The crossing intentions are mainly determined by the pressure *P * and the time difference *T* c in conflicts. A fuzzy inference model for crossing intentions is established with *P*, *T* c as the inputs and crossing intentions of vehicles as the outputs. 

**FIGURE 2. **Data acquisition. 

*a: PRESSURE*

where, *s*

When vehicles approach the conflict point, the conflict presi refers to the strategy selected by *i* th player and *s*∗

1

represents the optimal one, *S*∗

= *s*∗, . . . , *s*∗ , *s*∗ , . . . , sure *P * increases and the probability of crossing will increase

− *i*

1

*i*−1

*i*\+1

*s*∗ 

too. Assuming that the effective communication range at the *n*

refers to the strategy set of other players, *ui * refers to the payoff of *i* th player under given strategy set. 

intersection is 150m, the pressure *P * is set as 0 when the vehicles are on the boundary of this area. *P * is defined as: B. DATA

*Li*\( *t*\)

The data used in this article was collected by a subgrade *P *= 1 −

\(4\)

150

camera and a retrofit referee vehicle in the 2017-2018 World Intelligent Driving Challenge \(WIDC\). The symmetric expo-where, *Li*\(t\) refers to distance of the *i* th vehicle to the conflict nential moving average method \(sEMA\) was adopted to point. The range of *P * is empirically set as \{0.1, 0.3, 0.5, 0.7, smooth the training data \[13\]. 

0.9\} and the fuzzy set is represented as \{very small \(VS\), small \(S\), medium \(M\), large \(L\), large \(VL\)\}. 

1\) SUBGRADE DATA ACQUISITION

The subgrade data collecting process is as follows: *b: TIME*

\(1\) Use map software to calibrate the reference points. 

The collision possibilities among vehicles should be consid-Select 5 \(at least 5\) reference points in the video interface ered when intelligent vehicles cross unsignalized urban inter-one after another. The red dots represent the reference points sections. The time difference *T* c between the two vehicles marked manually, and the blue ones are the image coordinates passing through the conflict point is used to evaluate the risk of these reference points, which are transformed by their levels of collisions, which is defined as:

geodetic coordinates. Once the red dots and blue dots coin-L

*L*





1\( *t *\)

2\( *t *\) 

cide, the coordinate calibration can be regarded as accurate. 

*T* c = 

−



\(5\)

*v* 1\( *t *\)

*v* 2\( *t*\) 

The processing is shown in Fig. 2\(a\). 

\(2\) Add the vehicle ID. The trajectories of intelli-where, *L* 1\( *t*\) and *L* 2\( *t*\) refer to the distances of IV and HD

gent vehicles and human-driving vehicles are extracted, to the conflict point, respectively, *v* 1\( *t*\) and *v* 2\( *t*\) refer to including positions, velocities, accelerations, etc., to ana-the velocities of IV and HD, respectively. The range of time lyze the behaviors of vehicles. The partial trajectory data difference *T* c is empirically set as \{0, 3, 5, 7, 10\} and the fuzzy of vehicles at the intersection are shown in Table 1, set is \{VL, L, M, S, VS\} as defined above. 

189548

VOLUME 8, 2020





X. Chen *et al. *: Conflict Decision Model Based on Game Theory for Intelligent Vehicles at Urban Unsignalized Intersections **TABLE 1. **Partial trajectory data of vehicles at the intersection. 

**TABLE 2. **Fuzzy logic rules of crossing intentions \(IV\). 

**TABLE 3. **Fuzzy logic rules of driving types \(HD\). 

**FIGURE 3. **The work process of interaction model for vehicles. 

**TABLE 4. **Fuzzy logic rules of cooperation levels. 

Similarly, the crossing intentions of IV can be devided into \{very high\(VH\), high\(H\), medium\(M\), low\(L\), very low\(VL\)\}. Based on these analysis, the corresponding fuzzy logic rules are empirically listed in Table 2. The larger *P * is and the larger *T* c is, the more possible IV tends to cross. On the vehicles is established to infer the cooperation levels between contrary, the smaller *P * is and the smaller *T* c is, the less likely the two vehicles, as shown in Fig. 3. Their cooperation levels IV crosses. 

are discretized as \{H, M, L\}, corresponding to cooperative relationship, unclear relationship and competitive relation-2\) DRIVING TYPES

ship, respectively. The fuzzy logic rules of interaction model The willingness that vehicles accept or reject the crossing for vehicles are shown in Table 4. 

requests from other vehicles varies with different driving The fuzzy logic surface of the interaction model is shown types. With the velocity and acceleration of HD as inputs, in Fig. 4. Furtherly, the cooperation levels *p * between vehicles a fuzzy inference model for driving types is established are discretized as three specific values:

based on experts’ experience. In this article, the driving types



are divided into 3 types \{conservative\(C\), ordinary\(O\) and 1

0 < *p *≤ 0.4





impulsive\(I\)\}, and the vehicle velocity’ and acceleration’

cooperation levels between vehicles =

2

0.4 < *p *≤ 0.7

fuzzy sets are \{VL, L, M, S, VS\}, \{L, M, S\} respectively. 



 3

0.7 < *p *≤ 1

The fuzzy logic rules are shown in Table 3. 

\(6\)

3\) FUZZY INFERENCE PROCESS

where: 3, 2 and 1 represent the cooperative relation-Based on the crossing intentions of IV and the driving types ship, unclear relationship and competitive relationship, of HD, a fuzzy inference model for interaction types among respectively. 

VOLUME 8, 2020

189549





X. Chen *et al. *: Conflict Decision Model Based on Game Theory for Intelligent Vehicles at Urban Unsignalized Intersections C. DECISION-MAKING MODEL BASED ON GAME THEORY

By analyzing the decision process of human drivers crossing intersections with conflicts, the conflict problem is simplified as a two-player game model. Four basic elements are as follows \[15\]:

\(1\) The players set in the game is: *C *= \{ *C* 1, *C* 2\}

\(8\)

**FIGURE 4. **Fuzzy logic surface of interaction model for vehicles. 

where: *Ci * refers to the *i* th players, HD and IV are two players By predicting the cooperation levels between vehicles, in this model. 

their interaction behaviors under mixed traffic conditions

\(2\) The strategy set of all players is: are analyzed and it provides a basis for decision-making models of intelligent vehicles at urban unsignalized intersections. 

*S *= \{ *S* 1, *S* 2\}

\(9\)

B. ANALYSIS OF CONFLICTS AT URBAN

UNSIGNALIZED INTERSECTIONS

where: *Si*, *i *= 1, 2 refers to driving strategy set of vehicle *Ci*, Fig. 5\(a\) shows the conflicts between intelligent vehicles which is consisted of a series of driving strategies at different and other vehicles at intersections, where *C* ABCD refers to timesteps *si*, *i *= 1, 2, . . . , n. 

the conflict area, HD and IV refer to the human-driving \(3\) *Ui * refers to the expected utility value obtained by vehicle and the intelligent vehicle, respectively. When IV

vehicle *Ci*, which is not only related to its own strategy, but enters the conflict area, the decision-making model based also to the strategy of another vehicle. Therefore, the utility on game theory is established to avoid collisions in space value of vehicle *Ci * is represented as *Ui*\( *s* 1, *s* 2\). Where: *si* by controlling vehicles crossing the intersections at different refers to the strategy taken by vehicle *Ci *\(i.e. *si *∈ *Si*\). 

times. This article only focuses on the conflicts between

\(4\) A game with two vehicles can be represented as *G *=



motor vehicles. The conflicts between vehicles and non-C, *S*, *U *. If the strategy set *S*∗ = *s*∗, *s*∗ is a Nash equilib-1

2

motor vehicles or pedestrians will be discussed in future rium, the following must be satisfied:

work. 

To explicitly discuss the decision-making model, some assumptions are made as follows:

*Ui*\( *s*∗, 

\) ≥

, 

\), 

∀

*i*

*s*∗− *i*

*Ui*\( *si s*∗− *i*

*si *∈ *Si*, *i *= 1, 2

\(10\)

\(1\) Vehicles are all equipped with V2V systems so that they can obtain the driving characteristics of other vehicles, which where, *s*∗ refers to the optimal strategy selected by vehicle lays the foundation for the establishment of game theory *i*

*C*

refers to the strategy of another vehicle, *U*

model. 

*i*, *s*∗

− *i*

*i * refers to

the utility value of vehicle *C*

\(2\) Players in the game make decisions simultaneously. 

*i*, *Si * refers to the strategy set of vehicle *C*

In order to efficiently analyze the conflicts between IV

*i*. 

and HD, EPET\(Estimating Post Encroachment Time\) \[14\]

is employed, which is a vital index to depict the collisions 1\) REVENUE FUNCTION SELECTION

between vehicles with any angle. It is defined as time differ-The driving revenue is represented by the utility value *U*

ence between the former vehicle leaving the conflict area and in the proposed model, which is not only related to current the latter one entering the area, as shown in Fig. 5\(b\). 

conditions of vehicles, but also to the potential conflict levels \(

between them. Therefore, the safety revenue, efficiency rev-

| *T* IV1 − *T* HD2|, *T* HD1 ≤ *T* IV1 ≤ *T* HD2

EPET = f\( *x*\) =

\(7\)

enue and comfort revenue are comprehensively combined to

| *T* IV2 − *T* HD1|, *T* IV1 ≤ *T* HD1 ≤ *T* IV2

define the driving revenue in this section. 

where, *T* HD1 refers to the time when HD enters the conflict area, *T* HD2 refers to the time when HD leaves the conflict area, *a: SAFETY*

*T* IV1 refers to the time when the IV enters the conflict area, The safety mainly refers to the factors that can increase the *T* IV2 refers to the time when IV leaves the conflict area. When severity of the conflicts between vehicles, which is repre-T IV1 > *T* HD2, *T* HD1 > *T* IV2 are satisfied, there is no conflict sented by the time difference 1 *T * between the two vehicles among the two vehicles and they can cross the intersection arriving at the conflict point. The smaller the 1 *T * is, the with original driving mode. On the contrary, the conflicts smaller the driving revenue is. Otherwise, the larger the 1 *T*

among vehicles exist and they have to cross with cooperative is, the larger the driving revenue is. Considering the influence driving mode. 

of driving types on the driving strategies, the safety revenue 189550

VOLUME 8, 2020





X. Chen *et al. *: Conflict Decision Model Based on Game Theory for Intelligent Vehicles at Urban Unsignalized Intersections **FIGURE 5. **\(a\) Description of conflicts at intersections \(b\) The principle of EPET. 

is set as follows:

where: α, β, γ refer to the weights of the safety revenue, 



efficiency revenue and comfort revenue respectively, α \+

*U*



*safe *= *u *\(1 *T *\) = exp \(1 *T *\)



β \+ γ = 1. Then the whole problem can be expressed as:





1





" 

\#







2





2





*v*

*L*

*v*



To solve the Nash equilibrium of the model \(e.g. the optimal





1 \( *t *\)

1 \( *t *\)

1 \( *t *\)

 1



*T *= | *T* 1 − *T* 2| = 

\+2

−



driving strategies\) to maximize the overall driving revenue





*a*

*a*

*a*





1 \( *t *\)

1 \( *t *\)

1 \( *t *\)



based on \(14\). 



1



" 

\# 2





2









*v* 2 \( *t*\)

*L* 2 \( *t*\)

*v* 2 \( *t*\) 







−

\+ 2

−







*a*

*a*

*a*

2\) COOPERATIVE DECISION-MAKING



2 \( *t *\)

2 \( *t *\)

2 \( *t *\)















PROCESS OF VEHICLES



 *i *= 1, 2; 

*t *= 1, 2, . . . , *N*

The cooperative decision-making process of HD and IV at \(11\)

urban intersections filled with potential conflicts is shown where: *u*\(·\) refers to normalization, *v* in Fig. 6. And the decision-making model outputs the *i*\( *t *\), and *ai*\( *t *\) refer to the velocity and acceleration of the *i* th vehicle, respectively, *L*

optimal driving strategies of the two vehicles, as shown *i*\( *t *\)

refers to the distance of the *i* th vehicle to the conflict point. 

in \(15\):



n

\(1\)

\(1\)

o

*b: EFFICIENCY*

*S*

*a*

, *a *, · · · , *a*\(1\)



1 =

1

2

*n*



The efficiency refers to that vehicles expect to cross intersec-n

\(2\)

\(2\)

o

\(15\)

tions as quickly as possible to avoid the time delay caused by

, 

, 

 *S* 2 =

*a*

*a*

· · · , *a*\(2\)



1

2

*n*

decelerating or waiting. The efficiency revenue is set as:

 *U*

A series of deceleration or acceleration actions are



*efficence *= *u*\(1 *vi*\)

1 *v*

*i *= 1, 2 \(12\)

included in the optimal strategies, which decide whether *i *= *vi*\( *t *\+ 1\) − *vi*\( *t *\)



= *a*

the two vehicles yield or speed up to pass through the *i*\( *t *\) · 1 *t *, 

*t *= 1, 2, . . . , *N*

intersection. 

where, *u*\(·\) refers to normalization, 1 *vi * refers to the velocity change of *i* th vehicle during the time difference 1 *t*. 

**IV. EXPERIMENT AND COMPARISON**

A simulation platform based on Prescan and Matlab/Simulink *c: COMFORT*

has been built to evaluate the effectiveness and reliability of The longitudinal acceleration change |1 *a*| is mainly consid-the proposed model. 

ered to calculate the comfort revenue, the comfort revenue is set as:

A. SIMULATION AND VERIFICATION PLATFORM

\( *Ucomfort *= *u*\(1 *ai*\)

*i *= 1, 2 \(13\)

Prescan is a simulation environment for developing advanced 1 *ai *=| *ai*\( *t *\+1\)− *ai*\( *t*\)| , *t *=1, 2, . . . *N*

driver assistant systems \(ADAS\) and intelligent vehicle \(IV\) where:

systems. It is a platform that can be used to build 3D traffic *u*\(·\) refers to normalization. 1 *ai * refers to the acceleration change of

virtual scene, generate vehicles, pedestrians, traffic lights and *i* th vehicle during the time difference 1 *t*. 

Therefore, the comprehensive driving revenue is consisted other control modules. Prescan comes up with a powerful of safety revenue

graphics preprocessor, a high-end 3D visualization viewer, *Usafe*, efficiency revenue *Ueff * and comfort revenue

and a connection to standard MATLAB /Simulink. It is com-Ucom, which is defined as:

posed of various main modules, some of these main modules *U *= α *Usafe*\(1 *T *\) \+ β *Uefficence*\(1 *vi*\) \+ γ *Ucomfort * 1 *vi*\(1 *ai*\) represent a specific world and multiple sensors are simulated \(14\)

in the Sensor World. 

VOLUME 8, 2020

189551





X. Chen *et al. *: Conflict Decision Model Based on Game Theory for Intelligent Vehicles at Urban Unsignalized Intersections **FIGURE 6. **The cooperative decision-making process of IV and HD. 

**FIGURE 7. **\(b\) Inferred cooperation levels in Group A \(c\) Inferred cooperation levels in Group B. 

B. VERIFICATION OF INTERACTION BEHAVIORS

in Group A is higher to ensure they all can pass through the BETWEEN VEHICLES

intersection successfully and efficiently. 

In this section, driving data at real urban intersections To further verify the accuracy of the interaction model, \(Fig. 7\(a\)\) are collected to verify the effectiveness and reli-120 groups of crossing data at intersections are collected by a ability of the interaction model for vehicles. Two groups of subgrade camera to infer the cooperation levels between HD

driving data with successful crossing \(Group A\) and unsuc-and IV \(Fig. 8\). It can be seen the model can correctly classify cessful crossing \(Group B\) are respectively collected to infer most of the interaction behaviors with an accuracy of 91.6%. 

the cooperation levels between vehicles \(Fig. 7\(b-c\)\). The The results show that intelligent vehicles have the abilities results show that the cooperation levels between the vehicles to understand human behaviors, which provides theoretical 189552

VOLUME 8, 2020





X. Chen *et al. *: Conflict Decision Model Based on Game Theory for Intelligent Vehicles at Urban Unsignalized Intersections **TABLE 5. **Utility values of different driving strategies. 

**FIGURE 9. **Traffic scenario at urban intersections. 

**FIGURE 8. **Predicted results of interaction model for vehicles. 

*S* 1 and *S* 2 refer to the strategies taken by them respectively. 

support for the collaboration between human-driving and To simplify the decision-making model, the longitudinal intelligent vehicles. 

acceleration *a * is divided into 6 certain values \(e.g. *a *=

±1.5, ±1.0, ±0.5\}m/s2\) according to driving types \(conser-C. VERIFICATION OF DECISION-MAKING MODEL BASED

vative, ordinary, impulsive\). During the crossing process at ON GAME THEORY

the intersection, the two vehicles always select the driving The above experimental results show that the collabora-strategies that can maximize their utility values. Assuming tion between human-driving and intelligent vehicles can that the driving types of HD and IV are conservative- conser-be achieved at complex traffic conditions. In this section, vative, the utility values of HD and IV in 4 various driving a decision-making model based on game theory for intelligent strategy sets are shown in Table 5. The utility values of vehicles is established to improve traffic efficiency at urban optimal driving strategies at each timestep are marked as unsignalized intersections. 

bold data. During *t *= 1∼6s, the optimal strategies for HD

and IV are deceleration-acceleration. When *t *= 6s, they all 1\) SCENARIO SETTING

decelerate to ensure safety as IV reaches the conflict point The traffic scenarios have been built by Prescan, showed as earlier. After *t *= 8s, IV has passed through the conflict point, Fig. 9. And the initial conditions of the two vehicles are *X* 1 =

indicating that the conflicts among them have been resolved \( *L* 1, *v* 1, *a* 1\) = \(40, 12.5, 0\), *X* 2 = \( *L* 2, *v* 2, *a* 2\) = \(40, 12.5, 0\) and their optimal driving strategies turn into acceleration-respectively. The maximum velocity allowed at intersections acceleration, as shown in Fig. 10\(a\). 

should meet *v* max ≤ 15 m/s. Assuming that safety is the most Similarly, the optimal driving strategies of the two vehi-significant index in the crossing process, the weights α, β, γ

cles under other driving types are shown in Fig. 10\(b-f\). 

of the revenue function are select as 0.5, 0.3, 0.2, respectively *T* cross refers to the crossing time of vehicles, which defined in this article. 

as the moment when the last vehicle leaves the conflict point. The results show that IV can adjust its own driv-2\) THE RESULTS ANALYSIS IN CROSSING PROCESS

ing strategies based on the behaviors of HD and the cross-The crossing process can be represented as *G *= *S* 1, *S* 2; ing time *T* cross varies when they have different driving *U* 1, *U* 2, where, *U* 1 and *U* 2 refer to HD and IV respectively, types. 

VOLUME 8, 2020

189553





X. Chen *et al. *: Conflict Decision Model Based on Game Theory for Intelligent Vehicles at Urban Unsignalized Intersections **FIGURE 10. **The optimal driving strategies of the two vehicles under different driving types. 

**TABLE 6. **The results of the two decision-making models. 

is compared with it. The results show the position and velocity changes of the two vehicles to the conflict point \(Fig. 11\(a-b\)\). *T* pass refers to the moment that the first vehicle arrives at the conflict point and *T* cross is same defined as above. The results show that IV can adjust its own velocities to accelerate through the conflict point instead of waiting for HD passing firstly in the proposed model. Compared with the model based on conflict table, it can decrease *T* pass by 20 percent and *T* cross by 15 percent \(Table 6\), respectively, which can obviously improve the traffic efficiency at urban unsignalized intersections. 

**V. CONCLUSION AND FUTURE WORKS**

In order to help intelligent vehicles cross urban unsignalized intersections more safely and efficiently, this article proposed a decision-making model based on game theory for intelligent **FIGURE 11. **\(b\) The model based on conflict table. 

vehicles, which considers the complexity of traffic and interaction behaviors between vehicles at urban intersections. The 3\) THE RESULTS ANALYSIS WITH COMPARED MODEL

main conclusions are listed as follows:

To further verify the efficiency of the proposed model, the

\(1\) The interaction behaviors between vehicles in scenarios decision-making model based on the conflict table \[16\]

of intersection-crossing are studied and it provides theoretical 189554

VOLUME 8, 2020





X. Chen *et al. *: Conflict Decision Model Based on Game Theory for Intelligent Vehicles at Urban Unsignalized Intersections basis for the decision-making of intelligent vehicles at urban XUEMEI CHEN was born in Pingyi, Shandong, 

unsignalized intersections. The decision-making model based China, 1978. She received the B.E. degree in auto-on game theory and the optimal driving strategies under the mobile operation engineering from the Shandong University of Technology, Zibo, in 2000, and the Nash equilibrium are developed with the consideration of M.S. degree from the Beijing University of Tech-driving safety, efficiency and comfort. 

nology, Beijing, in 2003, and the Ph.D. degree

\(2\) By conducting a series of simulation experiments, from the Beijing Institute of Technology, Beijing, the reliability and effectiveness of the decision-making model in 2006. From 2006 to 2014, she has been an

Assistant Professor with the Mechanical Engineer-are verified. The results show the model can significantly ing Department, Beijing Institute of Technology. 

reduce the crossing time of vehicles at intersections. 

Since 2015, she has been an Associate Professor with the Mechanical Engi-The decision-making process of intelligent vehicles is neering Department, Beijing Institute of Technology. She is the author of influenced by many other factors. The impacts from pedes-three books and more than 50 articles. Her research interests include driver behavior model, autonomous vehicle decision-making, machine learning. 

trians, non-motor vehicles, road structure types and traffic She is a member of the China Automotive Engineering Society and Beijing flow density will be studied and discussed in future Institute of traffic engineering. She was a recipient of the Outstanding Talent work. 

of Beijing. She has presided over projects from the National Natural Science Foundation of China, China Ministry of Communications, and so on. She received the First Prize of Road Traffic Science and Technology, in 2014. 

**REFERENCES**

\[1\] A. Kurt, J. L. Yester, Y. Mochizuki, and U. Ozguner, ‘‘Hybrid-state YUFAN SUN received the B.E. degree in engi-driver/vehicle modelling, estimation and prediction,’’ in *Proc. 13th Int. *

neering from the Hefei University of Technol-IEEE Conf. Intell. Transp. Syst. , Sep. 2010, pp. 806–811. 

ogy, Hefei, in 2019. He is currently pursuing

\[2\] A. Zyner, S. Worrall, and E. Nebot, ‘‘A recurrent neural network solution the degree with the Beijing Institute of Technol-for predicting driver intention at unsignalized intersections,’’ *IEEE Robot. *

ogy. His research interests include driver behav-Autom. Lett. , vol. 3, no. 3, pp. 1759–1764, Jul. 2018. 

ior model, autonomous vehicle decision-making, 

\[3\] G. Xiong, Y. Li, S. Wang, X. Li, and P. Liu, ‘‘HMM and HSS based social machine learning, and so on. 

behavior of intelligent vehicles for freeway entrance ramp,’’ *Int. J. Control* *Autom. *, vol. 7, no. 10, pp. 79–90, Oct. 2014. 

\[4\] W. L. Song, G. M. Xiong, and S. Y. Wang, ‘‘Decision making for intelligent vehicles based on driver type analyzing in an intersection,’’ *Trans. Beijing* *Inst. Technol. *, vol. 36, no. 9, pp. 917–922, 2016. 

YANGJIAXIN OU was born in 1997. She received

\[5\] M. Wang, S. P. Hoogendoorn, W. Daamen, B. van Arem, and R. Happee, the bachelor’s degree in engineering from the

‘‘Game theoretic approach for predictive lane-changing and car-following Beijing Institute of Technology. She is currently control,’’ *Transp. Res. Part C, Emerg. Technol. *, vol. 58, pp. 73–92, pursuing the master’s degree with the Beijing Sep. 2015. 

Institute of Technology. Her research interests

\[6\] S. I. Bouderba and N. Moussa, ‘‘Evolutionary dilemma game for conflict include autonomous vehicle, decision-making, resolution at unsignalized traffic intersection,’’ *Int. J. Mod. Phys. C*, vol. 30, and simulation. 

Feb. 2019, Art. no. 1950018. 

\[7\] S. Pruekprasert, X. Zhang, J. Dubut, C. Huang, and M. Kishida, ‘‘Decision making for autonomous vehicles at unsignalized intersection in presence of malicious vehicles,’’ in *Proc. IEEE Intell. Transp. Syst. Conf. \(ITSC\)*, Oct. 2019, pp. 2299–2304. 

XUELONG ZHENG received the M.S. degree

\[8\] X.-M. Chen, M. Jin, Y.-S. Miao, and Q. Zhang, ‘‘Driving decision-making from the Beijing Institute of Technology, Beijing, analysis of car-following for autonomous vehicle under complex urban in 2017. He is currently pursuing the Ph.D. degree environment,’’ *J. Central South Univ. *, vol. 24, no. 6, pp. 1476–1482, in advanced manufacture with the Department of Jun. 2017. 

Mechanical Engineering. His research interests

\[9\] X.-M. Chen, Q. Zhang, Z.-H. Zhang, G.-M. Liu, J.-W. Gong, and include autonomous vehicle decision-making and C.-Y. Chan, ‘‘Research on intelligent merging decision-making of machine learning. 

unmanned vehicles based on reinforcement learning,’’ in *Proc. IEEE Intell. *

*Vehicles Symp. \(IV\)*, Jun. 2018, pp. 91–96. 

\[10\] J. L. Zhang, ‘‘Research on distributed optimization model and algorithm based on non-cooperative game,’’ Ph.D. dissertation, Dept. Elect., Zhejiang Univ., Hangzhou, China, 2014. 

ZIJIA WANG received the B.E. degree from

\[11\] X. F. Yang, S. Zhang, and Q. Fu, ‘‘Research of driving behavior under the Beijing University of Technology, Beijing, condition of complete information based on game theory,’’ *J. Highway* in 2018. He is currently pursuing the M.E. 

*Transp. Res. Develop. *, vol. 31, no. 7, pp. 105–111, 2015. 

degree with the Beijing Institute of Technol-

\[12\] C. H. Xu, F. Y. Lian, and M. X. Fu, ‘‘Research on the game problem of ogy, Beijing. His research interests include driver multi-intelligent agent decision Interaction,’’ *Comput. Sci. *, vol. 40, no. 7, behavior model, autonomous vehicle decision-pp. 196–200, 2013. 

making, machine learning, and so on. 

\[13\] Y. Gu, Y. Hashimoto, L.-T. Hsu, and S. Kamijo, ‘‘Motion planning based on learning models of pedestrian and driver behaviors,’’ in *Proc. IEEE 19th* *Int. Conf. Intell. Transp. Syst. \(ITSC\)*, Nov. 2016, pp. 808–813. 

\[14\] B. Wu, X. C. Zhu, and M. Z. Liao, ‘‘Safety boundary condition model MENGXI LI received the B.S. degree from the

based on vehicle intersection conflict and collision,’’ *J. Tianjin Normal* *Univ. *, vol. 39, no. 2, pp. 64–65, 2019. 

Hebei University of Technology. She is currently

\[15\] G. Rodrigues de Campos, P. Falcone, R. Hult, H. Wymeersch, and pursuing the B.S. degree with the Beijing Insti-J. Sjoberg, ‘‘Traffic coordination at road intersections: Autonomous tute of Technology. Her research interests include decision-making algorithms using model-based heuristics,’’ *IEEE Intell. *

unmanned vehicle perception and decision. 

*Transp. Syst. Mag. *, vol. 9, no. 1, pp. 8–21, Spring 2017. 

\[16\] G. Lu, L. Li, Y. Wang, R. Zhang, Z. Bao, and H. Chen, ‘‘A rule based control algorithm of connected vehicles in uncontrolled intersection,’’

in *Proc. 17th Int. IEEE Conf. Intell. Transp. Syst. \(ITSC\)*, Oct. 2014, pp. 115–120. 

VOLUME 8, 2020

189555



