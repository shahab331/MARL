## **IEEE VEHICULAR TECHNOLOGY SOCIETY SECTION**

Received December 8, 2021, accepted January 6, 2022, date of publication January 12, 2022, date of current version January 21, 2022. 

*Digital Object Identifier 10.1109/ACCESS.2022.3142450*

A Comprehensive Survey on Cooperative

Intersection Management for Heterogeneous

Connected Vehicles

ASHKAN GHOLAMHOSSEINIAN , \(Graduate Student Member, IEEE\), AND JOCHEN SEITZ , \(Member, IEEE\) Communication Networks Group, Technische Universität Ilmenau, 98693 Ilmenau, Germany Corresponding author: Ashkan Gholamhosseinian \(ashkan.gholamhosseinian@tu-ilmenau.de\) This work was supported by the Open Access Publication Fund of the Technische Universität Ilmenau. 

**ABSTRACT **Nowadays, with the advancement of technology, world is trending toward high mobility and dynamics. In this context, intersection management \(IM\) as one of the most crucial elements of the transportation sector demands high attention. Today, road entities including infrastructures, vulnerable road users \(VRUs\) such as motorcycles, moped, scooters, pedestrians, bicycles, and other types of vehicles such as trucks, buses, cars, emergency vehicles, and railway vehicles like trains or trams are able to communicate cooperatively using vehicle-to-everything \(V2X\) communications and provide traffic safety, efficiency, infotainment and ecological improvements. In this paper, we take into account different types of intersections in terms of signalized, semi-autonomous \(hybrid\) and autonomous intersections and conduct a comprehensive survey on various intersection management methods for heterogeneous connected vehicles \(CVs\). We consider heterogeneous classes of vehicles such as road and rail vehicles as well as VRUs including bicycles, scooters and motorcycles. All kinds of intersection goals, modeling, coordination architectures, scheduling policies are thoroughly discussed. Signalized and semi-autonomous intersections are assessed with respect to these parameters. We especially focus on autonomous intersection management \(AIM\) and categorize this section based on four major goals involving safety, efficiency, infotainment and environment. Each intersection goal provides an in-depth investigation on the corresponding literature from the aforementioned perspectives. Moreover, robustness and resiliency of IM are explored from diverse points of view encompassing sensors, information management and sharing, planning universal scheme, heterogeneous collaboration, vehicle classification, quality measurement, external factors, intersection types, localization faults, communication anomalies and channel optimization, synchronization, vehicle dynamics and model mismatch, model uncertainties, recovery, security and privacy. 

## **INDEX TERMS**

Vehicular ad-hoc networks \(VANETs\), intersection management \(IM\), vehicle-to-vehicle \(V2V\), vehicle-to-infrastructure \(V2I\), trajectory planning \(TP\), spatio-temporal \(ST\), connected autonomous vehicles \(CAVs\), vulnerable road users \(VRUs\), connected vehicles \(CVs\), autonomous vehicle \(AVs\). 

## **I. INTRODUCTION**

has a great impact on traffic safety, efficiency, infotainment Number of vehicles on the roads has grown dramatically and environment. Safety is recognized as one of the most in the recent years. In 2006, there were approximately important issues in IM in such a way that around one third of 250 million commercial vehicles and 680 million passenger accidents with injury are reported at the city intersections \[2\]. 

cars. In 2015, this number grew to 335 million commercial Besides, statistics in Europe and the United States show that vehicles and almost 950 million passenger cars \[1\] caus-over 40 percent of collisions take place at the intersections \[3\]. 

ing traffic congestion. IM appears to be one of the most This makes safety as one of the hottest topics in the IM

demanding issues within the transport and road sectors that sector that requires great deal of attention. Traffic efficiency as the second major pillar of the intelligent transport sys-The associate editor coordinating the review of this manuscript and tems \(ITS\) is intertwined with traffic safety and must be approving it for publication was Jie Gao

. 

jointly considered in many traffic situations. For example, This work is licensed under a Creative Commons Attribution 4.0 License. For more information, see https://creativecommons.org/licenses/by/4.0/

VOLUME 10, 2022

7937



A. Gholamhosseinian, J. Seitz: Comprehensive Survey on Cooperative IM for Heterogeneous CVs severe collisions with fatalities in low congested traffic are of a BSS \(basic service set\) known as \(OCB\) mode of more probable due to head-on collisions or in presence of IEEE 802.11. In addition, 802.11p forms the physical and VRUs. On the other hand, in congested situations, the likeli-MAC layer of DSRC \[9\] and ITS-G5 \[7\]. On the other hood of less serious crashes is higher. Traffic delay is another hand, standards of the protocols in the upper layers are management concern that intersections are dealing with and distinct. Upper layers of DSRC are characterized by IEEE

incurs huge congestion costs. Intersections largely contribute WAVE standards \[10\]. DSRC IEEE 1609 defines a broad-to travel delays and crash numbers in urban environments \[4\]. 

cast protocol for routing namely Wave Short Message Pro-Besides, crashes and delays have a great impact on human tocol \(WSMP\) \[7\]. Besides, it uses Basic Safety Message time and energy wastage \[3\]. It has been demonstrated that \(BSM\) \[11\] and its format is defined by SAE J2735 \[12\]

human errors have a significant role in road accidents by standards. In terms of ITS-G5, for instance, it uses Geo-75 percent \[5\]. Vehicle’s throughput, speed, travel time, fuel networking for single and multi-hop ad-hoc communication. 

consumption and emissions are other important factors that ITS-G5 mainly specifies two types of safety messages called are highly affected by an IM mechanism. 

cooperative awareness message \(CAM\) and decentralized To control the intersection, the advent of traffic lights has environmental notification message \(DENM\). CAM is peri-remarkably helped to improve the traffic performance at inter-odic while DENM is event-triggered message that notifies sections. Nonetheless, traffic lights seem to be not so effective a hazardous situation \[7\]. Nonetheless, some CVs benefit for a high volume of traffic since they are not dynamically from the cellular-V2X \(C-V2X\) that provides quality of ser-adaptable to the real time vehicular traffic \[6\]. Recently, vice \(QoS\) and incorporates technologies such as 3rd gener-autonomous vehicles \(AVs\) have emerged and they are ation partnership project \(3GPP\) \[13\] or long term evolution rapidly under development due to the tremendous advance-

\(LTE\) \[14\]. V2V via cellular network is performed through ments in computer, communication and automotive technolo-a particular mode that supports direct communication like gies, whereby they can hugely amend this problem at the DSRC. DSRC and ITS-G5 are short-range communications intersections. Together with vehicles autonomy, the genesis which are fast, reliable in sparse area, with extensive hard-of vehicular communications has promised great potentials ware support that preserve user privacy. On the contrary, for promotion of the intersection performance. It is assumed C-V2X operates more dependable in dense areas, supports that cooperative coordination of the vehicles and infrastruc-long-range communication, and has hardware support con-tures using vehicular ad-hoc networks \(VANETs\) contributes straints. Moreover, it supports point to point communication to the optimized traffic in terms of safety, efficiency, infotain-in addition to broadcasting. Besides, communication capacity ment and environmental sustainability. Furthermore, vehicles in ITS-G5 and DSRC is limited due to the spectrum allocation and roads are endowed with advanced sensors that yield and high demands resource optimization. In addition to the abundant information of the surroundings. Such sensor-based DSRC and C-V2X, some researchers have opted for other information together with vehicle state information provide types of wireless communications such as Bluetooth or Wi-Fi deeper, real-time and global perception of the environment for VANETs. 

beyond the visual field using VANETs. These smart IM

Development of an effective intersection management sys-approaches can significantly diminish travel time, fuel con-tem requires consideration of all aspects. Researchers in sumption and emissions of the vehicles. Besides, they can

\[15\]–\[17\] have proposed diverse approaches to coordinate also increase the drivers’ awareness and throughput com-the CVs at the intersections. Over the past few years, some pared to the traditional traffic lights. Considering level of surveys have addressed IM in different ways. Rios-Torres autonomy of the road users as well as installed infrastruc-and Malikopoulos \[18\] focused on state of the art schedul-tures, intersections can be categorized into three groups, i.e., ing policy methods based on heuristics and optimization signalized, autonomous and hybrid. Signalized intersections for intersection crossing and highway on ramps merging. 

benefit from stop signs or traffic lights to control the vehicles They considered both centralized and distributed coordina-crossing while they can negotiate with the traffic lights for an tion techniques. Chen and Englund \[19\] surveyed cooperative optimized passage order. In case of autonomous intersections, IM mechanisms at the signalized and free signalized cross-connected autonomous vehicles \(CAVs\) or CVs make their roads from three perspectives; virtual traffic lights, trajectory decision to traverse the intersection through V2V or V2I planning \(TP\) and spatio-temporal \(ST\) resource reserva-communications. Lastly, hybrid intersections accommodate tion. Namazi *et al. *\[20\] also conducted a literature review human-operated vehicles and CVs. 

on the management of signalized and non-signalized inter-Two major standards exist for V2X communications, sections under vehicular environment in a systematic way. 

ITS-G5 standardized in Europe \[7\] and dedicated short range Moreover, Khayatian *et al. *\[21\] presented a survey on IM

communication \(DSRC\) \[8\] in US. V2X communications of CAVs from different aspects consisting of architecture, incorporate V2V and V2I as the principal variations. Euro-vehicle dynamics, wireless technologies, scheduling mech-pean and US standards convey some similarities. They both anisms, collision detection, human-operated vehicles, recov-operate at 5.9 GHz band as the spectrum is sub-divided ery, security, safety, robustness issues and simulation tools. 

in a few 10 MHz channels. Security and privacy mecha-Krishnan *et al. *\[22\] performed a partial non technical study nisms are identical and they both operates outside the context on IM while Guo *et al. *\[23\] addressed solutions for traffic 7938

VOLUME 10, 2022



A. Gholamhosseinian, J. Seitz: Comprehensive Survey on Cooperative IM for Heterogeneous CVs flow estimation and optimizing traffic signal timings based analysis on IM solutions. Finally, the last section concludes on CAVs at the urban signalized intersections. Furthermore, the work. 

Zhong *et al. *\[24\] surveyed AIM with the focus on three hierarchical layers namely corridor coordination, IM and vehicle **II. INTERSECTION MANAGEMENT \(IM\) FUNDAMENTALS**

control. Other IM design concepts such as computation con-A. ARCHITECTURE ALTERNATIVES

volution, centralization, collision detection strategies, prior-Traffic coordination methodologies of the intersection is ity policies, and also roadmap from signalized IM to AIM

mainly categorized into two groups of V2I and V2V. V2I is were also discussed. In another work, Malik *et al. *\[25\] stud-the centralized approach and takes advantage of infrastruc-ied the recent articles in cooperative driving, related taxon-ture/intersection manager for traffic control while V2V is dis-omy, platooning and especially various issues that exist in the tributed and vehicles undertake coordination by exchanging leader election of vehicles platooning. Here, authors briefly information between each other and making decisions locally. 

addressed intersection management solutions as one of the Occasionally, in a hybrid methodology no infrastructure is collaborative driving applications and presented the relevant involved though a vehicle temporarily takes charge of the approaches. 

intersection coordination. 

In this paper, we explore the state-of-the-art cooperative intersection management approaches for heterogeneous 1\) DISTRIBUTED: VEHICLE-TO-VEHICLE

vehicles from different aspects in the last two decades. We COMMUNICATION \(V2V\)

analyzed more than 1,200 relevant publications including This approach is more suitable for non congested intersec-surveys, reviews and short articles involving heterogeneous tions like those in rural areas. Comparatively, distributed CAVs or CVs roaming roads and rails at various kinds of approaches can provide more reliability and resiliency. They intersections. Consequently, our research resulted in approx-are more scalable due to their independence from the road-imately 379 papers such that to the authors’ knowledge, this side unit \(RSU\) support. Besides, in the distributed control, study is the first that takes into account main aspects of computation is spread across the vehicles and TP and resource intersection management for heterogeneous vehicles at the reservation are performed locally in the vehicles. This leads signalized, non-signalized and hybrid intersections. We spec-to more robustness where a vehicle failure does not inevitably ified a goal-based classification of the literature and presented result in system breakdown. On the downside, high commu-a systematic evaluation of the approaches at the end. Addi-nication bandwidth is required due to drastic communications tionally, numerous challenges for a robust and resilient IM are among vehicles to make a common decision. 

discussed to enlighten the future directions for further studies in this field. 

This paper is organized as follows. Section II intro-2\) CENTRALIZED: VEHICLE-TO-INFRASTRUCTURE

duces the fundamentals of the intersection management COMMUNICATION \(V2I\)

in terms of a centralized and distributed architecture, dif-A centralized approach empowers more control and manage-ferent scheduling policies such as first come first serve ment over the vehicles as computations consisting TP and \(FCFS\), optimization and heuristic-based algorithms, inter-resource grant are conducted inside the RSU. Besides, they section modeling methods containing ST reservation and can also handle high computation loads and less network TP, and intersection goals namely; safety, efficiency, pas-overhead is assumed for this solution as the infrastructure senger infotainment and environment. Next, intersections are can maintain the traffic information. Therefore, vehicles need categorized into three groups namely; 1\) signalized inter-not periodically broadcast their status. As the pitfall, the sections 2\) semi-autonomous intersections 3\) autonomous deployment of RSUs is costly and these are not as reliable intersections. Sections III, IV and V address these types of as in distributed control due to the single point of failure. 

intersections consecutively where all the IM methods are Therefore, mechanisms are required to ensure system robust-introduced and compared. The following section deals with ness. V2I approaches are classified into two groups. In the IM literature for VRUs. Several communication types based first method, the RSU assigns a cross-time to the vehicles to on centralized and distributed architectures are involved to follow based on the received status information from them interconnect VRUs. Section VII deals with diverse chal-which results in higher throughput. Adversely, in the second lenges that intersections encounters and greatly affect their one, the vehicle proposes a safe cross speed/time by sending performance. These concerns span a wide range of items a query to the RSU and receives either approval or rejection comprising sensors, information management and sharing, for this request. This method requires more processing time planning universal scheme, heterogeneous collaboration, compared to the other approach due to its interface nature. 

vehicle classification, quality measurement, external fac-Additionally, the packet size of the exchanged information tors, intersection types, localization, faults, communication has an impact on the network overhead. 

anomalies and channel optimization, synchronization, vehicle dynamics and model mismatch, model uncertainties, B. SCHEDULING POLICY

recovery, and security and privacy. Section VIII summarizes Basically, in topology design of the intersection, a stan-the discussion, visualizes the results and conducts a deeper dard traffic coordination algorithms should be applicable to VOLUME 10, 2022

7939



A. Gholamhosseinian, J. Seitz: Comprehensive Survey on Cooperative IM for Heterogeneous CVs diverse kinds of intersections. Therefore, it should take into The main purpose of the optimization-based method is to account some other factors such as lane numbers, width, and reduce the mean travel time of the entire intersection as turn allowance or u-turn permissions. Several methods such opposed to FCFS policy. However, some approaches have as mathematical optimization, multi-agent systems \(MAS\), followed some other auxiliary optimization goals such as pas-heuristic, linear and dynamic programming cooperate in the senger infotainment, fuel consumption, communication effi-intersection management. Besides, apart from time and space, ciency, acceleration/deceleration, or velocity. The sequence some other variables contribute to the intersection safety such of vehicles approaching does not necessarily correspond to as braking, speed, headway, acceleration/deceleration, throt-the their crossing order. Numerous papers have studied and tling, maneuvering that are to be considered. Furthermore, applied the optimization-based methods as scheduling pol-sound algorithm design for an intersection management icy at non-signalized intersections to enhance the through-should make use of an adaptive and flexible vehicle model put \[17\], \[26\]–\[30\]. Efficient scheduling policies that have where variables are defined in execution time. Moreover, little waiting and processing times are still open to research. 

safety margin size and model inaccuracy are directly related. 

Vehicles enter the intersection and avoid collisions based on C. INTERSECTION MODELING

some coordination rules such as arrival time, scheduling pol-In the literature, researchers have addressed the modeling of icy and priorities that are defined in the algorithms. Besides, the intersections from two perspectives that can be helpful for algorithms should be fast and reliable to cope with high traffic collision detection as shown in Fig. 1 and Fig. 2. 

mobility. On the other hand, processing time to determine the collisions and schedule safe crossing at the intersection 1\) SPATIO-TEMPORAL \(ST\) RESERVATION

is of high importance particularly in case of an optimization-Space-time occupancy is a type of cooperative resource based approach. Bigger processing time leads to larger safety reservation that deals with intersection resource scheduling margin around vehicles which is not satisfactory. In addition, regarding time slots and space tiles. Here, intersection is dis-there is an uniform relationship between the processing time cretized into a grid of cells such that the route of each vehicle and size of the intersection. If processing time rises, inter-features a list of grid cells that it occupies at each timestamp section size escalates accordingly because vehicles need to along its path through the intersection. When the intersection initiate communication much farther than before in order to is modeled with cells, vehicles should reserve cells along get the timely reservations. As an alternative, we can also their path for a specific time period and pass the intersection apply upper bound on the processing time of scheduling. 

according to their reservation. This method is collision free Scheduling defines the crossing sequence of the vehicles and can be deployed in a centralized or distributed fashion and through the intersection. Scheduling policy as one of the most merged with optimization techniques to increase throughput important factors of intersection management has a great or other metrics. Basically, FCFS is the dominant algorithm impact on vehicles throughput. Additionally, when it comes in the centralized version. ST resource reservation is carried to selecting the right scheduling policy, we need to consider out via either vehicle agent or infrastructure. The aim of fairness and communication overhead in order to avoid long this approach is to prevent vehicles to be in a common cell waiting times and secure efficiency. Here, we exploit differ-simultaneously. Depending on the intensity of the cases, the ent algorithms that are classified into three classes namely granularity of grid partitioning changes. For example, the optimization-based, heuristic and FCFS for resource reser-entire intersection area can be a collision area or smaller vations and TP in order to secure traffic properties such tiles can model the intersection in more details which leads as safety, infotainment, ecology and efficiency. The FCFS

to higher algorithm complexity. Occupancy grid solution has scheduling mechanism operates as the name suggests. The less computational overhead compared to the other due to its first vehicle that arrives at the intersection is the first one that straightforward conflict areas checking until it is limited to a is processed. Several publications benefited from FCFS algo-few collision cells. 

rithm in their works. Among the scheduling policies, FCFS

algorithm satisfies fairness though its performance dramati-2\) TRAJECTORY PLANNING \(TP\)

cally deteriorates with respect to the intersection density as it In this approach, instead of using an occupancy grid for the scales. Heuristic approaches do not necessarily aim to provide intersection zone, vehicles follow pre-defined travel trajec-an optimal but to offer a fast solution. They seem to be capable tories while crossing the intersection resulting in the deter-of meeting a trade-off between the two essential elements mination of collision points. TP is divided into two groups, namely throughput and fairness. Besides, they can even reach namely safe pattern and priority-based. Typically, TP can higher throughput with a limited delay compared to FCFS. 

be combined with other safety parameters like accelera-Conversely, in optimization-based policies, the processing tion/deceleration and speed to maximize optimization and to seek the optimal scheduling is time-consuming though efficiency. 

they can provide better throughput comparatively. Furthermore, it might degrade when the intersection density expands. 

3\) INTERSECTION MANAGEMENT \(IM\) GOALS

On the other hand, analytical solutions can resolve this IM goals are classified into different classes including problem for heuristic and optimization-based approaches. 

safety, efficiency, environment and infotainment as illustrated 7940

VOLUME 10, 2022





A. Gholamhosseinian, J. Seitz: Comprehensive Survey on Cooperative IM for Heterogeneous CVs In these approaches, the infrastructure designates an optimal trajectory to the vehicles so that they catch the green light. Liu *et al. *\[34\] proposed a two speed optimization algorithm to minimize delay and travel time of the CVs. 

Fayazi *et al. *\[36\], \[37\] investigated the optimal scheduling arrivals of the CVs with Mixed Integer Linear Programming \(MILP\) and using an intersection controller. This helped to prevent collisions and minimizes travel time, fuel consumption and average number of stops at the intersection. 

In \[36\], they proposed a variant of the MILP controller introduced in \[37\] for mixed traffic flow management. Concerning delay, the proposed method had better performance than normal signalized intersections. Ashtiani *et al. *\[38\] followed the similar optimization-based approach as \[36\], \[37\] for a grid of intersections that resulted in positive influence on **FIGURE 1. **Grid representation of the intersection area. 

fuel consumption and mobility of the traffic. Furthermore, Chang and Park \[41\] availed an optimization-based system to control the traffic signals at the intersection. Here, in each lane, vehicles formed a group using V2V communication and estimated the traffic density \(queue length\) by a group leader that resulted in lower waiting time. Afterwards, an algorithm determined the signal cycle length and green light via V2I communication and the received information from the group leader. Xie and Wang \[42\] developed a smart decision assist system on-board of vehicles at a signalized intersections to guarantee safety and reduce unnecessary stops. The proposed system was supported by V2I communication and made use of a probabilistic sequential process for proper stop/go decisions that utilized the integrated information from the intersection and vehicles. 

Furthermore, Wang *et al. *\[43\] focused on infotainment, **FIGURE 2. **Trajectory representation of the intersection area. 

safety and efficiency and developed a V2I driving assistance system for the signalized intersection. The proposed system could provide advisory passing speed, warnings in terms in Fig. 3. Besides, some goals are categorized into several of traffic light violation and rear-end collision, and auto-sub-classes. In particular, the environment is divided into matic braking. Likewise, Meng and Cassandras \[39\] devel-fuel consumption and emission. Efficiency is decomposed of oped a system based on V2I that adapted the speed of the delay, throughput, congestion sub-goals while safety pertains AVs according to the information received from the traffic to collision avoidance. Based on the application, researchers light such that they could cross the signalized intersection have examined one or several goals in their studies on IM. 

non-stop. Their design also led to reduction in fuel consumption, travel time, and delay. With a similar approach, **III. SIGNALIZED INTERSECTIONS**

Zhao *et al. *\[44\] developed a cooperative optimal speed advi-Invention of traffic lights has definitively revolutionized sory system to spare fuel consumption at the signalized intersection safety and traffic flow. During the last decade, intersections. Wang *et al. *\[48\] studied a different method and quite a number of noticeable works have been conducted to devised a cluster-based cooperative application for CAVs. 

improve traffic lights functionality. They span a wide range In the proposed system, vehicles formed clusters in order of approaches such as mathematical models \[52\], max and to pass through the signalized intersection with less pol-back pressure \[53\]–\[55\], and agent-based learning methods lution, fuel consumption and better throughput. Moreover, 

\[31\]–\[33\]. Among the proposed solutions, vehicular wireless Saust *et al. *\[49\] deployed a cooperative V2I system to min-communication has exhibited superiority over the traditional imize delay, emissions and fuel consumption by regulating methods due to their wider detection area and more detailed traffic signal control as well as driving patterns of the vehi-conveyed information. Moreover, in V2X communications, cles. This approach optimized the longitudinal and lateral vehicles can collaborate for intersection coordination. 

movement strategies of the AVs using a max-min ant system Signal phase and timing \(SPaT\) control of the traffic lights at the signalized intersection. 

is recognized as the simplest optimization-based method and Shen *et al. *\[35\] made use of centralized MPC-based mech-can produce reasonable throughput \[34\], \[36\]–\[38\], \[56\]. 

anism and provided a platform for CAVs to approach the VOLUME 10, 2022

7941





A. Gholamhosseinian, J. Seitz: Comprehensive Survey on Cooperative IM for Heterogeneous CVs **FIGURE 3. **Intersection management goals. 

**TABLE 1. **Summary of literature reviews on signalized intersections. 

signalized intersection with a smooth speed. Gutesa and **IV. SEMI-AUTONOMOUS INTERSECTIONS \(Hybrid\)**

Besenski \[50\] developed a centralized IM mechanism for Intersections are still shared between autonomous connected CAVs based on trajectory planning at the signalized inter-and human-driven vehicles. Hence, there should be some section. A control algorithm allocated the optimal path con-control mechanisms such as traffic lights or on-board sen-sidering various inputs such as vehicle’s position, speed, sors for human-driven vehicles to control them. Recently, signalization status and current traffic at the intersection. 

hybrid intersections are absorbing more attention where they This approach resulted in lower delay, travel time and fuel incorporate human-driven and autonomous vehicles traffic. 

consumption of the vehicles. Zhu *et al. *\[40\] studied a safe This section deals with the articles that have addressed such eco-driving IM model for hybrid electric CAVs using a safe intersections and the proposed methodologies when two types novel off-policy-based reinforcement learning \(RL\) algo-of vehicles share the same intersection. 

rithm at the signalized intersection. The proposed model Pourmehrab *et al. *\[56\] studied joint SPaT and TP opti-was based on V2I communication and optimized the vehi-mization for human-driven vehicles and AVs respectively. 

cles trajectories such that fuel consumption and travel time The system showed better travel time compared to the con-were reduced significantly. The model improved the mean ventional methods. Qian *et al. *\[57\] presented a priority-based speed in comparison to the traditional vehicles. In addition, TP and integrated legacy vehicles that were controlled by some other researchers like Mandava *et al. *\[45\] along with traffic lights at a hybrid intersection. If a non-cooperative Kamalanathsharma and Rakha \[46\] employed V2I technol-vehicle and an autonomous vehicle approached the inter-ogy and focused on dynamic programming and optimiza-section from different roads, the manual one received the tion of individual vehicle velocity trajectory to pass through lower priority and could pass the intersection once the con-the intersection by saving fuel up to 12-14 and 30 percent nected vehicle has passed the conflict area. In case they were respectively. In another approach, Asadi and Vahidi \[51\] used on the same road, a virtual platoon was constructed where a centralized architecture and model predictive controller. 

an autonomous vehicle was followed by the legacy one to In this effort, they could reduce fuel consumption and CO2

cross the intersection. Verma and Vecchio \[59\] employed a emissions by 47 and 56 percent while considering travel semi-autonomous control system, a hybrid model in which time efficiency. Du and Pisu \[47\] deployed an energy effi-some vehicles were equipped with a cooperative active safety cient IM mechanism for CVs driving on two-lane road and system and others were human-based vehicles. Moreover, crossing multiple intersections. The MPC, speed control and Dresner and Stone \[15\] treated vehicles and intersections lane changing discretion were adopted to minimize the fuel as autonomous agents for autonomous intersection manage-consumption of the vehicles. A summary of literature reviews ment \(AIM\). A query-based reservation approach plus an on signalized intersections is presented in Table 1. 

FCFS policy were used to coordinate the autonomous CVs 7942

VOLUME 10, 2022



A. Gholamhosseinian, J. Seitz: Comprehensive Survey on Cooperative IM for Heterogeneous CVs through the intersection \(pass or stop\). They also integrated simple coordination protocols. Sayin *et al. *\[73\] exploited an human-driven vehicles in the system that followed the traffic information-centric V2I-based IM system which integrated lights rules. In terms of safety and delay, the proposed sys-useful information that can be provided exclusively by the tem outperformed traffic lights. Inspired by the AIM system driver and not the sensors. In this heuristic method, in the of this approach, Hausknecht *et al. *\[60\] managed a grid of vicinity of the intersection, drivers reported their utility func-connected intersections. They extended their work by inte-tions that they intend to maximize using an payment-based grating various navigation policies to dynamically change the incentive mechanism called Vickrey-Clarke-Groove. Then, planned vehicle route \(reversing lanes direction\) and decrease the roadside unit prioritized the intersection usage accord-its delay. In an analogous research, Sharon and Stone \[62\]

ingly and maximized the sum of all utility functions \(social modified the system with a distinction to \[15\]. In contrast welfare\) which was used to enhance the transportation qual-to FCFS reservation model proposed in \[15\], given that an ity. Ahn *et al. *\[69\] used a centralized intersection controller autonomous connected vehicle with a red light was present, namely supervisor that overrides the autonomous vehicles in the intersection manager did not revoke its reservation unless case of crash detection. The supervisor coordinated the traffic there was no other vehicle with a green light at the inter-with the help of an interior point and active set technique section. This method improved the performance of the interat the semi-autonomous intersection including one manual section for hybrid traffic. Another extension of \[15\] was and two autonomous vehicles. Additionally, Sinha *et al. *\[74\]

presented in \[63\], where different types of semi-autonomous introduced a new virtual traffic lights \(VTLs\) extension vehicles with features like cruise control received reser-model to enhance its functionality. It embodied VTL-enabled, vations similar to the CAVs. Shen *et al. *\[64\] deployed a ordinary vehicles and also an infrastructure to ensure FCFS-based centralized hybrid intersection system where safe, smoother traffic flow. Cheng *et al. *\[72\] employed an on-board units \(OBUs\) were proposed for non-autonomous approach based on heuristic RL to plan safe optimal trajec-vehicles to communicate with the controller using differ-tories of the CAVs and human-driven vehicles at the sig-ent signals like pass and stop. Further, Sharon *et al. *\[65\]

nalized intersection. Wang *et al. *\[58\] proposed a V2I-based designed a centralized hybrid intersection management pro-traffic control system for CVs and human-driven vehicles tocol that involved autonomous and manually operated vehi-at the hybrid intersection. This scheme could detour the cles. They used FCFS algorithm for CVs to traverse the CVs traffic with respect to congestion in the roads and out-intersection. 

