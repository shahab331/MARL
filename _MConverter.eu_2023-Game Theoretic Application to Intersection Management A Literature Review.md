1

Game Theoretic Application to Intersection

Management: A Literature Review

Ziye Qin, Student Member, IEEE, Ang Ji, Member, IEEE, Zhanbo Sun, Guoyuan Wu, Senior Member, IEEE, Peng Hao, Member, IEEE, and Xishun Liao, Student Member, IEEE

Abstract—The emergence of vehicle-to-everything \(V2X\) tech-area \[7\]. Simultaneously, management strategies have shifted nology offers new insights into intersection management. This, from focusing only on macroscopic measurements \(e.g., traffic however, has also presented new challenges, such as the need efficiency\) to microscopic considerations such as experiences to understand and model the interactions of traffic participants, and intentions of traffic participants \[8\]. 

including their competition and cooperation behaviors. Game theory has been widely adopted to study rationally selfish or In the context of management and control, intersections

cooperative behaviors during interactions and has been applied can be classified as signalized and un-signalized intersections to advanced intersection management. In this paper, we review

\[9\]. The optimization of signalized intersections typically the application of game theory to intersection management and involves the allocation of the signal phase and timing \(SPaT\). 

sort out relevant studies under various levels of intelligence and Through the optimization of SPaT, bus rapid transit \(BRT\) connectivity. First, the problem of urban intersection management and its challenges are briefly introduced. The basic elements priority strategies can be effectively executed \[10\]. With the of game theory specifically for intersection applications are then advancement of cooperative adaptive cruise control \(CACC\) summarized. Next, we present the game-theoretic models and technology, a compatible SPaT plan has been demonstrated

solutions that have been applied to intersection management. 

to improve intersection capacity \[11\]. In the partially/fully Finally, the limitations and potential opportunities for subsequent connected automated vehicle \(CAV\) environment, signal opti-studies within the game-theoretic application to intersection management are discussed. 

mization can be coupled with vehicle trajectory planning \[12\], 

\[13\]. The co-optimization of SPaT information and vehicle Index Terms—Intersection management, Game theory, Cooperative and non-cooperative behavior, Decision-making, Multi-speed has the potential to concurrently enhance eco-driving agent reinforcement learning. 

practices and traffic efficiency \[14\], \[15\]. Even given SPAT

information, optimizing vehicle trajectories can balance traffic efficiency and fuel economy \[16\], \[17\]. Meanwhile, the manI. INTRODUCTION

agement of signalized intersections, considering the stochastic INTERSECTIONS within urban traffic networks are subject behavior inherent to human-operated vehicles \(HVs\), is at-to traffic conflicts, leading to prolonged vehicle delay and tracting heightened interest \[18\], \[19\]. In an ideal environment elevated energy consumption \[1\]–\[3\]. Innovative technolo-characterized by a full penetration of CAVs, the utilization gies such as human-machine interface \(HMI\), and vehicle-of traffic signals may become redundant \(i.e., un-signalized to-everything \(V2X\) communications facilitate the collection intersections\). The main issues in managing un-signalized and sharing of vehicular and trip information, such as origin intersections pertain to right-of-way allocation and collision-and destination, vehicle trajectories, and personal attributes free vehicle trajectory planning \[20\]–\[23\]. The trajectory plan-

\[4\]–\[6\]. These advancements unlock a significant number of ning for cyclists, a vulnerable demographic at un-signalized opportunities for more efficient intersection management. For intersections, is garnering attention. This concern arises from example, traffic signal controllers can utilize more comprehen-the conflicts that cyclists may encounter both within their arXiv:2311.12341v1 \[cs.GT\] 21 Nov 2023 sive vehicle information to optimize signal phase and timing, group and with motorized vehicles \[24\]. For all types of and minimize overall traffic delays. Since the introduction interactions, the optimization cannot be solely considered from of the autonomous intersection management \(AIM\) system

the perspective of traffic efficiency; factors such as the value by Dresner and Stone, there have been increasing efforts

of time, time-to-collision \(TTC\), and fuel consumption are to explore the applications of emerging technologies in this also frequently investigated \[25\]–\[27\]. Several review articles Ziye Qin, Ang Ji, and Zhanbo Sun \(Corresponding author\) are have summarized the existing methodologies on intersection with the School of Transportation and Logistics, Southwest Jiaotong management and proposed promising future directions. For ex-University, 

Chengdu, 

Sichuan, 

611756, 

China, 

and

the

National

ample, Zhao et al. discussed the application of computational Engineering Laboratory of Integrated Transportation Big Data Application Technology, 

Southwest

Jiaotong

University, 

Chengdu, 

Sichuan, 

intelligence in traffic signal control that can address the large 611756, China. \(Email: ziye.qin@my.swjtu.edu.cn, ang.ji@swjtu.edu.cn, complex nonlinear problems in urban transportation systems zhanbo.sun@home.swjtu.edu.cn; 

Tel:

86-28-87600156; 

Fax:

86-28-

\[28\]. Araghi et al. also reviewed computational intelligence 87600156\). 

Ziye Qin, Guoyuan Wu, and Peng Hao are with the College of Engineering, methods for traffic signal control and compared the perfor-Center for Environmental Research and Technology, University of Califor-mance of various learning methods \[29\]. Wang et al. surveyed nia at Riverside, Riverside, CA 92507 USA. \(Email: gywu@cert.ucr.edu, the history of traffic self-adaptive control systems, pointed out haop@cert.ucr.edu\). 

Xishun Liao is with the University of California at Los Angeles, Los the deficiencies, and expressed the expectations for multi-agent Angeles, CA 90095 USA. \(Email: liaoxishun@gmail.com\). 

reinforcement learning in this field \[30\]. Yau et al. surveyed

2

the application of reinforcement learning algorithms to traffic

\[55\], \[56\]. In lane-changing and ramp-merging games, the signal control \[31\]. Florin and Olariu reviewed three adaptive number of participants may be much less than that at a

traffic signal control strategies for various levels of vehicular standard four-arm intersection where the interactions of traffic communications, including: \(i\) no vehicle communication; \(ii\) participants are more complex. In terms of the operational wireless transmission of vehicle status data; and \(iii\) on-board strategies, discrete actions such as acceleration/deceleration computation to optimize traffic signals \[32\]. Chen and Englund during lane-changing and yield/not yield during ramp-merging surveyed cooperative intersection management strategies under may be sufficient in decision-making modeling. However, as both signalized and un-signalized intersections and summa-the diversity and number of participants grow at intersections, rized related research projects worldwide \[33\]. Studies re-lateral and longitudinal joint strategies are needed for adapting lated to CAV-enabled intelligent intersection management were to complex situations. An example of this complexity is the summarized in \[34\]–\[36\]. Namazi et al. provided a systematic coordination of the green phase of traffic signals. Factors review of intelligent intersection management in mixed traffic such as TTC and travel time are widely used to construct

including autonomous vehicle \(AV\) and human-operated vehithe payoff function from the perspective of players’ safety cle \(HV\), also with high expectations for artificial intelligence and driving efficiency \[57\]. In scenarios where players are \(AI\)-enabled traffic management in the future \[37\]. Al-Turki et traffic operators, traffic signal delays and queue lengths are al. concluded signalized intersection control methods in mixed frequently considered \[58\], \[59\]. In addition, heterogeneous traffic and proposed an alternative machine learning \(ML\)-

trip characteristics, such as trip purpose and distance, result based solution to the design of intelligent adaptive traffic signal in diversified preferences of time, safety, and other measures controllers \[38\]. Additionally, the existing challenges and

\[51\], \[60\]. For example, catching a flight generally has a higher potential future directions were outlined. Shirazi and Morris value of time compared to shopping. Consequently, the payoff reviewed the behavior at intersections and the safety analysis functions should be more specific. Another concern is that for vehicles, drivers, and pedestrians, and made suggestions the continuous flow approaching the intersection makes the for the safety management of intersections \[39\]. Zhong et al. 

problem of passing sequence optimization even more complex, provided a summary of AIM research in terms of the corridor which can be NP-hard \[61\], \[62\]. Game theory serves as a coordination layer, the intersection management layer, and valuable instrument for decomposing complex interactions, the vehicle control layer \[40\]. Iliopoulou et al. summarized modeling decision-making processes, analyzing the behavior the market-inspired allocation of spatial-temporal resources at of traffic participants, and helping take reasonable actions to intersections within the context of the connected vehicle \(CV\) manage the aforementioned issues. Specifically, game theory environment \[41\]. The aforementioned reviews highlighted the recognizes and accommodates user heterogeneity in the first significant accomplishments in the development of technical category of issues, allowing for tailored personalization of tools for intersection management. Nevertheless, most traffic payoff function compositions in line with individual charac-management strategies, when scrutinized from an optimization teristics. For the second category, a synergistic combination of standpoint, have been developed in an altruistic manner, that game theory and multi-agent reinforcement learning \(MARL\) is, any player might have to sacrifice his or her own interest offers a potent solution, effectively resolving the intricate to achieve the global optimum. For example, vehicles are

challenges presented. 

often obliged to endure waiting times for the larger collec-Great efforts have been made to apply game-theoretic

tive benefits, without any compensation. Therefore, enhancing models for intersection management. The diversity of models our understanding of the needs of traffic participants, the makes it challenging to outline the existing studies, so a intricacies of their interactive behaviors, and the delicate clear lineage of game theoretic approaches for intersection equilibrium between individual gains and collective benefits management needs to be identified. Additionally, most stud-are worthy subjects for continued exploration. Toward this ies simplified intersection games by assuming a complete

end, a comprehensive summary of interaction analysis between information environment. In reality, self-interested players decision-makers at intersections holds promise in facilitating may exploit misreported private information to increase their the research of more user-friendly management strategies. 

payoff, making it more practical to address the problem in Consequently, there is an urgent demand to identify a suit-an incomplete information environment. In a nutshell, despite able tool for analyzing individual preferences and interaction the well-established conventional game models for intersection behaviors to guarantee fair decision-making in future intersec-management, there are several challenges to be tackled in tion management. Game theory – known as a classic math-practical applications, such as how to find an appropriate game ematical method to model conflicts and cooperation among

model and how to incentivize traffic participants to take part decision-makers, is commonly used to study the behaviors

in the games. 

of traffic participants \[42\]. A game consists of three basic Based on the author’s understanding, there have been few

elements: players, strategies for players, and payoff functions studies that provide a comprehensive summary of recent

that describe how much payoff or utility each player can obtain developments in game theory applications to intersections, under various environment states and joint actions chosen especially on the behavior analysis and the modeling of traffic by the players \[43\], \[44\]. Game theory has demonstrated participants to enhance intersection management. Moreover, as its potential for managing traffic in various scenarios such connected and automated technologies gradually integrate into as traffic congestion management \[45\], lane-changing \[46\]–

transportation systems, the emphasis on individual travel needs

\[50\], ramp-merging \[51\]–\[54\], and intersection management grows correspondingly. In this context, there is an evident

3

**Determine the keywords**

**Search in databases**

**Preliminary filtering**

**Delicate review**

 Intersection scenarios

Combine ‘intersection’ with

 Google scholar

 Relevance to topics

 Game theory models

 Game theory

 Web of Science

 Scientific impact of the 

 Basic elements

 Game theoretic

 Scopus

journal/conference

 Solutions

 Auction

 Cited and be cited in 

 Abstract

 Innovations and 

 Mechanism design

retrieved studies

 Highlights

shortcomings

Fig. 1. Literature retrieval and analysis workflow for collecting relevant papers demand for methods capable of balancing the requirements

in Fig. 1, we selected 88 articles, published between 2005 and of traffic participants, guaranteeing their respective interests. 

2023, for inclusion in this review. 

Game theory provides a fitting solution to this requirement. 

Employing game-theoretic methods to manage intersection

A. An Overview of Intersection Management

areas with multiple conflict points holds significant promise. 

Intersections serve as the critical points in urban transporta-To fill research gaps and facilitate knowledge and development tion networks where multiple roadways converge horizontally; for future relevant research, the paper provides a review on they also represent concentrated conflict areas, resulting in a the decision-making problems of intersection management

higher incidence of collisions compared to the other parts of and aims to investigate the applications of game theory to urban transportation networks \[63\]. Fig. 2 presents a standard intersections. The main contributions of this paper include: four-leg intersection with three movements along each ap-

\(i\) summarizing the existing applications of game theory

proach, including through traffic, left-turning traffic, and right-for intersections, including the intersection circumstances for turning traffic. When traffic flows from different directions deploying game theory, the basic elements of game theory, pass through the same section of the intersection, there are and the various types of game theory models and solutions; some potential collision areas \(defined as “conflict points”\) and \(ii\) highlighting existing issues and future directions in

\[64\]. Conflict points at intersections can be categorized as combining game theory and intersection management. 

merging conflict points, diverging conflict points, and crossing conflict points \[65\]. Merging conflict points arise when two paths converge or come together into a single path. Conversely, II. APPLICATIONS OF GAME THEORY TO INTERSECTION

diverging conflict points emerge when one path splits into two MANAGEMENT

or more paths. Lastly, crossing conflict points are observed To collect relevant literature on game-theoretic applications when two paths intersect each other perpendicularly or at to intersections, we presented a workflow for systematic liter-some angle, resulting in the potential for one road user to ature retrieval and analysis, illustrated in Fig. 1. This method-cross directly into the path of another. There exist thirty-two ology is versatile and can be adapted to trace advancements \(32\) conflict points among motorized traffic \(MT\) in the given in diverse research fields. We began by identifying critical scenario. This features eight \(8\) merging and eight \(8\) diverg-keywords associated with our research focus, incorporating ing conflict points, where rear-ended and sideswipe collisions terms such as “game theory”, “game theoretic”, “auction”, typically occur. Additionally, there are sixteen \(16\) crossing and “mechanism design”, combined with “intersection”, to

conflict points inside the intersection, with twelve \(12\) of them retrieve relevant studies. This was followed by a keyword associated with left-turn movements. The remaining four \(4\) search in prominent scientific repositories like Google Scholar, crossing conflict points involve the through movements on Web of Science, and Scopus. We also followed up on articles two adjacent approaches, where angle collisions may occur citing the selected publications. Subsequently, we undertook

\[66\]. Non-motorized traffic \(NmT\), as the vulnerable group, a preliminary screening step to offset potential inaccuracies encounters twenty-four \(24\) conflict points interacting with stemming from keyword searches. This involved a brief review motorized traffic. Conventional intersection management relies of the topics, abstracts, highlights, and the prestige of the on the separation of time-space conflicts among approaching journals in which these studies were disseminated. Finally, vehicles, using traffic signal control and lane channelization, we provide an in-depth review and summary of the game

which also limits intersection capacity. To balance efficiency theory framework as applied to intersection management. This and safety, many studies have explored game-theoretic ap-analysis is methodically presented, encompassing the types of proaches for intersection management, which have proven

intersections examined, the game theoretic modeling proce-to be a valuable tool for characterizing such interactions, dures, and both the innovations and limitations observed. An particularly in the decision-making of CAVs \[67\]–\[69\]. 

extensive search using specific keywords in databases yielded To better understand the operation mechanism of intera significant number of pertinent studies. However, initial sections and the interactions among traffic participants, we scrutiny and subsequent in-depth reviews identified instances revisited the intersection management solutions with the ap-of duplicative content. Finally, guided by the criteria presented plication of game theory. The intersection circumstances in





