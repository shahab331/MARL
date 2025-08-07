1

Cooperative Driving of Connected Autonomous Vehicles in Heterogeneous Mixed Traffic: A Game Theoretic Approach

Shiyu Fang, Peng Hang, Member, IEEE, Chongfeng Wei, Member, IEEE, Yang Xing, Member, IEEE, and Jian Sun

Abstract—High-density, unsignalized intersection has always be able to actively cooperate with other vehicles to resolve been a bottleneck of efficiency and safety. The emergence of conflict by properly arranging Right of Way \(ROW\). However, Connected Autonomous Vehicles \(CAVs\) results in a mixed traffic there still exist some challenges. On account of the complexity condition, further increasing the complexity of the transportation of real-world situations, CAVs may behave unreasonably when system. Against this background, this paper aims to study the intricate and heterogeneous interaction of vehicles and conflict interacting with Human Vehicles \(HVs\) which may lead to resolution at the high-density, mixed, unsignalized intersection. 

collision or deadlock. There is a further question about how Theoretical insights about the interaction between CAVs and to ascend system performance by coordinating the relationship Human-driven Vehicles \(HVs\) and the cooperation of CAVs between vehicles. Not to mention that CAV control in mixed are synthesized, based on which a novel cooperative decision-traffic containing CAVs and heterogeneous HVs is still a making framework in heterogeneous mixed traffic is proposed. 

Normalized Cooperative game is concatenated with Level-k game continuing cause for concern. 

\(NCL game\) to generate a system optimal solution. Then Lattice For decades, one of the ideas to ameliorate the above planner generates the optimal and collision-free trajectories problem is to explore the latent rules and patterns from for CAVs. To reproduce HVs in mixed traffic, interactions human interactions. Numerous studies have analyzed drivers’

from naturalistic human driving data are extracted as prior decision-making logic, cognitive structure, and inherent char-knowledge. Non-cooperative game and Inverse Reinforcement Learning \(IRL\) are integrated to mimic the decision making acteristics to design a human-like CAV. Game theory for-of heterogeneous HVs. Finally, three cases are conducted to mulates the interaction between incentive structures and the verify the performance of the proposed algorithm, including the relationship between players’ strategies which has been widely comparative analysis with different methods, the case study under used to replicate social decision making \[1, 2\]. Except for different Rates of Penetration \(ROP\) and the interaction analysis the advantage of interpretability, game theory is also suit-with heterogeneous HVs. It is found that the proposed cooperative decision-making framework is beneficial to the driving conflict able for dissimilar scenarios such as roundabouts \[3\], on-resolution and the traffic efficiency improvement of the mixed ramp merging areas \[4, 5\], and unsignalized intersections unsignalized intersection. Besides, due to the consideration of

\[6, 7\]. Instead of treating surrounding vehicles as moving driving heterogeneity, better human-machine interaction and obstacles, the game theoretic approach was adapted to mimic cooperation can be realized in this paper. 

human behavior by dynamically interacting with surrounding Index Terms—connected autonomous vehicles, heterogeneous vehicles for automatic lane changing \[8\]. Level-k game was mixed traffic, unsignalized intersection, level-k game, inverse combined with vehicle controller \[9\] and Monte Carlo tree reinforcement learning, cooperative driving search \(MTCS\) \[10\] respectively to model the time-extended, multi-step, and interactive decision making of CAV. Mean-I. INTRODUCTION

arXiv:2305.03563v1 \[cs.MA\] 5 May 2023

while, identifying real-time intentions through human cogni-THE past decade has seen the rapid development of tive structure plays an important role in developing human-Connected Autonomous Vehicles \(CAVs\). CAV has a centric intelligent vehicles. Therefore, Chu et al. \[11\] explored wider perception range and smaller perception error which the mechanisms behind distracted driving intentions based attach it the potential to perceive danger earlier and even on Stimulus-Organism-Response \(SOR\) cognitive theory. In addition, Artificial Neural Network \(ANN\) was designed by This work was supported in part by the Natural Science Foundation of China \(52232015 and 52125208\), the Fundamental Research Funds for the Central mimicking the mechanism by which information is transmitted Universities \(No. 2022-5-ZD-02\), and the Zhejiang Lab \(2021NL0AB02\). 

in the animal neural network and it was used to predict drivers’

S. Fang, P. Hang and J. Sun are with the Department of Traffic Engineering intentions in on-ramp merging \[12\], lane changing \[13\], and and Key Laboratory of Road and Traffic Engineering, Ministry of Education, Tongji University, Shanghai 201804, China. \(e-mail: \{2111219, hangpeng, left-turning \[14\]. Bi et al. \[15\] proposed a queuing network sunjian\}@tongji.edu.cn\)

cognitive architecture to infer intentions with and without C. Wei is with the School of Mechanical and Aerospace Engineering at distraction tasks and the experiments carried out on a driving Queen’s University Belfast, BT7 1NN Belfast, UK. \(email: c.wei@qub.ac.uk\) Y. Xing is with the School of Aerospace, Transport, and Manufacturing, simulator have shown a good performance in inferring typical Cranfield University, UK, MK43 0AL. \(e-mail: yang.x@cranfield.ac.uk\) and rapid lane-changing behavior intentions. Same to the Corresponding author: P. Hang

diverse and fickle intentions, drivers themselves also possess This work has been submitted to the IEEE for possible pubilcation. 

Copyright may transferred without notice, after which this version may no different characteristics. Huang et al. \[16\] adopted Inverse longer be accessible

Reinforcement Learning \(IRL\) to model the different driving

2

behavior from naturalistic human driving data. Schwarting or the cooperation methods in a CAVs-only environment et al. \[1\] addressed Social Value Orientation \(SVO\), which merely leads to a half-baked CAV, their performance under quantifies the degree of an agent’s selfishness or altruism, complex interactive scenarios should be further evaluated. So and then modeled the interactions between agents as a best-far, there has been little discussion about the verification response game. Despite a number of works that have shown and validation of CAV in mixed traffic. Wang et al. \[27\]

that the interaction between CAVs and HVs can be solved by a demonstrated his controller by adding background traffic flow best-response game, a rational collective decision might be the but only four vehicles at most were involved in their two-opposite of the socially optimum \[17\]. Therefore, a solution lane merging scenario. Besides, human-in-the-loop trail on the to tackle this phenomenon is to establish an institutional driving simulator is also a practical way to replicate mixed arrangement that can optimize the system performance via traffic. Sadigh et al. \[28\] pioneering excavated the ability cooperative driving. 

for CAV to actively gather the information of surrounding The cooperative driving of CAVs has been widely studied. 

HV, and experiments were carried out on a driving simulator. 

Cooperation refers to the decision-making process of vehicles The fly in the ointment is that experiments only consider aimed at orchestrating vehicles’ actions so as to achieve a one-on-one interaction. Furthermore, multiple human-machine goal that can not be achieved by each vehicle in isolation interactions seem unpractical on the driving simulator because

\[18\]. Furthermore, CAVs cooperative approaches can be clas-of the equipment limitations. Therefore, existing studies about sified into centralized, negotiation, agreement, and emergent mixed traffic are mainly low-density which is an extraordinary according to CAVs’ extent of autonomy. In the centralized simplification. While real-world heterogeneous mixed traffic control, a coordinator will act as an intersection manager to is far more hazardous because drivers’ preferences will drive reserve certain space-time for each approaching vehicle \[19\]

them to make different decisions. 

or to decide all vehicles’ strategies for at least one global task \[20\]. However, the capability of the coordinator is a To address the aforementioned challenges, the cooperative potential bottleneck. Zhou et al. \[21\] proposed a situation-driving of CAVs in heterogeneous mixed traffic conditions aware Reasoning Graph \(RG\) and combined it with some rules is studied. The contributions of this paper are presented as for maneuver compatibility and social interaction customs to follows:

quickly search for speed profiles that follow the reasoned 1. This paper proposes a novel cooperative driving frame-situations. Although Xu et al. \[22\] combined MCTS with work that enables CAVs to cooperate in high-density, mixed, heuristic rules to find a nearly global-optimal passing order unsignalized intersections and coordinate with heterogeneous for CAVs and results showed that it can keep a good trade-human drivers, in favor of driving conflict resolution, human-off between system performance and computation flexibility. 

machine interaction augmentation and traffic efficiency im-Under centralized control, CAVs only passively follow the provement. 

instruction of the coordinator so their potentials are far from being tapped. Negotiation and agreement approaches use fixed 2. The cooperative decision making of CAVs is realized and dynamics protocols respectively to allow CAVs to commu-by concatenating Normalized Cooperative game and Level-k nicate with others. Carlino et al. \[23\] proposed a decentralized game \(NCL game\), which outputs the k-allocation that cor-auction-based autonomous intersection management scheme to responds to maximum system overall efficiency. Then Lattice permit vehicle passage based on their value of time. Vu et al. 

planner is combined to generate an optimal and collision-free

\[24\] further migrated auctions to a cellular automaton model. 

CAV trajectory. The cooperation performance of CAVs under However, these cooperation approaches are infeasible for HVs different Rates of Penetration \(ROP\) is verified. 

because the action of human is uncontrollable. Simultaneously, during communication, CAVs adhering to a meticulously de-3. To simulate the human-machine interaction in authentic signed protocol will further cause robustness problems. Instead mixed traffic, heterogeneous HV decisions are modelled. By of directly communicating with other vehicles or following clustering, driver classification and composition are obtained any predefined cooperation protocol, in emergent approaches, and serve as prior knowledge. Non-cooperative game is used each vehicle makes its decision by estimating the rationality of to reproduce driver’s rational decision under an interactive others and deducing their actions based on the current state. 

environment and IRL is utilized to calibrate different drivers’

Wang et al. \[7\] established a cooperation model for agents decision-making preferences. Finally, heterogeneous HVs are with different priorities through game theory. In addition, introduced to the simulation experiment to examine the effec-previous work also hybridized objective-novelty evolutionary tiveness and robustness of the cooperative driving framework. 

search for synthesizing CAV cooperative behavior on CAVs-only roads \[25\]. Experiments showed that desired cooperative The rest of the paper is organized as follows. Section II driving behavior emerged when multiple vehicles interacted, introduces the main problem of our research and the corre-but their results failed to generalize to new roads. To sum up, sponding cooperative driving framework to solve it. Repro-the above research focused on CAVs-only environment cooper-ducing heterogeneous HV decision is described in Section III. 

ation. Nevertheless, real-world traffic flow will be mixed with Section IV discusses the process of CAV cooperative decision HVs for at least 40 years according to \[26\], so the effectiveness making and trajectory planning. In Section V, we validate our under a mixed traffic environment has yet to be proven. 

framework through several simulation experiments. Finally, Aiming at either the interactions between CAV and HV

conclusions are made in Section VI. 

3

In addition, for the cooperative decision making and trajectory planning of CAVs, the three-layer hierarchy that most autonomous robot controls are using to generate the safe and continuous state is adopted \[29, 30\]. At the top of the hierarchy, level-k game is introduced to imitate the human reasoning depths and also served as a next-layer’s independent variable. Then, based on cooperative game, k-allocation which leads to system optimum can be achieved by enumerating. At the bottom layer, Lattice planner will generate an optimal and collision-free trajectory that conforms to the vehicle’s dynamic constraints. 

Mixed traffic in the simulation will be updated every ∆t =

0.1s through vehicles dynamically competing and coordinating Fig. 1. 

Thumbnail of the high-density, unsignalized intersection with heterogeneous HVs involved. 

with each other. Finally, we validate our framework with experiments, including the comparative analysis with different methods, the case study under different Rates of Penetration \(ROP\) and the interaction analysis with heterogeneous HVs. 

II. PROBLEM STATEMENT AND COOPERATIVE DRIVING

FRAMEWORK

III. REPRODUCING HETEROGENEOUS HV DECISIONS IN

CAVs are still much-maligned due to their intricate ma-MIXED TRAFFIC

neuvers and deficient control methods. Deadlock and colli-Despite the uncertainty due to the absence of traffic lights, sion may happen when CAVs interact with others in com-unpredictable and uncontrollable HV latent intention of de-plex, interactive scenarios. Among all urban traffic scenarios, cision may lead to even greater strait for CAVs. In order unsignalized intersections are the most challenging owing to to validate the cooperative driving algorithm of CAVs in their numerous conflict points and fickle interaction opponents. 

heterogeneous mixed traffic. In this section, sophisticated real-Furthermore, human drivers are heterogeneous so they may world drivers’ demonstrations were extracted for reproducing adopt various maneuvers in the same circumstances based on heterogeneous HV decisions. 

their decision-making preferences. Therefore, CAVs always The main process consists of four steps. Firstly, interaction tend to passive defensive action such as excessive deceleration data from a real-world intersection were collected. Secondly, which leads to inefficiencies, or even worse, to the loss of trust drivers’ decisions were classified into three groups by K-means in CAVs. 

cluster. Then, non-cooperative game, known as a promising However, few studies have focused on multiple human-model to reproduce the process of human decision making, machine interactions which will be ubiquitous in the coming was selected to guide the generation of HVs’ decision. Finally, future. Hence the effectiveness and robustness of the algorithm the decision-making preference of each group was calibrated for CAVs remain unclear. We hold the opinion that investigat-through IRL. 

ing the interactions of CAVs and HVs in sophisticated scenarios is of great significance to the validation and application A. Data Collection

of our cooperative driving algorithm for CAVs. Therefore, the As mentioned before, investigating the interactions of HVs main problem of this paper is to enable CAVs to properly is of great use to establish either HVs or human-like CAVs. In respond to or even actively coordinate with heterogeneous HVs our paper, data acquisition was carried out at an intersection in a high-density, unsignalized intersection. Fig. 1 shows a in Shanghai, China: XianXia Rd-JianHe Rd \(XXJH\) based on thumbnail of the intersection. 

previous research of Ni et al. \[31\]. Then interaction event was To achieve the above purpose, an elaborate framework is extracted if its Post Encroachment Time \(PET\) was less than proposed, shown in Fig. 2. Firstly, naturalistic human driving 3s. 

data are collected and analyzed for investigating the driver After screening, 79 of 131 interaction events were retained. 

decision type and its distribution from a real-world intersec-Meanwhile, the trajectories of the HVs were extracted through tion. Besides, it has to be noted that modeling heterogeneous a semi-automated video image processing tool and then served drivers mammoth project. Given that this paper is primarily as prior knowledge. Furthermore, their speed and acceleration concerned with establishing a cooperative driving framework were calculated for clustering. 

for CAV, we turn to reproduce the heterogeneous decision for simplification. Then a series of feasible trajectories are generated through non-cooperative game and compare them B. Drivers’ Decisions Classification by K-means Cluster with expert demonstrations from naturalistic human driving As is known to all that drivers’ decisions can be divided data. Through maximum entropy IRL, different decision-into several types such as aggressive, normal, and conservative. 

making preferences θT are calibrated. We then reproduce In order to reproduce drivers with different decision-making the decision of heterogeneous HVs with Nash Equilibrium preferences. The first priority was to determine how many solution and generate the corresponding next state through decision clusters the drivers at the intersection of XXJH can vehicle dynamics. 

be divided into. 

4

Fig. 2. 

Cooperative driving framework in mixed traffic. 

Based on the result of the elbow method, a simple but it achieves more realistic human behavior when performing versatile theory to determine the number of clusters using conflicting maneuvers at intersections \[34, 35\]. Together with the Sum of Squared Errors \(SSE\), three clusters work best vehicle dynamics, feasible trajectories of each frame can be for our data. Considering that speed and acceleration are the concluded. 

most intuitive manifestation of decision making during driving, the average, maximum, minimum, and standard deviation of C. HVs’ Feasible Trajectories Generation through Non-speed and acceleration of vehicles were taken as the clustering cooperative Game