performed traditional methods in terms of delay and travel In another research work, Li and Zhou \[61\] designed time. Fu *et al. *\[71\] developed a centralized multi-intersection a V2I-based optimization platform that improved intersec-coordination platform based on C-V2X communications and tion capacity, mobility and delay via dynamic signal tim-resource reservation for CAVs. The goal was to enhance fault ing policies. They used MILP, a search algorithm like tolerance and traffic efficiency over conventional systems. 

sequential branch-and-bound \(BB\) to find the optimal phases Besides, authors could also simulated remote driving with at hybrid intersections. Similarly, Lin *et al. *\[29\] developed lower delay. Table 2 summarizes the hybrid intersections a centralized intersection coordination method where the approaches. 

road segment was split into three virtual sections of core, buffer and free areas. CVs speed and time adjustments **V. AUTONOMOUS INTERSECTIONS**

were assigned based on the buffer allocation mechanism in Non-signalized intersections reside no traffic lights or any the buffer area. Then, they were allowed to pass the core other controller. Eye contact or hand signaling are the sim-area \(intersection area\) with the constant speed. Human-plest way of safe passage through such intersections. Intro-driven vehicles trespassed in the free area. This method duction of V2X communications paved the road for easier and was able to promote delay, mobility and fuel consumption more accurate vehicles interactions. Particularly in non light compared to the traffic light system. To deal with the of sight or obstructed situations, vehicles avoid collisions by mixed traffic, Onieva *et al. *\[67\], \[68\] proposed an efficient exchanging traffic information. In this regard, agent based multi-objective algorithm, a fuzzy rule-based system for methods are extensively used especially for the V2V archi-hybrid intersections involving manual and CAVs where the tecture. An agent is a computational autonomous unit that speed of the CAVs was controlled in order to avoid col-fulfills certain objectives in a certain ambiance \[75\]. An agent lisions with manually driven vehicles. Additionally, Fayazi can be a vehicle, a traffic light or an infrastructure that gathers and Vahidi \[70\] devised a vehicle-in-the-loop \(VIL\) simu-information to coordinate the vehicles passing. In this section, lation platform using bi-directional cellular communication AIM methods are discussed in details in different categories wherein the infrastructure received the vehicles’ information with respect to the goals they serve. 

and scheduled the optimal arrival time and speed based on the MILP algorithm. 

A. SAFETY

Likewise, Liu *et al. *\[66\] deployed a safe IM framework Traffic safety is known as the most remarkable application of for hybrid traffic. They used V2I communication and model wireless vehicular communication. In this context, we must predictive control \(MPC\) for permission assignments of AVs protect not only cars but also VRUs such as motorcycles whereas for human-driven vehicle, traffic lights operated with or cyclists. In accidents, pedestrians and cyclists as VRUs VOLUME 10, 2022

7943



A. Gholamhosseinian, J. Seitz: Comprehensive Survey on Cooperative IM for Heterogeneous CVs **TABLE 2. **Summary of literature reviews on semi-autonomous \(hybrid\) intersections. 

are more exposed to fatal and serious injuries. As an exam-map-free intersections. It took advantage of a triple kalman ple, 2.6 million pedestrians and cyclists were involved in filter that employed GPS and sensors data to estimate the 5.9 million crashes in the European Union in 2013 \[76\]. 

vehicle mobility state information. Collision avoidance was The accident rate of this group is growing with 75 people done based on the received information of each vehicle via casualties and 750 injuries every day on European roads \[77\]. 

DSRC. Gabarron *et al. *\[88\] planned vehicles trajectories in a Nowadays, safety related solutions to diminish the risk of way to become collision free while traveling at high speeds. 

accidents for VRUs are being neglected \[78\]. Publications To this end, they utilized multi-objective optimization based regarding VRUs with emphasise on wheel-based VRUs are on lateral motion of the vehicles. Chen *et al. *\[89\] examined summarized in section VI. To provide traffic safety, there is a the effect of different intersection collision warning systems demand for the vehicles to communicate traffic information. 

\(ICWSs\) \(audio and visual\) on intersection accidents. Their Road traffic safety applications lie in two categories; V2I system was based on DSRC and could reduce the drivers’

and V2V applications. V2I safety spans a wide range of reaction times as well as crashes by 40 to 50 percent. Addi-applications comprising red light violation and curve speed tionally, Lu *et al. *\[90\] utilized a V2V protocol that defined warning, stop sign gap assist, spot weather impact warning, the vehicles passing sequence based on the traffic rules at the reduced speed/work zone warning and pedestrian in signal-non-signalized intersection. Besides, an algorithm was used ized crosswalk warning \[79\]. V2V safety related applications to determine a safe deceleration value for yielding vehicles encompass intersection movement assist \(IMA\), left turn to avoid collisions. Belkhouche \[91\] employed a coopera-assist \(LTA\), blind spot/lane change warning \(BSW/LCW\), tive optimal approach for conflict resolution of autonomous do not pass warning \(DNPW\) and vehicle turning right in vehicles at an non-signalized intersection. Collisions were front of bus warning \[79\]. Forward collision warning \(FCW\), detected using speed ratios, then a fast algorithm was used emergency electronic brake lights \(EEBL\), traffic signal vio-to compute the optimal actions according to cost function lation \[80\], \[81\] or even VTLs \[82\], \[83\] are other examples which is formulated in terms of current speed deviations. 

of this kind of applications. Among them and especially in Riegger *et al. *\[92\] developed a V2I-based MPC method for an urban environment, intersection collision/assistance is of autonomous vehicles at the intersection zone. They availed great significance \[84\], \[85\]. It is due to the fact that the large convex optimization to formulate the problem to provide extent of accidents around 40 percent occurs near or at the optimal trajectories and avoid collisions. 

intersections \[86\]. 

Furthermore, Altchø *et al. *\[93\] employed a supervi-Researchers have proposed several approaches to ensure sor at the intersection that availed mixed-integer quadratic collision avoidance at the intersection. Today, VTLs can programming \(MIQP\) to manage and manipulate the con-replace physical ones as vehicular communications enable trol inputs of the semi-autonomous vehicles and safely vehicles to exchange traffic information. Ferreira *et al. *\[83\]

navigate them through the intersection. In another article, designed a system where a VTL protocol coordinated the Jiang *et al. *\[94\] presented a distributed optimization algo-traffic flow. In the proposed system, VTL leader was selected rithm which was a sort of augmented Lagrangian based using V2V communications to undertake traffic signaling alternating direction inexact Newton method \(ALADIN\) that and controlling the intersection. Once the light was green for coordinated the vehicles passing with the presumption that the VTL leader, it preferably handed over the responsibility the order of precedence was provided. Here, every vehicle to the new leader closest to the intersection. Besides, some executed locally the control problem and shared the depar-researchers established their safety methodologies based ture and arrival information with its neighbors to prevent on the prediction of risk, collision probability calculation collisions. Furthermore, Rahmati and Talebpour \[4\] investi-or movement-based techniques. Tu and Huang \[87\] intro-gated a decision-making platform based on the game the-duced ‘‘Forwards’’, a distributed collision warning system for ory for CAVs focusing on the left-turn maneuvers under 7944

VOLUME 10, 2022



A. Gholamhosseinian, J. Seitz: Comprehensive Survey on Cooperative IM for Heterogeneous CVs assumption of being unprotected. This study tried to charac-developed a V2V application that automatically controlled terize vehicles interactions and behaviors at the intersection the longitudinal movements of two vehicles at the intersec-and to estimate the real choice of the driver at the respective tions. Collision avoidance was based on the calculation of situation. Murgovski *et al. *\[95\] optimally modeled the safe a capture set which is a collection of all situations in which passing order of the AVs with a centralized control using the system is unable to prevent a collision \[109\]. Their sys-a Convex function. Malikopoulos and Zhao \[96\] exploited tem could prevent collisions under desirable communication an analytical rear-end collision avoidance system with appli-conditions. Lefèvre *et al. *\[110\] proposed the intention and cation of Euler-Lagrange equation for CAVs. Shi *et al. *\[97\]

expectation comparison for risk assessment at an intersec-benefited from the closed-loop optimal control mechanism tion. Moreover, Liebner *et al. *\[111\] evaluated collision risks for AVs to avoid rear-end collisions in each lane in addition using drivers’ intent inference at intersections while Oh and to the conflicts inside the intersection zone. Moreover, Yu and Kim \[112\] used vehicle’s trajectory data for risk estimation of Petnga \[98\] introduced a multi-agent V2V-based scheme for the rear-end collisions. Weidl *et al. *\[113\] utilized Bayesian AVs to predict and avoid different kinds of collisions using networks to predict collision risks at the intersections from machine learning techniques and two spatio-temporal algo-data comprising vehicle self-awareness and localization, and rithms. Nekoui *et al. *\[99\] developed a warning system based infrastructure sensors. 

on V2I to avoid collisions at the intersections. Red light vio-In another approach, Goldhammer *et al. *\[114\] installed lation for an approaching vehicle was calculated depending diverse types of sensor networks including signal phase tap-on the position, speed and time to the intersection. In case ping, cameras, laser scanners, and also a V2I unit at an of a high crash probability, the driver and other vehicles were intersection. Collision avoidance was achieved via cooper-warned. Fu *et al. *\[100\] analyzed an algorithm that considered ation and calibrated alignment of these sensors. In \[115\], the vehicles’ state data to detect hazardous situations and researchers employed an efficient frontal crash detection warn the drivers using V2V and dynamic Bayesian networks and avoidance system. Here, the authors designed a proba-

\(DBNs\). In addition, Joerer *et al. *\[101\] assessed the drivers’s bilistic algorithm and a decision-making protocol to predict safety at an intersection in a suburban area by measuring two trajectories, assess the threats and mitigate collisions based types of V2V beaconing warning messages namely simple on a Kalman filter by using Euclidean space. In another and one-hop relaying. They showed that one-hop relayed article \[116\], a V2V-based collision warning framework beaconing can significantly improve the driver’s safety at was proposed where future vehicles trajectories were pre-the intersection. In \[85\], they addressed vehicular communi-dicted using a Kalman filter to estimate the collision risk. 

cation aspects and studied two congestion control methods Wang *et al. *\[117\] implemented a spatio-temporal technique including Transmit Rate Control \(TRC\) and Dynamic Bea-to warn three types of drivers; negative, normal and positive of coning \(DynB\) in urban and rural intersections. Rate adaption potential accidents earlier, on-time or with delay respectively of these algorithms were in accordance to different situations with respect to the safe braking distance. A V2I-based colli-and aimed to meet the safety requirements of vehicular use sion detection algorithm at T-shaped junction was proposed cases. In their other work \[102\], they analyzed the intersection in \[118\] that benefited from Location Based Services \(LBS\) collision avoidance system for two approaching vehicles and that contains IMU and GPS technologies to collect vehi-derived the likelihood of collisions between the two with cle state information at T-shaped intersections. In another respect to their future trajectories. 

research \[119\], a V2V-based collision warning approach was There are some papers that reviewed the intersection col-studied where vehicles left-turn trajectories were predicted lision avoidance from a risk estimation perspective. In this at T-shaped junctions based on LBS and Kalman filter-regard, Baek *et al. *\[103\] proposed an approach composed of ing. Kwon *et al. *\[120\] implemented some collision predic-vehicular communication and multiple in-vehicle sensors to tion algorithms at the intersection where road sensors sent estimate the vehicles trajectories and warn the driver to avoid position and velocity of the approaching vehicles to the collision using Kalman filter. Raut and Bajaj \[104\] employed infrastructure via a sensor network. Then, the infrastructure a collision avoidance framework based on V2I and V2V to broadcast the state information to the other vehicles so that estimate the crash probability at the intersection. In \[105\]

they could locally calculate the collision probability accordan efficient algorithm based on V2I and V2V was presented ingly. Salim *et al. *\[121\] proposed a centralized approach and to assess the risk, warn the driver and mitigate collisions at a safe communication protocol where an infrastructure agent the intersection using Dynamic Bayesian Networks \(DBNs\) received status messages from the vehicle agents, learns, and state information of the vehicle. Xia *et al. *\[106\] proposed detects and warns the drivers of the collisions. 

V2V-based efficient warning algorithms for two collision Furthermore, a novel collision predication algorithm was scenarios, namely rear-end and intersection with respect to investigated in \[141\] using V2V and based on comparison the information captured from the vehicle state. Additionally, of dynamic thresholds for the minimal distance between authors in \[107\] focused on calculation of the collision proba-vehicles to warn the drivers with normal or emergency warn-bility of two vehicles’ trajectories at the intersection with the ings. Malinverno *et al. *\[132\] introduced an effective cellular help of their speed, position, motion capture device, intention vehicle-to-infrastructure \(C-V2I\) scheme for collision avoid-of the driver and V2V communication. Hafner *et al. *\[108\]

ance \(CA\)/collision warning \(CW\) for human-operated and VOLUME 10, 2022

7945



A. Gholamhosseinian, J. Seitz: Comprehensive Survey on Cooperative IM for Heterogeneous CVs **TABLE 3. **Summary of literature reviews on safe autonomous intersections. 

AVs at the intersection. Colombo and Wymeersch \[128\]

on the predicted trajectories of both trams and velocity and deployed a V2I-based CA system under contained composition were the parameters to find the crash prediction. 

munication conditions using a wireless network where the Authors in \[140\] proposed a positive train control \(PTC\)-

infrastructure could override the vehicles’ input if necessary. 

VANET integrated system to reduce conflicts at rail road Another CW solution based on V2V was introduced in \[126\]

intersection. Barkouk et el. \[138\] performed an overview on that relied on the computation of time and distance to the RCAS and also PTC systems for V2T and V2V applica-intersection. Basma *et al. *\[129\] exploited a V2I-based CA tions. Mäder *et al. *\[139\] exploited a train to infrastructure system where four wireless sensor networks \(WSNs\) installed \(T2I\)/V2I based smart and safe railway crossing. In this sys-on each road monitored the passing vehicles, transmit the tem, the approaching train/tram and the vehicles periodically information to the base station wirelessly. Then, if a consent mobility information to the cloud infrastructure. Then, flict was imminent, the base station would communicate the traffic controller computed collisions and estimated the with the warning system fixed at each intersection side via train arrival time and sent advisory speeds or stop com-wireless or wired connection to warn the drivers. Similarly, mands to the vehicles depending on the train distance to the authors in \[130\] presented an empirical novel centralized intersection and the vehicles’ positions. In \[133\], researchers CA system called iICAS that inherited the same concepts employed an audio visual CW framework for rail-highway with one distinction. In addition to issuing a public warning, crossing by using V2T and V2I communication. In case the system could directly warn the vehicle at risk. Miller a crash with the train was predicted, speed deceleration is and Huang \[122\] deployed a V2V-based CW test-bed with triggered for the vehicles to decrease the collision probability. 

customizable parameters such as communication range and Ghoul and Sayed \[131\] focused on a V2I-based trajectory latency, coefficient of friction, vehicle speed, driver reaction planning system and implemented the optimal speeds for time and position accuracy. In addition, Guzman *et al. *\[125\]

CVs using deep RL and a rule-based strategy to bring safe addressed a V2V-based intersection safety application via passage of the vehicles at the intersections. Table 3 shows the a test field where an emergency vehicle was prioritized to literature addressed the safe autonomous intersections. 

cross the intersection. Suzuki *et al. *\[124\] investigated the distributed CA/CW using Very High Frequency \(VHF\) in B. EFFICIENCY

Non-line of sight \(NLOS\) situations. Mobility information Many methods have been introduced by researchers for were periodically broadcast by vehicles and if a potential improvement of the intersection efficiency from different crash was detected, a warning message was sent out to aspects such as throughput, delay or congestion remedy as the vehicles at risk. In \[127\], authors mainly addressed the follows. 

accuracy enhancement through development of a cooperative Malikopoulos and Zhao \[142\] employed a decentralized vector-based CW solution considering curve and intersection optimal lane and order control framework for each CAV to scenarios. 

cross the intersections. Qiao *et al. *\[151\] developed a virtual Not many papers can be found that deal with trains or trams roundabout for the management of AVs at the intersection. 

collisions. Choi *et al. *\[134\]–\[136\] analyzed the direct and This system outperformed FCFS and traffic lights in prop-indirect vehicle-to-train \(V2T\) communication for collision erties like traffic congestion and safety distance. Vasirani avoidance at a railroad crossing between a train and a vehi-and Ossowski \[160\] studied a computational market strat-cle in rural and suburban areas from different perspectives. 

egy in which driver agents trade the capacity use of the Avoiding train to train collision using a rail collision avoid-intersection with IM agents. This showed a more efficient ance system \(RCAS\) was published in \[137\]. They inves-behavior compared to the popular traffic lights. In their fol-tigated the train to train \(T2T\) communication and RCAS

lowing research \[161\], they analyzed a double V2I-based for trams where it warned the driver if there was a potential scenario with the reservation control model proposed by \[15\]. 

collision with another tram. Collision was calculated based Firstly, they performed reservations on an auction-based 7946

VOLUME 10, 2022



A. Gholamhosseinian, J. Seitz: Comprehensive Survey on Cooperative IM for Heterogeneous CVs policy in a single intersection. Secondly, they suggested a efficiently than traffic lights and FCFS systems. Au and novel competitive market-based distributed approach for traf-Stone \[146\] proposed a motion planning heuristic approach to fic assignment for multiple intersections. In the latter, they minimize the stopping time of the vehicles at the intersection made use of bidding rules including travel time and price for and to increase throughput. The earliest arrival time was driver’s path selection such that drivers with higher travel scheduled by the infrastructure based on the highest vehi-time could send higher price bids thereby reducing their cle’s speed. This method outperformed the optimal heuristic delay. Finally, a combination of both strategies were pro-methodology in \[147\] in terms of throughput, mean delay, and posed that could drastically decrease the travel time. Further, efficiency. 

ShangGuan *et al. *\[162\] proposed a novel V2I-based optimal Furthermore, Au *et al. *\[167\] leveraged the liveness and control scheme based on time delay petri nets \(TdPN\). The deadlock free features into AIM by introducing a batch-based proposed method resulted in better performance compared to reservation policy. Perronnet *et al. *\[154\] exploited a hierar-the traditional signal phase systems for non-signalized inter-chical deadlock free architecture for a grid of intersections sections. Yan *et al. *\[163\] exploited a V2I-based approach to via three routing policies including congestion avoidance, attain an optimal passage sequence and minimize the crossing shortest path and reservation which depend on the context of times for the autonomous vehicles at isolated intersections the traffic. The system diminished delay and computational based on dynamic programming. In another approach \[172\], overhead. In another approach, Carlin *et al. *\[155\] utilized an the authors designed a genetic algorithm to find an optimal auction-based policy where the system collects all bids from crossing order for several adjacent intersections in collabo-total roads to coordinate the vehicles passing sequence at the ration with dynamic programming and heuristic small extra intersection. The system maintained fairness by keeping a time \(SET\). They showed the inferiority of conventional logical travel time for low-budgets vehicles. Wuthishuwong methods like fixed-cycle time and adaptive control in compar-and Traechtler \[156\] deployed a graph-based traffic coor-ison to the branch and bound, genetic, dynamic programming dination method in a network of autonomous intersections algorithms, and heuristic SET. 

to balance the traffic density and elevate the throughput Moreover, Wu *et al. *\[171\] developed different traffic using a consensus discrete time algorithm and Greenshield’s control mechanisms namely; V2V and V2I to navigate the model. Additionally, Guler *et al. *\[157\] developed a holistic vehicles as fast as possible through the non-signalized inter-approach to find the optimal sequence times of entry and section. The authors took advantage of the Timed Petri Net exit of the vehicles using an iterative algorithm that reduces Model and dynamic programming for the simulation and con-delay and number of stops. An extension of the work of cluded that a global approach is the most efficient solution. 

Guler *et al. *\[157\] was proposed by Yang *et al. *\[148\]. The To achieve the best passing order, Wu *et al. *\[164\] introduced authors utilized an algorithm for trajectory assignment to an innovative scheduling model based on dynamic program-three classes of vehicles including conventional, connected, ming. In their system, intersection and vehicles were consid-and automated vehicles based on the collected information ered as machine and jobs respectively and could efficiently from all vehicles in the range of the infrastructure. They used handle normal congested situations. The authors extended a branch and bound algorithm and a Kalman filter to discover their work in \[152\] where they introduced an Ant Colony the optimal path of the vehicles after the determination of System \(ACS\) to control the vehicles individually on the basis the coming/leaving times. A centralized routing mechanism of localization and vehicular communication technologies. 

using an iterative algorithm was employed in \[168\] to reduce Their system outperformed the traditional adaptive controller delay, travel time and increase the throughput for a grid of and traffic lights. Besides, their scheme could find the mini-intersections. Philippe *et al. *\[158\] introduced a ‘‘profitabil-mum travel time of the vehicles and evacuate their sequence ity collectives’’ algorithm based on game and optimization of arrivals for numerous lanes and vehicles in an optimized theories using multi-agents to distributively coordinate the manner. Further, Zhang *et al. *\[165\] utilized a V2I priority-CVs at the intersection with a high level of performance. 

based reservation scheduling mechanism named PriorFIFO

Ameddah *et al. *\[143\] presented a V2V-based mechanism to for traversing of autonomous CVs. In a later research \[166\], manage the vehicles crossing based on their priorities in the authors inherited the concepts of the previous work and addition to other parameters such as density, distance of the adopted a cooperative V2I service-oriented ST reservation vehicle to the intersection and direction. The proposed system scheme for vehicles passing called csPriorFIFO. Here, all enhanced travel time and throughput. 

traffic participants, objects and the intersection environment In addition, Li and Liu \[173\] created a heuristic IM scheme were modeled to ensure the QoS of the highest priority vehi-for AVs under a V2I environment where a dynamic state cles. Wei *et al. *\[153\] employed a reservation-oriented con-list and a lane collision matrix were employed to deter-trol scheme named Batch-Light. A conflict matrix decision mine the real-time lane occupancy and passing order of the greedy algorithm was proposed to provide more reserva-vehicles. The proposed system outperformed adaptive and tions with specific fairness. Besides, the k-Shift optimiza-static traffic light methodologies with less computational tion algorithm was used to increase the possibility of more overhead and could enormously increase fairness and dimin-unlucky vehicles traversal through the intersection via decel-ish average delay. Rapelli *et al. *\[174\] developed a distributed eration or acceleration. The proposed system performed more heuristic-based virtual traffic light mechanism to coordinate VOLUME 10, 2022

7947



A. Gholamhosseinian, J. Seitz: Comprehensive Survey on Cooperative IM for Heterogeneous CVs **TABLE 4. **Summary of literature reviews on efficient autonomous intersections. 

the vehicles at the intersection. This solution could mini-method. They adopted the vehicles’ priority to build a graph mize the evacuation time, emissions and smooth the traffic containing the passing order of the robots and later they flow. In \[149\], a centralized intelligent traffic light solu-opted for a heuristic algorithm to plan relatively optimal and tion was devised over a content-based architecture called deadlock-free paths based on the priority graph leading to named data networking \(NDN\) to coordinate the vehicles lower trip time and safe traversal of the vehicles. Further, and reduce congestion and waiting time at the intersection. 

in \[175\] they addressed priority based robot motion planning Further, Chou *et al. *\[159\] proposed a strategy such that the at a controlled intersection. In the proposed system, a control VTL cycle was adapted according to the vehicle type and law included the proprieties and managed the robots within traffic density using V2V communication. The proposed the intersection to avoid collisions. Ghaffarian *et al. *\[176\]

approach increased the speed and throughput of the inter-introduced a V2I-based traffic controller that utilized inte-section. Authors in \[144\] suggested a V2V-based scheme ger linear program \(ILP\) to calculate optimal and safe where the traffic light listens to the information exchanged passing orders of the vehicles trajectories while ensuring between vehicles and adapts its timing based on the traffic maximal throughput. Researchers in \[177\]–\[179\] studied congestion near the intersection. In a different approach, sequence-based protocols for safe TP in cooperative real Zhu *et al. *\[169\] employed a centralized reservation-based IM

intersection. Vehicles negotiated the right of way individually system and designed a novel strategy to assign passing per-with the controller with regard to a passing sequence to mission to the vehicles with minimal delay called Look-ahead increase the throughput. In an different approach, Lee and Intersection Control Policy \(LICP\). The results demonstrated Park \[17\] utilized a cooperative V2I control system wherein its superiority over FCFS. In addition, a novel V2V-based an optimization algorithm \(nonlinear constrained\) could alter IM algorithm was presented in \[145\] where the problem was each autonomous vehicle’s maneuver to avoid collisions by modeled as a new version of mutual exclusion and was more removing conflicting trajectory overlaps at the intersection. 

efficient than adaptive traffic lights. Li *et al. *\[170\] made use Azimi *et al. *\[180\] exploited a family of V2V-based IM proto-of a sustainable time-space reservation-based IM solution in cols. They also provided an efficient collision detection algo-terms of emissions, fuel consumption and number of stops to rithm to prevent accidents at the intersections. The system coordinate the passing order of AVs at the intersection using was based on V2V communication and time-space resource V2I communication. Wu *et al. *\[150\] employed a congestion reservation. In another research \[181\], they developed two free traffic signal control scheme for CAVs where traffic was safe deadlock-free novel IM protocols based on distributed dynamically controlled using multi-agent RL in a grid of six ST method. They added parallelism and accurate vehicle intersections. In the proposed system, communication was models to maximize the vehicles progression and concurrent handled between traffic lights and vehicles. Table 4 presents crossing inside the intersection, decrease delay and improve the articles for the efficient autonomous intersections. 

throughput. In a later work \[182\], they adopted the similar approach by applying their protocols in the previous work C. SAFETY AND EFFICIENCY

in \[181\] for autonomous roundabouts by introducing a new To achieve a trade-off between safety and efficiency boosts collision detection algorithm. Authors in \[183\] studied an the usability of existing IM methods. This section introduces additional protocol that was analogous to one of the presented the literature that addressed these goals. 

protocols in their former works \[181\], \[182\] in terms of paral-Vehicle crossing scheduling can take advantage of robot lel progression. But the advantage was that the lower-priority motion planning methods such as path-velocity decompo-vehicle was allowed to first pass the intersection if its arrival sition for multi-robots environment. Firstly, this method time to the common collision area was shorter than the vehicle identifies and fixes the Communication Anomalies and with the higher priority. 

Channel Optimization path of each robot. Afterwards, veloc-Furthermore, Fok *et al. *\[184\] developed a safe cyber phys-ity adaptation is applied via input controls so that they tra-ical test-bed that consisted of several robotic mini vehicles verse the intersection safely. Gregoire *et al. *\[27\] advocated that all were equipped with sensors and could communicate a mathematical model based on the previously mentioned using 802.11g Wi-Fi technology. The aim was to evaluate 7948

VOLUME 10, 2022



A. Gholamhosseinian, J. Seitz: Comprehensive Survey on Cooperative IM for Heterogeneous CVs and compare six ST-based V2V and V2I policies with the proposed a slot-based intersection framework. Having existing intersection management rules such as stop signs received the requests, the BATCH algorithm heuristically and traditional traffic signals. The simulation results demon-re-ordered the vehicle’s arrival at the interaction after a period strated less travel time and delay compared to the state of of time instead of immediate assignment of the velocity to the art techniques. Quinlan *et al. *\[185\] implemented a mixed them in order to achieve safe and more efficient schedul-intersection testbed where a bunch of virtual vehicles in ing output. Furthermore, in \[198\] a heuristic approach was the simulation interacted with a real autonomous vehicle presented introducing a singular entrance scheduling scheme at an real intersection based on a centralized ST reserva-based on the reservation at intersections. To find the optimal tion approach using FCFS. Simulation results showed that sequence of vehicles arrival, a genetic algorithm was used vehicles traversed the autonomous intersection safely with and also vehicles were allowed to approach the intersec-better throughput compared to the conventional methods. 

tion with the desired speed. Besides, a red-black tree was Ahmane *et al. *\[186\] modeled ST resource reservation via created to store and manage the reservations. Elhadef \[199\]

Petri Nets based control policies for intersection management employed an adaptive V2I-based system and took advantage using V2I. Approaching vehicles requested ST reservations of a locking technique where the algorithm allows a vehicle to and right of way order was granted based on the timed Petri pass the intersection when it locks its conflicting lanes. This Net for intersection crossing in a safe and efficient manner. 

mechanism could satisfy fairness, safety and liveness to the Additionally, in \[187\] a cooperative optimization algorithm vehicles. 

was used for an optimal safe crossing order of the vehicles In addition, Fajardo *et al. *\[200\] showed the superiority with minimal travel time. Kloock *et al. *\[188\] analyzed the of FCFS performance over traffic lights in terms of delay safe and efficient intersection management using distributed and safety via simulation. Researchers in \[201\]–\[203\] took model predictive control \(DMPC\) scheme. Vehicles followed advantage of multi-agent reservation schemes based on V2V

