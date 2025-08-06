1

Evaluating Scenario-based Decision-making for Interactive Autonomous Driving Using Rational Criteria: A Survey

Zhen Tian†, Zhihao Lin†, Dezong Zhao⋆, Senior Member, IEEE, Wenjing Zhao, David Flynn, Member, IEEE, Shuja Ansari and Chongfeng Wei, Member, IEEE

Abstract—Autonomous vehicles \(AVs\) can significantly pro-With a safe decision-making system, AVs have the potential mote the advances in road transport mobility in terms of safety, to significantly decrease road crashes caused by human er-reliability, and decarbonization. However, ensuring safety and rors such as fatigue, distraction, and delayed reactions \[4\]. 

efficiency in interactive during within dynamic and diverse Moreover, AVs are capable of making optimal decisions faster environments is still a primary barrier to large-scale AV adoption. 

In recent years, deep reinforcement learning \(DRL\) has emerged than human drivers, thereby enhancing traffic efficiency \[5\]. 

as an advanced AI-based approach, enabling AVs to learn There are several typical driving scenarios, such as highways, decision-making strategies adaptively from data and interactions. 

roundabouts, on-ramping merging, and unsignalized intersec-DRL strategies are better suited than traditional rule-based meth-tions, each characterized by distinct road features and scenario-ods for handling complex, dynamic, and unpredictable driving specific requirements. Autonomous driving in such scenarios environments due to their adaptivity. However, varying driving scenarios present distinct challenges, such as avoiding obstacles is depicted in Fig. 1. For example, on-ramp merging involves on highways and reaching specific exits at intersections, requir-completing lane changes well in advance of any obstructed ing different scenario-specific decision-making algorithms. Many roadway, while navigating a roundabout requires seamlessly DRL algorithms have been proposed in interactive decision-exiting at the intended point. Achieving these scenario-based making. However, a rationale review of these DRL algorithms requirements relies heavily on precise and timely operational across various scenarios is lacking. Therefore, a comprehensive evaluation is essential to assess these algorithms from multiple decision-making in real time. Operational decision support perspectives, including those of vehicle users and vehicle manu-for AV driving includes perception, planning, and control facturers. This survey reviews the application of DRL algorithms modules. The perception module consists of onboard sensors in autonomous driving across typical scenarios, summarizing that continuously perceive the surrounding environment. The road features and recent advancements. The scenarios include perceived data is processed through perception algorithms, highways, on-ramp merging, roundabouts, and unsignalized intersections. Furthermore, DRL-based algorithms are evaluated such as YOLO methods \[6\], \[7\]. The planning module handles based on five rationale criteria: driving safety, driving efficiency, driving tasks based on scenario recognition. Subsequently, training efficiency, unselfishness, and interpretability \(DDTUI\). 

the motion planner generates discrete decisions and converts Each criterion of DDTUI is specifically analyzed in relation to them into feasible trajectories. These feasible trajectories are the reviewed algorithms. Finally, the challenges for future DRL-then transmitted to the control module to generate control based decision-making algorithms are summarized. 

commands, which are sent to the vehicle’s actuators. The Index Terms—Interactive autonomous driving, decision mak-actuators, including the steering wheel and pedals, receive and ing, deep reinforcement learning, typical scenarios, rationale evaluation. 

execute the control commands to drive the vehicle. 

The interactions between AVs and HDVs are complex and arXiv:2501.01886v1 \[cs.RO\] 3 Jan 2025

therefore continuous decision-making is required, such as lane I. INTRODUCTION

changes or braking \[8\]. The model-based, simple guidance, AUTONOMOUS vehicles \(AVs\) face significant chal- and learning-based methods are commonly used in interactive lenges in making reliable decisions when interacting with driving with HDVs. 

human-driven vehicles \(HDVs\). This challenge is primarily There are mainly four types of model-based approaches. 

due to the difficulty of accurately predicting the intentions The first model-based approach aims to predict the intentions of HDVs. Road traffic crashes cause significant fatalities and or trajectories of HDVs, but heavily relies on rule-based serious injuries, reflecting the global issue of millions of lives classification. For example, \[9\] predicts the trajectories of lost annually \[1\]. Since 2021, over 900 Tesla crashes involving HDVs within a fixed time window. However, the time required driver-assistance systems have been reported \[2\]. Despite for a lane-changing maneuver may exceed this fixed time win-unresolved safety issues, the number of AVs is projected to dow. The second model-based approach is to make decisions surpass 50 million by 2024 \[3\]. These statistics underscore using robust control methods, such as the min-max model the critical need for improving safety in autonomous driving. 

predictive control \[10\]. However, robust control methods make excessively cautious decisions based on a worst-case scenario The authors are with the James Watt School of Engineering, University of assumption \[11\]. These methods are not suitable for most Glasgow, Glasgow, G12 8QQ, U.K. 

⋆ Corresponding author: dezong.zhao@glasgow.ac.uk. 

real traffic environments because worst-case scenarios are

† Equal contribution

rare in real-world settings. Furthermore, decisions made for





2

Fig. 1. Autonomous driving in different scenarios. 

**a**

**Major: 6**

**\(2%\)**

**Conventional Mode:90**

****

**\(36%\)**

**Moving:108**

**Moderate: 40**

**\(43%\)**

**\(16%\)**

****

**HDV hit ADS:**

**252 \(79%\)**

**Autonomous Mode:162**

**\(64%\)**

**\(82%\)**

**Stopping:144**

**Minor: 206**

**\(57%\)**

****

**b**

**Major: 2**

**\(3%\)**

****

**Conventional Mode:48**

**Moderate:20**

**\(30%\)**

**\(72%\)**

**Moving:51**

****

**\(76%\)**

**ADS hit HDV:**

**67 \(21%\)**

**Minor:45**

**Autonomous Mode:19**

**Stopping:16**

****

**\(67%\)**

**\(28%\)**

**\(24%\)**

Fig. 2. Rear-end accident conditions between ADS and HDV: \(a\) Rear-end accidents that HDV hit an ADS from behind with a sample of 252; \(b\) Rear-end accidents that ADS hit an HDV from behind with a sample of 67 \[16\]. 

worst-case scenarios negatively impact driving quality, such that involve AVs hitting HDVs. Therefore, achieving collision-as resulting in slower driving speeds. On the other hand, free interactions with HDVs are still to be addressed. 

the game theory, the third model-based approach, has gained Compared to the aforementioned methods, simple guidance popularity recently. Game theory includes cooperative and methods, such as risk-quantified fields, are widely used be-non-cooperative games, both relying on equilibrium models. 

cause they do not need to predict HDVs’ intentions or make However, these models fail to capture the complexities of real-excessively cautious decisions \[15\]. The artificial potential world driving, which are characterized by uncertainties and field \(APF\) is a typical example, which can guide the AV

do not adhere to a regular equilibrium framework. Therefore, to the target lane without collisions by utilizing attractive and model-based methods are unable to handle interactive driv-repulsive force fields \[16\]. However, APF assumes that all ing with HDVs effectively. Additionally, the fourth model-areas around the vehicle have the same level of risk because based approach, including collision-avoidance methods \[12\]

it calculates risks toward the central point. This assumption and Voronoi diagram-based methods \[13\], is unable to safely differs from reality, where the front of a car faces more danger respond to movable objects. Real-world collisions between than other parts. Additionally, APF is difficult to generalize HDVs and vehicles equipped with advanced driving system across different scenarios without prior knowledge of the entire \(ADS\) assistance are summarized in \[14\]. As illustrated in Fig. 

environment \[17\]. 

2, 79 % of accidents involve HDVs hitting AVs, and 21 % of To promote collision-free interactions, a large number of





3

planning against surrounding obstacles. 

The DRL-based autonomous driving system is illustrated in Fig. 3. The agent interacts with the environment through actuators, observations, and rewards. The agent comprises a decision network that receives information from observations of the environment and uses rewards to assess its actions. 

These observations are provided by the observer, which interprets the state of the AV and its environment. Based on the observations, the agent generates control commands and then sends the commands to actuators. Following the actuation of these control commands, the renewed environment information and AV state are updated. Simultaneously, a reward function evaluates the agent’s actions based on predefined metrics such as safety, efficiency, or compliance to driving norms. This reward function assigns positive or negative rewards depending on how well the AV’s actions align with the desired outcomes. 

These rewards are then fed back to the agent, guiding the learning towards the optimal driving behavior. 

DRL has been proven effective in handling emergency situations, which are critical for real-world driving scenarios. 

Fig. 3. DRL-based autonomous driving system For example, \[28\] proposes a DRL-powered driving system designed to avoid collisions in emergencies. This system learns to react swiftly and safely to sudden changes, improving interactions are needed to exclude risky actions, taking into the robustness of decision-making in real-world conditions. 

account the uncertainties in decision-making and the varying Recently, several studies have been demonstrated in various driving conditions of HDVs. Learning-based methods facilitate scenarios \[29\]–\[38\]. However, different scenarios present dis-the exploration of control strategies by allowing full interaction tinct driving requirements, necessitating tailored algorithms. 

with the mixed-traffic environment. These methods enable AVs On highways, the decision-making of AVs primarily focuses to learn and adapt to complex driving scenarios through iter-on avoiding collisions with HDVs while maintaining a high ative interactions and feedback. Machine learning \(ML\) \[18\], 

average speed. In contrast, ramps introduce additional chal-

\[19\] focuses on developing algorithms to make decisions based lenges, such as blocked areas that are not present on highways, on data, including supervised, unsupervised, and reinforcement as illustrated in Fig. 4. Furthermore, it is essential to assess learning. Supervised learning trains models on labeled data, DRL-based algorithms based on demands from various social supporting tasks like classification \[20\], \[21\]. However, super-perspectives, including vehicle users, vehicle manufacturers, vised learning is less suited for implementation in real driving and public traffic systems. Research on DRL-based algorithms, environments, as labeling complex driving scenarios exhaus-categorized by driving scenarios and evaluated based on their tively is challenging and impractical. Unsupervised learning adaptability to real-world demands, is crucial for identifying methods are particularly suitable for interactive driving as they valuable research directions. 

do not require labeled data, allowing agents to learn decision-This survey aims to review DRL-based algorithms for making strategies independently. Unsupervised machine learn-autonomous interactive driving, classified by scenarios and ing has demonstrated robust performance across a range of evaluated for adaptation to real-world conditions. Four typical driving scenarios \[22\]. However, unsupervised learning often scenarios are included: highways, on-ramping merging, round-struggles with generalization in highly dynamic environments. 

abouts, and unsignalized intersections. Five key evaluation Reinforcement learning \(RL\) is a powerful technique for mak-factors are used, including driving safety \[39\], \[40\], driving ing optimal decisions in dynamic environments \[23\], \[24\]. RL

efficiency \[41\], \[42\], training efficiency \[35\], \[43\], unselfish-involves an agent that interacts with its environment and learns ness \[44\]–\[46\], and interpretability \[47\], \[48\] \(DDTUI\). DRL-safe control strategies through a reward-based framework. The based decision-making approaches are reviewed for the four adaptability of RL makes it ideal for interactive driving, where typical scenarios and evaluated using the criteria of DDTUI. 

the environment is constantly changing, and the AV must The evaluation is consistent across all papers by examining adjust its behavior accordingly. 

the inclusion of evaluation factors in the designed algorithms Deep reinforcement learning \(DRL\) is an advanced form of and their corresponding verifications. For example, if a paper RL that combines the principles of deep learning \[25\], \[26\]

discusses safety but doesn’t include verifications like a lower with RL. By utilizing deep neural networks to approximate number of collisions or consistently maintaining safe distances complex value functions, DRL enables agents to learn directly ds, it would not be considered to include the safety factor. 

from perceptual inputs, such as sensory data. This capability The reminder of this survey is structured as follows: Section allows DRL to handle more complex and real-time decision-II describes the features and driving tasks of the four typical making tasks compared to traditional RL. For example, \[27\]

scenarios. Section III explains the rationale for selecting the demonstrates the application of DRL in collision-free path five evaluation factors. Sections IV-VII evaluated DRL-based





4

4

4

4

\(c\)

\(d\)

Fig. 4. Example scenarios of autonomous driving: \(a\) highway; \(b\) on-ramp merging; \(c\) roundabout with 12 ports \(8 entrances: EM1–EM4, EB1–EB4; 4 exits: O1–O4\) and a central planted island; \(d\) unsignalized intersection. 

algorithms for highways, on-ramping merging, roundabouts, natural landscapes is reduced through careful route planning. 

and unsignalized intersections using the criteria of DDTUI, The Interstate Highway System in the United States is a respectively. Finally, Section VIII provides conclusions and vast network of highways designed to support long-distance discussions. 

travel and economic connectivity across states \[49\]. Similarly, Germany’s Autobahn, known for its sections without speed II. ROAD FEATURES AND DRIVING TASKS

limits, exemplifies the balance between high-speed travel and safety on highways \[50\]. 

This section provides the road features and driving tasks for AVs in the scenarios of highways, on-ramping merging, 2\) An Example of a Highway: Fig. 4\(a\) presents a scenario roundabouts, and unsignalized intersections. 

involving a three-lane highway. The AV drives in main lane 3 and interacts with HDVs in all three lanes. There are no disturbances or uncertainties other than the surrounding A. Highways

HDVs. Therefore, the issue of driving safety primarily relates 1\) Road Features and Driving Tasks: Highways are fun-to collisions with surrounding HDVs. In the car-following damental components of road networks, designed to enable phase, the AV can follow the HDV ahead by adjusting its vehicle movement over long distances with minimal interrup-acceleration. However, cautious following can lead to a loss of tion. The design of highways focuses on safety, efficiency, driving efficiency. To maintain high driving efficiency, the AV

