1

V2X Cooperative Perception for Autonomous

Driving: Recent Advances and Challenges

Tao Huang∗, Senior Member, IEEE, Jianan Liu∗, Xi Zhou∗, Graduate Student Member, IEEE, Dinh C. Nguyen, Member, IEEE, Mostafa Rahimi Azghadi, Senior Member, IEEE, Yuxuan Xia, Qing-Long Han†, Fellow, IEEE, and Sumei Sun, Fellow, IEEE

Abstract—Achieving fully autonomous driving with heightened across domains, such as 3D object detection using camera safety and efficiency depends on vehicle-to-everything \(V2X\)

\[9\]–\[13\], LiDAR \[14\]–\[19\], radar \[20\]–\[25\], and fusion \[26\]–

cooperative perception \(CP\), which allows vehicles to share

\[41\], as well as 3D multi-object tracking employing camera perception data, thereby enhancing situational awareness and

\[42\]–\[45\], LiDAR \[46\]–\[51\], radar \[52\]–\[55\], and fusion \[56\]–

overcoming the limitations of the sensing ability of individual vehicles. V2X CP is crucial for extending perception range, 

\[63\], to name just a few. However, single-vehicle perception improving accuracy, and strengthening the decision-making and technologies still grapple with notable limitations. Sparse control capabilities of autonomous vehicles in complex environ-observations due to occlusion, restricted sensor Field of View ments. This paper provides a comprehensive survey of recent \(FoV\), and sensor resolution remain primary challenges \[64\]. 

advances in V2X CP, introducing mathematical models of CP

Additionally, susceptibility to sensor errors arising from ad-processes across various collaboration strategies. We examine essential techniques for reliable perception sharing, including verse weather and hardware failures raises concerns about sys-agent selection, data alignment, and fusion methods. Key issues tem robustness \[65\]. These bottlenecks constrain the potential are analyzed, such as agent and model heterogeneity, perception and safety of automated vehicles in complex driving scenarios. 

uncertainty, and the impact of V2X communication constraints Cooperative Perception \(CP\) has been developed to mitigate like delays and data loss on CP effectiveness. To inspire further the constraints associated with the perception capabilities of advancements in V2X CP, we outline promising avenues, including privacy-preserving artificial intelligence \(AI\), collaborative individual vehicles. Enabled by Vehicle-to-Everything \(V2X\) AI, and integrated sensing frameworks, as pathways to enhance communication \[66\], CP allows Connected Autonomous Vehi-CP capabilities. 

cles \(CAVs\) to exchange information with each other \(V2V\) Index Terms—Autonomous driving; connected and automated

\[67\], infrastructure \(V2I\) \[68\], \[69\], pedestrians \(V2P\) \[70\], 

vehicles \(CAVs\); cooperative perception \(CP\); V2X Communica-and networks \(V2N\) \[71\]. This communication facilitates the tion; segmentation; object detection; multi-object tracking; data sharing of crucial information, such as traffic conditions, road fusion; deep learning; artificial intelligence \(AI\). 

hazards, and signal status, extending beyond the perceptual range of individual vehicles \[72\]. Through this data exchange, I. INTRODUCTION

CP enhances decision-making, enabling vehicles to better P

anticipate the movements of other road users, synchronize ac-ERCEPTION plays a pivotal role in ensuring safety in tions, and execute coordinated maneuvers, such as platooning autonomous driving, facilitating awareness of the sur-and safe lane changes. 

rounding road environment and other road participants over In full-stack autonomous driving, components like percep-time, and utilizing various sensor modalities \[1\]–\[8\]. Recent tion, localization, planning, control, and system integration advancements in intelligent vehicle technology have led to collectively enable a vehicle to operate autonomously and significant progress in single-vehicle perception techniques safely. V2X CP significantly enhances this stack by sharing arXiv:2310.03525v4 \[cs.CV\] 14 Nov 2024

∗Equal contribution. 

sensory and positional data via V2X communication between

†Corresponding author. 

connected vehicles and infrastructure, thereby extending each T. Huang, X. Zhou, and M. R. Azghadi are with the College vehicles awareness beyond the limits of its sensing range. 

of Science and Engineering, James Cook University, Cairns, QLD

4870, Australia. Email: tao.huang1@jcu.edu.au, xi.zhou1@my.jcu.edu.au, Through V2X CP, the perception layer benefits from improved mostafa.rahimiazghadi@jcu.edu.au. 

accuracy and safety, as vehicles can detect occluded or distant J. 

Liu

is

with

Vitalent

Consulting, 

Gothenburg, 

Sweden. 

Email:

objects using shared data from other agents1 in the environ-jianan.liu@vitalent.se. 

Dinh C. Nguyen is with the Department of Electrical and Computer ment. In localization, V2X CP refines vehicle positioning by Engineering, University of Alabama in Huntsville, Huntsville, AL 35899, leveraging positional data from surrounding agents, which is USA. Email: dinh.nguyen@uah.edu. 

especially valuable in areas with poor GPS signals. Planning Y. Xia is with the Department of Electrical Engineering, Linkping University, Linkping 58183, Sweden. Email: yuxuan.xia@liu.se. 

also becomes more adaptive and safer, as V2X CP allows Q.-L. Han is with the School of Science, Computing and Engineering access to real-time data on nearby vehicles movements, en-Technologies, Swinburne University of Technology, Melbourne, VIC 3122, abling vehicles to make smoother, more informed maneuvers. 

Australia. Email: qhan@swin.edu.au. 

S. Sun is with the Institute for Infocomm Research, Agency for Science, Additionally, the enhanced situational awareness that V2X CP

Technology and Research, Singapore 138632. Email: sunsm@i2r.a-star.edu.sg. 

This work has been submitted to the IEEE for possible publication. 

1“Agents” refer to autonomous entities within traffic environments, includ-Copyright may be transferred without notice, after which this version may ing vehicles and infrastructure equipped with sensors and communication no longer be accessible. 

systems, working together to enable cooperative perception. 

2

\(a\) Without V2X CP, the white car has a blocked front view and thus potentially \(b\) With V2X CP, the white car can detect the running boy due to the can have a fatal collision with the running boy. 

expanded perception range, enabling it to predict the boy’s behavior and avoid a potentially fatal collision. 

Fig. 2. An example of V2X CP improves road safety. 

provides indirectly improves control precision and supports hatchback whose front view is obstructed by a parked food seamless system integration, reducing the vehicles reliance on truck, preventing it from detecting a boy chasing a football any single sensor. Overall, V2X CP strengthens the robustness near the road, as depicted in Fig. 2a. This presents a significant and adaptability of autonomous systems, laying a foundation collision risk if the vehicle fails to stop promptly. However, for safer and more scalable deployment in real-world scenar-with CP enabled, the blue CAV shares information about ios. 

the boy’s movement with the white hatchback, allowing it to Fig. 1 illustrates an urban scenario of CP supported by anticipate and decelerate preemptively, as shown in Fig. 2b, 

V2X communication. In Fig. 1a, each vehicle operates inde-thereby avoiding a fatal accident. 

pendently, relying solely on its perception systems without While CP enables safer driving, numerous additional factors collaboration, which restricts their understanding of the envi-must be considered to bring V2X CP into practical application, ronment with a limited sensing range. Due to obstructions and aligning with the foundational technologies underpinning V2X

varying distances, autonomous vehicles face challenges such CP. For example, the associated data privacy \[74\]–\[76\] and as unreliable perception of distant objects and obstructed views ethical concerns \[77\], the associated development of smart

\[73\]. In contrast, Fig. 1b shows vehicles and the infrastructure cities \[78\], urban infrastructure \[79\], \[80\], the associated collaborating through wireless communication, leading to a standardization, regulation, and policy from governments and holistic understanding of the environment and eliminating regulatory bodies \[81\]–\[83\], the associated trust issue in blind spots. A specific scenario in Fig. 2 demonstrates a white human-system interaction \[84\], and the balance between ex-

3

TABLE I

A SUMMARY OF THE RECENTLY PUBLISHED SURVEYS IN COOPERATIVE PERCEPTION WITH V2X TECHNOLOGIES. 

The Taxonomy of Cooperative Perception System: Modules and Issues Paper

Year Publication

Survey Topic

CAS PIS PIC DSRC C-V2X LC CD APE CIF MH DH DS DP PU TD S2R Sim Data IEEE

Feature level based cooperative object detec-

√

√

√

\[85\]

2021

×

×

×

×

×

×

×

×

×

×

×

×

×

×

×

Network

tion. 

IEEE

V2I cooperative object detection and track-

√

√

√

\[86\]

2022

×

×

×

×

×

×

×

×

×

×

×

×

×

×

×

IV

ing. 

IEEE

Cooperation issues in localization, map gen-

√

√

√

√

√

\[87\]

2022

×

×

×

×

×

×

×

×

×

×

×

×

×

TITS

eration, object detection and tracking. 

IEEE

√

√

√

√

√

\[88\]

2023

Multi-sensor fusion and CP. 

×

×

×

×

×

×

×

×

×

×

×

×

×

MITS

Fundamental components and core aspects of

IEEE

√

√

√

√

√

√

\[89\]

2024

a CP system for enabling cooperative driving

×

×

×

×

×

×

×

×

×

×

×

×

TITS

automation. 

IEEE

V2X cooperation efficiency, robustness, and

√

√

√

√

√

√

√

√

√

\[90\]

2023

×

×

×

×

×

×

×

×

×

MITS

safety. 

The challenges of implementing CP within

V2X systems and the practical applicability

√

√

√

√

√

√

√

√

√

√

√

√

√

√

\[91\]

2023

−

×

×

×

×

of different CP methodologies in V2X envi-

ronments. 

CP in intelligent transportation systems, with

IEEE

√

√

√

√

√

√

√

√

\[92\]

2024

emphasizing road-to-vehicles collaboration at

×

×

×

×

×

×

×

×

×

×

TIV

intersections. 

The perception architecture and associated

IEEE

√

√

√

√

√

√

\[93\]

2024

technologies within the Vehicle-Road-Cloud

×

×

×

×

×

×

×

×

×

×

×

×

TITS

Integration System. 

The evolution of V2X CP technologies, key

This

elements of V2X CP, and V2X CP solutions

√

√

√

√

√

√

√

√

√

√

√

√

√

√

√

√

√

√

2024

−

survey

that tackle major issues in practical driving

scenarios. 

Note: CAS: Cooperative Agent Selection, PIS: Perception Information Selection, PIC: Perception Information Compression, DSRC: Dedicated Short-range Communication, C-V2X: Cellular-based Vehicle-to-Everything, LC: Lossy Communication, CD: Communication Delays, APE: Alignment for Pose Errors, CIF: Cooperative Information Fusion, MH: Model Heterogeneity, DH: Data Heterogeneity, DS: Data Security, DP: Data Privacy, PU: Perception Uncertainties, TD: Task Discrepancy, S2R: Simulation to Reality, Sim: Simulator, Data: Dataset. The exact meaning of these items in this taxonomy will be explained systematically in the following sections. 

cessive reliance and information inundation \[94\]. Thus, while assess mainstream CP approaches. A more recent survey the potential of V2X CP is profound, a concerted, multi-

\[92\] focused on CP at intersections, analyzing perception, dimensional effort is requisite for its holistic integration into communication, and downstream applications. However, these our daily lives. 

surveys overlook the critical role of V2X communication, Although various approaches have been proposed to ad-which is essential for enabling effective CP in autonomous dress these challenges, a comprehensive survey is needed vehicles by facilitating information transfer and supporting to assess recent advancements, identify research gaps, and decision-making. The work in \[93\] examined typical V2X

propose future directions. Some existing surveys often focus communication technologies, including Dedicated Short-range on specific aspects of CP, such as feature-level cooperative Communication \(DSRC\) and Cellular-based V2X communi-object detection \[85\] or infrastructure-based CP \[86\], but lack cation \(C-V2X\), and presented an overview of perception a systematic overview of V2X CP technologies. To fill this architectures and technologies within the Vehicle-Road-Cloud gap, the work in \[87\] provided an overview of CP algorithms, Integration System, encompassing single-node, multi-node, emphasizing challenges like localization and detection, while and vehicle-road-cloud cooperative perception frameworks. 

the review in \[88\] discussed communication delays and in-While it offers insights into these technologies, it does not formation fusion in multi-sensor V2V and V2I schemes. The explore specific algorithms and techniques in depth. This work survey in \[89\] explored CP system architectures and proposed contributes to a comprehensive understanding of CP and its a hierarchical framework for unifying CP scenarios. Despite enabling V2X technologies and builds upon existing survey covering common CP challenges, these surveys lacked an efforts. Table I compares our paper with these surveys. The analysis of CP progress regarding practical implementation key contributions are as follows:

challenges. 

• Filling gaps in existing surveys by conducting a thorough Recent work \[90\] evaluated collaborative modules and so-review of the evolution of V2X CP from its inception to lutions focusing on efficiency, robustness, and safety. Another state-of-the-art proposals. 

survey \[91\] addressed practical challenges in implementing

• Discussing established V2X communication technologies CP, such as latency, bandwidth constraints, and robustness, and the key impacts of real-world communication con-categorizing methodologies into early, intermediate, and late straints on CP. 

fusion. Environmental simulations were also conducted to

• Presenting a unified framework for V2X CP to eluci-

4

Fig. 3. Organization of this paper. 

TABLE II

CP system. 

LIST OF KEY ACRONYMS. 

• Introducing a new taxonomy to review V2X CP solutions, addressing significant practical driving scenario issues. 

Acronyms

Definitions

• Summarizing lessons learned, providing insights into AI

Artificial Intelligence

existing challenges, and highlighting potential avenues for BEV

Birds Eye View

future research. 

CAM

Cooperative Awareness Message

The structure of this paper is illustrated in Fig. 3. Section CAV

Connected Autonomous Vehicle

II presents the mathematical formulation of V2X CP. A brief CDA

Cooperative Driving Automation

CI

Covariance Intersection

historical overview of CP system development is provided in CNN

Convolutional Neural Network

Section III. Section IV introduces a generic framework for CP

Cooperative or Collaborative Perception

systematically understanding the CP system. Practical issues DSRC

Dedicated Short-range Communication

related to CP systems and relevant datasets are discussed in C-V2X

Cellular-based Vehicle-to-Everything

Sections V and VI, respectively. Section VII compares the IRS

Intelligent Reflecting Surface

performance of various CP methods in offline testing and CPM

Collective Perception Message

explores real-world implementations. Section VIII explores DT

Digital Twin

the challenges and potential future directions, and the paper FL

Federated Learning

concludes with Section IX. Table II lists key acronyms and FoV

Field of View

GNN

Graph Neural Network

abbreviations used throughout the paper. 

GNSS

Global Navigation Satellite System

GPS

Global Positioning System

II. MATHEMATICAL FORMULATION OF COOPERATIVE

IMU

Inertial Measurement Unit

PERCEPTION

ISAC

Integrated Sensing and Communication

ITS

Intelligent Transportation System

This section begins with an overview of sensors and CP

LSTM

Long Short-term Memory

collaboration strategies, followed by a detailed mathematical MIMO

Multiple-input Multiple-output

formulation for early, intermediate, and late collaboration RSU

Roadside Unit

strategies. 

V2I

Vehicle-to-Infrastructure

V2V

Vehicle-to-Vehicle

V2X

Vehicle-to-Everything

A. Overview

CP is built upon the shared data contributed by each participating agent. For each individual agent, raw observations date essential components of multi-agent collaboration, are collected via onboard sensors, including cameras, LiDAR, enhancing researchers’ systematic understanding of the radar, and, in some cases, ultrasonic sensors. Cameras provide

5

rich visual informationsuch as color, texture, and shapeessen-tial for object detection and scene interpretation \[95\]. LiDAR

generates high-resolution 3D point clouds by measuring the return time of laser pulses, enabling precise distance and shape estimation critical for detailed mapping and obstacle detection \[96\]. Radar supplies range, speed, and movement data, effectively detecting objects at greater distances and under diverse weather conditions, making it especially valuable for tracking the velocity of surrounding vehicles. Although ultrasonic sensors are less commonly utilized in CP, they contribute valuable proximity data in close-range applications, such as parking and low-speed maneuvers. 

CP strategies are categorized into three collaboration types: early, late, and intermediate collaboration, each defined by the level of data processing before sharing. Note that all types of sensor data can be utilized across any of these collaboration types. In early collaboration, raw sensor data is shared directly among agents, providing high-fidelity information but requiring substantial communication bandwidth and precise synchronization. This approach can be challenging in networks with limited bandwidth or high latency, leading to potential inconsistencies in data across agents. In late collaboration, \(a\) Early

\(b\) Late

\(c\) Intermediate

only the final perception outputs, such as object classifica-tions and location, are shared. This minimizes communication Fig. 4. Overview of collaboration schemes for autonomous driving: \(a\) Early collaboration; \(b\) Late collaboration; \(c\) Intermediate collaboration. 

demands significantly but limits data granularity, potentially restricting the system’s ability to perform detailed analysis or adapt to complex, rapidly evolving scenarios. Intermediate Then, the i-th agent uses an encoder FEncoder\(·\) to extract t

collaboration strikes a balance by pre-processing sensor data high-level CP feature e

F i from its fused CP raw data Oti:

to extract features before sharing them with other agents. 

t

This approach reduces data volume while retaining essential e

F = F

\). 

i

Encoder\(Oti

\(2\)

information, lowering bandwidth requirements. However, the Finally, the i-th agent uses a decoder FDecoder\(·\) to decode effectiveness depends on each agents feature extraction accu-t

t

the CP feature e

F

racy, and variability in feature quality may lead to perception i and obtain the CP results e

Y i:

t



t

inconsistencies across agents. 

e

Y = F

. 

i

Decoder

e

F i

\(3\)

A schematic overview of these collaboration schemes is provided in Fig. 4. For mathematical clarity, a scenario with N

collaborating agents is considered, where the local raw sensor data observed by the i-th agent at time step t is denoted as Xt C. Late Collaboration

i . 

In the following subsections, the workflow and mathematical In contrast to early collaboration, late collaboration involves formulation of each collaboration scheme are elaborated in exchanging individual perceptual outcomes, as depicted in Fig. 

detail. 

4b, requiring minimal data transmission \[100\]. 

In this case, the i-th agent independently processes its raw perception data Xti, generate its feature data F ti and its final B. Early Collaboration

perception result Rti, via \(4\) and \(5\) respectively: As illustrated in Fig. 4a, early collaboration involves aggre-F t = F



Encoder

Xt , 

\(4\)

gating raw sensor observations collected by all participating i

i

agents, fostering a comprehensive perspective \[97\]–\[99\]. The Rt = F

, 

i

Decoder

F ti

\(5\)

i-th agent broadcasts its raw observation Xti to the other N −1

where F

neighbouring agents and also receives the raw observation Encoder\(·\) and FDecoder\(·\) represent the encoder and decoder algorithms, respectively. 

Xt , j ∈ \{1, · · · , N \}, j ̸= i

j

. After that, it performs data fusion

After individual processing, the individual perception results on the received raw data with self-raw data and produces fused from each agent are shared with all other agents. Then, for the CP raw data Oti. For simplicity, we assume that all agents use i-th agent, it uses a late fusion algorithm F

the same fusion, encoder, and decoder algorithms. Thus, the LateFusion\(·\) to fuse

the received individual perception result from all other N − 1

raw data fusion at the i-th agent can be expressed as: t

agents and its own perception result to generate CP result b Y i:





Ot = F

Xt N

, 

t





i

EarlyFusion

k

\(1\)



N

k=1

b

Y = F

Rt

. 

i

LateFusion

k

\(6\)

k=1

where FEarlyFusion\(·\) denotes the early fusion algorithm. 

6

D. Intermediate Collaboration

necessitates temporal and spatial alignment before the post-In this case, as shown in Fig. 4c, each agent shared data fusion phase. Early studies addressed this challenge by intermediate features rather than raw data or final perception employing motion models and estimation algorithms rooted in results. Firstly, the i-th agent extracts its own feature data F t statistical signal processing. In \[105\], researchers leveraged a i

from its raw perception data Xt

Car2X-based perception module for object-level data fusion, i as described in \(4\). Then, 

the extracted individual feature data are shared among all utilizing an Unscented Kalman Filter to align the received N agents via V2X communication. After receiving shared bounding box proposals from communicating vehicles and feature data from other N − 1 agents, the i-th agent use an roadside stations. This module facilitated the prediction of the intermediate fusion algorithm F

object’s state directly to the current time step, utilizing the InterFusion\(·\) to generate the

fused CP feature data Ht

Constant Turn Rate and Acceleration motion model within the i :

spatial coordinate frame of the objects. Similarly, in the realm Ht = F

F t N

. 

i

InterFusion

k

\(7\)

of cooperative tracking for multiple vehicles, the study pre-k=1

sented in \[106\] extended a Gaussian Mixture Probability Hy-Finally, the fused CP feature Hti is fed into the decoder pothesis Density \(GM-PHD\) filter with a collaborative fusion FDecoder\(·\) to obtain the final CP result Y ti at the i-th agent: algorithm. State propagation relied on the Constant Turn Rate Y t = F

. 

and Velocity motion model, accommodating variable delays i

Decoder

Hti

\(8\)

in wireless communication by condensing the communicating tracks into GM-PHD densities. It is noteworthy, however, that these motion models, while effective in their own right, impose III. DEVELOPMENT OF COOPERATIVE PERCEPTION: FROM

significant constraints that limit their applicability within the EARLY TIME EXPLORATION TILL RECENT RESEARCH

domain of vehicular motion. 

CP involves the exchange of detected obstacles or percep-The rule-based algorithm, devoid of a learning process, tion data among agents, thereby expanding their perceptual offers a computationally efficient approach with demonstrated range, enhancing situational awareness, and ensuring safety engineering viability. In \[107\], an engineering-focused multi-

\[101\]. In the context of driving automation, Cooperative modal CP system was introduced to facilitate cooperative Prediction entails receiving intention or desired trajectory autonomous driving. This system employed a mirror-neuron-information from neighbouring vehicles, thereby enhancing inspired intention awareness algorithm. The mirror neuron the accuracy and efficiency of motion prediction. This ap-concept refers to neurons that activate when an organism per-proach offers the potential to improve strategic ego-planning forms or observes a similar action in others, forming the basis functionality \[102\]. 

for generating intention awareness. Specifically, it enabled In its nascent phase, research in cooperative transporta-all vehicles’ collective synthesis of anticipatory trajectories tion systems primarily centred on devising statistical signal by simulating drivers’ behaviours. However, it is essential to processing and rule-based algorithms, often supplemented by note that this approach relied heavily on precise estimation data from artificial sources or other sensors such as radar and outcomes from each agent within the vehicular network due LiDAR. For example, a study outlined in \[103\] introduced to its use of track-level data fusion, potentially affecting model a particle filter-based multi-target tracking framework that effectiveness. 

expanded detection range by utilizing artificial radar mea-Many conventional methods face challenges in effectively surements and facilitated vehicle position sharing via V2V

extracting attributes from shared information that accurately communication. Simulation outcomes underscored CP’s poten-represent the necessary entities for fulfilling the requirements tial to enhance the performance of intelligent vehicle systems of driver assistance systems. In recent years, deep learn-by amalgamating information from multiple vehicles, thus ing technology has demonstrated significant advancements in complementing single-vehicle detection systems. Similarly, in single-vehicle perception. As a result, numerous researchers

\[104\], research aimed to construct a synthesized representation have been actively involved in developing learning-based of the surrounding environment for multi-vehicle CP. This was CP frameworks to overcome the limitations of traditional achieved by transforming the visual perspectives of two vehi-approaches. For instance, in the realm of cooperative object decles into a shared spatial reference system predicated on the tection and classification, researchers have leveraged advanced estimated relative positions between the two vehicles. Subse-deep learning techniques such as the YOLO network \[108\] and quently, a laser line was employed to generate an approximate DenseNet \[109\] to extract 3D information from shared objects depth map of visual perceptions, establishing correspondence

\[110\]. Further discussion on recent research in this area will between the images. This innovative algorithm conferred the be presented in Sections IV and V. 

ego vehicle with the ability to perceive objects obstructed Traditional approaches in CP have typically relied on late in the foreground. Nevertheless, it had notable limitations, collaboration strategies due to the complexity of feature primarily stemming from imprecise pose estimation and the extraction and limited communication capabilities. With the use of an approximate depth map. 

rapid progress of deep learning, intermediate collaboration CP can be viewed as a mechanism designed to tackle the has gained prominence in multi-agent cooperation, primarily challenge of map merging, aligning perception data across due to its ability to alleviate the burden on communication multiple agents, and integrating it into a consistent refer-resources \[111\]. Nevertheless, it risks introducing extraneous ence frame \[105\]. Achieving precise results in this context and unnecessary information, particularly in dynamic net-

7

Fig. 5. The modern generic framework of the cooperative perception for autonomous driving. 

working conditions. To address this challenge, optimizing The collaboration stage encompasses four primary compo-cooperative information and collaborator selection becomes nents, as depicted in Fig. 5: preparation for transmission, V2X

imperative within a CP system. Furthermore, deep representa-communication, cooperative information alignment, and per-tion introduces higher levels of abstraction and implicitness in ception information fusion. To ensure efficient communication the spatial interactions between agents, necessitating suitable while preserving the accuracy of the cooperation system, the data alignment and information fusion algorithms. Developing initial step involves carefully selecting suitable cooperative a unified CP framework to address these issues is of significant agents and pertinent perceptual information. Subsequently, importance in advancing Cooperative Driving Automation each agent shares the CAM and the refined CPM with its peers \(CDA\). 

through V2X communication \[114\]. Following this, the ego vehicle aligns the acquired perception information with local data through coordinate conversion or pose transformation IV. MODERN GENERIC FRAMEWORK OF COOPERATIVE

techniques. Finally, the aggregated data undergoes consolida-PERCEPTION

tion via a fusion algorithm, followed by decoding, resulting This section introduces a contemporary and comprehensive in a conclusive perception outcome. Note that all CAVs can framework for CP in autonomous driving, along with relevant transmit their perceptual data to a roadside infrastructure via issues and methodologies. 

V2X networks. The associated edge computing infrastructure is responsible for aggregating and consolidating this incoming data, which is then distributed to CAVs according to their A. Framework Overview

specific needs. In the subsequent sections, we provide detailed Given multiple agents capable of perception and commu-insights and a review of existing works on the collaboration nication within a shared environment, the objective is to stage’s primary components. 

enhance each agent’s perceptual accuracy through distributed cooperation. Fig. 5 illustrates the operational process of the proposed framework, comprising two major stages: single-B. Preparation for Transmission

agent perception and multi-agent collaboration. 

During the single-agent perception phase, each agent ac-In CP systems, continuous information exchange among quires measurements of its Six Degrees-of-Freedom pose multiple agents is crucial for achieving comprehensive traffic while simultaneously perceiving the surrounding environment. 

awareness. However, real-world application scenarios often Communication messages are generated by packaging Co-face limitations in communication bandwidth. Excessive net-operative Awareness Messages \(CAMs\) \[112\] and Collective work load increases the risk of important data packets being Perception Messages \(CPMs\) \[113\]. CAM messages convey delayed or lost, which could compromise the performance and the agent’s status, encompassing information such as position safety of CP systems. Therefore, it is essential to balance and motion state, while CPM messages provide additional the trade-off between perception performance and communi-details regarding objects detected through sensor data, such cation efficiency. To address this challenge, researchers have as other vehicles and pedestrians. It is worth noting that the proposed various strategies aimed at reducing the volume of content of perceptual information may encompass raw sensor shared data prior to transmission and alleviating the burden observations, intermediate features, and/or detection outcomes, on vehicular networks. As summarized in Table III, these contingent upon the chosen style of cooperation. 

strategies can be grouped into four main approaches:

8

TABLE III

SUMMARY OF THE METHODS OF PREPARATION FOR TRANSMISSION. 

Category

Method

Year

Scenario

Modality

Dataset/Simulator

Cooperation Style

Downstream Task

Available Code

√

Who2com \[115\]

2020

−

Camera

AirSim-CP

Intermediate

Segmentation

√

When2com \[116\]

2020

−

Camera

AirSim-MAP

Intermediate

Segmentation

CPOB-LearnCom \[117\]

2022

V2I

LiDAR

CARLA-3D

Intermediate

Detection

×

AVUCB \[118\]

2022

V2X

Camera

MS-COCO

Early

Detection

×

CAS

MASS \[119\]

2023

V2V

LiDAR

DOLPHINS

Early

Detection

×

SelectComm \[120\]

2023

V2V

LiDAR

AUTOCASTSIM

Intermediate

Detection

×

√

IoSI-CP \[121\]

2023

V2X

LiDAR

OPV2V,V2XSet

Intermediate

Detection

InterCoop \[122\]

2024

V2V

LiDAR

CARLA

Intermediate

Decision-making

×

DyDisse \[123\]

2019

V2X

Camera/LiDAR

−

Late

Tracking

×

VehIdenti \[124\]

2023

V2X

−

CARTERY

−

−

×

RedunMitig \[125\]

2019

V2X

−

SUMO

Late

Detection

×

Look-ahead \[126\]

2019

V2X

−

SUMO

Late

Detection

×

√

AICP \[127\]

2022

V2V

Camera

−

Late

Detection,Tracking

Early& 

DFS \[128\]

2023

V2X

LiDAR

CARTI

Detection

×

Intermediate & Late

√

BM2CP \[129\]

2023

V2V

LiDAR & Camera

OPV2V, DAIR-V2X

Intermediate

Detection

PIS

DRLCP \[130\]

2020

V2X

Camera

CIVS

Late

−

×

√

FPV-RCNN \[131\]

2022

V2V

LiDAR

COMAP

Intermediate

Detection

√

UMC \[132\]

2023

V2X

LiDAR

V2X-Sim,OPV2V

Intermediate

Detection

Detection, 

GevBEV \[133\]

2023

V2V

LiDAR

OPV2V

Late

×

Segmentation

DAIR-V2X, V2XSet, 

√

IFTR \[134\]

2024

V2X

Camera

Intermediate

Detection

OPV2V

√

CodeFilling \[135\]

2024

V2X

Camera & LiDAR

DAIR-V2X, OPV2VH\+

Intermediate

Detection

V2X-PC \[136\]

2024

V2X

LiDAR

DAIR-V2X, V2XSet

Early

Detection

×

PAE \[137\]

2024

V2X

LiDAR

CARTI

Intermediate

Detection

×

√

ActFormer \[138\]

2024

V2X

Camera

V2X-Sim

Intermediate

Detection

V2X-Sim,DAIR-V2X, 

√

AIS

Where2comm \[139\]

2022

V2X

Camera/LiDAR

Intermediate

Detection

OPV2V,CoPerception-UAVs

Detection, 

V2VNet \[140\]

2020

V2V

LiDAR

V2V-Sim

Intermediate

×

Motion Prediction

CODS \[141\]

2023

V2V

Camera & LiDAR

CARLA

Intermediate

Detection

×

CPSC \[142\]

2024

V2X

LiDAR

DAIR-V2X, OPV2V

Intermediate

Detection

×

FS-COD \[143\]

2020

V2V

LiDAR

CARLA

Intermediate

Detection

×

√

DiscoNet \[144\]

2021

V2V

LiDAR

V2X-Sim

Intermediate

Detection

√

PIC

V2X-ViT \[145\]

2022

V2X

LiDAR

V2XSet

Intermediate

Detection

√

COOPERNAUT \[146\]

2022

V2V

LiDAR

AUTOCASTSIM

Intermediate

Policy Learning

CenterCoop \[147\]

2024

V2I

LiDAR

DAIR-V2X

Intermediate

Detection

×

Slim-FCP \[148\]

2022

V2V

LiDAR

KITTI, T&J

Intermediate

Detection

×

EMIFF \[149\]

2024

V2X

Camera

DAIR-V2X

Intermediate

Detection

×

DAIR-V2X,V2XSet, 

What2comm \[150\]

2023

V2X

LiDAR

Intermediate

Detection

×

OPV2V

SmartCooper \[151\]

2024

V2V

Camera

OpenCOOD

Intermediate

Detection

×

Note: CAS: Cooperative Agent Selection, PIS: Perception Information Selection, AIS: Agent and Information Selection, PIC: Perception Information Compression. 

• Cooperative Agent Selection: This approach focuses on volves compressing or encoding essential information be-minimizing communication costs by transmitting per-fore sharing, ensuring that the transmission rate remains ception data through a partially connected agent graph, within the required data rate limits. 

thereby reducing redundancy within the network. 

1\) Cooperative Agent Selection: Selecting the right col-