predefined routes and priorities were applied to them based communication to improve traffic congestion and delay while on their reaction times to stop before the intersection in case ensuring safety. Adams and Rutherford \[204\] exploited a they could not pass the intersection with the adjusted speed. 

cooperative variant of the centralized AIM problem pro-In \[189\], a ST-based TP system was developed to achieve posed in \[15\] to increase safety and reduce delay around safety and lower delay and intersection efficiency. They common locations \(way-points\). This multi-agent TP mecha-utilized priority-based and discrete forward-rolling optimal nism was more efficient that traffic light systems. Moreover, control \(DFROC\) algorithms to navigate the CVs through in \[205\], WIN-FIT, an innovative reservation policy was the intersection. The authors of \[190\] also studied the linear used in which autonomous vehicles built dynamic groups programming approach for CAVs and could solve the opti-and the winner was allowed to safely cross the intersection. 

mization with respect to the travel time by considering the Besides, specific vehicles in the other groups could pass traffic flows of each lane. 

through the intersection during the unused periods by the Besides, Timmerman and Boon \[191\] investigated dif-winner group. This solution could greatly lower the delay ferent platooning algorithms for vehicles that could mini-and improve the throughput. Aoki and Rajkumar \[206\], \[207\]

mize mean delay, provide fairness and safety. Guney and designed a configurable synchronous intersection protocol Raptis \[192\] harvested the optimal heuristic-based coor-

\(CSIP\). It was the resilient and robust version of the Ball-dination solution for AVs using an particle swarm opti-room intersection protocol \(BRIP\). In contrary to BRIP, CSIP

mization \(PSO\) algorithm and FCFS policy to remove satisfied the safety concerns in terms of localization inac-collisions and diminish the delay at the intersection. Fur-curacies, control faults, and flexible inter-vehicle distances ther, Xu *et al. *\[193\] coordinated the safe passing order of the for each intersection depending on safety requirements. CSIP

CAVs based on some heuristic strategies as well as Monte resulted in no accident occurrence, maximizing throughput Carlo tree search \(MCTS\) where the leaf node yields the opti-and minimizing delay compared to traditional intersections. 

mal solution. Buckman *et al. *\[194\] made use of a heuristic Besides, Elhenaway *et al. *\[208\] adopted a game theory tech-centralized coordination based on the revised FCFS algorithm niques to find the best heuristic-based solution for navigation for navigating the vehicle through the intersection safely. 

of AVs with the minimal delay at collision free intersec-In this work, the agents’ order was swapped having a social tion. With a similar method, Zohdy and Rakha \[209\] intro-psychology metric that could reduce delay while improving duced a centralized heuristic approach for AVs that are the utility function of every vehicle agent. Stevanovic and armed with cooperative adaptive cruise control \(CACC\). The Mitrovic \[195\] deployed a heuristic-based system where authors benefited from game theory to minimize the over-neighboring lanes direction were altered thereby less con-all delay and collisions at the non-signalized intersection. 

flicts happened at the intersection using a reservation-Savic *et al. *\[210\] proposed a distributed V2V algorithm to based algorithm. Similarly based on a heuristic approach, prevent collisions and reduce delays. This approach was Belkhouche \[196\] addressed the optimal time and cost effi-resistant to communication-failures in a great extent and met cient conflict resolution of the vehicles with the help of safety and liveness requirements for AVs. 

Lagrangian function and safety margins through V2V comIn another research work, Abdelhameed *et al. *\[211\] stud-munication. With a different approach, Tachet *et al. *\[197\]

ied a hybrid fuzzy-genetic controller to manage the vehicles’

VOLUME 10, 2022

7949



A. Gholamhosseinian, J. Seitz: Comprehensive Survey on Cooperative IM for Heterogeneous CVs flow at the intersections. The system comprised an inter-the intersection. Aloufi and Chatterjee \[224\] presented a section manager and vehicle agents for vehicles coordina-system that scheduled the AVs crossing based on production tion and control and could enhance throughput, mean and line technique. The proposed system eliminated conflicts peak delay, predicted collision avoidance and intersection and decreased waiting time. In addition, they utilized KNN

utilization. Moreover, a reservation method was employed to predict the vehicles that make right-turns. A heuristic in \[212\] for autonomous control of the emergency evac-ST approach was studied by Chouhan and Banda \[225\] to uation at the intersection. The proposed system was con-prevent collisions and to minimize delay at the intersection. 

flict free and improved speed, delay, travel time, and safety. 

The system outperformed FCFS, traffic lights, and also the Müller *et al. *\[213\] developed a centralized urban solution CIVIC algorithm \[17\] from the average delay perspective. 

that scheduled the safe and optimal arrival time of the AVs Moreover, Creemers *et al. *\[226\] optimized the passing order at the intersection by means of MILP and ensured minimum of the vehicles with the help of a centralized controller super-delay. Chai *et al. *\[214\] assigned slots to the approaching AVs vising the access of the vehicles to the interaction using beforehand to cross the intersection in an optimal manner MPC. With respect to the average delay and throughput, the with the least delay, collision free and nonstop. In a certain system was more effective than traditional traffic lights and distance from the intersection, IM calculated and sent out the FCFS. In \[227\], a distributed collision resolution strategy target state of every vehicle based on two novel algorithms. 

was utilized to navigate a group of CAVs safely through the One is called LOOSE which was used to improve safety, and intersection. In the proposed mechanism, optimization runs the other one is named COMPACT which aimed at efficiency locally on each vehicle such that vehicles estimate the desired enhancement. Additionally, Kamal *et al. *\[215\] presented a time and speed to traverse conflict zones along their path coordination framework for CAVs to safely and quickly based on the received information from other vehicles. Their cross the intersection using MPC. Likewise, Kim \[216\] made objective was to decrease delay and improve throughput of advantage of MPC for safe TP of the vehicles. Moreover, the traffic. 

they established some V2I and V2V coordination protocols Another work on MILP was performed by \[228\] to

for inter-vehicle safety, lane changing, and also intersection boost the crossing time and to ensure safe traffic flow passing. Similarly, Katriniok *et al. *\[217\] designed a system at the autonomous intersection. Simulation results demon-based on distributed MPC to manage the priority of the AVs strated that this approach is better than the coordination passage in a safe and efficient way at the non-signalized inter-algorithm based on discrete-time occupancy trajectory \[229\]

sections. Perronnet *et al. *\[178\] deployed a sequence-based and traffic lights in terms of throughput and delay. To sig-strategy for AVs that was resilient to communication latency nificantly increase the throughput together with safety and and could ensure safe crossing of the vehicles with minimum efficiency, Mo *et al. *\[230\] benefited from multi-agents delay. Lamouik *et al. *\[218\] employed a multi-agent coordi-RL to formulate vehicle scheduling. They introduced nation system using deep neural networks and reinforced V2V, collision set strategies, low-complexity algorithms learning \(RL\) in an autonomous environment. The proposed and handled the multiple-collision-set coordination. Further, system offered safe a rapid intersection passing. 

Steinmetz *et al. *\[231\] centrally harmonized the vehicles pas-In addition, De Campos *et al. *\[219\] focused on a decen-sage by a collision-aware resource allocation \(CARA\) mech-tralized coordination of the traffic for conflict resolution. 

anism that was self-triggered and considered communication Decisions were made using a combination of model-based constrains. A dynamic scheduling solution for AVs based heuristic and sequential optimal control. In another work, on queuing theory was used in \[232\]. Rate stability the-Ze-hua *et al. *\[220\] availed a discrete control method based on orem and low-complexity Lyapunov theorem-based algo-a hybrid automation model to increase the cooperation among rithms were used to obtain higher quality of service \(QoS\), AVs by altering their maximum and minimum velocities and delay, throughput, and road stability. In \[233\], a heuristic avoiding collisions. Furthermore, to elevate cooperation and approach based on various game theory techniques was uti-efficiency in particular zones, they presented market mecha-lized to improve throughput and avoid accidents. Addition-nisms. In a different approach, Zheng *et al. *\[221\] proposed ally, Cruz-Piris *et al. *\[234\] adopted a genetic algorithm to a delay-tolerant IM protocol in terms of communication. 

automatically optimize crossing of both manual and AVs. 

Besides, a framework was devised for safety, performance The authors made use of a cellular automation simulator to and liveliness analysis of the protocol and showed that the increase throughput. Likewise, Gonzalez *et al. *\[235\] used a system was collision free and decreased delay compared to cellular automaton model and suggested a fault-tolerant rule-the traffic lights. Gregoire and Frazzoli \[222\] employed an based distributed coordination system for AVs. The system efficient and safe hybrid V2I/V2V approach for AVs coordi-outperformed traffic lights from the throughput viewpoint. 

nation at the intersection. A centralized job scheduler planned An efficient V2I autonomous intersection scheduling proto-the crossing time for each vehicle with maximum speed col based on TP was developed in \[236\] to ensure safety with while a distributed controller guaranteed this time and con-minimum delay. In the proposed system, the infrastructure flict free passing of the vehicles. Besides, Zhang *et al. *\[223\]

collects vehicles’ information to plan collision free trajecto-designed and uniformly modeled centralized and decentral-ries and assign relative proprieties with the lowest delay using ized reservation-based mechanisms for AVs to safely cross a window searching algorithm. Then, vehicles individually 7950

VOLUME 10, 2022



A. Gholamhosseinian, J. Seitz: Comprehensive Survey on Cooperative IM for Heterogeneous CVs adapt their velocity using dynamic programming to cross the \(absolute value programming\) in addition to the time occu-intersection. 

pancy of the vehicles. The proposed method was applica-The authors in \[237\] availed a heuristic approach and ble with and without platoons and could reduce delay and modeled the order of the vehicles as multi-agent Markov increase throughput. Moreover, authors in \[248\] adopted decision processes \(MAMDPs\) via RL at autonomous intera framework based on discrete-time occupancy trajec-sections. They particularly used a decentralized coordina-tory \(DTOT\) where the intersection assigned modified tion multi-agent learning approach to mitigate collisions and DTOTs \(time slots\) to the formerly built queue of vehi-reduce delay. Further, Mirheli *et al. *\[238\] developed a dis-cles whose proposed DTOTs collide with each other. The tributed coordination scheme to ensure that CAVs trajectories described system performed based on the FCFS strategy in have no near crash situations. They used mixed-integer non-order to safely steer them through the intersection. A safe linear programs \(MINLPs\) for optimization. The proposed V2V interaction scheme was proposed in \[249\] to smoothly approach was efficient in terms of travel time and throughput. 

navigate the vehicles by means of speed adjustment with Wuthishuwong and Traechtler \[239\] designed an V2I based respect to the leading vehicle. 

intersection scheduling method using discrete mathematics Additionally, Englund *et al. *\[250\] deployed an intersec-for modeling the passing sequence and trajectory calculation cooperative speed limit advisory application based on tion via dynamic programming. The system had less waiting V2I and wave control mechanism. In this approach, already time than traffic lights. He *et al. *\[240\] used an efficient and speed-harmonized grouped vehicles on the same road orga-collision-free solution that coordinated the approaching AVs nized groups with other vehicles on other roads such that from all directions in such way that they were allowed to their arrival time were managed, traffic flow was coordinated travel on any entering lane and land on any exiting lane and collisions were avoided. Bian *et al. *\[251\] exploited a dis-of the intersection. Here, travel time and throughput were tributed IM mechanism by employing two offline and online lower than traditional traffic lights. A scheduling mechanism algorithms to model the intersection with virtual belts and to resolve conflicts and maximize throughput for AVs was apply them in a real-time manner for safe and efficient vehi-employed in \[241\]. Platooning and individual-based vehicle cles TP through the intersection. In \[261\], an efficient rule-arrival models were developed utilizing a heuristic algo-based application was deployed using V2V to avoid collisions rithm which aimed to optimally schedule the arrival time based on distance, time to intersection indices, road and vehi-of every vehicle. The proposed solution outperformed traf-cle priorities. Basjaruddin *et al. *\[262\] utilized a multi-agent fic lights. Furthermore, Aoki and Rajkumar \[242\] devised a cooperative V2V scheme to ensure safety and alleviate heuristic-based system where self-driving AVs could safely travel time at the intersection. Moreover, Elleuch *et al. *\[263\]

cross the dynamic intersection that are not shown in a map investigated a cooperative collision avoidance system using using sensors and V2V communication. They introduced a real-time databases and V2V communication to reduce com-cyber traffic light that acted as an intersection coordina-putation time and ensure safety. Each vehicle’s database tor in congested periods and increased traffic throughput. 

preserved the local and surrounding vehicles information, Katriniok *et al. *\[243\] introduced a distributed MPC system and as the vehicle approached the intersection, it referred that could designate speed advice to the vehicles and safely to its database and selected the objective vehicles to run schedule the vehicle passage through the non-signalized the system. Safe and efficient IM scheme based on VAIMA intersection. This method optimized the traffic flow and was introduced in \[264\], an algorithm that provided fairness they also accounted for the driver reactions in terms of and improved passage time, traffic capacity by consider-uncertainties. 

ing driver intention and V2V communication. Molinari and In \[244\], the authors studied a V2V TP based regime Raisch and Raisch \[265\] devised a V2V-based IM solution where each vehicle solved a non-linear MPC using the prox-where safe and optimal vehicles trajectories and also crossing imal averaged Newton method for optimal control \(PANOC\) sequences were computed and determined using MPC and and sent its planned path to other vehicles. Feng *et al. *\[245\]

vehicles dynamics respectively. With a heterogeneous solu-employed a joint optimal control on both signal and trajectory tion in \[266\], authors utilized a CA clustering platform using using dynamic programming and control theory respectively Wi-Fi and LTE channels. Wi-Fi was utilized for communica-with a goal to optimize fuel and travel time. In addition, tion inside the clusters while LTE was used for transmission Azimi *et al. *\[246\] introduced the ballroom intersection pro-of safety messages among clusters. The system was efficient tocol \(BRIP\) for intersection management. They used a in terms of reception rate and delay. 

ST method and aimed to maximize the concurrent passage Furthermore, Anadu *et al. *\[257\] developed a collision of vehicles through the intersection. The proposed system detection and avoidance system using mini robots equipped was deadlock free and vehicles could pass the intersec-with sensors, micro controllers, V2I and V2V communication in a specific time with a constant velocity and non-tion at the intersection. Lu and Kim \[267\] proposed an IM

stop. Moreover, the method was V2X independent and could coordination genetic algorithm that optimized the vehicles increase the throughput. In \[247\], a V2X scheduling algo-passing order in a way that emergency vehicles traversed rithm for collision avoidance was used based on the mod-the intersection with the highest priority and with the lowest eling of autonomous intersection to the scheduling sections negative impact on travel time of the other vehicles. Road VOLUME 10, 2022

7951



A. Gholamhosseinian, J. Seitz: Comprehensive Survey on Cooperative IM for Heterogeneous CVs throughput and capacity paradigms as two efficient poli-Qian *et al. *\[254\] developed an IM technique based on two cies were presented in \[123\] for safe driving in different mixed-integer nonlinear programs where vehicle trajectories, environments including intersection for AVs. The proposed departure and signal times were centrally optimized so that approach benefited from V2V and in-vehicles sensors. With a safety was ensured and travel times were shortened for CAVs. 

different approach, Bazzi *et al. *\[268\] exploited a VTL-based In addition, Wu *et al. *\[273\] introduced a cooperative dis-approach using V2V where the first priority was allocated to tributed collision-free framework for CAVs by formulating the closest vehicle to the intersection which was then handed the scenario as a multi-agent RL problem. The proposed over to the next one. Abdelhameed *et al. *\[252\] benefited from method could manage dynamic quantity of vehicles to pass a centralized multi-agent IM solution for AVs suing Fuzzy through the intersection with efficient trip time. Ma and and proportional–integral–derivative \(PID\) controller. The Li \[255\] utilized a centralized AIM based on two different collision of trajectories was predicted via Euclidean distance reservation strategy for automated and CVs to minimize the between the two vehicles and the intersection utilization for travel time and avoid collisions. The proposed system used linear and especially fuzzy controller outperformed tradi-MILP for trajectory planning whereby instead of using pre-tional traffic lights in terms of delay and throughput. Further, determined arrival time and speed of the vehicles, they were in \[269\], the authors built a V2V heuristic scheduling algo-optimized dynamically along the path. This method was able rithm where the neighboring vehicles exchanged information to assign a new trajectory to the vehicles with new arrival and only the leading approaching vehicle cooperated with speed and time in case of sharp or sudden changes in the other leaders to safely traverse the intersection with minimal traffic condition at the intersection. Literature regarding the delay. Milanés *et al. *\[270\] made use of V2V and a Fuzzy safe and efficient autonomous intersections are provided in logic controller to acquire the position and speed of the vehi-Table 5. 

cles, predict the collision point at the intersection and adjust the speed of the vehicle without right of way to yield. Addi-D. EFFICIENCY AND ENVIRONMENT

tionally, a V2V-based heuristic algorithm including shuffled Some researchers have proposed various IM methods in order frog leaping and genetic algorithms was proposed in \[274\] to to achieve the goals environmental benefits and efficiency. 

plan the AVs trajectories such that safe and fast mobility was Jin *et al. *\[275\] used a V2I approach that slightly varied guaranteed. Ferreira and D’Orey \[271\] investigated the good from \[284\] with an optimal scheduling policy. The authors performance of VTL in terms of emissions and speed based optimized the leaving times of the vehicle agents using linear on V2V communication. 

programming and big M method at the intersection. The Vieira *et al. *\[258\] presented an IM method through visible system aimed to reduce emissions, fuel and travel time. 

light communication \(VLC\) under vehicular environment. 

In another heuristic-based research \[278\], they followed a In the proposed system, streetlights, traffic lights, RSU and similar approach as \[284\] without the concept of platoons. 

vehicles were interconnected using VLC. Relative speed They implemented a centralized solution based on the com-and distance were derived from the exchanged messages bination of priority, FCFS, and lane based polices where such that the RSU could optimally coordinate the safe vehi-vehicles with higher priorities were served earlier. Similarly, cles crossing with the minimal delay. Pei *et al. *\[259\] studied Xu *et al. *\[276\] proposed a V2I based system which con-cooperative multi-intersection management using V2I com-currently optimized the AVs’ arrival time and signal tim-munications and a distributed ST method to ensure traffic ing to reduce travel time and total fuel consumption at the efficiency and safety for CAVs at the intersections. Moreover, intersection. Furthermore, in another article, Tlig *et al. *\[279\]

Xu *et al. *\[260\] introduced a safe and efficient cooperative presented a multi-agent two-level decentralized scheme that multi-intersection scheduling scheme for CAVs. the proposed optimized the traffic flow speed at the network level so that system was based on multi-agents and V2I communications AVs were allowed to cross the intersection nonstop with and benefited from deep RL and fastest crossing time point minimum energy consumption. Mahbub *et al. *\[280\] devised algorithm \(FCTP\) to increase throughput and travel time of a decentralized energy-optimal framework for two adjoining the vehicles. Zhang *et al. *\[253\] utilized a safe V2I framework intersections using interior boundary conditions. They could based on CNN and a sequential based algorithm to coordinate provide safe efficient trajectories for the CAVs and dimin-the optimal crossing time and order of CAVs. The proposed ish the environmental impacts and travel time compared to model improved delay and speed in comparison to FCFS

signalized intersections. In \[281\], the authors tried to coor-policy and traffic lights. Further, Worrawichaipat *et al. *\[256\]

dinate the vehicles crossing based on optimism of the travel proposed a decentralized ST agent-based IM algorithm for time and fuel consumption using MILP. Additionally, Hafzu-CAVs that provided safe crossing of CAVs while the obstruc-lazwan \[282\] conducted the similar approach with the goal of tions are present at the intersection incurring low traffic reaching the optimized fuel consumption and acceleration or throughput. Their system behaved more efficient than FCFC

deceleration. In \[283\], an architecture was proposed where a and traffic lights methods. Regnath *et al. *\[272\] proposed a manager controlled all the traffic lights. In the coverage area reservation-based decentralized IM scheme that planned safe of the traffic lights, vehicles establish direct communication trajectories for CAVs and ensured better performance in terms via V2I communication by sending their requests. Otherwise, of delay compared to the traffic lights and priority roads. 

vehicles ad-hoc communication with the front vehicle that 7952

VOLUME 10, 2022



A. Gholamhosseinian, J. Seitz: Comprehensive Survey on Cooperative IM for Heterogeneous CVs **TABLE 5. **Summary of literature reviews on safe and efficient autonomous intersections. 

**TABLE 6. **Summary of literature reviews on ecological and efficient autonomous intersections. 

was linked to the traffic light were performed. Afterwards, optimally computed the vehicles trajectories and enabled requests were forwarded to the controller to find the optimal smooth flow of the traffic with high throughput, less delay and green light timing and reduce emissions. Zhao *et al. *\[277\]

fuel consumption. Furthermore, a V2V IM method for AVs presented an centralized optimal coordination framework for based on multi-agent was developed in \[294\]. A collision free CAVs in the roundabout. Performance of the system was sequence order of the vehicles was determined with respect to also investigated under mixed traffic in the roundabout. The their future paths. Besides, velocities were adjusted to ensure propose method significantly diminished trip time and energy safe passing in addition to less energy consumption and consumption for CAVs whereas under the hybrid traffic situa-delay. Tlig *et al. *\[295\] defined an agent at each intersection tion it was not so effective and stable in congested traffic con-to locally synchronize the arrival time and also the speed of ditions. Table 6 summarizes the articles regarding efficient the other AVs vehicles agents thereby they could safely cross and ecological autonomous intersection. 

the intersection without stopping and consume less energy. 

In another research work \[296\], a novel algorithm was pro-E. SAFETY, EFFICIENCY, AND ENVIRONMENT

posed that took control of the speed to safely and efficiently This section introduces works that focused on safety, effi-route AVs in the non-congested traffic. Mirheli *et al. *\[297\]

ciency and environment. To fulfill safety and optimize energy developed a control logic via dynamic programming and consumption, Makarem and Gillet \[285\] availed their modi-benefited from look-ahead mechanism based on a tree search fied version in \[286\] and investigated the intersection coor-algorithm to suggest near-optimal maneuvers for AVs. Com-dination via distributed navigation function method for AVs. 

pared to the signal control, the proposed method was able In this heuristic approach, heavier vehicles consuming more to maximize throughput, minimize travel time and fuel con-energy were prioritized to pass the intersection before oth-sumption, avoid collisions and smooth the traffic flow at the ers to ensure energy optimization. The systems were more intersection. 

energy efficient compared to the traffic light. With a similar Additionally, Malikopoulos *et al. *\[304\] investigated a dis-concept in \[287\], they added inertia and intention of the tributed optimal control scheme based on FCFS for CAVs vehicles to the shared information in order to alleviate the to minimize fuel, travel time, energy consumption while system performance from intersection capacity, fuel con-satisfying safety and maximizing throughput. The system sumption, average speed, and traffic smoothness perspec-behaved more efficiently compared to the signal control. 

tives. Kamal *et al. *\[288\] utilized a centralized approach based Jin *et al. *\[284\] employed V2I communication to form a on MPC to safely coordinate the AVs. The proposed system safe multi-agent intersection management framework where VOLUME 10, 2022

7953



A. Gholamhosseinian, J. Seitz: Comprehensive Survey on Cooperative IM for Heterogeneous CVs **TABLE 7. **Summary of literature reviews on safe, efficient and ecological autonomous intersections. 

passages of vehicles platoons were scheduled using FCFS

emissions, fuel consumption, travel time and speed. Fur-and suggested reservation time slots. Here, the traffic per-ther, Bento *et al. *\[307\] developed a global agent-based IM

formance indicated higher values compared to the traffic system supported by V2V and V2I using a ST reservation lights in terms of delay, travel time, fuel consumption, and scheme that aimed to decrease ecological impact, collisions, emissions. The proposed system exhibited robustness to and congestion. Here, they developed a traffic simulator to density. Besides, in comparison to the non-platooning sys-evaluate the reservation-based scheme for roundabouts and tem, the communication load significantly declined. Bashiri crossroads management. ST cell reservation was performed and Fleming \[305\] deployed the similar approach as \[284\], via an infrastructure agent to minimize conflicts, conges-a platooning-based mechanism for IM and and benefited from tion and environmental impacts. The introduced system also reservation and two policies based on classical stop-sign that supported V2V communication. A different centralized ST

outperformed it in terms of delay. In their latter work \[306\], approach of their work including a small number of legacy they made use of a greedy-based cost function and reservation vehicles not supporting V2X communication was introduced based policies to devise a centralized scheduling strategy for in \[309\]. Simulation showed good performance in terms of vehicles platoons to safely traverse the intersection with min-travel time, energy-saving, and flow rate. They could inte-imum delay and fuel consumption which was more effective grate all intersection types including roundabouts. Zohdy and than traffic lights. In a different approach, Medina *et al. *\[298\]

Rakha \[291\] utilized an optimization framework that evoked exploited a decentralized virtual platooning control mecha-the concept of cooperative adaptive cruise control where an nism. Here, vehicles in different lanes and future directions intersection manager assigns an optimal safe speed to the AVs cooperatively formed a platoon to safely cross the intersec-so that they can pass through the intersection having lower tion with high throughput and less fuel consumption. This delay and fuel consumption. 

method showed better performance than traditional traffic In addition, Zhang *et al. *\[300\] deployed an optimal decen-lights. Moreover, Bichiou and Rakha \[26\] presented an opti-tralized approach for CAVs crossing two neighbor inter-mization algorithm based on control theory to control CAVs. 

sections applying the Euler-Lagrange equation and optimal The proposed method considered weather conditions as well dynamic speed that yielded continuous traffic flown, colli-as vehicle dynamics and except for computational expenses, sion avoidance, and lower travel time and fuel consumption. 

it demonstrated better performance compared to the exist-Researchers in \[301\] conducted an analytical research on the ing conventional IM methods in terms of delay, emissions optimal control of the intersection using a similar approach. 

and fuel consumption. In another article, Philip *et al. *\[289\]

The authors of \[302\] availed three techniques \(Genetic studied a collaborative approach between RSU and AVs in Algorithm \(GA\), Active-set Method \(ASM\), and sequential terms of their lane speeds to elevate intersection efficiency quadratic programming \(SQP\)\) for optimal scheduling CVs and reduce fuel consumption. To this end and to reach a close-in a corridor of intersections. In the proposed system, delay, optimal result, a consensus-based algorithm with constant rear-end collisions, emissions and fuel consumption declined. 

step-size gradient was used. 

Zohdy *et al. *\[30\] launched an optimization tool to navigate Moreover in \[290\], a collaborative method was adopted AVs through the intersection. They used cooperative adaptive that optimized both CAVs speed and signal timing cruise control as TP method to prevent crashes and reduce simultaneously to achieve lower travel time and fuel con-delay and fuel consumption. Du *et al. *\[311\] focused on a summation. The authors of \[310\] relied on V2V commu-rule-based V2I-based IM framework using FCFS. Under low nication for their system. They considered the intersection traffic, cooperative speed synchronization was applied while as a conflict zone and allowed only one vehicle to pass the in congested times, virtual platooning was used to coordinate intersection at a time based on the shortest arrival time and the vehicles passage through the intersection. The system FCFS. Speed adjustment was performed for vehicles with was able to spare energy, increase the intersection capacity lower priority to reach the clear intersection. The proposed and decrease travel time in both cases. In addition, in \[292\], system outperformed FCFS and traffic lights in terms of an intersection coordination approach for AVs using MPC

7954

VOLUME 10, 2022



A. Gholamhosseinian, J. Seitz: Comprehensive Survey on Cooperative IM for Heterogeneous CVs and V2I communication was presented to plan safe trajec-TABLE 8. Summary of literature reviews on safe and efficient autonomous intersections with infotainment aspects. 

tories with high mobility and minimal energy and ecological impact. Munst *et al. *\[303\] benefited from a VTL framework based on a cloud manager and V2I communication where the vehicle state information were augmented by the cloud and suggestions were sent to the vehicles at the intersection. 

This work aimed to improve traffic flow, safety and fuel H. SAFETY, EFFICIENCY, ENVIRONMENT, AND

consumption. Huang *et al. *\[308\] implemented a reservation-INFOTAINMENT

based test-bed under V2I communication where priorities It is quite idealistic if IM can take into account all these were assigned based on vehicle classes in terms of unstop-objectives and generate a trade-off between them. To ensure pable, stopping and others. The system showed better per-safety and alleviate fuel consumption, travel time, traffic flow, formance in terms of delay, emission, and fuel consumption emission, and driver infotainment level, Ding *et al. *\[317\]

compared to conventional control methods. Chen *et al. *\[293\]

studied a safe centralized approach for IM for AVs by aimed to find an optimal speed of the CAVs to minimize transforming the problem to a nonlinear constrained pro-their fuel consumption and travel time by use of a safe cen-gramming. Cao *et al. *\[323\] implemented a multi-agents rout-tralized intersection coordination method. Safe, efficient and ing strategy in a semi-decentralized fashion using the ecological approaches applied at autonomous intersections route assignment problem solved by infrastructure agents. 

are shown in Table 7. 

In addition, Qian *et al. *\[319\] adopted a decentralized MPC

scheme using a priority-based scheduling scheme for AVs to smoothly and safely coordinate them through the interF. SAFETY, EFFICIENCY, AND INFOTAINMENT

