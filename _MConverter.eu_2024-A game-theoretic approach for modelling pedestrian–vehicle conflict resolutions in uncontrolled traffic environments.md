Accident Analysis and Prevention 203 \(2024\) 107604

Contents lists available at ScienceDirect

Accident Analysis and Prevention

journal homepage: www.elsevier.com/locate/aap

A game-theoretic approach for modelling pedestrian–vehicle conflict resolutions in uncontrolled traffic environments

Roja Ezzati Amini a, ∗, Mohamed Abouelela a, Ashish Dhamaniya b, Bernhard Friedrich c, Constantinos Antoniou a

a *Chair of Transportation Systems Engineering, TUM School of Engineering and Design, Technical University of Munich, Arcisstrasse 21, 80333 Munich, Germany* b *SV National Institute of Technology, Civil Engineering Department, Surat 395007, Gujarat, India* c *Technische Universität Braunschweig, Hermann-Blenk-Str. 42, 38108 Braunschweig, Germany* A R T I C L E

I N F O

A B S T R A C T

*Keywords:*

The interactions of motorised vehicles with pedestrians have always been a concern in traffic safety. The major Conflict resolution strategy

threat to pedestrians comes from the high level of interactions imposed in uncontrolled traffic environments, Pedestrian–vehicle interactions

where road users have to compete over the right of way. In the absence of traffic management and control Game theory

systems in such traffic environments, road users have to negotiate the right of way while avoiding conflict. 

Uncontrolled traffic environments

Furthermore, the high level of movement freedom and agility of pedestrians, as one of the interactive parties, Traffic safety

can lead to exposing unpredictable behaviour on the road. Traffic interactions in uncontrolled mixed traffic environments will become more challenging by fully/partially automated driving systems’ deployment, where the intentions and decisions of interacting agents must be predicted/detected to avoid conflict and improve traffic safety and efficiency. This study aims to formulate a game-theoretic approach to model pedestrian interactions with passenger cars and light vehicles \(two-wheel and three-wheel vehicles\) in uncontrolled traffic settings. The proposed models employ the most influencing factors in the road user’s decision and choice of strategy to predict their movements and conflict resolution strategies in traffic interactions. The models are applied to two data sets of video recordings collected in a shared space in Hamburg and a mid-block crossing area in Surat, India, including the interactions of pedestrians with passenger cars and light vehicles, respectively. The models are calibrated using the identified conflicts between users and their conflict resolution strategies in the data sets. The proposed models indicate satisfactory performances considering the stochastic behaviour of road users – particularly in the mid-block crossing area in India – and have the potential to be used as a behavioural model for automated driving systems. 

**1. Introduction**

World Health Organisation, 2019\). Uncontrolled traffic environments can create a potential hazard for pedestrians since there are no traffic Every year, approximately 1.3 million people lose their lives as

management and control systems to conduct the traffic, and the road a result of a road traffic crash, and between 20–50 million people

priority is not predetermined. As a result, road users in such settings suffer non-fatal injuries \(World Health Organisation, 2019\). Among all, majorly rely on priority negotiation, and traffic movements implicate a vulnerable road users \(VRUs\) such as pedestrians, motorcyclists, and more frequent and complex interaction process among them. 

cyclists account for more than half of all road traffic fatalities \(World

During a traffic conflict – a traffic event involving the interaction

Health Organisation, 2019\). Crashes involving pedestrians occur most of users \(Parker and Zegeer, 1989\) – traffic participants intend to often in urban areas and while pedestrians cross the roadway at either dominate the road space they are moving towards while avoiding a

illegal locations out of crosswalks or pedestrian crossing facilities, collision. To fulfil these goals, road users perform various manoeuvres, as they include many conflict points between pedestrians and vehi-and a collision occurs if the performed manoeuvres fail to prevent