and environmental impact. Safety features include wide lanes may change lanes when the space ahead is limited. However, and clear signage to reduce collision risks.High efficiency is collisions with HDVs in the target lane could occur during the achieved by optimizing lane layouts to keep vehicles driving lane-changing. Therefore, the driving task on highways can be smoothly and reduce bottlenecks. The impact of highways on summarized as balancing collision avoidance with surrounding

5

HDVs while maintaining a consistently high speed. 

C. Roundabouts

1\) Road Features and Driving Tasks: Roundabouts are designed to improve traffic flow and enhance safety by reducing B. On-ramping Merging

the likelihood of severe accidents. One example of a typical 1\) Road Features and Driving Tasks: Ramps, including roundabout is Folon’s obelisk in Pietrasanta in Italy, which on-ramps or off-ramps, are essential components of highway features a central island and circular roads around it \[53\]. 

systems. Due to the symmetry between on-ramping and off-Another example is the Place Charles de Gaulle in Paris, ramping processes, this survey considers only on-ramping France, where twelve major avenues converge around the Arc merging. Ramps enable the smooth and safe transition of de Triomphe \[54\]. 

vehicles between different roadways, typically connecting sur-2\) An Example of a Roundabout: An example of a round-face streets with highways. Ramps provide access to highways about is presented in Fig. 4\(c\). The AV starts from the EB4

without disrupting traffic flow on the main highway lanes. 

port and has three possible exit choices: O1, O2, and O3. 

Ramp design focuses on safety, efficiency, and space utiliza-When the target exit is O1, the AV can simply follow the outer tion. Safety is crucial, as ramps must accommodate vehicles lane. For the target exit O2, there are two possible routes. One accelerating or decelerating while merging onto or diverging route is staying in the outer lane, which is generally safer. The from the highway. On-ramps enhance traffic flow by reducing other route is merging into the inner lane and exiting near O2. 

disruptions to mainline traffic and providing sufficient space This second route is more efficient, as the inner lane offers a for safe merging. Additionally, urban space constraints often shorter curve length for the same round angle. However, rear require innovative ramp designs, such as cloverleaf inter-vehicles driving in the inner lane bring potential collision risks. 

changes, to connect multiple roadways effectively. 

For the target exit O3, the AV must find the right moment to 2\) Comparison with Highways: Highways and ramps serve merge into the inner lane. After traveling in the inner lane for a different functions, which are summarized below. 

period, the AV is expected to change lanes near the exit. The main challenge is to safely interact with other HDVs when

• Functionality: Highways are designed for high-speed, approaching each of these three exits. 

long-distance travel with minimal interruption, while ramps are the transition between different road types. 

D. Unsignalized Intersections

• Design: Highways are characterized by long, straight 1\) Road Features and Driving Tasks: Unsignalized inter-stretches with multiple lanes, designed to maintain high sections are critical components of road networks where two speeds and efficient traffic flow. In contrast, ramps often or roads meet or cross. They are designed to manage traffic involve curves and elevation changes, designed to accom-flow from different directions, enabling vehicles to navigate modate vehicles as they speed up or slow down. 

safely through crossing points. Unsignalized intersection can

• Speed: Highways support higher speeds, with vehicles control and organize traffic movements, reduce congestion, and typically traveling at constant high speeds over long enhance safety for all vehicles. One example is the Diverging distances. Ramps involve acceleration or deceleration, Diamond Interchange \(DDI\) \[55\]. 

requiring careful design to manage the speed differential 2\) An Example of an Unsignalized Intersection: Fig. 4\(d\) between the ramp lane and the main lane. 

shows a three-lane unsignalized intersection designed for For example, the Cloverleaf Interchange is a common de-moderate to heavy traffic flow. The intersection accommodates sign that efficiently manages space while connecting highways vehicles from all four directions, with dedicated lanes for with multiple surface streets \[51\]. Another example is the High specific traffic movements. Each approach to the intersection Occupancy Vehicle \(HOV\) lane ramps, which are designed to includes three lanes, and the areas surrounding the intersection control the flow of carpool vehicles onto highways, providing are grassland. At the center, where all four roads meet, there is direct and less congested access points \[52\]. 

an ample space for vehicles to make turns from any direction. 

Consider a three-lane ramp scenario in Fig. 4\(b\), which This central area is essential for preventing bottlenecks and includes two main lanes and one ramp lane. The AV interacts ensuring smooth traffic flow. 

with both dynamic and static objects. The dynamic objects are surrounding HDVs, each with unique driving intentions, III. RATIONALE OF THE EVALUATION FACTORS

speeds, and acceleration patterns. The static object represents In the context of adapting decision-making algorithms to an obstruction within the ramp lane, rendering the lane impass-real-world driving, five key evaluation factors have been able and blocking access. As a result, the AV must change into selected: driving safety and efficiency, training efficiency, the main lane before the ramp ends, considering the HDVs and unselfishness, and interpretability. As depicted in Fig. 5, the feasibility in lane-changing. 

driving safety and efficiency form the foundation of any Waiting for enough space to change lanes and driving slowly autonomous driving system. Training efficiency enables faster to avoid blocked roads lead to safer driving. However, this convergence of algorithms. Unselfishness enhances interaction cautious driving can significantly reduce driving efficiency with surrounding traffic, promoting cooperation with HDVs. 

and lower road capacity on the ramp. Consequently, it is Meanwhile, interpretability fosters public trust and addresses challenging to navigate the ramp, avoid collisions with both algorithmic errors, ensuring that decision-making is transpar-surrounding HDVs and the blocked road ahead, while still ent and understandable. The detailed rationale behind selecting maintaining a high driving speed. 

these factors is discussed below. 





6

Driving Safety

Aggressive

Normal

Driving 

Unselfishness: Smart Interactive 

Efficiency

Driving

Public 

Feedback

1. Faster Convergence

Reliable Autonomous Driving

1. Public Trustworthyness

Interpretability

Training 

2. Higher Training Rewards

2. Debugging Simplicity

Efficiency

3. Better Performance

Trustworthy

High-quality

Transparent

Fast-update

Road Test

Fig. 5. The importance and necessaries of achieving DDTUI in real-world autonomous driving. 

A. Driving Safety

time and a smoother ride, significantly improving overall Driving safety is a fundamental requirement for autonomous satisfaction \[67\]–\[69\]. Besides, improving driving efficiency vehicles. Frequent collisions cause substantial economic losses is crucial for reducing the energy consumption \[70\], \[71\]. 

and pose severe safety risks \[56\], \[57\]. Therefore, driving safety is primarily evaluated based on the frequency of colli-C. Training Efficiency

sions with other vehicles \[58\], \[59\]. Minimizing collisions is a Training efficiency of algorithms directly impact the time direct measure of the vehicle’s compliance to safety standards. 

and resources required to bring a fully functional AV system to Collision avoidance commonly relies on flexible reactions to reality. One primary benefit of improved training efficiency is hazardous areas. Once a hazard is detected, the system assesses the reduced training time. The acceleration allows developers the risk by analyzing the relative speed, distance, and trajectory to focus more on system fine-tuning and extensive testing. Sev-of surrounding objects \[60\]. Additionally, some autonomous eral studies have reduced training time by adding extra training driving systems evaluate possible decisions to avoid collisions mechanisms or adjusting the structures of networks \[35\], \[72\]–

while maintaining high efficiency \[61\], \[62\]. Furthermore, 

\[74\]. Another important benefit is the reduction in device other autonomous driving systems use rule-based commands to wear and tear. Fast and efficient training reduces the required adjust the AV’s behavior when unsafe conditions emerge \[63\]. 

computational resources. By improving training efficiency, the For instance, AVs will be asked to stop when they encounter workload of computing equipment is minimized, resulting in an interaction and spot-lines simultaneously \[63\]. 

less frequent maintenance and replacement. 

B. Driving Efficiency

D. Unselfishness

Driving efficiency refers to an AV’s ability to maintain a In the context of autonomous driving, unselfishness refers high average speed while adapting to varying traffic condi-to an AV’s ability to consider and accommodate the intentions tions. However, the implications of driving efficiency extend of other HDVs on the road. Unselfishness evaluates how well far beyond speed, affecting road capacity, user experience, and an AV can cooperate with surrounding vehicles by predicting energy consumption. 

their intentions and adjusting its behavior accordingly. Human On road capacity, efficient driving allows vehicles to travel drivers often prioritize factors such as safety, efficiency, and at optimal speeds, minimizing delays and reducing traffic comfort, and these intentions vary widely depending on the congestion. For example, HDVs tend to drive faster on fa-specific situations. 

miliar roads, contributing to higher road capacity and traf-Accurately classifying these driving intentions is essen-fic flow \[64\]–\[66\]. Similarly, AVs promote smoother traffic tial for effective interactions with surrounding HDVs. Exist-flow when they operate efficiently. Therefore, efficient driving ing methods for recognizing driving intentions and enabling allows more vehicles to travel smoothly without congestion. 

interaction-aware driving have been reviewed in \[75\]. These On user experience, an efficient journey means shorter travel methods categorize driving intentions across various scenarios, 

7

including car following and lane changing \[76\], \[77\]. While derived from common driving practices, ensuring a ds with many papers have focused on the self-driving characteristics of other vehicles. The dynamically-learned safety module uses the ego vehicle \[78\], \[79\], the importance of unselfish behavior driving data to learn safety patterns. By integrating both is becoming increasingly recognized. 

the handcrafted and dynamically-learned safety modules, the An unselfish AV that effectively anticipates and responds to driving safety is improved. 

the intentions of other vehicles contributes to a smoother and Moreover, deep deterministic policy gradients \(DDPG\) have more harmonious traffic flow. By avoiding overly aggressive been used to improve driving efficiency by overtaking sur-or excessively cautious driving behaviors, the AV can help rounding vehicles in \[96\]. The overtaking-oriented training is minimize disruptions and conflicts with other vehicles. This achieved by adding a high reward for overtaking maneuvers. 

cooperative approach enhances the safety and efficiency of The reward function for overtaking is formulated as \[96\]:

all vehicles in the road network and improves the driving experience for everyone involved. 

Rovertaking = Rlane keeping \+ 100 × \(n − RacePos\) \(1\)

where Rlane keeping is the reward for lane-keeping, n is the E. Algorithm Interpretability

total number of vehicles in a given episode, and RaceP os Algorithm interpretability has gained significant importance reflects the number of vehicles in front of the AV. Therefore, due to DRL models are required to make logical decisions. 

the larger the RaceP os, the smaller the Rovertaking. Although A logical structure makes the black-box of learning more safety rewards are applied, the collision rate increases with the transparent \[47\], \[48\]. In DRL-based autonomous driving sys-frequency of overtaking. 

tems, improving interpretability is crucial for system’s safety Furthermore, non-linear model predictive control \(NMPC\) and transparency. To address the challenges in interpretability, has been integrated with DDQN to maintain safe highway driv-various approaches have been adopted, including policy visual-ing in \[97\]. NMPC inherently incorporates vehicle dynamics ization to showcase DRL behaviors \[80\], \[81\], and surrogate as constraints into its optimization, ensuring that the control models for approximate human-understandable explanations inputs from the DRL agent remain within safe and feasible

\[82\]–\[85\]. Furthermore, specific rule-based methods, algorith-bounds \[97\]:

mic structure-adapted methods, and human-grounded methods Z

T

have been proposed to assess interpretability. 

min

e\(t\)⊤Qe\(t\) \+ rδ2\(t\) \+ ru2\(t\)dt

Specific rules have been developed to assess interpretability x\(t\),u\(t\)

0

\[86\]. One such rule, known as F AST , evaluates interpretabil-s.t. 

˙

x\(t\) = f \(x\(t\), u\(t\)\), 

ity via four criteria: F for fairness, A for accountability, S for ey

≤ e

, 

\(2\)

min

y \(t\) ≤ eymax

sustainability, and T for transparency \[87\]. Fairness requires eψ

≤ eψ\(t\) ≤ eψ , 

models to be formalized using basic explanation labels and min

max

δ

functionality evaluation. Accountability refers to answerability min ≤ δ\(t\) ≤ δmax, 

and auditability, ensuring that the system has been clearly de-umin ≤ u1\(t\) ≤ umax

fined. Sustainability ensures safe operation without inequality where T is the prediction horizon, e\(t\) is the error vector to be or discrimination, while transparency ensures that the model’s regulated to zero, and Q = diag\(q

internal rule settings are accessible and understandable. 

1, q2\) is a diagonal matrix

of tracking weights. The control effort weight is denoted by Some methods focuses on assessing interpretability by ad-r. The steering angle is represented by δ\(t\), and the control justing DRL algorithmic structures. Researchers achieve this input is u\(t\). The state vector is x\(t\), and f represents the by developing standardized benchmarks that use interpretabil-system dynamics. e

ity metrics \[88\], \[89\] or by troubleshooting explanations y \(t\) and eψ \(t\) are the lateral position error and heading angle error, respectively. The variables

\[90\], \[91\] to identify instances where these explanations fall e

, e

, e

, e

, δ

short. In addition, some studies concentrate on altering neural ymin

ymax

ψmin

ψmax

min, δmax, umin, and umax are the

minimum and maximum admissible values for the lateral network architectures to enhance interpretability \[92\], \[93\]. 

position error, heading angle error, steering angle, and control Furthermore, human-grounded methods focus on how easily input, respectively. NMPC improves the interpretability of safe people can understand the model’s key computational sections control by providing a clear mathematical formulation that

\[94\]. DRL-based algorithms incorporating traffic-related mod-integrates the system’s constraints with the agent’s decision-els enable people to better understand their structures through making \[98\]–\[100\]. 

traffic knowledge or mathematical formulation, thereby im-Additionally, a policy gradient \(PG\) method has been used proving interpretability. 

with hard constraints to ensure safe highway driving in \[101\]. 

These hard constraints prevent the AV from approaching risky IV. DEEP REINFORCEMENT LEARNING-BASED