• Perception Information Selection: This category aims to laborators is crucial because inappropriate candidates can select a subset of perceptive data critical to the ego cause disruptions and disturbances that could harm overall vehicle’s situational awareness. It focuses on maximizing performance. 

informativeness, which refers to the quality of informa-The attention mechanism, recognized for its efficacy in im-tion, specifically the extent to which the data is relevant, proving model efficiency by focusing on relevant data, offers valuable, and reliable in enhancing perception accuracy. 

promise in selecting suitable agents for the ego CAV. In this

• Agent and Information Selection: This category encom-context, a multi-stage handshake communication mechanism passes a joint consideration of both cooperative agent was proposed in Who2com \[115\], employing the general selection and perception information selection, aiming to attention mechanism \[152\] to select the appropriate collab-balance communication efficiency and data importance. 

orators. This mechanism computes matching scores among

• Perception Information Compression: This strategy in-agents, selectively engaging the most pertinent agents to

9

optimize bandwidth usage. Based on Who2com, When2com computes an interaction score for each vehicle by analyzing

\[116\] introduced scaled general attention to ascertain optimal the geometric properties of the road network in conjunction communication timings, enabling the ego agent to initiate com-with the temporal dynamics of the trajectories, prioritizing munication solely under conditions of insufficient information, those most relevant to the prevailing driving conditions. 

thereby conserving network resources efficiently. Although 2\) Perception Information Selection: The selection of tar-this multi-stage communication process proves effective, its geted information for the ego vehicle is another essential implementation and optimization in dynamically varying en-factor in efficient CP. Recently, a growing focus has been vironments pose significant challenges. To address these chal-on the selection of cooperative message content to improve lenges, \[117\] proposed a dynamic communication mechanism communication efficiency. A number of methods have emerged that allows vehicles to dynamically determine which infras-for selecting or generating CPMs intended for transmission. 

tructures to communicate with based on the learned attention These methods can be broadly categorized into rule-based, weights, thus striking a balance between detection accuracy distance-based, and learning-based approaches, each rooted in and communication spectrum resources. 

distinct mechanisms and theoretical principles. 

To minimize energy consumption, the data sharing schedul-The rule-based approach to CPM generation/selection ening problem can be framed as a variant of the Multi-Armed tails designing rules that dictate which aspects of detected Bandit \(MAB\) problem \[153\], factoring in perception per-object information should be included in a CPM. For example, formance, time-varying wireless channels, and power con-the work in \[123\] proposed a rule that transmits information sumption. In this regard, an online learning-based algorithm about an object’s mode only if the object is turning or accel-known as the Adaptive Volatile Upper Confidence Bound erating. Similarly, in \[124\], visual information from detected \(AVUCB\) \[118\] was proposed to schedule the most advan-vehicles was used to determine their communication IDs, tageous vehicle, offering an enhanced view while adhering which are then used to integrate CPMs with local perception to communication bandwidth constraints. However, it does information. All detected vehicles that have exchanged CAM

not account for the high mobility of cooperative vehicles. 

messages will not be considered in future CPMs. Standardiza-To address this issue, the Mobility-Aware Sensor Scheduling tion efforts, led by the European Telecommunications Stan-

\(MASS\) algorithm \[119\] formulated decentralized CP schedul-dards Institute \(ETSI\), have also introduced CPM generation ing as a Restless-MAB \(RMAB\) problem \[154\]. In the RMAB

rules, specifying what information CPMs should include and context, rewards continually evolve, requiring each vehicle when to generate new messages. The work in \[125\] and to continuously learn about its surroundings while selecting

\[126\] has proposed improved algorithms for these rules to actions that empirically maximize rewards. When applied to a filter out redundant information about detected objects that practical SUMO trace, the MASS algorithm demonstrated the nearby vehicles have recently transmitted. While rule-based ability to enhance overall perception gain without incurring methods are straightforward to implement, they rely primarily additional costs associated with frequent meta-information on changes in the position and speed of detected objects. 

exchanges. 

Distance-based methods prioritize data based on distance Cooperative agent selection can also be likened to a Multi-metrics, considering the spatial location relative to the ego ve-agent Path Finding \(MAPF\) problem, which plans paths for hicle’s onboard sensors to measure data point significance. For multiple agents \[155\]. Inspired by MAPF, a selective com-instance, the Augmented Informative Collaborative Perception munication algorithm \[120\] was proposed to determine the \(AICP\) system \[127\] employed a fitness sorting algorithm subset of cooperative vehicles based on information gains based on Mahalanobis distance to select crucial information from connected vehicles. The ego-vehicle estimates informa-at the application level, effectively filtering out less relevant tion gains by comparing its detected objects’ positions to packets with minimal delay. In a separate approach, Dynamic received 2D centre positions from other connected vehicles. 

Feature Sharing \(DFS\) \[128\] identified relevant feature data The vehicles associated with the highest information gain for sharing through Random-K priorities based on Manhattan are selected to form the communication scope. In contrast to distance. DFS incorporated early, intermediate, and late fusion random selection, this algorithm achieved higher success rates strategies within the CP system to optimize dynamic node with minimal additional communication costs. 

engagement. 

All the aforementioned methods primarily focused on spa-While distance-based methods emphasize the transmission tial correlations, overlooking the significance of temporal of feature cells or data points close to the ego vehicle, they may dependencies in collaborator selection. To address this gap, only partially meet the ego vehicles’ perception information IoSI-CP \[121\] capitalized on the importance of semantic in-requirements in real-world scenarios. In contrast, learning-formation from both temporal and spatial dimensions to select based approaches leverage the entirety of perception data to optimal collaborators. This approach leveraged a Graph Neural intelligently determine information selection for sharing. In Network \(GNN\) to capture inherent correlations between the BM2CP \[129\], a modality-guided collaboration was designed ego vehicle and its neighbouring agents. Agents with weights to selectively share the most critical multi-modal features of zero or lower were considered ineligible for collabora-across agents, thereby promoting communication efficiency. 

tion, which eliminates unsuitable collaborators responsible for This was achieved by generating a preference threshold mask noise. Nevertheless, this approach relied on one-dimensional to filter BEV features. Deep Reinforcement Learning \(DRL\) weights that may not fully capture the intricacies addressed allows agents to learn policies through interactions with by high-dimensional representation methods. InterCoop \[122\]

their environment, maximizing cumulative rewards \[156\]–

10

\[158\]. The work \[130\] introduced a DRL-based Cooperative bandwidth in CP. One such approach, Where2comm \[139\], 

Perception \(DRLCP\) scheme, where each CAV intelligently introduces a spatial-confidence-aware CP framework that em-decides what information to transmit based on the context ploys spatial confidence maps generated by each agent to captured by its onboard sensors. DRLCP’s primary objective identify perceptually critical regions in the feature map. These is to determine whether to transmit or discard data, but it was critical features are compactly packaged into messages and evaluated on only two road networks without considering the shared via a sparsely connected communication graph. A impact of obstructions on vehicular communications. 

communication graph construction strategy is employed to Another

category

of

learning-based

approaches, 

the

selectively determine communication partners, thereby mini-selective-region mechanism, focuses on selecting CPM in-mizing unnecessary bandwidth usage. Furthermore, only non-formation within appropriate communication regions. For in-zero features and their corresponding indices are transmitted. 

stance, \[131\] employed a bounding box matching module and Experimental results indicate that Where2comm effectively strategic critical point selection to choose features enclosed facilitates mutually beneficial cooperation by sharing spatially within bounding box proposals for transmission. In contrast, sparse yet crucial features through V2X communication, op-UMC \[132\] introduced the Entropy-CS, a trainable region-timizing both perception accuracy and communication effi-wise communication selection module, leveraging entropy to ciency. 

distinguish informative regions and select suitable regions 4\) Perception

Information

Compression:

Compression

for transmission based on resolution levels. GevBEV \[133\]

techniques can effectively prioritize and retain the most critical used evidential BEV maps to identify areas where the ego features of perception data, ensuring that even with reduced vehicle needs additional information, applying evidential deep data size, the essential information required for perception learning with Dirichlet evidence \[159\] to quantify point-tasks is preserved. For example, V2VNet \[140\] utilized a based classification uncertainty, thereby highlighting the most variational image compression algorithm \[160\] to compress relevant regions for communication. 

feature maps. In \[141\], the feature maps from each vehicle Foreground regions contain more informative content than are compressed through quantization to reduce communication background regions. Based on this principle, the IFTR \[134\]

costs. This on-demand sharing mechanism enabled efficient employed a message selection and feature map reconstruction cooperation among connected vehicles by selectively sharing module to share the most relevant visual features from the compressed feature maps but ignored the integration of spatial-foreground regions. In CodeFilling \[135\], the information-temporal information. CPSC \[142\] performed feature-level filling-driven message selection was designed to determine the compression by focusing on critical regions of perceptual ego vehicle’s perceptual needs by solving a local optimiza-information in the spatial-temporal domain while adapting the tion problem based on the information score map gathered data transmission strategy based on network conditions. 

from other agents. An optimized selection matrix is produced Feature encoding using Convolutional Neural Networks to dictate which spatial regions should be prioritized for \(CNNs\) is a widely adopted method for feature compression. 

transmission. Spatial selection transmits only the informative FS-COD \[143\] employed a filter at the last layer of the CNN-regions identified by spatial confidence maps, but as bandwidth based feature extractor to control the size of the shared data constraints become more stringent, this approach may lead between cooperative vehicles. DiscoNet \[144\] used a 1 × 1

to the potential loss of objects \[136\]. In contrast, V2X-PC

convolutional autoencoder \[161\] to compress feature maps

\[136\] introduced a Point Cluster Packing module to control along the channel dimension, while V2X-ViT \[145\] applied bandwidth usage by sampling important points. The point multiple 1 × 1 convolutional filters for the same purpose. 

cluster representation preserves object features during message COOPERNAUT \[146\] introduced a Point Encoder using the packing, enables efficient message aggregation regardless of Point Transformer \[162\] to compress point clouds into com-collaboration range, and allows for explicit communication of pact representations, filtering partially processed data to bal-object structure information. 

ance perception accuracy and communication load. Similarly, Attention mechanism enables a single agent to intelli-CenterCoop \[147\] encoded informative cues from the entire gently identify the most relevant perception information from BEV context into compact center representations, significantly multiple agents. For example, the pillar attention encoder reducing communication costs by transmitting these compact \(PAE\) \[137\] extracted the attention value of each feature center features as queries instead of the entire feature map. 

as an importance indicator and selected the most important While CNN-generated feature maps offer potential data features for transmission based on communication bandwidth. 

volume reduction, their dimensions often exceed transmission In ActFormer \[138\], an active selection network was proposed feasibility within current V2X technology scopes \[148\]. In to assign each query with an interest score, which indicates

\[148\], the SENet channel attention module \[163\] was used to the relevance and significance of each feature for the ego’s weigh channel importance, determining optimal channels for perception. This method actively selects the most relevant transmission based on attention weights and the uniqueness sensory data from multiple robots based on spatial knowledge of semantic information. EMIFF \[149\] introduced a Feature without relying on the sensory measurements themselves, Compression module with channel and spatial compression which improves the efficiency of multi-agent object detection. 

blocks for transmission efficiency. Although these approaches 3\) Agent and Information Selection: Methods that consider effectively reduced the necessary transmission bandwidth, they both cooperative agent and information selection jointly can did not account for the heterogeneity of transmitted infor-offer a more balanced approach to optimizing precision and mation resulting from configuration disparities among agents

11

\[164\]. To address this issue, What2comm \[150\] introduced a\) Bandwidth and Spectrum Constraints: CP demands

a communication mechanism based on feature decoupling real-time, high-quality data, often involving high-resolution that strategically minimizes bandwidth usage by eliminating inputs from sensors such as LiDAR and radar, which places background noise to isolate sparse yet essential exclusive fea-significant data rate requirements on communication systems. 

tures and by compressing common features along the channel Achieving high data rates typically requires large bandwidth, dimension. 

stable transmission channels, and precise channel detection The aforementioned compression methods have uniformly and estimation. DSRC operates within the 5.9 GHz frequency applied the same compression ratio to all CAV data, but this band with a total bandwidth of 75 MHz, divided into seven fairness approach fails to account for the varying contributions 10 MHz channels \(5.850 − 5.925 GHz\). However, due to of CAVs to perception during data fusion \[165\]. SmartCooper high vehicle mobility, dynamic environmental changes, and

\[151\] optimized vehicle connectivity while considering com-multipath delay spread, DSRCs communication channels are munication constraints, using a learnable encoder to dynam-highly time- and frequency-selective \[172\]. Studies estimate ically adjust the compression ratio based on channel state that up to 50% of the coherence bandwidth is in the order information and employing a judger mechanism to filter out of 1 MHz, with coherence times as short as 0.2 ms \[172\], 

detrimental image data. 

limiting reliable transmission times and increasing dropout rates. Similar constraints affect C-V2X, which operates on C. V2X Communication

a narrower 30 MHz spectrum \(5.895 − 5.925 GHz\) \[173\]. 

CP depends on V2X communication technologies to faThe PC5 mode of C-V2X offers an advantage by utilizing a cilitate real-time information exchange among vehicles, in-blind hybrid automatic repeat request \(HARQ\) technique that frastructure, and other road users. Dedicated Short-Range combines turbo coding \(providing better performance than the Communications \(DSRC\) and Cellular V2X \(C-V2X\) are two convolutional coding used in DSRC\) with automatic repeat key technologies that support the low-latency and scalable request error control and soft-combining \[174\]. 

communication needed in CP systems. Each technology has Addressing these challenges requires improved network distinct features and challenges, which are explored below, planning and advanced channel detection and estimation tech-followed by an analysis of how these limitations impact CP

niques. For DSRC, \[175\] proposes an analytical model to performance and the primary development bottlenecks in V2X

assess key metrics such as Channel Busy Ratio and Packet communication. A comparison of the key technical differences Delivery Ratio over distance, facilitating optimized network between DSRC and C-V2X is presented in \[166\]. 

planning. Additionally, \[176\] enhances IEEE 802.11p through 1\) DSRC: DSRC was designed specifically for vehicle an OFDM-IM system that strategically positions pilot signals communication, adapting Wi-Fi technology into the IEEE

and leverages inactive channels to increase detection accuracy, 802.11p protocol \[167\]. Operating in the 5.9 GHz band, DSRC

while \[177\] introduces a low-complexity, high-speed deep enables fast, two-way communication over short distances neural network-augmented least square algorithm, effectively among vehicles, infrastructure, and other road users. Its decen-reducing model size and latency while improving accuracy tralized design enables direct data exchange between vehicles under varied noise levels and channel conditions. For C-without relying on a central network, minimizing latency V2X, \[178\] proposes a balanced resource allocation strategy

\[167\], but the communication range is limited to less than that evenly distributes resources across subframes, decreasing 1km, and the link capacity is less than 10 Mbps \[168\]. Thus, packet loss and enhancing data throughput. Similarly, \[179\]

DSRC can be used to implement Applications that require suggests a pilot design with zero-correlation zone sequences minimum latency, like collision warnings \[166\]. 

and a time-domain channel estimation approach to mitigate 2\) C-V2X: C-V2X, standardized by the 3rd Generation co-channel interference in C-V2X systems. 

Partnership Project \(3GPP\), enables broad V2X interactions b\) Latency and Synchronization: CP requires low latency encompassing V2V, V2I, V2N, and V2P connections. It op-and precise timing to ensure synchronized data fusion across erates in two modes defined in 3GPP Releases 14 through vehicles. Although DSRC and C-V2X are both designed to 16: Direct Communication \(PC5 interface\) and Network Com-minimize latency, high-density environments, network conges-munication \(Uu interface\) \[169\]–\[171\]. The PC5 interface tion, and physical obstructions can introduce delays. Studies enables direct communication between vehicles and nearby indicate that DSRC and C-V2X can support applications infrastructure in the 5.9 GHz band, ideal for low-latency, with an end-to-end latency of approximately 100 millisec-localized applications such as crash avoidance and real-time onds under moderate vehicular density \[180\]. However, CP

safety alerts. The Uu interface, meanwhile, connects vehicles demands stricter latency and high-quality service standards to to broader V2N applications through LTE or 5G networks, function effectively. Additionally, synchronization challenges supporting long-range data exchange for services like traffic arise when fusing data from multiple agents, often leading to management and infotainment, particularly for non-latency-temporal mismatches that degrade CP accuracy. Both DSRC

sensitive applications. 

and C-V2X utilize the Global Navigation Satellite System 3\) Impact of V2X on CP: V2X communication enables

\(GNSS\) for time synchronization, but DSRC operates with data sharing, which is essential for CP, but it faces limitations looser timing and asynchronous communication, while C-V2X

that restrict CPs full potential. Key challenges impacting CP

adheres to stricter time standards \[166\]. Despite these efforts, performance are bandwidth and spectrum constraints, as well network congestion can still impact latency and synchroniza-as latency and synchronization issues. 

tion reliability. 

12

To address congestion in DSRC, \[181\] proposes adjust-where Rz\(α\), Ry\(β\), and Rx\(γ\) are the basis rotation ments to vehicle settings based on information from supple-matrices around the z, y, and x axes, respectively: mentary channels, enabling lead vehicles to monitor hidden

cos\(α\) − sin\(α\) 0

nodes in a group. Furthermore, \[182\] presents a congestion-Rz\(α\) =

sin\(α\)

cos\(α\)

0 , 





\(11\)

aware forwarding scheme that optimizes multi-hop forwarding 0

0

1

reliability and reduces latency under heavy network load. 





In C-V2X, \[179\] introduces a rate control mechanism that cos\(β\)

0

sin\(β\)

allows power control to actively contribute to congestion Ry\(β\) =

0

1

0

, 





\(12\)

management, while \[183\] suggests a DQN-based adaptive

− sin\(β\)

0

cos\(β\)

congestion control algorithm, where a central controller trains

1

0

0



and distributes the policy, improving QoS compliance over R

0

cos\(γ\)

− sin\(γ\) . 

\(13\)

ETSIs Distributed Congestion Control in dense traffic scenar-x\(γ\) = 



0

sin\(γ\)

cos\(γ\)

ios. For synchronization, \[184\] offers a decentralized clock synchronization protocol to enhance DSRCs resilience against Based on \(9\), the transformation matrices TA and TB for GPS spoofing and improve reliability when GNSS signals agents A and B can be derived from their respective poses. To are unavailable. Meanwhile, \[185\] proposes a synchronization find the relative transformation matrix TB→A, multiply the signal design that uses generalized reciprocal sequences for inverse of TB by TA:

mmWave C-V2X. This approach enhances OFDM-based V2V

TB→A = T−1 · TA. 

\(14\)

synchronization by achieving high detection accuracy, mini-B

mizing interference, and reducing computational complexity. 

Each data point from agent B’s perspective is represented as pB = \[a, b, c\]. Converting these 3D points to homogeneous coordinates by appending a 1 as the fourth element yields D. Cooperative Information Alignment

pB = \[a, b, c, 1\]T. To align each data point with the ego Cooperative information alignment is crucial for CP sys-vehicle’s frame, multiply it by TB→A:

tems in autonomous driving to ensure that shared data from p = TB→A · pB, 

\(15\)

different sources are accurately represented within a common coordinate system \[186\]. This process is essential for fusing where p is the transformed point in the ego agent’s coordinate information from multiple agents to achieve a unified under-frame. This alignment enables the direct fusion of incoming standing of the environment. 

data from other agents with the ego’s data, as all points are now within the same coordinate system. 

1\) Data Alignment: Each collaborative agent typically op-2\) Alignment for Pose Errors: Accurate relative transfor-erates within its local coordinate system, which may differ in mation matrices are foundational for ensuring alignment in both position and orientation relative to the ego agent. Data a shared coordinate system. However, these matrices depend shared from cooperative agents, whether raw data, intermedion sensor measurements from posture detection systems such ate features, or perception outcomes, is initially referenced in as Global Positioning System \(GPS\) and Inertial Measurement each agent’s local frame. To align the cooperative data from a Unit \(IMU\), which are prone to noise and accuracy limitations, collaborative agent \(Agent B\) with the ego vehicle \(Agent A\), potentially leading to misalignment and reduced perception the messages transmitted must include the sender’s position performance \[187\]. 

and its orientation. Upon receiving data and pose information Many efforts have been undertaken to address pose errors, from the collaborative agent, the ego agent calculates a relative as summarized in Table IV. A widely adopted approach transformation matrix, T

involves statistical learning models. For instance, the method B→A, to map the incoming data into

the ego agent’s coordinate frame. 

presented in \[188\] corrected relative locations between two To compute T

CAVs by matching key points in their perception results B→A, it is essential first to establish the transformation matrix T that projects each agent’s local coordinate with the Random Sample Consensus \(RANSAC\) algorithm system onto the global coordinate frame. This matrix incorpo-

\[200\]. While effective, this approach required the setting of rates both rotation and translation components, determined by problem-specific thresholds. Based on V2VNet \[140\], a con-each agent’s global position \[x, y, z\] and orientation angles α, sistency module \[189\] was introduced to enhance relative pose β, and γ \(representing yaw, pitch, and roll, respectively\). The estimations by structuring the global coherence of absolute transformation matrix T is constructed as follows: poses as a Markov random field and incorporating Bayesian reweighting. Unfortunately, this model relies on ground-truth

r



11

r12

r13

x

poses during the training phase, which may be limited in r

T =  21

r22

r23

y

practical scenarios. CoAlign \[190\] proposed an Agent-Object



, 

\(9\)

r





31

r32

r33

z

Pose Graph Optimization method to improve pose consistency 0

0

0

1

using a pose graph and optimization techniques. RoCo \[191\]

where r

modelled the pose correction problem as an object-matching ij \(i, j

∈ \{1, 2, 3\}\) denotes the entries of the 3D

rotation matrix R, which can be calculated as:

task that reliably associates common objects detected by different agents, iteratively adjusting the agent poses to minimize R = Rz\(α\) · Ry\(β\) · Rx\(γ\), 

\(10\)

alignment errors of the associated objects. These two methods

13

TABLE IV

SUMMARY OF THE WORKS OF COOPERATIVE INFORMATION ALIGNMENT FOR POSE ERRORS. 

Method

Year

Scenario

Modality

Dataset/Simulator

Cooperation Style

Downstream Task

Available Code

RANSAC-based \[188\]

2022

V2V

LiDAR

COMAP

Late

Detection, Location

×

V2VNetrobust \[189\]

2021

V2V

LiDAR

V2V-Sim

Intermediate

Detection, Motion Prediction

×

√

CoAlign \[190\]

2022

V2X

LiDAR

OPV2V,V2X-Sim,DAIR-V2X

Intermediate

Detection

√

RoCo \[191\]

2024

V2X

LiDAR

DAIR-V2X, V2XSet

Intermediate

Detection

ICP&OP \[192\]

2022

V2V

LiDAR

OPV2V

Late

Detection

×

V2X-PC \[136\]

2024

V2X

LiDAR

DAIR-V2X, V2XSet

Early

Detection

×

√

CoBEVGlue \[193\]

2024

V2X

LiDAR

OPV2V,DAIR-V2X,V2V4Real

Intermediate

Detection

Map Container \[194\]

2022

V2X

Camera,LiDAR

VISSIM

Late

State Estimation

×

√

FreeAlign \[195\]

2024

V2X

LiDAR

OPV2V, DAIR-V2X

Intermediate

Detection

√

SCOPE \[196\]

2023

V2X

LiDAR

OPV2V,V2XSet,DAIR-V2X

Intermediate

Detection

√

V2X-ViT \[145\]

2022

V2X

LiDAR

V2XSet

Intermediate

Detection

EMIFF \[149\]

2024

V2X

Camera

DAIR-V2X

Intermediate

Detection

×

√

CBM \[197\]

2024

V2V

Camera,LiDAR

SIND, OPV2V

Late

Detection

KM-based \[198\]

2024

V2V

Camera

KITTI, PreScan

Late

Detection

×

√

DMGM \[199\]

2023

V2V

Camera

CARLA & SUMO

Early

−

effectively mitigated relative pose errors among agents without ness CP framework SCOPE \[196\] was designed to generate requiring precise supervision during training. 

robust representations while accounting for localization errors Point cloud registration methods typically focus on refining through confidence-aware multi-scale feature interaction. Sim-the Iterative Closest Point \(ICP\) algorithm \[201\], widely ilarly, the Multi-scale Window Attention Module in V2X-ViT

used for aligning 3D point clouds. In \[192\], an ICP-based

\[145\] was proposed to capture long-range spatial interactions matching algorithm aligned two point sets, one representing at multiple scales using a pyramid of resolution windows, 3D bounding boxes detected by the Ego and the other by the allowing for local and global spatial feature interactions and sender, with the relative transformation formulated as an opti-improving detection robustness against positioning errors. In mal transport problem \[202\] to minimize transportation costs EMIFF \[149\], the Multi-scale Cross Attention and Camera-between source and target points. V2X-PC \[136\] aligned point aware Channel Masking modules are developed to address clusters from spatial and temporal dimensions and proposed the negative effects of pose errors by selectively integrating parameter-free solutions that can adapt to different noisy levels features, applying spatial offsets, and reweighting features without finetuning. CoBEVGlue \[193\] introduced a spatial based on camera parameters. 

alignment module, BEVGlue, which estimates relative poses Inter-agent object association aims to mitigate localization between agents by matching co-visible objects across agents errors in pose transformation by matching key points or without relying on an external localization system. Unlike objects from connected agents and determining the optimal traditional point cloud registration methods, BEVGlue only relative pose transformation. To facilitate this, the Context-requires the transmission of bounding boxes and tracking IDs, based Matching \(CBM\) algorithm \[197\] generated object clus-reducing communication bandwidth while maintaining high-ters based on bounding box headings and established corre-quality matching by checking the spatial relationship between spondences through iterative pairwise comparison to maximize matched nodes. 

global consensus. The work in \[198\] handled spatial differ-High-definition maps represent a valuable resource for ences using a data association and spatial error calibration achieving precise spatial alignment, primarily due to their method based on the Kuhn-Munkres algorithm. However, ability to provide accurate self-vehicle localization. In this identifying correspondences can be challenging due to visual regard, a map-based CP framework called the “map con-folding, non-visible objects, and noisy perception. To address tainer” was introduced in \[194\], which establishes benchmarks this, \[199\] framed correspondence identification as a graph-for spatiotemporal transformations by automatically mapping matching problem, employing a masked GNN to manage non-multi-agent perceptual information into the map coordinate visible objects, explicitly addressing occlusion and limited space using a map-matching algorithm. Nevertheless, this FoV challenges. 

algorithm relies on the support of monocular cameras and GNSS/IMU devices. FreeAlign \[195\] leveraged the invariant geometric structure composed of objects commonly perceived E. Cooperative Information Fusion

and observed by the individual agents to estimate the relative poses without relying on expensive high-end global localiza-The effectiveness of CP crucially depends on the design tion. 

of an efficient fusion strategy, which aims to consolidate Multi-scale feature interaction can effectively reduce feature shared information to provide coherent and accurate perception map misalignment caused by pose errors by encoding the fea-results. The following will examine recent fusion methods ture into multiple scales and then aggregating them into a final employed in CP information. For reference, Table V provides collaboration feature. In this context, a spatiotemporal aware-a summary of all discussed fusion models in this subsection. 

14

TABLE V

SUMMARY OF THE WORKS OF COOPERATIVE INFORMATION FUSION. 

Method

Year

Scenario

Modality

Dataset/Simulator

Cooperation Style

Downstream Task

Available Code

Cooper \[97\]

2019

V2V

LiDAR

KITTI, T&J

Early

Detection

×

F-Cooper \[203\]

2019

V2V

LiDAR

KITTI, T&J

Intermediate

Detection

×

PillarGrid \[204\]

2022

V2X

LiDAR

CARTI

Intermediate

Detection

×

OPV2V\+, DAIR-V2X, 

√

CoCa3D \[205\]

2023

V2X

Camera

Intermediate

Detection

CoPerception-UAVs\+

SiCP \[206\]

2024

V2X

LiDAR

OPV2V

Intermediate

Detection

×

CoBEVFusion \[207\]

2023

V2V

LiDAR & Camera

OPV2V

Intermediate

Detection, Segmentation

×

V2X-BGN \[208\]

2024

V2X

Camera

V2XSet

Late

Detection

×

CPM-LCF \[209\]

2021

V2X

LiDAR

−

Late

Detection

×

CI-based \[210\]

2022

V2X

LiDAR

CARLA

Late

Tracking

×

√

CPV-RCNN \[211\]

2023

V2X

LiDAR

CARLA

Late

Detection

V2X-PC \[136\]

2024

V2X

LiDAR

DAIR-V2X, V2XSet

Early

Detection