section while minimizing pollution, mitigating gridlocks and In this section, we explore the literature that aimed saving energy. In \[320\], the proximity of the intersection to boost safety, passenger infotainment and efficiency. 

was analytically formulated as three zones and an optimiza-Krajewski *et al. *\[312\] investigated a decentralized graph-tion algorithm was performed based on Pontryagin’s mini-based

solution

for

vehicles

longitudinal

trajectories

mum principle \(PMP\) and the Euler-Lagrange equation to optimizations by usage of dynamic programming at inter-coordinate the CAVs at the intersection. The system fol-sections. The system outperformed manual vehicles and lowed multi-objectives including fuel reduction, driver info-non-cooperative AVs. To achieve the aforementioned three tainment, safety and efficiency. Furthermore, Azimi *et al. *\[3\]

goals, Dai *et al. *\[313\] implemented an automated opti-proposed V2V ST-based protocols to provide safety, infotainmal intersection control framework. An intersection con-ment, environmental sustainability, and boost the throughput trol model was transformed to the convex optimization at intersections and roundabouts using speed optimization of problem to schedule the smooth vehicle passage. Further, the vehicles. FCFS policy, road priorities, and vehicle identi-Mladenovi|c and Abbas \[314\] utilized a conflict free cooper-fication number \(VIN\) were applied for safe crossings of the ative self-organizing control scheme for AVs at the intersec-vehicles. The authors of \[321\] studied a greedy iterative algo-tions. The proposed method was based on the adjustment of rithm and a composite policy to organize multi-intersection the vehicle’s velocity trajectory and priority assignments that networks via trajectory optimization and route planning for provided less waiting time, delay, and travel time. In \[315\], CAVs. This framework ensured efficiency, safety, environ-they relied on a self-organizing priority-based agent-based ment sustainability and passenger infotainment. In \[322\], IM approach for AVs using V2V. Vehicles trajectories were a ST Fuzzy-based algorithm for roundabouts management planned according to the social priority and considering vehi-using V2V and V2I communication and connected and cles speed calculation. The system resulted in infotainment, non-CVs was proposed. The reservation was adaptive based safety, and efficiency. In addition, Wuthishuwong *et al. *\[316\]

on the vehicles speed and could reduce travel time, emis-established a V2I-based system that determined the safe time sions, congestion, energy and increase driving infotainment. 

and trajectories for AVs using discrete mathematics, dynamic Furthermore, Zhang *et al. *\[318\] adopted a novel V2I-based programming, and a node reservation algorithm at a one-AIM system for CAVs that planned safe and optimal tra-way intersection. Lower waiting time, smooth traffic flow, jectories of the vehicles considering factors such as travel and safe crossing were maintained in the system. Table 8

infotainment, fuel consumption, speed and acceleration. The describes the literature that cared for safe, efficient and proposed scheme took advantage of a priority-based mech-passenger infotainment at autonomous intersections. 

anism that improved the traffic efficiency and reduced the delays of emergency vehicles at the whole intersection zone. 

G. SAFETY, ENVIRONMENT, AND INFOTAINMENT

Literature concerned about autonomous intersections with In \[299\], the authors extended their decentralized control multi-objectives is presented in Table 9. 

framework from \[300\] by integrating left and right turns and took into account the passenger discomfort optimization in **VI. VULNERABLE ROAD USER \(VRU\)**

turnings in addition to ecological \(fuel consumption\) and Intersection users incorporate not only vehicles but also safety goals. 

VRUs such as bicycles, scooters and motorcycles. In spite VOLUME 10, 2022

7955



A. Gholamhosseinian, J. Seitz: Comprehensive Survey on Cooperative IM for Heterogeneous CVs **TABLE 9. **Summary of literature reviews on multi-objective autonomous through developing a toolbox consisting of socio-economic intersections. 

factors. Finally, XCYCLE \[330\] intended to enhance the cyclist detection in terms of active and passive, and warn the driver and cyclist of a danger at the intersections through effective mechanisms. 

Some papers have considered heterogeneous solutions as an alternative or addition to the pure classical 802.11p tech-of the significant importance of VRUs as one the most nology. In V-Alert \[334\], short-and long-range communica-paramount components of roads users, majority of the tion were combined giving more time to VRUs and drivers to researchers have focused on the intersection management take actions for collision avoidance especially at the intersec-solutions for vehicles and rarely investigated the VRUs safety tions. In their proposed system, on one hand, vehicles peri-in the traffic. In

the literature, researchers have reduced

odically sent position information to the RSU using 802.11p. 

the likelihood of crashes for VRUs at the intersections from Then, it relayed the information to a central server via LTE. 

various perspectives. Research on intersection management On the other hand, similarly, bicycles sent information to for VRUs has been limited mostly to safety concerns such the proxy bike through a WiFi network namely bike to as warning or detection. For example, the application of bike \(B2B\) communication so that it later would transmit different sensors is a traditional method that has been widely all the positions information via LTE to the central server used. However, sensors are not suitable for non-line of sight known as cellular-B2I or \(C-B2I\) communication. Therefore, situations and should integrate other technologies like DSRC

with the dissemination of the safety messages to the vehi-or LTE. Other emerging solutions such as wearable devices cles and bicycles group, imminent conflicts were prevented. 

and cellphones still need more research. Researchers in \[324\]

Besides, in the proposed scheme, pedestrians and motorcy-proposed a CA algorithm based on vehicle to bicycle \(V2B\) cles could be integrated. Thielen *et al. *\[78\] introduced a het-communication at an autonomous intersection. Additionally, erogeneous approach using an RSU to communicate between authors in \[325\] presented two cases for collision avoidance a cyclist and a vehicle. Cyclists sent safety messages to of bikes/pedestrians at the intersection; either WiFi com-the RSU through Wi-Fi. Afterwards, ITS-G5 was used to munication between bikes/pedestrians and infrastructure so relay the information to the vehicles in the vicinity. Further, called B2I/P2I whereby the RSU relayed the information via Anaya *et al. *\[335\] designed a system named ‘‘MotoWarn’’

DSRC/WAVE to the vehicles, or more efficient option which that targeted both cyclists and motorcycles. In regard to the involved direct communication using DSRC/WAVE between cyclist, it incorporated the iBeacon technology and Bluetooth the two target groups as vehicle to pedestrian \(V2P\)/V2B

to notify the vehicles about the nearby cyclists. The vehicle communication. 

was loaded with a Bluetooth interface to receive the iBea-There are some projects that investigated the safety of con messages from the cyclists. Concerning the motorcycle, road users from the experimental approach. RedEye \[326\]

it established a one-way 802.11p based communication to exploited a system where scooter rider decelerated and send the safety information from the motorcycle to the vehicle warned the nearby vehicles when it violated the red light. 

\(M2V\) whereby the vehicle could predict the collision and It also received the warning from other RedEye riders notify the driver. 

using smartphones. SPaT control of the traffic light was In the literature, a combination of human or sensor-based used as an optimization tool at the signalized intersection. 

methods and ITS-G5 has also been introduced to address VRUITS \[327\] was a project that investigated the mobility, the collision avoidance. Kwakkernaat *et al. *\[331\] proposed infotainment and safety of pedestrians, bikes, moped and a system that the vehicle was aware of the cyclist via motorcycles under various scenarios via ITS applications exchanging safety messages based on ITS-G5. It then merged and through V2I communication in addition to B2I, P2I and this acquired information with the data it received from moped/motorcycle to infrastructure \(M2I\) communications. 

the vision sensors to outperform the reliability of them. 

They introduced the intersection as the most dangerous colli-Inspired by \[102\], Segata *et al. *\[333\] explored the vehicle sion point basically in poor visibility. BikeCOM project \[328\]

cyclist intersection collision avoidance based on calculation utilized smartphones to establish a communication between of the collision probability and informed the vehicle driver to a cyclist and vehicle driver’s phone to exchange safety rel-avoid the accident. To avoid arbitrary collisions with bicycles, evant data and warn both the cyclist and the driver of the a treat assessment using vehicle dynamics along with longi-potential threat. Moreover, PROSPECT project \[329\] ana-tudinal and latitudinal movements of the vehicle have been lyzed the cyclist to vehicle collisions in different use cases modeled by Brännström *et al. *\[332\]. Summary of literature from the vehicle’s perspective. They discovered that intersec-reviews on VRUs is shown in Table 10. 

tions mostly contribute to the accidents. In addition, cyclist direction, driver’s intention, road topology and traffic rules influence were also studied. As further efforts in the VRUs **VII. CHALLENGES**

field, the aim of the in-Dev project \[336\] was to improve the Intersection management resiliency should be enormously safety of VRUs by investigating accident causation for VRUs observed since it is directly associated with human lives. 

7956

VOLUME 10, 2022



A. Gholamhosseinian, J. Seitz: Comprehensive Survey on Cooperative IM for Heterogeneous CVs **TABLE 10. **Summary of literature reviews on VRUs. 

There are many factors and challenges that contribute to the work properly under the given circumstances and can not robustness of the intersections operation as mentioned below. 

be generalized to other scenarios. However, road network involves plenty of scenarios that are hardly managed by a sin-A. SENSORS

gle solution. Hence, it is recommended to design a universal Sensors play an important role in data fusion from the vehi-approach such that it is adaptable to different situations and cles in the surroundings. They have many variations and is capable of meeting many cooperative IM goals \[25\]. 

deployment methods as follows \[337\]. Vision and sound sensors \(ultrasonic and acoustic\), remote sensing sensors D. HETEROGENEOUS COLLABORATION

like infrared, laser scanners, radar, Lidar, and RF/Wi-Fi/LTE

Vehicular traffic includes various vehicle types and brands transceivers, contact-based sensors including inductive loops, with distinctive characteristics and constraints encompassing magnetic sensors, strain gauge, piezoelectric, fiber optic, vehicle dynamics, sensors, communication equipment and pneumatic, seismic and vibration, off-road sensors such as so on. Thus, it is demanding to work on a generic standard unmanned aerial vehicles \(UAVs\), GPS, and mobile appa-that facilitates heterogeneous vehicles to collaborate with one ratus. All these miscellaneous sensors have various features another in an efficient way. 

such as coverage range, accuracy and light sensitivity. Thus, right usage or combination of sensors are necessary to be E. VEHICLE CLASSIFICATION

considered for better coordination of the traffic at the inter-Distinctive safety characteristics of heterogeneous vehicles section \[338\]. 

such as speed, acceleration, deceleration, reaction distance, breaking distance, stopping distance, and braking lag distance B. INFORMATION MANAGEMENT AND SHARING

highlights the necessity of vehicle classification especially There exist some challenging features in VANETs such as in safety critical IM applications. Gholamhosseinian and high mobility, speed and fast topology change that might Seitz \[337\] introduced VANETs as a potential approach for impact traffic safety and efficiency. In such a dynamic vehicle classification that took into account mobility and network, vehicles need to be very responsive and process physical parameters of the vehicles. In their investigation, the information rapidly. Apart from local processing in VANETs were introduced as an identical solution that could the vehicles or pre-processing sensors for delay-sensitive classify vehicles globally and in a real-time manner. In their applications, edge, fog and cloud computing are other alter-next research \[339\], they presented a VANET-based method-natives for data processing by bringing the computation ology to classify heterogeneous classes vehicles with respect and storage source closer to the vehicles at different levels. 

to their safety parameters such as acceleration, deceleration, This will decrease the perception and processing time of braking distance, stopping distance and also braking lag disa hazardous situation which is essential for safety critical tance of heterogeneous vehicle. Moreover, other important applications \[338\]. In addition to the location where vehicular parameters like velocity, load sensitivity, and reaction time information processing takes place either locally, on inter-were taken into consideration. 

mediate nodes or at the receiver side, there are other factors that highly influence the system performance and should be F. QUALITY MEASUREMENT

meticulously observed. These factors include data format, In order to fully exploit the advantages of cooperative IM, dissemination frequency and type of information that are it is suggested to measure the quality of cooperation at the shared among vehicles in different scenarios. Consequently, intersection. This topic has rarely gained attention in the the challenging task is to elaborate a concrete model that literature. Measurable parameters, quality model, scope of entails the whole environment characteristics adjacent to the quality rating, and responsible authority are open concerns intersection \[25\]. 

in this area that require careful consideration \[25\]. 

C. PLANNING UNIVERSAL SCHEME

G. EXTERNAL FACTORS

Majority of developed IM frameworks have been devised Researchers are recommended to consider different weather and tested for a particular scenario. Therefore, they only and road/rail conditions such as dry, wet, icy, snowy and oily VOLUME 10, 2022

7957



A. Gholamhosseinian, J. Seitz: Comprehensive Survey on Cooperative IM for Heterogeneous CVs as underlying factors in their IM solutions. These factors can location, and topology are important factors to gain applica-drastically impact traffic safety and efficiency. Additionally, tion reliability. 

they can directly affect travel time, speed, fuel consumption, In terms of channel optimization or information dissemina-throughput of the vehicles at the intersection. Further, from tion range, some approaches have been proposed for VANETs the safety perspective, inclement weather conditions might to diminish collisions on the roads. Tang and Yip \[343\]

influence vision, vehicle’s braking system, friction coeffi-researched a collision avoidance system based on the time-cient of the road/rail surface, and driver reaction time of to-avoid collision metric considering warning interval and different vehicles \[339\]. 

reaction time as well as different deceleration rates. For normal and poor channel conditions, DSRC transmission H. INTERSECTION TYPE

delays of 25 and 300 *ms * were assumed respectively. This Generally, intersections are classified into several categories approach might not be a comprehensive strategy due to size like crossroad, roundabout, X,Y and T-intersection, ramp of fixed delays. Furthermore, the behavior of the other inter-merge, deformed and misaligned intersections. Topology of secting car should also be considered to reach a sustainable intersection plays a vital role in IM such that it is defined safety. Sepulcre *et al. *\[344\] launched an empirical tests for according to a specific scenario and its particular traffic an intersection collision warning system. They realized that condition. 

the beacon rate of more than 2 *Hz * is required for a perfect warning reception. Besides, authors evaluated the challengI. LOCALIZATION FAULTS

ing case where a node at the intersection tried to congest the Simultaneous Localization and Mapping \(SLAM\) \[340\] is channel. Their work lacked the impact of congestion on the one of the advanced techniques used in many papers to mini-beacon rate as well as the latest congestion control methods. 

mize the localization error. Since this method is not flawless, Zinchenko *et al. *\[345\] investigated the impact of various den-a larger ST occupancy must be reserved by the intersection sities on static beacon intervals of 5, 10 and 15 *Hz * and figured manager in order to certainly prevent conflicts inside the out that information freshness of 0.2 second is not reachable intersection. The size of this safe margin is dependent on the for the rate 5Hz. To examine this V2X reliability test, they localization algorithm, maximum speed, and also the accu-moved the receiver along the road while the transmitter was racy of the vehicle sensors. In this context, \[15\] considered a maintained at different fixed locations. Moreover, by ana-safety space around the vehicles to compensate localization lyzing different scenarios, they discovered that better com-errors in sensors perception. Authors in \[196\] accounted for munication performance is acquired when the intersection a safety boundary for inter-crossing time of the vehicles to is fully surrounded by buildings in contrast to the situations overcome position uncertainties. 

where there is no building or they are placed on merely two corners. The reason lied in shadowing effects and partitioning J. COMMUNICATION ANOMALIES AND CHANNEL

of interference domain by the buildings. Joerer *et al. *\[346\]

OPTIMIZATION

proposed a V2V situation-based rate adaption solution for Communication delay, range and rate play critical roles in the endangered vehicles at the intersection to support vehicular intersection management efficiency, safety and scalability. 

safety. They applied this adaption on two congestion control Network delay is mainly proportional to the total number of mechanisms namely TRC and DynB and concluded that it CVs and their transmission packets. The processing capacity can increase the situation awareness. To mitigate collisions, of the intersection is derived according to the communication there are some approaches \[347\]–\[349\] and in \[350\]–\[353\], rate and also the traffic information that it receives from each the improvement of channel load, beaconing or information vehicle. Vehicle’s safety extremely depends on the reliability dissemination range were suggested. 

and timely reception and transmission of the information. 

Vehicles and infrastructure exchange information and should K. SYNCHRONIZATION

receive the safety information in a suitable distance from the To guarantee safety, it is imperative for the intersection par-intersection so that they can timely stop or slow down to avoid ticipants to be accurately synchronized. In Crossroads \[354\]

collisions. Haas and Hu \[341\] assessed the communication and its variation Crossroads\+ \[355\], synchronization and time performance of their systems by inserting collisions with high stamping between infrastructure and vehicles were proposed and constant velocity \(> 7 *m*/ *s*\) to the collision free routes as a reservation-based policy. Here, after clock synchroniza-of the vehicle and determined the probability of collision tion of all vehicles with the infrastructure, they shared their avoidance. This approach showed some drawbacks in terms status information with that. Afterwards, the infrastructure of realistic radio propagation models and low speed crash sent ‘‘time to actuate’’ and a constant speed to every vehicle situations. Zinchenko *et al. *\[342\] addressed the reliability of so that it could initiate to speed up or slow down at the V2V DSRC-based communication at the application level. 

relative time to adapt to the announced velocity. The system They considered information freshness, path prediction error showed notable efficiency. They considered an upper bound and communication range as their performance metrics and for the round trip delay and delegated ‘‘time-to-actuate’’ for developed some realistic scenarios at the intersections and vehicles to behave in a deterministic manner. In \[356\], the found out that traffic congestion, obstruction, intersection authors concentrated on a progressive data synchronization 7958

VOLUME 10, 2022



A. Gholamhosseinian, J. Seitz: Comprehensive Survey on Cooperative IM for Heterogeneous CVs strategy in order to prevent redundant transmissions of the utilized an optimal cruise control methodology based on vehicle agents at the autonomous intersections via bandwidth swarm algorithm, V2I and V2V communications to provide optimization and decreasing the data transmission. 

energy efficiency, lower trip time, passenger infotainment, higher throughput and safety for platoons of vehicles. They L. VEHICLE DYNAMICS AND MODEL MISMATCH

also considered vehicle dynamics and various constraints Basically, the estimation of the vehicle’s future trajectories at such as speed limit, engine power limit and stop-free strategy. 

the intersection area demands vehicle modeling. Researchers Researchers in \[361\] and \[362\] addressed measurement have modeled vehicles differently ranging from simple mod-and input uncertainties via some approximation algorithms els like one-dimension to more complex ones such as bicycle for collision avoidance heuristically. They utilized a central-and 4-wheel considering air drift, road slope, and mass mod-ized solution and verification problem and aimed to robustly els. The one-dimension model is the simplest model that takes avoid the \(invariant\) Bad Sets or dangerous situations for into account the velocity and longitudinal movement of the multiple vehicles \(agents\) at the intersection. Li *et al. *\[363\]

vehicle. It lacks the ability to capture the vehicle’s movement employed a heuristic approach and various game theory tech-in 2D space which is not so accurate. On the contrary, longi-niques to model the vehicle behavior and dynamics and find tudinal and latitudinal positions of the vehicle are considered the best heuristic-based solution for a collision free intersec-in the 4-wheel model. Additionally, velocity, heading and tion. Further, Bian *et al. *\[357\] studied the safe and efficient steering angle are also considered \[15\]. The bicycle model cooperation of vehicles at non-signalized intersections via represents an abstract variation of the 4-wheel model where partitioning the tasks into vehicle’s position and velocity two virtual wheels at the center of the vehicle represent the observation, safe arrival time optimization, and trajectory model. Other complex models can more precisely model the control areas. To this end, they designed distributed algo-vehicle’s behavior by considering additional features such rithms for every one of these tasks. 

as friction coefficient, mass, air drift, and road slope \[357\]. 

Specifically, parameters such as mechanical efficiency of the M. UNCERTAINTIES AND OTHERS FACTORS

drive-line, wheels torque, tire radius, gravitational accelera-Formal methods can not always guarantee safety for intersection, aerodynamic drag coefficient, rolling resistance, and the tions. Because vehicles might disregard the rules and deviate road slop are taken into consideration. However, these models from VTL signals, the planned trajectory or ST reservation. 

have enormous computational overhead and are not feasible Additionally, an approaching emergency vehicle can cause in dense situations. 

a disruption of the normal intersection management. Rea-The real vehicle and the considered vehicle model should sons may originate from IM crash, mechanical failure or match to avoid crashes at the intersection. Furthermore, sudden vehicle beak down, communications failure, distorted other external perturbations like wind may affect the normal information, human behavior or control reasons. This might vehicle behavior. In \[16\], a safe intersection crossing pro-also happen at hybrid intersections where the behavior of tocol was carried out by assigning two parameters arrival human-driven vehicles is unpredictable. Here, sound fault time \(FCFS\) and velocity from the infrastructure to the tolerant mechanisms are needed to detect the selfish actions approaching vehicles based on the received information from or other uncertainties. Some researchers have worked on this them. The authors proposed a system called RIM that utilized area. Recently, Khayatian *et al. *\[364\] proposed a resilient and a ST-based IM method for CAVs coordination at the intersec-robust algorithm for intersection management. In the studied tion. They studied the impact of confined external turbulence system, a rogue vehicle that does not follow the IM rules and demonstrated that model mismatch can be sorted out was detected. Then, IM broadcast a warning message to all with better throughput if a vehicle tracks a reference position vehicles and a big margin is accounted between the passing profile rather than a velocity one. The velocity reference time of them to ensure safety. Dedinsky *et al. *\[365\] utilized model \(assignment method\) is robust for an ideal situation a vision-based monitoring system to inform the IM in case where there is no external disturbances. The system showed a rogue vehicle appears or any other fault happens in the better throughput than existing IM methods. Qian *et al. *\[358\]

trajectories of the approaching vehicles to the intersection. 

suggested a control method for CAVs to reduce congestion, In \[366\], a collision avoidance system based on the coopera-travel time and ensure safety at the intersection. The optimal tive resource reservation was proposed. In the proposed sys-strategy was operated by an intersection manager and it was tem, an evasion plan database was considered for unexpected based on the TP by grouping the vehicles according to their situations like accidents or vehicle mechanical failures. In this longitudinal dynamics. Chen *et al. *\[359\] constructed a dis-case, the intersection manager could recover the possible tributed IM scheme for CAVs that employed safe geometric paths for the involved vehicles. 

topology of the vehicle platoons with efficient merge and Furthermore, the authors of \[367\] proposed a hybrid con-splitting of the groups. Authors considered vehicle dynam-trol of a centralized and distributed architecture for inter-ics, car-following model and topology of communication in section management. The centralized section assigned time their research to prevent collisions and improve velocity. The slots to the approaching vehicles whereas the distributed proposed model outperformed FCFS from the energy con-one ensured safety by allowing vehicles to optimally adjust sumption and travel time perspectives. Liu and Kamel \[360\]

the control inputs. Hafner *et al. *\[109\] studied the collision VOLUME 10, 2022

7959



A. Gholamhosseinian, J. Seitz: Comprehensive Survey on Cooperative IM for Heterogeneous CVs **TABLE 11. **Summary of literature reviews on robustness and resiliency challenges for IM. 

avoidance between two vehicles via control methods and performance of the system was also analyzed when vehicles vehicle states at the autonomous intersection. They availed experienced mechanical failures. 

capture sets to prevent vehicles to enter the bad sets at the same time whereby collisions occurred. In later work \[108\], O. SECURITY AND PRIVACY

they used the same concept but considered communication Authenticity of information that are exchanged among vehi-delay and model uncertainty in their experiment. In a similar cles is of crucial importance. authentication source, correct work, Campos *et al. *\[368\] addressed the same problem from information interval in case of false information dissem-the distributed perspective such that instead of globally pre-ination are other challenges that should be addressed. 

serving the capture and bad set, each vehicle maintained its Lefèvre *et al. *\[373\] studied the impact of privacy strategies local individual sets \(optimization\) that helped it to pass the on V2X communication. In cooperative vehicular wireless intersection and avoid collisions. In the next paper \[369\], they communication, security is one of the important concerns developed their work with receding horizon control scheme. 

since malicious information can lead to disaster especially at Moreover, authors in \[370\] proposed a decision-making sys-crucial places such as intersection. In spite of its significance, tem where a malicious vehicle does not hold to the intersec-there has been few efforts in the literature that addressed tion rules. In contrast, other vehicles play games according to the security of the intersection management systems. Today, their priority sequences which are based on the right of way CVs as well as intersection management systems are prone rules and compute the related Nash equilibrium as their con-to cyber attacks \[376\]. Attacks can target the wireless trol input for decision orders. Hubmann *et al. *\[28\] presented channel \[376\] in terms of Bluetooth, IEEE 802.11 or cellu-a safe model especially for uncertain maneuvers along the lar communications. Besides, they might physically install AVS path due to noisy sensor or drivers intention via usage of harmful applications \[377\] or access the vehicle’s controller POMDP \(partially observable Markov decision process\) and area network \(CAN\) bus \[378\]. Bentjen \[374\] examined two V2V to seek an optimal acceleration. 

scenarios where the system was attacked:

1\) *Sybil Attack * which deals with false or multi-reservations at a moment. They used FCFS and exhibited that traffic N. RECOVERY

jams mostly occur when some reservations have the When the abnormal situation at the intersection is resolved, most number of the collisions with other trajectories. 

it should possess a recovery plan to resume its regular oper-Other types of Sybil attacks are discussed in \[379\]: ation and avoid any deadlocks. However, in some conditions Nuisance which stands for delay in communication, like intersection blockage, vehicles must have embedded Herding which tricks the intersection to control various recovery systems to find a reroute. Li and Wang \[371\] devel-vehicles and Carjacking that implies single or multi oped four cooperative safe and time-optimal algorithms at a vehicle speed spoofing \[374\]. 

blind intersection based on spanning tree paradigm. In their 2\) *Squatting Attack * which enforces a vehicle to stop inside proposed methods, a recovery plan was also considered to the intersection. Thereby, the intersection manager is provide a new crossing schedule for the vehicles in situations compelled to notably lower the speed of other vehicles where an obstacle like a pedestrian abruptly appears on the resulting in traffic congestion. 

road or a pedestrian suddenly tries to pass the intersection. 

These problems might be mitigated as follows; defining a In another effort, Dresner and Stone \[372\] utilized a collision-lower bound on the speed of approaching vehicles for a squat-free centralized-based ST method at a hybrid intersection ting attack, detecting vehicles by ambient sensor deploy-using FCFS for AVs, and a similar mechanism for human ment or providing every message with a distinctive signed driven vehicles. In this multi-agent based system, recovery certificate in terms of Sybil attach. In another approach, 7960

VOLUME 10, 2022





A. Gholamhosseinian, J. Seitz: Comprehensive Survey on Cooperative IM for Heterogeneous CVs **FIGURE 4. **Distribution of intersection management goals. 

**FIGURE 5. **Distribution of literature based on the intersection management goals and architecture. 

Chen *et al. *\[375\] manifested a spoofing attacker effect on In addition, the proportion of efficiency comprised 14 percent the intersection manager. They investigated that a malicious while IM approaches with safe, efficient and environmental vehicle can trick the system and cause congestion by sending friendly goals showed only a slight decrease to 12 percent. 

false information to the intersection manager. Table 11 lists Five remaining goals inclusively covered 10 percent of the the literature that addressed different performance challenges literature. Efficient and ecological IM approaches contained for IM. 

4 percent of all publications similar to multi-objective solutions that incorporated 3 percent of entire research works. 

## **VIII. SUMMARY**

Moreover, IM methods considering safety, efficiency and In summary, Fig. 4 illustrates the percentage of nine types infotainment aspects contributed to 2 percent of the literature. 

of IM goals. Overall, the most significant goals addressed Lastly, apart from scant number of IM methods that addressed in the literature which accounted for 37 and 26 percent safe, ecological and infotainment goals, 1 percent of the were safety plus efficiency along with safety respectively. 

literature focused on environmental concerns. 

VOLUME 10, 2022

7961





A. Gholamhosseinian, J. Seitz: Comprehensive Survey on Cooperative IM for Heterogeneous CVs **FIGURE 6. **Distribution of literature based on the intersection management goals and coordination method. 

**FIGURE 7. **Distribution of literature based on the intersection management goals and intersection modeling. 

Fig. 5 illustrates the literature that investigated the IM

similar contribution as safety-driven goals with 18 and from an architecture perspective. Overall, V2V comprised 19 efforts respectively. Among the remaining four goals with the majority of articles including 68 papers on safety plus 16 papers, efficiency and environment category held the efficiency followed by safety with 39 papers. Safe, effi-majority papers with 8, followed by environment by 3 rele-cient and ecological V2V-based approaches comprised simi-vant articles. Multi-objective V2I-based schemes along with lar number of articles as efficient ones, with 18 and 19 papers articles involved in safe, efficient plus infotainment shared respectively. The other four goals with a total of 15 papers identical amount of literature, each with 2 publications. Fur-rarely contributed to the literature. In terms of V2I-based IM