4

**Motorized traffic \(MT\):**

Through traffic

Left-turning traffic

Right-turning traffic

**Non-motorized traffic \(NmT\):**

Pedestrians / Cyclists / Scooterists

**Conflict points:**

Crossing conflict \(MT-MT\)

Merging conflict \(MT-MT\)

Diverging conflict \(MT-MT\)

Crossing conflict \(MT-NmT\)

Fig. 2. Illustration of conflict points for a standard four-leg intersection game-theoretic studies can be classified based on several 1\) Players: Existing studies usually make two common as-criteria: \(i\) the presence or absence of traffic signals: signalized sumptions related to the rationality and intelligence of players and un-signalized intersections; \(ii\) the number of intersec-

\[42\]. Rational players adopt strategies that maximize their ex-tions under consideration: single, isolated intersections and/or pected payoff. If an intelligent player knows everything about multiple intersections; \(iii\) the type of traffic composition: the game, the player can make informed decisions regarding traffic flow with HVs only, CVs only, CAVs only, mixed

his or her next moves. Table I summarizes the literature con-traffic with pedestrians and vehicles. A brief overview of the cerning the categories and number of players involved during studies conducted in the various circumstances is presented intersection management. The number of players in a game

in Fig. 3. More than half of the game theory-related studies directly affects the choices of game theory models. Although \(63.5%\) have focused on the interactive behaviors among

the two-player game has been studied more extensively than vehicles at un-signalized intersections. The multi-intersection other games with multiple players \[44\], the two-player game coordination problem accounts for only 16.5% of studies, 

appears to be insufficient in behavioral modeling at intersec-which still needs further attention. A major chunk of studies tions where multiple players, such as vehicles and pedestrians, focuses on the traffic flow with CVs only or CAVs only since compete for the right-of-way. Therefore, in addition to the CVs/CAVs are more conducive to obtaining traffic information two-player matrix game, it is worthwhile to investigate multi-and implementing vehicle control strategies. 

player games to better represent the diverse interactions at intersections. Note that individual vehicles are widely applied B. Game Theory-based Modeling

as players in game-theoretic modeling at intersections, and it is The key to modeling with game theory is to identify three generally assumed that each vehicle takes the optimal action to basic elements in decision-making problems, i.e., players, maximize its expected payoff. In situations where pedestrian strategies, and payoff functions. However, identifying these signals are not present, pedestrians and motor vehicles also elements can be challenging due to the complex nature of

compete for right-of-way. Some researchers opt to consider intersections in urban environments. The set of players can players who represent a collective, such as phase, intersection, include a variety of traffic participants, such as HVs, CAVs, and platoon of vehicles, whose objective is to maximize the and pedestrians. The set of strategies can be represented by the collective payoff for all the vehicles encompassed within the various choices each participant can make, such as selecting aggregation. 

a movement direction or a speed profile. The payoff function 2\) Strategies: In game-theoretic modeling at intersections, can be defined based on various factors, i.e., vehicle delay, fuel players choose different strategies to maximize their expected consumption, and safety. Additionally, various game theory payoffs from a finite \(e.g., yield or not yield\) or infinite models, such as non-cooperative and cooperative games, can \(e.g., acceleration rate\) set of strategies. The strategies can be employed to analyze interactions among traffic participants also be categorized into two main types: non-cooperative and at the intersection. Identifying and applying these elements cooperative strategies. With cooperative strategies, players try and models can provide valuable insights for intersection to achieve mutual benefits. In non-cooperative games, on the management and can improve traffic flow efficiency and safety. 

other hand, players take actions to maximize their own payoffs

5

\+9VRQO\\WUDIILFIORZ

&9VRQO\\WUDIILFIORZ

&$9VRQO\\WUDIILFIORZ

6LQJOHLQWHUVHFWLRQ

0L\[HGWUDIILFIORZ

6LJQDOL\]HGLQWHUVHFWLRQ

6LQJOH 0XOWLSOHLQWHUVHFWLRQV

3HGHVWULDQVDQGYHKLFOHV

8QVLJQDOL\]HGLQWHUVHFWLRQ

0XOWLSOHLQWHUVHFWLRQV

8QVSHFLILHG





D

E

F

Fig. 3. Applications of game theory under various intersection circumstances TABLE I

PLAYERS AT THE INTERSECTION GAMES

Number of players

Players

Two-player

Multiple \(2\+\) players

Vehicle/Driver

\[61\], \[70\]–\[103\]

\[9\], \[20\], \[25\], \[55\], \[57\], \[92\], \[102\], \[104\]–\[123\]

Pedestrian

\[80\], \[83\], \[97\], \[98\]

-

Phase/Barrier group

\[59\], \[67\]–\[69\], \[124\], \[125\]

\[58\], \[59\], \[126\]

Intersection/Traffic operator/Signal controller

\[86\], \[127\]–\[131\]

\[105\], \[131\]–\[134\]

Incoming link/Path/Movement/Flow/Direction/Vehicle group/Platoon

\[27\], \[135\]–\[138\]

\[139\]–\[143\]

without considering the payoffs of others or the system. The operations such as traffic flow and safety. 

most common strategies are summarized below and outlined

3\) Payoff functions: The payoff function is a real-valued in Table II. 

function defined on the set of all outcomes and strategy pro-

\(i\) Yielding: This strategy involves a player giving up the files. The payoff function of each player maps the multidimen-right-of-way to others, which is usually adopted by traffic sional strategy profiles into real values to capture preferences. 

participants to avoid collision and to maintain safety at Importantly, the player’s payoff depends not only on his or her intersections. 

own strategy but also on the strategies of other players \[144\]. 

\(ii\) Accelerating: The strategy involves a player increasing The factors considered in the payoff functions are also diverse his/her speed to approach and/or depart from an intersec-among traffic scenarios. For example, traffic operators and tion, which is commonly used by traffic participants who

participants may be interested in safety, efficiency, comfort, want to avoid waiting at red lights or to pass through the and energy efficiency at intersections. 

intersection quickly. 

For safety, metrics such as TTC \[82\], \[111\], time difference \(iii\) Decelerating: This strategy involves players reducing to collision \(TDTC\) \[57\], \[77\], \[107\], post-encroachment time their speed to stay safe or to comply with traffic regula-

\(PET\) \[97\], and other surrogate safety measures \(SSMs\) are tions, which is commonly adopted by drivers who want

usually adopted, which are listed as follows:

to avoid accidents or obey traffic lights. 

\(i\) Time-to-collision \(TTC\) was introduced by Hayward

\(iv\) Signal control: This strategy pertains to the traffic signal

\[145\] to indicate the time it takes for two vehicles to controller that controls the phase and signal timing to

collide when the following vehicle is moving faster than

manage traffic flow and reduce congestion at intersec-

the leading vehicle in the same lane. TTC can be written

tions. 

as

In summary, players at intersections adopt a variety of

strategies to optimize their payoffs. The choice of strategy xl\(t\) − xf \(t\)

depends on the players’ type, the intersection circumstances, T T C\(t\) =

, ∀vl\(t\) < vf \(t\)

\(1\)

v

and the available information for decision-making. Game-

l\(t\) − vf \(t\)

theoretic modeling can help to understand how players interact where xl\(t\) and vl\(t\) are the location and velocity of the and how their choices of strategies would affect intersection leading vehicle, respectively, and xf \(t\) and vf \(t\) pertain

6

TABLE II

PLAYERS’ STRATEGIES

Players

Strategies

References

Vehicle

operation

\(accelerate/maintain

current

\[9\], \[20\], \[57\], \[61\], \[70\]–\[77\], \[81\], 

speed/decelerate; speed profile; go through/turn

\[82\], \[85\], \[87\]–\[90\], \[92\], \[99\], \[102\], 

left/turn right; heading angle; steering\)

\[103\], \[107\]–\[109\], \[111\], \[115\], \[118\]–

\[122\], \[130\]

Vehicle/Driver

Yield/Not yield

\[80\], \[83\], \[95\]–\[98\], \[100\], \[101\]

Cooperation/Defection, comply/disobey

\[78\], \[79\], \[84\], \[86\]

Bid for the right-of-way

\[25\], \[55\], \[91\], \[93\], \[94\], \[104\], \[106\], 

\[110\], \[112\]–\[114\], \[116\], \[117\], \[123\]

Route choice

\[105\]

Pedestrian

Wait/Cross

\[80\], \[83\], \[97\], \[98\]

Signal control \(green light time/red light time, keep

\[58\], \[59\], \[67\]–\[69\], \[124\]–\[126\]

Phase/Barrier group

current phase/change to next phase\)

Signal control \(green light time/red light time, keep

\[105\], \[127\], \[129\], \[131\]–\[134\]

current phase/change to next phase\)

Intersection/Traffic operator/Signal controller

Bid for the signal time

\[128\]

Passing permitted/Passing forbidden

\[86\]

Independent/Cooperative

\[130\]

Signal control \(green light time/red light time, keep

\[27\], \[136\], \[138\], \[139\], \[141\]–\[143\]

current phase/change to next phase\)

Incoming link/Path/Movement/Flow/Direction

Passing permitted/Passing forbidden

\[137\]

/Vehicle group/Platoon

Bid for the right-of-way

\[140\]

Speed profile

\[135\]

to the following vehicle. t is the current timestamp. 

\(ii\) Time different to collision \(TDTC\) in \(2\) was proposed Li\(t\)

Lj\(t\)

by \[146\] representing the time difference between the two T Adv\(t\) = |

−

| < TM

\(4\)

vi\(t\)

vj\(t\)

vehicles arriving at the conflict point. 

where i and j are the vehicle indexes, and Li\(t\), Lj\(t\)

denote the current distance from their position to the

s

v

point of conflict. vi\(t\) and vj\(t\) are the current velocities i\(t\)

2Li\(t\)

vi\(t\)

T DT C\(t\)i,j = |\(

\(

\)2 \+

−

\)−

of vehicle i and vehicle j, respectively. T

a

M is the time

i\(t\)

ai\(t\)

ai\(t\)

threshold of safety. 

s

v

\(2\)

j \(t\)

2Lj\(t\)

vj\(t\)

For traffic efficiency, individual vehicles focus on micro-

\(

\(

\)2 \+

−

\)|, 

aj\(t\)

aj\(t\)

aj\(t\)

scopic information, such as velocity, delay, and waiting time; traffic operators, on the other hand, concern more about macro-vmin ≤ vi\(t\), vj\(t\) ≤ vmax

level metrics such as queue length, and throughput from an where v

aggregated/systemic perspective. 

i\(t\) and ai\(t\) are the velocity and acceleration

at time t, respectively, and L

Velocity-based metrics are usually expressed in two ways. 

i\(t\) is the distance from

the current position of vehicle i to the conflict point. 

As shown in \(5\), the first way involves quantifying the change Similarly, v

of speed ∆vi\(t\) \(i.e., acceleration or deceleration rate\) of j \(t\), aj \(t\), and Lj \(t\) pertain to vehicle j. 

v

vehicle i, \[77\]. The second way in \(6\) is the absolute value or min and vmax are the minimum velocity and maximum

velocity, respectively. 

square of the difference between the vehicle’s current speed \(iii\) Post-encroachment time \(PET\) is defined by \[147\], which and the speed limit or desired speed \[9\]. 

is the time elapsed between the moment that the first

vehicle leaves the virtual conflict zone and the moment

∆vi\(t\) = vi\(t \+ 1\) − vi\(t\)

\(5\)

the second vehicle reaches it. 

v

L

i\(t \+ 1\) − vi\(t\)

i

Lj

φi\(t\) =

\(6\)

P ET = |

−

|

\(3\)

|vi\(t\) − ve|

vi

vj

where vi\(t \+ 1\) and vi\(t\) are the velocities of vehicle i at where i and j are the indexes of vehicles. Lj and Lj

time t and time t \+ 1, respectively, and ve is the speed limit represent the distance from their position to the conflict or desired speed. 

point. vi and vj are the velocity of vehicle i and vehicle Delay is considered as the difference between normal travel j, respectively. 

time on a roadway and the estimated travel time through a \(iv\) Time advantage \(TAdv\) describes situations where two work zone. Vehicle delay may be accumulated by the increased road users pass a common spatial area at different times

travel distance and/or reduced speed, insufficient capacity, and to avoid a collision \[72\], \[148\]. TAdv serves as a measure temporary stoppage of the traffic flow \[63\]. Many metrics such to evaluate PET, with the calculation method delineated

as the average total delay and the average stopped delay are as follows, 

widely used in payoff functions \[27\], \[58\], \[68\], \[148\]. 

7

Queue length is a common measure used to evaluate the efficiency of intersections. Average queue length is a conventional **3\(7**

**77& **

**\(QHUJ\\\)XHO**



indicator, which is the quantities of vehicles in the queue per **7'7& **

**6DIHW\\**

lane per time interval \[68\], \[149\]. Estimated queue length is **7$GY**



another frequent metric that has two different calculation meth-

**&ROOLVLRQVWDWXV**

ods. The first method calculates queue length by accumulating arrivals and departures at intersections, following input-output



**'HOD\\**

models. The second one analyzes the formation and dissipation

\)UHTXHQF\\

of queues using the shockwave theory \[150\]. 



**9HORFLW\\**

**\(IILFLHQF\\**

With respect to driving/riding comfort, the focus is typically

**:DLWLQJWLPH**

**&RPIRUW**

on the smoothness of vehicle control. Efforts to enhance



**7UDYHOWLPH**

comfort often focus on achieving a smooth trajectory. Tech-7KURXJKSXW

**4XHXHOHQJWK**

niques include penalizing impractical acceleration/deceleration



\[104\], applying filters to omit abrupt changes in acceleration/deceleration \[88\], and incorporating jerk minimization in optimization models \[73\], \[111\]. The commonly-used metric Fig. 4. Factors considered in payoff functions

is jerk jerki\(t\) in \(7\), which is the first-order derivative of acceleration. 

games investigate the decision-making of individual players, dai\(t\)

jerk

while cooperative games focus on the joint actions of groups i\(t\) =

\(7\)

dt

of players \[144\]. In addition, based on the amount and/or where ai\(t\) is the acceleration of vehicle i at time t. 

type of available information, games can also be classified Fuel \(energy\) consumption and emissions are crucial for

into complete information games and incomplete information both individual drivers and traffic operators, as they are games. The subsequent section presents the game theory

directly related to travel costs and environmental sustainability. 

models commonly adopted in intersection management. Table Models such as the Comprehensive Modal Emissions Model

III illustrates the applications of these game theory models \(CMEM\) \[151\], Virginia Tech Microscopic \(VT-Micro\) model and showcases their relevance and usefulness in the context

\[152\] and Motor Vehicle Emission Simulator \(MOVES\) model of intersection management. 

\[153\] are generally adopted in game-theoretic modeling. These Non-cooperative V.S. Cooperative:

models provide fine-grained estimates of fuel consumption and 1\) Non-cooperative games:

Non-cooperative \(strategic\)

emissions, enabling decision-makers to manage traffic flow game is a type of game in which individual players take strate-while minimizing environmental impacts. 