×

√

V2VNet \[140\]

2020

V2V

LiDAR

V2V-Sim

Intermediate

Detection, Motion Prediction

√

DiscoNet \[144\]

2021

V2V

LiDAR

V2X-Sim

Intermediate

Detection

√

V2X-ViT \[145\]

2022

V2X

LiDAR

V2XSet

Intermediate

Detection

HYDRO-3D \[212\]

2023

V2X

LiDAR

V2XSet

Intermediate

Detection

×

GraphAttention \[213\]

2024

V2X

LiDAR

V2X-Sim

Intermediate

Detection

×

√

CoBEVT \[214\]

2022

V2V

Camera

OPV2V

Intermediate

Segmentation

QUEST \[215\]

2024

V2I

Camera

DAIR-V2X

Intermediate

Detection

×

√

COOPERANAUT \[146\]

2022

V2V

LiDAR

AUTOCASTSIM

Intermediate

Policy Learning

V2VFormer \[216\]

2024

V2V

LiDAR & Camera

OPV2V, V2XSim, V2V4Real

Intermediate

Detection

×

V2VFormer\+\+ \[217\]

2024

V2V

LiDAR & Camera

OPV2V, V2XSim

Intermediate

Detection

×

√

MKD-Cooper \[218\]

2023

V2V

LiDAR

OPV2V, V2XSim, Experiment

Intermediate

Detection

√

V2X-AHD \[219\]

2023

V2X

LiDAR

V2Xset

Intermediate

Detection

√

IoSI-CP \[121\]

2023

V2X

LiDAR

OPV2V, V2XSet

Intermediate

Detection

Coop3D-Infra \[220\]

2022

V2I

LiDAR

CARLA

Hybrid

Detection

×

ML-Cooper \[221\]

2022

V2V

LiDAR

KITTI

Hybrid

Detection

×

Hybrid CP \[222\]

2023

V2V

LiDAR

OPV2V

Hybrid

Detection

×

1\) Traditional Fusion: Primary reduction operators, such based on confidence scores without requiring training or as summation, maximum, and average pooling, are widely fitting parameters. V2X-BGN \[208\] used NMS to aggregate used in cooperative information fusion for multi-agent per-redundant detection results from intelligent agents globally, ception. For example, the Cooper \[97\] was developed for based on 2D IoU in BEV space. A rule-based fusion scheme CAVs to enhance 3D object detection using raw point cloud for CPMs was proposed in \[209\] to associate locally detected data, though it involved high data overhead. F-Cooper \[203\]

objects with those identified via V2X communication, de-extended Cooper to the feature level, balancing bandwidth signed for scenarios where CAVs generate CPMs based on constraints and detection accuracy by using max pooling ETSI standards. This scheme utilized a fusion centre to merge for V2V voxel feature fusion. Similarly, PillarGrid \[204\]

and broadcast CPMs to nearby CAVs for further perception applied grid-wise max-pooling to integrate deep features for tasks. 

cooperative 3D object detection. CoCa3D \[205\] used point-The non-parametric fusion methods offer minimal compu-wise maximum fusion to combine BEV features from multiple tational costs but often fail to capture data correlations. In CAVs, enhancing camera-based detection through cooperative contrast, parametric methods generally provide more accu-depth estimation. Besides using these commonly accepted rate and reliable fusion by incorporating measurements and reduction operators, dedicated fusion modules were designed their uncertainties. For instance, the Covariance Intersection to fuse BEV features from CAVs as well. SiCP \[206\] proposed \(CI\) algorithm can consistently fuse estimates without prior a novel Dual-Perception Network \(DP-Net\) to assign different knowledge of cross-correlations. Building on this concept, weights for LiDAR point cloud provided by different CAVs by

\[210\] introduced a CI-based fusion strategy for CP, achieving extracting crucial gradient information requiring only a few pa-consistent fusion of local sensor data and object information rameters. CoBEVFusion \[207\] extended the idea by employing from other agents through V2X communication. 

a dedicated fusion module to combine heterogeneous features In contrast to object-level and BEV-based approaches that gathered from the camera and LiDAR on two CAVs. 

often lead to feature degradation, the Point Cluster Aggre-As the late fusion strategy requires a minimum volume of gation \(PCA\) module in V2X-PC \[136\] preserves the low-exchanged information between CAVs \[211\], several tradi-level structural details of point clusters, thereby improving the tional fusion approaches employing the late fusion strategy accuracy of proposal bounding boxes. PCA integrates point have been explored in practice. In the context of object clusters from multiple agents by matching them based on the detection, non-maximum suppression \(NMS\) serves as a non-distances between cluster centres and merging clusters that parametric method for filtering overlapping bounding boxes represent the same object into a new cluster. Its computational

15

complexity is determined solely by the number of point and a point transformer block for fusing multi-agent perception clusters, without requiring convolution or padding operations, data. Similarly, V2VFormer \[216\] and V2VFormer\+\+ \[217\]

which makes it both effective and efficient for long-range also utilized channel and spatial information based attentions collaborative perception. 

to fuse the features exacted from multiple CAVs. Together with 2\) Graph-based Fusion: Multi-agent collaboration can be knowledge distillation technology, several attention modules represented as a collaboration graph, with nodes as agent were employed to effectively transfer valuable knowledge from states and edges as pairwise collaborations. At the core is multiple excellent teacher models in different views and then the GNN, which extracts relational data and generates node aggregated into the student model on the ego CAV \[218\], 

embeddings using local attributes and neighbouring informa-

\[219\]. 

tion. Node states are continuously updated through inter-node Given the high cost of LiDAR sensors, the study in \[214\]

communication and aggregation. 

proposed a sparse vision transformer framework, CoBEVT, In V2VNet \[140\], each vehicle used a fully connected which uses multi-agent multi-camera features for collaborative GNN \[223\] as an aggregation module for data fusion from BEV segmentation. CoBEVT introduced a 3D vision trans-various viewpoints. Messages were aggregated at each node former that fuses BEV features from multiple agents using using a mask-aware accumulation operator, considering over-the Fused Axial attention module, which integrates global lapping FoVs. However, it employed a scalar-valued edge and local attention mechanisms to capture both long-range weight to indicate the importance of the neural message and detailed regional interactions. QUEST \[215\] followed the from one agent to another, which could not effectively model variable query concept first proposed by DETR \[224\] and the strength of collaboration between two agents. On the extended it to V2I CP settings for camera-based 3D object other hand, DiscoNet \[144\] employed an edge encoder to detection. 

establish correlations between feature maps from different The aforementioned attention-based models have signifi-agents, generating matrix-valued edge weights. The edge en-cantly advanced cooperative information fusion by focusing coder concatenated feature maps and applied convolutional primarily on spatial dimensions. However, their reliance on layers for downsampling, followed by a softmax operation single-frame prediction neglects historical context and over-for normalization. Knowledge distillation enhanced training looks important temporal semantic cues, limiting their ability by aligning intermediate fusion-based student model features to detect fast-moving objects due to point cloud sparsity. To with the early fusion-based teacher model, improving feature address these limitations, SCOPE \[196\] introduced a Context-abstraction and object detection performance. 

aware Information Aggregation model that uses a pyramid The Heterogeneous Multi-agent Self-attention \(HMSA\) LSTM to incorporate spatiotemporal data from previous ego module in V2X-ViT \[145\] fuse cooperative feature by associ-agent frames, generating refined context-aware features. These ating agent types with nodes and edges in a directed graph and features are fused with cooperative features based on com-computing importance weights between nodes accordingly. To plementary contributions and spatial attention maps obtained further enhance CP performance, HYDRO-3D \[212\] extends through max pooling, which may not fully capture correlations the V2X-ViT to create a hybrid object detection and tracking among informative features. To overcome this, IoSP-CP \[121\]

CP model by combining V2X-ViT’s detection features with proposed the Historical Prior Hybrid Attention \(HPHA\) fusion historical tracking data extracted using a spatial-temporal algorithm, comprising a multi-scale transformer and a short-pyramidal 3D network. The combined features improve ro-term attention module. The multi-scale transformer extracts bustness and enhance detection accuracy, as demonstrated in attention weights at different spatial scales, while the short-experiments. 

term attention mechanism captures temporal dependencies Traditional feature fusion methods, such as concatenation and identifies discriminative features, enhancing informative or summation, provide only fixed linear fusion and fail to features while reducing background noise. 

account for the varying importance of feature maps. To address 4\) Hybrid Fusion: Different collaboration schemes have this, \[213\] proposed a graph attention feature fusion network advantages and limitations and can complement each other that selectively emphasizes important regions within feature effectively. However, single-type fusion methods may not fully maps by employing both channel and spatial attention-based exploit the potential for both deep fusion of various data types aggregation. This approach adaptively highlights informative and consuming minimum communication bandwidth by gener-areas, enhancing the ego vehicle’s feature representation and ating higher-level collaborative representations. Hybrid fusion-improving object detection precision. 

based approaches offer promise in harnessing the strengths of 3\) Attention-based Fusion: The attention mechanism in-diverse collaboration schemes by integrating multiple fusion troduced in the transformer model has found widespread methods within a single CP model, thus balancing the accuracy use in determining fusion weights. The Point Transformer and transmission data size. 

\[162\] effectively learns compact representations from 3D point Objects near the onboard sensor typically exhibit a high clouds, excelling at capturing non-local interactions and gen-point density and are more easily detected using data from erating permutation-invariant representations. It is well-suited a single sensor, while distant points tend to be sparse due for aggregating LiDAR point clouds from multiple agents. In to limited sensor visibility. Early collaboration for distant COOPERNAUT \[146\], a point transformer-based representa-regions can improve detection accuracy, as demonstrated by tion aggregator was introduced for information fusion, consist-research \[220\], which proposed a V2I cooperative 3D object ing of a voxel max-pooling operation for spatial aggregation detection model using hybrid fusion. This method transmits

16

TABLE VI

SUMMARY OF THE WORKS ON ISSUES OF COOPERATIVE PERCEPTION AND CORRESPONDING METHODS. 

Category

Method

Year

Scenario

Modality

Dataset/Simulator

Cooperation style

Downstream task

Available Code

√

MAMP \[225\]

2022

V2V

LiDAR

OPV2V

Late

Detection

UDT2T \[226\]

2022

V2V

−

CARLA

Late

Tracking

×

MH

√

MPDA \[227\]

2022

V2X

LiDAR

V2XSet

Intermediate

Detection

√

MACP \[228\]

2024

V2V

LiDAR

V2V4Real, OPV2V

Intermediate

Detection

√

HM-ViT \[164\]

2023

V2V

Camera&LiDAR

OPV2V

Intermediate

Detection

√

DI-V2X \[229\]

2024

V2X

LiDAR

DAIR-V2X, V2XSet

Intermediate

Detection

√

DH

DG-CoPerception \[230\]

2023

V2V

Camera

OPV2V

Intermediate

Segmentation

VINet \[231\]

2022

V2X

LiDAR

CARTI

Intermediate

Detection

×

V2X-M2C \[232\]

2024

V2X

LiDAR

V2XSet, OPV2V

Intermediate

Detection

×

√

VIMI \[233\]

2023

V2I

Camera

DAIR-V2X

Intermediate

Detection

√

MH & DH

HEAL \[234\]

2024

V2X

Camera&LiDAR

OPV2V-H, DAIR-V2X

Intermediate

Detection

V2VAM\+LCRN \[235\]

2022

V2V

LiDAR

OPV2V

Intermediate

Detection

×

V2X-INCOP \[236\]

2024

V2X

LiDAR

V2X-Sim,OPV2V,DAIR-V2X

Intermediate

Detection

×

LC

SsAW \[237\]

2024

V2V

LiDAR

OPV2V, V2V4Real

Intermediate

Detection

×

TempCoBEV \[238\]

2024

V2V

Camera

OPV2V

Intermediate

Segmentation

×

CooperFuse \[239\]

2024

V2X

LiDAR

V2X-real

Late

Detection

×

√

FFNet \[240\]

2023

V2I

LiDAR

DAIR-V2X

Intermediate

Detection

√

SyncNet \[241\]

2022

V2V

LiDAR

V2V-Sim

Intermediate

Detection

√

CoBEVFlow \[242\]

2023

V2V

LiDAR

CARLA, DAIR-V2X

Intermediate

Detection

CD

Detection, 

V2VNet \[140\]

2020

V2V

LiDAR

V2V-Sim

Intermediate

×

Motion Prediction

√

V2X-ViT \[145\]

2022

V2X

LiDAR

V2XSet

Intermediate

Detection

V2X-PC \[136\]

2024

V2X

LiDAR

DAIR-V2X, V2XSet

Early

Detection

×

√

FreeAlign \[195\]

2024

V2X

LiDAR

OPV2V, DAIR-V2X

Intermediate

Detection

√

LC & CD

Ro-temd \[243\]

2024

V2V

LiDAR

OPV2V

Intermediate

Detection

AdversAttack \[244\]

2021

V2V

LiDAR

V2V-Sim

Intermediate

Detection

×

√

ROBOSAC \[245\]

2023

V2X

LiDAR

V2X-Sim

Intermediate

Detection

TrustEsti \[246\]

2019

V2V

Camera/LiDAR

−

−

−

×

DS

FDII \[247\]

2023

V2V

LiDAR

CARLA

Early

Detection

×

√

CAD \[248\]

2024

V2V

LiDAR

Adv-OPV2V, Adv-MCity

Early/Intermediate

Detection

MADE \[249\]

2024

V2V

LiDAR

V2X-sim, DAIR-V2X

Intermediate

Detection

×

Turning

FedAD \[250\]

2023

V2I

Camera

Udacity

−

×

Angle Prediction

√

DP

FedBEVT \[251\]

2023

V2X

Camera

CARLA&OpenCDA

−

Segmentation

FL-CCS \[252\]

2023

V2X

−

−

−

−

×

FedDWA \[253\]

2024

V2X

Camera

CARLA&OpenCDA

−

Segmentation

×

CoPEM \[254\]

2022

V2X

−

ViSTA

Late

Detection

×

DMMCP \[255\]

2023

V2X

Camera/LiDAR

−

Late

Detection, Tracking

×

CMP \[256\]

2024

V2V

LiDAR

OPV2V

Intermediate

Motion Prediction

×

Early

√

PU

Double-M \[257\]

2023

V2X

LiDAR

V2X-Sim

Detection

/Intermediate/Late

GevBEV \[133\]

2023

V2V

LiDAR

OPV2V

Late

Detection, Segmentation

×

MOT-CUP \[258\]

2024

V2X

LiDAR

V2X-Sim

Late

Detection, Tracking

×

√

DMSTrack \[259\]

2024

V2V

LiDAR

V2V4Real

Late

Tracking

GCDA \[260\]

2024

V2V

LiDAR

V2V4Real

Late

Tracking

×

Scene completion, 

√

STAR \[261\]

2022

V2X

LiDAR

V2X-Sim

Intermediate

Detection,Segmentation

TD

Scene completion, 

√

CORE \[262\]

2023

V2V

LiDAR

OPV2V

Intermediate

Detection,Segmentation

S2R-ViT \[263\]

2024

V2V

LiDAR

OPV2V,V2V4Real

Intermediate

Detection

×

S2R

DUSA \[264\]

2023

V2X

LiDAR

V2XSet, DAIR-V2X

Intermediate

Detection

×

Note: MH: Model Heterogeneity, DH: Data Heterogeneity, LC: Lossy Communication, CD: Communication Delays, DS: Data Security, DP: Data Privacy, PU: Perception Uncertainty, TD: Task Discrepancy, S2R: Simulation to Reality. 

raw data \(early fusion\) for low-density areas and shares object-based hybrid collaborative perception strategy. Collaboration level information \(late fusion\) for nearby areas, providing is classified into two types based on the overlap between a cost-effective solution but with limited flexibility in ad-the detection ranges of vehicles. For the overlapping area, justing data sharing. Hybrid CP \[222\] proposed a region-feature-level intermediate collaboration is used by exchanging

17

and fusing features from various CAVs. Late collaboration is heterogeneous perception fusion with varying state spaces, carried out in the non-overlapping area by developing and a CI-based track-to-track fusion approach was proposed in sharing the local detection result with a low communication

\[226\], augmenting low-dimensional tracks and exploring meth-volume. Conversely, ML-Cooper \[221\] employs an improved ods for state augmentation. 

Soft Actor-Critic \[265\] algorithm to optimize V2V bandwidth Late collaboration preserves model privacy by allowing by dynamically adjusting data sharing among raw, feature, agents to train models individually and share outputs, but this and object levels based on channel conditions, enhancing can introduce noise and degrade performance. Intermediate adaptability in dynamic vehicular networks. 

collaboration is more flexible and popular for V2X CP, but feature extractors’ differences can create a domain gap. To V. ISSUES OF COOPERATIVE PERCEPTION AND

overcome this issue, a Multi-agent Perception Domain Adapta-CORRESPONDING METHODS

tion \(MPDA\) framework was introduced in \[227\], incorporating a feature resizer and a sparse cross-domain transformer to While the majority of research on CP for driving automation align and produce domain-invariant features, thereby minimiz-has focused on key aspects of the collaboration process, ing disparities between agents utilizing heterogeneous feature such as communication latency, information alignment, and extraction networks. Inspired by the parameter-efficient fine-fusion strategies, as discussed in the previous section, limited tuning strategy \[266\], MACP \[228\] introduced a Convolution attention has been given to subtle yet crucial challenges Adapter \(ConAda\) to mitigate domain shifts by projecting the that have practical implications for advancing Cooperative source feature map to a lower dimension and then transforming ITS. This section delves into exploring recent findings and it back. Additionally, a single-agent pre-trained model was the corresponding methodologies to address these practical adapted to cooperative settings by freezing most parameters challenges. Table VI provides a comprehensive overview of and adding lightweight modules. While this approach effec-characteristics related to these advancements. 

tively mitigates domain shifts and enhances perception, it may exhibit reduced precision for objects in the 50-100m range due A. Agent Heterogeneity

to inherent biases in the pre-trained model. 

Although CP systems have made significant progress, it 2\) Data Heterogeneity: In practical autonomous driving, is important to acknowledge that these improvements often connected agents often have different sensor modalities: Li-assume that the agents involved are uniform. In reality, it DAR provides precise geometry, while cameras offer rich is difficult to achieve uniformity in agent configuration and semantics. Collaborating with agents with diverse sensors en-sensor equipment across connected agents due to varying hances perception by leveraging complementary information. 

preferences among system developers and automobile man-However, sharing data between camera and LiDAR agents ufacturers. Therefore, it is necessary to prioritize finding introduces semantic disparities, and measurements differ be-solutions to the practical challenges of agent heterogeneity, tween roadside infrastructure and CAVs. Additionally, sensor including model and data discrepancies among agents. 

noise varies due to maintenance and hardware precision, 1\) Model Heterogeneity: Sharing perception models with posing challenges for developing a heterogeneous cooperative identical parameters among agents could raise concerns about system. 

privacy and confidentiality, especially when CAVs come from In a multi-agent hetero-modal setting, connected agents various automotive manufacturers. Even within a single au-have various sensors, forming a dynamic heterogeneous graph tomotive enterprise, variations in vehicle types and model with stochastic sensor types and changing poses across scenes. 

update frequency can result in differences in perception among To handle these challenges, HM-ViT \[164\] introduced the model versions. However, using different models for individual H3GAT module for V2V cooperative 3D detection, which agents can create domain gaps in shared perception data. 

updates node states by extracting inter-agent and intra-agent Neglecting model heterogeneity can significantly reduce the cues using transformer blocks and a hetero-modal MLP layer. 

effectiveness of CP, thereby diminishing the benefits of multi-This allows processing camera and LiDAR features with dis-agent cooperation. 

tinct parameters, enabling flexibility, robustness, and superior Object-level CP frameworks avoid the need for full model performance in scenarios with diverse sensor modalities. 

data exchange by sharing perception results like bounding On the other hand, identical modality sensors can vary boxes and confidence scores participating agents \[225\]. Nev-in brand, resolution, and configuration, leading to domain ertheless, due to model heterogeneity, the confidence scores discrepancies that impact system performance. In response to provided by different agents may not always align accurately. 

this exigency, DI-V2X \[229\] introduced a teacher-student dis-In \[225\], a model-agnostic CP framework was proposed to tillation architecture with three key components: the Domain-tackle this confidence misalignment problem, using a Doubly Mixing Instance Augmentation module for aligning distri-Bounded Scaling calibrator to eliminate bias in confidence butions between teacher and student models, the Domain-scores and a Promote-suppress Aggregation algorithm to select Adaptive Fusion module for combining vehicle and infras-high-score bounding boxes based on calibrated confidence and tructure features, and the Progressive Domain-Invariant Dis-spatial consistency. In addition to variations in confidence tillation module to align student and teacher features before levels, connected agents’ detection outcomes may vary due and after fusion. This method improves V2X perception by to differences in motion prediction models, with some agents creating a generalized representation across various domains. 

lacking information like acceleration or yaw rate. To address Besides sensor characteristics, diverse environmental con-

18

ditions inevitably create a substantial domain gap and data it does not directly address feature loss. In contrast, V2X-heterogeneity among CAVs \[230\]. To address this, \[230\] pro-INCOP \[236\] recovered missing data by leveraging historical posed a domain generalization framework with an amplitude information, using an adaptive communication model that ex-augmentation module to reduce the model’s influence on low-tracts multi-scale spatial-temporal features to estimate missing spectral variations, a domain alignment mechanism to unify information, effectively countering communication interrup-image pixel distributions, and a meta-consistency training tions. In \[243\], a Historical Frame Prediction \(HFP\) module scheme to simulate domain shifts and optimize the model with was introduced to address information loss or delay issues by consistency loss, potentially eliminating the domain discrep-predicting the current frame with temporal associations, taking ancy among CAVs prior to inference. 

the stacked results of the previous few historical frames as The distinctness in data characteristics across different agent input. 

types presents significant challenges in CP. VINet \[231\] ad-Previous approaches often overlook realistic channel models dressed this challenge using a Two-stream Fusion algorithm and may not capture the complexity of real-world communica-to integrate heterogeneous features from infrastructures and tion channels. To address this, \[237\] incorporated Rician fad-CAVs via a feature mapping and max-out procedure on an ing with free-space path loss and the WINNER II model \[270\]

edge server. In V2X-M2C \[232\], a heterogeneity-reflected with multi-path fading to simulate practical channels. A self-convolution module was introduced to manage multiple het-supervised adaptive weighting model, based on a CNN with a erogeneous agents using two parallel convolution pipelines, Softmax layer, was introduced to mitigate channel distortion considering their different feature distributions while main-effects on intermediate fusion. The model was trained using taining a lightweight and efficient architecture. However, time contrastive self-supervision without manual annotations, and asynchrony and calibration errors between vehicle and infras-its generalization was validated across various data domains, tructure cameras can lead to inaccurate relative position detec-detection backbones, noise levels, and path loss factors. 

tion, causing misalignment between ground truth and projected Accessing historical information can reduce transmission 2D bounding boxes. VIMI \[233\] tackled the calibration noise frequency and provide a compensatory mechanism for po-issue through its Multi-scale Cross Attention and Camera-tential communication failures, thereby improving system re-aware Channel Masking modules, using multi-scale feature liability and performance. Building on this concept, Tem-fusion and camera parameter priors to correct for misalignment pCoBEV \[238\] introduced an importance-guided attention caused by time asynchrony. 

architecture to prioritize critical regions from the historical 3\) Model and Data Heterogeneity: While some existing context, compensating for communication failures. This tem-studies address the heterogeneity of data and models, effec-poral module can be integrated into state-of-the-art camera-tively modelling dynamically increasing heterogeneous scenar-based CP models without requiring complete model re-ios continues to pose significant challenges. In reality, new het-training, significantly reducing training time. Experiments on erogeneous agent types with different modalities and models the OPV2V dataset demonstrate that TempCoBEV outper-may continuously emerge, causing domain gaps and limiting forms non-temporal models in predicting current and future scalability. HEAL \[234\] solved this problem by establishing a BEV map segmentations, particularly in scenarios involving unified feature space for the initial homogeneous agents and communication failures. 

then aligning new heterogeneous agents to this space through a novel reverse alignment mechanism. This approach enables C. Communication Delays

the integration of new agent types with minimal training costs while preserving model and data privacy. Despite its scalability Latency resulting from network congestion reduces percep-and efficiency, HEAL’s reliance on BEV features requires tion accuracy and disrupts fusion alignment \[271\]. A basic compatibility with keypoint-based LiDAR models, and its solution to address latency issues is to adjust the timestamp performance depends on accurate agent localization, which can by compensating for the time difference with a reference be affected by localization noise in real-world scenarios. 

agent. Building on this concept, CooperFuse \[239\] introduced a multi-agent temporal synchronization module, incorporating time calibration communication, time compensation, and caliB. Lossy Communication

bration completion to minimize network transmission latency. 

In practical V2X communication, factors such as interfer-The time series prediction strategy is also effective in ad-ence, tampering, Doppler shifts \[267\], routing failures \[268\], 

dressing the latency issue by predicting the sender’s perception multipath effects, and signal fluctuations \[269\] frequently at the current time step based on historical frames. In this cause incomplete or inaccurate information exchange, thereby context, the FFNet \[240\] leveraged temporal coherence by ex-diminishing the performance of CP. 

tracting the first-order derivative of feature flow from previous Drawing inspiration from image-denoising networks, the infrastructure frames to predict future features and mitigate Lossy Communication Aware Repair Network \(LCRN\) \[235\]

asynchrony. While effective for very short time intervals, this utilized an encoder-decoder architecture with skip connections first-order expansion method has limitations. SyncNet \[241\]

to generate tensor-wise filters for repairing damaged features adopted a dual-branch pyramid Long Short-term Memory from lossy communication. These filters are applied to lossy \(LSTM\) network to infer real-time features and cooperative features, which are then fused via a V2V attention module. 

attention. The HFP module \[243\] can generate the prediction While LCRN mitigates the impact of feature degradation, of the current frame through a series of multidimensional

19

convolution mixing operations. However, these approaches crucial. Probabilistic modelling techniques have been utilized have not effectively addressed issues caused by irregular to estimate the trustworthiness of connected agents based on time delays. As a substitute, CoBEVFlow \[242\] treated each data consistency \[246\]. This approach applies a Bayes filter to collaboration message as an irregular sample, using historical quantify consistency, allowing the detection of forged infor-frames to estimate the BEV flow map for asynchronous feature mation by analyzing the correlation between data consistency alignment, though it still depends on past data for latency com-and agent reliability. However, this method is constrained in pensation. In contrast, V2X-PC \[136\] bypassed this reliance detecting attackers, as it requires substantial redundancy—

by directly utilizing low-level coordinate information in point specifically, at least triple redundancy in conflicting data—to clusters to predict their locations at the current timestamp. 

effectively identify malicious agents. 

Re-encoding received features with delay time is another FDII \[247\] addressed spoofing attacks by leveraging LiDAR

approach for mitigating communication delays. For instance, data from neighbouring vehicles to detect tampered points in V2X-ViT \[145\] addressed time delay through a Delay-aware the victim’s scan. By comparing the altered and unaltered Positional Encoding module that utilizes sinusoid functions scans, FDII identifies discrepancies and classifies attacks using conditioned on delay time and channel information to initialize a decision tree algorithm, which also updates the unsafe areas a learnable embedding. Similarly, V2VNet \[140\] utilized a for each vehicle. The approach proved effective in identifying CNN to manage latency by incorporating the received inter-attack types and reconstructing vulnerable regions. However, mediate feature, relative 6DoF pose, and delay time, producing decision trees may struggle with complex data relationships a time-delay-compensated representation. These methods as-and often a bias toward the majority class in imbalanced sume latency is known; however, latency is typically calculated datasets, potentially leading to the suboptimal classification using timestamps from different agents’ clocks, which may of minority classes. 

result in deviations and inaccurate latency measurements. 

To counter data fabrication attacks, the Collaborative To address this, FreeAlign \[195\] introduced a multi-anchor Anomaly Detection \(CAD\) model \[248\] allows benign vehi-based subgraph searching algorithm to identify the common cles to collectively detect malicious fabrications by sharing subgraph between salient-object graphs across different agents, and merging occupancy maps. These maps, represented by estimating clock deviations and determining the precise time fine-grained polygons, offer greater precision and flexibility difference between collaborative messages. This approach en-compared to grid-based alternatives. CAD incorporates motion sures accurate temporal alignment without relying on external estimation to track objects across frames, attaching motion clock signals. 

data to the maps. Consistency checks are performed to identify discrepancies among synchronized maps and compare perception results with the merged map, raising alerts for conflicted regions that suggest potential anomalies. Although D. Security and Privacy

CAD proves effective in real-world scenarios, its efficacy de-Data security and privacy are essential to the reliability pends on the presence of at least one benign CAV monitoring of CP systems. V2X communication networks connecting the attacked region. 

various agents are vulnerable to potential attacks during data Malicious Agent Detection \(MADE\) \[249\] used two key transmission, which could compromise system integrity. Fur-statistics, match loss and collaborative reconstruction loss, to thermore, data sharing between agents introduces risks of identify malicious agents. Match loss quantifies discrepancies privacy breaches, underscoring the need for robust security in bounding box proposals between the ego agent and the protocols within CP networks. 

inspected agent, while collaborative reconstruction loss mea-1\) Data Security: While cooperative multi-agent systems sures the consistency of feature maps when the two agents offer significant promise, they also present security risks due collaborate. These metrics can be applied independently or to the potential for malicious or unreliable communication together to form a multi-test with a controlled false detection between agents \[272\]. Malicious agents may tamper with rate, utilizing the Benjamini-Hochberg procedure \[275\]. Al-shared packets or generate forged data. The ego vehicle is though this approach offers valuable insights, MADEs reliance unable to independently verify missed events or confirm the on conformal p-values computed from calibration sets assumes authenticity of received data \[273\]. Imperceptible perturbations the ego agent is benign, a condition that may not always be introduced by adversaries can substantially alter perception valid in real-world scenarios. 

outputs, compromising system integrity. Although adversarial 2\) Data Privacy:

While collaboration among multiple

training has been used to address these threats \[244\], it adds agents shows great potential, it requires local data exchange training overhead and often fails to generalize to novel attacks between cooperating partners. In practice, connected agents

\[274\]. As a solution, ROBOSAC \[245\] was proposed, allowing often demonstrate heterogeneity and privacy concerns emerge ego vehicles to intelligently select trustworthy collaborators. 

as automotive manufacturers and software providers are gener-By detecting divergences in adversarial messages and aligning ally unwilling to share proprietary data. This reluctance leads with reliable collaborators, ROBOSAC generalizes to unseen to incomplete and insufficient information for perception tasks, adversarial strategies and offers a flexible trade-off between making it crucial to address privacy issues in V2X CP systems. 