thermore, combination of V2I and V2V-based methods with methods, which is the second most prevalent architecture, sum of 19 articles was the next favorite architecture used 44 papers focused on safety plus efficiency while 23 arti-for IM. Next, VRUs such as bikes, motorcycles, pedestrians, cles addressed efficient V2I-based IM techniques. Besides, scooters, with various forms of centralized and decentralized safe, efficient and environmental centralized methods showed architectures mostly dealt with safety issues, while one out of 7962

VOLUME 10, 2022





A. Gholamhosseinian, J. Seitz: Comprehensive Survey on Cooperative IM for Heterogeneous CVs **FIGURE 8. **Distribution of literature based on the intersection management goals and intersection types. 

13 reviewed papers examined safety, efficiency and infotain-the performance of the IM. In this paper, we presented a ment goals at once. Furthermore, researchers scarcely used comprehensive survey on current solutions for the IM under other types of architectures in their works. 

connected vehicles environment. Heterogeneous classes of With regard to the coordination methods, as it is shown vehicles such as trams/trains, VRUs, and other types of vehi-in Fig. 6, optimization-based policies with 277 articles was cles were discussed in our research. We studied signalized, by far the most commonly used method. Here, 96 papers hybrid and autonomous intersections with respect to diverse addressed safety plus efficiency while 78 and 40 papers were criteria including various intersection modeling, three sub-interested to conduct their research on safety as well as effi-stantial scheduling policies, different architectures and four ciency respectively. Moreover, 30 out of 63 remaining arti-major goals that they serve based on the application scenario. 

cles concerned safety, efficiency and environment. Besides, We emphasized on the autonomous intersections and investi-13 researchers explored optimal efficient and ecological IM

gated the relevant proposals in details in terms of safety, effi-whereas only 8 works were dedicated to multi-objective ciency, environment and infotainment. Further, we explored optimization-based IM strategies. Further, 7 researchers IM attempts for VRUs as one of the most important road users took advantage of optimization methods to provide a safe with the focus on wheeled and motorized vehicles. Besides, and efficient IM considering infotainment aspects. All the we described numerous parameters that influence the IM

4 environmental-friendly approaches benefited from opti-performance from the robustness and resiliency points of mization algorithms for traffic management at the intersec-view. Finally, multiple analyses were conducted to compare tions. In addition, heuristic-based approaches incorporated and visualize the results. 

20 papers while other mechanisms did not have noticeable To the authors knowledge, this paper is the first one that contribution to the literature. 

systematically addressed the cooperative IM from different In terms of intersection modelling, as it is illustrated in aspects such as heterogeneous vehicles, diverse intersec-Fig. 7, most of the publications were keen to use TP instead tion management goals and also variations of the intersec-of ST technique. There were only two exceptions; one was tions. We reviewed most of the published papers in well efficiency where TP and ST intersection modellings revealed reputed libraries. The initial research discovered more than analogous participation of the literature, each with 23 papers. 

1200 papers, which we eventually narrowed down to around The second one was demonstrated in safe and efficient 379 papers by eliminating trivial candidates. Compared to the IM frameworks where 37 out of 120 corresponding efforts existing surveys, we markedly considered more relevant and exploited ST. 

recent articles and endeavoured to present a comprehensive The last figure exhibits the distribution of IM goals with reference in the area of IM. In our study, we observed that respect to three different intersection types. Comparably, most of the researchers tend to apply optimization-based as shown in Fig. 8, ample amounts of efforts have been dis-scheduling methods rather than FCFS and heuristic coor-cussed for AIM rather than hybrid or signalized IM. Among dination mechanisms such that around 277 papers gener-all works that tackled IM for heterogeneous CVs, signal-ally benefited from this method. Further, compared to other ized intersections with 22 and semi-autonomous intersections methodologies, V2V-based architecture seemed to be more with 21 articles held marginal amount of studied articles in widespread as the corresponding literature demonstrated this survey. 

superiority over V2I-based methods with 159 articles compared to 119. With regard to the intersection modeling, **IX. CONCLUSION**

TP was more common than ST reservation mechanism in In near future, cooperative traffic coordination methods all mentioned goals where this modelling method was rarely using wireless vehicular communications promise to raise favored for IM systems except for safe and efficient IM ones VOLUME 10, 2022

7963



A. Gholamhosseinian, J. Seitz: Comprehensive Survey on Cooperative IM for Heterogeneous CVs in addition to safe proposed IM solutions that more exten-

\[20\] E. Namazi, J. Li, and C. Lu, ‘‘Intelligent intersection management sys-sively utilized such a method in their works. Furthermore, tems considering autonomous vehicles: A systematic literature review,’’

*IEEE Access*, vol. 7, pp. 91946–91965, 2019. 

the evaluation results indicated that majority of researchers

\[21\] M. Khayatian, M. Mehrabian, E. Andert, R. Dedinsky, S. Choudhary, opted for a combination of safety and efficiency as their Y. Lou, and A. Shirvastava, ‘‘A survey on intersection management of goals towards the management of the intersections. Safety, connected autonomous vehicles,’’ *ACM Trans. Cyber-Phys. Syst. *, vol. 4, no. 4, p. 48, 2020. 

efficiency and a mixture of the aforementioned goals with

\[22\] S. Krishnan, R. Govind Aadithya, R. Ramakrishnan, V. Arvindh, and environment were ranked subsequently. Last but not least, due K. Sivanathan, ‘‘A look at motion planning for AVs at an intersection,’’ in to our research, most of the researchers were highly inclined *Proc. 21st Int. Conf. Intell. Transp. Syst. \(ITSC\)*, Nov. 2018, pp. 333–340. 

to adopt AIM as apposed to signalized or hybrid intersections. 

\[23\] Q. Guo, L. Li, and X. J. Ban, ‘‘Urban traffic signal control with connected and automated vehicles: A survey,’’ *Transp. Res. C, Emerg. Technol. *, vol. 101, pp. 313–334, Apr. 2019. 

## **REFERENCES**

\[24\] Z. Zhong, M. Nejad, and E. E. Lee, ‘‘Autonomous and semiautonomous intersection management: A survey,’’ *IEEE Intell. Transp. Syst. Mag. *, 

\[1\] Statista. \(2021\). *Number of Passenger Cars and Commercial Vehicles in* vol. 13, no. 2, pp. 53–70, Summer 2021. 

*Use Worldwide From 2006 to 2015 in \(1,000 Units\)*. \[Online\]. Avail-

\[25\] S. Malik, M. A. Khan, and H. El-Sayed, ‘‘Collaborative autonomous able: https://www.statista.com/statistics/281134/number-of-vehicles-in-driving—A survey of solution approaches and future challenges,’’ *Sen-use-worldwide*
* 
sors, vol. 21, no. 11, pp. 6247–6254, May 2021. 

\[2\] U. Franke, C. Rabe, S. Gehrig, H. Badino, and A. Barth, ‘‘Dynamic stereo

\[26\] Y. Bichiou and H. A. Rakha, ‘‘Developing an optimal intersection control vision for intersection assistance,’’ in Proc. 32nd Congr. , vol. 2, 2008, system for automated connected vehicles,’’ IEEE Trans. Intell. Transp. 

pp. 180–189. 

Syst. , vol. 20, no. 5, pp. 1908–1916, Jun. 2018. 

\[3\] R. Azimi, G. Bhatia, R. R. Rajkumar, and P. Mudalige, ‘‘STIP: Spatio-

\[27\] J. Gregoire, S. Bonnabel, and A. de La Fortelle, ‘‘Optimal cooperative temporal intersection protocols for autonomous vehicles,’’ in Proc. 

motion planning for vehicles at intersections,’’ in Proc. IEEE IV Work-ACM/IEEE Int. Conf. Cyber-Phys. Syst. \(ICCPS\), Apr. 2014, pp. 1–12. 

shop Navigat., Accurate Positioning Mapping Intell. Vehicles, Oct. 2013, 

\[4\] Y. Rahmati and A. Talebpour, ‘‘Towards a collaborative connected, auto-pp. 1–6. 

mated driving environment: A game theory based decision framework for

\[28\] C. Hubmann, M. Becker, D. Althoff, D. Lenz, and C. Stiller, ‘‘Decision unprotected left turn maneuvers,’’ in Proc. IEEE Intell. Vehicles Symp. 

making for autonomous driving considering interaction and uncertain \(IV\), Jun. 2017, pp. 1316–1321. 

prediction of surrounding vehicles,’’ in Proc. IEEE Intell. Vehicles Symp. 

\[5\] N. A. Stanton and P. M. Salmon, ‘‘Human error taxonomies applied \(IV\), Jun. 2017, pp. 1671–1678. 

to driving: A generic driver error taxonomy and its implications for

\[29\] P. Lin, J. Liu, P. J. Jin, and B. Ran, ‘‘Autonomous vehicle-intersection intelligent transport systems,’’ Saf. Sci. , vol. 47, no. 2, pp. 227–237, 2009. 

coordination method in a connected vehicle environment,’’ IEEE Intell. 
*
*\[6\] M.-K. Shi, H. Jiang, and S.-H. Li, ‘‘An intelligent traffic-flow-based real-Transp. Syst. Mag. *, vol. 9, no. 4, pp. 37–47, Oct. 2017. 

time vehicles scheduling algorithm at intersection,’’ in *Proc. 14th Int. *

\[30\] I. H. Zohdy, R. K. Kamalanathsharma, and H. Rakha, ‘‘Intersection *Conf. Control, Autom., Robot. Vis. \(ICARCV\)*, Nov. 2016, pp. 1–5. 

management for autonomous vehicles using iCACC,’’ in *Proc. 15th Int. *

\[7\] A. Festag, ‘‘Cooperative intelligent transport systems standards in *IEEE Conf. Intell. Transp. Syst. *, Sep. 2012, pp. 1109–1114. 

Europe,’’ *IEEE Commun. Mag. *, vol. 53, no. 12, pp. 166–172, Dec. 2014. 

\[31\] A. L. C. Bazzan, D. de Oliveira, and B. C. da Silva, ‘‘Learning in groups

\[8\] Q. Chen, D. Jiang, and L. Delgrossi, ‘‘IEEE 1609.4 DSRC multi-channel of traffic signals,’’ *Eng. Appl. Artif. Intell. *, vol. 23, no. 4, pp. 560–568, operations and its implications on vehicle safety communications,’’ in 2010. 

*Proc. IEEE Veh. Netw. Conf. \(VNC\)*, Oct. 2009, pp. 1–8. 

\[32\] S. El-Tantawy and B. Abdulhai, ‘‘Towards multi-agent reinforcement

\[9\] A. M. Abdelgader and W. Lenan, ‘‘The physical layer of the IEEE

learning for integrated network of optimal traffic controllers \(MARLIN-802.11p WAVE communication standard: The specifications and chal-OTC\),’’ *Transp. Lett. *, vol. 2, no. 2, pp. 89–110, Apr. 2010. 

lenges,’’ in *Proc. World Congr. Eng. Comput. Sci. *, 2014, vol. 2, no. 71, 

\[33\] F. Zhu, H. M. A. Aziz, X. Qian, and S. V. Ukkusuri, ‘‘A junction-pp. 1–8. 

tree based learning algorithm to optimize network wide traffic control:

\[10\] Frank Perry. *SAE J2735*. Accessed: Nov. 23, 2021. \[Online\]. Available: A coordinated multi-agent framework,’’ *Transp. Res. C, Emerg. Technol. *, https://www.transportation.institute.ufl.edu/wp-content/uploads/2017/

vol. 58, pp. 487–501, Sep. 2015. 

04/HNTB-SAE-Standards.pdf

\[34\] S. Liu, W. Zhang, X. Wu, S. Feng, X. Pei, and D. Yao, ‘‘A simulation

\[11\] Y. J. Li, ‘‘An overview of the DSRC/WAVE technology,’’ in *Proc. Int. *

system and speed guidance algorithms for intersection traffic control *Conf. Heterogeneous Netw. Qual., Rel., Secur. Robustness*. Houston, TX, using connected vehicle technology,’’ *Tsinghua Sci. Technol. *, vol. 24, USA: Springer, 2010, pp. 544–558. 

no. 2, pp. 160–170, Apr. 2019. 

\[12\] J. Misener, ‘‘SAE connected vehicle standards,’’ Qualcomm Technol., 

\[35\] X. Shen, X. Zhang, T. Ouyang, Y. Li, and P. Raksincharoensak, ‘‘Coop-San Diego, CA, USA, Tech. Rep. CES 2016, 2016. 

erative comfortable-driving at signalized intersections for connected

\[13\] X. Wang, S. Mao, and M. X. Gong, ‘‘An overview of 3GPP cellular and automated vehicles,’’ *IEEE Robot. Autom. Lett. *, vol. 5, no. 4, vehicle-to-everything standards,’’ *GetMobile, Mobile Comput. Commun. *, pp. 6247–6254, Oct. 2020. 

vol. 21, no. 3, pp. 19–25, Nov. 2017. 

\[36\] S. A. Fayazi and A. Vahidi, ‘‘Mixed-integer linear programming for

\[14\] *Study on LTE Support for V2X Services*, document G.T. 22.885, optimal scheduling of autonomous vehicle intersection crossing,’’ *IEEE*

Feb. 2015. 

*Trans. Intell. Veh. *, vol. 3, no. 3, pp. 287–299, Sep. 2018. 

\[15\] K. Dresner and P. Stone, ‘‘A multiagent approach to autonomous intersec-

\[37\] S. A. Fayazi, A. Vahidi, and A. Luckow, ‘‘Optimal scheduling of tion management,’’ *J. Artif. Intell. Res. *, vol. 31, pp. 591–656, Mar. 2008. 

autonomous vehicle arrivals at intelligent intersections via MILP,’’ in

\[16\] M. Khayatian, M. Mehrabian, and A. Shrivastava, ‘‘RIM: Robust inter-Proc. Amer. Control Conf. \(ACC\), May 2017, pp. 4920–4925. 

section management for connected autonomous vehicles,’’ in *Proc. IEEE*

\[38\] F. Ashtiani, S. A. Fayazi, and A. Vahidi, ‘‘Multi-intersection traffic *Real-Time Syst. Symp. \(RTSS\)*, Dec. 2018, pp. 35–44. 

management for autonomous vehicles via distributed mixed integer linear

\[17\] J. Lee and B. Park, ‘‘Development and evaluation of a cooperative programming,’’ in *Proc. Annu. Amer. Control Conf. \(ACC\)*, Jun. 2018, vehicle intersection control algorithm under the connected vehicles envi-pp. 6341–6346. 

ronment,’’ *IEEE Trans. Intell. Transp. Syst. *, vol. 13, no. 3, pp. 81–90, 

\[39\] X. Meng and C. G. Cassandras, ‘‘Optimal control of autonomous vehicles Mar. 2012. 

for non-stop signalized intersection crossing,’’ in *Proc. IEEE Conf. Decis. *

\[18\] J. Rios-Torres and A. A. Malikopoulos, ‘‘A survey on the coordination *Control \(CDC\)*, Dec. 2018, pp. 6988–6993. 

of connected and automated vehicles at intersections and merging at

\[40\] Z. Zhu, N. Pivaro, S. Gupta, A. Gupta, and M. Canova, ‘‘Safe model-highway on-ramps,’’ *IEEE Trans. Intell. Transp. Syst. *, vol. 18, no. 5, based off-policy reinforcement learning for eco-driving in connected and pp. 1066–1077, May 2017. 

automated hybrid electric vehicles,’’ 2021, *arXiv:2105.11640*. 

\[19\] L. Chen and C. Englund, ‘‘Cooperative intersection management: A sur-

\[41\] H.-J. Chang and G.-T. Park, ‘‘A study on traffic signal control at signalized vey,’’ *IEEE Trans. Intell. Transp. Syst. *, vol. 17, no. 2, pp. 570–586, intersections in vehicular ad hoc networks,’’ *Ad Hoc Netw. *, vol. 11, no. 7, Feb. 2016. 

pp. 2115–2124, Sep. 2013. 

7964

VOLUME 10, 2022



A. Gholamhosseinian, J. Seitz: Comprehensive Survey on Cooperative IM for Heterogeneous CVs

\[42\] X.-F. Xie and Z.-J. Wang, ‘‘SIV-DSS: Smart in-vehicle decision support

\[64\] Z. Shen, A. Mahmood, Y. Wang, and L. Wang, ‘‘Coordination of con-system for driving at signalized intersections with V2I communication,’’

nected autonomous and human-operated vehicles at the intersection,’’ in *Transp. Res. C, Emerg. Technol. *, vol. 90, pp. 181–197, May 2018. 

*Proc. IEEE/ASME Int. Conf. Adv. Intell. Mechatronics \(AIM\)*, Jul. 2019, 

\[43\] J. Wang, D. Zhang, J. Liu, M. Lu, and K. Li, ‘‘Multi-objective driving pp. 1391–1396. 

assistance system for intersection support,’’ in *Proc. 13th Int. IEEE Conf. *

\[65\] G. Sharon, S. D. Boyles, and P. Stone, ‘‘Intersection management protocol *Intell. Transp. Syst. *, Sep. 2010, pp. 348–353. 

for mixed autonomous and human-operated vehicles,’’ *Transp. Res. C, *

\[44\] Y. Zhao, S. Yao, H. Shao, and T. Abdelzaher, ‘‘Codrive: Coopera-Emerg. Technol. , 2017. 

tive driving scheme for vehicles in urban signalized intersections,’’ in

\[66\] X. Liu, P.-C. Hsieh, and P. R. Kumar, ‘‘Safe intersection management *Proc. ACM/IEEE 9th Int. Conf. Cyber-Phys. Syst. \(ICCPS\)*, Apr. 2018, for mixed transportation systems with human-driven and autonomous pp. 308–319. 

vehicles,’’ in *Proc. 56th Annu. Allerton Conf. Commun., Control, Comput. *

\[45\] S. Mandava1, K. Boriboonsomsin, and M. Barth, ‘‘Arterial velocity plan-

*\(Allerton\)*, Oct. 2018, pp. 834–841. 

ning based on traffic signal information under light traffic conditions,’’ in

\[67\] E. Onieva, U. Hernandez-Jayo, E. Osaba, A. Perallos, and X. Zhang, *Proc. 12th Int. IEEE Conf. Intell. Transp. Syst. *, Oct. 2009, pp. 1–6. 

‘‘A multi-objective evolutionary algorithm for the tuning of fuzzy rule

\[46\] R. K. Kamalanathsharma and H. A. Rakha, ‘‘Leveraging connected vehi-bases for uncoordinated intersections in autonomous driving,’’ *Inf. Sci. *, cle technology and telematics to enhance vehicle fuel efficiency in the vol. 321, pp. 14–30, Nov. 2015. 

vicinity of signalized intersections,’’ *J. Intell. Transp. Syst. *, vol. 20, no. 1, 

\[68\] E. Onieva, V. Milanés, J. Villagrá, J. Pérez, and J. Godoy, ‘‘Genetic pp. 33–44, Jan. 2016. 

optimization of a vehicle fuzzy decision system for intersections,’’ *Expert*

\[47\] Z. Du and P. Pisu, ‘‘A fuel efficient control strategy for connected vehicles *Syst. Appl. *, vol. 39, no. 18, pp. 13148–13157, 2012. 

in multiple-lane urban roads,’’ in *Proc. IEEE 55th Conf. Decis. Control*

\[69\] H. Ahn, A. Rizzi, A. Colombo, and D. D. Vecchio, ‘‘Experimental testing *\(CDC\)*, Dec. 2016, pp. 715–720. 

of a semi-autonomous multi-vehicle collision avoidance algorithm at an

\[48\] Z. Wang, G. Wu, P. Hao, and M. J. Barth, ‘‘Cluster-wise cooperative intersection testbed,’’ in *Proc. IEEE/RSJ Int. Conf. Intell. Robots Syst. *

eco-approach and departure application along signalized arterials,’’ in *\(IROS\)*, Sep./Oct. 2015. 

*Proc. IEEE 20th Int. Conf. Intell. Transp. Syst. \(ITSC\)*, Oct. 2017, 

\[70\] S. A. Fayazi and A. Vahidi, ‘‘Vehicle-in-the-loop \(VIL\) verification of a pp. 145–150. 

smart city intersection control scheme for autonomous vehicles,’’ in *Proc. *

\[49\] F. Saust, J. M. Wille, and M. Maurer, ‘‘Energy-optimized driving with *IEEE Conf. Control Technol. Appl. \(CCTA\)*, Aug. 2017, pp. 1575–1580. 

an autonomous vehicle in urban environments,’’ in *Proc. IEEE 75th Veh. *

\[71\] S. Fu, W. Zhang, and Z. Jiang, ‘‘A network-level connected autonomous *Technol. Conf. \(VTC Spring\)*, May 2012, pp. 1–5. 

driving evaluation platform implementing C-V2X technology,’’ *China* *Commun. *, vol. 18, no. 6, pp. 77–88, Jun. 2021. 

\[50\] S. Gutesa, J. Lee, and D. Besenski, ‘‘Development and evaluation of

\[72\] Y. Cheng, C. Chen, X. Hu, K. Chen, Q. Tang, and Y. Song, ‘‘Enhancing cooperative intersection management algorithm under connected and mixed traffic flow safety via connected and autonomous vehicle trajec-automated vehicles environment,’’ *Transp. Res. Rec., J. Transp. Res. *

tory planning with a reinforcement learning approach,’’ *J. Adv. Transp. *, *Board*, vol. 2675, no. 7, pp. 94–104, Feb. 2021. 

vol. 2021, Jun. 2021, Art. no. 6117890. 

\[51\] B. Asadi and A. Vahidi, ‘‘Predictive cruise control: Utilizing upcoming

\[73\] M. O. Sayin, C.-W. Lin, S. Shiraishi, J. Shen, and T. Basar, ‘‘Information-traffic signal information for improving fuel economy and reducing trip driven autonomous intersection control via incentive compatible mecha-time,’’ *IEEE Trans. Control Syst. Technol. *, vol. 19, no. 3, pp. 707–714, nisms,’’ *IEEE Trans. Intell. Transp. Syst. *, vol. 20, no. 3, pp. 912–924, May 2011. 

Mar. 2019. 

\[52\] H. M. A. Aziz and S. V. Ukkusuri, ‘‘Unified framework for dynamic

\[74\] R. Sinha, P. S. Roop, and P. Ranjitkar, ‘‘Virtual traffic lights\+: traffic assignment and signal control with cell transmission model,’’

A robust, practical, and functionally safe intelligent transportation sys-Transp. Res. Rec., J. Transp. Res. Board, vol. 2311, no. 1, pp. 73–84, tem,’’ *J. Transp. Res. Board*, vol. 2831, no. 1, pp. 73–80, Dec. 2013. 

Jan. 2012. 

\[75\] M. Wooldridge, *An Introduction to Multiagent Systems*. New York, NY, 

\[53\] P. Varaiya, ‘‘Max pressure control of a network of signalized intersec-USA: Wiley, 2009. 

tions,’’ *Transp. Res. C, Emerg. Technol. *, vol. 36, pp. 177–195, Nov. 2013. 

\[76\] European Commission, Directorate-General for Mobility and Transport, 

\[54\] J. Gregoire, X. Qian, E. Frazzoli, A. de La Fortelle, and T. Wongpirom-

‘‘Road safety in the European union: Trends, statistics and main chal-sarn, ‘‘Capacity-aware backpressure traffic signal control,’’ *IEEE Trans. *

lenge,’’ Eur. Union, Maastricht, The Netherlands, Tech. Rep. MI-AC-15-Control Netw. Syst. , vol. 2, no. 2, pp. 164–173, Jun. 2015. 

001-EN-N, Mar. 2015. 

\[55\] J. Gregoire, E. Frazzoli, A. de La Fortelle, and T. Wongpiromsarn, ‘‘Back-

\[77\] *Horizon 2020-Work Programme 2014–2015, Smart, Green and Inte-pressure traffic signal control with unknown routing rates,’’ IFAC Proc. *
* 
grated Transport, European Commission, Brussels, Belgium, 2015. 

Volumes, vol. 47, no. 3, pp. 11332–11337, 2014. 

\[78\] D. Thielen, T. Lorenz, M. Hannibal, F. Koster, and J. Plattner, ‘‘A feasi-

\[56\] M. Pourmehrab, L. Elefteriadou, S. Ranka, and M. Martin-Gasulla, bility study on a cooperative safety application for cyclists crossing inter-

‘‘Optimizing signalized intersections performance under conventional sections,’’ in Proc. 15th Int. IEEE Conf. Intell. Transp. Syst. , Sep. 2012, and automated vehicles traffic,’’ IEEE Trans. Intell. Transp. Syst. , vol. 21, pp. 1197–1204. 

no. 7, pp. 2864–2873, Jul. 2020. 

\[79\] U. S. Department of Transportation. Accessed: Nov. 23, 2021. \[Online\]. 

\[57\] X. Qian, J. Gregoire, F. Moutarde, and A. De La Fortelle, ‘‘Priority-Available: https://www.its.dot.gov/pilots/pilots-v2i.htm based coordination of autonomous and legacy vehicles at intersection,’’

\[80\] ‘‘Vehicle safety communications project task 3 final report: Identify intel-in Proc. 17th Int. IEEE Conf. Intell. Transp. Syst. \(ITSC\), Oct. 2014, ligent vehicle safety applications enabled by DSRC,’’ US Dept. Transp., pp. 1166–1171. 

Nat. Highway Traffic Saf. Admin., Washington, DC, USA, Project Rep. 

\[58\] Z. Wang, H. Zhu, Y. Zhou, and X. Luo, ‘‘Joint traffic signal and connected DOT HS 809 859, Mar. 2005, pp. 809–859. 

vehicle control in IoV via deep reinforcement learning,’’ in Proc. IEEE

\[81\] M. Segata and R. L. Cigno, ‘‘Automatic emergency braking: Realistic Wireless Commun. Netw. Conf. \(WCNC\), Mar. 2021, pp. 1–6. 

analysis of car dynamics and network performance,’’ IEEE Trans. Veh. 

\[59\] R. Verma and D. D. Vecchio, ‘‘Semiautonomous multivehicle safety,’’

Technol. , vol. 62, no. 9, pp. 4150–4161, Nov. 2013. 

IEEE Robot. Automat. Mag. , vol. 18, no. 3, pp. 44–54, Sep. 2011. 

\[82\] T. Neudecker, N. An, O. K. Tonguz, T. Gaugel, and J. Mittag, ‘‘Feasibility

\[60\] M. Hausknecht, T.-C. Au, and P. Stone, ‘‘Autonomous intersection man-of virtual traffic lights in non-line-of-sight environments,’’ in Proc. 9th agement: Multi-intersection optimization,’’ in Proc. IEEE/RSJ Int. Conf. 

ACM Int. Workshop Veh. Inter-Netw., Syst., Appl. \(VANET\), Lake District, Intell. Robots Syst. , Sep. 2011, pp. 4581–4586. 

U.K., Jun. 2012, pp. 103–106. 

\[61\] P. Li and X. Zhou, ‘‘Recasting and optimizing intersection automation as a

\[83\] M. Ferreira, R. Fernandes, H. Conceição, W. Viriyasitavat, and connected-and-automated-vehicle \(CAV\) scheduling problem: A sequen-O. K. Tonguz, ‘‘Self-organized traffic control,’’ in Proc. 7th ACM Int. 
*
*tial branch-and-bound search approach in phase-time-traffic hypernet-Workshop Veh. Internetworking \(VANET\)*, vol. 7, Sep. 2010, pp. 85–90. 

work,’’ *Transp. Res. B, Methodol. *, vol. 105, pp. 479–506, Nov. 2017. 

\[84\] L. Le, A. Festag, R. Baldessari, and W. Zhang, ‘‘Vehicular wireless short-

\[62\] G. Sharon and P. Stone, ‘‘A protocol for mixed autonomous and human-range communication for improving intersection safety,’’ *IEEE Commun. *

operated vehicles at intersections,’’ in *Proc. Int. Conf. Auton. Agents* *Mag. *, vol. 47, no. 11, pp. 104–110, Nov. 2009. 

*Multiagent Syst. *, 2017, pp. 151–167. 

\[85\] S. Joerer, B. Bloessl, M. Segata, C. Sommer, R. L. Cigno, A. Jamalipour, 

\[63\] P. Stone, S. Zhang, and T.-C. Au, ‘‘Autonomous intersection management and F. Dressler, ‘‘Enabling situation awareness at intersections for IVC

for semi-autonomous vehicles,’’ in *Routledge Handbook of Transporta-congestion control mechanisms,’’ IEEE Trans. Mobile Comput. , vol. 15, tion. Evanston, IL, USA: Routledge, 2015, pp. 116–132. *
* 
no. 7, pp. 1674–1685, Jul. 2016. 

VOLUME 10, 2022

7965



A. Gholamhosseinian, J. Seitz: Comprehensive Survey on Cooperative IM for Heterogeneous CVs

\[86\] Statistics on Intersection Accidents. Accessed: Nov. 23, 2021. \[Online\]. 

\[108\] M. R. Hafner, D. Cunningham, L. Caminiti, and D. Vecchio, ‘‘Coop-Available:

https://www.autoaccident.com/statistics-on-intersection-erative collision avoidance at intersections: Algorithms and experi-accidents.html

ments,’’ IEEE Trans. Intell. Transp. Syst. , vol. 14, no. 3, pp. 1162–1175, 