parameters based on Chen et al. \[32\]. K-means clustering was then used to classify naturalistic human driving data samples As mentioned before, game theory describes human as a in XXJH. 

rational decision-maker who takes action dependencies into account. Hence, there is a growing application in the field of TABLE I

modeling human decision. In this paper, we regard human CLUSTERING CENTERS OF XXJH DATA

drivers as rational decision-makers and are aware of the consequence that their actions will influence other drivers who V \(m/s\)

Params

mean

max

max

min

have conflict with them in temporal and spatial dimensions. 

Cluster-1

3.31

4.42

2.36

0.66

Non-cooperative game was therefore established to mimic how Cluster-2

1.34

1.60

0.99

0.27

drivers conjecture and compete with each other while driving Cluster-3

6.29

6.98

5.40

0.50

A\(m/s2\)

in sharing space. 

Params

mean

max

max

min

We considered a sampling interval, ∆t = 0.1s, and an Cluster-1

-0.07

0.49

-0.72

0.37

action set including six strategies that represent common Cluster-2

0.08

0.55

-0.34

0.28

Cluster-3

-0.77

-0.30

-1.14

0.28

driving maneuvers in urban traffic based on Tian et al. \[3\], 

listed in Table. II. 

After the clustering algorithm converged, the center of each TABLE II

cluster can be obtained, as shown in Table. I. Since it was not ACTION SET U

the main concern of our study, we simply assumed that speed Action u

A\(m/s2\)

ω\(rad/s\)

was the most important variable affecting the aggressiveness of Maintain u1

0

0

a decision while driving based on Huang et al. \[33\]. Therefore, Accelerate u2

2

0

Decelerate u

the drivers’ decisions in the 79 interaction events were divided 3

-2

0

Brake u4

-4

0

into three clusters: normal, conservative, and aggressive. Fur-Turn left u5

0

π/4

thermore, their trajectories were used as expert demonstrations Turn right u6

0

−π/4

and then compared with HVs’ feasible trajectories to calibrate different decision-making preferences. In this paper, non-where U is the action set, ui = \[ai, ωi\]T

t

t

t

is the action of

cooperative game was chosen to estimate possible decisions vehicle i at t frame, ait is acceleration, and ωit is heading human may adopt when confronted with other drivers because angle rate. Therefore, six feasible trajectories can be generated

5

in each frame by constituting action uit with vehicle dynamics expert decision. IRL was proposed later than behavior cloning. 

in Eq. 1. 

Though they share many similarities. Differing from simply imitating expert maneuvers, IRL tries to infer the reason why

xi \+ vi cos\(γi\)∆t

t

t

t

experts make their decision and then optimize the strategy. In

 yi \+ vi sin\(γi\)∆t 

other words, except directly learning the state-action mapping, f \(si, ui\) =

t

t

t





t

t

\(1\)

 vi \+ ai∆t



IRL infers the form of reward weight and optimizes maneuvers



t

t



through it. 

γi \+ ωi∆t

t

t

Because of the aforementioned advantages, IRL has been where f denotes the uni-cycle model, si = \[xi, yi, vi, γi\]T

widespread in many fields. Among many IRL algorithms, the t

t

t

t

t

denotes the state of a vehicle, \(xi, yi\) maximum entropy method stands out due to its ability to t

t , vi

t and γi

t are the

position, speed, and yaw angle of vehicle i at t frame, address the ambiguity. A human driver follows the stochastic respectively. 

policies that may lead to a different distribution of candi-Furthermore, in a non-cooperative game, a discreet trade-off date decisions \[16\]. The principle of maximum entropy was between the consequence of each action and the rival’s possi-introduced to choose the distribution that does not exhibit ble corresponding response will be made in every ∆t = 0.1s. 

any additional preference. Therefore, ambiguity was resolved. 

Finally, after taking every action in Table II into account, Generally, the probability of a trajectory is proportional to the the best response to cope with the rival’s each action can exponential of the reward in Eq. 4. 

be concluded. After each player strives for the best response 1

1

which results in the lowest cost or the highest reward, Nash P \(ζ|θ\) =

eR\(ζ\) =

eθT fζ

\(4\)

Z\(θ\)

Z\(θ\)

equilibrium will be accomplished. In Nash equilibrium, none of the players are able to acquire a lower cost by unilaterally where P \(ζ|θ\) is the probability of trajectory ζ, R\(ζ\) is the adjusting their actions. Therefore, the mathematical definition corresponding reward function of expert trajectory ζ which is of Nash equilibrium is defined by

the multiplication of reward weight vector θT and trajectory feature vector fζ, and Z\(θ\) is the partition function. 

R\(ui∗ , u−i∗ \) ≥ R\(ui, u−i∗ \)

When confronted with a continuous or high-dimensional t

t

t

t

\(2\)

space problem, the partition function may fail to converge. 

where R is the reward function, ui∗

t

and u−i∗

t

are the action

However, in a finite horizon problem, the reward weights performed by player i and players other than player i when in maximizing entropy are certain to be convergent \[36\]. 

game achieves Nash equilibrium at t frame, uit is arbitrary Therefore, limited feasible trajectories were generated and action of player i in action set U . 

Eq. 4 could be rewritten as follows. 

In some cases, Nash equilibrium is not always the optimal solution \[17\]. However, we do not regard this as a drawback, eθT fζ

P \(ζ|θ\) =

\(5\)

but as a proxy for the limitation of human reasoning and the PM

eθT f˜ζ

i=1

consequence of being absolutely rational. As in the real-world, not all games have a happy ending. 

where f˜ is the feature of feasible trajectory ˜

ζ, and M is the

ζ

Here we considered a reward consisting of efficiency, com-finite feasible trajectory. By this approximation, probability is fort, and safety, denoted by distance to the destination, offset to much easier to calculate. 

the expected path, and Time to Collision \(TTC\), respectively. 

The kernel of IRL is to adjust the weights of reward function Then, the reward of each possible action can be calculated by to yield a maneuver that matches with expert demonstrations. 

si

To fulfill that purpose, the likelihood of expert demonstrations t, uit, and u−i

t

in Eq. 3. 

should be maximized by adjusting θT . 

1

R\(si, ui, u−i\) = \[−di − oi \+

\]θT

t

t

t

t

t

\(3\)

X

T T Cit

max L\(θ\) = max

logP \(ζ|θ\)

\(6\)

θ

θ

ζ∈D

where dit is the distance between the contemporary position of vehicle i and its destination at t frame, oi where L\(θ\) is the likelihood function and also the objective t is the offset to

the expected path, T T Ci

function, D = \{ζ

is the trajectory set containing N expert t is the time to collision, and θT is

i\}N

i=1

driver’s decision-making preference weight. 

demonstrations which are the real-world human trajectories we Therefore, combining Eq. 1 with Table

II, six feasible

screened and clustered before. 

trajectories can be generated in each frame. Max entropy Substituting P \(ζ|θ\) in Eq. 6 with Eq. 5, L\(θ\) can be IRL was then introduced to quantify the difference between rewritten as

feasible trajectories and expert demonstrations to calibrate M

HVs different decision-making preferences. 

X

X

L\(θ\) =

\[θT fζ \+ log

eθT f˜ζ\]

\(7\)

ζ∈D

i=1

D. Decision-making Preference Calibration by IRL

This function is convex and gradient-based optimization is After dividing drivers into groups and generating feasible used for solving optimal reward weight. The gradient can be trajectories through non-cooperative game. IRL was intro-written as the difference between the expert demonstrations fζ

duced to excavate inherent characteristics that influence the and the feasible trajectories f˜ in Eq. 8. 

ζ

6

TABLE III

IRL CALIBRATION RESULTS

M

X

X

eθT fζ

∇θL\(θ\) =

\[f \(ζ\) −

\]

\(8\)

Reward weights

PM

eθT f˜ζ

Type

ζ∈D

i=1

i=1

efficiency

comfort

safety

Aggressive HV

8.33

1.56

3.69