boundaries, such as track edges. For example, the AV’s longi-DECISION-MAKING ON HIGHWAYS

tudinal and lateral positions are restricted from approaching A. Single-factor Methods for Highway Driving the track boundaries. Cooperative lane-changing has been Many works consider only one of five key factors. A Double achieved in \[102\], enhancing the unselfishness. Interpretability Deep Q-Network \(DDQN\) is integrated with handcrafted has been improved by combining DRL with imitation learning safety and dynamically-learned safety modules in \[95\]. The \(IL\) in \[103\]. IL uses expert demonstrations to make the handcrafted safety module relies on heuristic safety rules learning more interpretable. Training efficiency in highway

8

driving is also enhanced by integrating a spatial attention efficiency and unselfishness are considered in highway driving. 

module and attention mechanism into the deep Q-network Driving efficiency is achieved by a reward based on v0, vmax, in \[104\]. 

and vmin. Unselfishness is achieved by penalizing unnecessary lane changes to reduce disturbances to HDVs. Driving safety B. Dual-factor Methods for Highway Driving and training efficiency have been addressed in \[114\]. Safety is maintained by ensuring a d

Additionally, two of the five considered factors are inte-s between vehicles using rule-

based constraints, while training efficiency is improved by grated in some recent studies. The Intelligent Driver Model incorporating a multi-head attention mechanism. 

\(IDM\) \[105\] has been incorporated into the DDQN for highway driving in \[106\]. The IDM prevents collisions during car-following and therefore, the integration of DDQN with C. Three-factor Methods for Highway Driving IDM enhances both the driving safety and interpretability in Furthermore, three of the five considered factors are com-highway driving. The IDM is formulated as \[106\]:

bined in a few recent papers. Driving safety, interpretability, 

" 

and driving efficiency have been improved in \[115\]. Driving v

4

g∗ 2\#

U

FV

IDM = Umax

1 −

−

\(3\)

safety and interpretability are enhanced by using a collision ve

g

penalty and the IDM. Driving efficiency is ensured by a reward where U

based on the velocity difference between v max is the maximum acceleration of the AV, ve is the max and v0. The

expected velocity, and g is the gap between the AV and the reward at time step t is formulated as \[115\]:

HDV. The desired gap g∗ between the AV and the front HDV

Rt = −Collision − 0.1 × \(vt

− vt \) − 0.4 × \(L − 1\)2 \(6\)

is formulated as \[106\]:

max

0

v

where Collision, vt

, and vt

max

0 are the occurrence of a collision, 

g∗ = d

AV∆v

s \+ vAVTe −

√

\(4\)

maximum velocity, and current velocity at time t, respectively. 

2 Umaxb

L represents the relative position the target lane, where L = 1

where Te is the expected time gap, ∆v is the velocity indicates that the vehicle has successfully reached the target difference between the AV and the front vehicle \(FV\), and lane. A collision results in a negative reward, and a larger b is the comfortable deceleration. 

difference between v0 and vmax also leads to a negative reward. 

The reward function of DDQN has been adapted to improve Additionally, if the vehicle does not drive in the target lane, a driving safety and efficiency in \[107\]. Specifically, a penalty is penalty is applied. 

applied when the vehicle goes off-road or the time-to-collision A multi reward-based DQN has been proposed to achieve \(TTC\) falls below a threshold \[108\] . The reward for driving safe, efficient, and unselfish driving in \[116\]. Three rewards efficiency is formulated as \[107\]:

are combined: speed reward, limited lane-changing reward, v0

R =

\(5\)

and overtaking reward. The speed reward is a normalized vmax

reward based on the current speed relative to the minimum where v

and maximum speed limits \[116\]:

max is the maximum velocity, and v0 is the current velocity. This reward function helps maintain a relatively high \(v0 − vmin\) ∗ rv

driving velocity, thus increasing driving efficiency. Moreover, Rv =

\(7\)

vmax − vmin