performance and computational cost. 

Federated Learning \(FL\)-assisted CAVs represent an emerg-To ensure data security, assessing the quality of received ing paradigm aimed at mitigating privacy concerns while re-information and detecting erroneous data before processing is ducing communication costs and diversifying the seen scenar-

20

ios in comparison to conventional centralized learning \[276\], 

prior knowledge from diverse motion models and applied

\[277\]. FL enables collaborating clients to effectively train a hybrid consensus strategy with a Cubature Kalman Filter models without the need for data aggregation or direct data \(CKF\) \[281\] for more accurate data fusion and model uncer-exchange \[278\]. However, determining the network resources tainty handling. Although effective, CKF initialization remains and sensor placements for multi-stage training with multi-challenging, especially with uncertain initial state estimates. 

modal datasets in varied scenarios can be a complex challenge. 

CMP \[256\] used the AB3DMOT tracker \[282\] to associate Conventional FL approaches face challenges in managing the detected 3D bounding boxes into trajectory segments. By data heterogeneity arising from diverse sensor configurations. 

incorporating cooperative perception and motion prediction Variations in camera positions across clients can result in FL

aggregation, CMP is able to address the issue of propagated results that deviate from the optimal values of local data. To uncertainties and inaccuracies from the upstream detection and tackle this issue, the FedBEVT \[251\] framework introduced a tracking tasks, leading to improved overall motion prediction federated transformer learning approach focused on camera-performance. 

attentive personalization, which alleviates the negative impacts Uncertainty quantification is essential for ensuring safety of data heterogeneity by privatizing the camera positional em-in CAV systems by estimating the likelihood of outcomes bedding. The work in \[253\] addressed the data heterogeneity when certain system aspects are uncertain. The Double-M

in CP by implementing a novel federated dynamic weighted

\[257\] addressed uncertainty in cooperative object detection by aggregation \(FedDWA\) algorithm along with a dynamic ad-utilizing temporal features. It applies a customized Moving-justing loss function. However, these methods ignore network Block Bootstrap algorithm to model the multivariate Gaus-heterogeneity. Varying connection qualities among clients can sian distribution for each bounding box corner, accounting result in communication delays, thereby impeding the FL

for auto-correlations in time-series data. By assigning higher process. To fill this gap, a contextual client selection pipeline uncertainties to low-accuracy objects, Double-M improves was introduced in \[252\], modelling networks and estimating accuracy, though it assumes each bounding box corner follows FL communication latency under predictive transport scenarios an independent multivariate Gaussian distribution. GevBEV

via digital twin simulations. This FL methodology effectively

\[133\] introduced a more comprehensive model by constructing tackles data and network heterogeneity, thereby improving a probabilistic BEV map using point-based spatial Gaussian communication efficiency through contextual client selection. 

distributions. It leverages Evidential Deep Learning \[159\] to Challenges in FL for CAVs also include unfairness due estimate probabilities and uncertainties, interpreting Gaussian to differences in data volumes and communication delays. 

densities as support for a Dirichlet distribution. This allows To address the issues of imbalanced data distribution and GevBEV to quantify and explain prediction uncertainty, with variable channel conditions, the study in \[250\] employed a experimental results showing it outperforms previous models local training strategy customized for each CAV based on on the OPV2V benchmark. 

its data volume and channel conditions, thereby minimizing In the context of object tracking, the MOT-CUP frame-the number of global rounds needed and reducing the time work \[258\] addressed uncertainty quantification by integrating intervals between rounds. Consequently, it promotes fairness in detection uncertainty into the Kalman Filter \(KF\) and the energy and time expenditure, accelerating model convergence object association process. It models uncertainty using direct while ensuring equitable costs for all CAVs. 

modelling \[283\] and conformal prediction \[284\], which is then applied to the Standard Deviation-based KF \(SDKF\) and E. Perception Uncertainty

a Negative Log-Likelihood \(NLL\) association improvement Multi-agent cooperation markedly enhances the perception procedure. SDKF leverages uncertainty to enhance location efficiency of autonomous vehicles. However, inherent uncer-prediction accuracy, while NLL improves tracking by account-tainties persist in CAVs due to out-of-range objects, sensor ering for low-quality detections. Similarly, DMSTrack \[259\]

rors, and adverse weather conditions \[279\]. These uncertainties used a differentiable multi-sensor KF to estimate uncertainty can result in false detections, adversely affecting subsequent for each detection, optimizing tracking through a learned self-driving modules like planning and control. Addressing covariance model. Nevertheless, neither approach uses multi-these uncertainties within CP is essential for ensuring safe vehicle tracking information for improved data association, autonomous driving. 

and temporary tracking failures remain a challenge. To this Capturing perception system uncertainties is crucial for end, the work in \[260\] proposed a complementary data asso-enhancing CAV safety. The Perception Error Model \(PEM\) ciation module to identify and compensate for missed objects

\[280\] incorporated single-agent perception errors into the using information shared among the CAVs. Experiments show ground truth to directly model uncertainties in the simula-that incorporating uncertainty improves multi-object tracking tion pipeline, eliminating the need for synthetic sensor data. 

performance. 

Expanding on this, the Cooperative Perception Error Model \(CoPEM\) \[254\] addresses occlusion by modelling V2X-related F. Task Discrepancy

perception errors and uncertainties, facilitating performance tuning as sensor numbers increase. However, CoPEM requires Most existing CP approaches are task-specific, necessitating a statistical model for each agent and overlooks the high ma-retraining the entire model for different perception tasks. 

neuverability of vehicle targets. To resolve this, the Consensus-These task-specific methods have limitations and potentially based Distributed Multi-Model CP \(DMMCP\) \[255\] integrated hinder the models’ generalization ability across a broader

21

spectrum of perception tasks. The development of a CP

ture distribution in actual driving situations is notably more in-framework independent of downstream tasks holds promise tricate than that in simulated data. To mitigate these two promi-for advancing cooperative driving automation. In this context, nent disparities, the work in \[263\] introduced the Simulation-recent endeavours have focused on a novel task known as to-Reality \(S2R\) transfer learning framework, specifically multi-agent scene completion, also referred to as cooperative S2R-ViT, which leverages labelled simulated data and unla-reconstruction. In this task, each agent learns to efficiently beled real-world data to minimize domain discrepancies in share information to reconstruct a complete scene observed cooperative 3D object detection. The S2R-ViT framework by all agents. By training models to reconstruct holistic comprises two key components: the S2R Uncertainty-aware observations, this approach encourages the acquisition of more Vision Transformer \(S2R-UViT\) and the S2R Agent-based effective task-agnostic feature representations. 

Feature Adaptation \(S2R-AFA\). In S2R-UViT, two multi-head The spatiotemporal auto-encoder \(STAR\) \[261\] aims to self-attention branches \(LG-MSA\) are utilized to incorporate disregard downstream tasks and concentrate on learning to both local and global attention mechanisms, enhancing feature reconstruct an entire scene through shared features in a self-interactions across spatial positions of all agents. Following supervised manner. STAR facilitates the transmission of sub-LG-MSA, an uncertainty-aware module is introduced to assign sampled features to collectively cover the entire spatial region, weights to the ego-agent’s features while considering uncertain striking a balance between scene reconstruction performance factors stemming from the shared features of other agents. The and communication costs. The reconstructed scene can then be S2R-AFA incorporates inter-agent and ego-agent discrimina-used for various downstream tasks without additional training. 

tors, enabling S2R-ViT to generate robust, domain-invariant This task-agnostic methodology represents a novel direction feature representations. Experimental results underscore the in CP, enabling the separation of cooperation training from importance of domain adaptation for LiDAR-based 3D object downstream task learning. However, due to its imperfect detection when transitioning from simulation to real-world scene completion, STAR still exhibits a performance gap in environments. 

downstream perception compared to task-specific methods. 

In addition to the domain gap between simulated and In contrast to STAR’s self-supervised learning approach, the real-world data, there is also a domain gap among real-CORE method, as described in \[262\], learns to reconstruct world collaborative agents, which further complicates the comprehensive scenes under the guidance of BEV represen-challenge of sim2real generalization. To tackle these issues, tations derived from the aggregation of raw sensor data from an unsupervised sim2real domain adaptation method named all agents. When provided with a group of agents and their Decoupled Unsupervised Sim2Real Adaptation \(DUSA\) was 2D BEV maps, CORE conducts cooperative reconstruction proposed in \[264\]. The DUSA solves the problems of sim2real through three main components: a compression module, a col-adaptation and inter-agent adaptation by introducing the laboration module, and a reconstruction module. The compres-Location-adaptive Sim2Real Adapter \(LSA\) module and the sion module calculates a compressed feature representation Confidence-aware Inter-agent Adapter \(CIA\) module, respec-for each BEV, considering channel-wise compression and sub-tively. The LSA module uses location importance to prompt sampling features along the spatial dimension. Drawing inspi-the feature extractor to produce sim/real invariant features, ration from prior work \[139\], CORE incorporates a lightweight while the CIA module uses confidence cues to help the feature attention-aware collaboration module to facilitate information extractor output agent-invariant features. This method effec-aggregation. The reconstruction module employs a decoder tively bridges the gap between simulated and real-world data structure to regenerate a complete scene observation from for V2X collaborative perception, demonstrating its superiority the fused features. This “learning-to-reconstruct” approach is over existing methods through experiments. 

task-agnostic and provides clear and meaningful supervision to encourage more effective cooperation, ultimately benefiting VI. ISSUES FOR DATASET

perception tasks. 

While CP has gained momentum in recent years, it remains a nascent field. One of the key obstacles impeding the G. Simulation to Reality

progress of CP algorithms is the substantial cost and potential Due to the scarcity of real multi-agent data and the resource-safety risks associated with conducting field experiments. Such intensive nature of manual labelling, most existing CP models experiments necessitate deploying numerous expensive CAVs often rely on simulated sensor data for training and testing. 

and sizeable test areas. Additionally, acquiring precise anno-However, when these simulation-trained models are deployed tations requires significant labour and time, especially when in real-world settings, they frequently experience a decline dealing with CP involving multiple agents \[285\]. To address in perception performance due to the substantial domain gap these challenges efficiently, an effective research strategy is between simulation and reality. Domain adaptation techniques to develop and validate CP algorithms within a simulated are employed to address these challenges by adapting models environment, which offers a cost-effective and safe alternative trained on labelled source domains to perform effectively in to real-world experimentation. However, validating V2X per-unlabeled target domains. 

ception in authentic scenarios remains challenging due to the In contrast to the idealized simulation environment, real-absence of well-established public benchmarks. This section world multi-agent scenarios introduce localization errors and delineates prominent simulation platforms and open-source communication latency among agents. Furthermore, the fea-datasets frequently employed in developing V2X CP systems. 

22

A. Simulation Tools

graph based on an existing scene. It identifies and selects Numerous simulation platforms have been developed to collaborators whose combined perspectives will likely lead to offer multi-modal sensory inputs and 3D annotations, thereby sub-optimal outcomes in perception tasks. The APS, on the advancing the development of multi-agent CP before the other hand, focuses on perturbing the positions of vehicles widespread availability of real-world datasets. For example, within the scene. It achieves this using black-box optimization SUMO \[286\] is a traditional traffic and driver behaviour algorithms tailored to perception tasks’ adversarial objectives. 

simulator renowned for its capacity to handle large-scale and Combining these two stages in V2XP-ASG offers an efficient realistic traffic flows. It incorporates dynamic modelling for approach to enhance the complexity and difficulty of the each vehicle, enabling users to swiftly create customized traffic scenarios presented in the simulation, thereby challenging the scenarios through the Traffic Control Interface \(TraCI\) API. 

V2X perception models under evaluation. 

SUMO is highly convenient for integrating naturalistic tra-4\) AUTOCASTSIM: In \[146\], researchers introduced AU-jectory data, which can be directly applied to the surrounding TOCASTSIM, an autonomous driving simulation framework environment for testing CDA. However, it has limitations when built on the CARLA platform. AUTOCASTSIM was de-providing high-resolution sensor data with exceptional fidelity. 

signed to evaluate cooperative driving models, particularly in In recent years, there has been a proliferation of autonomous accident-prone scenarios. This platform offers three bench-driving simulators designed to facilitate high-fidelity mod-mark traffic scenarios \(Overtaking, Left Turn, and Red Light elling of the traffic environment and sensor capabilities. The Violation\) that impose decision-making challenges due to following content will provide an overview of the fundamental restricted line-of-sight sensing. AUTOCASTSIM includes an characteristics of several prominent simulation tools used to integrated networking simulation feature, facilitating cus-develop and analyze CDA systems. 

tomization of V2V communication dynamics. Additionally, 1\) CARLA: CARLA \[287\] is a pioneering autonomous it incorporates an advanced driving model that incorporates driving simulator celebrated for its versatility in specifying privileged environmental information, enabling the creation of sensor suites and environmental conditions. This open-source customized and realistic traffic scenarios. 

platform was purpose-built to facilitate the development, train-5\) CMM Co-simulation Platform: The work in \[291\] high-ing, and validation of novel autonomous driving systems. 

lighted a common limitation in most current traffic simulators, CARLA’s architecture is notably scalable, employing a server-which typically use intrinsic attributes of target objects without multi-client model to distribute computations across multiple considering imperfect perception in CDA models. A CARLA-nodes. The server continuously updates the environmental based co-simulation platform called the Cyber Mobility Mirror physics while users exert control over the client side through \(CMM\) was developed to address this limitation. The CMM

the CARLA API. Although CARLA permits environment ex-platform enhances CDA by generating realistic perception tension, the process of swiftly creating scenarios and managing data. A deep learning-based perception pipeline was integrated substantial traffic volumes has grown intricate. CARLA does into the simulation system to establish a CMM framework offer a traffic manager module for generating background capable of faithfully perceiving and reconstructing simulated traffic. However, these modules rely on simplified behavioural traffic objects in 3D. This improvement enables CDA mod-rules that may not faithfully replicate actual driver behaviour. 

els to utilize perceived information from the CMM system, 2\) OpenCDA: OpenCDA \[288\], \[289\] stands as an open enhancing model fidelity and supporting more robust system and dedicated co-simulation framework designed for CDA. 

validation, ultimately boosting overall confidence. 

It encompasses both traffic and vehicles, offering a com-6\) OpenCDA-ROS: Existing CDA simulation platforms

plete CDA vehicle software pipeline. OpenCDA seamlessly often exhibit disparities between simulation and real-world integrates CARLA and SUMO for lifelike scene rendering, scenarios. To address this issue comprehensively, a unified vehicle modelling, and traffic simulation. This framework tool and framework are needed to support CDA development facilitates the evaluation of CDA within a CARLA \+ SUMO

in simulation and real-world environments. OpenCDA-ROS

co-simulation environment and supports diverse levels and

\[307\] has been developed as an extension of OpenCDA, tai-categories of cooperation among CAVs during simulation. 

lored for the Robot Operating System \(ROS\). This adaptation OpenCDA also provides a comprehensive library of CDA serves as a bridge between simulated and real-world CDA, research pipelines, source code, and standard autonomous ensuring that algorithms and vehicles perform similarly in both driving components encompassing perception, localization, settings. By reorganizing cooperative functions into a more planning, control, and V2X communication modules. One shareable structure, OpenCDA-ROS benefits simulation and of its key advantages is its flexibility, allowing users to real-world prototyping and deployment, facilitating the seam-easily substitute default modules with custom-designed ones less integration of these two domains in CDA development. 

to assess the impact of new functionalities on overall CDA performance. 

3\) V2XP-ASG: V2XP-ASG \[290\] is designed to assess B. Open Source Dataset

LiDAR-based V2X perception models by providing the ca-The development of CP models relies on perception datasets pability to generate complex and realistic scenarios. This gathered from various onboard sensors like radar, camera, simulation framework comprises two key components: Adver-and LiDAR. Utilizing these sensors for real-world perception sarial Collaborator Search \(ACS\) and Adversarial Perturbation tasks can be costly and time-consuming. A more economically Search \(APS\). The ACS creates an adversarial collaboration viable alternative is to obtain cooperative data from simulation

23

TABLE VII

COMPARISON BETWEEN COOPERATIVE PERCEPTION-RELATED DATASETS. 

Agent

Annotation

Object

RGB

LiDAR

3D

Category

Dataset

Year

Scenario

Maps OD OT SS MP AP

Number

Range

Category Image

Frame

Box

√

DAIR-V2X-C \[292\]

2022

V2I

2

280m

10

39k

39k

464k

×

×

×

×

×

√

√

√

√

V2X-Seq \[293\]

2023

V2I

2

280m

10

15k

15k

−

×

×

√

√

√

HoloVIC \[294\]

2024

V2I

2

70m

3

100k

100k

## 11.5M

×

×

×

√

√

√

V2V4Real \[295\]

2023

V2V

2

200m

5

40k

20k

240k

×

×

×

√

√

√

Real-world

LUCOOP \[296\]

2023

V2V

3

200m

5

0

54k

−

×

×

×

√

√

√

√

√

TUMTrafV2X \[297\] 2024

V2I

2

200m

8

5k

2k

30k

×

√

√

RCooper \[298\]

2024

I2I

2

230m

10

50k

30k

−

×

×

×

×

√

√

InScope \[299\]

2024

I2I

2

230m

4

0

21k

188k

×

×

×

×

√

√

V2X-Real \[300\]

2024

V2X

4

200m

10

171k

33k

## 1.2M

×

×

×

×

√

√

CODD \[301\]

2022

V2V

4–16

100m

2

0

## 13.5k

### 204k

×

×

×

×

√

√

√

OPV2V \[302\]

2022

V2V

2–7

120m

1

44k

11k

233k

×

×

×

√

√

√

√

V2X-Sim \[303\]

2022

V2X

2–5

70m

1

60k

10k

26k

×

×

√

√

Similation

V2XSet \[145\]

2022

V2X

2–7

120m

1

44k

11k

233k

×

×

×

×

√

DOLPHINS \[304\]

2022

V2X

3

200m

2

42k

42k

292k

×

×

×

×

×

√

√

√

√

√

DeepAccident \[305\]

2023

V2X

5

70m

6

57k

57k

285k

×

√

√

SCOPE \[306\]

2024

V2X

3–24

250m

5

17.6k

## 17.6k

### 575k

×

×

×

×

Note: OD: Object Detection, OT: Object Tracking, SS: Semantic Segmentation, AP: Accident Prediction. 

platforms featuring high-fidelity sensor modelling and percep-more, it delineates five distinct tasks to foster advancements tion capabilities. This subsection will outline several datasets in related research areas. 

relevant to CDA research, summarized in Table VII. 

The V2V4Real dataset \[295\], collected from two CAVs with 1\) Real-world Dataset: A direct approach to evaluating multi-modal sensors in Columbus, Ohio, USA, covers diverse V2X CP involves collecting diverse real-world test scenarios. 

driving scenarios such as intersections, highways, and city DAIR-V2X-C \[292\] is an autonomous driving dataset from streets. It includes 40k RGB frames, 20k LiDAR frames, 240k real scenarios designed for research on V2I cooperation-annotated 3D bounding boxes, and HDMaps for road topology related challenges. It comprises 38,845 LiDAR and 38,845

prediction, supporting cooperative 3D object detection and camera frames captured at intersections equipped with infras-Sim2Real adaptation. However, its two-vehicle setup limits tructure sensors. Expert annotators have meticulously labelled its comprehensiveness for broader cooperative applications. 

all frames with 3D annotations. While DAIR-V2X supports Addressing this, LUCOOP \[296\] provides data from three the perception task, it does not cover the essential motion CAVs over a 4 km trajectory, including 54k LiDAR frames, prediction aspect. V2X-Seq \[293\] offers a sequential V2I 700k IMU measurements, 2.5 hours of GNSS data, UWB-dataset, serving to develop and validate CP and motion fore-based V2V and V2X measurements, and accurate ground truth casting algorithms. This dataset comprises two distinct sub-poses. Although it offers a valuable resource for evaluating datasets: the sequential perception and trajectory forecasting CP methods, it lacks complex traffic scenarios. In contrast, datasets. The former includes over 15k frames from 95 sce-the TUMTraf-V2X \[297\] offers a more extensive collection, narios, encompassing various data types such as infrastructure focusing on challenging traffic situations, varying weather images, point clouds, vehicle-side images, point clouds, 3D

conditions, and rare events, making it a more comprehensive detection/tracking annotations, and vector maps. The latter tool for testing CP methods. It features 2k annotated point contains 80k infrastructure-view scenarios, 80k vehicle-view clouds, 5k images, and 30k 3D bounding boxes with track scenarios, and 50k cooperative-view scenarios captured from IDs. 

28 intersections, with a substantial data coverage of 672 hours. 

The datasets mentioned above primarily support either V2I DAIR-V2X-C and V2X-Seq employ a single viewpoint

or V2V cooperation, but not both modes together. In contrast, utilizing a camera and Lidar pair to gather data from various the V2X-Real dataset \[300\] is the first real-world dataset intersections. Nevertheless, the intricacy of traffic scenarios designed specifically for V2X CP research. It includes 33K

often results in frequent occlusion of targets captured by the LiDAR frames, 171K camera images, and over 1.2 million camera, thus significantly restricting the efficacy of single-annotated 3D bounding boxes across ten object categories, col-viewpoint roadside sensors. In contrast, HoloVIC \[294\] was lected from two CAVs and two smart infrastructures equipped developed through the establishment of multiple holographic with multi-modal sensors. The dataset is organized into four intersections equipped with diverse sensor configurations, in-sub-datasets based on the ego agent type and collaboration cluding cameras, lidars, and fisheye cameras. It comprises over mode: Vehicle-Centric, Infrastructure-Centric, V2V, and I2I 100k synchronized frames and provides annotations for 3D

CP. V2X-Real is collected in congested urban environments bounding boxes, object IDs, and global trajectories. Further-with dense traffic and pedestrian flow, providing rich and

24

challenging scenarios for V2X CP research. 

prehensive safety assessment of autonomous driving. To ad-All real-world datasets discussed so far have primarily dress this gap, the DeepAccident dataset \[305\] was created focused on vehicle-centric cooperative tasks, such as V2V

using the CARLA simulator, featuring 57k frames and 285k and V2I cooperation. However, roadside CP, particularly annotated samples for evaluating motion and accident pre-infrastructure-to-infrastructure \(I2I\) collaboration for compre-diction capabilities. Data is captured by four vehicles and hensive roadside coverage, remains unexplored. To address one infrastructure unit using multi-view RGB cameras and this, \[298\] introduced RCooper, the first real-world dataset for LiDAR, with corresponding annotations for perception and roadside CP, featuring over 50k images and 30k point clouds motion prediction tasks. This dataset provides safety-critical with 3D annotations across various weather, lighting, and scenarios and introduces an end-to-end accident prediction traffic conditions. InScope \[299\] is another large-scale roadside task for forecasting collision details. V2XFormer, proposed as CP dataset designed to tackle occlusion challenges in open a benchmark, demonstrates superior performance in motion traffic scenarios. It features multi-position LiDAR sensors and accident prediction compared to single-vehicle models. 

deployed on infrastructure to broaden perception and comple-However, DeepAccident lacks scenario diversity, realistic sen-ment vehicle-side systems, with 303 tracking trajectories and sor models, environmental conditions, and vulnerable road 187,787 3D bounding boxes captured over 20 days. InScope users. The SCOPE dataset \[306\] addresses these limitations offers benchmarks for tasks like 3D object detection and as the first synthetic multi-modal dataset for CP, incorporating multi-object tracking, providing comprehensive anti-occlusion realistic sensor models, physically accurate weather simula-algorithm evaluation. A new metric is also introduced to assess tions, over 40 diverse scenarios with up to 24 collaborative occlusion’s impact on detection performance. 

agents, and passive traffic. It also provides benchmarks for 2\) Simulation Dataset: While realistic datasets allow CP

2D/3D object detection and semantic segmentation. 

models to generalize effectively to real-world driving situations, they are expensive, time-consuming, and limited in VII. PERFORMANCE VALIDATION AND FIELD

scenarios. A cost-effective alternative is to gather large-scale EXPERIMENT

datasets in a high-fidelity simulator. The Cooperative Driving Evaluating CP systems requires a blend of simulations, Dataset \(CODD\) \[301\], generated using the CARLA simulator, offline testing, and real-world experiments. Simulations and comprises 108 snippets, each with 125 temporal frames of offline validation allow for controlled performance assess-LiDAR point cloud data. Each frame contains LiDAR data ments of V2X-based CP approaches, optimizing metrics to from all vehicles in the scenario, sensor poses, and ground-achieve optimal performance. In contrast, field experiments truth annotations for 3D bounding boxes of cars and pedestri-test CP adaptability in real-world conditions, revealing how ans. CODD focuses on a single driving scenario. In contrast, systems handle diverse traffic and communication challenges. 

the OPV2V dataset \[302\] includes both camera images and This section first compares the performance of various CP

LiDAR point clouds from connected vehicles across over 70

methods in offline testing and then explores real-world initia-diverse scenes, spanning eight CARLA towns and Culver City, tives, including experimental deployments, pilot projects, and Los Angeles, using OpenCDA and CARLA. Both CODD and field tests, to assess CP readiness for practical deployment. 

OPV2V provide ground truth for V2V cooperative 3D object detection, but neither includes roadside infrastructure, limiting their ability to evaluate V2I perception \[308\]. 

A. Performance Validation

The V2X-Sim dataset \[303\] is a synthetic V2X-assisted CP

In this subsection, performance validation is presented dataset for autonomous driving, aimed at advancing research in through a synthesis of experimental results from existing multi-agent, multi-modality, and multi-task perception. It was studies on CP methods for autonomous driving, using both generated using SUMO for realistic traffic flows and CARLA real-world and simulated datasets, with 3D object detection for capturing sensor streams from multiple vehicles at inused as an example downstream task. Average Precision \(AP\), tersections. V2X-Sim provides synchronized recordings from defined as the area under the precision-recall curve, serves roadside infrastructure and vehicles, along with comprehensive as the primary metric for 3D object detection, with APs ground truth annotations for tasks such as detection, tracking, at Intersection-over-Union \(IoU\) thresholds of 0.5 and 0.7

and segmentation. However, it lacks noise simulation and only utilized to assess various models. Performance comparisons includes a single type of road network. In contrast, the V2XSet are presented across several datasets, including the real-world dataset \[145\] incorporates real-world noise during V2X collab-datasets DAIR-V2X \[292\] and V2V4Real \[295\], as well as oration using CARLA and OpenCDA, featuring over 11,447

simulation-based datasets OPV2V \[302\], V2X-Sim \[303\], and frames divided into training, validation, and testing subsets. 

V2XSet \[145\]. 

The DOLPHINS dataset \[304\], generated with the CARLA 1\) Detection Performance Comparison: To ensure fairness simulator, encompasses six autonomous driving scenarios with and generalizability, all reported results reflect the best out-V2X communication and temporally synchronized sensor data comes from experimental evaluations of existing methods, from an ego vehicle, a cooperating vehicle, and a roadside with only those methods assessed on at least two datasets unit. It contains 42,376 frames of sensor data and 292,549 3D

included. Table VIII displays the AP values at IoU thresholds bounding box annotations for cars and pedestrians. 

of 0.5 and 0.7 across five datasets under default settings, While the previously mentioned datasets cover large-scale highlighting the highest AP values and indicating the source scenarios, they lack accident scenarios crucial for a com-for each result. The observed performance differences across

25

Fig. 6. The impact of time delay on the AP@0.7 performance metric for the Fig. 7. 

Detection performance on DAIR-V2X dataset with pose errors at OPV2V dataset. The results are referenced from \[150\] and \[217\]. 

four different noise levels. The pose noises follow Gaussian distribution N \(0, σt\) on x, y and N \(0, σr\) on θ, where x, y, θ are 2D centers and yaw angle of accurate global poses. We present AP@0.7 at noise level σt/σr = 0.0m/0.0◦, 0.2m/0.2◦, 0.4m/0.4◦, 0.6m/0.6◦. The results are methods and datasets indicate that certain algorithms are more referenced from \[190\] and \[191\]. 

effective under specific environmental or data conditions. 

Table VIII results indicate that DI-V2X achieves the highest AP@0.5 on DAIR-V2X at 0.7882, while DiscoNet leads errors remain unavoidable, requiring collaborative approaches on V2V4Real with an AP@0.5 of 0.7360. For AP@0.7 on to be resilient to these inaccuracies. Following \[190\], Gaussian V2V4Real, both FPV-RCNN and MACP achieve top perfor-noise N \(0, σt\) is added to x, y, and N \(0, σr\) to θ, to simulate mance at 0.4790, though MACP scores slightly lower than pose errors, where x, y, θ represent the 2D center and yaw FPV-RCNN with an AP@0.5 of 0.6760. Among simulation-angle of accurate global poses. Fig. 7 shows the detection based datasets, MKD-Cooper performs exceptionally on V2X-performance in terms of AP@0.7 for ten different methods on Sim, with an AP@0.5 of 0.9300 and AP@0.7 of 0.8520, and the DAIR-V2X dataset, evaluated at four levels of pose error achieves a high AP@0.7 of 0.9240 on OPV2V, positioning \(0.0m/0.0◦, 0.2m/0.2◦, 0.4m/0.4◦, 0.6m/0.6◦\), with results it as a leading method in simulated environments. V2X-PC

sourced from \[190\] and \[191\]. 

demonstrates robust performance across both real and simu-Among these methods, RoCo maintains the highest AP

lated datasets, achieving an AP@0.5 of 0.7689 and AP@0.7

scores across noise levels, demonstrating strong resilience of 0.6939 on DAIR-V2X and even higher scores on V2XSet to pose errors. In contrast, V2VNet shows the lowest AP

with an AP@0.5 of 0.9283 and AP@0.7 of 0.8955. These with substantial declines at higher noise levels, while its ro-findings suggest that V2X-PC excels across diverse datasets, bust variant, V2VNetrobust, outperforms the standard version, indicating strong adaptability to various conditions. 

indicating improved robustness to pose noise. CoAlign and CoBEVFlow perform well but yield slightly lower AP than 2\) Robustness to Time Delay: Time delay introduced by RoCo. F-Cooper, DiscoNet, OPV2V, and V2X-ViT display V2X communication presents a significant challenge in CP, stable performance across noise levels, suggesting greater leading to data asynchronization between ego and other agents resilience to pose errors. FPV-RCNN, despite moderate detec-during the data fusion process. To illustrate model robustness tion accuracy, shows notable AP declines as noise increases, to time latency, we present performance across delays ranging indicating higher sensitivity to positional errors. Overall, from 0 to 0.4 seconds, as shown in Fig. 6, with results increasing pose errors reduce AP@0.7 across all methods, referenced from \[150\] and \[217\]. 