L2 regularization is introduced to the likelihood function in Normal HV

8.2

1.72

5.7

order to prevent overfitting and λ > 0 is the regularization Conservative HV

7.79

2.1

8.44

parameter. Thus, Eq. 7 and Eq. 8 can be rewritten as M

driving comfort and safety, leading to conservative decisions. 

X

X

L\(θ\) =

\[θT fζ \+ log

eθT f˜ζ\] − λθ2

\(9\)

The reward weights of normal drivers were in the middle ζ∈D

i=1

range, these drivers do not have an over preference and try to balance efficiency, comfort, and safety while driving. 

M

In conclusion, the above results were in line with real-X

X

eθT f

∇

ζ

θ L\(θ\) =

\[f \(ζ\) −

\] − 2λθ

\(10\)

world expectations. On the other hand, they also confirmed PM

eθT f

ζ∈D

i=1

i=1

˜

ζ

that our definition of the cluster centers in subsection A was Then, the pseudocode of maximum entropy IRL is summa-reasonable. After calibrating different drivers’ preferences on rized in Algorithm. 1. Based on the clustering results, three decision making, the action corresponding to Nash equilibrium groups of expert demonstrations were respectively trained can be inferred and the next state of vehicle can be calculated by IRL to calibrate the preference of different drivers’ de-by substituting this action into Eq. 1. 

cision. Feasible trajectories and corresponding features can So far, we have modeled the heterogeneous HVs for estab-be obtained by utilizing non-cooperative game and Eq. 3, 

lishing a mixed environment. Next, we designed a cooperative respectively. 

driving framework that enables CAVs to not only interact, but also actively coordinate with other vehicles, advancing traffic efficiency and safety. 

Algorithm 1: Maximum entropy inverse reinforcement learning. 

IV. COOPERATIVE DECISION MAKING AND TRAJECTORY

Data: Three expert demonstrations dataset, learning PLANNING FOR CAVS

rate α, regularization parameter λ, training Unlike the unpredictable and uncontrollable of HVs’ trajec-epoch E

tories, CAVs are capable of cooperating and even coordinating Result: Optimized reward weights θT , including with others to nudge the system to greater efficiency. As efficiency, comfort, and safety

shown in Fig. 2, the cooperative driving algorithm for CAVs is 1 Initialize θT ← N \(0, 0.05\); 

introduced in three subsections. Level-k game and cooperative 2 Initialize buffer B ← \[\]; 

game are introduced in subsection A and subsection B to 3 Compute human features f ← PM

f

i=1

ζ ; 

search for an optimal k-allocation solution refers to the highest 4 while ζi ∈ D do

system efficiency. In subsection C, Lattice planner is used for 5

Generate feasible trajectories f˜; 

ζ

planning an optimal and collision-free trajectory based on k-6

Calculate features of ˜

ζ; 

allocation results. 

\+

7

Add features to buffer B ← ˜

ζ; 

8

i ← i \+ 1; 

A. Resolving Multiple Traffic Streams Conflict by Level-k 9 end

Game

10 while epoch < E do

Level-k game assumes that players generate strategies based 11

Calculate the likelihood function of each sample in on their depths of reasoning. In addition, k can also be defined buffer B; 

as ROW \[7\], driving style \[3, 6\]. Here, considering the absence 12

L\(θ\) = P \[θT f

of traffic lights will cause multiple traffic streams to intersect ζ \+ log PM

eθT f˜ζ\]; 

i=1

ζ∈D

in time and space, we denoted k as ROW to resolve conflicts. 

13

Calculate the gradient ∇θL\(θ\); 

In the case of trajectory planning, level-0 drivers regard 14

Update reward weights θ ← θ \+ α∇θL\(θ\); other vehicles as static obstacles and plan their trajectory 15

θ∗ ← θ; 

on this basic assumption. Then level-1 drivers will infer the 16 end

planning trajectory of level-0 drivers and then plan their trajectories while avoiding collision with level-0 trajectory. By that analogy, all drivers may obtain the expected paths based After training, the reward weights of different driver groups on their depth of reasoning. Therefore, the expected path of can be calibrated through maximizing entropy and iterating, vehicle i, denoted as ζ

shown in Table III. 

i, can be calculated from

As in Table III, the aggressive driver group possessed ζ

, ζ

the highest efficiency value, and lowest safety and comfort i\(k\) = max R\(k, siu

j \(k − 1\)\)

\(11\)

value, indicating their preference for passing at a high speed where ζi\(k\) is the trajectory of vehicle i with k level, and the and more willingness to detour rather than stop and wait. 

trajectory is determined by maximizing the reward function Meanwhile, conservative drivers were more concerned about R. 

7

In this paper, our CAV is free to generate its depths of than before. Finally, group rationality means that the system reasoning to maximize the system’s overall efficiency. In goals are the summation of individual rewards, i.e., addition, when multiple traffic streams intersect, a unique k will be assigned to each stream to prevent collision or X

O =

R\(Vi\)

\(14\)

deadlock. Researchers also pointed out that normally reasoning i∈N

depths of human are less than or equal to 2 according to where O is the system goal of a cooperative game and the sum

\[6, 37\]. Therefore, to prevent CAVs from behaving unreason-of individual reward at the same time. System goals are often ably, traffic streams with k greater than 2 were corrected to k in the form of minimum overall delay or maximum efficiency equal to 2 based on the limited human reasoning depths. 

such as moving faster or further. 

Level-k game provided a theoretical basis for the orderly Through experiments, we finally chose the inverse distance passage of vehicles. Though unsignalized intersections failed to the destination to represent system efficiency as it has shown to resolve conflict from the temporal dimension, countable a better performance than other surrogate variables. Therefore, streams lead to finite k-allocation solutions. By optimizing the objective function O is as follows. 

the k-allocation of streams, system optimum can be achieved and the conflict can be resolved. Therefore, cooperative game X

X

1

was utilized to quantify the system performance of each k-O\(k\) = max

\(15\)

di,j

allocation solution. 

i∈lane j∈group

where O\(k\) is the value of objective function under a certain k-allocation solution, d

B. Searching Best k-allocation through Cooperative Game i,j is the average distance to the destination of the expected path belonging to vehicles in i lane Reservation-based control methods such as First Come and j group. Each k-allocation solution will lead to a different First Serve \(FCFS\) and Batch-strategy have a long history di,j. 

and are widely used due to their succinct form \[19\]. FCFS

It should be noted that this distance is not the current control simply assumes that ROW is proportionate to the distance to destination but the average distance to destination entry order and firstly served as a reservation mechanism for of the planning trajectory under k-level. The value of di,j can autonomous vehicles ascend to Dresner and Stone \[38\]. Batch-be achieved by giving a specific k to the Lattice planner, which strategy believed that intersections will be more efficient from will be discussed in the next subsection. 

a capacity of view if served in batches. Therefore, vehicles At the same time, we were aware that going straight vehicles in each stream are grouped into batches and served at FCFS

and turning vehicles have different impacts on the system. 

principle then. While these methods reckon without system Therefore, coefficients of distance to the destination should efficiency and organize ROW merely depend on their order of be various and Eq. 15 can be rewritten as entry. 

Therefore, cooperative game was combined with the aforeX

1

X

α

mentioned level-k game to optimize system efficiency. Differ-max\(

\+

\)

\(16\)

ing from non-cooperative game that regards other participants d

d

0

j∈group

gs,j

0

0

j ∈group

turn,j

as rivals and emphasizes maximizing individual profit. Cooper-where α represents the weight of turning vehicles relative ative game refers to participants uniting as several coalitions to going straight vehicles, d

and trying to maximize system goals through collaborating gs and dturn are the distance

to destination of going straight vehicle and turning vehicle, with other coalitions. Meanwhile, cooperative game should respectively. Then, an investigation was carried out to unify meet the requirement of superadditivity, individual rationality, the dimension of d

and group rationality \[39, 40\]. 

gs and dturn. 

For the purpose of investigating the real-world relationship Superadditivity refers to the inequality of the reward of between going straight vehicles and turning vehicles, the in-coalitions and the total reward of separate individual vehicles. 