driving safety and altruism have been achieved using a level-k game-based DQN in \[109\]. The level-k game models the where Rv represents the reward for speed, encouraging higher reasoning interaction between AVs and HDVs, promoting speeds within safe limits. vmin is the minimum speed of the unselfish decision-making. A crash penalty is implemented agent vehicle, and rv is the base reward for speed. The limited in the DQN to prevent frequent collisions between AVs and lane-changing reward function is designed to minimize the HDVs. Additionally, unselfishness and training efficiency have number of lane changes, promoting safer driving and reducing been considered in \[110\]. Unselfishness is achieved through a the disturbance to surrounding vehicles: cooperative multi-goal credit function-based policy gradient \(−rl, if the agent vehicle changes lanes; \(PG\). This adapted PG accounts for the goals of all vehicles, Rl =

\(8\)

0, 

otherwise. 

optimizing overall performance during training. Training efficiency is improved by a multi-agent reinforcement learning where −rl is the penalty value for a lane change. The \(MARL\) curriculum, which reduces the number of trainable overtaking reward function encourages the agent vehicle to parameters and lowers computational costs. 

overtake more vehicles, improving driving efficiency: Unselfishness and driving efficiency on highways are \(

achieved in \[111\]. Unselfishness is promoted through MARL

ro, 

if the agent vehicle overtakes another vehicle; Ro =

by considering each vehicle’s state. Driving efficiency is en-0, 

otherwise. 

hanced by a reward function that selects actions to increase the \(9\)

average velocity of all vehicles. Driving safety and driving ef-where ro is the reward value for overtaking. 

ficiency have been achieved using multi-objective approximate Interpretability, driving safety, and driving efficiency have policy iteration \(MO-API\) in \[112\]. Driving safety is ensured been achieved in \[117\]. Safety and efficiency are enhanced by monitoring collisions, while driving efficiency has been by penalizing frequent lane changes and tracking the desired assessed by comparing the v0 with the ve. In \[113\], driving velocity vd, respectively. Interpretability is achieved through

9

a car-following process using a proportional-derivative \(PD\) Training efficiency is achieved through the potential-based controller with transparent mathematical formulation \[117\]:

reward shaping function. The total reward function and reward shaping function are given by \[121\]:

ddes,i = αjvj\+1

\(10\)

i

l

R′ = R\(s, a, s′\) \+ βF \(s, a, s′\)

\(16\)

acf,i = Kp\(xj\+1 − xj\) \+ K

− vj\)

\(11\)

l

i

d\(vj\+1

l

i

F \(s, a, s′\) = γϕ\(s′\) − ϕ\(s\)

\(17\)

where ddes,i is the desired following distance for the i-th vehicle, αj is a sensitivity parameter with random values from F \(s, a, s′, t, t′\) = γϕ\(s′, t′\) − ϕ\(s, t\) \(18\)

i

N \(1.3, 0.02\), vj\+1 is the speed of the leading vehicle in the l

where R′ is the new reward criterion, R\(s, a, s′\) is the original \(j \+ 1\)-th lane, acf,i is the acceleration command, Kp and Kd reward function, β is a weighting factor, F \(s, a, s′\) is the are the proportional and derivative gains, and xj\+1 and xj are l

i

potential-based reward shaping function, s and s′ are the the positions of the leading and i-th vehicles, respectively. 

current and next state, respectively, a is the action taken, In \[118\], driving safety, efficiency, and interpretability have and γ is the discount factor. ϕ\(s\) is the potential function also been combined. Safety and efficiency are achieved by mapping the state to a real number, and t and t′ are the penalizing collisions and rewarding high average velocity. 

time corresponding to s and s′, respectively. \(16\) combines Interpretability is enhanced by using the risk potential field the original reward function with an additional shaping term. 

\(RPF\), which models and visualizes risks around surrounding \(17\) defines the shaping function as the difference between the vehicles. In \[119\], driving safety and interpretability have been discounted potential of the next state and the current state. \(18\) achieved in adaptive cruise control \(ACC\), which maintains extends \(17\) by including time as a parameter and therefore ds between vehicles and provides interpretable mathematical allows for dynamic potential functions. 

formulations. Driving efficiency is achieved by rewarding each Driving safety, driving efficiency, unselfishness, and training high-speed state. Finally, driving safety, driving efficiency, efficiency on highways have been addressed in \[122\]. Driving and training efficiency have been achieved in \[120\]. Safety is safety and efficiency are considered in the reward function ensured through a collision penalty, and efficiency is rewarded of the DQN. Unselfishness is achieved through a joint policy based on the velocity difference between v0 and vmin. Training update, accounting for the profits of multiple vehicles. Training efficiency is improved by using a long short-term memory efficiency is enhanced by reusing the experiences of single \(LSTM\) network-assisted DDQN. 

agents within a MARL framework. In \[123\], driving safety, efficiency, unselfishness, and training efficiency on highways D. Four-factor Methods for Highway Driving have been explored. Safety and efficiency are ensured by Moreover, four of the five considered factors have been assessing the remaining reaction time during emergencies and included in some studies. Driving safety, driving efficiency, selecting the proper lane-changing point, respectively. Un-training efficiency, and interpretability have been considered selfishness is achieved using MARL for cooperative highway in \[121\]. Driving safety and driving efficiency are achieved by driving, while training efficiency is improved with a dynamic a reward function that maintains a d

coordinate graph \(DCG\) that enhances cooperative efficiency. 

s from the leading vehicle

while tracking the v

In \[124\], safety, efficiency, unselfishness, and training effi-d. 

Interpretability is ensured through

safety-based driving rules \[121\]:

ciency have been considered. Safety is ensured by applying penalties both for collisions and for deviating from the road. 



2\(v − v



f

\)

t

target

Efficiency is achieved by rewarding each state that overtakes f

= inf

t : t > 

\(12\)

min

admax

other vehicles. Unselfishness is promoted through MARL to 2\(v



coordinate driving. Training efficiency is enhanced by employ-b

− v\)

t

target

b

= inf

t : t > 

\(13\)

min

ing a parameter-sharing mechanism, which stores experience admax

of each agent to reinforce common scenario understanding. 

\(v − v



f \)tf

\(vb − v\)tb

In \[125\], safety, efficiency, unselfishness, and interpretabil-dtarget

= min

, 

\(14\)

min

2

2

ity have been considered. Safety, efficiency, and unselfishness are improved through rewards for collisions, velocity

∆dtarget = min |xAV − xf

|, |x

| 

\(15\)

target

AV − xbtarget

ratio between v0, vmax, and vmin, and limiting unnecessary where tf

and t

are the minimum safe time intervals

lane changes, respectively. Interpretability is enhanced by min

bmin

between the AV and the vehicles in front and behind in the integrating an autonomous emergency braking system, pro-target lane, respectively. v is the speed of the AV; vf and

moting safer decision-making. In \[126\], safety, efficiency, target

vb

are the speeds of the front and behind vehicles in the interpretability, and training efficiency have been addressed. 

target

target lane, respectively. ad

is the maximum deceleration. 

Safety and efficiency are enhanced by adding a safety layer max

dtarget

is the minimum distance between the AV and the FV

and incorporating the ratio between longitudinal speed, vmax, min

in the target lane, and ∆dtarget is the actual distance between and vmin. Interpretability is improved by using a support vector the AV and the nearest vehicle in the target lane. xAV, xf

, 

machine \(SVM\), which provides interpretable safe decision target

and xb

represent the horizontal coordinates of the AV, the boundaries. Training efficiency is boosted through an external target

front target vehicle, and the vehicle behind in the target lane, space attention mechanism that pays attention to the crucial respectively. By implementing these safety rules, the decision-areas of surrounding environment. 

making of the AV becomes more transparent and interpretable. 

In \[127\], safety, efficiency, unselfishness, a

10

nd training efficiency have been tackled. Safety, efficiency, Interpretability is achieved by using DDPG to tune a traditional and unselfishness are achieved through rewards for colli-controller’s parameters, keeping the traditional controller as sions, velocity ratios, and MARL, while training efficiency the main system to ensure transparency. Driving efficiency is is improved using a distributional DQN with multi-type input enhanced by reducing the error state, which reflects the gap data. Finally, in \[128\], safety, efficiency, unselfishness, and between actual and critical traffic density. A smaller error state interpretability have been considered. Safety, efficiency, and leads to higher traffic flow and average speed. 

unselfishness are enhanced through rewards for collisions, target velocity differences, and unnecessary lane changes, C. Three-factor Methods for On-ramping Merging respectively. Interpretability is achieved through rule-based Driving efficiency, interpretability, and training efficiency constraints, such as preventing lane changes with short lateral have been addressed in \[137\]. Driving efficiency is achieved distances to lead vehicles. 

through a reward using the difference between the start and end time of each trip. Training efficiency is improved by a teacher-E. Five-factor Methods for Highway Driving student model to train the decision-making system, where the Additionally, all the five factors are addressed in some stud-traditional control method acts as the teacher guiding the DQN

ies, such as \[129\]. Driving safety and efficiency, and unselfish-student. Similarly, driving efficiency, interpretability, and un-ness are achieved by reducing collisions, increasing speed, and selfishness have been improved in \[138\]. Driving efficiency is minimizing lane-change frequency through rewards. Training achieved by a reward that compares the average speed between efficiency is improved through a convolutional neural network-two consecutive time. Unselfishness and interpretability are based LSTM. Interpretability is enhanced by using spatio-achieved by combining ramp metering \(RM\) with Q-learning. 

temporal image representations for HDVs, which increase the RM optimizes average vehicle speed and is algorithmically interpretability of the inputs. The DRL-based decision making transparent. Driving safety, efficiency, and unselfishness have in highway driving based on DDTUI is summarized in Table been addressed in \[136\]. Driving safety is achieved through a I. 

penalty for small relative distances, driving efficiency is enhanced by minimizing the relative distance while maintaining at least the safe distance, and unselfishness is achieved using V. DEEP REINFORCEMENT LEARNING-BASED

MARL to optimize general driving performance. 

DECISION-MAKING IN ON-RAMPING MERGING

A. Single-factor Methods for On-ramping Merging D. Four-factor Methods for On-ramping Merging Driving efficiency has been considered using Q-learning Driving efficiency, training efficiency, unselfishness, and in \[130\]. The remaining time of AV on the ramp lane is interpretability have been improved in \[139\], where driving reduced by optimizing the reward function, thus promoting and training efficiency is enhanced by DDPG-assisted RM

fast lane-changing to the main lane. The reward function is and variable speed limit \(VSL\) control. Interpretability and formulated as \[130\]:

unselfishness are improved through RM and VSL, which are r

algorithmically transparent. Driving safety, efficiency, training t = µ¯

vt \+ ω ¯

qt, 

µ > 0, 

ω < 0

\(19\)

efficiency, and interpretability have been achieved in \[140\], 

where rt represents the reward after taking action at; ¯

vt

where safety and interpretability are enhanced by combining denotes the average speed in the merging area during time APF, which quantifies and visualizes risk areas and pro-step t; ¯

qt indicates the average queue length at the on-ramp vides interpretable input. Driving and training efficiency are during time steps t and t \+ 1; µ is a positive weight assigned achieved by combining MPC with DDQN, which outperforms to the speed reward, and ω is a negative weight for the single MPC or DDQN methods. Similarly, driving safety, queue length reward. These rewards help balance the trade-efficiency, training efficiency, and unselfishness have been ad-off between enhancing vehicle mobility on the mainline and dressed in \[141\], where safety and efficiency are promoted by reducing delays at the on-ramp. Driving efficiency has also penalties for collisions and stop maneuvers. Training efficiency been improved in \[131\] by reducing the total travel time reward is improved by integrating the driver’s intention model \(DIM\) \(RTTT\), represented by the summation of the total number of with DDPG, while unselfishness is achieved by considering vehicles at each time step. Driving safety has been achieved HDVs’ various cooperation intentions. In \[142\], driving safety, through a safety factor in \[132\]. The safety factor is a negative efficiency, training efficiency, and interpretability have been reward when the relative distances between AV and HDV are achieved by applying the safety, efficiency rewards, and IDM

small. Driving safety has been achieved in \[133\], by giving respectively, with independant PPO \(IPPO\) used for improved rewards for each state having a ds and penalties for collisions. 

training efficiency compared to baseline algorithms. 

B. Dual-factor Methods for On-ramping Merging E. Five-factor Methods for On-ramping Merging Driving efficiency and unselfishness have been considered In \[143\], driving safety and efficiency have been achieved in \[134\]. Driving efficiency is achieved by using the average through collision and stable speed assessment rewards, re-velocity of AVs as part of the reward, and unselfishness is spectively. Training efficiency is improved by using a safety achieved using MARL to maximize general profits. Inter-supervisor, filtering detectable collision cases. Interpretabil-pretability and driving efficiency have been addressed in \[135\]. 

ity is enhanced through rule-based safety constraints, and

11

TABLE I

EVALUATION OF THE DRL-BASED DECISION MAKING IN HIGHWAY DRIVING

Reference

Safety

Efficiency

Training Efficiency

Unselfishness

Interpretability

\[95\]

Safety modules

-

-

-

-

\[96\]

-

Overtaking reward

-

-

-

\[97\]

NMPC constraints

-

-

-

-

\[101\]

Hard constraints

-

-

-

-

\[102\]

-

-

-

Local interactions

-

\[103\]

-

-

-

-

Imitation learning

\[104\]

-

-

Attention module

-

-

\[106\]

IDM integration

-

-

-

IDM integration

\[107\]

TTC threshold

Velocity reward

-

-

-

\[109\]

Crash penalty

-

-

Level-k game

-

\[110\]

-

-

MARL curriculum

Cooperative function

-

\[111\]

-

Average velocity

-

MARL

-

\[112\]

Collision monitoring

Velocity comparison

-

-

-

\[113\]

-

Velocity reward

-

Lane change penalty

-

\[114\]

Rule-based

-

Attention mechanism

-

-

\[115\]

IDM & collision

Velocity difference

-

-

IDM integration

\[116\]

Speed-limit reward

Overtaking reward

-

Lane-change limit

-

\[117\]

Lane change penalty

Velocity tracking

-

-

PD controller

\[118\]

Reward function

Reward function

-

-

Risk potential field

\[119\]

Adaptive cruise

High-speed reward

-

-

ACC formulations

\[120\]

Collision penalty

Velocity difference

LSTM-DDQN

-

-

\[121\]

Safety rules

Reward function

Reward shaping

-

Safety rules

\[122\]

Reward function

Reward function

MARL reuse

Joint policy

-

\[123\]

Reaction time

Lane-changing point

DCG efficiency

MARL

-

\[124\]

Collision penalties

Overtaking reward

Parameter sharing

MARL

-

\[125\]

Collision rewards

Velocity ratio

-

Lane change limit

Emergency braking

\[126\]

Safety layer

Velocity ratio

Attention mechanism

-

SVM boundaries

\[127\]

Collision rewards

Velocity ratio

Distributional DQN

MARL

-

\[128\]

Collision rewards

Velocity difference

-

Lane change penalty

Rule-based

\[129\]

Collision reduction

Speed increase

CNN-LSTM

Lane change limit

Representations

’-’ indicates that the corresponding factor was not explicitly addressed in the study. 

unselfishness is achieved using MARL to maximize general ing capabilities. The DRL-based decision making on on-ramp profits. Similarly, all factors have been addressed in \[144\], 

merging based on DDTUI is summarized in Table II. 

where driving safety and efficiency are achieved via collision rewards and a velocity ratio, respectively. Training efficiency VI. DEEP REINFORCEMENT LEARNING-BASED

is enhanced by adversarial constraints, while unselfishness DECISION-MAKING AT ROUNDABOUTS

and interpretability is enhanced through a transparent Nash-based game that considers HDV’s profits. Finally, in \[145\], 

A. Single-factor Methods for Roundabout Driving driving safety and interpretability have been achieved using Driving efficiency in roundabout driving has been im-the deceleration rate to avoid a crash \(DRAC\), which has a proved using soft actor-critic \(SAC\) with higher peak rewards detailed mathematical formulation and is transparent. Driving in \[146\]. Training efficiency has been achieved through action efficiency is improved by using \(5\) as an efficiency reward. 

repeat and asynchronous advantage in \[147\]. Action repeat Unselfishness is addressed by considering the cooperation improves efficiency by allowing the agent to repeat the same intentions of other vehicles, and training efficiency is improved action for several time steps, decreasing the frequency of using multi-state representations to enhance the agent’s learn-making new decisions. Asynchronous advantage enables each

12

TABLE II

EVALUATION OF THE DRL-BASED DECISION MAKING IN ON-RAMPING MERGING

Ref. 

Safety

Efficiency

Training

Unselfishness

Interpretability

Efficiency

\[130\]

-

Reward

-

-

-

function

\[131\]

-

Travel time re-

-

-

-

ward

\[132\]

Safety factor

-

-

-

-

\[133\]

Collision-free

-

-

-

-

driving

\[134\]

-

Average veloc-

-

MARL

-

ity reward

\[135\]

-

Error state re-

-

-

Traditional

duction

controller

\[136\]

Distance penalty

Distance minimization

-

MARL

-

\[137\]

-

Trip time dif-

Teacher-

-

Traditional

ference

student model

control

\[138\]

-

Speed compari-

-

Ramp metering

Ramp metering

son

\[139\]

-

DDPG-assisted

DDPG

RM and VSL

RM and VSL

RM

\[140\]

APF

MPC

with

MPC

with

-

APF

DDQN

DDQN

\[141\]

Stop maneuver

HDV

Collision penalty

DIM with DDPG

-

penalty

intentions

\[142\]

Safety reward

Efficiency

IPPO

-

IDM

reward

\[143\]

Stable speed

Safety

Rule-based

Crash evaluation

MARL

assessment

supervisor

constraints

\[144\]

Collision

Velocity ratio

Adversarial

Nash-based

transparent

rewards

constraints

game

game process

\[145\]

DRAC

Velocity

ratio

Multi-state rep. 

Vehicle coop. 

DRAC

reward

agent to share its interaction experience with others. Training embedded DRL for adaptive decision-making, and inter-efficiency has been further improved by embedding the opera-pretability is enhanced by transparent model-based optimiza-tional design domain \(ODD\) into DQN in \[148\]. ODD guides tion. Driving safety and unselfishness have been achieved the training to more targeted scenarios, reducing unnecessary in \[153\], with safety ensured by penalizing collisions and exploration and accelerating convergence. 

ramping off the road, and unselfishness promoted by using MARL to maximize collective benefits. Driving safety and B. Dual-factor Methods for Roundabout Driving interpretability have been achieved in \[154\], with safety main-Driving efficiency and training efficiency are improved tained through penalties for collisions with HDVs and walls. 

using the Conditional Representation Model \(CRM\) in \[149\], 

Interpretability is supported by gradual training mode, similar which helps the agent better understand safety by defining to human learning, where the system starts with sparse traffic each state as safe or unsafe state. Training efficiency and and progresses to dense traffic later. 

interpretability have been improved by leveraging labeled data from domain experts as guidance in \[150\]. Driving safety and C. Three-factor Methods for Roundabout Driving driving efficiency have been enhanced in \[151\] by incorporating vd and allowable relative distance into the reward function. 

Driving safety, driving efficiency, and training efficiency Training efficiency and interpretability have been improved have been improved in \[155\]. Driving safety and driving in \[152\]. Training efficiency is achieved through optimization-efficiency are promoted through safety and efficiency rewards, 

13

respectively. Training efficiency is enhanced via trust region B. Dual-factor Methods for Unsignalized Intersection Driving policy optimization \(TPRO\), which converges faster than PPO

Both driving and training efficiency have been improved and DDPG. In \[156\], driving safety and driving efficiency in \[162\], where the driving efficiency is enhanced by using have been achieved by rewards for non-collision lane-changing total waiting time \(TWT\) as part of the reward. Training and the difference between initial and target velocities, respec-efficiency is increased by employing a background removal tively. Training efficiency is improved by embedding LSTM

ResNet as the Q-network, resulting in lower TWT than base-into the actor-critic network. Training efficiency, driving safety line algorithms. In \[163\], driving efficiency and interpretability and efficiency have been enhanced in \[157\]. Training effi-have been enhanced. The driving efficiency is improved by ciency is improved by normalizing the initial reward for faster using the difference between the v

convergence. Driving efficiency and driving safety benefit from d and v0 as part of the

reward, while the interpretability is achieved through the use multiple environments where agents are trained simultane-of IDM for safe and transparent vehicle following. Similarly, ously, achieving higher success rates and fewer crashes. 

in \[164\], both driving efficiency and interpretability have been improved. The former is enhanced by incorporating a velocity-D. Four-factor Methods for Roundabout Driving based reward, and the latter is enhanced by applying a safety-based rule policy. In \[165\], driving efficiency is increased by Driving safety, driving efficiency, training efficiency, and using the safe distance as a reward and the risky distance as unselfishness have been addressed in \[158\], where safety a penalty, resulting in higher success rates. Interpretability is is maintained using ds, and driving efficiency is enhanced achieved using a model-based transparent method combined by the ratio of initial to target velocity. Training efficiency with twin delayed deep deterministic policy gradient \(TD3\). 

is improved through a synthetic representation mechanism In \[166\], driving efficiency is enhanced by the ratio of v that enhances agents’ understanding, and unselfishness is 0 to

v

promoted using MARL to maximize joint benefits. Driving max as part of the reward, and interpretability is improved by gridding the coordination zone into different granularities, safety, driving efficiency, interpretability, and training effi-converting risky areas into a matrix format. 

ciency have been addressed in \[58\], where safety is ensured via crash penalties and efficiency via high-speed rewards. 

Both driving efficiency and training efficiency have been Interpretability is maintained using the IDM for safe, trans-improved in \[167\]. Driving efficiency is achieved by rewarding parent algorithmic-following. Training efficiency is improved goal attainment, and training efficiency is increased by using through an interval prediction model to precompute feasible DQN with common and specific sub-tasks. The common sub-paths, reducing training computation. Driving safety, driving task enables knowledge sharing across tasks, while the specific efficiency, training efficiency, and interpretability have been sub-task helps the system better understand a task’s main enhanced in \[159\]. Safety and efficiency are promoted through goal. Training efficiency and unselfishness have been im-penalties for collisions and vehicle-stop maneuvers, respec-proved in \[168\] through an incentive communication-assisted tively. Training efficiency is increased by integrating DDPG, MARL. Agents create custom messages to influence other DQN, and NMPC. Interpretability is enhanced via the NMPC. 

agents’ policies, improving coordination and achieving globally optimal decisions. The unselfishness is realized by using MARL to maximize overall profits. In \[169\], driving efficiency and training efficiency have been improved by the adaptive E. Five-factor Methods for Roundabout Driving dual-objective transit signal priority \(D2-TSP\) algorithm with All five factors have been considered in \[99\], where driving DDQN. D2-TSP optimizes bus speed, saving time for both safety and interpretability are ensured by a rule-based action passengers and those waiting at downstream stops. Similarly, inspector. Driving efficiency is enhanced via high-speed re-in \[170\], cooperative intersection management-enhanced DQN

wards. Training efficiency is achieved through a Kolmogorov-boosts both driving and training efficiency by leveraging Arnold network-enhanced DQN. Unselfishness is promoted connectivity between vehicles. 

through rule-based route planning that considers the varying distributions of HDVs on the roundabout. The DRL-based decision making in roundabouts based on DDTUI is summarized C. Three-factor Methods for Unsignalized Intersection Drivin Table III. 

ing

In \[171\], driving efficiency, unselfishness, and training effi-VII. DEEP REINFORCEMENT LEARNING-BASED

ciency have been addressed. Driving efficiency is enhanced DECISION-MAKING AT UNSIGNALIZED INTERSECTIONS

by penalizing each low-speed state, while unselfishness is achieved through MARL for maximizing overall profits. TrainA. Single-factor Methods for Intersection Driving ing efficiency is improved with multi-agent DQN, which offers Traffic efficiency has been improved by using the difference faster convergence than baseline algorithms. In \[172\], driving between v0 and vd as a reward in \[160\]. Additionally, a penalty efficiency, training efficiency, and interpretability have been is applied when the velocity drops below a threshold, further integrated. Driving efficiency is increased by rewarding each boosting traffic efficiency. In \[161\], driving efficiency has been high-velocity state, and training efficiency is achieved by com-achieved by applying a constant penalty as long as the AV has bining deep Q-learning with transfer learning. Interpretability not reached the target exits. 

is improved by using the IDM for safe vehicle following. 

14

TABLE III

EVALUATION OF THE DRL-BASED DECISION MAKING AT ROUNDABOUTS

Ref. 

Safety

Efficiency

Training

Unselfishness

Interpretability

Efficiency

\[146\]

-

SAC

with

-

-

-

higher

peak

rewards

\[147\]

-

-

Action

repeat, 

-

-

asynchronous

advantage

\[148\]

-

-

ODD-

-

-

embedded

DQN

\[149\]

-

CRM

CRM

-

-

\[150\]

-

-

Expert

-

Expert

guidance

guidance

\[151\]

Allowable rela-

vd

-

-

-

tive distance

\[152\]

-

-

Optimization-

-

Model-based

embedded

optimization

DRL

\[153\]

Collision

-

-

MARL

-

penalties

\[154\]

Collision

-

-

-

Gradual

train-

penalties

ing

\[155\]

Safety rewards

Efficiency

TPRO

-

-

rewards

\[156\]

Non-collision

Velocity differ-

LSTM-

-

-

rewards

ence rewards

embedded

actor-critic

\[157\]

Fewer crashes

Higher success

Reward

-

-

rates

normalization

\[158\]

Safety distance

Velocity ratio

Synthetic

rep-

MARL

-

resentation

\[58\]

Crash penalties

High-speed re-

Interval predic-

-

IDM

wards

tion

\[159\]

Collision

Vehicle-stop

DDPG, 

DQN, 

-

NMPC

penalties

penalties

NMPC integra-

tion

\[99\]

Rule-based in-

High-speed re-

KAN-DQN

Rule-based

Rule-based in-

spector

wards

planning

spector

In \[173\], driving safety, driving efficiency, and training D. Four-factor Methods for Unsignalized Intersection Driving efficiency have been incorporated. Driving safety is promoted through collision penalties, and driving efficiency is enhanced In \[175\], driving safety, driving efficiency, training effi-by rewarding velocities higher than a baseline. Training efficiency, and unselfishness have been incorporated. Driving ciency is improved by using a spatial and temporal attention safety is enhanced through autonomous intersection manage-module with SAC. In \[174\], all three aspects have also been ment \(AIM\), and driving efficiency is improved by applying addressed. Driving safety and efficiency are improved by a constant penalty until the AV reaches the exits. Training rewarding goal attainment and penalizing collisions. Training efficiency is improved by embedding AIM and LSTM into efficiency is enhanced using a randomized prior function the learning, and unselfishness is achieved through MARL. 

\(RPF\) for each ensemble member, leading to a better Bayesian In \[176\], driving safety, driving efficiency, training efficiency, posterior \[178\]. 

and interpretability have been integrated. Driving safety is promoted through collision penalties, and driving efficiency is enhanced by rewarding goal attainment. Training efficiency is improved through the Mix-Attention Network, synthetic

15

TABLE IV

EVALUATION OF THE DRL-BASED DECISION MAKING AT UNSIGNALIZED INTERSECTIONS

Ref. 

Safety

Efficiency

Training

Unselfishness

Interpretability

Efficiency

\[160\]

-

Velocity differ-

-

-

-

ence reward

\[161\]

-

Time penalty

-

-

-

\[162\]

-

Total

waiting

Background re-

-

-

time

moval ResNet

\[163\]

-

Velocity differ-

-

-

IDM

ence reward

\[164\]

-

Velocity-based

-

-

Safety-based

reward

rule policy

\[165\]

-

Safe

distance

-

-

MPC with TD3

reward

\[166\]

-

Velocity

ratio

-

-

Gridded

coor-

reward

dination zone

\[167\]

-

Goal

DQN with sub-

-

-

attainment

tasks

reward

\[168\]

-

-

Incentive com-

MARL

-

munication

\[169\]

-

D2-TSP

DDQN

-

-

\[170\]

-

CIM-enhanced

CIM-enhanced

-

-

DQN

DQN

\[171\]

-

Low-speed

Multi-agent

MARL

-

penalty

DQN

\[172\]

-

High-velocity

DQL

with

-

IDM

reward

transfer

learning

\[173\]

Collision

High-velocity

SAC with at-

-

-

penalties

reward

tention

\[174\]

Collision

Goal

RPF

-

-

penalties

attainment

reward

\[175\]

AIM

Constant

time

AIM

and

MARL

-

penalty

LSTM

\[176\]

Collision

Goal

Mix-Attention

-

IDM

penalties

attainment

Network

reward

\[177\]

Collision

Low-velocity

VD-MADQL

MARL

IDM

penalties

penalty

representation mechanism, and replay memory mechanism. 

VIII. CONCLUSION AND DISCUSSION

The interpretability is ensured by using the IDM. 

This survey presents a comprehensive overview of the current state of the art in DRL-based decision-making for E. Five-factor Methods for Intersection Driving autonomous vehicles. By discussing recent research efforts In \[177\], driving safety has been promoted through collision in this field, this survey highlights the diverse algorithms penalties, while driving efficiency is enhanced by penalizing developed to address decision-making tasks across various sce-each state with velocity lower than the vmin. Training efficiency narios, including highways, on-ramping merging, roundabouts, is improved using value decomposition-based multi-agent deep and unsignalized intersections. Our analysis goes beyond Q-learning. Unselfishness is achieved by employing MARL to simply presenting these algorithms by uncovering valuable minimize joint profits, and interpretability is ensured through insights, identifying key gaps in the current research, and high-the IDM. The DRL-based decision making on unsignalized lighting emerging trends in DRL-based decision making for intersections based on DDTUI is summarized in Table IV. 

autonomous driving. While driving efficiency and safety are

16

TABLE V

OCCURRENCE AND RATIO OF EVALUATION FACTORS ACROSS DIFFERENT SCENARIOS

Scenario

Safety

Efficiency

Training Efficiency Unselfishness

Interpretability

Highway

23 \(76.7%\)

20 \(66.7%\)

11 \(36.7%\)

13 \(43.3%\)

11 \(36.7%\)

Ramp

9 \(56.25%\)

14 \(87.5%\)

8 \(50%\)

8 \(50%\)

9 \(56.25%\)

Roundabout

10 \(62.5%\)

11 \(68.75%\)

12 \(75%\)

3 \(18.75%\)

6 \(37.5%\)

Intersection

5 \(27.7%\)

17 \(94.4%\)

12 \(66.7%\)

4 \(22.2%\)

6 \(33.3%\)

Total

47 \(58%\)

63 \(77.8%\)

44 \(54.3%\)

29 \(35.8%\)

32 \(39.5%\)

The numbers in parentheses indicate the percentage of the total studies for each factor. 

addressed across most studies, there is a growing trend towards pretability, such as using the APF and IDM concurrently. 

addressing multiple DDTUI factors concurrently. Emerging 3\) Enhancing the unselfishness of AVs in complex, multi-approaches, such as MARL and the integration of traditional agent environments: While approximately 50% of stud-control methods with DRL, show promise in tackling complex ies use MARL to promote unselfishness, the complexity challenges with increased unselfishness and interpretability in of real-world traffic scenarios presents uncertainties of autonomous driving. 

driving behaviors. Future research should explore more Based on existing studies, Table V summarizes the distribu-sophisticated MARL techniques based on real-world tion of evaluation factors considered in four typical scenarios. 

experience. For example, combining game theory with Most studies, i.e., 18 studies that account for 94.4% of ex-driving style classification based on real-world datasets isting studies, prioritize efficiency at intersections to optimize can better model the behaviors of HDVs. 

travel time in complex and interaction-heavy environments. 

Efficiency is also emphasized at ramps in 14 studies \(i.e., REFERENCES

87.5%\) to reduce congestion and streamline traffic flow. Safety is particularly emphasized on highways in 23 studies \(i.e., 

\[1\] Department

for

Transport, 

“Road

accidents

and

safety

76.7%\), which addresses the importance of accident prevention statistics,” 

https://www.gov.uk/government/collections/

road-accidents-and-safety-statistics, 2023, accessed: 2024-04-28. 

in high-speed settings. In contrast, intersections address safety

\[2\] D. Omeiza, H. Webb, M. Jirotka, and L. Kunze, “Explanations in less often. Training efficiency is significant at roundabouts autonomous driving: A survey,” IEEE Transactions on Intelligent in 12 studies \(i.e., 75%\) and unsignalized intersections in 12

Transportation Systems, vol. 23, no. 8, pp. 10 142–10 162, 2021. 

studies \(i.e., 66.7%\). This reflects a need for effective train-

\[3\] H. A. Ignatious, M. Khan et al., “An overview of sensors in autonomous vehicles,” Procedia Computer Science, vol. 198, pp. 736–741, 2022. 

ing methods to ensure smooth vehicle maneuvering in these

\[4\] “Self-driving cars: A survey,” Expert Systems with Applications, vol. 

challenging contexts. Interpretability is particularly valued at 165, p. 113816, 2021. 

ramps in 9 studies \(i.e., 56.25%\) and on highways in 11 studies

\[5\] J. Pérez, V. Milanés et al., “Autonomous driving manoeuvres in urban road traffic environment: a study on roundabouts,” IFAC Proceedings \(i.e., 36.7%\), respectively. This emphasizes understandable Volumes, vol. 44, no. 1, pp. 13 795–13 800, 2011. 

decision-making in these areas. Unselfishness receives less

\[6\] Z. Lin, Q. Zhang, Z. Tian, P. Yu, and J. Lan, “Dpl-slam: Enhancing emphasis overall, although highways and ramps give it much dynamic point-line slam through dense semantic methods,” IEEE

Sensors Journal, 2024. 

attention. Future challenges are summarized as

\[7\] Z. Lin, Q. Zhang, Z. Tian, P. Yu, Z. Ye, H. Zhuang, and J. Lan, “Slam2: 1\) Achieving a balance between all five DDTUI factors in Simultaneous localization and multimode mapping for indoor dynamic a single framework: This survey reveals that while many environments,” Pattern Recognition, p. 111054, 2024. 