gies and in which the outcome of the game is described by Fig. 4 visualizes the frequency of various factors used in the strategy taken by each player, along with the correspond-constructing payoff functions. We employed both color and the ing payoff for each player \[154\]. In non-cooperative games, range of circles to differentiate the frequency of various factors players do not form coalitions or cooperate directly with one in determining the payoff function. Specifically, a larger range another. Instead, they take strategy independently to maximize circle represents that the factor is prevalently adopted, and their individual payoffs. Note that “non-cooperative” does not more detailed frequencies can be observed through different mean there is no cooperation among players. Instead, the

colors. According to the statistics, traffic efficiency is the most game focuses on the individual strategies and payoffs, and it concerned, which is usually characterized by delay, queue analyzes the joint strategies without considering the possibility length, and velocity. For safety, conflict-related factors such as of some players forming coalitions and transferring their T T C, and T DT C are commonly used, mostly in the cases of payoff within the coalition \[44\]. Non-cooperative games are multi-vehicle cooperation and/or un-signalized intersections. 

widely used in modeling right-of-way competition at intersec-Note that only a few studies focus on comfort and energy con-tions, such as signal control, pedestrian crossing, and passing sumption, implying that passing through intersections safely sequence decision-making of CAVs. Some commonly used

and as fast as possible is still the most urgent demand. 

non-cooperative games for intersection management include and are not limited to N -player normal form games, Level-k C. Classifications of Game-theoretic Models

thinking, and Stackelberg games. 

Game theory is a powerful tool for modeling and an-

\(i\) N -player normal form games: The game describes all

alyzing complex interactions among traffic participants in possible combinations of strategies and the corresponding traffic systems. There are various ways to classify game

payoffs in a matrix for two players or multiple matrices

theory models according to different criteria, such as whether for more than two players. Players aiming to maximize

players will negotiate a binding contract and whether all their expected utilities may take a pure strategy, identified information is common knowledge for players. In general, 

as a deterministic single strategy. Alternatively, they may game theory models can be classified into non-cooperative resort to a mixed strategy, which assigns a probability

games and cooperative games, which are distinguished by

distribution to the possible pure strategies \[44\]. A finite considering whether a coalition is formed. Non-cooperative N -player normal form game can be formulated by using

8

TABLE III

GAME THEORY MODELS AND SOLUTIONS

Game type

Solutions

References

Pareto efficiency

\[27\], \[58\], \[134\]

Transferable utility game

Shapley value

\[125\]

Pareto efficiency

\[57\]

Cooperative games

Bargaining game

Nash bargaining solution

\[59\], \[124\]

Coalition formation game

Merge and split rule

\[126\]

Fuzzy coalitional game

Fuzzy Shapley method

\[111\]

\[25\], \[104\], \[106\], \[108\], \[110\], 

-

\[112\]–\[114\], \[117\], \[123\]

Auction-based game

First-price auction

\[93\], \[116\], \[128\], \[140\]

Second-price auction

\[93\], \[109\]

Vickrey-Clarke-Groove mechanism

\[55\]

Pareto improvement solution of Nash equilibrium

\[127\]

\[71\], \[73\], \[76\], \[83\], \[86\], \[90\], 

Nash equilibrium

\[91\], \[94\]–\[96\], \[99\]–\[101\], \[107\], 

N-player normal form game

\[129\], \[132\], \[136\], \[143\]

Non-cooperative games

Pareto efficiency

\[68\], \[130\], \[138\]

-

\[79\], \[84\]

Nash equilibrium

\[9\], \[20\], \[103\]

Sequential game

Stackelberg-Nash equilibrium

\[67\], \[102\], \[120\], \[131\], \[142\]

-

\[70\], \[74\], \[75\], \[115\], \[118\], \[122\]

Level-k model

Nash equilibrium

\[121\]

Differential game

Nash equilibrium and Stackelberg equilibrium

\[82\]

\[61\], \[67\], \[69\], \[72\], \[77\], \[87\], 

Others

Nash equilibrium/Pareto efficiency

\[88\], \[105\]

a tuple ⟨N , A, a⟩, where:

\(iv\) Auction-based game: An auction is a mechanism that al-

•N = \{1, 2, 3, . . . , N \} is the finite set of N -players, locates a set of goods to bidders based on their announced indexed by i. 

bids. Today, auctions are pervasive in e-commerce, e-

•A = A1 × A2 × . . . × AN represents the joint strategy

business transactions, and many other web-based applica-

set of players, where Ai is the finite strategy set available tions \[144\]. With the evolution of V2X technology, they to player i and a = \(a1, a2, . . . , aN \) ∈ A is a strategy have also found applications in intersection management

profile with ai ∈ Ai. 

\[110\], \[113\], \[123\]. Common types of auctions include

•u = \(u1, u2, . . . , uN \), ui : A → R is the payoff

the English auction, Dutch auction, first-price auction, 

function for player i, which maps the strategy profile a to and second-price auction. In subsequent sections on in-a real value. The payoff of player i is dependent not only complete information games, we will delve into those

on his or her own strategy but also on strategies taken by auction types frequently used in intersection management

others. Therefore, the utility function is defined over the that are incentive-compatible. 

space of A instead of Ai. 

\(v\) Differential game: Differential games are grounded in \(ii\) Level-k thinking: Level-k thinking assumes that play-a mathematical theory that addresses conflict problems

ers take their strategies based on predictions about the

modeled as games where players’ states continuously

strategies of others, thus we can categorize players by

vary over time \[155\]. In such games, the potential actions the “depth” of their strategic thought, a.k.a., “Levels” 

of players are modeled and analyzed using differential

\[115\]. “Level-zero” players take their strategies without equations that encompass control vectors manipulated by

considering the strategies of others. “Level-k” behave

players \[156\]. The inherent ability of differential games under the assumption that their fellow players are at

to handle continuous time challenges, combined with

“Level-k−1”. They then adopt the optimal response to the

their resemblance to control problems featuring multiple

strategies of the “Level-k−1” players. In \[115\], driving controllers with different objectives, makes them aptly

aggressiveness, encompassing both conservative vehicles

suited for intersection management, where traffic states

and aggressive vehicles, was utilized as a criterion to

are continuously evolving. 

demonstrate the “Level”. 

\(iii\) Stackelberg games: The Stackelberg game depicts the 2\) Cooperative games: The cooperative \(coalitional\) game

process in perfect information where one player is the

is a type of game in which players can negotiate binding

leader who takes a strategy first. The other players are

contracts that allow them to plan joint strategies, and no play-followers who observe the leader’s strategy and then

ers can do worse by cooperating \[126\], \[154\]. In cooperative choose their strategies accordingly \[44\]. In the context of games, a group of rational players cooperates to reach a shared intersection signal control, the signal phase with emer-goal, in which the most crucial step is the allocation of the gency vehicles can be deemed as a leader who first

payoff among the players. The mathematical definition of a determines its phase timing and the other phases may

cooperative game can be represented using an ordered pair be considered as followers \[67\]. 

⟨N, v⟩, where N is a finite set of players and v = 2N → R is the characteristic function, which describes the value created

9

by the group of players. It conforms to the v\(ϕ\) = 0, 

efficient outcome. In mechanism design, the designer chooses signifying that the collective payoff of an empty coalition is a mechanism that maximizes the social welfare subject to

zero \(0\) across all subsets of N \[157\]. Typical cooperative some constraints, such as incentive compatibility, individual games used in intersection management are transferable utility rationality, and budget balance. Incentive compatibility is games that allow a group of vehicles to “purchase” the travel an effective tool for revealing the real information players time from others \[27\], and bargaining games to optimize the possess, with two main types: \(1\) For dominant strategy

signal timing by modeling signal phases as players \[59\]. 

incentive compatibility \(DSIC\), truth revelation is the optimal \(i\) Transferable utility games: In a transferable utility game, response for each player, regardless of the information reported players can make unlimited side payments to others. 

by others; \(2\) for Bayesian incentive compatibility \(BIC\). 

This allows them to redistribute the value of a coalition truth revelation is the optimal response for each player in among the players in the coalition in any way as they

expectation of the information of other players \[144\]. Incentive deem appropriate \[158\]. The characteristic function in compatibility can be achieved by the following methods. 

transferable utility games assigns a value of v\(S\) to each \(i\) Second-price auction \(Vickrey auction\): A second-price coalition S ⊆ N , where v\(S\) is the value of the coalition auction is a sealed-bid auction where the highest bidder

S depicting the total amount of transferable utility that emerges as the winner but only pays a price equivalent

the members of S can earn without any help from the

to the second-highest bid \[144\]. 

player outside of S \[144\]. 

\(ii\) Vickrey-Clarke-Groves \(VCG\) mechanism: The Vickrey-

\(ii\) Bargaining games: Bargaining games describe the pro-

Clarke-Groves \(VCG\) mechanism is designed to elim-

cess by which two or more players bargain toward an

inate incentives for misreporting by imposing on each

agreed-upon outcome \[159\]. The two-player bargaining player the cost of any distortion they cause. In the

game was first presented by \[160\], where each player VCG mechanism, the payment for a player is set in

demands a portion of some good, if the sum of the

such a way that their report cannot influence the total

proposals is no more than the total good, then both

payoff for the rest of the players \[161\]. This approach players obtain their demand. Otherwise, both players

encourages truthful reporting by aligning the individual

receive nothing \[156\]. A two-player bargaining game player’s interests with the overall welfare of the group. 

can be represented by using the ordered pair \(S, d\), 

Research related to incomplete information environments at where S ⊆

2

R

is the set of alternatives, which is

intersections is comparatively limited, with key studies out-nonempty, compact, and convex; d = \(d1.d2\) ∈ S is

lined below: Initially, the second-price auction was applied to the conflict \(disagreement\) point. There is an alternative design a reservation policy for managing the passing sequence x = \(x1, x2\) ∈ S satisfying x ≫ d, which means that

of conflicting zone movements at intersections \[109\], \[110\]. 

if players agree on the alternative x, their payoffs are x1

Subsequently, the VCG mechanism was designed to reveal true and x2, respectively, if not, their payoffs are d1 and d2

private information from players, such as the urgency level, 

\[159\]. 

to schedule the vehicle passing sequence at intersections \[55\]. 

Complete information V.S. Incomplete information:

More recently, an online incentive-compatible mechanism was 3\) Complete information games: A game is regarded as

proposed to prevent players from misreporting their delay a complete information game if the players share common

costs, notably, it can be implemented in dynamic traffic envi-knowledge of the game being played, including each player’s ronments \[123\]. Sponsored search auction was employed as a strategy sets and payoff functions. This indicates that each solution for encouraging players to report truthful information player is aware of these elements, each player knows that all to prevent conflicts and deadlocks in the mixed traffic flow other players are aware, and this cycle of knowledge contin-comprising HVs and CAVs \[113\]. Following this, a sponsored ues indefinitely \[44\], \[144\]. In traffic scenarios, particularly search auction was extended for application in multi-vehicle at intersections, complete information gaming is an overly dynamic traffic environments to mitigate overflow issues \[112\]. 

idealized method of modeling, as traffic participants typically prefer to maintain the privacy of their trip information. Further-more, obtaining information about all users poses a significant D. Game solutions

challenge due to communication constraints. 

The solutions of a game represent the combinations of

4\) Incomplete information games: A game is regarded

strategies that players may adopt, and in turn predict the as an incomplete information \(also known as asymmetric

possible outcomes of the game, which may correspond to

information\) game when, as the players are ready to take

multiple different solutions. The general solutions of games a strategy, at least one player possesses private information are summarized below, and the applications for intersections about the game that the other players may not know \[144\]. 

are listed in Table III. 

In such scenarios, players must make decisions based on the 1\) Nash equilibrium: Nash equilibrium is one of the solu-available information and their beliefs about the undisclosed tion concepts prevalent in non-cooperative games, and players information. To address the information asymmetry in incom-have no incentives to deviate from their current strategies, even plete information games, mechanism design is commonly used if they know others’ strategies at Nash equilibrium \[162\]. 

to reveal the real information of the players \[144\]. Mechanism Given a non-cooperative game ⟨N , Si, ui⟩, let N

=

design involves designing a game that incentivizes players to

\{1, 2, 3, . . . , N \} be the set of players, Si be the possible reveal their private information truthfully, leading to a more strategy set of player i and ui be the payoff function of player

10

i. The strategy profile s∗ = \(s∗, s∗ \) where s∗

is strategies

MAS, combined with the imperative to examine complicated

i

−i

−i

of all players except player i is the Nash equilibrium if interactions among agents, has spurred the advancement of the MARL field. This is built on two fundamental pillars: the RL performed within AI and the interdisciplinary work ui\(s∗, s∗ \) ≥ u

\), ∀s

i

−i

i\(si, s∗

−i

i ∈ Si, i ∈ N

\(8\)

on game theory \[166\]. Game theory models MAS as a multi-which can also be formulated as

player game and can provide a rational strategy for each player in a game \[167\]. 

ui\(s∗, s∗ \) = max u

\), ∀i ∈ N

i

−i

i\(si, s∗

−i

\(9\)

A. A Brief Overview of Multi-agent Reinforcement Learning In short, each player’s Nash equilibrium is the best response The single-agent reinforcement learning process can be

to the other players’ Nash equilibrium \[144\]. 

formulated using a Markov decision process \(MDP\) \[168\]. The 2\) Pareto efficiency: Pareto efficiency \(Pareto optimality\) single agent will find the optimal policy through a trial-andis an economic state where resources cannot be reallocated to error process, which can maximize a possibly delayed reward make one individual better off without making at least one in a stochastic stationary environment \[166\]. In the single-individual worse off \[144\]. Pareto efficiency can be expressed agent scenario, each agent solves the sequential decision-mathematically as

making problem by trial and error, while this comes with the The strategy profile s is Pareto efficient if there is no other difficulty of defining an optimal learning goal for multiple strategy profile s′ such that the payoff u

agents \[169\]. Agents have to simultaneously interact with the i\(s′\) ≥ ui\(s\) for every

player i and u

environment and others, and the reward function is formulated j \(s′\) ≥ uj \(s′\) for some player j. 

3\) Shapley value: The Shapley value is a popular single-

by all agent’s joint actions, making this problem even more valued solution concept for cooperative games, which provides challenging in this dynamic case. With the development in a way to allocate total benefits to players in a coalition \[159\]. 

recent decades, the MARL has achieved remarkable accom-

The Shapley value gives player i in the coalition a share of plishments in many fields, such as StarCraft II \[170\], Atari

\[171\], and Robotics \[172\], and it has also made ripples in transportation \[173\]. 

X

|S|\!\(n − |S| − 1\)\! 

ϕi\(N, v\) =

\(v\(S ∪ i\) − v\(S\)\)

The decision-making process in multi-agent cases is usually n\! 

S⊆N \\i

modeled by the stochastic game in Definition 1 \[168\], \[174\]. 

\(10\)

Definition 1 \(Stochastic game\) A stochastic game is the

extension of MDP in the multi-agent case, which can be

in which n is the total number of players, |S| is the cardi-defined by a tuple ⟨N , S, \{Ai\}

nality of coalition S, and v\(S\) is the characteristic function i∈N , P , \{Ri\}i∈N , γ⟩. 

Where

indicating the worth of coalition S. 

4\) Core: In a transferable utility cooperative game, the core is the set of payoff allocations that are stable against deviations

• N : the number of agents, N = \{1, 2, · · · , N \}, N > 1

by any coalition of players, which ensures that no coalition has

• S : the state space shared by all agents

an incentive to break away and form a new coalition to obtain

• Ai: the action space of agent i. Let A:= A1 × A2 × A3 ×

· · · × AN