\[87\] L. Tu and C. Huang, ‘‘Forwards: A map-free intersection collision-Mar. 2013. 

warning system for all road patterns,’’ IEEE Trans. Veh. Technol. , vol. 59, 

\[109\] M. R. Hafner, D. Cunningham, L. Caminiti, and D. Del Vecchio, ‘‘Autono. 7, pp. 3233–3248, Sep. 2010. 

mated vehicle-to-vehicle collision avoidance at intersections,’’ in Proc. 
*
*\[88\] J.-B. Tomas-Gabarron, E. Egea-Lopez, and J. Garcia-Haro, ‘‘Vehicu-18th ITS World Congr. *, vol. 185, Oct. 2011, pp. 1–3. 

lar trajectory optimization for cooperative collision avoidance at high

\[110\] S. Lefèvre, C. Laugier, and J. Ibañez-Guzmán, ‘‘Risk assessment at road speeds,’’ *IEEE Trans. Intell. Transp. Syst. *, vol. 14, no. 4, pp. 1930–1941, intersections: Comparing intention and expectation,’’ in *Proc. IEEE Intell. *

Dec. 2013. 

*Vehicles Symp. *, Jun. 2012, pp. 165–171. 

\[89\] H. Chen, L. Cao, and D. B. Logan, ‘‘Investigation into the effect of an

\[111\] M. Liebner, M. Baumann, F. Klanner, and C. Stiller, ‘‘Driver intent intersection crash warning system on driving performance in a simulator,’’

inference at urban intersections using the intelligent driver model,’’ in *Traffic Injury Prevention*, vol. 12, no. 5, pp. 529–537, Oct. 2011. 

*Proc. IEEE Intell. Vehicles Symp. *, Jun. 2012, pp. 1162–1167. 

\[90\] G. Lu, L. Li, Y. Wang, R. Zhang, Z. Bao, and H. Chen, ‘‘A rule based

\[112\] C. Oh and T. Kim, ‘‘Estimation of rear-end crash potential using control algorithm of connected vehicles in uncontrolled intersection,’’

vehicle trajectory data,’’ *Accident Anal. Prevention*, vol. 42, no. 6, in *Proc. 17th Int. IEEE Conf. Intell. Transp. Syst. \(ITSC\)*, Oct. 2014, pp. 1888–1893, Nov. 2010. 

pp. 115–120. 

\[113\] G. Weidl, G. Breuel, and V. Singhal, ‘‘Collision risk prediction and

\[91\] F. Belkhouche, ‘‘Control of autonomous vehicles at an unsignalized inter-warning at road intersections using an object oriented Bayesian network,’’

section,’’ in *Proc. Amer. Control Conf. \(ACC\)*, May 2017, pp. 1340–1345. 

in *Proc. 5th Int. Conf. Automot. User Interfaces Interact. Veh. Appl. \(Auto-*

\[92\] L. Riegger, M. Carlander, N. Lidander, N. Murgovski, and J. Sjoberg, *motiveUI\)*, 2013, pp. 270–277. 

‘‘Centralized MPC for autonomous intersection crossing,’’ in *Proc. IEEE*

\[114\] M. Goldhammer, E. Strigel, D. Meissner, U. Brunsmann, K. Doll, and *19th Int. Conf. Intell. Transp. Syst. \(ITSC\)*, Nov. 2016, pp. 1372–1377. 

K. Dietmayer, ‘‘Cooperative multi sensor network for traffic safety appli-

\[93\] F. Altché, X. Qian, and A. D. L. Fortelle, ‘‘Least restrictive and minimally cations at intersections,’’ in *Proc. 15th Int. IEEE Conf. Intell. Transp. *

deviating supervisor for safe semi-autonomous driving at an intersection: *Syst. \(ITSC\)*, Sep. 2012, pp. 1178–1183. 

An MIQP approach,’’ in *Proc. IEEE 19th Int. Conf. Intell. Transp. Syst. *

*\(ITSC\)*, Nov. 2016, pp. 2520–2526. 

\[115\] G. R. de Campos, A. H. Runarsson, F. Granum, P. Falcone, and

\[94\] Y. Jiang, M. Zanon, R. Hult, and B. Houska, ‘‘Distributed algo-K. Alenljung, ‘‘Collision avoidance at intersections: A probabilistic rithm for optimal vehicle coordination at traffic intersections,’’ *IFAC-threat-assessment and decision-making system for safety interventions,’’*
* 
PapersOnLine, vol. 50, no. 1, pp. 11577–11582, 2017. 

in Proc. 17th Int. IEEE Conf. Intell. Transp. Syst. \(ITSC\), Oct. 2014, 

\[95\] N. Murgovski, G. R. de Campos, and J. Sjoberg, ‘‘Convex modeling pp. 8–11. 

of conflict resolution at traffic intersections,’’ in Proc. 54th IEEE Conf. 

\[116\] Y. Wang, E. Wenjuan, D. Tian, G. Lu, G. Yu, and Y. Wang, ‘‘Vehicle Decis. Control \(CDC\), Dec. 2015, pp. 4708–4713. 

collision warning system and collision detection algorithm based on

\[96\] A. A. Malikopoulos and L. Zhao, ‘‘A closed-form analytical solution vehicle infrastructure integration,’’ in Proc. 7th Adv. Forum Transp. China for optimal coordination of connected and automated vehicles,’’ in Proc. 

\(AFTC\), 2011, pp. 216–220. 

Amer. Control Conf. \(ACC\), Jul. 2019, pp. 3599–3604. 

\[117\] J. Wang, X. Xue, R. Chai, and N. Cao, ‘‘A temporal-spatial collision

\[97\] J. Shi, Y. Zheng, Y. Jiang, M. Zanon, R. Hult, and B. Houskal, ‘‘Dis-warning method at non-signalized intersection,’’ Proc. Eng. , vol. 137, tributed control algorithm for vehicle coordination at traffic intersec-pp. 827–835, Jan. 2016. 

tions,’’ in Proc. Eur. Control Conf. \(ECC\), Jun. 2018, pp. 1166–1171. 

\[118\] P. Wang, S. Fang, L. Zhang, and J. Wang, ‘‘A vehicle collision detection

\[98\] J. Yua and L. Petngab, ‘‘Space-based collision avoidance framework algorithm at T-shaped intersections based on location-based service,’’ in for autonomous vehicles,’’ Proc. Comput. Sci. , vol. 140, pp. 37–45, Proc. New Frontiers Road Airport Eng. , Oct. 2015, pp. 308–317. 

Jan. 2018. 

\[119\] P. Wang, L. Zhang, and S. Fang, ‘‘Trajectory prediction for left-turn
*
*\[99\] M. Nekoui, D. Ni, H. P. Nik, R. Prasad, M. R. Kanjee, H. Zhu, and vehicles at T-shaped intersections based on location based service,’’ in T. Nguyen, ‘‘Development of a VII-enabled prototype intersection col-Proc. Int. Conf. Transp. Inf. Saf. \(ICTIS\)*, Jun. 2015, pp. 29–33. 

lision warning system,’’ *Int. J. Internet Protocol Technol. *, vol. 4, no. 3, 

\[120\] O. Kwon, S.-H. Lee, J.-S. Kim, M.-S. Kim, and K.-J. Li, ‘‘Collision p. 173, 2009. 

prediction at intersection in sensor network environment,’’ in *Proc. IEEE*

\[100\] Y. Fu, C. Li, B. Xia, W. Dong, Y. Duan, and L. Xiong, ‘‘A novel *Intell. Transp. Syst. Conf. *, Sep. 2006, pp. 982–987. 

warning/avoidance algorithm for intersection collision based on dynamic

\[121\] F. D. Salim, L. Cai, M. Indrawan, and S. W. Loke, ‘‘Road intersections Bayesian networks,’’ in *Proc. IEEE Int. Conf. Commun. \(ICC\)*, May 2016, as pervasive computing environments: Towards a multiagent real-time pp. 1–6. 

collision warning system,’’ in *Proc. 6th Annu. IEEE Int. Conf. Pervasive*

\[101\] S. Joerer, M. Segata, B. Bloessl, R. L. Cigno, C. Sommer, and F. Dressler, *Comput. Commun. \(PerCom\)*, Mar. 2008, pp. 621–626. 

‘‘To crash or not to crash: Estimating its likelihood and potentials of

\[122\] R. Miller and Q. Huang, ‘‘An adaptive peer-to-peer collision warning beacon-based IVC systems,’’ in *Proc. IEEE Veh. Netw. Conf. \(VNC\)*, system,’’ in *Proc. IEEE 55th Veh. Technol. Conf. \(VTC Spring\)*, Oct. 2002, Nov. 2012, pp. 25–32. 

pp. 317–321. 

\[102\] S. Joerer, M. Segata, B. Bloessl, R. Lo Cigno, C. Sommer, and F. Dressler, 

\[123\] Y.-Y. Wang and H.-Y. Wei, ‘‘Road capacity and throughput for safe

‘‘A vehicular networking perspective on estimating vehicle collision driving autonomous vehicles,’’ *IEEE Access*, vol. 8, pp. 95779–95792, probability at intersections,’’ *IEEE Trans. Veh. Technol. *, vol. 63, no. 4, 2020. 

pp. 1802–1812, May 2014. 

\[124\] H. Suzuki, H. Murata, and K. Araki, ‘‘Performance of inter-vehicle

\[103\] M. Baek, D. Jeong, D. Choi, and S. Lee, ‘‘Vehicle trajectory prediction communication technique for intersection collision warning,’’ in *Proc. 5th* and collision warning via fusion of multisensors and wireless vehicular *Int. Conf. Inf. Commun. Signal Process. *, Dec. 2005, pp. 603–606. 

communications,’’ *Sensors*, vol. 20, no. 1, p. 288, Jan. 2020. 

\[104\] S. B. Raut, P. R. Bajaj, and L. G. Malik, ‘‘Prediction of vehicle collision

\[125\] J. Ibanez-Guzman, S. Lefevre, A. Mokkadem, and S. Rodhaim, ‘‘Vehi-probablity at intersection using V2 V communication,’’ *Int. J. Sci. Eng. *

cle to vehicle communications applied to road intersection safety, field *Res. *, vol. 6, no. 5, pp. 1–6, May 2015. 

results,’’ in *Proc. 13th Int. IEEE Conf. Intell. Transp. Syst. *, Sep. 2010, 

\[105\] Y. Fu, C. Li, T. H. Luan, Y. Zhang, and G. Mao, ‘‘Infrastructure-pp. 192–197. 

cooperative algorithm for effective intersection collision avoidance,’’

\[126\] H. Cho and B. Kim, ‘‘Cooperative intersection collision-warning system *Transp. Res. C, Emerg. Technol. *, vol. 89, pp. 188–204, Apr. 2018. 

based on vehicle-to-vehicle communication,’’ *Contemp. Eng. Sci. *, vol. 7, 

\[106\] X. Xia, Z. Ding, Y. Wang, and W. Kong, ‘‘Vehicle collision warning algo-no. 22, pp. 1147–1154, 2014. 

rithms implemented in VANET communication terminals,’’ in *Proc. Int. *

\[127\] C.-M. Huang and S.-Y. Lin, ‘‘Cooperative vehicle collision warning *Conf. Wireless Commun., Signal Process. Netw. \(WiSPNET\)*, Mar. 2017, system using the vector-based approach with dedicated short range com-pp. 2323–2328. 

munication data transmission,’’ *IET Intell. Transp. Syst. *, vol. 8, no. 2, 

\[107\] R. Zeng, W. Sheng, and D. Yang, ‘‘Collision probability computa-pp. 124–134, Mar. 2014. 

tion based on vehicle to vehicle communication,’’ in *Proc. IEEE Int. *

\[128\] A. Colombo and H. Wymeersch, ‘‘Cooperative intersection collision *Conf. Cyber Technol. Autom., Control, Intell. Syst. \(CYBER\)*, Jun. 2015, avoidance in a constrained communication environment,’’ in *Proc. IEEE*

pp. 8–12. 

*18th Int. Conf. Intell. Transp. Syst. *, Sep. 2015, pp. 375–380. 

7966

VOLUME 10, 2022



A. Gholamhosseinian, J. Seitz: Comprehensive Survey on Cooperative IM for Heterogeneous CVs

\[129\] F. Basma, Y. Tachwali, and H. H. Refai, ‘‘Intersection collision avoidance

\[152\] J. Wu, A. Abbas-Turki, and A. El Moudni, ‘‘Cooperative driving: An ant system using infrastructure communication,’’ in *Proc. 14th Int. IEEE*

colony system for autonomous intersection management,’’ *Appl. Intell. *, *Conf. Intell. Transp. Syst. \(ITSC\)*, Oct. 2011, pp. 422–427. 

vol. 37, no. 2, pp. 207–222, 2012. 

\[130\] A. Kaadan and H. H. Refai, ‘‘IICAS: Intelligent intersection collision

\[153\] X. Wei, G. Z. Tan, and N. Ding, ‘‘Batch-light: An adaptive intelligent avoidance system,’’ in *Proc. 15th Int. IEEE Conf. Intell. Transp. Syst. *, intersection control policy for autonomous vehicles,’’ in *Proc. IEEE Int. *

Sep. 2012, pp. 16–19. 

*Conf. Prog. Inform. Comput. *, May 2014, pp. 98–103. 

\[131\] T. Ghoul and T. Sayed, ‘‘Real-time safety optimization of connected vehi-

\[154\] F. Perronnet, A. Abbas-Turki, and A. El Moudni, ‘‘Vehicle routing cle trajectories using reinforcement learning,’’ *Sensors*, vol. 21, no. 11, through deadlock-free policy for cooperative traffic control in a network p. 3864, Jun. 2021. 

of intersections: Reservation and congestion,’’ in *Proc. 17th Int. IEEE*

\[132\] M. Malinverno, G. Avino, C. Casetti, C. F. Chiasserini, F. Malandrino, and *Conf. Intell. Transp. Syst. \(ITSC\)*, Oct. 2014, pp. 2233–2238. 

S. Scarpina, ‘‘Performance analysis of C-V2I-based automotive collision

\[155\] D. Carlino, S. D. Boyles, and P. Stone, ‘‘Auction-based autonomous avoidance,’’ in *Proc. IEEE 19th Int. Symp. ‘World Wireless, Mobile* intersection management,’’ in *Proc. 16th Int. IEEE Conf. Intell. Transp. *

*Multimedia Netw.’ \(WoWMoM\)*, Jun. 2018, pp. 1–9. 

*Syst. \(ITSC\)*, Oct. 2013, pp. 529–534. 

\[133\] X. Wang, J. Li, C. Zhang, and T. Z. Qiu, ‘‘Active warning system

\[156\] C. Wuthishuwong and A. Traechtler, ‘‘Consensus-based local information for highway-rail grade crossings using connected vehicle technologies,’’

coordination for the networked control of the autonomous intersection *J. Adv. Transp. *, vol. 2019, Feb. 2019, Art. no. 3219387. 

management,’’ *Complex Intell. Syst. *, vol. 3, no. 1, pp. 17–32, Mar. 2017. 

\[134\] J. Choi, V. Marojevic, A. Sharma, B. Zewede, R. Nealy, C. R. Anderson, 

\[157\] S. I. Guler, M. Menendez, and L. Meier, ‘‘Using connected vehicle J. Withers, and C. B. Dietrich, ‘‘Measurement and configuration of DSRC

technology to improve the efficiency of intersections,’’ *Transp. Res. C,* radios for vehicle-to-train \(V2T\) safety-critical communications,’’ *IEEE*

*Emerg. Technol. *, vol. 46, pp. 121–131, Sep. 2014. 

*Wireless Commun. Lett. *, vol. 7, no. 3, pp. 428–431, Jun. 2018. 

\[158\] C. Philippe, L. Adouane, A. Tsourdos, H.-S. Shin, and B. Thuilot, 

\[135\] J. Choi, V. Marojevic, C. B. Dietrich, and S. Ahn, ‘‘DSRC-enabled

‘‘Probability collectives algorithm applied to decentralized intersection train safety communication system at unmanned crossings,’’ 2021, coordination for connected autonomous vehicles,’’ in *Proc. IEEE Intell. *

*arXiv:2104.01727*. 

*Vehicles Symp. \(IV\)*, Jun. 2019, pp. 1928–1934. 

\[136\] J. Choi, V. Marojevic, and C. B. Dietrich, ‘‘Measurements and analysis

\[159\] L. D. Chou, J. H. Tseng, and J. Y. Yang, ‘‘Adaptive virtual traffic light of DSRC for V2T safety-critical communications,’’ in *Proc. IEEE 88th* based on vanets for mitigating congestion in smart city,’’ in *Proc. 3rd* *Veh. Technol. Conf. \(VTC-Fall\)*, Aug. 2018, pp. 1–5. 

*Int. Conf. Digital Inf. Commun. Technol. Appl. \(DICTAP\)*, Jul. 2013, 

\[137\] L. Doi, I. Herman, and Z. Hurák, ‘‘V2V communication-based rail pp. 40–44. 

collision avoidance system for urban light rail vehicles,’’ Jun. 2020, 

\[160\] M. Vasirani and S. Ossowski, ‘‘A computational market for distributed *arXiv:2006.02480*. 

control of urban road traffic systems,’’ *IEEE Trans. Intell. Transp. Syst. *, 

\[138\] H. Barkouk, E. M. En-Naimi, and A. Mahboub, ‘‘Overview of positive vol. 12, no. 2, pp. 313–321, Feb. 2011. 

train control \(PTC\) and railway collision avoidance system \(RCAS\),’’ in

\[161\] S. Vasirani and M. Ossowski, ‘‘A market-inspired approach for intersec-Proc. 2nd Int. Conf. Comput. Wireless Commun. Syst. \(ICCWCS\), 2017, tion management in urban road traffic networks,’’ *J. Artif. Intell. Res. *, pp. 1–6. 

vol. 43, pp. 621–659, Apr. 2012. 

\[139\] M. Mader, W. Munst, C. Dannheim, P. Sallis, N. Gay, B. Malnar, 

\[162\] W. ShangGuan, J. Yu, B. Cai, and J. Wang, ‘‘Research on unsigned M. Al-Mamun, and C. Icking, ‘‘A telemetry design for anticipating train-intersection control method based on cooperative vehicle infrastructure road crossing collisions,’’ in *Proc. 7th Int. Workshop Reliable Netw. *

system,’’ in *Proc. Chin. Autom. Congr. \(CAC\)*, Oct. 2017, pp. 6436–6441. 

*Design Modeling \(RNDM\)*, Oct. 2015, pp. 351–356. 

\[163\] F. Yan, M. Dridi, and A. El Moudni, ‘‘Autonomous vehicle sequencing

\[140\] M. Hartong, R. Goel, C. Farkas, and D. Wijesekera, ‘‘PTC-VANET inter-algorithm at isolated intersections,’’ in *Proc. 12th Int. IEEE Conf. Intell. *

actions to prevent highway rail intersection crossing accidents,’’ in *Proc. *

*Transp. Syst. *, Oct. 2009, pp. 1–6. 

*IEEE 65th Veh. Technol. Conf. \(VTC-Spring\)*, Apr. 2007, pp. 2550–2554. 

\[164\] J. Wu, A. Abbas-Turki, and A. E. Moudni, ‘‘Intersection traffic control by

\[141\] P. Wang and C. Chan, ‘‘Vehicle collision prediction at intersections based a novel scheduling model,’’ in *Proc. IEEE/INFORMS Int. Conf. Service* on comparison of minimal distance between vehicles and dynamic thresh-Oper., Logistics Inform. , Jul. 2009, pp. 329–334. 

olds,’’ *IET Intell. Transp. Syst. *, vol. 11, no. 10, pp. 676–684, Dec. 2017. 

\[165\] K. Zhang, A. D. L. Fortelle, D. Zhang, and X. Wu, ‘‘Analysis and mod-

\[142\] A. A. Malikopoulos and L. Zhao, ‘‘Decentralized optimal path planning eled design of one state-driven autonomous passing-through algorithm and coordination for connected and automated vehicles at signalized-free for driverless vehicles at intersections,’’ in *Proc. IEEE 16th Int. Conf. *

intersections,’’ *Mathematics*, vol. 3, pp. 1–6, Sep. 2019. 

*Comput. Sci. Eng. *, Dec. 2013, pp. 751–757. 

\[143\] M. A. Ameddah, B. Das, and J. Almhana, ‘‘Priority based algorithm for

\[166\] K. Zhang, A. Yang, H. Su, A. de La Fortelle, K. Miao, and Y. Yao, traffic intersections streaming using VANET,’’ in *Proc. 14th Int. Wireless*

‘‘Service-oriented cooperation models and mechanisms for heteroge-Commun. Mobile Comput. Conf. \(IWCMC\), Jun. 2018, pp. 898–903. 

neous driverless vehicles at continuous static critical sections,’’ *IEEE*

\[144\] V. Gradinescu, C. Gorgorin, R. Diaconescu, V. Cristea, and L. Iftode, *Trans. Intell. Transp. Syst. *, vol. 18, no. 7, pp. 1867–1881, Jul. 2017. 

‘‘Adaptive traffic lights using car-to-car communication,’’ in *Proc. IEEE*

\[167\] T.-C. Au, N. Shahidi, and P. Stone, ‘‘Enforcing liveness in autonomous *65th Veh. Technol. Conf. \(VTC-Spring\)*, Apr. 2007, pp. 21–25. 

traffic management,’’ in *Proc. 25th AAAI Conf. Artif. Intell. *, vol. 2, 

\[145\] W. Wu, J. Zhang, A. Luo, and J. Cao, ‘‘Distributed mutual exclusion Aug. 2011, pp. 1317–1322. 

algorithms for intersection traffic control,’’ *IEEE Trans. Parallel Distrib. *

\[168\] S.-H. Lin and T.-Y. Ho, ‘‘Autonomous vehicle routing in multiple *Syst. *, vol. 26, no. 1, pp. 65–74, Jan. 2015. 

intersections,’’ in *Proc. 24th Asia South Pacific Design Autom. Conf. *, 

\[146\] T.-C. Au and P. Stone, ‘‘Motion planning algorithms for autonomous Jan. 2019, pp. 585–590. 

intersection management,’’ in *Bridging Gap Between Task Motion Plan-*

\[169\] M. Zhu, X. Li, H. Huang, L. Kong, M. Li, and M.-Y. Wu, ‘‘LICP: A look-ning. Palo Alto, CA, USA: AAAI Press, 2010, pp. 2–9. 

ahead intersection control policy with intelligent vehicles,’’ in *Proc. IEEE*

\[147\] K. M. Dresner, ‘‘Autonomous intersection management,’’ Ph.D. disser-6th Int. Conf. Mobile Adhoc Sensor Syst. , Oct. 2009, pp. 633–638. 

tation, Dept. Comput. Sci., Univ. Texas at Austin, Austin, TX, USA, 

\[170\] Z. Li, M. V. Chitturi, L. Yu, A. R. Bill, and D. A. Noyce, ‘‘Sustainability Dec. 2009. 

effects of next-generation intersection control for autonomous vehicles,’’

\[148\] K. Yang, S. I. Guler, and M. Menendez, ‘‘Isolated intersection control for *Transport*, vol. 30, no. 3, pp. 342–352, Oct. 2015. 

various levels of vehicle technology: Conventional, connected, and auto-

\[171\] J. Wu, A. Abbas-Turki, and A. El Moudni, ‘‘Discrete methods for mated vehicles,’’ *Transp. Res. C, Emerg. Techn. *, vol. 72, pp. 109–129, urban intersection traffic controlling,’’ in *Proc. IEEE 69th Veh. Technol. *

Nov. 2016. 

*Conf. \(VTC Spring\)*, Apr. 2009, pp. 1–5. 

\[149\] M. Al-qutwani and X. Wang, ‘‘Smart traffic lights over vehicular named

\[172\] F. Yan, M. Dridi, and A. El Moudni, ‘‘An autonomous vehicle sequencing data networking,’’ *Information*, vol. 10, no. 3, p. 83, Feb. 2019. 

problem at intersections: A genetic algorithm approach,’’ *Int. J. Appl. *

\[150\] Q. Wu, P. Zhi, Y. Wei, L. Zhang, J. Wu, Q. Zhou, Q. Zhou, and *Math. Comput. Sci. *, vol. 23, no. 1, pp. 183–200, 2013. 

P. Gao, ‘‘Communicate with traffic lights and vehicles based on multi-

\[173\] Y. Li and Q. Liu, ‘‘Intersection management for autonomous vehicles agent reinforcement learning,’’ in *Proc. IEEE 24th Int. Conf. Comput. *

with vehicle-to-infrastructure communication,’’ *PLoS ONE*, vol. 15, no. 7, *Supported Cooperat. Work Design \(CSCWD\)*, May 2021, pp. 843–848. 

Jul. 2020, Art. no. e0235644. 

\[151\] J. Qiao, D. Zhang, and D. de Jonge, ‘‘Virtual roundabout protocol for

\[174\] M. Rapelli, C. Casetti, and M. Sgarbi, ‘‘A distributed V2 V-based virtual autonomous vehicles,’’ in *Proc. Australas. Joint Conf. Artif. Intell. *, 2018, traffic light system,’’ in *Proc. Int. Conf. Commun. Syst. Netw. \(COM-pp. 773–782. *
* 
SNETS\), Jan. 2020, pp. 122–128. 

VOLUME 10, 2022

7967



A. Gholamhosseinian, J. Seitz: Comprehensive Survey on Cooperative IM for Heterogeneous CVs

\[175\] J. Gregoire, S. Bonnabel, and A. de La Fortelle, ‘‘Priority-based coordi-

\[196\] F. Belkhouche, ‘‘Collaboration and optimal conflict resolution at an nation of robots,’’ in Proc. HAL, 2014, pp. 1–21. 

unsignalized intersection,’’ IEEE Trans. Intell. Transp. Syst. , vol. 20, 

\[176\] H. Ghaffarian, M. Fathy, and M. Soryani, ‘‘Vehicular ad hoc networks no. 6, pp. 2301–2312, Jun. 2019. 

enabled traffic controller for removing traffic lights in isolated intersec-

\[197\] R. Tachet, P. Santi, S. Sobolevsky, L. I. Reyes-Castro, E. Frazzoli, tions based on integer linear programming,’’ IET Intell. Transport Syst. , D. Helbing, and C. Ratti, ‘‘Revisiting street intersections using slot-based vol. 6, no. 2, pp. 115–123, Jun. 2012. 

systems,’’ PLoS ONE, vol. 11, no. 3, Mar. 2016, Art. no. e0149607. 

\[177\] F. Perronnet, A. Abbas-Turki, J. Buisson, A. El Moudni, R. Zéo, and
*
*\[198\] M. Choi, A. Rubenecia, and H. H. Choi, ‘‘Reservation-based traffic man-M. Ahmane, ‘‘Cooperative intersection management: Real implementa-agement for autonomous intersection crossing,’’ Int. J. Distrib. Sensor tion and feasibility study of a sequence based protocol for urban appli-Netw. *, vol. 15, no. 12, 2019, Art. no. 1550147719895956. 

cations,’’ in *Proc. 15th Int. IEEE Conf. Intell. Transp. Syst. *, Sep. 2012, 

\[199\] M. Elhadef, ‘‘An adaptable inVANETs-based intersection traffic control pp. 42–47. 

algorithm,’’ in *Proc. IEEE Int. Conf. Comput. Inf. Technol.; Ubiquitous*

\[178\] F. Perronnet, A. Abbas-Turki, and A. El Moudni, ‘‘A sequenced-based *Comput. Commun.; Dependable, Autonomic Secure Comput.; Pervasive* protocol to manage autonomous vehicles at isolated intersections,’’ in *Intell. Comput. *, Oct. 2015, pp. 2387–2392. 

*Proc. 16th Int. IEEE Conf. Intell. Transp. Syst. \(ITSC\)*, Oct. 2013, 

\[200\] D. Fajardo, T.-C. Au, S. T. Waller, P. Stone, and D. Yang, ‘‘Automated pp. 1811–1816. 

intersection control: Performance of future innovation versus current

\[179\] J. Wu, F. Perronnet, and A. Abbas-Turki, ‘‘Cooperative vehicle-actuator traffic signal control,’’ *Transp. Res. Rec., J. Transp. Res. Board*, vol. 2259, system: A sequence-based framework of cooperative intersections man-pp. 223–232, Jan. 2011. 

agement,’’ *IET Intell. Transp. Syst. *, vol. 8, no. 4, pp. 352–360, Jun. 2014. 

\[201\] M. V. Middlesworth, K. Dresner, and P. Stone, ‘‘Replacing the stop

\[180\] S. Azimi, G. Bhatia, R. Rajkumar, and P. Mudalige, ‘‘Vehicular networks sign: Unmanaged intersection control for autonomous vehicles,’’ in *Proc. *

for collision avoidance at intersections,’’ *SAE Int. J. Passenger Cars-7th Int. Joint Conf. Auton. Agents Multiagent Syst. \(AAMAS\)*, vol. 3, *Mech. Syst. *, vol. 4, no. 1, pp. 406–416, 2011. 

May 2008, pp. 1–4. 

\[181\] R. Azimi, G. Bhatia, R. Rajkumar, and P. Mudalige, ‘‘Intersection