\[8\] World Health Organization, “Road traffic injuries,” https://www.who. 

studies addressed multiple DDTUI factors, very few

int/news-room/fact-sheets/detail/road-traffic-injuries, 2023, accessed: managed to incorporate all five factors simultaneously. 

2024-04-28. 

For instance, only 3 out of 16 studies in roundabout sce-

\[9\] H. Vijayakumar, D. Zhao et al., “A holistic safe planner for automated driving considering interaction with human drivers,” IEEE Transaction narios and 1 out of 19 studies in intersection scenarios on Intelligent Vehicle, vol. 9, no. 1, pp. 2061–2076, 2023. 

addressed all five factors. This highlights the complexity

\[10\] J. Löfberg, Minimax approaches to robust model predictive control. 

of developing a unified framework that can effectively Linköping University Electronic Press, 2003, vol. 812. 

\[11\] S. V. Raković, “Model predictive control: classical, robust, and stochas-balance DDTUI. Future research should focus on devel-tic \[bookshelf\],” IEEE Control Systems Magazine, vol. 36, no. 6, pp. 

oping integrated frameworks that can holistically address 102–105, 2016. 

five DDTUI factors concurrently. 

\[12\] Z. Lin, Z. Tian et al., “Enhanced visual slam for collision-free driving 2\) Improving the interpretability of DRL models without with lightweight autonomous cars,” Sensors, vol. 24, no. 19, p. 6258, 2024. 

sacrificing performance: While some studies have made

\[13\] P. Bhattacharya and M. L. Gavrilova, “Voronoi diagram in optimal path strides in improving interpretability, such as using IDM

planning,” in Proceedings of the International Symposium on Voronoi for interpretable car-following, many high-performing Diagrams in Science and Engineering, 2007, pp. 38–47. 

\[14\] M. Abdel-Aty and S. Ding, “A matched case-control analysis of DRL models remain black boxes. Out of the reviewed autonomous vs human-driven vehicle accidents,” Nature Communica-papers, less than 40% explicitly addressed interpretabil-tions, vol. 15, no. 1, p. 4931, 2024. 

ity. Furthermore, most papers considering interpretabil-

\[15\] H. H. Triharminto, O. Wahyunggoro et al., “A novel of repulsive function on artificial potential field for robot path planning,” International ity use only one method. In the future, multiple in-Journal of Electrical and Computer Engineering, vol. 6, no. 6, p. 3262, terpretability methods can be applied to enhance inter-2016. 

17

\[16\] Q. Yao, Z. Zheng et al., “Path planning method with improved artificial Landscapes and trends,” ACM Transactions on Software Engineering potential field—a reinforcement learning perspective,” IEEE Access, and Methodology, vol. 32, no. 5, pp. 1–62, 2023. 

vol. 8, pp. 135 513–135 523, 2020. 

\[41\] K. Yang, X. Tang et al., “Towards robust decision-making for au-

\[17\] H. H. Triharminto, O. Wahyunggoro et al., “Local information using tonomous driving on highway,” IEEE Transactions on Vehicular Tech-stereo camera in artificial potential field based path planning,” IAENG

nology, vol. 72, no. 9, pp. 11 251–11 263, 2023. 