a more favorable payoff. Given a cooperative game ⟨N, v⟩, the core C\(N, v\) can be represented as

• P : S × Ai → ∆\(S \): the transition probability from any state s ∈ S to state s′ ∈ S for any joint actions a ∈ A

• Ri : S × A × S → R: the reward function that returns a

X

C\(N, v\) = \{x = x1, x2, x3, . . . , xn |

xi = v\(N \), 

scalar value to the agent i for a transition from \(s, a\) to i∈N

\(11\)

s′

X

and

xi ≥ v\(S\) f or all S ⊂ N \}

• γ ∈ \[0, 1\] is the discount factor

i∈S

At each time step t, given the state st, the agent ∈ N

where N is a finite set of players, v is the characteristic will execute the action ait, simultaneously with others. The function, S represents a coalition and x = \{x

joint actions of the agents make the system transit to the 1, x2, x3, . . . , xn\}

is a payoff vector \[163\]. 

next state st\+1 ∼ P \(·|st, at\), and rewards of the agent i by Ri\(st, at, st\+1\). The agent i aims at optimizing its long-term reward in \(12\) by finding the policy πi : S → ∆\(Ai\) such that III. MULTI-AGENT REINFORCEMENT LEARNING

ai ∼ πi\(·|s

AT INTERSECTIONS

t\). The common shorthand notation −i = N \\ i is

used to represent the set of other agents. Therefore, the value MARL has a significant connection to game theory, where

function V i : S → R of agent i is transformed into the joint players select actions to maximize payoffs in the presence of policy π : S → ∆\(A\) defined as π\(a|s\) := Q

πi\(ai|s\). 

other payoff-maximizing players \[164\]. A multi-agent system i∈N

Given the specific joint policy π and state s ∈ S. 

\(MAS\) is an extension of agent technology where a group of loosely connected autonomous agents act in an environment X

to achieve a common goal, which can be done either by

V i

γtRi\(s

∼ πi\(·|s

πi,π−i \(s\) := E\[

t, at, st\+1\)|ait

t\), s0 = s\]

cooperating or competing, sharing or not sharing knowledge t≥0

with each other \[165\]. Recently, the requirement for adaptive \(12\)

11

The optimal policy is

C. Pros and Cons of Game Theory V.S. MARL

Both game theory and MARL can tackle decision-making

π

π∗\(a

V i,π−i \(s\)

in multi-agent environments. Game theory offers an analytical i

i|s, π−i\) = arg max

\(13\)

i

πi

method, shedding light on players’ strategies and producing We recommend that interested readers refer to \[168\] and \[172\]

explainable outcomes like the Nash equilibrium and the Pareto for a detailed introduction to the MARL. 

optimality. However, its efficacy diminishes with continuous actions or an extensive number of agents while MARL is adept B. Benchmarks and Simulation Platforms

at generating continuous actions for numerous agents. Despite The opportunities of multi-agent learning in intersection its strengths, MARL’s challenges include time-consuming

management pointed out by Dresner and Stone have attracted training, transferability issues, and lack of explainability. 

and encouraged an increasing number of scholars to address Recognizing these possible shortcomings, hybrid algorithms the challenges of MARL in intersections \[175\]. Especially, like Minimax-Q and Nash-Q have emerged, integrating game

MARL is widely considered to be promising for traffic signal solutions with MARL to derive learning-based equilibrium

control \(TSC\) in large-scale road networks. The topic of

\[200\]. These hybrids aim to balance the rigor of game-theoretic MARL applications for intersection management has attracted solutions with the dynamic learning capabilities of MARL, increasing attention from researchers. 

addressing their individual limitations while leveraging their In the domain of intersection management, the application collective strengths. 

of MARL often entails performance comparisons with conven-tionally recognized methods to underscore their advantages. 

IV. LIMITATIONS AND FUTURE RESEARCH DIRECTIONS

Notably, several high-performing AI-based techniques have To facilitate the adoption of game theory in intersection also gained prominence. Hence, we provide a list of potential management, it is essential to address the technical challenges benchmarks here to facilitate related research. 

associated with these applications and to identify potential Conventional methods:

future research directions. This section discusses some of

• Fixed time \[176\]

the main challenges in using game theory for intersection

• MaxPressure \[177\]

management, as well as promising approaches and future

• GreenWave \[178\]

research directions in this field. 

• Longest queue first \[179\]

• SCOOT \[180\]

A. Limitations of existing related studies

• SOTL \[181\]

In the previous sections, the applications of game theory AI-based methods:

for intersections were reviewed and summarized. However, 

• PressLight \[182\]

despite numerous studies that have investigated various inter-

• CoLight \[183\]

section environments, there are still many limitations, as listed

• MA2C \[184\]

below. 

• MetaLight \[185\]

\(i\) One significant challenge is the development of game-

• IG-RL \[186\]

theoretic models in dynamic traffic environments. Traffic

• MARLIN-ATSC \[167\]

states at intersections can exhibit marked changes dynam-

• MPLight \[187\]

ically, such as the arrival of vehicles and vehicle states. 

• AttendLight \[188\]

Therefore, the game theory model should be able to adapt

MARL requires considerable training before it can be

to such changes and to make real-time decisions. Addi-

applied in practice, so a simulation platform that provides a tionally, the computational complexity of game-theoretic

more realistic picture of traffic operations is critical. With the models can make them challenging to implement in real-rapid development of MARL technology and its widespread

time traffic management systems \[20\]. Thus, there is a application at intersections, some platforms are becoming need to develop more efficient algorithms and techniques

compatible with multi-agent training. This section lists some to calculate with these models efficiently. 

prevailing platforms. 

\(ii\) Communication plays a crucial role in micro-level interactions among traffic participants, but some studies

• SUMO \[189\]

do not specify the degree of connectivity and intelli-

• Paramics \[190\]

gence required for effective communication. In general, 

• Aimsun \[191\]

vehicular communications rely on robust link and channel

• VISSIM \[192\]

access protocols, such as IEEE 802.11p wireless access

• CityFlow \[193\]

in vehicular environments \(WAVE\) \[201\]. It is worth

• Flow \[194\]

noting several inherent communication issues: \(a\) fre-

• Traffic3D \[195\]

quent topology partitioning resulting from the high-speed

• SMARTS \[196\]

mobility of traffic participants, \(b\) instability of long-

• highway-env \[197\]

range communication due to increased delay spread and

• Movsim \[198\]

diminished channel capacity, \(c\) complications arising

• Carla \[199\]

from the use of conventional routing protocols, and \(d\)

12

broadcast storm issue in high dense scenarios. Real-

instance, game theory models can be used to decide

time performance is crucial for intersection management. 

whether to adopt the planned vehicle trajectory or speed

Without a reliable communication network or accurate

profiles obtained from system-level optimization, thereby adherence to control strategies by vehicles, intersections improving the efficiency of intersections. 

can become highly disorganized and inefficient. Conse-

\(v\) Existing models assume rational players, but drivers’ and quently, potential communication challenges need further

passengers’ strategies can also be influenced by their

discussion and investigation. 

emotions and experience. Future research should consider

\(iii\) NmT, who are highly involved in traffic and interact the individual characteristics and bounded rationality of frequently still receive insufficient attention in related traffic participants. In addition, including more personal studies, and more research is needed to address their

travel information in constructing the payoff function can specific needs and challenges. 

make intersection management acceptable to all individ-

\(iv\) The assumption of a complete information environment uals. 

may be too idealistic in real-world scenarios, and traffic \(vi\) Future research directions in this field also include the participants may misreport their private information to

exploration of new game-theoretic models and techniques

gain more benefits, resulting in unfair resource allocation. 

for managing CAVs at intersections, the development

Thus, more research is needed to develop mechanisms

of multi-agent reinforcement learning approaches for

to detect and to mitigate the effects of information

adaptive intersection management, and the investigation

asymmetry. 

of game-theoretic approaches for managing interactions

\(v\) Existing studies have skillfully applied game theory

between MT and NmT. 

to upper-level decision-making for autonomous driving. 

Overall, game theory has the potential to revolutionize inter-However, the upper-level decisions made by game theory

section management by providing more efficient and adaptive models are not consistently well-integrated with lower-solutions to traffic control. However, significant technical level vehicle motion planning and control. 

challenges must be addressed, and innovative approaches must \(vi\) Game theory is formulated under the assumption of

be developed to fully realize the benefits of game theory in rational players, but players’ strategies can also be in-this field. 

fluenced by different characteristics. In existing studies, many utilitarian factors, such as total delay or throughput, V. CONCLUSION

are considered, but the real needs and preferences of

traffic participants are often not adequately addressed. 

In conjunction with the advancement of intelligent trans-

Heterogeneous users, with their diverse preferences and

portation systems, incorporating knowledge of game theory objectives, need further investigation in addition to the and mechanism design becomes imperative for ensuring the

mere differentiation in the categories of players. 

ground truth collected individual travel information \(such as the value of time\), thereby fostering fair decision-making processes. Moreover, rather than the conventional collective B. Future research directions

approach to intersection management considering all vehicles Based on the limitations of the available literature, several in an approach as a unified group, there is a growing emphasis gaps and opportunities for future research in game theory-on personalized guidance. Game theory becomes instrumental based intersection management can be identified. These in-in this shift, offering insights into individual behaviors and clude:

their interactions. In this paper, we provided a summary of \(i\) For micro-level interactions between vehicles, it is crucial the applications of game theory for urban intersections. First, to address the communication requirements of traffic

we proposed and applied a workflow for systematic literature participants in real-time scenarios. Simulating a con-retrieval and analysis, yielding high-quality relevant literature. 

nected environment by adding communication systems

Then, numerous game-theoretic modeling approaches and cor-to traffic simulation is one way to improve the realism

responding possible solutions applied to intersections were of the simulations. Additionally, field experiments under reviewed and summarized. Concurrently, the widely discussed connected conditions can provide valuable insights. 

multi-agent reinforcement learning \(MARL\), which is inextri-

\(ii\) The interaction among MT and NmT should receive more cably linked to game theory, is briefly summarized. Finally, attention in future research. These groups are highly

limitations and possible future directions in this area were involved in traffic and interact frequently, but their in-pointed out. In conclusion, numerous innovative solutions for teractions are often overlooked in existing studies. 

intersection management have been proposed by leveraging the \(iii\) Incomplete information environments are common in

advantages of game theory. Game theory excels in resolving real-world scenarios, and mechanism design under in-traffic conflicts and harmonizing the interests of multiple complete information in a dynamic traffic environment

traffic participants, making it an invaluable tool in the field of should be highlighted. Future research can explore the

transportation management. As the intelligent transportation interaction of traffic participants by considering incentive system continues to evolve, the strategic application of game compatibility and other constraints. 

theory for analyzing individual traffic participants’ interactions \(iv\) Combining optimization algorithms and game theory in can significantly contribute to establishing a harmonious trans-decision-making is a promising research direction. For

portation ecosystem. 

13

ACKNOWLEDGMENTS

\[15\] P. Sun, D. Nam, R. Jayakrishnan, and W. Jin, “An eco-driving algorithm based on vehicle to infrastructure \(v2i\) communications for signalized The work is supported by the National Natural Science

intersections,” Transp. Res. Part C, Emerg. Technol., vol. 144, p. 

Foundation of China via grant 52072316 and 52302418, 

103876, 2022, doi: 10.1016/j.trc.2022.103876. 

\[16\] P. Lin, J. Liu, P. J. Jin, and B. Ran, “Autonomous vehicle-intersection the Postdoctoral International Exchange Program via grant coordination method in a connected vehicle environment,” IEEE

YJ20220311, the Fundamental Research Funds for the Cen-

Intell. Transp. Syst. Mag., vol. 9, no. 4, pp. 37–47, 2017, doi: tral Universities via grant 2682023CX047, and the Tencent-

10.1109/MITS.2017.2743167. 

\[17\] H. Yang, F. Almutairi, and H. Rakha, “Eco-driving at signalized SWJTU Joint Laboratory of Intelligent Transportation Pro-intersections: A multiple signal optimization approach,” IEEE Trans. 

gram via grant R113623H01015. Any opinions, findings, 

Intell. Transp. Syst., vol. 22, no. 5, pp. 2943–2955, 2020, doi: conclusions, or recommendations expressed in this paper are

10.1109/TITS.2020.2978184. 

\[18\] B.-K. Xiong and R. Jiang, “Speed advice for connected vehicles those of the authors and do not necessarily reflect the views at an isolated signalized intersection in a mixed traffic flow con-of the sponsors. 

sidering stochasticity of human driven vehicles,” IEEE Trans. Intell. Transp. Syst., vol. 23, no. 8, pp. 11 261–11 272, 2021, doi:

10.1109/TITS.2021.3102430. 

R

\[19\] C. Chen, J. Wang, Q. Xu, J. Wang, and K. Li, “Mixed platoon control EFERENCES

of automated and human-driven vehicles at a signalized intersection: dynamical analysis and optimal control,” Transp. Res. Part C, Emerg. 

\[1\] A. Mirheli, M. Tajalli, L. Hajibabai, and A. Hajbabaie, “A consensus-Technol., vol. 127, p. 103138, 2021, doi: 10.1016/j.trc.2021.103138. 

based distributed trajectory control in a signal-free intersection,” 

\[20\] N. Li, Y. Yao, I. Kolmanovsky, E. Atkins, and A. R. Girard, Transp. Res. Part C, Emerg. Technol., vol. 100, pp. 161–176, 2019, 

“Game-theoretic modeling of multi-vehicle interactions at uncon-doi: 10.1016/j.trc.2019.01.004. 

trolled intersections,” IEEE Trans. Intell. Transp. Syst., 2020, doi:

\[2\] C. Yu, Y. Feng, H. X. Liu, W. Ma, and X. Yang, “Integrated opti-

10.1109/TITS.2020.3026160. 

mization of traffic signals and vehicle trajectories at isolated urban

\[21\] Z. Hu, J. Huang, D. Yang, and Z. Zhong, “Constraint-tree-driven intersections,” Transp. Res. Part B, Methodol., vol. 112, pp. 89–112, modeling and distributed robust control for multi-vehicle cooperation 2018, doi: 10.1016/j.trb.2018.04.007. 

at unsignalized intersections,” Transp. Res. Part C, Emerg. Technol., 

\[3\] B. Qian, H. Zhou, F. Lyu, J. Li, T. Ma, and F. Hou, “Toward collision-vol. 131, p. 103353, 2021, doi: 10.1016/j.trc.2021.103353. 

free and efficient coordination for automated vehicles at unsignalized

\[22\] C. Chen, Q. Xu, M. Cai, J. Wang, J. Wang, and K. Li, “Conflict-free co-intersection,” IEEE Internet Things J., vol. 6, no. 6, pp. 10 408–10 420, operation method for connected and automated vehicles at unsignalized 2019, doi: 10.1109/JIOT.2019.2939180. 

intersections: Graph-based modeling and optimality analysis,” IEEE

\[4\] K. C. Dey, A. Rayamajhi, M. Chowdhury, P. Bhavsar, and J. Martin, Trans. Intell. Transp. Syst., vol. 23, no. 11, pp. 21 897–21 914, 2022, 

“Vehicle-to-vehicle \(v2v\) and vehicle-to-infrastructure \(v2i\) communi-doi: 10.1109/TITS.2022.3182403. 

cation in a heterogeneous wireless network–performance evaluation,” 