teractions between going straight vehicles and turning vehicles It can be expressed by

were further extracted based on the XXJH data. Next, a logistic model was introduced to explore the relation between initial R\(Vi\) \+ R\(Vj\) ≤ R\(Vi ∪ Vj\)

\(12\)

distance to the destination and the actual order of passage. 

After calibrating by interaction data, results are presented as where R\(Vi\) is the reward function of vehicle i, and Vi ∪ Vj follows. 

stands for the coalitions consists of vehicle i and vehicle j. 

In addition, individual rationality should satisfy the following p

inequality. 

ln

= 0.0925dturn − 0.1332dgs \+ 2.35

\(17\)

1 − p

where p is the probability of going straight vehicle pass first. 

R\(Vi\) ≤ Ri\(Vi ∪ Vj... ∪ Vn\)

\(13\)

The relationship between p and dturn, dgs can be shown in where R

Fig. 3. 

i\(Vi ∪ Vj ... ∪ Vn\) represents the individual reward of vehicle i under cooperative game that n vehicles are united as Substituting p = 0.5 into Eq. 17, it yields that a coalition. This inequality stipulates that each vehicle could obtain a higher reward when controlled with cooperative game dturn = 1.44dgs − 25.4

\(18\)



8

path and obstacles. It mainly consists of coordinates trans-

�

forming, sampling, and curvature polynomials fitting. 

0.8

In the coordinates transforming step, the corresponding state in Frenet coordinates was transformed according to the 0.4

initial state in Cartesian coordinates. Then, planning horizons and maximum steering angles were sampled. For improving 0

computation speed, initial sampling space was relatively small. 

50

10

When it comes to no available solution, sampling space will 30

30

�

�

be enlarged. Simulation will be shut down and print out no

����

10

50

��

solution if there are still no available solutions. When it comes

�

to multiple solutions, optimal trajectory was determined by 0

0.3

0.6

0.9 1

reward. Finally, after sampling, curvature polynomials were used to generate the entire trajectory between the start point Fig. 3. 

Logistic relation of distance to destination and probability of going and end point. 

straight vehicle pass first. 

To control variables, the composition of rewards and reward weights for CAV was designed to be consistent with normal HV. The difference is HVs made decisions by searching Through the coefficients of dturn and dgs, a turning vehicle Nash equilibrium in non-cooperative game and then generated will cost more to maintain equality with a going straight trajectory through vehicle dynamics while CAVs replaced vehicle. This conclusion is consistent with relevant law which these steps with the NCL game we proposed and Lattice stipulated that turning vehicles should give precedence to planner respectively. Algorithm. 2 describes the procedure of going straight vehicles when in conflict at an intersection. 

CAVs’ cooperative decision making and trajectory planning. 

In addition, by substituting Eq. 16 into Eq. 18, the objective function is derived as follows. 

Algorithm 2: Cooperative decision making and trajec-X

1

X

1

max\(

\+

\)

tory planning for CAVs. 

d

1.44d

\(19\)

0 − 25.4

j∈group

gs,j

0

0

j ∈group

gs,j

Input: Vehicle’s state sit, traffic stream number lane, number of vehicles in each stream group Through the logistic model, the impacts of going straight Output: Vehicle decision-making depths k and next vehicles and turning vehicles to the system were normalized. 

state si

Social norms that going straight vehicle possess higher pri-t\+1 according to planning trajectory

; 

ority than turning vehicle at the intersection were also taken 1 Calculate all possible k-allocation solution A ← A2

lane

into consideration subtly during this normalization. Here, we 2 Initialize objective function list of cooperative game O; named it normalized cooperative game. 

3 foreach a ∈ A do

As indicated above, in cooperative game, vehicles will 4

Evaluate each a performance; 

unite as several coalitions. While maximizing system’s overall 5

foreach stream ∈ lane do

efficiency is the same goal that all coalitions share. This pro-6

foreach i ∈ group do

cess can be achieved by adjusting one’s strategy to influence 7

Calculate average distance to destination dj other coalitions. Differing from the above non-cooperative through Lattice\(k\); 

game where influence has been seen as a discrete action-8

Normalize dgs,j ← dj; 

action mapping. A trajectory-trajectory strategy mapping was 9

Calculate objective function of this solution needed for cooperative game because of the form of the Os\+ = dgs,j; 

objective function. To calculate Eq. 19, each vehicle’s planning 10

end

trajectory should be inferred according to the concept of level-11

end

\+

k game and Lattice planner. 

12

Add to O ← Os

Therefore, by combining normalized cooperative game with 13 end

level-k game, k-allocation solution that led to optimal system 14 Find the best k-allocation solution max O; efficiency can be easily obtained by enumerating finite k-15 Get each vehicle k and plan its next state sit\+1 through allocation solutions. In addition, a trajectory planner was Lattice\(k\) and best k-allocation solution; needed to generate trajectories based on the concept of level-k game to evaluate each k-allocation solution’s performance. 

Hence the Lattice planner was introduced. 

Steps in Algorithm 2 show the whole process of CAV cooperative decision making and trajectory planning. It will repeat C. Planning Optimal Trajectory with Lattice Planner every ∆t = 0.1s until the simulation duration is reached. After Lattice planner is a well-accepted motion planner to gen-finishing the modeling of HVs and CAVs, several experiments erate optimal and collision-free trajectory according to expect were conducted to validate our cooperative driving framework. 

9

Fig. 4. 

Simulation environment. 

Fig. 5. 

Average travel speed comparison of control method under different lane volume. 

V. SIMULATION VALIDATION

All simulations lasted 2 minutes, which is 1200 frames. 

After simulation, trajectories of all vehicles were recorded for A. Simulation Design

further evaluation. 

To evaluate the performance of the proposed algorithm framework, an isolated four-approach unsignalized intersection B. Case1: Comparison of Different Control Methods in Fig. 4 was used as simulation environment. All approaches For the purpose of evaluating the results of different control were 40 meters long and each approach contained one or two methods. Simulations were conducted in a full CAV environ-traffic streams as in Fig. 4. 

ment at first. Average travel speed was applied to evaluate Although we simplified the number of traffic streams, system efficiency. 

nearly ten conflicts still exist according to the topological Fig. 5 shows the average travel speed under different lane relationship. Except for various conflict points, simulation volumes. Clearly, it presented a negative relationship with lane environment also included confluence point and split-flow volume, which is consistent with basic cognizance about the point. This resulted in merging and diverging behaviors which relationship of speed and volume according to Greenshields further produced substantial impacts on vehicle behavior in et al. \[42\]. In addition, travel speed decreased dramatically mixed traffic \[41\]. Together with high-density traffic flow and under FCFS control when lane volume increased. But when heterogeneous HVs, we believe this unsignalized intersection lane volume was relatively low \(under 200veh/h\), FCFS con-is complicated enough for examining our algorithm frame-trol even outperform Batch-strategy because grouping vehicles work. 

into batches in low density may add unnecessary steps that In addition, preferences affect not only the drivers’ deci-lead to low efficiency. 

sions, but also their initial speed and target speed. Therefore, As seen in Fig. 5, CL game and NCL game showed a higher according to our prior knowledge based on XXJH data, HVs’

travel speed than reservation-based control method at all lane initial speed was designed same as the average speed, and volumes. Proving that the combination of cooperative game target speed same as the maximum speed. For example, and level-k game is effective from the system point of view. 

according to Table I, an aggressive driver will enter the simu-Also, the gap between CL game and NCL game narrowed as lation environment at speed of 6.3m/s and expect to travel at lane volume rose. This phenomenon attributed to the number speed of 7m/s if possible. In order to examine the effectiveness of vehicles in conflicting streams became more significant than and robustness of our framework, three simulation cases were the types of streams \(turning stream or going straight stream\). 

conducted in this paper. 