International Journal of Computer Science, vol. 44, no. 3, pp. 316–326, 

\[42\] J. Wu, Z. Song et al., “Deep reinforcement learning-based energy-2017. 

efficient decision-making for autonomous electric vehicle in dynamic

\[18\] B. Mahesh, “Machine learning algorithms-a review,” International traffic environments,” IEEE Transactions on Transportation Electrifi-Journal of Science and Research \(IJSR\).\[Internet\], vol. 9, no. 1, pp. 

cation, vol. 10, no. 1, pp. 875–887, 2023. 

381–386, 2020. 

\[43\] Y. Fu, C. Li et al., “An incentive mechanism of incorporating su-

\[19\] M. I. Jordan and T. M. Mitchell, “Machine learning: Trends, perspec-pervision game for federated learning in autonomous driving,” IEEE

tives, and prospects,” Science, vol. 349, no. 6245, pp. 255–260, 2015. 

Transactions on Intelligent Transportation Systems, vol. 24, no. 12, pp. 

\[20\] I. Muhammad and Z. Yan, “Supervised machine learning approaches: 14 800–14 812, 2023. 

A survey.” ICTACT Journal on Soft Computing, vol. 5, no. 3, 2015. 

\[44\] W. Yue, X. Wu, C. Li, N. Cheng, P. Duan, and Z. Han, “Navigating the

\[21\] M. Castelli, L. Vanneschi et al., “Supervised learning: classification,” 

impact of connected and automated vehicles on mixed traffic efficiency: por Ranganathan, S., M. Grisbskov, K. Nakai y C. Schönbach, vol. 1, A driving behavior perspective,” IEEE Internet of Things Journal, 2024. 

pp. 342–349, 2018. 

\[45\] B. Toghi, R. Valiente, D. Sadigh, R. Pedarsani, and Y. P. Fallah, “Social

\[22\] R. Tian, S. Li et al., “Adaptive game-theoretic decision making for coordination and altruism in autonomous driving,” IEEE Transactions autonomous vehicle control at roundabouts,” in Proceedings of the on Intelligent Transportation Systems, vol. 23, no. 12, pp. 24 791–

IEEE Conference on Decision and Control. 

IEEE, 2018, pp. 321–

24 804, 2022. 

326. 

\[46\] Y. Liu, X. Zhao, Y. Tian, and J. Sun, “Sociality probe: Game-

\[23\] L. P. Kaelbling, M. L. Littman, and A. W. Moore, “Reinforcement theoretic inverse reinforcement learning for modeling and quantifying learning: A survey,” Journal of Artificial Intelligence Research, vol. 4, social patterns in driving interaction,” IEEE Transactions on Intelligent pp. 237–285, 1996. 

Transportation Systems, 2024. 

\[24\] J. Lu, L. Han et al., “Event-triggered deep reinforcement learning

\[47\] X. Huang, D. Kroening, W. Ruan, J. Sharp, Y. Sun, E. Thamo, M. Wu, using parallel control: A case study in autonomous driving,” IEEE

and X. Yi, “A survey of safety and trustworthiness of deep neural Transactions on Intelligent Vehicles, vol. 8, no. 4, pp. 2821–2831, 2023. 

networks: Verification, testing, adversarial attack and defence, and

\[25\] Y. LeCun, Y. Bengio, and G. Hinton, “Deep learning,” nature, vol. 521, interpretability,” Computer Science Review, vol. 37, p. 100270, 2020. 

no. 7553, pp. 436–444, 2015. 

\[48\] F.-L. Fan, J. Xiong, M. Li, and G. Wang, “On interpretability of

\[26\] I. Goodfellow, Deep learning. 

MIT Press, 2016, vol. 196. 

artificial neural networks: A survey,” IEEE Transactions on Radiation

\[27\] K. Yeom, “Deep reinforcement learning based autonomous driving with and Plasma Medical Sciences, vol. 5, no. 6, pp. 741–760, 2021. 

collision free for mobile robots,” International Journal of Mechanical

\[49\] D. Karas, “Highway to inequity: the disparate impact of the interstate Engineering and Robotics Research, vol. 11, no. 5, pp. 338–344, 2022. 

highway system on poor and minority communities in american cities,” 

\[28\] A. J. M. Muzahid, S. F. Kamarulzaman et al., “Deep reinforcement New Visions for Public Affairs, vol. 7, no. April, pp. 9–21, 2015. 

learning-based driving strategy for avoidance of chain collisions and

\[50\] M. Gross, “Speed tourism: The german autobahn as a tourist destination its safety efficiency analysis in autonomous vehicles,” IEEE Access, and location of “unruly rules”,” Tourist Studies, vol. 20, no. 3, pp. 298–

vol. 10, pp. 43 303–43 319, 2022. 

313, 2020. 

\[29\] C. Xu, W. Zhao et al., “A Nash Q-learning based motion decision

\[51\] J. P. Leisch, “Freeway and interchange design: A historical perspec-algorithm with considering interaction to traffic participants,” IEEE

tive,” Transportation Research Record, pp. 60–60, 1993. 

Transactions on Vehicular Technology, vol. 69, no. 11, pp. 12 621–

\[52\] G. Davis, M. Contreras-Sweet et al., “Ramp meter design manual,” 

12 634, 2020. 

Traffic Operation Program, Department of California Highway Patrol, 

\[30\] K. Min, H. Kim et al., “Deep Q learning based high level driving 2000. 

policy determination,” in Proceedings of the IEEE Intelligent Vehicles

\[53\] A. Pratelli and R. R. Souleyrette, “Visibility, perception and roundabout Symposium, 2018, pp. 226–231. 

safety,” WIT Transactions on the Built Environment, vol. 107, pp. 577–

\[31\] S. Gu, T. Lillicrap et al., “Continuous deep Q-learning with model-588, 2009. 

based acceleration,” in Proceedings of the International Conference on Machine Learning, 2016, pp. 2829–2838. 

\[54\] M. Naderi, M. Papageorgiou et al., “Automated vehicle driving on

\[32\] H. Wei, X. Liu

large lane-free roundabouts,” in Proceeding of the IEEE International et al., “Mixed-autonomy traffic control with proximal Conference on Intelligent Transportation Systems policy optimization,” in

, 2022, pp. 1528–

Proceedings of the IEEE Vehicular Networking 1535. 

Conference, 2019, pp. 1–8. 

\[33\] F. Ye, X. Cheng et al., “Automated lane change strategy using proximal

\[55\] J. G. Bared, P. K. Edara et al., “Design and operational performance policy optimization-based deep reinforcement learning,” in Proceedings of double crossover intersection and diverging diamond interchange,” 

of the IEEE Intelligent Vehicles Symposium, 2020, pp. 1746–1752. 

Transportation Research Record, vol. 1912, no. 1, pp. 31–38, 2005. 

\[34\] G. Dulac-Arnold, R. Evans et al., “Deep reinforcement learning in large

\[56\] J. York and T. Maze, “Economic evaluation of truck collision warning discrete action spaces. arxiv 2015,” arXiv preprint arXiv:1512.07679. 

systems,” Transportation Research Circular, vol. 475, pp. 46–50, 1997. 

\[35\] Z. Tian, D. Zhao et al., “Efficient and balanced exploration-driven

\[57\] I. C. Burnett, Traffic Collisions in North Carolina: Weather, Human decision making for autonomous racing using local information,” IEEE

Factors, and Economic Analysis, 2013 to 2019. 

North Carolina State

Transactions on Intelligent Vehicles, 2024. 

University, 2023. 

\[36\] Z. Tian, D. Zhao, Z. Lin, D. Flynn, W. Zhao, and D. Tian, “Balanced

\[58\] J. Wang, J. Wu, X. Zheng, D. Ni, and K. Li, “Driving safety field reward-inspired reinforcement learning for autonomous vehicle racing,” 

theory modeling and its application in pre-collision warning system,” 

in 6th Annual Learning for Dynamics & Control Conference. PMLR, Transportation Research Part C: Emerging Technologies, vol. 72, pp. 

2024, pp. 628–640. 

306–324, 2016. 

\[37\] G. Basile, A. Petrillo, and S. Santini, “DDPG based end-to-end driving

\[59\] R. Nahata, D. Omeiza, R. Howard, and L. Kunze, “Assessing and enhanced with safe anomaly detection functionality for autonomous explaining collision risk in dynamic environments for autonomous vehicles,” in Proceedings of the IEEE International Conference on driving safety,” in Proceeding of the IEEE International Intelligent Metrology for Extended Reality, Artificial Intelligence and Neural Transportation Systems Conference. 

IEEE, 2021, pp. 223–230. 

Engineering, 2022, pp. 248–253. 

\[60\] M. Wang, L. Zhang, Z. Zhang, and Z. Wang, “A hybrid trajectory

\[38\] M. A. Hebaish, A. Hussein et al., “Towards safe and efficient modular planning strategy for intelligent vehicles in on-road dynamic scenarios,” 

path planning using twin delayed DDPG,” in Proceedings of the IEEE

IEEE Transactions on Vehicular Technology, vol. 72, no. 3, pp. 2832–

Vehicular Technology Conference, 2022, pp. 1–7. 

2847, 2023. 

\[39\] L. Abualigah, S. Ekinci et al., “Modified elite opposition-based ar-

\[61\] A. Botros and S. L. Smith, “Spatio-temporal lattice planning using tificial hummingbird algorithm for designing fopid controlled cruise optimal motion primitives,” IEEE Transactions on Intelligent Trans-control system.” Intelligent Automation & Soft Computing, vol. 38, portation Systems, 2023. 

no. 2, 2023. 

\[62\] W. Chen, Y. Chen et al., “Motion planning using feasible and smooth

\[40\] S. Tang, Z. Zhang, Y. Zhang, J. Zhou, Y. Guo, S. Liu, S. Guo, Y.-F. Li, tree for autonomous driving,” IEEE Transactions on Vehicular Tech-L. Ma, Y. Xue et al., “A survey on automated driving system testing: nology, vol. 73, no. 5, pp. 6270–6282, 2024. 

18

\[63\] F. Bouchard, S. Sedwards, and K. Czarnecki, “A rule-based behaviour

\[84\] P. M. Dassanayake, A. Anjum et al., “A deep learning based explainable planner for autonomous driving,” in Proceeding of the International control system for reconfigurable networks of edge devices,” IEEE

Joint Conference on Rules and Reasoning. 

Springer, 2022, pp. 263–

Transactions on Network Science and Engineering, vol. 9, no. 1, pp. 

279. 

7–19, 2021. 

\[64\] R. Gajjar and D. Mohandas, “Critical assessment of road capacities on

\[85\] M. Zemni, M. Chen et al., “Octet: Object-aware counterfactual expla-urban roads–a mumbai case-study,” Transportation Research Procedia, nations,” in Proceedings of the IEEE/CVF Conference on Computer vol. 17, pp. 685–692, 2016. 

Vision and Pattern Recognition, 2023, pp. 15 062–15 071. 

\[65\] M. A. S. Kamal, T. Hayakawa, and J.-i. Imura, “Road-speed profile

\[86\] Z. Chen, F. Xiao, F. Guo, and J. Yan, “Interpretable machine learning for enhanced perception of traffic conditions in a partially connected for building energy management: A state-of-the-art review,” Advances vehicle environment,” IEEE Transactions on Vehicular Technology, in Applied Energy, vol. 9, p. 100123, 2023. 

vol. 67, no. 8, pp. 6824–6837, 2018. 

\[87\] D. Leslie, “Understanding artificial intelligence ethics and safety,” 

\[66\] M. A. S. Kamal, S. Taguchi, and T. Yoshimura, “Efficient driving arXiv preprint arXiv:1906.05684, 2019. 

on multilane roads under a connected vehicle environment,” IEEE

\[88\] S. Hooker, D. Erhan, P.-J. Kindermans, and B. Kim, “A benchmark for Transactions on Intelligent Transportation Systems, vol. 17, no. 9, pp. 

interpretability methods in deep neural networks,” Advances in Neural 2541–2551, 2016. 

Information Processing Systems, vol. 32, 2019. 

\[67\] D. A. Hensher, “Valuation of travel time savings,” in A handbook of

\[89\] R. Tomsett, D. Harborne, S. Chakraborty, P. Gurram, and A. Preece, transport economics. 

Edward Elgar Publishing, 2011. 

“Sanity checks for saliency metrics,” in Proceedings of the AAAI

\[68\] F. Steck, V. Kolarova, F. Bahamonde-Birke, S. Trommer, and B. Lenz, Conference on Artificial Intelligence, vol. 34, no. 04, 2020, pp. 6021–

“How autonomous driving may affect the value of travel time savings 6029. 

for commuting,” Transportation Research Record, vol. 2672, no. 46, 

\[90\] J. Adebayo, J. Gilmer, M. Muelly, I. Goodfellow, M. Hardt, and pp. 11–20, 2018. 

B. Kim, “Sanity checks for saliency maps,” Advances in neural

\[69\] C. Zhai, F. Luo, Y. Liu, and Z. Chen, “Ecological cooperative look-information processing systems, vol. 31, 2018. 

ahead control for automated vehicles travelling on freeways with

\[91\] A. Ghorbani, A. Abid, and J. Zou, “Interpretation of neural networks varying slopes,” IEEE Transactions on Vehicular Technology, vol. 68, is fragile,” in Proceedings of the AAAI Conference on Artificial Intel-no. 2, pp. 1208–1221, 2018. 

ligence, vol. 33, no. 01, 2019, pp. 3681–3688. 

\[70\] S. A. Birrell, M. Fowkes et al., “Effect of using an in-vehicle smart

\[92\] A. A. Ismail, M. Gunady, L. Pessoa, H. Corrada Bravo, and S. Feizi, driving aid on real-world driver performance,” IEEE Transactions on

“Input-cell attention reduces vanishing saliency of recurrent neural net-Intelligent Transportation Systems, vol. 15, no. 4, pp. 1801–1810, 2014. 