\[202\] K. Dresner and P. Stone, ‘‘Multiagent traffic management: An improved management using vehicular networks,’’ SAE, Warrendale, PA, USA, intersection control mechanism,’’ in *Proc. 4th Int. Joint Conf. Auton. *

Tech. Rep. 2012-01-0292, Apr. 2012. 

*Agents Multiagent Syst. \(AAMAS\)*, Jul. 2005, pp. 471–477. 

\[182\] R. Azimi, G. Bhatia, R. Rajkumar, and P. Mudalige, ‘‘V2 V-intersection

\[203\] K. Dresner and P. Stone, ‘‘Multiagent traffic management: A reservation-management at roundabouts,’’ *SAE Int. J. Passenger Cars-Mech. Syst. *, based intersection control mechanism,’’ in *Proc. 3rd Int. Joint Conf. Auto. *

vol. 6, no. 2, pp. 681–690, Apr. 2013. 

*Agents Multiagent Syst. *, vol. 2, 2004, pp. 530–537. 

\[183\] S. R. Azimi, G. Bhatia, R. Rajkumar, and P. Mudalige, ‘‘Reliable inter-

\[204\] S. Adams and M. J. Rutherford, ‘‘Towards decentralized waypoint negoti-section protocols using vehicular networks,’’ in *Proc. ACM/IEEE 4th Int. *

ation,’’ Multiagent Pathfinding AAAI, Dept. Comput. Sci., Univ. Denver, *Conf. Cyber-Physical Syst. \(ICCPS\)*, Apr. 2013, pp. 1–10. 

Denver, CO, USA, Tech. Rep. WS-12-10, 2012, pp. 2–5. 

\[184\] C.-L. Fok, M. Hanna, S. Gee, T.-C. Au, P. Stone, C. Julien, and S. Vish-

\[205\] G. Chen and K.-D. Kang, ‘‘Win-fit: Efficient intersection management via wanath, ‘‘A platform for evaluating autonomous intersection management dynamic vehicle batching and scheduling,’’ in *Proc. Int. Conf. Connected* policies,’’ in *Proc. IEEE/ACM 3rd Int. Conf. Cyber-Phys. Syst. *, Apr. 2012, *Vehicles Expo \(ICCVE\)*, Oct. 2015, pp. 263–270. 

pp. 87–96. 

\[206\] S. Aoki and R. R. Rajkumar, ‘‘A configurable synchronous intersection

\[185\] M. Quinlan, T.-C. Au, J. Zhu, N. Stiurca, and P. Stone, ‘‘Bringing simula-protocol for self-driving vehicles,’’ in *Proc. IEEE 23rd Int. Conf. Embed-tion to life: A mixed reality autonomous intersection,’’ in Proc. IEEE/RSJ*
* 
ded Real-Time Comput. Syst. Appl. \(RTCSA\), Aug. 2017, pp. 1–11. 

Int. Conf. Intell. Robots Syst. , Oct. 2010, pp. 6083–6088. 

\[207\] S. Aoki and R. Rajkumar, ‘‘CSIP: A synchronous protocol for automated

\[186\] M. Ahmane, A. Abbas-Turkia, F. Perronnet, J. Wub, A. ElMoudni, vehicles at road intersections,’’ ACM Trans. Cyber-Phys. Syst. , vol. 3, J. Buisson, and R. Zeo, ‘‘Modeling and controlling an isolated urban no. 3, p. 25, Jun. 2019. 

intersection based on cooperative vehicles,’’ Transp. Res. C, Emerg. 

\[208\] M. Elhenawy, A. A. Elbery, A. A. Hassan, and H. A. Rakha, ‘‘An Technol. , vol. 28, pp. 44–62, Mar. 2013. 

intersection game-theory-based traffic control algorithm in a connected

\[187\] J. Karlsson, J. Sjöberg, N. Murgovski, L. Hanning, S. Luu, V. Olsson, vehicle environment,’’ in Proc. IEEE 18th Int. Conf. Intell. Transp. Syst. , and A. Rasch, ‘‘Intersection crossing with reduced number of con-Sep. 2015, pp. 343–347. 

flicts,’’ in Proc. 21st Int. Conf. Intell. Transp. Syst. \(ITSC\), Nov. 2018, 

\[209\] I. H. Zohdy and H. Rakha, ‘‘Game theory algorithm for intersection-based pp. 1993–1999. 

cooperative adaptive cruise control \(CACC\) systems,’’ in Proc. 15th Int. 

\[188\] M. Kloock, P. Scheffe, S. Marquardt, J. Maczijewski, B. Alrifaee, and IEEE Conf. Intell. Transp. Syst. , Sep. 2012, pp. 1097–1102. 

S. Kowalewski, ‘‘Distributed model predictive intersection control of

\[210\] V. Savic, E. M. Schiller, and M. Papatriantafilou, ‘‘Distributed algorithm multiple vehicles,’’ in Proc. IEEE Intell. Transp. Syst. Conf. \(ITSC\), for collision avoidance at road intersections in the presence of commu-Oct. 2019, pp. 1735–1740. 

nication failures,’’ in Proc. IEEE Intell. Vehicles Symp. \(IV\), Jun. 2017, 

\[189\] Z. Li, Q. Wu, H. Yu, C. Chen, G. Zhang, Z. Z. Tian, and P. D. Prevedouros, pp. 1005–1012. 

‘‘Temporal-spatial dimension extension-based intersection control for-

\[211\] M. M. Abdelhameed, M. Abdelaziz, S. Hammad, and O. M. Shehata, mulation for connected and autonomous vehicle systems,’’ Transp. Res. 

‘‘A hybrid fuzzy-genetic controller for a multi-agent intersection control C, Emerg. Technol. , vol. 104, pp. 234–248, Jul. 2019. 

system,’’ in Proc. Int. Conf. Eng. Technol. \(ICET\), Apr. 2014, pp. 1–6. 

\[190\] F. Zhu and S. V. Ukkusuri, ‘‘A linear programming formulation for

\[212\] Y. Chang and P. Edara, ‘‘AReBIC: Autonomous reservation-based inter-autonomous intersection control within a dynamic traffic assignment section control for emergency evacuation,’’ in Proc. IEEE Intell. Vehicles and connected vehicle environment,’’ Transp. Res. C, Emerg. Technol. , Symp. \(IV\), Jun. 2017, pp. 1887–1892. 

vol. 55, pp. 363–378, Jun. 2015. 

\[213\] E. R. Müller, R. C. Carlson, and W. K. Junior, ‘‘Intersection control

\[191\] R. W. Timmerman and M. A. A. Boon, ‘‘Platoon forming algorithms for for automated vehicles with MILP,’’ IFAC-PapersOnLine, vol. 49, no. 3, intelligent street intersections,’’ Transportmetrica A: Transp. Sci. , vol. 17, pp. 37–42, 2016. 

no. 3, pp. 278–307, Nov. 2019. 

\[214\] L. Chai, B. Cai, W. ShangGuan, and J. Wang, ‘‘Connected and

\[192\] M. A. Guney and I. A. Raptis, ‘‘Scheduling-based optimization for autonomous vehicles coordinating method at intersection utilizing pre-motion coordination of autonomous vehicles at multilane intersections,’’

assigned slots,’’ in Proc. IEEE 20th Int. Conf. Intell. Transp. Syst. \(ITSC\), J. Robot. , vol. 2020, Mar. 2020, Art. no. 6217409. 

Oct. 2017, pp. 1–6. 

\[193\] H. Xu, Y. Zhang, L. Li, and W. Li, ‘‘Cooperative driving at unsignalized

\[215\] M. A. S. Kamal, J. Imura, A. Ohata, T. Hayakawa, and K. Aihara, intersections using tree search,’’ IEEE Trans. Intell. Transp. Syst. , vol. 21, 

‘‘Coordination of automated vehicles at a traffic-lightless intersection,’’

no. 11, pp. 4563–4571, Nov. 2020. 

in Proc. 16th Int. IEEE Conf. Intell. Transp. Syst. \(ITSC\), Oct. 2013, 

\[194\] N. Buckman, A. Pierson, W. Schwarting, S. Karaman, and D. Rus, ‘‘Shar-pp. 922–927. 

ing is caring: Socially-compliant autonomous intersection negotiation,’’

\[216\] K. Kim, ‘‘Collision free autonomous ground traffic: A model predictive in Proc. IEEE/RSJ Int. Conf. Intell. Robots Syst. \(IROS\), Nov. 2019, control approach,’’ in Proc. ACM/IEEE 4th Int. Conf. Cyber-Phys. Syst. , pp. 6136–6143. 

Apr. 2013, pp. 51–60. 

\[195\] A. Stevanovic and N. Mitrovic, ‘‘Combined alternate-direction lane

\[217\] A. Katriniok, P. Kleibaum, C. Ress, and L. Eckstein, ‘‘Automation of road assignment and reservation-based intersection control,’’ in Proc. 21st Int. 

vehicles using V2X: An application to intersection automation,’’ SAE

Conf. Intell. Transp. Syst. \(ITSC\), Nov. 2018, pp. 14–19. 

Tech. Paper 2017-01-0078, 2017. 

7968

VOLUME 10, 2022



A. Gholamhosseinian, J. Seitz: Comprehensive Survey on Cooperative IM for Heterogeneous CVs

\[218\] I. Lamouik, A. Yahyaouy, and M. A. Sabri, ‘‘Smart multi-agent traffic

\[240\] Z. He, L. Zheng, L. Lu, and W. Guan, ‘‘Erasing lane changes from roads: coordinator for autonomous vehicles at intersections,’’ in Proc. Int. Conf. 

A design of future road intersections,’’ IEEE Trans. Intell. Vehicles, vol. 3, Adv. Technol. Signal Image Process. \(ATSIP\), May 2017, pp. 1–6. 

no. 2, pp. 173–184, Jun. 2018. 

\[219\] G. R. D. Campos, P. Falcone, R. Hult, H. Wymeersch, and J. Sjöberg, 

\[241\] Y. Xu, H. Zhou, B. Qian, H. Wu, Z. Zhang, and X. S. Shen, ‘‘When

‘‘Traffic coordination at road intersections: Autonomous decision-automated vehicles meet non-signalized intersections: A collision-free making algorithms using model-based heuristics,’’ IEEE Intell. Transp. 

scheduling solution,’’ in Proc. IEEE/CIC Int. Conf. Commun. China Syst. Mag. , vol. 9, no. 1, pp. 8–21, Spring 2017. 

\(ICCC\), Aug. 2018, pp. 709–713. 

\[220\] Z.-h. Fan, H.-b. Li, W. Huang, and Y.-T. Tian, ‘‘District control

\[242\] S. Aoki and R. Rajkumar, ‘‘Dynamic intersections and self-driving vehi-strategy for vehicle collision avoidance based on hybrid automaton cles,’’ in Proc. ACM/IEEE 9th Int. Conf. Cyber-Physical Syst. \(ICCPS\), model,’’ in Proc. 11th World Congr. Intell. Control Autom. , Jun. 2014, Apr. 2018, pp. 320–330. 

pp. 5378–5383. 

\[243\] A. Katriniok, S. Kojchev, E. Lefeber, and H. Nijmeijer, ‘‘Distributed

\[221\] B. Zheng, C. Lin, H. Liang, S. Shiraishi, W. Li, and Q. Zhu, ‘‘Delay-aware scenario model predictive control for driver aided intersection crossing,’’

design, analysis and verification of intelligent intersection management,’’

in Proc. Eur. Control Conf. \(ECC\), Jun. 2018, pp. 1746–1752. 

in Proc. IEEE Int. Conf. Smart Comput. \(SMARTCOMP\), May 2017, 

\[244\] A. Katriniok, P. Sopasakis, M. Schuurmans, and P. Patrinos, ‘‘Nonlinear pp. 1–8. 

model predictive control for distributed motion planning in road intersec-

\[222\] J. Gregoire and E. Frazzoli, ‘‘Hybrid centralized/distributed autonomous tions using PANOC,’’ in Proc. IEEE 58th Conf. Decis. Control \(CDC\), intersection control: Using a job scheduler as a planner and inheriting its Dec. 2019, pp. 5272–5278. 

efficiency guarantees,’’ in Proc. IEEE 55th Conf. Decis. Control \(CDC\), 

\[245\] Y. Feng, C. Yu, and H. X. Liu, ‘‘Spatiotemporal intersection control in a Dec. 2016, pp. 2549–2554. 

connected and automated vehicle environment,’’ Transp. Res. C, Emerg. 

\[223\] K. Zhang, A. Yang, H. Su, A. De La Fortelle, and X. Wu, ‘‘Unified Technol. , vol. 89, pp. 364–383, Apr. 2019. 

modeling and design of reservation-based cooperation mechanisms for

\[246\] R. Azimi, G. Bhatia, R. Rajkumar, and P. Mudalige, ‘‘Ballroom inter-intelligent vehicles,’’ in Proc. IEEE 19th Int. Conf. Intell. Transp. Syst. 

section protocol: Synchronous autonomous driving at intersections,’’ in \(ITSC\), Nov. 2016, pp. 1192–1199. 

Proc. IEEE 21st Int. Conf. Embedded Real-Time Comput. Syst. Appl. , 

\[224\] N. Aloufi and A. Chatterjee, ‘‘Autonomous vehicle scheduling at inter-Aug. 2015, pp. 167–175. 

sections based on production line technique,’’ in Proc. IEEE 88th Veh. 
*
*\[247\] B. Qian, H. Zhou, F. Lyu, J. Li, T. Ma, and F. Hou, ‘‘Toward collision-Technol. Conf. \(VTC-Fall\)*, Aug. 2018, pp. 1–5. 

free and efficient coordination for automated vehicles at unsignalized

\[225\] A. P. Chouhan and G. Banda, ‘‘Autonomous intersection management: intersection,’’ *IEEE Internet Things J. *, vol. 6, no. 6, pp. 10408–10420, A heuristic approach,’’ *IEEE Access*, vol. 6, pp. 53287–53295, 2018. 

Dec. 2019. 

\[226\] F. Creemers, A. I. M. Medina, E. Lefeber, and N. V. de Wouw, ‘‘Design of

\[248\] Q. Lu and K.-D. Kim, ‘‘Intelligent intersection management of a supervisory controller for cooperative intersection control using model autonomous traffic using discrete-time occupancies trajectory,’’ *J. Traffic* predictive control,’’ *IFAC-PapersOnLine*, vol. 51, no. 33, pp. 74–79, *Logistics Eng. *, vol. 4, no. 1, pp. 1–6, 2016. 

2018. 

\[249\] B. Yang and C. Monterola, ‘‘A simple distributed algorithm for lightless

\[227\] C. Liu, C. Lin, S. Shiraishi, and M. Tomizuka, ‘‘Distributed conflict intersection control based on non-linear interactions between vehicles,’’

resolution for connected autonomous vehicles,’’ *IEEE Trans. Intell. Veh. *, in *Proc. IEEE 20th Int. Conf. Intell. Transp. Syst. \(ITSC\)*, Oct. 2017, vol. 3, no. 1, pp. 18–29, Mar. 2018. 

pp. 1–6. 

\[228\] Q. Lu and K.-D. Kim, ‘‘A mixed integer programming approach for

\[250\] C. Englund, L. Chen, and A. Voronov, ‘‘Cooperative speed harmoniza-autonomous and connected intersection crossing traffic control,’’ in *Proc. *

tion for efficient road utilization,’’ in *Proc. 7th Int. Workshop Commun. *

*IEEE 88th Veh. Technol. Conf. \(VTC-Fall\)*, Aug. 2018, pp. 1–6. 

*Technol. Vehicles \(Nets4Cars-Fall\)*, Oct. 2014, pp. 19–23. 

\[229\] Q. Lu and K.-D. Kim, ‘‘Autonomous and connected intersection crossing

\[251\] C. Bian, G. Yin, L. Xu, and N. Zhang, ‘‘Virtual belt algorithm for the traffic management using discrete-time occupancies trajectory,’’ *Appl. *

management of isolated autonomous intersection,’’ *Algorithms*, vol. 11, *Intell. *, vol. 49, no. 5, pp. 1621–1635, 2019. 

no. 11, p. 183, Nov. 2018. 

\[230\] Y. Mo, M. Wang, T. Zhang, and Q. Zhang, ‘‘Autonomous cooperative

\[252\] M. M. Abdelhameed, M. Abdelaziz, S. Hammad, and O. M. Shehata, vehicle coordination at road intersections,’’ in *Proc. IEEE Int. Conf. *

‘‘Development and evaluation of a multi-agent autonomous vehicles *Commun. Syst. \(ICCS\)*, Dec. 2018, pp. 192–197. 

intersection control system,’’ in *Proc. Int. Conf. Eng. Technol. \(ICET\)*, 

\[231\] E. Steinmetzl, R. Hult, Z. Zou, R. Emardson, F. Brännsträm, Apr. 2014, pp. 1–6. 

P. Falcone, and H. Wymeersch, ‘‘Collision-aware communication for intersection management of automated vehicles,’’ *IEEE Access*, vol. 6, 

\[253\] J. Zhang, X. Jiang, Z. Liu, L. Zheng, and B. Ran, ‘‘A study on pp. 77359–77371, 2018. 

autonomous intersection management: Planning-based strategy improved

\[232\] M. Wang, T. Zhang, L. Gao, and Q. Zhang, ‘‘High throughput dynamic by convolutional neural network,’’ *KSCE J. Civil Eng. *, vol. 25, no. 10, vehicle coordination for intersection ground traffic,’’ in *Proc. IEEE 88th* pp. 3995–4004, Jul. 2021. 

*Veh. Technol. Conf. \(VTC-Fall\)*, Aug. 2018, pp. 1–6. 

\[254\] G. Qian, M. Guo, L. Zhang, Y. Wang, S. Hu, and D. Wang, ‘‘Traffic

\[233\] H. Wei, L. Mashayekhy, and J. Papineau, ‘‘Intersection management for scheduling and control in fully connected and automated networks,’’

connected autonomous vehicles: A game theoretic framework,’’ in *Proc. *

*Transp. Res. C, Emerg. Technol. *, vol. 126, May 2021, Art. no. 103011. 

*21st Int. Conf. Intell. Transp. Syst. \(ITSC\)*, Nov. 2018, pp. 583–588. 

\[255\] M. Ma and Z. Li, ‘‘A time-independent trajectory optimization approach

\[234\] L. Cruz-Piris, M. A. Lopez-Carmona, and I. Marsa-Maestre, ‘‘Automated for connected and autonomous vehicles under reservation-based inter-optimization of intersections using a genetic algorithm,’’ *IEEE Access*, section control,’’ *Transp. Res. Interdiscipl. Perspect. *, vol. 9, Mar. 2021, vol. 7, pp. 15452–15468, 2019. 

Art. no. 100312. 

\[235\] C. L. Gonzalez, J. L. Zapotecatl, J. M. Alberola, V. Julian, and

\[256\] P. Worrawichaipat, E. Gerding, I. Kaparias, and S. Ramchurn, ‘‘Resilient C. Gershenson, ‘‘Distributed management of traffic intersections,’’ in intersection management with multi-vehicle collision avoidance,’’ *Fron-Proc. Ambient Intell.–Softw. Appl., 9th Int. Symp. Ambient Intell. *, *tiers Sustain. Cities*, vol. 3, Jun. 2021, Art. no. 670454. 

Nov. 2018, pp. 56–64. 

\[257\] D. Anadu, C. Mushagalusa, N. Alsbou, and A. S. A. Abuabed, ‘‘Internet

\[236\] B. Liu, Q. Shi, Z. Song, and A. El Kamel, ‘‘Trajectory planning for of Things: Vehicle collision detection and avoidance in a VANET envi-autonomous intersection management of connected vehicles,’’ *Simul. *

ronment,’’ in *Proc. IEEE Int. Instrum. Meas. Technol. Conf. \(I2MTC\)*, *Model. Pract. Theory*, vol. 90, pp. 16–30, Jan. 2019. 

May 2018, pp. 1–6. 

\[237\] Y. Wu, H. Chen, and F. Zhu, ‘‘DCL-AIM: Decentralized coordination

\[258\] M. Vieira, M. Vieira, P. Louro, and P. Vieira, ‘‘Crossroad management learning of autonomous intersection management for connected and auto-through visible light communication in cooperative vehicular systems,’’

mated vehicles,’’ *Transp. Res. C, Emerg. Technol. *, vol. 103, pp. 246–260, *Proc. SPIE*, vol. 11713, Mar. 2021, Art. no. 117130I. 

Jun. 2019. 

\[259\] H. Pei, Y. Zhang, Q. Tao, S. Feng, and L. Li, ‘‘Distributed cooperative

\[238\] A. Mirheli, M. Tajalli, L. Hajibabai, and A. Hajbabaie, ‘‘A consensus-driving in multi-intersection road networks,’’ *IEEE Trans. Veh. Technol. *, based distributed trajectory control in a signal-free intersection,’’ *Transp. *

vol. 70, no. 6, pp. 5390–5403, Jun. 2021. 

*Res. C, Emerg. Technol. *, vol. 100, pp. 161–176, Mar. 2019. 

\[260\] Y. Xu, H. Zhou, T. Ma, J. Zhao, B. Qian, and X. Shen, ‘‘Leveraging

\[239\] C. Wuthishuwong and A. Traechtler, ‘‘Vehicle to infrastructure based safe multiagent learning for automated vehicles scheduling at nonsignalized trajectory planning for autonomous intersection management,’’ in *Proc. *

intersections,’’ *IEEE Internet Things J. *, vol. 8, no. 14, pp. 11427–11439, *13th Int. Conf. ITS Telecommun. \(ITST\)*, Nov. 2013, pp. 175–180. 

Jul. 2021. 

VOLUME 10, 2022

7969



A. Gholamhosseinian, J. Seitz: Comprehensive Survey on Cooperative IM for Heterogeneous CVs

\[261\] T. T. Yu, T. M. Wynn, and M. Z. Oo, ‘‘Rules based intersection collision

\[282\] B. M. N. M. Hafzulazwan, ‘‘Optimal scheduling of connected and auto-avoidance system for V2X safety,’’ *Int. J. Adv. Sci. Res. Eng. *, vol. 5, mated vehicles at urban intersections via MILP,’’ in *Proc. Joint Conf. *

no. 10, pp. 211–220, 2019. 

*Autom. Control*, 2018, pp. 160–165. 

\[262\] N. C. Basjaruddin, D. H. Widyantoro, S. Ramadhan, and U. Z. Abidin, 

\[283\] C. Li and S. Shimamoto, ‘‘A real time traffic light control scheme for

‘‘Multi agent protocol for cooperative intersection collision avoidance reducing vehicles CO2 emissions,’’ in *Proc. IEEE Consum. Commun. *

system,’’ in *Proc. 7th Eng. Int. Conf. Educ., Concept Appl. Green Tech-Netw. Conf. \(CCNC\)*, Jan. 2011, pp. 855–859. 

*nol. *, 2018, pp. 335–340. 

\[284\] Q. Jin, G. Wu, K. Boriboonsomsin, and M. Barth, ‘‘Platoon-based multi-

\[263\] I. Elleuch, A. Makni, and R. Bouaziz, ‘‘Cooperative intersection collision agent intersection management for connected vehicle,’’ in *Proc. 16th Int. *

avoidance persistent system based on V2 V communication and real-IEEE Conf. Intell. Transp. Syst. \(ITSC\), Oct. 2013, pp. 1462–1467. 

time databases,’’ in *Proc. IEEE/ACS 14th Int. Conf. Comput. Syst. Appl. *

\[285\] L. Makarem and D. Gillet, ‘‘Decentralized coordination of autonomous *\(AICCSA\)*, Oct. 2017, pp. 1082–1089. 

vehicles at intersections,’’ *IFAC Proc. Volumes*, vol. 44, no. 1, 

\[264\] I. Pisa, G. Boquet, J. L. Vicario, A. Morell, and J. Serrano, ‘‘VAIMA: pp. 13046–13051, 2011. 

A V2 V based intersection traffic management algorithm,’’ in *Proc. 14th*

\[286\] L. Makarem and D. Gillet, ‘‘Fluent coordination of autonomous vehicles *Annu. Conf. Wireless-Demand Netw. Syst. Services \(WONS\)*, Feb. 2018, at intersections,’’ in *Proc. IEEE Int. Conf. Syst., Man, Cybern. \(SMC\)*, pp. 125–128. 

Oct. 2012, pp. 2557–2562. 

\[287\] L. Makarem and D. Gillet, ‘‘Information sharing among autonomous

\[265\] F. Molinari and J. Raisch, ‘‘Automation of road intersections using vehicles crossing an intersection,’’ in *Proc. IEEE Int. Conf. Syst., Man,* consensus-based auction algorithms,’’ in *Proc. Annu. Amer. Control Conf. *

*Cybern. \(SMC\)*, Oct. 2012, pp. 2563–2567. 

*\(ACC\)*, Jun. 2018, pp. 5994–6001. 

\[288\] M. A. S. Kamal, J.-I. Imura, T. Hayakawa, A. Ohata, and K. Aihara, 

\[266\] L.-C. Tung, J. Mena, M. Gerla, and C. Sommer, ‘‘A cluster based architec-

‘‘A vehicle-intersection coordination scheme for smooth flows of traffic ture for intersection collision avoidance using heterogeneous networks,’’

without using traffic lights,’’ *IEEE Trans. Intell. Transp. Syst. *, vol. 16, in *Proc. 12th Annu. Medit. Ad Hoc Netw. Workshop \(MED-HOC-NET\)*, no. 3, pp. 1136–1147, Jun. 2015. 

Jun. 2013, pp. 82–88. 

\[289\] B. V. Philip, T. Alpcan, J. Jin, and M. Palaniswami, ‘‘Distributed real-time

\[267\] Q. Lu and K.-D. Kim, ‘‘A genetic algorithm approach for expedited IoT for autonomous vehicles,’’ *IEEE Trans. Ind. Informat. *, vol. 15, no. 2, crossing of emergency vehicles in connected and autonomous intersection pp. 1131–1140, Feb. 2019. 

traffic,’’ *J. Adv. Transp. *, vol. 2017, Oct. 2017, Art. no. 7318917. 

\[290\] B. Xu, X. J. Ban, Y. Bian, W. Li, J. Wang, S. E. Li, and K. Li, ‘‘Cooperative

\[268\] A. Bazzi, A. Zanella, and B. M. Masini, ‘‘A distributed virtual traffic light method of traffic signal optimization and speed control of connected vehi-algorithm exploiting short range V2 V communications,’’ *Ad Hoc Netw. *, cles at isolated intersections,’’ *IEEE Trans. Intell. Transp. Syst. *, vol. 20, vol. 49, pp. 42–57, Oct. 2016. 

no. 4, pp. 1390–1403, Apr. 2019. 

\[269\] A. A. Hassan and H. A. Rakha, ‘‘A fully-distributed heuristic algorithm

\[291\] I. H. Zohdy and H. A. Rakha, ‘‘Intersection management via vehicle for control of autonomous vehicle movements at isolated intersections,’’

connectivity: The intersection cooperative adaptive cruise control system *Int. J. Transp. Sci. Technol. *, vol. 3, no. 4, pp. 297–309, Dec. 2014. 

concept,’’ *J. Intell. Transp. Syst.-Technol., Planning Oper. *, vol. 20, no. 1, 

\[270\] V. Milanes, J. Perez, E. Onieva, and C. Gonzalez, ‘‘Controller for urban pp. 17–32, Dec. 2014. 

intersections based on wireless communications and fuzzy logic,’’ *IEEE*

\[292\] Y. Zheng, L. Jin, Y. Jiang, F. Wang, X. Guan, S. Ji, and J. Xu, ‘‘Research *Trans. Intell. Transp. Syst. *, vol. 11, no. 1, pp. 243–248, Mar. 2010. 

on cooperative vehicle intersection control scheme without using traffic

\[271\] M. Ferreira and P. M. d’Orey, ‘‘On the impact of virtual traffic lights on lights under the connected vehicles environment,’’ *Adv. Mech. Eng. *, carbon emissions mitigation,’’ *IEEE Trans. Intell. Transp. Syst. *, vol. 13, vol. 9, no. 8, pp. 1–13, Aug. 2017. 

no. 1, pp. 284–295, Mar. 2012. 

\[293\] B. Chen, X. Pan, S. A. Evangelou, and S. Timotheou, ‘‘Optimal control for

\[272\] E. Regnath, M. Birkner, and S. Steinhorst, ‘‘CISCAV: Consensus-based connected and autonomous vehicles at signal-free intersections,’’ *IFAC-intersection scheduling for connected autonomous vehicles,’’ in Proc. *
* 
PapersOnLine, vol. 53, no. 2, pp. 15306–15311, 2020. 

IEEE Int. Conf. Omni-Layer Intell. Syst. \(COINS\), Aug. 2021, pp. 1–7. 

\[294\] F. Hacioğlu and M. T. Söylemez, ‘‘Power consumption based multi

\[273\] T. Wu, M. Jiang, and L. Zhang, ‘‘Cooperative multiagent deep determin-agent intersection management method,’’ in Proc. 10th Int. Conf. Elect. 
*
*istic policy gradient \(CoMADDPG\) for intelligent connected transporta-Electron. Eng. \(ELECO\)*, Nov./Dec. 2017, pp. 954–958. 