underscoring their sensitivity to positional inaccuracies. 

As shown in Fig. 6, detection performance declines for all methods as time delay increases. V2VFormer\+\+ maintains relatively high AP scores, demonstrating the greatest resilience B. Field Experiments and Pilot Projects

to latency. CoBEVT and What2comm also show robust per-Field experiments of CP systems have progressed through a formance, though to a lesser extent. Where2com and V2X-range of global pilot projects, demonstrating CP’s adaptability ViT exhibit moderate robustness, with gradual AP declines and effectiveness under specific conditions. These initiatives indicating some sensitivity to delay. In contrast, DiscoNet showcase CPs potential to improve traffic efficiency, safety, and V2VNet experience sharper AP declines, reflecting higher and the functionality of CAVs within controlled environments, latency sensitivity. When2com begins with lower AP scores advancing research and development in intelligent transporta-and degrades significantly as delay increases, highlighting its tion systems. 

vulnerability to latency. In summary, V2VFormer\+\+ proves The Cooperative Adaptive Cruise Control \(CACC\) project the most delay-tolerant, while When2com is most affected by carried out in the U.S. leverages DSRC-based communication latency in the OPV2V setting, limiting its effectiveness under to enable real-time sharing of speed and positioning data substantial transmission delays. 

between vehicles, allowing for autonomous maintenance of 3\) Robustness to Pose Errors: Collaborative agents rely on safe inter-vehicle distances \[309\]. The project aims to enhance precise pose data from others to accurately transform the co-Adaptive Cruise Control \(ACC\) by dynamically coordinating ordinates of the data in the received messages. However, even vehicle spacing within a string, ultimately improving traffic with advanced localization technologies such as GPS, pose flow. Test cases for this project include simultaneous passing

26

TABLE VIII

3D OBJECT DETECTION PERFORMANCE COMPARISON ON DAIR-V2X, V2V4REAL, OPV2V, V2XSET, AND V2X-SIM DATASETS, WITH AP@0.5 AND

AP@0.7. 

Real-world Datasets

Simulation-based Datasets

Method

Year

DAIR-V2X

V2V4Real

OPV2V

V2XSet

V2X-Sim

AP@0.5/0.7

Source

AP@0.5/0.7

Source

AP@0.5/0.7

Source

AP@0.5/0.7

Source

AP@0.5/0.7

Source

F-Cooper \[203\]

2019 0.7370/0.5600 \[193\] 0.6930/0.4320 \[193\] 0.9070/0.8100 \[263\] 0.8400/0.6800 \[145\] 0.7150/0.5470 \[218\]

V2VNet \[140\]

2020 0.7097/0.4763 \[229\] 0.6470/0.3360 \[216\] 0.9350/0.7400 \[190\] 0.8710/0.6460 \[191\] 0.8850/0.6960 \[218\]

When2com \[116\]

2020 0.5188/0.3705 \[129\]

-

-

0.7785/0.6240 \[142\] 0.7016/0.5372 \[196\] 0.5206/0.4421 \[132\]

Who2com \[115\]

2020

-

-

-

-

0.5536/0.2339 \[132\]

-

-

0.4977/0.4230 \[132\]

V2VNetrobust \[189\] 2021 0.6610/0.4860 \[193\] 0.5500/0.3090 \[193\] 0.9420/0.8540 \[193\]

-

-

0.8400/0.7540 \[190\]

DiscoNet \[144\]

2021 0.7370/0.5840 \[193\]

0.7360/0.4660

\[193\] 0.9160/0.7910 \[190\] 0.9078/0.8381 \[136\] 0.8180/0.5370 \[218\]

OPV2V \[302\]

2022 0.7330/0.5530 \[190\] 0.6450/0.3430 \[216\] 0.9430/0.8270 \[190\] 0.9188/0.8475 \[136\] 0.8870/0.7340 \[218\]

Where2comm \[139\]

2022 0.7520/0.5880 \[193\] 0.7040/0.4690 \[193\] 0.9440/0.8550 \[193\] 0.9130/0.8530 \[232\] 0.6205/0.5459 \[132\]

V2X-Vit \[145\]

2022 0.7398/0.6150 \[136\] 0.6800/0.3910 \[193\] 0.9460/0.8560 \[190\] 0.9100/0.8030 \[191\] 0.9010/0.7950 \[218\]

CoBEVT \[214\]

2022 0.6390/0.5167 \[136\] 0.6650/0.3600 \[216\] 0.9140/0.8620 \[262\] 0.9033/0.8269 \[136\]

-

-

FPV-RCNN \[131\]

2022 0.6550/0.5050 \[190\]

0.7010/0.4790

\[193\] 0.8580/0.8400 \[190\] 0.8650/0.5630 \[191\] 0.8700/0.8380 \[190\]

UMC \[132\]

2023

-

-

-

-

0.6190/0.2450 \[132\]

-

-

0.6780/0.6001 \[132\]

What2comm \[150\]

2023 0.6081/0.4463 \[150\]

-

-

0.8683/0.7361 \[150\] 0.8459/0.6686 \[150\]

-

-

SCOPE \[196\]

2023 0.6518/0.4989 \[196\]

-

-

0.8971/0.8062 \[196\] 0.8752/0.7505 \[196\]

-

-

BM2CP \[129\]

2023 0.6403/0.4899 \[129\]

-

-

0.8372/0.6317 \[129\]

-

-

-

-

CoAlign \[190\]

2023 0.7460/0.6040 \[190\] 0.7090/0.4170 \[193\]

0.9660/0.9120

\[190\] 0.9190/0.8050 \[191\] 0.8580/0.7650 \[190\]

V2VFormer \[216\]

2024

-

-

0.6540/0.3610

\[216\] 0.9170/0.8760 \[216\]

-

-

0.6150/0.5500

\[216\]

CoBEVGlue \[193\]

2024 0.7400/0.5820

\[193\]

0.7020/0.4310

\[193\]

0.9580/0.9090

\[193\]

-

-

-

-

IFTR \[134\]

2024 0.2058/0.0665

\[134\]

-

-

0.8556/0.6604

\[134\]

0.7173/0.4967

\[134\]

-

-

V2X-M2C \[232\]

2024

-

-

-

-

0.8870/0.8280

\[232\]

0.9220/0.8600

\[232\]

-

-

CPSC \[142\]

2024 0.6542/0.4784

\[142\]

-

-

0.8911/0.7797

\[142\]

-

-

-

-

V2X-INCOP \[236\]

2024 0.6548/0.5526

\[236\]

-

-

0.9256/0.8318

\[236\]

-

-

-

-

RoCo\[191\]

2024 0.7630/0.6200

\[191\]

-

-

-

-

0.9190/0.8050

\[191\]

-

-

MACP \[228\]

2024

-

-

0.6760/0.4790

\[228\]

0.9370/0.9030

\[228\]

-

-

-

-

DI-V2X \[229\]

2024 0.7882/0.6616

\[229\]

-

-

-

-

0.9270/0.8270

\[229\]

-

-

MKD-Cooper \[218\]

2024

-

-

-

-

0.9650/0.9240

\[218\]

-

-

0.9300/0.8520

\[218\]

V2X-PC \[136\]

2024 0.7689/0.6939

\[136\]

-

-

-

-

0.9283/0.8955

\[136\]

-

-

of vehicles on adjacent lanes, driving in a string with induced the detection of occluded traffic participants and the evaluation oscillations to assess string stability, handling communication of collision risk \[312\]. A dataset has been produced from this interruptions in CACC mode, and evaluating the effects of project, containing laser scanner and video data from public positional inaccuracies in preceding or adjacent vehicles. 

intersections, and supports ongoing research on intersection The Autonomous Intersection Management \(AIM\) project perception and cooperative warning systems \[313\]. 

carried out in the U.S. explores autonomous traffic manage-The Virginia Connected Corridors \(VCC\) project in the ment at intersections without traditional traffic signals, using U.S. is led by the Virginia Department of Transportation a scalable multi-agent framework suitable for urban areas and the Virginia Tech Transportation Institute \[314\]. It serves

\[310\]. Recognizing the coexistence of autonomous and human-as a testbed for Connected and Autonomous Vehicle \(CAV\) driven vehicles, AIM introduced the Hybrid AIM protocol to applications. Since its launch in 2016, a fleet of 50 highly facilitate safer, more efficient integration at intersections. The instrumented light vehicles and 60 Roadside Units \(RSUs\) project employs augmented reality to create a mixed-reality have been deployed within the Northern Virginia Test Bed setup, simulating virtual traffic on real roads, allowing for for application testing. Each vehicle is equipped to communi-comprehensive testing of CP-enabled systems in dynamic and cate via DSRC with the surrounding connected infrastructure. 

complex scenarios. This project offers a valuable template When the vehicles are outside the range of a DSRC-equipped for urban areas aiming to reduce congestion through CP, RSU, they can use cellular technology for communication. A highlighting how CP can enhance intersection management by centralized cloud system is employed to manage the message enabling seamless coordination among diverse vehicle types. 

traffic between connected vehicles. The vehicles can connect The Ko-PER Project, carried out in Germany, focuses on to the cloud through either DSRC or cellular networks. It road safety, using distributed sensor networks to build a com-has been noted that cellular communications have a longer prehensive view of local traffic \[311\]. By integrating data from latency, ranging from 1.5 to 3.5 seconds, compared to DSRC

vehicle-mounted and infrastructure sensors, Ko-PER enables and are therefore used for applications where timely message

27

receipt is not critical. The aim of this project is to provide an traffic, ensuring stable and efficient cooperation. Key metrics, open development platform, allowing third-party developers to such as perception accuracy and energy efficiency, can guide test and deploy applications that enhance roadway safety and these decisions, with a fusion algorithm dynamically weighing mobility. 

factors like weather and traffic forecasts as conditions change. 

The iMOVE Cooperative Perception Project, led by the Aus-Effective implementation requires a cloud or edge-computing tralian Centre for Field Robotics at the University of Sydney in platform to aggregate real-time and historical data, enabling collaboration with Cohda Wireless, has demonstrated advance-CAVs to make informed, anticipatory collaboration choices. 

ments in pedestrian detection around corners through the use 2\) Real-world Communication Constraints: Existing CP

of CPMs and Dedicated Short-Range Communication \(DSRC\) methods have traditionally focused on optimizing perception technology \[315\]. Notably, this project illustrates how CAVs performance, often oversimplifying the critical challenges can autonomously and safely interact with pedestrians, both posed by real-world communication constraints such as limited walking and running, relying exclusively on CP information bandwidth, unstable channels, network congestion, and data provided by an intelligent roadside unit \(RSU\) \[315\]. This delays. These factors compromise the data received by the ego project represents one of the pioneering demonstrations of vehicle, and unlike conventional applications, retransmitting urban vehicle automation that relies solely on CP data for data in CP can render it unusable due to outdated information safe and efficient operation in complex environments. 

\[316\]. This results in missing data, asynchronous information These projects demonstrate the versatility of CP across from other agents, and, ultimately, inaccurate data fusion various traffic scenarios, including highway platooning, in-within the CP system. 

tersection management, and pedestrian detection in urban A promising approach is the integration of cross-layer areas. They underscore CP’s important role in addressing models to assess how communication constraints affect CP

perception gaps caused by occlusions or limited sensor range, algorithms \[317\], \[318\]. For example, combining network-ultimately leading to more reliable and robust autonomous layer routing with physical-layer channel modeling enables driving systems. Additionally, the challenges faced during CP systems to anticipate the effects of channel fading or these projects will inform the development of next-generation congestion on data transmission, facilitating adaptive adjust-CP algorithms and infrastructure to create safer and more ments in CP processes. Additionally, predictive perception efficient autonomous transportation ecosystems. 

models can enhance CP resilience by using historical data and probabilistic modeling to forecast surrounding vehicle VIII. LESSONS LEARNED

behavior, maintaining situational awareness even during data loss. This reduces dependency on continuous communication, CP technology plays a pivotal role in overcoming the ensuring reliable CP performance in real-world conditions. 

limitations inherent in single autonomous vehicles, addressing 3\) Malicious and Selfish Behavior: Trustworthy communi-issues like restricted perception range and obscured areas. 

cation is essential for fostering effective and safe CP. However, However, the unique characteristics of autonomous driving some road users may act in self-serving ways, collaborating and the evolution of communication technology bring forth only to reduce their own costs while potentially harming a multitude of challenges for CP. Drawing from recent re-others. These self-interested users, commonly known as “free-search and comprehensive analysis of cooperative autonomous riders, exploit shared information to benefit from coordinated driving, we have gleaned valuable insights and identified efforts without contributing their own insights to the collective open challenges and future directions that will significantly knowledge pool. Furthermore, the distributed deployment of influence the research trajectory in this field. 

multiple agents lowers defenses against cyber-attacks, increasing vulnerability to malicious activities by untrustworthy A. Challenges and Potential Solutions

users \[319\]. Malicious collaborators may deliberately transmit 1\) Collaboration Trigger: A prevailing challenge within CP

inaccurate environmental data, compromising the integrity of is the ability of each CAV to autonomously identify optimal CP by degrading data quality and reliability. This degradation opportunities for collaboration. Current research frequently not only disrupts CP effectiveness but also heightens risks to emphasizes predefined cooperative behaviors, often neglecting the safety of CAVs that rely on accurate, shared situational the necessity for ego CAVs to dynamically evaluate when col-awareness. 

laboration is advantageous. This process necessitates the devel-To tackle the challenges posed by unreliable collaborators opment of a mechanism referred to as a “collaboration trigger,” 

in CP, several strategies can enhance data reliability and safety. 

which assesses the trade-offs between independent actions and Implementing trust scoring and reputation systems allows collaborative efforts, informed by real-time conditions such as CAVs to prioritize data from agents with a history of reliability. 

weather, road attributes, and sensor performance. Furthermore, Machine learning-based anomaly detection can also identify ensuring stable and temporally consistent cooperation among unusual patterns that might indicate malicious behavior. Cross-multiple CAVs presents significant challenges, particularly in verifying data from multiple sources and utilizing multi-modal the context of dynamic driving scenarios. 

sensor fusion further improves the accuracy of CP, enabling To address these challenges, adaptive, context-aware sys-CAVs to detect and disregard inconsistent or unreliable inputs. 

tems are needed to determine when collaboration is optimal. 

Blockchain technology can introduce a decentralized layer of A dynamic decision model allows each ego CAV to assess trust by immutably logging data interactions, increasing agent real-time factors like sensor performance, road conditions, and accountability. Lastly, dynamic data prioritization ensures that

28

critical information, such as immediate obstacles, is priori-relying on rare real-life occurrences. Additionally, a model-tized, reducing the potential impact of harmful data. Together, driven data collection approach can be implemented, where these approaches strengthen the resilience of cooperative trained CP models actively monitor their predictions in real-perception, supporting safer and more reliable collaborative time. They can identify and flag low-confidence detections driving. 

or false positives/negatives as potential corner cases. These 4\) Generalizability in Real Scenarios: Constructing real-flagged instances can then be collected and prioritized for world scenes and collecting data for CP research presents further training. By creating datasets that encompass both substantial challenges, leading many CP methods to rely typical and rare autonomous driving conditions, CP systems on simulated datasets for development. While some recent can be better trained and validated, ultimately improving real-world datasets have emerged \[292\]–\[297\], they typically performance and reliability in real-world situations. 

involve limited agent participation, which fails to capture the full complexity of real-world collaborative scenarios. As a B. Future Directions

result, CP frameworks trained primarily on simulated datasets may struggle to generalize effectively in realistic collaboration 1\) Integrated Sensing and Communication for CP: In-settings. 

tegrated Sensing and Communication \(ISAC\) is an emerg-To address this gap, domain adaptation and synthetic data ing technology that utilizes the same frequency band and enhancement techniques offer promising solutions that can hardware for both sensing and communication \[322\]. This improve the applicability of CP models to real-world environ-innovation has the potential to significantly improve spectrum ments. Domain adaptation models, for instance, align features efficiency and reduce hardware costs. In the current context between simulated and real-world datasets through adversarial of cooperative autonomous driving, sensing and communica-training and transfer learning, reducing distributional discrep-tion systems typically operate on separate frequency bands. 

ancies and enabling CP models to perform more reliably in The widespread adoption of millimetre-wave and massive diverse, real-world settings \[320\]. 

MIMO technologies in infrastructure opens opportunities to In addition to domain adaptation, synthetic data enhance-implement radar perception in cooperative systems through ment techniques improve the realism of simulated datasets. 

ISAC. This enhances wireless communication throughput and One approach, described in \[321\], synthesizes training data radar perception resolution in future V2X networks. ISAC

using Augmented Reality, then refines it through a Generative is anticipated to be a critical technology in future V2X

Adversarial Network \(GAN\) to create robust photo-realistic CP, enabling low-latency, high-data-rate communication, and images under various weather and lighting conditions. Other high-resolution obstacle detection, particularly in challenging generative models, such as diffusion models, also play a vital scenarios like high occlusion and adverse weather. 

role by transforming simulated data into realistic visuals. 

2\) Responsible AI for CP: Cooperative autonomous driving These models adjust textures, lighting, and environmental relies heavily on Artificial Intelligence \(AI\), which excels in effects, effectively bridging the gap between synthetic and mastering increasingly complex computational tasks. Respon-real-world visuals. By enhancing dataset realism, these tech-sible AI initiatives can offer valuable insights for creating niques support more robust CP model training and improve realistic simulation environments that closely resemble real-generalization across varied real-world scenarios. 

world scenarios, benefiting the training and validation of 5\) Challenging Scenes and Corner Cases: While several V2X CP frameworks. Additionally, these initiatives can drive large-scale CP datasets have been developed in recent years, the development of domain adaptation techniques, enhancing many focus primarily on typical traffic situations and often knowledge transfer between simulated and real domains. This neglect challenging scenarios, particularly corner cases. Corner knowledge transfer improves the generalisation of the CP

cases are uncommon and extreme situations in autonomous model. Moreover, responsible AI efforts can stimulate the ad-driving, characterized by unusual conditions, hardware limi-vancement of deep learning methods tailored for generating CP

tations, or irregular obstacles, such as overturned vehicles or data featuring intricate scenarios and corner cases. Generative unusually shaped objects. These rare scenarios are frequently models and ethically guided data augmentation techniques are excluded from perception model training, which hinders the pivotal for constructing comprehensive datasets. This enriched models ability to identify objects accurately and can lead to dataset forms the basis for robust training for the V2X CP

missed or erroneous detections. Such inaccuracies in percep-system, equipping them to navigate and respond effectively to tion increase the risk of severe traffic accidents, highlighting challenging real-world situations. 

the urgent need for CP datasets that incorporate both intricate 3\) Privacy-preserved CP: To establish sustainable CP, en-scenarios and corner cases to support the development of more suring the privacy of data and messages exchanged via V2X

robust perception systems. 

communications is of paramount importance \[323\]. FL offers A combined approach of targeted data collection and syn-a viable solution to enhance CP intelligence while preserv-thetic data generation is essential to address the gap in corner ing privacy. FL facilitates intelligent CP by enabling fusion cases within CP datasets. Simulation environments can be algorithms to run on servers without requiring access to raw utilized to create synthetic data that replicates corner cases, data or information sharing. It employs a distributed training including overturned vehicles, unusual object shapes, and mechanism in which collaborating vehicles train localized scenarios with sensor occlusions. This method allows for the CP models using their data and then share only the trained generation of a wide variety of challenging conditions without model with the server for global aggregation \[324\]. This

29

approach ensures secure distributed learning, safeguarding significant performance improvement on planning and inter-the shared model from external adversaries. By prioritizing mediate perception outputs. 

privacy preservation, FL encourages more CAVs to participate in data perception, thus enhancing the overall robustness of CP

IX. CONCLUSIONS

systems. 

4\) Collaborative AI Integration for Enhanced CP and V2X

In this paper, we presented a comprehensive framework for Communication: In future intelligent transportation systems, V2X CP, addressing its foundational components and key as-efficient collaboration is envisaged between AI systems for pects. Through a novel taxonomic classification of mainstream V2X communication and AI systems for CP within each CAV. 

architectures and an in-depth literature review, we analyzed the The integration of AI into radio resource management for multifaceted challenges inherent to effective CP. We examined vehicle communication systems is driven by the imperative how V2X communication limitations, such as latency and to allocate communication resources efficiently, enabling real-data loss, can impact CP performance, emphasizing the need time data exchange among vehicles, infrastructure, and rel-for resilient communication strategies to maintain reliable evant entities \[325\]. International standardization efforts, led perception sharing. We also highlighted the value of open-by organizations like the 3GPP, are underway in anticipation source databases and simulators, which serve as essential of the 6G era. The forthcoming 6G technologies promise tools for evaluating and refining CP models in controlled unprecedented capabilities in data rates, low latency, and environments. These resources enable rigorous testing and accommodating a massive number of connected devices, all iterative optimization of CP algorithms, promoting advance-of which are crucial for CP in automated and connected ments in model accuracy and robustness. Furthermore, we transportation systems. 

underscored the importance of embedding ethical principles, In the context of CP, each CAV must intelligently determine such as fairness, transparency, and privacy, into the devel-the information it requires from other connected vehicles and opment and deployment of AI models for CP. Incorporating decide what information it should transmit to meet requests these principles fosters ethical AI usage in cooperative driving from other vehicles. This decision-making process is highly and supports the creation of realistic simulation environments, contingent on the dynamic traffic conditions. Therefore, each domain adaptation techniques, and diverse datasets, which are CAV’s AI system must efficiently manage CP’s necessary crucial for equipping CP models to handle the complexities of information, adapting to the current and near-future traffic real-world scenarios. In conclusion, CP is a rapidly evolving environment. However, to optimize information flow man-field with significant potential. By combining advanced V2X

agement, each CAV must collectively consider the available communication technologies, multimodal sensing, and AI-communication resources at their disposal. 

driven data processing, CP offers a pathway toward reliable, Consequently, further research is imperative to orchestrate efficient, and ethically sound solutions for autonomous driv-effective collaboration and coordination among distinct AI ing and intelligent transportation systems, ultimately enabling systems operating within individual CAVs and AI systems safer, more effective, and highly capable autonomous mobility. 

operating within the V2X network infrastructure. These AI systems must align their objectives and strategies to achieve REFERENCES

efficient CP, particularly in dynamic and complex traffic scenarios. Such endeavours are essential to harnessing the full

\[1\] Y. Li, L. Ma, Z. Zhong, F. Liu, M. A. Chapman, D. Cao, and J. Li, 

“Deep learning for LiDAR point clouds in autonomous driving: A potential of AI-driven CP to enhance road safety and traffic review,” IEEE Transactions on Neural Networks and Learning Systems, efficiency. 

vol. 32, no. 8, pp. 3412–3432, August 2021. 

5\) Migration of Advanced Perception Framework from Sin-

\[2\] X. Ma, W. Ouyang, A. Simonelli, and E. Ricci, “3D object detection from images for autonomous driving: A survey,” IEEE Transactions on gle Vehicle to Cooperative Vehicles: As the development of Pattern Analysis and Machine Intelligence, vol. 46, no. 5, pp. 3537–

transformer model \[326\] in both computer vision and large 3556, May 2024. 

language model areas, several advanced technologies have

\[3\] Y. Ma et al., “Vision-centric BEV perception: A survey,” IEEE Trans-been proposed for single-vehicle perception and autonomous actions on Pattern Analysis and Machine Intelligence, September 2024, 

doi:10.1109/TPAMI.2024.3449912. 

driving, e.g. end-to-end perception \[45\], \[327\], 3D occupancy

\[4\] Y. Cui, R. Chen, W. Chu, L. Chen, D. Tian, Y. Li, and D. Cao, “Deep grid prediction \[328\], \[329\], referring expression-based per-learning for image and point cloud fusion in autonomous driving: ception \[330\] with multi-modal large language model \[331\], 

A review,” IEEE Transactions on Intelligent Transportation Systems, vol. 23, no. 2, pp. 722–739, February 2022. 

self-supervised world-models for autonomous driving to boost

\[5\] J. Mao, S. Shi, X. Wang, and H. Li, “3D object detection for the downstream tasks by using the features extracted from autonomous driving: A comprehensive survey,” International Journal understanding and predicting/reconstruction of the environ-of Computer Vision, vol. 131, pp. 1909–1963, April 2023. 

\[6\] L. Wang, X. Zhang, Z. Song, J. Bi, G. Zhang, H. Wei, L. Tang, ment \[332\], \[333\], and end-to-end autonomous driving \[334\], 

L. Yang, J. Li, C. Jia, and L. Zhao, “Multi-modal 3D object detection

\[335\], etc. All of the aforementioned technologies have great in autonomous driving: A survey and taxonomy,” IEEE Transactions potential to be extended into cooperative vehicle settings as on Intelligent Vehicles, vol. 8, no. 7, pp. 3781–3798, July 2023. 

\[7\] Y. Shi, K. Jiang, J. Li, J. Wen, Z. Qian, M. Yang, K. Wang, and D. Yang, well, with the expectation of enhancing the capability of

“Grid-centric traffic scenario perception for autonomous driving: A autonomous driving. The most recent examples are \[336\], 

comprehensive review,” 2023, arXiv:2303.01212. 

\[337\] and \[338\]–\[340\], in which the end-to-end autonomous

\[8\] S. Yao et al., “Radar-camera fusion for object detection and semantic segmentation in autonomous driving: A comprehensive review,” IEEE

driving framework and 3D occupancy grid prediction function Transactions on Intelligent Vehicles, vol. 9, no. 1, pp. 2094–2128, are integrated with V2X cooperation, respectively, to achieve January 2024. 

30

\[9\] Y. Wang, W.-L. Chao, D. Garg, B. Hariharan, M. Campbell, and

\[27\] Y. Li et al., “Deepfusion: LiDAR-camera deep fusion for multi-modal K. Q. Weinberger, “Pseudo-LiDAR from visual depth estimation: 3D object detection,” in Proceedings of the IEEE/CVF Conference on Bridging the gap in 3D object detection for autonomous driving,” in Computer Vision and Pattern Recognition \(CVPR\), Louisiana, USA, Proceedings of the IEEE/CVF Conference on Computer Vision and 2022, pp. 17 182–17 191. 

Pattern Recognition \(CVPR\), Long Beach, CA, USA, 2019, pp. 8445–

\[28\] X. Bai, Z. Hu, X. Zhu, Q. Huang, Y. Chen, H. Fu, and C.-L. Tai, 8453. 

“Transfusion: Robust LiDAR-camera fusion for 3D object detection

\[10\] J. Philion and S. Fidler, “Lift, splat, shoot: Encoding images from with transformers,” in Proceedings of the IEEE/CVF Conference on arbitrary camera rigs by implicitly unprojecting to 3D,” in Proceedings Computer Vision and Pattern Recognition \(CVPR\), Louisiana, USA, of 16th European Conference on Computer Vision \(ECCV\), Glasgow, 2022, pp. 1090–1099. 

UK, 2020, pp. 194–210. 

\[29\] Z. Liu, H. Tang, A. Amini, X. Yang, H. Mao, D. Rus, and S. Han, 

\[11\] Z. Li, W. Wang, H. Li, E. Xie, C. Sima, T. Lu, Y. Qiao, and

“BEVFusion: Multi-task multi-sensor fusion with unified bird’s-eye J. Dai, “BEVFormer: Learning birds-eye-view representation from view representation,” in Proceedings of the IEEE International Confer-multi-camera images via spatiotemporal transformers,” in Proceedings ence on Robotics and Automation \(ICRA\), London, United Kingdom, of 17th European Conference on Computer Vision \(ECCV\), Tel Aviv, 2023, pp. 2774–2781. 

Israel, 2022, pp. 1–18. 

\[30\] X. Chen, T. Zhang, Y. Wang, Y. Wang, and H. Zhao, “FUTR3D: A

\[12\] Y. Su, Y. Di, G. Zhai, F. Manhardt, J. Rambach, B. Busam, D. Stricker, unified sensor fusion framework for 3D detection,” in Proceedings of and F. Tombari, “OPA-3D: Occlusion-aware pixel-wise aggregation the IEEE/CVF Conference on Computer Vision and Pattern Recognition for monocular 3D object detection,” IEEE Robotics and Automation \(CVPR\), Vabcouver, Canada, 2023, pp. 172–181. 

Letters, vol. 8, no. 3, pp. 1327–1334, March 2023. 

\[31\] J.-J. Hwang, H. Kretzschmar, J. Manela, S. Rafferty, N. Armstrong-

\[13\] H. Liu, Y. Teng, T. Lu, H. Wang, and L. Wang, “Sparsebev: High-Crews, T. Chen, and D. Anguelov, “CramNet: Camera-radar fusion performance sparse 3D object detection from multi-camera videos,” in with ray-constrained cross-attention for robust 3D object detection,” 

Proceedings of the IEEE/CVF International Conference on Computer in Proceedings of 17th European Conference on Computer Vision Vision, Paris, France, 2023, pp. 18 580–18 590. 

\(ECCV\), Tel Aviv, Israel, 2022, pp. 388–405. 

\[14\] S. Shi, X. Wang, and H. Li, “Pointrcnn: 3D object proposal generation

\[32\] T. Zhou, J. Chen, Y. Shi, K. Jiang, M. Yang, and D. Yang, “Bridging and detection from point cloud,” in Proceedings of the IEEE/CVF

the view disparity between radar and camera features for multi-modal Conference on Computer Vision and Pattern Recognition \(CVPR\), Long fusion 3D object detection,” IEEE Transactions on Intelligent Vehicles, Beach, CA, USA, 2019, pp. 770–779. 

vol. 8, no. 2, pp. 1523–1535, February 2023. 

\[15\] A. H. Lang, S. Vora, H. Caesar, L. Zhou, J. Yang, and O. Beijbom, 

\[33\] A. W. Harley, Z. Fang, J. Li, R. Ambrus, and K. Fragkiadaki, “Simple-

“Pointpillars: Fast encoders for object detection from point clouds,” in BEV: What really matters for multi-sensor BEV perception?” in Proceedings of the IEEE Conference on Computer Vision and Pattern Proceedings of the IEEE International Conference on Robotics and Recognition \(CVPR\), Long Beach, CA, USA, 2019, pp. 12 697–12 705. 

Automation \(ICRA\), London, United Kingdom, 2023, pp. 2759–2765. 

\[16\] T. Yin, X. Zhou, and P. Krahenbuhl, “Center-based 3D object detec-