works,” Advances in Neural Information Processing Systems, vol. 32, 

\[71\] C. Sun, J. Guanetti et al., “Optimal eco-driving control of connected 2019. 

and autonomous vehicles through signalized intersections,” IEEE In-

\[93\] M. Wu, M. Hughes, S. Parbhoo, M. Zazzi, V. Roth, and F. Doshi-Velez, ternet of Things Journal, vol. 7, no. 5, pp. 3759–3773, 2020. 

“Beyond sparsity: Tree regularization of deep models for interpretabil-

\[72\] A. Srinivas, T.-Y. Lin, N. Parmar, J. Shlens, P. Abbeel, and A. Vaswani, ity,” in Proceedings of the AAAI Conference on Artificial Intelligence, 

“Bottleneck transformers for visual recognition,” in Proceedings of the vol. 32, no. 1, 2018. 

IEEE/CVF Conference on Computer Vision and Pattern Recognition, 

\[94\] T. Speith and M. Langer, “A new perspective on evaluation methods 2021, pp. 16 519–16 529. 

for explainable artificial intelligence \(xai\),” in Proceeding of the

\[73\] R. Xu, J. Joshi et al., “Nn-emd: Efficiently training neural networks IEEE International Requirements Engineering Conference Workshops. 

using encrypted multi-sourced datasets,” IEEE Transactions on De-IEEE, 2023, pp. 325–331. 

pendable and Secure Computing, vol. 19, no. 4, pp. 2807–2820, 2021. 

\[95\] A. Baheri, S. Nageshrao et al., “Deep reinforcement learning with

\[74\] H. Touvron, P. Bojanowski et al., “Resmlp: Feedforward networks for enhanced safety for autonomous highway driving,” in Proceeding of image classification with data-efficient training,” IEEE transactions on the IEEE Intelligent Vehicles Symposium, 2020, pp. 1550–1555. 

Pattern Analysis and Machine Intelligence, vol. 45, no. 4, pp. 5314–

\[96\] M. Kaushik, V. Prasad et al., “Overtaking maneuvers in simulated 5321, 2022. 

highway driving using deep reinforcement learning,” in 2018 IEEE

\[75\] C. M. Martinez, M. Heucke, F.-Y. Wang, B. Gao, and D. Cao, “Driving Intelligent Vehicles Symposium. 

IEEE, 2018, pp. 1885–1890. 

style recognition for intelligent vehicle control and advanced driver

\[97\] N. Albarella, D. G. Lui et al., “A hybrid deep reinforcement learning assistance: A survey,” IEEE Transaction on Intelligent Transportation and optimal control architecture for autonomous highway driving,” 

System, vol. 19, no. 3, pp. 666–676, 2017. 

Energies, vol. 16, no. 8, p. 3490, 2023. 

\[76\] X. Li, W. Wang, and M. Roetting, “Estimating driver’s lane-change intent considering driving style and contextual traffic,” IEEE Transactions

\[98\] H. Meng, H. Bin et al., “Optimizing distributed energy system with an on Intelligent Transportation Systems, vol. 20, no. 9, pp. 3258–3271, enhanced reinforcement learning–model predictive control algorithm,” 

2018. 

Available at SSRN 4876862. 

\[77\] D. Xu, H. Zhao, F. Guillemard, S. Geronimi, and F. Aioun, “Aware

\[99\] Z. Lin, Z. Tian et al., “A conflicts-free, speed-lossless KAN-based of scene vehicles—probabilistic modeling of car-following behaviors reinforcement learning decision system for interactive driving in roundin real-world traffic,” IEEE Transactions on Intelligent Transportation abouts,” arXiv preprint arXiv:2408.08242, 2024. 

Systems, vol. 20, no. 6, pp. 2136–2148, 2018. 

\[100\] J. Gómez-Romero, “Explaining deep reinforcement learning-based

\[78\] P. Jardin, I. Moisidis, S. S. Zetina, and S. Rinderknecht, “Rule-methods for control of building hvac systems,” Methods, vol. 15, p. 52. 

based driving style classification using acceleration data profiles,” 

\[101\] S. Shalev-Shwartz, S. Shammah et al., “Safe, multi-agent, re-in Proceeding of the IEEE International Conference on Intelligent inforcement

learning

for

autonomous

driving,” 

arXiv

preprint

Transportation Systems, 2020, pp. 1–6. 

arXiv:1610.03295, 2016. 

\[79\] R. Vogel, F. Schmidsberger, A. Kühn, K. A. Schneider et al., “You can’t

\[102\] C. Yu, X. Wang, J. Hao, and Z. Feng, “Reinforcement learning for drive my car-a method to fingerprint individual driving styles in a sim-cooperative overtaking,” in Proceedings of the International Conference racing setting,” in Proceeding of the IEEE International Conference on on Autonomous Agents and Multiagent Systems, 2019, pp. 341–349. 

Electrical, Computer and Energy Technologies, 2022, pp. 1–9. 

\[103\] M. B. Ozcelik, B. Agin et al., “Decision making for autonomous driv-

\[80\] F. Lateef, M. Kas et al., “Saliency heat-map as visual attention for ing in a virtual highway environment based on generative adversarial autonomous driving using generative adversarial network \(GAN\),” 

imitation learning,” in Proceeding of the Innovations in Intelligent IEEE Transactions on Intelligent Transportation Systems, vol. 23, no. 6, Systems and Applications Conference, 2023, pp. 1–6. 

pp. 5360–5373, 2022. 

\[104\] S. Zhang, Y. Wu et al., “Spatial attention for autonomous decision-

\[81\] N. Ding, C. Zhang et al., “Saliendet: A saliency-based feature enhance-making in highway scene,” in Proceeding of the Annual Conference of ment algorithm for object detection for autonomous driving,” IEEE

the Society of Instrument and Control Engineers of Japan, 2020, pp. 

Transactions on Intelligent Vehicles, vol. 9, no. 1, pp. 2624–2635, 2023. 

1435–1440. 

\[82\] Z. Cui, M. Li et al., “An interpretation framework for autonomous

\[105\] M. Treiber, A. Hennecke, and D. Helbing, “Congested traffic states in vehicles decision-making via shap and rf,” in Proceeding of the CAA empirical observations and microscopic simulations,” Physical Review International Conference on Vehicular Control and Intelligence, 2022, E, vol. 62, no. 2, p. 1805, 2000. 

pp. 1–7. 

\[106\] S. Nageshrao, H. E. Tseng, and D. Filev, “Autonomous highway

\[83\] B. 

Gyevnar, 

C. 

Wang

et

al., 

“Causal

explanations

for

se-

driving using deep reinforcement learning,” in Proceedings of the IEEE

quential decision-making in multi-agent systems,” arXiv preprint International Conference on Systems, Man and Cybernetics, 2019, pp. 

arXiv:2302.10809, 2023. 

2326–2331. 

19

\[107\] J. Zhao, T. Qu et al., “A deep reinforcement learning approach for on Intelligent Transportation Systems, vol. 23, no. 8, pp. 10 902–10 911, autonomous highway driving,” IFAC-PapersOnLine, vol. 53, no. 5, pp. 

2022. 

542–546, 2020. 

\[129\] S. Cheng, B. Yang, Z. Wang, and K. Nakano, “Spatio-temporal

\[108\] W. Zhao, S. Gong, D. Zhao, F. Liu, N. Sze, M. Quddus, and H. Huang, image representation and deep-learning-based decision framework for

“A spatial-state-based omni-directional collision warning system for automated vehicles,” IEEE Transactions on Intelligent Transportation intelligent vehicles,” IEEE Transactions on Intelligent Transportation Systems, vol. 23, no. 12, pp. 24 866–24 875, 2022. 

Systems, 2024. 

\[130\] B. Liu, Y. Tang et al., “A deep reinforcement learning approach for

\[109\] B. M. Albaba and Y. Yildiz, “Driver modeling through deep rein-ramp metering based on traffic video data,” Journal of Advanced forcement learning and behavioral game theory,” IEEE Transactions Transportation, vol. 2021, no. 1, p. 6669028, 2021. 

on Control Systems Technology, vol. 30, no. 2, pp. 885–892, 2021. 

\[131\] M. Yang, Z. Li et al., “A deep reinforcement learning-based ramp

\[110\] J. Yang, A. Nakhaei et al., “Cm3: Cooperative multi-goal multi-stage metering control framework for improving traffic operation at freeway multi-agent reinforcement learning,” arXiv preprint arXiv:1809.05188, weaving sections,” in Proceedings of the Transportation Research 2018. 

Board Annual Meeting, Washington, DC, USA, 2019, pp. 13–17. 

\[111\] M. Schutera, N. Goby et al., “Transfer learning versus multi-agent

\[132\] P. Wang and C.-Y. Chan, “Formulation of deep reinforcement learning learning regarding distributed decision-making in highway traffic,” 

architecture toward autonomous driving for on-ramp merge,” in Pro-arXiv preprint arXiv:1810.08515, 2018. 

ceedings of the International Conference on Intelligent Transportation

\[112\] X. Xu, L. Zuo et al., “A reinforcement learning approach to au-Systems, 2017, pp. 1–6. 

tonomous decision making of intelligent vehicles on highways,” IEEE

\[133\] Y. Lin, J. McPhee et al., “Anti-jerk on-ramp merging using deep Transactions on Systems, Man, and Cybernetics: Systems, vol. 50, reinforcement learning,” in Proceedings of the Intelligent Vehicles no. 10, pp. 3884–3897, 2018. 

Symposium. 

IEEE, 2020, pp. 7–14. 

\[113\] Z. Bai, W. Shangguan et al., “Deep reinforcement learning based high-

\[134\] F. Deng, J. Jin et al., “Advanced self-improving ramp metering algo-level driving behavior decision-making model in heterogeneous traffic,” 

rithm based on multi-agent deep reinforcement learning,” in Proceeding in Proceeding of the IEEE Chinese Control Conference. IEEE, 2019, of the IEEE Intelligent Transportation Systems Conference, 2019, pp. 

pp. 8600–8605. 

3804–3809. 

\[114\] T. Liu, Q. Liu et al., “Combining deep reinforcement learning with

\[135\] M. Cheng, C. Zhang et al., “Adaptive coordinated variable speed rule-based constraints for safe highway driving,” in Proceeding of the limit between highway mainline and on-ramp with deep reinforcement China Automation Congress, 2022, pp. 2785–2790. 

learning,” Journal of Advanced Transportation, vol. 2022, no. 1, p. 

\[115\] J. Liao, T. Liu et al., “Decision-making strategy on highway for 2435643, 2022. 

autonomous vehicles using deep reinforcement learning,” IEEE Access, 

\[136\] S. Zhou, W. Zhuang et al., “Cooperative on-ramp merging control of vol. 8, pp. 177 804–177 814, 2020. 

connected and automated vehicles: Distributed multi-agent deep rein-

\[116\] W. Yuan, M. Yang et al., “Multi-reward architecture based reinforce-forcement learning approach,” in Proceeding of the IEEE International ment learning for highway driving policies,” in Proceeding of the IEEE

Conference on Intelligent Transportation Systems, 2022, pp. 402–408. 

Intelligent Transportation Systems Conference, 2019, pp. 3810–3815. 

\[137\] Z. Hu and W. Ma, “Guided deep reinforcement learning for coordi-

\[117\] S. Aradi, T. Becsi et al., “Policy gradient based reinforcement learning nated ramp metering and perimeter control in large scale networks,” 

approach for autonomous highway driving,” in Proceeding of the IEEE

Transportation Research Part C: Emerging Technologies, vol. 159, p. 

Conference on Control Technology and Applications. IEEE, 2018, pp. 

104461, 2024. 

670–675. 

\[138\] D. Deng, B. Yu et al., “Automated traffic state optimization in the

\[118\] H. Wang, S. Yuan et al., “Tactical driving decisions of unmanned weaving area of urban expressways by a reinforcement learning-based ground vehicles in complex highway environments: A deep reinforce-cooperative method of channelization and ramp metering,” Journal of ment learning approach,” Proceedings of the Institution of Mechanical Advanced Transportation, vol. 2023, no. 1, p. 4771946, 2023. 

Engineers, Part D: Journal of Automobile Engineering, vol. 235, no. 4, 

\[139\] C. Wang, Y. Xu et al., “Integrated traffic control for freeway recurrent pp. 1113–1127, 2021. 

bottleneck based on deep reinforcement learning,” IEEE Transactions

\[119\] A. M. Naveen, R. Ravish et al., “Distributional reinforcement learning on Intelligent Transportation Systems, vol. 23, no. 9, pp. 15 522–15 535, for automated driving vehicle,” in Proceeding of the IEEE Mysore Sub 2022. 

Section International Conference, 2022, pp. 1–6. 

\[140\] X. Qi, L. Zhang et al., “Learning-based mpc for autonomous motion

\[120\] J. Wang, T. Yang et al., “Learning an efficient and safe policy for planning at freeway off-ramp diverging,” IEEE Transactions on Intel-highway driving using supervised learning and reinforcement learning,” 

ligent Vehicles, pp. 1–11, 2024. 

in Proceeding of the International Conference on Real-time Computing

\[141\] Z. e. a. Kherroubi, S. Aknine, and R. Bacha, “Novel decision-making and Robotics, 2019, pp. 112–117. 

strategy for connected and autonomous vehicles in highway on-ramp

\[121\] K. Lv, X. Pei, C. Chen, and J. Xu, “A safe and efficient lane merging,” IEEE Transactions on Intelligent Transportation Systems, change decision-making strategy of autonomous driving based on deep vol. 23, no. 8, pp. 12 490–12 502, 2022. 

reinforcement learning,” Mathematics, vol. 10, no. 9, p. 1551, 2022. 

\[142\] X. Zhang, L. Wu et al., “High-speed ramp merging behavior decision