\[23\] J. Luo, T. Zhang, R. Hao, D. Li, C. Chen, Z. Na, and Transp. Res. Part C, Emerg. Technol., vol. 68, pp. 168–184, 2016, doi: Q. Zhang, “Real-time cooperative vehicle coordination at unsignal-

10.1016/j.trc.2016.03.008. 

ized road intersections,” IEEE Trans. Intell. Transp. Syst., 2023, doi:

\[5\] Z. Sun, T. Huang, and P. Zhang, “Cooperative decision-making for

10.1109/TITS.2023.3243940. 

mixed traffic: A ramp merging example,” Transp. Res. Part C, Emerg. 

\[24\] L. Huang and J. Wu, “Cyclists’ path planning behavioral model Technol., vol. 120, p. 102764, 2020, doi: 10.1016/j.trc.2020.102764. 

at unsignalized mixed traffic intersections in china,” IEEE In-

\[6\] L. Chen, Y. Li, C. Huang, B. Li, Y. Xing, D. Tian, L. Li, Z. Hu, X. Na, tell. Transp. Syst. Mag., vol. 1, no. 2, pp. 13–19, 2009, doi: Z. Li, S. Teng, C. Lv, J. Wang, D. Cao, N. Zheng, and F.-Y. Wang, 

10.1109/MITS.2009.933859. 

“Milestones in autonomous driving and intelligent vehicles: Survey of

\[25\] I. K. Isukapati and S. F. Smith, “Accommodating high value-of-time surveys,” IEEE Trans. Intell. Veh., vol. 8, no. 2, pp. 1046–1056, 2023, drivers in market-driven traffic signal control,” in Proc. 2017 IEEE

doi: 10.1109/TIV.2022.3223131. 

Intell. Veh. Symp. \(IV\). 

Los Angeles, CA, USA: IEEE, Jul. 2017, pp. 

\[7\] K. Dresner and P. Stone, “A multiagent approach to autonomous 1280–1286, doi: 10.1109/IVS.2017.7995888. 

intersection management,” J. Artif. Intell. Res., vol. 31, pp. 591–656, 

\[26\] R. Niroumand, M. Tajalli, L. Hajibabai, and A. Hajbabaie, “Joint 2008, doi: 10.1613/jair.2502. 

optimization of vehicle-group trajectory and signal timing: Introduc-

\[8\] W. Wang, L. Wang, C. Zhang, C. Liu, L. Sun et al., “Social interactions ing the white phase for mixed-autonomy traffic stream,” Transp. 

for autonomous driving: A review and perspectives,” Found. Trends Res. Part C, Emerg. Technol., vol. 116, p. 102659, 2020, doi: Robot., vol. 10, no. 3-4, pp. 198–376, 2022, doi: 10.1561/2300000078. 

10.1016/j.trc.2020.102659. 

\[9\] S. Pruekprasert, X. Zhang, J. Dubut, C. Huang, and M. Kishida, 

\[27\] D. Lin and S. E. Jabari, “Pay for intersection priority: A free market

“Decision making for autonomous vehicles at unsignalized inter-mechanism for connected vehicles,” IEEE Trans. Intell. Transp. Syst., section in presence of malicious vehicles,” in Proc. IEEE Intell. 

2021, doi: 10.1109/TITS.2020.3048475. 

Transp. Syst. Conf. \(ITSC\). 

IEEE, 2019, pp. 2299–2304, doi:

\[28\] D. Zhao, Y. Dai, and Z. Zhang, “Computational intelligence in

10.1109/ITSC.2019.8917132. 

urban traffic signal control: A survey,” IEEE Trans. Syst., Man, 

\[10\] J. Liu, P. Lin, and B. Ran, “A reservation-based coordinated transit Cybern. C, Appl. Rev., vol. 42, no. 4, pp. 485–494, 2011, doi: signal priority method for bus rapid transit system with connected

10.1109/TSMCC.2011.2161577. 

vehicle technologies,” IEEE Intell. Transp. Syst. Mag., vol. 13, no. 4, 

\[29\] S. Araghi, A. Khosravi, and D. Creighton, “A review on com-pp. 17–30, 2020, doi: 10.1109/MITS.2020.3014151. 

putational intelligence methods for controlling traffic signal tim-

\[11\] H. Liu, X.-Y. Lu, and S. E. Shladover, “Traffic signal control by ing,” Expert Syst. Appl., vol. 42, no. 3, pp. 1538–1550, 2015, doi: leveraging cooperative adaptive cruise control \(cacc\) vehicle platooning

10.1016/j.eswa.2014.09.003. 

capabilities,” Transp. Res. Part C, Emerg. Technol., vol. 104, pp. 390–

\[30\] Y. Wang, X. Yang, H. Liang, and Y. Liu, “A review of the self-adaptive 407, 2019, doi: 10.1016/j.trc.2019.05.027. 

traffic signal control system based on future traffic environment,” J. 

\[12\] Y. Guo, J. Ma, C. Xiong, X. Li, F. Zhou, and W. Hao, “Joint Adv. Transp., vol. 2018, 2018, doi: 10.1155/2018/10961237. 

optimization of vehicle trajectories and intersection controllers with

\[31\] K.-L. A. Yau, J. Qadir, H. L. Khoo, M. H. Ling, and P. Komisarczuk, connected automated vehicles: Combined dynamic programming and

“A survey on reinforcement learning models and algorithms for traffic shooting heuristic approach,” Transp. Res. Part C, Emerg. Technol., signal control,” ACM Comput. Surv., vol. 50, no. 3, pp. 1–38, 2017, vol. 98, pp. 54–72, 2019, doi: 10.1016/j.trc.2018.11.010. 

doi: 10.1145/3068287. 

\[13\] Y. Feng, C. Yu, and H. X. Liu, “Spatiotemporal intersection con-

\[32\] R. Florin and S. Olariu, “A survey of vehicular communications for trol in a connected and automated vehicle environment,” Transp. 

traffic signal optimization,” Veh. Commun., vol. 2, no. 2, pp. 70–79, Res. Part C, Emerg. Technol., vol. 89, pp. 364–383, 2018, doi: 2015, doi: 10.1016/j.vehcom.2015.03.002. 

10.1016/j.trc.2018.02.001. 

\[33\] L. Chen and C. Englund, “Cooperative intersection management: A

\[14\] P. Hao, G. Wu, K. Boriboonsomsin, and M. J. Barth, “Eco-approach survey,” IEEE Trans. Intell. Transp. Syst., vol. 17, no. 2, pp. 570–586, and departure \(ead\) application for actuated signals in real-world 2015, doi: 10.1109/TITS.2015.2471812. 

traffic,” IEEE Trans. Intell. Transp. Syst., vol. 20, no. 1, pp. 30–40, 

\[34\] J. Rios-Torres and A. A. Malikopoulos, “A survey on the coordination 2018, doi: 10.1109/TITS.2018.2794509. 

of connected and automated vehicles at intersections and merging at

14

highway on-ramps,” IEEE Trans. Intell. Transp. Syst., vol. 18, no. 5, compatible mechanisms,” IEEE Trans. Intell. Transp. Syst., vol. 20, pp. 1066–1077, 2016, doi: 10.1109/TITS.2016.2600504. 

no. 3, pp. 912–924, 2018, doi: 10.1109/TITS.2018.2838049. 

\[35\] Q. Guo, L. Li, and X. J. Ban, “Urban traffic signal control with con-

\[56\] Y. Wang, Y. Ren, S. Elliott, and W. Zhang, “Enabling courteous nected and automated vehicles: A survey,” Transp. Res. Part C, Emerg. 

vehicle interactions through game-based and dynamics-aware intent Technol., vol. 101, pp. 313–334, 2019, doi: 10.1016/j.trc.2019.01.026. 

inference,” IEEE Trans. Intell. Veh., vol. 5, no. 2, pp. 217–228, 2020, 

\[36\] M. Khayatian, M. Mehrabian, E. Andert, R. Dedinsky, S. Choudhary, doi: 10.1109/TIV.2019.2955897. 

Y. Lou, and A. Shirvastava, “A survey on intersection management of

\[57\] K. Wang, Y. Wang, H. Du, and K. Nam, “Game-theory-inspired connected autonomous vehicles,” ACM Trans. Cyber-Phys. Syst, vol. 4, hierarchical distributed control strategy for cooperative intersection no. 4, pp. 1–27, 2020, doi: 10.1145/3407903. 

considering priority negotiation,” IEEE Trans. Veh. Technol., vol. 70, 

\[37\] E. Namazi, J. Li, and C. Lu, “Intelligent intersection management no. 7, pp. 6438–6449, 2021, doi: 10.1109/TVT.2021.3086563. 

systems considering autonomous vehicles: A systematic literature re-

\[58\] R. Lloret-Batlle and R. Jayakrishnan, “Envy-minimizing pareto effi-view,” IEEE Access, vol. 7, pp. 91 946–91 965, 2019, doi: 10.1109/AC-

cient intersection control with brokered utility exchanges under user

CESS.2019.2927412. 

heterogeneity,” Transp. Res. Part B, Methodol., vol. 94, pp. 22–42, 

\[38\] M. Al-Turki, N. T. Ratrout, S. M. Rahman, and K. J. Assi, “Signalized 2016, doi: 10.1016/j.trb.2016.08.014. 

intersection control in mixed autonomous and regular vehicles traffic

\[59\] H. M. Abdelghaffar and H. A. Rakha, “Development and testing of environment–a critical review focusing on future control,” IEEE Access, a novel game theoretic de-centralized traffic signal controller,” IEEE

2022, doi: 10.1109/ACCESS.2022.3148706. 

Trans. Intell. Transp. Syst., vol. 22, no. 1, pp. 231–242, 2019, doi:

\[39\] M. S. Shirazi and B. T. Morris, “Looking at intersections: a survey of

10.1109/TITS.2019.2955918. 

intersection monitoring, behavior and safety analysis of recent studies,” 

\[60\] Z. Sun, X. Yao, Z. Qin, P. Zhang, and Z. Yang, “Modeling car-IEEE Trans. Intell. Transp. Syst., vol. 18, no. 1, pp. 4–24, 2016, doi: following heterogeneities by considering leader–follower compositions

10.1109/TITS.2016.2568920. 

and driving style differences,” Transp. Res. Rec., vol. 2675, no. 11, pp. 

\[40\] Z. Zhong, M. Nejad, and E. E. Lee, “Autonomous and semiautonomous 851–864, 2021, doi: 10.1177/03611981211020006. 

intersection management: A survey,” IEEE Intell. Transp. Syst. Mag., 

\[61\] L. Zhang, X. W. huang, and W. M. Wu, “The analysis of vol. 13, no. 2, pp. 53–70, 2020, doi: 10.1109/MITS.2020.3014074. 

driver’s

behavior

in

non-signalized

intersection

based

on

the

\[41\] C. Iliopoulou, K. Kepaptsoglou, and E. I. Vlahogianni, “A survey on game,” Appl. Mech. Mater., vol. 505, pp. 1157–1162, 2014, doi: market-inspired intersection control methods for connected vehicles,” 

10.4028/www.scientific.net/AMM.505-506.1157. 

IEEE Intell. Transp. Syst. Mag., vol. 15, no. 2, pp. 162–176, 2022, doi:

\[62\] Y. Zhang, R. Hao, T. Zhang, X. Chang, Z. Xie, and Q. Zhang, “A

10.1109/MITS.2022.3203573. 

trajectory optimization-based intersection coordination framework for

\[42\] R. B. Myerson, Game theory: Analysis of conflict. Harvard University cooperative autonomous vehicles,” IEEE Trans. Intell. Transp. Syst., Press, 1997. 

2021, doi: 10.1109/TITS.2021.3131570. 

\[43\] A. Ji and D. Levinson, “A review of game theory models of lane

\[63\] B. Wolshon, A. Pande et al., Traffic engineering handbook. 

John

changing,” Transportmetrica A, Transport Sci., vol. 16, no. 3, pp. 1628–

Wiley & Sons, 2016. 

1647, 2020, doi: 10.1080/23249935.2020.1770368. 

\[64\] F. Zhu and S. V. Ukkusuri, “A linear programming formulation for

\[44\] C. A. Kamhoua, C. D. Kiekintveld, F. Fang, and Q. Zhu, Game theory autonomous intersection control within a dynamic traffic assignment and machine learning for cyber security. 

John Wiley & Sons, 2021. 

and connected vehicle environment,” Transp. Res. Part C, Emerg. 

\[45\] F. Ahmad, O. Almarri, Z. Shah, and L. Al-Fagih, “Game the-Technol., vol. 55, pp. 363–378, 2015, doi: 10.1016/j.trc.2015.01.006. 

ory applications in traffic management: A review of authority-based

\[65\] M. W. Hancock and B. Wright, “A policy on geometric design of travel modelling,” Travel Behav. Soc., vol. 32, p. 100585, 2023, doi: highways and streets,” American Association of State Highway and

10.1016/j.tbs.2023.100585. 

Transportation Officials: Washington, DC, USA, vol. 3, 2013. 

\[46\] Q. Zhang, R. Langari, H. E. Tseng, D. Filev, S. Szwabowski, and

\[66\] L. A. Rodegerdts, B. L. Nevers, B. Robinson, J. Ringert, P. Koonce, S. Coskun, “A game theoretic model predictive controller with aggres-J. Bansen, T. Nguyen, J. McGill, D. Stewart, J. Suggett et al., siveness estimation for mandatory lane change,” IEEE Trans. Intell. 

“Signalized intersections: informational guide,” United States. Federal Veh., vol. 5, no. 1, pp. 75–89, 2020, doi: 10.1109/TIV.2019.2955367. 

Highway Administration, Tech. Rep., 2004. 

\[47\] A. Ji and D. Levinson, “Estimating the social gap with a game theory

\[67\] K. H. N. Bui, J. E. Jung, and D. Camacho, “Game theoretic approach model of lane changing,” IEEE Trans. Intell. Transp. Syst., vol. 22, on Real-time decision making for IoT-based traffic light control,” 

no. 10, pp. 6320–6329, 2020, doi: 10.1109/TITS.2020.2991242. 

Concurrency Comput. Pract. Exper., vol. 29, no. 11, 2017, doi:

\[48\] A. Ji, M. Ramezani, and D. Levinson, “Pricing lane changes,” Transp. 

10.1002/cpe.4077. 

Res. Part C, Emerg. Technol., vol. 149, p. 104062, 2023, doi:

10.1016/j.trc.2023.104062. 

\[68\] Y. Zhao, Y. Liang, J. Hu, and Z. Zhang, “Traffic Signal Control

\[49\] B. Wang, Z. Li, S. Wang, M. Li, and A. Ji, “Modeling bounded for Isolated Intersection Based on Coordination Game and Pareto rationality in discretionary lane change with the quantal response Efficiency,” in Proc. 2019 IEEE Intell. Transp. Syst. Conf., Auckland, equilibrium of game theory,” Transp. Res. Part B, Methodol., vol. 164, New Zealand, 2019, pp. 3508–3513, doi: 10.1109/ITSC.2019.8917165. 

pp. 145–161, 2022, doi: 10.1016/j.trb.2022.08.008. 

\[69\] M. Khanjary, “Using game theory to optimize traffic light of an inter-