Therefore, with the increase in lane volume, the effect of First of all, we compared NCL game and CL game \(NCL

normalization was subdued. 

game without normalization\) with reservation-based control Furthermore, Fig. 6 shows a case that eight vehicles exist methods under different traffic densities to evaluate the rock-in the simulation environment at the same time under Batch-bottom control method we proposed. FCFS and Batch-strategy strategy control and NCL game. Fig. 6 \(a\) depicts their initial were used as the representative of reservation-based method position and the numbers beside vehicles stand for the enter based on \[19\]. Next, in order to verify the effectiveness of sequence of a vehicle. Fig. 6 \(b\)-\(c\) exhibits the process of the proposed cooperative driving algorithm, simulation was vehicles’ position iterated over time. Owing to Batch-strategy conducted under different CAV rates of penetration. Finally, serving vehicles as batches, V7 \(stands for vehicle 7 in the differing from regarding all human drivers make normal de-figure\) obtained the same ROW as V3 and passed in a queue. 

cisions, we introduced drivers with different personal prefer-However, Batch-strategy still follows the principle of FCFS

ences to our simulation environment based on IRL calibration which led to V1 passed first even if there was only one vehicle results in Table III. 

in its stream. This phenomenon has caused other streams





10

**CAV**

T=0Ts=0s

Batch-strategy

/s\)

NCL game

1

5

6

8

4

2

3

Total Delay\(s\)

7