\[122\] R. R˘adulescu, M. Legrand et al., “Deep multi-agent reinforcement for autonomous vehicles based on multiagent reinforcement learning,” 

learning in a homogeneous open population,” in Artificial Intelligence: IEEE Internet of Things Journal, vol. 10, no. 24, pp. 22 664–22 672, 30th Benelux Conference, BNAIC 2018,‘s-Hertogenbosch, The Nether-2023. 

lands, November 8–9, 2018, Revised Selected Papers 30. 

Springer, 

\[143\] D. Chen, M. R. Hajidavalloo et al., “Deep multi-agent reinforcement 2019, pp. 90–105. 

learning for highway on-ramp merging in mixed traffic,” IEEE Transac-

\[123\] C. Yu, X. Wang et al., “Distributed multiagent coordinated learning tions on Intelligent Transportation Systems, vol. 24, no. 11, pp. 11 623–

for autonomous driving in highways based on dynamic coordination 11 638, 2023. 

graphs,” IEEE Transactions on Intelligent Transportation Systems, 

\[144\] X. He, B. Lou et al., “Robust decision making for autonomous vehicles vol. 21, no. 2, pp. 735–748, 2020. 

at highway on-ramps: A constrained adversarial reinforcement learning

\[124\] M. Kaushik, N. Singhania et al., “Parameter sharing reinforcement approach,” IEEE Transactions on Intelligent Transportation Systems, learning architecture for multi agent driving,” in Proceedings of the vol. 24, no. 4, pp. 4103–4113, 2023. 

2019 4th International Conference on Advances in Robotics, 2019, pp. 

\[145\] M. Li, Z. Li et al., “Enhancing cooperation of vehicle merging control 1–7. 

in heavy traffic using communication-based soft actor-critic algorithm,” 

\[125\] M. Molaie, A. Amirkhani et al., “Auto-driving policies in highway IEEE Transactions on Intelligent Transportation Systems, vol. 24, no. 6, based on distributional deep reinforcement learning,” in Proceeding pp. 6491–6506, 2023. 

of the International Conference on Pattern Recognition and Image

\[146\] J. Chen, B. Yuan et al., “Model-free deep reinforcement learning for Analysis, 2021, pp. 1–6. 

urban autonomous driving,” in Proceeding of the IEEE Intelligent

\[126\] G. Chen, Y. Zhang et al., “Attention-based highway safety planner for Transportation Systems Conference. 

IEEE, 2019, pp. 2765–2771. 

autonomous driving via deep reinforcement learning,” IEEE Transac-

\[147\] G. Bacchiani, D. Molinari, and M. Patander, “Microscopic traffic tions on Vehicular Technology, vol. 73, no. 1, pp. 162–175, 2024. 

simulation by cooperative multi-agent deep reinforcement learning,” 

\[127\] K. Min, H. Kim et al., “Deep distributional reinforcement learning arXiv preprint arXiv:1903.01365, 2019. 

based high-level driving policy determination,” IEEE Transactions on

\[148\] B. Montgomery, C. Muise et al., “Hierarchical deep reinforcement Intelligent Vehicles, vol. 4, no. 3, pp. 416–424, 2019. 

learning with cross-attention and planning for autonomous roundabout

\[128\] B. Gangopadhyay, H. Soora et al., “Hierarchical program-triggered re-navigation,” in Proceeding of the Canadian Conference on Electrical inforcement learning agents for automated driving,” IEEE Transactions and Computer Engineering, 2024, pp. 417–423. 

20

\[149\] Y. Tian, M. Han, L. Zhang, W. Liu, J. Wang, and W. Pan, “Variational Intelligent Transportation Systems, vol. 25, no. 8, pp. 10 147–10 160, constrained reinforcement learning with application to planning at 2024. 

roundabout,” 2020. 

\[169\] W. X. Hu, H. Ishihara, C. Chen, A. Shalaby, and B. Abdulhai, “Deep

\[150\] W. Wang, L. Jiang et al., “Imitation learning based decision-making for reinforcement learning two-way transit signal priority algorithm for autonomous vehicle control at traffic roundabouts,” Multimedia Tools optimizing headway adherence and speed,” IEEE Transactions on and Applications, vol. 81, no. 28, pp. 39 873–39 889, 2022. 

Intelligent Transportation Systems, vol. 24, no. 8, pp. 7920–7931, 2023. 

\[151\] L. Ferrarotti, M. Luca, G. Santin, G. Previati, G. Mastinu, M. Gobbi, 

\[170\] A. Lombard, A. Noubli, A. Abbas-Turki, N. Gaud, and S. Galland, E. Campi, L. Uccello, A. Albanese, P. Zalaya et al., “Autonomous and

“Deep reinforcement learning approach for v2x managed intersections human-driven vehicles interacting in a roundabout: A quantitative and of connected vehicles,” IEEE Transactions on Intelligent Transporta-qualitative evaluation,” IEEE Access, 2024. 

tion Systems, vol. 24, no. 7, pp. 7178–7189, 2023. 

\[152\] Y. Zhang, B. Gao et al., “Adaptive decision-making for automated

\[171\] D. Li, J. Wu et al., “Adaptive traffic signal control model on inter-vehicles under roundabout scenarios using optimization embedded sections based on deep reinforcement learning,” Journal of Advanced reinforcement learning,” IEEE Transactions on Neural Networks and Transportation, vol. 2020, no. 1, p. 6505893, 2020. 

Learning Systems, vol. 32, no. 12, pp. 5526–5538, 2021. 

\[172\] H. Shu, T. Liu, X. Mu, and D. Cao, “Driving tasks transfer using deep

\[153\] F. Konstantinidis, M. Sackmann, O. De Candido, U. Hofmann, J. Thi-reinforcement learning for decision-making of autonomous vehicles in elecke, and W. Utschick, “Parameter sharing reinforcement learning unsignalized intersection,” IEEE Transactions on Vehicular Technology, for modeling multi-agent driving behavior in roundabout scenarios,” in vol. 71, no. 1, pp. 41–52, 2021. 

Proceeding of the IEEE Intelligent Transportation Systems Conference, 

\[173\] H. Seong, C. Jung, S. Lee, and D. H. Shim, “Learning to drive at 2021, pp. 1974–1981. 

unsignalized intersections using attention-based deep reinforcement

\[154\] R. Nakaya, T. Harada et al., “Emergence of cooperative automated learning,” in Proceeding of the IEEE International Intelligent Trans-driving control at roundabouts using deep reinforcement learning,” in portation Systems Conference, 2021, pp. 559–566. 

Proceeding of the Annual Conference of the Society of Instrument and

\[174\] C.-J. Hoel, T. Tram, and J. Sjöberg, “Reinforcement learning with Control Engineers, 2023, pp. 97–102. 

uncertainty estimation for tactical decision-making in intersections,” 

\[155\] H. Yuan, P. Li et al., “Safe, efficient, comfort, and energy-saving in Proceeding of the IEEE International Conference on Intelligent automated driving through roundabout based on deep reinforcement Transportation Systems. 

IEEE, 2020, pp. 1–7. 

learning,” in Proceeding of the IEEE International Conference on

\[175\] G.-P. Antonio and C. Maria-Dolores, “Multi-agent deep reinforcement Intelligent Transportation Systems. 

IEEE, 2023, pp. 6074–6079. 

learning to manage connected autonomous vehicles at tomorrow’s

\[156\] W. Wang, F. Hui et al., “Deep reinforcement learning method for intersections,” IEEE Transactions on Vehicular Technology, vol. 71, trajectory planning of connected and autonomous vehicles in the no. 7, pp. 7033–7043, 2022. 

roundabout lane-changing scenario,” in Proceeding of the International

\[176\] W. Xiao, Y. Yang, X. Mu, Y. Xie, X. Tang, D. Cao, and T. Liu, Symposium on Computer Technology and Information Science, 2024, 

“Decision-making for autonomous vehicles in random task scenarios pp. 168–173. 

at unsignalized intersection using deep reinforcement learning,” IEEE

\[157\] A. P. Capasso, G. Bacchiani et al., “From simulation to real world Transactions on Vehicular Technology, vol. 73, no. 6, pp. 7812–7825, maneuver execution using deep reinforcement learning,” in Proceeding 2024. 

of the IEEE Intelligent Vehicles Symposium. 

IEEE, 2020, pp. 1570–

\[177\] Z. Guo, Y. Wu, L. Wang, and J. Zhang, “Coordination for con-1575. 

nected and automated vehicles at non-signalized intersections: A

\[158\] ——, “Intelligent roundabout insertion using deep reinforcement learn-value decomposition-based multiagent deep reinforcement learning ing,” arXiv preprint arXiv:2001.00786, 2020. 

approach,” IEEE Transactions on Vehicular Technology, vol. 72, no. 3, 

\[159\] S. Alighanbari and N. L. Azad, “Deep reinforcement learning with pp. 3025–3034, 2023. 

nmpc assistance nash switching for urban autonomous driving,” IEEE

\[178\] I. Osband, J. Aslanides, and A. Cassirer, “Randomized prior functions Transactions on Intelligent Vehicles, vol. 8, no. 3, pp. 2604–2615, 2023. 

for deep reinforcement learning,” Advances in Neural Information

\[160\] B. Peng, M. F. Keskin et al., “Connected autonomous vehicles for im-Processing Systems, vol. 31, 2018. 

proving mixed traffic efficiency in unsignalized intersections with deep reinforcement learning,” Communications in Transportation Research, vol. 1, p. 100017, 2021. 

\[161\] A. Pozzi, S. Bae, Y. Choi, F. Borrelli, D. M. Raimondo, and S. Moura, 

“Ecological velocity planning through signalized intersections: A deep reinforcement learning approach,” in Proceeding of the IEEE Conference on Decision and Control. 

IEEE, 2020, pp. 245–252. 

\[162\] K.-F. Chu, A. Y. S. Lam, and V. O. K. Li, “Traffic signal control using end-to-end off-policy deep reinforcement learning,” IEEE Transactions on Intelligent Transportation Systems, vol. 23, no. 7, pp. 7184–7195, 2022. 

\[163\] D. Quang Tran and S.-H. Bae, “Proximal policy optimization through a deep reinforcement learning framework for multiple autonomous vehicles at a non-signalized intersection,” Applied Sciences, vol. 10, no. 16, p. 5722, 2020. 

\[164\] Z. Bai, P. Hao, W. Shangguan, B. Cai, and M. J. Barth, “Hybrid reinforcement learning-based eco-driving strategy for connected and automated vehicles at signalized intersections,” IEEE Transactions on Intelligent Transportation Systems, vol. 23, no. 9, pp. 15 850–15 863, 2022. 

\[165\] R. Bautista-Montesano, R. Galluzzi et al., “Autonomous navigation at unsignalized intersections: A coupled reinforcement learning and model predictive control approach,” Transportation Research Part C: Emerging Technologies, vol. 139, p. 103662, 2022. 

\[166\] D. Li, F. Zhu, T. Chen, Y. D. Wong, C. Zhu, and J. Wu, “Coor-plt: A hierarchical control model for coordinating adaptive platoons of connected and autonomous vehicles at signal-free intersections based on deep reinforcement learning,” Transportation Research Part C: Emerging Technologies, vol. 146, p. 103933, 2023. 

\[167\] S. Kai, B. Wang et al., “A multi-task reinforcement learning approach for navigating unsignalized intersections,” in Proceeding of the IEEE

Intelligent Vehicles Symposium, 2020, pp. 1583–1588. 

\[168\] B. Zhou, Q. Zhou, S. Hu, D. Ma, S. Jin, and D.-H. Lee, “Cooperative traffic signal control using a distributed agent-based deep reinforcement learning with incentive communication,” IEEE Transactions on


# Document Outline

+ INTRODUCTION 
+ Road Features and Driving Tasks  
	+ Highways  
		+ Road Features and Driving Tasks 
		+ An Example of a Highway 

	+ On-ramping Merging  
		+ Road Features and Driving Tasks 
		+ Comparison with Highways 

	+ Roundabouts  
		+ Road Features and Driving Tasks 
		+ An Example of a Roundabout 

	+ Unsignalized Intersections  
		+ Road Features and Driving Tasks 
		+ An Example of an Unsignalized Intersection 


+ Rationale of the Evaluation Factors  
	+ Driving Safety 
	+ Driving Efficiency 
	+ Training Efficiency 
	+ Unselfishness 
	+ Algorithm Interpretability 

+ Deep Reinforcement Learning-based decision-making on Highways  
	+ Single-factor Methods for Highway Driving 
	+ Dual-factor Methods for Highway Driving 
	+ Three-factor Methods for Highway Driving 
	+ Four-factor Methods for Highway Driving 
	+ Five-factor Methods for Highway Driving 

+ Deep Reinforcement Learning-based decision-making in On-ramping Merging  
	+ Single-factor Methods for On-ramping Merging 
	+ Dual-factor Methods for On-ramping Merging 
	+ Three-factor Methods for On-ramping Merging 
	+ Four-factor Methods for On-ramping Merging 
	+ Five-factor Methods for On-ramping Merging 

+ Deep Reinforcement Learning-based decision-making at Roundabouts  
	+ Single-factor Methods for Roundabout Driving 
	+ Dual-factor Methods for Roundabout Driving 
	+ Three-factor Methods for Roundabout Driving 
	+ Four-factor Methods for Roundabout Driving 
	+ Five-factor Methods for Roundabout Driving 

+ Deep Reinforcement Learning-based decision-making at Unsignalized Intersections  
	+ Single-factor Methods for Intersection Driving 
	+ Dual-factor Methods for Unsignalized Intersection Driving 
	+ Three-factor Methods for Unsignalized Intersection Driving 
	+ Four-factor Methods for Unsignalized Intersection Driving 
	+ Five-factor Methods for Intersection Driving 

+ Conclusion and Discussion 
+ References