\[34\] Z. Wu, G. Chen, Y. Gan, L. Wang, and J. Pu, “MVFusion: Multi-view tion and tracking,” in Proceedings of the IEEE/CVF Conference on 3D object detection with semantic-aligned radar and camera fusion,” 

Computer Vision and Pattern Recognition \(CVPR\), 2021, pp. 11 784–

in Proceedings of the IEEE International Conference on Robotics and 11 793. 

Automation \(ICRA\), London, United Kingdom, 2023, pp. 2766–2773. 

\[17\] C. He, R. Li, S. Li, and L. Zhang, “Voxel set transformer: A set-to-set

\[35\] Y. Kim, J. Shin, S. Kim, I.-J. Lee, J. W. Choi, and D. Kum, “CRN: approach to 3D object detection from point clouds,” in Proceedings of Camera radar net for accurate, robust, efficient 3D perception,” in the IEEE/CVF Conference on Computer Vision and Pattern Recognition Proceedings of the IEEE/CVF International Conference on Computer \(CVPR\), Louisiana, USA, 2022, pp. 8417–8427. 

Vision \(ICCV\), Paris, France, 2023, pp. 17 615–17 626. 

\[18\] T. Lu, X. Ding, H. Liu, G. Wu, and L. Wang, “LinK: Linear kernel

\[36\] L. Zheng, S. Li, B. Tan, L. Yang, S. Chen, L. Huang, J. Bai, for LiDAR-based 3D perception,” in Proceedings of the IEEE/CVF

X. Zhu, and Z. Ma, “RCFusion: Fusing 4D radar and camera with Conference on Computer Vision and Pattern Recognition \(CVPR\), birds-eye view features for 3D object detection,” IEEE Transactions Vancouver, Canada, 2023, pp. 1105–1115. 

on Instrumentation and Measurement, vol. 72, May 2023, Art. no. 

\[19\] H. Wu, C. Wen, S. Shi, X. Li, and C. Wang, “Virtual sparse convolution 8503814. 

for multimodal 3D object detection,” in Proceedings of the IEEE/CVF

\[37\] W. Xiong, J. Liu, T. Huang, Q.-L. Han, Y. Xia, and B. Zhu, “LXL: Conference on Computer Vision and Pattern Recognition \(CVPR\), LiDAR excluded lean 3D object detection with 4D imaging radar and Vancouver, Canada, 2023, pp. 21 653–21 662. 

camera fusion,” IEEE Transactions on Intelligent Vehicles, vol. 9, no. 1, 

\[20\] W. Xiong, J. Liu, Y. Xia, T. Huang, B. Zhu, and W. Xiang, “Contrastive pp. 79–92, 2024. 

learning for automotive mmWave radar detection points based instance

\[38\] F. Fent, A. Palffy, and H. Caesar, “DPFT: Dual perspective fusion trans-segmentation,” in Proceedings of the IEEE 25th International Conformer for camera-radar-based object detection,” arXiv:2404.03015, ference on Intelligent Transportation Systems \(ITSC\), Macau, China, 2024. 

2022, pp. 1255–1261. 

\[39\] K. Qian, S. Zhu, X. Zhang, and L. E. Li, “Robust multimodal vehicle

\[21\] J. Liu, W. Xiong, L. Bai, Y. Xia, T. Huang, W. Ouyang, and B. Zhu, detection in foggy weather using complementary LiDAR and radar

“Deep instance segmentation with automotive radar detection points,” 

signals,” in Proceedings of the IEEE/CVF Conference on Computer IEEE Transactions on Intelligent Vehicles, vol. 8, no. 1, pp. 84–94, Vision and Pattern Recognition \(CVPR\), 2021, pp. 444–453. 

January 2023. 

\[40\] Y.-J. Li, J. Park, M. O’Toole, and K. Kitani, “Modality-agnostic learn-

\[22\] A. Palffy, J. Dong, J. F. Kooij, and D. M. Gavrila, “CNN based road ing for Radar-LiDAR fusion in vehicle detection,” in Proceedings of user detection using the 3D radar cube,” IEEE Robotics and Automation the IEEE/CVF Conference on Computer Vision and Pattern Recognition Letters, vol. 5, no. 2, pp. 1263–1270, April 2020. 

\(CVPR\), Louisiana, USA, 2022, pp. 918–927. 

\[23\] L. Zheng et al., “TJ4DRadSet: A 4D radar dataset for autonomous

\[41\] Y. Yang, J. Liu, T. Huang, Q.-L. Han, G. Ma, and B. Zhu, “RaLiBEV: driving,” in Proceedings of the IEEE 25th International Conference Radar and LiDAR BEV fusion learning for anchor box free object on Intelligent Transportation Systems \(ITSC\), Macau, China, 2022, pp. 

detection systems,” 2022, arXiv:2211.06108. 

493–498. 

\[42\] S. Scheidegger, J. Benjaminsson, E. Rosenberg, A. Krishnan, and

\[24\] B. Tan, Z. Ma, X. Zhu, S. Li, L. Zheng, S. Chen, L. Huang, and J. Bai, K. Granström, “Mono-camera 3D multi-object tracking using deep

“3D object detection for multi-frame 4D automotive millimeter-wave learning detections and pmbm filtering,” in 2018 IEEE Intelligent radar point cloud,” IEEE Sensors Journal, vol. 23, no. 11, pp. 11 125–

Vehicles Symposium \(IV\). 

IEEE, 2018, pp. 433–440. 

11 138, June 2023. 

\[43\] C. Cui, R. Song, X. Li, and Y. Ai, “Bevmot: A multi-object detec-

\[25\] J. Liu, Q. Zhao, W. Xiong, T. Huang, Q.-L. Han, and B. Zhu, “SMURF: tion and tracking method in bird’s-eye-view via spatiotemporal trans-Spatial multi-representation fusion for 3D object detection with 4D

formers,” in 2023 IEEE 26th International Conference on Intelligent imaging radar,” IEEE Transactions on Intelligent Vehicles, vol. 9, no. 1, Transportation Systems \(ITSC\). 

IEEE, 2023, pp. 5446–5451. 

pp. 799–812, 2024. 

\[44\] T. Zhang, X. Chen, Y. Wang, Y. Wang, and H. Zhao, “Mutr3d: A multi-

\[26\] K. Zhao, L. Ma, Y. Meng, L. Liu, J. Wang, J. M. Junior, W. N. 

camera tracking framework via 3d-to-2d queries,” in Proceedings of the Gonc¸alves, and J. Li, “3D vehicle detection using multi-level fusion IEEE/CVF Conference on Computer Vision and Pattern Recognition from point clouds and images,” IEEE Transactions on Intelligent \(CVPR\) Workshop, 2022, pp. 4537–4546. 

Transportation Systems, vol. 23, no. 9, pp. 15 146–15 154, September

\[45\] Y. Li, Z. Yu, J. Philion, A. Anandkumar, S. Fidler, J. Jia, and J. Alvarez, 2022. 

“End-to-end 3d tracking with decoupled queries,” in Proceedings of

31

the IEEE/CVF International Conference on Computer Vision, 2023, 

\[66\] R. Krecht, T. Budai, E. Horvth, . Kovcs, N. Mark, and M. Unger, pp. 18 302–18 311. 

“Network optimization aspects of autonomous vehicles: Challenges

\[46\] G. Guo and S. Zhao, “3D multi-object tracking with adaptive cubature and future directions,” IEEE Network, vol. 37, no. 4, pp. 282–288, Kalman filter for autonomous driving,” IEEE Transactions on Intelli-JulyAugust 2023. 

gent Vehicles, vol. 8, no. 1, pp. 512–519, February 2023. 

\[67\] H. Ngo, H. Fang, and H. Wang, “Cooperative perception with V2V

\[47\] H. Wu, W. Han, C. Wen, X. Li, and C. Wang, “3D multi-object communication for autonomous vehicles,” IEEE Transactions on Ve-tracking in point clouds based on prediction confidence-guided data hicular Technology, vol. 72, no. 9, pp. 11 122–11 131, September 2023. 

association,” IEEE Transactions on Intelligent Transportation Systems, 

\[68\] T. Huang, X. Yuan, J. Yuan, and W. Xiang, “Optimization of data vol. 23, no. 6, pp. 5668–5677, June 2022. 

exchange in 5G vehicle-to-infrastructure edge networks,” IEEE Trans-

\[48\] J. Liu, L. Bai, Y. Xia, T. Huang, B. Zhu, and Q.-L. Han, “GNN-PMB: actions on Vehicular Technology, vol. 69, no. 9, pp. 9376–9389, A simple but effective online 3D multi-object tracker without bells and September 2020. 

whistles,” IEEE Transactions on Intelligent Vehicles, vol. 8, no. 2, pp. 

\[69\] R. Fukatsu and K. Sakaguchi, “Automated driving with cooperative 1176–1189, February 2023. 

perception using millimeter-wave V2I communications for safe and

\[49\] Z. Zhang, J. Liu, Y. Xia, T. Huang, Q.-L. Han, and H. Liu, “LEGO: efficient passing through intersections,” in Proceedings of the IEEE

Learning and graph-optimized modular tracker for online multi-object Vehicular Technology Conference \(VTC\), Helsinki, Finland, 2021, pp. 

tracking with point clouds,” 2023, arXiv:2308.09908. 

1–5. 

\[50\] T. Sadjadpour, J. Li, R. Ambrus, and J. Bohg, “ShaSTA: Modeling

\[70\] R. Q. Malik, K. N. Ramli, Z. H. Kareem, M. I. Habelalmatee, A. H. Ab-shape and spatio-temporal affinities for 3D multi-object tracking,” IEEE

bas, and A. Alamoody, “An overview on v2p communication system: Robotics and Automation Letters, vol. 9, no. 5, pp. 4273–4280, May Architecture and application,” in 2020 3rd International Conference 2024. 

on Engineering Technology and its Applications \(IICETA\), Najaf, Iraq, 

\[51\] G. Ding, J. Liu, Y. Xia, T. Huang, B. Zhu, and J. Sun, “Lidar point 2020, pp. 174–178. 

cloud-based multiple vehicle tracking with probabilistic measurement-

\[71\] Y. He, B. Wu, Z. Dong, J. Wan, and W. Shi, “Towards C-V2X enabled region association,” in Proceedings of the International Conference on collaborative autonomous driving,” IEEE Transactions on Vehicular Information Fusion \(FUSION\), 2024, arXiv:2403.06423. 

Technology, vol. 72, no. 12, pp. 15 450–15 462, December 2023. 

\[52\] Z. Zhang, X. Wang, D. Huang, X. Fang, M. Zhou, and Y. Zhang, 

\[72\] H. Zhou, W. Xu, J. Chen, and W. Wang, “Evolutionary V2X technolo-

“MRPT: Millimeter-wave radar-based pedestrian trajectory tracking for gies toward the internet of vehicles: Challenges and opportunities,” 

autonomous urban driving,” IEEE Transactions on Instrumentation and Proceedings of the IEEE, vol. 108, no. 2, pp. 308–323, February 2020. 

Measurement, vol. 71, December 2021, Art. no. 8000117. 

\[73\] C. Pilz, A. Ulbel, and G. Steinbauer-Wagner, “The components of

\[53\] K. Shi, Z. Shi, C. Yang, S. He, J. Chen, and A. Chen, “Road-map cooperative perception-a proposal for future works,” in Proceedings aided GM-PHD filter for multi-vehicle tracking with automotive radar,” 

of the IEEE International Conference on Intelligent Transportation IEEE Transactions on Industrial Informatics, vol. 18, no. 1, pp. 97–

Systems \(ITSC\), Indianapolis, IN, USA, 2021, pp. 7–14. 

108, January 2022. 

\[74\] G. Li, C. Lai, R. Lu, and D. Zheng, “SecCDV: A security reference

\[54\] C. Yang, X. Cao, and Z. Shi, “Road-map aided Gaussian mixture architecture for Cybertwin-Driven 6G V2X,” IEEE Transactions on labeled multi-bernoulli filter for ground multi-target tracking,” IEEE

Vehicular Technology, vol. 71, no. 5, pp. 4535–4550, May 2022. 

Transactions on Vehicular Technology, vol. 72, no. 6, pp. 7137–7147, 

\[75\] R. Kumar, P. Kumar, R. Tripathi, G. P. Gupta, S. Garg, and M. M. 

June 2023. 

Hassan, “BDTwin: An integrated framework for enhancing security and

\[55\] J. Liu et al., “Which framework is suitable for online 3d multi-object privacy in Cybertwin-Driven automotive industrial internet of things,” 

tracking for autonomous driving with automotive 4d imaging radar?” 

IEEE Internet of Things Journal, vol. 9, no. 18, pp. 17 110–17 119, in 2024 IEEE Intelligent Vehicles Symposium \(IV\), Jeju Island, Korea, September 2022. 

2024, pp. 1258–1265. 

\[76\] Y. Lu, X. Huang, Y. Dai, S. Maharjan, and Y. Zhang, “Federated

\[56\] J. Bai, S. Li, L. Huang, and H. Chen, “Robust detection and tracking learning for data privacy preservation in vehicular cyber-physical method for moving object based on radar and camera data fusion,” 

systems,” IEEE Network, vol. 34, no. 3, pp. 50–56, MayJune 2020. 

IEEE Sensors Journal, vol. 21, no. 9, pp. 10 761–10 774, May 2021. 

\[77\] H. Wang, A. Khajepour, D. Cao, and T. Liu, “Ethical decision making

\[57\] Z. Liu, Y. Cai, H. Wang, L. Chen, H. Gao, Y. Jia, and Y. Li, “Robust in autonomous vehicles: Challenges and research progress,” IEEE

target recognition and tracking of self-driving cars with radar and Intelligent Transportation Systems Magazine, vol. 14, no. 1, pp. 6–17, camera information fusion under severe weather conditions,” IEEE

January-February 2022. 

Transactions on Intelligent Transportation Systems, vol. 23, no. 7, pp. 

\[78\] A. Arora, A. Jain, D. Yadav, V. Hassija, V. Chamola, and B. Sikdar, 6640–6653, July 2022. 

“Next generation of multi-agent driven smart city applications and

\[58\] L. Lindenmaier, S. Aradi, T. Bécsi, O. Tör˝o, and P. Gáspár, “GM-research paradigms,” IEEE Open Journal of the Communications PHD filter based sensor data fusion for automotive frontal perception Society, vol. 4, pp. 2104–2121, August 2023. 

system,” IEEE Transactions on Vehicular Technology, vol. 71, no. 7, 

\[79\] H. Mosavat-Jahromi, Y. Li, L. Cai, and L. Lu, “NCMAC: A distributed pp. 7215–7229, July 2022. 

mac protocol for reliable beacon broadcasting in V2X,” IEEE Trans-

\[59\] M. Lei, D. Yang, and X. Weng, “Integrated sensor fusion based actions on Vehicular Technology, vol. 70, no. 6, pp. 6044–6057, June on 4D MIMO radar and camera: A solution for connected vehicle 2021. 

applications,” IEEE Vehicular Technology Magazine, vol. 17, no. 4, 

\[80\] W. Jiang, H. Xiang, X. Cai, R. Xu, J. Ma, Y. Li, G. H. Lee, and pp. 38–46, December 2022. 

S. Liu, “Optimizing the placement of roadside LiDARs for autonomous

\[60\] A. Kim, A. Ošep, and L. Leal-Taixé, “EagerMOT: 3D multi-object driving,” in Proceedings of the IEEE/CVF International Conference on tracking via sensor fusion,” in Proceedings of the IEEE International Computer Vision \(ICCV\), Paris, France, 2023, pp. 18 381–18 390. 

Conference on Robotics and Automation \(ICRA\), Xi’an, China, 2021, 

\[81\] S. Chen, J. Hu, Y. Shi, L. Zhao, and W. Li, “A vision of C-V2X: pp. 11 315–11 321. 

Technologies, field testing, and challenges with chinese development,” 

\[61\] H.-k. Chiu, J. Li, R. Ambrus¸, and J. Bohg, “Probabilistic 3D multi-IEEE Internet of Things Journal, vol. 7, no. 5, pp. 3872–3881, May modal, multi-object tracking for autonomous driving,” in Proceedings 2020. 

of the IEEE International Conference on Robotics and Automation

\[82\] S.-Y. Lien and H.-L. Tsai, “3GPP V2X on unlicensed spectrum: \(ICRA\), Xi’an, China, 2021, pp. 14 227–14 233. 

Performance analysis and optimum channel access strategies,” IEEE

\[62\] X. Wang, C. Fu, Z. Li, Y. Lai, and J. He, “DeepFusionMOT: A 3D

Transactions on Vehicular Technology, vol. 70, no. 9, pp. 9230–9243, multi-object tracking framework based on camera-LiDAR fusion with September 2021. 

deep association,” IEEE Robotics and Automation Letters, vol. 7, no. 3, 

\[83\] M. Nichting, D. He, J. Schindler, T. Hesse, and F. Kster, “Space time pp. 8260–8267, July 2022. 

reservation procedure \(STRP\) for V2X-Based maneuver coordination

\[63\] L. Wang et al., “CAMO-MOT: Combined appearance-motion optimiza-of cooperative automated vehicles in diverse conflict scenarios,” in tion for 3D multi-object tracking with Camera-LiDAR fusion,” IEEE

Proceedings of IEEE Intelligent Vehicles Symposium \(IV\), Las Vegas, Transactions on Intelligent Transportation Systems, vol. 24, no. 11, pp. 

NV, USA, 2020, pp. 502–509. 

11 981–11 996, November 2023. 

\[84\] J. Lu, Z. Peng, S. Yang, Y. Ma, R. Wang, Z. Pang, X. Feng, Y. Chen, 

\[64\] L. Li and C. Sun, “NLOS Dies Twice: Challenges and solutions of and Y. Cao, “A review of sensory interactions between autonomous V2X for cooperative perception,” 2023, arXiv:2307.06615. 

vehicles and drivers,” Journal of Systems Architecture, vol. 141, p. 

\[65\] K. Ren, Q. Wang, C. Wang, Z. Qin, and X. Lin, “The security of 102932, August 2023. 

autonomous driving: Threats, defenses, and future directions,” Proceed-

\[85\] Q. Yang, S. Fu, H. Wang, and H. Fang, “Machine-learning-enabled ings of the IEEE, vol. 108, no. 2, pp. 357–372, February 2020. 

cooperative perception for connected autonomous vehicles: Challenges

32

and opportunities,” IEEE Network, vol. 35, no. 3, pp. 96–101, June

\[104\] H. Li and F. Nashashibi, “Multi-vehicle cooperative perception and 2021. 

augmented reality for driver assistance: A possibility to see through

\[86\] Z. Bai, G. Wu, X. Qi, Y. Liu, K. Oguchi, and M. J. Barth, front vehicle,” in Proceedings of the International Conference on

“Infrastructure-based object detection and tracking for cooperative Intelligent Transportation Systems \(ITSC\), Washington, DC, USA, driving automation: A survey,” in Proceedings of the IEEE Intelligent 2011, pp. 242–247. 

Vehicles Symposium \(IV\), Aachen, Germany, June 2022, pp. 1366–

\[105\] A. Rauch, F. Klanner, R. Rasshofer, and K. Dietmayer, “Car2X-based 1373. 

perception in a high-level fusion architecture for cooperative perception

\[87\] A. Caillot, S. Ouerghi, P. Vasseur, R. Boutteau, and Y. Dupuis, systems,” in Proceedings of the IEEE Intelligent Vehicles Symposium

“Survey on cooperative perception in an automotive context,” IEEE

\(IV\), Madrid, Spain, 2012, pp. 270–275. 

Transactions on Intelligent Transportation Systems, vol. 23, no. 9, pp. 

\[106\] M. Vasic and A. Martinoli, “A collaborative sensor fusion algorithm for 14 204–14 223, March 2022. 

multi-object tracking using a Gaussian mixture probability hypothesis

\[88\] C. Xiang, C. Feng, X. Xie, B. Shi, H. Lu, Y. Lv, M. Yang, and Z. Niu, density filter,” in Proceedings of the IEEE International Conference

“Multi-sensor fusion and cooperative perception for autonomous driv-on Intelligent Transportation Systems, Gran Canaria, Spain, 2015, pp. 

ing: A review,” IEEE Intelligent Transportation Systems Magazine, 491–498. 

vol. 15, no. 5, pp. 36–58, 2023. 

\[107\] S.-W. Kim and W. Liu, “Cooperative autonomous driving: A mirror

\[89\] Z. Bai et al., “A survey and framework of cooperative percep-neuron inspired intention awareness and cooperative perception ap-tion: From heterogeneous singleton to hierarchical cooperation,” 

proach,” IEEE Intelligent Transportation Systems Magazine, vol. 8, IEEE Transactions on Intelligent Transportation Systems, 2024, no. 3, pp. 23–32, July 2016. 

doi:10.1109/TITS.2024.3436012. 

\[108\] J. Redmon, S. Divvala, R. Girshick, and A. Farhadi, “You only look

\[90\] Y. Han, H. Zhang, H. Li, Y. Jin, C. Lang, and Y. Li, “Collaborative once: Unified, real-time object detection,” in Proceedings of the IEEE

perception in autonomous driving: Methods, datasets, and challenges,” 

Conference on computer vision and pattern recognition \(CVPR\), Las IEEE Intelligent Transportation Systems Magazine, vol. 15, no. 6, pp. 

Vegas, NV, USA, 2016, pp. 779–788. 

131–151, 2023. 

\[109\] G. Huang, Z. Liu, L. Van Der Maaten, and K. Q. Weinberger, 

\[91\] S. Liu, C. Gao, Y. Chen, X. Peng, X. Kong, K. Wang, R. Xu, 

“Densely connected convolutional networks,” in Proceedings of the W. Jiang, H. Xiang, J. Ma, and M. Wang, “Towards vehicle-to-IEEE conference on computer vision and pattern recognition \(CVPR\), everything autonomous driving: A survey on collaborative perception,” 

Honolulu, HI, USA, 2017, pp. 4700–4708. 

2023, arXiv:2308.16714. 

\[110\] Z. Y. Rawashdeh and Z. Wang, “Collaborative automated driving: A

\[92\] X. Gao, X. Zhang, Y. Lu, Y. Huang, L. Yang, Y. Xiong, and P. Liu, machine learning-based method to enhance the accuracy of shared

“A survey of collaborative perception in intelligent vehicles at inter-information,” in Proceedings of the International Conference on In-sections,” IEEE Transactions on Intelligent Vehicles, pp. 1–20, 2024, telligent Transportation Systems \(ITSC\), Maui, HI, USA, 2018, pp. 

doi:10.1109/TIV.2024.3395783. 

3961–3966. 

\[93\] B. Gao, J. Liu, H. Zou, J. Chen, L. He, and K. Li, “Vehicle-road-

\[111\] M.-Q. Dao, J. S. Berrio, V. Frmont, M. Shan, E. Hry, and S. Worrall, cloud collaborative perception framework and key technologies: A

“Practical collaborative perception: A framework for asynchronous review,” IEEE Transactions on Intelligent Transportation Systems, and multi-agent 3d object detection,” IEEE Transactions on Intelligent 2024, doi:10.1109/TITS.2024.3459799. 

Transportation Systems, pp. 1–13, 2024. 

\[94\] J. McCarthy, S. R. Chaudhry, P. Kuppuudaiyar, R. Loomba, and

\[112\] ETSI. \(2019, April\) Intelligent transport systems \(ITS\); vehicular S. Clarke, “QoSA-ICN: An information-centric approach to QoS in ve-communications; basic set of applications; part 2: Specification hicular environments,” Vehicular Communications, vol. 30, p. 100351, of

cooperative

awareness

basic

service. 

ETSI

EN

302

637-

August 2021. 

2 V1.4.1. \[Online\]. Available: https://www.etsi.org/deliver/etsi en/

\[95\] L. Li, Y. Cheng, C. Sun, and W. Zhang, “Icop: Image-based cooperative

302600 302699/30263702/01.04.01 60/en 30263702v010401p.pdf

perception for end-to-end autonomous driving,” in Proceedings of the

\[113\] ——. \(2019, December\) Intelligent transport systems \(ITS\); vehicular IEEE Intelligent Vehicles Symposium \(IV\), 2024, pp. 2367–2374. 

communications; basic set of applications; analysis of the collective

\[96\] X. Liu, B. Li, R. Xu, J. Ma, X. Li, J. Li, and H. Yu, “V2x-dsi: A perception service \(CPS\); release 2. ETSI TR 103 562 V2.1.1. \[Online\]. 

density-sensitive infrastructure lidar benchmark for economic vehicle-Available: https://www.etsi.org/deliver/etsi tr/103500 103599/103562/

to-everything cooperative perception,” in Proceedings of the IEEE

02.01.01 60/tr 103562v020101p.pdf

Intelligent Vehicles Symposium \(IV\), 2024, pp. 490–495. 

\[114\] G. Kueppers, J.-P. Busch, L. Reiher, and L. Eckstein, “V2aix: A multi-

\[97\] Q. Chen, S. Tang, Q. Yang, and S. Fu, “Cooper: Cooperative perception modal real-world dataset of etsi its v2x messages in public road traffic,” 

for connected autonomous vehicles based on 3D point clouds,” in arXiv preprint arXiv:2403.10221, 2024. 

Proceedings of the IEEE International Conference on Distributed

\[115\] Y.-C. Liu, J. Tian, C.-Y. Ma, N. Glaser, C.-W. Kuo, and Z. Kira, Computing Systems \(ICDCS\), Dallas, TX, USA, 2019, pp. 514–524. 

“Who2com: Collaborative perception via learnable handshake com-

\[98\] R. Chen, Y. Mu, R. Xu, W. Shao, C. Jiang, H. Xu, Y. Qiao, Z. Li, and munication,” in Proceedings of the IEEE International Conference on P. Luo, “CO3: Cooperative unsupervised 3D representation learning for Robotics and Automation \(ICRA\), Paris, France, 2020, pp. 6876–6883. 

autonomous driving,” in Proceedings of the International Conference

\[116\] Y.-C. Liu, J. Tian, N. Glaser, and Z. Kira, “When2com: Multi-agent on Learning Representations \(ICLR\), Kigali, Rwanda, 2023. 

perception via communication graph grouping,” in Proceedings of the

\[99\] Z. Li, T. Yu, T. Suzuki, and K. Sakaguchi, “Building an SDVN

IEEE/CVF Conference on Computer Vision and Pattern Recognition framework for rsu-centric cooperative perception with heterogeneous \(CVPR\), 2020, pp. 4106–4115. 

V2X,” in Proceedings of the IEEE Consumer Communications & 

\[117\] J. Wang, Y. Zeng, and Y. Gong, “Collaborative 3D object detection Networking Conference \(CCNC\), Las Vegas, NV, USA, January 2023, for automatic vehicle systems via learnable communications,” IEEE

pp. 1–7. 

Transactions on Intelligent Transportation Systems, vol. 24, no. 9, pp. 

\[100\] B. C. Tedeschini et al., “Cooperative LiDAR sensing for pedestrian 9804–9816, September 2023. 

detection: Data association based on message passing neural networks,” 

\[118\] Y. Jia, R. Mao, Y. Sun, S. Zhou, and Z. Niu, “Online V2X scheduling IEEE Transactions on Signal Processing, vol. 71, pp. 3028–3042, for raw-level cooperative perception,” in Proceedings of the IEEE

August 2023. 

International Conference on Communications \(ICC\), Seoul, Korea, 

\[101\] S.-W. Kim, B. Qin, Z. J. Chong, X. Shen, W. Liu, M. H. Ang, 2022, pp. 309–314. 

E. Frazzoli, and D. Rus, “Multivehicle cooperative driving using

\[119\] ——, “MASS: Mobility-aware sensor scheduling of cooperative per-cooperative perception: Design and experimental validation,” IEEE

ception for connected automated driving,” IEEE Transactions on Vehic-Transactions on Intelligent Transportation Systems, vol. 16, no. 2, pp. 

ular Technology, vol. 72, no. 11, pp. 14 962–14 977, November 2023. 

663–680, April 2015. 

\[120\] H.-k. Chiu and S. F. Smith, “Selective communication for co-

\[102\] S.-W. Kim, W. Liu, M. H. Ang, E. Frazzoli, and D. Rus, “The impact of operative perception in end-to-end autonomous driving,” 2023, cooperative perception on decision making and planning of autonomous arXiv:2305.17181. 

vehicles,” IEEE Intelligent Transportation Systems Magazine, vol. 7, 

\[121\] Y. 

Liu, 

Q. 

Huang, 

R. 

Li, 

X. 

Chen, 

Z. 

Zhao, 

S. 

Zhao, 

no. 3, pp. 39–50, July 2015. 

Y. Zhu, and H. Zhang, “Rethinking collaborative perception from

\[103\] M. Rockl, T. Strang, and M. Kranz, “V2V communications in auto-the spatial-temporal importance of semantic information,” 2023, motive multi-sensor multi-target tracking,” in Proceedings of the IEEE

arXiv:2307.16517. 

Vehicular Technology Conference \(VTC\), Calgary, AB, Canada, 2008, 

\[122\] W. Wang, H. Xu, and G. Tan, “Intercoop: Spatio-temporal interaction pp. 1–5. 

aware cooperative perception for networked vehicles,” in Proceedings

33

of the IEEE International Conference on Robotics and Automation sion,” IEEE Transactions on Vehicular Technology, pp. 1–9, 2024, \(ICRA\), 2024, pp. 14 443–14 449. 

doi:10.1109/TVT.2024.3403263. 

\[123\] C. Allig and G. Wanielik, “Dynamic dissemination method for collec-

\[143\] E. E. Marvasti, A. Raftari, A. E. Marvasti, Y. P. Fallah, R. Guo, and tive perception,” in Proceedings of the IEEE Intelligent Transportation H. Lu, “Cooperative LiDAR object detection via feature sharing in Systems Conference \(ITSC\), Auckland, New Zealand, 2019, pp. 3756–

deep networks,” in Proceedings of the IEEE Vehicular Technology 3762. 

Conference \(VTC2020-Fall\), Victoria, BC, Canada, 2020, pp. 1–7. 

\[124\] H. Masuda, O. E. Marai, M. Tsukada, T. Taleb, and H. Esaki, “Feature-

\[144\] Y. Li, S. Ren, P. Wu, S. Chen, C. Feng, and W. Zhang, “Learning dis-based vehicle identification framework for optimization of collective tilled collaboration graph for multi-agent perception,” in Proceedings perception messages in vehicular networks,” IEEE Transactions on of the Advances in Neural Information Processing Systems \(NeurIPS\), Vehicular Technology, vol. 72, no. 2, pp. 2120–2129, February 2023. 

vol. 34, 2021, pp. 29 541–29 552. 