cles \(Lord et al. , 2007; NSC-Injury Facts, 2019\). Amongst pedestrian physical contact between the interacting users. Traffic collisions and crossing facilities, uncontrolled traffic environments are associated with a higher level of traffic collisions and pedestrians’ fatalities compared critical conflicts have severe impact on traffic safety and efficiency; to controlled settings \(Pfortmueller et al. , 2014; Lloyd et al., 2015; 

however, the majority of road users interact with no serious conflict

∗ Corresponding author. 

*E-mail address: *roja.ezzati@tum.de \(R. Ezzati Amini\). 

https://doi.org/10.1016/j.aap.2024.107604

Received 19 November 2023; Received in revised form 23 March 2024; Accepted 27 April 2024

Available online 10 May 2024

0001-4575/© 2024 The Authors. Published by Elsevier Ltd. This is an open access article under the CC BY-NC-ND license \(http://creativecommons.org/licenses/by-

nc-nd/4.0/\). 

*R. Ezzati Amini et al. *

*Accident Analysis and Prevention 203 \(2024\) 107604*

or collision and are not of interest from the traffic safety point of distance. In the field of user behaviour and traffic interactions, the view, but still crucial in terms of road user experience and traffic modelling approaches have been mostly focused on a limited number

efficiency \(Madigan et al., 2019; Golakiya et al. , 2019\). 

of influencing factors in users’ decision \(e.g., dynamic factors, traffic A safe and efficient traffic interaction demands road users to cor-characteristics\), without considering the decision-making process of rectly interpret and predict the strategies of their interactive party, road users collectively and various significant factors that may affect although this may become complex when heterogeneous users interact

the process \(Ezzati Amini et al. , 2021b\). Besides, the majority of col-on a crossing site. The heterogeneity of users \(vehicles vs. pedestri-lision/conflict prediction methods estimate the traffic safety outcomes ans\) may cause different decision-making processes and users to react based on unchanged trajectory and speed of road users. This assump-differently during the interaction process. Besides, light road users tion ignores various evasive manoeuvres that road users may employ to \(e.g., pedestrians, two-wheel vehicles\) can make a sudden change of avoid a conflict/collision on the road, and hence, restricts the model ca-direction or speed and, thus, are prone to perform more unpredictable pability in evaluation of traffic outcomes in such circumstances \(Amini

behaviour on the road. Therefore, a suitable modelling framework is

et al. , 2022\). Therefore, a thorough understanding of user behaviour is required to predict the trajectory and movement of traffic participants vital for building a suitable model for pedestrian–vehicle interactions. 

during a traffic conflict and consequently enhance safety and efficiency Further, developing a safe and efficient interaction concept is crucial on the road. 

for emerging technologies design, such as advanced driver assistance systems \(ADAS\) and ADS. With such automation and driver assistance

*Research contributions*

technologies, more and more driving tasks are handled automatically which leads to partial engagement of drivers in partially automated ve-The main objective of this research is to model pedestrian inter-

hicles, or complete absence of a human driver in fully automation cases. 

actions with different vehicle types during road crossing scenarios in As a result, traffic interactions among pedestrians and such road users uncontrolled traffic environments. Based in the reviewed literature \(i.e., automated driving systems\) undergo substantial changes, where \(Section 2\) that the applicability of the previously proposed models is such systems would require an accurate comprehension of human road

mostly restricted to specific types of road users \(i.e., passenger cars and users’ behaviour in traffic interactions to predict user behaviour and pedestrians\). This would ignore the variety of strategy choices available movement intentions, and react aptly \(Schneemann and Gohl, 2016\). 

for user types based on their speed limit and degree of movement free-However, similar to conventional traffic interactions, prediction of road dom \(e.g., deviation and deceleration strategy\), and thus a less efficient user behaviour is challenging, and a suitable modelling framework is prediction of their behaviour. Therefore, game-theoretic models are required to ensure the safety of pedestrians interacting with ADS and developed in this study for pedestrian interactions with passenger cars ensure the efficiency of these systems on the road. 

and light vehicles in different road designs. To better reflect the user The following subsections review some of previous research in

decision-making process, the utility functions of the proposed game traffic interactions and the developed modelling approaches. 

are formulated based upon three principle layers; \(1\) safety level to estimate the severity level and the collision probability of a conflict *2.1. Pedestrian–vehicle interactions*

event, \(2\) travel level associated with the detour, and deceleration imposed to interacting users by changing their speed and movement

Several studies investigate user behaviour and model pedestrian–

direction to escape a conflict and \(3\) social layer to describe the traffic vehicle interactions in unregulated settings at a microscopic level. For environment conditions influencing the user’s choice of strategy. The example, Pascucci et al. \(2018\) formulated a discrete choice model proposed interaction model predicts the conflict resolution strategies of to identify the conflict resolution strategies of users interacting on users in interaction and has the potential application as a behavioural the road. The authors defined a set of explanatory variables to build model of the automated driving systems \(ADS\). 

the model, i.e., the movement-specific parameters \(e.g., relative posi-The remainder of this paper is organised as follows: Section 2

tion, speed, acceleration\), collision-specific parameters \(e.g., time to provides an overview of the previous studies in the field. The detailed collision, the existence of leading car\), and the number of simulta-formulation of the game-theoretic model is described in Section 3. 

neous conflicts of users. In another approach, Pascucci et al. \(2015\) Section 4 includes the description of the study areas, as well as conflict utilised the future position of the interacting users and the time of detection and analysis strategies. Section 5 documents the application leaving the conflict zone as indicators to determine the crossing pri-of the game-theoretic approach to the analysed data. Section 6 presents ority. Both studies found that models effectively predict basic con-the model evaluation and estimation using the analysed data. Finally, flicts between pedestrians and cars but highlighted the necessity for Sections 7 and 8 present the discussions and conclusions, respectively. 

further research into more complex interactions involving multiple

road users. To explore more complex interactions, Schönauer \(2017\) **2. Literature review**

used a Stackelberg competition game to model road user behaviour

in conflicting situations, in which the probability of collision, agents’

During a traffic interaction, the characteristics’ discrepancy of dif-position and distance, and rule-based and social-based behaviour of ferent user types may lead to exposing various behaviour. For instance, users determine their conflict resolving strategies. The authors sug-a driver approaching a crossing may decelerate and let the pedestrian gested that factors such as traffic cultures \(e.g., different countries, cross the road first, while the pedestrian deviates to create a bigger gap different traffic regulations\), and traffic density \(e.g., group behaviour, with the car and, thus, escape a potential conflict. Previous studies have gap acceptance behaviour\) can significantly influence traffic behaviour investigated a broad range of factors that may influence user behaviour and should be taken into account in the future for the model’s transfer-on the road, such as pedestrian characteristics and walking speed, vehi-ability. In line with this, Johora and Müller \(2020\) combined the social cle’s approaching speed, and road characteristics \(Beggiato et al. , 2017; 

force model with the Stackelberg competition approach to model the

Sun et al. , 2003; Pawar and Patil, 2015\). Ezzati Amini et al. \(2019\)

road user interactions. In this approach, the interactions are classified argued that road users adopt a conflict resolution strategy by consid-into simple and complex. The proposed model covers various inter-

ering a wide range of factors knowingly \(e.g., the time/distance gap actions, including pedestrian–pedestrian, multiple pedestrian–vehicle, estimation\) and/or unknowingly \(e.g., user age or gender\) while they and vehicle–vehicle interactions. Besides, it employs factors such as employ different communication methods to ease the interaction when the number of active interactions, speed, and travelled distance to needed. Besides, various strategies that users can perform to avoid a capture the dynamics of these interactions accurately. Nasernejad et al. 

potential conflict on the road may result in different granted/expected

\(2021\) similarly employed agent-based framework to model pedes-utilities, e.g., gaining priority, saving time and shortening the traversed trian behaviour during near misses when interacting with vehicles. 

2

*R. Ezzati Amini et al. *

*Accident Analysis and Prevention 203 \(2024\) 107604*

Pedestrian–vehicle conflicts are represented using the Markov decision images and positions to determine pedestrian destinations and applies process framework, with a Gaussian process inverse reinforcement

trajectory planning toward these destinations. The output produces

learning \(GP-IRL\) method used to infer pedestrian collision avoidance a probability distribution map of possible destinations using Markov strategies. A deep reinforcement learning model is employed to esti-decision processes and the forward–backward algorithm. Experimen-

mate optimal pedestrian strategies during conflicts. The model predicts tal validation demonstrated the system’s accuracy in predicting both pedestrian trajectories, evasive manoeuvres, and post-encroachment

user destinations and trajectories. Expanding on pedestrian trajectory time, highlighting the importance of developing safety-focused ap-prediction, Jayaraman et al. \(2020\) developed a hybrid system model proaches for modelling user interactions in mixed traffic conditions. A incorporating pedestrian gap acceptance behaviour and interacting

study by Nasernejad et al. \(2023\) emphasised on the multi-agent nature user speeds. This model categorises pedestrian states as approaching of traffic interactions and formulated a Markov-Game framework to

a crosswalk, waiting, crossing, and walking away, aiming to capture model pedestrian–vehicle interactions and their collision avoidance belong-term \( *> * 5 s\) pedestrian crossing behaviour. The study showed haviour in mixed traffic environments. In this framework, agents were the model’s effectiveness in predicting long-term pedestrian crossing considered rational and interacted with each other simultaneously. The trajectories, particularly at crosswalks. However, real-world scenarios authors then contrasted this multi-agent model with a single-agent

involving multiple pedestrians pose challenges for ADS in distinguish-GP-IRL approach, aiming to learn and replicate pedestrians’ evasive ing between crossing and non-crossing individuals, suggesting the need manoeuvres assuming fixed trajectories for vehicles. The study findings for future model improvements. In a related vein, Fox et al. \(2018\) illustrated that multi-agent models outperformed single-agent models proposed a game-theoretic model for priority negotiation between au-in predicting collision avoidance strategies of road users. In a sim-tomated vehicles and other users \(e.g., a vehicle or pedestrian\) in ilar manner, multiple studies employed the Markov game to model

unsignalised intersections/crossings. This model assumes that agents’

pedestrian interactions with motorcyclists and compared the results optimal behaviour includes a non-zero probability of collision occur-with those obtained from a GP-IRL single-agent approach \(Lanzaro

rence, with yielding probability gradually increasing as interacting

et al. , 2022; Alsaleh and Sayed, 2021\), and a maximum entropy IRL

users get closer. The model assumption of the non-zero probability of algorithm \(Alsaleh and Sayed, 2020\). Once again, the multi-agent collision occurrence validates previous findings that ADS will make framework exhibited superior prediction accuracy compared to the

little or no progress if they are known to be perfectly safe and always single-agent model. 

yield to the interacting users. The authors suggest extending the model In summary, extensive research has explored user behaviour and

to incorporate further realistic details such as continuous speed to modelled pedestrian–vehicle interactions at a microscopic level. The reflect deceleration strategies of road users \(rather than discrete speed\), reviewed studies emphasise the significance of considering factors such traffic regulations, norms, and vehicle lateral positions to enhance its as traffic cultures, density, and multi-agent dynamics to enhance the applicability. 

transferability and accuracy of models. Overall, these findings un-

In summary, research in ADS has made significant progress in un-

derscore the importance of comprehensive modelling approaches in

derstanding pedestrian–vehicle interactions. However, challenges per-addressing the complexities of pedestrian–vehicle interactions across sist in real-world scenarios, such as accurately predicting pedestrians’

diverse traffic environments. 

intentions during traffic interactions and ensuring model transferability across diverse environments. Further research is needed to address

*2.2. Pedestrian-ADS interactions*

these challenges in order to improve ADS performance and enhance

road safety when automated vehicles become integrated into traffic

With respect to the ADS, and through the application of various

systems. 

methods, objects in motion \(e.g., vehicles, pedestrians, cyclists\) are tracked to predict their trajectories and future positions. The prediction **3. Conflict resolution model**

system, then, hypothesises multiple possible predictions of the future movement of dynamic objects. Several studies investigated the inter-Understanding and predicting road user behaviour is a complex

action of pedestrians with automated vehicles and proposed modelling modelling problem since it includes understanding and predicting of approaches to simulate the ADS interactions with VRUs \(Schneemann

surroundings, and interacting users’ current and future actions \(Fox

and Heinemann, 2016; Chen et al. , 2016; Møgelmose et al. , 2015\). 

et al. , 2018\). The latter issue may lead to paradox and incomputability In a research, Feng et al. \(2019\) used Cellular Automata to model issues as described in Gödel theorem and Halting problem \(Velupillai, interactions at mid-block crossings by considering a broad range of

2009\). Game theory provides a cooperative and competitive paradigm factors, such as the lane width and length, number of lanes, speed limit, to manage the self-referential decisions of players \(i.e., road users in vehicle size, and speed. The model employs the yielding regulations the game\) and describe pairwise traffic interactions \(Fox et al. , 2018\). 

at crossings in China and evaluates the lane-based post-encroachment The cooperative and competitive characteristics of game-theory-based time between a vehicle and pedestrian as a safety index. The results models align with real-world traffic interaction scenarios, where road showed that the proposed conflict elimination method effectively re-users employ conflict resolution strategies in response to the strategies duces conflicts between automated vehicles and pedestrians. However, of other users. This means that the gain or expected utility of users the authors noted a limitation in the model’s transferability, as it depends on the reactions of interacting users, while they strive to primarily focuses on pedestrian safety in China. In another study, Völz

maximise their own utilities \(Talebpour et al. , 2015; Ali et al. , 2019\). 

et al. \(2018\) combined motion tracking algorithms with data-driven These are similar to the real-world behaviour of road users in traffic methods to predict the crossing intention of pedestrians. The authors interactions, where, for instance, they compete over the road space argued that the correct prediction of pedestrian intentions at a crossing and try to avoid critical traffic conflicts. For this reason, a game-is essential to prevent unnecessarily slowing down traffic. For instance, theoretic approach is applied in this research to determine the user when an automated vehicle stops for a pedestrian with no intentions decisions interacting in uncontrolled traffic settings and predict the to cross the roadway. The proposed model considers the dynamic

conflict resolution strategies. The proposed game-theoretic approach distance measures of pedestrian and vehicle motion on approaching

focuses on pedestrian road crossing scenarios and highlights the active the crossing site to predict the next action. However, as stated by the nature of road users as players in traffic interactions. It takes into authors, this approach cannot ensure consistent performance across

account the collective decision-making process of interactive users and crosswalks with significantly different geometries. In the realm of determines the game outcome accordingly. 

pedestrian intention recognition and prediction, Rehder et al. \(2018\)

Depending on the user type, each player in the game \(referring to

introduced an Artificial Neural Network approach. This method utilises the interacting users in a conflict\) has specific degrees of permitted 3



*R. Ezzati Amini et al. *

*Accident Analysis and Prevention 203 \(2024\) 107604*

*3.2. Stackelberg game solution*

The game solution is determined by finding the sub-game perfect

Nash equilibrium \(SPNE\). A SPNE is a strategic outcome in game theory where each player’s chosen strategy maximises their payoff, accounting for current and future interactions. It ensures no player has an incentive to deviate from their strategy at any point. This stable solution captures optimal decision-making throughout the entire game, considering both immediate and long-term considerations. One prevalent method to find the SPNE is backward induction, i.e., the best responses of the follower \( *𝐵* follower\) must be computed first to allow the leader to maximise its payoff:

**Fig. 1. **Conflict resolution strategies of passenger cars \(left\) and pedestrians \(right\) in *𝐵* follower = *𝑚𝑎𝑥*\( *𝑠𝐹 *∈ *𝑆𝐹 *\) *𝑈 𝐹 *\( *𝑠𝐹 *| *𝑠𝐿*\) \(1\)

an interaction. 2W and 3W users have similar strategy sets as pedestrians. 

SPNE = ***𝒂𝒓𝒈𝒎𝒂𝒙**𝑠𝐿*∈ *𝑆𝐿 𝑈𝐿*\( *𝑠𝐿, 𝐵* follower\) \(2\)

movements that define their trajectories in the game. For instance, Where *𝑈 𝐿 * yields the leader’s maximum utility for selecting the best a large goods vehicle commonly moves straight without deviating

strategy from its choice of actions \( *𝑆𝐿, 𝑠𝐿 *∈ *𝑆𝐿*\). In the proposed game-from its forward trajectory \(in a safe driving situation\): while lighter theoretic approach, agents may receive different payoffs by playing user types, such as pedestrian, two-wheel \(2W\) and three-wheel \(3W\) the same strategies, as conflicting users are heterogeneous \(vehicle vs. 

vehicles, can swerve right or left due to their agile characteristics. 

pedestrian\) with distinct characteristics and objectives on the road. 

Further, users may apply speed changes/adjustments to avoid conflicts. 

Further, road users’ payoffs/strategies may vary depending on the

A combination of the trajectory and speed changes that users can

strategy choice of their interacting user. Therefore, Eqs. \(1\) & \(2\) employ to avoid a conflict is defined as the player’s strategy set in the can be transformed into the mixed strategy approach to finding the

game and clustered as:

optimal game solution. In this approach, the probability vectors of *𝑃 𝐿*\( *𝑠𝐿*\) and *𝑃 𝐹 *\( *𝑠𝐹 *| *𝑠𝐿*\) reflect the likelihood of performing a strategy

• **Continuing strategy **\( *𝑆𝐶𝑜𝑛𝑡*\): applicable for all user types and by the game leader and a strategy by the follower given the leader’s by moving along the free-flow trajectory \(FFT\) with preferred/

strategy, respectively. As proved by Nash \(1951\), one mixed strategy current speed, 

Nash Equilibrium exists in a game given the outcomes of:

• **Deceleration strategy **\( *𝑆𝐷𝑒𝑐*\): applicable for all user types, and *𝑃 *\( *𝑠𝐿, 𝑠𝐹 *\) = *𝑃 𝐿*\( *𝑠𝐿*\) ∗ *𝑃 𝐹 *\( *𝑠𝐹 *| *𝑠𝐿*\) \(3\)

by moving along the FFT with reduced speed, 

• **Deviation strategy **\( *𝑆𝐷𝑒𝑣*\): applicable only for light users \(i.e., pedestrians, 2W and 3W\), and by deviating to the left

*3.3. Formulation of utility functions*

\( *𝑆𝐷𝑒𝑣.𝑙𝑒𝑓𝑡*\) or right \( *𝑆𝐷𝑒𝑣.𝑟𝑖𝑔ℎ𝑡*\) from the FFT or collision point with preferred/current speed. 

Within the framework of the Stackelberg game, the study assumes

the rationality of players and their pursuit of utility maximisation

Fig. 1 demonstrates a schematic overview of the users’ trajectories when making strategic choices. The selection of strategies within the corresponding to the various available strategy choices defined per user game is expected to align with the objective of maximising utility, type. 

with a particular focus on minimising collision risk and energy loss while simultaneously maximising driving/crossing comfort. Road users’

utilities are defined based on an extensive literature review conducted *3.1. General structure of the Stackelberg game*

by Ezzati Amini et al. \(2019, 2021b\), which identifies influential parameters pertaining to road user behaviour during pedestrian–vehicle In a traffic interaction, the competition of road users over the right and pedestrian-ADS interactions. By integrating the utility formulation of way results in conflicting interests among them. Given the conflict-with the identified influential factors, this study strives to contribute ing interests among users, a strategic game of Stackelberg leadership to a comprehensive understanding of road user behaviour and its

competition is formulated to model pedestrian–vehicle interactions in implications within traffic interactions. 

uncontrolled traffic settings \(Ezzati Amini et al., 2021a\). The two-The study defines three layers to formulate the utility functions; 

player Stackelberg game assumes that one of the players is the leader safety layer, travel layer, and social layer, and explained in the follow-of the game and the other is the follower. In the game, the leader plays ing subsections. 

a strategy first, and then the follower reacts to the leader’s announced strategy. This approach highlights that in most traffic interactions, the *3.3.1. Safety layer*

decisions of road users are not made concurrently but more in the form The safety layer is defined to estimate the severity level and the

of action and reaction. Besides, the users employ a conflict resolution collision probability of conflict events regarding the performed conflict strategy with respect to the strategy of their interacting users, i.e., the resolution strategies. For instance, how safe a conflict outcome would gain/expected utility of the users depends on the interacting user’s be if a car continues its path and a pedestrian \(as its interacting user\) reaction. Fig. 2 illustrates a two-player Stackelberg game tree and deviates right to cross in front of the car. Whether the time/distance payoffs for taking each strategy pair in the game. One player performs gap would be long enough for the pedestrian to cross the road safely or the game leader \(L\) role with its available strategy choice \( *𝑠𝐿, *… *, 𝑠𝐿*\) ∈

1

*𝑛*

a critical condition/collision would occur. The conflict risk evaluation *𝑆𝐿 * and another player is the follower \(F\) with \( *𝑠𝐹 , *… *, 𝑠𝐹 *\) ∈ *𝑆𝐹 * as its 1

*𝑚*

model for pedestrian–vehicle interactions, developed by Amini et al. 

strategy set. Specifying one strategy *𝑠𝐿 * for the leader and one strategy *𝑛*

\(2022\), is embedded in the game to assess the severity of traffic *𝑠𝐹 * for the follower yields an outcome represented as a payoffs pair of conflict. The model emphasises how performing various evasive ma-𝑚

\( *𝑈 𝐿*\( *𝑠𝐿, 𝑠𝐹 *\) *, 𝑈 𝐹 *\( *𝑠𝐹 *| *𝑠𝐿*\)\), where *𝑈 𝐿 * is the utility that the leader receives noeuvres affects the users’ safety. The conflict risk evaluation models *𝑛*

*𝑚*

*𝑚*

*𝑛*

and *𝑈 𝐹 * is the utility of the follower. In this paper, payoff and utility are formulated using logit models and three surrogate safety measures, terms are used interchangeably. 

where the discrete choices of conflict and non-conflict are examined. A 4

*R. Ezzati Amini et al. *

*Accident Analysis and Prevention 203 \(2024\) 107604*

**Fig. 2. **Stackelberg game tree and sub-games. The payoffs of playing each strategy pair are shown in the terminal nodes. 

logit model assumes a linear relationship between predictor variables **Table 1**

\(e.g., *𝑥*

Parameter estimates of the logit models for pedestrian conflict events with passenger *𝑖*\) and the binary response variable *𝑌 * as:

cars and light vehicles \(Amini et al., 2022\). 

*𝑝*

𝓁 = *𝑙𝑜𝑔*

Parameter

Estimate

Std. Err. 

Z-value

Pr\( *> *|z|\)

*𝑏*

= *𝛴𝜃*

1 − *𝑝*

*𝑖𝑥𝑖*

\(4\)

Pedestrian–passenger car model

where 𝓁, *𝑏*, and *𝜃 * are the logit, logarithm base, and model parameters, Intercept

4.327

0.578

7.48

*< * 7 *𝑒*−14∗∗∗

respectively. Hence, the probability of the response variable *𝑌 *= 1

MD

−2.898

0.256

−11.31

*< * 2 *𝑒*−16∗∗∗

\(i.e., critical conflict\) with the predictor variables \(i.e., *𝑥𝑖*\) is: TMD

−3.067

0.304

−10.08

*< * 2 *𝑒*−16∗∗∗

1

CS

0.376

0.079

4.73

2 *. * 2 *𝑒*−06∗∗∗

*𝑝 *=

= *𝑆𝑏*\( *𝛴𝜃𝑖𝑥𝑖*\)

\(5\)

1 \+ *𝑏*−\( *𝛴𝜃*

Pedestrian–light vehicle model

*𝑖 𝑥𝑖 *\)

where *𝑆*

Intercept

4.490

0.373

12.03

*< * 2 *𝑒*−16∗∗∗

*𝑏 * is the sigmoid function with base *𝑏*, and *𝜃𝑖 * are estimated MD

−2.813

0.168

−16.69

*< * 2 *𝑒*−16∗∗∗

model parameters. The selected surrogate safety indicators employed TMD

−2.365

0.184

−12.80

*< * 2 *𝑒*−16∗∗∗

in the model are as follows:

CS

0.263

0.040

6.24

3 *. * 5 *𝑒*−11∗∗∗

**I. Minimum future relative distance \(MD\) **indicator evaluates the distance proximity of users after applying different strategy pairs. The MD compensates for the limitations of previously implemented mea-critical traffic conditions. The results indicate the average accuracy sures for collision risk prediction, assuming that users would collide of 92.4%, and sensitivity of 83.4%. for the pedestrian–passenger car if the condition remains unchanged. The MD indicator identifies new model, and average accuracy of 92.9% and sensitivity of 86.2% for

collision points or estimates the distance proximity of users when the the pedestrian–light vehicle model. Similar data sets as this study theoretical collision point changes or no longer exists \(e.g., in deviation are used to develop and validate conflict risk evaluation models for strategies\). 

the interaction of pedestrians with vehicles \(passenger cars\) and light **II. Time to minimum distance \(TMD\) **indicator estimates the avail-vehicles \(2Ws and 3Ws\) separately. Table 1 summarises the parameter able time gap between the arrival of the users to the MD or theoretical estimates for pedestrian–vehicle and pedestrian–light vehicle conflict collision point, if any. This time-based indicator is added to the conflict risk evaluation models. 

analysis to capture the simultaneous arrival of the users to the MD, The threshold of 0.425 is determined for the pedestrian–vehicle

i.e., the distance and time proximity of the users after performing model, and 0.512 for the pedestrian–light vehicle model through the p-conflict resolution strategies. The TMD estimation is based on the user’s tile method with the best performance. In the concept of game theory, if speed defined per strategy. 

the conflict risk exceeds the determined thresholds, the event is labelled as a critical conflict, and players receive \(−1\) as a penalty for playing **III. Conflicting speed \(CS\) **refers to the speed of heavier interacting the strategy pair. Conversely, for taking strategies with conflict risk road users when evasive manoeuvres are taken and at the moment of

lower than the thresholds, users receive \(0\) for the safety layer utility: minimum distance. The CS reflects the severity level of the conflict by

\{

taking into account the speed changes of users during an evasive action

−1 *, 𝑐𝑜𝑛𝑓 𝑙𝑖𝑐𝑡 𝑟𝑖𝑠𝑘 *⩾ *𝑡ℎ𝑟𝑒𝑠ℎ𝑜𝑙𝑑*

*𝑆𝑎𝑓 𝑒𝑡𝑦 𝑢𝑡𝑖𝑙𝑖𝑡𝑦 *=

\(6\)

\(e.g., deceleration strategy\). This is particularly important in traffic 0 *, 𝑐𝑜𝑛𝑓 𝑙𝑖𝑐𝑡 𝑟𝑖𝑠𝑘 < 𝑡ℎ𝑟𝑒𝑠ℎ𝑜𝑙𝑑*

situations where users \(usually motorised vehicles\) either come to a complete stop before/while reaching the MD threshold or roll over a *3.3.2. Travel layer*

small gap. Although the MD and TMD are below the thresholds in such This layer is associated with the detour \(DT\) and deceleration \(DC\) cases, the traffic condition is still considered safe. 

imposed on interacting users by changing their speed and movement

The model estimates these three safety measures for all possible

direction to escape a conflict. This class aims to quantify the comfort combinations of strategies available for user types to avoid a con-level of different strategies. Road users tend to reach their destinations flict and evaluates the safety of the outcomes. The model thresholds by taking the shortest path \(i.e., the FFT\) while maintaining their are determined by applying various methods \(i.e., intersection point, speed. Therefore, the extra traversed distance by players to reach their maximum between-class variance, p-tile, and minimum cross-entropy

destination return a detour dis-utility for users. For this purpose, the method\) to separate potential critical conflicts against normal traffic free-flow trajectory of users to reach the theoretical collision point –

conditions. Then, the F-score method is used to select the optimal

extracted through the conflict detection procedure \(see Section 4.2\) – is thresholds with the best performance \(van Rijsbergen, 1979\). Finally, compared with their traversed trajectory while deviating to the right or the overall performance of the models and their thresholds are as-left from the FFT. The deviation angles determined in Section 4.3.3 are sessed using two metrics: \(I\) accuracy reflecting the percentage of utilised to compute the new traversed distance in deviation strategies, correct predictions \(i.e., normal and critical traffic conditions\), and \(II\) and the corresponding dis-utility is returned for the additional distance sensitivity showing the percentage of the events correctly labelled as implied while performing deviation strategies. A similar approach is 5

*R. Ezzati Amini et al. *

*Accident Analysis and Prevention 203 \(2024\) 107604*

**Table 2**

Utility functions to compute payoffs of strategy pairs for player *𝑖 * as the game leader, and *𝑗 * as the follower. *𝑑𝑠𝑡𝑟 * refers to the traversed distance in each game strategy, and *𝑑𝐹 𝐹 𝑇*

to the distance of traversing the FFT \(see Section 4.2, Step 2\). 

Category

Metrics

Utility

Formula

Specification

MD \(m\)

Predicted conflict of the

Model thresholds:

Safety layer

TMD \(s\)

*𝑆𝐿*

estimated models in Table 1

pedestrian-car = 0.425

*𝑖𝑗*

CS \(m/s\)

for user type conflicts. 

pedestrian-light vehicle = 0.512

Detour \( *𝑑 *, *𝑑 *\)

*𝐷𝑇 , 𝐷𝑇*

exp\( *𝑑𝐹 𝐹 𝑇 *− *𝑑𝑆𝑡𝑟*\) − 1

*𝑑𝑆𝑡𝑟 > 𝑑𝐹 𝐹 𝑇*

Travel layer

*𝑖*

*𝑗*

*𝑖*

*𝑗*

*𝑖*

*𝑖*

*𝑖*

*𝑖*

Deceleration rate \( *𝑑𝑐 *, *𝑑𝑐 *\)

*𝐷𝐶 , 𝐷𝐶*

exp\( *𝑑𝑐 *\) − 1

*𝑖*

*𝑗*

*𝑖*

*𝑗*

*𝑖*

Pedestrian group size

*𝑃 𝐿 , 𝑃 𝐿*

\{−1 *, * 0 *, * 1\}

Group size *> * 2

*𝑖*

*𝑗*

Social layer

Pedestrian approaching lane

*𝐿𝑁 , 𝐿𝑁*

\{−1 *, * 0 *, * 1\}

Middle lane or kerbside

*𝑖*

*𝑗*

Right of way

*𝑅𝑊 , 𝑅𝑊*

\{0 *, * 1\}

Who gets priority? 

*𝑖*

*𝑗*

∑

Utility of playing strategy pair \( *𝑆𝐿, 𝑆𝐹 *\)

Leader: *𝑈 *\( *𝑆𝐿, 𝑆𝐹 *\) =

*𝑈 𝑡𝑖𝑙𝑖𝑡𝑖𝑒𝑠*

*𝐿*

∑

Follower: *𝑈 *\( *𝑆𝐹 *| *𝑆𝐿*\) =

*𝑈 𝑡𝑖𝑙𝑖𝑡𝑖𝑒𝑠*

*𝐹*

applied for users decelerating due to a conflict on the road. The average prefer to take strategies that return such utilities, and strategies such deceleration rate of user types is used to reflect the deceleration disas continuing always become dominant in the game, which contrasts

utility when users change their speed in reaction to a conflict on the with the real-world decision-making process of users in interactions. 

road. The average deceleration rate is extracted from the data sets and Regarding the right of way, the player who gets priority by taking a for each road user type and applied accordingly to estimate the utility strategy receives utility \(\+1\) and \(0\) otherwise. 

\(see Section 4.3.2\). The exponential functions scale the utility values

Table 2 summarises the utility computations in all layers of the between \(−1\) and \(0\) in the travel layer. 

game. 

*3.3.3. Social layer*

*3.3.4. Utility function*

This layer describes the traffic environment conditions that influ-

All attributes influencing the agents’ preferences to deliver the

ence the user’s choice of action. This class includes the influencing supra objects integrate into one utility function \(multi-attribute utility factors of pedestrian group size \(PL\), approaching lane \(LN\), and the function\), representing the overall agent’s utility. The final formulation right of way \(RW\). The parameter group size of pedestrians affects

of utilities for the leader strategy choice is calculated in the following road user behaviour in traffic interactions \(Sun et al., 2003; Sucha

way by considering a set of weights *𝜃 * for the parameters:

et al. , 2017; Malenje et al., 2018\). Larger groups enhance visibility *𝑈*

and perceived safety, leading to more assertive actions like crossing *𝐿*\( *𝑠𝐿, 𝑠𝐹 *\) = *𝜃𝑠𝑙 𝑆 𝐿𝑖𝑗 *\+ *𝜃𝑑𝑡𝐷𝑇𝑖 *\+ *𝜃𝑑𝑐 𝐷𝐶𝑖*

\(7\)

or merging. They also promote collective behaviour and conformity. 

\+ *𝜃𝑝𝑙𝑃 𝐿𝑖 *\+ *𝜃𝑙𝑛𝐿𝑁𝑖 *\+ *𝜃𝑟𝑤𝑅𝑊𝑖*

In contrast, smaller groups tend to be more cautious due to reduced visibility and vulnerability. Additionally, the group size can affect other **4. Data collection and conflict analysis**

road users’ behaviour, with larger groups attracting more attention and potentially altering driver behaviour. Similarly, the approaching lane Two video graphic surveys are used for conflict analysis and model

of traffic influences pedestrian–vehicle interactions on the road \(Fricker

application in this research. The data analysis relies on the users’ trajec-

and Zhang, 2019; Kadali and Vedagiri, 2020\). Factors such as visibility, tories and a set of explanatory variables extracted from the data sets. A crossing behaviour of pedestrians, driver awareness of pedestrians, conflict detection procedure is applied to identify the potential conflicts expectation of right of way are impacted depending on the approaching among road users and determine the conflict resolution strategies of lane. Therefore, understanding these dynamics is crucial in pedestrian–

interacting users. For each conflict event, the utilities of interacting vehicle interactions and parameters are included in the modelling

users are computed for all possible combinations of strategies \(with framework. 

respect to the user type\) that players could perform in the game, 

For pedestrian group size and approaching lane, the strategies are

including the real-world strategies in the data sets. 

evaluated with respect to the interacting user’s strategy, and based A similar approach is applied to compute the utility of the follower on the aggressiveness level: aggressive, neutral, and courteous. Players *𝑈𝐹 *\( *𝑠𝐹 *| *𝑠𝐿*\). 

receive \(−1\) as a penalty for performing aggressive strategies, \(0\) for neutral strategies, and \(\+1\) as an incentive for taking courteous ma-4.1. Video surveys

noeuvres. For instance, a car receives dis-utility of \(−1\) if it continues its path and does not yield to the interacting pedestrians who cross in Two video graphic surveys were used in this study to analyse road

a group greater than two persons. In the same scenario, the car gets user behaviour in uncontrolled traffic settings; \(1\) a mid-block crossing \(\+1\) as a utility if it decelerates, and pedestrians continuing to cross in Surat city, Gujarat, India \(Golakiya and Dhamaniya, 2018\), and \(2\) the road would receive \(0\). Similarly, users receive \(−1\), \(0\), or \(\+1\) a shared space in Hamburg city, Germany \(Pascucci et al. , 2021\). The for pedestrians approaching from the kerbside or the middle lane of interaction data from these locations were used to investigate road user the road, based on the performed manoeuvres. Factors of pedestrian

behaviour, conflict resolution strategies, and factors influencing their group size and approaching lane are added to the game utilities to

choice of actions during traffic conflicts. The selection of these locations also reflect the importance of the social norms in traffic conflicts, was based on the diverse road user types interacting with pedestrians i.e., whether social norms support a conflict resolution strategy. These \(e.g., passenger cars, light vehicles\), and dominance of said road user factors aid in weighting the high utility of saving energy in taking types in the areas with low interference in the interaction dynamic aggressive manoeuvres \(e.g., continuing strategy with high detour, and among them \(Pascucci, 2020\). The chosen study locations also priori-deceleration utilities\) and the energy loss in taking courteous strategies tised high-traffic volume areas to examine road user behaviour with in the presence of risky conditions \(e.g., deceleration strategy with low higher exposure to traffic interactions and safety critical circumstances detour, and deceleration utilities\). In the absence of the social norm \(pedestrian flow of 304 ped/h, 2W flow of 2393 veh/h, and 3W flow

utility, interacting users aim to maximise their individual utilities by of 1350 veh/h in mid-block crossing area, and vehicle flow of 600

minimising energy loss, e.g., traversing shorter distance \(Kemloh wag-

veh/h and pedestrian flow of 2200 ped/h in the shared space area\). 

oum et al. , 2012; Liao et al., 2017\). Consequently, users invariably Additionally, the selection of study locations considered road layouts 6





*R. Ezzati Amini et al. *

*Accident Analysis and Prevention 203 \(2024\) 107604*

**Fig. 3. **The street view of the mid-block crossing area from where the camera is placed \(right\) \(Golakiya and Dhamaniya, 2018\), and the aerial view of the site \(left\). 

**Fig. 4. **The street view of the shared space area from where the cameras are placed \(right\) \(Pascucci et al., 2021\), and the aerial view of the site \(left\). 

with longitudinal vehicular traffic movement facilitating pedestrian *4.1.2. Shared space interactions*

crossings from one side to the other, as well as the number of lanes and The second video graphic survey is collected through video record-roadway width during the selection process. These significant propering for a shared space zone in the district of Bergedorf \(Weidebaum-ties assisted in developing a more suitable modelling framework which sweg\), Hamburg city, Germany \(Pascucci et al., 2021\). The length of the is capable of predicting road user behaviour during traffic interactions shared space area is 63 m and is in the proximity of a shopping mall and and is not limited by culture-, traffic layout- and user types-specific retail stores. Two cameras were placed at an elevation of approximately 7 m and in opposite directions of traffic to perform the video survey characteristics of the case studies \(Amini, 2022\). 

\(Fig. 4\). The video was recorded on Saturday, April 2, 2016, from It is important to mention that this study utilises pre-processed

13:30 to 16:30. A 30-min of the recorded data \(period between 1:50

video data obtained from different sources \(Golakiya and Dhamaniya, 

and 2:20 p.m.\) is selected for conducting detailed analysis of road user

2018; Pascucci, 2020\), which introduces the possibility of biases stem-behaviour since during this time, the pedestrian volume was found to ming from variations in the pre-processing methods employed. There-be the highest among all video material. The software Tracker is used fore, it is crucial to interpret the results within the context of these to pre-process the data \(Douglas, 2017; Pascucci, 2020\). The extracted limitations. 

data includes the trajectory data in terms of coordinates every 0.5 s, velocity, and acceleration for passenger cars, pedestrians, and cyclists. 

However, cyclists are out of this research interest and neglected in the *4.1.1. Mid-block crossing interactions*

analysis. In the shared space, vehicles have priority over other road The first video graphic survey is collected in a mid-block crossing users, and pedestrians should use the given/available gap when it is area in Surat city, Gujarat, India, where traffic drive on the left \(Go-

long enough to traverse the crossing. 

lakiya and Dhamaniya, 2018\). The crossing is located on a six-lane It is worth noting that there is no real-world collision between

arterial urban road with an additional Bus Rapid Transit lane and in the traffic participants in the studied data; however, a conflict detection vicinity of businesses, stores, and hospitals. Two lanes of the road in the procedure was applied to identify traffic conflicts and evasive actions mid-block crossing area are selected for the video observation and data of interacting road users. 

analysis \(Fig. 3\). The video survey is performed by placing a camera on a building at an elevation of 15 m. On January 3rd, 2017, a survey was *4.2. Conflict detection strategies*

conducted from 09:00 until 19:00. Within this time frame, a specific 30-Uncontrolled traffic environments entail a constant interaction

min period from 09:30 to 10:00 was selected, during which the overall among road users. In such traffic events, at least one of the interacting traffic flow, including both pedestrians and vehicles, was observed to users would need to take an evasive manoeuvre to avoid the conflict; be at its highest. The data is pre-processed by overlaying a grid of size otherwise, a collision would occur. For this reason, a four-step conflict 40 × 8 *. * 85 m2 over the captured video using the Ulead VideoStudio 11

detection procedure is designed to identify the users in conflict. The software \(Golakiya and Dhamaniya, 2018\). The Avidemux 2.6 software data analysis was performed using R programming language. Coding

is used for tracking the video by 0.48 s time steps \(12 video frames\). A consistency was ensured through a stepwise approach, starting with

variety of traffic modes pass through the road, leading to more complex a small sample size and iteratively applying it to the entire data

traffic interactions in the mid-block crossing area. The extracted data set. Trajectory data of interacting road users were compared with

contains the trajectory of passenger cars, heavy goods vehicles \(HGVs\), time/speed data, and results were reviewed twice to confirm alignment large goods vehicles \(LGVs\), 2Ws, 3Ws, and pedestrians. 

between identified conflicts and road user data. 

7

*R. Ezzati Amini et al. *

*Accident Analysis and Prevention 203 \(2024\) 107604*

**Table 3**

Summary of the identified conflict events with pedestrians in the studied areas \(Amini

et al. , 2022\). 

Location

Car

2W

3W

HGV/LGV

Total

Shared space area

120

NA

NA

NA

120

Mid-block crossing

11

92

51

4

158

format \(GIF\) files were generated to verify the identified strategies by displaying the decision points of users \(i.e., to spot where/when users change their speed\) and their animated movements. For simplification, the combination of the strategies and performing multiple strategies **Fig. 5. **A simplified example of the conflict detection procedure in a pedestrian–

were neglected in the analysis, and the last actions were considered passenger car interaction. 

the users’ conflict resolution strategies. The identified strategies are clustered as described in Section 3 for each user type. It is worth noting that deviation strategies are only defined for light road users \(i.e., 2w, **Step 1. Data simplification**: A street boundary is specified to keep the 3w, and pedestrians\), due to:

trajectories of pedestrians who cross the roadway and remove

the rest walking along the road. The conflict analysis also ex-

• The higher degree of movement freedom for such user types and

cludes vehicles that exit the road before reaching the mid-block

consequently a wider range of available strategy choices on the

crossing \(in the mid-block crossing data set\) and vehicles being

road, 

parked or pulling-in along the road \(in both data sets\). Then, 

• The analysed interaction data in the studied location where de-

data are divided into 60-s time intervals to reduce the number

viation strategies are commonly employed by light users and

of events and simplify the analysis. 

heavier road users \(e.g., passenger cars\) move along their forward

**Step 2. Free flow trajectories \(FFTs\)**: The FFTs of road users are trajectories, and

plotted by connecting the shortest path from their origin to their

• The road layouts in the sites with longitudinal movement of ve-

destination. The FFTs are employed since traffic participants

hicular traffic along two lanes, and pedestrians crossing the road

tend to take the shortest path to reach their destination without

from one side to the other. Accordingly, road users’ movements

a traffic event and evasive manoeuvre. 

were based on the lane width, traffic directions, and the layout of **Step 3. Intersection points**: A theoretical collision point \(TCP\) is the road and conflict zone: deviation trajectories were limited to

defined to identify the intersected trajectories of users if they had the lighter road user type, and heavier user types only deviated

taken the FFTs to reach their destinations \(Fig. 5\). In addition, to exit the road or park/stop along the road. 

a buffer zone is considered for all vehicle types to improve the

Fig. 6 shows the strategy of users in conflict determined through accuracy of the collision points. The buffer zone assumption

the conflict resolution determination procedure for both data sets. The implies the real-world collision events in which vehicles hit the

following subsections explain the preferred speed, deceleration rates, pedestrians at the buffer, than/before the TCPs. 

and deviation angles specified for strategies per user type. 

**Step 4. Time to collision \(TTC\)**: For identified TCPs, a minimum relative TTC of 3 s \(Sayed and Zein, 1999\) is assumed to capture *4.3.1. Determination of the preferred speed*

the simultaneous arrival of the vehicle and pedestrian at the

For continuation and deviation strategies, the users’ preferred speed TCP and users’ buffers \(near- or far-buffer, depending on the

for crossing the road is extracted from the data sets for each user type. 

approaching direction\). TTC is calculated based on the average

Since there are significant differences regarding user behaviour and speed for each user. The Minimum TTC was computed as:

infrastructure designs in the studied locations, the preferred speed of

| *𝑇 𝑇 𝐶*

|

user types is estimated separately. 

*𝑣𝑒ℎ𝑖𝑐𝑙𝑒 *− *𝑇 𝑇 𝐶𝑝𝑒𝑑𝑒𝑠𝑡𝑟𝑖𝑎𝑛*

⩽ 3 s

\(8\)

A k-mean clustering approach is used to compute the preferred

The position of interacting users and their direction of move-

crossing speed of pedestrians in the shared space data set. Initially, ment/approach concerning the other involved user are taken into

non-conflict pedestrians – who are not involved in any conflicts/

account during the procedure. The application of the conflict detection interactions – are grouped based on the approaching direction. Then, procedure to the collected data led to identifying 120 conflict events different crossing phases are defined for pedestrians on approaching between pairs in the shared space data set and 158 events in the mid-a crosswalk \(Gorrini et al., 2016\), or while avoiding a conflict on the block crossing, where evasive manoeuvres were performed by one/both road \(Pascucci, 2020\). Based on non-conflict trajectories of pedestrians interacting users to escape the potential collisions \(Table 3\). Some in the shared space data, the crossing is divided into three movement users had more than one theoretical conflict \(i.e., involved in multiple phases: \(I\) pedestrian decelerates on approaching the crossing/road conflicts\) and were analysed independently. In the shared space area, kerb while evaluating the available gap to cross the road, \(II\) after the group of pedestrians at the crossing – interacted with the same accepting the gap, pedestrian accelerates to reach the crossing speed, vehicles – were analysed separately. The presence of other road users and \(III\) pedestrian crosses the road with roughly constant speed, 

in the interaction scene, regardless of playing their independent games, which is assumed to be the preferred crossing speed. These stages

is reflected in pay-off functions, such as pedestrians walking in a group are displayed in Fig. 7, where the acceleration changes of pedestrians or approaching from the opposite lane. However, the collected data in reflect the movement phases. It is worth noting that few samples with the mid-block crossing did not allow the independent analysis of the constant crossing speeds greater than 2.5 m/s are removed from the

pedestrians crossing in a group, and they were analysed as a group. 

analysis. Finally, a k-means algorithm is applied on variables walking speed, acceleration, and corresponding crossing time \(i.e., speed and ac-4.3. Conflict resolution determination

celeration at each time step of crossing\) of pedestrians as below \(Lloyd, 

1982\):

The conflict resolution strategies of users are determined manually and according to their FFTs, observed trajectories and speed profile

• Determination of the number of clusters \(k\): The Elbow method

during the interaction process. Additionally, the graphics interchange is used to determine the optimal number of clusters \(k = 3\). 

8



*R. Ezzati Amini et al. *

*Accident Analysis and Prevention 203 \(2024\) 107604*

**Fig. 6. **Conflict resolution strategy of users plotted by their position at the reaction time. From left to right: the first two figures show the vehicular traffic and pedestrians’

strategies on approaching the mid-block crossing area, the second two figures show the vehicular traffic and pedestrians’ strategies in the shared space. 

**Fig. 7. **Non-conflict trajectories of pedestrians in crossing the road in the shared space data set. 

**Table 4**

**Table 5**

K-Means clustering results of preferred crossing speed of pedestrians in the shared space. 

The preferred speed of vehicle types in the studied areas. 

Cluster

Variables

Size

Silhouette

Vehicle type

Speed limit

Mean speed

Std. dev. 

85th percentile

Speed

Acceleration

Time

width

*Vehicles in the shared space*

1

1.184

−0.009

3.49

4023

0.65

Passenger car

5.5

2.64

1.91

**4.7**

2

1.270

0.039

9.91

4294

0.52

*Vehicles in the mid-block crossing*

3

**1.312**

0.006

17.84

3971

0.52

Passenger car

16

7.83

2.43

**10.41**

*𝐵𝑒𝑡𝑤𝑒𝑒𝑛 𝑆*∕ *𝑡𝑜𝑡𝑎𝑙 𝑆 *= 86 *. * 6%

*𝑆*

*𝑆*

2W

14

8.76

4.27

**9.51**

3W

10

7.61

2.32

**8.75**

LGV&HGV

11

8.43

1.67

**10.41**

Pedestrian

–

0.81

0.66

**1.04**

• Centroid initialisation: The traditional random points method is

Speed unit: m/s. 

used to initialise centroids for clustering. 

• Assigning points to the closest cluster centroid: Based on the

distance from the centroid, data points are assigned to different

clusters. 

Although India is not a signatory of the Vienna Convention, driver

• Re-computation of centroids: The process is repeated until the

behaviour to adjust the speed assumes to be similar. The preferred

centroids of clusters remain unchanged \(100 iteration\). 

speed is applied in the continuing strategy of all vehicle types, and deviation strategy of light vehicles. The 85th percentile of the speed is

Table 4 summarises the details of the K-means clustering applica-also assumed to determine the preferred crossing speed of pedestrians tion, as well as the Silhouette coefficients for validation of consistency at the mid-block crossing, given that a small number of the user free within data clusters. The mean pedestrian walking speed in cluster 3

flow crossing is available from the data set \(Table 5\). This is due \(1.31 m/s\) – corresponding to the third movement phase of crossing –

to the high level of interactions and the traffic density at the mid-is selected as the preferred crossing speed of pedestrians for continuing block crossing, where pedestrians predominantly cross the roadway

and deviation strategies in the shared space. 

after escaping a conflict with the vehicles \(based on the applied conflict In preference to the speed limit, the 85th percentile of the speed

detection procedure in this study\). 

for the vehicle type in the data set is considered as the preferred speed For all user types, when the user speed at the reaction moment is

\(Table 5\). Vehicles commonly tend to drive at or near the same speed as higher than the preferred speed, the current speed is considered the traffic around, regardless of the speed limit. This is in accordance with strategy speed \(in continuing and deviation strategies\). 

the Vienna Convention speed adjustment rules, where drivers need to pay constant regard to the circumstances, such as the state of the road, *4.3.2. Determination of deceleration rate*

the weather conditions, and the density of traffic, to be able to stop the Determination of the deceleration rate of user types for the corre-vehicle timely if needed \(Vienna convention on Road Traffic, 1968\). 

sponding strategy \(i.e., deceleration strategy\) is not straightforward. 

9





*R. Ezzati Amini et al. *

*Accident Analysis and Prevention 203 \(2024\) 107604*

**Fig. 8. **A general framework of the game-theoretic model application. 

The reason is that the deceleration rate depends on several factors, e.g., the user’s initial speed, available time/distance gap to clear the conflict zone, and the presence of other road users. As a consequence, it is difficult to estimate an explicit deceleration rate that reflects the general behaviour of users decelerating in reaction to a conflict on the road. Nevertheless, the average deceleration rate of user types in both data sets is used to predict the deceleration strategy in the model. 

*4.3.3. Determination of deviation angle*

The average deviation angle of users deviated from their forward

trajectories – and consequently from the TCP – is regarded as the

deviation angle of user type for the associated strategies \(i.e., deviation right and deviation left strategies\). As the degree of movement freedom can vary from one road design to another, the deviation angles of

users are estimated independently for the shared space and mid-block crossing. In the shared space, the average deviation angle of pedestrians is 22.28 degrees, with a standard deviation of 9 *. * 15◦. For simplification reasons, the deviation angle of the pedestrians is assumed as 22 degrees in the model. In the mid-block crossing, pedestrians and light vehicles **Fig. 9. **An illustrative example shows a pedestrian and a car performing continuing-

\(2Ws and 3Ws\) deviate with the average angle of 26 *. * 5◦ \(rounded as 26◦

deceleration and right deviation-continuing strategies. It features initial and strategy in the model\) with a standard deviation of 9 *. * 35◦, and 11 *. * 11◦ \(rounded speeds \( *𝑣*\) and positions. Two alternative strategy combinations are demonstrated for as 11◦ in the model\) with a standard deviation of 6 *. * 85◦, respectively. 

users’ conflict avoidance without depicting body size \(Amini, 2022\). 

Other vehicle types in the data sets have no deviation strategy in their choice of actions. 

The R \(R Core Team, 2024\) programming language is used for **5. Application of the Stackelberg game**

detecting conflict events, the utility computation, and finding the game solution. Algorithm 1 \(see Appendix\) presents the employed approach This

section

discusses

the

application

of

the

developed

for probability computation of performing a strategy by a user in con-game-theoretic model to conflict events. A general framework of the flict. The computation is based on the user role \(leader or follower\) and game-theoretic model application is depicted in Fig. 8. As shown in the interacting user choice of action. The probability of the outcomes the figure, the initial step to apply the model is detecting a conflict. 

is, then, determined through Eq. \(3\) for each strategy combination In this work, a conflict detection procedure is applied to the collected in the game. The highest probability returns the game solution and, data to identify the users in conflict \(see Section 4.2 for details\). 

therefore, the user’s choice of actions to avoid the conflict. In the model However, for the general application of the model, the perpendicular application, all users in conflict are assumed to once be the leader and users’ trajectories would be replaced with the proposed FFTs to identify once the follower of the game. 

the theoretical collision point and the conflict event, if any. After identifying the conflict events, the interacting users’ position and speed **6. Model results**

at the moment of conflict detection, and the TCP coordinates are used to compute the game utilities \(see Fig. 9 for illustration of possible *6.1. Estimating the game-theoretic models*

user’s strategy combinations during interactions\). Users receive utility for each strategy combination in the game, i.e., the leader and fol-A likelihood approach is employed to estimate the parameter values

lower strategy combination determined from their available choice of \( *𝜃𝑖*\) of the Stackelberg game. The utility of strategy choice \( *𝑠 *∈ *𝑆*\) for actions. The game outcome, then, is determined through the backward players in the game is computed based on Eq. \(7\) for the game leader induction method as discussed in Section 3.2. 

and a similar approach for the follower. The probability of strategy 10

*R. Ezzati Amini et al. *

*Accident Analysis and Prevention 203 \(2024\) 107604*

**Table 6**

Parameter values and their standard deviation for model estimations in the shared space and mid-block crossing data sets. LB and UB: Lower and upper bound of confidence intervals. *𝐴𝑙𝑝ℎ𝑎 *= 0 *. * 05. 

Parameter

Shared space

Mid-block crossing

*𝜇*

*𝜎̄*

LB

UB

t-value

p-value

*𝜇*

*𝜎*

LB

UB

t-value

p-value

*𝑖*

*̄𝑖*

*𝜃*

1.42

0.20

1.02

1.81

6.97

<.0001

1.77

0.16

1.45

2.09

10.98

<.0001

*𝑠𝑙*

*𝜃*

1.99

0.28

1.45

2.54

7.20

<.0001

1.48

0.12

1.25

1.71

12.49

<.0001

*𝑑𝑡*

*𝜃*

1.13

0.54

0.07

2.18

2.09

<.01

3.36

0.26

2.85

3.87

12.89

<.0001

*𝑑𝑐*

*𝜃*

1.17

0.14

0.88

1.45

8.13

<.0001

1.29

0.20

0.89

1.69

6.37

<.0001

*𝑝𝑙*

*𝜃*

1.05

0.11

0.84

1.26

9.79

<.0001

0.80

0.10

0.61

1.00

8.05

<.0001

*𝑙𝑛*

*𝜃*

0.88

0.13

0.62

1.14

6.54

<.0001

0.80

0.11

0.59

1.01

7.44

<.0001

*𝑟𝑤*

**Table 7**

Leadership

determination

methods

for

the

pedestrian–passenger

car

and

the

pedestrian–light vehicle models. 

Selection criteria

Negative log-likelihood

Shared space

Mid-block crossing

Time to TCP

976.4

1335.0

User type

985.8

**1280.2**

Reaction time

**826.6**

1352.2

choice for players can be obtained through the sub-game probability for the follower and choice probability for the leader of the game, providing the overall probability of the strategy pairs as:

*𝑃 *\( *𝑠𝐿, 𝑠𝐹 *\) = *𝑃𝐿*\( *𝑠𝐿*\) ∗ *𝑃𝐹 *\( *𝑠𝐹 *| *𝑠𝐿*\) \(9\)

Therefore, the log-likelihood function is applied for the model estimation:

∑ ∑

**Fig. 10. **Flowchart of the optimisation process. 

*𝐿𝐿*\( *𝜃*| *𝑦𝑖𝑛*\) =

*𝑦𝑖𝑛 * log \( *𝑃 *\( *𝑠𝐿, 𝑠𝐹 *\)\)

\(10\)

*𝑖*

*𝑗*

where *𝑦𝑖𝑛 * is, 1 when the strategy pair is selected by the players in the

• **Time to TCP: **The player closer to the TCP \(in terms of time\) is game, and otherwise 0. Then, the negative log-likelihood is minimised the game leader, while the other interacting player is the follower. 

using the numerical optimisation algorithm for a quasi-Newton method

• **User type: **The type of users interacting on the road defines the of Broyden Fletcher Goldfarb Shanno \(BFGS\) \(Coppola et al., 2014\) in leadership; motorised versus non-motorised road users. In case of

R programming language. Fig. 10 depicts the optimisation flowchart employed for the estimation of parameter values in the model. Since pedestrian interaction with motorised vehicles, pedestrian is the

data sets have substantial differences in terms of user behaviour and follower and motorised vehicle is the game leader. 

infrastructure design, the model estimations are applied separately to

• **Reaction time: **The user who reacts first to a stimulus \(i.e., con-the shared space for pedestrian–passenger car conflicts and the mid-flict\) on the road is considered the game leader, and its interacting block crossing for the pedestrian–light vehicle conflicts. Few passenger user is the follower. In this research, users’ reaction time is

cars, HGVs, and LGVs in the mid-block crossing are not considered

recorded based on their speed and trajectory changes during

in the estimation to improve the model’s accuracy involving light

the conflict resolution determination procedure and utilises to

vehicles. This is mainly to develop a model that predicts the conflict determine the game leader. 

resolution strategies of users with respect to their type. In order to have different data sets for model estimation and validation, a hold-out A likelihood approach is employed to select the best leadership

method is applied to split the conflict events on both data sets into 70%

determination method \(similar to the utilised method by Schönauer

for training and 30% for testing purposes. The model estimations are

\(2017\)\), and the results are shown in Table 7. The likelihood results applied to the training samples, and different parameters’ combinations in the pedestrian–passenger car model and the shared space data set are examined to obtain the optimal training results \(i.e., highest sen-reveal that reaction time is a better method for leadership determina-sitivity, specificity, and accuracy\). In both models, the combination of tion. This supports the logic behind the Stackelberg leadership game, all proposed parameters provides the highest performance, and thus all where the leader of the game plays a strategy first, and the follower utilised in the models’ estimation. Table 6 summarises the estimated reacts to the leader’s strategy. Regarding the pedestrian–light vehicle parameters \( *𝜃𝑖*\) in both models using the calibration data acquired model in the mid-block crossing, the likelihood method yields slightly at the shared space and mid-blocking data sets. The mean values \( *𝜇*\) similar results for the time to TCP and reaction time methods; however, are returned by the maximum likelihood method, and the standard

as expected, the user type is the best fit to define the game leadership. 

error of the mean \( *𝜎̄𝑖*\) and confidence intervals for parameter estimates are computed through the observed Fisher information. The t-statistic *6.3. Model performance and validation*

and the *𝑝*-value are used to assess the significance of the estimated parameters. As summarised in Table 6 all the employed parameters The testing data sets are used to assess the overall performance of are statistically significant for the prediction of game outcomes in the the developed models. For this reason, confusion tables are created for models. 

categories: game choice \(as ‘‘success’’\) and non-choice \(as ‘‘failure’’\), *6.2. Game leadership estimation*

denoting the counts by true positive \(TP\), false positive \(FP\), true negative \(TN\), and false negative \(FN\). The accuracy, sensitivity, and As mentioned earlier in Section 5, the models are applied by switch-specificity across all classes are computed for both models. The results ing the leadership role among the users in conflict. To better determine are summarised in Tables 8 & 9. The model sensitivity and specificity the game leadership in the model, different approaches are evaluated: are used as metrics to evaluate the model’s ability to predict TPs and 11





*R. Ezzati Amini et al. *

*Accident Analysis and Prevention 203 \(2024\) 107604*

**Fig. 11. **Probabilities of strategy choices in a pedestrian–passenger car conflict. From left: probability of strategy choices for pedestrian as the game leader, for car as the follower, and the probability of game outcomes for strategy combinations \( *𝑃 *\( *𝑠𝐿, 𝑠𝐹 *\)\). 

**Fig. 12. **Probabilities of strategy choices in a pedestrian-2W conflict. From left: probability of strategy choices for 2W as the game leader, for pedestrian as the follower, and the probability of game outcomes for strategy combinations \( *𝑃 *\( *𝑠𝐿, 𝑠𝐹 *\)\). 

**Table 8**

**Table 9**

Confusion table for pedestrian–passenger car model. 

Confusion table for pedestrian-light vehicle model. 

True value

Total

True value

Total

Choice

Non-choice

Choice

Non-choice

Predicted: choice

60

12

72

Predicted: choice

54

28

82

Predicted: non-choice

12

492

504

Predicted: non-choice

28

1202

1230

*𝐴𝐶𝐶 *= 0 *. * 958

*𝐴𝐶𝐶 *= 0 *. * 957

TNs of each conflict event, respectively. The pedestrian–passenger car game. The application of time frames aims to demonstrate the model

model in the shared data set shows an average accuracy of 95.8%, a

performance concerning the variation in the game. The first example sensitivity of 83.3%, and specificity of 97.6% \(see Table 8\). The accu-is a pedestrian–passenger car conflict in the shared space where the racy of the pedestrian–light vehicle model is 95.7%, with a sensitivity of pedestrian is the game leader, and the passenger car is the follower 65.8% and specificity of 97.7% \(see Table 9\). The pedestrian–passenger

\(Fig. 11\). In the real-world scenario, the pedestrian continues its path, car model with a misclassification rate of 16.7% shows a good per-and the passenger car decelerates to let the pedestrian pass first. The formance reflecting the user decision-making process in the shared

probability of strategy choice in Fig. 11 shows that the deviation space. Regarding the mid-block crossing model, the misclassification strategy to cross behind the passenger car initially returns a higher rate amounts to 34.2% for the pedestrian–light vehicle model. This

utility \(time frame = −2\); however, the probability of the continuing performance considers satisfactory given the user behaviour in the

strategy increases over the time and remains the preferred strategy studied location and the wide range of factors influencing the user of the leader. The strategy choice probability for the passenger car in decisions, such as high traffic volume, road design, traffic behaviour, 

Fig. 11 demonstrates the highest utility in taking the deceleration strat-vehicle size, and driving culture. The methodology used shows that

egy during the illustrated period. The high utility of the deceleration the models can be applied in different traffic setups \(e.g., mid-block strategy is mainly due to the pedestrian group size \( *> * 2\) in the conflict crossing, shared spaces\), traffic patterns \(e.g., various user types\), and example. The probability of the game outcomes \( *𝑃 *\( *𝑠𝐿, 𝑠𝐹 *\)\) shows that traffic behaviour \(i.e., user behaviour in different countries\). 

the strategy deceleration-continuing returns a higher probability at the Two specific examples are selected from data sets to further explain reaction time \(time frame = 0\), where both players receive the highest the model performance and characteristics. The results are visualised in utility from their strategy choices. 

Fig. 11 & 12. The model is applied to conflict events in the time frames The second example is a pedestrian-2W conflict from the mid-block

prior/following the actual reaction time of the interacting users in the crossing data set \(Fig. 12\). The preferred strategy of the 2W, as the 12

*R. Ezzati Amini et al. *

*Accident Analysis and Prevention 203 \(2024\) 107604*

game leader, is to continue its path where the highest utility is gained. 

however, it is stronger in the pedestrian-passenger car model with

The pedestrian selects the left deviation strategy to cross the roadway deviation strategy choices available only for pedestrians. The effect of behind the 2W, rather than waiting until the conflict zone is clear. The deceleration variable is strong in both models \( *𝜃𝑑𝑐 > * 2 *𝜎 ̄ *\); however, *𝑑𝑐*

strategy pair of continuing-deviation left returns the highest probability deceleration is clearly dominant in the decision-making process of users at the actual reaction time of users \(time frame = 0\) as the final game in the mid-block crossing. This supports the user behaviour in the

outcome, in which the game leader receives its highest utility from its studied location, in which there is less tendency to slow down to give strategy choices. The final game outcome \( *𝑃 *\( *𝑠𝐿, 𝑠𝐹 *\)\) is similar to the the right of way in traffic interactions. The overall driver yielding rate taken strategies of users in the real-world conflict scenario. 

for pedestrians during the conflict scenarios in the mid-block crossing is approximately 12%, and motorised vehicles often deviate to pass

**7. Discussion**

the conflict zone. Therefore, the strategies with no speed changes are preferred by users in the game. 

In this research, a game-theoretic model is applied to predict the

conflict resolution strategies of pedestrians interacting with motorised **Social layer **\( ***𝜽𝒑𝒍***, ***𝜽𝒍𝒏***, ***𝜽𝒓𝒘***\): This layer of the game utility incorporates vehicles. The model assumes that users select a strategy that maximises the pedestrian group size, approaching lane, and the right of way. All their utilities. Further, the user’s choice of strategy in the proposed three variables have significant impact on user’s strategy choice in the Stackelberg game is based on the possible reaction of the interacting shared space model \( *𝜃𝑝𝑙 > * 2 *𝜎 ̄ *& *𝜃*

& *𝜃*

*𝑝𝑙*

*𝑙𝑛 > * 2 *𝜎 ̄*

*𝑙𝑛*

*𝑟𝑤 > * 2 *𝜎 ̄*

*𝑟𝑤*\) reflecting the

user to avoid a conflict. The latter property is substantial for a safe importance of social norms in safe movements of different user types traffic interaction – as a bilateral event – where the collective strategies in such urban designs. The social layer has slightly different influence of interacting users determine the outcome. The game utilities are

on the pedestrian–light vehicle model due to the user behaviour in the formulated in three layers of safety, travel, and social to cover a broad studied location. While the pedestrian group size is relevant for the range of factors influencing the user’s decision in a traffic conflict. In decision-making process of users in conflict in the mid-block crossing, the safety layer, previously developed conflict risk evaluation models approaching lane seems to be less strong. 

by Amini et al. \(2022\), are utilised to assess the safety of interacting It is worth noting that previous studies found a wider range of

users after performing each strategy pair. The safety layer estimates the factors influencing pedestrian behaviour during interactions, such as future minimum distance between interacting users, the relative time pedestrian age and gender, personal characteristics, culture, and wait-of users’ arrival at the collision zone \(i.e., new collision point or MD\), ing time. However, it is hard for the current stage of ADS development and conflicting speed. Then, based on the estimated surrogate safety to process such pedestrian-associated information \(Ezzati Amini et al. , indicators and model thresholds, the model identifies the hazardous

2021b\). Therefore, this research only employs the most significant traffic conditions between pedestrians and vehicles and returns a dis-factors – identified in the literature – currently feasible to process by utility when applicable. The comfort level of different strategies is the ADS. 

quantified in the travel layer for the detour, and deceleration im-

posed by users’ speed/trajectory changes. The users receive dis-utilities *7.2. Stackelberg game model applicability*

for the corresponding energy loss of each conflict resolution strategy available for users in the game. The third utility layer covers three The complexity of pedestrian interactions with motorised vehicles

of the most significant environmental factors influencing the user’s presents considerable challenges for users’ behavioural modelling and choice of strategy; pedestrian group size, pedestrian approaching lane, prediction. The characteristics’ discrepancy of different road user types and the right of way. The social layer signifies the importance of

and, thus, their granted/expected utilities, lead to exposing different be-social norms in improving safety in uncontrolled traffic environments. 

haviour on the interaction scene, where users employ various strategies Finally, the outcome of the proposed strategic game of the Stack-to escape a conflict. In the automation technology domain, there are elberg leadership competition is determined through the backward

many uncertainties regarding the most influential factors of pedestrian induction method. The proposed game-theoretic approach is estimated behaviour, the possible impact of these factors on pedestrian behaviour, separately for pedestrian interactions with passenger cars and light and the implementation of these factors in ADS \(Ezzati Amini et al. , vehicles \(i.e., 2Ws and 3Ws\). 

2021b\). However, there are several technological advancements to maintain pedestrian safety in the absence of a human driver in uncer-7.1. Impact factors

tain/conflicting traffic situations, such as pedestrian/object detection, To better evaluate the model variables, a Probability Density Func-tracking objects in motion, automated braking systems in case of haz-tion \(PDF\) \(sampling distribution of the sample mean\) is used to

ardous conditions, and pedestrian protection systems to minimise the visualise the relation between the shared space and mid-block crossing damage when a collision is unavoidable. Yet, in complex urban sce-for each parameter value \( *𝜃*

narios with a high level of elaborated interaction strategies among *𝑖*\) returned after the model estimations \(see

Fig. 13\):

road users, ADS are not fully capable of handling an efficient priority \(

\)

negotiation with traffic participants \(Fox et al. , 2018\). Therefore, a 2

1

−1

*𝑥*− *𝜇*

*𝑓 *\( *𝜃 *|

2

*𝜎*

suitable interaction method is required to ensure the efficiency of ADS

*𝑖 𝜇, 𝜎*\) =

√ *𝑒*

\(11\)

*𝜎*

2 *𝜋*

on the road and the safety of road users interacting with such vehicles. 

where *𝜇 * is the mean value and *𝜎 * is the standard error computed by the The proposed game-theoretic approach predicts the conflict resolution maximum likelihood method per *𝜃*. 

strategies of users in interaction by taking into account the safety outcome of various strategies in a conflict event and the impact of **Safety layer **\( ***𝜽𝒔𝒍***\): As expected, in both shared space and mid-block travel and environmental factors on user decisions. The game-theoretic crossing data sets, safety layer plays a significant role \( *𝜃𝑠𝑙 > * 2 *𝜎 ̄ *\). 

*𝑠𝑙*

approach has the potential to be used as a behavioural model for

This is because road users maximise their safety by employing conflict ADS and improve pedestrian safety, particularly in uncontrolled traffic resolution strategies that minimise the critical conflict and/or collision settings. The proposed model enables the ADS to make more informed

risk on the road. In the mid-block crossing model, the collision avoid-decisions during a traffic interaction, have a dynamic interaction with ance is crucial in strategy choice of users; however, the analysed data pedestrians, and react adequately to their actions when required. Such indicates that pedestrians primarily take courteous strategies during the interaction concept can prevent the ‘‘bullying behaviour’’ by other traf-interactions. 

fic participants to block the automated vehicle path or/and occurring **Travel layer **\( ***𝜽***

so-called ‘‘freezing robot problem’’ that they may be subject to Madigan

***𝒅𝒕***, ***𝜽𝒅𝒄 ***\): In both models \(i.e., data sets\), the parameter value of detour is substantial in user’s choice of strategy \( *𝜃𝑑𝑡 > * 2 *𝜎 ̄ *\); 

et al. \(2019\) and Färber \(2016\). 

*𝑑𝑡*

13

*R. Ezzati Amini et al. *

*Accident Analysis and Prevention 203 \(2024\) 107604*

**Fig. 13. **Comparison of the parameter estimates in developed models using the shared space and mid-block crossing data sets. 

Finally, such behavioural models can offer insights for policymak-

traffic settings, by using for instance, multiple participant simulator ers, urban planners, and transportation engineers seeking to enhance \(MPS\) technique \(Lehsing and Feldstein, 2018\). The MPS techniques pedestrian interactions with ADS in uncontrolled traffic environments. 

provide the same virtual environment for simultaneous interactions

For instance, policymakers could utilise the model’s predictions to among participants and can be used to improve the performance of

develop/improve regulations and guidelines, ensuring safe and effi-

the proposed models. Additionally, further validation approach can

cient integration of ADS. Urban planners could use the insights to

be employed to validate and refine the game-theoretic framework by

design pedestrian-friendly infrastructure and implement measures to comparing simulated outcomes with observed real-world data. Such

enhance pedestrian-ADS interactions, such as dedicated lanes or signal processes will allow adjustment of model parameters and algorithms to systems. Transportation engineers could apply the findings to optimise better align with actual traffic behaviour. These testing and validating traffic flow and minimise congestion by incorporating pedestrian be-efforts extend beyond the scope of the current study’s focus. 

haviour into traffic management strategies. These examples highlight Further, the Stackelberg game assumes that players \(i.e., interacting the practical relevance of such modelling approaches in real-world

road users\) within the game are rational and will try to maximise their decision-making and planning processes. 

payoffs; however, this may not always be the case. Road users can

behave irrationally during traffic interactions, or they may not have *7.3. Limitations and further research*

full information available for maximising payoffs. Such assumptions in game-theoretic approaches may potentially result in overlooking

In this research, the game-theoretic models are developed based on

certain conflict resolution strategies during traffic interactions, com-interaction data in a shared space in Hamburg, Germany, and a mid-

binations of evasive manoeuvres or undefined strategies in the game. 

block crossing in Surat, India. Despite the differences in crossing facility Therefore, the future model development requires adding an element

types and user behaviour in the studied locations, the models demon-of randomness that can explain several phenomena where players

strated good performance, verifying the transferability of the proposed do not behave in line with the rationality assumptions of the game

models. However, to construct a more suitable and realistic model, 

theory. Alternatively, other solutions that assume sub-optimal decision-further investigation is required. This entails conducting comprehen-making can be evaluated to relax such game assumptions \(Alsaleh

sive data analysis across varied traffic settings in different locations, 

and Sayed, 2022\). Besides, road users can perform a broader range of while employing harmonised pre-processing techniques. To address

evasive manoeuvres to avoid conflict in real-world traffic interactions. 

potential biases arising from data heterogeneity, the study undertakes For instance, pedestrians may execute unexpected changes in their

separate estimation of game-theoretic models for different conflict movement directions or suddenly stop at any crossroads point. How-scenarios observed in each location. By leveraging diverse interaction ever, it can be hard to incorporate such unpredictable behaviour into data, the study aims to develop a widely functional behavioural model the behavioural modelling approaches. Similarly, considering decision capable of capturing various user behaviour in uncontrolled traffic factors such as traffic culture, traffic volume, traffic layout, and age in environments. Moreover, it could be worth considering the inclusion behavioural models at this stage presents a challenge due to the current of road users with disabilities \(e.g., cane, wheelchair, guide dogs\) limitations of automated driving systems \(ADS\) in processing such

as well as pedestrians pushing strollers or prams, in future models, pedestrian-associated information. In addition, the deviation strategy to conduct additional testing and enhance the overall performance. 

of users in the model is considered with no speed changes to simplify Besides, this study suggests future works to focus on further test-the interaction model and avoid generating a computationally expen-

ing and validating the proposed model and its capability in various sive algorithm. Finally, the independent parameters of the proposed 14

*R. Ezzati Amini et al. *

*Accident Analysis and Prevention 203 \(2024\) 107604*

model are mostly based on the findings of the studies on traditional **Algorithm 1: **The strategy performance probability with respect pedestrian–vehicle interactions and the current stage of ADS develop-to the interacting user strategy in a pedestrian-passenger car

ment. This research suggests further studies to investigate how the vast conflict. 

existence of automated vehicles in the public realm can alter pedestrian **Input: ** *𝑈 * is the player exponential utility for each strategy behaviour, and which influencing factors in traditional interactions are \(combination\), *𝑖 * is the user in conflict events *𝑛*. *𝑠 * is the applicable within the ADS conceptual framework. 

user strategy, and *𝑆 * is strategy combinations always in

order of \( *𝑠𝑐𝑎𝑟, 𝑠𝑝𝑒𝑑𝑒𝑠𝑡𝑟𝑖𝑎𝑛*\):

**8. Conclusions**

*𝑐𝑐 *= \( *𝑠𝑐𝑜𝑛𝑡, 𝑠𝑐𝑜𝑛𝑡*\); *𝑐𝑑 *= \( *𝑠𝑐𝑜𝑛𝑡, 𝑠𝑑𝑒𝑐*\) *𝑐𝑙 *= \( *𝑠𝑐𝑜𝑛𝑡, 𝑠𝑑𝑒𝑣.𝑙𝑒𝑓𝑡*\); *𝑐𝑟 *= \( *𝑠𝑐𝑜𝑛𝑡, 𝑠𝑑𝑒𝑣.𝑟𝑖𝑔ℎ𝑡*\) Pedestrians with a high level of movement freedom on the road

*𝑑𝑐 *= \( *𝑠𝑑𝑒𝑐, 𝑠𝑐𝑜𝑛𝑡*\); *𝑑𝑑 *= \( *𝑠𝑑𝑒𝑐, 𝑠𝑑𝑒𝑐*\) can perform unexpected behaviour, leading to more complex traffic

*𝑑𝑙 *= \( *𝑠𝑑𝑒𝑐, 𝑠𝑑𝑒𝑣.𝑙𝑒𝑓𝑡*\); *𝑑𝑟 *= \( *𝑠𝑑𝑒𝑐, 𝑠𝑑𝑒𝑣.𝑟𝑖𝑔ℎ𝑡*\) interactions. Traffic participants intend to dominate the road space **Output: ** *𝑃 *: the strategy performance probability

during the interaction process while their safety is assured. Such comfor *𝑖 *← 1 ***to **𝑛 ***do**

petitions over the road space are more complicated in uncontrolled

**if ** *𝑙𝑒𝑎𝑑𝑒𝑟 = car*

*& *

*𝑝𝑙𝑎𝑦𝑒𝑟 = car ***then**

∑

mixed environments where users have to negotiate the right of way. 

*𝑃 𝐿*\( *𝑠*

∕

*𝑈 𝐿*

*𝑖*

*𝑖*\) = *𝑈 𝐿*

*𝑠*

*𝑠*∈ *𝐴𝐿𝐿*

Furthermore, the pedestrian interactions with other road users may

*𝑖*

**else if ** *𝑙𝑒𝑎𝑑𝑒𝑟 = car*

*& *

*𝑝𝑙𝑎𝑦𝑒𝑟 = pedestrian*

*& *

*𝑠𝑖*

become more challenging with the integration of ADS as a new road

∈ *𝑆* 1 ∶ \{ *𝑐𝑐, 𝑐𝑑, 𝑐𝑙, 𝑐𝑟*\} **then**

∑

user into the traffic and when the road infrastructure is not fully ready *𝑃 𝐹 *\( *𝑠 *| *𝑠*

∕

*𝑈 𝐹*

*𝑖*

*𝑖*

*𝑐𝑜𝑛𝑡*\) = *𝑈 𝐹*

*𝑠*

*𝑠*∈ *𝑆*

for merging such vehicles. In this case, the ADS require a suitable *𝑖*

1

**else if ** *𝑙𝑒𝑎𝑑𝑒𝑟 = car*

*& *

*𝑝𝑙𝑎𝑦𝑒𝑟 = pedestrian*

*& *

*𝑠𝑖*

interaction method to predict the intentions/decisions of interacting

∈ *𝑆* 2 ∶ \{ *𝑑𝑐, 𝑑𝑑, 𝑑𝑙, 𝑑𝑟*\} **then**

∑

users and consequently avoid conflict and improve traffic efficiency. 

*𝑃 𝐹 *\( *𝑠 *| *𝑠*

∕

*𝑈 𝐹*

*𝑖*

*𝑖*

*𝑑𝑒𝑐 *\) = *𝑈 𝐹*

*𝑠*

*𝑠*∈ *𝑆*

In this research, a game-theoretic approach is proposed to predict

*𝑖*

2

**else if ** *𝑙𝑒𝑎𝑑𝑒𝑟 = pedestrian*

*& *

*𝑝𝑙𝑎𝑦𝑒𝑟 = pedestrian ***then**

the conflict resolution strategies of pedestrians interacting with passen-

∑

*𝑃 𝐿*\( *𝑠*

∕

*𝑈 𝐿*

ger cars and light vehicles \(two-wheel and three-wheel vehicles\) during *𝑖*

*𝑖*\) = *𝑈 𝐿*

*𝑠𝑖*

*𝑠*∈ *𝐴𝑙𝑙*

**else if ** *𝑙𝑒𝑎𝑑𝑒𝑟 = pedestrian*

*& *

*𝑝𝑙𝑎𝑦𝑒𝑟 = car*

*& *

*𝑠*

road crossing scenarios in uncontrolled traffic settings. The models *𝑖*

∈ *𝑆*

employ a variety of factors influencing the decision-making process of 3 ∶ \{ *𝑐𝑐, 𝑑𝑐*\} **then **∑

*𝑃 𝐹 *\( *𝑠 *| *𝑠*

∕

*𝑈 𝐹*

users during a traffic conflict and are calibrated using interaction data *𝑖*

*𝑖*

*𝑐𝑜𝑛𝑡*\) = *𝑈 𝐹*

*𝑠𝑖*

*𝑠*∈ *𝑆* 2

**else if ** *𝑙𝑒𝑎𝑑𝑒𝑟 = pedestrian*

*& *

*𝑝𝑙𝑎𝑦𝑒𝑟 = car*

*& *

*𝑠*

of shared space and mid-block crossing areas. The models indicate good *𝑖*

∈ *𝑆*

performance given the stochastic behaviour of road users – particularly 4 ∶ \{ *𝑐𝑑, 𝑑𝑑*\} **then **∑

*𝑃 𝐹 *\( *𝑠 *| *𝑠*

∕

*𝑈 𝐹*

in the mid-block crossing area in India – and can potentially be used *𝑖*

*𝑖*

*𝑑𝑒𝑐 *\) = *𝑈 𝐹*

*𝑠𝑖*

*𝑠*∈ *𝑆* 4

**else if ** *𝑙𝑒𝑎𝑑𝑒𝑟 = pedestrian*

*& *

*𝑝𝑙𝑎𝑦𝑒𝑟 = car*

*& *

*𝑠*

as a behavioural model for the ADS. 

*𝑖*

∈ *𝑆* 5 ∶ \{ *𝑐𝑙, 𝑐𝑙*\} **then**

∑

*𝑃 𝐹 *\( *𝑠 *| *𝑠*

∕

*𝑈 𝐹*

**CRediT authorship contribution statement**

*𝑖*

*𝑑𝑒𝑣.𝑙𝑒𝑓 𝑡*\) = *𝑈 𝐹*

*𝑠𝑖*

*𝑠*∈ *𝑆* 4

**else**

∑

**Roja Ezzati Amini: **Software, Methodology, Investigation, Formal *𝑃 𝐹 *\( *𝑠 *| *𝑠*

∕

*𝑈 𝐹*

; 

*𝑠*

*𝑖*

*𝑖*

*𝑑𝑒𝑣.𝑟𝑖𝑔ℎ𝑡*\) = *𝑈 𝐹*

*𝑠*

*𝑖 *∈ *𝑆* 5 ∶ \{ *𝑐𝑟, 𝑐𝑟*\}

*𝑖*

*𝑠*∈ *𝑆* 5

analysis, Conceptualization, Validation, Visualization, Writing – orig-end

inal draft. **Mohamed Abouelela: **Writing – review & editing, Formal **end**

analysis, Software. **Ashish Dhamaniya: **Supervision, Writing – re-R packages used to run the code of this algorithm: tidyverse, dplyr, view & editing. **Bernhard Friedrich: **Supervision, Writing – review purrr, pipeR, data.table, readr \(R Core Team, 2024\). 

& editing. **Constantinos Antoniou: **Supervision, Writing – review & editing. 

**Appendix**

**Declaration of competing interest**

The authors declare that they have no known competing finan-

See Algorithm 1. 

cial interests or personal relationships that could have appeared to influence the work reported in this paper. 

**References**

**Data availability**

Ali, Y., Zheng, Z., Haque, M.M., Wang, M., 2019. A game theory-based approach for

modelling mandatory lane-changing behaviour in a connected environment. Transp. 

The authors do not have permission to share data. 

Res. C 106, 220–242. 

Alsaleh, R., Sayed, T., 2020. Modeling pedestrian-cyclist interactions in shared space

using inverse reinforcement learning. Transp. Res. F 70, 37–57. 

**Acknowledgements**

Alsaleh, R., Sayed, T., 2021. Markov-game modeling of cyclist-pedestrian interactions in

shared spaces: A multi-agent adversarial inverse reinforcement learning approach. 

This work is supported by the European Union Horizon 2020

Transp. Res. C 128, 103191. 

research and innovation programme under grant agreement No 815001

Alsaleh, R., Sayed, T., 2022. Do road users play Nash equilibrium? A comparison

\(Drive2thefuture project\), and the DAAD project number 57474280

between Nash and Logistic stochastic Equilibriums for multiagent modeling of road

user interactions in shared spaces. Expert Syst. Appl. 205, 117710. 

Verkehr-SuTra: Technologies for Sustainable Transportation, within the

Amini, R.E., 2022. An Interaction Game for Prediction of Road Users’ Conflict Reso-

Programme ‘‘A New Passage to India - Deutsch-Indische Hochschulko-

lution Strategies in Uncontrolled Traffic Environments \(Ph.D. thesis\). Universität

operationen ab 2019’’, the German Federal Ministry of Education

München. 

and Research, Bundesministerium für Bildung und Forschung \(BMBF\), 

Amini, R.E., Yang, K., Antoniou, C., 2022. Development of a conflict risk evaluation

project FuturTrans: Indo-German Collaborative Research Center on

model to assess pedestrian safety in interaction with vehicles. Accid. Anal. Prev. 

Intelligent Transportation Systems. The authors thankfully acknowl-

175, 106773. 

Beggiato, M., Witzlack, C., Krems, J.F., 2017. Gap acceptance and time-to-arrival

edge the contribution of the research project MODIS \(Multi mODal

estimates as basis for informal communication between pedestrians and vehicles. 

Intersection Simulation\) for providing and pre-processing the shared

In: Proceedings of the 9th International Conference on Automotive User Interfaces

space data-set utilised in this study. 

and Interactive Vehicular Applications. pp. 50–57. 

15

*R. Ezzati Amini et al. *

*Accident Analysis and Prevention 203 \(2024\) 107604*

Chen, Y., Liu, M., Liu, S.-Y., Miller, J., How, J.P., 2016. Predictive modeling of

Møgelmose, A., Trivedi, M.M., Moeslund, T.B., 2015. Trajectory analysis and prediction

pedestrian motion patterns with bayesian nonparametrics. In: AIAA Guidance, 

for improved pedestrian safety: Integrated framework and evaluations. In: 2015

Navigation, and Control Conference. p. 1861. 

IEEE Intelligent Vehicles Symposium. IV, IEEE, pp. 330–335. 

Coppola, A., Stewart, B., Okazaki, N., 2014. Lbfgs: Limited-memory BFGS optimization. 

Nasernejad, P., Sayed, T., Alsaleh, R., 2021. Modeling pedestrian behavior in pedestrian-

URL: https://CRAN.R-project.org/package=lbfgs, R package version 1.2.1. 

vehicle near misses: A continuous Gaussian process inverse reinforcement learning

Douglas, B., 2017. Tracker: Video analysis and modeling tool. Tracker version 4.11.0

\(GP-IRL\) approach. Accid. Anal. Prev. 161, 106355. 

4. 

Nasernejad, P., Sayed, T., Alsaleh, R., 2023. Multiagent modeling of pedestrian-vehicle

Ezzati Amini, R., Dhamaniya, A., Antoniou, C., 2021a. Towards a game theoretic

conflicts using Adversarial Inverse Reinforcement Learning. Transportmetrica A:

approach to model pedestrian road crossings. Transp. Res. Procedia 52, 692–699. 

Transp. Sci. 19 \(3\), 2061081. 

Ezzati Amini, R., Katrakazas, C., Antoniou, C., 2019. Negotiation and decision-making

Nash, J., 1951. Non-cooperative games. Ann. of Math. 286–295. 

for a pedestrian roadway crossing: A literature review. Sustainability 11 \(23\), 6713. 

NSC-Injury Facts, N.S.C., 2019. Pedestrian fatalities. https://injuryfacts.nsc.org/motor-

Ezzati Amini, R., Katrakazas, C., Riener, A., Antoniou, C., 2021b. Interaction of

vehicle/road-users/pedestrians/. 

automated driving systems with pedestrians: challenges, current solutions, and

Parker, Jr., M., Zegeer, C.V., 1989. Traffic Conflict Techniques for Safety and Op-

recommendations for eHMIs. Transp Rev 1–26. 

erations: Observers Manual. Technical Report, United States. Federal Highway

Färber, B., 2016. Communication and communication problems between autonomous

Administration. 

vehicles and human drivers. In: Autonomous Driving. Springer, pp. 125–144. 

Pascucci, F., 2020. A Microsimulation Based Method to Evaluate Shared Space

Feng, C., Cunbao, Z., Bin, Z., 2019. Method of pedestrian-vehicle conflict eliminating

Performances

\(Ph.D. 

thesis\). 

Technische

Universität

Carolo-Wilhelmina

zu

at unsignalized mid-block crosswalks for autonomous vehicles. In: 2019 5th

Braunschweig. 

International Conference on Transportation Information and Safety. ICTIS, IEEE, 

Pascucci, F., Rinke, N., Schiermeyer, C., Berkhahn, V., Friedrich, B., 2018. A discrete

pp. 511–519. 

choice model for solving conflict situations between pedestrians and vehicles in

Fox, C., Camara, F., Markkula, G., Romano, R., Madigan, R., Merat, N., 2018. 

shared space. In: The 97th Annual Meeting of the Transportation Research Board

When should the chicken cross the road?-game theory for autonomous vehicle-

\(TRB\) January 2018, Washington D.C.. USA, pp. 7–11. 

human interactions. In: Proceedings of the 4th International Conference on Vehicle

Pascucci, F., Rinke, N., Schiermeyer, C., Friedrich, B., Berkhahn, V., 2015. Modeling

Technology and Intelligent Transport Systems. Vol. 1, SciTePress, pp. 431–439. 

of shared space with multi-modal traffic using a multi-layer social force approach. 

Fricker, J.D., Zhang, Y., 2019. Modeling pedestrian and motorist interaction at semi-

Transp. Res. Procedia 10, 316–326. 

controlled crosswalks: The effects of a change from one-way to two-way street

Pascucci, F., Rinke, N., Timmermann, C., Berkhahn, V., Friedrich, B., 2021. Dataset

operation. Transp. Res. Rec. 2673 \(11\), 433–446. 

used for discrete choice modeling of conflicts in shared spaces. http://dx. 

Golakiya, H., Dhamaniya, A., 2018. Evaluation of pedestrian safety index at urban

doi.org/10.24355/dbbs.084-202111081809-0, URL: https://publikationsserver.tu-

mid-block. In: Urbanization Challenges in Emerging Economies: Energy and Water

braunschweig.de/receive/dbbs\_mods\_00069907, This dataset belongs to the foll-

Infrastructure; Transportation Infrastructure; and Planning and Financing. American

wing article publications: Pascucci, F., Rinke, N., Schiermeyer, C., Berkhahn, V., & 

Society of Civil Engineers Reston, VA, pp. 676–687. 

Friedrich, B. \(2017\). A discrete choice model for solving conflict situations between

Golakiya, H.D., Patkar, M., Dhamaniya, A., 2019. Impact of midblock pedestrian

pedestrians and vehicles in shared space. arXiv preprint arXiv:1709.09412. 

crossing on speed characteristics and capacity of urban arterials: civil engineering:

Pawar, D.S., Patil, G.R., 2015. Pedestrian temporal and spatial gap acceptance at

transportation engineering. Arab. J. Sci. Eng. 44, 8675–8689. 

mid-block street crossing in developing world. J. Saf. Res. 52, 39–46. 

Gorrini, A., Vizzari, G., Bandini, S., 2016. Towards modelling pedestrian-vehicle

Pfortmueller, C.A., Marti, M., Kunz, M., Lindner, G., Exadaktylos, A.K., 2014. Injury

interactions: Empirical study on urban unsignalized intersection. In: Proceeding of

severity and mortality of adult zebra crosswalk and non-zebra crosswalk road

the 8th International Conference on Pedestrian Evacuation Dynamics. pp. 25–33. 

crossing accidents: a cross-sectional analysis. PLoS One 9 \(3\), e90835. 

Jayaraman, K., Tilbury, D.M., Yang, X.J., Pradhan, A.K., Robert, L.P., 2020. Analysis

R Core Team, 2024. R: A Language and Environment for Statistical Computing. 

and prediction of pedestrian crosswalk behavior during automated vehicle interac-

R Foundation for Statistical Computing, Vienna, Austria, URL:

https://www.R-

tions. In: 2020 IEEE International Conference on Robotics and Automation. ICRA, 

project.org/. 

IEEE, pp. 6426–6432. 

Rehder, E., Wirth, F., Lauer, M., Stiller, C., 2018. Pedestrian prediction by planning

Johora, F.T., Müller, J.P., 2020. Zone-specific interaction modeling of pedestrians and

using deep neural networks. In: 2018 IEEE International Conference on Robotics

cars in shared spaces. Transp. Res. Procedia 47, 251–258. 

and Automation. ICRA, IEEE, pp. 5903–5908. 

Kadali, B.R., Vedagiri, P., 2020. Role of number of traffic lanes on pedestrian gap

van Rijsbergen, C., 1979. Information Retrieval, second ed. Butterworths, London. 

acceptance and risk taking behaviour at uncontrolled crosswalk locations. J. Transp. 

Sayed, T., Zein, S., 1999. Traffic conflict standards for intersections. Transp. Plan. 

Health 19, 100950. 

Technol. 22 \(4\), 309–323. 

Kemloh wagoum, A.U., Seyfried, A., Holl, S., 2012. Modeling the dynamic route choice

Schneemann, F., Gohl, I., 2016. Analyzing driver-pedestrian interaction at crosswalks:

of pedestrians to assess the criticality of building evacuation. Adv. Complex Syst. 

A contribution to autonomous driving in urban environments. In: 2016 IEEE

15 \(07\), 1250029. 

Intelligent Vehicles Symposium. IV, IEEE, pp. 38–43. 

Lanzaro, G., Sayed, T., Alsaleh, R., 2022. Modeling motorcyclist–pedestrian near misses:

Schneemann, F., Heinemann, P., 2016. Context-based detection of pedestrian crossing

A multiagent adversarial inverse reinforcement learning approach. J. Comput. Civ. 

intention for autonomous driving in urban environments. In: 2016 IEEE/RSJ

Eng. 36 \(6\), 04022038. 

International Conference on Intelligent Robots and Systems. IROS, IEEE, pp. 

Lehsing, C., Feldstein, I.T., 2018. Urban interaction–getting vulnerable road users into

2243–2248. 

driving simulation. UR: BAN Hum. Fact. Traffic: Appr. Safe Effic. Stress-free Urban

Schönauer, R., 2017. A Microscopic Traffic Flow Model for Shared Space \(Ph.D. thesis\). 

Traffic 347–362. 

Graz University of Technology. 

Liao, W., Kemloh Wagoum, A.U., Bode, N.W., 2017. Route choice in pedestrians:

Sucha, M., Dostal, D., Risser, R., 2017. Pedestrian-driver communication and decision

determinants for initial choices and revising decisions. J. R. Soc. Interface 14 \(127\), 

strategies at marked crossings. Accid. Anal. Prev. 102, 41–50. 

20160684. 

Sun, D., Ukkusuri, S., Benekohal, R.F., Waller, S.T., 2003. Modeling of motorist-

Lloyd, S., 1982. Least squares quantization in PCM. IEEE Trans. Inform. Theory 28 \(2\), 

pedestrian interaction at uncontrolled mid-block crosswalks. In: Transp. Res. Rec., 

129–137. 

TRB Annual Meeting CD-ROM. Washington, DC. 

Lloyd, D., Wilson, D., Mais, D., Deda, W., Bhagat, A., 2015. Reported road casualties

Talebpour, A., Mahmassani, H.S., Hamdar, S.H., 2015. Modeling lane-changing behavior

great britain: 2014 annual report. 

in a connected environment: A game theory approach. Transp. Res. Procedia 7, 

Lord, D., van Schalkwyk, I., Chrysler, S., Staplin, L., 2007. A strategy to reduce

420–440. 

older driver injuries at intersections using more accommodating roundabout design

Velupillai, K.V., 2009. Uncomputability and undecidability in economic theory. Appl. 

practices. Accid. Anal. Prev. 39 \(3\), 427–432. 

Math. Comput. 215 \(4\), 1404–1416. 

Madigan, R., Nordhoff, S., Fox, C., Amini, R.E., Louw, T., Wilbrink, M., Schieben, A., 

1968. Vienna convention on road traffic. https://unece.org/DAM/trans/conventn/Conv\_

Merat, N., 2019. Understanding interactions between Automated Road Transport

road\_traffic\_EN.pdf. 

Systems and other road users: A video analysis. Transp. Res. F 66, 196–213. 

Völz, B., Mielenz, H., Gilitschenski, I., Siegwart, R., Nieto, J., 2018. Inferring pedestrian

Malenje, J.O., Zhao, J., Li, P., Han, Y., 2018. An extended car-following model with

motions at urban crosswalks. IEEE Trans. Intell. Transp. Syst. 20 \(2\), 544–555. 

the consideration of the illegal pedestrian crossing. Phys. A 508, 650–661. 

World Health Organisation, 2019. Road traffic injuries. URL:

https://www.who.int/

news-room/fact-sheets/detail/road-traffic-injuries. 

16



# Document Outline

+ A game-theoretic approach for modelling pedestrian–vehicle conflict resolutions in uncontrolled traffic environments  
	+ Introduction  
		+ Research contributions 

	+ Literature review  
		+ Pedestrian–vehicle interactions 
		+ Pedestrian-ADS interactions 

	+ Conflict resolution model  
		+ General structure of the Stackelberg game 
		+ Stackelberg game solution 
		+ Formulation of utility functions  
			+ Safety layer 
			+ Travel layer 
			+ Social layer 
			+ Utility function 


	+ Data collection and conflict analysis  
		+ Video surveys  
			+ Mid-block crossing interactions 
			+ Shared space interactions 

		+ Conflict detection strategies 
		+ Conflict resolution determination  
			+ Determination of the preferred speed 
			+ Determination of deceleration rate 
			+ Determination of deviation angle 


	+ Application of the Stackelberg game 
	+ Model results  
		+ Estimating the game-theoretic models 
		+ Game leadership estimation 
		+ Model performance and validation 

	+ Discussion  
		+ Impact factors 
		+ Stackelberg game model applicability 
		+ Limitations and further research 

	+ Conclusions 
	+ CRediT authorship contribution statement 
	+ Declaration of competing interest 
	+ Data availability 
	+ Acknowledgements 
	+ Appendix 
	+ References