\[50\] S. Karimi, A. Karimi, and A. Vahidi, “Level-k reasoning, deep section,” in Proc. 14th Int. Symp. Comput. Intell. Inform., Budapest, reinforcement learning, and monte carlo decision process for fast Hungary, 2013, pp. 249–253, doi: 10.1109/CINTI.2013.6705201. 

and safe automated lane change and speed management,” IEEE

\[70\] N. Li, I. Kolmanovsky, A. Girard, and Y. Yildiz, “Game theoretic Trans. Intell. Veh., vol. 8, no. 6, pp. 3556–3571, 2023, doi: modeling of vehicle interactions at unsignalized intersections and ap-

10.1109/TIV.2023.3265311. 

plication to autonomous vehicle control,” in Proc. Annu. Amer. Control

\[51\] Z. Sun, Z. Qin, R. Ma, T. Huang, Z. Gao, and A. Ji, “Mi-Conf. \(ACC\), 2018, pp. 3215–3220, doi: 10.23919/ACC.2018.8430842. 

croscopic right-of-way trading mechanism for cooperative decision-

\[71\] M. Elhenawy, A. A. Elbery, A. A. Hassan, and H. A. Rakha, “An making: Theories and preliminary results,” SSRN Electron. J., 2023, intersection game-theory-based traffic control algorithm in a connected doi: 10.2139/ssrn.4571173. 

vehicle environment,” in Proc. IEEE 18th Int. Conf. Intell. Transp. Syst, 

\[52\] X. Liao, X. Zhao, Z. Wang, K. Han, P. Tiwari, M. J. Barth, and G. Wu, Gran Canaria, Spain, 2015, pp. 343–347, doi: 10.1109/ITSC.2015.65. 

“Game theory-based ramp merging for mixed traffic with unity-sumo

\[72\] C. Cheng, Z. Yang, and D. Yao, “A speed guide model for collision co-simulation,” IEEE Trans. Syst. Man Cybern.: Syst., vol. 52, no. 9, avoidance in non-signalized intersections based on reduplicate game pp. 5746–5757, 2021, doi: 10.1109/TSMC.2021.3131431. 

theory,” in Proc. IEEE Intell. Vehicles Symp. \(IV\), Changshu, China, 

\[53\] W. Li, F. Qiu, L. Li, Y. Zhang, and K. Wang, “Simulation of 2018, pp. 1614–1619, doi: 10.1109/IVS.2018.8500502. 

vehicle interaction behavior in merging scenarios: A deep max-

\[73\] X. Chen, Y. Sun, Y. Ou, X. Zheng, Z. Wang, and M. Li, “A conflict imum entropy- inverse reinforcement learning method combined decision model based on game theory for intelligent vehicles at urban with game theory,” IEEE Trans. Intell. Veh., pp. 1–15, 2023, doi: unsignalized intersections,” IEEE Access, vol. 8, pp. 189 546–189 555, 

10.1109/TIV.2023.3323138. 

2020, doi: 10.1109/ACCESS.2020.3031674. 

\[54\] Z. Sun, T. Huang, Z. Qin, and Z. Gao, “Microscopic right-of-way

\[74\] X. Jin, K. Li, Q.-S. Jia, H. Xia, Y. Bai, and D. Ren, “A game-trading mechanism for cooperative decision-making: A ramp merging theoretic reinforcement learning approach for adaptive interaction at example,” in Proc. Transp. Res. Board 99th Annu. Meeting \(TRB\), intersections,” in Proc. Chin. Autom. Congr. \(CAC\), Shanghai, China, Washington, DC, 2020. 

2020, pp. 4451–4456, doi: 10.1109/CAC51589.2020.9327245. 

\[55\] M. O. Sayin, C.-W. Lin, S. Shiraishi, J. Shen, and T. Bas¸ar, 

\[75\] R. Tian, S. Li, N. Li, I. Kolmanovsky, A. Girard, and Y. Yildiz, “Adap-

“Information-driven autonomous intersection control via incentive tive game-theoretic decision making for autonomous vehicle control at

15

roundabouts,” in Proc. IEEE Conf. Decis. Control \(CDC\), Miami, FL, 

\[95\] D. Li, A. Liu, H. Pan, and W. Chen, “Safe, efficient and socially-USA, Dec. 2018, pp. 321–326, doi: 10.1109/CDC.2018.8619275. 

compatible decision of automated vehicles: a case study of unsignal-

\[76\] I. H. Zohdy and H. Rakha, “Game theory algorithm for intersection-ized intersection driving,” Automot. Innov., pp. 1–16, 2023, doi: based cooperative adaptive cruise control \(cacc\) systems,” in Proc. 

10.1007/s42154-023-00219-2. 

IEEE 15th Int. Conf. Intell. Transp. Syst., Anchorage, AK, USA, Sep. 

\[96\] M. Liu, Y. Wan, F. L. Lewis, S. Nageshrao, and D. Filev, “A three-level 2012, pp. 1097–1102, doi: 10.1109/ITSC.2012.6338644. 

game-theoretic decision-making framework for autonomous vehicles,” 

\[77\] Z. Yang, H. Huang, D. Yao, and Y. Zhang, “Cooperative driving model IEEE Trans. Intell. Transp. Syst., vol. 23, no. 11, pp. 20 298–20 308, for non-signalized intersections based on reduplicate dynamic game,” in 2022, doi: 10.1109/TITS.2022.3172926. 

Proc. IEEE 19th Int. Conf. Intell. Transp. Syst. \(ITSC\), Rio de Janeiro, 

\[97\] D. Zhu, N. N. Sze, Z. Feng, and Z. Yang, “A two-stage safety Nov. 2016, pp. 1366–1371, doi: 10.1109/ITSC.2016.7795735. 

evaluation model for the red light running behaviour of pedestrians

\[78\] H. Fan, B. Jia, J. Tian, and L. Yun, “Characteristics of traffic flow using the game theory,” Safety Sci., vol. 147, no. November 2021, p. 

at a non-signalized intersection in the framework of game theory,” 

105600, 2022, doi: 10.1016/j.ssci.2021.105600. 

Phys. A, Statist. Mech. Appl., vol. 415, pp. 172–180, 2014, doi:

\[98\] C. Yang, J. Wang, and J. Dong, “Capacity Model of Ex-

10.1016/j.physa.2014.07.031. 

clusive Right-Turn Lane at Signalized Intersection considering

\[79\] W. Zhang and W. Chen, “Dilemma game in a cellular automaton model Pedestrian-Vehicle Interaction,” J. Adv. Transp., vol. 2020, 2020, doi: with a non-signalized intersection,” Eur. Phys. J. B, vol. 85, no. 2, pp. 

10.1155/2020/1534564. 

1–8, 2012, doi: 10.1140/epjb/e2012-20904-x. 

\[99\] H. Wang, Q. Meng, S. Chen, and X. Zhang, “Competitive and

\[80\] L. Wang, N. G. Xie, and R. Meng, “Dirty-face game analysis on cooperative behaviour analysis of connected and autonomous vehi-mixed traffic flow at unsignalized intersection,” Adv. Mat. Res., vol. 

cles across unsignalised intersections: A game-theoretic approach,” 

201, pp. 2119–2125, 2011, doi: 10.4028/www.scientific.net/AMR.201-

Transp. Res. Part B, Methodol., vol. 149, pp. 322–346, 2021, doi:

203.2119. 

10.1016/j.trb.2021.05.007. 

\[81\] M. Lemmer, S. Schwab, and S. Hohmann, “Driver interaction at

\[100\] Y. Rahmati, M. K. Hosseini, and A. Talebpour, “Helping Automated intersections: A hybrid dynamic game based model,” in Proc. IEEE

Vehicles With Left-Turn Maneuvers: A Game Theory-Based Decision Int. Conf. Syst., Man, Cybern. \(SMC\), Toronto, ON, Canada, Oct. 2020, Framework for Conflicting Maneuvers at Intersections,” IEEE Trans. 

pp. 2269–2276, doi: 10.1109/SMC42975.2020.9283079. 

Intell. Transp. Syst., pp. 1–14, 2021, doi: 10.1109/TITS.2021.3108409. 

\[82\] P. Hang, C. Huang, Z. Hu, and C. Lv, “Driving conflict resolu-

\[101\] D. Arbis, V. V. Dixit, and T. H. Rashidi, “Impact of risk atti-tion of autonomous vehicles at unsignalized intersections: A differ-tudes and perception on game theoretic driving interactions and ential game approach,” IEEE/ASME Trans. Mechatron., 2022, doi: safety,” Accid. Anal. Prev., vol. 94, pp. 135–142, 2016, doi:

10.1109/TMECH.2022.3174273. 

10.1016/j.aap.2016.05.027. 

\[83\] X. Qiu, L. Yang, L. Zhang, and Z. Huang, “The non-signal intersection

\[102\] X. Lu, H. Zhao, C. Li, B. Gao, and H. Chen, “A game-theoretic traffic behavior analysis based on game theory,” in Proc. 4th Int. Symp. 

approach on conflict resolution of autonomous vehicles at unsignal-Comput. Intell. Design \(ISCID\), vol. 2, Hangzhou, China, Oct. 2011, ized intersections,” IEEE Trans. Intell. Transp. Syst., 2023, doi: pp. 122–124, doi: 10.1109/ISCID.2011.132. 

10.1109/TITS.2023.3285597. 

\[84\] S. I. Bouderba and N. Moussa, “Evolutionary dilemma game

\[103\] S. Jia, Y. Zhang, X. Li, X. Na, Y. Wang, B. Gao, B. Zhu, and for conflict resolution at unsignalized traffic intersection,” Int. 

R. Yu, “Interactive decision-making with switchable game modes for J. Mod. Phys. C, vol. 30, no. 02n03, p. 1950018, 2019, doi: automated vehicles at intersections,” IEEE Trans. Intell. Transp. Syst., 

10.1142/S0129183119500189. 

2023, doi: 10.1109/TITS.2023.3286075. 

\[85\] J. Cai, P. Hang, and C. Lv, “Game theoretic modeling and decision

\[104\] F. Molinari and J. Raisch, “Automation of Road Intersections Using making for connected vehicle interactions at urban intersections,” in Consensus-based Auction Algorithms,” in Proc. Annu. Amer. Control Proc. IEEE Int. Conf. Adv. Robot. Mech \(ICARM\), Chongqing, China, Conf. \(ACC\), vol. 2018-June, Milwaukee, WI, USA, Jun. 2018, pp. 

Jul. 2021, pp. 874–880, doi: 10.1109/ICARM52023.2021.9536147. 

5994–6001, doi: 10.23919/ACC.2018.8430865. 

\[86\] W. Qi, H. Wen, C. Fu, and M. Song, “Game theory model of traffic par-

\[105\] Y. Xu, D. Li, and Y. Xi, “A Game-Based Adaptive Traffic Sig-ticipants within amber time at signalized intersection,” Comput. Intell. 

nal Control Policy Using the Vehicle to Infrastructure \(V2I\),” IEEE

Neurosci., vol. 2014, pp. 56–56, 2014, doi: 10.1155/2014/756235. 

Trans. Veh. Technol., vol. 68, no. 10, pp. 9425–9437, 2019, doi:

\[87\] G. Liu, B. Xiao, and D. Li, “Game-theory based driving deci-

10.1109/TVT.2019.2933317. 

sion algorithm for intersection scenarios considering driver irra-tionality,” in

\[106\] M. Vasirani and S. Ossowski, “A Market-Inspired Approach for Inter-Proc. IEEE 4th CAA Int. Conf. Veh. Control In-

section Management in Urban Road Traffic Networks,” J. Artif. Intell. 

tell \(CVCI\), Hangzhou, China, Dec. 2020, pp. 747–752, doi:

10.1109/CVCI51460.2020.9338515. 

Res., vol. 43, pp. 621–659, 2012, doi: 10.1613/jair.3560. 

\[88\] D. Li, G. Liu, and B. Xiao, “Human-like driving decision at

\[107\] C. Cheng, D. Yao, Y. Zhang, J. Li, and Y. Guo, “A Vehicle Passing unsignalized intersections based on game theory,” Proc. Inst. 

Model in Non-signalized Intersections based on Non-cooperative Game Mech. Eng., Part D: J. Automob. Eng., pp. 159–173, 2022, doi: Theory,” Proc. 2019 IEEE Intell. Transp. Syst. Conf., pp. 2286–2291, 

10.1177/09544070221075423. 

Oct. 2019, doi: 10.1109/ITSC.2019.8917396. 

\[89\] A. Baz, P. Yi, and A. Qurashi, “Intersection control and delay opti-

\[108\] G. Cabri, L. Gherardini, M. Montangero, and F. Muzzini, “About mization for autonomous vehicles flows only as well as mixed flows auction strategies for intersection management when human-driven with ordinary vehicles,” Vehicles, vol. 2, no. 3, pp. 523–541, 2020, doi: and autonomous vehicles coexist,” Multimed. Tools. Appl., pp. 15 921–

10.3390/vehicles2030029. 

15 936, 2021, doi: 10.1007/s11042-020-10222-y. 

\[90\] H. Wei, L. Mashayekhy, and J. Papineau, “Intersection management

\[109\] D. Carlino, S. D. Boyles, and P. Stone, “Auction-based autonomous for connected autonomous vehicles: A game theoretic framework,” in intersection management,” in Proc. 16th Int. IEEE Conf. Intell. Transp. 

Proc. 21st Int. Conf. Intell. Transp. Syst. \(ITSC\), Maui, HI, USA, Nov. 

Syst. \(ITSC\), The Hague, Netherlands, Oct. 2013, pp. 529–534, doi: 2018, doi: 10.1109/ITSC.2018.8569307. 

10.1109/ITSC.2013.6728285. 

\[91\] M. Liu, Y. Chen, G. Lu, and Y. Wang, “Modeling crossing behavior

\[110\] H. Schepperle and K. Böhm, “Auction-based traffic management: of drivers at unsignalized intersections with consideration of risk Towards effective concurrent utilization of road intersections,” in Proc. 

perception,” Transp. Res. Part F, Traffic Psychol. Behav., vol. 45, pp. 

2008 10th IEEE Conf. E-Commerce Tech. 5th IEEE Conf. Enterprise 14–26, 2017, doi: 10.1016/j.trf.2016.11.012. 

Comput., E-Commerce E-Services, Arlington, VA, USA, 2008, pp. 

\[92\] M. Lemmer, S. Schwab, and S. Hohmann, “Driver interaction at 105–112, doi: 10.1109/CECandEEE.2008.88. 

intersections: A hybrid dynamic game based model,” in Proc. IEEE

\[111\] P. Hang, C. Huang, Z. Hu, and C. Lv, “Decision making for connected Int. Conf. Syst., Man, Cybern. \(SMC\), Toronto, ON, Canada, Oct. 2020, automated vehicles at urban intersections considering social and indi-doi: 10.1109/SMC42975.2020.9283079. 

vidual benefits,” IEEE Trans. Intell. Transp. Syst., vol. 23, no. 11, pp. 

\[93\] D. Lin and S. E. Jabari, “Comparative analysis of economic instruments 22 549–22 562, 2022, doi: 10.1109/TITS.2022.3209607. 

in intersection operation: A user-based perspective,” in Proc. 2020

\[112\] N. Suriyarachchi, R. Chandra, J. S. Baras, and D. Manocha, IEEE 23rd Int. Conf. Int. Transp. Syst. \(ITSC\), Rhodes, Greece, Sep. 