tion with unsignalized intersection,’’ *Math. Problems Eng. *, vol. 2020, 

\[295\] M. Tlig, O. Buffet, and O. Simonin, ‘‘Decentralized traffic management: Jul. 2020, Art. no. 1820527. 

A synchronization-based intersection control,’’ in *Proc. Int. Conf. Adv. *

\[274\] Y. Zheng, L. Jin, L. Gao, K. Li, Y. Wang, and F. Wang, ‘‘Development *Logistics Transp. \(ICALT\)*, May 2014, pp. 109–114. 

of a distributed cooperative vehicles control algorithm based on V2 V

\[296\] K. S. N. Ripon, J. Solaas, and H. Dissen, ‘‘Multi-objective evolutionary communication,’’ *Proc. Eng. *, vol. 137, pp. 649–658, Jan. 2016. 

optimization for autonomous intersection management,’’ in *Proc. 11th* *Asia–Pacific Conf. Simulated Evol. Learn. \(SEAL\)*, 2017, pp. 297–308. 

\[275\] Q. Jin, G. Wu, K. Boriboonsomsin, and M. Barth, ‘‘Multi-agent inter-

\[297\] A. Mirheli, L. Hajibabai, and A. Hajbabaie, ‘‘Development of a section management for connected vehicles using an optimal schedul-signal-head-free intersection control logic in a fully connected and ing approach,’’ in *Proc. Int. Conf. Connected Vehicles Expo \(ICCVE\)*, autonomous vehicle environment,’’ *Transp. Res. C, Emerg. Technol. *, Dec. 2012, pp. 185–190. 

vol. 92, pp. 412–425, Jul. 2018. 

\[276\] B. Xu, X. J. Ban, Y. Bian, J. Wang, and K. Li, ‘‘V2I based cooperation

\[298\] A. I. M. Medina, N. van de Wouw, and H. Nijmeijer, ‘‘Cooperative between traffic signal and approaching automated vehicles,’’ in *Proc. *

intersection control based on virtual platooning,’’ *IEEE Trans. Intell. *

*IEEE Intell. Vehicles Symp. \(IV\)*, Jun. 2017, pp. 1658–1664. 

*Transp. Syst. *, vol. 19, no. 6, pp. 1727–1740, Jun. 2018. 

\[277\] L. Zhao, A. Malikopoulos, and J. Rios-Torres, ‘‘Optimal control of

\[299\] Y. Zhang, A. A. Malikopoulos, and C. G. Cassandras, ‘‘Decentralized connected and automated vehicles at roundabouts: An investigation optimal control for connected automated vehicles at intersections includin a mixed-traffic environment,’’ *IFAC-PapersOnLine*, vol. 51, no. 9, ing left and right turns,’’ in *Proc. IEEE 56th Annu. Conf. Decis. Control* pp. 73–78, 2018. 

*\(CDC\)*, Dec. 2017, pp. 4428–4433. 

\[278\] Q. Jin, G. Wu, K. Boriboonsomsin, and M. Barth, ‘‘Advanced intersec-

\[300\] Y. J. Zhang, A. A. Malikopoulos, and C. G. Cassandras, ‘‘Optimal tion management for connected vehicles using a multi-agent systems control and coordination of connected and automated vehicles at urban approach,’’ in *Proc. IEEE Intell. Vehicles Symp. *, Jun. 2012, pp. 932–937. 

traffic intersections,’’ in *Proc. Amer. Control Conf. \(ACC\)*, Jul. 2016, 

\[279\] M. Tlig, O. Buffet, and O. Simonin, ‘‘Stop-free strategies for traffic pp. 6227–6232. 

networks: Decentralized on-line optimization,’’ in *Proc. 21st Eur. Conf. *

\[301\] L. Zhao and A. A. Malikopoulos, ‘‘Decentralized optimal control of *Artif. Intell. \(ECAI\)*, Aug. 2014, pp. 1191–1196. 

connected and automated vehicles in a corridor,’’ in *Proc. 21st Int. Conf. *

\[280\] A. M. Ishtiaque Mahbub, L. Zhao, D. Assanis, and A. A. Malikopoulos, *Intell. Transp. Syst. \(ITSC\)*, Nov. 2018, pp. 1252–1257. 

‘‘Energy-optimal coordination of connected and automated vehicles at

\[302\] J. Lee, B. Park, K. Malakorn, and J. So, ‘‘Sustainability assessments of multiple intersections,’’ in *Proc. Amer. Control Conf. \(ACC\)*, Jul. 2019, cooperative vehicle intersection control at an urban corridor,’’ *Transp. *

pp. 2664–2669. 

*Res. C, Emerg. Technol. *, vol. 32, pp. 193–206, Jul. 2013. 

\[281\] A. Hadjigeorgiou and S. Timotheou, ‘‘Optimizing the trade-off between

\[303\] W. Munst, C. Dannheim, M. Mader, N. Gay, B. Malnar, M. Al-Mamun, fuel consumption and travel time in an unsignalized autonomous intersec-and C. Icking, ‘‘Virtual traffic lights: Managing intersections in the tion crossing,’’ in *Proc. IEEE Intell. Transp. Syst. Conf. \(ITSC\)*, Oct. 2019, cloud,’’ in *Proc. 7th Int. Workshop Reliable Netw. Design Modeling* pp. 2443–2448. 

*\(RNDM\)*, Oct. 2015, pp. 329–334. 

7970

VOLUME 10, 2022



A. Gholamhosseinian, J. Seitz: Comprehensive Survey on Cooperative IM for Heterogeneous CVs

\[304\] A. A. Malikopoulos, C. G. Cassandras, and Y. Zhang, ‘‘A decentralized

\[324\] M. Baek, H. Lee, H. Choi, and K. Ko, ‘‘Development of intersection energy-optimal control framework for connected automated vehicles at collision avoidance algorithm for B2 V safety service,’’ *Int. J. Control* signal-free intersections,’’ *Automatica*, vol. 93, pp. 244–256, Jul. 2018. 

*Autom. *, vol. 8, no. 12, pp. 229–240, Dec. 2015. 

\[305\] M. Bashiri and C. H. Fleming, ‘‘A platoon-based intersection manage-

\[325\] M. A. Abid, O. Chakroun, and S. Cherkaoui, ‘‘Pedestrian collision avoid-ment system for autonomous vehicles,’’ in *Proc. IEEE Intell. Vehicles* ance in vehicular networks,’’ in *Proc. IEEE Int. Conf. Commun. \(ICC\)*, *Symp. \(IV\)*, Jun. 2017, pp. 667–672. 

Jun. 2013, pp. 2928–2932. 

\[306\] M. Bashiri, H. Jafarzadeh, and C. H. Fleming, ‘‘PAIM: Platoon-based

\[326\] K. S. Huang, P. J. Chiu, H. M. Tsai, C. C. Kuo, H. Y. Lee, and Y. C. 

autonomous intersection management,’’ in *Proc. 21st Int. Conf. Intell. *

F. Wang, ‘‘RedEye: Preventing collisions caused by red-light running *Transp. Syst. \(ITSC\)*, Nov. 2018, pp. 374–380. 

scooters with smartphones,’’ *IEEE Trans. Intell. Transp. Syst. *, vol. 17, 

\[307\] L. C. Bento, R. Parafita, and U. Nunes, ‘‘Intelligent traffic management no. 5, pp. 1243–1257, May 2016. 

at intersections supported by V2 V and V2I communications,’’ in *Proc. *

\[327\] J. Scholliers, D. Bell, A. Morris, and A. B. García, ‘‘Improving safety and *15th Int. IEEE Conf. Intell. Transp. Syst. *, Sep. 2012, pp. 1495–1502. 

mobility of vulnerable road users through ITS applications,’’ in *Proc. 5th*

\[308\] S. Huang, A. W. Sadek, and Y. Zhao, ‘‘Assessing the mobility and envi-Transp. Res. Arena \(TRA\), Apr. 2014, pp. 253–270. 

ronmental benefits of reservation-based intelligent intersections using an

\[328\] P. Gustafsson, J. Muñoz, L. Lindgren, C. Boda, and M. Dozza, ‘‘Bike-integrated simulator,’’ *IEEE Trans. Intell. Transp. Syst. *, vol. 13, no. 3, COM: Cooperative safety application supporting cyclists and drivers at pp. 1201–1214, Sep. 2012. 

intersections,’’ in *Proc. 3rd Int. Conf. Driver Distraction Inattention*, 

\[309\] L. C. Bento, R. Parafita, S. Santos, and U. Nunes, ‘‘Intelligent traffic Sep. 2013, pp. 1–16. 

management at intersections: Legacy mode for vehicles not equipped with

\[329\] I. Gohl, A. Schneider, J. Stoll, M. Wisch, and V. Nitsch, ‘‘Car-to-cyclist V2 V and V2I communications,’’ in *Proc. 16th Int. IEEE Conf. Intell. *

accidents from the car driver’s point of view,’’ in *Proc. 5th Int. Cycling* *Transp. Syst. \(ITSC\)*, Oct. 2013, pp. 726–731. 

*Saf. Conf. \(ICSC\)*, Nov. 2016, pp. 1–18. 

\[310\] B. Filocamo, J. A. Ruiz, and M. A. Sotelo, ‘‘Efficient management of

\[330\] *Xcycle Project*. Accessed: Nov. 23, 2021. \[Online\]. Available: road intersections for automated vehicles—The FRFP system applied to https://site.unibo.it/xcycle/en/the-project

the various types of intersections and roundabouts,’’ *Appl. Sci. *, vol. 10, 

\[331\] M. Kwakkernaat, F. Ophelders, J. Vissers, D. Willemsen, and P. Sukumar, no. 1, p. 316, 2020. 

‘‘Cooperative automated emergency braking for improved safety beyond sensor line-of-sight and field-ofview,’’ in *Proc. FISITA World Automot. *

\[311\] W. Du, A. Abbas-Turki, A. Koukam, S. Galland, and F. Gechter, ‘‘On *Congr. *, Jun. 2014, pp. 2–6. 

the V2X speed synchronization at intersections: Rule based System for extended virtual platooning,’’ *Proc. Comput. Sci. *, vol. 141, pp. 255–262, 

\[332\] M. Brännström, E. Coelingh, and J. Sjöberg, ‘‘Model-based threat assess-Jan. 2018. 

ment for avoiding arbitrary vehicle collisions,’’ *IEEE Trans. Intell. *

*Transp. Syst. *, vol. 11, no. 3, pp. 658–669, Sep. 2010. 

\[312\] R. Krajewski, P. Themann, and L. Eckstein, ‘‘Decoupled cooperative

\[333\] M. Segata, R. Vijeikis, and R. L. Cigno, ‘‘Communication-based colli-trajectory optimization for connected highly automated vehicles at urban sion avoidance between vulnerable road users and cars,’’ in *Proc. IEEE*

intersections,’’ in *Proc. IEEE Intell. Vehicles Symp. \(IV\)*, Jun. 2016, *Conf. Comput. Commun. Workshops \(INFOCOM WKSHPS\)*, May 2017, pp. 741–746. 

pp. 565–570. 

\[313\] P. Dai, K. Liu, Q. Zhuge, E. H.-M. Sha, V. C. S. Lee, and S. H. Son, 

\[334\] U. Hernandez-Jayo, I. De-la-Iglesia, and J. Perez, ‘‘V-Alert: Description

‘‘Quality-of-experience-oriented autonomous intersection control in and validation of a vulnerable road user alert system in the framework of vehicular networks,’’ *IEEE Trans. Intell. Transp. Syst. *, vol. 17, no. 7, a smart city,’’ *Sensors*, vol. 15, no. 8, pp. 18480–18505, 2015. 

pp. 1956–1967, Jul. 2016. 

\[335\] J. J. Anaya, E. Talavera, D. Gimenez, N. Gomez, F. Jimenez, and

\[314\] M. N. Mladenovic and M. M. Abbas, ‘‘Self-organizing control framework J. E. Naranjo, ‘‘Vulnerable road users detection using V2X communi-for driverless vehicles,’’ in *Proc. 16th Int. IEEE Conf. Intell. Transp. Syst. *

cations,’’ in *Proc. IEEE 18th Int. Conf. Intell. Transp. Syst. *, Sep. 2015, *\(ITSC\)*, Oct. 2013, pp. 2076–2081. 

pp. 107–112. 

\[315\] M. N. Mladenovic and M. Abbas, ‘‘Priority-based intersection control

\[336\] InDev Project. \(2018\). *In-Depth Understanding of Accident Causa-framework for self-driving vehicles: Agent-based model development tion for Vulnerable Road Users. \[Online\]. Available: https://cordis. *
* 
and evaluation,’’ in Proc. Int. Conf. Connected Vehicles Expo \(ICCVE\), europa.eu/project/id/635895

Nov. 2014, pp. 377–384. 

\[337\] A. Gholamhosseinian and J. Seitz, ‘‘Vehicle classification in intelligent

\[316\] C. Wuthishuwong, A. Traechtler, and T. Bruns, ‘‘Safe trajectory planning transport systems: An overview, methods and software perspective,’’
*
*for autonomous intersection management by using vehicle to infrastruc-IEEE Open J. Intell. Transp. Syst. *, vol. 2, pp. 173–194, 2021. 

ture communication,’’ *EURASIP J. Wireless Commun. Netw. *, vol. 2015, 

\[338\] C. F. Caruntu, A. V. Militaru, and C. R. Comsa, ‘‘Cyber-physical systems-no. 1, p. 33, Dec. 2015. 

based architecture for signalized traffic corridors: Monitoring and syn-

\[317\] J. Ding, H. Xu, J. Hu, and Y. Zhang, ‘‘Centralized cooperative intersection chronized coordination,’’ in *Proc. 23rd Int. Conf. Control Syst. Comput. *

control under automated vehicle environment,’’ in *Proc. IEEE Intell. *

*Sci. \(CSCS\)*, May 2021, pp. 314–321. 

*Vehicles Symp. \(IV\)*, Jun. 2017, pp. 972–977. 

\[339\] A. Gholamhosseinian and J. Seitz, ‘‘Safety-centric vehicle classification

\[318\] H. Zhang, R. Zhang, C. Chen, D. Duan, X. Cheng, and L. Yang, using vehicular networks,’’ *Proc. Comput. Sci. *, vol. 191, pp. 238–245, 

‘‘A priority-based autonomous intersection management \(AIM\) scheme Jan. 2021. 

for connected automated vehicles \(CAVs\),’’ *Vehicles*, vol. 3, no. 3, 

\[340\] T. Bailey and H. Durrant-Whyte, ‘‘Simultaneous localization and map-pp. 533–544, Aug. 2021. 

ping \(SLAM\): Part II,’’ *IEEE Robot. Autom. Mag. *, vol. 13, no. 3, 

\[319\] X. Qian, J. Gregoire, A. de La Fortelle, and F. Moutarde, ‘‘Decen-pp. 108–117, Sep. 2006. 

tralized model predictive control for smooth coordination of automated

\[341\] J. J. Haas and Y.-C. Hu, ‘‘Communication requirements for crash avoid-vehicles at intersection,’’ in *Proc. Eur. Control Conf. \(ECC\)*, Jul. 2015, ance,’’ in *Proc. 7th ACM Int. Workshop Veh. InterNETworking \(VANET\)*, pp. 3452–3458. 

2010, pp. 1–10. 

\[320\] X. Zhao, J. Wang, Y. Chen, and G. Yin, ‘‘Multi-objective cooperative

\[342\] T. Zinchenko, H. Tchouankem, L. Wolf, and A. Leschke, ‘‘Reliability scheduling of CAVs at non-signalized intersection,’’ in *Proc. 21st Int. *

analysis of vehicle-to-vehicle applications based on real world mea-Conf. Intell. Transp. Syst. \(ITSC\), Nov. 2018, pp. 3314–3319. 

surements,’’ in *Proc. 10th ACM Int. Workshop Veh. Inter-Netw., Syst., *

\[321\] Y. Wang, P. Cai, and G. Lu, ‘‘Cooperative autonomous traffic organi-Appl. \(VANET\), 2013, pp. 11–20. 

zation method for connected automated vehicles in multi-intersection

\[343\] A. Tang and A. Yip, ‘‘Collision avoidance timing analysis of DSRC-road networks,’’ *Transp. Res. C, Emerg. Technol. *, vol. 111, pp. 458–476, based vehicles,’’ *Accident Anal. Prevention*, vol. 42, no. 1, pp. 182–195, Feb. 2020. 

2010. 

\[322\] I. Bosankić and L. Banjanovic-Mehmedovic, ‘‘Cooperative intelligence

\[344\] M. Sepulcre, J. Mittag, P. Santi, H. Hartenstein, and J. Gozalvez, ‘‘Conin roundabout intersections using hierarchical fuzzy behavior calculation gestion and awareness control in cooperative vehicular systems,’’ *Proc. *

of vehicle speed profile,’’ in *Proc. 5th Int. Conf. Transp. Traffic Eng. *

*IEEE*, vol. 99, no. 7, pp. 1260–1279, Jul. 2011. 

*\(ICTTE\)*, Jul. 2016, pp. 1–6. 

\[345\] T. Zinchenko, H. Tchouankem, and L. Wolf, ‘‘Reliability of vehicle-

\[323\] Z. Cao, H. Guo, and J. Zhang, ‘‘A multiagent-based approach for vehicle to-vehicle communication at urban intersections,’’ in *Proc. 7th Int. *

routing by considering both arriving on time and total travel time,’’ *ACM*

*Workshop Commun. Technol. Vehicles \(Nets4Cars-Fall\)*, Oct. 2014, *Trans. Intell. Syst. Technol. *, vol. 9, no. 3, pp. 1–21, 2017. 

pp. 7–11. 

VOLUME 10, 2022

7971





A. Gholamhosseinian, J. Seitz: Comprehensive Survey on Cooperative IM for Heterogeneous CVs

\[346\] S. Joerer, B. Bloessl, M. Segata, C. Sommer, R. L. Cigno, and F. Dressler, 

\[368\] G. R. de Campos, P. Falcone, and J. Sjoberg, ‘‘Autonomous cooperative

‘‘Fairness kills safety: A comparative study for intersection assistance driving: A velocity-based negotiation approach for intersection crossing,’’

applications,’’ in *Proc. IEEE 25th Annu. Int. Symp. Pers., Indoor, Mobile* in *Proc. 16th Int. IEEE Conf. Intell. Transp. Syst. \(ITSC\)*, Oct. 2013, *Radio Commun. \(PIMRC\)*, Sep. 2014, pp. 1442–1447. 

pp. 1456–1461. 

\[347\] O. K. Tonguz, N. Wisitpongphan, and F. Bai, ‘‘DV-CAST: A distributed

\[369\] G. R. Campos, P. Falcone, H. Wymeersch, R. Hult, and J. Sjöberg, ‘‘Coop-vehicular broadcast protocol for vehicular ad hoc networks,’’ *IEEE Wire-erative receding horizon conflict resolution at traffic intersections,’’ in less Commun. , vol. 17, no. 2, pp. 47–57, Apr. 2010. *
* 
Proc. 53rd IEEE Conf. Decis. Control, Dec. 2014, pp. 2932–2937. 

\[348\] C. Sommer, O. K. Tonguz, and F. Dressler, ‘‘Traffic information systems:

\[370\] S. Pruekprasert, X. Zhang, J. Dubut, C. Huang, and M. Kishida, ‘‘Deci-Efficient message dissemination via adaptive beaconing,’’ IEEE Com-sion making for autonomous vehicles at unsignalized intersection in mun. Mag. , vol. 49, no. 5, pp. 173–179, May 2011. 

presence of malicious vehicles,’’ in Proc. IEEE Intell. Transp. Syst. Conf. 

\[349\] R. K. Schmidt, T. Leinmüller, E. Schoch, F. Kargl, and G. Schäfer, \(ITSC\), Oct. 2019, pp. 2299–2304. 

‘‘Exploration of adaptive beaconing for efficient intervehicle safety com-

\[371\] L. Li and F. Y. Wang, ‘‘Cooperative driving at blind crossings using munication,’’ IEEE Netw. , vol. 24, no. 1, pp. 14–19, Jan. 2010. 

intervehicle communication,’’ IEEE Trans. Veh. Technol. , vol. 55, no. 6, 

\[350\] C. Sommer, S. Joerer, M. Segata, O. K. Tonguz, R. L. Cigno, and pp. 1712–1724, Nov. 2006. 

F. Dressler, ‘‘How shadowing hurts vehicular communications and

\[372\] K. Dresner and P. Stone, ‘‘Mitigating catastrophic failure at intersections how dynamic beaconing can help,’’ in Proc. 32nd IEEE INFOCOM, of autonomous vehicles,’’ in Proc. 7th Int. Joint Conf. Auton. Agents Apr. 2013, pp. 110–114. 

Multiagent Syst. , vol. 3, May 2008, pp. 1393–1396. 

\[351\] M. Werner, R. Lupoaie, S. Subramanian, and J. Jose, ‘‘MAC layer perfor-

\[373\] S. Lefèvre, J. Petit, R. Bajcsy, C. Laugier, and F. Kargl, ‘‘Impact of V2X

mance of its G5-optimized DCC and advanced transmitter coordination,’’

privacy strategies on intersection collision avoidance systems,’’ in Proc. 

in 4th ETSI TC ITS Workshop, Feb. 2012, pp. 1–21. 

5th IEEE Veh. Netw. Conf. , Dec. 2013, pp. 71–78. 

\[352\] Intelligent Transport Systems \(Its\); Decentralized Congestion Control

\[374\] K. C. Bentjen, ‘‘Mitigating the effects of cyber attacks and human control Mechanisms for Intelligent Transport Systems Operating in the 5 GHz in an autonomous intersection,’’ Air Force Inst. Technol., Dept. Elect. 

Range; Access Layer Part, Standard TS 102 687 V1.1.1, Jul. 2011. 

Eng. Comput. Eng., AFIT Scholar, Tech. Rep. AFIT-ENG-MS-18-M-

\[353\] O. Algazali and A. Gholamhosseinian, ‘‘Evaluation of decentralized con-008, 2018. 

gestion control algorithm candidates for wireless vehicular communica-

\[375\] Q. A. Chen, Y. Yin, Y. Feng, Z. M. Mao, and H. X. Liu, ‘‘Exposing tion,’’ Eurecom, Paris, France, Tech. Rep. 1, Jun. 2014. 

congestion attack on emerging connected vehicle based traffic signal con-

\[354\] E. Andert, M. Khayatian, and A. Shrivastava, ‘‘Crossroads: Time-trol,’’ in Proc. Netw. Distrib. Syst. Secur. Symp. \(NDSS\), 2018, pp. 1–15. 

sensitive autonomous intersection management technique,’’ in Proc. 54th

\[376\] S. Checkoway, D. McCoy, B. Kantor, D. Anderson, H. Shacham, S. Sav-Annu. Design Automat. Conf. , Jun. 2017, pp. 1–6. 

age, K. Koscher, A. Czeskis, F. Roesner, and T. Kohno, ‘‘Comprehensive

\[355\] M. Khayatian, Y. Lou, M. Mehrabian, and A. Shirvastava, ‘‘Cross-experimental analyses of automotive attack surfaces,’’ in Proc. USENIX
*
*roads\+: A time-aware approach for intersection management of con-Secur. Symp. *, vol. 4, 2011, pp. 447–462. 

nected autonomous vehicles,’’ *ACM Trans. Cyber-Phys. Syst. *, vol. 4, 

\[377\] S. Mazloom, M. Rezaeirad, A. Hunter, and D. McCoy, ‘‘A security no. 2, pp. 1–28, 2019. 

analysis of an in-vehicle infotainment and app platform,’’ in *Proc. 10th*

\[356\] C. Yu, G. Tan, and Y. Yu, ‘‘Make driver agent more reserved: An AIM-USENIX Workshop Offensive Technol. \(WOOT\), 2016, pp. 1–12. 

based incremental data synchronization policy,’’ in *Proc. IEEE 9th Int. *

\[378\] K. Koscher, A. Czeskis, F. Roesner, S. Patel, T. Kohno, S. Checkoway, *Conf. Mobile Ad-Hoc Sensor Netw. *, Dec. 2013, pp. 198–205. 

D. McCoy, B. Kantor, D. Anderson, and H. Shacham, ‘‘Experimental

\[357\] Y. Bian, S. E. Li, W. Ren, J. Wang, K. Li, and H. X. Liu, ‘‘Cooperation security analysis of a modern automobile,’’ in *Proc. IEEE Symp. Secur. *

of multiple connected vehicles at unsignalized intersections: Distributed *Privacy*, May 2010, pp. 447–462. 

observation, optimization, and control,’’ *IEEE Trans. Ind. Electron. *, 

\[379\] J. R. Douceur, ‘‘The sybil attack,’’ in *Proc. Int. Workshop Peer–Peer Syst. *, vol. 67, no. 12, pp. 10744–10754, Dec. 2020. 

2002, pp. 251–260. 

\[358\] L. Qian, C. Chen, B. Wu, L. Xuan, and T. Wang, ‘‘Optimal control of connected and automated vehicles at unsignalized intersections: Discrete and regroup,’’ in *Proc. Int. Conf. Intell. Eng. Manage. \(ICIEM\)*, Jun. 2020, pp. 370–375. 

ASHKAN GHOLAMHOSSEINIAN \(Graduate

\[359\] X. Chen, B. Xu, X. Qin, Y. Bian, M. Hu, and N. Sun, ‘‘Non-signalized Student Member, IEEE\) received the bachelor’s

intersection network management with connected and automated vehi-degree in computer engineering-software in Iran, cles,’’ *IEEE Access*, vol. 8, pp. 122065–122077, 2020. 

the M.Sc. degree in computer network engineering

\[360\] B. Liu and A. El Kamel, ‘‘V2X-based decentralized cooperative adaptive from Halmstad University, Sweden, and the Post

cruise control in the vicinity of intersections,’’ *IEEE Trans. Intell. Transp. *

master’s degree in communications for intelligent *Syst. *, vol. 17, no. 3, pp. 644–658, Mar. 2016. 

transport systems from Eurecom, France. He is

\[361\] L. Bruni, A. Colombo, and D. D. Vecchio, ‘‘Robust multi-agent collision currently pursuing the Ph.D. degree in electri-avoidance through scheduling,’’ in *Proc. 52nd IEEE Conf. Decis. Control*, cal engineering and information technology with

Dec. 2013, pp. 3944–3950. 

the Communication Networks Group, Technische

\[362\] A. Colombo and D. Del Vecchio, ‘‘Efficient algorithms for collision Universität Ilmenau, Germany. His research interests include vehicular net-avoidance at intersections,’’ in *Proc. 15th ACM Int. Conf. Hybrid Syst.,* works, intelligent transport systems, computer networks, and wireless and *Comput. Control \(HSCC\)*, 2012, pp. 145–154. 

mobile networks and communications. 

\[363\] N. Li, Y. Yao, I. Kolmanovsky, E. Atkins, and A. R. Girard, ‘‘Game-theoretic modeling of multi-vehicle interactions at uncontrolled intersections,’’ *IEEE Trans. Intell. Transp. Syst. *, early access, Oct. 6, 2020, doi:

10.1109/TITS.2020.3026160. 

JOCHEN SEITZ \(Member, IEEE\) studied com-

\[364\] M. Khayatian, R. Dedinsky, S. Choudhary, M. Mehrabian, and puter science at the University of Karlsruhe \(TH\). 

A. Shrivastava, ‘‘R2IM–robust and resilient intersection management of He received the Ph.D. degree in integration of

connected autonomous vehicles,’’ in *Proc. IEEE 23rd Int. Conf. Intell. *

heterogeneous network management architectures

*Transp. Syst. \(ITSC\)*, Sep. 2020, pp. 1–6. 

and the Habilitation in cooperative network and

\[365\] R. Dedinsky, M. Khayatian, M. Mehrabian, and A. Shrivastava, systems management from the TH. He held a post-

‘‘A dependable detection mechanism for intersection management of con-doctoral position at the Distributed Multimedia

nected autonomous vehicles \(interactive presentation\),’’ in *Proc. Work-Research Group, Lancaster University, along with shop Auton. Syst. Design \(ASD\), 2019, pp. 7:1–7:13. *
* 
\[366\] T.-C. Au, C.-L. Fok, S. Vishwanath, C. Julien, and P. Stone, ‘‘Evasion Prof. Davies. He was a substitute Professor of

planning for autonomous vehicles at intersections,’’ in Proc. IEEE/RSJ

distributed systems with the University of Tech-

Int. Conf. Intell. Robots Syst. , Oct. 2012, pp. 1541–1546. 

nology Braunschweig. Since 2001, he has been a Professor of communi-

\[367\] H. Kowshik, D. Caveney, and P. R. Kumar, ‘‘Provable systemwide safety cation networks with the Faculty of Electrical Engineering and Information in intelligent intersections,’’ IEEE Trans. Veh. Technol. , vol. 60, no. 3, Technology, Technische Universität Ilmenau. 

pp. 804–818, Mar. 2011. 

7972

VOLUME 10, 2022


*