\[125\] G. Thandavarayan, M. Sepulcre, and J. Gozalvez, “Redundancy mitiga-

\[145\] R. Xu, H. Xiang, Z. Tu, X. Xia, M.-H. Yang, and J. Ma, “V2X-ViT: tion in cooperative perception for connected and automated vehicles,” 

Vehicle-to-everything cooperative perception with vision transformer,” 

in Proceedings of the IEEE Vehicular Technology Conference \(VTC\), in Proceedings of the European Conference on Computer Vision Antwerp, Belgium, 2020, pp. 1–5. 

\(ECCV\), Tel Aviv, Israel, 2022, pp. 107–124. 

\[126\] ——, “Generation of cooperative perception messages for connected

\[146\] J. Cui, H. Qiu, D. Chen, P. Stone, and Y. Zhu, “Coopernaut: End-and automated vehicles,” IEEE Transactions on Vehicular Technology, to-end driving with cooperative perception for networked vehicles,” 

vol. 69, no. 12, pp. 16 336–16 341, November 2020. 

in Proceedings of the IEEE/CVF Conference on Computer Vision

\[127\] P. Zhou, P. Kortoc¸i, Y.-P. Yau, B. Finley, X. Wang, T. Braud, L.-

and Pattern Recognition \(CVPR\), Louisiana, USA, 2022, pp. 17 252–

H. Lee, S. Tarkoma, J. Kangasharju, and P. Hui, “AICP: Augmented 17 262. 

informative cooperative perception,” IEEE Transactions on Intelligent

\[147\] L. Zhou, Z. Gan, and J. Fan, “CenterCoop: Center-based feature aggre-Transportation Systems, vol. 23, no. 11, pp. 22 505–22 518, November gation for communication-efficient vehicle-infrastructure cooperative 2022. 

3d object detection,” IEEE Robotics and Automation Letters, vol. 9, 

\[128\] Z. Bai, G. Wu, M. J. Barth, Y. Liu, E. A. Sisbot, and K. Oguchi, no. 4, pp. 3570–3577, 2024. 

“Cooperverse: A mobile-edge-cloud framework for universal cooperative perception with mixed connectivity and automation,” 2023, 

\[148\] J. Guo, D. Carrillo, Q. Chen, Q. Yang, S. Fu, H. Lu, and R. Guo, “Slim-arXiv:2302.03128. 

FCP: Lightweight-feature-based cooperative perception for connected

\[129\] B. Zhao, W. ZHANG, and Z. Zou, “BM2CP: Efficient collaborative automated vehicles,” IEEE Internet of Things Journal, vol. 9, no. 17, perception with LiDAR-camera modalities,” in Conference on Robot pp. 15 630–15 638, September 2022. 

Learning \(CoRL\), Atlanta, USA, 2023, pp. 1022–1035. 

\[149\] Z. Wang, S. Fan, X. Huo, T. Xu, Y. Wang, J. Liu, Y. Chen, and Y.-Q. 

\[130\] S. Aoki, T. Higuchi, and O. Altintas, “Cooperative perception with Zhang, “Emiff: Enhanced multi-scale image feature fusion for vehicle-deep reinforcement learning for connected vehicles,” in Proceedings of infrastructure cooperative 3d object detection,” in Proceedings of the the IEEE Intelligent Vehicles Symposium \(IV\), Las Vegas, NV, USA, IEEE International Conference on Robotics and Automation \(ICRA\), 2020, pp. 328–334. 

2024, pp. 16 388–16 394. 

\[131\] Y. Yuan, H. Cheng, and M. Sester, “Keypoints-based deep feature

\[150\] K. Yang, D. Yang, J. Zhang, H. Wang, P. Sun, and L. Song, fusion for cooperative vehicle detection of autonomous driving,” IEEE

“What2comm: Towards communication-efficient collaborative percep-Robotics and Automation Letters, vol. 7, no. 2, pp. 3054–3061, January tion via feature decoupling,” in Proceedings of the 31st ACM Inter-2022. 

national Conference on Multimedia, Ottawa, ON, Canada, 2023, pp. 

\[132\] T. Wang, G. Chen, K. Chen, Z. Liu, B. Zhang, A. Knoll, and C. Jiang, 7686–7695. 

“UMC: A unified bandwidth-efficient and multi-resolution based col-

\[151\] Y. Zhang, H. An, Z. Fang, G. Xu, Y. Zhou, X. Chen, and Y. Fang, laborative perception framework,” in Proceedings of the IEEE/CVF

“Smartcooper: Vehicular collaborative perception with adaptive fusion international conference on computer vision \(ICCV\), Paris, France, and judger mechanism,” in Proceedings of the IEEE International 2023, pp. 8187–8196. 

Conference on Robotics and Automation \(ICRA\), 2024, pp. 4450–4456. 

\[133\] Y. Yuan, H. Cheng, M. Y. Yang, and M. Sester, “Generating evidential

\[152\] M.-T. Luong, H. Pham, and C. D. Manning, “Effective approaches to BEV maps in continuous driving space,” 2023, arXiv:2302.02928. 

attention-based neural machine translation,” in Proc. Conf. Empirical

\[134\] S. Wang, L. Bin, X. Xiao, Z. Xiang, H. Shan, and E. Liu, “Iftr: An Methods Natural Lang. Process., Lisbon, Portugal, 2015, pp. 1412–

instance-level fusion transformer for visual collaborative perception,” 

## 1421. 

2024, arXiv:2407.09857. 

\[153\] A. Slivkins, “Introduction to multi-armed bandits,” Foundations and

\[135\] Y. Hu, J. Peng, S. Liu, J. Ge, S. Liu, and S. Chen, “Communication-Trends® in Machine Learning, vol. 12, no. 1-2, pp. 1–286, November efficient collaborative perception via information filling with code-2019. 

book,” in Proceedings of the IEEE/CVF Conference on Computer

\[154\] P. Whittle, “Restless bandits: Activity allocation in a changing world,” 

Vision and Pattern Recognition \(CVPR\), 2024. 

Journal of applied probability, vol. 25, no. A, pp. 287–298, July 1988. 

\[136\] S. Liu, Z. Ding, J. Fu, H. Li, S. Chen, S. Zhang, and X. Zhou, “V2x-pc:

\[155\] Z. Ma, Y. Luo, and J. Pan, “Learning selective communication for Vehicle-to-everything collaborative perception via point cluster,” 2024, multi-agent path finding,” IEEE Robotics and Automation Letters, arXiv:2403.16635. 

vol. 7, no. 2, pp. 1455–1462, April 2021. 

\[137\] Z. Bai, G. Wu, M. J. Barth, H. Qiu, Y. Liu, E. A. Sisbot, and K. Oguchi, 

\[156\] H. Xu and X. Liu, “Perception synergy optimization with deep rein-

“Pillar attention encoder for adaptive cooperative perception,” IEEE

forcement learning for cooperative perception in C-V2V scenarios,” 

Internet of Things Journal, vol. 11, no. 14, pp. 24 998–25 009, July Vehicular Communications, vol. 38, p. 100536, December 2022. 

## 2024. 

\[157\] M. K. Abdel-Aziz, C. Perfecto, S. Samarakoon, M. Bennis, and

\[138\] S. Huang, J. Zhang, Y. Li, and C. Feng, “Actformer: Scalable col-W. Saad, “Vehicular cooperative perception through action branching laborative perception via active queries,” in Proceedings of the IEEE

and federated reinforcement learning,” IEEE Transactions on Commu-International Conference on Robotics and Automation \(ICRA\), 2024, nications, vol. 70, no. 2, pp. 891–903, February 2022. 

pp. 14 716–14 723. 

\[139\] Y. Hu, S. Fang, Z. Lei, Y. Zhong, and S. Chen, “Where2comm:

\[158\] Y. Fu, C. Li, F. R. Yu, T. H. Luan, and Y. Zhang, “A selective Communication-efficient collaborative perception via spatial confi-federated reinforcement learning strategy for autonomous driving,” 

dence maps,” in Proceedings of the Advances in Neural Information IEEE Transactions on Intelligent Transportation Systems, vol. 24, no. 2, Processing Systems \(NeurIPS\), vol. 35, New Orleans, Louisiana, United pp. 1655–1668, February 2023. 

States, 2022, pp. 4874–4886. 

\[159\] M. Sensoy, L. Kaplan, and M. Kandemir, “Evidential deep learning

\[140\] T.-H. Wang, S. Manivasagam, M. Liang, B. Yang, W. Zeng, and to quantify classification uncertainty,” in Proceedings of the Advances R. Urtasun, “V2VNet: Vehicle-to-vehicle communication for joint in neural information processing systems \(NeurIPS\), vol. 31, Montral perception and prediction,” in Proceedings of the European Conference Canada, 2018, pp. 3183–3193. 

on Computer Vision \(ECCV\), Glasgow, UK, 2020, pp. 605–621. 

\[160\] J. Ballé, D. Minnen, S. Singh, S. J. Hwang, and N. Johnston, “Vari-

\[141\] F. Chi, Y. Wang, M. T. Pourazad, P. Nasiopoulos, and V. C. Leung, ational image compression with a scale hyperprior,” arXiv preprint

“Multimodal cooperative 3d object detection over connected vehicles arXiv:1802.01436, 2018. 

for autonomous driving,” IEEE Network, vol. 37, no. 4, pp. 265–272, 

\[161\] J. Masci, U. Meier, D. Cires¸an, and J. Schmidhuber, “Stacked con-JulyAugust 2023. 

volutional auto-encoders for hierarchical feature extraction,” in 21st

\[142\] J. Zhang, K. Yang, H. Wang, P. Sun, and L. Song, “Efficient vehicular International Conference on Artificial Neural Networks. 

Espoo, 

collaborative perception based on saptial-temporal feature compres-Finland: Springer, 2011, pp. 52–59. 

34

\[162\] H. Zhao, L. Jiang, J. Jia, P. H. Torr, and V. Koltun, “Point transformer,” 

tions on Intelligent Transportation Systems, vol. 21, no. 1, pp. 233–247, in Proceedings of the IEEE/CVF international conference on computer 2020. 

vision \(ICCV\), 2021, pp. 16 259–16 268. 

\[183\] W. Yang et al., “Cellular-v2x qos adaptive distributed congestion

\[163\] J. Hu, L. Shen, and G. Sun, “Squeeze-and-excitation networks,” in control: A deep q network approach,” in 2023 IEEE 20th Consumer Proceedings of the IEEE Conference on computer vision and pattern Communications & Networking Conference \(CCNC\), Las Vegas, NV, recognition \(CVPR\), Salt Lake City, UT, USA, 2018, pp. 7132–7141. 

USA, 2023, pp. 967–968. 

\[164\] H. Xiang, R. Xu, and J. Ma, “HM-ViT: Hetero-modal vehicle-to-

\[184\] S. Hussein et al., “Vanet clock synchronization for resilient dsrc safety vehicle cooperative perception with vision transformer,” in Proceedings applications,” in 2017 Resilience Week \(RWS\), Wilmington, DE, USA, of the IEEE/CVF International Conference on Computer Vision \(ICCV\), 2017, pp. 57–63. 

Paris, France, 2023, pp. 284–295. 

\[185\] Y. J. Kim et al., “Synchronization signal design for millimeter-wave

\[165\] E. R. Magsino and I. W.-H. Ho, “An enhanced information sharing cellular V2X communications,” IEEE Communications Letters, vol. 25, roadside unit allocation scheme for vehicular networks,” IEEE Transac-no. 2, pp. 603–607, 2021. 

tions on Intelligent Transportation Systems, vol. 23, no. 9, pp. 15 462–

\[186\] C. Allig and G. Wanielik, “Alignment of perception information for 15 475, 2022. 

cooperative perception,” in Proceedings of the IEEE Intelligent Vehicles

\[166\] S. Ding, K. Muthuswamy, E. van Vulpen, and A. Desai, “A comparative Symposium \(IV\), Paris, France, 2019, pp. 1849–1854. 

assessment of C-ITS technologies,” iMOVE CRC, Technical Report, 

\[187\] H. Su, S. Arakawa, and M. Murata, “3D multi-object tracking based 2024. 

on two-stage data association for collaborative perception scenarios,” 

\[167\] IEEE Standard for Information technology– Local and metropolitan in Proceedings of the IEEE Intelligent Vehicles Symposium \(IV\), area networks– Specific requirements– Part 11: Wireless LAN Medium Anchorage, AK, USA, 2023, pp. 1–7. 

Access Control \(MAC\) and Physical Layer \(PHY\) Specifications

\[188\] Y. Yuan and M. Sester, “Leveraging dynamic objects for relative Amendment 6: Wireless Access in Vehicular Environments, IEEE Std localization correction in a connected autonomous vehicle network,” 

802.11p-2010 \(Amendment to IEEE Std 802.11-2007 as amended by in Proceedings of the ISPRS Annals of the Photogrammetry, Remote IEEE Std 802.11k-2008, IEEE Std 802.11r-2008, IEEE Std 802.11y-Sensing and Spatial Information Sciences, vol. 1, Nice, France, 2022, 2008, IEEE Std 802.11n-2009, and IEEE Std 802.11w-2009\), IEEE

pp. 101–109. 

Std., July 2010. 

\[189\] N. Vadivelu, M. Ren, J. Tu, J. Wang, and R. Urtasun, “Learning to

\[168\] H. Zhou, W. Xu, J. Chen, and W. Wang, “Evolutionary V2X technolo-communicate and correct pose errors,” in Proceedings of the Confer-gies toward the internet of vehicles: Challenges and opportunities,” 

ence on Robot Learning \(CoRL\), vol. 155, Cambridge MA, USA, 2021, Proceedings of the IEEE, vol. 108, no. 2, pp. 308–323, 2020. 

pp. 1195–1210. 

\[169\] “3gpp tr21.914, release 14,” 3rd Generation Partnership Project

\[190\] Y. Lu, Q. Li, B. Liu, M. Dianat, C. Feng, S. Chen, and Y. Wang, \(3GPP\), 

Tech. 

Rep., 

2018, 

available:

https://www.3gpp.org/

“Robust collaborative 3D object detection in presence of pose errors,” 

specifications-technologies/releases/release-14. 

in Proceedings of the IEEE International Conference on Robotics and Automation \(ICRA\), London, United Kingdom, 2023, pp. 4812–4818. 

\[170\] “3gpp tr21.915, release 15,” 3rd Generation Partnership Project

\[191\] Z. Huang, S. Wang, Y. Wang, W. Li, D. Li, and L. Wang, “Roco: \(3GPP\), 

Tech. 

Rep., 

2019, 

available:

https://www.3gpp.org/

Robust collaborative perception by iterative object matching and pose

specifications-technologies/releases/release-15. 

adjustment,” in Proceedings of the ACM International Multimedia

\[171\] “3gpp tr21.916, release 16,” 3rd Generation Partnership Project Conference \(MM\), 2024, arXiv:2408.00257. 

\(3GPP\), 

Tech. 

Rep., 

2022, 

available:

https://www.3gpp.org/

\[192\] Z. Song, F. Wen, H. Zhang, and J. Li, “A cooperative perception

specifications-technologies/releases/release-16. 

system robust to localization errors,” in 2023 IEEE Intelligent Vehicles

\[172\] X. Wu et al., “Vehicular communications using DSRC: Challenges, Symposium \(IV\), Anchorage, AK, USA, 2023, pp. 1–6. 

enhancements, and evolution,” IEEE Journal on Selected Areas in

\[193\] Z. Ni, Z. Lei, Y. Lu, D. Wang, C. Feng, Y. Wang, and S. Chen, “Self-Communications, vol. 31, no. 9, pp. 399–408, 2013. 

localized collaborative perception,” arXiv preprint arXiv:2406.12712, 

\[173\] Federal

Communications

Commission, 

“FCC

Modernizes

5.9

## 2024. 

GHz Band to Improve Wi-Fi and Automotive Safety,” Federal

\[194\] K. Jiang, Y. Shi, B. Wijaya, M. Yang, T. Wen, Z. Xiao, and D. Yang, Communications

Commission, 

November

2020, 

retrieved

1

“Map container: A map-based framework for cooperative perception,” 

November 2024. \[Online\]. Available: https://www.fcc.gov/document/

2022, arXiv:2208.13226. 

fcc-modernizes-59-ghz-band-improve-wi-fi-and-automotive-safety

\[195\] Z. Lei, Z. Ni, R. Han, S. Tang, C. Feng, S. Chen, and Y. Wang, 

\[174\] “C-V2X technical performance,” Qualcomm Technologies, Inc., Tech-

“Robust collaborative perception without external localization and nical Report, October 2019. 

clock devices,” in Proceedings of the IEEE International Conference

\[175\] M. Sepulcre, M. Gonzalez-Martn, J. Gozalvez, R. Molina-Masegosa, on Robotics and Automation \(ICRA\), 2024, pp. 7280–7286. 

and B. Coll-Perales, “Analytical models of the performance of ieee

\[196\] K. Yang, D. Yang, J. Zhang, M. Li, Y. Liu, J. Liu, H. Wang, P. Sun, 802.11p vehicle to vehicle communications,” IEEE Transactions on and L. Song, “Spatio-temporal domain awareness for multi-agent col-Vehicular Technology, vol. 71, no. 1, pp. 713–724, 2022. 

laborative perception,” in Proceedings of the IEEE/CVF International

\[176\] Q.-S. Dong, S.-Y. Zhang, B. Shahrrava, and H. Zheng, “An enhanced Conference on Computer Vision \(ICCV\), Paris, France, October 2023, channel estimation scheme in OFDM-IM systems with index pilots pp. 23 383–23 392. 

for IEEE 802.11p standard,” IEEE Access, vol. 12, pp. 74 389–74 405, 

\[197\] Z. Song, T. Xie, H. Zhang, J. Liu, F. Wen, and J. Li, “A spatial 2024. 

calibration method for robust cooperative perception,” IEEE Robotics

\[177\] S. A. U. Haq, V. Singh, B. T. Tanaji, and S. Darak, “Low complexity and Automation Letters, vol. 9, no. 5, pp. 4011–4018, 2024. 

high speed deep neural network augmented wireless channel estima-

\[198\] Y. Zha, W. ShangGuan, and L. Chai, “V2v based visual cooperative tion,” in 2024 37th International Conference on VLSI Design and perception for connected autonomous vehicles: Far-sight and see-2024 23rd International Conference on Embedded Systems \(VLSID\), through,” in Proceedings of the IEEE Intelligent Vehicles Symposium Kolkata, India, 2024, pp. 235–240. 

\(IV\), 2024, pp. 2784–2790. 

\[178\] M. Ali, H. Hwang, and Y.-T. Kim, “Performance enhancement of C-

\[199\] P. Gao, Q. Zhu, H. Lu, C. Gan, and H. Zhang, “Deep masked graph V2X mode 4 with balanced resource allocation,” in ICC 2022 - IEEE

matching for correspondence identification in collaborative perception,” 

International Conference on Communications, Seoul, Korea, 2022, pp. 

in Proceedings of the IEEE International Conference on Robotics and 2750–2755. 

Automation \(ICRA\), London, United Kingdom, 2023, pp. 6117–6123. 

\[179\] Y. Yoon and H. Kim, “Balancing power and rate control for improved

\[200\] M. A. Fischler and R. C. Bolles, “Random sample consensus: a congestion control in cellular v2x communication environments,” IEEE

paradigm for model fitting with applications to image analysis and Access, vol. 8, pp. 105 071–105 081, 2020. 

automated cartography,” Communications of the ACM, vol. 24, no. 6, 

\[180\] R. Molina-Masegosa and J. Gozalvez, “Lte-v for sidelink 5g v2x ve-pp. 381–395, June 1981. 

hicular communications: A new 5g technology for short-range vehicle-

\[201\] P. Besl and N. D. McKay, “A method for registration of 3-D shapes,” 

to-everything communications,” IEEE Vehicular Technology Magazine, IEEE Transactions on Pattern Analysis and Machine Intelligence, vol. 12, no. 4, pp. 30–39, 2017. 

vol. 14, no. 02, pp. 239–256, February 1992. 

\[181\] J. Zheng, B. Wang, and C. Li, “A c-v2x mode 4 and 802.11p-based

\[202\] C. Villani et al., Optimal transport: old and new. Springer, 2009, vol. 

resource selection scheme for intraplatoon message delivery,” IEEE

## 338. 

Internet of Things Journal, vol. 11, no. 20, pp. 33 537–33 549, 2024. 

\[203\] Q. Chen, X. Ma, S. Tang, J. Guo, Q. Yang, and S. Fu, “F-Cooper:

\[182\] S. Khlmorgen et al., “Evaluation of congestion-enabled forwarding Feature based cooperative perception for autonomous vehicle edge with mixed data traffic in vehicular communications,” IEEE Transac-computing system using 3D point clouds,” in Proceedings of the 4th

35

ACM/IEEE Symposium on Edge Computing, Washington DC, USA, 

\[222\] P. Liu, Z. Wang, G. Yu, B. Zhou, and P. Chen, “Region-based hybrid 2019, pp. 88–100. 

collaborative perception for connected autonomous vehicles,” IEEE

\[204\] Z. Bai, G. Wu, M. J. Barth, Y. Liu, E. A. Sisbot, and K. Oguchi, Transactions on Vehicular Technology, pp. 1–10, 2023. 

“PillarGrid: Deep learning-based cooperative perception for 3D object

\[223\] M. Schlichtkrull, T. N. Kipf, P. Bloem, R. Van Den Berg, I. Titov, detection from onboard-roadside LiDAR,” in Proceedings of the IEEE

and M. Welling, “Modeling relational data with graph convolutional International Conference on Intelligent Transportation Systems \(ITSC\), networks,” in Proceedings of the European Semantic Web Conference Macau, China, 2022, pp. 1743–1749. 

\(ESWC 2018\), Heraklion, Crete, Greece, 2018, pp. 593–607. 

\[205\] Y. Hu, Y. Lu, R. Xu, W. Xie, S. Chen, and Y. Wang, “Collaboration

\[224\] N. Carion, F. Massa, G. Synnaeve, N. Usunier, A. Kirillov, and helps camera overtake LiDAR in 3D detection,” in Proceedings of the S. Zagoruyko, “End-to-end object detection with transformers,” in IEEE/CVF Conference on Computer Vision and Pattern Recognition European Conference on Computer Vision \(ECCV\). 

Springer, 2020, 

\(CVPR\), Vancouver, Canada, 2023, pp. 9243–9252. 

pp. 213–229. 

\[206\] D. Qu, Q. Chen, T. Bai, A. Qin, H. Lu, H. Fan, S. Fu, and Q. Yang, 

\[225\] R. Xu, W. Chen, H. Xiang, L. Liu, and J. Ma, “Model-agnostic multi-

“SiCP: Simultaneous individual and cooperative perception for 3D

agent perception framework,” in Proceedings of the IEEE International object detection in connected and automated vehicles,” in Proceedings Conference on Robotics and Automation \(ICRA\), London, UK, 2023, of the IEEE/RSJ International Conference on Intelligent Robots and pp. 1471–1478. 

Systems \(IROS\), 2024, arXiv:2312.04822. 

\[226\] C. Allig and G. Wanielik, “Unequal dimension track-to-track fusion

\[207\] D. Qiao and F. Zulkernine, “CoBEVFusion: Cooperative percep-approaches using covariance intersection,” IEEE Transactions on In-tion with LiDAR-camera bird’s-eye view fusion,” arXiv preprint telligent Transportation Systems, vol. 23, no. 6, pp. 5881–5886, June arXiv:2310.06008, 2023. 

## 2022. 

\[208\] C. Zhang, B. Tian, S. Meng, S. Qi, Y. Sun, Y. Ai, and L. Chen, 

\[227\] R. Xu, J. Li, X. Dong, H. Yu, and J. Ma, “Bridging the domain gap

“V2x-bgn: Camera-based v2x-collaborative 3d object detection with for multi-agent perception,” in Proceedings of the IEEE International bev global non-maximum suppression,” in Proceedings of the IEEE

Conference on Robotics and Automation \(ICRA\), London, UK, 2023, Intelligent Vehicles Symposium \(IV\), 2024, pp. 602–607. 

pp. 6035–6042. 

\[209\] N. Mouawad and V. Mannoni, “Collective perception messages: New

\[228\] Y. Ma, J. Lu, C. Cui, S. Zhao, X. Cao, W. Ye, and Z. Wang, “MACP: low complexity fusion and V2X connectivity analysis,” in Proceedings Efficient model adaptation for cooperative perception,” in Proceedings of the IEEE Vehicular Technology Conference \(VTC\), Norman, OK, of the IEEE/CVF Winter Conference on Applications of Computer USA, 2021, pp. 1–5. 

Vision \(WACV\), Waikoloa, Hawaii, 2024, pp. 3373–3382. 

\[229\] X. Li, J. Yin, W. Li, C. Xu, R. Yang, and J. Shen, “Di-v2x: Learning

\[210\] M. Shan, K. Narula, S. Worrall, Y. F. Wong, J. Stephany Berrio Perez, domain-invariant representation for vehicle-infrastructure collaborative P. Gray, and E. Nebot, “A novel probabilistic V2X data fusion 3d object detection,” in Proceedings of the AAAI Conference on framework for cooperative perception,” in Proceedings of the IEEE

Artificial Intelligence, vol. 38, no. 4, 2024, pp. 3208–3215. 

International Conference on Intelligent Transportation Systems \(ITSC\), Macau, China, 2022, pp. 2013–2020. 

\[230\] S. Hu, Z. Fang, X. Chen, Y. Fang, and S. Kwong, “Towards full-scene domain generalization in multi-agent collaborative bird’s eye

\[211\] S. Teufel, J. Gamerdinger, G. Volk, and O. Bringmann, “Collective view segmentation for connected and autonomous driving,” 2023, PV-RCNN: A novel fusion technique using collective detections for arXiv:2311.16754. 

enhanced local LiDAR-based perception,” in Proceedings of the IEEE

\[231\] Z. Bai, G. Wu, M. J. Barth, Y. Liu, E. A. Sisbot, and K. Oguchi, International Conference on Intelligent Transportation Systems \(ITSC\), 

“VINet: Lightweight, scalable, and heterogeneous cooperative per-2023. 

ception for 3D object detection,” Mechanical Systems and Signal

\[212\] Z. Meng, X. Xia, R. Xu, W. Liu, and J. Ma, “HYDRO-3D: Hybrid Processing, vol. 204, p. 110723, December 2023. 

object detection and tracking for cooperative perception using 3D

\[232\] H. Bae, M. Kang, and H. Ahn, “V2x-m2c: Efficient multi-module col-LiDAR,” IEEE Transactions on Intelligent Vehicles, vol. 8, no. 8, pp. 

laborative perception with two connections,” 2024, arXiv:2407.11546. 

4069–4080, August 2023. 

\[233\] Z. Wang, S. Fan, X. Huo, T. Xu, Y. Wang, J. Liu, Y. Chen, and Y.-Q. 

\[213\] A. N. Ahmed, S. Mercelis, and A. Anwar, “Graph attention based Zhang, “VIMI: Vehicle-infrastructure multi-view intermediate fusion feature fusion for collaborative perception,” in Proceedings of the IEEE

for camera-based 3D object detection,” 2023, arXiv:2303.10975. 

Intelligent Vehicles Symposium \(IV\), 2024, pp. 2317–2324. 

\[234\] Y. Lu, Y. Hu, Y. Zhong, D. Wang, Y. Wang, and S. Chen, “An extensible

\[214\] R. Xu, Z. Tu, H. Xiang, W. Shao, B. Zhou, and J. Ma, “CoBEVT: framework for open heterogeneous collaborative perception,” in The Cooperative bird’s eye view semantic segmentation with sparse trans-12th International Conference on Learning Representations, 2024. 

formers,” in Proceedings of the Conference on Robot Learning \(CoRL\), 

\[Online\]. Available: https://openreview.net/forum?id=KkrDUGIASk

Auckland, NZ, 2023, pp. 989–1000. 

\[235\] J. Li, R. Xu, X. Liu, J. Ma, Z. Chi, J. Ma, and H. Yu, “Learning for

\[215\] S. Fan, H. Yu, W. Yang, J. Yuan, and Z. Nie, “QUEST: Query stream vehicle-to-vehicle cooperative perception under lossy communication,” 

for practical cooperative perception,” in Proceedings of the IEEE

IEEE Transactions on Intelligent Vehicles, vol. 8, no. 4, pp. 2650–2660, International Conference on Robotics and Automation \(ICRA\), 2024, April 2023. 

pp. 18 436–18 442. 

\[236\] S. Ren, Z. Lei, Z. Wang, M. Dianati, Y. Wang, S. Chen, and W. Zhang, 

\[216\] C. Lin, D. Tian, X. Duan, J. Zhou, D. Zhao, and D. Cao, “V2VFormer:

“Interruption-aware cooperative perception for V2X communication-Vehicle-to-vehicle cooperative perception with spatial-channel trans-aided autonomous driving,” IEEE Transactions on Intelligent Vehicles, former,” IEEE Transactions on Intelligent Vehicles, vol. 9, no. 2, pp. 

vol. 9, no. 4, pp. 4698–4714, April 2024. 

3384–3395, 2024. 

\[237\] C. Liu, J. Chen, Y. Chen, R. Payton, M. Riley, and S.-H. Yang, 

\[217\] H. Yin, D. Tian, C. Lin, X. Duan, J. Zhou, D. Zhao, and D. Cao, 

“Self-supervised adaptive weighting for cooperative perception in v2v

“V2VFormer \+\+ : Multi-modal vehicle-to-vehicle cooperative per-communications,” IEEE Transactions on Intelligent Vehicles, vol. 9, ception via global-local transformer,” IEEE Transactions on Intelligent no. 2, pp. 3569–3580, 2024. 

Transportation Systems, vol. 25, no. 2, pp. 2153–2166, 2024. 

\[238\] D. Rößle, J. Gerner, K. Bogenberger, D. Cremers, S. Schmidtner, 

\[218\] Z. Li, H. Liang, H. Wang, M. Zhao, J. Wang, and X. Zheng, “MKD-and T. Schön, “Unlocking past information: Temporal embeddings in Cooper: Cooperative 3D object detection for autonomous driving via cooperative bird’s eye view prediction,” in Proceedings of the IEEE

multi-teacher knowledge distillation,” IEEE Transactions on Intelligent Intelligent Vehicles Symposium \(IV\), 2024, pp. 2220–2225. 

Vehicles, vol. 9, no. 1, pp. 1490–1500, 2024. 

\[239\] Z. Zheng, X. Xia, L. Gao, H. Xiang, and J. Ma, “Cooperfuse: A real-