Average Travel Speed\(m

Time\(s\)

\(a\)

\(d\)

Batch-strategy

T=5s

T=15s

T=25s

4

5

6

8

3

7

5

6 8

7

5

6 8

4

2

3

1

7

2

\(b\)

Fig. 7. 

Average travel speed and delay under different ROP. 

NCL game

T=5s

T=15s

T=25s

T=5s

T=15s

1

1

4

5

6

8

6

8

7

4

3

3

4

7

1

Batch-strategy as control methods. Each control method was 7

2

conducted under three ROP, i.e., 100%, 60%, and 20%. 

Average travel speed and total delay were calculated and \(c\)

standardized in Fig. 7. There is a clear trend when ROP

rose, average travel speed increased and total delay decreased, Fig. 6. 

Interaction case: comparison of NCL game and Batch-strategy: representing the improvement of system efficiency. In addition, \(a\) shows the initial position of the vehicles; \(b\)-\(c\) show three subsequent when CAV was controlled with NCL game, system showed steps of CAVs control with Batch-strategy and NCL game, respectively. \(d\) summarizes the average travel speed and total delay of this interaction case; better performance at all ROP. From another perspective, the numbers next to the vehicles refer to the order in which they enter the minimum average travel speed when using NCL game control simulation environment. 

was even higher than the maximum travel speed using Batch-strategy control which confirmed that high-density continuous traffic flow indeed amplified the gap between NCL game which had conflict with V1 have to recede no matter how many and Batch-strategy. Same conclusions can be applied to total vehicles were in that group, resulting in inefficiency. 

delay, proving that NCL game we proposed is superior to the There is a clear trend that when controlled with NCL

traditional reservation-based method and is suitable for the game, vehicles in Approach 2 possessed the highest ROW, mixed traffic flow containing both CAVs and HVs. 

and vehicles in Approach 3 were the second after screening all The above analysis was aimed at evaluating the efficiency possible k-allocation solutions and finding the most efficient of intersection. Safety should also be noted because of its one. Fig. 6 \(d\) shows the average travel speed of the whole dependency on people’s trust in CAV which is currently system at different simulation times. Obviously, NCL game a major obstacle to the popularization of CAV. Hence the we proposed brought a higher efficiency than Batch-strategy. 

PET was introduced to evaluate our algorithm from a safety In addition, the total delay of the whole intersection is almost perspective. Initially, PET was introduced by Allen et al. \[43\]

half of controlled by Batch-strategy. It should be noted that as the time between the moment when the front vehicle leaves this gap will ulteriorly amplify if vehicles ceaselessly enter conflict area or invasion line and the rear vehicle reaches the simulation environment. 

conflict area or invasion line. The distribution of PET under Therefore, considering that high-density continuous traffic different ROP and control methods is shown in Fig. 8. 

flow causes more trouble for CAV trajectory planning and According to the box plots above, the distribution of PET

more challenge to the whole system. In the following exper-became more discrete when ROP decreased, which indicates iments, we fixed lane volume at 300 veh/h to evaluate the that interactions between vehicles were more chaotic and suitability of our work under mixed traffic. 

inefficient. At the same time, the decline of ROP also led to higher maximum PET and average PET, which symbolizes a longer interval between vehicle’s passage based on the C. Case2: Experiment under Different ROP

concept of PET. In other words, as the proportion of HV

CAVs are expected to operate in traffic with HVs long rose, interactions became conservative and hazardous. Thus, into the future. Therefore, interactions between CAV and HV

deadlocks were more likely to occur. 

should be fully studied under different circumstances. Building Another line of evidence came from minimum PET, which on the experiment above, we evaluated the intersection system indicates the most dangerous interaction case during the whole operation status under different ROP with NCL game and simulation duration. Fig. 8 shows a positive correlation be-

11

D. Case3: Heterogeneous Human Driver Involved We conducted three experiments at 60% ROP at first. 

Instead of generating all HVs make normal decisions while interacting with other vehicles like in Case 2. Half of HVs were replaced by aggressive type or conservative type, which may produce more unpredictable behavior. Total delay and the distribution of average travel speed are shown in Fig. 10. 

Fig. 10 shows that when there is only normal type HV mixed with CAVs in simulation environment, average travel speed was significantly higher than aggressive HV or conservative HV involved. In addition, when 20% of normal HV was replaced by aggressive HV, though aggressive HV has a 100% ROP60% ROP20% ROP 100% ROP60% ROP20% ROP

NCL 

NCL 

NCL 

Batch

Batch

Batch

higher initial speed and target speed as we appointed in game

game

game

strategy strategy strategy

subsection A, the proportion of low-speed \(velocity <2.4m/s\) vehicles increased on the contrary. Not to mention that the Fig. 9. 

Composition of conflict under different ROP. 

proportion of low-speed vehicles will increase sharply from 22% to 67% if 20% normal vehicles were replaced by 20%

conservative vehicles. Though little difference was found in terms of total delay between the three experiments, the above tween ROP and minimum PET, proving that increasing the experiments yet emphasized the difficulty when interacting number of our CAV is of help to improve system safety. 

with heterogeneous HVs whose decisions are fickle. 

Qi et al. \[44\] determined an appropriate threshold of Whereas these findings only prove our CAV is capable PET from conflict data. Dividing conflict into four sections. 

of interacting with heterogeneous HVs because no collision PET<0.7s means a serious conflict, 0.7s ≤PET<1.31s means or deadlock happened, experiments should be carried out a general conflict, 1.31s ≤PET<2.25s means a slight conflict, to examine if our CAV can improve system efficiency to and PET≥ 2.25s means a potential conflict. Furthermore, we testify their ability of coordinating with heterogeneous HVs. 

calculated and visualized the conflict composition in Fig. 9

Therefore, a real-world based environment was established based on above partition. 

according to the HV composition in XXJH data. Finally, the Fig. 9 shows that interaction was either slight conflict or experimental group consisted of 13% aggressive HV, 41%

potential conflict in all CAV environment \(100% ROP\). What normal HV, and 46% conservative HV. In the control group, is more, the proportion of serious conflict and general conflict normal HVs were replaced by the CAV we designed \(note increased with the decrease of ROP. 

that they share the same initial speed, target speed, reward Through average travel speed, total delay, and PET, we composition, and reward weights\). 

have proven that the CAV we designed has the ability to According to Fig. 11, after replacing normal HV with our nudge the intersection system toward greater efficiency and CAV, system has been improved in all aspects. Specifically, safety. However, in addition to high-density and mixed traffic, average travel speed of the intersection system increased by human drivers possess different decision-making preferences 0.3m/s and the proportion of high-speed vehicles increased. 

that leads to heterogeneous traffic. Therefore, interaction with The more striking change was a 42.5% reduction in total heterogeneous HVs involved will fortify the persuasion of our delay which confirmed the robustness and the superiority of CAV algorithm framework. 

our CAV algorithm framework under a heterogeneous mixed

12

Fig. 12. 

Distribution of PET based on XXJH vehicle composition. 

Fig. 13. 

Interaction case: comparison of normal HV and CAV involved. \(a\) shows the initial position of the vehicles and the colors of vehicles depict their type; \(b\) shows the six subsequent steps of the interaction that only HVs participant; \(c\) shows the corresponding steps after replacing normal HVs with CAVs; \(d\) summarizes the average travel speed and total delay of this interaction case; numbers next to the vehicles refer to the order in which environment. 

they enter the simulation environment. 

Similar to Case2, we calculated the PET of the interactions during the simulation duration. As seen in Fig. 12, after replacing normal HV with CAV, distribution of PET became more concentrated and minimum PET increased, indicating able to actively induce the aggressive vehicle to slow down that our CAV has the ability to properly organize other vehi-by showing a willingness to pass first \(by comparing the cles’ passage and improve driving safety. We further carried a status of Fig. 13 \(b\)-\(c\) at T = 5s and T = 10s\). This interaction case to visualize the different system evolutionary was attributed to our game-based cooperative method. Their processes of normal HV and CAV involved. 

cooperative behaviors were emergent rather than generated by From the comparative analysis of Fig. 6 \(d\) and Fig. 13

some predefined protocol which gave us the potential to apply \(d\), it can be found that the introduction of heterogeneous to more complex scenarios. Although average travel speed of HVs has led to a lower average travel speed and higher total the whole intersection was slightly lower at first based on delay which brought more challenge to our cooperative driving Fig. 13 \(d\), speed at later simulation duration and total delay algorithm framework. Fig. 13 \(b\)-\(c\) shows the process of are significantly better than without CAVs participation. So interaction in detail. In all HV environment, aggressive V

far, the effectiveness and robustness of our CAV cooperative 1

pursued his own benefits and managed to pass as fast as driving framework under various environment have been tes-possible. This phenomenon led to a higher average travel speed tified. 

of the system at the beginning of interaction. While average In conclusion, three simulation cases were conducted for travel speed plummeted after the aggressive vehicle left the the verification and validation of our cooperative driving intersection due to its hoggish maneuver that may harm other framework. The simulation results show that with the designed vehicles in long-range. 

framework, CAVs are capable of coordinating with hetero-After we replaced normal HVs with CAVs, CAVs were geneous vehicles in the high-density, mixed, unsignalized

13

intersection. Besides, as the proportion of CAV increased, the

\[13\] K. Yu, L. Lin, M. Alazab, L. Tan, and B. Gu, “Deep learning-based efficiency and safety of the intersection system improved. 

traffic safety solution for a mixture of autonomous and manual vehicles in a 5g-enabled intelligent transportation system,” IEEE transactions on intelligent transportation systems, vol. 22, no. 7, pp. 4337–4347, 2020. 

VI. CONCLUSION

\[14\] R. Yao, W. Zeng, Y. Chen, and Z. He, “A deep learning framework for modelling left-turning vehicle behaviour considering diagonal-crossing With the combination of normalized cooperative game and motorcycle conflicts at mixed-flow intersections,” Transportation re-level-k game, a cooperative driving framework is proposed search part C: emerging technologies, vol. 132, p. 103415, 2021. 

for CAVs to address the driving conflict in the high-density, 

\[15\] L. Bi, G. Gan, J. Shang, and Y. Liu, “Queuing network modeling of driver lateral control with or without a cognitive distraction task,” IEEE

mixed, unsignalized intersection. Differing from reservation-Transactions on Intelligent Transportation Systems, vol. 13, no. 4, pp. 

based control methods, the proposed NCL game theoretic 1810–1820, 2012. 

approach is capable of cooperating and even actively coordi-

\[16\] Z. Huang, J. Wu, and C. Lv, “Driving behavior modeling using naturalistic human driving data with inverse reinforcement learning,” IEEE

nating with other vehicles. Namely, besides the cooperation Transactions on Intelligent Transportation Systems, 2021. 

between CAVs, CAVs can collaborate with heterogeneous

\[17\] I. V. Chremos, L. E. Beaver, and A. A. Malikopoulos, “A game-theoretic HVs. Three simulation cases are conducted for verification analysis of the social impact of connected and automated vehicles,” in 2020 IEEE 23rd International Conference on Intelligent Transportation and validation, including the comparative analysis with dif-Systems \(ITSC\). 

IEEE, 2020, pp. 1–6. 

ferent methods, the case study under different ROP and the

\[18\] S. Mariani, G. Cabri, and F. Zambonelli, “Coordination of autonomous interaction analysis with heterogeneous HVs. The performance vehicles: taxonomy and survey,” ACM Computing Surveys \(CSUR\), vol. 54, no. 1, pp. 1–33, 2021. 

of the intersection system is analyzed through average travel

\[19\] C. Yu, W. Sun, H. X. Liu, and X. Yang, “Managing connected speed, total delay, and PET. Experiment results indicate that and automated vehicles at isolated intersections: From reservation-to the proposed cooperative driving framework is capable of optimization-based methods,” Transportation research part B: method-ological, vol. 122, pp. 416–435, 2019. 

confronting complex, mixed traffic scenarios and therefore

\[20\] J. Rios-Torres and A. A. Malikopoulos, “A survey on the coordination nudging system to greater efficiency and safety. 

of connected and automated vehicles at intersections and merging at highway on-ramps,” IEEE Transactions on Intelligent Transportation Systems, vol. 18, no. 5, pp. 1066–1077, 2016. 

REFERENCES

\[21\] D. Zhou, Z. Ma, X. Zhao, and J. Sun, “Reasoning graph: A situation-

\[1\] W. Schwarting, A. Pierson, J. Alonso-Mora, S. Karaman, and D. Rus, aware framework for cooperating unprotected turns under mixed con-

“Social behavior for autonomous vehicles,” Proceedings of the National nected and autonomous traffic environments,” Transportation Research Academy of Sciences, vol. 116, no. 50, pp. 24 972–24 978, 2019. 

Part C: Emerging Technologies, vol. 143, p. 103815, 2022. 

\[2\] C. F. Camerer and E. Fehr, “When does” economic man” dominate

\[22\] H. Xu, Y. Zhang, L. Li, and W. Li, “Cooperative driving at unsignal-social behavior?” science, vol. 311, no. 5757, pp. 47–52, 2006. 

ized intersections using tree search,” IEEE Transactions on Intelligent

\[3\] R. Tian, S. Li, N. Li, I. Kolmanovsky, A. Girard, and Y. Yildiz, “Adap-Transportation Systems, vol. 21, no. 11, pp. 4563–4571, 2019. 

tive game-theoretic decision making for autonomous vehicle control

\[23\] D. Carlino, S. D. Boyles, and P. Stone, “Auction-based autonomous at roundabouts,” in 2018 IEEE Conference on Decision and Control intersection management,” in 16th International IEEE Conference on \(CDC\). 

IEEE, 2018, pp. 321–326. 

Intelligent Transportation Systems \(ITSC 2013\). IEEE, 2013, pp. 529–

\[4\] C. Xu, W. Zhao, L. Li, Q. Chen, D. Kuang, and J. Zhou, “A nash q-534. 

learning based motion decision algorithm with considering interaction to

\[24\] H. Vu, S. Aknine, and S. D. Ramchurn, “A decentralised approach to traffic participants,” IEEE Transactions on Vehicular Technology, vol. 69, intersection traffic management.” in IJCAI, 2018, pp. 527–533. 

no. 11, pp. 12 621–12 634, 2020. 

\[25\] C.-L. Huang and G. Nitschke, “Evolutionary automation of coordinated

\[5\] M. Garzón and A. Spalanzani, “Game theoretic decision making for au-autonomous vehicles,” in 2020 IEEE Congress on Evolutionary Com-tonomous vehicles’ merge manoeuvre in high traffic scenarios,” in 2019

putation \(CEC\). 

IEEE, 2020, pp. 1–7. 

IEEE Intelligent Transportation Systems Conference \(ITSC\). 

IEEE, 

\[26\] T. Litman, Autonomous vehicle implementation predictions. 

Victoria

2019, pp. 3448–3453. 

Transport Policy Institute Victoria, BC, Canada, 2017. 

\[6\] R. Tian, N. Li, I. Kolmanovsky, Y. Yildiz, and A. R. Girard, “Game-

\[27\] M. Wang, S. P. Hoogendoorn, W. Daamen, B. van Arem, and theoretic modeling of traffic in unsignalized intersection network for R. Happee, “Game theoretic approach for predictive lane-changing autonomous vehicle control verification and validation,” IEEE Transac-and car-following control,” Transportation Research Part C: Emerging tions on Intelligent Transportation Systems, 2020. 

Technologies, vol. 58, pp. 73–92, 2015. 

\[7\] H. Wang, Y. Li, and H. V. Zhao, “Performance analysis of road

\[28\] D. Sadigh, N. Landolfi, S. S. Sastry, S. A. Seshia, and A. D. Dragan, intersections based on game theory and dynamic level-k model,” 

“Planning for cars that coordinate with people: leveraging effects on in 2020 IEEE Intl Conf on Parallel & Distributed Process-human actions for planning and active information gathering over human ing with Applications, Big Data & Cloud Computing, Sustainable internal state,” Autonomous Robots, vol. 42, no. 7, pp. 1405–1426, 2018. 

Computing & Communications, Social Computing & Networking

\[29\] S. Vaskov, S. Kousik, H. Larson, F. Bu, J. Ward, S. Worrall, M. Johnson-

\(ISPA/BDCloud/SocialCom/SustainCom\). IEEE, 2020, pp. 1112–1119. 

Roberson, and R. Vasudevan, “Towards provably not-at-fault control of

\[8\] H. Yu, H. E. Tseng, and R. Langari, “A human-like game theory-based autonomous robots in arbitrary dynamic environments,” arXiv preprint controller for automatic lane changing,” Transportation Research Part arXiv:1902.02851, 2019. 

C: Emerging Technologies, vol. 88, pp. 140–158, 2018. 

\[30\] M. Liu, Y. Wan, F. L. Lewis, S. Nageshrao, and D. Filev, “A three-level

\[9\] N. Li, I. Kolmanovsky, A. Girard, and Y. Yildiz, “Game theoretic game-theoretic decision-making framework for autonomous vehicles,” 

modeling of vehicle interactions at unsignalized intersections and appli-IEEE Transactions on Intelligent Transportation Systems, 2022. 

cation to autonomous vehicle control,” in 2018 Annual American Control

\[31\] Y. Ni, M. Wang, J. Sun, and K. Li, “Evaluation of pedestrian safety Conference \(ACC\). 

IEEE, 2018, pp. 3215–3220. 

at intersections: A theoretical framework based on pedestrian-vehicle

\[10\] S. Karimi and A. Vahidi, “Receding horizon motion planning for interaction patterns,” Accident Analysis & Prevention, vol. 96, pp. 118–

automated lane change and merge using monte carlo tree search and 129, 2016. 

level-k game theory,” in 2020 American Control Conference \(ACC\). 

\[32\] K.-T. Chen, H.-Y. W. Chen, and H.-Y. W. Chen, “Driving style clustering IEEE, 2020, pp. 1223–1228. 

using naturalistic driving data,” Transportation research record, vol. 

\[11\] P. Chu, Y. Yu, J. Yang, and C. Huang, “Understanding the mechanism 2673, no. 6, pp. 176–188, 2019. 

behind young drivers’ distracted driving behaviour based on sor theory,” 

\[33\] Y. Huang, D. J. Sun, and L.-H. Zhang, “Effects of congestion on drivers’

Journal of Transportation Safety & Security, vol. 14, no. 10, pp. 1655–

speed choice: Assessing the mediating role of state aggressiveness based 1673, 2022. 

on taxi floating car data,” Accident Analysis & Prevention, vol. 117, pp. 

\[12\] Z. el abidine Kherroubi, S. Aknine, and R. Bacha, “Novel decision-318–327, 2018. 

making strategy for connected and autonomous vehicles in highway

\[34\] Y. Rahmati, M. K. Hosseini, and A. Talebpour, “Helping automated on-ramp merging,” IEEE Transactions on Intelligent Transportation vehicles with left-turn maneuvers: a game theory-based decision frame-Systems, 2021. 

work for conflicting maneuvers at intersections,” IEEE Transactions on

14

Intelligent Transportation Systems, 2021. 

\[35\] C. Cheng, D. Yao, Y. Zhang, J. Li, and Y. Guo, “A vehicle passing model in non-signalized intersections based on non-cooperative game theory,” in 2019 IEEE Intelligent Transportation Systems Conference \(ITSC\). 

IEEE, 2019, pp. 2286–2291. 

\[36\] B. D. Ziebart, A. L. Maas, J. A. Bagnell, A. K. Dey et al., “Maximum entropy inverse reinforcement learning.” in Aaai, vol. 8. 

Chicago, IL, 

USA, 2008, pp. 1433–1438. 

\[37\] X. Wang, S. Zhang, and H. Peng, “Comprehensive safety evaluation of highly automated vehicles at the roundabout scenario,” IEEE Transactions on Intelligent Transportation Systems, 2022. 

\[38\] K. Dresner and P. Stone, “A multiagent approach to autonomous intersection management,” Journal of artificial intelligence research, vol. 31, pp. 591–656, 2008. 

\[39\] Z. Yang, H. Huang, G. Wang, X. Pei, and D.-y. Yao, “Cooperative driving model for non-signalized intersections with cooperative games,” 

Journal of Central South University, vol. 25, no. 9, pp. 2164–2181, 2018. 

\[40\] R. Xing, Z. Su, Q. Xu, N. Zhang, and T. H. Luan, “Secure content delivery for connected and autonomous trucks: A coalition formation game approach,” IEEE Transactions on Intelligent Transportation Systems, 2022. 

\[41\] J. Guo, S. Cheng, and Y. Liu, “Merging and diverging impact on mixed traffic of regular and autonomous vehicles,” IEEE Transactions on Intelligent Transportation Systems, vol. 22, no. 3, pp. 1639–1649, 2020. 

\[42\] B. Greenshields, J. Bibbins, W. Channing, and H. Miller, “A study of traffic capacity,” in Highway research board proceedings, vol. 1935. 

National Research Council \(USA\), Highway Research Board, 1935. 

\[43\] B. L. Allen, B. T. Shin, and P. J. Cooper, “Analysis of traffic conflicts and collisions,” Tech. Rep., 1978. 

\[44\] W. Qi, W. Wang, B. Shen, and J. Wu, “A modified post encroachment time model of urban road merging area based on lane-change characteristics,” IEEE Access, vol. 8, pp. 72 835–72 846, 2020. 


# Document Outline

+ I Introduction 
+ II Problem Statement and Cooperative Driving Framework 
+ III Reproducing Heterogeneous HV Decisions in Mixed Traffic  
	+ III-A Data Collection 
	+ III-B Drivers' Decisions Classification by K-means Cluster 
	+ III-C HVs' Feasible Trajectories Generation through Non-cooperative Game 
	+ III-D Decision-making Preference Calibration by IRL 

+ IV Cooperative Decision Making and trajectory planning for CAVs  
	+ IV-A Resolving Multiple Traffic Streams Conflict by Level-k Game 
	+ IV-B Searching Best k-allocation through Cooperative Game 
	+ IV-C Planning Optimal Trajectory with Lattice Planner 

+ V Simulation Validation  
	+ V-A Simulation Design 
	+ V-B Case1: Comparison of Different Control Methods 
	+ V-C Case2: Experiment under Different ROP 
	+ V-D Case3: Heterogeneous Human Driver Involved 

+ VI Conclusion