“Gameopt: Optimal real-time multi-agent planning and control 2020, pp. 1–6, doi: 10.1109/ITSC45102.2020.9294641. 

for dynamic intersections,” in Proc. IEEE 25th Int. Conf. In-

\[94\] M. O. Sayin, C.-W. Lin, S. Shiraishi, and T. Bas¸ar, “Reliable intersec-tell. Transp. Syst., Macau, China, Nov. 2022, pp. 2599–2606, doi: tion control in non-cooperative environments,” in Proc. Annu. Amer. 

10.1109/ITSC55140.2022.9921968. 

Control Conf. \(ACC\), Milwaukee, WI, USA, Jun. 2018, pp. 609–614, 

\[113\] R. Chandra and D. Manocha, “GamePlan: Game-Theoretic Multi-doi: 10.23919/ACC.2018.8430809. 

Agent Planning with Human Drivers at Intersections, Roundabouts, 

16

and Merging,” IEEE Robot. Autom. Lett., vol. 7, no. 2, pp. 2676–2683, proach,” Eng. Appl. Artif. Intell., vol. 43, pp. 147–156, 2015, doi: 2022, doi: 10.1109/LRA.2022.3144516. 

10.1016/j.engappai.2015.04.009. 

\[114\] F. Molinari, A. M. Dethof, and J. Raisch, “Traffic automation in

\[132\] R. Castillo González, J. B. Clempner, and A. S. Poznyak, “Solving urban road networks using consensus-based auction algorithms for road traffic queues at controlled-signalized intersections in continuous-time intersections,” Proc. 18th Eur. Control Conf., pp. 3008–3015, Jun. 2019, Markov games,” Math. Comput. Simul., vol. 166, pp. 283–297, 2019, doi: 10.23919/ECC.2019.8796170. 

doi: 10.1016/j.matcom.2019.06.002. 

\[115\] R. Tian, N. Li, I. Kolmanovsky, Y. Yildiz, and A. R. Girard, “Game-

\[133\] L. H. Xu, X. H. Xia, and Q. Luo, “The study of reinforcement learning Theoretic Modeling of Traffic in Unsignalized Intersection Network for traffic self-adaptive control under multiagent Markov game environ-for Autonomous Vehicle Control Verification and Validation,” IEEE

ment,” Math. Probl. Eng., vol. 2013, 2013, doi: 10.1155/2013/962869. 

Trans. Intell. Transp. Syst., vol. 23, no. 3, pp. 2211–2226, 2022, doi:

\[134\] Y. Zhu, Z. He, and G. Li, “A bi-hierarchical game-theoretic approach

10.1109/TITS.2020.3035363. 

for network-wide traffic signal control using trip-based data,” IEEE

\[116\] M. W. Levin and S. D. Boyles, “Intersection auctions and reservation-Trans. Intell. Transp. Syst., vol. 23, no. 9, pp. 15 408–15 419, 2022, based control in dynamic traffic assignment,” Transp. Res. Rec., vol. 

doi: 10.1109/TITS.2022.3140511. 

2497, pp. 35–44, 2015, doi: 10.3141/2497-04. 

\[135\] M. Stryszowski, S. Longo, D. D’Alessandro, E. Velenis, G. Foros-

\[117\] M. Liu, S. Zhang, and L. Teng, “Method of Controlling Vehicles at tovsky, and S. Manfredi, “A Framework for Self-Enforced Op-Intersections Based on the Auction Algorithm,” J. Phys. Conf. Ser., vol. 

timal Interaction between Connected Vehicles,” IEEE Trans. In-1453, no. 1, 2020, doi: 10.1088/1742-6596/1453/1/012050. 

tell. Transp. Syst., vol. 22, no. 10, pp. 6152–6161, 2021, doi:

\[118\] H. Wang, Y. Li, and H. V. Zhao, “Performance analysis of

10.1109/TITS.2020.2988150. 

road intersections based on game theory and dynamic level-

\[136\] Z. Dai, H. Dong, and Q. Wang, “A multi-intersection coordinated k model,” Proc. IEEE Int. Conf Parallel Distrib. Process. With control algorithm based on game theory and maximal flow,” in Proc. 

Appl., 

Big

Data

Cloud

Comput., 

Sustain. 

Comput. 

Commun., 

IECON 39th Annu. Conf. IEEE Ind. Electron. Soc., Vienna, Nov. 2013, Social Comput. Netw. \(ISPA/BDCloud/SocialCom/SustainCom\), pp. 

pp. 3258–3263, doi: 10.1109/IECON.2013.6699650. 

1112–1119, Dec. 2020, doi: 10.1109/ISPA-BDCloud-SocialCom-

\[137\] R. P. Adkins, D. M. Mount, and A. A. Zhang, “A game-theoretic

SustainCom51426.2020.00166. 

approach for minimizing delays in autonomous intersections,” in Traffic

\[119\] C. Philippe, L. Adouane, A. Tsourdos, H.-S. Shin, and B. Thuilot, and Granular Flow ’17, S. H. Hamdar, Ed. 

Cham: Springer Interna-

“Probability collectives algorithm applied to decentralized intersection tional Publishing, 2019, pp. 131–139. 

coordination for connected autonomous vehicles,” in Proc. IEEE Intell. 

\[138\] A. J. Malo Tamayo, A. Poznyak, and I. Á. Villalobos, “Optimization Vehicles Symp. \(IV\), Paris, France, Jun. 2019, pp. 1928–1934, doi: and game at an urban intersection,” IFAC Proc. Vol., no. 1983, pp. 

10.1109/IVS.2019.8813827. 

526–530, 2009, doi: 10.3182/20090902-3-US-2007.0030. 

\[120\] W. Schwarting, A. Pierson, J. Alonso-Mora, S. Karaman, and D. Rus, 

\[139\] J. Guo and I. Harmati, “Evaluating semi-cooperative Nash/Stackelberg

“Social behavior for autonomous vehicles,” Proc. Natl. Acad. Sci., vol. 

Q-learning for traffic routes plan in a single intersection,” Con-116, no. 50, pp. 2492–24 978, 2019, doi: 10.1073/pnas.1820676116. 

trol Eng. Pract., vol. 102, no. June, p. 104525, 2020, doi:

\[121\] A. Sarkar and K. Czarnecki, “Solution Concepts in Hierarchical Games

10.1016/j.conengprac.2020.104525. 

Under Bounded Rationality With Applications to Autonomous Driv-

\[140\] M. Mashayekhi and G. F. List, “A multiagent auction-based approach ing,” in Proc. 35th Conf. Artif. Intell. \(AAAI\), vol. 6B, no. Samuelson for modeling of signalized intersections,” in Proc. IJCAI Workshops 1995, 2021, pp. 5698–5708, doi: 10.1609/aaai.v35i6.16715. 

Synergies Between Multiagent Syst., Mach. Learn. Complex Syst., 2015. 

\[122\] M. Yuan, J. Shan, and K. Mi, “Deep reinforcement learning

\[141\] J. Guo and I. Harmati, “Optimization of traffic signal control with based game-theoretic decision-making for autonomous vehicles,” 

different game theoretical strategies,” in Proc. 2019 23rd Int. Conf. 

IEEE Robot. Autom. Lett., vol. 7, no. 2, pp. 818–825, 2021, doi: Syst. Theory, Control Comput., Sinaia, Romania, Oct. 2019, pp. 750–

10.1109/LRA.2021.3134249. 

755, doi: 10.1109/ICSTCC.2019.8885458. 

\[123\] D. Rey, M. W. Levin, and V. V. Dixit, “Online incentive-compatible

\[142\] S. Moya and J. Escobar, “Stackelberg-Nash equilibrium in a traffic con-mechanisms for traffic intersection auctions,” Eur. J. Oper. Res., vol. 

trol problem at an intersection on a priority road,” IMA J. Math. Control 293, no. 1, pp. 229–247, 2021, doi: 10.1016/j.ejor.2020.12.030. 

Inf., vol. 32, no. 1, pp. 161–194, 2015, doi: 10.1093/imamci/dnt036. 

\[124\] L. Tan, X. Zhao, D. Hu, Y. Shang, and W. Ren, “A study of single

\[143\] J. Guo and I. Harmati, “Comparison of game theoretical strategy intersection traffic signal control based on two-player cooperation game and reinforcement learning in traffic light control,” Periodica Poly-model,” in Proc. Int. Conf. Inf. Eng, vol. 2, Beidai, China, Aug. 2010, technica Transp. Eng., vol. 48, no. 4, pp. 313–319, 2020, doi: pp. 322–327, doi: 10.1109/ICIE.2010.172. 

10.3311/PPTR.15923. 

\[125\] L. Tan, Y. Wang, Q. Wang, Y. Sun, and Z. Li, “Multi-phase signal con-

\[144\] Y. Narahari, Game theory and mechanism design. 

World Scientific, 

trol method for single intersection based on multi-person cooperative 2014, vol. 4. 

game theory,” in Proc. 2017 2nd Jt. Int. Inf. Technol. Mech. Electron. 

\[145\] J. C. Hayward, “Near-miss determination through use of a scale of Eng. Conf. \(JIMEC 2017\), Oct. 2017, pp. 335–339, doi: 10.2991/jimec-

danger,” Highway Res. Rec., no. 384, 1972. 

17.2017.74. 

\[146\] Y. Zhang, D. Yao, T. Z. Qiu, L. Peng, and Y. Zhang, “Pedestrian

\[126\] K. H. Nam Bui and J. J. Jung, “Cooperative game-theoretic safety analysis in mixed traffic conditions using video data,” IEEE

approach to traffic flow optimization for multiple intersections,” 

Trans. Intell. Transp. Syst., vol. 13, no. 4, pp. 1832–1844, 2012, doi: Comput. 

Electr. 

Eng., 

vol. 

71, 

pp. 

1012–1024, 

2018, 

doi:

10.1109/TITS.2012.2210881. 

10.1016/j.compeleceng.2017.10.016. 

\[147\] A. Varhelyi, “Drivers’ speed behaviour at a zebra crossing: a case

\[127\] H. Dong and Z. Dai, “A multi intersections signal coordinate study,” Accid. Anal. Prev., vol. 30, no. 6, pp. 731–743, 1998, doi: control method based on game theory,” Proc. Int. Conf. Elec-

10.1016/S0001-4575\(98\)00026-8. 

tron., Commun. Control \(ICECC\), no. 3, pp. 1232–1235, 2011, doi:

\[148\] H. M. Abdelghaffar and H. A. Rakha, “A novel decentralized game-

10.1109/ICECC.2011.6066604. 

theoretic adaptive traffic signal controller: Large-scale testing,” Sensors, 

\[128\] J. Raphael, E. I. Sklar, and S. Maskell, “An intersection-centric auction-vol. 19, no. 10, p. 2282, 2019, doi: 10.3390/s19102282. 

based traffic signal control framework,” in Agent-Based Modeling of

\[149\] P. Hao, X. J. Ban, D. Guo, and Q. Ji, “Cycle-by-cycle intersec-Sustainable Behaviors. 

Cham, Switzerland: Springer International

tion queue length distribution estimation using sample travel times,” 

Publishing, 2017, pp. 121–142, doi: 10.1007/978-3-319-46331-5 6. 

Transp. Res. Part B, Methodol., vol. 68, pp. 185–204, 2014, doi:

\[129\] X.-h. Xia, “Adaptive traffic signal coordinated timing decision for

10.1016/j.trb.2014.06.004. 

adjacent intersections with chicken game,” in Intelligent Transport

\[150\] X. J. Ban, P. Hao, and Z. Sun, “Real time queue length estimation Systems – From Research and Development to the Market Uptake, for signalized intersections using travel times from mobile sensors,” 

T. Kováčiková, Ľ. Buzna, G. Pourhashem, G. Lugano, Y. Cornet, and Transp. Res. Part C, Emerg. Technol., vol. 19, no. 6, pp. 1133–1156, N. Lugano, Eds. 

Cham: Springer International Publishing, 2018, pp. 

2011, doi: 10.1016/j.trc.2011.01.002. 

239–251, doi: 10.1007/978-3-319-93710-6 25. 

\[151\] M. Barth, F. An, J. Norbeck, and M. Ross, “Modal emissions modeling:

\[130\] M. Abdoos, “A cooperative multiagent system for traffic signal A physical approach,” Transp. Res. Rec., vol. 1520, no. 1, pp. 81–88, control using game theory and reinforcement learning,” IEEE In-1996, doi: 10.1177/0361198196152000110. 

tell. Transp. Syst. Mag., vol. 13, no. 4, pp. 6–16, 2021, doi:

\[152\] H. Rakha, K. Ahn, and A. Trani, “Development of VT-Micro model

10.1109/MITS.2020.2990189. 

for estimating hot stabilized light duty vehicle and truck emissions,” 

\[131\] J. B. Clempner and A. S. Poznyak, “Modeling the multi-traffic Transp. Res. Part D, Transp. Environ., vol. 9, no. 1, pp. 49–74, 2004, signal-control synchronization: A Markov chains game theory ap-doi: 10.1016/S1361-9209\(03\)00054-3. 

17

\[153\] Z. Wang, G. Wu, and G. Scora, “Movestar: An open-source vehicle

\[179\] Y. Wu, H. Chen, and F. Zhu, “Dcl-aim: Decentralized coordination fuel and emission model based on usepa moves,” arXiv preprint, 2020, learning of autonomous intersection management for connected and doi: 10.48550/arXiv.2008.04986. 

automated vehicles,” Transp. Res. Part C, Emerg. Technol., vol. 103, 

\[154\] A. Barkley, The economics of food and agricultural markets. 

New

pp. 246–260, 2019, doi: 10.1016/j.trc.2019.04.012. 

Prairie Press, 2019. 

\[180\] D. I. Robertson and R. D. Bretherton, “Optimizing networks of traffic

\[155\] M. Quincampoix, Differential Games. 

New York, NY: Springer New

signals in real time-the scoot method,” IEEE Trans. Veh. Technol., York, 2012, pp. 854–861, doi: 10.1007/978-1-4614-1800-9 55. 

vol. 40, no. 1, pp. 11–15, 1991, doi: 10.1109/25.69966. 

\[156\] M. E. Mkiramweni, C. Yang, J. Li, and W. Zhang, “A survey of

\[181\] S.-B. Cools, C. Gershenson, and B. D’Hooghe, Self-Organizing Traffic game theory in unmanned aerial vehicles communications,” IEEE

Lights: A Realistic Simulation. 

London: Springer London, 2013, pp. 

Commun. Surveys Tuts., vol. 21, no. 4, pp. 3386–3416, 2019, doi: 45–55, doi: 10.1007/978-1-4471-5113-5 3. 

10.1109/COMST.2019.2919613. 

\[182\] H. Wei, C. Chen, G. Zheng, K. Wu, V. Gayah, K. Xu, and

\[157\] T. S. Driessen, Cooperative games, solutions and applications. 

Z. Li, “Presslight: Learning max pressure control to coordinate traf-Springer Science & Business Media, 2013, vol. 3. 

fic signals in arterial network,” in Proc. 25th ACM SIGKDD Int. 

\[158\] J. Wilson, “Cooperative games with transferable utility,” in Wiley Conf. Knowl. Discovery Data Mining, 2019, pp. 1290–1298, doi: Encyclopedia of Operations Research and Management Science. John

10.1145/3292500.3330949. 

Wiley & Sons, Ltd, 2011, doi: 10.1002/9780470400531.eorms0199. 