\[219\] C. He, H. Wang, L. Chen, T. Luo, and Y. Cai, “V2X-AHD: Vehicle-time cooperative perception fusion framework,” in Proceedings of the to-everything cooperation perception via asymmetric heterogenous IEEE Intelligent Vehicles Symposium \(IV\), 2024, pp. 533–538. 

distillation network,” arXiv preprint arXiv:2310.06603, 2023. 

\[240\] H. Yu, Y. Tang, E. Xie, J. Mao, P. Luo, and Z. Nie, “Flow-based feature

\[220\] E. Arnold, M. Dianati, R. de Temple, and S. Fallah, “Cooperative fusion for vehicle-infrastructure cooperative 3d object detection,” in perception for 3D object detection in driving scenarios using infrastruc-Proceedings of the Conference on Advances in Neural Information ture sensors,” IEEE Transactions on Intelligent Transportation Systems, Processing Systems \(NeurIPS\), 2023. 

vol. 23, no. 3, pp. 1852–1864, March 2022. 

\[241\] Z. Lei, S. Ren, Y. Hu, W. Zhang, and S. Chen, “Latency-aware

\[221\] Q. Xie, X. Zhou, T. Qiu, Q. Zhang, and W. Qu, “Soft actorcritic-based collaborative perception,” in Proceedings of the European Conference multilevel cooperative perception for connected autonomous vehicles,” 

on Computer Vision \(ECCV\), Glasgow, UK, 2022, pp. 316–332. 

IEEE Internet of Things Journal, vol. 9, no. 21, pp. 21 370–21 381, 

\[242\] S. Wei, Y. Wei, Y. Hu, Y. Lu, Y. Zhong, S. Chen, and Y. Zhang, November 2022. 

“Asynchrony-robust collaborative perception via bird’s eye view flow,” 

36

in Proceedings of the Conference on Advances in Neural Information

\[262\] B. Wang, L. Zhang, Z. Wang, Y. Zhao, and T. Zhou, “CORE: Processing Systems \(NeurIPs\), Louisiana, USA, 2023. 

Cooperative reconstruction for multi-agent perception,” in Proceedings

\[243\] X. He, Y. Li, T. Cui, M. Wang, T. Liu, and Y. Yue, “Robust of the IEEE/CVF international conference on computer vision \(ICCV\), collaborative perception against temporal information disturbance,” in Paris, France, 2023, pp. 8710–8720. 

Proceedings of the IEEE International Conference on Robotics and

\[263\] J. Li, R. Xu, X. Liu, B. Li, Q. Zou, J. Ma, and H. Yu, “S2R-ViT for Automation \(ICRA\), 2024, pp. 16 207–16 213. 

multi-agent cooperative perception: Bridging the gap from simulation

\[244\] J. Tu, T. Wang, J. Wang, S. Manivasagam, M. Ren, and R. Urtasun, to reality,” in Proceedings of the IEEE International Conference on

“Adversarial attacks on multi-agent communication,” in Proceedings of Robotics and Automation \(ICRA\), 2024, pp. 16 374–16 380. 

the IEEE/CVF International Conference on Computer Vision, Montreal, 

\[264\] X. Kong, W. Jiang, J. Jia, Y. Shi, R. Xu, and S. Liu, “DUSA: QC, Canada, 2021, pp. 7768–7777. 

Decoupled unsupervised sim2real adaptation for vehicle-to-everything

\[245\] Y. Li, Q. Fang, J. Bai, S. Chen, F. Juefei-Xu, and C. Feng, “Among collaborative perception,” in Proceedings of the 31st ACM International us: Adversarially robust collaborative perception by consensus,” in Conference on Multimedia \(MM\), Ottawa, Canada, 2023, pp. 1943–

Proceedings of the IEEE/CVF International Conference on Computer 1954. 

Vision, Paris, France, 2023, pp. 186–195. 

\[265\] T. Haarnoja, A. Zhou, P. Abbeel, and S. Levine, “Soft actor-critic: Off-

\[246\] C. Allig, T. Leinmüller, P. Mittal, and G. Wanielik, “Trustworthiness policy maximum entropy deep reinforcement learning with a stochastic estimation of entities within collective perception,” in Proceedings actor,” in Proceedings of the 35th International Conference on Machine of the IEEE Vehicular Networking Conference \(VNC\), Los Angeles, Learning \(ICML\), vol. 80, Stockholm, Sweden, 2018, pp. 1861–1870. 

California, 2019, pp. 1–8. 

\[266\] N. Houlsby, A. Giurgiu, S. Jastrzebski, B. Morrone, Q. De Laroussilhe, 

\[247\] H. Zhang, Z. Li, S. Cheng, and A. Clark, “Cooperative perception for A. Gesmundo, M. Attariyan, and S. Gelly, “Parameter-efficient transfer safe control of autonomous vehicles under LiDAR spoofing attacks,” 

learning for nlp,” in Proceedings of the 36th International conference 2023, arXiv:2302.07341. 

on machine learning. 

Long Beach, CA, USA: PMLR, 2019, pp. 

\[248\] Q. Zhang, S. Jin, R. Zhu, J. Sun, X. Zhang, Q. A. Chen, and Z. M. Mao, 2790–2799. 

“On data fabrication in collaborative vehicular perception: Attacks

\[267\] Y. Zhao and S.-G. Haggman, “Intercarrier interference self-cancellation and countermeasures,” in Proceedings of the 33rd USENIX Security scheme for OFDM mobile communication systems,” IEEE Transac-Symposium \(USENIX Security 24\), 2024, pp. 6309–6326. 

tions on Communnication, vol. 49, no. 7, pp. 1185–1191, July 2001. 

\[249\] Y. Zhao, Z. Xiang, S. Yin, X. Pang, S. Chen, and Y. Wang, “Malicious

\[268\] D. Patra, S. Chavhan, D. Gupta, A. Khanna, and J. J. Rodrigues, “V2X

agent detection for robust multi-agent collaborative perception,” in communication based dynamic topology control in VANETs,” in Ad-Proceedings of the IEEE/RSJ International Conference on Intelligent junct Proceedings of the 2021 International Conference on Distributed Robots and Systems \(IROS\), 2024, arXiv:2310.11901. 

Computing and Networking \(ICDCN\), New York, NY, USA, 2021, pp. 

\[250\] X. Tang, J. Zhang, Y. Fu, C. Li, N. Cheng, and X. Yuan, “A fair 62–68. 

and efficient federated learning algorithm for autonomous driving,” 

\[269\] Y. Yan, H. Du, Q.-L. Han, and W. Li, “Discrete multi-objective in Proceedings of the IEEE 98th Vehicular Technology Conference switching topology sliding mode control of connected autonomous \(VTC2023-Fall\), Hong Kong, 2023, pp. 1–5. 

vehicles with packet loss,” IEEE Transactions on Intelligent Vehicles, 

\[251\] R. Song, R. Xu, A. Festag, J. Ma, and A. Knoll, “Fedbevt: Federated vol. 8, no. 4, pp. 2926–2938, April 2023. 

learning bird’s eye view perception transformer in road traffic systems,” 

\[270\] P. Kyosti et al., “Winner ii channel models,” IST, Tech. Rep. 

IEEE Transactions on Intelligent Vehicles, vol. 9, no. 1, pp. 958–969, IST-4-027756 WINNER II D1.1.2 V1.2, 2007. \[Online\]. Available: 2024. 

https://cir.nii.ac.jp/crid/1571698600936523008

\[252\] R. Song, L. Lyu, W. Jiang, A. Festag, and A. Knoll, “V2X-Boosted

\[271\] Y. Zhu, C. Zhao, and Y. Du, “Latency impact analysis of point federated learning for cooperative intelligent transportation systems cloud fusion modes for cooperative perception in autonomous driving,” 

with contextual client selection,” 2023, arXiv:2305.11654. 

in Proceedings of the IEEE International Conference on Intelligent

\[253\] Z. Zhang, J. Liu, X. Zhou, T. Huang, Q.-L. Han, J. Liu, and H. Liu, Transportation Systems \(ITSC\), Macau, China, 2022, pp. 1024–1029. 

“On the federated learning framework for cooperative perception,” 

\[272\] M. Tsukada, S. Arii, H. Ochiai, and H. Esaki, “Misbehavior detection IEEE Robotics and Automation Letters, vol. 9, no. 11, pp. 9423–9430, using collective perception under privacy considerations,” in Proceed-November 2024. 

ings of the IEEE Annual Consumer Communications & Networking

\[254\] A. Piazzoni, J. Cherian, R. Vijay, L.-P. Chau, and J. Dauwels, “CoPEM: Conference \(CCNC\), Las Vegas, NV, USA, 2022, pp. 808–814. 

Cooperative perception error models for autonomous driving,” in

\[273\] Y. Tao, Y. Jiang, P. Lin, M. Tsukada, and H. Esaki, “zk-PoT: Zero-Proceedings of the IEEE International Conference on Intelligent Trans-knowledge proof of traffic for privacy enabled cooperative perception,” 

portation Systems \(ITSC\), Macau, China, 2022, pp. 3934–3939. 

in Proceedings of the IEEE Annual Consumer Communications & 

\[255\] K. Cai, T. Qu, B. Gao, and H. Chen, “Consensus-based distributed Networking Conference \(CCNC\), Las Vegas, NV, USA, 2023, pp. 261–

cooperative perception for connected and automated vehicles,” IEEE

## 268. 

Transactions on Intelligent Transportation Systems, vol. 24, no. 8, pp. 

\[274\] J. Zhang and C. Li, “Adversarial examples: Opportunities and chal-8188–8208, August 2023. 

lenges,” IEEE Transactions on Neural Networks and Learning Systems, 

\[256\] Z. Wu, Y. Wang, H. Ma, Z. Li, H. Qiu, and J. Li, “Cmp: Co-vol. 31, no. 7, pp. 2578–2593, July 2019. 

operative motion prediction with multi-agent communication,” 2024, 

\[275\] Y. Benjamini and Y. Hochberg, “Controlling the false discovery rate: arXiv:2403.17916. 

a practical and powerful approach to multiple testing,” Journal of the

\[257\] S. Su, Y. Li, S. He, S. Han, C. Feng, C. Ding, and F. Miao, Royal statistical society: series B \(Methodological\), vol. 57, no. 1, pp. 

“Uncertainty quantification of collaborative detection for self-driving,” 

289–300, 1995. 

in Proceedings of the IEEE International Conference on Robotics and

\[276\] S. Wang, C. Li, D. W. K. Ng, Y. C. Eldar, H. V. Poor, Q. Hao, and Automation \(ICRA\), London, UK, 2023, pp. 5588–5594. 

C. Xu, “Federated deep learning meets autonomous vehicle perception:

\[258\] S. Su, S. Han, Y. Li, Z. Zhang, C. Feng, C. Ding, and F. Miao, “Collab-Design and verification,” IEEE Network, vol. 37, no. 3, pp. 16–25, June orative multi-object tracking with conformal uncertainty propagation,” 

## 2023. 

IEEE Robotics and Automation Letters, vol. 9, no. 4, pp. 3323–3330, 

\[277\] F. Chi, Y. Wang, P. Nasiopoulos, and V. C. Leung, “Federated coop-2024. 

erative 3d object detection for autonomous driving,” in Proceedings of

\[259\] H.-k. Chiu, C.-Y. Wang, M.-H. Chen, and S. F. Smith, “Proba-the IEEE 33rd International Workshop on Machine Learning for Signal bilistic 3d multi-object cooperative tracking for autonomous driving Processing \(MLSP\), Rome, Italy, 2023, pp. 1–6. 

via differentiable multi-sensor kalman filter,” in Proceedings of the

\[278\] V. P. Chellapandi, L. Yuan, C. G. Brinton, S. H. ak, and Z. Wang, IEEE International Conference on Robotics and Automation \(ICRA\), 

“Federated learning for connected and automated vehicles: A survey of Yokohama, Japan, 2024, pp. 18 458–18 464. 

existing approaches and challenges,” IEEE Transactions on Intelligent

\[260\] H. Su, S. Arakawa, and M. Murata, “Cooperative 3D multi-object Vehicles, vol. 9, no. 1, pp. 119–137, January 2024. 

tracking for connected and automated vehicles with complementary

\[279\] B. S. Chawky, M. S. Hefeida, and A. Noureldin, “Evaluation of data association,” in Proceedings of the IEEE Intelligent Vehicles sensors impact on information redundancy in cooperative perception Symposium \(IV\), 2024, pp. 285–291. 

system,” in Proceedings of the IEEE Global Communications Confer-

\[261\] Y. Li, J. Zhang, D. Ma, Y. Wang, and C. Feng, “Multi-robot scene ence \(GLOBECOM\), Rio de Janeiro, Brazil, 2022, pp. 2739–2744. 

completion: Towards task-agnostic collaborative perception,” in Pro-

\[280\] A. Piazzoni, J. Cherian, M. Slavik, and J. Dauwels, “Modeling per-ceedings of The 6th Conference on Robot Learning, vol. 205, Auckland, ception errors towards robust decision making in autonomous vehi-NZ, 2022, pp. 2062–2072. 

cles,” in Proceedings of the Twenty-Ninth International Conference on

37

International Joint Conferences on Artificial Intelligence, Yokohama Conference on Computer Vision and Pattern Recognition \(CVPR\), Yokohama, Japan, 2021, pp. 3494–3500. 

## 2024. 

\[281\] B. Jia, M. Xin, and Y. Cheng, “High-degree cubature Kalman filter,” 

\[299\] X. Zhang, Y. Li, J. Wang, X. Qin, Y. Shen, Z. Fan, and X. Tan, “In-Automatica, vol. 49, no. 2, pp. 510–518, February 2013. 

scope: A new real-world 3d infrastructure-side collaborative perception

\[282\] X. Weng, J. Wang, D. Held, and K. Kitani, “3D multi-object tracking: A dataset for open traffic scenarios,” 2024, arXiv:2407.21581. 

baseline and new evaluation metrics,” in Proceedings of the IEEE/RSJ

\[300\] H. Xiang, Z. Zheng, X. Xia, R. Xu, L. Gao, Z. Zhou, X. Han, X. Ji, International Conference on Intelligent Robots and Systems \(IROS\), M. Li, Z. Meng et al., “V2X-Real: a largs-scale dataset for vehicle-to-Las Vegas, USA, 2020, pp. 10 359–10 366. 

everything cooperative perception,” 2024, arXiv:2403.16034. 

\[283\] G. P. Meyer and N. Thakurdesai, “Learning an uncertainty-aware object

\[301\] E. Arnold, S. Mozaffari, and M. Dianati, “Fast and robust registration detector for autonomous driving,” in Proceedings of the IEEE/RSJ

of partially overlapping point clouds,” IEEE Robotics and Automation International Conference on Intelligent Robots and Systems \(IROS\), Letters, vol. 7, no. 2, pp. 1502–1509, April 2022. 

Las Vegas, USA, 2020, pp. 10 521–10 527. 

\[302\] R. Xu, H. Xiang, X. Xia, X. Han, J. Li, and J. Ma, “OPV2V: An open

\[284\] A. N. Angelopoulos and S. Bates, “A gentle introduction to confor-benchmark dataset and fusion pipeline for perception with vehicle-mal prediction and distribution-free uncertainty quantification,” 2021, to-vehicle communication,” in Proceedings of the IEEE International arXiv:2107.07511. 

Conference on Robotics and Automation \(ICRA\), Philadelphia, PA, 

\[285\] Y. Han, H. Zhang, H. Zhang, and Y. Li, “SSC3OD: Sparsely supervised USA, 2022, pp. 2583–2589. 

collaborative 3D object detection from lidar point clouds,” in 2023

\[303\] Y. Li, D. Ma, Z. An, Z. Wang, Y. Zhong, S. Chen, and C. Feng, “V2X-IEEE International Conference on Systems, Man, and Cybernetics Sim: Multi-agent collaborative perception dataset and benchmark for \(SMC\), Honolulu, Oahu, HI, USA, 2023, pp. 1360–1367. 

autonomous driving,” IEEE Robotics and Automation Letters, vol. 7, 

\[286\] P. A. Lopez, M. Behrisch, L. Bieker-Walz, J. Erdmann, Y.-P. Flötteröd, no. 4, pp. 10 914–10 921, July 2022. 

R. Hilbrich, L. Lücken, J. Rummel, P. Wagner, and E. Wießner, 

\[304\] R. Mao, J. Guo, Y. Jia, Y. Sun, S. Zhou, and Z. Niu, “DOLPHINS:

“Microscopic traffic simulation using SUMO,” in Proceedings of the Dataset for collaborative perception enabled harmonious and intercon-International Conference on Intelligent Transportation Systems \(ITSC\), nected self-driving,” in Proceedings of Asian Conference on Computer Maui, HI, USA, 2018, pp. 2575–2582. 

Vision \(ACCV\), Macau SAR, China, 2022, pp. 4361–4377. 

\[287\] A. Dosovitskiy, G. Ros, F. Codevilla, A. Lopez, and V. Koltun, 

\[305\] T. Wang et al., “Deepaccident: A motion and accident prediction

“CARLA: An open urban driving simulator,” in Proceedings of the benchmark for V2X autonomous driving,” in Proceedings of the AAAI Conference on Robot Learning, California, USA, 2017, pp. 1–16. 

Conference on Artificial Intelligence, vol. 38, no. 6, 2024, pp. 5599–

\[288\] R. Xu, Y. Guo, X. Han, X. Xia, H. Xiang, and J. Ma, “OpenCDA: 5606. 

an open cooperative driving automation framework integrated with

\[306\] J. Gamerdinger, S. Teufel, P. Schulz, S. Amann, J.-P. Kirchner, and co-simulation,” in Proceedings of the International Conference on O. Bringmann, “Scope: A synthetic multi-modal dataset for collec-Intelligent Transportation Systems \(ITSC\), Indianapolis, IN, USA, tive perception including physical-correct weather conditions,” 2024, 2021, pp. 1155–1162. 

arXiv:2408.03065. 

\[289\] R. Xu, H. Xiang, X. Han, X. Xia, Z. Meng, C.-J. C. C.-J. Chen, , and

\[307\] Z. Zheng, X. Han, X. Xia, L. Gao, H. Xiang, and J. Ma, “OpenCDA-J. Ma, “The OpenCDA open-source ecosystem for cooperative driving ROS: Enabling seamless integration of simulation and real-world coop-automation research,” IEEE Transactions on Intelligent Vehicles, vol. 8, erative driving automation,” IEEE Transactions on Intelligent Vehicles, no. 4, pp. 2698–2711, April 2023. 

vol. 8, no. 7, pp. 3775–3780, July 2023. 

\[290\] H. Xiang, R. Xu, X. Xia, Z. Zheng, B. Zhou, and J. Ma, “V2XP-ASG:

\[308\] R. Zhang, D. Meng, S. Shen, T. Wang, T. Karir, M. Maile, and H. X. 

Generating adversarial scenes for vehicle-to-everything perception,” in Liu, “Evaluating roadside perception for autonomous vehicles: Insights Proceedings of the IEEE International Conference on Robotics and from field testing,” 2024, arXiv:2401.12392. 

Automation \(ICRA\), London, UK, 2023, pp. 3584–3591. 

\[309\] J. Parikh et al., “Vehicle-to-infrastructure program cooperative adaptive

\[291\] Z. Bai, G. Wu, X. Qi, Y. Liu, K. Oguchi, and M. J. Barth, “Cyber cruise control.” U.S. Department of Transportation, Technical Report mobility mirror for enabling cooperative driving automation in mixed FHWA-JPO-16-257, 2015. \[Online\]. Available: https://rosap.ntl.bts. 

traffic: A co-simulation platform,” IEEE Intelligent Transportation

gov/view/dot/3580

Systems Magazine, vol. 15, no. 2, pp. 251–265, March 2023. 

\[310\] The Artificial Intelligence Lab, The University of Texas, “The au-

\[292\] H. Yu et al., “DAIR-V2X: A large-scale dataset for vehicle-tonomous intersection management project,” https://www.cs.utexas. 

infrastructure cooperative 3D object detection,” in Proceedings of the

edu/∼aim/, accessed: November 1, 2024. 

IEEE/CVF Conference on Computer Vision and Pattern Recognition

\[311\] F. Seeliger et al., “Advisory warnings based on cooperative perception,” 

\(CVPR\), Louisiana, USA, 2022, pp. 21 361–21 370. 

in 2014 IEEE Intelligent Vehicles Symposium Proceedings, Dearborn, 

\[293\] H. Yu, W. Yang, H. Ruan, Z. Yang, Y. Tang, X. Gao, X. Hao, Y. Shi, MI, USA, 2014, pp. 246–252. 

Y. Pan, N. Sun, J. Song, J. Yuan, P. Luo, and Z. Nie, “V2X-Seq: A large-scale sequential dataset for vehicle-infrastructure cooperative

\[312\] G. A. C. \(DLR\), “Ko-PER–cooperative perception,” https://www. 

perception and forecasting,” in

forwiss.uni-passau.de/en/projects/67/, accessed: November 1, 2024. 

Proceedings of the IEEE/CVF Confer-

ence on Computer Vision and Pattern Recognition \(CVPR\), Vancouver, 

\[313\] E. Strigel et al., “The ko-per intersection laserscanner and video Canada, 2023, pp. 5486–5495. 

dataset,” in 17th International IEEE Conference on Intelligent Trans-

\[294\] C. Ma et al., “HoloVIC: Large-scale dataset and benchmark for multi-portation Systems \(ITSC\), Qingdao, China, 2014, pp. 1900–1901. 

sensor holographic intersection and vehicle-infrastructure cooperative,” 

\[314\] V. T. T. Institute, “Development and use of cooperative perception for in Proceedings of the IEEE/CVF Conference on Computer Vision and cavs,” https://www.vtti.vt.edu/vcc/purpose.html, accessed: November 1, Pattern Recognition, 2024, pp. 22 129–22 138. 

## 2024. 

\[295\] R. Xu, X. Xia, J. Li, H. Li, S. Zhang, Z. Tu, Z. Meng, H. Xiang, 

\[315\] M. Shan et al., “Demonstrations of cooperative perception: Safety and X. Dong, R. Song, H. Yu, B. Zhou, and J. Ma, “V2V4Real: A real-robustness in connected and automated vehicle operations,” Sensors, world large-scale dataset for vehicle-to-vehicle cooperative perception,” 

vol. 21, no. 1, p. 200, 2020. 

in Proceedings of the IEEE/CVF Conference on Computer Vision and

\[316\] C. Liu, Y. Chen, J. Chen, R. Payton, M. Riley, and S.-H. Yang, Pattern Recognition \(CVPR\), Vancouver, Canada, 2023, pp. 13 712–

“Cooperative perception with learning-based V2V communications,” 

13 722. 

IEEE Wireless Communications Letters, vol. 12, no. 11, pp. 1831–

\[296\] J. Axmann, R. Moftizadeh, J. Su, B. Tennstedt, Q. Zou, Y. Yuan, 1835, November 2023. 

D. Ernst, H. Alkhatib, C. Brenner, and S. Schön, “LUCOOP: Leibniz

\[317\] V. G. Stepanyants and A. Y. Romanov, “A survey of integrated university cooperative perception and urban navigation dataset,” in Pro-simulation environments for connected automated vehicles: Require-ceedings of the IEEE Intelligent Vehicles Symposium \(IV\), Anchorage, ments, tools, and architecture,” IEEE Intelligent Transportation Systems AK, USA, 2023, pp. 1–8. 

Magazine, vol. 16, no. 2, pp. 6–22, 2024. 

\[297\] W. Zimmer, G. A. Wardana, S. Sritharan, X. Zhou, R. Song, and

\[318\] G. Luo, C. Shao, N. Cheng, H. Zhou, H. Zhang, Q. Yuan, and A. C. Knoll, “TUMTraf V2X cooperative perception dataset,” in J. Li, “EdgeCooper: Network-aware cooperative LiDAR perception for Proceedings of the IEEE/CVF Conference on Computer Vision and enhanced vehicular awareness,” IEEE Journal on Selected Areas in Pattern Recognition \(CVPR\), June 2024, pp. 22 668–22 677. 

Communications, vol. 42, no. 1, pp. 207–222, January 2024. 

\[298\] R. Hao, S. Fan, Y. Dai, Z. Zhang, C. Li, Y. Wang, H. Yu, W. Yang, 

\[319\] J. Han, Z. Ju, X. Chen, M. Yang, H. Zhang, and R. Huai, “Secure J. Yuan, and Z. Nie, “Rcooper: A real-world large-scale dataset for operations of connected and autonomous vehicles,” IEEE Transactions roadside cooperative perception,” in Proceedings of the IEEE/CVF

on Intelligent Vehicles, vol. 8, no. 11, pp. 4484–4497, November 2023. 

38

\[320\] G. Wilson and D. J. Cook, “A survey of unsupervised deep domain the IEEE/CVF Conference on Computer Vision and Pattern Recognition adaptation,” ACM Transactions on Intelligent Systems and Technology \(CVPR\), 2024. 

\(TIST\), vol. 11, no. 5, pp. 1–46, July 2020. 

\[321\] R. Zhang, D. Meng, L. Bassett, S. Shen, Z. Zou, and H. X. Liu, “Robust roadside perception: an automated data synthesis pipeline minimizing human annotation,” IEEE Transactions on Intelligent Vehicles, pp. 1–

10, 2024, doi:10.1109/TIV.2024.3364977. 

\[322\] Z. Wei, H. Qu, Y. Wang, X. Yuan, H. Wu, Y. Du, K. Han, N. Zhang, and Z. Feng, “Integrated sensing and communication signals toward 5G-A and 6G: A survey,” IEEE Internet of Things Journal, vol. 10, no. 13, pp. 11 068–11 092, July 2023. 

\[323\] L. Xing, P. Zhao, J. Gao, H. Wu, and H. Ma, “A survey of the social internet of vehicles: Secure data issues, solutions, and federated learning,” IEEE Intelligent Transportation Systems Magazine, vol. 15, no. 2, pp. 70–84, April 2023. 

\[324\] L. Barbieri, S. Savazzi, M. Brambilla, and M. Nicoli, “Decentralized federated learning for extended sensing in 6G connected vehicles,” 

Vehicular Communications, vol. 33, January 2022, Art. no. 100396. 

\[325\] Y. Chen, Z. Liu, Y. Zhang, Y. Wu, X. Chen, and L. Zhao, “Deep reinforcement learning-based dynamic resource management for mobile edge computing in industrial internet of things,” IEEE Transactions on Industrial Informatics, vol. 17, no. 7, pp. 4925–4934, July 2021. 

\[326\] A. Vaswani, N. Shazeer, N. Parmar, J. Uszkoreit, L. Jones, A. N. 

Gomez, Ł. Kaiser, and I. Polosukhin, “Attention is all you need,” 

Advances in neural information processing systems, vol. 30, 2017. 

\[327\] T. Meinhardt, A. Kirillov, L. Leal-Taixe, and C. Feichtenhofer, “Track-former: Multi-object tracking with transformers,” in Proceedings of the IEEE/CVF conference on computer vision and pattern recognition, 2022, pp. 8844–8854. 

\[328\] W. Tong, C. Sima, T. Wang, L. Chen, S. Wu, H. Deng, Y. Gu, L. Lu, P. Luo, D. Lin et al., “Scene as occupancy,” in Proceedings of the IEEE/CVF International Conference on Computer Vision, 2023, pp. 

8406–8415. 

\[329\] Y. Wei, L. Zhao, W. Zheng, Z. Zhu, J. Zhou, and J. Lu, “Surroundocc: Multi-camera 3d occupancy prediction for autonomous driving,” in Proceedings of the IEEE/CVF International Conference on Computer Vision, 2023, pp. 21 729–21 740. 

\[330\] B. Yan, Y. Jiang, J. Wu, D. Wang, P. Luo, Z. Yuan, and H. Lu, 

“Universal instance perception as object discovery and retrieval,” in Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition, 2023, pp. 15 325–15 336. 

\[331\] S. Yang, J. Liu, R. Zhang, M. Pan, Z. Guo, X. Li, Z. Chen, P. Gao, Y. Guo, and S. Zhang, “Lidar-llm: Exploring the potential of large language models for 3d lidar understanding,” arXiv preprint arXiv:2312.14074, 2023. 

\[332\] A. Hu, L. Russell, H. Yeo, Z. Murez, G. Fedoseev, A. Kendall, J. Shotton, and G. Corrado, “Gaia-1: A generative world model for autonomous driving,” arXiv preprint arXiv:2309.17080, 2023. 

\[333\] X. Wang, Z. Zhu, G. Huang, X. Chen, and J. Lu, “Drivedreamer: Towards real-world-driven world models for autonomous driving,” 

arXiv preprint arXiv:2309.09777, 2023. 

\[334\] Y. Hu, J. Yang, L. Chen, K. Li, C. Sima, X. Zhu, S. Chai, S. Du, T. Lin, W. Wang et al., “Planning-oriented autonomous driving,” in Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition \(CVPR\), 2023, pp. 17 853–17 862. 

\[335\] J. Gu, C. Hu, T. Zhang, X. Chen, Y. Wang, Y. Wang, and H. Zhao, 

“Vip3d: End-to-end visual trajectory prediction via 3d agent queries,” 

in Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition \(CVPR\), 2023, pp. 5496–5506. 

\[336\] H. Yu, W. Yang, J. Zhong, Z. Yang, S. Fan, P. Luo, and Z. Nie, “End-to-end autonomous driving through v2x cooperation,” arXiv preprint arXiv:2404.00717, 2024. 

\[337\] G. Liu, Y. Hu, C. Xu, W. Mao, J. Ge, Z. Huang, Y. Lu, Y. Xu, J. Xia, Y. Wang et al., “Towards collaborative autonomous driving: Simulation platform and end-to-end system,” 2024, arXiv:2404.09496. 

\[338\] Y. Yan, B. Liu, J. Ai, Q. Li, R. Wan, and J. Pu, “PointSSC: A cooperative vehicle-infrastructure point cloud benchmark for semantic scene completion,” in Proceedings of the IEEE International Conference on Robotics and Automation \(ICRA\), 2024, pp. 17 027–17 034. 

\[339\] C. Chang, J. Zhang, K. Zhang, W. Zhong, X. Peng, S. Li, and L. Li, 

“Bev-v2x: Cooperative birds-eye-view fusion and grid occupancy prediction via v2x-based data sharing,” IEEE Transactions on Intelligent Vehicles, vol. 8, no. 11, pp. 4498–4514, 2023. 

\[340\] R. Song, C. Liang, H. Cao, Z. Yan, W. Zimmer, M. Gross, A. Festag, and A. Knoll, “Collaborative semantic occupancy prediction with hybrid feature fusion in connected automated vehicles,” in Proceedings of