\[183\] H. Wei, N. Xu, H. Zhang, G. Zheng, X. Zang, C. Chen, W. Zhang, 

\[159\] M. Maschler, S. Zamir, and E. Solan, Game theory. 

Cambridge

Y. Zhu, K. Xu, and Z. Li, “Colight: Learning network-level cooperation University Press, 2020. 

for traffic signal control,” in Proc. 28th ACM Int. Conf. Inf. Knowl. 

\[160\] J. F. Nash Jr, “The bargaining problem,” Econometrica: J. Econometric Manage., 2019, pp. 1913–1922, doi: 10.1145/3357384.3357902. 

Soc., pp. 155–162, 1950, doi: 10.2307/1907266. 

\[184\] T. Chu, J. Wang, L. Codecà, and Z. Li, “Multi-agent deep rein-

\[161\] P. Milgrom and P. R. Milgrom, Putting auction theory to work. 

forcement learning for large-scale traffic signal control,” IEEE Trans. 

Cambridge University Press, 2004. 

Intell. Transp. Syst., vol. 21, no. 3, pp. 1086–1095, 2019, doi:

\[162\] J. Nash Jr, “Non-cooperative games,” in Essays on Game Theory. 

10.1109/TITS.2019.2901791. 

Edward Elgar Publishing, 1996, pp. 22–33. 

\[185\] X. Zang, H. Yao, G. Zheng, N. Xu, K. Xu, and Z. Li, “Metalight: Value-based meta-reinforcement learning for traffic signal control,” in

\[163\] C. Luo, X. Zhou, and B. Lev, “Core, shapley value, nucleolus and Proc. AAAI Conf. Artif. Intell., vol. 34, no. 01, 2020, pp. 1153–1160, nash bargaining solution: A survey of recent developments and ap-doi: 10.1609/aaai.v34i01.5467. 

plications in operations management,” Omega, p. 102638, 2022, doi:

\[186\] F.-X. Devailly, D. Larocque, and L. Charlin, “Ig-rl: Inductive graph

10.1016/j.omega.2022.102638. 

reinforcement learning for massive-scale traffic signal control,” IEEE

\[164\] M. Bowling and M. Veloso, “Multiagent learning using a variable Trans. Intell. Transp. Syst., vol. 23, no. 7, pp. 7496–7507, 2021, doi: learning rate,” Artif. Intell., vol. 136, no. 2, pp. 215–250, 2002, doi:

10.1109/TITS.2021.3070835. 

10.1016/S0004-3702\(02\)00121-2. 

\[187\] C. Chen, H. Wei, N. Xu, G. Zheng, M. Yang, Y. Xiong, K. Xu, 

\[165\] P. G. Balaji and D. Srinivasan, “An introduction to multi-agent and Z. Li, “Toward a thousand lights: Decentralized deep rein-systems,” in Innovations in multi-agent systems and applications-1. 

forcement learning for large-scale traffic signal control,” in Proc. 

Springer, 2010, pp. 1–27. 

AAAI Conf. Artif. Intell., vol. 34, no. 04, 2020, pp. 3414–3421, doi:

\[166\] A. Nowé, P. Vrancx, and Y.-M. D. Hauwere, “Game theory and multi-

10.1609/aaai.v34i04.5744. 

agent reinforcement learning,” in Reinforcement Learning. 

Springer, 

\[188\] A. Oroojlooy, M. Nazari, D. Hajinezhad, and J. Silva, “Attendlight: 2012, pp. 441–470. 

Universal attention-based reinforcement learning model for traffic

\[167\] S. El-Tantawy, B. Abdulhai, and H. Abdelgawad, “Multiagent rein-signal

control,” 

in

Proc. 

Adv. 

Neural

Inf. 

Process. 

Syst., 

forcement learning for integrated network of adaptive traffic signal H. Larochelle, M. Ranzato, R. Hadsell, M. Balcan, and H. Lin, controllers \(marlin-atsc\): methodology and large-scale application on Eds., vol. 33. 

Curran Associates, Inc., 2020, pp. 4079–4090. 

downtown toronto,” IEEE Trans. Intell. Transp. Syst., vol. 14, no. 3, 

\[Online\]. Available: https://proceedings.neurips.cc/paper files/paper/

pp. 1140–1150, 2013, doi: 10.1109/TITS.2013.2255286. 

2020/file/29e48b79ae6fc68e9b6480b677453586-Paper.pdf

\[168\] Y. Yang and J. Wang, “An overview of multi-agent reinforcement

\[189\] P. A. Lopez, M. Behrisch, L. Bieker-Walz, J. Erdmann, Y.-P. Flötteröd, learning from game theoretical perspective,” arXiv preprint, 2020, doi: R. Hilbrich, L. Lücken, J. Rummel, P. Wagner, and E. Wießner, 

10.48550/arXiv.2011.00583. 

“Microscopic traffic simulation using sumo,” in Proc. 21st Int. Conf. 

\[169\] L. Busoniu, R. Babuska, and B. De Schutter, “A comprehensive Intell. Transp. Syst. \(ITSC\), Maui, HI, USA, Nov. 2018, pp. 2575–2582, survey of multiagent reinforcement learning,” IEEE Trans. Syst., Man, doi: 10.1109/ITSC.2018.8569938. 

Cybern. C, Appl. Rev., vol. 38, no. 2, pp. 156–172, 2008, doi:

\[190\] G. D. Cameron and G. I. Duncan, “Paramics—parallel microscopic

10.1109/TSMCC.2007.913919. 

simulation of road traffic,” J. Supercomput., vol. 10, pp. 25–53, 1996, 

\[170\] O. Vinyals, T. Ewalds, S. Bartunov, P. Georgiev, A. S. Vezhnevets, doi: 10.1007/BF00128098. 

M. Yeo, A. Makhzani, H. Küttler, J. Agapiou, J. Schrittwieser et al., 

\[191\] J. Casas, J. L. Ferrer, D. Garcia, J. Perarnau, and A. Torday, Traffic

“Starcraft ii: A new challenge for reinforcement learning,” arXiv Simulation with Aimsun. 

New York, NY: Springer New York, 2010, 

preprint, 2017, doi: 10.48550/arXiv.1708.04782. 

pp. 173–232, doi: 10.1007/978-1-4419-6142-6 5. 

\[171\] J. Terry, B. Black, N. Grammel, M. Jayakumar, A. Hari, R. Sullivan, 

\[192\] M. Fellendorf and P. Vortisch, Microscopic Traffic Flow Simulator L. Santos, R. Perez, C. Horsch, C. Dieffendahl et al., “Pettingzoo: VISSIM. 

New York, NY: Springer New York, 2010, pp. 63–93, doi:

Gym for multi-agent reinforcement learning,” arXiv e-prints, 2020, doi:

10.1007/978-1-4419-6142-6 2. 

10.48550/arXiv.2009.14471. 

\[193\] H. Zhang, S. Feng, C. Liu, Y. Ding, Y. Zhu, Z. Zhou, W. Zhang, Y. Yu, 

\[172\] K. Zhang, Z. Yang, and T. Bas¸ar, “Multi-agent reinforcement learning: H. Jin, and Z. Li, “Cityflow: A multi-agent reinforcement learning A selective overview of theories and algorithms,” in Handbook of environment for large scale city traffic scenario,” in Proc. World Wide Reinforcement Learning and Control. 

Springer, 2021, pp. 321–384. 

Web Conf., 2019, pp. 3620–3624, doi: 10.1145/3308558.3314139. 

\[173\] A. L. Bazzan, “Opportunities for multiagent systems and multiagent

\[194\] C. Wu, A. R. Kreidieh, K. Parvate, E. Vinitsky, and A. M. Bayen, reinforcement learning in traffic control,” Auton. Agents Multi-Agent

“Flow: A modular learning framework for mixed autonomy traffic,” 

Syst., vol. 18, no. 3, pp. 342–375, 2009, doi: 10.1007/s10458-008-

IEEE Trans. Robot., vol. 38, no. 2, pp. 1270–1286, 2021, doi:

9062-9. 

10.1109/TRO.2021.3087314. 

\[174\] L. S. Shapley, “Stochastic games,” Proc. Nat. Acad. Sci., vol. 39, no. 10, 

\[195\] D. Garg, M. Chli, and G. Vogiatzis, “Traffic3d: A new traffic simulation pp. 1095–1100, 1953, doi: 10.1073/pnas.39.10.1095. 

paradigm,” in Proc. Int. Jt. Conf. Auton. Agents Multiagent Syst., 2019, 

\[175\] K. Dresner and P. Stone, “Multiagent traffic management: Opportuni-pp. 2354–2356, doi: 10.5555/3306127.3332110. 

ties for multiagent learning,” in Proc. Learn. Adaption Multiagent Syst. 

\[196\] M. Zhou, J. Luo, J. Villella, Y. Yang, D. Rusu, J. Miao, W. Zhang, Springer, 2006, pp. 129–138, doi: 10.1007/11691839. 

M. Alban, I. Fadakar, Z. Chen et al., “Smarts: Scalable multi-agent

\[176\] P. Koonce and L. Rodegerdts, “Traffic signal timing manual.” United reinforcement learning training school for autonomous driving,” arXiv States. Federal Highway Administration, Tech. Rep., 2008. 

preprint, 2020, doi: 10.48550/arXiv.2010.09776 . 

\[177\] P. Varaiya, “The max-pressure controller for arbitrary networks of

\[197\] E. Leurent, “An environment for autonomous driving decision-making,” 

signalized intersections,” in Advances in Dynamic Network Modeling

https://github.com/eleurent/highway-env, 2018. 

in Complex Transportation Systems. 

Springer, 2013, pp. 27–66. 

\[198\] M. Treiber and A. Kesting, “An open-source microscopic traffic sim-

\[178\] R. P. Roess, E. S. Prassas, and W. R. McShane, Traffic engineering. 

ulator,” IEEE Intell. Transp. Syst. Mag., vol. 2, no. 3, pp. 6–13, 2010, Prentice Hall, 2011. 

doi: 10.1109/MITS.2010.939208. 





18

\[199\] A. Dosovitskiy, G. Ros, F. Codevilla, A. Lopez, and V. Koltun, Guoyuan Wu \(M’09-SM’15\) received his Ph.D. de-

“Carla: An open urban driving simulator,” in Proc. Conf. Robot Learn. 

gree in mechanical engineering from the University

PMLR, 2017, pp. 1–16. \[Online\]. Available: https://proceedings.mlr. 

of California, Berkeley in 2010. Currently, he holds

press/v78/dosovitskiy17a.html

a Full Researcher and Adjunct Professor position at

\[200\] M. Bowling and M. Veloso, “An analysis of stochastic game theory for Bourns College of Engineering – Center for Envi-multiagent reinforcement learning,” Carnegie Mellon Univ., Pittsburgh, ronmental Research & Technology \(CE–CERT\) and

PA, USA, Tech. Rep. No. CMU-CS00-165, 2000. 

Department of Electrical & Computer Engineering

\[201\] F. J. Martinez, C.-K. Toh, J.-C. Cano, C. T. Calafate, and P. Manzoni, in the University of California at Riverside. His

“Emergency services in future intelligent transportation systems based research interest has been focused on the develop-on vehicular communication networks,” IEEE Intell. Transp. Syst. 

ment and evaluation of sustainable and intelligent

Mag., vol. 2, no. 2, pp. 6–20, 2010, doi: 10.1109/MITS.2010.938166. 

transportation system \(SITS\) technologies, including

connected and automated transportation systems \(CATS\), shared mobility, transportation electrification, optimization and control of vehicles, traffic VI. BIOGRAPHY SECTION

simulation, and energy/emissions measurement and modeling. Dr. Wu serves as an Associate Editor for a few prestigious journals. He is a member of National Academy of Inventors \(NAI\) and a member of a few Standing Committees of the Transportation Research Board \(TRB\). He is the recipient of 2020 Vincent Bendix Automotive Electronics Engineering Award, 2021

Arch T. Colwell Merit Award, and 2017-2020 IEEE-ITSM Outstanding Survey Paper Award. 

Peng Hao \(M’16\) received Ph.D. degree in trans-

Ziye Qin \(S’23\) is currently pursuing the Ph.D. 

portation engineering from Rensselaer Polytechnic

degree at the School of Transportation and Logistics, 

Institute in 2013. He is currently an Assistant

Southwest Jiaotong University, Chengdu, China. He

Research Engineer with the Transportation Sys-

is also a visiting student with the College of En-

tems Research Group, Center for Environmental

gineering, Center for Environmental Research and

Research and Technology, Bourns College of Engi-

Technology, University of California at Riverside, 

neering, University of California, Riverside, USA. 

Riverside, CA, USA. His research interests include

His research interests include connected vehicles, 

game theory and mechanism design, motion plan-

eco-approach and departure, sensor-aided modeling, 

ning and cooperative driving automation. 

shared mobility and traffic operations. 

Xishun Liao \(S’19\) received the Ph.D. degree in

electrical and computer engineering from University

of California at Riverside in 2023, the M.Eng. de-

gree in mechanical engineering from University of

Maryland at College Park in 2018, and the B.E. 

degree in mechanical engineering and automation

Ang Ji \(M’23\) received the Ph.D. degree from

from Beijing University of Posts and Telecommu-

the School of Civil Engineering, The University of

nications in 2016. He is currently a postdoctoral

Sydney, Australia, in 2022. He now serves as an As-

scholar at the University of California at Los An-

sistant Professor at the School of Transportation and

geles. His research focuses on motion planning and

Logistics, Southwest Jiaotong University, Chengdu, 

control, driver behavior, intelligent transportation

China. His research interests include connected au-

system technologies. 

tomated vehicles, deep/reinforcement learning, mi-

croscopic traffic modeling, and game-theoretic ap-

plications. 

Zhanbo Sun received his Ph.D. degree from Rens-

selaer Polytechnic Institute in 2014 and the B.E. 

degree from Tsinghua University in 2009. He is

now a Professor at the School of Transportation

and Logistics in Southwest Jiaotong University. His

research focuses on intelligent connected vehicles, 

green transportation, and rail transit. He has won

the Jeme Tianyou Railway Science and Technology

Award and the Best Paper Award of the International

Federation of Automatic Control \(IFAC TA 2019\). 



# Document Outline

+ Introduction 
+ Applications of Game Theory to Intersection Management  
	+ An Overview of Intersection Management 
	+ Game Theory-based Modeling  
		+ Players 
		+ Strategies 
		+ Payoff functions 

	+ Classifications of Game-theoretic Models  
		+ Non-cooperative games 
		+ Cooperative games 
		+ Complete information games 
		+ Incomplete information games 

	+ Game solutions  
		+ Nash equilibrium 
		+ Pareto efficiency 
		+ Shapley value 
		+ Core 


+ MULTI-AGENT REINFORCEMENT LEARNING AT INTERSECTIONS  
	+ A Brief Overview of Multi-agent Reinforcement Learning 
	+ Benchmarks and Simulation Platforms 
	+ Pros and Cons of Game Theory V.S. MARL 

+ Limitations and future research directions  
	+ Limitations of existing related studies 
	+ Future research directions 

+ Conclusion 
+ References 
+ Biography Section 
+ Biographies  
	+ Ziye Qin 
	+ Ang Ji 
	+ Zhanbo Sun 
	+ Guoyuan Wu 
	+ Peng Hao 
	+ Xishun Liao



